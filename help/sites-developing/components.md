---
title: 구성 요소 개요
seo-title: 구성 요소
description: 구성 요소는 웹 사이트에 컨텐츠를 제공하기 위한 특정 기능을 구현하는 모듈형 유닛입니다
seo-description: 구성 요소는 웹 사이트에 컨텐츠를 제공하기 위한 특정 기능을 구현하는 모듈형 유닛입니다
uuid: fb39aeb8-8f43-4091-8083-ebfab89e6e63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 45efff93-2fe5-4313-83a0-0e23a540da93
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 17%

---


# 구성 요소 개요{#components-overview}

이 페이지에서는 페이지 작성에 사용되는 [과 같은 Adobe Experience Manager(AEM) 구성 요소에 대한 개요를 제공합니다](/help/sites-authoring/default-components-foundation.md).

## 구성 요소란?{#what-exactly-is-a-component}

* 웹 사이트에 컨텐츠를 제공하기 위한 특정 기능을 실현하는 모듈형 유닛
* 재사용
* 저장소의 한 폴더 내에 독립된 단위로 개발되었습니다.
* 숨겨진 구성 파일이 없습니다.
* 다른 구성 요소를 포함할 수 있습니다.
* 모든 AEM 시스템 내에서 어디에서나 실행할 수 있습니다. 특정 구성 요소에서 실행되도록 제한할 수도 있습니다.
* 사용자 인터페이스가 표준화되었습니다.
* 구성할 수 있는 편집 비헤이비어가 있어야 합니다.
* [MOCK] Use dialog box that are built using sub-elements based on Granite UI components
* [HTL](https://docs.adobe.com/content/help/ko-KR/experience-manager-htl/using/overview.html)(권장) 또는 JSP를 사용하여 개발됩니다.
* 기본 기능을 확장하는 사용자 지정된 구성 요소를 만들기 위해 개발할 수 있습니다.

구성 요소는 모듈이므로 다음을 수행할 수 있습니다.

* 로컬 인스턴스에서 새 구성 요소를 개발합니다.
* 테스트 환경에 배포합니다.
* 작성자 및/또는 관리자가 컨텐츠를 추가하고 구성할 수 있는 라이브 제작 환경에 배포합니다.
* 웹 사이트 방문자의 컨텐츠를 렌더링하는 데 사용되는 라이브 게시 환경에 배포합니다. 커뮤니티 등의 특정 구성 요소도 사용자의 입력을 받아들입니다.

각 AEM 구성 요소:

* 리소스 유형입니다.
* 특정 기능을 완벽하게 구현하는 스크립트 모음입니다.
* AEM 또는 포털 내의 것을 의미하는 *격리*&#x200B;에서 사용할 수 있습니다.

## AEM {#out-of-the-box-components-within-aem} 내 기본 구성 요소

AEM에는 다음과 같은 포괄적인 기능을 제공하는 다양한 [즉시 사용 가능한 구성 요소](/help/sites-authoring/default-components.md)가 포함되어 있습니다.

* 단락 시스템 ( `parsys`)
* 페이지( `responsivegrid` - 터치 지원 UI만 해당)
* 텍스트
* 이미지, 텍스트 포함
* 도구 모음

제공된 구성 요소 및 [샘플 We.Retail 웹 사이트](/help/sites-developing/we-retail.md)에서 해당 사용은 구성 요소를 구현하고 사용하는 방법을 보여줍니다. 구성 요소는 모든 소스 코드와 함께 제공되며, 수정하거나 확장된 구성 요소의 시작점으로 사용할 수 있습니다.

### 핵심 구성 요소 및 기본 구성 요소 {#core-components-and-foundation-components}

두 가지 Adobe 제공 AEM 구성 요소 세트가 있습니다.

* [코어 구성 요소](https://docs.adobe.com/content/help/ko-KR/experience-manager-core-components/using/introduction.html)
* [기초 구성 요소](/help/sites-authoring/default-components-foundation.md)

**핵심** 구성 요소는 AEM 6.3에서 도입되었으며 유연하고 기능이 풍부한 저작 기능을 제공합니다. [We.Retail 참조 사이트](/help/sites-developing/we-retail.md)에서는 핵심 구성 요소를 사용할 수 있는 방법을 보여 주고, 구성 요소 개발의 현재 모범 사례를 나타냅니다.

**Foundation** Component는 다양한 버전의 AEM에서 사용할 수 있으며 표준 AEM 설치에서 바로 사용할 수 있습니다. 여전히 지원되지만, 대부분은 더 이상 사용되지 않으며, 더 이상 향상된 기능이 없으며, 기존 기술을 기반으로 합니다.

>[!NOTE]
>
>[핵심 ](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) 구성 요소는 구성 요소 디자인 및 개발에 대한 최신 모범 사례를 나타내며 참조 구현 역할을 제공합니다.
>
>[AEM 현대화 ](modernization-tools.md) 도구 검색을 통해 핵심 구성 요소로 마이그레이션할 수 있습니다.

### 사용 가능한 구성 요소 보기 {#viewing-available-components}

AEM 인스턴스에서 사용 가능한 모든 구성 요소에 대한 개요를 보려면 [구성 요소 콘솔](/help/sites-authoring/default-components-console.md)을 사용하십시오.

또는 CRXDE Lite을 사용하여 저장소에서 사용 가능한 모든 구성 요소 목록을 가져올 수도 있습니다.

1. **[!UICONTROL CRXDE Lite]**&#x200B;의 도구 모음에서 **[!UICONTROL 도구]**&#x200B;를 선택한 다음 **[!UICONTROL 쿼리]**&#x200B;를 선택하면 **[!UICONTROL 쿼리]** 탭이 열립니다.

1. **[!UICONTROL 쿼리]** 탭에서 `XPath`을 **[!UICONTROL 유형]**&#x200B;으로 선택합니다.

1. **[!UICONTROL 쿼리]** 입력 필드에 다음 문자열을 입력합니다.

   `//element(*, cq:Component)`

1. **[!UICONTROL 실행]**&#x200B;을 클릭하면 구성 요소가 나열됩니다.

## 추가 리소스 {#further-reading}

다음 페이지에서는 이러한 구성 요소 및 기타 구성 요소 개발에 대한 자세한 정보를 제공합니다.

* [AEM 구성 요소 - 기본 사항](/help/sites-developing/components-basics.md)
* [AEM 구성 요소 개발](/help/sites-developing/developing-components.md)
* [AEM 구성 요소 개발 - 코드 샘플](/help/sites-developing/developing-components-samples.md)
* [여러 즉석 편집기 구성](/help/sites-developing/multiple-inplace-editors.md)
* [개발자 모드](/help/sites-developing/developer-mode.md)
* [UI 테스트](/help/sites-developing/hobbes.md)
* [컨텐츠 조각용 구성 요소](/help/sites-developing/components-content-fragments.md)
* [JSON 형식으로 페이지 정보 얻기](/help/sites-developing/pageinfo.md)
* [구성 요소 다국어화](/help/sites-developing/i18n.md)
* [코어 구성 요소](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html)
* [숨기기 조건 사용](/help/sites-developing/hide-conditions.md)
* 클래식 UI

   * [AEM 구성 요소(클래식 UI)](/help/sites-developing/developing-components-classic.md)
   * [위젯 사용 및 확장(클래식 UI)](/help/sites-developing/widgets.md)
   * [xtype 사용(클래식 UI)](/help/sites-developing/xtypes.md)
   * [양식 개발(클래식 UI)](/help/sites-developing/developing-forms.md)

