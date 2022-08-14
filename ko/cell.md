# 세포

RichTextRun 은 서식있는 텍스트 실행의 설정을 직접 맵핑합니다.

```go
type RichTextRun struct {
    Font *Font
    Text string
}
```

HyperlinkOpts 는 [`SetCellHyperlink`](cell.md#SetCellHyperlink) 에 전달되어 선택적 하이퍼 링크 속성 (예: 표시 할 텍스트 및 화면 팁 텍스트) 을 설정할 수 있습니다.

```go
type HyperlinkOpts struct {
    Display *string
    Tooltip *string
}
```

FormulaOpts 는 다른 수식 유형을 사용하기 위해 [`SetCellFormula`](cell.md#SetCellFormula) 로 전달할 수 있습니다.

```go
type FormulaOpts struct {
    Type *string // 수식 유형
    Ref  *string // 공유 수식 참조
}
```

## 셀 값 설정 {#SetCellValue}

```go
func (f *File) SetCellValue(sheet, axis string, value interface{}) error
```

SetCellValue 셀값을 설정하는 함수를 제공합니다. 지정된 좌표는 테이블의 첫 번째 행에 없어야합니다. 다음은 지원되는 데이터 형식을 보여 주며:

|지원되는 데이터 유형|
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

기본 날짜 형식은 `time.Time` 유형 값의 `m/d/yy h:mm` 입니다. [`SetCellStyle`](cell.md#SetCellStyle) 방식으로 숫자 형식을 설정할 수 있습니다. 1900 년 1 월 0 일 또는 1900 년 2 월 29 일과 같이 Excel 에서 특수 날짜를 설정해야 하는 경우 이러한 시간은 Go 언어의 `time.Time` 데이터 형식으로 표현할 수 없습니다. 셀 값을 숫자 0 또는 60 으로 설정한 다음 셀에 대한 날짜-시간 숫자 형식 스타일을 만들고 바인딩하십시오.

## 부울 값 설정 {#SetCellBool}

```go
func (f *File) SetCellBool(sheet, axis string, value bool) error
```

SetCellBool 은 주어진 워크 시트 이름, 셀 좌표 및 셀 값에 의해 셀의 bool 형식 값을 설정하는 기능을 제공합니다.

## RAW 값 설정 {#SetCellDefault}

```go
func (f *File) SetCellDefault(sheet, axis, value string) error
```

SetCellDefault 는 셀을 이스케이프하지 않고 셀의 문자열 형식 값을 기본 형식으로 설정하는 기능을 제공합니다.

## 정수 값 설정 {#SetCellInt}

```go
func (f *File) SetCellInt(sheet, axis string, value int) error
```

SetCellInt 는 지정된 워크 시트 이름, 셀 좌표 및 셀 값으로 셀의 int 형식 값을 설정하는 기능을 제공합니다.

## 문자열 값 설정 {#SetCellStr}

```go
func (f *File) SetCellStr(sheet, axis, value string) error
```

SetCellStr 셀의 문자열 형식 값을 설정하는 함수를 제공합니다. 셀에 `32767` 문자를 포함할 수 있는 총 문자 수입니다.

## 셀 스타일 설정 {#SetCellStyle}

```go
func (f *File) SetCellStyle(sheet, hCell, vCell string, styleID int) error
```

SetCellStyle 지정된 워크 시트 이름, 좌표 영역 및 스타일 ID 에 의해 셀에 대 한 스타일 특성을 추가 하는 기능을 제공 합니다. 스타일 인덱스는 [`NewStyle`](style.md#NewStyle) 함수로 가져올 수 있습니다. `diagonalDown` 및 `diagonalUp` 유형 테두리는 동일한 좌표 영역에서 동일한 색상을 사용해야 합니다. SetCellStyle 은 셀의 기존 스타일을 덮어쓰며 기존 스타일에 스타일을 추가하거나 병합하지 않습니다.

- 예제 1 에서 `Sheet1` 에서 셀 `D7` 의 테두리를 만듭니다:

```go
style, err := f.NewStyle(&excelize.Style{
    Border: []excelize.Border{
        {Type: "left", Color: "0000FF", Style: 3},
        {Type: "top", Color: "00FF00", Style: 4},
        {Type: "bottom", Color: "FFFF00", Style: 5},
        {Type: "right", Color: "FF0000", Style: 6},
        {Type: "diagonalDown", Color: "A020F0", Style: 7},
        {Type: "diagonalUp", Color: "A020F0", Style: 8},
    },
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_01.png" alt="셀에 대한 테두리 스타일 설정"></p>

셀 `D7` 의 네 개의 테두리는 서로 다른 스타일과 색상으로 설정됩니다. 이는 [`NewStyle`](style.md#NewStyle) 함수를 호출할 때 매개 변수와 관련이 있습니다. 해당 장의 설명서를 참조하려면 다른 스타일을 설정해야 합니다.

- 예제 2, `Sheet1` 라는 워크 시트 `D7` 셀에 대한 그라데이션 스타일을 설정:

```go
style, err := f.NewStyle(&excelize.Style{
    Fill: excelize.Fill{Type: "gradient", Color: []string{"#FFFFFF", "#E0EBF5"}, Shading: 1},
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_02.png" alt="셀에 대한 그라데이션 스타일 설정"></p>

셀 `D7` 은 그라데이션 효과의 색상 채우기로 설정됩니다. 그라데이션 채우기 효과는 [`NewStyle`](style.md#NewStyle) 함수가 호출될 때 매개변수와 관련이 있습니다. 이 장의 설명서를 참조하려면 다른 스타일을 설정해야 합니다.

- 예제 3, `Sheet1` 이라는 이름의 `D7` 셀에 대한 솔리드 채우기를 설정합니다:

```go
style, err := f.NewStyle(&excelize.Style{
    Fill: excelize.Fill{Type: "pattern", Color: []string{"#E0EBF5"}, Pattern: 1},
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_03.png" alt="셀에 대한 솔리드 채우기 설정"></p>

셀 `D7` 은 솔리드 채우기로 설정됩니다.

- 예제 4, `Sheet1` 라는 이름의 `D7` 셀에 대한 문자 간격 및 회전 각도를 설정합니다:

```go
f.SetCellValue("Sheet1", "D7", "Style")
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

<p align="center"><img width="612" src="./images/SetCellStyle_04.png" alt="캐릭터 간격 및 회전 각도 설정"></p>

- 예 5, Excel 의 날짜와 시간은 예를 들어 `2017/7/4 12:00:00 PM` 이라는 숫자로 `42920.5` 로 나타낼 수 있습니다. 워크시트 `D7` 셀의 시간 형식을 `Sheet1` 으로 설정합니다.

```go
f.SetCellValue("Sheet1", "D7", 42920.5)
f.SetColWidth("Sheet1", "D", "D", 13)
style, err := f.NewStyle(&excelize.Style{NumFmt: 22})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_05.png" alt="셀의 시간 형식 설정"></p>

셀 `D7` 은 시간 형식으로 설정됩니다. 시간 형식이 적용된 셀 너비가 너무 좁아서 완전히 표시되지 않으면 `####` 로 표시되며, `SetColWidth` 함수를 호출하여 열을 적절한 크기로 설정하여 일반 디스플레이로 만들 수 있습니다.

- 예제 6, `Sheet1` 이라는 워크시트 `D7` 셀의 글꼴, 글꼴 크기, 색상 및 기울이기 스타일을 설정합니다:

```go
f.SetCellValue("Sheet1", "D7", "Excel")
style, err := f.NewStyle(&excelize.Style{
    Font: &excelize.Font{
        Bold:   true,
        Italic: true,
        Family: "Times New Roman",
        Size:   36,
        Color:  "#777777",
    },
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_06.png" alt="셀에 글꼴, 글꼴 크기, 색상 및 기울이기 스타일 설정"></p>

- 예 7, `Sheet1` 라는 워크 시트 `D7` 셀을 잠그고 숨김:

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

셀을 잠그거나 수식을 숨기려면 워크시트를 보호하십시오. "검토" 탭에서 "워크시트 보호"를 클릭합니다.

## 하이퍼 링크 설정 {#SetCellHyperLink}

```go
func (f *File) SetCellHyperLink(sheet, axis, link, linkType string, opts ...HyperlinkOpts) error
```

SetCellHyperLink 는 주어진 워크 시트 이름과 링크 URL 주소로 셀 하이퍼링크를 설정하는 기능을 제공합니다. LinkType 은 이 통합 문서의 셀 중 하나로 이동하기 위한 웹 사이트용 하이퍼링크 `External` 또는 `Location` 의 두 가지 유형을 정의합니다. 워크시트의 최대 제한 하이퍼링크는 `65530` 입니다. 이 함수는 셀의 하이퍼링크를 설정하는 데만 사용되며 셀의 값에는 영향을 미치지 않습니다. 셀의 값을 설정해야 하는 경우 [`SetCellStyle`](cell.md#SetCellStyle) 또는 [`SetSheetRow`](sheet.md#SetSheetRow) 와 같은 다른 기능을 사용하십시오. 다음은 외부 링크의 예입니다.

- 예제 1, `Sheet1` 이라는 워크시트의 `A3` 셀에 외부 링크를 추가합니다:

```go
display, tooltip := "https://github.com/xuri/excelize", "Excelize on GitHub"
if err := f.SetCellHyperLink("Sheet1", "A3",
    "https://github.com/xuri/excelize", "External", excelize.HyperlinkOpts{
        Display: &display,
        Tooltip: &tooltip,
    }); err != nil {
    fmt.Println(err)
}
// Set the font and underline style for the cell
style, err := f.NewStyle(&excelize.Style{
    Font: &excelize.Font{Color: "#1265BE", Underline: "single"},
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "A3", "A3", style)
```

- 예제 2, `Sheet1` 이라는 이름의 `A3` 셀에 내부 위치 링크를 추가합니다:

```go
err := f.SetCellHyperLink("Sheet1", "A3", "Sheet1!A40", "Location")
```

## 셀에 서식있는 텍스트 설정 {#SetCellRichText}

```go
func (f *File) SetCellRichText(sheet, cell string, runs []RichTextRun) error
```

SetCellRichText 는 주어진 워크 시트에 의해 리치 텍스트가있는 셀을 설정하는 기능을 제공합니다.

예를 들어, 이름이 `Sheet1` 인 워크 시트의 `A1` 셀에 서식있는 텍스트를 설정하십시오:

<p align="center"><img width="612" src="./images/rich_text.png" alt="셀에 서식있는 텍스트 설정"></p>

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
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
                Color:  "2354e8",
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
                Color:  "e83723",
                Italic: true,
                Family: "Times New Roman",
            },
        },
        {
            Text: "text with color and font-family,",
            Font: &excelize.Font{
                Bold:   true,
                Color:  "2354e8",
                Family: "Times New Roman",
            },
        },
        {
            Text: "\r\nlarge text with ",
            Font: &excelize.Font{
                Size:  14,
                Color: "ad23e8",
            },
        },
        {
            Text: "strike",
            Font: &excelize.Font{
                Color:  "e89923",
                Strike: true,
            },
        },
        {
            Text: " superscript",
            Font: &excelize.Font{
                Color:     "dbc21f",
                VertAlign: "superscript",
            },
        },
        {
            Text: " and ",
            Font: &excelize.Font{
                Size:      14,
                Color:     "ad23e8",
                VertAlign: "baseline",
            },
        },
        {
            Text: "underline",
            Font: &excelize.Font{
                Color:     "23e833",
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

## 서식있는 텍스트 형식 가져 오기 {#GetCellRichText}

```go
func (f *File) GetCellRichText(sheet, cell string) ([]RichTextRun, error)
```

지정된 워크 시트 및 셀 좌표에 따라 지정된 셀의 서식있는 텍스트 형식을 가져옵니다.

## 셀 값 가져 오기 {#GetCellValue}

```go
func (f *File) GetCellValue(sheet, axis string, opts ...Options) (string, error)
```

셀의 값은 지정된 워크시트 및 셀 좌표에 따라 검색되고 반환 값은 `string` 유형으로 변환됩니다. 셀 형식을 셀 값에 적용할 수 있는 경우 적용된 값이 반환되고 그렇지 않으면 원래 값이 반환됩니다. 병합 범위 내의 모든 셀의 값은 동일합니다.

## 셀 유형 가져오기 {#GetCellType}

```go
func (f *File) GetCellType(sheet, axis string) (CellType, error)
```

GetCellType 은 스프레드시트 파일에서 주어진 워크시트 이름과 축으로 셀의 데이터 유형을 가져오는 기능을 제공합니다.

## 열로 모든 셀 값 가져 오기 {#GetCols}

```go
func (f *File) GetCols(sheet string, opts ...Options) ([][]string, error)
```

GetCols 는 지정된 워크시트 이름 을 기반으로 워크시트의 모든 셀 값을 가져오고, 2차원 배열로 반환되며, 여기서 셀 값은 `string` 유형으로 변환됩니다. 셀 형식을 셀 값에 적용할 수 있으면 적용된 값을 사용하고, 그렇지 않으면 원래 값을 사용합니다.

예를 들어, `Sheet1` 이라는 워크 시트에서 열을 기준으로 모든 셀의 값을 가져 오십시오.

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

## 행으로 모든 셀 값 가져 오기 {#GetRows}

```go
func (f *File) GetRows(sheet string, opts ...Options) ([][]string, error)
```

GetRows 는 시트의 모든 행을 지정된 워크시트 이름 으로 반환하고, 2 차원 배열로 반환되며, 여기서 셀 값은 `string` 유형으로 변환됩니다. 셀 형식을 셀 값에 적용할 수 있으면 적용된 값을 사용하고, 그렇지 않으면 원래 값을 사용합니다. GetRows 가 값 또는 수식 셀이 있는 행을 가져오면 각 행의 꼬리에 있는 계속해서 비어 있는 셀을 건너뛰므로 각 행의 길이가 일치하지 않을 수 있습니다.

예를 들어, `Sheet1` 이라는 워크 시트에서 모든 셀의 값을 행으로 가로지 릅니다.

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

## 하이퍼 링크 가져 오기 {#GetCellHyperLink}

```go
func (f *File) GetCellHyperLink(sheet, axis string) (bool, string, error)
```

지정된 워크시트 이름 및 셀 좌표를 기반으로 셀 하이퍼링크를 가져옵니다. 셀에 하이퍼링크가 있는 경우 `true` 와 링크 주소를 반환하고 그렇지 않으면 `false` 와 빈 링크 주소를 반환합니다.

예를 들어 `Sheet1` 이라는 워크시트에서 `H6` 셀에 대한 하이퍼링크를 가져옵니다.

```go
link, target, err := f.GetCellHyperLink("Sheet1", "H6")
```

## 스타일 색인 가져 오기 {#GetCellStyle}

```go
func (f *File) GetCellStyle(sheet, axis string) (int, error)
```

셀 스타일 인덱스는 지정된 워크시트 이름 및 셀 좌표에서 가져오며, 얻은 인덱스는 셀 스타일을 복사할 때 `SetCellValue` 함수를 호출하는 매개 변수로 사용할 수 있습니다.

## 셀 병합 {#MergeCell}

```go
func (f *File) MergeCell(sheet, hCell, vCell string) error
```

지정된 시트 이름 및 셀 좌표 범위를 기반으로 셀을 병합합니다. 병합 범위 내에서는 왼쪽 위 셀의 값만 유지되며 다른 셀의 값은 무시됩니다. 예를 들어 `Sheet1` 이라는 워크시트의 `D3:E9` 영역에서 셀을 병합합니다.

```go
err := f.MergeCell("Sheet1", "D3", "E9")
```

지정된 셀 좌표 영역이 다른 기존 병합셀과 겹치면 기존 병합된 셀이 삭제됩니다.

## 셀 병합 취소 {#UnmergeCell}

```go
func (f *File) UnmergeCell(sheet string, hCell, vCell string) error
```

UnmergeCell 은 주어진 좌표 영역을 병합 해제하는 기능을 제공합니다. 예를 들어 `Sheet1` 의 `D3:E9` 영역 병합 해제:

```go
err := f.UnmergeCell("Sheet1", "D3", "E9")
```

주의: 겹쳐진 영역도 병합되지 않습니다.

## 병합 셀 가져 오기 {#GetMergeCells}

GetMergeCells 는 현재 워크 시트에서 병합 된 모든 셀을 얻을 수 있는 함수를 제공합니다.

```go
func (f *File) GetMergeCells(sheet string) ([]MergeCell, error)
```

### 병합된 셀 값 가져오기

```go
func (m *MergeCell) GetCellValue() string
```

GetCellValue 는 병합된 셀 값을 반환합니다.

### 병합된 범위의 왼쪽 상단 셀 좌표 가져오기

```go
func (m *MergeCell) GetStartAxis() string
```

GetStartAxis 는 병합된 범위의 왼쪽 상단 셀 좌표를 반환합니다, 예: `C2`.

### 병합된 범위의 오른쪽 하단 셀 좌표 가져오기

```go
func (m *MergeCell) GetEndAxis() string
```

GetEndAxis 는 병합된 범위의 오른쪽 하단 셀 좌표를 반환합니다, 예: `D4`.

## 의견 추가 {#AddComment}

```go
func (f *File) AddComment(sheet, cell, format string) error
```

AddComment 는 지정된 워크 시트 인덱스, 셀 및 형식 집합 (예: 작성자 및 텍스트) 을 사용하여 시트에 주석을 추가하는 방법을 제공합니다. 최대 작성자 길이는 255 이고 최대 텍스트 길이는 32512 입니다. 예를 들어 `Sheet1!$A$3` 에 주석을 추가합니다:

<p align="center"><img width="612" src="./images/comment.png" alt="Excel 문서에 주석 추가"></p>

```go
err := f.AddComment("Sheet1", "A3", `{"author":"Excelize: ","text":"This is a comment."}`)
```

## 의견 가져 오기 {#GetComments}

```go
func (f *File) GetComments() (comments map[string][]Comment)
```

GetComments 는 모든 주석을 검색하고 워크시트 이름 맵을 워크시트 주석에 반환합니다.

## 셀 수식 설정 {#SetCellFormula}

```go
func (f *File) SetCellFormula(sheet, axis, formula string, opts ...FormulaOpts) error
```

SetCellFormula 는 주어진 워크시트 이름 과 셀 수식 설정에 따라 셀에 수식을 설정하는 기능을 제공합니다. 수식 셀의 결과는 Office Excel 응용 프로그램에서 워크시트를 열거나 [CalcCellValue](cell.md#CalcCellValue) 함수를 사용할 수 있을 때 계산된 셀 값을 얻을 수 있습니다. 엑셀 응용 프로그램이 통합 문서를 열었을 때 수식을 자동으로 계산하지 않으면 셀 수식 기능을 설정한 후 [UpdateLinkedValue](utils.md#UpdateLinkedValue) 를 호출하십시오.

- 예 1, `Sheet1` 의 `A3` 셀에 대해 일반 수식 `=SUM(A1,B1)` 설정:

```go
err := f.SetCellFormula("Sheet1", "A3", "=SUM(A1,B1)")
```

- 예 2, `Sheet1` 의 `A3` 셀에 대해 1차원 수직 상수 배열(행 배열) 수식 `1,2,3` 을 설정합니다:

```go
err := f.SetCellFormula("Sheet1", "A3", "={1,2,3}")
```

- 예 3, `Sheet1` 의 `A3` 셀에 대해 1차원 수평 상수 배열(열 배열) 수식 `"a","b","c"` 를 설정합니다:

```go
err := f.SetCellFormula("Sheet1", "A3", "={\"a\",\"b\",\"c\"}")
```

- 예 4, `Sheet1` 의 `A3` 셀에 대해 2차원 상수 배열 수식 `{1,2,"a","b"}` 을 설정합니다:

```go
formulaType, ref := excelize.STCellFormulaTypeArray, "A3:A3"
err := f.SetCellFormula("Sheet1", "A3", "={1,2,\"a\",\"b\"}",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- 예 5, `Sheet1` 의 `A3` 셀에 대해 범위 배열 수식 `A1:A2` 를 설정합니다:

```go
formulaType, ref := excelize.STCellFormulaTypeArray, "A3:A3"
err := f.SetCellFormula("Sheet1", "A3", "=A1:A2",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- 예 6, `Sheet1` 의 `C1:C5` 셀에 대해 공유 수식 `=A1+B1` 를 설정하고, `C1` 은 마스터 셀입니다:

```go
formulaType, ref := excelize.STCellFormulaTypeShared, "C1:C5"
err := f.SetCellFormula("Sheet1", "C1", "=A1+B1",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- 예 7, `Sheet1` 의 `C2` 셀에 대해 테이블 수식 `=SUM(Table1[[A]:[B]])` 를 설정합니다:

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    for idx, row := range [][]interface{}{{"A", "B", "C"}, {1, 2}} {
        if err := f.SetSheetRow("Sheet1", fmt.Sprintf("A%d", idx+1), &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    if err := f.AddTable("Sheet1", "A1", "C2",
        `{"table_name":"Table1","table_style":"TableStyleMedium2"}`); err != nil {
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

## 셀 수식 가져 오기 {#GetCellFormula}

```go
func (f *File) GetCellFormula(sheet, axis string) (string, error)
```

지정된 워크시트 이름 및 셀 좌표를 기반으로 셀에 수식을 가져옵니다.

## 셀 값 계산 {#CalcCellValue}

```go
func (f *File) CalcCellValue(sheet, cell string) (string, error)
```

CalcCellValue 는 계산된 셀 값을 가져오는 함수를 제공합니다. 이 기능은 현재 처리 중입니다. 반복 계산, 암시적 교차, 명시적 교차, 배열 수식, 테이블 수식 및 일부 기타 수식은 현재 지원되지 않습니다.

지원되는 공식 :

```text
ABS
ACCRINT
ACCRINTM
ACOS
ACOSH
ACOT
ACOTH
ADDRESS
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
