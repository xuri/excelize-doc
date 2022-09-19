# Libro

`Options` define las opciones para abrir y leer hojas de cálculo.

```go
type Options struct {
    Password          string
    RawCellValue      bool
    UnzipSizeLimit    int64
    UnzipXMLSizeLimit int64
}
```

`Password` especifica la contraseña de la hoja de cálculo en texto plano.

`RawCellValue` especifica si se aplica el formato de número para el valor de la celda o se obtiene el valor sin procesar.

`UnzipSizeLimit` especifica el límite de tamaño de descompresión en bytes al abrir la hoja de cálculo, este valor debe ser mayor o igual que `UnzipXMLSizeLimit`, el límite de tamaño predeterminado es 16GB.

`UnzipXMLSizeLimit` specifies the memory limit on unzipping worksheet and shared string table in bytes, worksheet XML will be extracted to system temporary directory when the file size is over this value, this value should be less than or equal to `UnzipSizeLimit`, the default value is 16MB.

## Crear una hoja de cálculo {#NewFile}

```go
func NewFile() *File
```

NewFile proporciona una función para crear un nuevo archivo de forma predeterminada. El libro recién creado contendrá de forma predeterminada una hoja de cálculo denominada `Sheet1`. Por ejemplo:

## Abierto {#OpenFile}

```go
func OpenFile(filename string, opts ...Options) (*File, error)
```

OpenFile toma el nombre de un archivo de hoja de cálculo y devuelve una estructura de archivo de hoja de cálculo rellenada para él. Por ejemplo, abra una hoja de cálculo con protección con contraseña:

```go
f, err := excelize.OpenFile("Book1.xlsx", excelize.Options{Password: "password"})
if err != nil {
    return
}
```

Cierre el archivo por [`Close()`](workbook.md#Close) después de abrir la hoja de cálculo.

## Flujo de datos abiertos {#OpenReader}

```go
func OpenReader(r io.Reader, opts ...Options) (*File, error)
```

OpenReader lee el flujo de datos de `io.Reader` y devuelva un archivo de hoja de cálculo rellenado.

Por ejemplo, cree un servidor HTTP para manejar la plantilla de carga y, a continuación, el archivo de descarga de respuesta con la nueva hoja de cálculo agregada:

```go
package main

import (
    "fmt"
    "net/http"

    "github.com/xuri/excelize/v2"
)

func process(w http.ResponseWriter, req *http.Request) {
    file, _, err := req.FormFile("file")
    if err != nil {
        fmt.Fprint(w, err.Error())
        return
    }
    defer file.Close()
    f, err := excelize.OpenReader(file)
    if err != nil {
        fmt.Fprint(w, err.Error())
        return
    }
    f.Path = "Book1.xlsx"
    f.NewSheet("NewSheet")
    w.Header().Set("Content-Disposition", fmt.Sprintf("attachment; filename=%s", f.Path))
    w.Header().Set("Content-Type", req.Header.Get("Content-Type"))
    if err := f.Write(w); err != nil {
        fmt.Fprint(w, err.Error())
    }
}

func main() {
    http.HandleFunc("/process", process)
    http.ListenAndServe(":8090", nil)
}
```

Prueba con cURL:

```bash
curl --location --request GET 'http://127.0.0.1:8090/process' \
--form 'file=@/tmp/template.xltx' -O -J
```

## Salvar {#Save}

```go
func (f *File) Save(opts ...Options) error
```

Save proporciona una función para invalidar el archivo de hoja de cálculo con la ruta de origen.

## Guardar como {#SaveAs}

```go
func (f *File) SaveAs(name string, opts ...Options) error
```

SaveAs proporciona una función para crear o actualizar el archivo de hoja de cálculo en la ruta proporcionada.

## Cerrar libro de trabajo {#Close}

```go
func (f *File) Close() error
```

Close cierra y limpia el archivo temporal abierto para la hoja de cálculo.

## Crear hoja de trabajo {#NewSheet}

```go
func (f *File) NewSheet(sheet string) int
```

NewSheet proporciona la función para crear una nueva hoja por un nombre de hoja de cálculo y devuelve el índice de las hojas en el libro (hoja de cálculo) después de anexar. Tenga en cuenta que al crear un nuevo archivo de hoja de cálculo, se creará la hoja de cálculo predeterminada denominada `Sheet1`.

## Eliminar hoja de trabajo {#DeleteSheet}

```go
func (f *File) DeleteSheet(sheet string)
```

DeleteSheet proporciona una función para eliminar la hoja de trabajo en un libro de trabajo por el nombre de la hoja de trabajo dado, los nombres de las hojas no distinguen entre mayúsculas y minúsculas. Utilice este método con precaución, ya que afectará los cambios en las referencias, como fórmulas, gráficos, etc. Si hay algún valor de referencia de la hoja de cálculo eliminada, se producirá un error de archivo cuando lo abra. Esta función no será válida cuando solo quede una hoja de trabajo.

## Copiar hoja de trabajo {#CopySheet}

```go
func (f *File) CopySheet(from, to int) error
```

CopySheet proporciona una función para duplicar una hoja de cálculo mediante el índice de hoja de cálculo de origen y destino dado. Tenga en cuenta que actualmente no admite libros de trabajo duplicados que contengan tablas, gráficos o imágenes. Por ejemplo:

```go
// Sheet1 ya existe...
index := f.NewSheet("Sheet2")
err := f.CopySheet(1, index)
return err
```

## Hojas de trabajo grupales {#GroupSheets}

```go
func (f *File) GroupSheets(sheets []string) error
```

GroupSheets proporciona una función para agrupar hojas de trabajo por nombres de hojas de trabajo dados. Las hojas de trabajo grupales deben contener una hoja de trabajo activa.

## Desagrupar hojas de trabajo {#UngroupSheets}

```go
func (f *File) UngroupSheets() error
```

UngroupSheets proporciona una función para desagrupar hojas de trabajo.

## Establecer el fondo de la hoja de trabajo {#SetSheetBackground}

```go
func (f *File) SetSheetBackground(sheet, picture string) error
```

SetSheetBackground proporciona una función para establecer una imagen de fondo por el nombre de la hoja de cálculo dado.

## Establecer la hoja de trabajo predeterminada {#SetActiveSheet}

```go
func (f *File) SetActiveSheet(index int)
```

SetActiveSheet proporciona una función para establecer la hoja activa predeterminada del libro por un índice determinado. Tenga en cuenta que el índice activo es diferente del identificador devuelto por la función [`GetSheetMap`](sheet.md#GetSheetMap). Debe ser mayor o igual que 0 y menor que el total de números de hoja de cálculo.

## Obtener índice de hoja activo {#GetActiveSheetIndex}

```go
func (f *File) GetActiveSheetIndex() int
```

GetActiveSheetIndex proporciona una función para obtener una hoja de cálculo activa del libro. Si no se encuentra, la hoja activa devolverá el entero '0'.

## Establecer la hoja de trabajo visible {#SetSheetVisible}

```go
func (f *File) SetSheetVisible(sheet string, visible bool) error
```

SetSheetVisible proporciona una función para establecer la hoja de cálculo visible por el nombre de la hoja de cálculo dado. Un libro de trabajo debe contener al menos una hoja de cálculo visible. Si se ha activado la hoja de cálculo determinada, esta configuración se invalidará. Valores de estado de hoja definidos por [SheetStateValues Enum](https://docs.microsoft.com/es-es/dotnet/api/documentformat.openxml.spreadsheet.sheetstatevalues?view=openxml-2.8.1):

|Valores de estado de hoja|
|---|
|visible|
|hidden|
|veryHidden|

Por ejemplo, ocultar `Sheet1`:

```go
err := f.SetSheetVisible("Sheet1", false)
```

## Obtener la hoja de trabajo visible {#GetSheetVisible}

```go
func (f *File) GetSheetVisible(sheet string) bool
```

GetSheetVisible proporciona una función para que la hoja de cálculo sea visible con el nombre de la hoja de cálculo especificado. Por ejemplo, obtenga el estado visible de `Sheet1`:

```go
f.GetSheetVisible("Sheet1")
```

## Establecer propiedades de formato de hoja de cálculo {#SetSheetFormatPr}

```go
func (f *File) SetSheetFormatPr(sheet string, opts ...SheetFormatPrOptions) error
```

SetSheetFormatPr proporciona una función para establecer las propiedades de formato de hoja de cálculo.

Opciones disponibles:

Parámetro de formato opcional |Tipo
---|---
BaseColWidth | uint8
DefaultColWidth | float64
DefaultRowHeight | float64
CustomHeight | bool
ZeroHeight | bool
ThickTop | bool
ThickBottom | bool

Por ejemplo, haga que las filas de la hoja de cálculo sean predeterminadas como ocultas:

<p align="center"><img width="612" src="./images/sheet_format_pr_01.png" alt="Establecer propiedades de formato de hoja de cálculo"></p>

```go
f := excelize.NewFile()
const sheet = "Sheet1"
if err := f.SetSheetFormatPr("Sheet1", excelize.ZeroHeight(true)); err != nil {
    fmt.Println(err)
}
if err := f.SetRowVisible("Sheet1", 10, true); err != nil {
    fmt.Println(err)
}
f.SaveAs("Book1.xlsx")
```

## Obtener propiedades de formato de hoja de cálculo {#GetSheetFormatPr}

```go
func (f *File) GetSheetFormatPr(sheet string, opts ...SheetFormatPrOptionsPtr) error
```

GetSheetFormatPr proporciona una función para obtener propiedades de formato de hoja de cálculo.

Opciones disponibles:

Parámetro de formato opcional |Tipo
---|---
BaseColWidth | uint8
DefaultColWidth | float64
DefaultRowHeight | float64
CustomHeight | bool
ZeroHeight | bool
ThickTop | bool
ThickBottom | bool

Por ejemplo:

```go
f := excelize.NewFile()
const sheet = "Sheet1"

var (
    baseColWidth     excelize.BaseColWidth
    defaultColWidth  excelize.DefaultColWidth
    defaultRowHeight excelize.DefaultRowHeight
    customHeight     excelize.CustomHeight
    zeroHeight       excelize.ZeroHeight
    thickTop         excelize.ThickTop
    thickBottom      excelize.ThickBottom
)

if err := f.GetSheetFormatPr(sheet,
    &baseColWidth,
    &defaultColWidth,
    &defaultRowHeight,
    &customHeight,
    &zeroHeight,
    &thickTop,
    &thickBottom,
); err != nil {
    fmt.Println(err)
}
fmt.Println("Defaults:")
fmt.Println("- baseColWidth:", baseColWidth)
fmt.Println("- defaultColWidth:", defaultColWidth)
fmt.Println("- defaultRowHeight:", defaultRowHeight)
fmt.Println("- customHeight:", customHeight)
fmt.Println("- zeroHeight:", zeroHeight)
fmt.Println("- thickTop:", thickTop)
fmt.Println("- thickBottom:", thickBottom)
```

Obtener salida:

```text
Defaults:
- baseColWidth: 0
- defaultColWidth: 0
- defaultRowHeight: 15
- customHeight: false
- zeroHeight: false
- thickTop: false
- thickBottom: false
```

## Establecer propiedades de vista de hoja de cálculo {#SetSheetViewOptions}

```go
func (f *File) SetSheetViewOptions(sheet string, viewIndex int, opts ...SheetViewOption) error
```

SetSheetViewOptions establece las opciones de vista de hoja. El `viewIndex` puede ser negativo y si es así se cuenta hacia atrás (`-1` es la última vista).

Opciones disponibles:

Parámetro de formato opcional |Tipo
---|---
DefaultGridColor | bool
ShowFormulas | bool
ShowGridLines | bool
ShowRowColHeaders | bool
ShowZeros | bool
RightToLeft | bool
ShowRuler | bool
View | string
TopLeftCell | string
ZoomScale | float64

- Ejemplo 1:

```go
err = f.SetSheetViewOptions("Sheet1", -1, ShowGridLines(false))
```

- Ejemplo 2:

```go
f := excelize.NewFile()
const sheet = "Sheet1"

if err := f.SetSheetViewOptions(sheet, 0,
    excelize.DefaultGridColor(false),
    excelize.ShowFormulas(true),
    excelize.ShowGridLines(true),
    excelize.ShowRowColHeaders(true),
    excelize.RightToLeft(false),
    excelize.ShowRuler(false),
    excelize.View("pageLayout"),
    excelize.TopLeftCell("C3"),
    excelize.ZoomScale(80),
); err != nil {
    fmt.Println(err)
}

var zoomScale ZoomScale
fmt.Println("Default:")
fmt.Println("- zoomScale: 80")

if err := f.SetSheetViewOptions(sheet, 0, excelize.ZoomScale(500)); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &zoomScale); err != nil {
    fmt.Println(err)
}

fmt.Println("Used out of range value:")
fmt.Println("- zoomScale:", zoomScale)

if err := f.SetSheetViewOptions(sheet, 0, excelize.ZoomScale(123)); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &zoomScale); err != nil {
    fmt.Println(err)
}

fmt.Println("Used correct value:")
fmt.Println("- zoomScale:", zoomScale)
```

Obtener salida:

```text
Default:
- zoomScale: 80
Used out of range value:
- zoomScale: 80
Used correct value:
- zoomScale: 123
```

## Obtener propiedades de vista de hoja de cálculo {#GetSheetViewOptions}

```go
func (f *File) GetSheetViewOptions(sheet string, viewIndex int, opts ...SheetViewOptionPtr) error
```

GetSheetViewOptions obtiene el valor de las opciones de vista de hoja. El `viewIndex` puede ser negativo y si es así se cuenta hacia atrás (`-1` es la última vista).

Opciones disponibles:

Parámetro de formato opcional |Tipo
---|---
DefaultGridColor | bool
ShowFormulas | bool
ShowGridLines | bool
ShowRowColHeaders | bool
ShowZeros | bool
RightToLeft | bool
ShowRuler | bool
View | string
TopLeftCell | string
ZoomScale | float64

- Ejemplo 1, para obtener la configuración de propiedades de la cuadrícula para la última vista en la hoja de cálculo denominada `Sheet1`:

```go
var showGridLines excelize.ShowGridLines
err = f.GetSheetViewOptions("Sheet1", -1, &showGridLines)
```

- Ejemplo 2:

```go
f := NewFile()
const sheet = "Sheet1"

var (
    defaultGridColor  excelize.DefaultGridColor
    showFormulas      excelize.ShowFormulas
    showGridLines     excelize.ShowGridLines
    showRowColHeaders excelize.ShowRowColHeaders
    showZeros         excelize.ShowZeros
    rightToLeft       excelize.RightToLeft
    showRuler         excelize.ShowRuler
    view              excelize.View
    topLeftCell       excelize.TopLeftCell
    zoomScale         excelize.ZoomScale
)

if err := f.GetSheetViewOptions(sheet, 0,
    &defaultGridColor,
    &showFormulas,
    &showGridLines,
    &showRowColHeaders,
    &showZeros,
    &rightToLeft,
    &showRuler,
    &view,
    &topLeftCell,
    &zoomScale,
); err != nil {
    fmt.Println(err)
}

fmt.Println("Default:")
fmt.Println("- defaultGridColor:", defaultGridColor)
fmt.Println("- showFormulas:", showFormulas)
fmt.Println("- showGridLines:", showGridLines)
fmt.Println("- showRowColHeaders:", showRowColHeaders)
fmt.Println("- showZeros:", showZeros)
fmt.Println("- rightToLeft:", rightToLeft)
fmt.Println("- showRuler:", showRuler)
fmt.Println("- view:", view)
fmt.Println("- topLeftCell:", `"`+topLeftCell+`"`)
fmt.Println("- zoomScale:", zoomScale)

if err := f.SetSheetViewOptions(sheet, 0, excelize.ShowGridLines(false)); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &showGridLines); err != nil {
    fmt.Println(err)
}

if err := f.SetSheetViewOptions(sheet, 0, excelize.ShowZeros(false)); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &showZeros); err != nil {
    fmt.Println(err)
}

if err := f.SetSheetViewOptions(sheet, 0, excelize.View("pageLayout")); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &view); err != nil {
    fmt.Println(err)
}

if err := f.SetSheetViewOptions(sheet, 0, excelize.TopLeftCell("B2")); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &topLeftCell); err != nil {
    fmt.Println(err)
}

fmt.Println("After change:")
fmt.Println("- showGridLines:", showGridLines)
fmt.Println("- showZeros:", showZeros)
fmt.Println("- view:", view)
fmt.Println("- topLeftCell:", topLeftCell)
```

Obtener salida:

```text
Default:
- defaultGridColor: true
- showFormulas: false
- showGridLines: true
- showRowColHeaders: true
- showZeros: true
- rightToLeft: false
- showRuler: true
- view: normal
- topLeftCell: ""
- zoomScale: 0
After change:
- showGridLines: false
- showZeros: false
- view: pageLayout
- topLeftCell: B2
```

## Establecer el diseño de la página de la hoja de trabajo {#SetPageLayout}

```go
func (f *File) SetPageLayout(sheet string, opts ...PageLayoutOption) error
```

SetPageLayout proporciona una función para establecer el diseño de página de hoja de cálculo. Opciones disponibles:

- `BlackAndWhite` especificó impresión en blanco y negro.

- `FirstPageNumber` especificó el primer número de página impresa. Si no se especifica ningún valor, se asume "automático".

- `PageLayoutOrientation` proporciona un método para establecer la orientación de la hoja de cálculo, la orientación predeterminada es "retrato". A continuación se muestran los parámetros de orientación admitidos por Excelize index number:

Parámetro|Orientación
---|---
OrientationPortrait|retrato
OrientationLandscape|paisaje

- `PageLayoutPaperSize` proporciona un método para establecer el tamaño del papel de la hoja de trabajo, el tamaño de papel predeterminado de la hoja de trabajo es "Papel carta (8.5 pulgadas por 11 pulgadas)". A continuación se muestra el tamaño del papel ordenado por el número de índice de Excelize:

Indice|Tamaño del papel
---|---
1   | Papel de carta (8.5 in. × 11 in.)
2   | Carta de papel pequeño (8.5 in. × 11 in.)
3   | Papel tabloide (11 in. × 17 in.)
4   | Papel contable (17 in. × 11 in.)
5   | Documento legal (8.5 in. × 14 in.)
6   | Documento de estado de cuenta (5.5 in. × 8.5 in.)
7   | Documento ejecutivo (7.25 in. × 10.5 in.)
8   | Papel A3 (297 mm × 420 mm)
9   | Papel A4 (210 mm × 297 mm)
10  | Papel pequeño A4 (210 mm × 297 mm)
11  | Papel A5 (148 mm × 210 mm)
12  | Papel B4 (250 mm × 353 mm)
13  | Papel B5 (176 mm × 250 mm)
14  | Folio papel (8.5 in. × 13 in.)
15  | Papel de cuarzo (215 mm × 275 mm)
16  | Papel estándar (10 in. × 14 in.)
17  | Papel estándar (11 in. × 17 in.)
18  | Papel de la nota (8.5 in. × 11 in.)
19  | #9 Sobre (3.875 in. × 8.875 in.)
20  | #10 Sobre (4.125 in. × 9.5 in.)
21  | #11 Sobre (4.5 in. × 10.375 in.)
22  | #12 Sobre (4.75 in. × 11 in.)
23  | #14 Sobre (5 in. × 11.5 in.)
24  | C papel (17 in. × 22 in.)
25  | D papel (22 in. × 34 in.)
26  | E papel (34 in. × 44 in.)
27  | DL Sobre (110 mm × 220 mm)
28  | C5 Sobre (162 mm × 229 mm)
29  | C3 Sobre (324 mm × 458 mm)
30  | C4 Sobre (229 mm × 324 mm)
31  | C6 Sobre (114 mm × 162 mm)
32  | C65 Sobre (114 mm × 229 mm)
33  | B4 Sobre (250 mm × 353 mm)
34  | B5 Sobre (176 mm × 250 mm)
35  | B6 Sobre (176 mm × 125 mm)
36  | Italia Sobre (110 mm × 230 mm)
37  | Monarca Sobre (3.875 in. × 7.5 in.).
38  | 6¾ Sobre (3.625 in. × 6.5 in.)
39  | Ventilador estándar de EE. UU. (14.875 in. × 11 in.)
40  | Ventilador estándar alemán (8.5 in. × 12 in.)
41  | Fanfold legal alemán (8.5 in. × 13 in.)
42  | ISO B4 (250 mm × 353 mm)
43  | Postal japonesa (100 mm × 148 mm)
44  | Estándar papel (9 in. × 11 in.)
45  | Estándar papel (10 in. × 11 in.)
46  | Estándar papel (15 in. × 11 in.)
47  | Invite Sobre (220 mm × 220 mm)
50  | Papel extra carta (9.275 in. × 12 in.)
51  | Documento adicional legal (9.275 in. × 15 in.)
52  | Papel extra tabloide (11.69 in. × 18 in.)
53  | A4 papel extra (236 mm × 322 mm)
54  | Papel transversal de carta (8.275 in. × 11 in.)
55  | Papel transversal A4 (210 mm × 297 mm)
56  | Papel transversal adicional carta (9.275 in. × 12 in.)
57  | SuperA/SuperA/Papel A4 (227 mm × 356 mm)
58  | SuperB/SuperB/Papel A3 (305 mm × 487 mm)
59  | Carta más papel (8.5 in. × 12.69 in.)
60  | Papel A4 más (210 mm × 330 mm)
61  | A5 papel transversal (148 mm × 210 mm)
62  | JIS B5 papel transversal (182 mm × 257 mm)
63  | A3 papel extra (322 mm × 445 mm)
64  | A5 papel extra (174 mm × 235 mm)
65  | ISO B5 papel extra (201 mm × 276 mm)
66  | A2 papel (420 mm × 594 mm)
67  | A3 papel transversal (297 mm × 420 mm)
68  | A3 extra papel transversal (322 mm × 445 mm)
69  | Postal Doble Japonesa (200 mm × 148 mm)
70  | A6 (105 mm × 148 mm)
71  | Sobre japonés Kaku #2
72  | Sobre japonés Kaku #3
73  | Sobre japonés Chou #3
74  | Sobre japonés Chou #4
75  | Carta rotada (11 × 8½ in.)
76  | A3 rotada (420 mm × 297 mm)
77  | A4 rotada (297 mm × 210 mm)
78  | A5 rotada (210 mm × 148 mm)
79  | B4 (JIS) rotada (364 mm × 257 mm)
80  | B5 (JIS) rotada (257 mm × 182 mm)
81  | Postal Japonesa Rotada (148 mm × 100 mm)
82  | Doble postal japonesa rotada (148 mm × 200 mm)
83  | A6 rotada (148 mm × 105 mm)
84  | Sobre japonés Kaku #2 Rotado
85  | Sobre japonés Kaku #3 Rotado
86  | Sobre japonés Chou #3 Rotado
87  | Sobre japonés Chou #4 Rotado
88  | B6 (JIS) (128 mm × 182 mm)
89  | B6 (JIS) rotada (182 mm × 128 mm)
90  | (12 in × 11 in)
91  | Sobre japonés que #4
92  | Sobre japonés que #4 rotado
93  | PRC 16K (146 mm × 215 mm)
94  | PRC 32K (97 mm × 151 mm)
95  | PRC 32K(Big) (97 mm × 151 mm)
96  | #1 Sobre de la PRC (102 mm × 165 mm)
97  | #2 Sobre de la PRC (102 mm × 176 mm)
98  | #3 Sobre de la PRC (125 mm × 176 mm)
99  | #4 Sobre de la PRC (110 mm × 208 mm)
100 | #5 Sobre de la PRC (110 mm × 220 mm)
101 | #6 Sobre de la PRC (120 mm × 230 mm)
102 | #7 Sobre de la PRC (160 mm × 230 mm)
103 | #8 Sobre de la PRC (120 mm × 309 mm)
104 | #9 Sobre de la PRC (229 mm × 324 mm)
105 | #10 Sobre de la PRC (324 mm × 458 mm)
106 | PRC 16K rotada
107 | PRC 32K rotada
108 | PRC 32K(Big) rotada
109 | Sobre PRC #1 rota (165 mm × 102 mm)
110 | Sobre PRC #2 rota (176 mm × 102 mm)
111 | Sobre PRC #3 rota (176 mm × 125 mm)
112 | Sobre PRC #4 rota (208 mm × 110 mm)
113 | Sobre PRC #5 rota (220 mm × 110 mm)
114 | Sobre PRC #6 rota (230 mm × 120 mm)
115 | Sobre PRC #7 rota (230 mm × 160 mm)
116 | Sobre PRC #8 rota (309 mm × 120 mm)
117 | Sobre PRC #9 rota (324 mm × 229 mm)
118 | Sobre PRC #10 rota (458 mm × 324 mm)

- `FitToHeight` especificó el número de páginas verticales en las que encajar.

- `FitToWidth` especifica el número de páginas horizontales en las que caben.

- `PageLayoutScale` define la escala de impresión. Este atributo está restringido a valores que oscilan entre 10 (10%) y 400 (400%). Esta configuración se anula cuando se utilizan `FitToWidth` y / o `FitToHeight`.

- Por ejemplo, configure el diseño de página para `Hoja1` con impresión en blanco y negro, primer número de página impresa desde `2`, papel pequeño A4 horizontal (210 mm por 297 mm), 2 páginas verticales para ajustar, 2 páginas horizontales para ajustar encendido y escala de impresión del 50%:

```go
f := excelize.NewFile()
if err := f.SetPageLayout(
    "Hoja1",
    excelize.BlackAndWhite(true),
    excelize.FirstPageNumber(2),
    excelize.PageLayoutOrientation(excelize.OrientationLandscape),
    excelize.PageLayoutPaperSize(10),
    excelize.FitToHeight(2),
    excelize.FitToWidth(2),
    excelize.PageLayoutScale(50),
); err != nil {
    fmt.Println(err)
}
```

## Obtener el diseño de la página de la hoja de trabajo {#GetPageLayout}

```go
func (f *File) GetPageLayout(sheet string, opts ...PageLayoutOptionPtr) error
```

- `PageLayoutOrientation` proporciona un método para obtener la orientación de la hoja de trabajo
- `PageLayoutPaperSize` proporciona un método para obtener el tamaño del papel de la hoja de trabajo

- Por ejemplo, obtener el diseño de página de `Hoja1`:

```go
f := excelize.NewFile()
const sheet = "Hoja1"
var (
    orientation excelize.PageLayoutOrientation
    paperSize   excelize.PageLayoutPaperSize
)
if err := f.GetPageLayout("Hoja1", &orientation); err != nil {
    fmt.Println(err)
}
if err := f.GetPageLayout("Hoja1", &paperSize); err != nil {
    fmt.Println(err)
}
fmt.Println("Defaults:")
fmt.Printf("- orientation: %q\n", orientation)
fmt.Printf("- paper size: %d\n", paperSize)
```

Salida:

```text
Defaults:
- orientation: "portrait"
- paper size: 1
```

## Establecer márgenes de página de hoja de cálculo {#SetPageMargins}

```go
func (f *File) SetPageMargins(sheet string, opts ...PageMarginsOptions) error
```

SetPageMargins proporciona una función para establecer los márgenes de la página de la hoja de cálculo. Opciones disponibles:

Opciones|Tipo
---|---
PageMarginBotom|float64
PageMarginFooter|float64
PageMarginHeader|float64
PageMarginLeft|float64
PageMarginRight|float64
PageMarginTop|float64

- Por ejemplo, establezca los márgenes de página de `Hoja1`:

```go
f := excelize.NewFile()
const sheet = "Hoja1"

if err := f.SetPageMargins(sheet,
    excelize.PageMarginBottom(1.0),
    excelize.PageMarginFooter(1.0),
    excelize.PageMarginHeader(1.0),
    excelize.PageMarginLeft(1.0),
    excelize.PageMarginRight(1.0),
    excelize.PageMarginTop(1.0),
); err != nil {
    fmt.Println(err)
}
```

## Obtener márgenes de página de la hoja de trabajo {#GetPageMargins}

```go
func (f *File) GetPageMargins(sheet string, opts ...PageMarginsOptionsPtr) error
```

GetPageMargins proporciona una función para obtener márgenes de página de hoja de cálculo. Opciones disponibles:

Opciones|Tipo
---|---
PageMarginBotom|float64
PageMarginFooter|float64
PageMarginHeader|float64
PageMarginLeft|float64
PageMarginRight|float64
PageMarginTop|float64

- Por ejemplo, obtener los márgenes de página de `Hoja1`:

```go
f := excelize.NewFile()
const sheet = "Hoja1"

var (
    marginBottom excelize.PageMarginBottom
    marginFooter excelize.PageMarginFooter
    marginHeader excelize.PageMarginHeader
    marginLeft   excelize.PageMarginLeft
    marginRight  excelize.PageMarginRight
    marginTop    excelize.PageMarginTop
)

if err := f.GetPageMargins(sheet,
    &marginBottom,
    &marginFooter,
    &marginHeader,
    &marginLeft,
    &marginRight,
    &marginTop,
); err != nil {
    fmt.Println(err)
}
fmt.Println("Defaults:")
fmt.Println("- marginBottom:", marginBottom)
fmt.Println("- marginFooter:", marginFooter)
fmt.Println("- marginHeader:", marginHeader)
fmt.Println("- marginLeft:", marginLeft)
fmt.Println("- marginRight:", marginRight)
fmt.Println("- marginTop:", marginTop)
```

Salida:

```text
Defaults:
- marginBottom: 0.75
- marginFooter: 0.3
- marginHeader: 0.3
- marginLeft: 0.7
- marginRight: 0.7
- marginTop: 0.75
```

## Establecer las propiedades del libro de trabajo {#SetWorkbookPrOptions}

```go
func (f *File) SetWorkbookPrOptions(opts ...WorkbookPrOption) error
```

SetWorkbookPrOptions proporciona una función para establecer las propiedades del libro. Opciones Disponibles:

Opciones|Tipo
---|---
Date1904|bool
FilterPrivacy|bool
CodeName|string

Por ejemplo, establezca propiedades para el libro de trabajo:

```go
f := excelize.NewFile()
if err := f.SetWorkbookPrOptions(
    excelize.Date1904(false),
    excelize.FilterPrivacy(false),
    excelize.CodeName("code"),
); err != nil {
    fmt.Println(err)
}
```

## Obtener propiedades del libro de trabajo {#GetWorkbookPrOptions}

```go
func (f *File) GetWorkbookPrOptions(opts ...WorkbookPrOptionPtr) error
```

GetWorkbookPrOptions proporciona una función para obtener las propiedades del libro de trabajo. Opciones Disponibles:

Opciones|Tipo
---|---
Date1904|bool
FilterPrivacy|bool
CodeName|string

Por ejemplo, obtenga las propiedades del libro de trabajo:

```go
f := excelize.NewFile()
var (
    date1904      excelize.Date1904
    filterPrivacy excelize.FilterPrivacy
    codeName      excelize.CodeName
)
if err := f.GetWorkbookPrOptions(&date1904); err != nil {
    fmt.Println(err)
}
if err := f.GetWorkbookPrOptions(&filterPrivacy); err != nil {
    fmt.Println(err)
}
if err := f.GetWorkbookPrOptions(&codeName); err != nil {
    fmt.Println(err)
}
fmt.Println("Defaults:")
fmt.Printf("- date1904: %t\n", date1904)
fmt.Printf("- filterPrivacy: %t\n", filterPrivacy)
fmt.Printf("- codeName: %q\n", codeName)
```

Salida:

```text
Defaults:
- filterPrivacy: true
- codeName: ""
```

## Establecer encabezado y pie de página {#SetHeaderFooter}

```go
func (f *File) SetHeaderFooter(sheet string, settings *FormatHeaderFooter) error
```

SetHeaderFooter proporciona una función para establecer encabezados y pies de página por el nombre de la hoja de cálculo y los caracteres de control.

Los encabezados y pies de página se especifican mediante los siguientes campos de configuración:

Campos           | Descripción
---|---
AlignWithMargins | Alinee los márgenes de pie de página de encabezado con los márgenes de página
DifferentFirst   | Diferente indicador de encabezado y pie de página de primera página
DifferentOddEven | Diferente indicador de encabezados y pies de página impares e pares
ScaleWithDoc     | Escalar encabezado y pie de página con escalado de documentos
OddFooter        | Pie de página impar
OddHeader        | Encabezado extraño
EvenFooter       | Pie de página par
EvenHeader       | Incluso encabezado de página
FirstFooter      | Primer pie de página
FirstHeader      | Encabezado de la primera página

Los siguientes códigos de formato se pueden utilizar en 6 campos de tipo de cadena: `OddHeader`, `OddFooter`, `EvenHeader`, `EvenFooter`, `FirstFooter`, `FirstHeader`

<table>
    <thead>
        <tr>
            <th>Formato de código</th>
            <th>Descripción</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>&amp;&amp;</code></td>
            <td>El personaje &quot;&amp;&quot;</td>
        </tr>
        <tr>
            <td><code>&amp;font-size</code></td>
            <td>Tamaño de la fuente de texto, donde el tamaño de fuente es un tamaño de fuente decimal en puntos</td>
        </tr>
        <tr>
            <td><code>&amp;&quot;font name,font type&quot;</code></td>
            <td>Una cadena de nombre de fuente de texto, un nombre de fuente y una cadena de tipo de fuente de texto, tipo de fuente</td>
        </tr>
        <tr>
            <td><code>&amp;&quot;-,Regular&quot;</code></td>
            <td>Formato de texto normal. Alterna los modos en negrita y cursiva a desactivados</td>
        </tr>
        <tr>
            <td><code>&amp;A</code></td>
            <td>Nombre de la pestaña de la hoja de trabajo actual</td>
        </tr>
        <tr>
            <td><code>&amp;B</code> or <code>&amp;&quot;-,Bold&quot;</code></td>
            <td>Formato de texto en negrita, de apagado a en adelante, o viceversa. El modo predeterminado está desactivado</td>
        </tr>
        <tr>
            <td><code>&amp;D</code></td>
            <td>Fecha actual</td>
        </tr>
        <tr>
            <td><code>&amp;C</code></td>
            <td>Sección central</td>
        </tr>
        <tr>
            <td><code>&amp;E</code></td>
            <td>Formato de texto de subrayado doble</td>
        </tr>
        <tr>
            <td><code>&amp;F</code></td>
            <td>Nombre de archivo del libro de trabajo actual</td>
        </tr>
        <tr>
            <td><code>&amp;G</code></td>
            <td>Dibujar objeto como fondo (No es compatible actualmente)</td>
        </tr>
        <tr>
            <td><code>&amp;H</code></td>
            <td>Formato de texto de sombra</td>
        </tr>
        <tr>
            <td><code>&amp;I</code> or <code>&amp;&quot;-,Italic&quot;</code></td>
            <td>Formato de texto en cursiva</td>
        </tr>
        <tr>
            <td><code>&amp;K</code></td>
            <td>Color de fuente de texto<br>Un color RGB se especifica como RRGGBB<br>Un color de tema se especifica como TTSNNN donde TT es el identificador de color del tema, S es &quot;+&quot; o &quot;-&quot; del valor de tinte/sombra, y NNN es el valor de tinte/sombra</td>
        </tr>
        <tr>
            <td><code>&amp;L</code></td>
            <td>Sección izquierda</td>
        </tr>
        <tr>
            <td><code>&amp;N</code></td>
            <td>Número total de páginas</td>
        </tr>
        <tr>
            <td><code>&amp;O</code></td>
            <td>Formato de texto de esquema</td>
        </tr>
        <tr>
            <td><code>&amp;P[[+\|-]n]</code></td>
            <td>Sin el sufijo opcional, el número de página actual en decimal</td>
        </tr>
        <tr>
            <td><code>&amp;R</code></td>
            <td>Sección derecha</td>
        </tr>
        <tr>
            <td><code>&amp;S</code></td>
            <td>Formato de texto tachado</td>
        </tr>
        <tr>
            <td><code>&amp;T</code></td>
            <td>Hora actual</td>
        </tr>
        <tr>
            <td><code>&amp;U</code></td>
            <td>Formato de texto de subrayado único. Si el modo de subrayado doble está activado, la siguiente aparición en un especificador de sección cambia el modo de subrayado doble a desactivado; de lo contrario, alterna el modo de subrayado único, de apagado a encendido, o viceversa. El modo predeterminado está desactivado</td>
        </tr>
        <tr>
            <td><code>&amp;X</code></td>
            <td>Formato de texto superíndice</td>
        </tr>
        <tr>
            <td><code>&amp;Y</code></td>
            <td>Formato de texto de subíndice</td>
        </tr>
        <tr>
            <td><code>&amp;Z</code></td>
            <td>Current workbook&#39;s file path</td>
        </tr>
    </tbody>
</table>

Por ejemplo:

```go
err := f.SetHeaderFooter("Sheet1", &excelize.FormatHeaderFooter{
    DifferentFirst:   true,
    DifferentOddEven: true,
    OddHeader:        "&R&P",
    OddFooter:        "&C&F",
    EvenHeader:       "&L&P",
    EvenFooter:       "&L&D&R&T",
    FirstHeader:      `&CCenter &"-,Bold"Bold&"-,Regular"HeaderU+000A&D`,
})
```

Este ejemplo muestra:

- La primera página tiene su propio encabezado y pie de página
- Las páginas impares e pares tienen diferentes encabezados y pies de página
- Número de página actual en la sección derecha de los encabezados de página impar
- Nombre de archivo del libro de trabajo actual en la sección central de pies de página impar
- Número de página actual en la sección izquierda de encabezados de página par
- Fecha actual en la sección izquierda y la hora actual en la sección derecha de pies de página pares
- El texto "Center Bold Header" en la primera línea de la sección central de la primera página, y la fecha en la segunda línea de la sección central de esa misma página
- No hay pie de página en la primera página

## Establecer nombre definido {#SetDefinedName}

```go
func (f *File) SetDefinedName(definedName *DefinedName) error
```

SetDefinedName proporciona una función para establecer los nombres definidos del libro o la hoja de cálculo. Si no se especifica el ámbito, el ámbito predeterminado es el libro.

Por ejemplo:

```go
f.SetDefinedName(&excelize.DefinedName{
    Name:     "Amount",
    RefersTo: "Sheet1!$A$2:$D$5",
    Comment:  "defined name comment",
    Scope:    "Sheet2",
})
```

Configuración del área de impresión e impresión de títulos para la hoja de trabajo:

<p align="center"><img width="644" src="./images/page_setup_01.png" alt="Configuración del área de impresión e impresión de títulos para la hoja de trabajo"></p>

```go
f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Area",
    RefersTo: "Sheet1!$A$1:$Z$100",
    Scope:    "Sheet1",
})
f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Titles",
    RefersTo: "Sheet1!$A:$A,Sheet1!$1:$1",
    Scope:    "Sheet1",
})
```

## Obtener el nombre definido {#GetDefinedName}

```go
func (f *File) GetDefinedName() []DefinedName
```

GetDefinedName proporciona una función para obtener los nombres definidos del libro o la hoja de cálculo.

## Eliminar nombre definido {#DeleteDefinedName}

```go
func (f *File) DeleteDefinedName(definedName *DefinedName) error
```

DeleteDefinedName proporciona una función para eliminar los nombres definidos del libro o la hoja de cálculo. Si no se especifica el ámbito, el ámbito predeterminado es el libro. Por ejemplo:

```go
f.DeleteDefinedName(&excelize.DefinedName{
    Name:     "Amount",
    Scope:    "Sheet2",
})
```

## Establecer propiedades de la aplicación {#SetAppProps}

```go
func (f *File) SetAppProps(appProperties *AppProperties) error
```

SetAppProps proporciona una función para establecer las propiedades de la aplicación de documentos. Las propiedades que se pueden configurar son:

Propiedad      | Descripción
---|---
Application       | El nombre de la aplicación que creó este documento.
ScaleCrop         | Indica el modo de visualización de la miniatura del documento. Establezca este elemento en `true` para habilitar la escala de la miniatura del documento en la pantalla. Establezca este elemento en `false` para permitir el recorte de la miniatura del documento para mostrar solo las secciones que se ajustarán a la pantalla.
DocSecurity       | Nivel de seguridad de un documento como valor numérico. La seguridad del documento se define como:<br>1 - El documento está protegido con contraseña.<br>2 - Se recomienda abrir el documento como de solo lectura.<br>3 - El documento debe abrirse como de solo lectura.<Br >4 - el documento está bloqueado para anotaciones.
Company           | The name of a company associated with the document.
LinksUpToDate     | Indica si los hipervínculos de un documento están actualizados. Establezca este elemento en `true` para indicar que los hipervínculos están actualizados. Establezca este elemento en `false` para indicar que los hipervínculos están desactualizados.
HyperlinksChanged | Especifica que uno o más hipervínculos en esta parte fueron actualizados exclusivamente en esta parte por un productor. El próximo productor que abra este documento deberá actualizar las relaciones de hipervínculos con los nuevos hipervínculos especificados en esta parte.
AppVersion        | Especifica la versión de la aplicación que produjo este documento. El contenido de este elemento tendrá la forma XX.YYYY donde X e Y representan valores numéricos, o el documento se considerará no conforme.

Por ejemplo:

```go
err := f.SetAppProps(&excelize.AppProperties{
    Application:       "Microsoft Excel",
    ScaleCrop:         true,
    DocSecurity:       3,
    Company:           "Company Name",
    LinksUpToDate:     true,
    HyperlinksChanged: true,
    AppVersion:        "16.0000",
})
```

## Obtener propiedades de la aplicación {#GetAppProps}

```go
func (f *File) GetAppProps() (*AppProperties, error)
```

GetAppProps proporciona una función para obtener propiedades de la aplicación de documentos.

## Establecer las propiedades del documento {#SetDocProps}

```go
func (f *File) SetDocProps(docProperties *DocProperties) error
```

SetDocProps proporciona una función para establecer las propiedades del núcleo del documento. Las propiedades que se pueden establecer son:

Propiedad      | Descripción
---|---
Category       | Una categorización del contenido de este paquete.
ContentStatus  | El estado del contenido. Por ejemplo, los valores pueden incluir "Draft", "Reviewed" y "Final".
Created        | La hora de modificación del contenido del recurso.
Creator        | Una entidad responsable principal de hacer que el contenido del recurso.
Description    | Una explicación del contenido del recurso.
Identifier     | Una referencia inequívoca al recurso dentro de un contexto determinado.
Keywords       | Un conjunto delimitado de palabras clave para admitir la búsqueda y la indexación. Normalmente se trata de una lista de términos que no están disponibles en otras partes de las propiedades.
Language       | El lenguaje del contenido intelectual del recurso.
LastModifiedBy | El usuario que realizó la última modificación. La identificación es específica del entorno.
Modified       | La hora de modificación del contenido del recurso.
Revision       | El número de revisión del contenido del recurso.
Subject        | El tema del contenido del recurso.
Title          | El nombre se dio al recurso.
Version        | El número de versión. Este valor lo establece el usuario o la aplicación.

Por ejemplo:

```go
err := f.SetDocProps(&excelize.DocProperties{
    Category:       "category",
    ContentStatus:  "Draft",
    Created:        "2019-06-04T22:00:10Z",
    Creator:        "Go Excelize",
    Description:    "This file created by Go Excelize",
    Identifier:     "xlsx",
    Keywords:       "Spreadsheet",
    LastModifiedBy: "Go Author",
    Modified:       "2019-06-04T22:00:10Z",
    Revision:       "0",
    Subject:        "Test Subject",
    Title:          "Test Title",
    Language:       "en-US",
    Version:        "1.0.0",
})
```

## Obtener propiedades del documento {#GetDocProps}

```go
func (f *File) GetDocProps() (*DocProperties, error)
```

GetDocProps proporciona una función para obtener las propiedades principales del documento.
