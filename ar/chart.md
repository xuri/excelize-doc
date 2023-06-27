# الرسم البياني

## أضف الرسم البياني {#AddChart}

```go
func (f *File) AddChart(sheet, cell string, chart *ChartOptions, combo ...*ChartOptions) error
```

يوفر AddChart طريقة لإضافة مخطط في ورقة عمل من خلال مجموعة تنسيق مخطط معين (مثل الإزاحة والقياس وإعدادات نسبة العرض إلى الارتفاع وإعدادات الطباعة) ومجموعة الخصائص.

يوضح ما يلي `Type` الرسم البياني الذي يدعمه برنامج excelize:

ID|تعداد|الرسم البياني
---|---|---
0  | Area                        | مخطط منطقة ثنائي الأبعاد
1  | AreaStacked                 | مخطط مساحي مكدس ثنائي الأبعاد
2  | AreaPercentStacked          | مخطط مساحي مكدس بنسبة 100٪ ثنائي الأبعاد
3  | Area3D                      | مخطط مساحي ثلاثي الأبعاد
4  | Area3DStacked               | ممخطط مساحي مكدس ثلاثي الأبعاد
5  | Area3DPercentStacked        | مخطط مساحي مكدس بنسبة 100٪ ثلاثي الأبعاد
6  | Bar                         | مخطط شريطي متفاوت الأبعاد ثنائي الأبعاد
7  | BarStacked                  | مخطط شريطي مكدس ثنائي الأبعاد
8  | BarPercentStacked           | مخطط شريطي مكدس ثنائي الأبعاد بنسبة 100٪
9  | Bar3DClustered              | مخطط شريطي ثلاثي الأبعاد متفاوت
10 | Bar3DStacked                | مخطط شريطي مكدس ثلاثي الأبعاد
11 | Bar3DPercentStacked         | مخطط شريطي مكدس ثلاثي الأبعاد بنسبة 100٪
12 | Bar3DConeClustered          | مخطط شريطي مخروطي ثلاثي الأبعاد متفاوت
13 | Bar3DConeStacked            | مخطط شريطي مخروطي ثلاثي الأبعاد مكدس
14 | Bar3DConePercentStacked     | مخطط شريطي مخروطي 100٪ ثلاثي الأبعاد
15 | Bar3DPyramidClustered       | ممخطط شريطي ثلاثي الأبعاد هرمي متفاوت
16 | Bar3DPyramidStacked         | الرسم البياني الشريطي ثلاثي الأبعاد المكدس بالهرم
17 | Bar3DPyramidPercentStacked  | الرسم البياني الشريطي ثلاثي الأبعاد المكدس بالهرم 100٪
18 | Bar3DCylinderClustered      | مخطط شريطي اسطوانات ثلاثية الأبعاد متفاوت المسافات
19 | Bar3DCylinderStacked        | مخطط شريطي مكدس اسطوانة ثلاثية الأبعاد
20 | Bar3DCylinderPercentStacked | مخطط شريطي مكدس اسطوانة ثلاثية الأبعاد 100٪
21 | Col                         | مخطط عمودي ثنائي الأبعاد متفاوت
22 | ColStacked                  | مخطط عمودي مكدس ثنائي الأبعاد
23 | ColPercentStacked           | مخطط عمودي مكدس ثنائي الأبعاد 100٪
24 | Col3DClustered              | مخطط عمودي ثلاثي الأبعاد متفاوت
25 | Col3D                       | مخطط عمودي ثلاثي الأبعاد
26 | Col3DStacked                | مخطط عمودي مكدس ثلاثي الأبعاد
27 | Col3DPercentStacked         | مخطط عمودي مكدس ثلاثي الأبعاد 100٪
28 | Col3DCone                   | ممخطط عمودي مخروطي ثلاثي الأبعاد
29 | Col3DConeClustered          | مخطط عمودي مخروط ثلاثي الأبعاد متفاوت المسافات
30 | Col3DConeStacked            | ممخطط عمودي مكدس مخروطي ثلاثي الأبعاد
31 | Col3DConePercentStacked     | مخطط عمودي مكدس مخروطي ثلاثي الأبعاد 100٪
32 | Col3DPyramid                | مخطط عمودي هرمي ثلاثي الأبعاد
33 | Col3DPyramidClustered       | مخطط عمودي هرم ثلاثي الأبعاد متفاوت
34 | Col3DPyramidStacked         | مخطط عمودي هرمي ثلاثي الأبعاد مكدس
35 | Col3DPyramidPercentStacked  | مخطط عمودي هرمي ثلاثي الأبعاد مكدس 100٪
36 | Col3DCylinder               | مخطط عمودي اسطوانات ثلاثية الأبعاد
37 | Col3DCylinderClustered      | مخطط عمود أسطواني ثلاثي الأبعاد متفاوت
38 | Col3DCylinderStacked        | مخطط عمودي مكدس بأسطوانة ثلاثية الأبعاد
39 | Col3DCylinderPercentStacked | مخطط عمودي مكدس بأسطوانة ثلاثية الأبعاد 100٪
40 | Doughnut                    | دونات الرسم البياني
41 | Line                        | مخطط خطي
42 | Line3D                      | مخطط خطي ثلاثي الأبعاد
43 | Pie                         | مخطط دائري
44 | Pie3D                       | مخطط دائري ثلاثي الأبعاد
45 | PieOfPie                    | مخطط دائري مزدوج
46 | BarOfPie                    | شريط الرسم البياني
47 | Radar                       | مخطط رادار
48 | Scatter                     | مخطط مبعثر
49 | Surface3D                   | مخطط سطحي ثلاثي الأبعاد
50 | WireframeSurface3D          | مخطط سطح إطار سلكي ثلاثي الأبعاد
51 | Contour                     | مخطط كونتور
52 | WireframeContour            | مخطط كفاف الإطار السلكي
53 | Bubble                      | مخطط فقاعي
54 | Bubble3D                    | مخطط فقاعي ثلاثي الأبعاد

في نطاق بيانات مخطط Office Excel ، تحدد `Series` مجموعة المعلومات التي سيتم رسم البيانات لها ، وعنصر وسيلة الإيضاح (سلسلة) ، وتسمية المحور الأفقي (الفئة).

خيارات `Series` التي يمكن تعيينها هي:

معامل|تفسير
---|---
Name|عنصر وسيلة الإيضاح (سلسلة) ، معروض في وسيلة إيضاح الرسم البياني وشريط الصيغة. معلمة `Name` اختيارية. إذا لم تحدد هذه القيمة ، فستكون القيمة الافتراضية هي `Series 1 .. n`. دعم `Name` لتمثيل الصيغة ، على سبيل المثال: `Sheet1!$A$1`.
Categories|تسمية المحور الأفقي (الفئة). معلمة `Categories` اختيارية في معظم أنواع المخططات ، والمعلمة الافتراضية هي تسلسل متجاور من النموذج `1..n`.
Values|تعتبر منطقة بيانات المخطط ، وهي أهم معلمة في `Series` ، هي أيضًا المعلمة الوحيدة المطلوبة عند إنشاء مخطط. يربط هذا الخيار المخطط ببيانات ورقة العمل التي يعرضها.
Line|هذا يحدد تنسيق الخط للمخطط الخطي. تعتبر خاصية `Line` اختيارية وإذا لم يتم توفيرها ، فسيتم نمطها الافتراضي. الخيارات التي يمكن تعيينها هي `Width`. نطاق `Width` هو 0.25 نقطة - 999 نقطة. إذا كانت قيمة العرض خارج النطاق ، فإن العرض الافتراضي للخط هو 2 نقطة.
Marker|يؤدي هذا إلى تعيين علامة المخطط الخطي والمخطط المبعثر. نطاق الحقل الاختياري `Size` هو 2-72 (القيمة الافتراضية هي `5`). قيمة التعداد للحقل الاختياري `Symbol` هي (القيمة الافتراضية هي `auto`): `circle`, `dash`, `diamond`, `dot`, `none`, `picture`, `plus`, `square`, `star`, `triangle`, `x`, `auto`.

تعيين خصائص وسيلة إيضاح الرسم البياني. الخيارات التي يمكن ضبطها هي:

معامل|اكتب|تفسير
---|---|---
Position        | `string` | موضع وسيلة إيضاح الرسم البياني
ShowLegendKey   | `bool`   | تعيين مفاتيح وسيلة الإيضاح يجب أن تظهر في تسميات البيانات

قم بتعيين `Position` لوسيلة إيضاح الرسم البياني. موضع وسيلة الإيضاح الافتراضي هو `right`. الوظائف المتاحة هي:

معامل|تفسير
---|---
none|تعطيل وسيلة الإيضاح
top|على القمة
bottom|في الاسفل
left|على اليسار
right|على اليمين
top_right|في أعلى اليمين

تعيين المعلمة `ShowLegendKey`  ، يجب أن تظهر مفاتيح وسيلة الإيضاح في ملصقات البيانات. القيمة الافتراضية هي `false`.

يتم تعيين عنوان المخطط عن طريق تحديد معلمة `Name` لكائن `Title` ، وسيتم عرض العنوان أعلى المخطط. تدعم المعلمة `Name` استخدام تمثيلات الصيغة ، مثل `Sheet1!$A$1` ، إذا لم تحدد عنوان رمز ، فستكون القيمة الافتراضية خالية.

توفر المعلمة `ShowBlanksAs` إعداد "إخفاء الخلايا وإفراغها". القيمة الافتراضية هي: `gap`. في تطبيق Excel "يتم عرض الخلية الفارغة على أنها": "الفراغ". فيما يلي قيم اختيارية لهذه المعلمة:

معامل|تفسير
---|---
gap|الفراغ
span|ربط نقاط البيانات بخطوط مستقيمة
zero|قيمة صفرية

يحدد أن لكل علامة بيانات في السلسلة لون مختلف حسب `VaryColors`. القيمة الافتراضية هي `true`.

توفر المعلمة `Format` إعدادات للمعلمات مثل إزاحة المخطط ، والمقياس ، وإعدادات نسبة العرض إلى الارتفاع ، وخصائص الطباعة ، بالإضافة إلى تلك المستخدمة في الوظيفة [`AddPicture`](image.md#AddPicture).

تعيين موضع منطقة رسم المخطط بواسطة منطقة الرسم. الخصائص التي يمكن تعيينها هي:

معامل|اكتب|إفتراضي|تفسير
---|---|---|---
ShowBubbleSize  | `bool` | `false` | يحدد حجم الفقاعة الذي يجب أن يظهر في ملصق البيانات.
ShowCatName     | `bool` | `false` | اسم التصنيف
ShowLeaderLines | `bool` | `false` | يحدد أن اسم الفئة يجب أن يظهر في تسمية البيانات.
ShowPercent     | `bool` | `false` | يحدد أن النسبة يجب أن تظهر في تسمية البيانات.
ShowSerName     | `bool` | `false` | يحدد أن اسم السلسلة يجب أن يظهر في تسمية البيانات.
ShowVal         | `bool` | `false` | يحدد أن القيمة يجب أن تظهر في تسمية البيانات.

عيّن الخيارات الأساسية للمحور الأفقي والعمودي حسب `XAxis` و `YAxis`.

خصائص `XAxis` التي يمكن تعيينها هي:

معامل|اكتب|إفتراضي|تفسير
---|---|---|---
None           | `bool`          | `false` | تعطيل المحاور.
MajorGridLines | `bool`          | `false` | يحدد خطوط الشبكة الرئيسية.
MinorGridLines | `bool`          | `false` | يحدد خطوط الشبكة الثانوية.
TickLabelSkip  | `int`           | `1`     | يحدد عدد علامات التجزئة المطلوب تخطيها بين التسمية المرسومة. خاصية `TickLabelSkip` اختيارية. القيمة الافتراضية هي تلقائي.
ReverseOrder   | `bool`          | `false` | يحدد أن الفئات أو القيم بترتيب عكسي (اتجاه المخطط). خاصية `ReverseOrder` اختيارية.
Maximum        | `*float64`      | `0`     | يحدد أن الحد الأقصى الثابت ، 0 هو تلقائي. الخاصية القصوى اختيارية.
Minimum        | `*float64`      | `0`     | يحدد أن الحد الأدنى الثابت ، 0 هو تلقائي. الحد الأدنى من الممتلكات اختياري. القيمة الافتراضية هي تلقائي.
Font           | `Font`          | غير متاح| يحدد أن خط المحور الأفقي.
NumFmt         | `ChartNumFmt`   | غير متاح| يحدد أنه في حالة الارتباط بالمصدر وتعيين رمز تنسيق رقم مخصص للمحور.
Title          | `[]RichTextRun` | غير متاح| يحدد أن عنوان المحور الأفقي الأساسي وتغيير حجم المخطط.

خصائص `YAxis` التي يمكن تعيينها هي:

معامل|اكتب|إفتراضي|تفسير
---|---|---|---
None           | `bool`          | `false` |تعطيل المحاور.
MajorGridLines | `bool`          | `false` | يحدد خطوط الشبكة الرئيسية.
MinorGridLines | `bool`          | `false` | يحدد خطوط الشبكة الثانوية.
MajorUnit      | `float64`       | `0`     | يحدد المسافة بين العلامات الرئيسية. يجب أن يحتوي على رقم موجب من الفاصلة العائمة. الخاصية `MajorUnit` اختيارية. القيمة الافتراضية هي تلقائي.
ReverseOrder   | `bool`          | `false` | يحدد أن الفئات أو القيم بترتيب عكسي (اتجاه المخطط). خاصية `ReverseOrder` اختيارية.
Maximum        | `*float64`      | `0`     | يحدد أن الحد الأقصى الثابت ، 0 هو تلقائي. الخاصية القصوى اختيارية.
Minimum        | `*float64`      | `0`     | يحدد أن الحد الأدنى الثابت ، 0 هو تلقائي. الحد الأدنى من الممتلكات اختياري. القيمة الافتراضية هي تلقائي.
Font           | `Font`          | غير متاح| يحدد أن خط المحور الرأسي.
LogBase        | `float64`       | غير متاح| يحدد الرقم الأساسي للمقياس اللوغاريتمي للمحور العمودي.
NumFmt         | `ChartNumFmt`   | غير متاح| يحدد أنه في حالة الارتباط بالمصدر وتعيين رمز تنسيق رقم مخصص للمحور.
Title          | `[]RichTextRun` | غير متاح| يحدد أن عنوان المحور الرأسي الأساسي وتغيير حجم المخطط.

عيِّن حجم الرسم البياني حسب خاصية `Dimension`. خاصية البعد اختيارية. الخصائص التي يمكن تعيينها هي:

معامل|اكتب|إفتراضي|تفسير
---|---|---|---
Height | `uint` | 260 | ارتفاع
Width  | `uint` | 480 | عرض

تحدد المعلمة `combo` إنشاء مخطط يجمع بين نوعين أو أكثر من أنواع المخططات في مخطط واحد. على سبيل المثال ، أنشئ مخططًا خطيًا متفاوت المسافات يحتوي على البيانات `Sheet1!$E$1:$L$15`:

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
    for idx, row := range [][]interface{}{
        {nil, "تفاح", "برتقال", "كمثرى"},
        {"صغير", 2, 3, 3},
        {"عادي", 5, 2, 4},
        {"كبير", 6, 7, 8},
    } {
        cell, err := excelize.CoordinatesToCellName(1, idx+1)
        if err != nil {
            fmt.Println(err)
            return
        }
        if err := f.SetSheetRow("Sheet1", cell, &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    enable, disable := true, false
    if err := f.SetSheetView("Sheet1", -1, &excelize.ViewOptions{
        RightToLeft: &enable,
    }); err != nil {
        fmt.Println(err)
    }
    if err := f.AddChart("Sheet1", "E1", &excelize.Chart{
        Type: excelize.Col,
        Series: []excelize.ChartSeries{
            {
                Name:       "Sheet1!$A$2",
                Categories: "Sheet1!$B$1:$D$1",
                Values:     "Sheet1!$B$2:$D$2",
            },
        },
        Format: excelize.GraphicOptions{
            ScaleX:          1,
            ScaleY:          1,
            OffsetX:         15,
            OffsetY:         10,
            PrintObject:     &enable,
            LockAspectRatio: false,
            Locked:          &disable,
        },
        Title: excelize.ChartTitle{
            Name: "عمود متفاوت المسافات - تخطيط خطي",
        },
        Legend: excelize.ChartLegend{
            Position: "left",
        },
        PlotArea: excelize.ChartPlotArea{
            ShowCatName:     false,
            ShowLeaderLines: false,
            ShowPercent:     true,
            ShowSerName:     true,
            ShowVal:         true,
        },
    }, &excelize.Chart{
        Type: excelize.Line,
        Series: []excelize.ChartSeries{
            {
                Name:       "Sheet1!$A$4",
                Categories: "Sheet1!$B$1:$D$1",
                Values:     "Sheet1!$B$4:$D$4",
                Marker: excelize.ChartMarker{
                    Symbol: "none", Size: 10,
                },
            },
        },
        Format: excelize.GraphicOptions{
            ScaleX:          1,
            ScaleY:          1,
            OffsetX:         15,
            OffsetY:         10,
            PrintObject:     &enable,
            LockAspectRatio: false,
            Locked:          &disable,
        },
        Legend: excelize.ChartLegend{
            Position: "right",
        },
        PlotArea: excelize.ChartPlotArea{
            ShowCatName:     false,
            ShowLeaderLines: false,
            ShowPercent:     true,
            ShowSerName:     true,
            ShowVal:         true,
        },
    }); err != nil {
        fmt.Println(err)
        return
    }
    // احفظ جدول البيانات بالمسار المحدد.
    if err := f.SaveAs("المصنف1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## أضف ورقة عمل المخطط {#AddChartSheet}

```go
func (f *File) AddChartSheet(sheet string, chart *ChartOptions, combo ...*ChartOptions) error
```

توفر AddChartSheet طريقة لإنشاء ورقة مخطط من خلال مجموعة تنسيق مخطط معينة (مثل الإزاحة والمقياس وإعداد نسبة العرض إلى الارتفاع وإعدادات الطباعة) ومجموعة الخصائص. في Excel ، ورقة المخطط هي ورقة عمل تحتوي فقط على مخطط.

## حذف مخطط {#DeleteChart}

```go
func (f *File) DeleteChart(sheet, cell string) error
```

يوفر DeleteChart وظيفة لحذف المخططات في جدول بيانات عن طريق اسم الخلية وورقة العمل المحددة.
