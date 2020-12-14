---
title: ' [!DNL Adobe Experience Manager] 6.5에 대한 일반 릴리스 노트'
description: '[!DNL Adobe Experience Manager] 6.5 노트는 릴리스 정보, 새로운 기능, 설치 방법 및 상세 변경 목록을 설명합니다.'
translation-type: tm+mt
source-git-commit: 8d60e064ab50f24016c049c8d5d0fceb784c99a3
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 71%

---


# [!DNL Adobe Experience Manager] 6.5{#general-release-notes-for-adobe-experience-manager}에 대한 일반 릴리스 노트

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] |
|---|---|
| 버전 | 6.5 |
| 유형 | 주요 릴리스 |
| 일반 공급 일자 | 2019년 4월 8일 |
| 권장 업데이트 | [AEM 최근 업데이트](https://helpx.adobe.com/kr/experience-manager/aem-releases-updates.html)를 참조하십시오. |

### 일반 {#trivia}

2018년 4월 4일에 시작된 이 버전의 [!DNL Adobe Experience Manager]의 릴리스 주기는 23회의 품질 보증 및 버그 수정을 거쳐 2019년 3월 28일에 종료되었습니다. 이 릴리스의 개선 사항과 새로운 기능 수정을 포함한 문제에 관련된 총 고객 수는 1345명입니다.

[!DNL Adobe Experience Manager] 6.5는 일반적으로 2019년 4월 8일부터 제공됩니다.

![AEM 6.5 로그인 화면](/help/assets/assets/aem65-login-v4.png)

## 새로운 기능 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5는  [!DNL Adobe Experience Manager] 6.4 코드 베이스에 대한 업그레이드 릴리스입니다. 새롭고 향상된 기능, 주요 고객 수정 사항, 우선 순위가 높은 고객 개선 사항 및 제품 안정화를 위한 일반적인 버그 수정을 제공합니다. 또한 SP4까지 [!DNL Adobe Experience Manager] 6.4 서비스 팩 릴리스를 포함합니다.

아래 목록은 개요를 제공하며, 다음 페이지에는 전체 세부 정보가 나열됩니다.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[AEM Foundation](/help/release-notes/wcm-platform.md)의 전체 변경 목록입니다.

[!DNL Adobe Experience Manager] 6.5 빌드의 플랫폼은 업데이트된 버전의 OSGi 기반 프레임워크(Apache Sling 및 Apache Felix)와 Java Content Repository를 기반으로 합니다.아파치 잭래빗 오크 1.10.2.

빠른 시작은 Eclipse Jetty 9.4.15를 서블릿 엔진으로 사용합니다.

#### Java 지원  {#java-support}

* Java 8에 대한 기존 지원과 함께 Java 11을 새롭게 지원.
* 최적의 성능을 위해 기본 GC 값을 다른 값으로 대체합니다. 자세한 내용은 [설치 및 업데이트](/help/sites-deploying/custom-standalone-install.md) 섹션을 참조하십시오.
* Java 11 및 Java 8 유지 관리 업데이트는 Adobe에서 공개적으로 사용할 수 없는 경우 AEM 관련 프로젝트에서 고객이 사용하도록 Oracle에 의해 배포됩니다.

#### Java 개발 {#java-development}

* 이제 Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies)의 두 버전인 [이 있으며, 사용 중단으로 표시되지 않은 공용 인터페이스를 사용하는 권장 버전뿐만 아니라 사용 중단으로 표시된 인터페이스를 포함하는 버전이 있습니다.

#### 사용자 인터페이스 {#user-interface}

UI의 생산성과 사용 편의성을 향상시키기 위해 UI에 다양한 개선 사항이 적용되었습니다.

* 사용자 및 그룹에 대한 새 권한 관리 UI.
* 이제 열 보기는 화면에 표시되는 항목만 로드하고 사용자가 스크롤을 시작할 때만 추가로 로드됩니다. 목록 보기 및 카드 보기는 6.0 이후부터 이미 해당 기능이 적용되었습니다(6.4에서 강화됨)..
* 이제 열 보기에는 해당하는 경우 페이지/자산에 대한 워크플로우 상태가 포함됩니다.
* [모두 선택](/help/sites-authoring/basic-handling.md#select-all) 작업은 동일한 폴더에 있는 모든 페이지/자산을 포함하는 작업을 빠르게 실행하는 방법입니다.
* [모두 선택](/help/sites-authoring/basic-handling.md#select-all) 조치는 로드된 페이지/자산이 아니라 모든 페이지/자산에 대해 조치를 시도합니다. 일괄 작업을 처리하도록 작업이 업그레이드되지 않은 경우 경고 대화 상자가 표시됩니다.

>[!CAUTION]
>
>Adobe는 향후 클래식 UI를 개선할 계획이 없습니다. AEM 6.5에는 클래식 UI가 포함되어 있으며 이전 릴리스에서 업그레이드하는 고객은 있는 그대로 사용할 수 있습니다. 클래식 UI는 더 이상 사용하지 않을 때 완전히 지원된다는 점을 참고하십시오.[자세히 보기](/help/sites-deploying/ui-recommendations.md).

#### 검색 및 인덱싱 {#indexing-and-search}

* Oak에서의 검색이 이제 동적 패싯을 지원합니다. 예를 들어 자산 검색의 필터 레일은 예상 결과 양을 보여줍니다.
* 동적 패싯이 있는 결과를 제공하도록 QueryBuilder가 확장되었습니다.

#### 업그레이드 {#upgrade}

* AEM 6.5에 대한 직접 업그레이드는 AEM 6.2, 6.3 및 6.4를 실행하는 고객을 위해 지원됩니다. 즉각적인 업그레이드 위해 5.x 또는 6.0/6.1을 사용하는 고객은 먼저 6.4로 업그레이드한 다음 6.5로 업그레이드하거나 인스턴스 간에 AEM 6.5로 직접 컨텐츠를 전송하여 업그레이드해야 합니다.

#### 프로젝트 및 워크플로우 {#projects-and-workflows}

* 6.4에 도입된 새로운 워크플로우 모델 편집기는 워크플로우 단계에서 복사 및 게시, 변수 지원과 같은 다양한 작동과 개선된 OR 및 AND 분할이 포함되도록 개선되었습니다.

### [!DNL Experience Manager] 사이트 {#experience-manager-sites}

[AEM Sites 및 Add-ons](/help/release-notes/sites.md)의 전체 변경 사항 목록.

#### 관리된 단일 페이지 앱 {#managed-single-page-apps}

페이지 편집기는 컨텍스트 내에서 컨텐츠를 편집하고 클라이언트 측 렌더링 환경에서 작성/레이아웃하는 기능을 추가합니다([SPA 편집기](/help/sites-developing/spa-architecture.md)로 알려짐). JavaScript 프레임워크로 구축된 기존 단일 페이지 앱인 React 또는 Angular는 AEM SJ SDK로 확장되어 실무자들이 편집할 수 있습니다.

AEM 6.4 SP2의 일부로 처음 출시되었으며, AEM 6.5에서는 SPA 지원이 다음과 같은 기능을 제공합니다.

* 템플릿 편집기를 사용하여 SPA의 AEM 편집 가능 부분을 편집 및 구성합니다.
* 다중 사이트 관리를 사용하여 국가, 프랜차이즈 또는 화이트 레이블 SPA 경험을 생성합니다.

#### 헤드리스 컨텐츠 관리 {#headless-content-management}

AEM은 다양한 형식 및 다양한 스택 레벨에서 컨텐츠를 제공할 수 있습니다. 2008년부터 [Sling GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) 및 [POST Servlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html)에서 일부가 도입되었습니다. Content Services([Sling Model Exporter](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/develop-sling-model-exporter.html))가 AEM 6.3에서 도입되었으며, AEM 등록 SDK에서 단일 페이지 앱을 하이드레이팅하는 데 사용되는 방법입니다. [HTTP API for Assets](/help/assets/mac-api-assets.md)은 CRUD API이며, AEM 6.5에서 확장되었습니다.

새로운 HTTP API 기능:

* ](/help/assets/assets-api-content-fragments.md)HTTP API for Assets에 컨텐츠 조각[을 추가하여 조각을 생성, 업데이트, 읽기 및 삭제할 수 있습니다.
* [컨텐츠 조각 목록 코어 구성 요소](https://opensource.adobe.com/aem-core-wcm-components/library/content-fragment-list.html)를 사용하여 Content Services를 통해 컨텐츠 조각 목록을 노출합니다.
* [코어 구성 요소 라이브러리](https://opensource.adobe.com/aem-core-wcm-components/library.html)는 각 구성 요소에 대한 기본 Content Services JSON 출력을 표시합니다.

#### 화면 추가 기능 {#screens-add-on}

인터랙티브 키오스크에서 전자 간판에 이르는 모든 디지털 디스플레이에서 경험을 효율적으로 설계, 전달 및 최적화합니다.

**디자인**

* 컨텐츠 재사용을 위해 디지털 및 매장 내에서 경험과 컨텐츠를 통합합니다.
* 출시 지원을 통해 작성 및 승인/게시 워크플로우를 간소화합니다.
* SPA 편집기를 사용하여 풍부한 인터랙티브 경험을 편집하고 전달합니다.

**전달**

* 대형 간판 네트워크까지 확장할 수 있는 강력한 온라인 및 오프라인 작업(Smart Sync)으로 미디어 플레이어 지원을 확대합니다.

**최적화**

* 동적 자리 표시자를 사용하여 데이터 트리거된 컨텐츠 위치 또는 구성을 맞춤 설정합니다.
* Adobe Analytics를 AEM Screens Player에 통합하여 인사이트를 제공합니다.

AEM Screens 변경에 대한 자세한 내용은 [AEM Screens 사용자 안내서](https://docs.adobe.com/content/help/ko-KR/experience-manager-screens/user-guide/aem-screens-introduction.html)의 릴리스 노트를 참조하십시오.

### [!DNL Experience Manager Assets] {#experience-manager-assets}

[AEM 6.5 에셋 릴리스 정보](/help/release-notes/assets.md)의 전체 변경 내용 목록.

AEM 6.5에서는 AEM 사용자, DAM 역할 및 연관된 광고 및 마케팅 역할의 생산성을 향상시키기 위해 다음과 같은 기능과 개선 사항이 도입되었습니다.

#### Adobe Creative Cloud와 통합  {#integration-with-adobe-creative-cloud}

Photoshop, Illustrator 및 InDesign을 비롯한 Adobe Creative Cloud 애플리케이션으로 작업하는 창의적인 사용자를 위한 인앱 환경인 [Adobe Asset Link](https://helpx.adobe.com/kr/enterprise/using/adobe-asset-link.html) 도입으로 컨텐츠 작성 프로세스에서 광고 및 마케팅 담당자 간의 공동 작업을 간소화합니다. AEM 데스크탑 앱은 모든 파일 유형 및 데스크탑 애플리케이션을 사용하여 데스크탑에서 AEM의 에셋을 사용하여 작업하는 사용자의 요구 사항을 계속 지원합니다.

또한 AEM은 Adobe Stock과 통합되어 AEM Web UI에서 직접 Adobe Stock 자산을 찾아 미리 보고, 라이센스를 지정하거나 저장할 수 있습니다.

![Photoshop의 자산 링크 패널](/help/assets/assets/aem65-assetlink-photoshop.png)

#### 연결된 자산 {#connected-assets}

연결된 에셋 기능은 중앙 AEM Assets DAM 배포의 에셋을 활용해야 하는 다양한 AEM Sites 배포를 통해 대규모 배포를 대상으로 합니다. 이를 통해 다양한 Sites 배포에 대한 자산 제공의 효율성을 강화하는 동시에 중앙집중식으로 관리되는 자산에 대한 제어 기능을 개선할 수 있습니다.

### Dynamic Media {#dynamic-media}

Dynamic Media는 AEM Assets에서 향상된 리치 미디어 작성 및 전달 기능을 제공하여 몰입 및 맞춤화된 최신 경험을 제공합니다. 고품질의 단일 마스터 자산을 사용하면 고급 클라우드 렌더링, Smart Crop 및 업계 최고의 뷰어를 활용하여 업계 최고의 성능으로 가장 매력적인 경험을 제공할 수 있습니다.

새로운 기능은 다음과 같습니다.

* 360 비디오 및 VR 헤드셋 지원
* 사용자 지정 비디오 썸네일
* 향상된 액세스 가능성 지원
* 핫 링크 보호

#### 사용자 환경 및 검색 {#user-experience-and-search}

주요 개선 사항을 통해 동적 검색 패싯을 제공하여 올바른 자산을 신속하게 찾고, 폴더 또는 검색 결과에서 모든 자산을 선택하는 기능을 제공하여 여러 자산을 보다 효율적으로 관리할 수 있습니다.

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM 6.5 Forms에는 여러 가지 새로운 기능과 개선 사항이 제공됩니다. 주요 내용은 다음과 같습니다.

* 트랜잭션 보고서는 제출된 양식, 처리된 문서 및 렌더링된 문서의 수를 추적할 수 있습니다.
* 인터랙티브 통신에 대한 사용성 개선
* 적응형 양식의 클라우드 기반 디지털 서명
* AEM Sites 단일 페이지 애플리케이션(SPA)에 적응형 양식 및 인터랙리브 통신 포함
* AEM 워크플로우의 변수에 대한 지원
* 인터랙티브 통신에서 데이터 디스플레이 패턴 지원
* 적응형 양식 및 인터랙티브 통신 테이블 분류
* 양식 데이터 모델에서 입력 데이터 검증 자동화

새로운 기능 및 향상된 설명서 리소스에 대한 자세한 내용은 [AEM 6.5 Forms](/help/forms/using/whats-new.md)의 새로운 기능 및 개선 사항에 대한 요약을 참조하십시오.

### [!DNL Experience Manager Communities] {#communitiesreleasenotes}

AEM 6.5는 Communities에 새로운 기능 및 개선 사항을 추가합니다. 이 릴리스의 주요 내용은 다음과 같습니다.

* 사용자 생성 컨텐츠를 작성하는 동안 등록된 멤버 태그 지정(@mention)이 지원됩니다.
* 구성원 그룹에 대한 직접적인 대량 메시지 작성이 지원됩니다.
* 대량 조정 UI에서 사용자 지정 필터가 개발 및 추가됩니다. 태그별 필터링을 시연하는 [샘플 프로젝트](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)는 유사한 사용자 정의 필터를 개발하기 위한 기초로 사용할 수 있습니다.
* 향상된 대량 조정 UI와 함께 새 목록 보기가 제공됩니다.
* 단일 커뮤니티 관리자 대신 다른 커뮤니티 사이트 및 중첩 그룹에 대한 별도의 관리자를 지정할 수 있습니다.
* AEM 6.5 Communities의 지원 기능은 [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) 엔진을 지원합니다.
* 액세스 가능성 개선을 위해 지원 구성 요소에서 키보드 탐색을 지원합니다.
* MSRP 및 DSRP를 설정하는 중 Apache Solr 7.0이 지원됩니다.

변경 사항에 대한 자세한 목록은 [AEM 6.5 커뮤니티 릴리스 노트](/help/release-notes/communities-release-notes.md)를 참조하십시오.

### [!DNL Experience Manager Livefyre] {#experience-manager-livefyre}

Livefyre를 AEM 6.5 인스턴스와 통합할 수 있습니다. AEM[과 Livefyre를 통합하는 방법을 참조하십시오.](https://docs.adobe.com/content/help/en/experience-manager-64/administering/integration/livefyre.html)

### 고객 중심의 개발 {#leverage-customer-focused-development} 활용

Adobe는 고객 중심 개발 모델을 사용하여 고객이 사양, 개발 및 테스트 중에 개발 프로세스의 모든 단계에 기여할 수 있도록 합니다. 이 프로세스에 참여하신 모든 고객과 파트너에게 감사의 인사를 드립니다.

Adobe는 고객 중심 버그 해결 및 개선 요청 개발의 수집, 우선 순위 지정 및 추적을 위한 절차와 프로세스를 마련했습니다. [Adobe Marketing Cloud 지원 포털](https://helpx.adobe.com/kr/contact/enterprise-support.ec.html)은 Adobe 개선 및 결함 추적 시스템과 통합됩니다. 고객 문의는 가능한 경우 고객 지원 센터에서 식별 및 해결합니다. R&amp;D로 에스컬레이션하면 모든 고객 정보가 캡처되고 우선 순위 지정 및 보고용으로 사용됩니다. 개발 시에는 유료 지원, 보증 문제 및 고객 유료 향상 기능이 우선 제공됩니다.

이러한 우선 순위 지정 프로세스를 통해 750가지 이상의 고객 중심 변경 사항이 AEM 6.5에서 수정되었습니다.

## 릴리스의 일부인 파일 목록  {#list-of-files-that-are-part-of-the-release}

**Foundation**

* 독립형 빠른 시작:`cq-quickstart-6.5.0.jar`.
* 응용 프로그램 서버 빠른 시작:`cq-quickstart-6.5.0.war`.
* 다양한 웹 서버 및 플랫폼용 Dispatcher 4.3.2 이상 [다운로드 링크](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/getting-started/release-notes.html)를 참조하십시오.
* Eclipse IDE용 플러그인([자세히 보기 및 다운로드](/help/sites-developing/aem-eclipse.md))

* 괄호 코드 편집기 확장([자세히 보기 및 다운로드](/help/sites-developing/aem-brackets.md))
* Maven/Gradle 종속성([다운로드 링크](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/aem/uber-jar/6.5.0/))

**사이트**

* 쿠어 구성 요소([GitHub 프로젝트](https://github.com/adobe/aem-core-wcm-components))
* We.Retail 참조 구현([자세히 보기](/help/sites-developing/we-retail.md))
* Maven Project Archetypes:

   * 전체 스택 사이트: [GitHub 프로젝트](https://github.com/adobe/aem-project-archetype)
   * React/Angular의 단일 페이지 앱: [GitHub 프로젝트](https://github.com/adobe/aem-spa-project-archetype)

* 다양한 대상 플랫폼에 대한 AEM Screens Players([다운로드](https://download.macromedia.com/screens/))

* 스마트 컨텐츠 언어 모델입니다. 영어는 사전 설치되어 있으며 더 많은 언어를 다운로드할 수 있습니다.

   * [독일어](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [스페인어](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [이탈리아어](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [프랑스어](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* AEM Modernize Tools 제품군(예: 대화 상자 변환 도구) ([GitHub 프로젝트](https://github.com/adobe/aem-modernize-tools))

**자산**

* 확장된 PDF Rasterizer 추가 패키지([자세히 보기](/help/assets/aem-pdf-rasterizer.md))
* 확장된 RAW 이미지 지원 추가 패키지([자세히 보기](/help/assets/camera-raw.md))

**양식**

* ](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html)AEM Forms 기능 패키지[
* [AEM Forms OSGi Client SDK](https://repo.adobe.com/nexus/content/repositories/public/com/adobe/aemfd/aemfd-client-sdk/6.0.80/)

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

## {#install-update} 설치 및 업데이트

설치 요구 사항은 [설치 지침](/help/sites-deploying/custom-standalone-install.md)을 참조하십시오.

자세한 내용은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하십시오.

## 지원되는 플랫폼 {#supported-platforms}

지원 수준을 포함한 지원되는 플랫폼의 전체 매트릭스를 [AEM 6.5 기술 요구 사항](/help/sites-deploying/technical-requirements.md)에서 확인하십시오.

>[!NOTE]
>
>Oracle은 Oracle Java SE 제품에 대한 LTS(Long Term Support) 모델로 옮겨졌습니다. Java 9 및 10은 Oracle에서 제공하는 비LTS 릴리스입니다.[Oracle Java SE 지원 로드맵](https://www.oracle.com/technetwork/java/eol-135779.html)을 참조하십시오. Adobe은 프로덕션에서 AEM만 실행할 수 있도록 Java의 LTS 릴리스를 지원합니다. Java 11은 AEM 6.5와 함께 사용하는 데 권장되는 버전입니다.

## 더 이상 사용되지 않는 및 제거된 기능 {#deprecated-and-removed-features}

Adobe는 제품 기능을 지속적으로 평가하고 시간이 흘러도 더욱 강력한 버전으로 기능을 대체할 계획을 세우거나 이후 기대치나 확장에 효율적으로 대비할 수 있도록 선택된 부분을 재구현할 수 있습니다.

[!DNL Adobe Experience Manager] 6.5의 경우 [더 이상 사용되지 않고 제거된 기능 목록](/help/release-notes/deprecated-removed-features.md)을 읽으십시오. 또한 이 페이지에는 예정된 변경 사항에 대한 사전 공지 및 이전 릴리스에서 업데이트하는 고객을 위한 중요 알림이 포함되어 있습니다.

## 알려진 문제 {#known-issues}

](/help/release-notes/known-issues.md)알려진 문제 목록[

### 제품 다운로드 및 지원(제한됨 사이트)  {#product-download-and-support-restricted-sites}

다음 사이트는 고객만 사용할 수 있습니다. 액세스가 필요한 고객의 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/).

* [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 추가 기능을 위한 제품 업데이트, 패치 및 패키지.

* [Admin Console을 통한 고객 지원](https://adminconsole.adobe.com/). 자세한 내용은 [새 Adobe 고객 지원 경험](https://docs.adobe.com/content/help/ko-KR/customer-one/using/home.html)을 참조하십시오.
