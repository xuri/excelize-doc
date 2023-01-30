# Рабочая книга

`Параметры` определяют параметры чтения и записи электронных таблиц.

```go
type Options struct {
    Password          string
    RawCellValue      bool
    UnzipSizeLimit    int64
    UnzipXMLSizeLimit int64
}
```

`Password` указывает пароль электронной таблицы в виде обычного текста.

`RawCellValue` указывает, применять ли числовой формат для значения ячейки или получить необработанное значение.

`UnzipSizeLimit` указывает предел размера распакованного архива в байтах при открытии электронной таблицы, это значение должно быть больше или равно `UnzipXMLSizeLimit`, ограничение размера по умолчанию составляет 16ГБ.

`UnzipXMLSizeLimit` указывает предел памяти при распаковке рабочего листа в байтах, XML рабочего листа будет извлечен во временный каталог системы, когда размер файла превышает это значение, это значение должно быть меньше или равно `UnzipSizeLimit`, значение по умолчанию - 16МБ.

## Создать документ Excel {#NewFile}

```go
func NewFile() *File
```

NewFile предоставляет функцию для создания нового файла по умолчанию. Вновь созданная рабочая книга по умолчанию будет содержать таблицу с именем `Sheet1`. Например:

## Открыть {#OpenFile}

```go
func OpenFile(filename string, opts ...Options) (*File, error)
```

OpenFile берет имя файла электронной таблицы и возвращает для него заполненную структуру файла электронной таблицы. Например, откройте электронную таблицу с защитой паролем:

```go
f, err := excelize.OpenFile("Book1.xlsx", excelize.Options{Password: "password"})
if err != nil {
    return
}
```

Закройте файл с помощью [`Close()`](workbook.md#Close) после открытия электронной таблицы.

## Открытый поток данных {#OpenReader}

```go
func OpenReader(r io.Reader, opts ...Options) (*File, error)
```

OpenReader считывает поток данных из `io.Reader` и возвращает заполненный файл электронной таблицы.

Например, создайте HTTP-сервер для обработки загружаемого шаблона, а затем загрузите ответный файл с новым рабочим листом:

```go
package main

import (
    "fmt"
    "net/http"

    "github.com/xuri/excelize/v2"
)

func process(w http.ResponseWriter, req *http.Request) {
    file, _, err := req.FormFile("file")
    if err != nil {
        fmt.Fprint(w, err.Error())
        return
    }
    defer file.Close()
    f, err := excelize.OpenReader(file)
    if err != nil {
        fmt.Fprint(w, err.Error())
        return
    }
    f.Path = "Book1.xlsx"
    f.NewSheet("NewSheet")
    w.Header().Set("Content-Disposition", fmt.Sprintf("attachment; filename=%s", f.Path))
    w.Header().Set("Content-Type", req.Header.Get("Content-Type"))
    if err := f.Write(w); err != nil {
        fmt.Fprint(w, err.Error())
    }
}

func main() {
    http.HandleFunc("/process", process)
    http.ListenAndServe(":8090", nil)
}
```

Тест с cURL:

```bash
curl --location --request GET 'http://127.0.0.1:8090/process' \
--form 'file=@/tmp/template.xltx' -O -J
```

## Сохранить {#Save}

```go
func (f *File) Save(opts ...Options) error
```

Save предоставляет функцию для переопределения файла xlsx с исходным путем.

## Сохранить как {#SaveAs}

```go
func (f *File) SaveAs(name string, opts ...Options) error
```

SaveAs предоставляет функцию для создания или обновления файла xlsx по предоставленному пути.

## Закрыть книгу {#Close}

```go
func (f *File) Close() error
```

Close закрывает и очищает открытый временный файл для электронной таблицы.

## Создать рабочий лист {#NewSheet}

```go
func (f *File) NewSheet(sheet string) (int, error)
```

NewSheet предоставляет функцию для создания нового листа по заданному имени рабочего листа и возвращает индекс листов в книге (электронной таблице) после его добавления. Обратите внимание, что при создании нового файла электронной таблицы будет создан рабочий лист по умолчанию с именем `Sheet1`.

## Удалить рабочий лист {#DeleteSheet}

```go
func (f *File) DeleteSheet(sheet string) error
```

DeleteSheet предоставляет функцию для удаления рабочего листа в рабочей книге по заданному имени рабочего листа, имена листов не чувствительны к регистру. Используйте этот метод с осторожностью, так как это повлияет на изменения в ссылках, таких как формулы, диаграммы и т. д. Если есть какое-либо ссылочное значение удаленного рабочего листа, это вызовет ошибку файла при его открытии. Эта функция будет недействительна, если останется только один рабочий лист.

## Лист копирования {#CopySheet}

```go
func (f *File) CopySheet(from, to int) error
```

CopySheet предоставляет функцию для дублирования рабочего листа путем указания индекса источника и целевого листа. Обратите внимание, что в настоящее время не поддерживается дублирование книг, содержащих таблицы, диаграммы или изображения. Например:

```go
// Sheet1 уже существует...
index, err := f.NewSheet("Sheet2")
if err != nil {
    fmt.Println(err)
    return
}
err := f.CopySheet(1, index)
```

## Рабочие листы группы {#GroupSheets}

```go
func (f *File) GroupSheets(sheets []string) error
```

GroupSheets предоставляет функцию для группировки листов по заданным именам листов. Рабочие листы групп должны содержать активный рабочий лист.

## Разгруппировать листы {#UngroupSheets}

```go
func (f *File) UngroupSheets() error
```

UngroupSheets предоставляет функцию для разгруппировки листов.

## Фон рабочего листа {#SetSheetBackground}

```go
func (f *File) SetSheetBackground(sheet, picture string) error
```

SetSheetBackground предоставляет функцию для установки фонового изображения по заданному имени рабочего листа и пути к файлу. Поддерживаемые типы изображений: EMF, EMZ, GIF, JPEG, JPG, PNG, SVG, TIF, TIFF, WMF и WMZ.

```go
func (f *File) SetSheetBackgroundFromBytes(sheet, extension string, picture []byte) error
```

SetSheetBackgroundFromBytes предоставляет функцию для установки фонового изображения по заданному имени рабочего листа, имени расширения и данным изображения. Поддерживаемые типы изображений: EMF, EMZ, GIF, JPEG, JPG, PNG, SVG, TIF, TIFF, WMF и WMZ.

## Установить рабочий лист по умолчанию {#SetActiveSheet}

```go
func (f *File) SetActiveSheet(index int)
```

SetActiveSheet предоставляет функцию для установки активного листа книги по умолчанию по заданному индексу. Обратите внимание, что активный индекс отличается от идентификатора, возвращаемого функцией [`GetSheetMap`](sheet.md#GetSheetMap). Оно должно быть больше или равно `0` и меньше общего числа листов.

## Получить активный индекс листа {#GetActiveSheetIndex}

```go
func (f *File) GetActiveSheetIndex() int
```

GetActiveSheetIndex предоставляет функцию для получения активного листа XLSX. Если не найден, активный лист вернет целое число `0`.

## Сделать лист видимым {#SetSheetVisible}

```go
func (f *File) SetSheetVisible(sheet string, visible bool, veryHidden ...bool) error
```

SetSheetVisible предоставляет функцию для установки рабочего листа, видимого по заданному имени рабочего листа. Рабочая книга должна содержать хотя бы одну видимую рабочую таблицу. Если данный лист был активирован, этот параметр будет недействительным. Третий необязательный параметр `veryHidden` работает только тогда, когда `visible` имеет значение `false`.

Например, скрыть `Sheet1`:

```go
err := f.SetSheetVisible("Sheet1", false)
```

## Получить рабочий лист видимым {#GetSheetVisible}

```go
func (f *File) GetSheetVisible(sheet string) (bool, error)
```

GetSheetVisible предоставляет функцию для отображения рабочего листа по заданному имени. Например, получить видимое состояние `Sheet1`:

```go
visible, err := f.GetSheetVisible("Sheet1")
```

## Установить свойства листа {#SetSheetProps}

```go
func (f *File) SetSheetProps(sheet string, opts *SheetPropsOptions) error
```

SetSheetProps предоставляет функцию для задания свойств листа. Можно задать следующие свойства:

Параметры|Тип|Описание
---|---|---
CodeName                          | `*string`  | Задает стабильное имя листа, которое не должно меняться со временем и не изменяется в результате ввода данных пользователем. Это имя должно использоваться кодом для ссылки на конкретный лист
EnableFormatConditionsCalculation | `*bool`    | Указание на то, должны ли оцениваться вычисления условного форматирования. Если задано значение false, то минимальные/максимальные значения цветовых шкал или полос данных или пороговых значений в правилах Top N не обновляются. По сути, условное форматирование "calc" выключено
Published                         | `*bool`    | Указывая, опубликован ли лист, значение по умолчанию равно `true`
AutoPageBreaks                    | `*bool`    | Указывая, отображается ли на листе автоматические разрывы страниц, значение по умолчанию равно `true`
FitToPage                         | `*bool`    | Указывая, включен ли параметр печати "По размеру страницы", значение по умолчанию равно `false`
TabColorIndexed                   | `*int`     | Представляет индексированное значение цвета
TabColorRGB                       | `*string`  | Представляет стандартное значение цвета ARGB (альфа-красный зеленый синий)
TabColorTheme                     | `*int`     | Представляет отсчитываемый от нуля индекс в коллекции, ссылаясь на определенное значение, выраженное в части Theme
TabColorTint                      | `*float64` | Задает значение оттенка, примененное к цвету, значение по умолчанию равно `0.0`
OutlineSummaryBelow               | `*bool`    | Указывая, отображаются ли сводные строки ниже подробных сведений в структуре, при применении структуры значение по умолчанию равно `true`
OutlineSummaryRight               | `*bool`    | Указывая, отображаются ли сводные столбцы справа от деталей в структуре, при применении структуры значение по умолчанию равно `true`
BaseColWidth                      | `*uint8`   | Задает количество символов максимальной ширины цифры шрифта обычного стиля. Это значение не включает заполнение полей или дополнительное заполнение для линий сетки. Это только количество символов, значение по умолчанию `8`
DefaultColWidth                   | `*float64` | Задает ширину столбца по умолчанию, измеряемую как количество символов максимальной ширины цифры шрифта обычного стиля
DefaultRowHeight                  | `*float64` | Задает высоту строки по умолчанию, измеряемую в размере точки. Оптимизация, поэтому нам не нужно писать высоту на всех строках. Это может быть выписано, если большинство строк имеют пользовательскую высоту, для достижения оптимизации
CustomHeight                      | `*bool`    | Задает пользовательскую высоту, значение по умолчанию равно `false`
ZeroHeight                        | `*bool`    | Указывает, что если строки скрыты, значение по умолчанию равно `false`
ThickTop                          | `*bool`    | Указывает, что если строки по умолчанию имеют толстую верхнюю границу, то значение по умолчанию равно `false`
ThickBottom                       | `*bool`    | Указывает, что если строки по умолчанию имеют толстую нижнюю границу, то значение по умолчанию равно `false`

Например, сделать строки на листе по умолчанию скрытыми:

<p align="center"><img width="612" src="./images/sheet_format_pr_01.png" alt="Установить свойства листа"></p>

```go
f, enable := excelize.NewFile(), true
if err := f.SetSheetProps("Sheet1", &excelize.SheetPropsOptions{
    ZeroHeight: &enable,
}); err != nil {
    fmt.Println(err)
}
if err := f.SetRowVisible("Sheet1", 10, true); err != nil {
    fmt.Println(err)
}
f.SaveAs("Book1.xlsx")
```

## Получить свойства листа {#SetSheetProps}

```go
func (f *File) GetSheetProps(sheet string) (SheetPropsOptions, error)
```

GetSheetProps предоставляет функцию для получения свойств листа. Можно задать следующие свойства:

Параметры|Тип|Описание
---|---|---
DefaultGridColor  | `*bool`    | Указание на то, что потребляющее приложение должно использовать цвет линий сетки по умолчанию (зависит от системы). Переопределяет любой цвет, указанный в colorId, значение по умолчанию равно `true`
RightToLeft       | `*bool`    | Указание на то, находится ли лист в режиме отображения «справа налево». В этом режиме столбец A находится в крайнем правом углу, столбец B; на один столбец слева от столбца A и так далее. Также информация в ячейках отображается в формате справа налево, значение по умолчанию равно `false`
ShowFormulas      | `*bool`    | Указывая, должен ли этот лист отображать формулы, значение по умолчанию равно `false`
ShowGridLines     | `*bool`    | Указывая, должен ли этот лист отображать линии сетки, значение по умолчанию равно `true`
ShowRowColHeaders | `*bool`    | Указывая, должен ли лист отображать заголовки строк и столбцов, значение по умолчанию равно `true`
ShowRuler         | `*bool`    | Указывая, что на этом листе должна отображаться линейка, значение по умолчанию равно `true`
ShowZeros         | `*bool`    | Указание на то, следует ли "показывать ноль в ячейках, имеющих нулевое значение". При использовании формулы для ссылки на другую ячейку, которая пуста, указанное значение становится `0`, когда флаг `true`, значение по умолчанию `true`
TopLeftCell       | `*string`  | Задает расположение левой видимой верхней ячейки Расположение левой видимой ячейки в правой нижней панели (в режиме слева направо)
View              | `*string`  | Указывая, как отображается лист, по умолчанию он использует пустую строку, доступные опции: `normal`, `pageBreakPreview` и `pageLayout`
ZoomScale         | `*float64` | Задает увеличение масштаба окна для текущего представления, представляющего значения в процентах. Этот атрибут ограничен значениями в диапазоне от `10` до `400`. Горизонтальный и вертикальный масштаб вместе, значение по умолчанию равно `100`

## Задать свойства представления листа {#SetSheetView}

```go
func (f *File) SetSheetView(sheet string, viewIndex int, opts *ViewOptions) error
```

SetSheetView задает свойства представления листа. `viewIndex` может быть отрицательным, и если это так, то отсчитывается в обратном порядке (`-1` - последнее представление).

## Получить свойства вида листа {#GetSheetView}

```go
func (f *File) GetSheetView(sheet string, viewIndex int) (ViewOptions, error)
```

GetSheetView получает значение свойств представления листа. `viewIndex` может быть отрицательным, и если это так, то отсчитывается в обратном порядке (`-1` - последнее представление).

## Установить макет страницы листа {#SetPageLayout}

```go
func (f *File) SetPageLayout(sheet string, opts *PageLayoutOptions) error
```

SetPageLayout предоставляет функцию для установки макета страницы листа Доступные Варианты:

`Size` предоставляет метод для установки размера бумаги на листе, по умолчанию размер листа составляет "Letter 8S × 11 дюймов". Ниже показан формат бумаги, отсортированный по номеру индекса Excelize:

Индекс | Размер бумаги
---|---
1   | Letter paper (8.5 in. × 11 in.)
2   | Letter small paper (8.5 in. × 11 in.)
3   | Tabloid paper (11 in. × 17 in.)
4   | Ledger paper (17 in. × 11 in.)
5   | Legal paper (8.5 in. × 14 in.)
6   | Statement paper (5.5 in. × 8.5 in.)
7   | Executive paper (7.25 in. × 10.5 in.)
8   | A3 paper (297 mm × 420 mm)
9   | A4 paper (210 mm × 297 mm)
10  | A4 small paper (210 mm × 297 mm)
11  | A5 paper (148 mm × 210 mm)
12  | B4 paper (250 mm × 353 mm)
13  | B5 paper (176 mm × 250 mm)
14  | Folio paper (8.5 in. × 13 in.)
15  | Quarto paper (215 mm × 275 mm)
16  | Standard paper (10 in. × 14 in.)
17  | Standard paper (11 in. × 17 in.)
18  | Note paper (8.5 in. × 11 in.)
19  | #9 envelope (3.875 in. × 8.875 in.)
20  | #10 envelope (4.125 in. × 9.5 in.)
21  | #11 envelope (4.5 in. × 10.375 in.)
22  | #12 envelope (4.75 in. × 11 in.)
23  | #14 envelope (5 in. × 11.5 in.)
24  | C paper (17 in. × 22 in.)
25  | D paper (22 in. × 34 in.)
26  | E paper (34 in. × 44 in.)
27  | DL envelope (110 mm × 220 mm)
28  | C5 envelope (162 mm × 229 mm)
29  | C3 envelope (324 mm × 458 mm)
30  | C4 envelope (229 mm × 324 mm)
31  | C6 envelope (114 mm × 162 mm)
32  | C65 envelope (114 mm × 229 mm)
33  | B4 envelope (250 mm × 353 mm)
34  | B5 envelope (176 mm × 250 mm)
35  | B6 envelope (176 mm × 125 mm)
36  | Italy envelope (110 mm × 230 mm)
37  | Monarch envelope (3.875 in. × 7.5 in.).
38  | 6¾ envelope (3.625 in. × 6.5 in.)
39  | US standard fanfold (14.875 in. × 11 in.)
40  | German standard fanfold (8.5 in. × 12 in.)
41  | German legal fanfold (8.5 in. × 13 in.)
42  | ISO B4 (250 mm × 353 mm)
43  | Japanese postcard (100 mm × 148 mm)
44  | Standard paper (9 in. × 11 in.)
45  | Standard paper (10 in. × 11 in.)
46  | Standard paper (15 in. × 11 in.)
47  | Invite envelope (220 mm × 220 mm)
50  | Letter extra paper (9.275 in. × 12 in.)
51  | Legal extra paper (9.275 in. × 15 in.)
52  | Tabloid extra paper (11.69 in. × 18 in.)
53  | A4 extra paper (236 mm × 322 mm)
54  | Letter transverse paper (8.275 in. × 11 in.)
55  | A4 transverse paper (210 mm × 297 mm)
56  | Letter extra transverse paper (9.275 in. × 12 in.)
57  | SuperA/SuperA/A4 paper (227 mm × 356 mm)
58  | SuperB/SuperB/A3 paper (305 mm × 487 mm)
59  | Letter plus paper (8.5 in. × 12.69 in.)
60  | A4 plus paper (210 mm × 330 mm)
61  | A5 transverse paper (148 mm × 210 mm)
62  | JIS B5 transverse paper (182 mm × 257 mm)
63  | A3 extra paper (322 mm × 445 mm)
64  | A5 extra paper (174 mm × 235 mm)
65  | ISO B5 extra paper (201 mm × 276 mm)
66  | A2 paper (420 mm × 594 mm)
67  | A3 transverse paper (297 mm × 420 mm)
68  | A3 extra transverse paper (322 mm × 445 mm)
69  | Japanese Double Postcard (200 mm × 148 mm)
70  | A6 (105 mm × 148 mm)
71  | Japanese Envelope Kaku #2
72  | Japanese Envelope Kaku #3
73  | Japanese Envelope Chou #3
74  | Japanese Envelope Chou #4
75  | Letter Rotated (11 × 8½ in.)
76  | A3 Rotated (420 mm × 297 mm)
77  | A4 Rotated (297 mm × 210 mm)
78  | A5 Rotated (210 mm × 148 mm)
79  | B4 (JIS) Rotated (364 mm × 257 mm)
80  | B5 (JIS) Rotated (257 mm × 182 mm)
81  | Japanese Postcard Rotated (148 mm × 100 mm)
82  | Double Japanese Postcard Rotated (148 mm × 200 mm)
83  | A6 Rotated (148 mm × 105 mm)
84  | Japanese Envelope Kaku #2 Rotated
85  | Japanese Envelope Kaku #3 Rotated
86  | Japanese Envelope Chou #3 Rotated
87  | Japanese Envelope Chou #4 Rotated
88  | B6 (JIS) (128 mm × 182 mm)
89  | B6 (JIS) Rotated (182 mm × 128 mm)
90  | (12 in × 11 in)
91  | Japanese Envelope You #4
92  | Japanese Envelope You #4 Rotated
93  | PRC 16K (146 mm × 215 mm)
94  | PRC 32K (97 mm × 151 mm)
95  | PRC 32K(Big) (97 mm × 151 mm)
96  | PRC Envelope #1 (102 mm × 165 mm)
97  | PRC Envelope #2 (102 mm × 176 mm)
98  | PRC Envelope #3 (125 mm × 176 mm)
99  | PRC Envelope #4 (110 mm × 208 mm)
100 | PRC Envelope #5 (110 mm × 220 mm)
101 | PRC Envelope #6 (120 mm × 230 mm)
102 | PRC Envelope #7 (160 mm × 230 mm)
103 | PRC Envelope #8 (120 mm × 309 mm)
104 | PRC Envelope #9 (229 mm × 324 mm)
105 | PRC Envelope #10 (324 mm × 458 mm)
106 | PRC 16K Rotated
107 | PRC 32K Rotated
108 | PRC 32K(Big) Rotated
109 | PRC Envelope #1 Rotated (165 mm × 102 mm)
110 | PRC Envelope #2 Rotated (176 mm × 102 mm)
111 | PRC Envelope #3 Rotated (176 mm × 125 mm)
112 | PRC Envelope #4 Rotated (208 mm × 110 mm)
113 | PRC Envelope #5 Rotated (220 mm × 110 mm)
114 | PRC Envelope #6 Rotated (230 mm × 120 mm)
115 | PRC Envelope #7 Rotated (230 mm × 160 mm)
116 | PRC Envelope #8 Rotated (309 mm × 120 mm)
117 | PRC Envelope #9 Rotated (324 mm × 229 mm)
118 | PRC Envelope #10 Rotated (458 mm × 324 mm)

`Orientation` указанная ориентация листа, по умолчанию — `portrait`. Возможные значения для этого поля — `portrait` и `landscape`.

`FirstPageNumber` указывает номер первой печатной страницы. Если значение не указано, то предполагается «автоматический».

`AdjustTo` указывает масштабирование печати. Этот атрибут ограничен значениями в диапазоне от 10 (10%) до 400 (400%). Этот параметр переопределяется, когда используются `FitToWidth` и/или `FitToHeight`.

`FitToHeight` указал количество вертикальных страниц, на которые можно поместиться.

`FitToWidth` указывал количество горизонтальных страниц, на которые можно поместиться.

`BlackAndWhite` указал печать черно-белую.

Например, установите макет страницы для `Sheet1` с черно-белой печатью, номер первой напечатанной страницы от `2`, альбомная ориентация на маленькую бумагу A4 (210 мм на 297 мм), 2 вертикальные страницы для размещения и 2 горизонтальные страницы для размещения:

```go
f := excelize.NewFile()
var (
    size                 = 10
    orientation          = "landscape"
    firstPageNumber uint = 2
    adjustTo        uint = 100
    fitToHeight          = 2
    fitToWidth           = 2
    blackAndWhite        = true
)
if err := f.SetPageLayout("Sheet1", &excelize.PageLayoutOptions{
    Size:            &size,
    Orientation:     &orientation,
    FirstPageNumber: &firstPageNumber,
    AdjustTo:        &adjustTo,
    FitToHeight:     &fitToHeight,
    FitToWidth:      &fitToWidth,
    BlackAndWhite:   &blackAndWhite,
}); err != nil {
    fmt.Println(err)
}
```

## Получить макет страницы листа {#GetPageLayout}

```go
func (f *File) GetPageLayout(sheet string) (PageLayoutOptions, error)
```

GetPageLayout предоставляет функцию для получения макета страницы листа.

## Задать поля страницы листа {#SetPageMargins}

```go
func (f *File) SetPageMargins(sheet string, opts *PageLayoutMarginsOptions) error
```

SetPageMargins предоставляет функцию для установки полей страницы рабочего листа. Доступные Варианты:

Параметры|Тип|Описание
---|---|---
Bottom | *float64 | Дно
Footer | *float64 | Колонтитул
Header | *float64 | Заголовок
Left | *float64 | Ліворуч
Right | *float64 | Правильно
Top | *float64 | Топ
Horizontally | *bool | Центр на странице: горизонтально
Vertically | *bool | По центру на странице: по вертикали

## Получить поля страницы листа {#GetPageMargins}

```go
func (f *File) GetPageMargins(sheet string) (PageLayoutMarginsOptions, error)
```

GetPageMargins предоставляет функцию для получения полей страницы рабочего листа.

## Установить свойства книги {#SetWorkbookProps}

```go
func (f *File) SetWorkbookProps(opts *WorkbookPropsOptions) error
```

SetWorkbookProps предоставляет функцию для установки свойств книги. Доступные Варианты:

Параметры|Тип|Описание
---|---|---
Date1904      | `*bool`   | Указывает, следует ли использовать систему дат 1900 или 1904 годов при преобразовании последовательной даты и времени в книге в даты.
FilterPrivacy | `*bool`   | Задает логическое значение, указывающее, проверило ли приложение книгу на наличие личных сведений ( PII). Если этот флаг установлен, приложение предупреждает пользователя каждый раз, когда пользователь выполняет действие, которое вставляет PII в документ.
CodeName      | `*string` | Задает кодовое имя приложения, создавшего эту книгу. Этот атрибут используется для отслеживания содержимого файла в добавочных выпусках приложения.

## Получить свойства книги {#GetWorkbookProps}

```go
func (f *File) GetWorkbookProps() (WorkbookPropsOptions, error)
```

GetWorkbookProps предоставляет функцию для получения свойств книги.

## Установить верхний и нижний колонтитулы {#SetHeaderFooter}

```go
func (f *File) SetHeaderFooter(sheet string, opts *HeaderFooterOptions) error
```

SetHeaderFooter предоставляет функцию установки верхних и нижних колонтитулов по заданному имени рабочего листа и управляющим символам.

Верхние и нижние колонтитулы указываются с помощью следующих полей настроек:

Поля | Описание
---|---
AlignWithMargins | Выравнивание полей нижнего колонтитула с полями страницы
DifferentFirst   | Различные индикаторы верхнего и нижнего колонтитула первой страницы
DifferentOddEven | Различные нечетные и четные заголовки страниц и индикатор нижних колонтитулов
ScaleWithDoc     | Масштабирование верхнего и нижнего колонтитула с масштабированием документа
OddFooter        | Нижний колонтитул нечетной страницы
OddHeader        | Нечетный заголовок
EvenFooter       | Нижний колонтитул четной страницы
EvenHeader       | Заголовок четной страницы
FirstFooter      | Нижний колонтитул первой страницы
FirstHeader      | Заголовок первой страницы

Следующие коды форматирования могут использоваться в 6 полях строкового типа: `OddHeader`, `OddFooter`, `EvenHeader`, `EvenFooter`, `FirstFooter`, `FirstHeader`

<table>
    <thead>
        <tr>
            <th>Код форматирования</th>
            <th>Описание</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>&amp;&amp;</code></td>
            <td>Персонаж &quot;&amp;&quot;</td>
        </tr>
        <tr>
            <td><code>&amp;font-size</code></td>
            <td>Размер шрифта текста, где font-size — десятичный размер шрифта в пунктах</td>
        </tr>
        <tr>
            <td><code>&amp;&quot;font name,font type&quot;</code></td>
            <td>Текстовая строка font-name, имя шрифта и текстовая строка font-type, тип шрифта</td>
        </tr>
        <tr>
            <td><code>&amp;&quot;-,Regular&quot;</code></td>
            <td>Обычный текстовый формат. Отключает полужирный и курсивный режимы</td>
        </tr>
        <tr>
            <td><code>&amp;A</code></td>
            <td>Имя вкладки текущего рабочего листа</td>
        </tr>
        <tr>
            <td><code>&amp;B</code> or <code>&amp;&quot;-,Bold&quot;</code></td>
            <td>Формат полужирного текста, от выкл. к вкл. или наоборот. Режим по умолчанию выключен</td>
        </tr>
        <tr>
            <td><code>&amp;D</code></td>
            <td>Текущая дата</td>
        </tr>
        <tr>
            <td><code>&amp;C</code></td>
            <td>Центральная часть</td>
        </tr>
        <tr>
            <td><code>&amp;E</code></td>
            <td>Формат текста с двойным подчеркиванием</td>
        </tr>
        <tr>
            <td><code>&amp;F</code></td>
            <td>Имя файла текущей книги</td>
        </tr>
        <tr>
            <td><code>&amp;G</code></td>
            <td>Объект рисования в качестве фона (В настоящее время не поддерживается)</td>
        </tr>
        <tr>
            <td><code>&amp;H</code></td>
            <td>Формат теневого текста</td>
        </tr>
        <tr>
            <td><code>&amp;I</code> or <code>&amp;&quot;-,Italic&quot;</code></td>
            <td>Курсивный текстовый формат</td>
        </tr>
        <tr>
            <td><code>&amp;K</code></td>
            <td>Цвет шрифта текста<br>Цвет RGB указан как RRGGBB<br>Цвет темы указывается как TTSNNN, где TT — это идентификатор цвета темы, S — это &quot;+&quot; или &quot;-&quot; значения оттенка/оттенка, а NNN — это значение оттенка/оттенка.</td>
        </tr>
        <tr>
            <td><code>&amp;L</code></td>
            <td>Левая часть</td>
        </tr>
        <tr>
            <td><code>&amp;N</code></td>
            <td>Общее количество страниц</td>
        </tr>
        <tr>
            <td><code>&amp;O</code></td>
            <td>Контурный текстовый формат</td>
        </tr>
        <tr>
            <td><code>&amp;P[[+\|-]n]</code></td>
            <td>Без дополнительного суффикса номер текущей страницы в десятичном формате</td>
        </tr>
        <tr>
            <td><code>&amp;R</code></td>
            <td>Правая часть</td>
        </tr>
        <tr>
            <td><code>&amp;S</code></td>
            <td>Формат зачеркнутого текста</td>
        </tr>
        <tr>
            <td><code>&amp;T</code></td>
            <td>Текущее время</td>
        </tr>
        <tr>
            <td><code>&amp;U</code></td>
            <td>Формат текста с одним подчеркиванием. Если режим двойного подчеркивания включен, следующее вхождение в описателе раздела отключает режим двойного подчеркивания; в противном случае он переключает режим одинарного подчеркивания с выключенного на включенный или наоборот. Режим по умолчанию выключен</td>
        </tr>
        <tr>
            <td><code>&amp;X</code></td>
            <td>Надстрочный текстовый формат</td>
        </tr>
        <tr>
            <td><code>&amp;Y</code></td>
            <td>Текстовый формат нижнего индекса</td>
        </tr>
        <tr>
            <td><code>&amp;Z</code></td>
            <td>Путь к файлу текущей книги</td>
        </tr>
    </tbody>
</table>

Например:

```go
err := f.SetHeaderFooter("Sheet1", &excelize.HeaderFooterOptions{
    DifferentFirst:   true,
    DifferentOddEven: true,
    OddHeader:        "&R&P",
    OddFooter:        "&C&F",
    EvenHeader:       "&L&P",
    EvenFooter:       "&L&D&R&T",
    FirstHeader:      `&CCenter &"-,Bold"Bold&"-,Regular"HeaderU+000A&D`,
})
```

Этот пример показывает:

- Первая страница имеет свой собственный верхний и нижний колонтитулы
- Нечетные и четные страницы имеют разные верхние и нижние колонтитулы
- Номер текущей страницы в правой части заголовков нечетных страниц
- Имя файла текущей книги в центральной части нижнего колонтитула
- Номер текущей страницы в левой части заголовков четных страниц
- текущая дата в левом разделе и текущее время в правом разделе нижнего колонтитула четных страниц
- текст `Center Bold Header` в первой строке центральной части первой страницы и дата во второй строке центральной части той же страницы
- Нет нижнего колонтитула на первой странице

## Установить определенное имя {#SetDefinedName}

```go
func (f *File) SetDefinedName(definedName *DefinedName) error
```

SetDefinedName предоставляет функцию для установки определенных имен рабочей книги или рабочего листа. Если не указано scopr, областью по умолчанию является книга. Например:

```go
err := f.SetDefinedName(&excelize.DefinedName{
    Name:     "Amount",
    RefersTo: "Sheet1!$A$2:$D$5",
    Comment:  "defined name comment",
    Scope:    "Sheet2",
})
```

Параметры области печати и заголовков печати для рабочего листа:

<p align="center"><img width="755" src="./images/page_setup_01.png" alt="Параметры области печати и заголовков печати для рабочего листа"></p>

```go
if err := f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Area",
    RefersTo: "Sheet1!$A$1:$Z$100",
    Scope:    "Sheet1",
}); err != nil {
    fmt.Println(err)
}
if err := f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Titles",
    RefersTo: "Sheet1!$A:$A,Sheet1!$1:$1",
    Scope:    "Sheet1",
}); err != nil {
    fmt.Println(err)
}
```

## Получить определенное имя {#GetDefinedName}

```go
func (f *File) GetDefinedName() []DefinedName
```

GetDefinedName предоставляет функцию для получения определенных имен рабочей книги или рабочего листа.

## Удалить определенное имя {#DeleteDefinedName}

```go
func (f *File) DeleteDefinedName(definedName *DefinedName) error
```

DeleteDefinedName предоставляет функцию для удаления определенных имен рабочей книги или рабочего листа. Если не указана область, областью по умолчанию является рабочая книга. Например:

```go
err := f.DeleteDefinedName(&excelize.DefinedName{
    Name:     "Amount",
    Scope:    "Sheet2",
})
```

## Установить свойства приложения {#SetAppProps}

```go
func (f *File) SetAppProps(appProperties *AppProperties) error
```

SetAppProps предоставляет функцию для установки свойств приложения документа. Можно установить следующие свойства:

Недвижимость   | Описание
---|---
Application       | Имя приложения, создавшего этот документ.
ScaleCrop         | Указывает режим отображения эскиза документа. Установите для этого элемента значение `true`, чтобы разрешить масштабирование миниатюры документа для отображения. Установите для этого элемента значение `false`, чтобы разрешить обрезку эскиза документа, чтобы отображались только те разделы, которые подходят для отображения.
DocSecurity       | Уровень безопасности документа как числовое значение. Безопасность документа определяется как:<br>1 - Документ защищен паролем<br>2 - Документ рекомендуется открывать только для чтения<br>3 - Документ принудительно открывается только для чтения<br>4 - документ заблокирован для аннотации
Company           | The name of a company associated with the document.
LinksUpToDate     | Указывает, актуальны ли гиперссылки в документе. Установите для этого элемента значение `true`, чтобы указать, что гиперссылки обновлены. Установите для этого элемента значение `false`, чтобы указать, что гиперссылки устарели.
HyperlinksChanged | Указывает, что одна или несколько гиперссылок в этой части были обновлены исключительно в этой части производителем. Следующий производитель, который откроет этот документ, должен обновить отношения гиперссылок новыми гиперссылками, указанными в этой части.
AppVersion        | Задает версию приложения, создавшего этот документ. Содержание этого элемента должно иметь форму XX.YYYY, где X и Y представляют собой числовые значения, в противном случае документ будет считаться несоответствующим.

Например:

```go
err := f.SetAppProps(&excelize.AppProperties{
    Application:       "Microsoft Excel",
    ScaleCrop:         true,
    DocSecurity:       3,
    Company:           "Company Name",
    LinksUpToDate:     true,
    HyperlinksChanged: true,
    AppVersion:        "16.0000",
})
```

## Получить свойства приложения {#GetAppProps}

```go
func (f *File) GetAppProps() (*AppProperties, error)
```

GetAppProps предоставляет функцию для получения свойств приложения документа.

## Установить свойства документа {#SetDocProps}

```go
func (f *File) SetDocProps(docProperties *DocProperties) error
```

SetDocProps предоставляет функцию для установки основных свойств документа. Свойства, которые можно установить:

Недвижимость   | Описание
---|---
Category       | Категоризация содержимого этого пакета.
ContentStatus  | Статус контента. Например: значения могут включать `Draft`, `Reviewed` и `Final`
Created        | Время создания содержимого ресурса.
Creator        | Сущность, в первую очередь ответственная за создание контента ресурса.
Description    | Разъяснение содержания ресурса.
Identifier     | Однозначная ссылка на ресурс в данном контексте.
Keywords       | Набор ключевых слов с разделителями для поддержки поиска и индексации. Обычно это список терминов, которые недоступны в других местах свойств.
Language       | Язык интеллектуального содержания ресурса.
LastModifiedBy | Пользователь, который выполнил последнюю модификацию. Идентификация зависит от окружающей среды.
Modified       | Время модификации содержимого ресурса.
Revision       | Номер редакции содержимого ресурса.
Subject        | Тема о содержании ресурса.
Title          | Название, данное ресурсу.
Version        | Номер версии. Это значение задается пользователем или приложением.

Например:

```go
err := f.SetDocProps(&excelize.DocProperties{
    Category:       "category",
    ContentStatus:  "Draft",
    Created:        "2019-06-04T22:00:10Z",
    Creator:        "Go Excelize",
    Description:    "This file created by Go Excelize",
    Identifier:     "xlsx",
    Keywords:       "Spreadsheet",
    LastModifiedBy: "Go Author",
    Modified:       "2019-06-04T22:00:10Z",
    Revision:       "0",
    Subject:        "Test Subject",
    Title:          "Test Title",
    Language:       "en-US",
    Version:        "1.0.0",
})
```

## Получить свойства документа {#GetDocProps}

```go
func (f *File) GetDocProps() (*DocProperties, error)
```

GetDocProps предоставляет функцию для получения основных свойств документа.

## Защитить книгу {#ProtectWorkbook}

```go
func (f *File) ProtectWorkbook(opts *WorkbookProtectionOptions) error
```

ProtectWorkbook предоставляет функцию для предотвращения случайного или преднамеренного изменения, перемещения или удаления данных в книге другими пользователями. В необязательном поле `AlgorithmName` указывается хеш-алгоритм, поддерживается XOR, MD4, MD5, SHA-1, SHA2-56, SHA-384 и SHA-512. В настоящее время, если хэш-алгоритм не указан, будет использоваться алгоритм XOR по умолчанию. Например, защитите книгу с помощью параметров защиты:

```go
err := f.ProtectWorkbook(&excelize.WorkbookProtectionOptions{
    Password:      "password",
    LockStructure: true,
})
```

WorkbookProtectionOptions напрямую отображает параметры защиты книги.

```go
type WorkbookProtectionOptions struct {
    AlgorithmName string
    Password      string
    LockStructure bool
    LockWindows   bool
}
```

## Снять защиту с книги {#UnprotectWorkbook}

```go
func (f *File) UnprotectWorkbook(password ...string) error
```

UnprotectWorkbook предоставляет функцию для снятия защиты книги, для которой указан необязательный параметр пароля, чтобы снять защиту книги с проверкой пароля.
