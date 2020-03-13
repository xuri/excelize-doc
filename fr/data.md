# Données

## Ajouter la validation des données {#AddDataValidation}

```go
func (f *File) AddDataValidation(sheet string, dv *DataValidation)
```

AddDataValidation fournit la validation des données définies sur une plage de la feuille de calcul par objet de validation de données et nom de feuille de calcul donnés. L'objet de validation de données peut être créé par la fonction `NewDataValidation`. Le type de validation des données et les opérateurs peuvent être trouvés dans la section [Constants](constants.md).

Exemple 1, validation de données situé sur `Sheet1!A1:B2` avec les paramètres de critères de validation, d'alerte d'erreur de série après des données non valides sont entrées avec "Stop" style et titre personnalisé "error body":

!["La validation des données"](./images/data_validation_01.png "La validation des données")

```go
dvRange := excelize.NewDataValidation(true)
dvRange.Sqref = "A1:B2"
dvRange.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorBetween)
dvRange.SetError(excelize.DataValidationErrorStyleStop, "error title", "error body")
f.AddDataValidation("Sheet1", dvRange)
```

Exemple 2, définissez la validation des données sur `Sheet1!A3:B4` avec les paramètres de validation et affichez le message lorsque la cellule est sélectionnée:

!["La validation des données"](./images/data_validation_02.png "La validation des données")

```go
dvRange = excelize.NewDataValidation(true)
dvRange.Sqref = "A3:B4"
dvRange.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorGreaterThan)
dvRange.SetInput("input title", "input body")
f.AddDataValidation("Sheet1", dvRange)
```

Exemple 3, définissez la validation des données sur `Sheet1!A5:B6` avec les paramètres de validation, créez un menu déroulant dans la cellule en autorisant la source de liste:

!["La validation des données"](./images/data_validation_03.png "La validation des données")

```go
dvRange = excelize.NewDataValidation(true)
dvRange.Sqref = "A5:B6"
dvRange.SetDropList([]string{"1", "2", "3"})
f.AddDataValidation("Sheet1", dvRange)
```

Example 4，définir la validation des données sur `Sheet1!A7:B8` avec la source des critères de validation `Sheet1!E1:E3`, créer un menu déroulant dans la cellule en autorisant la source de liste:

!["Data validation"](./images/data_validation_04.png "Data validation")

```go
dvRange := excelize.NewDataValidation(true)
dvRange.Sqref = "A7:B8"
dvRange.SetSqrefDropList("$E$1:$E$3", true)
f.AddDataValidation("Sheet1", dvRange)
```

## Supprimer la validation des données {#DeleteDataValidation}

```go
func (f *File) DeleteDataValidation(sheet, sqref string) error
```

DeleteDataValidation supprime la validation des données par le nom de feuille de calcul donné et la séquence de référence.
