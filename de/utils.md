# Dienstprogramme

## Tabelle {#AddTable}

```go
func (f *File) AddTable(sheet, hCell, vCell, opts string) error
```

AddTable bietet die Methode zum Hinzufügen einer Tabelle zu einem Arbeitsblatt anhand des angegebenen Arbeitsblattnamens, des Koordinatenbereichs und des Formatsatzes.

- Beispiel 1: Erstellen Sie eine Tabelle mit `A1:D5` auf `Sheet1`:

<p align="center"><img width="612" src="./images/addtable_01.png" alt="Tabelle hinzufügen"></p>

```go
err := f.AddTable("Sheet1", "A1", "D5", ``)
```

- Beispiel 2: Erstellen Sie eine Tabelle mit `F2:H6` auf `Sheet2` mit dem folgenden Format:

<p align="center"><img width="612" src="./images/addtable_02.png" alt="Tabelle mit festgelegtem Format hinzufügen"></p>

```go
err := f.AddTable("Sheet2", "F2", "H6", `{
    "table_name": "table",
    "table_style": "TableStyleMedium2",
    "show_first_column": true,
    "show_last_column": true,
    "show_row_stripes": false,
    "show_column_stripes": true
}`)
```

Beachten Sie, dass die Tabelle mindestens zwei Zeilen einschließlich der Kopfzeile enthalten muss. Die Header-Zellen müssen Zeichenfolgen enthalten und eindeutig sein und die Header-Zeilendaten der Tabelle festlegen, bevor die AddTable-Funktion aufgerufen wird. Mehrere Tabellen koordinieren Bereiche, die keinen Schnittpunkt haben können.

`table_name`: Der Name der Tabelle im selben Arbeitsblattnamen der Tabelle sollte eindeutig sein.

`table_style`: Die Namen der integrierten Tabellenstile:

```text
TableStyleLight1 - TableStyleLight21
TableStyleMedium1 - TableStyleMedium28
TableStyleDark1 - TableStyleDark11
```

Index|Stil|Index|Stil|Index|Stil
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

## Automatischer Filter {#AutoFilter}

```go
unc (f *File) AutoFilter(sheet, hCell, vCell, opts string) error
```

AutoFilter bietet die Methode zum Hinzufügen eines automatischen Filters in einem Arbeitsblatt anhand des angegebenen Arbeitsblattnamens, des Koordinatenbereichs und der Einstellungen. Ein automatischer Filter in Excel ist eine Möglichkeit, einen 2D-Datenbereich anhand einiger einfacher Kriterien zu filtern.

Beispiel 1: Anwenden eines automatischen Filters auf einen Zellbereich `A1:D4` in `Sheet1`:

<p align="center"><img width="612" src="./images/autofilter_01.png" alt="Automatischen Filter hinzufügen"></p>

```go
err := f.AutoFilter("Sheet1", "A1", "D4", "")
```

Beispiel 2: Filtern von Daten in einem automatischen Filter:

```go
err := f.AutoFilter("Sheet1", "A1", "D4", `{"column":"B","expression":"x != blanks"}`)
```

`column` definiert die Filterspalten in einem automatischen Filterbereich anhand einfacher Kriterien.

Es reicht nicht aus, nur die Filterbedingung anzugeben. Sie müssen auch alle Zeilen ausblenden, die nicht der Filterbedingung entsprechen. Zeilen werden mit der Methode [`SetRowVisible()`](sheet.md#SetRowVisible) ausgeblendet. Excelize kann Zeilen nicht automatisch filtern, da dies nicht Teil des Dateiformats ist.

Festlegen von Filterkriterien für eine Spalte:

`expression` definiert die Bedingungen, die folgenden Operatoren stehen zum Festlegen der Filterkriterien zur Verfügung:

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

Ein Ausdruck kann eine einzelne Anweisung oder zwei Anweisungen umfassen, die durch die Operatoren `and` und `or` getrennt sind. Zum Beispiel:

```text
x <  2000
x >  2000
x == 2000
x >  2000 and x <  5000
x == 2000 or  x == 5000
```

Das Filtern von leeren oder nicht leeren Daten kann erreicht werden, indem ein Wert von Leer oder Nicht leer im Ausdruck verwendet wird:

```text
x == Blanks
x == NonBlanks
```

Office Excel ermöglicht auch einige einfache Zeichenfolgenabgleichsvorgänge:

```text
x == b*      // beginnt mit b
x != b*      // beginnt nicht mit b
x == *b      // endet mit b
x != *b      // endet nicht mit b
x == *b*     // enthält b
x != *b*     // enthält nicht b
```

Sie können auch `*` verwenden, um mit einem beliebigen Zeichen oder einer beliebigen Zahl übereinzustimmen, und `?`, Um mit einem einzelnen Zeichen oder einer einzelnen Zahl übereinzustimmen. Kein anderer Quantifizierer für reguläre Ausdrücke wird von den Excel-Filtern unterstützt. Die regulären Ausdruckszeichen von Excel können mit `~` maskiert werden.

Die Platzhaltervariable `x` in den obigen Beispielen kann durch eine einfache Zeichenfolge ersetzt werden. Der tatsächliche Platzhaltername wird intern ignoriert, sodass alle folgenden Elemente gleichwertig sind:

```text
x     < 2000
col   < 2000
Price < 2000
```

## Verknüpften Wert aktualisieren {#UpdateLinkedValue}

```go
func (f *File) UpdateLinkedValue() error
```

UpdateLinkedValue fix verknüpfte Werte in einer Tabelle werden in Office Excel 2007 und 2010 nicht aktualisiert. Diese Funktion entfernt das Wertetag, wenn eine Zelle einen verknüpften Wert hat. Referenz [https://social.technet.microsoft.com/Forums/office/en-US/e16bae1f-6a2c-4325-8013-e989a3479066/excel-2010-linked-cells-not-updating](https://social.technet.microsoft.com/Forums/office/en-US/e16bae1f-6a2c-4325-8013-e989a3479066/excel-2010-linked-cells-not-updating) Hinweis: Nach dem Öffnen der Tabellenkalkulationsdatei aktualisiert Excel den verknüpften Wert, generiert einen neuen Wert und fordert zum Speichern der Datei auf oder nicht.

Der Effekt des Löschens des Zellencaches in der Arbeitsmappe wird als Änderung des Tags `<v>` angezeigt, z. B. des Zellencaches vor dem Löschen:

```xml
<row r="19" spans="2:2">
    <c r="B19">
        <f>SUM(Sheet2!D2,Sheet2!D11)</f>
        <v>100</v>
     </c>
</row>
```

Nach dem Löschen des Zellencaches:

```xml
<row r="19" spans="2:2">
    <c r="B19">
        <f>SUM(Sheet2!D2,Sheet2!D11)</f>
    </c>
</row>
```

## Geteilter Zellname {#SplitCellName}

```go
func SplitCellName(cell string) (string, int, error)
```

SplitCellName teilt den Zellennamen in den Spaltennamen und die Zeilennummer auf. Zum Beispiel:

```go
excelize.SplitCellName("AK74") // rückkehr "AK", 74, nil
```

## Join-Zellenname {#JoinCellName}

```go
func JoinCellName(col string, row int) (string, error)
```

JoinCellName verbindet den Zellennamen aus dem Spaltennamen und der Zeilennummer.

## Spaltenname zu Nummer {#ColumnNameToNumber}

```go
func ColumnNameToNumber(name string) (int, error)
```

ColumnNameToNumber bietet eine Funktion zum Konvertieren des Spaltennamens einer Excel-Tabelle in `int`. Spaltenname ohne Berücksichtigung der Groß- und Kleinschreibung. Die Funktion gibt einen Fehler zurück, wenn der Spaltenname falsch ist. Zum Beispiel:

```go
excelize.ColumnNameToNumber("AK") // rückkehr 37, nil
```

## Die zu benennende Spaltennummer {#ColumnNumberToName}

```go
func ColumnNumberToName(num int) (string, error)
```

ColumnNumberToName bietet eine Funktion zum Konvertieren der Ganzzahl in den Spaltentitel des Excel-Arbeitsblatts. Zum Beispiel:

```go
excelize.ColumnNumberToName(37) // rückkehr "AK", nil
```

## Zellenname zu Koordinaten {#CellNameToCoordinates}

```go
func CellNameToCoordinates(cell string) (int, int, error)
```

CellNameToCoordinates konvertiert den alphanumerischen Zellennamen in `[X, Y]` Koordinaten oder gibt einen Fehler zurück. Zum Beispiel:

```go
excelize.CellNameToCoordinates("A1") // rückkehr 1, 1, nil
excelize.CellNameToCoordinates("Z3") // rückkehr 26, 3, nil
```

## Koordinaten zum Zellnamen {#CoordinatesToCellName}

```go
func CoordinatesToCellName(col, row int, abs ...bool) (string, error)
```

CoordinatesToCellName konvertiert `[X, Y]` Koordinaten in alphanumerische Zellennamen oder gibt einen Fehler zurück. Zum Beispiel:

```go
excelize.CoordinatesToCellName(1, 1) // rückkehr "A1", nil
excelize.CoordinatesToCellName(1, 1, true) // rückkehr "$A$1", nil
```

## Bedingter Stil {#NewConditionalStyle}

```go
func (f *File) NewConditionalStyle(style string) (int, error)
```

NewConditionalStyle bietet eine Funktion zum Erstellen eines Stils für das bedingte Format anhand des angegebenen Stilformats. Die Parameter sind die gleichen wie bei der Funktion [`NewStyle`](style.md#NewStyle). Beachten Sie, dass das Farbfeld RGB-Farbcode verwendet und nur das Festlegen von Schriftart, Füllungen, Ausrichtung und Rahmen unterstützt.

## Bedingtes Format festlegen {#SetConditionalFormat}

```go
func (f *File) SetConditionalFormat(sheet, reference, opts string) error
```

SetConditionalFormat bietet eine Funktion zum Erstellen einer bedingten Formatierungsregel für den Zellenwert. Die bedingte Formatierung ist eine Funktion von Office Excel, mit der Sie ein Format auf eine Zelle oder einen Zellbereich basierend auf bestimmten Kriterien anwenden können.

Die Option `type` ist ein erforderlicher Parameter und hat keinen Standardwert. Zulässige Typwerte und die zugehörigen Parameter sind:

<table>
    <thead>
        <tr>
            <th>Typ</th>
            <th>Parameters</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=4>cell</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>value</td>
        </tr>
        <tr>
            <td>minimum</td>
        </tr>
        <tr>
            <td>maximum</td>
        </tr>
        <tr>
            <td rowspan=4>date</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>value</td>
        </tr>
        <tr>
            <td>minimum</td>
        </tr>
        <tr>
            <td>maximum</td>
        </tr>
        <tr>
            <td>time_period</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td rowspan=2>text</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>value</td>
        </tr>
        <tr>
            <td>average</td>
            <td>criteria</td>
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
            <td>criteria</td>
        </tr>
        <tr>
            <td>value</td>
        </tr>
        <tr>
            <td rowspan=2>bottom</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>value</td>
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
            <td>min_type</td>
        </tr>
        <tr>
            <td>max_type</td>
        </tr>
        <tr>
            <td>min_value</td>
        </tr>
        <tr>
            <td>max_value</td>
        </tr>
        <tr>
            <td>min_color</td>
        </tr>
        <tr>
            <td>max_color</td>
        </tr>
        <tr>
            <td rowspan=9>3_color_scale</td>
            <td>min_type</td>
        </tr>
        <tr>
            <td>mid_type</td>
        </tr>
        <tr>
            <td>max_type</td>
        </tr>
        <tr>
            <td>min_value</td>
        </tr>
        <tr>
            <td>mid_value</td>
        </tr>
        <tr>
            <td>max_value</td>
        </tr>
        <tr>
            <td>min_color</td>
        </tr>
        <tr>
            <td>mid_color</td>
        </tr>
        <tr>
            <td>max_color</td>
        </tr>
        <tr>
            <td rowspan=5>data_bar</td>
            <td>min_type</td>
        </tr>
        <tr>
            <td>max_type</td>
        </tr>
        <tr>
            <td>min_value</td>
        </tr>
        <tr>
            <td>max_value</td>
        </tr>
        <tr>
            <td>bar_color</td>
        </tr>
        <tr>
            <td>formula</td>
            <td>criteria</td>
        </tr>
    </tbody>
</table>

Der Parameter `criteria` wird verwendet, um die Kriterien festzulegen, nach denen die Zellendaten ausgewertet werden. Es hat keinen Standardwert. Die häufigsten Kriterien für `{"type"："cell"}` sind:

Textbeschreibung Charakter|Symbolische Darstellung
---|---
between|
not between|
equal to|==
not equal to|!=
greater than|>
less than|<
greater than or equal to|>=
less than or equal to|<=

Sie können entweder die Textbeschreibungszeichenfolgen von Excel in der ersten Spalte oben oder die gängigsten symbolischen Alternativen verwenden.

Zusätzliche Kriterien, die für andere bedingte Formattypen spezifisch sind, werden in den entsprechenden Abschnitten unten gezeigt.

`value`: Der Wert wird im Allgemeinen zusammen mit dem Parameter `criteria` verwendet, um die Regel festzulegen, nach der die Zellendaten ausgewertet werden:

```go
f.SetConditionalFormat("Sheet1", "D1:D10", fmt.Sprintf(`[
{
    "type": "cell",
    "criteria": ">",
    "format": %d,
    "value": "6"
}]`, format))
```

Die Eigenschaft `value` kann auch eine Zellreferenz sein:

```go
f.SetConditionalFormat("Sheet1", "D1:D10", fmt.Sprintf(`[
{
    "type": "cell",
    "criteria": ">",
    "format": %d,
    "value": "$C$1"
}]`, format))
```

type: `format` - Der Parameter `format` wird verwendet, um das Format anzugeben, das auf die Zelle angewendet wird, wenn das Kriterium der bedingten Formatierung erfüllt ist. Das Format wird mit der Methode [`NewConditionalStyle()`](utils.md#NewConditionalStyle) auf dieselbe Weise wie die Zellenformate erstellt:

```go
format, err = f.NewConditionalStyle(`{
    "font":
    {
        "color": "#9A0511"
    },
    "fill":
    {
        "type": "pattern",
        "color": ["#FEC7CE"],
        "pattern": 1
    }
}`)
if err != nil {
    fmt.Println(err)
}
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "cell",
    "criteria": ">",
    "format": %d,
    "value": "6"
}]`, format))
```

Hinweis: In Excel wird ein bedingtes Format über das vorhandene Zellenformat gelegt, und nicht alle Eigenschaften des Zellenformats können geändert werden. Eigenschaften, die in einem bedingten Format nicht geändert werden können, sind Schriftname, Schriftgröße, hochgestellt und tiefgestellt, diagonale Ränder, alle Ausrichtungseigenschaften und alle Schutzeigenschaften.

Excel gibt einige Standardformate an, die bei der bedingten Formatierung verwendet werden sollen. Diese können mit den folgenden Excel-Formaten repliziert werden:

```go
// Rosenformat für schlechte Bedingungen.
format1, err = f.NewConditionalStyle(`{
    "font":
    {
        "color": "#9A0511"
    },
    "fill":
    {
        "type": "pattern",
        "color": ["#FEC7CE"],
        "pattern": 1
    }
}`)

// Hellgelbes Format für neutrale Bedingungen.
format2, err = f.NewConditionalStyle(`{
    "font":
    {
        "color": "#9B5713"
    },
    "fill":
    {
        "type": "pattern",
        "color": ["#FEEAA0"],
        "pattern": 1
    }
}`)

// Hellgrünes Format für gute Bedingungen.
format3, err = f.NewConditionalStyle(`{
    "font":
    {
        "color": "#09600B"
    },
    "fill":
    {
        "type": "pattern",
        "color": ["#C7EECF"],
        "pattern": 1
    }
}`)
```

type: `minimum` - Der Parameter `minimum` wird verwendet, um den unteren Grenzwert festzulegen, wenn das `criteria` entweder `between` oder `not between` liegt.

```go
// Markieren Sie die Regel für Zellen: zwischen ...
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "cell",
    "criteria": "between",
    "format": %d,
    "minimum": "6",
    "maximum": "8"
}]`, format))
```

type: `maximum` - Der Parameter `maximum` wird verwendet, um den oberen Grenzwert festzulegen, wenn die Kriterien entweder `between` oder `not between` liegen. Siehe das vorherige Beispiel.

type: `average` - Der Typ `average` wird verwendet, um das bedingte Format im "Durchschnitt" -Stil von Office Excel anzugeben:

```go
// Top/Bottom-Regeln: Überdurchschnittlich...
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "average",
    "criteria": "=",
    "format": %d,
    "above_average": true
}]`, format1))

// Top/Bottom-Regeln: Unterdurchschnittlich...
f.SetConditionalFormat("Sheet1", "B1:B10", fmt.Sprintf(`[
{
    "type": "average",
    "criteria": "=",
    "format": %d,
    "above_average": false
}]`, format2))
```

type: `duplicate` - Der Typ `duplicate` wird verwendet, um doppelte Zellen in einem Bereich hervorzuheben:

```go
// Markieren Sie die Zellenregeln: Werte duplizieren...
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "duplicate",
    "criteria": "=",
    "format": %d
}]`, format))
```

type: `unique` - Der Typ `unique` wird verwendet, um eindeutige Zellen in einem Bereich hervorzuheben:

```go
// Markieren Sie die Zellenregeln: Nicht gleich...
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "unique",
    "criteria": "=",
    "format": %d
}]`, format))
```

type: `top` - Der Typ `top` wird verwendet, um die oberen n-Werte nach Anzahl oder Prozentsatz in einem Bereich anzugeben:

```go
// Top/Bottom-Regeln: Top 10.
f.SetConditionalFormat("Sheet1", "H1:H10", fmt.Sprintf(`[
{
    "type": "top",
    "criteria": "=",
    "format": %d,
    "value": "6"
}]`, format))
```

Die Kriterien können verwendet werden, um anzuzeigen, dass eine prozentuale Bedingung erforderlich ist:

```go
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "top",
    "criteria": "=",
    "format": %d,
    "value": "6",
    "percent": true
}]`, format))
```

type: `2_color_scale` - Der Typ `2_color_scale` wird verwendet, um das bedingte Format im Excel-Stil "2 Farbskala" anzugeben:

```go
// Farbskalen: 2 Farben.
f.SetConditionalFormat("Sheet1", "A1:A10", `[
{
    "type": "2_color_scale",
    "criteria": "=",
    "min_type": "min",
    "max_type": "max",
    "min_color": "#F8696B",
    "max_color": "#63BE7B"
}]`)
```

Dieser bedingte Typ kann mit `min_type`, `max_type`, `min_value`, `max_value`, `min_color` und `max_color` geändert werden (siehe unten).

type: `3_color_scale` - Der Typ `3_color_scale` wird verwendet, um das bedingte Format des Excel-Stils "3 Color Scale" anzugeben:

```go
// Farbskalen: 3 Farben.
f.SetConditionalFormat("Sheet1", "A1:A10", `[
{
    "type": "3_color_scale",
    "criteria": "=",
    "min_type": "min",
    "mid_type": "percentile",
    "max_type": "max",
    "min_color": "#F8696B",
    "mid_color": "#FFEB84",
    "max_color": "#63BE7B"
}]`)
```

Dieser bedingte Typ kann mit `min_type`, `mid_type`, `max_type`, `min_value`, `mid_value`, `max_value`, `min_color`, `mid_color` und `max_color` geändert werden (siehe unten).

type: `data_bar` - Der Typ `data_bar` wird verwendet, um das bedingte Format im Excel-Stil "Data Bar" anzugeben.

`min_type` - Die Eigenschaften `min_type` und `max_type` sind verfügbar, wenn der bedingte Formatierungstyp `2_color_scale`, `3_color_scale` oder `data_bar` ist. Der `mid_type` ist für `3_color_scale` verfügbar. Die Eigenschaften werden wie folgt verwendet:

```go
// Datenbalken: Verlaufsfüllung.
f.SetConditionalFormat("Sheet1", "K1:K10", `[
{
    "type": "data_bar",
    "criteria": "=",
    "min_type": "min",
    "max_type": "max",
    "bar_color": "#638EC6"
}]`)
```

Die verfügbaren `min/mid/max` -Typen sind:

Parameter|Erläuterung
---|---
min|Minimalwert (nur für `min_type`)
num|Numerisch
percent|Prozentsatz
percentile|Perzentil
formula|Formel
max|Maximum (nur für `max_type`)

`mid_type` - Wird für `3_color_scale` verwendet. Gleich wie `min_type`, siehe oben.

`max_type` - Gleich wie `min_type`, siehe oben.

`min_value` - Die Eigenschaften `min_value` und `max_value` sind verfügbar, wenn der bedingte Formatierungstyp `2_color_scale`, `3_color_scale` oder `data_bar` ist. Der `mid_value` ist für `3_color_scale` verfügbar.

`mid_value` - Wird für `3_color_scale` verwendet. Gleich wie `min_value`, siehe oben.

`max_value` - Gleich wie `min_value`, siehe oben.

`min_color` - Die Eigenschaften `min_color` und `max_color` sind verfügbar, wenn der bedingte Formatierungstyp `2_color_scale`, `3_color_scale` oder `data_bar` ist. Die `mid_color` ist für `3_color_scale` verfügbar. Die Eigenschaften werden wie folgt verwendet:

```go
// Farbskalen: 3 Farben.
f.SetConditionalFormat("Sheet1", "B1:B10", `[
{
    "type": "3_color_scale",
    "criteria": "=",
    "min_type": "min",
    "mid_type": "percentile",
    "max_type": "max",
    "min_color": "#F8696B",
    "mid_color": "#FFEB84",
    "max_color": "#63BE7B"
}]`)
```

`mid_color` - Wird für `3_color_scale` verwendet. Gleich wie `min_color`, siehe oben.

`max_color` - Gleich wie `min_color`, siehe oben.

`bar_color` - Wird für `data_bar` verwendet. Gleich wie `min_color`, siehe oben.

Heben Sie beispielsweise die höchsten und niedrigsten Werte in einem Zellbereich `A1:D4` hervor, indem Sie die bedingte Formatierung auf `Sheet1` festlegen:

<p align="center"><img width="1044" src="./images/condition_format_01.png" alt="Bedingte Formatierung in einem Zellbereich festlegen"></p>

```go
package main

import (
    "fmt"
    "math/rand"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    for r := 1; r <= 4; r++ {
        row := []int{rand.Intn(100), rand.Intn(100), rand.Intn(100), rand.Intn(100)}
        if err := f.SetSheetRow("Sheet1", fmt.Sprintf("A%d", r), &row); err != nil {
            fmt.Println(err)
        }
    }
    red, err := f.NewConditionalStyle(`{
        "font":
        {
            "color": "#9A0511"
        },
        "fill":
        {
            "type": "pattern",
            "color": ["#FEC7CE"],
            "pattern": 1
        }
    }`)
    if err != nil {
        fmt.Println(err)
    }
    if err := f.SetConditionalFormat("Sheet1", "A1:D4", fmt.Sprintf(`[
        {
            "type": "bottom",
            "criteria": "=",
            "value": "1",
            "format": %d
        }]`, red)); err != nil {
        fmt.Println(err)
    }
    green, err := f.NewConditionalStyle(`{
        "font":
        {
            "color": "#09600B"
        },
        "fill":
        {
            "type": "pattern",
            "color": ["#C7EECF"],
            "pattern": 1
        }
    }`)
    if err != nil {
        fmt.Println(err)
    }
    if err := f.SetConditionalFormat("Sheet1", "A1:D4", fmt.Sprintf(`[
        {
            "type": "top",
            "criteria":"=",
            "value":"1",
            "format": %d
        }]`, green)); err != nil {
        fmt.Println(err)
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Bedingtes Format erhalten {#GetConditionalFormats}

```go
func (f *File) GetConditionalFormats(sheet string) (map[string]string, error)
```

GetConditionalFormats gibt bedingte Formateinstellungen nach dem angegebenen Arbeitsblattnamen zurück.

## Entfernen des bedingten Formats {#UnsetConditionalFormat}

```go
func (f *File) UnsetConditionalFormat(sheet, reference string) error
```

UnsetConditionalFormat bietet eine Funktion zum Aufheben des bedingten Formats anhand des angegebenen Arbeitsblattnamens und -bereichs.

## Bereiche {#SetPanes}

```go
func (f *File) SetPanes(sheet, panes string)
```

SetPanes bietet eine Funktion zum Erstellen und Entfernen von Freeze-Fenstern und zum Teilen von Fenstern anhand des angegebenen Arbeitsblattnamens und des festgelegten Fensterformats.

`activePane` definiert das aktive Fenster. Die möglichen Werte für dieses Attribut sind in der folgenden Tabelle definiert:

Aufzählungswert|Beschreibung
---|---
bottomLeft (Unten links) |Unten links, wenn sowohl vertikale als auch horizontale Teilungen angewendet werden.<br><br>Dieser Wert wird auch verwendet, wenn nur eine horizontale Aufteilung angewendet wurde, die den Bereich in obere und untere Bereiche unterteilt. In diesem Fall gibt dieser Wert den unteren Bereich an.
bottomRight (Unten rechts) | Unten rechts, wenn sowohl vertikale als auch horizontale Teilungen angewendet werden.
topLeft (Oben links)|Oben links, wenn sowohl vertikale als auch horizontale Teilungen angewendet werden.<br><br>Dieser Wert wird auch verwendet, wenn nur eine horizontale Aufteilung angewendet wurde, die den Bereich in obere und untere Bereiche unterteilt. In diesem Fall gibt dieser Wert den oberen Bereich an.<br><br>Dieser Wert wird auch verwendet, wenn nur eine vertikale Teilung angewendet wurde, die den Bereich in rechte und linke Bereiche unterteilt. In diesem Fall gibt dieser Wert den linken Bereich an.
topRight (Top Right Pane)|Oben rechts, wenn sowohl vertikale als auch horizontale Teilungen angewendet werden.<br><br> Dieser Wert wird auch verwendet, wenn nur eine vertikale Teilung angewendet wurde, die den Bereich in rechte und linke Bereiche unterteilt. In diesem Fall gibt dieser Wert den rechten Bereich an.

Der Statusstatus des Bereichs ist auf die unterstützten Werte beschränkt, die derzeit in der folgenden Tabelle aufgeführt sind:

Aufzählungswert|Beschreibung
---|---
frozen (Gefroren)|Die Scheiben sind eingefroren, wurden aber beim Teilen nicht gespalten. In diesem Zustand wird beim erneuten Auffrieren der Fenster ein einzelnes Fenster ohne Teilung erstellt.<br><br>In diesem Zustand sind die geteilten Balken nicht einstellbar.
split (Teilt)|Die Scheiben sind geteilt, aber nicht gefroren. In diesem Zustand sind die geteilten Balken vom Benutzer einstellbar.

`x_split` - Horizontale Position der Teilung in 1/20 eines Punktes; 0 (Null) wenn keine. Wenn der Bereich eingefroren ist, gibt dieser Wert die Anzahl der im oberen Bereich sichtbaren Spalten an.

`y_split` - Vertikale Position der Teilung in 1/20 eines Punktes; 0 (Null) wenn keine. Wenn der Bereich eingefroren ist, gibt dieser Wert die Anzahl der im linken Bereich sichtbaren Zeilen an. Die möglichen Werte für dieses Attribut werden durch den doppelten Datentyp W3C XML Schema definiert.

`top_left_cell` - Position der sichtbaren Zelle oben links im unteren rechten Bereich (im Modus von links nach rechts).

`sqref` - Bereich der Auswahl. Kann ein nicht zusammenhängender Satz von Bereichen sein.

Beispiel 1: Spalte `A` in `Sheet1` einfrieren und die aktive Zelle auf `Sheet1!K16` setzen:

<p align="center"><img width="770" src="./images/setpans_01.png" alt="Gefrorene Säule"></p>

```go
f.SetPanes("Sheet1", `{
    "freeze": true,
    "split": false,
    "x_split": 1,
    "y_split": 0,
    "top_left_cell": "B1",
    "active_pane": "topRight",
    "panes": [
    {
        "sqref": "K16",
        "active_cell": "K16",
        "pane": "topRight"
    }]
}`)
```

Beispiel 2: Frieren Sie die Zeilen 1 bis 9 in `Sheet1` ein und setzen Sie die aktiven Zellbereiche auf AA `Sheet1!A11:XFD11`:

<p align="center"><img width="770" src="./images/setpans_02.png" alt="Spalten einfrieren und aktive Zellbereiche festlegen"></p>

```go
f.SetPanes("Sheet1", `{
    "freeze": true,
    "split": false,
    "x_split": 0,
    "y_split": 9,
    "top_left_cell": "A34",
    "active_pane": "bottomLeft",
    "panes": [
    {
        "sqref": "A11:XFD11",
        "active_cell": "A11",
        "pane": "bottomLeft"
    }]
}`)
```

Beispiel 3: Erstellen Sie geteilte Fenster in `Sheet1` und setzen Sie die aktive Zelle auf `Sheet1!J60`:

<p align="center"><img width="755" src="./images/setpans_03.png" alt="Erstellen Sie geteilte Fenster"></p>

```go
f.SetPanes("Sheet1", `{
    "freeze": false,
    "split": true,
    "x_split": 3270,
    "y_split": 1800,
    "top_left_cell": "N57",
    "active_pane": "bottomLeft",
    "panes": [
    {
        "sqref": "I36",
        "active_cell": "I36"
    },
    {
        "sqref": "G33",
        "active_cell": "G33",
        "pane": "topRight"
    },
    {
        "sqref": "J60",
        "active_cell": "J60",
        "pane": "bottomLeft"
    },
    {
        "sqref": "O60",
        "active_cell": "O60",
        "pane": "bottomRight"
    }]
}`)
```

Beispiel 4: Entfrieren und entfernen Sie alle Fenster auf `Sheet1`:

```go
f.SetPanes("Sheet1", `{"freeze":false,"split":false}`)
```

## Farbe {#ThemeColor}

```go
func ThemeColor(baseColor string, tint float64) string
```

ThemeColor hat die Farbe mit dem Farbtonwert angewendet:

```go
package main

import (
    "fmt"
    "strings"

    "github.com/xuri/excelize/v2"
)

func main() {
    f, err := excelize.OpenFile("Book1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(getCellBgColor(f, "Sheet1", "A1"))
    if err = f.Close(); err != nil {
        fmt.Println(err)
    }
}

func getCellBgColor(f *excelize.File, sheet, cell string) string {
    styleID, err := f.GetCellStyle(sheet, cell)
    if err != nil {
        return err.Error()
    }
    fillID := *f.Styles.CellXfs.Xf[styleID].FillID
    fgColor := f.Styles.Fills.Fill[fillID].PatternFill.FgColor
    if fgColor != nil && f.Theme != nil {
        if clrScheme := f.Theme.ThemeElements.ClrScheme; fgColor.Theme != nil {
            if val, ok := map[int]*string{
                0: &clrScheme.Lt1.SysClr.LastClr,
                1: &clrScheme.Dk1.SysClr.LastClr,
                2: clrScheme.Lt2.SrgbClr.Val,
                3: clrScheme.Dk2.SrgbClr.Val,
                4: clrScheme.Accent1.SrgbClr.Val,
                5: clrScheme.Accent2.SrgbClr.Val,
                6: clrScheme.Accent3.SrgbClr.Val,
                7: clrScheme.Accent4.SrgbClr.Val,
                8: clrScheme.Accent5.SrgbClr.Val,
                9: clrScheme.Accent6.SrgbClr.Val,
            }[*fgColor.Theme]; ok && val != nil {
                return strings.TrimPrefix(excelize.ThemeColor(*val, fgColor.Tint), "FF")
            }
        }
        return strings.TrimPrefix(fgColor.RGB, "FF")
    }
    return "FFFFFF"
}
```

## Konvertieren von RGB in HSL {#RGBToHSL}

```go
func RGBToHSL(r, g, b uint8) (h, s, l float64)
```

RGBToHSL konvertiert ein RGB-Tripel in ein HSL-Tripel.

## Konvertieren von HSL in RGB {#HSLToRGB}

```go
func HSLToRGB(h, s, l float64) (r, g, b uint8)
```

HSLToRGB konvertiert ein HSL-Tripel in ein RGB-Tripel.

## Datei-Brenner {#FileWriter}

### Write {#Write}

```go
func (f *File) Write(w io.Writer, opts ...Options) error
```

Write bietet eine Funktion zum Schreiben in einen `io.Writer`.

### WriteTo {#WriteTo}

```go
func (f *File) WriteTo(w io.Writer, opts ...Options) (int64, error)
```

WriteTo implementiert `io.WriterTo`, um die Datei zu schreiben.

### WriteToBuffer {#WriteToBuffer}

```go
func (f *File) WriteToBuffer() (*bytes.Buffer, error)
```

WriteToBuffer bietet eine Funktion zum Abrufen von `*bytes.Buffer` aus der gespeicherten Datei.

## VBA-Projekt hinzufügen {#AddVBAProject}

```go
func (f *File) AddVBAProject(bin string) error
```

AddVBAProject bietet die Methode zum Hinzufügen der Datei `vbaProject.bin`, die Funktionen und/oder Makros enthält. Die Dateierweiterung sollte `.xlsm` sein. Zum Beispiel:

```go
codeName := "Sheet1"
if err := f.SetSheetProps("Sheet1", &excelize.SheetPropsOptions{
    CodeName: &codeName,
}); err != nil {
    fmt.Println(err)
}
if err := f.AddVBAProject("vbaProject.bin"); err != nil {
    fmt.Println(err)
}
if err := f.SaveAs("macros.xlsm"); err != nil {
    fmt.Println(err)
}
```

## Excel-Datum zur Uhrzeit {#ExcelDateToTime}

```go
func ExcelDateToTime(excelDate float64, use1904Format bool) (time.Time, error)
```

ExcelDateToTime konvertiert eine Float-basierte Excel-Datumsdarstellung in eine `time.Time`.

## Zeichentranscoder {#CharsetTranscoder}

```go
func (f *File) CharsetTranscoder(fn charsetTranscoderFn) *File
```

CharsetTranscoder Legt die benutzerdefinierte Codepage-Transcoder-Funktion zum Öffnen der Tabelle mit Nicht-UTF-8-Codierung fest.
