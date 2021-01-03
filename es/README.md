# Introducción

<p align="center"><img width="650" src="../images/excelize.svg" alt="Excelize logo"></p>

Excelize es una biblioteca escrita en Go puro que proporciona un conjunto de funciones que le permiten escribir y leer desde archivos XLSX / XLSM / XLTM. Admite la lectura y escritura de documentos de hoja de cálculo generados por Microsoft Excel&trade; 2007 y versiones posteriores. Admite componentes complejos por alta compatibilidad y proporciona API de streaming para generar o leer datos de una hoja de trabajo con grandes cantidades de datos. Esta biblioteca necesita Go versión 1.10 o posterior.

- Código fuente: [github.com/360EntSecGroup-Skylar/excelize](https://github.com/360EntSecGroup-Skylar/excelize)
- Problema: [github.com/360EntSecGroup-Skylar/excelize/issues](https://github.com/360EntSecGroup-Skylar/excelize/issues)
- go.dev: [pkg.go.dev/github.com/360EntSecGroup-Skylar/excelize/v2?tab=doc](https://pkg.go.dev/github.com/360EntSecGroup-Skylar/excelize/v2?tab=doc)
- Licencias: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- Ultima versión: [v2.3.2](https://github.com/360EntSecGroup-Skylar/excelize/releases/latest)
- Tiempo de actualización del documento: enero 4, 2021

## Misión del proyecto

El objetivo de Excelize es crear y mantener una versión de lenguaje Go de la API de documentos de Excel para controlar los archivos xlsx que se ajustan al estándar Office Open XML (OOXML). Con Excelize puede usar Ir para leer y escribir archivos de MS Excel.

## Por qué usar Excelize

En algunos casos, necesitamos manipular documentos de Excel a través de programas, como: abrir para leer el contenido de documentos de Excel existente, crear nuevos documentos de Excel, generar nuevos documentos de Excel basados en documentos existentes (plantillas), insertar imágenes en documentos de Excel, gráficos Elementos como tablas y a veces necesitan implementar estas operaciones en plataformas. Excelize puede satisfacer fácilmente estas necesidades.

## Clientes conocidos

<a href="https://www.360.cn" title="Qihoo 360" target="_blank"><img width="165" src="../images/vendor/360@2x.png" alt="Qihoo 360"></a> <a href="https://www.baidu.com" title="Baidu, Inc." target="_blank"><img width="165" src="../images/vendor/baidu@2x.png" alt="Baidu, Inc."></a> [![INTSIG](../images/vendor/intsig.com_en.png)](https://en.intsig.com) <a href="https://www.inke.cn" title="Inke, Inc." target="_blank"><img width="165" src="../images/vendor/inke@2x.png" alt="Inke, Inc."></a> <a href="https://www.meituan.com" title="Meituan-Dianping" target="_blank"><img width="165" src="../images/vendor/meituan@2x.png" alt="Meituan-Dianping"></a> <a href="https://www.163.com" title="NetEase" target="_blank"><img width="165" src="../images/vendor/netease@2x.png" alt="NetEase"></a> <a href="https://www.bilibili.com" title="Bilibili" target="_blank"><img width="165" src="../images/vendor/bilibili@2x.png" alt="Bilibili"></a> <a href="https://www.qianxin.com" title="Qi An Xin Group" target="_blank"><img width="165" src="../images/vendor/qianxin.com_en@2x.png" alt="Qi An Xin Group"></a> <a href="https://www.alibabagroup.com" title="Alibaba Group" target="_blank"><img width="165" src="../images/vendor/alibabagroup@2x.png" alt="Alibaba Group"></a> <a href="https://www.ele.me" title="ele.me" target="_blank"><img width="165" src="../images/vendor/ele.me@2x.png" alt="ele.me"></a> <a href="https://www.huifu.com" title="Huifu" target="_blank"><img width="165" src="../images/vendor/huifu.com@2x.png" alt="Huifu"></a> <a href="https://www.dodoca.com" title="Dodoca Information Technology" target="_blank"><img width="165" src="../images/vendor/dodoca.com@2x.png" alt="Dodoca Information Technology"></a> <a href="https://bytedance.com" title="ByteDance" target="_blank"><img width="165" src="../images/vendor/bytedance@2x.png" alt="ByteDance"></a> <a href="https://www.flashexpress.com" title="Flash Express" target="_blank"><img width="165" src="../images/vendor/flashexpress.com@2x.png" alt="Flash Express"></a> <a href="http://www.bigbaser.com" title="Big Baser" target="_blank"><img width="165" src="../images/vendor/bigbaser.com@2x.png" alt="Big Baser"></a> <a href="https://jimengio.com" title="JimengIO" target="_blank"><img width="165" src="../images/vendor/jimengio.com@2x.png" alt="JimengIO"></a> <a href="https://www.shannonai.com" title="Shannon.AI" target="_blank"><img width="165" src="../images/vendor/shannonai.com@2x.png" alt="Shannon.AI"></a> <a href="https://ibm.com" title="IBM" target="_blank"><img width="165" src="../images/vendor/ibm@2x.png" alt="IBM"></a> <a href="https://www.basedig.com" title="Basedig" target="_blank"><img width="165" src="../images/vendor/basedig.com@2x.png" alt="Basedig"></a>

Si su empresa o producto también está utilizando Excelize, dé la bienvenida a <a href="mailto: xuri.me@gmail.com?Subject=Please add our company in Excelize Introduction page&amp;Body=Hello%2C%20this%20is%20%3Cyour%20name%3E%20from%20%3Cyour%20company%20name%3E.%0AWe%20are%20using%20Excelize%20and%20will%20be%20proud%20to%20add%20our%20company%20name%20to%20Excelize%20Introduction%20page.%0APlease%20see%20attachment%20for%20our%20logo.%20%3CBe%20sure%20to%20include%20logo%20in%20attachment%3E%0A" title="send Logo via E-mail">enviar logotipo</a> a nosotros.

<a href="https://join.slack.com/t/xuri/shared_invite/zt-eriqdkeo-wV04zcCdBiiZveFgY86Wzw" title="Excelize Slack Channel" target="_blank"><img style="margin-top: 25px;" height="60" src="../images/slack.svg" alt="Excelize Slack Channel"></a> <a href="https://t.me/excelize" title="Excelize Community on Telegram" target="_blank"><img style="margin: 25px 0 0 25px;" height="60" src="../images/telegram.svg" alt="Excelize Community on Telegram"></a> <a href="https://discord.gg/MWV8MBQGtv" title="Excelize Community on Discord" target="_blank"><img style="margin: 25px 0 0 25px;" height="60" src="../images/discord.svg" alt="Excelize Community on Discord"></a>

## Patrocinador Excelize Development

Si usted es un usuario individual y ha disfrutado de la productividad de usar Excelize, considere donar como una señal de agradecimiento - como comprarme café de vez en cuando. Apoya este proyecto convirtiéndote en patrocinador.

<a href="https://www.paypal.com/paypalme/xuri" title="Donar con PayPal" target="_blank"><img width="170" src="../images/donate@2x.png" alt="Donar con PayPal"></a> <a href="https://opencollective.com/excelize" title="conviértete en patrocinador" target="_blank"><img height="61" src="../images/opencollective.com@2x.png" alt="conviértete en patrocinador"></a> <a href="https://www.patreon.com/xuri" title="Soporte Excelize en Patreon" target="_blank"><img height="61" src="../images/patreon.com@2x.png" alt="Soporte Excelize en Patreon"></a>
