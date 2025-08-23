# 스타일

Alignment 는 셀의 맞춤 설정을 직접 매핑합니다.

```go
type Alignment struct {
    Horizontal      string
    Indent          int
    JustifyLastLine bool
    ReadingOrder    uint64
    RelativeIndent  int
    ShrinkToFit     bool
    TextRotation    int
    Vertical        string
    WrapText        bool
}
```

Border 는 셀의 테두리 설정을 직접 매핑합니다.

```go
type Border struct {
    Type  string
    Color string
    Style int
}
```

Font 는 글꼴의 글꼴 설정을 직접 매핑합니다.

```go
type Font struct {
    Bold         bool
    Italic       bool
    Underline    string
    Family       string
    Size         float64
    Strike       bool
    Color        string
    ColorIndexed int
    ColorTheme   *int
    ColorTint    float64
    VertAlign    string
}
```

Fill 는 셀의 채우기 설정을 직접 매핑합니다.

```go
type Fill struct {
    Type         string
    Pattern      int
    Color        []string
    Shading      int
    Transparency int
}
```

Protection 는 셀의 보호 설정을 직접 매핑합니다.

```go
type Protection struct {
    Hidden bool
    Locked bool
}
```

Style 는 셀의 스타일 설정을 직접 매핑합니다.

```go
type Style struct {
    Border        []Border
    Fill          Fill
    Font          *Font
    Alignment     *Alignment
    Protection    *Protection
    NumFmt        int
    DecimalPlaces int
    CustomNumFmt  *string
    NegRed        bool
}
```

## 스타일 만들기 {#NewStyle}

```go
func (f *File) NewStyle(style *Style) (int, error)
```

NewStyle 은 주어진 스타일 옵션으로 셀에 대한 스타일을 생성하는 기능을 제공하고 스타일 인덱스를 반환합니다. 동일한 스타일 인덱스는 다른 통합 문서에서 사용할 수 없습니다. 이 함수는 동시성 안전합니다. `Font.Color` 필드는 `RRGGBB` 16진 수 표기법으로 표현되는 RGB 색상을 사용합니다.

### 테두리 {#border}

다음 표는 excelize 에서 지원하는 `Border.Type` 에서 사용되는 테두리 유형을 보여줍니다:

유형|설명|유형|설명
---|---|---|---
left|왼쪽 테두리|top|위쪽 테두리
right|오른쪽 테두리|bottom|하단 테두리
diagonalDown|대각선 아래쪽 테두리|diagonalUp|대각선 위쪽 테두리

다음 표는 excelize 인덱스 번호가 지원하는 `Border.Style` 에서 사용되는 테두리 스타일을 보여줍니다:

인덱스|스타일|라인|미리 보기
---|---|---|---
0|아무도|0|
1|마디 없는|1|!["마디 없는"](../images/style/border_01.png)
2|마디 없는|2|!["마디 없는"](../images/style/border_02.png)
3|대시|1|!["대시"](../images/style/border_03.png)
4|점|1|!["Dot"](../images/style/border_04.png)
5|마디 없는|3|!["마디 없는"](../images/style/border_05.png)
6|더블|3|!["더블"](../images/style/border_06.png)
7|마디 없는|0|!["마디 없는"](../images/style/border_07.png)
8|대시|2|!["대시"](../images/style/border_08.png)
9|대시 도트|1|!["대시 도트"](../images/style/border_09.png)
10|대시 도트|2|!["대시 도트"](../images/style/border_10.png)
11|대시 도트 도트|1|!["대시 도트 도트"](../images/style/border_11.png)
12|대시 도트 도트|2|!["대시 도트 도트"](../images/style/border_12.png)
13|슬랜트 대시 도트|2|!["슬랜트 대시 도트"](../images/style/border_13.png)

다음 표는 Excel 대화 상자에 표시된 순서대로 `Border.Style` 에서 사용되는 테두리 스타일을 보여줍니다:

인덱스|미리 보기|인덱스|미리 보기
---|---|---|---
0||12|!["국경 12"](../images/style/border_12.png)
7|!["국경 7"](../images/style/border_07.png)|13|!["국경 13"](../images/style/border_13.png)
4|!["국경 4"](../images/style/border_04.png)|10|!["국경 19"](../images/style/border_10.png)
11|!["국경 11"](../images/style/border_11.png)|8|!["국경 8"](../images/style/border_08.png)
9|!["국경 9"](../images/style/border_09.png)|2|!["국경 2"](../images/style/border_02.png)
3|!["국경 3"](../images/style/border_03.png)|5|!["국경 5"](../images/style/border_05.png)
1|!["국경 1"](../images/style/border_01.png)|6|!["국경 6"](../images/style/border_06.png)

### 색상 채우기 {#shading}

다음 표는 excelize 인덱스 번호가 지원하는 `Fill.Shading` 에서 사용되는 음영 스타일을 보여줍니다:

인덱스|스타일|인덱스|스타일
---|---|---|---
0|수평의|3|대각선 아래로
1|수직의|4|코너에서
2|대각선 위로|5|중앙에서

### 패턴 채우기 {#pattern}

다음 표는 Excelize 인덱스 번호가 지원하는 `Fill.Pattern` 에서 사용되는 패턴 스타일을 보여줍니다:

인덱스|스타일|인덱스|스타일
---|---|---|---
0|없음|10|!["패턴 채우기 10"](../images/style/pattern_10.png)
1|!["패턴 채우기 1"](../images/style/pattern_01.png)|11|!["패턴 채우기 11"](../images/style/pattern_11.png)
2|!["패턴 채우기 2"](../images/style/pattern_02.png)|12|!["패턴 채우기 12"](../images/style/pattern_12.png)
3|!["패턴 채우기 3"](../images/style/pattern_03.png)|13|!["패턴 채우기 13"](../images/style/pattern_13.png)
4|!["패턴 채우기 4"](../images/style/pattern_04.png)|14|!["패턴 채우기 14"](../images/style/pattern_14.png)
5|!["패턴 채우기 5"](../images/style/pattern_05.png)|15|!["패턴 채우기 15"](../images/style/pattern_15.png)
6|!["패턴 채우기 6"](../images/style/pattern_06.png)|16|!["패턴 채우기 16"](../images/style/pattern_16.png)
7|!["패턴 채우기 7"](../images/style/pattern_07.png)|17|!["패턴 채우기 17"](../images/style/pattern_17.png)
8|!["패턴 채우기 8"](../images/style/pattern_08.png)|18|!["패턴 채우기 18"](../images/style/pattern_18.png)
9|!["패턴 채우기 9](../images/style/pattern_09.png)||

### 투명도 {#transparency}

`Fill.Transparency` 는 차트와 도형의 투명도를 설정하는 데만 사용되며, 셀에는 사용되지 않습니다. 값은 0 에서 100 사이의 숫자여야 하며, 0% 에서 100% 를 나타냅니다. 기본값은 0 이며, 완전 불투명 (투명하지 않음) 을 나타냅니다.

### 정렬 {#align}

#### 톱니 모양

`Indent` 는 정수 값이며 1씩 증가하면 3개의 공백을 나타냅니다. 셀의 텍스트에 대한 들여쓰기의 공백 (일반 스타일 글꼴) 수를 나타냅니다. 들여쓰기할 공백의 수는 다음과 같이 계산됩니다.

들여쓰기할 공백 수 = 들여쓰기 값 * 3

예를 들어 들여쓰기 값이 1이면 텍스트가 셀 가장자리에서 3개의 여백 너비(일반 스타일 글꼴)에서 시작함을 의미합니다. 참고: 한 공백 문자의 너비는 글꼴로 정의됩니다. 왼쪽, 오른쪽 및 분산 수평 정렬만 지원됩니다.

#### 수평 정렬

다음 표는 `Alignment.Horizontal` 에서 사용되는 셀의 수평 정렬 유형을 보여줍니다:

유형|스타일
---|---
left             | 왼쪽(들여쓰기)
center           | 중심
right            | 오른쪽(들여쓰기)
fill             | 충전재
justify          | 정당화
centerContinuous | 교차 열 중심
distributed      | 분산 정렬(들여쓰기)

#### 수직 정렬

다음 표는 `Alignment.Vertical` 에서 사용되는 셀의 수직 정렬 유형을 보여줍니다:

유형|스타일
---|---
top         | 상단 정렬
center      | 중심
justify     | 정당화
distributed | 분산 정렬

#### 읽기 순서

`ReadingOrder` 는 셀의 읽기 순서가 왼쪽에서 오른쪽인지, 오른쪽에서 왼쪽인지 또는 상황에 따라 달라지는지를 나타내는 uint64 값입니다. 이 필드의 유효한 값은 다음과 같습니다.

값|설명
---|---
0 | 컨텍스트에 따라 다름 - 첫 번째 비공백 문자에 대한 텍스트를 스캔하여 읽기 순서를 결정합니다. 강한 오른쪽에서 왼쪽 문자인 경우 읽기 순서는 오른쪽에서 왼쪽입니다. 그렇지 않으면 왼쪽에서 오른쪽으로 읽는 순서입니다
1 | 왼쪽에서 오른쪽: 읽기 순서는 영어와 같이 셀에서 왼쪽에서 오른쪽입니다
2 | 오른쪽에서 왼쪽: 읽기 순서는 히브리어에서와 같이 셀에서 오른쪽에서 왼쪽입니다

#### 상대 들여쓰기

`RelativeIndent` 는 셀의 텍스트에 맞게 조정할 추가 들여쓰기 공간 수를 나타내는 정수 값입니다.

### 글꼴 밑줄 {#underline}

다음 표는 `Font.Underline` 에서 사용되는 글꼴 밑줄 스타일의 유형을 보여줍니다:

유형|스타일
---|---
single | 하나의 선
double | 이중선

### 숫자 형식 {#number_format}

Excel의 기본 제공 모든 언어 형식 (`Style.NumFmt` 필드) 은 다음 표에 나와 있습니다:

인덱스|형식
---|---
0|`General`
1|`0`
2|`0.00`
3|`#,##0`
4|`#,##0.00`
5|`($#,##0_);($#,##0)`
6|`($#,##0_);[Red]($#,##0)`
7|`($#,##0.00_);($#,##0.00)`
8|`($#,##0.00_);[Red]($#,##0.00)`
9|`0%`
10|`0.00%`
11|`0.00E+00`
12|`# ?/?`
13|`# ??/??`
14|`mm-dd-yy`
15|`d-mmm-yy`
16|`d-mmm`
17|`mmm-yy`
18|`h:mm AM/PM`
19|`h:mm:ss AM/PM`
20|`h:mm`
21|`h:mm:ss`
22|`m/d/yy h:mm`
...|`...`
37|`(#,##0_);(#,##0)`
38|`(#,##0_);[Red](#,##0)`
39|`(#,##0.00_);(#,##0.00)`
40|`(#,##0.00_);[Red](#,##0.00)`
41|`_(* #,##0_);_(* (#,##0);_(* "-"_);_(@_)`
42|`_($* #,##0_);_($* (#,##0);_($* "-"_);_(@_)`
43|`_(* #,##0.00_);_(* (#,##0.00);_(* "-"??_);_(@_)`
44|`_($* #,##0.00_);_($* (#,##0.00);_($* "-"??_);_(@_)`
45|`mm:ss`
46|`[h]:mm:ss`
47|`mm:ss.0`
48|`##0.0E+0`
49|`@`

#### 중국어 번체 숫자 형식

`zh-tw` 언어의 숫자 형식 코드:

인덱스|형식
---|---
27|`[$-404]e/m/d`
28|`[$-404]e"年"m"月"d"日"`
29|`[$-404]e"年"m"月"d"日"`
30|`m/d/yy`
31|`yyyy"年"m"月"d"日"`
32|`hh"時"mm"分"`
33|`hh"時"mm"分"ss"秒"`
34|`上午/下午 hh"時"mm"分"`
35|`上午/下午 hh"時"mm"分"ss"秒"`
36|`[$-404]e/m/d`
50|`[$-404]e/m/d`
51|`[$-404]e"年"m"月"d"日"`
52|`上午/下午 hh"時"mm"分"`
53|`上午/下午 hh"時"mm"分"ss"秒"`
54|`[$-404]e"年"m"月"d"日"`
55|`上午/下午 hh"時"mm"分"`
56|`上午/下午 hh"時"mm"分"ss"秒"`
57|`[$-404]e/m/d`
58|`[$-404]e"年"m"月"d"日"`

#### 간체 중국어 숫자 형식

`zh-cn` 언어로 된 숫자 형식 코드:

인덱스|형식
---|---
27|`yyyy"年"m"月"`
28|`m"月"d"日"`
29|`m"月"d"日"`
30|`m-d-yy`
31|`yyyy"年"m"月"d"日"`
32|`h"时"mm"分"`
33|`h"时"mm"分"ss"秒"`
34|`上午/下午 h"时"mm"分"`
35|`上午/下午 h"时"mm"分"ss"秒`
36|`yyyy"年"m"月`
50|`yyyy"年"m"月`
51|`m"月"d"日`
52|`yyyy"年"m"月`
53|`m"月"d"日`
54|`m"月"d"日`
55|`上午/下午 h"时"mm"分`
56|`上午/下午 h"时"mm"分"ss"秒`
57|`yyyy"年"m"月`
58|`m"月"d"日"`

#### 일본어 숫자 형식

`ja-jp` 언어로 된 번호 형식 코드:

인덱스|형식
---|---
27|`[$-411]ge.m.d`
28|`[$-411]ggge"年"m"月"d"日`
29|`[$-411]ggge"年"m"月"d"日`
30|`m/d/y`
31|`yyyy"年"m"月"d"日`
32|`h"時"mm"分`
33|`h"時"mm"分"ss"秒`
34|`yyyy"年"m"月`
35|`m"月"d"日`
36|`[$-411]ge.m.d`
50|`[$-411]ge.m.d`
51|`[$-411]ggge"年"m"月"d"日`
52|`yyyy"年"m"月`
53|`m"月"d"日`
54|`[$-411]ggge"年"m"月"d"日`
55|`yyyy"年"m"月`
56|`m"月"d"日`
57|`[$-411]ge.m.d`
58|`[$-411]ggge"年"m"月"d"日"`

#### 한국어 숫자 형식

`ko-kr` 언어의 번호 형식 코드:

인덱스|형식
---|---
27|`yyyy"年" mm"月" dd"日`
28|`mm-d`
29|`mm-d`
30|`mm-dd-y`
31|`yyyy"년" mm"월" dd"일`
32|`h"시" mm"분`
33|`h"시" mm"분" ss"초`
34|`yyyy-mm-d`
35|`yyyy-mm-d`
36|`yyyy"年" mm"月" dd"日`
50|`yyyy"年" mm"月" dd"日`
51|`mm-d`
52|`yyyy-mm-d`
53|`yyyy-mm-d`
54|`mm-d`
55|`yyyy-mm-d`
56|`yyyy-mm-d`
57|`yyyy"年" mm"月" dd"日`
58|`mm-dd`

#### 태국어 번호 형식

`th-th` 언어로 된 숫자 형식 코드:

인덱스|형식
---|---
59|`t`
60|`t0.0`
61|`t#,##`
62|`t#,##0.0`
67|`t0`
68|`t0.00`
69|`t# ?/`
70|`t# ??/?`
71|`ว/ด/ปปป`
72|`ว-ดดด-ป`
73|`ว-ดด`
74|`ดดด-ป`
75|`ช:น`
76|`ช:นน:ท`
77|`ว/ด/ปปปป ช:น`
78|`นน:ท`
79|`[ช]:นน:ท`
80|`นน:ทท.`
81|`d/m/bb`

### 통화 형식

Excelize 기본 제공 통화 형식은 다음 표에 표시되며 다음 표에서 이러한 형식만 지원합니다 (인덱스 번호는 태그에만 사용되며 Excel 파일 내에서 사용되지 않으며 함수 [`GetCellValue`](cell.md#GetCellValue)) 에 의해 서식을 지정한 값을 얻을 수 없습니다) 현재:

인덱스|통화 형식
---|---
164|¥
165|$ English (United States)
166|$ Cherokee (United States)
167|$ Chinese (Singapore)
168|$ Chinese (Taiwan)
169|$ English (Australia)
170|$ English (Belize)
171|$ English (Canada)
172|$ English (Jamaica)
173|$ English (New Zealand)
174|$ English (Singapore)
175|$ English (Trinidad & Tobago)
176|$ English (U.S. Virgin Islands)
177|$ English (United States)
178|$ French (Canada)
179|$ Hawaiian (United States)
180|$ Malay (Brunei)
181|$ Quechua (Ecuador)
182|$ Spanish (Chile)
183|$ Spanish (Colombia)
184|$ Spanish (Ecuador)
185|$ Spanish (El Salvador)
186|$ Spanish (Mexico)
187|$ Spanish (Puerto Rico)
188|$ Spanish (United States)
189|$ Spanish (Uruguay)
190|£ English (United Kingdom)
191|£ Scottish Gaelic (United Kingdom)
192|£ Welsh (United Kindom)
193|¥ Chinese (China)
194|¥ Japanese (Japan)
195|¥ Sichuan Yi (China)
196|¥ Tibetan (China)
197|¥ Uyghur (China)
198|֏ Armenian (Armenia)
199|؋ Pashto (Afghanistan)
200|؋ Persian (Afghanistan)
201|৳ Bengali (Bangladesh)
202|៛ Khmer (Cambodia)
203|₡ Spanish (Costa Rica)
204|₦ Hausa (Nigeria)
205|₦ Igbo (Nigeria)
206|₩ Korean (South Korea)
207|₪ Hebrew (Israel)
208|₫ Vietnamese (Vietnam)
209|€ Basque (Spain)
210|€ Breton (France)
211|€ Catalan (Spain)
212|€ Corsican (France)
213|€ Dutch (Belgium)
214|€ Dutch (Netherlands)
215|€ English (Ireland)
216|€ Estonian (Estonia)
217|€ Euro (€ 123)
218|€ Euro (123 €)
219|€ Finnish (Finland)
220|€ French (Belgium)
221|€ French (France)
222|€ French (Luxembourg)
223|€ French (Monaco)
224|€ French (Réunion)
225|€ Galician (Spain)
226|€ German (Austria)
227|€ German (German)
228|€ German (Luxembourg)
229|€ Greek (Greece)
230|€ Inari Sami (Finland)
231|€ Irish (Ireland)
232|€ Italian (Italy)
233|€ Latin (Italy)
234|€ Latin, Serbian (Montenegro)
235|€ Larvian (Latvia)
236|€ Lithuanian (Lithuania)
237|€ Lower Sorbian (Germany)
238|€ Luxembourgish (Luxembourg)
239|€ Maltese (Malta)
240|€ Northern Sami (Finland)
241|€ Occitan (France)
242|€ Portuguese (Portugal)
243|€ Serbian (Montenegro)
244|€ Skolt Sami (Finland)
245|€ Slovak (Slovakia)
246|€ Slovenian (Slovenia)
247|€ Spanish (Spain)
248|€ Swedish (Finland)
249|€ Swiss German (France)
250|€ Upper Sorbian (Germany)
251|€ Western Frisian (Netherlands)
252|₭ Lao (Laos)
253|₮ Mongolian (Mongolia)
254|₮ Mongolian, Mongolian (Mongolia)
255|₱ English (Philippines)
256|₱ Filipino (Philippines)
257|₴ Ukrainian (Ukraine)
258|₸ Kazakh (Kazakhstan)
259|₹ Arabic, Kashmiri (India)
260|₹ English (India)
261|₹ Gujarati (India)
262|₹ Hindi (India)
263|₹ Kannada (India)
264|₹ Kashmiri (India)
265|₹ Konkani (India)
266|₹ Manipuri (India)
267|₹ Marathi (India)
268|₹ Nepali (India)
269|₹ Oriya (India)
270|₹ Punjabi (India)
271|₹ Sanskrit (India)
272|₹ Sindhi (India)
273|₹ Tamil (India)
274|₹ Urdu (India)
275|₺ Turkish (Turkey)
276|₼ Azerbaijani (Azerbaijan)
277|₼ Cyrillic, Azerbaijani (Azerbaijan)
278|₽ Russian (Russia)
279|₽ Sakha (Russia)
280|₾ Georgian (Georgia)
281|B/. Spanish (Panama)
282|Br Oromo (Ethiopia)
283|Br Somali (Ethiopia)
284|Br Tigrinya (Ethiopia)
285|Bs Quechua (Bolivia)
286|Bs Spanish (Bolivia)
287|BS. Spanish (Venezuela)
288|BWP Tswana (Botswana)
289|C$ Spanish (Nicaragua)
290|CA$ Latin, Inuktitut (Canada)
291|CA$ Mohawk (Canada)
292|CA$ Unified Canadian Aboriginal Syllabics, Inuktitut (Canada)
293|CFA French (Mali)
294|CFA French (Senegal)
295|CFA Fulah (Senegal)
296|CFA Wolof (Senegal)
297|CHF French (Switzerland)
298|CHF German (Liechtenstein)
299|CHF German (Switzerland)
300|CHF Italian (Switzerland)
301|CHF Romansh (Switzerland)
302|CLP Mapuche (Chile)
303|CN¥ Mongolian, Mongolian (China)
304|DZD Central Atlas Tamazight (Algeria)
305|FCFA French (Cameroon)
306|Ft Hungarian (Hungary)
307|G French (Haiti)
308|Gs. Spanish (Paraguay)
309|GTQ K'iche' (Guatemala)
310|HK$ Chinese (Hong Kong (China))
311|HK$ English (Hong Kong (China))
312|HRK Croatian (Croatia)
313|IDR English (Indonesia)
314|IQD Arbic, Central Kurdish (Iraq)
315|ISK Icelandic (Iceland)
316|K Burmese (Myanmar (Burma))
317|Kč Czech (Czech Republic)
318|KM Bosnian (Bosnia & Herzegovina)
319|KM Croatian (Bosnia & Herzegovina)
320|KM Latin, Serbian (Bosnia & Herzegovina)
321|kr Faroese (Faroe Islands)
322|kr Northern Sami (Norway)
323|kr Northern Sami (Sweden)
324|kr Norwegian Bokmål (Norway)
325|kr Norwegian Nynorsk (Norway)
326|kr Swedish (Sweden)
327|kr. Danish (Denmark)
328|kr. Kalaallisut (Greenland)
329|Ksh Swahili (kenya)
330|L Romanian (Moldova)
331|L Russian (Moldova)
332|L Spanish (Honduras)
333|Lekë Albanian (Albania)
334|MAD Arabic, Central Atlas Tamazight (Morocco)
335|MAD French (Morocco)
336|MAD Tifinagh, Central Atlas Tamazight (Morocco)
337|MOP$ Chinese (Macau (China))
338|MVR Divehi (Maldives)
339|Nfk Tigrinya (Eritrea)
340|NGN Bini (Nigeria)
341|NGN Fulah (Nigeria)
342|NGN Ibibio (Nigeria)
343|NGN Kanuri (Nigeria)
344|NOK Lule Sami (Norway)
345|NOK Southern Sami (Norway)
346|NZ$ Maori (New Zealand)
347|PKR Sindhi (Pakistan)
348|PYG Guarani (Paraguay)
349|Q Spanish (Guatemala)
350|R Afrikaans (South Africa)
351|R English (South Africa)
352|R Zulu (South Africa)
353|R$ Portuguese (Brazil)
354|RD$ Spanish (Dominican Republic)
355|RF Kinyarwanda (Rwanda)
356|RM English (Malaysia)
357|RM Malay (Malaysia)
358|RON Romanian (Romania)
359|Rp Indonesoan (Indonesia)
360|Rs Urdu (Pakistan)
361|Rs. Tamil (Sri Lanka)
362|RSD Latin, Serbian (Serbia)
363|RSD Serbian (Serbia)
364|RUB Bashkir (Russia)
365|RUB Tatar (Russia)
366|S/. Quechua (Peru)
367|S/. Spanish (Peru)
368|SEK Lule Sami (Sweden)
369|SEK Southern Sami (Sweden)
370|soʻm Latin, Uzbek (Uzbekistan)
371|soʻm Uzbek (Uzbekistan)
372|SYP Syriac (Syria)
373|THB Thai (Thailand)
374|TMT Turkmen (Turkmenistan)
375|US$ English (Zimbabwe)
376|ZAR Northern Sotho (South Africa)
377|ZAR Southern Sotho (South Africa)
378|ZAR Tsonga (South Africa)
379|ZAR Tswana (south Africa)
380|ZAR Venda (South Africa)
381|ZAR Xhosa (South Africa)
382|zł Polish (Poland)
383|ден Macedonian (Macedonia)
384|KM Cyrillic, Bosnian (Bosnia & Herzegovina)
385|KM Serbian (Bosnia & Herzegovina)
386|лв. Bulgarian (Bulgaria)
387|p. Belarusian (Belarus)
388|сом Kyrgyz (Kyrgyzstan)
389|сом Tajik (Tajikistan)
390|ج.م. Arabic (Egypt)
391|د.أ. Arabic (Jordan)
392|د.أ. Arabic (United Arab Emirates)
393|د.ب. Arabic (Bahrain)
394|د.ت. Arabic (Tunisia)
395|د.ج. Arabic (Algeria)
396|د.ع. Arabic (Iraq)
397|د.ك. Arabic (Kuwait)
398|د.ل. Arabic (Libya)
399|د.م. Arabic (Morocco)
400|ر Punjabi (Pakistan)
401|ر.س. Arabic (Saudi Arabia)
402|ر.ع. Arabic (Oman)
403|ر.ق. Arabic (Qatar)
404|ر.ي. Arabic (Yemen)
405|ریال Persian (Iran)
406|ل.س. Arabic (Syria)
407|ل.ل. Arabic (Lebanon)
408|ብር Amharic (Ethiopia)
409|रू Nepaol (Nepal)
410|රු. Sinhala (Sri Lanka)
411|ADP
412|AED
413|AFA
414|AFN
415|ALL
416|AMD
417|ANG
418|AOA
419|ARS
420|ATS
421|AUD
422|AWG
423|AZM
424|AZN
425|BAM
426|BBD
427|BDT
428|BEF
429|BGL
430|BGN
431|BHD
432|BIF
433|BMD
434|BND
435|BOB
436|BOV
437|BRL
438|BSD
439|BTN
440|BWP
441|BYR
442|BZD
443|CAD
444|CDF
445|CHE
446|CHF
447|CHW
448|CLF
449|CLP
450|CNY
451|COP
452|COU
453|CRC
454|CSD
455|CUC
456|CVE
457|CYP
458|CZK
459|DEM
460|DJF
461|DKK
462|DOP
463|DZD
464|ECS
465|ECV
466|EEK
467|EGP
468|ERN
469|ESP
470|ETB
471|EUR
472|FIM
473|FJD
474|FKP
475|FRF
476|GBP
477|GEL
478|GHC
479|GHS
480|GIP
481|GMD
482|GNF
483|GRD
484|GTQ
485|GYD
486|HKD
487|HNL
488|HRK
489|HTG
490|HUF
491|IDR
492|IEP
493|ILS
494|INR
495|IQD
496|IRR
497|ISK
498|ITL
499|JMD
500|JOD
501|JPY
502|KAF
503|KES
504|KGS
505|KHR
506|KMF
507|KPW
508|KRW
509|KWD
510|KYD
511|KZT
512|LAK
513|LBP
514|LKR
515|LRD
516|LSL
517|LTL
518|LUF
519|LVL
520|LYD
521|MAD
522|MDL
523|MGA
524|MGF
525|MKD
526|MMK
527|MNT
528|MOP
529|MRO
530|MTL
531|MUR
532|MVR
533|MWK
534|MXN
535|MXV
536|MYR
537|MZM
538|MZN
539|NAD
540|NGN
541|NIO
542|NLG
543|NOK
544|NPR
545|NTD
546|NZD
547|OMR
548|PAB
549|PEN
550|PGK
551|PHP
552|PKR
553|PLN
554|PTE
555|PYG
556|QAR
557|ROL
558|RON
559|RSD
560|RUB
561|RUR
562|RWF
563|SAR
564|SBD
565|SCR
566|SDD
567|SDG
568|SDP
569|SEK
570|SGD
571|SHP
572|SIT
573|SKK
574|SLL
575|SOS
576|SPL
577|SRD
578|SRG
579|STD
580|SVC
581|SYP
582|SZL
583|THB
584|TJR
585|TJS
586|TMM
587|TMT
588|TND
589|TOP
590|TRL
591|TRY
592|TTD
593|TWD
594|TZS
595|UAH
596|UGX
597|USD
598|USN
599|USS
600|UYI
601|UYU
602|UZS
603|VEB
604|VEF
605|VND
606|VUV
607|WST
608|XAF
609|XAG
610|XAU
611|XB5
612|XBA
613|XBB
614|XBC
615|XBD
616|XCD
617|XDR
618|XFO
619|XFU
620|XOF
621|XPD
622|XPF
623|XPT
624|XTS
625|XXX
626|YER
627|YUM
628|ZAR
629|ZMK
630|ZMW
631|ZWD
632|ZWL
633|ZWN
634|ZWR

셀에 대한 지원 세트 사용자 정의 번호 형식을 Excelize 합니다. 예를 들어 `Sheet1!A6` 에 대한 우루과이 (스페인어) 형식의 날짜 유형으로 설정:

<p align="center"><img width="612" src="./images/number_format_01.png" alt="숫자 형식 설정"></p>

```go
f := excelize.NewFile()
defer func() {
    if err := f.Close(); err != nil {
        fmt.Println(err)
    }
}()
if err := f.SetCellValue("Sheet1", "A6", 42920.5); err != nil {
    fmt.Println(err)
    return
}
exp := "[$-380A]dddd\\,\\ dd\" de \"mmmm\" de \"yyyy;@"
style, err := f.NewStyle(&excelize.Style{CustomNumFmt: &exp})
if err != nil {
    fmt.Println(err)
    return
}
err = f.SetCellStyle("Sheet1", "A6", "A6", style)
```

Excel 응용 프로그램의 셀 `Sheet1!A6`: `martes, 04 de Julio de 2017`

## 스타일을 얻으세요 {#GetStyle}

```go
func (f *File) GetStyle(idx int) (*Style, error)
```

GetStyle 은 주어진 스타일 인덱스로 스타일 정의를 가져오는 기능을 제공합니다.

## 열 스타일 설정 {#SetColStyle}

```go
func (f *File) SetColStyle(sheet, columns string, styleID int) error
```

SetColStyle 지정된 워크 시트 이름, 열 범위 및 스타일 ID 에 의해 열의 스타일을 설정하는 기능을 제공합니다. 이 기능은 동시성 안전에 사용될 수 있습니다. 이렇게 하면 열의 기존 스타일을 덮어쓰며 기존 스타일과 스타일을 추가하거나 병합하지 않습니다.

예를 들어 `Sheet1` 에서 `H` 열의 스타일 집합:

```go
err = f.SetColStyle("Sheet1", "H", style)
```

`Sheet1` 에서 열 `C:F` 의 스타일 설정:

```go
err = f.SetColStyle("Sheet1", "C:F", style)
```

## 열 스타일 가져오기 {#GetColStyle}

```go
func (f *File) GetColStyle(sheet, col string) (int, error)
```

GetColStyle 은 지정된 워크시트 이름과 열 이름으로 열 스타일 ID를 가져오는 함수를 제공합니다.

## 행 스타일 설정 {#SetRowStyle}

```go
func (f *File) SetRowStyle(sheet string, start, end, styleID int) error
```

SetRowStyle 은 주어진 워크시트 이름, 행 범위 및 스타일 ID 로 행의 스타일을 설정하는 기능을 제공합니다. 이 기능은 동시성 안전에 사용될 수 있습니다. 이것은 행의 기존 스타일을 덮어쓰며 기존 스타일과 스타일을 추가하거나 병합하지 않습니다.

예를 들어 `Sheet1` 에서 행 1의 스타일을 설정합니다:

```go
err := f.SetRowStyle("Sheet1", 1, 1, styleID)
```

`Sheet1` 에서 행 1 - 10 의 스타일 설정:

```go
err := f.SetRowStyle("Sheet1", 1, 10, styleID)
```

## 기본 글꼴 설정 {#SetDefaultFont}

```go
func (f *File) SetDefaultFont(fontName string)
```

SetDefaultFont 는 통합 문서의 기본 글꼴을 변경합니다.

## 기본 글꼴 가져오기 {#GetDefaultFont}

```go
func (f *File) GetDefaultFont() string
```

GetDefaultFont 는 통합 문서에 현재 설정된 기본 글꼴 이름을 제공합니다. Excelize 기본 글꼴로 생성된 스프레드시트는 Calibri 입니다.
