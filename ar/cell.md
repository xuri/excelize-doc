# الخليه

يقوم RichTextRun بتعيين إعدادات تشغيل النص المنسق مباشرةً.

```go
type RichTextRun struct {
    Font *Font
    Text string
}
```

## تعيين قيمة الخلية {#SetCellValue}

```go
func (f *File) SetCellValue(sheet, axis string, value interface{}) error
```

يوفر SetCellValue دالة لتعيين قيمة خلية. يجب ألا تكون الإحداثيات المحددة في الصف الأول من الجدول. يوضح ما يلي أنواع البيانات المدعومة:

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

## تعيين قيمة منطقية {#SetCellBool}

```go
func (f *File) SetCellBool(sheet, axis string, value bool) error
```

يوفر SetCellBool وظيفة لتعيين قيمة نوع منطقي لخلية من خلال اسم ورقة العمل المحدد وإحداثيات الخلية وقيمة الخلية.

## تعيين قيمة RAW {#SetCellDefault}

```go
func (f *File) SetCellDefault(sheet, axis, value string) error
```

يوفر SetCellDefault وظيفة لتعيين قيمة نوع السلسلة لخلية كتنسيق افتراضي دون هروب الخلية.

## تعيين قيمة عدد صحيح {#SetCellInt}

```go
func (f *File) SetCellInt(sheet, axis string, value int) error
```

يوفر SetCellInt دالة لتعيين قيمة نوع int لخلية من خلال اسم ورقة العمل المحدد وإحداثيات الخلية وقيمة الخلية.

## تعيين قيمة السلسلة {#SetCellStr}

```go
func (f *File) SetCellStr(sheet, axis, value string) error
```

يوفر SetCellStr وظيفة لتعيين قيمة نوع السلسلة للخلية. العدد الإجمالي للأحرف التي يمكن أن تحتويها الخلية على `32767` حرفًا.

## تعيين نمط الخلية {#SetCellStyle}

```go
func (f *File) SetCellStyle(sheet, hcell, vcell string, styleID int) error
```

يوفر SetCellStyle وظيفة لإضافة سمة نمط للخلايا من خلال اسم ورقة العمل المعطى ومنطقة الإحداثيات ومعرف النمط. يمكن الحصول على فهارس النمط من خلال وظيفة [`NewStyle`](style.md#NewStyle). لاحظ أن حد النوع `diagonalDown` و `diagonalUp` يجب أن يستخدموا نفس اللون في نفس منطقة الإحداثيات.

- المثال 1 ، أنشئ حدودًا للخلية `D7` في `Sheet1`:

```go
style, err := f.NewStyle(`{
    "border": [
    {
        "type": "left",
        "color": "0000FF",
        "style": 3
    },
    {
        "type": "top",
        "color": "00FF00",
        "style": 4
    },
    {
        "type": "bottom",
        "color": "FFFF00",
        "style": 5
    },
    {
        "type": "right",
        "color": "FF0000",
        "style": 6
    },
    {
        "type": "diagonalDown",
        "color": "A020F0",
        "style": 7
    },
    {
        "type": "diagonalUp",
        "color": "A020F0",
        "style": 8
    }]
}`)
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_01.png" alt="تعيين نمط حد لخلية"></p>

تم تعيين الحدود الأربعة للخلية `D7` بأنماط وألوان مختلفة. يرتبط هذا بالمعلمات عند استدعاء وظيفة [`NewStyle`](style.md#NewStyle). تحتاج إلى تعيين أنماط مختلفة للإشارة إلى الوثائق الخاصة بهذا الفصل.

- المثال 2 ، تعيين نمط التدرج لخلية ورقة العمل `D7` المسماة `Sheet1`:

```go
style, err := f.NewStyle(`{"fill":{"type":"gradient","color":["#FFFFFF","#E0EBF5"],"shading":1}}`)
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_02.png" alt="قم بتعيين نمط متدرج للخلية"></p>

تم تعيين الخلية `D7` بتعبئة اللون لتأثير التدرج. يرتبط تأثير التعبئة المتدرجة بالمعامل عند استدعاء الوظيفة [`NewStyle`](style.md#NewStyle). تحتاج إلى تعيين أنماط مختلفة للإشارة إلى وثائق هذا الفصل.

- مثال 3 ، عيّن تعبئة خالصة للخلية `D7` المسماة `Sheet1`:

```go
style, err := f.NewStyle(`{"fill":{"type":"pattern","color":["#E0EBF5"],"pattern":1}}`)
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
style, err := f.NewStyle(`{
    "alignment":
    {
        "horizontal": "center",
        "ident": 1,
        "justify_last_line": true,
        "reading_order": 0,
        "relative_indent": 1,
        "shrink_to_fit": true,
        "text_rotation": 45,
        "vertical": "",
        "wrap_text": true
    }
}`)
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
style, err := f.NewStyle(`{"number_format": 22}`)
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
style, err := f.NewStyle(`{
    "font":
    {
        "bold": true,
        "italic": true,
        "family": "Times New Roman",
        "size": 36,
        "color": "#777777"
    }
}`)
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_06.png" alt="تعيين الخط وحجم الخط واللون ونمط الانحراف للخلايا"></p>

- مثال 7 ، تأمين وإخفاء خلية ورقة العمل `D7` المسماة `Sheet1`:

```go
style, err := f.NewStyle(`{"protection":{"hidden":true, "locked":true}}`)
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

لتأمين خلية أو إخفاء صيغة ، قم بحماية ورقة العمل. في علامة التبويب "مراجعة" ، انقر فوق "حماية ورقة العمل".

## تعيين ارتباط تشعبي {#SetCellHyperLink}

```go
func (f *File) SetCellHyperLink(sheet, axis, link, linkType string) error
```

يوفر SetCellHyperLink وظيفة لتعيين الارتباطات التشعبية للخلايا عن طريق اسم ورقة العمل وعنوان URL للرابط. يعرّف LinkType نوعين من الارتباطات التشعبية  `External` لموقع الويب أو `Location` للانتقال إلى إحدى الخلايا في هذا المصنف. الحد الأقصى للارتباطات التشعبية في ورقة العمل هو `65530`. أدناه مثال على ارتباط خارجي.

- مثال 1 ، إضافة ارتباط خارجي إلى الخلية `A3` من ورقة العمل المسماة `Sheet1`:

```go
err := f.SetCellHyperLink("Sheet1", "A3",
    "https://github.com/360EntSecGroup-Skylar/excelize", "External")
// عيّن الخط ونمط التسطير للخلية
style, err := f.NewStyle(`{"font":{"color":"#1265BE","underline":"single"}}`)
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

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    f := excelize.NewFile()
    if err := f.SetRowHeight("Sheet1", 1, 35); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SetSheetViewOptions("Sheet1", -1,
        excelize.RightToLeft(true),
    ); err != nil {
        fmt.Println(err)
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
                Color:  "2354e8",
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
            Text: "italic",
            Font: &excelize.Font{
                Bold:   true,
                Color:  "e83723",
                Italic: true,
                Family: "Times New Roman",
            },
        },
        {
            Text: "text with color and font-family,",
            Font: &excelize.Font{
                Bold:   true,
                Color:  "2354e8",
                Family: "Times New Roman",
            },
        },
        {
            Text: "\r\nlarge text with ",
            Font: &excelize.Font{
                Size:  14,
                Color: "ad23e8",
            },
        },
        {
            Text: "strike",
            Font: &excelize.Font{
                Color:  "e89923",
                Strike: true,
            },
        },
        {
            Text: " and ",
            Font: &excelize.Font{
                Size:  14,
                Color: "ad23e8",
            },
        },
        {
            Text: "underline.",
            Font: &excelize.Font{
                Color:     "23e833",
                Underline: "single",
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

## الحصول على قيمة الخلية {#GetCellValue}

```go
func (f *File) GetCellValue(sheet, axis string) (string, error)
```

يتم استرداد قيمة الخلية وفقًا لورقة العمل المحددة وإحداثيات الخلية ، ويتم تحويل قيمة الإرجاع إلى نوع `string`. إذا كان من الممكن تطبيق تنسيق الخلية على قيمة خلية ، فسيتم إرجاع القيمة المطبقة ، وإلا سيتم إرجاع القيمة الأصلية.

## الحصول على كل قيمة الخلية حسب الأعمدة {#GetCols}

```go
func (f *File) GetCols(sheet string) ([][]string, error)
```

الحصول على قيمة جميع الخلايا حسب الأعمدة في ورقة العمل بناءً على اسم ورقة العمل المحدد (حساس لحالة الأحرف) ، والتي يتم إرجاعها كمصفوفة ثنائية الأبعاد ، حيث يتم تحويل قيمة الخلية إلى نوع `string`. إذا كان يمكن تطبيق تنسيق الخلية على قيمة الخلية ، فسيتم استخدام القيمة المطبقة ، وإلا فسيتم استخدام القيمة الأصلية.

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
func (f *File) GetRows(sheet string) ([][]string, error)
```

الحصول على قيمة جميع الخلايا حسب الصفوف في ورقة العمل بناءً على اسم ورقة العمل المحدد (حساس لحالة الأحرف) ، والتي يتم إرجاعها كمصفوفة ثنائية الأبعاد ، حيث يتم تحويل قيمة الخلية إلى نوع `string`. إذا كان يمكن تطبيق تنسيق الخلية على قيمة الخلية ، فسيتم استخدام القيمة المطبقة ، وإلا فسيتم استخدام القيمة الأصلية.

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
func (f *File) GetCellHyperLink(sheet, axis string) (bool, string, error)
```

الحصول على ارتباط تشعبي للخلية بناءً على اسم ورقة العمل المحددة (حساسة لحالة الأحرف) وإحداثيات الخلية. إذا كانت الخلية تحتوي على ارتباط تشعبي ، فستعرض `true` وعنوان الارتباط ، وإلا ستعرض `false` وعنوان ارتباط فارغ.

على سبيل المثال ، احصل على ارتباط تشعبي لخلية `H6` في ورقة عمل باسم `Sheet1`:

```go
link, target, err := f.GetCellHyperLink("Sheet1", "H6")
```

## الحصول على فهرس النمط {#GetCellStyle}

```go
func (f *File) GetCellStyle(sheet, axis string) (int, error)
```

يتم الحصول على فهرس نمط الخلية من اسم ورقة العمل المحددة (حساسة لحالة الأحرف) وإحداثيات الخلية ، ويمكن استخدام الفهرس الذي تم الحصول عليه كمعامل لاستدعاء وظيفة `SetCellValue` عند نسخ نمط الخلية.

## دمج الخلايا {#MergeCell}

```go
func (f *File) MergeCell(sheet, hcell, vcell string) error
```

دمج الخلايا بناءً على اسم ورقة العمل المحدد (حساس لحالة الأحرف) ومناطق إحداثيات الخلية. على سبيل المثال ، ادمج الخلايا في منطقة `D3:E9` في ورقة عمل تسمى `Sheet1`:

```go
err := f.MergeCell("Sheet1", "D3", "E9")
```

إذا تداخلت منطقة إحداثيات الخلية المحددة مع الخلايا المدمجة الأخرى الموجودة ، فسيتم حذف الخلايا المدمجة الحالية.

## خلايا إلغاء الدمج {#UnmergeCell}

```go
func (f *File) UnmergeCell(sheet string, hcell, vcell string) error
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

## إضافة تعليق {#AddComment}

```go
func (f *File) AddComment(sheet, cell, format string) error
```

يوفر AddComment طريقة لإضافة التعليقات في ورقة من خلال فهرس ورقة العمل والخلية ومجموعة التنسيق (مثل المؤلف والنص). لاحظ أن الحد الأقصى لطول المؤلف هو 255 والحد الأقصى لطول النص هو 32512. على سبيل المثال ، أضف تعليقًا في `Sheet1!$A$3`:

<p align="center"><img width="613" src="./images/comment.png" alt="أضف تعليقًا إلى مستند Excel"></p>

```go
err := f.AddComment("Sheet1", "A3", `{"author":"Excelize: ","text":"هذا تعليق."}`)
```

## الحصول على تعليق {#GetComments}

```go
func (f *File) GetComments() (comments map[string][]Comment)
```

يقوم GetComments باسترداد جميع التعليقات وإرجاع خريطة اسم ورقة العمل إلى تعليقات ورقة العمل.

## تعيين صيغة الخلية {#SetCellFormula}

```go
func (f *File) SetCellFormula(sheet, axis, formula string, opts ...FormulaOpts) error
```

يتم أخذ الصيغة الموجودة في الخلية وفقًا لاسم ورقة العمل المحدد (حساس لحالة الأحرف) وإعدادات صيغة الخلية. يتم حساب نتيجة الصيغة عندما يتم فتح ورقة العمل بواسطة تطبيق Office Excel ، ولا يوفر Excelize حاليًا محرك حساب الصيغة ، لذلك لا يمكن حساب نتائج الصيغة.

## الحصول على صيغة الخلية {#GetCellFormula}

```go
func (f *File) GetCellFormula(sheet, axis string) (string, error)
```

احصل على الصيغة في الخلية بناءً على اسم ورقة العمل المحددة (حساسة لحالة الأحرف) وإحداثيات الخلية.

## حساب قيمة الخلية {#CalcCellValue}

```go
func (f *File) CalcCellValue(sheet, cell string) (result string, err error)
```

توفر CalcCellValue دالة للحصول على قيمة الخلية المحسوبة. هذه الميزة قيد المعالجة حاليًا. صيغة الصفيف وصيغة الجدول وبعض الصيغ الأخرى غير مدعومة حاليًا.

الصيغ المدعومة:

```text
ABS, ACOS, ACOSH, ACOT, ACOTH, AND, ARABIC, ASIN, ASINH, ATAN2, ATANH,
BASE, CEILING, CEILING.MATH, CEILING.PRECISE, COMBIN, COMBINA, COS,
COSH, COT, COTH, COUNTA, CSC, CSCH, DECIMAL, DEGREES, EVEN, EXP, FACT,
FACTDOUBLE, FLOOR, FLOOR.MATH, FLOOR.PRECISE, GCD, INT, ISBLANK, ISERR,
ISERROR, ISEVEN, ISNA, ISNONTEXT, ISNUMBER, ISO.CEILING, ISODD, LCM,
LN, LOG, LOG10, MDETERM, MEDIAN, MOD, MROUND, MULTINOMIAL, MUNIT, NA,
ODD, OR, PI, POWER, PRODUCT, QUOTIENT, RADIANS, RAND, RANDBETWEEN,
ROUND, ROUNDDOWN, ROUNDUP, SEC, SECH, SIGN, SIN, SINH, SQRT, SQRTPI,
SUM, SUMIF, SUMSQ, TAN, TANH, TRUNC
```
