# Рабочая книга

## Создать документ Excel {#NewFile}

```go
func NewFile() *File
```

NewFile предоставляет функцию для создания нового файла по умолчанию. Вновь созданная рабочая книга по умолчанию будет содержать таблицу с именем `Sheet1`. Например:

## Открыть {#OpenFile}

```go
func OpenFile(filename string) (*File, error)
```

OpenFile принимает имя файла XLSX и возвращает для него заполненную файловую структуру XLSX.

## Сохранить {#Save}

```go
func (f *File) Save() error
```

Save предоставляет функцию для переопределения файла xlsx с исходным путем.

## Сохранить как {#SaveAs}

```go
func (f *File) SaveAs(name string) error
```

SaveAs предоставляет функцию для создания или обновления файла xlsx по предоставленному пути.

## Создать рабочий лист {#NewSheet}

```go
func (f *File) NewSheet(name string) int
```

NewSheet предоставляет функцию для создания нового листа по заданному имени листа при создании нового файла XLSX, при создании нового файла будет создан лист по умолчанию.

## Удалить рабочий лист {#DeleteSheet}

```go
func (f *File) DeleteSheet(name string)
```

DeleteSheet предоставляет функцию для удаления рабочего листа в рабочей книге с помощью заданного имени листа. Используйте этот метод с осторожностью, что повлияет на изменения в ссылках, таких как формулы, диаграммы и т. Д. Если есть какое-либо ссылочное значение удаленного листа, это приведет к ошибке файла при его открытии. Эта функция будет недействительной, если останется только один лист.

## Лист копирования {#CopySheet}

```go
func (f *File) CopySheet(from, to int) error
```

CopySheet предоставляет функцию для дублирования рабочего листа путем указания индекса источника и целевого листа. Обратите внимание, что в настоящее время не поддерживается дублирование книг, содержащих таблицы, диаграммы или изображения. Например:

```go
// Sheet1 уже существует...
index := xlsx.NewSheet("Sheet2")
err := xlsx.CopySheet(1, index)
return err
```

## Фон рабочего листа {#SetSheetBackground}

```go
func (f *File) SetSheetBackground(sheet, picture string) error
```

SetSheetBackground предоставляет функцию для установки фонового изображения с помощью имени рабочего листа.

## Установить рабочий лист по умолчанию {#SetActiveSheet}

```go
func (f *File) SetActiveSheet(index int)
```

SetActiveSheet предоставляет функцию для установки активного рабочего листа по умолчанию XLSX по заданному индексу. Обратите внимание, что активный индекс отличается индексом, полученным функцией [`GetSheetMap`](sheet.md#GetSheetMap), и должен быть больше, чем `0` и меньше, чем общее число рабочих листов.

## Получить активный индекс листа {#GetActiveSheetIndex}

```go
func (f *File) GetActiveSheetIndex() int
```

GetActiveSheetIndex предоставляет функцию для получения активного листа XLSX. Если не найден, активный лист вернет целое число `0`.

## Получить свойства вида листа {#GetSheetViewOptions}

```go
func (f *File) GetSheetViewOptions(name string, viewIndex int, opts ...SheetViewOptionPtr) error
```

GetSheetViewOptions получает значение параметров просмотра листа. `ViewIndex` может быть отрицательным, и если это так отсчитывается в обратном направлении (`-1` это последний вид). Доступные Варианты:

Необязательный параметр просмотра|Тип
---|---
DefaultGridColor|bool
RightToLeft|bool
ShowFormulas|bool
ShowGridLines|bool
ShowRowColHeaders|bool

- Пример 1, чтобы получить параметры свойства сетки для последнего представления на листе с именем `Sheet1`:

```go
var showGridLines excelize.ShowGridLines
err = f.GetSheetViewOptions("Sheet1", -1, &showGridLines)
```

- Пример 2:

```go
xl := excelize.NewFile()
const sheet = "Sheet1"

var (
    defaultGridColor  excelize.DefaultGridColor
    rightToLeft       excelize.RightToLeft
    showFormulas      excelize.ShowFormulas
    showGridLines     excelize.ShowGridLines
    showRowColHeaders excelize.ShowRowColHeaders
    zoomScale         excelize.ZoomScale
    topLeftCell       excelize.TopLeftCell
)

if err := xl.GetSheetViewOptions(sheet, 0,
    &defaultGridColor,
    &rightToLeft,
    &showFormulas,
    &showGridLines,
    &showRowColHeaders,
    &zoomScale,
    &topLeftCell,
); err != nil {
    panic(err)
}

fmt.Println("Default:")
fmt.Println("- defaultGridColor:", defaultGridColor)
fmt.Println("- rightToLeft:", rightToLeft)
fmt.Println("- showFormulas:", showFormulas)
fmt.Println("- showGridLines:", showGridLines)
fmt.Println("- showRowColHeaders:", showRowColHeaders)
fmt.Println("- zoomScale:", zoomScale)
fmt.Println("- topLeftCell:", `"`+topLeftCell+`"`)

if err := xl.SetSheetViewOptions(sheet, 0, excelize.TopLeftCell("B2")); err != nil {
    panic(err)
}

if err := xl.GetSheetViewOptions(sheet, 0, &topLeftCell); err != nil {
    panic(err)
}

if err := xl.SetSheetViewOptions(sheet, 0, excelize.ShowGridLines(false)); err != nil {
    panic(err)
}

if err := xl.GetSheetViewOptions(sheet, 0, &showGridLines); err != nil {
    panic(err)
}

fmt.Println("After change:")
fmt.Println("- showGridLines:", showGridLines)
fmt.Println("- topLeftCell:", topLeftCell)
```

вывод:

```text
Default:
- defaultGridColor: true
- rightToLeft: false
- showFormulas: false
- showGridLines: true
- showRowColHeaders: true
- zoomScale: 0
- topLeftCell: ""
After change:
- showGridLines: false
- topLeftCell: B2
```
