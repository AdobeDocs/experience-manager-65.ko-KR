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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM Adobe PhoneGap{#aem-adobe-phonegap}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

AEM은 PhoneGap과 통합되므로 AEM 페이지를 사용하여 앱을 쉽게 만들 수 있습니다. PhoneGap을 사용하면 사용자가 컨텐츠를 사용하여 작업할 수 있는 유틸리티 앱을 만들 수 있습니다. 컨텐츠 동기화를 사용하면 앱과 번들로 묶을 수 있는 페이지 아카이브를 만들 수 있습니다.

일반적으로 AEM ***관리자는*** 만들기 마법사를 사용하여 새 앱을 만들거나 기존 애플리케이션을 가져와 AEM Mobile 카탈로그에 새 애플리케이션을 추가할 책임이 있습니다.

여기에서 AEM ***작성자*** (또는 마케터 **)는 바로 사용 가능한 템플릿과 구성 요소를 사용하여 페이지를 추가 및 편집하고 구성 요소를 드래그 앤 드롭하며 DAM에서 이미지, 비디오 및 텍스트 조각(컨텐츠 조각)을 비롯한 모든 유형의 미디어를 추가할 수 있습니다.

AEM Mobile의 진정한 장점은 *전문* AEM Developer ***가*** 사용자 정의 웹 템플릿과 구성 요소를 확장 및 만들어 AEM Author가 *매력적이고 멋진* 모바일 경험을 만들 수 있다는것입니다. 이러한 템플릿 및 구성 요소는 모바일 앱 환경에만 최적화되어 있지 않습니다.그러나 장치 및 AEM 서버(모든 원격 서버)와 전체 채널 서비스 종단점에 모두 통신합니다.

>[!NOTE]
>
>AEM *작성자가* 앱이 준비되었다고 판단하면 우선 이해 관계자가 검토 및 승인을 위해 Adobe Verify(AppStore와 PlayStore 모두에서 **[](/help/mobile/phonegap-mobile-quickstart.md)**사용 가능)를 사용하여 앱을 다운로드하도록 할 수 있습니다. 녹색 표시등이 켜지면 AEM Mobile ContentSync 콘텐츠 릴리스 관리 대시보드를 통해 사용자에게 직접 이 새로운 콘텐츠나 업데이트된 콘텐츠를 제공할 수 있습니다. 한 사람이 모든 역할을 맡을 수 있으며, 이는 귀하와 귀하의 관리 정책에 달려 있습니다.

## 전제 조건 {#prerequisites}

AEM Mobile은 전체 AEM 플랫폼을 구성하는 한 기둥에 불과합니다.

AEM Mobile을 사용하여 작업하고 이 시작하기 안내서의 단계를 따르기 전에 AEM 및 AEM Mobile Control Center에 익숙해야 합니다. 다음을 참조하십시오.

[AEM 시작하기](/help/sites-deploying/deploy.md)

[AEM Mobile 컨트롤 센터 연습](/help/mobile/phonegap-authoring-apps.md)

## 작성자를 위한 빠른 링크 {#quicklinks-for-authors}

작성자의 [역할과 책임에 대한 자세한 내용은 AEM의](/help/mobile/phonegap.md) Adobe PhoneGap Enterprise용 작성을 참조하십시오.

## 개발자를 위한 QuickLinks {#quicklinks-for-developers}

AEM Mobile과 통합되고 개발자가 사용자 정의할 수 있는 샘플 애플리케이션이 있습니다. Developing [Adobe PhoneGap Enterprise with AEM을 클릭합니다](/help/mobile/developing-in-phonegap.md).

이후 장에서는 애플리케이션, 현지화, 국제화, ContentSync, Targeting, Analytics 등과 같은 고급 개념에 대해 살펴봅니다.

## 관리자를 위한 빠른 링크 {#quicklinks-for-administrators}

모바일 [애플리케이션을 설정 및](/help/mobile/administer-phonegap.md) 관리하려면 Adobe PhoneGap Enterprise와 AEM용 컨텐츠 관리를 참조하십시오.

>[!NOTE]
>
>하이브리드 모바일 기술을 사용하면 AEM Mobile을 사용하여 오프라인 및 온라인 *방식으로* 실행되는 리치 모바일 애플리케이션을 제작할 수 있습니다. 많은 고객은 온라인 또는 오프라인 상태에 따라 반응하는 앱을 제작하려고 합니다.
