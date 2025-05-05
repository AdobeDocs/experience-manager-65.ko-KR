---
title: AEM Mobile On-demand Services 우수 사례
description: 모바일 앱 템플릿 및 구성 요소를 빌드하려는 사이트에 대해 유능한 Adobe Experience Manager(AEM) 개발자를 지원하는 모범 사례 및 지침에 대해 알아봅니다.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# 모범 사례 {#best-practices}

{{ue-over-mobile}}

AEM Mobile On-demand Services 앱을 빌드하는 것은 Cordova(또는 PhoneGap) 셸에서 직접 실행되는 앱을 빌드하는 것과 다릅니다. 개발자는 다음 사항에 익숙해야 합니다.

* 즉시 지원되는 플러그인 및 Adobe Experience Manager(AEM) 모바일 특정 플러그인입니다.

>[!NOTE]
>
>플러그인에 대해 자세히 알아보려면 다음 리소스를 참조하십시오.
>
>* [AEM Mobile에서 Cordova 플러그인 사용](https://helpx.adobe.com/kr/digital-publishing-solution/help/cordova-api.html)
>* [AEM Mobile 전용 Cordova 사용 플러그인 사용](https://helpx.adobe.com/kr/digital-publishing-solution/help/app-runtime-api.html)
>

* 플러그인 기능을 사용하는 템플릿은 플러그인 브리지가 없어도 브라우저에서 계속 작성할 수 있는 방식으로 작성되어야 합니다.

   * 예를 들어 플러그 인의 API에 액세스하기 전에 *deviceready* 함수를 기다려야 합니다.

## AEM 개발자를 위한 지침 {#guidelines-for-aem-developers}

다음 지침은 모바일 앱 템플릿 및 구성 요소를 빌드하려는 사이트에 대해 유능한 AEM 개발자를 지원하는 데 도움이 됩니다.

**재사용 및 확장성을 장려하는 AEM 사이트 템플릿 구성**

* 단일 모놀리식 스크립트보다 여러 구성 요소 스크립트 파일 선호

   * *customheaderlibs.html* 및 *customfooterlibs.html*&#x200B;과 같은 빈 확장 지점이 제공되어 개발자가 가능한 한 적은 수의 코어 코드를 복제하는 동안 페이지 템플릿을 변경할 수 있습니다
   * 그런 다음 Sling의 *sling:resourceSuperType* 메커니즘을 통해 템플릿을 확장하고 사용자 지정할 수 있습니다.

* 템플릿 언어로서 JSP보다 Sightly/HTL 선호

   * 이를 사용하면 마크업에서 코드가 분리되고, 내장된 XSS 보호를 제공하며, 더 익숙한 구문이 있습니다

**온디바이스 성능 최적화**

* dps-article contentsync 템플릿을 사용하여 아티클별 스크립트 및 스타일 시트를 아티클 페이로드에 포함해야 합니다
* 둘 이상의 문서에서 공유한 스크립트 및 스타일 시트는 dps-HTMLResources contentsync 템플릿을 통해 공유 리소스에 포함되어야 합니다
* 렌더링 차단되는 외부 스크립트를 참조하지 않음

>[!NOTE]
>
>렌더링 차단 외부 스크립트에 대한 자세한 내용은 [여기](https://developers.google.com/speed/docs/insights/BlockingJS)를 참조하세요.

**웹용 라이브러리보다 앱별 클라이언트측 JS 및 CSS 라이브러리 선호**

* jQuery Mobile과 같은 라이브러리에서 오버헤드를 방지하여 광범위한 디바이스와 브라우저를 처리합니다.
* 템플릿이 앱의 웹 보기에서 실행될 때 앱이 지원할 플랫폼 및 버전을 제어하고 JavaScript에서 지원하는 지식이 제공됩니다. 예를 들어, jQuery Mobile보다 Ionic(CSS만 해당), Bootstrap보다 Onsen UI를 선호합니다.

>[!NOTE]
>
>jQuery mobile에 대해 자세히 알아보려면 [여기](https://jquerymobile.com/browser-support/1.4/)를 클릭하십시오.

**전체 스택보다 마이크로 라이브러리 선호**

* 콘텐트가 장치 유리에 표시되는 데 걸리는 시간은 문서가 의존하는 모든 라이브러리에 의해 느려집니다. 이 둔화는 새 웹 보기를 사용하여 모든 문서를 렌더링할 때 혼합되므로 각 라이브러리를 처음부터 다시 초기화해야 합니다
* 문서가 SPA(단일 페이지 앱)로 빌드되지 않은 경우 Angular과 같은 전체 스택 라이브러리를 포함할 필요가 없을 수 있습니다
* [Fastclick](https://github.com/ftlabs/fastclick) 또는 [Velocity.js](https://velocityjs.org)와 같이 페이지에 필요한 상호 작용을 추가하는 데 도움이 되는 더 작은 단일 목적 라이브러리를 선호합니다.

**문서 페이로드 크기 최소화**

* 지원 중인 가장 큰 뷰포트를 효과적으로 지원할 수 있는 가장 작은 에셋을 합리적인 해상도로 사용합니다
* 초과 메타데이터를 제거할 수 있도록 이미지에 *ImageOptim*&#x200B;과(와) 같은 도구를 사용하십시오.

## 시작하기 {#getting-ahead}

다른 두 가지 역할과 책임에 대한 자세한 내용은 아래 리소스를 참조하십시오.

* [관리자](/help/mobile/aem-mobile.md)
* [작성자](/help/mobile/aem-mobile-on-demand.md)
