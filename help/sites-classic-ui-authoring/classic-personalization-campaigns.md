---
title: Campaign Management
seo-title: Campaign Management
description: 캠페인 관리는 디지털 마케터에게 개인화된 콘텐츠를 제공하여 방문자를 위한 전용 경험을 만들 수 있는 기회를 제공합니다. 이를 통해 웹, 이메일 및 모바일 서비스에서 마케팅 캠페인을 오케스트레이션하여 방문자를 참여시킬 수 있습니다.
seo-description: Campaign management provides digital marketers the opportunity to deliver personalized content and so create dedicated experiences for visitors. It allows you to orchestrate your marketing campaigns across the web, email and mobile services and so engage your visitors.
uuid: 202d614b-a607-45de-8c24-1ee66b230315
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e8b70971-4f23-45f8-8c23-e147413243c2
exl-id: d1741525-a475-4a76-bd16-55318023495e
source-git-commit: 1ba34f95cf3ce3f136482075802d2e4372f28917
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 1%

---


# Campaign Management{#campaign-management}

캠페인 관리는 디지털 마케터에게 개인화된 콘텐츠를 제공하여 방문자를 위한 전용 경험을 만들 수 있는 기회를 제공합니다.

이를 통해 웹, 이메일 및 모바일 서비스에서 마케팅 캠페인을 오케스트레이션하여 방문자를 참여시킬 수 있습니다. 콘텐츠를 만들고, 방문자를 세그먼트화하고, 특정 사용자 프로필에 대한 타겟팅된 콘텐츠를 푸시 및 홍보하고, 여러 채널에서 캠페인을 관리할 수 있습니다.

이 문서에서는 캠페인을 구성하는 다양한 요소에 대해 설명합니다. 자세한 내용은 다음 문서에서 확인할 수 있습니다.

* [티저 및 전략](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [이메일 마케팅](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [랜딩 페이지](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Target 오퍼](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [마케팅 캠페인 관리자 작업](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [세그먼테이션 이해](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [캠페인 설정](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

캠페인 관리는 다양한 요소로 구성됩니다.

* **브랜드**
AEM에서 브랜드는 최상위 수준의 단위이며 다음과 같은 컬렉션을 구성합니다. **캠페인**.

* **캠페인**
캠페인은 개인의 컬렉션입니다 **경험**.

* **경험**
포커스가 있는 콘텐츠는 방문자에게 표시되는 다양한 경험을 형성합니다. **접점**. 사용 가능한 경험에는 몇 가지 유형이 있습니다.

   * **티저**
     [티저 페이지/단락](#teasers) 특정 방문자를 유도하는 데 사용됩니다. **세그먼트** 관심 분야에 초점을 맞춘 콘텐츠를 제공합니다.

     티저 페이지는 다음과 같은 작업을 수행할 수 있습니다.

      * 방문자가 선택할 수 있는 다양한 옵션을 제공합니다.
      * 특정 방문자 세그먼트를 기반으로 하는 티저 단락을 하나만 표시합니다. 예를 들어, 표시되는 티저 단락은 방문자의 나이에 따라 달라질 수 있습니다.

     일반적으로 티저 페이지는 다음 티저 페이지로 대체될 때까지 특정 기간 동안 지속되는 임시 작업입니다.

   * **뉴스레터**

     [전자 메일 통신](#emailmarketing) 는 사용자를 참여시키고 웹 사이트를 방문하도록 권장하는 데 사용됩니다. 일반적으로 뉴스레터 형식을 취하여 **잠재 고객** (보통 다음과 같이 그룹화됨) **목록**). **참고:** Adobe은 이 기능을 더 강화하지 않을 계획입니다. 권장 사항은 다음과 같습니다 [Adobe Campaign 및 AEM에 통합 활용](/help/sites-administering/campaign.md).

   * **Adobe Target**

     이를 통해 마케터에게 지속적인 온라인 콘텐츠 및 고객과 관련된 오퍼를 더욱 강력하게 만드는 데 필요한 기능을 갖춘 전환 웹 사이트 최적화 도구를 제공하는 Adobe Target Target(이전 Test&amp;Offer)와 통합할 수 있습니다. Adobe Target은 테스트 디자인 및 실행, 대상 세그먼트 만들기 및 단일 애플리케이션에서 콘텐츠 타겟팅을 위한 직관적인 인터페이스를 제공합니다.

* **터치포인트**

  다음은 방문자와 캠페인 간의 연락 지점입니다. 터치포인트는 사용자가 만든 경험에 연결됩니다.

  예를 들어 티저의 경우 티저 단락이 있는 콘텐츠 페이지이고 뉴스레터의 경우 메일링 목록입니다.

* **리드**

  방문자에 대해 수집한 정보와 연락하는 방법은 리드의 기초가 됩니다. **참고:** Adobe은 이 기능을 더 강화하지 않을 계획입니다.

  권장 사항은 다음과 같습니다 [Adobe Campaign 및 AEM에 통합 활용](/help/sites-administering/campaign.md).

* **목록**

  리드는 일반적으로 목록으로 그룹화되어 그에 대해 공동 작업을 수행할 수 있습니다. 참고: **참고:** Adobe은 이 기능을 더 강화하지 않을 계획입니다.

  권장 사항은 다음과 같습니다 [Adobe Campaign 및 AEM에 대한 통합을 활용합니다.](/help/sites-administering/campaign.md)

* **세그먼트**

  사이트 방문자는 사이트를 방문할 때 서로 다른 관심사와 목표를 갖습니다. 웹 사이트에서의 활동, 등록된 프로필 정보 및 다른 웹 사이트에서의 활동 등의 요소에 따라 이를 분석하면 세그먼트를 정의하는 데 도움이 됩니다. 그런 다음 콘텐츠를 일치하는 세그먼트에 따라 방문자의 요구 사항 및 관심 분야에 구체적으로 타겟팅할 수 있습니다.

* **MCM**

  마케팅 캠페인 관리자(MCM)는 캠페인, 브랜드, 경험, 터치포인트, 리드, 목록, 세그먼트 및 보고서를 만들고 제어하는 데 필요한 모든 기능에 액세스할 수 있는 콘솔입니다.

  다양한 위치에서 액세스할 수 있습니다( 로 레이블이 지정됨). **캠페인**)를 입력하거나, URL을 사용하는 등의 작업을 수행할 수 있습니다.

  `http://localhost:4502/libs/mcm/content/admin.html`
