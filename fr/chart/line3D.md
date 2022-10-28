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
    categories := map[string]string{
        "A2": "Small", "A3": "Normal", "A4": "Large", "B1": "Apple", "C1": "Orange", "D1": "Pear"}
    values := map[string]int{
        "B2": 2, "C2": 3, "D2": 3, "B3": 5, "C3": 2, "D3": 4, "B4": 6, "C4": 7, "D4": 8}
    f := excelize.NewFile()
    f.SetSheetName("Sheet1", "Feuil1")
    for k, v := range categories {
        f.SetCellValue("Feuil1", k, v)
    }
    for k, v := range values {
        f.SetCellValue("Feuil1", k, v)
    }
    if err := f.AddChart("Feuil1", "E1", `{
        "type": "line3D",
        "series": [
        {
            "name": "Feuil1!$A$2",
            "categories": "Feuil1!$B$1:$D$1",
            "values": "Feuil1!$B$2:$D$2"
        },
        {
            "name": "Feuil1!$A$3",
            "categories": "Feuil1!$B$1:$D$1",
            "values": "Feuil1!$B$3:$D$3"
        },
        {
            "name": "Feuil1!$A$4",
            "categories": "Feuil1!$B$1:$D$1",
            "values": "Feuil1!$B$4:$D$4"
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
            "name": "Graphique en courbes 3D"
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
    // Enregistrer le classeur
    if err := f.SaveAs("Classeur1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```
