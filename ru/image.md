# Изображение

## Добавить изображение {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture string, opts *GraphicOptions) error
```

AddPicture предоставляет метод для добавления изображения на рабочий лист по заданному набору форматов изображения (например, смещение, масштаб, настройка соотношения сторон и настройки печати) и пути к файлу, поддерживаемые типы изображений: BMP, EMF, EMZ, GIF, ICO, JPEG, JPG, PNG, SVG, TIF, TIFF, WMF и WMZ. Эта функция является параллелизм-безопасной. Обратите внимание, что эта функция поддерживает только добавление изображений, размещенных поверх ячеек в данный момент, и не поддерживает добавление изображений, размещенных в ячейках, или создание ячеек встроенных изображений Kingsoft WPS Office.

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

Необязательный параметр `AltText` используется для добавления альтернативного текста к объекту графика.

Необязательный параметр `PrintObject` указывает, печатается ли изображение при печати рабочего листа, значение по умолчанию - `true`.

Необязательный параметр `Locked` указывает, заблокировано ли изображение. Блокировка объекта не имеет никакого эффекта, если лист не защищен.

Необязательный параметр `LockAspectRatio` указывает, заблокировано ли соотношение сторон изображения, значение по умолчанию - `false`.

Необязательный параметр `AutoFit` указывает, подходит ли размер изображения автоматически для ячейки, значение по умолчанию - `false`.

Необязательный параметр `OffsetX` указывает горизонтальное смещение изображения с ячейкой, значение по умолчанию - 0.

Необязательный параметр `OffsetY` указывает вертикальное смещение изображения с ячейкой, значение по умолчанию - 0.

Необязательный параметр `ScaleX` задает горизонтальный масштаб объекта графика. Значение `ScaleX` должно быть числом с плавающей запятой больше 0 с точностью до двух десятичных знаков. Значение по умолчанию 1.0, что соответствует 100%.

Необязательный параметр `ScaleY` задает вертикальный масштаб объекта графика. Значение `ScaleY` должно быть числом с плавающей запятой больше 0 с точностью до двух десятичных знаков. Значение по умолчанию 1.0, что соответствует 100%.

Необязательный параметр `Hyperlink` указывает гиперссылку изображения.

Необязательный параметр `HyperlinkType` определяет два типа гиперссылки `External` для веб-сайта или `Location` для перехода к одной из ячеек в этой книге. Если для параметра `HyperlinkType` указано значение `Location`, координаты должны начинаться с символа `#`.

Необязательный параметр `Positioning` определяет 3 типа положения объекта графика в электронной таблице: `oneCell` (переместить, но не изменять размер с ячейками), `twoCell` (переместить и изменить размер с помощью ячеек) и `absolute` ( Не перемещайте и не изменяйте размер с помощью ячеек). Если вы не зададите этот параметр, позиционирование по умолчанию будет перемещаться и изменять размер с ячейками.

```go
func (f *File) AddPictureFromBytes(sheet, cell string, pic *Picture) error
```

Метод AddPictureFromBytes позволяет добавить изображение на лист, задав формат изображения (например, смещение, масштаб, соотношение сторон и параметры печати), описание в формате Alt, имя расширения и содержимое файла в формате `[]byte`. Поддерживаемые типы изображений: EMF, EMZ, GIF, ICO, JPEG, JPG, PNG, SVG, TIF, TIFF, WMF и WMZ. Обратите внимание, что эта функция поддерживает только добавление изображений, размещенных поверх ячеек, и не поддерживает добавление изображений, размещенных внутри ячеек, или создание ячеек с встроенными изображениями Kingsoft WPS Office.

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
    if err := f.AddPictureFromBytes("Sheet1", "A2", &excelize.Picture{
        Extension: ".jpg",
        File:      file,
        Format:    &excelize.GraphicOptions{AltText: "Excel Logo"},
    }); err != nil {
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
func (f *File) GetPictures(sheet, cell string) ([]Picture, error)
```

Функция GetPicture позволяет получить базовое имя изображения и исходное содержимое, встроенное в электронную таблицу, по заданному имени листа и ячейки. Эта функция безопасна для параллельного выполнения. Функция возвращает имя файла в электронной таблице и содержимое файла в виде данных типа `[]byte`. Обратите внимание, что в настоящее время эта функция не поддерживает получение всех свойств из свойства `Format` изображения, а значения свойств `ScaleX` и `ScaleY` представляют собой число с плавающей запятой больше 0 с точностью до двух десятичных знаков.

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
pics, err := f.GetPictures("Sheet1", "A2")
if err != nil {
    fmt.Println(err)
}
for idx, pic := range pics {
    name := fmt.Sprintf("image%d%s", idx+1, pic.Extension)
    if err := os.WriteFile(name, pic.File, 0644); err != nil {
        fmt.Println(err)
    }
}
```

## Удалить картинку {#DeletePicture}

```go
func (f *File) DeletePicture(sheet, cell string) error
```

DeletePicture предоставляет функцию для удаления диаграмм в XLSX по заданному рабочему листу и имени ячейки. Обратите внимание, что файл изображения не будет удален из документа в настоящее время.
