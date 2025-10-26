# Gráfico de ações Abertura-Máxima-Mínima-Fechamento {#stockOpenHighLowClose}

Por exemplo, adicione um Gráfico de ações Abertura-Máxima-Mínima-Fechamento semelhante a este:

<p align="center"><img width="823" src="../images/stock_open_high_low_close_chart.png" alt="crie um Gráfico de ações Abertura-Máxima-Mínima-Fechamento com Excelize usando Go"></p>

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
        {"Data", "Abertura", "Alto", "Baixo", "Fechamento"},
        {45593, 431.66, 431.94, 426.3, 426.59},
        {45590, 426.76, 432.52, 426.57, 428.15},
        {45589, 425.33, 425.98, 422.4, 424.73},
        {45588, 430.86, 431.08, 422.53, 424.6},
        {45587, 418.49, 430.58, 418.04, 427.51},
        {45586, 416.12, 418.96, 413.75, 418.78},
        {45583, 417.14, 419.65, 416.26, 418.16},
        {45582, 422.36, 422.5, 415.59, 416.72},
        {45581, 415.17, 416.36, 410.48, 416.12},
        {45580, 422.18, 422.48, 415.26, 418.74},
        {45579, 417.77, 424.04, 417.52, 419.14},
        {45576, 416.14, 417.13, 413.25, 416.32},
        {45575, 415.23, 417.35, 413.15, 415.84},
        {45574, 415.86, 420.38, 414.3, 417.46},
        {45573, 410.9, 415.66, 408.17, 414.71},
        {45572, 416, 417.11, 409, 409.54},
        {45569, 418.24, 419.75, 414.97, 416.06},
        {45568, 417.63, 419.55, 414.29, 416.54},
        {45567, 422.58, 422.82, 416.71, 417.13},
        {45566, 428.45, 428.48, 418.81, 420.69},
        {45565, 428.21, 430.42, 425.37, 430.3},
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
    if err := f.AddChart("Planilha1", "F1", &excelize.Chart{
        Type: excelize.StockOpenHighLowClose,
        Series: []excelize.ChartSeries{
            {
                Name:       "Planilha1!$B$1",
                Categories: "Planilha1!$A$2:$A$22",
                Values:     "Planilha1!$B$2:$B$22",
            },
            {
                Name:       "Planilha1!$C$1",
                Categories: "Planilha1!$A$2:$A$22",
                Values:     "Planilha1!$C$2:$C$22",
            },
            {
                Name:       "Planilha1!$D$1",
                Categories: "Planilha1!$A$2:$A$22",
                Values:     "Planilha1!$D$2:$D$22",
            },
            {
                Name:       "Planilha1!$E$1",
                Categories: "Planilha1!$A$2:$A$22",
                Values:     "Planilha1!$E$2:$E$22",
            },
        },
        Legend: excelize.ChartLegend{Position: "none"},
        Title: []excelize.RichTextRun{
            {Text: "Gráfico de ações Abertura-Máxima-Mínima-Fechamento"},
        },
        XAxis: excelize.ChartAxis{
            NumFmt: excelize.ChartNumFmt{CustomNumFmt: "yyyy-mm-dd"},
        },
        PlotArea: excelize.ChartPlotArea{
            UpBars: excelize.ChartUpDownBar{
                Border: excelize.ChartLine{Type: excelize.ChartLineNone},
                Fill: excelize.Fill{
                    Type: "pattern", Color: []string{"00B050"}, Pattern: 1,
                },
            },
            DownBars: excelize.ChartUpDownBar{
                Border: excelize.ChartLine{Type: excelize.ChartLineNone},
                Fill: excelize.Fill{
                    Type: "pattern", Color: []string{"FF0000"}, Pattern: 1,
                },
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
