---
title: AEM Sites 릴리스 노트
description: Adobe Experience Manager 6.5 Sites에 관한 릴리스 노트입니다.
uuid: 676ead61-3d97-4f23-b616-c647d590bc8f
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: f82e9bd4-f7b6-492d-8e02-593e74fa1058
docset: aem65
translation-type: tm+mt
source-git-commit: a430c4de89bde3b907d342106465d3b5a7c75cc8
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 64%

---


# AEM Sites 릴리스 노트{#aem-sites-release-notes}

AEM Sites 6.5 개선 사항에 대한 자세한 정보는 다음을 참조하십시오.

## 구성 요소 및 템플릿 개발 {#component-amp-template-development}

* 새 프로젝트에 대한 Maven Project Archetype 18+의 경우 [Github 릴리스 노트](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/releases)를 참조하십시오.
* 새 프로젝트에 대한 단일 페이지 Maven Project Archetype 1.0.6+의 경우 [Github 릴리스 노트](https://github.com/adobe/aem-spa-project-archetype/releases)를 참조하십시오.
* HTL 버전 1.4의 경우, [Github 릴리스 노트](https://github.com/adobe/htl-spec/releases/tag/1.4)를 참조하십시오.

   * 문자열, 배열 및 개체의 &quot;in&quot; 연산자:

      ```
      ${'a' in 'abc’}
       ${100 in myArray}
       ${'a' in myObject}
      ```

   * 데이터-슬라이셋으로 변수 선언:
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * 목록 및 반복 컨트롤 매개 변수: 시작, 단계, 끝:
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * 데이터-줄바꿈용 식별자:

      ```
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
       text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
       </div>
      ```

   * 음수에 대한 지원

* 코어 구성 요소 2.3.2+의 경우, ](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/releases)Github 릴리스 노트[를 참조하십시오.
* 레이아웃 컨테이너 그리드 시스템의 경우, [Github](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid)를 참조하십시오.
* Clientlib 관리자: Google Closure Compiler가 JavaScript clientlibs의 축소 설정(이전 기본값은 Yahoo YUI임) 및 업데이트된 Google Closure Compiler를 버전 v20190121로 업데이트했습니다.
* 템플릿 편집기 및 정책

   * JS SDK(SPA Editor라고도 함)를 사용하는 단일 페이지 앱용 템플릿을 만들고 편집할 수 있습니다.

* Reference Site We.Retail 4.0의 경우 [Github 릴리스 노트](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases)를 참조하십시오.
* Toolkit to upgrade existing sites to leverage the latest editor capabilities, see [Github repository](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM에는 기존 사용자 지정 코드와 최대 호환성을 제공하기 위해 jQuery 라이브러리의 버전 1.12.4가 포함되어 있습니다. 알려진 보안 문제를 해결하기 위해 Adobe에서 수정을 완료했습니다.

## 사이트 관리 {#site-administration}

* [참조](/help/sites-authoring/author-environment-tools.md#references) 레일에는 선택한 페이지를 가리키는 내부 링크를 나열하는 새 섹션이 있습니다. 이 기능은 페이지를 오프라인으로 전환하거나 삭제할 때 어떤 페이지를 오프라인으로 전환하기 전에 조정해야 하는지 확인할 때 유용합니다.
* [목록 보기](/help/sites-authoring/basic-handling.md#list-view)에는 페이지가 현재 워크플로우에 있을 때 상태를 표시하는 새 워크플로우 열이 있습니다.
* [페이지 속성](/help/sites-authoring/editing-page-properties.md)에서 페이지에 썸네일을 지정할 때(썸네일 탭) 기존 자산을 탐색할 수 있습니다.

## 페이지 편집기 {#page-editor}

* JS SDK(SPA 편집기라고도 함)를 활용하는 React 및 Angular 클라이언트 측 구성 요소를 사용하여 단일 페이지 앱 환경의 컨텍스트 내 편집 및 작성 구축을 허용합니다.
* 스캐폴딩 모드는 페이지에 스캐폴딩 페이지가 구성된 경우에만 표시됩니다.

## 컨텐츠 조각 및 편집기 {#content-fragments-amp-editor}

* 컨텐츠 조각 편집기의 새로운 [주석](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) 레일을 통해 일반 주석을 작성하고 텍스트 내에서 주석 확인(타임라인 레일에도 표시)
* Ability to set the default content type of a multi-line text element in a [Content Fragment model](/help/assets/content-fragments/content-fragments-models.md) to simple text, rich text or markdown
* RTE(전체 화면 뷰)의 텍스트를 선택하여 [주석](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)을 추가
* 참조 레일을 통해 컨텐츠 조각을 나란히 [버전 비교](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions)
* 자산 [보고서 다운로드]는 해당 컨텐츠 조각을 표시
* /api.json를 통해 [Assets HTTP API에 컨텐츠 조각 지원](/help/assets/assets-api-content-fragments.md)을 추가합니다. 컨텐츠 조각을 작성, 업데이트, 읽기 및 삭제하기 위한 API가 있습니다.

## 경험 조각 {#experience-fragments}

* [경험 조각](/help/sites-authoring/experience-fragments.md)의 색인 생성 기능이 개선했으므로 컨텐츠가 사용 중인 페이지에서 검색됩니다.
* ](/help/sites-administering/experience-fragments-target.md)Export to Target[ 옵션을 통해 경험 조각을 JSON(기본값: HTML) 또는 두 가지 모두로 보낼 수 있습니다.

## 번역 {#translation}

* 프로젝트 마스터를 사용하여 변역 프로젝트 생성 간소화
* 번역 작업을 기본적으로 승인된 상태로 설정하여 번역 프로젝트 실행 간소화
* 타사 번역 메모리의 변경 사항으로 번역 페이지 업데이트 허용
* JSON 형식으로 번역 작업 내보내기 허용
* V3 API를 사용하도록 Microsoft Translation 통합 업데이트

## Multi-Site Management(MSM) {#multi-site-management-msm}

* PushOnModify를 사용하는 롤아웃 구성의 경우, 일관성 없는 상태를 방지하기 위해 페이지 이동 작업을 보다 효과적으로 처리할 수 있습니다.
* 라이브 카피 구조 내에서 새 페이지를 생성하면 기본적으로 독립 페이지가 만들어짐
* JS SDK(SPA Editor라고도 함)를 사용하는 단일 페이지 앱에서 MSM 기능 사용

## 론치 {#launches}

* 실행을 위한 신규 검토 및 승인 워크플로우, 승인된 실행 페이지만 프로모션할 수 있는 기능
* 프로모션 단계](/help/sites-authoring/launches-promoting.md#promoting-launch-pages) 직후 [실행]을 삭제할 수 있도록 선택하기 위해 UI에 옵션 추가[

## 컨텐츠 타깃팅 및 시뮬레이션 {#content-targeting-simulation}

* ContextHub 데이터 계층 및 클라이언트측 규칙 엔진 JavaScript가 기본적으로 jQuery 3을 사용하도록 업데이트되었습니다.

## AEM and Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>AEM 6.5 릴리스 시점에는 AEM에서 at.js 2.x가 지원되지 않습니다. 최신 버전의 at.js 1.x를 사용하십시오.

* 이제 Adobe Target 통합은 Target Standard API를 사용할 수 있습니다. 이전 버전의 AEM에서는 이제 더 이상 사용되지 않는 Target Classic HTTP API를 사용합니다.
* Adobe Target `mbox.js` version 63 is included. Adobe strongly recommends to switch implementation to `at.js` v1.x.
* `at.js` 버전 1.5.0이 이제 포함됩니다. Adobe recommends that you use [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) to provision `at.js` v1.x into the site.

## AEM and Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` H.27.5가 포함되어 있습니다. 구현은 `AppMeasurement.js`
* `AppMeasurement.js` v1.8.0이 포함되어 있습니다. Adobe recommends to use [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) to provision AppMeasurement.js into the site.

## AEM 및 상거래 {#aem-commerce}

Improvements to the Commerce Integration Framework are on a faster release cycle since AEM 6.4. [Learn more here](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/docs.html).

## Communities 추가 기능 {#communities-add-on}

[Communities 릴리스 노트 페이지](../release-notes/communities-release-notes.md)를 참조하십시오.

## 화면 추가 기능 {#screens-add-on}

* 론치를 사용하여 사이니지 컨텐츠에 대한 향후 컨텐츠 변경 계획
* 시퀀스 채널의 유료 재생
* 소스 파일을 사용하여 프로젝트 구조를 자동 생성(예: Excel 시트)

For more details on changes to AEM Screens - see the Release Notes in the [AEM Screens User Guide](https://docs.adobe.com/content/help/ko-KR/experience-manager-screens/user-guide/aem-screens-introduction.html).
