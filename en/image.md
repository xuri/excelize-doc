# Picture

## Add Picture {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture string, opts *GraphicOptions) error
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
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    // Insert a picture.
    if err := f.AddPicture("Sheet1", "A2", "image.png", nil); err != nil {
        fmt.Println(err)
        return
    }
    // Insert a picture scaling in the cell with location hyperlink.
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
    // Insert a picture offset in the cell with external hyperlink, printing and positioning support.
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

The optional parameter `AutoFit` specifies if make image size auto fits the cell, the default value of that is `false`.

The optional parameter `Hyperlink` specifies the hyperlink of the image.

The optional parameter `HyperlinkType` defines two types of hyperlink `External` for the website or `Location` for moving to one of the cells in this workbook. When the `HyperlinkType` is `Location`, coordinates need to start with `#`.

The optional parameter `Positioning` defines two types of the position of a picture in an Excel spreadsheet, `oneCell` (Move but don't size with cells) or `absolute` (Don't move or size with cells). If you don't set this parameter, the default positioning is move and size with cells.

The optional parameter `PrintObject` indicates whether the image is printed when the worksheet is printed, the default value of that is `true`.

The optional parameter `LockAspectRatio` indicates whether lock aspect ratio for the image, the default value of that is `false`.

The optional parameter `Locked` indicates whether lock the image. Locking an object has no effect unless the sheet is protected.

The optional parameter `OffsetX` specifies the horizontal offset of the image with the cell, the default value of that is 0.

The optional parameter `ScaleX` specifies the horizontal scale of images, the default value of that is 1.0 which presents 100%.

The optional parameter `OffsetY` specifies the vertical offset of the image with the cell, the default value of that is 0.

The optional parameter `ScaleY` specifies the vertical scale of images, the default value of that is 1.0 which presents 100%.

```go
func (f *File) AddPictureFromBytes(sheet, cell, name, extension string, file []byte, opts *GraphicOptions) error
```

AddPictureFromBytes provides the method to add a picture in a sheet by given picture format set (such as offset, scale, aspect ratio setting and print settings), alt text description, extension name and file content in `[]byte` type.

For example:

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
    if err := f.AddPictureFromBytes("Sheet1", "A2", "Excel Logo", ".jpg", file, nil); err != nil {
        fmt.Println(err)
        return
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
defer func() {
    if err := f.Close(); err != nil {
        fmt.Println(err)
    }
}()
file, raw, err := f.GetPicture("Sheet1", "A2")
if err != nil {
    fmt.Println(err)
    return
}
if err := os.WriteFile(file, raw, 0644); err != nil {
    fmt.Println(err)
}
```

## Delete Picture {#DeletePicture}

```go
func (f *File) DeletePicture(sheet, cell string) error
```

DeletePicture provides a function to delete charts in a spreadsheet by given worksheet name and cell reference. Note that the image file won't be deleted from the document currently.
