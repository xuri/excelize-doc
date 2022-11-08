# Изображение

## Добавить изображение {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture, format string) error
```

AddPicture предоставляет способ добавления изображения на листе с помощью заданного формата изображения (например, смещение, масштаб, соотношение сторон и параметры печати) и путь к файлу. Эта функция может быть использована для безопасности параллелизма.

Например:

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
    // Вставьте снимок.
    if err := f.AddPicture("Sheet1", "A2", "image.jpg", ""); err != nil {
        fmt.Println(err)
    }
    // Вставьте масштабирование изображения в ячейку с гиперссылкой местоположения.
    if err := f.AddPicture("Sheet1", "D2", "image.png", `{
        "x_scale": 0.5,
        "y_scale": 0.5,
        "hyperlink": "#Sheet2!D8",
        "hyperlink_type": "Location"
    }`); err != nil {
        fmt.Println(err)
    }
    // Вставьте смещение изображения в ячейку с внешней гиперссылкой, поддержкой печати и позиционирования.
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

Необязательный параметр `autofit` указывает, подходит ли размер изображения автоматически для ячейки, значение по умолчанию - `false`.

Необязательный параметр `hyperlink` указывает гиперссылку изображения.

Необязательный параметр `hyperlink_type` определяет два типа гиперссылки `External` для веб-сайта или `Location` для перехода к одной из ячеек в этой книге. Если для параметра `hyperlink_type` указано значение `Location`, координаты должны начинаться с символа `#`.

Необязательный параметр `positioning` определяет два типа положения изображения в электронной таблице Excel: `oneCell` (перемещать, но не изменять размер с ячейками) или `absolute` (не перемещать и не изменять размер с ячейками). Если вы не установите этот параметр, по умолчанию используется перемещение и размер с ячейками.

Необязательный параметр `print_obj` указывает, печатается ли изображение при печати рабочего листа, значение по умолчанию - `true`.

Необязательный параметр `lock_aspect_ratio` указывает, заблокировано ли соотношение сторон изображения, значение по умолчанию - `false`.

Необязательный параметр `locked` указывает, заблокировано ли изображение. Блокировка объекта не имеет никакого эффекта, если лист не защищен.

Необязательный параметр `x_offset` указывает горизонтальное смещение изображения с ячейкой, значение по умолчанию - 0.

Необязательный параметр `x_scale` определяет горизонтальный масштаб изображений, значение по умолчанию - 1.0, что соответствует 100%.

Необязательный параметр `y_offset` указывает вертикальное смещение изображения с ячейкой, значение по умолчанию - 0.

Необязательный параметр `y_scale` определяет вертикальный масштаб изображений, значение по умолчанию - 1.0, что соответствует 100%.

```go
func (f *File) AddPictureFromBytes(sheet, cell, opts, name, extension string, file []byte) error
```

AddPictureFromBytes предоставляет способ добавления изображения на листе с помощью заданного формата изображения (такого как смещение, масштаб, настройка формата изображения и настройки печати), текстовое описание, имя расширения и содержимое файла в `[]byte`.

Например:

```go
package main

import (
    _ "image/jpeg"
    "os"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()

    file, err := os.ReadFile("image.jpg")
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

## Получить изображение {#GetPicture}

```go
func (f *File) GetPicture(sheet, cell string) (string, []byte, error)
```

GetPicture предоставляет функцию для получения базового имени изображения и необработанного содержимого в XLSX с помощью заданного рабочего листа и имени ячейки. Эта функция может быть использована для безопасности параллелизма. Эта функция возвращает имя файла в XLSX и файлы содержимого в `[] byte` типов данных.

Например:

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
if err = os.WriteFile(file, raw, 0644); err != nil {
    fmt.Println(err)
}
```

## Удалить картинку {#DeletePicture}

```go
func (f *File) DeletePicture(sheet, cell string) (err error)
```

DeletePicture предоставляет функцию для удаления диаграмм в XLSX по заданному рабочему листу и имени ячейки. Обратите внимание, что файл изображения не будет удален из документа в настоящее время.
