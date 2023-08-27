# Daten

## Hinzufügen von Datenüberprüfungen {#AddDataValidation}

```go
func (f *File) AddDataValidation(sheet string, dv *DataValidation)
```

AddDataValidation bietet eine festgelegte Datenüberprüfung für einen Bereich des Arbeitsblatts anhand des angegebenen Datenüberprüfungsobjekts und des Arbeitsblattnamens. Das Datenüberprüfungsobjekt kann mit der Funktion `NewDataValidation` erstellt werden. Datenvalidierungstyp und Operatoren finden Sie im Abschnitt [Constants](constants.md).

Beispiel 1: Setzen Sie die Datenvalidierung auf `Sheet1!A1:B2` mit den Einstellungen für die Validierungskriterien. Zeigen Sie eine Fehlerwarnung an, nachdem ungültige Daten mit dem Stil "Stop" und dem benutzerdefinierten Titel "Fehlerkörper" eingegeben wurden:

<p align="center"><img width="665" src="./images/data_validation_01.png" alt="Datenvalidierung"></p>

```go
dv := excelize.NewDataValidation(true)
dv.SetSqref("A1:B2")
dv.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorBetween)
dv.SetError(excelize.DataValidationErrorStyleStop, "error title", "Fehlerkörper")
f.AddDataValidation("Sheet1", dv)
```

Beispiel 2: Stellen Sie die Datenvalidierung auf `Sheet1!A3:B4` mit den Einstellungen für die Validierungskriterien ein und zeigen Sie die Eingabemeldung an, wenn die Zelle ausgewählt ist:

<p align="center"><img width="665" src="./images/data_validation_02.png" alt="Datenvalidierung"></p>

```go
dv = excelize.NewDataValidation(true)
dv.SetSqref("A3:B4")
dv.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorGreaterThan)
dv.SetInput("input title", "input body")
f.AddDataValidation("Sheet1", dv)
```

Beispiel 3: Setzen Sie die Datenvalidierung auf `Sheet1!A5:B6` mit den Einstellungen für die Validierungskriterien. Erstellen Sie ein Dropdown-Menü in der Zelle, indem Sie die Listenquelle zulassen:

<p align="center"><img width="665" src="./images/data_validation_03.png" alt="Datenvalidierung"></p>

```go
dv = excelize.NewDataValidation(true)
dv.SetSqref("A5:B6")
dv.SetDropList([]string{"1", "2", "3"})
f.AddDataValidation("Sheet1", dv)
```

Wenn Sie die Elemente in das Datenvalidierungsdialogfeld (eine durch Trennzeichen getrennte Liste) eingeben, beträgt die Grenze 255 Zeichen, einschließlich der Trennzeichen. Wenn die Quellformel Ihrer Datenvalidierungsliste die maximale Längenbeschränkung überschreitet, legen Sie bitte die zulässigen Werte in den Arbeitsblattzellen fest und verwenden Sie die Funktion `SetSqrefDropList`, um die Referenz für ihre Zellen festzulegen.

Beispiel 4: Setzen Sie die Datenvalidierung auf `Sheet1!A7:B8` mit den Einstellungen der Validierungskriterienquelle `Sheet1!E1:E3`. Erstellen Sie ein Dropdown-Menü in der Zelle, indem Sie die Listenquelle zulassen:

<p align="center"><img width="665" src="./images/data_validation_04.png" alt="Datenvalidierung"></p>

```go
dv := excelize.NewDataValidation(true)
dv.SetSqref("A7:B8")
dv.SetSqrefDropList("$E$1:$E$3")
f.AddDataValidation("Sheet1", dv)
```

Die Anzahl der Elemente, die in einer Datenvalidierungs-Dropdown-Liste angezeigt werden, ist begrenzt: Die Liste kann bis zu 32768 Elemente aus einer Liste im Arbeitsblatt anzeigen. Wenn Sie mehr Elemente benötigen, können Sie eine abhängige Dropdown-Liste erstellen, die nach Kategorien aufgeschlüsselt ist.

## Datenvalidierung erhalten {#GetDataValidations}

```go
func (f *File) GetDataValidations(sheet string) ([]*DataValidation, error)
```

GetDataValidations gibt eine Datenvalidierungsliste nach dem angegebenen Arbeitsblattnamen zurück.

## Datenvalidierung löschen {#DeleteDataValidation}

```go
func (f *File) DeleteDataValidation(sheet string, sqref ...string) error
```

DeleteDataValidation Löscht die Datenvalidierung anhand des angegebenen Arbeitsblattnamens und der Referenzsequenz. Alle Datenvalidierungen im Arbeitsblatt werden gelöscht, wenn kein Referenzsequenzparameter angegeben wird.
