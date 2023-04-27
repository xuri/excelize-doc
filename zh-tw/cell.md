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

`FormulaOpts` 用於在 [`SetCellFormula`](cell.md#SetCellFormula) 函數中指定設定特殊公式類型。

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

請注意，此函數默認為 `time.Time` 類型的存儲格的值設定 `m/d/yy h:mm` 數字格式，您可透過 [`SetCellStyle`](cell.md#SetCellStyle) 更改該設定。若您需設定無法通過 Go 語言 `time.Time` 類型表示的 Excel 特殊日期，例如 1900 年 1 月 0 日或 1900 年 2 月 29 日，請先設定存儲格的值為 0 或 60，再為其設定具有日期數字格式的樣式。

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

根據給定的工作表名、儲存格坐標、浮點數、浮點數尾數部分精度和浮點數類型設定浮點型單元格的值。

## 設定字符型值 {#SetCellStr}

```go
func (f *File) SetCellStr(sheet, cell, value string) error
```

根據給定的工作表名和儲存格坐標設定字符型儲存格的值，字符將會進行特殊字符過濾，並且字符串的累計長度應不超過 `32767`，多餘的字符將會被忽略。

## 設定儲存格樣式 {#SetCellStyle}

```go
func (f *File) SetCellStyle(sheet, hCell, vCell string, styleID int) error
```

根據給定的工作表名、儲存格坐標區域和樣式索引設定儲存格的值。此功能是併發安全的。樣式索引可以通過 [`NewStyle`](style.md#NewStyle) 函數獲取。注意，在同一個坐標區域內的 `diagonalDown` 和 `diagonalUp` 需要保持色彩一致。SetCellStyle 將覆蓋存儲格的已有樣式，而不會將樣式與已有樣式疊加或合併。

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

儲存格 `D7` 的四個外框被設定了不同的樣式和色彩，這與調用 [`NewStyle`](style.md#NewStyle) 函數時的參數有關，需要設定不同的樣式可參考該章節的文檔。

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

儲存格 `D7` 被設定了漸變效果的色彩填滿，漸變填滿效果與調用 [`NewStyle`](style.md#NewStyle) 函數時的參數有關，需要設定不同的樣式可參考該章節的文檔。

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

儲存格 `D7` 被設定了時間格式。注意，當應用了時間格式的儲存格寬度過窄無法完整展示時會顯示為 `####`，可以拖拽調整欄寬或者通過調用 `SetColWidth` 函數設定欄寬到合適的大小使其正常顯示。

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

根據給定的工作表、儲存格坐標、鏈接資源和資源類別設定儲存格的超鏈接。資源類別分為外部鏈接地址 `External` 和活頁簿內部位置鏈接 `Location` 兩種。每個工作表中的包含最大超鏈接限制為 `65530` 個。該方法僅設定存儲格的超鏈接而不影響存儲格的值，若需設定存儲格的值，請通過 [`SetCellStyle`](cell.md#SetCellStyle) 或 [`SetSheetRow`](sheet.md#SetSheetRow) 等函數另行設定。

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
// 為儲存格設定字型和下划線樣式
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

根據給定的工作表名和儲存格坐標獲取儲存格樣式索引，獲取到的索引可以在設定儲存格樣式時，作為調用 `SetCellStyle` 函數的參數使用。

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
    Runs: []excelize.RichTextRun{
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

根據給定的工作表名和儲存格坐標設定該儲存格上的公式。公式的結果會在工作表被 Office Excel 應用程式打開時計算，或通過 [CalcCellValue](cell.md#CalcCellValue) 函數計算存儲格的值。若 Excel 應用程式打開活頁簿後未對設定的存儲格公式進行計算，請在設定公式後調用 [UpdateLinkedValue](utils.md#UpdateLinkedValue) 清除存儲格緩存。

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
    if err := f.AddTable("Sheet1", "A1:C2", &excelize.TableOptions{
        Name: "Table1", StyleName: "TableStyleMedium2",
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

根據給定的工作表名和存儲格坐標計算包含公式存儲格的值。該方法目前正在開發中，尚未支持迭代計算、隱式交集、顯式交集、數組函數、數組函數、表格函數和其他部分函數。

支持的函數列表如下：

```text
ABS
ACCRINT
ACCRINTM
ACOS
ACOSH
ACOT
ACOTH
ADDRESS
AGGREGATE
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
DAVERAGE
DAY
DAYS
DAYS360
DB
DCOUNT
DCOUNTA
DDB
DEC2BIN
DEC2HEX
DEC2OCT
DECIMAL
DEGREES
DELTA
DEVSQ
DGET
DISC
DMAX
DMIN
DOLLARDE
DOLLARFR
DPRODUCT
DSTDEV
DSTDEVP
DSUM
DURATION
DVAR
DVARP
EFFECT
EDATE
ENCODEURL
EOMONTH
ERF
ERF.PRECISE
ERFC
ERFC.PRECISE
ERROR.TYPE
EUROCONVERT
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
HYPERLINK
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
NETWORKDAYS
NETWORKDAYS.INTL
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
STEYX
SUBSTITUTE
SUBTOTAL
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
WEEKNUM
WEIBULL
WEIBULL.DIST
WORKDAY
WORKDAY.INTL
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
