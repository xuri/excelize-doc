# 快速開始

## 安裝 {#install}

使用最新版本 Excelize 要求您使用的 Go 語言為 1.15 或更高版本。

- 安裝命令

```bash
go get github.com/xuri/excelize
```

- 如果您使用 [Go Modules](https://go.dev/blog/using-go-modules) 管理軟體包，請使用下面的命令來安裝最新版本。

```bash
go get github.com/xuri/excelize/v2
```

## 更新 {#update}

- 更新命令

```bash
go get -u github.com/xuri/excelize/v2
```

## 創建 Excel 文檔 {#NewFile}

下面是一個創建 Excel 文檔的簡單例子：

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
    // 創建一個工作表
    index, err := f.NewSheet("Sheet2")
    if err != nil {
        fmt.Println(err)
        return
    }
    // 設定儲存格的值
    f.SetCellValue("Sheet2", "A2", "Hello world.")
    f.SetCellValue("Sheet1", "B2", 100)
    // 設定活頁簿的默認工作表
    f.SetActiveSheet(index)
    // 根據指定路徑儲存檔案
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## 讀取 Excel 文檔 {#read}

下面是讀取 Excel 文檔的例子：

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f, err := excelize.OpenFile("Book1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    // 獲取工作表中指定儲存格的值
    cell, err := f.GetCellValue("Sheet1", "B2")
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(cell)
    // 獲取 Sheet1 上所有儲存格
    rows, err := f.GetRows("Sheet1")
    if err != nil {
        fmt.Println(err)
        return
    }
    for _, row := range rows {
        for _, colCell := range row {
            fmt.Print(colCell, "\t")
        }
        fmt.Println()
    }
}
```

## 在 Excel 文檔中創建圖表 {#chart}

使用 Excelize 生成圖表十分簡單，僅需幾行代碼。您可以根據工作表中的已有資料構建圖表，或向工作表中添加資料並創建圖表。

<p align="center"><img width="770" src="../images/base.png" alt="在 Excel 文檔中創建圖表"></p>

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
        {nil, "Apple", "Orange", "Pear"}, {"Small", 2, 3, 3},
        {"Normal", 5, 2, 4}, {"Large", 6, 7, 8},
    } {
        cell, err := excelize.CoordinatesToCellName(1, idx+1)
        if err != nil {
            fmt.Println(err)
            return
        }
        f.SetSheetRow("Sheet1", cell, &row)
    }
    if err := f.AddChart("Sheet1", "E1", &excelize.Chart{
        Type: "col3DClustered",
        Series: []excelize.ChartSeries{
            {
                Name:       "Sheet1!$A$2",
                Categories: "Sheet1!$B$1:$D$1",
                Values:     "Sheet1!$B$2:$D$2",
            },
            {
                Name:       "Sheet1!$A$3",
                Categories: "Sheet1!$B$1:$D$1",
                Values:     "Sheet1!$B$3:$D$3",
            },
            {
                Name:       "Sheet1!$A$4",
                Categories: "Sheet1!$B$1:$D$1",
                Values:     "Sheet1!$B$4:$D$4",
            }},
        Title: excelize.ChartTitle{
            Name: "立體群組直條圖",
        },
    }); err != nil {
        fmt.Println(err)
        return
    }
    // 根據指定路徑儲存檔案
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## 向 Excel 文檔中插入圖片 {#image}

```go
package main

import (
    "fmt"
    _ "image/gif"
    _ "image/jpeg"
    _ "image/png"
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f, err := excelize.OpenFile("Book1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    // 插入圖片
    if err := f.AddPicture("Sheet1", "A2", "image.png", nil); err != nil {
        fmt.Println(err)
        return
    }
    // 在工作表中插入圖片，並設定圖片的縮放比例
    if err := f.AddPicture("Sheet1", "D2", "image.jpg",
        &excelize.GraphicOptions{ScaleX: 0.5, ScaleY: 0.5}); err != nil {
        fmt.Println(err)
        return
    }
    // 在工作表中插入圖片，並設定圖片的打印屬性
    enable, disable := true, false
    if err := f.AddPicture("Sheet1", "H2", "image.gif",
        &excelize.GraphicOptions{
            PrintObject:     &enable,
            LockAspectRatio: false,
            OffsetX:         15,
            OffsetY:         10,
            Locked:          &disable,
        }); err != nil {
        fmt.Println(err)
        return
    }
    // 儲存檔案
    if err = f.Save(); err != nil {
        fmt.Println(err)
    }
}
```
