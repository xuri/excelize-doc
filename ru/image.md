# Изображение

## Добавить изображение {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture string, opts *GraphicOptions) error
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
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    // Вставьте снимок.
    if err := f.AddPicture("Sheet1", "A2", "image.png", nil); err != nil {
        fmt.Println(err)
        return
    }
    // Вставьте масштабирование изображения в ячейку с гиперссылкой местоположения.
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
    // Вставьте смещение изображения в ячейку с внешней гиперссылкой, поддержкой печати и позиционирования.
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

Необязательный параметр `AutoFit` указывает, подходит ли размер изображения автоматически для ячейки, значение по умолчанию - `false`.

Необязательный параметр `Hyperlink` указывает гиперссылку изображения.

Необязательный параметр `HyperlinkType` определяет два типа гиперссылки `External` для веб-сайта или `Location` для перехода к одной из ячеек в этой книге. Если для параметра `HyperlinkType` указано значение `Location`, координаты должны начинаться с символа `#`.

Необязательный параметр `Positioning` определяет два типа положения изображения в электронной таблице Excel: `oneCell` (перемещать, но не изменять размер с ячейками) или `absolute` (не перемещать и не изменять размер с ячейками). Если вы не установите этот параметр, по умолчанию используется перемещение и размер с ячейками.

Необязательный параметр `PrintObject` указывает, печатается ли изображение при печати рабочего листа, значение по умолчанию - `true`.

Необязательный параметр `LockAspectRatio` указывает, заблокировано ли соотношение сторон изображения, значение по умолчанию - `false`.

Необязательный параметр `Locked` указывает, заблокировано ли изображение. Блокировка объекта не имеет никакого эффекта, если лист не защищен.

Необязательный параметр `OffsetX` указывает горизонтальное смещение изображения с ячейкой, значение по умолчанию - 0.

Необязательный параметр `ScaleX` определяет горизонтальный масштаб изображений, значение по умолчанию - 1.0, что соответствует 100%.

Необязательный параметр `OffsetY` указывает вертикальное смещение изображения с ячейкой, значение по умолчанию - 0.

Необязательный параметр `ScaleY` определяет вертикальный масштаб изображений, значение по умолчанию - 1.0, что соответствует 100%.

```go
func (f *File) AddPictureFromBytes(sheet, cell, name, extension string, file []byte, opts *GraphicOptions) error
```

AddPictureFromBytes предоставляет способ добавления изображения на листе с помощью заданного формата изображения (такого как смещение, масштаб, настройка формата изображения и настройки печати), текстовое описание, имя расширения и содержимое файла в `[]byte`.

Например:

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
