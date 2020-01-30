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

## Get stream writer {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter return stream writer struct by given worksheet name to generate a new worksheet with large amounts of data. Note that after set rows, you must call the [`Flush`](stream.md#Flush) method to end the streaming writing process and ensure that the order of line numbers is ascending. For example, set data for the worksheet of size `102400` rows x `50` columns with numbers and style:

```go
file := excelize.NewFile()
streamWriter, err := file.NewStreamWriter("Sheet1")
if err != nil {
    println(err.Error())
}
styleID, err := file.NewStyle(`{"font":{"color":"#777777"}}`)
if err != nil {
    println(err.Error())
}
if err := streamWriter.SetRow("A1", []interface{}{excelize.Cell{StyleID: styleID, Value: "Data"}}); err != nil {
    println(err.Error())
}
for rowID := 2; rowID <= 102400; rowID++ {
    row := make([]interface{}, 50)
    for colID := 0; colID < 50; colID++ {
        row[colID] = rand.Intn(640000)
    }
    cell, _ := excelize.CoordinatesToCellName(1, rowID)
    if err := streamWriter.SetRow(cell, row); err != nil {
        println(err.Error())
    }
}
if err := streamWriter.Flush(); err != nil {
    println(err.Error())
}
if err := file.SaveAs("Book1.xlsx"); err != nil {
    println(err.Error())
}
```

## Write sheet row to stream {#SetRow}

```go
func (sw *StreamWriter) SetRow(axis string, slice interface{}) error
```

SetRow writes an array to stream row by given worksheet name, starting coordinate and a pointer to array type `slice`. Note that, you must call the [`Flush`](stream.md#Flush) method to end the streaming writing process.

## Flush stream {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush ending the streaming writing process.
