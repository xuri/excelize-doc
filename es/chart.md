# Gráfico

## Añadir gráfico {#AddChart}

```go
func (f *File) AddChart(sheet, cell string, chart *ChartOptions, combo ...*ChartOptions) error
```

AddChart proporciona el método para agregar un gráfico en una hoja de trabajo por un conjunto de formato de gráfico dado (como desplazamiento, escala, configuración de relación de aspecto y configuración de impresión) y conjunto de propiedades.

A continuación se muestra el `Type` de gráfico compatible con excelize:

ID|Enumeración|Gráfico
---|---|---
0  | Area                        | Gráfico de área 2D
1  | AreaStacked                 | Gráfico de áreas apiladas 2D
2  | AreaPercentStacked          | Gráfico de área 2D 100% apilada
3  | Area3D                      | Gráfico de área 3D
4  | Area3DStacked               | Gráfico de áreas apiladas 3D
5  | Area3DPercentStacked        | Gráfico de área 3D 100% apilada
6  | Bar                         | Gráfico de barras agrupadas 2D
7  | BarStacked                  | Gráfico de barras apiladas 2D
8  | BarPercentStacked           | Gráfico de barras 2D 100% apilado
9  | Bar3DClustered              | Gráfico de barras agrupadas 3D
10 | Bar3DStacked                | Gráfico de barras apiladas 3D
11 | Bar3DPercentStacked         | Gráfico de barras 3D 100% apilado
12 | Bar3DConeClustered          | Gráfico de barras agrupadas con cono 3D
13 | Bar3DConeStacked            | Gráfico de barras apiladas con con cono 3D
14 | Bar3DConePercentStacked     | Gráfico de barras de cono 3D 100%
15 | Bar3DPyramidClustered       | Gráfico de barras agrupadas pirámide 3D
16 | Bar3DPyramidStacked         | Gráfico de barras apiladas pirámide 3D
17 | Bar3DPyramidPercentStacked  | Gráfico de barras apiladas 3D 100% pirámide
18 | Bar3DCylinderClustered      | Gráfico de barras agrupados de cilindros 3D
19 | Bar3DCylinderStacked        | Gráfico de barras apilados de cilindros 3D
20 | Bar3DCylinderPercentStacked | Gráfico de barras apilados 3D 100% cilindro
21 | Col                         | Gráfico de columnas agrupadas 2D
22 | ColStacked                  | Gráfico de columnas apiladas 2D
23 | ColPercentStacked           | Gráfico de columnas apiladas 2D 100%
24 | Col3DClustered              | Gráfico de columnas agrupadas 3D
25 | Col3D                       | Gráfico de columnas 3D
26 | Col3DStacked                | Gráfico de columnas apiladas 3D
27 | Col3DPercentStacked         | Gráfico de columnas apiladas 3D 100%
28 | Col3DCone                   | Gráfico de columnas de cono 3D
29 | Col3DConeClustered          | Gráfico de columnas agrupadas con cono 3D
30 | Col3DConeStacked            | Gráfico de columnas apiladas con cono 3D
31 | Col3DConePercentStacked     | Gráfico de columnas apiladas 3D 100% cono
32 | Col3DPyramid                | Gráfico de columnas piramidales 3D
33 | Col3DPyramidClustered       | Gráfico de columnas agrupadas piramidal 3D
34 | Col3DPyramidStacked         | Gráfico de columnas apiladas pirámide 3D
35 | Col3DPyramidPercentStacked  | Gráfico de columnas apiladas 3D 100% pirámide
36 | Col3DCylinder               | Gráfico de columnas de cilindros 3D
37 | Col3DCylinderClustered      | Gráfico de columnas agrupadas de cilindros 3D
38 | Col3DCylinderStacked        | Gráfico de columnas apiladas de cilindro 3D
39 | Col3DCylinderPercentStacked | Gráfico de columnas apiladas 3D 100% cilindro
40 | Doughnut                    | Gráfico de rosquillas
41 | Line                        | Gráfico de líneas
42 | Line3D                      | Gráfico de líneas 3D
43 | Pie                         | Gráfico circular
44 | Pie3D                       | Gráfico circular 3D
45 | PieOfPie                    | Doble de gráfico circular
46 | BarOfPie                    | Pastel de gráfico circular
47 | Radar                       | Gráfico de radar
48 | Scatter                     | Gráfico de dispersión
49 | Surface3D                   | Gráfico de superficie 3D
50 | WireframeSurface3D          | Gráfico de superficie de estructura alámbrica 3D
51 | Contour                     | Gráfico de contornos
52 | WireframeContour            | Gráfico de contorno de estructura alámbrica
53 | Bubble                      | Gráfico de burbujas
54 | Bubble3D                    | Gráfico de burbujas 3D

En el rango de datos del gráfico de Office Excel, `Series` especifica el conjunto de información para qué datos dibujar, el elemento de leyenda (serie) y la etiqueta del eje horizontal (categoría).

Las opciones de `Series` que se pueden configurar son:

Parámetro|Explicación
---|---
Name|Elemento de leyenda (serie), que se muestra en la barra de fórmulas y la leyenda del gráfico. El parámetro `Name` es opcional. Si no especifica este valor, el valor predeterminado será `Serie 1 .. n`. Soporte de `Name` para la representación de fórmulas, por ejemplo: `Sheet1!$A$1`.
Categories|Etiqueta de eje horizontal (categoría). El parámetro `Categories` es opcional en la mayoría de los tipos de gráficos, el valor predeterminado es una secuencia contigua de la forma `1..n`.
Values|El área de datos del gráfico, que es el parámetro más importante de la `Series`, también es el único parámetro obligatorio al crear un gráfico. Esta opción vincula el gráfico a los datos de la hoja de trabajo que muestra.
Line|Esto establece el formato de línea del gráfico de líneas. La propiedad `Line` es opcional y, si no se proporciona, tendrá el estilo predeterminado. Las opciones que se pueden configurar son `Width`. El rango de `Width` es 0.25pt - 999pt. Si el valor del ancho está fuera del rango, el ancho predeterminado de la línea es 2 puntos.
Marker|Esto establece el marcador del gráfico de líneas y el gráfico de dispersión. El rango del campo opcional `Size` es 2-72 (el valor predeterminado es `5`). El valor de enumeración del campo opcional `Symbol` es (el valor predeterminado es `auto`): `circle`, `dash`, `diamond`, `dot`, `none`, `picture`, `plus`, `square`, `star`, `triangle`, `x`, `auto`.

Establezca las propiedades de la leyenda del gráfico. Las opciones que se pueden configurar son:

Parámetro|Tipo|Explicación
---|---|---
Position        | `string` | La posición de la leyenda del gráfico
ShowLegendKey   | `bool`   | Establecer las claves de leyenda se mostrarán en las etiquetas de datos

Establece la `Position` de la leyenda del gráfico. La posición predeterminada de la leyenda es `right`. Las posiciones disponibles son:

Parámetro|Explicación
---|---
none|Deshabilitar leyenda
top|En la parte superior
bottom|En la parte inferior
left|A la izquierda
right|A la derecha
top_right|Arriba a la derecha

El parámetro `ShowLegendKey`  establece las claves de la leyenda se mostrarán en las etiquetas de datos. El valor predeterminado es `false`.

El título del gráfico se establece seleccionando el parámetro `Name` del objeto `Title`, y el título se mostrará encima del gráfico. El parámetro `Name` admite el uso de representaciones de fórmulas, como `Sheet1!$A$1`, si no especifica un título de icono, el valor predeterminado es nulo.

El parámetro `ShowBlanksAs` proporciona la configuración "Ocultar y vaciar celdas". El valor predeterminado es: `gap`. En la aplicación Excel, la "celda vacía se muestra como": "espacio". Los siguientes son valores opcionales para este parámetro:

Parámetro|Explicación
---|---
gap|espacio
span|Conecte puntos de datos con líneas rectas
zero|valor cero

Especifica que cada marcador de datos de la serie tiene un color diferente por `VaryColors`. El valor predeterminado es `true`.

El parámetro `Format` proporciona ajustes para parámetros como el desplazamiento del gráfico, la escala, la configuración de la relación de aspecto y las propiedades de impresión, así como los que se utilizan en la función [`AddPicture`](image.md#AddPicture).

Establezca la posición del área de trazado del gráfico por área de trazado. Las propiedades que se pueden configurar son:

Parámetro|Tipo|Defecto|Explicación
---|---|---|---
ShowBubbleSize  | `bool` | `false` | Especifica que el tamaño de la burbuja se mostrará en una etiqueta de datos.
ShowCatName     | `bool` | `false` | Nombre de la categoría.
ShowLeaderLines | `bool` | `false` | Especifica que el nombre de la categoría se mostrará en la etiqueta de datos.
ShowPercent     | `bool` | `false` | Especifica que el porcentaje se mostrará en una etiqueta de datos.
ShowSerName     | `bool` | `false` | Especifica que el nombre de la serie se mostrará en una etiqueta de datos.
ShowVal         | `bool` | `false` | Especifica que el valor se mostrará en una etiqueta de datos.

Establezca las opciones principales de eje horizontal y vertical por `XAxis` y `YAxis`.

Las propiedades de `XAxis` que se pueden configurar son:

Parámetro|Tipo|Defecto|Explicación
---|---|---|---
None           | `bool`          | `false` | Deshabilitar ejes.
MajorGridLines | `bool`          | `false` | Especifica las principales líneas de cuadrícula.
MinorGridLines | `bool`          | `false` | Especifica líneas de cuadrícula menores.
TickLabelSkip  | `int`           | `1`     | Especifica cuántas etiquetas de marca se deben omitir entre una etiqueta dibujada. La propiedad `TickLabelSkip` es opcional. El valor predeterminado es automático.
ReverseOrder   | `bool`          | `false` | Especifica que las categorías o valores en orden inverso (orientación del gráfico). La propiedad `ReverseOrder` es opcional.
Maximum        | `*float64`      | `0`     | Especifica que el máximo fijo, 0 es automático. La propiedad máxima es opcional.
Minimum        | `*float64`      | `0`     | Especifica que el mínimo fijo, 0 es automático. La propiedad mínima es opcional. El valor predeterminado es automático.
Font           | `Font`          | N/A     | Especifica que la fuente del eje horizontal.
NumFmt         | `ChartNumFmt`   | N/A     | Especifica que si está vinculado a la fuente y establece un código de formato de número personalizado para el eje.
Title          | `[]RichTextRun` | N/A     | Especifica que el título del eje horizontal principal y el gráfico de cambio de tamaño.

Las propiedades de `YAxis` que se pueden configurar son:

Parámetro|Tipo|Defecto|Explicación
---|---|---|---
None           | `bool`          | `false` | Deshabilitar ejes.
MajorGridLines | `bool`          | `false` | Especifica las principales líneas de cuadrícula.
MinorGridLines | `bool`          | `false` | Especifica líneas de cuadrícula menores.
MajorUnit      | `float64`       | `0`     | Especifica la distancia entre las marcas principales. Debe contener un número de coma flotante positivo. La propiedad `MajorUnit` es opcional. El valor predeterminado es automático.
ReverseOrder   | `bool`          | `false` | Especifica que las categorías o valores en orden inverso (orientación del gráfico). La propiedad `ReverseOrder` es opcional.
Maximum        | `*float64`      | `0`     | Especifica que el máximo fijo, 0 es automático. La propiedad máxima es opcional.
Minimum        | `*float64`      | `0`     | Especifica que el mínimo fijo, 0 es automático. La propiedad mínima es opcional. El valor predeterminado es automático.
Font           | `Font`          | N/A     | Especifica que la fuente del eje vertical.
LogBase        | `float64`       | N/A     | Especifica el número base de la escala logarítmica del eje vertical.
NumFmt         | `ChartNumFmt`   | N/A     | Especifica que si está vinculado a la fuente y establece un código de formato de número personalizado para el eje.
Title          | `[]RichTextRun` | N/A     | Especifica que el título del eje vertical principal y el gráfico de cambio de tamaño.

Establezca el tamaño del gráfico por la propiedad `Dimension`. La propiedad de dimensión es opcional. Las propiedades que se pueden configurar son:

Parámetro|Tipo|Defecto|Explicación
---|---|---|---
Height | `uint` | 260 | Altura
Width  | `uint` | 480 | Anchura

El parámetro `combo` especifica la creación de un gráfico que combine dos o más tipos de gráficos en un solo gráfico. Por ejemplo, cree un gráfico de líneas y columnas agrupadas con los datos `Sheet1!$E$1:$L$15`:

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    if err := f.SetSheetName("Sheet1", "Hoja1"); err != nil {
        fmt.Println(err)
        return
    }
    for idx, row := range [][]interface{}{
        {nil, "Manzana", "Naranja", "Pera"},
        {"Pequeño", 2, 3, 3},
        {"Normal", 5, 2, 4},
        {"Grande", 6, 7, 8},
    } {
        cell, err := excelize.CoordinatesToCellName(1, idx+1)
        if err != nil {
            fmt.Println(err)
            return
        }
        if err := f.SetSheetRow("Hoja1", cell, &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    enable, disable := true, false
    if err := f.AddChart("Hoja1", "E1", &excelize.Chart{
        Type: excelize.Col,
        Series: []excelize.ChartSeries{
            {
                Name:       "Hoja1!$A$2",
                Categories: "Hoja1!$B$1:$D$1",
                Values:     "Hoja1!$B$2:$D$2",
            },
        },
        Format: excelize.GraphicOptions{
            ScaleX:          1,
            ScaleY:          1,
            OffsetX:         15,
            OffsetY:         10,
            PrintObject:     &enable,
            LockAspectRatio: false,
            Locked:          &disable,
        },
        Title: []excelize.RichTextRun{
            {
                Text: "Columna agrupada - gráfico de líneas",
            },
        },
        Legend: excelize.ChartLegend{
            Position: "left",
        },
        PlotArea: excelize.ChartPlotArea{
            ShowCatName:     false,
            ShowLeaderLines: false,
            ShowPercent:     true,
            ShowSerName:     true,
            ShowVal:         true,
        },
    }, &excelize.Chart{
        Type: excelize.Line,
        Series: []excelize.ChartSeries{
            {
                Name:       "Hoja1!$A$4",
                Categories: "Hoja1!$B$1:$D$1",
                Values:     "Hoja1!$B$4:$D$4",
                Marker: excelize.ChartMarker{
                    Symbol: "none", Size: 10,
                },
            },
        },
        Format: excelize.GraphicOptions{
            ScaleX:          1,
            ScaleY:          1,
            OffsetX:         15,
            OffsetY:         10,
            PrintObject:     &enable,
            LockAspectRatio: false,
            Locked:          &disable,
        },
        Legend: excelize.ChartLegend{
            Position: "right",
        },
        PlotArea: excelize.ChartPlotArea{
            ShowCatName:     false,
            ShowLeaderLines: false,
            ShowPercent:     true,
            ShowSerName:     true,
            ShowVal:         true,
        },
    }); err != nil {
        fmt.Println(err)
        return
    }
    // Guarde la hoja de cálculo por la ruta dada.
    if err := f.SaveAs("Libro1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Añadir hoja de gráficos {#AddChartSheet}

```go
func (f *File) AddChartSheet(sheet string, chart *ChartOptions, combo ...*ChartOptions) error
```

AddChartSheet proporciona el método para crear una hoja de gráfico por un conjunto de formato de gráfico dado (como desplazamiento, escala, configuración de relación de aspecto y configuración de impresión) y el conjunto de propiedades. En Excel, una hoja de gráfico es una hoja de trabajo que solo contiene un gráfico.

## Eliminar gráfico {#DeleteChart}

```go
func (f *File) DeleteChart(sheet, cell string) error
```

DeleteChart proporciona una función para eliminar gráficos en una hoja de cálculo por la hoja de trabajo y el nombre de celda dados.
