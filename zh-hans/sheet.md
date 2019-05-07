# 工作表

## 设置列可见性 {#SetColVisible}

```go
func (f *File) SetColVisible(sheet, col string, visible bool) error
```

根据给定的工作表名称（大小写敏感）和列名称设置列可见性。例如隐藏名为 `Sheet1` 工作表上的 `D` 列：

```go
err := f.SetColVisible("Sheet1", "D", false)
```

## 设置列宽度 {#SetColWidth}

```go
func (f *File) SetColWidth(sheet, startcol, endcol string, width float64) error
```

根据给定的工作表名称（大小写敏感）、列范围和宽度值设置单个或多个列的宽度。例如设置名为 `Sheet1` 工作表上 `A` 到 `H` 列的宽度为 `20`：

```go
f := excelize.NewFile()
err := f.SetColWidth("Sheet1", "A", "H", 20)
```

## 设置行高度 {#SetRowHeight}

```go
func (f *File) SetRowHeight(sheet string, row int, height float64) error
```

根据给定的工作表名称（大小写敏感）、行号和高度值设置单行高度。例如设置名为 `Sheet1` 工作表首行的高度为 `50`：

```go
err := f.SetRowHeight("Sheet1", 1, 50)
```

## 设置行可见性 {#SetRowVisible}

```go
func (f *File) SetRowVisible(sheet string, row int, visible bool) error
```

根据给定的工作表名称（大小写敏感）和行号设置行可见性。例如隐藏名为 `Sheet1` 工作表上第二行：

```go
err := f.SetRowVisible("Sheet1", 2, false)
```

## 获取工作表名 {#GetSheetName}

```go
func (f *File) GetSheetName(index int) string
```

根据给定的工作表索引获取工作表名称，如果工作表不存在将返回空字符。

## 获取列可见性 {#GetColVisible}

```go
func (f *File) GetColVisible(sheet, column string) (bool, error)
```

根据给定的工作表名称（大小写敏感）和列名获取工作表中指定列的可见性，可见返回值为 `true`，否则为 `false`。例如，获取名为 `Sheet1` 的工作表上 `D` 列的可见性：

```go
visible, err := f.GetColVisible("Sheet1", "D")
```

## 获取列宽度 {#GetColWidth}

```go
func (f *File) GetColWidth(sheet, col string) (float64, error)
```

根据给定的工作表和列名获取工作表中指定列的宽度。

## 获取行高度 {#GetRowHeight}

```go
func (f *File) GetRowHeight(sheet string, row int) (float64, error)
```

根据给定的工作表名称（大小写敏感）和行号获取工作表中指定行的高度。例如，获取名为 `Sheet1` 的工作表首行的高度：

```go
height, err := f.GetRowHeight("Sheet1", 1)
```

## 获取行可见性 {#GetRowVisible}

```go
func (f *File) GetRowVisible(sheet string, row int) (bool, error)
```

根据给定的工作表名称（大小写敏感）和行号获取工作表中指定行的可见性。例如，获取名为 `Sheet1` 的工作表第 2 行的可见性：

```go
err := f.GetRowVisible("Sheet1", 2)
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
f, err := excelize.OpenFile("./Book1.xlsx")
if err != nil {
    return
}
for index, name := range f.GetSheetMap() {
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
f := excelize.NewFile()
const sheet = "Sheet1"

var (
    codeName                          excelize.CodeName
    enableFormatConditionsCalculation excelize.EnableFormatConditionsCalculation
    published                         excelize.Published
    fitToPage                         excelize.FitToPage
    autoPageBreaks                    excelize.AutoPageBreaks
    outlineSummaryBelow               excelize.OutlineSummaryBelow
)

if err := f.GetSheetPrOptions(sheet,
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
func (f *File) InsertCol(sheet, column string) error
```

根据给定的工作表名称（大小写敏感）和列名称，在指定列前插入空白列。例如，在名为 `Sheet1` 的工作表的 `C` 列前插入空白列：

```go
err := f.InsertCol("Sheet1", "C")
```

## 插入行 {#InsertRow}

```go
func (f *File) InsertRow(sheet string, row int) error
```

根据给定的工作表名称（大小写敏感）和行号，在指定行前插入空白行。例如，在名为 `Sheet1` 的工作表的第 3 行前插入空白行：

```go
err := f.InsertRow("Sheet1", 3)
```

## 追加复制行 {#DuplicateRow}

```go
func (f *File) DuplicateRow(sheet string, row int) error
```

根据给定的工作表名称（大小写敏感）和行号，在该行后追加复制。例如，将名为 `Sheet1` 的工作表的第 2 行复制到第 3 行：

```go
err := f.DuplicateRow("Sheet1", 2)
```

请谨慎使用此方法，这将影响所有对该工作表中原有公式、图表等资源引用的更改。如果该工作表包含任何引用值，在使用此方法后使用 Excel 应用程序打开它时将可能导致文件错误。excelize 目前仅支持对工作表上部分引用对更新。

## 复制行 {#DuplicateRowTo}

```go
func (f *File) DuplicateRowTo(sheet string, row, row2 int) error
```

根据给定的工作表名称（大小写敏感）和行号，在指定行后复制该行。例如，将名为 `Sheet1` 的工作表的第 2 行后复制到第 7 行：

```go
err := f.DuplicateRowTo("Sheet1", 2, 7)
```

请谨慎使用此方法，这将影响所有对该工作表中原有公式、图表等资源引用的更改。如果该工作表包含任何引用值，在使用此方法后使用 Excel 应用程序打开它时将可能导致文件错误。excelize 目前仅支持对工作表上部分引用对更新。

## 创建行的分级显示 {#SetRowOutlineLevel}

```go
func (f *File) SetRowOutlineLevel(sheet string, row int, level uint8) error
```

根据给定的工作表名称（大小写敏感）、行号和分级参数创建组。例如，在名为 `Sheet1` 的工作表的第 2 行创建 1 级分组。

<p align="center"><img width="612" src="./images/row_outline_level.png" alt="创建行的分级显示"></p>

```go
err := f.SetRowOutlineLevel("Sheet1", 2, 1)
```

## 创建列的分级显示 {#SetColOutlineLevel}

```go
func (f *File) SetColOutlineLevel(sheet, col string, level uint8) error
```

根据给定的工作表名称（大小写敏感）、列名称和分级参数创建组。例如，在名为 `Sheet1` 的工作表的 `D` 列创建 2 级分组。

<p align="center"><img width="612" src="./images/col_outline_level.png" alt="创建列的分级显示"></p>

```go
err := f.SetColOutlineLevel("Sheet1", "D", 2)
```

## 获取行的分级显示 {#GetRowOutlineLevel}

```go
func (f *File) GetRowOutlineLevel(sheet string, row int) (uint8, error)
```

根据给定的工作表名称（大小写敏感）和行号获取分组级别。例如，获取名为 `Sheet1` 的工作表第 2 行的分组级别。

```go
err := f.GetRowOutlineLevel("Sheet1", 2)
```

## 获取列的分级显示 {#GetColOutlineLevel}

```go
func (f *File) GetColOutlineLevel(sheet, col string) (uint8, error)
```

根据给定的工作表名称（大小写敏感）和列名称获取分组分级。例如，获取名为 `Sheet1` 的工作表的 `D` 列的分组级别。

```go
level, err := f.GetColOutlineLevel("Sheet1", "D")
```

## 行迭代器 {#Rows}

```go
func (f *File) Rows(sheet string) (*Rows, error)
```

根据给定的工作表名称（大小写敏感）获取该工作表的行迭代器。使用行迭代器遍历单元格：

```go
rows, err := f.Rows("Sheet1")
for rows.Next() {
   row, err := rows.Columns()
   for _, colCell := range row {
       fmt.Print(colCell, "\t")
   }
   fmt.Println()
}
```

### 行迭代器 - 单行操作

```go
func (rows *Rows) Columns() ([]string, error)
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
func (f *File) SearchSheet(sheet, value string, reg ...bool) ([]string, error)
```

根据给定的工作表名称（大小写敏感），单元格值或正则表达式来获取坐标。此函数仅支持字符串和数字的完全匹配，不支持公式计算后的结果、格式化数字和条件搜索。如果搜索结果是合并的单元格，将返回合并区域左上角的坐标。

例如，在名为 `Sheet1` 的工作表中搜索值 `100` 的坐标:

```go
result, err := f.SearchSheet("Sheet1", "100")
```

例如，在名为 `Sheet1` 的工作表中搜索 `0-9` 范围内数值的坐标:

```go
result, err := f.SearchSheet("Sheet1", "[0-9]", true)
```

## 保护工作表 {#ProtectSheet}

```go
func (f *File) ProtectSheet(sheet string, settings *FormatSheetProtection) error
```

防止其他用户意外或有意更改、移动或删除工作表中的数据。例如，为名为 `Sheet1` 的工作表设置密码保护，但是允许选择锁定的单元格、选择未锁定的单元格、编辑方案：

<p align="center"><img width="790" src="./images/protect_sheet.png" alt="保护工作表"></p>

```go
err := f.ProtectSheet("Sheet1", &excelize.FormatSheetProtection{
    Password:      "password",
    EditScenarios: false,
})
```

## 取消保护工作表 {#UnprotectSheet}

```go
func (f *File) UnprotectSheet(sheet string) error
```

根据给定的工作表名称（大小写敏感）取消保护该工作表。
