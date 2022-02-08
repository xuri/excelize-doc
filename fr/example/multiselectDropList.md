# Liste déroulante à sélection multiple

Créez une liste déroulante à sélection multiple sans VBA dans la feuille de calcul avec Excelize en utilisant Go:

<p align="center"><img width="426" src="../images/multiselect_drop_list.gif" alt="Créez une liste déroulante à sélection multiple sans VBA dans la feuille de calcul avec Excelize en utilisant Go"></p>

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    // créer une nouvelle feuille de calcul
    f := excelize.NewFile()
    var (
        sheetName = "Sheet1"
        selection = []string{"red", "blue", "green", "yellow"}
        // valeurs de cellule
        data = [][]interface{}{
            {"Element", "Picklist", nil, "Select below"},
            {selection[0] + " "},
            {selection[1] + " "},
            {selection[2] + " "},
            {selection[3] + " "},
        }
        cell string
        err  error
    )
    // définir chaque valeur de cellule
    for r, row := range data {
        if cell, err = excelize.JoinCellName("A", r+1); err != nil {
            fmt.Println(err)
            return
        }
        if err = f.SetSheetRow(sheetName, cell, &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    // définir le nom défini
    for index, value := range selection {
        if cell, err = excelize.CoordinatesToCellName(1, index+2, true); err != nil {
            fmt.Println(err)
            return
        }
        if err = f.SetDefinedName(&excelize.DefinedName{
            Name:     value,
            RefersTo: fmt.Sprintf("%s!%s", sheetName, cell),
            Scope:    sheetName,
        }); err != nil {
            fmt.Println(err)
            return
        }
        if cell, err = excelize.CoordinatesToCellName(2, index+2); err != nil {
            fmt.Println(err)
            return
        }
        formula := fmt.Sprintf("=IF(ISNUMBER(FIND(%s,D2)),\"\",D2&%s)", value, value)
        if err := f.SetCellFormula(sheetName, cell, formula); err != nil {
            fmt.Println(err)
            return
        }
    }
    // définir la validation des données
    dvRange := excelize.NewDataValidation(true)
    dvRange.Sqref = "D2:D2"
    dvRange.SetSqrefDropList("$B$2:$B$5")
    if err = f.AddDataValidation(sheetName, dvRange); err != nil {
        fmt.Println(err)
        return
    }
    // définir la largeur de colonne personnalisée
    for col, width := range map[string]float64{"A": 10, "B": 18, "D": 18} {
        if err = f.SetColWidth(sheetName, col, col, width); err != nil {
            fmt.Println(err)
            return
        }
    }
    // créer un tableau
    if err = f.AddTable(sheetName, "A1", "B5", `{
        "table_name": "table",
        "table_style": "TableStyleMedium2"
    }`); err != nil {
        fmt.Println(err)
        return
    }
    // enregistrer le fichier de feuille de calcul
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```
