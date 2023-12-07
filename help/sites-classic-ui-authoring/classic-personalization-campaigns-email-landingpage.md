---
title: 효과적인 뉴스레터 랜딩 페이지 만들기
description: 효과적인 뉴스레터 랜딩 페이지는 최대한 많은 사람들이 뉴스레터(또는 기타 이메일 마케팅 캠페인)에 등록하도록 도와줍니다. 뉴스레터 등록에서 수집한 정보를 사용하여 리드를 받을 수 있습니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: c2fbf858-8815-426e-a2e5-f92bcf909ad0
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# 효과적인 뉴스레터 랜딩 페이지 만들기{#creating-an-effective-newsletter-landing-page}

효과적인 뉴스레터 랜딩 페이지는 최대한 많은 사람들이 뉴스레터(또는 기타 이메일 마케팅 캠페인)에 등록하도록 도와줍니다. 뉴스레터 등록에서 수집한 정보를 사용하여 리드를 받을 수 있습니다.

효과적인 뉴스레터 랜딩 페이지를 만들려면 다음 작업을 수행해야 합니다.

1. 사람들이 뉴스레터를 구독할 수 있도록 뉴스레터 목록을 만듭니다.
1. 등록 양식을 만듭니다. 이렇게 하면 뉴스레터에 등록한 사람을 리드 목록에 자동으로 추가하는 워크플로우 단계를 추가합니다.
1. 등록해 주신 사용자에게 감사하며 프로모션을 제공하는 확인 페이지를 만드십시오.
1. 티저를 추가합니다.

>[!NOTE]
>
>Adobe은 이 기능(리드 및 목록 관리)을 더 강화하지 않을 계획입니다.
>권장 사항은 [Adobe Campaign 및 AEM에 통합](/help/sites-administering/campaign.md).

## 뉴스레터 목록 만들기 {#creating-a-list-for-the-newsletter}

목록 만들기(예: ) **Geometrixx 뉴스레터** MCM에서 사람들이 구독해야 하는 뉴스레터에 대해 설명합니다. 목록 만들기에 대해서는 다음에 설명되어 있습니다 [목록 만들기](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingnewlists).

다음은 목록의 예입니다.

![mcm_listcreate](assets/mcm_listcreate.png)

## 등록 양식 만들기 {#create-a-sign-up-form}

사용자가 태그를 구독할 수 있는 뉴스레터 등록 양식을 만듭니다. 샘플 Geometrixx 웹 사이트에서는 양식을 만들 수 있는 뉴스레터 페이지를 Geometrixx 도구 모음에 제공합니다.

나만의 뉴스레터 양식을 만들려면 다음에서 양식을 만드는 방법을 참조하십시오. [Forms 설명서](/help/sites-authoring/default-components.md#form). 뉴스레터는 태그 라이브러리의 태그를 사용합니다. 태그를 더 추가하려면 를 참조하십시오. [태그 관리](/help/sites-authoring/tags.md#tagadministration).

다음 예제에서 숨김 필드는 최소한의 정보(이메일)만 제공합니다. 또한 나중에 필드를 추가할 수 있지만 이는 전환율에 영향을 줍니다.

다음 예제는 https://localhost:4502/cf#/content/geometrixx/en/toolbar/newsletter.html에서 만든 양식입니다.

1. 양식을 만듭니다.

   ![mcm_newsletterpage](assets/mcm_newsletterpage.png)

1. 클릭 **편집** 감사 페이지로 이동하도록 양식을 구성하는 양식 구성 요소( 참조) [감사 인사 페이지 만들기](#creating-a-thank-you-page)).

   ![dc_formstart_thankyou](assets/dc_formstart_thankyou.png)

1. 양식 작업(양식을 제출할 때 발생할 작업)을 설정하고 이전에 만든 목록(예: geometrixx-newsletter)에 등록된 사용자를 할당하도록 그룹을 구성합니다.

   ![dc_formstart_thankyouadvanced](assets/dc_formstart_thankyouadvanced.png)

### 감사 인사 페이지 만들기 {#creating-a-thank-you-page}

사용자가 **지금 가입**&#x200B;감사 인사 페이지가 자동으로 열립니다. Geometrixx 뉴스레터 페이지에서 감사 인사 페이지를 만듭니다. 뉴스레터 양식을 작성한 후 양식 구성 요소를 편집하고 감사 페이지에 경로를 추가합니다.

요청을 제출하면 사용자가으로 이동합니다. **감사합니다.** 이메일을 받게 되는 페이지입니다. 이 감사 페이지는 /content/geometrixx/en/toolbar/newsletter/thank_you에 만들어졌습니다.

![mcm_newsletter_thankyupage](assets/mcm_newsletter_thankyoupage.png)

### 티저 추가 {#adding-teasers}

추가 [티저](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers) 특정 대상을 타깃팅할 수 있습니다. 예를 들어 감사 인사 페이지 및 뉴스레터 등록 페이지에 티저를 추가할 수 있습니다.

티저를 추가하여 효과적인 뉴스레터 랜딩 페이지를 만들려면:

1. 등록 선물의 티저 단락을 만듭니다. 선택 **첫 번째** 전략으로 어떤 선물을 받게 될지 알려주는 텍스트를 포함합니다.

   ![dc_teaser_thankyou](assets/dc_teaser_thankyou.png)

1. 감사 인사 페이지의 티저 단락을 만듭니다. 선택 **첫 번째** 를 전략으로 사용하고 선물을 준비 중임을 나타내는 텍스트를 포함합니다.

   ![chlimage_1-103](assets/chlimage_1-103.png)

1. 두 개의 티저(비즈니스로 태그 1개와 태그가 지정되지 않은 태그 1개)로 캠페인을 만듭니다.

### 구독자에게 콘텐츠 푸시 {#pushing-content-to-subscribers}

MCM의 뉴스레터 기능을 통해 페이지에 대한 변경 사항을 푸시합니다. 그런 다음 업데이트된 콘텐츠를 구독자에게 푸시합니다.

다음을 참조하십시오 [뉴스레터 보내기](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters).
