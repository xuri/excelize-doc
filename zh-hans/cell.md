# 单元格

## 设置单元格的值 {#SetCellValue}

```go
func (f *File) SetCellValue(sheet, axis string, value interface{})
```

根据给定的工作表名和单元格坐标设置单元格的值。

|支持的数据类型|
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

## 设置布尔型值 {#SetCellBool}

```go
func (f *File) SetCellBool(sheet, axis string, value bool)
```

根据给定的工作表名和单元格坐标设置布尔型单元格的值。

## 设置默认字符型值 {#SetCellDefault}

```go
func (f *File) SetCellDefault(sheet, axis, value string)
```

根据给定的工作表名和单元格坐标设置字符型单元格的值，字符将不会进行特殊字符过滤。

## 设置实数 {#SetCellInt}

```go
func (f *File) SetCellInt(sheet, axis string, value int)
```

根据给定的工作表名和单元格坐标设置实数单元格的值。

## 设置字符型值 {#SetCellStr}

```go
func (f *File) SetCellStr(sheet, axis, value string)
```

根据给定的工作表名和单元格坐标设置字符型单元格的值，字符将会进行特殊字符过滤，并且字符串的累计长度应不超过 `32767`，多余的字符将会被忽略。

## 设置单元格样式 {#SetCellStyle}

```go
func (f *File) SetCellStyle(sheet, hcell, vcell string, styleID int)
```

根据给定的工作表名、单元格坐标区域和样式索引设置单元格的值。样式索引可以通过 `NewStyle` 函数获取。注意，在同一个坐标区域内的 `diagonalDown` 和 `diagonalUp` 需要保持颜色一致。

- 例1，为名为 `Sheet1` 的工作表 `D7` 单元格设置边框样式：

```go
style, err := xlsx.NewStyle(`{"border":[{"type":"left","color":"0000FF","style":3},{"type":"top","color":"00FF00","style":4},{"type":"bottom","color":"FFFF00","style":5},{"type":"right","color":"FF0000","style":6},{"type":"diagonalDown","color":"A020F0","style":7},{"type":"diagonalUp","color":"A020F0","style":8}]}`)
if err != nil {
    fmt.Println(err)
}
xlsx.SetCellStyle("Sheet1", "D7", "D7", style)
```

!["为单元格设置边框样式"](./images/SetCellStyle_01.png "为单元格设置边框样式")

单元格 `D7` 的四个边框被设置了不同的样式和颜色，这与调用 `NewStyle` 函数时的参数有关，需要设置不同的样式可参考该章节的文档。

- 例2，为名为 `Sheet1` 的工作表 `D7` 单元格设置渐变样式：

```go
style, err := xlsx.NewStyle(`{"fill":{"type":"gradient","color":["#FFFFFF","#E0EBF5"],"shading":1}}`)
if err != nil {
    fmt.Println(err)
}
xlsx.SetCellStyle("Sheet1", "D7", "D7", style)
```

!["为单元格设置渐变样式"](./images/SetCellStyle_02.png "为单元格设置渐变样式")

单元格 `D7` 被设置了渐变效果的颜色填充，渐变填充效果与调用 `NewStyle` 函数时的参数有关，需要设置不同的样式可参考该章节的文档。

- 例3，为名为 `Sheet1` 的工作表 `D7` 单元格设置纯色填充：

```go
style, err := xlsx.NewStyle(`{"fill":{"type":"pattern","color":["#E0EBF5"],"pattern":1}}`)
if err != nil {
    fmt.Println(err)
}
xlsx.SetCellStyle("Sheet1", "D7", "D7", style)
```

!["为单元格设置纯色填充"](./images/SetCellStyle_03.png "为单元格设置纯色填充")

单元格 `D7` 被设置了纯色填充。

- 例4，为名为 `Sheet1` 的工作表 `D7` 单元格设置字符间距与旋转角度：

```go
xlsx.SetCellValue("Sheet1", "D7", "样式")
style, err := xlsx.NewStyle(`{"alignment":{"horizontal":"center","ident":1,"justify_last_line":true,"reading_order":0,"relative_indent":1,"shrink_to_fit":true,"text_rotation":45,"vertical":"","wrap_text":true}}`)
if err != nil {
    fmt.Println(err)
}
xlsx.SetCellStyle("Sheet1", "D7", "D7", style)
```

!["设置字符间距与旋转角度"](./images/SetCellStyle_04.png "设置字符间距与旋转角度")

- 例5，Excel 中的日期和时间用实数表示，例如 `2017/7/4  12:00:00 PM` 可以用数字 `42920.5` 来表示。为名为 `Sheet1` 的工作表 `D7` 单元格设置时间格式：

```go
xlsx.SetCellValue("Sheet1", "D7", 42920.5)
xlsx.SetColWidth("Sheet1", "D", "D", 13)
style, err := xlsx.NewStyle(`{"number_format": 22}`)
if err != nil {
    fmt.Println(err)
}
xlsx.SetCellStyle("Sheet1", "D7", "D7", style)
```

!["为单元格设置时间格式"](./images/SetCellStyle_05.png "为单元格设置时间格式")

单元格 `D7` 被设置了时间格式。注意，当应用了时间格式的单元格宽度过窄无法完整展示时会显示为 `####`，可以拖拽调整列宽或者通过调用 `SetColWidth` 函数设置列款到合适的大小使其正常显示。

- 例6，为名为 `Sheet1` 的工作表 `D7` 单元格设置字体、字号、颜色和倾斜样式：

```go
xlsx.SetCellValue("Sheet1", "D7", "Excel")
style, err := xlsx.NewStyle(`{"font":{"bold":true,"italic":true,"family":"Berlin Sans FB Demi","size":36,"color":"#777777"}}`)
if err != nil {
    fmt.Println(err)
}
xlsx.SetCellStyle("Sheet1", "D7", "D7", style)
```

!["为单元格设置字体、字号、颜色和倾斜样式"](./images/SetCellStyle_06.png "为单元格设置字体、字号、颜色和倾斜样式")

- 例7，锁定并隐藏名为 `Sheet1` 的工作表 `D7` 单元格：

```go
style, err := xlsx.NewStyle(`{"protection":{"hidden":true, "locked":true}}`)
if err != nil {
    fmt.Println(err)
}
xlsx.SetCellStyle("Sheet1", "D7", "D7", style)
```

要锁定单元格或隐藏公式，请保护工作表。在“审阅”选项卡上，单击“保护工作表”。

## 设置超链接 {#SetCellHyperLink}

```go
func (f *File) SetCellHyperLink(sheet, axis, link, linkType string)
```

根据给定的工作表、单元格坐标、链接资源和资源类型设置单元格的超链接。资源类型分为外部链接地址 `External` 和工作簿内部位置链接 `Location` 两种。

- 例1，为名为 `Sheet1` 的工作表 `A3` 单元格添加外部链接：

```go
xlsx.SetCellHyperLink("Sheet1", "A3", "https://github.com/360EntSecGroup-Skylar/excelize", "External")
// 为单元格设置字体和下划线样式
style, _ := xlsx.NewStyle(`{"font":{"color":"#1265BE","underline":"single"}}`)
xlsx.SetCellStyle("Sheet1", "A3", "A3", style)
```

- 例2，为名为 `Sheet1` 的工作表 `A3` 单元格添加内部位置链接：

```go
xlsx.SetCellHyperLink("Sheet1", "A3", "Sheet1!A40", "Location")
```

## 获取单元格的值 {#GetCellValue}

```go
func (f *File) GetCellValue(sheet, axis string) string
```

根据给定的工作表和单元格坐标获取单元格的值，返回值将转换为 `string` 类型。如果可以将单元格格式应用于单元格的值，将返回应用后的值，否则将返回原始值。

## 获取全部单元格的值 {#GetRows}

```go
func (f *File) GetRows(sheet string) [][]string
```

根据给定的工作表名（大小写敏感）获取该工作表上全部单元格的值，以二维数组形式返回，其中单元格的值将转换为 `string` 类型。如果可以将单元格格式应用于单元格的值，将使用应用后的值，否则将使用原始值。

例如，获取并遍历输出名为 `Sheet1` 的工作表上的所有单元格的值：

```go
for _, row := range xlsx.GetRows("Sheet1") {
    for _, colCell := range row {
        fmt.Print(colCell, "\t")
    }
    fmt.Println()
}
```

## 获取超链接 {#GetCellHyperLink}

```go
func (f *File) GetCellHyperLink(sheet, axis string) (bool, string)
```

根据给定的工作表名（大小写敏感）和单元格坐标获取单元格超链接，如果该单元格存在超链接，将返回 `true` 和链接地址，否则将返回 `false` 和空的链接地址。

例如，获取名为 `Sheet1` 的工作表上坐标为 `H6` 单元格的超链接：

```go
link, target := xlsx.GetCellHyperLink("Sheet1", "H6")
```

## 获取样式索引 {#GetCellStyle}

```go
func (f *File) GetCellStyle(sheet, axis string) int
```

根据给定的工作表名（大小写敏感）和单元格坐标获取单元格样式索引，获取到的索引可以在复制单元格样式时，作为调用 `SetCellValue` 函数的参数使用。

## 合并单元格 {#MergeCell}

```go
func (f *File) MergeCell(sheet, hcell, vcell string)
```

根据给定的工作表名（大小写敏感）和单元格坐标区域合并单元格。例如，合并名为 `Sheet1` 的工作表上 `D3:E9` 区域内的单元格：

```go
xlsx.MergeCell("Sheet1", "D3", "E9")
```

如果给定的单元格坐标区域与已有的其他合并单元格相重叠，已有的合并单元格将会被删除。

## 获取合并单元格 {#GetMergeCells}

根据给定的工作表名（大小写敏感）获取全部合并单元格的坐标区域和值。

```go
func (f *File) GetMergeCells(sheet string) []MergeCell
```

## 添加批注 {#AddComment}

```go
func (f *File) AddComment(sheet, cell, format string) error
```

根据给定的工作表名称、单元格坐标和样式参数（作者与文本信息）添加批注。作者信息最大长度为 255 个字符，最大文本内容长度为 32512 个字符，超出该范围的字符将会被忽略。例如，为 `Sheet1!$A$3` 单元格添加批注：

!["在 Excel 文档中添加批注"](./images/comment.png "在 Excel 文档中添加批注")

```go
xlsx.AddComment("Sheet1", "A3", `{"author":"Excelize: ","text":"This is a comment."}`)
```

## 获取批注 {#GetComments}

```go
func (f *File) GetComments() (comments map[string][]Comment)
```

通过该方法可以获取全部工作表中的批注。

## 设置公式 {#SetCellFormula}

```go
func (f *File) SetCellFormula(sheet, axis, formula string)
```

根据给定的工作表名（大小写敏感）和单元格坐设置取该单元格上的公式。公式的结果会在工作表被 Office Excel 应用程序打开时计算，Excelize 目前不提供公式计算引擎，所以无法计算公式结果。

## 获取公式 {#GetCellFormula}

```go
func (f *File) GetCellFormula(sheet, axis string) string
```

根据给定的工作表名（大小写敏感）和单元格坐标获取该单元格上的公式。
