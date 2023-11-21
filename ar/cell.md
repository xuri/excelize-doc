# الخليه

يقوم `RichTextRun` بتعيين إعدادات تشغيل النص المنسق مباشرةً.

```go
type RichTextRun struct {
    Font *Font
    Text string
}
```

يمكن تمرير `HyperlinkOpts` إلى [`SetCellHyperlink`](cell.md#SetCellHyperlink) لتعيين سمات الارتباط التشعبي الاختيارية (مثل النص المراد عرضه ونص تلميح الشاشة).

```go
type HyperlinkOpts struct {
    Display *string
    Tooltip *string
}
```

يمكن تمرير `FormulaOpts` إلى [`SetCellFormula`](cell.md#SetCellFormula) لاستخدام أنواع الصيغ الأخرى.

```go
type FormulaOpts struct {
    Type *string // نوع الصيغة
    Ref  *string // مرجع صيغة مشتركة
}
```

## تعيين قيمة الخلية {#SetCellValue}

```go
func (f *File) SetCellValue(sheet, cell string, value interface{}) error
```

يوفر SetCellValue دالة لتعيين قيمة خلية. هذه الوظيفة آمنة للتزامن. يجب ألا تكون الإحداثيات المحددة في الصف الأول من الجدول. التي تدعم أنواع البيانات التالية:

|أنواع البيانات المدعومة|
|---|
|int|
|int8|
|int16|
|int32|
|int64|
|uint|
|uint8|
|uint16|
|uint32|
|uint64|
|float32|
|float64|
|string|
|[]byte|
|time.Duration|
|time.Time|
|bool|
|nil|

لاحظ أن تنسيق التاريخ الافتراضي هو `m/d/yy h:mm` لقيمة نوع الوقت. يمكنك ضبط تنسيق الأرقام بطريقة [`SetCellStyle`](cell.md#SetCellStyle). إذا كنت بحاجة إلى تعيين التاريخ المتخصص في Excel مثل 0 يناير 1900 أو 29 فبراير 1900 ، فلا يمكن تمثيل هذه الأوقات في نوع بيانات Go بلغة البرمجة `time.Time`. يرجى تعيين قيمة الخلية كرقم 0 أو 60 ، ثم إنشاء وربط نمط تنسيق رقم التاريخ والوقت للخلية.

## تعيين قيمة منطقية {#SetCellBool}

```go
func (f *File) SetCellBool(sheet, cell string, value bool) error
```

يوفر SetCellBool وظيفة لتعيين قيمة نوع منطقي لخلية من خلال اسم ورقة العمل المحدد وإحداثيات الخلية وقيمة الخلية.

## تعيين قيمة RAW {#SetCellDefault}

```go
func (f *File) SetCellDefault(sheet, cell, value string) error
```

يوفر SetCellDefault وظيفة لتعيين قيمة نوع السلسلة لخلية كتنسيق افتراضي دون هروب الخلية.

## تعيين قيمة عدد صحيح {#SetCellInt}

```go
func (f *File) SetCellInt(sheet, cell string, value int) error
```

يوفر SetCellInt دالة لتعيين قيمة نوع int لخلية من خلال اسم ورقة العمل المحدد وإحداثيات الخلية وقيمة الخلية.

## تعيين قيمة عدد صحيح غير موقعة {#SetCellUint}

```go
func (f *File) SetCellUint(sheet, cell string, value uint64) error
```

يوفر SetCellUint وظيفة لتعيين قيمة نوع البيانات الصحيحة غير الموقعة للخلية من خلال اسم ورقة العمل المحددة ومرجع الخلية وقيمة الخلية.

## تعيين قيمة النقطة العائمة {#SetCellFloat}

```go
func (f *File) SetCellFloat(sheet, cell string, value float64, precision, bitSize int) error
```

يعيّن SetCellFloat قيمة النقطة العائمة في خلية. تحدد معلمة `precision` عدد الأماكن بعد العلامة العشرية التي سيتم عرضها بينما تعد `-1` قيمة خاصة ستستخدم العديد من المنازل العشرية حسب الضرورة لتمثيل الرقم. `bitSize` هو `32` أو `64` بناءً على ما إذا كان `float32` أو `float64` مستخدمًا في الأصل للقيمة.

## تعيين قيمة السلسلة {#SetCellStr}

```go
func (f *File) SetCellStr(sheet, cell, value string) error
```

يوفر SetCellStr وظيفة لتعيين قيمة نوع السلسلة للخلية. العدد الإجمالي للأحرف التي يمكن أن تحتويها الخلية على `32767` حرفًا.

## تعيين نمط الخلية {#SetCellStyle}

```go
func (f *File) SetCellStyle(sheet, hCell, vCell string, styleID int) error
```

يوفر SetCellStyle وظيفة لإضافة سمة نمط للخلايا من خلال اسم ورقة العمل المعطى ومنطقة الإحداثيات ومعرف النمط. هذه الوظيفة آمنة للتزامن. يمكن الحصول على فهارس النمط من خلال وظيفة [`NewStyle`](style.md#NewStyle). لاحظ أن حد النوع `diagonalDown` و `diagonalUp` يجب أن يستخدموا نفس اللون في نفس منطقة الإحداثيات. سيقوم SetCellStyle بالكتابة فوق الأنماط الموجودة للخلية ، ولن يقوم بإلحاق أو دمج النمط مع الأنماط الموجودة.

- المثال 1 ، أنشئ حدودًا للخلية `D7` في `Sheet1`:

```go
style, err := f.NewStyle(&excelize.Style{
    Border: []excelize.Border{
        {Type: "left", Color: "0000FF", Style: 3},
        {Type: "top", Color: "00FF00", Style: 4},
        {Type: "bottom", Color: "FFFF00", Style: 5},
        {Type: "right", Color: "FF0000", Style: 6},
        {Type: "diagonalDown", Color: "A020F0", Style: 8},
        {Type: "diagonalUp", Color: "A020F0", Style: 8},
    },
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_01.png" alt="تعيين نمط حد لخلية"></p>

تم تعيين الحدود الأربعة للخلية `D7` بأنماط وألوان مختلفة. يرتبط هذا بالمعلمات عند استدعاء وظيفة [`NewStyle`](style.md#NewStyle). تحتاج إلى تعيين أنماط مختلفة للإشارة إلى الوثائق الخاصة بهذا الفصل.

- المثال 2 ، تعيين نمط التدرج لخلية ورقة العمل `D7` المسماة `Sheet1`:

```go
style, err := f.NewStyle(&excelize.Style{
    Fill: excelize.Fill{Type: "gradient", Color: []string{"FFFFFF", "E0EBF5"}, Shading: 1},
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_02.png" alt="قم بتعيين نمط متدرج للخلية"></p>

تم تعيين الخلية `D7` بتعبئة اللون لتأثير التدرج. يرتبط تأثير التعبئة المتدرجة بالمعامل عند استدعاء الوظيفة [`NewStyle`](style.md#NewStyle). تحتاج إلى تعيين أنماط مختلفة للإشارة إلى وثائق هذا الفصل.

- مثال 3 ، عيّن تعبئة خالصة للخلية `D7` المسماة `Sheet1`:

```go
style, err := f.NewStyle(&excelize.Style{
    Fill: excelize.Fill{Type: "pattern", Color: []string{"E0EBF5"}, Pattern: 1},
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_03.png" alt="قم بتعيين تعبئة صلبة للخلية"></p>

تم تعيين الخلية `D7` بتعبئة ثابتة.

- مثال 4 ، عيّن تباعد الأحرف وزاوية الدوران للخلية `D7` المسماة `Sheet1`:

```go
f.SetCellValue("Sheet1", "D7", "أسلوب")
style, err := f.NewStyle(&excelize.Style{
    Alignment: &excelize.Alignment{
        Horizontal:      "center",
        Indent:          1,
        JustifyLastLine: true,
        ReadingOrder:    0,
        RelativeIndent:  1,
        ShrinkToFit:     true,
        TextRotation:    45,
        Vertical:        "",
        WrapText:        true,
    },
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_04.png" alt="اضبط تباعد الأحرف وزاوية الدوران"></p>

- مثال 5 ، يتم تمثيل التاريخ والوقت في Excel بأرقام حقيقية ، على سبيل المثال ، `2017/7/4 12:00:00 PM` يمكن تمثيلها بالرقم `42920.5`. عيّن تنسيق الوقت لخلية ورقة العمل `D7` المسماة `Sheet1`:

```go
f.SetCellValue("Sheet1", "D7", 42920.5)
f.SetColWidth("Sheet1", "D", "D", 13)
style, err := f.NewStyle(&excelize.Style{NumFmt: 22})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_05.png" alt="عيّن تنسيق الوقت للخلية"></p>

تم تعيين الخلية `D7` على تنسيق الوقت. لاحظ أنه عندما يكون عرض الخلية مع تنسيق الوقت المطبق ضيقًا جدًا بحيث لا يمكن عرضها بالكامل ، فسيتم عرضها كـ `####` ، يمكنك سحب عرض العمود وإفلاته أو تعيين العمود إلى الحجم المناسب عن طريق استدعاء وظيفة `SetColWidth` لجعلها عرضًا عاديًا.

- مثال 6 ، تعيين الخط وحجم الخط واللون ونمط الانحراف لخلية ورقة العمل `D7` المسماة `Sheet1`:

```go
f.SetCellValue("Sheet1", "D7", "Excel")
style, err := f.NewStyle(&excelize.Style{
    Font: &excelize.Font{
        Bold:   true,
        Italic: true,
        Family: "Times New Roman",
        Size:   36,
        Color:  "777777",
    },
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_06.png" alt="تعيين الخط وحجم الخط واللون ونمط الانحراف للخلايا"></p>

- مثال 7 ، تأمين وإخفاء خلية ورقة العمل `D7` المسماة `Sheet1`:

```go
style, err := f.NewStyle(&excelize.Style{
    Protection: &excelize.Protection{
        Hidden: true,
        Locked: true,
    },
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

لتأمين خلية أو إخفاء صيغة ، قم بحماية ورقة العمل. في علامة التبويب "مراجعة" ، انقر فوق "حماية ورقة العمل".

## تعيين ارتباط تشعبي {#SetCellHyperLink}

```go
func (f *File) SetCellHyperLink(sheet, cell, link, linkType string, opts ...HyperlinkOpts) error
```

يوفر SetCellHyperLink وظيفة لتعيين الارتباطات التشعبية للخلايا عن طريق اسم ورقة العمل وعنوان URL للرابط. يعرّف LinkType نوعين من الارتباطات التشعبية `External` لموقع الويب أو `Location` للانتقال إلى إحدى الخلايا في هذا المصنف. الحد الأقصى للارتباطات التشعبية في ورقة العمل هو `65530`. تُستخدم هذه الوظيفة فقط لتعيين الارتباط التشعبي للخلية ولا تؤثر على قيمة الخلية. إذا كنت بحاجة إلى تعيين قيمة الخلية ، فالرجاء استخدام الوظائف الأخرى مثل [`SetCellStyle`](cell.md#SetCellStyle) أو [`SetSheetRow`](sheet.md#SetSheetRow). أدناه مثال على ارتباط خارجي.

- مثال 1 ، إضافة ارتباط خارجي إلى الخلية `A3` من ورقة العمل المسماة `Sheet1`:

```go
display, tooltip := "https://github.com/xuri/excelize", "Excelize on GitHub"
if err := f.SetCellHyperLink("Sheet1", "A3",
    "https://github.com/xuri/excelize", "External", excelize.HyperlinkOpts{
        Display: &display,
        Tooltip: &tooltip,
    }); err != nil {
    fmt.Println(err)
}
// عيّن الخط ونمط التسطير للخلية
style, err := f.NewStyle(&excelize.Style{
    Font: &excelize.Font{Color: "1265BE", Underline: "single"},
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "A3", "A3", style)
```

- المثال 2 ، إضافة ارتباط موقع داخلي إلى الخلية `A3` المسماة `Sheet1`:

```go
err := f.SetCellHyperLink("Sheet1", "A3", "Sheet1!A40", "Location")
```

## تعيين نص منسق للخلية {#SetCellRichText}

```go
func (f *File) SetCellRichText(sheet, cell string, runs []RichTextRun) error
```

يوفر SetCellRichText وظيفة لتعيين خلية بنص منسق بواسطة ورقة عمل معينة.

على سبيل المثال ، قم بتعيين نص منسق في الخلية `A1` من ورقة العمل المسماة `Sheet1`:

<p align="center"><img width="612" src="./images/rich_text.png" alt="تعيين خلية نص منسق"></p>

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
    enable := true
    if err := f.SetSheetView("Sheet1", -1, &excelize.ViewOptions{
        RightToLeft: &enable,
    }); err != nil {
        fmt.Println(err)
    }
    if err := f.SetRowHeight("Sheet1", 1, 35); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SetColWidth("Sheet1", "A", "A", 44); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SetCellRichText("Sheet1", "A1", []excelize.RichTextRun{
        {
            Text: "bold",
            Font: &excelize.Font{
                Bold:   true,
                Color:  "2354E8",
                Family: "Times New Roman",
            },
        },
        {
            Text: " and ",
            Font: &excelize.Font{
                Family: "Times New Roman",
            },
        },
        {
            Text: "italic ",
            Font: &excelize.Font{
                Bold:   true,
                Color:  "E83723",
                Italic: true,
                Family: "Times New Roman",
            },
        },
        {
            Text: "text with color and font-family,",
            Font: &excelize.Font{
                Bold:   true,
                Color:  "2354E8",
                Family: "Times New Roman",
            },
        },
        {
            Text: "\r\nlarge text with ",
            Font: &excelize.Font{
                Size:  14,
                Color: "AD23E8",
            },
        },
        {
            Text: "strike",
            Font: &excelize.Font{
                Color:  "E89923",
                Strike: true,
            },
        },
        {
            Text: " superscript",
            Font: &excelize.Font{
                Color:     "DBC21F",
                VertAlign: "superscript",
            },
        },
        {
            Text: " and ",
            Font: &excelize.Font{
                Size:      14,
                Color:     "AD23E8",
                VertAlign: "baseline",
            },
        },
        {
            Text: "underline",
            Font: &excelize.Font{
                Color:     "23E833",
                Underline: "single",
            },
        },
        {
            Text: " subscript.",
            Font: &excelize.Font{
                Color:     "017505",
                VertAlign: "subscript",
            },
        },
    }); err != nil {
        fmt.Println(err)
        return
    }
    style, err := f.NewStyle(&excelize.Style{
        Alignment: &excelize.Alignment{
            WrapText: true,
        },
    })
    if err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SetCellStyle("Sheet1", "A1", "A1", style); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("المصنف1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## احصل على نص منسق للخلية {#GetCellRichText}

```go
func (f *File) GetCellRichText(sheet, cell string) ([]RichTextRun, error)
```

يوفر GetCellRichText وظيفة للحصول على نص منسق للخلايا بواسطة ورقة عمل معينة.

## الحصول على قيمة الخلية {#GetCellValue}

```go
func (f *File) GetCellValue(sheet, cell string, opts ...Options) (string, error)
```

يتم استرداد قيمة الخلية وفقًا لورقة العمل المحددة وإحداثيات الخلية ، ويتم تحويل قيمة الإرجاع إلى نوع `string`. هذه الوظيفة آمنة للتزامن. إذا كان من الممكن تطبيق تنسيق الخلية على قيمة خلية ، فسيتم إرجاع القيمة المطبقة ، وإلا سيتم إرجاع القيمة الأصلية. ستكون جميع قيم الخلايا هي نفسها في النطاق المدمج.

## احصل على نوع الخلية {#GetCellType}

```go
func (f *File) GetCellType(sheet, cell string) (CellType, error)
```

يوفر GetCellType وظيفة للحصول على نوع بيانات الخلية عن طريق اسم ورقة العمل المحددة والمحور في ملف جدول البيانات.

## الحصول على كل قيمة الخلية حسب الأعمدة {#GetCols}

```go
func (f *File) GetCols(sheet string, opts ...Options) ([][]string, error)
```

يحصل GetCols على قيمة جميع الخلايا حسب الأعمدة في ورقة العمل استنادًا إلى اسم ورقة العمل المحدد ، ويتم إرجاعه كمصفوفة ثنائية الأبعاد ، حيث يتم تحويل قيمة الخلية إلى نوع `string`. إذا كان من الممكن تطبيق تنسيق الخلية على قيمة الخلية ، فسيتم استخدام القيمة المطبقة ، وإلا سيتم استخدام القيمة الأصلية. فمثلا:

على سبيل المثال ، احصل على قيمة جميع الخلايا واجتيازها حسب الأعمدة في ورقة عمل تسمى `Sheet1`:

```go
cols, err := f.GetCols("Sheet1")
if err != nil {
    fmt.Println(err)
    return
}
for _, col := range cols {
    for _, rowCell := range col {
        fmt.Print(rowCell, "\t")
    }
    fmt.Println()
}
```

## الحصول على كل قيمة الخلية بالصفوف {#GetRows}

```go
func (f *File) GetRows(sheet string, opts ...Options) ([][]string, error)
```

يُرجع GetRows كافة الصفوف في الورقة بواسطة اسم ورقة العمل المحدد ، ويتم إرجاعه كمصفوفة ثنائية الأبعاد ، حيث يتم تحويل قيمة الخلية إلى نوع `string`. إذا كان من الممكن تطبيق تنسيق الخلية على قيمة الخلية ، فسيتم استخدام القيمة المطبقة ، وإلا سيتم استخدام القيمة الأصلية. جلب GetRows الصفوف ذات القيمة أو خلايا الصيغة ، وسيتم تخطي الخلايا الفارغة باستمرار في ذيل كل صف ، لذلك قد يكون طول كل صف غير متسق.

على سبيل المثال ، احصل على قيمة جميع الخلايا واجتيازها حسب الصفوف في ورقة عمل تسمى `Sheet1`:

```go
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
```

## الحصول على ارتباط تشعبي {#GetCellHyperLink}

```go
func (f *File) GetCellHyperLink(sheet, cell string) (bool, string, error)
```

يحصل GetCellHyperLink على ارتباط تشعبي للخلية استنادًا إلى اسم ورقة العمل المحددة وإحداثيات الخلية. إذا كانت الخلية تحتوي على ارتباط تشعبي ، فستعرض `true` وعنوان الارتباط ، وإلا ستعرض `false` وعنوان ارتباط فارغًا.

على سبيل المثال ، احصل على ارتباط تشعبي لخلية `H6` في ورقة عمل باسم `Sheet1`:

```go
link, target, err := f.GetCellHyperLink("Sheet1", "H6")
```

## الحصول على فهرس النمط {#GetCellStyle}

```go
func (f *File) GetCellStyle(sheet, cell string) (int, error)
```

يتم الحصول على فهرس نمط الخلية من اسم ورقة العمل المحددة وإحداثيات الخلية ، ويمكن استخدام الفهرس الذي تم الحصول عليه كمعامل لاستدعاء وظيفة `SetCellStyle` عند نسخ نمط الخلية.

## دمج الخلايا {#MergeCell}

```go
func (f *File) MergeCell(sheet, hCell, vCell string) error
```

دمج الخلايا بناءً على اسم ورقة العمل المحدد ومناطق إحداثيات الخلية. يؤدي دمج الخلايا إلى الاحتفاظ فقط بقيمة الخلية العلوية اليسرى ، ويتجاهل القيم الأخرى. على سبيل المثال ، ادمج الخلايا في منطقة `D3:E9` في ورقة عمل تسمى `Sheet1`:

```go
err := f.MergeCell("Sheet1", "D3", "E9")
```

إذا تداخلت منطقة إحداثيات الخلية المحددة مع الخلايا المدمجة الأخرى الموجودة ، فسيتم حذف الخلايا المدمجة الحالية.

## خلايا إلغاء الدمج {#UnmergeCell}

```go
func (f *File) UnmergeCell(sheet string, hCell, vCell string) error
```

يوفر UnmergeCell وظيفة لإلغاء دمج منطقة إحداثيات معينة. على سبيل المثال ، إلغاء دمج المنطقة `D3:E9` في `Sheet1`:

```go
err := f.UnmergeCell("Sheet1", "D3", "E9")
```

تنبيه: المناطق المتداخلة ستكون أيضًا غير مدمجة.

## الحصول على خلايا دمج {#GetMergeCells}

يوفر GetMergeCells وظيفة للحصول على جميع الخلايا المدمجة من ورقة العمل حاليًا.

```go
func (f *File) GetMergeCells(sheet string) ([]MergeCell, error)
```

### احصل على قيمة خلية مدمجة

```go
func (m *MergeCell) GetCellValue() string
```

إرجاع GetCellValue قيمة الخلية المدمجة.

### احصل على إحداثيات الخلية اليسرى العلوية للنطاق المدمج

```go
func (m *MergeCell) GetStartAxis() string
```

يُرجع GetStartAxis إحداثيات الخلية اليسرى العلوية للنطاق المدمج ، على سبيل المثال: `C2`.

### احصل على إحداثيات الخلية اليمنى السفلية للنطاق المدمج

```go
func (m *MergeCell) GetEndAxis() string
```

يُرجع GetEndAxis إحداثيات الخلية اليمنى السفلية للنطاق المدمج ، على سبيل المثال: `D4`.

## إضافة تعليق {#AddComment}

```go
func (f *File) AddComment(sheet string, comment Comment) error
```

يوفر AddComment طريقة لإضافة التعليقات في ورقة من خلال فهرس ورقة العمل والخلية ومجموعة التنسيق (مثل المؤلف والنص). لاحظ أن الحد الأقصى لطول المؤلف هو 255 والحد الأقصى لطول النص هو 32512. على سبيل المثال ، أضف تعليقًا في `Sheet1!$A$3`:

<p align="center"><img width="613" src="./images/comment.png" alt="أضف تعليقًا إلى مستند Excel"></p>

```go
err := f.AddComment("Sheet1", excelize.Comment{
    Cell:   "A3",
    Author: "Excelize",
    Paragraph: []excelize.RichTextRun{
        {Text: "Excelize: ", Font: &excelize.Font{Bold: true}},
        {Text: "هذا تعليق."},
    },
})
```

## الحصول على تعليق {#GetComments}

```go
func (f *File) GetComments(sheet string) ([]Comment, error)
```

يقوم GetComments باسترداد جميع التعليقات في ورقة العمل حسب اسم ورقة العمل المحدد.

## حذف تعليق {#DeleteComment}

```go
func (f *File) DeleteComment(sheet, cell string) error
```

يوفر DeleteComment طريقة حذف تعليق في ورقة بواسطة ورقة عمل معينة. على سبيل المثال ، احذف التعليق في `Sheet1!$A$30`:

```go
err := f.DeleteComment("Sheet1", "A30")
```

## تعيين صيغة الخلية {#SetCellFormula}

```go
func (f *File) SetCellFormula(sheet, cell, formula string, opts ...FormulaOpts) error
```

يوفر SetCellFormula وظيفة لتعيين الصيغة على الخلية يتم أخذها وفقًا لاسم ورقة العمل المحدد وإعدادات صيغة الخلية. يمكن حساب نتيجة خلية الصيغة عند فتح ورقة العمل بواسطة تطبيق Office Excel أو يمكن أن تستخدم الدالة [CalcCellValue](cell.md#CalcCellValue) أيضاً الحصول على قيمة الخلية المحسوبة. إذا لم يقم تطبيق Excel بحساب الصيغة تلقائيًا عند فتح المصنف ، يرجى الاتصال بـ [UpdateLinkedValue](utils.md#UpdateLinkedValue) بعد تعيين وظائف صيغة الخلية.

- مثال 1 ،  تعيين الصيغة العادية `=SUM(A1,B1)` للخلية `A3` على `Sheet1`:

```go
err := f.SetCellFormula("Sheet1", "A3", "=SUM(A1,B1)")
```

- مثال 2 ،  تعيين صفيف ثابت عمودي أحادي الأبعاد (صفيف عمود) الصيغة `1;2;3` للخلية `A3` على `Sheet1`:

```go
err := f.SetCellFormula("Sheet1", "A3", "={1;2;3}")
```

- مثال 3 ،  تعيين صفيف ثابت أفقي أحادي الأبعاد (صف صف الصفيف) الصيغة `"a","b","c"` للخلية `A3` على `Sheet1`:

```go
err := f.SetCellFormula("Sheet1", "A3", "={\"a\",\"b\",\"c\"}")
```

- مثال 4 ،  تعيين صيغة صفيف ثابت ثنائي الأبعاد `{1,2;"a","b"}` للخلية `A3` على `Sheet1`:

```go
formulaType, ref := excelize.STCellFormulaTypeArray, "A3:A3"
err := f.SetCellFormula("Sheet1", "A3", "={1,2;\"a\",\"b\"}",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- مثال 5 ،  تعيين صيغة صفيف النطاق `A1:A2` للخلية `A3` على `Sheet1`:

```go
formulaType, ref := excelize.STCellFormulaTypeArray, "A3:A3"
err := f.SetCellFormula("Sheet1", "A3", "=A1:A2",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- مثال 6 ، قم بتعيين الصيغة المشتركة `=A1+B1` للخلايا `C1:C5` في `Sheet1` ، `C1` هي الخلية الرئيسية:

```go
formulaType, ref := excelize.STCellFormulaTypeShared, "C1:C5"
err := f.SetCellFormula("Sheet1", "C1", "=A1+B1",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- مثال 7 ، تعيين صيغة الجدول `=SUM(Table1[[A]:[B]])` للخلية `C2` في `Sheet1`:

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
    for idx, row := range [][]interface{}{{"A", "B", "C"}, {1, 2}} {
        if err := f.SetSheetRow("Sheet1", fmt.Sprintf("A%d", idx+1), &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    if err := f.AddTable("Sheet1",
        &excelize.Table{
            Range:     "A1:C2",
            Name:      "Table1",
            StyleName: "TableStyleMedium2",
        }); err != nil {
        fmt.Println(err)
        return
    }
    formulaType := excelize.STCellFormulaTypeDataTable
    if err := f.SetCellFormula("Sheet1", "C2", "=SUM(Table1[[A]:[B]])",
        excelize.FormulaOpts{Type: &formulaType}); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## الحصول على صيغة الخلية {#GetCellFormula}

```go
func (f *File) GetCellFormula(sheet, cell string) (string, error)
```

احصل على الصيغة في الخلية بناءً على اسم ورقة العمل المحددة وإحداثيات الخلية.

## حساب قيمة الخلية {#CalcCellValue}

```go
func (f *File) CalcCellValue(sheet, cell string, opts ...Options) (string, error)
```

توفر CalcCellValue دالة للحصول على قيمة الخلية المحسوبة. هذه الميزة قيد المعالجة حاليًا. الحساب التكراري والتقاطع الضمني والتقاطع الصريح وصيغة الصفيف وصيغة الجدول وبعض الصيغ الأخرى غير مدعومة حاليًا.

الصيغ المدعومة:

اسم الدالة | النوع والوصف
---|---
ABS                      | إرجاع القيمة المطلقة لأحد الأرقام
ACCRINT                  | إرجاع الفائدة المستحقة للورقة المالية الذي يعطي فائدة دورية
ACCRINTM                 | إرجاع الفائدة المستحقة للورقة المالية تُدفع فائدتها عند الاستحقاق
ACOS                     | إرجاع قوس جيب التمام لأحد الأرقام
ACOSH                    | إرجاع جيب التمام العكسي للقطع الزائد لأحد الأرقام
ACOT                     | إرجاع قوس ظل التمام لأحد الأرقام
ACOTH                    | إرجاع قوس ظل التمام الزائدي لأحد الأرقام
ADDRESS                  | إرجاع مرجع كنص إلى خلية مفردة في ورقة عمل
AGGREGATE                | إرجاع تجميع في قائمة أو قاعدة بيانات
AMORDEGRC                | إرجاع الإهلاك لكل فترة محاسبية باستخدام مُعامل إهلاك
AMORLINC                 | إرجاع الإهلاك لكل فترة محاسبية
AND                      | إرجاع TRUE إذا كانت كافة وسيطاتها TRUE
ARABIC                   | تحويل رقم روماني إلى رقم عربي، كرقم
ARRAYTOTEXT              | تُرجع مصفوفة من القيم النصية من أي نطاق محدد.
ASIN                     | إرجاع قوس جيب الزاوية لأحد الأرقام
ASINH                    | إرجاع جيب الزاوية العكسي الزائدي لأحد الأرقام
ATAN                     | إرجاع قوس ظل الزاوية لأحد الأرقام
ATAN2                    | إرجاع قوس ظل الزاوية من الإحداثيات س وص
ATANH                    | إرجاع ظل الزاوية الزائدي العكسي لقطع زائد لأحد الأرقام
AVEDEV                   | إرجاع متوسط الانحرافات المطلقة لنقاط البيانات عن الوسط الخاص بها
AVERAGE                  | إرجاع متوسط الوسيطات الخاصة بالدالة
AVERAGEA                 | إرجاع متوسط الوسيطات الخاصة بالدالة، بما في ذلك الأرقام والنصوص والقيم المنطقية
AVERAGEIF                | إرجاع المتوسط (الوسط الحسابي) لكافة الخلايا الموجودة في نطاق والتي تفي بمعايير معينة
AVERAGEIFS               | إرجاع المتوسط (الوسط الحسابي) لكافة الخلايا التي تفي بمعايير متعددة
BASE                     | تحويل رقم إلى تمثيل نصي بالجذر (الأساس) المعين
BESSELI                  | إرجاع دالة Bessel المعدلة In(x)
BESSELJ                  | إرجاع دالة Jn(x) Bessel
BESSELK                  | إرجاع دالة Bessel المعدلة Kn(x)
BESSELY                  | إرجاع الدالة Yn(x) Bessel
BETADIST                 | إرجاع دالة التوزيع التراكمي لبيتا
BETA.DIST                | إرجاع دالة التوزيع التراكمي لبيتا
BETAINV                  | إرجاع عكس دالة التوزيع التراكمي لتوزيع بيتا معين. في Excel 2007، هذه الدالة هي دالة إحصائية
BETA.INV                 | إرجاع عكس دالة التوزيع التراكمي لتوزيع بيتا معين
BIN2DEC                  | تحويل رقم ثنائي إلى رقم عشري
BIN2HEX                  | تحويل رقم ثنائي إلى رقم ست عشري
BIN2OCT                  | تحويل رقم ثنائي إلى رقم ثماني
BINOMDIST                | إرجاع المصطلح الفردي لاحتمال التوزيع ذي الحدين. في Excel 2007، هذه الدالة هي دالة إحصائية
BINOM.DIST               | إرجاع المصطلح الفردي لاحتمال التوزيع ذي الحدين
BINOM.DIST.RANGE         | إرجاع احتمال نتيجة تجريبية باستخدام التوزيع ذي الحدين
BINOM.INV                | إرجاع أصغر قيمة يكون عندها التوزيع التراكمي ذو الحدين أصغر من قيمة المعيار أو مساوياً لها
BITAND                   | إرجاع البت 'و' لرقمين
BITLSHIFT                | إرجاع قيمة رقم مزاحة لليسار بواسطة وحدات بت shift_amount
BITOR                    | إرجاع البت 'OR' لرقمين
BITRSHIFT                | إرجاع قيمة رقم مزاحة لليمين بواسطة وحدات بت shift_amount
BITXOR                   | ترجع ناتج رابطة البت 'Exclusive Or' لرقمين
CEILING                  | تقريب رقم إلى أقرب عدد صحيح أو إلى أقرب مضاعف ذي أهمية
CEILING.MATH             | تقريب رقم إلى الأعلى وصولاً إلى أقرب عدد صحيح أو إلى أقرب مضاعف ذي أهمية
CEILING.PRECISE          | تقريب رقم إلى أقرب عدد صحيح أو إلى أقرب مضاعف ذي أهمية. يتم تقريب الرقم إلى الأعلى بغض النظر عن علامته
CHAR                     | إرجاع الحرف المحدد برقم الرمز
CHIDIST                  | إرجاع الاحتمال وحيد الطرف لتوزيع كاي تربيع. في Excel 2007، هذه الدالة هي دالة إحصائية
CHIINV                   | إرجاع عكس الاحتمال وحيد الطرف لتوزيع كاي تربيع. في Excel 2007، هذه الدالة هي دالة إحصائية
CHITEST                  | إرجاع اختبار الاستقلال. في Excel 2007، هذه الدالة هي دالة إحصائية
CHISQ.DIST               | إرجاع دالة كثافة احتمالات بيتا التراكمية
CHISQ.DIST.RT            | إرجاع الاحتمال وحيد الطرف لتوزيع كاي تربيع
CHISQ.INV                | إرجاع دالة كثافة احتمالات بيتا التراكمية
CHISQ.INV.RT             | إرجاع عكس الاحتمال وحيد الطرف لتوزيع كاي تربيع
CHISQ.TEST               | إرجاع اختبار الاستقلال
CHOOSE                   | تختار قيمة من قائمة قيم
CLEAN                    | إزالة كافة الأحرف غير القابلة للطباعة من النص
CODE                     | إرجاع رمز رقمي للحرف الأول بإحدى السلاسل النصية
COLUMN                   | إرجاع رقم العمود الخاص بمرجع
COLUMNS                  | إرجاع عدد الأعمدة الموجودة في مرجع
COMBIN                   | إرجاع عدد التوافقيات لعدد معين من العناصر
COMBINA                  | إرجاع عدد التركيبات لعدد معين من العناصر
COMPLEX                  | تحويل المُعاملات الحقيقية والتخيلية إلى رقم مركب
CONCAT                   | دمج النص من نطاقات و/أو سلاسل متعددة، ولكن لا توفر المحدِد أو وسيطات تجاهل الفارغ
CONCATENATE              | ربط عدة عناصر نصية في عنصر نصي واحد
CONFIDENCE               | إرجاع فاصل الثقة لوسط محتوى. في Excel 2007، هذه الدالة هي دالة إحصائية
CONFIDENCE.NORM          | إرجاع فاصل الثقة لوسط محتوى
CONFIDENCE.T             | إرجاع فاصل الثقة لوسط محتوى، باستخدام توزيع t للطالب
CONVERT                  | تحويل رقم من نظام قياس إلى آخر
CORREL                   | إرجاع مُعامل الارتباط بين مجموعتين من البيانات
COS                      | إرجاع جيب التمام لأحد الأرقام
COSH                     | إرجاع جيب التمام الزائدي لأحد الأرقام
COT                      | إرجاع جيب التمام الزائدي لأحد الأرقام
COTH                     | إرجاع ظل التمام لزاوية
COUNT                    | حساب عدد الأرقام الموجودة في قائمة الوسيطات
COUNTA                   | حساب عدد القيم الموجودة في قائمة الوسيطات
COUNTBLANK               | حساب عدد الخلايا الفارغة داخل نطاق
COUNTIF                  | حساب عدد الخلايا داخل نطاق والتي تفي بالمعايير المعينة
COUNTIFS                 | حساب عدد الخلايا داخل نطاق والتي تفي بالمعايير المعينة
COUPDAYBS                | إرجاع عدد الأيام من بداية فترة القسيمة إلى تاريخ التسوية
COUPDAYS                 | إرجاع عدد الأيام في فترة القسيمة التي تتضمن تاريخ التسوية
COUPDAYSNC               | إرجاع عدد الأيام من تاريخ التسوية إلى تاريخ القسيمة التالي
COUPNCD                  | إرجاع تاريخ القسيمة التالي بعد تاريخ التسوية
COUPNUM                  | إرجاع عدد القسائم المستحقة الدفع بين تاريخ التسوية وتاريخ الاستحقاق
COUPPCD                  | إرجاع تاريخ القسيمة السابق قبل تاريخ التسوية
COVAR                    | إرجاع التباين المشترك، معدل ضرب الانحرافات المزدوجة. في Excel 2007، هذه الدالة هي دالة إحصائية
COVARIANCE.P             | إرجاع التباين المشترك، معدل ضرب الانحرافات المزدوجة
COVARIANCE.S             | إرجاع التباين المشترك، معدل ضرب الانحرافات لكل زوج من نقاط البيانات في مجموعتين من البيانات
CRITBINOM                | إرجاع أصغر قيمة يكون عندها التوزيع التراكمي ذو الحدين أصغر من قيمة المعيار أو مساوياً لها. في Excel 2007، هذه الدالة هي دالة إحصائية
CSC                      | إرجاع قاطع التمام لزاوية
CSCH                     | إرجاع قاطع التمام الزائدي لزاوية
CUMIPMT                  | إرجاع الفائدة المتراكمة المدفوعة بين فترتين
CUMPRINC                 | إرجاع رأس المال المتراكم المدفوع على قرض بين فترتين
DATE                     | إرجاع الرقم التسلسلي لتاريخ معين
DATEDIF                  | تحسب هذه الدالة عدد الأيام، أو الأشهر أو السنوات بين تاريخين. تُعتبر هذه الدالة مفيدة في الصيغ التي تحتاج فيها إلى حساب العمر
DATEVALUE                | تحويل تاريخ على شكل نص إلى رقم تسلسلي
DAVERAGE                 | إرجاع متوسط إدخالات قاعدة البيانات المحددة
DAY                      | تحويل رقم تسلسلي إلى يوم من أيام الشهر
DAYS                     | إرجاع عدد الأيام بين تاريخين
DAYS360                  | حساب عدد الأيام بين تاريخين استناداً إلى سنة مكونة من 360 يوماً
DB                       | إرجاع إهلاك الأصول لفترة معينة باستخدام أسلوب الرصيد المتناقص الثابت
DCOUNT                   | حساب الخلايا التي تحتوي على أرقام في قاعدة بيانات
DCOUNTA                  | حساب الخلايا غير الفارغة في قاعدة بيانات
DDB                      | إرجاع إهلاك الأصول لفترة معينة باستخدام أسلوب الرصيد المتناقص المزدوج أو أساليب أخرى تحددها
DEC2BIN                  | تحويل رقم عشري إلى رقم ثنائي
DEC2HEX                  | تحويل رقم عشري إلى رقم ست عشري
DEC2OCT                  | تحويل رقم عشري إلى رقم ثماني
DECIMAL                  | تحويل تمثيل نصي لأحد الأرقام في أساس معين إلى رقم عشري
DEGREES                  | تحويل من تقدير دائري إلى درجات
DELTA                    | اختبار المساواة بين قيمتين
DEVSQ                    | إرجاع مجموع مربعات الانحرافات
DGET                     | استخراج سجل مفرد من قاعدة بيانات يطابق المعايير المعينة
DISC                     | إرجاع نسبة الخصم على الورقة المالية
DMAX                     | إرجاع القيمة القصوى من إدخالات قاعدة البيانات المحددة
DMIN                     | إرجاع القيمة الدنيا من إدخالات قاعدة البيانات المحددة
DOLLARDE                 | تحويل سعر دولار، يتم التعبير عنه ككسر، إلى سعر دولار، يتم التعبير عنه كرقم عشري
DOLLARFR                 | تحويل سعر دولار، يتم التعبير عنه كرقم عشري، إلى سعر دولار، يتم التعبر عنه ككسر
DPRODUCT                 | تضرب القيم في حقل سجلات معين يطابق المعيار الموجود في قاعدة بيانات
DSTDEV                   | تقدير الانحراف المعياري استناداً إلى عينة من إدخالات قاعدة بيانات محددة
DSTDEVP                  | حساب الانحراف المعياري استناداً إلى المحتوى بالكامل لإدخالات قاعدة البيانات المحددة
DSUM                     | جمع الأرقام في عمود الحقل الخاص بالسجلات في قاعدة البيانات التي تطابق المعايير
DURATION                 | إرجاع المدة السنوية لورقة مالية لها مدفوعات فوائد دورية
DVAR                     | تقدير التباين استناداً إلى عينة من إدخالات قاعدة البيانات المحددة
DVARP                    | حساب التباين استناداً إلى المحتوى بالكامل لإدخالات قاعدة البيانات المحددة
EDATE                    | إرجاع الرقم التسلسلي للتاريخ المشار إليه بعدد الأشهر قبل تاريخ البداية أو بعده
EFFECT                   | إرجاع النسبة الفعلية السنوية للفائدة
ENCODEURL                | إرجاع سلسلة مرمّزة بـ URL. هذه الدالة غير متوفرة في Excel للويب
EOMONTH                  | إرجاع الرقم التسلسلي لليوم الأخير من الشهر الذي يقع قبل عدد محدد من الأشهر أو يليه
ERF                      | إرجاع دالة الخطأ
ERF.PRECISE              | إرجاع دالة الخطأ
ERFC                     | إرجاع دالة الخطأ التكميلية
ERFC.PRECISE             | إرجاع دالة ERF التكميلية بالتكامل بين x وما لا نهاية
ERROR.TYPE               | إرجاع رقم مطابق لأحد أنواع الخطأ
EUROCONVERT              | تحويل رقم إلى عملة اليورو أو تحويل رقم من عملة اليورو إلى عملة اليورو لأي من الدول الأعضاء في الاتحاد الأوروبي أو تحويل رقم من عملة دولة عضو في الاتحاد الأوروبي إلى عملة دولة أخرى باستخدام اليورو كوسيط (التثليث)
EVEN                     | تقريب رقم إلى الأعلى إلى أقرب رقم صحيح زوجي
EXACT                    | التحقق من تطابق قيمتين نصيتين
EXP                      | ترجع e المرفوعة إلى أس أي رقم معين
EXPON.DIST               | إرجاع التوزيع الأسي
EXPONDIST                | إرجاع التوزيع الأسي. في Excel 2007، هذه الدالة هي دالة إحصائية
FACT                     | إرجاع مضروب لأحد الأرقام
FACTDOUBLE               | إرجاع المضروب المزدوج لأحد الأرقام
FALSE                    | إرجاع القيمة المنطقية FALSE
F.DIST                   | إرجاع توزيع الاحتمال F
FDIST                    | إرجاع توزيع الاحتمال F. في Excel 2007، هذه الدالة هي دالة إحصائية
F.DIST.RT                | إرجاع توزيع الاحتمال F
FIND                     | البحث عن إحدى القيم النصية داخل قيمة نصية أخرى (تحسس حالة الأحرف)
FINDB                    | البحث عن إحدى القيم النصية داخل قيمة نصية أخرى (تحسس حالة الأحرف)
F.INV                    | إرجاع عكس توزيع الاحتمال F
F.INV.RT                 | إرجاع عكس توزيع الاحتمال F
FINV                     | إرجاع عكس توزيع الاحتمال F. في Excel 2007، هذه الدالة هي دالة إحصائية
FISHER                   | إرجاع تحويل Fisher
FISHERINV                | إرجاع عكس تحويل Fisher
FIXED                    | تنسيق رقم كنص باستخدام عدد ثابت من المنازل العشرية
FLOOR                    | تقريب رقم للأسفل، باتجاه الصفر. في Excel 2007 وExcel 2010، هذه الدالة هي دالة رياضيات ومثلثات
FLOOR.MATH               | تقريب رقم للأسفل إلى أقرب عدد صحيح أو إلى أقرب مضاعف من المضاعفات ذات أهمية
FLOOR.PRECISE            | تقريب رقم إلى أقرب عدد صحيح أو إلى أقرب مضاعف ذي أهمية. يتم تقريب الرقم إلى الأعلى بغض النظر عن علامته
FORECAST                 | إرجاع قيمة موجودة على اتجاه خطي
FORECAST.LINEAR          | إرجاع قيمة موجودة على اتجاه خطي
FORMULATEXT              | إرجاع صيغة في مرجع معين كنص
FREQUENCY                | إرجاع توزيع تكراري كصفيف عمودي
F.TEST                   | إرجاع نتيجة اختبار F
FTEST                    | إرجاع نتيجة اختبار F. في Excel 2007، هذه الدالة هي دالة إحصائية
FV                       | إرجاع القيمة المستقبلية للاستثمار
FVSCHEDULE               | إرجاع القيمة المستقبلية لرأس المال الأولي بعد تطبيق سلسلة من نسب الفوائد المركبة
GAMMA                    | إرجاع قيمة دالة غاما
GAMMA.DIST               | إرجاع توزيع غاما
GAMMA.INV                | إرجاع عكس توزيع غاما التراكمي
GAMMADIST                | إرجاع توزيع غاما. في Excel 2007، هذه الدالة هي دالة إحصائية
GAMMAINV                 | إرجاع عكس توزيع غاما التراكمي. في Excel 2007، هذه الدالة هي دالة إحصائية
GAMMALN                  | إرجاع اللوغاريتم العادي لدالة غاما، Γ(x)
GAMMALN.PRECISE          | إرجاع اللوغاريتم العادي لدالة غاما، Γ(x)
GAUSS                    | إرجاع 0.5 أقل من التوزيع التراكمي القياسي العادي
GCD                      | إرجاع أكبر عامل قسمة مشترك
GEOMEAN                  | إرجاع الوسط الهندسي
GESTEP                   | اختبار ما إذا كان أحد الأرقام أكبر من قيمة البدء
GROWTH                   | إرجاع القيم الموجودة على اتجاه أسي
HARMEAN                  | إرجاع الوسط التوافقي
HEX2BIN                  | تحويل رقم سداسي عشري إلى رقم ثنائي
HEX2DEC                  | تحويل رقم سداسي عشري إلى رقم عشري
HEX2OCT                  | تحويل رقم سداسي عشري إلى رقم ثماني
HLOOKUP                  | البحث في الصف العلوي لصفيف وإرجاع قيمة الخلية المُشار إليها
HOUR                     | تحوّل رقم تسلسلي إلى ساعة
HYPERLINK                | إنشاء اختصار أو انتقال سريع يفتح مستنداً مخزناً على خادم شبكة أو إنترانت أو الإنترنت
HYPGEOM.DIST             | إرجاع توزيع الهندسة الفوقية
HYPGEOMDIST              | إرجاع توزيع الهندسة الفوقية. في Excel 2007، هذه الدالة هي دالة إحصائية
IF                       | تعيين اختبار منطقي لتنفيذه
IFERROR                  | إرجاع قيمة تحددها إذا تم تقييم الصيغة إلى خطأ؛ وخلاف ذلك، إرجاع نتيجة الصيغة
IFNA                     | إرجاع القيمة التي تحددها إذا تحوّل التعبير إلى #N/A، وبخلاف ذلك، يتم إرجاع نتيجة التعبير
IFS                      | التحقق مما إذا كانت تتم تلبيه شرط واحد أو أكثر وإرجاع قيمة تطابق شرط TRUE الأول
IMABS                    | يقوم بإرجاع القيمة المطلقة (المعامل) الخاصة بعدد مركب
IMAGINARY                | إرجاع المُعامل التخيلي لعدد مركب
IMARGUMENT               | إرجاع وسيطة ثيتا، وهي زاوية مقاسة بالتقدير الدائري
IMCONJUGATE              | إرجاع المرافق المركب لعدد مركب
IMCOS                    | إرجاع جيب التمام لعدد مركب
IMCOSH                   | إرجاع جيب التمام الزائدي لعدد مركب
IMCOT                    | إرجاع ظل التمام لعدد مركب
IMCSC                    | إرجاع قاطع التمام لعدد مركب
IMCSCH                   | إرجاع قاطع التمام الزائدي لعدد مركب
IMDIV                    | إرجاع حاصل قسمة رقمين مركبين
IMEXP                    | إرجاع الأس الخاص بعدد مركب
IMLN                     | إرجاع اللوغاريتم العادي لعدد مركب
IMLOG10                  | إرجاع لوغاريتم ذي أساس 10 لعدد مركب
IMLOG2                   | إرجاع لوغاريتم ذي أساس 2 لعدد مركب
IMPOWER                  | إرجاع عدد مركب تم رفعه لأس عدد صحيح
IMPRODUCT                | إرجاع ناتج الأعداد المركبة
IMREAL                   | إرجاع المُعامل الحقيقي لعدد مركب
IMSEC                    | إرجاع قاطع المنحنى لعدد مركب
IMSECH                   | إرجاع قاطع المنحنى الزائدي لعدد مركب
IMSIN                    | إرجاع جيب الزاوية لعدد مركب
IMSINH                   | إرجاع جيب الزاوية الزائدي لعدد مركب
IMSQRT                   | إرجاع الجذر التربيعي لعدد مركب
IMSUB                    | إرجاع الفرق بين عددين مركبين
IMSUM                    | إرجاع مجموع الأعداد المركبة
IMTAN                    | إرجاع ظل الزاوية الخاص بعدد مركب
INDEX                    | استخدام فهرس لاختيار قيمة من مرجع أو صفيف
INDIRECT                 | إرجاع مرجع مُشار إليه بقيمة نصية
INT                      | تقريب رقم إلى الأدنى إلى أقرب عدد صحيح
INTERCEPT                | إرجاع نقطة تقاطع خط الانحدار الخطي
INTRATE                  | إرجاع نسبة الفائدة لورقة مالية تم استثمارها بشكل كامل
IPMT                     | إرجاع مدفوعات الفوائد لاستثمار في فترة زمنية معينة
IRR                      | إرجاع معدل العائد الداخلي لسلسلة من التدفقات النقدية
ISBLANK                  | إرجاع TRUE إذا كانت القيمة فارغة
ISERR                    | إرجاع TRUE إذا كانت القيمة أي قيمة خطأ غير #N/A
ISERROR                  | إرجاع TRUE إذا كانت القيمة أي قيمة خطأ
ISEVEN                   | إرجاع القيمة TRUE إذا كان الرقم زوجياً
ISFORMULA                | إرجاع TRUE إذا كان هناك مرجع لخلية تحتوي على صيغة
ISLOGICAL                | إرجاع القيمة TRUE إذا كانت القيمة عبارة عن قيمة منطقية
ISNA                     | إرجاع القيمة TRUE إذا كانت القيمة عبارة عن قيمة الخطأ #N/A
ISNONTEXT                | إرجاع القيمة TRUE إذا لم تكن القيمة نصاً
ISNUMBER                 | إرجاع القيمة TRUE إذا كانت القيمة رقماً
ISODD                    | ترجع القيمة TRUE إذا كان الرقم فردياً
ISREF                    | إرجاع القيمة TRUE إذا كانت القيمة مرجعاً
ISTEXT                   | إرجاع القيمة TRUE إذا كانت القيمة نصاً
ISO.CEILING              | إرجاع رقم تم تقريبه إلى الأعلى، إلى أقرب عدد صحيح أو إلى أقرب مضاعف ذي أهمية
ISOWEEKNUM               | إرجاع رقم أسبوع ISO من العام لتاريخ محدد
ISPMT                    | حساب الفائدة المدفوعة خلال فترة معينة للاستثمار
KURT                     | ترجع تفرطح مجموعة البيانات
LARGE                    | إرجاع ترتيب القيم الكبرى في مجموعة بيانات
LCM                      | إرجاع أقل مضاعف مشترك
LEFT                     | إرجاع الأحرف الموجودة في أقصى اليسار من قيمة نصية
LEFTB                    | إرجاع الأحرف الموجودة في أقصى اليسار من قيمة نصية
LEN                      | ترجع عدد الأحرف في سلسلة نصية
LENB                     | ترجع عدد الأحرف في سلسلة نصية
LN                       | إرجاع اللوغاريتم العادي لأحد الأرقام
LOG                      | إرجاع لوغاريتم رقم إلى أساس معين
LOG10                    | إرجاع لوغاريتم ذي أساس 10 لأحد الأرقام
LOGEST                   | إرجاع معلمات اتجاه أسي
LOGINV                   | إرجاع عكس التوزيع اللوغاريتمي العادي التراكمي
LOGNORM.DIST             | إرجاع التوزيع اللوغاريتمي الطبيعي التراكمي
LOGNORM.INV              | إرجاع عكس التوزيع اللوغاريتمي العادي التراكمي
LOOKUP                   | البحث عن قيم في خط متجه أو صفيف
LOWER                    | تحول نص إلى أحرف صغيرة
MATCH                    | البحث عن قيم في مرجع أو صفيف
MAX                      | إرجاع القيمة القصوى في قائمة وسيطات
MAXA                     | إرجاع القيمة القصوى في قائمة وسيطات، بما في ذلك الأرقام والنصوص والقيم المنطقية
MAXIFS                   | إرجاع القيمة القصوى بين الخلايا المحددة بمجموعة معينة من الشروط أو المعايير
MDETERM                  | إرجاع محدد المصفوفة لصفيف
MDURATION                | إرجاع فترة ماكولي المعدلة للورقة المالية قيمة سعر تعادل مفترض يقدر بـ 100$
MEDIAN                   | إرجاع الوسيط للأرقام المعينة
MID                      | إرجاع عدد معين من الأحرف من سلسلة نصية بدءاً من الموضع الذي تحدده
MIDB                     | إرجاع عدد معين من الأحرف من سلسلة نصية بدءاً من الموضع الذي تحدده
MIN                      | إرجاع القيمة الدنيا في قائمة وسيطات
MINIFS                   | إرجاع أدنى قيمة بين الخلايا المحددة بمجموعة معينة من الشروط أو المعايير
MINA                     | إرجاع أصغر قيمة في قائمة وسيطات، بما في ذلك الأرقام والنصوص والقيم المنطقية
MINUTE                   | تحويل رقم تسلسلي إلى دقيقة
MINVERSE                 | إرجاع عكس المصفوفة لصفيف
MIRR                     | إرجاع النسبة الداخلية للعائد الذي يتم فيه توفير التدفقات المالية الموجبة والسالبة بنسب مختلفة
MMULT                    | إرجاع المصفوفة الناتجة عن ضرب صفيفين
MOD                      | إرجاع الباقي من القسمة
MODE                     | إرجاع القيمة الأكثر شيوعاً في مجموعة بيانات. في Excel 2007، هذه الدالة هي دالة إحصائية
MODE.MULT                | إرجاع صفيف عمودي للقيم الأكثر تكراراً أو الأكثر ظهوراً في صفيف أو نطاق من البيانات
MODE.SNGL                | إرجاع القيمة الأكثر شيوعاً في مجموعة بيانات
MONTH                    | تحويل رقم تسلسلي إلى شهر
MROUND                   | إرجاع رقم مقرب إلى المضاعف المطلوب
MULTINOMIAL              | إرجاع التسمية المتعددة لمجموعة من الأرقام
MUNIT                    | إرجاع مصفوفة الوحدة للبعد المحدد
N                        | إرجاع قيمة محولة لأحد الأرقام
NA                       | إرجاع قيمة الخطأ #N/A
NEGBINOM.DIST            | إرجاع التوزيع السالب ذي الحدين
NEGBINOMDIST             | إرجاع التوزيع السالب ذي الحدين. في Excel 2007، هذه الدالة هي دالة إحصائية
NETWORKDAYS              | إرجاع عدد أيام العمل بين تاريخين
NETWORKDAYS.INTL         | إرجاع عدد أيام العمل بالكامل بين تاريخين باستخدام المعلمات لتحديد أيام عطلة الأسبوع وعددها
NOMINAL                  | إرجاع معدل الفائدة السنوية الاسمية
NORM.DIST                | إرجاع التوزيع التراكمي العادي
NORM.INV                 | إرجاع عكس التوزيع التراكمي العادي. في Excel 2007، هذه الدالة هي دالة إحصائية
NORM.S.DIST              | إرجاع التوزيع التراكمي العادي القياسي
NORM.S.INV               | إرجاع عكس التوزيع التراكمي العادي القياسي
NORMDIST                 | إرجاع التوزيع التراكمي العادي. في Excel 2007، هذه الدالة هي دالة إحصائية
NORMINV                  | إرجاع عكس التوزيع التراكمي العادي
NORMSDIST                | إرجاع التوزيع التراكمي العادي القياسي. في Excel 2007، هذه الدالة هي دالة إحصائية
NORMSINV                 | إرجاع عكس التوزيع التراكمي العادي القياسي. في Excel 2007، هذه الدالة هي دالة إحصائية
NOT                      | عكس منطق الوسيطة الخاصة بها
NOW                      | إرجاع الرقم التسلسلي للتاريخ والوقت الحالي
NPER                     | إرجاع عدد الفترات للاستثمار
NPV                      | إرجاع القيمة الحالية الصافية لاستثمار بالاستناد إلى سلسلة من التدفقات النقدية الدورية ومعدل الخصم
OCT2BIN                  | تحويل رقم ثماني إلى رقم ثنائي
OCT2DEC                  | تحويل رقم ثماني إلى رقم عشري
OCT2HEX                  | تحويل رقم ثماني إلى رقم ست عشري
ODD                      | تقريب رقم إلى الأعلى إلى أقرب رقم صحيح فردي
ODDFPRICE                | إرجاع السعر لكل قيمة اسمية لـ 100$ لورقة مالية في جزء أول من فترة كلية
ODDFYIELD                | إرجاع العائد الخاص بالورقة المالية في جزء أول من فترة كلية
ODDLPRICE                | إرجاع السعر لكل قيمة اسمية لـ 100$ لورقة مالية في جزء أخير من فترة كلية
ODDLYIELD                | إرجاع عائد ورقة مالية في جزء أخير من فترة كلية
OR                       | إرجاع TRUE إذا كانت أية وسيطة TRUE
PDURATION                | إرجاع عدد الفترات المطلوب بواسطة استثمار للوصول إلى قيمة محددة
PEARSON                  | إرجاع مربع معامل الارتباط العزومي لحواصل الضرب
PERCENTILE.EXC           | إرجاع النسب المئوية القيمة المئوية k للقيم ضمن نطاق، حيث يقع k في النطاق من 0 إلى 1، حصراً
PERCENTILE.INC           | إرجاع النسب المئوية للقيم في نطاق
PERCENTILE               | إرجاع النسب المئوية للقيم في نطاق. في Excel 2007، هذه الدالة هي دالة إحصائية
PERCENTRANK.EXC          | إرجاع رتبة القيمة في مجموعة بيانات كنسبة مئوية (من 0 إلى 1 حصراً) من مجموعة البيانات
PERCENTRANK.INC          | إرجاع رتبة النسبة المئوية لقيمة في مجموعة بيانات
PERCENTRANK              | إرجاع رتبة النسبة المئوية لقيمة في مجموعة بيانات. في Excel 2007، هذه الدالة هي دالة إحصائية
PERMUT                   | إرجاع عدد التباديل لعدد محدد من العناصر
PERMUTATIONA             | إرجاع عدد التباديل لعدد محدد من العناصر (مع التكرارات) التي يمكن تحديدها من إجمالي العناصر
PHI                      | إرجاع قيمة دالة كثافة التوزيع القياسي العادي
PI                       | إرجاع قيمة pi
PMT                      | إرجاع الدفعات الدورية لمرتب دوري
POISSON                  | إرجاع توزيع Poisson. في Excel 2007، هذه الدالة هي دالة إحصائية
POISSON.DIST             | إرجاع توزيع Poisson
POWER                    | إرجاع نتيجة عدد مرفوع إلى أس
PPMT                     | إرجاع المدفوعات على رأس مال لاستثمار في فترة زمنية معينة
PRICE                    | إرجاع السعر لكل قيمة اسمية لـ 100 ر. س. لورقة مالية يستحق عنها فائدة دورية
PRICEDISC                | إرجاع القيمة الاسمية لسعر كل 100 ر. س. لورقة مالية ذات خصم
PRICEMAT                 | إرجاع السعر لكل قيمة اسمية لـ 100$ لورقة مالية تُدفع فائدتها عند الاستحقاق
PROB                     | إرجاع احتمال وقوع قيم النطاق بين حدين
PRODUCT                  | ضرب الوسيطات الخاصة بالدالة
PROPER                   | تغيير الحرف الأول إلى حرف كبير في كل كلمة من قيمة نصية
PV                       | إرجاع القيمة الحالية للاستثمار
QUARTILE                 | إرجاع ربع مجموعة بيانات. في Excel 2007، هذه الدالة هي دالة إحصائية
QUARTILE.EXC             | إرجاع ربع مجموعة البيانات، استناداً إلى قيم النسب المئوية من 0 إلى 1 حصراً
QUARTILE.INC             | إرجاع ربع مجموعة بيانات
QUOTIENT                 | إرجاع جزء العدد الصحيح الخاص بالقسمة
RADIANS                  | تحويل الدرجات إلى التقدير الدائري
RAND                     | إرجاع رقم عشوائي بين 0 و1
RANDBETWEEN              | إرجاع رقم عشوائي بين الأرقام التي تحددها
RANK.EQ                  | إرجاع رتبة رقم في قائمة الأرقام
RANK                     | إرجاع رتبة رقم في قائمة الأرقام. في Excel 2007، هذه الدالة هي دالة إحصائية
RATE                     | إرجاع معدل الفائدة لكل فترة من فترات المرتب الدوري
RECEIVED                 | ترجع مقدار المبلغ الذي سيتم تلقيه عند تاريخ الاستحقاق لورقة مالية تم استثمارها بشكل كامل
REPLACE                  | استبدال الأحرف ضمن نص
REPLACEB                 | استبدال الأحرف ضمن نص
REPT                     | تكرار النص لعدد معين من المرات
RIGHT                    | إرجاع الأحرف الموجودة في أقصى اليمين من قيمة نصية
RIGHTB                   | إرجاع الأحرف الموجودة في أقصى اليمين من قيمة نصية
ROMAN                    | تحويل الأرقام العربية إلى رومانية على شكل نص
ROUND                    | تقريب رقم إلى عدد خانات رقمية معين
ROUNDDOWN                | تقريب رقم للأسفل، باتجاه الصفر
ROUNDUP                  | تقريب رقم للأعلى، بعيداً عن الصفر
ROW                      | إرجاع رقم الصف لمرجع
ROWS                     | إرجاع عدد الصفوف الموجودة في مرجع
RRI                      | إرجاع معدل فائدة يكون مكافئاً لنمو الاستثمار
RSQ                      | إرجاع مربع معامل الارتباط العزومي لحواصل الضرب
SEARCH                   | البحث عن إحدى القيم النصية داخل قيمة نصية أخرى (عدم تحسس حالة الأحرف)
SEARCHB                  | البحث عن إحدى القيم النصية داخل قيمة نصية أخرى (عدم تحسس حالة الأحرف)
SEC                      | إرجاع قاطع المنحنى لزاوية
SECH                     | إرجاع قاطع المنحنى الزائدي لزاوية
SECOND                   | تحويل رقم تسلسلي إلى ثانية
SERIESSUM                | إرجاع مجموع سلسلة الأس استناداً إلى الصيغة
SHEET                    | إرجاع رقم الورقة للورقة المشار إليها
SHEETS                   | إرجاع عدد الأوراق في مرجع
SIGN                     | إرجاع إشارة لأحد الأرقام
SIN                      | إرجاع جيب الزاوية لزاوية معينة
SINH                     | إرجاع جيب الزاوية الزائدي لأحد الأرقام
SKEW                     | إرجاع تخالف التوزيع
SKEW.P                   | إرجاع تخالف التوزيع استناداً إلى محتوى: وصف لدرجة اللا تماثل لتوزيع حول وسطه
SLN                      | إرجاع الإهلاك الثابت لأصل في فترة زمنية واحدة
SLOPE                    | إرجاع ميل خط الانحدار الخطي
SMALL                    | إرجاع ترتيب القيم الصغرى في مجموعة بيانات
SORT                     | تقوم بفرز محتويات نطاق أو صفيف
SQRTPI                   | إرجاع الجذر التربيعي لـ (number \* pi)
STANDARDIZE              | إرجاع قيمة مسوّاة
STDEV                    | تقدير الانحراف المعياري استناداً إلى نموذج
STDEV.P                  | حساب الانحراف المعياري استناداً إلى المحتوى بأكمله
STDEV.S                  | تقدير الانحراف المعياري استناداً إلى نموذج
STDEVA                   | تقدير الانحراف المعياري استناداً إلى نموذج، بما في ذلك الأرقام والنصوص والقيم المنطقية
STDEVP                   | حساب الانحراف المعياري استناداً إلى المحتوى بأكمله. في Excel 2007، هذه الدالة هي دالة إحصائية
STDEVPA                  | حساب الانحراف المعياري استناداً إلى المحتوى بأكمله، بما في ذلك الأرقام والنصوص والقيم المنطقية
STEYX                    | إرجاع الخطأ القياسي لقيم y المتوقعة وذلك من أجل كل قيمة x في انحدار
SUBSTITUTE               | استبدال نص قديم بنص جديد في سلسلة نصية
SUBTOTAL                 | إرجاع مجموع فرعي في قائمة أو قاعدة بيانات
SUM                      | جمع الوسيطات الخاصة بالدالة
SUMIF                    | جمع الخلايا المحددة بواسطة معيار معين
SUMIFS                   | جمع الخلايا الموجودة في نطاق والتي تفي بمعايير متعددة
SUMPRODUCT               | إرجاع مجموع المنتجات الخاص بمكونات الصفائف المتطابقة
SUMSQ                    | إرجاع مجموع مربعات الوسيطات
SUMX2MY2                 | إرجاع مجموع الفوارق بين المربعات للقيم المناظرة في صفيفين
SUMX2PY2                 | إرجاع المجموع الخاص بمجموع مربعات قيم مناظرة في صفيفين
SUMXMY2                  | إرجاع مجموع مربعات فوارق القيم المناظرة في صفيفين
SWITCH                   | تقييم تعبير مقابل الحصول على قائمة بالقيم وإرجاع النتيجة المطابقة للقيمة المطابقة الأولى. إذا لم يكن هناك أي تطابق، قد يتم إرجاع القيمة الافتراضية الاختيارية
SYD                      | إرجاع أرقام مجموع سنوات استهلاك أحد الأصول لفترة معيّنة
T                        | تحويل الوسيطات الخاصة بالدالة إلى نص
TAN                      | إرجاع ظل الزاوية لأحد الأرقام
TANH                     | ترجع ظل الزاوية الزائدية لأحد الأرقام
TBILLEQ                  | إرجاع العائد المساوي للسند لإذن الخزانة
TBILLPRICE               | إرجاع السعر لكل قيمة اسمية لـ 100$ لإذن خزانة
TBILLYIELD               | إرجاع العائد الخاص بإذن الخزانة
T.DIST                   | إرجاع نقاط النسبة المئوية (الاحتمال) لتوزيع t للطالب
T.DIST.2T                | إرجاع نقاط النسبة المئوية (الاحتمال) لتوزيع t للطالب
T.DIST.RT                | إرجاع توزيع t للطالب
TDIST                    | إرجاع توزيع t للطالب
TEXT                     | تنسق رقم وتحوله إلى نص
TEXTAFTER                | ترجع النص الذي يقع بعد حرف أو سلسلة معينة
TEXTBEFORE               | ترجع النص الذي يقع قبل حرف أو سلسلة معينة
TEXTJOIN                 | تدمج النص من نطاقات و/أو سلاسل متعددة
TIME                     | إرجاع الرقم التسلسلي لوقت معين
TIMEVALUE                | تحويل وقت في شكل نص إلى رقم تسلسلي
T.INV                    | إرجاع القيمة t لتوزيع t للطالب كدالة الاحتمال ودرجات الحرية
T.INV.2T                 | إرجاع عكس توزيع t للطالب
TINV                     | ترجع عكس توزيع T ستيودنت الاحتمالي
TODAY                    | إرجاع الرقم التسلسلي لتاريخ اليوم
TRANSPOSE                | إرجاع الموضع البديل لصفيف
TREND                    | إرجاع القيم الموجودة على الاتجاه الخطي
TRIM                     | إزالة المسافات من نص
TRIMMEAN                 | إرجاع وسط الجزء الداخلي من مجموعة بيانات
TRUE                     | إرجاع القيمة المنطقية TRUE
TRUNC                    | اقتطاع رقم إلى عدد صحيح
T.TEST                   | إرجاع الاحتمال المقترن باختبار الطالب t-test
TTEST                    | إرجاع الاحتمال المقترن باختبار الطالب t-test. في Excel 2007، هذه الدالة هي دالة إحصائية
TYPE                     | إرجاع رقم يشير إلى نوع بيانات قيمة ما
UNICHAR                  | ارجاع الحرف Unicode الذي تشير إليه قيمة رقمية معينة
UNICODE                  | إرجاع الرقم (نقطة الرمز) المقابل للحرف الأول من النص
UPPER                    | تحويل نص إلى أحرف كبيرة
VALUE                    | تحول وسيطة نصية لرقم
VALUETOTEXT              | ترجع نص من أي قيمة محددة
VAR                      | تقدير التباين استناداً إلى نموذج. في Excel 2007، هذه الدالة هي دالة إحصائية
VAR.P                    | حساب التباين استناداً إلى المحتوى بأكمله
VAR.S                    | تقدير التباين استناداً إلى نموذج
VARA                     | تقدير التباين استناداً إلى نموذج، بما في ذلك الأرقام والنصوص والقيم المنطقية
VARP                     | حساب التباين استناداً إلى المحتوى بأكمله. في Excel 2007، هذه الدالة هي دالة إحصائية
VARPA                    | حساب التباين استناداً إلى المحتوى بأكمله، بما في ذلك الأرقام والنصوص والقيم المنطقية
VDB                      | إرجاع إهلاك الأصول لفترة محددة أو جزئية باستخدام أسلوب الاستهلاك المتناقص
VLOOKUP                  | تبحث في العمود الأول لصفيف والتنقل عبر خلايا الصف لإرجاع قيمة خلية
WEEKDAY                  | تحويل رقم تسلسلي إلى يوم من أيام الأسبوع
WEEKNUM                  | تحويل رقم تسلسلي إلى رقم يمثل رقم الأسبوع في السنة
WEIBULL                  | حساب التباين استناداً إلى المحتوى بأكمله، بما في ذلك الأرقام والنصوص والقيم المنطقية. في Excel 2007، هذه الدالة هي دالة إحصائية
WEIBULL.DIST             | إرجاع توزيع Weibull
WORKDAY                  | إرجاع الرقم التسلسلي لتاريخ يقع قبل عدد معين من أيام العمل أو بعده
WORKDAY.INTL             | ترجع الرقم التسلسلي لتاريخ يقع قبل عدد أيام عمل معين أو بعده باستخدام معلمات لتحديد أيام نهايات الأسبوع وعددها
XIRR                     | إرجاع معدل العائد الداخلي لجدول تدفقات نقدية غير دورية بالضرورة
XLOOKUP                  | يبحث في نطاق أو مصفوفة، ويعيد عنصراً مطابقاً للمطابقة الأولى التي يعثر عليها. إذا لم يكن هناك تطابق، فيمكن لدالة XLOOKUP إرجاع أقرب تطابق (تقريبي)
XNPV                     | إرجاع القيمة الحالية الصافية لجدول تدفقات نقدية غير دورية بالضرورة
XOR                      | إرجاع Exclusive OR منطقية لكل الوسيطات
YEAR                     | تحويل رقم تسلسلي إلى سنة
YEARFRAC                 | إرجاع كسر السنة الذي يمثل عدد الأيام الكاملة التي تقع بين تاريخ البدء start_date وتاريخ الانتهاء end_date
YIELD                    | إرجاع العائد الخاص بالورقة المالية التي يستحق عنها فائدة دورية
YIELDDISC                | إرجاع العائد السنوي لورقة مالية عليها خصم؛ على سبيل المثال، إذن الخزانة
YIELDMAT                 | إرجاع العائد السنوي لورقة مالية تُدفع فائدتها عند الاستحقاق
Z.TEST                   | إرجاع قيمة الاحتمال وحيد الطرف لـ z-test
ZTEST                    | إرجاع قيمة الاحتمال وحيد الطرف لـ z-test. في Excel 2007، هذه الدالة هي دالة إحصائية
