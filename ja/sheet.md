# ワークシート

## 列の可視性設定 {#SetColVisible}

```go
func (f *File) SetColVisible(sheet, column string, visible bool)
```

与えられたワークシート名（大文字と小文字を区別）と列名に基づいて列の表示/非表示を設定します。例えば、`Sheet1` ワークシートの `D` 列を隠す：

```go
xlsx.SetColVisible("Sheet1", "D", false)
```

## 列幅の設定 {#SetColWidth}

```go
func (f *File) SetColWidth(sheet, startcol, endcol string, width float64)
```

指定されたシート名（大文字と小文字を区別）、列範囲、および幅の値に基づいて、単一または複数の列の幅を設定します。たとえば、`Sheet1` という名前の `A` から `H` の列の幅を `20` に設定します。

```go
xlsx := excelize.NewFile()
xlsx.SetColWidth("Sheet1", "A", "H", 20)
err := xlsx.Save()
if err != nil {
    fmt.Println(err)
}
```

## 行の高さを設定 {#SetRowHeight}

```go
func (f *File) SetRowHeight(sheet string, row int, height float64)
```

指定されたシート名（大文字と小文字を区別）、行番号、および高さの値に基づいて単一行の高さを設定します。たとえば、`Sheet1` という名前の最初の行の高さを `50` に設定します。

```go
xlsx.SetRowHeight("Sheet1", 1, 50)
```

## 行の表示設定 {#SetRowVisible}

```go
func (f *File) SetRowVisible(sheet string, rowIndex int, visible bool)
```

指定されたワークシート名（大文字と小文字を区別）と行番号に基づいて行の表示/非表示を設定します。たとえば、`Sheet1` という名前のワークシートの 2 行目を隠します。

```go
xlsx.SetRowVisible("Sheet1", 2, false)
```

## ワークシート名を取得する {#GetSheetName}

```go
func (f *File) GetSheetName(index int) string
```

指定されたワークシートインデックスに基づいてワークシート名を取得し、ワークシートが存在しない場合は空の文字を返します。

## 列の可視性を取得する {#GetColVisible}

```go
func (f *File) GetColVisible(sheet, column string) bool
```

指定されたワークシート名（大文字と小文字を区別）と列名に基づいて、ワークシート内の指定された列の可視性を取得します可視の戻り値は `true`、そうでない場合は `false` です。たとえば、`Sheet1` という名前のワークシートの `D` 列の可視性を取得します。

```go
xlsx.GetColVisible("Sheet1", "D")
```

## 列幅を取得 {#GetColWidth}

```go
func (f *File) GetColWidth(sheet, column string) float64
```

指定されたワークシートと列名に基づいて、ワークシート内の指定された列の幅を取得します。

## 行の高さを取得する {#GetRowHeight}

```go
func (f *File) GetRowHeight(sheet string, row int) float64
```

指定されたワークシート名（大文字と小文字を区別）と行番号に基づいて、ワークシート内の指定された行の高さを取得します。たとえば、`Sheet1` という名前のワークシートの最初の行の高さを取得します。

```go
xlsx.GetRowHeight("Sheet1", 1)
```

## 行の可視性を取得する {#GetRowVisible}

```go
func (f *File) GetRowVisible(sheet string, rowIndex int) bool
```

指定されたワークシート名（大文字と小文字を区別）と行番号に基づいて、ワークシート内の指定された行の可視性を取得します。たとえば、`Sheet1`という名前のワークシートの 2 行目の可視性を取得します。

```go
xlsx.GetRowVisible("Sheet1", 2)
```

## ワークシートインデックスを取得 {#GetSheetIndex}

```go
func (f *File) GetSheetIndex(name string) int
```

指定されたワークシート名に基づいてワークシートのインデックスを取得し（大文字と小文字を区別）、ワークシートが存在しない場合は `0` を返します。取得したインデックスは、ワークブックのデフォルトワークシートを設定するときに [`SetActiveSheet()`](workbook.md#SetActiveSheet) 関数を呼び出すためのパラメータとして使用できます。

## ワークシート一覧を取得する  {#GetSheetMap}

```go
func (f *File) GetSheetMap() map[int]string
```

名前とインデックスで構成されるブック内のすべてのワークシートのリストを取得します。

```go
xlsx, err := excelize.OpenFile("./Book1.xlsx")
if err != nil {
    return
}
for index, name := range xlsx.GetSheetMap() {
    fmt.Println(index, name)
}
```

## ワークシートのプロパティを取得する {#GetSheetPrOptions}

```go
func (f *File) GetSheetPrOptions(name string, opts ...SheetPrOptionPtr) error
```

与えられたワークシート名（大文字と小文字を区別）とフィルタリングに基づいてワークシートのプロパティを取得します。

|オプション属性|タイプ|
|---|---|
|CodeName|string|
|EnableFormatConditionsCalculation|bool|
|Published|bool|
|FitToPage|bool|
|AutoPageBreaks|bool|
|OutlineSummaryBelow|bool|

例えば、

```go
xl := excelize.NewFile()
const sheet = "Sheet1"

var (
    codeName                          excelize.CodeName
    enableFormatConditionsCalculation excelize.EnableFormatConditionsCalculation
    published                         excelize.Published
    fitToPage                         excelize.FitToPage
    autoPageBreaks                    excelize.AutoPageBreaks
    outlineSummaryBelow               excelize.OutlineSummaryBelow
)

if err := xl.GetSheetPrOptions(sheet,
    &codeName,
    &enableFormatConditionsCalculation,
    &published,
    &fitToPage,
    &autoPageBreaks,
    &outlineSummaryBelow,
); err != nil {
    panic(err)
}
fmt.Println("Defaults:")
fmt.Printf("- codeName: %q\n", codeName)
fmt.Println("- enableFormatConditionsCalculation:", enableFormatConditionsCalculation)
fmt.Println("- published:", published)
fmt.Println("- fitToPage:", fitToPage)
fmt.Println("- autoPageBreaks:", autoPageBreaks)
fmt.Println("- outlineSummaryBelow:", outlineSummaryBelow)
```

出力：

```text
Defaults:
- codeName: ""
- enableFormatConditionsCalculation: true
- published: true
- fitToPage: false
- autoPageBreaks: false
- outlineSummaryBelow: true
```

## 列を挿入 {#InsertCol}

```go
func (f *File) InsertCol(sheet, column string)
```

指定されたシート名（大文字と小文字を区別）と列名に基づいて、指定された列の前に空白の列を挿入します。例えば、`Sheet1` という名前のワークシートの `C` 列の前に空白の列を挿入します。

```go
xlsx.InsertCol("Sheet1", "C")
```

## 行挿入 {#InsertRow}

```go
func (f *File) InsertRow(sheet string, row int)
```

指定されたシート名（大文字と小文字を区別）と行インデックスに基づいて、指定された行の前に空白行を挿入します。例えば、`Sheet1` という名前のワークシートの 3 行目の前に空白行を挿入します。

```go
xlsx.InsertRow("Sheet1", 2)
```

## 重複行を追加 {#DuplicateRow}

```go
func (f *File) DuplicateRow(sheet string, row int)
```

指定されたワークシート名（大文字と小文字を区別）と行番号に基づいて、行の後に複製を追加します。たとえば、`Sheet1` という名前のワークシートの 2 行目を 3 行目にコピーします。

```go
xlsx.DuplicateRow("Sheet1", 2)
```

## 行を複製 {#DuplicateRowTo}

```go
func (f *File) DuplicateRowTo(sheet string, row, row2 int)
```

指定したシート名（大文字と小文字を区別）と行番号に基づいて、指定した行の後に行がコピーされます。たとえば、`Sheet1` という名前のワークシートの 2 行目を 7 行目にコピーします。

```go
xlsx.DuplicateRowTo("Sheet1", 2, 7)
```

## 行のアウトラインを作成する {#SetRowOutlineLevel}

```go
func (f *File) SetRowOutlineLevel(sheet string, rowIndex int, level uint8)
```

指定されたワークシート名（大文字と小文字を区別）、行インデックス、および評価パラメータに基づいてグループを作成します。たとえば、`Sheet1`という名前のワークシートの 2 行目にレベル 1 のグループを作成します。

<p align="center"><img width="612" src="./images/row_outline_level.png" alt="行のアウトラインを作成する"></p>

```go
xlsx.SetRowOutlineLevel("Sheet1", 2, 1)
```

## 列のアウトラインを作成する {#SetColOutlineLevel}

```go
func (f *File) SetColOutlineLevel(sheet, column string, level uint8)
```

指定されたワークシート名（大文字と小文字を区別）、列名、および評価パラメータに基づいてグループを作成します。たとえば、`Sheet` という名前のワークシートの `D` 列にレベル 2 のグループを作成します。

<p align="center"><img width="612" src="./images/col_outline_level.png" alt="列のアウトラインを作成する"></p>

```go
xlsx.SetColOutlineLevel("Sheet1", "D", 2)
```

## 行のアウトラインを取得する {#GetRowOutlineLevel}

```go
func (f *File) GetRowOutlineLevel(sheet string, rowIndex int) uint8
```

指定されたシート名（大文字と小文字を区別）と行インデックスに基づいてグループ化レベルを取得します。たとえば、`Sheet1` という名前のワークシートの行 2 のグループ化レベルを取得します。

```go
xlsx.GetRowOutlineLevel("Sheet1", 2)
```

## 列のアウトラインを取得 {#GetColOutlineLevel}

```go
func (f *File) GetColOutlineLevel(sheet, column string) uint8
```

指定されたシート名（大文字と小文字を区別）と列名に基づいてグループ化評価を取得します。たとえば、`Sheet1` という名前のワークシートの `D` 列のグループ化レベルを取得します。

```go
xlsx.GetColOutlineLevel("Sheet1", "D")
```

## 行イテレーター {#Rows}

```go
func (f *File) Rows(sheet string) (*Rows, error)
```

指定されたワークシート名に基づいてワークシートの行反復子を取得します（大文字と小文字を区別）。行反復子を使用してセルをトラバースする

```go
rows, err := xlsx.Rows("Sheet1")
for rows.Next() {
    for _, colCell := range rows.Columns() {
        fmt.Print(colCell, "\t")
    }
    fmt.Println()
}
```

### 行イテレーター - 単一行操作

```go
func (rows *Rows) Columns() []string
```

現在行のすべての列の値を返します。

### 行イテレーター - トラバーサル操作

```go
func (rows *Rows) Next() bool
```

次の行に値があれば、それは `true` を返します。

### 行イテレーター - 错误处理

```go
func (rows *Rows) Error() error
```

次の行でエラーを探すと `error` が返されます。

## 検索シート {#SearchSheet}

```go
func (f *File) SearchSheet(sheet, value string, reg ...bool) []string
```

指定されたワークシート名（大文字と小文字を区別）、セル値、または正規表現に基づいて座標を取得します。この関数は、文字列と数値の完全一致のみをサポートし、数式計算結果、書式設定された数値、および条件付き検索はサポートしません。 検索結果が結合セルの場合は、結合領域の左上隅の座標が返されます。

たとえば、`Sheet1` という名前のワークシートで値 `100` の座標を検索します。

```go
xlsx.SearchSheet("Sheet1", "100")
```

たとえば、`Sheet1` という名前のワークシートで `0-9` の範囲の座標を検索します。

```go
xlsx.SearchSheet("Sheet1", "[0-9]", true)
```

## シートを保護する {#ProtectSheet}

```go
func (f *File) ProtectSheet(sheet string, settings *FormatSheetProtection)
```

他のユーザーが誤ってまたは故意にワークシートのデータを変更、移動、または削除することを防止します。たとえば、`Sheet1` という名前のワークシートにパスワード保護を設定しますが、ロックされたセルの選択を許可し、ロックされていないセルを選択し、スキームを編集します。

<p align="center"><img width="933" src="./images/protect_sheet.png" alt="シートを保護する"></p>

```go
xlsx.ProtectSheet("Sheet1", &excelize.FormatSheetProtection{
    Password:      "password",
    EditScenarios: false,
})
```

## 無防備シート {#UnprotectSheet}

```go
func (f *File) UnprotectSheet(sheet string)
```

指定されたワークシート名に基づいてワークシートの保護を解除します（大文字と小文字を区別）。
