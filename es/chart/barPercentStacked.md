# Gráfico de barras 2D 100% apilado {#barPercentStacked}

Por ejemplo, agregue un Gráfico de barras 2D 100% apilado como este:

<p align="center"><img width="771" src="../images/2d_percent_stacked_bar_chart.png" alt="crear un Gráfico de barras 2D 100% apilado con excelize usando el lenguaje Go"></p>

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
    if err := f.SetSheetName("Sheet1", "Hoja1"); err != nil {
        fmt.Println(err)
        return
    }
    for idx, row := range [][]interface{}{
        {nil, "Manzana", "Naranja", "Pera"},
        {"Pequeño", 2, 3, 3},
        {"Normal", 5, 2, 4},
        {"Grande", 6, 7, 8},
    } {
        cell, err := excelize.CoordinatesToCellName(1, idx+1)
        if err != nil {
            fmt.Println(err)
            return
        }
        if err := f.SetSheetRow("Hoja1", cell, &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    if err := f.AddChart("Hoja1", "E1", &excelize.Chart{
        Type: excelize.BarPercentStacked,
        Series: []excelize.ChartSeries{
            {
                Name:       "Hoja1!$A$2",
                Categories: "Hoja1!$B$1:$D$1",
                Values:     "Hoja1!$B$2:$D$2",
            },
            {
                Name:       "Hoja1!$A$3",
                Categories: "Hoja1!$B$1:$D$1",
                Values:     "Hoja1!$B$3:$D$3",
            },
            {
                Name:       "Hoja1!$A$4",
                Categories: "Hoja1!$B$1:$D$1",
                Values:     "Hoja1!$B$4:$D$4",
            },
        },
        Format: excelize.GraphicOptions{
            OffsetX: 15,
            OffsetY: 10,
        },
        Legend: excelize.ChartLegend{
            Position: "left",
        },
        Title: []excelize.RichTextRun{
            {
                Text: "Gráfico de barras 2D 100% apilado",
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
    // Guarde la hoja de cálculo por la ruta dada.
    if err := f.SaveAs("Libro1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```
