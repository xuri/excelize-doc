# Imagen

## Añadir imagen {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture, format string) error
```

AddPicture proporciona el método para agregar una imagen a una hoja de trabajo mediante un conjunto de formato de imagen determinado (como desplazamiento, escala, configuración de relación de aspecto y configuración de impresión) y la ruta del archivo.

Por ejemplo:

```go
package main

import (
    "fmt"
    _ "image/gif"
    _ "image/jpeg"
    _ "image/png"

    "github.com/360EntSecGroup-Skylar/excelize"
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
}
```

LinkType define dos tipos de hipervínculos `External` para un sitio web o `Location` para moverse a una de las celdas de este libro. Cuando el `hyperlink_type` es `Location`, las coordenadas deben comenzar con `#`.

El posicionamiento define dos tipos de posición de una imagen en una hoja de cálculo de Excel, `oneCell` (Mover pero no dimensionar con celdas) o "absoluto" (No mover ni dimensionar con celdas). Si no establece este parámetro, el `positioning` predeterminado es mover y dimensionar con celdas.

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

    "github.com/360EntSecGroup-Skylar/excelize"
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

GetPicture proporciona una función para obtener el nombre base de la imagen y el contenido sin procesar incrustado en una hoja de cálculo por la hoja de trabajo y el nombre de celda dados. Esta función devuelve el nombre del archivo en la hoja de cálculo y el contenido del archivo como tipos de datos `[]byte`.

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
