# Изображение

## Добавить изображение {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture, format string) error
```

AddPicture предоставляет способ добавления изображения на листе с помощью заданного формата изображения (например, смещение, масштаб, соотношение сторон и параметры печати) и путь к файлу.

Например:

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
    xlsx := excelize.NewFile()
    // Вставьте снимок.
    err := xlsx.AddPicture("Sheet1", "A2", "./image1.jpg", "")
    if err != nil {
        fmt.Println(err)
    }
    // Вставьте масштабирование изображения в ячейку с гиперссылкой местоположения.
    err = xlsx.AddPicture("Sheet1", "D2", "./image1.png", `{"x_scale": 0.5, "y_scale": 0.5, "hyperlink": "#Sheet2!D8", "hyperlink_type": "Location"}`)
    if err != nil {
        fmt.Println(err)
    }
    // Вставьте смещение изображения в ячейку с внешней гиперссылкой, поддержкой печати и позиционирования.
    err = xlsx.AddPicture("Sheet1", "H2", "./image3.gif", `{"x_offset": 15, "y_offset": 10, "hyperlink": "https://github.com/360EntSecGroup-Skylar/excelize", "hyperlink_type": "External", "print_obj": true, "lock_aspect_ratio": false, "locked": false, "positioning": "oneCell"}`)
    if err != nil {
        fmt.Println(err)
    }
    err = xlsx.SaveAs("./Book1.xlsx")
    if err != nil {
        fmt.Println(err)
    }
}
```

LinkType определяет два типа гиперссылки `External` для сайта или `Location` для перехода к одной из сот в этой книге. Когда `hyperlink_type` является `Location`, координаты должны начинаться с `#`.

Позиционирование определяет два типа положения изображения в электронной таблице Excel, `oneCell` (перемещение, но не размер с ячейками) или «абсолютное» (не перемещать и не изменять размер с ячейками). Если вы не установите этот параметр, по умолчанию `positioning` будет перемещаться и размер с ячейками.

```go
func (f *File) AddPictureFromBytes(sheet, cell, format, name, extension string, file []byte) error
```

AddPictureFromBytes предоставляет способ добавления изображения на листе с помощью заданного формата изображения (такого как смещение, масштаб, настройка формата изображения и настройки печати), текстовое описание, имя расширения и содержимое файла в `[]byte`.

Например:

```go
package main

import (
    "fmt"
    _ "image/jpeg"
    "io/ioutil"

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    xlsx := excelize.NewFile()

    file, err := ioutil.ReadFile("./image1.jpg")
    if err != nil {
        fmt.Println(err)
    }
    err = xlsx.AddPictureFromBytes("Sheet1", "A2", "", "Excel Logo", ".jpg", file)
    if err != nil {
        fmt.Println(err)
    }
    err = xlsx.SaveAs("./Book1.xlsx")
    if err != nil {
        fmt.Println(err)
    }
}
```

## Получить изображение {#GetPicture}

```go
func (f *File) GetPicture(sheet, cell string) (string, []byte)
```

GetPicture предоставляет функцию для получения базового имени изображения и необработанного содержимого в XLSX с помощью заданного рабочего листа и имени ячейки. Эта функция возвращает имя файла в XLSX и файлы содержимого в `[] byte` типов данных.

Например:

```go
xlsx, err := excelize.OpenFile("./Book1.xlsx")
if err != nil {
    fmt.Println(err)
    return
}
file, raw := xlsx.GetPicture("Sheet1", "A2")
if file == "" {
    return
}
err := ioutil.WriteFile(file, raw, 0644)
if err != nil {
    fmt.Println(err)
}
```