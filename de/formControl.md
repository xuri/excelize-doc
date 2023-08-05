# Formular-Steuerelemente

FormControl ordnet die Formularsteuerinformationen direkt zu.

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

## Hinzufügen von Formularsteuerelementen {#AddFormControl}

```go
func (f *File) AddFormControl(sheet string, opts FormControl) error
```

AddFormControl stellt die Methode zum Hinzufügen einer Formularsteuerschaltfläche in einem Arbeitsblatt bereit, indem der Arbeitsblattname und die Formularsteueroptionen angegeben werden. Unterstützte Formularsteuerelementtypen: Schaltfläche, Kontrollkästchen, Gruppenfeld, Beschriftung, Optionsschaltfläche, Bildlaufleiste und Spinner. Wenn ein Makro für das Formularsteuerelement festgelegt wird, sollte die Arbeitsmappenerweiterung `.xlsm` oder `.xltm` sein. Der Bildlaufwert muss zwischen 0 und 30000 liegen.

Beispiel 1: Fügen Sie eine Schaltflächenformularsteuerung mit Makro, Rich-Text, benutzerdefinierter Schaltflächengröße und Druckeigenschaft auf `Tabelle1!A2` hinzu und lassen Sie die Schaltfläche nicht mit den Zellen verschieben oder ihre Größe ändern:

<p align="center"><img width="180" src="./images/form_ctrl_button.gif" alt="Hinzufügen von Schaltflächenformularsteuerelementen mit Excelize"></p>

```go
err := f.AddFormControl("Tabelle1", excelize.FormControl{
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

Beispiel 2: Optionsfeld-Formularsteuerelemente mit aktiviertem Status und Text auf `Tabelle1!A1` und `Tabelle1!A2` hinzufügen:

<p align="center"><img width="127" src="./images/form_ctrl_option_button.gif" alt="Fügen Sie Optionsfeld-Formularsteuerelemente mit Excelize hinzu"></p>

```go
if err := f.AddFormControl("Tabelle1", excelize.FormControl{
    Cell:    "A1",
    Type:    excelize.FormControlOptionButton,
    Text:    "Option Button 1",
    Checked: true,
}); err != nil {
    fmt.Println(err)
}
if err := f.AddFormControl("Tabelle1", excelize.FormControl{
    Cell:    "A2",
    Type:    excelize.FormControlOptionButton,
    Text:    "Option Button 2",
}); err != nil {
    fmt.Println(err)
}
```

Beispiel 3: Fügen Sie ein Drehschaltflächen-Formularsteuerelement zu `Tabelle1!B1` hinzu, um den Wert von `Tabelle1!A1` zu erhöhen oder zu verringern:

<p align="center"><img width="126" src="./images/form_ctrl_spin_button.gif" alt="Fügen Sie mit Excelize die Formularsteuerung für Drehschaltflächen hinzu"></p>

```go
err := f.AddFormControl("Tabelle1", excelize.FormControl{
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

Beispiel 4: Fügen Sie ein Formularsteuerelement mit horizontaler Bildlaufleiste zu `Tabelle1!A2` hinzu, um den Wert von `Tabelle1!A1` zu ändern, indem Sie auf die Bildlaufpfeile klicken oder das Bildlauffeld ziehen:

<p align="center"><img width="180" src="./images/form_ctrl_scroll_bar.gif" alt="Fügen Sie mit Excelize eine horizontale Bildlaufleisten-Formularsteuerung hinzu"></p>

```go
err := f.AddFormControl("Tabelle1", excelize.FormControl{
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

## Holen Sie sich Formularsteuerelemente {#GetFormControls}

```go
func (f *File) GetFormControls(sheet string) ([]FormControl, error)
```

GetFormControls ruft alle Formularsteuerelemente in einem Arbeitsblatt nach einem bestimmten Arbeitsblattnamen ab. Beachten Sie, dass diese Funktion derzeit nicht das Abrufen der Breite und Höhe der Formularsteuerelemente unterstützt.

## Löschen Sie die Formularsteuerelemente {#DeleteFormControl}

```go
func (f *File) DeleteFormControl(sheet, cell string) error
```

DeleteFormControl bietet die Methode zum Löschen von Formularsteuerelementen in einem Arbeitsblatt anhand des angegebenen Arbeitsblattnamens und der Zellreferenz. Löschen Sie beispielsweise das Formularsteuerelement in `Tabelle1!$A$1`:

```go
err := f.DeleteFormControl("Tabelle1", "A1")
```
