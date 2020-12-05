# صورة

## إضافة الصورة {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture, format string) error
```

يوفر AddPicture طريقة لإضافة صورة إلى ورقة العمل عن طريق مجموعة تنسيق صورة معينة (مثل الإزاحة ، المقياس ، إعداد نسبة العرض إلى الارتفاع ، وإعدادات الطباعة) ومسار الملف.

فمثلا:

```go
package main

import (
    "fmt"
    _ "image/gif"
    _ "image/jpeg"
    _ "image/png"

    "github.com/360EntSecGroup-Skylar/excelize"
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
}
```

يعرّف LinkType نوعين من الارتباطات التشعبية `External` لموقع ويب أو `Location` للانتقال إلى إحدى الخلايا في هذا المصنف. عندما يكون `hyperlink_type` هو `Location` ، يجب أن تبدأ الإحداثيات بـ `#`.

يحدد الموضع نوعين من موضع الصورة في جدول بيانات Excel ، `oneCell` (نقل ولكن بدون تغيير الحجم مع الخلايا) أو "مطلق" (لا تتحرك أو تحجم مع الخلايا). إذا لم تقم بتعيين هذه المعلمة ، فإن `positioning` الافتراضي هو النقل والحجم مع الخلايا.

```go
func (f *File) AddPictureFromBytes(sheet, cell, format, name, extension string, file []byte) error
```

يوفر AddPictureFromBytes طريقة لإضافة صورة في ورقة من خلال مجموعة تنسيق صورة معينة (مثل الإزاحة ، المقياس ، إعداد نسبة العرض إلى الارتفاع وإعدادات الطباعة) ، وصف النص البديل ، اسم الامتداد ومحتوى الملف في نوع `[]byte`.

فمثلا:

```go
package main

import (
    _ "image/jpeg"
    "io/ioutil"

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    f := excelize.NewFile()
    if err := f.SetSheetViewOptions("Sheet1", -1,
        excelize.RightToLeft(true),
    ); err != nil {
        fmt.Println(err)
    }
    file, err := ioutil.ReadFile("image.jpg")
    if err != nil {
        fmt.Println(err)
    }
    if err := f.AddPictureFromBytes("Sheet1", "A2", "", "Excel Logo", ".jpg", file); err != nil {
        fmt.Println(err)
    }
    if err := f.SaveAs("المصنف1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## احصل على صورة {#GetPicture}

```go
func (f *File) GetPicture(sheet, cell string) (string, []byte, error)
```

يوفر GetPicture وظيفة للحصول على اسم قاعدة الصورة والمحتوى الخام المضمن في جدول بيانات بواسطة ورقة عمل واسم خلية معينين. تقوم هذه الوظيفة بإرجاع اسم الملف في جدول البيانات ومحتويات الملف كأنواع بيانات `[]byte`.

فمثلا:

```go
f, err := excelize.OpenFile("المصنف1.xlsx")
if err != nil {
    fmt.Println(err)
    return
}
file, raw, err := f.GetPicture("Sheet1", "A2")
if err != nil {
    fmt.Println(err)
    return
}
if err := ioutil.WriteFile(file, raw, 0644); err != nil {
    fmt.Println(err)
}
```

## حذف الصورة {#DeletePicture}

```go
func (f *File) DeletePicture(sheet, cell string) (err error)
```

يوفر DeletePicture وظيفة لحذف المخططات في جدول بيانات عن طريق اسم الخلية وورقة العمل المحددة. لاحظ أنه لن يتم حذف ملف الصورة من المستند حاليًا.
