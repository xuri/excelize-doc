# ワークブック

## Excel 文書を作成する {#NewFile}

```go
func NewFile() *File
```

`NewFile` を使って新しいExcelワークブックを作成します。新しく作成されたワークブックにはデフォルトで `Sheet1` という名前のワークシートが含まれます。

## 開く {#OpenFile}

```go
func OpenFile(filename string) (*File, error)
```

既存の Excel 文書を `OpenFile` で開きます。

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

指定されたワークシート名に基づいて新しいワークシートを追加し、ワークシートのインデックスを返します。新しく作成されたワークブックは `Sheet1` と呼ばれるデフォルトのワークブックを含みます。

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

デフォルトワークシートは与えられたインデックス値に従って設定され、インデックスの値は `0` より大きくワークブックに含まれる累積ワークシートの総数よりも小さくなければなりません。

## アクティブシートインデックスを取得する {#GetActiveSheetIndex}

```go
func (f *File) GetActiveSheetIndex() int
```

デフォルトのワークシートのインデックスを取得します。デフォルトのワークシートが見つからない場合は、`0` を返します。

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

- 例1、`Sheet1` という名前のワークシートの最後のビューのグリッド線プロパティ設定を取得します。

```go
var showGridLines excelize.ShowGridLines
err = f.GetSheetViewOptions("Sheet1", -1, &showGridLines)
```

- 例2：

```go
xl := excelize.NewFile()
const sheet = "Sheet1"

var (
    defaultGridColor  excelize.DefaultGridColor
    rightToLeft       excelize.RightToLeft
    showFormulas      excelize.ShowFormulas
    showGridLines     excelize.ShowGridLines
    showRowColHeaders excelize.ShowRowColHeaders
    zoomScale         excelize.ZoomScale
    topLeftCell       excelize.TopLeftCell
)

if err := xl.GetSheetViewOptions(sheet, 0,
    &defaultGridColor,
    &rightToLeft,
    &showFormulas,
    &showGridLines,
    &showRowColHeaders,
    &zoomScale,
    &topLeftCell,
); err != nil {
    panic(err)
}

fmt.Println("Default:")
fmt.Println("- defaultGridColor:", defaultGridColor)
fmt.Println("- rightToLeft:", rightToLeft)
fmt.Println("- showFormulas:", showFormulas)
fmt.Println("- showGridLines:", showGridLines)
fmt.Println("- showRowColHeaders:", showRowColHeaders)
fmt.Println("- zoomScale:", zoomScale)
fmt.Println("- topLeftCell:", `"`+topLeftCell+`"`)

if err := xl.SetSheetViewOptions(sheet, 0, excelize.TopLeftCell("B2")); err != nil {
    panic(err)
}

if err := xl.GetSheetViewOptions(sheet, 0, &topLeftCell); err != nil {
    panic(err)
}

if err := xl.SetSheetViewOptions(sheet, 0, excelize.ShowGridLines(false)); err != nil {
    panic(err)
}

if err := xl.GetSheetViewOptions(sheet, 0, &showGridLines); err != nil {
    panic(err)
}

fmt.Println("After change:")
fmt.Println("- showGridLines:", showGridLines)
fmt.Println("- topLeftCell:", topLeftCell)
```

出力を取得する：

```text
Default:
- defaultGridColor: true
- rightToLeft: false
- showFormulas: false
- showGridLines: true
- showRowColHeaders: true
- zoomScale: 0
- topLeftCell: ""
After change:
- showGridLines: false
- topLeftCell: B2
```

## ワークシートのページレイアウトを設定する {#SetPageLayout}

```go
func (f *File) SetPageLayout(sheet string, opts ...PageLayoutOption) error
```

指定されたワークシート名とページレイアウトパラメータに基づいて、ワークシートのページレイアウトプロパティを設定します。 現在設定でサポートされているページレイアウトプロパティ:

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
38  | 封筒 6 3/4 3.625 × 6.5 インチ
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
75  | Letter Rotated (11in x 8 1/2 11 in)
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

- たとえば、`Sheet1` という名前のワークシートページレイアウトを横に設定し、A4 小さい 210 × 297 mm 紙を使用します。

```go
xl := excelize.NewFile()
const sheet = "Sheet1"

if err := xl.SetPageLayout(
    "Sheet1",
    excelize.PageLayoutOrientation(excelize.OrientationLandscape),
); err != nil {
    panic(err)
}
if err := xl.SetPageLayout(
    "Sheet1",
    excelize.PageLayoutPaperSize(10),
); err != nil {
    panic(err)
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
xl := excelize.NewFile()
const sheet = "Sheet1"
var (
    orientation excelize.PageLayoutOrientation
    paperSize   excelize.PageLayoutPaperSize
)
if err := xl.GetPageLayout("Sheet1", &orientation); err != nil {
    panic(err)
}
if err := xl.GetPageLayout("Sheet1", &paperSize); err != nil {
    panic(err)
}
fmt.Println("Defaults:")
fmt.Printf("- orientation: %q\n", orientation)
fmt.Printf("- paper size: %d\n", paperSize)
// Output:
// Defaults:
// - orientation: "portrait"
// - paper size: 1
```
