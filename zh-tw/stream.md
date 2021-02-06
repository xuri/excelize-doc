# 流式寫入

StreamWriter 用於定義流式寫入器的資料類別。

```go
type StreamWriter struct {
    File    *File
    Sheet   string
    SheetID int
    // 還包含其他已過濾或未導出的欄位
}
```

## 獲取流式寫入器 {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter 通過給定的工作表名稱傳回流式寫入器，用於生成包含大規模資料的工作表。請注意通過此方法按行向工作表寫入資料後，必須調用 [`Flush`](stream.md#Flush) 函數來結束流式寫入過程，並需要確所保寫入的行號是遞增的，普通 API 不能與流式 API 混合使用在工作表中寫入資料。例如，向工作表流式按行寫入 `102400` 行 x `50` 列帶有樣式的數據：

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

## 按行流式寫入工作表 {#SetRow}

```go
func (sw *StreamWriter) SetRow(axis string, slice interface{}) error
```

SetRow 通過給定的工作表名稱、起始坐標和指向數組類別「切片」的指針將資料按行流式寫入工作表中。請注意，在設定行之後，必須調用 [`Flush`](stream.md#Flush) 函數來結束流式寫入過程，並需要確所保寫入的行號是遞增的。

## 結束流式寫入 {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush 用於結束流式寫入過程。
