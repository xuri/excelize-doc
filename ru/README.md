# Введение

<p align="center"><img width="650" src="../images/excelize.svg" alt="Excelize logo"></p>

EXCELIZE - это библиотека, написанная на чистом Go, предоставляющая набор функций, которые позволяют записывать и читать файлы XLSX / XLSM / XLTM. Поддерживает чтение и запись электронных таблиц, созданных в Microsoft Excel 2007 и более поздних версиях. Поддерживает сложные компоненты благодаря высокой совместимости и предоставляет потоковый API для генерации или чтения данных из листа с огромными объемами данных. Эта библиотека нуждается в версии 1.10 или более поздней.

- Исходный код: [github.com/360EntSecGroup-Skylar/excelize](https://github.com/360EntSecGroup-Skylar/excelize)
- вопрос: [github.com/360EntSecGroup-Skylar/excelize/issues](https://github.com/360EntSecGroup-Skylar/excelize/issues)
- go.dev: [pkg.go.dev/github.com/360EntSecGroup-Skylar/excelize/v2?tab=doc](https://pkg.go.dev/github.com/360EntSecGroup-Skylar/excelize/v2?tab=doc)
- Лицензии: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- Последняя версия: [v2.2.0](https://github.com/360EntSecGroup-Skylar/excelize/releases/latest)
- Время обновления документа: 20 Мэй 2020 г.

## Миссия проекта

Целью Excelize является создание и поддержка языковой версии Go API документов Excel для обработки файлов xlsx, соответствующих стандарту Office Open XML (OOXML). С помощью Excelize вы можете использовать Go для чтения и записи файлов MS Excel.

## Зачем использовать Excelize

В некоторых случаях нам нужно манипулировать документами Excel через программы, такие как: открывать для чтения существующий документ Excel, создавать новые документы Excel, создавать новые документы Excel на основе существующих документов (шаблонов), вставлять изображения в документы Excel, диаграммы Элементы такие как таблицы, и иногда им необходимо реализовать эти операции на разных платформах. Excelize может легко удовлетворить эти потребности.

## Известные клиенты

<a href="https://www.360.cn" title="Qihoo 360" target="_blank"><img width="165" src="../images/vendor/360@2x.png" alt="Qihoo 360"></a> <a href="https://www.baidu.com" title="Baidu, Inc." target="_blank"><img width="165" src="../images/vendor/baidu@2x.png" alt="Baidu, Inc."></a> [![CCi. Inc.](../images/vendor/ccint.com.png)](https://www.ccint.com) <a href="https://www.inke.cn" title="Inke, Inc." target="_blank"><img width="165" src="../images/vendor/inke@2x.png" alt="Inke, Inc."></a> <a href="https://www.meituan.com" title="Meituan-Dianping" target="_blank"><img width="165" src="../images/vendor/meituan@2x.png" alt="Meituan-Dianping"></a> <a href="https://www.163.com" title="NetEase" target="_blank"><img width="165" src="../images/vendor/netease@2x.png" alt="NetEase"></a> <a href="https://www.bilibili.com" title="Bilibili" target="_blank"><img width="165" src="../images/vendor/bilibili@2x.png" alt="Bilibili"></a> <a href="https://www.qianxin.com" title="Qi An Xin Group" target="_blank"><img width="165" src="../images/vendor/qianxin.com_en@2x.png" alt="Qi An Xin Group"></a> <a href="https://www.alibabagroup.com" title="Alibaba Group" target="_blank"><img width="165" src="../images/vendor/alibabagroup@2x.png" alt="Alibaba Group"></a> <a href="https://www.ele.me" title="ele.me" target="_blank"><img width="165" src="../images/vendor/ele.me@2x.png" alt="ele.me"></a> <a href="https://www.huifu.com" title="Huifu" target="_blank"><img width="165" src="../images/vendor/huifu.com@2x.png" alt="Huifu"></a> <a href="https://www.dodoca.com" title="Dodoca Information Technology" target="_blank"><img width="165" src="../images/vendor/dodoca.com@2x.png" alt="Dodoca Information Technology"></a> <a href="https://bytedance.com" title="ByteDance" target="_blank"><img width="165" src="../images/vendor/bytedance@2x.png" alt="ByteDance"></a> <a href="https://www.flashexpress.com" title="Flash Express" target="_blank"><img width="165" src="../images/vendor/flashexpress.com@2x.png" alt="Flash Express"></a> <a href="https://jimengio.com" title="JimengIO" target="_blank"><img width="165" src="../images/vendor/jimengio.com@2x.png" alt="JimengIO"></a>

Если ваша компания или продукт также использует Excelize, добро пожаловать на <a href="mailto: xuri.me@gmail.com?Subject=Please add our company in Excelize Introduction page&amp;Body=Hello%2C%20this%20is%20%3Cyour%20name%3E%20from%20%3Cyour%20company%20name%3E.%0AWe%20are%20using%20Excelize%20and%20will%20be%20proud%20to%20add%20our%20company%20name%20to%20Excelize%20Introduction%20page.%0APlease%20see%20attachment%20for%20our%20logo.%20%3CBe%20sure%20to%20include%20logo%20in%20attachment%3E%0A" title="отправку">отправку</a> логотипа нам.

<a href="https://join.slack.com/t/xuri/shared_invite/zt-eriqdkeo-wV04zcCdBiiZveFgY86Wzw" title="Excelize Slack Channel" target="_blank"><img style="margin-top: 25px;" height="60" src="../images/slack.svg" alt="Excelize Slack Channel"></a>

## Спонсор Excelize разработки

Если вы являетесь индивидуальным пользователем и наслаждаетесь продуктивностью использования Excelize, подумайте о том, чтобы пожертвовать как признак признательности - как покупка кофе время от времени.

<a href="https://www.paypal.me/xuri" title="Пожертвовать с помощью Paypal" target="_blank"><img width="170" src="../images/donate@2x.png" alt="Пожертвовать с помощью Paypal"></a>
