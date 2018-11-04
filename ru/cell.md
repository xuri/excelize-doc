# клетка

## Установить значение ячейки {#SetCellValue}

```go
func (f *File) SetCellValue(sheet, axis string, value interface{})
```

SetCellValue предоставляет функцию для установки значения ячейки. Ниже приведены поддерживаемые типы данных:

|Поддерживаемые типы данных|
|---|
|int|
|int8|
|int16|
|int32|
|int64|
|uint|
|uint8|
|uint16|
|uint32|
|uint64|
|float32|
|float64|
|string|
|[]byte|
|time.Duration|
|time.Time|
|bool|
|nil|

## Установить логическое значение {#SetCellBool}

```go
func (f *File) SetCellBool(sheet, axis string, value bool)
```

SetCellBool предоставляет функцию для установки значения типа bool ячейки с помощью заданного имени листа, координат ячейки и значения ячейки.

## Установить значение RAW {#SetCellDefault}

```go
func (f *File) SetCellDefault(sheet, axis, value string)
```

SetCellDefault предоставляет функцию для установки значения типа строки ячейки как формата по умолчанию, не выходя из ячейки.

## Установить целочисленное значение {#SetCellInt}

```go
func (f *File) SetCellInt(sheet, axis string, value int)
```

SetCellInt предоставляет функцию для установки значения типа int ячейки с помощью заданного имени листа, координат ячейки и значения ячейки.

## Установить строковое значение {#SetCellStr}

```go
func (f *File) SetCellStr(sheet, axis, value string)
```

SetCellStr предоставляет функцию для установки значения типа строки для ячейки. Общее количество символов, которое ячейка может содержать символы `32767`.

## Установить стиль ячейки {#SetCellStyle}

```go
func (f *File) SetCellStyle(sheet, hcell, vcell string, styleID int)
```

SetCellStyle предоставляет функцию добавления атрибута стиля для ячеек по заданному имени рабочего листа, области координат и идентификатору стиля. Индексы стиля можно получить с помощью функции `NewStyle`. Обратите внимание, что границы `diagonalDown` и `diagonalUp` должны использоваться одинаковым цветом в одной и той же координатной области.

- Пример 1, создайте границы ячейки `D7` на` Sheet1`:

```go
style, err := xlsx.NewStyle(`{"border":[{"type":"left","color":"0000FF","style":3},{"type":"top","color":"00FF00","style":4},{"type":"bottom","color":"FFFF00","style":5},{"type":"right","color":"FF0000","style":6},{"type":"diagonalDown","color":"A020F0","style":7},{"type":"diagonalUp","color":"A020F0","style":8}]}`)
if err != nil {
    fmt.Println(err)
}
xlsx.SetCellStyle("Sheet1", "D7", "D7", style)
```

!["Установите стиль рамки для ячейки"](./images/SetCellStyle_01.png "Установите стиль рамки для ячейки")

Четыре границы ячейки `D7` установлены с разными стилями и цветами. Это связано с параметрами при вызове функции `NewStyle`. Вам нужно установить разные стили для ссылки на документацию для этой главы.

- Пример 2, установив стиль градиента для ячейки `D7` листа `Sheet1`:

```go
style, err := xlsx.NewStyle(`{"fill":{"type":"gradient","color":["#FFFFFF","#E0EBF5"],"shading":1}}`)
if err != nil {
    fmt.Println(err)
}
xlsx.SetCellStyle("Sheet1", "D7", "D7", style)
```

!["Установите стиль градиента для ячейки"](./images/SetCellStyle_02.png "Установите стиль градиента для ячейки")

В ячейке `D7` задается цветовая заливка эффекта градиента. Эффект градиентной заливки связан с параметром при вызове функции `NewStyle`. Вам нужно установить разные стили для ссылки на документацию этой главы.

- Пример 3, установите сплошную заливку для ячейки `D7` с именем `Sheet1`:

```go
style, err := xlsx.NewStyle(`{"fill":{"type":"pattern","color":["#E0EBF5"],"pattern":1}}`)
if err != nil {
    fmt.Println(err)
}
xlsx.SetCellStyle("Sheet1", "D7", "D7", style)
```

!["Установите сплошную заливку для ячейки"](./images/SetCellStyle_03.png "Установите сплошную заливку для ячейки")

Ячейка `D7` установлена с заполнением.

- Пример 4, задайте расстояние между символами и угол поворота для ячейки `D7` с именем `Sheet1`:

```go
xlsx.SetCellValue("Sheet1", "D7", "样式")
style, err := xlsx.NewStyle(`{"alignment":{"horizontal":"center","ident":1,"justify_last_line":true,"reading_order":0,"relative_indent":1,"shrink_to_fit":true,"text_rotation":45,"vertical":"","wrap_text":true}}`)
if err != nil {
    fmt.Println(err)
}
xlsx.SetCellStyle("Sheet1", "D7", "D7", style)
```

!["Установите расстояние между символами и угол поворота"](./images/SetCellStyle_04.png "Установите расстояние между символами и угол поворота")

- Пример 5, дата и время в Excel представлены действительными числами, например `2017/7/4  12:00:00 PM` могут быть представлены числом `42920.5`. Установите формат времени для ячейки таблицы `D7` с именем `Sheet1`:

```go
xlsx.SetCellValue("Sheet1", "D7", 42920.5)
xlsx.SetColWidth("Sheet1", "D", "D", 13)
style, err := xlsx.NewStyle(`{"number_format": 22}`)
if err != nil {
    fmt.Println(err)
}
xlsx.SetCellStyle("Sheet1", "D7", "D7", style)
```

!["Установите формат времени для ячейки"](./images/SetCellStyle_05.png "Установите формат времени для ячейки")

В ячейке `D7` установлен формат времени. Обратите внимание, что когда ширина ячейки с применяемым временным форматом слишком узкая, чтобы ее можно было полностью отобразить, она будет отображаться как `####`, вы можете перетащить ширину столбца или установить столбец в соответствующий размер, вызвав `SetColWidth`, чтобы сделать его нормальным. дисплей.

- Пример 6, установив шрифт, размер шрифта, цвет и стиль перекоса для ячейки `D7` листа `Sheet1`:

```go
xlsx.SetCellValue("Sheet1", "D7", "Excel")
style, err := xlsx.NewStyle(`{"font":{"bold":true,"italic":true,"family":"Berlin Sans FB Demi","size":36,"color":"#777777"}}`)
if err != nil {
    fmt.Println(err)
}
xlsx.SetCellStyle("Sheet1", "D7", "D7", style)
```

!["Установите шрифт, размер шрифта, цвет и стиль перекоса для ячеек"](./images/SetCellStyle_06.png "Установите шрифт, размер шрифта, цвет и стиль перекоса для ячеек")

- Пример 7, блокировка и скрытие ячейки `D7` с именем `Sheet1`:

```go
style, err := xlsx.NewStyle(`{"protection":{"hidden":true, "locked":true}}`)
if err != nil {
    fmt.Println(err)
}
xlsx.SetCellStyle("Sheet1", "D7", "D7", style)
```

Чтобы заблокировать ячейку или скрыть формулу, защитите рабочий лист. На вкладке «Обзор» нажмите «Защитить рабочий лист».

## Установить гиперссылку {#SetCellHyperLink}

```go
func (f *File) SetCellHyperLink(sheet, axis, link, linkType string)
```

SetCellHyperLink предоставляет функцию для установки гиперссылки на ячейки с помощью заданного имени рабочего листа и URL-адреса URL-адреса. LinkType определяет два типа гиперссылки `External` для сайта или `Location` для перехода к одной из сот в этой книге. Ниже приведен пример внешней ссылки.

- Пример 1, добавление внешней ссылки на ячейку `A3` на листе с именем `Sheet1`:

```go
xlsx.SetCellHyperLink("Sheet1", "A3", "https://github.com/360EntSecGroup-Skylar/excelize", "External")
// Задайте стиль шрифта и подчеркивания для ячейки
style, _ := xlsx.NewStyle(`{"font":{"color":"#1265BE","underline":"single"}}`)
xlsx.SetCellStyle("Sheet1", "A3", "A3", style)
```

- Пример 2: добавление внутренней ссылки на ячейку `A3` с именем `Sheet1`:

```go
xlsx.SetCellHyperLink("Sheet1", "A3", "Sheet1!A40", "Location")
```

## Получить значение ячейки {#GetCellValue}

```go
func (f *File) GetCellValue(sheet, axis string) string
```

Значение ячейки извлекается в соответствии с данным рабочим листом и координатами ячейки, а возвращаемое значение преобразуется в тип `string`. Если формат ячейки можно применить к значению ячейки, прикладное значение будет возвращено, иначе исходное значение будет возвращено.

## Получить все значения ячейки {#GetRows}

```go
func (f *File) GetRows(sheet string) [][]string
```

Получает значение всех ячеек на листе на основе заданного имени листа (с учетом регистра), возвращаемого в виде двумерного массива, где значение ячейки преобразуется в тип `string`. Если формат ячейки можно применить к значению ячейки, применяется прикладное значение, в противном случае будет использоваться исходное значение.

Например, получите и перемещайте значение всех ячеек на листе с именем `Sheet1`:

```go
for _, row := range xlsx.GetRows("Sheet1") {
    for _, colCell := range row {
        fmt.Print(colCell, "\t")
    }
    fmt.Println()
}
```

## Получить гиперссылку {#GetCellHyperLink}

```go
func (f *File) GetCellHyperLink(sheet, axis string) (bool, string)
```

Получает гиперссылку на ячейку на основе заданного имени листа (с учетом регистра) и координат ячейки. Если ячейка имеет гиперссылку, она вернет `true` и адрес ссылки, иначе он вернет `false` и пустой адрес ссылки.

Например, получите гиперссылку на ячейку `H6` на листе с именем `Sheet1`:

```go
link, target := xlsx.GetCellHyperLink("Sheet1", "H6")
```

## Получить индекс стиля {#GetCellStyle}

```go
func (f *File) GetCellStyle(sheet, axis string) int
```

Индекс стиля ячейки получается из заданного имени листа (с учетом регистра) и координат ячейки, а полученный индекс может использоваться как параметр для вызова функции `SetCellValue` при копировании стиля ячейки.

## Объединить ячейки {#MergeCell}

```go
func (f *File) MergeCell(sheet, hcell, vcell string)
```

Объединить ячейки на основе заданного имени листа (с учетом регистра) и областей координат ячейки. Например, слияние ячеек в области `D3:E9` на листе с именем `Sheet1`:

```go
xlsx.MergeCell("Sheet1", "D3", "E9")
```

Если заданная координатная область ячейки перекрывается с другими существующими объединенными ячейками, существующие объединенные ячейки будут удалены.

## Добавить комментарий {#AddComment}

```go
func (f *File) AddComment(sheet, cell, format string) error
```

AddComment предоставляет метод добавления комментариев в листе с помощью заданного индекса, набора ячеек и формата (например, автора и текста). Обратите внимание, что максимальная длина автора равна 255, а максимальная длина текста - 32512. Например, добавьте комментарий в `Sheet1!$A$3`:

!["Добавить комментарий к документу Excel"](./images/comment.png "Добавить комментарий к документу Excel")

```go
xlsx.AddComment("Sheet1", "A3", `{"author":"Excelize: ","text":"This is a comment."}`)
```

## Получить комментари {#GetComments}

```go
func (f *File) GetComments() (comments map[string][]Comment)
```

GetComments извлекает все комментарии и возвращает карту имени рабочего листа в комментарии рабочего листа.

## Установить формулу ячейки {#SetCellFormula}

```go
func (f *File) SetCellFormula(sheet, axis, formula string)
```

Формула на ячейке берется согласно заданному имени листа (с учетом регистра) и настройкам формулы ячейки. Результат формулы вычисляется, когда рабочий лист открывается приложением Office Excel, а Excelize в настоящее время не предоставляет механизм вычисления формулы, поэтому результаты формулы не могут быть рассчитаны.

## Получить формулу ячейки {#GetCellFormula}

```go
func (f *File) GetCellFormula(sheet, axis string) string
```

Получите формулу в ячейке на основе заданного имени листа (с учетом регистра) и координат ячейки.
