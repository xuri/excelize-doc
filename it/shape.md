# Forma

## Aggiungi forma

```go
func (f *File) AddShape(sheet string, opts *Shape) error
```

AddShape fornisce il metodo per aggiungere forma in un foglio in base all'indice del foglio di lavoro, al formato della forma impostato (come offset, scala, impostazione delle proporzioni e impostazioni di stampa) e alle proprietà impostate. Ad esempio, aggiungi una casella di testo (forma rettangolare) in `Foglio1`:

```go
lineWidth := 1.2
err := f.AddShape("Foglio1",
    &excelize.Shape{
        Cell: "G6",
        Type: "rect",
        Line: excelize.ShapeLine{Color: "4286F4", Width: &lineWidth},
        Fill: excelize.Fill{Color: []string{"8EB9FF"}},
        Paragraph: []excelize.RichTextRun{
            {
                Text: "Forma rettangolare",
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

Di seguito viene mostrato il tipo di forma supportata da Excelize:

Tipo|Forma|Anteprima
---|---|---
accentBorderCallout1 | Callout 1 con bordo e forma accentuata | <p style="text-align: center;"><img src="../images/shapes/accentBorderCallout1.svg" height="50" width="50"></p>
accentBorderCallout2 | Callout 2 con bordo e forma accentuata | <p style="text-align: center;"><img src="../images/shapes/accentBorderCallout2.svg" height="50" width="50"></p>
accentBorderCallout3 | Callout 3 con bordo e forma accentuata | <p style="text-align: center;"><img src="../images/shapes/accentBorderCallout3.svg" height="50" width="50"></p>
accentCallout1 | Richiamo 1 Forma | <p style="text-align: center;"><img src="../images/shapes/accentCallout1.svg" height="50" width="50"></p>
accentCallout2 | Richiamo 2 Forma | <p style="text-align: center;"><img src="../images/shapes/accentCallout2.svg" height="50" width="50"></p>
accentCallout3 | Richiamo 3 Forma | <p style="text-align: center;"><img src="../images/shapes/accentCallout3.svg" height="50" width="50"></p>
actionButtonBackPrevious | Forma del pulsante Indietro o Precedente | <p style="text-align: center;"><img src="../images/shapes/actionButtonBackPrevious.svg" height="50" width="50"></p>
actionButtonBeginning | Forma del pulsante iniziale | <p style="text-align: center;"><img src="../images/shapes/actionButtonBeginning.svg" height="50" width="50"></p>
actionButtonBlank | Forma del pulsante vuoto | <p style="text-align: center;"><img src="../images/shapes/actionButtonBlank.svg" height="50" width="50"></p>
actionButtonDocument | Forma del pulsante del documento | <p style="text-align: center;"><img src="../images/shapes/actionButtonDocument.svg" height="50" width="50"></p>
actionButtonEnd | Forma del pulsante finale | <p style="text-align: center;"><img src="../images/shapes/actionButtonEnd.svg" height="50" width="50"></p>
actionButtonForwardNext | Forma del pulsante Avanti o Avanti | <p style="text-align: center;"><img src="../images/shapes/actionButtonForwardNext.svg" height="50" width="50"></p>
actionButtonHelp | Forma del pulsante di aiuto | <p style="text-align: center;"><img src="../images/shapes/actionButtonHelp.svg" height="50" width="50"></p>
actionButtonHome | Forma del pulsante Home | <p style="text-align: center;"><img src="../images/shapes/actionButtonHome.svg" height="50" width="50"></p>
actionButtonInformation | Forma del pulsante informativo | <p style="text-align: center;"><img src="../images/shapes/actionButtonInformation.svg" height="50" width="50"></p>
actionButtonMovie | Forma del pulsante del film | <p style="text-align: center;"><img src="../images/shapes/actionButtonMovie.svg" height="50" width="50"></p>
actionButtonReturn | Forma del pulsante di ritorno | <p style="text-align: center;"><img src="../images/shapes/actionButtonReturn.svg" height="50" width="50"></p>
actionButtonSound | Forma del pulsante sonoro | <p style="text-align: center;"><img src="../images/shapes/actionButtonSound.svg" height="50" width="50"></p>
arc | Forma ad arco curvo | <p style="text-align: center;"><img src="../images/shapes/arc.svg" height="50" width="50"></p>
bentArrow | Forma di freccia piegata | <p style="text-align: center;"><img src="../images/shapes/bentArrow.svg" height="50" width="50"></p>
bentConnector2 | Forma del connettore piegato 2 | <p style="text-align: center;"><img src="../images/shapes/bentConnector2.svg" height="50" width="50"></p>
bentConnector3 | Forma del connettore piegato 3 | <p style="text-align: center;"><img src="../images/shapes/bentConnector3.svg" height="50" width="50"></p>
bentConnector4 | Forma del connettore piegato 4 | <p style="text-align: center;"><img src="../images/shapes/bentConnector4.svg" height="50" width="50"></p>
bentConnector5 | Forma del connettore piegato 5 | <p style="text-align: center;"><img src="../images/shapes/bentConnector5.svg" height="50" width="50"></p>
bentUpArrow | Forma di freccia piegata | <p style="text-align: center;"><img src="../images/shapes/bentUpArrow.svg" height="50" width="50"></p>
bevel | Forma smussata | <p style="text-align: center;"><img src="../images/shapes/bevel.svg" height="50" width="50"></p>
blockArc | Blocco a forma di arco | <p style="text-align: center;"><img src="../images/shapes/blockArc.svg" height="50" width="50"></p>
borderCallout1 | Richiamo 1 con forma del bordo | <p style="text-align: center;"><img src="../images/shapes/borderCallout1.svg" height="50" width="50"></p>
borderCallout2 | Richiamo 2 con forma del bordo | <p style="text-align: center;"><img src="../images/shapes/borderCallout2.svg" height="50" width="50"></p>
borderCallout3 | Richiamo 3 con forma del bordo | <p style="text-align: center;"><img src="../images/shapes/borderCallout3.svg" height="50" width="50"></p>
bracePair | Forma della coppia di parentesi graffe | <p style="text-align: center;"><img src="../images/shapes/bracePair.svg" height="50" width="50"></p>
bracketPair | Forma della coppia di staffe | <p style="text-align: center;"><img src="../images/shapes/bracketPair.svg" height="50" width="50"></p>
callout1 | Richiamo 1 Forma | <p style="text-align: center;"><img src="../images/shapes/callout1.svg" height="50" width="50"></p>
callout2 | Richiamo 2 Forma | <p style="text-align: center;"><img src="../images/shapes/callout2.svg" height="50" width="50"></p>
callout3 | Richiamo 3 Forma | <p style="text-align: center;"><img src="../images/shapes/callout3.svg" height="50" width="50"></p>
can | Può modellare | <p style="text-align: center;"><img src="../images/shapes/can.svg" height="50" width="50"></p>
chartPlus | Grafico più forma | <p style="text-align: center;"><img src="../images/shapes/chartPlus.svg" height="50" width="50"></p>
chartStar | Grafico a forma di stella | <p style="text-align: center;"><img src="../images/shapes/chartStar.svg" height="50" width="50"></p>
chartX | Grafico a forma di X | <p style="text-align: center;"><img src="../images/shapes/chartX.svg" height="50" width="50"></p>
chevron | Forma Chevron | <p style="text-align: center;"><img src="../images/shapes/chevron.svg" height="50" width="50"></p>
chord | Forma dell'accordo | <p style="text-align: center;"><img src="../images/shapes/chord.svg" height="50" width="50"></p>
circularArrow | Forma di freccia circolare | <p style="text-align: center;"><img src="../images/shapes/circularArrow.svg" height="50" width="50"></p>
cloud | Forma di nuvola | <p style="text-align: center;"><img src="../images/shapes/cloud.svg" height="50" width="50"></p>
cloudCallout | Forma di nuvola di richiamo | <p style="text-align: center;"><img src="../images/shapes/cloudCallout.svg" height="50" width="50"></p>
corner | Forma d'angolo | <p style="text-align: center;"><img src="../images/shapes/corner.svg" height="50" width="50"></p>
cornerTabs | Forma delle linguette angolari | <p style="text-align: center;"><img src="../images/shapes/cornerTabs.svg" height="50" width="50"></p>
cube | Forma cubica | <p style="text-align: center;"><img src="../images/shapes/cube.svg" height="50" width="50"></p>
curvedConnector2 | Forma del connettore curvo 2 | <p style="text-align: center;"><img src="../images/shapes/curvedConnector2.svg" height="50" width="50"></p>
curvedConnector3 | Forma del connettore curvo 3 | <p style="text-align: center;"><img src="../images/shapes/curvedConnector3.svg" height="50" width="50"></p>
curvedConnector4 | Forma del connettore curvo 4 | <p style="text-align: center;"><img src="../images/shapes/curvedConnector4.svg" height="50" width="50"></p>
curvedConnector5 | Forma del connettore curvo 5 | <p style="text-align: center;"><img src="../images/shapes/curvedConnector5.svg" height="50" width="50"></p>
curvedDownArrow | Forma di freccia curva verso il basso | <p style="text-align: center;"><img src="../images/shapes/curvedDownArrow.svg" height="50" width="50"></p>
curvedLeftArrow | Forma di freccia sinistra curva | <p style="text-align: center;"><img src="../images/shapes/curvedLeftArrow.svg" height="50" width="50"></p>
curvedRightArrow | Forma curva della freccia destra | <p style="text-align: center;"><img src="../images/shapes/curvedRightArrow.svg" height="50" width="50"></p>
curvedUpArrow | Forma di freccia curva verso l'alto | <p style="text-align: center;"><img src="../images/shapes/curvedUpArrow.svg" height="50" width="50"></p>
decagon | Forma decagonale | <p style="text-align: center;"><img src="../images/shapes/decagon.svg" height="50" width="50"></p>
diagStripe | Forma a strisce diagonali | <p style="text-align: center;"><img src="../images/shapes/diagStripe.svg" height="50" width="50"></p>
diamond | Forma di diamante | <p style="text-align: center;"><img src="../images/shapes/diamond.svg" height="50" width="50"></p>
dodecagon | Forma dodecagonale | <p style="text-align: center;"><img src="../images/shapes/dodecagon.svg" height="50" width="50"></p>
donut | Forma di ciambella | <p style="text-align: center;"><img src="../images/shapes/donut.svg" height="50" width="50"></p>
doubleWave | Forma a doppia onda | <p style="text-align: center;"><img src="../images/shapes/doubleWave.svg" height="50" width="50"></p>
downArrow | Forma della freccia verso il basso | <p style="text-align: center;"><img src="../images/shapes/downArrow.svg" height="50" width="50"></p>
downArrowCallout | Forma della freccia rivolta verso il basso | <p style="text-align: center;"><img src="../images/shapes/downArrowCallout.svg" height="50" width="50"></p>
ellipse | Forma ellittica | <p style="text-align: center;"><img src="../images/shapes/ellipse.svg" height="50" width="50"></p>
ellipseRibbon | Forma del nastro ellittico| <p style="text-align: center;"><img src="../images/shapes/ellipseRibbon.svg" height="50" width="50"></p>
ellipseRibbon2 | Forma del nastro ellittico 2 | <p style="text-align: center;"><img src="../images/shapes/ellipseRibbon2.svg" height="50" width="50"></p>
flowChartAlternateProcess | Forma del flusso del processo alternativo | <p style="text-align: center;"><img src="../images/shapes/flowChartAlternateProcess.svg" height="50" width="50"></p>
flowChartCollate | Raccogli la forma del flusso | <p style="text-align: center;"><img src="../images/shapes/flowChartCollate.svg" height="50" width="50"></p>
flowChartConnector | Forma del flusso del connettore | <p style="text-align: center;"><img src="../images/shapes/flowChartConnector.svg" height="50" width="50"></p>
flowChartDecision | Forma del flusso decisionale | <p style="text-align: center;"><img src="../images/shapes/flowChartDecision.svg" height="50" width="50"></p>
flowChartDelay | Ritarda la forma del flusso | <p style="text-align: center;"><img src="../images/shapes/flowChartDelay.svg" height="50" width="50"></p>
flowChartDisplay | Visualizza la forma del flusso | <p style="text-align: center;"><img src="../images/shapes/flowChartDisplay.svg" height="50" width="50"></p>
flowChartDocument | Forma del flusso di documenti | <p style="text-align: center;"><img src="../images/shapes/flowChartDocument.svg" height="50" width="50"></p>
flowChartExtract | Estrai forma del flusso | <p style="text-align: center;"><img src="../images/shapes/flowChartExtract.svg" height="50" width="50"></p>
flowChartInputOutput | Forma del flusso di ingresso e uscita | <p style="text-align: center;"><img src="../images/shapes/flowChartInternalStorage.svg" height="50" width="50"></p>
flowChartInternalStorage | Forma del flusso di archiviazione interna | <p style="text-align: center;"><img src="../images/shapes/flowChartInternalStorage.svg" height="50" width="50"></p>
flowChartMagneticDisk | Forma del flusso del disco magnetico | <p style="text-align: center;"><img src="../images/shapes/flowChartMagneticDisk.svg" height="50" width="50"></p>
flowChartMagneticDrum | Forma del flusso del tamburo magnetico | <p style="text-align: center;"><img src="../images/shapes/flowChartMagneticDrum.svg" height="50" width="50"></p>
flowChartMagneticTape | Forma del flusso del nastro magnetico | <p style="text-align: center;"><img src="../images/shapes/flowChartMagneticTape.svg" height="50" width="50"></p>
flowChartManualInput | Forma del flusso di input manuale | <p style="text-align: center;"><img src="../images/shapes/flowChartManualInput.svg" height="50" width="50"></p>
flowChartManualOperation | Forma del flusso del funzionamento manuale | <p style="text-align: center;"><img src="../images/shapes/flowChartManualOperation.svg" height="50" width="50"></p>
flowChartMerge | Unisci forma di flusso | <p style="text-align: center;"><img src="../images/shapes/flowChartMerge.svg" height="50" width="50"></p>
flowChartMultidocument | Forma del flusso multi-documento | <p style="text-align: center;"><img src="../images/shapes/flowChartMultidocument.svg" height="50" width="50"></p>
flowChartOfflineStorage | Forma del flusso di archiviazione offline | <p style="text-align: center;"><img src="../images/shapes/flowChartOfflineStorage.svg" height="50" width="50"></p>
flowChartOffpageConnector | Forma del flusso del connettore fuori pagina | <p style="text-align: center;"><img src="../images/shapes/flowChartOffpageConnector.svg" height="50" width="50"></p>
flowChartOnlineStorage | Forma del flusso di archiviazione online | <p style="text-align: center;"><img src="../images/shapes/flowChartOnlineStorage.svg" height="50" width="50"></p>
flowChartOr | O forma del flusso | <p style="text-align: center;"><img src="../images/shapes/flowChartOr.svg" height="50" width="50"></p>
flowChartPredefinedProcess | Forma del flusso di processo predefinita | <p style="text-align: center;"><img src="../images/shapes/flowChartPredefinedProcess.svg" height="50" width="50"></p>
flowChartPreparation | Forma del flusso di preparazione | <p style="text-align: center;"><img src="../images/shapes/flowChartPredefinedProcess.svg" height="50" width="50"></p>
flowChartProcess | Forma del flusso del processo | <p style="text-align: center;"><img src="../images/shapes/flowChartPreparation.svg" height="50" width="50"></p>
flowChartPunchedCard | Forma del flusso della carta perforata | <p style="text-align: center;"><img src="../images/shapes/flowChartPunchedCard.svg" height="50" width="50"></p>
flowChartPunchedTape | Forma di flusso del nastro perforato | <p style="text-align: center;"><img src="../images/shapes/flowChartPunchedTape.svg" height="50" width="50"></p>
flowChartSort | Ordina la forma del flusso | <p style="text-align: center;"><img src="../images/shapes/flowChartSort.svg" height="50" width="50"></p>
flowChartSummingJunction | Forma del flusso della giunzione sommatrice | <p style="text-align: center;"><img src="../images/shapes/flowChartSummingJunction.svg" height="50" width="50"></p>
flowChartTerminator | Forma del flusso del terminatore | <p style="text-align: center;"><img src="../images/shapes/flowChartTerminator.svg" height="50" width="50"></p>
foldedCorner | Forma ad angolo piegato | <p style="text-align: center;"><img src="../images/shapes/foldedCorner.svg" height="50" width="50"></p>
frame | Forma del telaio | <p style="text-align: center;"><img src="../images/shapes/frame.svg" height="50" width="50"></p>
funnel | Forma ad imbuto | <p style="text-align: center;"><img src="../images/shapes/funnel.svg" height="50" width="50"></p>
gear6 | Forma dell'ingranaggio 6 | <p style="text-align: center;"><img src="../images/shapes/gear6.svg" height="50" width="50"></p>
gear9 | Forma dell'ingranaggio 9 | <p style="text-align: center;"><img src="../images/shapes/gear9.svg" height="50" width="50"></p>
halfFrame | Forma a mezza cornice | <p style="text-align: center;"><img src="../images/shapes/halfFrame.svg" height="50" width="50"></p>
heart | A forma di cuore | <p style="text-align: center;"><img src="../images/shapes/heart.svg" height="50" width="50"></p>
heptagon | Forma ettagonale | <p style="text-align: center;"><img src="../images/shapes/heptagon.svg" height="50" width="50"></p>
hexagon | Forma esagonale | <p style="text-align: center;"><img src="../images/shapes/hexagon.svg" height="50" width="50"></p>
homePlate | Forma del piatto domestico | <p style="text-align: center;"><img src="../images/shapes/homePlate.svg" height="50" width="50"></p>
horizontalScroll | Forma di scorrimento orizzontale | <p style="text-align: center;"><img src="../images/shapes/horizontalScroll.svg" height="50" width="50"></p>
irregularSeal1 | Forma del sigillo irregolare 1 | <p style="text-align: center;"><img src="../images/shapes/irregularSeal1.svg" height="50" width="50"></p>
irregularSeal2 | Forma del sigillo irregolare 2 | <p style="text-align: center;"><img src="../images/shapes/irregularSeal2.svg" height="50" width="50"></p>
leftArrow | Forma della freccia sinistra | <p style="text-align: center;"><img src="../images/shapes/leftArrow.svg" height="50" width="50"></p>
leftArrowCallout | Forma della freccia sinistra del richiamo | <p style="text-align: center;"><img src="../images/shapes/leftArrowCallout.svg" height="50" width="50"></p>
leftBrace | Forma del tutore sinistro | <p style="text-align: center;"><img src="../images/shapes/leftBrace.svg" height="50" width="50"></p>
leftBracket | Forma della parentesi sinistra | <p style="text-align: center;"><img src="../images/shapes/leftBracket.svg" height="50" width="50"></p>
leftCircularArrow | Forma di freccia circolare sinistra | <p style="text-align: center;"><img src="../images/shapes/leftCircularArrow.svg" height="50" width="50"></p>
leftRightArrow | Forma della freccia sinistra destra | <p style="text-align: center;"><img src="../images/shapes/leftRightArrow.svg" height="50" width="50"></p>
leftRightArrowCallout | Forma della freccia sinistra destra del callout | <p style="text-align: center;"><img src="../images/shapes/leftRightArrowCallout.svg" height="50" width="50"></p>
leftRightCircularArrow | Forma di freccia circolare sinistra destra | <p style="text-align: center;"><img src="../images/shapes/leftRightCircularArrow.svg" height="50" width="50"></p>
leftRightRibbon | Forma del nastro sinistra destra | <p style="text-align: center;"><img src="../images/shapes/leftRightRibbon.svg" height="50" width="50"></p>
leftRightUpArrow | Forma di freccia su sinistra destra | <p style="text-align: center;"><img src="../images/shapes/leftRightUpArrow.svg" height="50" width="50"></p>
leftUpArrow | Forma freccia su sinistra | <p style="text-align: center;"><img src="../images/shapes/leftUpArrow.svg" height="50" width="50"></p>
lightningBolt | Forma di fulmine | <p style="text-align: center;"><img src="../images/shapes/lightningBolt.svg" height="50" width="50"></p>
line | Forma della linea | <p style="text-align: center;"><img src="../images/shapes/line.svg" height="50" width="50"></p>
lineInv | Forma inversa della linea | <p style="text-align: center;"><img src="../images/shapes/lineInv.svg" height="50" width="50"></p>
mathDivide | Dividere la forma matematica | <p style="text-align: center;"><img src="../images/shapes/mathDivide.svg" height="50" width="50"></p>
mathEqual | Forma matematica uguale | <p style="text-align: center;"><img src="../images/shapes/mathEqual.svg" height="50" width="50"></p>
mathMinus | Meno forma matematica | <p style="text-align: center;"><img src="../images/shapes/mathMinus.svg" height="50" width="50"></p>
mathMultiply | Moltiplica la forma matematica | <p style="text-align: center;"><img src="../images/shapes/mathMultiply.svg" height="50" width="50"></p>
mathNotEqual | Forma matematica non uguale | <p style="text-align: center;"><img src="../images/shapes/mathNotEqual.svg" height="50" width="50"></p>
mathPlus | Inoltre forma matematica | <p style="text-align: center;"><img src="../images/shapes/mathPlus.svg" height="50" width="50"></p>
moon | Forma della luna | <p style="text-align: center;"><img src="../images/shapes/moon.svg" height="50" width="50"></p>
nonIsoscelesTrapezoid | Forma trapezoidale non isoscele | <p style="text-align: center;"><img src="../images/shapes/nonIsoscelesTrapezoid.svg" height="50" width="50"></p>
noSmoking | Forma per non fumare | <p style="text-align: center;"><img src="../images/shapes/noSmoking.svg" height="50" width="50"></p>
notchedRightArrow | Forma di freccia destra dentellata | <p style="text-align: center;"><img src="../images/shapes/notchedRightArrow.svg" height="50" width="50"></p>
octagon | Forma ottagonale | <p style="text-align: center;"><img src="../images/shapes/octagon.svg" height="50" width="50"></p>
parallelogram | Forma a parallelogramma | <p style="text-align: center;"><img src="../images/shapes/parallelogram.svg" height="50" width="50"></p>
pentagon | Forma pentagonale | <p style="text-align: center;"><img src="../images/shapes/pentagon.svg" height="50" width="50"></p>
pie | Forma di torta | <p style="text-align: center;"><img src="../images/shapes/pie.svg" height="50" width="50"></p>
pieWedge | Forma a cuneo di torta | <p style="text-align: center;"><img src="../images/shapes/pieWedge.svg" height="50" width="50"></p>
plaque | Forma della placca | <p style="text-align: center;"><img src="../images/shapes/plaque.svg" height="50" width="50"></p>
plaqueTabs | Forma delle linguette della placca | <p style="text-align: center;"><img src="../images/shapes/plaqueTabs.svg" height="50" width="50"></p>
plus | Più forma | <p style="text-align: center;"><img src="../images/shapes/plus.svg" height="50" width="50"></p>
quadArrow | Forma a quattro frecce | <p style="text-align: center;"><img src="../images/shapes/quadArrow.svg" height="50" width="50"></p>
quadArrowCallout | Callout a forma di freccia quadrupla | <p style="text-align: center;"><img src="../images/shapes/quadArrowCallout.svg" height="50" width="50"></p>
rect | Forma rettangolare | <p style="text-align: center;"><img src="../images/shapes/rect.svg" height="50" width="50"></p>
ribbon | Forma del nastro | <p style="text-align: center;"><img src="../images/shapes/ribbon.svg" height="50" width="50"></p>
ribbon2 | Nastro 2 Forma | <p style="text-align: center;"><img src="../images/shapes/ribbon2.svg" height="50" width="50"></p>
rightArrow | Forma della freccia destra | <p style="text-align: center;"><img src="../images/shapes/rightArrow.svg" height="50" width="50"></p>
rightArrowCallout | Forma della freccia destra del richiamo | <p style="text-align: center;"><img src="../images/shapes/rightArrowCallout.svg" height="50" width="50"></p>
rightBrace | Forma del tutore destro | <p style="text-align: center;"><img src="../images/shapes/rightBrace.svg" height="50" width="50"></p>
rightBracket | Forma della parentesi destra | <p style="text-align: center;"><img src="../images/shapes/rightBracket.svg" height="50" width="50"></p>
round1Rect | Forma rettangolare con angolo arrotondato | <p style="text-align: center;"><img src="../images/shapes/round1Rect.svg" height="50" width="50"></p>
round2DiagRect | Forma rettangolare a due angoli rotondi diagonali | <p style="text-align: center;"><img src="../images/shapes/round2DiagRect.svg" height="50" width="50"></p>
round2SameRect | Due forme rettangolari con angoli arrotondati sullo stesso lato | <p style="text-align: center;"><img src="../images/shapes/round2SameRect.svg" height="50" width="50"></p>
roundRect | Forma rettangolare con angoli arrotondati | <p style="text-align: center;"><img src="../images/shapes/roundRect.svg" height="50" width="50"></p>
rtTriangle | Forma di triangolo rettangolo | <p style="text-align: center;"><img src="../images/shapes/rtTriangle.svg" height="50" width="50"></p>
smileyFace | Forma di faccina sorridente | <p style="text-align: center;"><img src="../images/shapes/smileyFace.svg" height="50" width="50"></p>
snip1Rect | Forma rettangolare con un angolo di taglio | <p style="text-align: center;"><img src="../images/shapes/snip1Rect.svg" height="50" width="50"></p>
snip2DiagRect | Forma rettangolare con due angoli di taglio diagonali | <p style="text-align: center;"><img src="../images/shapes/snip2DiagRect.svg" height="50" width="50"></p>
snip2SameRect | Forma rettangolare con due angoli di taglio sullo stesso lato | <p style="text-align: center;"><img src="../images/shapes/snip2SameRect.svg" height="50" width="50"></p>
snipRoundRect | Una forma rettangolare con angolo arrotondato e un taglio | <p style="text-align: center;"><img src="../images/shapes/snipRoundRect.svg" height="50" width="50"></p>
squareTabs | Forma di linguette quadrate | <p style="text-align: center;"><img src="../images/shapes/squareTabs.svg" height="50" width="50"></p>
star10 | Forma di stella a dieci punte | <p style="text-align: center;"><img src="../images/shapes/star10.svg" height="50" width="50"></p>
star12 | Forma di stella a dodici punte | <p style="text-align: center;"><img src="../images/shapes/star12.svg" height="50" width="50"></p>
star16 | Forma di stella a sedici punte | <p style="text-align: center;"><img src="../images/shapes/star16.svg" height="50" width="50"></p>
star24 | Forma di stella a ventiquattro punte | <p style="text-align: center;"><img src="../images/shapes/star24.svg" height="50" width="50"></p>
star32 | Forma di stella a trentadue punte | <p style="text-align: center;"><img src="../images/shapes/star32.svg" height="50" width="50"></p>
star4 | Forma di stella a quattro punte | <p style="text-align: center;"><img src="../images/shapes/star4.svg" height="50" width="50"></p>
star5 | Forma di stella a cinque punte | <p style="text-align: center;"><img src="../images/shapes/star5.svg" height="50" width="50"></p>
star6 | Forma di stella a sei punte | <p style="text-align: center;"><img src="../images/shapes/star6.svg" height="50" width="50"></p>
star7 | Forma di stella a sette punte | <p style="text-align: center;"><img src="../images/shapes/star7.svg" height="50" width="50"></p>
star8 | Forma di stella a otto punte | <p style="text-align: center;"><img src="../images/shapes/star8.svg" height="50" width="50"></p>
straightConnector1 | Connettore dritto 1 forma | <p style="text-align: center;"><img src="../images/shapes/straightConnector1.svg" height="50" width="50"></p>
stripedRightArrow | Forma di freccia destra a strisce | <p style="text-align: center;"><img src="../images/shapes/stripedRightArrow.svg" height="50" width="50"></p>
sun | Forma del sole | <p style="text-align: center;"><img src="../images/shapes/sun.svg" height="50" width="50"></p>
swooshArrow | Swoosh a forma di freccia | <p style="text-align: center;"><img src="../images/shapes/swooshArrow.svg" height="50" width="50"></p>
teardrop | Forma a goccia | <p style="text-align: center;"><img src="../images/shapes/teardrop.svg" height="50" width="50"></p>
trapezoid | Forma trapezoidale | <p style="text-align: center;"><img src="../images/shapes/trapezoid.svg" height="50" width="50"></p>
triangle | Forma triangolare | <p style="text-align: center;"><img src="../images/shapes/triangle.svg" height="50" width="50"></p>
upArrow | Forma di freccia su | <p style="text-align: center;"><img src="../images/shapes/upArrow.svg" height="50" width="50"></p>
upArrowCallout | Forma di freccia su didascalia | <p style="text-align: center;"><img src="../images/shapes/upArrowCallout.svg" height="50" width="50"></p>
upDownArrow | Forma di freccia su giù | <p style="text-align: center;"><img src="../images/shapes/upDownArrow.svg" height="50" width="50"></p>
upDownArrowCallout | Callout a forma di freccia su giù | <p style="text-align: center;"><img src="../images/shapes/upDownArrowCallout.svg" height="50" width="50"></p>
uturnArrow | Forma di freccia di inversione a U | <p style="text-align: center;"><img src="../images/shapes/uturnArrow.svg" height="50" width="50"></p>
verticalScroll | Forma di scorrimento verticale | <p style="text-align: center;"><img src="../images/shapes/verticalScroll.svg" height="50" width="50"></p>
wave | Forma d'onda | <p style="text-align: center;"><img src="../images/shapes/wave.svg" height="50" width="50"></p>
wedgeEllipseCallout | Forma di ellisse a cuneo di richiamo | <p style="text-align: center;"><img src="../images/shapes/wedgeEllipseCallout.svg" height="50" width="50"></p>
wedgeRectCallout | Forma rettangolare a cuneo di richiamo | <p style="text-align: center;"><img src="../images/shapes/wedgeRectCallout.svg" height="50" width="50"></p>
wedgeRoundRectCallout | Forma rettangolare rotonda con cuneo di richiamo | <p style="text-align: center;"><img src="../images/shapes/wedgeRoundRectCallout.svg" height="50" width="50"></p>
