# 통합 문서

## Excel 문서 만들기 {#NewFile}

```go
func NewFile() *File
```

`NewFile` 을 사용 하 여 새 Excel 통합 문서를 만들고 새로 만든 통합 문서에는 기본적으로 `Sheet1` 이라는 워크시트가 포함 됩니다.

## 열기 {#OpenFile}

```go
func OpenFile(filename string) (*File, error)
```

`OpenFile` 을 사용 하 여 기존 Excel 문서를 엽니다.

## 저장 {#Save}

```go
func (f *File) Save() error
```

`Save` 을 사용 하 여 Excel 문서에 대 한 편집 내용을 저장 합니다.

## 다른 이름으로 저장 {#SaveAs}

```go
func (f *File) SaveAs(name string) error
```

Excel 문서를 지정 된 파일로 저장 하려면 `SaveAs` 를 사용 하십시오.

## 워크 시트 만들기 {#NewSheet}

```go
func (f *File) NewSheet(name string) int
```

지정 된 워크 시트 이름을 기반으로 새 워크 시트를 추가 하 고 워크 시트 인덱스로 돌아갑니다. 새로 만든 통합 문서에는 `Sheet1` 이라는 기본 통합 문서가 포함 됩니다.

## 워크 시트 삭제 {#DeleteSheet}

```go
func (f *File) DeleteSheet(name string)
```

지정 된 워크시트 이름을 기반으로 지정한 워크시트를 삭제 합니다. 이 메서드는 삭제 된 워크시트와 관련 된 수식, 참조, 차트 및 기타 요소에 영향을 주는 주의 해 서 사용 해야 합니다. 삭제 된 워크시트에서 값을 참조 하는 다른 구성 요소가 있는 경우 오류 프롬프트가 발생 하 고 통합 문서를 열지 못하게 됩니다. 하나의 워크시트가 통합 문서에 포함 된 경우이 메서드를 호출 해도 유효 하지 않습니다.

## 워크 시트 복사 {#CopySheet}

```go
func (f *File) CopySheet(from, to int) error
```

대상 워크시트 인덱스에는 지정 된 복사 된 워크시트와 워크시트를 복사 하는 대상 워크시트 인덱스에 따라 개발자가 이미 존재 하는지 확인 해야 합니다. 셀 값과 수식이 포함 된 워크시트 간의 복제는 현재 지원 되며 테이블, 그림, 차트 및 피벗 테이블과 같은 요소를 포함 하는 워크시트 간의 복제를 지원 하지 않습니다.

```go
// Sheet1 이름이 있는 워크시트가 이미 있습니다 ...
index := xlsx.NewSheet("Sheet2")
err := xlsx.CopySheet(1, index)
return err
```

## 워크 시트 배경 {#SetSheetBackground}

```go
func (f *File) SetSheetBackground(sheet, picture string) error
```

지정 된 워크시트 이름과 그림 주소를 기준으로 지정한 워크시트에 대 한 타일 효과의 배경 그림을 설정 합니다.

## 기본 워크 시트 설정 {#SetActiveSheet}

```go
func (f *File) SetActiveSheet(index int)
```

지정 된 인덱스 값을 기준으로 기본 워크시트를 설정 하면 인덱스 값이 `0` 보다 커야 하 고 통합 문서에 포함 된 누적 워크시트의 총 개수 보다 작아야 합니다.

## 활성 시트 색인 가져 오기 {#GetActiveSheetIndex}

```go
func (f *File) GetActiveSheetIndex() int
```

기본 워크시트의 인덱스를 가져오고 기본 워크시트를 찾을 수 없는 경우 `0` 을 반환 합니다.

## 워크 시트 뷰 속성 가져 오기 {#GetSheetViewOptions}

```go
func (f *File) GetSheetViewOptions(name string, viewIndex int, opts ...SheetViewOptionPtr) error
```

지정 된 워크 시트 이름, 뷰 인덱스 및 뷰 매개 변수를 기반으로 워크 시트 보기 속성 가져 오기, `viewIndex` 가 음수 이면 역방향으로 계산 됩니다 (`-1` 은 마지막 보기를 나타냄).

선택적 뷰 매개 변수 | 유형
---|---
DefaultGridColor|bool
RightToLeft|bool
ShowFormulas|bool
ShowGridLines|bool
ShowRowColHeaders|bool

- 예 1: `Sheet1` 이라는 워크 시트의 마지막 뷰에 대 한 그리드 선 특성 설정을 가져옵니다.

```go
var showGridLines excelize.ShowGridLines
err = f.GetSheetViewOptions("Sheet1", -1, &showGridLines)
```

- 예 2:

```go
xl := excelize.NewFile()
const sheet = "Sheet1"

var (
    defaultGridColor  excelize.DefaultGridColor
    rightToLeft       excelize.RightToLeft
    showFormulas      excelize.ShowFormulas
    showGridLines     excelize.ShowGridLines
    showRowColHeaders excelize.ShowRowColHeaders
    zoomScale         excelize.ZoomScale
    topLeftCell       excelize.TopLeftCell
)

if err := xl.GetSheetViewOptions(sheet, 0,
    &defaultGridColor,
    &rightToLeft,
    &showFormulas,
    &showGridLines,
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
fmt.Println("- showRowColHeaders:", showRowColHeaders)
fmt.Println("- zoomScale:", zoomScale)
fmt.Println("- topLeftCell:", `"`+topLeftCell+`"`)

if err := xl.SetSheetViewOptions(sheet, 0, excelize.TopLeftCell("B2")); err != nil {
    panic(err)
}

if err := xl.GetSheetViewOptions(sheet, 0, &topLeftCell); err != nil {
    panic(err)
}

if err := xl.SetSheetViewOptions(sheet, 0, excelize.ShowGridLines(false)); err != nil {
    panic(err)
}

if err := xl.GetSheetViewOptions(sheet, 0, &showGridLines); err != nil {
    panic(err)
}

fmt.Println("After change:")
fmt.Println("- showGridLines:", showGridLines)
fmt.Println("- topLeftCell:", topLeftCell)
```

출력 가져오기:

```text
Default:
- defaultGridColor: true
- rightToLeft: false
- showFormulas: false
- showGridLines: true
- showRowColHeaders: true
- zoomScale: 0
- topLeftCell: ""
After change:
- showGridLines: false
- topLeftCell: B2
```

## 워크 시트 페이지 레이아웃 설정 {#SetPageLayout}

```go
func (f *File) SetPageLayout(sheet string, opts ...PageLayoutOption) error
```

지정 된 워크시트 이름 및 페이지 레이아웃 매개 변수를 기반으로 워크시트의 페이지 레이아웃 속성을 설정 합니다. 현재 설정에 대해 지원 되는 페이지 레이아웃 속성:

- `PageLayoutOrientation` 메서드로 페이지 레이아웃 방향 설정, 기본 페이지 레이아웃 방향은 "세로" 입니다. 다음 표는 Excelize 에서 페이지 레이아웃 방향의 `PageLayoutOrientation` 매개 변수 목록입니다:

매개 변수 | 방향
---|---
OrientationPortrait | 세로
OrientationLandscape | 가로

- `PageLayoutPaperSize` 방법을 사용 하 여 페이지 용지의 크기를 설정 합니다, 기본 페이지 레이아웃 크기는 "Letter paper (8.5 in. by 11 in.)" 입니다. 다음 표는 excel에서 페이지 레이아웃 크기와 인덱스 `PageLayoutPaperSize` 매개 변수를 비교한 것입니다:

색인 | 용지 크기
---|---
1   | Letter paper (8.5 in. by 11 in.)
2   | Letter small paper (8.5 in. by 11 in.)
3   | Tabloid paper (11 in. by 17 in.)
4   | Ledger paper (17 in. by 11 in.)
5   | Legal paper (8.5 in. by 14 in.)
6   | Statement paper (5.5 in. by 8.5 in.)
7   | Executive paper (7.25 in. by 10.5 in.)
8   | A3 paper (297 mm by 420 mm)
9   | A4 paper (210 mm by 297 mm)
10  | A4 small paper (210 mm by 297 mm)
11  | A5 paper (148 mm by 210 mm)
12  | B4 paper (250 mm by 353 mm)
13  | B5 paper (176 mm by 250 mm)
14  | Folio paper (8.5 in. by 13 in.)
15  | Quarto paper (215 mm by 275 mm)
16  | Standard paper (10 in. by 14 in.)
17  | Standard paper (11 in. by 17 in.)
18  | Note paper (8.5 in. by 11 in.)
19  | #9 envelope (3.875 in. by 8.875 in.)
20  | #10 envelope (4.125 in. by 9.5 in.)
21  | #11 envelope (4.5 in. by 10.375 in.)
22  | #12 envelope (4.75 in. by 11 in.)
23  | #14 envelope (5 in. by 11.5 in.)
24  | C paper (17 in. by 22 in.)
25  | D paper (22 in. by 34 in.)
26  | E paper (34 in. by 44 in.)
27  | DL envelope (110 mm by 220 mm)
28  | C5 envelope (162 mm by 229 mm)
29  | C3 envelope (324 mm by 458 mm)
30  | C4 envelope (229 mm by 324 mm)
31  | C6 envelope (114 mm by 162 mm)
32  | C65 envelope (114 mm by 229 mm)
33  | B4 envelope (250 mm by 353 mm)
34  | B5 envelope (176 mm by 250 mm)
35  | B6 envelope (176 mm by 125 mm)
36  | Italy envelope (110 mm by 230 mm)
37  | Monarch envelope (3.875 in. by 7.5 in.).
38  | 6 3/4 envelope (3.625 in. by 6.5 in.)
39  | US standard fanfold (14.875 in. by 11 in.)
40  | German standard fanfold (8.5 in. by 12 in.)
41  | German legal fanfold (8.5 in. by 13 in.)
42  | ISO B4 (250 mm by 353 mm)
43  | Japanese postcard (100 mm by 148 mm)
44  | Standard paper (9 in. by 11 in.)
45  | Standard paper (10 in. by 11 in.)
46  | Standard paper (15 in. by 11 in.)
47  | Invite envelope (220 mm by 220 mm)
50  | Letter extra paper (9.275 in. by 12 in.)
51  | Legal extra paper (9.275 in. by 15 in.)
52  | Tabloid extra paper (11.69 in. by 18 in.)
53  | A4 extra paper (236 mm by 322 mm)
54  | Letter transverse paper (8.275 in. by 11 in.)
55  | A4 transverse paper (210 mm by 297 mm)
56  | Letter extra transverse paper (9.275 in. by 12 in.)
57  | SuperA/SuperA/A4 paper (227 mm by 356 mm)
58  | SuperB/SuperB/A3 paper (305 mm by 487 mm)
59  | Letter plus paper (8.5 in. by 12.69 in.)
60  | A4 plus paper (210 mm by 330 mm)
61  | A5 transverse paper (148 mm by 210 mm)
62  | JIS B5 transverse paper (182 mm by 257 mm)
63  | A3 extra paper (322 mm by 445 mm)
64  | A5 extra paper (174 mm by 235 mm)
65  | ISO B5 extra paper (201 mm by 276 mm)
66  | A2 paper (420 mm by 594 mm)
67  | A3 transverse paper (297 mm by 420 mm)
68  | A3 extra transverse paper (322 mm by 445 mm)
69  | Japanese Double Postcard (200 mm x 148 mm)
70  | A6 (105 mm x 148 mm)
71  | Japanese Envelope Kaku #2
72  | Japanese Envelope Kaku #3
73  | Japanese Envelope Chou #3
74  | Japanese Envelope Chou #4
75  | Letter Rotated (11in x 8 1/2 11 in)
76  | A3 Rotated (420 mm x 297 mm)
77  | A4 Rotated (297 mm x 210 mm)
78  | A5 Rotated (210 mm x 148 mm)
79  | B4 (JIS) Rotated (364 mm x 257 mm)
80  | B5 (JIS) Rotated (257 mm x 182 mm)
81  | Japanese Postcard Rotated (148 mm x 100 mm)
82  | Double Japanese Postcard Rotated (148 mm x 200 mm)
83  | A6 Rotated (148 mm x 105 mm)
84  | Japanese Envelope Kaku #2 Rotated
85  | Japanese Envelope Kaku #3 Rotated
86  | Japanese Envelope Chou #3 Rotated
87  | Japanese Envelope Chou #4 Rotated
88  | B6 (JIS) (128 mm x 182 mm)
89  | B6 (JIS) Rotated (182 mm x 128 mm)
90  | (12 in x 11 in)
91  | Japanese Envelope You #4
92  | Japanese Envelope You #4 Rotated
93  | PRC 16K (146 mm x 215 mm)
94  | PRC 32K (97 mm x 151 mm)
95  | PRC 32K(Big) (97 mm x 151 mm)
96  | PRC Envelope #1 (102 mm x 165 mm)
97  | PRC Envelope #2 (102 mm x 176 mm)
98  | PRC Envelope #3 (125 mm x 176 mm)
99  | PRC Envelope #4 (110 mm x 208 mm)
100 | PRC Envelope #5 (110 mm x 220 mm)
101 | PRC Envelope #6 (120 mm x 230 mm)
102 | PRC Envelope #7 (160 mm x 230 mm)
103 | PRC Envelope #8 (120 mm x 309 mm)
104 | PRC Envelope #9 (229 mm x 324 mm)
105 | PRC Envelope #10 (324 mm x 458 mm)
106 | PRC 16K Rotated
107 | PRC 32K Rotated
108 | PRC 32K(Big) Rotated
109 | PRC Envelope #1 Rotated (165 mm x 102 mm)
110 | PRC Envelope #2 Rotated (176 mm x 102 mm)
111 | PRC Envelope #3 Rotated (176 mm x 125 mm)
112 | PRC Envelope #4 Rotated (208 mm x 110 mm)
113 | PRC Envelope #5 Rotated (220 mm x 110 mm)
114 | PRC Envelope #6 Rotated (230 mm x 120 mm)
115 | PRC Envelope #7 Rotated (230 mm x 160 mm)
116 | PRC Envelope #8 Rotated (309 mm x 120 mm)
117 | PRC Envelope #9 Rotated (324 mm x 229 mm)
118 | PRC Envelope #10 Rotated (458 mm x 324 mm)

- 예를 들어 `Sheet1` 이라는 워크시트 페이지 레이아웃을 가로로 설정 하 고 A4 small paper (210 mm by 297 mm) 용지를 사용 합니다:

```go
xl := excelize.NewFile()
const sheet = "Sheet1"

if err := xl.SetPageLayout(
    "Sheet1",
    excelize.PageLayoutOrientation(excelize.OrientationLandscape),
); err != nil {
    panic(err)
}
if err := xl.SetPageLayout(
    "Sheet1",
    excelize.PageLayoutPaperSize(10),
); err != nil {
    panic(err)
}
```

## 워크 시트 페이지 레이아웃 가져 오기 {#GetPageLayout}

```go
func (f *File) GetPageLayout(sheet string, opts ...PageLayoutOptionPtr) error
```

지정 된 워크시트 이름 및 페이지 레이아웃 매개 변수를 기반으로 워크시트의 페이지 레이아웃 속성을 가져옵니다.

- `PageLayoutOrientation` 방법으로 페이지 레이아웃 방향 가져오기
- `PageLayoutPaperSize` 방법으로 페이지 용지 크기 가져오기

예를 들어 `Sheet1` 이라는 워크시트 페이지 레이아웃 설정을 가져옵니다:

```go
xl := excelize.NewFile()
const sheet = "Sheet1"
var (
    orientation excelize.PageLayoutOrientation
    paperSize   excelize.PageLayoutPaperSize
)
if err := xl.GetPageLayout("Sheet1", &orientation); err != nil {
    panic(err)
}
if err := xl.GetPageLayout("Sheet1", &paperSize); err != nil {
    panic(err)
}
fmt.Println("Defaults:")
fmt.Printf("- orientation: %q\n", orientation)
fmt.Printf("- paper size: %d\n", paperSize)
// Output:
// Defaults:
// - orientation: "portrait"
// - paper size: 1
```
