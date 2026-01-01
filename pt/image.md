# Imagem

## Inserir imagem {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture string, opts *GraphicOptions) error
```

AddPicture fornece o método para adicionar uma imagem a uma planilha com base em um conjunto de formatos de imagem (como deslocamento, escala, configuração de proporção e configurações de impressão) e caminho de arquivo, além dos tipos de imagem suportados: BMP, EMF, EMZ, GIF, ICO, JPEG, JPG, PNG, SVG, TIF, TIFF, WMF e WMZ. Esta função é segura para concorrência. Observe que esta função suporta apenas a adição de imagens posicionadas sobre as células atuais e não suporta a adição de imagens posicionadas em células ou a criação de células de imagem incorporadas do Kingsoft WPS Office.

Por exemplo:

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
    if err := f.SetSheetName("Sheet1", "Planilha1"); err != nil {
        fmt.Println(err)
        return
    }
    // Insira uma imagem.
    if err := f.AddPicture("Planilha1", "A2", "image.png", nil); err != nil {
        fmt.Println(err)
        return
    }
    // Insira uma escala de imagem na célula com hiperlink de localização.
    enable, disable := true, false
    if err := f.AddPicture("Planilha1", "D2", "image.jpg",
        &excelize.GraphicOptions{
            ScaleX:        0.5,
            ScaleY:        0.5,
            Hyperlink:     "#Planilha2!D8",
            HyperlinkType: "Location",
        },
    ); err != nil {
        fmt.Println(err)
        return
    }
    // Insira um deslocamento de imagem na célula com hiperlink externo, suporte para impressão e posicionamento.
    if err := f.AddPicture("Planilha1", "H2", "image.gif",
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
    if err := f.SaveAs("Pasta1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

O parâmetro opcional `AltText` é usado para adicionar texto alternativo a um objeto gráfico.

O parâmetro opcional `PrintObject` indica se o objeto gráfico é impresso quando a planilha é impressa, o valor padrão é `true`.

O parâmetro opcional `Locked` indica se bloqueia o objeto gráfico. Bloquear um objeto não tem efeito a menos que a planilha esteja protegida.

O parâmetro opcional `LockAspectRatio` indica se a proporção de aspecto do objeto gráfico é bloqueada, o valor padrão é `false`.

O parâmetro opcional `AutoFit` especifica se o tamanho do objeto gráfico se ajusta automaticamente à célula, o valor padrão disso é `false`.

O parâmetro opcional `OffsetX` especifica o deslocamento horizontal do objeto gráfico com a célula, o valor padrão é 0.

O parâmetro opcional `OffsetY` especifica o deslocamento vertical do objeto gráfico com a célula, o valor padrão é 0.

O parâmetro opcional `ScaleX` especifica a escala horizontal do objeto gráfico. O valor de `ScaleX` deve ser um número de ponto flutuante maior que 0 com precisão de duas casas decimais. O valor padrão é 1.0, que representa 100%.

O parâmetro opcional `ScaleY` especifica a escala vertical do objeto gráfico. O valor de `ScaleY` deve ser um número de ponto flutuante maior que 0 com precisão de duas casas decimais. O valor padrão é 1.0, que representa 100%.

O parâmetro opcional `Hyperlink` especifica o hiperlink do objeto gráfico.

O parâmetro opcional `HyperlinkType` define dois tipos de hiperlink `Externo` para o site ou `Local` para mover para uma das células desta pasta de trabalho. Quando `HyperlinkType` for `Location`, as coordenadas precisam começar com `#`.

O parâmetro opcional `Positioning` define 3 tipos de posição de um objeto gráfico em uma planilha: `oneCell` (mover mas não dimensionar com células), `twoCell` (mover e dimensionar com células) e `absolute` ( Não mova ou dimensione com células). Se você não definir esse parâmetro, o posicionamento padrão será mover e dimensionar com células.

```go
func (f *File) AddPictureFromBytes(sheet, cell string, pic *Picture) error
```

AddPictureFromBytes fornece o método para adicionar uma imagem em uma planilha por determinado conjunto de formato de imagem (como deslocamento, escala, configuração de proporção e configurações de impressão), descrição de texto alternativo, nome de extensão e conteúdo do arquivo no tipo `[]byte`. Tipos de imagem suportados: EMF, EMZ, GIF, ICO, JPEG, JPG, PNG, SVG, TIF, TIFF, WMF e WMZ. Observe que esta função suporta apenas a adição de imagens posicionadas sobre as células atuais e não suporta a adição de imagens posicionadas em células ou a criação de células de imagem incorporadas do Kingsoft WPS Office.

Por exemplo:

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
    if err := f.SetSheetName("Sheet1", "Planilha1"); err != nil {
        fmt.Println(err)
        return
    }
    file, err := os.ReadFile("image.jpg")
    if err != nil {
        fmt.Println(err)
        return
    }
    if err := f.AddPictureFromBytes("Planilha1", "A2", &excelize.Picture{
        Extension: ".jpg",
        File:      file,
        Format:    &excelize.GraphicOptions{AltText: "Logotipo do Excel"},
    }); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("Pasta1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Obter imagem {#GetPicture}

```go
func (f *File) GetPictures(sheet, cell string) ([]Picture, error)
```

GetPicture fornece uma função para obter o nome base da imagem e o conteúdo bruto incorporado em uma planilha por meio de uma determinada planilha e nome da célula. Esta função é segura para simultaneidade. Esta função retorna o nome do arquivo na planilha e o conteúdo do arquivo como tipos de dados `[]byte`. Observe que esta função atualmente não suporta a recuperação de todas as propriedades da propriedade `Format` da imagem, e o valor das propriedades `ScaleX` e `ScaleY` é um número de ponto flutuante maior que 0 com precisão de duas casas decimais.

Por exemplo:

```go
f, err := excelize.OpenFile("Pasta1.xlsx")
if err != nil {
    fmt.Println(err)
    return
}
defer func() {
    if err := f.Close(); err != nil {
        fmt.Println(err)
    }
}()
pics, err := f.GetPictures("Planilha1", "A2")
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

## Excluir imagem {#DeletePicture}

```go
func (f *File) DeletePicture(sheet, cell string) error
```

DeletePicture fornece uma função para excluir gráficos em uma planilha por determinado nome de planilha e referência de célula. Observe que o arquivo de imagem não será excluído do documento atualmente.
