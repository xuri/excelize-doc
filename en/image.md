# Picture

## Add Picture {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture, format string) error
```

AddPicture provides the method to add a picture to a worksheet by given picture format set (such as offset, scale, aspect ratio setting, and print settings) and file path. This function is concurrency safe.

For example:

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
    // Insert a picture.
    if err := f.AddPicture("Sheet1", "A2", "image.jpg", ""); err != nil {
        fmt.Println(err)
    }
    // Insert a picture scaling in the cell with location hyperlink.
    if err := f.AddPicture("Sheet1", "D2", "image.png", `{
        "x_scale": 0.5,
        "y_scale": 0.5,
        "hyperlink": "#Sheet2!D8",
        "hyperlink_type": "Location"
    }`); err != nil {
        fmt.Println(err)
    }
    // Insert a picture offset in the cell with external hyperlink, printing and positioning support.
    if err := f.AddPicture("Sheet1", "H2", "image.gif", `{
        "x_offset": 15,
        "y_offset": 10,
        "hyperlink": "https://github.com/xuri/excelize",
        "hyperlink_type": "External",
        "print_obj": true,
        "lock_aspect_ratio": false,
        "locked": false,
        "positioning": "oneCell"
    }`); err != nil {
        fmt.Println(err)
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

The optional parameter `autofit` specifies if make image size auto fits the cell, the default value of that is `false`.

The optional parameter `hyperlink` specifies the hyperlink of the image.

The optional parameter `hyperlink_type` defines two types of hyperlink `External` for the website or `Location` for moving to one of the cells in this workbook. When the `hyperlink_type` is `Location`, coordinates need to start with `#`.

The optional parameter `positioning` defines two types of the position of a picture in an Excel spreadsheet, `oneCell` (Move but don't size with cells) or `absolute` (Don't move or size with cells). If you don't set this parameter, the default positioning is move and size with cells.

The optional parameter `print_obj` indicates whether the image is printed when the worksheet is printed, the default value of that is `true`.

The optional parameter `lock_aspect_ratio` indicates whether lock aspect ratio for the image, the default value of that is `false`.

The optional parameter `locked` indicates whether lock the image. Locking an object has no effect unless the sheet is protected.

The optional parameter `x_offset` specifies the horizontal offset of the image with the cell, the default value of that is 0.

The optional parameter `x_scale` specifies the horizontal scale of images, the default value of that is 1.0 which presents 100%.

The optional parameter `y_offset` specifies the vertical offset of the image with the cell, the default value of that is 0.

The optional parameter `y_scale` specifies the vertical scale of images, the default value of that is 1.0 which presents 100%.

```go
func (f *File) AddPictureFromBytes(sheet, cell, format, name, extension string, file []byte) error
```

AddPictureFromBytes provides the method to add a picture in a sheet by given picture format set (such as offset, scale, aspect ratio setting and print settings), alt text description, extension name and file content in `[]byte` type.

For example:

```go
package main

import (
    _ "image/jpeg"
    "io/ioutil"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()

    file, err := ioutil.ReadFile("image.jpg")
    if err != nil {
        fmt.Println(err)
    }
    if err := f.AddPictureFromBytes("Sheet1", "A2", "", "Excel Logo", ".jpg", file); err != nil {
        fmt.Println(err)
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Get Picture {#GetPicture}

```go
func (f *File) GetPicture(sheet, cell string) (string, []byte, error)
```

GetPicture provides a function to get picture base name and raw content embed in a spreadsheet by given worksheet and cell name. This function is concurrency safe. This function returns the file name in the spreadsheet and file contents as `[]byte` data types.

For example:

```go
f, err := excelize.OpenFile("Book1.xlsx")
if err != nil {
    fmt.Println(err)
    return
}
file, raw, err := f.GetPicture("Sheet1", "A2")
if err != nil {
    fmt.Println(err)
    return
}
if err := ioutil.WriteFile(file, raw, 0644); err != nil {
    fmt.Println(err)
}
```

## Delete Picture {#DeletePicture}

```go
func (f *File) DeletePicture(sheet, cell string) (err error)
```

DeletePicture provides a function to delete charts in a spreadsheet by given worksheet and cell name. Note that the image file won't be deleted from the document currently.
