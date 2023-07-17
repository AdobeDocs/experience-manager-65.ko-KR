---
title: 포털에 양식 게시 소개
description: Adobe Experience Manager Forms은 Forms 포털을 빌드하는 데 사용할 수 있는 구성 요소를 제공합니다. 이 문서에서는 사용 가능한 Forms 포털 구성 요소를 소개합니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: 240ed4d8-b21b-46eb-80a9-9e8093b77235
source-git-commit: 60924e7ee204e43a2ff833fbc394beca8db9c9d9
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 0%

---

# 포털에 양식 게시 소개{#introduction-to-publishing-forms-on-a-portal}

## AEM Forms 포털 구성 요소 개요 {#aem-forms-portal-components-overview}

일반적인 양식 중심의 포털 배포 시나리오에서 양식 개발 및 포털 개발은 두 가지 단절 활동입니다. 양식 디자이너는 리포지토리에서 양식을 디자인하고 저장하는 동안 웹 개발자는 양식을 나열하고 양식 제출을 처리하는 웹 응용 프로그램을 만듭니다. 양식 저장소와 웹 애플리케이션 간에 통신이 없으므로 Forms이 웹 계층에 복사됩니다.

이러한 시나리오는 종종 관리 문제와 생산 지연을 초래합니다. 예를 들어 저장소에서 최신 버전의 양식을 사용할 수 있는 경우 웹 계층에서 양식을 바꾸고 웹 응용 프로그램을 수정한 다음 공개 사이트에서 양식을 재배포해야 합니다. 웹 애플리케이션을 다시 배포하면 일부 서버 다운타임이 발생할 수 있습니다. 일반적으로 서버 다운타임은 계획된 작업이므로 변경 사항을 즉시 공개 사이트로 푸시할 수 없습니다.

AEM Forms은 관리 오버헤드와 프로덕션 지연을 줄이는 포털 구성 요소를 제공합니다. 구성 요소를 사용하면 웹 개발자가 Adobe Experience Manager(AEM)를 사용하여 작성된 웹 사이트에서 Forms 포털을 만들고 사용자 지정할 수 있습니다.

![AEM Forms 포털](assets/aem-forms-portal.png)

양식 포털 구성 요소를 사용하여 다음 기능을 추가할 수 있습니다.

* 사용자 지정된 레이아웃의 목록 양식입니다. 기본적으로 목록 보기, 카드 보기 및 패널 보기 레이아웃이 제공됩니다. 자신만의 사용자 지정 레이아웃을 만들 수 있습니다.
* 목록을 작성하는 동안 사용자 지정 메타데이터 및 사용자 지정 작업을 표시할 수 있습니다.
* AEM Forms Portal 구성 요소가 사용 중인 게시 인스턴스에 Forms UI에서 게시한 목록 양식입니다.
* 최종 사용자가 양식을 HTML 및 PDF 형식으로 렌더링할 수 있도록 허용합니다.
* 사용자 지정 HTML 프로필을 사용하여 양식을 렌더링합니다.
* 양식 속성, 메타데이터 및 태그와 같은 다양한 기준을 기반으로 양식 검색을 활성화합니다.
* 서블릿에 양식 데이터를 제출합니다.
* 사용자 지정 CSS를 사용하여 포털의 모양과 느낌을 사용자 지정합니다.
* 양식에 대한 링크를 만듭니다.
* 최종 사용자가 만든 적응형 양식과 관련된 초안 및 제출을 나열합니다.

## 사용 가능한 AEM Forms 포털 구성 요소 {#available-aem-forms-portal-components}

AEM Forms은 다음과 같은 포털 구성 요소를 즉시 제공하며 **문서 서비스** 및 **문서 서비스 조건자** 구성 요소 그룹:

### Search &amp; Lister {#search-amp-lister}

검색 및 목록 구성 요소를 사용하면 양식 저장소에서 포털 페이지로 양식을 나열할 수 있고 지정된 기준에 따라 양식을 나열하는 구성 옵션을 제공할 수 있습니다. 또한 포털 사용자가 양식 목록에서 검색할 수 있도록 검색 조건을 지정할 수 있습니다.

### 초안 및 제출 {#drafts-amp-submissions}

검색 및 목록 구성 요소에는 Forms 작성자가 공개한 양식이 표시되지만 초안 및 제출 구성 요소에는 이후 및 제출된 양식을 완료하기 위해 초안으로 저장된 양식이 표시됩니다. 이 구성 요소는 로그인한 사용자에게 개인화된 경험을 제공합니다.

### 링크 {#link}

링크 구성 요소를 사용하여 페이지의 어디에서든 양식에 대한 링크를 만들 수 있습니다. 교육 프로그램을 제공하고 사용자가 교육에 등록할 양식을 제출하도록 하는 시나리오를 고려하십시오. 웹 사이트에 프로그램 세부 사항을 게시했습니다. 세부 정보 아래에서 등록 양식에 대한 링크를 제공합니다. 링크 구성 요소는 해당 링크를 만드는 데 도움이 될 수 있습니다.

## Forms 포털 워크플로 {#forms-portal-workflow}

Forms 포털을 사용하면 양식 저장소의 양식을 포털 페이지에 나열할 수 있습니다. 또한 포털 사용자가 양식 목록에서 검색할 수 있도록 검색 조건을 지정할 수 있습니다. 초안 및 제출 구성 요소를 사용하여 나중에 제출한 양식을 완성하기 위해 초안으로 저장된 양식을 표시할 수도 있습니다. Sites 페이지에서 이러한 기능을 사용할 수 있게 되기 전에 특정 작업 세트를 수행합니다. 나열된 시퀀스의 단계를 수행하여 구성 요소 및 해당 기능을 사이트 페이지에서 사용할 수 있도록 합니다.

1. **Forms 포털 구성 요소 활성화**: 기본적으로 Forms 포털 구성 요소는 사용할 수 없습니다. [AEM 사이드 킥에서 구성 요소 활성화](/help/forms/using/enabling-forms-portal-components.md) AEM Sites 페이지의 경우.
1. **페이지에 양식 나열(Forms 포털 페이지 만들기):** AEM Sites 및 비 AEM 사이트 페이지 모두에 양식을 나열할 수 있습니다. 이 목록에는 게시 인스턴스에서 사용할 수 있는 양식이 포함되어 있습니다. 사용자는 양식을 열고 작성을 시작할 수 있습니다. 사용자가 양식을 열 때마다 양식의 새 인스턴스가 만들어집니다.

   1. **AEM Sites 페이지의 목록 양식**: 를 추가합니다. **[Search &amp; Lister](../../forms/using/creating-form-portal-page.md)** 구성 요소를 페이지에 추가하고 구성 요소 **[목록 창](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** 을 눌러 페이지에 양식을 나열합니다. 추가 및 구성 **검색 창** 구성 요소를 **Search &amp; Lister** 구성 요소를 사용하여 페이지에 검색 기능을 추가할 수도 있습니다. Forms 포털 구성 요소가 있는 페이지를 라고 합니다. [Forms 포털 페이지](../../forms/using/creating-form-portal-page.md).

   1. **AEM Sites이 아닌 페이지의 목록 양식:** 사용 [Forms 포털 검색 API](/help/forms/using/listing-forms-webpage-using-apis.md) AEM Sites이 아닌 페이지에서 양식을 쿼리하고 검색하고 나열하려면 다음을 수행합니다.

1. **Forms 포털 페이지에 초안 및 제출된 양식 나열**: Forms 포털 페이지에 초안 및 제출 구성 요소를 추가하고 구성합니다. 구성 요소에는 초안 상태인 모든 양식과 이미 제출된 양식이 나열됩니다.

   제출된 적응형 양식을 제출 탭에 표시할 수 있도록 하려면 다음을 설정합니다. **제출 액션** 끝 **[Forms 포털 제출 액션](configuring-submit-actions.md).** 또는 Forms 포털 제출 옵션을 활성화합니다. 사용자가 양식을 제출할 때마다 제출 탭에 양식이 추가됩니다.

1. **초안 및 제출된 양식 데이터의 저장소를 구성합니다.** 기본적으로 초안 및 제출 데이터는 AEM 저장소에 저장됩니다. 프로덕션 환경에서는 초안 또는 제출된 양식 데이터를 AEM 저장소에 저장하지 않는 것이 좋습니다. [데이터를 보안 위치에 저장하도록 Forms 포털 구성 요소 구성](../../forms/using/draft-submission-component.md#customizing-the-storage).
1. **(선택 사항) Forms 포털 구성 요소 사용자 지정:** [Forms 포털 페이지 템플릿 사용자 지정](../../forms/using/customizing-templates-forms-portal-components.md) 구성 요소에 고유한 모양을 제공합니다.
1. **(선택 사항) 양식에 사용자 지정 메타데이터 추가:** [양식에 사용자 지정 메타데이터 추가](../../forms/using/customizing-templates-forms-portal-components.md) 목록 및 검색 환경을 개선합니다.
1. **Forms 포털 페이지 게시:** 이제 Forms 포털 페이지가 준비되었습니다. 페이지를 게시합니다.

## 관련 문서 {#related-articles}

* [Forms 포털 구성 요소 활성화](/help/forms/using/enabling-forms-portal-components.md)
* [Forms 포털 만들기 페이지](../../forms/using/creating-form-portal-page.md)
* [API를 사용하여 웹 페이지의 목록 양식](/help/forms/using/listing-forms-webpage-using-apis.md)
* [초안 및 제출 구성 요소 사용](../../forms/using/draft-submission-component.md)
* [초안 및 제출된 양식의 스토리지 사용자 지정](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [초안 및 제출 구성 요소와 데이터베이스를 통합하기 위한 샘플](integrate-draft-submission-database.md)
* [Forms 포털 구성 요소에 대한 템플릿 맞춤화](../../forms/using/customizing-templates-forms-portal-components.md)
* [포털에 양식 게시 소개](../../forms/using/introduction-publishing-forms.md)
