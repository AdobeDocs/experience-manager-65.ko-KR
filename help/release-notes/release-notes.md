---
title: ' [!DNL Adobe Experience Manager] 6.5 릴리스 정보'
description: ' [!DNL Adobe Experience Manager] 6.5에 대한 릴리스 정보, 새로운 기능, 설치 방법 및 자세한 변경 목록을 찾으십시오.'
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 8cbf7188baf8cc997e0747be366f13c3b6c2c632
workflow-type: tm+mt
source-wordcount: '4590'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager] 6.5 최신 서비스 팩 릴리스 노트 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section. -->

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 버전 | 6.5.23.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2025년 5월 22일 목요일 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 다운로드 URL | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## [!DNL Experience Manager] 6.5.23.0에 포함된 항목 {#what-is-included-in-aem-6523}

[!DNL Experience Manager] 6.5.23.0에는 새로운 기능, 주요 고객 요청 개선 사항 및 버그 수정 사항이 포함되어 있습니다. 또한 2019년 4월 6.5의 최초 출시 이후 발표된 성능, 안정성 및 보안 개선 사항이 포함되어 있습니다. [!DNL Experience Manager] 6.5에서 [이 서비스 팩을 설치](#install)합니다.

<!-- UPDATE FOR EACH NEW RELEASE -->

## 주요 기능 및 개선 사항

<!--### Sites {#sites}

* A () -->

<!--
### [!DNL Assets]

* A ()
-->

### Forms {#forms-sp23}

이번 릴리스의 주요 기능 및 개선 사항은 다음과 같습니다.

* [정적 PDF에서 혼합 텍스트 스타일을 사용하는 액세스 가능한 하이퍼링크](https://helpx.adobe.com/kr/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf): 이제 정적 PDF에서 혼합 텍스트 스타일을 포함하는 하이퍼링크에 액세스 가능한 단일 요소로 태그가 지정됩니다. 이러한 향상된 기능은 태그 트리 구조를 단순화하고, 화면 판독기 탐색을 개선하며, 향상된 접근성 규정 준수를 지원합니다.

* [지원되는 플랫폼 매트릭스를 업데이트했습니다](/help/forms/using/aem-forms-jee-supported-platforms.md)

  최신 버전에서는 지원되는 플랫폼 매트릭스에 대한 업데이트를 도입하여 최신 기술과의 호환성을 보장합니다.

   * IBM Content Manager 클라이언트 8.7

   * MongoDB Enterprise 7.0

   * MySQL 8.4

   * Microsoft® SQL Server 2022

   * Microsoft® SQL Server JDBC 드라이버 12.8

   * Microsoft® Office 2021

   * Red Hat® Enterprise Linux® 9(커널 4.x, 64비트) 



* [파일 첨부 파일 구성 요소 강화](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment): 이제 보안 조치로서 구성 요소가 허용된 파일 형식 검사를 무시하는 수정된 확장자를 가진 파일 제출을 방지합니다. 이러한 파일은 제출 중에 차단되어 유효한 파일 형식만 허용됩니다.

<!--* **Two-Factor authentication with SAML for AdminUI** 

  AdminUI in AEM Forms JEE now supports two-factor authentication using Security Assertion Markup Language (SAML) single sign-on (SSO), providing stronger security and a seamless login experience for administrators, similar to what is available in HTML Workspace. 

#### New GA features in AEM Forms {#ga-aem-forms-sp23}

* A ()

#### New Beta features in AEM Forms {#beta-aem-forms-sp23}
-->

## 서비스 팩 23의 문제가 해결되었습니다. {#fixed-issues}

<!-- 6.5.23.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-6523}

#### 접근성 {#sites-accessibility-6523}

* 이제 AEM 편집기 페이지의 캔버스 섹션에서 전체 키보드 접근성을 지원합니다. 사용자는 마우스로 가리키지 않고 키보드만 사용하여 섹션 제목을 활성화하고 버튼을 편집할 수 있습니다. 이 업데이트는 WCAG 2.1.1을 준수하도록 하며 티저, 이미지, 회전 메뉴, 레이아웃, 시간 비틀기 및 주석 모달과 같은 구성 요소 전반의 사용성을 개선합니다. (SITES-25256) <!-- 6.5 LTS SP1 -->
* 페르소나, 장바구니 또는 포기와 같은 단추를 활성화한 후 키보드 포커스가 예기치 않게 인구 통계학적 도구 모음의 시작으로 재설정되는 AEM 페이지 편집기의 접근성 문제를 해결했습니다. 이제 일관된 키보드 탐색 및 화면 판독기 워크플로우를 지원하기 위해 활성화된 단추에 포커스가 유지됩니다. (SITES-25306)
* AEM 페이지 편집기에서 키보드만 사용하여 여러 대화 상자와 모달(예: 에셋 레일 또는 레이아웃 미리 보기)의 캔버스 요소를 작동할 수 없는 중요한 접근성 문제를 수정했습니다. 모든 대화형 캔버스 요소는 이제 키보드 전용 탐색을 지원하므로 WCAG 2.1 성공 기준 2.1.1(SITE-25256)을 준수합니다
* 만들기 팝업의 인터랙티브 목록 항목이 잘못된 ARIA 역할을 사용하는 사이트 관리 UI의 접근성 문제를 수정했습니다. 링크처럼 동작한 요소에 `role="menuitem"` 대신 `role="listitem"`이(가) 할당되어 ARIA 디자인 패턴을 위반하고 화면 판독기를 혼동했습니다. 업데이트는 모든 목록 구성 요소가 적절한 의미 체계 역할을 따라 향상된 키보드 및 보조 기술 지원을 제공하도록 합니다. (SITES-24493)
* 페이지 제목 및 태그 필드에 대한 접근성 레이블 연결 문제를 수정했습니다. 이제 AEM 인터페이스는 JAWS와 같은 화면 판독기를 사용할 때 액세스 가능성 레이블을 &quot;제목&quot; 및 &quot;페이지 제목&quot; 필드와 올바르게 연결합니다. 이 수정 사항은 적절한 레이블 읽기를 보장하며 페이지 생성, 속성 및 이동 워크플로우에서 ADA 준수를 향상시킵니다. (SITES-27149)
* 권한 대화 상자의 표 식별에 대한 접근성 문제를 수정했습니다. 이제 AEM의 권한 테이블에서는 올바른 ARIA 역할 및 속성을 사용하여 JAWS와 같은 화면 판독기에서 이를 테이블로 제대로 식별하도록 합니다. 이 수정 사항은 접근성 준수를 향상시키고 사용자가 정확한 탐색 및 콘텐츠 공지를 받도록 합니다. (SITES-27140)
* 타임라인의 주석 입력 필드에 대한 시각적 레이블이 누락되는 문제를 해결했습니다. 접근성을 개선하기 위해 타임라인 섹션 아래의 &quot;댓글&quot; 입력 필드에 대한 시각적 레이블이 누락되었습니다. 업데이트를 통해 화면 판독기에서 필드 레이블을 정확하게 알릴 수 있습니다. 이 경험은 모든 사용자, 특히 보조 기술에 의존하는 개인을 위해 양식 탐색 및 제출을 향상시킵니다. (SITES-26903)
* 타임라인 주석에서 줄임표 단추에 대한 키보드 접근성을 수정했습니다. 타임라인 섹션의 주석 옆에 있는 생략 부호(세 점) 단추에 대한 키보드 탐색을 활성화했습니다. 이제 사용자는 tab 키를 사용하여 버튼에 액세스하고 버튼과 상호 작용할 수 있으므로 키보드 전용 탐색에 의존하는 사용자의 접근성을 향상시킵니다. (SITES-26891)
* 선택 대화 상자의 검색 결과에 대한 NVDA/내레이터 공지가 개선되었습니다. NVDA 또는 내레이터와 같은 화면 판독기를 사용할 때 검색 결과가 검색되는지 여부를 알리도록 선택 열기 대화 상자를 업데이트했습니다. 이러한 개선된 기능은 보조 기술에 의존하는 사용자가 시각적 확인이 필요 없이 검색 작업의 결과를 이해하는 데 도움이 됩니다. (SITES-26883)
* 댓글 입력 필드 옆에 있는 줄임표 아이콘에 대한 ARIA 역할을 수정했습니다. 올바른 ARIA 역할을 사용하도록 주석 입력 필드 옆에 있는 생략 부호(세 점) 아이콘을 업데이트하여 화면 판독기에서 요소를 정확하게 식별할 수 있도록 했습니다. 이러한 개선 사항은 접근성 규정 준수를 향상시키며 보조 기술에 의존하는 사용자의 경험을 개선합니다. (SITES-26881)
* Coral UI 구성 요소에서 잘못된 ARIA 속성을 수정했습니다. 모든 ARIA 속성이 유효한 값을 사용하도록 Coral UI 구성 요소를 업데이트하여 접근성 준수를 개선했습니다. 특히 `aria-modal="dialog"`과(와) 같은 잘못된 값이 잘못 할당된 경우가 해결되었습니다. 이 향상된 기능을 통해 화면 판독기에서 대화 상자 요소를 올바르게 해석할 수 있으므로 보조 기술에 의존하는 사용자의 접근성을 향상시킬 수 있습니다. (SITES-26873)
* 리플로우 시나리오에서 아이콘에 대한 가시성 및 도구 설명이 개선되었습니다. **다운로드**, **에셋 재처리** 및 **체크아웃** 아이콘에 대한 도구 설명이 올바르게 표시되도록 리플로우 동작을 개선했습니다. 뷰포트 크기가 조정되거나 브라우저 확대/축소 설정이 변경될 때 아이콘과 해당 레이블이 보이지 않는 접근성 문제에 초점을 맞췄습니다. 이 수정 사항은 리플로우 동안 가시성을 유지하고 적절한 아이콘 설명을 제공하여 저시력 사용자를 지원합니다. (SITES-26871)

#### 관리 사용자 인터페이스{#sites-adminui-6523}

외부화 종단점이 누락되어 유니버설 편집기 URL 서비스 예외가 수정되었습니다. 이제 유니버설 편집기 URL 서비스가 예외를 throw하지 않고 누락된 작성자, 게시 또는 로컬 외부화 끝점을 처리합니다. 일부 외부화 구성이 완료되지 않은 경우에도 관리자 사용자가 페이지 편집기를 열 수 있습니다. (SITES-28877) <!-- LTS -->

#### 클래식 UI{#sites-classicui-6523}

* 클래식 UI 대화 상자에서 버튼을 토글하면 텍스트 영역이 숨겨지고 이후 클릭 시 다시 표시되지 않는 문제가 발생합니다. 이 수정 사항을 사용하면 전환할 때 텍스트 영역이 올바르게 다시 표시되어 예상 동작을 복원하고 다이내믹 대화 상자 워크플로우에 대한 중단을 방지할 수 있습니다. (SITES-30230)
* 서비스 팩 22 업그레이드 후 손상된 클래식 UI 이미지 자산 파인더 기능이 수정되었습니다. 이제 클래식 UI 이미지 자산 파인더가 공백이나 특수 문자를 포함하는 자산 이름을 올바르게 처리합니다. 이 업데이트를 통해 에셋 파인더가 파일 이름을 올바르게 인코딩하여 검색 실패를 방지하고 작성자는 오류 없이 이미지 에셋을 찾아 선택할 수 있습니다. (SITES-29151)

#### [!DNL Content Fragments]{#sites-contentfragments-6523}

* `DeleteVariationIT.testUpdateBasic`에 대한 유효성 검사 테스트 실패를 수정했습니다. 서비스 팩 유효성 검사를 실행하는 동안 `DeleteVariationIT.testUpdateBasic` 테스트가 더 이상 실패하지 않습니다. 이 수정 사항은 JSON 처리 논리에서 누락된 텍스트 매핑 문제를 수정하여 테스트 안정성을 보장하고 불필요한 테스트 중단을 방지합니다. (SITES-28022)
* 이제 AEM은 이미지 에셋에서 잘못된 형식의 XMP 메타데이터로 인한 성능 저하를 방지합니다. 숫자 세그먼트나 정규화되지 않은 구조가 있는 Assets과 같이 잘못되거나 호환되지 않는 XMP 속성 이름이 포함된 는 처리 중에 더 이상 반복된 경고 로그를 트리거하지 않습니다. 시스템은 문제가 있는 메타데이터를 필터링하여 자산 수집 및 유효성 검사를 오류 없이 완료합니다. (SITES-30683) <!-- AEM 6.5 LTS SP1 -->


<!-- #### [!DNL Content Fragments] - Admin{#sites-admin-6523}

* A () -->


#### [!DNL Content Fragments] - 조각 편집기{#sites-fragments-editor-6523}

다른 작성자는 다른 작성자가 체크아웃하더라도 콘텐츠 조각을 게시할 수 있으며, 이는 체크아웃 기능의 의도한 비헤이비어와 상반됩니다. 이 수정 사항으로 인해 콘텐츠 조각을 체크아웃할 때 작성 인터페이스에서 다른 사용자가 게시 버튼을 보거나 사용할 수 없습니다. (SITES-30578) <!-- LTS -->

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6523}

콘텐츠 조각 스키마에서 GraphQL QueryValidationError를 수정했습니다. `cq-dam-cfm-graphql` 번들을 새로 고치면 콘텐츠 조각 참조를 사용할 때 스키마 유효성 검사 오류가 수정됩니다. 이 수정 사항은 패키지 배포 후 수동으로 스키마를 다시 정렬하거나 다시 게시하지 않아도 GraphQL 쿼리가 제대로 작동하도록 합니다. (SITES-27001) <!-- LTS -->


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6523}

* A () -->

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6523}

* A () -->


#### 구성 요소 콘솔{#sites-component-console-6523}

구성 요소 라이브 사용량 페이지 로드 개선 사항. 대규모 데이터 세트를 스크롤할 때 빈 행이 표시되지 않도록 AEM의 &quot;구성 요소 라이브 사용량&quot; 페이지를 최적화합니다. 광범위한 사용 참조가 있는 구성 요소를 로드하는 사용자는 이제 불필요한 간격이나 빈 항목 없이 연속적인 데이터 로드를 경험할 수 있습니다. 이 경험은 구성 요소 사용 보고 전반에 걸쳐 페이지 탐색, 추적 정확도 및 관리 효율성을 개선합니다. (SITES-26454)

#### 핵심 백엔드{#sites-core-backend-6523}

* 잘못된 에셋 이름으로 인한 콘텐츠 파인더 에셋 나열 실패를 수정했습니다. 이제 콘텐츠 파인더가 인코딩할 수 없는 문자가 있는 자산 이름을 올바르게 처리합니다. 문제가 있는 이름의 자산이 발견될 때 페이지 편집기의 자산 목록에 더 이상 실패하거나 예외가 발생하지 않습니다. (SITES-28722)
* `SearchPathLimiter` 구성 요소가 각 호출에 대해 ERROR 수준에서 메시지를 인쇄하여 과도한 로그 항목을 생성하는 문제가 발생했습니다. 이 동작은 서비스 팩 17 이후에 시작되었으며 로그 볼륨이 매우 높아 성능 문제가 발생했습니다. 이 수정 사항으로 로그 수준이 DEBUG로 다운그레이드되어 로그 노이즈가 크게 줄어들고 시스템 모니터링 및 진단 효율성이 향상됩니다. (SITES-29835)
* `ValidationDataServlet`에서 이미지 자산을 처리하는 동안 형식이 잘못된 XMP 메타데이터에서 오류가 발생했습니다. 이 수정 사항은 규정을 준수하는 메타데이터 처리를 보장하며 잘못된 속성의 중복 구문 분석을 방지합니다. (SITE-30683) <!-- LTS -->


<!-- #### Core Components{#sites-core-components-6523}

* A () -->

<!-- #### Campaign integration{#sites-campaign-integration-6523}

* A () -->

<!-- #### Experience Fragments{#sites-experiencefragments-6523}

* A () -->

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6523}

* A () -->


#### 론치{#sites-launches-6523}

* 12월 25일부터 12월 31일 사이의 잘못된 론치 날짜 표시를 수정했습니다. 이제 시작 UI에 올바른 연도가 포함된 12월 25일부터 12월 31일 사이의 날짜가 표시됩니다. 이 수정은 날짜가 더 이상 다음 연도를 잘못 표시하지 않도록 하여 캠페인 계획 및 일정 조정 중에 혼동을 피할 수 있도록 합니다. (SITES-28706)
* 서비스 팩 22 업그레이드 후 손상된 AEM Launch 템플릿을 수정했습니다. 이제 서비스 팩 22 업그레이드 후 AEM Launch 템플릿이 올바르게 로드됩니다. 이 수정 사항은 내부 실행 구성에서 잘못된 데이터를 수정하여 사용자가 오류나 필드 누락 없이 실행을 보고, 편집하고, 만들 수 있도록 합니다. (SITES-28504)


<!-- #### Link Checker{#sites-link-checker-6523}

* A () -->

<!-- #### MSM - Live Copies{#sites-msm-live-copies-6523}

* A () -->


#### 페이지 편집기{#sites-pageeditor-6523}

* 낮은 화면 해상도의 AssetPicker 로드 문제를 해결했습니다. 이제 사용자가 낮은 화면 해상도(1728×1117 이하)로 스크롤할 때 AssetPicker가 자산을 올바르게 로드합니다. 사용자가 스크롤하는 동안 더 이상 에셋이 누락되지 않아 여러 디바이스 중단점에서 에셋 관리가 개선되었습니다. (SITES-28065)
* 페이지 잠금 및 잠금 해제 작업에 대한 화면 판독기 알림 누락 문제를 해결했습니다. 이제 페이지 편집기에서 사용자가 잠금/잠금 해제 단추를 활성화하면 &quot;정보: 페이지가 잠금/잠금 해제되었습니다&quot; 메시지를 올바르게 알립니다. 이 수정 사항을 통해 접근성 준수가 향상되고 페이지 편집 중에 화면 판독기 사용자가 동적 업데이트를 받을 수 있습니다. (SITES-27143)
* AEM 작성의 구성 요소 작업에 대한 키보드 포커스 동작이 개선되었습니다. 구성, 삭제 또는 변환과 같은 작업 후 새로 만들어지거나 선택한 구성 요소에 포커스가 유지되도록 AEM 작성자 도구의 키보드 탐색이 개선되었습니다. 이전에는 포커스가 페이지 상단으로 이동했으므로 접근성 준수 문제가 발생했습니다. 이 업데이트는 키보드 및 보조 기술 사용자의 사용자 경험을 개선합니다. 편집 워크플로우 내에서 논리적 포커스 진행을 유지함으로써 그렇게 됩니다. (SITES-26549)
* 작성자 대화 상자의 탭 탐색이 개선되었습니다. 사용자가 설명 편집 상자에 도달한 후 계속 앞으로 탭할 수 있도록 하여 AEM 작성자 대화 상자의 키보드 탐색을 개선합니다. 이전에는 설명 필드에서 포커스가 트래핑되면 특별한 키 조합을 사용하지 않고 탐색을 더 이상 할 수 없었습니다. 이 업데이트를 통해 사용자는 Tab 키만 사용하여 필드를 원활하게 이동할 수 있으므로 접근성 규정 준수 및 사용자 경험이 향상됩니다. (SITES-26524)
* 사용자가 Launch 제목에 공백을 포함할 수 없는 회귀가 AEM 6.5 서비스 팩 22에 도입되었습니다. 이 수정 사항은 공백을 사용하는 기능을 복원하여 팀이 예상 동작에 맞게 Launch 이름을 보다 유연하게 정의하고 구성할 수 있도록 합니다. (SITES-29414)
* 숨기기/숨기기 취소 작업 후 레이아웃 컨테이너 내의 구성 요소에 대한 크기 조정 문제를 수정했습니다. 이제 페이지 편집기에서 레이아웃 컨테이너를 숨기고 숨김을 취소한 후 열 값을 올바르게 계산합니다. 사용자는 오류 없이 구성 요소의 크기를 조정할 수 있으며 크기 조정 작업 중에 열이 올바르게 표시됩니다. (SITES-28463)
* 페이지 편집기에서 컨텐츠 트리 버튼 위치가 잘못 표시되었습니다. 이제 페이지 편집기는 잘못된 섹션 대신 의도한 &quot;헤드 티저&quot; 대화 상자 아래에 콘텐츠 트리 구성 버튼을 올바르게 배치합니다. 이 수정 사항은 `bottom:0` 대신 `top:0`을(를) 사용하도록 콘텐츠 트리 대화 상자의 CSS를 업데이트하여 올바른 단추 배치를 보장합니다. (SITES-28448)


<!-- #### Replication{#sites-replication-6523}

* A () -->


#### 리치 텍스트 편집기{#sites-rte-6523}

일반 텍스트 붙여넣기 모드로 리치 텍스트 편집기에서 예기치 않은 `<br>`개 태그를 수정했습니다. 이제 일반 텍스트 `defaultPasteMode`을(를) 사용할 때 서식 있는 텍스트 편집기에서 잘라내기 및 붙여넣기 작업을 올바르게 처리합니다. 이 수정 사항으로 인해 사용자가 RTE 필드 내에서 텍스트를 잘라내어 붙여넣을 때 예기치 않은 `<br>` 태그가 삽입되지 않으므로 콘텐츠를 편집하는 동안 깔끔한 서식이 유지됩니다. (SITES-27780)

#### Universal Editor {#sites-universal-editor-6523}

* 쿼리 매개 변수가 포함된 여러 요청이 AEM으로 전송되는 경우 로그인 토큰 쿠키가 제시간에 반환되지 않아 로그인에 실패할 수 있습니다. (SITES-30659) <!-- LTS -->
* SAML 처리기와의 호환성 및 지원을 보장하려면 `Query Token Auth` 처리기가 `SAML Auth` 처리기를 *이전*&#x200B;에 실행되도록 `service.ranking` 속성을 구성해야 합니다. (SITES-29684)

### [!DNL Assets]{#assets-6523}

* ![Assets](/help/assets/assets/Smock_Asset_18_N.svg)**[!UICONTROL Assets ]**을(를) 선택하고**[!UICONTROL  Adobe Stock 검색&#x200B;]**폴더로 이동한 다음 스톡 이미지를 선택한 후 [!DNL AEM] 온-프레미스(6.5.22.0) 탐색 페이지에서 다음 문제가 발생합니다.
   * **[!UICONTROL 라이선스 및 저장]**&#x200B;을 클릭하면 빈 드롭다운이 표시되므로 선택한 스톡 이미지에 라이선스를 부여하고 저장할 수 없습니다.
   * 스톡 이미지를 선택하거나 스톡 페이지 URL을 다시 입력하면 [!DNL AEM] 홈페이지로 리디렉션되어 Adobe Stock 이미지에 액세스할 수 없습니다. (ASSETS-48687)
* [!DNL AEM] On-Premise(6.5.22.0) 탐색 페이지에서 폴더 이름에 `/`이(가) 포함된 경우 폴더를 관리하는 동안 문제가 발생합니다. (ASSETS-46740)
* [!DNL AEM] 6.5의 경우 메모리 사용량이 많아 ![컬렉션](/help/assets/assets/Smock_Collection_18_N.svg)**[!UICONTROL 컬렉션&#x200B;]**보기에서 자산 세부 정보 페이지가 로드되지 않습니다. (ASSETS-46738)
* [!DNL InDesign]을(를) `Day CQ DAM Mime Type OSGI` 서비스로 통합하는 동안 문제가 발생하여 [!DNL InDesign] 파일이 `x-indesign` 대신 `x-adobe-indesign`(으)로 잘못 식별됩니다. (ASSETS-45953)
* [!DNL AEM 6.5.21] 세션 누수가 기본 **[!UICONTROL Brand Portal에 예약된 게시]** 워크플로 단계로 추적되었습니다. (ASSETS-44104)
* 이미지를 처리하고 게시할 때 **[!UICONTROL 메모리 부족(OOM)]** 오류가 [!DNL AEM]에 표시됩니다. 이 문제는 **[!DNL Dam Asset update]** 및 **[!DNL Dynamic Media: Reprocess assets]**&#x200B;과(와) 같이 워크플로우에서 더 이상 사용되지 않는 메서드로 인해 발생했습니다. (ASSETS-43343)
* 제목을 업데이트하는 등의 사소한 변경 작업을 수행한 후 로컬 Sites 인스턴스에서 **[!DNL Connected Assets configuration]**&#x200B;을(를) 다시 열고 다시 저장합니다. 그러면 원격 인스턴스가 로컬 인스턴스와의 연결을 잃게 됩니다. 따라서 로컬 Sites 인스턴스와의 통신을 설정할 수 없습니다. (ASSETS-44484)
* [!DNL AEM 6.5.21]에서 목록 보기의 자산 업로드가 취소되고 두 번째 업로드가 수행되면 [!DNL AEM]에 업로드된 NaN 자산 중 **[!UICONTROL 0개]** 오류가 표시됩니다. (ASSETS-44124)

#### [!DNL Dynamic Media]{#assets-dm-6523}

실패한 스마트 자르기 생성을 식별하기 위해 메타데이터 속성(`jcr:content/metadata/dam:scene7SmartCropStatus`)을 자산에 추가했습니다. 수동 또는 자동화된 워크플로우를 통해 스마트 자르기 문제가 있는 자산을 효율적으로 검색, 필터링 및 재처리할 수 있습니다. (ASSETS-46237)

#### [!DNL Dynamic Media] - 하이브리드 모드 {#assets-dm-hybrid-6523}

##### Dynamic Media - 하이브리드 추가 기능 패키지(AEM 6.5.23 이상)

AEM 6.5 서비스 팩 23부터 Dynamic Media - 하이브리드 모드에 새 추가 기능 패키지를 사용할 수 있습니다. 이 패키지에는 Dynamic Media - 하이브리드 실행 모드와 호환되는 `cq-scene7-imaging` 번들이 포함되어 있습니다.

**키 수정 포함**

오류 없이 복제가 성공해도 `/conf/global/settings/dam/dm/imageserver`의 `catalog.expiration` 매개 변수에 대한 업데이트가 서버 또는 작성자 URL에 반영되지 않는 Dynamic Media - 하이브리드 배포의 문제를 해결했습니다. 업데이트는 CRX/DE, 서버 응답 및 공개 게재 URL 간에 일관된 만료 값을 보장합니다. 결과적으로 캐시 비헤이비어와 이미지 변환의 신뢰성을 향상시킵니다. (ASSETS-44837)

**중요 고려 사항**

* 기본 AEM 6.5.23 이상 설치의 `cq-scene7-imaging` 번들은 Dynamic Media - 하이브리드 실행 모드와 *호환되지 않음*&#x200B;입니다.
* 서비스 팩 23 이상을 설치하면 Dynamic Media - 하이브리드(`-r dynamicmedia` 실행 모드)에 대해 구성된 AEM 인스턴스에서 기존 `cq-scene7-imaging` 번들을 *자동으로 업데이트하지 않습니다*.

**하이브리드 추가 기능 패키지를 설치할 때**

* AEM 6.5.19 또는 이전 버전에서 AEM 6.5.23(또는 이상)으로 직접 업그레이드하는 경우.
* Dynamic Media - 하이브리드 기능 관련 수정 사항이 필요한 경우.
* 새 Dynamic Media - 하이브리드 인스턴스를 AEM 6.5 GA(일반 가용성)에서 서비스 팩 23(이상)으로 직접 배포할 때

**하이브리드 추가 기능 패키지 다운로드**

하이브리드 추가 기능 패키지는 2025년 5월 22일 목요일부터 Adobe 소프트웨어 배포에서 공식 릴리스인 AEM 6.5.23과 함께 공개적으로 사용할 수 있습니다. 사용자는 소프트웨어 배포에서 **AEM 6.5 Dynamic Media 하이브리드 추가 기능 패키지**&#x200B;를 검색하여 찾을 수 있습니다.


<!--### [!DNL Forms]{#forms-6523}


#### Forms Designer 

* When a user exports the data for an XFA-based PDF using the exportDataAPI, the resulting XML shows discrepancies when compared with the XML data exported manually using Acrobat Reader. Values of some fields were missing in the output compared to the output generated from Acrobat Reader. (LC-3922791).  

* On AEM Forms 6.5.22.0, when a user attempts to generate a tagged PDF using the Output Service in Workbench, the resulting PDF contains an extra label tag under the reference tag in the table of content item. (LC-3922756) 

* When a user places field captions with bottom or right alignment in AEM Forms Designer, the tag tree includes only the caption without the corresponding value, leading to incomplete accessibility tagging. (LC-3922619). 

* On upgrading from AEM Forms 6.5 Service Pack 6 to AEM Forms Service Pack 20, the QR codes in generated PDFs become unreadable. The alternative text for the QR codes also fails accessibility testing, affecting screen reader compatibility. (LC-3922551). 

* When a user renders a letter in Agent UI on AEM Forms Service Pack 18, the content fails to display correctly due to the FormService.render() API. (LC-3922461). 

 

#### Forms

* When a user enables "Allow Rich Text for Title" on the root panel in an AEM Forms Adaptive Form, the "Exclude Title from Document of Record" setting on a nested panel incorrectly hides the root panel's title in the auto-generated Document of Record. (FORMS-19696). 

* When a user attempts to assign a custom sling:resourceType to a core component using the aem:afProperties in a JSON schema on an on-premise AEM 6.5 instance, the custom resource type is not applied. (FORMS-19691). 

* When a user submits an Adaptive Form with prefilled attachments using URIs, the form submission fails with a NullPointerException due to missing binary data. (FORMS-19371) (FORMS-19486). 

* When a user uploads a PDF under the 'Forms and Documents' section in AEM 6.5 Forms, the timeline feature stops functioning. (FORMS-19407)(FORMS-19234). 

* When a user uploads files using the out-of-the-box (OOTB) file attachment component in AEM Forms, security vulnerabilities are identified. This leads to potential interception of the submission process by unauthorized entities. (FORMS-19271). 

* When a user configures an out-of-the-box Adaptive Form in AEM Forms to automatically generate a Document of Record (DoR), the "Title" field in Acrobat Reader's Document Properties does not display the captured DoR title, and the form title does not appear by default in place of the filename. (FORMS-19263). 

* When a user opens an Interactive Communication in Agent UI, the prefilled data cannot be completely erased; upon removal, it automatically refills with the same data. (FORMS-19151). 

* When a user previews a date field in the Agent UI, the date unexpectedly changes due to time zone discrepancies between the VM's UTC setting and the system's interpretation of the date. (FORMS-19115). 

* When a user submits a form, file attachments may duplicate leading to multiple uploads of the same file. (FORMS-19045)(FORMS-19051). 

* Adding coordinators to policy sets in AEM 6.5 Document Security fails across both production and lower environments. (FORMS-18603, FORMS-18212, FORMS-19697). 

* When a user clicks the "datepicker-calendar-icon" in desktop mode with an empty field in AEM Forms Service Pack 22, an error occurs due to the undefined _$focusedDate variable, disrupting associated custom scripts. (FORMS-18483)(FORMS-18268). 

* On AEM Forms Service Pack 19 (6.5.19.0), when a customer previews a letter, the 'Amount in words' field fails to display or update number values incorrectly, leading to misalignment and missing spaces in the content. (FORMS-18437, FORMS-17330, FORMS-18209, FORMS-18557, CTG-4150848,FORMS-19614, LC-3922004) 

* When a customer previews a saved letter in AEM Forms 6.5 SP19 on RHEL, the content misaligns, spaces are missing, and unexpected characters like 'x' appear. (FORMS-18422)(FORMS-17641). 

* When a user navigates between tabs in AEM Forms, selecting components on the first tab becomes unresponsive. (FORMS-18345). 

* In AEM Forms 6.5.21.0, when a user converts an HTML file to PDF using the WebToPDF option, the output PDF is missing the header section, including metadata and title tags. (FORMS-18223, FORMS-17835, FORMS-19642, FORMS-18224). 

* In the AEM JEE Process Manager SDK, when a user invokes the retryAction(long actionOid) method, the system incorrectly retries the first action found in the tb_action_instance table. This occurs even when a specific action ID is provided or when the ID is null, resulting in unintended behavior. (FORMS-18187). 

* After updating to SP22, a user encounters issues where the save draft and submission functionalities fail without displaying any error message. (FORMS-18069). 

* In AEM 6.5.21.0, transitioning from XSD-based foundation components to core components prevents the implementation of cross-file references in JSON schemas, impacting Adaptive Forms migration. (FORMS-18065). 

* When a user previews a letter in the Agent UI, the date field shows an incorrect value due to IC time conversion issues. These discrepancies arise from time zone differences between the VM environment and the system's interpretation of time (UTC vs. local time). (FORMS-17988) (FORMS-17248). 

* When a user previews letters using Notice IC templates in AEM Forms, PDF generation times vary significantly, from 1.5 seconds to more than 10 seconds, even on the same server. This inconsistency affects business critical workflows. (FORMS-17951). 

* When a user binds a Scribble Signature object in an Adaptive Form to an XDP using the 'Data Sources' option, changes cannot be saved due to persistent aspect ratio validation errors, even when using valid values. (FORMS-17587). 

* When a user uses a specific XDP with many hidden fields for document fragments, AEM creates CRX nodes with the cm:optional property set to false, which causes the Interactive Communication (IC) submission to fail. (FORMS-17538). 

* On AEM Forms 6.5.19.0, when a customer previews a letter, the numeric box field fails to handle negative values correctly when digit limits for Lead and Frac are defined. This issue occurs due to the use of parseFloat, which treats the minus sign as part of the number. (FORMS-17451). 

* On AEM Forms 6.5, when a letter is previewed, the use of the "*" wildcard in the Adobe.json file is noticed, raising a concern about its purpose and potential modification (FORMS-17317). 

* When a user uses a screen reader on the "Apply for a Fixed Rate Saver joint account", the headings are incorrectly announced as 'clickable', causing accessibility issues. (FORMS-17038). 

* When a form is embedded, the generated iframe is missing a title attribute, leading to an accessibility compliance issue. (FORMS-17010). 

* It is not possible to download a form using the Forms Manager UI without including associated dependencies such as themes and fragments. (FORMS-15811). 

* When a user accesses the form on mobile devices (iOS and Android), the 'next' and 'previous' buttons on the first page are disabled, but the screen reader does not identify them as disabled. (FORMS-15773). 

* When a user saves a large form with fragments and lazy loading enabled, it fails to retrieve drafts, disrupting the workflow. (FORMS-19890, FORMS-19808). 

 

#### Forms JEE 

* When a user reconfigures the database in AEM Forms, the connection fails due to hardcoded parameters. (FORMS-19568, FORMS-17621) 

* When a user sets up AEM 6.5 with MySQL 8.4 using the partial turnkey method, the LiveCycle Configuration Manager (LCM) fails to recognize the required MySQL connector driver during the database connection test, causing the setup to fail. (FORMS-19442). 

* When a user runs LCM with JDBC 12.8.1 on JRE 11 in a JEE environment, the setup fails due to incompatibility issues.(FORMS-19276). 

* When a user opens a task in AEM On-Premise, the system executes the Workspace Start Action Profile instead of the AssignedUserProfile. (FORMS-19065). 

* When a user uses the retryAction(long actionOid) method in the AEM JEE Process Manager, unexpected behavior occurs. (FORMS-18357)(FORMS-18187). 

* On AEM Forms 6.5.21.0, the PDFG conversion fails with the error below: (FORMS-16851)(FORMS-14613).   
 
#### Forms Captcha {#forms-captcha-6523} 

* Improved reCAPTCHA alerting in Adaptive Forms by updating submit error codes to 400. Also, refined log alerts to distinguish between timeouts, expirations, and bot detection failures, enhancing troubleshooting accuracy and system observability. (FORMS-19240) 
* Closed an unclosed `ResourceResolver` instance in `ReCaptchaConfigurationServiceImpl` to prevent potential resource leaks and improve system stability when using reCAPTCHA integrations in AEM Forms. (FORMS-19242) 
* Improved CAPTCHA configuration handling for AEM Forms by ensuring the correct configuration binds to each form when multiple entries exist in the `/conf/global` folder. Prevents unintended use of incorrect CAPTCHA settings when the configuration container is not explicitly selected. (FORMS-19239)-->


<!--
#### XMLFM {#forms-xmlfm-6523}

* A () -->

<!--
#### [!DNL Adaptive Forms] {#adaptive-forms-6523}

* A () -->

<!--
#### [!DNL Forms Designer] {#forms-designer-6523}

* A () -->


### 기초 {#foundation-6523}

* 서비스 팩 21로 업그레이드한 후 텍스트 색상이 검정색이 아닌 흰색으로 표시되는 Coral 경고 배너 문제를 수정했습니다. 올바른 스타일이 적용되어 인터페이스에서 경고 메시지의 적절한 대비와 가독성을 유지할 수 있습니다. (NPR-42359)
* JWT(JSON 웹 토큰) 사용 중단에 맞게 스마트 태그 구성에서 OAuth 통합에 대한 지원을 추가했습니다. 업데이트된 인증 방법을 사용하여 스마트 태그 기능의 지속적인 기능을 보장합니다. (NPR-42296)

#### Apache Felix {#foundation-apachefelix-6523}

개인 키 파일을 CRX의 이진 형식 속성 필드에 업로드할 때 발생하는 NullPointerException을 해결하여 서비스 팩 16을 통해 있던 호환성을 복원했습니다. 서버 오류나 인증서 갱신 프로세스 중단 없이 AEM Managed Services에서 보안 키 파일 업로드 워크플로우를 사용할 수 있습니다. (CQ-4359178)


<!--
#### Campaign{#foundation-campaign-6523}

* A () -->

<!--
#### Cloud Services{#foundation-cloudservices-6523}

* A () -->

<!--
#### Communities {#foundation-communities-6523}

* A () -->

<!--
#### Content distribution{#foundation-content-distribution-6523}

* A () -->

<!--
#### CRX {#foundation-crx-6523}

* A () -->


#### Granite{#foundation-granite-6523}

* 서비스 팩 21로 업그레이드한 후 HTML 페이지를 로드할 때 지연 또는 실패를 발생시킨 Apache Sling 스크립팅 서비스 간의 OSGi 종속성 주기가 해결되었습니다. `SightlyScriptingEngineFactory` 및 관련 구성 요소와 관련된 순환 종속성을 제거하기 위해 내부 서비스 참조를 업데이트하여 스크립팅 엔진의 안정성 및 시작 동작을 개선했습니다. (GRANITE-56808)
* JS 시작 시 Apache Sling의 스크립트 사용 을 업데이트했습니다. 이 스크립트를 사용하면 스레드 경합이 발생하지 않고 게시 서버가 로드 중에 응답하지 않는 위험을 줄일 수 있습니다. 이 변경 사항은 초기 스크립트 해결로 인한 리소스 잠금을 방지하여 트래픽이 많은 시나리오 중에 서버 안정성과 응답 시간을 향상시킵니다. (GRANITE-56611)
* 입력 필드의 자리 표시자가 레이블로 잘못 표시되어 시각적 혼동을 초래하는 AEM Omnisearch의 문제를 수정했습니다. 일관되고 액세스 가능한 양식 동작을 유지하면서 필터 필드 간에 자리 표시자를 적절히 렌더링합니다. (GRANITE-51791)
* 콘텐츠 조각 모델 편집기에서 다중 필드 참조가 있는 30개 이상의 CFM(콘텐츠 조각 모델)을 선택할 때 트리거된 서버 오류를 해결했습니다. POST 작업을 지원하도록 필터 제안 구성 요소를 개선했습니다. 이 기능을 사용하면 콘텐츠 조각을 만드는 동안 큰 참조 세트를 적절하게 처리하고 대량 모델 구성의 안정성을 향상시킬 수 있습니다. (GRANITE-57164)
* 확인란 닫기를 클릭할 때 의도하지 않게 상태가 전환된 CFM 문제를 해결했습니다. 클릭 활성화를 확인란 요소로 엄격히 제한하도록 스타일을 업데이트하여 우발적인 사용자 상호 작용을 방지하고 양식 유용성과 접근성을 개선했습니다. (GRANITE-52384)


<!--
#### Integrations{#foundation-integrations-6523}

* A () -->


#### Jetty{#foundation-jetty-6523}

SNI 유효성 검사가 사용자 지정 호스트 헤더와 함께 Dispatcher SSL 구성을 사용하는 AEM 고객에 대해 HTTPS를 통한 API 호출을 차단한 문제를 해결했습니다. Jetty 구성의 일부로 SNI 유효성 검사를 비활성화하는 옵션을 도입하여 `mod_proxy`을(를) 실행할 수 없는 특정 역방향 프록시 설정과의 호환성을 활성화합니다. (NPR-42614)


<!--
#### Localization{#foundation-localization-6523}

* A () -->

<!--
#### Oak {#foundation-oak-6523}

* A () -->


#### Platform{#foundation-platform-6523}

* 태그가 인라인으로 생성되는지 또는 표준 태그 생성 방법을 통해 생성되는지에 관계없이 병합된 태그 값이 자산 간에 항상 올바르게 표시되므로 일관되지 않은 태그 병합 동작이 수정되었습니다. `EN:title` 필드의 잔차 값이 병합된 태그 표시를 재정의하지 못하도록 합니다. (CQ-4358812)
* 태그 편집 대화 상자 내의 태그 값에서 앰퍼샌드 문자의 반복된 인코딩을 수정했습니다. 저장 시마다 추가 &quot;&amp;&quot; 엔티티가 추가되지 않도록 하여 태그 값이 편집 시 깔끔하고 일관되도록 하고 작성된 콘텐츠에 표시 오류가 발생하지 않도록 합니다. (CQ-4359048)
* WebSphere®에서 실행되는 AEM 6.5의 적응형 양식 제출에서 전자 메일을 전송할 수 없는 `ClassCastException` 오류가 해결되었습니다. 이 수정 사항을 통해 `com.sun.mail.handlers.text_plain`과(와) `java.activation.DataContentHandler` 간의 호환성을 보장하고 WebSphere® 환경에서 예상하는 메일 처리기 구성에 맞게 이메일을 성공적으로 전송할 수 있습니다. (NPR-42500)
* 설치에 실패하고 오류 응답이 비어 있을 때 AEM에서 명확한 메시지가 표시되도록 하여 패키지 관리자에서 오류 처리가 개선되었습니다. 이 수정 사항은 자동 오류를 방지하고 패키지 배포 중 더 빠른 디버깅을 지원합니다. (NPR-42375)

<!--
#### Security{#foundation-security-6523}

* A -->

<!--
#### Sling{#foundation-sling-6523}

* A () -->


#### 번역{#foundation-translation-6523}

**언어 사본 업데이트**&#x200B;를 사용하여 워크플로우에서 콘텐츠 조각을 업데이트할 때 트리거되는 NPE(NullPointerException) 문제를 해결했습니다. 이 수정 사항을 사용하면 번역 참조에 연결된 콘텐츠를 편집할 때 워크플로우가 실패 상태로 전환되거나 실행 중인 상태로 유지되지 않습니다. (NPR-42115)

#### 사용자 인터페이스{#foundation-ui-6523}

누락된 `title` 특성을 구성 요소 편집 대화 상자의 Coral UI 대화 상자 단추(예: **완료** 및 **취소**)에 추가하여 접근성을 개선하고 자동 유효성 검사를 활성화합니다. 마크업 렌더링 동안 단추가 예상 속성을 유지하도록 하여 Selenium 기반 UI 테스트의 실패를 방지합니다. (NPR-42412)

#### WCM{#foundation-wcm-6523}

서비스 팩 19 이상 환경에서 **언어 사본 업데이트**&#x200B;를 사용할 때 페이지를 번역 작업에 추가할 수 없는 문제를 해결했습니다. 번역 워크플로가 예상대로 진행되도록 하여 수동 개입 없이 언어 사본 간에 적절한 페이지를 전송할 수 있습니다. (CQ-4357929)

#### 워크플로{#foundation-workflow-6523}

핫픽스 배포 후 `getSegmentId` 메서드가 `null`을(를) 반환하여 워크플로우 처리 중 이메일 트리거가 실패하는 `EmailNotificationServiceProcessor`의 문제를 해결했습니다. 프로세서가 AEM 인스턴스 전반에 걸쳐 이메일 알림 워크플로우를 지원하는 데 필요한 `SegmentInfo` 값을 검색하도록 하여 올바른 세그먼트 ID 확인 논리를 복원합니다. (CQ-4359755)


## [!DNL Experience Manager] 6.5.23.0 설치{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.23.0에는 [!DNL Experience Manager] 6.5가 필요합니다. 자세한 지침은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하십시오. <!-- UPDATE FOR EACH NEW RELEASE -->
* 서비스 팩은 Adobe [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip)에서 다운로드할 수 있습니다.
* MongoDB 및 여러 인스턴스가 있는 배포에서 패키지 관리자를 사용하여 작성자 인스턴스 중 하나에 [!DNL Experience Manager] 6.5.23.0을(를) 설치합니다.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe에서는 [!DNL Experience Manager] 6.5.23.0 패키지를 제거하거나 제거하지 않는 것이 좋습니다. 따라서 팩을 설치하기 전에 `crx-repository`을(를) 롤백해야 하는 경우 백업을 만들어야 합니다. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### [!DNL Experience Manager] 6.5에 서비스 팩 설치{#install-service-pack}

1. 인스턴스가 업데이트 모드에 있는 경우(인스턴스가 이전 버전에서 업데이트된 경우) 설치 전에 인스턴스를 다시 시작하십시오. Adobe은 인스턴스의 현재 가동 시간이 높을 경우 다시 시작할 것을 권장합니다.

1. 설치하기 전에 [!DNL Experience Manager] 인스턴스의 스냅숏 또는 새 백업을 만듭니다.

1. [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip)에서 서비스 자루를 다운로드합니다. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 패키지 관리자를 연 다음 **[!UICONTROL 패키지 업로드]**&#x200B;를 선택하여 패키지를 업로드합니다. 자세한 내용은 [패키지 관리자](/help/sites-administering/package-manager.md)를 참조하세요.

1. 패키지를 선택한 다음 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

1. S3 커넥터를 업데이트하려면 서비스 팩을 설치한 후 인스턴스를 중지하고 기존 커넥터를 설치 폴더에 있는 새 이진 파일로 바꾼 다음 인스턴스를 다시 시작하십시오. [Amazon S3 데이터 저장소](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)를 참조하세요.

>[!NOTE]
>
>패키지 관리자 UI의 대화 상자가 서비스 팩을 설치하는 동안 종료되는 경우가 있습니다. 배포에 액세스하기 전에 오류 로그가 안정될 때까지 기다리는 것이 좋습니다. 업데이터 번들 제거와 관련된 특정 로그를 기다린 후 설치가 성공했는지 확인합니다. 일반적으로 이 문제는 [!DNL Safari] 브라우저에서 발생하지만 모든 브라우저에서 간헐적으로 발생할 수 있습니다.

**자동 설치**

[!DNL Experience Manager] 6.5.23.0.<!-- UPDATE FOR EACH NEW RELEASE -->을(를) 설치하는 데 사용할 수 있는 두 가지 메서드가 있습니다.

* 서버가 온라인 상태일 때 패키지를 `../crx-quickstart/install` 폴더에 넣습니다. 패키지가 자동으로 설치됩니다.
* 패키지 관리자에서 [HTTP API 사용](/help/sites-administering/package-manager.md#package-share). 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

>[!NOTE]
>
>Experience Manager 6.5.23.0은(는) Bootstrap 설치를 지원하지 않습니다. <!-- UPDATE FOR EACH NEW RELEASE -->

**설치 확인**

이 릴리스에서 사용할 수 있는 인증된 플랫폼을 확인하려면 [기술 요구 사항](/help/sites-deploying/technical-requirements.md)을 참조하세요.

1. 제품 정보 페이지(`/system/console/productinfo`)에는 [!UICONTROL 설치된 제품]에 업데이트된 버전 문자열 `Adobe Experience Manager (6.5.23.0)`이(가) 표시됩니다. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 모든 OSGI 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]**&#x200B;이거나 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 콘솔 사용: `/system/console/bundles`).

1. OSGi 번들 `org.apache.jackrabbit.oak-core`은(는) 버전 1.22.20 이상입니다(웹 콘솔 사용: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### [!DNL Experience Manager] Forms용 서비스 팩 설치{#install-aem-forms-add-on-package}

Experience Manager Forms에 서비스 팩을 설치하는 방법은 [Experience Manager Forms 서비스 팩 설치 지침](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)을 참조하십시오.

>[!NOTE]
>
>[AEM 6.5 QuickStart](https://experienceleague.adobe.com/ko/docs/experience-manager-65/content/implementing/deploying/deploying/deploy)에서 사용 가능한 적응형 양식 기능은 탐색 및 평가 목적으로만 사용하도록 설계되었습니다. 프로덕션 용도로 사용하려면 적응형 양식 기능에 적절한 라이선싱이 필요하므로 AEM Forms에 대해 유효한 라이선스를 확보해야 합니다.

### Experience Manager 컨텐츠 조각용 GraphQL 인덱스 패키지 설치{#install-aem-graphql-index-add-on-package}

GraphQL을 사용하는 고객은 GraphQL 색인 패키지 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip)에 [Experience Manager 콘텐츠 조각을 설치해야 합니다.

이렇게 하면 필요한 인덱스 정의가 실제로 사용하는 기능을 기반으로 추가할 수 있습니다.

이 패키지를 설치하지 않으면 GraphQL 쿼리가 느려지거나 실패할 수 있습니다.

>[!NOTE]
>
>이 패키지는 인스턴스당 한 번만 설치하십시오. 모든 서비스 팩으로 다시 설치할 필요는 없습니다.

### UberJar{#uber-jar}

[!DNL Experience Manager] 6.5.23.0에 대한 UberJar를 [Maven 중앙 저장소](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.22/)에서 사용할 수 있습니다. <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Maven 프로젝트에서 UberJar를 사용하려면 [UberJar 사용 방법](/help/sites-developing/ht-projects-maven.md)을 참조하여 프로젝트 POM에 다음 종속성을 포함하십시오. <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.23</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar 및 기타 관련 아티팩트는 Adobe Public Maven 저장소(`repo.adobe.com`) 대신 Maven Central Repository에서 사용할 수 있습니다. 기본 UberJar 파일의 이름이 `uber-jar-<version>.jar`(으)로 바뀝니다. 따라서 `dependency` 태그에 대한 값으로 `apis`을(를) 가진 `classifier`이(가) 없습니다.



## 이제 사용되지 않는 기능과 제거된 기능{#removed-deprecated-features}

AEM 6.5에서 더 이상 사용되지 않거나 제거된 모든 기능에 대한 자세한 목록은 [사용되지 않거나 제거된 기능](/help/release-notes/deprecated-removed-features.md/)을 참조하십시오.

### SPA 편집기 {#spa-editor}

[SPA 편집기](/help/sites-developing/spa-overview.md)는 AEM 6.5의 릴리스 6.5.23부터 새 프로젝트에 대해 더 이상 사용되지 않습니다. SPA 편집기는 기존 프로젝트에 대해 계속 지원되지만 새 프로젝트에 사용해서는 안 됩니다.

AEM에서 Headless 콘텐츠를 관리하기 위한 권장 편집기는 다음과 같습니다.

* 시각적 편집을 위한 [범용 편집기](/help/sites-developing/universal-editor/introduction.md)
* 양식 기반 편집을 위한 [콘텐츠 조각 편집기](/help/sites-developing/universal-editor/introduction.md)

## 알려진 문제{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **AEM 6.5.21-6.5.23 및 AEM 6.5 LTS GA의 JSP 스크립팅 번들 문제**
AEM 6.5.21, 6.5.22, 6.5.23 및 AEM 6.5 LTS GA는 알려진 문제가 포함된 `org.apache.sling.scripting.jsp:2.6.0` 번들과 함께 제공됩니다. 이 문제는 일반적으로 AEM 인스턴스가 많은 동시 요청을 처리할 때 로드가 높은 상태에서 발생합니다.

  이 문제가 발생하면 `org.apache.sling.scripting.jsp:2.6.0`에 대한 참조와 함께 다음 예외 중 하나가 오류 로그에 표시될 수 있습니다.

   * `java.io.IOException: classFile.delete() failed`
   * `java.io.IOException: tmpFile.renameTo(classFile) failed`
   * `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
   * `java.io.FileNotFoundException`

  이 오류가 발생하면 유일한 복구 방법은 AEM 인스턴스를 다시 시작하는 것입니다.

  Adobe 고객 지원 센터에 문의하여 이 릴리스 노트를 참조하여 문제를 해결하십시오.

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

* 콘텐츠 조각, 사이트 또는 페이지를 이동, 삭제 또는 게시하려고 할 때 콘텐츠 조각 참조를 가져올 때 문제가 있습니다. 백그라운드 쿼리가 실패합니다. 즉, 기능이 작동하지 않습니다.
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

* AEM 6.5.15부터 ```org.apache.servicemix.bundles.rhino``` 번들에서 제공한 Rhino JavaScript 엔진에 새로운 호스팅 동작이 있습니다. 엄격 모드(```use strict;```)를 사용하는 스크립트는 올바른 변수를 선언해야 합니다. 그렇지 않으면 실행되지 않고 결국 런타임 오류가 발생합니다.

* 공식 업데이트 패키지를 통해 태그 지정 관련 기본 제공 콘텐츠를 설치하면 `/content/cq:tags` 노드의 언어 속성이 기본값으로 재설정됩니다. 이 작업은 서비스 팩, 보안 서비스 팩, 확장 기능 팩, 누적 기능 팩, 패치 등에 적용됩니다. 따라서 설치하기 전에 속성에서 추가해야 합니다.

### AEM Sites의 알려진 문제 {#known-issues-aem-sites-6523}

큰 조각 트리에 대한 DoS 보호로 인해 콘텐츠 조각-미리보기가 실패합니다. 기본 GraphQL 쿼리 실행기 구성 옵션에 대한 [KB 문서 보기](https://experienceleague.adobe.com/ko/docs/experience-cloud-kcs/kbarticles/ka-23945)&#x200B;(SITES-17934)

<!--### Known issues for AEM Forms {#known-issues-aem-forms-6523}

* When a customer upgrades from Struts 2.x to 6.x, stricter type checking can cause silent failures—especially when checkbox components return false and are bound to a List *Integer*. This value mismatch must be handled explicitly to avoid deserialization errors.

* If the HTML to PDF conversion fails on a SUSE&reg; Linux&reg; (SLES 15 SP6 onwards) server with the following error:
  
  ```Auto configuration failed 4143511872:error:0E079065:configuration file routines:DEF_LOAD_BIO:missing equal sign:conf_def.c:362:line 57```
  then set the following environment variable and restart the server:
    `OPENSSL_CONF=/etc/ssl`

* After installing AEM Forms JEE Service Pack 21 (6.5.21.0), if you find duplicate entries of Geode jars `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` under the `<AEM_Forms_Installation>/lib/caching/lib` folder (FORMS-14926), perform the following steps to resolve the issue:

  1. Stop the locators, if they are running.
  1. Stop the AEM Server. 
  1. Go to the `<AEM_Forms_Installation>/lib/caching/lib`. 
  1. Remove all the Geode patch files except `geode-*-1.15.1.2.jar`. Confirm that only the Geode jars with `version 1.15.1.2` are present.
  1. Open the command prompt in administrator mode.  
  1. Install the Geode patch using the `geode-*-1.15.1.2.jar` file. 

* If a user tries to preview a draft letter with saved XML data, it gets stuck in `Loading` state for some specific letters. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (FORMS-14521)
  
* After upgrading to AEM Forms Service Pack 6.5.21.0, the `PaperCapture` service fails to perform OCR (Optical Character Recognition) operations on PDFs. The service does not generate output in the form of a PDF or a log file. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (CQDOC-21680)

* When users upgraded from AEM 6.5 Forms Service Pack 18 or 19 to Service Pack 20 or 21, they encountered a JSP compilation error. This error prevented them from opening or creating adaptive forms. It also caused issues with other AEM interfaces. Those interfaces included the Page Editor, AEM Forms UI, Workflow editor, and System Overview UI. (FORMS-15256)

  If you face such an issue, perform the following steps to resolve it:
    1. Navigate to the directory `/libs/fd/aemforms/install/` in CRXDE.
    1. Delete the bundle with the name `com.adobe.granite.ui.commons-5.10.26.jar`.
    1. Restart your AEM Server.

* After updating to AEM Forms Service Pack 20 (6.5.20.0) with the Forms Add-On, configurations relying on the legacy Adobe Analytics Cloud Service using credential-based authentication stop working. This issue prevented analytics rules from executing correctly. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (FORMS-15428)

* When a user updates to AEM Forms Service Pack 20 (6.5.20.0) on the JEE server and generates PDFs using output services, the PDFs render with accessibility issues. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3922112)
* When a user generates Tagged PDFs using the output service on JEE, it shows "Inappropriate structure warning." To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3922038)
* When a form is submitted on AEM Forms JEE, the instances of a repeating XML element are removed from the data. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3922017)
* When a user in a Linux&reg; environment renders an Adaptive Form (on JEE) in HTML, it fails to render properly. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3921957)
* When a user converts an XTG file to PostScript format using the Output Service on AEM Forms JEE, it fails with the error: `AEM_OUT_001_003: Unexpected Exception: PAExecute Failure: XFA_RENDER_FAILURE`. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3921720)
* After upgrading to AEM Forms Service Pack 18 (6.5.18.0) on JEE server, when a user submits a form, it fails to render HTML5 or PDF Forms and XMLFM crashes. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3921718)
* In the Print Preview of the Interactive Communications Agent UI, the currency symbol (such as the dollar sign $) is inconsistently displayed for all field values. It appears for values up to 999 but is missing for values of 1000 and above. (FORMS-16557)
* Any modifications to nested layout fragments' XDP in an Interactive Communication are not reflected in the IC editor. (FORMS-16575)
* In the Print Preview of the Interactive Communications Agent UI, some calculated values are not displayed correctly. (FORMS-16603)
* When the letter is viewed in Print Preview, the content is changed. That is, some spaces disappear, and certain letters are replaced with `x`. (FORMS-15681)
* When a user configures a WebLogic 14c instance, the PDFG service in AEM Forms Service Pack 21 (6.5.21.0) on JEE running on JBoss&reg; fails due to classloader conflicts involving the SLF4J library. The error is displayed as follows (CQDOC-22178):
  
    ```java
    Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
    the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
    @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
    (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
    have different Class objects for the type org/slf4j/ILoggerFactory used in the signature-->

## OSGi 번들 및 콘텐츠 패키지가 포함됨{#osgi-bundles-and-content-packages-included}

다음 텍스트 문서에는 이 [!DNL Experience Manager] 6.5 서비스 팩 릴리스에 포함된 OSGi 번들 및 컨텐츠 패키지 목록이 나와 있습니다.

* [Experience Manager에 포함된 OSGi 번들 목록 6.5.23.0](/help/release-notes/assets/65230-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager에 포함된 콘텐츠 패키지 목록 6.5.23.0](/help/release-notes/assets/65230-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 제한된 웹 사이트{#restricted-sites}

이러한 웹 사이트는 고객만 사용할 수 있습니다. 고객이고 액세스 권한이 필요한 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [Adobe 고객 지원 센터에 문의](https://experienceleague.adobe.com/en/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 제품 페이지](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 설명서](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [Adobe 우선 순위 제품 업데이트 구독](https://www.adobe.com/kr/subscription/priority-product-update.html)
