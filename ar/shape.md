# الشكل

## أضف الشكل

```go
func (f *File) AddShape(sheet, cell string, opts *Shape) error
```

يوفر AddShape طريقة لإضافة شكل في ورقة من خلال فهرس ورقة عمل معين ومجموعة تنسيق الشكل (مثل الإزاحة والقياس وإعدادات نسبة العرض إلى الارتفاع وإعدادات الطباعة) ومجموعة الخصائص. على سبيل المثال ، أضف مربع نص (شكل مستطيل) في "Sheet1":

```go
width, height, lineWidth := 180, 40, 1.2
err := f.AddShape("Sheet1", "G6",
    &excelize.Shape{
        Type:  "rect",
        Color: excelize.ShapeColor{Line: "#4286f4", Fill: "#8eb9ff"},
        Paragraph: []excelize.ShapeParagraph{
            {
                Text: "شكل مستطيل",
                Font: excelize.Font{
                    Bold:      true,
                    Italic:    true,
                    Family:    "Times New Roman",
                    Size:      18,
                    Color:     "#777777",
                    Underline: "sng",
                },
            },
        },
        Width:  &width,
        Height: &height,
        Line:   excelize.ShapeLine{Width: &lineWidth},
    },
)
```

يوضح ما يلي نوع الشكل الذي يدعمه برنامج excelize:

اكتب|الشكل|معاينة
---|---|---
accentBorderCallout1 | وسيلة الشرح 1 ذات شكل الحدود والتشديد | <p style="text-align: center;"><img src="../images/shapes/accentBorderCallout1.svg" height="50" width="50"></p>
accentBorderCallout2 | وسيلة الشرح 2 ذات شكل الحدود والتشديد | <p style="text-align: center;"><img src="../images/shapes/accentBorderCallout2.svg" height="50" width="50"></p>
accentBorderCallout3 | وسيلة الشرح 3 ذات شكل الحدود والتشديد | <p style="text-align: center;"><img src="../images/shapes/accentBorderCallout3.svg" height="50" width="50"></p>
accentCallout1 | شكل وسيلة الشرح 1 | <p style="text-align: center;"><img src="../images/shapes/accentCallout1.svg" height="50" width="50"></p>
accentCallout2 | شكل وسيلة الشرح 2 | <p style="text-align: center;"><img src="../images/shapes/accentCallout2.svg" height="50" width="50"></p>
accentCallout3 | شكل وسيلة الشرح 3 | <p style="text-align: center;"><img src="../images/shapes/accentCallout3.svg" height="50" width="50"></p>
actionButtonBackPrevious | الخلف أو شكل الزر السابق | <p style="text-align: center;"><img src="../images/shapes/actionButtonBackPrevious.svg" height="50" width="50"></p>
actionButtonBeginning | بداية شكل الزر | <p style="text-align: center;"><img src="../images/shapes/actionButtonBeginning.svg" height="50" width="50"></p>
actionButtonBlank | شكل زر فارغ | <p style="text-align: center;"><img src="../images/shapes/actionButtonBlank.svg" height="50" width="50"></p>
actionButtonDocument | وثيقة شكل زر | <p style="text-align: center;"><img src="../images/shapes/actionButtonDocument.svg" height="50" width="50"></p>
actionButtonEnd | شكل زر الإنهاء | <p style="text-align: center;"><img src="../images/shapes/actionButtonEnd.svg" height="50" width="50"></p>
actionButtonForwardNext | إلى الأمام أو شكل الزر التالي | <p style="text-align: center;"><img src="../images/shapes/actionButtonForwardNext.svg" height="50" width="50"></p>
actionButtonHelp | شكل زر المساعدة | <p style="text-align: center;"><img src="../images/shapes/actionButtonHelp.svg" height="50" width="50"></p>
actionButtonHome | شكل زر الصفحة الرئيسية | <p style="text-align: center;"><img src="../images/shapes/actionButtonHome.svg" height="50" width="50"></p>
actionButtonInformation | شكل زر المعلومات | <p style="text-align: center;"><img src="../images/shapes/actionButtonInformation.svg" height="50" width="50"></p>
actionButtonMovie | شكل زر الفيلم | <p style="text-align: center;"><img src="../images/shapes/actionButtonMovie.svg" height="50" width="50"></p>
actionButtonReturn | عودة شكل زر | <p style="text-align: center;"><img src="../images/shapes/actionButtonReturn.svg" height="50" width="50"></p>
actionButtonSound | شكل زر الصوت | <p style="text-align: center;"><img src="../images/shapes/actionButtonSound.svg" height="50" width="50"></p>
arc | شكل قوس منحني | <p style="text-align: center;"><img src="../images/shapes/arc.svg" height="50" width="50"></p>
bentArrow | شكل سهم عازمة | <p style="text-align: center;"><img src="../images/shapes/bentArrow.svg" height="50" width="50"></p>
bentConnector2 | موصل عازمة 2 الشكل | <p style="text-align: center;"><img src="../images/shapes/bentConnector2.svg" height="50" width="50"></p>
bentConnector3 | موصل عازمة 3 الشكل | <p style="text-align: center;"><img src="../images/shapes/bentConnector3.svg" height="50" width="50"></p>
bentConnector4 | موصل عازمة 4 الشكل | <p style="text-align: center;"><img src="../images/shapes/bentConnector4.svg" height="50" width="50"></p>
bentConnector5 | موصل عازمة 5 الشكل | <p style="text-align: center;"><img src="../images/shapes/bentConnector5.svg" height="50" width="50"></p>
bentUpArrow | شكل سهم منحني | <p style="text-align: center;"><img src="../images/shapes/bentUpArrow.svg" height="50" width="50"></p>
bevel | شكل شطبة | <p style="text-align: center;"><img src="../images/shapes/bevel.svg" height="50" width="50"></p>
blockArc | كتلة على شكل قوس | <p style="text-align: center;"><img src="../images/shapes/blockArc.svg" height="50" width="50"></p>
borderCallout1 | وسيلة الشرح 1 مع شكل الحدود | <p style="text-align: center;"><img src="../images/shapes/borderCallout1.svg" height="50" width="50"></p>
borderCallout2 | وسيلة الشرح 2 مع شكل الحدود | <p style="text-align: center;"><img src="../images/shapes/borderCallout2.svg" height="50" width="50"></p>
borderCallout3 | وسيلة الشرح 3 مع شكل الحدود | <p style="text-align: center;"><img src="../images/shapes/borderCallout3.svg" height="50" width="50"></p>
bracePair | شكل زوج الدعامة | <p style="text-align: center;"><img src="../images/shapes/bracePair.svg" height="50" width="50"></p>
bracketPair | شكل زوج القوس | <p style="text-align: center;"><img src="../images/shapes/bracketPair.svg" height="50" width="50"></p>
callout1 | شكل وسيلة الشرح 1 | <p style="text-align: center;"><img src="../images/shapes/callout1.svg" height="50" width="50"></p>
callout2 | شكل وسيلة الشرح 2 | <p style="text-align: center;"><img src="../images/shapes/callout2.svg" height="50" width="50"></p>
callout3 | شكل وسيلة الشرح 3 | <p style="text-align: center;"><img src="../images/shapes/callout3.svg" height="50" width="50"></p>
can | يمكن أن تشكل | <p style="text-align: center;"><img src="../images/shapes/can.svg" height="50" width="50"></p>
chartPlus | مخطط زائد الشكل | <p style="text-align: center;"><img src="../images/shapes/chartPlus.svg" height="50" width="50"></p>
chartStar | شكل نجمة الرسم البياني | <p style="text-align: center;"><img src="../images/shapes/chartStar.svg" height="50" width="50"></p>
chartX | شكل X المخطط | <p style="text-align: center;"><img src="../images/shapes/chartX.svg" height="50" width="50"></p>
chevron | شكل شيفرون | <p style="text-align: center;"><img src="../images/shapes/chevron.svg" height="50" width="50"></p>
chord | شكل وتر | <p style="text-align: center;"><img src="../images/shapes/chord.svg" height="50" width="50"></p>
circularArrow | شكل سهم دائري | <p style="text-align: center;"><img src="../images/shapes/circularArrow.svg" height="50" width="50"></p>
cloud | شكل السحابة | <p style="text-align: center;"><img src="../images/shapes/cloud.svg" height="50" width="50"></p>
cloudCallout | وسيلة شرح شكل سحابة | <p style="text-align: center;"><img src="../images/shapes/cloudCallout.svg" height="50" width="50"></p>
corner | شكل الزاوية | <p style="text-align: center;"><img src="../images/shapes/corner.svg" height="50" width="50"></p>
cornerTabs | شكل علامات تبويب الزاوية | <p style="text-align: center;"><img src="../images/shapes/cornerTabs.svg" height="50" width="50"></p>
cube | شكل مكعب | <p style="text-align: center;"><img src="../images/shapes/cube.svg" height="50" width="50"></p>
curvedConnector2 | موصل منحن 2 شكل | <p style="text-align: center;"><img src="../images/shapes/curvedConnector2.svg" height="50" width="50"></p>
curvedConnector3 | موصل منحن 3 شكل | <p style="text-align: center;"><img src="../images/shapes/curvedConnector3.svg" height="50" width="50"></p>
curvedConnector4 | موصل منحن 4 شكل | <p style="text-align: center;"><img src="../images/shapes/curvedConnector4.svg" height="50" width="50"></p>
curvedConnector5 | موصل منحن 5 شكل | <p style="text-align: center;"><img src="../images/shapes/curvedConnector5.svg" height="50" width="50"></p>
curvedDownArrow | شكل سهم منحني لأسفل | <p style="text-align: center;"><img src="../images/shapes/curvedDownArrow.svg" height="50" width="50"></p>
curvedLeftArrow | شكل السهم الأيسر المنحني | <p style="text-align: center;"><img src="../images/shapes/curvedLeftArrow.svg" height="50" width="50"></p>
curvedRightArrow | شكل السهم الأيمن المنحني | <p style="text-align: center;"><img src="../images/shapes/curvedRightArrow.svg" height="50" width="50"></p>
curvedUpArrow | منحني شكل سهم لأعلى | <p style="text-align: center;"><img src="../images/shapes/curvedUpArrow.svg" height="50" width="50"></p>
decagon | شكل عشري | <p style="text-align: center;"><img src="../images/shapes/decagon.svg" height="50" width="50"></p>
diagStripe | شكل شريط قطري | <p style="text-align: center;"><img src="../images/shapes/diagStripe.svg" height="50" width="50"></p>
diamond | شكل الماس | <p style="text-align: center;"><img src="../images/shapes/diamond.svg" height="50" width="50"></p>
dodecagon | شكل Dodecagon | <p style="text-align: center;"><img src="../images/shapes/dodecagon.svg" height="50" width="50"></p>
donut | شكل دونات | <p style="text-align: center;"><img src="../images/shapes/donut.svg" height="50" width="50"></p>
doubleWave | شكل موجة مزدوجة | <p style="text-align: center;"><img src="../images/shapes/doubleWave.svg" height="50" width="50"></p>
downArrow | شكل السهم لأسفل | <p style="text-align: center;"><img src="../images/shapes/downArrow.svg" height="50" width="50"></p>
downArrowCallout | وسيلة شرح شكل سهم لأسفل | <p style="text-align: center;"><img src="../images/shapes/downArrowCallout.svg" height="50" width="50"></p>
ellipse | شكل القطع الناقص | <p style="text-align: center;"><img src="../images/shapes/ellipse.svg" height="50" width="50"></p>
ellipseRibbon | شكل الشريط الناقص | <p style="text-align: center;"><img src="../images/shapes/ellipseRibbon.svg" height="50" width="50"></p>
ellipseRibbon2 | الشريط الناقص 2 الشكل | <p style="text-align: center;"><img src="../images/shapes/ellipseRibbon2.svg" height="50" width="50"></p>
flowChartAlternateProcess | شكل تدفق العملية البديل | <p style="text-align: center;"><img src="../images/shapes/flowChartAlternateProcess.svg" height="50" width="50"></p>
flowChartCollate | ترتيب شكل التدفق | <p style="text-align: center;"><img src="../images/shapes/flowChartCollate.svg" height="50" width="50"></p>
flowChartConnector | شكل تدفق الموصل | <p style="text-align: center;"><img src="../images/shapes/flowChartConnector.svg" height="50" width="50"></p>
flowChartDecision | شكل تدفق القرار | <p style="text-align: center;"><img src="../images/shapes/flowChartDecision.svg" height="50" width="50"></p>
flowChartDelay | شكل تدفق التأخير | <p style="text-align: center;"><img src="../images/shapes/flowChartDelay.svg" height="50" width="50"></p>
flowChartDisplay | عرض شكل التدفق | <p style="text-align: center;"><img src="../images/shapes/flowChartDisplay.svg" height="50" width="50"></p>
flowChartDocument | شكل تدفق المستند | <p style="text-align: center;"><img src="../images/shapes/flowChartDocument.svg" height="50" width="50"></p>
flowChartExtract | استخراج شكل التدفق | <p style="text-align: center;"><img src="../images/shapes/flowChartExtract.svg" height="50" width="50"></p>
flowChartInputOutput | شكل تدفق الإدخال والإخراج | <p style="text-align: center;"><img src="../images/shapes/flowChartInternalStorage.svg" height="50" width="50"></p>
flowChartInternalStorage | شكل تدفق التخزين الداخلي | <p style="text-align: center;"><img src="../images/shapes/flowChartInternalStorage.svg" height="50" width="50"></p>
flowChartMagneticDisk | شكل تدفق القرص المغناطيسي | <p style="text-align: center;"><img src="../images/shapes/flowChartMagneticDisk.svg" height="50" width="50"></p>
flowChartMagneticDrum | شكل تدفق الأسطوانة المغناطيسية | <p style="text-align: center;"><img src="../images/shapes/flowChartMagneticDrum.svg" height="50" width="50"></p>
flowChartMagneticTape | شكل تدفق الشريط المغناطيسي | <p style="text-align: center;"><img src="../images/shapes/flowChartMagneticTape.svg" height="50" width="50"></p>
flowChartManualInput | شكل تدفق الإدخال اليدوي | <p style="text-align: center;"><img src="../images/shapes/flowChartManualInput.svg" height="50" width="50"></p>
flowChartManualOperation | شكل تدفق التشغيل اليدوي | <p style="text-align: center;"><img src="../images/shapes/flowChartManualOperation.svg" height="50" width="50"></p>
flowChartMerge | دمج شكل التدفق | <p style="text-align: center;"><img src="../images/shapes/flowChartMerge.svg" height="50" width="50"></p>
flowChartMultidocument | شكل تدفق متعدد المستندات | <p style="text-align: center;"><img src="../images/shapes/flowChartMultidocument.svg" height="50" width="50"></p>
flowChartOfflineStorage | شكل تدفق التخزين دون اتصال | <p style="text-align: center;"><img src="../images/shapes/flowChartOfflineStorage.svg" height="50" width="50"></p>
flowChartOffpageConnector | شكل تدفق الموصل خارج الصفحة | <p style="text-align: center;"><img src="../images/shapes/flowChartOffpageConnector.svg" height="50" width="50"></p>
flowChartOnlineStorage | شكل تدفق التخزين عبر الإنترنت | <p style="text-align: center;"><img src="../images/shapes/flowChartOnlineStorage.svg" height="50" width="50"></p>
flowChartOr | أو شكل التدفق | <p style="text-align: center;"><img src="../images/shapes/flowChartOr.svg" height="50" width="50"></p>
flowChartPredefinedProcess | شكل تدفق العملية المحدد مسبقًا | <p style="text-align: center;"><img src="../images/shapes/flowChartPredefinedProcess.svg" height="50" width="50"></p>
flowChartPreparation | شكل تدفق التحضير | <p style="text-align: center;"><img src="../images/shapes/flowChartPredefinedProcess.svg" height="50" width="50"></p>
flowChartProcess | شكل تدفق العملية | <p style="text-align: center;"><img src="../images/shapes/flowChartPreparation.svg" height="50" width="50"></p>
flowChartPunchedCard | شكل تدفق بطاقة مثقوبة | <p style="text-align: center;"><img src="../images/shapes/flowChartPunchedCard.svg" height="50" width="50"></p>
flowChartPunchedTape | شكل تدفق الشريط المثقوب | <p style="text-align: center;"><img src="../images/shapes/flowChartPunchedTape.svg" height="50" width="50"></p>
flowChartSort | فرز شكل التدفق | <p style="text-align: center;"><img src="../images/shapes/flowChartSort.svg" height="50" width="50"></p>
flowChartSummingJunction | جمع شكل تدفق التقاطع | <p style="text-align: center;"><img src="../images/shapes/flowChartSummingJunction.svg" height="50" width="50"></p>
flowChartTerminator | شكل تدفق المنهي | <p style="text-align: center;"><img src="../images/shapes/flowChartTerminator.svg" height="50" width="50"></p>
foldedCorner | زاوية مطوية | <p style="text-align: center;"><img src="../images/shapes/foldedCorner.svg" height="50" width="50"></p>
frame | شكل الإطار | <p style="text-align: center;"><img src="../images/shapes/frame.svg" height="50" width="50"></p>
funnel | شكل قمع | <p style="text-align: center;"><img src="../images/shapes/funnel.svg" height="50" width="50"></p>
gear6 | جير 6 شكل | <p style="text-align: center;"><img src="../images/shapes/gear6.svg" height="50" width="50"></p>
gear9 | جير 9 شكل | <p style="text-align: center;"><img src="../images/shapes/gear9.svg" height="50" width="50"></p>
halfFrame | نصف شكل إطار | <p style="text-align: center;"><img src="../images/shapes/halfFrame.svg" height="50" width="50"></p>
heart | شكل القلب | <p style="text-align: center;"><img src="../images/shapes/heart.svg" height="50" width="50"></p>
heptagon | شكل سباعي | <p style="text-align: center;"><img src="../images/shapes/heptagon.svg" height="50" width="50"></p>
hexagon | الشكل السداسي | <p style="text-align: center;"><img src="../images/shapes/hexagon.svg" height="50" width="50"></p>
homePlate | شكل لوحة المنزل | <p style="text-align: center;"><img src="../images/shapes/homePlate.svg" height="50" width="50"></p>
horizontalScroll | شكل التمرير الأفقي | <p style="text-align: center;"><img src="../images/shapes/horizontalScroll.svg" height="50" width="50"></p>
irregularSeal1 | شكل الختم غير المنتظم 1 | <p style="text-align: center;"><img src="../images/shapes/irregularSeal1.svg" height="50" width="50"></p>
irregularSeal2 | شكل الختم غير المنتظم 2 | <p style="text-align: center;"><img src="../images/shapes/irregularSeal2.svg" height="50" width="50"></p>
leftArrow | شكل السهم الأيسر | <p style="text-align: center;"><img src="../images/shapes/leftArrow.svg" height="50" width="50"></p>
leftArrowCallout | وسيلة شرح شكل السهم الأيسر | <p style="text-align: center;"><img src="../images/shapes/leftArrowCallout.svg" height="50" width="50"></p>
leftBrace | الأيسر هدفين الشكل | <p style="text-align: center;"><img src="../images/shapes/leftBrace.svg" height="50" width="50"></p>
leftBracket | شكل القوس الأيسر | <p style="text-align: center;"><img src="../images/shapes/leftBracket.svg" height="50" width="50"></p>
leftCircularArrow | شكل سهم دائري يسار | <p style="text-align: center;"><img src="../images/shapes/leftCircularArrow.svg" height="50" width="50"></p>
leftRightArrow | شكل السهم الأيمن الأيسر | <p style="text-align: center;"><img src="../images/shapes/leftRightArrow.svg" height="50" width="50"></p>
leftRightArrowCallout | وسيلة شرح شكل سهم يسار يمين | <p style="text-align: center;"><img src="../images/shapes/leftRightArrowCallout.svg" height="50" width="50"></p>
leftRightCircularArrow | شكل السهم الدائري الأيمن الأيسر | <p style="text-align: center;"><img src="../images/shapes/leftRightCircularArrow.svg" height="50" width="50"></p>
leftRightRibbon | شكل الشريط الأيمن الأيسر | <p style="text-align: center;"><img src="../images/shapes/leftRightRibbon.svg" height="50" width="50"></p>
leftRightUpArrow | اليسار واليمين لأعلى شكل السهم | <p style="text-align: center;"><img src="../images/shapes/leftRightUpArrow.svg" height="50" width="50"></p>
leftUpArrow | شكل سهم لليسار لأعلى | <p style="text-align: center;"><img src="../images/shapes/leftUpArrow.svg" height="50" width="50"></p>
lightningBolt | شكل صاعقة البرق | <p style="text-align: center;"><img src="../images/shapes/lightningBolt.svg" height="50" width="50"></p>
line | شكل خط | <p style="text-align: center;"><img src="../images/shapes/line.svg" height="50" width="50"></p>
lineInv | شكل خط معكوس | <p style="text-align: center;"><img src="../images/shapes/lineInv.svg" height="50" width="50"></p>
mathDivide | قسّم الشكل الرياضي | <p style="text-align: center;"><img src="../images/shapes/mathDivide.svg" height="50" width="50"></p>
mathEqual | شكل رياضيات متساوية | <p style="text-align: center;"><img src="../images/shapes/mathEqual.svg" height="50" width="50"></p>
mathMinus | شكل ناقص الرياضيات | <p style="text-align: center;"><img src="../images/shapes/mathMinus.svg" height="50" width="50"></p>
mathMultiply | اضرب الشكل الرياضي | <p style="text-align: center;"><img src="../images/shapes/mathMultiply.svg" height="50" width="50"></p>
mathNotEqual | غير متكافئ الرياضيات الشكل | <p style="text-align: center;"><img src="../images/shapes/mathNotEqual.svg" height="50" width="50"></p>
mathPlus | بالإضافة إلى شكل الرياضيات | <p style="text-align: center;"><img src="../images/shapes/mathPlus.svg" height="50" width="50"></p>
moon | شكل القمر | <p style="text-align: center;"><img src="../images/shapes/moon.svg" height="50" width="50"></p>
nonIsoscelesTrapezoid | شكل شبه منحرف غير متساوي الساقين | <p style="text-align: center;"><img src="../images/shapes/nonIsoscelesTrapezoid.svg" height="50" width="50"></p>
noSmoking | شكل ممنوع التدخين | <p style="text-align: center;"><img src="../images/shapes/noSmoking.svg" height="50" width="50"></p>
notchedRightArrow | شكل السهم الأيمن | <p style="text-align: center;"><img src="../images/shapes/notchedRightArrow.svg" height="50" width="50"></p>
octagon | شكل المثمن | <p style="text-align: center;"><img src="../images/shapes/octagon.svg" height="50" width="50"></p>
parallelogram | شكل متوازي الأضلاع | <p style="text-align: center;"><img src="../images/shapes/parallelogram.svg" height="50" width="50"></p>
pentagon | شكل البنتاغون | <p style="text-align: center;"><img src="../images/shapes/pentagon.svg" height="50" width="50"></p>
pie | شكل فطيرة | <p style="text-align: center;"><img src="../images/shapes/pie.svg" height="50" width="50"></p>
pieWedge | شكل فطيرة الوتد | <p style="text-align: center;"><img src="../images/shapes/pieWedge.svg" height="50" width="50"></p>
plaque | شكل البلاك | <p style="text-align: center;"><img src="../images/shapes/plaque.svg" height="50" width="50"></p>
plaqueTabs | شكل علامات البلاك | <p style="text-align: center;"><img src="../images/shapes/plaqueTabs.svg" height="50" width="50"></p>
plus | شكل زائد | <p style="text-align: center;"><img src="../images/shapes/plus.svg" height="50" width="50"></p>
quadArrow | شكل رباعي السهم | <p style="text-align: center;"><img src="../images/shapes/quadArrow.svg" height="50" width="50"></p>
quadArrowCallout | وسيلة شرح شكل رباعي السهم | <p style="text-align: center;"><img src="../images/shapes/quadArrowCallout.svg" height="50" width="50"></p>
rect | شكل مستطيل | <p style="text-align: center;"><img src="../images/shapes/rect.svg" height="50" width="50"></p>
ribbon | شكل الشريط | <p style="text-align: center;"><img src="../images/shapes/ribbon.svg" height="50" width="50"></p>
ribbon2 | شكل الشريط 2 | <p style="text-align: center;"><img src="../images/shapes/ribbon2.svg" height="50" width="50"></p>
rightArrow | شكل السهم الأيمن | <p style="text-align: center;"><img src="../images/shapes/rightArrow.svg" height="50" width="50"></p>
rightArrowCallout | وسيلة شرح شكل السهم الأيمن | <p style="text-align: center;"><img src="../images/shapes/rightArrowCallout.svg" height="50" width="50"></p>
rightBrace | شكل القوس الأيمن | <p style="text-align: center;"><img src="../images/shapes/rightBrace.svg" height="50" width="50"></p>
rightBracket | شكل القوس الأيمن | <p style="text-align: center;"><img src="../images/shapes/rightBracket.svg" height="50" width="50"></p>
round1Rect | زاوية مستديرة واحدة الشكل | <p style="text-align: center;"><img src="../images/shapes/round1Rect.svg" height="50" width="50"></p>
round2DiagRect | اثنان قطري زاوية مستطيل الشكل | <p style="text-align: center;"><img src="../images/shapes/round2DiagRect.svg" height="50" width="50"></p>
round2SameRect | اثنان من نفس الجانب مستطيل الشكل الزاوية | <p style="text-align: center;"><img src="../images/shapes/round2SameRect.svg" height="50" width="50"></p>
roundRect | مستدير الزاوية مستطيل الشكل | <p style="text-align: center;"><img src="../images/shapes/roundRect.svg" height="50" width="50"></p>
rtTriangle | شكل مثلث قائم | <p style="text-align: center;"><img src="../images/shapes/rtTriangle.svg" height="50" width="50"></p>
smileyFace |شكل وجه مبتسم | <p style="text-align: center;"><img src="../images/shapes/smileyFace.svg" height="50" width="50"></p>
snip1Rect | شكل مستطيل ذو زاوية قص واحدة | <p style="text-align: center;"><img src="../images/shapes/snip1Rect.svg" height="50" width="50"></p>
snip2DiagRect | شكل مستطيل ذو زاويتين قصائيتين قطريتين | <p style="text-align: center;"><img src="../images/shapes/snip2DiagRect.svg" height="50" width="50"></p>
snip2SameRect | شكل مستطيل بزاوية قص ذات جانبين | <p style="text-align: center;"><img src="../images/shapes/snip2SameRect.svg" height="50" width="50"></p>
snipRoundRect | مقطع واحد مستطيل ذو زاوية مستديرة | <p style="text-align: center;"><img src="../images/shapes/snipRoundRect.svg" height="50" width="50"></p>
squareTabs | شكل علامات التبويب المربعة | <p style="text-align: center;"><img src="../images/shapes/squareTabs.svg" height="50" width="50"></p>
star10 | عشر شكل نجمة مدببة | <p style="text-align: center;"><img src="../images/shapes/star10.svg" height="50" width="50"></p>
star12 | اثني عشر شكل نجمة مدببة | <p style="text-align: center;"><img src="../images/shapes/star12.svg" height="50" width="50"></p>
star16 | ستة عشر شكل نجمة مدببة | <p style="text-align: center;"><img src="../images/shapes/star16.svg" height="50" width="50"></p>
star24 | أربع وعشرون نجمة مدببة الشكل | <p style="text-align: center;"><img src="../images/shapes/star24.svg" height="50" width="50"></p>
star32 | اثنان وثلاثون شكل نجمة مدببة | <p style="text-align: center;"><img src="../images/shapes/star32.svg" height="50" width="50"></p>
star4 | أربع شكل نجمة مدببة | <p style="text-align: center;"><img src="../images/shapes/star4.svg" height="50" width="50"></p>
star5 | شكل نجمة خماسية | <p style="text-align: center;"><img src="../images/shapes/star5.svg" height="50" width="50"></p>
star6 | شكل نجمة سداسية | <p style="text-align: center;"><img src="../images/shapes/star6.svg" height="50" width="50"></p>
star7 | شكل نجمة سبعة مدببة | <p style="text-align: center;"><img src="../images/shapes/star7.svg" height="50" width="50"></p>
star8 | ثمانية شكل نجمة مدببة | <p style="text-align: center;"><img src="../images/shapes/star8.svg" height="50" width="50"></p>
straightConnector1 | موصل مستقيم 1 الشكل | <p style="text-align: center;"><img src="../images/shapes/straightConnector1.svg" height="50" width="50"></p>
stripedRightArrow | شكل سهم لليمين مخطط | <p style="text-align: center;"><img src="../images/shapes/stripedRightArrow.svg" height="50" width="50"></p>
sun | شكل الشمس | <p style="text-align: center;"><img src="../images/shapes/sun.svg" height="50" width="50"></p>
swooshArrow | شكل سهم سووش | <p style="text-align: center;"><img src="../images/shapes/swooshArrow.svg" height="50" width="50"></p>
teardrop | شكل الدمعة | <p style="text-align: center;"><img src="../images/shapes/teardrop.svg" height="50" width="50"></p>
trapezoid | شكل شبه منحرف | <p style="text-align: center;"><img src="../images/shapes/trapezoid.svg" height="50" width="50"></p>
triangle | شكل مثلث | <p style="text-align: center;"><img src="../images/shapes/triangle.svg" height="50" width="50"></p>
upArrow | شكل السهم لأعلى | <p style="text-align: center;"><img src="../images/shapes/upArrow.svg" height="50" width="50"></p>
upArrowCallout | وسيلة شرح السهم لأعلى | <p style="text-align: center;"><img src="../images/shapes/upArrowCallout.svg" height="50" width="50"></p>
upDownArrow | لأعلى سهم لأسفل الشكل | <p style="text-align: center;"><img src="../images/shapes/upDownArrow.svg" height="50" width="50"></p>
upDownArrowCallout | وسيلة شرح لأعلى سهم لأسفل الشكل | <p style="text-align: center;"><img src="../images/shapes/upDownArrowCallout.svg" height="50" width="50"></p>
uturnArrow | شكل السهم U-Turn | <p style="text-align: center;"><img src="../images/shapes/uturnArrow.svg" height="50" width="50"></p>
verticalScroll | شكل التمرير العمودي | <p style="text-align: center;"><img src="../images/shapes/verticalScroll.svg" height="50" width="50"></p>
wave | شكل متموج | <p style="text-align: center;"><img src="../images/shapes/wave.svg" height="50" width="50"></p>
wedgeEllipseCallout | وسيلة شرح إسفين الشكل البيضاوي | <p style="text-align: center;"><img src="../images/shapes/wedgeEllipseCallout.svg" height="50" width="50"></p>
wedgeRectCallout | وسيلة شرح مستطيل إسفين الشكل | <p style="text-align: center;"><img src="../images/shapes/wedgeRectCallout.svg" height="50" width="50"></p>
wedgeRoundRectCallout | وسيلة شرح إسفين مستدير الشكل  | <p style="text-align: center;"><img src="../images/shapes/wedgeRoundRectCallout.svg" height="50" width="50"></p>
