# Introduzione

<p align="center"><img width="650" src="../images/excelize.svg" alt="Logo Excelize"></p>

Excelize è una libreria scritta in puro Go che fornisce una serie di funzioni che consentono di scrivere e leggere da file XLAM / XLSM / XLSX / XLTM / XLTX. Supporta la lettura e la scrittura di documenti di fogli di calcolo generati da Microsoft Excel™ 2007 e versioni successive. Supporta componenti complessi grazie all'elevata compatibilità e fornisce API di streaming per generare o leggere dati da un foglio di lavoro con enormi quantità di dati. Questa libreria richiede Go versione 1.18 o successiva.

- Codice sorgente: [github.com/xuri/excelize](https://github.com/xuri/excelize)
- Problema: [github.com/xuri/excelize/issues](https://github.com/xuri/excelize/issues)
- go.dev: [pkg.go.dev/github.com/xuri/excelize/v2](https://pkg.go.dev/github.com/xuri/excelize/v2)
- Licenze: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- Ultima versione: [v2.9.0](https://github.com/xuri/excelize/releases/latest)
- Orario aggiornamento documento: ottobre 15, 2024

## Missione del progetto

L'obiettivo di Excelize è creare e mantenere una versione in linguaggio Go dell'API dei documenti di Excel per gestire file xlsx conformi allo standard Office Open XML (OOXML). Con Excelize puoi utilizzare Go per leggere e scrivere file MS Excel.

## Perché utilizzare Excelize

In alcuni casi, dobbiamo manipolare i documenti Excel attraverso programmi, come: aprire per leggere il contenuto del documento Excel esistente, creare nuovi documenti Excel, generare nuovi documenti Excel basati su documenti esistenti (modelli), inserire immagini in documenti Excel, grafici Elementi come come tabelle e talvolta è necessario implementare queste operazioni su più piattaforme. Excelize può facilmente soddisfare queste esigenze.

## Clienti famosi

<a href="https://www.360.cn" title="Qihoo 360" target="_blank"><img width="165" src="../images/vendor/360@2x.png" alt="Qihoo 360"></a> <a href="https://www.baidu.com" title="Baidu, Inc." target="_blank"><img width="165" src="../images/vendor/baidu@2x.png" alt="Baidu, Inc."></a> [![INTSIG](../images/vendor/intsig.com_en.png)](https://en.intsig.com) <a href="https://www.inke.cn" title="Inke, Inc." target="_blank"><img width="165" src="../images/vendor/inke@2x.png" alt="Inke, Inc."></a> <a href="https://www.meituan.com" title="Meituan-Dianping" target="_blank"><img width="165" src="../images/vendor/meituan@2x.png" alt="Meituan-Dianping"></a> <a href="https://www.163.com" title="NetEase" target="_blank"><img width="165" src="../images/vendor/netease@2x.png" alt="NetEase"></a> <a href="https://www.bilibili.com" title="Bilibili" target="_blank"><img width="165" src="../images/vendor/bilibili@2x.png" alt="Bilibili"></a> <a href="https://www.qianxin.com" title="Qi An Xin Group" target="_blank"><img width="165" src="../images/vendor/qianxin.com_en@2x.png" alt="Qi An Xin Group"></a> <a href="https://www.alibabagroup.com" title="Alibaba Group" target="_blank"><img width="165" src="../images/vendor/alibabagroup@2x.png" alt="Alibaba Group"></a> <a href="https://www.ele.me" title="ele.me" target="_blank"><img width="165" src="../images/vendor/ele.me@2x.png" alt="ele.me"></a> <a href="https://www.huifu.com" title="Huifu" target="_blank"><img width="165" src="../images/vendor/huifu.com@2x.png" alt="Huifu"></a> <a href="http://www.dodoca.com" title="Dodoca Information Technology" target="_blank"><img width="165" src="../images/vendor/dodoca.com@2x.png" alt="Dodoca Information Technology"></a> <a href="https://bytedance.com" title="ByteDance" target="_blank"><img width="165" src="../images/vendor/bytedance@2x.png" alt="ByteDance"></a> <a href="https://www.flashexpress.com" title="Flash Express" target="_blank"><img width="165" src="../images/vendor/flashexpress.com@2x.png" alt="Flash Express"></a> <a href="https://jimengio.com" title="JimengIO" target="_blank"><img width="165" src="../images/vendor/jimengio.com@2x.png" alt="JimengIO"></a> <a href="https://www.shannonai.com" title="Shannon.AI" target="_blank"><img width="165" src="../images/vendor/shannonai.com@2x.png" alt="Shannon.AI"></a> <a href="https://ibm.com" title="IBM" target="_blank"><img width="165" src="../images/vendor/ibm@2x.png" alt="IBM"></a> <a href="https://www.basedig.com" title="Basedig" target="_blank"><img width="165" src="../images/vendor/basedig.com@2x.png" alt="Basedig"></a> <a href="https://www.meitu.com" title="Meitui" target="_blank"><img width="165" src="../images/vendor/meitu.com@2x.png" alt="Meitui"></a> <a href="https://www.amazon.com" title="Amazon" target="_blank"><img width="165" src="../images/vendor/amazon@2x.png" alt="Amazon"></a> <a href="https://www.deloitte.com" title="Deloitte" target="_blank"><img width="165" src="../images/vendor/deloitte@2x.png" alt="Deloitte"></a> <a href="https://nl-a.ru" title="Neuro Lab! Algorithms" target="_blank"><img width="165" src="../images/vendor/nl-a.ru@2x.png" alt="Neuro Lab! Algorithms"></a> <a href="https://58.com" title="58.com" target="_blank"><img width="165" src="../images/vendor/58.com@2x.png" alt="58.com"></a> <a href="https://ke.com" title="ke.com" target="_blank"><img width="165" src="../images/vendor/ke.com@2x.png" alt="ke.com"></a> <a href="https://www.microsoft.com" title="Microsoft" target="_blank"><img width="165" src="../images/vendor/microsoft@2x.png" alt="Microsoft"></a> <a href="https://www.bytebase.com" title="ByteBase" target="_blank"><img width="165" src="../images/vendor/bytebase.com@2x.png" alt="ByteBase"></a> <a href="https://www.intel.com" title="Intel" target="_blank"><img width="165" src="../images/vendor/intel@2x.png" alt="Intel"></a> <a href="https://www.tencent.com" title="Tencent" target="_blank"><img width="165" src="../images/vendor/tencent@2x.png" alt="Tencent"></a> <a href="https://www.mihoyo.com" title="miHoYo" target="_blank"><img width="165" src="../images/vendor/mihoyo@2x.png" alt="miHoYo"></a> <a href="http://www.nsfocus.com.cn" title="NSFOCUS Technologies Group Co Ltd" target="_blank"><img width="165" src="../images/vendor/nsfocus@2x.png" alt="NSFOCUS Technologies Group Co Ltd"></a>

Se anche la tua azienda o il tuo prodotto utilizza Excelize, <a href="mailto: xuri.me@gmail.com?Subject=Si prega di aggiungere la nostra azienda nella pagina di introduzione di Excelize&amp;Body=Salve%2C%20sono%20%3Cil%20tuo%20nome%3E%20di%20%3Cnome%20della%20tua%20azienda%3E.
Stiamo%20utilizzando%20Excelize%20e%20saremo%20orgogliosi%20di%20aggiungere%20il%20nome%20della%20nostra%20azienda%20alla%20pagina%20Introduzione%20di%20Excelize.
Si%20prega%20di%20consultare%20l'allegato%20per%20il%20nostro%20logo.%20%3CAssicuratevi%20di%20includere%20il%20logo%20nell'allegato%3E%0A" title="send Logo via E-mail">inviaci il logo</a>.

## Comunità

- [Gruppo Facebook](https://www.facebook.com/groups/excelize)
- [Gruppo Google](https://groups.google.com/g/excelize)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/excelize)
- [Slack Canale](https://join.slack.com/t/xuri/shared_invite/zt-eriqdkeo-wV04zcCdBiiZveFgY86Wzw)
- [Gitter](https://gitter.im/excelize/community)
- [Comunità su Telegram](https://t.me/excelize)
- [Comunità su Discord](https://discord.gg/MWV8MBQGtv)
- [Excelize Comunità su Microsoft Teams](https://teams.live.com/l/invite/FBA8aHkflqEj5SNzQM)
- [Comunità Skype](https://join.skype.com/YW3OFS5QjYcV?source=qr-ios): <a href="../images/skype_group@2x.png" alt="Excelize la comunità Skype" target="_blank" target="_blank">partecipare tramite codice QR</a>
- [Comunità di Line](http://line.me/ti/g/NFIjhfbP_g): <a href="../images/line_group@2x.png" alt="Comunità Excelize Line" target="_blank" target="_blank">partecipare tramite codice QR</a>
- [ID gruppo DingTalk](https://qr.dingtalk.com/action/joingroup?code=v1,k1,6tmzbBbJuQkGezVdHJjsHz29CZI9F49xeW+cvOaECtk=&_dt_no_comment=1&origin=11): `30047129` | <a href="../images/dingtalk_group@2x.png" alt="Excelize il gruppo DingTalk" target="_blank" target="_blank">partecipare tramite codice QR</a>
- ID gruppo QQ: `1302058237` (Verification info: Excelize) | <a href="../images/qq_group@2x.png" alt="Excelize l'ID del gruppo QQ" target="_blank" target="_blank">partecipare tramite codice QR</a>
- Excelize l'ID WeChat: `hixuri` (Informazioni sulla verifica: Excelize) | <a href="../images/wechat_group@2x.png" alt="Eccelle la comunità WeChat" target="_blank" target="_blank">partecipare tramite codice QR</a>
- Gruppo WeCom (Informazioni sulla verifica: Excelize): <a href="../images/wecom_group@2x.png" title="Excelize WeCom Group" target="_blank">partecipare tramite codice QR</a>
- ID gruppo InFlow: `4375928` | <a href="../images/inflow_group@2x.png" alt="Gruppo di afflusso Excelize" target="_blank" target="_blank">partecipare tramite codice QR</a>

## Sponsorizza lo sviluppo di Excelize

Se sei un utente individuale e hai apprezzato la produttività dell'utilizzo di Excelize, considera la donazione come un segno di apprezzamento, ad esempio comprandomi un caffè di tanto in tanto, oppure sostieni questo progetto diventando uno sponsor.

<a href="https://github.com/sponsors/xuri" title="Sponsor di GitHub" target="_blank"><img width="170" src="../images/github_sponsor@2x.png" alt="Sponsor di GitHub"></a> <a href="https://www.paypal.com/paypalme/xuri" title="Dona con Paypal" target="_blank"><img width="170" src="../images/donate@2x.png" alt="Dona con Paypal"></a> <a href="https://opencollective.com/excelize" title="Diventa uno sponsor" target="_blank"><img height="61" src="../images/opencollective.com@2x.png" alt="Diventa uno sponsor"></a> <a href="https://www.patreon.com/xuri" title="Supporta Excelize su Patreon" target="_blank"><img height="61" src="../images/patreon.com@2x.png" alt="Supporta Excelize su Patreon"></a>
