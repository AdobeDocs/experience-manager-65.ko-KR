---
title: 에 대한 일반 릴리스 노트 [!DNL Adobe Experience Manager] 6.5
description: "[!DNL Adobe Experience Manager] 6.5 노트는 릴리스 정보, 새로운 기능, 설치 방법 및 상세 변경 목록을 설명합니다."
exl-id: b3d4a527-44ca-4eb6-b393-f3e8117cf1a6
source-git-commit: e3caa3e3067cf5e29cfcdf4286047eb346aefa23
workflow-type: tm+mt
source-wordcount: '4697'
ht-degree: 55%

---

# 에 대한 일반 릴리스 노트 [!DNL Adobe Experience Manager] 6.5{#general-release-notes-for-adobe-experience-manager}

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] |
|---|---|
| 버전 | 6.5 |
| 유형 | 주요 릴리스 |
| 일반 공급 일자 | 2019년 4월 8일 |
| 권장 업데이트 | 다음을 참조하십시오 [AEM 최근 업데이트](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=en). |

### 일반 {#trivia}

이 버전의 릴리스 주기 [!DNL Adobe Experience Manager] 2018년 4월 4일에 시작하여 23회에 걸쳐 품질 보증 및 버그 수정을 거쳐 2019년 3월 28일에 종료되었습니다. 이번 릴리스에서 수정된 개선 사항 및 새로운 기능 등 고객 관련 문제의 총 수는 1345개입니다.

[!DNL Adobe Experience Manager] 6.5는 2019년 4월 8일부터 일반적으로 사용할 수 있습니다.

![AEM 6.5 로그인 화면](/help/assets/assets/aem65-login-v4.png)

## 새로운 기능 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5는 [!DNL Adobe Experience Manager] 6.4 코드 베이스입니다. 새롭고 향상된 기능, 주요 고객 수정 사항, 우선 순위가 높은 고객 개선 사항 및 제품 안정화를 위한 일반적인 버그 수정 사항을 제공합니다. 이 호에는 다음의 것도 포함된다. [!DNL Adobe Experience Manager] 6.4 서비스 팩은 SP4까지 릴리스됩니다.

아래 목록은 개요를 제공하며 후속 페이지에는 전체 세부 정보가 나열됩니다.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

플랫폼 [!DNL Adobe Experience Manager] 6.5 OSGi 기반 프레임워크(Apache Sling 및 Apache Felix) 및 Java™ 콘텐츠 저장소의 업데이트된 버전 위에 빌드합니다. Apache Jackrabbit Oak 1.10.2.

빠른 시작은 Eclipse Jetty 9.4.15를 서블릿 엔진으로 사용합니다.

#### Java™ 지원  {#java-support}

* Java™ 11 및 이미 지원되는 Java™ 8에 대한 새로운 지원
* 최적의 성능을 위해 기본 GC 값을 다른 값으로 대체합니다. 자세한 내용은 [설치 및 업데이트](/help/sites-deploying/custom-standalone-install.md) 섹션.
* Java™ 11 및 Java™ 8 유지 관리 업데이트는 Oracle에서 공개적으로 제공되지 않을 경우 AEM 관련 프로젝트에서 고객이 사용할 수 있도록 Adobe에 따라 배포됩니다.

#### Java™ 개발 {#java-development}

* 현재 [Uberjar의 두 버전](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies), 사용 중지로 표시되지 않은 공용 인터페이스가 포함된 권장 버전 및 사용 중지로 표시된 인터페이스가 포함된 버전.

#### 사용자 인터페이스 {#user-interface}

UI의 생산성과 사용 편의성을 향상시키기 위해 UI에 다양한 개선 사항이 적용되었습니다.

* 사용자 및 그룹에 대한 새 권한 관리 UI.
* 이제 열 보기 도 화면에 표시되는 항목만 로드하고 사용자가 스크롤하기 시작할 때만 더 로드합니다. 목록 및 카드 보기는 6.0(6.4에서 개선됨) 이후 이미 수행되었습니다.
* 이제 해당되는 경우 열 보기에 페이지/에셋의 워크플로 상태가 포함됩니다.
* 다음 [모두 선택](/help/sites-authoring/basic-handling.md#select-all) 작업 은 동일한 폴더에 있는 모든 페이지/에셋으로 작업을 빠르게 실행할 수 있는 방법입니다.
* [모두 선택](/help/sites-authoring/basic-handling.md#select-all) 조치는 로드된 페이지/자산이 아니라 모든 페이지/자산에 대해 조치를 시도합니다. 작업이 일괄 작업을 처리하도록 업그레이드되지 않은 경우 경고 대화 상자가 표시됩니다.

>[!CAUTION]
>
>Adobe는 향후 클래식 UI를 개선할 계획이 없습니다. AEM 6.5에는 클래식 UI가 포함되어 있으며 이전 릴리스에서 업그레이드하는 고객은 있는 그대로 사용할 수 있습니다. 클래식 UI는 더 이상 사용되지 않는 동안 완전히 지원됩니다. [자세히 보기](/help/sites-deploying/ui-recommendations.md)

#### 검색 및 색인 지정 {#indexing-and-search}

* Oak에서의 검색이 이제 동적 패싯을 지원합니다. 예를 들어 에셋 검색의 필터 레일은 예상 결과 수를 보여줍니다.
* QueryBuilder가 확장되어 동적 패싯이 있는 결과를 제공합니다.

#### 업그레이드 {#upgrade}

* AEM 6.2, 6.3 및 6.4를 실행하는 고객은 AEM 6.5로 직접 바로 업그레이드할 수 있습니다. 5.x 또는 6.0/6.1을 사용하는 고객 중 현장 업그레이드를 사용하려는 고객은 먼저 6.4로 업그레이드해야 합니다. 그런 다음 6.5로 업그레이드하거나 인스턴스 간에 콘텐츠를 AEM 6.5로 직접 전송하는 방식으로 업그레이드합니다.
* 업그레이드 절차는 대부분 6.5에서 동일하게 유지됩니다.
* 6.4에 도입된 이전 버전과의 호환성 , 업그레이드 복잡성 평가 및 지속 가능한 업그레이드 기능을 계속 지원합니다. 필요한 경우 이러한 영역에 대한 버전별 업데이트가 수행되었습니다.
* 이제 패턴 탐지기 포장이 간소화되었습니다. 사용 가능한 소스 버전에 대해 6.5로의 업그레이드를 평가하는 패키지가 하나 있습니다.
* 업그레이드 절차에 대한 자세한 내용은 [업그레이드 설명서](/help/sites-deploying/upgrade.md).

#### 프로젝트 및 워크플로우 {#projects-and-workflows}

* 6.4에 도입된 새로운 워크플로우 모델 편집기는 복사 및 게시, 워크플로우 단계의 변수 지원 및 개선과 같은 더 많은 작업을 포함하도록 개선되었습니다 `OR` 및 `AND` 분할됩니다.

#### 저장소 {#repository}

* Adobe Experience Manager 6.5의 기반은 업데이트된 버전의 OSGi 기반 프레임워크(Apache Sling 및 Apache Felix) 및 Java™ 콘텐츠 저장소(Apache Jackrabbit Oak 1.10.2) 위에 구축됩니다.
* 해결된 문제에 대한 개요는 를 참조하십시오. [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [아파치 잭래빗 오크 Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) 및 [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt).

>[!CAUTION]
>
>AEM 6.3 이후 제공되는 Oak 세그먼트 Tar의 새 버전에는 저장소 마이그레이션이 필요합니다. 이전 버전의 TarMK에서 업그레이드하거나 다른 유형의 지속성에서 새 Segment Tar를 전환하려는 경우에는 이 단계가 필수입니다. 새 세그먼트 Tar의 이점에 대한 자세한 내용은 [Oak 세그먼트 Tar로 마이그레이션 FAQ](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).

#### OSGI {#osgi}

* OSGi Promises 및 Converter 유틸리티 라이브러리가 추가됨.

#### 보안 {#security}

* 관리자용 암호 만료가 추가되었습니다.

#### 웹 서버 {#web-server}

* 빠른 시작 배포는 Eclipse Jetty 9.4.15를 서블릿 엔진으로 사용합니다(AEM 6.4는 9.3.22와 함께 제공됨).

### [!DNL Experience Manager] Sites {#experience-manager-sites}

#### 관리된 단일 페이지 앱 {#managed-single-page-apps}

페이지 편집기는 컨텍스트 내에서 컨텐츠를 편집하고 클라이언트 측 렌더링 환경에서 작성/레이아웃하는 기능을 추가합니다([SPA 편집기](/help/sites-developing/spa-architecture.md)로 알려짐). JavaScript 프레임워크로 구축된 기존 단일 페이지 앱인 React 또는 Angular는 AEM SJ SDK로 확장되어 실무자들이 편집할 수 있습니다.

AEM 6.4 SP2의 일부로 처음 출시되었으며, AEM 6.5에서는 SPA 지원이 다음과 같은 기능을 제공합니다.

* 템플릿 편집기를 사용하여 SPA의 AEM 편집 가능 부분을 편집 및 구성합니다.
* 다중 사이트 관리를 사용하여 국가, 프랜차이즈 또는 흰색 레이블이 지정된 SPA 경험을 만듭니다.

#### 헤드리스 컨텐츠 관리 {#headless-content-management}

AEM은 다양한 형식 및 다양한 스택 수준에서 콘텐츠를 제공할 수 있습니다. 2008년부터 [Sling GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) 및 [POST Servlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html)에서 일부가 도입되었습니다. Content Services([Sling Model Exporter](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=en))가 AEM 6.3에서 도입되었으며, AEM 등록 SDK에서 단일 페이지 앱을 하이드레이팅하는 데 사용되는 방법입니다. [HTTP API for Assets](/help/assets/mac-api-assets.md)은 CRUD API이며, AEM 6.5에서 확장되었습니다.

새로운 HTTP API 기능:

* 추가됨 [에셋용 HTTP API에 대한 콘텐츠 조각 지원](/help/assets/assets-api-content-fragments.md) 조각을 만들고, 업데이트하고, 읽고, 삭제합니다.
* [컨텐츠 조각 목록 코어 구성 요소](https://www.aemcomponents.dev)를 사용하여 Content Services를 통해 컨텐츠 조각 목록을 노출합니다.
* [코어 구성 요소 라이브러리](https://www.aemcomponents.dev)는 각 구성 요소에 대한 기본 Content Services JSON 출력을 표시합니다.

#### 화면 추가 기능 {#screens-add-on}

대화형 키오스크에서 디지털 사이니지에 이르기까지 모든 디지털 디스플레이에서 경험을 효율적으로 디자인, 전달 및 최적화할 수 있습니다.

* 컨텐츠 재사용을 위해 디지털 및 매장 내에서 경험과 컨텐츠를 통합합니다.
* 출시 지원을 통해 작성 및 승인/게시 워크플로우를 간소화합니다.
* SPA 편집기를 사용하여 풍부한 인터랙티브 경험을 편집하고 전달합니다.
* Launches를 사용하여 간판 컨텐츠의 향후 컨텐츠 변경 계획
* 시퀀스 채널의 유료 재생
* Excel 시트와 같은 소스 파일을 사용하여 프로젝트 구조 자동 생성
* 대형 간판 네트워크까지 확장할 수 있는 강력한 온라인 및 오프라인 작업(Smart Sync)으로 미디어 플레이어 지원을 확대합니다.
* 동적 자리 표시자를 사용하여 데이터 트리거된 컨텐츠 위치 또는 구성을 맞춤 설정합니다.
* Adobe Analytics를 AEM Screens Player에 통합하여 인사이트를 제공합니다.

AEM Screens 변경에 대한 자세한 내용은 [AEM Screens 사용자 안내서](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=en)의 릴리스 노트를 참조하십시오.

#### 구성 요소 및 템플릿 개발 {#component-amp-template-development}

* 새 프로젝트에 대한 Maven Project Archetype 18+의 경우 참조 [릴리스 노트의 GitHub](https://github.com/adobe/aem-project-archetype/releases).
* 새 프로젝트의 단일 페이지 App Maven Project Archetype 1.0.6+는 을 참조하십시오. [릴리스 노트의 GitHub](https://github.com/adobe/aem-spa-project-archetype/releases).
* HTL 버전 1.4, 참조 [릴리스 노트의 GitHub](https://github.com/adobe/htl-spec/releases/tag/1.4).

   * 문자열, 배열 및 개체의 &quot;in&quot; 연산자:

      ```html
      ${'a' in 'abc’}
      ${100 in myArray}
      ${'a' in myObject}
      ```

   * data-sly-set을 사용한 변수 선언:
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * 목록 및 반복 제어 매개 변수: begin, step, end:
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * data-sly-unwrap용 식별자:

      ```html
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
      text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
      </div>
      ```

   * 음수 지원

* 코어 구성 요소 2.3.2+의 경우 다음을 참조하십시오. [릴리스 노트의 GitHub](https://github.com/adobe/aem-core-wcm-components/releases).
* 레이아웃 컨테이너 그리드 시스템의 경우 참조 [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid).
* Clientlib Manager: Google Closure Compiler가 JavaScript clientlibs(이전 기본값은 Yahoo YUI)를 축소하고 v20190121 버전으로 Google Closure Compiler를 업데이트했습니다.
* 템플릿 편집기 및 정책

   * JS SDK(SPA 편집기라고도 함)를 사용하는 단일 페이지 앱에 대한 템플릿 생성 및 편집 

* 참조 사이트 We.Retail 4.0, 참조 [릴리스 노트의 GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases).
* 기존 사이트를 업그레이드하여 최신 편집기 기능을 사용할 수 있는 도구는 [GitHub 저장소](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM에는 기존 사용자 정의 코드와의 최대 호환성을 제공하기 위해 jQuery 라이브러리의 버전 1.12.4가 포함됩니다. 알려진 보안 문제를 해결하기 위해 Adobe에서 수정을 완료했습니다.

#### 사이트 관리 {#site-administration}

* [참조](/help/sites-authoring/author-environment-tools.md#references) 레일에는 선택한 페이지를 가리키는 내부 링크를 나열하는 새 섹션이 있습니다. 이 기능은 페이지를 오프라인으로 전환하거나 삭제할 때 어떤 페이지를 오프라인으로 전환하기 전에 조정해야 하는지 확인할 때 유용합니다.
* 다음 [목록 보기](/help/sites-authoring/basic-handling.md#list-view) 에는 페이지가 워크플로우에 있을 때의 상태를 보여 주는 새 워크플로우 열이 있습니다.
* [페이지 속성](/help/sites-authoring/editing-page-properties.md)에서 페이지에 썸네일을 지정할 때(썸네일 탭) 기존 자산을 탐색할 수 있습니다.

#### 페이지 편집기 {#page-editor}

* JS SDK(SPA Editor라고도 함)를 사용하는 React 및 Angular 클라이언트측 구성 요소로 빌드된 단일 페이지 앱 경험을 컨텍스트에서 편집하고 구성할 수 있습니다.
* 스캐폴딩 모드는 페이지에 스캐폴딩 페이지가 구성된 경우에만 표시됩니다.

#### 컨텐츠 조각 및 편집기 {#content-fragments-amp-editor}

* 신규 [주석](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) 일반 주석을 작성하고 텍스트 내에서 주석 확인(타임라인 레일에도 표시)을 위한 콘텐츠 조각 편집기의 레일
* 에서 여러 줄 텍스트 요소의 기본 컨텐츠 유형을 설정하는 기능 [콘텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md) 를 단순 텍스트, 서식 있는 텍스트 또는 Markdown으로 변환
* RTE(전체 화면 뷰)의 텍스트를 선택하여 [주석](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)을 추가
* 참조 레일을 통해 컨텐츠 조각을 나란히 [버전 비교](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions)
* 자산 [보고서 다운로드]는 해당 컨텐츠 조각을 표시
* /api.json를 통해 [Assets HTTP API에 컨텐츠 조각 지원](/help/assets/assets-api-content-fragments.md)을 추가합니다. 콘텐츠 조각의 만들기, 업데이트, 읽기 및 삭제를 위한 API가 있습니다.

#### 경험 조각 {#experience-fragments}

* [경험 조각](/help/sites-authoring/experience-fragments.md)의 색인 생성 기능이 개선했으므로 컨텐츠가 사용 중인 페이지에서 검색됩니다..
* 다음 [Target으로 내보내기](/help/sites-administering/experience-fragments-target.md) 이제 옵션을 사용하여 경험 조각을 JSON(기본값: HTML) 또는 둘 다로 보낼 수 있습니다.

#### 번역 {#translation}

* 프로젝트 마스터를 사용하여 변역 프로젝트 생성 간소화.
* 기본적으로 번역 작업을 승인 상태로 설정하여 번역 프로젝트 실행 간소화.
* 타사 번역 메모리의 변경 사항으로 번역 페이지 업데이트 허용.
* JSON 형식으로 번역 작업 내보내기 허용.
* V3 API를 사용하도록 Microsoft® 번역 통합을 업데이트합니다.

#### Multi-Site Management(MSM) {#multi-site-management-msm}

* PushOnModify를 사용하는 롤아웃 구성의 경우, 불일치 상태를 방지하기 위해 페이지 이동 조작을 효율적으로 처리.
* 라이브 카피 구조 내에 페이지를 만들면 기본적으로 독립 페이지가 만들어집니다.
* JS SDK(SPA 편집기라고도 함)를 사용하는 단일 페이지 앱에서 MSM 기능 사용

#### 론치 {#launches}

* 실행을 위한 신규 검토 및 승인 워크플로우, 승인된 실행 페이지만 프로모션할 수 있는 기능
* 프로모션 단계[ 직후 [실행]을 삭제할 수 있도록 선택하기 위해 UI에 옵션 추가](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

#### 컨텐츠 타깃팅 및 시뮬레이션 {#content-targeting-simulation}

* ContextHub 데이터 계층 및 클라이언트측 규칙 엔진 JavaScript가 기본적으로 jQuery 3을 사용하도록 업데이트되었습니다.

#### AEM 및 Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>현재:
>
>* 전용 `at.js 1.x` AEM 활동 콘솔 내에서 타깃팅 엔진으로 Adobe Target을 사용하는 경우에 이 지원됩니다.
>
>* 모두 `at.js. 1.x` 및 `at.js 2.x` Target에 경험 조각 내보내기를 사용하고 Target 콘솔 내에서 활동을 실행하는 경우에 지원됩니다.


* 이제 Adobe Target 통합에서 Target Standard API를 사용합니다. AEM의 이전 버전에서는 이제 더 이상 사용되지 않는 Target Classic HTTP API를 사용합니다.
* Adobe Target `mbox.js` 버전 63이 포함되어 있습니다. Adobe은 구현을 로 전환할 것을 강력히 권장합니다. `at.js` v1.x
* 이제 `at.js` 버전 1.5.0이 포함되어 있습니다. [Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html)를 사용하여 사이트에 `at.js` v1.x를 프로비저닝할 것을 권장합니다.

#### AEM 및 Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` H.27.5가 포함됩니다. 구현을 `AppMeasurement.js`로 전환할 것을 권장합니다.
* `AppMeasurement.js` v1.8.0이 포함됩니다. Adobe은 다음을 권장합니다. [Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html) 를 사용하여 사이트에 AppMeasurement.js를 프로비저닝할 수 있습니다.

#### AEM 및 Commerce {#aem-commerce}

Commerce Integation Framework 개선 사항은 AEM 6.4 이후 더욱 빠른 릴리스 주기로 제공됩니다. [여기에서 자세한 내용을 확인하십시오](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/magento.html).

#### Communities 추가 기능 {#communities-add-on}

최신 릴리스를 얻으려면 [커뮤니티 배포](/help/communities/deploy-communities.md) 섹션에 자세히 설명되어 있습니다.

##### 커뮤니티 참여에 대한 개선 {#enhancements-to-community-engagement}

**@Mentions 지원**
이제 AEM Communities을 통해 등록된 사용자는 사용자 생성 콘텐츠에서 다른 등록된 멤버를 태그 지정(언급)하여 주의를 끌 수 있습니다. 그런 다음 태그가 지정된(멘션된) 구성원에게 해당 사용자 생성 컨텐츠에 대한 상세 링크와 정보가 제공됩니다. 그러나 사용자는 웹 및 이메일 알림을 사용/사용 안함으로 설정할 수 있습니다.

![@mentions 지원](/help/release-notes/assets/at-mentions.png)

커뮤니티 사용자는 자신의 이름, 성 또는 사용자 이름을 검색할 필요가 없으며, 연락한 사람이 있는지 또는 주의를 기울여야 하는지 확인할 수 있습니다. 또한 UGC 작성자는 문제를 가장 잘 처리하고 입력을 추가할 수 있는 등록된 특정 사용자의 응답을 찾을 수 있습니다.

커뮤니티 관리자는 다음을 수행해야 합니다. **언급 활성화** 커뮤니티 구성 요소에서 등록된 사용자가 해당 구성 요소의 기능을 사용할 수 있도록 합니다.

**그룹 메시징**

등록된 커뮤니티 회원은 그룹 구성원에게 동일한 메시지를 개별적으로 보내는 대신 단일 이메일 작성을 통해 대량으로 메시지를 그룹에게 전송할 수 있습니다. [그룹 메시징](/help/communities/configure-messaging.md)을 허용하려면 [Messaging Operations Service](/help/communities/messaging.md#group-messaging)의 인스턴스를 모두 활성화하십시오.

![그룹 메시지](/help/release-notes/assets/group-messaging.png)

##### 대량 조정 개선 {#enhancements-to-bulk-moderation}

일괄 중재에서 맞춤형 필터

[맞춤형 필터](/help/communities/moderation.md#custom-filters) 는 이제 개발 및 벌크 중재 UI에 추가할 수 있습니다.

A [샘플 프로젝트](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) 태그를 통한 필터링은에서 사용할 수 있습니다 [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter). 이 프로젝트를 기본으로 사용하여 유사한 사용자 지정 필터를 개발할 수 있습니다.

![사용자 지정 필터](/help/release-notes/assets/custom-tag-filter.png)

**대량 조정에서 목록 보기**

사용자 생성 컨텐츠 항목을 표시하기 위해 대량 조정에 개선된 UI가 있는 새 목록 보기가 제공되었습니다.

![목록 보기의 대량 조정](/help/release-notes/assets/list-view-moderation.png)

##### 사이트 및 그룹 관리에 대한 개선 사항 {#enhancements-to-site-and-group-management}

**작성자 측 사이트 및 그룹 관리자**

AEM 6.5 Communities 이상에서는 서로 다른 커뮤니티 사이트 및 그룹/중첩 그룹의 분산된 관리를 허용합니다. 여러 커뮤니티 사이트 및 중첩 그룹을 호스팅하는 조직은 이제 사이트(및 그룹) 작성 시 작성자 측에서 관리자 역할의 구성원을 선택할 수 있습니다.

![사이트 관리자](/help/release-notes/assets/site-admin.png)

사이트 관리자는 계층 구조 레벨에서 그룹을 생성하고 기본 관리자가 될 수 있습니다. 이러한 관리자는 나중에 다른 그룹 관리자가 제거할 수 있습니다. 그룹 관리자는 자신의 그룹 G1을 관리하고 G1 아래에 중첩된 하위 그룹을 생성할 수 있습니다.

##### 지원 기능 개선 {#enhancements-to-enablement}

**SCORM2017.1 지원**

AEM 6.5 Communities 지원 공유 가능한 콘텐츠 개체 참조 모델의 지원 기능 [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) 엔진.

* 지원 구성 요소에 대한 키보드 탐색 지원
* AEM Communities의 지원 구성 요소(예: 카탈로그 및 과정 재생, 할당, 파일 라이브러리)는 향상된 접근성을 위해 키보드 탐색을 지원합니다.

##### 기타 개선 사항 {#other-enhancements}

* Solr 7 지원
* AEM 6.5 커뮤니티는 MSRP 및 DSRP를 설정하는 동안 검색 플랫폼의 Apache Solr 7.0 버전을 지원합니다.

### [!DNL Experience Manager Assets] {#experience-manager-assets}

AEM 6.5에서는 AEM 사용자, DAM 역할 및 연관된 광고 및 마케팅 역할의 생산성을 향상시키기 위해 다음과 같은 기능과 개선 사항이 도입되었습니다.

#### [!DNL Adobe Creative Cloud] 및 광고 워크플로우와 통합 {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager]는 광고 및 마케팅 또는 비즈니스 팀이 밀접하게 협력하는 워크플로우에서 [!DNL Adobe Creative Cloud]와 통합하고 자산을 공유하는 다양한 방법을 제공합니다. [!DNL Experience Manager] 6.5는 통합 과정에서 지속적으로 개선되고 더 많은 기회를 노출하며 기존 방법을 간소화합니다.

의 특정 기능 및 통합 관련 사항을 숙지하고 있어야 합니다. [!DNL Experience Manager] 6.5 - 콘텐츠 속도 사용 사례를 최상으로 지원하는 데 사용할 수 있습니다.

##### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link]는 컨텐츠 작성 프로세스에서 광고 팀과 마케터 간의 협업을 강화합니다. 광고 팀은 친숙한 앱을 종료하지 않고 [!DNL Experience Manager Assets]에 저장된 컨텐츠에 액세스할 수 있습니다. 광고 팀은 [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] 및 [!DNL Adobe InDesign] 앱에서 앱 내 패널을 사용하여 자산을 원활하게 탐색, 검색, 체크아웃 및 체크인할 수 있습니다.

[!DNL Adobe Asset Link]는 [Creative Cloud for Enterprise](https://www.adobe.com/kr/creativecloud/business/enterprise.html) 제품의 일부입니다. [!DNL Experience Manager] 배포의 필수 구성을 포함한 자세한 정보는 [Adobe Asset Link](https://helpx.adobe.com/kr/enterprise/using/adobe-asset-link.html)를 참조하십시오.

![Adobe Photoshop에서 자산 검색](/help/release-notes/assets/asset_search_photoshop.png)

##### [!DNL Adobe Stock] 통합 {#stock}

조직은 [!DNL Experience Manager Assets] 내에서 [!DNL Adobe Stock] 엔터프라이즈 플랜을 사용하여 라이선스가 있는 자산이 귀사의 광고 및 마케팅 프로젝트에 폭넓게 사용 가능한지 확인할 수 있습니다. [!DNL Adobe Stock]의 강력한 DAM 기능을 사용하여 Experience Manager에 저장된 [!DNL Experience Manager] 자산을 빠르게 찾고, 미리 보고, 라이선스를 제공할 수 있습니다.

[!DNL Adobe Stock] 서비스는 디자이너와 기업의 모든 광고 프로젝트를 위해 고품질로 큐레이팅된 로열티가 없는 수백만 장의 사진, 벡터, 일러스트레이션, 비디오, 템플릿 및 3D 자산에 대한 액세스를 제공합니다.

자세한 내용은 [Experience Manager Assets에서 Adobe Stock 에셋 사용](/help/assets/aem-assets-adobe-stock.md).

![Experience Manager Assets 내에서 Adobe Stock 이미지 및 라이선스 미리 보기](/help/release-notes/assets/stock_image_preview_license_options.png)

*그림: [!DNL Experience Manager Assets] 내의 [!DNL Adobe Stock] 이미지 및 라이선스 미리 보기.*

![Experience Manager에서 라이선스가 있는 Adobe Stock 이미지 검색 및 필터링](/help/release-notes/assets/aem-search-filters2.jpg)

*그림: [!DNL Adobe Stock]에서 라이선스가 부여된* 이미지 검색 및 필터링.[!DNL Experience Manager]

##### [!DNL Adobe InDesign]에서 동적 참조  {#dynamic-references-in-indesign}

[!DNL Adobe InDesign] 파일에 사용된 [!DNL Experience Manager Assets]이 동적입니다. 참조된 자산이 저장소에서 이동하면 참조가 자동으로 업데이트됩니다. 자세한 내용은 [조합 자산을 관리하는 방법](/help/assets/managing-linked-subassets.md).

#### Brand Portal 기능 {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal]은 승인된 자산을 외부 공급업체/에이전시 및 내부 비즈니스 사용자가 간편하게 구매하고 효과적으로 제어하며 장치 간에 안전하게 분배할 수 있도록 지원합니다. 자산 공유의 효율성을 향상시키고 자산의 시장 출시 시간을 가속화하며 비준수 사용량 및 무단 액세스의 위함을 방지하는 데 도움이 됩니다.

자세한 내용은 [Brand Portal의 새로운 기능](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=ko-KR).

#### 연결된 에셋 {#connectedassets}

대기업에서는 웹 사이트를 구축하는 데 필요한 인프라를 분배할 수 있습니다. 간혹 웹 사이트 작성 기능과 필수 디지털 자산이 다른 사일로에 상주하는 경우가 있습니다.

[!DNL Experience Manager Sites]는 웹 페이지를 구축하는 기능을 제공하며, [!DNL Experience Manager Assets]은 웹 사이트에 필요한 자산을 제공하는 DAM(디지털 자산 관리) 시스템입니다. [!DNL Experience Manager]는 이제 [!DNL Sites] 및 [!DNL Assets]을 통합하여 위의 사용 사례를 지원합니다. [연결된 자산 기능을 구성하고 사용하는 방법](/help/assets/use-assets-across-connected-assets-instances.md)을 참조하십시오.

![다른 [!DNL Experience Manager] 배포의 [!DNL Sites] 페이지에 있는 [!DNL Experience Manager] 배포의 자산을 드래그합니다.](/help/release-notes/assets/connected-assets-drag-and-drop-only.gif)

*그림: 다른 [!DNL Experience Manager] 배포의 [!DNL Sites] 페이지에 있는 [!DNL Experience Manager] 배포의 자산을 드래그합니다.*

#### Dynamic Media {#dynamic-media}

[!DNL Dynamic Media]는 [!DNL Experience Manager Assets]에서 향상된 리치 미디어 작성 및 전달 기능을 제공하여 몰입 및 맞춤화된 최신 경험을 제공합니다. 고품질의 단일 기본 에셋을 업로드하고 Adobe의 고급 클라우드 렌더링 및 뷰어를 사용하여 모든 표현물의 조합을 제공하여 조직의 미디어 전략을 지원할 수 있습니다.

새로 만들기에 대한 자세한 내용 [!DNL Dynamic Media] 기능, 참조 [Dynamic Media 릴리스 노트](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html).

##### 360 비디오 지원 {#video-support}

에서 직접 360 비디오 파일 관리 [!DNL Experience Manager] 최첨단 뷰어를 사용하여 데스크탑, 모바일 및 VR 헤드셋에 VR 경험을 제공할 수 있습니다. 자세한 내용은 [360 비디오 사용](/help/assets/360-video.md).

##### 사용자 지정 비디오 썸네일 {#custom-video-thumbnails}

비디오 자체 또는 DAM에 저장된 기타 컨텐츠의 프레임을 사용하여 비디오 자산의 썸네일을 사용자 지정할 수 있습니다. 추가 지침은 [비디오 축소판 정보](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

##### 접근성 개선 {#accessibility-enhancements}

이제 [!DNL Dynamic Media] 뷰어에는 Aria 지원, 화면 판독기 및 대체 텍스트와 같은 향상된 액세스 가능성에 대한 지원이 포함되어 있습니다. 자세한 내용은 [뷰어 참조 안내서](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html).

#### 검색 환경 개선 {#experience-enhancement-for-searching}

[!DNL Experience Manager] 6.5에서는 마케터가 검색 결과 페이지에서 원하는 자산을 더 빨리 발견할 수 있습니다. 검색 패싯은 검색 필터를 적용하기 전에도 자산 수로 업데이트됩니다. 필터에 대한 예상 수를 확인하면 사용자가 검색 결과를 효율적으로 탐색할 수 있습니다. 자세한 내용은 [Experience Manager에서 자산 검색](/help/assets/search-assets.md)을 참조하십시오.

![검색 패싯에서 검색 결과를 필터링하지 않고 자산 수를 확인합니다](/help/assets/assets/asset_search_results_in_facets_filters.png)

*그림: 검색 패싯에서 검색 결과를 필터링하지 않고 자산 수 확인.*

#### 유용성 개선 {#usability-enhancement}

이제 폴더 내 또는 검색 결과에서 한 번에 로드된 모든 자산을 선택할 수 있습니다. 여러 자산을 신속하게 관리하는 데 도움이 됩니다. 이 확인란은 시나리오에 표시되는 자산뿐만 아니라 시나리오에 맞는 모든 자산, 즉 검색 결과를 선택합니다. [!DNL Experience Manager] 인터페이스.

![두 선택 옵션을 사용하여 한 번의 클릭으로 모든 자산을 선택합니다.](/help/release-notes/assets/select-all-in-aem-assets.gif)

*그림: 모두 선택 옵션을 사용하여 한 번의 클릭으로 모든 자산 선택.*

#### 메타데이터 개선 사항 {#metadata-enhancements}

[!DNL Assets] 을 사용하면 폴더 속성 페이지에 표시되는 레이아웃 및 메타데이터를 정의하는 자산 폴더에 대한 메타데이터 스키마를 생성할 수 있습니다. 이제 폴더 메타데이터 스키마를 기존 폴더에 할당하거나 폴더를 만들 수 있습니다. 자세한 내용은 [폴더 메타데이터 스키마](/help/assets/metadata-config.md#folder-metadata-schema)를 참조하십시오.

계단식 메타데이터를 지정할 때 형식에 수동으로 입력하는 대신 런타임 시 JSON 파일에서 선택 항목을 로드할 수 있습니다. 자세한 내용은 [계단식 메타데이터](/help/assets/metadata-schemas.md#cascading-metadata).

#### 보고 개선 사항 {#reporting-enhancements}

컨텐츠 조각 및 링크 공유는 지금 다운로드된 보고서에 포함됩니다. 자세한 정보는 [자산 보고서](/help/assets/asset-reports.md)를 참조하십시오.

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM 6.5 Forms은 몇 가지 새로운 기능과 개선 사항을 제공합니다. 주요 내용은 다음과 같습니다.

* 트랜잭션 보고서는 제출된 양식, 처리된 문서 및 렌더링된 문서의 수를 추적할 수 있습니다.
* 인터랙티브 통신에 대한 사용성 개선
* 적응형 양식의 클라우드 기반 디지털 서명
* 적응형 양식 및 대화형 커뮤니케이션을 AEM Sites SPA(단일 페이지 애플리케이션)에 임베드합니다.
* AEM 워크플로우의 변수에 대한 지원
* 인터랙티브 통신에서 데이터 디스플레이 패턴 지원
* 적응형 양식 및 인터랙티브 통신 테이블 분류
* 양식 데이터 모델에서 입력 데이터 검증 자동화

다음을 참조하십시오. [AEM 6.5 Forms의 새로운 기능 및 개선 사항 요약](/help/forms/using/whats-new.md) 새 기능 및 향상된 기능 및 설명서 리소스에 대한 자세한 내용

### [!DNL Experience Manager Livefyre] {#experience-manager-livefyre}

Livefyre를 AEM 6.5 인스턴스와 통합할 수 있습니다. 다음을 참조하십시오 [livefyre를 AEM과 통합하는 방법](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/livefyre.html).

### 고객 중심 개발 사용 {#leverage-customer-focused-development}

Adobe은 사양, 개발 및 테스트 중 개발 프로세스의 모든 단계에 고객이 기여할 수 있도록 하는 고객 중심 개발 모델을 사용하고 있습니다. 이 과정에서 모든 기여 고객 및 파트너에게 감사를 드립니다.

Adobe에는 고객 중심의 버그 해결 및 개선 요청 개발을 위한 수집, 우선 순위 지정 및 추적을 활성화하는 절차 및 프로세스가 있습니다. 다음 [Experience Manager 지원 포털](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) 은 Adobe 개선 및 결함 추적 시스템과 통합됩니다. 고객 질문은 가능한 경우 고객 지원 팀에서 식별하고 해결합니다. R&amp;D로 에스컬레이션하면 모든 고객 정보가 캡처되고 우선 순위 지정 및 보고용으로 사용됩니다. 개발에서 유료 지원, 보증 문제 및 고객 유료 개선 사항에 우선 순위가 부여됩니다.

이러한 우선 순위 지정 프로세스를 통해 750가지 이상의 고객 중심 변경 사항이 AEM 6.5에서 수정되었습니다.

## 릴리스의 일부인 파일 목록 {#list-of-files-that-are-part-of-the-release}

**Foundation**

* 독립형 빠른 시작: `cq-quickstart-6.5.0.jar`.
* 애플리케이션 서버 빠른 시작: `cq-quickstart-6.5.0.war`.
* 다양한 웹 서버 및 플랫폼용 Dispatcher 4.3.2 이상 다음을 참조하십시오 [다운로드 링크](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html)
* Eclipse IDE용 플러그인([자세히 보기 및 다운로드](/help/sites-developing/aem-eclipse.md))

* 괄호 코드 편집기 확장([자세히 보기 및 다운로드](/help/sites-developing/aem-brackets.md))
* Maven/Gradle 종속성([다운로드 링크](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/))

**사이트**

* 쿠어 구성 요소([GitHub 프로젝트](https://github.com/adobe/aem-core-wcm-components))
* We.Retail 참조 구현([자세히 보기](/help/sites-developing/we-retail.md))
* Maven Project Archetypes:

   * 전체 스택 사이트: [GitHub 프로젝트](https://github.com/adobe/aem-project-archetype)
   * React/Angular의 단일 페이지 앱: [GitHub 프로젝트](https://github.com/adobe/aem-spa-project-archetype)

* 다양한 대상 플랫폼에 대한 AEM Screens Players([다운로드](https://download.macromedia.com/screens/))

* 스마트 컨텐츠 언어 모델입니다. 영어가 사전 설치되어 더 많은 언어를 다운로드할 수 있습니다.

   * [독일어](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [스페인어](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [이탈리아어](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [프랑스어](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* 대화 상자 변환 도구 등 AEM 현대화 도구 세트. ([GitHub 프로젝트](https://github.com/adobe/aem-modernize-tools))

**Assets**

* 확장된 PDF Rasterizer 추가 패키지([자세히 보기](/help/assets/aem-pdf-rasterizer.md))
* 확장된 RAW 이미지 지원 추가 패키지([자세히 보기](/help/assets/camera-raw.md))

**양식**

* ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)AEM Forms 기능 패키지[
* [AEM Forms OSGi 클라이언트 SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

## 언어 {#languages}

다음의 언어로 사용자 인터페이스를 사용할 수 있습니다.

* 영어
* 독일어
* 프랑스어
* 스페인어
* 이탈리아어
* 브라질 포르투갈어
* 일본어
* 중국어 간체
* 중국어 번체(제한된 지원)
* 한국어

[!DNL Experience Manager] 6.5에서는 중국어 인코딩 표준을 사용하도록 GB18030-2005 CITS에 대해 인증되었습니다.

## 설치 및 업데이트 {#install-update}

설정 요구 사항은 다음을 참조하십시오. [설치 지침](/help/sites-deploying/custom-standalone-install.md).

자세한 지침은 [업그레이드 설명서](/help/sites-deploying/upgrade.md).

## 지원되는 플랫폼 {#supported-platforms}

의 지원 수준을 포함하여 지원되는 플랫폼에 대한 전체 매트릭스 찾기 [AEM 6.5 기술 요구 사항](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Oracle이 Oracle Java™ SE 제품에 대한 LTS(장기 지원) 모델로 전환되었습니다. Java™ 9 및 10은 Oracle에서 LTS가 아닌 릴리스입니다. 다음을 참조하십시오 [Oracle Java™ SE 지원 로드맵](https://www.oracle.com/technetwork/java/eol-135779.html). Adobe은 Java™의 LTS 릴리스를 지원하여 프로덕션에서 AEM만 실행할 수 있습니다. AEM 6.5에서 Java™ 11을 사용하는 것이 좋습니다.

## 더 이상 사용되지 않는/제거된 기능 {#deprecated-and-removed-features}

Adobe은 제품의 기능을 지속적으로 평가하고 시간이 지남에 따라 기능을 보다 강력한 버전으로 교체하기 위한 계획을 세우거나 향후 기대치 또는 확장에 더 잘 대비하기 위해 선택한 부품을 재구현하기로 합니다.

대상 [!DNL Adobe Experience Manager] 6.5, [더 이상 사용되지 않거나 제거된 기능 목록 읽기](/help/release-notes/deprecated-removed-features.md). 이 페이지에는 향후 변경될 사항에 대한 사전 공지 및 이전 릴리스에서 업데이트되는 고객에 대한 중요 공지 사항이 포함되어 있습니다.

## 알려진 문제 {#known-issues}

### 플랫폼 {#platform}

* CRX-Quickstart와 그 컨텐츠가 삭제되는 문제가 보고됩니다.

   이러한 각 작업에 대해 속성을 확인합니다 `htmllibmanager.fileSystemOutputCacheLocation` 은(는) 빈 문자열이 아닙니다.

   1. 호출 중 `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. AEM 6.5로 업그레이드
   3. AEM 6.5에서 &quot;레이지 컨텐츠 마이그레이션&quot; 실행.

   이 문제에 대한 보다 자세한 내용 및 해결 방법에 대해서는 [기술 자료](https://helpx.adobe.com/kr/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) 문서를 이용할 수 있습니다.

* AEM 6.5 인스턴스에서 JDK 11을 사용하는 경우 일부 패키지를 배포한 후 일부 페이지가 공백으로 표시될 수 있습니다. 로그 파일에 다음 오류 메시지가 표시됩니다.

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

이 오류를 해결하려면

1. AEM 인스턴스를 중지합니다. `<aem_server_path_on_server>crx-quickstart\conf`로 이동하고 `sling.properties` 파일을 엽니다. 이 파일을 백업하는 것이 좋습니다.

1. `org.osgi.framework.bootdelegation=`을 검색합니다. 추가 `jdk.internal.reflect,jdk.internal.reflect.*` 결과를 표시할 속성

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. 파일을 저장하고 AEM 인스턴스를 다시 시작합니다.

### Sites {#sites}

* **페이지 버전 사용**: [페이지가 이동된 경우 이동 전에 만든 버전에서는 더 이상 미리보기를 수행할 수 없습니다](/help/sites-authoring/working-with-page-versions.md#previewing-a-version).

### Assets {#assets}

* **검색:** 검색 문자열에 선행 공백()이 포함된 경우 결과를 검색하지 않습니다.[오크-](https://issues.apache.org/jira/browse/OAK-4786))
* **폴더 메타데이터 스키마**: 선택 버튼을 추가한 후에 ID 및 값 필드가 예상대로 렌더링되지 않고 삭제 기능이 작동하지 않습니다. (CQ-4261144)
* 자산의 이름을 변경할 때 자산 이름에서 공백을 사용할 수 없습니다. (CQ-4266403)

### Forms {#forms}

* AEM Forms이 Linux® 운영 체제에 설치된 경우 하드웨어 보안 모듈의 디지털 서명이 작동하지 않습니다. (CQ-4266721)
* (WebSphere의 AEM Forms® 해당) **Forms Workflow** > **작업 검색** 옵션을 검색해도 결과가 반환되지 않음 **관리자** 포함 **사용자 이름** 을 검색 기준으로 사용합니다. (CQ-4266457)

* AEM Forms에서 JPEG 압축이 있는 TIF 및 TIFF 파일을 PDF 문서로 변환하지 못했습니다. (CQ-4265972)
* **AEM Forms 자산 스캐너** 및 **인터랙티브 커뮤니케이션 마이그레이션 서신** 옵션이 **AEM Forms Migration** 페이지에서 작동하지 않습니다. (CQ-4266572)

* (JBoss® 7만 해당) 이전 버전에서 AEM 6.5 Forms으로 업그레이드하고 이전 버전에는 기본 제출 또는 기본 렌더링 프로세스의 사본을 작성 및 사용한 프로세스(.lca)가 있는 경우, 이러한 프로세스(.lca)를 사용하는 HTML5 Forms은 필수 작업을 수행하지 못합니다. (CQ-4243928)
* 적응형 양식에서 양식 데이터 모델 서비스가 규칙 편집기에서 호출되어 이미지 선택 구성 요소 값을 동적으로 업데이트하는 경우 이미지 선택 구성 요소 값이 업데이트되지 않습니다. (CQ-4254754)
* AEM Forms Designer 설치 프로그램에는 32비트 버전의 [Visual C++ redistributable runtime package 2012](https://docs.microsoft.com/en-US/cpp/windows/latest-supported-vc-redist?view=msvc-170) 및 [Visual C++ redistributable runtime packages 2013](https://support.microsoft.com/en-us/topic/update-for-visual-c-2013-and-visual-c-redistributable-package-5b2ac5ab-4139-8acc-08e2-9578ec9b2cf1)이 필요합니다. 설치를 시작하기 전에 앞에서 언급한 재배포 가능 런타임 패키지가 설치되어 있는지 확인하십시오. (CQ-4265668)

* PDF 생성기가 스마트 카드 기반 인증을 지원하지 않습니다. 관리자가 그룹 정책을 사용하도록 설정하는 경우 `Interactive Logon: Require Smart card` windows 서버에서는 기존의 모든 PDF 생성기 사용자가 무효화됩니다.

* 적응형 양식이 구성 요소의 값을 동적으로 업데이트하도록 구성되고 양식을 호스팅하는 게시 인스턴스가 Dispatcher를 통해 액세스되면 필드의 값을 동적으로 업데이트하는 기능이 작동하지 않습니다. 이 문제를 해결하려면 게시 인스턴스에서 CRXDE를 열고 다음으로 이동합니다. `/libs/fd/af/runtime/clientlibs/guideChartReducer`을 클릭하고 아래에 나열된 속성을 만듭니다.

   * Name: allowProxy
   * Type: Boolean
   * Value: true
   * Protected: False
   * Mandatory: False
   * Multiple: False
   * 자동 생성됨: False

   이 속성으로 런타임 폴더 아래의 클라이언트 라이브러리가 프록시에 액세스할 수 있습니다. (CQ-4268679)

* AEM Forms가 시작되면 `SAX Security Manager could not be setup`라는 경고가 나타납니다.
* Adobe Acrobat Reader 버전 20.10.00을 실행하는 Apple iOS 또는 iPadOS에서 AEM Forms Document Security로 보호된 PDF을 열 경우
* Apple iOS 디바이스에서 표준 HTML 업로드 필드가 포함된 양식을 제출할 경우, 때때로 파일의 콘텐츠가 전송되지 않고 반대편에서 0바이트 파일이 수신됩니다. Apple iOS 15.1은 이 문제에 대한 해결 방법을 제공합니다.

## 제품 다운로드 및 지원(제한됨 사이트) {#product-download-and-support-restricted-sites}

다음 사이트는 고객만 사용할 수 있습니다. 액세스가 필요한 고객의 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/).

* 의 추가 기능을 위한 제품 업데이트, 패치 및 패키지 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).

* [Admin Console을 통한 고객 지원](https://adminconsole.adobe.com/). 자세한 내용은 [새로운 Adobe 고객 지원 경험](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en).
