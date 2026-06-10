---
title: ' [!DNL Adobe Experience Manager] 6.5 릴리스 정보'
description: ' [!DNL Adobe Experience Manager] 6.5에 대한 릴리스 정보, 새로운 기능, 설치 방법 및 자세한 변경 목록을 찾으십시오.'
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: e8b2b6b52c4071aa90fddaf2cd19fec1236b8472
workflow-type: tm+mt
source-wordcount: '8148'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] 6.5 최신 서비스 팩 릴리스 노트 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!--
DO NOT DELETE THIS HIDDEN NOTE!      DO NOT DELETE THIS HIDDEN NOTE!
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section.
-->

## 릴리스 요약 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 버전 | 6.5.25.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2026년 5월 21일 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 다운로드 URL | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

Experience Manager 6.5.25.0에는 새로운 기능, 주요 고객 요청 개선 사항 및 버그 수정 사항이 포함되어 있습니다. 또한 2019년 4월 이후 제공되는 6.5 기반 위에 구축된 성능, 안정성 및 보안 개선 사항이 포함되어 있습니다.

이 서비스 팩 릴리스는 중요한 버그 수정 및 보안 강화 등 사이트, Assets 및 Foundation에 걸쳐 275개의 백포트를 제공합니다. 또한 이 릴리스는 광범위한 키보드 탐색, 포커스 관리, ARIA 의미 체계, 색상 대비 개선 사항 및 WCAG 표준에 맞는 터치 타겟 크기 조정으로 사이트 작성 전반에 대한 접근성을 향상시킵니다.

이 릴리스에서는 기본적으로 횡단보도를 사용할 수 있으므로 설치 후 별도의 패키지 또는 구성이 필요하지 않습니다.

보안 백포트는 XSS 취약점을 해결하고 공유 에셋 메타데이터 처리를 개선합니다.

콘텐츠 조각 및 GraphQL API는 또한 포함된 이미지 참조, 지속 쿼리 처리 및 편집기 현지화에 대해 포함하여 안정성이 개선되었습니다.


<!-- UPDATE FOR EACH NEW RELEASE -->

### Forms의 주요 기능 및 개선 사항

* [다중 스레드 PDF Generator 전환](/help/forms/using/install-configure-document-services.md#windows-only-enable-multi-threaded-pdf-generator-conversions): AEM Forms이 구성된 단일 사용자 계정에서 Windows 서비스로 실행될 때 Microsoft Word(doc/docx) 및 Excel(xls/xlsx) 동시 전환을 실행할 수 있는 지원이 추가되었습니다.

* [XFA 기반 PDF에 대한 계층 구조 책갈피](https://helpx.adobe.com/kr/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf): 이제 출력 서비스 및 AEM Forms Designer에서 정적 대화형 및 플랫 XFA 기반 PDF에 구조화된 책갈피 계층을 생성합니다. 책갈피는 텍스트 상자의 접근성 속성에 설정된 제목 수준(H1~H6)을 따르므로 H2~H6 항목은 병렬로 표시되지 않고 올바른 상위 항목 아래에 중첩됩니다.

* [JEE 트랜잭션 로그의 양식 수준 세부 정보](/help/forms/using/transaction-report-overview-jee.md#form-level-details-transaction-log-jee): 이제 JEE의 AEM Forms은 기존 서비스 및 작업 정보와 더불어 각 트랜잭션에 대해 `transaction_log.log`에 양식 수준 세부 정보를 기록합니다. 관리자는 제출, 변환 및 변환을 분석할 때 트랜잭션 보고 데이터를 특정 양식과 상호 연관시킬 수 있습니다. (FORMS-21574)

* [지원되는 플랫폼 매트릭스를 업데이트했습니다](/help/forms/using/aem-forms-jee-supported-platforms.md): JEE 서비스 팩 6.5.25.0의 AEM Forms은 다음 최신 기술과의 호환성을 지원합니다.
   * JBoss® EAP(Enterprise Application Platform) 7.4.23
   * ® Content Manager 클라이언트 8.7
   * ® Windows Terminal Server 2025의 AEM Forms Designer



## 서비스 팩 25의 문제가 해결되었습니다. {#fixed-issues}

<!-- 6.5.25.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->


### [!DNL Sites]{#sites-6525}

#### 접근성 {#sites-accessibility-6525}

* 사이트 목록 보기의 테이블 행 끌어서 놓기 컨트롤은 이제 키보드 탐색과 함께 작동합니다. 화면 판독기 및 키보드 사용자는 작업 중에 행을 재정렬하고 피드백을 받을 수 있습니다. (SITES-24946)

* 이제 레이아웃 편집 도구 모음에 의미 있는 화면 판독기 시퀀스에서 더 작은 화면 및 태블릿 레이블이 표시됩니다. 사용자는 순서에 관계없이 듣는 대신 관련 자 측정으로 레이블을 듣습니다. (SITES-25291)
* 이제 [견본] 팝오버 모달이 주석 모달에서 열릴 때 포커스를 올바르게 관리합니다. 포커스는 선택한 견본 버튼으로 직접 이동하는 대신 모달 머리글에서 시작됩니다. (SITES-25275)
* 이제 티저 모달 을 통해 키보드로 대화 상자를 이동할 수 있습니다. 사용자는 페이지에서 모달의 위치를 변경할 때 더 이상 마우스가 필요하지 않습니다. (SITES-25226)
* 카드 보기는 불필요한 ARIA 그리드 동작을 제거하여 액세스 가능성을 향상시킵니다. 화면 판독기 사용자는 시각적 레이아웃과 일치하지 않는 그리드 탐색 컨트롤 없이 보다 명확한 카드 정보를 받을 수 있습니다. (SITES-24933)
* 이제 반복 가리키기 작업 후 삭제 모달의 도구 설명이 일관되게 표시됩니다. 사용자는 포인터를 멀리 이동하고 아이콘으로 돌아가 툴팁을 다시 읽을 수 있습니다. (SITES-24778)
* 이제 사용자가 Sites 홈 페이지에서 왼쪽 레일을 열면 왼쪽 레일이 예상 순서로 포커스를 받습니다. 키보드 및 화면 판독기 사용자는 확장된 영역을 건너뛰지 않고 구성 버튼에서 레일 컨텐츠로 이동할 수 있습니다. (SITES-24754)
* 이제 포커스 관리는 회전 모달 대화 상자에서 일관되게 작동합니다. 키보드 및 화면 판독기 사용자는 모달 머리글에서 시작하여 대화 상자를 닫은 후 원래 컨트롤로 돌아갈 수 있습니다. (SITES-24716)
* 이제 링크 선택 대화 상자가 대화 상자를 닫은 후 링크 선택 대화 상자를 연 컨트롤로 포커스를 돌아갑니다. 대화 상자를 닫아도 키보드와 화면 판독기 사용자가 더 이상 위치를 잃지 않습니다. (SITES-24707)
* 작성자가 대화 상자를 열거나 닫을 때 이미지 모달이 더 이상 첫 번째 탭이나 기본 페이지 랜드마크로 포커스를 이동하지 않습니다. 포커스는 대화 상자 머리글로 이동한 다음 대화 상자를 연 컨트롤로 돌아갑니다. (SITES-24693)
* 이제 모달 대화 상자가 열리면 참조 레일이 포커스를 올바르게 관리합니다. 키보드 및 화면 판독기 사용자는 대화 상자를 닫을 때까지 대화 상자 내에 남아 있다가 컨텍스트를 손실하지 않고 탐색을 계속합니다. (SITES-24683)
* 하이퍼링크 경로 선택 모달 작성자가 열거나 닫을 때 더 이상 포커스가 잘못된 필드나 컨트롤로 이동하지 않습니다. 포커스는 모달 머리글에서 시작되고 모달을 연 버튼으로 돌아갑니다. (SITES-24672)
* 작성자가 티저 모달을 열거나 닫을 때 티저 모달이 더 이상 첫 번째 탭이나 페이지 맨 위로 포커스를 이동하지 않습니다. 이제 포커스가 예상되는 대화 상자 흐름을 따르며 불필요한 화면 판독기 알림을 줄입니다. (SITES-24522)

* 이제 페이지 편집기 잠금 버튼을 사용하여 보다 정밀한 화면 판독기 피드백을 제공할 수 있습니다. 화면 판독기는 가능한 경우 title 속성을 사용하므로 보조 기술을 사용하는 작성자의 자세한 알림을 줄일 수 있습니다. (SITES-41431)
* 이제 키보드 탐색에서 숨겨진 콘텐츠를 건너뜁니다. 사용자는 볼 수 없는 콘텐츠로 포커스를 이동하지 않고 표시되는 인터페이스 요소를 통해 이동할 수 있습니다. (SITES-41430)
* 이제 사용자가 오버레이를 닫으면 키보드 포커스가 트리거 요소로 돌아갑니다. 페이지 편집기에서 더 이상 포커스를 오버레이로 다시 보내지 않으므로 키보드 사용자의 탐색이 향상됩니다. (SITES-40819)
* 이제 사용자가 키보드로 도구 모음 항목을 탐색할 때 페이지 편집기 도구 모음에 도구 설명과 같은 레이블이 표시됩니다. 포커스가 항목에서 항목으로 이동할 때 각 도구 모음 작업을 이해할 수 있습니다. (SITES-40751)
* 구성 요소 브라우저 항목을 마우스로 가리키면 활성 텍스트 구성 요소에서 더 이상 포커스가 제거되지 않습니다. 작성자는 중단 없이 텍스트를 편집할 수 있으며 키보드 포커스는 예측 가능합니다. (SITES-35370)
* 이제 화면 판독기에 Search Modal sort direction 버튼이 더 명확하게 표시됩니다. 단추 레이블이 더 이상 동일한 방향을 반복하지 않으며 전환 동작을 더 잘 설명합니다. (SITES-25534)
* 이제 검색 모달에 파일 또는 폴더 변경 목록 상자에서 선택한 옵션에 대한 시각적 표시기가 표시됩니다. 사용자는 포커스에만 의존하지 않고 현재 이동 경로 옵션을 식별할 수 있습니다. (SITES-25532)
* 이제 검색 모달이 정렬 기준 레이블의 대비를 증가시킵니다. 텍스트는 접근성 요구 사항을 충족하며 시력이 낮은 사용자의 가독성을 향상시킵니다. (SITES-25531)
* 이제 장치 선택 단추에 레이아웃 편집 도구 모음에 올바른 현재 상태 정보가 표시됩니다. 화면 판독기 사용자는 오해의 소지가 있는 토글 상태를 듣지 않고도 활성 장치를 식별할 수 있습니다. (SITES-25524)
* 이제 키보드 및 화면 판독기 탐색에서 포커스가 사라지면 받은 편지함 메뉴가 닫힙니다. 사용자는 포커스가 다른 곳으로 이동하는 동안 메뉴가 열려 있는 혼동 상태를 방지합니다. (SITES-25518)
* 이제 키보드 및 화면 판독기 탐색에서 포커스가 없으면 도움말 메뉴가 닫힙니다. 메뉴가 열려 있는 동안에는 포커스가 더 이상 메뉴 외부의 콘텐츠로 이동하지 않습니다. (SITES-25517)
* 이제 콘텐츠 조각 홈 페이지에서 사이드바 탭에 대해 일관되게 액세스 가능한 레이블을 제공합니다. NVDA는 사용자가 탭 컨트롤을 탐색할 때 탭 레이블을 올바르게 발표합니다. (SITES-25509)
* 이제 페이지 정보 메뉴의 집중 옵션이 최소 대비 요구 사항을 충족합니다. 향상된 대비는 시력이 낮은 사용자가 활성 메뉴 항목을 식별하는 데 도움이 됩니다. (SITES-25321)
* 이제 키보드 탐색은 축소된 인구 통계 도구 모음의 숨겨진 컨트롤을 건너뜁니다. 포커스는 보이는 대화형 요소에 유지되므로 레이아웃 미리 보기에서 탐색 순서가 개선됩니다. (SITES-25304)
* 이제 디바이스 회전 버튼을 통해 레이아웃 편집 도구 모음에서 화면 판독기 피드백을 더 명확하게 확인할 수 있습니다. 화면 판독기는 현재 방향과 이를 변경하는 동작을 알려줍니다. (SITES-25292)
* 이제 레이아웃 편집 도구 모음에 데스크탑 버튼에 대해 선택된 상태가 선명하게 표시됩니다. 데스크탑 옵션은 다른 장치 버튼과 일치하며 활성 보기를 보다 쉽게 식별할 수 있도록 합니다. (SITES-25290)
* 이제 레이아웃 편집 도구 모음에서 보조 기술에 대한 눈금자 영역에 레이블을 지정합니다. 화면 판독기 사용자는 레이아웃 편집 중에 더 이상 레이블이 지정되지 않은 측정 값이 발생하지 않습니다. (SITES-25287)
* 이제 레이아웃 편집 도구 모음에 전체 iPhone 8 Plus 단추 레이블이 선택 취소 상태로 표시됩니다. 버튼 주위에 충분한 공간이 있으면 레이블이 더 이상 잘리지 않습니다. (SITES-25284)
* 보고된 문제는 레이아웃 편집 도구 모음에 있는 포커스 표시기에 대해 설명했는데, 이 표시기는 여러 장치 컨트롤을 포함하는 것으로 보입니다. 포커스 윤곽선에 인접 단추가 들어 있을 때 활성 컨트롤을 추적하지 못할 수 있는 키보드 사용자에게 문제가 집중되었습니다. 문제가 설계대로 작동하고 있었습니다. (SITES-25283)
* 보고된 문제는 각 버튼 레이블 전에 주석을 발표한 주석 양식 버튼을 설명했습니다. 주석, 색상 견본, 삭제와 같은 작업에 대한 명확하지 않은 화면 판독기 출력에 관심이 집중되었습니다. (SITES-25277)
* 이제 주석 단추 텍스트에 주석 모달에서 충분한 대비가 사용됩니다. 이 업데이트는 시력이 낮은 사용자의 가독성을 향상시키고 WCAG 대비 요구 사항을 지원합니다. (SITES-25267)
* 이제 사용자가 새 구성 요소 삽입 목록을 필터링하면 화면 판독기에 상태 업데이트가 수신됩니다. 모달은 사용자가 입력하는 동안 목록이 변경되었음을 이해할 수 있도록 결과 변경 사항을 알려줍니다. (SITES-25251)
* 기록된 문제는 주석 양식 제목에 대한 누락된 제목 의미를 설명했습니다. 문제는 화면 판독기 탐색과 양식 구조를 이해하는 기능에 중점을 둡니다. (SITES-25248)
* 이제 페이지 편집기 측면 레일의 머리글 수준은 더 명확한 콘텐츠 계층 구조를 따릅니다. 왼쪽 레일 섹션은 더 이상 보조 기술의 기본 페이지 머리글로 표시되지 않습니다. (SITES-25222)
* 이제 Assets 왼쪽 레일의 편집 버튼에 더 큰 터치 대상이 있습니다. 이동성이 필요한 사용자는 보다 쉽게 버튼을 활성화하고 가까운 제어 장치를 피할 수 있습니다. (SITES-25221)
* 이제 Assets 왼쪽 레일에서 편집 버튼을 누르면 새 브라우저 탭이 열립니다. 사용자는 예기치 않게 컨텍스트를 잃는 대신 탐색 변경을 예상할 수 있습니다. (SITES-25220)
* 사용자가 텍스트 간격을 늘리면 구성 요소 제목이 올바르게 표시됩니다. 측면 레일은 읽을 수 있는 레이블을 유지하고 WCAG 텍스트 간격 요구 사항을 지원합니다. (SITES-25219)
* 이제 사이드 레일 구성 요소의 필터 필드가 적절한 액세스 가능한 이름을 노출합니다. 이 업데이트는 화면 판독기 사용자가 자리 표시자 텍스트에 의존하지 않고 필드를 식별하는 데 도움이 됩니다. (SITES-25212)
* 보고된 문제가 주석 모드에서 비논리적 포커스 시퀀스를 설명했습니다. 키보드 사용자는 모드를 활성화한 후 Shift+Tab을 사용하지 않으면 주석 도구 모음을 놓친 것으로 알려졌습니다. (SITES-24996)
* 편집기 캔버스는 상단 표시줄 제목을 머리글로 노출합니다. 화면 판독기는 올바른 구조로 제목을 알려 탐색과 페이지 이해력을 향상시킬 수 있습니다. (SITES-24993)
* 접근성 보고서에서 사용자가 보기를 전환하는 동안 표시되는 로드 상태 메시지에 대해 부족한 대비를 기록했습니다. 시력이 약하거나 색맹인 사용자가 가독성에 초점을 맞췄다. (SITES-24991)
* 접근성 보고서는 카드 링크에 설명이 아닌 텍스트가 포함되어 있음을 주목했습니다. 이 문제는 화면 판독기 사용자가 추가 컨텍스트 없이 각 링크 대상을 이해할 수 있도록 돕는 데 중점을 둡니다. (SITES-24975)
* 이제 사이트 목록 보기에 라이브 카피 텍스트가 더 강한 대비를 사용하여 표시됩니다. 업데이트는 시력이 낮은 작성자와 밝은 화면 조건에서 작업하는 사용자의 가독성을 향상시킵니다. (SITES-24956)
* 사용자가 키보드를 확장하면 키보드 탐색이 포커스를 에뮬레이터 메뉴로 이동합니다. 이 동작은 화면 판독기 및 키보드 사용자가 예상한 순서로 메뉴 옵션에 액세스하는 데 도움이 됩니다. (SITES-24954)
* 이제 사이트 목록 보기를 통해 테이블 행에서 드래그 앤 드롭 버튼의 가시성이 향상되었습니다. 작성자가 콘텐츠 순서를 변경할 때 컨트롤을 보다 쉽게 식별할 수 있습니다. (SITES-24951)
* 카드가 동일한 대상을 공유할 때 더 이상 이미지 링크와 제목 링크를 별도의 링크로 표시하지 않습니다. 이 업데이트는 화면 판독기 복잡도를 줄이고 탐색 효율성을 개선합니다. (SITES-24947)
* 이제 헤더 메뉴 단추에 더 정확한 접근성 특성이 사용됩니다. 화면 판독기는 단추를 대화 상자를 여는 컨트롤 대신 확장 가능한 컨트롤로 알려줍니다. (SITES-24742)
* 이제 받은 편지함은 의미 목록 마크업으로 관련 링크를 표시합니다. 화면 판독기 사용자는 받은 편지함 링크의 수와 그룹화를 보다 쉽게 이해할 수 있습니다. (SITES-24730)
* 이제 헤더 단추 레이블은 자세한 액세스 가능한 이름을 사용하지 않습니다. 화면 판독기 사용자는 아이콘 텍스트에서 중복 역할 정보 없이 더 명확한 공지를 받을 수 있습니다. (SITES-24715)
* 이제 CSV 보고서 버튼을 통해 새 탭 동작에 대한 명확한 피드백을 제공할 수 있습니다. 사용자는 버튼을 선택하면 활성화하기 전에 새 브라우저 탭이 열립니다. (SITES-24704)
* 이제 모달 대화 상자에서는 헤더 컨트롤에 더 정확한 접근성 마크업을 사용합니다. 도움말 및 전체 화면 전환 단추는 대화형 컨트롤로 유지되며 더 이상 화면 판독기의 제목으로 나타나지 않습니다. (SITES-24696)
* 이제 필터 레일 랜드마크는 용도를 식별하는 고유한 레이블을 사용합니다. 화면 판독기 사용자는 여러 개의 유사한 랜드마크가 있는 페이지를 보다 자신 있게 탐색할 수 있습니다. (SITES-24686)
* 참조 레일 메시지는 이제 충분한 텍스트 대비를 사용하는 사용자에게 가독성을 제공합니다. 보고된 문제는 배경에 비해 너무 밝게 보이는 선택 및 다중 선택 메시지와 관련되었습니다. (SITES-24666)
* 이제 검색 모달에서 위치 제거 및 닫기 단추에 대한 더 큰 터치 대상을 제공합니다. 이러한 변화는 손 떨림, 연축 또는 저시력 사용자가 의도한 제어를 활성화하는 데 도움이 됩니다. (SITES-24530)
* Adobe Experience Manager 헤더 링크가 잘못된 ARIA 속성을 사용한다고 보고되었습니다. 테스트를 통해 링크가 확장 가능한 콘텐츠를 제어하므로 기존 액세스 가능 상태가 적절한지 확인했습니다. (SITES-24528)
* [구성 요소] 목록에서 더 이상 [줄 바꿈] 단추의 포커스 표시기가 잘려서 나타나지 않습니다. 표시되는 윤곽선은 키보드 사용자가 편집기에서 위치를 추적하는 데 도움이 됩니다. (SITES-24503)
* 보고된 문제는 구성 요소 패널에서 정보 툴팁 아이콘에 대한 텍스트 대체 요소가 누락된 것을 설명했습니다. 문제가 재현되지는 않았지만 검토 결과 정보 제공 아이콘에 액세스 가능한 명확한 이름이 표시되어야 합니다. (SITES-24500)
* 페이지 편집기는 더 이상 동일한 레이블을 사용하여 여러 지역 랜드마크를 노출하지 않습니다. 이제 각 랜드마크에는 액세스 가능한 고유한 이름이 있으므로 화면 판독기 사용자가 현재 영역을 식별할 수 있습니다. (SITES-24497)
* 이제 Change file 또는 folder 컨트롤은 컨트롤 레이블을 상태 정보와 구분합니다. 화면 판독기 사용자가 헤더 컨트롤을 탐색할 때 더 짧고 선명한 이름을 듣습니다. (SITES-24496)
* 이제 콘텐츠 조각 관리 테이블의 양방향 컨트롤에서 표준 키보드 탐색을 지원합니다. 키보드 사용자는 화살표 키 탐색을 통해서만 버튼과 링크를 발견하는 대신 탭하여 버튼과 링크를 찾을 수 있습니다. (SITES-24285)
* 이제 사이트 관리 UI는 화면 판독기에 대해 장식용 지구본 아이콘을 올바르게 처리합니다. 아이콘은 빈 대체 텍스트를 사용하므로 사용자는 의미 있는 인터페이스 콘텐츠만 들을 수 있습니다. (SITES-3057)

#### 관리 사용자 인터페이스{#sites-adminui-6525}

이제 사이트 콘솔에 저장된 **목록 보기** 열 설정이 올바르게 표시됩니다. 작성자가 설정 대화 상자를 다시 열면 선택한 열이 계속 선택되어 있고 활성 열 수가 정확하게 유지됩니다. (SITES-38576)

#### 클래식 UI{#sites-classicui-6525}

이제 클래식 UI 텍스트 구성 요소 대화 상자에 리치 텍스트 편집기(RTE) 컨텐츠가 원시 HTML 대신 서식 있는 텍스트로 표시됩니다. 작성자가 Source 모드로 전환하거나 마크업을 수동으로 제거하지 않고도 기존 텍스트를 편집할 수 있습니다. (SITES-38709)

#### 구성 요소 콘솔{#sites-component-console-6525}

* 이제 현지화된 문자 또는 멀티바이트 문자로 구성 요소 콘솔을 검색할 수 있습니다. 콘솔에는 번역되지 않은 영어 문자열 대신 현지화된 **제거** 레이블도 표시됩니다. (SITES-39747)
* 이제 구성 요소 속성 페이지는 도구 > 구성 요소 > 구성 요소 속성에서 문자열을 현지화합니다. 현지화된 작성 인터페이스에서 더 이상 번역되지 않은 영어 레이블을 볼 수 없습니다. (SITES-39745)

#### [!DNL Content Fragments]{#sites-contentfragments-6525}

이제 사용자가 필터를 선택하거나 변경하면 Assets 검색이 올바르게 응답합니다. 필터링된 결과 세트는 예상대로 업데이트되므로 Assets 콘솔에서 안정적인 검색 세분화를 복원할 수 있습니다. (SITES-38686)

#### [!DNL Content Fragments] - 관리자{#sites-admin-6525}

* 이제 Assets 목록 보기에 잠긴 콘텐츠 조각에 대해 현지화된 체크아웃한 도구 설명이 표시됩니다. 이 수정 사항은 작성자가 워크플로우 행을 검토할 때 현지화 일관성을 향상시킵니다. (SITES-42531)

* 이제 AEM은 콘텐츠 조각 다운로드 대화 상자에서 주 레이블을 현지화합니다. 이 수정 사항은 영어 이외의 로케일에서 다운로드 워크플로우를 일관되게 유지합니다. (SITES-42534)
* 이제 작성자가 Assets에서 콘텐츠 조각 게시를 예약할 때 AEM은 `Later` 상태 레이블을 변환합니다. 이 수정 사항은 현지화된 인터페이스에서 게시된 열을 일관되게 유지합니다. (SITES-42532)
* 이제 작성자가 제목 필드에 잘못된 문자를 입력하면 콘텐츠 조각 만들기에 현지화된 유효성 검사 메시지가 표시됩니다. 대화 상자에 현지화되지 않은 &quot;잘못된 이름 입력&quot; 문자열이 더 이상 표시되지 않습니다. (SITES-19796)
* 이제 콘텐츠 조각 편집 페이지에서 태그 및 컬렉션에 대해 현지화된 레이블을 사용합니다. 작성자는 현지화되지 않은 영어 문자열 대신 번역된 필드 이름을 볼 수 있습니다. (SITES-977)

#### [!DNL Content Fragments] - 조각 편집기{#sites-fragments-editor-6525}

* 이제 작성자가 컬렉션에서 컨텐츠를 제거할 때 컨텐츠 조각 편집기의 관련 컨텐츠에 올바른 현지화된 문자열이 표시됩니다. 이 대화 상자는 더 이상 컨텐츠 이름을 정의되지 않음으로 대체하지 않습니다. (SITES-33675)
* 이제 콘텐츠 조각 편집기에 구성된 자리 표시자 없이 탭의 번역된 일반 레이블이 표시됩니다. 현지화된 인터페이스는 더 이상 해당 편집기 영역에 번역되지 않은 영어 문자열을 표시하지 않습니다. (SITES-30715)
* 이제 콘텐츠 조각 편집기의 콘텐츠 참조 선택기에 허용된 에셋 유형에 대한 현지화된 레이블이 표시됩니다. 현지화된 인터페이스는 더 이상 지원되는 에셋 범주에 대한 영어 형식 이름을 표시하지 않습니다. (SITES-29699)

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6525}

* 이제 DAM 파일 이름에 공백 또는 비 ASCII 문자가 포함된 경우 GraphQL JSON 응답에는 콘텐츠 조각 리치 텍스트 필드의 포함된 이미지 참조가 포함됩니다. 이 수정 사항은 작성자가 에셋의 이름을 변경하지 않고도 애플리케이션이 참조된 이미지를 렌더링하는 데 도움이 됩니다. (SITES-42191)
* 이제 콘텐츠 조각에 대한 GraphQL 응답이 지속 쿼리를 더 안정적으로 처리합니다. 이 업데이트는 중복 캐시 헤더를 수정하고, 인코딩된 변수 처리를 개선하며, 누락된 콘텐츠 또는 실패한 쿼리에 대한 보다 명확한 응답을 반환합니다. (SITES-40159)
* 이제 GraphQL 지속 쿼리가 불필요한 오류 및 WARN 메시지 없이 로그에 실행됩니다. AEM은 인코딩된 변수를 올바르게 처리하므로 성공적인 쿼리는 더 이상 잘못된 `PersistedQueryServlet` 항목을 만들지 않습니다. (SITES-39354)

* 이제 GraphQL 엔드포인트 편집 대화 상자에서 인터페이스 문자열을 현지화합니다. 지역화된 인터페이스의 구성 메시지에서 번역되지 않은 GraphQL 스키마를 가져왔다는 것을 사용자가 더 이상 볼 수 없습니다. (SITES-34018)

#### [!DNL Content Fragments] - GraphQL 쿼리 편집기{#sites-graphql-query-editor-6525}

이제 선택한 구성 브라우저 이름에 CJK 또는 키릴 자모 문자가 포함되어 있으면 GraphQL 쿼리 편집기를 열 수 있습니다. 편집기에 오류가 표시되지 않고 끝점에 대한 지속 쿼리가 표시됩니다. (SITES-31616)

#### [!DNL Content Fragments] - 모델 및 모델 편집기{#sites-models-model-editor-6525}

* 이제 선택한 값에 유효한 모델 유형이 필요한 경우 콘텐츠 조각 모델 편집기에 현지화된 유효성 검사 메시지가 표시됩니다. 편집기에 번역되지 않은 영어 메시지가 현지화된 인터페이스에 더 이상 표시되지 않습니다. (SITES-41117)
* 이제 콘텐츠 조각 모델 필터 패널이 상태와 제목 문자열을 현지화합니다. 모델 제목, 상태, 초안, 활성화됨 및 비활성화됨 과 같은 번역되지 않은 레이블이 사용자에게 더 이상 표시되지 않습니다. (SITES-30863)

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6525} -->

#### ContextHub{#sites-contexthub-6525}

이제 ContextHub가 JavaScript 오류 없이 로드되어 개인화가 중단되었습니다. 티저 및 기타 개인화된 경험은 영향을 받는 페이지에서 올바르게 렌더링될 수 있습니다. (SITES-38430)

<!-- #### Core Backend{#sites-core-backend-6525} -->

#### 핵심 구성 요소{#sites-core-components-6525}

* 요청이 누락된 DAM 리소스를 타깃팅할 때 AEM이 더 이상 반복된 ThumbnailServlet 오류를 생성하지 않습니다. 서블릿은 리디렉션 후 처리를 중지하여 NullPointerException 항목이 오류 로그를 초과하지 않도록 합니다. (SITES-41238)
* AEM은 작성자가 구성 요소 대화 상자를 다시 열 때 필요한 옵션 대화 상자 필드에 더 이상 플래그를 지정하지 않습니다. 이 대화 상자는 실제로 입력이 필요한 필드에 유효성 검사 포커스를 두어 오해의 소지가 있는 탭 수준 오류를 방지합니다. (SITES-40449)

* AEM에는 사이트 및 관련 Cloud Services 구성 요소를 강화하는 몇 가지 배경 보안 수정 사항이 포함되어 있습니다. 이러한 수정 사항을 통해 사이트 간 스크립팅 위험을 줄이고 영향을 받는 작성 경로 전반에서 요청 처리를 개선할 수 있습니다. (SITES-38314)
* 이제 이미지 v3 구성 요소 구성 대화 상자가 페이지 편집기에서 문자열을 현지화합니다. 작성자가 현지화된 인터페이스에서 이미지 구성 요소를 구성할 때 번역되지 않은 레이블이 더 이상 표시되지 않습니다. (SITES-38726)

<!-- #### Campaign integration{#sites-campaign-integration-6525} -->

<!-- #### ContentHub {#sites-contenthub-6525} -->

#### 횡단보도 {#sites-crosswalk-6525}

* 횡단보도는 설치 후 더 이상 별도의 패키지와 구성 설정이 필요하지 않습니다. AEM에는 필요한 번들, 콘텐츠 패키지, 시스템 사용자, 서비스 사용자 매핑 및 기본 제공 패키지의 기능 전환이 포함됩니다. (SITES-41417)
* 이제 횡단보도 워크플로우가 AEM 6.5에서 필요한 cq-wcm-core 지원과 함께 작동합니다. 작성자는 별도의 핵심 번들 업데이트 없이 템플릿 만들기 및 유니버설 편집기 열기 작업을 사용할 수 있습니다. (SITES-37666)

#### 경험 조각{#sites-experiencefragments-6525}

이제 작성자가 경험 조각 변형을 만들고 처음 40개 결과를 스크롤하면 AEM에 올바른 템플릿이 로드됩니다. 템플릿 선택기는 페이지 매김 중에 선택한 경험 조각 경로를 유지합니다. (SITES-41531)

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6525} -->

#### 론치{#sites-launches-6525}

* 이제 사이트 타임라인은 AEM이 론치를 홍보하기 전에 버전을 만들 때 나타나는 메시지를 현지화합니다. 지역화된 인터페이스에서 번역되지 않은 영어 문자열이 더 이상 사용자에게 표시되지 않습니다. (SITES-39157)
* 이제 론치 목록에 템플릿 또는 라이브 카피 상속 없이 생성된 론치에 대한 올바른 설명이 표시됩니다. 사용자는 더 이상 잘못된 재정의 템플릿 레이블을 볼 수 없습니다. (SITES-34229)

<!-- #### Link Checker{#sites-link-checker-6525} -->

#### 현지화{#sites-localization-6525}

* 이제 경험 조각의 텍스트 구성 요소 속성에서 현지화된 레이블을 사용합니다. 서식 메뉴에 단락, 제목, 따옴표 또는 서식 있는 텍스트 선택 항목의 지역화되지 않은 문자열이 더 이상 표시되지 않습니다. (SITES-15091)

* 이제 템플릿 상태 텍스트가 **도구** > **일반** > **템플릿**&#x200B;에서 올바르게 정렬됩니다. 업데이트, 활성화 및 게시된 상태 레이블이 한 가로줄에 나타납니다. (SITES-36797)
* 이제 페이지 이동 대화 상자에 전체 날짜 및 시간 선택 레이블이 표시됩니다. 프랑스어와 같이 현지화된 인터페이스에서 레이블이 더 이상 잘리지 않습니다. (SITES-36795)
* 이제 템플릿 편집기의 Assets 섹션에 번역된 태그 레이블이 표시됩니다. 현지화된 작성 인터페이스는 템플릿 구성 중에 일관된 레이블을 제공합니다. (SITES-33770)
* 이제 템플릿 편집기에서 페이지 정책 설명이 올바르게 렌더링됩니다. 사용자는 스타일 탭에서 잘린 텍스트 없이 전체 기본 CSS 클래스 지침을 읽을 수 있습니다. (SITES-29724)
* 이제 작성자가 구성 요소를 삭제된 템플릿으로 드래그하려고 하면 템플릿 편집기에 현지화된 오류가 표시됩니다. 메시지가 더 이상 번역되지 않은 &quot;처리 중&quot; 문자열로 표시되지 않습니다. (SITES-19313)
* 이제 티저 구성 창의 &quot;Target&quot; 레이블이 현지화된 텍스트와 함께 표시됩니다. 하이퍼링크 섹션은 더 이상 영어가 아닌 로케일로 영어 문자열을 표시하지 않습니다. (SITES-18622)
* 이제 페이지 편집기의 워크플로우 시작 대화 상자에 현지화된 워크플로우 작업 레이블이 표시됩니다. 작성자가 워크플로 옵션에 대해 영어 문자열을 더 이상 보지 않습니다. 옵션에는 승인, 게시, 요청 및 게시 취소 작업이 포함됩니다. (SITES-18103)
* 이제 구분 기호 편집 패널의 상위 드롭다운 메뉴에 잘리지 않고 현지화된 문자열이 표시됩니다. 작성자는 구성 요소를 구성할 때 전체 레이블을 검토할 수 있습니다. (SITES-17480)
* 이제 페이지 편집기에 컨테이너 구성 요소 스타일 메뉴에 &quot;전체 너비&quot; 및 &quot;고정 너비&quot;에 대한 현지화된 레이블이 표시됩니다. 지원되는 로케일을 사용하는 작성자는 더 이상 해당 문자열을 영어로 볼 수 없습니다. (SITES-17478)
* 작성자는 이제 템플릿 콘솔의 탐색 속성 영역에서 전체 도구 설명을 읽을 수 있습니다. UI는 도구 설명을 정렬하고 템플릿 편집 중에 텍스트가 잘리지 않도록 합니다. (SITES-15480)
* 작성자는 이제 참조 측면 패널에서 전체 &quot;Forms 및 템플릿을 사용하는 문서&quot; 레이블을 읽을 수 있습니다. 템플릿 콘솔에서는 더 이상 지원되는 로케일에 대한 문자열을 잘라내지 않습니다. (SITES-13167)
* 이제 참조 보기에서 새로 고침 오류 메시지에 현지화된 텍스트를 사용합니다. AEM에서 참조 목록을 업데이트할 수 없는 경우 작성자가 번역된 메시지를 봅니다. (SITES-13102)
* 이제 양식 유효성 검사가 잘못된 시간 값이 포함된 필드를 식별합니다. 시간 비틀기 모달에는 보다 명확한 오류 메시지가 표시되므로 작성자는 영향을 받는 시간 또는 분 필드를 수정할 수 있습니다. (SITES-10980)
* 이제 템플릿 콘솔에 이미지 선택 대화 상자에 현지화된 Assets 레이블이 표시됩니다. 작성자가 템플릿 속성에서 에셋을 검색할 때 레이블이 올바르게 표시됩니다. (SITES-8113)

#### MSM - Live Copy{#sites-msm-live-copies-6525}

* 이제 라이브 카피 개요는 관계 상태 보기에서 날짜 형식을 현지화합니다. L **라이브 카피 Source 마지막 수정 날짜**, **라이브 카피 마지막 수정 날짜** 및 **마지막 롤아웃 날짜** 필드에는 사용자의 로캘과 일치하는 날짜가 표시됩니다. (SITES-40756)
* 이제 MSM이 푸시-온-수정 이벤트에 대한 자세한 내용을 기록합니다. 추가된 이벤트 정보는 팀이 롤아웃 활동을 추적하고 예기치 않은 페이지 변경의 원인을 식별하는 데 도움이 됩니다. (SITES-38029)

#### 페이지 편집기{#sites-pageeditor-6525}

* 작성자는 이제 대문자나 공백을 포함하는 태그를 만든 후 첫 번째 페이지 속성 저장 시 적용할 수 있습니다. AEM은 동일한 작업 중에 태그를 만들고 페이지 메타데이터에 올바른 값을 기록합니다. (SITES-42550)

* 이제 작성자는 이름에 아포스트로피가 포함된 DAM 폴더에서 콘텐츠 조각을 만들 수 있습니다. AEM은 인코딩된 폴더 경로를 올바르게 처리하며 작성 중에 더 이상 NullPointerException을 트리거하지 않습니다. (SITES-38653)

* 이제 AEM은 페이지 편집기에서 구성된 콘텐츠 조각 구성 요소에 대해 복사 및 붙여넣기 작업을 지원합니다. 구성 요소는 콘텐츠 조각 참조를 유지하므로 작성자는 수동으로 다시 작성하지 않고도 콘텐츠를 복제할 수 있습니다. (SITES-41586)
* 이제 페이지 편집기에 구성 요소 대화 상자에 첫 번째 필드 설명 툴팁이 올바르게 표시됩니다. 긴 설명이 표시되므로 작성자는 툴팁 상단에 있는 텍스트를 손실하지 않고 필드 지침을 검토할 수 있습니다. (SITES-39937)
* 작성자가 이제 HTTP를 통해 AEM을 사용할 때 리치 텍스트 편집기 링크 대화 상자를 열 수 있습니다. 이 수정 사항은 HTTPS를 사용하지 않는 온-프레미스 환경에 대한 링크 편집을 복원합니다. (SITES-39467)

<!-- #### Replication{#sites-replication-6525} -->

<!-- #### Rich Text Editor{#sites-rte-6525} -->

#### 범용 편집기 {#sites-universal-editor-6525}

* 유니버설 편집기는 기본적으로 더 이상 미리보기 모드에서 열리지 않습니다. AEM은 미리 보기 동작을 명시적으로 요청하지 않는 한 사용자를 프로덕션 유니버설 편집기 환경으로 보냅니다. (SITES-37193)
* 이제 Universal Editor가 AEM 개발, 신속한 개발 및 스테이징 환경을 위한 미리보기 모드로 열립니다. 열기 명령은 비프로덕션 인스턴스에 대해 올바른 미리 보기 동작을 사용합니다. (SITES-33839)

### [!DNL Assets] {#assets-6525}

* 이제 내 공유 클라이언트 라이브러리는 공유 에셋 제목 데이터를 페이지 마크업에 추가하기 전에 안전하게 처리합니다. 생성된 공유 페이지는 조작된 에셋 메타데이터를 통해 사용자를 더 이상 스크립트 삽입에 노출하지 않습니다. (ASSETS-60898)

* 이제 Adobe Stock 라이선싱이 Assets 사용자 인터페이스에서 올바르게 작동합니다. AEM이 스톡 에셋 프로필 및 자격 데이터를 로드한 후에도 라이선스 버튼이 더 이상 비활성화된 상태로 유지되지 않습니다. (ASSETS-62610)
* 이제 기본 에셋 만료 알림이 만료에 근접한 날짜를 올바르게 처리합니다. 미리 알림 이메일은 8일 만료로 자산을 건너뛰는 대신 남은 시간이 구성된 임계값에 도달하면 실행됩니다. (ASSETS-57857)

* 이제 AEM Assets은 사용자가 저장된 검색을 선택한 후 키보드 탐색을 복원합니다. 인터페이스를 사용하면 Assets 보기를 새로 고치거나 다시 시작하지 않고도 드롭다운에서 벗어날 수 있습니다. (ASSETS-52061)

* 이제 관리 보기 다운로드 워크플로우는 ZIP 파일 이름을 올바르게 유지합니다. ZIP 에셋을 다운로드하면 더 이상 .zip 확장자가 더블 인 파일 이름이 생성되지 않습니다. (ASSETS-62207)
* 이제 Assets 참조 워크플로가 파일 이름의 공백을 올바르게 처리합니다. 선택한 파일 이름에 하나 이상의 공백이 포함되어 있으면 관련 에셋 업데이트가 더 이상 실패하지 않습니다. (ASSETS-56418)

#### [!DNL Dynamic Media]{#assets-dm-6525}

이제 자막 및 오디오 트랙 드롭다운에 Dynamic Media에서 아랍어가 지원되는 언어로 표시됩니다. 이 업데이트를 통해 사용자는 사용자 지정 해결 방법 없이 아랍어 자막 트랙을 추가할 수 있습니다. (ASSETS-61771)

### [!DNL Forms]{#forms-6525}

* 이제 대화형 통신 미리 보기가 AEM Forms 서비스 팩 6.5.24.0 후에 콘텐츠를 올바르게 로드합니다. 텍스트가 더 이상 공백이 누락된 상태로 느리게 로드되지 않으므로 미리 보기가 작성된 콘텐츠와 일치하고 더 쉽게 읽을 수 있습니다. (FORMS-25346)
* 이제 유효성 검사 패턴을 구성하고 양식을 저장하면 유효성 검사 세부 사항이 적응형 Forms 핵심 구성 요소에 표시됩니다. 패턴은 작성 인터페이스에 계속 표시됩니다. (FORMS-25236)
* 이제 문서 생성이 AEM Forms 6.5 서비스 팩 23 및 AEM Forms 서비스 팩 6.5.24.0 환경에서 중첩된 XDP(Extensible Forms Description Language) 조각을 올바르게 처리합니다. (FORMS-25234)
* 이제 Rhino 엔진을 사용하여 적응형 Forms 서버측 유효성 재검사 중에 양식 조각 외부에 현지화된 텍스트가 올바른 언어로 표시됩니다. 제출 후 텍스트가 더 이상 기본 언어로 되돌려지지 않습니다. (FORMS-25224)
* AEM Forms 서비스 팩 6.5.24.0(으)로 업그레이드한 후 Red Hat Enterprise Linux(RHEL) 8에서 잘못된 명령 오류로 인해 출력 서비스가 더 이상 충돌하지 않습니다. 갑작스러운 서비스 중지 없이 문서 생성 및 양식 출력 처리가 완료되었습니다. (FORMS-25192)
* 이제 초기 인스턴스 수가 0으로 설정되면 적응형 Forms에서 addInstance() 함수를 사용하여 동적으로 추가된 패널 및 컨텐츠가 표시됩니다. (FORMS-25169, FORMS-25124)
* 이제 AEM Forms 서비스 팩 6.5.24.0(으)로 업그레이드한 후 중국어 번체(홍콩)가 작성자 및 게시 환경에 올바르게 표시됩니다. 현지화된 zh-HK 콘텐츠가 더 이상 잘못된 언어로 표시되지 않거나 예기치 않게 기본 문자열로 대체됩니다. (FORMS-25042)
* 이제 적응형 Forms의 스크리블 서명 필드에서 키보드 탐색이 양식을 탭 처리하는 동안 포커스를 서명 영역 안과 밖으로 일관되게 이동합니다. (FORMS-25011)
* 이제 구성 및 업데이트 작업 중에 웹 서비스 호출 단계에서 WSDL(웹 서비스 설명 언어) 파일이 올바르게 로드됩니다. (FORMS-24992, FORMS-24789, FORMS-24188)
* 이제 텍스트 조각에 조건을 적용할 때 편지 초안에는 줄바꿈이 유지됩니다. 여러 줄 컨텐츠가 더 이상 하나의 연속 줄로 표시되지 않습니다. (FORMS-24602)
* Adobe Sign 단계에 도달한 후 서명 상태 응답이 반환되지 않으면 AEM Forms on Adobe Managed Services(AMS)의 Adobe Sign 워크플로가 더 이상 중단되지 않습니다. (FORMS-24514)
* HTML에서 Portable Document Format(PDF)으로 변환하는 작업이 더 크거나 복잡한 변환 작업을 포함하여 AEM Forms 서비스 팩 6.5.24.0에서 더 이상 간헐적으로 시간 초과되지 않습니다. (FORMS-23978)
* 패치 AEMForms-6.5.0-0112를 설치한 후 관리 사용자 인터페이스에서 안전 백업 모드 관리가 올바르게 작동합니다. 옵션을 사용할 수 있는 경우 사용자가 안전 백업 모드를 비활성화하거나 끌 수 있습니다. (FORMS-23976, FORMS-23718)
* 양식 데이터 모델 데이터 소스 검색이 더 이상 실패하거나 검색 결과에 원시 HTML(HyperText Markup Language) 태그를 표시하지 않습니다. 결과는 읽을 수 있는 텍스트를 표시합니다. (FORMS-23875)
* 적응형 Forms이 AEM Forms 서비스 팩 6.5.24.0에서 지원되는 핵심 구성 요소 버전을 사용하여 Sites 페이지에 포함되면 이제 사용자 지정 함수가 런타임에 로드됩니다. (FORMS-23802)
* 이제 대화형 통신 숫자 규칙은 업데이트된 Sling Commons JavaScript 개체 표기법(JSON) 라이브러리를 사용하여 구문 분석할 때 값을 올바르게 평가합니다. 숫자 필드는 BigDecimal 구문 분석 변경 사항을 일관되게 처리합니다. (FORMS-23733)
* 이제 버전 6.5.0 이상 릴리스에서 작업할 때 기록 문서 비헤이비어가 일관됩니다. 양식 출력 및 관련 처리가 최신 환경의 예상 동작과 일치합니다. (FORMS-23338)

#### FORMS JEE {#forms-jee-6525}

* org.owasp.eapi.reference.JavaLogFactory 오류에 대한 클래스를 찾을 수 없는 로깅 구성 요소를 로드할 때 응용 프로그램 시작이 더 이상 실패하지 않습니다. 영향을 받는 환경은 서비스를 다시 시작하거나 재구성하지 않고 올바르게 초기화됩니다. (FORMS-25348)
* 서비스 팩 25를 적용하면 시작이 성공적으로 완료됩니다. 초기화가 완료되기 전에 시스템 부트스트랩 프로세스가 더 이상 실패하지 않습니다. (FORMS-25347)
* 이제 코어 CPDF(Portable Document Format) 구성 요소가 실행 중에 예기치 않게 중단되지 않고 Linux 환경에서 올바르게 빌드 및 실행됩니다. (FORMS-25115)
* 바코드 추출 중에 특정 PDF(Portable Document Format) 파일을 처리할 때 DecodingException 오류로 인해 바코드 디코딩이 더 이상 실패하지 않습니다. (FORMS-23534, FORMS-23449)

#### Forms Designer {#forms-designer-6525}

* 이제 버전 6.5에서 ExportData를 사용할 때 ExportData 출력이 양식 데이터와 일치합니다. 내보낸 XML(Extensible Markup Language) 필드는 원래 양식에 표시된 값에 맞게 정렬됩니다. (LC-3922791)
* 이제 출력 서비스에서 AEM Forms 서비스 팩 6.5.22.0에 만든 Portable Document Format(PDF) 파일에 올바른 접근성 태그를 생성합니다. 보조 기술은 요소를 건너뛰지 않고 올바른 순서로 콘텐츠를 읽습니다. (LC-3922756)
* 이제 태깅이 활성화된 Portable Document Format(PDF) 양식을 병합할 때 출력 서비스에 숨겨진 필드 상태나 비활성화된 필드 상태가 올바르게 반영됩니다. (LC-3922708)
* 이제 Workbench의 하단 캡션이 있는 필드에 올바른 태깅을 적용하여 생성된 문서의 일관성과 접근성을 개선합니다. (LC-3922619)
* AEM Forms 서비스 팩 6.5.20.0(으)로 업그레이드한 후에도 양식의 QR 코드는 계속 스캔할 수 있습니다. 표준 스캐너는 생성된 QR 코드를 안정적으로 읽습니다. (LC-3922551)
* 이제 Forms 서비스 렌더링은 서로 다른 서비스 팩에서 동일한 입력을 사용할 때 일관된 출력을 생성합니다. 렌더링된 값은 AEM Forms 서비스 팩 6.5.17.0과(와) AEM Forms 서비스 팩 6.5.18.0 간에 더 이상 다르지 않습니다. (LC-3922461)
* XDP(XML Data Package) 템플릿에서 생성된 PDF/A 문서는 이제 기울어진 정사각형 테두리 스타일을 올바르게 렌더링합니다. 양식 필드 모양이 디자인된 레이아웃과 일치합니다. (LC-3922180)
* 병합된 portable Document Format(PDF) 제출은 이제 모든 섹션의 데이터를 유지합니다. 입력한 값은 병합된 최종 문서에 남아 있습니다. (LC-3922008)
* 변환된 정적 Portable Document Format(PDF) 파일은 더 이상 원본 XDP 템플릿의 단일 링크에서 여러 링크 태그를 생성하지 않습니다. (LC-3921997)
* 이제 AEM Forms에서 제출을 내보내면 내보낸 출력 파일의 모든 필드가 포함됩니다. (LC-3921983)


### 기초 {#foundation-6525}

#### Apache Felix {#foundation-apachefelix-6525}

이제 시작은 Felix 기반 인증을 위해 CredentialsSupport 서비스를 올바르게 연결합니다. 이렇게 하면 AEM 시작 중 토큰 인증에 영향을 줄 수 있는 종속성 오류가 방지됩니다. (GRANITE-63186)

<!-- #### Campaign{#foundation-campaign-6525} -->

<!-- #### Cloud Services{#foundation-cloudservices-6525} -->

<!-- #### Communities {#foundation-communities-6525} -->

<!-- #### Content distribution{#foundation-content-distribution-6525} -->

#### CRX {#foundation-crx-6525}

이제 AEM 6.5 업그레이드 후 CRXDE Lite에서 JSP 파일 편집이 예상대로 작동합니다. CodeMirror 편집기는 JSP 탭을 비워 두지 않고 파일 콘텐츠를 로드합니다. (GRANITE-64333)

<!-- #### Granite{#foundation-granite-6525} -->

<!-- #### Integrations{#foundation-integrations-6525} -->

<!-- #### Jetty{#foundation-jetty-6525} -->

#### 현지화{#foundation-localization-6525}

* 이제 보안 > Trust Store의 인증서 업로드 대화 상자에 지역화된 데이터 형식 레이블이 표시됩니다. 사용자가 인증서를 추가할 때 현지화되지 않은 영어 레이블이 더 이상 표시되지 않습니다. (NPR-43412)

* 이제 KeyStore 만들기 대화 상자에서 취소 단추를 다른 대화 상자 단추에 맞춥니다. 버튼 레이아웃은 일관되게 유지되며 더 이상 정렬에서 벗어나서 이동하지 않습니다. (NPR-43291)
* 이제 **보안** > A **Adobe IMS 구성**&#x200B;의 확인 대화 상자에 지역화된 확인 텍스트가 표시됩니다. 확인 및 삭제 메시지가 더 이상 현지화되지 않은 영어 문자열로 표시되지 않습니다. (NPR-43289)
* 현지화된 UI 레이블이 이제 영향을 받는 대화 상자와 키 저장소 탭에 올바르게 나타납니다. Aria 레이블 값은 번역된 문자열을 사용하고 암호 필드 레이블은 잘리지 않고 표시됩니다. (NPR-43285)
* 이제 새 사용자 만들기 워크플로에 잘못된 문자에 대한 지역화된 유효성 검사 오류가 표시됩니다. 사용자는 현지화되지 않은 IllegalArgumentException 문자열 대신 명확하고 번역된 메시지를 받게 됩니다. (GRANITE-52920)

<!-- #### Oak {#foundation-oak-6525} -->

#### Platform{#foundation-platform-6525}

* 이제 태그 참조 표시 단추에 선택한 태그에 대한 참조 수가 표시됩니다. 이 업데이트는 사용자가 별도의 탐색 없이 태그 사용을 이해하는 데 도움이 됩니다. (CQ-4355509)
* 이제 태그 지정의 이동 대화 상자에 유효성 검사 메시지가 올바르게 배치됩니다. 사용자가 필수 필드가 비어 있는 대화 상자를 제출할 때 오류 텍스트가 더 이상 검색 경로 아이콘을 표시하지 않습니다. (CQ-4353009)

#### 보안{#foundation-security-6525}

이제 AEM은 클라이언트 암호가 포함된 추가 키워드를 허용 목록 합니다. 지원되는 통합이 이러한 클라이언트 암호 이름 지정 패턴을 사용하는 경우 구성 만들기가 더 이상 실패하지 않습니다. (GRANITE-66495)

<!-- #### Sling{#foundation-sling-6525} -->

<!-- #### SPA editor {#foundation-spa-editor-6525} -->

#### 번역{#foundation-translation-6525}

업그레이드 후 번역 프로젝트 상태 카운트가 올바르게 업데이트됩니다. 작성자는 이전 서비스 팩 동작의 오래된 메타데이터에 의존하지 않고 초안, 진행 중 및 전체 값을 검토할 수 있습니다. (NPR-43418)

#### 사용자 인터페이스{#foundation-ui-6525}

* 이제 수동으로 입력한 사이트 콘솔 URL이 의도한 페이지 또는 폴더 경로로 확인됩니다. 콘텐츠 계층은 새로 고침 후 일관되게 유지되며 더 이상 기본 URL로 대체되지 않습니다. (NPR-43688)
* AEM 6.5 LTS SP1 인스턴스를 LTS SP2로 업그레이드한 후에도 Adobe CRX 패키지 관리자 테스트 세트가 더 이상 실패하지 않습니다. 이제 썸네일 목록 서블릿 테스트가 예상대로 완료됩니다. (NPR-43534)

* 이제 각 브라우저를 새로 고친 후 사이트 콘솔 콘텐츠 트리가 지속적으로 로드됩니다. 작성자는 콘텐츠가 존재할 때 더 이상 빈 왼쪽 레일 또는 &quot;항목이 없습니다&quot; 메시지가 표시되지 않습니다. (NPR-43442)

<!-- #### WCM{#foundation-wcm-6525} -->

#### 워크플로{#foundation-workflow-6525}

* 이제 워크플로우 모델 편집기에서 테넌트별 워크플로우 모델 경로를 올바르게 확인합니다. 테넌트 수준 /conf 경로 아래에 워크플로 모델을 저장하는 고객은 해당 모델을 전역 구성 경로로 이동하지 않고 편집할 수 있습니다. (GRANITE-65376)

* 이제 워크플로우 모델 편집기에서 경로 유효성 검사 중에 Windows 파일 경로를 표준화합니다. 작성자는 모델 업데이트를 차단하는 액세스 오류 없이 Windows 서버에서 워크플로 모델을 편집할 수 있습니다. (GRANITE-63692)
* 이제 작업 생성에는 기한 일자에 대한 서버측 유효성 검사가 포함됩니다. 사용자는 시작 날짜 이전에 기한이 있는 작업을 만들 수 없으므로 받은 편지함 작업 데이터의 일관성이 유지됩니다. (CQ-4362253)
* 이제 네임스페이스 만들기가 현지화된 텍스트를 올바르게 처리합니다. 사용자는 제목 필드에 라틴어가 아닌 문자를 입력하고 유효성 검사 오류 없이 네임스페이스를 만들 수 있습니다. (CQ-4355587)

## [!DNL Experience Manager] 6.5.25.0 설치{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.25.0에는 [!DNL Experience Manager] 6.5가 필요합니다. 자세한 지침은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하세요. <!-- UPDATE FOR EACH NEW RELEASE -->
* 서비스 팩은 Adobe [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip)에서 다운로드할 수 있습니다.
* MongoDB 및 여러 인스턴스가 있는 배포에서 패키지 관리자를 사용하여 작성자 인스턴스 중 하나에 [!DNL Experience Manager] 6.5.25.0을(를) 설치합니다.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe에서는 [!DNL Experience Manager] 6.5.25.0 패키지를 제거하거나 제거하지 않는 것이 좋습니다. 따라서 팩을 설치하기 전에 `crx-repository`을(를) 롤백해야 하는 경우 백업을 만들어야 합니다. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### [!DNL Experience Manager] 6.5에 서비스 팩 설치{#install-service-pack}

1. 인스턴스가 업데이트 모드에 있는 경우(인스턴스가 이전 버전에서 업데이트된 경우) 설치 전에 인스턴스를 다시 시작하십시오. Adobe은 인스턴스의 현재 가동 시간이 높을 경우 다시 시작할 것을 권장합니다.

1. 설치하기 전에 [!DNL Experience Manager] 인스턴스의 스냅숏 또는 새 백업을 만듭니다.

1. [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip)에서 서비스 팩을 다운로드합니다. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 패키지 관리자를 연 다음 **[!UICONTROL 패키지 업로드]**&#x200B;를 선택하여 패키지를 업로드합니다. 자세한 내용은 [패키지 관리자](/help/sites-administering/package-manager.md)를 참조하세요.

1. 패키지를 선택한 다음 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

1. S3 커넥터를 업데이트하려면 서비스 팩을 설치한 후 인스턴스를 중지하고 기존 커넥터를 설치 폴더에 있는 새 이진 파일로 바꾼 다음 인스턴스를 다시 시작하십시오. [Amazon S3 데이터 저장소](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)를 참조하세요.

>[!NOTE]
>
>패키지 관리자 UI의 대화 상자가 서비스 팩을 설치하는 동안 종료되는 경우가 있습니다. 배포에 액세스하기 전에 오류 로그가 안정될 때까지 기다리는 것이 좋습니다. 업데이터 번들 제거와 관련된 특정 로그를 기다린 후 설치가 성공했는지 확인합니다. 일반적으로 이 문제는 [!DNL Safari] 브라우저에서 발생하지만 모든 브라우저에서 간헐적으로 발생할 수 있습니다.

**자동 설치**

[!DNL Experience Manager] 6.5.25.0.<!-- UPDATE FOR EACH NEW RELEASE -->을(를) 설치하는 데 사용할 수 있는 두 가지 메서드가 있습니다.

* 서버가 온라인 상태일 때 패키지를 `../crx-quickstart/install` 폴더에 넣습니다. 패키지가 자동으로 설치됩니다.
* 패키지 관리자에서 [HTTP API 사용](/help/sites-administering/package-manager.md#package-share). 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

>[!NOTE]
>
>Experience Manager 6.5.25.0은(는) Bootstrap 설치를 지원하지 않습니다. <!-- UPDATE FOR EACH NEW RELEASE -->

**설치 확인**

이 릴리스에서 사용할 수 있는 인증된 플랫폼을 확인하려면 [기술 요구 사항](/help/sites-deploying/technical-requirements.md)을 참조하세요.

1. 제품 정보 페이지(`/system/console/productinfo`)에는 [!UICONTROL 설치된 제품]에 업데이트된 버전 문자열 `Adobe Experience Manager (6.5.25.0)`이(가) 표시됩니다. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 모든 OSGI 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]**&#x200B;이거나 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 콘솔 사용: `/system/console/bundles`).

1. OSGi 번들 `org.apache.jackrabbit.oak-core`은(는) 버전 1.22.20 이상입니다(웹 콘솔 사용: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### [!DNL Experience Manager] Forms용 서비스 팩 설치{#install-aem-forms-add-on-package}

Experience Manager Forms에 서비스 팩을 설치하는 방법은 [Experience Manager Forms 서비스 팩 설치 지침](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)을 참조하십시오.

>[!NOTE]
>
>[AEM 6.5 QuickStart](https://experienceleague.adobe.com/ko/docs/experience-manager-65/content/implementing/deploying/deploying/deploy)에서 사용 가능한 적응형 양식 기능은 탐색 및 평가 목적으로만 사용하도록 설계되었습니다. 프로덕션 용도로 사용하려면 적응형 양식 기능에 적절한 라이선싱이 필요하므로 AEM Forms에 대해 유효한 라이선스를 확보해야 합니다.

### Experience Manager 컨텐츠 조각용 GraphQL 인덱스 패키지 설치{#install-aem-graphql-index-add-on-package}

GraphQL을 사용하는 고객은 GraphQL 색인 패키지 1.1.1[&#128279;](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip)에 Experience Manager 콘텐츠 조각을 설치해야 합니다.

이렇게 하면 필요한 인덱스 정의가 실제로 사용하는 기능을 기반으로 추가할 수 있습니다.

이 패키지를 설치하지 않으면 GraphQL 쿼리가 느려지거나 실패할 수 있습니다.

>[!NOTE]
>
>이 패키지는 인스턴스당 한 번만 설치하십시오. 모든 서비스 팩으로 다시 설치할 필요는 없습니다.

### UberJar{#uber-jar}

[!DNL Experience Manager] 6.5.25.0에 대한 UberJar를 [Maven 중앙 저장소](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.25/)에서 사용할 수 있습니다. <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Maven 프로젝트에서 UberJar를 사용하려면 [UberJar 사용 방법](/help/sites-developing/ht-projects-maven.md)을 참조하여 프로젝트 POM에 다음 종속성을 포함하십시오. <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.25</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar 및 기타 관련 아티팩트는 Adobe Public Maven 저장소(`repo.adobe.com`) 대신 Maven Central Repository에서 사용할 수 있습니다. 기본 UberJar 파일의 이름이 `uber-jar-<version>.jar`(으)로 바뀝니다. 따라서 `dependency` 태그에 대한 값으로 `apis`을(를) 가진 `classifier`이(가) 없습니다.



## 더 이상 사용되지 않는 기능과 제거된 기능{#removed-deprecated-features}

AEM 6.5에서 더 이상 사용되지 않거나 제거된 모든 기능에 대한 자세한 목록은 [사용되지 않거나 제거된 기능](/help/release-notes/deprecated-removed-features.md)을 참조하십시오.

### AEM Assets REST API의 콘텐츠 조각 지원 {#cf-support-assets-rest-api}

AEM 6.5 LTS SP2가 콘텐츠 조각 및 모델 관리를 위한 최신 OpenAPI를 제공하므로 AEM Assets REST API의 이전 콘텐츠 조각 지원 엔드포인트는 이제 더 이상 사용되지 않습니다.

Adobe은 서비스 종료 공지가 있을 때까지 이러한 이전 끝점을 계속 사용할 수 있도록 합니다. Adobe에서는 더 이상 사용되지 않는 엔드포인트에 대한 추가 개선 사항을 계획하지 않습니다.

### SPA 편집기 {#spa-editor}

[SPA 편집기](/help/sites-developing/spa-overview.md)는 AEM 6.5의 릴리스 6.5.25부터 새 프로젝트에 대해 더 이상 사용되지 않습니다. SPA 편집기는 기존 프로젝트에 대해 계속 지원되지만 새 프로젝트에 사용해서는 안 됩니다.

AEM에서 Headless 콘텐츠를 관리하기 위한 권장 편집기는 다음과 같습니다.

* 시각적 편집을 위한 [범용 편집기](/help/sites-developing/universal-editor/introduction.md)
* 양식 기반 편집을 위한 [콘텐츠 조각 편집기](/help/sites-developing/universal-editor/introduction.md)

## 알려진 문제{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **Oak 관련**
서비스 팩 13 이상부터 지속성 캐시에 영향을 주는 다음 오류 로그가 나타나기 시작했습니다.

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  또는

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  이 예외를 해결하려면 다음을 수행합니다.

   1. `crx-quickstart/repository/`에서 다음 두 폴더 삭제

      * `cache`
      * `diff-cache`

   1. 서비스 팩을 설치하거나 Experience Manager as a Cloud Service을 다시 시작합니다.
`cache` 및 `diff-cache`의 새 폴더가 자동으로 만들어지고 `error.log`에서 더 이상 `mvstore`과(와) 관련된 예외가 발생하지 않습니다.

* 콘텐츠 모델의 기본 이름을 대신 사용하도록 콘텐츠 모델에 대해 사용자 지정 API 이름을 사용했을 수 있는 GraphQL 쿼리를 업데이트합니다.

* GraphQL 쿼리에서 `fragments` 인덱스 대신 `damAssetLucene` 인덱스를 사용할 수 있습니다. 이 작업으로 인해 GraphQL 쿼리가 실패하거나 실행하는 데 시간이 오래 걸릴 수 있습니다.

  문제를 해결하려면 `/indexRules/dam:Asset/properties` 아래에 다음 두 속성을 포함하도록 `damAssetLucene`을(를) 구성해야 합니다.

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  인덱스 정의를 변경한 후에는 리인덱싱이 필요합니다(`reindex` = `true`).

  이러한 단계 후에는 GraphQL 쿼리가 더 빨리 수행됩니다.

* 콘텐츠 조각, 사이트 또는 페이지를 이동, 삭제 또는 게시하려고 할 때 콘텐츠 조각 참조를 가져올 때 문제가 있습니다. 백그라운드 쿼리가 실패하고 기능이 작동하지 않습니다.
올바른 작업을 위해 인덱스 정의 노드 `/oak:index/damAssetLucene`에 다음 속성을 추가해야 합니다(리인덱싱이 필요하지 않음).

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* [!DNL Experience Manager] 인스턴스를 6.5.0 - 6.5.4에서 Java™ 11의 최신 서비스 팩으로 업그레이드하는 경우 `error.log` 파일에 `RRD4JReporter` 예외가 표시됩니다. 예외를 중지하려면 [!DNL Experience Manager]의 인스턴스를 다시 시작하십시오. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 사용자는 [!DNL Assets]의 계층 구조에서 폴더의 이름을 바꾸고 중첩된 폴더를 [!DNL Brand Portal]에 게시할 수 있습니다. 그러나 루트 폴더가 다시 게시될 때까지 폴더의 제목이 [!DNL Brand Portal]에서 업데이트되지 않습니다.

* [!DNL Experience Manager] 6.5.x.x를 설치하는 동안 다음 오류 및 경고 메시지가 표시될 수 있습니다.
   * &quot;Target Standard API(IMS 인증)를 사용하여 [!DNL Experience Manager]에서 Adobe Target 통합이 구성된 경우 경험 조각을 Target으로 내보내면 잘못된 오퍼 유형이 생성됩니다. Target에서는 &quot;경험 조각&quot;/소스 &quot;Adobe Experience Manager&quot; 유형 대신 &quot;HTML&quot;/소스 &quot;Adobe Target Classic&quot; 유형의 여러 오퍼를 만듭니다.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: `granite/operations/maintenance`에 유지 관리 창이 없습니다.
   * SUM, MAX 및 MIN과 같은 집계 함수를 사용하는 경우 적용형 양식 서버측 유효성 검사가 실패합니다(CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : `granite/operations/maintenance`에 유지 관리 창이 없습니다.
   * 쇼퍼블 배너 뷰어를 통해 자산을 미리 볼 때 Dynamic Media 대화형 이미지의 핫스팟이 표시되지 않습니다.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : 등록 변경이 등록 취소를 완료할 때까지 기다리는 동안 시간이 초과되었습니다.

* AEM 6.5.15부터 `org.apache.servicemix.bundles.rhino` 번들에서 제공한 Rhino JavaScript 엔진에 새로운 호스팅 동작이 있습니다. 엄격 모드(`use strict;`)를 사용하는 스크립트는 올바른 변수를 선언해야 합니다. 그렇지 않으면 실행되지 않고 결국 런타임 오류가 발생합니다.

* 공식 업데이트 패키지를 통해 태그 지정 관련 기본 제공 콘텐츠를 설치하면 `/content/cq:tags` 노드의 언어 속성이 기본값으로 재설정됩니다. 이 작업은 서비스 팩, 보안 서비스 팩, 확장 기능 팩, 누적 기능 팩, 패치 등에 적용됩니다. 따라서 설치하기 전에 속성에서 추가해야 합니다.

### AEM Sites의 알려진 문제 {#known-issues-aem-sites-6525}

큰 조각 트리에 대한 DoS 보호로 인해 콘텐츠 조각-미리보기가 실패합니다. 기본 GraphQL 쿼리 실행기 구성 옵션에 대한 [KB 문서 보기](https://experienceleague.adobe.com/ko/docs/experience-cloud-kcs/kbarticles/ka-23945)&#x200B;(SITES-17934)

### AEM Forms의 알려진 문제 {#known-issues-aem-forms-6525}

* **FORMS-14521** 사용자가 저장된 XML 데이터가 있는 초안 문자를 미리 보려고 하면 일부 특정 문자에 대해 `Loading` 상태로 중단됩니다.
* **FORMS-16603** 대화형 통신 에이전트 UI의 인쇄 미리 보기에서 일부 계산된 값이 올바르게 표시되지 않습니다.
* **FORMS-15681** 인쇄 미리 보기에서 편지를 보면 내용이 바뀌고 일부 공백은 사라지며 특정 문자는 `x`(으)로 바뀝니다.
* **FORMS-15428** Forms 추가 기능을 사용하여 AEM Forms 서비스 팩 20(6.5.20.0)으로 업데이트한 후 자격 증명 기반 인증을 사용하여 레거시 Adobe Analytics Cloud 서비스에 의존하는 구성이 작동하지 않습니다. 이 문제로 인해 분석 규칙이 올바르게 실행되지 못했습니다.
* **FORMS-16557** 대화형 통신 에이전트 UI의 인쇄 미리 보기에서 통화 기호(예: 달러 기호 $)가 모든 필드 값에 대해 일관되지 않게 표시됩니다. 999까지의 값에 대해 표시되지만 1000 이상의 값에 대해서는 누락됩니다.
* **FORMS-16575** 대화형 통신에서 중첩된 레이아웃 조각의 XDP에 대한 수정 내용은 IC 편집기에 반영되지 않습니다.
* **FORMS-21378** SSV(서버측 유효성 검사)를 사용하는 경우 양식 제출이 실패할 수 있습니다. 이 문제가 발생하면 Adobe 지원 센터에 문의하십시오.
* **FORMS-23722** `bindref`을(를) 사용하는 **첨부 파일** 필드가 포함된 양식을 **작업 할당** 단계를 통해 AEM Workflow에 제출하면 첨부 파일이 표시되지 않습니다. 따라서 작업이 받은 편지함에서 열리면 나타나지 않습니다. 파일이 저장소에 올바르게 저장되지만 작업 할당 단계 UI에 첨부 파일이 표시되지 않습니다.
* 적응형 양식이 Sites 페이지에 포함된 경우 **FORMS-23802** 사용자 지정 함수가 미리 보기 또는 게시에서 로드되지 않습니다. 이 문제는 **aem-forms-core-component** 라이브러리 버전이 1.1.76 이전일 때 발생합니다. 로그에 `InvalidFormContainerException: No form container found` 같은 오류가 표시될 수 있습니다. 이 문제를 해결하려면 AEM Forms SP24용 핫픽스를 [다운로드 및 설치](/help/release-notes/aem-forms-hotfix.md)하십시오(AddOn 6.0.1454).

#### 핫픽스에 대한 알려진 문제 사용 가능 {#aem-forms-issues-with-hotfixes}

<!--
>[!NOTE]
>
>Avoid upgrading to Service Pack 6.5.25.0 for issues without an available hotfix. It may lead to unexpected errors. Upgrade to Service Pack 6.5.25.0 only after the required hotfixes are released.
-->

다음 문제에는 다운로드 및 설치에 사용할 수 있는 핫픽스가 있습니다. [핫픽스를 다운로드하여 설치](/help/release-notes/aem-forms-hotfix.md)하여 다음 문제를 해결할 수 있습니다.

* **FORMS-23881** 6.5.23.0 전체 설치 관리자를 사용하여 설정된 AEM Forms JEE 배포에서 호출에서 사용자 지정 XCI 파일이 제공되면 출력 서비스에서 요청을 처리하지 못합니다. 이 문제를 해결하려면 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 포털에서 최신 AEM 6.5.25.0 Forms 서비스 팩을 설치하십시오.
* **FORMS-23789**(JEE의 AEM Forms만 해당): 사용자가 JEE SP24의 AEM Forms에서 Log4j에 문제가 발생하여 엔터프라이즈 고객의 로깅 및 모니터링에 차질이 발생했습니다. 이 문제를 해결하려면 JEE 서비스 팩 6.5.25.0에서 AEM Forms용 핫픽스를 [다운로드하여 설치](/help/release-notes/aem-forms-hotfix.md)하십시오.
* **FORMS-23802** 사용자 지정 함수는 이전 aem-forms-core-component 버전(&lt;1.1.76)의 Sites 페이지에 양식이 있을 때 미리 보기 또는 게시에서 로드되지 않습니다. 이 문제를 해결하려면 SP24용 [AEM Forms AddOn 핫픽스 6.0.1454](/help/release-notes/aem-forms-hotfix.md)을(를) 설치하십시오.
* **FORMS-23789**(JEE의 AEM Forms만 해당): 사용자가 JEE SP24의 AEM Forms에서 Log4j에 문제가 발생하여 엔터프라이즈 고객의 로깅 및 모니터링에 차질이 발생했습니다. 이 문제를 해결하려면 JEE 서비스 팩 6.5.25.0에서 AEM Forms용 핫픽스를 [다운로드하여 설치](/help/release-notes/aem-forms-hotfix.md)하십시오.
* **FORMS-23802** 사용자 지정 함수는 이전 aem-forms-core-component 버전(&lt;1.1.76)의 Sites 페이지에 양식이 있을 때 미리 보기 또는 게시에서 로드되지 않습니다. 이 문제를 해결하려면 SP24용 [AEM Forms AddOn 핫픽스 6.0.1454](/help/release-notes/aem-forms-hotfix.md)을(를) 설치하십시오.
* 이제 AEM Forms에 양식 구성 요소에 대한 Struts 버전을 2.5.33에서 6.x로 업그레이드하는 기능이 포함됩니다. 이 업그레이드는 SP24에 포함되지 않은 이전에 누락된 Struts 변경 사항을 제공합니다. 최신 버전의 Struts에 대한 지원을 추가하기 위해 다운로드하여 설치할 수 있는 [핫픽스](/help/release-notes/aem-forms-hotfix.md)를 통해 지원이 추가되었습니다.
* **FORMS-14926** AEM Forms JEE 서비스 팩 21(6.5.21.0)을 설치한 후 `<AEM_Forms_Installation>/lib/caching/lib` 폴더 아래에서 Geode jar `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)`의 중복 항목을 찾으면 다음 단계를 수행하여 문제를 해결하십시오.

   1. 로케이터가 실행 중인 경우 중지합니다.
   2. AEM 서버를 중지합니다.
   3. `<AEM_Forms_Installation>/lib/caching/lib`(으)로 이동합니다.
   4. `geode-*-1.15.1.2.jar`을(를) 제외한 모든 Geode 패치 파일을 제거합니다. `version 1.15.1.2`이(가) 있는 Geode jar만 있는지 확인합니다.
   5. 관리자 모드에서 명령 프롬프트를 엽니다.
   6. `geode-*-1.15.1.2.jar` 파일을 사용하여 Geode 패치를 설치합니다.

* **FORMS-15256** 사용자가 AEM 6.5 Forms 서비스 팩 18 또는 19에서 서비스 팩 20 또는 21로 업그레이드할 때 JSP 컴파일 오류가 발생했습니다. 이 오류로 인해 적응형 양식을 열거나 만들 수 없습니다. 또한 다른 AEM 인터페이스에 문제가 발생했습니다. 이러한 인터페이스에는 페이지 편집기, AEM Forms UI, 워크플로우 편집기 및 시스템 개요 UI가 포함되었습니다.

  이러한 문제가 발생하면 다음 단계를 수행하여 해결하십시오.
   1. CRXDE의 `/libs/fd/aemforms/install/` 디렉터리로 이동합니다.
   2. 이름이 `com.adobe.granite.ui.commons-5.10.26.jar`인 번들을 삭제합니다.
   3. AEM 서버를 다시 시작합니다.

* **FORMS-23703** `contains` 규칙이 기본값 없이 구성된 경우 적응형 양식에 대한 서버측 유효성 검사가 실패합니다. 최신 버전의 [AEM Forms 6.5.25.0 서비스 팩](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#aem-65-forms-releases)을 설치하여 문제를 해결할 수 있습니다.
* **GRANITE-63681** 기본 시스템 구성은 필요한 키워드 및 정규 표현식 패턴을 차단하므로 양식 데이터 모델 커넥터의 인증이 방지됩니다. 이 문제를 해결하려면 [link](/help/release-notes/aem-forms-hotfix.md)에서 핫픽스를 다운로드하여 설치하십시오.
* **FORMS-23979** PDFG(HTML-to-PDF 전환)에 간헐적인 시간 초과가 발생할 수 있습니다. 이후에 수정 사항이 포함된 SP24용 Forms 추가 기능의 최신 버전이 릴리스되었습니다. 이 문제가 발생하면 환경을 6.5.25.0[&#128279;](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#aem-65-forms-releases)에 대해 최신 릴리스된 Forms 추가 기능으로 업데이트하십시오.
* **FORMS-23717** **AEM Forms6.5.25.0**(으)로 업그레이드한 후 `server.log` 및 `error.log`에 *보안 파서 팩토리 생성 실패* 또는 *보안 특성... 지원되지 않음*&#x200B;과 같은 반복된 WARN 메시지가 표시될 수 있습니다. 로그는 약 **5-10줄/초**(시간당 수백MB) 증가하여 디스크를 채우고 프로덕션 롤아웃을 차단할 수 있습니다.

로그 볼륨을 줄이려면 응용 프로그램 서버 구성에서 또는 JVM 인수 `-Dlogging.level.com.adobe.util.XMLSecurityUtil=ERROR`을(를) 통해 `com.adobe.util.XMLSecurityUtil`의 로깅 수준을 `ERROR`(으)로 설정합니다. 이 기능은 메시지를 숨기기만 하며 근본적인 원인은 해결하지 않습니다.

* **FORMS-23875** 양식 데이터 모델 검색에서 관련 엔터티가 없는 경우에도 UI에 HTML 태그가 표시됩니다. 이 문제를 해결하려면 [링크](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bb-expressionmanager-pkg-10.0.48.zip)에서 핫픽스를 다운로드하여 설치하십시오.

## OSGi 번들 및 콘텐츠 패키지 포함됨{#osgi-bundles-and-content-packages-included}

다음 zip 파일에는 이 [!DNL Experience Manager] 6.5 서비스 팩 릴리스에 포함된 OSGi 번들 및 콘텐츠 패키지를 나열하는 텍스트 문서가 포함되어 있습니다.

* [Experience Manager에 포함된 OSGi 번들 목록 6.5.25.0](/help/release-notes/assets/65250-bundles.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager에 포함된 콘텐츠 패키지 목록 6.5.25.0](/help/release-notes/assets/65250-packages.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->

## 제한된 웹 사이트{#restricted-sites}

이러한 웹 사이트는 고객만 사용할 수 있습니다. 고객이시며 액세스 권한이 필요한 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [Adobe 고객 지원 센터](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience#)에 문의하십시오.

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 제품 페이지](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 설명서](https://experienceleague.adobe.com/ko/docs/experience-manager-65)
>* [Adobe 우선 순위 제품 업데이트 구독](https://www.adobe.com/kr/subscription/priority-product-update.html)



