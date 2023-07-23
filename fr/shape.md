# Forme

## Ajouter une forme

```go
func (f *File) AddShape(sheet string, opts *Shape) error
```

AddShape fournit la méthode permettant d'ajouter une forme dans une feuille en fonction d'un index de feuille de calcul donné, d'un ensemble de formats de forme (tels que décalage, échelle, paramètres de format et paramètres d'impression) et de propriétés. Par exemple, ajoutez une zone de texte (forme rectale) dans `Sheet1`:

```go
lineWidth := 1.2
err := f.AddShape("Sheet1",
    &excelize.Shape{
        Cell: "G6",
        Type: "rect",
        Line: excelize.ShapeLine{Color: "4286F4", Width: &lineWidth},
        Fill: excelize.Fill{Color: []string{"8EB9FF"}},
        Paragraph: []excelize.RichTextRun{
            {
                Text: "Rectangle Shape",
                Font: &excelize.Font{
                    Bold:      true,
                    Italic:    true,
                    Family:    "Times New Roman",
                    Size:      18,
                    Color:     "777777",
                    Underline: "sng",
                },
            },
        },
        Width:  180,
        Height: 40,
    },
)
```

Ce qui suit montre le type de forme supporté par excelize:

Type|Forme|Style
---|---|---
accentBorderCallout1 | Légende 1 avec bordure et la forme d'accentuation | <p style="text-align: center;"><img src="../images/shapes/accentBorderCallout1.svg" height="50" width="50"></p>
accentBorderCallout2 | Légende 2 avec bordure et la forme d'accentuation | <p style="text-align: center;"><img src="../images/shapes/accentBorderCallout2.svg" height="50" width="50"></p>
accentBorderCallout3 | Légende 3 avec bordure et la forme d'accentuation | <p style="text-align: center;"><img src="../images/shapes/accentBorderCallout3.svg" height="50" width="50"></p>
accentCallout1 | Forme de légende 1 | <p style="text-align: center;"><img src="../images/shapes/accentCallout1.svg" height="50" width="50"></p>
accentCallout2 | Forme de légende 2 | <p style="text-align: center;"><img src="../images/shapes/accentCallout2.svg" height="50" width="50"></p>
accentCallout3 | Forme de légende 3 | <p style="text-align: center;"><img src="../images/shapes/accentCallout3.svg" height="50" width="50"></p>
actionButtonBackPrevious | Forme de bouton précédent | <p style="text-align: center;"><img src="../images/shapes/actionButtonBackPrevious.svg" height="50" width="50"></p>
actionButtonBeginning | Forme de bouton de début | <p style="text-align: center;"><img src="../images/shapes/actionButtonBeginning.svg" height="50" width="50"></p>
actionButtonBlank | Forme bouton vide | <p style="text-align: center;"><img src="../images/shapes/actionButtonBlank.svg" height="50" width="50"></p>
actionButtonDocument | Forme de bouton de document | <p style="text-align: center;"><img src="../images/shapes/actionButtonDocument.svg" height="50" width="50"></p>
actionButtonEnd | Forme de bouton de fin | <p style="text-align: center;"><img src="../images/shapes/actionButtonEnd.svg" height="50" width="50"></p>
actionButtonForwardNext | Transférer ou le bouton suivant de forme | <p style="text-align: center;"><img src="../images/shapes/actionButtonForwardNext.svg" height="50" width="50"></p>
actionButtonHelp | Forme de bouton d'aide | <p style="text-align: center;"><img src="../images/shapes/actionButtonHelp.svg" height="50" width="50"></p>
actionButtonHome | Bouton Accueil forme | <p style="text-align: center;"><img src="../images/shapes/actionButtonHome.svg" height="50" width="50"></p>
actionButtonInformation | Forme de bouton d'informations | <p style="text-align: center;"><img src="../images/shapes/actionButtonInformation.svg" height="50" width="50"></p>
actionButtonMovie | Forme de bouton vidéo | <p style="text-align: center;"><img src="../images/shapes/actionButtonMovie.svg" height="50" width="50"></p>
actionButtonReturn | Retourne la forme du bouton | <p style="text-align: center;"><img src="../images/shapes/actionButtonReturn.svg" height="50" width="50"></p>
actionButtonSound | Forme de son bouton | <p style="text-align: center;"><img src="../images/shapes/actionButtonSound.svg" height="50" width="50"></p>
arc | Forme d'Arc courbé | <p style="text-align: center;"><img src="../images/shapes/arc.svg" height="50" width="50"></p>
bentArrow | Forme de flèche courbée | <p style="text-align: center;"><img src="../images/shapes/bentArrow.svg" height="50" width="50"></p>
bentConnector2 | Forme de connecteur courbé 2 | <p style="text-align: center;"><img src="../images/shapes/bentConnector2.svg" height="50" width="50"></p>
bentConnector3 | Forme de connecteur courbé 3 | <p style="text-align: center;"><img src="../images/shapes/bentConnector3.svg" height="50" width="50"></p>
bentConnector4 | Forme de connecteur courbé 4 | <p style="text-align: center;"><img src="../images/shapes/bentConnector4.svg" height="50" width="50"></p>
bentConnector5 | Forme de connecteur courbé 5 | <p style="text-align: center;"><img src="../images/shapes/bentConnector5.svg" height="50" width="50"></p>
bentUpArrow | Angle droit d'une forme de flèche | <p style="text-align: center;"><img src="../images/shapes/bentUpArrow.svg" height="50" width="50"></p>
bevel | Forme de biseau | <p style="text-align: center;"><img src="../images/shapes/bevel.svg" height="50" width="50"></p>
blockArc | Forme d'Arc de bloc | <p style="text-align: center;"><img src="../images/shapes/blockArc.svg" height="50" width="50"></p>
borderCallout1 | Légende 1 avec la forme de la bordure | <p style="text-align: center;"><img src="../images/shapes/borderCallout1.svg" height="50" width="50"></p>
borderCallout2 | Légende 2 avec la forme de la bordure | <p style="text-align: center;"><img src="../images/shapes/borderCallout2.svg" height="50" width="50"></p>
borderCallout3 | Légende 3 avec la forme de la bordure | <p style="text-align: center;"><img src="../images/shapes/borderCallout3.svg" height="50" width="50"></p>
bracePair | Légende 3 avec la forme de la bordure | <p style="text-align: center;"><img src="../images/shapes/bracePair.svg" height="50" width="50"></p>
bracketPair | Accolade paire forme | <p style="text-align: center;"><img src="../images/shapes/bracketPair.svg" height="50" width="50"></p>
callout1 | Forme de légende 1 | <p style="text-align: center;"><img src="../images/shapes/callout1.svg" height="50" width="50"></p>
callout2 | Forme de légende 2 | <p style="text-align: center;"><img src="../images/shapes/callout2.svg" height="50" width="50"></p>
callout3 | Forme de légende 3 | <p style="text-align: center;"><img src="../images/shapes/callout3.svg" height="50" width="50"></p>
can | La forme peut | <p style="text-align: center;"><img src="../images/shapes/can.svg" height="50" width="50"></p>
chartPlus | Forme ainsi que de graphique | <p style="text-align: center;"><img src="../images/shapes/chartPlus.svg" height="50" width="50"></p>
chartStar | Graphique de forme en étoile | <p style="text-align: center;"><img src="../images/shapes/chartStar.svg" height="50" width="50"></p>
chartX | Forme graphique X | <p style="text-align: center;"><img src="../images/shapes/chartX.svg" height="50" width="50"></p>
chevron | Forme de chevron | <p style="text-align: center;"><img src="../images/shapes/chevron.svg" height="50" width="50"></p>
chord | Forme de corde | <p style="text-align: center;"><img src="../images/shapes/chord.svg" height="50" width="50"></p>
circularArrow | Forme de flèche circulaire | <p style="text-align: center;"><img src="../images/shapes/circularArrow.svg" height="50" width="50"></p>
cloud | Forme de nuage | <p style="text-align: center;"><img src="../images/shapes/cloud.svg" height="50" width="50"></p>
cloudCallout | Forme de nuage de légende | <p style="text-align: center;"><img src="../images/shapes/cloudCallout.svg" height="50" width="50"></p>
corner | Forme angle | <p style="text-align: center;"><img src="../images/shapes/corner.svg" height="50" width="50"></p>
cornerTabs | Forme d'onglets angle | <p style="text-align: center;"><img src="../images/shapes/cornerTabs.svg" height="50" width="50"></p>
cube | Forme de cube | <p style="text-align: center;"><img src="../images/shapes/cube.svg" height="50" width="50"></p>
curvedConnector2 | Connecteur en arc 2 forme | <p style="text-align: center;"><img src="../images/shapes/curvedConnector2.svg" height="50" width="50"></p>
curvedConnector3 | Connecteur en arc 3 forme | <p style="text-align: center;"><img src="../images/shapes/curvedConnector3.svg" height="50" width="50"></p>
curvedConnector4 | Connecteur en arc 4 forme | <p style="text-align: center;"><img src="../images/shapes/curvedConnector4.svg" height="50" width="50"></p>
curvedConnector5 | Connecteur en arc 5 forme | <p style="text-align: center;"><img src="../images/shapes/curvedConnector5.svg" height="50" width="50"></p>
curvedDownArrow | Courbé vers le bas de la forme de flèche | <p style="text-align: center;"><img src="../images/shapes/curvedDownArrow.svg" height="50" width="50"></p>
curvedLeftArrow | Courbé forme de flèche vers la gauche | <p style="text-align: center;"><img src="../images/shapes/curvedLeftArrow.svg" height="50" width="50"></p>
curvedRightArrow | Courbé forme de flèche vers la droite | <p style="text-align: center;"><img src="../images/shapes/curvedRightArrow.svg" height="50" width="50"></p>
curvedUpArrow | Courbé vers le haut la forme de flèche | <p style="text-align: center;"><img src="../images/shapes/curvedUpArrow.svg" height="50" width="50"></p>
decagon | Forme decagon | <p style="text-align: center;"><img src="../images/shapes/decagon.svg" height="50" width="50"></p>
diagStripe | Forme de bande diagonale | <p style="text-align: center;"><img src="../images/shapes/diagStripe.svg" height="50" width="50"></p>
diamond | Forme de losange | <p style="text-align: center;"><img src="../images/shapes/diamond.svg" height="50" width="50"></p>
dodecagon | Forme dodecagon | <p style="text-align: center;"><img src="../images/shapes/dodecagon.svg" height="50" width="50"></p>
donut | Forme café | <p style="text-align: center;"><img src="../images/shapes/donut.svg" height="50" width="50"></p>
doubleWave | Double vague forme | <p style="text-align: center;"><img src="../images/shapes/doubleWave.svg" height="50" width="50"></p>
downArrow | La forme de flèche | <p style="text-align: center;"><img src="../images/shapes/downArrow.svg" height="50" width="50"></p>
downArrowCallout | Forme de flèche vers le bas de la légende | <p style="text-align: center;"><img src="../images/shapes/downArrowCallout.svg" height="50" width="50"></p>
ellipse | Forme de l'ellipse | <p style="text-align: center;"><img src="../images/shapes/ellipse.svg" height="50" width="50"></p>
ellipseRibbon | Forme de ruban ellipse | <p style="text-align: center;"><img src="../images/shapes/ellipseRibbon.svg" height="50" width="50"></p>
ellipseRibbon2 | Forme de ruban 2 ellipse | <p style="text-align: center;"><img src="../images/shapes/ellipseRibbon2.svg" height="50" width="50"></p>
flowChartAlternateProcess | Forme de flux de processus de substitution | <p style="text-align: center;"><img src="../images/shapes/flowChartAlternateProcess.svg" height="50" width="50"></p>
flowChartCollate | Assembler des flux de forme | <p style="text-align: center;"><img src="../images/shapes/flowChartCollate.svg" height="50" width="50"></p>
flowChartConnector | Forme de flux de connecteur| <p style="text-align: center;"><img src="../images/shapes/flowChartConnector.svg" height="50" width="50"></p>
flowChartDecision | Forme de flux de décision | <p style="text-align: center;"><img src="../images/shapes/flowChartDecision.svg" height="50" width="50"></p>
flowChartDelay | Forme de flux de délai d'attente | <p style="text-align: center;"><img src="../images/shapes/flowChartDelay.svg" height="50" width="50"></p>
flowChartDisplay | Afficher la forme de flux | <p style="text-align: center;"><img src="../images/shapes/flowChartDisplay.svg" height="50" width="50"></p>
flowChartDocument | Forme de flux de document | <p style="text-align: center;"><img src="../images/shapes/flowChartDocument.svg" height="50" width="50"></p>
flowChartExtract | Extraire la forme de flux | <p style="text-align: center;"><img src="../images/shapes/flowChartExtract.svg" height="50" width="50"></p>
flowChartInputOutput | Forme de flux d'entrée / sortie | <p style="text-align: center;"><img src="../images/shapes/flowChartInternalStorage.svg" height="50" width="50"></p>
flowChartInternalStorage | Forme de flux de stockage interne | <p style="text-align: center;"><img src="../images/shapes/flowChartInternalStorage.svg" height="50" width="50"></p>
flowChartMagneticDisk | Forme de flux de disque magnétique | <p style="text-align: center;"><img src="../images/shapes/flowChartMagneticDisk.svg" height="50" width="50"></p>
flowChartMagneticDrum | Forme de flux magnétique tambour | <p style="text-align: center;"><img src="../images/shapes/flowChartMagneticDrum.svg" height="50" width="50"></p>
flowChartMagneticTape | Forme de flux de bande magnétique | <p style="text-align: center;"><img src="../images/shapes/flowChartMagneticTape.svg" height="50" width="50"></p>
flowChartManualInput | Forme de flux d'entrée manuelle | <p style="text-align: center;"><img src="../images/shapes/flowChartManualInput.svg" height="50" width="50"></p>
flowChartManualOperation | Forme de flux opération manuelle | <p style="text-align: center;"><img src="../images/shapes/flowChartManualOperation.svg" height="50" width="50"></p>
flowChartMerge | Fusionner des flux de forme | <p style="text-align: center;"><img src="../images/shapes/flowChartMerge.svg" height="50" width="50"></p>
flowChartMultidocument | Forme de flux de documents multiples | <p style="text-align: center;"><img src="../images/shapes/flowChartMultidocument.svg" height="50" width="50"></p>
flowChartOfflineStorage | Forme de flux de stockage en mode hors connexion | <p style="text-align: center;"><img src="../images/shapes/flowChartOfflineStorage.svg" height="50" width="50"></p>
flowChartOffpageConnector | Connecteur hors Page flux de forme | <p style="text-align: center;"><img src="../images/shapes/flowChartOffpageConnector.svg" height="50" width="50"></p>
flowChartOnlineStorage | Forme de flux de stockage en ligne | <p style="text-align: center;"><img src="../images/shapes/flowChartOnlineStorage.svg" height="50" width="50"></p>
flowChartOr | Ou d'une forme de flux | <p style="text-align: center;"><img src="../images/shapes/flowChartOr.svg" height="50" width="50"></p>
flowChartPredefinedProcess | Forme de flux de processus prédéfinis | <p style="text-align: center;"><img src="../images/shapes/flowChartPredefinedProcess.svg" height="50" width="50"></p>
flowChartPreparation | Préparation de la forme de flux | <p style="text-align: center;"><img src="../images/shapes/flowChartPredefinedProcess.svg" height="50" width="50"></p>
flowChartProcess | Forme de flux de processus | <p style="text-align: center;"><img src="../images/shapes/flowChartPreparation.svg" height="50" width="50"></p>
flowChartPunchedCard | Forme de flux de carte perforées | <p style="text-align: center;"><img src="../images/shapes/flowChartPunchedCard.svg" height="50" width="50"></p>
flowChartPunchedTape | Forme de flux de bande perforée | <p style="text-align: center;"><img src="../images/shapes/flowChartPunchedTape.svg" height="50" width="50"></p>
flowChartSort | Forme de flux de tri | <p style="text-align: center;"><img src="../images/shapes/flowChartSort.svg" height="50" width="50"></p>
flowChartSummingJunction | Forme de flux de jonction de sommaire | <p style="text-align: center;"><img src="../images/shapes/flowChartSummingJunction.svg" height="50" width="50"></p>
flowChartTerminator | Forme de flux de terminaison | <p style="text-align: center;"><img src="../images/shapes/flowChartTerminator.svg" height="50" width="50"></p>
foldedCorner | Forme corné | <p style="text-align: center;"><img src="../images/shapes/foldedCorner.svg" height="50" width="50"></p>
frame | Forme de cadre | <p style="text-align: center;"><img src="../images/shapes/frame.svg" height="50" width="50"></p>
funnel | Entonnoir forme | <p style="text-align: center;"><img src="../images/shapes/funnel.svg" height="50" width="50"></p>
gear6 | Forme d'engrenage 6 | <p style="text-align: center;"><img src="../images/shapes/gear6.svg" height="50" width="50"></p>
gear9 | Forme d'engrenage 9 | <p style="text-align: center;"><img src="../images/shapes/gear9.svg" height="50" width="50"></p>
halfFrame | Forme moitié du cadre | <p style="text-align: center;"><img src="../images/shapes/halfFrame.svg" height="50" width="50"></p>
heart | Forme de cœur | <p style="text-align: center;"><img src="../images/shapes/heart.svg" height="50" width="50"></p>
heptagon | Forme sur un heptagone | <p style="text-align: center;"><img src="../images/shapes/heptagon.svg" height="50" width="50"></p>
hexagon | Forme hexagone | <p style="text-align: center;"><img src="../images/shapes/hexagon.svg" height="50" width="50"></p>
homePlate | Forme de plaque d'accueil | <p style="text-align: center;"><img src="../images/shapes/homePlate.svg" height="50" width="50"></p>
horizontalScroll | Forme de défilement horizontale | <p style="text-align: center;"><img src="../images/shapes/horizontalScroll.svg" height="50" width="50"></p>
irregularSeal1 | Forme joint irrégulier 1 | <p style="text-align: center;"><img src="../images/shapes/irregularSeal1.svg" height="50" width="50"></p>
irregularSeal2 | Forme joint irrégulier 2 | <p style="text-align: center;"><img src="../images/shapes/irregularSeal2.svg" height="50" width="50"></p>
leftArrow | Forme de flèche vers la gauche | <p style="text-align: center;"><img src="../images/shapes/leftArrow.svg" height="50" width="50"></p>
leftArrowCallout | Forme de flèche gauche de la légende | <p style="text-align: center;"><img src="../images/shapes/leftArrowCallout.svg" height="50" width="50"></p>
leftBrace | Forme de l'accolade gauche | <p style="text-align: center;"><img src="../images/shapes/leftBrace.svg" height="50" width="50"></p>
leftBracket | Forme crochet gauche | <p style="text-align: center;"><img src="../images/shapes/leftBracket.svg" height="50" width="50"></p>
leftCircularArrow | Forme de flèche circulaire vers la gauche | <p style="text-align: center;"><img src="../images/shapes/leftCircularArrow.svg" height="50" width="50"></p>
leftRightArrow | Forme de flèche gauche et droite | <p style="text-align: center;"><img src="../images/shapes/leftRightArrow.svg" height="50" width="50"></p>
leftRightArrowCallout | Forme de flèche vers la droite de gauche de la légende | <p style="text-align: center;"><img src="../images/shapes/leftRightArrowCallout.svg" height="50" width="50"></p>
leftRightCircularArrow | Forme de flèche droite circulaire gauche | <p style="text-align: center;"><img src="../images/shapes/leftRightCircularArrow.svg" height="50" width="50"></p>
leftRightRibbon | Forme de ruban droite gauche | <p style="text-align: center;"><img src="../images/shapes/leftRightRibbon.svg" height="50" width="50"></p>
leftRightUpArrow | Droit de la forme de flèche à gauche | <p style="text-align: center;"><img src="../images/shapes/leftRightUpArrow.svg" height="50" width="50"></p>
leftUpArrow | Forme de flèche vers la gauche | <p style="text-align: center;"><img src="../images/shapes/leftUpArrow.svg" height="50" width="50"></p>
lightningBolt | Éclair boulon forme | <p style="text-align: center;"><img src="../images/shapes/lightningBolt.svg" height="50" width="50"></p>
line | Forme de trait | <p style="text-align: center;"><img src="../images/shapes/line.svg" height="50" width="50"></p>
lineInv | Forme Inverse de la ligne | <p style="text-align: center;"><img src="../images/shapes/lineInv.svg" height="50" width="50"></p>
mathDivide | Diviser forme Math | <p style="text-align: center;"><img src="../images/shapes/mathDivide.svg" height="50" width="50"></p>
mathEqual | Forme mathématique égale | <p style="text-align: center;"><img src="../images/shapes/mathEqual.svg" height="50" width="50"></p>
mathMinus | Moins de forme Math | <p style="text-align: center;"><img src="../images/shapes/mathMinus.svg" height="50" width="50"></p>
mathMultiply | Multipliez la forme Math | <p style="text-align: center;"><img src="../images/shapes/mathMultiply.svg" height="50" width="50"></p>
mathNotEqual | Forme mathématique différent | <p style="text-align: center;"><img src="../images/shapes/mathNotEqual.svg" height="50" width="50"></p>
mathPlus | De plus, forme Math | <p style="text-align: center;"><img src="../images/shapes/mathPlus.svg" height="50" width="50"></p>
moon | Forme de lune. | <p style="text-align: center;"><img src="../images/shapes/moon.svg" height="50" width="50"></p>
nonIsoscelesTrapezoid | Non-triangle isocèle forme trapézoïdale | <p style="text-align: center;"><img src="../images/shapes/nonIsoscelesTrapezoid.svg" height="50" width="50"></p>
noSmoking | Aucune forme de tabac | <p style="text-align: center;"><img src="../images/shapes/noSmoking.svg" height="50" width="50"></p>
notchedRightArrow | Forme de flèche droite à entaille | <p style="text-align: center;"><img src="../images/shapes/notchedRightArrow.svg" height="50" width="50"></p>
octagon | Forme octogone | <p style="text-align: center;"><img src="../images/shapes/octagon.svg" height="50" width="50"></p>
parallelogram | Parallélogramme à forme | <p style="text-align: center;"><img src="../images/shapes/parallelogram.svg" height="50" width="50"></p>
pentagon | Forme pentagone | <p style="text-align: center;"><img src="../images/shapes/pentagon.svg" height="50" width="50"></p>
pie | Forme en secteurs | <p style="text-align: center;"><img src="../images/shapes/pie.svg" height="50" width="50"></p>
pieWedge | Forme de coins en secteurs | <p style="text-align: center;"><img src="../images/shapes/pieWedge.svg" height="50" width="50"></p>
plaque | Forme d'étiquette | <p style="text-align: center;"><img src="../images/shapes/plaque.svg" height="50" width="50"></p>
plaqueTabs | Forme d'onglets plaque | <p style="text-align: center;"><img src="../images/shapes/plaqueTabs.svg" height="50" width="50"></p>
plus | Plus de forme | <p style="text-align: center;"><img src="../images/shapes/plus.svg" height="50" width="50"></p>
quadArrow | Forme de flèche à quatre | <p style="text-align: center;"><img src="../images/shapes/quadArrow.svg" height="50" width="50"></p>
quadArrowCallout | Forme de légende avec flèche à quatre cœurs | <p style="text-align: center;"><img src="../images/shapes/quadArrowCallout.svg" height="50" width="50"></p>
rect | Forme de rectangle | <p style="text-align: center;"><img src="../images/shapes/rect.svg" height="50" width="50"></p>
ribbon | Forme de ruban | <p style="text-align: center;"><img src="../images/shapes/ribbon.svg" height="50" width="50"></p>
ribbon2 | Forme de ruban 2 | <p style="text-align: center;"><img src="../images/shapes/ribbon2.svg" height="50" width="50"></p>
rightArrow | Forme de flèche vers la droite | <p style="text-align: center;"><img src="../images/shapes/rightArrow.svg" height="50" width="50"></p>
rightArrowCallout | Forme de flèche droite de la légende | <p style="text-align: center;"><img src="../images/shapes/rightArrowCallout.svg" height="50" width="50"></p>
rightBrace | Forme de l'accolade droite | <p style="text-align: center;"><img src="../images/shapes/rightBrace.svg" height="50" width="50"></p>
rightBracket | Forme de parenthèse fermante | <p style="text-align: center;"><img src="../images/shapes/rightBracket.svg" height="50" width="50"></p>
round1Rect | Une forme de Rectangle arrondi angle | <p style="text-align: center;"><img src="../images/shapes/round1Rect.svg" height="50" width="50"></p>
round2DiagRect | Forme de Rectangle deux coin arrondi Diagonal | <p style="text-align: center;"><img src="../images/shapes/round2DiagRect.svg" height="50" width="50"></p>
round2SameRect | Forme de Rectangle deux coin arrondi même côté | <p style="text-align: center;"><img src="../images/shapes/round2SameRect.svg" height="50" width="50"></p>
roundRect | Forme de Rectangle arrondi angle | <p style="text-align: center;"><img src="../images/shapes/roundRect.svg" height="50" width="50"></p>
rtTriangle | Forme Triangle rectangle | <p style="text-align: center;"><img src="../images/shapes/rtTriangle.svg" height="50" width="50"></p>
smileyFace | Forme de Face émoticônes | <p style="text-align: center;"><img src="../images/shapes/smileyFace.svg" height="50" width="50"></p>
snip1Rect | Capture d'une forme de Rectangle angle | <p style="text-align: center;"><img src="../images/shapes/snip1Rect.svg" height="50" width="50"></p>
snip2DiagRect | Forme de Rectangle coin deux rogner en diagonale | <p style="text-align: center;"><img src="../images/shapes/snip2DiagRect.svg" height="50" width="50"></p>
snip2SameRect | Forme de Rectangle coin deux rogner même côté | <p style="text-align: center;"><img src="../images/shapes/snip2SameRect.svg" height="50" width="50"></p>
snipRoundRect | Un rogner une forme de Rectangle coin arrondi | <p style="text-align: center;"><img src="../images/shapes/snipRoundRect.svg" height="50" width="50"></p>
squareTabs | Forme de tabulations carrées | <p style="text-align: center;"><img src="../images/shapes/squareTabs.svg" height="50" width="50"></p>
star10 | Dix pointe forme en étoile | <p style="text-align: center;"><img src="../images/shapes/star10.svg" height="50" width="50"></p>
star12 | Étoile à douze branches | <p style="text-align: center;"><img src="../images/shapes/star12.svg" height="50" width="50"></p>
star16 | Étoile à seize branches | <p style="text-align: center;"><img src="../images/shapes/star16.svg" height="50" width="50"></p>
star24 | Vingt quatre vers laquelle pointe la forme en étoile | <p style="text-align: center;"><img src="../images/shapes/star24.svg" height="50" width="50"></p>
star32 | Trente deux vers laquelle pointe la forme en étoile | <p style="text-align: center;"><img src="../images/shapes/star32.svg" height="50" width="50"></p>
star4 | Quatre pointes de forme en étoile | <p style="text-align: center;"><img src="../images/shapes/star4.svg" height="50" width="50"></p>
star5 | Cinq pointe forme en étoile | <p style="text-align: center;"><img src="../images/shapes/star5.svg" height="50" width="50"></p>
star6 | Étoile à six branches | <p style="text-align: center;"><img src="../images/shapes/star6.svg" height="50" width="50"></p>
star7 | Sept pointe forme en étoile | <p style="text-align: center;"><img src="../images/shapes/star7.svg" height="50" width="50"></p>
star8 | Étoile à huit branches | <p style="text-align: center;"><img src="../images/shapes/star8.svg" height="50" width="50"></p>
straightConnector1 | Forme de connecteur droit 1 | <p style="text-align: center;"><img src="../images/shapes/straightConnector1.svg" height="50" width="50"></p>
stripedRightArrow | Agrégés par bandes forme de flèche vers la droite | <p style="text-align: center;"><img src="../images/shapes/stripedRightArrow.svg" height="50" width="50"></p>
sun | Forme Sun | <p style="text-align: center;"><img src="../images/shapes/sun.svg" height="50" width="50"></p>
swooshArrow | Coup de pinceau forme de flèche | <p style="text-align: center;"><img src="../images/shapes/swooshArrow.svg" height="50" width="50"></p>
teardrop | Forme de larme | <p style="text-align: center;"><img src="../images/shapes/teardrop.svg" height="50" width="50"></p>
trapezoid | Forme trapézoïdale | <p style="text-align: center;"><img src="../images/shapes/trapezoid.svg" height="50" width="50"></p>
triangle | Forme de triangle | <p style="text-align: center;"><img src="../images/shapes/triangle.svg" height="50" width="50"></p>
upArrow | Forme de flèche | <p style="text-align: center;"><img src="../images/shapes/upArrow.svg" height="50" width="50"></p>
upArrowCallout | Forme de flèche vers le haut de la légende | <p style="text-align: center;"><img src="../images/shapes/upArrowCallout.svg" height="50" width="50"></p>
upDownArrow | La forme de flèche vers le haut | <p style="text-align: center;"><img src="../images/shapes/upDownArrow.svg" height="50" width="50"></p>
upDownArrowCallout | Haut de la légende forme de flèche vers le bas | <p style="text-align: center;"><img src="../images/shapes/upDownArrowCallout.svg" height="50" width="50"></p>
uturnArrow | Forme de flèche demi-tour en u | <p style="text-align: center;"><img src="../images/shapes/uturnArrow.svg" height="50" width="50"></p>
verticalScroll | Forme de défilement verticale | <p style="text-align: center;"><img src="../images/shapes/verticalScroll.svg" height="50" width="50"></p>
wave | Forme de vague | <p style="text-align: center;"><img src="../images/shapes/wave.svg" height="50" width="50"></p>
wedgeEllipseCallout | Forme de légende coins Ellipse | <p style="text-align: center;"><img src="../images/shapes/wedgeEllipseCallout.svg" height="50" width="50"></p>
wedgeRectCallout | Forme de légende triangle Rectangle | <p style="text-align: center;"><img src="../images/shapes/wedgeRectCallout.svg" height="50" width="50"></p>
wedgeRoundRectCallout | Légende des coins arrondis forme Rectangle | <p style="text-align: center;"><img src="../images/shapes/wedgeRoundRectCallout.svg" height="50" width="50"></p>
