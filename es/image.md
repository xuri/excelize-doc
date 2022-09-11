# Imagen

## Añadir imagen {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture, format string) error
```

AddPicture proporciona el método para agregar una imagen a una hoja de trabajo mediante un conjunto de formato de imagen determinado (como desplazamiento, escala, configuración de relación de aspecto y configuración de impresión) y la ruta del archivo. Esta función es segura para la simultaneidad.

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
    f, err := excelize.OpenFile("Book1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    // Insertar una imagen.
    if err := f.AddPicture("Sheet1", "A2", "image.png", ""); err != nil {
        fmt.Println(err)
    }
    // Inserte una imagen en la hoja de trabajo con escalado.
    if err := f.AddPicture("Sheet1", "D2", "image.jpg", `{
        "x_scale": 0.5,
        "y_scale": 0.5
    }`); err != nil {
        fmt.Println(err)
    }
    // Inserte un desplazamiento de imagen en la celda con soporte de impresión.
    if err := f.AddPicture("Sheet1", "H2", "image.gif", `{
        "x_offset": 15,
        "y_offset": 10,
        "print_obj": true,
        "lock_aspect_ratio": false,
        "locked": false
    }`); err != nil {
        fmt.Println(err)
    }
    // Guarde la hoja de cálculo por la ruta dada.
    if err = f.Save(); err != nil {
        fmt.Println(err)
    }
    if err = f.Close(); err != nil {
        fmt.Println(err)
    }
}
```

El parámetro opcional `autofit` especifica si el tamaño de la imagen se ajusta automáticamente a la celda, el valor predeterminado es `false`.

El parámetro opcional `hyperlink` especifica el hipervínculo de la imagen.

El parámetro opcional `hyperlink_type` define dos tipos de hipervínculo `External` para el sitio web o `Location` para moverse a una de las celdas de este libro de trabajo. Cuando el `hyperlink_type` es `Location`, las coordenadas deben comenzar con `#`.

El parámetro opcional `positioning` define dos tipos de posición de una imagen en una hoja de cálculo de Excel, `oneCell` (mover pero no dimensionar con celdas) o `absolute` (no mover ni dimensionar con celdas). Si no configura este parámetro, la posición predeterminada es mover y tamaño con celdas.

El parámetro opcional `print_obj` indica si la imagen se imprime cuando se imprime la hoja de trabajo, el valor predeterminado de eso es `true`.

El parámetro opcional `lock_aspect_ratio` indica si se bloquea la relación de aspecto de la imagen, el valor predeterminado es `false`.

El parámetro opcional `locked` indica si se bloquea la imagen. Bloquear un objeto no tiene ningún efecto a menos que la hoja esté protegida.

El parámetro opcional `x_offset` especifica el desplazamiento horizontal de la imagen con la celda, el valor predeterminado es 0.

El parámetro opcional `x_scale` especifica la escala horizontal de las imágenes, el valor predeterminado de eso es 1.0 que presenta 100%.

El parámetro opcional `y_offset` especifica el desplazamiento vertical de la imagen con la celda, cuyo valor predeterminado es 0.

El parámetro opcional `y_scale` especifica la escala vertical de las imágenes, el valor predeterminado de eso es 1.0 que presenta 100%.

```go
func (f *File) AddPictureFromBytes(sheet, cell, format, name, extension string, file []byte) error
```

AddPictureFromBytes proporciona el método para agregar una imagen en una hoja mediante un conjunto de formato de imagen determinado (como desplazamiento, escala, configuración de relación de aspecto y configuración de impresión), descripción de texto alternativo, nombre de extensión y contenido de archivo en el tipo `[]byte`.

Por ejemplo:

```go
package main

import (
    _ "image/jpeg"
    "io/ioutil"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()

    file, err := ioutil.ReadFile("image.jpg")
    if err != nil {
        fmt.Println(err)
    }
    if err := f.AddPictureFromBytes("Sheet1", "A2", "", "Excel Logo", ".jpg", file); err != nil {
        fmt.Println(err)
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Obtener imagen {#GetPicture}

```go
func (f *File) GetPicture(sheet, cell string) (string, []byte, error)
```

GetPicture proporciona una función para obtener el nombre base de la imagen y el contenido sin procesar incrustado en una hoja de cálculo por la hoja de trabajo y el nombre de celda dados. Esta función es segura para la simultaneidad. Esta función devuelve el nombre del archivo en la hoja de cálculo y el contenido del archivo como tipos de datos `[]byte`.

Por ejemplo:

```go
f, err := excelize.OpenFile("Book1.xlsx")
if err != nil {
    fmt.Println(err)
    return
}
file, raw, err := f.GetPicture("Sheet1", "A2")
if err != nil {
    fmt.Println(err)
    return
}
if err := ioutil.WriteFile(file, raw, 0644); err != nil {
    fmt.Println(err)
}
```

## Eliminar imagen {#DeletePicture}

```go
func (f *File) DeletePicture(sheet, cell string) (err error)
```

DeletePicture proporciona una función para eliminar gráficos en una hoja de cálculo por la hoja de trabajo y el nombre de celda dados. Tenga en cuenta que el archivo de imagen no se eliminará del documento actualmente.
