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

## 스트리밍 할 시트 행 쓰기 {#SetRow}

```go
func (sw *StreamWriter) SetRow(axis string, slice interface{}) error
```

SetRow 는 주어진 워크 시트 이름, 시작 좌표 및 배열 유형 `slice` 에 대한 포인터로 행을 스트림에 배열을 기록합니다. 스트리밍 쓰기 프로세스를 끝내려면 [`Flush`](stream.md#Flush) 메소드를 호출해야합니다.

## 플러시 스트림 {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush ending the streaming writing process.
