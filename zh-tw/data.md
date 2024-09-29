# 資料

{{ book.info }}

## 添加資料驗證 {#AddDataValidation}

```go
func (f *File) AddDataValidation(sheet string, dv *DataValidation)
```

根據給定的工作表名和資料驗證對象設定資料驗證規則，資料驗證對象可透過 `NewDataValidation` 函式創建，資料驗證類別和條件參考[常量](constants.md)中的定義。

例1，為 `Sheet1!A1:B2` 設定包含驗證條件為允許介於整數 10 到 20 的資料驗證規則，輸入無效資料時顯示出錯警告，標題為: "error title"，錯誤信息 "error body":

<p align="center"><img width="654" src="./images/data_validation_01.png" alt="資料驗證"></p>

```go
dv := excelize.NewDataValidation(true)
dv.SetSqref("A1:B2")
dv.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorBetween)
dv.SetError(excelize.DataValidationErrorStyleStop, "error title", "error body")
f.AddDataValidation("Sheet1", dv)
```

例2，為 `Sheet1!A3:B4` 設定包含驗證條件為允許大於整數 10 的資料驗證規則，選定儲存格時顯示輸入信息，輸入信息為: "input body":

<p align="center"><img width="654" src="./images/data_validation_02.png" alt="資料驗證"></p>

```go
dv = excelize.NewDataValidation(true)
dv.SetSqref("A3:B4")
dv.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorGreaterThan)
dv.SetInput("input title", "input body")
f.AddDataValidation("Sheet1", dv)
```

例3，為 `Sheet1!A5:B6` 設定驗證條件為序列的資料驗證規則，忽略空值並提供下拉箭頭:

<p align="center"><img width="654" src="./images/data_validation_03.png" alt="資料驗證"></p>

```go
dv = excelize.NewDataValidation(true)
dv.SetSqref("A5:B6")
dv.SetDropList([]string{"1", "2", "3"})
f.AddDataValidation("Sheet1", dv)
```

如果您在序列中設定的項目超過限制累計 255 個字符的限制，請使用另一種方式設定：在工作表存儲格中設定允許的值，並使用 `SetSqrefDropList` 函數設定序列中引用存儲格的範圍。

例4，為 `Sheet1!A7:B8` 設定以 `Sheet1!E1:E3` 為來源的驗證條件，忽略空值並提供下拉箭頭:

<p align="center"><img width="654" src="./images/data_validation_04.png" alt="資料驗證"></p>

```go
dv := excelize.NewDataValidation(true)
dv.SetSqref("A7:B8")
dv.SetSqrefDropList("E1:E3")
f.AddDataValidation("Sheet1", dv)
```

資料驗證下拉列表中顯示的項目數量有限制：該列表最多可以顯示 32768 個項目。如果您需要更多項目，可以透過級聯列表將項目分類。

## 獲取資料驗證 {#GetDataValidations}

```go
func (f *File) GetDataValidations(sheet string) ([]*DataValidation, error)
```

根據給定的工作表名獲取改工作表中全部資料驗證區域和資料驗證規則。

## 刪除資料驗證 {#DeleteDataValidation}

```go
func (f *File) DeleteDataValidation(sheet string, sqref ...string) error
```

根據給定的工作表名和資料驗證區域刪除資料驗證規則。若未指定資料驗證區域，將刪除給定工作表中全部資料驗證區規則。

## 添加交叉分析篩選器 {#AddSlicer}

`SlicerOptions` 定義了交叉分析篩選器的屬性。

```go
type SlicerOptions struct {
    Name          string
    Table         string
    Cell          string
    Caption       string
    Macro         string
    Width         uint
    Height        uint
    DisplayHeader *bool
    ItemDesc      bool
    Format        GraphicOptions
}
```

`Name` 為必選參數，用於設定交叉分析篩選器的名稱，必須是工作表中已有表格或數據透視表中字段名稱。

`Table` 為必選參數，用於設定交叉分析篩選器關聯的表格或數據透視表名稱。

`Cell` 為必選參數，用於設定交叉分析篩選器左上角存儲格坐標位置。

`Caption` 為可選參數，用於設定交叉分析篩選器的標題。

`Macro` 為可選參數，用於為交叉分析篩選器設定巨集。當使用該參數設定時，保存活頁簿時的文件擴展名應為 `.xlsm` 或者 `.xltm`。

`Width` 為可選參數，用於為設定交叉分析篩選器的寬度。

`Height` 為可選參數，用於為設定交叉分析篩選器的高度。

`DisplayHeader` 為可選參數，用於設定是否顯示交叉分析篩選器的頁首，默認顯示交叉分析篩選器的頁首。

`ItemDesc` 為可選參數，用於設定使用遞減 (Z-A) 為交叉分析篩選器項目排序，默認設定為 `false`（表示使用遞增）。

`Format` 為可選參數，用於設定交叉分析篩選器的格式（大小和屬性）。

```go
func (f *File) AddSlicer(sheet string, opts *SlicerOptions) error
```

透過給定的工作表名稱和交叉分析篩選器設定，在工作表中添加交叉分析篩選器。例如，在 `Sheet1!E1` 存儲格中，為表格 `Table1` 名為 `Column1` 的列添加交叉分析篩選器:

```go
err := f.AddSlicer("Sheet1", &excelize.SlicerOptions{
    Name:       "Column1",
    Cell:       "E1",
    TableSheet: "Sheet1",
    TableName:  "Table1",
    Caption:    "Column1",
    Width:      200,
    Height:     200,
})
```

## 获取交叉分析篩選器 {#GetSlicers}

```go
func (f *File) GetSlicers(sheet string) ([]SlicerOptions, error)
```

通過給定的工作表名稱獲取指定工作表中的全部交叉分析篩選器。注意，該函數目前尚未支持獲取交叉分析篩選器的高度、寬度和圖形屬性。

## 刪除交叉分析篩選器 {#DeleteSlicer}

```go
func (f *File) DeleteSlicer(name string) error
```

根據給定的交叉分析篩選器名稱刪除指定交叉分析篩選器。
