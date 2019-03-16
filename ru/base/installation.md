# Основное использование

## Установка {#install}

Использование библиотеки Excelize необходима Go версия 1.8 или более поздняя версия.

- Установка

```bash
go get github.com/360EntSecGroup-Skylar/excelize
```

## Обновление {#update}

- Обновление

```bash
go get -u github.com/360EntSecGroup-Skylar/excelize
```

## Создать документ Excel {#NewFile}

Вот минимальный пример использования, который будет создавать файл XLSX:

```go
package main

import (
    "fmt"

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    xlsx := excelize.NewFile()
    // Создать новый лист.
    index := xlsx.NewSheet("Sheet2")
    // Установленное значение ячейки.
    xlsx.SetCellValue("Sheet2", "A2", "Hello world.")
    xlsx.SetCellValue("Sheet1", "B2", 100)
    // Установить активный лист рабочей книги.
    xlsx.SetActiveSheet(index)
    // Сохранить файл xlsx по данному пути.
    err := xlsx.SaveAs("./Book1.xlsx")
    if err != nil {
        fmt.Println(err)
    }
}
```

## Чтение документа Excel {#read}

Ниже представляет собой голое прочитать документ XLSX:

```go
package main

import (
    "fmt"

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    xlsx, err := excelize.OpenFile("./Book1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    // Получить значение из ячейки по заданному имени и оси листа.
    cell := xlsx.GetCellValue("Sheet1", "B2")
    fmt.Println(cell)
    // Получить все строки в Sheet1.
    rows := xlsx.GetRows("Sheet1")
    for _, row := range rows {
        for _, colCell := range row {
            fmt.Print(colCell, "\t")
        }
        fmt.Println()
    }
}
```

## Добавить диаграмму в документ Excel {#chart}

С Excelize создание и управление диаграммами так же просто, как несколько строк кода. Вы можете создавать диаграммы на основе данных на вашем листе или создавать диаграммы без каких-либо данных на вашем листе вообще.

<p align="center"><img width="769" src="../images/base.png" alt="Добавить диаграмму в документ Excel"></p>

```go
package main

import (
    "fmt"

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    categories := map[string]string{"A2": "Small", "A3": "Normal", "A4": "Large", "B1": "Apple", "C1": "Orange", "D1": "Pear"}
    values := map[string]int{"B2": 2, "C2": 3, "D2": 3, "B3": 5, "C3": 2, "D3": 4, "B4": 6, "C4": 7, "D4": 8}
    xlsx := excelize.NewFile()
    for k, v := range categories {
        xlsx.SetCellValue("Sheet1", k, v)
    }
    for k, v := range values {
        xlsx.SetCellValue("Sheet1", k, v)
    }
    xlsx.AddChart("Sheet1", "E1", `{"type":"col3DClustered","series":[{"name":"Sheet1!$A$2","categories":"Sheet1!$B$1:$D$1","values":"Sheet1!$B$2:$D$2"},{"name":"Sheet1!$A$3","categories":"Sheet1!$B$1:$D$1","values":"Sheet1!$B$3:$D$3"},{"name":"Sheet1!$A$4","categories":"Sheet1!$B$1:$D$1","values":"Sheet1!$B$4:$D$4"}],"title":{"name":"Fruit 3D Clustered Column Chart"}}`)
    // Сохранить файл xlsx по данному пути.
    err := xlsx.SaveAs("./Book1.xlsx")
    if err != nil {
        fmt.Println(err)
    }
}
```

## Добавить изображение в документ Excel {#image}

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
    xlsx, err := excelize.OpenFile("./Book1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    // Вставить картинку.
    err = xlsx.AddPicture("Sheet1", "A2", "./image1.png", "")
    if err != nil {
        fmt.Println(err)
    }
    // Вставка изображения в рабочий лист с масштабированием.
    err = xlsx.AddPicture("Sheet1", "D2", "./image2.jpg", `{"x_scale": 0.5, "y_scale": 0.5}`)
    if err != nil {
        fmt.Println(err)
    }
    // Вставьте смещение изображения в ячейке с поддержкой печати.
    err = xlsx.AddPicture("Sheet1", "H2", "./image3.gif", `{"x_offset": 15, "y_offset": 10, "print_obj": true, "lock_aspect_ratio": false, "locked": false}`)
    if err != nil {
        fmt.Println(err)
    }
    // Сохраните файл xlsx с исходным путем.
    err = xlsx.Save()
    if err != nil {
        fmt.Println(err)
    }
}
```