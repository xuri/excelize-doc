# Потоковое создать файл

StreamWriter определил тип создателя потока.

```go
type StreamWriter struct {
    File    *File
    Sheet   string
    SheetID int
    // содержит отфильтрованные или неэкспортированные поля
}
```

Ячейку можно использовать непосредственно в StreamWriter.SetRow для указания стиля и значения.

```go
type Cell struct {
    StyleID int
    Formula string
    Value   interface{}
}
```

## Получить потокового писателя {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter возвращает структуру записи потока по заданному имени рабочего листа для создания нового рабочего листа с большими объемами данных. Обратите внимание, что после установки строк необходимо вызвать метод [`Flush`](stream.md#Flush), чтобы завершить процесс потоковой записи и убедиться, что порядок номеров строк возрастает, общий API и потоковый API нельзя смешивать для записи данных на рабочие листы. Например, задайте данные для рабочего листа размером `102400` строк x `50` столбцов с номерами:

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

Задайте значение ячейки и формулу ячейки для рабочего листа с помощью средства записи потока:

```go
err := streamWriter.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1},
    excelize.Cell{Value: 2},
    excelize.Cell{Formula: "SUM(A1,B1)"}});
```

## Запись строки листа в поток {#SetRow}

```go
func (sw *StreamWriter) SetRow(axis string, slice interface{}) error
```

SetRow записывает массив в строку потока по заданному имени рабочего листа, начальной координате и указателю на тип массива `slice`. Обратите внимание, что вы должны вызвать метод [`Flush`](stream.md#Flush), чтобы завершить процесс потоковой записи.

## Flush поток {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush завершает процесс потоковой записи.
