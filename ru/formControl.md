# Элементы управления формы

FormControl напрямую отображает информацию об элементах управления формы.

```go
type FormControl struct {
    Cell         string
    Macro        string
    Width        uint
    Height       uint
    Checked      bool
    CurrentVal   uint
    MinVal       uint
    MaxVal       uint
    IncChange    uint
    PageChange   uint
    Horizontally bool
    CellLink     string
    Text         string
    Paragraph    []RichTextRun
    Type         FormControlType
    Format       GraphicOptions
}
```

## Добавить элемент управления формой {#AddFormControl}

```go
func (f *File) AddFormControl(sheet string, opts FormControl) error
```

AddFormControl предоставляет метод для добавления кнопки управления формой на рабочий лист с заданным именем рабочего листа и параметрами управления формой. Поддерживаемый тип управления формой: кнопка, флажок, групповое поле, метка, кнопка выбора, полоса прокрутки и счетчик. Если задан макрос для элемента управления формы, расширение рабочей книги должно быть `.xlsm` или `.xltm`. Значение прокрутки должно быть между 0 и 30000.

Пример 1, добавьте элемент управления формы кнопки с макросом, форматированным текстом, настраиваемым размером кнопки, свойством печати на `Лист1!A2` и разрешите кнопке не перемещаться и не изменять размер с ячейками:

<p align="center"><img width="180" src="./images/form_ctrl_button.gif" alt="добавить управление формой кнопки с помощью Excelize"></p>

```go
err := f.AddFormControl("Лист1", excelize.FormControl{
    Cell:   "A2",
    Type:   excelize.FormControlButton,
    Macro:  "Button1_Click",
    Width:  140,
    Height: 60,
    Text:   "Button 1\r\n",
    Paragraph: []excelize.RichTextRun{
        {
            Font: &excelize.Font{
                Bold:      true,
                Italic:    true,
                Underline: "single",
                Family:    "Times New Roman",
                Size:      14,
                Color:     "777777",
            },
            Text: "C1=A1+B1",
        },
    },
    Format: excelize.GraphicOptions{
        PrintObject: &enable,
        Positioning: "absolute",
    },
})
```

Пример 2, добавьте элементы управления формы опциональной кнопки с проверенным статусом и текстом на `Лист1!A1` и `Лист1!A2`:

<p align="center"><img width="127" src="./images/form_ctrl_option_button.gif" alt="добавить элементы управления формой опциональной кнопки с помощью Excelize"></p>

```go
if err := f.AddFormControl("Лист1", excelize.FormControl{
    Cell:    "A1",
    Type:    excelize.FormControlOptionButton,
    Text:    "Option Button 1",
    Checked: true,
}); err != nil {
    fmt.Println(err)
}
if err := f.AddFormControl("Лист1", excelize.FormControl{
    Cell:    "A2",
    Type:    excelize.FormControlOptionButton,
    Text:    "Option Button 2",
}); err != nil {
    fmt.Println(err)
}
```

Пример 3: добавьте элемент управления формой кнопки прокрутки на `Лист1!B1`, чтобы увеличить или уменьшить значение `Лист1!A1`:

<p align="center"><img width="126" src="./images/form_ctrl_spin_button.gif" alt="добавить элемент управления формой кнопки вращения с помощью Excelize"></p>

```go
err := f.AddFormControl("Лист1", excelize.FormControl{
    Cell:       "B1",
    Type:       excelize.FormControlSpinButton,
    Width:      15,
    Height:     40,
    CurrentVal: 7,
    MinVal:     5,
    MaxVal:     10,
    IncChange:  1,
    CellLink:   "A1",
})
```

Пример 4: добавьте горизонтальную полосу прокрутки на лист `Лист1!A2`, чтобы изменить значение `Лист1!A1`, щелкнув стрелки прокрутки или перетащив ползунок:

<p align="center"><img width="180" src="./images/form_ctrl_scroll_bar.gif" alt="добавить элемент управления формой горизонтальной полосы прокрутки с помощью Excelize"></p>

```go
err := f.AddFormControl("Лист1", excelize.FormControl{
    Cell:         "A2",
    Type:         excelize.FormControlScrollBar,
    Width:        140,
    Height:       20,
    CurrentVal:   50,
    MinVal:       10,
    MaxVal:       100,
    IncChange:    1,
    PageChange:   1,
    CellLink:     "A1",
    Horizontally: true,
})
```

## Получить элементы управления формой {#GetFormControls}

```go
func (f *File) GetFormControls(sheet string) ([]FormControl, error)
```

GetFormControls извлекает все элементы управления формы на листе по заданному имени листа. Обратите внимание, что в настоящее время эта функция не поддерживает получение ширины и высоты элементов управления формы.

## Удалить элемент управления формой {#DeleteFormControl}

```go
func (f *File) DeleteFormControl(sheet, cell string) error
```

DeleteFormControl предоставляет метод для удаления элемента управления формой на листе по заданному имени листа и ссылке на ячейку. Например, удалите элемент управления формы в `Лист1!$A$1`:

```go
err := f.DeleteFormControl("Лист1", "A1")
```
