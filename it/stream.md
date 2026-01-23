# Scrittura in streaming

`StreamWriter` ha definito il tipo di scrittore di flussi.

```go
type StreamWriter struct {
    File    *File
    Sheet   string
    SheetID int
    // contiene campi filtrati o non esportati
}
```

`Cell` può essere utilizzato direttamente in `StreamWriter.SetRow` per specificare uno stile e un valore.

```go
type Cell struct {
    StyleID int
    Formula string
    Value   interface{}
}
```

`RowOpts` definisce le opzioni per la riga impostata, può essere utilizzato direttamente in `StreamWriter.SetRow` per specificare lo stile e le proprietà della riga.

```go
type RowOpts struct {
    Height       float64
    Hidden       bool
    StyleID      int
    OutlineLevel int
}
```

## Ottieni lo scrittore di flussi {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter restituisce la struttura dello scrittore di flusso in base al nome del foglio di lavoro specificato utilizzato per scrivere dati su un nuovo foglio di lavoro vuoto esistente con grandi quantità di dati. Tieni presente che dopo aver scritto i dati con lo stream writer per il foglio di lavoro, devi chiamare il metodo [`Flush`](stream.md#Flush) per terminare il processo di scrittura dello streaming, assicurarti che l'ordine dei numeri di riga sia crescente quando vengono impostate le righe e che le funzioni della modalità normale e della modalità stream non può essere un lavoro combinato con la scrittura dei dati sui fogli di lavoro. Lo stream writer proverà a utilizzare file temporanei sul disco per ridurre l'utilizzo della memoria quando i dati in memoria superano i 16 MB e al momento non è possibile ottenere il valore della cella. Ad esempio, imposta i dati per un foglio di lavoro di dimensioni `102400` righe x `50` colonne con numeri e stile:

```go
f := excelize.NewFile()
defer func() {
    if err := f.Close(); err != nil {
        fmt.Println(err)
    }
}()
sw, err := f.NewStreamWriter("Foglio1")
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
        excelize.Cell{StyleID: styleID, Value: "Dati"},
        []excelize.RichTextRun{
            {Text: "Ricco ", Font: &excelize.Font{Color: "2354E8"}},
            {Text: "Testo", Font: &excelize.Font{Color: "E83723"}},
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
if err := f.SaveAs("Cartel1.xlsx"); err != nil {
    fmt.Println(err)
}
```

Imposta il valore della cella e la formula della cella per un foglio di lavoro con lo stream writer:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1},
    excelize.Cell{Value: 2},
    excelize.Cell{Formula: "SUM(A1,B1)"}})
```

Imposta il valore della cella e lo stile delle righe per un foglio di lavoro con lo stream writer:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}},
    excelize.RowOpts{StyleID: styleID, Height: 20, Hidden: false})
```

Imposta il valore della cella e il livello della struttura della riga per un foglio di lavoro con lo stream writer:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}}, excelize.RowOpts{OutlineLevel: 1})
```

## Scrivi la riga del foglio nello streaming {#SetRow}

```go
func (sw *StreamWriter) SetRow(cell string, values []interface{}, opts ...RowOpts) error
```

SetRow scrive una matrice per lo streaming delle righe fornendo un riferimento alla cella iniziale e un puntatore a una matrice di valori. Tieni presente che devi chiamare la funzione [`Flush`](stream.md#Flush) per terminare il processo di scrittura dello streaming.

## Aggiungi tabella allo streaming {#AddTable}

```go
func (sw *StreamWriter) AddTable(table *Table) error
```

AddTable crea una tabella Excel per `StreamWriter` utilizzando l'intervallo di celle e il formato impostati.

Esempio 1, crea una tabella di `A1:D5`:

```go
err := sw.AddTable(&excelize.Table{Range: "A1:D5"})
```

Esempio 2, crea una tabella di `F2:H6` con il formato impostato:

```go
disable := false
err := sw.AddTable(&excelize.Table{
    Range:             "F2:H6",
    Name:              "tavolo",
    StyleName:         "TableStyleMedium2",
    ShowFirstColumn:   true,
    ShowLastColumn:    true,
    ShowRowStripes:    &disable,
    ShowColumnStripes: true,
})
```

Tieni presente che la tabella deve contenere almeno due righe inclusa l'intestazione. Le celle di intestazione devono contenere stringhe e devono essere univoche. Attualmente è consentita solo una tabella per `StreamWriter`. [`AddTable`](stream.md#AddTable) deve essere chiamato dopo che le righe sono state scritte ma prima di [`Flush`](stream.md#Flush). Vedi [`AddTable`](utils.md#AddTable) per i dettagli sul formato della tabella.

## Inserisci interruzione di pagina per lo streaming {#InsertPageBreak}

```go
func (sw *StreamWriter) InsertPageBreak(cell string) error
```

InsertPageBreak crea un'interruzione di pagina per determinare dove finisce la pagina stampata e dove inizia quella successiva in base a un determinato riferimento di cella, il contenuto prima dell'interruzione di pagina verrà stampato su una pagina e dopo l'interruzione di pagina su un'altra.

## Imposta i riquadri per lo streaming {#SetPanes}

```go
func (sw *StreamWriter) SetPanes(panes *Panes) error
```

SetPanes fornisce una funzione per creare e rimuovere riquadri bloccati e riquadri divisi fornendo opzioni di riquadri per `StreamWriter`. Tieni presente che devi chiamare la funzione [`SetRow`](stream.md#SetRow) prima della funzione `SetRow`.

## Unisci la cella allo streaming {#MergeCell}

```go
func (sw *StreamWriter) MergeCell(topLeftCell, bottomRightCell string) error
```

MergeCell fornisce una funzione per unire le celle in base a un determinato intervallo di riferimento per `StreamWriter`. Non creare una cella unita che si sovrappone a un'altra cella unita esistente.

## Imposta il contorno della colonna nel flusso {#SetColOutlineLevel}

```go
func (sw *StreamWriter) SetColOutlineLevel(col int, level uint8) error
```

SetColOutlineLevel fornisce una funzione per impostare il livello di struttura di una singola colonna per StreamWriter. Il valore del parametro `level` è compreso tra 1 e 7. Si noti che è necessario chiamare la funzione `SetColOutlineLevel` prima della funzione [`SetRow`](stream.md#SetRow). Ad esempio, impostare il livello di struttura della colonna `D` a 2:

```go
err := sw.SetColOutlineLevel(4, 2)
```

## Imposta lo stile della colonna su streaming {#SetColStyle}

```go
func (sw *StreamWriter) SetColStyle(minVal, maxVal, styleID int) error
```

SetColStyle fornisce una funzione per impostare lo stile di una singola colonna o di più colonne per `StreamWriter`. Nota che devi chiamare la funzione `SetColStyle` prima della funzione [`SetRow`](stream.md#SetRow). Ad esempio, imposta lo stile della colonna `H`:

```go
err := sw.SetColStyle(8, 8, style)
```

## Imposta la visibilità della colonna nel flusso {#SetColVisible}

```go
func (sw *StreamWriter) SetColVisible(minVal, maxVal int, visible bool) error
```

SetColVisible fornisce una funzione che imposta la visibilità di una singola colonna o di più colonne per `StreamWriter`. Si noti che è necessario chiamare la funzione `SetColVisible` prima della funzione [`SetRow`](stream.md#SetRow). Ad esempio, nascondere la colonna `D`:

```go
err := sw.SetColVisible(4, 4, false)
```

Nascondi le colonne da `D` a `F` (incluse):

```go
err := sw.SetColVisible(4, 6, false)
```

## Imposta la larghezza della colonna per lo streaming {#SetColWidth}

```go
func (sw *StreamWriter) SetColWidth(min, max int, width float64) error
```

SetColWidth fornisce una funzione per impostare la larghezza di una singola colonna o di più colonne per `StreamWriter`. Tieni presente che devi chiamare la funzione `SetColWidth` prima della funzione [`SetRow`](stream.md#SetRow). Ad esempio, imposta la larghezza della colonna `B:C` come `20`:

```go
err := sw.SetColWidth(2, 3, 20)
```

## Flusso a streaming {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush termina il processo di scrittura in streaming.
