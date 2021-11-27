# Uso básico

## Instalación {#install}

Using the latest version Excelize library require to Go version 1.15 or later.

- Instalación

```bash
go get github.com/xuri/excelize
```

- Si la administración de paquetes con [Go Modules](https://go.dev/blog/using-go-modules), instálelo con el siguiente comando.

```bash
go get github.com/xuri/excelize/v2
```

## Actualizar {#update}

- Actualizar

```bash
go get -u github.com/xuri/excelize/v2
```

## Crear una hoja de cálculo {#NewFile}

Este es un uso mínimo de ejemplo que creará un archivo de hoja de cálculo:

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    // Crear una nueva hoja de trabajo.
    index := f.NewSheet("Sheet2")
    // Establecer el valor de una celda.
    f.SetCellValue("Sheet2", "A2", "Hello world.")
    f.SetCellValue("Sheet1", "B2", 100)
    // Establezca la hoja de trabajo activa del libro de trabajo.
    f.SetActiveSheet(index)
    // Guarde la hoja de cálculo por la ruta dada.
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Lectura de hojas de cálculo {#read}

Lo siguiente constituye el desnudo para leer un documento de hoja de cálculo:

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
    // Obtener valor de la celda por el nombre y el eje de la hoja de trabajo dado.
    cell, err := f.GetCellValue("Sheet1", "B2")
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(cell)
    // Obtener todas las filas en el Sheet1.
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
}
```

## Añadir un gráfico a una hoja de cálculo {#chart}

Con Excelize la generación y administración de gráficos es tan fácil como unas pocas líneas de código. Puede crear gráficos basados en datos en su hoja de trabajo o generar gráficos sin ningún dato en su hoja de trabajo en absoluto.

<p align="center"><img width="770" src="../images/base.png" alt="Añadir un gráfico a una hoja de cálculo"></p>

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    categories := map[string]string{
        "A2": "Pequeño", "A3": "Normal", "A4": "Grande", "B1": "Manzana", "C1": "Naranja", "D1": "Pera"}
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
        "type": "col3DClustered",
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
        },
        {
            "name": "Sheet1!$A$4",
            "categories": "Sheet1!$B$1:$D$1",
            "values": "Sheet1!$B$4:$D$4"
        }],
        "title":
        {
            "name": "Gráfico de columnas agrupadas 3D"
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

## Añadir una imagen a la hoja de cálculo {#image}

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
