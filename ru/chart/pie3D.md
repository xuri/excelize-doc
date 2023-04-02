# 3D круговая диаграмма {#pie3D}

Например, добавьте диаграмму, подобную этой:

<p align="center"><img width="770" src="../images/3d_pie_chart.png" alt="создать 3D круговая диаграмма с Excelize с помощью Go"></p>

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
    if err := f.SetSheetName("Sheet1", "Лист1"); err != nil {
        fmt.Println(err)
        return
    }
    for idx, row := range [][]interface{}{
        {"Яблоко", "Апельсин", "Груша"},
        {2, 3, 3},
    } {
        cell, err := excelize.CoordinatesToCellName(1, idx+1)
        if err != nil {
            fmt.Println(err)
            return
        }
        if err := f.SetSheetRow("Лист1", cell, &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    if err := f.AddChart("Лист1", "E1", &excelize.Chart{
        Type: excelize.Pie3D,
        Series: []excelize.ChartSeries{
            {
                Name:       "количество",
                Categories: "Лист1!$A$1:$C$1",
                Values:     "Лист1!$A$2:$C$2",
            },
        },
        Format: excelize.GraphicOptions{
            OffsetX: 15,
            OffsetY: 10,
        },
        Title: excelize.ChartTitle{
            Name: "3D круговая диаграмма",
        },
        PlotArea: excelize.ChartPlotArea{
            ShowPercent: true,
        },
    }); err != nil {
        fmt.Println(err)
        return
    }
    // Сохранить workbook
    if err := f.SaveAs("Книга1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```
