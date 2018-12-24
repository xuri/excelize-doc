# Стиль

## Создать стиль {#NewStyle}

```go
func (f *File) NewStyle(style string) (int, error)
```

NewStyle предоставляет функцию для создания стиля для ячеек по заданному стилю. Обратите внимание, что в цветовом поле используется цветовой код RGB.

### бордюр {#border}

Ниже показано стили границ `type`, отсортированные по индексу excelize:

Индекс|Стиль|линия|Просмотр
---|---|---|---
0|Никто|0|
1|непрерывный|1|!["непрерывный"](../images/style/border_01.png)
2|непрерывный|2|!["непрерывный"](../images/style/border_02.png)
3|тире|1|!["тире"](../images/style/border_03.png)
4|точка|1|!["точка"](../images/style/border_04.png)
5|непрерывный|3|!["непрерывный"](../images/style/border_05.png)
6|Double|3|!["Double"](../images/style/border_06.png)
7|непрерывный|0|!["непрерывный"](../images/style/border_07.png)
8|тире|2|!["тире"](../images/style/border_08.png)
9|тире точка|1|!["тире точка"](../images/style/border_09.png)
10|тире точка|2|!["тире точка"](../images/style/border_10.png)
11|тире точка точка|1|!["тире точка точка"](../images/style/border_11.png)
12|тире точка точка|2|!["тире точка точка"](../images/style/border_12.png)
13|Наклонная черточка точка|2|!["Наклонная черточка точка"](../images/style/border_13.png)

Ниже показан `borders` в порядке, указанном в диалоговом окне Excel:

Индекс|Preview|Индекс|Просмотр
---|---|---|---
0||12|!["бордюр 12"](../images/style/border_12.png)
7|!["бордюр 7"](../images/style/border_07.png)|13|!["бордюр 13"](../images/style/border_13.png)
4|!["бордюр 4"](../images/style/border_04.png)|10|!["бордюр 19"](../images/style/border_10.png)
11|!["бордюр 11"](../images/style/border_11.png)|8|!["бордюр 8"](../images/style/border_08.png)
9|!["бордюр 9"](../images/style/border_09.png)|2|!["бордюр 2"](../images/style/border_02.png)
3|!["бордюр 3"](../images/style/border_03.png)|5|!["бордюр 5"](../images/style/border_05.png)
1|!["бордюр 1"](../images/style/border_01.png)|6|!["бордюр 6"](../images/style/border_06.png)

### Цвет заливки {#shading}

Ниже показаны стили `shading`, отсортированные по индексу excelize:

Индекс|Стиль|Индекс|Стиль
---|---|---|---
0|горизонтальный|3|Диагональ вниз
1|вертикальный|4|Из угла
2|Диагональ вверх|5|От центра

### образец заливки {#pattern}

Ниже показаны стили `pattern`, отсортированные по индексу excelize index:

Индекс|Стиль|Индекс|Стиль
---|---|---|---
0|None|10|!["Pattern fill 10"](../images/style/pattern_10.png)
1|!["заполнить шаблон 1"](../images/style/pattern_01.png)|11|!["заполнить шаблон 11"](../images/style/pattern_11.png)
2|!["заполнить шаблон 2"](../images/style/pattern_02.png)|12|!["заполнить шаблон 12"](../images/style/pattern_12.png)
3|!["заполнить шаблон 3"](../images/style/pattern_03.png)|13|!["заполнить шаблон 13"](../images/style/pattern_13.png)
4|!["заполнить шаблон 4"](../images/style/pattern_04.png)|14|!["заполнить шаблон 14"](../images/style/pattern_14.png)
5|!["заполнить шаблон 5"](../images/style/pattern_05.png)|15|!["заполнить шаблон 15"](../images/style/pattern_15.png)
6|!["заполнить шаблон 6"](../images/style/pattern_06.png)|16|!["заполнить шаблон 16"](../images/style/pattern_16.png)
7|!["заполнить шаблон 7"](../images/style/pattern_07.png)|17|!["заполнить шаблон 17"](../images/style/pattern_17.png)
8|!["заполнить шаблон 8"](../images/style/pattern_08.png)|18|!["заполнить шаблон 18"](../images/style/pattern_18.png)
9|!["заполнить шаблон 9](../images/style/pattern_09.png)||

### Выровнять {#align}

#### Горизонтальное выравнивание

Следующий типа выравнивания `horizontal` в клетках:

Тип|Стиль
---|---
left|Левый (с отступом)
center|центрированный
right|Справа (с отступом)
fill|начинка
justify|Оправдано
centerContinuous|Межстрочный центрированный
distributed|Децентрализованное выравнивание (с отступом)

#### Vertical alignment

Следующий типа `vertical` выравнивания в клетках:

Тип|Стиль
---|---
top|Верхнее выравнивание
center|центрированный
justify|Оправдано
distributed|Децентрализованное выравнивание

### Подчеркивание шрифта {#underline}

Следующий тип шрифта `underline` style:

Тип|Стиль
---|---
single|Одна линия
double|Двойная линия

### Формат номера {#number_format}

Встроенные форматы всех языков Excel (параметр `number_format`) показаны в следующей таблице:

Индекс|Тип
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
14|`m/d/yy`
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

#### Традиционный китайский формат номера

Код формата номера на языке `zh-tw`:

Индекс|Тип
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

#### Упрощенный китайский формат номера

Код формата номера на языке `zh-cn`:

Индекс|Тип
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

#### Unicode традиционный китайский формат чисел

Код формата номера со значениями unicode, указанными для языковых символов, где они встречаются на языке `zh-tw`:

Индекс|Тип
---|---
27|`[$-404]e/m/`
28|`[$-404]e"5E74"m"6708"d"65E5`
29|`[$-404]e"5E74"m"6708"d"65E5`
30|`m/d/y`
31|`yyyy"5E74"m"6708"d"65E5`
32|`hh"6642"mm"5206`
33|`hh"6642"mm"5206"ss"79D2`
34|`4E0A5348/4E0B5348hh"6642"mm"5206`
35|`4E0A5348/4E0B5348hh"6642"mm"5206"ss"79D2`
36|`[$-404]e/m/`
50|`[$-404]e/m/`
51|`[$-404]e"5E74"m"6708"d"65E5`
52|`4E0A5348/4E0B5348hh"6642"mm"5206`
53|`4E0A5348/4E0B5348hh"6642"mm"5206"ss"79D2`
54|`[$-404]e"5E74"m"6708"d"65E5`
55|`4E0A5348/4E0B5348hh"6642"mm"5206`
56|`4E0A5348/4E0B5348hh"6642"mm"5206"ss"79D2`
57|`[$-404]e/m/`
58|`[$-404]e"5E74"m"6708"d"65E5"`

#### Unicode упрощенный китайский формат номера

Код формата номера с значениями юникода, предоставленными для языковых символов, где они встречаются на языке `zh-cn`:

Индекс|Тип
---|---
27|`yyyy"5E74"m"6708`
28|`m"6708"d"65E5`
29|`m"6708"d"65E5`
30|`m-d-y`
31|`yyyy"5E74"m"6708"d"65E5`
32|`h"65F6"mm"5206`
33|`h"65F6"mm"5206"ss"79D2`
34|`4E0A5348/4E0B5348h"65F6"mm"5206`
35|`4E0A5348/4E0B5348h"65F6"mm"5206"ss"79D2`
36|`yyyy"5E74"m"6708`
50|`yyyy"5E74"m"6708`
51|`m"6708"d"65E5`
52|`yyyy"5E74"m"6708`
53|`m"6708"d"65E5`
54|`m"6708"d"65E5`
55|`4E0A5348/4E0B5348h"65F6"mm"5206`
56|`4E0A5348/4E0B5348h"65F6"mm"5206"ss"79D2`
57|`yyyy"5E74"m"6708`
58|`m"6708"d"65E5"`

#### Японский формат номера

Код формата номера на языке `ja-jp`:

Индекс|Тип
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

#### Корейский формат номера

Код формата номера на языке `ko-kr`:

Индекс|Тип
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

#### Юникод японский формат номера

Код формата номера с значениями unicode, указанными для языковых символов, где они встречаются на языке `ja-jp`:

Индекс|Тип
---|---
27|`[$-411]ge.m.d`
28|`[$-411]ggge"5E74"m"6708"d"65E5`
29|`[$-411]ggge"5E74"m"6708"d"65E5`
30|`m/d/y`
31|`yyyy"5E74"m"6708"d"65E5`
32|`h"6642"mm"5206`
33|`h"6642"mm"5206"ss"79D2`
34|`yyyy"5E74"m"6708`
35|`m"6708"d"65E5`
36|`[$-411]ge.m.d`
50|`[$-411]ge.m.d`
51|`[$-411]ggge"5E74"m"6708"d"65E5`
52|`yyyy"5E74"m"6708`
53|`m"6708"d"65E5`
54|`[$-411]ggge"5E74"m"6708"d"65E5`
55|`yyyy"5E74"m"6708`
56|`m"6708"d"65E5`
57|`[$-411]ge.m.d`
58|`[$-411]ggge"5E74"m"6708"d"65E5"`

#### Кодийский формат Unicode

Код формата номера со значениями unicode, указанными для языковых символов, где они встречаются на языке `ko-kr`:

Индекс|Тип
---|---
27|`yyyy"5E74" mm"6708" dd"65E5`
28|`mm-d`
29|`mm-d`
30|`mm-dd-y`
31|`yyyy"B144" mm"C6D4" dd"C77C`
32|`h"C2DC" mm"BD84`
33|`h"C2DC" mm"BD84" ss"CD08`
34|`yyyy-mm-d`
35|`yyyy-mm-d`
36|`yyyy"5E74" mm"6708" dd"65E5`
50|`yyyy"5E74" mm"6708" dd"65E5`
51|`mm-d`
52|`yyyy-mm-d`
53|`yyyy-mm-d`
54|`mm-d`
55|`yyyy-mm-d`
56|`yyyy-mm-d`
57|`yyyy"5E74" mm"6708" dd"65E5`
58|`mm-dd`

#### Формат номера в тайском языке

Код формата номера на языке `th-th`:

Индекс|Тип
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

#### Формат номера в формате Unicode для тайского языка

Код формата номера со значениями unicode, указанными для языковых символов, где они встречаются на языке `th-th`:

Индекс|Тип
---|---
59|`t`
60|`t0.0`
61|`t#,##`
62|`t#,##0.0`
67|`t0`
68|`t0.00`
69|`t# ?/`
70|`t# ??/?`
71|`0E27/0E14/0E1B0E1B0E1B0E1`
72|`0E27-0E140E140E14-0E1B0E1`
73|`0E27-0E140E140E1`
74|`0E140E140E14-0E1B0E1`
75|`0E0A:0E190E1`
76|`0E0A:0E190E19:0E170E1`
77|`0E27/0E14/0E1B0E1B0E1B0E1B 0E0A:0E190E1`
78|`0E190E19:0E170E1`
79|`[0E0A]:0E190E19:0E170E1`
80|`0E190E19:0E170E17.`
81|`d/m/bb`

### Формат валюты

Excelize встроенные форматы валют показаны в следующей таблице, поддерживают только эти типы в следующей таблице (номер индекса используется только для разметки и не используется внутри файла Excel, и вы не можете получить форматированное значение функцией [`GetCellValue`](cell.md#GetCellValue)) в настоящее время:

Индекс|Формат валюты
---|---
164|`CN¥`
165|`$ English (China)`
166|`$ Cherokee (United States)`
167|`$ Chinese (Singapore)`
168|`$ Chinese (Taiwan)`
169|`$ English (Australia)`
170|`$ English (Belize)`
171|`$ English (Canada)`
172|`$ English (Jamaica)`
173|`$ English (New Zealand)`
174|`$ English (Singapore)`
175|`$ English (Trinidad & Tobago)`
176|`$ English (U.S. Vigin Islands)`
177|`$ English (United States)`
178|`$ French (Canada)`
179|`$ Hawaiian (United States)`
180|`$ Malay (Brunei)`
181|`$ Quechua (Ecuador)`
182|`$ Spanish (Chile)`
183|`$ Spanish (Colombia)`
184|`$ Spanish (Ecuador)`
185|`$ Spanish (El Salvador)`
186|`$ Spanish (Mexico)`
187|`$ Spanish (Puerto Rico)`
188|`$ Spanish (United States)`
189|`$ Spanish (Uruguay)`
190|`£ English (United Kingdom)`
191|`£ Scottish Gaelic (United Kingdom)`
192|`£ Welsh (United Kindom)`
193|`¥ Chinese (China)`
194|`¥ Japanese (Japan)`
195|`¥ Sichuan Yi (China)`
196|`¥ Tibetan (China)`
197|`¥ Uyghur (China)`
198|`֏ Armenian (Armenia)`
199|`؋ Pashto (Afghanistan)`
200|`؋ Persian (Afghanistan)`
201|`৳ Bengali (Bangladesh)`
202|`៛ Khmer (Cambodia)`
203|`₡ Spanish (Costa Rica)`
204|`₦ Hausa (Nigeria)`
205|`₦ Igbo (Nigeria)`
206|`₦ Yoruba (Nigeria)`
207|`₩ Korean (South Korea)`
208|`₪ Hebrew (Israel)`
209|`₫ Vietnamese (Vietnam)`
210|`€ Basque (Spain)`
211|`€ Breton (France)`
212|`€ Catalan (Spain)`
213|`€ Corsican (France)`
214|`€ Dutch (Belgium)`
215|`€ Dutch (Netherlands)`
216|`€ English (Ireland)`
217|`€ Estonian (Estonia)`
218|`€ Euro (€ 123)`
219|`€ Euro (123 €)`
220|`€ Finnish (Finland)`
221|`€ French (Belgium)`
222|`€ French (France)`
223|`€ French (Luxembourg)`
224|`€ French (Monaco)`
225|`€ French (Réunion)`
226|`€ Galician (Spain)`
227|`€ German (Austria)`
228|`€ German (Luxembourg)`
229|`€ Greek (Greece)`
230|`€ Inari Sami (Finland)`
231|`€ Irish (Ireland)`
232|`€ Italian (Italy)`
233|`€ Latin (Italy)`
234|`€ Latin, Serbian (Montenegro)`
235|`€ Larvian (Latvia)`
236|`€ Lithuanian (Lithuania)`
237|`€ Lower Sorbian (Germany)`
238|`€ Luxembourgish (Luxembourg)`
239|`€ Maltese (Malta)`
240|`€ Northern Sami (Finland)`
241|`€ Occitan (France)`
242|`€ Portuguese (Portugal)`
243|`€ Serbian (Montenegro)`
244|`€ Skolt Sami (Finland)`
245|`€ Slovak (Slovakia)`
246|`€ Slovenian (Slovenia)`
247|`€ Spanish (Spain)`
248|`€ Swedish (Finland)`
249|`€ Swiss German (France)`
250|`€ Upper Sorbian (Germany)`
251|`€ Western Frisian (Netherlands)`
252|`₭ Lao (Laos)`
253|`₮ Mongolian (Mongolia)`
254|`₮ Mongolian, Mongolian (Mongolia)`
255|`₱ English (Philippines)`
256|`₱ Filipino (Philippines)`
257|`₴ Ukrainian (Ukraine)`
258|`₸ Kazakh (Kazakhstan)`
259|`₹ Arabic, Kashmiri (India)`
260|`₹ English (India)`
261|`₹ Gujarati (India)`
262|`₹ Hindi (India)`
263|`₹ Kannada (India)`
264|`₹ Kashmiri (India)`
265|`₹ Konkani (India)`
266|`₹ Manipuri (India)`
267|`₹ Marathi (India)`
268|`₹ Nepali (India)`
269|`₹ Oriya (India)`
270|`₹ Punjabi (India)`
271|`₹ Sanskrit (India)`
272|`₹ Sindhi (India)`
273|`₹ Tamil (India)`
274|`₹ Urdu (India)`
275|`₺ Turkish (Turkey)`
276|`₼ Azerbaijani (Azerbaijan)`
277|`₼ Cyrillic, Azerbaijani (Azerbaijan)`
278|`₽ Russian (Russia)`
279|`₽ Sakha (Russia)`
280|`₾ Georgian (Georgia)`
281|`B/. Spanish (Panama)`
282|`Br Oromo (Ethiopia)`
283|`Br Somali (Ethiopia)`
284|`Br Tigrinya (Ethiopia)`
285|`Bs Quechua (Bolivia)`
286|`Bs Spanish (Bolivia)`
287|`BS. Spanish (Venezuela)`
288|`BWP Tswana (Botswana)`
289|`C$ Spanish (Nicaragua)`
290|`CA$ Latin, Inuktitut (Canada)`
291|`CA$ Mohawk (Canada)`
292|`CA$ Unified Canadian Aboriginal Syllabics, Inuktitut (Canada)`
293|`CFA French (Mali)`
294|`CFA French (Senegal)`
295|`CFA Fulah (Senegal)`
296|`CFA Wolof (Senegal)`
297|`CHF French (Switzerland)`
298|`CHF German (Liechtenstein)`
299|`CHF German (Switzerland)`
300|`CHF Italian (Switzerland)`
301|`CHF Romansh (Switzerland)`
302|`CLP Mapuche (Chile)`
303|`CN¥ Mongolian, Mongolian (China)`
304|`DZD Central Atlas Tamazight (Algeria)`
305|`FCFA French (Cameroon)`
306|`Ft Hungarian (Hungary)`
307|`G French (Haiti)`
308|`Gs. Spanish (Paraguay)`
309|`GTQ K'iche' (Guatemala)`
310|`HK$ Chinese (Hong Kong (China))`
311|`HK$ English (Hong Kong (China))`
312|`HRK Croatian (Croatia)`
313|`IDR English (Indonesia)`
314|`IQD Arbic, Central Kurdish (Iraq)`
315|`ISK Icelandic (Iceland)`
316|`K Burmese (Myanmar (Burma))`
317|`Kč Czech (Czech Republic)`
318|`KM Bosnian (Bosnia & Herzegovina)`
319|`KM Croatian (Bosnia & Herzegovina)`
320|`KM Latin, Serbian (Bosnia & Herzegovina)`
321|`kr Faroese (Faroe Islands)`
322|`kr Northern Sami (Norway)`
323|`kr Northern Sami (Sweden)`
324|`kr Norwegian Bokmål (Norway)`
325|`kr Norwegian Nynorsk (Norway)`
326|`kr Swedish (Sweden)`
327|`kr. Danish (Denmark)`
328|`kr. Kalaallisut (Greenland)`
329|`Ksh Swahili (kenya)`
330|`L Romanian (Moldova)`
331|`L Russian (Moldova)`
332|`L Spanish (Honduras)`
333|`Lekë Albanian (Albania)`
334|`MAD Arabic, Central Atlas Tamazight (Morocco)`
335|`MAD French (Morocco)`
336|`MAD Tifinagh, Central Atlas Tamazight (Morocco)`
337|`MOP$ Chinese (Macau (China))`
338|`MVR Divehi (Maldives)`
339|`Nfk Tigrinya (Eritrea)`
340|`NGN Bini (Nigeria)`
341|`NGN Fulah (Nigeria)`
342|`NGN Ibibio (Nigeria)`
343|`NGN Kanuri (Nigeria)`
344|`NOK Lule Sami (Norway)`
345|`NOK Southern Sami (Norway)`
346|`NZ$ Maori (New Zealand)`
347|`PKR Sindhi (Pakistan)`
348|`PYG Guarani (Paraguay)`
349|`Q Spanish (Guatemala)`
350|`R Afrikaans (South Africa)`
351|`R English (South Africa)`
352|`R Zulu (South Africa)`
353|`R$ Portuguese (Brazil)`
354|`RD$ Spanish (Dominican Republic)`
355|`RF Kinyarwanda (Rwanda)`
356|`RM English (Malaysia)`
357|`RM Malay (Malaysia)`
358|`RON Romanian (Romania)`
359|`Rp Indonesoan (Indonesia)`
360|`Rs Urdu (Pakistan)`
361|`Rs. Tamil (Sri Lanka)`
362|`RSD Latin, Serbian (Serbia)`
363|`RSD Serbian (Serbia)`
364|`RUB Bashkir (Russia)`
365|`RUB Tatar (Russia)`
366|`S/. Quechua (Peru)`
367|`S/. Spanish (Peru)`
368|`SEK Lule Sami (Sweden)`
369|`SEK Southern Sami (Sweden)`
370|`soʻm Latin, Uzbek (Uzbekistan)`
371|`soʻm Uzbek (Uzbekistan)`
372|`SYP Syriac (Syria)`
373|`THB Thai (Thailand)`
374|`TMT Turkmen (Turkmenistan)`
375|`US$ English (Zimbabwe)`
376|`ZAR Northern Sotho (South Africa)`
377|`ZAR Southern Sotho (South Africa)`
378|`ZAR Tsonga (South Africa)`
379|`ZAR Tswana (south Africa)`
380|`ZAR Venda (South Africa)`
381|`ZAR Xhosa (South Africa)`
382|`zł Polish (Poland)`
383|`ден Macedonian (Macedonia)`
384|`KM Cyrillic, Bosnian (Bosnia & Herzegovina)`
385|`KM Serbian (Bosnia & Herzegovina)`
386|`лв. Bulgarian (Bulgaria)`
387|`p. Belarusian (Belarus)`
388|`сом Kyrgyz (Kyrgyzstan)`
389|`сом Tajik (Tajikistan)`
390|`ج.م. Arabic (Egypt)`
391|`د.أ. Arabic (Jordan)`
392|`د.أ. Arabic (United Arab Emirates)`
393|`د.ب. Arabic (Bahrain)`
394|`د.ت. Arabic (Tunisia)`
395|`د.ج. Arabic (Algeria)`
396|`د.ع. Arabic (Iraq)`
397|`د.ك. Arabic (Kuwait)`
398|`د.ل. Arabic (Libya)`
399|`د.م. Arabic (Morocco)`
400|`ر Punjabi (Pakistan)`
401|`ر.س. Arabic (Saudi Arabia)`
402|`ر.ع. Arabic (Oman)`
403|`ر.ق. Arabic (Qatar)`
404|`ر.ي. Arabic (Yemen)`
405|`ریال Persian (Iran)`
406|`ل.س. Arabic (Syria)`
407|`ل.ل. Arabic (Lebanon)`
408|`ብር Amharic (Ethiopia)`
409|`रू Nepaol (Nepal)`
410|`රු. Sinhala (Sri Lanka)`
411|`ADP`
412|`AED`
413|`AFA`
414|`AFN`
415|`ALL`
416|`AMD`
417|`ANG`
418|`AOA`
419|`ARS`
420|`ATS`
421|`AUD`
422|`AWG`
423|`AZM`
424|`AZN`
425|`BAM`
426|`BBD`
427|`BDT`
428|`BEF`
429|`BGL`
430|`BGN`
431|`BHD`
432|`BIF`
433|`BMD`
434|`BND`
435|`BOB`
436|`BOV`
437|`BRL`
438|`BSD`
439|`BTN`
440|`BWP`
441|`BYR`
442|`BZD`
443|`CAD`
444|`CDF`
445|`CHE`
446|`CHF`
447|`CHW`
448|`CLF`
449|`CLP`
450|`CNY`
451|`COP`
452|`COU`
453|`CRC`
454|`CSD`
455|`CUC`
456|`CVE`
457|`CYP`
458|`CZK`
459|`DEM`
460|`DJF`
461|`DKK`
462|`DOP`
463|`DZD`
464|`ECS`
465|`ECV`
466|`EEK`
467|`EGP`
468|`ERN`
469|`ESP`
470|`ETB`
471|`EUR`
472|`FIM`
473|`FJD`
474|`FKP`
475|`FRF`
476|`GBP`
477|`GEL`
478|`GHC`
479|`GHS`
480|`GIP`
481|`GMD`
482|`GNF`
483|`GRD`
484|`GTQ`
485|`GYD`
486|`HKD`
487|`HNL`
488|`HRK`
489|`HTG`
490|`HUF`
491|`IDR`
492|`IEP`
493|`ILS`
494|`INR`
495|`IQD`
496|`IRR`
497|`ISK`
498|`ITL`
499|`JMD`
500|`JOD`
501|`JPY`
502|`KAF`
503|`KES`
504|`KGS`
505|`KHR`
506|`KMF`
507|`KPW`
508|`KRW`
509|`KWD`
510|`KYD`
511|`KZT`
512|`LAK`
513|`LBP`
514|`LKR`
515|`LRD`
516|`LSL`
517|`LTL`
518|`LUF`
519|`LVL`
520|`LYD`
521|`MAD`
522|`MDL`
523|`MGA`
524|`MGF`
525|`MKD`
526|`MMK`
527|`MNT`
528|`MOP`
529|`MRO`
530|`MTL`
531|`MUR`
532|`MVR`
533|`MWK`
534|`MXN`
535|`MXV`
536|`MYR`
537|`MZM`
538|`MZN`
539|`NAD`
540|`NGN`
541|`NIO`
542|`NLG`
543|`NOK`
544|`NPR`
545|`NTD`
546|`NZD`
547|`OMR`
548|`PAB`
549|`PEN`
550|`PGK`
551|`PHP`
552|`PKR`
553|`PLN`
554|`PTE`
555|`PYG`
556|`QAR`
557|`ROL`
558|`RON`
559|`RSD`
560|`RUB`
561|`RUR`
562|`RWF`
563|`SAR`
564|`SBD`
565|`SCR`
566|`SDD`
567|`SDG`
568|`SDP`
569|`SEK`
570|`SGD`
571|`SHP`
572|`SIT`
573|`SKK`
574|`SLL`
575|`SOS`
576|`SPL`
577|`SRD`
578|`SRG`
579|`STD`
580|`SVC`
581|`SYP`
582|`SZL`
583|`THB`
584|`TJR`
585|`TJS`
586|`TMM`
587|`TMT`
588|`TND`
589|`TOP`
590|`TRL`
591|`TRY`
592|`TTD`
593|`TWD`
594|`TZS`
595|`UAH`
596|`UGX`
597|`USD`
598|`USN`
599|`USS`
600|`UYI`
601|`UYU`
602|`UZS`
603|`VEB`
604|`VEF`
605|`VND`
606|`VUV`
607|`WST`
608|`XAF`
609|`XAG`
610|`XAU`
611|`XB5`
612|`XBA`
613|`XBB`
614|`XBC`
615|`XBD`
616|`XCD`
617|`XDR`
618|`XFO`
619|`XFU`
620|`XOF`
621|`XPD`
622|`XPF`
623|`XPT`
624|`XTS`
625|`XXX`
626|`YER`
627|`YUM`
628|`ZAR`
629|`ZMK`
630|`ZMW`
631|`ZWD`
632|`ZWL`
633|`ZWN`
634|`ZWR`

Поддержка Excelize устанавливает пользовательский формат номера для ячейки. Например, установите номер в качестве типа даты в формате Уругвай (испанский) для `Sheet1!A6`:

!["Установить формат номера"](./images/number_format_01.png "Установить формат номера")

```go
xlsx := excelize.NewFile()
xlsx.SetCellValue("Sheet1", "A6", 42920.5)
style, _ := xlsx.NewStyle(`{"custom_number_format": "[$-380A]dddd\\,\\ dd\" de \"mmmm\" de \"yyyy;@"}`)
xlsx.SetCellStyle("Sheet1", "A6", "A6", style)
```

клетка `Sheet1!A6` в приложении Excel: `martes, 04 de Julio de 2017`
