# 快速開始

{{ book.info }}

## 安裝 {#install}

下表列出了各版本 Excelize 基礎庫對 Go 語言版本最低要求的情況：

Excelize 版本 | 對 Go 語言版本的最低要求
---|---
master | 1.23
v2.8.1 ~ v2.9.0 | 1.18
v2.7.0 ~ v2.8.0 | 1.16
v2.4.0 ~ v2.6.1 | 1.15
v2.0.2 ~ v2.3.2 | 1.10
v1.0.0 ~ v2.0.1 | 1.6

使用最新版本 Excelize 要求您使用的 Go 語言為 1.20 或更高版本。請注意，Go 1.21.0 中存在[不兼容的更改](https://github.com/golang/go/issues/61881)，導致 Excelize 基礎庫無法在該版本上正常工作，如果您使用的是 Go 1.21.x，請升級到 Go 1.21.1 及更高版本。

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

## 創建 Excel 檔案 {#NewFile}

下面是一個創建 Excel 檔案的簡單例子：

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

## 讀取 Excel 檔案 {#read}

下面是讀取 Excel 檔案的例子：

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

## 在 Excel 檔案中創建圖表 {#chart}

使用 Excelize 生成圖表十分簡單，僅需幾行代碼。您可以根據工作表中的已有資料構建圖表，或向工作表中添加資料並創建圖表。

<p align="center"><img width="770" src="../images/base.png" alt="在 Excel 檔案中創建圖表"></p>

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
        Type: excelize.Col3DClustered,
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
        Title: []excelize.RichTextRun{
            {
                Text: "立體群組直條圖",
            },
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

## 向 Excel 檔案中插入圖片 {#image}

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
    // 在工作表中插入圖片，並設定圖片的列印屬性
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
