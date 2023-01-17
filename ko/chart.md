# 차트

## 차트 추가 {#AddChart}

```go
func (f *File) AddChart(sheet, cell string, chart *ChartOptions, combo ...*ChartOptions) error
```

AddChart 는 지정된 차트 형식 집합 (예: 오프셋, 축척, 종횡비 설정 및 인쇄 설정) 및 속성 집합을 사용하여 시트에 차트를 추가하는 방법을 제공합니다.

다음은 excelize 에서 지원하는 차트의 `Type` 을 보여 주며:

유형|차트
---|---
area                        | 2D 영역 차트
areaStacked                 | 2D 스택 영역 차트
areaPercentStacked          | 2D 100% 스택 영역 차트
area3D                      | 3D 영역 차트
area3DStacked               | 3D 스택 영역 차트
area3DPercentStacked        | 3D 100% 누적 영역 차트
bar                         | 2D 클러스터 막대 차트
barStacked                  | 2D 스택 막대 차트
barPercentStacked           | 2D 100% 스택 막대 차트
bar3DClustered              | 3D 클러스터 막대 차트
bar3DStacked                | 3D 누적 막 대형 차트
bar3DPercentStacked         | 3D 100% 스택 막대 차트
bar3DConeClustered          | 3D 원뿔 클러스터된 막대 차트
bar3DConeStacked            | 3D 원뿔 누적 막대 차트
bar3DConePercentStacked     | 3D 100% 콘 막대 차트
bar3DPyramidClustered       | 3D 피라미드 클러스터 막대 차트
bar3DPyramidStacked         | 3D 피라미드 누적 막대 차트
bar3DPyramidPercentStacked  | 3D 100% 피라미드 누적 막대 차트
bar3DCylinderClustered      | 3D 실린더 클러스터된 막대 차트
bar3DCylinderStacked        | 3D 실린더 스택 막대 차트
bar3DCylinderPercentStacked | 3D 100% 실린더 적층 막대 차트
col                         | 2D 클러스터형 세로 막 대형 차트
colStacked                  | 2D 누적 세로 막 대형 차트
colPercentStacked           | 2D 100% 스택 세로 막 대형 차트
col3DClustered              | 3D 클러스터 된 세로 막 대형 차트
col3D                       | 3D 세로 막 대형 차트
col3DStacked                | 3D 누적 세로 막 대형 차트
col3DPercentStacked         | 3D 100% 누적 세로 막 대형 차트
col3DCone                   | 3D 원뿔 열차트
col3DConeClustered          | 3D 원뿔 클러스터된 열 차트
col3DConeStacked            | 3D 원뿔 누적 열 차트
col3DConePercentStacked     | 3D 100% 콘 스택 열 차트
col3DPyramid                | 3D 피라미드 열차트
col3DPyramidClustered       | 3D 피라미드 클러스터된 열 차트
col3DPyramidStacked         | 3D 피라미드 누적 열 차트
col3DPyramidPercentStacked  | 3D 100% 피라미드 누적 열 차트
col3DCylinder               | 3D 원통 열차트
col3DCylinderClustered      | 3D 실린더 클러스터된 열 차트
col3DCylinderStacked        | 3D 실린더 스택 컬럼 차트
col3DCylinderPercentStacked | 3D 100% 실린더 스택 컬럼 차트
doughnut                    | 도넛 차트
line                        | 꺾은 선형 차트
pie                         | 원형 차트
pie3D                       | 3D 원형 차트
radar                       | 레이더 차트
scatter                     | 분산 형 차트
surface3D                   | 3D 표면 차트
wireframeSurface3D          | 3D 와이어프레임 표면 차트
contour                     | 등고선 차트
wireframeContour            | 와이어프레임 윤곽 차트
bubble                      | 버블 차트
bubble3D                    | 3D 버블 차트

Office Excel 차트 데이터 영역 `Series` 에서 데이터를 그릴 정보 집합, 범례 항목 (계열) 및 가로 (범주) 축 레이블을 지정합니다.

설정할 수 있는 `Series` 옵션은 다음과 같습니다:

매개 변수|설명
---|---
Name|범례 항목 (계열) 은 차트 범례 및 수식 표시줄에 표시됩니다. `Name` 매개 변수는 선택 사항입니다. 이 값을 지정하지 않으면 기본값은 `Series 1 .. n`. 수식 표현에 대한 `Name` 지원(예: `Sheet1!$A$1`).
Categories|Horizontal (category) axis label. The `Categories` parameter is optional in most chart types, the default is a contiguous sequence of the form `1..n`.
수평(범주) 축 레이블입니다. '범주' 매개 변수는 대부분의 차트 유형에서 선택 사항이며 기본값은 '1..n' 형식의 연속 시퀀스입니다.
Values|`Series` 에서 가장 중요한 매개 변수인 차트 데이터 영역도 차트를 만들 때 필요한 유일한 매개 변수입니다. 이 옵션은 차트를 차트가 표시하는 워크시트 데이터에 연결합니다.
Line| 선 차트의 선 형식을 설정합니다. `Line` 속성은 선택 사항이며 제공되지 않으면 기본 스타일이됩니다. 설정할 수있는 옵션은 `Width` 입니다. `Width` 의 범위는 0.25pt-999pt 입니다. 너비 값이 범위를 벗어나면 선의 기본 너비는 2pt 입니다.
Marker|선형 차트 및 분산 형 차트의 마커를 설정합니다. 선택적 필드 `Size` 의 범위는 2-72 입니다 (기본값은 `5`). 선택적 필드 `Symbol` 의 열거 값은 다음과 같습니다 (기본값은 `auto`): `circle`, `dash`, `diamond`, `dot`, `none`, `picture`, `plus`, `square`, `star`, `triangle`, `x`, `auto`.

차트 범례의 속성을 설정합니다. 설정할 수 있는 옵션은 다음과 같습니다:

매개 변수|유형|설명
---|---|---
Position        | `string` | 차트 범례의 위치
ShowLegendKey   | `bool`   | 데이터 레이블에 범례 항목 레이블을 표시할지 여부를 지정합니다

차트 범례의 `Position` 을 설정합니다. 기본 범례 위치는 `right` 입니다. 다음은이 매개 변수의 선택적 값입니다:

매개 변수|설명
---|---
none|범례 비활성화
top|On top
bottom|On bottom
left|On left
right|On right
top_right|On top right

범례 키를 설정하는 `ShowLegendKey`  매개 변수는 데이터 레이블에 표시됩니다. 기본값은 `false` 입니다.

차트 제목은 `Title` 개체의 `Name` 매개변수를 선택하여 설정되며 제목은 차트 위에 표시됩니다. 매개 변수 `Name` 은 아이콘 제목을 지정하지 않으면 `Sheet1!$A$1` 과 같은 수식 표현의 사용을 지원합니다.

`ShowBlanksAs` 매개변수는 "셀 숨기기 및 빈 셀" 설정을 제공합니다. 기본값은 `gap` 입니다. Excel 응용 프로그램에서 "빈 셀은" 로 표시됩니다: "space". 다음은 이 매개 변수에 대한 선택적 값입니다.

매개 변수|설명
---|---
gap|space
span|Connect data points with straight lines
zero|zero value

계열의 각 데이터 마커는 `VaryColors` 에 의해 다른 색상을 가지고 있음을 지정합니다. 기본 값은 `true` 입니다.

매개변수 `format` 은 차트 오프셋, 배율, 종횡비 설정 및 인쇄 특성과 [`AddPicture`](image.md#AddPicture) 함수에 사용되는 매개 변수에 대한 설정을 제공합니다.

차트 플롯 영역의 위치를 플롯 영역별로 설정합니다. 설정할 수 있는 속성은 다음과 같습니다:

매개 변수|유형|기본값|설명
---|---|---|---
ShowBubbleSize  | `bool` | `false` | 거품 크기를 지정하여 데이터 레이블에 표시해야 합니다.
ShowCatName     | `bool` | `true`  | 범주 이름
ShowLeaderLines | `bool` | `false` | 범주 이름이 데이터 레이블에 표시되도록 지정합니다.
ShowPercent     | `bool` | `false` | 백분율이 데이터 레이블에 표시되도록 지정합니다.
ShowSerName     | `bool` | `false` | 계열 이름이 데이터 레이블에 표시되도록 지정합니다.
ShowVal         | `bool` | `false` | 값이 데이터 레이블에 표시되도록 지정합니다.

기본 수평 및 세로 축 옵션을 `XAxis` 및 `YAxis` 으로 설정합니다.

설정할 수있는 `XAxis` 의 속성은 다음과 같습니다:

매개 변수|유형|기본값|설명
---|---|---|---
None           | `bool`     | `false` | 축 비활성화.
MajorGridLines | `bool`     | `false` | 주요 눈금 선을 지정합니다.
MinorGridLines | `bool`     | `false` | 작은 눈금 선을 지정합니다.
TickLabelSkip  | `int`      | `1`     | 그려진 레이블간에 건너 뛸 눈금 레이블 수를 지정합니다. `TickLabelSkip` 속성은 선택 사항입니다. 기본값은 auto 입니다.
ReverseOrder   | `bool`     | `false` | 역순 (차트 방향) 의 범주 또는 값을 지정합니다. `ReverseOrder` 속성은 선택 사항입니다.
Maximum        | `*float64` | `0`     | 고정 최대값 0 이 자동임을 지정합니다. 최대 속성은 선택 사항입니다.
Minimum        | `*float64` | `0`     |  고정 된 최소, 0 은 자동 지정 합니다. 최소 속성은 선택 사항입니다. 기본값은 자동입니다.

설정할 수있는 `YAxis` 의 속성은 다음과 같습니다:

매개 변수|유형|기본값|설명
---|---|---|---
None           | `bool`     | `false` | 축 비활성화.
MajorGridLines | `bool`     | `false` | 주요 눈금 선을 지정합니다.
MinorGridLines | `bool`     | `false` | 작은 눈금 선을 지정합니다.
MajorUnit      | `float64`  | `0`     | 주요 눈금 사이의 거리를 지정합니다. 양의 부동 소수점 숫자를 포함해야합니다. `MajorUnit` 속성은 선택 사항입니다. 기본값은 auto 입니다.
ReverseOrder   | `bool`     | `false` | 역순 (차트 방향) 의 범주 또는 값을 지정합니다. `ReverseOrder` 속성은 선택 사항입니다.
Maximum        | `*float64` | `0`     | 고정 최대값 0 이 자동임을 지정합니다. 최대 속성은 선택 사항입니다.
Minimum        | `*float64` | `0`     |  고정 된 최소, 0 은 자동 지정 합니다. 최소 속성은 선택 사항입니다. 기본값은 자동입니다.

차트 크기를 `Dimension` 속성으로 설정합니다. 차원 속성은 선택 사항입니다. 설정할 수 있는 속성은 다음과 같습니다:

매개 변수|유형|기본값|설명
---|---|---|---
height | `int` | 290 | 높이
width  | `int` | 480 | 너비

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
        Type: "col",
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
        Title: excelize.ChartTitle{
            Name: "2D 클러스터형 세로 막 대형 차트 - 꺾은 선형 차트",
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
        Type: "line",
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
