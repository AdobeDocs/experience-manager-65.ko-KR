---
title: AEM Adobe PhoneGap
seo-title: AEM Adobe PhoneGap
description: AEM은 AEM 페이지를 사용하여 앱을 쉽게 만들 수 있도록 PhoneGap과 통합됩니다. Adobe PhoneGap Enterprise를 시작하려면 이 페이지를 따르십시오.
seo-description: AEM integrates with PhoneGap so that you can easily create apps using AEM pages. Follow this page to get started with Adobe PhoneGap Enterprise.
uuid: bdd90cda-2489-4763-a90a-9c409d6e68ae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: fbcdea8a-72e9-431b-9c32-dc02d4cdb9c8
exl-id: d989e235-5993-4738-8523-5b9a5f6bf712
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 1%

---

# AEM Adobe PhoneGap{#aem-adobe-phonegap}

>[!NOTE]
>
>Adobe 단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에는 SPA Editor를 사용하는 것이 좋습니다. [자세히 알아보기](/help/sites-developing/spa-overview.md).

AEM은 AEM 페이지를 사용하여 앱을 쉽게 만들 수 있도록 PhoneGap과 통합됩니다. PhoneGap을 사용하면 사용자가 콘텐츠로 작업할 수 있는 유틸리티 앱을 만들 수 있습니다. 콘텐츠 동기화를 사용하면 앱과 번들로 연결할 페이지의 버전 지정 아카이브를 만들 수 있습니다.

일반적으로 ***AEM 관리자*** 는 생성 마법사를 사용하여 새 앱을 만들거나 기존 애플리케이션을 가져와서 AEM Mobile 카탈로그에 새 애플리케이션을 추가하는 역할을 합니다.

여기에서 ***AEM 작성자*** (또는 *마케터*)는 이제 기본 제공 템플릿 및 구성 요소를 사용하여 페이지를 추가 및 편집하고, 구성 요소를 드래그 앤 드롭하고, 이미지, 비디오 및 텍스트 조각(콘텐츠 조각)을 포함하여 DAM의 모든 유형의 미디어를 추가할 수 있습니다.

AEM Mobile의 진정한 힘은 *총명하* ***AEM 개발자*** 은(는) 사용자 지정 웹 템플릿과 구성 요소를 확장 및 만들어 *AEM 작성자* 매력적이고 매력적인 모바일 경험을 만들 수 있습니다. 이러한 템플릿과 구성 요소는 모바일 앱 환경에 최적화될 뿐만 아니라, 옴니채널 서비스 엔드포인트에 대해 디바이스와 AEM 서버(임의 원격 서버) 모두에 통신합니다.

>[!NOTE]
>
>다음의 경우 *AEM 작성자* 앱이 준비되었다고 판단되면 이해 당사자에게 앱을 다운로드할 수 있습니다. **[Adobe 확인](/help/mobile/phonegap-mobile-quickstart.md)** (AppStore 및 PlayStore 모두에서 사용 가능) 검토 및 승인용. 승인을 받으면 AEM Mobile ContentSync 콘텐츠 릴리스 관리 대시보드를 통해 이 신규 콘텐츠 또는 업데이트된 콘텐츠를 사용자에게 직접 릴리스할 수 있습니다. 한 사람이 여러 역할을 맡을 수 있으며, 이는 귀하와 귀하의 거버넌스 정책에 따라 결정됩니다.

## 사전 요구 사항 {#prerequisites}

AEM Mobile은 완전한 AEM 플랫폼을 구성하는 하나의 기둥에 불과합니다.

AEM Mobile으로 작업하고 이 시작 안내서의 단계를 따르려면 먼저 사용자가 AEM 및 AEM Mobile 제어 센터에 익숙해야 합니다. 다음을 참조하십시오.

[AEM 시작하기](/help/sites-deploying/deploy.md)

[AEM Mobile 제어 센터에 대한 연습](/help/mobile/phonegap-authoring-apps.md)

## 작성자를 위한 빠른 링크 {#quicklinks-for-authors}

다음을 참조하십시오 [AEM에서 Adobe PhoneGap Enterprise용 작성](/help/mobile/phonegap.md) 작성자의 역할과 책임에 대해 알아봅니다.

## 개발자용 빠른 링크 {#quicklinks-for-developers}

AEM Mobile과 통합되고 개발자가 사용자 지정할 수 있는 샘플 애플리케이션이 있습니다. 클릭 [AEM을 사용하여 Adobe PhoneGap Enterprise 개발](/help/mobile/developing-in-phonegap.md).

후속 장에서는 애플리케이션 레이블 지정, 로컬라이제이션, 국제화, ContentSync, 타기팅, Analytics 등과 같은 고급 개념에 대해 알아봅니다.

## 관리자용 빠른 링크 {#quicklinks-for-administrators}

다음을 참조하십시오 [AEM을 사용하여 Adobe PhoneGap Enterprise용 컨텐츠 관리](/help/mobile/administer-phonegap.md) 모바일 애플리케이션을 설정 및 관리합니다.

>[!NOTE]
>
>하이브리드 모바일 기술을 사용하면 다음과 같은 풍부한 모바일 애플리케이션을 만들 수 있습니다. *오프라인 및 온라인 실행* 실제로 AEM Mobile을 사용하면 많은 고객이 온라인 또는 오프라인 상태일 때를 확인하고 그에 따라 동작하는 앱을 만들도록 선택합니다.
