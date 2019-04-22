# Введение

<p align="center"><img width="650" src="../images/excelize.png" alt="Excelize logo"></p>

<p align="center">
    <a href="https://travis-ci.org/360EntSecGroup-Skylar/excelize"><img src="https://travis-ci.org/360EntSecGroup-Skylar/excelize.svg?branch=master" alt="Build Status"></a>
    <a href="https://codecov.io/gh/360EntSecGroup-Skylar/excelize"><img src="https://codecov.io/gh/360EntSecGroup-Skylar/excelize/branch/master/graph/badge.svg" alt="Code Coverage"></a>
    <a href="https://goreportcard.com/report/github.com/360EntSecGroup-Skylar/excelize"><img src="https://goreportcard.com/badge/github.com/360EntSecGroup-Skylar/excelize" alt="Go Report Card"></a>
    <a href="https://godoc.org/github.com/360EntSecGroup-Skylar/excelize"><img src="https://godoc.org/github.com/360EntSecGroup-Skylar/excelize?status.svg" alt="GoDoc"></a>
    <a href="https://opensource.org/licenses/BSD-3-Clause"><img src="https://img.shields.io/badge/license-bsd-orange.svg" alt="Licenses"></a>
    <a href="https://www.paypal.me/xuri"><img src="https://img.shields.io/badge/Donate-PayPal-green.svg" alt="Donate"></a>
</p>

Excelize - это библиотека, написанная на чистом Go и предоставляющая набор функций, которые позволяют вам писать и читать из файлов XLSX. Поддержка чтения и записи файла XLSX, созданного Microsoft Excel&trade; 2007 и более поздних версий. Поддержка сохранения файла без потери оригинальных графиков XLSX. Эта библиотека нуждается в версии 1.8 или более поздней.

- Исходный код: [github.com/360EntSecGroup-Skylar/excelize](https://github.com/360EntSecGroup-Skylar/excelize)
- вопрос: [github.com/360EntSecGroup-Skylar/excelize/issues](https://github.com/360EntSecGroup-Skylar/excelize/issues)
- GoDoc: [godoc.org/github.com/360EntSecGroup-Skylar/excelize](https://godoc.org/github.com/360EntSecGroup-Skylar/excelize)
- Лицензии: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- Последняя версия: [v2.0.0](https://github.com/360EntSecGroup-Skylar/excelize/releases/latest)
- Время обновления документа: 16 марш 2019 г.

## Миссия проекта

Целью Excelize является создание и поддержка языковой версии Go API документов Excel для обработки файлов xlsx, соответствующих стандарту Office Open XML (OOXML). С помощью Excelize вы можете использовать Go для чтения и записи файлов MS Excel.

## Зачем использовать Excelize

В некоторых случаях нам нужно манипулировать документами Excel через программы, такие как: открывать для чтения существующий документ Excel, создавать новые документы Excel, создавать новые документы Excel на основе существующих документов (шаблонов), вставлять изображения в документы Excel, диаграммы Элементы такие как таблицы, и иногда им необходимо реализовать эти операции на разных платформах. Excelize может легко удовлетворить эти потребности.

## Известные клиенты

<a href="https://360.net" title="360 Группа безопасности предприятия" target="_blank"><img width="165" src="../images/vendor/360@2x.png" alt="360 Группа безопасности предприятия"></a> <a href="https://www.baidu.com" title="Baidu, Inc." target="_blank"><img width="165" src="../images/vendor/baidu@2x.png" alt="Baidu, Inc."></a> [![CCi. Inc.](../images/vendor/ccint.com.png)](https://www.ccint.com) <a href="https://www.inke.cn" title="Inke, Inc." target="_blank"><img width="165" src="../images/vendor/inke@2x.png" alt="Inke, Inc."></a> <a href="https://www.meituan.com" title="Meituan-Dianping" target="_blank"><img width="165" src="../images/vendor/meituan@2x.png" alt="Meituan-Dianping"></a> <a href="https://www.163.com" title="NetEase" target="_blank"><img width="165" src="../images/vendor/netease@2x.png" alt="NetEase"></a>

Если ваша компания или продукт также использует Excelize, добро пожаловать на [отправку](mailto: xuri.me@gmail.com?Subject=Please add our company in Excelize Introduction page&amp;Body=Hello%2C%20this%20is%20%3Cyour%20name%3E%20from%20%3Cyour%20company%20name%3E.%0AWe%20are%20using%20Excelize%20and%20will%20be%20proud%20to%20add%20our%20company%20name%20to%20Excelize%20Introduction%20page.%0APlease%20see%20attachment%20for%20our%20logo.%20%3CBe%20sure%20to%20include%20logo%20in%20attachment%3E%0A) логотипа нам.