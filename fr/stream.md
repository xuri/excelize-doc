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

NewStreamWriter renvoie la structure d'écriture de flux par le nom de feuille de calcul donné utilisé pour écrire des données sur une nouvelle feuille de calcul vide existante avec de grandes quantités de données. Notez qu'après avoir écrit des données avec l'écrivain de flux pour la feuille de calcul, vous devez appeler la méthode [`Flush`](stream.md#Flush) pour mettre fin au processus d'écriture en continu, vous assurer que l'ordre des numéros de ligne est croissant lorsque vous définissez des lignes, et les fonctions de mode normal et les fonctions de mode flux ne peut pas être un travail mélangé à l'écriture de données sur les feuilles de calcul. Le rédacteur de flux essaiera d'utiliser des fichiers temporaires sur le disque pour réduire l'utilisation de la mémoire lorsque les données en mémoire dépassent 16 Mo, et vous ne pouvez pas obtenir la valeur de la cellule pour le moment. Par exemple, définissez des données pour une feuille de calcul de taille `102400` lignes x `50` colonnes avec des nombres et un style:

```go
f := excelize.NewFile()
defer func() {
    if err := f.Close(); err != nil {
        fmt.Println(err)
    }
}()
sw, err := f.NewStreamWriter("Sheet1")
if err != nil {
    fmt.Println(err)
    return
}
styleID, err := f.NewStyle(&excelize.Style{Font: &excelize.Font{Color: "777777"}})
if err != nil {
    fmt.Println(err)
    return
}
if err := sw.SetRow("A1",
    []interface{}{
        excelize.Cell{StyleID: styleID, Value: "Data"},
        []excelize.RichTextRun{
            {Text: "Rich ", Font: &excelize.Font{Color: "2354E8"}},
            {Text: "Text", Font: &excelize.Font{Color: "E83723"}},
        },
    },
    excelize.RowOpts{Height: 45, Hidden: false}); err != nil {
    fmt.Println(err)
    return
}
for rowID := 2; rowID <= 102400; rowID++ {
    row := make([]interface{}, 50)
    for colID := 0; colID < 50; colID++ {
        row[colID] = rand.Intn(640000)
    }
    cell, err := excelize.CoordinatesToCellName(1, rowID)
    if err != nil {
        fmt.Println(err)
        break
    }
    if err := sw.SetRow(cell, row); err != nil {
        fmt.Println(err)
        break
    }
}
if err := sw.Flush(); err != nil {
    fmt.Println(err)
    return
}
if err := f.SaveAs("Book1.xlsx"); err != nil {
    fmt.Println(err)
}
```

Définissez la valeur de la cellule et la formule de la cellule pour une feuille de calcul avec l'écrivain de flux:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1},
    excelize.Cell{Value: 2},
    excelize.Cell{Formula: "SUM(A1,B1)"}})
```

Définissez la valeur de la cellule et le style des lignes d'une feuille de calcul avec le rédacteur de flux:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}},
    excelize.RowOpts{StyleID: styleID, Height: 20, Hidden: false})
```

Définissez la valeur de la cellule et le niveau de contour de la ligne pour une feuille de calcul avec un rédacteur de flux:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}}, excelize.RowOpts{OutlineLevel: 1})
```

## Écrire la ligne de feuille au flux {#SetRow}

```go
func (sw *StreamWriter) SetRow(cell string, values []interface{}, opts ...RowOpts) error
```

SetRow écrit un tableau dans la ligne de flux en fonction de la coordonnée de départ donnée et d'un pointeur vers le type de tableau `slice`. Notez que vous devez appeler la méthode [`Flush`](stream.md#Flush) pour terminer le processus d'écriture en continu.

## Ajouter une table à diffuser {#AddTable}

```go
func (sw *StreamWriter) AddTable(table *Table) error
```

AddTable crée un tableau Excel pour StreamWriter en utilisant la zone de coordonnées et le jeu de formats donnés.

Exemple 1, créez une table de `A1:D5`:

```go
err := sw.AddTable(&excelize.Table{Range: "A1:D5"})
```

Exemple 2, créez une table de `F2:H6` avec le format défini:

```go
disable := false
err := sw.AddTable(&excelize.Table{
    Range:             "F2:H6",
    Name:              "table",
    StyleName:         "TableStyleMedium2",
    ShowFirstColumn:   true,
    ShowLastColumn:    true,
    ShowRowStripes:    &disable,
    ShowColumnStripes: true,
})
```

Notez que le tableau doit comporter au moins deux lignes, y compris l'en-tête. Les cellules d'en-tête doivent contenir des chaînes et doivent être uniques. Actuellement, une seule table est autorisée pour un `StreamWriter`. [`AddTable`](stream.md#AddTable) doit être appelé après l'écriture des lignes mais avant `Flush`. Voir [`AddTable`](utils.md#AddTable) pour plus de détails sur le format de la table.

## Insérer un saut de page pour diffuser {#InsertPageBreak}

```go
func (sw *StreamWriter) InsertPageBreak(cell string) error
```

InsertPageBreak crée un saut de page pour déterminer où se termine la page imprimée et où commence la suivante par une référence de cellule donnée, le contenu avant le saut de page sera imprimé sur une page et après le saut de page sur une autre.

## Définir les volets pour la diffusion en continu {#SetPanes}

```go
func (sw *StreamWriter) SetPanes(panes *Panes) error
```

SetPanes fournit une fonction pour créer et supprimer des volets de gel et des volets fractionnés en donnant des options de volets pour le `StreamWriter`. Notez que vous devez appeler la fonction `SetPanes` avant la fonction [`SetRow`](stream.md#SetRow).

## Fusionner la cellule pour diffuser {#MergeCell}

```go
func (sw *StreamWriter) MergeCell(topLeftCell, bottomRightCell string) error
```

MergeCell fournit une fonction pour fusionner les cellules par une zone de coordonnées donnée pour `StreamWriter`. Ne créez pas de cellule fusionnée qui chevauche une autre cellule fusionnée existante.

## Définir le contour des colonnes dans le flux {#SetColOutlineLevel}

```go
func (sw *StreamWriter) SetColOutlineLevel(col int, level uint8) error
```

La fonction SetColOutlineLevel permet de définir le niveau de plan d'une colonne du `StreamWriter`. Le paramètre `level` peut prendre les valeurs de 1 à 7. Il est impératif d'appeler la fonction `SetColOutlineLevel` avant la fonction [`SetRow`](stream.md#SetRow). Par exemple, pour définir le niveau de plan de la colonne `D` à 2:

```go
err := sw.SetColOutlineLevel(4, 2)
```

## Définir le style de colonne dans le flux {#SetColStyle}

```go
func (sw *StreamWriter) SetColStyle(minVal, maxVal, styleID int) error
```

SetColStyle fournit une fonction permettant de définir le style d'une colonne unique ou de plusieurs colonnes pour `StreamWriter`. Notez que vous devez appeler la fonction `SetColStyle` avant la fonction [`SetRow`](stream.md#SetRow). Par exemple, définissez le style de la colonne `H`:

```go
err := sw.SetColStyle(8, 8, style)
```

## Définir la visibilité des colonnes dans le flux {#SetColVisible}

```go
func (sw *StreamWriter) SetColVisible(minVal, maxVal int, visible bool) error
```

La fonction SetColVisible permet de définir la visibilité d'une ou plusieurs colonnes pour le `StreamWriter`. Notez qu'il est impératif d'appeler la fonction `SetColVisible` avant la fonction [`SetRow`](stream.md#SetRow). Par exemple, pour masquer la colonne `D`:

```go
err := sw.SetColVisible(4, 4, false)
```

Masquer les colonnes de `D` à `F` (incluses):

```go
err := sw.SetColVisible(4, 6, false)
```

## Définir la largeur de la colonne dans le flux {#SetColWidth}

```go
func (sw *StreamWriter) SetColWidth(min, max int, width float64) error
```

SetColWidth fournit une fonction pour définir la largeur d'une seule colonne ou de plusieurs colonnes pour le `StreamWriter`. Notez que vous devez appeler la fonction `SetColWidth` avant la fonction [`SetRow`](stream.md#SetRow). Par exemple, définissez la colonne de largeur `B:C` comme `20`:

```go
err := sw.SetColWidth(2, 3, 20)
```

## Flush le flux {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush mettant fin au processus d'écriture en streaming.
