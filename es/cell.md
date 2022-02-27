# Celda

RichTextRun mapea directamente la configuración de la ejecución de texto enriquecido.

```go
type RichTextRun struct {
    Font *Font
    Text string
}
```

HyperlinkOpts se puede pasar a [`SetCellHyperlink`](cell.md#SetCellHyperlink) para establecer atributos de hipervínculo opcionales (por ejemplo, texto para mostrar y texto de sugerencia en pantalla).

```go
type HyperlinkOpts struct {
    Display *string
    Tooltip *string
}
```

FormulaOpts se puede pasar a [`SetCellFormula`](cell.md#SetCellFormula) para usar otros tipos de fórmula.

```go
type FormulaOpts struct {
    Type *string // Tipo de fórmula
    Ref  *string // Referencia de fórmula compartida
}
```

## Establecer el valor de la celda {#SetCellValue}

```go
func (f *File) SetCellValue(sheet, axis string, value interface{}) error
```

SetCellValue proporciona una función para establecer el valor de una celda. Las coordenadas especificadas no deben estar en la primera fila de la tabla. A continuación, se muestran los tipos de datos admitidos:

|Tipos de datos admitidos|
|---|
|int|
|int8|
|int16|
|int32|
|int64|
|uint|
|uint8|
|uint16|
|uint32|
|uint64|
|float32|
|float64|
|string|
|[]byte|
|time.Duration|
|time.Time|
|bool|
|nil|

## Establecer valor booleano {#SetCellBool}

```go
func (f *File) SetCellBool(sheet, axis string, value bool) error
```

SetCellBool proporciona una función para establecer el valor de tipo bool de una celda por nombre de hoja de trabajo, coordenadas de celda y valor de celda dados.

## Establecer el valor RAW {#SetCellDefault}

```go
func (f *File) SetCellDefault(sheet, axis, value string) error
```

SetCellDefault proporciona una función para establecer el valor del tipo de cadena de una celda como formato predeterminado sin escapar de la celda.

## Establecer valor entero {#SetCellInt}

```go
func (f *File) SetCellInt(sheet, axis string, value int) error
```

SetCellInt proporciona una función para establecer el valor de tipo int de una celda por nombre de hoja de trabajo, coordenadas de celda y valor de celda dados.

## Establecer el valor de cadena {#SetCellStr}

```go
func (f *File) SetCellStr(sheet, axis, value string) error
```

SetCellStr proporciona una función para establecer el valor del tipo de cadena de una celda. El número total de caracteres que una celda puede contener `32767` caracteres.

## Establecer estilo de celda {#SetCellStyle}

```go
func (f *File) SetCellStyle(sheet, hCell, vCell string, styleID int) error
```

SetCellStyle proporciona una función para agregar atributos de estilo para celdas por nombre de hoja de trabajo, área de coordenadas e ID de estilo dados. Los índices de estilo se pueden obtener con la función [`NewStyle`](style.md#NewStyle). Tenga en cuenta que los bordes de tipo `diagonalDown` y `diagonalUp` deben usar el mismo color en la misma área de coordenadas. SetCellStyle sobrescribirá los estilos existentes para la celda, no agregará ni fusionará el estilo con los estilos existentes.

- Ejemplo 1, cree bordes de celda `D7` en `Sheet1`:

```go
style, err := f.NewStyle(&excelize.Style{
    Border: []excelize.Border{
        {Type: "left", Color: "0000FF", Style: 3},
        {Type: "top", Color: "00FF00", Style: 4},
        {Type: "bottom", Color: "FFFF00", Style: 5},
        {Type: "right", Color: "FF0000", Style: 6},
        {Type: "diagonalDown", Color: "A020F0", Style: 7},
        {Type: "diagonalUp", Color: "A020F0", Style: 8},
    },
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_01.png" alt="Establecer un estilo de borde para una celda"></p>

Los cuatro bordes de la celda `D7` se establecen con diferentes estilos y colores. Esto está relacionado con los parámetros al llamar a la función [`NewStyle`](style.md#NewStyle). Debe establecer diferentes estilos para consultar la documentación de ese capítulo.

- Ejemplo 2, configurando el estilo de degradado para la celda de la hoja de trabajo `D7` llamada `Sheet1`:

```go
style, err := f.NewStyle(&excelize.Style{
    Fill: excelize.Fill{Type: "gradient", Color: []string{"#FFFFFF", "#E0EBF5"}, Shading: 1},
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_02.png" alt="Establecer un estilo de degradado para la celda"></p>

La celda `D7` se establece con el relleno de color del efecto de degradado. El efecto de relleno de degradado está relacionado con el parámetro cuando se llama a la función [`NewStyle`](style.md#NewStyle). Debe establecer diferentes estilos para consultar la documentación de este capítulo.

- Ejemplo 3, establezca un relleno sólido para la celda `D7` llamada `Sheet1`:

```go
style, err := f.NewStyle(&excelize.Style{
    Fill: excelize.Fill{Type: "pattern", Color: []string{"#E0EBF5"}, Pattern: 1},
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_03.png" alt="Establecer un relleno sólido para la celda"></p>

La celda `D7` se establece con un relleno sólido.

- Ejemplo 4, establezca el espaciado de caracteres y el ángulo de rotación para la celda `D7` llamada `Sheet1`:

```go
f.SetCellValue("Sheet1", "D7", "Estilo")
style, err := f.NewStyle(&excelize.Style{
    Alignment: &excelize.Alignment{
        Horizontal:      "center",
        Indent:          1,
        JustifyLastLine: true,
        ReadingOrder:    0,
        RelativeIndent:  1,
        ShrinkToFit:     true,
        TextRotation:    45,
        Vertical:        "",
        WrapText:        true,
    },
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_04.png" alt="Establecer el espacio entre caracteres y el ángulo de rotación"></p>

- En el ejemplo 5, la fecha y la hora en Excel están representadas por números reales, por ejemplo, `2017/7/4 12:00:00 PM` se puede representar con el número `42920.5`. Establezca el formato de hora para la celda de la hoja de trabajo `D7` llamada `Sheet1`:

```go
f.SetCellValue("Sheet1", "D7", 42920.5)
f.SetColWidth("Sheet1", "D", "D", 13)
style, err := f.NewStyle(&excelize.Style{NumFmt: 22})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_05.png" alt="Establecer el formato de hora para la celda"></p>

La celda `D7` se establece en el formato de hora. Tenga en cuenta que cuando el ancho de celda con el formato de hora aplicado es demasiado estrecho para mostrarse por completo, se mostrará como `####`, puede arrastrar y soltar el ancho de la columna o establecer la columna en el tamaño apropiado llamando al Función `SetColWidth` para que sea una visualización normal.

- Ejemplo 6, configuración de la fuente, tamaño de fuente, color y estilo sesgado para la celda de la hoja de trabajo `D7` denominada `Sheet1`:

```go
f.SetCellValue("Sheet1", "D7", "Excel")
style, err := f.NewStyle(&excelize.Style{
    Font: &excelize.Font{
        Bold:   true,
        Italic: true,
        Family: "Times New Roman",
        Size:   36,
        Color:  "#777777",
    },
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_06.png" alt="Establecer fuente, tamaño de fuente, color y estilo sesgado para celdas"></p>

- Ejemplo 7, bloquear y ocultar la celda de la hoja de trabajo `D7` denominada `Sheet1`:

```go
style, err := f.NewStyle(&excelize.Style{
    Protection: &excelize.Protection{
        Hidden: true,
        Locked: true,
    },
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

Para bloquear una celda u ocultar una fórmula, proteja la hoja de trabajo. En la pestaña "Revisar", haga clic en "Proteger hoja de trabajo".

## Establecer hipervínculo {#SetCellHyperLink}

```go
func (f *File) SetCellHyperLink(sheet, axis, link, linkType string) error
```

SetCellHyperLink proporciona una función para establecer hipervínculos de celda según el nombre de la hoja de trabajo y la dirección URL del enlace. LinkType define dos tipos de hipervínculos `External` para el sitio web o `Location` para moverse a una de las celdas de este libro. El límite máximo de hipervínculos en una hoja de trabajo es `65530`. A continuación se muestra un ejemplo de un enlace externo.

- Ejemplo 1, agregando un enlace externo a la celda `A3` de la hoja de trabajo llamada `Sheet1`:

```go
if err := f.SetCellHyperLink("Sheet1", "A3",
    "https://github.com/xuri/excelize", "External"); err != nil {
    fmt.Println(err)
}
// Establecer la fuente y el estilo de subrayado para la celda
style, err := f.NewStyle(&excelize.Style{
    Font: &excelize.Font{Color: "#1265BE", Underline: "single"},
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "A3", "A3", style)
```

- Ejemplo 2, agregando un enlace de ubicación interna a la celda `A3` llamada `Sheet1`:

```go
err := f.SetCellHyperLink("Sheet1", "A3", "Sheet1!A40", "Location")
```

## Establecer texto enriquecido de celda {#SetCellRichText}

```go
func (f *File) SetCellRichText(sheet, cell string, runs []RichTextRun) error
```

SetCellRichText proporciona una función para configurar una celda con texto enriquecido por una hoja de trabajo determinada.

Por ejemplo, establezca texto enriquecido en la celda `A1` de la hoja de trabajo denominada `Sheet1`:

<p align="center"><img width="612" src="./images/rich_text.png" alt="Establecer texto enriquecido de celda"></p>

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    if err := f.SetRowHeight("Sheet1", 1, 35); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SetColWidth("Sheet1", "A", "A", 44); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SetCellRichText("Sheet1", "A1", []excelize.RichTextRun{
        {
            Text: "bold",
            Font: &excelize.Font{
                Bold:   true,
                Color:  "2354e8",
                Family: "Times New Roman",
            },
        },
        {
            Text: " and ",
            Font: &excelize.Font{
                Family: "Times New Roman",
            },
        },
        {
            Text: "italic",
            Font: &excelize.Font{
                Bold:   true,
                Color:  "e83723",
                Italic: true,
                Family: "Times New Roman",
            },
        },
        {
            Text: "text with color and font-family,",
            Font: &excelize.Font{
                Bold:   true,
                Color:  "2354e8",
                Family: "Times New Roman",
            },
        },
        {
            Text: "\r\nlarge text with ",
            Font: &excelize.Font{
                Size:  14,
                Color: "ad23e8",
            },
        },
        {
            Text: "strike",
            Font: &excelize.Font{
                Color:  "e89923",
                Strike: true,
            },
        },
        {
            Text: " and ",
            Font: &excelize.Font{
                Size:  14,
                Color: "ad23e8",
            },
        },
        {
            Text: "underline.",
            Font: &excelize.Font{
                Color:     "23e833",
                Underline: "single",
            },
        },
    }); err != nil {
        fmt.Println(err)
        return
    }
    style, err := f.NewStyle(&excelize.Style{
        Alignment: &excelize.Alignment{
            WrapText: true,
        },
    })
    if err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SetCellStyle("Sheet1", "A1", "A1", style); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Obtener texto enriquecido de celda {#GetCellRichText}

```go
func (f *File) GetCellRichText(sheet, cell string) (runs []RichTextRun, err error)
```

GetCellRichText proporciona una función para obtener el texto enriquecido de las celdas mediante una hoja de trabajo determinada.

## Obtener valor de celda {#GetCellValue}

```go
func (f *File) GetCellValue(sheet, axis string, opts ...Options) (string, error)
```

El valor de la celda se recupera de acuerdo con la hoja de trabajo y las coordenadas de la celda dadas, y el valor de retorno se convierte al tipo `string`. Si el formato de celda se puede aplicar al valor de una celda, se devolverá el valor aplicado; de lo contrario, se devolverá el valor original. Los valores de todas las celdas serán los mismos en un rango combinado.

## Obtener el tipo de datos de la celda {#GetCellType}

```go
func (f *File) GetCellType(sheet, axis string) (CellType, error)
```

GetCellType proporciona una función para obtener el tipo de datos de la celda por el nombre y el eje de la hoja de trabajo dados en el archivo de la hoja de cálculo.

## Obtener todo el valor de celda por columnas {#GetCols}

```go
func (f *File) GetCols(sheet string, opts ...Options) ([][]string, error)
```

Obtiene el valor de todas las celdas por columnas en la hoja de trabajo en función del nombre de la hoja de trabajo dada (distingue entre mayúsculas y minúsculas), devuelto como una matriz bidimensional, donde el valor de la celda se convierte al tipo `string`. Si el formato de celda se puede aplicar al valor de la celda, se usará el valor aplicado; de lo contrario, se usará el valor original.

Por ejemplo, obtenga y recorra el valor de todas las celdas por columnas en una hoja de trabajo llamada `Sheet1`:

```go
cols, err := f.GetCols("Sheet1")
if err != nil {
    fmt.Println(err)
    return
}
for _, col := range cols {
    for _, rowCell := range col {
        fmt.Print(rowCell, "\t")
    }
    fmt.Println()
}
```

## Obtener todo el valor de celda por filas {#GetRows}

```go
func (f *File) GetRows(sheet string, opts ...Options) ([][]string, error)
```

Obtiene el valor de todas las celdas por filas en la hoja de trabajo en función del nombre de la hoja de trabajo dada (distingue entre mayúsculas y minúsculas), devuelto como una matriz bidimensional, donde el valor de la celda se convierte al tipo `string`. Si el formato de celda se puede aplicar al valor de la celda, se usará el valor aplicado; de lo contrario, se usará el valor original. GetRows obtuvo las filas con celdas de fórmula o valor, la cola de celda continuamente vacía se omitirá.

Por ejemplo, obtenga y recorra el valor de todas las celdas por filas en una hoja de trabajo llamada `Sheet1`:

```go
rows, err := f.GetRows("Sheet1")
if err != nil {
    fmt.Println(err)
    return
}
for _, row := range rows {
    for _, colCell := range row {
        fmt.Print(colCell, "\t")
    }
    fmt.Println()
}
if err = rows.Close(); err != nil {
    fmt.Println(err)
}
```

## Obtener hipervínculo {#GetCellHyperLink}

```go
func (f *File) GetCellHyperLink(sheet, axis string) (bool, string, error)
```

Obtiene un hipervínculo de celda según el nombre de la hoja de trabajo (distingue entre mayúsculas y minúsculas) y las coordenadas de la celda. Si la celda tiene un hipervínculo, devolverá `true` y la dirección del enlace; de lo contrario, devolverá `false` y una dirección de enlace vacía.

Por ejemplo, obtenga un hipervínculo a una celda `H6` en una hoja de trabajo llamada `Sheet1`:

```go
link, target, err := f.GetCellHyperLink("Sheet1", "H6")
```

## Obtener índice de estilo {#GetCellStyle}

```go
func (f *File) GetCellStyle(sheet, axis string) (int, error)
```

El índice de estilo de celda se obtiene a partir del nombre de la hoja de trabajo (distingue entre mayúsculas y minúsculas) y las coordenadas de la celda, y el índice obtenido se puede utilizar como parámetro para llamar a la función `SetCellValue` al copiar el estilo de celda.

## Combinar celdas {#MergeCell}

```go
func (f *File) MergeCell(sheet, hCell, vCell string) error
```

Fusionar celdas según el nombre de la hoja de trabajo (distingue entre mayúsculas y minúsculas) y las regiones de coordenadas de celda. La combinación de celdas solo conserva el valor de la celda superior izquierda y descarta los demás valores. Por ejemplo, combine celdas en el área `D3:E9` en una hoja de trabajo llamada `Sheet1`:

```go
err := f.MergeCell("Sheet1", "D3", "E9")
```

Si el área de coordenadas de celda dada se superpone con otras celdas fusionadas existentes, las celdas fusionadas existentes se eliminarán.

## Unmerge celdas {#UnmergeCell}

```go
func (f *File) UnmergeCell(sheet string, hCell, vCell string) error
```

UnmergeCell proporciona una función para separar un área de coordenadas determinada. Por ejemplo, separe el área `D3:E9` en `Sheet1`:

```go
err := f.UnmergeCell("Sheet1", "D3", "E9")
```

Atención: las áreas superpuestas tampoco se fusionarán.

## Obtener celdas de combinación {#GetMergeCells}

GetMergeCells proporciona una función para obtener todas las celdas combinadas de una hoja de trabajo actualmente.

```go
func (f *File) GetMergeCells(sheet string) ([]MergeCell, error)
```

### Obtener valor de celda combinada

```go
func (m *MergeCell) GetCellValue() string
```

GetCellValue devuelve el valor de la celda combinada.

### Obtenga las coordenadas de la celda superior izquierda del rango combinado

```go
func (m *MergeCell) GetStartAxis() string
```

GetStartAxis devuelve las coordenadas de la celda superior izquierda del rango combinado, por ejemplo: `C2`.

### Obtenga las coordenadas de la celda inferior derecha del rango combinado

```go
func (m *MergeCell) GetEndAxis() string
```

GetEndAxis devuelve las coordenadas de la celda inferior derecha del rango combinado, por ejemplo: `D4`.

## Añadir comentario {#AddComment}

```go
func (f *File) AddComment(sheet, cell, format string) error
```

AddComment proporciona el método para agregar comentarios en una hoja por índice de hoja de trabajo, celda y conjunto de formato dado (como autor y texto). Tenga en cuenta que la longitud máxima del autor es 255 y la longitud máxima del texto es 32512. Por ejemplo, agregue un comentario en `Sheet1!$A$3`:

<p align="center"><img width="612" src="./images/comment.png" alt="Agregar un comentario a un documento de Excel"></p>

```go
err := f.AddComment("Sheet1", "A3", `{"author":"Excelize: ","text":"Este es un comentario."}`)
```

## Obtener comentarios {#GetComments}

```go
func (f *File) GetComments() (comments map[string][]Comment)
```

GetComments recupera todos los comentarios y devuelve un mapa del nombre de la hoja de trabajo a los comentarios de la hoja de trabajo.

## Establecer fórmula de celda {#SetCellFormula}

```go
func (f *File) SetCellFormula(sheet, axis, formula string, opts ...FormulaOpts) error
```

La fórmula de la celda se toma de acuerdo con el nombre de la hoja de trabajo (distingue entre mayúsculas y minúsculas) y la configuración de la fórmula de la celda. El resultado de la celda de fórmula se puede calcular cuando la aplicación de Office Excel abre la hoja de cálculo o puede usar la función [CalcCellValue](cell.md#CalcCellValue) también puede obtener el valor de celda calculado. Si la aplicación de Excel no calcula la fórmula automáticamente cuando se abre el libro, llame a [UpdateLinkedValue](utils.md#UpdateLinkedValue) después de configurar las funciones de la fórmula de la celda.

- Ejemplo 1, establezca la fórmula normal `=SUM(A1,B1)` para la celda `A3` en `Sheet1`:

```go
err := f.SetCellFormula("Sheet1", "A3", "=SUM(A1,B1)")
```

- Ejemplo 2, establezca la fórmula de matriz constante vertical unidimensional (matriz de fila) `1,2,3` para la celda `A3` en `Sheet1`:

```go
err := f.SetCellFormula("Sheet1", "A3", "={1,2,3}")
```

- Ejemplo 3, establezca la fórmula de matriz constante horizontal unidimensional (matriz de columnas) `"a","b","c"` para la celda `A3` en `Sheet1`:

```go
err := f.SetCellFormula("Sheet1", "A3", "={\"a\",\"b\",\"c\"}")
```

- Ejemplo 4, establezca la fórmula de matriz constante bidimensional `{1,2,"a","b"}` para la celda `A3` en `Sheet1`:

```go
formulaType, ref := excelize.STCellFormulaTypeArray, "A3:A3"
err := f.SetCellFormula("Sheet1", "A3", "={1,2,\"a\",\"b\"}",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- Ejemplo 5, establezca la fórmula de matriz de rango `A1:A2` para la celda `A3` en `Sheet1`:

```go
formulaType, ref := excelize.STCellFormulaTypeArray, "A3:A3"
err := f.SetCellFormula("Sheet1", "A3", "=A1:A2",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- Ejemplo 6, establezca la fórmula compartida `=A1+B1` para las celdas `C1:C5` en `Sheet1`, `C1` es la celda maestra:

```go
formulaType, ref := excelize.STCellFormulaTypeShared, "C1:C5"
err := f.SetCellFormula("Sheet1", "C1", "=A1+B1",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- Ejemplo 7, establecer la fórmula de tabla `=SUM(Table1[[A]:[B]])` para la celda `C2` en `Sheet1`:

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    for idx, row := range [][]interface{}{{"A", "B", "C"}, {1, 2}} {
        if err := f.SetSheetRow("Sheet1", fmt.Sprintf("A%d", idx+1), &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    if err := f.AddTable("Sheet1", "A1", "C2",
        `{"table_name":"Table1","table_style":"TableStyleMedium2"}`); err != nil {
        fmt.Println(err)
        return
    }
    formulaType := excelize.STCellFormulaTypeDataTable
    if err := f.SetCellFormula("Sheet1", "C2", "=SUM(Table1[[A]:[B]])",
        excelize.FormulaOpts{Type: &formulaType}); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Obtener fórmula celular {#GetCellFormula}

```go
func (f *File) GetCellFormula(sheet, axis string) (string, error)
```

Obtenga la fórmula en la celda según el nombre de la hoja de trabajo (distingue entre mayúsculas y minúsculas) y las coordenadas de la celda.

## Calcular el valor de la celda {#CalcCellValue}

```go
func (f *File) CalcCellValue(sheet, cell string) (result string, err error)
```

CalcCellValue proporciona una función para obtener el valor de celda calculado. Esta característica está actualmente en proceso de trabajo. La fórmula de matriz, la fórmula de tabla y algunas otras fórmulas no son compatibles actualmente.

Fórmulas compatibles:

```text
ABS
ACCRINT
ACCRINTM
ACOS
ACOSH
ACOT
ACOTH
ADDRESS
AMORDEGRC
AMORLINC
AND
ARABIC
ASIN
ASINH
ATAN
ATAN2
ATANH
AVEDEV
AVERAGE
AVERAGEA
AVERAGEIF
BASE
BESSELI
BESSELJ
BESSELK
BESSELY
BIN2DEC
BIN2HEX
BIN2OCT
BITAND
BITLSHIFT
BITOR
BITRSHIFT
BITXOR
CEILING
CEILING.MATH
CEILING.PRECISE
CHAR
CHIDIST
CHOOSE
CLEAN
CODE
COLUMN
COLUMNS
COMBIN
COMBINA
COMPLEX
CONCAT
CONCATENATE
CONFIDENCE
CONFIDENCE.NORM
COS
COSH
COT
COTH
COUNT
COUNTA
COUNTBLANK
COUNTIF
COUNTIFS
COUPDAYBS
COUPDAYS
COUPDAYSNC
COUPNCD
COUPNUM
COUPPCD
CSC
CSCH
CUMIPMT
CUMPRINC
DATE
DATEDIF
DATEVALUE
DAY
DAYS
DB
DDB
DEC2BIN
DEC2HEX
DEC2OCT
DECIMAL
DEGREES
DELTA
DEVSQ
DISC
DOLLARDE
DOLLARFR
DURATION
EFFECT
ENCODEURL
ERF
ERF.PRECISE
ERFC
ERFC.PRECISE
ERROR.TYPE
EVEN
EXACT
EXP
FACT
FACTDOUBLE
FALSE
FIND
FINDB
FISHER
FISHERINV
FIXED
FLOOR
FLOOR.MATH
FLOOR.PRECISE
FV
FVSCHEDULE
GAMMA
GAMMALN
GCD
GEOMEAN
GESTEP
HARMEAN
HEX2BIN
HEX2DEC
HEX2OCT
HLOOKUP
HOUR
IF
IFERROR
IFNA
IFS
IMABS
IMAGINARY
IMARGUMENT
IMCONJUGATE
IMCOS
IMCOSH
IMCOT
IMCSC
IMCSCH
IMDIV
IMEXP
IMLN
IMLOG10
IMLOG2
IMPOWER
IMPRODUCT
IMREAL
IMSEC
IMSECH
IMSIN
IMSINH
IMSQRT
IMSUB
IMSUM
IMTAN
INDEX
INT
INTRATE
IPMT
IRR
ISBLANK
ISERR
ISERROR
ISEVEN
ISFORMULA
ISLOGICAL
ISNA
ISNONTEXT
ISNUMBER
ISODD
ISREF
ISTEXT
ISO.CEILING
ISOWEEKNUM
ISPMT
KURT
LARGE
LCM
LEFT
LEFTB
LEN
LENB
LN
LOG
LOG10
LOOKUP
LOWER
MATCH
MAX
MAXA
MAXIFS
MDETERM
MDURATION
MEDIAN
MID
MIDB
MIN
MINA
MINIFS
MINUTE
MIRR
MOD
MONTH
MROUND
MULTINOMIAL
MUNIT
N
NA
NOMINAL
NORM.DIST
NORMDIST
NORM.INV
NORMINV
NORM.S.DIST
NORMSDIST
NORM.S.INV
NORMSINV
NOT
NOW
NPER
NPV
OCT2BIN
OCT2DEC
OCT2HEX
ODD
ODDFPRICE
OR
PDURATION
PERCENTILE.EXC
PERCENTILE.INC
PERCENTILE
PERCENTRANK.EXC
PERCENTRANK.INC
PERCENTRANK
PERMUT
PERMUTATIONA
PI
PMT
POISSON.DIST
POISSON
POWER
PPMT
PRICE
PRICEDISC
PRICEMAT
PRODUCT
PROPER
PV
QUARTILE
QUARTILE.EXC
QUARTILE.INC
QUOTIENT
RADIANS
RAND
RANDBETWEEN
RANK
RANK.EQ
RATE
RECEIVED
REPLACE
REPLACEB
REPT
RIGHT
RIGHTB
ROMAN
ROUND
ROUNDDOWN
ROUNDUP
ROW
ROWS
RRI
SEC
SECH
SECOND
SHEET
SHEETS
SIGN
SIN
SINH
SKEW
SLN
SMALL
SQRT
SQRTPI
STANDARDIZE
STDEV
STDEV.P
STDEV.S
STDEVA
STDEVP
SUBSTITUTE
SUM
SUMIF
SUMSQ
SWITCH
SYD
T
TAN
TANH
TBILLEQ
TBILLPRICE
TBILLYIELD
TEXTJOIN
TIME
TIMEVALUE
TODAY
TRANSPOSE
TRIM
TRIMMEAN
TRUE
TRUNC
UNICHAR
UNICODE
UPPER
VALUE
VAR
VAR.P
VAR.S
VARA
VARP
VARPA
VDB
VLOOKUP
WEEKDAY
WEIBULL
WEIBULL.DIST
XIRR
XLOOKUP
XNPV
XOR
YEAR
YEARFRAC
YIELD
YIELDDISC
YIELDMAT
Z.TEST
ZTEST
```
