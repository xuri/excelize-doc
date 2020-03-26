# форма

## Добавить форму

```go
func (f *File) AddShape(sheet, cell, format string) error
```

AddShape предоставляет метод добавления фигуры на листе с помощью заданного индекса рабочего листа, формата формы (например, смещения, масштаба, настройки соотношения сторон и параметров печати) и свойств. Например, добавьте текстовое поле (прямая форма) в `Sheet1`:

```go
err := f.AddShape("Sheet1", "G6", `{"type":"rect","color":{"line":"#4286F4","fill":"#8eb9ff"},"paragraph":[{"text":"Rectangle Shape","font":{"bold":true,"italic":true,"family":"Times New Roman","size":36,"color":"#777777","underline":"sng"}}],"width":180,"height": 90}`)
```

Ниже показан тип формы, поддерживаемый excelize:

Тип|Форма|Стиль
---|---|---
accentBorderCallout1 | Выноска 1 с границей и фигуры диакритических знаков | <p style="text-align: center;"><img src="../images/shapes/accentBorderCallout1.svg" height="50" width="50"></p>
accentBorderCallout2 | Выноска 2 с границей и фигуры диакритических знаков | <p style="text-align: center;"><img src="../images/shapes/accentBorderCallout2.svg" height="50" width="50"></p>
accentBorderCallout3 | Выноска 3 с границей и фигуры диакритических знаков | <p style="text-align: center;"><img src="../images/shapes/accentBorderCallout3.svg" height="50" width="50"></p>
accentCallout1 | Фигура выноски 1 | <p style="text-align: center;"><img src="../images/shapes/accentCallout1.svg" height="50" width="50"></p>
accentCallout2 | Фигура выноски 2 | <p style="text-align: center;"><img src="../images/shapes/accentCallout2.svg" height="50" width="50"></p>
accentCallout3 | Фигура выноски 3 | <p style="text-align: center;"><img src="../images/shapes/accentCallout3.svg" height="50" width="50"></p>
actionButtonBackPrevious | Кнопка Назад фигуры | <p style="text-align: center;"><img src="../images/shapes/actionButtonBackPrevious.svg" height="50" width="50"></p>
actionButtonBeginning | Фигура начала кнопка | <p style="text-align: center;"><img src="../images/shapes/actionButtonBeginning.svg" height="50" width="50"></p>
actionButtonBlank | Пустая кнопка фигуры | <p style="text-align: center;"><img src="../images/shapes/actionButtonBlank.svg" height="50" width="50"></p>
actionButtonDocument | Фигура кнопка документа | <p style="text-align: center;"><img src="../images/shapes/actionButtonDocument.svg" height="50" width="50"></p>
actionButtonEnd | Фигура окончания кнопка | <p style="text-align: center;"><img src="../images/shapes/actionButtonEnd.svg" height="50" width="50"></p>
actionButtonForwardNext | Переадресация или далее кнопку фигуры | <p style="text-align: center;"><img src="../images/shapes/actionButtonForwardNext.svg" height="50" width="50"></p>
actionButtonHelp | Фигура кнопки справки | <p style="text-align: center;"><img src="../images/shapes/actionButtonHelp.svg" height="50" width="50"></p>
actionButtonHome | Домашняя страница кнопка фигуры | <p style="text-align: center;"><img src="../images/shapes/actionButtonHome.svg" height="50" width="50"></p>
actionButtonInformation | Фигура кнопку сведения | <p style="text-align: center;"><img src="../images/shapes/actionButtonInformation.svg" height="50" width="50"></p>
actionButtonMovie | Фигура кнопка фильма | <p style="text-align: center;"><img src="../images/shapes/actionButtonMovie.svg" height="50" width="50"></p>
actionButtonReturn | Возвращает форму кнопки | <p style="text-align: center;"><img src="../images/shapes/actionButtonReturn.svg" height="50" width="50"></p>
actionButtonSound |При нажатии кнопки звук фигуры | <p style="text-align: center;"><img src="../images/shapes/actionButtonSound.svg" height="50" width="50"></p>
arc | Фигура кривой Arc | <p style="text-align: center;"><img src="../images/shapes/arc.svg" height="50" width="50"></p>
bentArrow | Фигура стрелку углом | <p style="text-align: center;"><img src="../images/shapes/bentArrow.svg" height="50" width="50"></p>
bentConnector2 | Фигура углом соединителя 2 | <p style="text-align: center;"><img src="../images/shapes/bentConnector2.svg" height="50" width="50"></p>
bentConnector3 | Фигура углом соединителя 3 | <p style="text-align: center;"><img src="../images/shapes/bentConnector3.svg" height="50" width="50"></p>
bentConnector4 | Фигура углом соединителя 4 | <p style="text-align: center;"><img src="../images/shapes/bentConnector4.svg" height="50" width="50"></p>
bentConnector5 | Фигура углом соединителя 5 | <p style="text-align: center;"><img src="../images/shapes/bentConnector5.svg" height="50" width="50"></p>
bentUpArrow | Углом вверх стрелки | <p style="text-align: center;"><img src="../images/shapes/bentUpArrow.svg" height="50" width="50"></p>
bevel | Багетная рамка фигуры | <p style="text-align: center;"><img src="../images/shapes/bevel.svg" height="50" width="50"></p>
blockArc | Фигура Arc блокировки | <p style="text-align: center;"><img src="../images/shapes/blockArc.svg" height="50" width="50"></p>
borderCallout1 | Выноска 1 с границы фигуры | <p style="text-align: center;"><img src="../images/shapes/borderCallout1.svg" height="50" width="50"></p>
borderCallout2 | Выноска 2 с границы фигуры | <p style="text-align: center;"><img src="../images/shapes/borderCallout2.svg" height="50" width="50"></p>
borderCallout3 | Выноска 3 с границы фигуры | <p style="text-align: center;"><img src="../images/shapes/borderCallout3.svg" height="50" width="50"></p>
bracePair | Правая фигурная пары фигуры | <p style="text-align: center;"><img src="../images/shapes/bracePair.svg" height="50" width="50"></p>
bracketPair | Фигура пары скобку | <p style="text-align: center;"><img src="../images/shapes/bracketPair.svg" height="50" width="50"></p>
callout1 | Фигура выноски 1 | <p style="text-align: center;"><img src="../images/shapes/callout1.svg" height="50" width="50"></p>
callout2 | Фигура выноски 2 | <p style="text-align: center;"><img src="../images/shapes/callout2.svg" height="50" width="50"></p>
callout3 | Фигура выноски 3 | <p style="text-align: center;"><img src="../images/shapes/callout3.svg" height="50" width="50"></p>
can | Можно изменить | <p style="text-align: center;"><img src="../images/shapes/can.svg" height="50" width="50"></p>
chartPlus | Кроме того фигуры диаграммы | <p style="text-align: center;"><img src="../images/shapes/chartPlus.svg" height="50" width="50"></p>
chartStar | Звезда диаграммы | <p style="text-align: center;"><img src="../images/shapes/chartStar.svg" height="50" width="50"></p>
chartX | Диаграмма X фигуры | <p style="text-align: center;"><img src="../images/shapes/chartX.svg" height="50" width="50"></p>
chevron | Шеврон фигуры | <p style="text-align: center;"><img src="../images/shapes/chevron.svg" height="50" width="50"></p>
chord | Фигура кабеля | <p style="text-align: center;"><img src="../images/shapes/chord.svg" height="50" width="50"></p>
circularArrow | Круговые стрелки | <p style="text-align: center;"><img src="../images/shapes/circularArrow.svg" height="50" width="50"></p>
cloud | Фигуры в облаке | <p style="text-align: center;"><img src="../images/shapes/cloud.svg" height="50" width="50"></p>
cloudCallout | Фигура выноски облака | <p style="text-align: center;"><img src="../images/shapes/cloudCallout.svg" height="50" width="50"></p>
corner | Угол фигуры | <p style="text-align: center;"><img src="../images/shapes/corner.svg" height="50" width="50"></p>
cornerTabs | Фигура вкладок угла | <p style="text-align: center;"><img src="../images/shapes/cornerTabs.svg" height="50" width="50"></p>
cube | Фигура куба | <p style="text-align: center;"><img src="../images/shapes/cube.svg" height="50" width="50"></p>
curvedConnector2 | Круглая соединителя 2 фигуры | <p style="text-align: center;"><img src="../images/shapes/curvedConnector2.svg" height="50" width="50"></p>
curvedConnector3 | Круглая соединителя 3 фигуры | <p style="text-align: center;"><img src="../images/shapes/curvedConnector3.svg" height="50" width="50"></p>
curvedConnector4 | Круглая соединителя 4 фигуры | <p style="text-align: center;"><img src="../images/shapes/curvedConnector4.svg" height="50" width="50"></p>
curvedConnector5 | Круглая соединителя 5 фигуры | <p style="text-align: center;"><img src="../images/shapes/curvedConnector5.svg" height="50" width="50"></p>
curvedDownArrow | Круглая вниз стрелки | <p style="text-align: center;"><img src="../images/shapes/curvedDownArrow.svg" height="50" width="50"></p>
curvedLeftArrow | Круглая стрелка влево фигуры | <p style="text-align: center;"><img src="../images/shapes/curvedLeftArrow.svg" height="50" width="50"></p>
curvedRightArrow | Круглая Стрелка вправо фигуры | <p style="text-align: center;"><img src="../images/shapes/curvedRightArrow.svg" height="50" width="50"></p>
curvedUpArrow | Круглая вверх стрелки | <p style="text-align: center;"><img src="../images/shapes/curvedUpArrow.svg" height="50" width="50"></p>
decagon | Фигура decagon | <p style="text-align: center;"><img src="../images/shapes/decagon.svg" height="50" width="50"></p>
diagStripe | Диагональная полоса фигуры | <p style="text-align: center;"><img src="../images/shapes/diagStripe.svg" height="50" width="50"></p>
diamond | Ромб фигуры | <p style="text-align: center;"><img src="../images/shapes/diamond.svg" height="50" width="50"></p>
dodecagon | Фигура dodecagon | <p style="text-align: center;"><img src="../images/shapes/dodecagon.svg" height="50" width="50"></p>
donut | Фигура пончик | <p style="text-align: center;"><img src="../images/shapes/donut.svg" height="50" width="50"></p>
doubleWave | Двойная волнистая фигуры | <p style="text-align: center;"><img src="../images/shapes/doubleWave.svg" height="50" width="50"></p>
downArrow | Вниз стрелки | <p style="text-align: center;"><img src="../images/shapes/downArrow.svg" height="50" width="50"></p>
downArrowCallout | Фигура стрелка вниз выноски | <p style="text-align: center;"><img src="../images/shapes/downArrowCallout.svg" height="50" width="50"></p>
ellipse | Фигура эллипс | <p style="text-align: center;"><img src="../images/shapes/ellipse.svg" height="50" width="50"></p>
ellipseRibbon | Фигура эллипс ленты | <p style="text-align: center;"><img src="../images/shapes/ellipseRibbon.svg" height="50" width="50"></p>
ellipseRibbon2 | Фигура ленты 2 эллипс | <p style="text-align: center;"><img src="../images/shapes/ellipseRibbon2.svg" height="50" width="50"></p>
flowChartAlternateProcess | Альтернативный процесс поток фигуры | <p style="text-align: center;"><img src="../images/shapes/flowChartAlternateProcess.svg" height="50" width="50"></p>
flowChartCollate | Сопоставление поток фигуры | <p style="text-align: center;"><img src="../images/shapes/flowChartCollate.svg" height="50" width="50"></p>
flowChartConnector | Фигура поток соединителя | <p style="text-align: center;"><img src="../images/shapes/flowChartConnector.svg" height="50" width="50"></p>
flowChartDecision | Фигура поток принятия решений | <p style="text-align: center;"><img src="../images/shapes/flowChartDecision.svg" height="50" width="50"></p>
flowChartDelay | Задержка поток фигуры | <p style="text-align: center;"><img src="../images/shapes/flowChartDelay.svg" height="50" width="50"></p>
flowChartDisplay | Отображение фигуры потока | <p style="text-align: center;"><img src="../images/shapes/flowChartDisplay.svg" height="50" width="50"></p>
flowChartDocument | Фигура поток обработки документов | <p style="text-align: center;"><img src="../images/shapes/flowChartDocument.svg" height="50" width="50"></p>
flowChartExtract | Извлечение потока фигуры | <p style="text-align: center;"><img src="../images/shapes/flowChartExtract.svg" height="50" width="50"></p>
flowChartInputOutput | Фигура потока ввода-вывода | <p style="text-align: center;"><img src="../images/shapes/flowChartInternalStorage.svg" height="50" width="50"></p>
flowChartInternalStorage | Внутреннее хранилище потока фигуры | <p style="text-align: center;"><img src="../images/shapes/flowChartInternalStorage.svg" height="50" width="50"></p>
flowChartMagneticDisk | Фигура поток магнитным диска | <p style="text-align: center;"><img src="../images/shapes/flowChartMagneticDisk.svg" height="50" width="50"></p>
flowChartMagneticDrum | Фигура Магнитное барабана потока | <p style="text-align: center;"><img src="../images/shapes/flowChartMagneticDrum.svg" height="50" width="50"></p>
flowChartMagneticTape | Фигура ленточного потока | <p style="text-align: center;"><img src="../images/shapes/flowChartMagneticTape.svg" height="50" width="50"></p>
flowChartManualInput | Фигура вручную входной поток | <p style="text-align: center;"><img src="../images/shapes/flowChartManualInput.svg" height="50" width="50"></p>
flowChartManualOperation | Фигура поток ручные операции | <p style="text-align: center;"><img src="../images/shapes/flowChartManualOperation.svg" height="50" width="50"></p>
flowChartMerge | Объединение фигур потока | <p style="text-align: center;"><img src="../images/shapes/flowChartMerge.svg" height="50" width="50"></p>
flowChartMultidocument | Поток обработки нескольких документов фигуры | <p style="text-align: center;"><img src="../images/shapes/flowChartMultidocument.svg" height="50" width="50"></p>
flowChartOfflineStorage | Offline Storage Flow Shape | <p style="text-align: center;"><img src="../images/shapes/flowChartOfflineStorage.svg" height="50" width="50"></p>
flowChartOffpageConnector | Off-Page Connector Flow Shape | <p style="text-align: center;"><img src="../images/shapes/flowChartOffpageConnector.svg" height="50" width="50"></p>
flowChartOnlineStorage | Online Storage Flow Shape | <p style="text-align: center;"><img src="../images/shapes/flowChartOnlineStorage.svg" height="50" width="50"></p>
flowChartOr | Or Flow Shape | <p style="text-align: center;"><img src="../images/shapes/flowChartOr.svg" height="50" width="50"></p>
flowChartPredefinedProcess | Predefined Process Flow Shape | <p style="text-align: center;"><img src="../images/shapes/flowChartPredefinedProcess.svg" height="50" width="50"></p>
flowChartPreparation | Preparation Flow Shape | <p style="text-align: center;"><img src="../images/shapes/flowChartPredefinedProcess.svg" height="50" width="50"></p>
flowChartProcess | Process Flow Shape | <p style="text-align: center;"><img src="../images/shapes/flowChartPreparation.svg" height="50" width="50"></p>
flowChartPunchedCard | Punched Card Flow Shape | <p style="text-align: center;"><img src="../images/shapes/flowChartPunchedCard.svg" height="50" width="50"></p>
flowChartPunchedTape | Punched Tape Flow Shape | <p style="text-align: center;"><img src="../images/shapes/flowChartPunchedTape.svg" height="50" width="50"></p>
flowChartSort | Sort Flow Shape | <p style="text-align: center;"><img src="../images/shapes/flowChartSort.svg" height="50" width="50"></p>
flowChartSummingJunction | Summing Junction Flow Shape | <p style="text-align: center;"><img src="../images/shapes/flowChartSummingJunction.svg" height="50" width="50"></p>
flowChartTerminator | Terminator Flow Shape | <p style="text-align: center;"><img src="../images/shapes/flowChartTerminator.svg" height="50" width="50"></p>
foldedCorner | Folded Corner Shape | <p style="text-align: center;"><img src="../images/shapes/foldedCorner.svg" height="50" width="50"></p>
frame | Frame Shape | <p style="text-align: center;"><img src="../images/shapes/frame.svg" height="50" width="50"></p>
funnel | Funnel Shape | <p style="text-align: center;"><img src="../images/shapes/funnel.svg" height="50" width="50"></p>
gear6 | Gear 6 Shape | <p style="text-align: center;"><img src="../images/shapes/gear6.svg" height="50" width="50"></p>
gear9 | Gear 9 Shape | <p style="text-align: center;"><img src="../images/shapes/gear9.svg" height="50" width="50"></p>
halfFrame | Half Frame Shape | <p style="text-align: center;"><img src="../images/shapes/halfFrame.svg" height="50" width="50"></p>
heart | Heart Shape | <p style="text-align: center;"><img src="../images/shapes/heart.svg" height="50" width="50"></p>
heptagon | Heptagon Shape | <p style="text-align: center;"><img src="../images/shapes/heptagon.svg" height="50" width="50"></p>
hexagon | Hexagon Shape | <p style="text-align: center;"><img src="../images/shapes/hexagon.svg" height="50" width="50"></p>
homePlate | Home Plate Shape | <p style="text-align: center;"><img src="../images/shapes/homePlate.svg" height="50" width="50"></p>
horizontalScroll | Horizontal Scroll Shape | <p style="text-align: center;"><img src="../images/shapes/horizontalScroll.svg" height="50" width="50"></p>
irregularSeal1 | Irregular Seal 1 Shape | <p style="text-align: center;"><img src="../images/shapes/irregularSeal1.svg" height="50" width="50"></p>
irregularSeal2 | Irregular Seal 2 Shape | <p style="text-align: center;"><img src="../images/shapes/irregularSeal2.svg" height="50" width="50"></p>
leftArrow | Left Arrow Shape | <p style="text-align: center;"><img src="../images/shapes/leftArrow.svg" height="50" width="50"></p>
leftArrowCallout | Callout Left Arrow Shape | <p style="text-align: center;"><img src="../images/shapes/leftArrowCallout.svg" height="50" width="50"></p>
leftBrace | Left Brace Shape | <p style="text-align: center;"><img src="../images/shapes/leftBrace.svg" height="50" width="50"></p>
leftBracket | Left Bracket Shape | <p style="text-align: center;"><img src="../images/shapes/leftBracket.svg" height="50" width="50"></p>
leftCircularArrow | Left Circular Arrow Shape | <p style="text-align: center;"><img src="../images/shapes/leftCircularArrow.svg" height="50" width="50"></p>
leftRightArrow | Left Right Arrow Shape | <p style="text-align: center;"><img src="../images/shapes/leftRightArrow.svg" height="50" width="50"></p>
leftRightArrowCallout | Callout Left Right Arrow Shape | <p style="text-align: center;"><img src="../images/shapes/leftRightArrowCallout.svg" height="50" width="50"></p>
leftRightCircularArrow | Left Right Circular Arrow Shape | <p style="text-align: center;"><img src="../images/shapes/leftRightCircularArrow.svg" height="50" width="50"></p>
leftRightRibbon | Left Right Ribbon Shape | <p style="text-align: center;"><img src="../images/shapes/leftRightRibbon.svg" height="50" width="50"></p>
leftRightUpArrow | Left Right Up Arrow Shape | <p style="text-align: center;"><img src="../images/shapes/leftRightUpArrow.svg" height="50" width="50"></p>
leftUpArrow | Left Up Arrow Shape | <p style="text-align: center;"><img src="../images/shapes/leftUpArrow.svg" height="50" width="50"></p>
lightningBolt | Lightning Bolt Shape | <p style="text-align: center;"><img src="../images/shapes/lightningBolt.svg" height="50" width="50"></p>
line | Line Shape | <p style="text-align: center;"><img src="../images/shapes/line.svg" height="50" width="50"></p>
lineInv | Line Inverse Shape | <p style="text-align: center;"><img src="../images/shapes/lineInv.svg" height="50" width="50"></p>
mathDivide | Divide Math Shape | <p style="text-align: center;"><img src="../images/shapes/mathDivide.svg" height="50" width="50"></p>
mathEqual | Equal Math Shape | <p style="text-align: center;"><img src="../images/shapes/mathEqual.svg" height="50" width="50"></p>
mathMinus | Minus Math Shape | <p style="text-align: center;"><img src="../images/shapes/mathMinus.svg" height="50" width="50"></p>
mathMultiply | Multiply Math Shape | <p style="text-align: center;"><img src="../images/shapes/mathMultiply.svg" height="50" width="50"></p>
mathNotEqual | Not Equal Math Shape | <p style="text-align: center;"><img src="../images/shapes/mathNotEqual.svg" height="50" width="50"></p>
mathPlus | Plus Math Shape | <p style="text-align: center;"><img src="../images/shapes/mathPlus.svg" height="50" width="50"></p>
moon | Moon Shape | <p style="text-align: center;"><img src="../images/shapes/moon.svg" height="50" width="50"></p>
nonIsoscelesTrapezoid | Non-Isosceles Trapezoid Shape | <p style="text-align: center;"><img src="../images/shapes/nonIsoscelesTrapezoid.svg" height="50" width="50"></p>
noSmoking | No Smoking Shape | <p style="text-align: center;"><img src="../images/shapes/noSmoking.svg" height="50" width="50"></p>
notchedRightArrow | Notched Right Arrow Shape | <p style="text-align: center;"><img src="../images/shapes/notchedRightArrow.svg" height="50" width="50"></p>
octagon | Octagon Shape | <p style="text-align: center;"><img src="../images/shapes/octagon.svg" height="50" width="50"></p>
parallelogram | Parallelogram Shape | <p style="text-align: center;"><img src="../images/shapes/parallelogram.svg" height="50" width="50"></p>
pentagon | Pentagon Shape | <p style="text-align: center;"><img src="../images/shapes/pentagon.svg" height="50" width="50"></p>
pie | Pie Shape | <p style="text-align: center;"><img src="../images/shapes/pie.svg" height="50" width="50"></p>
pieWedge | Pie Wedge Shape | <p style="text-align: center;"><img src="../images/shapes/pieWedge.svg" height="50" width="50"></p>
plaque | Plaque Shape | <p style="text-align: center;"><img src="../images/shapes/plaque.svg" height="50" width="50"></p>
plaqueTabs | Plaque Tabs Shape | <p style="text-align: center;"><img src="../images/shapes/plaqueTabs.svg" height="50" width="50"></p>
plus | Plus Shape | <p style="text-align: center;"><img src="../images/shapes/plus.svg" height="50" width="50"></p>
quadArrow | Quad-Arrow Shape | <p style="text-align: center;"><img src="../images/shapes/quadArrow.svg" height="50" width="50"></p>
quadArrowCallout | Callout Quad-Arrow Shape | <p style="text-align: center;"><img src="../images/shapes/quadArrowCallout.svg" height="50" width="50"></p>
rect | Rectangle Shape | <p style="text-align: center;"><img src="../images/shapes/rect.svg" height="50" width="50"></p>
ribbon | Ribbon Shape | <p style="text-align: center;"><img src="../images/shapes/ribbon.svg" height="50" width="50"></p>
ribbon2 | Ribbon 2 Shape | <p style="text-align: center;"><img src="../images/shapes/ribbon2.svg" height="50" width="50"></p>
rightArrow | Right Arrow Shape | <p style="text-align: center;"><img src="../images/shapes/rightArrow.svg" height="50" width="50"></p>
rightArrowCallout | Callout Right Arrow Shape | <p style="text-align: center;"><img src="../images/shapes/rightArrowCallout.svg" height="50" width="50"></p>
rightBrace | Right Brace Shape | <p style="text-align: center;"><img src="../images/shapes/rightBrace.svg" height="50" width="50"></p>
rightBracket | Right Bracket Shape | <p style="text-align: center;"><img src="../images/shapes/rightBracket.svg" height="50" width="50"></p>
round1Rect | One Round Corner Rectangle Shape | <p style="text-align: center;"><img src="../images/shapes/round1Rect.svg" height="50" width="50"></p>
round2DiagRect | Two Diagonal Round Corner Rectangle Shape | <p style="text-align: center;"><img src="../images/shapes/round2DiagRect.svg" height="50" width="50"></p>
round2SameRect | Two Same-side Round Corner Rectangle Shape | <p style="text-align: center;"><img src="../images/shapes/round2SameRect.svg" height="50" width="50"></p>
roundRect | Round Corner Rectangle Shape | <p style="text-align: center;"><img src="../images/shapes/roundRect.svg" height="50" width="50"></p>
rtTriangle | Right Triangle Shape | <p style="text-align: center;"><img src="../images/shapes/rtTriangle.svg" height="50" width="50"></p>
smileyFace | Smiley Face Shape | <p style="text-align: center;"><img src="../images/shapes/smileyFace.svg" height="50" width="50"></p>
snip1Rect | One Snip Corner Rectangle Shape | <p style="text-align: center;"><img src="../images/shapes/snip1Rect.svg" height="50" width="50"></p>
snip2DiagRect | Two Diagonal Snip Corner Rectangle Shape | <p style="text-align: center;"><img src="../images/shapes/snip2DiagRect.svg" height="50" width="50"></p>
snip2SameRect | Two Same-side Snip Corner Rectangle Shape | <p style="text-align: center;"><img src="../images/shapes/snip2SameRect.svg" height="50" width="50"></p>
snipRoundRect | One Snip One Round Corner Rectangle Shape | <p style="text-align: center;"><img src="../images/shapes/snipRoundRect.svg" height="50" width="50"></p>
squareTabs | Square Tabs Shape | <p style="text-align: center;"><img src="../images/shapes/squareTabs.svg" height="50" width="50"></p>
star10 | Ten Pointed Star Shape | <p style="text-align: center;"><img src="../images/shapes/star10.svg" height="50" width="50"></p>
star12 | Twelve Pointed Star Shape | <p style="text-align: center;"><img src="../images/shapes/star12.svg" height="50" width="50"></p>
star16 | Sixteen Pointed Star Shape | <p style="text-align: center;"><img src="../images/shapes/star16.svg" height="50" width="50"></p>
star24 | Twenty Four Pointed Star Shape | <p style="text-align: center;"><img src="../images/shapes/star24.svg" height="50" width="50"></p>
star32 | Thirty Two Pointed Star Shape | <p style="text-align: center;"><img src="../images/shapes/star32.svg" height="50" width="50"></p>
star4 | Four Pointed Star Shape | <p style="text-align: center;"><img src="../images/shapes/star4.svg" height="50" width="50"></p>
star5 | Five Pointed Star Shape | <p style="text-align: center;"><img src="../images/shapes/star5.svg" height="50" width="50"></p>
star6 | Six Pointed Star Shape | <p style="text-align: center;"><img src="../images/shapes/star6.svg" height="50" width="50"></p>
star7 | Seven Pointed Star Shape | <p style="text-align: center;"><img src="../images/shapes/star7.svg" height="50" width="50"></p>
star8 | Eight Pointed Star Shape | <p style="text-align: center;"><img src="../images/shapes/star8.svg" height="50" width="50"></p>
straightConnector1 | Straight Connector 1 Shape | <p style="text-align: center;"><img src="../images/shapes/straightConnector1.svg" height="50" width="50"></p>
stripedRightArrow | Striped Right Arrow Shape | <p style="text-align: center;"><img src="../images/shapes/stripedRightArrow.svg" height="50" width="50"></p>
sun | Sun Shape | <p style="text-align: center;"><img src="../images/shapes/sun.svg" height="50" width="50"></p>
swooshArrow | Swoosh Arrow Shape | <p style="text-align: center;"><img src="../images/shapes/swooshArrow.svg" height="50" width="50"></p>
teardrop | Teardrop Shape | <p style="text-align: center;"><img src="../images/shapes/teardrop.svg" height="50" width="50"></p>
trapezoid | Trapezoid Shape | <p style="text-align: center;"><img src="../images/shapes/trapezoid.svg" height="50" width="50"></p>
triangle | Triangle Shape | <p style="text-align: center;"><img src="../images/shapes/triangle.svg" height="50" width="50"></p>
upArrow | Up Arrow Shape | <p style="text-align: center;"><img src="../images/shapes/upArrow.svg" height="50" width="50"></p>
upArrowCallout | Callout Up Arrow Shape | <p style="text-align: center;"><img src="../images/shapes/upArrowCallout.svg" height="50" width="50"></p>
upDownArrow | Up Down Arrow Shape | <p style="text-align: center;"><img src="../images/shapes/upDownArrow.svg" height="50" width="50"></p>
upDownArrowCallout | Callout Up Down Arrow Shape | <p style="text-align: center;"><img src="../images/shapes/upDownArrowCallout.svg" height="50" width="50"></p>
uturnArrow | U-Turn Arrow Shape | <p style="text-align: center;"><img src="../images/shapes/uturnArrow.svg" height="50" width="50"></p>
verticalScroll | Vertical Scroll Shape | <p style="text-align: center;"><img src="../images/shapes/verticalScroll.svg" height="50" width="50"></p>
wave | Wave Shape | <p style="text-align: center;"><img src="../images/shapes/wave.svg" height="50" width="50"></p>
wedgeEllipseCallout | Callout Wedge Ellipse Shape | <p style="text-align: center;"><img src="../images/shapes/wedgeEllipseCallout.svg" height="50" width="50"></p>
wedgeRectCallout | Callout Wedge Rectangle Shape | <p style="text-align: center;"><img src="../images/shapes/wedgeRectCallout.svg" height="50" width="50"></p>
wedgeRoundRectCallout | Callout Wedge Round Rectangle Shape  | <p style="text-align: center;"><img src="../images/shapes/wedgeRoundRectCallout.svg" height="50" width="50"></p>
