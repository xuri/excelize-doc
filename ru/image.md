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
    _ "image/gif"
    _ "image/jpeg"
    _ "image/png"

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    f := excelize.NewFile()
    // Вставьте снимок.
    if err := f.AddPicture("Sheet1", "A2", "image.jpg", ""); err != nil {
        println(err.Error())
    }
    // Вставьте масштабирование изображения в ячейку с гиперссылкой местоположения.
    if err := f.AddPicture("Sheet1", "D2", "image.png", `{"x_scale": 0.5, "y_scale": 0.5, "hyperlink": "#Sheet2!D8", "hyperlink_type": "Location"}`); err != nil {
        println(err.Error())
    }
    // Вставьте смещение изображения в ячейку с внешней гиперссылкой, поддержкой печати и позиционирования.
    if err := f.AddPicture("Sheet1", "H2", "image.gif", `{"x_offset": 15, "y_offset": 10, "hyperlink": "https://github.com/360EntSecGroup-Skylar/excelize", "hyperlink_type": "External", "print_obj": true, "lock_aspect_ratio": false, "locked": false, "positioning": "oneCell"}`); err != nil {
        println(err.Error())
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        println(err.Error())
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
    _ "image/jpeg"
    "io/ioutil"

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    f := excelize.NewFile()

    file, err := ioutil.ReadFile("image.jpg")
    if err != nil {
        println(err.Error())
    }
    if err := f.AddPictureFromBytes("Sheet1", "A2", "", "Excel Logo", ".jpg", file); err != nil {
        println(err.Error())
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        println(err.Error())
    }
}
```

## Получить изображение {#GetPicture}

```go
func (f *File) GetPicture(sheet, cell string) (string, []byte, error)
```

GetPicture предоставляет функцию для получения базового имени изображения и необработанного содержимого в XLSX с помощью заданного рабочего листа и имени ячейки. Эта функция возвращает имя файла в XLSX и файлы содержимого в `[] byte` типов данных.

Например:

```go
f, err := excelize.OpenFile("Book1.xlsx")
if err != nil {
    println(err.Error())
    return
}
file, raw, err := f.GetPicture("Sheet1", "A2")
if err != nil {
    println(err.Error())
    return
}
if err = ioutil.WriteFile(file, raw, 0644); err != nil {
    println(err.Error())
}
```

## Удалить картинку {#DeletePicture}

```go
func (f *File) DeletePicture(sheet, cell string) (err error)
```

DeletePicture предоставляет функцию для удаления диаграмм в XLSX по заданному рабочему листу и имени ячейки. Обратите внимание, что файл изображения не будет удален из документа в настоящее время.
