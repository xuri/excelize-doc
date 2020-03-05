# 資料

## 資料驗證 {#AddDataValidation}

```go
func (f *File) AddDataValidation(sheet string, dv *DataValidation)
```

根據給定的工作表名和資料驗證對象設置資料驗證規則，資料驗證對象可通過 `NewDataValidation` 函數創建，資料驗證類別和條件參考[常量](constants.md)中的定義。

例1，為 `Sheet1!A1:B2` 設置包含驗證條件為允許介於整數 10 到 20 的資料驗證規則，輸入無效資料時顯示出錯警告，標題為: "error title"，錯誤信息 "error body":

<p align="center"><img width="654" src="./images/data_validation_01.png" alt="資料驗證"></p>

```go
dvRange := excelize.NewDataValidation(true)
dvRange.Sqref = "A1:B2"
dvRange.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorBetween)
dvRange.SetError(excelize.DataValidationErrorStyleStop, "error title", "error body")
f.AddDataValidation("Sheet1", dvRange)
```

例2，為 `Sheet1!A3:B4` 設置包含驗證條件為允許大於整數 10 的資料驗證規則，選定儲存格時顯示輸入信息，輸入信息為: "input body":

<p align="center"><img width="654" src="./images/data_validation_02.png" alt="資料驗證"></p>

```go
dvRange = excelize.NewDataValidation(true)
dvRange.Sqref = "A3:B4"
dvRange.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorGreaterThan)
dvRange.SetInput("input title", "input body")
f.AddDataValidation("Sheet1", dvRange)
```

例3，為 `Sheet1!A5:B6` 設置驗證條件為序列的資料驗證規則，忽略空值並提供下拉箭頭:

<p align="center"><img width="654" src="./images/data_validation_03.png" alt="資料驗證"></p>

```go
dvRange = excelize.NewDataValidation(true)
dvRange.Sqref = "A5:B6"
dvRange.SetDropList([]string{"1", "2", "3"})
f.AddDataValidation("Sheet1", dvRange)
```

例4，為 `Sheet1!A7:B8` 設置以 `Sheet1!E1:E3` 為來源的驗證條件，忽略空值並提供下拉箭頭:

<p align="center"><img width="654" src="./images/data_validation_04.png" alt="資料驗證"></p>

```go
dvRange := excelize.NewDataValidation(true)
dvRange.Sqref = "A7:B8"
dvRange.SetSqrefDropList("$E$1:$E$3", true)
f.AddDataValidation("Sheet1", dvRange)
```
