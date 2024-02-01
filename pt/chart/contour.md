# Gráfico de contorno {#contour}

Por exemplo, adicione um gráfico de contorno como este:

<p align="center"><img width="770" src="../images/contour_chart.png" alt="crie gráfico de contorno com Excelize usando Go"></p>

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
    if err := f.SetSheetName("Sheet1", "Planilha1"); err != nil {
        fmt.Println(err)
        return
    }
    for idx, row := range [][]interface{}{
        {nil, "Maçã", "Laranja", "Pera"},
        {"Pequeno", 7, 7, 8},
        {"Normal", 5, 4, 4},
        {"Grande", 2, 3, 3},
    } {
        cell, err := excelize.CoordinatesToCellName(1, idx+1)
        if err != nil {
            fmt.Println(err)
            return
        }
        if err := f.SetSheetRow("Planilha1", cell, &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    if err := f.AddChart("Planilha1", "E1", &excelize.Chart{
        Type: excelize.Contour,
        Series: []excelize.ChartSeries{
            {
                Name:       "Planilha1!$A$2",
                Categories: "Planilha1!$B$1:$D$1",
                Values:     "Planilha1!$B$2:$D$2",
            },
            {
                Name:       "Planilha1!$A$3",
                Categories: "Planilha1!$B$1:$D$1",
                Values:     "Planilha1!$B$3:$D$3",
            },
            {
                Name:       "Planilha1!$A$4",
                Categories: "Planilha1!$B$1:$D$1",
                Values:     "Planilha1!$B$4:$D$4",
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
                Text: "gráfico de contorno",
            },
        },
    }); err != nil {
        fmt.Println(err)
        return
    }
    // Salva a pasta de trabalho
    if err := f.SaveAs("Pasta1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```
