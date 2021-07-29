# Kalender

Erstellen Sie einen Kalender mit Excelize in der Sprache Go:

<p align="center"><img width="933" src="../images/example_calendar.png" alt="Erstellen Sie einen Kalender mit Excelize in der Sprache Go"></p>

```go
package main

import (
    "fmt"
    "strconv"

    "github.com/xuri/excelize/v2"
)

func main() {
    // Erstellen Sie eine neue Tabelle
    f := excelize.NewFile()
    var (
        monthStyle, titleStyle, dataStyle, blankStyle,
        grayBlankStyle, grayDataStyle, noteStyle, noteLineStyle int
        err   error
        addr  string
        sheet = "Sheet1"
        // Zellwerte
        data = map[int][]interface{}{
            1: {"Mai 2020"},
            3: {"SONNTAG", "MONTAG", "DIENSTAG", "MITTWOCH",
                "DONNERSTAG", "FREITAG", "SAMSTAG"},
            4:  {26, 27, 28, 29, 30, 1, 2},
            6:  {3, 4, 5, 6, 7, 8, 9},
            8:  {10, 11, 12, 13, 14, 15, 16},
            10: {17, 18, 19, 20, 21, 22, 23},
            12: {24, 25, 26, 27, 28, 29, 30},
            14: {31, 1, 2, 3, 4, 5, 6},
            18: {"Notizen"},
        }
        // benutzerdefinierte Zeilenhöhe
        height = map[int]float64{
            1: 45, 3: 22, 5: 44, 7: 44, 9: 44, 11: 44, 13: 44, 15: 44,
            18: 24, 19: 24, 20: 24, 21: 24, 22: 24, 23: 24, 24: 24,
        }
        top    = excelize.Border{Type: "top", Style: 1, Color: "DADEE0"}
        left   = excelize.Border{Type: "left", Style: 1, Color: "DADEE0"}
        right  = excelize.Border{Type: "right", Style: 1, Color: "DADEE0"}
        bottom = excelize.Border{Type: "bottom", Style: 1, Color: "DADEE0"}
        fill   = excelize.Fill{Type: "pattern", Color: []string{"EFEFEF"}, Pattern: 1}
    )
    // Stellen Sie jeden Zellenwert ein
    for r, row := range data {
        if addr, err = excelize.JoinCellName("B", r); err != nil {
            fmt.Println(err)
            return
        }
        if err = f.SetSheetRow(sheet, addr, &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    // Stellen Sie die benutzerdefinierte Zeilenhöhe ein
    for r, ht := range height {
        if err = f.SetRowHeight(sheet, r, ht); err != nil {
            fmt.Println(err)
            return
        }
    }
    // Legen Sie die benutzerdefinierte Spaltenbreite fest
    if err = f.SetColWidth(sheet, "B", "H", 16.5); err != nil {
        fmt.Println(err)
        return
    }
    // Zelle für den 'MONAT' zusammenführen
    if err = f.MergeCell(sheet, "B1", "D1"); err != nil {
        fmt.Println(err)
        return
    }
    // Definieren Sie den Schriftstil für den 'MONAT'.
    if monthStyle, err = f.NewStyle(&excelize.Style{
        Font: &excelize.Font{Color: "1f7f3b", Bold: true, Size: 22, Family: "Arial"},
    }); err != nil {
        fmt.Println(err)
        return
    }
    // Legen Sie den Schriftstil für den 'MONAT' fest.
    if err = f.SetCellStyle(sheet, "B1", "D1", monthStyle); err != nil {
        fmt.Println(err)
        return
    }
    // Definieren Sie den Stil für 'SONNTAG' bis 'SAMSTAG'.
    if titleStyle, err = f.NewStyle(&excelize.Style{
        Font:      &excelize.Font{Color: "1f7f3b", Bold: true, Family: "Arial"},
        Fill:      excelize.Fill{Type: "pattern", Color: []string{"E6F4EA"}, Pattern: 1},
        Alignment: &excelize.Alignment{Vertical: "center", Horizontal: "center"},
        Border:    []excelize.Border{{Type: "top", Style: 2, Color: "1f7f3b"}},
    }); err != nil {
        fmt.Println(err)
        return
    }
    // Setze den Stil für 'SONNTAG' auf 'SAMSTAG'
    if err = f.SetCellStyle(sheet, "B3", "H3", titleStyle); err != nil {
        fmt.Println(err)
        return
    }
    // Definieren Sie den Zellrand für die Datumszelle im Datumsbereich
    if dataStyle, err = f.NewStyle(&excelize.Style{
        Border: []excelize.Border{top, left, right},
    }); err != nil {
        fmt.Println(err)
        return
    }
    // Legen Sie den Zellenrand für die Datumszelle im Datumsbereich fest
    for _, r := range []int{4, 6, 8, 10, 12, 14} {
        if err = f.SetCellStyle(sheet, "B"+strconv.Itoa(r),
            "H"+strconv.Itoa(r), dataStyle); err != nil {
            fmt.Println(err)
            return
        }
    }
    // Definieren Sie den Zellrand für die leere Zelle im Datumsbereich
    if blankStyle, err = f.NewStyle(&excelize.Style{
        Border: []excelize.Border{left, right, bottom},
    }); err != nil {
        fmt.Println(err)
        return
    }
    // Legen Sie den Zellenrand für die leere Zelle im Datumsbereich fest
    for _, r := range []int{5, 7, 9, 11, 13, 15} {
        if err = f.SetCellStyle(sheet, "B"+strconv.Itoa(r),
            "H"+strconv.Itoa(r), blankStyle); err != nil {
            fmt.Println(err)
            return
        }
    }
    // Definieren Sie den Rahmen und den Füllstil für die leere Zelle im vorherigen und nächsten Monat
    if grayBlankStyle, err = f.NewStyle(&excelize.Style{
        Border: []excelize.Border{left, right, bottom},
        Fill:   fill}); err != nil {
        fmt.Println(err)
        return
    }
    // Legen Sie den Rahmen und den Füllstil für die leere Zelle im vorherigen und nächsten Monat fest
    if err = f.SetCellStyle(sheet, "B5", "F5", grayBlankStyle); err != nil {
        fmt.Println(err)
        return
    }
    if err = f.SetCellStyle(sheet, "C15", "H15", grayBlankStyle); err != nil {
        fmt.Println(err)
        return
    }
    // Definieren Sie den Rahmen und den Füllstil für die Datumszelle im vorherigen und nächsten Monat
    if grayDataStyle, err = f.NewStyle(&excelize.Style{
        Border: []excelize.Border{left, right, top},
        Font:   &excelize.Font{Color: "777777"}, Fill: fill}); err != nil {
        fmt.Println(err)
        return
    }
    // Legen Sie den Rahmen und den Füllstil für die Datumszelle im vorherigen und nächsten Monat fest
    if err = f.SetCellStyle(sheet, "B4", "F4", grayDataStyle); err != nil {
        fmt.Println(err)
        return
    }
    if err = f.SetCellStyle(sheet, "C14", "H14", grayDataStyle); err != nil {
        fmt.Println(err)
        return
    }
    // Definieren Sie den Schriftstil für die 'Notizen'.
    if noteStyle, err = f.NewStyle(&excelize.Style{
        Font: &excelize.Font{Color: "1f7f3b", Bold: true, Size: 14, Family: "Arial"},
    }); err != nil {
        fmt.Println(err)
        return
    }
    // Legen Sie den Schriftstil für die 'Notizen' fest.
    if err = f.SetCellStyle(sheet, "B18", "B18", noteStyle); err != nil {
        fmt.Println(err)
        return
    }
    // Definieren Sie Zellstile für den Notenbereich
    if noteLineStyle, err = f.NewStyle(&excelize.Style{
        Border: []excelize.Border{{Type: "bottom", Style: 4, Color: "DDDDDD"}},
    }); err != nil {
        fmt.Println(err)
        return
    }
    // Legen Sie die Zellstile für den Notenbereich fest
    for r := 19; r < 25; r++ {
        if err = f.SetCellStyle(sheet, "B"+strconv.Itoa(r),
            "H"+strconv.Itoa(r), noteLineStyle); err != nil {
            fmt.Println(err)
            return
        }
    }
    // Gitterlinien für das Arbeitsblatt ausblenden
    if err = f.SetSheetViewOptions(sheet, 0,
        excelize.ShowGridLines(false)); err != nil {
        fmt.Println(err)
        return
    }
    // Arbeitsblatt umbenennen
    f.SetSheetName(sheet, "Mai 20")
    // Tabellenkalkulationsdatei speichern
    if err = f.SaveAs("Kalender.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```
