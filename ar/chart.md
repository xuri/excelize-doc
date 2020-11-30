# الرسم البياني

## أضف الرسم البياني {#AddChart}

```go
func (f *File) AddChart(sheet, cell, format string, combo ...string) error
```

يوفر AddChart طريقة لإضافة مخطط في ورقة عمل من خلال مجموعة تنسيق مخطط معين (مثل الإزاحة والقياس وإعدادات نسبة العرض إلى الارتفاع وإعدادات الطباعة) ومجموعة الخصائص.

يوضح ما يلي `type` الرسم البياني الذي يدعمه برنامج excelize:

اكتب|الرسم البياني
---|---
area                        | مخطط منطقة 2D
areaStacked                 | مخطط منطقة مكدسة 2D
areaPercentStacked          | مخطط منطقة مكدس 2D 100%
area3D                      | مخطط منطقة ثلاثي الأبعاد
area3DStacked               | مخطط منطقة مكدس ثلاثي الأبعاد
area3DPercentStacked        | مخطط المساحة مكدسة 3D 100%
bar                         | مخطط شريطي مقسم إلى 2D
barStacked                  | مخطط شريطي مكدس 2D
barPercentStacked           | مخطط شريطي مكدس 2D 100%
bar3DClustered              | مخطط شريطي ثلاثي الأبعاد مُكتلّّد
bar3DStacked                | مخطط شريطي مكدس ثلاثي الأبعاد
bar3DPercentStacked         | مخطط شريطي مكدس 3D 100%
bar3DConeClustered          | مخطط شريطي مخروطي ثلاثي الأبعاد
bar3DConeStacked            | مخطط شريطي مكدس ثلاثي الأبعاد
bar3DConePercentStacked     | مخروط شريطية الرسم البياني 3D 100%
bar3DPyramidClustered       | مخطط شريطي هرمي ثلاثي الأبعاد
bar3DPyramidStacked         | مخطط شريطي مرصوف هرمي ثلاثي الأبعاد
bar3DPyramidPercentStacked  | هرم مخطط شريطي مكدس 3D 100%
bar3DCylinderClustered      | مخطط شريطي مُكدّد ثلاثي الأبعاد من الأسطوانات
bar3DCylinderStacked        | مخطط شريطي مكدس ثلاثي الأبعاد من الأسطوانات
bar3DCylinderPercentStacked | اسطوانات مخطط شريطي مكدس 3D 100%
col                         | مخطط عمودي مقسم إلى 2D
colStacked                  | مخطط عمودي مكدس 2D
colPercentStacked           | مخطط عمودي مكدس 2D 100%
col3DClustered              | مخطط عمودي مُكدَّد ثلاثي الأبعاد
col3D                       | مخطط عمودي ثلاثي الأبعاد
col3DStacked                | مخطط عمودي مكدس ثلاثي الأبعاد
col3DPercentStacked         | مخطط عمودي مكدس 3D 100%
col3DCone                   | مخطط عمودي مخروط ثلاثي الأبعاد
col3DConeClustered          | مخطط عمودي مخروطي ثلاثي الأبعاد
col3DConeStacked            | مخطط عمودي مكدس ثلاثي الأبعاد مخروطي
col3DConePercentStacked     | مخروط مخطط عمودي مكدس 3D 100%
col3DPyramid                | مخطط عمودي هرمي ثلاثي الأبعاد
col3DPyramidClustered       | مخطط عمودي مقسم هرمي ثلاثي الأبعاد
col3DPyramidStacked         | مخطط عمودي مرصوف هرمي ثلاثي الأبعاد
col3DPyramidPercentStacked  | هرم مخطط عمودي مكدس 3D 100%
col3DCylinder               | مخطط عمودي اسطوانات ثلاثية الأبعاد
col3DCylinderClustered      | مخطط عمودي مُكدّد من الاسطوانة ثلاثية الأبعاد
col3DCylinderStacked        | مخطط عمودي مكدس الأسطوانات ثلاثية الأبعاد
col3DCylinderPercentStacked | اسطوانات مخطط عمودي مكدس 3D 100%
doughnut                    | مخطط دائري مجوف
line                        | مخطط خطي
pie                         | مخطط دائري
pie3D                       | مخطط دائري ثلاثي الأبعاد
radar                       | مخططات رادارية
scatter                     | مخطط مبعثر
surface3D                   | مخطط سطحي ثلاثي الأبعاد
wireframeSurface3D          | مخطط سطحي 3D إطار سلكي
contour                     | مخطط محيط
wireframeContour            | مخطط محيط الإطار السلكي
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

تعيين خصائص وسيلة إيضاح الرسم البياني. الخيارات التي يمكن ضبطها هي:

معامل|اكتب|تفسير
---|---|---
position|string|موضع وسيلة إيضاح الرسم البياني
show_legend_key|bool|إظهار وسيلة الإيضاح ولكن لا تتداخل مع المخطط

عيّن `position` وسيلة إيضاح الرسم البياني. موضع وسيلة الإيضاح الافتراضي هو `right`. الوظائف المتاحة هي:

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
major_grid_lines|bool|`false`|يحدد خطوط الشبكة الرئيسية.
minor_grid_lines|bool|`false`|يحدد خطوط الشبكة الثانوية.
tick_label_skip|int|`1`|يحدد عدد علامات التجزئة المطلوب تخطيها بين التسمية المرسومة. خاصية `tick_label_skip` اختيارية. القيمة الافتراضية هي تلقائي.
reverse_order|bool|`false`|يحدد أن الفئات أو القيم بترتيب عكسي (اتجاه المخطط). خاصية `reverse_order` اختيارية.
maximum|int|`0`|يحدد أن الحد الأقصى الثابت ، 0 هو تلقائي. الخاصية القصوى اختيارية.
minimum|int|`0`|يحدد أن الحد الأدنى الثابت ، 0 هو تلقائي. الحد الأدنى من الممتلكات اختياري. القيمة الافتراضية هي تلقائي.

خصائص `y_axis` التي يمكن تعيينها هي:

معامل|اكتب|إفتراضي|تفسير
---|---|---|---
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

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    categories := map[string]string{
        "A2": "صغير", "A3": "عادي", "A4": "كبير", "B1": "تفاح", "C1": "برتقال", "D1": "كمثرى"}
    values := map[string]int{
        "B2": 2, "C2": 3, "D2": 3, "B3": 5, "C3": 2, "D3": 4, "B4": 6, "C4": 7, "D4": 8}
    f := excelize.NewFile()
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
            "position": "left",
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
    if err := f.SaveAs("Book1.xlsx"); err != nil {
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
