# Imagen

## Añadir imagen {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture string, opts *GraphicOptions) error
```

AddPicture permite agregar una imagen a una hoja de cálculo según el formato de imagen (como desplazamiento, escala, relación de aspecto y configuración de impresión) y la ruta de archivo. Los tipos de imagen admitidos son: BMP, EMF, EMZ, GIF, ICO, JPEG, JPG, PNG, SVG, TIF, TIFF, WMF y WMZ. Esta función es compatible con concurrencia. Tenga en cuenta que, actualmente, esta función solo permite agregar imágenes sobre las celdas, no las imágenes dentro de las celdas ni crear celdas de imagen incrustadas en Kingsoft WPS Office.

Por ejemplo:

```go
package main

import (
    "fmt"
    _ "image/gif"
    _ "image/jpeg"
    _ "image/png"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    // Insertar una imagen.
    if err := f.AddPicture("Sheet1", "A2", "image.png", nil); err != nil {
        fmt.Println(err)
        return
    }
    // Inserte una imagen en la hoja de trabajo con escalado.
    enable, disable := true, false
    if err := f.AddPicture("Sheet1", "D2", "image.jpg",
        &excelize.GraphicOptions{
            ScaleX:        0.5,
            ScaleY:        0.5,
            Hyperlink:     "#Sheet2!D8",
            HyperlinkType: "Location",
        },
    ); err != nil {
        fmt.Println(err)
        return
    }
    // Inserte un desplazamiento de imagen en la celda con soporte de impresión.
    if err := f.AddPicture("Sheet1", "H2", "image.gif",
        &excelize.GraphicOptions{
            OffsetX:         15,
            OffsetY:         10,
            Hyperlink:       "https://github.com/xuri/excelize",
            HyperlinkType:   "External",
            PrintObject:     &enable,
            LockAspectRatio: false,
            Locked:          &disable,
            Positioning:     "oneCell",
        },
    ); err != nil {
        fmt.Println(err)
        return
    }
    // Guarde la hoja de cálculo por la ruta dada.
    if err = f.Save(); err != nil {
        fmt.Println(err)
    }
}
```

El parámetro opcional `AltText` se usa para agregar texto alternativo a un objeto gráfico.

El parámetro opcional `PrintObject` indica si la imagen se imprime cuando se imprime la hoja de trabajo, el valor predeterminado de eso es `true`.

El parámetro opcional `Locked` indica si se bloquea la imagen. Bloquear un objeto no tiene ningún efecto a menos que la hoja esté protegida.

El parámetro opcional `LockAspectRatio` indica si se bloquea la relación de aspecto de la imagen, el valor predeterminado es `false`.

El parámetro opcional `AutoFit` especifica si el tamaño de la imagen se ajusta automáticamente a la celda, el valor predeterminado es `false`.

El parámetro opcional `OffsetX` especifica el desplazamiento horizontal de la imagen con la celda, el valor predeterminado es 0.

El parámetro opcional `OffsetY` especifica el desplazamiento vertical de la imagen con la celda, cuyo valor predeterminado es 0.

El parámetro opcional `ScaleX` especifica la escala horizontal de las imágenes, el valor predeterminado de eso es 1.0 que presenta 100%.

El parámetro opcional `ScaleY` especifica la escala vertical de las imágenes, el valor predeterminado de eso es 1.0 que presenta 100%.

El parámetro opcional `Hyperlink` especifica el hipervínculo de la imagen.

El parámetro opcional `HyperlinkType` define dos tipos de hipervínculo `External` para el sitio web o `Location` para moverse a una de las celdas de este libro de trabajo. Cuando el `HyperlinkType` es `Location`, las coordenadas deben comenzar con `#`.

El parámetro opcional `Positioning` define 3 tipos de posición de un objeto gráfico en una hoja de cálculo: `oneCell` (Mover pero no cambiar el tamaño de las celdas), `twoCell` (Mover y cambiar el tamaño de las celdas) y `absolute` (No mover ni dimensionar con celdas). Si no establece este parámetro, el posicionamiento predeterminado es mover y cambiar el tamaño de las celdas.

```go
func (f *File) AddPictureFromBytes(sheet, cell string, pic *Picture) error
```

AddPictureFromBytes proporciona el método para agregar una imagen en una hoja mediante un conjunto de formato de imagen determinado (como desplazamiento, escala, configuración de relación de aspecto y configuración de impresión), descripción de texto alternativo, nombre de extensión y contenido de archivo en el tipo `[]byte`. Tipos de imagen compatibles: EMF, EMZ, GIF, ICO, JPEG, JPG, PNG, SVG, TIF, TIFF, WMF y WMZ. Tenga en cuenta que esta función solo permite añadir imágenes sobre las celdas, no las insertadas en celdas ni crear celdas con imágenes incrustadas en Kingsoft WPS Office.

Por ejemplo:

```go
package main

import (
    "fmt"
    _ "image/jpeg"
    "os"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    file, err := os.ReadFile("image.jpg")
    if err != nil {
        fmt.Println(err)
        return
    }
    if err := f.AddPictureFromBytes("Sheet1", "A2", &excelize.Picture{
        Extension: ".jpg",
        File:      file,
        Format:    &excelize.GraphicOptions{AltText: "Excel Logo"},
    }); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Obtener imagen {#GetPicture}

```go
func (f *File) GetPictures(sheet, cell string) ([]Picture, error)
```

GetPicture proporciona una función para obtener el nombre base de la imagen y el contenido sin procesar incrustado en una hoja de cálculo por la hoja de trabajo y el nombre de celda dados. Esta función es segura para la simultaneidad. Esta función devuelve el nombre del archivo en la hoja de cálculo y el contenido del archivo como tipos de datos `[]byte`.

Por ejemplo:

```go
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
pics, err := f.GetPictures("Sheet1", "A2")
if err != nil {
    fmt.Println(err)
}
for idx, pic := range pics {
    name := fmt.Sprintf("image%d%s", idx+1, pic.Extension)
    if err := os.WriteFile(name, pic.File, 0644); err != nil {
        fmt.Println(err)
    }
}
```

## Eliminar imagen {#DeletePicture}

```go
func (f *File) DeletePicture(sheet, cell string) error
```

DeletePicture proporciona una función para eliminar gráficos en una hoja de cálculo por la hoja de trabajo y el nombre de celda dados. Tenga en cuenta que el archivo de imagen no se eliminará del documento actualmente.
