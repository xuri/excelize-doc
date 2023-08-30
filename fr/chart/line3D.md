# Graphique en ligne 3D {#line}

Par exemple, ajoutez un graphique qui ressemble à ceci:

<p align="center"><img width="770" src="../images/3d_line_chart.png" alt="créer graphique en ligne 3D avec excelize en utilisant Go"></p>

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
    if err := f.SetSheetName("Sheet1", "Feuil1"); err != nil {
        fmt.Println(err)
        return
    }
    for idx, row := range [][]interface{}{
        {nil, "Apple", "Orange", "Pear"},
        {"Small", 2, 3, 3},
        {"Normal", 5, 2, 4},
        {"Large", 6, 7, 8},
    } {
        cell, err := excelize.CoordinatesToCellName(1, idx+1)
        if err != nil {
            fmt.Println(err)
            return
        }
        if err := f.SetSheetRow("Feuil1", cell, &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    if err := f.AddChart("Feuil1", "E1", &excelize.Chart{
        Type: excelize.Line3D,
        Series: []excelize.ChartSeries{
            {
                Name:       "Feuil1!$A$2",
                Categories: "Feuil1!$B$1:$D$1",
                Values:     "Feuil1!$B$2:$D$2",
            },
            {
                Name:       "Feuil1!$A$3",
                Categories: "Feuil1!$B$1:$D$1",
                Values:     "Feuil1!$B$3:$D$3",
            },
            {
                Name:       "Feuil1!$A$4",
                Categories: "Feuil1!$B$1:$D$1",
                Values:     "Feuil1!$B$4:$D$4",
            },
        },
        Format: excelize.GraphicOptions{
            OffsetX: 15,
            OffsetY: 10,
        },
        Legend: excelize.ChartLegend{
            Position: "top",
        },
        Title: []excelize.RichTextRun{
            {
                Text: "Graphique en courbes 3D",
            },
        },
        PlotArea: excelize.ChartPlotArea{
            ShowCatName:     false,
            ShowLeaderLines: false,
            ShowPercent:     false,
            ShowSerName:     false,
            ShowVal:         false,
        },
        ShowBlanksAs: "zero",
    }); err != nil {
        fmt.Println(err)
        return
    }
    // Enregistrer le classeur
    if err := f.SaveAs("Classeur1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```
