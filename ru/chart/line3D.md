# Трехмерная линейная диаграмма {#line3D}

Например, добавьте диаграмму, подобную этой:

<p align="center"><img width="770" src="../images/3d_line_chart.png" alt="создать Трехмерная линейная диаграмма с Excelize с помощью Go"></p>

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    categories := map[string]string{
        "A2": "Small", "A3": "Normal", "A4": "Large", "B1": "Apple", "C1": "Orange", "D1": "Pear"}
    values := map[string]int{
        "B2": 2, "C2": 3, "D2": 3, "B3": 5, "C3": 2, "D3": 4, "B4": 6, "C4": 7, "D4": 8}
    f := excelize.NewFile()
    f.SetSheetName("Sheet1", "Лист1")
    for k, v := range categories {
        f.SetCellValue("Лист1", k, v)
    }
    for k, v := range values {
        f.SetCellValue("Лист1", k, v)
    }
    if err := f.AddChart("Лист1", "E1", `{
        "type": "line3D",
        "series": [
        {
            "name": "Лист1!$A$2",
            "categories": "Лист1!$B$1:$D$1",
            "values": "Лист1!$B$2:$D$2"
        },
        {
            "name": "Лист1!$A$3",
            "categories": "Лист1!$B$1:$D$1",
            "values": "Лист1!$B$3:$D$3"
        },
        {
            "name": "Лист1!$A$4",
            "categories": "Лист1!$B$1:$D$1",
            "values": "Лист1!$B$4:$D$4"
        }],
        "format":
        {
            "x_scale": 1.0,
            "y_scale": 1.0,
            "x_offset": 15,
            "y_offset": 10,
            "print_obj": true,
            "lock_aspect_ratio": false,
            "locked": false
        },
        "legend":
        {
            "position": "top",
            "show_legend_key": false
        },
        "title":
        {
            "name": "Трехмерная линейная диаграмма"
        },
        "plotarea":
        {
            "show_bubble_size": false,
            "show_cat_name": false,
            "show_leader_lines": false,
            "show_percent": false,
            "show_series_name": false,
            "show_val": false
        },
        "show_blanks_as": "zero"
    }`); err != nil {
        fmt.Println(err)
    }
    // Сохранить workbook
    if err := f.SaveAs("Книга1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```
