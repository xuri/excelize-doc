# Streaming-Schreiben

`StreamWriter` hat den Typ des Stream-Writers definiert.

```go
type StreamWriter struct {
    File    *File
    Sheet   string
    SheetID int
    // enthält gefilterte oder nicht exportierte Felder
}
```

`Cell` kann direkt in `StreamWriter.SetRow` verwendet werden, um einen Stil und einen Wert anzugeben.

```go
type Cell struct {
    StyleID int
    Formula string
    Value   interface{}
}
```

`RowOpts` definieren die Optionen für die eingestellte Zeile, sie kann direkt in `StreamWriter.SetRow` verwendet werden, um den Stil und die Eigenschaften der Zeile anzugeben.

```go
type RowOpts struct {
    Height       float64
    Hidden       bool
    StyleID      int
    OutlineLevel int
}
```

## Stream-Writer abrufen {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter gibt die Stream-Writer-Struktur anhand des angegebenen Arbeitsblattnamens zurück, um ein neues Arbeitsblatt mit großen Datenmengen zu generieren. Beachten Sie, dass Sie nach dem Festlegen von Zeilen die [`Flush`](stream.md#Flush) Methode aufrufen müssen, um den Streaming-Schreibvorgang zu beenden und sicherzustellen, dass die Reihenfolge der Zeilennummern aufsteigend ist. Verwenden Sie nicht die normalen Modusfunktionen und Streammodusfunktionen, die mit dem Schreiben von Daten auf die Arbeitsblätter gemischt sind. Legen Sie beispielsweise Daten für das Arbeitsblatt der Größe `102400` Zeilen x `50` Spalten mit Zahlen und Stil fest:

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

Festlegen des Zellenwerts und der Zellformel für ein Arbeitsblatt mit Stream Writer:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1},
    excelize.Cell{Value: 2},
    excelize.Cell{Formula: "SUM(A1,B1)"}})
```

Legen Sie den Zellenwert und den Zeilenstil für ein Arbeitsblatt mit Stream Writer fest:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}},
    excelize.RowOpts{StyleID: styleID, Height: 20, Hidden: false})
```

Legen Sie den Zellenwert und die Zeilengliederungsebene für ein Arbeitsblatt mit Stream Writer fest:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}}, excelize.RowOpts{OutlineLevel: 1})
```

## Schreiben der Zulaufzeile {#SetRow}

```go
func (sw *StreamWriter) SetRow(cell string, values []interface{}, opts ...RowOpts) error
```

SetRow schreibt ein Array in die Stream-Zeile, indem eine Startkoordinate und ein Zeiger auf den Array-Typ `slice` angegeben werden. Beachten Sie, dass Sie die Methode [`Flush`](stream.md#Flush) aufrufen müssen, um den Streaming-Schreibvorgang zu beenden.

## Fügen Sie eine Tabelle zum Streamen hinzu {#AddTable}

```go
func (sw *StreamWriter) AddTable(table *Table) error
```

AddTable erstellt eine Excel-Tabelle für den StreamWriter unter Verwendung des angegebenen Koordinatenbereichs und Formatsatzes.

Beispiel 1: Erstellen Sie eine Tabelle mit `A1:D5`:

```go
err := sw.AddTable(&excelize.Table{Range: "A1:D5"})
```

Beispiel 2: Erstellen Sie eine Tabelle mit `F2:H6` mit dem folgenden Format:

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

Beachten Sie, dass die Tabelle mindestens zwei Zeilen einschließlich der Kopfzeile enthalten muss. Die Header-Zellen müssen Zeichenfolgen enthalten und eindeutig sein. Derzeit ist nur eine Tabelle für einen StreamWriter zulässig. [`AddTable`](stream.md#AddTable) muss aufgerufen werden, nachdem die Zeilen geschrieben wurden, jedoch vor `Flush`. Weitere Informationen zum Tabellenformat finden Sie unter [`AddTable`](utils.md#AddTable).

## Seitenumbruch zum Streamen einfügen {#InsertPageBreak}

```go
func (sw *StreamWriter) InsertPageBreak(cell string) error
```

InsertPageBreak erstellt einen Seitenumbruch, um festzulegen, wo die gedruckte Seite endet und wo die nächste beginnt. Durch einen gegebenen Zellbezug wird der Inhalt vor dem Seitenumbruch auf eine Seite gedruckt und nach dem Seitenumbruch auf eine andere.

## Stellen Sie Fensterbereiche auf Stream ein {#SetPanes}

```go
func (sw *StreamWriter) SetPanes(panes *Panes) error
```

SetPanes bietet eine Funktion zum Erstellen und Entfernen von Einfrierfenstern und geteilten Fenstern, indem es Fensteroptionen für den `StreamWriter` gibt. Beachten Sie, dass Sie die Funktion `SetPanes` vor der Funktion [`SetRow`](stream.md#SetRow) aufrufen müssen.

## Zelle zum Streaming zusammenführen {#MergeCell}

```go
func (sw *StreamWriter) MergeCell(hCell, vCell string) error
```

MergeCell bietet eine Funktion zum Zusammenführen von Zellen nach einem bestimmten Koordinatenbereich für den StreamWriter. Erstellen Sie keine zusammengeführte Zelle, die sich mit einer anderen vorhandenen zusammengeführten Zelle überschneidet.

## Festlegen der Spaltenbreite für den Stream {#SetColWidth}

```go
func (sw *StreamWriter) SetColWidth(min, max int, width float64) error
```

SetColWidth bietet eine Funktion zum Festlegen der Breite einer einzelnen Spalte oder mehrerer Spalten für den `StreamWriter`. Beachten Sie, dass Sie die Funktion `SetColWidth` vor der Funktion [`SetRow`](stream.md#SetRow) aufrufen müssen. Legen Sie beispielsweise die Breitenspalte `B:C` als `20` fest:

```go
err := sw.SetColWidth(2, 3, 20)
```

## Flush-Stream {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush beendet den Streaming-Schreibvorgang.
