# Потоковое создать файл

`StreamWriter` определил тип создателя потока.

```go
type StreamWriter struct {
    File    *File
    Sheet   string
    SheetID int
    // содержит отфильтрованные или неэкспортированные поля
}
```

`Cell` можно использовать непосредственно в `StreamWriter.SetRow` для указания стиля и значения.

```go
type Cell struct {
    StyleID int
    Formula string
    Value   interface{}
}
```

`RowOpts` определяет параметры для установленной строки, его можно использовать непосредственно в `StreamWriter.SetRow` для указания стиля и свойств строки.

```go
type RowOpts struct {
    Height  float64
    Hidden  bool
    StyleID int
}
```

## Получить потокового писателя {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter возвращает структуру записи потока по заданному имени рабочего листа для создания нового рабочего листа с большими объемами данных. Обратите внимание, что после установки строк необходимо вызвать метод [`Flush`](stream.md#Flush), чтобы завершить процесс потоковой записи и убедиться, что порядок номеров строк возрастает, функции нормального режима и функции потокового режима не могут быть смешаны для записи данных на листах. Например, задайте данные для рабочего листа размером `102400` строк x `50` столбцов с номерами:

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

Задайте значение ячейки и формулу ячейки для рабочего листа с помощью средства записи потока:

```go
err := streamWriter.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1},
    excelize.Cell{Value: 2},
    excelize.Cell{Formula: "SUM(A1,B1)"}});
```

Задайте значение ячейки и стиль строк для рабочего листа с помощью средства записи потока:

```go
err := streamWriter.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}},
    excelize.RowOpts{StyleID: styleID, Height: 20, Hidden: false});
```

## Запись строки листа в поток {#SetRow}

```go
func (sw *StreamWriter) SetRow(cell string, values []interface{}, opts ...RowOpts) error
```

SetRow записывает массив в строку потока по заданной начальной координате и указателю на массив типа `slice`. Обратите внимание, что вы должны вызвать метод [`Flush`](stream.md#Flush), чтобы завершить процесс потоковой записи.

## Добавить таблицу в поток {#AddTable}

```go
func (sw *StreamWriter) AddTable(hCell, vCell, opts string) error
```

AddTable создает таблицу Excel для StreamWriter, используя заданную область координат и набор форматов.

Пример 1, создайте таблицу `A1:D5`:

```go
err := streamWriter.AddTable("A1", "D5", "")
```

Пример 2, создайте таблицу `F2:H6` с установленным форматом:

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

Обратите внимание, что таблица должна состоять как минимум из двух строк, включая заголовок. Ячейки заголовка должны содержать строки и быть уникальными. В настоящее время для StreamWriter разрешена только одна таблица. [`AddTable`](stream.md#AddTable) должен вызываться после записи строк, но до `Flush`. См. [`AddTable`](utils.md#AddTable) для получения подробной информации о формате таблицы.

## Объединить ячейку в поток {#MergeCell}

```go
func (sw *StreamWriter) MergeCell(hCell, vCell string) error
```

MergeCell предоставляет функцию объединения ячеек по заданной области координат для StreamWriter. Не создавайте объединенную ячейку, которая перекрывается с другой существующей объединенной ячейкой.

## Установите ширину столбца в потоке {#SetColWidth}

```go
func (sw *StreamWriter) SetColWidth(min, max int, width float64) error
```

SetColWidth предоставляет функцию для настройки ширины одной колонки или нескольких столбцов для `StreamWriter`. Обратите внимание, что вы должны позвонить функции `SetColWidth` перед функцией [`SetRow`](stream.md#SetRow). Например, установите столбец ширины `B:C` как `20`:

```go
err := streamWriter.SetColWidth(2, 3, 20)
```

## Flush поток {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush завершает процесс потоковой записи.
