---
title: PWA Studio용 AEM 확장 시작하기
description: PWA Studio을 사용하여 AEM 헤드리스 콘텐츠 및 상거래 프로젝트를 배포하는 방법을 알아봅니다.
topics: Commerce
feature: Commerce Integration Framework
thumbnail: 37843.jpg
exl-id: de7b8f05-b6b7-4105-84a5-940c16ebf2b4
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---

# PWA Studio용 AEM 확장 시작하기 {#getting-started-pwa}

기본적으로 PWA Studio은 GraphQL을 통해 Adobe Commerce과 원활하게 통합되며 혁신적이고 매력적인 상점 및 기타 디지털 경험을 생성하는 무제한 옵션을 제공합니다.

컨텐츠 조각은 GraphQL을 다양한 형식(예: JSON, Markdown)에서 API로 사용하고 독립적으로 렌더링되는 방식으로 헤드리스 방식으로 사용할 수 있도록 미리 정의된 구조를 갖는 컨텐츠 조각입니다. 컨텐츠 조각에는 GraphQL에서 필요한 모든 데이터 유형과 필드가 포함되어 있으므로 애플리케이션에서 사용 가능한 항목만 요청하고 예상대로 수신됩니다. 구조화 방식에 따라 유연하게 제공되므로 여러 위치 및 여러 채널에서 사용할 수 있습니다.

Adobe Experience Manager 내의 컨텐츠 조각 모델 편집기를 사용하면 필요한 구조를 쉽게 디자인할 수 있습니다. Adobe Experience Manager 컨텐츠 조각(또는 기타 데이터)과 PWA Studio 애플리케이션을 통합해야 하는 주요 문제는 여러 GraphQL 종단점에서 데이터를 가져오는 것입니다. 이는 PWA Studio이 단일 Adobe Commerce GraphQL 종단점에서 작동하기 때문입니다.

## 아키텍처 {#architecture}

![PWA 헤드리스 아키텍처](/help/commerce/cif/assets/pwa-studio/PWA-Studio_Architecture.png)

## 설정 PWA Studio {#setup-pwa}

Adobe Commerce 팔로우 [PWA Studio 설명서](https://developer.adobe.com/commerce/pwa-studio/tutorials/) PWA Studio 앱을 설정하려면 다음을 수행하십시오.

PWA Studio을 AEM의 GraphQL 종단점과 연결하려면 [PWA Studio용 AEM 확장](https://github.com/adobe/aem-pwa-studio-extensions).

1. 리포지토리 체크 아웃

1. PWA Studio 애플리케이션에서 확장을 개발 종속성으로 추가합니다.

   ```javascript
   yarn add --dev file:{path-to-extension}/extension
   ```

1. PWA Studio 애플리케이션에 Apollo Link 래퍼를 추가합니다. pwa-root/src/index.js에서 다음 사항을 변경합니다.

   ```javascript
     import { linkWrapper } from '@adobe/pwa-studio-aem-cfm-blog-extension';
   
   // ...
   
   <Adapter apiBase={apiBase} apollo={{ link: linkWrapper(apolloLink) }} store={store}>
   ```

   Apollo Client 사용자 지정에 대한 자세한 내용은 [linkWrapper.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/linkWrapper.js).

1. 탐색 구성 요소를 블로그 항목으로 확장하려면 pwa-root/local-intercept.js에 다음 옵션을 추가합니다.

   ```javascript
   const addBlogToNavigation = require('@adobe/pwa-studio-aem-cfm-blog-extension/src/addBlogToNavigation');
   
   function localIntercept(targets) {
       addBlogToNavigation(targets);
   }    
   ```

   에서 탐색 구성 요소의 사용자 지정에 대한 자세한 내용을 찾을 수 있습니다 [addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js) 그리고 [확장성 프레임워크](https://developer.adobe.com/commerce/pwa-studio/guides/general-concepts/extensibility/) PWA Studio 설명서.

1. Apollo 클라이언트는 AEM GraphQL 종단점을 <https://pwa-studio/endpoint.js>. 끝점을 이 위치에 매핑하려면 PWA Studio 애플리케이션의 위쪽 구성을 사용자 지정해야 합니다. a. AEM_CFM_GRAPHQL 변수를 pwa-root/.env에 추가하고 AEM 컨텐츠 조각 GraphQL 엔드포인트를 가리키도록 조정합니다.

   예: AEM_CFM_GRAPHQL=<http://localhost:4503/content/graphql/global>

   나. 프록시 확인자를 위쪽 구성에 추가합니다. 다음은 샘플 상향 구성입니다.

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

AEM 컨텐츠 조각 설명서에 따라 AEM 프로젝트에 대한 GraphQL 엔드포인트를 설정합니다. 또한 AEM 프로젝트에서 다음 구성을 추가하여 PWA Studio 응용 프로그램이 GraphQL 종단점에 액세스할 수 있도록 합니다.

* Adobe Granite CORS(원본 간 리소스 공유 정책)(com.adobe.granite.cors.impl.CORSPolicyImpl)

   할당된 원본 속성을 PWA 응용 프로그램의 전체 호스트 이름으로 설정합니다.

   예:  <https://pwa-studio-test-vflyn.local.pwadev:9366>

* Apache Sling Referrer Filter(org.apache.sling.security.impl.ReferrerFilter.cfg.json)

   allow.hosts 속성을 PWA 응용 프로그램의 호스트 이름으로 설정합니다.

   예: pwa-studio-test-vflyn.local.pwadev

두 구성에 대한 전체 예는 다음과 같습니다. <https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config>.

GraphQL 엔드포인트를 보여주기 위해 컨텐츠 패키지를 통해 일부 샘플 컨텐츠 조각 모델 및 데이터를 준비했습니다. 이러한 구성 요소는 PWA Studio 확장과 함께 제공된 React 구성 요소와 잘 작동합니다.

## 사용 방법 {#how-to-use}

이 확장은 AEM과 PWA Studio 애플리케이션을 연결하여 GraphQL을 통해 컨텐츠를 검색하고 렌더링하는 방법의 예제 구현으로 간주됩니다.

사용 사례에 따라 고유한 사용자 지정 컨텐츠 조각 모델을 만들어 사용자 지정 GraphQL 스키마를 생성할 수 있으며 이러한 스키마는 사용자 고유의 React 구성 요소에서 사용할 수 있습니다.

프로덕션 설정은 여러 측면에서 다를 수 있습니다.

* Apollo 클라이언트를 사용자 지정하는 대신 AEM 및 Adobe Commerce GraphQL 데이터를 결합하는 단일 Federated GraphQL 엔드포인트가 있을 수 있습니다.
* PWA Studio 응용 프로그램에서 상향 프록시가 없는 AEM GrapHQL 끝점 URL을 직접 사용할 수 있습니다. 프록시를 다른 레이어(예: CDN)로 이동할 수도 있습니다.
* 또한 최종 사용자에게 PWA Studio 애플리케이션을 제공하는 방법에 따라 어떤 접근 방식이 가장 적합한지도 크게 달라집니다.

이 확장은 두 가지 예와 함께 제공됩니다.

### 블로그 {#blog}

일부 컨텐츠 조각 모델을 기반으로 블로그 게시물을 표시합니다. 또한 AEM GraphQL 종단점에서 작동하도록 Apollo 클라이언트를 구성하는 방법 및 PWA Studio에서 탐색 구성 요소를 확장하는 방법에 대한 예를 포함합니다. 자세한 내용은 [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension) 자세한 내용

### PDP 강화 {#pdp-enrichment}

컨텐츠 조각으로 관리되는 추가 컨텐츠로 PDP를 쉽게 보강할 수 있습니다.  자세한 내용은 [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension) 자세한 내용
