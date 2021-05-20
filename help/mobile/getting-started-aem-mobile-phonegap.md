---
title: AEM Adobe PhoneGap
seo-title: AEM Adobe PhoneGap
description: AEM은 PhoneGap과 통합되므로 AEM 페이지를 사용하여 앱을 쉽게 만들 수 있습니다. Adobe PhoneGap Enterprise를 시작하려면 이 페이지를 따르십시오.
seo-description: AEM은 PhoneGap과 통합되므로 AEM 페이지를 사용하여 앱을 쉽게 만들 수 있습니다. Adobe PhoneGap Enterprise를 시작하려면 이 페이지를 따르십시오.
uuid: bdd90cda-2489-4763-a90a-9c409d6e68ae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: fbcdea8a-72e9-431b-9c32-dc02d4cdb9c8
exl-id: d989e235-5993-4738-8523-5b9a5f6bf712
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 1%

---

# AEM Adobe PhoneGap{#aem-adobe-phonegap}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

AEM은 PhoneGap과 통합되므로 AEM 페이지를 사용하여 앱을 쉽게 만들 수 있습니다. PhoneGap을 사용하면 사용자가 컨텐츠에서 작업할 수 있는 유틸리티 앱을 만들 수 있습니다. 컨텐츠 동기화를 사용하면 앱과 번들링을 위해 페이지의 버전이 지정된 아카이브를 만들 수 있습니다.

일반적으로 ***AEM 관리자***&#x200B;는 만들기 마법사를 사용하여 새 앱을 만들거나 기존 애플리케이션을 가져와서 새 애플리케이션을 AEM Mobile 카탈로그에 추가해야 합니다.

여기에서 ***AEM Author***(또는 *Marketter*)는 이제 기본 제공 템플릿 및 구성 요소를 사용하여 페이지를 추가 및 편집하고, 구성 요소를 드래그 앤 드롭하고 이미지, 비디오 및 텍스트 조각(컨텐츠 조각)을 포함하여 DAM에서 모든 유형의 미디어를 추가할 수 있습니다.

AEM Mobile의 진정한 장점은 *데비드* ***AEM 개발자***&#x200B;가 사용자 지정 웹 템플릿과 구성 요소를 확장 및 만들어 *AEM 작성자*&#x200B;에서 아름답고 매력적인 모바일 경험을 만들 수 있다는 것입니다. 이러한 템플릿 및 구성 요소는 모바일 앱 환경에만 최적화되어 있지 않습니다.그러나 장치 및 AEM 서버(임의의 원격 서버)에 모두 연결하여 옴니채널 서비스 종단점에 연결합니다.

>[!NOTE]
>
>*AEM Author*&#x200B;가 앱이 준비되었다고 생각되면 먼저 이해 관계자가 검토 및 승인을 위해 **[Adobe 확인](/help/mobile/phonegap-mobile-quickstart.md)**(AppStore 및 PlayStore 모두에서 사용 가능)을 사용하여 앱을 다운로드하도록 할 수 있습니다. 일단 녹색 표시등이 켜지면 AEM Mobile ContentSync 콘텐츠 릴리스 관리 대시보드를 통해 사용자에게 직접 이 새로운 콘텐츠 또는 업데이트된 콘텐츠를 릴리스할 수 있습니다. 한 사람이 어떤 수의 역할이든 맡을 수 있으며, 이는 여러분과 여러분의 거버넌스 정책입니다.

## 전제 조건 {#prerequisites}

AEM Mobile은 전체 AEM 플랫폼을 구성하는 한 기둥에 지나지 않습니다.

AEM Mobile을 사용하여 작업하고 이 시작 안내서의 단계를 따르려면 먼저 AEM 및 AEM Mobile 컨트롤 센터에 대해 알고 있어야 합니다. 다음을 참조하십시오.

[AEM 시작하기](/help/sites-deploying/deploy.md)

[AEM Mobile Control Center 연습](/help/mobile/phonegap-authoring-apps.md)

## 작성자에 대한 빠른 링크 {#quicklinks-for-authors}

작성자의 역할과 책임에 대해 알려면 [AEM에서 Adobe PhoneGap Enterprise용 작성](/help/mobile/phonegap.md)을 참조하십시오.

## 개발자를 위한 빠른 링크 {#quicklinks-for-developers}

AEM Mobile과 통합되고 개발자가 사용자 지정할 수 있는 샘플 애플리케이션이 있습니다. [AEM을 사용하여 Adobe PhoneGap Enterprise 개발](/help/mobile/developing-in-phonegap.md)을 클릭합니다.

이후 장에서는 애플리케이션, 현지화, 국제화, ContentSync, Targeting, Analytics 등 고급 개념에 대해 알아봅니다.

## 관리자용 빠른 링크 {#quicklinks-for-administrators}

모바일 애플리케이션을 설정 및 관리하려면 [AEM을 사용하여 Adobe PhoneGap Enterprise용 컨텐츠 관리](/help/mobile/administer-phonegap.md)를 참조하십시오.

>[!NOTE]
>
>하이브리드 모바일 기술을 사용하면 *오프라인 및 AEM Mobile을 사용하여 온라인*&#x200B;으로 실행하는 풍부한 모바일 애플리케이션을 만들 수 있습니다. 실제로 많은 고객이 온라인 또는 오프라인일 때를 확인하고 그에 따라 동작하는 앱을 생성하도록 선택할 수 있습니다.
