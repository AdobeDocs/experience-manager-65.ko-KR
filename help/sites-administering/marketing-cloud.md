---
title: Adobe Marketing Cloud과 통합
description: Adobe Experience Manager과 Adobe Marketing Cloud을 통합하는 방법을 살펴보십시오.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
translation-type: tm+mt
source-git-commit: 4333cfde433d00ddc4cb013b31fe52956791da46
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 1%

---


# Adobe Marketing Cloud{#integrating-with-the-adobe-marketing-cloud}과 통합

[Adobe Marketing Cloud](https://www.adobe.com/solutions/digital-marketing.html)에는 성공적인 온라인 이니셔티브를 추진하기 위해 실행 가능한 실시간 데이터와 통찰력을 제공하는 강력한 웹 분석 및 웹 사이트 최적화 제품이 포함되어 있습니다. 온라인 비즈니스 최적화를 위한 통합 개방형 플랫폼을 제공합니다. Cloud는 고객 확보, 전환 및 유지 노력을 최적화하고 컨텐츠를 제작 및 배포할 수 있는 강력한 고객 통찰력을 수집 및 제공하는 통합 애플리케이션으로 구성되어 있습니다.

AEM(Adobe Experience Manager)을 사용하면 다음 Adobe Marketing Cloud 제품과 매끄럽게 통합할 수 있습니다.

* Adobe Analytics은 온라인 전략 및 마케팅 이니셔티브에 대한 실용적인 실시간 인텔리전스를 마케터에게 제공합니다.
* Adobe Target을 사용하면 마케터는 고객과 연관성이 높은 온라인 컨텐츠를 지속적으로 제작하여 전환율을 향상시킬 수 있습니다.
* Adobe Dynamic Media Classic은 호스팅된 환경에서 미디어 관리를 자동화하고 웹 퍼블리싱을 간소화하며 웹 경험을 향상시켜 줍니다.
* Adobe 다이내믹 태그 관리는 마케터에게 Adobe 및 제3자 태그를 제한 없이 빠르고 손쉽게 관리할 수 있는 직관적인 툴을 제공합니다.
* Adobe Search &amp; Promote을 통해 마케터는 자신의 사이트에서 검색 결과를 제어하고 최적화할 수 있습니다.
* Adobe Campaign을 사용하면 Adobe Experience Manager에서 바로 이메일 전달 컨텐츠를 관리할 수 있습니다.

또한 [AEM을 Creative Cloud](/help/assets/aem-cc-folder-sharing-best-practices.md) 및 [타사 서비스](/help/sites-administering/third-party-services.md)와 통합할 수 있습니다.

## Adobe Analytics와 통합 {#integrating-with-adobe-analytics}

[Adobe ](https://www.omniture.com/en/products/analytics/sitecatalyst) 분석은 디지털 마케터에게 여러 마케팅 채널에서 모든 온라인 이니셔티브의 통합 데이터를 측정, 분석 및 최적화할 수 있는 한 장소를 제공하는 업계 선도적인 솔루션입니다. 마케터는 디지털 전략 및 마케팅 이니셔티브에 대한 실행 가능한 실시간 웹 분석 인텔리전스를 제공합니다. Adobe Analytics을 사용하면 마케터는 웹 사이트를 통해 가장 수익성 높은 경로를 신속하게 식별하고 고부가가치 웹 방문자를 파악하기 위해 트래픽을 세분화하며 방문자가 사이트를 이탈한 위치를 확인하고 온라인 마케팅 캠페인에 대한 중요한 성공 지표를 식별할 수 있습니다.

Adobe Analytics을 사용하여 사이트의 데이터를 분석할 수 있습니다.

Adobe Analytics과 통합하면 다음을 수행할 수 있습니다.

* Analytics 사용자 추적을 활성화합니다.
* 실행 모드(예: 작성자, 게시)를 다른 보고서 세트에 매핑합니다.
* 클라이언트 컨텍스트 변수를 전환 변수 또는 트래픽 속성으로 제출합니다.
* 미리 정의된 변수 매핑을 사용합니다.
* 한 번에 전체 사이트 섹션을 구성합니다.
* 사용자 정의 이벤트를 추적합니다.

AEM과 Analytics 통합에 대한 자세한 내용은 [Adobe Analytics](/help/sites-administering/adobeanalytics.md)과 통합을 참조하십시오.

[옵트인 마법사](/help/sites-administering/opt-in.md)를 사용하여 손쉽게 통합을 수행할 수도 있습니다.

## Adobe Target과 통합 {#integrating-with-adobe-target}

[Adobe ](https://www.omniture.com/en/products/conversion/test-and-target) Target은 마케터가 온라인 테스트를 설계 및 실행하고, 행동에 따라 고객 세그먼트를 신속하게 생성하고, 컨텐츠 및 온라인 경험 타깃팅을 자동화하는 데 사용됩니다.

오늘날 온라인 소비자는 끊임없이 변화하는 요구 사항을 충족하고 다양한 사이트 및 컨텐츠 소스를 통해 연관성 있고 개인화된 컨텐츠를 기대합니다. 온라인 고객의 참여를 유도하려면 온라인 마케터가 고객에게 연관성 있고 매력적인 제품 및 컨텐츠를 신속하게 파악하는 것이 중요합니다. 이러한 지식을 바탕으로 마케터는 사이트를 지속적으로 발전시키고 다양한 고객에게 적합한 컨텐츠를 타깃팅할 수 있는 기능을 필요로 합니다.

[Adobe과 통합 ](/help/sites-administering/target.md) Target은 사이트를 Target과 통합하는 방법을 설명합니다.

[옵트인 마법사](/help/sites-administering/opt-in.md)를 사용하여 손쉽게 통합을 수행할 수도 있습니다.

## Analytics 및 Target {#opting-in-to-analytics-and-target}으로 선택

AEM은 Adobe Analytics 및 Adobe Target과 통합하기 위한 간단한 옵트인 절차를 제공합니다. 관리자로 로그인하고 프로젝트 콘솔을 방문하면 옵트인 마법사가 표시됩니다.

![chlimage_1-107](assets/chlimage_1-107a.png)

페이지 추적 및 분석 기능 및 개인화 기능을 사용할 수 있도록 분석 및/또는 Target과의 통합을 선택하십시오. 옵트인하면 사용자 계정 정보를 제공하고 추적되는 페이지를 지정해야 합니다.

자세한 내용은 [Adobe Analytics 및 Adobe Target에 선택](/help/sites-administering/opt-in.md)을 참조하십시오.

## Adobe Dynamic Media Classic {#integrating-with-scene}과 통합

Adobe Dynamic Media Classic은 다이내믹 마케팅 에셋과 풍부한 시각적 머천다이징을 웹, 모바일, 이메일, 소셜 미디어, 인터넷에 연결된 디스플레이 및 인쇄물로 게시, 관리, 향상 및 전달하기 위한 호스팅된 솔루션입니다.

Adobe Experience Manager에서는 Adobe Experience Manager에서 Dynamic Media Classic으로 디지털 자산을 직접 게시할 수 있으며, Dynamic Media Classic에서 Adobe Experience Manager으로 디지털 자산을 게시할 수 있습니다.

또한 Dynamic Media Classic에 게시된 Adobe Experience Manager 에셋은 기본 확대/축소 및 비디오와 같은 다양한 뷰어에서 볼 수 있습니다.

Adobe Experience Manager과 Dynamic Media Classic의 통합 방법에 대한 자세한 내용은 [Dynamic Media Classic과 통합](/help/sites-administering/scene7.md) 설명서를 참조하십시오.

## Adobe 다이내믹 태그 관리 {#integrating-with-adobe-dynamic-tag-management}와 통합

[Adobe 다이내믹 태그 관리](https://www.adobe.com/solutions/digital-marketing/dynamic-tag-management.html) 는 마케터에게 Adobe 및 제3자 태그를 무제한으로 빠르고 쉽게 관리할 수 있는 직관적인 도구를 제공합니다. IT 리소스에 대한 의존도를 줄이면서 온라인에서 거의 모든 것을 보다 정확하고 유연하게 최적화할 수 있습니다.

[다이내믹 태그 관리 ](/help/sites-administering/dtm.md) 웹 속성을 사용하여 AEM 사이트를 추적할 수 있도록 Adobe 다이내믹 태그 관리를 AEM과 통합할 수 있습니다.

## Adobe Audience Manager {#integrating-with-adobe-audience-manager}과 통합

AEM 6.3에서 Audience Manager 통합이 제거되었습니다.

## Search &amp; Promote {#integrating-with-search-promote}과 통합

마케터는 Adobe Search &amp; Promote을 사용하여 방문자가 웹 및 모바일 사이트에서 관련 제품과 컨텐츠를 검색하고 비교 및 선택하는 방법을 최적화할 수 있습니다. 기업은 비즈니스 목표 및 방문자 의도를 기반으로 우선 순위 항목을 손쉽게 홍보할 수 있을 뿐만 아니라 KPI 기반 트리거 또는 지표를 통해 머천다이징 및 홍보 활동을 자동화할 수 있습니다.

Adobe Search &amp; Promote은 소매업체에서 뉴스 사이트에 이르는 방문자가 많은 온라인 비즈니스를 위해 안정적이고 확장 가능한 호스팅되는 사이트 검색 애플리케이션입니다. 탁월한 수준의 마케터 제어 기능과 측정 지표 기반의 연관성을 제공합니다.

AEM 및 Search &amp; Promote 통합에 대한 자세한 내용은 [Adobe Search &amp; Promote과 통합](/help/sites-administering/search-and-promote.md)을 참조하십시오.

## Adobe Campaign {#integrating-with-adobe-campaign}과 통합

[Adobe ](https://www.adobe.com/solutions/campaign-management.html) 캠페인을 사용하면 Adobe Experience Manager에서 바로 이메일 전달 컨텐츠를 관리할 수 있습니다.

AEM과 Adobe Campaign의 통합 방법에 대한 자세한 내용은 [Adobe Campaign](/help/sites-administering/campaignstandard.md)과 통합을 참조하십시오.

## Livefyre와 통합하기 {#integrating-with-livefyre}

AEM 및 Livefyre에 대한 자세한 내용:

* [Livefyre 시작하기](https://answers.livefyre.com/developers/getting-started)

* [Livefyre 및 AEM](https://answers.livefyre.com/product/livefyre-for-adobe-experience-manager-aem/livefyre-for-adobe-experience-manager/)

