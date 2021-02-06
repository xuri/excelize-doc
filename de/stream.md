# Streaming-Schreiben

StreamWriter hat den Typ des Stream-Writers definiert.

```go
type StreamWriter struct {
    File    *File
    Sheet   string
    SheetID int
    // enthält gefilterte oder nicht exportierte Felder
}
```

## Stream-Writer abrufen {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter gibt die Stream-Writer-Struktur anhand des angegebenen Arbeitsblattnamens zurück, um ein neues Arbeitsblatt mit großen Datenmengen zu generieren. Beachten Sie, dass Sie nach dem Festlegen von Zeilen die [`Flush`](stream.md#Flush) Methode aufrufen müssen, um den Streaming-Schreibvorgang zu beenden und sicherzustellen, dass die Reihenfolge der Zeilennummern aufsteigend ist. Die allgemeine API und die Stream-API können nicht gemischt werden, um Daten in die Arbeitsblätter zu schreiben. Legen Sie beispielsweise Daten für das Arbeitsblatt der Größe `102400` Zeilen x `50` Spalten mit Zahlen und Stil fest:

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

## Schreiben der Zulaufzeile {#SetRow}

```go
func (sw *StreamWriter) SetRow(axis string, slice interface{}) error
```

SetRow schreibt ein Array in die Stream-Zeile mit dem angegebenen Arbeitsblattnamen, der Startkoordinate und einem Zeiger auf den Array-Typ `slice`. Beachten Sie, dass Sie die [`Flush`](stream.md#Flush) Methode aufrufen müssen, um den Streaming-Schreibvorgang zu beenden.

## Flush-Stream {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush beendet den Streaming-Schreibvorgang.
