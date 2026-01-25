# 차트

## 차트 추가 {#AddChart}

```go
func (f *File) AddChart(sheet, cell string, chart *ChartOptions, combo ...*ChartOptions) error
```

AddChart 는 지정된 차트 형식 집합 (예: 오프셋, 축척, 종횡비 설정 및 인쇄 설정) 및 속성 집합을 사용하여 시트에 차트를 추가하는 방법을 제공합니다.

다음은 excelize 에서 지원하는 차트의 `Type` 을 보여 주며:

ID|열거|차트
---|---|---
0  | Area                        | 2D 영역 차트
1  | AreaStacked                 | 2D 스택 영역 차트
2  | AreaPercentStacked          | 2D 100% 스택 영역 차트
3  | Area3D                      | 3D 영역 차트
4  | Area3DStacked               | 3D 스택 영역 차트
5  | Area3DPercentStacked        | 3D 100% 누적 영역 차트
6  | Bar                         | 2D 클러스터 막대 차트
7  | BarStacked                  | 2D 스택 막대 차트
8  | BarPercentStacked           | 2D 100% 스택 막대 차트
9  | Bar3DClustered              | 3D 클러스터 막대 차트
10 | Bar3DStacked                | 3D 누적 막 대형 차트
11 | Bar3DPercentStacked         | 3D 100% 스택 막대 차트
12 | Bar3DConeClustered          | 3D 원뿔 클러스터된 막대 차트
13 | Bar3DConeStacked            | 3D 원뿔 누적 막대 차트
14 | Bar3DConePercentStacked     | 3D 100% 콘 막대 차트
15 | Bar3DPyramidClustered       | 3D 피라미드 클러스터 막대 차트
16 | Bar3DPyramidStacked         | 3D 피라미드 누적 막대 차트
17 | Bar3DPyramidPercentStacked  | 3D 100% 피라미드 누적 막대 차트
18 | Bar3DCylinderClustered      | 3D 실린더 클러스터된 막대 차트
19 | Bar3DCylinderStacked        | 3D 실린더 스택 막대 차트
20 | Bar3DCylinderPercentStacked | 3D 100% 실린더 적층 막대 차트
21 | Col                         | 2D 클러스터형 세로 막 대형 차트
22 | ColStacked                  | 2D 누적 세로 막 대형 차트
23 | ColPercentStacked           | 2D 100% 스택 세로 막 대형 차트
24 | Col3DClustered              | 3D 클러스터 된 세로 막 대형 차트
25 | Col3D                       | 3D 세로 막 대형 차트
26 | Col3DStacked                | 3D 누적 세로 막 대형 차트
27 | Col3DPercentStacked         | 3D 100% 누적 세로 막 대형 차트
28 | Col3DCone                   | 3D 원뿔 열차트
29 | Col3DConeClustered          | 3D 원뿔 클러스터된 열 차트
30 | Col3DConeStacked            | 3D 원뿔 누적 열 차트
31 | Col3DConePercentStacked     | 3D 100% 콘 스택 열 차트
32 | Col3DPyramid                | 3D 피라미드 열차트
33 | Col3DPyramidClustered       | 3D 피라미드 클러스터된 열 차트
34 | Col3DPyramidStacked         | 3D 피라미드 누적 열 차트
35 | Col3DPyramidPercentStacked  | 3D 100% 피라미드 누적 열 차트
36 | Col3DCylinder               | 3D 원통 열차트
37 | Col3DCylinderClustered      | 3D 실린더 클러스터된 열 차트
38 | Col3DCylinderStacked        | 3D 실린더 스택 컬럼 차트
39 | Col3DCylinderPercentStacked | 3D 100% 실린더 스택 컬럼 차트
40 | Doughnut                    | 도넛 차트
41 | Line                        | 꺾은 선형 차트
42 | Line3D                      | 3D 꺾은 선형 차트
43 | Pie                         | 원형 차트
44 | Pie3D                       | 3D 원형 차트
45 | PieOfPie                    | 이중 원형 차트
46 | BarOfPie                    | 원형 차트 막대
47 | Radar                       | 레이더 차트
48 | Scatter                     | 분산 형 차트
49 | Surface3D                   | 3D 표면 차트
50 | WireframeSurface3D          | 3D 와이어프레임 표면 차트
51 | Contour                     | 등고선 차트
52 | WireframeContour            | 와이어프레임 윤곽 차트
53 | Bubble                      | 버블 차트
54 | Bubble3D                    | 3D 버블 차트
55 | StockHighLowClose           | 고가-저가-종가 주식 차트
56 | StockOpenHighLowClose       | 시가-고가-저가-종가 주식 차트

Office Excel 차트 데이터 영역 `Series` 에서 데이터를 그릴 정보 집합, 범례 항목 (계열) 및 가로 (범주) 축 레이블을 지정합니다.

설정할 수 있는 `Series` 옵션은 다음과 같습니다:

매개 변수|설명
---|---
Name              | 범례 항목 (계열) 은 차트 범례 및 수식 표시줄에 표시됩니다. `Name` 매개 변수는 선택 사항입니다. 이 값을 지정하지 않으면 기본값은 `Series 1 .. n`. 수식 표현에 대한 `Name` 지원(예: `Sheet1!$A$1`).
Categories        | 가로(범주) 축 레이블입니다. `Categories` 매개변수는 대부분의 차트 유형에서 선택사항이며, 기본값은 `1..n` 형식의 연속 시퀀스입니다.
Values            | `Series` 에서 가장 중요한 매개 변수인 차트 데이터 영역도 차트를 만들 때 필요한 유일한 매개 변수입니다. 이 옵션은 차트를 차트가 표시하는 워크시트 데이터에 연결합니다.
Fill              | 데이터 시리즈 채우기 형식을 설정합니다.
Legend            | 데이터 시리즈의 범례 텍스트 글꼴을 설정합니다. `Legend` 속성은 선택 사항입니다.
Line              | 선 차트의 선 형식을 설정합니다. `Line` 속성은 선택 사항이며 제공되지 않으면 기본 스타일이됩니다. 설정할 수있는 옵션은 `Width` 입니다. `Width` 의 범위는 0.25pt-999pt 입니다. 너비 값이 범위를 벗어나면 선의 기본 너비는 2pt 입니다.
Marker            | 선형 차트 및 분산 형 차트의 마커를 설정합니다. 선택적 필드 `Size` 의 범위는 2-72 입니다 (기본값은 `5`). 선택적 필드 `Symbol` 의 열거 값은 다음과 같습니다 (기본값은 `auto`): `circle`, `dash`, `diamond`, `dot`, `none`, `picture`, `plus`, `square`, `star`, `triangle`, `x`, `auto`.
DataLabelPosition | 차트 시리즈 데이터 라벨의 위치를 설정합니다.
DataPoint         | 도넛형, 원형 또는 3D 원형 차트 시리즈의 개별 데이터 포인트 형식을 설정합니다. `DataPoint` 속성은 선택 사항입니다.

차트 범례의 속성을 설정합니다. 설정할 수 있는 옵션은 다음과 같습니다:

매개 변수|유형|설명
---|---|---
Position      | `string` | 차트 범례의 위치
ShowLegendKey | `bool`   | 데이터 레이블에 범례 항목 레이블을 표시할지 여부를 지정합니다
Font          | `Font`   | 차트 범례 텍스트의 글꼴 속성을 설정합니다. 설정할 수 있는 속성은 셀 서식에 사용되는 글꼴 개체와 동일합니다. 글꼴 모음, 크기, 색상, 굵게, 기울임꼴, 밑줄, 취소선 속성을 설정할 수 있습니다

차트 범례의 `Position` 을 설정합니다. 기본 범례 위치는 `right` 입니다. 다음은이 매개 변수의 선택적 값입니다:

매개 변수|설명
---|---
none      | 범례 비활성화
top       | 상단에
bottom    | 바닥에
left      | 왼쪽
right     | 오른쪽
top_right | 오른쪽 상단

범례 키를 설정하는 `ShowLegendKey`  매개 변수는 데이터 레이블에 표시됩니다. 기본값은 `false` 입니다.

차트 제목은 `Title` 개체의 `Name` 매개변수를 선택하여 설정되며 제목은 차트 위에 표시됩니다. 매개 변수 `Name` 은 아이콘 제목을 지정하지 않으면 `Sheet1!$A$1` 과 같은 수식 표현의 사용을 지원합니다.

`ShowBlanksAs` 매개변수는 "셀 숨기기 및 빈 셀" 설정을 제공합니다. 기본값은 `gap` 입니다. Excel 응용 프로그램에서 "빈 셀은" 로 표시됩니다: "space". 다음은 이 매개 변수에 대한 선택적 값입니다.

매개 변수|설명
---|---
gap  | 공간
span | 데이터 포인트를 직선으로 연결
zero | 0 값

`Legend` 속성을 사용하여 모든 데이터 시리즈의 차트 범례를 설정합니다. `Legend` 속성은 선택 사항입니다.

버블 차트 또는 3D 버블 차트의 모든 데이터 시리즈에 버블 크기를 'BubbleSizes' 속성으로 설정합니다. `BubbleSizes` 속성은 선택 사항입니다. 기본 너비는 `100` 이며 값은 0 보다 크고 300 보다 작거나 같아야 합니다.

`HoleSize` 속성으로 도넛 차트의 모든 데이터 계열에 있는 도넛 구멍 크기를 설정합니다. `HoleSize` 속성은 선택사항입니다. 기본 너비는 `75` 이며 값은 0 보다 크고 90 보다 작거나 같아야 합니다.

계열의 각 데이터 마커는 `VaryColors` 에 의해 다른 색상을 가지고 있음을 지정합니다. 기본 값은 `true` 입니다.

매개변수 `Format` 은 차트 오프셋, 배율, 종횡비 설정 및 인쇄 특성과 [`AddPicture`](image.md#AddPicture) 함수에 사용되는 매개 변수에 대한 설정을 제공합니다.

차트 플롯 영역의 위치를 플롯 영역별로 설정합니다. 설정할 수 있는 속성은 다음과 같습니다:

매개 변수|유형|기본값|설명
---|---|---|---
SecondPlotValues  | `int`            | `0`     | `PieOfPie` 및 `BarOfPie` 차트에 대한 두 번째 플롯의 값을 지정합니다.
ShowBubbleSize    | `bool`           | `false` | 거품 크기를 지정하여 데이터 레이블에 표시해야 합니다.
ShowCatName       | `bool`           | `true`  | 데이터 레이블에 범주 이름을 표시하도록 지정합니다. `ShowCatName` 속성은 선택 사항입니다.
ShowDataTable     | `bool`           | `false` | 차트 아래에 데이터 표를 추가하는 데 사용되며, 차트 유형에 따라 영역형, 막대형, 세로형 및 선형 계열 차트에만 사용할 수 있습니다.
ShowDataTableKeys | `bool`           | `false` | 데이터 테이블에 범례 키를 추가하는 데 사용되며, `ShowDataTable` 이 활성화된 경우에만 작동합니다. `ShowDataTableKeys` 속성은 선택 사항입니다.
ShowLeaderLines   | `bool`           | `false` | 데이터 레이블에 지시선을 표시할지 여부를 지정합니다. `ShowLeaderLines` 속성은 선택 사항입니다.
ShowPercent       | `bool`           | `false` | 백분율이 데이터 레이블에 표시되도록 지정합니다.
ShowSerName       | `bool`           | `false` | 계열 이름이 데이터 레이블에 표시되도록 지정합니다.
ShowVal           | `bool`           | `false` | 값이 데이터 레이블에 표시되도록 지정합니다.
Fill              | `Fill`           | N/A     | 차트의 채우기 색상을 설정합니다.
UpBars            | `ChartUpDownBar` | N/A     | 주식형 차트의 상향 막대 형식을 지정합니다. `UpBars` 속성은 선택 사항입니다.
DownBars          | `ChartUpDownBar` | N/A     | 주식형 차트의 하향 막대 형식을 지정합니다. `DownBars` 속성은 선택 사항입니다.
NumFmt            | `ChartNumFmt`    | N/A     | 소스에 연결된 경우 데이터 레이블에 대한 사용자 정의 숫자 형식 코드를 설정하도록 지정합니다. `NumFmt` 속성은 선택 사항입니다. 기본 형식 코드는 `General` 입니다.

기본 수평 및 세로 축 옵션을 `XAxis` 및 `YAxis` 으로 설정합니다.

설정할 수있는 `XAxis` 의 속성은 다음과 같습니다:

매개 변수|유형|기본값|설명
---|---|---|---
None           | `bool`          | `false` | 축 비활성화.
DropLines      | `bool`          | `false` | 2D 및 3D 영역 차트와 선 차트에 대한 드롭 라인을 지정합니다. 드롭 라인은 차트의 데이터 포인트를 가로축 (범주) 으로 연결하는 수직선입니다. 드롭 라인은 선 차트나 영역 차트에서 각 데이터 포인트의 정확한 범주 위치를 쉽게 확인할 수 있도록 하는 데 자주 사용됩니다. `DropLines` 속성은 선택 사항입니다.
HighLowLines   | `bool`          | `false` | 2D 및 3D 영역 차트와 선 차트에 대한 드롭 라인을 지정합니다. 드롭 라인은 차트의 데이터 포인트를 가로축 (범주) 으로 연결하는 수직선입니다. 드롭 라인은 선 차트나 영역 차트에서 각 데이터 포인트의 정확한 범주 위치를 쉽게 확인할 수 있도록 하는 데 자주 사용됩니다. `DropLines` 속성은 선택 사항입니다.
MajorGridLines | `bool`          | `false` | 주요 눈금 선을 지정합니다.
MinorGridLines | `bool`          | `false` | 작은 눈금 선을 지정합니다.
TickLabelSkip  | `int`           | `1`     | 그려진 레이블간에 건너 뛸 눈금 레이블 수를 지정합니다. `TickLabelSkip` 속성은 선택 사항입니다. 기본값은 auto 입니다.
ReverseOrder   | `bool`          | `false` | 역순 (차트 방향) 의 범주 또는 값을 지정합니다. `ReverseOrder` 속성은 선택 사항입니다.
Maximum        | `*float64`      | `0`     | 고정 최대값 0 이 자동임을 지정합니다. 최대 속성은 선택 사항입니다.
Minimum        | `*float64`      | `0`     | 고정 된 최소, 0 은 자동 지정 합니다. 최소 속성은 선택 사항입니다. 기본값은 자동입니다.
Alignment      | `Alignment`     | N/A     | 수평 및 수직 축의 정렬을 지정합니다. 설정할 수 있는 글꼴 속성은 다음과 같습니다. `TextRotation` 및 `Vertical`
Font           | `Font`          | N/A     | 가로축의 글꼴을 지정합니다.
NumFmt         | `ChartNumFmt`   | N/A     | 소스에 연결된 경우를 지정하고 축에 대한 사용자 지정 숫자 형식 코드를 설정합니다.
Title          | `[]RichTextRun` | N/A     | 기본 가로 축 제목 및 차트 크기 조정을 지정합니다.

설정할 수있는 `YAxis` 의 속성은 다음과 같습니다:

매개 변수|유형|기본값|설명
---|---|---|---
None           | `bool`          | `false` | 축 비활성화.
MajorGridLines | `bool`          | `false` | 주요 눈금 선을 지정합니다.
MinorGridLines | `bool`          | `false` | 작은 눈금 선을 지정합니다.
MajorUnit      | `float64`       | `0`     | 주요 눈금 사이의 거리를 지정합니다. 양의 부동 소수점 숫자를 포함해야합니다. `MajorUnit` 속성은 선택 사항입니다. 기본값은 auto 입니다.
ReverseOrder   | `bool`          | `false` | 역순 (차트 방향) 의 범주 또는 값을 지정합니다. `ReverseOrder` 속성은 선택 사항입니다.
Maximum        | `*float64`      | `0`     | 고정 최대값 0 이 자동임을 지정합니다. 최대 속성은 선택 사항입니다.
Minimum        | `*float64`      | `0`     | 고정 된 최소, 0 은 자동 지정 합니다. 최소 속성은 선택 사항입니다. 기본값은 자동입니다.
Alignment      | `Alignment`     | N/A     | 수평 및 수직 축의 정렬을 지정합니다. 설정할 수 있는 글꼴 속성은 다음과 같습니다. `TextRotation` 및 `Vertical`
Font           | `Font`          | N/A     | 세로축의 글꼴을 지정합니다.
LogBase        | `float64`       | N/A     | 세로축의 대수 눈금 밑수를 지정합니다.
NumFmt         | `ChartNumFmt`   | N/A     | 소스에 연결된 경우를 지정하고 축에 대한 사용자 지정 숫자 형식 코드를 설정합니다.
Title          | `[]RichTextRun` | N/A     | 기본 세로 축 제목 및 차트 크기 조정을 지정합니다.

-90 에서 90 까지 설정할 수 있는 `TextRotation` 값입니다.

설정할 수 있는 `Vertical` 값은 `horz`, `vert`, `vert270`, `wordArtVert`, `eaVert`, `mongolianVert` 및 `wordArtVertRtl`입니다.

차트 크기를 `Dimension` 속성으로 설정합니다. 차원 속성은 선택 사항입니다. 설정할 수 있는 속성은 다음과 같습니다:

매개 변수|유형|기본값|설명
---|---|---|---
Height | `uint` | 260 | 높이
Width  | `uint` | 480 | 너비

`combo` 매개 변수는 단일 차트에서 둘 이상의 차트 유형을 결합하는 차트 작성을 지정합니다. 예를 들어, `Sheet1!$E$1:$L$15` 데이터가 포함 된 군집 기둥 형 꺾은 선형 차트를 만듭니다:

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
    for idx, row := range [][]interface{}{
        {nil, "Apple", "Orange", "Pear"},
        {"Small", 2, 3, 3},
        {"Normal", 5, 2, 4},
        {"Large", 6, 7, 8},
    } {
        cell, err := excelize.CoordinatesToCellName(1, idx+1)
        if err != nil {
            fmt.Println(err)
            return
        }
        if err := f.SetSheetRow("Sheet1", cell, &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    enable, disable := true, false
    if err := f.AddChart("Sheet1", "E1", &excelize.Chart{
        Type: excelize.Col,
        Series: []excelize.ChartSeries{
            {
                Name:       "Sheet1!$A$2",
                Categories: "Sheet1!$B$1:$D$1",
                Values:     "Sheet1!$B$2:$D$2",
            },
        },
        Format: excelize.GraphicOptions{
            ScaleX:          1,
            ScaleY:          1,
            OffsetX:         15,
            OffsetY:         10,
            PrintObject:     &enable,
            LockAspectRatio: false,
            Locked:          &disable,
        },
        Title: []excelize.RichTextRun{
            {
                Text: "2D 클러스터형 세로 막 대형 차트 - 꺾은 선형 차트",
            },
        },
        Legend: excelize.ChartLegend{
            Position: "left",
        },
        PlotArea: excelize.ChartPlotArea{
            ShowCatName:     false,
            ShowLeaderLines: false,
            ShowPercent:     true,
            ShowSerName:     true,
            ShowVal:         true,
        },
    }, &excelize.Chart{
        Type: excelize.Line,
        Series: []excelize.ChartSeries{
            {
                Name:       "Sheet1!$A$4",
                Categories: "Sheet1!$B$1:$D$1",
                Values:     "Sheet1!$B$4:$D$4",
                Marker: excelize.ChartMarker{
                    Symbol: "none", Size: 10,
                },
            },
        },
        Format: excelize.GraphicOptions{
            ScaleX:          1,
            ScaleY:          1,
            OffsetX:         15,
            OffsetY:         10,
            PrintObject:     &enable,
            LockAspectRatio: false,
            Locked:          &disable,
        },
        Legend: excelize.ChartLegend{
            Position: "right",
        },
        PlotArea: excelize.ChartPlotArea{
            ShowCatName:     false,
            ShowLeaderLines: false,
            ShowPercent:     true,
            ShowSerName:     true,
            ShowVal:         true,
        },
    }); err != nil {
        fmt.Println(err)
        return
    }
    // 통합 문서 저장
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## 차트 시트 추가 {#AddChartSheet}

```go
func (f *File) AddChartSheet(sheet string, chart *ChartOptions, combo ...*ChartOptions) error
```

AddChartSheet 는 주어진 차트 형식 세트 (예: 오프셋, 배율, 종횡비 설정 및 인쇄 설정) 및 속성 세트별로 차트 시트를 작성하는 방법을 제공합니다. Excel 에서 차트 시트는 차트 만 포함 된 워크 시트입니다.

## 차트 삭제 {#DeleteChart}

```go
func (f *File) DeleteChart(sheet, cell string) error
```

DeleteChart 는 주어진 워크 시트와 셀 이름으로 XLSX 에서 차트를 삭제하는 기능을 제공합니다.
