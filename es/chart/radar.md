# Gráfico de radar {#radar}

Por ejemplo, agregue un Gráfico de radar como este:

<p align="center"><img width="771" src="../images/radar_chart.png" alt="crear un Gráfico de radar con excelize usando el lenguaje Go"></p>

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    categories := map[string]string{
        "A2": "Pequeño", "A3": "Normal", "A4": "Grande", "B1": "Manzana", "C1": "Naranja", "D1": "Pera"}
    values := map[string]int{
        "B2": 2, "C2": 3, "D2": 3, "B3": 5, "C3": 2, "D3": 4, "B4": 6, "C4": 7, "D4": 8}
    f := excelize.NewFile()
    f.SetSheetName("Sheet1", "Hoja1")
    for k, v := range categories {
        f.SetCellValue("Hoja1", k, v)
    }
    for k, v := range values {
        f.SetCellValue("Hoja1", k, v)
    }
    if err := f.AddChart("Hoja1", "E1", `{
        "type": "radar",
        "series": [
        {
            "name": "Hoja1!$A$2",
            "categories": "Hoja1!$B$1:$D$1",
            "values": "Hoja1!$B$2:$D$2"
        },
        {
            "name": "Hoja1!$A$3",
            "categories": "Hoja1!$B$1:$D$1",
            "values": "Hoja1!$B$3:$D$3"
        },
        {
            "name": "Hoja1!$A$4",
            "categories": "Hoja1!$B$1:$D$1",
            "values": "Hoja1!$B$4:$D$4"
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
            "name": "Gráfico de radar"
        },
        "plotarea":
        {
            "show_bubble_size": true,
            "show_cat_name": false,
            "show_leader_lines": false,
            "show_percent": true,
            "show_series_name": false,
            "show_val": false
        },
        "show_blanks_as": "span"
    }`); err != nil {
        fmt.Println(err)
    }
    // Guarde la hoja de cálculo por la ruta dada.
    if err := f.SaveAs("Libro1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```
