# 活頁簿

## 創建 {#NewFile}

```go
func NewFile() *File
```

使用 `NewFile` 新建 Excel 工作薄，新創建的活頁簿中會默認包含一個名為 `Sheet1` 的工作表。

## 打開 {#OpenFile}

```go
func OpenFile(filename string) (*File, error)
```

使用 `OpenFile` 打開已有 Excel 文檔。

## 儲存 {#Save}

```go
func (f *File) Save() error
```

使用 `Save` 儲存對 Excel 文檔的編輯。

## 另存為 {#SaveAs}

```go
func (f *File) SaveAs(name string) error
```

使用 `SaveAs` 儲存 Excel 文檔為指定檔案。

## 新建工作表 {#NewSheet}

```go
func (f *File) NewSheet(name string) int
```

根據給定的工作表名稱添加新的工作表，並傳回工作表索引。新創建的活頁簿將會包含一個名為 `Sheet1` 的默認活頁簿。

## 刪除工作表 {#DeleteSheet}

```go
func (f *File) DeleteSheet(name string)
```

根據給定的工作表名稱刪除指定工作表，謹慎使用此方法，這將會影響到與被刪除工作表相關聯的公式、引用、圖表等元素。如果有其他組件引用了被刪除工作表上的值，將會引發錯誤提示，甚至將會導致打開活頁簿失敗。當活頁簿中僅包含一個工作表時，調用此方法無效。

## 複製工作表 {#CopySheet}

```go
func (f *File) CopySheet(from, to int) error
```

根據給定的被複製工作表與目標工作表索引複製工作表，目標工作表索引需要開發者自行確認是否已經存在。目前支持僅包含儲存格值和公式的工作表間的複製，不支持包含表格、圖片、圖表和透視表等元素的工作表之間的複製。

```go
// 名稱為 Sheet1 的工作表已經存在 ...
index := f.NewSheet("Sheet2")
err := f.CopySheet(1, index)
return err
```

## 設置工作表背景圖片 {#SetSheetBackground}

```go
func (f *File) SetSheetBackground(sheet, picture string) error
```

根據給定的工作表名稱和圖片地址為指定的工作表設置平鋪效果的背景圖片。

## 設置默認工作表 {#SetActiveSheet}

```go
func (f *File) SetActiveSheet(index int)
```

根據給定的索引值設置默認工作表，索引的值應該大於 `0` 且小於活頁簿所包含的累積工作表總數。

## 獲取默認工作表索引 {#GetActiveSheetIndex}

```go
func (f *File) GetActiveSheetIndex() int
```

獲取默認工作表的索引，如果沒有找到默認工作表將傳回 `0`。

## 設置工作表可見性 {#SetSheetVisible}

```go
func (f *File) SetSheetVisible(name string, visible bool) error
```

根據給定的工作表名稱和可見性參數設置工作表的可見性。一個活頁簿中至少包含一個可見工作表。如果給定的工作表為默認工作表，則對其可見性設置無效。工作表可見性狀態可參考[工作表狀態枚舉](https://docs.microsoft.com/zh-cn/dotnet/api/documentformat.openxml.spreadsheet.sheetstatevalues?view=openxml-2.8.1):

|工作表狀態枚舉|
|---|
|visible|
|hidden|
|veryHidden|

例如，隱藏名為 `Sheet1` 的工作表:

```go
err := f.SetSheetVisible("Sheet1", false)
```

## 獲取工作表可見性 {#GetSheetVisible}

```go
func (f *File) GetSheetVisible(name string) bool
```

根據給定的工作表名稱獲取工作表可見性設置。例如，獲取名為 `Sheet1` 的工作表可見性設置:

```go
f.GetSheetVisible("Sheet1")
```

## 設置工作表檢視屬性 {#SetSheetViewOptions}

```go
func (f *File) SetSheetViewOptions(name string, viewIndex int, opts ...SheetViewOption) error
```

根據給定的工作表名稱、檢視索引和檢視參數設置工作表檢視屬性，`viewIndex` 可以是負數，如果是這樣，則向後計數（`-1` 代表最後一個檢視）。

可選檢視參數|類別
---|---
DefaultGridColor|bool
RightToLeft|bool
ShowFormulas|bool
ShowGridLines|bool
ShowRowColHeaders|bool
ZoomScale|float64
TopLeftCell|string

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
    println(err.Error())
}

var zoomScale excelize.ZoomScale
fmt.Println("Default:")
fmt.Println("- zoomScale: 80")

if err := f.SetSheetViewOptions(sheet, 0, excelize.ZoomScale(500)); err != nil {
    println(err.Error())
}

if err := f.GetSheetViewOptions(sheet, 0, &zoomScale); err != nil {
    println(err.Error())
}

fmt.Println("Used out of range value:")
fmt.Println("- zoomScale:", zoomScale)

if err := f.SetSheetViewOptions(sheet, 0, excelize.ZoomScale(123)); err != nil {
    println(err.Error())
}

if err := f.GetSheetViewOptions(sheet, 0, &zoomScale); err != nil {
    println(err.Error())
}

fmt.Println("Used correct value:")
fmt.Println("- zoomScale:", zoomScale)
```

得到輸出：

```text
Default:
- zoomScale: 80
Used out of range value:
- zoomScale: 80
Used correct value:
- zoomScale: 123
```

## 獲取工作表檢視屬性 {#GetSheetViewOptions}

```go
func (f *File) GetSheetViewOptions(name string, viewIndex int, opts ...SheetViewOptionPtr) error
```

根據給定的工作表名稱、檢視索引和檢視參數獲取工作表檢視屬性，`viewIndex` 可以是負數，如果是這樣，則向後計數（`-1` 代表最後一個檢視）。

可選檢視參數|類別
---|---
DefaultGridColor|bool
RightToLeft|bool
ShowFormulas|bool
ShowGridLines|bool
ShowRowColHeaders|bool
ZoomScale|float64
TopLeftCell|string

- 例1，獲取名為 `Sheet1` 的工作表上最後一個檢視的網格線屬性設置：

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
    panic(err)
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
    panic(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &topLeftCell); err != nil {
    panic(err)
}

if err := f.SetSheetViewOptions(sheet, 0, excelize.ShowGridLines(false)); err != nil {
    panic(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &showGridLines); err != nil {
    panic(err)
}

if err := f.SetSheetViewOptions(sheet, 0, excelize.ShowZeros(false)); err != nil {
    panic(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &showZeros); err != nil {
    panic(err)
}

fmt.Println("After change:")
fmt.Println("- showGridLines:", showGridLines)
fmt.Println("- showZeros:", showZeros)
fmt.Println("- topLeftCell:", topLeftCell)
```

得到輸出：

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

## 設置工作表頁面佈局 {#SetPageLayout}

```go
func (f *File) SetPageLayout(sheet string, opts ...PageLayoutOption) error
```

根據給定的工作表名稱和頁面佈局參數設置工作表的頁面佈局屬性。目前支持設置的頁面佈局屬性：

- 通過 `PageLayoutOrientation` 方法設置頁面佈局方向，默認頁面佈局方向為「直向」。下面的表格是 Excelize 中頁面佈局方向 `PageLayoutOrientation` 參數的列表：

參數 | 方向
---|---
OrientationPortrait | 直向
OrientationLandscape | 橫向

- 通過 `PageLayoutPaperSize` 方法設置頁面紙張大小，默認頁面佈局大小為「信紙 8½ × 11 英吋」。下面的表格是 Excelize 中頁面佈局大小和索引 `PageLayoutPaperSize` 參數的關係對照：

索引 | 紙張大小
---|---
1   | 信紙 8½ × 11 英吋
2   | 簡式信紙 8½ × 11 英吋
3   | 卡片 11 × 17 英吋
4   | 賬單 17 × 11 英吋
5   | 律師公文紙 8½ × 14 英吋
6   | 報告單 5½ × 8½ 英吋
7   | 行政公文紙 7½ × 10 英吋
8   | A3 297 × 420 毫米
9   | A4 210 × 297 毫米
10  | A4(小) 210 × 297 毫米
11  | A5 148 × 210 毫米
12  | B4 250 × 353 毫米
13  | B5 176 × 250 毫米
14  | 對開本 8½ × 13 英吋
15  | 四開 215 × 275 毫米
16  | 美式標準紙張 10 × 14 英吋
17  | 美式標準紙張 11 × 17 英吋
18  | Note paper 8.5 × 11 英吋
19  | 信封 #9 3.875 × 8.875 英吋
20  | 信封 #10 4-1/8 × 9½ 英吋
21  | 信封 #11 4.5 × 10.375 英吋
22  | 信封 #12 4.75 × 11 英吋
23  | 信封 #14 5 × 11.5 英吋
24  | C paper 17 × 22 英吋
25  | D paper 22 × 34 英吋
26  | E paper 34 × 44 英吋
27  | 信封 DL 110 × 220 毫米
28  | 信封 C5 162 × 229 毫米
29  | 信封 C3 324 × 458 毫米
30  | 信封 C4 229 × 324 毫米
31  | 信封 C6 114 × 162 毫米
32  | 信封 C65 114 × 229 毫米
33  | 信封 B4 250 × 353 毫米
34  | 信封 B5 176 × 250 毫米
35  | 信封 B6 176 × 125 毫米
36  | 信封 Italy 110 × 230 毫米
37  | 君主式信封 3.88 × 7.5 英吋
38  | 信封 6 3/4 3.625 × 6.5 英吋
39  | US standard fanfold 14.875 × 11 英吋
40  | German standard fanfold 8.5 × 12 英吋
41  | German legal fanfold 8.5 × 13 英吋
42  | ISO B4 250 × 353 毫米
43  | 日式明信片 100 × 148 毫米
44  | Standard paper 9 × 11 英吋
45  | Standard paper 10 × 11 英吋
46  | Standard paper 15 × 11 英吋
47  | 邀請信 220 × 220 毫米
50  | Letter extra paper 9.275 × 12 英吋
51  | Legal extra paper 9.275 × 15 英吋
52  | Tabloid extra paper 11.69 × 18 英吋
53  | A4 extra paper 236 × 322 毫米
54  | Letter transverse paper 8.275 × 11 英吋
55  | A4 transverse paper 210 × 297 毫米
56  | Letter extra transverse paper 9.275 × 12 英吋
57  | SuperA/SuperA/A4 paper 227 × 356 毫米
58  | SuperB/SuperB/A3 paper 305 × 487 毫米
59  | Letter plus paper 8.5 × 12.69 英吋
60  | A4 plus paper 210 × 330 毫米
61  | A5 transverse paper 148 × 210 毫米
62  | JIS B5 transverse paper 182 × 257 毫米
63  | A3 extra paper 322 × 445 毫米
64  | A5 extra paper 174 × 235 毫米
65  | ISO B5 extra paper 201 × 276 毫米
66  | A2 420 × 594 毫米
67  | A3 transverse paper 297 × 420 毫米
68  | A3 extra transverse paper 322 × 445 毫米
69  | 雙層日式明信片 200 × 148 毫米
70  | A6 105 × 148 毫米
71  | 日式信封 Kaku #2
72  | 日式信封 Kaku #3
73  | 日式信封 Chou #3
74  | 日式信封 Chou #4
75  | Letter Rotated (11in x 8 1/2 11 in)
76  | A3 橫向旋轉 420 × 297 毫米
77  | A4 橫向旋轉 297 × 210 毫米
78  | A5 橫向旋轉 210 × 148 毫米
79  | B4 (JIS) 橫向旋轉 364 × 257 毫米
80  | B5 (JIS) 橫向旋轉 257 × 182 毫米
81  | 日式明信片 橫向旋轉 148 × 100 毫米
82  | 雙層日式明信片 橫向旋轉 148 × 200 毫米
83  | A6 橫向旋轉 148 × 105 毫米
84  | 日式信封 Kaku #2 橫向旋轉
85  | 日式信封 Kaku #3 橫向旋轉
86  | 日式信封 Chou #3 橫向旋轉
87  | 日式信封 Chou #4 橫向旋轉
88  | B6 (JIS) 128 × 182 毫米
89  | B6 (JIS) 橫向旋轉 182 × 128 毫米
90  | 12 × 11 英吋
91  | 日式信封 You #4
92  | 日式信封 You #4 橫向旋轉
93  | 中式 16 開 146 × 215 毫米
94  | 中式 32 開 97 × 151 毫米
95  | 中式大 32 開 97 × 151 毫米
96  | 中式信封 #1 102 × 165 毫米
97  | 中式信封 #2 102 × 176 毫米
98  | 中式信封 #3 125 × 176 毫米
99  | 中式信封 #4 110 × 208 毫米
100 | 中式信封 #5 110 × 220 毫米
101 | 中式信封 #6 120 × 230 毫米
102 | 中式信封 #7 160 × 230 毫米
103 | 中式信封 #8 120 × 309 毫米
104 | 中式信封 #9 229 × 324 毫米
105 | 中式信封 #10 324 × 458 毫米
106 | 中式 16 開 橫向旋轉
107 | 中式 32 開 橫向旋轉
108 | 中式大 32 開 橫向旋轉
109 | 中式信封 #1 橫向旋轉 165 × 102 毫米
110 | 中式信封 #2 橫向旋轉 176 × 102 毫米
111 | 中式信封 #3 橫向旋轉 176 × 125 毫米
112 | 中式信封 #4 橫向旋轉 208 × 110 毫米
113 | 中式信封 #5 橫向旋轉 220 × 110 毫米
114 | 中式信封 #6 橫向旋轉 230 × 120 毫米
115 | 中式信封 #7 橫向旋轉 230 × 160 毫米
116 | 中式信封 #8 橫向旋轉 309 × 120 毫米
117 | 中式信封 #9 橫向旋轉 324 × 229 毫米
118 | 中式信封 #10 橫向旋轉 458 × 324 毫米

- 例如，將名為 `Sheet1` 的工作表頁面佈局設置為橫向並使用 A4(小) 210 × 297 毫米紙張：

```go
f := excelize.NewFile()
const sheet = "Sheet1"

if err := f.SetPageLayout(
    "Sheet1",
    excelize.PageLayoutOrientation(excelize.OrientationLandscape),
); err != nil {
    panic(err)
}
if err := f.SetPageLayout(
    "Sheet1",
    excelize.PageLayoutPaperSize(10),
); err != nil {
    panic(err)
}
```

## 獲取工作表頁面佈局 {#GetPageLayout}

```go
func (f *File) GetPageLayout(sheet string, opts ...PageLayoutOptionPtr) error
```

根據給定的工作表名稱和頁面佈局參數獲取工作表的頁面佈局屬性。

- 通過 `PageLayoutOrientation` 方法獲取頁面佈局方向
- 通過 `PageLayoutPaperSize` 方法獲取頁面紙張大小

例如，獲取名為 `Sheet1` 的工作表頁面佈局設置：

```go
f := excelize.NewFile()
const sheet = "Sheet1"
var (
    orientation excelize.PageLayoutOrientation
    paperSize   excelize.PageLayoutPaperSize
)
if err := f.GetPageLayout("Sheet1", &orientation); err != nil {
    panic(err)
}
if err := f.GetPageLayout("Sheet1", &paperSize); err != nil {
    panic(err)
}
fmt.Println("Defaults:")
fmt.Printf("- orientation: %q\n", orientation)
fmt.Printf("- paper size: %d\n", paperSize)
```

得到輸出：

```text
Defaults:
- orientation: "portrait"
- paper size: 1
```

## 設置工作表頁邊距 {#SetPageMargins}

```go
func (f *File) SetPageMargins(sheet string, opts ...PageMarginsOptions) error
```

根據給定的工作表名稱和頁邊距參數設置工作表的頁邊距。頁邊距可選參數：

參數|資料類別
---|---
PageMarginBotom|float64
PageMarginFooter|float64
PageMarginHeader|float64
PageMarginLeft|float64
PageMarginRight|float64
PageMarginTop|float64

- 例如，設置名為 `Sheet1` 的工作表頁邊距:

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
    panic(err)
}
```

## 獲取工作表頁邊距 {#GetPageMargins}

根據給定的工作表名稱和頁邊距參數獲取工作表的頁邊距。頁邊距可選參數：

參數|資料類別
---|---
PageMarginBotom|float64
PageMarginFooter|float64
PageMarginHeader|float64
PageMarginLeft|float64
PageMarginRight|float64
PageMarginTop|float64

- 例如，獲取名為 `Sheet1` 的工作表頁邊距:

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
    panic(err)
}
fmt.Println("Defaults:")
fmt.Println("- marginBottom:", marginBottom)
fmt.Println("- marginFooter:", marginFooter)
fmt.Println("- marginHeader:", marginHeader)
fmt.Println("- marginLeft:", marginLeft)
fmt.Println("- marginRight:", marginRight)
fmt.Println("- marginTop:", marginTop)
```

得到輸出：

```text
Defaults:
- marginBottom: 0.75
- marginFooter: 0.3
- marginHeader: 0.3
- marginLeft: 0.7
- marginRight: 0.7
- marginTop: 0.75
```

## 設置頁眉和頁腳 {#SetHeaderFooter}

```go
func (f *File) SetHeaderFooter(sheet string, settings *FormatHeaderFooter) error
```

根據給定的工作表名稱和控制字符設置工作表的頁眉和頁腳。頁眉和頁腳包含如下欄位：

Headers and footers are specified using the following settings fields:

欄位           | 描述
---|---
AlignWithMargins | 設定頁眉頁腳頁邊距與頁邊距對齊
DifferentFirst   | 設定第一頁頁眉和頁腳
DifferentOddEven | 設定奇數和偶數頁頁眉和頁腳
ScaleWithDoc     | 設定頁眉和頁腳跟隨文檔縮放
OddFooter        | 奇數頁頁腳控制字符
OddHeader        | 奇數頁頁眉控制字符
EvenFooter       | 偶數頁頁腳控制字符
EvenHeader       | 偶數頁頁眉控制字符
FirstFooter      | 首頁頁腳控制字符
FirstHeader      | 首頁頁眉控制字符

下表中的格式代碼可用於 6 個字符串類別欄位: `OddHeader`, `OddFooter`, `EvenHeader`, `EvenFooter`, `FirstFooter`, `FirstHeader`

<table>
    <thead>
        <tr>
            <th>格式代碼</th>
            <th>描述</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>&amp;&amp;</code></td>
            <td>字符 &quot;&amp;&quot;</td>
        </tr>
        <tr>
            <td><code>&amp;font-size</code></td>
            <td>文本字型的大小, 其中字型大小為以磅為單位的十進制字型大小</td>
        </tr>
        <tr>
            <td><code>&amp;&quot;font name,font type&quot;</code></td>
            <td>文本字型名字符串、字型名稱和文本字型類別字符串、字型類別</td>
        </tr>
        <tr>
            <td><code>&amp;&quot;-,Regular&quot;</code></td>
            <td>常規文本格式。關閉粗體和斜體模式</td>
        </tr>
        <tr>
            <td><code>&amp;A</code></td>
            <td>當前工作表名稱</td>
        </tr>
        <tr>
            <td><code>&amp;B</code> or <code>&amp;&quot;-,Bold&quot;</code></td>
            <td>粗體文本格式, 關閉或打開，默認關閉。</td>
        </tr>
        <tr>
            <td><code>&amp;D</code></td>
            <td>當前日期</td>
        </tr>
        <tr>
            <td><code>&amp;C</code></td>
            <td>中間部分</td>
        </tr>
        <tr>
            <td><code>&amp;E</code></td>
            <td>對文本使用雙下划線</td>
        </tr>
        <tr>
            <td><code>&amp;F</code></td>
            <td>當前活頁簿檔案名稱</td>
        </tr>
        <tr>
            <td><code>&amp;G</code></td>
            <td>將指定對象做為背景</td>
        </tr>
        <tr>
            <td><code>&amp;H</code></td>
            <td>文字陰影</td>
        </tr>
        <tr>
            <td><code>&amp;I</code> or <code>&amp;&quot;-,Italic&quot;</code></td>
            <td>文字傾斜</td>
        </tr>
        <tr>
            <td><code>&amp;K</code></td>
            <td>字型色彩<br>格式為 RRGGBB 的 RGB 色彩<br>主題色彩被指定為 TTSNNN, 其中 TT 是主題色彩 id, S 是色調或陰影的 &quot;+&quot; 或者 &quot;-&quot;, 是色調或陰影的值</td>
        </tr>
        <tr>
            <td><code>&amp;L</code></td>
            <td>左側部分</td>
        </tr>
        <tr>
            <td><code>&amp;N</code></td>
            <td>總頁數</td>
        </tr>
        <tr>
            <td><code>&amp;O</code></td>
            <td>大綱文本格式</td>
        </tr>
        <tr>
            <td><code>&amp;P[[+\|-]n]</code></td>
            <td>如果沒有可選的後綴, 當前頁碼 (十進制)</td>
        </tr>
        <tr>
            <td><code>&amp;R</code></td>
            <td>右側部分</td>
        </tr>
        <tr>
            <td><code>&amp;S</code></td>
            <td>文本刪除線</td>
        </tr>
        <tr>
            <td><code>&amp;T</code></td>
            <td>當前時間</td>
        </tr>
        <tr>
            <td><code>&amp;U</code></td>
            <td>為文本添加單下划線。默認模式處於關閉狀態</td>
        </tr>
        <tr>
            <td><code>&amp;X</code></td>
            <td>上標格式</td>
        </tr>
        <tr>
            <td><code>&amp;Y</code></td>
            <td>下標格式</td>
        </tr>
        <tr>
            <td><code>&amp;Z</code></td>
            <td>當前活頁簿檔案路徑</td>
        </tr>
    </tbody>
</table>

例如：

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

上面的例子蘊含如下格式：

- 第一頁有自己的頁眉和頁腳
- 奇數和偶數頁具有不同的頁眉和頁腳
- 奇數頁標題右側部分為當前頁碼
- 奇數頁頁腳中心部分為當前活頁簿的檔案名
- 偶數頁標題左側部分為當前頁碼
- 左側部分為當前日期，偶數頁頁腳右側部分為當前時間
- 第一頁中心部分的第一行上的文本為「Center Bold Header」, 第二行為日期
- 第一頁上沒有頁腳

## 設置名稱 {#SetDefinedName}

```go
func (f *File) SetDefinedName(definedName *DefinedName) error
```

根據給定的名稱和作範圍設置名稱，默認範圍是活頁簿。例如：

```go
f.SetDefinedName(&excelize.DefinedName{
    Name:     "Amount",
    RefersTo: "Sheet1!$A$2:$D$5",
    Comment:  "defined name comment",
    Scope:    "Sheet2",
})
```

## 獲取名稱 {#GetDefinedName}

```go
func (f *File) GetDefinedName() []DefinedName
```

獲取作用範圍內的活頁簿和工作表的名稱列表。

# 刪除名稱 {#DeleteDefinedName}

```go
func (f *File) DeleteDefinedName(definedName *DefinedName) error
```

根據給定的名稱和名稱作用範圍刪除已定義的名稱，默認名稱的作用範圍為活頁簿。例如：

```go
f.DeleteDefinedName(&excelize.DefinedName{
    Name:     "Amount",
    Scope:    "Sheet2",
})
```

## 設置活頁簿屬性 {#SetDocProps}

```go
func (f *File) SetDocProps(docProperties *DocProperties) error
```

設置活頁簿的核心屬性。 可以設置的屬性包括:

屬性           | 描述
---|---
Title          | 文檔標題
Subject        | 文檔主題
Creator        | 創作者
Keywords       | 文檔關鍵詞
Description    | 資源內容的說明
LastModifiedBy | 執行上次修改的用戶
Language       | 文檔內容的主要語言
Identifier     | 對給定上下文中的資源的明確引用
Revision       | 文檔修訂版本
ContentStatus  | 文檔內容的狀態。例如: 值可能包括 "Draft"、"Reviewed" 和 "Final"
Category       | 文檔內容的分類
Version        | 版本號，該值由用戶或應用程式設置

例如：

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

## 獲取活頁簿屬性 {#GetDocProps}

```go
func (f *File) GetDocProps() (*DocProperties, error)
```

獲取活頁簿的核心屬性。
