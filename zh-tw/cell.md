# 儲存格

`RichTextRun` 定義了富文本的屬性。

```go
type RichTextRun struct {
    Font *Font
    Text string
}
```

`HyperlinkOpts` 用來指定可選的超鏈接屬性，例如要顯示的文字與屏幕提示文字。

```go
type HyperlinkOpts struct {
    Display *string
    Tooltip *string
}
```

`FormulaOpts` 用於在 [`SetCellFormula`](cell.md#SetCellFormula) 函式中指定設定特殊公式類型。

```go
type FormulaOpts struct {
    Type *string // 公式類型
    Ref  *string // 共享公式引用
}
```

## 設定儲存格的值 {#SetCellValue}

```go
func (f *File) SetCellValue(sheet, cell string, value interface{}) error
```

根據給定的工作表名和儲存格坐標設定儲存格的值。此功能是併發安全的。指定的坐標不應在表格的第一列範圍，使用字符文本設定複數。

|支持的資料類別|
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

請注意，此函式默認為 `time.Time` 類型的存儲格的值設定 `m/d/yy h:mm` 數字格式，您可透過 [`SetCellStyle`](cell.md#SetCellStyle) 更改該設定。若您需設定無法透過 Go 語言 `time.Time` 類型表示的 Excel 特殊日期，例如 1900 年 1 月 0 日或 1900 年 2 月 29 日，請先設定存儲格的值為 0 或 60，再為其設定具有日期數字格式的樣式。

## 設定布林型值 {#SetCellBool}

```go
func (f *File) SetCellBool(sheet, cell string, value bool) error
```

根據給定的工作表名和儲存格坐標設定布林型儲存格的值。

## 設定默認字符型值 {#SetCellDefault}

```go
func (f *File) SetCellDefault(sheet, cell, value string) error
```

根據給定的工作表名和儲存格坐標設定字符型儲存格的值，字符將不會進行特殊字符過濾。

## 設定整數 {#SetCellInt}

```go
func (f *File) SetCellInt(sheet, cell string, value int) error
```

根據給定的工作表名和儲存格坐標設定整數儲存格的值。

## 設定浮點數 {#SetCellFloat}

```go
func (f *File) SetCellFloat(sheet, cell string, value float64, precision, bitSize int) error
```

根據給定的工作表名、儲存格坐標、浮點數、浮點數尾數部分精度和浮點數類型設定浮點型存儲格的值。

## 設定字符型值 {#SetCellStr}

```go
func (f *File) SetCellStr(sheet, cell, value string) error
```

根據給定的工作表名和儲存格坐標設定字符型儲存格的值，字符將會進行特殊字符過濾，並且字符串的累計長度應不超過 `32767`，多餘的字符將會被忽略。

## 設定儲存格樣式 {#SetCellStyle}

```go
func (f *File) SetCellStyle(sheet, hCell, vCell string, styleID int) error
```

根據給定的工作表名、儲存格坐標區域和樣式索引設定儲存格的值。此功能是併發安全的。樣式索引可以透過 [`NewStyle`](style.md#NewStyle) 函式獲取。注意，在同一個坐標區域內的 `diagonalDown` 和 `diagonalUp` 需要保持色彩一致。SetCellStyle 將覆蓋存儲格的已有樣式，而不會將樣式與已有樣式疊加或合併。

- 例1，為名為 `Sheet1` 的工作表 `D7` 儲存格設定外框樣式：

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

<p align="center"><img width="612" src="./images/SetCellStyle_01.png" alt="為儲存格設定外框樣式"></p>

儲存格 `D7` 的四個外框被設定了不同的樣式和色彩，這與調用 [`NewStyle`](style.md#NewStyle) 函式時的參數有關，需要設定不同的樣式可參考該章節的文檔。

- 例2，為名為 `Sheet1` 的工作表 `D7` 儲存格設定漸變樣式：

```go
style, err := f.NewStyle(&excelize.Style{
    Fill: excelize.Fill{Type: "gradient", Color: []string{"FFFFFF", "E0EBF5"}, Shading: 1},
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_02.png" alt="為儲存格設定漸變樣式"></p>

儲存格 `D7` 被設定了漸變效果的色彩填滿，漸變填滿效果與調用 [`NewStyle`](style.md#NewStyle) 函式時的參數有關，需要設定不同的樣式可參考該章節的文檔。

- 例3，為名為 `Sheet1` 的工作表 `D7` 儲存格設定純色填滿：

```go
style, err := f.NewStyle(&excelize.Style{
    Fill: excelize.Fill{Type: "pattern", Color: []string{"E0EBF5"}, Pattern: 1},
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_03.png" alt="為儲存格設定純色填滿"></p>

儲存格 `D7` 被設定了純色填滿。

- 例4，為名為 `Sheet1` 的工作表 `D7` 儲存格設定字符間距與旋轉角度：

```go
f.SetCellValue("Sheet1", "D7", "樣式")
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

<p align="center"><img width="612" src="./images/SetCellStyle_04.png" alt="設定字符間距與旋轉角度"></p>

- 例5，Excel 中的日期和時間用實數表示，例如 `2017/7/4  12:00:00 PM` 可以用數字 `42920.5` 來表示。為名為 `Sheet1` 的工作表 `D7` 儲存格設定時間格式：

```go
f.SetCellValue("Sheet1", "D7", 42920.5)
f.SetColWidth("Sheet1", "D", "D", 13)
style, err := f.NewStyle(&excelize.Style{NumFmt: 22})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_05.png" alt="為儲存格設定時間格式"></p>

儲存格 `D7` 被設定了時間格式。注意，當應用了時間格式的儲存格寬度過窄無法完整展示時會顯示為 `####`，可以拖拽調整欄寬或者透過調用 `SetColWidth` 函式設定欄寬到合適的大小使其正常顯示。

- 例6，為名為 `Sheet1` 的工作表 `D7` 儲存格設定字型、字號、色彩和傾斜樣式：

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

<p align="center"><img width="612" src="./images/SetCellStyle_06.png" alt="為儲存格設定字型、字號、色彩和傾斜樣式"></p>

- 例7，鎖定並隱藏名為 `Sheet1` 的工作表 `D7` 儲存格：

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

要鎖定儲存格或隱藏公式，請保護工作表。在「審閱」選項卡上，單擊「保護工作表」。

## 設定超鏈接 {#SetCellHyperLink}

```go
func (f *File) SetCellHyperLink(sheet, cell, link, linkType string, opts ...HyperlinkOpts) error
```

根據給定的工作表、儲存格坐標、鏈接資源和資源類別設定儲存格的超鏈接。資源類別分為外部鏈接地址 `External` 和活頁簿內部位置鏈接 `Location` 兩種。每個工作表中的包含最大超鏈接限制為 `65530` 個。該方法僅設定存儲格的超鏈接而不影響存儲格的值，若需設定存儲格的值，請透過 [`SetCellStyle`](cell.md#SetCellStyle) 或 [`SetSheetRow`](sheet.md#SetSheetRow) 等函式另行設定。

- 例1，為名為 `Sheet1` 的工作表 `A3` 儲存格添加外部鏈接：

```go
display, tooltip := "https://github.com/xuri/excelize", "Excelize on GitHub"
if err := f.SetCellHyperLink("Sheet1", "A3",
    "https://github.com/xuri/excelize", "External", excelize.HyperlinkOpts{
        Display: &display,
        Tooltip: &tooltip,
    }); err != nil {
    fmt.Println(err)
}
// 為儲存格設定字型和底線樣式
style, err := f.NewStyle(&excelize.Style{
    Font: &excelize.Font{Color: "1265BE", Underline: "single"},
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "A3", "A3", style)
```

- 例2，為名為 `Sheet1` 的工作表 `A3` 儲存格添加內部位置鏈接：

```go
err := f.SetCellHyperLink("Sheet1", "A3", "Sheet1!A40", "Location")
```

## 設定富文本格式 {#SetCellRichText}

```go
func (f *File) SetCellRichText(sheet, cell string, runs []RichTextRun) error
```

根據給定的工作表、儲存格坐標和富文本格式為指定儲存格設定富文本。

例如，在名為 `Sheet1` 的工作表 `A1` 儲存格設定富文本格式：

<p align="center"><img width="612" src="./images/rich_text.png" alt="設定富文本格式"></p>

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

## 獲取富文本格式 {#GetCellRichText}

```go
func (f *File) GetCellRichText(sheet, cell string) ([]RichTextRun, error)
```

根據給定的工作表、儲存格坐標獲取指定儲存格的富文本格式。

## 獲取儲存格的值 {#GetCellValue}

```go
func (f *File) GetCellValue(sheet, cell string, opts ...Options) (string, error)
```

根據給定的工作表和儲存格坐標獲取儲存格的值，傳回值將轉換為 `string` 類別。此功能是併發安全的。如果可以將儲存格格式應用於儲存格的值，將傳回應用後的值，否則將傳回原始值。合併區域內所有儲存格的值都相同。

## 獲取存儲格數據類型 {#GetCellType}

```go
func (f *File) GetCellType(sheet, cell string) (CellType, error)
```

根據給定的工作表、儲存格坐標獲取指定儲存格的數據類型。

## 按欄獲取全部儲存格的值 {#GetCols}

```go
func (f *File) GetCols(sheet string, opts ...Options) ([][]string, error)
```

根據給定的工作表名按欄獲取該工作表上全部儲存格的值，以二維數組形式傳回，其中儲存格的值將轉換為 `string` 類別。如果可以將儲存格格式應用於儲存格的值，將使用應用後的值，否則將使用原始值。

例如，按欄獲取並遍歷輸出名為 `Sheet1` 的工作表上的所有儲存格的值：

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

## 按列獲取全部儲存格的值 {#GetRows}

```go
func (f *File) GetRows(sheet string, opts ...Options) ([][]string, error)
```

根據給定的工作表名按列獲取該工作表上全部儲存格的值，以二維數組形式傳回，其中儲存格的值將轉換為 `string` 類別。如果可以將儲存格格式應用於儲存格的值，將使用應用後的值，否則將使用原始值。GetRows 獲取帶有值或公式存儲格的列，列尾連續為空的存儲格將被跳過，每列中的存儲格數目可能不同。

例如，按列獲取並遍歷輸出名為 `Sheet1` 的工作表上的所有儲存格的值：

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

## 獲取超鏈接 {#GetCellHyperLink}

```go
func (f *File) GetCellHyperLink(sheet, cell string) (bool, string, error)
```

根據給定的工作表名和儲存格坐標獲取儲存格超鏈接，如果該儲存格存在超鏈接，將傳回 `true` 和鏈接地址，否則將傳回 `false` 和空的鏈接地址。

例如，獲取名為 `Sheet1` 的工作表上坐標為 `H6` 儲存格的超鏈接：

```go
link, target, err := f.GetCellHyperLink("Sheet1", "H6")
```

## 獲取樣式索引 {#GetCellStyle}

```go
func (f *File) GetCellStyle(sheet, cell string) (int, error)
```

根據給定的工作表名和儲存格坐標獲取儲存格樣式索引，獲取到的索引可以在設定儲存格樣式時，作為調用 `SetCellStyle` 函式的參數使用。

## 合併儲存格 {#MergeCell}

```go
func (f *File) MergeCell(sheet, hCell, vCell string) error
```

根據給定的工作表名和儲存格坐標區域合併儲存格。合併區域內僅保留左上角儲存格的值，其他儲存格的值將被忽略。例如，合併名為 `Sheet1` 的工作表上 `D3:E9` 區域內的儲存格：

```go
err := f.MergeCell("Sheet1", "D3", "E9")
```

如果給定的儲存格坐標區域與已有的其他合併儲存格相重疊，已有的合併儲存格將會被刪除。

## 取消合併儲存格 {#UnmergeCell}

```go
func (f *File) UnmergeCell(sheet string, hCell, vCell string) error
```

根據給定的工作表名和儲存格坐標區域取消合併儲存格。例如，取消合併名為 `Sheet1` 的工作表上 `D3:E9` 區域內的儲存格：

```go
err := f.UnmergeCell("Sheet1", "D3", "E9")
```

如果給定的儲存格坐標區域包含多個合併儲存格，則全部合併儲存格都將被取消合併。

## 獲取合併儲存格 {#GetMergeCells}

根據給定的工作表名獲取全部合併儲存格的坐標區域和值。

```go
func (f *File) GetMergeCells(sheet string) ([]MergeCell, error)
```

### 獲取合併存儲格的值

```go
func (m *MergeCell) GetCellValue() string
```

GetCellValue 返回合併存儲格的值。

### 獲取合併存儲格區域左上角存儲格坐標

```go
func (m *MergeCell) GetStartAxis() string
```

GetStartAxis 返回合併存儲格區域左上角存儲格的坐標，例如：`C2`。

### 獲取合併存儲格區域右下角存儲格坐標

```go
func (m *MergeCell) GetEndAxis() string
```

GetEndAxis 返回合併存儲格區域右下角存儲格的坐標，例如：`D4`。

## 添加註解 {#AddComment}

```go
func (f *File) AddComment(sheet string, comment Comment) error
```

根據給定的工作表名稱、儲存格坐標和樣式參數（作者與文本信息）添加註解。作者信息最大長度為 255 個字符，最大文本內容長度為 32512 個字符，超出該範圍的字符將會被忽略。例如，為 `Sheet1!$A$3` 儲存格添加註解：

<p align="center"><img width="612" src="./images/comment.png" alt="在 Excel 文檔中添加註解"></p>

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

## 獲取註解 {#GetComments}

```go
func (f *File) GetComments(sheet string) ([]Comment, error)
```

根據給定的工作表名稱獲取工作表中的所有存儲格註解。

## 刪除註解 {#DeleteComment}

```go
func (f *File) DeleteComment(sheet, cell string) error
```

根據給定的工作表名稱、儲存格坐標刪除註解。例如，刪除 `Sheet1!$A$30` 儲存格註解：

```go
err := f.DeleteComment("Sheet1", "A30")
```

## 設定公式 {#SetCellFormula}

```go
func (f *File) SetCellFormula(sheet, cell, formula string, opts ...FormulaOpts) error
```

根據給定的工作表名和儲存格坐標設定該儲存格上的公式。公式的結果會在工作表被 Office Excel 應用程式開啓時計算，或透過 [CalcCellValue](cell.md#CalcCellValue) 函式計算存儲格的值。若 Excel 應用程式開啓活頁簿後未對設定的存儲格公式進行計算，請在設定公式後調用 [UpdateLinkedValue](utils.md#UpdateLinkedValue) 清除存儲格緩存。

- 例1，為名為 `Sheet1` 的工作表 `A3` 存儲格設定普通公式 `=SUM(A1,B1)`：

```go
err := f.SetCellFormula("Sheet1", "A3", "=SUM(A1,B1)")
```

- 例2，為名為 `Sheet1` 的工作表 `A3` 存儲格設定一維縱向常量數組（欄數組）公式 `1;2;3`:

```go
err := f.SetCellFormula("Sheet1", "A3", "={1;2;3}")
```

- 例3，為名為 `Sheet1` 的工作表 `A3` 存儲格設定一維橫向常量數組（列數組）公式 `"a","b","c"`:

```go
err := f.SetCellFormula("Sheet1", "A3", "={\"a\",\"b\",\"c\"}")
```

- 例4，為名為 `Sheet1` 的工作表 `A3` 存儲格設定二維常量數組公式 `{1,2;"a","b"}`:

```go
formulaType, ref := excelize.STCellFormulaTypeArray, "A3:A3"
err := f.SetCellFormula("Sheet1", "A3", "={1,2;\"a\",\"b\"}",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- 例5，為名為 `Sheet1` 的工作表 `A3` 存儲格設定區域數組公式 `A1:A2`:

```go
formulaType, ref := excelize.STCellFormulaTypeArray, "A3:A3"
err := f.SetCellFormula("Sheet1", "A3", "=A1:A2",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- 例6，為名為 `Sheet1` 的工作表 `C1:C5` 區域的存儲格設定共享公式 `=A1+B1`，其中 `C1` 為主存儲格:

```go
formulaType, ref := excelize.STCellFormulaTypeShared, "C1:C5"
err := f.SetCellFormula("Sheet1", "C1", "=A1+B1",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- 例7，為名為 `Sheet1` 的工作表 `C2` 存儲格設定表格公式 `=SUM(Table1[[A]:[B]])`:

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

## 獲取公式 {#GetCellFormula}

```go
func (f *File) GetCellFormula(sheet, cell string) (string, error)
```

根據給定的工作表名和儲存格坐標獲取該儲存格上的公式。

## 計算存儲格的值 {#CalcCellValue}

```go
func (f *File) CalcCellValue(sheet, cell string, opts ...Options) (string, error)
```

根據給定的工作表名和存儲格坐標計算包含公式存儲格的值。該方法目前正在開發中，尚未支持反覆運算、隱式交集、顯式交集、數組函式、數組函式、表格函式和其他部分函式。

支持的公式函式列表如下：

函式名稱 | 描述
---|---
ABS                      | 傳回數字的絕對值
ACCRINT                  | 傳回支付定期利息之債券的應計利息
ACCRINTM                 | 傳回到期時支付利息之債券的應計利息
ACOS                     | 傳回數字的反餘弦
ACOSH                    | 傳回數字的反雙曲餘弦
ACOT                     | 傳回數字的反餘切
ACOTH                    | 傳回數字的雙曲餘切
AGGREGATE                | 傳回清單或資料庫的彙總
ADDRESS                  | 以文字格式傳回參照至工作表中的單一儲存格
AMORDEGRC                | 傳回每個會計週期的折舊，使用折舊係數
AMORLINC                 | 傳回每個會計週期的折舊
AND                      | 如果其所有引數都為 TRUE，則傳回 TRUE
ARABIC                   | 將羅馬數字轉換為阿拉伯數字
ARRAYTOTEXT              | 傳回任何指定範圍內的文字值陣列
ASIN                     | 傳回數字的反正弦
ASINH                    | 傳回數字的反雙曲正弦
ATAN                     | 傳回數字的反正切
ATAN2                    | 從 x 和 y 座標傳回反正切值
ATANH                    | 傳回數字的反雙曲正切
AVEDEV                   | 會從資料點的平均值中傳回資料點的平均絕對差
AVERAGE                  | 傳回其引數的平均值
AVERAGEA                 | 傳回其引數的平均值，包括數字、文字和邏輯值
AVERAGEIF                | 傳回符合指定準則的範圍中所有儲存格的平均 (算術平均數)
AVERAGEIFS               | 傳回符合多個準則的所有儲存格的平均 (算術平均數)
BASE                     | 將數字轉換為具有指定基數 (底數) 的文字表示
BESSELI                  | 傳回修正 Bessel 函式 In(x)
BESSELJ                  | 傳回 Bessel 函式 Jn(x)
BESSELK                  | 傳回修正 Bessel 函式 Kn(x)
BESSELY                  | 傳回 Bessel 函式 Yn(x)
BETADIST                 | 傳回 Beta 累加分配函式
BETA.DIST                | 傳回 Beta 累加分配函式
BETAINV                  | 傳回指定 Beta 分配累加分配函式的反函式
BETA.INV                 | 傳回指定 Beta 分配累加分配函式的反函式
BIN2DEC                  | 將二進位數字轉換為十進位
BIN2HEX                  | 將二進位數字轉換為十六進位
BIN2OCT                  | 將二進位數字轉換為八進位
BINOMDIST                | 傳回特定次數的二項式分佈機率
BINOM.DIST               | 傳回特定次數的二項式分佈機率
BINOM.DIST.RANGE         | 傳回使用二項分配試驗結果的機率
BINOM.INV                | 傳回累加二項式分佈小於或等於臨界值的最小值
BITAND                   | 傳回兩個數字的「位元 And」
BITLSHIFT                | 傳回向左位移 shift_amount 位元的值數字
BITOR                    | 傳回 2 個數字的位元 OR
BITRSHIFT                | 傳回向右位移 shift_amount 位元的值數字
BITXOR                   | 傳回兩個數字的位元「互斥 Or」
CEILING                  | 將數字四捨五入至最接近的整數或最接近的比較基數倍數
CEILING.MATH             | 將數字四捨五入至最接近的整數，或四捨五入為最接近的基數倍數
CEILING.PRECISE          | 將數字四捨五入至最接近的整數，或四捨五入至最接近的基數倍數。不論數字正負號，數字都會四捨五入
CHAR                     | 傳回代碼所指定的字元
CHIDIST                  | 傳回卡方分佈的單側機率
CHIINV                   | 傳回卡方分佈單側機率的反函式
CHITEST                  | 傳回獨立性檢定的結果
CHISQ.DIST               | 傳回累加 beta 機率密度函式
CHISQ.DIST.RT            | 傳回卡方分佈的單側機率
CHISQ.INV                | 傳回累加 beta 機率密度函式
CHISQ.INV.RT             | 傳回卡方分佈單側機率的反函式
CHISQ.TEST               | 傳回獨立性檢定的結果
CHOOSE                   | 從值清單選取一個值
CLEAN                    | 移除文字中所有無法列印的字元
CODE                     | 傳回文字字串中第一個字元的數字碼
COLUMN                   | 傳回參照的資料行編號
COLUMNS                  | 傳回參照的資料行數目
COMBIN                   | 傳回指定物件數的組合數
COMBINA                  | 傳回指定項目數的組合數 (含重複)
COMPLEX                  | 將實係數及虛係數轉換為複數
CONCAT                   | 合併來自多個範圍和/或字串的文字，但它不會提供分隔符號或 IgnoreEmpty 引數
CONCATENATE              | 聯結多個文字項目到一個文字項目
CONFIDENCE               | 傳回母體平均數的信賴區間
CONFIDENCE.NORM          | 傳回母體平均數的信賴區間
CONFIDENCE.T             | 使用 Student T 分配，傳回母體平均數的信賴區間
CONVERT                  | 將數字從一個度量系統轉換到另一個
CORREL                   | 傳回兩個資料集之間的相關係數
COS                      | 傳回數字的餘弦
COSH                     | 傳回數字的雙曲線餘弦
COT                      | 傳回數字的雙曲線餘弦
COTH                     | 傳回角度的餘切值
COUNT                    | 計算引數清單中有多少數字
COUNTA                   | 計算引數清單中有多少值
COUNTBLANK               | 計算範圍內空白儲存格數
COUNTIF                  | 計算符合指定準則範圍內的儲存格數
COUNTIFS                 | 計算符合多個準則範圍內的儲存格數
COUPDAYBS                | 傳回從票息週期的開始到結算日期之間的日數
COUPDAYS                 | 傳回包含結算日期之票息週期中的日數
COUPDAYSNC               | 傳回從結算日期到下一個票息日期之間的日數
COUPNCD                  | 傳回結算日期之後的下一個票息日期
COUPNUM                  | 傳回可在結算日期和到期日期之間支付的票息數字
COUPPCD                  | 傳回結算日期前的上一個票息日期
COVAR                    | 傳回共變數，即成對誤差乘積的平均值
COVARIANCE.P             | 傳回共變數，即成對誤差乘積的平均值
COVARIANCE.S             | 傳回樣本共變數，即兩個資料集中各個成對資料點的乘積誤差平均值
CRITBINOM                | 傳回累加二項式分佈小於或等於臨界值的最小值
CSC                      | 傳回角度的餘割值
CSCH                     | 傳回角度的雙曲餘割值
CUMIPMT                  | 傳回兩個期間之間的累積支付利息
CUMPRINC                 | 傳回兩個期間之間的累積支付本金
DATE                     | 傳回特定日期的序列值
DATEDIF                  | 計算兩個日期之間的日數、月數或年數。若您需要在公式中計算年齡，此函式很有用
DATEVALUE                | 將文字形式的日期轉換為序列值
DAVERAGE                 | 傳回選取資料庫項目的平均值
DAY                      | 將序列值轉換為一月中的某日
DAYS                     | 傳回兩個日期之間的天數
DAYS360                  | 根據一年 360 天計算兩個日期之間的天數
DB                       | 傳回資產在指定期間內使用定率餘額遞減法所計算的折舊
DCOUNT                   | 計算資料庫中包含數字的儲存格
DCOUNTA                  | 計算資料庫中非空白的儲存格
DDB                      | 傳回資產在指定期間內使用倍率餘額遞減法或其他指定方法所計算的折舊
DEC2BIN                  | 將十進位數字轉換為二進位
DEC2HEX                  | 將十進位數字轉換為十六進位
DEC2OCT                  | 將十進位數字轉換為八進位
DECIMAL                  | 將指定基數的數字的文字表示轉換為十進位數字
DEGREES                  | 將弧度轉換為角度
DELTA                    | 測試兩個值是否相等
DEVSQ                    | 傳回偏差的平方和
DGET                     | 從資料庫擷取符合指定準則的單筆記錄
DISC                     | 傳回債券的貼現率
DMAX                     | 傳回選取資料庫項目的最大值
DMIN                     | 傳回選取資料庫項目的最小值
DOLLARDE                 | 將以分數表示的價格轉換為以小數表示
DOLLARFR                 | 將以小數表示的價格轉換為以分數表示
DPRODUCT                 | 將符合資料庫中準則的特定記錄欄位中的值相乘
DSTDEV                   | 根據選取的資料庫項目的樣本來估計標準差
DSTDEVP                  | 根據選取的資料庫項目的整體母體計算標準差
DSUM                     | 將資料庫中符合準則的記錄欄位資料行中的數字相加
DURATION                 | 傳回定期支付利息的債券每年持續時間
DVAR                     | 根據所選資料庫項目的樣本來估計變異數
DVARP                    | 根據選取的資料庫項目的整體母體計算差異
EDATE                    | 傳回開始日期之前或之後的指定月數的日期序列值
EFFECT                   | 傳回有效年利率
ENCODEURL                | 傳回 URL 編碼字串
EOMONTH                  | 傳回指定月數之前或之後的當月最後一天的序列值
ERF                      | 傳回誤差函式
ERF.PRECISE              | 傳回誤差函式
ERFC                     | 傳回補充誤差函式
ERFC.PRECISE             | 傳回 x 和無限之間整合的補充 ERF 函式
ERROR.TYPE               | 傳回對應至錯誤類型的數字
EUROCONVERT              | 用於將數字轉換為歐元形式、將數字由歐元形式轉換為歐元成員國貨幣形式，或利用歐元做為中間貨幣，將數字由某一歐元成員國貨幣轉化為另一歐元成員國貨幣形式
EVEN                     | 將數字四捨五入至最接近的偶數整數
EXACT                    | 檢查兩個文字值是否相同
EXP                      | 傳回 e 的指定次數乘冪
EXPON.DIST               | 傳回指數分佈
EXPONDIST                | 傳回指數分佈
FACT                     | 傳回數字的階乘
FACTDOUBLE               | 傳回數字的雙階乘
FALSE                    | 傳回邏輯值 FALSE
F.DIST                   | 傳回 F 機率分佈
FDIST                    | 傳回 F 機率分佈
F.DIST.RT                | 傳回 F 機率分佈
FIND                     | 在文字值間尋找文字值 (區分大小寫)
FINDB                    | 在文字值間尋找文字值 (區分大小寫)
F.INV                    | 傳回 F 機率分佈的反函式值
F.INV.RT                 | 傳回 F 機率分佈的反函式值
FINV                     | 傳回 F 機率分佈的反函式值
FISHER                   | 傳回 Fisher 轉換
FISHERINV                | 傳回 Fisher 轉換的反函式值
FIXED                    | 將數字格式化為具有固定小數位數字的文字
FLOOR                    | 將數字無條件捨去，趨近於零
FLOOR.MATH               | 將數字無條件捨去至最接近的整數，或無條件捨去至最接近的基數倍數
FLOOR.PRECISE            | 將數字四捨五入至最接近的整數，或四捨五入至最接近的基數倍數。不論數字正負號，數字都會四捨五入
FORECAST                 | 傳回線性趨勢值
FORECAST.LINEAR          | 傳回線性趨勢值
FORMULATEXT              | 以文字格式傳回指定參照的公式
FREQUENCY                | 傳回垂直陣列的頻率分佈
F.TEST                   | 傳回 F 檢定的結果
FTEST                    | 傳回 F 檢定的結果
FV                       | 傳回投資的未來值
FVSCHEDULE               | 傳回一筆本金在經過一系列複利計算後的本利和
GAMMA                    | 傳回 Gamma 函式值
GAMMA.DIST               | 傳回 Gamma 分佈
GAMMADIST                | 傳回 Gamma 分佈
GAMMA.INV                | 傳回 Gamma 累加分佈的反函式值
GAMMAINV                 | 傳回 Gamma 累加分佈的反函式值
GAMMALN                  | 傳回伽瑪函式的自然對數 Γ(x)
GAMMALN.PRECISE          | 傳回伽瑪函式的自然對數 Γ(x)
GAUSS                    | 傳回較標準常態累加分佈小 0.5 的值
GCD                      | 傳回最大公因數
GEOMEAN                  | 傳回幾何平均數
GESTEP                   | 測試數字是否大於臨界值
GROWTH                   | 傳回指數趨勢值
HARMEAN                  | 傳回調和平均數
HEX2BIN                  | 將十六進位數字轉換為二進位
HEX2DEC                  | 將十六進位數字轉換為十進位
HEX2OCT                  | 將十六進位數字轉換為八進位
HLOOKUP                  | 在陣列的第一列尋找並傳回指示的儲存格的值
HOUR                     | 將序列值轉換為小時
HYPERLINK                | 建立捷徑或跳躍點，開啟儲存在網路伺服器、內部網路或網際網路上的文件
HYPGEOM.DIST             | 傳回超幾何分佈
HYPGEOMDIST              | 傳回超幾何分佈
IF                       | 指定要執行的邏輯測試
IFERROR                  | 如果公式計算結果錯誤，就傳回您所指定的值，否則傳回公式的結果
IFNA                     | 如果運算式解析為 #N/A，傳回您指定的值，否則傳回運算式的結果
IFS                      | 檢查是否符合一或多個條件，並傳回對應至第一個 TRUE 條件的值
IMABS                    | 傳回複數的絕對值 (模數)
IMAGINARY                | 傳回複數的虛係數
IMARGUMENT               | 傳回引數樞紐角度，以弧度表示的角度
IMCONJUGATE              | 傳回複數的共軛複數
IMCOS                    | 傳回複數的餘弦
IMCOSH                   | 傳回複數的雙曲餘弦
IMCOT                    | 傳回複數的餘切
IMCSC                    | 傳回複數的餘割
IMCSCH                   | 傳回複數的雙曲餘割
IMDIV                    | 傳回兩個複數的商數
IMEXP                    | 傳回複數的指數
IMLN                     | 傳回複數的自然對數
IMLOG10                  | 傳回複數以 10 為底數的對數
IMLOG2                   | 傳回複數以 2 為底數的對數
IMPOWER                  | 傳回遞增至整數冪的複數
IMPRODUCT                | 傳回複數的乘積
IMREAL                   | 傳回複數的實係數
IMSEC                    | 傳回複數的正割
IMSECH                   | 傳回複數的雙曲正割
IMSIN                    | 傳回複數的正弦
IMSINH                   | 傳回複數的雙曲正弦
IMSQRT                   | 傳回複數的平方根
IMSUB                    | 傳回兩個複數之間的差異
IMSUM                    | 傳回複數的總和
IMTAN                    | 傳回複數的正切
INDEX                    | 使用索引從參照或陣列中選擇值
INDIRECT                 | 傳回依文字值指出的參照
INT                      | 將數字四捨五入至最接近的整數
INTERCEPT                | 傳回線性迴歸線的截距
INTRATE                  | 傳回完整投資債券的利率
IPMT                     | 傳回在指定期間內的投資的利息支付
IRR                      | 傳回一系列現金流量的內部報酬率
ISBLANK                  | 如果值為空白，則傳回 TRUE
ISERR                    | 如果值為 #N/A 以外的任何錯誤值，則傳回 TRUE
ISERROR                  | 如果值為任何錯誤值，則傳回 TRUE
ISEVEN                   | 如果數字為偶數，則傳回 TRUE
ISFORMULA                | 如果有包含公式的儲存格參照，則傳回 TRUE
ISLOGICAL                | 如果值為邏輯值，則傳回 TRUE
ISNA                     | 如果值為 #N/A 錯誤值，則傳回 TRUE
ISNONTEXT                | 如果值不是文字值，則傳回 TRUE
ISNUMBER                 | 如果值為數值，則傳回 TRUE
ISODD                    | 如果數字為奇數，則傳回 TRUE
ISREF                    | 如果值為參照，則傳回 TRUE
ISTEXT                   | 如果值為文字值，則傳回 TRUE
ISO.CEILING              | 傳回數字，四捨五入至最接近的整數，或四捨五入至最接近的基數倍數
ISOWEEKNUM               | 傳回指定日期的年度 ISO 週數的數字
ISPMT                    | 計算投資的特定期間支付的利息
KURT                     | 傳回資料集的峰度值
LARGE                    | 傳回資料集中第 k 個最大的值
LCM                      | 傳回最小公倍數
LEFT                     | 傳回文字值最左邊的字元
LEFTB                    | 傳回文字值最左邊的字元
LEN                      | 傳回文字字串中的字元數
LENB                     | 傳回文字字串中的字元數
LN                       | 傳回數字的自然對數
LOG                      | 傳回數字的對數至指定的底數
LOG10                    | 傳回數字以 10 為底數的對數
LOGINV                   | 傳回對數累加分佈的反函式值
LOGNORM.DIST             | 傳回累加對數分佈
LOGNORMDIST              | 傳回累加對數分佈
LOGNORM.INV              | 傳回對數累加分佈的反函式值
LOOKUP                   | 在向量或陣列中查詢值
LOWER                    | 將文字轉換為小寫
MATCH                    | 在參照或陣列中查詢值
MAX                      | 傳回引數清單中的最大值
MAXA                     | 傳回引數清單中的最大值，包括數字、文字和邏輯值
MAXIFS                   | 傳回由指定一組條件或準則所指定的儲存格間的最大值
MDETERM                  | 傳回陣列的矩陣行列式
MDURATION                | 傳回假定面額為 100 元之債券的 Macauley 修正有效期間
MEDIAN                   | 傳回指定數字的中位數
MID                      | 從您指定的文字字串位置開始傳回特定字元數
MIDB                     | 從您指定的文字字串位置開始傳回特定字元數
MIN                      | 傳回引數清單中的最小值
MINIFS                   | 傳回由指定一組條件或準則所指定的儲存格間的最小值
MINA                     | 傳回引數清單中的最小值，包括數字、文字和邏輯值
MINUTE                   | 將序列值轉換為分鐘
MINVERSE                 | 傳回陣列的反矩陣
MIRR                     | 傳回內部報酬率，其中正負現金流是使用不同的費率
MMULT                    | 傳回兩個陣列的矩陣乘積
MOD                      | 傳回除數的餘數
MODE                     | 傳回資料集中最常見的值
MODE.MULT                | 傳回陣列或資料範圍中最常出現或重複之值的垂直陣列
MODE.SNGL                | 傳回資料集中最常見的值
MONTH                    | 將序列值轉換為月份
MROUND                   | 傳回數字，四捨五入至所要的倍數
MULTINOMIAL              | 傳回數字集的多項式
MUNIT                    | 傳回指定維度的單位矩陣
N                        | 傳回轉換為數字的值
NA                       | 傳回錯誤值 #N/A
NEGBINOM.DIST            | 傳回負二項式分配
NEGBINOMDIST             | 傳回負二項式分配
NETWORKDAYS              | 傳回兩個日期之間的全部工作日數
NETWORKDAYS.INTL         | 使用參數傳回兩個日期之間的全部工作日數，指出有哪些天以及有幾天是週末
NOMINAL                  | 傳回名目年利率
NORM.DIST                | 傳回常態累加分佈
NORMDIST                 | 傳回常態累加分佈
NORMINV                  | 傳回常態累加分佈的反函式值
NORM.INV                 | 傳回常態累加分佈的反函式值
NORM.S.DIST              | 傳回標準常態累加分佈
NORMSDIST                | 傳回標準常態累加分佈
NORM.S.INV               | 傳回標準常態累加分佈的反函式值
NORMSINV                 | 傳回標準常態累加分佈的反函式值
NOT                      | 將引數的邏輯值反轉
NOW                      | 傳回目前日期和時間的序列值
NPER                     | 傳回投資的期數
NPV                      | 在已知連續週期現金流量及貼現率的條件下，傳回某項投資的淨現值
OCT2BIN                  | 將八進位數字轉換為二進位
OCT2DEC                  | 將八進位數字轉換為十進位
OCT2HEX                  | 將八進位數字轉換為十六進位
ODD                      | 將數字四捨五入至最接近的奇數整數
ODDFPRICE                | 傳回具有奇數第一個週期的債券每 $100 美元面額的價格
ODDFYIELD                | 傳回具有奇數第一個週期的債券收益
ODDLPRICE                | 傳回具有奇數最後週期的債券每 $100 美元面額的價格
ODDLYIELD                | 傳回具有奇數最後週期的債券收益
OR                       | 如果任一引數為 TRUE，則傳回 TRUE
PDURATION                | 傳回投資達到指定值時所需的週期數
PEARSON                  | 傳回 Pearson 積差相關係數
PERCENTILE.EXC           | 傳回範圍中位於第 k 個百分比的數值，k 是在 0 到 1 的範圍內 (不含)
PERCENTILE.INC           | 傳回範圍中第 k 個百分位數的值
PERCENTILE               | 傳回範圍中第 k 個百分位數的值
PERCENTRANK.EXC          | 傳回某數值在一個資料集中的百分比 (介於 0 與 1 之間，不包含 0 與 1) 的等級
PERCENTRANK.INC          | 傳回值在資料集中的百分比排名
PERCENTRANK              | 傳回值在資料集中的百分比排名
PERMUT                   | 傳回指定數量物件的排列方式的數目
PERMUTATIONA             | 傳回從所有物件選取指定數量的物件時 (包括重複選取物件)，所有可能排列方式的數目
PHI                      | 傳回標準常態分佈的密度函式值
PI                       | 傳回 Pi 的值
PMT                      | 傳回年金的定期付款
POISSON.DIST             | 傳回波式分佈
POISSON                  | 傳回波式分佈
POWER                    | 傳回數字乘幕的結果
PPMT                     | 傳回在指定期間內的投資的本金支付
PRICE                    | 傳回應定期支付利息的債券每 $100 美元面額的價格
PRICEDISC                | 傳回貼現債券每 $100 美元面額的價格
PRICEMAT                 | 傳回應在到期時支付利息的債券每 $100 美元面額的價格
PROB                     | 傳回落在兩個限制之間的機率值
PRODUCT                  | 乘以其引數
PROPER                   | 將每個文字值單字的第一個字母轉換為大寫字母
PV                       | 傳回投資的現值
QUARTILE                 | 傳回資料點的四分位數
QUARTILE.EXC             | 傳回資料集的四分位數，以介於 0 與 1 之間 (不包含 0 與 1) 的百分位數值為基礎
QUARTILE.INC             | 傳回資料點的四分位數
QUOTIENT                 | 傳回除法的整數部分
RADIANS                  | 將角度轉換為弧度
RAND                     | 傳回介於 0 到 1 之間的亂數
RANDBETWEEN              | 傳回您指定的數字之間的隨機數字
RANK.EQ                  | 傳回數字在數列中的排名
RANK                     | 傳回數字在數列中的排名
RATE                     | 傳回年金每個時期的利率
RECEIVED                 | 傳回完整投資債券在到期時收到的金額
REPLACE                  | 取代文字內的字元
REPLACEB                 | 取代文字內的字元
REPT                     | 以指定的次數重複文字
RIGHT                    | 傳回文字值最右邊的字元
RIGHTB                   | 傳回文字值最右邊的字元
ROMAN                    | 將阿拉伯數字轉換為羅馬數字文字
ROUND                    | 將數字四捨五入至指定的位數
ROUNDDOWN                | 將數字無條件捨去，趨近於零
ROUNDUP                  | 將數字四捨五入，背離於零
ROW                      | 傳回參照的列號
ROWS                     | 傳回參照範圍的列數
RRI                      | 傳回投資成長的對等利率
RSQ                      | 傳回 Pearson 積差相關係數的平方
SEARCH                   | 在文字值間尋找文字值 (不區分大小寫)
SEARCHB                  | 在文字值間尋找文字值 (不區分大小寫)
SEC                      | 傳回角度的正割
SECH                     | 傳回角度的雙曲正割值
SECOND                   | 將序列值轉換為秒鐘
SERIESSUM                | 傳回依據公式的冪級數總和
SHEET                    | 傳回參照工作表的工作表號碼
SHEETS                   | 傳回參照中的工作表數目
SIGN                     | 傳回代表數字正負號的代碼
SIN                      | 傳回給定角度的正弦值
SINH                     | 傳回數值的雙曲正弦值
SKEW                     | 傳回分佈的偏態
SKEW.P                   | 傳回以某個母體為基礎的分佈偏態，所謂偏態是指一個分佈的不對稱情形
SLN                      | 傳回某項固定資產按直線折舊法所計算的每期折舊金額
SLOPE                    | 傳回線性迴歸線的斜率
SMALL                    | 傳回資料集中第 k 最小的值
SORT                     | 排序範圍或陣列的內容
SQRTPI                   | 傳回 (number * pi) 的平方根
STANDARDIZE              | 傳回標準化的值
STDEV                    | 根據樣本估計標準差
STDEV.P                  | 根據整體母體計算標準差
STDEV.S                  | 根據樣本估計標準差
STDEVA                   | 根據樣本，包括數字、文字和邏輯值來估計標準差
STDEVP                   | 根據整體母體計算標準差
STDEVPA                  | 根據整體母體，包括數字、文字和邏輯值來計算標準差
STEYX                    | 傳回迴歸分析中為每個 x 所預測之 y 值的標準誤差
SUBSTITUTE               | 用新文字取代文字字串中的舊文字
SUBTOTAL                 | 傳回清單或資料庫中的小計
SUM                      | 加上其引數
SUMIF                    | 將滿足給定條件的儲存格的值相加
SUMIFS                   | 將符合多個準則的範圍中的儲存格相加
SUMPRODUCT               | 傳回對應陣列元素之乘積的總和
SUMSQ                    | 傳回引數的平方和
SUMX2MY2                 | 傳回兩個陣列中對應值之平方差的總和
SUMX2PY2                 | 傳回兩個陣列中對應值之平方和的總和
SUMXMY2                  | 傳回兩個陣列中對應值之差的平方和
SWITCH                   | 根據值清單評估運算式，並傳回對應到第一個相符值的結果。如果沒有相符的值，可能傳回選用的預設值
SYD                      | 按年數合計法計算，傳回某固定資產在某一指定期間的折舊金額
T                        | 將其引數轉換為文字
TAN                      | 傳回數字的正切
TANH                     | 傳回數值的雙曲正切值
TBILLEQ                  | 傳回美國國家債券的債券約當收益率
TBILLPRICE               | 傳回美國國家債券每 $100 美元面額的價格
TBILLYIELD               | 傳回美國國家債券的收益
T.DIST                   | 傳回 Student T 分配的百分比點 (機率)
T.DIST.2T                | 傳回 Student T 分配的百分比點 (機率)
T.DIST.RT                | 傳回 Student T 分配
TDIST                    | 傳回 Student T 分配
TEXT                     | 格式化數字並將其轉換為文字
TEXTAFTER                | 傳回在特定字元或字串之後出現的文字
TEXTBEFORE               | 傳回特定字元或字串之前的文字
TEXTJOIN                 | 合併多個範圍和/或字串中的文字
TIME                     | 傳回特定時間的序列值
TIMEVALUE                | 將文字形式的時間轉換為序列值
T.INV                    | 以機率函式和自由度為形式，傳回 Student T 分配的 t 值
T.INV.2T                 | 傳回 Student T 分配的反函式值
TINV                     | 傳回 Student T 分配的反函式值
TODAY                    | 傳回今天日期的序列值
TRANSPOSE                | 傳回陣列的轉置
TREND                    | 傳回線性趨勢值
TRIM                     | 移除文字中的空格
TRIMMEAN                 | 傳回資料集內部的平均數
TRUE                     | 傳回邏輯值 TRUE
TRUNC                    | 將數值的小數部分截去
T.TEST                   | 傳回與 Student T 檢定相關的機率
TTEST                    | 傳回與 Student T 檢定相關的機率
TYPE                     | 傳回數字，指出值的資料類型
UNICHAR                  | 傳回指定數值所參考的 Unicode 字元
UNICODE                  | 傳回對應至文字的第一個字元的數字 (字碼指標)
UPPER                    | 將文字轉換為大寫
VALUE                    | 將文字引數轉換為數字
VALUETOTEXT              | 傳回來自任何指定值的文字
VAR                      | 根據樣本來估計變異數
VAR.P                    | 根據整體母體計算變異數
VAR.S                    | 根據樣本來估計變異數
VARA                     | 根據樣本，包括數字、文字和邏輯值來估計變異數
VARP                     | 根據整體母體計算變異數
VARPA                    | 根據整體母體，包括數字、文字和邏輯值來計算變異數
VDB                      | 傳回資產在指定或部分期間內使用餘額遞減法所計算的折舊
VLOOKUP                  | 在陣列的第一欄尋找某一列，並傳回該列之儲存格中的數值
WEEKDAY                  | 將序列值轉換為一週中的某日天
WEEKNUM                  | 將序列值轉換為數字，表示週數上落在年份的位置
WEIBULL                  | 根據整體母體，包括數字、文字和邏輯值來計算變異數
WEIBULL.DIST             | 傳回 Weibull 分佈
WORKDAY                  | 傳回指定的工作日數目之前或之後，日期的數列數字
WORKDAY.INTL             | 使用參數傳回指定的工作日數目之前或之後的日期的數列數字，指出有哪些天以及有幾天是週末
XIRR                     | 傳回現金流量排程 (不一定為週期性) 的內部報酬率
XLOOKUP                  | 搜尋範圍或陣列，並傳回找到的第一個對應項目。如果相符項目不存在，則 XLOOKUP 可以傳回最接近的 (大約) 相符項目
XNPV                     | 傳回現金流量時程的淨現值，該現金流量不一定是定期的流量
XOR                      | 傳回所有引數的邏輯獨佔 OR
YEAR                     | 將序列值轉換為年份
YEARFRAC                 | 傳回代表在 start_date 和 end_date 之間所有日期數字的年份分數
YIELD                    | 傳回定期支付利息的債券收益
YIELDDISC                | 傳回貼現債券的年收益；例如，美國國家債券
YIELDMAT                 | 傳回債券的年收益，該債券在到期時支付利息
Z.TEST                   | 傳回 Z 檢定的單尾機率值
ZTEST                    | 傳回 Z 檢定的單尾機率值
