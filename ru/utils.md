# Функция инструмента

ZipWriter определяет интерфейс для записи файлов в ZIP-архив. Он предоставляет методы для создания новых файлов в архиве, добавления файлов из файловой системы и закрытия архива после завершения записи.

```go
type ZipWriter interface {
    Create(name string) (io.Writer, error)
    AddFS(fsys fs.FS) error
    Close() error
}
```

## Добавить таблицу {#AddTable}

```go
func (f *File) AddTable(sheet string, table *Table) error
```

AddTable предоставляет метод для добавления таблицы в рабочий лист с помощью заданного имени рабочего листа, области координат и формата.

- Пример 1, создайте таблицу `A1:D5` на `Sheet1`:

<p align="center"><img width="612" src="./images/addtable_01.png" alt="Добавить таблицу"></p>

```go
err := f.AddTable("Sheet1", &excelize.Table{Range: "A1:D5"})
```

- Пример 2, создайте таблицу `F2:H6` на `Sheet2` с установленным форматом:

<p align="center"><img width="612" src="./images/addtable_02.png" alt="Добавить таблицу с установленным форматом"></p>

```go
disable := false
err := f.AddTable("Sheet2", &excelize.Table{
    Range:             "F2:H6",
    Name:              "table",
    StyleName:         "TableStyleMedium2",
    ShowFirstColumn:   true,
    ShowLastColumn:    true,
    ShowRowStripes:    &disable,
    ShowColumnStripes: true,
})
```

Обратите внимание, что таблица должна содержать не менее двух строк, включая заголовок. Ячейки заголовка должны содержать строки и должны быть уникальными, а также должны устанавливать данные строки заголовка таблицы перед вызовом функции AddTable. Несколько таблиц координируют области, которые не могут иметь пересечения.

`Name`: Имя таблицы в том же листе таблицы таблицы должно быть уникальным.

`StyleName`: Встроенные имена стиля таблицы:

```text
TableStyleLight1 - TableStyleLight21
TableStyleMedium1 - TableStyleMedium28
TableStyleDark1 - TableStyleDark11
```

Индекс|Стиль|Индекс|Стиль|Индекс|Стиль
---|---|---|---|---|---
|<img src="../images/table_style/light/0.png" width="61">|TableStyleLight1|<img src="../images/table_style/light/1.png" width="61">|TableStyleLight2|<img src="../images/table_style/light/2.png" width="61">
TableStyleLight3|<img src="../images/table_style/light/3.png" width="61">|TableStyleLight4|<img src="../images/table_style/light/4.png" width="61">|TableStyleLight5|<img src="../images/table_style/light/5.png" width="61">
TableStyleLight6|<img src="../images/table_style/light/6.png" width="61">|TableStyleLight7|<img src="../images/table_style/light/7.png" width="61">|TableStyleLight8|<img src="../images/table_style/light/8.png" width="61">
TableStyleLight9|<img src="../images/table_style/light/9.png" width="61">|TableStyleLight10|<img src="../images/table_style/light/10.png" width="61">|TableStyleLight11|<img src="../images/table_style/light/11.png" width="61">
TableStyleLight12|<img src="../images/table_style/light/12.png" width="61">|TableStyleLight13|<img src="../images/table_style/light/13.png" width="61">|TableStyleLight14|<img src="../images/table_style/light/14.png" width="61">
TableStyleLight15|<img src="../images/table_style/light/15.png" width="61">|TableStyleLight16|<img src="../images/table_style/light/16.png" width="61">|TableStyleLight17|<img src="../images/table_style/light/17.png" width="61">
TableStyleLight18|<img src="../images/table_style/light/18.png" width="61">|TableStyleLight19|<img src="../images/table_style/light/19.png" width="61">|TableStyleLight20|<img src="../images/table_style/light/20.png" width="61">
TableStyleLight21|<img src="../images/table_style/light/21.png" width="61">|TableStyleMedium1|<img src="../images/table_style/medium/1.png" width="61">|TableStyleMedium2|<img src="../images/table_style/medium/2.png" width="61">
TableStyleMedium3|<img src="../images/table_style/medium/3.png" width="61">|TableStyleMedium4|<img src="../images/table_style/medium/4.png" width="61">|TableStyleMedium5|<img src="../images/table_style/medium/5.png" width="61">
TableStyleMedium6|<img src="../images/table_style/medium/6.png" width="61">|TableStyleMedium7|<img src="../images/table_style/medium/7.png" width="61">|TableStyleMedium8|<img src="../images/table_style/medium/8.png" width="61">
TableStyleMedium9|<img src="../images/table_style/medium/9.png" width="61">|TableStyleMedium10|<img src="../images/table_style/medium/10.png" width="61">|TableStyleMedium11|<img src="../images/table_style/medium/11.png" width="61">
TableStyleMedium12|<img src="../images/table_style/medium/12.png" width="61">|TableStyleMedium13|<img src="../images/table_style/medium/13.png" width="61">|TableStyleMedium14|<img src="../images/table_style/medium/14.png" width="61">
TableStyleMedium15|<img src="../images/table_style/medium/15.png" width="61">|TableStyleMedium16|<img src="../images/table_style/medium/16.png" width="61">|TableStyleMedium17|<img src="../images/table_style/medium/17.png" width="61">
TableStyleMedium18|<img src="../images/table_style/medium/18.png" width="61">|TableStyleMedium19|<img src="../images/table_style/medium/19.png" width="61">|TableStyleMedium20|<img src="../images/table_style/medium/20.png" width="61">
TableStyleMedium21|<img src="../images/table_style/medium/21.png" width="61">|TableStyleMedium22|<img src="../images/table_style/medium/22.png" width="61">|TableStyleMedium23|<img src="../images/table_style/medium/23.png" width="61">
TableStyleMedium24|<img src="../images/table_style/medium/24.png" width="61">|TableStyleMedium25|<img src="../images/table_style/medium/25.png" width="61">|TableStyleMedium26|<img src="../images/table_style/medium/26.png" width="61">
TableStyleMedium27|<img src="../images/table_style/medium/27.png" width="61">|TableStyleMedium28|<img src="../images/table_style/medium/28.png" width="61">|TableStyleDark1|<img src="../images/table_style/dark/1.png" width="61">
TableStyleDark2|<img src="../images/table_style/dark/2.png" width="61">|TableStyleDark3|<img src="../images/table_style/dark/3.png" width="61">|TableStyleDark4|<img src="../images/table_style/dark/4.png" width="61">
TableStyleDark5|<img src="../images/table_style/dark/5.png" width="61">|TableStyleDark6|<img src="../images/table_style/dark/6.png" width="61">|TableStyleDark7|<img src="../images/table_style/dark/7.png" width="61">
TableStyleDark8|<img src="../images/table_style/dark/8.png" width="61">|TableStyleDark9|<img src="../images/table_style/dark/9.png" width="61">|TableStyleDark10|<img src="../images/table_style/dark/10.png" width="61">
TableStyleDark11|<img src="../images/table_style/dark/11.png" width="61">||||

## Получить таблицы {#GetTables}

```go
func (f *File) GetTables(sheet string) ([]Table, error)
```

GetTables предоставляет метод для получения всех таблиц на листе по заданному имени листа.

## Удалить таблицу {#DeleteTable}

```go
func (f *File) DeleteTable(name string) error
```

DeleteTable предоставляет метод удаления таблицы по заданному имени таблицы.

## Авто фильтр {#AutoFilter}

```go
func (f *File) AutoFilter(sheet, rangeRef string, opts []AutoFilterOptions) error
```

AutoFilter предоставляет метод добавления автоматического фильтра в рабочий лист с помощью имени рабочего листа, области координат и настроек. Автофильтр в Excel представляет собой способ фильтрации 2D спектра данных на основе простых критериев.

Пример 1, применяя автоматический фильтр к диапазону ячеек `A1:D4` в `Sheet1`:

<p align="center"><img width="612" src="./images/autofilter_01.png" alt="Добавить автоматический фильтр"></p>

```go
err := f.AutoFilter("Sheet1", "A1:D4", []excelize.AutoFilterOptions{})
```

Пример 2, данные фильтра в автофильтре:

```go
err := f.AutoFilter("Sheet1", "A1:D4", []excelize.AutoFilterOptions{
    {Column: "B", Expression: "x != blanks"},
})
```

`Column` определяет столбцы фильтра в диапазоне автоматического фильтра на основе простых критериев

Недостаточно просто указать условие фильтра. Вы также должны скрыть любые строки, которые не соответствуют условию фильтра. Строки скрыты с помощью метода [`SetRowVisible()`](sheet.md#SetRowVisible). Excelize не может автоматически фильтровать строки, поскольку это не является частью формата файла.

Установка критериев фильтра для столбца:

`Expression` определяет условия, доступны следующие операторы для установки критериев фильтра:

```text
==
!=
>
<
>=
<=
and
or
```

Выражение может содержать один оператор или два оператора, разделенных операторами `and` и `or`. Например:

```text
x <  2000
x >  2000
x == 2000
x >  2000 and x <  5000
x == 2000 or  x == 5000
```

Фильтрация пустых или непустых данных может быть достигнута путем использования значения Бланков или NonBlanks в выражении:

```text
x == Blanks
x == NonBlanks
```

Office Excel также позволяет выполнять некоторые простые операции сопоставления строк:

```text
x == b*      // начинается с b
x != b*      // не начинается с b
x == *b      // заканчивается буквой b
x != *b      // не заканчивается на b
x == *b*     // содержит b
x != *b*     // не содержит b
```

Вы также можете использовать `*` для соответствия любому символу или номеру и `?` Для соответствия любому одиночному символу или номеру. Фильтры Excel не поддерживаются никаким другим квантором регулярных выражений. Символы регулярного выражения Excel могут быть экранированы с помощью `~`.

Замещающая переменная `x` в приведенных выше примерах может быть заменена любой простой строкой. Фактическое имя заполнителя игнорируется внутренне, поэтому следующие эквиваленты:

```text
x     < 2000
col   < 2000
Price < 2000
```

## Обновить связанное значение {#UpdateLinkedValue}

```go
func (f *File) UpdateLinkedValue() error
```

UpdateLinkedValue фиксирует связанные значения в электронной таблице, не обновляется в Office Excel 2007 и 2010. Эта функция будет удалять тег значения, когда встречная ячейка имеет связанное значение. Справка [https://learn.microsoft.com/en-us/archive/msdn-technet-forums/e16bae1f-6a2c-4325-8013-e989a3479066](https://learn.microsoft.com/en-us/archive/msdn-technet-forums/e16bae1f-6a2c-4325-8013-e989a3479066). Обратите внимание: после открытия XLSX-файла Excel будет обновлять связанное значение и генерировать новое значение и вызывать файл сохранения или нет.

Эффект очистки кеша ячейки в рабочей книге появляется как модификация тега `<v>`, например кеш ячейки перед очисткой:

```xml
<row r="19">
    <c r="B19">
        <f>SUM(Sheet2!D2,Sheet2!D11)</f>
        <v>100</v>
     </c>
</row>
```

После очистки кеша ячейки:

```xml
<row r="19">
    <c r="B19">
        <f>SUM(Sheet2!D2,Sheet2!D11)</f>
    </c>
</row>
```

## Разделить имя ячейки {#SplitCellName}

```go
func SplitCellName(cell string) (string, int, error)
```

SplitCellName разделяет имя ячейки на имя столбца и номер строки. Например:

```go
excelize.SplitCellName("AK74") // return "AK", 74, nil
```

## Присоединиться к имени ячейки {#JoinCellName}

```go
func JoinCellName(col string, row int) (string, error)
```

JoinCellName объединяет имя ячейки из имени столбца и номера строки.

## Имя столбца в номер {#ColumnNameToNumber}

```go
func ColumnNameToNumber(name string) (int, error)
```

ColumnNameToNumber предоставляет функцию для преобразования имени столбца листа Excel в `int`. Имя столбца нечувствительно к регистру. Функция возвращает ошибку, если имя столбца неверно. Например:

```go
excelize.ColumnNameToNumber("AK") // returns 37, nil
```

## Номер столбца к имени {#ColumnNumberToName}

```go
func ColumnNumberToName(num int) (string, error)
```

ColumnNumberToName предоставляет функцию для преобразования целого числа в заголовок столбца листа Excel. Например:

```go
excelize.ColumnNumberToName(37) // returns "AK", nil
```

## Имя ячейки для координат {#CellNameToCoordinates}

```go
func CellNameToCoordinates(cell string) (int, int, error)
```

CellNameToCoordinates преобразует буквенно-цифровое имя ячейки в координаты `[X, Y]` или возвращает ошибку. Например:

```go
excelize.CellNameToCoordinates("A1") // returns 1, 1, nil
excelize.CellNameToCoordinates("Z3") // returns 26, 3, nil
```

## Координаты на имя ячейки {#CoordinatesToCellName}

```go
func CoordinatesToCellName(col, row int, abs ...bool) (string, error)
```

CoordinatesToCellName преобразует `[X, Y]` координаты в буквенно-цифровое имя ячейки или возвращает ошибку. Например:

```go
excelize.CoordinatesToCellName(1, 1) // returns "A1", nil
excelize.CoordinatesToCellName(1, 1, true) // returns "$A$1", nil
```

## Создать условный стиль {#NewConditionalStyle}

```go
func (f *File) NewConditionalStyle(style *Style) (int, error)
```

NewConditionalStyle предоставляет функцию для создания стиля для условного формата по заданному стилю. Параметры такие же, как и функция [`NewStyle`](style.md#NewStyle). Обратите внимание, что в цветовом поле используется цветовой код RGB и поддерживается только для установки шрифта, заливок, выравнивания и границ в настоящее время.

## Получить условный стиль {#GetConditionalStyle}

```go
func (f *File) GetConditionalStyle(idx int) (*Style, error)
```

GetConditionalStyle возвращает определение стиля условного формата по указанному индексу стиля.

## Установка условного формата {#SetConditionalFormat}

```go
func (f *File) SetConditionalFormat(sheet, rangeRef string, opts []ConditionalFormatOptions) error
```

SetConditionalFormat предоставляет функцию для создания правила условного форматирования для значения ячейки. Условное форматирование - это функция Office Excel, которая позволяет применять формат к ячейке или диапазону ячеек на основе определенных критериев.

Опция `Type` является обязательным параметром и не имеет значения по умолчанию. Допустимые значения типов и связанные с ними параметры:

<table>
    <thead>
        <tr>
            <th>Тип</th>
            <th>параметры</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=4>cell</td>
            <td>Criteria</td>
        </tr>
        <tr>
            <td>Value</td>
        </tr>
        <tr>
            <td>MinValue</td>
        </tr>
        <tr>
            <td>MaxValue</td>
        </tr>
        <tr>
            <td>time_period</td>
            <td>Criteria</td>
        </tr>
        <tr>
            <td rowspan=2>text</td>
            <td>Criteria</td>
        </tr>
        <tr>
            <td>Value</td>
        </tr>
        <tr>
            <td>average</td>
            <td>Criteria</td>
        </tr>
        <tr>
            <td>duplicate</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td>unique</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td rowspan=2>top</td>
            <td>Criteria</td>
        </tr>
        <tr>
            <td>Value</td>
        </tr>
        <tr>
            <td rowspan=2>bottom</td>
            <td>Criteria</td>
        </tr>
        <tr>
            <td>Value</td>
        </tr>
        <tr>
            <td>blanks</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td>no_blanks</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td>errors</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td>no_errors</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td rowspan=6>2_color_scale</td>
            <td>MinType</td>
        </tr>
        <tr>
            <td>MaxType</td>
        </tr>
        <tr>
            <td>MinValue</td>
        </tr>
        <tr>
            <td>MaxValue</td>
        </tr>
        <tr>
            <td>MinColor</td>
        </tr>
        <tr>
            <td>MaxColor</td>
        </tr>
        <tr>
            <td rowspan=9>3_color_scale</td>
            <td>MinType</td>
        </tr>
        <tr>
            <td>MidType</td>
        </tr>
        <tr>
            <td>MaxType</td>
        </tr>
        <tr>
            <td>MinValue</td>
        </tr>
        <tr>
            <td>MidValue</td>
        </tr>
        <tr>
            <td>MaxValue</td>
        </tr>
        <tr>
            <td>MinColor</td>
        </tr>
        <tr>
            <td>MidColor</td>
        </tr>
        <tr>
            <td>MaxColor</td>
        </tr>
        <tr>
            <td rowspan=9>data_bar</td>
            <td>MinType</td>
        </tr>
        <tr>
            <td>MaxType</td>
        </tr>
        <tr>
            <td>MinValue</td>
        </tr>
        <tr>
            <td>MaxValue</td>
        </tr>
        <tr>
            <td>BarBorderColor</td>
        </tr>
        <tr>
            <td>BarColor</td>
        </tr>
        <tr>
            <td>BarDirection</td>
        </tr>
        <tr>
            <td>BarOnly</td>
        </tr>
        <tr>
            <td>BarSolid</td>
        </tr>
        <tr>
            <td rowspan=3>iconSet</td>
            <td>IconStyle</td>
        </tr>
        <tr>
            <td>ReverseIcons</td>
        </tr>
        <tr>
            <td>IconsOnly</td>
        </tr>
        <tr>
            <td>formula</td>
            <td>Criteria</td>
        </tr>
    </tbody>
</table>

Параметр `Criteria` используется для установки критериев, по которым будут оцениваться данные ячейки. Он не имеет значения по умолчанию. Наиболее распространенные критерии применительно к `excelize.ConditionalFormatOptions{Type: "cell"}`:

Символ описания текста|Символическое представление
---|---
between|
not between|
equal to|==
not equal to|!=
greater than|>
less than|<
greater than or equal to|>=
less than or equal to|<=

Вы можете использовать строки текстового описания Excel в первом столбце выше или более распространенные символические альтернативы.

Дополнительные критерии, которые относятся к другим типам условного формата, приведены в соответствующих разделах ниже.

`Value`: значение обычно используется вместе с параметром `Criteria` для установки правила, по которому будут оцениваться данные ячейки:

```go
err := f.SetConditionalFormat("Sheet1", "D1:D10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "cell",
            Criteria: ">",
            Format:   &format,
            Value:    "6",
        },
    },
)
```

Свойство `Value` также может быть ссылкой на ячейку:

```go
err := f.SetConditionalFormat("Sheet1", "D1:D10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "cell",
            Criteria: ">",
            Format:   &format,
            Value:    "$C$1",
        },
    },
)
```

Тип: `Format` - The `Format` параметр используется для указания формата, который будет применен к клетке, когда условное форматирование критерия. Формат создается с помощью метода [`NewConditionalStyle()`](utils.md#NewConditionalStyle) таким же образом, как и форматы ячеек:

```go
format, err := f.NewConditionalStyle(
    &excelize.Style{
        Font: &excelize.Font{Color: "9A0511"},
        Fill: excelize.Fill{
            Type: "pattern", Color: []string{"FEC7CE"}, Pattern: 1,
        },
    },
)
if err != nil {
    fmt.Println(err)
}
err = f.SetConditionalFormat("Sheet1", "D1:D10",
    []excelize.ConditionalFormatOptions{
        {Type: "cell", Criteria: ">", Format: &format, Value: "6"},
    },
)
```

Примечание. В Excel условный формат накладывается поверх существующего формата ячейки, и не все свойства формата ячейки могут быть изменены. Свойства, которые не могут быть изменены в условном формате имя шрифта, размер шрифта, верхние и нижние индексы, диагональные границы, все свойства выравнивания и все защитные свойства.

Excel указывает некоторые стандартные форматы, которые будут использоваться с условным форматированием. Они могут быть реплицированы с использованием следующих форматов excelize:

```go
// Розовый формат для плохих условных.
format1, err := f.NewConditionalStyle(
    &excelize.Style{
        Font: &excelize.Font{Color: "9A0511"},
        Fill: excelize.Fill{
            Type: "pattern", Color: []string{"FEC7CE"}, Pattern: 1,
        },
    },
)

// Светло-желтый формат для нейтральных условных.
format2, err := f.NewConditionalStyle(
    &excelize.Style{
        Font: &excelize.Font{Color: "9B5713"},
        Fill: excelize.Fill{
            Type: "pattern", Color: []string{"FEEAA0"}, Pattern: 1,
        },
    },
)

// Светло-зеленый формат для хорошего условного.
format3, err := f.NewConditionalStyle(
    &excelize.Style{
        Font: &excelize.Font{Color: "09600B"},
        Fill: excelize.Fill{
            Type: "pattern", Color: []string{"C7EECF"}, Pattern: 1,
        },
    },
)
```

Тип: `MinValue` - Минимальный параметр используется для установки нижнего предельного значения, когда `Criteria` либо `between`или `not between`.

```go
// Выделяйте правила ячеек: между...
err := f.SetConditionalFormat("Sheet1", "A1:A10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "cell",
            Criteria: "between",
            Format:   &format,
            MinValue: "6",
            MaxValue: "8",
        },
    },
)
```

Тип: `MaxValue` - `MaxValue` параметр используется для задания верхнего предельного значения, когда критерии являются либо `between` или `not between`. См. Предыдущий пример.

Тип: `average` - `average` типа используются для указания «Average» стиль условного формата Office Excel в:

```go
// Правила сверху / снизу: выше среднего...
err := f.SetConditionalFormat("Sheet1", "A1:A10",
    []excelize.ConditionalFormatOptions{
        {
            Type:         "average",
            Criteria:     "=",
            Format:       &format1,
            AboveAverage: true,
        },
    },
)

// Правила сверху / снизу: ниже среднего...
err := f.SetConditionalFormat("Sheet1", "B1:B10",
    []excelize.ConditionalFormatOptions{
        {
            Type:         "average",
            Criteria:     "=",
            Format:       &format2,
            AboveAverage: false,
        },
    },
)
```

Тип: `duplicate` - Тип `duplicate` используется для выделения повторяющихся ячеек в диапазоне:

```go
// Выделять правила ячеек: повторяющиеся значения...
err := f.SetConditionalFormat("Sheet1", "A1:A10",
    []excelize.ConditionalFormatOptions{
        {Type: "duplicate", Criteria: "=", Format: &format},
    },
)
```

Тип: `unique` - Уникальный тип используется для выделения уникальных ячеек в диапазоне:

```go
// Выделить правила ячеек: не равно...
err := f.SetConditionalFormat("Sheet1", "A1:A10",
    []excelize.ConditionalFormatOptions{
        {Type: "unique", Criteria: "=", Format: &format},
    },
)
```

Тип: `top` - Тип `top` используется для указания верхних n значений по числу или проценту в диапазоне:

```go
// Верх / Низ правила: Топ 10.
err := f.SetConditionalFormat("Sheet1", "H1:H10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "top",
            Criteria: "=",
            Format:   &format,
            Value:    "6",
        },
    },
)
```

Критерии могут использоваться, чтобы указать, что требуется процентное условие:

```go
err := f.SetConditionalFormat("Sheet1", "A1:A10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "top",
            Criteria: "=",
            Format:   &format,
            Value:    "6",
            Percent:  true,
        },
    },
)
```

Тип: `2_color_scale` - Тип `2_color_scale` используется для указания условного формата стиля Excel «2 Цветные весы»:

```go
// Цветные весы: 2 цвета.
err := f.SetConditionalFormat("Sheet1", "A1:A10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "2_color_scale",
            Criteria: "=",
            MinType:  "min",
            MaxType:  "max",
            MinColor: "#F8696B",
            MaxColor: "#63BE7B",
        },
    },
)
```

Этот условный тип может быть изменен с помощью `MinType`, `MaxType`, `MinValue`, `MaxValue`, `MinColor` и `MaxColor`, Смотри ниже.

Тип: `3_color_scale` - Тип `3_color_scale` используется для указания условного формата стиля Excel «3 Цветные весы»:

```go
// Цветные весы: 3 цвета.
err := f.SetConditionalFormat("Sheet1", "A1:A10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "3_color_scale",
            Criteria: "=",
            MinType:  "min",
            MidType:  "percentile",
            MaxType:  "max",
            MinColor: "#F8696B",
            MidColor: "#FFEB84",
            MaxColor: "#63BE7B",
        },
    },
)
```

Этот условный тип может быть изменен с помощью `MinType`, `MidType`, `MaxType`, `MinValue`, `MidValue`, `MaxValue`, `MinColor`, `MidColor` и `MaxColor`, Смотри ниже.

Тип: `data_bar` - Тип `data_bar` используется для указания условного формата стиля Excel «Панель данных».

`MinType` - Тип `MinType` и `MaxType` свойства доступны, когда тип условного форматирования `2_color_scale`, `3_color_scale` или `data_bar`. Тип `MidType` доступен для `3_color_scale`. Свойства используются следующим образом:

```go
// Панель данных: Градиентная заливка.
err := f.SetConditionalFormat("Sheet1", "K1:K10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "data_bar",
            Criteria: "=",
            MinType:  "min",
            MaxType:  "max",
            BarColor: "#638EC6",
        },
    },
)
```

Доступные типы `min/mid/max`:

Параметр|Объяснение
---|---
min|Минимальное значение (только для `MinType`)
num|числовой
percent|процент
percentile|процентиль
formula|формула
max|Максимум (только для `MaxType`)

`MidType` - Используется для `3_color_scale`. То же, что и `MinType`, см. Выше.

`MaxType` - То же, что и `MinType`, см. Выше.

`MinValue` - В `MinValue` и `MaxValue` свойства доступны при условный тип форматирования `2_color_scale`, `3_color_scale` или `data_bar`. `MidValue` доступен для `3_color_scale`.

`MidValue` - Используется для `3_color_scale`. То же, что и `MinValue`, см. Выше.

`MaxValue` - То же, что и `MinValue`, см. Выше.

`MinColor` - The `MinColor` and `MaxColor` properties are available when the conditional formatting type is `2_color_scale`, `3_color_scale` or `data_bar`. The `MidColor` is available for `3_color_scale`. The properties are used as follows:

```go
// Цветные весы: 3 цвета.
err := f.SetConditionalFormat("Sheet1", "B1:B10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "3_color_scale",
            Criteria: "=",
            MinType:  "min",
            MidType:  "percentile",
            MaxType:  "max",
            MinColor: "#F8696B",
            MidColor: "#FFEB84",
            MaxColor: "#63BE7B",
        },
    },
)
```

`MidColor` - Используется для `3_color_scale`. То же, что и `MinColor`, см. Выше.

`MaxColor` - То же, что и `MinColor`, см. Выше.

`BarColor` - Используется для `data_bar`. То же, что и `MinColor`, см. Выше.

`BarBorderColor` - Используется для установки цвета линии границы гистограммы, это видно только в Excel 2010 и более поздних версиях.

`BarDirection` - Используется для установки направления гистограмм. Доступные варианты:

Значение|Пояснение
---|---
context     | Направление панели данных задается приложением для работы с электронными таблицами в зависимости от контекста отображаемых данных.
leftToRight | Направление строки данных справа налево.
rightToLeft | Направление панели данных слева направо.

`BarOnly` - Используется для set отображает данные столбца, но не данные в ячейках.

`BarSolid` - Используется для включения сплошной (неградиентной) заливки гистограмм. Это видно только в Excel 2010 и более поздних версиях.

`IconStyle` - Доступные варианты:

|Значение|
|---|
|3Arrows        |
|3ArrowsGray    |
|3Flags         |
|3Signs         |
|3Symbols       |
|3Symbols2      |
|3TrafficLights1|
|3TrafficLights2|
|4Arrows        |
|4ArrowsGray    |
|4Rating        |
|4RedToBlack    |
|4TrafficLights |
|5Arrows        |
|5ArrowsGray    |
|5Quarters      |
|5Rating        |

`ReverseIcons` - Используется для набора перевернутых наборов значков.

`IconsOnly` - Используется для множества, отображаемого без значения ячейки.

`StopIfTrue` - Используется для установки функции «остановить, если истинно» правила условного форматирования, когда к ячейке или диапазону ячеек применяется более одного правила. Когда этот параметр установлен, последующие правила не оцениваются, если текущее правило истинно.

Например, выделите наибольшее и наименьшее значения в диапазоне ячеек `A1:D4`, установив условное форматирование для `Sheet1`:

<p align="center"><img width="1044" src="./images/condition_format_01.png" alt="Установить условное форматирование в диапазоне ячеек"></p>

```go
func main() {
    f := excelize.NewFile()
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    for r := 1; r <= 4; r++ {
        row := []int{
            rand.Intn(100), rand.Intn(100), rand.Intn(100), rand.Intn(100),
        }
        if err := f.SetSheetRow("Sheet1", fmt.Sprintf("A%d", r), &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    red, err := f.NewConditionalStyle(
        &excelize.Style{
            Font: &excelize.Font{
                Color: "9A0511",
            },
            Fill: excelize.Fill{
                Type:    "pattern",
                Color:   []string{"FEC7CE"},
                Pattern: 1,
            },
        },
    )
    if err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SetConditionalFormat("Sheet1", "A1:D4",
        []excelize.ConditionalFormatOptions{
            {
                Type:     "bottom",
                Criteria: "=",
                Value:    "1",
                Format:   &red,
            },
        },
    ); err != nil {
        fmt.Println(err)
        return
    }
    green, err := f.NewConditionalStyle(
        &excelize.Style{
            Font: &excelize.Font{
                Color: "09600B",
            },
            Fill: excelize.Fill{
                Type:    "pattern",
                Color:   []string{"C7EECF"},
                Pattern: 1,
            },
        },
    )
    if err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SetConditionalFormat("Sheet1", "A1:D4",
        []excelize.ConditionalFormatOptions{
            {
                Type:     "top",
                Criteria: "=",
                Value:    "1",
                Format:   &green,
            },
        },
    ); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
        return
    }
}
```

## Получить условный формат {#GetConditionalFormats}

```go
func (f *File) GetConditionalFormats(sheet string) (map[string][]ConditionalFormatOptions, error)
```

Метод GetConditionalFormats возвращает параметры условного формата по заданному имени листа.

## Удалить условный формат {#UnsetConditionalFormat}

```go
func (f *File) UnsetConditionalFormat(sheet, rangeRef string) error
```

UnsetConditionalFormat предоставляет функцию для сброса условного формата по заданному имени и диапазону листа.

## Настройка панелей {#SetPanes}

```go
func (f *File) SetPanes(sheet string, panes *Panes) error
```

SetPanes предоставляет функцию для создания и удаления стоп-кадр и разделения панелей с помощью заданного имени листа и формата панелей.

`ActivePane` определяет активную панель. Возможные значения для этого атрибута определены в следующей таблице:

Значение перечисления|Описание
---|---
bottomLeft (Bottom Left Pane) |Нижняя левая панель, когда применяются как вертикальные, так и горизонтальные расщепления.<br><br>Это значение также используется, когда применяется только горизонтальный раскол, разделяя панель на верхнюю и нижнюю области. В этом случае это значение указывает нижнюю панель.
bottomRight (Bottom Right Pane) |Нижняя правая панель, когда применяются как вертикальные, так и горизонтальные расщепления.
topLeft (Top Left Pane)|Верхняя левая панель, когда применяются как вертикальные, так и горизонтальные расщепления.<br><br>Это значение также используется, когда применяется только горизонтальное разделение, разделяя панель на верхнюю и нижнюю области. В этом случае это значение указывает верхнюю панель.<br><br>Это значение также используется, когда применяется только вертикальный раскол, разделяющий панель на правую и левую области. В этом случае это значение указывает левую панель.
topRight (Top Right Pane)|Верхняя правая панель, когда применяются как вертикальные, так и горизонтальные расщепления.<br><br>Это значение также используется, когда применяется только вертикальное разделение, разделяя панель на правую и левую области. В этом случае это значение указывает правильную панель.

Тип состояния панели ограничен значениями, которые в настоящее время перечислены в следующей таблице:

Значение перечисления|Описание
---|---
frozen (Frozen)|Панели замораживаются, но не разрываются. В этом состоянии, когда панели снова разморожены, появляется одно окно без разделения.<br><br>В этом состоянии разделительные панели не регулируются.
split (Split)|Панели разделены, но не заморожены. В этом состоянии разделительные полосы настраиваются пользователем.

`XSplit` - Горизонтальное положение раскола в 1/20 точки; 0 (ноль), если нет. Если панель заморожена, это значение указывает количество столбцов, отображаемых в верхней панели.

`YSplit` - Вертикальное положение раскола в 1/20 точки; 0 (ноль), если нет. Если панель заморожена, это значение указывает количество строк, видимых на левой панели. Возможные значения для этого атрибута определяются двойным типом данных W3C XML Schema.

`TopLeftCell` - Расположение верхней левой части видимой ячейки в нижней правой панели (когда в режиме «Влево-Вправо»).

`SQRef` - Диапазон выбора. Может быть несмежным набором диапазонов.

Пример 1: зафиксировать столбец `A` в `Sheet1` и установить активную ячейку на `Sheet1!K16`:

<p align="center"><img width="770" src="./images/setpans_01.png" alt="Замороженная колонна"></p>

```go
err := f.SetPanes("Sheet1", &excelize.Panes{
    Freeze:      true,
    XSplit:      1,
    TopLeftCell: "B1",
    ActivePane:  "topRight",
    Selection: []excelize.Selection{
        {SQRef: "K16", ActiveCell: "K16", Pane: "topRight"},
    },
})
```

Пример 2: заморозить строки с 1 по 9 в Листе 1 и установить диапазоны активных ячеек на `Sheet1!A11:XFD11`:

<p align="center"><img width="770" src="./images/setpans_02.png" alt="Зафиксировать столбцы и установить диапазоны активных ячеек"></p>

```go
err := f.SetPanes("Sheet1", &excelize.Panes{
    Freeze:      true,
    YSplit:      9,
    TopLeftCell: "A34",
    ActivePane:  "bottomLeft",
    Selection: []excelize.Selection{
        {SQRef: "A11:XFD11", ActiveCell: "A11", Pane: "bottomLeft"},
    },
})
```

Пример 3: создать разделенные панели в `Sheet1` и установить активную ячейку на `Sheet1!J60`:

<p align="center"><img width="780" src="./images/setpans_03.png" alt="Создание разделенных стекол"></p>

```go
err := f.SetPanes("Sheet1", &excelize.Panes{
    Split:       true,
    XSplit:      3270,
    YSplit:      1800,
    TopLeftCell: "N57",
    ActivePane:  "bottomLeft",
    Selection: []excelize.Selection{
        {SQRef: "I36", ActiveCell: "I36"},
        {SQRef: "G33", ActiveCell: "G33", Pane: "topRight"},
        {SQRef: "J60", ActiveCell: "J60", Pane: "bottomLeft"},
        {SQRef: "O60", ActiveCell: "O60", Pane: "bottomRight"},
    },
})
```

Пример 4, разморозить и удалить все панели на `Sheet1`:

```go
err := f.SetPanes("Sheet1", &excelize.Panes{Freeze: false, Split: false})
```

## Получение панелей {#GetPanes}

```go
func (f *File) GetPanes(sheet string) (Panes, error)
```

GetPanes предоставляет функцию для получения закрепления областей, разделенных областей и представлений рабочего листа по заданному имени рабочего листа.

## Цвет {#ThemeColor}

```go
func (f *File) GetBaseColor(hexColor string, indexedColor int, themeColor *int) string
```

GetBaseColor возвращает предпочтительный шестнадцатеричный код цвета, предоставляя шестнадцатеричный код цвета, индексированный цвет и цвет темы.

```go
func ThemeColor(baseColor string, tint float64) string
```

ThemeColor применил цвет со значением оттенка.

Для текста в электронной таблице существует три типа цветов: шестнадцатеричный цвет, индексированный цвет и цвет темы. Приоритет этих цветов заключается в том, что шестнадцатеричный цвет имеет приоритет над цветом темы, а цвет темы имеет приоритет над индексированным цветом. Кроме того, цвет также поддерживает применение значения оттенка на основе шестнадцатеричного цвета, поэтому нам нужно использовать функцию ThemeColor, чтобы применить оттенок для базового цвета и получить рассчитанное шестнадцатеричное значение цвета. Например:

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
    runs, err := f.GetCellRichText("Sheet1", "A1")
    if err != nil {
        fmt.Println(err)
        return
    }
    for _, run := range runs {
        var hexColor string
        if run.Font != nil {
            baseColor := f.GetBaseColor(run.Font.Color, run.Font.ColorIndexed, run.Font.ColorTheme)
            hexColor = strings.TrimPrefix(excelize.ThemeColor(baseColor, run.Font.ColorTint), "FF")
        }
        fmt.Printf("text: %s, color: %s\r\n", run.Text, hexColor)
    }
}
```

## Преобразование RGB в HSL {#RGBToHSL}

```go
func RGBToHSL(r, g, b uint8) (h, s, l float64)
```

RGBToHSL преобразует тройку RGB в тройку HSL.

## Конвертировать HSL в RGB {#HSLToRGB}

```go
func HSLToRGB(h, s, l float64) (r, g, b uint8)
```

HSLToRGB преобразует тройку HSL в тройку RGB.

## Файловый писатель {#FileWriter}

### Write {#Write}

```go
func (f *File) Write(w io.Writer, opts ...Options) error
```

Write предоставляет функцию для записи в `io.Writer`.

### WriteTo {#WriteTo}

```go
func (f *File) WriteTo(w io.Writer, opts ...Options) (int64, error)
```

WriteTo реализует `io.WriterTo` для записи файла.

### WriteToBuffer {#WriteToBuffer}

```go
func (f *File) WriteToBuffer() (*bytes.Buffer, error)
```

WriteToBuffer предоставляет функцию для получения `*bytes.Buffer` из сохраненного файла.

## Добавить проект VBA {#AddVBAProject}

```go
func (f *File) AddVBAProject(file []byte) error
```

AddVBAProject предоставляет метод добавления файла `vbaProject.bin`, который содержит функции и/или макросы. Расширение файла должно быть `.xlsm` или `.xltm`. Например:

```go
codeName := "Sheet1"
if err := f.SetSheetProps("Sheet1", &excelize.SheetPropsOptions{
    CodeName: &codeName,
}); err != nil {
    fmt.Println(err)
    return
}
file, err := os.ReadFile("vbaProject.bin")
if err != nil {
    fmt.Println(err)
    return
}
if err := f.AddVBAProject(file); err != nil {
    fmt.Println(err)
    return
}
if err := f.SaveAs("macros.xlsm"); err != nil {
    fmt.Println(err)
    return
}
```

## Преобразование даты Excel в то время {#ExcelDateToTime}

```go
func ExcelDateToTime(excelDate float64, use1904Format bool) (time.Time, error)
```

ExcelDateToTime конвертирует представление даты в формате `float` в значение `time.Time`.

## Транскодер персонажа {#CharsetTranscoder}

```go
func (f *File) CharsetTranscoder(fn func(charset string, input io.Reader) (rdr io.Reader, err error)) *File
```

CharsetTranscoder Устанавливает пользовательскую функцию транскодера кодовой страницы для открытого XLSX из кодировки не UTF-8.

## Установить ZIP-архиватор {#SetZipWriter}

```go
func (f *File) SetZipWriter(fn func(io.Writer) ZipWriter) *File
```

SetZipWriter устанавливает определяемую пользователем функцию записи ZIP-архива для сохранения рабочей книги.
