# Introduction

<p align="center"><img width="650" src="../images/excelize.svg" alt="Excelize logo"></p>

Excelize est une bibliothèque écrite en pure Go fournissant un ensemble de fonctions qui vous permettent d'écrire et de lire à partir de fichiers XLAM / XLSM / XLSX / XLTM / XLTX. Prend en charge la lecture et l'écriture de feuilles de calcul générées par Microsoft Excel&trade; 2007 et versions ultérieures. Prend en charge les composants complexes par une compatibilité élevée et fournit une API de streaming pour générer ou lire des données à partir d'une feuille de calcul contenant d'énormes quantités de données. Cette bibliothèque a besoin de Go version 1.23.0 ou ultérieure.

- Code source: [github.com/xuri/excelize](https://github.com/xuri/excelize)
- Problème: [github.com/xuri/excelize/issues](https://github.com/xuri/excelize/issues)
- go.dev: [pkg.go.dev/github.com/xuri/excelize/v2](https://pkg.go.dev/github.com/xuri/excelize/v2)
- Licenses: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- Dernière version: [v2.10.0](https://github.com/xuri/excelize/releases/latest)
- Heure de mise à jour du document: 15 janvier 2026

## Mission du projet

L'objectif d'Excelize est de créer et de gérer une version en langage Go de l'API de document Excel pour gérer les fichiers xlsx conformes à la norme Office Open XML (OOXML). Avec Excelize, vous pouvez utiliser Go pour lire et écrire des fichiers MS Excel.

## Pourquoi utiliser Excelize

Dans certains cas, nous devons manipuler des documents Excel à travers des programmes tels que: ouvrir pour lire du contenu de document Excel existant, créer de nouveaux documents Excel, générer de nouveaux documents Excel basés sur des documents existants (modèles), insérer des images dans des documents Excel en tant que tables et parfois besoin de mettre en œuvre ces opérations sur les plates-formes. Excelize peut facilement répondre à ces besoins.

## Sponsors or

<a href="https://www.gravityclimate.com" alt="Gravity"><img width="165" src="../images/vendor/gravityclimate.com.svg" alt="Gravity"></a>

## Des clients connus

<img width="165" src="../images/vendor/360@2x.png" alt="Qihoo 360"> <img width="165" src="../images/vendor/baidu@2x.png" alt="Baidu, Inc."> ![INTSIG](../images/vendor/intsig.com_en.png) <img width="165" src="../images/vendor/inke@2x.png" alt="Inke, Inc."> <img width="165" src="../images/vendor/meituan@2x.png" alt="Meituan-Dianping"> <img width="165" src="../images/vendor/netease@2x.png" alt="NetEase"> <img width="165" src="../images/vendor/bilibili@2x.png" alt="Bilibili"> <img width="165" src="../images/vendor/qianxin.com_en@2x.png" alt="Qi An Xin Group"> <img width="165" src="../images/vendor/alibabagroup@2x.png" alt="Alibaba Group"> <img width="165" src="../images/vendor/ele.me@2x.png" alt="ele.me"> <img width="165" src="../images/vendor/huifu.com@2x.png" alt="Huifu"> <img width="165" src="../images/vendor/dodoca.com@2x.png" alt="Dodoca Information Technology"> <img width="165" src="../images/vendor/bytedance@2x.png" alt="ByteDance"> <img width="165" src="../images/vendor/flashexpress.com@2x.png" alt="Flash Express"> <img width="165" src="../images/vendor/jimengio.com@2x.png" alt="JimengIO"> <img width="165" src="../images/vendor/shannonai.com@2x.png" alt="Shannon.AI"> <img width="165" src="../images/vendor/ibm@2x.png" alt="IBM"> <img width="165" src="../images/vendor/basedig.com@2x.png" alt="Basedig"> <img width="165" src="../images/vendor/meitu.com@2x.png" alt="Meitui"> <img width="165" src="../images/vendor/amazon@2x.png" alt="Amazon"> <img width="165" src="../images/vendor/deloitte@2x.png" alt="Deloitte"> <img width="165" src="../images/vendor/cisco@2x.png" alt="Cisco"> <img width="165" src="../images/vendor/nl-a.ru@2x.png" alt="Neuro Lab! Algorithms"> <img width="165" src="../images/vendor/58.com@2x.png" alt="58.com"> <img width="165" src="../images/vendor/ke.com@2x.png" alt="ke.com"> <img width="165" src="../images/vendor/microsoft@2x.png" alt="Microsoft"> <img width="165" src="../images/vendor/bytebase.com@2x.png" alt="ByteBase"> <img width="165" src="../images/vendor/intel@2x.png" alt="Intel"> <img width="165" src="../images/vendor/icbc.com.cn@2x.png" alt="Industrial and Commercial Bank of China"> <img width="165" src="../images/vendor/ccb.com@2x.png" alt="China Construction Bank"> <img width="165" src="../images/vendor/chinatelecom@2x.png" alt="China Telecommunications Corporation"> <img width="165" src="../images/vendor/tencent@2x.png" alt="Tencent"> <img width="165" src="../images/vendor/mihoyo@2x.png" alt="miHoYo"> <img width="165" src="../images/vendor/nsfocus@2x.png" alt="NSFOCUS Technologies Group Co Ltd"> <img width="165" src="../images/vendor/gree.com@2x.png" alt="Gree"> <img width="165" src="../images/vendor/jd.com@2x.png" alt="JD.com, Inc."> <img width="165" src="../images/vendor/zhiyitech.cn@2x.png" alt="Hangzhou Zhiyi Technology Co., Ltd.">

Si votre entreprise ou produit utilise également Excelize, bienvenue <a href="mailto: xuri.me@gmail.com?Subject=Veuillez%20ajouter%20notre%20entreprise%20dans%20la%20page%20d'introduction%20d'Excelize&amp;Body=Bonjour%2C%20voici%20%3Cvotre%20nom%3E%20de%20%3Cnom%20de%20votre%20entreprise%3E.%0ANous%20utilisons%20Excelize%20et%20serons%20fiers%20d'ajouter%20le%20nom%20de%20notre%20entreprise%20%C3%A0%20la%20page%20d'introduction%20d'Excelize.
Veuillez%20consulter%20la%20pi%C3%A8ce%20jointe%20pour%20notre%20logo.%20%3CAssurez-vous%20d'inclure%20le%20logo%20dans%20la%20pi%C3%A8ce%20jointe%3E%0A" title="envoyer Logo">envoyer Logo</a> à nous.

## Communauté

- [Facebook Group](https://www.facebook.com/groups/excelize)
- [Google Group](https://groups.google.com/g/excelize)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/excelize)
- [Slack Channel](https://join.slack.com/t/xuri/shared_invite/zt-eriqdkeo-wV04zcCdBiiZveFgY86Wzw)
- [Gitter](https://gitter.im/excelize/community)
- [Community on Telegram](https://t.me/excelize)
- [Community on Discord](https://discord.gg/MWV8MBQGtv)
- [Excelize Community on Microsoft Teams](https://teams.live.com/l/invite/FBA8aHkflqEj5SNzQM)
- [Line Community](http://line.me/ti/g/NFIjhfbP_g): <a href="../images/line_group@2x.png" title="Excelize Line Community" target="_blank">join via QR Code</a>
- [DingTalk Group ID](https://qr.dingtalk.com/action/joingroup?code=v1,k1,6tmzbBbJuQkGezVdHJjsHz29CZI9F49xeW+cvOaECtk=&_dt_no_comment=1&origin=11): `30047129` | <a href="../images/dingtalk_group@2x.png" title="Excelize DingTalk Group" target="_blank">join via QR Code</a>
- QQ Group ID: `1302058237` (Verification info: Excelize) | <a href="../images/qq_group@2x.png" title="Excelize QQ Group ID" target="_blank">join via QR Code</a>
- Excelize WeChat ID: `hixuri` (Verification info: Excelize) | <a href="../images/wechat_group@2x.png" title="Excelize WeChat Community" target="_blank">join via QR Code</a>
- WeCom Group (Verification info: Excelize): <a href="../images/wecom_group@2x.png" title="Excelize WeCom Group" target="_blank">join via QR Code</a>
- Inflow Group ID: `4375928` | <a href="../images/inflow_group@2x.png" title="Excelize Inflow Group" target="_blank">join via QR Code</a>

## Parrainer Excelize Development

Si vous êtes un utilisateur individuel et que vous avez apprécié la productivité de l'utilisation d'Excelize, considérez le don comme un signe d'appréciation - comme l'achat de café de temps en temps. Soutenez ce projet en devenant sponsor.

<a href="https://github.com/sponsors/xuri" title="GitHub Sponsor" target="_blank"><img width="170" src="../images/github_sponsor@2x.png" alt="GitHub Sponsor"></a> <a href="https://www.paypal.com/paypalme/xuri" title="Faire un don avec Paypal" target="_blank"><img width="170" src="../images/donate@2x.png" alt="Faire un don avec Paypal"></a> <a href="https://opencollective.com/excelize" title="Devenez sponsor" target="_blank"><img height="61" src="../images/opencollective.com@2x.png" alt="Devenez sponsor"></a> <a href="https://www.patreon.com/xuri" title="Soutenir Excelize sur Patreon" target="_blank"><img height="61" src="../images/patreon.com@2x.png" alt="Soutenir Excelize sur Patreon"></a>
