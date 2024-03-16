# 图片

## 插入图片 {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture string, opts *GraphicOptions) error
```

根据给定的工作表名称、单元格坐标、图片地址和图片格式（例如偏移、缩放和打印设置等），在对应的单元格上插入图片。此功能是并发安全的。

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
    // 插入图片
    if err := f.AddPicture("Sheet1", "A2", "image.png", nil); err != nil {
        fmt.Println(err)
        return
    }
    // 插入带有缩放比例和超链接的图片
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
    // 插入图片，并设置图片的外部超链接、打印和位置属性
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

可选参数 `AltText` 用以指定图形对象的可选文字。

可选参数 `PrintObject` 指定打印工作表时是否打印图形对象，其默认值为 `true`。

可选参数 `Locked` 指定是否锁定图形对象。除非工作表受到保护，否则锁定对象无效。

可选参数 `LockAspectRatio` 指定是否锁定图形对象的纵横比，其默认值为 `false。`

可选参数 `AutoFit` 用以指定是否使图形对象尺寸自动适合单元格，其默认值为 `false`。

可选参数 `OffsetX` 指定图形对象与插入单元格的水平偏移量，其默认值为 0。

可选参数 `OffsetY` 指定图形对象与插入单元格的垂直偏移量，其默认值为 0。

可选参数 `ScaleX` 指定图形对象的水平缩放比例，默认值为 1.0，表示 100%。

可选参数 `ScaleY` 指定图形对象的垂直缩放比例，其默认值为 1.0，表示 100%。

可选参数 `Hyperlink` 用以指定图形对象的超链接。

可选参数 `HyperlinkType` 指定图形对象超链接的类型，支持外部链接 `External` 和内部链接 `Location` 两种类型，当使用 `Location` 连接到单元格位置时，坐标需要以 `#` 开始。

可选参数 `Positioning` 定义了电子表格中图形对象位置属性的 3 种类型：`oneCell`（大小固定，位置随单元格改变）、`twoCell`（大小和位置随单元格改变）和 `absolute` （大小、位置均固定）两种类型，当不设置此参数时，默认属性为大小、位置随单元格改变。

```go
func (f *File) AddPictureFromBytes(sheet, cell string, pic *Picture) error
```

根据给定的工作表名称、单元格坐标、图片地址和图片格式（例如偏移、缩放和打印设置等）、图片描述、图片扩展名和 `[]byte` 类型的图片内容，在对应的单元格上插入图片。

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

## 获取图片 {#GetPicture}

```go
func (f *File) GetPictures(sheet, cell string) ([]Picture, error)
```

根据给定的工作表名称和单元格坐标获取工作簿上的图片，将以 `[]byte` 类型返回嵌入在 Excel 文档中的图片。此功能是并发安全的。例如，获取名为 `Sheet1` 的工作表上 `A2` 单元格上的图片：

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

## 删除图片 {#DeletePicture}

```go
func (f *File) DeletePicture(sheet, cell string) error
```

根据给定的工作表名称和单元格坐标，删除对应单元格上的图片。
