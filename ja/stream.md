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
    Height       float64
    Hidden       bool
    StyleID      int
    OutlineLevel int
}
```

## ストリームライターを取得する {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter は、大量のデータを含む新しい既存の空のワークシートにデータを書き込むために使用される、指定されたワークシート名によるストリーム ライター構造体を返します。 ストリーム ライターを使用してワークシートにデータを書き込んだ後、[`Flush`](stream.md#Flush) メソッドを呼び出してストリーミング書き込みプロセスを終了し、行を設定するときに行番号の順序が昇順であることを確認し、通常モード関数とストリーム モード関数を呼び出す必要があることに注意してください。 ワークシートへのデータの書き込みと作業を混在させることはできません。 ストリーム ライターは、メモリ内のデータが 16 MB を超えてチャンク化される場合、ディスク上の一時ファイルを使用してメモリ使用量を削減しようとしますが、現時点ではセル値を取得できません。 たとえば、サイズ `102400` 行 x `50` 列のワークシートに数値とスタイルを使用してデータを設定します。

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

ストリームライターを使用してワークシートのセル値とセル数式を設定します:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1},
    excelize.Cell{Value: 2},
    excelize.Cell{Formula: "SUM(A1,B1)"}})
```

ストリームライターを使用してワークシートのセル値と行スタイルを設定します:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}},
    excelize.RowOpts{StyleID: styleID, Height: 20, Hidden: false})
```

ストリーム ライターを使用して、ワークシートのセル値と行のアウトライン レベルを設定します:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}}, excelize.RowOpts{OutlineLevel: 1})
```

## ストリームにシート行を書き込む {#SetRow}

```go
func (sw *StreamWriter) SetRow(cell string, values []interface{}, opts ...RowOpts) error
```

SetRow は、指定された開始座標と配列型 `slice` へのポインターを使用して、ワークシートに行ごとにデータをストリーミングします。行を設定した後、[`Flush`](stream.md#Flush) 関数を呼び出してストリーミング書き込みプロセスを終了し、書き込みが保証されている行番号がインクリメントされている必要があります。

## ストリーミングするテーブルを追加する {#AddTable}

```go
func (sw *StreamWriter) AddTable(table *Table) error
```

指定したセル座標範囲と条件付き書式に基づいてテーブルをストリーミングします。

例 1 では、`A1:D5` 領域でテーブルをストリーミングして作成します:

```go
err := sw.AddTable(&excelize.Table{Range: "A1:D5"})
```

例 2 では、ワークシート `F2:H6` 領域に条件付き書式のテーブルを作成します:

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

表の座標領域は、文字型のヘッダー行とコンテンツ行の少なくとも 2 行をカバーする必要があります。各列ヘッダー行の文字は一意であり、現在、各ワークシートで 1 つのテーブルのみのストリーミングがサポートされ、関数を呼び出す前に [`SetRow`](stream.md#SetRow) を使用してテーブルのヘッダー行データをストリーミングする必要があります。サポートされている表スタイルは、非フロー作成表 [`AddTable`](utils.md#AddTable) と同じです。

## ストリームに改ページを挿入 {#InsertPageBreak}

```go
func (sw *StreamWriter) InsertPageBreak(cell string) error
```

InsertPageBreak は、特定のセル参照によって、印刷されるページが終了する場所と次のページが開始される場所を決定するために改ページを作成します。改ページの前のコンテンツは 1 つのページに印刷され、改ページの後のコンテンツは別のページに印刷されます。

## ストリームによるペインの設定 {#SetPanes}

```go
func (sw *StreamWriter) SetPanes(panes *Panes) error
```

SetPanes は、`StreamWriter` にペイン オプションを与えることで、フリーズ ペインと分割ペインを作成および削除する機能を提供します。[`SetRow`](stream.md#SetRow) 関数の前に `SetPanes` 関数を呼び出さなければならないことに注意してください。

## ストリームでマージセル {#MergeCell}

```go
func (sw *StreamWriter) MergeCell(topLeftCell, bottomRightCell string) error
```

指定されたセル座標範囲を使用してセルをストリーミングすると、現在、重なり合うセル以外のセルの結合のみがサポートされます。

## ストリームの列幅を設定する {#SetColWidth}

```go
func (sw *StreamWriter) SetColWidth(min, max int, width float64) error
```

SetColWidth は、`StreamWriter` の単一の列または複数の列の幅を設定する関数を提供します。[`SetRow`](stream.md#SetRow) 関数の前に `SetColWidth` 関数を呼び出す必要があることに注意してください。たとえば、幅列 `B:C` を `20` に設定します。

```go
err := sw.SetColWidth(2, 3, 20)
```

## エンディングストリーム {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

ストリーミング書き込みプロセスを終了します。
