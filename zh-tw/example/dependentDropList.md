# 級聯列表

{{ book.info }}

使用 Go 語言在 Excel 檔案中創建多級聯動菜單列表:

<p align="center"><img width="375" src="../images/dependent_drop_list.gif" alt="使用 Go 語言在 Excel 檔案中創建多級聯動菜單列表"></p>

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    // 創建活頁簿
    f := excelize.NewFile()
    var (
        // 定義儲存格的值
        data = [][]interface{}{
            {"Fruits", "Vegetables"},
            {"Mango", "Potato", nil, "Drop Down 1", "Drop Down 2"},
            {"Apple", "Tomato"},
            {"Grapes", "Spinach"},
            {"Strawberry", "Onion"},
            {"Kiwi", "Cucumber"},
        }
        addr                    string
        err                     error
        cellsStyle, headerStyle int
    )
    // 按列賦值
    for r, row := range data {
        if addr, err = excelize.JoinCellName("A", r+1); err != nil {
            fmt.Println(err)
            return
        }
        if err = f.SetSheetRow("Sheet1", addr, &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    // 設定數據驗證
    dvRange1 := excelize.NewDataValidation(true)
    dvRange1.Sqref = "D3:D3"
    dvRange1.SetSqrefDropList("$A$1:$B$1")
    if err = f.AddDataValidation("Sheet1", dvRange1); err != nil {
        fmt.Println(err)
        return
    }
    dvRange2 := excelize.NewDataValidation(true)
    dvRange2.Sqref = "E3:E3"
    dvRange2.SetSqrefDropList("INDIRECT(D3)")
    if err = f.AddDataValidation("Sheet1", dvRange2); err != nil {
        fmt.Println(err)
        return
    }
    // 設定自訂名稱
    if err = f.SetDefinedName(&excelize.DefinedName{
        Name:     "Fruits",
        RefersTo: "Sheet1!$A$2:$A$6",
        Scope:    "Sheet1",
    }); err != nil {
        fmt.Println(err)
        return
    }
    if err = f.SetDefinedName(&excelize.DefinedName{
        Name:     "Vegetables",
        RefersTo: "Sheet1!$B$2:$B$6",
        Scope:    "Sheet1",
    }); err != nil {
        fmt.Println(err)
        return
    }
    // 自訂欄寬
    for col, width := range map[string]float64{
        "A": 12, "B": 12, "C": 6, "D": 12, "E": 12} {
        if err = f.SetColWidth("Sheet1", col, col, width); err != nil {
            fmt.Println(err)
            return
        }
    }
    // 隱藏工作表網格線
    disable := false
    if err := f.SetSheetView("Sheet1", -1, &excelize.ViewOptions{
        ShowGridLines: &disable,
    }); err != nil {
        fmt.Println(err)
    }
    // 定義外框樣式
    border := []excelize.Border{
        {Type: "top", Style: 1, Color: "cccccc"},
        {Type: "left", Style: 1, Color: "cccccc"},
        {Type: "right", Style: 1, Color: "cccccc"},
        {Type: "bottom", Style: 1, Color: "cccccc"},
    }
    // 定義儲存格樣式
    if cellsStyle, err = f.NewStyle(&excelize.Style{
        Font:   &excelize.Font{Color: "333333"},
        Border: border}); err != nil {
        fmt.Println(err)
        return
    }
    // 定義標題欄儲存格樣式
    if headerStyle, err = f.NewStyle(&excelize.Style{
        Font: &excelize.Font{Bold: true},
        Fill: excelize.Fill{
            Type: "pattern", Color: []string{"dae9f3"}, Pattern: 1},
        Border: border},
    ); err != nil {
        fmt.Println(err)
        return
    }
    // 為儲存格設定樣式
    if err = f.SetCellStyle("Sheet1", "A2", "B6", cellsStyle); err != nil {
        fmt.Println(err)
        return
    }
    if err = f.SetCellStyle("Sheet1", "D3", "E3", cellsStyle); err != nil {
        fmt.Println(err)
        return
    }
    // 為標題列設定樣式
    if err = f.SetCellStyle("Sheet1", "A1", "B1", headerStyle); err != nil {
        fmt.Println(err)
        return
    }
    if err = f.SetCellStyle("Sheet1", "D2", "E2", headerStyle); err != nil {
        fmt.Println(err)
        return
    }
    // 保存活頁簿
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```
