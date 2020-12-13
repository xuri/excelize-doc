# Basic Usage

## Installation {#install}

Using the latest version Excelize library require to Go version 1.10 or later.

- Installation

```bash
go get github.com/360EntSecGroup-Skylar/excelize
```

- If your package management with [Go Modules](https://blog.golang.org/using-go-modules), please install with the following command.

```bash
go get github.com/360EntSecGroup-Skylar/excelize/v2
```

## Upgrade {#update}

- Upgrade

```bash
go get -u github.com/360EntSecGroup-Skylar/excelize/v2
```

## Create Excel document {#NewFile}

Here is a minimal example usage that will create spreadsheet file:

```go
package main

import (
    "fmt"

    "github.com/360EntSecGroup-Skylar/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    // Create a new worksheet.
    index := f.NewSheet("Sheet2")
    // Set value of a cell.
    f.SetCellValue("Sheet2", "A2", "Hello world.")
    f.SetCellValue("Sheet1", "B2", 100)
    // Set the active worksheet of the workbook.
    f.SetActiveSheet(index)
    // Save the spreadsheet by the given path.
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Reading Excel document {#read}

The following constitutes the bare to read a spreadsheet document:

```go
package main

import (
    "fmt"

    "github.com/360EntSecGroup-Skylar/excelize/v2"
)

func main() {
    f, err := excelize.OpenFile("Book1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    // Get value from the cell by given worksheet name and axis.
    cell, err := f.GetCellValue("Sheet1", "B2")
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(cell)
    // Get all the rows in the Sheet1.
    rows, err := f.GetRows("Sheet1")
    for _, row := range rows {
        for _, colCell := range row {
            fmt.Print(colCell, "\t")
        }
        fmt.Println()
    }
}
```

## Add chart to Excel document {#chart}

With Excelize chart generation and management is as easy as a few lines of code. You can build charts based on data in your worksheet or generate charts without any data in your worksheet at all.

<p align="center"><img width="770" src="../images/base.png" alt="Add chart to Excel document"></p>

```go
package main

import (
    "fmt"

    "github.com/360EntSecGroup-Skylar/excelize/v2"
)

func main() {
    categories := map[string]string{
        "A2": "Small", "A3": "Normal", "A4": "Large", "B1": "Apple", "C1": "Orange", "D1": "Pear"}
    values := map[string]int{
        "B2": 2, "C2": 3, "D2": 3, "B3": 5, "C3": 2, "D3": 4, "B4": 6, "C4": 7, "D4": 8}
    f := excelize.NewFile()
    for k, v := range categories {
        f.SetCellValue("Sheet1", k, v)
    }
    for k, v := range values {
        f.SetCellValue("Sheet1", k, v)
    }
    if err := f.AddChart("Sheet1", "E1", `{
        "type": "col3DClustered",
        "series": [
        {
            "name": "Sheet1!$A$2",
            "categories": "Sheet1!$B$1:$D$1",
            "values": "Sheet1!$B$2:$D$2"
        },
        {
            "name": "Sheet1!$A$3",
            "categories": "Sheet1!$B$1:$D$1",
            "values": "Sheet1!$B$3:$D$3"
        },
        {
            "name": "Sheet1!$A$4",
            "categories": "Sheet1!$B$1:$D$1",
            "values": "Sheet1!$B$4:$D$4"
        }],
        "title":
        {
            "name": "Fruit 3D Clustered Column Chart"
        }
    }`); err != nil {
        fmt.Println(err)
        return
    }
    // Save the spreadsheet by the given path.
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Add picture to Excel document {#image}

```go
package main

import (
    "fmt"
    _ "image/gif"
    _ "image/jpeg"
    _ "image/png"

    "github.com/360EntSecGroup-Skylar/excelize/v2"
)

func main() {
    f, err := excelize.OpenFile("Book1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    // Insert a picture.
    if err := f.AddPicture("Sheet1", "A2", "image.png", ""); err != nil {
        fmt.Println(err)
    }
    // Insert a picture to worksheet with scaling.
    if err := f.AddPicture("Sheet1", "D2", "image.jpg", `{
        "x_scale": 0.5,
        "y_scale": 0.5
    }`); err != nil {
        fmt.Println(err)
    }
    // Insert a picture offset in the cell with printing support.
    if err := f.AddPicture("Sheet1", "H2", "image.gif", `{
        "x_offset": 15,
        "y_offset": 10,
        "print_obj": true,
        "lock_aspect_ratio": false,
        "locked": false
    }`); err != nil {
        fmt.Println(err)
    }
    // Save the spreadsheet with the origin path.
    if err = f.Save(); err != nil {
        fmt.Println(err)
    }
}
```
