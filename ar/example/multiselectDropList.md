# قائمة منسدلة متعددة التحديد

قم بإنشاء قائمة منسدلة متعددة التحديد بدون VBA في جدول البيانات باستخدام Excelize باستخدام Go:

<p align="center"><img width="426" src="../images/multiselect_drop_list.gif" alt="قم بإنشاء قائمة منسدلة متعددة التحديد بدون VBA في جدول البيانات باستخدام Excelize باستخدام Go"></p>

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    // إنشاء جدول بيانات جديد
    f := excelize.NewFile()
    var (
        sheetName = "Sheet1"
        selection = []string{"red", "blue", "green", "yellow"}
        // قيم الخلية
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
    // قم بتعيين قيمة كل خلية
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
    // تعيين الاسم المحدد
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
    // ضبط التحقق من صحة البيانات
    dvRange := excelize.NewDataValidation(true)
    dvRange.Sqref = "D2:D2"
    dvRange.SetSqrefDropList("$B$2:$B$5")
    if err = f.AddDataValidation(sheetName, dvRange); err != nil {
        fmt.Println(err)
        return
    }
    // تعيين عرض العمود المخصص
    for col, width := range map[string]float64{"A": 10, "B": 18, "D": 18} {
        if err = f.SetColWidth(sheetName, col, col, width); err != nil {
            fmt.Println(err)
            return
        }
    }
    // إنشاء جدول
    if err = f.AddTable(sheetName, "A1", "B5", `{
        "table_name": "table",
        "table_style": "TableStyleMedium2"
    }`); err != nil {
        fmt.Println(err)
        return
    }
    // حفظ ملف جدول البيانات
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```
