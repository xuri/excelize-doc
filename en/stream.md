# Streaming write

`StreamWriter` defined the type of stream writer.

```go
type StreamWriter struct {
    File    *File
    Sheet   string
    SheetID int
    // contains filtered or unexported fields
}
```

`Cell` can be used directly in `StreamWriter.SetRow` to specify a style and a value.

```go
type Cell struct {
    StyleID int
    Formula string
    Value   interface{}
}
```

`RowOpts` define the options for the set row, it can be used directly in `StreamWriter.SetRow` to specify the style and properties of the row.

```go
type RowOpts struct {
    Height       float64
    Hidden       bool
    StyleID      int
    OutlineLevel int
}
```

## Get stream writer {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter returns stream writer struct by given worksheet name used for writing data on a new existing empty worksheet with large amounts of data. Note that after writing data with the stream writer for the worksheet, you must call the [`Flush`](stream.md#Flush) method to end the streaming writing process, ensure that the order of row numbers is ascending when set rows, and the normal mode functions and stream mode functions can not be work mixed to writing data on the worksheets. The stream writer will try to use temporary files on disk to reduce the memory usage when in-memory chunks data over 16MB, and you can't get cell value at this time. For example, set data for worksheet of size `102400` rows x `50` columns with numbers and style:

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
            {Text: "Rich ", Font: &excelize.Font{Color: "2354E8"}},
            {Text: "Text", Font: &excelize.Font{Color: "E83723"}},
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

Set cell value and cell formula for a worksheet with stream writer:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1},
    excelize.Cell{Value: 2},
    excelize.Cell{Formula: "SUM(A1,B1)"}})
```

Set cell value and rows style for a worksheet with stream writer:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}},
    excelize.RowOpts{StyleID: styleID, Height: 20, Hidden: false})
```

Set cell value and row outline level for a worksheet with stream writer:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}}, excelize.RowOpts{OutlineLevel: 1})
```

## Write sheet row in stream {#SetRow}

```go
func (sw *StreamWriter) SetRow(cell string, values []interface{}, opts ...RowOpts) error
```

SetRow writes an array to stream rows by giving starting cell reference and a pointer to an array of values. Note that you must call the [`Flush`](stream.md#Flush) function to end the streaming writing process.

## Add table in stream {#AddTable}

```go
func (sw *StreamWriter) AddTable(table *Table) error
```

AddTable creates an Excel table for the `StreamWriter` using the given cell range and format set.

Example 1, create a table of `A1:D5`:

```go
err := sw.AddTable(&excelize.Table{Range: "A1:D5"})
```

Example 2, create a table of `F2:H6` with format set:

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

Note that the table must be at least two lines including the header. The header cells must contain strings and must be unique. Currently only one table is allowed for a `StreamWriter`. [`AddTable`](stream.md#AddTable) must be called after the rows are written but before `Flush`. See [`AddTable`](utils.md#AddTable) for details on the table format.

## Insert page break in stream {#InsertPageBreak}

```go
func (sw *StreamWriter) InsertPageBreak(cell string) error
```

InsertPageBreak creates a page break to determine where the printed page ends and where begins the next one by a given cell reference, the content before the page break will be printed on one page and after the page break on another.

## Set panes in stream {#SetPanes}

```go
func (sw *StreamWriter) SetPanes(panes *Panes) error
```

SetPanes provides a function to create and remove freeze panes and split panes by giving panes options for the `StreamWriter`. Note that you must call the `SetPanes` function before the [`SetRow`](stream.md#SetRow) function.

## Merge cell in stream {#MergeCell}

```go
func (sw *StreamWriter) MergeCell(topLeftCell, bottomRightCell string) error
```

MergeCell provides a function to merge cells by a given range reference for the `StreamWriter`. Don't create a merged cell that overlaps with another existing merged cell.

## Set column style in stream {#SetColStyle}

```go
func (sw *StreamWriter) SetColStyle(minVal, maxVal, styleID int) error
```

SetColStyle provides a function to set the style of a single column or multiple columns for the `StreamWriter`. Note that you must call the `SetColStyle` function before the [`SetRow`](stream.md#SetRow) function. For example set style of column `H`:

```go
err := sw.SetColStyle(8, 8, style)
```

## Set column width in stream {#SetColWidth}

```go
func (sw *StreamWriter) SetColWidth(min, max int, width float64) error
```

SetColWidth provides a function to set the width of a single column or multiple columns for the `StreamWriter`. Note that you must call the `SetColWidth` function before the [`SetRow`](stream.md#SetRow) function. For example set the width column `B:C` as `20`:

```go
err := sw.SetColWidth(2, 3, 20)
```

## Flush stream {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush ending the streaming writing process.
