# Picture

## Add Picture {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture, format string) error
```

AddPicture provides the method to add picture in a sheet by given picture format set (such as offset, scale, aspect ratio setting and print settings) and file path.

For example:

```go
package main

import (
    _ "image/gif"
    _ "image/jpeg"
    _ "image/png"

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    f := excelize.NewFile()
    // Insert a picture.
    if err := f.AddPicture("Sheet1", "A2", "image.jpg", ""); err != nil {
        fmt.Println(err)
    }
    // Insert a picture scaling in the cell with location hyperlink.
    if err := f.AddPicture("Sheet1", "D2", "image.png", `{"x_scale": 0.5, "y_scale": 0.5, "hyperlink": "#Sheet2!D8", "hyperlink_type": "Location"}`); err != nil {
        fmt.Println(err)
    }
    // Insert a picture offset in the cell with external hyperlink, printing and positioning support.
    if err := f.AddPicture("Sheet1", "H2", "image.gif", `{"x_offset": 15, "y_offset": 10, "hyperlink": "https://github.com/360EntSecGroup-Skylar/excelize", "hyperlink_type": "External", "print_obj": true, "lock_aspect_ratio": false, "locked": false, "positioning": "oneCell"}`); err != nil {
        fmt.Println(err)
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

LinkType defines two types of hyperlink `External` for web site or `Location` for moving to one of cell in this workbook. When the `hyperlink_type` is `Location`, coordinates need to start with `#`.

Positioning defines two types of the position of a picture in an Excel spreadsheet, `oneCell` (Move but don't size with cells) or "absolute" (Don't move or size with cells). If you don't set this parameter, default `positioning` is move and size with cells.

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

    "github.com/360EntSecGroup-Skylar/excelize"
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

GetPicture provides a function to get picture base name and raw content embed in XLSX by given worksheet and cell name. This function returns the file name in XLSX and file contents as `[]byte` data types.

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

DeletePicture provides a function to delete charts in XLSX by given worksheet and cell name. Note that the image file won't be deleted from the document currently.
