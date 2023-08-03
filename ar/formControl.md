# عناصر تحكم النموذج

يقوم FormControl بتعيين معلومات عناصر تحكم النموذج مباشرة.

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

## إضافة عنصر تحكم نموذج {#AddFormControl}

```go
func (f *File) AddFormControl(sheet string, opts FormControl) error
```

يوفر AddFormControl طريقة لإضافة زر عنصر تحكم النموذج في ورقة عمل حسب اسم ورقة العمل المحددة وخيارات التحكم في النموذج. نوع عنصر تحكم النموذج المعتمد: الزر وخانة الاختيار ومربع المجموعة والتسمية وزر الخيار وشريط التمرير ودوار. في حالة تعيين ماكرو لعنصر تحكم النموذج، يجب أن يكون ملحق المصنف `.xlsm` أو `.xltm`. يجب أن تكون قيمة التمرير بين 0 و 30000.

مثال 1 ، أضف عنصر تحكم نموذج الزر باستخدام ماكرو ونص منسق وحجم زر مخصص وخاصية الطباعة على `ورقة1!A2` ، ودع الزر لا يتحرك أو يحجم مع الخلايا:

<p align="center"><img width="180" src="./images/form_ctrl_button.gif" alt="إضافة عنصر تحكم نموذج زر باستخدام Excelize"></p>

```go
err := f.AddFormControl("ورقة1", excelize.FormControl{
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

مثال 2 ، أضف عناصر تحكم نموذج زر الخيار مع تحديد الحالة والنص على `ورقة1!A1` و `ورقة1!A2`:

<p align="center"><img width="127" src="./images/form_ctrl_option_button.gif" alt="إضافة عناصر تحكم نموذج زر الخيار باستخدام Excelize"></p>

```go
if err := f.AddFormControl("ورقة1", excelize.FormControl{
    Cell:    "A1",
    Type:    excelize.FormControlOptionButton,
    Text:    "Option Button 1",
    Checked: true,
}); err != nil {
    fmt.Println(err)
}
if err := f.AddFormControl("ورقة1", excelize.FormControl{
    Cell:    "A2",
    Type:    excelize.FormControlOptionButton,
    Text:    "Option Button 2",
}); err != nil {
    fmt.Println(err)
}
```

مثال 3 ، أضف عنصر تحكم نموذج زر الدوران في `ورقة1!B1` لزيادة أو تقليل قيمة `ورقة1!A1`:

<p align="center"><img width="126" src="./images/form_ctrl_spin_button.gif" alt="إضافة عنصر تحكم نموذج زر الدوران باستخدام Excelize"></p>

```go
err := f.AddFormControl("ورقة1", excelize.FormControl{
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

مثال 4 ، أضف عنصر تحكم نموذج شريط التمرير أفقيا على `ورقة1!A2` لتغيير قيمة `ورقة1!A1` بالنقر فوق أسهم التمرير أو اسحب مربع التمرير:

<p align="center"><img width="180" src="./images/form_ctrl_scroll_bar.gif" alt="إضافة عنصر تحكم نموذج شريط التمرير أفقيا باستخدام Excelize"></p>

```go
err := f.AddFormControl("ورقة1", excelize.FormControl{
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

## احصل على عناصر تحكم النموذج {#GetFormControls}

```go
func (f *File) GetFormControls(sheet string) ([]FormControl, error)
```

يسترد GetFormControls جميع عناصر التحكم في النموذج في ورقة عمل باسم ورقة عمل معينة. لاحظ أن هذه الوظيفة لا تدعم الحصول على عرض وارتفاع عناصر التحكم في النموذج حاليًا.

## حذف عنصر تحكم النموذج {#DeleteFormControl}

```go
func (f *File) DeleteFormControl(sheet, cell string) error
```

يوفر DeleteFormControl طريقة حذف عنصر تحكم النموذج في ورقة عمل حسب اسم ورقة العمل ومرجع الخلية المحددين. على سبيل المثال، احذف عنصر تحكم النموذج في `ورقة1!$A$1`:

```go
err := f.DeleteFormControl("ورقة1", "A1")
```
