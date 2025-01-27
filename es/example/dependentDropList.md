# Lista desplegable dependiente

Cree una lista desplegable dependiente en la hoja de cálculo con Excelize usando Go::

<p align="center"><img width="375" src="../images/dependent_drop_list.gif" alt="Cree una lista desplegable dependiente en la hoja de cálculo con Excelize usando Go"></p>

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    // crear una nueva hoja de cálculo
    f := excelize.NewFile()
    var (
        // valores de celda
        data = [][]interface{}{
            {"Fruits", "Vegetables"},
            {"Mango", "Potato", nil, "Drop Down 1", "Drop Down 2"},
            {"Apple", "Tomato"},
            {"Grapes", "Spinach"},
            {"Strawberry", "Onion"},
            {"Kiwi", "Cucumber"},
        }
        addr                    string
        err                     error
        cellsStyle, headerStyle int
    )
    // establecer cada valor de celda
    for r, row := range data {
        if addr, err = excelize.JoinCellName("A", r+1); err != nil {
            fmt.Println(err)
            return
        }
        if err = f.SetSheetRow("Sheet1", addr, &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    // establecer validación de datos
    dvRange1 := excelize.NewDataValidation(true)
    dvRange1.Sqref = "D3:D3"
    dvRange1.SetSqrefDropList("$A$1:$B$1")
    if err = f.AddDataValidation("Sheet1", dvRange1); err != nil {
        fmt.Println(err)
        return
    }
    dvRange2 := excelize.NewDataValidation(true)
    dvRange2.Sqref = "E3:E3"
    dvRange2.SetSqrefDropList("INDIRECT(D3)")
    if err = f.AddDataValidation("Sheet1", dvRange2); err != nil {
        fmt.Println(err)
        return
    }
    // establecer nombre definido
    if err = f.SetDefinedName(&excelize.DefinedName{
        Name:     "Fruits",
        RefersTo: "Sheet1!$A$2:$A$6",
        Scope:    "Sheet1",
    }); err != nil {
        fmt.Println(err)
        return
    }
    if err = f.SetDefinedName(&excelize.DefinedName{
        Name:     "Vegetables",
        RefersTo: "Sheet1!$B$2:$B$6",
        Scope:    "Sheet1",
    }); err != nil {
        fmt.Println(err)
        return
    }
    // establecer ancho de columna personalizado
    for col, width := range map[string]float64{
        "A": 12, "B": 12, "C": 6, "D": 12, "E": 12} {
        if err = f.SetColWidth("Sheet1", col, col, width); err != nil {
            fmt.Println(err)
            return
        }
    }
    // ocultar líneas de cuadrícula para la hoja de trabajo
    disable := false
    if err := f.SetSheetView("Sheet1", -1, &excelize.ViewOptions{
        ShowGridLines: &disable,
    }); err != nil {
        fmt.Println(err)
    }
    // definir el estilo del borde
    border := []excelize.Border{
        {Type: "top", Style: 1, Color: "CCCCCC"},
        {Type: "left", Style: 1, Color: "CCCCCC"},
        {Type: "right", Style: 1, Color: "CCCCCC"},
        {Type: "bottom", Style: 1, Color: "CCCCCC"},
    }
    // definir el estilo de las celdas
    if cellsStyle, err = f.NewStyle(&excelize.Style{
        Font:   &excelize.Font{Color: "333333"},
        Border: border}); err != nil {
        fmt.Println(err)
        return
    }
    // definir el estilo de la fila del encabezado
    if headerStyle, err = f.NewStyle(&excelize.Style{
        Font: &excelize.Font{Bold: true},
        Fill: excelize.Fill{
            Type: "pattern", Color: []string{"DAE9F3"}, Pattern: 1},
        Border: border},
    ); err != nil {
        fmt.Println(err)
        return
    }
    // establecer estilo de celda
    if err = f.SetCellStyle("Sheet1", "A2", "B6", cellsStyle); err != nil {
        fmt.Println(err)
        return
    }
    if err = f.SetCellStyle("Sheet1", "D3", "E3", cellsStyle); err != nil {
        fmt.Println(err)
        return
    }
    // establecer el estilo de celda para la fila del encabezado
    if err = f.SetCellStyle("Sheet1", "A1", "B1", headerStyle); err != nil {
        fmt.Println(err)
        return
    }
    if err = f.SetCellStyle("Sheet1", "D2", "E2", headerStyle); err != nil {
        fmt.Println(err)
        return
    }
    // guardar archivo de hoja de cálculo
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```
