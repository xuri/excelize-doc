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

Cell 在 StreamWriter.SetRow 中使用，用于指定单元格的值、公式和样式。

```go
type Cell struct {
    StyleID int
    Formula string
    Value   interface{}
}
```

RowOpts 在 StreamWriter.SetRow 中使用，用于设置行样式。

```go
type RowOpts struct {
    Height  float64
    Hidden  bool
    StyleID int
}
```

## 获取流式写入器 {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter 通过给定的工作表名称返回流式写入器，用于生成包含大规模数据的工作表。请注意通过此方法按行向工作表写入数据后，必须调用 [`Flush`](stream.md#Flush) 函数来结束流式写入过程，并需要确所保写入的行号是递增的，普通 API 不能与流式 API 混合使用在工作表中写入数据。例如，向工作表流式按行写入 `102400` 行 x `50` 列带有样式的数据：

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

流式设置单元格的公式和值：

```go
err := streamWriter.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1},
    excelize.Cell{Value: 2},
    excelize.Cell{Formula: "SUM(A1,B1)"}});
```

流式设置单元格的值和行样式：

```go
err := streamWriter.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}},
    excelize.RowOpts{StyleID: styleID, Height: 20, Hidden: false});
```

## 按行流式写入工作表 {#SetRow}

```go
func (sw *StreamWriter) SetRow(axis string, slice interface{}) error
```

SetRow 通过给定的起始坐标和指向数组类型“切片”的指针将数据按行流式写入工作表中。请注意，在设置行之后，必须调用 [`Flush`](stream.md#Flush) 函数来结束流式写入过程，并需要确所保写入的行号是递增的。

## 流式创建表格 {#AddTable}

```go
func (sw *StreamWriter) AddTable(hCell, vCell, format string) error
```

根据给定的单元格坐标区域和条件格式流式创建表格。

例1，在 `A1:D5` 区域流式创建表格：

```go
err := streamWriter.AddTable("A1", "D5", "")
```

例2，在工作表 `F2:H6` 区域创建带有条件格式的表格：

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

注意，表格坐标区域至少需要包含两行：字符型的标题行和内容行。每列标题行的字符需保证是唯一的，当前仅支持在每个工作表中流式创建一张表格，并且必须在调用该函数前通过 [`SetRow`](stream.md#SetRow) 流式设置表格的标题行数据。支持的表格样式与非流式创建表格 [`AddTable`](utils.md#AddTable) 相同。

## 流式合并单元格 {#MergeCell}

```go
func (sw *StreamWriter) MergeCell(hCell, vCell string) error
```

通过给定的单元格坐标区域流式合并单元格，当前仅支持合并非交叠区域单元格。

## 流式设置列宽度 {#SetColWidth}

```go
func (sw *StreamWriter) SetColWidth(min, max int, width float64) error
```

根据给定的列范围和宽度值设置单个或多个列的宽度，必须在调用 [`SetRow`](stream.md#SetRow) 之前调用该函数设置列宽度。例如设置工作表上 `B` 到 `C` 列的宽度为 `20`：

```go
err := streamWriter.SetColWidth(2, 3, 20)
```

## 结束流式写入 {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush 用于结束流式写入过程。
