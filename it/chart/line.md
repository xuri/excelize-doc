# Grafico a linee {#line}

Ad esempio, aggiungi un grafico a linee come questo:

<p align="center"><img width="769" src="../images/line_chart.png" alt="crea un grafico a linee con Excelize utilizzando Go"></p>

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
    if err := f.SetSheetName("Sheet1", "Foglio1"); err != nil {
        fmt.Println(err)
        return
    }
    for idx, row := range [][]interface{}{
        {nil, "Mela", "Arancia", "Pera"},
        {"Piccolo", 2, 3, 3},
        {"Normale", 5, 2, 4},
        {"Grande", 6, 7, 8},
    } {
        cell, err := excelize.CoordinatesToCellName(1, idx+1)
        if err != nil {
            fmt.Println(err)
            return
        }
        if err := f.SetSheetRow("Foglio1", cell, &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    if err := f.AddChart("Foglio1", "E1", &excelize.Chart{
        Type: excelize.Line,
        Series: []excelize.ChartSeries{
            {
                Name:       "Foglio1!$A$2",
                Categories: "Foglio1!$B$1:$D$1",
                Values:     "Foglio1!$B$2:$D$2",
                Line: excelize.ChartLine{
                    Smooth: true,
                },
            },
            {
                Name:       "Foglio1!$A$3",
                Categories: "Foglio1!$B$1:$D$1",
                Values:     "Foglio1!$B$3:$D$3",
                Line: excelize.ChartLine{
                    Smooth: true,
                },
            },
            {
                Name:       "Foglio1!$A$4",
                Categories: "Foglio1!$B$1:$D$1",
                Values:     "Foglio1!$B$4:$D$4",
                Line: excelize.ChartLine{
                    Smooth: true,
                },
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
                Text: "Grafico a linee",
            },
        },
        PlotArea: excelize.ChartPlotArea{
            ShowCatName:     false,
            ShowLeaderLines: false,
            ShowPercent:     true,
            ShowSerName:     true,
            ShowVal:         true,
        },
        ShowBlanksAs: "zero",
    }); err != nil {
        fmt.Println(err)
        return
    }
    // Salva cartella di lavoro
    if err := f.SaveAs("Cartel1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```
