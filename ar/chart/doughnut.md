# دونات الرسم البياني {#doughnut}

على سبيل المثال ، أضف دونات الرسم البياني مثل هذا:

<p align="center"><img width="772" src="../images/doughnut_chart.png" alt="إنشاء دونات الرسم البياني باستخدام برنامج excelize باستخدام لغة Go"></p>

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {

    categories := map[string]string{"A1": "تفاح", "B1": "برتقال", "C1": "كمثرى"}
    values := map[string]int{"A2": 2, "B2": 3, "C2": 3}
    f := excelize.NewFile()
    f.SetSheetName("Sheet1", "ورقة1")
    enable := true
    if err := f.SetSheetView("ورقة1", -1, &excelize.ViewOptions{
        RightToLeft: &enable,
    }); err != nil {
        fmt.Println(err)
    }
    for k, v := range categories {
        f.SetCellValue("ورقة1", k, v)
    }
    for k, v := range values {
        f.SetCellValue("ورقة1", k, v)
    }
    if err := f.AddChart("ورقة1", "E1", `{
        "type": "doughnut",
        "series": [
        {
            "name": "ورقة1!$A$2",
            "categories": "ورقة1!$A$1:$C$1",
            "values": "ورقة1!$A$2:$C$2"
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
            "name": "دونات الرسم البياني"
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
    // احفظ جدول البيانات بالمسار المحدد.
    if err := f.SaveAs("المصنف1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```
