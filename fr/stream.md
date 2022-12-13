# Écriture en flux

`StreamWriter` a défini le type d'écrivain de flux.

```go
type StreamWriter struct {
    File    *File
    Sheet   string
    SheetID int
    // contient des champs filtrés ou non exportés
}
```

`Cell` peut être utilisée directement dans `StreamWriter.SetRow` pour spécifier un style et une valeur.

```go
type Cell struct {
    StyleID int
    Formula string
    Value   interface{}
}
```

`RowOpts` définit les options de la ligne définie, il peut être utilisé directement dans `StreamWriter.SetRow` pour spécifier le style et les propriétés de la ligne.

```go
type RowOpts struct {
	Height       float64
	Hidden       bool
	StyleID      int
	OutlineLevel int
}
```

## Obtenez le flux écrivain {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter renvoie la structure de l'écrivain de flux par un nom de feuille de calcul donné pour générer une nouvelle feuille de calcul avec de grandes quantités de données. Notez qu'après avoir défini des lignes, vous devez appeler la méthode [`Flush`](stream.md#Flush) pour terminer le processus d'écriture en continu et vous assurer que l'ordre des numéros de ligne est croissant, n'utilisez pas les fonctions de mode normal et les fonctions de mode de flux mélangées à l'écriture de données sur les feuilles de calcul. Par exemple, définissez des données pour la feuille de calcul de taille `102400` lignes x `50` colonnes avec des nombres:

```go
file := excelize.NewFile()
defer func() {
    if err := file.Close(); err != nil {
        fmt.Println(err)
    }
}()
streamWriter, err := file.NewStreamWriter("Sheet1")
if err != nil {
    fmt.Println(err)
}
styleID, err := file.NewStyle(&excelize.Style{Font: &excelize.Font{Color: "#777777"}})
if err != nil {
    fmt.Println(err)
}
if err := streamWriter.SetRow("A1",
    []interface{}{
        excelize.Cell{StyleID: styleID, Value: "Data"},
        []excelize.RichTextRun{
            {Text: "Rich ", Font: &excelize.Font{Color: "2354e8"}},
            {Text: "Text", Font: &excelize.Font{Color: "e83723"}},
        },
    },
    excelize.RowOpts{Height: 45, Hidden: false}); err != nil {
    fmt.Println(err)
}
for rowID := 2; rowID <= 102400; rowID++ {
    row := make([]interface{}, 50)
    for colID := 0; colID < 50; colID++ {
        row[colID] = rand.Intn(640000)
    }
    cell, _ := excelize.CoordinatesToCellName(1, rowID)
    if err := streamWriter.SetRow(cell, row); err != nil {
        fmt.Println(err)
    }
}
if err := streamWriter.Flush(); err != nil {
    fmt.Println(err)
}
if err := file.SaveAs("Book1.xlsx"); err != nil {
    fmt.Println(err)
}
```

Définissez la valeur de la cellule et la formule de la cellule pour une feuille de calcul avec l'écrivain de flux:

```go
err := streamWriter.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1},
    excelize.Cell{Value: 2},
    excelize.Cell{Formula: "SUM(A1,B1)"}});
```

Définissez la valeur de la cellule et le style des lignes d'une feuille de calcul avec le rédacteur de flux:

```go
err := streamWriter.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}},
    excelize.RowOpts{StyleID: styleID, Height: 20, Hidden: false});
```

Définissez la valeur de la cellule et le numéro du niveau hiérarchique de la ligne pour une feuille de calcul avec un rédacteur de flux:

```go
err := streamWriter.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}},
    excelize.RowOpts{StyleID: styleID, Height: 20, Hidden: false, OutlineLevel: 1});
```

## Écrire la ligne de feuille au flux {#SetRow}

```go
func (sw *StreamWriter) SetRow(cell string, values []interface{}, opts ...RowOpts) error
```

SetRow écrit un tableau dans la ligne de flux en fonction de la coordonnée de départ donnée et d'un pointeur vers le type de tableau `slice`. Notez que vous devez appeler la méthode [`Flush`](stream.md#Flush) pour terminer le processus d'écriture en continu.

## Ajouter une table à diffuser {#AddTable}

```go
func (sw *StreamWriter) AddTable(hCell, vCell, opts string) error
```

AddTable crée un tableau Excel pour StreamWriter en utilisant la zone de coordonnées et le jeu de formats donnés.

Exemple 1, créez une table de `A1:D5`:

```go
err := streamWriter.AddTable("A1", "D5", "")
```

Exemple 2, créez une table de `F2:H6` avec le format défini:

```go
err := streamWriter.AddTable("F2", "H6", `{
    "table_name": "table",
    "table_style": "TableStyleMedium2",
    "show_first_column": true,
    "show_last_column": true,
    "show_row_stripes": false,
    "show_column_stripes": true
}`)
```

Notez que le tableau doit comporter au moins deux lignes, y compris l'en-tête. Les cellules d'en-tête doivent contenir des chaînes et doivent être uniques. Actuellement, une seule table est autorisée pour un StreamWriter. [`AddTable`](stream.md#AddTable) doit être appelé après l'écriture des lignes mais avant `Flush`. Voir [`AddTable`](utils.md#AddTable) pour plus de détails sur le format de la table.

## Insérer un saut de page pour diffuser {#InsertPageBreak}

```go
func (sw *StreamWriter) InsertPageBreak(cell string) error
```

InsertPageBreak crée un saut de page pour déterminer où se termine la page imprimée et où commence la suivante par une référence de cellule donnée, le contenu avant le saut de page sera imprimé sur une page et après le saut de page sur une autre.

## Définir les volets pour la diffusion en continu {#SetPanes}

```go
func (sw *StreamWriter) SetPanes(panes string) error
```

SetPanes fournit une fonction pour créer et supprimer des volets de gel et des volets fractionnés en donnant des options de volets pour le `StreamWriter`. Notez que vous devez appeler la fonction `SetPanes` avant la fonction [`SetRow`](stream.md#SetRow).

## Fusionner la cellule pour diffuser {#MergeCell}

```go
func (sw *StreamWriter) MergeCell(hCell, vCell string) error
```

MergeCell fournit une fonction pour fusionner les cellules par une zone de coordonnées donnée pour StreamWriter. Ne créez pas de cellule fusionnée qui chevauche une autre cellule fusionnée existante.

## Définir la largeur de la colonne dans le flux {#SetColWidth}

```go
func (sw *StreamWriter) SetColWidth(min, max int, width float64) error
```

SetColWidth fournit une fonction pour définir la largeur d’une seule colonne ou de plusieurs colonnes pour le `StreamWriter`. Notez que vous devez appeler la fonction `SetColWidth` avant la fonction [`SetRow`](stream.md#SetRow). Par exemple, définissez la colonne de largeur `B:C` comme `20`:

```go
err := streamWriter.SetColWidth(2, 3, 20)
```

## Flush le flux {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush mettant fin au processus d'écriture en streaming.
