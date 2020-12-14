---
title: AEM 6.5의 이전 버전과의 호환성
seo-title: AEM 6.5의 이전 버전과의 호환성
description: AEM 6.5와 호환되는 앱 및 구성을 유지하는 방법 살펴보기
seo-description: AEM 6.5와 호환되는 앱 및 구성을 유지하는 방법 살펴보기
uuid: 81dc2771-f59b-4b24-8932-9e938cba05e0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: f3b4ec1d-9054-47d4-afcb-0a0121b94190
docset: aem65
translation-type: tm+mt
source-git-commit: c863e438df45fd54c29c1b99114eea07aaeb6162
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---


# AEM 6.5의 이전 버전과의 호환성{#backward-compatibility-in-aem}

## 개요 {#overview}

>[!NOTE]
>
>호환성 패키지의 범위에 속하지 않는 내용 및 구성 변경 사항의 목록은 [AEM](/help/sites-deploying/repository-restructuring.md)의 리포지토리 재구성을 참조하십시오.

AEM 6.5에서는 모든 기능이 이전 버전과의 호환성을 고려하여 개발되었습니다.

대부분의 경우 AEM 6.3을 실행하는 고객은 업그레이드를 수행할 때 코드나 사용자 지정을 변경할 필요가 없습니다. AEM 6.1 및 6.2 고객의 경우 6.3으로 업그레이드하는 동안 발생하는 변화와 다른 변경 사항은 없습니다.

기능을 이전 버전과 호환하지 못하는 경우, 6.4용 호환성 패키지를 설치하면 번들과 콘텐츠에 대한 이전 버전 호환성 문제를 완화할 수 있습니다(다운로드 위치에 대한 자세한 내용은 아래 설정 방법 참조). 이 압축 패키지는 AEM 6.4와 호환되는 대부분의 응용 프로그램의 호환성을 복원하는 데 도움이 됩니다.

호환성 패키지를 사용하면 호환성 모드에서 AEM을 실행하고 새로운 AEM 기능에 대해 사용자 정의 개발을 연기할 수 있습니다.

>[!NOTE]
>
>호환성 패키지는 AEM 6.5 호환 시 필요한 개발을 유예하는 임시 솔루션일 뿐이며 업그레이드 후 바로 개발 단계에서 호환성 문제를 해결할 수 없는 경우에만 마지막 옵션으로 권장됩니다. 6.5 기반의 사용자 정의 개발 및 6.5 기능을 모두 사용하려면 기본 모드로 전환하고 호환성 패키지를 제거하는 것이 좋습니다.

![sase](assets/sase.png)

호환성 패키지에는 다음 두 가지 모드가 있습니다.**라우팅 사용** 및 **라우팅 사용 안 함**.

이렇게 하면 AEM 6.5를 다음 3가지 모드로 실행할 수 있습니다.

**기본 모드:**

기본 모드는 AEM 6.5의 모든 새로운 기능을 사용하고 일부 개발을 완료하여 맞춤화를 모든 새로운 기능과 함께 사용할 수 있도록 하려는 고객을 위한 것입니다.

즉, 업그레이드 직후 애플리케이션을 조정해야 할 수도 있습니다.

**호환성 모드:라우팅 활성화와 함께 설치된 호환성 패키지**

호환성 모드는 이전 버전과 호환되지 않는 인터페이스를 사용자 정의한 고객을 위한 것입니다. 이를 통해 AEM은 호환성 모드에서 실행하고 일부 사용자 정의 코드와 호환되지 않는 새로운 AEM 기능에 대한 사용자 정의 개발을 연기할 수 있습니다.

**레거시 모드:라우팅이 비활성화되어 설치된 호환성 패키지**

레거시 모드는 호환성 패키지에서 이동한 기존 코드 또는 사용되지 않는 코드를 기반으로 사용자 정의 인터페이스를 갖는 고객을 위한 것입니다.

![사분](assets/sapte.png)

## 설정 방법 {#how-to-set-up}

AEM 6.3 호환성 패키지는 이 [link](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/compatpack/aem-compat-cq64-to-cq63)의 패키지 관리자를 사용하여 패키지로 설치할 수 있습니다.

호환성 패키지가 설치되면 아래 표시된 것처럼 OSGI 구성에서 스위치를 사용하여 라우팅을 활성화하거나 비활성화할 수 있습니다.

![screen_shot_2017-11-27at122421pm](assets/screen_shot_2017-11-27at122421pm.png)

호환성 패키지를 설치하고 설정하면 선택한 호환성 모드를 기반으로 기능이 사용됩니다.
