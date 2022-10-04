# ストリーミング書き込み

`StreamWriter` は、ストリームライターのタイプを定義しました。

```go
type StreamWriter struct {
    File    *File
    Sheet   string
    SheetID int
    // フィルタされたフィールドまたはエクスポートされていないフィールドが含まれています
}
```

`Cell` は `StreamWriter.SetRow` で直接使用して、スタイルと値を指定できます。

```go
type Cell struct {
    StyleID int
    Formula string
    Value   interface{}
}
```

`RowOpts` は、設定された行のオプションを定義します。`StreamWriter.SetRow` で直接使用して、行のスタイルとプロパティを指定できます。

```go
type RowOpts struct {
    Height  float64
    Hidden  bool
    StyleID int
}
```

## ストリームライターを取得する {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter は、指定されたワークシート名でストリームライター構造体を返し、大量のデータを含む新しいワークシートを生成します。行を設定した後、[`Flush`](stream.md#Flush) メソッドを呼び出してストリーミング書き込みプロセスを終了し、行番号の順序が昇順であることを確認する必要があることに注意してください、通常モード関数とストリーム モード関数を混在させてワークシートにデータを書き込むことは使用しないでください。たとえば、サイズが `102400` 行 x `50` 列のサイズのワークシートにデータを設定します:

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

ストリームライターを使用してワークシートのセル値とセル数式を設定します:

```go
err := streamWriter.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1},
    excelize.Cell{Value: 2},
    excelize.Cell{Formula: "SUM(A1,B1)"}});
```

ストリームライターを使用してワークシートのセル値と行スタイルを設定します:

```go
err := streamWriter.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}},
    excelize.RowOpts{StyleID: styleID, Height: 20, Hidden: false});
```

## ストリームにシート行を書き込む {#SetRow}

```go
func (sw *StreamWriter) SetRow(cell string, values []interface{}, opts ...RowOpts) error
```

SetRow は、指定された開始座標と配列型 `slice` へのポインターを使用して、ワークシートに行ごとにデータをストリーミングします。行を設定した後、[`Flush`](stream.md#Flush) 関数を呼び出してストリーミング書き込みプロセスを終了し、書き込みが保証されている行番号がインクリメントされている必要があります。

## ストリーミングするテーブルを追加する {#AddTable}

```go
func (sw *StreamWriter) AddTable(hCell, vCell, opts string) error
```

指定したセル座標範囲と条件付き書式に基づいてテーブルをストリーミングします。

例 1 では、`A1:D5` 領域でテーブルをストリーミングして作成します:

```go
err := streamWriter.AddTable("A1", "D5", "")
```

例 2 では、ワークシート `F2:H6` 領域に条件付き書式のテーブルを作成します:

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

表の座標領域は、文字型のヘッダー行とコンテンツ行の少なくとも 2 行をカバーする必要があります。各列ヘッダー行の文字は一意であり、現在、各ワークシートで 1 つのテーブルのみのストリーミングがサポートされ、関数を呼び出す前に [`SetRow`](stream.md#SetRow) を使用してテーブルのヘッダー行データをストリーミングする必要があります。サポートされている表スタイルは、非フロー作成表 [`AddTable`](utils.md#AddTable) と同じです。

## ストリームでマージセル {#MergeCell}

```go
func (sw *StreamWriter) MergeCell(hCell, vCell string) error
```

指定されたセル座標範囲を使用してセルをストリーミングすると、現在、重なり合うセル以外のセルの結合のみがサポートされます。

## ストリームの列幅を設定する {#SetColWidth}

```go
func (sw *StreamWriter) SetColWidth(min, max int, width float64) error
```

SetColWidth は、`StreamWriter` の単一の列または複数の列の幅を設定する関数を提供します。[`SetRow`](stream.md#SetRow) 関数の前に `SetColWidth` 関数を呼び出す必要があることに注意してください。たとえば、幅列 `B:C` を `20` に設定します。

```go
err := streamWriter.SetColWidth(2, 3, 20)
```

## エンディングストリーム {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

ストリーミング書き込みプロセスを終了します。
