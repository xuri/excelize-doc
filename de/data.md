# Daten

## Hinzufügen von Datenüberprüfungen {#AddDataValidation}

```go
func (f *File) AddDataValidation(sheet string, dv *DataValidation)
```

AddDataValidation bietet eine festgelegte Datenüberprüfung für einen Bereich des Arbeitsblatts anhand des angegebenen Datenüberprüfungsobjekts und des Arbeitsblattnamens. Das Datenüberprüfungsobjekt kann mit der Funktion `NewDataValidation` erstellt werden. Datenvalidierungstyp und Operatoren finden Sie im Abschnitt [Constants](constants.md).

Beispiel 1: Setzen Sie die Datenvalidierung auf `Sheet1!A1:B2` mit den Einstellungen für die Validierungskriterien. Zeigen Sie eine Fehlerwarnung an, nachdem ungültige Daten mit dem Stil "Stop" und dem benutzerdefinierten Titel "Fehlerkörper" eingegeben wurden:

<p align="center"><img width="665" src="./images/data_validation_01.png" alt="Datenvalidierung"></p>

```go
dvRange := excelize.NewDataValidation(true)
dvRange.Sqref = "A1:B2"
dvRange.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorBetween)
dvRange.SetError(excelize.DataValidationErrorStyleStop, "error title", "Fehlerkörper")
f.AddDataValidation("Sheet1", dvRange)
```

Beispiel 2: Stellen Sie die Datenvalidierung auf `Sheet1!A3:B4` mit den Einstellungen für die Validierungskriterien ein und zeigen Sie die Eingabemeldung an, wenn die Zelle ausgewählt ist:

<p align="center"><img width="665" src="./images/data_validation_02.png" alt="Datenvalidierung"></p>

```go
dvRange = excelize.NewDataValidation(true)
dvRange.Sqref = "A3:B4"
dvRange.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorGreaterThan)
dvRange.SetInput("input title", "input body")
f.AddDataValidation("Sheet1", dvRange)
```

Beispiel 3: Setzen Sie die Datenvalidierung auf `Sheet1!A5:B6` mit den Einstellungen für die Validierungskriterien. Erstellen Sie ein Dropdown-Menü in der Zelle, indem Sie die Listenquelle zulassen:

<p align="center"><img width="665" src="./images/data_validation_03.png" alt="Datenvalidierung"></p>

```go
dvRange = excelize.NewDataValidation(true)
dvRange.Sqref = "A5:B6"
dvRange.SetDropList([]string{"1", "2", "3"})
f.AddDataValidation("Sheet1", dvRange)
```

Beispiel 4: Setzen Sie die Datenvalidierung auf `Sheet1!A7:B8` mit den Einstellungen der Validierungskriterienquelle `Sheet1!E1:E3`. Erstellen Sie ein Dropdown-Menü in der Zelle, indem Sie die Listenquelle zulassen:

<p align="center"><img width="665" src="./images/data_validation_04.png" alt="Datenvalidierung"></p>

```go
dvRange := excelize.NewDataValidation(true)
dvRange.Sqref = "A7:B8"
dvRange.SetSqrefDropList("$E$1:$E$3")
f.AddDataValidation("Sheet1", dvRange)
```

## Datenvalidierung löschen {#DeleteDataValidation}

```go
func (f *File) DeleteDataValidation(sheet, sqref string) error
```

DeleteDataValidation löscht die Datenüberprüfung anhand des angegebenen Arbeitsblattnamens und der Referenzsequenz.
