# 工作簿

## 创建 {#NewFile}

```go
func NewFile() *File
```

使用 `NewFile` 新建 Excel 工作薄，新创建的工作簿中会默认包含一个名为 `Sheet1` 的工作表。

## 打开 {#OpenFile}

```go
func OpenFile(filename string) (*File, error)
```

使用 `OpenFile` 打开已有 Excel 文档。

## 保存 {#Save}

```go
func (f *File) Save() error
```

使用 `Save` 保存对 Excel 文档的编辑。

## 另存为 {#SaveAs}

```go
func (f *File) SaveAs(name string) error
```

使用 `SaveAs` 保存 Excel 文档为指定文件。

## 新建工作表 {#NewSheet}

```go
func (f *File) NewSheet(name string) int
```

根据给定的工作表名称添加新的工作表，并返回工作表索引。新创建的工作簿将会包含一个名为 `Sheet1` 的默认工作簿。

## 删除工作表 {#DeleteSheet}

```go
func (f *File) DeleteSheet(name string)
```

根据给定的工作表名称删除指定工作表，谨慎使用此方法，这将会影响到与被删除工作表相关联的公式、引用、图表等元素。如果有其他组件引用了被删除工作表上的值，将会引发错误提示，甚至将会导致打开工作簿失败。当工作簿中仅包含一个工作表时，调用此方法无效。

## 复制工作表 {#CopySheet}

```go
func (f *File) CopySheet(from, to int) error
```

根据给定的被复制工作表与目标工作表索引复制工作表，目标工作表索引需要开发者自行确认是否已经存在。目前支持仅包含单元格值和公式的工作表间的复制，不支持包含表格、图片、图表和透视表等元素的工作表之间的复制。

```go
// 名称为 Sheet1 的工作表已经存在 ...
index := f.NewSheet("Sheet2")
err := f.CopySheet(1, index)
return err
```

## 设置工作表背景图片 {#SetSheetBackground}

```go
func (f *File) SetSheetBackground(sheet, picture string) error
```

根据给定的工作表名称和图片地址为指定的工作表设置平铺效果的背景图片。

## 设置默认工作表 {#SetActiveSheet}

```go
func (f *File) SetActiveSheet(index int)
```

根据给定的索引值设置默认工作表，索引的值应该大于 `0` 且小于工作簿所包含的累积工作表总数。

## 获取默认工作表索引 {#GetActiveSheetIndex}

```go
func (f *File) GetActiveSheetIndex() int
```

获取默认工作表的索引，如果没有找到默认工作表将返回 `0`。

## 设置工作表可见性 {#SetSheetVisible}

```go
func (f *File) SetSheetVisible(name string, visible bool) error
```

根据给定的工作表名称和可见性参数设置工作表的可见性。 一个工作簿中至少包含一个可见工作表。如果给定的工作表为默认工作表，则对其可见性设置无效。工作表可见性状态可参考[工作表状态枚举](https://docs.microsoft.com/zh-cn/dotnet/api/documentformat.openxml.spreadsheet.sheetstatevalues?view=openxml-2.8.1):

|工作表状态枚举|
|---|
|visible|
|hidden|
|veryHidden|

例如，隐藏名为 `Sheet1` 的工作表:

```go
err := f.SetSheetVisible("Sheet1", false)
```

## 获取工作表可见性 {#GetSheetVisible}

```go
func (f *File) GetSheetVisible(name string) bool
```

根据给定的工作表名称获取工作表可见性设置。例如，获取名为 `Sheet1` 的工作表可见性设置:

```go
f.GetSheetVisible("Sheet1")
```

## 获取工作表视图属性 {#GetSheetViewOptions}

```go
func (f *File) GetSheetViewOptions(name string, viewIndex int, opts ...SheetViewOptionPtr) error
```

根据给定的工作表名称、视图索引和视图参数获取工作表视图属性，`viewIndex` 可以是负数，如果是这样，则向后计数（`-1` 代表最后一个视图）。

可选视图参数|类型
---|---
DefaultGridColor|bool
RightToLeft|bool
ShowFormulas|bool
ShowGridLines|bool
ShowRowColHeaders|bool
ZoomScale|float64
TopLeftCell|string

- 例1，获取名为 `Sheet1` 的工作表上最后一个视图的网格线属性设置：

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

得到输出：

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

## 设置工作表页面布局 {#SetPageLayout}

```go
func (f *File) SetPageLayout(sheet string, opts ...PageLayoutOption) error
```

根据给定的工作表名称和页面布局参数设置工作表的页面布局属性。目前支持设置的页面布局属性：

- 通过 `PageLayoutOrientation` 方法设置页面布局方向，默认页面布局方向为“纵向”。下面的表格是 Excelize 中页面布局方向 `PageLayoutOrientation` 参数的列表：

参数 | 方向
---|---
OrientationPortrait | 纵向
OrientationLandscape | 横向

- 通过 `PageLayoutPaperSize` 方法设置页面纸张大小，默认页面布局大小为“信纸 8½ × 11 英寸”。下面的表格是 Excelize 中页面布局大小和索引 `PageLayoutPaperSize` 参数的关系对照：

索引 | 纸张大小
---|---
1   | 信纸 8½ × 11 英寸
2   | 简式信纸 8½ × 11 英寸
3   | 卡片 11 × 17 英寸
4   | 账单 17 × 11 英寸
5   | 律师公文纸 8½ × 14 英寸
6   | 报告单 5½ × 8½ 英寸
7   | 行政公文纸 7½ × 10 英寸
8   | A3 297 × 420 毫米
9   | A4 210 × 297 毫米
10  | A4(小) 210 × 297 毫米
11  | A5 148 × 210 毫米
12  | B4 250 × 353 毫米
13  | B5 176 × 250 毫米
14  | 对开本 8½ × 13 英寸
15  | 四开 215 × 275 毫米
16  | 美式标准纸张 10 × 14 英寸
17  | 美式标准纸张 11 × 17 英寸
18  | Note paper 8.5 × 11 英寸
19  | 信封 #9 3.875 × 8.875 英寸
20  | 信封 #10 4-1/8 × 9½ 英寸
21  | 信封 #11 4.5 × 10.375 英寸
22  | 信封 #12 4.75 × 11 英寸
23  | 信封 #14 5 × 11.5 英寸
24  | C paper 17 × 22 英寸
25  | D paper 22 × 34 英寸
26  | E paper 34 × 44 英寸
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
37  | 君主式信封 3.88 × 7.5 英寸
38  | 信封 6 3/4 3.625 × 6.5 英寸
39  | US standard fanfold 14.875 × 11 英寸
40  | German standard fanfold 8.5 × 12 英寸
41  | German legal fanfold 8.5 × 13 英寸
42  | ISO B4 250 × 353 毫米
43  | 日式明信片 100 × 148 毫米
44  | Standard paper 9 × 11 英寸
45  | Standard paper 10 × 11 英寸
46  | Standard paper 15 × 11 英寸
47  | 邀请信 220 × 220 毫米
50  | Letter extra paper 9.275 × 12 英寸
51  | Legal extra paper 9.275 × 15 英寸
52  | Tabloid extra paper 11.69 × 18 英寸
53  | A4 extra paper 236 × 322 毫米
54  | Letter transverse paper 8.275 × 11 英寸
55  | A4 transverse paper 210 × 297 毫米
56  | Letter extra transverse paper 9.275 × 12 英寸
57  | SuperA/SuperA/A4 paper 227 × 356 毫米
58  | SuperB/SuperB/A3 paper 305 × 487 毫米
59  | Letter plus paper 8.5 × 12.69 英寸
60  | A4 plus paper 210 × 330 毫米
61  | A5 transverse paper 148 × 210 毫米
62  | JIS B5 transverse paper 182 × 257 毫米
63  | A3 extra paper 322 × 445 毫米
64  | A5 extra paper 174 × 235 毫米
65  | ISO B5 extra paper 201 × 276 毫米
66  | A2 420 × 594 毫米
67  | A3 transverse paper 297 × 420 毫米
68  | A3 extra transverse paper 322 × 445 毫米
69  | 双层日式明信片 200 × 148 毫米
70  | A6 105 × 148 毫米
71  | 日式信封 Kaku #2
72  | 日式信封 Kaku #3
73  | 日式信封 Chou #3
74  | 日式信封 Chou #4
75  | Letter Rotated (11in x 8 1/2 11 in)
76  | A3 横向旋转 420 × 297 毫米
77  | A4 横向旋转 297 × 210 毫米
78  | A5 横向旋转 210 × 148 毫米
79  | B4 (JIS) 横向旋转 364 × 257 毫米
80  | B5 (JIS) 横向旋转 257 × 182 毫米
81  | 日式明信片 横向旋转 148 × 100 毫米
82  | 双层日式明信片 横向旋转 148 × 200 毫米
83  | A6 横向旋转 148 × 105 毫米
84  | 日式信封 Kaku #2 横向旋转
85  | 日式信封 Kaku #3 横向旋转
86  | 日式信封 Chou #3 横向旋转
87  | 日式信封 Chou #4 横向旋转
88  | B6 (JIS) 128 × 182 毫米
89  | B6 (JIS) 横向旋转 182 × 128 毫米
90  | 12 × 11 英寸
91  | 日式信封 You #4
92  | 日式信封 You #4 横向旋转
93  | 中式 16 开 146 × 215 毫米
94  | 中式 32 开 97 × 151 毫米
95  | 中式大 32 开 97 × 151 毫米
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
106 | 中式 16 开 横向旋转
107 | 中式 32 开 横向旋转
108 | 中式大 32 开 横向旋转
109 | 中式信封 #1 横向旋转 165 × 102 毫米
110 | 中式信封 #2 横向旋转 176 × 102 毫米
111 | 中式信封 #3 横向旋转 176 × 125 毫米
112 | 中式信封 #4 横向旋转 208 × 110 毫米
113 | 中式信封 #5 横向旋转 220 × 110 毫米
114 | 中式信封 #6 横向旋转 230 × 120 毫米
115 | 中式信封 #7 横向旋转 230 × 160 毫米
116 | 中式信封 #8 横向旋转 309 × 120 毫米
117 | 中式信封 #9 横向旋转 324 × 229 毫米
118 | 中式信封 #10 横向旋转 458 × 324 毫米

- 例如，将名为 `Sheet1` 的工作表页面布局设置为横向并使用 A4(小) 210 × 297 毫米纸张：

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

## 获取工作表页面布局 {#GetPageLayout}

```go
func (f *File) GetPageLayout(sheet string, opts ...PageLayoutOptionPtr) error
```

根据给定的工作表名称和页面布局参数获取工作表的页面布局属性。

- 通过 `PageLayoutOrientation` 方法获取页面布局方向
- 通过 `PageLayoutPaperSize` 方法获取页面纸张大小

例如，获取名为 `Sheet1` 的工作表页面布局设置：

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

得到输出：

```text
Defaults:
- orientation: "portrait"
- paper size: 1
```

## 设置工作表页边距 {#SetPageMargins}

根据给定的工作表名称和页边距参数设置工作表的页边距。页边距可选参数：

参数|数据类型
---|---
PageMarginBotom|float64
PageMarginFooter|float64
PageMarginHeader|float64
PageMarginLeft|float64
PageMarginRight|float64
PageMarginTop|float64

- 例如，设置名为 `Sheet1` 的工作表页边距:

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

## 获取工作表页边距 {#GetPageMargins}

根据给定的工作表名称和页边距参数获取工作表的页边距。页边距可选参数：

参数|数据类型
---|---
PageMarginBotom|float64
PageMarginFooter|float64
PageMarginHeader|float64
PageMarginLeft|float64
PageMarginRight|float64
PageMarginTop|float64

- 例如，获取名为 `Sheet1` 的工作表页边距:

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

得到输出：

```text
Defaults:
- marginBottom: 0.75
- marginFooter: 0.3
- marginHeader: 0.3
- marginLeft: 0.7
- marginRight: 0.7
- marginTop: 0.75
```

## 设置页眉和页脚 {#SetHeaderFooter}

```go
func (f *File) SetHeaderFooter(sheet string, settings *FormatHeaderFooter) error
```

根据给定的工作表名称和控制字符设置工作表的页眉和页脚。页眉和页脚包含如下字段：

Headers and footers are specified using the following settings fields:

字段           | 描述
---|---
AlignWithMargins | 设定页眉页脚页边距与页边距对齐
DifferentFirst   | 设定第一页页眉和页脚
DifferentOddEven | 设定奇数和偶数页页眉和页脚
ScaleWithDoc     | 设定页眉和页脚跟随文档缩放
OddFooter        | 奇数页页脚控制字符
OddHeader        | 奇数页页眉控制字符
EvenFooter       | 偶数页页脚控制字符
EvenHeader       | 偶数页页眉控制字符
FirstFooter      | 首页页脚控制字符
FirstHeader      | 首页页眉控制字符

下表中的格式代码可用于 6 个字符串类型字段: `OddHeader`, `OddFooter`, `EvenHeader`, `EvenFooter`, `FirstFooter`, `FirstHeader`

<table>
    <thead>
        <tr>
            <th>格式代码</th>
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
            <td>文本字体的大小, 其中字体大小为以磅为单位的十进制字体大小</td>
        </tr>
        <tr>
            <td><code>&amp;&quot;font name,font type&quot;</code></td>
            <td>文本字体名字符串、字体名称和文本字体类型字符串、字体类型</td>
        </tr>
        <tr>
            <td><code>&amp;&quot;-,Regular&quot;</code></td>
            <td>常规文本格式。关闭粗体和斜体模式</td>
        </tr>
        <tr>
            <td><code>&amp;A</code></td>
            <td>当前工作表名称</td>
        </tr>
        <tr>
            <td><code>&amp;B</code> or <code>&amp;&quot;-,Bold&quot;</code></td>
            <td>粗体文本格式, 关闭或打开，默认关闭。</td>
        </tr>
        <tr>
            <td><code>&amp;D</code></td>
            <td>当前日期</td>
        </tr>
        <tr>
            <td><code>&amp;C</code></td>
            <td>中间部分</td>
        </tr>
        <tr>
            <td><code>&amp;E</code></td>
            <td>对文本使用双下划线</td>
        </tr>
        <tr>
            <td><code>&amp;F</code></td>
            <td>当前工作簿文件名称</td>
        </tr>
        <tr>
            <td><code>&amp;G</code></td>
            <td>将指定对象做为背景</td>
        </tr>
        <tr>
            <td><code>&amp;H</code></td>
            <td>文字阴影</td>
        </tr>
        <tr>
            <td><code>&amp;I</code> or <code>&amp;&quot;-,Italic&quot;</code></td>
            <td>文字倾斜</td>
        </tr>
        <tr>
            <td><code>&amp;K</code></td>
            <td>字体颜色<br>格式为 RRGGBB 的 RGB 颜色<br>主题颜色被指定为 TTSNNN, 其中 TT 是主题颜色 id, S 是色调或阴影的 &quot;+&quot; 或者 &quot;-&quot;, 是色调或阴影的值</td>
        </tr>
        <tr>
            <td><code>&amp;L</code></td>
            <td>左侧部分</td>
        </tr>
        <tr>
            <td><code>&amp;N</code></td>
            <td>总页数</td>
        </tr>
        <tr>
            <td><code>&amp;O</code></td>
            <td>大纲文本格式</td>
        </tr>
        <tr>
            <td><code>&amp;P[[+\|-]n]</code></td>
            <td>如果没有可选的后缀, 当前页码 (十进制)</td>
        </tr>
        <tr>
            <td><code>&amp;R</code></td>
            <td>右侧部分</td>
        </tr>
        <tr>
            <td><code>&amp;S</code></td>
            <td>文本删除线</td>
        </tr>
        <tr>
            <td><code>&amp;T</code></td>
            <td>当前时间</td>
        </tr>
        <tr>
            <td><code>&amp;U</code></td>
            <td>为文本添加单下划线。默认模式处于关闭状态</td>
        </tr>
        <tr>
            <td><code>&amp;X</code></td>
            <td>上标格式</td>
        </tr>
        <tr>
            <td><code>&amp;Y</code></td>
            <td>下标格式</td>
        </tr>
        <tr>
            <td><code>&amp;Z</code></td>
            <td>当前工作簿文件路径</td>
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

上面的例子蕴含如下格式：

- 第一页有自己的页眉和页脚
- 奇数和偶数页具有不同的页眉和页脚
- 奇数页标题右侧部分为当前页码
- 奇数页页脚中心部分为当前工作簿的文件名
- 偶数页标题左侧部分为当前页码
- 左侧部分为当前日期，偶数页页脚右侧部分为当前时间
- 第一页中心部分的第一行上的文本为“Center Bold Header”, 第二行为日期
- 第一页上没有页脚

## 设置名称 {#SetDefinedName}

```go
func (f *File) SetDefinedName(definedName *DefinedName) error
```

根据给定的名称和作范围设置名称，默认范围是工作簿。例如：

```go
f.SetDefinedName(&excelize.DefinedName{
    Name:     "Amount",
    RefersTo: "Sheet1!$A$2:$D$5",
    Comment:  "defined name comment",
    Scope:    "Sheet2",
})
```

## 获取名称 {#GetDefinedName}

```go
func (f *File) GetDefinedName() []DefinedName
```

获取作用范围内的工作簿和工作表的名称列表。

# 删除名称 {#DeleteDefinedName}

```go
func (f *File) DeleteDefinedName(definedName *DefinedName) error
```

根据给定的名称和名称作用范围删除已定义的名称，默认名称的作用范围为工作簿。例如：

```go
f.DeleteDefinedName(&excelize.DefinedName{
    Name:     "Amount",
    Scope:    "Sheet2",
})
```

## 设置工作簿属性 {#SetDocProps}

```go
func (f *File) SetDocProps(docProperties *DocProperties) error
```

设置工作簿的核心属性。 可以设置的属性包括:

属性           | 描述
---|---
Title          | 文档标题
Subject        | 文档主题
Creator        | 创作者
Keywords       | 文档关键词
Description    | 资源内容的说明
LastModifiedBy | 执行上次修改的用户
Language       | 文档内容的主要语言
Identifier     | 对给定上下文中的资源的明确引用
Revision       | 文档修订版本
ContentStatus  | 文档内容的状态。例如: 值可能包括 "Draft"、"Reviewed" 和 "Final"
Category       | 文档内容的分类
Version        | 版本号，该值由用户或应用程序设置

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

## 获取工作簿属性 {#GetDocProps}

```go
func (f *File) GetDocProps() (*DocProperties, error)
```

获取工作簿的核心属性。
