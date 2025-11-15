# Immagine

## Aggiungi immagine {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture string, opts *GraphicOptions) error
```

AddPicture fornisce il metodo per aggiungere un'immagine a un foglio di lavoro in base a un set di formati immagine (come offset, scala, impostazioni di proporzioni e impostazioni di stampa) e al percorso del file. I tipi di immagine supportati sono: BMP, EMF, EMZ, GIF, ICO, JPEG, JPG, PNG, SVG, TIF, TIFF, WMF e WMZ. Questa funzione è sicura per la concorrenza. Si noti che questa funzione supporta solo l'aggiunta di immagini posizionate sopra le celle correnti e non supporta l'aggiunta di immagini posizionate nelle celle o la creazione di celle con immagini incorporate in Kingsoft WPS Office.

Per esempio:

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
    if err := f.SetSheetName("Sheet1", "Foglio1"); err != nil {
        fmt.Println(err)
        return
    }
    // Inserisci un'immagine.
    if err := f.AddPicture("Foglio1", "A2", "image.png", nil); err != nil {
        fmt.Println(err)
        return
    }
    // Inserisci un'immagine in scala nella cella con il collegamento
    // ipertestuale della posizione.
    enable, disable := true, false
    if err := f.AddPicture("Foglio1", "D2", "image.jpg",
        &excelize.GraphicOptions{
            ScaleX:        0.5,
            ScaleY:        0.5,
            Hyperlink:     "#Foglio2!D8",
            HyperlinkType: "Location",
        },
    ); err != nil {
        fmt.Println(err)
        return
    }
    // Inserisci un offset dell'immagine nella cella con collegamento
    // ipertestuale esterno, supporto per la stampa e il posizionamento.
    if err := f.AddPicture("Foglio1", "H2", "image.gif",
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
    if err := f.SaveAs("Cartel1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

Il parametro opzionale `AltText` viene utilizzato per aggiungere testo alternativo a un oggetto grafico.

Il parametro opzionale `PrintObject` indica se l'oggetto grafico viene stampato quando viene stampato il foglio di lavoro, il valore predefinito è `true`.

Il parametro opzionale `Locked` indica se bloccare l'oggetto grafico. Bloccare un oggetto non ha alcun effetto a meno che il foglio non sia protetto.

Il parametro facoltativo `LockAspectRatio` indica se bloccare le proporzioni per l'oggetto grafico, il cui valore predefinito è `false`.

Il parametro facoltativo `AutoFit` specifica se la dimensione dell'oggetto grafico si adatta automaticamente alla cella, il cui valore predefinito è `false`.

Il parametro opzionale `OffsetX` specifica l'offset orizzontale dell'oggetto grafico con la cella, il cui valore predefinito è 0.

Il parametro opzionale `OffsetY` specifica l'offset verticale dell'oggetto grafico con la cella, il cui valore predefinito è 0.

Il parametro opzionale `ScaleX` specifica la scala orizzontale dell'oggetto grafico, il cui valore predefinito è 1.0 che rappresenta il 100%.

Il parametro opzionale `ScaleY` specifica la scala verticale dell'oggetto grafico, il cui valore predefinito è 1.0 che rappresenta il 100%.

Il parametro opzionale `Hyperlink` specifica il collegamento ipertestuale dell'oggetto grafico.

Il parametro facoltativo `HyperlinkType` definisce due tipi di collegamento ipertestuale `External` per il sito Web o `Location` per spostarsi in una delle celle di questa cartella di lavoro. Quando `HyperlinkType` è `Location`, le coordinate devono iniziare con `#`.

Il parametro opzionale `Positioning` definisce 3 tipi di posizione di un oggetto grafico in un foglio di calcolo: `oneCell` (Sposta ma non ridimensiona con le celle), `twoCell` (Sposta e ridimensiona con le celle) e `absolute` ( Non spostare o ridimensionare con le celle). Se non imposti questo parametro, il posizionamento predefinito prevede lo spostamento e il ridimensionamento con le celle.

```go
func (f *File) AddPictureFromBytes(sheet, cell string, pic *Picture) error
```

AddPictureFromBytes fornisce il metodo per aggiungere un'immagine in un foglio in base a un determinato formato immagine impostato (come offset, scala, impostazione delle proporzioni e impostazioni di stampa), descrizione del testo alternativo, nome dell'estensione e contenuto del file nel tipo `[]byte`. Tipi di immagine supportati: EMF, EMZ, GIF, ICO, JPEG, JPG, PNG, SVG, TIF, TIFF, WMF e WMZ. Si noti che questa funzione supporta solo l'aggiunta di immagini posizionate sopra le celle e non supporta l'aggiunta di immagini posizionate nelle celle o la creazione di celle con immagini incorporate in Kingsoft WPS Office.

Per esempio:

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
    if err := f.SetSheetName("Sheet1", "Foglio1"); err != nil {
        fmt.Println(err)
        return
    }
    file, err := os.ReadFile("immagine.jpg")
    if err != nil {
        fmt.Println(err)
        return
    }
    if err := f.AddPictureFromBytes("Foglio1", "A2", &excelize.Picture{
        Extension: ".jpg",
        File:      file,
        Format:    &excelize.GraphicOptions{AltText: "Logo Excel"},
    }); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("Cartel1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Ottieni immagine {#GetPicture}

```go
func (f *File) GetPictures(sheet, cell string) ([]Picture, error)
```

GetPicture fornisce una funzione per ottenere il nome base dell'immagine e il contenuto non elaborato incorporato in un foglio di calcolo in base al foglio di lavoro e al nome della cella specificati. Questa funzione è sicura per la concorrenza. Questa funzione restituisce il nome del file nel foglio di calcolo e il contenuto del file come tipi di dati `[]byte`.

Per esempio:

```go
f, err := excelize.OpenFile("Cartel1.xlsx")
if err != nil {
    fmt.Println(err)
    return
}
defer func() {
    if err := f.Close(); err != nil {
        fmt.Println(err)
    }
}()
pics, err := f.GetPictures("Foglio1", "A2")
if err != nil {
    fmt.Println(err)
}
for idx, pic := range pics {
    name := fmt.Sprintf("immagine%d%s", idx+1, pic.Extension)
    if err := os.WriteFile(name, pic.File, 0644); err != nil {
        fmt.Println(err)
    }
}
```

## Elimina immagine {#DeletePicture}

```go
func (f *File) DeletePicture(sheet, cell string) error
```

DeletePicture fornisce una funzione per eliminare i grafici in un foglio di calcolo in base al nome del foglio di lavoro e al riferimento alla cella. Tieni presente che al momento il file immagine non verrà eliminato dal documento.
