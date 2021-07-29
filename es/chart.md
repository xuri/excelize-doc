# Gráfico

## Añadir gráfico {#AddChart}

```go
func (f *File) AddChart(sheet, cell, format string, combo ...string) error
```

AddChart proporciona el método para agregar un gráfico en una hoja de trabajo por un conjunto de formato de gráfico dado (como desplazamiento, escala, configuración de relación de aspecto y configuración de impresión) y conjunto de propiedades.

A continuación se muestra el `type` de gráfico compatible con excelize:

Tipo|Gráfico
---|---
area                        | Gráfico de área 2D
areaStacked                 | Gráfico de áreas apiladas 2D
areaPercentStacked          | Gráfico de área 2D 100% apilada
area3D                      | Gráfico de área 3D
area3DStacked               | Gráfico de áreas apiladas 3D
area3DPercentStacked        | Gráfico de área 3D 100% apilada
bar                         | Gráfico de barras agrupadas 2D
barStacked                  | Gráfico de barras apiladas 2D
barPercentStacked           | Gráfico de barras 2D 100% apilado
bar3DClustered              | Gráfico de barras agrupadas 3D
bar3DStacked                | Gráfico de barras apiladas 3D
bar3DPercentStacked         | Gráfico de barras 3D 100% apilado
bar3DConeClustered          | Gráfico de barras agrupadas con cono 3D
bar3DConeStacked            | Gráfico de barras apiladas con con cono 3D
bar3DConePercentStacked     | Gráfico de barras de cono 3D 100%
bar3DPyramidClustered       | Gráfico de barras agrupadas pirámide 3D
bar3DPyramidStacked         | Gráfico de barras apiladas pirámide 3D
bar3DPyramidPercentStacked  | Gráfico de barras apiladas 3D 100% pirámide
bar3DCylinderClustered      | Gráfico de barras agrupados de cilindros 3D
bar3DCylinderStacked        | Gráfico de barras apilados de cilindros 3D
bar3DCylinderPercentStacked | Gráfico de barras apilados 3D 100% cilindro
col                         | Gráfico de columnas agrupadas 2D
colStacked                  | Gráfico de columnas apiladas 2D
colPercentStacked           | Gráfico de columnas apiladas 2D 100%
col3DClustered              | Gráfico de columnas agrupadas 3D
col3D                       | Gráfico de columnas 3D
col3DStacked                | Gráfico de columnas apiladas 3D
col3DPercentStacked         | Gráfico de columnas apiladas 3D 100%
col3DCone                   | Gráfico de columnas de cono 3D
col3DConeClustered          | Gráfico de columnas agrupadas con cono 3D
col3DConeStacked            | Gráfico de columnas apiladas con cono 3D
col3DConePercentStacked     | Gráfico de columnas apiladas 3D 100% cono
col3DPyramid                | Gráfico de columnas piramidales 3D
col3DPyramidClustered       | Gráfico de columnas agrupadas piramidal 3D
col3DPyramidStacked         | Gráfico de columnas apiladas pirámide 3D
col3DPyramidPercentStacked  | Gráfico de columnas apiladas 3D 100% pirámide
col3DCylinder               | Gráfico de columnas de cilindros 3D
col3DCylinderClustered      | Gráfico de columnas agrupadas de cilindros 3D
col3DCylinderStacked        | Gráfico de columnas apiladas de cilindro 3D
col3DCylinderPercentStacked | Gráfico de columnas apiladas 3D 100% cilindro
doughnut                    | Gráfico de rosquillas
line                        | Gráfico de líneas
pie                         | Gráfico circular
pie3D                       | Gráfico circular 3D
radar                       | Gráfico de radar
scatter                     | Gráfico de dispersión
surface3D                   | Gráfico de superficie 3D
wireframeSurface3D          | Gráfico de superficie de estructura alámbrica 3D
contour                     | Gráfico de contornos
wireframeContour            | Gráfico de contorno de estructura alámbrica
bubble                      | Gráfico de burbujas
bubble3D                    | Gráfico de burbujas 3D

En el rango de datos del gráfico de Office Excel, `series` especifica el conjunto de información para qué datos dibujar, el elemento de leyenda (serie) y la etiqueta del eje horizontal (categoría).

Las opciones de `series` que se pueden configurar son:

Parámetro|Explicación
---|---
name|Elemento de leyenda (serie), que se muestra en la barra de fórmulas y la leyenda del gráfico. El parámetro `name` es opcional. Si no especifica este valor, el valor predeterminado será `Serie 1 .. n`. Soporte de `name` para la representación de fórmulas, por ejemplo: `Sheet1!$A$1`.
categories|Etiqueta de eje horizontal (categoría). El parámetro `categorías` es opcional en la mayoría de los tipos de gráficos, el valor predeterminado es una secuencia contigua de la forma `1..n`.
values|El área de datos del gráfico, que es el parámetro más importante de la `series`, también es el único parámetro obligatorio al crear un gráfico. Esta opción vincula el gráfico a los datos de la hoja de trabajo que muestra.
line|Esto establece el formato de línea del gráfico de líneas. La propiedad `line` es opcional y, si no se proporciona, tendrá el estilo predeterminado. Las opciones que se pueden configurar son `width`. El rango de `width` es 0.25pt - 999pt. Si el valor del ancho está fuera del rango, el ancho predeterminado de la línea es 2 puntos.
marker|Esto establece el marcador del gráfico de líneas y el gráfico de dispersión. El rango del campo opcional `size` es 2-72 (el valor predeterminado es `5`). El valor de enumeración del campo opcional `symbol` es (el valor predeterminado es `auto`): `circle`, `dash`, `diamond`, `dot`, `none`, `picture`, `plus`, `square`, `star`, `triangle`, `x`, `auto`.

Establezca las propiedades de la leyenda del gráfico. Las opciones que se pueden configurar son:

Parámetro|Tipo|Explicación
---|---|---
none|bool|Especifique si muestra la leyenda sin superponer el gráfico. El valor predeterminado es `false`
position|string|La posición de la leyenda del gráfico
show_legend_key|bool|Establecer las claves de leyenda se mostrarán en las etiquetas de datos

Establece la `position` de la leyenda del gráfico. La posición predeterminada de la leyenda es `right`. Este parámetro solo tiene efecto cuando `none` es `false`. Las posiciones disponibles son:

Parámetro|Explicación
---|---
top|En la parte superior
bottom|En la parte inferior
left|A la izquierda
right|A la derecha
top_right|Arriba a la derecha

El parámetro `show_legend_key` establece las claves de la leyenda se mostrarán en las etiquetas de datos. El valor predeterminado es `false`.

El título del gráfico se establece seleccionando el parámetro `name` del objeto `title`, y el título se mostrará encima del gráfico. El parámetro `name` admite el uso de representaciones de fórmulas, como `Sheet1!$A$1`, si no especifica un título de icono, el valor predeterminado es nulo.

El parámetro `show_blanks_as` proporciona la configuración "Ocultar y vaciar celdas". El valor predeterminado es: `gap`. En la aplicación Excel, la "celda vacía se muestra como": "espacio". Los siguientes son valores opcionales para este parámetro:

Parámetro|Explicación
---|---
gap|espacio
span|Conecte puntos de datos con líneas rectas
zero|valor cero

Especifica que cada marcador de datos de la serie tiene un color diferente por `vary_colors`. El valor predeterminado es `true`.

El parámetro `formato` proporciona ajustes para parámetros como el desplazamiento del gráfico, la escala, la configuración de la relación de aspecto y las propiedades de impresión, así como los que se utilizan en la función [`AddPicture()`](image.md#AddPicture).

Establezca la posición del área de trazado del gráfico por área de trazado. Las propiedades que se pueden configurar son:

Parámetro|Tipo|Defecto|Explicación
---|---|---|---
show_bubble_size|bool|`false`|Especifica que el tamaño de la burbuja se mostrará en una etiqueta de datos.
show_cat_name|bool|`true`|Nombre de la categoría.
show_leader_lines|bool|`false`|Especifica que el nombre de la categoría se mostrará en la etiqueta de datos.
show_percent|bool|`false`|Especifica que el porcentaje se mostrará en una etiqueta de datos.
show_series_name|bool|`false`|Especifica que el nombre de la serie se mostrará en una etiqueta de datos.
show_val|bool|`false`|Especifica que el valor se mostrará en una etiqueta de datos.

Establezca las opciones principales de eje horizontal y vertical por `x_axis` y `y_axis`.

Las propiedades de `x_axis` que se pueden configurar son:

Parámetro|Tipo|Defecto|Explicación
---|---|---|---
none|bool|`false`|Deshabilitar ejes.
major_grid_lines|bool|`false`|Especifica las principales líneas de cuadrícula.
minor_grid_lines|bool|`false`|Especifica líneas de cuadrícula menores.
tick_label_skip|int|`1`|Especifica cuántas etiquetas de marca se deben omitir entre una etiqueta dibujada. La propiedad `tick_label_skip` es opcional. El valor predeterminado es automático.
reverse_order|bool|`false`|Especifica que las categorías o valores en orden inverso (orientación del gráfico). La propiedad `reverse_order` es opcional.
maximum|int|`0`|Especifica que el máximo fijo, 0 es automático. La propiedad máxima es opcional.
minimum|int|`0`|Especifica que el mínimo fijo, 0 es automático. La propiedad mínima es opcional. El valor predeterminado es automático.

Las propiedades de `y_axis` que se pueden configurar son:

Parámetro|Tipo|Defecto|Explicación
---|---|---|---
none|bool|`false`|Deshabilitar ejes.
major_grid_lines|bool|`false`|Especifica las principales líneas de cuadrícula.
minor_grid_lines|bool|`false`|Especifica líneas de cuadrícula menores.
major_unit|float64|`0`|Especifica la distancia entre las marcas principales. Debe contener un número de coma flotante positivo. La propiedad `major_unit` es opcional. El valor predeterminado es automático.
reverse_order|bool|`false`|Especifica que las categorías o valores en orden inverso (orientación del gráfico). La propiedad `reverse_order` es opcional.
maximum|int|`0`|Especifica que el máximo fijo, 0 es automático. La propiedad máxima es opcional.
minimum|int|`0`|Especifica que el mínimo fijo, 0 es automático. La propiedad mínima es opcional. El valor predeterminado es automático.

Establezca el tamaño del gráfico por la propiedad `dimension`. La propiedad de dimensión es opcional. Las propiedades que se pueden configurar son:

Parámetro|Tipo|Defecto|Explicación
---|---|---|---
height|int|290|Altura
width|int|480|Anchura

El parámetro `combo` especifica la creación de un gráfico que combine dos o más tipos de gráficos en un solo gráfico. Por ejemplo, cree un gráfico de líneas y columnas agrupadas con los datos `Sheet1!$E$1:$L$15`:

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    categories := map[string]string{
        "A2": "Pequeño", "A3": "Normal", "A4": "Grande",
        "B1": "Manzana", "C1": "Naranja", "D1": "Pera"}
    values := map[string]int{
        "B2": 2, "C2": 3, "D2": 3, "B3": 5, "C3": 2, "D3": 4, "B4": 6, "C4": 7, "D4": 8}
    f := excelize.NewFile()
    for k, v := range categories {
        f.SetCellValue("Sheet1", k, v)
    }
    for k, v := range values {
        f.SetCellValue("Sheet1", k, v)
    }
    if err := f.AddChart("Sheet1", "E1", `{
        "type": "col",
        "series": [
        {
            "name": "Sheet1!$A$2",
            "categories": "Sheet1!$B$1:$D$1",
            "values": "Sheet1!$B$2:$D$2"
        },
        {
            "name": "Sheet1!$A$3",
            "categories": "Sheet1!$B$1:$D$1",
            "values": "Sheet1!$B$3:$D$3"
        }],
        "format":
        {
            "x_scale": 1.0,
            "y_scale": 1.0,
            "x_offset": 15,
            "y_offset": 10,
            "print_obj": true,
            "lock_aspect_ratio": false,
            "locked": false
        },
        "legend":
        {
            "position": "left",
            "show_legend_key": false
        },
        "title":
        {
            "name": "Columna agrupada - gráfico de líneas"
        },
        "plotarea":
        {
            "show_bubble_size": true,
            "show_cat_name": false,
            "show_leader_lines": false,
            "show_percent": true,
            "show_series_name": true,
            "show_val": true
        }
    }`, `{
        "type": "line",
        "series": [
        {
            "name": "Sheet1!$A$4",
            "categories": "Sheet1!$B$1:$D$1",
            "values": "Sheet1!$B$4:$D$4"
        }],
        "format":
        {
            "x_scale": 1.0,
            "y_scale": 1.0,
            "x_offset": 15,
            "y_offset": 10,
            "print_obj": true,
            "lock_aspect_ratio": false,
            "locked": false
        },
        "legend":
        {
            "position": "right",
            "show_legend_key": false
        },
        "plotarea":
        {
            "show_bubble_size": true,
            "show_cat_name": false,
            "show_leader_lines": false,
            "show_percent": true,
            "show_series_name": true,
            "show_val": true
        }
    }`); err != nil {
        fmt.Println(err)
        return
    }
    // Guarde la hoja de cálculo por la ruta dada.
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Añadir hoja de gráficos {#AddChartSheet}

```go
func (f *File) AddChartSheet(sheet, format string, combo ...string) error
```

AddChartSheet proporciona el método para crear una hoja de gráfico por un conjunto de formato de gráfico dado (como desplazamiento, escala, configuración de relación de aspecto y configuración de impresión) y el conjunto de propiedades. En Excel, una hoja de gráfico es una hoja de trabajo que solo contiene un gráfico.

## Eliminar gráfico {#DeleteChart}

```go
func (f *File) DeleteChart(sheet, cell string) (err error)
```

DeleteChart proporciona una función para eliminar gráficos en una hoja de cálculo por la hoja de trabajo y el nombre de celda dados.
