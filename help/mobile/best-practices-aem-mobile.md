---
title: 우수 사례
seo-title: 우수 사례
description: 모바일 앱 템플릿 및 구성 요소를 구축하려는 사이트의 숙련된 AEM 개발자에게 도움이 되는 모범 사례와 가이드라인을 살펴보려면 이 페이지를 따르십시오.
seo-description: 모바일 앱 템플릿 및 구성 요소를 구축하려는 사이트의 숙련된 AEM 개발자에게 도움이 되는 모범 사례와 가이드라인을 살펴보려면 이 페이지를 따르십시오.
uuid: 7733c8b1-a88c-455c-8080-f7add4205b92
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a0647696-72c3-409b-85ba-9275d8f99cff
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 1%

---


# 우수 사례 {#best-practices}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

AEM Mobile On-demand Services 앱을 빌드하는 것은 Cordova(또는 PhoneGap) 셸에서 직접 실행되는 앱을 빌드하는 것과 다릅니다. 개발자는

* AEM Mobile 특정 플러그인뿐만 아니라 기본적으로 지원되는 플러그인입니다.

>[!NOTE]
>
>플러그인에 대한 자세한 내용은 다음 리소스를 참조하십시오.
>
>* [AEM Mobile에서 Cordova 플러그인 사용](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [AEM Mobile 전용 Cordova 활성 플러그인 사용](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)

>



* 플러그인 기능을 사용하는 템플릿은 플러그인 브리지가 없는 브라우저에서 계속 저작할 수 있도록 작성해야 합니다.

   * 예를 들어 플러그인의 API에 액세스하기 전에 *deviceready* 함수를 기다려야 합니다.

## AEM 개발자를 위한 지침 {#guidelines-for-aem-developers}

다음 지침은 모바일 앱 템플릿 및 구성 요소를 빌드하려는 사이트를 위한 숙련된 AEM 개발자에게 도움이 됩니다.

**AEM 사이트 템플릿을 구성하여 재사용 및 확장성 촉진**

* 하나의 모놀리식 파일 대신 여러 구성 요소 스크립트 파일 필요

   * *customerlibs.html* 및 *customfoterlibs.html*&#x200B;과 같은 빈 확장 지점이 제공되며, 이 경우 개발자는 가능한 한 적은 코어 코드를 복제하는 동안 페이지 템플릿을 변경할 수 있습니다.
   * 그런 다음 Sling의 *sling:resourceSuperType* 메커니즘을 통해 템플릿을 확장하고 사용자 정의할 수 있습니다.

* 템플릿 작성 언어로 JSP보다 Sightly/HTL을 선호함

   * 이 기능을 사용하면 마크업과 코드가 분리되고, XSS 보호 기능이 내장되어 있으며, 보다 익숙한 구문이 제공됩니다

**디바이스 내 성능 최적화**

* 아티클 특정 스크립트 및 스타일 시트는 dps-article contentsync 템플릿을 사용하여 아티클 페이로드에 포함되어야 합니다.
* 둘 이상의 아티클에서 공유한 스크립트 및 스타일 시트는 dps-HTMLResources contentsync 템플릿을 통해 공유 리소스에 포함되어야 합니다
* 렌더링 차단 중인 외부 스크립트를 참조하지 마십시오.

>[!NOTE]
>
>렌더링 차단 외부 스크립트 [여기](https://developers.google.com/speed/docs/insights/BlockingJS)에 대해 자세히 알아볼 수 있습니다.

**웹 전용 JS 및 CSS 라이브러리 대신 앱 전용 클라이언트측 JS 및 CSS 라이브러리 선호**

* jQuery Mobile과 같은 라이브러리의 오버헤드를 방지하여 다양한 디바이스와 브라우저를 처리할 수 있습니다.
* 템플릿이 앱의 웹 뷰에서 실행되는 경우 JavaScript 지원이 제공된다는 것은 물론, 앱이 지원할 플랫폼과 버전을 제어할 수 있습니다. 예를 들어 Bootstrap보다 Ionic(예: CSS)을 선호하고 jQuery Mobile과 온센 UI를 선호합니다.

>[!NOTE]
>
>jQuery Mobile에 대한 자세한 내용을 보려면 [여기](https://jquerymobile.com/browser-support/1.4/)를 클릭하십시오.

**전체 스택보다 마이크로 라이브러리 선호**

* 아티클이 의존하는 모든 라이브러리에서 콘텐츠를 장치의 유리에 가져오는 데 걸리는 시간이 느려집니다. 모든 아티클을 렌더링하는 데 새로운 웹 보기를 사용하는 경우 이 감소 효과는 더욱 향상되므로 각 라이브러리를 처음부터 다시 초기화해야 합니다
* 아티클이 SPA(단일 페이지 앱)로 빌드되지 않은 경우 Angular와 같은 전체 스택 라이브러리를 포함할 필요가 없을 수 있습니다
* [Fastclick](https://github.com/ftlabs/fastclick) 또는 [Velocity.js](https://velocityjs.org)와 같이 페이지에 필요한 인터랙션을 추가할 수 있도록 작은 단일 목적의 라이브러리를 선호합니다.

**아티클 페이로드 크기 최소화**

* 적절한 해상도로 지원할 가장 큰 뷰포트를 효과적으로 덮을 수 있는 가장 작은 에셋을 사용합니다.
* 이미지에 *ImageOptim*&#x200B;과 같은 도구를 사용하여 초과되는 메타데이터를 제거합니다.

## {#getting-ahead} 앞에 가져오기

다른 두 가지 역할과 책임에 대한 자세한 내용은 아래 리소스를 참조하십시오.

* [관리자](/help/mobile/aem-mobile.md)
* [작성](/help/mobile/aem-mobile-on-demand.md)
