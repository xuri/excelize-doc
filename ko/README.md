# 소개

<p align="center"><img width="650" src="../images/excelize.png" alt="Excelize logo"></p>

<p align="center">
    <a href="https://travis-ci.org/360EntSecGroup-Skylar/excelize"><img src="https://travis-ci.org/360EntSecGroup-Skylar/excelize.svg?branch=master" alt="Build Status"></a>
    <a href="https://codecov.io/gh/360EntSecGroup-Skylar/excelize"><img src="https://codecov.io/gh/360EntSecGroup-Skylar/excelize/branch/master/graph/badge.svg" alt="Code Coverage"></a>
    <a href="https://goreportcard.com/report/github.com/360EntSecGroup-Skylar/excelize"><img src="https://goreportcard.com/badge/github.com/360EntSecGroup-Skylar/excelize" alt="Go Report Card"></a>
    <a href="https://godoc.org/github.com/360EntSecGroup-Skylar/excelize"><img src="https://godoc.org/github.com/360EntSecGroup-Skylar/excelize?status.svg" alt="GoDoc"></a>
    <a href="https://opensource.org/licenses/BSD-3-Clause"><img src="https://img.shields.io/badge/license-bsd-orange.svg" alt="Licenses"></a>
    <a href="https://www.paypal.me/xuri"><img src="https://img.shields.io/badge/Donate-PayPal-green.svg" alt="Donate"></a>
</p>

Excelize 는 순수 Go 로 작성되고 XLSX 파일에 쓰고 읽을 수있는 함수 세트를 제공하는 라이브러리입니다. 지원은 Microsoft Excel&trade; 2007 이후 버전에서 생성 된 XLSX 파일을 읽고 씁니다. XLSX 의 원본 차트를 잃지 않고 파일 저장을 지원합니다. 이 라이브러리에는 Go 버전 1.8 이상이 필요합니다.

- 소스 코드: [github.com/360EntSecGroup-Skylar/excelize](https://github.com/360EntSecGroup-Skylar/excelize)
- 발행물: [github.com/360EntSecGroup-Skylar/excelize/issues](https://github.com/360EntSecGroup-Skylar/excelize/issues)
- GoDoc: [godoc.org/github.com/360EntSecGroup-Skylar/excelize](https://godoc.org/github.com/360EntSecGroup-Skylar/excelize)
- 면허: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- 마지막 버전: [v1.4.1](https://github.com/360EntSecGroup-Skylar/excelize/releases/latest)
- 문서 업데이트 시간: 2019 년 3 월 16 일

## 프로젝트 미션

Excelize 의 목표는 OOXML (Office Open XML) 표준을 준수하는 xlsx 파일을 처리하는 Excel 문서 API의 Go 언어 버전을 만들고 유지 관리하는 것입니다. Excelize 를 사용하면 Go를 사용하여 MS Excel 파일을 읽고 쓸 수 있습니다.

## Excelize 를 사용해야하는 이유

어떤 경우에는 기존 Excel 문서 내용 읽기, 새 Excel 문서 작성, 기존 문서 (템플릿) 기반의 새 Excel 문서 생성, Excel 문서에 이미지 삽입, 차트 등의 프로그램을 통해 Excel 문서를 조작해야합니다. 테이블로 사용하고 때로는 여러 플랫폼에서 이러한 작업을 구현해야합니다. Excelize 는 이러한 요구를 쉽게 충족시킬 수 있습니다.

## 잘 알려진 고객

<a href="https://360.net" title="360 엔터프라이즈 보안 그룹" target="_blank"><img width="165" src="../images/vendor/360@2x.png" alt="360 엔터프라이즈 보안 그룹"></a> <a href="https://www.baidu.com" title="Baidu, Inc." target="_blank"><img width="165" src="../images/vendor/baidu@2x.png" alt="Baidu, Inc."></a> [![CCi. Inc.](../images/vendor/ccint.com.png)](https://www.ccint.com) <a href="https://www.inke.cn" title="Inke, Inc." target="_blank"><img width="165" src="../images/vendor/inke@2x.png" alt="Inke, Inc."></a> <a href="https://www.meituan.com" title="Meituan-Dianping" target="_blank"><img width="165" src="../images/vendor/meituan@2x.png" alt="Meituan-Dianping"></a> <a href="https://www.163.com" title="NetEase" target="_blank"><img width="165" src="../images/vendor/netease@2x.png" alt="NetEase"></a>

회사 나 제품이 Excelize 도 사용하고 있다면 [로고 보내주기](mailto: xuri.me@gmail.com?Subject=Please add our company in Excelize Introduction page&amp;Body=Hello%2C%20this%20is%20%3Cyour%20name%3E%20from%20%3Cyour%20company%20name%3E.%0AWe%20are%20using%20Excelize%20and%20will%20be%20proud%20to%20add%20our%20company%20name%20to%20Excelize%20Introduction%20page.%0APlease%20see%20attachment%20for%20our%20logo.%20%3CBe%20sure%20to%20include%20logo%20in%20attachment%3E%0A).