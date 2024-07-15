---
title: Campaign Management
description: 캠페인 관리는 디지털 마케터에게 개인화된 콘텐츠를 제공하여 방문자를 위한 전용 경험을 만들 수 있는 기회를 제공합니다. 웹, 이메일 및 모바일 서비스에서 마케팅 캠페인을 오케스트레이션하여 방문자를 참여시킬 수 있습니다.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: d1741525-a475-4a76-bd16-55318023495e
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---


# Campaign Management{#campaign-management}

캠페인 관리는 디지털 마케터에게 개인화된 콘텐츠를 제공하여 방문자를 위한 전용 경험을 만들 수 있는 기회를 제공합니다.

웹, 이메일 및 모바일 서비스에서 마케팅 캠페인을 오케스트레이션하여 방문자를 참여시킬 수 있습니다. 콘텐츠를 만들고, 방문자를 세그먼트화하고, 특정 사용자 프로필에 대한 타겟팅된 콘텐츠를 푸시하고, 홍보하고, 여러 채널에서 캠페인을 관리할 수 있습니다.

이 문서에서는 캠페인을 구성하는 다양한 요소에 대해 설명합니다. 자세한 내용은 다음 문서에서 확인할 수 있습니다.

* [티저 및 전략](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [이메일 마케팅](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [랜딩 페이지](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Target 오퍼](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [마케팅 캠페인 관리자 작업](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [세분화 이해](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [캠페인 설정](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

캠페인 관리는 다양한 요소로 구성됩니다.

* **브랜드**
Adobe Experience Manager(AEM)에서 브랜드는 최상위 단위이며 **캠페인**&#x200B;의 컬렉션을 구성합니다.

* **캠페인**
캠페인은 개별 **경험**&#x200B;의 컬렉션입니다.

* **경험**
포커스가 있는 콘텐츠는 **터치포인트**&#x200B;에서 방문자에게 표시되는 다양한 경험을 형성합니다. 사용 가능한 경험에는 몇 가지 유형이 있습니다.

   * **티저**
     [티저 페이지/단락](#teasers)은(는) 특정 방문자 **세그먼트**&#x200B;를 관심사에 집중된 콘텐츠로 안내하는 데 사용됩니다.

     티저 페이지는 다음과 같은 작업을 수행할 수 있습니다.

      * 방문자가 선택할 수 있는 다양한 옵션을 제공합니다.
      * 특정 방문자 세그먼트를 기반으로 하는 티저 단락을 하나만 표시합니다. 예를 들어 표시되는 티저 단락은 방문자의 나이에 따라 달라질 수 있습니다.

     일반적으로 티저 페이지는 다음 티저 페이지로 대체될 때까지 특정 기간 동안 지속되는 임시 작업입니다.

   * **뉴스레터**

     [전자 메일 통신](#emailmarketing)은 사용자를 참여시키고 사용자가 웹 사이트를 방문하도록 유도하는 데 사용됩니다. 일반적으로 뉴스레터 형식을 취하여 **리드**(**목록**(으)로 그룹화됨)로 보냅니다. **참고:** Adobe은 이 기능을 더 향상시킬 계획이 없습니다. 권장 사항은 [Adobe Campaign을 사용하고 AEM에 통합](/help/sites-administering/campaign.md)하는 것입니다.

   * **Adobe Target**

     이를 통해 Adobe Target(이전의 Test&amp;Target)와 통합하여 마케터에게 지속적인 온라인 콘텐츠 및 고객 산출 더 큰 전환과 관련된 오퍼를 만드는 데 필요한 기능을 갖춘 전환 웹 사이트 최적화 도구를 제공합니다. Adobe Target은 테스트 디자인 및 실행, 대상 세그먼트 만들기 및 단일 애플리케이션에서 콘텐츠 타겟팅을 위한 직관적인 인터페이스를 제공합니다.

* **접점**

  다음은 방문자와 캠페인 간의 연락 지점입니다. 터치포인트는 사용자가 만든 경험에 연결됩니다.

  예를 들어 티저의 경우 티저 단락이 있는 콘텐츠 페이지이고 뉴스레터의 경우 메일링 목록입니다.

* **리드**

  방문자에 대해 수집한 정보와 연락하는 방법은 리드의 기초가 됩니다. **참고:** Adobe은 이 기능을 더 향상시킬 계획이 없습니다.

  권장 사항은 [Adobe Campaign을 사용하고 AEM에 통합](/help/sites-administering/campaign.md)하는 것입니다.

* **목록**

  리드는 목록으로 그룹화되어 그에 대해 공동 작업을 수행할 수 있습니다. 참고: **참고:** Adobe은 이 기능을 더 향상시킬 계획이 없습니다.

  권장 사항은 [Adobe Campaign 및 AEM에 통합을 사용하는 것입니다.](/help/sites-administering/campaign.md)

* **세그먼트**

  사이트 방문자는 사이트를 방문할 때 서로 다른 관심사와 목표를 갖습니다. 웹 사이트에서의 활동, 등록된 프로필 정보 및 다른 웹 사이트에서의 활동 등의 요소에 따라 이를 분석하면 세그먼트를 정의하는 데 도움이 됩니다. 그런 다음 콘텐츠를 일치하는 세그먼트에 따라 방문자의 요구 사항 및 관심사에 타기팅할 수 있습니다.

* **MCM**

  마케팅 캠페인 관리자(MCM)는 캠페인, 브랜드, 경험, 터치포인트, 리드, 목록, 세그먼트 및 보고서를 만들고 제어하는 데 필요한 모든 기능에 액세스할 수 있는 콘솔입니다.

  다양한 위치(**캠페인**)에서 액세스하거나 URL과 같은 방법으로 액세스할 수 있습니다.

  `http://localhost:4502/libs/mcm/content/admin.html`
