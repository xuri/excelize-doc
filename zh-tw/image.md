# 圖片

{{ book.info }}

## 插入圖片 {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture string, opts *GraphicOptions) error
```

根據給定的工作表名稱、儲存格坐標、圖片地址和圖片格式（例如偏移、縮放和列印設定等），在對應的儲存格上插入圖片。此功能是併發安全的。

例如：

```go
package main

import (
    "fmt"
    _ "image/gif"
    _ "image/jpeg"
    _ "image/png"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
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
    // 插入帶有縮放比例和超鏈接的圖片
    enable, disable := true, false
    if err := f.AddPicture("Sheet1", "D2", "image.jpg",
        &excelize.GraphicOptions{
            ScaleX:        0.5,
            ScaleY:        0.5,
            Hyperlink:     "#Sheet2!D8",
            HyperlinkType: "Location",
        },
    ); err != nil {
        fmt.Println(err)
        return
    }
    // 插入圖片，並設定圖片的外部超鏈接、列印和位置屬性
    if err := f.AddPicture("Sheet1", "H2", "image.gif",
        &excelize.GraphicOptions{
            OffsetX:         15,
            OffsetY:         10,
            Hyperlink:       "https://github.com/xuri/excelize",
            HyperlinkType:   "External",
            PrintObject:     &enable,
            LockAspectRatio: false,
            Locked:          &disable,
            Positioning:     "oneCell",
        },
    ); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

可選參數 `AltText` 設定圖形對象的可選文字。

可選參數 `PrintObject` 設定列印工作表時是否列印圖形對象，其缺省值為 `true`。

可選參數 `Locked` 設定是否鎖定圖形對象。除非工作表受到保護，否則鎖定對象無效。

可選參數 `LockAspectRatio` 設定是否鎖定圖形對象的縱橫比，其缺省值為 `false`。

可選參數 `AutoFit` 設定是否使圖形對象尺寸自動適合儲存格，其缺省值為 `false`。

可選參數 `OffsetX` 設定圖形對象與插入儲存格的水平偏移量，其缺省值為 0。

可選參數 `OffsetY` 設定圖形對象與插入儲存格的垂直偏移量，缺省值為 0。

可選參數 `ScaleX` 設定圖形對象的水平縮放比例，其缺省值為 1.0，表示 100%。

可選參數 `ScaleY` 設定圖形對象的垂直縮放比例，其缺省值為 1.0，表示 100%。

可選參數 `Hyperlink` 用以設定圖形對象的超鏈接。

可選參數 `HyperlinkType` 設定圖形對象超鏈接的類型，支援外部鏈接 `External` 和內部鏈接 `Location` 兩種類型，當使用 `Location` 連接到儲存格位置時，坐標需要以 `#` 開始。

可選參數 `Positioning` 定義了電子錶格中圖形對象位置屬性的 3 種類型：`oneCell`（大小固定，位置隨儲存格改變）、`twoCell`（大小和位置隨儲存格改變）和 `absolute` （大小、位置均固定）兩種類型，當不設定此參數時，默認屬性為大小、位置隨儲存格改變。

```go
func (f *File) AddPictureFromBytes(sheet, cell string, pic *Picture) error
```

根據給定的工作表名稱、儲存格坐標、圖片地址和圖片格式（例如偏移、縮放和列印設定等）、圖片描述、圖片擴展名和 `[]byte` 類別的圖片內容，在對應的儲存格上插入圖片。

例如：

```go
package main

import (
    "fmt"
    _ "image/jpeg"
    "os"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    file, err := os.ReadFile("image.jpg")
    if err != nil {
        fmt.Println(err)
        return
    }
    if err := f.AddPictureFromBytes("Sheet1", "A2", &excelize.Picture{
        Extension: ".jpg",
        File:      file,
        Format:    &excelize.GraphicOptions{AltText: "Excel Logo"},
    }); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## 獲取圖片 {#GetPicture}

```go
func (f *File) GetPictures(sheet, cell string) ([]Picture, error)
```

根據給定的工作表名稱和儲存格坐標獲取活頁簿上的圖片，將以 `[]byte` 類別傳回嵌入在 Excel 檔案中的圖片。此功能是併發安全的。例如，獲取名為 `Sheet1` 的工作表上 `A2` 儲存格上的圖片：

```go
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
pics, err := f.GetPictures("Sheet1", "A2")
if err != nil {
    fmt.Println(err)
}
for idx, pic := range pics {
    name := fmt.Sprintf("image%d%s", idx+1, pic.Extension)
    if err := os.WriteFile(name, pic.File, 0644); err != nil {
        fmt.Println(err)
    }
}
```

## 刪除圖片 {#DeletePicture}

```go
func (f *File) DeletePicture(sheet, cell string) error
```

根據給定的工作表名稱和儲存格坐標，刪除對應儲存格上的圖片。
