# Datos

## Agregar validación de datos {#AddDataValidation}

```go
func (f *File) AddDataValidation(sheet string, dv *DataValidation)
```

AddDataValidation proporciona una validación de datos establecida en un rango de la hoja de trabajo por objeto de validación de datos y nombre de la hoja de trabajo. El objeto de validación de datos puede ser creado por la función `NewDataValidation`. Los operadores y el tipo de validación de datos se pueden encontrar en la sección [Constants](constants.md).

Ejemplo 1, configure la validación de datos en `Sheet1!A1:B2` con la configuración de los criterios de validación, Mostrar alerta de error después de ingresar datos no válidos con el estilo "Detener" y el título personalizado "cuerpo de error":

<p align="center"><img width="683" src="./images/data_validation_01.png" alt="Validación de datos"></p>

```go
dv := excelize.NewDataValidation(true)
dv.SetSqref("A1:B2")
dv.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorBetween)
dv.SetError(excelize.DataValidationErrorStyleStop, "error title", "cuerpo de error")
f.AddDataValidation("Sheet1", dv)
```

Ejemplo 2, configure la validación de datos en `Sheet1!A3:B4` con la configuración de los criterios de validación y muestre el mensaje de entrada cuando se seleccione la celda:

<p align="center"><img width="683" src="./images/data_validation_02.png" alt="Validación de datos"></p>

```go
dv = excelize.NewDataValidation(true)
dv.SetSqref("A3:B4")
dv.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorGreaterThan)
dv.SetInput("input title", "input body")
f.AddDataValidation("Sheet1", dv)
```

Ejemplo 3, configure la validación de datos en `Sheet1!A5:B6` con la configuración de los criterios de validación, cree un menú desplegable en la celda permitiendo la fuente de la lista:

<p align="center"><img width="683" src="./images/data_validation_03.png" alt="Validación de datos"></p>

```go
dv = excelize.NewDataValidation(true)
dv.SetSqref("A5:B6")
dv.SetDropList([]string{"1", "2", "3"})
f.AddDataValidation("Sheet1", dv)
```

Si escribe los elementos en el cuadro de diálogo de validación de datos (una lista delimitada), el límite es de 255 caracteres, incluidos los separadores. Si la fórmula de origen de su lista de validación de datos supera el límite de longitud máxima, establezca los valores permitidos en las celdas de la hoja de trabajo y utilice la función `SetSqrefDropList` para establecer la referencia para sus celdas.

Ejemplo 4, configure la validación de datos en `Sheet1!A7:B8` con la fuente de criterios de validación `Sheet1!E1:E3`, cree un menú desplegable en la celda permitiendo la fuente de la lista:

<p align="center"><img width="683" src="./images/data_validation_04.png" alt="Validación de datos"></p>

```go
dv := excelize.NewDataValidation(true)
dv.SetSqref("A7:B8")
dv.SetSqrefDropList("$E$1:$E$3")
f.AddDataValidation("Sheet1", dv)
```

Hay límites en la cantidad de elementos que se mostrarán en una lista desplegable de validación de datos: la lista puede mostrar hasta 32768 elementos de una lista en la hoja de trabajo. Si necesita más elementos, puede crear una lista desplegable dependiente, desglosada por categoría.

## Obtener validación de datos{#GetDataValidations}

```go
func (f *File) GetDataValidations(sheet string) ([]*DataValidation, error)
```

GetDataValidations devuelve la lista de validaciones de datos por nombre de hoja de trabajo dado.

## Eliminar validación de datos {#DeleteDataValidation}

```go
func (f *File) DeleteDataValidation(sheet string, sqref ...string) error
```

DeleteDataValidation elimina la validación de datos por el nombre de la hoja de trabajo y la secuencia de referencia. Todas las validaciones de datos en la hoja de trabajo se eliminarán si no se especifica el parámetro de secuencia de referencia.
