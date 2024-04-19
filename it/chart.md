# Grafico

## Aggiungi grafico {#AddChart}

```go
func (f *File) AddChart(sheet, cell, opts string, combo ...string) error
```

AddChart fornisce il metodo per aggiungere un grafico in un foglio di lavoro in base al formato del grafico specificato (come offset, scala, impostazione delle proporzioni e impostazioni di stampa) e alle proprietà impostate.

Di seguito viene mostrato il `Type` di grafico supportato da Excelize:

ID|Enumerazione|Grafico
---|---|---
0  | Area                        | Grafico ad area 2D
1  | AreaStacked                 | Grafico ad area in pila 2D
2  | AreaPercentStacked          | Grafico ad area in pila 2D al 100%
3  | Area3D                      | Grafico ad area 3D
4  | Area3DStacked               | Grafico ad area in pila 3D
5  | Area3DPercentStacked        | Grafico ad area in pila 3D al 100%
6  | Bar                         | Grafico a barre raggruppate 2D
7  | BarStacked                  | Grafico a barre in pila 2D
8  | BarPercentStacked           | Grafico a barre in pila 2D al 100%
9  | Bar3DClustered              | Grafico a barre raggruppate 3D
10 | Bar3DStacked                | Grafico a barre in pila 3D
11 | Bar3DPercentStacked         | Grafico a barre in pila 3D al 100%
12 | Bar3DConeClustered          | Grafico a barre raggruppato a cono 3D
13 | Bar3DConeStacked            | Grafico a barre in pila a cono 3D
14 | Bar3DConePercentStacked     | Grafico a barre a cono 3D al 100%
15 | Bar3DPyramidClustered       | Grafico a barre raggruppato a piramide 3D
16 | Bar3DPyramidStacked         | Grafico a barre in pila a piramide 3D
17 | Bar3DPyramidPercentStacked  | Grafico a barre in pila piramidale 3D al 100%
18 | Bar3DCylinderClustered      | Grafico a barre raggruppato di cilindri 3D
19 | Bar3DCylinderStacked        | Grafico a barre in pila a cilindri 3D
20 | Bar3DCylinderPercentStacked | Grafico a barre in pila 3D con cilindri al 100%
21 | Col                         | Istogramma a colonne raggruppate 2D
22 | ColStacked                  | Istogramma in pila 2D
23 | ColPercentStacked           | Istogramma in pila 2D al 100%
24 | Col3DClustered              | Istogramma a colonne raggruppate 3D
25 | Col3D                       | Grafico a colonne 3D
26 | Col3DStacked                | Istogramma in pila 3D
27 | Col3DPercentStacked         | Istogramma in pila 3D al 100%
28 | Col3DCone                   | Istogramma a cono 3D
29 | Col3DConeClustered          | Istogramma a colonne raggruppate a cono 3D
30 | Col3DConeStacked            | Istogramma in pila a cono 3D
31 | Col3DConePercentStacked     | Istogramma in pila a cono 3D al 100%
32 | Col3DPyramid                | Grafico a colonne piramidale 3D
33 | Col3DPyramidClustered       | Istogramma a colonne raggruppate a piramide 3D
34 | Col3DPyramidStacked         | Istogramma in pila a piramide 3D
35 | Col3DPyramidPercentStacked  | Grafico a colonne in pila piramidale 3D al 100%
36 | Col3DCylinder               | Grafico a colonne del cilindro 3D
37 | Col3DCylinderClustered      | Istogramma a colonne raggruppate con cilindri 3D
38 | Col3DCylinderStacked        | Istogramma a colonne in pila a cilindri 3D
39 | Col3DCylinderPercentStacked | Grafico a colonne in pila a cilindri 3D al 100%
40 | Doughnut                    | Grafico a ciambella
41 | Line                        | Grafico a linee
42 | Line3D                      | Grafico a linee 3D
43 | Pie                         | Grafico a torta
44 | Pie3D                       | Grafico a torta 3D
45 | PieOfPie                    | Torta del grafico a torta
46 | BarOfPie                    | Barra del grafico a torta
47 | Radar                       | Carta radar
48 | Scatter                     | Grafico a dispersione
49 | Surface3D                   | Grafico di superficie 3D
50 | WireframeSurface3D          | Grafico di superficie wireframe 3D
51 | Contour                     | Grafico del contorno
52 | WireframeContour            | Grafico di contorno wireframe
53 | Bubble                      | Grafico a bolle
54 | Bubble3D                    | Grafico a bolle 3D

Nell'intervallo di dati del grafico di Office Excel, `Series` specifica l'insieme di informazioni per cui i dati tracciare, l'elemento della legenda (serie) e l'etichetta dell'asse orizzontale (categoria).

Le opzioni `Series` che possono essere impostate sono:

Parametro|Spiegazione
---|---
Name              | Elemento della legenda (serie), visualizzato nella legenda del grafico e nella barra della formula. Il parametro `Name` è facoltativo. Se non specifichi questo valore, il valore predefinito sarà `Serie 1 .. n`. Supporto `Name` per la rappresentazione della formula, ad esempio: `Foglio1!$A$1`.
Categories        | Etichetta dell'asse orizzontale (categoria). Il parametro `Categories` è facoltativo nella maggior parte dei tipi di grafici, il valore predefinito è una sequenza contigua nella forma `1..n`.
Values            | L'area dati del grafico, che è il parametro più importante in `Series`, è anche l'unico parametro richiesto durante la creazione di un grafico. Questa opzione collega il grafico ai dati del foglio di lavoro visualizzato.
Fill              | Imposta il formato per il riempimento delle serie di dati.
Line              | Imposta il formato della linea del grafico a linee. La proprietà `Line` è facoltativa e se non viene fornita avrà lo stile predefinito. L'opzione che può essere impostata è `Width`. L'intervallo di `Width` è compreso tra 0.25pt e 999pt. Se il valore della larghezza non è compreso nell'intervallo, la larghezza predefinita della linea è 2pt.
Marker            | Imposta l'indicatore del grafico a linee e del grafico a dispersione. L'intervallo del campo facoltativo `Size` è compreso tra 2 e 72 (il valore predefinito è `5`). Il valore di enumerazione del campo opzionale `Symbol` è (il valore predefinito è `auto`): `circle`, `dash`, `diamond`, `dot`, `none`, `picture`, `plus`, `square`, `star`, `triangle`, `x` e `auto`.
DataLabelPosition | Imposta la posizione dell'etichetta dati della serie di grafici.

Imposta le proprietà della legenda del grafico. Le opzioni che è possibile impostare sono:

Parametro|Tipo|Spiegazione
---|---|---
Position      | `string` | La posizione della legenda del grafico
ShowLegendKey | `bool`   | Impostare le chiavi della legenda che verranno visualizzate nelle etichette dati

Imposta la `Position` della legenda del grafico. La posizione predefinita della legenda è `right`. Questo parametro ha effetto solo quando `None` è `false`. Le posizioni disponibili sono:

Parametro|Spiegazione
---|---
none      | Disabilita legenda
top       | In cima
bottom    | Sul fondo
left      | Sulla sinistra
right     | Sulla destra
top_right | In alto a destra

Il parametro `ShowLegendKey` imposta le chiavi della legenda devono essere mostrate nelle etichette dei dati. Il valore predefinito è `false`.

Il titolo del grafico viene impostato selezionando il parametro `Name` dell'oggetto `Title` e il titolo verrà visualizzato sopra il grafico. Il parametro `Name` supporta l'uso di rappresentazioni di formule, come `Foglio1!$A$1`, se non specifichi il titolo di un'icona, il valore predefinito è null.

Il parametro `ShowBlanksAs` fornisce l'impostazione "Nascondi e svuota celle". Il valore predefinito è: `gap`. Nell'applicazione Excel "la cella vuota viene visualizzata come": "spazio". I seguenti sono valori facoltativi per questo parametro:

Parametro|Spiegazione
---|---
gap  | Spazio
span | Collega i punti dati con linee rette
zero | Valore zero

Imposta la dimensione della bolla in tutte le serie di dati per il grafico a bolle o il grafico a bolle 3D tramite la proprietà `BubbleSizes`. La proprietà `BubbleSizes` è facoltativa. La larghezza predefinita è `100` e il valore deve essere maggiore di 0 e minore o uguale a 300.

Imposta la dimensione del foro della ciambella in tutte le serie di dati per il grafico a ciambella tramite la proprietà `HoleSize`. La proprietà `HoleSize` è facoltativa. La larghezza predefinita è `75` e il valore deve essere maggiore di 0 e inferiore o uguale a 90.

Specifica che ciascun indicatore di dati nella serie ha un colore diverso da `VaryColors`. Il valore predefinito è `true`.

Il parametro `Format` fornisce impostazioni per parametri quali offset del grafico, scala, impostazioni del rapporto d'aspetto e proprietà di stampa, nonché quelli utilizzati nella funzione [`AddPicture`](image.md#AddPicture).

Imposta la posizione dell'area del grafico in base all'area del grafico. Le proprietà che è possibile impostare sono:

Parametro|Tipo|Predefinito|Spiegazione
---|---|---|---
SecondPlotValues | `int`         | `0`     | Specifica i valori nel secondo grafico per il grafico `pieOfPie` e `barOfPie`.
ShowBubbleSize   | `bool`        | `false` | Specifica che la dimensione della bolla deve essere mostrata in un'etichetta dati.
ShowCatName      | `bool`        | `true`  | Nome della categoria.
ShowLeaderLines  | `bool`        | `false` | Specifica che il nome della categoria deve essere mostrato nell'etichetta dati.
ShowPercent      | `bool`        | `false` | Specifica che la percentuale deve essere mostrata in un'etichetta dati.
ShowSerName      | `bool`        | `false` | Specifica che il nome della serie deve essere mostrato in un'etichetta dati.
ShowVal          | `bool`        | `false` | Specifica che il valore deve essere mostrato in un'etichetta dati.
NumFmt           | `ChartNumFmt` | N/A     | Specifica che se collegato all'origine e imposta il codice del formato numerico personalizzato per le etichette dati. La proprietà `NumFmt` è facoltativa. Il codice del formato predefinito è `General`.

Imposta le opzioni dell'asse orizzontale e verticale primario con `XAxis` e `YAxis`.

Le proprietà di `XAxis` che possono essere impostate sono:

Parametro|Tipo|Predefinito|Spiegazione
---|---|---|---
None           | `bool`          | `false` | Disabilitare gli assi.
MajorGridLines | `bool`          | `false` | Specifica le principali linee della griglia.
MinorGridLines | `bool`          | `false` | Specifica le linee della griglia minori.
TickLabelSkip  | `int`           | `1`     | Specifica quante etichette di spunta saltare tra l'etichetta disegnata. La proprietà `TickLabelSkip` è facoltativa. Il valore predefinito è automatico.
ReverseOrder   | `bool`          | `false` | Specifica che le categorie o i valori sono in ordine inverso (orientamento del grafico). La proprietà `ReverseOrder` è facoltativa.
Maximum        | `*float64`      | `0`     | Specifica che il massimo fisso, 0, è automatico. La proprietà massima è facoltativa.
Minimum        | `*float64`      | `0`     | Specifica che il minimo fisso, 0, è automatico. La proprietà minima è facoltativa. Il valore predefinito è automatico.
Font           | `Font`          | N/A     | Specifica il carattere dell'asse orizzontale.
NumFmt         | `ChartNumFmt`   | N/A     | Specifica che se collegato all'origine e imposta il codice del formato numerico personalizzato per l'asse.
Title          | `[]RichTextRun` | N/A     | Specifica il titolo dell'asse orizzontale primario e il ridimensionamento del grafico.

Le proprietà di `YAxis` che possono essere impostate sono:

Parametro|Tipo|Predefinito|Spiegazione
---|---|---|---
None           | `bool`          | `false` | Disabilitare gli assi.
MajorGridLines | `bool`          | `false` | Specifica le principali linee della griglia.
MinorGridLines | `bool`          | `false` | Specifica le linee della griglia minori.
MajorUnit      | `float64`       | `0`     | Specifica la distanza tra i tick principali. Deve contenere un numero a virgola mobile positivo. La proprietà `MajorUnit` è facoltativa. Il valore predefinito è automatico.
ReverseOrder   | `bool`          | `false` | Specifica che le categorie o i valori sono in ordine inverso (orientamento del grafico). La proprietà `ReverseOrder` è facoltativa.
Maximum        | `*float64`      | `0`     | Specifica che il massimo fisso, 0, è automatico. La proprietà massima è facoltativa.
Minimum        | `*float64`      | `0`     | Specifica che il minimo fisso, 0, è automatico. La proprietà minima è facoltativa. Il valore predefinito è automatico.
Font           | `Font`          | N/A     | Specifica il carattere dell'asse verticale.
LogBase        | `float64`       | N/A     | Specifica il numero di base della scala logaritmica dell'asse verticale.
NumFmt         | `ChartNumFmt`   | N/A     | Specifica che se collegato all'origine e imposta il codice del formato numerico personalizzato per l'asse.
Title          | `[]RichTextRun` | N/A     | Specifica il titolo dell'asse verticale primario e il ridimensionamento del grafico.

Imposta la dimensione del grafico tramite la proprietà `Dimension`. La proprietà dimensione è facoltativa. Le proprietà che è possibile impostare sono:

Parametro|Tipo|Predefinito|Spiegazione
---|---|---|---
Height | `uint` | 260 | Altezza
Width  | `uint` | 480 | Larghezza

Il parametro `combo` specifica la creazione di un grafico che combina due o più tipi di grafico in un unico grafico. Ad esempio, crea un grafico a linee e colonne raggruppate con i dati `Foglio1!$E$1:$L$15`:

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
    if err := f.SetSheetName("Sheet1", "Foglio1"); err != nil {
        fmt.Println(err)
        return
    }
    for idx, row := range [][]interface{}{
        {nil, "Mela", "Arancia", "Pera"},
        {"Piccolo", 2, 3, 3},
        {"Normale", 5, 2, 4},
        {"Grande", 6, 7, 8},
    } {
        cell, err := excelize.CoordinatesToCellName(1, idx+1)
        if err != nil {
            fmt.Println(err)
            return
        }
        if err := f.SetSheetRow("Foglio1", cell, &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    enable, disable := true, false
    if err := f.AddChart("Foglio1", "E1", &excelize.Chart{
        Type: excelize.Col,
        Series: []excelize.ChartSeries{
            {
                Name:       "Foglio1!$A$2",
                Categories: "Foglio1!$B$1:$D$1",
                Values:     "Foglio1!$B$2:$D$2",
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
                Text: "Colonne raggruppate - Grafico a linee",
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
                Name:       "Foglio1!$A$4",
                Categories: "Foglio1!$B$1:$D$1",
                Values:     "Foglio1!$B$4:$D$4",
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
    // Salva il foglio di calcolo seguendo il percorso indicato.
    if err := f.SaveAs("Cartel1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Aggiungi foglio grafico {#AddChartSheet}

```go
func (f *File) AddChartSheet(sheet, opts string, combo ...string) error
```

AddChartSheet fornisce il metodo per creare un foglio grafico in base al formato del grafico impostato (come offset, scala, impostazione delle proporzioni e impostazioni di stampa) e alle proprietà impostate. In Excel un foglio grafico è un foglio di lavoro che contiene solo un grafico.

## Elimina grafico {#DeleteChart}

```go
func (f *File) DeleteChart(sheet, cell string) error
```

DeleteChart fornisce una funzione per eliminare il grafico nel foglio di calcolo in base al nome del foglio di lavoro e al riferimento alla cella.
