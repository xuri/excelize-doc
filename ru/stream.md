# Потоковое создать файл

StreamWriter определил тип создателя потока.

```go
type StreamWriter struct {
    File      *File
    Sheet     string
    SheetID   int
    SheetData bytes.Buffer
    // содержит отфильтрованные или неэкспортированные поля
}
```

## Получить потокового писателя {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter возвращает структуру записи потока по заданному имени рабочего листа для создания нового рабочего листа с большими объемами данных. Обратите внимание, что после установки строк необходимо вызвать метод [`Flush`](stream.md#Flush), чтобы завершить процесс потоковой записи и убедиться, что порядок номеров строк возрастает. Например, задайте данные для рабочего листа размером `102400` строк x` 50` столбцов с номерами:

```go
file := excelize.NewFile()
streamWriter, err := file.NewStreamWriter("Sheet1")
if err != nil {
    panic(err)
}
for rowID := 1; rowID <= 102400; rowID++ {
    row := make([]interface{}, 50)
    for colID := 0; colID < 50; colID++ {
        row[colID] = rand.Intn(640000)
    }
    cell, _ := excelize.CoordinatesToCellName(1, rowID)
    if err := streamWriter.SetRow(cell, &row); err != nil {
        panic(err)
    }
}
if err := streamWriter.Flush(); err != nil {
    panic(err)
}
if err := file.SaveAs("Book1.xlsx"); err != nil {
    panic(err)
}
```

## Запись строки листа в поток {#SetRow}

```go
func (sw *StreamWriter) SetRow(axis string, slice interface{}) error
```

SetRow записывает массив в строку потока по заданному имени рабочего листа, начальной координате и указателю на тип массива `slice`. Обратите внимание, что настройки ячеек со стилями в настоящее время не поддерживаются, и после установки строк необходимо вызвать метод [`Flush`](stream.md#Flush), чтобы завершить процесс потоковой записи. Ниже показаны поддерживаемые типы данных:

|Поддерживаемые типы данных|
|---|
|int|
|string|

## Flush поток {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush завершает процесс потоковой записи.
