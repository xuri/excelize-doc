# تدفق الكتابة

حدد `StreamWriter` نوع كاتب الدفق.

```go
type StreamWriter struct {
    File    *File
    Sheet   string
    SheetID int
    // يحتوي على حقول مصفاة أو غير مُصدرة
}
```

يمكن استخدام `Cell` مباشرةً في `StreamWriter.SetRow` لتحديد نمط وقيمة.

```go
type Cell struct {
    StyleID int
    Formula string
    Value   interface{}
}
```

تحدد `RowOpts` خيارات الصف المحدد ، ويمكن استخدامها مباشرة في `StreamWriter.SetRow` لتحديد نمط الصف وخصائصه.

```go
type RowOpts struct {
    Height  float64
    Hidden  bool
    StyleID int
}
```

## الحصول على دفق الكاتب {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

تقوم NewStreamWriter بإرجاع بنية كاتب الدفق حسب اسم ورقة العمل المحددة لإنشاء ورقة عمل جديدة تحتوي على كميات كبيرة من البيانات. لاحظ أنه بعد تعيين الصفوف ، يجب استدعاء طريقة [`Flush`](stream.md#Flush) لإنهاء عملية الكتابة المتدفقة والتأكد من أن ترتيب أرقام الأسطر تصاعديًا، لا تستخدم دالات الوضع العادي ووظائف وضع الدفق مختلطة لكتابة البيانات على أوراق العمل. على سبيل المثال ، قم بتعيين بيانات ورقة العمل بحجم `102400` من الصفوف × `50` من الأعمدة بالأرقام والنمط:

```go
file := excelize.NewFile()
streamWriter, err := file.NewStreamWriter("Sheet1")
if err != nil {
    fmt.Println(err)
}
styleID, err := file.NewStyle(&excelize.Style{Font: &excelize.Font{Color: "#777777"}})
if err != nil {
    fmt.Println(err)
}
if err := streamWriter.SetRow("A1",
    []interface{}{
        excelize.Cell{StyleID: styleID, Value: "Data"},
        []excelize.RichTextRun{
            {Text: "Rich ", Font: &excelize.Font{Color: "2354e8"}},
            {Text: "Text", Font: &excelize.Font{Color: "e83723"}},
        },
    },
    excelize.RowOpts{Height: 45, Hidden: false}); err != nil {
    fmt.Println(err)
}
for rowID := 2; rowID <= 102400; rowID++ {
    row := make([]interface{}, 50)
    for colID := 0; colID < 50; colID++ {
        row[colID] = rand.Intn(640000)
    }
    cell, _ := excelize.CoordinatesToCellName(1, rowID)
    if err := streamWriter.SetRow(cell, row); err != nil {
        fmt.Println(err)
    }
}
if err := streamWriter.Flush(); err != nil {
    fmt.Println(err)
}
if err := file.SaveAs("Book1.xlsx"); err != nil {
    fmt.Println(err)
}
```

تعيين قيمة الخلية وصيغة الخلية لورقة عمل باستخدام كاتب الدفق:

```go
err := streamWriter.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1},
    excelize.Cell{Value: 2},
    excelize.Cell{Formula: "SUM(A1,B1)"}});
```

تعيين قيمة الخلية ونمط الصفوف لورقة عمل باستخدام كاتب الدفق:

```go
err := streamWriter.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}},
    excelize.RowOpts{StyleID: styleID, Height: 20, Hidden: false});
```

## كتابة صف ورقة إلى الدفق {#SetRow}

```go
func (sw *StreamWriter) SetRow(cell string, values []interface{}, opts ...RowOpts) error
```

يكتب SetRow مصفوفة لصف الدفق بإعطاء إحداثي بداية ومؤشر لنوع المصفوفة `slice`. لاحظ أنه يجب عليك استدعاء طريقة [`Flush`](stream.md#Flush) لإنهاء عملية الكتابة المتدفقة.

## إضافة جدول إلى تيار {#AddTable}

```go
func (sw *StreamWriter) AddTable(hCell, vCell, opts string) error
```

يقوم AddTable بإنشاء جدول Excel لـ StreamWriter باستخدام منطقة الإحداثيات المحددة ومجموعة التنسيق.

مثال 1 ، أنشئ جدولاً من "A1: D5":

```go
err := streamWriter.AddTable("A1", "D5", "")
```

مثال 2 ، أنشئ جدولاً من `F2:H6` مع ضبط التنسيق:

```go
err := streamWriter.AddTable("F2", "H6", `{
    "table_name": "table",
    "table_style": "TableStyleMedium2",
    "show_first_column": true,
    "show_last_column": true,
    "show_row_stripes": false,
    "show_column_stripes": true
}`)
```

لاحظ أن الجدول يجب أن يتكون من سطرين على الأقل بما في ذلك الرأس. يجب أن تحتوي خلايا الرأس على سلاسل ويجب أن تكون فريدة. حاليًا ، يُسمح بجدول واحد فقط لـ StreamWriter. يجب استدعاء [`AddTable`](stream.md#AddTable) بعد كتابة الصفوف ولكن قبل `Flush`. راجع [`AddTable`](utils.md#AddTable) للحصول على تفاصيل حول تنسيق الجدول.

## دمج الخلية للدفق {#MergeCell}

```go
func (sw *StreamWriter) MergeCell(hCell, vCell string) error
```

يوفر MergeCell وظيفة لدمج الخلايا بواسطة منطقة إحداثيات معينة لـ StreamWriter. لا تقم بإنشاء خلية مدمجة تتداخل مع خلية مدمجة أخرى موجودة.

## تعيين عرض العمود في الدفق {#SetColWidth}

```go
func (sw *StreamWriter) SetColWidth(min, max int, width float64) error
```

يوفر SetColWidth دالة لتعيين عرض عمود واحد أو أعمدة متعددة ل `StreamWriter`. لاحظ أنه يجب استدعاء الدالة `SetColWidth` قبل الدالة [`SetRow`](stream.md#SetRow). على سبيل المثال تعيين العمود عرض `B:C` ك `20`:

```go
err := streamWriter.SetColWidth(2, 3, 20)
```

## تدفق الدفق {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush إنهاء عملية الكتابة المتدفقة.
