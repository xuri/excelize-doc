# Escritura en streaming

StreamWriter definió el tipo de escritor de flujo.

```go
type StreamWriter struct {
    File    *File
    Sheet   string
    SheetID int
    // contiene campos filtrados o no exportados
}
```

Cell se puede utilizar directamente en StreamWriter.SetRow para especificar un estilo y un valor.

```go
type Cell struct {
    StyleID int
    Formula string
    Value   interface{}
}
```

RowOpts define las opciones para la fila establecida, se puede usar directamente en StreamWriter.SetRow para especificar el estilo y las propiedades de la fila.

```go
type RowOpts struct {
    Height  float64
    Hidden  bool
    StyleID int
}
```

## Obtener escritor de flujo {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter devuelve la estructura del escritor de flujo por el nombre de la hoja de trabajo para generar una nueva hoja de trabajo con grandes cantidades de datos. Tenga en cuenta que después de establecer filas, debe llamar al método [`Flush`](stream.md#Flush) para finalizar el proceso de escritura de transmisión y asegurarse de que el orden de los números de línea sea ascendente, la API común y la API de flujo no se pueden combinar para escribir datos en las hojas de trabajo. Por ejemplo, configure los datos para la hoja de trabajo de tamaño `102400` filas x `50` columnas con números y estilo:

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

Establezca el valor de celda y la fórmula de celda para una hoja de trabajo con el escritor de flujo:

```go
err := streamWriter.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1},
    excelize.Cell{Value: 2},
    excelize.Cell{Formula: "SUM(A1,B1)"}});
```

Establezca el valor de celda y el estilo de las filas para una hoja de trabajo con el escritor de flujo:

```go
err := streamWriter.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}},
    excelize.RowOpts{StyleID: styleID, Height: 20, Hidden: false});
```

## Escribir fila de hoja para transmitir {#SetRow}

```go
func (sw *StreamWriter) SetRow(cell string, values []interface{}, opts ...RowOpts) error
```

SetRow escribe una matriz en la fila de flujo mediante una coordenada inicial dada y un puntero al tipo de matriz `slice`. Tenga en cuenta que debe llamar al método [`Flush`](stream.md#Flush) para finalizar el proceso de escritura de transmisión.

## Agregar una tabla para transmitir {#AddTable}

```go
func (sw *StreamWriter) AddTable(hCell, vCell, opts string) error
```

AddTable crea una tabla de Excel para StreamWriter utilizando el área de coordenadas y el formato establecidos.

Ejemplo 1, cree una tabla de `A1:D5`:

```go
err := streamWriter.AddTable("A1", "D5", "")
```

Ejemplo 2, cree una tabla de `F2:H6` con el formato establecido:

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

Tenga en cuenta que la tabla debe tener al menos dos líneas, incluido el encabezado. Las celdas del encabezado deben contener cadenas y deben ser únicas. Actualmente, solo se permite una tabla para StreamWriter. [`AddTable`](stream.md#AddTable) se debe llamar después de que se escriban las filas pero antes de `Flush`. Consulte [`AddTable`](utils.md#AddTable) para obtener detalles sobre el formato de la tabla.

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
err := streamWriter.SetColWidth(2, 3, 20)
```

## Corriente de vaciado {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush finalizando el proceso de escritura en streaming.
