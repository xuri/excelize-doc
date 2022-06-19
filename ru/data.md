# Данные

## Добавить проверку данных {#AddDataValidation}

```go
func (f *File) AddDataValidation(sheet string, dv *DataValidation)
```

AddDataValidation предоставляет проверенную проверку данных в диапазоне рабочего листа с помощью заданного объекта проверки данных и имени листа. Объект проверки данных может быть создан с помощью функции `NewDataValidation`. Тип и операторы проверки данных можно найти в разделе [Константы](constants.md).

Пример 1, установите проверку данных на `Sheet1!A1:B2` с настройками критериев проверки, покажите предупреждение об ошибке после ввода неверных данных с стилем "Stop" и пользовательским названием "error body":

!["Проверка данных"](./images/data_validation_01.png "Проверка данных")

```go
dvRange := excelize.NewDataValidation(true)
dvRange.Sqref = "A1:B2"
dvRange.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorBetween)
dvRange.SetError(excelize.DataValidationErrorStyleStop, "error title", "error body")
f.AddDataValidation("Sheet1", dvRange)
```

Пример 2, установите проверку данных на `Sheet1!A3:B4` с настройками критериев проверки и покажите входное сообщение, когда выбрана ячейка:

!["Проверка данных"](./images/data_validation_02.png "Проверка данных")

```go
dvRange = excelize.NewDataValidation(true)
dvRange.Sqref = "A3:B4"
dvRange.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorGreaterThan)
dvRange.SetInput("input title", "input body")
f.AddDataValidation("Sheet1", dvRange)
```

Пример 3, установите проверку данных на `Sheet1!A5:B6` с настройками критериев проверки, создайте раскрывающийся список в ячейке, используя источник списка:

!["Проверка данных"](./images/data_validation_03.png "Проверка данных")

```go
dvRange = excelize.NewDataValidation(true)
dvRange.Sqref = "A5:B6"
dvRange.SetDropList([]string{"1", "2", "3"})
f.AddDataValidation("Sheet1", dvRange)
```

Пример 4, установите проверку данных на `Sheet1!A7:B8` с параметрами критериев проверки. Параметры `Sheet1!E1:E3`, создайте раскрывающийся список в ячейке, разрешив источник списка:

!["Data validation"](./images/data_validation_04.png "Data validation")

```go
dvRange := excelize.NewDataValidation(true)
dvRange.Sqref = "A7:B8"
dvRange.SetSqrefDropList("$E$1:$E$3")
f.AddDataValidation("Sheet1", dvRange)
```

## Удалить данные проверки {#DeleteDataValidation}

```go
func (f *File) DeleteDataValidation(sheet string, sqref ...string) error
```

DeleteDataValidation удалить проверку данных по заданному имени рабочего листа и последовательности ссылок. Все проверки данных на листе будут удалены, если не указать параметр эталонной последовательности.
