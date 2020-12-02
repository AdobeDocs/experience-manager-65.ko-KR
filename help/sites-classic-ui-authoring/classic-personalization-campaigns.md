---
title: 캠페인 관리
seo-title: 캠페인 관리
description: 캠페인 관리는 디지털 마케터에게 맞춤형 컨텐츠를 전달하고 방문자만을 위한 경험을 만들 수 있는 기회를 제공합니다. 이를 통해 웹, 이메일, 모바일 서비스 전체에서 마케팅 캠페인을 조정하고 방문자를 유치할 수 있습니다.
seo-description: 캠페인 관리는 디지털 마케터에게 맞춤형 컨텐츠를 전달하고 방문자만을 위한 경험을 만들 수 있는 기회를 제공합니다. 이를 통해 웹, 이메일, 모바일 서비스 전체에서 마케팅 캠페인을 조정하고 방문자를 유치할 수 있습니다.
uuid: 202d614b-a607-45de-8c24-1ee66b230315
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e8b70971-4f23-45f8-8c23-e147413243c2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 94%

---


# 캠페인 관리{#campaign-management}

캠페인 관리는 디지털 마케터에게 맞춤형 컨텐츠를 전달하고 방문자만을 위한 경험을 만들 수 있는 기회를 제공합니다.

이를 통해 웹, 이메일, 모바일 서비스 전체에서 마케팅 캠페인을 조정하고 방문자를 유치할 수 있습니다. 여러 채널에서 컨텐츠를 만들고, 방문자를 세그먼트로 구분하고, 특정 사용자 프로필에 맞는 맞춤 컨텐츠를 추천하고, 캠페인을 관리할 수 있습니다.

이 문서에서는 캠페인을 구성하는 다양한 요소에 대해 설명합니다. 자세한 정보는 다음 문서에서 확인할 수 있습니다.

* [티저 및 전략](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [이메일 마케팅](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [랜딩 페이지](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Target 오퍼](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [마케팅 캠페인 관리자 작업](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [세그멘테이션 이해](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [캠페인 설정](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

캠페인 관리는 다음과 같은 다양한 요소로 구성되어 있습니다.

* **브랜드**
AEM에서 브랜드는 최상위 단위이며 
**캠페인**.

* **캠페인**
캠페인은 개별 
**경험**.

* **경험**
집중된 컨텐츠는 
**터치포인트**. 다음과 같은 몇 가지 유형의 경험을 사용할 수 있습니다.

   * **Teaser**
      [Teaser 페이지/단락](#teasers)은 특정 방문자 **세그먼트**&#x200B;를 그들의 관심사에 초점을 맞춘 컨텐트로 유도하는 데 사용됩니다.

      Teaser 페이지는 다음과 같은 역할을 할 수 있습니다.

      * 방문자가 선택할 수 있는 다양한 옵션을 제공합니다.
      * 특정 방문자 세그먼트를 기반으로 하나의 티저 단락만 표시합니다. 예를 들어 방문자 연령에 따라 티저 단락이 표시될 수 있습니다.

      일반적으로 티저 페이지는 특정 기간 동안만 일시적으로 작동하며, 기간이 지나면 다음 티저 페이지로 대체됩니다.

   * **뉴스레터**

      [이메일 통신](#emailmarketing)은 사용자를 확보하고 웹 사이트 방문을 독려하는 데 사용됩니다. 일반적으로 **리드**(주로 **목록**&#x200B;으로 그룹화됨)에게 발송되는 뉴스레터 형태를 갖습니다. **참고:** Adobe는 이 기능을 추가로 개선할 계획이 없습니다. [AEM을 Adobe Campaign과 통합](/help/sites-administering/campaign.md)하여 활용하는 것이 좋습니다.

   * **Adobe Target**

      고객과 연관성이 더 높은 온라인 컨텐츠와 오퍼를 지속적으로 만드는 데 필요한 기능을 갖춘 전환 웹 사이트 최적화 도구를 마케터에게 제공함으로써 더 많은 전환을 만들어 낼 수 있는 Adobe Target(이전 Test&amp;Target)과의 통합을 가능하도록 합니다. Adobe Target은 단일 애플리케이션에서 테스트를 디자인 및 실행하고, 대상 세그먼트를 만들고, 컨텐츠를 타깃팅하기 위한 직관적인 인터페이스를 제공합니다.


* **터치포인트**

   방문자와 캠페인의 접촉점입니다. 터치포인트는 사용자가 만든 경험과 연결되어 있습니다.

   예를 들어 Teaser의 경우 Teaser 단락이 있는 컨텐트 페이지, Newsletter의 경우에는 메일링 목록이 터치포인트입니다.

* **리드**

   방문자에 대해 수집한 정보와 연락 방법이 리드의 기반을 형성합니다. **참고:** Adobe는 이 기능을 추가로 개선할 계획이 없습니다.

   [AEM을 Adobe Campaign과 통합](/help/sites-administering/campaign.md)하여 활용하는 것이 좋습니다.

* **목록**

   일반적으로 리드는 목록으로 그룹화되므로 사용자는 이들 전체를 대상으로 행동을 취할 수 있습니다. **참고:** Adobe는 이 기능을 추가로 개선할 계획이 없습니다.

   [AEM을 Adobe Campaign과 통합](/help/sites-administering/campaign.md)하여 활용하는 것이 좋습니다.

* **세그먼트**

   사이트 방문자가 갖는 관심사와 목표는 매우 다양합니다. 웹 사이트에서의 활동, 등록된 프로필 정보 및 기타 웹 사이트에서의 활동 등 요인을 바탕으로 한 분석은 세그먼트를 정의하는 데 도움이 됩니다. 다음으로 방문자에 맞는 세그먼트에 따라 방문자의 필요 및 관심사에 컨텐츠를 맞출 수 있습니다.

* **MCM**

   MCM(마케팅 캠페인 관리자)은 캠페인, 브랜드, 경험, 터치포인트, 리드, 목록, 세그먼트 및 보고서를 만들고 제어하는 데 필요한 모든 기능에 액세스할 수 있는 콘솔입니다.

   다양한 위치(**캠페인**&#x200B;이라고 레이블된)에서 또는 예를 들어

   `http://localhost:4502/libs/mcm/content/admin.html`

