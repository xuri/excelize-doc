# 流式写入

StreamWriter 用于定义流式写入器的数据类型。

```go
type StreamWriter struct {
    File    *File
    Sheet   string
    SheetID int
    // 还包含其他已过滤或未导出的字段
}
```

## 获取流式写入器 {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter 通过给定的工作表名称返回流式写入器，用于生成包含大规模数据的工作表。请注意通过此方法按行向工作表写入数据后，必须调用 [`Flush`](stream.md#Flush) 函数来结束流式写入过程，并需要确所保写入的行号是递增的。例如，向工作表流式按行写入 `102400` 行 x `50` 列带有样式的数据：

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
if err := streamWriter.SetRow("A1", []interface{}{excelize.Cell{StyleID: styleID, Value: "Data"}}); err != nil {
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

## 按行流式写入工作表 {#SetRow}

```go
func (sw *StreamWriter) SetRow(axis string, slice interface{}) error
```

SetRow 通过给定的工作表名称、起始坐标和指向数组类型“切片”的指针将数据按行流式写入工作表中。请注意，在设置行之后，必须调用 [`Flush`](stream.md#Flush) 函数来结束流式写入过程，并需要确所保写入的行号是递增的。

## 结束流式写入 {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush 用于结束流式写入过程。
