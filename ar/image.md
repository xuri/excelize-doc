# صورة

## إضافة الصورة {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture string, opts *GraphicOptions) error
```

توفر أداة AddPicture طريقة لإضافة صورة إلى ورقة عمل من خلال تحديد تنسيق الصورة (مثل الإزاحة، والمقياس، وإعدادات نسبة العرض إلى الارتفاع، وإعدادات الطباعة) ومسار الملف، وأنواع الصور المدعومة: BMP، وEMF، وEMZ، وGIF، وJPEG، وJPG، وPNG، وSVG، وTIF، وTIFF، وWMF، وWMZ. هذه الدالة آمنة للتزامن. يُرجى العلم أن هذه الدالة تدعم فقط إضافة الصور الموضوعة فوق الخلايا حاليًا، ولا تدعم إضافة الصور الموضوعة في الخلايا أو إنشاء خلايا صور مضمنة في Kingsoft WPS Office.

فمثلا:

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
    f := excelize.NewFile()
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    // إدراج صورة.
    if err := f.AddPicture("Sheet1", "A2", "image.png", nil); err != nil {
        fmt.Println(err)
        return
    }
    // إدراج صورة في ورقة عمل مع التحجيم.
    enable, disable := true, false
    if err := f.AddPicture("Sheet1", "D2", "image.jpg",
        &excelize.GraphicOptions{
            ScaleX:        0.5,
            ScaleY:        0.5,
            Hyperlink:     "#Sheet2!D8",
            HyperlinkType: "Location",
        },
    ); err != nil {
        fmt.Println(err)
        return
    }
    // إدراج إزاحة صورة في الخلية مع دعم الطباعة.
    if err := f.AddPicture("Sheet1", "H2", "image.gif",
        &excelize.GraphicOptions{
            OffsetX:         15,
            OffsetY:         10,
            Hyperlink:       "https://github.com/xuri/excelize",
            HyperlinkType:   "External",
            PrintObject:     &enable,
            LockAspectRatio: false,
            Locked:          &disable,
            Positioning:     "oneCell",
        },
    ); err != nil {
        fmt.Println(err)
        return
    }
    // احفظ جدول البيانات بالمسار المحدد.
    if err = f.Save(); err != nil {
        fmt.Println(err)
    }
}
```

يتم استخدام المعلمة الاختيارية `AltText` لإضافة نص بديل إلى كائن الرسم البياني.

تشير المعلمة الاختيارية `PrintObject` إلى ما إذا كانت الصورة ستتم طباعتها عند طباعة ورقة العمل ، والقيمة الافتراضية لذلك هي `true`.

تشير المعلمة الاختيارية `Locked` إلى ما إذا كان يتم قفل الصورة أم لا. لا يكون لتأمين الكائن أي تأثير إلا إذا كانت الورقة محمية.

تشير المعلمة الاختيارية `LockAspectRatio` إلى ما إذا كان قفل نسبة العرض إلى الارتفاع للصورة ، والقيمة الافتراضية لذلك هي `false`.

تحدد المعلمة الاختيارية `AutoFit` ما إذا كان حجم الصورة يناسب الخلية تلقائيًا ، فإن القيمة الافتراضية لذلك هي `false`.

تحدد المعلمة الاختيارية `OffsetX` الإزاحة الأفقية للصورة بالخلية ، والقيمة الافتراضية لذلك هي 0.

تحدد المعلمة الاختيارية `OffsetY` الإزاحة الرأسية للصورة بالخلية ، والقيمة الافتراضية لذلك هي 0.

تحدد المعلمة الاختيارية `ScaleX` المقياس الأفقي للصور ، والقيمة الافتراضية لذلك هي 1.0 والتي تقدم 100٪.

تحدد المعلمة الاختيارية `ScaleY` المقياس الرأسي للصور ، والقيمة الافتراضية لذلك هي 1.0 والتي تقدم 100٪.

تحدد المعلمة الاختيارية `Hyperlink` الارتباط التشعبي للصورة.

تحدد المعلمة الاختيارية `HyperlinkType` نوعين من الارتباط التشعبي `External` لموقع الويب أو `Location` للانتقال إلى إحدى الخلايا في هذا المصنف. عندما يكون `HyperlinkType` هو `Location` ، يجب أن تبدأ الإحداثيات بـ `#`.

تحدد المعلمة الاختيارية `Positioning` ثلاثة أنواع من موضع كائن الرسم البياني في جدول بيانات: `oneCell` (نقل ولكن بدون تغيير الحجم مع الخلايا) ، و `twoCell` (النقل والحجم مع الخلايا) ، و `absolute` ( لا تتحرك أو تحجم بالخلايا). إذا لم تقم بتعيين هذه المعلمة ، فسيكون الموضع الافتراضي هو نقل الخلايا وتغيير حجمها.

```go
func (f *File) AddPictureFromBytes(sheet, cell string, pic *Picture) error
```

يوفر AddPictureFromBytes طريقة لإضافة صورة في ورقة من خلال مجموعة تنسيق صورة معينة (مثل الإزاحة ، المقياس ، إعداد نسبة العرض إلى الارتفاع وإعدادات الطباعة) ، وصف النص البديل ، اسم الامتداد ومحتوى الملف في نوع `[]byte`. أنواع الصور المدعومة: EMF، EMZ، GIF، JPEG، JPG، PNG، SVG، TIF، TIFF، WMF، وWMZ. يُرجى العلم أن هذه الوظيفة تدعم فقط إضافة الصور الموضوعة فوق الخلايا حاليًا، ولا تدعم إضافة الصور الموضوعة داخل الخلايا أو إنشاء خلايا صور Kingsoft WPS Office المضمنة.

فمثلا:

```go
package main

import (
    "fmt"
    _ "image/jpeg"
    "os"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    enable := true
    if err := f.SetSheetView("Sheet1", -1, &excelize.ViewOptions{
        RightToLeft: &enable,
    }); err != nil {
        fmt.Println(err)
    }
    file, err := os.ReadFile("image.jpg")
    if err != nil {
        fmt.Println(err)
        return
    }
    if err := f.AddPictureFromBytes("Sheet1", "A2", &excelize.Picture{
        Extension: ".jpg",
        File:      file,
        Format:    &excelize.GraphicOptions{AltText: "Excel Logo"},
    }); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("المصنف1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## احصل على صورة {#GetPicture}

```go
func (f *File) GetPictures(sheet, cell string) ([]Picture, error)
```

يوفر GetPicture وظيفة للحصول على اسم قاعدة الصورة والمحتوى الخام المضمن في جدول بيانات بواسطة ورقة عمل واسم خلية معينين. هذه الوظيفة آمنة للتزامن. تقوم هذه الوظيفة بإرجاع اسم الملف في جدول البيانات ومحتويات الملف كأنواع بيانات `[]byte`.

فمثلا:

```go
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
pics, err := f.GetPictures("Sheet1", "A2")
if err != nil {
    fmt.Println(err)
}
for idx, pic := range pics {
    name := fmt.Sprintf("image%d%s", idx+1, pic.Extension)
    if err := os.WriteFile(name, pic.File, 0644); err != nil {
        fmt.Println(err)
    }
}
```

## حذف الصورة {#DeletePicture}

```go
func (f *File) DeletePicture(sheet, cell string) error
```

يوفر DeletePicture وظيفة لحذف المخططات في جدول بيانات عن طريق اسم الخلية وورقة العمل المحددة. لاحظ أنه لن يتم حذف ملف الصورة من المستند حاليًا.
