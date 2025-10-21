# 株価チャート (出来高-始値-高値-安値-終値) {#stockVolumeOpenHighLowClose}

例えば、次のような効果を持つ 株価チャート (出来高-始値-高値-安値-終値) 作成します:

<p align="center"><img width="876" src="../images/stock_volume_open_high_low_close_chart.png" alt="Go 言語を使用して Excel ドキュメントで 株価チャート (出来高-始値-高値-安値-終値) 作成する"></p>

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
    for idx, row := range [][]interface{}{
        {"日付", "出来高", "始値", "高値", "安値", "終値"},
        {45593, 14864000, 431.66, 431.94, 426.3, 426.59},
        {45590, 16899100, 426.76, 432.52, 426.57, 428.15},
        {45589, 13581600, 425.33, 425.98, 422.4, 424.73},
        {45588, 19654400, 430.86, 431.08, 422.53, 424.6},
        {45587, 25482200, 418.49, 430.58, 418.04, 427.51},
        {45586, 14206100, 416.12, 418.96, 413.75, 418.78},
        {45583, 17145300, 417.14, 419.65, 416.26, 418.16},
        {45582, 14820000, 422.36, 422.5, 415.59, 416.72},
        {45581, 15508900, 415.17, 416.36, 410.48, 416.12},
        {45580, 18900200, 422.18, 422.48, 415.26, 418.74},
        {45579, 16653100, 417.77, 424.04, 417.52, 419.14},
        {45576, 14144900, 416.14, 417.13, 413.25, 416.32},
        {45575, 13848400, 415.23, 417.35, 413.15, 415.84},
        {45574, 14974300, 415.86, 420.38, 414.3, 417.46},
        {45573, 19229300, 410.9, 415.66, 408.17, 414.71},
        {45572, 20919800, 416, 417.11, 409, 409.54},
        {45569, 19169700, 418.24, 419.75, 414.97, 416.06},
        {45568, 13686400, 417.63, 419.55, 414.29, 416.54},
        {45567, 16582300, 422.58, 422.82, 416.71, 417.13},
        {45566, 19092900, 428.45, 428.48, 418.81, 420.69},
        {45565, 16807300, 428.21, 430.42, 425.37, 430.3},
    } {
        cell, err := excelize.CoordinatesToCellName(1, idx+1)
        if err != nil {
            fmt.Println(err)
            return
        }
        if err := f.SetSheetRow("Sheet1", cell, &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    if err := f.AddChart("Sheet1", "G1", &excelize.Chart{
        Type: excelize.Col,
        Series: []excelize.ChartSeries{
            {
                Name:       "Sheet1!$B$1",
                Categories: "Sheet1!$A$2:$A$22",
                Values:     "Sheet1!$B$2:$B$22",
            },
        },
        XAxis: excelize.ChartAxis{
            NumFmt: excelize.ChartNumFmt{CustomNumFmt: "yyyy-mm-dd"},
        },
        YAxis: excelize.ChartAxis{
            NumFmt: excelize.ChartNumFmt{CustomNumFmt: "#,##0"},
        },
        Title: []excelize.RichTextRun{
            {Text: "株価チャート (出来高-始値-高値-安値-終値)"},
        },
    }, &excelize.Chart{
        Type: excelize.StockOpenHighLowClose,
        Series: []excelize.ChartSeries{
            {
                Name:       "Sheet1!$C$1",
                Categories: "Sheet1!$A$2:$A$22",
                Values:     "Sheet1!$C$2:$C$22",
            },
            {
                Name:       "Sheet1!$D$1",
                Categories: "Sheet1!$A$2:$A$22",
                Values:     "Sheet1!$D$2:$D$22",
            },
            {
                Name:       "Sheet1!$E$1",
                Categories: "Sheet1!$A$2:$A$22",
                Values:     "Sheet1!$E$2:$E$22",
            },
            {
                Name:       "Sheet1!$F$1",
                Categories: "Sheet1!$A$2:$A$22",
                Values:     "Sheet1!$F$2:$F$22",
            },
        },
        YAxis: excelize.ChartAxis{Secondary: true},
    }); err != nil {
        fmt.Println(err)
        return
    }
    // ブックを保存する
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```
