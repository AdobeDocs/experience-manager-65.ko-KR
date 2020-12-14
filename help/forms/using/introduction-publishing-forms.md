---
title: 포털에서 양식 게시 소개
seo-title: 포털에서 양식 게시 소개
description: AEM Forms은 양식 포털을 구축할 때 사용할 수 있는 구성 요소를 제공합니다. 이 문서에서는 사용 가능한 양식 포털 구성 요소에 대해 설명합니다.
seo-description: AEM Forms은 양식 포털을 구축할 때 사용할 수 있는 구성 요소를 제공합니다. 이 문서에서는 사용 가능한 양식 포털 구성 요소에 대해 설명합니다.
uuid: 658de12b-66e5-438b-ae8f-872ec11a9c3e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9f1beb89-8eb1-4e37-a5e8-19752b21374a
docset: aem65
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 0%

---


# 포털{#introduction-to-publishing-forms-on-a-portal}에 양식 게시 소개

## AEM Forms 포털 구성 요소 개요 {#aem-forms-portal-components-overview}

일반적인 양식 중심의 포털 배포 시나리오에서는 양식 개발 및 포털 개발이 두 가지 분리된 활동입니다. 양식 디자이너는 양식을 디자인하고 저장소에 저장하지만 웹 개발자는 양식을 나열하고 양식 제출을 처리하는 웹 애플리케이션을 만듭니다. Forms은 양식 저장소와 웹 애플리케이션 간에 커뮤니케이션이 없으므로 웹 티어로 복사됩니다.

이러한 시나리오는 종종 관리 문제와 제작 지연을 초래합니다. 예를 들어 저장소에서 사용할 수 있는 양식의 최신 버전이 있는 경우 웹 계층에서 양식을 교체하고 웹 응용 프로그램을 수정하고 공개 사이트에 양식을 다시 배포해야 합니다. 웹 응용 프로그램을 다시 배포하면 일부 서버 다운타임이 발생할 수 있습니다. 일반적으로 서버 다운타임은 계획된 작업이므로 변경 사항을 즉시 공개 사이트로 푸시할 수 없습니다.

AEM Forms은 관리 오버헤드 및 제작 지연을 줄이는 포털 구성 요소를 제공합니다. 웹 개발자는 이 구성 요소를 사용하여 AEM(Adobe Experience Manager)을 사용하여 제작한 웹 사이트에서 양식 포털을 만들고 사용자 정의할 수 있습니다.

![AEM Forms 포털](assets/aem-forms-portal.png)

양식 포털 구성 요소를 사용하면 다음 기능을 추가할 수 있습니다.

* 사용자 정의된 레이아웃에 양식을 나열합니다. 즉시 사용 가능한 레이아웃, 목록 보기, 카드 보기 및 패널 보기 레이아웃이 제공됩니다. 자신만의 레이아웃을 만들 수 있습니다.
* 사용자 지정 메타데이터와 사용자 지정 작업을 나열하는 동안 표시할 수 있습니다.
* Forms Portal 구성 요소가 사용 중인 게시 인스턴스에 AEM Forms UI에서 게시한 양식을 나열합니다.
* 최종 사용자가 HTML 및 PDF 포맷으로 양식을 렌더링할 수 있습니다.
* 사용자 정의 HTML 프로필을 사용하여 양식을 렌더링합니다.
* 양식 속성, 메타데이터 및 태그와 같은 다양한 기준을 기반으로 양식을 검색할 수 있습니다.
* 양식 데이터를 서블릿에 제출합니다.
* 맞춤형 CSS를 사용하여 포털의 모양과 느낌을 사용자 정의할 수 있습니다.
* 양식에 대한 링크를 만듭니다.
* 최종 사용자가 만든 응용 양식과 관련된 초안 및 제출 목록을 나열합니다.

## 사용 가능한 AEM Forms 포털 구성 요소 {#available-aem-forms-portal-components}

AEM Forms은 **Document Services** 및 **Document Services 설명** 구성 요소 그룹 아래에 그룹화된 다음 포털 구성 요소를 즉시 제공합니다.

### 검색 및 목록 작성자 {#search-amp-lister}

Search &amp; Lister 구성 요소를 사용하면 양식 저장소의 양식을 포털 페이지로 나열하고 지정된 기준에 따라 양식을 나열하는 구성 옵션을 제공합니다. 또한 포털 사용자가 양식 목록에서 검색할 수 있도록 검색 기준을 지정할 수 있습니다.

### 초안 및 제출 {#drafts-amp-submissions}

Search &amp; Lister 구성 요소는 Forms 작성자가 공개한 양식을 표시하지만 초안 및 제출 구성 요소는 나중에 작성한 양식을 작성하기 위해 초안으로 저장한 양식을 표시합니다. 이 구성 요소는 로그인한 모든 사용자에게 개인화된 환경을 제공합니다.

### 링크 {#link}

링크 구성 요소를 사용하면 페이지의 아무 곳이나 양식에 대한 링크를 만들 수 있습니다. 교육 프로그램을 제공할 경우 사용자가 교육 등록을 위한 양식을 제출하도록 하는 시나리오를 생각해 보십시오. 웹 사이트에서 프로그램 세부 정보를 게시했습니다. 세부 사항 아래에서는 등록 양식에 대한 링크를 제공합니다. 링크 구성 요소를 사용하면 해당 링크를 만들 수 있습니다.

## Forms 포털 워크플로 {#forms-portal-workflow}

Forms 포털을 통해 양식 저장소의 양식을 포털 페이지로 나열할 수 있습니다. 또한 포털 사용자가 양식 목록에서 검색할 수 있도록 검색 기준을 지정할 수 있습니다. 초안 및 제출 구성 요소를 사용하여 나중에 제출한 양식을 작성하기 위해 초안으로 저장한 양식을 표시할 수도 있습니다. 이러한 기능을 사이트 페이지에서 사용할 수 있으려면 먼저 특정 작업 세트를 수행해야 합니다. 나열된 시퀀스의 단계를 수행하여 사이트 페이지에서 구성 요소 및 각 기능을 사용할 수 있도록 합니다.

1. **Forms Portal 구성 요소** 활성화:기본적으로 양식 포털 구성 요소는 사용할 수 없습니다. [AEM Sites 페이지에 대해 AEM ](/help/forms/using/enabling-forms-portal-components.md) 사이드 킥의 구성 요소를 활성화합니다.
1. **페이지에 양식 나열(양식 포털 페이지 만들기): AEM Sites 및 AEM이 아닌 사이트 페이지 모두에서 양식을** 표시할 수 있습니다. 목록에는 게시 인스턴스에서 사용할 수 있는 양식이 포함되어 있습니다. 사용자는 양식을 열고 양식을 채울 수 있습니다. 사용자가 양식을 열 때마다 양식의 새 인스턴스가 만들어집니다.

   1. **AEM Sites 페이지에 양식** 나열:페이지에  **[검색 및](../../forms/using/creating-form-portal-page.md)** 라이브러리 구성 요소를 추가하고 목록  **[패널을 구성하여](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** 페이지에 양식을 나열합니다. **검색 창** 구성 요소를 **검색 및 작성자** 구성 요소에 추가 및 구성하여 검색 기능을 페이지에 추가합니다. 양식 포털 구성 요소가 있는 페이지를 [양식 포털 페이지](../../forms/using/creating-form-portal-page.md)라고 합니다.

   1. **AEM Sites이 아닌 페이지에 양식** 표시:  [양식 포털 검색 ](/help/forms/using/listing-forms-webpage-using-apis.md) API를 사용하여 AEM Sites 이외의 페이지에 양식을 쿼리, 검색 및 나열합니다.

1. **양식 포털 페이지에 초안 및 제출된 양식을 나열합니다**.양식 포털 페이지에 초안 및 제출 구성 요소를 추가하고 구성합니다. 구성 요소에는 초안 상태에 있는 모든 양식과 이미 제출된 양식이 나열됩니다.

   제출된 적응형 양식이 제출 탭에 표시되도록 하려면 **Submit action**&#x200B;을 **[Forms Portal 제출 작업](configuring-submit-actions.md)으로 설정합니다.** 또는 Forms Portal 제출 옵션을 활성화합니다. 사용자가 양식을 제출할 때마다 제출 탭에 양식이 추가됩니다.

1. **초안 및 제출된 양식 데이터의 저장소 구성:** 기본적으로 초안 및 제출 데이터는 AEM 저장소에 저장됩니다. 제작 환경에서는 초안 또는 제출된 양식 데이터를 AEM 저장소에 저장하지 않는 것이 좋습니다. [양식 포털 구성 요소를 구성하여 데이터를 보안 위치에 저장합니다](../../forms/using/draft-submission-component.md#customizing-the-storage).
1. **(선택 사항) 양식 포털 구성 요소 사용자 정의:** [양식 포털 페이지 ](../../forms/using/customizing-templates-forms-portal-components.md) 템플릿을 사용자 정의하여 구성 요소에 독특한 모양을 제공합니다.
1. **(선택 사항) 양식에 사용자 정의 메타데이터 추가:** [사용자 정의 메타데이터를 양식에 ](../../forms/using/customizing-templates-forms-portal-components.md) 추가하여 목록 및 검색 경험을 향상시킬 수 있습니다.
1. **양식 포털 페이지 게시:** 이제 양식 포털 페이지가 준비되었습니다. 페이지를 게시합니다.

## 관련 아티클 {#related-articles}

* [양식 포털 구성 요소 활성화](/help/forms/using/enabling-forms-portal-components.md)
* [양식 포털 페이지 만들기](../../forms/using/creating-form-portal-page.md)
* [API를 사용하여 웹 페이지에 양식 목록 표시](/help/forms/using/listing-forms-webpage-using-apis.md)
* [초안 및 제출 구성 요소 사용](../../forms/using/draft-submission-component.md)
* [초안 및 제출된 양식의 저장 영역 사용자 정의](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [초안 및 제출 구성 요소를 데이터베이스와 통합하는 샘플](integrate-draft-submission-database.md)
* [양식 포털 구성 요소에 대한 템플릿 사용자 정의](../../forms/using/customizing-templates-forms-portal-components.md)
* [포털에서 양식 게시 소개](../../forms/using/introduction-publishing-forms.md)

