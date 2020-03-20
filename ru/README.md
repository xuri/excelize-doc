# Введение

<p align="center"><img width="650" src="../images/excelize.svg" alt="Excelize logo"></p>

Excelize - это библиотека, написанная на чистом Go и предоставляющая набор функций, которые позволяют вам писать и читать из файлов XLSX. Поддержка чтения и записи файла XLSX, созданного Microsoft Excel&trade; 2007 и более поздних версий. Поддержка сохранения файла без потери оригинальных графиков XLSX. Эта библиотека нуждается в версии 1.10 или более поздней.

- Исходный код: [github.com/360EntSecGroup-Skylar/excelize](https://github.com/360EntSecGroup-Skylar/excelize)
- вопрос: [github.com/360EntSecGroup-Skylar/excelize/issues](https://github.com/360EntSecGroup-Skylar/excelize/issues)
- go.dev: [pkg.go.dev/github.com/360EntSecGroup-Skylar/excelize/v2?tab=doc](https://pkg.go.dev/github.com/360EntSecGroup-Skylar/excelize/v2?tab=doc)
- Лицензии: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- Последняя версия: [v2.1.0](https://github.com/360EntSecGroup-Skylar/excelize/releases/latest)
- Время обновления документа: 21 март 2020 г.

## Миссия проекта

Целью Excelize является создание и поддержка языковой версии Go API документов Excel для обработки файлов xlsx, соответствующих стандарту Office Open XML (OOXML). С помощью Excelize вы можете использовать Go для чтения и записи файлов MS Excel.

## Зачем использовать Excelize

В некоторых случаях нам нужно манипулировать документами Excel через программы, такие как: открывать для чтения существующий документ Excel, создавать новые документы Excel, создавать новые документы Excel на основе существующих документов (шаблонов), вставлять изображения в документы Excel, диаграммы Элементы такие как таблицы, и иногда им необходимо реализовать эти операции на разных платформах. Excelize может легко удовлетворить эти потребности.

## Известные клиенты

<a href="https://www.360.cn" title="Qihoo 360" target="_blank"><img width="165" src="../images/vendor/360@2x.png" alt="Qihoo 360"></a> <a href="https://www.baidu.com" title="Baidu, Inc." target="_blank"><img width="165" src="../images/vendor/baidu@2x.png" alt="Baidu, Inc."></a> [![CCi. Inc.](../images/vendor/ccint.com.png)](https://www.ccint.com) <a href="https://www.inke.cn" title="Inke, Inc." target="_blank"><img width="165" src="../images/vendor/inke@2x.png" alt="Inke, Inc."></a> <a href="https://www.meituan.com" title="Meituan-Dianping" target="_blank"><img width="165" src="../images/vendor/meituan@2x.png" alt="Meituan-Dianping"></a> <a href="https://www.163.com" title="NetEase" target="_blank"><img width="165" src="../images/vendor/netease@2x.png" alt="NetEase"></a> <a href="https://www.bilibili.com" title="Bilibili" target="_blank"><img width="165" src="../images/vendor/bilibili@2x.png" alt="Bilibili"></a> <a href="https://www.qianxin.com" title="Qi An Xin Group" target="_blank"><img width="165" src="../images/vendor/qianxin.com_en@2x.png" alt="Qi An Xin Group"></a> <a href="https://www.alibabagroup.com" title="Alibaba Group" target="_blank"><img width="165" src="../images/vendor/alibabagroup@2x.png" alt="Alibaba Group"></a> <a href="https://www.ele.me" title="ele.me" target="_blank"><img width="165" src="../images/vendor/ele.me@2x.png" alt="ele.me"></a> <a href="https://www.huifu.com" title="Huifu" target="_blank"><img width="165" src="../images/vendor/huifu.com@2x.png" alt="Huifu"></a> <a href="https://www.dodoca.com" title="Dodoca Information Technology" target="_blank"><img width="165" src="../images/vendor/dodoca.com@2x.png" alt="Dodoca Information Technology"></a> <a href="https://bytedance.com" title="ByteDance" target="_blank"><img width="165" src="../images/vendor/bytedance@2x.png" alt="ByteDance"></a> <a href="https://www.flashexpress.com" title="Flash Express" target="_blank"><img width="165" src="../images/vendor/flashexpress.com@2x.png" alt="Flash Express"></a> <a href="https://jimengio.com" title="JimengIO" target="_blank"><img width="165" src="../images/vendor/jimengio.com@2x.png" alt="JimengIO"></a>

Если ваша компания или продукт также использует Excelize, добро пожаловать на <a href="mailto: xuri.me@gmail.com?Subject=Please add our company in Excelize Introduction page&amp;Body=Hello%2C%20this%20is%20%3Cyour%20name%3E%20from%20%3Cyour%20company%20name%3E.%0AWe%20are%20using%20Excelize%20and%20will%20be%20proud%20to%20add%20our%20company%20name%20to%20Excelize%20Introduction%20page.%0APlease%20see%20attachment%20for%20our%20logo.%20%3CBe%20sure%20to%20include%20logo%20in%20attachment%3E%0A" title="отправку">отправку</a> логотипа нам.
