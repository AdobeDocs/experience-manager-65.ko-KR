---
title: 우수 사례
seo-title: 우수 사례
description: 모바일 앱 템플릿 및 구성 요소를 빌드하려는 sites에 대한 숙련된 AEM 개발자에게 도움이 되는 모범 사례 및 지침을 알려면 이 페이지를 따르십시오.
seo-description: 모바일 앱 템플릿 및 구성 요소를 빌드하려는 sites에 대한 숙련된 AEM 개발자에게 도움이 되는 모범 사례 및 지침을 알려면 이 페이지를 따르십시오.
uuid: 7733c8b1-a88c-455c-8080-f7add4205b92
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a0647696-72c3-409b-85ba-9275d8f99cff
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 1%

---

# 우수 사례 {#best-practices}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

AEM Mobile On-demand Services 앱을 빌드하는 것은 Cordova(또는 PhoneGap) 셸에서 직접 실행되는 앱을 빌드하는 것과 다릅니다. 개발자는 다음 사항에 익숙해야 합니다.

* 기본적으로 지원되는 플러그인과 AEM Mobile 관련 플러그인이 있습니다.

>[!NOTE]
>
>플러그인에 대한 자세한 내용은 다음 리소스를 참조하십시오.
>
>* [AEM Mobile에서 Cordova 플러그인 사용](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [AEM Mobile용 Cordova 활성화 플러그인 사용](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)

>



* 플러그인 기능을 사용하는 템플릿은 플러그인 브리지가 없는 브라우저에서 계속 작성할 수 있도록 작성해야 합니다.

   * 예를 들어 플러그인의 API에 액세스하려고 하기 전에 *deviceready* 함수를 대기해야 합니다.

## AEM 개발자를 위한 지침 {#guidelines-for-aem-developers}

다음 지침은 모바일 앱 템플릿 및 구성 요소를 빌드하려는 숙련된 AEM for sites 개발자에게 도움이 됩니다.

**재사용 및 확장성을 유도하기 위해 AEM 사이트 템플릿을 구조화합니다.**

* 단일 모놀리식 스크립트보다 여러 구성 요소 스크립트 파일 필요

   * *customerlibs.html* 및 *customfoterlibs.html*&#x200B;와 같이 많은 빈 확장 포인트가 제공되는데, 이 경우 개발자는 가능한 한 적은 코어 코드를 복제하면서도 페이지 템플릿을 변경할 수 있습니다
   * 그런 다음 Sling의 *sling:resourceSuperType* 메커니즘을 통해 템플릿을 확장 및 사용자 지정할 수 있습니다

* 템플릿 언어로서 JSP보다 Sightly/HTL을 선호함

   * 이를 사용하면 마크업과 XSS 보호 기능을 갖춘 오퍼를 분리하고 보다 친숙한 구문을 사용할 수 있습니다

**장치 내 성능 최적화**

* 문서 특정 스크립트 및 스타일시트는 dps-article contentsync 템플릿을 사용하여 문서 페이로드에 포함해야 합니다
* 두 개 이상의 문서가 공유하는 스크립트 및 스타일시트는 dps-HTMLRessources contentsync 템플릿을 통해 공유 리소스에 포함해야 합니다
* 렌더링 차단 상태인 외부 스크립트를 참조하지 마십시오

>[!NOTE]
>
>렌더링 차단 외부 스크립트 [여기](https://developers.google.com/speed/docs/insights/BlockingJS)에 대해 자세히 알 수 있습니다.

**웹용 JS 및 CSS 라이브러리보다 앱별 클라이언트측 JS 및 CSS 라이브러리 선호함**

* jQuery Mobile과 같은 라이브러리의 오버헤드를 방지하기 위해 매우 광범위한 장치와 브라우저를 처리합니다
* 템플릿이 앱의 웹 보기에서 실행되는 경우 해당 앱이 지원할 플랫폼과 버전 및 JavaScript 지원이 있다는 지식을 제어할 수 있습니다. 예를 들어, Bootstrap보다 jQuery Mobile 및 Onsen UI보다 Ionic(아마도 CSS)을 선호합니다.

>[!NOTE]
>
>jQuery 모바일에 대해 자세히 알아보려면 [여기](https://jquerymobile.com/browser-support/1.4/)를 클릭하십시오.

**전체 스택보다 마이크로 라이브러리 선호**

* 컨텐츠가 장치 유리에 도달하는 데 걸리는 시간은 문서가 의존하는 모든 라이브러리에 의해 느려집니다. 모든 문서를 렌더링하는 데 새 웹 보기를 사용하는 경우 이러한 둔화는 가중되므로 각 라이브러리를 처음부터 다시 초기화해야 합니다
* 문서가 SPA(단일 페이지 앱)로 빌드되지 않은 경우 Angular과 같은 전체 스택 라이브러리를 포함할 필요가 없습니다
* [Fastclick](https://github.com/ftlabs/fastclick) 또는 [Velocity.js](https://velocityjs.org)와 같이 페이지에 필요한 인터랙션을 추가하려면 더 작은 단일 목적 라이브러리를 선호하십시오

**문서 페이로드 크기 최소화**

* 합리적인 해상도로 지원할 가장 큰 뷰포트를 효과적으로 커버할 수 있는 가장 작은 자산을 사용하십시오
* 이미지에 *ImageOptimizer* 같은 도구를 사용하여 불필요한 메타데이터를 제거합니다

## 미리 보기 {#getting-ahead}

다른 두 역할과 책임에 대한 자세한 내용은 아래 리소스를 참조하십시오.

* [관리자](/help/mobile/aem-mobile.md)
* [작성](/help/mobile/aem-mobile-on-demand.md)
