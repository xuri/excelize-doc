# 유틸리티 기능

## 양식 만들기 {#AddTable}

```go
func (f *File) AddTable(sheet, hcell, vcell, format string) error
```

AddTable 은 지정된 워크 시트 이름, 좌표 영역 및 형식 집합으로 워크 시트에 테이블을 추가하는 방법을 제공합니다.

- 예제 1, 에서는 `Sheet1`에서 `A1:D5` 테이블을 만듭니다:

<p align="center"><img width="612" src="./images/addtable_01.png" alt="양식 만들기"></p>

```go
err := f.AddTable("Sheet1", "A1", "D5", ``)
```

- 예제 2, 형식 집합으로 `Sheet2` 에서 `F2:H6` 테이블을 만듭니다:

<p align="center"><img width="612" src="./images/addtable_02.png" alt="형식 집합으로 테이블 추가"></p>

```go
err := f.AddTable("Sheet2", "F2", "H6", `{
    "table_name": "table",
    "table_style": "TableStyleMedium2",
    "show_first_column": true,
    "show_last_column": true,
    "show_row_stripes": false,
    "show_column_stripes": true
}`)
```

표는 머리글을 포함하여 두 줄 이상이어야합니다. 헤더 셀은 문자열을 포함해야하며 고유해야하며 AddTable 함수를 호출하기 전에 테이블의 헤더 행 데이터를 설정해야합니다. 여러 테이블은 교차점이없는 영역을 조정합니다.

`table_name`: 테이블의 이름은 테이블의 동일한 워크시트 이름에서 고유해야 합니다.

`table_style`: 기본 제공 테이블 스타일 이름:

```text
TableStyleLight1 - TableStyleLight21
TableStyleMedium1 - TableStyleMedium28
TableStyleDark1 - TableStyleDark11
```

인덱스|스타일|인덱스|스타일|인덱스|스타일
---|---|---|---|---|---
|<img src="../images/table_style/light/0.png" width="61">|TableStyleLight1|<img src="../images/table_style/light/1.png" width="61">|TableStyleLight2|<img src="../images/table_style/light/2.png" width="61">
TableStyleLight3|<img src="../images/table_style/light/3.png" width="61">|TableStyleLight4|<img src="../images/table_style/light/4.png" width="61">|TableStyleLight5|<img src="../images/table_style/light/5.png" width="61">
TableStyleLight6|<img src="../images/table_style/light/6.png" width="61">|TableStyleLight7|<img src="../images/table_style/light/7.png" width="61">|TableStyleLight8|<img src="../images/table_style/light/8.png" width="61">
TableStyleLight9|<img src="../images/table_style/light/9.png" width="61">|TableStyleLight10|<img src="../images/table_style/light/10.png" width="61">|TableStyleLight11|<img src="../images/table_style/light/11.png" width="61">
TableStyleLight12|<img src="../images/table_style/light/12.png" width="61">|TableStyleLight13|<img src="../images/table_style/light/13.png" width="61">|TableStyleLight14|<img src="../images/table_style/light/14.png" width="61">
TableStyleLight15|<img src="../images/table_style/light/15.png" width="61">|TableStyleLight16|<img src="../images/table_style/light/16.png" width="61">|TableStyleLight17|<img src="../images/table_style/light/17.png" width="61">
TableStyleLight18|<img src="../images/table_style/light/18.png" width="61">|TableStyleLight19|<img src="../images/table_style/light/19.png" width="61">|TableStyleLight20|<img src="../images/table_style/light/20.png" width="61">
TableStyleLight21|<img src="../images/table_style/light/21.png" width="61">|TableStyleMedium1|<img src="../images/table_style/medium/1.png" width="61">|TableStyleMedium2|<img src="../images/table_style/medium/2.png" width="61">
TableStyleMedium3|<img src="../images/table_style/medium/3.png" width="61">|TableStyleMedium4|<img src="../images/table_style/medium/4.png" width="61">|TableStyleMedium5|<img src="../images/table_style/medium/5.png" width="61">
TableStyleMedium6|<img src="../images/table_style/medium/6.png" width="61">|TableStyleMedium7|<img src="../images/table_style/medium/7.png" width="61">|TableStyleMedium8|<img src="../images/table_style/medium/8.png" width="61">
TableStyleMedium9|<img src="../images/table_style/medium/9.png" width="61">|TableStyleMedium10|<img src="../images/table_style/medium/10.png" width="61">|TableStyleMedium11|<img src="../images/table_style/medium/11.png" width="61">
TableStyleMedium12|<img src="../images/table_style/medium/12.png" width="61">|TableStyleMedium13|<img src="../images/table_style/medium/13.png" width="61">|TableStyleMedium14|<img src="../images/table_style/medium/14.png" width="61">
TableStyleMedium15|<img src="../images/table_style/medium/15.png" width="61">|TableStyleMedium16|<img src="../images/table_style/medium/16.png" width="61">|TableStyleMedium17|<img src="../images/table_style/medium/17.png" width="61">
TableStyleMedium18|<img src="../images/table_style/medium/18.png" width="61">|TableStyleMedium19|<img src="../images/table_style/medium/19.png" width="61">|TableStyleMedium20|<img src="../images/table_style/medium/20.png" width="61">
TableStyleMedium21|<img src="../images/table_style/medium/21.png" width="61">|TableStyleMedium22|<img src="../images/table_style/medium/22.png" width="61">|TableStyleMedium23|<img src="../images/table_style/medium/23.png" width="61">
TableStyleMedium24|<img src="../images/table_style/medium/24.png" width="61">|TableStyleMedium25|<img src="../images/table_style/medium/25.png" width="61">|TableStyleMedium26|<img src="../images/table_style/medium/26.png" width="61">
TableStyleMedium27|<img src="../images/table_style/medium/27.png" width="61">|TableStyleMedium28|<img src="../images/table_style/medium/28.png" width="61">|TableStyleDark1|<img src="../images/table_style/dark/1.png" width="61">
TableStyleDark2|<img src="../images/table_style/dark/2.png" width="61">|TableStyleDark3|<img src="../images/table_style/dark/3.png" width="61">|TableStyleDark4|<img src="../images/table_style/dark/4.png" width="61">
TableStyleDark5|<img src="../images/table_style/dark/5.png" width="61">|TableStyleDark6|<img src="../images/table_style/dark/6.png" width="61">|TableStyleDark7|<img src="../images/table_style/dark/7.png" width="61">
TableStyleDark8|<img src="../images/table_style/dark/8.png" width="61">|TableStyleDark9|<img src="../images/table_style/dark/9.png" width="61">|TableStyleDark10|<img src="../images/table_style/dark/10.png" width="61">
TableStyleDark11|<img src="../images/table_style/dark/11.png" width="61">||||

## 자동 필터 {#AutoFilter}

```go
func (f *File) AutoFilter(sheet, hcell, vcell, format string) error
```

AutoFilter 는 지정된 워크시트 이름, 좌표 영역 및 설정으로 워크시트에 자동 필터를 추가하는 방법을 제공합니다. Excel 의 자동 필터는 몇 가지 간단한 기준에 따라 2D 데이터 범위를 필터링하는 방법입니다.

예제 1, `Sheet1` 의 셀 범위 `A1:D4` 에 자동 필터를 적용합니다:

<p align="center"><img width="612" src="./images/autofilter_01.png" alt="자동 필터 추가"></p>

```go
err := f.AutoFilter("Sheet1", "A1", "D4", "")
```

예제 2, 에서는 자동 필터에서 데이터를 필터링합니다:

```go
err := f.AutoFilter("Sheet1", "A1", "D4", `{"column":"B","expression":"x != blanks"}`)
```

`column` 은 간단한 기준에 따라 자동 필터 범위의 필터 열을 정의합니다.

필터 조건을 지정하는 것만으로는 충분하지 않습니다. 필터 조건과 일치하지 않는 행도 숨겨야 합니다. 행은 [`SetRowVisible()`](sheet.md#SetRowVisible) 방법을 사용하여 숨김이 있습니다. Excelize 는 파일 형식의 일부가 아니므로 행을 자동으로 필터링할 수 없습니다.

열에 대한 필터 기준 설정:

`expression` 은 조건을 정의하며, 필터 조건을 설정하는 데 다음 연산자가 사용할 수 있습니다:

```text
==
!=
>
<
>=
<=
and
or
```

식은 `and` 및 `or` 연산자로 구분된 단일 문 또는 두 개의 문으로 구성할 수 있습니다. 예를 들어:

```text
x <  2000
x >  2000
x == 2000
x >  2000 and x <  5000
x == 2000 or  x == 5000
```

공백 또는 비블 데이터의 필터링은 식에서 공백 또는 비공백 값을 사용하여 수행할 수 있습니다:

```text
x == Blanks
x == NonBlanks
```

Office Excel 에서는 다음과 같은 간단한 문자열 일치 작업도 허용합니다:

```text
x == b*      // begins with b
x != b*      // doesn't begin with b
x == *b      // ends with b
x != *b      // doesn't end with b
x == *b*     // contains b
x != *b*     // doesn't contains b
```

`*` 를 사용하여 문자 나 숫자와 일치시키고 `?` 를 사용하여 단일 문자 또는 숫자와 일치시킬 수도 있습니다. Excel 의 필터에서 다른 정규식 수량자는 지원되지 않습니다. Excel의 정규 표현식 문자는 `~` 를 사용하여 이스케이프할 수 있습니다.

위의 예제에서 자리 표시자 변수 `x`를 간단한 문자열로 대체할 수 있습니다. 실제 자리 표시자 이름은 내부적으로 무시되므로 다음의 모든 이름이 동일합니다:

```text
x     < 2000
col   < 2000
Price < 2000
```

## 링크 된 값 업데이트 {#UpdateLinkedValue}

```go
func (f *File) UpdateLinkedValue() error
```

업데이트링크드밸류 수정 스프레드시트 내의 링크된 값은 Office Excel 2007 및 2010 에서 업데이트되지 않습니다. 이 함수는 셀에 연결된 값이 있을 때 값 태그를 제거합니다. 참조 [https://social.technet.microsoft.com/Forums/office/en-US/e16bae1f-6a2c-4325-8013-e989a3479066/excel-2010-linked-cells-not-updating](https://social.technet.microsoft.com/Forums/office/en-US/e16bae1f-6a2c-4325-8013-e989a3479066/excel-2010-linked-cells-not-updating) 주의 사항 : 열면 XLSX 파일 Excel 은 연결된 값을 업데이트하고 새 값을 생성하며 파일을 저장하거나 저장하라는 메시지가 표시됩니다.

통합 문서의 셀 캐시를 지우는 효과는 `<v>` 태그에 대한 수정으로 나타납니다. 예를 들어 지우기 전에 셀 캐시를 선택합니다:

```xml
<row r="19" spans="2:2">
    <c r="B19">
        <f>SUM(Sheet2!D2,Sheet2!D11)</f>
        <v>100</v>
     </c>
</row>
```

셀 캐시를 지운 후:

```xml
<row r="19" spans="2:2">
    <c r="B19">
        <f>SUM(Sheet2!D2,Sheet2!D11)</f>
    </c>
</row>
```

## 셀 이름 분할 {#SplitCellName}

```go
func SplitCellName(cell string) (string, int, error)
```

SplitCellName 열 이름과 행 번호로 셀 이름을 분할합니다. 예를 들어:

```go
excelize.SplitCellName("AK74") // return "AK", 74, nil
```

## 셀 이름 결합 {#JoinCellName}

```go
func JoinCellName(col string, row int) (string, error)
```

JoinCellName 열 이름 및 행 번호에서 셀 이름을 조인합니다.

## 열 이름을 숫자로 {#ColumnNameToNumber}

```go
func ColumnNameToNumber(name string) (int, error)
```

ColumnNameToNumber는 Excel 시트 열 이름을 `int` 로 변환하는 기능을 제공합니다. 열 이름 케이스를 구분하지 않습니다. 열 이름이 올바르지 않은 경우 함수에서 오류를 반환합니다. 예를 들어:

```go
excelize.ColumnNameToNumber("AK") // returns 37, nil
```

## 이름에 대 한 열 번호 {#ColumnNumberToName}

```go
func ColumnNumberToName(num int) (string, error)
```

ColumnNumberToName 은 정수를 Excel 시트 열 제목으로 변환하는 기능을 제공합니다. 예를 들어:

```go
excelize.ColumnNumberToName(37) // returns "AK", nil
```

## 좌표에 대 한 셀 이름 {#CellNameToCoordinates}

```go
func CellNameToCoordinates(cell string) (int, int, error)
```

CellNameToCoordinates 는 `[X, Y]` 좌표로 상형 셀 이름을 변환하거나 오류를 반환합니다. 예를 들어:

```go
CellCoordinates("A1") // returns 1, 1, nil
CellCoordinates("Z3") // returns 26, 3, nil
```

## 셀 이름에 좌표 지정 {#CoordinatesToCellName}

```go
func CoordinatesToCellName(col, row int) (string, error)
```

CoordinatesToCellName 는 `[X, Y]` 좌표를 알파 숫자 셀 이름으로 변환하거나 오류를 반환합니다. 예를 들어:

```go
CoordinatesToCellName(1, 1) // returns "A1", nil
```

## 조건 스타일 {#NewConditionalStyle}

```go
func (f *File) NewConditionalStyle(style string) (int, error)
```

NewConditionalStyle 지정된 스타일 형식에 의해 조건부 형식에 대 한 스타일을 만드는 함수를 제공 합니다. 매개 변수는 함수 [`NewStyle()`](style.md#NewStyle) 와 동일합니다. 색상 필드는 RGB 색상 코드를 사용하고 현재 글꼴, 채우기, 정렬 및 테두리를 설정하기 위해 지원만 사용합니다.

## 조건 형식 {#SetConditionalFormat}

```go
func (f *File) SetConditionalFormat(sheet, area, formatSet string) error
```

SetConditionalFormat 는 셀 값에 대한 조건부 서식 지정 규칙을 만드는 함수를 제공합니다. 조건부 서식지정은 특정 기준에 따라 셀 또는 셀 범위에 형식을 적용할 수 있는 Office Excel 의 기능입니다.

`type` 옵션은 필수 매개 변수이며 기본값이 없습니다. 허용 형식 값과 관련 매개 변수는 다음과 같습니다:

<table>
    <thead>
        <tr>
            <th>형식</th>
            <th>매개 변수</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=4>cell</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>value</td>
        </tr>
        <tr>
            <td>minimum</td>
        </tr>
        <tr>
            <td>maximum</td>
        </tr>
        <tr>
            <td rowspan=4>date</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>value</td>
        </tr>
        <tr>
            <td>minimum</td>
        </tr>
        <tr>
            <td>maximum</td>
        </tr>
        <tr>
            <td>time_period</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td rowspan=2>text</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>value</td>
        </tr>
        <tr>
            <td>average</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>duplicate</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td>unique</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td rowspan=2>top</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>value</td>
        </tr>
        <tr>
            <td rowspan=2>bottom</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>value</td>
        </tr>
        <tr>
            <td>blanks</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td>no_blanks</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td>errors</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td>no_errors</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td rowspan=6>2_color_scale</td>
            <td>min_type</td>
        </tr>
        <tr>
            <td>max_type</td>
        </tr>
        <tr>
            <td>min_value</td>
        </tr>
        <tr>
            <td>max_value</td>
        </tr>
        <tr>
            <td>min_color</td>
        </tr>
        <tr>
            <td>max_color</td>
        </tr>
        <tr>
            <td rowspan=9>3_color_scale</td>
            <td>min_type</td>
        </tr>
        <tr>
            <td>mid_type</td>
        </tr>
        <tr>
            <td>max_type</td>
        </tr>
        <tr>
            <td>min_value</td>
        </tr>
        <tr>
            <td>mid_value</td>
        </tr>
        <tr>
            <td>max_value</td>
        </tr>
        <tr>
            <td>min_color</td>
        </tr>
        <tr>
            <td>mid_color</td>
        </tr>
        <tr>
            <td>max_color</td>
        </tr>
        <tr>
            <td rowspan=5>data_bar</td>
            <td>min_type</td>
        </tr>
        <tr>
            <td>max_type</td>
        </tr>
        <tr>
            <td>min_value</td>
        </tr>
        <tr>
            <td>max_value</td>
        </tr>
        <tr>
            <td>bar_color</td>
        </tr>
        <tr>
            <td>formula</td>
            <td>criteria</td>
        </tr>
    </tbody>
</table>

`criteria` 매개 변수는 셀 데이터가 평가되는 기준을 설정하는 데 사용됩니다. 기본값이 없습니다. `{"type": "cell}` 에 적용되는 가장 일반적인 기준은 다음과 같습니다:

텍스트 설명 문자|기호 표현
---|---
between|
not between|
equal to|==
not equal to|!=
greater than|>
less than|<
greater than or equal to|>=
less than or equal to|<=

위의 첫 번째 열에서 Excel 의 텍스트 설명 문자열을 사용하거나 보다 일반적인 기호 대안을 사용할 수 있습니다.

다른 조건부 형식 유형과 관련된 추가 기준은 아래 관련 섹션에 나와 있습니다.

`value`: 값은 일반적으로 `criteria` 매개 변수와 함께 사용되어 셀 데이터가 평가되는 규칙을 설정합니다:

```go
f.SetConditionalFormat("Sheet1", "D1:D10", fmt.Sprintf(`[
{
    "type": "cell",
    "criteria": ">",
    "format": %d,
    "value": "6"
}]`, format))
```

`value` 속성은 셀 참조일 수도 있습니다:

```go
f.SetConditionalFormat("Sheet1", "D1:D10", fmt.Sprintf(`[
{
    "type": "cell",
    "criteria": ">",
    "format": %d,
    "value": "$C$1"
}]`, format))
```

type: `format` - 조건부 서식 기준이 충족될 때 셀에 적용되는 형식을 지정하는 데 `format` 매개 변수가 사용됩니다. 형식은 셀 형식과 동일한 방식으로 [`NewConditionalStyle()`](utils.md#NewConditionalStyle) 메서드를 사용하여 만들어집니다:

```go
format, err = f.NewConditionalStyle(`{
    "font":
    {
        "color": "#9A0511"
    },
    "fill":
    {
        "type": "pattern",
        "color": ["#FEC7CE"],
        "pattern": 1
    }
}`)
if err != nil {
    fmt.Println(err)
}
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "cell",
    "criteria": ">",
    "format": %d,
    "value": "6"
}]`, format))
```

참고: Excel 에서 조건부 형식은 기존 셀 형식 위에 중첩되며 모든 셀 형식 속성을 수정할 수 있는 것은 아닙니다. 조건부 형식으로 수정할 수 없는 속성은 글꼴 이름, 글꼴 크기, 초중문자 및 하위 스크립트, 대각선 테두리, 모든 정렬 속성 및 모든 보호 속성입니다.

Excel 은 조건부 서식에 사용할 일부 기본 형식을 지정합니다. 다음과 같은 excelize 형식을 사용하여 복제할 수 있습니다:

```go
// 나쁜 조건부 장미 형식입니다.
format1, err = f.NewConditionalStyle(`{
    "font":
    {
        "color": "#9A0511"
    },
    "fill":
    {
        "type": "pattern",
        "color": ["#FEC7CE"],
        "pattern": 1
    }
}`)

// 중립 조건부에 대한 밝은 노란색 형식입니다.
format2, err = f.NewConditionalStyle(`{
    "font":
    {
        "color": "#9B5713"
    },
    "fill":
    {
        "type": "pattern",
        "color": ["#FEEAA0"],
        "pattern": 1
    }
}`)

// 좋은 조건부에 대한 밝은 녹색 형식입니다.
format3, err = f.NewConditionalStyle(`{
    "font":
    {
        "color": "#09600B"
    },
    "fill":
    {
        "type": "pattern",
        "color": ["#C7EECF"],
        "pattern": 1
    }
}`)
```

type: `minimum` - 최소 매개변수는 `criteria` 가 `between` 또는 `not between` 일 때 하한 값을 설정하는 데 사용됩니다.

```go
// Highlight cells rules: between...
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "cell",
    "criteria": "between",
    "format": %d,
    "minimum": "6",
    "maximum": "8"
}]`, format))
```

type: `maximum` - `maximum` 매개변수는 기준이 `between` 또는 `not between` 일 때 상한 값을 설정하는 데 사용됩니다. 이전 예제를 참조하십시오.

type: `average` - `average` 형식은 Office Excel 의 "Average" 스타일 조건부 형식을 지정하는 데 사용됩니다.

```go
// Top/Bottom rules: Above Average...
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "average",
    "criteria": "=",
    "format": %d,
    "above_average": true
}]`, format1))

// Top/Bottom rules: Below Average...
f.SetConditionalFormat("Sheet1", "B1:B10", fmt.Sprintf(`[
{
    "type": "average",
    "criteria": "=",
    "format": %d,
    "above_average": false
}]`, format2))
```

type: `duplicate` - `duplicate` 유형은 범위의 중복 셀을 강조 표시하는 데 사용됩니다:

```go
// Highlight cells rules: Duplicate Values...
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "duplicate",
    "criteria": "=",
    "format": %d
}]`, format))
```

type: `unique` - 고유 유형은 범위의 고유한 셀을 강조 표시하는 데 사용됩니다:

```go
// Highlight cells rules: Not Equal To...
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "unique",
    "criteria": "=",
    "format": %d
}]`, format))
```

type: `top` - `top` 형식은 범위의 숫자 또는 백분율로 상위 n 값을 지정하는 데 사용됩니다:

```go
// Top/Bottom rules: Top 10.
f.SetConditionalFormat("Sheet1", "H1:H10", fmt.Sprintf(`[
{
    "type": "top",
    "criteria": "=",
    "format": %d,
    "value": "6"
}]`, format))
```

기준은 백분율 조건이 필요하다는 것을 나타내는 데 사용할 수 있습니다:

```go
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "top",
    "criteria": "=",
    "format": %d,
    "value": "6",
    "percent": true
}]`, format))
```

type: `2_color_scale` - `2_color_scale` 형식은 Excel의 "2 색 배율" 스타일 조건부 형식을 지정하는 데 사용됩니다:

```go
// Color scales: 2 color.
f.SetConditionalFormat("Sheet1", "A1:A10", `[
{
    "type": "2_color_scale",
    "criteria": "=",
    "min_type": "min",
    "max_type": "max",
    "min_color": "#F8696B",
    "max_color": "#63BE7B"
}]`)
```

이 조건부 형식은 `min_type`, `max_type`, `min_value`, `max_value`, `min_color` 및 `max_color` 로 수정할 수 있습니다. 아래를 참조하십시오.

type: `3_color_scale` - `3_color_scale` 형식은 Excel 의 "3 색 배율" 스타일 조건부 형식을 지정하는 데 사용됩니다:

```go
// Color scales: 3 color.
f.SetConditionalFormat("Sheet1", "A1:A10", `[
{
    "type": "3_color_scale",
    "criteria": "=",
    "min_type": "min",
    "mid_type": "percentile",
    "max_type": "max",
    "min_color": "#F8696B",
    "mid_color": "#FFEB84",
    "max_color": "#63BE7B"
}]`)
```

이 조건부 형식은 `min_type`, `mid_type`, `max_type`, `min_value`, `mid_value`, `max_value`, `min_color`, `mid_color` 및 `max_color` 로 수정할 수 있습니다. 아래를 참조하십시오.

type: `data_bar` - `data_bar` 형식은 Excel 의 "Data Bar" 스타일 조건부 형식을 지정하는 데 사용됩니다.

`min_type` - `min_type` 및 `max_type` 속성은 조건부 서식 지정 유형이 `2_color_scale`, `3_color_scale` 또는 `data_bar` 인 경우에 사용할 수 있습니다. `mid_type` 은 `3_color_scale` 에서 사용할 수 있습니다. 속성은 다음과 같이 사용됩니다:

```go
// Data Bars: Gradient Fill.
f.SetConditionalFormat("Sheet1", "K1:K10", `[
{
    "type": "data_bar",
    "criteria": "=",
    "min_type": "min",
    "max_type": "max",
    "bar_color": "#638EC6"
}]`)
```

사용 가능한 `min/mid/max` 유형은 다음과 같습니다:

매개 변수|설명
---|---
min|Minimum value (for `min_type` only)
num|Numeric
percent|Percentage
percentile|Percentile
formula|Formula
max|Maximum (for `max_type` only)

`mid_type` - `3_color_scale` 에 사용. `min_type` 와 동일, 위의 참조.

`max_type` - `min_type` 와 동일, 위의 참조.

`min_value` - The `min_value` and `max_value` properties are available when the conditional formatting type is `2_color_scale`, `3_color_scale` or `data_bar`. The `mid_value` is available for `3_color_scale`.

`mid_value` - `3_color_scale` 에 사용. `min_value` 와 동일, 위의 참조.

`max_value` - `min_value` 와 동일, 위의 참조.

`min_color` - 조건부 서식 지정 유형이 `2_color_scale`, `3_color_scale` 또는 `data_bar` 인 경우 `min_color` 및 `max_color` 속성을 사용할 수 있습니다. `mid_color` 는 `3_color_scale` 에서 사용할 수 있습니다. 속성은 다음과 같이 사용됩니다.

```go
// Color scales: 3 color.
f.SetConditionalFormat("Sheet1", "B1:B10", `[
{
    "type": "3_color_scale",
    "criteria": "=",
    "min_type": "min",
    "mid_type": "percentile",
    "max_type": "max",
    "min_color": "#F8696B",
    "mid_color": "#FFEB84",
    "max_color": "#63BE7B"
}]`)
```

`mid_color` - `3_color_scale` 에 사용. `min_color` 와 동일, 위의 참조.

`max_color` - `min_color` 와 동일, 위의 참조.

`bar_color` - `data_bar` 에 사용. `min_color` 와 동일, 위의 참조.


## 조건부 서식을 제거합니다 {#UnsetConditionalFormat}

```go
func (f *File) UnsetConditionalFormat(sheet, area string) error
```

UnsetConditionalFormat 은 주어진 워크 시트 이름과 범위에 따라 조건부 서식을 설정 해제하는 기능을 제공합니다.

## 설정 창 {#SetPanes}

```go
func (f *File) SetPanes(sheet, panes string)
```

SetPanes 는 지정된 워크 시트 이름과 창 형식 집합으로 동결 창 및 분할 창을 만들고 제거하는 기능을 제공합니다.

`activePane` 는 활성 창을 정의합니다. 이 특성에 대한 가능한 값은 다음 표에 정의되어 있습니다:

열거 가치|설명
---|---
bottomLeft (Bottom Left Pane) |수직 및 수평 분할이 모두 적용되는 경우 왼쪽 아래 창입니다.<br><br>이 값은 창을 위쪽 및 하부 영역으로 분할하는 가로 분할만 적용된 경우에도 사용됩니다. 이 경우 이 값은 아래쪽 창을 지정합니다.
bottomRight (Bottom Right Pane) | 수직 및 수평 분할이 모두 적용되는 경우 오른쪽 아래 창입니다.
topLeft (Top Left Pane)|수직 및 수평 분할이 모두 적용되는 경우 왼쪽 상단 창입니다.<br><br>이 값은 창을 위쪽 및 하부 영역으로 분할하는 가로 분할만 적용된 경우에도 사용됩니다. 이 경우 이 값은 위쪽 창을 지정합니다.<br><br>이 값은 창을 오른쪽 및 왼쪽 영역으로 분할하는 세로 분할만 적용된 경우에도 사용됩니다. 이 경우 이 값은 왼쪽 창을 지정합니다.
topRight (Top Right Pane)|수직 및 수평 분할이 모두 적용되는 오른쪽 상단 창입니다.<br><br> 이 값은 창을 오른쪽 및 왼쪽 영역으로 분할하는 세로 분할만 적용된 경우에도 사용됩니다. 이 경우 이 값은 오른쪽 창을 지정합니다.

창 상태 유형은 다음 표에 현재 나열된 값으로 제한됩니다:

열거 가치|설명
---|---
frozen (Frozen)|창은 고정되지만 분할되지 않았습니다. 이 상태에서 창이 다시 고정해제되면 분할 없이 단일 창이 생성됩니다.<br><br>이 상태에서분할 막대는 조정할 수 없습니다.
split (Split)|창은 분할되지만 고정되지는 않습니다. 이 상태에서 분할 막대는 사용자가 조정할 수 있습니다.

`x_split` - 분할의 수평 위치, 점의 1/20 에서; 0 이 없는 경우. 창이 고정된 경우 이 값은 위쪽 창에 표시되는 열 수를 나타냅니다.

`y_split` - 분할의 수직 위치, 점의 1/20 에서; 0 이 없는 경우. 창이 고정되면 이 값은 왼쪽 창에 표시되는 행 수를 나타냅니다. 이 특성에 대한 가능한 값은 W3C XML 스키마 이중 데이터 입력에 의해 정의됩니다.

`top_left_cell` - 오른쪽 하단 창에서 왼쪽 상단 셀의 위치 (왼쪽에서 오른쪽으로 이동).

`sqref` - 선택 영역의 범위입니다. 비 연속 범위 집합일 수 있습니다.

예 1: `Sheet1` 에서 열 `A` 를 고정하고 활성 셀을 `Sheet1!K16` 로 설정합니다:

<p align="center"><img width="770" src="./images/setpans_01.png" alt="고정 된 열"></p>

```go
f.SetPanes("Sheet1", `{
    "freeze": true,
    "split": false,
    "x_split": 1,
    "y_split": 0,
    "top_left_cell": "B1",
    "active_pane": "topRight",
    "panes": [
    {
        "sqref": "K16",
        "active_cell": "K16",
        "pane": "topRight"
    }]
}`)
```

예 2: Sheet1 에서 행 1 - 9 행을 고정하고 `Sheet1!A11:XFD11` 에서 활성 셀 범위를 설정합니다:

<p align="center"><img width="770" src="./images/setpans_02.png" alt="열을 고정하고 활성 셀 범위를 설정합니다"></p>

```go
f.SetPanes("Sheet1", `{
    "freeze": true,
    "split": false,
    "x_split": 0,
    "y_split": 9,
    "top_left_cell": "A34",
    "active_pane": "bottomLeft",
    "panes": [
    {
        "sqref": "A11:XFD11",
        "active_cell": "A11",
        "pane": "bottomLeft"
    }]
}`)
```

예 3: `Sheet1` 에서 분할 창을 만들고 `Sheet1!J60` 에서 활성 셀을 설정합니다:

<p align="center"><img width="775" src="./images/setpans_03.png" alt="분할 창 만들기"></p>

```go
f.SetPanes("Sheet1", `{
    "freeze": false,
    "split": true,
    "x_split": 3270,
    "y_split": 1800,
    "top_left_cell": "N57",
    "active_pane": "bottomLeft",
    "panes": [
    {
        "sqref": "I36",
        "active_cell": "I36"
    },
    {
        "sqref": "G33",
        "active_cell": "G33",
        "pane": "topRight"
    },
    {
        "sqref": "J60",
        "active_cell": "J60",
        "pane": "bottomLeft"
    },
    {
        "sqref": "O60",
        "active_cell": "O60",
        "pane": "bottomRight"
    }]
}`)
```

예 4, 고정을 해제 하 고 `Sheet1` 에 있는 모든 창을 제거:

```go
f.SetPanes("Sheet1", `{"freeze":false,"split":false}`)
```

## 색상 값 계산 {#ThemeColor}

```go
func ThemeColor(baseColor string, tint float64) string
```

ThemeColor 는 색조 값으로 색상을 적용했습니다:

```go
package main

import (
    "fmt"
    "strings"

    "github.com/360EntSecGroup-Skylar/excelize/v2"
)

func main() {
    f, err := excelize.OpenFile("Book1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(getCellBgColor(f, "Sheet1", "A1"))
}

func getCellBgColor(f *excelize.File, sheet, axix string) string {
    styleID, err := f.GetCellStyle(sheet, axix)
    if err != nil {
        return err.Error()
    }
    fillID := *f.Styles.CellXfs.Xf[styleID].FillID
    fgColor := f.Styles.Fills.Fill[fillID].PatternFill.FgColor
    if fgColor.Theme != nil {
        children := f.Theme.ThemeElements.ClrScheme.Children
        if *fgColor.Theme < 4 {
            dklt := map[int]string{
                0: children[1].SysClr.LastClr,
                1: children[0].SysClr.LastClr,
                2: *children[3].SrgbClr.Val,
                3: *children[2].SrgbClr.Val,
            }
            return strings.TrimPrefix(
                excelize.ThemeColor(dklt[*fgColor.Theme], fgColor.Tint), "FF")
        }
        srgbClr := *children[*fgColor.Theme].SrgbClr.Val
        return strings.TrimPrefix(excelize.ThemeColor(srgbClr, fgColor.Tint), "FF")
    }
    return strings.TrimPrefix(fgColor.RGB, "FF")
}
```

## RGB 를 HSL 로 변환 {#RGBToHSL}

```go
func RGBToHSL(r, g, b uint8) (h, s, l float64)
```

RGBToHSL 은 RGB 트리플을 HSL 트리플로 변환합니다.

## HSL 을 RGB 로 변환 {#HSLToRGB}

```go
func HSLToRGB(h, s, l float64) (r, g, b uint8)
```

HSLToRGB 는 HSL 트리플을 RGB 트리플로 변환합니다.

## 파일 작성자 {#FileWriter}

### Write {#Write}

```go
func (f *File) Write(w io.Writer) error
```

쓰기는 `io.Writer` 에 쓸 수 있는 함수를 제공합니다.

### WriteTo {#WriteTo}

```go
func (f *File) WriteTo(w io.Writer) (int64, error)
```

WriteTo 파일을 작성 하는 `io.WriterTo` 를 구현 합니다.

### WriteToBuffer {#WriteToBuffer}

```go
func (f *File) WriteToBuffer() (*bytes.Buffer, error)
```

WriteToBuffer 저장 된 파일에서 `*bytes.Buffer` 를 얻을 수 있는 함수를 제공 합니다.

## VBA 프로젝트 추가 {#AddVBAProject}

```go
func (f *File) AddVBAProject(bin string) error
```

AddVBAProject 는 함수 및/또는 매크로를 포함하는 `vbaProject.bin` 파일을 추가하는 방법을 제공합니다. 파일 확장은 `.xlsm` 이어야 합니다. 예를 들어:

```go
if err := f.SetSheetPrOptions("Sheet1", excelize.CodeName("Sheet1")); err != nil {
    fmt.Println(err)
}
if err := f.AddVBAProject("vbaProject.bin"); err != nil {
    fmt.Println(err)
}
if err := f.SaveAs("macros.xlsm"); err != nil {
    fmt.Println(err)
}
```

## Excel 날짜를 시간으로 변환 {#ExcelDateToTime}

```go
func ExcelDateToTime(excelDate float64, use1904Format bool) (time.Time, error)
```

ExcelDateToTime 은 `float` 기반 Excel 날짜 표현을 `time.Time` 으로 변환합니다.

## 문자셋 트랜스 코더 {#CharsetTranscoder}

```go
func (f *File) CharsetTranscoder(fn charsetTranscoderFn) *File
```

CharsetTranscoder UTF-8 이외의 인코딩에서 열린 XLSX에 대한 사용자 정의 코드 페이지 트랜스 코더 기능을 설정합니다.
