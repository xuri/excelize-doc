# Основное использование

## Установка {#install}

В следующей таблице показаны минимальные требования к языку Go для каждой выпущенной версии Excelize:

Версия Excelize | Минимальные требования к языковой версии Go
---|---
v2.7.0 | 1.16
v2.4.0 ~ v2.6.1 | 1.15
v2.0.2 ~ v2.3.2 | 1.10
v1.0.0 ~ v2.0.1 | 1.6

Для использования библиотеки Excelize последней версии требуется версия Go 1.16 или более поздняя.

- Установка

```bash
go get github.com/xuri/excelize
```

- Если ваш пакет управления с помощью [Go Modules](https://go.dev/blog/using-go-modules), пожалуйста, установите с помощью следующей команды.

```bash
go get github.com/xuri/excelize/v2
```

## Обновление {#update}

- Обновление

```bash
go get -u github.com/xuri/excelize/v2
```

## Создать документ Excel {#NewFile}

Вот минимальный пример использования, который будет создавать файл XLSX:

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
    // Создать новый лист
    index, err := f.NewSheet("Sheet2")
    if err != nil {
        fmt.Println(err)
        return
    }
    // Установленное значение ячейки
    f.SetCellValue("Sheet2", "A2", "Hello world.")
    f.SetCellValue("Sheet1", "B2", 100)
    // Установить активный лист рабочей книги
    f.SetActiveSheet(index)
    // Сохранить файл xlsx по данному пути
    if err := f.SaveAs("Book1.xlsx"); err != nil {
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
    // Получить значение из ячейки по заданному имени и оси листа
    cell, err := f.GetCellValue("Sheet1", "B2")
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(cell)
    // Получить все строки в Sheet1
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

## Добавить диаграмму в документ Excel {#chart}

С Excelize создание и управление диаграммами так же просто, как несколько строк кода. Вы можете создавать диаграммы на основе данных на вашем листе или создавать диаграммы без каких-либо данных на вашем листе вообще.

<p align="center"><img width="769" src="../images/base.png" alt="Добавить диаграмму в документ Excel"></p>

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
        Title: excelize.ChartTitle{
            Name: "Fruit 3D Clustered Column Chart",
        },
    }); err != nil {
        fmt.Println(err)
        return
    }
    // Сохранить файл xlsx по данному пути
    if err := f.SaveAs("Book1.xlsx"); err != nil {
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
    // Вставить картинку
    if err := f.AddPicture("Sheet1", "A2", "image.png", nil); err != nil {
        fmt.Println(err)
        return
    }
    // Вставка изображения в рабочий лист с масштабированием
    if err := f.AddPicture("Sheet1", "D2", "image.jpg",
        &excelize.GraphicOptions{ScaleX: 0.5, ScaleY: 0.5}); err != nil {
        fmt.Println(err)
        return
    }
    // Вставьте смещение изображения в ячейке с поддержкой печати
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
    // Сохраните файл xlsx с исходным путем
    if err = f.Save(); err != nil {
        fmt.Println(err)
    }
}
```
