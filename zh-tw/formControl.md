# 表單控制項

FormControl 定義了表單控制項的屬性。

```go
type FormControl struct {
    Cell         string
    Macro        string
    Width        uint
    Height       uint
    Checked      bool
    CurrentVal   uint
    MinVal       uint
    MaxVal       uint
    IncChange    uint
    PageChange   uint
    Horizontally bool
    CellLink     string
    Text         string
    Paragraph    []RichTextRun
    Type         FormControlType
    Format       GraphicOptions
}
```

## 添加表單控制項 {#AddFormControl}

```go
func (f *File) AddFormControl(sheet string, opts FormControl) error
```

AddFormControl 透過給定的工作表名稱和表單控制項選項在工作表中添加表單控制項。支援的表單控制項類型為：按鈕、核取方塊、群組方塊、標籤、選項按鈕、捲軸和微調按鈕。若需要為表單控制項指定巨集，保存的活頁簿擴展名應為 `.xlsm` 或者 `.xltm`。滾動值應介於 0 到 30000 之間。

例1，在 `Sheet1!A2` 存儲格添加帶有指定巨集、富文本、自訂尺寸和摘要資訊的按鈕表單控制項：

<p align="center"><img width="180" src="./images/form_ctrl_button.gif" alt="使用 Excelize 在工作表中添加按鈕表單控制項"></p>

```go
enable := true
err := f.AddFormControl("Sheet1", excelize.FormControl{
    Cell:   "A2",
    Type:   excelize.FormControlButton,
    Macro:  "Button1_Click",
    Width:  140,
    Height: 60,
    Text:   "Button 1\r\n",
    Paragraph: []excelize.RichTextRun{
        {
            Font: &excelize.Font{
                Bold:      true,
                Italic:    true,
                Underline: "single",
                Family:    "Times New Roman",
                Size:      14,
                Color:     "777777",
            },
            Text: "C1=A1+B1",
        },
    },
    Format: excelize.GraphicOptions{
        PrintObject: &enable,
        Positioning: "absolute",
    },
})
```

例2，在 `Sheet1!A1` 和 `Sheet1!A2` 存儲格添加帶有選中狀態的選項按鈕表單控制項：

<p align="center"><img width="127" src="./images/form_ctrl_option_button.gif" alt="使用 Excelize 在工作表中添加選項按鈕表單控制項"></p>

```go
if err := f.AddFormControl("Sheet1", excelize.FormControl{
    Cell:    "A1",
    Type:    excelize.FormControlOptionButton,
    Text:    "Option Button 1",
    Checked: true,
    Height:  20,
}); err != nil {
    fmt.Println(err)
}
if err := f.AddFormControl("Sheet1", excelize.FormControl{
    Cell:    "A2",
    Type:    excelize.FormControlOptionButton,
    Text:    "Option Button 2",
    Height:  20,
}); err != nil {
    fmt.Println(err)
}
```

例3，在 `Sheet1!B1` 存儲格添加帶有控制選項的微調按鈕來增大或減小 `Sheet1!A1` 存儲格的值：

<p align="center"><img width="126" src="./images/form_ctrl_spin_button.gif" alt="使用 Excelize 在工作表中添加微調按鈕表單控制項"></p>

```go
err := f.AddFormControl("Sheet1", excelize.FormControl{
    Cell:       "B1",
    Type:       excelize.FormControlSpinButton,
    Width:      15,
    Height:     40,
    CurrentVal: 7,
    MinVal:     5,
    MaxVal:     10,
    IncChange:  1,
    CellLink:   "A1",
})
```

例4，在 `Sheet1!A2` 存儲格添加水平捲軸，透過拖動滾動框輸入或修改 `Sheet1!A1` 存儲格的值：

<p align="center"><img width="180" src="./images/form_ctrl_scroll_bar.gif" alt="使用 Excelize 在工作表中添加水平捲軸表單控制項"></p>

```go
err := f.AddFormControl("Sheet1", excelize.FormControl{
    Cell:         "A2",
    Type:         excelize.FormControlScrollBar,
    Width:        140,
    Height:       20,
    CurrentVal:   50,
    MinVal:       10,
    MaxVal:       100,
    IncChange:    1,
    PageChange:   1,
    CellLink:     "A1",
    Horizontally: true,
})
```

## 獲取表單控制項 {#GetFormControls}

```go
func (f *File) GetFormControls(sheet string) ([]FormControl, error)
```

根據給定的工作表名稱獲取工作表中的全部表單控制項。注意，該函數目前尚未支援獲取表單控制項的寬高。

## 刪除表單控制項 {#DeleteFormControl}

```go
func (f *File) DeleteFormControl(sheet, cell string) error
```

DeleteFormControl 透過給定的工作表名稱和存儲格坐標刪除指定的表單控制項。例如，刪除位於 `Sheet1!$A$1` 存儲格的表單控制項:

```go
err := f.DeleteFormControl("Sheet1", "A1")
```
