# 피벗 테이블 {#PivotTable}

피벗 테이블은보다 광범위한 테이블의 데이터 (예 : 데이터베이스, 스프레드 시트 또는 비즈니스 인텔리전스 프로그램)를 요약하는 통계 테이블입니다. 이 요약에는 피벗 테이블이 의미있는 방식으로 그룹화되는 합계, 평균 또는 기타 통계가 포함될 수 있습니다.

`PivotTableOptions` 은 피벗 테이블의 형식 설정을 직접 매핑합니다.

```go
type PivotTableOptions struct {
    pivotTableSheetName string
    DataRange           string            `json:"data_range"`
    PivotTableRange     string            `json:"pivot_table_range"`
    Rows                []PivotTableField `json:"rows"`
    Columns             []PivotTableField `json:"columns"`
    Data                []PivotTableField `json:"data"`
    Filter              []PivotTableField `json:"filter"`
    RowGrandTotals      bool              `json:"row_grand_totals"`
    ColGrandTotals      bool              `json:"col_grand_totals"`
    ShowDrill           bool              `json:"show_drill"`
    UseAutoFormatting   bool              `json:"use_auto_formatting"`
    PageOverThenDown    bool              `json:"page_over_then_down"`
    MergeItem           bool              `json:"merge_item"`
    CompactData         bool              `json:"compact_data"`
    ShowError           bool              `json:"show_error"`
    ShowRowHeaders      bool              `json:"show_row_headers"`
    ShowColHeaders      bool              `json:"show_col_headers"`
    ShowRowStripes      bool              `json:"show_row_stripes"`
    ShowColStripes      bool              `json:"show_col_stripes"`
    ShowLastColumn      bool              `json:"show_last_column"`
    PivotTableStyleName string            `json:"pivot_table_style_name"`
    // 필터링되거나 내 보내지 않은 필드를 포함합니다
}
```

`PivotTableStyleName` 내장 피벗 테이블 스타일 이름:

```text
PivotStyleLight1 - PivotStyleLight28
PivotStyleMedium1 - PivotStyleMedium28
PivotStyleDark1 - PivotStyleDark28
```

`PivotTableField` 는 피벗 테이블의 필드 설정을 직접 매핑합니다.

```go
type PivotTableField struct {
    Compact         bool   `json:"compact"`
    Data            string `json:"data"`
    Name            string `json:"name"`
    Outline         bool   `json:"outline"`
    Subtotal        string `json:"subtotal"`
    DefaultSubtotal bool   `json:"default_subtotal"`
}
```

`Subtotal` 은이 데이터 필드에 적용되는 집계 함수를 지정합니다. 기본값은 `Sum` 입니다. 이 속성에 가능한 값은 다음과 같습니다.

|선택적 값|
|---|
|Average|
|Count|
|CountNums|
|Max|
|Min|
|Product|
|StdDev|
|StdDevp|
|Sum|
|Var|
|Varp|

`Name` 은 데이터 필드의 이름을 지정합니다. 데이터 필드 이름에 최대 `255` 자를 사용할 수 있으며 초과 문자는 잘립니다.

## 피벗 테이블 만들기 {#AddPivotTable}

```go
func (f *File) AddPivotTable(opts *PivotTableOptions) error
```

AddPivotTable 은 지정된 피벗 테이블 옵션으로 피벗 테이블을 추가하는 방법을 제공합니다.

예를 들어, `Sheet1!$G$2:$M$34` 영역에 데이터 소스가 `Sheet1!$A$1:$E$31` 인 피벗 테이블을 작성하십시오.

<p align="center"><img width="1117" src="./images/pivot_table_01.png" alt="Go 를 사용하여 excelize 로 피벗 테이블 만들기"></p>

```go
package main

import (
    "fmt"
    "math/rand"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    // 시트에 일부 데이터 생성
    month := []string{"Jan", "Feb", "Mar", "Apr", "May",
        "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"}
    year := []int{2017, 2018, 2019}
    types := []string{"Meat", "Dairy", "Beverages", "Produce"}
    region := []string{"East", "West", "North", "South"}
    f.SetSheetRow("Sheet1", "A1", &[]string{"Month", "Year", "Type", "Sales", "Region"})
    for row := 2; row < 32; row++ {
        f.SetCellValue("Sheet1", fmt.Sprintf("A%d", row), month[rand.Intn(12)])
        f.SetCellValue("Sheet1", fmt.Sprintf("B%d", row), year[rand.Intn(3)])
        f.SetCellValue("Sheet1", fmt.Sprintf("C%d", row), types[rand.Intn(4)])
        f.SetCellValue("Sheet1", fmt.Sprintf("D%d", row), rand.Intn(5000))
        f.SetCellValue("Sheet1", fmt.Sprintf("E%d", row), region[rand.Intn(4)])
    }
    if err := f.AddPivotTable(&excelize.PivotTableOptions{
        DataRange:       "Sheet1!$A$1:$E$31",
        PivotTableRange: "Sheet1!$G$2:$M$34",
        Rows: []excelize.PivotTableField{
            {Data: "Month", DefaultSubtotal: true}, {Data: "Year"}},
        Filter: []excelize.PivotTableField{
            {Data: "Region"}},
        Columns: []excelize.PivotTableField{
            {Data: "Type", DefaultSubtotal: true}},
        Data: []excelize.PivotTableField{
            {Data: "Sales", Name: "Summarize", Subtotal: "Sum"}},
        RowGrandTotals: true,
        ColGrandTotals: true,
        ShowDrill:      true,
        ShowRowHeaders: true,
        ShowColHeaders: true,
        ShowLastColumn: true,
    }); err != nil {
        fmt.Println(err)
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```
