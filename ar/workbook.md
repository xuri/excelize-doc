# دفتر العمل

تحدد `Options` خيارات قراءة وكتابة جداول البيانات.

```go
type Options struct {
    MaxCalcIterations uint
    Password          string
    RawCellValue      bool
    UnzipSizeLimit    int64
    UnzipXMLSizeLimit int64
    ShortDatePattern  string
    LongDatePattern   string
    LongTimePattern   string
    CultureInfo       CultureName
}
```

يحدد `MaxCalcIterations` الحد الأقصى من التكرارات للحساب التكراري ، والقيمة الافتراضية هي 0.

تحدد `Password` كلمة مرور جدول البيانات بنص عادي.

يحدد `RawCellValue` ما إذا كان يتم تطبيق تنسيق الأرقام لقيمة الخلية أو الحصول على القيمة الأولية.

يحدّد `UnzipSizeLimit` حد حجم فك الضغط بالبايت عند فتح جدول البيانات ، ويجب أن تكون هذه القيمة أكبر من أو تساوي `UnzipXMLSizeLimit` ، الحد الافتراضي للحجم هو 16 غيغابايت.

يحدد `UnzipXMLSizeLimit` حد الذاكرة لفك ضغط ورقة العمل بالبايت ، وسيتم استخراج XML لورقة العمل إلى دليل النظام المؤقت عندما يكون حجم الملف أكبر من هذه القيمة ، يجب أن تكون هذه القيمة أقل من أو تساوي `UnzipSizeLimit` ، القيمة الافتراضية هي 16 ميغا بايت.

يحدد `ShortDatePattern` رمز تنسيق رقم التاريخ القصير. في تطبيقات جداول البيانات ، تعرض تنسيقات التاريخ الأرقام التسلسلية للتاريخ والوقت كقيم للتاريخ. تستجيب تنسيقات التاريخ التي تبدأ بعلامة النجمة (\*) للتغييرات في إعدادات التاريخ والوقت الإقليمية المحددة لنظام التشغيل. لا تتأثر التنسيقات التي لا تحتوي على علامة النجمة بإعدادات نظام التشغيل. يحدد `ShortDatePattern` المستخدم لتنسيقات التاريخ التي تبدأ بعلامة النجمة.

يحدد `LongDatePattern` رمز تنسيق رقم التاريخ الطويل.

يحدد `LongTimePattern` رمز تنسيق الرقم لفترة طويلة.

يحدد `CultureInfo` رمز البلد لتطبيق كود تنسيق رقم اللغة المدمج الذي يؤثر على إعدادات اللغة المحلية للنظام.

`HeaderFooterImagePositionType` هو نوع موضع صورة الرأس والتذييل.

```go
type HeaderFooterImagePositionType byte
```

يقوم هذا القسم بتعريف أنواع مواضع صور الرأس والتذييل في ورقة العمل.

```go
const (
    HeaderFooterImagePositionLeft HeaderFooterImagePositionType = iota
    HeaderFooterImagePositionCenter
    HeaderFooterImagePositionRight
)
```

تعرف CalcPropsOptions مجموعة الخصائص التي تستخدمها التطبيق لتسجيل حالة الحساب والتفاصيل.

```go
type CalcPropsOptions struct {
    CalcID                *uint
    CalcMode              *string
    FullCalcOnLoad        *bool
    RefMode               *string
    Iterate               *bool
    IterateCount          *uint
    IterateDelta          *float64
    FullPrecision         *bool
    CalcCompleted         *bool
    CalcOnSave            *bool
    ConcurrentCalc        *bool
    ConcurrentManualCount *uint
    ForceFullCalc         *bool
}
```

## قم بإنشاء جدول بيانات {#NewFile}

```go
func NewFile(opts ...Options) *File
```

يوفر `NewFile` وظيفة لإنشاء ملف جديد بواسطة القالب الافتراضي. سيحتوي المصنف الذي تم إنشاؤه حديثًا بشكل افتراضي على ورقة عمل باسم `Sheet1`. فمثلا:

## افتح {#OpenFile}

```go
func OpenFile(filename string, opts ...Options) (*File, error)
```

يأخذ OpenFile اسم ملف جدول البيانات ويعيد بنية ملف جدول بيانات معبأة له. على سبيل المثال ، افتح جدول بيانات محميًا بكلمة مرور:

```go
f, err := excelize.OpenFile("المصنف1.xlsx", excelize.Options{Password: "password"})
if err != nil {
    return
}
```

أغلق الملف عن طريق [`Close()`](workbook.md#Close) بعد فتح جدول البيانات.

## فتح دفق البيانات {#OpenReader}

```go
func OpenReader(r io.Reader, opts ...Options) (*File, error)
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
        fmt.Fprint(w, err.Error())
        return
    }
    defer file.Close()
    f, err := excelize.OpenReader(file)
    if err != nil {
        fmt.Fprint(w, err.Error())
        return
    }
    f.Path = "Book1.xlsx"
    f.NewSheet("NewSheet")
    w.Header().Set("Content-Disposition", fmt.Sprintf("attachment; filename=%s", f.Path))
    w.Header().Set("Content-Type", req.Header.Get("Content-Type"))
    if err := f.Write(w); err != nil {
        fmt.Fprint(w, err.Error())
    }
}

func main() {
    http.HandleFunc("/process", process)
    http.ListenAndServe(":8090", nil)
}
```

اختبار مع cURL:

```bash
curl --location --request GET 'http://127.0.0.1:8090/process' \
--form 'file=@/tmp/template.xltx' -O -J
```

## حفظ {#Save}

```go
func (f *File) Save(opts ...Options) error
```

يوفر Save وظيفة لتجاوز جدول البيانات بمسار الأصل.

## حفظ باسم {#SaveAs}

```go
func (f *File) SaveAs(name string, opts ...Options) error
```

يوفر SaveAs وظيفة لإنشاء أو تحديث جدول بيانات في المسار المتوفر.

## إغلاق المصنف {#Close}

```go
func (f *File) Close() error
```

يقوم Close بإغلاق وتنظيف الملف المؤقت المفتوح لجدول البيانات.

## قم بإنشاء ورقة عمل {#NewSheet}

```go
func (f *File) NewSheet(sheet string) (int, error)
```

يوفر NewSheet وظيفة لإنشاء ورقة جديدة من خلال إعطاء اسم ورقة العمل وإرجاع فهرس الأوراق في المصنف (جدول البيانات) بعد إلحاقه. لاحظ أنه عند إنشاء ملف جدول بيانات جديد ، سيتم إنشاء ورقة العمل الافتراضية المسماة `Sheet1`.

## احذف ورقة العمل {#DeleteSheet}

```go
func (f *File) DeleteSheet(sheet string) error
```

يوفر DeleteSheet وظيفة لحذف ورقة العمل في مصنف حسب اسم ورقة العمل المحدد ، وأسماء الأوراق ليست حساسة لحالة الأحرف. استخدم هذه الطريقة بحذر ، مما سيؤثر على التغييرات في المراجع مثل الصيغ والمخططات وما إلى ذلك. إذا كان هناك أي قيمة مرجعية لورقة العمل المحذوفة ، فسوف يتسبب ذلك في حدوث خطأ في الملف عند فتحه. ستكون هذه الوظيفة غير صالحة عند ترك ورقة عمل واحدة فقط.

## نقل ورقة العمل {#MoveSheet}

```go
func (f *File) MoveSheet(source, target string) error
```

MoveSheet تنقل ورقة إلى موضع محدد في المصنف. تنقل الوظيفة ورقة المصدر قبل ورقة الهدف. بعد النقل، سيتم نقل الأوراق الأخرى إلى اليسار أو اليمين. إذا كانت الورقة بالفعل في الموضع المستهدف، فلن تقوم الوظيفة بأي إجراء. لا يعني هذا أن هذه الوظيفة ستقوم بإلغاء تجميع كل الأوراق بعد النقل. نقل `ورقة2` قبل `ورقة1`:

```go
err := f.MoveSheet("ورقة2", "ورقة1")
```

## نسخ ورقة العمل {#CopySheet}

```go
func (f *File) CopySheet(from, to int) error
```

يوفر CopySheet وظيفة لتكرار ورقة العمل من خلال إعطاء فهرس ورقة العمل المصدر والهدف. لاحظ أنه لا يدعم حاليًا المصنفات المكررة التي تحتوي على جداول أو مخططات أو صور. فمثلا:

```go
// Sheet1 موجود بالفعل...
index, err := f.NewSheet("Sheet2")
if err != nil {
    fmt.Println(err)
    return
}
err := f.CopySheet(1, index)
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

يوفر SetSheetBackground وظيفة لتعيين صورة الخلفية عن طريق اسم ورقة العمل ومسار الملف. أنواع الصور المدعومة: BMP و EMF و EMZ و GIF و JPEG و JPG و PNG و SVG و TIF و TIFF و WMF و WMZ.

```go
func (f *File) SetSheetBackgroundFromBytes(sheet, extension string, picture []byte) error
```

يوفر SetSheetBackgroundFromBytes وظيفة لتعيين صورة الخلفية عن طريق اسم ورقة العمل المعطى واسم الامتداد وبيانات الصورة. أنواع الصور المدعومة: BMP و EMF و EMZ و GIF و JPEG و JPG و PNG و SVG و TIF و TIFF و WMF و WMZ.

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
func (f *File) SetSheetVisible(sheet string, visible bool, veryHidden ...bool) error
```

يوفر SetSheetVisible وظيفة لتعيين ورقة العمل مرئية من خلال اسم ورقة العمل المحدد. يجب أن يحتوي المصنف على ورقة عمل مرئية واحدة على الأقل. إذا تم تنشيط ورقة العمل المحددة ، فسيتم إبطال هذا الإعداد. لا تعمل المعلمة الاختيارية الثالثة `veryHidden` إلا عندما تكون `visible` هي `false`.

على سبيل المثال ، إخفاء `Sheet1`:

```go
err := f.SetSheetVisible("Sheet1", false)
```

## احصل على ورقة العمل مرئية {#GetSheetVisible}

```go
func (f *File) GetSheetVisible(sheet string) (bool, error)
```

يوفر GetSheetVisible وظيفة لإظهار ورقة العمل من خلال اسم ورقة العمل المحدد. على سبيل المثال ، احصل على الحالة المرئية لـ `Sheet1`:

```go
visible, err := f.GetSheetVisible("Sheet1")
```

## تعيين خصائص الورقة {#SetSheetProps}

```go
func (f *File) SetSheetProps(sheet string, opts *SheetPropsOptions) error
```

يوفر SetSheetProps وظيفة لتعيين خصائص ورقة العمل. الخصائص التي يمكن تعيينها هي:

خيارات|اكتب|وصف
---|---|---
CodeName                          | `*string`  | يحدد اسما ثابتا للورقة، والذي يجب ألا يتغير بمرور الوقت، ولا يتغير من إدخال المستخدم. يجب استخدام هذا الاسم بواسطة التعليمات البرمجية للإشارة إلى ورقة معينة
EnableFormatConditionsCalculation | `*bool`    | بيان ما إذا كان سيتم تقييم حسابات التنسيق الشرطي. إذا تم تعيينها إلى false، فلن يتم تحديث قيم الصغر/الحد الأقصى لمقاييس الألوان أو أشرطة البيانات أو قيم العتبة في قواعد Top N. أساسا التنسيق الشرطي "calc" هو قبالة
Published                         | `*bool`    | بالإشارة إلى ما إذا كان قد تم نشر ورقة العمل أم لا، تكون القيمة الافتراضية هي `true`
AutoPageBreaks                    | `*bool`    | بالإشارة إلى ما إذا كانت الورقة تعرض فواصل الصفحات التلقائية، تكون القيمة الافتراضية هي `true`
FitToPage                         | `*bool`    | بالإشارة إلى ما إذا كان خيار طباعة احتواء الصفحة ممكنا أم لا، تكون القيمة الافتراضية هي `false`
TabColorIndexed                   | `*int`     | يمثل قيمة اللون المفهرسة
TabColorRGB                       | `*string`  | يمثل قيمة اللون ARGB (ألفا أحمر أخضر أزرق) القياسية
TabColorTheme                     | `*int`     | يمثل الفهرس المستند إلى الصفر في المجموعة، مع الإشارة إلى قيمة معينة يتم التعبير عنها في جزء النسق
TabColorTint                      | `*float64` | يحدد قيمة الصبغة المطبقة على اللون، والقيمة الافتراضية هي `0.0`
OutlineSummaryBelow               | `*bool`    | للإشارة إلى ما إذا كانت صفوف الملخص تظهر أسفل التفاصيل في مخطط تفصيلي، عند تطبيق مخطط تفصيلي، تكون القيمة الافتراضية هي `true`
OutlineSummaryRight               | `*bool`    | للإشارة إلى ما إذا كانت أعمدة الملخص تظهر على يسار التفاصيل في مخطط تفصيلي، عند تطبيق مخطط تفصيلي، تكون القيمة الافتراضية هي `true`
BaseColWidth                      | `*uint8`   | يحدد عدد أحرف الحد الأقصى لعرض الأرقام لخط النمط العادي. لا تتضمن هذه القيمة حشو الهامش أو الحشو الإضافي لخطوط الشبكة. إنه فقط عدد الأحرف ، القيمة الافتراضية هي `8`
DefaultColWidth                   | `*float64` | يحدد عرض العمود الافتراضي الذي تم قياسه كعدد أحرف الحد الأقصى لعرض الأرقام لخط النمط العادي
DefaultRowHeight                  | `*float64` | يحدد ارتفاع الصف الافتراضي الذي تم قياسه بحجم النقطة. التحسين حتى لا نضطر إلى كتابة الارتفاع على جميع الصفوف. يمكن كتابة ذلك إذا كان لمعظم الصفوف ارتفاع مخصص ، لتحقيق التحسين
CustomHeight                      | `*bool`    | يحدد الارتفاع المخصص ، القيمة الافتراضية هي `false`
ZeroHeight                        | `*bool`    | يحدد ما إذا كانت الصفوف مخفية، تكون القيمة الافتراضية هي `false`
ThickTop                          | `*bool`    | يحدد ما إذا كانت الصفوف تحتوي على حد علوي سميك بشكل افتراضي، فإن القيمة الافتراضية هي `false`
ThickBottom                       | `*bool`    | يحدد ما إذا كانت الصفوف تحتوي على حد سفلي سميك بشكل افتراضي، فإن القيمة الافتراضية هي `false`

على سبيل المثال ، اجعل صفوف ورقة العمل الافتراضية مخفية:

<p align="center"><img width="613" src="./images/sheet_format_pr_01.png" alt="تعيين خصائص الورقة"></p>

```go
f, enable := excelize.NewFile(), true
if err := f.SetSheetView("Sheet1", -1, &excelize.ViewOptions{
    RightToLeft: &enable,
}); err != nil {
    fmt.Println(err)
}
if err := f.SetSheetProps("Sheet1", &excelize.SheetPropsOptions{
    ZeroHeight: &enable,
}); err != nil {
    fmt.Println(err)
}
if err := f.SetRowVisible("Sheet1", 10, true); err != nil {
    fmt.Println(err)
}
f.SaveAs("المصنف1.xlsx")
```

## الحصول على خصائص ورقة {#GetSheetProps}

```go
func (f *File) GetSheetProps(sheet string) (SheetPropsOptions, error)
```

يوفر GetSheetProps دالة للحصول على خصائص ورقة العمل. الخصائص التي يمكن تعيينها هي:

خيارات|اكتب|وصف
---|---|---
DefaultGridColor  | `*bool`    | الإشارة إلى أن التطبيق المستهلك يجب أن يستخدم لون خطوط الشبكة الافتراضي (يعتمد على النظام). يتجاوز أي لون محدد في colorId ، القيمة الافتراضية هي `true`
RightToLeft       | `*bool`    | الإشارة إلى ما إذا كانت الورقة في وضع العرض "من اليمين إلى اليسار". عندما يكون العمود A في هذا الوضع ، يكون في أقصى اليمين ، العمود B ؛ هو عمود واحد يسار العمود A، وهكذا. أيضا ، يتم عرض المعلومات في الخلايا بتنسيق من اليمين إلى اليسار ، والقيمة الافتراضية هي `false`
ShowFormulas      | `*bool`    | للإشارة إلى ما إذا كان يجب أن تعرض هذه الورقة صيغا ، فإن القيمة الافتراضية هي `false`
ShowGridLines     | `*bool`    | بالإشارة إلى ما إذا كان يجب أن تعرض هذه الورقة خطوط الشبكة ، فإن القيمة الافتراضية هي `true`
ShowRowColHeaders | `*bool`    | بالإشارة إلى ما إذا كان يجب أن تعرض الورقة عناوين الصفوف والأعمدة، تكون القيمة الافتراضية هي `true`
ShowRuler         | `*bool`    | بالإشارة إلى أن هذه الورقة يجب أن تعرض المسطرة ، فإن القيمة الافتراضية هي `true`
ShowZeros         | `*bool`    | الإشارة إلى ما إذا كان يجب "إظهار صفر في الخلايا التي لها قيمة صفرية". عند استخدام صيغة للإشارة إلى خلية أخرى فارغة، تصبح القيمة المشار إليها `0` عندما تكون العلامة `true`، وتكون القيمة الافتراضية هي `true`
TopLeftCell       | `*string`  | يحدد موقعا للخلية المرئية العلوية اليسرى موقع الخلية المرئية العلوية اليسرى في الجزء السفلي الأيسر (عندما تكون في الوضع من اليسار إلى اليمين)
View              | `*string`  | للإشارة إلى كيفية عرض الورقة ، فإنها تستخدم افتراضيا سلسلة فارغة وخيارات متاحة: `normal` و `pageBreakPreview` و `pageLayout`
ZoomScale         | `*float64` | يحدد تكبير تكبير النافذة للعرض الحالي الذي يمثل قيم النسبة المئوية. تقتصر هذه السمة على قيم تتراوح من `10` إلى `400`. مقياس أفقي ورأسي معا ، القيمة الافتراضية هي `100`

## تعيين خصائص عرض ورقة العمل {#SetSheetView}

```go
func (f *File) SetSheetView(sheet string, viewIndex int, opts *ViewOptions) error
```

تعيين SetSheetView خصائص عرض الورقة. قد يكون `viewIndex` سالبًا وإذا كان الأمر كذلك يتم حسابه تنازليًا (`-1` هو العرض الأخير).

## احصل على خصائص عرض ورقة العمل {#GetSheetView}

```go
func (f *File) GetSheetView(sheet string, viewIndex int) (ViewOptions, error)
```

يحصل GetSheetView على قيمة خصائص عرض الورقة. قد يكون `viewIndex` سالبًا وإذا كان الأمر كذلك يتم حسابه تنازليًا (`-1` هو العرض الأخير).

## تعيين تخطيط صفحة ورقة العمل {#SetPageLayout}

```go
func (f *File) SetPageLayout(sheet string, opts *PageLayoutOptions) error
```

يوفر SetPageLayout وظيفة لتعيين تخطيط صفحة ورقة العمل. الخيارات المتاحة:

حدد `Size` حجم ورق ورقة العمل ، وحجم الورق الافتراضي لورقة العمل هو "ورقة الرسالة (8.5 بوصة × 11 بوصة)". يوضح ما يلي حجم الورق مرتبة حسب رقم فهرس Excelize:

فهرس|حجم الورق
---|---
1   | ورقة الرسالة (8.5 بوصة × 11 بوصة)
2   | رسالة ورقية صغيرة (8.5 بوصة × 11 بوصة)
3   | ورق التابلويد (11 بوصة × 17 بوصة)
4   | ورق دفتر الأستاذ (17 بوصة × 11 بوصة)
5   | ورقة قانونية (8.5 بوصة × 14 بوصة)
6   | ورقة البيان (5.5 بوصة × 8.5 بوصة)
7   | ورقة تنفيذية (7.25 بوصة × 10.5 بوصة)
8   | ورق A3 (297 مم × 420 مم)
9   | ورق A4 (210 مم × 297 مم)
10  | ورق صغير مقاس A4 (210 مم × 297 مم)
11  | ورق A5 (148 مم × 210 مم)
12  | ورق B4 (250 مم × 353 مم)
13  | ورق B5 (176 مم × 250 مم)
14  | ورق فوليو (8.5 بوصة × 13 بوصة)
15  | ورق الكوارتو (215 مم × 275 مم)
16  | ورق قياسي (10 بوصة × 14 بوصة)
17  | ورق قياسي (11 بوصة × 17 بوصة)
18  | ورقة الملاحظات (8.5 بوصة × 11 بوصة)
19  | #9 ظرف (3.875 بوصة × 8.875 بوصة)
20  | #10 ظرف (4.125 بوصة × 9.5 بوصة)
21  | #11 ظرف (4.5 بوصة × 10.375 بوصة)
22  | #12 ظرف (4.75 بوصة × 11 بوصة)
23  | #14 ظرف (5 بوصة × 11.5 بوصة)
24  | ورق ج (17 بوصة × 22 بوصة)
25  | ورقة د (22 بوصة × 34 بوصة)
26  | والأوراق (34 بوصة × 44 بوصة)
27  | مغلف DL (110 مم × 220 مم)
28  | مظروف C5 (162 مم × 229 مم)
29  | غلاف C3 (324 مم × 458 مم)
30  | مغلف C4 (229 مم × 324 مم)
31  | مغلف C6 (114 مم × 162 مم)
32  | مغلف C65 (114 مم × 229 مم)
33  | مغلف B4 (250 مم × 353 مم)
34  | مغلف B5 (176 مم × 250 مم)
35  | مغلف B6 (176 مم × 125 مم)
36  | غلاف إيطاليا (110 مم × 230 مم)
37  | مظروف العاهل (3.875 بوصة × 7.5 بوصة)
38  | 6¾ ظرف (3.625 بوصة × 6.5 بوصة)
39  | مروحية قياسية أمريكية (14.875 بوصة × 11 بوصة)
40  | مروحة قياسية ألمانية (8.5 بوصة × 12 بوصة)
41  | fanfold القانونية الألمانية (8.5 بوصة × 13 بوصة)
42  | ايزو ب4 (250 مم × 353 مم)
43  | بطاقة بريدية يابانية (100 مم × 148 مم)
44  | ورق قياسي (9 بوصة × 11 بوصة)
45  | ورق قياسي (10 بوصة × 11 بوصة)
46  | ورق قياسي (15 بوصة × 11 بوصة)
47  | دعوة المغلف (220 مم × 220 مم)
50  | حرف ورق إضافي (9.275 بوصة × 12 بوصة)
51  | ورقة إضافية قانونية (9.275 بوصة × 15 بوصة)
52  | صحيفة التابلويد ورقة اضافية (11.69 بوصة × 18 بوصة)
53  | ورق إضافي مقاس A4 (236 مم × 322 مم)
54  | ورقة عرضية الرسالة (8.275 بوصة × 11 بوصة)
55  | ورق عرضي A4 (210 مم × 297 مم)
56  | حرف ورق عرضي إضافي (9.275 بوصة × 12 بوصة)
57  | ورق SuperA/SuperA/A4 (227 مم × 356 مم)
58  | ورق SuperB/SuperB/A3 (305 مم × 487 مم)
59  | حرف زائد ورقة (8.5 بوصة × 12.69 بوصة)
60  | ورق A4 بلس (210 مم × 330 مم)
61  | ورق عرضي A5 (148 مم × 210 مم)
62  | JIS B5 ورقة عرضية (182 مم × 257 مم)
63  | ورق إضافي A3 (322 مم × 445 مم)
64  | ورق إضافي A5 (174 مم × 235 مم)
65  | ورق إضافي ISO B5 (201 مم × 276 مم)
66  | ورق A2 (420 مم × 594 مم)
67  | ورق عرضي A3 (297 مم × 420 مم)
68  | ورق عرضي إضافي مقاس A3 (322 مم × 445 مم)
69  | بطاقة بريدية مزدوجة يابانية (200 مم × 148 مم)
70  | A6 (105 مم × 148 مم)
71  | المغلف الياباني كاكو #2
72  | المغلف الياباني كاكو #3
73  | المغلف الياباني تشو #3
74  | المغلف الياباني تشو #4
75  | تم تدوير الرسالة (11 بوصة × 8½ بوصة)
76  | A3 استدارة (420 مم × 297 مم)
77  | A4 استدارة (297 مم × 210 مم)
78  | A5 استدارة (210 مم × 148 مم)
79  | تم تدوير B4 (JIS). (364 مم × 257 مم)
80  | تم تدوير B5 (JIS). (257 مم × 182 مم)
81  | تم تدوير البطاقة البريدية اليابانية (148 مم × 100 مم)
82  | بطاقة بريدية يابانية مزدوجة تم تدويرها (148 مم × 200 مم)
83  | A6 استدارة (148 مم × 105 مم)
84  | تم تدوير المظروف الياباني Kaku رقم 2
85  | تم تدوير المظروف الياباني Kaku رقم 3
86  | تم تدوير المظروف الياباني Chou رقم 3
87  | تم تدوير المظروف الياباني Chou رقم 4
88  | B6 (JIS) (128 مم × 182 مم)
89  | تم تدوير B6 (JIS) (182 مم × 128 مم)
90  | 12 بوصة × 11 بوصة
91  | المغلف الياباني أنت #4
92  | تم تدوير المظروف الياباني رقم #4
93  | لجان المقاومة الشعبية 16K (146 مم × 215 مم)
94  | لجان المقاومة الشعبية 32K (97 مم × 151 مم)
95  | لجان المقاومة الشعبية 32K (كبير) (97 مم × 151 مم)
96  | مظروف جمهورية الصين الشعبية رقم 1 (102 مم × 165 مم)
97  | مظروف جمهورية الصين الشعبية رقم 2 (102 مم × 176 مم)
98  | مظروف جمهورية الصين الشعبية رقم 3 (125 مم × 176 مم)
99  | مظروف جمهورية الصين الشعبية رقم 4 (110 مم × 208 مم)
100 | مظروف جمهورية الصين الشعبية رقم 5 (110 مم × 220 مم)
101 | مظروف جمهورية الصين الشعبية رقم 6 (120 مم × 230 مم)
102 | مظروف جمهورية الصين الشعبية رقم 7 (160 مم × 230 مم)
103 | مظروف جمهورية الصين الشعبية رقم 8 (120 مم × 309 مم)
104 | مظروف جمهورية الصين الشعبية رقم 9 (229 مم × 324 مم)
105 | مظروف جمهورية الصين الشعبية رقم 10 (324 مم × 458 مم)
106 | استدارة لجان المقاومة الشعبية 16K
107 | لجان المقاومة الشعبية 32K استدارة
108 | جمهورية الصين الشعبية 32K (كبير) استدارة
109 | تم تدوير مظروف جمهورية الصين الشعبية رقم 1 (165 مم × 102 مم)
110 | تم تدوير مظروف جمهورية الصين الشعبية رقم 2 (176 مم × 102 مم)
111 | تم تدوير مظروف جمهورية الصين الشعبية رقم 3 (176 مم × 125 مم)
112 | تم تدوير مظروف جمهورية الصين الشعبية رقم 4 (208 مم × 110 مم)
113 | تم تدوير مظروف جمهورية الصين الشعبية رقم 5 (220 مم × 110 مم)
114 | تم تدوير مظروف جمهورية الصين الشعبية رقم 6 (230 مم × 120 مم)
115 | تم تدوير مظروف جمهورية الصين الشعبية رقم 7 (230 مم × 160 مم)
116 | تم تدوير مظروف جمهورية الصين الشعبية رقم 8 (309 مم × 120 مم)
117 | تم تدوير مظروف جمهورية الصين الشعبية رقم 9 (324 مم × 229 مم)
118 | تم تدوير مظروف جمهورية الصين الشعبية رقم 10 (458 مم × 324 مم)

حدد `Orientation` المحدد في اتجاه ورقة العمل ، والاتجاه الافتراضي هو `portrait`. القيم المحتملة لهذا الحقل هي `portrait` و `landscape`.

حدد `FirstPageNumber` رقم أول صفحة مطبوعة. إذا لم يتم تحديد قيمة ، فسيتم افتراض "تلقائي".

حدد `AdjustTo` مقياس الطباعة. هذه السمة مقيدة بقيم تتراوح من 10 (10٪) إلى 400 (400٪). يتم تجاوز هذا الإعداد عند استخدام `FitToWidth` و / أو `FitToHeight`.

حدد `FitToHeight` عدد الصفحات الرأسية التي سيتم احتواؤها.

حدد `FitToWidth` عدد الصفحات الأفقية التي يجب احتواؤها.

حدد `BlackAndWhite` الطباعة بالأبيض والأسود.

يحدد `PageOrder` ترتيب الصفحات المتعددة. القيم المقبولة: `overThenDown` و `downThenOver`.

- على سبيل المثال ، عيّن تخطيط الصفحة لـ `Sheet1` بطباعة بالأبيض والأسود ، ورقم الصفحة الأول المطبوع من `2` ، وورق A4 صغير الحجم أفقيًا (210 مم × 297 مم) ، صفحتان رأسيتان للملاءمة وصفحتان أفقيتان لملاءمتهما:

```go
f := excelize.NewFile()
var (
    size                 = 10
    orientation          = "landscape"
    firstPageNumber uint = 2
    adjustTo        uint = 100
    fitToHeight          = 2
    fitToWidth           = 2
    blackAndWhite        = true
)
if err := f.SetPageLayout("Sheet1", &excelize.PageLayoutOptions{
    Size:            &size,
    Orientation:     &orientation,
    FirstPageNumber: &firstPageNumber,
    AdjustTo:        &adjustTo,
    FitToHeight:     &fitToHeight,
    FitToWidth:      &fitToWidth,
    BlackAndWhite:   &blackAndWhite,
}); err != nil {
    fmt.Println(err)
}
```

## احصل على تخطيط صفحة ورقة العمل {#GetPageLayout}

```go
func (f *File) GetPageLayout(sheet string) (PageLayoutOptions, error)
```

يوفر GetPageLayout وظيفة للحصول على تخطيط صفحة ورقة العمل.

## تعيين هوامش صفحة ورقة العمل {#SetPageMargins}

```go
func (f *File) SetPageMargins(sheet string, opts *PageLayoutMarginsOptions) error
```

يوفر SetPageMargins وظيفة لتعيين هوامش صفحة ورقة العمل. الخيارات المتاحة:

خيارات|اكتب|وصف
---|---|---
Bottom       | `*float64` | الأسفل
Footer       | `*float64` | تذييل
Header       | `*float64` | رأس
Left         | `*float64` | اليسار
Right        | `*float64` | الصحيح
Top          | `*float64` | قمة
Horizontally | `*bool`    | توسيط في الصفحة: أفقيًا
Vertically   | `*bool`    | توسيط في الصفحة: عموديًا

## احصل على هوامش صفحة ورقة العمل {#GetPageMargins}

```go
func (f *File) GetPageMargins(sheet string) (PageLayoutMarginsOptions, error)
```

يوفر GetPageMargins وظيفة للحصول على هوامش صفحة ورقة العمل.

## تعيين خصائص المصنف {#SetWorkbookProps}

```go
func (f *File) SetWorkbookProps(opts *WorkbookPropsOptions) error
```

يوفر SetWorkbookProps دالة لتعيين خصائص المصنف. الخيارات المتاحة:

خيارات|اكتب|وصف
---|---|---
Date1904      | `*bool`   | يشير إلى ما إذا كان سيتم استخدام نظام تاريخ 1900 أو 1904 عند تحويل أوقات التاريخ التسلسلي في المصنف إلى تواريخ.
FilterPrivacy | `*bool`   | تحدد قيمة منطقية تشير إلى ما إذا كان التطبيق قد قام بفحص المصنف لمعرفة معلومات التعريف الشخصية (PII). إذا تم تعيين هذه العلامة ، فإن التطبيق يحذر المستخدم في أي وقت يقوم فيه المستخدم بإجراء من شأنه إدراج معلومات تحديد الهوية الشخصية في المستند.
CodeName      | `*string` | يحدد الاسم الرمزي للتطبيق الذي أنشأ هذا المصنف. استخدم هذه السمة لتعقب محتوى الملف في الإصدارات المتزايدة من التطبيق.

## احصل على خصائص المصنف {#GetWorkbookProps}

```go
func (f *File) GetWorkbookProps() (WorkbookPropsOptions, error)
```

يوفر GetWorkbookProps دالة للحصول على خصائص المصنف.

## تعيين الرأس والتذييل {#SetHeaderFooter}

```go
func (f *File) SetHeaderFooter(sheet string, opts *HeaderFooterOptions) error
```

يوفر SetHeaderFooter وظيفة لتعيين الرؤوس والتذييلات من خلال اسم ورقة العمل المحددة وأحرف التحكم.

يتم تحديد الرؤوس والتذييلات باستخدام حقول الإعدادات التالية:

مجالات           | وصف
---|---
AlignWithMargins | محاذاة هوامش تذييل الرأس مع هوامش الصفحة
DifferentFirst   | مؤشر مختلف لرأس وتذييل الصفحة الأولىمؤشر مختلف لرأس وتذييل الصفحة الأولى
DifferentOddEven | مؤشرات مختلفة للرؤوس والتذييلات الفردية والزوجية
ScaleWithDoc     | مقياس الرأس والتذييل باستخدام مقياس المستند
OddFooter        | تذييل الصفحة الفردية، أو تذييل الصفحة الأساسي إذا كانت قيمة `DifferentOddEven` هي `false`
OddHeader        | رأس فردي، أو رأس الصفحة الأساسي إذا كانت قيمة `DifferentOddEven` هي `false`
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
            <td>كائن رسومي كخلفية (استخدم AddHeaderFooterImage)</td>
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
err := f.SetHeaderFooter("Sheet1", &excelize.HeaderFooterOptions{
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

## إضافة صورة رأس وتذييل {#AddHeaderFooterImage}

```go
func (f *File) AddHeaderFooterImage(sheet string, opts *HeaderFooterImageOptions) error
```

توفر AddHeaderFooterImage آلية لتعيين الرسومات التي يمكن الرجوع إليها في تعريفات الرأس والتذييل عبر `&G`، وأنواع الصور المدعومة: EMF، EMZ، GIF، JPEG، JPG، PNG، SVG، TIF، TIFF، WMF و WMZ.

## تعيين الاسم المحدد {#SetDefinedName}

```go
func (f *File) SetDefinedName(definedName *DefinedName) error
```

يوفر SetDefinedName دالة لتعيين الأسماء المحددة للمصنف أو ورقة العمل. إذا لم يتم تحديد النطاق ، فإن النطاق الافتراضي هو المصنف. فمثلا:

```go
err := f.SetDefinedName(&excelize.DefinedName{
    Name:     "Amount",
    RefersTo: "Sheet1!$A$2:$D$5",
    Comment:  "defined name comment",
    Scope:    "Sheet2",
})
```

إعدادات منطقة الطباعة وعناوين الطباعة لورقة العمل:

<p align="center"><img width="628" src="./images/page_setup_01.png" alt="منطقة الطباعة وإعدادات عناوين الطباعة لورقة العمل"></p>

```go
if err := f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Area",
    RefersTo: "Sheet1!$A$1:$Z$100",
    Scope:    "Sheet1",
}); err != nil {
    fmt.Println(err)
}
if err := f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Titles",
    RefersTo: "Sheet1!$A:$A,Sheet1!$1:$1",
    Scope:    "Sheet1",
}); err != nil {
    fmt.Println(err)
}
```

إذا قمت بملء خاصية `RefersTo` بنطاق عمود واحد فقط بدون فاصلة، فسوف تعمل كـ "الأعمدة التي سيتم تكرارها على اليسار" فقط. على سبيل المثال:

```go
if err := f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Titles",
    RefersTo: "Sheet1!$A:$A",
    Scope:    "Sheet1",
}); err != nil {
    fmt.Println(err)
}
```

إذا قمت بملء خاصية `RefersTo` بنطاق صف واحد فقط دون فاصلة، فسوف تعمل كـ "الصفوف التي سيتم تكرارها في الأعلى" فقط. على سبيل المثال:

```go
if err := f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Titles",
    RefersTo: "Sheet1!$1:$1",
    Scope:    "Sheet1",
}); err != nil {
    fmt.Println(err)
}
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
err := f.DeleteDefinedName(&excelize.DefinedName{
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

خاصية | وصف
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

## تعيين خصائص الحساب {#SetCalcProps}

```go
func (f *File) SetCalcProps(opts *CalcPropsOptions) error
```

يوفر SetCalcProps دالة لتعيين خصائص الحساب.

القيمة الاختيارية لخاصية `CalcMode` هي: `manual` أو `auto` أو `autoNoTable`.

القيمة الاختيارية للخاصية `RefMode` هي: `A1` أو `R1C1`.

## الحصول على خصائص الحساب {#GetCalcProps}

```go
func (f *File) GetCalcProps() (CalcPropsOptions, error)
```

يوفر GetCalcProps دالة للحصول على خصائص الحساب.

## حماية المصنف {#ProtectWorkbook}

```go
func (f *File) ProtectWorkbook(opts *WorkbookProtectionOptions) error
```

يوفر ProtectWorkbook وظيفة لمنع المستخدمين الآخرين من تغيير أو نقل أو حذف البيانات في مصنف عن طريق الخطأ أو عن عمد. الحقل الاختياري `AlgorithmName` خوارزمية التجزئة المحددة ، ودعم XOR و MD4 و MD5 و SHA-1 و SHA2-56 و SHA-384 و SHA-512 حاليًا ، إذا لم يتم تحديد خوارزمية تجزئة ، فسيتم استخدام خوارزمية XOR كإعداد افتراضي. على سبيل المثال ، حماية المصنف بإعدادات الحماية:

```go
err := f.ProtectWorkbook(&excelize.WorkbookProtectionOptions{
    Password:      "password",
    LockStructure: true,
})
```

WorkbookProtectionOptions تعيين إعدادات حماية المصنف مباشرة.

```go
type WorkbookProtectionOptions struct {
    AlgorithmName string
    Password      string
    LockStructure bool
    LockWindows   bool
}
```

## إلغاء حماية المصنف {#UnprotectWorkbook}

```go
func (f *File) UnprotectWorkbook(password ...string) error
```

يوفر UnprotectWorkbook وظيفة لإزالة الحماية للمصنف ، وحدد معلمة كلمة المرور الاختيارية لإزالة حماية المصنف باستخدام التحقق من كلمة المرور.
