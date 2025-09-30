# Введение

<p align="center"><img width="650" src="../images/excelize.svg" alt="Excelize logo"></p>

EXCELIZE - это библиотека, написанная на чистом Go, предоставляющая набор функций, которые позволяют записывать и читать файлы XLAM / XLSM / XLSX / XLTM / XLTX. Поддерживает чтение и запись электронных таблиц, созданных в Microsoft Excel 2007 и более поздних версиях. Поддерживает сложные компоненты благодаря высокой совместимости и предоставляет потоковый API для генерации или чтения данных из листа с огромными объемами данных. Эта библиотека нуждается в версии 1.23.0 или более поздней.

- Исходный код: [github.com/xuri/excelize](https://github.com/xuri/excelize)
- вопрос: [github.com/xuri/excelize/issues](https://github.com/xuri/excelize/issues)
- go.dev: [pkg.go.dev/github.com/xuri/excelize/v2](https://pkg.go.dev/github.com/xuri/excelize/v2)
- Лицензии: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- Последняя версия: [v2.9.1](https://github.com/xuri/excelize/releases/latest)
- Время обновления документа: 30 сентябрь 2025 г.

## Миссия проекта

Целью Excelize является создание и поддержка языковой версии Go API документов Excel для обработки файлов xlsx, соответствующих стандарту Office Open XML (OOXML). С помощью Excelize вы можете использовать Go для чтения и записи файлов MS Excel.

## Зачем использовать Excelize

В некоторых случаях нам нужно манипулировать документами Excel через программы, такие как: открывать для чтения существующий документ Excel, создавать новые документы Excel, создавать новые документы Excel на основе существующих документов (шаблонов), вставлять изображения в документы Excel, диаграммы Элементы такие как таблицы, и иногда им необходимо реализовать эти операции на разных платформах. Excelize может легко удовлетворить эти потребности.

## Известные клиенты

<img width="165" src="../images/vendor/360@2x.png" alt="Qihoo 360"> <img width="165" src="../images/vendor/baidu@2x.png" alt="Baidu, Inc."> ![INTSIG](../images/vendor/intsig.com_en.png) <img width="165" src="../images/vendor/inke@2x.png" alt="Inke, Inc."> <img width="165" src="../images/vendor/meituan@2x.png" alt="Meituan-Dianping"> <img width="165" src="../images/vendor/netease@2x.png" alt="NetEase"> <img width="165" src="../images/vendor/bilibili@2x.png" alt="Bilibili"> <img width="165" src="../images/vendor/qianxin.com_en@2x.png" alt="Qi An Xin Group"> <img width="165" src="../images/vendor/alibabagroup@2x.png" alt="Alibaba Group"> <img width="165" src="../images/vendor/ele.me@2x.png" alt="ele.me"> <img width="165" src="../images/vendor/huifu.com@2x.png" alt="Huifu"> <img width="165" src="../images/vendor/dodoca.com@2x.png" alt="Dodoca Information Technology"> <img width="165" src="../images/vendor/bytedance@2x.png" alt="ByteDance"> <img width="165" src="../images/vendor/flashexpress.com@2x.png" alt="Flash Express"> <img width="165" src="../images/vendor/jimengio.com@2x.png" alt="JimengIO"> <img width="165" src="../images/vendor/shannonai.com@2x.png" alt="Shannon.AI"> <img width="165" src="../images/vendor/ibm@2x.png" alt="IBM"> <img width="165" src="../images/vendor/basedig.com@2x.png" alt="Basedig"> <img width="165" src="../images/vendor/meitu.com@2x.png" alt="Meitui"> <img width="165" src="../images/vendor/amazon@2x.png" alt="Amazon"> <img width="165" src="../images/vendor/deloitte@2x.png" alt="Deloitte"> <img width="165" src="../images/vendor/cisco@2x.png" alt="Cisco"> <img width="165" src="../images/vendor/nl-a.ru@2x.png" alt="Neuro Lab! Algorithms"> <img width="165" src="../images/vendor/58.com@2x.png" alt="58.com"> <img width="165" src="../images/vendor/ke.com@2x.png" alt="ke.com"> <img width="165" src="../images/vendor/microsoft@2x.png" alt="Microsoft"> <img width="165" src="../images/vendor/bytebase.com@2x.png" alt="ByteBase"> <img width="165" src="../images/vendor/intel@2x.png" alt="Intel"> <img width="165" src="../images/vendor/icbc.com.cn@2x.png" alt="Industrial and Commercial Bank of China"> <img width="165" src="../images/vendor/ccb.com@2x.png" alt="China Construction Bank"> <img width="165" src="../images/vendor/chinatelecom@2x.png" alt="China Telecommunications Corporation"> <img width="165" src="../images/vendor/tencent@2x.png" alt="Tencent"> <img width="165" src="../images/vendor/mihoyo@2x.png" alt="miHoYo"> <img width="165" src="../images/vendor/nsfocus@2x.png" alt="NSFOCUS Technologies Group Co Ltd"> <img width="165" src="../images/vendor/gree.com@2x.png" alt="Gree"> <img width="165" src="../images/vendor/jd.com@2x.png" alt="JD.com, Inc."> <img width="165" src="../images/vendor/zhiyitech.cn@2x.png" alt="Hangzhou Zhiyi Technology Co., Ltd.">

Если ваша компания или продукт также использует Excelize, добро пожаловать на <a href="mailto: xuri.me@gmail.com?Subject=%D0%9F%D0%BE%D0%B6%D0%B0%D0%BB%D1%83%D0%B9%D1%81%D1%82%D0%B0%2C%20%D0%B4%D0%BE%D0%B1%D0%B0%D0%B2%D1%8C%D1%82%D0%B5%20%D0%BD%D0%B0%D1%88%D1%83%20%D0%BA%D0%BE%D0%BC%D0%BF%D0%B0%D0%BD%D0%B8%D1%8E%20%D0%BD%D0%B0%20%D1%81%D1%82%D1%80%D0%B0%D0%BD%D0%B8%D1%86%D1%83%20%D0%B2%D0%B2%D0%B5%D0%B4%D0%B5%D0%BD%D0%B8%D1%8F%20Excelize&amp;Body=%D0%97%D0%B4%D1%80%D0%B0%D0%B2%D1%81%D1%82%D0%B2%D1%83%D0%B9%D1%82%D0%B5%2C%20%D1%8D%D1%82%D0%BE%20%3C%D0%B2%D0%B0%D1%88%D0%B5%20%D0%B8%D0%BC%D1%8F%3E%20%D0%B8%D0%B7%20%3C%D0%BD%D0%B0%D0%B7%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5%20%D0%B2%D0%B0%D1%88%D0%B5%D0%B9%20%D0%BA%D0%BE%D0%BC%D0%BF%D0%B0%D0%BD%D0%B8%D0%B8%3E.%0A%D0%9C%D1%8B%20%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D1%83%D0%B5%D0%BC%20Excelize%20%D0%B8%20%D0%B1%D1%83%D0%B4%D0%B5%D0%BC%20%D1%80%D0%B0%D0%B4%D1%8B%20%D0%B4%D0%BE%D0%B1%D0%B0%D0%B2%D0%B8%D1%82%D1%8C%20%D0%BD%D0%B0%D0%B7%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5%20%D0%BD%D0%B0%D1%88%D0%B5%D0%B9%20%D0%BA%D0%BE%D0%BC%D0%BF%D0%B0%D0%BD%D0%B8%D0%B8%20%D0%BD%D0%B0%20%D1%81%D1%82%D1%80%D0%B0%D0%BD%D0%B8%D1%86%D1%83%20%D0%B2%D0%B2%D0%B5%D0%B4%D0%B5%D0%BD%D0%B8%D1%8F%20Excelize.%0A%D0%9F%D0%BE%D0%B6%D0%B0%D0%BB%D1%83%D0%B9%D1%81%D1%82%D0%B0%2C%20%D1%81%D0%BC%D0%BE%D1%82%D1%80%D0%B8%D1%82%D0%B5%20%D0%B2%20%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B8%20%D0%BD%D0%B0%D1%88%20%D0%BB%D0%BE%D0%B3%D0%BE%D1%82%D0%B8%D0%BF.%20%3C%D0%9E%D0%B1%D1%8F%D0%B7%D0%B0%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D0%BE%20%D1%83%D0%BA%D0%B0%D0%B6%D0%B8%D1%82%D0%B5%20%D0%BB%D0%BE%D0%B3%D0%BE%D1%82%D0%B8%D0%BF%20%D0%B2%D0%BE%20%D0%B2%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B8%3E%0A" title="отправку">отправку</a> логотипа нам.

## Сообщество

- [Группа в Фейсбуке](https://www.facebook.com/groups/excelize)
- [Группа Google](https://groups.google.com/g/excelize)
- [Переполнение стека](https://stackoverflow.com/questions/tagged/excelize)
- [Slack-канал](https://join.slack.com/t/xuri/shared_invite/zt-eriqdkeo-wV04zcCdBiiZveFgY86Wzw)
- [Gitter](https://gitter.im/excelize/community)
- [Сообщество в Telegram](https://t.me/excelize)
- [Сообщество в Discord](https://discord.gg/MWV8MBQGtv)
- [Сообщество Excelize в Microsoft Teams](https://teams.live.com/l/invite/FBA8aHkflqEj5SNzQM)
- [Линия Сообщества](http://line.me/ti/g/NFIjhfbP_g): <a href="../images/line_group@2x.png" title="Excelize Line Community" target="_blank">присоединиться через QR-код</a>
- [Идентификатор группы DingTalk](https://qr.dingtalk.com/action/joingroup?code=v1,k1,6tmzbBbJuQkGezVdHJjsHz29CZI9F49xeW+cvOaECtk=&_dt_no_comment=1&origin=11): `30047129` | <a href="../images/dingtalk_group@2x.png" title="Excelize DingTalk Group" target="_blank">присоединиться через QR-код</a>
- QQ Group ID: `1302058237` (Информация о проверке: Excelize) | <a href="../images/qq_group@2x.png" title="Excelize QQ Group ID" target="_blank">присоединиться через QR-код</a>
- Excelize WeChat ID: `hixuri` (Информация о проверке: Excelize) | <a href="../images/wechat_group@2x.png" title="Excelize WeChat Community" target="_blank">присоединиться через QR-код</a>
- WeCom Group (Информация о проверке: Excelize): <a href="../images/wecom_group@2x.png" title="Excelize WeCom Group" target="_blank">присоединиться через QR-код</a>
- Inflow Group ID: `4375928` | <a href="../images/inflow_group@2x.png" title="Excelize Inflow Group" target="_blank">присоединиться через QR-код</a>

## Спонсор Excelize разработки

Если вы являетесь индивидуальным пользователем и наслаждаетесь продуктивностью использования Excelize, подумайте о том, чтобы пожертвовать как признак признательности - как покупка кофе время от времени. Поддержите этот проект, став спонсором.

<a href="https://github.com/sponsors/xuri" title="GitHub Sponsor" target="_blank"><img width="170" src="../images/github_sponsor@2x.png" alt="GitHub Sponsor"></a> <a href="https://www.paypal.com/paypalme/xuri" title="Пожертвовать с помощью Paypal" target="_blank"><img width="170" src="../images/donate@2x.png" alt="Пожертвовать с помощью Paypal"></a> <a href="https://opencollective.com/excelize" title="Стать спонсором" target="_blank"><img height="61" src="../images/opencollective.com@2x.png" alt="Стать спонсором"></a> <a href="https://www.patreon.com/xuri" title="Поддержка Excelize на Patreon" target="_blank"><img height="61" src="../images/patreon.com@2x.png" alt="Поддержка Excelize на Patreon"></a>
