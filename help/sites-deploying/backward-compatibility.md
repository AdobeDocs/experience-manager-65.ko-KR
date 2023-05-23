---
title: AEM 6.5의 이전 버전과의 호환성
seo-title: Backward Compatibility in AEM 6.5
description: 앱 및 구성을 AEM 6.5와 호환되도록 하는 방법에 대해 알아봅니다
seo-description: Learn how to keep your apps and configurations compatible with AEM 6.5
uuid: 81dc2771-f59b-4b24-8932-9e938cba05e0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: f3b4ec1d-9054-47d4-afcb-0a0121b94190
docset: aem65
feature: Upgrading
exl-id: c432a014-2dab-4c49-a25b-e4f461d13f9b
source-git-commit: 50a11e30ccd720065962e8dd03cbcc71ec9f715a
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# AEM 6.5의 이전 버전과의 호환성{#backward-compatibility-in-aem}

## 개요 {#overview}

>[!NOTE]
>
>호환성 패키지의 범위에 포함되지 않은 콘텐츠 및 구성 변경 사항 목록은 을 참조하십시오. [AEM의 저장소 재구성](/help/sites-deploying/repository-restructuring.md).

AEM 6.5에서는 모든 기능이 이전 버전과의 호환성을 염두에 두고 개발되었습니다.

대부분의 경우 AEM 6.3을 실행하는 고객은 업그레이드를 수행할 때 코드나 사용자 지정을 변경할 필요가 없습니다. AEM 6.1 및 6.2 고객의 경우 6.3으로 업그레이드하는 동안 발생하는 추가 중단 변경 사항이 없습니다.

이전 버전과의 호환성을 유지할 수 없는 기능의 예외가 발생하면 6.4용 호환성 패키지를 설치하여 번들 및 콘텐츠에 대한 이전 버전과의 비호환성 문제를 완화할 수 있습니다(다운로드 위치에 대한 자세한 내용은 아래 설정 방법 참조). 이 호환성 패키지는 대부분의 경우 AEM 6.4 호환 응용 프로그램의 호환성을 복원하는 데 도움이 됩니다.

호환성 패키지를 사용하면 호환성 모드에서 AEM을 실행하고 새로운 AEM 기능에 대해 사용자 지정 개발을 연기할 수 있습니다.

>[!NOTE]
>
>호환성 패키지는 AEM 6.5 호환에 필요한 개발을 연기하기 위한 임시 솔루션일 뿐이며, 업그레이드 직후 개발을 통해 호환성 문제를 해결할 수 없는 경우 마지막 옵션으로만 권장됩니다. 6.5 기반 사용자 지정 개발을 진행하고 전체 6.5 기능을 사용하려면 기본 모드로 전환하고 호환성 패키지를 제거하는 것이 좋습니다.

![사세](assets/sase.png)

호환성 패키지에는 두 가지 모드가 있습니다. **라우팅 활성화됨** 및 **라우팅 사용 안 함**.

이렇게 하면 AEM 6.5를 다음 세 가지 모드로 실행할 수 있습니다.

**기본 모드:**

기본 모드는 AEM 6.5의 모든 새로운 기능을 사용하고 일부 개발을 수행하여 맞춤화가 모든 새로운 기능과 함께 작동하도록 하려는 고객을 위한 것입니다.

즉, 업그레이드 직후 애플리케이션을 조정해야 할 수 있습니다.

**호환성 모드: 라우팅이 활성화된 호환성 패키지가 설치됨**

호환성 모드는 이전 버전과 호환되지 않는 인터페이스의 사용자 지정을 사용하는 고객을 위한 것입니다. 이를 통해 AEM을 호환성 모드에서 실행하고 일부 사용자 지정 코드와 호환되지 않는 새 AEM 기능에 대해 필요한 사용자 지정 개발을 연기할 수 있습니다.

**레거시 모드: 라우팅이 비활성화된 호환 패키지 설치**

레거시 모드는 호환성 패키지에서 이전된 AEM의 기존 코드 또는 더 이상 사용되지 않는 코드를 기반으로 하는 사용자 지정 인터페이스를 사용하는 고객을 위한 것입니다.

![삽테](assets/sapte.png)

## 설정 방법 {#how-to-set-up}

다음 **6.5용 AEM 6.4 호환성 팩** 는 패키지 관리자를 사용하여 패키지로 설치할 수 있습니다. 다음을 다운로드할 수 있습니다. [소프트웨어 배포의 AEM 6.4 호환성 팩 6.5](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=compat*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=20&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fcompatpack%2Faem-compat-cq65-to-cq64) 사이트.

호환성 패키지가 설치되면 아래와 같이 OSGI 구성에서 스위치를 사용하여 라우팅을 활성화하거나 비활성화할 수 있습니다.

![비교 스위치](assets/compat-switches.png)

호환성 패키지를 설치하고 설정하면 선택한 호환성 모드를 기반으로 기능이 사용됩니다.
