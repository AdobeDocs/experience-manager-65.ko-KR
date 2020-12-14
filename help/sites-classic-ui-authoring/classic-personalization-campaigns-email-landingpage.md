---
title: 효과적인 뉴스레터 랜딩 페이지 만들기
seo-title: 효과적인 뉴스레터 랜딩 페이지 만들기
description: 효과적인 뉴스레터 랜딩 페이지는 뉴스레터 또는 기타 이메일 마케팅 캠페인의 가입자를 최대한으로 늘리는 데 도움이 됩니다. 뉴스레터에 등록한 가입자의 정보를 사용하여 리드를 생성할 수 있습니다.
seo-description: 효과적인 뉴스레터 랜딩 페이지는 뉴스레터 또는 기타 이메일 마케팅 캠페인의 가입자를 최대한으로 늘리는 데 도움이 됩니다. 뉴스레터에 등록한 가입자의 정보를 사용하여 리드를 생성할 수 있습니다.
uuid: 0799b954-076b-4e95-8724-3661ae8fddb6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: b41de64a-7d27-4633-a8d5-ac91d47eb1bb
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 93%

---


# 효과적인 뉴스레터 랜딩 페이지 만들기{#creating-an-effective-newsletter-landing-page}

효과적인 뉴스레터 랜딩 페이지는 뉴스레터 또는 기타 이메일 마케팅 캠페인의 가입자를 최대한으로 늘리는 데 도움이 됩니다. 뉴스레터에 등록한 가입자의 정보를 사용하여 리드를 생성할 수 있습니다.

효과적인 뉴스레터 랜딩 페이지를 만들려면 다음을 수행해야 합니다.

1. 사람들이 뉴스레터에 가입할 수 있도록 뉴스레터 목록을 만듭니다.
1. 등록 양식을 만듭니다. 이때 뉴스레터에 등록하는 사람을 리드 목록에 자동으로 추가하는 Workflow 단계를 추가해야 합니다.
1. 등록한 사용자에게 감사를 표하고 판촉 행사 등을 제공할 수 있는 확인 페이지를 만듭니다.
1. 티저를 추가합니다.

>[!NOTE]
>
>Adobe는 이 기능(리드 및 목록 관리)을 추가로 개선할 계획이 없습니다.
>권장 사항은 [Adobe Campaign을 활용하고 AEM](/help/sites-administering/campaign.md)과의 통합을 활용하는 것입니다.

## 뉴스레터 목록 만들기 {#creating-a-list-for-the-newsletter}

MCM에서 사람들이 가입할 수 있는 **Geometrixx 뉴스레터**&#x200B;와 같은 목록을 만듭니다. 목록 만들기에 대해서는 [목록 만들기](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingnewlists)에 설명되어 있습니다.

다음은 목록의 예입니다.

![mcm_listcreate](assets/mcm_listcreate.png)

## 등록 양식 만들기 {#create-a-sign-up-form}

사용자가 태그에 가입할 수 있는 뉴스레터 등록 양식을 만듭니다. 샘플 Geometrixx 웹 사이트의 Geometrixx 도구 모음에 있는 뉴스레터 페이지에 양식을 만들어 볼 수 있습니다.

자신만의 뉴스레터 양식을 만들려면 [양식 설명서](/help/sites-authoring/default-components.md#form)에서 양식 작성에 대한 정보를 참조하십시오. 뉴스레터에서는 태그 라이브러리의 태그를 사용합니다. 태그를 더 추가하려면 [태그 관리](/help/sites-authoring/tags.md#tagadministration)를 참조하십시오.

다음 예제의 숨김 필드는 최소한도로 필요한 정보(이메일)를 제공합니다. 이후에 필드를 더 추가할 수 있지만 필드가 너무 많으면 전환율에 영향을 줄 수 있습니다.

다음 예제는 https://localhost:4502/cf#/content/geometrixx/en/toolbar/newsletter.html에서 만든 양식입니다.

1. 양식을 만듭니다.

   ![mcm_newsletterpage](assets/mcm_newsletterpage.png)

1. 양식 구성 요소에서 **편집**&#x200B;을 클릭하여 양식이 감사 인사 페이지로 이동하도록 구성합니다([감사 인사 페이지 만들기](#creating-a-thank-you-page) 참조).

   ![dc_formstart_thangyou](assets/dc_formstart_thankyou.png)

1. 양식 작업(양식을 전송할 때 발생하는 작업)을 설정하고 그룹을 구성하여 등록한 사용자를 앞에서 만든 목록(예: geometrixx-newsletter)에 지정합니다.

   ![dc_formstart_thankyouadvanced](assets/dc_formstart_thankyouadvanced.png)

### 감사 인사 페이지 만들기 {#creating-a-thank-you-page}

사용자가 **지금 가입**&#x200B;을 클릭할 때 자동으로 감사 인사 페이지를 열 수 있습니다. Geometrixx 뉴스레터 페이지에 감사 인사 페이지를 만듭니다. Newsletter 양식을 만든 후 양식 구성 요소를 편집하고 감사 인사 페이지에 대한 경로를 추가합니다.

요청을 전송하면 사용자에게 **감사 인사** 페이지가 표시된 후 이메일이 발송됩니다. 이 감사 인사 페이지가 만들어진 위치는 /content/geometrixx/kr/toolbar/newsletter/thank_you입니다.

![mcm_newsletter_thankyoupage](assets/mcm_newsletter_thankyoupage.png)

### 티저 추가 {#adding-teasers}

특정 대상을 타깃팅하려면 [티저](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers)를 추가하십시오. 예를 들어 감사 인사 페이지 및 Newsletter 등록 페이지에 Teaser를 추가할 수 있습니다.

효과적인 Newsletter 랜딩 페이지를 만들기 위해 Teaser를 추가하는 방법은 다음과 같습니다.

1. 등록 선물에 대한 Teaser 단락을 만듭니다. 전략으로 **처음**&#x200B;을 선택하고 등록 시 증정되는 선물에 대한 텍스트를 포함합니다.

   ![dc_teaser_thangyou](assets/dc_teaser_thankyou.png)

1. 감사 인사 페이지에 티저 단락을 만듭니다. 전략으로 **처음**&#x200B;을 선택하고 선물이 배송되었다는 텍스트를 포함합니다.

   ![chlimage_1-103](assets/chlimage_1-103.png)

1. 두 개의 Teaser가 있는 캠페인을 만듭니다. 하나에는 비즈니스 태그를 달고 하나에는 태그를 달지 않습니다.

### 가입자에게 컨텐트 보내기 {#pushing-content-to-subscribers}

MCM의 뉴스레터 기능을 통해 페이지 변경 사항을 보냅니다. 그런 다음 업데이트된 컨텐츠를 가입자에게 보냅니다.

[뉴스레터 전송](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters)을 참조하십시오.
