# ワークシート

## 列の可視性設定 {#SetColVisible}

```go
func (f *File) SetColVisible(sheet, col string, visible bool) error
```

与えられたワークシート名と列名に基づいて列の表示/非表示を設定します。この関数は、同時実行セーフをサポートします。例えば、`Sheet1` ワークシートの `D` 列を隠す：

```go
err := f.SetColVisible("Sheet1", "D", false)
```

`D` から `F`（含まれる）の列を非表示にします：

```go
err := f.SetColVisible("Sheet1", "D:F", false)
```

## 列幅の設定 {#SetColWidth}

```go
func (f *File) SetColWidth(sheet, startCol, endCol string, width float64) error
```

指定されたシート名、列範囲、および幅の値に基づいて、単一または複数の列の幅を設定します。この関数は、同時実行セーフをサポートします。たとえば、`Sheet1` という名前の `A` から `H` の列の幅を `20` に設定します。

```go
f := excelize.NewFile()
err := f.SetColWidth("Sheet1", "A", "H", 20)
```

## 行の高さを設定 {#SetRowHeight}

```go
func (f *File) SetRowHeight(sheet string, row int, height float64) error
```

指定されたシート名、行番号、および高さの値に基づいて単一行の高さを設定します。たとえば、`Sheet1` という名前の最初の行の高さを `50` に設定します。

```go
err := f.SetRowHeight("Sheet1", 1, 50)
```

## 行の表示設定 {#SetRowVisible}

```go
func (f *File) SetRowVisible(sheet string, row int, visible bool) error
```

指定されたワークシート名と行番号に基づいて行の表示/非表示を設定します。たとえば、`Sheet1` という名前のワークシートの 2 行目を隠します。

```go
err := f.SetRowVisible("Sheet1", 2, false)
```

## ワークシート名を取得する {#GetSheetName}

```go
func (f *File) GetSheetName(index int) string
```

指定されたワークシートインデックスに基づいてワークシート名を取得し、ワークシートが存在しない場合は空の文字を返します。

## 列の可視性を取得する {#GetColVisible}

```go
func (f *File) GetColVisible(sheet, column string) (bool, error)
```

指定されたワークシート名と列名に基づいて、ワークシート内の指定された列の可視性を取得します可視の戻り値は `true`、そうでない場合は `false` です。この関数は、同時実行セーフをサポートします。たとえば、`Sheet1` という名前のワークシートの `D` 列の可視性を取得します。

```go
visible, err := f.GetColVisible("Sheet1", "D")
```

## 列幅を取得 {#GetColWidth}

```go
func (f *File) GetColWidth(sheet, col string) (float64, error)
```

指定されたワークシートと列名に基づいて、ワークシート内の指定された列の幅を取得します。この関数は、同時実行セーフをサポートします。

## 行の高さを取得する {#GetRowHeight}

```go
func (f *File) GetRowHeight(sheet string, row int) (float64, error)
```

指定されたワークシート名と行番号に基づいて、ワークシート内の指定された行の高さを取得します。たとえば、`Sheet1` という名前のワークシートの最初の行の高さを取得します。

```go
height, err := f.GetRowHeight("Sheet1", 1)
```

## 行の可視性を取得する {#GetRowVisible}

```go
func (f *File) GetRowVisible(sheet string, row int) (bool, error)
```

指定されたワークシート名と行番号に基づいて、ワークシート内の指定された行の可視性を取得します。たとえば、`Sheet1`という名前のワークシートの 2 行目の可視性を取得します。

```go
visible, err := f.GetRowVisible("Sheet1", 2)
```

## ワークシートインデックスを取得 {#GetSheetIndex}

```go
func (f *File) GetSheetIndex(sheet string) (int, error)
```

GetSheetIndex は、指定されたシート名でブックのシートインデックスを取得する関数を提供します。指定されたシート名が無効な場合、整数型の値 `-1` を返します。

取得したインデックスは、ワークブックのデフォルトワークシートを設定するときに [`SetActiveSheet()`](workbook.md#SetActiveSheet) 関数を呼び出すためのパラメータとして使用できます。

## ワークシートマップを取得する {#GetSheetMap}

```go
func (f *File) GetSheetMap() map[int]string
```

GetSheetMap は、ワークシート、チャートシート、ダイアログシート ID、およびワークブックの名前マップを取得する関数を提供します。例えば：

```go
f, err := excelize.OpenFile("Book1.xlsx")
if err != nil {
    return
}
defer func() {
    if err := f.Close(); err != nil {
        fmt.Println(err)
    }
}()
for index, name := range f.GetSheetMap() {
    fmt.Println(index, name)
}
```

## ワークシートリストを取得する {#GetSheetList}

```go
func (f *File) GetSheetList() []string
```

GetSheetList は、ワークシート、チャートシート、およびワークブックのダイアログシート名リストを取得する関数を提供します。

## ワークシート名を設定 {#SetSheetName}

```go
func (f *File) SetSheetName(source, target string) error
```

SetSheetName は、指定された古いワークシート名と新しいワークシート名でワークシート名を設定する関数を提供します。シートのタイトルには最大 31 文字を使用できます。この関数はシートの名前を変更するだけで、セルに関連付けられた数式または参照のシート名は更新しません。そのため、問題の数式エラーまたは参照が欠落している可能性があります。

## 列を挿入 {#InsertCols}

```go
func (f *File) InsertCols(sheet, col string, n int) error
```

InsertCols には、指定された列名と列数の前に新しい列を挿入する関数が用意されています。たとえば、`Sheet1` の列 `C` の前に 2 つの列を作成します。

```go
err := f.InsertCols("Sheet1", "C", 2)
```

## 行挿入 {#InsertRows}

```go
func (f *File) InsertRows(sheet string, row, n int) error
```

InsertRows は、指定された Excel の行番号の後に `1` から始まる行数と行数の後に新しい行を挿入する関数を提供します。たとえば、`Sheet1` の行 `3` の前に 2 つの行を作成します。

```go
err := f.InsertRows("Sheet1", 3, 2)
```

## 重複行を追加 {#DuplicateRow}

```go
func (f *File) DuplicateRow(sheet string, row int) error
```

指定されたワークシート名と行番号に基づいて、行の後に複製を追加します。たとえば、`Sheet1` という名前のワークシートの 2 行目を 3 行目にコピーします。

```go
err := f.DuplicateRow("Sheet1", 2)
```

このメソッドは注意して使用してください。式やグラフなどの参照の変更に影響します。ワークシートの参照値がある場合、それを開くとファイルエラーが発生します。現在、Excelize はこれらの参照を部分的にのみ更新します。

## 行を複製 {#DuplicateRowTo}

```go
func (f *File) DuplicateRowTo(sheet string, row, row2 int) error
```

指定したシート名と行番号に基づいて、指定した行の後に行がコピーされます。たとえば、`Sheet1` という名前のワークシートの 2 行目を 7 行目にコピーします。

```go
err := f.DuplicateRowTo("Sheet1", 2, 7)
```

このメソッドは注意して使用してください。式やグラフなどの参照の変更に影響します。ワークシートの参照値がある場合、それを開くとファイルエラーが発生します。現在、Excelize はこれらの参照を部分的にのみ更新します。

## 行のアウトラインを作成する {#SetRowOutlineLevel}

```go
func (f *File) SetRowOutlineLevel(sheet string, row int, level uint8) error
```

指定されたワークシート名、行インデックス、および評価パラメータに基づいてグループを作成します。たとえば、`Sheet1` という名前のワークシートの 2 行目にレベル 1 のグループを作成します。

<p align="center"><img width="612" src="./images/row_outline_level.png" alt="行のアウトラインを作成する"></p>

```go
err := f.SetRowOutlineLevel("Sheet1", 2, 1)
```

## 列のアウトラインを作成する {#SetColOutlineLevel}

```go
func (f *File) SetColOutlineLevel(sheet, col string, level uint8) error
```

指定されたワークシート名、列名、および評価パラメータに基づいてグループを作成します。たとえば、`Sheet` という名前のワークシートの `D` 列にレベル 2 のグループを作成します。

<p align="center"><img width="612" src="./images/col_outline_level.png" alt="列のアウトラインを作成する"></p>

```go
err := f.SetColOutlineLevel("Sheet1", "D", 2)
```

## 行のアウトラインを取得する {#GetRowOutlineLevel}

```go
func (f *File) GetRowOutlineLevel(sheet string, row int) (uint8, error)
```

指定されたシート名と行インデックスに基づいてグループ化レベルを取得します。たとえば、`Sheet1` という名前のワークシートの行 2 のグループ化レベルを取得します。

```go
err := f.GetRowOutlineLevel("Sheet1", 2)
```

## 列のアウトラインを取得 {#GetColOutlineLevel}

```go
func (f *File) GetColOutlineLevel(sheet, col string) (uint8, error)
```

指定されたシート名と列名に基づいてグループ化評価を取得します。たとえば、`Sheet1` という名前のワークシートの `D` 列のグループ化レベルを取得します。

```go
level, err := f.GetColOutlineLevel("Sheet1", "D")
```

## 列イテレータ {#Cols}

```go
func (f *File) Cols(sheet string) (*Cols, error)
```

Cols は列イテレータを返します。これは、大きなデータを含むワークシートのデータをストリーミングして読み取るために使用されます。この関数は、同時実行セーフをサポートします。例えば：

```go
cols, err := f.Cols("Sheet1")
if err != nil {
    fmt.Println(err)
    return
}
for cols.Next() {
    col, err := cols.Rows()
    if err != nil {
        fmt.Println(err)
    }
    for _, rowCell := range col {
        fmt.Print(rowCell, "\t")
    }
    fmt.Println()
}
```

### 列イテレータ - 列

```go
func (cols *Cols) Rows(opts ...Options) ([]string, error)
```

Rows は、現在の列の行の値を返します。

### 列イテレータ - トラバース

```go
func (cols *Cols) Next() bool
```

Next は、次の列が見つかった場合に `true` を返します。

### 列イテレータ - エラー処理

```go
func (cols *Cols) Error() error
```

エラーが発生すると、Error は `error` を返します。

## 行イテレータ {#Rows}

```go
func (f *File) Rows(sheet string) (*Rows, error)
```

Rows は行イテレータを返します。これは、大きなデータを含むワークシートのデータのストリーミングストリーミングに使用されます。この関数は、同時実行セーフをサポートします。例えば:

```go
rows, err := f.Rows("Sheet1")
if err != nil {
    fmt.Println(err)
    return
}
for rows.Next() {
    row, err := rows.Columns()
    if err != nil {
        fmt.Println(err)
    }
    for _, colCell := range row {
        fmt.Print(colCell, "\t")
    }
    fmt.Println()
}
if err = rows.Close(); err != nil {
    fmt.Println(err)
}
```

### 行イテレーター - 単一行操作

```go
func (rows *Rows) Columns(opts ...Options) ([]string, error)
```

Columns は、現在の行の列の値を返します。これにより、ワークシートデータがストリームとしてフェッチされ、行の各セルがそのまま返され、ワークシートの末尾の空の行がスキップされません。

### 行イテレーター - トラバーサル操作

```go
func (rows *Rows) Next() bool
```

次の行に値があれば、それは `true` を返します。

### 行イテレーター - 错误处理

```go
func (rows *Rows) Error() error
```

エラーが発生すると、Error は `error` を返します。

### 行イテレーター - 行オプションの取得

```go
func (rows *Rows) GetRowOpts() RowOpts
```

GetRowOpts は、現在の行の `RowOpts` を返します。

### 行イテレーター - 閉じる

```go
func (rows *Rows) Close() error
```

Close は、システム一時ディレクトリで開いているワークシート XML ファイルを閉じます。

## 検索シート {#SearchSheet}

```go
func (f *File) SearchSheet(sheet, value string, reg ...bool) ([]string, error)
```

指定されたワークシート名、セル値、または正規表現に基づいて座標を取得します。この関数は、文字列と数値の完全一致のみをサポートし、数式計算結果、書式設定された数値、および条件付き検索はサポートしません。検索結果が結合セルの場合は、結合領域の左上隅の座標が返されます。

たとえば、`Sheet1` という名前のワークシートで値 `100` の座標を検索します。

```go
result, err := f.SearchSheet("Sheet1", "100")
```

たとえば、`Sheet1` という名前のワークシートで `0-9` の範囲の座標を検索します。

```go
result, err := f.SearchSheet("Sheet1", "[0-9]", true)
```

## シートを保護する {#ProtectSheet}

```go
func (f *File) ProtectSheet(sheet string, opts *SheetProtectionOptions) error
```

ProtectSheet は、他のユーザーがワークシート内のデータを誤ってまたは故意に変更、移動、または削除するのを防ぐ機能を提供します。 オプションのフィールド `AlgorithmName` で指定されたハッシュアルゴリズムは、XOR、MD4、MD5、SHA-1、SHA-256、SHA-384、および SHA-512 をサポートし、ハッシュアルゴリズムが指定されていない場合、デフォルトで XOR アルゴリズムを使用します。 たとえば、保護設定で `Sheet1` を保護します:

<p align="center"><img width="933" src="./images/protect_sheet.png" alt="シートを保護する"></p>

```go
err := f.ProtectSheet("Sheet1", &excelize.SheetProtectionOptions{
    AlgorithmName:       "SHA-512",
    Password:            "password",
    SelectLockedCells:   true,
    SelectUnlockedCells: true,
    EditScenarios:       true,
})
```

SheetProtectionOptions は、ワークシート保護の設定を直接マップします。

```go
type SheetProtectionOptions struct {
    AlgorithmName       string
    AutoFilter          bool
    DeleteColumns       bool
    DeleteRows          bool
    EditObjects         bool
    EditScenarios       bool
    FormatCells         bool
    FormatColumns       bool
    FormatRows          bool
    InsertColumns       bool
    InsertHyperlinks    bool
    InsertRows          bool
    Password            string
    PivotTables         bool
    SelectLockedCells   bool
    SelectUnlockedCells bool
    Sort                bool
}
```

## 無防備シート {#UnprotectSheet}

```go
func (f *File) UnprotectSheet(sheet string, password ...string) error
```

UnprotectSheet は、シートの保護を削除する機能を提供し、パスワード検証でシート保護を削除するための 2 番目のオプションのパスワードパラメーターを指定しました。

## 列を削除 {#RemoveCol}

```go
func (f *File) RemoveCol(sheet, col string) error
```

RemoveColは、与えられたワークシート名と列インデックスによって単一の列を削除する機能を提供します。たとえば、`Sheet1`の `C` 列を削除します。

```go
err := f.RemoveCol("Sheet1", "C")
```

このメソッドは注意して使用してください。式やグラフなどの参照の変更に影響します。ワークシートの参照値がある場合、それを開くとファイルエラーが発生します。現在、Excelize はこれらの参照を部分的にのみ更新します。

## 行を削除 {#RemoveRow}

```go
func (f *File) RemoveRow(sheet string, row int) error
```

RemoveRow は、与えられたワークシート名とExcelの行番号で単一行を削除する機能を提供します。例えば、`Sheet1` の `3`行を削除する：

```go
err := f.RemoveRow("Sheet1", 3)
```

この方法は慎重に使用してください。式、グラフなどの参照の変更に影響します。ワークシートの参照値がある場合は、開くとファイルエラーが発生します。excelize は現在これらの参照を部分的にしか更新しません。

## 列の値を設定する {#SetSheetCol}

```go
func (f *File) SetSheetCol(sheet, cell string, slice interface{}) error
```

SetSheetCol は、指定されたワークシート名、開始座標、および配列型 `slice` へのポインターによって列に配列を書き込みます。たとえば、列 `B` に `Sheet1` のセル `B6` で始まる配列を書き込みます。

```go
err := f.SetSheetCol("Sheet1", "B6", &[]interface{}{"1", nil, 2})
```

## 行の値を設定 {#SetSheetRow}

```go
func (f *File) SetSheetRow(sheet, cell string, slice interface{}) error
```

SetSheetRow は与えられたワークシート名、開始座標、配列型 `slice` へのポインタで配列を行に書き込みます。この関数は、同時実行セーフをサポートします。例えば、 `Sheet1` の `B6`のセルから始まる行 `6` の配列を書き込みます。

```go
err := f.SetSheetRow("Sheet1", "B6", &[]interface{}{"1", nil, 2})
```

## 改ページを挿入 {#InsertPageBreak}

```go
func (f *File) InsertPageBreak(sheet, cell string) error
```

InsertPageBreak は、改ページを作成して、印刷されたページの終了位置と特定のワークシート名と軸による次のページの開始位置を決定します。

## 改ページを削除 {#RemovePageBreak}

```go
func (f *File) RemovePageBreak(sheet, cell string) error
```

RemovePageBreak は、指定されたワークシート名と軸による改ページを削除します。
