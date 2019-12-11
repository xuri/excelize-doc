# ストリーミング書き込み

StreamWriter は、ストリームライターのタイプを定義しました。

```go
type StreamWriter struct {
    File      *File
    Sheet     string
    SheetID   int
    SheetData bytes.Buffer
    // フィルタされたフィールドまたはエクスポートされていないフィールドが含まれています
}
```

## ストリームライターを取得する {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter は、指定されたワークシート名でストリームライター構造体を返し、大量のデータを含む新しいワークシートを生成します。 行を設定した後、[`Flush`](stream.md#Flush) メソッドを呼び出してストリーミング書き込みプロセスを終了し、行番号の順序が昇順であることを確認する必要があることに注意してください。 たとえば、サイズが `102400` 行 x `50` 列のサイズのワークシートにデータを設定します:

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

## ストリームにシート行を書き込む {#SetRow}

```go
func (sw *StreamWriter) SetRow(axis string, slice interface{}) error
```

SetRowは、指定されたワークシート名、開始座標、および配列型 `slice`へのポインタによって配列をストリーム行に書き込みます。 スタイル付きのセル設定は現在サポートされておらず、行を設定した後、ストリーミング書き込みプロセスを終了するには [`Flush`](stream.md#Flush) メソッドを呼び出す必要があることに注意してください。 サポートされているデータ型を次に示します:

|サポートされているデータ型|
|---|
|int|
|string|

## エンディングストリーム {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

ストリーミング書き込みプロセスを終了します。
