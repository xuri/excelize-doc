# 소개

<p align="center"><img width="650" src="../images/excelize.svg" alt="Excelize logo"></p>

Excelize 는 순수 Go로 작성된 라이브러리로 XLAM / XLSM / XLSX / XLTM / XLTX 파일에서 읽고 쓸 수있는 기능 세트를 제공합니다. Microsoft Excel&trade; 2007 이상에서 생성 된 스프레드 시트 문서 읽기 및 쓰기를 지원합니다. 높은 호환성으로 복잡한 구성 요소를 지원하고 대량의 데이터가있는 워크 시트에서 데이터를 생성하거나 읽을 수있는 스트리밍 API 를 제공했습니다. 이 라이브러리에는 Go 버전 1.23.0 이상이 필요합니다.

- 소스 코드: [github.com/xuri/excelize](https://github.com/xuri/excelize)
- 발행물: [github.com/xuri/excelize/issues](https://github.com/xuri/excelize/issues)
- go.dev: [pkg.go.dev/github.com/xuri/excelize/v2](https://pkg.go.dev/github.com/xuri/excelize/v2)
- 면허: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- 마지막 버전: [v2.9.1](https://github.com/xuri/excelize/releases/latest)
- 문서 업데이트 시간: 2025 년 6 월 24 일

## 프로젝트 미션

Excelize 의 목표는 OOXML (Office Open XML) 표준을 준수하는 xlsx 파일을 처리하는 Excel 문서 API의 Go 언어 버전을 만들고 유지 관리하는 것입니다. Excelize 를 사용하면 Go를 사용하여 MS Excel 파일을 읽고 쓸 수 있습니다.

## Excelize 를 사용해야하는 이유

어떤 경우에는 기존 Excel 문서 내용 읽기, 새 Excel 문서 작성, 기존 문서 (템플릿) 기반의 새 Excel 문서 생성, Excel 문서에 이미지 삽입, 차트 등의 프로그램을 통해 Excel 문서를 조작해야합니다. 테이블로 사용하고 때로는 여러 플랫폼에서 이러한 작업을 구현해야합니다. Excelize 는 이러한 요구를 쉽게 충족시킬 수 있습니다.

## 잘 알려진 고객

<img width="165" src="../images/vendor/360@2x.png" alt="Qihoo 360"> <img width="165" src="../images/vendor/baidu@2x.png" alt="Baidu, Inc."> ![INTSIG](../images/vendor/intsig.com_en.png) <img width="165" src="../images/vendor/inke@2x.png" alt="Inke, Inc."> <img width="165" src="../images/vendor/meituan@2x.png" alt="Meituan-Dianping"> <img width="165" src="../images/vendor/netease@2x.png" alt="NetEase"> <img width="165" src="../images/vendor/bilibili@2x.png" alt="Bilibili"> <img width="165" src="../images/vendor/qianxin.com_en@2x.png" alt="Qi An Xin Group"> <img width="165" src="../images/vendor/alibabagroup@2x.png" alt="Alibaba Group"> <img width="165" src="../images/vendor/ele.me@2x.png" alt="ele.me"> <img width="165" src="../images/vendor/huifu.com@2x.png" alt="Huifu"> <img width="165" src="../images/vendor/dodoca.com@2x.png" alt="Dodoca Information Technology"> <img width="165" src="../images/vendor/bytedance@2x.png" alt="ByteDance"> <img width="165" src="../images/vendor/flashexpress.com@2x.png" alt="Flash Express"> <img width="165" src="../images/vendor/jimengio.com@2x.png" alt="JimengIO"> <img width="165" src="../images/vendor/shannonai.com@2x.png" alt="Shannon.AI"> <img width="165" src="../images/vendor/ibm@2x.png" alt="IBM"> <img width="165" src="../images/vendor/basedig.com@2x.png" alt="Basedig"> <img width="165" src="../images/vendor/meitu.com@2x.png" alt="Meitui"> <img width="165" src="../images/vendor/amazon@2x.png" alt="Amazon"> <img width="165" src="../images/vendor/deloitte@2x.png" alt="Deloitte"> <img width="165" src="../images/vendor/nl-a.ru@2x.png" alt="Neuro Lab! Algorithms"> <img width="165" src="../images/vendor/58.com@2x.png" alt="58.com"> <img width="165" src="../images/vendor/ke.com@2x.png" alt="ke.com"> <img width="165" src="../images/vendor/microsoft@2x.png" alt="Microsoft"> <img width="165" src="../images/vendor/bytebase.com@2x.png" alt="ByteBase"> <img width="165" src="../images/vendor/intel@2x.png" alt="Intel"> <img width="165" src="../images/vendor/tencent@2x.png" alt="Tencent"> <img width="165" src="../images/vendor/mihoyo@2x.png" alt="miHoYo"> <img width="165" src="../images/vendor/nsfocus@2x.png" alt="NSFOCUS Technologies Group Co Ltd"> <img width="165" src="../images/vendor/gree.com@2x.png" alt="Gree"> <img width="165" src="../images/vendor/jd.com@2x.png" alt="JD.com, Inc."> <img width="165" src="../images/vendor/zhiyitech.cn@2x.png" alt="Hangzhou Zhiyi Technology Co., Ltd.">

회사 나 제품이 Excelize 도 사용하고 있다면 <a href="mailto: xuri.me@gmail.com?Subject=Excelize%20%EC%86%8C%EA%B0%9C%20%ED%8E%98%EC%9D%B4%EC%A7%80%EC%97%90%20%EB%8B%B9%EC%82%AC%EB%A5%BC%20%EC%B6%94%EA%B0%80%ED%95%B4%EC%A3%BC%EC%84%B8%EC%9A%94&amp;Body=%EC%95%88%EB%85%95%ED%95%98%EC%84%B8%EC%9A%94.%20%EC%A0%80%EB%8A%94%20%3C%EA%B7%80%ED%95%98%EC%9D%98%20%ED%9A%8C%EC%82%AC%20%EC%9D%B4%EB%A6%84%3E%20%EC%9D%98%20%3C%EA%B7%80%ED%95%98%EC%9D%98%20%EC%9D%B4%EB%A6%84%3E%20%EC%9E%85%EB%8B%88%EB%8B%A4.%0A%EC%9A%B0%EB%A6%AC%EB%8A%94%20Excelize%20%EB%A5%BC%20%EC%82%AC%EC%9A%A9%ED%95%98%EA%B3%A0%20%EC%9E%88%EC%9C%BC%EB%A9%B0%20Excelize%20%EC%86%8C%EA%B0%9C%20%ED%8E%98%EC%9D%B4%EC%A7%80%EC%97%90%20%EC%9A%B0%EB%A6%AC%20%ED%9A%8C%EC%82%AC%20%EC%9D%B4%EB%A6%84%EC%9D%84%20%EC%B6%94%EA%B0%80%ED%95%98%EA%B2%8C%20%EB%90%9C%20%EA%B2%83%EC%9D%84%20%EC%9E%90%EB%9E%91%EC%8A%A4%EB%9F%BD%EA%B2%8C%20%EC%83%9D%EA%B0%81%ED%95%A9%EB%8B%88%EB%8B%A4.%0A%EB%8B%B9%EC%82%AC%20%EB%A1%9C%EA%B3%A0%EB%8A%94%20%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC%EC%9D%84%20%EC%B0%B8%EC%A1%B0%ED%95%98%EC%84%B8%EC%9A%94.%20%3C%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC%EC%97%90%20%EB%A1%9C%EA%B3%A0%EB%A5%BC%20%EB%B0%98%EB%93%9C%EC%8B%9C%20%ED%8F%AC%ED%95%A8%ED%95%B4%EC%A3%BC%EC%84%B8%EC%9A%94%3E%0A" title="로고 보내주기">로고 보내주기</a>.

## 커뮤니티

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
- [DingTalk Group ID](https://qr.dingtalk.com/action/joingroup?code=v1,k1,6tmzbBbJuQkGezVdHJjsHz29CZI9F49xeW+cvOaECtk=&_dt_no_comment=1&origin=11): `30047129` | <a href="../images/dingtalk_group@2x.png" title="Excelize DingTalk Group" target="_blank">join via QR Code</a>
- QQ Group ID: `1302058237` (Verification info: Excelize) | <a href="../images/qq_group@2x.png" title="Excelize QQ Group ID" target="_blank">join via QR Code</a>
- Excelize WeChat ID: `hixuri` (Verification info: Excelize) | <a href="../images/wechat_group@2x.png" title="Excelize WeChat Community" target="_blank">join via QR Code</a>
- WeCom Group (Verification info: Excelize): <a href="../images/wecom_group@2x.png" title="Excelize WeCom Group" target="_blank">join via QR Code</a>
- Inflow Group ID: `4375928` | <a href="../images/inflow_group@2x.png" title="Excelize Inflow Group" target="_blank">join via QR Code</a>

## 스폰서 Excelize 개발

개인 사용자이고 Excelize 를 사용하는 생산성을 즐겼다면 가끔 커피를 사는 것과 같이 감사의 표시로 기부하는 것이 좋습니다. 스폰서되기 를 통해이 프로젝트를 지원할 수도 있습니다.

<a href="https://github.com/sponsors/xuri" title="GitHub Sponsor" target="_blank"><img width="170" src="../images/github_sponsor@2x.png" alt="GitHub Sponsor"></a> <a href="https://www.paypal.com/paypalme/xuri" title="Paypal 로 기부하기" target="_blank"><img width="170" src="../images/donate@2x.png" alt="Paypal 로 기부하기"></a> <a href="https://opencollective.com/excelize" title="스폰서되기" target="_blank"><img height="61" src="../images/opencollective.com@2x.png" alt="스폰서되기"></a> <a href="https://www.patreon.com/xuri" title="Patreon 에서 Excelize 지원" target="_blank"><img height="61" src="../images/patreon.com@2x.png" alt="Patreon 서 Excelize 지원"></a>
