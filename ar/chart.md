# الرسم البياني

## أضف الرسم البياني {#AddChart}

```go
func (f *File) AddChart(sheet, cell, format string, combo ...string) error
```

يوفر AddChart طريقة لإضافة مخطط في ورقة عمل من خلال مجموعة تنسيق مخطط معين (مثل الإزاحة والقياس وإعدادات نسبة العرض إلى الارتفاع وإعدادات الطباعة) ومجموعة الخصائص.

يوضح ما يلي `type` الرسم البياني الذي يدعمه برنامج excelize:

اكتب|الرسم البياني
---|---
area                        | مخطط منطقة ثنائي الأبعاد
areaStacked                 | مخطط مساحي مكدس ثنائي الأبعاد
areaPercentStacked          | مخطط مساحي مكدس بنسبة 100٪ ثنائي الأبعاد
area3D                      | مخطط مساحي ثلاثي الأبعاد
area3DStacked               | ممخطط مساحي مكدس ثلاثي الأبعاد
area3DPercentStacked        | مخطط مساحي مكدس بنسبة 100٪ ثلاثي الأبعاد
bar                         | مخطط شريطي متفاوت الأبعاد ثنائي الأبعاد
barStacked                  | مخطط شريطي مكدس ثنائي الأبعاد
barPercentStacked           | مخطط شريطي مكدس ثنائي الأبعاد بنسبة 100٪
bar3DClustered              | مخطط شريطي ثلاثي الأبعاد متفاوت
bar3DStacked                | مخطط شريطي مكدس ثلاثي الأبعاد
bar3DPercentStacked         | مخطط شريطي مكدس ثلاثي الأبعاد بنسبة 100٪
bar3DConeClustered          | مخطط شريطي مخروطي ثلاثي الأبعاد متفاوت
bar3DConeStacked            | مخطط شريطي مخروطي ثلاثي الأبعاد مكدس
bar3DConePercentStacked     | مخطط شريطي مخروطي 100٪ ثلاثي الأبعاد
bar3DPyramidClustered       | ممخطط شريطي ثلاثي الأبعاد هرمي متفاوت
bar3DPyramidStacked         | الرسم البياني الشريطي ثلاثي الأبعاد المكدس بالهرم
bar3DPyramidPercentStacked  | الرسم البياني الشريطي ثلاثي الأبعاد المكدس بالهرم 100٪
bar3DCylinderClustered      | مخطط شريطي اسطوانات ثلاثية الأبعاد متفاوت المسافات
bar3DCylinderStacked        | مخطط شريطي مكدس اسطوانة ثلاثية الأبعاد
bar3DCylinderPercentStacked | مخطط شريطي مكدس اسطوانة ثلاثية الأبعاد 100٪
col                         | مخطط عمودي ثنائي الأبعاد متفاوت
colStacked                  | مخطط عمودي مكدس ثنائي الأبعاد
colPercentStacked           | مخطط عمودي مكدس ثنائي الأبعاد 100٪
col3DClustered              | مخطط عمودي ثلاثي الأبعاد متفاوت
col3D                       | مخطط عمودي ثلاثي الأبعاد
col3DStacked                | مخطط عمودي مكدس ثلاثي الأبعاد
col3DPercentStacked         | مخطط عمودي مكدس ثلاثي الأبعاد 100٪
col3DCone                   | ممخطط عمودي مخروطي ثلاثي الأبعاد
col3DConeClustered          | مخطط عمودي مخروط ثلاثي الأبعاد متفاوت المسافات
col3DConeStacked            | ممخطط عمودي مكدس مخروطي ثلاثي الأبعاد
col3DConePercentStacked     | مخطط عمودي مكدس مخروطي ثلاثي الأبعاد 100٪
col3DPyramid                | مخطط عمودي هرمي ثلاثي الأبعاد
col3DPyramidClustered       | مخطط عمودي هرم ثلاثي الأبعاد متفاوت
col3DPyramidStacked         | مخطط عمودي هرمي ثلاثي الأبعاد مكدس
col3DPyramidPercentStacked  | مخطط عمودي هرمي ثلاثي الأبعاد مكدس 100٪
col3DCylinder               | مخطط عمودي اسطوانات ثلاثية الأبعاد
col3DCylinderClustered      | مخطط عمود أسطواني ثلاثي الأبعاد متفاوت
col3DCylinderStacked        | مخطط عمودي مكدس بأسطوانة ثلاثية الأبعاد
col3DCylinderPercentStacked | مخطط عمودي مكدس بأسطوانة ثلاثية الأبعاد 100٪
doughnut                    | دونات الرسم البياني
line                        | مخطط خطي
pie                         | مخطط دائري
pie3D                       | مخطط دائري ثلاثي الأبعاد
radar                       | مخطط رادار
scatter                     | مخطط مبعثر
surface3D                   | مخطط سطحي ثلاثي الأبعاد
wireframeSurface3D          | مخطط سطح إطار سلكي ثلاثي الأبعاد
contour                     | مخطط كونتور
wireframeContour            | مخطط كفاف الإطار السلكي
bubble                      | مخطط فقاعي
bubble3D                    | مخطط فقاعي ثلاثي الأبعاد

في نطاق بيانات مخطط Office Excel ، تحدد `series` مجموعة المعلومات التي سيتم رسم البيانات لها ، وعنصر وسيلة الإيضاح (سلسلة) ، وتسمية المحور الأفقي (الفئة).

خيارات `series` التي يمكن تعيينها هي:

معامل|تفسير
---|---
name|عنصر وسيلة الإيضاح (سلسلة) ، معروض في وسيلة إيضاح الرسم البياني وشريط الصيغة. معلمة `name` اختيارية. إذا لم تحدد هذه القيمة ، فستكون القيمة الافتراضية هي `Series 1 .. n`. دعم `name` لتمثيل الصيغة ، على سبيل المثال: `Sheet1!$A$1`.
categories|تسمية المحور الأفقي (الفئة). معلمة `categories` اختيارية في معظم أنواع المخططات ، والمعلمة الافتراضية هي تسلسل متجاور من النموذج `1..n`.
values|تعتبر منطقة بيانات المخطط ، وهي أهم معلمة في `series` ، هي أيضًا المعلمة الوحيدة المطلوبة عند إنشاء مخطط. يربط هذا الخيار المخطط ببيانات ورقة العمل التي يعرضها.
line|هذا يحدد تنسيق الخط للمخطط الخطي. تعتبر خاصية `line` اختيارية وإذا لم يتم توفيرها ، فسيتم نمطها الافتراضي. الخيارات التي يمكن تعيينها هي `width`. نطاق `width` هو 0.25 نقطة - 999 نقطة. إذا كانت قيمة العرض خارج النطاق ، فإن العرض الافتراضي للخط هو 2 نقطة.
marker|يؤدي هذا إلى تعيين علامة المخطط الخطي والمخطط المبعثر. نطاق الحقل الاختياري `size` هو 2-72 (القيمة الافتراضية هي `5`). قيمة التعداد للحقل الاختياري `symbol` هي (القيمة الافتراضية هي `auto`): `circle`, `dash`, `diamond`, `dot`, `none`, `picture`, `plus`, `square`, `star`, `triangle`, `x`, `auto`.

تعيين خصائص وسيلة إيضاح الرسم البياني. الخيارات التي يمكن ضبطها هي:

معامل|اكتب|تفسير
---|---|---
none|bool|حدد ما إذا كنت تريد إظهار وسيلة الإيضاح دون تداخل الرسم البياني القيمة الافتراضية هي `false`
position|string|موضع وسيلة إيضاح الرسم البياني
show_legend_key|bool|تعيين مفاتيح وسيلة الإيضاح يجب أن تظهر في تسميات البيانات

قم بتعيين `position` لوسيلة إيضاح الرسم البياني. موضع وسيلة الإيضاح الافتراضي هو `right`. تسري هذه المعلمة فقط عندما تكون `none` هي `false`. الوظائف المتاحة هي:

معامل|تفسير
---|---
top|على القمة
bottom|في الاسفل
left|على اليسار
right|على اليمين
top_right|في أعلى اليمين

تعيين المعلمة `show_legend_key` ، يجب أن تظهر مفاتيح وسيلة الإيضاح في ملصقات البيانات. القيمة الافتراضية هي `false`.

يتم تعيين عنوان المخطط عن طريق تحديد معلمة `name` لكائن `title` ، وسيتم عرض العنوان أعلى المخطط. تدعم المعلمة `name` استخدام تمثيلات الصيغة ، مثل `Sheet1!$A$1` ، إذا لم تحدد عنوان رمز ، فستكون القيمة الافتراضية خالية.

توفر المعلمة `show_blanks_as` إعداد "إخفاء الخلايا وإفراغها". القيمة الافتراضية هي: `gap`. في تطبيق Excel "يتم عرض الخلية الفارغة على أنها": "الفراغ". فيما يلي قيم اختيارية لهذه المعلمة:

معامل|تفسير
---|---
gap|الفراغ
span|ربط نقاط البيانات بخطوط مستقيمة
zero|قيمة صفرية

يحدد أن لكل علامة بيانات في السلسلة لون مختلف حسب `vary_colors`. القيمة الافتراضية هي `true`.

توفر المعلمة `format` إعدادات للمعلمات مثل إزاحة المخطط ، والمقياس ، وإعدادات نسبة العرض إلى الارتفاع ، وخصائص الطباعة ، بالإضافة إلى تلك المستخدمة في الوظيفة [`AddPicture()`](image.md#AddPicture).

تعيين موضع منطقة رسم المخطط بواسطة منطقة الرسم. الخصائص التي يمكن تعيينها هي:

معامل|اكتب|إفتراضي|تفسير
---|---|---|---
show_bubble_size|bool|`false`|يحدد حجم الفقاعة الذي يجب أن يظهر في ملصق البيانات.
show_cat_name|bool|`true`|اسم التصنيف
show_leader_lines|bool|`false`|يحدد أن اسم الفئة يجب أن يظهر في تسمية البيانات.
show_percent|bool|`false`|يحدد أن النسبة يجب أن تظهر في تسمية البيانات.
show_series_name|bool|`false`|يحدد أن اسم السلسلة يجب أن يظهر في تسمية البيانات.
show_val|bool|`false`|يحدد أن القيمة يجب أن تظهر في تسمية البيانات.

عيّن الخيارات الأساسية للمحور الأفقي والعمودي حسب `x_axis` و `y_axis`.

خصائص `x_axis` التي يمكن تعيينها هي:

معامل|اكتب|إفتراضي|تفسير
---|---|---|---
none|bool|`false`|تعطيل المحاور.
major_grid_lines|bool|`false`|يحدد خطوط الشبكة الرئيسية.
minor_grid_lines|bool|`false`|يحدد خطوط الشبكة الثانوية.
tick_label_skip|int|`1`|يحدد عدد علامات التجزئة المطلوب تخطيها بين التسمية المرسومة. خاصية `tick_label_skip` اختيارية. القيمة الافتراضية هي تلقائي.
reverse_order|bool|`false`|يحدد أن الفئات أو القيم بترتيب عكسي (اتجاه المخطط). خاصية `reverse_order` اختيارية.
maximum|int|`0`|يحدد أن الحد الأقصى الثابت ، 0 هو تلقائي. الخاصية القصوى اختيارية.
minimum|int|`0`|يحدد أن الحد الأدنى الثابت ، 0 هو تلقائي. الحد الأدنى من الممتلكات اختياري. القيمة الافتراضية هي تلقائي.

خصائص `y_axis` التي يمكن تعيينها هي:

معامل|اكتب|إفتراضي|تفسير
---|---|---|---
none|bool|`false`|تعطيل المحاور.
major_grid_lines|bool|`false`|يحدد خطوط الشبكة الرئيسية.
minor_grid_lines|bool|`false`|يحدد خطوط الشبكة الثانوية.
major_unit|float64|`0`|يحدد المسافة بين العلامات الرئيسية. يجب أن يحتوي على رقم موجب من الفاصلة العائمة. الخاصية `major_unit` اختيارية. القيمة الافتراضية هي تلقائي.
reverse_order|bool|`false`|يحدد أن الفئات أو القيم بترتيب عكسي (اتجاه المخطط). خاصية `reverse_order` اختيارية.
maximum|int|`0`|يحدد أن الحد الأقصى الثابت ، 0 هو تلقائي. الخاصية القصوى اختيارية.
minimum|int|`0`|يحدد أن الحد الأدنى الثابت ، 0 هو تلقائي. الحد الأدنى من الممتلكات اختياري. القيمة الافتراضية هي تلقائي.

عيِّن حجم الرسم البياني حسب خاصية `dimension`. خاصية البعد اختيارية. الخصائص التي يمكن تعيينها هي:

معامل|اكتب|إفتراضي|تفسير
---|---|---|---
height|int|290|ارتفاع
width|int|480|عرض

تحدد المعلمة `combo` إنشاء مخطط يجمع بين نوعين أو أكثر من أنواع المخططات في مخطط واحد. على سبيل المثال ، أنشئ مخططًا خطيًا متفاوت المسافات يحتوي على البيانات `Sheet1!$E$1:$L$15`:

```go
package main

import (
    "fmt"

    "github.com/360EntSecGroup-Skylar/excelize/v2"
)

func main() {
    categories := map[string]string{
        "A2": "صغير", "A3": "عادي", "A4": "كبير",
        "B1": "تفاح", "C1": "برتقال", "D1": "كمثرى"}
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
        "type": "col",
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
            "position": "left",
            "show_legend_key": false
        },
        "title":
        {
            "name": "عمود متفاوت المسافات - تخطيط خطي"
        },
        "plotarea":
        {
            "show_bubble_size": true,
            "show_cat_name": false,
            "show_leader_lines": false,
            "show_percent": true,
            "show_series_name": true,
            "show_val": true
        }
    }`, `{
        "type": "line",
        "series": [
        {
            "name": "Sheet1!$A$4",
            "categories": "Sheet1!$B$1:$D$1",
            "values": "Sheet1!$B$4:$D$4"
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
            "position": "right",
            "show_legend_key": false
        },
        "plotarea":
        {
            "show_bubble_size": true,
            "show_cat_name": false,
            "show_leader_lines": false,
            "show_percent": true,
            "show_series_name": true,
            "show_val": true
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

## أضف ورقة عمل المخطط {#AddChartSheet}

```go
func (f *File) AddChartSheet(sheet, format string, combo ...string) error
```

توفر AddChartSheet طريقة لإنشاء ورقة مخطط من خلال مجموعة تنسيق مخطط معينة (مثل الإزاحة والمقياس وإعداد نسبة العرض إلى الارتفاع وإعدادات الطباعة) ومجموعة الخصائص. في Excel ، ورقة المخطط هي ورقة عمل تحتوي فقط على مخطط.

## حذف مخطط {#DeleteChart}

```go
func (f *File) DeleteChart(sheet, cell string) (err error)
```

يوفر DeleteChart وظيفة لحذف المخططات في جدول بيانات عن طريق اسم الخلية وورقة العمل المحددة.
