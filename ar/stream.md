# تدفق الكتابة

حدد StreamWriter نوع كاتب الدفق.

```go
type StreamWriter struct {
    File    *File
    Sheet   string
    SheetID int
    // يحتوي على حقول مصفاة أو غير مُصدرة
}
```

## الحصول على دفق الكاتب {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

تقوم NewStreamWriter بإرجاع بنية كاتب الدفق حسب اسم ورقة العمل المحددة لإنشاء ورقة عمل جديدة تحتوي على كميات كبيرة من البيانات. لاحظ أنه بعد تعيين الصفوف ، يجب استدعاء طريقة [`Flush`](stream.md#Flush) لإنهاء عملية الكتابة المتدفقة والتأكد من أن ترتيب أرقام الأسطر تصاعديًا. على سبيل المثال ، قم بتعيين بيانات ورقة العمل بحجم `102400` من الصفوف × `50` من الأعمدة بالأرقام والنمط:

```go
file := excelize.NewFile()
streamWriter, err := file.NewStreamWriter("Sheet1")
if err != nil {
    fmt.Println(err)
}
styleID, err := file.NewStyle(`{"font":{"color":"#777777"}}`)
if err != nil {
    fmt.Println(err)
}
if err := streamWriter.SetRow("A1", []interface{}{
    excelize.Cell{StyleID: styleID, Value: "Data"}}); err != nil {
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

## كتابة صف ورقة إلى الدفق {#SetRow}

```go
func (sw *StreamWriter) SetRow(axis string, slice interface{}) error
```

يكتب SetRow مصفوفة لدفق الصف حسب اسم ورقة العمل المحدد ، وبدء التنسيق ومؤشر لنوع المصفوفة `slice`. لاحظ أنه يجب عليك استدعاء طريقة [`Flush`](stream.md#Flush) لإنهاء عملية الكتابة المتدفقة.

## تدفق الدفق {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush إنهاء عملية الكتابة المتدفقة.
