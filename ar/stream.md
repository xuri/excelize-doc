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
    Height       float64
    Hidden       bool
    StyleID      int
    OutlineLevel int
}
```

## الحصول على دفق الكاتب {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

تقوم NewStreamWriter بإرجاع بنية كاتب الدفق بواسطة اسم ورقة العمل المعطى المستخدم لكتابة البيانات على ورقة عمل فارغة جديدة مع كميات كبيرة من البيانات. لاحظ أنه بعد كتابة البيانات باستخدام كاتب الدفق لورقة العمل ، يجب عليك استدعاء طريقة [`Flush`](stream.md#Flush) لإنهاء عملية الكتابة المتدفقة ، والتأكد من أن ترتيب أرقام الصفوف تصاعدي عند تعيين الصفوف ، ووظائف الوضع العادي ووظائف وضع الدفق لا يمكن عمل مختلط لكتابة البيانات على أوراق العمل. سيحاول كاتب الدفق استخدام الملفات المؤقتة على القرص لتقليل استخدام الذاكرة عندما تقطع البيانات في الذاكرة أكثر من 16 ميغا بايت ، ولا يمكنك الحصول على قيمة الخلية في هذا الوقت. على سبيل المثال ، قم بتعيين البيانات لورقة عمل بحجم `102400` صفًا × `50` عمودًا بالأرقام والنمط:

```go
f := excelize.NewFile()
defer func() {
    if err := f.Close(); err != nil {
        fmt.Println(err)
    }
}()
sw, err := f.NewStreamWriter("Sheet1")
if err != nil {
    fmt.Println(err)
    return
}
styleID, err := f.NewStyle(&excelize.Style{Font: &excelize.Font{Color: "777777"}})
if err != nil {
    fmt.Println(err)
    return
}
if err := sw.SetRow("A1",
    []interface{}{
        excelize.Cell{StyleID: styleID, Value: "Data"},
        []excelize.RichTextRun{
            {Text: "Rich ", Font: &excelize.Font{Color: "2354e8"}},
            {Text: "Text", Font: &excelize.Font{Color: "e83723"}},
        },
    },
    excelize.RowOpts{Height: 45, Hidden: false}); err != nil {
    fmt.Println(err)
    return
}
for rowID := 2; rowID <= 102400; rowID++ {
    row := make([]interface{}, 50)
    for colID := 0; colID < 50; colID++ {
        row[colID] = rand.Intn(640000)
    }
    cell, err := excelize.CoordinatesToCellName(1, rowID)
    if err != nil {
        fmt.Println(err)
        break
    }
    if err := sw.SetRow(cell, row); err != nil {
        fmt.Println(err)
        break
    }
}
if err := sw.Flush(); err != nil {
    fmt.Println(err)
    return
}
if err := f.SaveAs("Book1.xlsx"); err != nil {
    fmt.Println(err)
}
```

تعيين قيمة الخلية وصيغة الخلية لورقة عمل باستخدام كاتب الدفق:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1},
    excelize.Cell{Value: 2},
    excelize.Cell{Formula: "SUM(A1,B1)"}})
```

تعيين قيمة الخلية ونمط الصفوف لورقة عمل باستخدام كاتب الدفق:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}},
    excelize.RowOpts{StyleID: styleID, Height: 20, Hidden: false})
```

قم بتعيين قيمة الخلية ورقم مستوى المخطط التفصيلي للصف لورقة عمل باستخدام كاتب الدفق:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}}, excelize.RowOpts{OutlineLevel: 1})
```

## كتابة صف ورقة إلى الدفق {#SetRow}

```go
func (sw *StreamWriter) SetRow(cell string, values []interface{}, opts ...RowOpts) error
```

يكتب SetRow مصفوفة لصف الدفق بإعطاء إحداثي بداية ومؤشر لنوع المصفوفة `slice`. لاحظ أنه يجب عليك استدعاء طريقة [`Flush`](stream.md#Flush) لإنهاء عملية الكتابة المتدفقة.

## إضافة جدول إلى تيار {#AddTable}

```go
func (sw *StreamWriter) AddTable(table *Table) error
```

يقوم AddTable بإنشاء جدول Excel لـ StreamWriter باستخدام منطقة الإحداثيات المحددة ومجموعة التنسيق.

مثال 1 ، أنشئ جدولاً من "A1: D5":

```go
err := sw.AddTable(&excelize.Table{Range: "A1:D5"})
```

مثال 2 ، أنشئ جدولاً من `F2:H6` مع ضبط التنسيق:

```go
disable := false
err := sw.AddTable(&excelize.Table{
    Range:             "F2:H6",
    Name:              "table",
    StyleName:         "TableStyleMedium2",
    ShowFirstColumn:   true,
    ShowLastColumn:    true,
    ShowRowStripes:    &disable,
    ShowColumnStripes: true,
})
```

لاحظ أن الجدول يجب أن يتكون من سطرين على الأقل بما في ذلك الرأس. يجب أن تحتوي خلايا الرأس على سلاسل ويجب أن تكون فريدة. حاليًا ، يُسمح بجدول واحد فقط لـ StreamWriter. يجب استدعاء [`AddTable`](stream.md#AddTable) بعد كتابة الصفوف ولكن قبل `Flush`. راجع [`AddTable`](utils.md#AddTable) للحصول على تفاصيل حول تنسيق الجدول.

## إدراج فاصل صفحة للدفق {#InsertPageBreak}

```go
func (sw *StreamWriter) InsertPageBreak(cell string) error
```

يُنشئ InsertPageBreak فاصل صفحة لتحديد مكان انتهاء الصفحة المطبوعة وأين يبدأ الفصل التالي بمرجع خلية معين ، وستتم طباعة المحتوى قبل فاصل الصفحة على صفحة واحدة وبعد فاصل الصفحة على أخرى.

## تعيين جزء النافذة للدفق {#SetPanes}

```go
func (sw *StreamWriter) SetPanes(panes *Panes) error
```

يوفر SetPanes وظيفة لإنشاء وإزالة ألواح التجميد وتقسيم الألواح عن طريق إعطاء خيارات الأجزاء لـ `StreamWriter`. لاحظ أنه يجب استدعاء الدالة `SetPanes` قبل الدالة [`SetRow`](stream.md#SetRow).

## دمج الخلية للدفق {#MergeCell}

```go
func (sw *StreamWriter) MergeCell(topLeftCell, bottomRightCell string) error
```

يوفر MergeCell وظيفة لدمج الخلايا بواسطة منطقة إحداثيات معينة لـ StreamWriter. لا تقم بإنشاء خلية مدمجة تتداخل مع خلية مدمجة أخرى موجودة.

## تعيين عرض العمود في الدفق {#SetColWidth}

```go
func (sw *StreamWriter) SetColWidth(min, max int, width float64) error
```

يوفر SetColWidth دالة لتعيين عرض عمود واحد أو أعمدة متعددة ل `StreamWriter`. لاحظ أنه يجب استدعاء الدالة `SetColWidth` قبل الدالة [`SetRow`](stream.md#SetRow). على سبيل المثال تعيين العمود عرض `B:C` ك `20`:

```go
err := sw.SetColWidth(2, 3, 20)
```

## تدفق الدفق {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush إنهاء عملية الكتابة المتدفقة.
