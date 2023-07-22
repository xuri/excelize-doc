# 도형

## 셰이프 추가

```go
func (f *File) AddShape(sheet string, opts *Shape) error
```

AddShape는 지정된 워크시트 인덱스, 모양 형식 집합(예: 간격띄우기, 축척, 종횡비 설정 및 인쇄 설정) 및 속성 집합을 사용하여 시트에 셰이프를 추가하는 방법을 제공합니다. 예를 들어 `Sheet1` 에 텍스트 상자 (직사각형 모양) 를 추가합니다:

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

다음은 excelize 에서 지원하는 셰이프 유형을 보여 주며 다음과 같은 것입니다:

유형|모양|스타일
---|---|---
accentBorderCallout1 | 테두리 및 악센트 모양이 있는 설명선 1 | <p style="text-align: center;"><img src="../images/shapes/accentBorderCallout1.svg" height="50" width="50"></p>
accentBorderCallout2 | 테두리 및 악센트 모양이 있는 설명선 2 | <p style="text-align: center;"><img src="../images/shapes/accentBorderCallout2.svg" height="50" width="50"></p>
accentBorderCallout3 | 테두리 및 악센트 모양이 있는 설명선 3 | <p style="text-align: center;"><img src="../images/shapes/accentBorderCallout3.svg" height="50" width="50"></p>
accentCallout1 | 설명선 1 모양 | <p style="text-align: center;"><img src="../images/shapes/accentCallout1.svg" height="50" width="50"></p>
accentCallout2 | 설명선 2 모양| <p style="text-align: center;"><img src="../images/shapes/accentCallout2.svg" height="50" width="50"></p>
accentCallout3 | 설명선 3 모양 | <p style="text-align: center;"><img src="../images/shapes/accentCallout3.svg" height="50" width="50"></p>
actionButtonBackPrevious | 뒤로 또는 이전 버튼 모양 | <p style="text-align: center;"><img src="../images/shapes/actionButtonBackPrevious.svg" height="50" width="50"></p>
actionButtonBeginning | 시작 단추 모양 | <p style="text-align: center;"><img src="../images/shapes/actionButtonBeginning.svg" height="50" width="50"></p>
actionButtonBlank | 빈 버튼 모양 | <p style="text-align: center;"><img src="../images/shapes/actionButtonBlank.svg" height="50" width="50"></p>
actionButtonDocument | 문서 단추 모양 | <p style="text-align: center;"><img src="../images/shapes/actionButtonDocument.svg" height="50" width="50"></p>
actionButtonEnd | 종료 버튼 모양 | <p style="text-align: center;"><img src="../images/shapes/actionButtonEnd.svg" height="50" width="50"></p>
actionButtonForwardNext | 앞으로 또는 다음 버튼 모양 | <p style="text-align: center;"><img src="../images/shapes/actionButtonForwardNext.svg" height="50" width="50"></p>
actionButtonHelp | 도움말 버튼 모양 | <p style="text-align: center;"><img src="../images/shapes/actionButtonHelp.svg" height="50" width="50"></p>
actionButtonHome | 홈 버튼 모양 | <p style="text-align: center;"><img src="../images/shapes/actionButtonHome.svg" height="50" width="50"></p>
actionButtonInformation | 정보 버튼 모양 | <p style="text-align: center;"><img src="../images/shapes/actionButtonInformation.svg" height="50" width="50"></p>
actionButtonMovie | 동영상 버튼 모양 | <p style="text-align: center;"><img src="../images/shapes/actionButtonMovie.svg" height="50" width="50"></p>
actionButtonReturn | 리턴 버튼 모양 | <p style="text-align: center;"><img src="../images/shapes/actionButtonReturn.svg" height="50" width="50"></p>
actionButtonSound | 사운드 버튼 모양 | <p style="text-align: center;"><img src="../images/shapes/actionButtonSound.svg" height="50" width="50"></p>
arc | 곡선 아크 모양 | <p style="text-align: center;"><img src="../images/shapes/arc.svg" height="50" width="50"></p>
bentArrow | 구부러진 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/bentArrow.svg" height="50" width="50"></p>
bentConnector2 | 구부러진 커넥터 2 모양 | <p style="text-align: center;"><img src="../images/shapes/bentConnector2.svg" height="50" width="50"></p>
bentConnector3 | 구부러진 커넥터 3 모양 | <p style="text-align: center;"><img src="../images/shapes/bentConnector3.svg" height="50" width="50"></p>
bentConnector4 | 구부러진 커넥터 4 모양 | <p style="text-align: center;"><img src="../images/shapes/bentConnector4.svg" height="50" width="50"></p>
bentConnector5 | 구부러진 커넥터 5 모양 | <p style="text-align: center;"><img src="../images/shapes/bentConnector5.svg" height="50" width="50"></p>
bentUpArrow | 구부러진 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/bentUpArrow.svg" height="50" width="50"></p>
bevel | 베벨 모양 | <p style="text-align: center;"><img src="../images/shapes/bevel.svg" height="50" width="50"></p>
blockArc | 블록 호 모양 | <p style="text-align: center;"><img src="../images/shapes/blockArc.svg" height="50" width="50"></p>
borderCallout1 | 테두리 모양이 있는 설명선 1 | <p style="text-align: center;"><img src="../images/shapes/borderCallout1.svg" height="50" width="50"></p>
borderCallout2 | 테두리 모양이 있는 설명선 2 | <p style="text-align: center;"><img src="../images/shapes/borderCallout2.svg" height="50" width="50"></p>
borderCallout3 | 테두리 모양이 있는 설명선 3 | <p style="text-align: center;"><img src="../images/shapes/borderCallout3.svg" height="50" width="50"></p>
bracePair | 가새 쌍 모양 | <p style="text-align: center;"><img src="../images/shapes/bracePair.svg" height="50" width="50"></p>
bracketPair | 브래킷 쌍 모양 | <p style="text-align: center;"><img src="../images/shapes/bracketPair.svg" height="50" width="50"></p>
callout1 | 설명선 1 모양 | <p style="text-align: center;"><img src="../images/shapes/callout1.svg" height="50" width="50"></p>
callout2 | 설명선 2 모양 | <p style="text-align: center;"><img src="../images/shapes/callout2.svg" height="50" width="50"></p>
callout3 | 설명선 3 모양 | <p style="text-align: center;"><img src="../images/shapes/callout3.svg" height="50" width="50"></p>
can | 캔 셰이프 | <p style="text-align: center;"><img src="../images/shapes/can.svg" height="50" width="50"></p>
chartPlus | 차트 더하기 모양 | <p style="text-align: center;"><img src="../images/shapes/chartPlus.svg" height="50" width="50"></p>
chartStar | 차트 별 모양 | <p style="text-align: center;"><img src="../images/shapes/chartStar.svg" height="50" width="50"></p>
chartX | 차트 X 모양 | <p style="text-align: center;"><img src="../images/shapes/chartX.svg" height="50" width="50"></p>
chevron | 쉐브론 모양 | <p style="text-align: center;"><img src="../images/shapes/chevron.svg" height="50" width="50"></p>
chord | 현 모양 | <p style="text-align: center;"><img src="../images/shapes/chord.svg" height="50" width="50"></p>
circularArrow | 원형 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/circularArrow.svg" height="50" width="50"></p>
cloud | 구름 모양 | <p style="text-align: center;"><img src="../images/shapes/cloud.svg" height="50" width="50"></p>
cloudCallout | 설명선 구름 모양 | <p style="text-align: center;"><img src="../images/shapes/cloudCallout.svg" height="50" width="50"></p>
corner | 모서리 모양 | <p style="text-align: center;"><img src="../images/shapes/corner.svg" height="50" width="50"></p>
cornerTabs | 코너 탭 모양 | <p style="text-align: center;"><img src="../images/shapes/cornerTabs.svg" height="50" width="50"></p>
cube | 큐브 모양 | <p style="text-align: center;"><img src="../images/shapes/cube.svg" height="50" width="50"></p>
curvedConnector2 | 곡선 커넥터 2 모양 | <p style="text-align: center;"><img src="../images/shapes/curvedConnector2.svg" height="50" width="50"></p>
curvedConnector3 | 곡선 커넥터 3 모양 | <p style="text-align: center;"><img src="../images/shapes/curvedConnector3.svg" height="50" width="50"></p>
curvedConnector4 | 곡선 커넥터 4 모양 | <p style="text-align: center;"><img src="../images/shapes/curvedConnector4.svg" height="50" width="50"></p>
curvedConnector5 | 곡선 커넥터 5 모양 | <p style="text-align: center;"><img src="../images/shapes/curvedConnector5.svg" height="50" width="50"></p>
curvedDownArrow | 아래로 구부러진 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/curvedDownArrow.svg" height="50" width="50"></p>
curvedLeftArrow | 구부러진 왼쪽 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/curvedLeftArrow.svg" height="50" width="50"></p>
curvedRightArrow | 구부러진 오른쪽 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/curvedRightArrow.svg" height="50" width="50"></p>
curvedUpArrow | 위로 구부러진 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/curvedUpArrow.svg" height="50" width="50"></p>
decagon | 십각형 모양 | <p style="text-align: center;"><img src="../images/shapes/decagon.svg" height="50" width="50"></p>
diagStripe | 대각선 줄무늬 모양 | <p style="text-align: center;"><img src="../images/shapes/diagStripe.svg" height="50" width="50"></p>
diamond | 다이아몬드 모양 | <p style="text-align: center;"><img src="../images/shapes/diamond.svg" height="50" width="50"></p>
dodecagon | 십이각형 모양 | <p style="text-align: center;"><img src="../images/shapes/dodecagon.svg" height="50" width="50"></p>
donut | 도넛 모양 | <p style="text-align: center;"><img src="../images/shapes/donut.svg" height="50" width="50"></p>
doubleWave | 더블 웨이브 모양 | <p style="text-align: center;"><img src="../images/shapes/doubleWave.svg" height="50" width="50"></p>
downArrow | 아래쪽 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/downArrow.svg" height="50" width="50"></p>
downArrowCallout | 설명선 아래쪽 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/downArrowCallout.svg" height="50" width="50"></p>
ellipse | 타원 모양 | <p style="text-align: center;"><img src="../images/shapes/ellipse.svg" height="50" width="50"></p>
ellipseRibbon | 타원 리본 모양 | <p style="text-align: center;"><img src="../images/shapes/ellipseRibbon.svg" height="50" width="50"></p>
ellipseRibbon2 | 타원 리본 2 모양 | <p style="text-align: center;"><img src="../images/shapes/ellipseRibbon2.svg" height="50" width="50"></p>
flowChartAlternateProcess | 대체 프로세스 흐름 형태 | <p style="text-align: center;"><img src="../images/shapes/flowChartAlternateProcess.svg" height="50" width="50"></p>
flowChartCollate | 분류 흐름 모양 | <p style="text-align: center;"><img src="../images/shapes/flowChartCollate.svg" height="50" width="50"></p>
flowChartConnector | 커넥터 흐름 모양 | <p style="text-align: center;"><img src="../images/shapes/flowChartConnector.svg" height="50" width="50"></p>
flowChartDecision | 의사 결정 흐름 형태 | <p style="text-align: center;"><img src="../images/shapes/flowChartDecision.svg" height="50" width="50"></p>
flowChartDelay | 지연 흐름 모양 | <p style="text-align: center;"><img src="../images/shapes/flowChartDelay.svg" height="50" width="50"></p>
flowChartDisplay | 디스플레이 흐름 모양 | <p style="text-align: center;"><img src="../images/shapes/flowChartDisplay.svg" height="50" width="50"></p>
flowChartDocument | 문서 흐름 형태 | <p style="text-align: center;"><img src="../images/shapes/flowChartDocument.svg" height="50" width="50"></p>
flowChartExtract | 흐름 형태 추출 | <p style="text-align: center;"><img src="../images/shapes/flowChartExtract.svg" height="50" width="50"></p>
flowChartInputOutput | 입력 출력 흐름 형태 | <p style="text-align: center;"><img src="../images/shapes/flowChartInternalStorage.svg" height="50" width="50"></p>
flowChartInternalStorage | 내부 저장 흐름 형태 | <p style="text-align: center;"><img src="../images/shapes/flowChartInternalStorage.svg" height="50" width="50"></p>
flowChartMagneticDisk | 자기 디스크 흐름 모양 | <p style="text-align: center;"><img src="../images/shapes/flowChartMagneticDisk.svg" height="50" width="50"></p>
flowChartMagneticDrum | 자기 드럼 흐름 모양 | <p style="text-align: center;"><img src="../images/shapes/flowChartMagneticDrum.svg" height="50" width="50"></p>
flowChartMagneticTape | 자기 테이프 흐름 모양 | <p style="text-align: center;"><img src="../images/shapes/flowChartMagneticTape.svg" height="50" width="50"></p>
flowChartManualInput | 수동 입력 흐름 형태 | <p style="text-align: center;"><img src="../images/shapes/flowChartManualInput.svg" height="50" width="50"></p>
flowChartManualOperation | 수동 운전 흐름 형태 | <p style="text-align: center;"><img src="../images/shapes/flowChartManualOperation.svg" height="50" width="50"></p>
flowChartMerge | 흐름 셰이프 병합 | <p style="text-align: center;"><img src="../images/shapes/flowChartMerge.svg" height="50" width="50"></p>
flowChartMultidocument | 다중 문서 흐름 형태 | <p style="text-align: center;"><img src="../images/shapes/flowChartMultidocument.svg" height="50" width="50"></p>
flowChartOfflineStorage | 오프라인 스토리지 흐름 형태 | <p style="text-align: center;"><img src="../images/shapes/flowChartOfflineStorage.svg" height="50" width="50"></p>
flowChartOffpageConnector | 오프 페이지 커넥터 흐름 형태 | <p style="text-align: center;"><img src="../images/shapes/flowChartOffpageConnector.svg" height="50" width="50"></p>
flowChartOnlineStorage | 온라인 스토리지 흐름 형태 | <p style="text-align: center;"><img src="../images/shapes/flowChartOnlineStorage.svg" height="50" width="50"></p>
flowChartOr | 또는 흐름 모양 | <p style="text-align: center;"><img src="../images/shapes/flowChartOr.svg" height="50" width="50"></p>
flowChartPredefinedProcess | 미리 정의된 프로세스 흐름 형태 | <p style="text-align: center;"><img src="../images/shapes/flowChartPredefinedProcess.svg" height="50" width="50"></p>
flowChartPreparation | 준비 흐름 모양 | <p style="text-align: center;"><img src="../images/shapes/flowChartPredefinedProcess.svg" height="50" width="50"></p>
flowChartProcess | 프로세스 흐름 모양 | <p style="text-align: center;"><img src="../images/shapes/flowChartPreparation.svg" height="50" width="50"></p>
flowChartPunchedCard | 천공 카드 흐름 모양 | <p style="text-align: center;"><img src="../images/shapes/flowChartPunchedCard.svg" height="50" width="50"></p>
flowChartPunchedTape | 구멍을 뚫은 테이프 흐름 모양 | <p style="text-align: center;"><img src="../images/shapes/flowChartPunchedTape.svg" height="50" width="50"></p>
flowChartSort | 정렬 흐름 형태 | <p style="text-align: center;"><img src="../images/shapes/flowChartSort.svg" height="50" width="50"></p>
flowChartSummingJunction | 합산 교차점 흐름 모양 | <p style="text-align: center;"><img src="../images/shapes/flowChartSummingJunction.svg" height="50" width="50"></p>
flowChartTerminator | 터미네이터 흐름 모양 | <p style="text-align: center;"><img src="../images/shapes/flowChartTerminator.svg" height="50" width="50"></p>
foldedCorner | 접힌 모서리 모양 | <p style="text-align: center;"><img src="../images/shapes/foldedCorner.svg" height="50" width="50"></p>
frame | 프레임 모양 | <p style="text-align: center;"><img src="../images/shapes/frame.svg" height="50" width="50"></p>
funnel | 깔때기 모양 | <p style="text-align: center;"><img src="../images/shapes/funnel.svg" height="50" width="50"></p>
gear6 | 기어 6 모양 | <p style="text-align: center;"><img src="../images/shapes/gear6.svg" height="50" width="50"></p>
gear9 | 기어 9 모양 | <p style="text-align: center;"><img src="../images/shapes/gear9.svg" height="50" width="50"></p>
halfFrame | 하프 프레임 모양 | <p style="text-align: center;"><img src="../images/shapes/halfFrame.svg" height="50" width="50"></p>
heart | 하트 모양 | <p style="text-align: center;"><img src="../images/shapes/heart.svg" height="50" width="50"></p>
heptagon | 칠각형 모양 | <p style="text-align: center;"><img src="../images/shapes/heptagon.svg" height="50" width="50"></p>
hexagon | 육각형 모양 | <p style="text-align: center;"><img src="../images/shapes/hexagon.svg" height="50" width="50"></p>
homePlate | 홈 플레이트 모양 | <p style="text-align: center;"><img src="../images/shapes/homePlate.svg" height="50" width="50"></p>
horizontalScroll | 가로 스크롤 모양 | <p style="text-align: center;"><img src="../images/shapes/horizontalScroll.svg" height="50" width="50"></p>
irregularSeal1 | 불규칙한 씰 1 모양 | <p style="text-align: center;"><img src="../images/shapes/irregularSeal1.svg" height="50" width="50"></p>
irregularSeal2 | 불규칙한 씰 2 모양 | <p style="text-align: center;"><img src="../images/shapes/irregularSeal2.svg" height="50" width="50"></p>
leftArrow | 왼쪽 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/leftArrow.svg" height="50" width="50"></p>
leftArrowCallout | 설명선 왼쪽 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/leftArrowCallout.svg" height="50" width="50"></p>
leftBrace | 왼쪽 버팀대 모양 | <p style="text-align: center;"><img src="../images/shapes/leftBrace.svg" height="50" width="50"></p>
leftBracket | 왼쪽 브라켓 모양 | <p style="text-align: center;"><img src="../images/shapes/leftBracket.svg" height="50" width="50"></p>
leftCircularArrow | 왼쪽 원형 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/leftCircularArrow.svg" height="50" width="50"></p>
leftRightArrow | 왼쪽 오른쪽 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/leftRightArrow.svg" height="50" width="50"></p>
leftRightArrowCallout | 설명선 왼쪽 오른쪽 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/leftRightArrowCallout.svg" height="50" width="50"></p>
leftRightCircularArrow | 왼쪽 오른쪽 원형 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/leftRightCircularArrow.svg" height="50" width="50"></p>
leftRightRibbon | 왼쪽 오른쪽 리본 모양 | <p style="text-align: center;"><img src="../images/shapes/leftRightRibbon.svg" height="50" width="50"></p>
leftRightUpArrow | 왼쪽 오른쪽 위쪽 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/leftRightUpArrow.svg" height="50" width="50"></p>
leftUpArrow | 왼쪽 위쪽 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/leftUpArrow.svg" height="50" width="50"></p>
lightningBolt | 번개 모양 | <p style="text-align: center;"><img src="../images/shapes/lightningBolt.svg" height="50" width="50"></p>
line | 선 모양 | <p style="text-align: center;"><img src="../images/shapes/line.svg" height="50" width="50"></p>
lineInv | 선의 반대 모양 | <p style="text-align: center;"><img src="../images/shapes/lineInv.svg" height="50" width="50"></p>
mathDivide | 수학 모양 나누기 | <p style="text-align: center;"><img src="../images/shapes/mathDivide.svg" height="50" width="50"></p>
mathEqual | 등호 수학 모양 | <p style="text-align: center;"><img src="../images/shapes/mathEqual.svg" height="50" width="50"></p>
mathMinus | 빼기 수학 모양 | <p style="text-align: center;"><img src="../images/shapes/mathMinus.svg" height="50" width="50"></p>
mathMultiply | 곱하기 수학 모양 | <p style="text-align: center;"><img src="../images/shapes/mathMultiply.svg" height="50" width="50"></p>
mathNotEqual | 같지 않은 수학 모양 | <p style="text-align: center;"><img src="../images/shapes/mathNotEqual.svg" height="50" width="50"></p>
mathPlus | 더하기 수학 모양 | <p style="text-align: center;"><img src="../images/shapes/mathPlus.svg" height="50" width="50"></p>
moon | 달 모양 | <p style="text-align: center;"><img src="../images/shapes/moon.svg" height="50" width="50"></p>
nonIsoscelesTrapezoid | 비등변 사다리꼴 모양 | <p style="text-align: center;"><img src="../images/shapes/nonIsoscelesTrapezoid.svg" height="50" width="50"></p>
noSmoking | 금연 모양 | <p style="text-align: center;"><img src="../images/shapes/noSmoking.svg" height="50" width="50"></p>
notchedRightArrow | 노치 오른쪽 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/notchedRightArrow.svg" height="50" width="50"></p>
octagon | 팔각형 모양 | <p style="text-align: center;"><img src="../images/shapes/octagon.svg" height="50" width="50"></p>
parallelogram | 평행사변형 모양 | <p style="text-align: center;"><img src="../images/shapes/parallelogram.svg" height="50" width="50"></p>
pentagon | 오각형 모양 | <p style="text-align: center;"><img src="../images/shapes/pentagon.svg" height="50" width="50"></p>
pie | 파이 모양 | <p style="text-align: center;"><img src="../images/shapes/pie.svg" height="50" width="50"></p>
pieWedge | 파이 웨지 모양 | <p style="text-align: center;"><img src="../images/shapes/pieWedge.svg" height="50" width="50"></p>
plaque | 플라크 모양 | <p style="text-align: center;"><img src="../images/shapes/plaque.svg" height="50" width="50"></p>
plaqueTabs | 플라크 탭 모양 | <p style="text-align: center;"><img src="../images/shapes/plaqueTabs.svg" height="50" width="50"></p>
plus | 더하기 모양 | <p style="text-align: center;"><img src="../images/shapes/plus.svg" height="50" width="50"></p>
quadArrow | 쿼드 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/quadArrow.svg" height="50" width="50"></p>
quadArrowCallout | 콜아웃 쿼드 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/quadArrowCallout.svg" height="50" width="50"></p>
rect | 직사각형 모양 | <p style="text-align: center;"><img src="../images/shapes/rect.svg" height="50" width="50"></p>
ribbon | 리본 모양 | <p style="text-align: center;"><img src="../images/shapes/ribbon.svg" height="50" width="50"></p>
ribbon2 | 리본 2 모양 | <p style="text-align: center;"><img src="../images/shapes/ribbon2.svg" height="50" width="50"></p>
rightArrow | 오른쪽 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/rightArrow.svg" height="50" width="50"></p>
rightArrowCallout | 설명선 오른쪽 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/rightArrowCallout.svg" height="50" width="50"></p>
rightBrace | 오른쪽 버팀대 모양 | <p style="text-align: center;"><img src="../images/shapes/rightBrace.svg" height="50" width="50"></p>
rightBracket | 오른쪽 브라켓 모양 | <p style="text-align: center;"><img src="../images/shapes/rightBracket.svg" height="50" width="50"></p>
round1Rect | 하나의 둥근 모서리 직사각형 모양 | <p style="text-align: center;"><img src="../images/shapes/round1Rect.svg" height="50" width="50"></p>
round2DiagRect | 두 개의 대각선 둥근 모서리 직사각형 모양 | <p style="text-align: center;"><img src="../images/shapes/round2DiagRect.svg" height="50" width="50"></p>
round2SameRect | 두 개의 같은 면이 둥근 모서리 직사각형 모양 | <p style="text-align: center;"><img src="../images/shapes/round2SameRect.svg" height="50" width="50"></p>
roundRect | 모서리가 둥근 사각형 모양 | <p style="text-align: center;"><img src="../images/shapes/roundRect.svg" height="50" width="50"></p>
rtTriangle | 직각 삼각형 모양 | <p style="text-align: center;"><img src="../images/shapes/rtTriangle.svg" height="50" width="50"></p>
smileyFace | 웃는 얼굴 모양 | <p style="text-align: center;"><img src="../images/shapes/smileyFace.svg" height="50" width="50"></p>
snip1Rect | 하나의 싹둑 코너 사각형 모양 | <p style="text-align: center;"><img src="../images/shapes/snip1Rect.svg" height="50" width="50"></p>
snip2DiagRect | 두 개의 대각선 싹둑 모서리 직사각형 모양 | <p style="text-align: center;"><img src="../images/shapes/snip2DiagRect.svg" height="50" width="50"></p>
snip2SameRect | 두 개의 동일면 자르기 코너 직사각형 모양 | <p style="text-align: center;"><img src="../images/shapes/snip2SameRect.svg" height="50" width="50"></p>
snipRoundRect | 하나의 싹둑 하나의 둥근 모서리 직사각형 모양 | <p style="text-align: center;"><img src="../images/shapes/snipRoundRect.svg" height="50" width="50"></p>
squareTabs | 정사각형 탭 모양 | <p style="text-align: center;"><img src="../images/shapes/squareTabs.svg" height="50" width="50"></p>
star10 | 10 개의 뾰족한 별 모양 | <p style="text-align: center;"><img src="../images/shapes/star10.svg" height="50" width="50"></p>
star12 | 12 개의 뾰족한 별 모양 | <p style="text-align: center;"><img src="../images/shapes/star12.svg" height="50" width="50"></p>
star16 | 16 개의 뾰족한 별 모양 | <p style="text-align: center;"><img src="../images/shapes/star16.svg" height="50" width="50"></p>
star24 | 24 개의 뾰족한 별 모양 | <p style="text-align: center;"><img src="../images/shapes/star24.svg" height="50" width="50"></p>
star32 | 32 개의 뾰족한 별 모양 | <p style="text-align: center;"><img src="../images/shapes/star32.svg" height="50" width="50"></p>
star4 | 4 개의 뾰족한 별 모양 | <p style="text-align: center;"><img src="../images/shapes/star4.svg" height="50" width="50"></p>
star5 | 5 개의 뾰족한 별 모양 | <p style="text-align: center;"><img src="../images/shapes/star5.svg" height="50" width="50"></p>
star6 | 6 개의 뾰족한 별 모양 | <p style="text-align: center;"><img src="../images/shapes/star6.svg" height="50" width="50"></p>
star7 | 7 개의 뾰족한 별 모양 | <p style="text-align: center;"><img src="../images/shapes/star7.svg" height="50" width="50"></p>
star8 | 8 개의 뾰족한 별 모양 | <p style="text-align: center;"><img src="../images/shapes/star8.svg" height="50" width="50"></p>
straightConnector1 | 스트레이트 커넥터 1형 | <p style="text-align: center;"><img src="../images/shapes/straightConnector1.svg" height="50" width="50"></p>
stripedRightArrow | 줄무늬 오른쪽 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/stripedRightArrow.svg" height="50" width="50"></p>
sun | 태양 모양 | <p style="text-align: center;"><img src="../images/shapes/sun.svg" height="50" width="50"></p>
swooshArrow | 스우시 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/swooshArrow.svg" height="50" width="50"></p>
teardrop | 눈물 모양 | <p style="text-align: center;"><img src="../images/shapes/teardrop.svg" height="50" width="50"></p>
trapezoid | 사다리꼴 모양 | <p style="text-align: center;"><img src="../images/shapes/trapezoid.svg" height="50" width="50"></p>
triangle | 삼각형 모양 | <p style="text-align: center;"><img src="../images/shapes/triangle.svg" height="50" width="50"></p>
upArrow | 위쪽 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/upArrow.svg" height="50" width="50"></p>
upArrowCallout | 설명선 위쪽 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/upArrowCallout.svg" height="50" width="50"></p>
upDownArrow | 위쪽 아래쪽 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/upDownArrow.svg" height="50" width="50"></p>
upDownArrowCallout | 설명선 위쪽 아래쪽 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/upDownArrowCallout.svg" height="50" width="50"></p>
uturnArrow | 유턴 화살표 모양 | <p style="text-align: center;"><img src="../images/shapes/uturnArrow.svg" height="50" width="50"></p>
verticalScroll | 세로 스크롤 모양 | <p style="text-align: center;"><img src="../images/shapes/verticalScroll.svg" height="50" width="50"></p>
wave | 웨이브 셰이프 | <p style="text-align: center;"><img src="../images/shapes/wave.svg" height="50" width="50"></p>
wedgeEllipseCallout | 설명선 웨지 타원 모양 | <p style="text-align: center;"><img src="../images/shapes/wedgeEllipseCallout.svg" height="50" width="50"></p>
wedgeRectCallout | 설명선 웨지 직사각형 모양 | <p style="text-align: center;"><img src="../images/shapes/wedgeRectCallout.svg" height="50" width="50"></p>
wedgeRoundRectCallout | 설명선 웨지 원형 직사각형 모양 | <p style="text-align: center;"><img src="../images/shapes/wedgeRoundRectCallout.svg" height="50" width="50"></p>
