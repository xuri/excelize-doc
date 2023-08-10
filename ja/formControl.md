# フォーム コントロール

フォーム コントロールは、フォーム コントロール情報を直接マップします。

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

## フォーム コントロールの追加 {#AddFormControl}

```go
func (f *File) AddFormControl(sheet string, opts FormControl) error
```

AddFormControl は、指定されたワークシート名とフォーム コントロール オプションによってワークシートにフォーム コントロール ボタンを追加するメソッドを提供します。サポートされているフォームコントロールの種類: ボタン、チェックボックス、グループボックス、ラベル、オプションボタン、スクロールバー、スピナー。フォーム コントロールのマクロを設定する場合、ブックの拡張機能は `.xlsm` または `.xltm` である必要があります。スクロール値は 0 から 30000 の間でなければなりません。

例1、マクロ、リッチテキスト、カスタムボタンサイズ、印刷プロパティを持つボタンフォームコントロールを `Sheet1!A2`、ボタンを移動したり、セルに合わせてサイズを変更したりしないようにします:

<p align="center"><img width="180" src="./images/form_ctrl_button.gif" alt="Excelize でボタンフォームコントロールを追加する"></p>

```go
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

例2、`Sheet1!A1` と `Sheet1!A2` にチェックされたステータスとテキストを持つオプションボタンフォームコントロールを追加します:

<p align="center"><img width="127" src="./images/form_ctrl_option_button.gif" alt="Excelize でオプション ボタン フォーム コントロールを追加する"></p>

```go
if err := f.AddFormControl("Sheet1", excelize.FormControl{
    Cell:    "A1",
    Type:    excelize.FormControlOptionButton,
    Text:    "Option Button 1",
    Checked: true,
}); err != nil {
    fmt.Println(err)
}
if err := f.AddFormControl("Sheet1", excelize.FormControl{
    Cell:    "A2",
    Type:    excelize.FormControlOptionButton,
    Text:    "Option Button 2",
}); err != nil {
    fmt.Println(err)
}
```

例3、`Sheet1!B1` にスピンボタンフォームコントロールを追加して、`Sheet1!A1` の値を増減します:

<p align="center"><img width="126" src="./images/form_ctrl_spin_button.gif" alt="Excelize でスピンボタンフォームコントロールを追加する"></p>

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

例4、`Sheet1!A2` に水平スクロール バー フォーム コントロールを追加して、スクロール矢印をクリックするか、スクロール ボックスをドラッグして `Sheet1!A2` の値を変更します:

<p align="center"><img width="180" src="./images/form_ctrl_scroll_bar.gif" alt="Excelize を使用して水平スクロールバーフォームコントロールを追加する"></p>

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

## フォーム コントロールを取得する {#GetFormControls}

```go
func (f *File) GetFormControls(sheet string) ([]FormControl, error)
```

GetFormControls は、指定されたワークシート名によってワークシート内のすべてのフォーム コントロールを取得します。現在、この関数はフォーム コントロールの幅と高さの取得をサポートしていないことに注意してください。

## フォーム コントロールの削除 {#DeleteFormControl}

```go
func (f *File) DeleteFormControl(sheet, cell string) error
```

DeleteFormControl は、指定されたワークシート名とセル参照によってワークシート内のフォーム コントロールを削除するメソッドを提供します。たとえば、`Sheet1!$A$1` のフォーム コントロールを削除します:

```go
err := f.DeleteFormControl("Sheet1", "A1")
```
