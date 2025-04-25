# 양식 컨트롤

FormControl 은 양식 컨트롤 정보를 직접 매핑합니다.

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

## 양식 컨트롤 추가 {#AddFormControl}

```go
func (f *File) AddFormControl(sheet string, opts FormControl) error
```

AddFormControl 은 지정된 워크시트 이름 및 양식 제어 옵션에 따라 워크시트에 양식 제어 단추를 추가하는 메서드를 제공합니다. 지원되는 양식 제어 유형: 단추, 확인란, 그룹 상자, 레이블, 옵션 단추, 스크롤 막대 및 스피너. 양식 컨트롤에 대해 매크로를 설정한 경우 통합 문서 확장은 `.xlsm` 또는 `.xltm` 이어야 합니다. 스크롤 값은 0 에서 30000 사이여야 합니다. 확인란 양식 컨트롤에 대해 셀 링크가 설정된 경우 Excelize는 확인란을 선택할 때 연결된 셀에 값을 할당하지 않습니다. 체크박스 상태를 반영하려면 [`SetCellValue`](cell.md#SetCellValue) 기능을 사용하여 연결된 셀의 값을 수동으로 `true` 로 설정하십시오.

예제 1, 매크로, 서식 있는 텍스트, 사용자 지정 단추 크기, 인쇄 속성이 있는 단추 양식 컨트롤을 `Sheet1!A2` 로 설정하고 버튼이 셀과 함께 움직이거나 크기가 조정되지 않도록 합니다:

<p align="center"><img width="180" src="./images/form_ctrl_button.gif" alt="Excelize 로 단추 양식 컨트롤 추가"></p>

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

예 2, `Sheet1!A1` 및 `Sheet1!A2` 에 체크 상태 및 텍스트가 있는 옵션 버튼 양식 컨트롤을 추가합니다:

<p align="center"><img width="127" src="./images/form_ctrl_option_button.gif" alt="Excelize 로 옵션 단추 양식 컨트롤 추가"></p>

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

예 3, `Sheet1!A1` 의 값을 늘리거나 줄이기 위해 `Sheet1!B1` 에 스핀 버튼 양식 컨트롤을 추가합니다:

<p align="center"><img width="126" src="./images/form_ctrl_spin_button.gif" alt="Excelize 로 스핀 버튼 양식 컨트롤 추가"></p>

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

예제 4, `Sheet1!A2` 에 가로 스크롤 막대 양식 컨트롤을 추가하여 스크롤 화살표를 클릭하거나 스크롤 상자를 드래그하여 `Sheet1!A1` 값을 변경합니다:

<p align="center"><img width="180" src="./images/form_ctrl_scroll_bar.gif" alt="Excelize 를 사용하여 가로 스크롤 막대 양식 컨트롤 추가"></p>

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

## 양식 컨트롤 가져오기 {#GetFormControls}

```go
func (f *File) GetFormControls(sheet string) ([]FormControl, error)
```

GetFormControls 는 지정된 워크시트 이름으로 워크시트의 모든 양식 컨트롤을 검색합니다. 이 함수는 현재 양식 컨트롤의 너비와 높이 가져오기를 지원하지 않습니다.

## 양식 컨트롤 삭제 {#DeleteFormControl}

```go
func (f *File) DeleteFormControl(sheet, cell string) error
```

DeleteFormControl 은 지정된 워크시트 이름과 셀 참조에 따라 워크시트에서 양식 컨트롤을 삭제하는 메서드를 제공합니다. 예를 들어 `Sheet1!$A$1` 에서 양식 컨트롤을 삭제합니다.

```go
err := f.DeleteFormControl("Sheet1", "A1")
```
