# Introduction

<p align="center"><img width="650" src="../images/excelize.svg" alt="Excelize logo"></p>

Excelize est une bibliothèque écrite en pure Go fournissant un ensemble de fonctions qui vous permettent d'écrire et de lire à partir de fichiers XLSX / XLSM / XLTM. Prend en charge la lecture et l'écriture de feuilles de calcul générées par Microsoft Excel&trade; 2007 et versions ultérieures. Prend en charge les composants complexes par une compatibilité élevée et fournit une API de streaming pour générer ou lire des données à partir d'une feuille de calcul contenant d'énormes quantités de données. Cette bibliothèque a besoin de Go version 1.10 ou ultérieure.

- Code source: [github.com/360EntSecGroup-Skylar/excelize](https://github.com/360EntSecGroup-Skylar/excelize)
- Problème: [github.com/360EntSecGroup-Skylar/excelize/issues](https://github.com/360EntSecGroup-Skylar/excelize/issues)
- go.dev: [pkg.go.dev/github.com/360EntSecGroup-Skylar/excelize/v2?tab=doc](https://pkg.go.dev/github.com/360EntSecGroup-Skylar/excelize/v2?tab=doc)
- Licenses: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- Dernière version: [v2.2.0](https://github.com/360EntSecGroup-Skylar/excelize/releases/latest)
- Heure de mise à jour du document: 26 Juin 2020

## Mission du projet

L'objectif d'Excelize est de créer et de gérer une version en langage Go de l'API de document Excel pour gérer les fichiers xlsx conformes à la norme Office Open XML (OOXML). Avec Excelize, vous pouvez utiliser Go pour lire et écrire des fichiers MS Excel.

## Pourquoi utiliser Excelize

Dans certains cas, nous devons manipuler des documents Excel à travers des programmes tels que: ouvrir pour lire du contenu de document Excel existant, créer de nouveaux documents Excel, générer de nouveaux documents Excel basés sur des documents existants (modèles), insérer des images dans des documents Excel en tant que tables et parfois besoin de mettre en œuvre ces opérations sur les plates-formes. Excelize peut facilement répondre à ces besoins.

## Des clients connus

<a href="https://www.360.cn" title="Qihoo 360" target="_blank"><img width="165" src="../images/vendor/360@2x.png" alt="Qihoo 360"></a> <a href="https://www.baidu.com" title="Baidu, Inc." target="_blank"><img width="165" src="../images/vendor/baidu@2x.png" alt="Baidu, Inc."></a> [![CCi. Inc.](../images/vendor/ccint.com.png)](https://www.ccint.com) <a href="https://www.inke.cn" title="Inke, Inc." target="_blank"><img width="165" src="../images/vendor/inke@2x.png" alt="Inke, Inc."></a> <a href="https://www.meituan.com" title="Meituan-Dianping" target="_blank"><img width="165" src="../images/vendor/meituan@2x.png" alt="Meituan-Dianping"></a> <a href="https://www.163.com" title="NetEase" target="_blank"><img width="165" src="../images/vendor/netease@2x.png" alt="NetEase"></a> <a href="https://www.bilibili.com" title="Bilibili" target="_blank"><img width="165" src="../images/vendor/bilibili@2x.png" alt="Bilibili"></a> <a href="https://www.qianxin.com" title="Qi An Xin Groupe" target="_blank"><img width="165" src="../images/vendor/qianxin.com_en@2x.png" alt="Qi An Xin Groupe"></a> <a href="https://www.alibabagroup.com" title="Alibaba Group" target="_blank"><img width="165" src="../images/vendor/alibabagroup@2x.png" alt="Alibaba Group"></a> <a href="https://www.ele.me" title="ele.me" target="_blank"><img width="165" src="../images/vendor/ele.me@2x.png" alt="ele.me"></a> <a href="https://www.huifu.com" title="Huifu" target="_blank"><img width="165" src="../images/vendor/huifu.com@2x.png" alt="Huifu"></a> <a href="https://www.dodoca.com" title="Dodoca Information Technology" target="_blank"><img width="165" src="../images/vendor/dodoca.com@2x.png" alt="Dodoca Information Technology"></a> <a href="https://bytedance.com" title="ByteDance" target="_blank"><img width="165" src="../images/vendor/bytedance@2x.png" alt="ByteDance"></a> <a href="https://www.flashexpress.com" title="Flash Express" target="_blank"><img width="165" src="../images/vendor/flashexpress.com@2x.png" alt="Flash Express"></a> <a href="http://www.bigbaser.com" title="Big Baser" target="_blank"><img width="165" src="../images/vendor/bigbaser.com@2x.png" alt="Big Baser"></a> <a href="https://jimengio.com" title="JimengIO" target="_blank"><img width="165" src="../images/vendor/jimengio.com@2x.png" alt="JimengIO"></a>

Si votre entreprise ou produit utilise également Excelize, bienvenue <a href="mailto: xuri.me@gmail.com?Subject=Please add our company in Excelize Introduction page&amp;Body=Hello%2C%20this%20is%20%3Cyour%20name%3E%20from%20%3Cyour%20company%20name%3E.%0AWe%20are%20using%20Excelize%20and%20will%20be%20proud%20to%20add%20our%20company%20name%20to%20Excelize%20Introduction%20page.%0APlease%20see%20attachment%20for%20our%20logo.%20%3CBe%20sure%20to%20include%20logo%20in%20attachment%3E%0A" title="envoyer Logo">envoyer Logo</a> à nous.

<a href="https://join.slack.com/t/xuri/shared_invite/zt-eriqdkeo-wV04zcCdBiiZveFgY86Wzw" title="Excelize Slack Channel" target="_blank"><img style="margin-top: 25px;" height="60" src="../images/slack.svg" alt="Excelize Slack Channel"></a>

## Parrainer Excelize Development

Si vous êtes un utilisateur individuel et que vous avez apprécié la productivité de l'utilisation d'Excelize, considérez le don comme un signe d'appréciation - comme l'achat de café de temps en temps.

<a href="https://www.paypal.me/xuri" title="Faire un don avec Paypal" target="_blank"><img width="170" src="../images/donate@2x.png" alt="Faire un don avec Paypal"></a>
