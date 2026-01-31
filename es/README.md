# Introducción

<p align="center"><img width="650" src="../images/excelize.svg" alt="Excelize logo"></p>

Excelize es una biblioteca escrita en Go puro que proporciona un conjunto de funciones que le permiten escribir y leer desde archivos XLAM / XLSM / XLSX / XLTM / XLTX. Admite la lectura y escritura de documentos de hoja de cálculo generados por Microsoft Excel&trade; 2007 y versiones posteriores. Admite componentes complejos por alta compatibilidad y proporciona API de streaming para generar o leer datos de una hoja de trabajo con grandes cantidades de datos. Esta biblioteca necesita Go versión 1.23.0 o posterior.

- Código fuente: [github.com/xuri/excelize](https://github.com/xuri/excelize)
- Problema: [github.com/xuri/excelize/issues](https://github.com/xuri/excelize/issues)
- go.dev: [pkg.go.dev/github.com/xuri/excelize/v2](https://pkg.go.dev/github.com/xuri/excelize/v2)
- Licencias: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- Ultima versión: [v2.10.0](https://github.com/xuri/excelize/releases/latest)
- Tiempo de actualización del documento: enero 31, 2026

## Misión del proyecto

El objetivo de Excelize es crear y mantener una versión de lenguaje Go de la API de documentos de Excel para controlar los archivos xlsx que se ajustan al estándar Office Open XML (OOXML). Con Excelize puede usar Ir para leer y escribir archivos de MS Excel.

## Por qué usar Excelize

En algunos casos, necesitamos manipular documentos de Excel a través de programas, como: abrir para leer el contenido de documentos de Excel existente, crear nuevos documentos de Excel, generar nuevos documentos de Excel basados en documentos existentes (plantillas), insertar imágenes en documentos de Excel, gráficos Elementos como tablas y a veces necesitan implementar estas operaciones en plataformas. Excelize puede satisfacer fácilmente estas necesidades.

## Patrocinadores de oro

<a href="https://www.gravityclimate.com" alt="Gravity"><img width="165" src="../images/vendor/gravityclimate.com.svg" alt="Gravity"></a>

## Clientes conocidos

<img width="165" src="../images/vendor/360@2x.png" alt="Qihoo 360"> <img width="165" src="../images/vendor/baidu@2x.png" alt="Baidu, Inc."> ![INTSIG](../images/vendor/intsig.com_en.png) <img width="165" src="../images/vendor/inke@2x.png" alt="Inke, Inc."> <img width="165" src="../images/vendor/meituan@2x.png" alt="Meituan-Dianping"> <img width="165" src="../images/vendor/netease@2x.png" alt="NetEase"> <img width="165" src="../images/vendor/bilibili@2x.png" alt="Bilibili"> <img width="165" src="../images/vendor/qianxin.com_en@2x.png" alt="Qi An Xin Group"> <img width="165" src="../images/vendor/alibabagroup@2x.png" alt="Alibaba Group"> <img width="165" src="../images/vendor/ele.me@2x.png" alt="ele.me"> <img width="165" src="../images/vendor/huifu.com@2x.png" alt="Huifu"> <img width="165" src="../images/vendor/dodoca.com@2x.png" alt="Dodoca Information Technology"> <img width="165" src="../images/vendor/bytedance@2x.png" alt="ByteDance"> <img width="165" src="../images/vendor/flashexpress.com@2x.png" alt="Flash Express"> <img width="165" src="../images/vendor/jimengio.com@2x.png" alt="JimengIO"> <img width="165" src="../images/vendor/shannonai.com@2x.png" alt="Shannon.AI"> <img width="165" src="../images/vendor/ibm@2x.png" alt="IBM"> <img width="165" src="../images/vendor/basedig.com@2x.png" alt="Basedig"> <img width="165" src="../images/vendor/meitu.com@2x.png" alt="Meitui"> <img width="165" src="../images/vendor/amazon@2x.png" alt="Amazon"> <img width="165" src="../images/vendor/deloitte@2x.png" alt="Deloitte"> <img width="165" src="../images/vendor/cisco@2x.png" alt="Cisco"> <img width="165" src="../images/vendor/nl-a.ru@2x.png" alt="Neuro Lab! Algorithms"> <img width="165" src="../images/vendor/58.com@2x.png" alt="58.com"> <img width="165" src="../images/vendor/ke.com@2x.png" alt="ke.com"> <img width="165" src="../images/vendor/microsoft@2x.png" alt="Microsoft"> <img width="165" src="../images/vendor/bytebase.com@2x.png" alt="ByteBase"> <img width="165" src="../images/vendor/intel@2x.png" alt="Intel"> <img width="165" src="../images/vendor/icbc.com.cn@2x.png" alt="Industrial and Commercial Bank of China"> <img width="165" src="../images/vendor/ccb.com@2x.png" alt="China Construction Bank"> <img width="165" src="../images/vendor/chinatelecom@2x.png" alt="China Telecommunications Corporation"> <img width="165" src="../images/vendor/tencent@2x.png" alt="Tencent"> <img width="165" src="../images/vendor/mihoyo@2x.png" alt="miHoYo"> <img width="165" src="../images/vendor/nsfocus@2x.png" alt="NSFOCUS Technologies Group Co Ltd"> <img width="165" src="../images/vendor/gree.com@2x.png" alt="Gree"> <img width="165" src="../images/vendor/jd.com@2x.png" alt="JD.com, Inc."> <img width="165" src="../images/vendor/zhiyitech.cn@2x.png" alt="Hangzhou Zhiyi Technology Co., Ltd.">

Si su empresa o producto también está utilizando Excelize, dé la bienvenida a <a href="mailto: xuri.me@gmail.com?Subject=Agregue%20nuestra%20empresa%20en%20la%20p%C3%A1gina%20de%20introducci%C3%B3n%20de%20Excelize&amp;Body=Hola%2C%20soy%20%3Ctu%20nombre%3E%20de%20%3Cnombre%20de%20tu%20empresa%3E.%0AEstamos%20utilizando%20Excelize%20y%20estaremos%20orgullosos%20de%20agregar%20el%20nombre%20de%20nuestra%20empresa%20a%20la%20p%C3%A1gina%20de%20introducci%C3%B3n%20de%20Excelize.
Consulte%20el%20archivo%20adjunto%20para%20ver%20nuestro%20logotipo.%20%3CAseg%C3%BArese%20de%20incluir%20el%20logotipo%20en%20el%20archivo%20adjunto%3E%0A" title="send Logo via E-mail">enviar logotipo</a> a nosotros.

## Comunidad

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

## Patrocinador Excelize Development

Si usted es un usuario individual y ha disfrutado de la productividad de usar Excelize, considere donar como una señal de agradecimiento - como comprarme café de vez en cuando. Apoya este proyecto convirtiéndote en patrocinador.

<a href="https://github.com/sponsors/xuri" title="GitHub Sponsor" target="_blank"><img width="170" src="../images/github_sponsor@2x.png" alt="GitHub Sponsor"></a> <a href="https://www.paypal.com/paypalme/xuri" title="Donar con PayPal" target="_blank"><img width="170" src="../images/donate@2x.png" alt="Donar con PayPal"></a> <a href="https://opencollective.com/excelize" title="conviértete en patrocinador" target="_blank"><img height="61" src="../images/opencollective.com@2x.png" alt="conviértete en patrocinador"></a> <a href="https://www.patreon.com/xuri" title="Soporte Excelize en Patreon" target="_blank"><img height="61" src="../images/patreon.com@2x.png" alt="Soporte Excelize en Patreon"></a>
