# الاستخدام الأساسي

## التركيب {#install}

استخدام أحدث إصدار Excelize مكتبة تتطلب الانتقال الإصدار 1.15 أو أحدث.

- التركيب

```bash
go get github.com/xuri/excelize
```

- إذا كانت إدارة الحزمة مع [Go Modules](https://go.dev/blog/using-go-modules)، يرجى تثبيت مع الأمر التالي.

```bash
go get github.com/xuri/excelize/v2
```

## ترقيه {#update}

- ترقيه

```bash
go get -u github.com/xuri/excelize/v2
```

## قم بإنشاء مستند جدول بيانات {#NewFile}

هنا هو الحد الأدنى من الاستخدام الأمثلة التي من شأنها أن تخلق ملف جدول البيانات:

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    if err := f.SetSheetViewOptions("Sheet1", -1,
        excelize.RightToLeft(true),
    ); err != nil {
        fmt.Println(err)
    }
    // إنشاء ورقة عمل جديدة.
    index := f.NewSheet("Sheet2")
    // تعيين قيمة خلية.
    f.SetCellValue("Sheet2", "A2", "Hello world.")
    f.SetCellValue("Sheet1", "B2", 100)
    // تعيين ورقة نشطة للمصنف.
    f.SetActiveSheet(index)
    // احفظ جدول البيانات بالمسار المحدد.
    if err := f.SaveAs("المصنف1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## قراءة وثيقة إكسل {#read}

وفيما يلي يشكل عارية لقراءة وثيقة جدول:

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f, err := excelize.OpenFile("المصنف1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    // الحصول على قيمة من الخلية حسب اسم ورقة العمل والمحور.
    cell, err := f.GetCellValue("Sheet1", "B2")
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(cell)
    // الحصول على جميع الصفوف في Sheet1.
    rows, err := f.GetRows("Sheet1")
    if err != nil {
        fmt.Println(err)
        return
    }
    for _, row := range rows {
        for _, colCell := range row {
            fmt.Print(colCell, "\t")
        }
        fmt.Println()
    }
}
```

## أضف مخططًا إلى جدول بيانات {#chart}

مع Excelize إنشاء المخطط والإدارة سهلاً مثل بضعة أسطر من التعليمات البرمجية. يمكنك إنشاء مخططات استناداً إلى بيانات في ورقة العمل أو إنشاء مخططات بدون أية بيانات في ورقة العمل على الإطلاق.

<p align="center"><img width="770" src="../images/base.png" alt="أضف مخططًا إلى جدول بيانات"></p>

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
    if err := f.SetSheetViewOptions("Sheet1", -1,
        excelize.RightToLeft(true),
    ); err != nil {
        fmt.Println(err)
    }
    for k, v := range categories {
        f.SetCellValue("Sheet1", k, v)
    }
    for k, v := range values {
        f.SetCellValue("Sheet1", k, v)
    }
    if err := f.AddChart("Sheet1", "E1", `{
        "type": "col3DClustered",
        "series": [
        {
            "name": "Sheet1!$A$2",
            "categories": "Sheet1!$B$1:$D$1",
            "values": "Sheet1!$B$2:$D$2"
        },
        {
            "name": "Sheet1!$A$3",
            "categories": "Sheet1!$B$1:$D$1",
            "values": "Sheet1!$B$3:$D$3"
        },
        {
            "name": "Sheet1!$A$4",
            "categories": "Sheet1!$B$1:$D$1",
            "values": "Sheet1!$B$4:$D$4"
        }],
        "title":
        {
            "name": "مخطط عمودي مُكدَّد ثلاثي الأبعاد"
        }
    }`); err != nil {
        fmt.Println(err)
        return
    }
    // احفظ جدول البيانات بالمسار المحدد.
    if err := f.SaveAs("المصنف1.xlsx"); err != nil {
        fmt.Println(err)
    }
}

```

## أضف صورة إلى جدول البيانات {#image}

```go
package main

import (
    "fmt"
    _ "image/gif"
    _ "image/jpeg"
    _ "image/png"

    "github.com/xuri/excelize/v2"
)

func main() {
    f, err := excelize.OpenFile("المصنف1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    // إدراج صورة.
    if err := f.AddPicture("Sheet1", "A2", "image.png", ""); err != nil {
        fmt.Println(err)
    }
    // إدراج صورة في ورقة عمل مع التحجيم.
    if err := f.AddPicture("Sheet1", "D2", "image.jpg", `{
        "x_scale": 0.5,
        "y_scale": 0.5
    }`); err != nil {
        fmt.Println(err)
    }
    // إدراج إزاحة صورة في الخلية مع دعم الطباعة.
    if err := f.AddPicture("Sheet1", "H2", "image.gif", `{
        "x_offset": 15,
        "y_offset": 10,
        "print_obj": true,
        "lock_aspect_ratio": false,
        "locked": false
    }`); err != nil {
        fmt.Println(err)
    }
    // احفظ جدول البيانات بالمسار المحدد.
    if err = f.Save(); err != nil {
        fmt.Println(err)
    }
    if err = f.Close(); err != nil {
        fmt.Println(err)
    }
}
```
