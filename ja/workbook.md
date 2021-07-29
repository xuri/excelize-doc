# ワークブック

Options は、開いているスプレッドシートのオプションを定義します。

```go
type Options struct {
    Password string
}
```

## Excel 文書を作成する {#NewFile}

```go
func NewFile() *File
```

`NewFile` を使って新しいExcelワークブックを作成します。新しく作成されたワークブックにはデフォルトで `Sheet1` という名前のワークシートが含まれます。

## 開く {#OpenFile}

```go
func OpenFile(filename string, opt ...Options) (*File, error)
```

既存の Excel 文書を `OpenFile` で開きます。たとえば、パスワード保護された開いているスプレッドシート:

```go
f, err := excelize.OpenFile("Book1.xlsx", excelize.Options{Password: "password"})
if err != nil {
    return
}
```

現在、Excelize は復号化のみをサポートしており、暗号化はサポートしていません。[`Save()`](workbook.md#Save) および [`SaveAs()`](workbook.md#SaveAs) で保存されたスプレッドシートは、パスワードなしで保護されていません。

## データストリームを開く {#OpenReader}

```go
func OpenReader(r io.Reader, opt ...Options) (*File, error)
```

OpenReaderは `io.Reader` からデータストリームを読み取り、入力されたスプレッドシートファイルを返します。

たとえば、アップロードテンプレートを処理するHTTPサーバーを作成してから、新しいワークシートが追加された応答ダウンロードファイルを作成します:

```go
package main

import (
    "fmt"
    "net/http"

    "github.com/xuri/excelize/v2"
)

func process(w http.ResponseWriter, req *http.Request) {
    file, _, err := req.FormFile("file")
    if err != nil {
        fmt.Fprintf(w, err.Error())
        return
    }
    defer file.Close()
    f, err := excelize.OpenReader(file)
    if err != nil {
        fmt.Fprintf(w, err.Error())
        return
    }
    f.NewSheet("NewSheet")
    w.Header().Set("Content-Disposition", "attachment; filename=Book1.xlsx")
    w.Header().Set("Content-Type", req.Header.Get("Content-Type"))
    if _, err := f.WriteTo(w); err != nil {
        fmt.Fprintf(w, err.Error())
    }
    return
}

func main() {
    http.HandleFunc("/process", process)
    http.ListenAndServe(":8090", nil)
}
```

cURLを使用してテストします:

```bash
curl --location --request GET 'http://127.0.0.1:8090/process' \
--form 'file=@/tmp/template.xlsx' -O -J
curl: Saved to filename 'Book1.xlsx'
```

## 保存 {#Save}

```go
func (f *File) Save() error
```

Excel 文書に編集内容を保存するには `Save` を使います。

## 名前を付けて保存 {#SaveAs}

```go
func (f *File) SaveAs(name string) error
```

指定したファイルとして Excel 文書を保存するには `SaveAs` を使います。

## ワークシートを作成する {#NewSheet}

```go
func (f *File) NewSheet(name string) int
```

NewSheet は、ワークシート名を指定して新しいシートを作成する関数を提供し、ワークブック（スプレッドシート）に追加された後のシートのインデックスを返します。新しいスプレッドシートファイルを作成すると、`Sheet1`という名前のデフォルトのワークシートが作成されることに注意してください。

## ワークシートを削除する {#DeleteSheet}

```go
func (f *File) DeleteSheet(name string)
```

指定されたワークシート名に基づいて指定されたワークシートを削除する場合は、この方法を慎重に使用してください。削除するワークシートに関連付けられている数式、参照、グラフ、その他の要素に影響します。削除されたワークシートの値を参照する他のコンポーネントがあると、エラーが発生し、ワークブックも開くことができません。 ワークブックにワークシートが1つしか含まれていない場合、このメソッドを呼び出しても効果はありません。

## ワークシートをコピーする {#CopySheet}

```go
func (f *File) CopySheet(from, to int) error
```

与えられた複製ワークシートおよびターゲットワークシートインデックスコピーワークシートに従って、ターゲットワークシートインデックスはそれが既に存在するかどうかを確認するために開発者を必要とします。セル値と数式のみを含むワークシート間の複製は現在サポートされています。テーブル、イメージ、チャート、ピボットテーブルなどの要素を含むワークシート間の複製はサポートされていません。

```go
// Sheet1 という名前のワークシートは既に存在します ...
index := f.NewSheet("Sheet2")
err := f.CopySheet(1, index)
return err
```

## ワークシートの背景 {#SetSheetBackground}

```go
func (f *File) SetSheetBackground(sheet, picture string) error
```

指定されたシート名と画像アドレスに基づいて、指定されたワークシートのタイリング効果の背景画像を設定します。

## デフォルトワークシートを設定する {#SetActiveSheet}

```go
func (f *File) SetActiveSheet(index int)
```

SetActiveSheet は、指定されたインデックスによってワークブックのデフォルトのアクティブシートを設定する関数を提供します。 アクティブなインデックスは、[`GetSheetMap`](sheet.md#GetSheetMap) 関数によって返されるIDとは異なることに注意してください。`0` 以上で、ワークシートの総数よりも少ない必要があります。

## アクティブシートインデックスを取得する {#GetActiveSheetIndex}

```go
func (f *File) GetActiveSheetIndex() int
```

デフォルトのワークシートのインデックスを取得します。デフォルトのワークシートが見つからない場合は、`0` を返します。

## ワークシートの表示設定 {#SetSheetVisible}

```go
func (f *File) SetSheetVisible(name string, visible bool) error
```

SetSheetVisible は、与えられたワークシート名でワークシートを見えるように設定する機能を提供します。 ワークブックには少なくとも1つの表示可能なワークシートが含まれている必要があります。 指定したワークシートがアクティブになっている場合、この設定は無効になります。[SheetStateValues Enum](https://docs.microsoft.com/ja-jp/dotnet/api/documentformat.openxml.spreadsheet.sheetstatevalues?view=openxml-2.8.1) で定義されているシート状態値:

|ワークシート状態値|
|---|
|visible|
|hidden|
|veryHidden|

例えば `Sheet1` を隠す:

```go
err := f.SetSheetVisible("Sheet1", false)
```

## ワークシートの表示設定を取得する {#GetSheetVisible}

```go
func (f *File) GetSheetVisible(name string) bool
```

GetSheetVisible は、与えられたワークシート名でワークシートを見えるようにする機能を提供します。 たとえば、`Sheet1` の可視状態を取得します。

```go
f.GetSheetVisible("Sheet1")
```

## ワークシート形式のプロパティを設定する {#SetSheetFormatPr}

```go
func (f *File) SetSheetFormatPr(sheet string, opts ...SheetFormatPrOptions) error
```

SetSheetFormatPr は、ワークシートのフォーマットプロパティを設定する関数を提供します。

利用可能なオプション：

オプションのフォーマットパラメータ|タイプ
---|---
BaseColWidth | uint8
DefaultColWidth | float64
DefaultRowHeight | float64
CustomHeight | bool
ZeroHeight | bool
ThickTop | bool
ThickBottom | bool

たとえば、ワークシートの行をデフォルトで非表示にします。

<p align="center"><img width="612" src="./images/sheet_format_pr_01.png" alt="ワークシート形式のプロパティを設定する"></p>

```go
f := excelize.NewFile()
const sheet = "Sheet1"
if err := f.SetSheetFormatPr("Sheet1", excelize.ZeroHeight(true)); err != nil {
    fmt.Println(err)
}
if err := f.SetRowVisible("Sheet1", 10, true); err != nil {
    fmt.Println(err)
}
f.SaveAs("Book1.xlsx")
```

## ワークシート形式のプロパティを取得する {#GetSheetFormatPr}

```go
func (f *File) GetSheetFormatPr(sheet string, opts ...SheetFormatPrOptionsPtr) error
```

GetSheetFormatPr は、ワークシートのフォーマットプロパティを取得する関数を提供します。

利用可能なオプション：

オプションのフォーマットパラメータ|タイプ
---|---
BaseColWidth | uint8
DefaultColWidth | float64
DefaultRowHeight | float64
CustomHeight | bool
ZeroHeight | bool
ThickTop | bool
ThickBottom | bool

例えば：

```go
f := excelize.NewFile()
const sheet = "Sheet1"

var (
    baseColWidth     excelize.BaseColWidth
    defaultColWidth  excelize.DefaultColWidth
    defaultRowHeight excelize.DefaultRowHeight
    customHeight     excelize.CustomHeight
    zeroHeight       excelize.ZeroHeight
    thickTop         excelize.ThickTop
    thickBottom      excelize.ThickBottom
)

if err := f.GetSheetFormatPr(sheet,
    &baseColWidth,
    &defaultColWidth,
    &defaultRowHeight,
    &customHeight,
    &zeroHeight,
    &thickTop,
    &thickBottom,
); err != nil {
    fmt.Println(err)
}
fmt.Println("Defaults:")
fmt.Println("- baseColWidth:", baseColWidth)
fmt.Println("- defaultColWidth:", defaultColWidth)
fmt.Println("- defaultRowHeight:", defaultRowHeight)
fmt.Println("- customHeight:", customHeight)
fmt.Println("- zeroHeight:", zeroHeight)
fmt.Println("- thickTop:", thickTop)
fmt.Println("- thickBottom:", thickBottom)
```

出力を取得する：

```text
Defaults:
- baseColWidth: 0
- defaultColWidth: 0
- defaultRowHeight: 15
- customHeight: false
- zeroHeight: false
- thickTop: false
- thickBottom: false
```

## ワークシートビューのプロパティを設定する {#SetSheetViewOptions}

```go
func (f *File) SetSheetViewOptions(name string, viewIndex int, opts ...SheetViewOption) error
```

SetSheetViewOptions は、シートビューオプションを設定します。`viewIndex` は負の場合があり、その場合は逆方向にカウントされます（`-1` は最後のビューです）。

利用可能なオプション：

オプションのビューパラメータ|タイプ
---|---
DefaultGridColor|bool
RightToLeft|bool
ShowFormulas|bool
ShowGridLines|bool
ShowRowColHeaders|bool
ZoomScale|float64
TopLeftCell|string
ShowZeros|bool

- 例1:

```go
err = f.SetSheetViewOptions("Sheet1", -1, ShowGridLines(false))
```

- 例2:

```go
f := excelize.NewFile()
const sheet = "Sheet1"

if err := f.SetSheetViewOptions(sheet, 0,
    excelize.DefaultGridColor(false),
    excelize.RightToLeft(false),
    excelize.ShowFormulas(true),
    excelize.ShowGridLines(true),
    excelize.ShowRowColHeaders(true),
    excelize.ZoomScale(80),
    excelize.TopLeftCell("C3"),
); err != nil {
    fmt.Println(err)
}

var zoomScale excelize.ZoomScale
fmt.Println("Default:")
fmt.Println("- zoomScale: 80")

if err := f.SetSheetViewOptions(sheet, 0, excelize.ZoomScale(500)); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &zoomScale); err != nil {
    fmt.Println(err)
}

fmt.Println("Used out of range value:")
fmt.Println("- zoomScale:", zoomScale)

if err := f.SetSheetViewOptions(sheet, 0, excelize.ZoomScale(123)); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &zoomScale); err != nil {
    fmt.Println(err)
}

fmt.Println("Used correct value:")
fmt.Println("- zoomScale:", zoomScale)
```

出力を取得する：

```text
Default:
- zoomScale: 80
Used out of range value:
- zoomScale: 80
Used correct value:
- zoomScale: 123
```

## ワークシートビュープロパティを取得する {#GetSheetViewOptions}

```go
func (f *File) GetSheetViewOptions(name string, viewIndex int, opts ...SheetViewOptionPtr) error
```

指定されたワークシート名、ビューインデックスの取得、およびビューパラメータに基づくワークシートビューのプロパティ，`viewIndex`は負の数にすることができ、もしそうなら、逆方向に数えます（`-1` は最後のビューを表します）。

オプションのビューパラメータ|タイプ
---|---
DefaultGridColor|bool
RightToLeft|bool
ShowFormulas|bool
ShowGridLines|bool
ShowRowColHeaders|bool
ZoomScale|float64
TopLeftCell|string
ShowZeros|bool

- 例1、`Sheet1` という名前のワークシートの最後のビューのグリッド線プロパティ設定を取得します。

```go
var showGridLines excelize.ShowGridLines
err = f.GetSheetViewOptions("Sheet1", -1, &showGridLines)
```

- 例2：

```go
f := excelize.NewFile()
const sheet = "Sheet1"

var (
    defaultGridColor  excelize.DefaultGridColor
    rightToLeft       excelize.RightToLeft
    showFormulas      excelize.ShowFormulas
    showGridLines     excelize.ShowGridLines
    showZeros         excelize.ShowZeros
    showRowColHeaders excelize.ShowRowColHeaders
    zoomScale         excelize.ZoomScale
    topLeftCell       excelize.TopLeftCell
)

if err := f.GetSheetViewOptions(sheet, 0,
    &defaultGridColor,
    &rightToLeft,
    &showFormulas,
    &showGridLines,
    &showZeros,
    &showRowColHeaders,
    &zoomScale,
    &topLeftCell,
); err != nil {
    fmt.Println(err)
}

fmt.Println("Default:")
fmt.Println("- defaultGridColor:", defaultGridColor)
fmt.Println("- rightToLeft:", rightToLeft)
fmt.Println("- showFormulas:", showFormulas)
fmt.Println("- showGridLines:", showGridLines)
fmt.Println("- showZeros:", showZeros)
fmt.Println("- showRowColHeaders:", showRowColHeaders)
fmt.Println("- zoomScale:", zoomScale)
fmt.Println("- topLeftCell:", `"`+topLeftCell+`"`)

if err := f.SetSheetViewOptions(sheet, 0, excelize.TopLeftCell("B2")); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &topLeftCell); err != nil {
    fmt.Println(err)
}

if err := f.SetSheetViewOptions(sheet, 0, excelize.ShowGridLines(false)); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &showGridLines); err != nil {
    fmt.Println(err)
}

if err := f.SetSheetViewOptions(sheet, 0, excelize.ShowZeros(false)); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &showZeros); err != nil {
    fmt.Println(err)
}

fmt.Println("After change:")
fmt.Println("- showGridLines:", showGridLines)
fmt.Println("- showZeros:", showZeros)
fmt.Println("- topLeftCell:", topLeftCell)
```

出力を取得する：

```text
Default:
- defaultGridColor: true
- rightToLeft: false
- showFormulas: false
- showGridLines: true
- showZeros: true
- showRowColHeaders: true
- zoomScale: 0
- topLeftCell: ""
After change:
- showGridLines: false
- showZeros: false
- topLeftCell: B2
```

## ワークシートのページレイアウトを設定する {#SetPageLayout}

```go
func (f *File) SetPageLayout(sheet string, opts ...PageLayoutOption) error
```

指定されたワークシート名とページレイアウトパラメータに基づいて、ワークシートのページレイアウトプロパティを設定します。 現在設定でサポートされているページレイアウトプロパティ:

- `BlackAndWhite` メソッドを使用してモノクロ印刷 true または false を設定し、既定値は false オフです。

- `FirstPageNumber` メソッドを使用して、ページの開始ページ番号を自動に設定します。

- ページレイアウトの方向は `PageLayoutOrientation` メソッドによって設定され、デフォルトのページレイアウトの方向は「縦」です。 次の表は Excelize のページレイアウト指示の `PageLayoutOrientation` パラメータのリストです：

パラメータ|方向
---|---
OrientationPortrait | 縦
OrientationLandscape | 横

- `PageLayoutPaperSize` メソッドでページの用紙サイズを設定するデフォルトのページレイアウトサイズは「レター用紙 8 1/2 × 11 インチ」です。次の表は Excelize のページレイアウトサイズとインデックスの `PageLayoutPaperSize `パラメータの比較です。

インデックス|用紙サイズ
---|---
1   | レター 8 1/2 × 11 インチ
2   | Letter Small 8 1/2 × 11 インチ
3   | タブロイド 11 × 17 インチ
4   | Ledger 17 × 11 インチ
5   | リーガル紙 8 1/2 × 14 インチ
6   | 声明紙 5 1/2 × 8 1/2 インチ
7   | 行政書用紙 7 1/2 × 10 インチ
8   | A3 297 × 420 mm
9   | A4 210 × 297 mm
10  | A4 小さい紙 210 × 297 mm
11  | A5 148 × 210 mm
12  | B4 250 × 353 mm
13  | B5 176 × 250 mm
14  | フォリオ紙 8 1/2 × 13 インチ
15  | 四分紙 215 × 275 mm
16  | アメリカ標準紙 10 × 14 インチ
17  | アメリカ標準紙 11 × 17 インチ
18  | Note paper 8.5 × 11 インチ
19  | 封筒 #9 3.875 × 8.875 インチ
20  | 封筒 #10 4-1/8 × 9 1/2 インチ
21  | 封筒 #11 4.5 × 10.375 インチ
22  | 封筒 #12 4.75 × 11 インチ
23  | 封筒 #14 5 × 11.5 インチ
24  | C paper 17 × 22 インチ
25  | D paper 22 × 34 インチ
26  | E paper 34 × 44 インチ
27  | 封筒 DL 110 × 220 mm
28  | 封筒 C5 162 × 229 mm
29  | 封筒 C3 324 × 458 mm
30  | 封筒 C4 229 × 324 mm
31  | 封筒 C6 114 × 162 mm
32  | 封筒 C65 114 × 229 mm
33  | 封筒 B4 250 × 353 mm
34  | 封筒 B5 176 × 250 mm
35  | 封筒 B6 176 × 125 mm
36  | 封筒 Italy 110 × 230 mm
37  | 君主の封筒 3.88 × 7.5 インチ
38  | 6¾ 封筒 3.625 × 6.5 インチ
39  | US standard fanfold 14.875 × 11 インチ
40  | German standard fanfold 8.5 × 12 インチ
41  | German legal fanfold 8.5 × 13 インチ
42  | ISO B4 250 × 353 mm
43  | 官製はがき 100 × 148 mm
44  | Standard paper 9 × 11 インチ
45  | Standard paper 10 × 11 インチ
46  | Standard paper 15 × 11 インチ
47  | 招待状 220 × 220 mm
50  | Letter extra paper 9.275 × 12 インチ
51  | Legal extra paper 9.275 × 15 インチ
52  | Tabloid extra paper 11.69 × 18 インチ
53  | A4 extra paper 236 × 322 mm
54  | Letter transverse paper 8.275 × 11 インチ
55  | A4 transverse paper 210 × 297 mm
56  | Letter extra transverse paper 9.275 × 12 インチ
57  | SuperA/SuperA/A4 paper 227 × 356 mm
58  | SuperB/SuperB/A3 paper 305 × 487 mm
59  | Letter plus paper 8.5 × 12.69 インチ
60  | A4 plus paper 210 × 330 mm
61  | A5 transverse paper 148 × 210 mm
62  | JIS B5 transverse paper 182 × 257 mm
63  | A3 extra paper 322 × 445 mm
64  | A5 extra paper 174 × 235 mm
65  | ISO B5 extra paper 201 × 276 mm
66  | A2 420 × 594 mm
67  | A3 transverse paper 297 × 420 mm
68  | A3 extra transverse paper 322 × 445 mm
69  | 往復はがき 200 × 148 mm
70  | A6 105 × 148 mm
71  | 日本の封筒 Kaku #2
72  | 日本の封筒 Kaku #3
73  | 日本の封筒 Chou #3
74  | 日本の封筒 Chou #4
75  | Letter Rotated (11 × 8½ in)
76  | A3 横回転 420 × 297 mm
77  | A4 横回転 297 × 210 mm
78  | A5 横回転 210 × 148 mm
79  | B4 (JIS) 横回転 364 × 257 mm
80  | B5 (JIS) 横回転 257 × 182 mm
81  | 官製はがき 横回転 148 × 100 mm
82  | 往復はがき 横回転 148 × 200 mm
83  | A6 横回転 148 × 105 mm
84  | 日本の封筒 Kaku #2 横回転
85  | 日本の封筒 Kaku #3 横回転
86  | 日本の封筒 Chou #3 横回転
87  | 日本の封筒 Chou #4 横回転
88  | B6 (JIS) 128 × 182 mm
89  | B6 (JIS) 横回転 182 × 128 mm
90  | 12 × 11 インチ
91  | 日本の封筒 You #4
92  | 日本の封筒 You #4 横回転
96  | 中国の封筒 #1 102 × 165 mm
97  | 中国の封筒 #2 102 × 176 mm
98  | 中国の封筒 #3 125 × 176 mm
99  | 中国の封筒 #4 110 × 208 mm
100 | 中国の封筒 #5 110 × 220 mm
101 | 中国の封筒 #6 120 × 230 mm
102 | 中国の封筒 #7 160 × 230 mm
103 | 中国の封筒 #8 120 × 309 mm
104 | 中国の封筒 #9 229 × 324 mm
105 | 中国の封筒 #10 324 × 458 mm
109 | 中国の封筒 #1 横回転 165 × 102 mm
110 | 中国の封筒 #2 横回転 176 × 102 mm
111 | 中国の封筒 #3 横回転 176 × 125 mm
112 | 中国の封筒 #4 横回転 208 × 110 mm
113 | 中国の封筒 #5 横回転 220 × 110 mm
114 | 中国の封筒 #6 横回転 230 × 120 mm
115 | 中国の封筒 #7 横回転 230 × 160 mm
116 | 中国の封筒 #8 横回転 309 × 120 mm
117 | 中国の封筒 #9 横回転 324 × 229 mm
118 | 中国の封筒 #10 横回転 458 × 324 mm

- `FitToHeight` メソッドを使用してページの拡大/縮小を設定し、ページの幅を `1` に設定します。

- `FitToWidth` メソッドを使用して、ページのズームを設定してページの高さを調整し、既定値は `1` です。

- `PageLayoutScale` メソッドを使用して、10 ~ 400 の範囲の値、つまり 10 ~ 400% の範囲のページ ズームを設定し、既定値は `100` 標準サイズです。

- たとえば、`Sheet1` という名前のシート ページ レイアウトをモノクロ印刷、開始ページ番号 `2`、横向き、A4 (小) 210 × 297 mm 用紙、2 ページ幅、2 ページの高さ、および 50% のスケーリングに設定します:

```go
f := excelize.NewFile()
if err := f.SetPageLayout(
    "Sheet1",
    excelize.BlackAndWhite(true),
    excelize.FirstPageNumber(2),
    excelize.PageLayoutOrientation(excelize.OrientationLandscape),
    excelize.PageLayoutPaperSize(10),
    excelize.FitToHeight(2),
    excelize.FitToWidth(2),
    excelize.PageLayoutScale(50),
); err != nil {
    fmt.Println(err)
}
```

## ワークシートのページレイアウトを取得する {#GetPageLayout}

```go
func (f *File) GetPageLayout(sheet string, opts ...PageLayoutOptionPtr) error
```

指定されたシート名とページレイアウトパラメータに基づいて、ワークシートのページレイアウトプロパティを取得します。

- `PageLayoutOrientation` メソッドでページレイアウトの方向を取得
- `PageLayoutPaperSize` メソッドでページのページサイズを取得

たとえば、`Sheet1` という名前のワークシートページレイアウト設定を取得します。

```go
f := excelize.NewFile()
const sheet = "Sheet1"
var (
    orientation excelize.PageLayoutOrientation
    paperSize   excelize.PageLayoutPaperSize
)
if err := f.GetPageLayout("Sheet1", &orientation); err != nil {
    fmt.Println(err)
}
if err := f.GetPageLayout("Sheet1", &paperSize); err != nil {
    fmt.Println(err)
}
fmt.Println("Defaults:")
fmt.Printf("- orientation: %q\n", orientation)
fmt.Printf("- paper size: %d\n", paperSize)
```

出力:

```text
Defaults:
- orientation: "portrait"
- paper size: 1
```

## ワークシートのページ余白を設定する {#SetPageMargins}

```go
func (f *File) SetPageMargins(sheet string, opts ...PageMarginsOptions) error
```

SetPageMargins は、ワークシートのページ余白を設定する機能を提供します。利用可能なオプション：

オプション|タイプ
---|---
PageMarginBotom|float64
PageMarginFooter|float64
PageMarginHeader|float64
PageMarginLeft|float64
PageMarginRight|float64
PageMarginTop|float64

- たとえば、`Sheet1` のページマージンを設定します:

```go
f := excelize.NewFile()
const sheet = "Sheet1"

if err := f.SetPageMargins(sheet,
    excelize.PageMarginBottom(1.0),
    excelize.PageMarginFooter(1.0),
    excelize.PageMarginHeader(1.0),
    excelize.PageMarginLeft(1.0),
    excelize.PageMarginRight(1.0),
    excelize.PageMarginTop(1.0),
); err != nil {
    fmt.Println(err)
}
```

## ワークシートのページ余白を取得する {#GetPageMargins}

GetPageMargins は、ワークシートのページ余白を取得する関数を提供します。 利用可能なオプション：

オプション|タイプ
---|---
PageMarginBotom|float64
PageMarginFooter|float64
PageMarginHeader|float64
PageMarginLeft|float64
PageMarginRight|float64
PageMarginTop|float64

- たとえば、`Sheet1` のページマージンを取得します:

```go
f := excelize.NewFile()
const sheet = "Sheet1"

var (
    marginBottom excelize.PageMarginBottom
    marginFooter excelize.PageMarginFooter
    marginHeader excelize.PageMarginHeader
    marginLeft   excelize.PageMarginLeft
    marginRight  excelize.PageMarginRight
    marginTop    excelize.PageMarginTop
)

if err := f.GetPageMargins(sheet,
    &marginBottom,
    &marginFooter,
    &marginHeader,
    &marginLeft,
    &marginRight,
    &marginTop,
); err != nil {
    fmt.Println(err)
}
fmt.Println("Defaults:")
fmt.Println("- marginBottom:", marginBottom)
fmt.Println("- marginFooter:", marginFooter)
fmt.Println("- marginHeader:", marginHeader)
fmt.Println("- marginLeft:", marginLeft)
fmt.Println("- marginRight:", marginRight)
fmt.Println("- marginTop:", marginTop)
```

出力:

```text
Defaults:
- marginBottom: 0.75
- marginFooter: 0.3
- marginHeader: 0.3
- marginLeft: 0.7
- marginRight: 0.7
- marginTop: 0.75
```

## ヘッダとフッタを設定する {#SetHeaderFooter}

```go
func (f *File) SetHeaderFooter(sheet string, settings *FormatHeaderFooter) error
```

SetHeaderFooter は、与えられたワークシート名と制御文字によってヘッダーとフッターを設定する機能を提供します。

ヘッダーとフッターは、次の設定フィールドを使って指定します。

Fields           | Description
---|---
AlignWithMargins | Align header footer margins with page margins
DifferentFirst   | Different first-page header and footer indicator
DifferentOddEven | Different odd and even page headers and footers indicator
ScaleWithDoc     | Scale header and footer with document scaling
OddFooter        | Odd Page Footer
OddHeader        | Odd Header
EvenFooter       | Even Page Footer
EvenHeader       | Even Page Header
FirstFooter      | First Page Footer
FirstHeader      | First Page Header

以下のフォーマットコードは、6 つの文字列型フィールドで使用できます。`OddHeader`, `OddFooter`, `EvenHeader`, `EvenFooter`, `FirstFooter`, `FirstHeader`

<table>
    <thead>
        <tr>
            <th>Formatting Code</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>&amp;&amp;</code></td>
            <td>The character &quot;&amp;&quot;</td>
        </tr>
        <tr>
            <td><code>&amp;font-size</code></td>
            <td>Size of the text font, where font-size is a decimal font size in points</td>
        </tr>
        <tr>
            <td><code>&amp;&quot;font name,font type&quot;</code></td>
            <td>A text font-name string, font name, and a text font-type string, font type</td>
        </tr>
        <tr>
            <td><code>&amp;&quot;-,Regular&quot;</code></td>
            <td>Regular text format. Toggles bold and italic modes to off</td>
        </tr>
        <tr>
            <td><code>&amp;A</code></td>
            <td>Current worksheet&#39;s tab name</td>
        </tr>
        <tr>
            <td><code>&amp;B</code> or <code>&amp;&quot;-,Bold&quot;</code></td>
            <td>Bold text format, from off to on, or vice versa. The default mode is off</td>
        </tr>
        <tr>
            <td><code>&amp;D</code></td>
            <td>Current date</td>
        </tr>
        <tr>
            <td><code>&amp;C</code></td>
            <td>Center section</td>
        </tr>
        <tr>
            <td><code>&amp;E</code></td>
            <td>Double-underline text format</td>
        </tr>
        <tr>
            <td><code>&amp;F</code></td>
            <td>Current workbook&#39;s file name</td>
        </tr>
        <tr>
            <td><code>&amp;G</code></td>
            <td>Drawing object as background</td>
        </tr>
        <tr>
            <td><code>&amp;H</code></td>
            <td>Shadow text format</td>
        </tr>
        <tr>
            <td><code>&amp;I</code> or <code>&amp;&quot;-,Italic&quot;</code></td>
            <td>Italic text format</td>
        </tr>
        <tr>
            <td><code>&amp;K</code></td>
            <td>Text font color<br>An RGB Color is specified as RRGGBB<br>A Theme Color is specified as TTSNNN where TT is the theme color Id, S is either &quot;+&quot; or &quot;-&quot; of the tint/shade value, and NNN is the tint/shade value</td>
        </tr>
        <tr>
            <td><code>&amp;L</code></td>
            <td>Left section</td>
        </tr>
        <tr>
            <td><code>&amp;N</code></td>
            <td>Total number of pages</td>
        </tr>
        <tr>
            <td><code>&amp;O</code></td>
            <td>Outline text format</td>
        </tr>
        <tr>
            <td><code>&amp;P[[+\|-]n]</code></td>
            <td>Without the optional suffix, the current page number in decimal</td>
        </tr>
        <tr>
            <td><code>&amp;R</code></td>
            <td>Right section</td>
        </tr>
        <tr>
            <td><code>&amp;S</code></td>
            <td>Strikethrough text format</td>
        </tr>
        <tr>
            <td><code>&amp;T</code></td>
            <td>Current time</td>
        </tr>
        <tr>
            <td><code>&amp;U</code></td>
            <td>Single-underline text format. If double-underline mode is on, the next occurrence in a section specifier toggles double-underline mode to off; otherwise, it toggles single-underline mode, from off to on, or vice versa. The default mode is off</td>
        </tr>
        <tr>
            <td><code>&amp;X</code></td>
            <td>Superscript text format</td>
        </tr>
        <tr>
            <td><code>&amp;Y</code></td>
            <td>Subscript text format</td>
        </tr>
        <tr>
            <td><code>&amp;Z</code></td>
            <td>Current workbook&#39;s file path</td>
        </tr>
    </tbody>
</table>

例えば：

```go
err := f.SetHeaderFooter("Sheet1", &excelize.FormatHeaderFooter{
    DifferentFirst:   true,
    DifferentOddEven: true,
    OddHeader:        "&R&P",
    OddFooter:        "&C&F",
    EvenHeader:       "&L&P",
    EvenFooter:       "&L&D&R&T",
    FirstHeader:      `&CCenter &"-,Bold"Bold&"-,Regular"HeaderU+000A&D`,
})
```

この例は次のことを示しています:

- 最初のページには独自のヘッダーとフッターがあります
- 奇数ページと偶数ページでヘッダーとフッターが異なる
- 奇数ページヘッダの右側のセクションにある現在のページ番号
- 奇数ページのフッターの中央部分にある現在のワークブックのファイル名
- 偶数ページヘッダの左側のセクションにある現在のページ番号
- 偶数ページのフッターの左側のセクションに現在の日付と右側のセクションに現在の時刻
- 最初のページの中央セクションの1行目のテキスト "Center Bold Header"、および同じページの中央セクションの2行目の日付
- 最初のページにフッターなし

### 名前を設定する {#SetDefinedName}

```go
func (f *File) SetDefinedName(definedName *DefinedName) error
```

与えられた名前とスコープに基づいて名前を設定しますデフォルトのスコープはワークブックです。例えば、

```go
f.SetDefinedName(&excelize.DefinedName{
    Name:     "Amount",
    RefersTo: "Sheet1!$A$2:$D$5",
    Comment:  "defined name comment",
    Scope:    "Sheet2",
})
```

ワークシートの印刷領域と印刷タイトルの設定:

<p align="center"><img width="657" src="./images/page_setup_01.png" alt="ワークシートの印刷領域と印刷タイトルの設定"></p>

```go
f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Area",
    RefersTo: "Sheet1!$A$1:$Z$100",
    Scope:    "Sheet1",
})
f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Titles",
    RefersTo: "Sheet1!$A:$A,Sheet1!$1:$1",
    Scope:    "Sheet1",
})
```

## 名前を取得する {#GetDefinedName}

```go
func (f *File) GetDefinedName() []DefinedName
```

範囲内のワークブックとワークシートの名前のリストを取得します。

## 定義された名前を削除 {#DeleteDefinedName}

```go
func (f *File) DeleteDefinedName(definedName *DefinedName) error
```

DeleteDefinedName は、ワークブックまたはワークシートの定義名を削除する機能を提供します。スコープが指定されていない場合、デフォルトのスコープはワークブックです。例えば：

```go
f.DeleteDefinedName(&excelize.DefinedName{
    Name:     "Amount",
    Scope:    "Sheet2",
})
```

## ブックのプロパティを設定する {#SetDocProps}

```go
func (f *File) SetDocProps(docProperties *DocProperties) error
```

ワークブックのコアプロパティを設定します。設定できるプロパティは次のとおりです:

プロパティ      | 説明
---|---
Title          | リソースに指定された名前。
Subject        | リソースのコンテンツのトピック。
Creator        | 主にリソースのコンテンツを作成するエンティティ。
Keywords       | 検索とインデックス作成をサポートするキーワードの区切られたセット。これは通常、プロパティ内の他の場所では使用できない用語の一覧です。
Description    | リソースの内容の説明。
LastModifiedBy | 最後の変更を実行したユーザー。識別は環境固有です。
Language       | リソースの知的コンテンツの言語。
Identifier     | 特定のコンテキスト内のリソースへの明確な参照。
Revision       | リソースのコンテンツのトピック。
ContentStatus  | コンテンツの状態。たとえば、値には "Draft"、"Reviewed"、および "Final" が含まれる場合があります。
Category       | このパッケージの内容の分類。
Version        | バージョン番号。この値は、ユーザーまたはアプリケーションによって設定されます。

例えば、

```go
err := f.SetDocProps(&excelize.DocProperties{
    Category:       "category",
    ContentStatus:  "Draft",
    Created:        "2019-06-04T22:00:10Z",
    Creator:        "Go Excelize",
    Description:    "This file created by Go Excelize",
    Identifier:     "xlsx",
    Keywords:       "Spreadsheet",
    LastModifiedBy: "Go Author",
    Modified:       "2019-06-04T22:00:10Z",
    Revision:       "0",
    Subject:        "Test Subject",
    Title:          "Test Title",
    Language:       "en-US",
    Version:        "1.0.0",
})
```

## ブックのプロパティを取得する {#GetDocProps}

```go
func (f *File) GetDocProps() (*DocProperties, error)
```

ワークブックのコアとなるプロパティを取得してください。
