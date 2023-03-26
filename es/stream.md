# Escritura en streaming

`StreamWriter` definió el tipo de escritor de flujo.

```go
type StreamWriter struct {
    File    *File
    Sheet   string
    SheetID int
    // contiene campos filtrados o no exportados
}
```

`Cell` se puede utilizar directamente en `StreamWriter.SetRow` para especificar un estilo y un valor.

```go
type Cell struct {
    StyleID int
    Formula string
    Value   interface{}
}
```

`RowOpts` define las opciones para la fila establecida, se puede usar directamente en `StreamWriter.SetRow` para especificar el estilo y las propiedades de la fila.

```go
type RowOpts struct {
    Height       float64
    Hidden       bool
    StyleID      int
    OutlineLevel int
}
```

## Obtener escritor de flujo {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter devuelve la estructura del escritor de flujo por el nombre de la hoja de trabajo para generar una nueva hoja de trabajo con grandes cantidades de datos. Tenga en cuenta que después de establecer filas, debe llamar al método [`Flush`](stream.md#Flush) para finalizar el proceso de escritura de transmisión y asegurarse de que el orden de los números de línea sea ascendente, no utilice las funciones de modo normal y modo de secuencia mezcladas para escribir datos en las hojas de cálculo. Por ejemplo, configure los datos para la hoja de trabajo de tamaño `102400` filas x `50` columnas con números y estilo:

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

Establezca el valor de celda y la fórmula de celda para una hoja de trabajo con el escritor de flujo:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1},
    excelize.Cell{Value: 2},
    excelize.Cell{Formula: "SUM(A1,B1)"}})
```

Establezca el valor de celda y el estilo de las filas para una hoja de trabajo con el escritor de flujo:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}},
    excelize.RowOpts{StyleID: styleID, Height: 20, Hidden: false})
```

Establezca el valor de celda y el nivel de esquema de fila para una hoja de trabajo con escritor de flujo:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}}, excelize.RowOpts{OutlineLevel: 1})
```

## Escribir fila de hoja para transmitir {#SetRow}

```go
func (sw *StreamWriter) SetRow(cell string, values []interface{}, opts ...RowOpts) error
```

SetRow escribe una matriz en la fila de flujo mediante una coordenada inicial dada y un puntero al tipo de matriz `slice`. Tenga en cuenta que debe llamar al método [`Flush`](stream.md#Flush) para finalizar el proceso de escritura de transmisión.

## Agregar una tabla para transmitir {#AddTable}

```go
func (sw *StreamWriter) AddTable(table *Table) error
```

AddTable crea una tabla de Excel para StreamWriter utilizando el área de coordenadas y el formato establecidos.

Ejemplo 1, cree una tabla de `A1:D5`:

```go
err := sw.AddTable(&excelize.Table{Range: "A1:D5"})
```

Ejemplo 2, cree una tabla de `F2:H6` con el formato establecido:

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

Tenga en cuenta que la tabla debe tener al menos dos líneas, incluido el encabezado. Las celdas del encabezado deben contener cadenas y deben ser únicas. Actualmente, solo se permite una tabla para StreamWriter. [`AddTable`](stream.md#AddTable) se debe llamar después de que se escriban las filas pero antes de `Flush`. Consulte [`AddTable`](utils.md#AddTable) para obtener detalles sobre el formato de la tabla.

## Insertar salto de página para transmitir {#InsertPageBreak}

```go
func (sw *StreamWriter) InsertPageBreak(cell string) error
```

InsertPageBreak crea un salto de página para determinar dónde termina la página impresa y dónde comienza la siguiente según una referencia de celda dada, el contenido antes del salto de página se imprimirá en una página y después del salto de página en otra.

## Establecer paneles para transmitir {#SetPanes}

```go
func (sw *StreamWriter) SetPanes(panes *Panes) error
```

SetPanes proporciona una función para crear y eliminar paneles congelados y paneles divididos al brindar opciones de paneles para `StreamWriter`. Tenga en cuenta que debe llamar a la función `SetPanes` antes de la función [`SetRow`](stream.md#SetRow).

## Combinar celda para transmitir {#MergeCell}

```go
func (sw *StreamWriter) MergeCell(hCell, vCell string) error
```

MergeCell proporciona una función para fusionar celdas por un área de coordenadas determinada para StreamWriter. No cree una celda combinada que se superponga con otra celda combinada existente.

## Establecer el ancho de columna en la secuencia {#SetColWidth}

```go
func (sw *StreamWriter) SetColWidth(min, max int, width float64) error
```

SetColWidth proporciona una función para establecer el ancho de una sola columna o varias columnas para el `StreamWriter`. Tenga en cuenta que debe llamar a la función `SetColWidth` antes de la función [`SetRow`](stream.md#SetRow). Por ejemplo, establezca la columna de ancho `B:C` como `20`:

```go
err := sw.SetColWidth(2, 3, 20)
```

## Corriente de vaciado {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush finalizando el proceso de escritura en streaming.
