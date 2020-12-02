---
title: AEM Adobe PhoneGap
seo-title: AEM Adobe PhoneGap
description: AEM은 PhoneGap과 통합되어 있으므로 AEM 페이지를 사용하여 앱을 손쉽게 제작할 수 있습니다. 이 페이지에 따라 Adobe PhoneGap Enterprise를 시작하십시오.
seo-description: AEM은 PhoneGap과 통합되어 있으므로 AEM 페이지를 사용하여 앱을 손쉽게 제작할 수 있습니다. 이 페이지에 따라 Adobe PhoneGap Enterprise를 시작하십시오.
uuid: bdd90cda-2489-4763-a90a-9c409d6e68ae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: fbcdea8a-72e9-431b-9c32-dc02d4cdb9c8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 1%

---


# AEM Adobe PhoneGap{#aem-adobe-phonegap}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에서는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

AEM은 PhoneGap과 통합되어 있으므로 AEM 페이지를 사용하여 앱을 손쉽게 제작할 수 있습니다. PhoneGap을 사용하면 사용자가 컨텐츠를 사용하여 작업할 수 있는 유틸리티 앱을 만들 수 있습니다. 컨텐츠 동기화를 사용하면 앱과 번들로 묶을 페이지의 버전 관리 아카이브를 만들 수 있습니다.

일반적으로 ***AEM 관리자***&#x200B;는 만들기 마법사를 사용하여 새 앱을 만들거나 기존 애플리케이션을 가져와 새 애플리케이션을 AEM Mobile 카탈로그에 추가할 책임이 있습니다.

여기서 ***AEM 작성자***(또는 *마케터*)는 이제 즉시 사용 가능한 템플릿 및 구성 요소를 사용하여 페이지를 추가 및 편집하고, 구성 요소를 드래그 앤 드롭하고 DAM에서 이미지, 비디오 및 텍스트 조각(컨텐츠 조각)을 비롯한 모든 유형의 미디어를 추가할 수 있습니다.

AEM Mobile의 진정한 장점은 *맹세* ***AEM 개발자***&#x200B;가 사용자 정의 웹 템플릿 및 구성 요소를 확장 및 만들어 *AEM Author*&#x200B;에서 매력적이고 매력적인 모바일 경험을 제작할 수 있다는 것입니다. 이러한 템플릿 및 구성 요소는 모바일 앱 환경에만 최적화되어 있을 뿐만 아니라그러나 장치 및 AEM 서버(모든 원격 서버)와 옴니채널 서비스 종단점을 모두 통신합니다.

>[!NOTE]
>
>*AEM 작성자*&#x200B;가 앱이 준비되었다고 생각되면 우선 이해 관계자가 검토 및 승인을 위해 **[Adobe Verify](/help/mobile/phonegap-mobile-quickstart.md)**(AppStore 및 PlayStore 모두에서 제공)로 앱을 다운로드하도록 할 수 있습니다. 일단 녹색 조명을 받으면 AEM Mobile ContentSync 컨텐츠 릴리스 관리 대시보드를 통해 사용자에게 이 새로운 콘텐츠나 업데이트된 콘텐츠를 바로 제공할 수 있습니다. 한 사람이 모든 역할을 수행할 수 있으며 이는 귀하와 귀하의 관리 정책에 달려 있습니다.

## 전제 조건 {#prerequisites}

AEM Mobile은 완벽한 AEM 플랫폼을 구성하는 한 기둥이다.

AEM Mobile을 사용하여 작업하고 이 시작하기 안내서의 단계를 따르기 전에 사용자는 AEM 및 AEM Mobile 제어 센터에 익숙해야 합니다. 다음을 참조하십시오.

[AEM 시작하기](/help/sites-deploying/deploy.md)

[AEM Mobile 제어 센터 연습](/help/mobile/phonegap-authoring-apps.md)

## 작성자를 위한 빠른 링크 {#quicklinks-for-authors}

작성자의 역할 및 책임을 알아보려면 AEM](/help/mobile/phonegap.md)에서 Adobe PhoneGap 엔터프라이즈용 작성[을 참조하십시오.

## 개발자용 QuickLinks {#quicklinks-for-developers}

AEM Mobile과 통합되고 개발자가 사용자 정의할 수 있는 샘플 애플리케이션이 있습니다. [AEM이 있는 Adobe PhoneGap 엔터프라이즈 개발](/help/mobile/developing-in-phonegap.md)을 클릭합니다.

이후 장에서는 애플리케이션, 로컬라이제이션, 국제화, ContentSync, 타깃팅, 분석 등과 같은 고급 개념을 소개합니다.

## 관리자용 빠른 링크 {#quicklinks-for-administrators}

모바일 응용 프로그램을 설정하고 관리하려면 [AEM](/help/mobile/administer-phonegap.md)과 함께 Adobe PhoneGap Enterprise용 내용 관리를 참조하십시오.

>[!NOTE]
>
>하이브리드 모바일 기술을 사용하면 AEM Mobile과 함께 *오프라인 및 온라인*&#x200B;을 실행하는 리치 모바일 애플리케이션을 제작할 수 있습니다. 실제로 많은 고객이 온라인 또는 오프라인일 때 앱을 확인하고 그에 따라 동작하는 앱을 제작하려고 합니다.
