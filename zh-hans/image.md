# 图片

## 插入图片 {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture, format string) error
```

根据给定的工作表名称、单元格坐标、图片地址和图片格式（例如偏移、缩放和打印设置等），在对应的单元格上插入图片。

例如：

```go
package main

import (
    "fmt"
    _ "image/gif"
    _ "image/jpeg"
    _ "image/png"

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    f := excelize.NewFile()
    // 插入图片
    err := f.AddPicture("Sheet1", "A2", "./image1.jpg", "")
    if err != nil {
        fmt.Println(err)
    }
    // 插入带有缩放比例和超链接的图片
    err = f.AddPicture("Sheet1", "D2", "./image1.png", `{"x_scale": 0.5, "y_scale": 0.5, "hyperlink": "#Sheet2!D8", "hyperlink_type": "Location"}`)
    if err != nil {
        fmt.Println(err)
    }
    // 插入图片，并设置图片的外部超链接、打印和位置属性
    err = f.AddPicture("Sheet1", "H2", "./image3.gif", `{"x_offset": 15, "y_offset": 10, "hyperlink": "https://github.com/360EntSecGroup-Skylar/excelize", "hyperlink_type": "External", "print_obj": true, "lock_aspect_ratio": false, "locked": false, "positioning": "oneCell"}`)
    if err != nil {
        fmt.Println(err)
    }
    err = f.SaveAs("./Book1.xlsx")
    if err != nil {
        fmt.Println(err)
    }
}
```

链接类型 `hyperlink_type` 支持外部链接 `External` 和内部链接 `Location` 两种类型，当使用 `Location` 连接到单元格位置时，坐标需要以 `#` 开始。

位置属性 `positioning` 支持 `oneCell`（大小固定，位置随单元格改变）和 `absolute` （大小、位置均固定）两种类型，当不设置此参数时，默认属性为大小、位置随单元格而改变。

```go
func (f *File) AddPictureFromBytes(sheet, cell, format, name, extension string, file []byte) error
```

根据给定的工作表名称、单元格坐标、图片地址和图片格式（例如偏移、缩放和打印设置等）、图片描述、图片扩展名和 `[]byte` 类型的图片内容，在对应的单元格上插入图片。

例如：

```go
package main

import (
    "fmt"
    _ "image/jpeg"
    "io/ioutil"

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    f := excelize.NewFile()

    file, err := ioutil.ReadFile("./image1.jpg")
    if err != nil {
        fmt.Println(err)
    }
    err = f.AddPictureFromBytes("Sheet1", "A2", "", "Excel Logo", ".jpg", file)
    if err != nil {
        fmt.Println(err)
    }
    err = f.SaveAs("./Book1.xlsx")
    if err != nil {
        fmt.Println(err)
    }
}
```

## 获取图片 {#GetPicture}

```go
func (f *File) GetPicture(sheet, cell string) (string, []byte, error)
```

根据给定的工作表名称（大小写敏感）和单元格坐标获取工作簿上的图片，将以 `[]byte` 类型返回嵌入在 Excel 文档中的图片。例如，获取名为 `Sheet1` 的工作表上 `A2` 单元格上的图片：

```go
f, err := excelize.OpenFile("./Book1.xlsx")
if err != nil {
    fmt.Println(err)
    return
}
file, raw, err := f.GetPicture("Sheet1", "A2")
if err != nil {
    fmt.Println(err)
    return
}
err = ioutil.WriteFile(file, raw, 0644)
if err != nil {
    fmt.Println(err)
}
```