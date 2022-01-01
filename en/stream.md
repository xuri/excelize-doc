# Streaming write

StreamWriter defined the type of stream writer.

```go
type StreamWriter struct {
    File    *File
    Sheet   string
    SheetID int
    // contains filtered or unexported fields
}
```

Cell can be used directly in StreamWriter.SetRow to specify a style and a value.

```go
type Cell struct {
    StyleID int
    Formula string
    Value   interface{}
}
```

RowOpts define the options for the set row, it can be used directly in StreamWriter.SetRow to specify the style and properties of the row.

```go
type RowOpts struct {
    Height  float64
    Hidden  bool
    StyleID int
}
```

## Get stream writer {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter return stream writer struct by given worksheet name to generate a new worksheet with large amounts of data. Note that after set rows, you must call the [`Flush`](stream.md#Flush) method to end the streaming writing process and ensure that the order of line numbers is ascending, the common API and stream API can't be work mixed to writing data on the worksheets. For example, set data for the worksheet of size `102400` rows x `50` columns with numbers and style:

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

Set cell value and cell formula for a worksheet with stream writer:

```go
err := streamWriter.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1},
    excelize.Cell{Value: 2},
    excelize.Cell{Formula: "SUM(A1,B1)"}});
```

Set cell value and rows style for a worksheet with stream writer:

```go
err := streamWriter.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}},
    excelize.RowOpts{StyleID: styleID, Height: 20, Hidden: false});
```

## Write sheet row to stream {#SetRow}

```go
func (sw *StreamWriter) SetRow(axis string, slice interface{}) error
```

SetRow writes an array to stream row by given starting coordinate and a pointer to array type `slice`. Note that, you must call the [`Flush`](stream.md#Flush) method to end the streaming writing process.

## Add table to stream {#AddTable}

```go
func (sw *StreamWriter) AddTable(hcell, vcell, format string) error
```

AddTable creates an Excel table for the StreamWriter using the given coordinate area and format set.

Example 1, create a table of `A1:D5`:

```go
err := streamWriter.AddTable("A1", "D5", "")
```

Example 2, create a table of `F2:H6` with format set:

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

Note that the table must be at least two lines including the header. The header cells must contain strings and must be unique. Currently only one table is allowed for a StreamWriter. [`AddTable`](stream.md#AddTable) must be called after the rows are written but before `Flush`. See [`AddTable`](utils.md#AddTable) for details on the table format.

## Merge cell to stream {#MergeCell}

```go
func (sw *StreamWriter) MergeCell(hcell, vcell string) error
```

MergeCell provides a function to merge cells by a given coordinate area for the StreamWriter. Don't create a merged cell that overlaps with another existing merged cell.

## Set column width to stream {#SetColWidth}

```go
func (sw *StreamWriter) SetColWidth(min, max int, width float64) error
```

SetColWidth provides a function to set the width of a single column or multiple columns for the `StreamWriter`. Note that you must call the `SetColWidth` function before the [`SetRow`](stream.md#SetRow) function. For example set the width column `B:C` as `20`:

```go
err := streamWriter.SetColWidth(2, 3, 20)
```

## Flush stream {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush ending the streaming writing process.
