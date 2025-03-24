# 통합 문서

`Options` 은 스프레드 시트를 읽고 쓰는 옵션을 정의합니다.

```go
type Options struct {
    MaxCalcIterations uint
    Password          string
    RawCellValue      bool
    UnzipSizeLimit    int64
    UnzipXMLSizeLimit int64
    ShortDatePattern  string
    LongDatePattern   string
    LongTimePattern   string
    CultureInfo       CultureName
}
```

`MaxCalcIterations` 는 반복 계산을 위한 최대 반복을 지정하며 기본값은 0 입니다.

`Password` 는 스프레드시트의 비밀번호를 일반 텍스트로 지정합니다.

`RawCellValue` 는 셀 값에 숫자 형식을 적용할지 아니면 원시 값을 가져올지 지정합니다.

`UnzipSizeLimit` 은 스프레드시트를 열 때 압축 해제 크기 제한을 바이트 단위로 지정합니다. 이 값은 `UnzipXMLSizeLimit` 이상이어야 하며 기본 크기 제한은 16GB 입니다.

`UnzipXMLSizeLimit` 은 압축 해제 워크시트 및 공유 문자열 테이블의 메모리 제한을 바이트 단위로 지정합니다. 파일 크기가 이 값을 초과하면 워크시트 XML이 시스템 임시 디렉토리로 추출됩니다. 이 값은 기본값인 `UnzipSizeLimit` 보다 작거나 같아야 합니다. 값은 16MB 입니다.

`ShortDatePattern` 은 간단한 날짜 숫자 형식 코드를 지정합니다. 스프레드시트 애플리케이션에서 날짜 형식은 날짜 및 시간 일련 번호를 날짜 값으로 표시합니다. 별표 (\*) 로 시작하는 날짜 형식은 운영 체제에 지정된 지역 날짜 및 시간 설정의 변경 사항에 응답합니다. 별표가 없는 형식은 운영 체제 설정의 영향을 받지 않습니다. 별표로 시작하는 적용 날짜 형식을 지정하는 데 사용되는 `ShortDatePattern` 입니다.

`LongDatePattern` 은 긴 날짜 숫자 형식 코드를 지정합니다.

`LongTimePattern` 은 긴 시간 숫자 형식 코드를 지정합니다.

`CultureInfo` 는 시스템의 현지 언어 설정에 따른 영향을 받는 내장 언어 번호 형식 코드를 적용하기 위한 국가 코드를 지정합니다.

`HeaderFooterImagePositionType` 은 헤더와 푸터 이미지 위치의 유형입니다.

```go
type HeaderFooterImagePositionType byte
```

이 섹션에서는 워크시트 머리글 및 바닥글 이미지 위치 유형 열거형을 정의합니다.

```go
const (
    HeaderFooterImagePositionLeft HeaderFooterImagePositionType = iota
    HeaderFooterImagePositionCenter
    HeaderFooterImagePositionRight
)
```

`CalcPropsOptions` 는 애플리케이션이 계산 상태와 세부 정보를 기록하는 데 사용하는 속성 컬렉션을 정의합니다.

```go
type CalcPropsOptions struct {
    CalcID                *uint
    CalcMode              *string
    FullCalcOnLoad        *bool
    RefMode               *string
    Iterate               *bool
    IterateCount          *uint
    IterateDelta          *float64
    FullPrecision         *bool
    CalcCompleted         *bool
    CalcOnSave            *bool
    ConcurrentCalc        *bool
    ConcurrentManualCount *uint
    ForceFullCalc         *bool
}
```

## Excel 문서 만들기 {#NewFile}

```go
func NewFile(opts ...Options) *File
```

`NewFile` 을 사용 하 여 새 Excel 통합 문서를 만들고 새로 만든 통합 문서에는 기본적으로 `Sheet1` 이라는 워크시트가 포함 됩니다.

## 열기 {#OpenFile}

```go
func OpenFile(filename string, opts ...Options) (*File, error)
```

`OpenFile` 을 사용 하 여 기존 Excel 문서를 엽니다. 예를 들어, 암호로 보호 된 스프레드 시트를 엽니 다:

```go
f, err := excelize.OpenFile("Book1.xlsx", excelize.Options{Password: "password"})
if err != nil {
    return
}
```

스프레드시트를 연 후 [`Close()`](workbook.md#Close) 로 파일을 닫습니다.

## 열린 데이터 스트림 {#OpenReader}

```go
func OpenReader(r io.Reader, opts ...Options) (*File, error)
```

OpenReader 는 `io.Reader` 에서 데이터 스트림을 읽고 채워진 스프레드 시트 파일을 반환합니다.

예를 들어, 업로드 템플리트를 처리 할 HTTP 서버를 작성한 후 새 워크 시트가 추가 된 응답 다운로드 파일:

```go
package main

import (
    "fmt"
    "net/http"

    "github.com/xuri/excelize/v2"
)

func process(w http.ResponseWriter, req *http.Request) {
    file, _, err := req.FormFile("file")
    if err != nil {
        fmt.Fprint(w, err.Error())
        return
    }
    defer file.Close()
    f, err := excelize.OpenReader(file)
    if err != nil {
        fmt.Fprint(w, err.Error())
        return
    }
    f.Path = "Book1.xlsx"
    f.NewSheet("NewSheet")
    w.Header().Set("Content-Disposition", fmt.Sprintf("attachment; filename=%s", f.Path))
    w.Header().Set("Content-Type", req.Header.Get("Content-Type"))
    if err := f.Write(w); err != nil {
        fmt.Fprint(w, err.Error())
    }
}

func main() {
    http.HandleFunc("/process", process)
    http.ListenAndServe(":8090", nil)
}
```

cURL 로 테스트:

```bash
curl --location --request GET 'http://127.0.0.1:8090/process' \
--form 'file=@/tmp/template.xltx' -O -J
```

## 저장 {#Save}

```go
func (f *File) Save(opts ...Options) error
```

`Save` 을 사용 하 여 Excel 문서에 대 한 편집 내용을 저장 합니다.

## 다른 이름으로 저장 {#SaveAs}

```go
func (f *File) SaveAs(name string, opts ...Options) error
```

Excel 문서를 지정 된 파일로 저장 하려면 `SaveAs` 를 사용 하십시오.

## 통합 문서 닫기 {#Close}

```go
func (f *File) Close() error
```

Close 는 스프레드시트에 대해 열려 있는 임시 파일을 닫고 정리합니다.

## 워크 시트 만들기 {#NewSheet}

```go
func (f *File) NewSheet(sheet string) (int, error)
```

NewSheet 는 워크 시트 이름을 지정하여 새 시트를 만드는 기능을 제공하고 추가 된 후 통합 문서 (스프레드 시트)의 시트 인덱스를 반환합니다. 새 스프레드 시트 파일을 만들 때 `Sheet1` 이라는 기본 워크 시트가 생성됩니다.

## 워크 시트 삭제 {#DeleteSheet}

```go
func (f *File) DeleteSheet(sheet string) error
```

DeleteSheet 는 지정된 워크 시트 이름으로 통합 문서의 워크 시트를 삭제하는 기능을 제공하며 시트 이름은 대/소문자를 구분하지 않습니다. 이 방법은 수식, 차트 등과 같은 참조의 변경에 영향을 주는 주의해서 사용하십시오. 삭제된 워크시트의 참조된 값이 있으면 워크시트를 열 때 파일 오류가 발생합니다. 이 함수는 워크시트가 하나만 남아 있으면 유효하지 않습니다.

## 이동 워크시트 {#MoveSheet}

```go
func (f *File) MoveSheet(source, target string) error
```

MoveSheet 는 워크북에서 지정된 위치로 시트를 이동합니다. 이 함수는 대상 시트 앞으로 소스 시트를 이동합니다. 이동한 후 다른 시트는 왼쪽이나 오른쪽으로 이동합니다. 시트가 이미 대상 위치에 있는 경우 이 함수는 아무런 동작도 수행하지 않습니다. 이 함수가 이동한 후 모든 시트를 그룹 해제하지는 않습니다. 예를 들어, `Sheet2` 를 `Sheet1` 앞으로 이동합니다:

```go
err := f.MoveSheet("Sheet2", "Sheet1")
```

## 워크 시트 복사 {#CopySheet}

```go
func (f *File) CopySheet(from, to int) error
```

대상 워크시트 인덱스에는 지정 된 복사 된 워크시트와 워크시트를 복사 하는 대상 워크시트 인덱스에 따라 개발자가 이미 존재 하는지 확인 해야 합니다. 셀 값과 수식이 포함 된 워크시트 간의 복제는 현재 지원 되며 테이블, 그림, 차트 및 피벗 테이블과 같은 요소를 포함 하는 워크시트 간의 복제를 지원 하지 않습니다.

```go
// Sheet1 이름이 있는 워크시트가 이미 있습니다 ...
index, err := f.NewSheet("Sheet2")
if err != nil {
    fmt.Println(err)
    return
}
err := f.CopySheet(1, index)
```

## 그룹 워크시트 {#GroupSheets}

```go
func (f *File) GroupSheets(sheets []string) error
```

GroupSheets 는 주어진 워크시트 이름으로 워크시트를 그룹화하는 기능을 제공합니다. 그룹 워크시트에는 활성 워크시트가 있어야 합니다.

## 워크시트 그룹 해제 {#UngroupSheets}

```go
func (f *File) UngroupSheets() error
```

UngroupSheets 는 워크시트를 그룹 해제하는 기능을 제공합니다.

## 워크 시트 배경 {#SetSheetBackground}

```go
func (f *File) SetSheetBackground(sheet, picture string) error
```

SetSheetBackground 는 주어진 워크시트 이름과 파일 경로로 배경 그림을 설정하는 기능을 제공합니다. 지원되는 이미지 유형: BMP, EMF, EMZ, GIF, JPEG, JPG, PNG, SVG, TIF, TIFF, WMF 및 WMZ.

```go
func (f *File) SetSheetBackgroundFromBytes(sheet, extension string, picture []byte) error
```

SetSheetBackgroundFromBytes 는 주어진 워크시트 이름, 확장자 이름 및 이미지 데이터로 배경 그림을 설정하는 기능을 제공합니다. 지원되는 이미지 유형: BMP, EMF, EMZ, GIF, JPEG, JPG, PNG, SVG, TIF, TIFF, WMF 및 WMZ.

## 기본 워크 시트 설정 {#SetActiveSheet}

```go
func (f *File) SetActiveSheet(index int)
```

SetActiveSheet 는 지정된 인덱스로 통합 문서의 기본 활성 시트를 설정하는 기능을 제공합니다. 활성 인덱스는 [`GetSheetMap`](sheet.md#GetSheetMap) 함수가 리턴 한 ID와 다릅니다. 총 워크 시트 수보다 `0` 보다 크거나 같아야합니다.

## 활성 시트 색인 가져 오기 {#GetActiveSheetIndex}

```go
func (f *File) GetActiveSheetIndex() int
```

기본 워크시트의 인덱스를 가져오고 기본 워크시트를 찾을 수 없는 경우 `0` 을 반환 합니다.

## 워크 시트 가시성 설정 {#SetSheetVisible}

```go
func (f *File) SetSheetVisible(sheet string, visible bool, veryHidden ...bool) error
```

SetSheetVisible 은 지정된 워크 시트 이름으로 표시되는 워크 시트를 설정하는 함수를 제공합니다. 통합 문서에는 최소한 하나의 보이는 워크 시트가 있어야합니다. 지정된 워크 시트가 활성화 된 경우이 설정은 무효화됩니다. 세 번째 선택적 `veryHidden` 매개변수는 `visible` 이 `false` 인 경우에만 작동합니다.

예를 들어,`Sheet1` 을 숨 깁니다.

```go
err := f.SetSheetVisible("Sheet1", false)
```

## 워크 시트 가시성 확보 {#GetSheetVisible}

```go
func (f *File) GetSheetVisible(sheet string) (bool, error)
```

GetSheetVisible 은 주어진 워크 시트 이름으로 볼 수있는 워크 시트를 가져 오는 기능을 제공합니다. 예를 들어, `Sheet1` 의 표시 상태 가져 오기:

```go
visible, err := f.GetSheetVisible("Sheet1")
```

## 워크 시트 속성 설정 {#SetSheetProps}

```go
func (f *File) SetSheetProps(sheet string, opts *SheetPropsOptions) error
```

SetSheetProps 는 워크시트 속성을 설정하는 함수를 제공합니다. 설정할 수 있는 속성은 다음과 같습니다:

옵션|유형|설명설명
---|---|---
CodeName                          | `*string`  | 시간이 지남에 따라 변경되지 않아야 하며 사용자 입력에서 변경되지 않는 시트의 안정적인 이름을 지정합니다. 이 이름은 코드에서 특정 시트를 참조하는 데 사용해야 합니다.
EnableFormatConditionsCalculation | `*bool`    | 조건부 서식 계산을 평가할지 여부를 나타냅니다. false로 설정된 경우 상위 N 규칙의 색상 배율 또는 데이터 막대 또는 임계값의 최소/최대 값은 업데이트되지 않습니다. 기본적으로 조건부 형식 "calc" 는 꺼져 있습니다.
Published                         | `*bool`    | 워크시트가 게시되었는지 여부를 나타내는 기본값은 `true` 입니다.
AutoPageBreaks                    | `*bool`    | 시트에 자동 페이지 나누기가 표시되는지 여부를 나타내는 기본값은 `true` 입니다.
FitToPage                         | `*bool`    | "페이지에 맞춤" 인쇄 옵션이 활성화되어 있는지 여부를 나타내는 기본값은 `false` 입니다.
TabColorIndexed                   | `*int`     | 인덱싱된 색상 값을 나타냅니다.
TabColorRGB                       | `*string`  | 표준 ARGB (알파 빨강 녹색 파랑) 색상 값을 나타냅니다.
TabColorTheme                     | `*int`     | 컬렉션에 제로 기반 인덱스를 나타내며 테마 파트에 표현된 특정 값을 참조합니다.
TabColorTint                      | `*float64` | 색상에 적용되는 색조 값을 지정하며, 기본값은 `0.0` 입니다.
OutlineSummaryBelow               | `*bool`    | 요약 행이 윤곽선의 세부 정보 아래에 나타나는지 여부를 나타내는 경우 윤곽선을 적용할 때 기본값은 `true` 입니다.
OutlineSummaryRight               | `*bool`    | 요약 열이 윤곽선의 세부 정보 오른쪽에 표시되는지 여부를 나타냅니다. 윤곽선을 적용할 때 기본값은 `true` 입니다.
BaseColWidth                      | `*uint8`   | 일반 스타일 글꼴의 최대 자릿수 너비의 문자 수를 지정합니다. 이 값에는 격자선에 대한 여백 패딩이나 추가 패딩이 포함되지 않습니다. 문자 수일 뿐이며 기본값은 `8` 입니다.
DefaultColWidth                   | `*float64` | 일반 스타일 글꼴의 최대 자릿수 너비의 문자 수로 측정된 기본 열 너비를 지정합니다.
DefaultRowHeight                  | `*float64` | 포인트 크기로 측정된 기본 행 높이를 지정합니다. 최적화를 통해 모든 행에 높이를 쓸 필요가 없습니다. 최적화를 달성하기 위해 대부분의 행에 사용자 정의 높이가있는 경우 작성할 수 있습니다.
CustomHeight                      | `*bool`    | 사용자 지정 높이를 지정하고, 기본값은 `false` 입니다.
ZeroHeight                        | `*bool`    | 행이 숨겨져 있는 경우 기본값은 `false` 를 지정합니다.
ThickTop                          | `*bool`    | 행에 기본적으로 두꺼운 위쪽 테두리가 있는 경우 기본값은 `false` 를 지정합니다.
ThickBottom                       | `*bool`    | 행에 기본적으로 두꺼운 아래쪽 테두리가 있는지 지정하며 기본값은 `false` 입니다.

예를 들어, 워크 시트 행을 기본적으로 숨김으로 설정하십시오:

<p align="center"><img width="612" src="./images/sheet_format_pr_01.png" alt="워크 시트 속성 설정"></p>

```go
f, enable := excelize.NewFile(), true
if err := f.SetSheetProps("Sheet1", &excelize.SheetPropsOptions{
    ZeroHeight: &enable,
}); err != nil {
    fmt.Println(err)
}
if err := f.SetRowVisible("Sheet1", 10, true); err != nil {
    fmt.Println(err)
}
f.SaveAs("Book1.xlsx")
```

## 워크 시트 속성 가져 오기 {#GetSheetProps}

```go
func (f *File) GetSheetProps(sheet string) (SheetPropsOptions, error)
```

GetSheetProps 는 워크시트 속성을 가져오는 함수를 제공합니다.

## 워크 시트보기 속성 설정 {#SetSheetView}

```go
func (f *File) SetSheetView(sheet string, viewIndex int, opts *ViewOptions) error
```

SetSheetView 는 시트 뷰 속성을 설정합니다. `viewIndex` 는 음수 일 수 있으며 그렇다면 뒤로 계산됩니다 (`-1` 은 마지막 뷰입니다). 설정할 수 있는 속성은 다음과 같습니다:

옵션|유형|설명설명
---|---|---
DefaultGridColor  | `*bool`    | 사용 중인 응용 프로그램이 기본 격자선 색상(시스템에 따라 다름)을 사용해야 함을 나타냅니다. colorId 에 지정된 모든 색상을 재정의하고 기본값은 `true` 입니다.
RightToLeft       | `*bool`    | 시트가 "오른쪽에서 왼쪽으로" 표시 모드에 있는지 여부를 나타냅니다. 이 모드에서 A 열은 맨 오른쪽, B 열에 있습니다. 는 A 열의 왼쪽 열 중 하나입니다. 또한 셀의 정보는 오른쪽에서 왼쪽 형식으로 표시되며 기본값은 `false` 입니다.
ShowFormulas      | `*bool`    | 이 시트에 수식이 표시되어야 하는지 여부를 나타내는 기본값은 `false` 입니다.
ShowGridLines     | `*bool`    | 이 시트에 격자선을 표시할지 여부를 나타내는 기본값은 `true` 입니다.
ShowRowColHeaders | `*bool`    | 시트에 행 및 열 머리글이 표시되어야 하는지 여부를 나타내는 기본값은 `true` 입니다.
ShowRuler         | `*bool`    | 이 시트에 눈금자가 표시되어야 함을 나타내면 기본값은 `true` 입니다.
ShowZeros         | `*bool`    | "값이 0인 셀에 0 을 표시" 할지 여부를 나타냅니다. 수식을 사용하여 비어 있는 다른 셀을 참조할 때 플래그가 `true` 일 때 참조된 값은 `0` 이 되고 기본값은 `true` 가 됩니다.
TopLeftCell       | `*string`  | 왼쪽 위에 보이는 셀의 위치를 지정합니다. 오른쪽 아래 창에서 왼쪽 위에 표시되는 셀의 위치 (왼쪽에서 오른쪽 모드인 경우).
View              | `*string`  | 시트가 표시되는 방식을 나타내며 기본적으로 빈 문자열, 사용 가능한 옵션을 사용합니다: `normal`, `pageBreakPreview` 및 `pageLayout`.
ZoomScale         | `*float64` | 백분율 값을 나타내는 현재 뷰의 창 확대/축소 배율을 지정합니다. 이 속성은 `10` 에서 `400` 사이의 값으로 제한됩니다. 수평 및 수직 배율을 함께 사용하면 기본값은 `100` 입니다.

## 워크 시트 뷰 속성 가져 오기 {#GetSheetView}

```go
func (f *File) GetSheetView(sheet string, viewIndex int) (ViewOptions, error)
```

GetSheetView 는 시트 뷰 속성의 값을 가져옵니다. `viewIndex` 는 음수 일 수 있으며 그렇다면 뒤로 계산됩니다 (`-1` 은 마지막 뷰입니다).

## 워크 시트 페이지 레이아웃 설정 {#SetPageLayout}

```go
func (f *File) SetPageLayout(sheet string, opts *PageLayoutOptions) error
```

지정 된 워크시트 이름 및 페이지 레이아웃 매개 변수를 기반으로 워크시트의 페이지 레이아웃 속성을 설정 합니다. 현재 설정에 대해 지원 되는 페이지 레이아웃 속성:

`Size` 방법을 사용 하 여 페이지 용지의 크기를 설정 합니다, 기본 페이지 레이아웃 크기는 "Letter 용지  (8.5 인치 x 11 인치)" 입니다. 다음 표는 excel에서 페이지 레이아웃 크기와 인덱스 `Size` 매개 변수를 비교한 것입니다:

색인 | 용지 크기
---|---
1   | Letter 용지  (8.5 인치 x 11 인치)
2   | Letter 작은 용지  (8.5 인치 x 11 인치)
3   | Tabloid 용지 (11 인치 x 17 인치)
4   | Ledger 용지 (17 인치 x 11 인치)
5   | Legal 용지  (8.5 인치 x 14 인치)
6   | Statement 용지  (5.5 인치 x 8.5 인치)
7   | Executive 용지  (7.25 인치 x 10.5 인치)
8   | A3 용지 (297 mm x 420 mm)
9   | A4 용지 (210 mm x 297 mm)
10  | A4 작은 용지 (210 mm x 297 mm)
11  | A5 용지 (148 mm x 210 mm)
12  | B4 용지 (250 mm x 353 mm)
13  | B5 용지 (176 mm x 250 mm)
14  | Folio 용지 (8.5 인치 x 13 인치)
15  | Quarto 용지 (215 mm x 275 mm)
16  | 표준 용지 (10 인치 x 14 인치)
17  | 표준 용지 (11 인치 x 17 인치)
18  | 편지지 (8.5 인치 x 11인치)
19  | #9 봉투 (3.875 인치 x 8.875 인치)
20  | #10 봉투 (4.125 인치 x 9.5 인치)
21  | #11 봉투 (4.5 인치 x 10.375 인치)
22  | #12 봉투 (4.75 인치 x 11 인치)
23  | #14 봉투 (5 인치 x  11.5 인치)
24  | C 용지 (17 인치 x 22 인치)
25  | D 용지 (22 인치 x 34 인치)
26  | E 용지 ( 34 인치  x 44 인치)
27  | DL 봉투 (110 mm x 220 mm)
28  | C5 봉투 (162 mm x 229 mm)
29  | C3 봉투 (324 mm x 458 mm)
30  | C4 봉투 (229 mm x 324 mm)
31  | C6 봉투 (114 mm x 162 mm)
32  | C65 봉투 (114 mm x 229 mm)
33  | B4 봉투 (250 mm x 353 mm)
34  | B5 봉투 (176 mm x 250 mm)
35  | B6 봉투 (176 mm x 125 mm)
36  | 이탈리아 봉투 (110 mm x 230 mm)
37  | 군주 봉투  (3.875 인치 x 7.5 인치)
38  | 6 3/4 봉투  (3.625 인치 x 6.5 인치)
39  | 미국 표준 Fanfold (14.875 인치 x 11 인치)
40  | 독일 표준 Fanfold (8.5 인치 x 12 인치)
41  | 독일 Legal Fanfold (8.5 인치 x 13 인치)
42  | ISO B4 (250 mm x 353 mm)
43  | 일본 엽서 (100 mm x 148 mm)
44  | 표준 용지 (9 인치 x 11 인치)
45  | 표준 용지 (10 인치 x 11 인치)
46  | 표준 용지 (15 인치 x 11 인치)
47  | 초대 봉투 (220 mm x 220 mm)
50  | Letter 대형 용지 (9.275 인치 x 12 인치)
51  | Legal 대형 용지 (9.275 인치 x 15 인치)
52  | Tabloid 대형 용지 ( 11.69 인치 x 18 인치)
53  | A4 대형 용지 (236 mm x 322 mm)
54  | Letter 가로 용지 (8.275 인치 x 11 인치)
55  | A4 가로 용지 (210 mm x 297 mm)
56  | Letter 큰 가로 용지 (9.275 인치 x 12 인치)
57  | SuperA/SuperA/A4 용지 (227 mm x 356 mm)
58  | SuperB/SuperB/A3 용지 (305 mm x 487 mm)
59  | Letter 플러스 용지  (8.5 인치 x 12.69 인치)
60  | A4 플러스 용지 (210 mm x 330 mm)
61  | A5 가로 용지 (148 mm x 210 mm)
62  | JIS B5 가로 용지 (182 mm x 257 mm)
63  | A3 대형 용지 (322 mm x 445 mm)
64  | A5 대형 용지 (174 mm x 235 mm)
65  | ISO B5 대형 용지 (201 mm x 276 mm)
66  | A2 용지 (420 mm x 594 mm)
67  | A3 가로 용지 (297 mm x 420 mm)
68  | A3 큰 가로 용지 (322 mm x 445 mm)
69  | 일본 이중 엽서 (200 mm x 148 mm)
70  | A6 용지 (105 mm x 148 mm)
71  | 일본 Kaku #2 봉투
72  | 일본 Kaku #3 봉투
73  | 일본 Chou #3 봉투
74  | 일본 Chou #4 봉투
75  | Letter 회전 용지 (11 인치 x  8.5 인치)
76  | A3 회전 용지 (420 mm x 297 mm)
77  | A4 회전 용지 (297 mm x 210 mm)
78  | A5 회전 용지 (210 mm x 148 mm)
79  | JIS B4 회전 용지 (364 mm x 257 mm)
80  | JIS B5 회전 용지 (257 mm x 182 mm)
81  | 일본어 회전 용지 (148 mm x 100 mm)
82  | 일본 회전 이중 엽서 (148 mm x 200 mm)
83  | A6 회전 용지 (148 mm x 105 mm)
84  | 일본 회전 Kaku #2 봉투
85  | 일본 회전 Kaku #3 봉투
86  | 일본어 회전 Chou #3 봉투
87  | 일본 회전 Chou #4 봉투
88  | JIS B6 용지 (128 mm x 182 mm)
89  | JIS B6 회전 용지 (182 mm x 128 mm)
90  | 표준 용지 (12 인치 x 11 인치)
91  | 일본 You #4 봉투
92  | 일본 You #4 회전 봉투
93  | 16K 용지 (146 mm x 215 mm)
94  | 32K 용지 (97 mm x 151 mm)
95  | 32K 큰 용지 (97 mm x 151 mm)
96  | #1 봉투 (102 mm x 165 mm)
97  | #2 봉투 (102 mm x 176 mm)
98  | #3 봉투 (125 mm x 176 mm)
99  | #4 봉투 (110 mm x 208 mm)
100 | #5 봉투 (110 mm x 220 mm)
101 | #6 봉투 (120 mm x 230 mm)
102 | #7 봉투 (160 mm x 230 mm)
103 | #8 봉투 (120 mm x 309 mm)
104 | #9 봉투 (229 mm x 324 mm)
105 | #10 봉투 (324 mm x 458 mm)
106 | 16K 회전 용지 (146 mm x 215 mm)
107 | 32K 회전 용지 (97 mm x 151 mm)
108 | 32K 큰 회전 용지 (97 mm x 151 mm)
109 | #1 회전 봉투 (165 mm x 102 mm)
110 | #2 회전 봉투 (176 mm x 102 mm)
111 | #3 회전 봉투 (176 mm x 125 mm)
112 | #4 회전 봉투 (208 mm x 110 mm)
113 | 봉투 #5 회전 봉투 (220 mm x 110 mm)
114 | #6 회전 봉투 (230 mm x 120 mm)
115 | #7 회전 봉투 (230 mm x 160 mm)
116 | #8 회전 봉투 (309 mm x 120 mm)
117 | #9 회전 봉투 (324 mm x 229 mm)
118 | #10 회전 봉투 (458 mm x 324 mm)

`Orientation` 은 워크시트 방향을 지정했으며 기본 방향은 `portrait` 입니다. 이 필드에 사용할 수 있는 값은 `portrait` 와 `landscape` 입니다.

`FirstPageNumber` 는 첫 번째 인쇄된 페이지 번호를 지정했습니다. 값을 지정하지 않으면 "자동" 으로 간주됩니다.

`AdjustTo` 는 인쇄 배율을 지정했습니다. 이 속성은 10(10%) 에서 400(400%) 사이의 값으로 제한됩니다. 이 설정은 `FitToWidth` 및/또는 `FitToHeight` 를 사용 중일 때 재정의됩니다.

`FitToHeight` 는 맞출 세로 페이지 수를 지정했습니다.

`FitToWidth` 는 맞출 가로 페이지의 수를 지정했습니다.

`BlackAndWhite` 는 흑백으로 인쇄를 지정했습니다.

`PageOrder` 는 여러 페이지의 순서를 지정합니다. 허용되는 값: `overThenDown` 및 `downThenOver`.

예를 들어 `Sheet1` 이라는 시트 페이지 레이아웃을 단색 인쇄로 설정하고, 시작 페이지 번호를 `2` 로 설정하고, 가로로, A4(작은) 210× 297mm 용지 사용, 2 세로 페이지에 맞게 조정하고 2 개의 가로 페이지를 맞출 수 있습니다:

```go
f := excelize.NewFile()
var (
    size                 = 10
    orientation          = "landscape"
    firstPageNumber uint = 2
    adjustTo        uint = 100
    fitToHeight          = 2
    fitToWidth           = 2
    blackAndWhite        = true
)
if err := f.SetPageLayout("Sheet1", &excelize.PageLayoutOptions{
    Size:            &size,
    Orientation:     &orientation,
    FirstPageNumber: &firstPageNumber,
    AdjustTo:        &adjustTo,
    FitToHeight:     &fitToHeight,
    FitToWidth:      &fitToWidth,
    BlackAndWhite:   &blackAndWhite,
}); err != nil {
    fmt.Println(err)
}
```

## 워크 시트 페이지 레이아웃 가져 오기 {#GetPageLayout}

```go
func (f *File) GetPageLayout(sheet string) (PageLayoutOptions, error)
```

GetPageLayout 은 워크시트 페이지 레이아웃을 가져오는 함수를 제공합니다.

## 워크 시트 페이지 여백 설정 {#SetPageMargins}

```go
func (f *File) SetPageMargins(sheet string, opts *PageLayoutMarginsOptions) error
```

SetPageMargins 는 워크 시트 페이지 여백을 설정하는 기능을 제공합니다. 사용 가능한 옵션:

옵션|유형|설명설명
---|---|---
Bottom       | `*float64` | 아래쪽
Footer       | `*float64` | 바닥글
Header       | `*float64` | 머리글
Left         | `*float64` | 왼쪽
Right        | `*float64` | 오른쪽
Top          | `*float64` | 위쪽
Horizontally | `*bool`    | 페이지 중심: 가로로
Vertically   | `*bool`    | 페이지 중앙: 세로

## 워크 시트 페이지 여백 가져 오기 {#GetPageMargins}

```go
func (f *File) GetPageMargins(sheet string) (PageLayoutMarginsOptions, error)
```

GetPageMargins 는 워크 시트 페이지 여백을 얻는 기능을 제공합니다.

## 통합 문서 속성 설정 {#SetWorkbookProps}

```go
func (f *File) SetWorkbookProps(opts *WorkbookPropsOptions) error
```

SetWorkbookProps 는 통합 문서 속성을 설정하는 기능을 제공합니다. 사용 가능한 옵션:

옵션|유형|설명설명
---|---|---
Date1904      | `*bool`   | 통합 문서의 직렬 날짜-시간을 날짜로 변환할 때 1900 또는 1904 날짜 시스템을 사용할지 여부를 나타냅니다.
FilterPrivacy | `*bool`   | 응용 프로그램이 통합 문서에 PII(개인 식별 정보)를 검사했는지 여부를 나타내는 부울 값을 지정합니다. 이 플래그가 설정된 경우 응용 프로그램은 사용자가 문서에 PII를 삽입하는 작업을 수행할 때마다 사용자에게 경고합니다.
CodeName      | `*string` | 이 통합 문서를 만든 응용 프로그램의 코드 이름을 지정합니다. 이 특성을 사용하여 응용 프로그램의 증분 릴리스에서 파일 콘텐츠를 추적할 수 있습니다.

## 통합 문서 속성 가져오기 {#GetWorkbookProps}

```go
func (f *File) GetWorkbookProps() (WorkbookPropsOptions, error)
```

GetWorkbookProps 는 통합 문서 속성을 가져오는 기능을 제공합니다.

## 머리글 및 바닥 글 설정 {#SetHeaderFooter}

```go
func (f *File) SetHeaderFooter(sheet string, opts *HeaderFooterOptions) error
```

SetHeaderFooter 는 주어진 워크 시트 이름과 제어 문자로 머리글과 바닥 글을 설정하는 기능을 제공합니다.

머리글과 바닥 글은 다음 설정 필드를 사용하여 지정됩니다.

필드           | 설명
---|---
AlignWithMargins | 머리글 바닥글 여백을 페이지 여백에 맞추기
DifferentFirst   | 다른 첫 페이지 머리글 및 바닥글 표시기
DifferentOddEven | 다른 홀수 및 짝수 페이지 머리글 및 바닥글 표시기
ScaleWithDoc     | 문서 크기 조정으로 머리글 및 바닥글 크기 조정
OddFooter        | 홀수 페이지 바닥글 또는 `DifferentOddEven` 이 `false` 인 경우 기본 페이지 바닥글
OddHeader        | 홀수 헤더 또는 `DifferentOddEven` 이 `false` 인 경우 기본 페이지 헤더
EvenFooter       | 짝수 페이지 바닥글
EvenHeader       | 짝수 페이지 머리글
FirstFooter      | 첫 페이지 바닥글
FirstHeader      | 첫 페이지 머리글

다음 형식 코드는 6 개의 문자열 형식 필드에서 사용할 수 있습니다: `OddHeader`, `OddFooter`, `EvenHeader`, `EvenFooter`, `FirstFooter`, `FirstHeader`

<table>
    <thead>
        <tr>
            <th>서식 코드</th>
            <th>설명</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>&amp;&amp;</code></td>
            <td>캐릭터 &quot;&amp;&quot;</td>
        </tr>
        <tr>
            <td><code>&amp;font-size</code></td>
            <td>텍스트 글꼴의 크기입니다. 여기서 font-size 는 소수점 글꼴 크기 (포인트 단위) 입니다</td>
        </tr>
        <tr>
            <td><code>&amp;&quot;font name,font type&quot;</code></td>
            <td>텍스트 글꼴 이름 문자열, 글꼴 이름 및 텍스트 글꼴 유형 문자열, 글꼴 유형</td>
        </tr>
        <tr>
            <td><code>&amp;&quot;-,Regular&quot;</code></td>
            <td>일반 텍스트 형식입니다. 굵게 및 기울임꼴 모드를 끕니다</td>
        </tr>
        <tr>
            <td><code>&amp;A</code></td>
            <td>현재 워크시트의 탭 이름</td>
        </tr>
        <tr>
            <td><code>&amp;B</code> or <code>&amp;&quot;-,Bold&quot;</code></td>
            <td>굵은 텍스트 형식, 끄기에서 켜기 또는 그 반대로. 기본 모드는 꺼져 있습니다</td>
        </tr>
        <tr>
            <td><code>&amp;D</code></td>
            <td>현재 날짜</td>
        </tr>
        <tr>
            <td><code>&amp;C</code></td>
            <td>중앙 섹션</td>
        </tr>
        <tr>
            <td><code>&amp;E</code></td>
            <td>이중 밑줄 텍스트 형식</td>
        </tr>
        <tr>
            <td><code>&amp;F</code></td>
            <td>현재 통합 문서의 파일 이름</td>
        </tr>
        <tr>
            <td><code>&amp;G</code></td>
            <td>배경으로 개체 그리기 (AddHeaderFooterImage 를 사용하세요)</td>
        </tr>
        <tr>
            <td><code>&amp;H</code></td>
            <td>그림자 텍스트 형식</td>
        </tr>
        <tr>
            <td><code>&amp;I</code> or <code>&amp;&quot;-,Italic&quot;</code></td>
            <td>기울임꼴 텍스트 형식</td>
        </tr>
        <tr>
            <td><code>&amp;K</code></td>
            <td>텍스트 글꼴 색상<br>RGB 색상은 RRGGBB 로 지정됩니다<br>테마 색상은 TTSNNN 으로 지정되며, 여기서 TT 는 테마 색상 ID 이고, S 는 색조/음영 값의 &quot;+&quot; 또는 &quot;-&quot; 이며, NNN 은 색조/음영 값입니다</td>
        </tr>
        <tr>
            <td><code>&amp;L</code></td>
            <td>왼쪽 섹션</td>
        </tr>
        <tr>
            <td><code>&amp;N</code></td>
            <td>총 페이지 수</td>
        </tr>
        <tr>
            <td><code>&amp;O</code></td>
            <td>개요 텍스트 형식</td>
        </tr>
        <tr>
            <td><code>&amp;P[[+\|-]n]</code></td>
            <td>선택적 접미사가 없으면 현재 페이지 번호 (10 진수)</td>
        </tr>
        <tr>
            <td><code>&amp;R</code></td>
            <td>오른쪽 섹션</td>
        </tr>
        <tr>
            <td><code>&amp;S</code></td>
            <td>취소선 텍스트 형식</td>
        </tr>
        <tr>
            <td><code>&amp;T</code></td>
            <td>현재 시간</td>
        </tr>
        <tr>
            <td><code>&amp;U</code></td>
            <td>단일 밑줄 텍스트 형식입니다. 이중 밑줄 모드가 켜져 있는 경우 섹션 지정자가 다음에 나타나면 이중 밑줄 모드가 해제됩니다. 그렇지 않으면 단일 밑줄 모드를 끄기에서 켜기 또는 그 반대로 전환합니다. 기본 모드는 꺼져 있습니다</td>
        </tr>
        <tr>
            <td><code>&amp;X</code></td>
            <td>위 첨자 텍스트 형식</td>
        </tr>
        <tr>
            <td><code>&amp;Y</code></td>
            <td>첨자 텍스트 형식</td>
        </tr>
        <tr>
            <td><code>&amp;Z</code></td>
            <td>현재 통합 문서의 파일 경로</td>
        </tr>
    </tbody>
</table>

예:

```go
err := f.SetHeaderFooter("Sheet1", &excelize.HeaderFooterOptions{
    DifferentFirst:   true,
    DifferentOddEven: true,
    OddHeader:        "&R&P",
    OddFooter:        "&C&F",
    EvenHeader:       "&L&P",
    EvenFooter:       "&L&D&R&T",
    FirstHeader:      `&CCenter &"-,Bold"Bold&"-,Regular"HeaderU+000A&D`,
})
```

이 예는 다음과 같습니다:

- 첫 페이지에는 고유 한 머리말과 꼬리말이 있습니다.
- 홀수 페이지와 짝수 페이지는 서로 다른 머리글과 바닥 글을 가지고 있습니다.
- 홀수 페이지 헤더의 오른쪽 섹션에있는 현재 페이지 번호
홀수 페이지 바닥 글의 가운데 섹션에있는 현재 통합 문서의 파일 이름
- 짝수 페이지 헤더의 왼쪽 섹션에있는 현재 페이지 번호
- 왼쪽 섹션의 현재 날짜와 짝수 페이지 바닥 글의 오른쪽 섹션의 현재 시간
- 첫 번째 페이지의 가운데 섹션의 첫 번째 줄에있는 텍스트 "Center Bold Header"과 같은 페이지의 가운데 섹션의 두 번째 줄에있는 날짜
- 첫 페이지에 꼬리말 없음

## 헤더와 푸터 이미지 추가 {#AddHeaderFooterImage}

```go
func (f *File) AddHeaderFooterImage(sheet string, opts *HeaderFooterImageOptions) error
```

AddHeaderFooterImage 는 `&G` 를 통해 헤더 및 푸터 정의에서 참조할 수 있는 그래픽을 설정하는 메커니즘을 제공하며, 지원되는 이미지 유형은 EMF, EMZ, GIF, JPEG, JPG, PNG, SVG, TIF, TIFF, WMF 및 WMZ 입니다.

## 이름 설정 {#SetDefinedName}

```go
func (f *File) SetDefinedName(definedName *DefinedName) error
```

지정된 이름과 범위를 기반으로 이름을 설정합니다. 기본 범위는 통합 문서입니다. 예:

```go
err := f.SetDefinedName(&excelize.DefinedName{
    Name:     "Amount",
    RefersTo: "Sheet1!$A$2:$D$5",
    Comment:  "defined name comment",
    Scope:    "Sheet2",
})
```

워크 시트의 인쇄 영역 및 인쇄 제목 설정:

<p align="center"><img width="628" src="./images/page_setup_01.png" alt="워크 시트의 인쇄 영역 및 인쇄 제목 설정"></p>

```go
if err := f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Area",
    RefersTo: "Sheet1!$A$1:$Z$100",
    Scope:    "Sheet1",
}); err != nil {
    fmt.Println(err)
}
if err := f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Titles",
    RefersTo: "Sheet1!$A:$A,Sheet1!$1:$1",
    Scope:    "Sheet1",
}); err != nil {
    fmt.Println(err)
}
```

`RefersTo` 속성을 쉼표 없이 열 범위 하나만 채우면 "왼쪽에서 반복할 열" 로만 작동합니다. 예를 들어:

```go
if err := f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Titles",
    RefersTo: "Sheet1!$A:$A",
    Scope:    "Sheet1",
}); err != nil {
    fmt.Println(err)
}
```

`RefersTo` 속성을 쉼표 없이 행 범위 하나만 채우면 "위에서 반복할 행" 으로만 작동합니다. 예를 들어:

```go
if err := f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Titles",
    RefersTo: "Sheet1!$1:$1",
    Scope:    "Sheet1",
}); err != nil {
    fmt.Println(err)
}
```

## 이름 가져 오기 {#GetDefinedName}

```go
func (f *File) GetDefinedName() []DefinedName
```

범위에있는 통합 문서 및 워크 시트의 이름 목록을 얻습니다.

## 정의 된 이름 삭제 {#DeleteDefinedName}

```go
func (f *File) DeleteDefinedName(definedName *DefinedName) error
```

DeleteDefinedName 은 통합 문서 또는 워크 시트의 정의 된 이름을 삭제하는 기능을 제공합니다. 범위를 지정하지 않으면 기본 범위는 통합 문서입니다. 예를 들면 다음과 같습니다:

```go
err := f.DeleteDefinedName(&excelize.DefinedName{
    Name:     "Amount",
    Scope:    "Sheet2",
})
```

## 애플리케이션 속성 설정 {#SetAppProps}

```go
func (f *File) SetAppProps(appProperties *AppProperties) error
```

SetAppProps 는 문서 애플리케이션 속성을 설정하는 기능을 제공합니다. 설정할 수 있는 속성은 다음과 같습니다.

속성            | 기술
---|---
Application       | 이 문서를 만든 응용 프로그램의 이름입니다.
ScaleCrop         | 문서 축소판의 표시 모드를 나타냅니다. 이 요소를 `true` 로 설정하면 문서 축소판을 디스플레이에 맞게 조정할 수 있습니다. 이 요소를 `false` 로 설정하면 디스플레이에 맞는 섹션만 표시하도록 문서 축소판을 잘라낼 수 있습니다.
DocSecurity       | 숫자 값으로 나타낸 문서의 보안 수준입니다. 문서 보안은 다음과 같이 정의됩니다.<br>1 - 문서가 비밀번호로 보호되어 있습니다<br>2 - 문서를 읽기 전용으로 여는 것이 좋습니다<br>3 - 문서가 읽기 전용으로 열리도록 강제 실행됩니다<br>4 - 문서가 주석을 위해 잠겨 있습니다
Company           | 문서와 연결된 회사의 이름입니다.
LinksUpToDate     | 문서의 하이퍼링크가 최신 상태인지 여부를 나타냅니다. 하이퍼링크가 업데이트되었음을 나타내려면 이 요소를 `true` 로 설정합니다. 하이퍼링크가 오래되었음을 나타내려면 이 요소를 `false` 로 설정합니다.
HyperlinksChanged | 이 부분에 있는 하나 이상의 하이퍼링크가 생산자에 의해 이 부분에서만 독점적으로 업데이트되었음을 지정합니다. 이 문서를 여는 다음 제작자는 이 부분에 지정된 새 하이퍼링크로 하이퍼링크 관계를 업데이트해야 합니다.
AppVersion        | 이 문서를 생성한 애플리케이션의 버전을 지정합니다. 이 요소의 내용은 XX.YYYY 형식이어야 하며 여기서 X 와 Y 는 숫자 값을 나타내거나 문서는 부적합한 것으로 간주됩니다.

예:

```go
err := f.SetAppProps(&excelize.AppProperties{
    Application:       "Microsoft Excel",
    ScaleCrop:         true,
    DocSecurity:       3,
    Company:           "Company Name",
    LinksUpToDate:     true,
    HyperlinksChanged: true,
    AppVersion:        "16.0000",
})
```

## 애플리케이션 속성 가져오기 {#GetAppProps}

```go
func (f *File) GetAppProps() (*AppProperties, error)
```

GetAppProps 는 문서 응용 프로그램 속성을 가져오는 기능을 제공합니다.

## 문서 속성 설정 {#SetDocProps}

```go
func (f *File) SetDocProps(docProperties *DocProperties) error
```

통합 문서의 핵심 속성을 설정합니다. 설정할 수있는 속성은 다음과 같습니다:

속성            | 기술
---|---
Category       | 이 패키지의 내용을 분류합니다.
ContentStatus  | 내용의 상태. 예: "Draft", "Reviewed" 및 "Final"
Created        | 리소스 콘텐츠의 생성 시간입니다.
Creator        | 자원의 내용을 만드는 일을 주로 담당하는 주체.
Description    | 자원의 내용에 대한 설명.
Identifier     | 지정된 컨텍스트 내의 리소스에 대한 모호하지 않은 참조입니다.
Keywords       | 검색 및 색인 생성을 지원하는 구분 된 키워드 집합입니다. 일반적으로 속성의 다른 곳에서는 사용할 수없는 용어 목록입니다.
Language       | 자원의 지적 내용의 언어.
LastModifiedBy | 마지막 수정을 수행 한 사용자입니다. 식별은 환경에 따라 다릅니다.
Modified       | 리소스 콘텐츠의 수정된 시간입니다.
Revision       | 리소스 콘텐츠의 개정 번호입니다.
Subject        | 자원 내용의 주제.
Title          | 리소스에 지정된 이름입니다.
Version        | 버전 번호. 이 값은 사용자 또는 응용 프로그램에 의해 설정됩니다.

예:

```go
err := f.SetDocProps(&excelize.DocProperties{
    Category:       "category",
    ContentStatus:  "Draft",
    Created:        "2019-06-04T22:00:10Z",
    Creator:        "Go Excelize",
    Description:    "This file created by Go Excelize",
    Identifier:     "xlsx",
    Keywords:       "Spreadsheet",
    LastModifiedBy: "Go Author",
    Modified:       "2019-06-04T22:00:10Z",
    Revision:       "0",
    Subject:        "Test Subject",
    Title:          "Test Title",
    Language:       "en-US",
    Version:        "1.0.0",
})
```

## 문서 속성 가져오기 {#GetDocProps}

```go
func (f *File) GetDocProps() (*DocProperties, error)
```

통합 문서의 핵심 속성을 가져옵니다.

## 계산 속성 설정 {#SetCalcProps}

```go
func (f *File) SetCalcProps(opts *CalcPropsOptions) error
```

SetCalcProps는 계산 속성을 설정하는 함수를 제공합니다.

`CalcMode` 속성의 선택 값은 `manual`, `auto` 또는 `autoNoTable` 입니다.

`RefMode` 속성의 선택 값은 `A1` 또는 `R1C1` 입니다.

## 계산 속성 가져오기 {#GetCalcProps}

```go
func (f *File) GetCalcProps() (CalcPropsOptions, error)
```

GetCalcProps 는 계산 속성을 가져오는 함수를 제공합니다.

## 통합 문서 보호 {#ProtectWorkbook}

```go
func (f *File) ProtectWorkbook(opts *WorkbookProtectionOptions) error
```

ProtectWorkbook 은 다른 사용자가 실수로 또는 의도적으로 통합 문서의 데이터를 변경, 이동 또는 삭제하는 것을 방지하는 기능을 제공합니다. 선택 필드 `AlgorithmName` 은 해시 알고리즘을 지정했으며 현재 XOR, MD4, MD5, SHA-1, SHA2-56, SHA-384 및 SHA-512 를 지원하며 해시 알고리즘이 지정되지 않은 경우 XOR 알고리즘을 기본값으로 사용합니다. 예를 들어 보호 설정으로 통합 문서를 보호합니다:

```go
err := f.ProtectWorkbook(&excelize.WorkbookProtectionOptions{
    Password:      "password",
    LockStructure: true,
})
```

WorkbookProtectionOptions 는 통합 문서 보호 설정을 직접 매핑합니다.

```go
type WorkbookProtectionOptions struct {
    AlgorithmName string
    Password      string
    LockStructure bool
    LockWindows   bool
}
```

## 통합 문서 보호 해제 {#UnprotectWorkbook}

```go
func (f *File) UnprotectWorkbook(password ...string) error
```

UnprotectWorkbook 은 통합 문서에 대한 보호를 제거하는 기능을 제공하며 암호 확인을 통해 통합 문서 보호를 제거하기 위해 선택적 암호 매개 변수를 지정합니다.
