# Données

## Ajouter la validation des données {#AddDataValidation}

```go
func (f *File) AddDataValidation(sheet string, dv *DataValidation)
```

AddDataValidation fournit la validation des données définies sur une plage de la feuille de calcul par objet de validation de données et nom de feuille de calcul donnés. L'objet de validation de données peut être créé par la fonction `NewDataValidation`. Le type de validation des données et les opérateurs peuvent être trouvés dans la section [Constants](constants.md).

Exemple 1, validation de données situé sur `Sheet1!A1:B2` avec les paramètres de critères de validation, d'alerte d'erreur de série après des données non valides sont entrées avec "Stop" style et titre personnalisé "error body":

!["La validation des données"](./images/data_validation_01.png "La validation des données")

```go
dv := excelize.NewDataValidation(true)
dv.SetSqref("A1:B2")
dv.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorBetween)
dv.SetError(excelize.DataValidationErrorStyleStop, "error title", "error body")
f.AddDataValidation("Sheet1", dv)
```

Exemple 2, définissez la validation des données sur `Sheet1!A3:B4` avec les paramètres de validation et affichez le message lorsque la cellule est sélectionnée:

!["La validation des données"](./images/data_validation_02.png "La validation des données")

```go
dv = excelize.NewDataValidation(true)
dv.SetSqref("A3:B4")
dv.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorGreaterThan)
dv.SetInput("input title", "input body")
f.AddDataValidation("Sheet1", dv)
```

Exemple 3, définissez la validation des données sur `Sheet1!A5:B6` avec les paramètres de validation, créez un menu déroulant dans la cellule en autorisant la source de liste:

!["La validation des données"](./images/data_validation_03.png "La validation des données")

```go
dv = excelize.NewDataValidation(true)
dv.SetSqref("A5:B6")
dv.SetDropList([]string{"1", "2", "3"})
f.AddDataValidation("Sheet1", dv)
```

Si vous saisissez les éléments dans la boîte de dialogue de validation des données (une liste délimitée), la limite est de 255 caractères, séparateurs compris. Si la formule source de votre liste de validation de données dépasse la limite de longueur maximale, veuillez définir les valeurs autorisées dans les cellules de la feuille de calcul et utilisez la fonction `SetSqrefDropList` pour définir la référence de leurs cellules.

Example 4，définir la validation des données sur `Sheet1!A7:B8` avec la source des critères de validation `Sheet1!E1:E3`, créer un menu déroulant dans la cellule en autorisant la source de liste:

!["Data validation"](./images/data_validation_04.png "Data validation")

```go
dv := excelize.NewDataValidation(true)
dv.SetSqref("A7:B8")
dv.SetSqrefDropList("$E$1:$E$3")
f.AddDataValidation("Sheet1", dv)
```

Il existe des limites au nombre d'éléments qui s'afficheront dans une liste déroulante de validation des données: la liste peut afficher 32768 éléments d'une liste sur la feuille de calcul. Si vous avez besoin de plus d'éléments que cela, vous pouvez créer une liste déroulante dépendante, divisée par catégorie.

## Obtenir la validation des données{#GetDataValidations}

```go
func (f *File) GetDataValidations(sheet string) ([]*DataValidation, error)
```

GetDataValidations renvoie la liste des validations de données par nom de feuille de calcul donné.

## Supprimer la validation des données {#DeleteDataValidation}

```go
func (f *File) DeleteDataValidation(sheet string, sqref ...string) error
```

DeleteDataValidation supprimer la validation des données par le nom de feuille de calcul et la séquence de référence donnés. Toutes les validations de données dans la feuille de calcul seront supprimées si vous ne spécifiez pas le paramètre de séquence de référence.
