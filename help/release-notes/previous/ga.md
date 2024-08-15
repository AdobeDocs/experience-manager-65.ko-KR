---
title: ' [!DNL Adobe Experience Manager] 6.5의 일반 릴리스 노트'
description: "[!DNL Adobe Experience Manager] 6.5 릴리스 정보, 새로운 기능, 설치 방법 및 자세한 변경 목록을 요약한 노트가 있습니다."
exl-id: b3d4a527-44ca-4eb6-b393-f3e8117cf1a6
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '4493'
ht-degree: 22%

---

# [!DNL Adobe Experience Manager] 6.5의 일반 릴리스 노트{#general-release-notes-for-adobe-experience-manager}

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] |
|---|---|
| 버전 | 6.5 |
| 유형 | 주요 릴리스 |
| 일반 가용 날짜 | 2019년 4월 8일 |
| 권장 업데이트 | [AEM 최근 업데이트](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html)를 참조하세요. |

### 트리비아 {#trivia}

이 [!DNL Adobe Experience Manager] 버전의 릴리스 주기는 2018년 4월 4일에 시작해서 23회의 품질 보증 및 버그 수정을 반복했으며 2019년 3월 28일에 끝났습니다. 이번 릴리스에서 수정된 개선 사항 및 새로운 기능 등 고객 관련 문제의 총 수는 1345개입니다.

[!DNL Adobe Experience Manager] 6.5는 2019년 4월 8일부터 일반적으로 사용할 수 있습니다.

![AEM 6.5 로그인 화면](/help/assets/assets/aem65-login-v4.png)

## 새로운 기능 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5는 [!DNL Adobe Experience Manager] 6.4 코드 베이스에 대한 업그레이드 릴리스입니다. 새롭고 향상된 기능, 주요 고객 수정 사항, 우선 순위가 높은 고객 개선 사항 및 제품 안정화를 위한 일반적인 버그 수정을 제공합니다. SP4까지 [!DNL Adobe Experience Manager] 6.4 서비스 팩 릴리스도 포함됩니다.

아래 목록은 개요를 제공하며 후속 페이지에는 전체 세부 정보가 나열됩니다.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5의 플랫폼은 OSGi 기반 프레임워크(Apache Sling 및 Apache Felix) 및 Java™ 콘텐츠 저장소의 업데이트된 버전 위에 빌드합니다. Apache Jackrabbit Oak 1.10.2.

Quickstart는 Eclipse Jetty 9.4.15를 서블릿 엔진으로 사용합니다.

#### Java™ 지원  {#java-support}

* Java™ 11 및 이미 지원되는 Java™ 8에 대한 새로운 지원
* 최적의 성능을 위해 기본 GC 값을 다른 값으로 재정의합니다. 자세한 내용은 [설치 및 업데이트](/help/sites-deploying/custom-standalone-install.md) 섹션을 참조하십시오.
* Java™ 11 및 Java™ 8 유지 관리 업데이트는 Oracle에서 공개적으로 제공되지 않을 경우 AEM 관련 프로젝트에서 고객이 사용할 수 있도록 Adobe에 따라 배포됩니다.

#### Java™ 개발 {#java-development}

* 이제 Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies)의 [두 버전, 사용 중지로 표시되지 않은 공용 인터페이스가 포함된 권장 버전 및 사용 중지로 표시된 인터페이스가 포함된 버전이 있습니다.

#### 사용자 인터페이스 {#user-interface}

UI를 보다 생산적이고 사용하기 쉽게 만들기 위해 다양한 개선 사항이 적용되었습니다.

* 사용자 및 그룹을 위한 새로운 권한 관리 UI.
* 이제 열 보기 도 화면에 표시되는 항목만 로드하고 사용자가 스크롤하기 시작할 때만 더 로드합니다. 목록 및 카드 보기는 6.0(6.4에서 개선됨) 이후 이미 수행되었습니다.
* 이제 해당되는 경우 열 보기에 페이지/에셋의 워크플로 상태가 포함됩니다.
* [모두 선택](/help/sites-authoring/basic-handling.md#select-all) 작업은 동일한 폴더에 있는 모든 페이지/에셋으로 작업을 빠르게 실행할 수 있는 방법입니다.
* [모두 선택](/help/sites-authoring/basic-handling.md#select-all) 작업은 로드된 항목뿐만 아니라 모든 페이지/자산에 대해 작업을 수행하려고 합니다. 작업이 일괄 작업을 처리하도록 업그레이드되지 않은 경우 경고 대화 상자가 표시됩니다.

>[!CAUTION]
>
>Adobe은 클래식 UI를 추가로 개선할 계획이 없습니다. AEM 6.5에는 클래식 UI가 포함되어 있으며 이전 릴리스에서 업그레이드하는 고객은 있는 그대로 사용할 수 있습니다. 클래식 UI는 더 이상 사용되지 않는 동안 완전히 지원됩니다. [자세한 내용](/help/sites-deploying/ui-recommendations.md).

#### 검색 및 색인 지정 {#indexing-and-search}

* 이제 Oak에서 검색이 동적 패싯을 지원합니다. 예를 들어 에셋 검색의 필터 레일은 예상 결과 수를 보여줍니다.
* QueryBuilder가 확장되어 동적 패싯이 있는 결과를 제공합니다.

#### 업그레이드 {#upgrade}

* AEM 6.2, 6.3 및 6.4를 실행하는 고객은 AEM 6.5로 직접 바로 업그레이드할 수 있습니다. 5.x 또는 6.0/6.1을 사용하는 고객 중 현장 업그레이드를 사용하려는 고객은 먼저 6.4로 업그레이드해야 합니다. 그런 다음 6.5로 업그레이드하거나 인스턴스 간에 콘텐츠를 AEM 6.5로 직접 전송하는 방식으로 업그레이드합니다.
* 업그레이드 절차는 대부분 6.5에서 동일하게 유지됩니다.
* 6.4에 도입된 이전 버전과의 호환성 , 업그레이드 복잡성 평가 및 지속 가능한 업그레이드 기능을 계속 지원합니다. 필요한 경우 이러한 영역에 대한 버전별 업데이트가 수행되었습니다.
* 이제 패턴 탐지기 포장이 간소화되었습니다. 사용 가능한 소스 버전에 대해 6.5로의 업그레이드를 평가하는 패키지가 하나 있습니다.
* 업그레이드 절차에 대한 자세한 내용은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하세요.

#### 프로젝트 및 워크플로 {#projects-and-workflows}

* 6.4에 도입된 새 워크플로 모델 편집기는 복사 및 Publish, 워크플로 단계의 변수 지원 및 향상된 `OR` 및 `AND` 분할과 같은 더 많은 작업을 포함하도록 개선되었습니다.

#### 저장소 {#repository}

* Adobe Experience Manager 6.5의 기반은 업데이트된 버전의 OSGi 기반 프레임워크(Apache Sling 및 Apache Felix) 및 Java™ 콘텐츠 저장소(Apache Jackrabbit Oak 1.10.2) 위에 구축됩니다.
* 해결된 문제에 대한 개요는 [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) 및 [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt)을 참조하십시오.

>[!CAUTION]
>
>AEM 6.3 이후 출시된 Oak 세그먼트 Tar의 새 버전은 저장소 마이그레이션이 필요합니다. 이전 버전의 TarMK에서 업그레이드하거나 새 세그먼트 Tar을 다른 유형의 지속성에서 전환하려는 경우 이 단계는 필수입니다. 새 세그먼트 Tar의 이점에 대한 자세한 내용은 [Oak 세그먼트 Tar로 마이그레이션 FAQ](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar)를 참조하십시오.

#### OSGI {#osgi}

* OSGi 약속 및 변환기 유틸리티 라이브러리가 추가되었습니다.

#### 보안 {#security}

* 관리자용 암호 만료가 추가되었습니다.

#### 웹 서버 {#web-server}

* 빠른 시작 배포는 Eclipse Jetty 9.4.15를 서블릿 엔진으로 사용합니다(AEM 6.4는 9.3.22와 함께 제공됨).

### [!DNL Experience Manager]개 사이트 {#experience-manager-sites}

#### 관리되는 단일 페이지 앱 {#managed-single-page-apps}

페이지 편집기는 클라이언트측 렌더링된 경험([SPA 편집기](/help/sites-developing/spa-architecture.md))에서 콘텐츠 및 작성/레이아웃을 상황에 맞게 편집하는 기능을 추가합니다. JavaScript 프레임워크 React 또는 Angular을 사용하여 빌드된 기존 단일 페이지 앱은 AEM SJ SDK를 사용하여 확장하여 전문가가 편집할 수 있습니다.

AEM 6.5와 함께 AEM 6.4 SP2로 처음 제공되는 SPA 지원은 다음과 같은 기능을 제공합니다.

* 템플릿 편집기 를 사용하여 AEMSPA 에서 편집 가능한 부분을 편집하고 구성합니다.
* 다중 사이트 관리를 사용하여 국가, 프랜차이즈 또는 흰색 레이블이 지정된 SPA 경험을 만듭니다.

#### 헤드리스 콘텐츠 관리 {#headless-content-management}

AEM은 다양한 형식 및 다양한 스택 수준에서 콘텐츠를 제공할 수 있습니다. 일부는 2008년 이후 [Sling GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) 및 [POST 서블릿](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html)과 함께 사용되었습니다. 컨텐츠 서비스([Sling 모델 내보내기](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=ko-KR))는 AEM 6.3에서 도입되었으며, AEM SJ SDK가 단일 페이지 앱을 하이드레이션하는 데 사용하는 메서드입니다. [Assets용 HTTP API](/help/assets/mac-api-assets.md)은(는) AEM 6.5용으로 확장된 CRUD API입니다.

새로운 HTTP API 기능:

* 조각을 만들고, 업데이트하고, 읽고, 삭제하기 위해 Assets용 HTTP API에 [콘텐츠 조각 지원을 추가했습니다](/help/assets/assets-api-content-fragments.md).
* [콘텐츠 조각 목록 핵심 구성 요소](https://www.aemcomponents.dev)와(과) 함께 콘텐츠 서비스를 통해 콘텐츠 조각 목록을 노출합니다.
* 각 구성 요소에 대한 기본 Content Services JSON 출력을 표시하는 [핵심 구성 요소 라이브러리](https://www.aemcomponents.dev)

#### Screens 추가 기능 {#screens-add-on}

대화형 키오스크에서 디지털 사이니지에 이르기까지 모든 디지털 디스플레이에서 경험을 효율적으로 디자인, 전달 및 최적화할 수 있습니다.

* 개선된 콘텐츠 재사용을 통해 디지털 및 인스토어 환경에서 경험과 콘텐츠를 통합합니다.
* Launches를 지원하여 작성 및 승인/게시 워크플로 간소화
* SPA Editor를 사용하여 풍부한 대화형 경험 편집 및 전달
* Launches를 사용하여 간판 컨텐츠의 향후 컨텐츠 변경 계획
* 시퀀스 채널에서 유료 재생
* Excel 시트와 같은 소스 파일을 사용하여 프로젝트 구조 자동 생성
* 강력한 온라인 및 오프라인 작업(Smart Sync)을 통해 미디어 플레이어를 확장하여 가장 큰 간판 네트워크까지 확장할 수 있습니다.
* 동적 자리 표시자를 사용하여 데이터 트리거된 콘텐츠의 위치 또는 구성으로 개인화합니다.
* AEM Screens Player로의 Adobe Analytics 통합으로 추진된 통합 인사이트

AEM Screens 변경에 대한 자세한 내용은 [AEM Screens 사용자 안내서](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html)의 릴리스 노트를 참조하십시오.

#### 구성 요소 및 템플릿 개발 {#component-amp-template-development}

* 새 프로젝트에 대한 Maven Project Archetype 18+의 경우 [GitHub 릴리스 노트](https://github.com/adobe/aem-project-archetype/releases)를 참조하십시오.
* 새 프로젝트의 단일 페이지 App Maven Project Archetype 1.0.6+는 [GitHub 릴리스 노트](https://github.com/adobe/aem-spa-project-archetype/releases)를 참조하십시오.
* HTL 버전 1.4의 경우 [GitHub 릴리스 노트](https://github.com/adobe/htl-spec/releases/tag/1.4)를 참조하십시오.

   * 문자열, 배열 및 개체의 &quot;in&quot; 연산자:

     ```html
     ${'a' in 'abc'}
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

* 핵심 구성 요소 2.3.2+의 경우 [GitHub 릴리스 노트](https://github.com/adobe/aem-core-wcm-components/releases)를 참조하십시오.
* 레이아웃 컨테이너 그리드 시스템의 경우 [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid)을(를) 참조하십시오.
* Clientlib Manager: Google Closure Compiler가 JavaScript clientlibs(이전 기본값은 Yahoo YUI)를 축소하고 v20190121 버전으로 Google Closure Compiler를 업데이트했습니다.
* 템플릿 편집기 및 정책

   * JS SDK(SPA 편집기라고도 함)를 사용하는 단일 페이지 앱에 대한 템플릿 생성 및 편집 

* Reference Site We.Retail 4.0의 경우 [GitHub 릴리스 노트](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases)를 참조하십시오.
* 기존 사이트를 업그레이드하여 최신 편집기 기능을 사용할 수 있는 도구는 [GitHub 저장소](https://github.com/adobe/aem-modernize-tools)를 참조하십시오.

>[!CAUTION]
>
>AEM에는 기존 사용자 정의 코드와의 최대 호환성을 제공하기 위해 jQuery 라이브러리의 버전 1.12.4가 포함됩니다. 알려진 보안 문제를 해결하기 위해 Adobe이 수정했습니다.

#### 사이트 관리 {#site-administration}

* [참조](/help/sites-authoring/author-environment-tools.md#references) 레일에는 선택한 페이지를 가리키는 내부 링크를 나열하는 새로운 섹션이 있습니다. 페이지를 오프라인으로 전환하거나 삭제하여 오프라인으로 전환하기 전에 조정해야 하는 페이지를 확인할 때 유용합니다.
* [목록 보기](/help/sites-authoring/basic-handling.md#list-view)에는 페이지가 워크플로우에 있을 때의 상태를 표시하는 새 워크플로우 열이 있습니다.
* 이제 페이지에 썸네일을 할당할 때 [페이지 속성](/help/sites-authoring/editing-page-properties.md)에서 기존 자산을 검색할 수 있습니다(썸네일 탭).

#### 페이지 편집기 {#page-editor}

* JS SDK(SPA Editor라고도 함)를 사용하는 React 및 Angular 클라이언트측 구성 요소로 빌드된 단일 페이지 앱 경험을 컨텍스트에서 편집하고 구성할 수 있습니다.
* 스캐폴딩 모드는 페이지에 스캐폴딩 페이지가 구성된 경우에만 표시됩니다.

#### 컨텐츠 조각 및 편집기 {#content-fragments-amp-editor}

* 콘텐츠 조각 편집기의 새로운 [주석](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) 레일을 통해 일반 주석을 작성하고 텍스트 내에서 주석 확인(타임라인 레일에도 표시)
* [콘텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md)에서 여러 줄 텍스트 요소의 기본 콘텐츠 형식을 단순 텍스트, 서식 있는 텍스트 또는 Markdown으로 설정하는 기능
* RTE(전체 화면 보기)에서 텍스트를 선택하여 [댓글/주석](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) 추가
* 참조 레일을 통해 콘텐츠 조각의 [버전 비교](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions)
* 이제 에셋 다운로드 보고서에 콘텐츠 조각이 그에 따라 표시됩니다
* /api.json을 통해 [콘텐츠 조각 지원을 Assets HTTP API에 추가](/help/assets/assets-api-content-fragments.md)합니다. 콘텐츠 조각의 만들기, 업데이트, 읽기 및 삭제를 위한 API가 있습니다.

#### 경험 조각 {#experience-fragments}

* [경험 조각](/help/sites-authoring/experience-fragments.md)의 색인화가 개선되어 해당 콘텐츠가 사용 중인 페이지 검색에서 검색됩니다.
* [Export to Target](/help/sites-administering/experience-fragments-target.md) 옵션을 사용하면 경험 조각을 JSON(기본값: HTML) 또는 둘 다로 보낼 수 있습니다.

#### 번역 {#translation}

* 프로젝트 마스터를 사용하여 번역 프로젝트 만들기를 단순화합니다.
* 기본적으로 번역 작업을 승인 상태로 설정하여 번역 프로젝트 실행을 간소화합니다.
* 서드파티 번역 메모리의 변경 사항을 사용하여 번역된 페이지를 업데이트할 수 있습니다.
* JSON 형식으로 번역 작업 내보내기를 허용합니다.
* V3 API를 사용하도록 Microsoft® 번역 통합을 업데이트합니다.

#### 다중 사이트 관리(MSM) {#multi-site-management-msm}

* PushOnModify를 사용하는 롤아웃 구성의 경우, 일관되지 않은 상태를 방지하기 위해 페이지 이동 작업을 보다 효율적으로 처리할 수 있습니다.
* 라이브 카피 구조 내에 페이지를 만들면 기본적으로 독립 페이지가 만들어집니다.
* JS SDK(SPA 편집기라고도 함)를 사용하는 단일 페이지 앱에서 MSM 기능 사용

#### 론치 {#launches}

* 론치에 대한 새로운 검토 및 승인 워크플로우 및 승인된 론치 페이지만 홍보하는 기능
* 프로모션 단계[ 직후 [실행]을 삭제할 수 있도록 선택하기 위해 UI에 옵션 추가](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

#### 콘텐츠 타겟팅 및 시뮬레이션 {#content-targeting-simulation}

* ContextHub 데이터 계층 및 클라이언트측 규칙 엔진 JavaScript가 기본적으로 jQuery 3을 사용하도록 업데이트되었습니다.

#### AEM 및 Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>현재:
>
>* AEM의 활동 콘솔에서 타깃팅 엔진으로 Adobe Target을 사용하는 경우 `at.js 1.x`만 지원됩니다.
>
>* Target으로 경험 조각 내보내기를 사용하고 Target의 콘솔 내에서 활동을 실행하는 경우 `at.js. 1.x` 및 `at.js 2.x`이(가) 모두 지원됩니다.

* 이제 Adobe Target 통합에서 Target Standard API를 사용합니다. AEM의 이전 버전에서는 이제 더 이상 사용되지 않는 Target Classic HTTP API를 사용합니다.
* Adobe Target `mbox.js` 버전 63이 포함되어 있습니다. Adobe은 구현을 `at.js` v1.x(으)로 전환할 것을 강력히 권장합니다.
* 이제 `at.js` 버전 1.5.0이 포함되어 있습니다. [Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html)를 사용하여 사이트에 `at.js` v1.x를 프로비저닝할 것을 권장합니다.

#### AEM 및 Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` H.27.5가 포함됩니다. 구현을 `AppMeasurement.js`로 전환할 것을 권장합니다.
* `AppMeasurement.js` v1.8.0이 포함됩니다. Adobe은 [Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html)을(를) 사용하여 사이트에 AppMeasurement.js를 프로비저닝할 것을 권장합니다.

#### AEM 및 Commerce {#aem-commerce}

AEM 6.4 이후 Commerce integration framework 개선 사항이 더 빠른 릴리스 주기에 있습니다. [Commerce integration framework을 사용한 AEM 및 Adobe Commerce 통합](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/magento.html)에서 자세히 알아보세요.

#### Communities 추가 기능 {#communities-add-on}

최신 릴리스를 얻으려면 설명서의 [커뮤니티 배포](/help/communities/deploy-communities.md) 섹션을 참조하십시오.

##### 커뮤니티 참여 개선 사항 {#enhancements-to-community-engagement}

**@Mentions 지원**
이제 AEM Communities을 통해 등록된 사용자는 사용자 생성 콘텐츠에서 다른 등록된 멤버를 태그 지정(언급)하여 주의를 끌 수 있습니다. 그러면 태그가 지정된(언급된) 멤버에게 알림이 전송되며 해당 사용자 생성 컨텐츠에 대한 딥링크가 표시됩니다. 그러나 사용자는 웹 및 이메일 알림을 비활성화/활성화하도록 선택할 수 있습니다.

![언급 지원 시](/help/release-notes/assets/at-mentions.png)

커뮤니티 사용자는 자신의 이름, 성 또는 사용자 이름을 검색할 필요가 없으며, 연락한 사람이 있는지 또는 주의를 기울여야 하는지 확인할 수 있습니다. 또한 UGC 작성자는 문제를 가장 잘 해결하고 입력을 추가할 수 있는 등록된 특정 사용자로부터 응답을 구할 수 있습니다.

커뮤니티 관리자는 등록된 사용자가 해당 구성 요소에서 기능을 사용할 수 있도록 하려면 커뮤니티 구성 요소에 대해 **언급을 활성화**&#x200B;해야 합니다.

**그룹 메시지**

이제 등록된 커뮤니티 구성원은 그룹 구성원에게 동일한 메시지를 개별적으로 보내는 대신 단일 이메일 작성을 통해 그룹에 직접 메시지를 일괄 보낼 수 있습니다. [그룹 메시징](/help/communities/configure-messaging.md)을(를) 허용하려면 [메시징 작업 서비스](/help/communities/messaging.md#group-messaging)의 인스턴스를 모두 사용하도록 설정하십시오.

![그룹 메시지](/help/release-notes/assets/group-messaging.png)

##### 벌크 중재 개선 사항 {#enhancements-to-bulk-moderation}

일괄 중재에서 맞춤형 필터

이제 [사용자 지정 필터](/help/communities/moderation.md#custom-filters)을(를) 개발하여 일괄 중재 UI에 추가할 수 있습니다.

태그를 통한 필터링을 보여 주는 [샘플 프로젝트](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)는 [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)에서 사용할 수 있습니다. 이 프로젝트는 유사한 맞춤형 필터를 개발하는 기반으로 사용할 수 있습니다.

![사용자 지정 필터](/help/release-notes/assets/custom-tag-filter.png)

**일괄 중재에서 목록 보기**

사용자 생성 콘텐츠 항목을 표시하기 위해 향상된 UI를 제공하는 새 목록 보기가 일괄 중재에 제공되었습니다.

![목록 보기의 일괄 중재](/help/release-notes/assets/list-view-moderation.png)

##### 사이트 및 그룹 관리 개선 사항 {#enhancements-to-site-and-group-management}

**작성자측 사이트 및 그룹 관리자**

Communities, AEM 6.5 이상에서는 다른 커뮤니티 사이트와 그룹/중첩 그룹의 분산 관리(및 관리)를 허용합니다. 이제 여러 커뮤니티 사이트 및 중첩된 그룹을 호스팅하는 조직은 사이트(및 그룹) 생성 시 작성자 측에서 관리자 역할의 구성원을 선택할 수 있습니다.

![사이트 관리자](/help/release-notes/assets/site-admin.png)

사이트 관리자는 계층 구조 수준에서 그룹을 만들고 기본 관리자가 될 수 있습니다. 이러한 관리자는 나중에 다른 그룹 관리자가 제거할 수 있습니다. 그룹 관리자는 그룹 G1을 관리하고 G1 아래에 중첩된 하위 그룹을 만들 수 있습니다.

##### 지원 개선 사항 {#enhancements-to-enablement}

**SCORM 2017.1 지원**

AEM 6.5 Communities의 지원 기능이 공유 가능한 콘텐츠 개체 참조 모델 [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) 엔진을 지원합니다.

* 지원 구성 요소에 대한 키보드 탐색 지원
* AEM Communities의 지원 구성 요소(예: 카탈로그 및 과정 재생, 할당, 파일 라이브러리)는 향상된 접근성을 위해 키보드 탐색을 지원합니다.

##### 기타 개선 사항 {#other-enhancements}

* Solr 7 지원
* AEM 6.5 커뮤니티는 MSRP 및 DSRP를 설정하는 동안 검색 플랫폼의 Apache Solr 7.0 버전을 지원합니다.

### [!DNL Experience Manager Assets] {#experience-manager-assets}

AEM 6.5에서는 AEM 사용자, DAM 역할 및 관련 크리에이티브 및 마케팅 역할의 생산성을 높이기 위해 다음과 같은 기능과 개선 사항을 도입했습니다.

#### [!DNL Adobe Creative Cloud] 및 크리에이티브 워크플로우와 통합 {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager]는 광고 및 마케팅 또는 비즈니스 팀이 밀접하게 협력하는 워크플로에서 [!DNL Adobe Creative Cloud]와 통합하고 자산을 공유하는 다양한 방법을 제공합니다. [!DNL Experience Manager] 6.5는 통합 과정에서 지속적으로 개선되고 더 많은 기회를 노출하며 기존 방법을 간소화합니다.

콘텐츠 속도 사용 사례를 최상으로 지원하는 데 사용할 수 있는 [!DNL Experience Manager] 6.5의 특정 기능 및 통합에 대해 알아보려면 계속 읽어 보십시오.

##### Adobe 에셋 링크 {#aal}

[!DNL Adobe Asset Link]는 컨텐츠 작성 프로세스에서 광고 팀과 마케터 간의 협업을 강화합니다. 광고 팀은 친숙한 앱을 종료하지 않고 [!DNL Experience Manager Assets]에 저장된 컨텐츠에 액세스할 수 있습니다. 광고 팀은 [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] 및 [!DNL Adobe InDesign] 앱에서 앱 내 패널을 사용하여 자산을 원활하게 탐색, 검색, 체크아웃 및 체크인할 수 있습니다.

[!DNL Adobe Asset Link]는 [Creative Cloud for Enterprise](https://www.adobe.com/kr/creativecloud/business/enterprise.html) 제품의 일부입니다. [!DNL Experience Manager] 배포의 필수 구성을 포함한 자세한 정보는 [Adobe Asset Link](https://helpx.adobe.com/kr/enterprise/using/adobe-asset-link.html)를 참조하십시오.

![Adobe Photoshop에서 자산 검색](/help/release-notes/assets/asset_search_photoshop.png)

##### [!DNL Adobe Stock] 통합 {#stock}

조직은 [!DNL Experience Manager Assets] 내에서 [!DNL Adobe Stock] 엔터프라이즈 플랜을 사용하여 라이선스가 있는 자산이 귀사의 광고 및 마케팅 프로젝트에 폭넓게 사용 가능한지 확인할 수 있습니다. [!DNL Adobe Stock]의 강력한 DAM 기능을 사용하여 Experience Manager에 저장된 [!DNL Experience Manager] 자산을 빠르게 찾고, 미리 보고, 라이선스를 제공할 수 있습니다.

[!DNL Adobe Stock] 서비스는 디자이너와 기업의 모든 광고 프로젝트를 위해 고품질로 큐레이팅된 로열티가 없는 수백만 장의 사진, 벡터, 일러스트레이션, 비디오, 템플릿 및 3D 자산에 대한 액세스를 제공합니다.

자세한 내용은 [Experience Manager Assets에서 Adobe Stock 자산 사용](/help/assets/aem-assets-adobe-stock.md)을 참조하세요.

![Experience Manager Assets 내에서 Adobe Stock 이미지 및 라이선스 미리 보기](/help/release-notes/assets/stock_image_preview_license_options.png)

*그림: [!DNL Experience Manager Assets] 내의 [!DNL Adobe Stock] 이미지 및 라이선스 미리 보기.*

![Experience Manager에서 라이선스가 있는 Adobe Stock 이미지 검색 및 필터링](/help/release-notes/assets/aem-search-filters2.jpg)

*그림: [!DNL Adobe Stock]에서 라이선스가 부여된* 이미지 검색 및 필터링.[!DNL Experience Manager]

##### [!DNL Adobe InDesign]의 동적 참조 {#dynamic-references-in-indesign}

[!DNL Adobe InDesign] 파일에 사용된 [!DNL Experience Manager Assets]이 동적입니다. 참조된 자산이 저장소에서 이동하면 참조가 자동으로 업데이트됩니다. 자세한 내용은 [복합 자산을 관리하는 방법](/help/assets/managing-linked-subassets.md)을 참조하세요.

#### Brand Portal 기능 {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal]은 승인된 자산을 외부 공급업체/에이전시 및 내부 비즈니스 사용자가 간편하게 구매하고 효과적으로 제어하며 장치 간에 안전하게 분배할 수 있도록 지원합니다. 자산 공유의 효율성을 향상시키고, 자산 출시 시기를 앞당길 수 있으며, 규정을 준수하지 않고 무단 액세스하는 위험을 방지할 수 있습니다.

자세한 내용은 [Brand Portal의 새로운 기능](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html)을 참조하세요.

#### 연결된 자산 {#connectedassets}

대기업에서는 웹 사이트를 만드는 데 필요한 인프라를 배포할 수 있습니다. 웹 사이트 생성 기능과 필요한 디지털 자산이 서로 다른 사일로에 있는 경우가 있습니다.

[!DNL Experience Manager Sites]는 웹 페이지를 구축하는 기능을 제공하며, [!DNL Experience Manager Assets]은 웹 사이트에 필요한 자산을 제공하는 DAM(디지털 자산 관리) 시스템입니다. [!DNL Experience Manager]는 이제 [!DNL Sites] 및 [!DNL Assets]을 통합하여 위의 사용 사례를 지원합니다. [연결된 자산 기능을 구성하고 사용하는 방법](/help/assets/use-assets-across-connected-assets-instances.md)을 참조하십시오.

![다른 [!DNL Experience Manager] 배포의 [!DNL Sites] 페이지에 있는 [!DNL Experience Manager] 배포의 자산을 드래그합니다.](/help/release-notes/assets/connected-assets-drag-and-drop-only.gif)

*그림: 다른 [!DNL Experience Manager] 배포의 [!DNL Sites] 페이지에 있는 [!DNL Experience Manager] 배포의 자산을 드래그합니다.*

#### Dynamic Media {#dynamic-media}

[!DNL Dynamic Media]는 [!DNL Experience Manager Assets]에서 향상된 리치 미디어 작성 및 전달 기능을 제공하여 몰입 및 맞춤화된 최신 경험을 제공합니다. 고품질의 단일 기본 에셋을 업로드하고 Adobe의 고급 클라우드 렌더링 및 뷰어를 사용하여 모든 표현물의 조합을 제공하여 조직의 미디어 전략을 지원할 수 있습니다.

새 [!DNL Dynamic Media] 기능에 대한 자세한 내용은 [Dynamic Media 릴리스 노트](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html)를 참조하십시오.

##### 360 비디오 지원 {#video-support}

최첨단 뷰어를 사용하여 [!DNL Experience Manager]에서 직접 360 비디오 파일을 관리하여 데스크톱, 모바일 및 VR 헤드셋에 VR 경험을 제공할 수 있습니다. 자세한 내용은 [360 동영상 사용](/help/assets/360-video.md)을 참조하세요.

##### 사용자 지정 비디오 썸네일 {#custom-video-thumbnails}

이제 비디오 자체의 프레임이나 DAM에 저장된 다른 콘텐츠를 사용하여 비디오 에셋의 썸네일을 사용자 지정할 수 있습니다. 자세한 지침은 [비디오 축소판 정보](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode)를 참조하세요.

##### 액세스 가능성 개선 {#accessibility-enhancements}

이제 [!DNL Dynamic Media] 뷰어에는 Aria 지원, 화면 판독기 및 대체 텍스트와 같은 향상된 액세스 가능성에 대한 지원이 포함되어 있습니다. 자세한 내용은 [뷰어 참조 안내서](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html)를 참조하십시오.

#### 향상된 검색 경험 {#experience-enhancement-for-searching}

[!DNL Experience Manager] 6.5에서는 마케터가 검색 결과 페이지에서 원하는 자산을 더 빨리 발견할 수 있습니다. 검색 패싯은 검색 필터를 적용하기 전에도 자산 수로 업데이트됩니다. 필터에 대한 예상 수를 확인하면 사용자가 검색 결과를 효율적으로 탐색할 수 있습니다. 자세한 내용은 [Experience Manager에서 자산 검색](/help/assets/search-assets.md)을 참조하십시오.

![검색 패싯에서 검색 결과를 필터링하지 않고 자산 수를 확인합니다](/help/assets/assets/asset_search_results_in_facets_filters.png)

*그림: 검색 패싯에서 검색 결과를 필터링하지 않고 자산 수 확인.*

#### 유용성 개선 {#usability-enhancement}

이제 폴더 내 또는 검색 결과에서 한 번에 로드된 모든 자산을 선택할 수 있습니다. 여러 자산을 신속하게 관리하는 데 도움이 됩니다. 이 확인란은 [!DNL Experience Manager] 인터페이스에 표시되는 자산뿐만 아니라 시나리오에 맞는 모든 자산, 즉 검색 결과를 선택합니다.

![두 선택 옵션을 사용하여 한 번의 클릭으로 모든 자산을 선택합니다.](/help/release-notes/assets/select-all-in-aem-assets.gif)

*그림: 모두 선택 옵션을 사용하여 한 번의 클릭으로 모든 자산 선택.*

#### 메타데이터 개선 사항 {#metadata-enhancements}

[!DNL Assets]을(를) 사용하면 폴더 속성 페이지에 표시되는 레이아웃 및 메타데이터를 정의하는 자산 폴더에 대한 메타데이터 스키마를 만들 수 있습니다. 이제 폴더 메타데이터 스키마를 기존 폴더에 할당하거나 폴더를 만들 수 있습니다. 자세한 내용은 [폴더 메타데이터 스키마](/help/assets/metadata-config.md#folder-metadata-schema)를 참조하십시오.

계단식 메타데이터를 지정할 때, 양식에 수동으로 입력하는 대신, 런타임 시 JSON 파일에서 선택 사항을 로드할 수 있습니다. 자세한 내용은 [계단식 메타데이터](/help/assets/metadata-schemas.md#cascading-metadata)를 참조하십시오.

#### 보고 개선 사항 {#reporting-enhancements}

컨텐츠 조각 및 링크 공유는 지금 다운로드된 보고서에 포함됩니다. 자세한 정보는 [자산 보고서](/help/assets/asset-reports.md)를 참조하십시오.

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM 6.5 Forms은 몇 가지 새로운 기능과 개선 사항을 제공합니다. 주요 기능은 다음과 같습니다.

* 제출된 양식, 처리된 문서 및 렌더링된 문서의 수를 추적하는 트랜잭션 보고서
* 대화형 커뮤니케이션의 유용성 개선
* 적응형 양식의 클라우드 기반 디지털 서명
* 적응형 양식 및 대화형 커뮤니케이션을 AEM Sites SPA(단일 페이지 애플리케이션)에 임베드합니다.
* AEM 워크플로우에서 변수 지원
* 대화형 커뮤니케이션에서 데이터 표시 패턴 지원
* 적응형 양식 및 대화형 통신 표 정렬
* 양식 데이터 모델에서 입력 데이터 자동 유효성 검사

새롭고 개선된 기능 및 설명서 리소스에 대한 자세한 내용은 [AEM 6.5 Forms의 새로운 기능 및 향상된 기능 요약](/help/forms/using/whats-new.md)을 참조하십시오.

### 고객 중심 개발 사용 {#use-customer-focused-development}

Adobe은 사양, 개발 및 테스트 중 개발 프로세스의 모든 단계에 고객이 기여할 수 있도록 하는 고객 중심 개발 모델을 사용하고 있습니다. 이 과정에서 모든 기여 고객 및 파트너에게 감사를 드립니다.

Adobe에는 고객 중심의 버그 해결 및 개선 요청 개발을 위한 수집, 우선 순위 지정 및 추적을 활성화하는 절차 및 프로세스가 있습니다. [Experience Manager 지원 포털](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support)은(는) Adobe 개선 및 결함 추적 시스템과 통합되었습니다. 고객 질문은 가능한 경우 고객 지원 팀에서 식별하고 해결합니다. R&amp;D로 에스컬레이션되면 모든 고객 정보가 캡처되어 우선 순위 지정 및 보고 용도로 사용됩니다. 개발에서 유료 지원, 보증 문제 및 고객 유료 개선 사항에 우선 순위가 부여됩니다.

이 우선 순위 지정 프로세스를 통해 AEM 6.5에서 수정된 고객 중심의 변경 사항이 750개 이상 생성되었습니다.

## 릴리스에 포함된 파일 목록 {#list-of-files-that-are-part-of-the-release}

**기초**

* 독립형 빠른 시작: `cq-quickstart-6.5.0.jar`.
* 응용 프로그램 서버 빠른 시작: `cq-quickstart-6.5.0.war`.
* 다양한 웹 서버 및 플랫폼용 Dispatcher 4.3.2 이상 [다운로드 링크](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html) 보기
* Eclipse IDE용 플러그인([자세한 내용 보기 및 다운로드](/help/sites-developing/aem-eclipse.md))

* Brackets 코드 편집기의 확장([자세히 읽고 다운로드](/help/sites-developing/aem-brackets.md))
* Maven/Gradle 종속성([다운로드 링크](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/))

**사이트**

* 핵심 구성 요소([GitHub 프로젝트](https://github.com/adobe/aem-core-wcm-components))
* We.Retail 참조 구현([자세히 보기](/help/sites-developing/we-retail.md))
* Maven 프로젝트 원형:

   * 전체 스택 사이트의 경우: [GitHub 프로젝트](https://github.com/adobe/aem-project-archetype)
   * React/Angular이 있는 단일 페이지 앱의 경우: [GitHub 프로젝트](https://github.com/adobe/aem-spa-project-archetype)

* 다양한 대상 플랫폼에 대한 AEM Screens 플레이어([다운로드](https://download.macromedia.com/screens/))

* 스마트 컨텐츠 언어 모델. 영어가 사전 설치되어 더 많은 언어를 다운로드할 수 있습니다.

   * [독일어](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [스페인어](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [이탈리아어](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [프랑스어](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* 대화 상자 변환 도구 등 AEM 현대화 도구 세트. ([GitHub 프로젝트](https://github.com/adobe/aem-modernize-tools))

**Assets**

* 향상된 PDF 래스터라이저 추가 패키지([자세히 읽기](/help/assets/aem-pdf-rasterizer.md))
* 확장된 RAW 이미지 지원을 추가할 패키지([자세히 읽기](/help/assets/camera-raw.md))

**양식**

* [AEM Forms 기능용 패키지](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [AEM Forms OSGi 클라이언트 SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

## 언어 {#languages}

사용자 인터페이스는 다음 언어로 제공됩니다.

* 영어
* 독일어
* 프랑스어
* 스페인어
* 이탈리아어
* 포르투갈어(브라질)
* 일본어
* 중국어 간체
* 중국어 번체(제한적 지원)
* 한국어

[!DNL Experience Manager] 6.5가 GB18030-2005 CITS에서 중국어 인코딩 표준을 사용하도록 인증되었습니다.

## 설치 및 업데이트 {#install-update}

설치 요구 사항은 [설치 지침](/help/sites-deploying/custom-standalone-install.md)을 참조하십시오.

자세한 지침은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하세요.

## 지원되는 플랫폼 {#supported-platforms}

[AEM 6.5 기술 요구 사항](/help/sites-deploying/technical-requirements.md)에 대한 지원 수준을 포함하여 지원되는 플랫폼의 전체 매트릭스를 확인하십시오.

>[!NOTE]
>
>Oracle이 Oracle Java™ SE 제품에 대한 LTS(장기 지원) 모델로 전환되었습니다. Java™ 9 및 10은 Oracle에서 LTS가 아닌 릴리스입니다. [Oracle Java™ SE 지원 로드맵](https://www.oracle.com/technetwork/java/eol-135779.html)을 참조하세요. Adobe은 Java™의 LTS 릴리스를 지원하여 프로덕션에서 AEM만 실행할 수 있습니다. AEM 6.5에서 Java™ 11을 사용하는 것이 좋습니다.

## 사용 중단되거나 제거된 기능 {#deprecated-and-removed-features}

Adobe은 제품의 기능을 지속적으로 평가하고 시간이 지남에 따라 기능을 보다 강력한 버전으로 교체하기 위한 계획을 세우거나 향후 기대치 또는 확장에 더 잘 대비하기 위해 선택한 부품을 재구현하기로 합니다.

[!DNL Adobe Experience Manager] 6.5의 경우 [더 이상 사용되지 않거나 제거된 기능 목록을 읽어보세요](/help/release-notes/deprecated-removed-features.md). 이 페이지에는 향후 변경될 사항에 대한 사전 공지 및 이전 릴리스에서 업데이트되는 고객에 대한 중요 공지 사항이 포함되어 있습니다.

## 알려진 문제 {#known-issues}

### Platform {#platform}

* CRX-Quickstart와 그 컨텐츠가 삭제되는 문제가 보고됩니다.

  다음 각 작업에서 `htmllibmanager.fileSystemOutputCacheLocation` 속성이 빈 문자열이 아닌지 확인하십시오.

   1. `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`을(를) 호출하고 있습니다.
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

1. `org.osgi.framework.bootdelegation=`을 검색합니다. 결과를 표시할 `jdk.internal.reflect,jdk.internal.reflect.*` 속성을 추가하십시오.

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. 파일을 저장하고 AEM 인스턴스를 다시 시작합니다.

### Sites {#sites}

* **페이지 버전을 사용하여 작업**: [페이지가 이동되면 이동 전에 만든 버전에서는 더 이상 미리 보기를 수행할 수 없습니다](/help/sites-authoring/working-with-page-versions.md#previewing-a-version).

### 자산 {#assets}

* **검색:** 검색 문자열에 선행 공백([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))이 포함된 경우 결과를 반환하지 않습니다.
* **폴더 메타데이터 스키마**: 선택 단추를 추가한 후 ID 및 값 필드가 예상대로 렌더링되지 않고 삭제 기능이 작동하지 않습니다. (CQ-4261144)
* 에셋의 이름을 바꿀 때 에셋 이름에는 공백을 사용할 수 없습니다. (CQ-4266403)

### Forms {#forms}

* AEM Forms이 Linux® 운영 체제에 설치된 경우 하드웨어 보안 모듈의 디지털 서명이 작동하지 않습니다. (CQ-4266721)
* (WebSphere의 AEM Forms만 해당®) 검색 기준으로 **Forms Workflow**&#x200B;을(를) 사용하여 **관리자**&#x200B;를 검색하는 경우 **사용자** > **작업 검색** 옵션이 결과를 반환하지 않습니다. (CQ-4266457)

* AEM Forms에서 JPEG 압축이 있는 TIF 및 TIFF 파일을 PDF 문서로 변환하지 못했습니다. (CQ-4265972)
* **AEM Forms Assets 스캐너** 및 **대화형 통신 마이그레이션에 대한 편지** 옵션이 **AEM Forms 마이그레이션** 페이지에서 작동하지 않습니다. (CQ-4266572)

* (JBoss® 7만 해당) 이전 버전에서 AEM 6.5 Forms으로 업그레이드하고 이전 버전에는 기본 제출 또는 기본 렌더링 프로세스의 사본을 작성 및 사용한 프로세스(.lca)가 있는 경우, 이러한 프로세스(.lca)를 사용하는 HTML5 Forms은 필수 작업을 수행하지 못합니다. (CQ-4243928)
* 적응형 원본에서 규칙 편집기에서 양식 데이터 모델 서비스를 호출하여 이미지 선택 구성 요소의 값을 동적으로 업데이트하면 이미지 선택 구성 요소의 값이 업데이트되지 않습니다. (CQ-4254754)
* AEM Forms Designer 설치 프로그램에는 32비트 버전의 [Visual C++ redistributable runtime package 2012](https://docs.microsoft.com/en-US/cpp/windows/latest-supported-vc-redist?view=msvc-170) 및 [Visual C++ redistributable runtime packages 2013](https://support.microsoft.com/en-us/topic/update-for-visual-c-2013-and-visual-c-redistributable-package-5b2ac5ab-4139-8acc-08e2-9578ec9b2cf1)이 필요합니다. 설치를 시작하기 전에 앞에서 언급한 재배포 가능 런타임 패키지가 설치되어 있는지 확인하십시오. (CQ-4265668)

* PDF Generator이 스마트 카드 기반 인증을 지원하지 않습니다. 관리자가 Windows 서버에서 그룹 정책 `Interactive Logon: Require Smart card`을(를) 사용하도록 설정하면 기존의 모든 PDF Generator 사용자가 무효화됩니다.

* 적응형 양식이 구성 요소의 값을 동적으로 업데이트하도록 구성되어 있고 양식을 호스팅하는 게시 인스턴스가 Dispatcher을 통해 액세스되는 경우 필드의 값을 동적으로 업데이트하는 기능이 작동하지 않습니다. 이 문제를 해결하려면 게시 인스턴스에서 CRXDE를 열고 `/libs/fd/af/runtime/clientlibs/guideChartReducer`(으)로 이동한 다음 아래에 나열된 속성을 만듭니다.

   * 이름: allowProxy
   * 유형: 부울
   * 값: true
   * 보호: False
   * 필수: False
   * 다중: False
   * 자동 생성됨: False

  이 속성으로 런타임 폴더 아래의 클라이언트 라이브러리가 프록시에 액세스할 수 있습니다. (CQ-4268679)

* AEM Forms가 시작되면 `SAX Security Manager could not be setup`라는 경고가 나타납니다.
* Adobe Acrobat Reader 버전 20.10.00을 실행하는 Apple iOS 또는 iPadOS에서 AEM Forms Document Security로 보호된 PDF을 열 경우
* Apple iOS 디바이스에서 표준 HTML 업로드 필드가 포함된 양식을 제출할 경우, 때때로 파일의 콘텐츠가 전송되지 않고 반대편에서 0바이트 파일이 수신됩니다. Apple iOS 15.1은 이 문제에 대한 해결 방법을 제공합니다.

## 제품 다운로드 및 지원(제한된 사이트) {#product-download-and-support-restricted-sites}

다음 사이트는 고객만 사용할 수 있습니다. 고객이고 액세스 권한이 필요한 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/).

* [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에 대한 추가 기능을 위한 제품 업데이트, 패치 및 패키지

* [Admin Console을 통한 고객 지원](https://adminconsole.adobe.com/). 자세한 내용은 [새 Adobe 고객 지원 환경](https://experienceleague.adobe.com/docs/customer-one/using/home.html)을 참조하세요.
