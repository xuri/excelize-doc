# Tableau croisé dynamique {#PivotTable}

Un tableau croisé dynamique est un tableau de statistiques qui résume les données d'un tableau plus détaillé (tel qu'une base de données, un tableur ou un programme d'aide à la décision). Ce résumé peut inclure des sommes, des moyennes ou d’autres statistiques que le tableau croisé dynamique regroupe de manière significative.

PivotTableOptions mappe directement les paramètres de format du tableau croisé dynamique.

```go
type PivotTableOptions struct {
    pivotTableSheetName string
    DataRange           string            `json:"data_range"`
    PivotTableRange     string            `json:"pivot_table_range"`
    Rows                []PivotTableField `json:"rows"`
    Columns             []PivotTableField `json:"columns"`
    Data                []PivotTableField `json:"data"`
    Filter              []PivotTableField `json:"filter"`
    RowGrandTotals      bool              `json:"row_grand_totals"`
    ColGrandTotals      bool              `json:"col_grand_totals"`
    ShowDrill           bool              `json:"show_drill"`
    UseAutoFormatting   bool              `json:"use_auto_formatting"`
    PageOverThenDown    bool              `json:"page_over_then_down"`
    MergeItem           bool              `json:"merge_item"`
    CompactData         bool              `json:"compact_data"`
    ShowError           bool              `json:"show_error"`
    ShowRowHeaders      bool              `json:"show_row_headers"`
    ShowColHeaders      bool              `json:"show_col_headers"`
    ShowRowStripes      bool              `json:"show_row_stripes"`
    ShowColStripes      bool              `json:"show_col_stripes"`
    ShowLastColumn      bool              `json:"show_last_column"`
    PivotTableStyleName string            `json:"pivot_table_style_name"`
    // contains filtered or unexported fields
}
```

`PivotTableStyleName`: Les noms de style de tableau croisé dynamique intégrés:

```text
PivotStyleLight1 - PivotStyleLight28
PivotStyleMedium1 - PivotStyleMedium28
PivotStyleDark1 - PivotStyleDark28
```

PivotTableField mappe directement les paramètres de champ du tableau croisé dynamique.

```go
type PivotTableField struct {
    Compact         bool   `json:"compact"`
    Data            string `json:"data"`
    Name            string `json:"name"`
    Outline         bool   `json:"outline"`
    Subtotal        string `json:"subtotal"`
    DefaultSubtotal bool   `json:"default_subtotal"`
}
```

Subtotal spécifie la fonction d'agrégation qui s'applique à ce champ de données. La valeur par défaut est `Sum`. Les valeurs possibles pour cet attribut sont:

|Valeur facultative|
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

Name spécifie le nom du champ de données. Un maximum de `255` caractères est autorisé dans le nom du champ de données, les caractères en excès seront tronqués.

## Créer un tableau croisé dynamique {#AddPivotTable}

```go
func (f *File) AddPivotTable(opts *PivotTableOptions) error
```

AddPivotTable fournit la méthode pour ajouter un tableau croisé dynamique en fonction des options de tableau croisé dynamique données.

Par exemple, créez un tableau croisé dynamique dans la zone `Sheet1!$G$2:$M$34` avec la région `Sheet1!$A$1:$E$31` comme source de données, récapitulez par somme pour les ventes:

<p align="center"><img width="1117" src="./images/pivot_table_01.png" alt="créer un tableau croisé dynamique avec excelize en utilisant Go"></p>

```go
package main

import (
    "fmt"
    "math/rand"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    // Créer des données dans une feuille
    month := []string{"Jan", "Feb", "Mar", "Apr", "May",
        "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"}
    year := []int{2017, 2018, 2019}
    types := []string{"Meat", "Dairy", "Beverages", "Produce"}
    region := []string{"East", "West", "North", "South"}
    f.SetSheetRow("Sheet1", "A1", &[]string{"Month", "Year", "Type", "Sales", "Region"})
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
            {Data: "Month", DefaultSubtotal: true}, {Data: "Year"}},
        Filter: []excelize.PivotTableField{
            {Data: "Region"}},
        Columns: []excelize.PivotTableField{
            {Data: "Type", DefaultSubtotal: true}},
        Data: []excelize.PivotTableField{
            {Data: "Sales", Name: "Summarize", Subtotal: "Sum"}},
        RowGrandTotals: true,
        ColGrandTotals: true,
        ShowDrill:      true,
        ShowRowHeaders: true,
        ShowColHeaders: true,
        ShowLastColumn: true,
    }); err != nil {
        fmt.Println(err)
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```
