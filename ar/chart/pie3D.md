على سبيل المثال ، أضف مخطط دائري ثلاثي الأبعاد مثل هذا:

<p align="center"><img width="772" src="../images/3d_pie_chart.png" alt="إنشاء مخطط دائري ثلاثي الأبعاد باستخدام برنامج excelize باستخدام لغة Go"></p>

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
    if err := f.SetSheetName("Sheet1", "ورقة1"); err != nil {
        fmt.Println(err)
        return
    }
    enable := true
    if err := f.SetSheetView("ورقة1", -1, &excelize.ViewOptions{
        RightToLeft: &enable,
    }); err != nil {
        fmt.Println(err)
    }
    for idx, row := range [][]interface{}{
        {"تفاح", "برتقال", "كمثرى"},
        {2, 3, 3},
    } {
        cell, err := excelize.CoordinatesToCellName(1, idx+1)
        if err != nil {
            fmt.Println(err)
            return
        }
        if err := f.SetSheetRow("ورقة1", cell, &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    if err := f.AddChart("ورقة1", "E1", &excelize.Chart{
        Type: excelize.Pie3D,
        Series: []excelize.ChartSeries{
            {
                Name:       "مقدار",
                Categories: "ورقة1!$A$1:$C$1",
                Values:     "ورقة1!$A$2:$C$2",
            },
        },
        Format: excelize.GraphicOptions{
            OffsetX: 15,
            OffsetY: 10,
        },
        Title: []excelize.RichTextRun{
            {
                Text: "مخطط دائري ثلاثي الأبعاد",
            },
        },
        PlotArea: excelize.ChartPlotArea{
            ShowPercent:     true,
        },
    }); err != nil {
        fmt.Println(err)
        return
    }
    // احفظ جدول البيانات بالمسار المحدد.
    if err := f.SaveAs("المصنف1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```
