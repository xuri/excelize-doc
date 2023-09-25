# Pivot-Tabelle {#PivotTable}

Eine Pivot-Tabelle ist eine Statistiktabelle, in der die Daten einer umfangreicheren Tabelle (z. B. aus einer Datenbank, einer Tabelle oder einem Business Intelligence-Programm) zusammengefasst sind. Diese Zusammenfassung kann Summen, Durchschnittswerte oder andere Statistiken enthalten, die in der Pivot-Tabelle auf sinnvolle Weise zusammengefasst werden.

`PivotTableOptions` ordnet die Formateinstellungen der Pivot-Tabelle direkt zu.

```go
type PivotTableOptions struct {
    DataRange           string
    PivotTableRange     string
    Rows                []PivotTableField
    Columns             []PivotTableField
    Data                []PivotTableField
    Filter              []PivotTableField
    RowGrandTotals      bool
    ColGrandTotals      bool
    ShowDrill           bool
    UseAutoFormatting   bool
    PageOverThenDown    bool
    MergeItem           bool
    CompactData         bool
    ShowError           bool
    ShowRowHeaders      bool
    ShowColHeaders      bool
    ShowRowStripes      bool
    ShowColStripes      bool
    ShowLastColumn      bool
    PivotTableStyleName string
    // enthält gefilterte oder nicht exportierte Felder
}
```

`PivotTableStyleName`: Die integrierten Stilnamen für Pivot-Tabellen:

```text
PivotStyleLight1 - PivotStyleLight28
PivotStyleMedium1 - PivotStyleMedium28
PivotStyleDark1 - PivotStyleDark28
```

`PivotTableField` ordnet die Feldeinstellungen der Pivot-Tabelle direkt zu.

```go
type PivotTableField struct {
    Compact         bool
    Data            string
    Name            string
    Outline         bool
    Subtotal        string
    DefaultSubtotal bool
}
```

`Subtotal` gibt die Aggregationsfunktion an, die für dieses Datenfeld gilt. Der Standardwert ist `Sum`. Die möglichen Werte für dieses Attribut sind:

|Optionaler Wert|
|---|
|Average|
|Count|
|CountNums|
|Max|
|Min|
|Product|
|StdDev|
|StdDevp|
|Sum|
|Var|
|Varp|

`Name` gibt den Namen des Datenfelds an. Im Namen des Datenfelds sind maximal `255` Zeichen zulässig, überschüssige Zeichen werden abgeschnitten.

## Erstellen einer Pivot-Tabelle {#AddPivotTable}

```go
func (f *File) AddPivotTable(opts *PivotTableOptions) error
```

AddPivotTable bietet die Methode zum Hinzufügen einer Pivot-Tabelle anhand der angegebenen Pivot-Tabellenoptionen.

Erstellen Sie beispielsweise eine Pivot-Tabelle im Bereich `Sheet1!$G$2:$M$34` mit der Region `Sheet1!$A$1:$E$31` als Datenquelle, zusammengefasst nach Umsatzsumme:

<p align="center"><img width="1139" src="./images/pivot_table_01.png" alt="Erstellen Sie eine Pivot-Tabelle mit Excelize mit Go"></p>

```go
package main

import (
    "fmt"
    "math/rand"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    // Erstellen Sie einige Daten in einem Arbeitsblatt
    month := []string{"Januar", "Februar", "März", "April", "Kann",
        "Juni", "Juli", "August", "September", "Oktober", "November", "Dezember"}
    year := []int{2017, 2018, 2019}
    types := []string{"Fleisch", "Molkerei", "Beverages", "Getränke"}
    region := []string{"Osten", "Westen", "Norden", "Süden"}
    f.SetSheetRow("Sheet1", "A1", &[]string{"Monat", "Jahr", "Art", "Der Umsatz", "Region"})
    for row := 2; row < 32; row++ {
        f.SetCellValue("Sheet1", fmt.Sprintf("A%d", row), month[rand.Intn(12)])
        f.SetCellValue("Sheet1", fmt.Sprintf("B%d", row), year[rand.Intn(3)])
        f.SetCellValue("Sheet1", fmt.Sprintf("C%d", row), types[rand.Intn(4)])
        f.SetCellValue("Sheet1", fmt.Sprintf("D%d", row), rand.Intn(5000))
        f.SetCellValue("Sheet1", fmt.Sprintf("E%d", row), region[rand.Intn(4)])
    }
    if err := f.AddPivotTable(&excelize.PivotTableOptions{
        DataRange:       "Sheet1!$A$1:$E$31",
        PivotTableRange: "Sheet1!$G$2:$M$34",
        Rows: []excelize.PivotTableField{
            {Data: "Monat", DefaultSubtotal: true}, {Data: "Jahr"}},
        Filter: []excelize.PivotTableField{
            {Data: "Region"}},
        Columns: []excelize.PivotTableField{
            {Data: "Type", DefaultSubtotal: true}},
        Data: []excelize.PivotTableField{
            {Data: "Der Umsatz", Name: "Zusammenfassen", Subtotal: "Sum"}},
        RowGrandTotals: true,
        ColGrandTotals: true,
        ShowDrill:      true,
        ShowRowHeaders: true,
        ShowColHeaders: true,
        ShowLastColumn: true,
    }); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("Mappe1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Holen Sie sich Pivot-Tabellen {#GetPivotTables}

```go
func (f *File) GetPivotTables(sheet string) ([]PivotTableOptions, error)
```

GetPivotTables gibt alle Pivot-Tabellendefinitionen in einem Arbeitsblatt nach dem angegebenen Arbeitsblattnamen zurück.
