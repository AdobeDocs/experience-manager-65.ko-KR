---
title: PWA Studio을 위한 AEM 확장 시작하기
description: PWA Studio을 사용하여 AEM Headless 콘텐츠 및 상거래 프로젝트를 배포하는 방법에 대해 알아봅니다.
topics: Commerce
feature: Commerce Integration Framework
exl-id: de7b8f05-b6b7-4105-84a5-940c16ebf2b4
solution: Experience Manager,Commerce
source-git-commit: 1751bfb32386685e3a159939113b9667b5e17f0e
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 0%

---

# PWA Studio을 위한 AEM 확장 시작하기 {#getting-started-pwa}

즉시 사용 가능한 PWA Studio은 GraphQL을 통해 Adobe Commerce과 원활하게 통합되어 혁신적이고 매력적인 상점 및 기타 디지털 경험을 구축할 수 있는 옵션을 무제한으로 제공합니다.

콘텐츠 조각은 GraphQL을 API로 사용하여 다양한 형식(예: JSON, Markdown)으로 Headless 방식으로 소비하고 독립적으로 렌더링할 수 있도록 하는 사전 정의된 구조의 콘텐츠 조각입니다. 컨텐츠 조각에는 GraphQL에서 애플리케이션이 사용 가능한 항목만 요청하고 예상되는 항목을 수신하도록 하는 데 필요한 모든 데이터 유형과 필드가 포함되어 있습니다. 구성 방식 측면에서 제공되는 유연성은 여러 위치 및 여러 채널에서 사용하기에 적합합니다.

Adobe Experience Manager 내의 콘텐츠 조각 모델 편집기를 사용하면 필요한 구조를 쉽게 디자인할 수 있습니다. Adobe Experience Manager 콘텐츠 조각(또는 기타 데이터)을 PWA Studio 애플리케이션과 통합하는 주요 과제는 여러 GraphQL 끝점에서 데이터를 가져오는 것입니다. 이유는 기본적으로 PWA Studio이 단일 Adobe Commerce GraphQL 종단점에서 작동하기 때문입니다.

## 아키텍처 {#architecture}

![PWA 헤드리스 아키텍처](/help/commerce/cif/assets/pwa-studio/PWA-Studio_Architecture.png)

## 설정 PWA Studio {#setup-pwa}

PWA Studio 앱을 설정하려면 Adobe Commerce을 따르십시오 [PWA Studio 설명서](https://developer.adobe.com/commerce/pwa-studio/tutorials/).

AEM의 GraphQL 끝점과 PWA Studio을 연결하려면 [PWA Studio을 위한 AEM 확장](https://github.com/adobe/aem-pwa-studio-extensions).

1. 저장소 체크 아웃

1. PWA Studio 애플리케이션에서 확장을 개발 종속성으로 추가합니다.

   ```javascript
   yarn add --dev file:{path-to-extension}/extension
   ```

1. Apollo Link 래퍼를 PWA Studio 애플리케이션에 추가합니다. pwa-root/src/index.js에서 다음 사항을 변경합니다.

   ```javascript
     import { linkWrapper } from '@adobe/pwa-studio-aem-cfm-blog-extension';
   
   // ...
   
   <Adapter apiBase={apiBase} apollo={{ link: linkWrapper(apolloLink) }} store={store}>
   ```

   에서 아폴로 클라이언트 사용자 지정에 대한 자세한 내용을 찾을 수 있습니다. [linkWrapper.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/linkWrapper.js).

1. 블로그 항목으로 탐색 구성 요소를 확장하려면 pwa-root/local-intercept.js에 다음 수정 사항을 추가하십시오.

   ```javascript
   const addBlogToNavigation = require('@adobe/pwa-studio-aem-cfm-blog-extension/src/addBlogToNavigation');
   
   function localIntercept(targets) {
       addBlogToNavigation(targets);
   }    
   ```

   탐색 구성 요소 맞춤화에 대한 자세한 내용은에서 확인할 수 있습니다. [addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js) 및 [확장성 프레임워크](https://developer.adobe.com/commerce/pwa-studio/guides/general-concepts/extensibility/) PWA Studio 설명서.

1. Apollo 고객은 AEM GraphQL 엔드포인트를 다음 위치에 기대합니다. `<https://pwa-studio/endpoint.js>`. 끝점을 이 위치에 매핑하려면 PWA Studio 응용 프로그램의 UPPER 구성을 사용자 지정합니다(a. To). `pwa-root/.env`를 클릭하고 AEM_CFM_GRAPHQL 변수를 추가한 다음 AEM 콘텐츠 조각 GraphQL 엔드포인트를 가리키도록 조정합니다.

   예: AEM_CFM_GRAPHQL=<http://localhost:4503/content/graphql/global>

   b. 상향 구성에 프록시 해결자를 추가합니다. 샘플 상향 구성은 다음과 같습니다.

```json
   response:
     resolver: conditional
     when:
       - matches: request.url.pathname
         pattern: ^/endpoint.json(/|$)
         use: aemProxy
     default: veniaResponse

   aemProxy:
     resolver: proxy
     target: env.AEM_CFM_GRAPHQL
     ignoreSSLErrors: true

   status: response.status
   headers: response.headers
   body: response.body
```

## AEM 설정 {#setup-aem}

AEM 콘텐츠 조각 설명서에 따라 AEM 프로젝트에 대한 GraphQL 끝점을 설정합니다. 또한 AEM 프로젝트에서 다음 구성을 추가하여 PWA Studio 애플리케이션이 GraphQL 엔드포인트에 액세스할 수 있도록 합니다.

* Adobe Granite 원본 간 리소스 공유 정책(com.adobe.granite.cors.impl.CORSPolicyImpl)

  설정 `allowedorigin` 속성을 PWA 애플리케이션의 전체 호스트 이름으로 설정합니다.

  예:  `<https://pwa-studio-test-vflyn.local.pwadev:9366>`

* Apache Sling Referrer Filter (org.apache.sling.security.impl.ReferrerFilter.cfg.json)

  allow.hosts 속성을 PWA 응용 프로그램의 호스트 이름으로 설정합니다.

  예: pwa-studio-test-vflyn.local.pwadev

두 구성의 전체 예는 여기에서 찾을 수 있습니다. <https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config>.

GraphQL 엔드포인트를 표시하기 위해 Adobe은 콘텐츠 패키지를 통해 일부 샘플 콘텐츠 조각 모델 및 데이터를 준비했습니다. 이러한 조각은 PWA Studio 확장과 함께 제공된 React Components와 함께 작동합니다.

## 사용 방법 {#how-to-use}

이 확장은 PWA Studio 애플리케이션을 AEM과 연결하여 GraphQL을 통해 콘텐츠를 검색하고 렌더링하는 방법의 예제 구현으로 간주됩니다.

사용 사례에 따라 사용자 지정 콘텐츠 조각 모델을 만들어 사용자 지정 GraphQL 스키마를 만들고 이를 자체 React 구성 요소에서 사용할 수 있습니다.

프로덕션 설정은 여러 측면에서 달라질 수 있습니다.

* Apollo 클라이언트를 사용자 지정하는 대신 AEM과 Adobe Commerce GraphQL 데이터를 결합하는 단일 페더레이션 GraphQL 엔드포인트가 있을 수 있습니다.
* PWA Studio 애플리케이션은 상향 버전의 프록시 없이 AEM GraphQL 엔드포인트 URL을 직접 사용할 수 있습니다. 프록시를 다른 레이어(예: CDN)로 이동할 수도 있습니다.
* 가장 적합한 접근 방식은 최종 사용자에게 PWA Studio 애플리케이션을 제공하는 방식에 따라 크게 달라집니다.

이 확장은 두 가지 예와 함께 제공됩니다.

### 블로그 {#blog}

일부 콘텐츠 조각 모델을 기반으로 블로그 게시물을 표시합니다. 또한 AEM GraphQL 종단점과 함께 작동하도록 Apollo 클라이언트를 구성하는 방법 및 PWA Studio에서 탐색 구성 요소를 확장하는 방법에 대한 예가 포함되어 있습니다. 다음을 참조하십시오 [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension) 을 참조하십시오.

### PDP 보강 {#pdp-enrichment}

마케터는 콘텐츠 조각으로 관리되는 추가 콘텐츠로 PDP를 쉽게 보강할 수 있습니다. 다음을 참조하십시오 [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension) 을 참조하십시오.
