# Utilidades

## Agregar tabla {#AddTable}

```go
func (f *File) AddTable(sheet string, table *Table) error
```

AddTable proporciona el método para agregar una tabla en una hoja de trabajo por el nombre de la hoja de trabajo, el área de coordenadas y el conjunto de formato dados.

- Ejemplo 1, cree una tabla de `A1:D5` en `Sheet1`:

<p align="center"><img width="612" src="./images/addtable_01.png" alt="Agregar tabla"></p>

```go
err := f.AddTable("Sheet1", &excelize.Table{Range: "A1:D5"})
```

- Ejemplo 2, cree una tabla de `F2:H6` en `Sheet2` con el formato establecido:

<p align="center"><img width="612" src="./images/addtable_02.png" alt="Agregar tabla con conjunto de formato"></p>

```go
disable := false
err := f.AddTable("Sheet2", &excelize.Table{
    Range:             "F2:H6",
    Name:              "table",
    StyleName:         "TableStyleMedium2",
    ShowFirstColumn:   true,
    ShowLastColumn:    true,
    ShowRowStripes:    &disable,
    ShowColumnStripes: true,
})
```

Tenga en cuenta que la tabla debe tener al menos dos líneas, incluido el encabezado. Las celdas del encabezado deben contener cadenas y deben ser únicas, y deben establecer los datos de la fila del encabezado de la tabla antes de llamar a la función AddTable. Varias tablas coordinan áreas que no pueden tener una intersección.

`Name`: El nombre de la tabla, en el mismo nombre de hoja de trabajo de la tabla, debe ser único.

`StyleName`: Los nombres de estilo de tabla integrados:

```text
TableStyleLight1 - TableStyleLight21
TableStyleMedium1 - TableStyleMedium28
TableStyleDark1 - TableStyleDark11
```

Índice|Estilo|Índice|Estilo|Índice|Estilo
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

## Obtener tablas {#GetTables}

```go
func (f *File) GetTables(sheet string) ([]Table, error)
```

GetTables proporciona el método para obtener todas las tablas de una hoja de trabajo según el nombre de la hoja de trabajo.

## Eliminar tabla {#DeleteTable}

```go
func (f *File) DeleteTable(name string) error
```

DeleteTable proporciona el método para eliminar una tabla según el nombre de la tabla.

## Filtro automático {#AutoFilter}

```go
func (f *File) AutoFilter(sheet, rangeRef string, opts []AutoFilterOptions) error
```

AutoFilter proporciona el método para agregar un filtro automático en una hoja de trabajo por el nombre de la hoja de trabajo, el área de coordenadas y la configuración. Un filtro automático en Excel es una forma de filtrar un rango de datos 2D basado en algunos criterios simples.

Ejemplo 1, aplicando un filtro automático a un rango de celdas `A1:D4` en la `Sheet1`:

<p align="center"><img width="612" src="./images/autofilter_01.png" alt="Agregar filtro automático"></p>

```go
err := f.AutoFilter("Sheet1", "A1:D4", []excelize.AutoFilterOptions{})
```

Ejemplo 2, filtrar datos en un filtro automático:

```go
err := f.AutoFilter("Sheet1", "A1:D4", []excelize.AutoFilterOptions{
    {Column: "B", Expression: "x != blanks"},
})
```

`Column` define las columnas de filtro en un rango de filtro automático basado en criterios simples.

No es suficiente especificar la condición del filtro. También debe ocultar las filas que no coincidan con la condición del filtro. Las filas se ocultan mediante el método [`SetRowVisible()`](sheet.md#SetRowVisible). Excelize no puede filtrar filas automáticamente porque esto no es parte del formato de archivo.

Establecer criterios de filtro para una columna:

`Expression` define las condiciones, los siguientes operadores están disponibles para establecer los criterios de filtrado:

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

Una expresión puede comprender una sola declaración o dos declaraciones separadas por los operadores `and` y `or`. Por ejemplo:

```text
x <  2000
x >  2000
x == 2000
x >  2000 and x <  5000
x == 2000 or  x == 5000
```

El filtrado de datos en blanco o no en blanco se puede lograr utilizando un valor de Blanks o NonBlanks en la expresión:

```text
x == Blanks
x == NonBlanks
```

Office Excel también permite algunas operaciones simples de coincidencia de cadenas:

```text
x == b*      // comienza con b
x != b*      // no comienza con b
x == *b      // termina con b
x != *b      // no termina con b
x == *b*     // contiene b
x != *b*     // no contiene b
```

También puede utilizar `*` para hacer coincidir cualquier carácter o número y `?` Para hacer coincidir cualquier carácter o número. Los filtros de Excel no admiten ningún otro cuantificador de expresión regular. Los caracteres de expresión regular de Excel se pueden escapar usando `~`.

La variable de marcador de posición `x` en los ejemplos anteriores se puede reemplazar por cualquier cadena simple. El nombre real del marcador de posición se ignora internamente, por lo que los siguientes son todos equivalentes:

```text
x     < 2000
col   < 2000
Price < 2000
```

## Actualizar valor vinculado {#UpdateLinkedValue}

```go
func (f *File) UpdateLinkedValue() error
```

UpdateLinkedValue corrige los valores vinculados dentro de una hoja de cálculo no se actualizan en Office Excel 2007 y 2010. Esta función eliminará la etiqueta de valor cuando se encuentre una celda que tenga un valor vinculado. Referencia [https://learn.microsoft.com/en-us/archive/msdn-technet-forums/e16bae1f-6a2c-4325-8013-e989a3479066](https://learn.microsoft.com/en-us/archive/msdn-technet-forums/e16bae1f-6a2c-4325-8013-e989a3479066). Aviso: después de abrir el archivo de hoja de cálculo, Excel actualizará el valor vinculado y generará un nuevo valor y solicitará guardar el archivo o no.

El efecto de borrar el caché de la celda en el libro de trabajo aparece como una modificación de la etiqueta `<v>`, por ejemplo, el caché de la celda antes de borrar:

```xml
<row r="19">
    <c r="B19">
        <f>SUM(Sheet2!D2,Sheet2!D11)</f>
        <v>100</v>
     </c>
</row>
```

Después de borrar la memoria caché de la celda:

```xml
<row r="19">
    <c r="B19">
        <f>SUM(Sheet2!D2,Sheet2!D11)</f>
    </c>
</row>
```

## Nombre de celda dividida {#SplitCellName}

```go
func SplitCellName(cell string) (string, int, error)
```

SplitCellName divide el nombre de la celda en el nombre de la columna y el número de fila. Por ejemplo:

```go
excelize.SplitCellName("AK74") // regreso "AK", 74, nil
```

## Unir el nombre de la celda {#JoinCellName}

```go
func JoinCellName(col string, row int) (string, error)
```

JoinCellName une el nombre de la celda del nombre de la columna y el número de fila.

## Nombre de columna a número {#ColumnNameToNumber}

```go
func ColumnNameToNumber(name string) (int, error)
```

ColumnNameToNumber proporciona una función para convertir el nombre de la columna de la hoja de Excel a `int`. El nombre de la columna no distingue entre mayúsculas y minúsculas. La función devuelve un error si el nombre de la columna es incorrecto. Por ejemplo:

```go
excelize.ColumnNameToNumber("AK") // regreso 37, nil
```

## El número de columna al nombre {#ColumnNumberToName}

```go
func ColumnNumberToName(num int) (string, error)
```

ColumnNumberToName proporciona una función para convertir el número entero al título de la columna de la hoja de Excel. Por ejemplo:

```go
excelize.ColumnNumberToName(37) // regreso "AK", nil
```

## Nombre de la celda a las coordenadas {#CellNameToCoordinates}

```go
func CellNameToCoordinates(cell string) (int, int, error)
```

CellNameToCoordinates convierte el nombre de celda alfanumérico en coordenadas `[X, Y]` o devuelve un error. Por ejemplo:

```go
excelize.CellNameToCoordinates("A1") // regreso 1, 1, nil
excelize.CellNameToCoordinates("Z3") // regreso 26, 3, nil
```

## Coordenadas al nombre de la celda {#CoordinatesToCellName}

```go
func CoordinatesToCellName(col, row int, abs ...bool) (string, error)
```

CoordinatesToCellName convierte las coordenadas `[X, Y]` a un nombre de celda alfanumérico o devuelve un error. Por ejemplo:

```go
excelize.CoordinatesToCellName(1, 1) // regreso "A1", nil
excelize.CoordinatesToCellName(1, 1, true) // regreso "$A$1", nil
```

## Crear estilo condicional {#NewConditionalStyle}

```go
func (f *File) NewConditionalStyle(style *Style) (int, error)
```

NewConditionalStyle proporciona una función para crear un estilo para el formato condicional por formato de estilo dado. Los parámetros son los mismos que los de la función [`NewStyle`](style.md#NewStyle). Tenga en cuenta que el campo de color utiliza código de color RGB y solo admite la configuración de fuente, rellenos, alineación y bordes actualmente.

## Obtener estilo condicional {#GetConditionalStyle}

```go
func (f *File) GetConditionalStyle(idx int) (*Style, error)
```

GetConditionalStyle devuelve la definición de estilo de formato condicional según el índice de estilo especificado.

## Establecer formato condicional {#SetConditionalFormat}

```go
func (f *File) SetConditionalFormat(sheet, rangeRef string, opts []ConditionalFormatOptions) error
```

SetConditionalFormat proporciona una función para crear una regla de formato condicional para el valor de la celda. El formato condicional es una característica de Office Excel que le permite aplicar un formato a una celda o un rango de celdas según ciertos criterios.

La opción `Type` es un parámetro obligatorio y no tiene un valor predeterminado. Los valores de tipo permitidos y sus parámetros asociados son:

<table>
    <thead>
        <tr>
            <th>Tipo</th>
            <th>Parámetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=4>cell</td>
            <td>Criteria</td>
        </tr>
        <tr>
            <td>Value</td>
        </tr>
        <tr>
            <td>MinValue</td>
        </tr>
        <tr>
            <td>MaxValue</td>
        </tr>
        <tr>
            <td>time_period</td>
            <td>Criteria</td>
        </tr>
        <tr>
            <td rowspan=2>text</td>
            <td>Criteria</td>
        </tr>
        <tr>
            <td>Value</td>
        </tr>
        <tr>
            <td>average</td>
            <td>Criteria</td>
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
            <td>Criteria</td>
        </tr>
        <tr>
            <td>Value</td>
        </tr>
        <tr>
            <td rowspan=2>bottom</td>
            <td>Criteria</td>
        </tr>
        <tr>
            <td>Value</td>
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
            <td>MinType</td>
        </tr>
        <tr>
            <td>MaxType</td>
        </tr>
        <tr>
            <td>MinValue</td>
        </tr>
        <tr>
            <td>MaxValue</td>
        </tr>
        <tr>
            <td>MinColor</td>
        </tr>
        <tr>
            <td>MaxColor</td>
        </tr>
        <tr>
            <td rowspan=9>3_color_scale</td>
            <td>MinType</td>
        </tr>
        <tr>
            <td>MidType</td>
        </tr>
        <tr>
            <td>MaxType</td>
        </tr>
        <tr>
            <td>MinValue</td>
        </tr>
        <tr>
            <td>MidValue</td>
        </tr>
        <tr>
            <td>MaxValue</td>
        </tr>
        <tr>
            <td>MinColor</td>
        </tr>
        <tr>
            <td>MidColor</td>
        </tr>
        <tr>
            <td>MaxColor</td>
        </tr>
        <tr>
            <td rowspan=9>data_bar</td>
            <td>MinType</td>
        </tr>
        <tr>
            <td>MaxType</td>
        </tr>
        <tr>
            <td>MinValue</td>
        </tr>
        <tr>
            <td>MaxValue</td>
        </tr>
        <tr>
            <td>BarBorderColor</td>
        </tr>
        <tr>
            <td>BarColor</td>
        </tr>
        <tr>
            <td>BarDirection</td>
        </tr>
        <tr>
            <td>BarOnly</td>
        </tr>
        <tr>
            <td>BarSolid</td>
        </tr>
        <tr>
            <td rowspan=3>iconSet</td>
            <td>IconStyle</td>
        </tr>
        <tr>
            <td>ReverseIcons</td>
        </tr>
        <tr>
            <td>IconsOnly</td>
        </tr>
        <tr>
            <td>formula</td>
            <td>Criteria</td>
        </tr>
    </tbody>
</table>

El parámetro `Criteria` se utiliza para establecer los criterios por los cuales se evaluarán los datos de la celda. No tiene ningún valor predeterminado. Los criterios más comunes aplicados a `excelize.ConditionalFormatOptions{Type: "cell"}` son:

Carácter de descripción de texto|Representación simbólica
---|---
between|
not between|
equal to|==
not equal to|!=
greater than|>
less than|<
greater than or equal to|>=
less than or equal to|<=

Puede utilizar las cadenas de descripción textual de Excel, en la primera columna de arriba, o las alternativas simbólicas más comunes.

Los criterios adicionales que son específicos de otros tipos de formato condicional se muestran en las secciones relevantes a continuación.

`Value`: El valor se usa generalmente junto con el parámetro `Criteria` para establecer la regla por la cual se evaluarán los datos de la celda:

```go
err := f.SetConditionalFormat("Sheet1", "D1:D10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "cell",
            Criteria: ">",
            Format:   format,
            Value:    "6",
        },
    },
)
```

La propiedad `Value` también puede ser una referencia de celda:

```go
err := f.SetConditionalFormat("Sheet1", "D1:D10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "cell",
            Criteria: ">",
            Format:   format,
            Value:    "$C$1",
        },
    },
)
```

type: `Format` - El parámetro `Format` se utiliza para especificar el formato que se aplicará a la celda cuando se cumpla el criterio de formato condicional. El formato se crea usando el método [`NewConditionalStyle()`](utils.md#NewConditionalStyle) de la misma manera que los formatos de celda:

```go
format, err := f.NewConditionalStyle(
    &excelize.Style{
        Font: &excelize.Font{Color: "9A0511"},
        Fill: excelize.Fill{
            Type: "pattern", Color: []string{"FEC7CE"}, Pattern: 1,
        },
    },
)
if err != nil {
    fmt.Println(err)
}
err = f.SetConditionalFormat("Sheet1", "D1:D10",
    []excelize.ConditionalFormatOptions{
        {Type: "cell", Criteria: ">", Format: format, Value: "6"},
    },
)
```

Nota: En Excel, se superpone un formato condicional sobre el formato de celda existente y no todas las propiedades del formato de celda se pueden modificar. Las propiedades que no se pueden modificar en un formato condicional son nombre de fuente, tamaño de fuente, superíndice y subíndice, bordes diagonales, todas las propiedades de alineación y todas las propiedades de protección.

Excel especifica algunos formatos predeterminados que se utilizarán con formato condicional. Estos se pueden replicar utilizando los siguientes formatos de Excel:

```go
// Formato rosa para mal condicional.
format1, err := f.NewConditionalStyle(
    &excelize.Style{
        Font: &excelize.Font{Color: "9A0511"},
        Fill: excelize.Fill{
            Type: "pattern", Color: []string{"FEC7CE"}, Pattern: 1,
        },
    },
)

// Formato amarillo claro para condicional neutro.
format2, err := f.NewConditionalStyle(
    &excelize.Style{
        Font: &excelize.Font{Color: "9B5713"},
        Fill: excelize.Fill{
            Type: "pattern", Color: []string{"FEEAA0"}, Pattern: 1,
        },
    },
)

// Formato verde claro para buenas condiciones.
format3, err := f.NewConditionalStyle(
    &excelize.Style{
        Font: &excelize.Font{Color: "09600B"},
        Fill: excelize.Fill{
            Type: "pattern", Color: []string{"C7EECF"}, Pattern: 1,
        },
    },
)
```

type: `MinValue` - El parámetro `MinValue` se utiliza para establecer el valor límite inferior cuando el `Criteria` es `between` o `not between`.

```go
// Regla de las celdas resaltadas: entre...
err := f.SetConditionalFormat("Sheet1", "A1:A10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "cell",
            Criteria: "between",
            Format:   format,
            MinValue: "6",
            MaxValue: "8",
        },
    },
)
```

type: `MaxValue` - El parámetro `maximum` se utiliza para establecer el valor límite superior cuando los criterios están `between` o `not between`. Vea el ejemplo anterior.

type: `average` - El tipo `average` se utiliza para especificar el formato condicional de estilo "Average" de Office Excel:

```go
// Reglas superiores/inferiores: por encima del promedio...
err := f.SetConditionalFormat("Sheet1", "A1:A10",
    []excelize.ConditionalFormatOptions{
        {
            Type:         "average",
            Criteria:     "=",
            Format:       format1,
            AboveAverage: true,
        },
    },
)

// Reglas superiores/inferiores: Inferior al promedio...
err := f.SetConditionalFormat("Sheet1", "B1:B10",
    []excelize.ConditionalFormatOptions{
        {
            Type:         "average",
            Criteria:     "=",
            Format:       format2,
            AboveAverage: false,
        },
    },
)
```

type: `duplicate` - El tipo `duplicate` se usa para resaltar celdas duplicadas en un rango:

```go
// Resaltar reglas de celdas: valores duplicados...
err := f.SetConditionalFormat("Sheet1", "A1:A10",
    []excelize.ConditionalFormatOptions{
        {Type: "duplicate", Criteria: "=", Format: format},
    },
)
```

type: `unique` - El tipo `unique` se usa para resaltar celdas únicas en un rango:

```go
// Resaltar reglas de celdas: No es igual a...
err := f.SetConditionalFormat("Sheet1", "A1:A10",
    []excelize.ConditionalFormatOptions{
        {Type: "unique", Criteria: "=", Format: format},
    },
)
```

type: `top` - El tipo `top` se usa para especificar los n valores principales por número o porcentaje en un rango:

```go
// Reglas de Top/Bottom: Top 10.
err := f.SetConditionalFormat("Sheet1", "H1:H10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "top",
            Criteria: "=",
            Format:   format,
            Value:    "6",
        },
    },
)
```

Los criterios se pueden utilizar para indicar que se requiere una condición de porcentaje:

```go
err := f.SetConditionalFormat("Sheet1", "A1:A10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "top",
            Criteria: "=",
            Format:   format,
            Value:    "6",
            Percent:  true,
        },
    },
)
```

type: `2_color_scale` - El tipo `2_color_scale` se utiliza para especificar el formato condicional de estilo "Escala de 2 colores" de Excel:

```go
// Escalas de color: 2 colores.
err := f.SetConditionalFormat("Sheet1", "A1:A10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "2_color_scale",
            Criteria: "=",
            MinType:  "min",
            MaxType:  "max",
            MinColor: "#F8696B",
            MaxColor: "#63BE7B",
        },
    },
)
```

Este tipo condicional se puede modificar con `MinType`, `MaxType`, `MinValue`, `MaxValue`, `MinColor` y `MaxColor`, ver más abajo.

type: `3_color_scale` - El tipo `3_color_scale` se utiliza para especificar el formato condicional de estilo "Escala de 3 colores" de Excel:

```go
// Escalas de color: 3 colores.
err := f.SetConditionalFormat("Sheet1", "A1:A10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "3_color_scale",
            Criteria: "=",
            MinType:  "min",
            MidType:  "percentile",
            MaxType:  "max",
            MinColor: "#F8696B",
            MidColor: "#FFEB84",
            MaxColor: "#63BE7B",
        },
    },
)
```

Este tipo condicional se puede modificar con `MinType`, `MidType`, `MaxType`, `MinValue`, `MidValue`, `MaxValue`, `MinColor`, `MidColor` y `MaxColor`, ver más abajo.

type: `data_bar` - El tipo `data_bar` se utiliza para especificar el formato condicional de estilo "Data Bar" de Excel.

`MinType` - Las propiedades `MinType` y `MaxType` están disponibles cuando el tipo de formato condicional es `2_color_scale`, `3_color_scale` o `data_bar`. El `MidType` está disponible para `3_color_scale`. Las propiedades se utilizan de la siguiente manera:

```go
// Barras de datos: relleno degradado.
err := f.SetConditionalFormat("Sheet1", "K1:K10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "data_bar",
            Criteria: "=",
            MinType:  "min",
            MaxType:  "max",
            BarColor: "#638EC6",
        },
    },
)
```

Los tipos `min/mid/max` disponibles son:

Parámetro|Explicación
---|---
min|El valor mínimo (solo para `MinType`)
num|Numérica
percent|Porcentaje
percentile|Percentil
formula|Fórmula
max|Máxima (solo para `MaxType`)

`MidType` - Usado para `3_color_scale`. Igual que `MinType`, ver arriba.

`MaxType` - Igual que `MinType`, ver arriba.

`MinValue` - Las propiedades `MinValue` y `MaxValue` están disponibles cuando el tipo de formato condicional es `2_color_scale`, `3_color_scale` o `data_bar`. El `MidValue` está disponible para `3_color_scale`.

`MidValue` - Usado para `3_color_scale`. Igual que `MinValue`, ver arriba.

`MaxValue` - Igual que `MinValue`, ver arriba.

`MinColor` - Las propiedades `MinColor` y `MaxColor` están disponibles cuando el tipo de formato condicional es `2_color_scale`, `3_color_scale` o `data_bar`. El `MidColor` está disponible para `3_color_scale`. Las propiedades se utilizan de la siguiente manera:

```go
// Escalas de color: 3 colores.
err := f.SetConditionalFormat("Sheet1", "B1:B10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "3_color_scale",
            Criteria: "=",
            MinType:  "min",
            MidType:  "percentile",
            MaxType:  "max",
            MinColor: "#F8696B",
            MidColor: "#FFEB84",
            MaxColor: "#63BE7B",
        },
    },
)
```

`MidColor` - Usado para `3_color_scale`. Igual que `MinColor`, ver arriba.

`MaxColor` - Igual que `MinColor`, ver arriba.

`BarColor` - Usado para `data_bar`. Igual que `MinColor`, ver arriba.

`BarBorderColor` - Se utiliza para establecer el color de la línea del borde de una barra de datos, esto solo es visible en Excel 2010 y versiones posteriores.

`BarDirection` - Usado para establece la dirección de las barras de datos. Las opciones disponibles son:

Valor|Explicación
---|---
context     | La aplicación de hoja de cálculo establece la dirección de la barra de datos según el contexto de los datos que se muestran.
leftToRight | La dirección de la barra de datos es de derecha a izquierda.
rightToLeft | La dirección de la barra de datos es de izquierda a derecha.

`BarOnly` - Usado para establecer muestra una barra de datos pero no los datos en las celdas.

`BarSolid` - Se usa para activar un relleno sólido (sin degradado) para las barras de datos, esto solo es visible en Excel 2010 y versiones posteriores.

`IconStyle` - Las opciones disponibles son:

|Valor|
|---|
|3Arrows        |
|3ArrowsGray    |
|3Flags         |
|3Signs         |
|3Symbols       |
|3Symbols2      |
|3TrafficLights1|
|3TrafficLights2|
|4Arrows        |
|4ArrowsGray    |
|4Rating        |
|4RedToBlack    |
|4TrafficLights |
|5Arrows        |
|5ArrowsGray    |
|5Quarters      |
|5Rating        |

`ReverseIcons` - Se utiliza para establecer conjuntos de iconos invertidos.

`IconsOnly` - Se utiliza para el conjunto que se muestra sin el valor de la celda.

`StopIfTrue` - Se utiliza para establecer la función "detener si es verdadero" de una regla de formato condicional cuando se aplica más de una regla a una celda o rango de celdas. Cuando se establece este parámetro, las reglas posteriores no se evalúan si la regla actual es verdadera.

Por ejemplo, resalte los valores más altos y más bajos en un rango de celdas `A1:D4` estableciendo un formato condicional en `Sheet1`:

<p align="center"><img width="938" src="./images/condition_format_01.png" alt="Establecer formato condicional en un rango de celdas"></p>

```go
func main() {
    f := excelize.NewFile()
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    for r := 1; r <= 4; r++ {
        row := []int{
            rand.Intn(100), rand.Intn(100), rand.Intn(100), rand.Intn(100),
        }
        if err := f.SetSheetRow("Sheet1", fmt.Sprintf("A%d", r), &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    red, err := f.NewConditionalStyle(
        &excelize.Style{
            Font: &excelize.Font{
                Color: "9A0511",
            },
            Fill: excelize.Fill{
                Type:    "pattern",
                Color:   []string{"FEC7CE"},
                Pattern: 1,
            },
        },
    )
    if err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SetConditionalFormat("Sheet1", "A1:D4",
        []excelize.ConditionalFormatOptions{
            {
                Type:     "bottom",
                Criteria: "=",
                Value:    "1",
                Format:   red,
            },
        },
    ); err != nil {
        fmt.Println(err)
        return
    }
    green, err := f.NewConditionalStyle(
        &excelize.Style{
            Font: &excelize.Font{
                Color: "09600B",
            },
            Fill: excelize.Fill{
                Type:    "pattern",
                Color:   []string{"C7EECF"},
                Pattern: 1,
            },
        },
    )
    if err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SetConditionalFormat("Sheet1", "A1:D4",
        []excelize.ConditionalFormatOptions{
            {
                Type:     "top",
                Criteria: "=",
                Value:    "1",
                Format:   green,
            },
        },
    ); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
        return
    }
}
```

## Obtener formato condicional {#GetConditionalFormats}

```go
func (f *File) GetConditionalFormats(sheet string) (map[string][]ConditionalFormatOptions, error)
```

GetConditionalFormats devuelve la configuración de formato condicional según el nombre de la hoja de cálculo.

## Eliminar formato condicional {#UnsetConditionalFormat}

```go
func (f *File) UnsetConditionalFormat(sheet, rangeRef string) error
```

UnsetConditionalFormat proporciona una función para anular el formato condicional por el nombre y el rango de la hoja de trabajo.

## Establecer paneles {#SetPanes}

```go
func (f *File) SetPanes(sheet string, panes *Panes) error
```

SetPanes proporciona una función para crear y eliminar paneles congelados y paneles divididos según el nombre de la hoja de trabajo y el formato de paneles determinados.

`ActivePane` define el panel que está activo. Los posibles valores para este atributo se definen en la siguiente tabla:

Valor de enumeración|Descripción
---|---
bottomLeft (Panel inferior izquierdo) |Panel inferior izquierdo cuando se aplican divisiones verticales y horizontales.<br><br>Este valor también se usa cuando solo se ha aplicado una división horizontal, dividiendo el panel en regiones superior e inferior. En ese caso, este valor especifica el panel inferior.
bottomRight (Panel inferior derecho) | Panel inferior derecho, cuando se aplican divisiones verticales y horizontales.
topLeft (Panel superior izquierdo)|Panel superior izquierdo, cuando se aplican divisiones verticales y horizontales.<br><br>Este valor también se usa cuando solo se ha aplicado una división horizontal, dividiendo el panel en regiones superior e inferior. En ese caso, este valor especifica el panel superior.<br><br>Este valor también se usa cuando solo se ha aplicado una división vertical, dividiendo el panel en regiones derecha e izquierda. En ese caso, este valor especifica el panel izquierdo.
topRight (Panel superior derecho)|Panel superior derecho, cuando se aplican divisiones verticales y horizontales.<br><br> Este valor también se usa cuando solo se ha aplicado una división vertical, dividiendo el panel en regiones derecha e izquierda. En ese caso, este valor especifica el panel derecho.

El tipo de estado de panel está restringido a los valores admitidos actualmente enumerados en la siguiente tabla:

Valor de enumeración|Descripción
---|---
frozen (Congelada)|Los paneles están congelados, pero no se dividieron al congelarse. En este estado, cuando los paneles se descongelan nuevamente, se produce un solo panel, sin división.<br><br>En este estado, las barras divididas no son ajustables.
split (División)|Los paneles están divididos, pero no congelados. En este estado, las barras divididas son ajustables por el usuario.

`XSplit` - Posición horizontal de la división, en una vigésima parte de un punto; 0 (cero) si ninguno. Si el panel está congelado, este valor indica el número de columnas visibles en el panel superior.

`YSplit` - La posición vertical de la división, en una vigésima parte de un punto; 0 (cero) si ninguno. Si el panel está congelado, este valor indica el número de filas visibles en el panel izquierdo. Los valores posibles para este atributo están definidos por el tipo de datos doble del esquema XML del W3C.

`TopLeftCell` - Ubicación de la celda visible superior izquierda en el panel inferior derecho (en el modo de izquierda a derecha).

`SQRef` - Rango de la selección. Puede ser un conjunto de rangos no contiguos.

Ejemplo 1: congelar la columna `A` en la `Sheet1` y establecer la celda activa en `Sheet1!K16`:

<p align="center"><img width="770" src="./images/setpans_01.png" alt="Columna congelada"></p>

```go
err := f.SetPanes("Sheet1", &excelize.Panes{
    Freeze:      true,
    XSplit:      1,
    TopLeftCell: "B1",
    ActivePane:  "topRight",
    Selection: []excelize.Selection{
        {SQRef: "K16", ActiveCell: "K16", Pane: "topRight"},
    },
})
```

Ejemplo 2: congele las filas 1 a 9 en la `Sheet1` y establezca los rangos de celdas activas en `Sheet1!A11:XFD11`:

<p align="center"><img width="770" src="./images/setpans_02.png" alt="Congelar columnas y establecer rangos de celdas activos"></p>

```go
err := f.SetPanes("Sheet1", &excelize.Panes{
    Freeze:      true,
    YSplit:      9,
    TopLeftCell: "A34",
    ActivePane:  "bottomLeft",
    Selection: []excelize.Selection{
        {SQRef: "A11:XFD11", ActiveCell: "A11", Pane: "bottomLeft"},
    },
})
```

Ejemplo 3: cree paneles divididos en `Sheet1` y establezca la celda activa en `Sheet1!J60`:

<p align="center"><img width="755" src="./images/setpans_03.png" alt="Crear paneles divididos"></p>

```go
err := f.SetPanes("Sheet1", &excelize.Panes{
    Split:       true,
    XSplit:      3270,
    YSplit:      1800,
    TopLeftCell: "N57",
    ActivePane:  "bottomLeft",
    Selection: []excelize.Selection{
        {SQRef: "I36", ActiveCell: "I36"},
        {SQRef: "G33", ActiveCell: "G33", Pane: "topRight"},
        {SQRef: "J60", ActiveCell: "J60", Pane: "bottomLeft"},
        {SQRef: "O60", ActiveCell: "O60", Pane: "bottomRight"},
    },
})
```

Ejemplo 4, descongelar y quitar todos los paneles en `Sheet1`:

```go
err := f.SetPanes("Sheet1", &excelize.Panes{Freeze: false, Split: false})
```

## Obtener paneles {#GetPanes}

```go
func (f *File) GetPanes(sheet string) (Panes, error)
```

GetPanes proporciona una función para obtener paneles inmovilizados, paneles divididos y vistas de hoja de cálculo por nombre de hoja de cálculo determinado.

## Color {#ThemeColor}

```go
func (f *File) GetBaseColor(hexColor string, indexedColor int, themeColor *int) string
```

GetBaseColor devuelve el código de color hexadecimal preferido proporcionando un código de color hexadecimal, un color indexado y un color de tema.

```go
func ThemeColor(baseColor string, tint float64) string
```

ThemeColor aplicó el color con valor de tinte.

Hay 3 tipos de colores para el texto en la hoja de cálculo: color hexadecimal, color indexado y color de tema. La prioridad de estos colores es que el color hexadecimal tiene prioridad sobre el color del tema, y el color del tema tiene prioridad sobre el color indexado. Además, el color también admite la aplicación de un valor de matiz basado en el color hexadecimal, por lo que necesitamos usar la función ThemeColor para aplicar el matiz del color basado para obtener el valor de color hexadecimal calculado. Por ejemplo:

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f, err := excelize.OpenFile("Book1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    runs, err := f.GetCellRichText("Sheet1", "A1")
    if err != nil {
        fmt.Println(err)
        return
    }
    for _, run := range runs {
        var hexColor string
        if run.Font != nil {
            baseColor := f.GetBaseColor(run.Font.Color, run.Font.ColorIndexed, run.Font.ColorTheme)
            hexColor = strings.TrimPrefix(excelize.ThemeColor(baseColor, run.Font.ColorTint), "FF")
        }
        fmt.Printf("text: %s, color: %s\r\n", run.Text, hexColor)
    }
}
```

## Convertir RGB a HSL {#RGBToHSL}

```go
func RGBToHSL(r, g, b uint8) (h, s, l float64)
```

RGBToHSL convierte un triple RGB en un triple HSL.

## Convertir HSL a RGB {#HSLToRGB}

```go
func HSLToRGB(h, s, l float64) (r, g, b uint8)
```

HSLToRGB convierte un triple HSL en un triple RGB.

## Escritor de archivos {#FileWriter}

### Write {#Write}

```go
func (f *File) Write(w io.Writer, opts ...Options) error
```

Write proporciona una función para escribir en un `io.Writer`.

### WriteTo {#WriteTo}

```go
func (f *File) WriteTo(w io.Writer, opts ...Options) (int64, error)
```

WriteTo implementa `io.WriterTo` para escribir el archivo.

### WriteToBuffer {#WriteToBuffer}

```go
func (f *File) WriteToBuffer() (*bytes.Buffer, error)
```

WriteToBuffer proporciona una función para obtener `*bytes.Buffer` del archivo guardado.

## Agregar proyecto VBA {#AddVBAProject}

```go
func (f *File) AddVBAProject(file []byte) error
```

AddVBAProject proporciona el método para agregar el archivo `vbaProject.bin` que contiene funciones y/o macros. La extensión del archivo debe ser `.xlsm` o `.xltm`. Por ejemplo:

```go
codeName := "Sheet1"
if err := f.SetSheetProps("Sheet1", &excelize.SheetPropsOptions{
    CodeName: &codeName,
}); err != nil {
    fmt.Println(err)
    return
}
file, err := os.ReadFile("vbaProject.bin")
if err != nil {
    fmt.Println(err)
    return
}
if err := f.AddVBAProject(file); err != nil {
    fmt.Println(err)
    return
}
if err := f.SaveAs("macros.xlsm"); err != nil {
    fmt.Println(err)
    return
}
```

## Fecha de Excel a la hora {#ExcelDateToTime}

```go
func ExcelDateToTime(excelDate float64, use1904Format bool) (time.Time, error)
```

ExcelDateToTime convierte una representación de fecha de Excel basada en flotante en un `time.Time`.

## Transcodificador Charset {#CharsetTranscoder}

```go
func (f *File) CharsetTranscoder(fn charsetTranscoderFn) *File
```

CharsetTranscoder Establece la función de transcodificador de página de códigos definida por el usuario para abrir la hoja de cálculo desde una codificación que no sea UTF-8.
