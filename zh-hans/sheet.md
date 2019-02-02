# 工作表

## 设置列可见性 {#SetColVisible}

```go
func (f *File) SetColVisible(sheet, column string, visible bool)
```

根据给定的工作表名称（大小写敏感）和列名称设置列可见性。例如隐藏名为 `Sheet1` 工作表上的 `D` 列：

```go
xlsx.SetColVisible("Sheet1", "D", false)
```

## 设置列宽度 {#SetColWidth}

```go
func (f *File) SetColWidth(sheet, startcol, endcol string, width float64)
```

根据给定的工作表名称（大小写敏感）、列范围和宽度值设置单个或多个列的宽度。例如设置名为 `Sheet1` 工作表上 `A` 到 `H` 列的宽度为 `20`：

```go
xlsx := excelize.NewFile()
xlsx.SetColWidth("Sheet1", "A", "H", 20)
err := xlsx.Save()
if err != nil {
    fmt.Println(err)
}
```

## 设置行高度 {#SetRowHeight}

```go
func (f *File) SetRowHeight(sheet string, row int, height float64)
```

根据给定的工作表名称（大小写敏感）、行号和高度值设置单行高度。例如设置名为 `Sheet1` 工作表首行的高度为 `50`：

```go
xlsx.SetRowHeight("Sheet1", 1, 50)
```

## 设置行可见性 {#SetRowVisible}

```go
func (f *File) SetRowVisible(sheet string, rowIndex int, visible bool)
```

根据给定的工作表名称（大小写敏感）和行号设置行可见性。例如隐藏名为 `Sheet1` 工作表上第二行：

```go
xlsx.SetRowVisible("Sheet1", 2, false)
```

## 获取工作表名 {#GetSheetName}

```go
func (f *File) GetSheetName(index int) string
```

根据给定的工作表索引获取工作表名称，如果工作表不存在将返回空字符。

## 获取列可见性 {#GetColVisible}

```go
func (f *File) GetColVisible(sheet, column string) bool
```

根据给定的工作表名称（大小写敏感）和列名获取工作表中指定列的可见性，可见返回值为 `true`，否则为 `false`。例如，获取名为 `Sheet1` 的工作表上 `D` 列的可见性：

```go
xlsx.GetColVisible("Sheet1", "D")
```

## 获取列宽度 {#GetColWidth}

```go
func (f *File) GetColWidth(sheet, column string) float64
```

根据给定的工作表和列名获取工作表中指定列的宽度。

## 获取行高度 {#GetRowHeight}

```go
func (f *File) GetRowHeight(sheet string, row int) float64
```

根据给定的工作表名称（大小写敏感）和行号获取工作表中指定行的高度。例如，获取名为 `Sheet1` 的工作表首行的高度：

```go
xlsx.GetRowHeight("Sheet1", 1)
```

## 获取行可见性 {#GetRowVisible}

```go
func (f *File) GetRowVisible(sheet string, rowIndex int) bool
```

根据给定的工作表名称（大小写敏感）和行号获取工作表中指定行的可见性。例如，获取名为 `Sheet1` 的工作表第 2 行的可见性：

```go
xlsx.GetRowVisible("Sheet1", 2)
```

## 获取工作表索引 {#GetSheetIndex}

```go
func (f *File) GetSheetIndex(name string) int
```

根据给定的工作表名称（大小写敏感）获取该工作表的索引，如果工作表不存在将返回 `0`。获取到的索引可以在设置工作簿默认工作表时，作为调用 [`SetActiveSheet()`](workbook.md#SetActiveSheet) 函数的参数使用。

## 获取工作表列表  {#GetSheetMap}

```go
func (f *File) GetSheetMap() map[int]string
```

获取工作簿中以名称和索引构成的全部工作表的列表。

```go
xlsx, err := excelize.OpenFile("./Book1.xlsx")
if err != nil {
    return
}
for index, name := range xlsx.GetSheetMap() {
    fmt.Println(index, name)
}
```

## 获取工作表属性 {#GetSheetPrOptions}

```go
func (f *File) GetSheetPrOptions(name string, opts ...SheetPrOptionPtr) error
```

根据给定的工作表名称（大小写敏感）和筛选想获取工作表属性。

|可选属性|类型|
|---|---|
|CodeName|string|
|EnableFormatConditionsCalculation|bool|
|Published|bool|
|FitToPage|bool|
|AutoPageBreaks|bool|
|OutlineSummaryBelow|bool|

例如：

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

输出：

```text
Defaults:
- codeName: ""
- enableFormatConditionsCalculation: true
- published: true
- fitToPage: false
- autoPageBreaks: false
- outlineSummaryBelow: true
```

## 插入列 {#InsertCol}

```go
func (f *File) InsertCol(sheet, column string)
```

根据给定的工作表名称（大小写敏感）和列名称，在指定列前插入空白列。例如，在名为 `Sheet1` 的工作表的 `C` 列前插入空白列：

```go
xlsx.InsertCol("Sheet1", "C")
```

## 插入行 {#InsertRow}

```go
func (f *File) InsertRow(sheet string, row int)
```

根据给定的工作表名称（大小写敏感）和行索引，在指定行前插入空白行。例如，在名为 `Sheet1` 的工作表的第 3 行前插入空白行：

```go
xlsx.InsertRow("Sheet1", 2)
```

## 追加复制行 {#DuplicateRow}

```go
func (f *File) DuplicateRow(sheet string, row int)
```

根据给定的工作表名称（大小写敏感）和行号，在该行后追加复制。例如，将名为 `Sheet1` 的工作表的第 2 行复制到第 3 行：

```go
xlsx.DuplicateRow("Sheet1", 2)
```

## 复制行 {#DuplicateRowTo}

```go
func (f *File) DuplicateRowTo(sheet string, row, row2 int)
```

根据给定的工作表名称（大小写敏感）和行号，在指定行后复制该行。例如，将名为 `Sheet1` 的工作表的第 2 行后复制到第 7 行：

```go
xlsx.DuplicateRowTo("Sheet1", 2, 7)
```

## 创建行的分级显示 {#SetRowOutlineLevel}

```go
func (f *File) SetRowOutlineLevel(sheet string, rowIndex int, level uint8)
```

根据给定的工作表名称（大小写敏感）、行索引和分级参数创建组。例如，在名为 `Sheet1` 的工作表的第 2 行创建 1 级分组。

!["创建行的分级显示"](./images/row_outline_level.png "创建行的分级显示")

```go
xlsx.SetRowOutlineLevel("Sheet1", 2, 1)
```

## 创建列的分级显示 {#SetColOutlineLevel}

```go
func (f *File) SetColOutlineLevel(sheet, column string, level uint8)
```

根据给定的工作表名称（大小写敏感）、列名称和分级参数创建组。例如，在名为 `Sheet1` 的工作表的 `D` 列创建 2 级分组。

!["创建列的分级显示"](./images/col_outline_level.png "创建列的分级显示")

```go
xlsx.SetColOutlineLevel("Sheet1", "D", 2)
```

## 获取行的分级显示 {#GetRowOutlineLevel}

```go
func (f *File) GetRowOutlineLevel(sheet string, rowIndex int) uint8
```

根据给定的工作表名称（大小写敏感）和行索引获取分组级别。例如，获取名为 `Sheet1` 的工作表第 2 行的分组级别。

```go
xlsx.GetRowOutlineLevel("Sheet1", 2)
```

## 获取列的分级显示 {#GetColOutlineLevel}

```go
func (f *File) GetColOutlineLevel(sheet, column string) uint8
```

根据给定的工作表名称（大小写敏感）和列名称获取分组分级。例如，获取名为 `Sheet1` 的工作表的 `D` 列的分组级别。

```go
xlsx.GetColOutlineLevel("Sheet1", "D")
```

## 行迭代器 {#Rows}

```go
func (f *File) Rows(sheet string) (*Rows, error)
```

根据给定的工作表名称（大小写敏感）获取该工作表的行迭代器。使用行迭代器遍历单元格：

```go
rows, err := xlsx.Rows("Sheet1")
for rows.Next() {
    for _, colCell := range rows.Columns() {
        fmt.Print(colCell, "\t")
    }
    fmt.Println()
}
```

### 行迭代器 - 单行操作

```go
func (rows *Rows) Columns() []string
```

返回当前行所有列的值。

### 行迭代器 - 遍历操作

```go
func (rows *Rows) Next() bool
```

如果下一行有值存在将返回 `true`。

### 行迭代器 - 错误处理

```go
func (rows *Rows) Error() error
```

当查找下一行出现错误时将返回 `error`。

## 在工作表中搜索 {#SearchSheet}

```go
func (f *File) SearchSheet(sheet, value string, reg ...bool) []string
```

根据给定的工作表名称（大小写敏感），单元格值或正则表达式来获取坐标。此函数仅支持字符串和数字的完全匹配，不支持公式计算后的结果、格式化数字和条件搜索。如果搜索结果是合并的单元格，将返回合并区域左上角的坐标。

例如，在名为 `Sheet1` 的工作表中搜索值 `100` 的坐标:

```go
xlsx.SearchSheet("Sheet1", "100")
```

例如，在名为 `Sheet1` 的工作表中搜索 `0-9` 范围内数值的坐标:

```go
xlsx.SearchSheet("Sheet1", "[0-9]", true)
```

## 保护工作表 {#ProtectSheet}

```go
func (f *File) ProtectSheet(sheet string, settings *FormatSheetProtection)
```

防止其他用户意外或有意更改、移动或删除工作表中的数据。例如，为名为 `Sheet1` 的工作表设置密码保护，但是允许选择锁定的单元格、选择未锁定的单元格、编辑方案：

!["保护工作表"](./images/protect_sheet.png "保护工作表")

```go
xlsx.ProtectSheet("Sheet1", &excelize.FormatSheetProtection{
    Password:      "password",
    EditScenarios: false,
})
```

## 取消保护工作表 {#UnprotectSheet}

```go
func (f *File) UnprotectSheet(sheet string)
```

根据给定的工作表名称（大小写敏感）取消保护该工作表。
