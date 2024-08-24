# Introdução

<p align="center"><img width="650" src="../images/excelize.svg" alt="Logotipo da Excelize"></p>

Excelize é uma biblioteca escrita em Go puro que fornece um conjunto de funções que permitem escrever e ler arquivos XLAM / XLSM / XLSX / XLTM / XLTX. Suporta leitura e gravação de documentos de planilhas gerados pelo Microsoft Excel&trade; 2007 e posterior. Suporta componentes complexos por alta compatibilidade e fornece API de streaming para gerar ou ler dados de uma planilha com grandes quantidades de dados. Esta biblioteca precisa do Go versão 1.18 ou posterior.

- Código-fonte: [github.com/xuri/excelize](https://github.com/xuri/excelize)
- Emitir: [github.com/xuri/excelize/issues](https://github.com/xuri/excelize/issues)
- go.dev: [pkg.go.dev/github.com/xuri/excelize/v2](https://pkg.go.dev/github.com/xuri/excelize/v2)
- Licenças: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- Última versão: [v2.8.1](https://github.com/xuri/excelize/releases/latest)
- Hora de atualização do documento: agosto 24, 2024

## Missão do projeto

O objetivo do Excelize é criar e manter uma versão em linguagem Go da API de documentos do Excel para lidar com arquivos xlsx que estejam em conformidade com o padrão Office Open XML (OOXML). Com o Excelize você pode usar Go para ler e gravar arquivos do MS Excel.

## Por que usar o Excelize

Em alguns casos, precisamos manipular documentos Excel por meio de programas, como: abrir para ler o conteúdo existente de documentos Excel, criar novos documentos Excel, gerar novos documentos Excel com base em documentos existentes (modelos), inserir imagens em documentos Excel, gráficos Elementos como como tabelas e às vezes precisam implementar essas operações entre plataformas. O Excelize pode facilmente atender a essas necessidades.

## Clientes conhecidos

<a href="https://www.360.cn" title="Qihoo 360" target="_blank"><img width="165" src="../images/vendor/360@2x.png" alt="Qihoo 360"></a> <a href="https://www.baidu.com" title="Baidu, Inc." target="_blank"><img width="165" src="../images/vendor/baidu@2x.png" alt="Baidu, Inc."></a> [![INTSIG](../images/vendor/intsig.com_en.png)](https://en.intsig.com) <a href="https://www.inke.cn" title="Inke, Inc." target="_blank"><img width="165" src="../images/vendor/inke@2x.png" alt="Inke, Inc."></a> <a href="https://www.meituan.com" title="Meituan-Dianping" target="_blank"><img width="165" src="../images/vendor/meituan@2x.png" alt="Meituan-Dianping"></a> <a href="https://www.163.com" title="NetEase" target="_blank"><img width="165" src="../images/vendor/netease@2x.png" alt="NetEase"></a> <a href="https://www.bilibili.com" title="Bilibili" target="_blank"><img width="165" src="../images/vendor/bilibili@2x.png" alt="Bilibili"></a> <a href="https://www.qianxin.com" title="Qi An Xin Group" target="_blank"><img width="165" src="../images/vendor/qianxin.com_en@2x.png" alt="Qi An Xin Group"></a> <a href="https://www.alibabagroup.com" title="Alibaba Group" target="_blank"><img width="165" src="../images/vendor/alibabagroup@2x.png" alt="Alibaba Group"></a> <a href="https://www.ele.me" title="ele.me" target="_blank"><img width="165" src="../images/vendor/ele.me@2x.png" alt="ele.me"></a> <a href="https://www.huifu.com" title="Huifu" target="_blank"><img width="165" src="../images/vendor/huifu.com@2x.png" alt="Huifu"></a> <a href="http://www.dodoca.com" title="Dodoca Information Technology" target="_blank"><img width="165" src="../images/vendor/dodoca.com@2x.png" alt="Dodoca Information Technology"></a> <a href="https://bytedance.com" title="ByteDance" target="_blank"><img width="165" src="../images/vendor/bytedance@2x.png" alt="ByteDance"></a> <a href="https://www.flashexpress.com" title="Flash Express" target="_blank"><img width="165" src="../images/vendor/flashexpress.com@2x.png" alt="Flash Express"></a> <a href="https://jimengio.com" title="JimengIO" target="_blank"><img width="165" src="../images/vendor/jimengio.com@2x.png" alt="JimengIO"></a> <a href="https://www.shannonai.com" title="Shannon.AI" target="_blank"><img width="165" src="../images/vendor/shannonai.com@2x.png" alt="Shannon.AI"></a> <a href="https://ibm.com" title="IBM" target="_blank"><img width="165" src="../images/vendor/ibm@2x.png" alt="IBM"></a> <a href="https://www.basedig.com" title="Basedig" target="_blank"><img width="165" src="../images/vendor/basedig.com@2x.png" alt="Basedig"></a> <a href="https://www.meitu.com" title="Meitui" target="_blank"><img width="165" src="../images/vendor/meitu.com@2x.png" alt="Meitui"></a> <a href="https://www.amazon.com" title="Amazon" target="_blank"><img width="165" src="../images/vendor/amazon@2x.png" alt="Amazon"></a> <a href="https://www.deloitte.com" title="Deloitte" target="_blank"><img width="165" src="../images/vendor/deloitte@2x.png" alt="Deloitte"></a> <a href="https://nl-a.ru" title="Neuro Lab! Algorithms" target="_blank"><img width="165" src="../images/vendor/nl-a.ru@2x.png" alt="Neuro Lab! Algorithms"></a> <a href="https://58.com" title="58.com" target="_blank"><img width="165" src="../images/vendor/58.com@2x.png" alt="58.com"></a> <a href="https://ke.com" title="ke.com" target="_blank"><img width="165" src="../images/vendor/ke.com@2x.png" alt="ke.com"></a> <a href="https://www.microsoft.com" title="Microsoft" target="_blank"><img width="165" src="../images/vendor/microsoft@2x.png" alt="Microsoft"></a> <a href="https://www.bytebase.com" title="ByteBase" target="_blank"><img width="165" src="../images/vendor/bytebase.com@2x.png" alt="ByteBase"></a> <a href="https://www.intel.com" title="Intel" target="_blank"><img width="165" src="../images/vendor/intel@2x.png" alt="Intel"></a> <a href="https://www.tencent.com" title="Tencent" target="_blank"><img width="165" src="../images/vendor/tencent@2x.png" alt="Tencent"></a> <a href="https://www.mihoyo.com" title="miHoYo" target="_blank"><img width="165" src="../images/vendor/mihoyo@2x.png" alt="miHoYo"></a> <a href="http://www.nsfocus.com.cn" title="NSFOCUS Technologies Group Co Ltd" target="_blank"><img width="165" src="../images/vendor/nsfocus@2x.png" alt="NSFOCUS Technologies Group Co Ltd"></a>

Se sua empresa ou produto também utiliza Excelize, seja bem-vindo, <a href="mailto: xuri.me@gmail.com?Subject=Please add our company in Excelize Introduction page&amp;Body=Ol%C3%A1%2C%20aqui%20%C3%A9%20%3Cseu%20nome%3E%20da%20%3Cnome%20da%20sua%20empresa%3E.%0AEstamos%20usando%20o%20Excelize%20e%20teremos%20orgulho%20de%20adicionar%20o%20nome%20da%20nossa%20empresa%20%C3%A0%20p%C3%A1gina%20de%20introdu%C3%A7%C3%A3o%20do%20Excelize.%0APor%20favor%2C%20veja%20o%20anexo%20do%20nosso%20logotipo.%20%3CCertifique-se%20de%20incluir%20o%20logotipo%20no%20anexo%3E%0A" title="enviar logotipo por e-mail">envie-nos o logotipo</a>.

## Comunidade

- [Grupo do Facebook](https://www.facebook.com/groups/excelize)
- [Grupo do Google](https://groups.google.com/g/excelize)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/excelize)
- [Canal Slack](https://join.slack.com/t/xuri/shared_invite/zt-eriqdkeo-wV04zcCdBiiZveFgY86Wzw)
- [Gitter](https://gitter.im/excelize/community)
- [Comunidade no Telegram](https://t.me/excelize)
- [Comunidade no Discord](https://discord.gg/MWV8MBQGtv)
- [Comunidade Excelize no Microsoft Teams](https://teams.live.com/l/invite/FBA8aHkflqEj5SNzQM)
- [Comunidade Skype](https://join.skype.com/YW3OFS5QjYcV?source=qr-ios): <a href="../images/skype_group@2x.png" alt="Comunidade Excelize Skype" target="_blank" target="_blank">participe via QR Code</a>
- [Comunidade Line](http://line.me/ti/g/NFIjhfbP_g): <a href="../images/line_group@2x.png" alt="Comunidade Excelize Line" target="_blank" target="_blank">participe via QR Code</a>
- [ID do grupo DingTalk](https://qr.dingtalk.com/action/joingroup?code=v1,k1,6tmzbBbJuQkGezVdHJjsHz29CZI9F49xeW+cvOaECtk=&_dt_no_comment=1&origin=11): `30047129` | <a href="../images/dingtalk_group@2x.png" alt="Grupo Excelize DingTalk" target="_blank" target="_blank">participe via QR Code</a>
- ID do grupo QQ: `1302058237` (Informações de verificação: Excelize) | <a href="../images/qq_group@2x.png" alt="Excelize QQ Group ID" target="_blank" target="_blank">participe via QR Code</a>
- Excelize o ID do WeChat: `hixuri` (Informações de verificação: Excelize) | <a href="../images/wechat_group@2x.png" alt="Comunidade Excelize WeChat" target="_blank" target="_blank">participe via QR Code</a>
- Grupo WeCom (Informações de verificação: Excelize): <a href="../images/wecom_group@2x.png" title="Grupo Excelize WeCom" target="_blank">participe via QR Code</a>
- ID do grupo InFlow: `4375928` | <a href="../images/inflow_group@2x.png" alt="Grupo Excelize Inflow" target="_blank" target="_blank">participe via QR Code</a>

## Patrocinador Excelize Development

Se você é um usuário individual e gostou da produtividade de usar o Excelize, considere fazer uma doação como um sinal de agradecimento - como comprar um café para mim de vez em quando ou apoiar este projeto tornando-se um patrocinador.

<a href="https://github.com/sponsors/xuri" title="GitHub Sponsor" target="_blank"><img width="170" src="../images/github_sponsor@2x.png" alt="GitHub Sponsor"></a> <a href="https://www.paypal.com/paypalme/xuri" title="Doe com Paypal" target="_blank"><img width="170" src="../images/donate@2x.png" alt="Doe com Paypal"></a> <a href="https://opencollective.com/excelize" title="Torne-se um patrocinador" target="_blank"><img height="61" src="../images/opencollective.com@2x.png" alt="Torne-se um patrocinador"></a> <a href="https://www.patreon.com/xuri" title="Apoie o Excelize no Patreon" target="_blank"><img height="61" src="../images/patreon.com@2x.png" alt="Apoie o Excelize no Patreon"></a>
