# Gráfico de rosquillas {#doughnut}

Por ejemplo, agregue un Gráfico de rosquillas como este:

<p align="center"><img width="771" src="../images/doughnut_chart.png" alt="crear un Gráfico de rosquillas con excelize usando el lenguaje Go"></p>

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    categories := map[string]string{"A1": "Manzana", "B1": "Naranja", "C1": "Pera"}
    values := map[string]int{"A2": 2, "B2": 3, "C2": 3}
    f := excelize.NewFile()
    f.SetSheetName("Sheet1", "Hoja1")
    for k, v := range categories {
        f.SetCellValue("Hoja1", k, v)
    }
    for k, v := range values {
        f.SetCellValue("Hoja1", k, v)
    }
    if err := f.AddChart("Hoja1", "E1", `{
        "type": "doughnut",
        "series": [
        {
            "name": "Hoja1!$A$2",
            "categories": "Hoja1!$A$1:$C$1",
            "values": "Hoja1!$A$2:$C$2"
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
            "position": "right",
            "show_legend_key": false
        },
        "title":
        {
            "name": "Gráfico de rosquillas"
        },
        "plotarea":
        {
            "show_bubble_size": false,
            "show_cat_name": false,
            "show_leader_lines": false,
            "show_percent": true,
            "show_series_name": false,
            "show_val": false
        },
        "show_blanks_as": "zero"
    }`); err != nil {
        fmt.Println(err)
    }
    // Guarde la hoja de cálculo por la ruta dada.
    if err := f.SaveAs("Libro1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```
