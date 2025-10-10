# Gráfico de acciones de Alto-Bajo-Cierre {#stockHighLowClose}

Por ejemplo, agregue un Gráfico de acciones de Alto-Bajo-Cierre como este:

<p align="center"><img width="770" src="../images/stock_high_low_close_chart.png" alt="crear un Gráfico de acciones de Alto-Bajo-Cierre con excelize usando el lenguaje Go"></p>

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
        {"Fecha", "Alta", "Baja", "Cierre"},
        {45593, 431.94, 426.3, 426.59},
        {45590, 432.52, 426.57, 428.15},
        {45589, 425.98, 422.4, 424.73},
        {45588, 431.08, 422.53, 424.6},
        {45587, 430.58, 418.04, 427.51},
        {45586, 418.96, 413.75, 418.78},
        {45583, 419.65, 416.26, 418.16},
        {45582, 422.5, 415.59, 416.72},
        {45581, 416.36, 410.48, 416.12},
        {45580, 422.48, 415.26, 418.74},
        {45579, 424.04, 417.52, 419.14},
        {45576, 417.13, 413.25, 416.32},
        {45575, 417.35, 413.15, 415.84},
        {45574, 420.38, 414.3, 417.46},
        {45573, 415.66, 408.17, 414.71},
        {45572, 417.11, 409, 409.54},
        {45569, 419.75, 414.97, 416.06},
        {45568, 419.55, 414.29, 416.54},
        {45567, 422.82, 416.71, 417.13},
        {45566, 428.48, 418.81, 420.69},
        {45565, 430.42, 425.37, 430.3},
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
        Type: excelize.StockHighLowClose,
        Series: []excelize.ChartSeries{
            {
                Name:       "Hoja1!$B$1",
                Categories: "Hoja1!$A$2:$A$22",
                Values:     "Hoja1!$B$2:$B$22",
            },
            {
                Name:       "Hoja1!$C$1",
                Categories: "Hoja1!$A$2:$A$22",
                Values:     "Hoja1!$C$2:$C$22",
            },
            {
                Name:       "Hoja1!$D$1",
                Categories: "Hoja1!$A$2:$A$22",
                Values:     "Hoja1!$D$2:$D$22",
            },
        },
        Legend: excelize.ChartLegend{Position: "none"},
        Title: []excelize.RichTextRun{
            {Text: "Gráfico de acciones de Alto-Bajo-Cierre"},
        },
        XAxis: excelize.ChartAxis{
            NumFmt: excelize.ChartNumFmt{CustomNumFmt: "yyyy-mm-dd"},
        },
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
