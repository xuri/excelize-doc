# セル

`RichTextRun` は、リッチテキストランの設定を直接マップします。

```go
type RichTextRun struct {
    Font *Font
    Text string
}
```

`HyperlinkOpts` を [`SetCellHyperlink`](cell.md#SetCellHyperlink) に渡して、オプションのハイパーリンク属性（表示するテキストや画面のヒントテキストなど）を設定できます。

```go
type HyperlinkOpts struct {
    Display *string
    Tooltip *string
}
```

`FormulaOpts` を [`SetCellFormula`](cell.md#SetCellFormula) に渡して、他の数式タイプを使用することができます。

```go
type FormulaOpts struct {
    Type *string // フォーミュラ タイプ
    Ref  *string // 共有式参照
}
```

## セル値設定 {#SetCellValue}

```go
func (f *File) SetCellValue(sheet, cell string, value interface{}) error
```

指定されたワークシート名とセル座標に基づいて、セルの値を設定します。この関数は、同時実行セーフをサポートします。指定された座標は、テーブルの最初の行にあるべきではありません。

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
func (f *File) SetCellBool(sheet, cell string, value bool) error
```

指定されたワークシート名とセル座標に基づいて、ブール型 (Boolean) のセルの値を設定します。

## 既定の文字の種類の値を設定する {#SetCellDefault}

```go
func (f *File) SetCellDefault(sheet, cell, value string) error
```

指定されたワークシート名とセル座標に基づいて、文字セルの値を設定し、特殊文字に対してはフィルタされません。

## 実数を設定する {#SetCellInt}

```go
func (f *File) SetCellInt(sheet, cell string, value int64) error
```

指定されたワークシート名、セル参照、およびセル値によってセルの `int64` 型の値を設定する関数を提供します。

## 符号なし整数値を設定する {#SetCellUint}

```go
func (f *File) SetCellUint(sheet, cell string, value uint64) error
```

SetCellUint は、指定されたワークシート名、セル参照、およびセル値によってセルの符号なし整数データ型の値を設定する関数を提供します。

## 浮動小数点値の設定 {#SetCellFloat}

```go
func (f *File) SetCellFloat(sheet, cell string, value float64, precision, bitSize int) error
```

SetCellFloat は浮動小数点値をセルに設定します。`precision` パラメータは小数点以下の桁数を指定しますが、`-1` は数値を表すために必要な数の小数点以下の桁数を使用する特別な値です。`bitSize` は、`float32` または `float64` が最初に値に使用されたかどうかに応じて、`32` または `64` です。

## 文字列値の設定 {#SetCellStr}

```go
func (f *File) SetCellStr(sheet, cell, value string) error
```

指定したワークシート名とセル座標に基づいて文字セルの値を設定すると、文字は特殊文字でフィルタリングされ、文字列の累積長は `32767` を超えてはならず、余分な文字は無視されます。

## セルスタイルの設定 {#SetCellStyle}

```go
func (f *File) SetCellStyle(sheet, topLeftCell, bottomRightCell string, styleID int) error
```

指定されたワークシート名、セル座標領域、およびスタイルインデックスに基づいて、セルの値を設定します。この関数は、同時実行セーフをサポートします。スタイルインデックスは [`NewStyle`](style.md#NewStyle) 関数を使用して取得できます。同じ座標領域内の `diagonaldown` と `diagonalup` は同じ色で保持する必要があることに注意してください。SetCellStyle は、セルの既存のスタイルを上書きし、スタイルを既存のスタイルに追加またはマージしません。

- 例1、ワークシート `D7` セル `Sheet1` の境界線のスタイルを設定します:

```go
style, err := f.NewStyle(&excelize.Style{
    Border: []excelize.Border{
        {Type: "left", Color: "0000FF", Style: 3},
        {Type: "top", Color: "00FF00", Style: 4},
        {Type: "bottom", Color: "FFFF00", Style: 5},
        {Type: "right", Color: "FF0000", Style: 6},
        {Type: "diagonalDown", Color: "A020F0", Style: 8},
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
    Fill: excelize.Fill{Type: "gradient", Color: []string{"FFFFFF", "E0EBF5"}, Shading: 1},
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
    Fill: excelize.Fill{Type: "pattern", Color: []string{"E0EBF5"}, Pattern: 1},
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
        Color:  "777777",
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
func (f *File) SetCellHyperLink(sheet, cell, link, linkType string, opts ...HyperlinkOpts) error
```

指定したワークシート、セル座標、リンクされたリソース、およびリソースの種類に基づいて、セルのハイパーリンクを設定します。 リソースの種類は、外部リンクアドレス `External` とブック内部の場所のリンク `Location` 2 種類に分割されます。ワークシート内の最大ハイパーリンク数は `65530` です。この関数は、セルのハイパーリンクを設定するためにのみ使用され、セルの値には影響しません。セルの値を設定する必要がある場合は、[`SetCellStyle`](cell.md#SetCellStyle) や [`SetSheetRow`](sheet.md#SetSheetRow) などの他の関数を使用してください。

- 例1、ワークシート `A3` セル `Sheet1` という名前の外部リンクを追加します:

```go
display, tooltip := "https://github.com/xuri/excelize", "Excelize on GitHub"
if err := f.SetCellHyperLink("Sheet1", "A3",
    "https://github.com/xuri/excelize", "External", excelize.HyperlinkOpts{
        Display: &display,
        Tooltip: &tooltip,
    }); err != nil {
    fmt.Println(err)
}
// セルのフォントとアンダースコアのスタイルを設定する
style, err := f.NewStyle(&excelize.Style{
    Font: &excelize.Font{Color: "1265BE", Underline: "single"},
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
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
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
                Color:  "2354E8",
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
            Text: "italic ",
            Font: &excelize.Font{
                Bold:   true,
                Color:  "E83723",
                Italic: true,
                Family: "Times New Roman",
            },
        },
        {
            Text: "text with color and font-family,",
            Font: &excelize.Font{
                Bold:   true,
                Color:  "2354E8",
                Family: "Times New Roman",
            },
        },
        {
            Text: "\r\nlarge text with ",
            Font: &excelize.Font{
                Size:  14,
                Color: "AD23E8",
            },
        },
        {
            Text: "strike",
            Font: &excelize.Font{
                Color:  "E89923",
                Strike: true,
            },
        },
        {
            Text: " superscript",
            Font: &excelize.Font{
                Color:     "DBC21F",
                VertAlign: "superscript",
            },
        },
        {
            Text: " and ",
            Font: &excelize.Font{
                Size:      14,
                Color:     "AD23E8",
                VertAlign: "baseline",
            },
        },
        {
            Text: "underline",
            Font: &excelize.Font{
                Color:     "23E833",
                Underline: "single",
            },
        },
        {
            Text: " subscript.",
            Font: &excelize.Font{
                Color:     "017505",
                VertAlign: "subscript",
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
func (f *File) GetCellRichText(sheet, cell string) ([]RichTextRun, error)
```

指定されたワークシートとセル座標に従って、指定されたセルのリッチテキスト形式を取得します。

## セル値取得 {#GetCellValue}

```go
func (f *File) GetCellValue(sheet, cell string, opts ...Options) (string, error)
```

指定されたワークシートとセルの座標に基づいてセルの値を取得すると、戻り値は `string` 型に変換されます。この関数は、同時実行セーフをサポートします。セルの値にセル書式を適用できる場合は、適用された値が返されます。差し込み印刷範囲内のすべてのセルの値は同じです。

## セルタイプを取得します {#GetCellType}

```go
func (f *File) GetCellType(sheet, cell string) (CellType, error)
```

GetCellType は、スプレッドシートファイル内の指定されたワークシート名と軸によってセルのデータ型を取得する関数を提供します。

## 列ごとにすべてのセル値を取得する {#GetCols}

```go
func (f *File) GetCols(sheet string, opts ...Options) ([][]string, error)
```

GetCols は、指定されたワークシート名に基づいてワークシートの列ごとにすべてのセルの値を取得し、2 次元配列として返されます。ここで、セルの値は `string`タイプに変換されます。セル形式をセルの値に適用できる場合は、適用された値が使用されます。それ以外の場合は、元の値が使用されます。

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

GetRows は、指定されたワークシート名でシート内のすべての行を返し、2 次元配列として返されます。ここで、セルの値は `string` タイプに変換されます。セル形式をセルの値に適用できる場合は、適用された値が使用されます。それ以外の場合は、元の値が使用されます。GetRows は、値セルまたは数式セルを含む行をフェッチしました。各行の末尾にある空白のセルはスキップされるため、各行の長さが一致しない場合があります。

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
```

## ハイパーリンクを取得 {#GetCellHyperLink}

```go
func (f *File) GetCellHyperLink(sheet, cell string) (bool, string, error)
```

指定されたワークシート名とセル座標に基づいてセルのハイパーリンクを取得し、セルにハイパーリンクがある場合は `true` とリンクアドレスが返され、それ以外の場合は `false` と空のリンクアドレスが返されます。

たとえば、`Sheet1` という名前のワークシートのハイパーリンクを `H6` セルの座標で取得します:

```go
link, target, err := f.GetCellHyperLink("Sheet1", "H6")
```

## スタイルインデックスの取得 {#GetCellStyle}

```go
func (f *File) GetCellStyle(sheet, cell string) (int, error)
```

指定されたワークシート名とセルの座標に基づいてセルスタイルのインデックスを取得し、セルのスタイルをコピーするときに `SetCellStyle` 関数を呼び出すパラメーターとして使用できるインデックスを取得します。

## セルを結合 {#MergeCell}

```go
func (f *File) MergeCell(sheet, topLeftCell, bottomRightCell string) error
```

指定したシート名 (大文字と小文字に敏感) とセルの座標範囲に基づいてセルを結合します。結合領域内には左上のセルの値のみが保持され、他のセルの値は無視されます。たとえば、`Sheet1` という名前のワークシートの `D3:E9` 領域のセルを結合します。

```go
err := f.MergeCell("Sheet1", "D3", "E9")
```

指定したセルの座標領域が既に存在する他の結合セルと重なっている場合、既存の結合セルは削除されます。

## セルの結合を解除 {#UnmergeCell}

```go
func (f *File) UnmergeCell(sheet, topLeftCell, bottomRightCell string) error
```

UnmergeCell は、指定された座標領域の結合を解除する機能を提供します。たとえば、`Sheet1` の領域 `D3E9` のマージを解除します:

```go
err := f.UnmergeCell("Sheet1", "D3", "E9")
```

重要：重複した領域もマージされません。

## セルを結合する {#GetMergeCells}

```go
func (f *File) GetMergeCells(sheet string, withoutValues ...bool) ([]MergeCell, error)
```

GetMergeCells は、特定のワークシートからすべての結合セルを取得する関数を提供します。`withoutValues` パラメータを `true` に設定すると、結合セルのセル値は返されず、範囲参照のみが返されます。例えば、`Sheet1` のすべての結合セルを取得するには、次のようにします:

```go
mergeCells, err := f.GetMergeCells("Sheet1")
```

セル値のない結合セルを取得する場合は、次のコードを使用できます:

```go
mergeCells, err := f.GetMergeCells("Sheet1", true)
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

## 画像セルを取得する {#GetPictureCells}

```go
func (f *File) GetPictureCells(sheet string) ([]string, error)
```

GetPictureCells は、特定のワークシート名でワークシート内のすべてのピクチャ セル参照を返します。

## コメント追加 {#AddComment}

```go
func (f *File) AddComment(sheet string, comment Comment) error
```

AddComment は、ワークシートのインデックス、セル、および書式設定（作成者やテキストなど）を指定して、シートにコメントを追加するメソッドを提供します。作成者の最大文字数は 255 文字、テキストの最大文字数は 32512 文字です。また、各セルにはコメントを 1 つしか設定できません。既にコメントが設定されているセルにコメントを追加するとエラーが発生します。例えば、`Sheet1!A3` にコメントを追加するには、次のようにします。

<p align="center"><img width="612" src="./images/comment.png" alt="Excel ドキュメントに注釈を追加する"></p>

```go
err := f.AddComment("Sheet1", excelize.Comment{
    Cell:   "A3",
    Author: "Excelize",
    Paragraph: []excelize.RichTextRun{
        {Text: "Excelize: ", Font: &excelize.Font{Bold: true}},
        {Text: "This is a comment."},
    },
})
```

## コメントを得る {#GetComments}

```go
func (f *File) GetComments(sheet string) ([]Comment, error)
```

GetComments は、指定されたワークシート名でワークシート内のすべてのコメントを取得します。

## コメントを削除 {#DeleteComment}

```go
func (f *File) DeleteComment(sheet, cell string) error
```

DeleteComment は、特定のワークシートでシート内のコメントを削除するメソッドを提供します。 たとえば、`Sheet1!A30` のコメントを削除します。

```go
err := f.DeleteComment("Sheet1", "A30")
```

## 無視されたエラーを追加する {#AddIgnoredErrors}

```go
func (f *File) AddIgnoredErrors(sheet, rangeRef string, ignoredErrorsType IgnoredErrorsType) error
```

AddIgnoredErrors は、セル範囲のエラーを無視する方法を提供します。たとえば、`Sheet1` のセル範囲 `D15 C18:D19` の「数値がテキストとして保存されています」エラーを無視します。

```go
err := f.AddIgnoredErrors("Sheet1", "D15 C18:D19", excelize.IgnoredErrorsNumberStoredAsText)
```

## セル式の設定 {#SetCellFormula}

```go
func (f *File) SetCellFormula(sheet, cell, formula string, opts ...FormulaOpts) error
```

SetCellFormula は、指定されたワークシート名およびセル式の設定に従って、セルに式が取得されるように設定する関数を提供します。数式セルの結果は、ワークシートが Office Excel アプリケーションで開かれた場合、または計算されたセル値を取得する場合に [CalcCellValue](cell.md#CalcCellValue) 関数を使用して計算できます。Excel アプリケーションがブックを開いたときに数式を自動的に計算しない場合は、セルの数式関数を設定した後に [UpdateLinkedValue](utils.md#UpdateLinkedValue) を呼び出してください。

- 例1, `Sheet1` のセル `A3` に通常の数式 `=SUM(A1,B1)` を設定します：

```go
err := f.SetCellFormula("Sheet1", "A3", "SUM(A1,B1)")
```

- 例2, `Sheet1` のセル `A3` に1次元の垂直定数配列式（列配列） `1;2;3` を設定します：

```go
err := f.SetCellFormula("Sheet1", "A3", "{1;2;3}")
```

- 例3, `Sheet1` のセル `A3` に1次元の水平定数配列（行配列）の数式 `"a","b","c"` を設定します：

```go
err := f.SetCellFormula("Sheet1", "A3", "{\"a\",\"b\",\"c\"}")
```

- 例4, `Sheet1` のセル `A3` に2次元定数配列数式 `{1,2;"a","b"}` を設定します：

```go
formulaType, ref := excelize.STCellFormulaTypeArray, "A3:A3"
err := f.SetCellFormula("Sheet1", "A3", "{1,2;\"a\",\"b\"}",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- 例5, `Sheet1` のセル `A3` に範囲配列数式 `A1:A2` を設定します：

```go
formulaType, ref := excelize.STCellFormulaTypeArray, "A3:A3"
err := f.SetCellFormula("Sheet1", "A3", "A1:A2",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- 例6, `Sheet1` のセル `C1:C5` に共有数式 `=A1+B1` を設定します。`C1` はマスターセルです：

```go
formulaType, ref := excelize.STCellFormulaTypeShared, "C1:C5"
err := f.SetCellFormula("Sheet1", "C1", "A1+B1",
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
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    for idx, row := range [][]interface{}{{"A", "B", "C"}, {1, 2}} {
        if err := f.SetSheetRow("Sheet1", fmt.Sprintf("A%d", idx+1), &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    if err := f.AddTable("Sheet1",
        &excelize.Table{
            Range:     "A1:C2",
            Name:      "Table1",
            StyleName: "TableStyleMedium2",
        }); err != nil {
        fmt.Println(err)
        return
    }
    formulaType := excelize.STCellFormulaTypeDataTable
    if err := f.SetCellFormula("Sheet1", "C2", "SUM(Table1[[A]:[B]])",
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
func (f *File) GetCellFormula(sheet, cell string) (string, error)
```

指定されたワークシート名とセルの座標に基づいて、セルの数式を取得します。

## セル値を計算する {#CalcCellValue}

```go
func (f *File) CalcCellValue(sheet, cell string, opts ...Options) (string, error)
```

CalcCellValue は、計算されたセル値を取得する関数を提供します。この機能は現在処理中です。反復計算、暗黙的交差、明示的交差、配列式、テーブル式、およびその他のいくつかの式は現在サポートされていません。

サポートされている式：

関数名 | 種類と説明
---|---
ABS                      | 数値の絶対値を返します
ACCRINT                  | 定期的に利息が支払われる証券の未収利息額を返します
ACCRINTM                 | 満期日に利息が支払われる証券の未収利息額を返します
ACOS                     | 数値の逆余弦 (アークコサイン) を返します
ACOSH                    | 数値の逆双曲線余弦を返します
ACOT                     | 数値の逆余接 (アークコタンジェント) を返します
ACOTH                    | 数値の逆双曲線余接を返します
AGGREGATE                | リストまたはデータベースの総計を返します
ADDRESS                  | ワークシート上の1つのセルにセル参照をテキストとして返します
AMORDEGRC                | 減価償却係数を使用して、各会計期における減価償却費を返します
AMORLINC                 | 各会計期における減価償却費を返します
AND                      | すべての引数が TRUE のときに TRUE を返します
ARABIC                   | ローマ数字をアラビア数字に変換します
ARRAYTOTEXT              | 指定した範囲のテキスト値の配列を返します
ASIN                     | 数値の逆正弦 (アークサイン) を返します
ASINH                    | 数値の逆双曲線正弦を返します
ATAN                     | 数値の逆正接 (アークタンジェント) を返します
ATAN2                    | 指定された x-y 座標の逆正接 (アークタンジェント) を返します
ATANH                    | 数値の逆双曲線正接を返します
AVEDEV                   | データ全体の平均値に対するそれぞれのデータの絶対偏差の平均を返します
AVERAGE                  | 引数の平均値を返します
AVERAGEA                 | 数値、文字列、および論理値を含む引数の平均値を返します
AVERAGEIF                | 範囲内の検索条件に一致するすべてのセルの平均値 (算術平均) を返します
AVERAGEIFS               | 複数の検索条件に一致するすべてのセルの平均値 (算術平均) を返します
BAHTTEXT                 | 数値をタイ語の文字列に変換し、バーツを表す接尾文字列を付加します
BASE                     | 数値を、指定された基数 (底) のテキスト表現に変換します
BESSELI                  | 修正ベッセル関数 In(x) を返します
BESSELJ                  | ベッセル関数 Jn(x) を返します
BESSELK                  | 修正ベッセル関数 Kn(x) を返します
BESSELY                  | ベッセル関数 Yn(x) を返します
BETADIST                 | β 分布の累積分布関数の値を返します。これは Excel 2007 では、統計関数になります
BETA.DIST                | β 分布の累積分布関数の値を返します
BETAINV                  | 指定された β 分布の累積分布関数の逆関数値を返します。これは Excel 2007 では、統計関数になります
BETA.INV                 | 指定された β 分布の累積分布関数の逆関数値を返します
BIN2DEC                  | 2 進数を 10 進数に変換します
BIN2HEX                  | 2 進数を 16 進数に変換します
BIN2OCT                  | 2 進数を 8 進数に変換します
BINOMDIST                | 二項分布の確率関数の値を返します。これは Excel 2007 では、統計関数になります
BINOM.DIST               | 二項分布の確率関数の値を返します
BINOM.DIST.RANGE         | 二項分布を使用した試行結果の確率を返します
BINOM.INV                | 累積二項分布の値が基準値以下になるような最小の値を返します
BITAND                   | 2 つの数値のビット演算 AND を返します
BITLSHIFT                | 左に移動数ビット (shift_amount) 移動する数値を返します
BITOR                    | 2 つの数値のビット演算 OR を返します
BITRSHIFT                | 右に移動数ビット (shift_amount) 移動する数値を返します
BITXOR                   | 2 つの数値のビット演算 "排他的 OR" を返します
CEILING                  | 指定された基準値の倍数のうち、最も近い値に数値を切り上げます
CEILING.MATH             | 数値を最も近い整数、または基準値に最も近い倍数に切り上げます
CEILING.PRECISE          | 数値を最も近い整数、または基準値に最も近い倍数に切り上げます。数値の符号に関係なく、切り上げます
CHAR                     | コード番号で指定された文字を返します
CHIDIST                  | カイ 2 乗分布の片側確率の値を返します。注: これは Excel 2007 では、統計関数になります
CHIINV                   | カイ 2 乗分布の片側確率の逆関数値を返します。注: これは Excel 2007 では、統計関数になります
CHITEST                  | 独立性検定を行います。注: これは Excel 2007 では、統計関数になります
CHISQ.DIST               | 累積 β 確率密度関数の値を返します
CHISQ.DIST.RT            | カイ 2 乗分布の片側確率の値を返します
CHISQ.INV                | 累積 β 確率密度関数の値を返します
CHISQ.INV.RT             | カイ 2 乗分布の片側確率の逆関数値を返します
CHISQ.TEST               | 独立性検定を行います
CHOOSE                   | 値のリストから値を選択します
CLEAN                    | 印刷できない文字を文字列から削除します
CODE                     | テキスト文字列内の先頭文字の数値コードを返します
COLUMN                   | セル参照の列番号を返します
COLUMNS                  | 指定の範囲に含まれる列数を返します
COMBIN                   | 指定された個数のオブジェクトを選択するときの組み合わせの数を返します
COMBINA                  | 指定された個数の項目を選択するときの組み合わせ (反復あり) の数を返します
COMPLEX                  | 実数係数と虚数係数を、複素数に変換します
CONCAT                   | 複数の範囲や文字列からのテキストを結合しますが、区切り記号または IgnoreEmpty 引数は提供しません
CONCATENATE              | 複数の文字列を 1 つの文字列に結合します
CONFIDENCE               | 母集団の平均に対する信頼区間を返します。これは Excel 2007 では、統計関数になります
CONFIDENCE.NORM          | 母集団の平均に対する信頼区間を返します
CONFIDENCE.T             | スチューデントの t 分布を使用して、母集団の平均に対する信頼区間を返します
CONVERT                  | 数値の単位を変換します
CORREL                   | 指定した2つの配列データの相関係数を返します
COS                      | 数値の余弦 (コサイン) を返します
COSH                     | 数値の双曲線余弦を返します
COT                      | 数値の双曲線余弦を返します
COTH                     | 角度のコタンジェントを返します
COUNT                    | 引数リストに含まれる数値の個数をカウントします
COUNTA                   | 引数リストに含まれる値の個数をカウントします
COUNTBLANK               | 指定された範囲に含まれる空白セルの個数をカウントします
COUNTIF                  | 指定された範囲に含まれるセルのうち、検索条件に一致するセルの個数をカウントします
COUNTIFS                 | 指定された範囲に含まれるセルのうち、複数の検索条件に一致するセルの個数を返します
COUPDAYBS                | 利払期間の第 1 日目から受渡日までの日数を返します
COUPDAYS                 | 受渡日を含む利払期間内の日数を返します
COUPDAYSNC               | 受渡日から次の利払日までの日数を返します
COUPNCD                  | 受渡日後の次の利払日を返します
COUPNUM                  | 受渡日と満期日の間の利払回数を返します
COUPPCD                  | 受渡日の直前の利払日を返します
COVAR                    | 共分散とは、2 組の対応するデータ間での標準偏差の積の平均値です。これは Excel 2007 では、統計関数になります
COVARIANCE.P             | 共分散とは、2 組の対応するデータ間での標準偏差の積の平均値です
COVARIANCE.S             | 共分散とは、2 組の対応するデータ間での標準偏差の積の平均値です
CRITBINOM                | 累積二項分布の値が基準値以下になるような最小の値を返します。これは Excel 2007 では、統計関数になります
CSC                      | 角度の余割 (コセカント) を返します
CSCH                     | 角度の双曲線余割を返します
CUMIPMT                  | 指定の期間に支払われる利息の累計を返します
CUMPRINC                 | 指定期間に、貸付金に対して支払われる元金の累計を返します
DATE                     | 指定された日付に対応するシリアル値を返します
DATEDIF                  | 指定された期間の日数、月数、年数を計算して返します。この関数は、年齢を計算する数式に使うと便利です
DATEVALUE                | 日付を表す文字列をシリアル値に変換します
DAVERAGE                 | 選択したデータベース レコードの平均値を返します
DAY                      | シリアル値を日付に変換します
DAYS                     | 2 つの日付間の日数を返します
DAYS360                  | 1 年を 360 日として、2 つの日付間の日数を返します
DB                       | 定率法 (Fixed-declining Balance Method) を利用して、特定の期における資産の減価償却費を返します
DCOUNT                   | データベース内にある数値を含むセルの個数をカウントします
DCOUNTA                  | データベース内にある空白でないセルの個数をカウントします
DDB                      | 倍額定率法 (Double-declining Balance Method) または指定した他の方法を使用して、特定の期における資産の減価償却費を返します
DEC2BIN                  | 10 進数を 2 進数に変換します
DEC2HEX                  | 10 進数を 16 進数に変換します
DEC2OCT                  | 10 進数を 8 進数に変換します
DECIMAL                  | 指定された底の数値のテキスト表現を 10 進数に変換します
DEGREES                  | ラジアンを度に変換します
DELTA                    | 2 つの値が等しいかどうかをテストします
DEVSQ                    | 偏差の平方和を返します
DGET                     | 指定された条件に一致する 1 つのレコードをデータベースから抽出します
DISC                     | 証券に対する割引率を返します
DMAX                     | 選択したデータベース レコードの最大値を返します
DMIN                     | 選択したデータベース レコードの最小値を返します
DOLLAR                   | 通貨形式を使用して数値をテキストに変換します。小数点は指定した桁数に丸められます
DOLLARDE                 | 分数で表されたドル単位の価格を、小数表示のドル価格に変換します
DOLLARFR                 | 小数で表されたドル単位の価格を、分数表示のドル価格に変換します
DPRODUCT                 | データベース内の、条件に一致するレコードの特定のフィールド値を乗算します
DSTDEV                   | 選択したデータベース レコードの標本に基づいて、標準偏差の推定値を返します
DSTDEVP                  | 選択したデータベース レコードの母集団全体に基づいて標準偏差を算出します
DSUM                     | データベース内の、条件に一致するレコードのフィールド列にある数値を合計します
DURATION                 | 定期的に利子が支払われる証券の年間のマコーレー デュレーションを返します
DVAR                     | 選択したデータベース レコードの標本に基づく分散の推定値を返します
DVARP                    | 選択したデータベース レコードの母集団全体に基づく分散を算出します
EDATE                    | 開始日から起算して、指定した月数だけ前または後の日付に対応するシリアル値を返します
EFFECT                   | 実効年利率を返します
ENCODEURL                | URL 形式でエンコードされた文字列を返します。この関数は Web 用 Excel では利用できません
EOMONTH                  | 指定した月数だけ前または後の月の最終日に対応するシリアル値を返します
ERF                      | 誤差関数の値を返します
ERF.PRECISE              | 誤差関数の値を返します
ERFC                     | 相補誤差関数の値を返します
ERFC.PRECISE             | x から無限大の範囲で、相補誤差関数の積分値を返します
ERROR.TYPE               | エラーの種類に対応する数値を返します
EUROCONVERT              | 数値からユーロ通貨への換算、ユーロ通貨からユーロ通貨使用国の現地通貨への換算、またはユーロ通貨を基にしてユーロ通貨を使用する参加国間の通貨の換算 (三通貨換算) を行います
EVEN                     | 指定された数値を最も近い偶数に切り上げた値を返します
EXACT                    | 2 つのテキスト値が等しいかどうかを判定します
EXP                      | e を底とする数値のべき乗を返します
EXPON.DIST               | 指数分布を返します
EXPONDIST                | 指数分布を返します。これは Excel 2007 では、統計関数になります
FACT                     | 数値の階乗を返します
FACTDOUBLE               | 数値の二重階乗を返します
FALSE                    | 論理値 FALSE を返します
F.DIST                   | F 分布の確率関数の値を返します
FDIST                    | F 分布の確率関数の値を返します。これは Excel 2007 では、統計関数になります
F.DIST.RT                | F 分布の確率関数の値を返します
FIND                     | 指定されたテキスト値を他のテキスト値の中で検索します。大文字と小文字は区別されます
FINDB                    | 指定されたテキスト値を他のテキスト値の中で検索します。大文字と小文字は区別されます
F.INV                    | F 分布の確率関数の逆関数の値を返します
F.INV.RT                 | F 分布の確率関数の逆関数の値を返します
FINV                     | F 分布の確率関数の逆関数の値を返します。これは Excel 2007 では、統計関数になります
FISHER                   | フィッシャー変換の値を返します
FISHERINV                | フィッシャー変換の逆関数値を返します
FIXED                    | 数値を、一定の桁数のテキストとして書式設定します
FLOOR                    | 数値を指定された桁数で切り捨てます。これは Excel 2007 と Excel 2010 では、数学/三角関数になります
FLOOR.MATH               | 最も近い整数値、または基準値の倍数のうちで最も近い値に切り下げます
FLOOR.PRECISE            | 数値を最も近い整数、または基準値に最も近い倍数に切り上げます。数値の符号に関係なく、切り上げます
FORECAST                 | 線形トレンドに沿った値を返します
FORECAST.LINEAR          | 線形トレンドに沿った値を返します
FORMULATEXT              | 指定された参照の位置にある数式をテキストとして返します
FREQUENCY                | 頻度分布を計算して、垂直配列として返します
F.TEST                   | F 検定の結果を返します
FTEST                    | F 検定の結果を返します。これは Excel 2007 では、統計関数になります
FV                       | 投資の将来価値を返します
FVSCHEDULE               | 一連の金利を複利計算することにより、初期投資した元金の将来の価値を返します
GAMMA                    | Gamma 関数値を返します
GAMMA.DIST               | ガンマ分布の値を返します
GAMMADIST                | ガンマ分布の値を返します。これは Excel 2007 では、統計関数になります
GAMMA.INV                | ガンマの累積分布の逆関数値を返します
GAMMAINV                 | ガンマの累積分布の逆関数値を返します。これは Excel 2007 では、統計関数になります
GAMMALN                  | ガンマ関数 Γ(x) の値の自然対数を返します
GAMMALN.PRECISE          | ガンマ関数 Γ(x) の値の自然対数を返します
GAUSS                    | 標準正規分布の累積分布関数より 0.5 小さい値を返します
GCD                      | 最大公約数を返します
GEOMEAN                  | 相乗平均を返します
GESTEP                   | 数値がしきい値以上であるかどうかをテストします
GROWTH                   | 指数曲線から予測される値を返します
HARMEAN                  | 調和平均を返します
HEX2BIN                  | 16 進数を 2 進数に変換します
HEX2DEC                  | 16 進数を 10 進数に変換します
HEX2OCT                  | 16 進数を 8 進数に変換します
HLOOKUP                  | 配列の上端行で特定の値を検索し、対応するセルの値を返します
HOUR                     | シリアル値を時刻に変換します
HYPERLINK                | ネットワーク サーバー、イントラネット、またはインターネット上に格納されているドキュメントを開くショートカットまたはジャンプを作成します
HYPGEOM.DIST             | 超幾何分布を返します
HYPGEOMDIST              | 超幾何分布を返します。これは Excel 2007 では、統計関数になります
IF                       | 実行する論理テストを指定します
IFERROR                  | 数式の結果がエラーの場合は指定した値を返し、それ以外の場合は数式の結果を返します
IFNA                     | それ以外の場合は、式の結果を返します
IFS                      | 1つ以上の条件が満たされているかどうかをチェックして、最初の TRUE 条件に対応する値を返します
IMABS                    | 指定した複素数の絶対値を返します
IMAGINARY                | 指定した複素数の虚数係数を返します
IMARGUMENT               | 偏角シータを (ラジアンで表した角度で) 返します
IMCONJUGATE              | 複素数の複素共役を返します
IMCOS                    | 複素数のコサインを返します
IMCOSH                   | 複素数の双曲線余弦を返します
IMCOT                    | 複素数の余接 (コタンジェント) を返します
IMCSC                    | 複素数の余割 (コセカント) を返します
IMCSCH                   | 複素数の双曲線余割を返します
IMDIV                    | 2 つの複素数の商を返します
IMEXP                    | 複素数のべき乗を返します
IMLN                     | 複素数の自然対数を返します
IMLOG10                  | 複素数の 10 を底とする対数 (常用対数) を返します
IMLOG2                   | 複素数の 2 を底とする対数を返します
IMPOWER                  | 複素数の整数乗を返します
IMPRODUCT                | 複素数の積を返します
IMREAL                   | 複素数の実数係数を返します
IMSEC                    | 複素数の正割 (セカント) を返します
IMSECH                   | 複素数の双曲線正割を返します
IMSIN                    | 複素数の正弦を返します
IMSINH                   | 複素数の双曲線正弦を返します
IMSQRT                   | 複素数の平方根を返します
IMSUB                    | 2 つの複素数の差を返します
IMSUM                    | 複素数の和を返します
IMTAN                    | 複素数の正接 (タンジェント) を返します
INDEX                    | セル参照または配列から、指定された位置の値を返します
INDIRECT                 | テキスト値によって指定されるセル参照を返します
INT                      | 指定された数値を最も近い整数に切り捨てます
INTERCEPT                | 線形回帰直線の切片を返します
INTRATE                  | 全額投資された証券の利率を返します
IPMT                     | 投資の指定された期に支払われる金利を返します
IRR                      | 一連のキャッシュ フローに対する内部利益率を返します
ISBLANK                  | 対象が空白セルを参照するときに TRUE を返します
ISERR                    | 対象が #N/A 以外のエラー値のときに TRUE を返します
ISERROR                  | 対象が任意のエラー値のときに TRUE を返します
ISEVEN                   | 数値が偶数のときに TRUE を返します
ISFORMULA                | 数式が含まれるセルへの参照がある場合に TRUE を返します
ISLOGICAL                | 対象が論理値のときに TRUE を返します
ISNA                     | 対象がエラー値 #N/A のときに TRUE を返します
ISNONTEXT                | 対象が文字列以外のときに TRUE を返します
ISNUMBER                 | 対象が数値のときに TRUE を返します
ISODD                    | 数値が奇数のときに TRUE を返しま
ISREF                    | 対象が参照であるときに TRUE を返します
ISTEXT                   | 対象がテキストであるときに TRUE を返します
ISO.CEILING              | 最も近い整数に切り上げた値、または、指定された基準値の倍数のうち最も近い値を返します
ISOWEEKNUM               | 指定された日付のその年における ISO 週番号を返します
ISPMT                    | 投資の指定された期に支払われる金利を計算します
KURT                     | データ セットの尖度を返します
LARGE                    | 指定されたデータ セットの中で k 番目に大きなデータを返します
LCM                      | 最小公倍数を返します
LEFT                     | 文字列の先頭 (左端) から指定された文字数の文字を返します
LEFTB                    | 文字列の先頭 (左端) から指定された文字数の文字を返します
LEN                      | 文字列に含まれる文字数を返します
LENB                     | 文字列に含まれる文字数を返します
LN                       | 数値の自然対数を返します
LOG                      | 指定された数を底とする数値の対数を返します
LOG10                    | 10 を底とする数値の対数 (常用対数) を返します
LOGINV                   | 対数の累積分布の逆関数値を返します
LOGNORM.DIST             | 対数の累積分布の値を返します
LOGNORMDIST              | 対数の累積分布の値を返します
LOGNORM.INV              | 対数の累積分布の逆関数値を返します
LOOKUP                   | ベクトルまたは配列を検索して、対応する値を返します
LOWER                    | テキストを小文字に変換します
MATCH                    | 参照または配列で値を検索します
MAX                      | 引数リストに含まれる最大値を返します
MAXA                     | 数値、文字列、および論理値を含む引数リストから最大値を返します
MAXIFS                   | 条件セットで指定されたセルの中の最大値を返します
MDETERM                  | 配列の行列式を返します
MDURATION                | 額面価格を $100 と仮定して、証券に対する修正済マコーレー デュレーションを返します
MEDIAN                   | 指定された数値のメジアン (中央値) を返します
MID                      | 文字列の任意の位置から指定された文字数の文字を返します
MIDB                     | 文字列の任意の位置から指定された文字数の文字を返します
MIN                      | 引数リストに含まれる最小値を返します
MINIFS                   | 条件セットで指定されたセルの中の最小値を返します
MINA                     | 数値、文字列、および論理値を含む引数リストから最小値を返します
MINUTE                   | シリアル値を時刻の分に変換します
MINVERSE                 | 配列の逆行列を返します
MIRR                     | 支払い (負の値) と収益 (正の値) のキャッシュ フローがさまざまな率で行われる場合の修正内部利益率を返します
MMULT                    | 2 つの配列の行列積を返します
MOD                      | 除算の剰余を返します
MODE                     | 最も頻繁に出現する値 (最頻値) を返します。これは Excel 2007 では、統計関数になります
MODE.MULT                | 配列またはセル範囲として指定されたデータの中で、最も頻繁に出現する値 (最頻値) を縦方向の配列として返します
MODE.SNGL                | 最も頻繁に出現する値 (最頻値) を返します
MONTH                    | シリアル値を月に変換します
MROUND                   | 指定された値の倍数になるように、数値を四捨五入します
MULTINOMIAL              | 指定された複数の数値の多項係数を返します
MUNIT                    | 指定された次元の単位行列を返します
N                        | 値を数値に変換します
NA                       | エラー値 #N/A を返します
NEGBINOM.DIST            | 負の二項分布を返します
NEGBINOMDIST             | 負の二項分布を返します。これは Excel 2007 では、統計関数になります
NETWORKDAYS              | 2 つの日付間の稼働日の日数を返します
NETWORKDAYS.INTL         | 週末がどの曜日で何日間あるかを示すパラメーターを使用して、2 つの日付間にある稼働日の日数を返します
NOMINAL                  | 名目年利率を返します
NORM.DIST                | 正規分布の累積分布の値を返します
NORMDIST                 | 正規分布の累積分布の値を返します。これは Excel 2007 では、統計関数になります
NORMINV                  | 正規分布の累積分布の逆関数値を返します
NORM.INV                 | 正規分布の累積分布の逆関数値を返します。注: これは Excel 2007 では、統計関数になります
NORM.S.DIST              | 標準正規分布の累積分布の値を返します
NORMSDIST                | 標準正規分布の累積分布の値を返します。これは Excel 2007 では、統計関数になります
NORM.S.INV               | 標準正規分布の累積分布の逆関数値を返します
NORMSINV                 | 標準正規分布の累積分布の逆関数値を返します。これは Excel 2007 では、統計関数になります
NOT                      | 引数の論理値を逆にして返します
NOW                      | 現在の日付と時刻に対応するシリアル値を返します
NPER                     | 投資に必要な期間を返します
NPV                      | 定期的に発生する一連のキャッシュ フローと割引率に基づいて、投資の正味現在価値を返します
OCT2BIN                  | 8 進数を 2 進数に変換します
OCT2DEC                  | 8 進数を 10 進数に変換します
OCT2HEX                  | 8 進数を 16 進数に変換します
ODD                      | 指定された数値を最も近い奇数に切り上げた値を返します
ODDFPRICE                | 1 期目の日数が半端な証券に対して、額面 $100 あたりの価格を返します
ODDFYIELD                | 1 期目の日数が半端な証券の利回りを返します
ODDLPRICE                | 最終期の日数が半端な証券に対して、額面 $100 あたりの価格を返します
ODDLYIELD                | 最終期の日数が半端な証券の利回りを返します
OR                       | いずれかの引数が TRUE のときに TRUE を返します
PDURATION                | 投資が指定した価値に達するまでの投資期間を返します
PEARSON                  | ピアソンの積率相関係数 r の値を返します
PERCENTILE.EXC           | 特定の範囲に含まれるデータの第 k 百分位数に当たる値を返します (k は 0 より大きく 1 より小さい値)
PERCENTILE.INC           | 特定の範囲に含まれるデータの第 k 百分位数に当たる値を返します
PERCENTILE               | 特定の範囲に含まれるデータの第 k 百分位数に当たる値を返します。これは Excel 2007 では、統計関数になります
PERCENTRANK.EXC          | データ セット内での値の順位を百分率 (0 より大きく 1 より小さい) で表した値を返します
PERCENTRANK.INC          | データ セット内での値の順位を百分率で表した値を返します
PERCENTRANK              | データ セット内での値の順位を百分率で表した値を返します。これは Excel 2007 では、統計関数になります
PERMUT                   | 指定された個数のオブジェクトを選択するときの順列の数を返します
PERMUTATIONA             | すべてのオブジェクトから指定された数のオブジェクト (繰り返しを含む) を選択する場合の順列の数を返します
PHI                      | 標準正規分布の密度関数の値を返します
PI                       | 円周率 π を返します
PMT                      | 年間の定期支払額を算出します
POISSON.DIST             | ポワソン分布の値を返します
POISSON                  | ポワソン分布の値を返します。これは Excel 2007 では、統計関数になります
POWER                    | 数値のべき乗を返します
PPMT                     | 指定した期に支払われる投資元金を返します
PRICE                    | 定期的に利息が支払われる証券に対して、額面 $100 あたりの価格を返します
PRICEDISC                | 割引証券の額面 $100 あたりの価格を返します
PRICEMAT                 | 満期日に利息が支払われる証券に対して、額面 $100 あたりの価格を返します
PROB                     | 指定した範囲に含まれる値が上限と下限との間に収まる確率を返します
PRODUCT                  | 引数を乗算します
PROPER                   | 文字列に含まれる英単語の先頭文字だけを大文字に変換します
PV                       | 投資の現在価値を返します
QUARTILE                 | データ セットの四分位数を返します。これは Excel 2007 では、統計関数になります
QUARTILE.EXC             | 0 より大きく 1 より小さい百分位値に基づいて、データ セットに含まれるデータから四分位数を返します
QUARTILE.INC             | データ セットの四分位数を返します
QUOTIENT                 | 除算の商の整数部を返します
RADIANS                  | 度をラジアンに変換します
RAND                     | 0 から 1 の乱数を返します
RANDBETWEEN              | 指定された範囲内の数値の乱数を返します
RANK.EQ                  | 数値のリストの中で、指定した数値の順位を返します
RANK                     | 数値のリストの中で、指定した数値の順位を返します。これは Excel 2007 では、統計関数になります
RATE                     | 年間の投資金利を返します
RECEIVED                 | 全額投資された証券に対して、満期日に支払われる金額を返しま
REPLACE                  | テキスト内の文字を置き換えます
REPLACEB                 | テキスト内の文字を置き換えます
REPT                     | テキストを指定した回数だけ繰り返します
RIGHT                    | 文字列の末尾 (右端) から指定された文字数の文字を返します
RIGHTB                   | 文字列の末尾 (右端) から指定された文字数の文字を返します
ROMAN                    | アラビア数字を、ローマ数字を表す文字列に変換します
ROUND                    | 数値を四捨五入して指定された桁数にします
ROUNDDOWN                | 数値を指定された桁数で切り捨てます
ROUNDUP                  | 数値を指定された桁数で切り上げます
ROW                      | セル参照の行番号を返します
ROWS                     | 指定の範囲に含まれる行数を返します
RRI                      | 投資の成長に対する等価利率を返します
RSQ                      | ピアソンの積率相関係数の 2 乗値を返します
SEARCH                   | 大文字と小文字は区別されません
SEARCHB                  | 大文字と小文字は区別されません
SEC                      | 角度の正割 (セカント) を返します
SECH                     | 角度の双曲線正割を返します
SECOND                   | シリアル値を秒に変換します
SERIESSUM                | 数式で定義されるべき級数の和を返します
SHEET                    | 参照先のシートのシート番号を返します
SHEETS                   | 参照内のシート数を返します
SIGN                     | 数値の符号を返します
SIN                      | 指定された角度のサインを返します
SINH                     | 数値の双曲線正弦を返します
SKEW                     | 分布の歪度を返します
SKEW.P                   | 母集団に基づく分布の歪度を取得します。歪度とは、分布の平均値周辺での両側の非対称度を表す値です
SLN                      | 定額法 (Straight-line Method) を使用して、資産の 1 期あたりの減価償却費を返します
SLOPE                    | 回帰直線の傾きを返します
SMALL                    | 指定されたデータ セットの中で k 番目に小さなデータを返します
SORTBY                   | SORTBY 関数は、範囲または配列の内容を、対応する範囲または配列の値に基づいて並べ替えます
SQRT                     | 正の平方根を返します
SQRTPI                   | (数値 * π) の平方根を返します
STANDARDIZE              | 正規化された値を返します
STDEV                    | 標本に基づく標準偏差の推定値を返します
STDEV.P                  | 母集団全体に基づいて、標準偏差を計算します
STDEV.S                  | 標本に基づく標準偏差の推定値を返します
STDEVA                   | 数値、文字列、および論理値を含む標本に基づいて、標準偏差の推定値を返します
STDEVP                   | 母集団全体に基づいて、標準偏差を計算します。これは Excel 2007 では、統計関数になります
STDEVPA                  | 数値、文字列、および論理値を含む母集団全体に基づいて、標準偏差を計算します
STEYX                    | 回帰直線上の予測値の標準誤差を返します
SUBSTITUTE               | 文字列中の指定された文字を他の新しい文字に置き換えます
SUBTOTAL                 | リストまたはデータベースの集計値を返します
SUM                      | 引数を合計します
SUMIF                    | 指定された検索条件に一致するセルの値を合計します
SUMIFS                   | セル範囲内で、複数の検索条件を満たすセルの値を合計します
SUMPRODUCT               | 指定された配列で対応する要素の積を合計します
SUMSQ                    | 引数の 2 乗の和 (平方和) を返します
SUMX2MY2                 | 2 つの配列で対応する配列要素の平方差を合計します
SUMX2PY2                 | 2 つの配列で対応する配列要素の平方和を合計します
SUMXMY2                  | 指定した2つの配列内の対応する配列要素の差を2乗して合計して返します
SWITCH                   | 値の一覧に対して式を評価し、最初に一致する値に対応する結果を返します。いずれにも一致しない場合は、任意指定の既定値が返されます
SYD                      | 級数法 (Sum-of-Year's Digits Method) を使用して、特定の期における減価償却費を返します
T                        | 引数をテキストに変換します
TAN                      | 数値の正接 (タンジェント) を返します
TANH                     | 数値の双曲線正接を返します
TBILLEQ                  | 米国財務省短期証券 (TB) の債券換算利回りを返します
TBILLPRICE               | 米国財務省短期証券 (TB) の額面 $100 あたりの価格を返します
TBILLYIELD               | 米国財務省短期証券 (TB) の利回りを返します
T.DIST                   | スチューデントの t 分布のパーセンテージ (確率) を返します
T.DIST.2T                | スチューデントの t 分布のパーセンテージ (確率) を返します
T.DIST.RT                | スチューデントの t 分布の値を返します
TDIST                    | スチューデントの t 分布の値を返します
TEXT                     | 数値を、書式設定したテキストに変換します
TEXTAFTER                | 指定された文字または文字列の後に出現するテキストを返します
TEXTBEFORE               | 指定した文字または文字列の前に出現するテキストを返します
TEXTJOIN                 | 複数の範囲や文字列のテキストを結合す
TIME                     | 指定した時刻に対応するシリアル値を返します
TIMEVALUE                | 時刻を表す文字列をシリアル値に変換します
T.INV                    | スチューデントの t 分布の t 値を、確率の関数と自由度で返します
T.INV.2T                 | スチューデントの t 分布の逆関数値を返します
TINV                     | スチューデントの t 分布の逆関数値を返します
TODAY                    | 現在の日付に対応するシリアル値を返します
TRANSPOSE                | 指定したセル範囲のデータの行と列を入れ替えた配列を返します
TREND                    | 回帰直線による予測値を配列で返します
TRIM                     | テキストからスペースを削除します
TRIMMEAN                 | データ セットの中間項の平均を返します
TRUE                     | 論理値 TRUE を返します
TRUNC                    | 数値の小数部を切り捨てて整数にします
T.TEST                   | スチューデントの t 検定における確率を返します
TTEST                    | スチューデントの t 検定における確率を返します，これは Excel 2007 では、統計関数になります
TYPE                     | 値のデータ型を表す数値を返します
UNICHAR                  | 指定された数値により参照される Unicode 文字を返します
UNICODE                  | 文字列の最初の文字に対応する番号 (コード ポイント) を返します
UNIQUE                   | リストまたは範囲内の一意の値のリストを返します
UPPER                    | 文字列に含まれる英字をすべて大文字に変換します
VALUE                    | テキスト引数を数値に変換します
VALUETOTEXT              | 指定した値からテキストを返します
VAR                      | 標本に基づいて、分散の推定値を返します。これは Excel 2007 では、統計関数になります
VAR.P                    | 母集団全体に基づいて、分散を計算します
VAR.S                    | 標本に基づいて、分散の推定値を返します
VARA                     | 数値、文字列、および論理値を含む標本に基づいて、分散の推定値を返します
VARP                     | 母集団全体に基づいて、分散を計算します。これは Excel 2007 では、統計関数になります
VARPA                    | 数値、文字列、および論理値を含む母集団全体に基づいて、分散を計算します
VDB                      | 定率法 (declining Balance Method) を利用して、特定の期または部分的な期における資産の減価償却費を返します
VLOOKUP                  | 配列の左端列で特定の値を検索し、その行内で移動して、対応するセルの値を返します
WEEKDAY                  | シリアル値を曜日に変換します
WEEKNUM                  | シリアル値をその年の何週目に当たるかを示す値に変換します
WEIBULL                  | 数値、文字列、および論理値を含む母集団全体に基づいて、分散を計算します。これは Excel 2007 では、統計関数になります
WEIBULL.DIST             | ワイブル分布の値を返します
WORKDAY                  | 指定した稼動日数だけ前または後の日付に対応するシリアル値を返します
WORKDAY.INTL             | 週末がどの曜日で何日間あるかを示すパラメーターを使用して、指定した稼働日数だけ前または後の日付に対応するシリアル値を返します
XIRR                     | 定期的でないキャッシュ フローの特定のスケジュールに対する内部利益率を返します
XLOOKUP                  | Office 365 ボタン  範囲または配列を検索し、最初に見つかった一致に対応する項目を返します。一致するものがない場合、XLOOKUP は最も近い (近似) 一致を返します
XNPV                     | 定期的でないキャッシュ フローの特定のスケジュールに対する正味現在価値を返します
XOR                      | すべての引数の論理排他 OR を返します
YEAR                     | シリアル値を年に変換します
YEARFRAC                 | 開始日と終了日を指定して、その間の期間が 1 年間に対して占める割合を返します
YIELD                    | 利息が定期的に支払われる証券の利回りを返します
YIELDDISC                | 米国財務省短期証券 (TB) などの割引債の年利回りを返します
YIELDMAT                 | 満期日に利息が支払われる証券の利回りを返します
Z.TEST                   | Z 検定の片側確率の値を返します
ZTEST                    | Z 検定の片側確率の値を返します。これは Excel 2007 では、統計関数になります
