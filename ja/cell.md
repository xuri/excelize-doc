# セル

RichTextRun は、リッチテキストランの設定を直接マップします。

```go
type RichTextRun struct {
    Font *Font
    Text string
}
```

HyperlinkOpts を [`SetCellHyperlink`](cell.md#SetCellHyperlink) に渡して、オプションのハイパーリンク属性（表示するテキストや画面のヒントテキストなど）を設定できます。

```go
type HyperlinkOpts struct {
    Display *string
    Tooltip *string
}
```

数式の種類を使用する [`SetCellFormula`](cell.md#SetCellFormula) に渡すことができます。

```go
type FormulaOpts struct {
    Type *string // フォーミュラ タイプ
    Ref  *string // 共有式参照
}
```

## セル値設定 {#SetCellValue}

```go
func (f *File) SetCellValue(sheet, axis string, value interface{}) error
```

指定されたワークシート名とセル座標に基づいて、セルの値を設定します。指定された座標は、テーブルの最初の行にあるべきではありません。

|サポートされているデータ型|
|---|
|int|
|int8|
|int16|
|int32|
|int64|
|uint|
|uint8|
|uint16|
|uint32|
|uint64|
|float32|
|float64|
|string|
|[]byte|
|time.Duration|
|time.Time|
|bool|
|nil|

デフォルトの日付形式は、`time.Time` タイプの値の `m/d/yy h:mm` であることに注意してください。[`SetCellStyle`](cell.md#SetCellStyle) メソッドで数値フォーマットを設定できます。1900 年 1 月 0 日や 1900 年 2 月 29 日などの Excel で特殊な日付を設定する必要がある場合、これらの時刻は Go 言語の `time.Time` データ型で表すことはできません。セルの値を数値 0 または 60 に設定してから、セルの日時数値形式スタイルを作成してバインドしてください。

## ブール値設定 {#SetCellBool}

```go
func (f *File) SetCellBool(sheet, axis string, value bool) error
```

指定されたワークシート名とセル座標に基づいて、ブール型 (Boolean) のセルの値を設定します。

## 既定の文字の種類の値を設定する {#SetCellDefault}

```go
func (f *File) SetCellDefault(sheet, axis, value string) error
```

指定されたワークシート名とセル座標に基づいて、文字セルの値を設定し、特殊文字に対してはフィルタされません。

## 実数を設定する {#SetCellInt}

```go
func (f *File) SetCellInt(sheet, axis string, value int) error
```

指定されたワークシート名とセル座標に基づいて、実際のセルの値を設定します。

## 文字列値の設定 {#SetCellStr}

```go
func (f *File) SetCellStr(sheet, axis, value string) error
```

指定したワークシート名とセル座標に基づいて文字セルの値を設定すると、文字は特殊文字でフィルタリングされ、文字列の累積長は `32767` を超えてはならず、余分な文字は無視されます。

## セルスタイルの設定 {#SetCellStyle}

```go
func (f *File) SetCellStyle(sheet, hCell, vCell string, styleID int) error
```

指定されたワークシート名、セル座標領域、およびスタイルインデックスに基づいて、セルの値を設定します。スタイルインデックスは [`NewStyle`](style.md#NewStyle) 関数を使用して取得できます。同じ座標領域内の `diagonaldown` と `diagonalup` は同じ色で保持する必要があることに注意してください。SetCellStyle は、セルの既存のスタイルを上書きし、スタイルを既存のスタイルに追加またはマージしません。

- 例1、ワークシート `D7` セル `Sheet1` の境界線のスタイルを設定します:

```go
style, err := f.NewStyle(&excelize.Style{
    Border: []excelize.Border{
        {Type: "left", Color: "0000FF", Style: 3},
        {Type: "top", Color: "00FF00", Style: 4},
        {Type: "bottom", Color: "FFFF00", Style: 5},
        {Type: "right", Color: "FF0000", Style: 6},
        {Type: "diagonalDown", Color: "A020F0", Style: 7},
        {Type: "diagonalUp", Color: "A020F0", Style: 8},
    },
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_01.png" alt="Excel セルの枠線のスタイルを設定する"></p>

セル `D7` の4つの境界は、[`NewStyle`](style.md#NewStyle) 関数を呼び出すときにパラメータに関連する異なるスタイルと色に設定されており、その章のドキュメントを参照するために異なるスタイルを設定する必要があります。

- 例2では、ワークシート `D7` セル `Sheet1` という名前のグラデーションスタイルを設定します:

```go
style, err := f.NewStyle(&excelize.Style{
    Fill: excelize.Fill{Type: "gradient", Color: []string{"#FFFFFF", "#E0EBF5"}, Shading: 1},
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_02.png" alt="セルのグラデーションスタイルを設定する"></p>

セル `D7` はグラデーション効果の塗りつぶしに設定され、グラデーションの塗りつぶし効果は [`NewStyle`](style.md#NewStyle) 関数を呼び出すときのパラメーターに関連しており、その章のドキュメントを参照するために異なるスタイルを設定する必要があります。

- 例3では、ワークシート `D7` セル `Sheet1` という名前の単色の塗りつぶしを設定します:

```go
style, err := f.NewStyle(&excelize.Style{
    Fill: excelize.Fill{Type: "pattern", Color: []string{"#E0EBF5"}, Pattern: 1},
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_03.png" alt="セルに単色の塗りつぶしを設定する"></p>

セル `D7` は単色の塗りつぶしに設定されています。

- 例4では、ワークシート `D7` セルの文字間隔と回転角度を `Sheet1` という名前で設定します:

```go
f.SetCellValue("Sheet1", "D7", "Style")
style, err := f.NewStyle(&excelize.Style{
    Alignment: &excelize.Alignment{
        Horizontal:      "center",
        Indent:          1,
        JustifyLastLine: true,
        ReadingOrder:    0,
        RelativeIndent:  1,
        ShrinkToFit:     true,
        TextRotation:    45,
        Vertical:        "",
        WrapText:        true,
    },
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_04.png" alt="文字間隔と回転角度を設定する"></p>

- 例5の日付と時刻は、Excel が実数で表され、たとえば `2017/7/4  12:00:00 PM` が番号 `42920.5` で表すことができる。`Sheet1` という名前のワークシート `D7` セルの時刻形式を設定します:

```go
f.SetCellValue("Sheet1", "D7", 42920.5)
f.SetColWidth("Sheet1", "D", "D", 13)
style, err := f.NewStyle(&excelize.Style{NumFmt: 22})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_05.png" alt="セルの時間形式を設定する"></p>

セル `D7` は時刻形式で設定されています。 時刻形式のセルの幅が狭すぎて完全に表示できない場合は、`####` と表示され、調整列の幅をドラッグアンドドロップするか、適切なサイズに設定するために `SetColWidth` 関数を呼び出すことによって、列の大きさが適切であることを確認します。

- 例6、ワークシート `D7` という名前のセルのフォント、フォントサイズ、色、および傾きのスタイルを設定します：

```go
f.SetCellValue("Sheet1", "D7", "Excel")
style, err := f.NewStyle(&excelize.Style{
    Font: &excelize.Font{
        Bold:   true,
        Italic: true,
        Family: "Times New Roman",
        Size:   36,
        Color:  "#777777",
    },
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_06.png" alt="セルのフォント、フォントサイズ、色、および傾きのスタイルを設定する"></p>

- 例7、ワークシート `D7` セル `Sheet1` という名前をロックして非表示にします:

```go
style, err := f.NewStyle(&excelize.Style{
    Protection: &excelize.Protection{
        Hidden: true,
        Locked: true,
    },
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

セルをロックしたり数式を非表示にしたりするには、ワークシートを保護します。「校閲」タブで、「ワークシートの保護」をクリックします。

## ハイパーリンクの設定 {#SetCellHyperLink}

```go
func (f *File) SetCellHyperLink(sheet, axis, link, linkType string) error
```

指定したワークシート、セル座標、リンクされたリソース、およびリソースの種類に基づいて、セルのハイパーリンクを設定します。 リソースの種類は、外部リンクアドレス `External` とブック内部の場所のリンク `Location` 2 種類に分割されます。ワークシート内の最大ハイパーリンク数は `65530` です。この関数は、セルのハイパーリンクを設定するためにのみ使用され、セルの値には影響しません。セルの値を設定する必要がある場合は、[`SetCellStyle`](cell.md#SetCellStyle) や [`SetSheetRow`](sheet.md#SetSheetRow) などの他の関数を使用してください。

- 例1、ワークシート `A3` セル `Sheet1` という名前の外部リンクを追加します:

```go
if err := f.SetCellHyperLink("Sheet1", "A3",
    "https://github.com/xuri/excelize", "External"); err != nil {
    fmt.Println(err)
}
// セルのフォントとアンダースコアのスタイルを設定する
style, err := f.NewStyle(&excelize.Style{
    Font: &excelize.Font{Color: "#1265BE", Underline: "single"},
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "A3", "A3", style)
```

- 例2では、ワークシート `A3` セル `Sheet1` という名前の内部の場所のリンクを追加します:

```go
err := f.SetCellHyperLink("Sheet1", "A3", "Sheet1!A40", "Location")
```

## セルのリッチテキストを設定する {#SetCellRichText}

```go
func (f *File) SetCellRichText(sheet, cell string, runs []RichTextRun) error
```

SetCellRichText は、特定のワークシートによってリッチテキストを含むセルを設定する関数を提供します。

たとえば、`Sheet1`という名前のワークシートの `A1` セルにリッチテキストを設定します：

<p align="center"><img width="612" src="./images/rich_text.png" alt="セルのリッチテキストを設定する"></p>

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    if err := f.SetRowHeight("Sheet1", 1, 35); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SetColWidth("Sheet1", "A", "A", 44); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SetCellRichText("Sheet1", "A1", []excelize.RichTextRun{
        {
            Text: "bold",
            Font: &excelize.Font{
                Bold:   true,
                Color:  "2354e8",
                Family: "Times New Roman",
            },
        },
        {
            Text: " and ",
            Font: &excelize.Font{
                Family: "Times New Roman",
            },
        },
        {
            Text: "italic",
            Font: &excelize.Font{
                Bold:   true,
                Color:  "e83723",
                Italic: true,
                Family: "Times New Roman",
            },
        },
        {
            Text: "text with color and font-family,",
            Font: &excelize.Font{
                Bold:   true,
                Color:  "2354e8",
                Family: "Times New Roman",
            },
        },
        {
            Text: "\r\nlarge text with ",
            Font: &excelize.Font{
                Size:  14,
                Color: "ad23e8",
            },
        },
        {
            Text: "strike",
            Font: &excelize.Font{
                Color:  "e89923",
                Strike: true,
            },
        },
        {
            Text: " and ",
            Font: &excelize.Font{
                Size:  14,
                Color: "ad23e8",
            },
        },
        {
            Text: "underline.",
            Font: &excelize.Font{
                Color:     "23e833",
                Underline: "single",
            },
        },
    }); err != nil {
        fmt.Println(err)
        return
    }
    style, err := f.NewStyle(&excelize.Style{
        Alignment: &excelize.Alignment{
            WrapText: true,
        },
    })
    if err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SetCellStyle("Sheet1", "A1", "A1", style); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## リッチテキスト形式を取得する {#GetCellRichText}

```go
func (f *File) GetCellRichText(sheet, cell string) (runs []RichTextRun, err error)
```

指定されたワークシートとセル座標に従って、指定されたセルのリッチテキスト形式を取得します。

## セル値取得 {#GetCellValue}

```go
func (f *File) GetCellValue(sheet, axis string, opts ...Options) (string, error)
```

指定されたワークシートとセルの座標に基づいてセルの値を取得すると、戻り値は `string` 型に変換されます。セルの値にセル書式を適用できる場合は、適用された値が返されます。差し込み印刷範囲内のすべてのセルの値は同じです。

## セルタイプを取得します {#GetCellType}

```go
func (f *File) GetCellType(sheet, axis string) (CellType, error)
```

GetCellType は、スプレッドシートファイル内の指定されたワークシート名と軸によってセルのデータ型を取得する関数を提供します。

## 列ごとにすべてのセル値を取得する {#GetCols}

```go
func (f *File) GetCols(sheet string, opts ...Options) ([][]string, error)
```

指定されたワークシート名（大文字と小文字を区別）に基づいて、ワークシートの列ごとにすべてのセルの値を取得し、2次元配列として返されます。セルの値は `string` タイプに変換されます。 セルのフォーマットをセルの値に適用できる場合は、適用された値が使用されます。それ以外の場合は、元の値が使用されます。

たとえば、`Sheet1` という名前のワークシートの列ごとにすべてのセルの値を取得してトラバースします。

```go
cols, err := f.GetCols("Sheet1")
if err != nil {
    fmt.Println(err)
    return
}
for _, col := range cols {
    for _, rowCell := range col {
        fmt.Print(rowCell, "\t")
    }
    fmt.Println()
}
```

## 行ごとにすべてのセル値を取得する {#GetRows}

```go
func (f *File) GetRows(sheet string, opts ...Options) ([][]string, error)
```

指定されたワークシート名（大文字と小文字を区別）に基づいて、ワークシートの行ごとにすべてのセルの値を取得し、2次元配列として返されます。セルの値は `string` タイプに変換されます。 セルのフォーマットをセルの値に適用できる場合は、適用された値が使用されます。それ以外の場合は、元の値が使用されます。GetRows は、値セルまたは数式セルを含む行をフェッチしました。末尾の連続して空のセルはスキップされます。

たとえば、`Sheet1` という名前のワークシートの行ごとにすべてのセルの値を取得してトラバースします。

```go
rows, err := f.GetRows("Sheet1")
if err != nil {
    fmt.Println(err)
    return
}
for _, row := range rows {
    for _, colCell := range row {
        fmt.Print(colCell, "\t")
    }
    fmt.Println()
}
if err = rows.Close(); err != nil {
    fmt.Println(err)
}
```

## ハイパーリンクを取得 {#GetCellHyperLink}

```go
func (f *File) GetCellHyperLink(sheet, axis string) (bool, string, error)
```

指定されたワークシート名 (大文字小文字を区別する) とセル座標に基づいてセルのハイパーリンクを取得し、セルにハイパーリンクがある場合は `true` とリンクアドレスが返され、それ以外の場合は `false` と空のリンクアドレスが返されます。

たとえば、`Sheet1` という名前のワークシートのハイパーリンクを `H6` セルの座標で取得します:

```go
link, target, err := f.GetCellHyperLink("Sheet1", "H6")
```

## スタイルインデックスの取得 {#GetCellStyle}

```go
func (f *File) GetCellStyle(sheet, axis string) (int, error)
```

指定されたワークシート名 (大文字小文字の区別) とセルの座標に基づいてセルスタイルのインデックスを取得し、セルのスタイルをコピーするときに `setcellvalue` 関数を呼び出すパラメーターとして使用できるインデックスを取得します。

## セルを結合 {#MergeCell}

```go
func (f *File) MergeCell(sheet, hCell, vCell string) error
```

指定したシート名 (大文字と小文字に敏感) とセルの座標範囲に基づいてセルを結合します。結合領域内には左上のセルの値のみが保持され、他のセルの値は無視されます。たとえば、`Sheet1` という名前のワークシートの `D3:E9` 領域のセルを結合します。

```go
err := f.MergeCell("Sheet1", "D3", "E9")
```

指定したセルの座標領域が既に存在する他の結合セルと重なっている場合、既存の結合セルは削除されます。

## セルの結合を解除 {#UnmergeCell}

```go
func (f *File) UnmergeCell(sheet string, hCell, vCell string) error
```

UnmergeCell は、指定された座標領域の結合を解除する機能を提供します。たとえば、`Sheet1` の領域 `D3E9` のマージを解除します:

```go
err := f.UnmergeCell("Sheet1", "D3", "E9")
```

重要：重複した領域もマージされません。

## セルを結合する {#GetMergeCells}

指定されたワークシート名 (大文字小文字の区別) に基づいて、すべての結合セルの座標領域と値を取得します。

```go
func (f *File) GetMergeCells(sheet string) ([]MergeCell, error)
```

### 結合されたセルの値を取得する

```go
func (m *MergeCell) GetCellValue() string
```

GetCellValue は、結合されたセル値を返します。

### マージされた範囲の左上のセル座標を取得します

```go
func (m *MergeCell) GetStartAxis() string
```

GetStartAxis は、マージされた範囲の左上のセル座標を返します（例：`C2`）。

### マージされた範囲の右下のセル座標を取得します

```go
func (m *MergeCell) GetEndAxis() string
```

GetEndAxis は、マージされた範囲の右下のセル座標を返します（例：`D4`）。

## コメント追加 {#AddComment}

```go
func (f *File) AddComment(sheet, cell, format string) error
```

指定されたワークシート名、セル座標、およびスタイルパラメータ (作成者とテキスト情報) に基づいて注釈を追加します。作成者情報の最大長は 255 文字で、テキストの最大内容は 32512 文字で、その範囲を超える文字は無視されます。たとえば、`Sheet1!$A$3` セルに注釈を追加します。

<p align="center"><img width="612" src="./images/comment.png" alt="Excel ドキュメントに注釈を追加する"></p>

```go
err := f.AddComment("Sheet1", "A3", `{"author":"Excelize: ","text":"This is a comment."}`)
```

## コメントを得る {#GetComments}

```go
func (f *File) GetComments() (comments map[string][]Comment)
```

このメソッドを使用すると、すべてのワークシートからコメントを取得できます。

## セル式の設定 {#SetCellFormula}

```go
func (f *File) SetCellFormula(sheet, axis, formula string, opts ...FormulaOpts) error
```

指定されたワークシート名 (大文字小文字の区別) とセルの設定に基づいて、セルの数式を設定します。数式セルの結果は、ワークシートが Office Excel アプリケーションで開かれた場合、または計算されたセル値を取得する場合に [CalcCellValue](cell.md#CalcCellValue) 関数を使用して計算できます。Excel アプリケーションがブックを開いたときに数式を自動的に計算しない場合は、セルの数式関数を設定した後に [UpdateLinkedValue](utils.md#UpdateLinkedValue) を呼び出してください。

- 例1, `Sheet1` のセル `A3` に通常の数式 `=SUM(A1,B1)` を設定します：

```go
err := f.SetCellFormula("Sheet1", "A3", "=SUM(A1,B1)")
```

- 例2, `Sheet1` のセル `A3` に1次元の垂直定数配列（行配列）式 `1,2,3` を設定します：

```go
err := f.SetCellFormula("Sheet1", "A3", "={1,2,3}")
```

- 例3, `Sheet1` のセル `A3` に1次元の水平定数配列（列配列）の数式 `"a","b","c"` を設定します：

```go
err := f.SetCellFormula("Sheet1", "A3", "={\"a\",\"b\",\"c\"}")
```

- 例4, `Sheet1` のセル `A3` に2次元定数配列数式 `{1,2,"a","b"}` を設定します：

```go
formulaType, ref := excelize.STCellFormulaTypeArray, "A3:A3"
err := f.SetCellFormula("Sheet1", "A3", "={1,2,\"a\",\"b\"}",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- 例5, `Sheet1` のセル `A3` に範囲配列数式 `A1:A2` を設定します：

```go
formulaType, ref := excelize.STCellFormulaTypeArray, "A3:A3"
err := f.SetCellFormula("Sheet1", "A3", "=A1:A2",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- 例6, `Sheet1` のセル `C1:C5` に共有数式 `=A1+B1` を設定します。`C1` はマスターセルです：

```go
formulaType, ref := excelize.STCellFormulaTypeShared, "C1:C5"
err := f.SetCellFormula("Sheet1", "C1", "=A1+B1",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- 例7, `Sheet1` のセル `C2` にテーブル数式 `=SUM(Table1[[A]:[B]])` を設定します：

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    for idx, row := range [][]interface{}{{"A", "B", "C"}, {1, 2}} {
        if err := f.SetSheetRow("Sheet1", fmt.Sprintf("A%d", idx+1), &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    if err := f.AddTable("Sheet1", "A1", "C2",
        `{"table_name":"Table1","table_style":"TableStyleMedium2"}`); err != nil {
        fmt.Println(err)
        return
    }
    formulaType := excelize.STCellFormulaTypeDataTable
    if err := f.SetCellFormula("Sheet1", "C2", "=SUM(Table1[[A]:[B]])",
        excelize.FormulaOpts{Type: &formulaType}); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## セル式を取得する {#GetCellFormula}

```go
func (f *File) GetCellFormula(sheet, axis string) (string, error)
```

指定されたワークシート名 (大文字小文字の区別) とセルの座標に基づいて、セルの数式を取得します。

## セル値を計算する {#CalcCellValue}

```go
func (f *File) CalcCellValue(sheet, cell string) (result string, err error)
```

CalcCellValue は、計算されたセル値を取得する関数を提供します。この機能は現在処理中です。配列数式、テーブル数式、その他の数式は現在サポートされていません。

サポートされている式：

```text
ABS
ACCRINT
ACCRINTM
ACOS
ACOSH
ACOT
ACOTH
ADDRESS
AMORDEGRC
AMORLINC
AND
ARABIC
ASIN
ASINH
ATAN
ATAN2
ATANH
AVEDEV
AVERAGE
AVERAGEA
AVERAGEIF
AVERAGEIFS
BASE
BESSELI
BESSELJ
BESSELK
BESSELY
BETADIST
BETA.DIST
BETAINV
BETA.INV
BIN2DEC
BIN2HEX
BIN2OCT
BINOMDIST
BINOM.DIST
BINOM.DIST.RANGE
BINOM.INV
BITAND
BITLSHIFT
BITOR
BITRSHIFT
BITXOR
CEILING
CEILING.MATH
CEILING.PRECISE
CHAR
CHIDIST
CHIINV
CHITEST
CHISQ.DIST
CHISQ.DIST.RT
CHISQ.INV
CHISQ.INV.RT
CHISQ.TEST
CHOOSE
CLEAN
CODE
COLUMN
COLUMNS
COMBIN
COMBINA
COMPLEX
CONCAT
CONCATENATE
CONFIDENCE
CONFIDENCE.NORM
CONFIDENCE.T
CONVERT
CORREL
COS
COSH
COT
COTH
COUNT
COUNTA
COUNTBLANK
COUNTIF
COUNTIFS
COUPDAYBS
COUPDAYS
COUPDAYSNC
COUPNCD
COUPNUM
COUPPCD
COVAR
COVARIANCE.P
COVARIANCE.S
CRITBINOM
CSC
CSCH
CUMIPMT
CUMPRINC
DATE
DATEDIF
DATEVALUE
DAY
DAYS
DB
DDB
DEC2BIN
DEC2HEX
DEC2OCT
DECIMAL
DEGREES
DELTA
DEVSQ
DISC
DOLLARDE
DOLLARFR
DURATION
EFFECT
ENCODEURL
ERF
ERF.PRECISE
ERFC
ERFC.PRECISE
ERROR.TYPE
EVEN
EXACT
EXP
EXPON.DIST
EXPONDIST
FACT
FACTDOUBLE
FALSE
F.DIST
F.DIST.RT
FDIST
FIND
FINDB
F.INV
F.INV.RT
FINV
FISHER
FISHERINV
FIXED
FLOOR
FLOOR.MATH
FLOOR.PRECISE
FORMULATEXT
F.TEST
FTEST
FV
FVSCHEDULE
GAMMA
GAMMA.DIST
GAMMADIST
GAMMA.INV
GAMMAINV
GAMMALN
GAMMALN.PRECISE
GAUSS
GCD
GEOMEAN
GESTEP
GROWTH
HARMEAN
HEX2BIN
HEX2DEC
HEX2OCT
HLOOKUP
HOUR
HYPGEOM.DIST
HYPGEOMDIST
IF
IFERROR
IFNA
IFS
IMABS
IMAGINARY
IMARGUMENT
IMCONJUGATE
IMCOS
IMCOSH
IMCOT
IMCSC
IMCSCH
IMDIV
IMEXP
IMLN
IMLOG10
IMLOG2
IMPOWER
IMPRODUCT
IMREAL
IMSEC
IMSECH
IMSIN
IMSINH
IMSQRT
IMSUB
IMSUM
IMTAN
INDEX
INDIRECT
INT
INTRATE
IPMT
IRR
ISBLANK
ISERR
ISERROR
ISEVEN
ISFORMULA
ISLOGICAL
ISNA
ISNONTEXT
ISNUMBER
ISODD
ISREF
ISTEXT
ISO.CEILING
ISOWEEKNUM
ISPMT
KURT
LARGE
LCM
LEFT
LEFTB
LEN
LENB
LN
LOG
LOG10
LOGINV
LOGNORM.DIST
LOGNORMDIST
LOGNORM.INV
LOOKUP
LOWER
MATCH
MAX
MAXA
MAXIFS
MDETERM
MDURATION
MEDIAN
MID
MIDB
MIN
MINA
MINIFS
MINUTE
MINVERSE
MIRR
MMULT
MOD
MODE
MODE.MULT
MODE.SNGL
MONTH
MROUND
MULTINOMIAL
MUNIT
N
NA
NEGBINOM.DIST
NEGBINOMDIST
NOMINAL
NORM.DIST
NORMDIST
NORM.INV
NORMINV
NORM.S.DIST
NORMSDIST
NORM.S.INV
NORMSINV
NOT
NOW
NPER
NPV
OCT2BIN
OCT2DEC
OCT2HEX
ODD
ODDFPRICE
OR
PDURATION
PEARSON
PERCENTILE.EXC
PERCENTILE.INC
PERCENTILE
PERCENTRANK.EXC
PERCENTRANK.INC
PERCENTRANK
PERMUT
PERMUTATIONA
PHI
PI
PMT
POISSON.DIST
POISSON
POWER
PPMT
PRICE
PRICEDISC
PRICEMAT
PRODUCT
PROPER
PV
QUARTILE
QUARTILE.EXC
QUARTILE.INC
QUOTIENT
RADIANS
RAND
RANDBETWEEN
RANK
RANK.EQ
RATE
RECEIVED
REPLACE
REPLACEB
REPT
RIGHT
RIGHTB
ROMAN
ROUND
ROUNDDOWN
ROUNDUP
ROW
ROWS
RRI
RSQ
SEC
SECH
SECOND
SERIESSUM
SHEET
SHEETS
SIGN
SIN
SINH
SKEW
SKEW.P
SLN
SLOPE
SMALL
SQRT
SQRTPI
STANDARDIZE
STDEV
STDEV.P
STDEV.S
STDEVA
STDEVP
STDEVPA
SUBSTITUTE
SUM
SUMIF
SUMIFS
SUMPRODUCT
SUMSQ
SUMX2MY2
SUMX2PY2
SUMXMY2
SWITCH
SYD
T
TAN
TANH
TBILLEQ
TBILLPRICE
TBILLYIELD
T.DIST
T.DIST.2T
T.DIST.RT
TDIST
TEXTJOIN
TIME
TIMEVALUE
T.INV
T.INV.2T
TINV
TODAY
TRANSPOSE
TREND
TRIM
TRIMMEAN
TRUE
TRUNC
T.TEST
TTEST
TYPE
UNICHAR
UNICODE
UPPER
VALUE
VAR
VAR.P
VAR.S
VARA
VARP
VARPA
VDB
VLOOKUP
WEEKDAY
WEIBULL
WEIBULL.DIST
XIRR
XLOOKUP
XNPV
XOR
YEAR
YEARFRAC
YIELD
YIELDDISC
YIELDMAT
Z.TEST
ZTEST
```
