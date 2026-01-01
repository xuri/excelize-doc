# Einleitung

<p align="center"><img width="650" src="../images/excelize.svg" alt="Excelize logo"></p>

Excelize ist eine Bibliothek, die in reinem Go geschrieben wurde und eine Reihe von Funktionen bereitstellt, mit denen Sie in XLAM / XLSM / XLSX / XLTM / XLTX-Dateien schreiben und sie aus ihnen lesen können. Unterstützt das Lesen und Schreiben von Tabellenkalkulationsdokumenten, die von Microsoft Excel&trade; 2007 und höher generiert wurden. Unterstützt komplexe Komponenten durch hohe Kompatibilität und bereitgestellte Streaming-API zum Generieren oder Lesen von Daten aus einem Arbeitsblatt mit riesigen Datenmengen. Diese Bibliothek benötigt Go Version 1.23.0 oder höher.

- Quellcode: [github.com/xuri/excelize](https://github.com/xuri/excelize)
- Problem: [github.com/xuri/excelize/issues](https://github.com/xuri/excelize/issues)
- go.dev: [pkg.go.dev/github.com/xuri/excelize/v2](https://pkg.go.dev/github.com/xuri/excelize/v2)
- Lizenzen: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- Letzte Version: [v2.10.0](https://github.com/xuri/excelize/releases/latest)
- Dokument Aktualisierungszeit: Januar 1, 2026

## Project mission

Das Ziel von Excelize besteht darin, eine Go-Sprachversion der Excel-Dokument-API zu erstellen und zu verwalten, um xlsx-Dateien zu verarbeiten, die dem Office Open XML (OOXML)-Standard entsprechen. Mit Excelize können Sie Go zum Lesen und Schreiben von MS Excel-Dateien verwenden.

## Warum Excelize verwenden

In einigen Fällen müssen wir Excel-Dokumente über Programme bearbeiten, z. B.: Öffnen, um vorhandene Excel-Dokumentinhalte zu lesen, neue Excel-Dokumente zu erstellen, neue Excel-Dokumente basierend auf vorhandenen Dokumenten (Vorlagen) zu generieren, Bilder in Excel-Dokumente einzufügen, Diagramme Elemente wie Tabellen und manchmal diese Vorgänge plattformübergreifend implementieren müssen. Excelize kann diese Anforderungen problemlos erfüllen.

## Bekannte Kunden

<img width="165" src="../images/vendor/360@2x.png" alt="Qihoo 360"> <img width="165" src="../images/vendor/baidu@2x.png" alt="Baidu, Inc."> ![INTSIG](../images/vendor/intsig.com_en.png) <img width="165" src="../images/vendor/inke@2x.png" alt="Inke, Inc."> <img width="165" src="../images/vendor/meituan@2x.png" alt="Meituan-Dianping"> <img width="165" src="../images/vendor/netease@2x.png" alt="NetEase"> <img width="165" src="../images/vendor/bilibili@2x.png" alt="Bilibili"> <img width="165" src="../images/vendor/qianxin.com_en@2x.png" alt="Qi An Xin Group"> <img width="165" src="../images/vendor/alibabagroup@2x.png" alt="Alibaba Group"> <img width="165" src="../images/vendor/ele.me@2x.png" alt="ele.me"> <img width="165" src="../images/vendor/huifu.com@2x.png" alt="Huifu"> <img width="165" src="../images/vendor/dodoca.com@2x.png" alt="Dodoca Information Technology"> <img width="165" src="../images/vendor/bytedance@2x.png" alt="ByteDance"> <img width="165" src="../images/vendor/flashexpress.com@2x.png" alt="Flash Express"> <img width="165" src="../images/vendor/jimengio.com@2x.png" alt="JimengIO"> <img width="165" src="../images/vendor/shannonai.com@2x.png" alt="Shannon.AI"> <img width="165" src="../images/vendor/ibm@2x.png" alt="IBM"> <img width="165" src="../images/vendor/basedig.com@2x.png" alt="Basedig"> <img width="165" src="../images/vendor/meitu.com@2x.png" alt="Meitui"> <img width="165" src="../images/vendor/amazon@2x.png" alt="Amazon"> <img width="165" src="../images/vendor/deloitte@2x.png" alt="Deloitte"> <img width="165" src="../images/vendor/cisco@2x.png" alt="Cisco"> <img width="165" src="../images/vendor/nl-a.ru@2x.png" alt="Neuro Lab! Algorithms"> <img width="165" src="../images/vendor/58.com@2x.png" alt="58.com"> <img width="165" src="../images/vendor/ke.com@2x.png" alt="ke.com"> <img width="165" src="../images/vendor/microsoft@2x.png" alt="Microsoft"> <img width="165" src="../images/vendor/bytebase.com@2x.png" alt="ByteBase"> <img width="165" src="../images/vendor/intel@2x.png" alt="Intel"> <img width="165" src="../images/vendor/icbc.com.cn@2x.png" alt="Industrial and Commercial Bank of China"> <img width="165" src="../images/vendor/ccb.com@2x.png" alt="China Construction Bank"> <img width="165" src="../images/vendor/chinatelecom@2x.png" alt="China Telecommunications Corporation"> <img width="165" src="../images/vendor/tencent@2x.png" alt="Tencent"> <img width="165" src="../images/vendor/mihoyo@2x.png" alt="miHoYo"> <img width="165" src="../images/vendor/nsfocus@2x.png" alt="NSFOCUS Technologies Group Co Ltd"> <img width="165" src="../images/vendor/gree.com@2x.png" alt="Gree"> <img width="165" src="../images/vendor/jd.com@2x.png" alt="JD.com, Inc."> <img width="165" src="../images/vendor/zhiyitech.cn@2x.png" alt="Hangzhou Zhiyi Technology Co., Ltd.">

Wenn Ihr Unternehmen oder Produkt auch Excelize verwendet, begrüßen Sie <a href="mailto: xuri.me@gmail.com?Subject=Bitte%20f%C3%BCgen%20Sie%20unser%20Unternehmen%20auf%20der%20Excelize-Einf%C3%BChrungsseite%20hinzu&amp;Body=Hallo%2C%20hier%20ist%20%3CIhr%20Name%3E%20von%20%3CName%20Ihres%20Unternehmens%3E.%0AWir%20verwenden%20Excelize%20und%20sind%20stolz%20darauf%2C%20unseren%20Firmennamen%20zur%20Excelize-Einf%C3%BChrungsseite%20hinzuzuf%C3%BCgen.%0AUnser%20Logo%20finden%20Sie%20im%20Anhang.%20%3CAchten%20Sie%20darauf%2C%20das%20Logo%20im%20Anhang%20beizuf%C3%BCgen%3E%0A" title="send Logo via E-mail">Logo senden</a> an uns.

## Gemeinschaft

- [Facebook Gruppe](https://www.facebook.com/groups/excelize)
- [Google Gruppe](https://groups.google.com/g/excelize)
- [Stapelüberlauf](https://stackoverflow.com/questions/tagged/excelize)
- [Slack-Kanal](https://join.slack.com/t/xuri/shared_invite/zt-eriqdkeo-wV04zcCdBiiZveFgY86Wzw)
- [Gitter](https://gitter.im/excelize/community)
- [Community auf Telegram](https://t.me/excelize)
- [Community auf Discord](https://discord.gg/MWV8MBQGtv)
- [Excelize Community in Microsoft Teams](https://teams.live.com/l/invite/FBA8aHkflqEj5SNzQM)
- [Line Community](http://line.me/ti/g/NFIjhfbP_g): <a href="../images/line_group@2x.png" title="Excelize Line Community" target="_blank">Teilnahme per QR-Code</a>
- [DingTalk Gruppen ID](https://qr.dingtalk.com/action/joingroup?code=v1,k1,6tmzbBbJuQkGezVdHJjsHz29CZI9F49xeW+cvOaECtk=&_dt_no_comment=1&origin=11): `30047129` | <a href="../images/dingtalk_group@2x.png" title="Excelize DingTalk Group" target="_blank">Teilnahme per QR-Code</a>
- QQ DingTalk ID: `1302058237` (Verifizierungsinformationen: Excelize) | <a href="../images/qq_group@2x.png" title="Excelize QQ DingTalk ID" target="_blank">Teilnahme per QR-Code</a>
- Excelize WeChat ID: `hixuri` (Verifizierungsinformationen: Excelize) | <a href="../images/wechat_group@2x.png" title="Excelize WeChat Community" target="_blank">Teilnahme per QR-Code</a>
- WeCom DingTalk (Verifizierungsinformationen: Excelize): <a href="../images/wecom_group@2x.png" title="Excelize WeCom DingTalk" target="_blank">Teilnahme per QR-Code</a>
- Inflow DingTalk ID: `4375928` | <a href="../images/inflow_group@2x.png" title="Excelize Inflow DingTalk" target="_blank">Teilnahme per QR-Code</a>

## Sponsor Excelize Development

Wenn Sie ein einzelner Benutzer sind und die Produktivität der Verwendung von Excelize genossen haben, betrachten Sie das Essen als Zeichen der Wertschätzung - wie mir Kaffee zu kaufen ab und zu. Unterstützen Sie dieses Projekt, indem Sie Sponsor werden.

<a href="https://github.com/sponsors/xuri" title="GitHub Sponsor" target="_blank"><img width="170" src="../images/github_sponsor@2x.png" alt="GitHub Sponsor"></a> <a href="https://www.paypal.com/paypalme/xuri" title="Spenden mit PayPal" target="_blank"><img width="170" src="../images/donate@2x.png" alt="Spenden mit PayPal"></a> <a href="https://opencollective.com/excelize" title="Werden Sie Sponsor" target="_blank"><img height="61" src="../images/opencollective.com@2x.png" alt="Werden Sie Sponsor"></a> <a href="https://www.patreon.com/xuri" title="Unterstützen Sie Excelize auf Patreon" target="_blank"><img height="61" src="../images/patreon.com@2x.png" alt="Unterstützen Sie Excelize auf Patreon"></a>
