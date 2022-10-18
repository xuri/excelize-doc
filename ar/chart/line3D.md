# مخطط خطي ثلاثي الأبعاد {#line3D}

على سبيل المثال ، أضف مخطط خطي ثلاثي الأبعاد مثل هذا:

<p align="center"><img width="771" src="../images/3d_line_chart.png" alt="إنشاء مخطط خطي ثلاثي الأبعاد باستخدام برنامج excelize باستخدام لغة Go"></p>

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    categories := map[string]string{
        "A2": "صغير", "A3": "عادي", "A4": "كبير", "B1": "تفاح", "C1": "برتقال", "D1": "كمثرى"}
    values := map[string]int{
        "B2": 2, "C2": 3, "D2": 3, "B3": 5, "C3": 2, "D3": 4, "B4": 6, "C4": 7, "D4": 8}
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
        "type": "line3D",
        "series": [
        {
            "name": "ورقة1!$A$2",
            "categories": "ورقة1!$B$1:$D$1",
            "values": "ورقة1!$B$2:$D$2"
        },
        {
            "name": "ورقة1!$A$3",
            "categories": "ورقة1!$B$1:$D$1",
            "values": "ورقة1!$B$3:$D$3"
        },
        {
            "name": "ورقة1!$A$4",
            "categories": "ورقة1!$B$1:$D$1",
            "values": "ورقة1!$B$4:$D$4"
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
            "name": "مخطط خطي ثلاثي الأبعاد"
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
    // احفظ جدول البيانات بالمسار المحدد.
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```
