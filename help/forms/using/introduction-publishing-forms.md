---
title: 포털에서 양식 게시 소개
seo-title: Introduction to publishing forms on a portal
description: AEM Forms은 forms 포털을 구축하는 데 사용할 수 있는 구성 요소를 제공합니다. 이 문서에서는 사용 가능한 양식 포털 구성 요소를 소개합니다.
seo-description: AEM Forms provides with components that you can use to build your forms portal. This articles introduces you to the available forms portal components.
uuid: 658de12b-66e5-438b-ae8f-872ec11a9c3e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9f1beb89-8eb1-4e37-a5e8-19752b21374a
docset: aem65
exl-id: 240ed4d8-b21b-46eb-80a9-9e8093b77235
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 0%

---

# 포털에서 양식 게시 소개{#introduction-to-publishing-forms-on-a-portal}

## AEM Forms 포털 구성 요소 개요 {#aem-forms-portal-components-overview}

일반적인 양식 중심의 포털 배포 시나리오에서 양식 개발 및 포털 개발은 두 가지 서로 다른 작업입니다. Form Designer가 양식을 디자인하고 저장소에 저장하는 동안 Web Developers에서 양식을 나열하고 양식 제출을 처리하는 웹 응용 프로그램을 만듭니다. Forms은 forms 리포지토리와 웹 애플리케이션 간에 통신이 없으므로 웹 계층에 복사됩니다.

이러한 시나리오는 종종 관리 문제와 프로덕션 지연을 초래합니다. 예를 들어 리포지토리에서 사용할 수 있는 최신 버전의 양식이 있는 경우 웹 계층의 양식을 바꾸고 웹 응용 프로그램을 수정한 다음 공용 사이트에서 양식을 재배포해야 합니다. 웹 응용 프로그램을 다시 배포하면 서버 다운타임이 발생할 수 있습니다. 일반적으로 서버 다운타임은 계획된 활동이므로 변경 사항을 즉시 공용 사이트에 푸시할 수 없습니다.

AEM Forms은 관리 오버헤드 및 프로덕션 지연을 줄이는 포털 구성 요소를 제공합니다. 이 구성 요소는 AEM(Adobe Experience Manager)을 사용하여 작성된 웹 사이트에서 양식 포털을 만들고 사용자 지정할 수 있도록 웹 개발자를 제공합니다.

![AEM Forms 포털](assets/aem-forms-portal.png)

양식 포털 구성 요소를 사용하면 다음 기능을 추가할 수 있습니다.

* 양식을 사용자 지정된 레이아웃으로 나열합니다. 즉시 사용 가능한 목록 보기, 카드 보기 및 패널 보기 레이아웃이 제공됩니다. 자신만의 사용자 정의 레이아웃을 만들 수 있습니다.
* 사용자 지정 메타데이터와 사용자 지정 작업을 나열하는 동안 표시할 수 있습니다.
* Forms Portal 구성 요소가 사용되는 게시 인스턴스에 AEM Forms UI에서 게시한 양식을 나열합니다.
* 최종 사용자가 HTML 형식뿐만 아니라 PDF 형식으로 양식을 렌더링할 수 있도록 허용합니다.
* 양식을 렌더링하려면 사용자 지정 HTML 프로필을 사용하십시오.
* 양식 속성, 메타데이터 및 태그와 같은 다양한 기준에 따라 양식을 검색할 수 있도록 설정합니다.
* 서블릿에 양식 데이터를 제출합니다.
* 사용자 지정 CSS를 사용하여 포털의 모양과 느낌을 사용자 지정합니다.
* 양식에 대한 링크를 만듭니다.
* 최종 사용자가 만든 적응형 양식과 관련된 초안 및 제출을 나열합니다.

## 사용 가능한 AEM Forms 포털 구성 요소 {#available-aem-forms-portal-components}

AEM Forms은 다음과 같이 그룹화된 기본 제공 포털 구성 요소를 제공합니다 **문서 서비스** 및 **문서 서비스 설명** 구성 요소 그룹:

### 검색 및 목록 작성자 {#search-amp-lister}

Search &amp; Lister 구성 요소를 사용하면 양식 리포지토리의 양식을 포털 페이지로 나열할 수 있으며, 지정된 기준에 따라 양식을 나열하는 구성 옵션을 제공합니다. 또한 포털 사용자가 양식 목록에서 검색할 수 있도록 검색 기준을 지정할 수 있습니다.

### 초안 및 제출 {#drafts-amp-submissions}

Search &amp; Lister 구성 요소는 Forms 작성자가 공개한 양식을 표시하는 동안 초안 및 제출 구성 요소는 나중 및 제출된 양식을 완료하기 위해 초안으로 저장된 양식을 표시합니다. 이 구성 요소는 로그인한 모든 사용자에게 개인화된 경험을 제공합니다.

### 링크 {#link}

링크 구성 요소를 사용하면 페이지의 어디에나 양식에 대한 링크를 만들 수 있습니다. 교육 프로그램을 제공하는 시나리오를 생각해 보십시오. 사용자가 교육 등록 양식을 제출하도록 하십시오. 웹 사이트에서는 프로그램 세부 사항을 게시했습니다. 세부 사항 아래에서 등록 양식에 링크를 제공하려고 합니다. 링크 구성 요소는 해당 링크를 만드는 데 도움이 될 수 있습니다.

## Forms 포털 워크플로우 {#forms-portal-workflow}

Forms 포털 을 사용하면 양식 리포지토리의 양식을 포털 페이지로 나열할 수 있습니다. 또한 포털 사용자가 양식 목록에서 검색할 수 있도록 검색 기준을 지정할 수 있습니다. 초안 및 제출 구성 요소를 사용하여 나중 및 제출된 양식을 완료하기 위한 초안으로 저장된 양식을 표시할 수도 있습니다. 사이트 페이지에서 이러한 기능을 사용할 수 있으려면 먼저 특정 작업 세트를 수행해야 합니다. 나열된 순서로 단계를 수행하여 구성 요소 및 각 기능을 사이트 페이지에서 사용할 수 있도록 합니다.

1. **Forms Portal 구성 요소 활성화**: 기본적으로 forms 포털 구성 요소는 사용할 수 없습니다. [AEM 사이드 킥에서 구성 요소를 활성화합니다](/help/forms/using/enabling-forms-portal-components.md) AEM Sites 페이지.
1. **페이지에 양식 나열(forms portal 페이지 만들기):** AEM Sites 페이지와 AEM이 아닌 사이트 페이지 모두에 양식을 나열할 수 있습니다. 목록에는 게시 인스턴스에서 사용할 수 있는 양식이 포함되어 있습니다. 사용자는 양식을 열고 양식을 채울 수 있습니다. 사용자가 양식을 열 때마다 양식의 새 인스턴스가 만들어집니다.

   1. **AEM Sites 페이지에 양식 나열**: 추가 **[검색 및 목록](../../forms/using/creating-form-portal-page.md)** 구성 요소를 페이지에 구성 하여 **[목록 창](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** 이 보기에서 페이지에 양식을 나열하려면 다음을 수행하십시오. 추가 및 구성 **검색 창** 구성 요소를 **검색 및 목록** 구성 요소를 사용하여 페이지에 검색 기능을 추가할 수도 있습니다. Forms 포털 구성 요소가 있는 페이지를 다음과 같이 합니다. [forms 포털 페이지](../../forms/using/creating-form-portal-page.md).

   1. **AEM Sites이 아닌 페이지에 양식 나열:** 를 사용하십시오 [forms 포털 검색 API](/help/forms/using/listing-forms-webpage-using-apis.md) AEM Sites이 아닌 페이지에서 양식을 쿼리, 검색 및 나열하려면 다음을 수행하십시오.

1. **양식 포털 페이지에 초안 및 제출된 양식 나열**: Forms 포털 페이지에 초안 및 제출 구성 요소를 추가하고 구성합니다. 구성 요소에는 초안 상태에 있는 모든 양식과 이미 제출된 양식이 나열됩니다.

   제출된 적응형 양식이 제출 탭에 표시되도록 하려면 **작업 제출** to **[Forms 포털 제출 작업](configuring-submit-actions.md).** 또는 Forms Portal 제출 옵션을 활성화합니다. 사용자가 양식을 제출할 때마다 양식이 제출 탭에 추가됩니다.

1. **초안 및 제출된 양식 데이터에 대한 저장 공간을 구성합니다.** 기본적으로 초안 및 제출 데이터는 AEM 저장소에 저장됩니다. 프로덕션 환경에서는 초안 또는 제출된 양식 데이터를 AEM 저장소에 저장하지 않는 것이 좋습니다. [데이터를 보안 위치에 저장하도록 forms 포털 구성 요소 구성](../../forms/using/draft-submission-component.md#customizing-the-storage).
1. **(선택 사항) Forms 포털 구성 요소 사용자 지정:** [양식 포털 페이지 템플릿 사용자 지정](../../forms/using/customizing-templates-forms-portal-components.md) 그 구성요소들의 독특한 모양을 제공하다.
1. **(선택 사항) 양식에 사용자 지정 메타데이터를 추가합니다.** [양식에 사용자 지정 메타데이터 추가](../../forms/using/customizing-templates-forms-portal-components.md) 목록 및 검색 경험을 개선합니다.
1. **양식 포털 페이지를 게시합니다.** 이제 양식 포털 페이지를 사용할 수 있습니다. 페이지를 게시합니다.

## 관련 문서 {#related-articles}

* [Forms 포털 구성 요소 활성화](/help/forms/using/enabling-forms-portal-components.md)
* [Forms 포털 만들기 페이지](../../forms/using/creating-form-portal-page.md)
* [API를 사용하여 웹 페이지의 양식 나열](/help/forms/using/listing-forms-webpage-using-apis.md)
* [초안 및 제출 구성 요소 사용](../../forms/using/draft-submission-component.md)
* [초안 및 제출된 양식의 저장 공간 사용자 정의](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [초안 및 제출 구성 요소와 데이터베이스를 통합하기 위한 샘플](integrate-draft-submission-database.md)
* [Forms 포털 구성 요소에 대한 템플릿 사용자 지정](../../forms/using/customizing-templates-forms-portal-components.md)
* [포털에서 양식 게시 소개](../../forms/using/introduction-publishing-forms.md)
