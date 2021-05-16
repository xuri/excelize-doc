# 스트리밍 쓰기

StreamWriter 는 스트림 작성기 유형을 정의했습니다.

```go
type StreamWriter struct {
    File    *File
    Sheet   string
    SheetID int
    // 필터링되거나 내 보내지 않은 필드를 포함합니다
}
```

Cell 은 StreamWriter.SetRow 에서 직접 사용하여 스타일과 값을 지정할 수 있습니다.

```go
type Cell struct {
    StyleID int
    Formula string
    Value   interface{}
}
```

## 스트림 라이터 받기 {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter 는 주어진 워크 시트 이름으로 스트림 기록기를 반환하여 대량의 데이터가 포함 된 새 워크 시트를 생성합니다. 행을 설정 한 후 스트리밍 쓰기 프로세스를 종료하고 행 번호 순서가 오름차순이되도록 [`Flush`](stream.md#Flush) 메소드를 호출해야합니다. 워크 시트에 데이터를 쓰기 위해 일반 API를 스트리밍 API와 혼합 할 수 없습니다. 예를 들어, 크기가 `102400` 행 x `50` 열인 워크 시트의 데이터를 숫자로 설정하십시오:

```go
file := excelize.NewFile()
streamWriter, err := file.NewStreamWriter("Sheet1")
if err != nil {
    fmt.Println(err)
}
styleID, err := file.NewStyle(`{"font":{"color":"#777777"}}`)
if err != nil {
    fmt.Println(err)
}
if err := streamWriter.SetRow("A1", []interface{}{
    excelize.Cell{StyleID: styleID, Value: "Data"}}); err != nil {
    fmt.Println(err)
}
for rowID := 2; rowID <= 102400; rowID++ {
    row := make([]interface{}, 50)
    for colID := 0; colID < 50; colID++ {
        row[colID] = rand.Intn(640000)
    }
    cell, _ := excelize.CoordinatesToCellName(1, rowID)
    if err := streamWriter.SetRow(cell, row); err != nil {
        fmt.Println(err)
    }
}
if err := streamWriter.Flush(); err != nil {
    fmt.Println(err)
}
if err := file.SaveAs("Book1.xlsx"); err != nil {
    fmt.Println(err)
}
```

스트림 작성기를 사용하여 워크 시트의 셀 값 및 셀 수식을 설정합니다:

```go
err := streamWriter.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1},
    excelize.Cell{Value: 2},
    excelize.Cell{Formula: "SUM(A1,B1)"}});
```

## 스트리밍 할 시트 행 쓰기 {#SetRow}

```go
func (sw *StreamWriter) SetRow(axis string, slice interface{}) error
```

SetRow 는 지정된 시작 좌표와 배열 유형 `slice` 에 대한 포인터를 사용하여 워크시트에 행으로 데이터를 스트리밍합니다. 행을 설정한 후에는 [`Flush`](stream.md#Flush) 함수를 호출하여 스트리밍 쓰기 프로세스를 종료해야 하며 기록된 줄 번호가 증가해야 합니다.

## 테이블을 스트리밍합니다 {#AddTable}

```go
func (sw *StreamWriter) AddTable(hcell, vcell, format string) error
```

지정된 셀 좌표 범위 및 조건부 서식을 기반으로 테이블을 만듭니다.

예 1, `A1:D5` 영역에서 테이블을 스트리밍합니다:

```go
err := streamWriter.AddTable("A1", "D5", "")
```

예 2, 워크시트 `F2:H6` 영역에 조건부 형식의 테이블을 만듭니다:

```go
err := streamWriter.AddTable("F2", "H6", `{
    "table_name": "table",
    "table_style": "TableStyleMedium2",
    "show_first_column": true,
    "show_last_column": true,
    "show_row_stripes": false,
    "show_column_stripes": true
}`)
```

테이블 좌표 영역은 문자 유형의 제목 줄과 콘텐츠 줄의 두 개 이상의 줄을 덮어씁니다. 각 머리글 행의 문자는 고유해야 하며 현재 각 워크시트에서 하나의 테이블만 스트리밍할 수 있으며 함수를 호출하기 전에 [`SetRow`](stream.md#SetRow) 를 통해 테이블의 머리글 행 데이터를 스트리밍해야 합니다. 지원되는 테이블 스타일은 비스트리밍 테이블 만들기 [`AddTable`](utils.md#AddTable) 과 동일합니다.

## 셀을 스트리밍병합합니다 {#MergeCell}

```go
func (sw *StreamWriter) MergeCell(hcell, vcell string) error
```

지정된 셀 좌표 범위 스트리밍병합 셀을 통해 현재 겹침이 아닌 범위 셀만 병합할 수 있습니다.

## 스트림에서 열 너비 설정 {#SetColWidth}

```go
func (sw *StreamWriter) SetColWidth(min, max int, width float64) error
```

SetColWidth 는 `StreamWriter` 에 대한 단일 열 또는 여러 열의 너비를 설정하는 함수를 제공합니다. [`SetRow`](stream.md#SetRow) 함수 전에 `SetColWidth` 함수를 호출해야 합니다. 예를 들어 너비 열 `B:C` 를 `20` 으로 설정합니다:

```go
err := streamWriter.SetColWidth(2, 3, 20)
```

## 플러시 스트림 {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush ending the streaming writing process.
