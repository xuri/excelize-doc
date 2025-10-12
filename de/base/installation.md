# Grundlegende Nutzung

## Installation {#install}

Die folgende Tabelle zeigt die Mindestanforderungen der Go-Sprache für jede veröffentlichte Version von Excelize:

Excelize-Version | Mindestanforderungen für die Go-Sprachversion
---|---
v2.10.0 ~ master | 1.24.0
v2.9.1 | 1.23.0
v2.8.1 ~ v2.9.0 | 1.18
v2.7.0 ~ v2.8.0 | 1.16
v2.4.0 ~ v2.6.1 | 1.15
v2.0.2 ~ v2.3.2 | 1.10
v1.0.0 ~ v2.0.1 | 1.6

Für die Verwendung der neuesten Version Excelize Bibliothek erfordern, um Version 1.24.0 oder höher. Beachten Sie, dass es in Go 1.21.0 einige [inkompatible Änderungen](https://github.com/golang/go/issues/61881) gibt. Diese Bibliothek kann mit dieser Version nicht funktionieren. Wenn Sie Go 1.21.x verwenden, aktualisieren Sie bitte auf Go 1.21.1 und eine spätere Version.

- Installation

```bash
go get github.com/xuri/excelize
```

- Wenn Ihre Paketverwaltung mit [Go Modules](https://go.dev/blog/using-go-modules), installieren Sie bitte mit dem folgenden Befehl.

```bash
go get github.com/xuri/excelize/v2
```

## Upgrade {#update}

- Upgrade auf die neueste stabile Version

```bash
go get -u github.com/xuri/excelize/v2
```

- Upgrade auf den neuesten Code des Entwicklungszweigs

```bash
go get -u github.com/xuri/excelize/v2@master
```

## Erstellen einer Kalkulationstabelle {#NewFile}

Hier ist eine minimale Beispielverwendung, die eine Tabellenkalkulationsdatei erstellt:

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    // Erstellen eines neuen Arbeitsblatts.
    index, err := f.NewSheet("Sheet2")
    if err != nil {
        fmt.Println(err)
        return
    }
    // Festlegen des Wertes einer Zelle.
    f.SetCellValue("Sheet2", "A2", "Hello world.")
    f.SetCellValue("Sheet1", "B2", 100)
    // Aktives Arbeitsblatt der Arbeitsmappe festlegen.
    f.SetActiveSheet(index)
    // Speichern Sie die Tabelle unter dem angegebenen Pfad.
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Tabellenkalkulation lesen {#read}

Im Folgenden wird das Nackte zum Lesen eines Tabellendokuments dargestellt:

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f, err := excelize.OpenFile("Book1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    // Abrufen von Wert aus der Zelle durch angegebenen Arbeitsblattnamen und Achse.
    cell, err := f.GetCellValue("Sheet1", "B2")
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(cell)
    // Abrufen aller Zeilen im Sheet1.
    rows, err := f.GetRows("Sheet1")
    if err != nil {
        fmt.Println(err)
        return
    }
    for _, row := range rows {
        for _, colCell := range row {
            fmt.Print(colCell, "\t")
        }
        fmt.Println()
    }
}
```

## Hinzufügen eines Diagramms zur Tabellenkalkulation {#chart}

Mit Excelize Diagrammgenerierung und -verwaltung ist so einfach wie ein paar Zeilen Quellcode. Sie können Diagramme basierend auf Daten in Ihrem Arbeitsblatt erstellen oder Diagramme ohne Daten in Ihrem Arbeitsblatt generieren.

<p align="center"><img width="770" src="../images/base.png" alt="Hinzufügen eines Diagramms zur Tabellenkalkulation"></p>

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    for idx, row := range [][]interface{}{
        {nil, "Apfel", "Orange", "Birne"}, {"Klein", 2, 3, 3},
        {"Normal", 5, 2, 4}, {"Groß", 6, 7, 8},
    } {
        cell, err := excelize.CoordinatesToCellName(1, idx+1)
        if err != nil {
            fmt.Println(err)
            return
        }
        f.SetSheetRow("Sheet1", cell, &row)
    }
    if err := f.AddChart("Sheet1", "E1", &excelize.Chart{
        Type: excelize.Col3DClustered,
        Series: []excelize.ChartSeries{
            {
                Name:       "Sheet1!$A$2",
                Categories: "Sheet1!$B$1:$D$1",
                Values:     "Sheet1!$B$2:$D$2",
            },
            {
                Name:       "Sheet1!$A$3",
                Categories: "Sheet1!$B$1:$D$1",
                Values:     "Sheet1!$B$3:$D$3",
            },
            {
                Name:       "Sheet1!$A$4",
                Categories: "Sheet1!$B$1:$D$1",
                Values:     "Sheet1!$B$4:$D$4",
            }},
        Title: []excelize.RichTextRun{
            {
                Text: "3D Cluster-Säulendiagramm",
            },
        },
    }); err != nil {
        fmt.Println(err)
        return
    }
    // Speichern Sie die Tabelle unter dem angegebenen Pfad.
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Hinzufügen eines Bildes zur Tabellenkalkulation {#image}

```go
package main

import (
    "fmt"
    _ "image/gif"
    _ "image/jpeg"
    _ "image/png"

    "github.com/xuri/excelize/v2"
)

func main() {
    f, err := excelize.OpenFile("Book1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    // Fügen Sie ein Bild ein.
    if err := f.AddPicture("Sheet1", "A2", "image.png", nil); err != nil {
        fmt.Println(err)
        return
    }
    // Fügen Sie ein Bild mit Skalierung in ein Arbeitsblatt ein.
    if err := f.AddPicture("Sheet1", "D2", "image.jpg",
        &excelize.GraphicOptions{ScaleX: 0.5, ScaleY: 0.5}); err != nil {
        fmt.Println(err)
        return
    }
    // Fügen Sie mit Druckunterstützung einen Bildversatz in die Zelle ein.
    enable, disable := true, false
    if err := f.AddPicture("Sheet1", "H2", "image.gif",
        &excelize.GraphicOptions{
            PrintObject:     &enable,
            LockAspectRatio: false,
            OffsetX:         15,
            OffsetY:         10,
            Locked:          &disable,
        }); err != nil {
        fmt.Println(err)
        return
    }
    // Speichern Sie die Tabellenkalkulationsdatei mit dem Ursprungspfad.
    if err = f.Save(); err != nil {
        fmt.Println(err)
    }
}
```
