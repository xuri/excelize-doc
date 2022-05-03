# Introduction

<p align="center"><img width="650" src="../images/excelize.svg" alt="Excelize logo"></p>

Excelize est une bibliothèque écrite en pure Go fournissant un ensemble de fonctions qui vous permettent d'écrire et de lire à partir de fichiers XLAM / XLSM / XLSX / XLTM / XLTX. Prend en charge la lecture et l'écriture de feuilles de calcul générées par Microsoft Excel&trade; 2007 et versions ultérieures. Prend en charge les composants complexes par une compatibilité élevée et fournit une API de streaming pour générer ou lire des données à partir d'une feuille de calcul contenant d'énormes quantités de données. Cette bibliothèque a besoin de Go version 1.15 ou ultérieure.

- Code source: [github.com/xuri/excelize](https://github.com/xuri/excelize)
- Problème: [github.com/xuri/excelize/issues](https://github.com/xuri/excelize/issues)
- go.dev: [pkg.go.dev/github.com/xuri/excelize/v2](https://pkg.go.dev/github.com/xuri/excelize/v2)
- Licenses: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- Dernière version: [v2.6.0](https://github.com/xuri/excelize/releases/latest)
- Heure de mise à jour du document: 3 Mai 2022

## Mission du projet

L'objectif d'Excelize est de créer et de gérer une version en langage Go de l'API de document Excel pour gérer les fichiers xlsx conformes à la norme Office Open XML (OOXML). Avec Excelize, vous pouvez utiliser Go pour lire et écrire des fichiers MS Excel.

## Pourquoi utiliser Excelize

Dans certains cas, nous devons manipuler des documents Excel à travers des programmes tels que: ouvrir pour lire du contenu de document Excel existant, créer de nouveaux documents Excel, générer de nouveaux documents Excel basés sur des documents existants (modèles), insérer des images dans des documents Excel en tant que tables et parfois besoin de mettre en œuvre ces opérations sur les plates-formes. Excelize peut facilement répondre à ces besoins.

## Des clients connus

<a href="https://www.360.cn" title="Qihoo 360" target="_blank"><img width="165" src="../images/vendor/360@2x.png" alt="Qihoo 360"></a> <a href="https://www.baidu.com" title="Baidu, Inc." target="_blank"><img width="165" src="../images/vendor/baidu@2x.png" alt="Baidu, Inc."></a> [![INTSIG](../images/vendor/intsig.com_en.png)](https://en.intsig.com) <a href="https://www.inke.cn" title="Inke, Inc." target="_blank"><img width="165" src="../images/vendor/inke@2x.png" alt="Inke, Inc."></a> <a href="https://www.meituan.com" title="Meituan-Dianping" target="_blank"><img width="165" src="../images/vendor/meituan@2x.png" alt="Meituan-Dianping"></a> <a href="https://www.163.com" title="NetEase" target="_blank"><img width="165" src="../images/vendor/netease@2x.png" alt="NetEase"></a> <a href="https://www.bilibili.com" title="Bilibili" target="_blank"><img width="165" src="../images/vendor/bilibili@2x.png" alt="Bilibili"></a> <a href="https://www.qianxin.com" title="Qi An Xin Groupe" target="_blank"><img width="165" src="../images/vendor/qianxin.com_en@2x.png" alt="Qi An Xin Groupe"></a> <a href="https://www.alibabagroup.com" title="Alibaba Group" target="_blank"><img width="165" src="../images/vendor/alibabagroup@2x.png" alt="Alibaba Group"></a> <a href="https://www.ele.me" title="ele.me" target="_blank"><img width="165" src="../images/vendor/ele.me@2x.png" alt="ele.me"></a> <a href="https://www.huifu.com" title="Huifu" target="_blank"><img width="165" src="../images/vendor/huifu.com@2x.png" alt="Huifu"></a> <a href="http://www.dodoca.com" title="Dodoca Information Technology" target="_blank"><img width="165" src="../images/vendor/dodoca.com@2x.png" alt="Dodoca Information Technology"></a> <a href="https://bytedance.com" title="ByteDance" target="_blank"><img width="165" src="../images/vendor/bytedance@2x.png" alt="ByteDance"></a> <a href="https://www.flashexpress.com" title="Flash Express" target="_blank"><img width="165" src="../images/vendor/flashexpress.com@2x.png" alt="Flash Express"></a> <a href="http://www.bigbaser.com" title="Big Baser" target="_blank"><img width="165" src="../images/vendor/bigbaser.com@2x.png" alt="Big Baser"></a> <a href="https://jimengio.com" title="JimengIO" target="_blank"><img width="165" src="../images/vendor/jimengio.com@2x.png" alt="JimengIO"></a> <a href="https://www.shannonai.com" title="Shannon.AI" target="_blank"><img width="165" src="../images/vendor/shannonai.com@2x.png" alt="Shannon.AI"></a> <a href="https://ibm.com" title="IBM" target="_blank"><img width="165" src="../images/vendor/ibm@2x.png" alt="IBM"></a> <a href="https://www.basedig.com" title="Basedig" target="_blank"><img width="165" src="../images/vendor/basedig.com@2x.png" alt="Basedig"></a> <a href="https://www.meitu.com" title="Meitui" target="_blank"><img width="165" src="../images/vendor/meitu.com@2x.png" alt="Meitui"></a> <a href="https://www.amazon.com" title="Amazon" target="_blank"><img width="165" src="../images/vendor/amazon@2x.png" alt="Amazon"></a> <a href="https://www.deloitte.com" title="Deloitte" target="_blank"><img width="165" src="../images/vendor/deloitte@2x.png" alt="Deloitte"></a>

Si votre entreprise ou produit utilise également Excelize, bienvenue <a href="mailto: xuri.me@gmail.com?Subject=Please add our company in Excelize Introduction page&amp;Body=Hello%2C%20this%20is%20%3Cyour%20name%3E%20from%20%3Cyour%20company%20name%3E.%0AWe%20are%20using%20Excelize%20and%20will%20be%20proud%20to%20add%20our%20company%20name%20to%20Excelize%20Introduction%20page.%0APlease%20see%20attachment%20for%20our%20logo.%20%3CBe%20sure%20to%20include%20logo%20in%20attachment%3E%0A" title="envoyer Logo">envoyer Logo</a> à nous.

## Communauté

- [Facebook Group](https://www.facebook.com/groups/excelize)
- [Google Group](https://groups.google.com/g/excelize)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/excelize)
- [Slack Channel](https://join.slack.com/t/xuri/shared_invite/zt-eriqdkeo-wV04zcCdBiiZveFgY86Wzw)
- [Gitter](https://gitter.im/excelize/community)
- [Community on Telegram](https://t.me/excelize)
- [Community on Discord](https://discord.gg/MWV8MBQGtv)
- [Excelize Community on Microsoft Teams](https://teams.live.com/l/invite/FBA8aHkflqEj5SNzQM)
- [Skype Community](https://join.skype.com/YW3OFS5QjYcV?source=qr-ios): <a href="../images/skype_group@2x.png" title="Excelize Skype Community" target="_blank">join via QR Code</a>
- [Line Community](http://line.me/ti/g/NFIjhfbP_g): <a href="../images/line_group@2x.png" title="Excelize Line Community" target="_blank">join via QR Code</a>
- [DingTalk Group ID](https://h5.dingtalk.com/circle/healthCheckin.html?dtaction=os&corpId=dingf7955a3077788503103115db31258e39&ed1be3ec=97369f3c&cbdbhh=qwertyuiop): `30047129` | <a href="../images/dingtalk_group@2x.png" title="Excelize DingTalk Group" target="_blank">join via QR Code</a>
- [QQ Group ID](https://jq.qq.com/?_wv=1027&k=5imdV9h): `207895940` | <a href="../images/qq_group@2x.png" title="Excelize QQ Group ID" target="_blank">join via QR Code</a>
- Excelize WeChat ID: `hixuri` (Verification info: Excelize) | <a href="../images/wechat_group@2x.png" title="Excelize Excelize WeChat Community" target="_blank">join via QR Code</a>
- Inflow Group ID: `4375928` | <a href="../images/inflow_group@2x.png" title="Excelize Inflow Group" target="_blank">join via QR Code</a>

## Parrainer Excelize Development

Si vous êtes un utilisateur individuel et que vous avez apprécié la productivité de l'utilisation d'Excelize, considérez le don comme un signe d'appréciation - comme l'achat de café de temps en temps. Soutenez ce projet en devenant sponsor.

<a href="https://www.paypal.com/paypalme/xuri" title="Faire un don avec Paypal" target="_blank"><img width="170" src="../images/donate@2x.png" alt="Faire un don avec Paypal"></a> <a href="https://opencollective.com/excelize" title="Devenez sponsor" target="_blank"><img height="61" src="../images/opencollective.com@2x.png" alt="Devenez sponsor"></a> <a href="https://www.patreon.com/xuri" title="Soutenir Excelize sur Patreon" target="_blank"><img height="61" src="../images/patreon.com@2x.png" alt="Soutenir Excelize sur Patreon"></a>
