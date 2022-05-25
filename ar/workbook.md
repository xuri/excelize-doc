# دفتر العمل

يحدد `Options` الخيارات لفتح جداول البيانات وقراءتها.

```go
type Options struct {
    Password          string
    RawCellValue      bool
    UnzipSizeLimit    int64
    UnzipXMLSizeLimit int64
}
```

تحدد `Password` كلمة مرور جدول البيانات بنص عادي.

يحدد `RawCellValue` ما إذا كان يتم تطبيق تنسيق الأرقام لقيمة الخلية أو الحصول على القيمة الأولية.

يحدّد `UnzipSizeLimit` حد حجم فك الضغط بالبايت عند فتح جدول البيانات ، ويجب أن تكون هذه القيمة أكبر من أو تساوي `UnzipXMLSizeLimit` ، الحد الافتراضي للحجم هو 16 غيغابايت.

يحدد `UnzipXMLSizeLimit` حد الذاكرة لفك ضغط ورقة العمل بالبايت ، وسيتم استخراج XML لورقة العمل إلى دليل النظام المؤقت عندما يكون حجم الملف أكبر من هذه القيمة ، يجب أن تكون هذه القيمة أقل من أو تساوي `UnzipSizeLimit` ، القيمة الافتراضية هي 16 ميغا بايت.

## قم بإنشاء جدول بيانات {#NewFile}

```go
func NewFile() *File
```

يوفر `NewFile` وظيفة لإنشاء ملف جديد بواسطة القالب الافتراضي. سيحتوي المصنف الذي تم إنشاؤه حديثًا بشكل افتراضي على ورقة عمل باسم `Sheet1`. فمثلا:

## افتح {#OpenFile}

```go
func OpenFile(filename string, opt ...Options) (*File, error)
```

يأخذ OpenFile اسم ملف جدول البيانات ويعيد بنية ملف جدول بيانات معبأة له. على سبيل المثال ، افتح جدول بيانات محميًا بكلمة مرور:

```go
f, err := excelize.OpenFile("المصنف1.xlsx", excelize.Options{Password: "password"})
if err != nil {
    return
}
```

لاحظ أن excelize يدعم فقط فك التشفير ولا يدعم التشفير حاليًا ، وسيكون جدول البيانات المحفوظ بواسطة [`Save`](workbook.md#Save) و [`SaveAs()`](workbook.md#SaveAs) بدون كلمة مرور غير محمية. أغلق الملف عن طريق [`Close()`](workbook.md#Close) بعد فتح جدول البيانات.

## فتح دفق البيانات {#OpenReader}

```go
func OpenReader(r io.Reader, opt ...Options) (*File, error)
```

يقوم OpenReader بقراءة دفق البيانات من `io.Reader` وإرجاع ملف جدول بيانات ممتلئ.

على سبيل المثال ، أنشئ خادم HTTP للتعامل مع قالب التحميل ، ثم استجابة ملف التنزيل مع إضافة ورقة عمل جديدة:

```go
package main

import (
    "fmt"
    "net/http"

    "github.com/xuri/excelize/v2"
)

func process(w http.ResponseWriter, req *http.Request) {
    file, _, err := req.FormFile("file")
    if err != nil {
        fmt.Fprintf(w, err.Error())
        return
    }
    defer file.Close()
    f, err := excelize.OpenReader(file)
    if err != nil {
        fmt.Fprintf(w, err.Error())
        return
    }
    f.NewSheet("NewSheet")
    w.Header().Set("Content-Disposition", "attachment; filename=Book1.xlsx")
    w.Header().Set("Content-Type", req.Header.Get("Content-Type"))
    if _, err := f.WriteTo(w); err != nil {
        fmt.Fprintf(w, err.Error())
    }
    return
}

func main() {
    http.HandleFunc("/process", process)
    http.ListenAndServe(":8090", nil)
}
```

اختبار مع cURL:

```bash
curl --location --request GET 'http://127.0.0.1:8090/process' \
--form 'file=@/tmp/template.xlsx' -O -J
curl: Saved to filename 'Book1.xlsx'
```

## حفظ {#Save}

```go
func (f *File) Save() error
```

يوفر Save وظيفة لتجاوز جدول البيانات بمسار الأصل.

## حفظ باسم {#SaveAs}

```go
func (f *File) SaveAs(name string) error
```

يوفر SaveAs وظيفة لإنشاء أو تحديث جدول بيانات في المسار المتوفر.

## إغلاق المصنف {#Close}

```go
func (f *File) Close() error
```

يقوم Close بإغلاق وتنظيف الملف المؤقت المفتوح لجدول البيانات.

## قم بإنشاء ورقة عمل {#NewSheet}

```go
func (f *File) NewSheet(name string) int
```

يوفر NewSheet وظيفة لإنشاء ورقة جديدة من خلال إعطاء اسم ورقة العمل وإرجاع فهرس الأوراق في المصنف (جدول البيانات) بعد إلحاقه. لاحظ أنه عند إنشاء ملف جدول بيانات جديد ، سيتم إنشاء ورقة العمل الافتراضية المسماة `Sheet1`.

## احذف ورقة العمل {#DeleteSheet}

```go
func (f *File) DeleteSheet(name string)
```

يوفر DeleteSheet وظيفة لحذف أوراق العمل في مصنف حسب اسم ورقة العمل المحدد. استخدم هذه الطريقة بحذر ، مما سيؤثر على التغييرات في المراجع مثل الصيغ والمخططات وما إلى ذلك. إذا كان هناك أي قيمة مرجعية لورقة العمل المحذوفة ، فسوف يتسبب ذلك في حدوث خطأ في الملف عند فتحه. ستكون هذه الوظيفة غير صالحة عند ترك ورقة عمل واحدة فقط.

## نسخ ورقة العمل {#CopySheet}

```go
func (f *File) CopySheet(from, to int) error
```

يوفر CopySheet وظيفة لتكرار ورقة العمل من خلال إعطاء فهرس ورقة العمل المصدر والهدف. لاحظ أنه لا يدعم حاليًا المصنفات المكررة التي تحتوي على جداول أو مخططات أو صور. فمثلا:

```go
// Sheet1 موجود بالفعل...
index := f.NewSheet("Sheet2")
err := f.CopySheet(1, index)
return err
```

## أوراق عمل المجموعة {#GroupSheets}

```go
func (f *File) GroupSheets(sheets []string) error
```

توفر GroupSheets وظيفة لتجميع أوراق العمل حسب اسم أوراق العمل المحدد. يجب أن تحتوي أوراق العمل الجماعية على ورقة عمل نشطة.

## فك تجميع أوراق العمل {#UngroupSheets}

```go
func (f *File) UngroupSheets() error
```

توفر UngroupSheets وظيفة لفك تجميع أوراق العمل.

## تعيين خلفية ورقة العمل {#SetSheetBackground}

```go
func (f *File) SetSheetBackground(sheet, picture string) error
```

يوفر SetSheetBackground وظيفة لتعيين صورة الخلفية بواسطة اسم ورقة العمل المحدد.

## تعيين ورقة العمل الافتراضية {#SetActiveSheet}

```go
func (f *File) SetActiveSheet(index int)
```

يوفر SetActiveSheet وظيفة لتعيين الورقة النشطة الافتراضية للمصنف بواسطة فهرس معين. لاحظ أن الفهرس النشط يختلف عن المعرف الذي تم إرجاعه بواسطة الوظيفة `GetSheetMap`. يجب أن يكون أكبر أو يساوي 0 وأقل من إجمالي أرقام ورقة العمل.

## احصل على فهرس الورقة النشط {#GetActiveSheetIndex}

```go
func (f *File) GetActiveSheetIndex() int
```

يوفر GetActiveSheetIndex وظيفة للحصول على ورقة عمل نشطة من المصنف. إذا لم يتم العثور على الورقة النشطة ، فستعرض عددًا صحيحًا `0`.

## تعيين ورقة العمل مرئية {#SetSheetVisible}

```go
func (f *File) SetSheetVisible(name string, visible bool) error
```

يوفر SetSheetVisible وظيفة لتعيين ورقة العمل مرئية من خلال اسم ورقة العمل المحدد. يجب أن يحتوي المصنف على ورقة عمل مرئية واحدة على الأقل. إذا تم تنشيط ورقة العمل المحددة ، فسيتم إبطال هذا الإعداد. قيم حالة الورقة على النحو المحدد بواسطة [SheetStateValues Enum](https://docs.microsoft.com/ar-sa/dotnet/api/documentformat.openxml.spreadsheet.sheetstatevalues?view=openxml-2.8.1):

|قيم حالة ورقة العمل|
|---|
|visible|
|hidden|
|veryHidden|

على سبيل المثال ، إخفاء `Sheet1`:

```go
err := f.SetSheetVisible("Sheet1", false)
```

## احصل على ورقة العمل مرئية {#GetSheetVisible}

```go
func (f *File) GetSheetVisible(name string) bool
```

يوفر GetSheetVisible وظيفة لإظهار ورقة العمل من خلال اسم ورقة العمل المحدد. على سبيل المثال ، احصل على الحالة المرئية لـ `Sheet1`:

```go
f.GetSheetVisible("Sheet1")
```

## تعيين خصائص تنسيق ورقة العمل {#SetSheetFormatPr}

```go
func (f *File) SetSheetFormatPr(sheet string, opts ...SheetFormatPrOptions) error
```

يوفر SetSheetFormatPr وظيفة لتعيين خصائص تنسيق ورقة العمل.

الخيارات المتاحة:

معلمة تنسيق اختيارية |اكتب
---|---
BaseColWidth | uint8
DefaultColWidth | float64
DefaultRowHeight | float64
CustomHeight | bool
ZeroHeight | bool
ThickTop | bool
ThickBottom | bool

على سبيل المثال ، اجعل صفوف ورقة العمل الافتراضية مخفية:

<p align="center"><img width="613" src="./images/sheet_format_pr_01.png" alt="تعيين خصائص تنسيق ورقة العمل"></p>

```go
f := excelize.NewFile()
if err := f.SetSheetViewOptions("Sheet1", -1,
    excelize.RightToLeft(true),
); err != nil {
    fmt.Println(err)
}
const sheet = "Sheet1"
if err := f.SetSheetFormatPr("Sheet1", excelize.ZeroHeight(true)); err != nil {
    fmt.Println(err)
}
if err := f.SetRowVisible("Sheet1", 10, true); err != nil {
    fmt.Println(err)
}
f.SaveAs("المصنف1.xlsx")
```

## احصل على خصائص تنسيق ورقة العمل {#GetSheetFormatPr}

```go
func (f *File) GetSheetFormatPr(sheet string, opts ...SheetFormatPrOptionsPtr) error
```

يوفر GetSheetFormatPr وظيفة للحصول على خصائص تنسيق ورقة العمل.

الخيارات المتاحة:

معلمة تنسيق اختيارية |اكتب
---|---
BaseColWidth | uint8
DefaultColWidth | float64
DefaultRowHeight | float64
CustomHeight | bool
ZeroHeight | bool
ThickTop | bool
ThickBottom | bool

فمثلا:

```go
f := excelize.NewFile()
const sheet = "Sheet1"

var (
    baseColWidth     excelize.BaseColWidth
    defaultColWidth  excelize.DefaultColWidth
    defaultRowHeight excelize.DefaultRowHeight
    customHeight     excelize.CustomHeight
    zeroHeight       excelize.ZeroHeight
    thickTop         excelize.ThickTop
    thickBottom      excelize.ThickBottom
)

if err := f.GetSheetFormatPr(sheet,
    &baseColWidth,
    &defaultColWidth,
    &defaultRowHeight,
    &customHeight,
    &zeroHeight,
    &thickTop,
    &thickBottom,
); err != nil {
    fmt.Println(err)
}
fmt.Println("Defaults:")
fmt.Println("- baseColWidth:", baseColWidth)
fmt.Println("- defaultColWidth:", defaultColWidth)
fmt.Println("- defaultRowHeight:", defaultRowHeight)
fmt.Println("- customHeight:", customHeight)
fmt.Println("- zeroHeight:", zeroHeight)
fmt.Println("- thickTop:", thickTop)
fmt.Println("- thickBottom:", thickBottom)
```

الحصول على الإخراج:

```text
Defaults:
- baseColWidth: 0
- defaultColWidth: 0
- defaultRowHeight: 15
- customHeight: false
- zeroHeight: false
- thickTop: false
- thickBottom: false
```

## تعيين خصائص عرض ورقة العمل {#SetSheetViewOptions}

```go
func (f *File) SetSheetViewOptions(name string, viewIndex int, opts ...SheetViewOption) error
```

يحدد SetSheetViewOptions خيارات عرض الورقة. قد يكون `viewIndex` سالبًا وإذا كان الأمر كذلك يتم حسابه للخلف (`-1` هو العرض الأخير).

الخيارات المتاحة:

معلمة العرض الاختيارية |اكتب
---|---
DefaultGridColor | bool
ShowFormulas | bool
ShowGridLines | bool
ShowRowColHeaders | bool
ShowZeros | bool
RightToLeft | bool
ShowRuler | bool
View | string
TopLeftCell | string
ZoomScale | float64

- مثال 1:

```go
err = f.SetSheetViewOptions("Sheet1", -1, ShowGridLines(false))
```

- مثال 2:

```go
f := excelize.NewFile()
const sheet = "Sheet1"

if err := f.SetSheetViewOptions(sheet, 0,
    excelize.DefaultGridColor(false),
    excelize.ShowFormulas(true),
    excelize.ShowGridLines(true),
    excelize.ShowRowColHeaders(true),
    excelize.RightToLeft(false),
    excelize.ShowRuler(false),
    excelize.View("pageLayout"),
    excelize.TopLeftCell("C3"),
    excelize.ZoomScale(80),
); err != nil {
    fmt.Println(err)
}

var zoomScale ZoomScale
fmt.Println("Default:")
fmt.Println("- zoomScale: 80")

if err := f.SetSheetViewOptions(sheet, 0, excelize.ZoomScale(500)); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &zoomScale); err != nil {
    fmt.Println(err)
}

fmt.Println("Used out of range value:")
fmt.Println("- zoomScale:", zoomScale)

if err := f.SetSheetViewOptions(sheet, 0, excelize.ZoomScale(123)); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &zoomScale); err != nil {
    fmt.Println(err)
}

fmt.Println("Used correct value:")
fmt.Println("- zoomScale:", zoomScale)
```

الحصول على الإخراج:

```text
Default:
- zoomScale: 80
Used out of range value:
- zoomScale: 80
Used correct value:
- zoomScale: 123
```

## احصل على خصائص عرض ورقة العمل {#GetSheetViewOptions}

```go
func (f *File) GetSheetViewOptions(name string, viewIndex int, opts ...SheetViewOptionPtr) error
```

يحصل GetSheetViewOptions على قيمة خيارات عرض الورقة. قد يكون `viewIndex` سالبًا وإذا كان الأمر كذلك يتم حسابه للخلف (`-1` هو العرض الأخير). الخيارات المتاحة:

معلمة العرض الاختيارية |اكتب
---|---
DefaultGridColor | bool
ShowFormulas | bool
ShowGridLines | bool
ShowRowColHeaders | bool
ShowZeros | bool
RightToLeft | bool
ShowRuler | bool
View | string
TopLeftCell | string
ZoomScale | float64

- المثال 1 ، للحصول على إعدادات خاصية خط الشبكة لطريقة العرض الأخيرة في ورقة العمل المسماة `Sheet1`:

```go
var showGridLines excelize.ShowGridLines
err = f.GetSheetViewOptions("Sheet1", -1, &showGridLines)
```

- المثال 2:

```go
f := NewFile()
const sheet = "Sheet1"

var (
    defaultGridColor  excelize.DefaultGridColor
    showFormulas      excelize.ShowFormulas
    showGridLines     excelize.ShowGridLines
    showRowColHeaders excelize.ShowRowColHeaders
    showZeros         excelize.ShowZeros
    rightToLeft       excelize.RightToLeft
    showRuler         excelize.ShowRuler
    view              excelize.View
    topLeftCell       excelize.TopLeftCell
    zoomScale         excelize.ZoomScale
)

if err := f.GetSheetViewOptions(sheet, 0,
    &defaultGridColor,
    &showFormulas,
    &showGridLines,
    &showRowColHeaders,
    &showZeros,
    &rightToLeft,
    &showRuler,
    &view,
    &topLeftCell,
    &zoomScale,
); err != nil {
    fmt.Println(err)
}

fmt.Println("Default:")
fmt.Println("- defaultGridColor:", defaultGridColor)
fmt.Println("- showFormulas:", showFormulas)
fmt.Println("- showGridLines:", showGridLines)
fmt.Println("- showRowColHeaders:", showRowColHeaders)
fmt.Println("- showZeros:", showZeros)
fmt.Println("- rightToLeft:", rightToLeft)
fmt.Println("- showRuler:", showRuler)
fmt.Println("- view:", view)
fmt.Println("- topLeftCell:", `"`+topLeftCell+`"`)
fmt.Println("- zoomScale:", zoomScale)

if err := f.SetSheetViewOptions(sheet, 0, excelize.ShowGridLines(false)); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &showGridLines); err != nil {
    fmt.Println(err)
}

if err := f.SetSheetViewOptions(sheet, 0, excelize.ShowZeros(false)); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &showZeros); err != nil {
    fmt.Println(err)
}

if err := f.SetSheetViewOptions(sheet, 0, excelize.View("pageLayout")); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &view); err != nil {
    fmt.Println(err)
}

if err := f.SetSheetViewOptions(sheet, 0, excelize.TopLeftCell("B2")); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &topLeftCell); err != nil {
    fmt.Println(err)
}

fmt.Println("After change:")
fmt.Println("- showGridLines:", showGridLines)
fmt.Println("- showZeros:", showZeros)
fmt.Println("- view:", view)
fmt.Println("- topLeftCell:", topLeftCell)
```

الحصول على الإخراج:

```text
Default:
- defaultGridColor: true
- showFormulas: false
- showGridLines: true
- showRowColHeaders: true
- showZeros: true
- rightToLeft: false
- showRuler: true
- view: normal
- topLeftCell: ""
- zoomScale: 0
After change:
- showGridLines: false
- showZeros: false
- view: pageLayout
- topLeftCell: B2
```

## تعيين تخطيط صفحة ورقة العمل {#SetPageLayout}

```go
func (f *File) SetPageLayout(sheet string, opts ...PageLayoutOption) error
```

يوفر SetPageLayout وظيفة لتعيين تخطيط صفحة ورقة العمل. الخيارات المتاحة:

- حدد `BlackAndWhite` طباعة أبيض وأسود.

- حدد `FirstPageNumber` رقم أول صفحة مطبوعة. إذا لم يتم تحديد قيمة ، فسيتم افتراض "تلقائي".

- يوفر `PageLayoutOrientation` طريقة لتعيين اتجاه ورقة العمل ، والاتجاه الافتراضي هو "صورة". يوضح ما يلي معلمات الاتجاه التي يدعمها رقم فهرس Excelize:

معامل|اتجاه
---|---
OrientationPortrait|صورة
OrientationLandscape|المناظر الطبيعيه

- يوفر `PageLayoutPaperSize` طريقة لتعيين حجم ورق ورقة العمل ، وحجم الورق الافتراضي لورقة العمل هو "ورق إلكتروني (8.5 بوصة في 11 بوصة)". يوضح ما يلي حجم الورق مرتبة حسب رقم فهرس Excelize:

فهرس|حجم الورق
---|---
1   | Letter paper (8.5 in. × 11 in.)
2   | Letter small paper (8.5 in. × 11 in.)
3   | Tabloid paper (11 in. × 17 in.)
4   | Ledger paper (17 in. × 11 in.)
5   | Legal paper (8.5 in. × 14 in.)
6   | Statement paper (5.5 in. × 8.5 in.)
7   | Executive paper (7.25 in. × 10.5 in.)
8   | A3 paper (297 mm × 420 mm)
9   | A4 paper (210 mm × 297 mm)
10  | A4 small paper (210 mm × 297 mm)
11  | A5 paper (148 mm × 210 mm)
12  | B4 paper (250 mm × 353 mm)
13  | B5 paper (176 mm × 250 mm)
14  | Folio paper (8.5 in. × 13 in.)
15  | Quarto paper (215 mm × 275 mm)
16  | Standard paper (10 in. × 14 in.)
17  | Standard paper (11 in. × 17 in.)
18  | Note paper (8.5 in. × 11 in.)
19  | #9 envelope (3.875 in. × 8.875 in.)
20  | #10 envelope (4.125 in. × 9.5 in.)
21  | #11 envelope (4.5 in. × 10.375 in.)
22  | #12 envelope (4.75 in. × 11 in.)
23  | #14 envelope (5 in. × 11.5 in.)
24  | C paper (17 in. × 22 in.)
25  | D paper (22 in. × 34 in.)
26  | E paper (34 in. × 44 in.)
27  | DL envelope (110 mm × 220 mm)
28  | C5 envelope (162 mm × 229 mm)
29  | C3 envelope (324 mm × 458 mm)
30  | C4 envelope (229 mm × 324 mm)
31  | C6 envelope (114 mm × 162 mm)
32  | C65 envelope (114 mm × 229 mm)
33  | B4 envelope (250 mm × 353 mm)
34  | B5 envelope (176 mm × 250 mm)
35  | B6 envelope (176 mm × 125 mm)
36  | Italy envelope (110 mm × 230 mm)
37  | Monarch envelope (3.875 in. × 7.5 in.).
38  | 6¾ envelope (3.625 in. × 6.5 in.)
39  | US standard fanfold (14.875 in. × 11 in.)
40  | German standard fanfold (8.5 in. × 12 in.)
41  | German legal fanfold (8.5 in. × 13 in.)
42  | ISO B4 (250 mm × 353 mm)
43  | Japanese postcard (100 mm × 148 mm)
44  | Standard paper (9 in. × 11 in.)
45  | Standard paper (10 in. × 11 in.)
46  | Standard paper (15 in. × 11 in.)
47  | Invite envelope (220 mm × 220 mm)
50  | Letter extra paper (9.275 in. × 12 in.)
51  | Legal extra paper (9.275 in. × 15 in.)
52  | Tabloid extra paper (11.69 in. × 18 in.)
53  | A4 extra paper (236 mm × 322 mm)
54  | Letter transverse paper (8.275 in. × 11 in.)
55  | A4 transverse paper (210 mm × 297 mm)
56  | Letter extra transverse paper (9.275 in. × 12 in.)
57  | SuperA/SuperA/A4 paper (227 mm × 356 mm)
58  | SuperB/SuperB/A3 paper (305 mm × 487 mm)
59  | Letter plus paper (8.5 in. × 12.69 in.)
60  | A4 plus paper (210 mm × 330 mm)
61  | A5 transverse paper (148 mm × 210 mm)
62  | JIS B5 transverse paper (182 mm × 257 mm)
63  | A3 extra paper (322 mm × 445 mm)
64  | A5 extra paper (174 mm × 235 mm)
65  | ISO B5 extra paper (201 mm × 276 mm)
66  | A2 paper (420 mm × 594 mm)
67  | A3 transverse paper (297 mm × 420 mm)
68  | A3 extra transverse paper (322 mm × 445 mm)
69  | Japanese Double Postcard (200 mm × 148 mm)
70  | A6 (105 mm × 148 mm)
71  | Japanese Envelope Kaku #2
72  | Japanese Envelope Kaku #3
73  | Japanese Envelope Chou #3
74  | Japanese Envelope Chou #4
75  | Letter Rotated (11 × 8½ in.)
76  | A3 Rotated (420 mm × 297 mm)
77  | A4 Rotated (297 mm × 210 mm)
78  | A5 Rotated (210 mm × 148 mm)
79  | B4 (JIS) Rotated (364 mm × 257 mm)
80  | B5 (JIS) Rotated (257 mm × 182 mm)
81  | Japanese Postcard Rotated (148 mm × 100 mm)
82  | Double Japanese Postcard Rotated (148 mm × 200 mm)
83  | A6 Rotated (148 mm × 105 mm)
84  | Japanese Envelope Kaku #2 Rotated
85  | Japanese Envelope Kaku #3 Rotated
86  | Japanese Envelope Chou #3 Rotated
87  | Japanese Envelope Chou #4 Rotated
88  | B6 (JIS) (128 mm × 182 mm)
89  | B6 (JIS) Rotated (182 mm × 128 mm)
90  | (12 in × 11 in)
91  | Japanese Envelope You #4
92  | Japanese Envelope You #4 Rotated
93  | PRC 16K (146 mm × 215 mm)
94  | PRC 32K (97 mm × 151 mm)
95  | PRC 32K(Big) (97 mm × 151 mm)
96  | PRC Envelope #1 (102 mm × 165 mm)
97  | PRC Envelope #2 (102 mm × 176 mm)
98  | PRC Envelope #3 (125 mm × 176 mm)
99  | PRC Envelope #4 (110 mm × 208 mm)
100 | PRC Envelope #5 (110 mm × 220 mm)
101 | PRC Envelope #6 (120 mm × 230 mm)
102 | PRC Envelope #7 (160 mm × 230 mm)
103 | PRC Envelope #8 (120 mm × 309 mm)
104 | PRC Envelope #9 (229 mm × 324 mm)
105 | PRC Envelope #10 (324 mm × 458 mm)
106 | PRC 16K Rotated
107 | PRC 32K Rotated
108 | PRC 32K(Big) Rotated
109 | PRC Envelope #1 Rotated (165 mm × 102 mm)
110 | PRC Envelope #2 Rotated (176 mm × 102 mm)
111 | PRC Envelope #3 Rotated (176 mm × 125 mm)
112 | PRC Envelope #4 Rotated (208 mm × 110 mm)
113 | PRC Envelope #5 Rotated (220 mm × 110 mm)
114 | PRC Envelope #6 Rotated (230 mm × 120 mm)
115 | PRC Envelope #7 Rotated (230 mm × 160 mm)
116 | PRC Envelope #8 Rotated (309 mm × 120 mm)
117 | PRC Envelope #9 Rotated (324 mm × 229 mm)
118 | PRC Envelope #10 Rotated (458 mm × 324 mm)

- حدد `FitToHeight` عدد الصفحات الرأسية التي سيتم احتواؤها.

- عدد FitToWidth المحدد من الصفحات الأفقية ليتم احتواؤها.

- يحدد `PageLayoutScale` قياس الطباعة. هذه السمة مقيدة بقيم تتراوح من 10 (10٪) إلى 400 (400٪). يتم تجاوز هذا الإعداد عند استخدام `fitToWidth` و / أو `fitToHeight`.

- على سبيل المثال ، عيّن تخطيط الصفحة لـ `Sheet1` بطباعة بالأبيض والأسود ، ورقم الصفحة الأول المطبوع من `2` ، وورق A4 صغير الحجم أفقيًا (210 مم × 297 مم) ، وصفحتان عموديتان للملاءمة ، وصفحتان أفقيتان لملاءمتهما و 50٪ مقياس طباعة

```go
f := excelize.NewFile()
if err := f.SetPageLayout(
    "Sheet1",
    excelize.BlackAndWhite(true),
    excelize.FirstPageNumber(2),
    excelize.PageLayoutOrientation(excelize.OrientationLandscape),
    excelize.PageLayoutPaperSize(10),
    excelize.FitToHeight(2),
    excelize.FitToWidth(2),
    excelize.PageLayoutScale(50),
); err != nil {
    fmt.Println(err)
}
```

## احصل على تخطيط صفحة ورقة العمل {#GetPageLayout}

```go
func (f *File) GetPageLayout(sheet string, opts ...PageLayoutOptionPtr) error
```

يوفر GetPageLayout وظيفة للحصول على تخطيط صفحة ورقة العمل. الخيارات المتاحة:

- يوفر `PageLayoutOrientation` طريقة للحصول على اتجاه ورقة العمل
- يوفر `PageLayoutPaperSize` طريقة للحصول على حجم ورق ورقة العمل

- فمثلا, الحصول على تخطيط صفحة `Sheet1`:

```go
f := excelize.NewFile()
const sheet = "Sheet1"
var (
    orientation excelize.PageLayoutOrientation
    paperSize   excelize.PageLayoutPaperSize
)
if err := f.GetPageLayout("Sheet1", &orientation); err != nil {
    fmt.Println(err)
}
if err := f.GetPageLayout("Sheet1", &paperSize); err != nil {
    fmt.Println(err)
}
fmt.Println("Defaults:")
fmt.Printf("- orientation: %q\n", orientation)
fmt.Printf("- paper size: %d\n", paperSize)
```

انتاج:

```text
Defaults:
- orientation: "portrait"
- paper size: 1
```

## تعيين هوامش صفحة ورقة العمل {#SetPageMargins}

```go
func (f *File) SetPageMargins(sheet string, opts ...PageMarginsOptions) error
```

يوفر SetPageMargins وظيفة لتعيين هوامش صفحة ورقة العمل. الخيارات المتاحة:

خيارات|اكتب
---|---
PageMarginBotom|float64
PageMarginFooter|float64
PageMarginHeader|float64
PageMarginLeft|float64
PageMarginRight|float64
PageMarginTop|float64

- فمثلا, تعيين هوامش الصفحة لـ `Sheet1`:

```go
f := excelize.NewFile()
const sheet = "Sheet1"

if err := f.SetPageMargins(sheet,
    excelize.PageMarginBottom(1.0),
    excelize.PageMarginFooter(1.0),
    excelize.PageMarginHeader(1.0),
    excelize.PageMarginLeft(1.0),
    excelize.PageMarginRight(1.0),
    excelize.PageMarginTop(1.0),
); err != nil {
    fmt.Println(err)
}
```

## احصل على هوامش صفحة ورقة العمل {#GetPageMargins}

```go
func (f *File) GetPageMargins(sheet string, opts ...PageMarginsOptionsPtr) error
```

يوفر GetPageMargins وظيفة للحصول على هوامش صفحة ورقة العمل. الخيارات المتاحة:

خيارات|اكتب
---|---
PageMarginBotom|float64
PageMarginFooter|float64
PageMarginHeader|float64
PageMarginLeft|float64
PageMarginRight|float64
PageMarginTop|float64

- فمثلا, الحصول على هوامش صفحة `Sheet1`:

```go
f := excelize.NewFile()
const sheet = "Sheet1"

var (
    marginBottom excelize.PageMarginBottom
    marginFooter excelize.PageMarginFooter
    marginHeader excelize.PageMarginHeader
    marginLeft   excelize.PageMarginLeft
    marginRight  excelize.PageMarginRight
    marginTop    excelize.PageMarginTop
)

if err := f.GetPageMargins(sheet,
    &marginBottom,
    &marginFooter,
    &marginHeader,
    &marginLeft,
    &marginRight,
    &marginTop,
); err != nil {
    fmt.Println(err)
}
fmt.Println("Defaults:")
fmt.Println("- marginBottom:", marginBottom)
fmt.Println("- marginFooter:", marginFooter)
fmt.Println("- marginHeader:", marginHeader)
fmt.Println("- marginLeft:", marginLeft)
fmt.Println("- marginRight:", marginRight)
fmt.Println("- marginTop:", marginTop)
```

انتاج:

```text
Defaults:
- marginBottom: 0.75
- marginFooter: 0.3
- marginHeader: 0.3
- marginLeft: 0.7
- marginRight: 0.7
- marginTop: 0.75
```

## تعيين خصائص المصنف {#SetWorkbookPrOptions}

```go
func (f *File) SetWorkbookPrOptions(opts ...WorkbookPrOption) error
```

يوفر SetWorkbookPrOptions دالة لتعيين خصائص المصنف. الخيارات المتاحة:

خيارات|اكتب
---|---
Date1904|bool
FilterPrivacy|bool
CodeName|string

- فمثلا, تعيين خصائص المصنف:

```go
f := excelize.NewFile()
if err := f.SetWorkbookPrOptions(
    excelize.Date1904(false),
    excelize.FilterPrivacy(false),
    excelize.CodeName("code"),
); err != nil {
    fmt.Println(err)
}
```

## احصل على خصائص المصنف {#GetWorkbookPrOptions}

```go
func (f *File) GetWorkbookPrOptions(opts ...WorkbookPrOptionPtr) error
```

يوفر GetWorkbookPrOptions دالة للحصول على خصائص المصنف. الخيارات المتاحة:

خيارات|اكتب
---|---
Date1904|bool
FilterPrivacy|bool
CodeName|string

- فمثلا, احصل على خصائص المصنف:

```go
f := excelize.NewFile()
var (
    date1904      excelize.Date1904
    filterPrivacy excelize.FilterPrivacy
    codeName      excelize.CodeName
)
if err := f.GetWorkbookPrOptions(&date1904); err != nil {
    fmt.Println(err)
}
if err := f.GetWorkbookPrOptions(&filterPrivacy); err != nil {
    fmt.Println(err)
}
if err := f.GetWorkbookPrOptions(&codeName); err != nil {
    fmt.Println(err)
}
fmt.Println("Defaults:")
fmt.Printf("- date1904: %t\n", date1904)
fmt.Printf("- filterPrivacy: %t\n", filterPrivacy)
fmt.Printf("- codeName: %q\n", codeName)
```

انتاج:

```text
Defaults:
- filterPrivacy: true
- codeName: ""
```

## تعيين الرأس والتذييل {#SetHeaderFooter}

```go
func (f *File) SetHeaderFooter(sheet string, settings *FormatHeaderFooter) error
```

يوفر SetHeaderFooter وظيفة لتعيين الرؤوس والتذييلات من خلال اسم ورقة العمل المحددة وأحرف التحكم.

يتم تحديد الرؤوس والتذييلات باستخدام حقول الإعدادات التالية:

مجالات           | وصف
---|---
AlignWithMargins | محاذاة هوامش تذييل الرأس مع هوامش الصفحة
DifferentFirst   | مؤشر مختلف لرأس وتذييل الصفحة الأولىمؤشر مختلف لرأس وتذييل الصفحة الأولى
DifferentOddEven | مؤشرات مختلفة للرؤوس والتذييلات الفردية والزوجية
ScaleWithDoc     | مقياس الرأس والتذييل باستخدام مقياس المستند
OddFooter        | تذييل الصفحة الفردية
OddHeader        | رأس فردي
EvenFooter       | حتى تذييل الصفحة
EvenHeader       | حتى رأس الصفحة
FirstFooter      | تذييل الصفحة الأولى
FirstHeader      | رأس الصفحة الأولى

يمكن استخدام رموز التنسيق التالية في 6 حقول من نوع السلسلة: `OddHeader`, `OddFooter`, `EvenHeader`, `EvenFooter`, `FirstFooter`, `FirstHeader`

<table>
    <thead>
        <tr>
            <th>كود التنسيق</th>
            <th>وصف</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>&amp;&amp;</code></td>
            <td>الشخصية &quot;&amp;&quot;</td>
        </tr>
        <tr>
            <td><code>&amp;font-size</code></td>
            <td>حجم خط النص ، حيث يكون حجم الخط هو حجم الخط العشري بالنقاط</td>
        </tr>
        <tr>
            <td><code>&amp;&quot;font name,font type&quot;</code></td>
            <td>سلسلة اسم الخط النصي ، واسم الخط ، وسلسلة نوع الخط النصي ، ونوع الخط</td>
        </tr>
        <tr>
            <td><code>&amp;&quot;-,Regular&quot;</code></td>
            <td>تنسيق النص العادي. تبديل الوضعين الغامق والمائل إلى إيقاف التشغيل</td>
        </tr>
        <tr>
            <td><code>&amp;A</code></td>
            <td>اسم علامة تبويب ورقة العمل الحالية</td>
        </tr>
        <tr>
            <td><code>&amp;B</code> or <code>&amp;&quot;-,Bold&quot;</code></td>
            <td>تنسيق نص عريض ، من إيقاف تشغيل إلى تشغيل ، أو العكس. الوضع الافتراضي معطل</td>
        </tr>
        <tr>
            <td><code>&amp;D</code></td>
            <td>التاريخ الحالي</td>
        </tr>
        <tr>
            <td><code>&amp;C</code></td>
            <td>قسم المركز</td>
        </tr>
        <tr>
            <td><code>&amp;E</code></td>
            <td>تنسيق نص مزدوج التسطير</td>
        </tr>
        <tr>
            <td><code>&amp;F</code></td>
            <td>اسم ملف المصنف الحالي</td>
        </tr>
        <tr>
            <td><code>&amp;G</code></td>
            <td>كائن رسومي كخلفية (لا يدعم حاليا)</td>
        </tr>
        <tr>
            <td><code>&amp;H</code></td>
            <td>تنسيق نص الظل</td>
        </tr>
        <tr>
            <td><code>&amp;I</code> or <code>&amp;&quot;-,Italic&quot;</code></td>
            <td>تنسيق نص مائل</td>
        </tr>
        <tr>
            <td><code>&amp;K</code></td>
            <td>لون خط النص<br>تم تحديد لون RGB على أنه RRGGBB<br>يتم تحديد لون النسق على أنه TTSNNN حيث يكون TT هو معرف لون النسق ، S إما &quot;+&quot; أو &quot;-&quot; قيمة الصبغة / الظل ، و NNN هي قيمة الصبغة / الظل</td>
        </tr>
        <tr>
            <td><code>&amp;L</code></td>
            <td>القسم الأيسر</td>
        </tr>
        <tr>
            <td><code>&amp;N</code></td>
            <td>العدد الإجمالي للصفحات</td>
        </tr>
        <tr>
            <td><code>&amp;O</code></td>
            <td>تنسيق نص المخطط التفصيلي</td>
        </tr>
        <tr>
            <td><code>&amp;P[[+\|-]n]</code></td>
            <td>بدون اللاحقة الاختيارية ، يكون رقم الصفحة الحالي في النظام العشري</td>
        </tr>
        <tr>
            <td><code>&amp;R</code></td>
            <td>القسم الأيمن</td>
        </tr>
        <tr>
            <td><code>&amp;S</code></td>
            <td>تنسيق نص يتوسطه خط</td>
        </tr>
        <tr>
            <td><code>&amp;T</code></td>
            <td>الوقت الحالي</td>
        </tr>
        <tr>
            <td><code>&amp;U</code></td>
            <td>تنسيق نص تسطير واحد. إذا كان وضع التسطير المزدوج قيد التشغيل ، فإن التواجد التالي في محدد القسم يقوم بتبديل وضع التسطير المزدوج إلى وضع الإيقاف ؛ وإلا ، فإنه يقوم بتبديل وضع التسطير الفردي ، من إيقاف تشغيل إلى تشغيل ، أو العكس. الوضع الافتراضي معطل</td>
        </tr>
        <tr>
            <td><code>&amp;X</code></td>
            <td>تنسيق نص مرتفع</td>
        </tr>
        <tr>
            <td><code>&amp;Y</code></td>
            <td>تنسيق نص منخفض</td>
        </tr>
        <tr>
            <td><code>&amp;Z</code></td>
            <td>مسار ملف المصنف الحالي</td>
        </tr>
    </tbody>
</table>

فمثلا:

```go
err := f.SetHeaderFooter("Sheet1", &excelize.FormatHeaderFooter{
    DifferentFirst:   true,
    DifferentOddEven: true,
    OddHeader:        "&R&P",
    OddFooter:        "&C&F",
    EvenHeader:       "&L&P",
    EvenFooter:       "&L&D&R&T",
    FirstHeader:      `&CCenter &"-,Bold"Bold&"-,Regular"HeaderU+000A&D`,
})
```

يوضح هذا المثال:

- تحتوي الصفحة الأولى على رأس وتذييل خاصين بها
- الصفحات الفردية والزوجية لها رؤوس وتذييلات مختلفة
- رقم الصفحة الحالي في القسم الأيمن من رؤوس الصفحات الفردية
- اسم ملف المصنف الحالي في القسم الأوسط من تذييلات الصفحات الفردية
- رقم الصفحة الحالي في القسم الأيسر من رؤوس الصفحات الزوجية
- التاريخ الحالي في القسم الأيسر والوقت الحالي في القسم الأيمن من تذييلات الصفحات الزوجية
- النص "Center Bold Header" في السطر الأول من القسم الأوسط من الصفحة الأولى ، والتاريخ في السطر الثاني من القسم الأوسط من نفس الصفحة
- لا يوجد تذييل في الصفحة الأولى

## تعيين الاسم المحدد {#SetDefinedName}

```go
func (f *File) SetDefinedName(definedName *DefinedName) error
```

يوفر SetDefinedName دالة لتعيين الأسماء المحددة للمصنف أو ورقة العمل. إذا لم يتم تحديد النطاق ، فإن النطاق الافتراضي هو المصنف.

فمثلا:

```go
f.SetDefinedName(&excelize.DefinedName{
    Name:     "Amount",
    RefersTo: "Sheet1!$A$2:$D$5",
    Comment:  "defined name comment",
    Scope:    "Sheet2",
})
```

إعدادات منطقة الطباعة وعناوين الطباعة لورقة العمل:

<p align="center"><img width="628" src="./images/page_setup_01.png" alt="منطقة الطباعة وإعدادات عناوين الطباعة لورقة العمل"></p>

```go
f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Area",
    RefersTo: "Sheet1!$A$1:$Z$100",
    Scope:    "Sheet1",
})
f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Titles",
    RefersTo: "Sheet1!$A:$A,Sheet1!$1:$1",
    Scope:    "Sheet1",
})
```

## احصل على اسم محدد {#GetDefinedName}

```go
func (f *File) GetDefinedName() []DefinedName
```

يوفر GetDefinedName دالة للحصول على الأسماء المحددة للمصنف أو ورقة العمل.

## حذف الاسم المحدد {#DeleteDefinedName}

```go
func (f *File) DeleteDefinedName(definedName *DefinedName) error
```

يوفر DeleteDefinedName وظيفة لحذف الأسماء المعرفة للمصنف أو ورقة العمل. إذا لم يتم تحديد النطاق ، فإن النطاق الافتراضي هو المصنف. فمثلا:

```go
f.DeleteDefinedName(&excelize.DefinedName{
    Name:     "Amount",
    Scope:    "Sheet2",
})
```

## تعيين خصائص التطبيق {#SetAppProps}

```go
func (f *File) SetAppProps(appProperties *AppProperties) error
```

يوفر SetAppProps وظيفة لتعيين خصائص تطبيق المستند. الخصائص التي يمكن تعيينها هي:

خاصية       | وصف
---|---
Application       | اسم التطبيق الذي أنشأ هذا المستند.
ScaleCrop         | يشير إلى وضع عرض الصورة المصغرة للوثيقة. اضبط هذا العنصر على `true` لتمكين تغيير حجم الصورة المصغرة للمستند إلى العرض. اضبط هذا العنصر على `false` لتمكين اقتصاص الصورة المصغرة للمستند لإظهار الأقسام التي تناسب العرض فقط.
DocSecurity       | مستوى الأمان للمستند كقيمة عددية. يتم تعريف أمان المستند على أنه:<br>1 - المستند محمي بكلمة مرور<br>2 - يُوصى بفتح المستند للقراءة فقط<br>3 - يتم فرض المستند لفتحه للقراءة فقط<br >4 - تم قفل المستند للتعليق التوضيحي
Company           | اسم الشركة المرتبطة بالمستند.
LinksUpToDate     | يشير إلى ما إذا كانت الارتباطات التشعبية في مستند محدثة أم لا. عيّن هذا العنصر على `true` للإشارة إلى تحديث الارتباطات التشعبية. عيّن هذا العنصر على `false` للإشارة إلى أن الارتباطات التشعبية قديمة.
HyperlinksChanged | تعيين ارتباط تشعبي واحد أو أكثر في هذا الجزء تم تحديثه حصريًا في هذا الجزء بواسطة المنتج. يجب على المنتج التالي الذي سيفتح هذا المستند تحديث علاقات الارتباط التشعبي بالارتباطات التشعبية الجديدة المحددة في هذا الجزء.
AppVersion        | يحدد إصدار التطبيق الذي أنتج هذا المستند. يجب أن يكون محتوى هذا العنصر بالصيغة XX.YYYY حيث تمثل X و Y قيمًا عددية ، أو تعتبر الوثيقة غير متوافقة.

فمثلا:

```go
err := f.SetAppProps(&excelize.AppProperties{
    Application:       "Microsoft Excel",
    ScaleCrop:         true,
    DocSecurity:       3,
    Company:           "Company Name",
    LinksUpToDate:     true,
    HyperlinksChanged: true,
    AppVersion:        "16.0000",
})
```

## احصل على خصائص التطبيق {#GetAppProps}

```go
func (f *File) GetAppProps() (*AppProperties, error)
```

يوفر GetAppProps وظيفة للحصول على خصائص تطبيق المستند.

## تعيين خصائص الوثيقة {#SetDocProps}

```go
func (f *File) SetDocProps(docProperties *DocProperties) error
```

يوفر SetDocProps وظيفة لتعيين خصائص الوثيقة الأساسية. الخصائص التي يمكن تعيينها هي:

خاصية       | وصف
---|---
Category       | تصنيف محتوى هذه الحزمة.
ContentStatus  | حالة المحتوى. فمثلا: قد تتضمن القيم "Draft" و "Reviewed" و "Final"
Created        | وقت إنشاء محتوى المورد.
Creator        | الكيان مسؤول بشكل أساسي عن صنع محتوى المورد
Description    | شرح لمحتوى المصدر.
Identifier     | إشارة لا لبس فيها إلى المورد ضمن سياق معين.
Keywords       | مجموعة محددة من الكلمات الأساسية لدعم البحث والفهرسة. عادةً ما تكون هذه قائمة بالمصطلحات غير المتوفرة في أي مكان آخر في الخصائص.
Language       | لغة المحتوى الفكري للمصدر.
LastModifiedBy | المستخدم الذي أجرى التعديل الأخير. التعريف خاص بالبيئة.
Modified       | الوقت المعدل لمحتوى المورد.
Revision       | رقم مراجعة محتوى المصدر.
Subject        | موضوع محتوى المصدر.
Title          | تم إعطاء الاسم للمورد.
Version        | رقم الإصدار. يتم تعيين هذه القيمة من قبل المستخدم أو بواسطة التطبيق.

فمثلا:

```go
err := f.SetDocProps(&excelize.DocProperties{
    Category:       "category",
    ContentStatus:  "Draft",
    Created:        "2019-06-04T22:00:10Z",
    Creator:        "Go Excelize",
    Description:    "This file created by Go Excelize",
    Identifier:     "xlsx",
    Keywords:       "Spreadsheet",
    LastModifiedBy: "Go Author",
    Modified:       "2019-06-04T22:00:10Z",
    Revision:       "0",
    Subject:        "Test Subject",
    Title:          "Test Title",
    Language:       "en-US",
    Version:        "1.0.0",
})
```

## احصل على خصائص المستند {#GetDocProps}

```go
func (f *File) GetDocProps() (*DocProperties, error)
```

يوفر GetDocProps وظيفة للحصول على خصائص المستند الأساسية.
