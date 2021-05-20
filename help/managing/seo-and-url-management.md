---
title: SEO 및 URL 관리 우수 사례
seo-title: SEO 및 URL 관리 우수 사례
description: AEM 구현에서 이를 수행하기 위한 SEO 우수 사례 및 권장 사항에 대해 알아봅니다.
seo-description: AEM 구현에서 이를 수행하기 위한 SEO 우수 사례 및 권장 사항에 대해 알아봅니다.
uuid: 943e76c4-bd88-4b52-bb43-db375eb89d23
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
discoiquuid: 7c8f2cec-870b-41a8-8d98-70e29b495587
docset: aem65
exl-id: b138f6d1-0870-4071-b96e-4a759ad9a76e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3119'
ht-degree: 98%

---

# SEO 및 URL 관리 우수 사례{#seo-and-url-management-best-practices}

SEO(검색 엔진 최적화)는 많은 마케터의 주요 관심사가 되었습니다. 따라서 많은 AEM 프로젝트에서 SEO 문제를 해결해야 합니다.

이 문서에서는 먼저 AEM 구현에서 이를 잘 수행하기 위한 [SEO 우수 사례](#seo-best-practices) 및 권장 사항에 대해 설명합니다. 그런 다음 첫 번째 섹션에서 제기한 보다 [복잡한 구현 절차](#aem-configurations) 중 일부를 자세히 살펴봅니다.

## SEO 우수 사례 {#seo-best-practices}

이 섹션에서는 일반적인 SEO 우수 사례에 대해 설명합니다.

### URL {#urls}

URL과 관련하여 일반적으로 받아들여지는 우수 사례가 있습니다.

AEM 프로젝트에서 URL을 평가할 때에는 다음 사항을 자문해 보십시오.

&quot;사용자가 이 URL은 보고 페이지에 있는 컨텐츠는 보지 못하는 경우 이 페이지의 내용을 설명할 수 있습니까?&quot;

답변이 예라면 검색 엔진에서 URL이 제대로 작동할 가능성이 높습니다.

다음은 SEO용 URL을 구성하는 방법에 대한 일반적인 팁입니다.

* 하이픈을 사용하여 단어를 구분합니다.

   * 하이픈(-)을 구분 기호로 사용하여 페이지의 이름을 지정합니다.
   * 카멜 표기법, 밑줄 및 공백을 사용하면 안 됩니다.

* 가능하면 쿼리 매개 변수를 사용하지 않습니다. 필요할 경우 두 개 이하로 제한합니다.

   * 사용 가능한 경우 디렉토리 구조를 사용하여 정보 아키텍처를 나타냅니다.
   * 디렉토리 구조가 선택 사항이 아닌 경우 쿼리 문자열보다는 URL에서 Sling 선택기를 사용합니다. Sling 선택기를 사용하면 SEO 값이 제공될 뿐 아니라 디스패처의 페이지를 캐시할 수 있습니다.

* URL은 사람이 읽기 쉬울수록 더 좋습니다. 따라서 URL에 키워드가 있으면 더욱 효과적입니다.

   * 페이지에서 선택기를 사용하는 경우 의미론적 가치를 제공하는 선택기가 선호됩니다.
   * 사람이 읽을 수 없는 URL은 검색 엔진도 읽을 수 없습니다.
   * 예:
      `mybrand.com/products/product-detail.product-category.product-name.html`이 보다 선호됩니다. 
`mybrand.com/products/product-detail.1234.html`

* 검색 엔진이 사이트의 SEO 값을 조각화하여 하위 도메인을 다른 엔티티로 취급하므로 가능한 경우에는 항상 하위 도메인을 사용하면 안 됩니다.

   * 대신 첫 번째 수준 하위 경로를 사용합니다. 예를 들어, `es.mybrand.com/home.html` 대신 `www.mybrand.com/es/home.html`을 사용합니다.

   * 이 지침에 따라 컨텐츠가 표시되는 방식과 일치하도록 컨텐츠 계층 구조를 계획합니다.

* URL의 키워드 효과는 URL의 길이와 키워드 위치가 증가하면 감소합니다. 즉, 짧을수록 좋습니다.

   * AEM에서 제공하는 URL 단축 기법 및 기능을 사용하여 불필요한 URL 조각을 제거합니다.
   * 예를 들어 `mybrand.com/en/myPage.html`이 `mybrand.com/content/my-brand/en/myPage.html`보다 좋습니다.

* 정식 URL을 사용합니다.

   * 어떤 URL이 다른 경로나 다른 매개 변수 또는 선택기에서 제공될 수 있는 경우 페이지에서 `rel=canonical` 태그를 사용해야 합니다.

   * 이 태그는 AEM 템플릿의 코드에 포함할 수 있습니다.

* 가능하면 페이지 제목과 URL을 일치시킵니다.

   * 컨텐츠 작성자는 이 방법을 따라야 합니다.

* URL 요청에서 대소문자를 구분하지 않습니다.

   * 모든 인바운드 요청을 소문자로 다시 작성하도록 디스패처를 구성합니다.
   * 모든 페이지를 소문자를 사용하여 만들도록 컨텐츠 작성자를 교육합니다.

* 각 페이지가 하나의 프로토콜에서만 제공되어야 합니다.

   * 경우에 따라 사이트는 사용자가 체크아웃이나 로그인 양식 등이 있는 페이지에 도달하기 전까지 `http`를 통해 제공되고, 이러한 페이지에 도달하면 `https`로 전환됩니다. 이 페이지에서 연결할 때 사용자가 `http` 페이지로 돌아가서 `https`를 통해 해당 페이지에 액세스할 수 있으면 검색 엔진은 해당 페이지를 두 개의 개별 페이지로 추적하게 됩니다.

   * 현재 Google에서는 `http` 페이지보다 `https` 페이지를 선호합니다. 이러한 이유로 `https`를 통해 전체 사이트를 제공하는 것이 대개 더 편리합니다.

### 서버 구성 {#server-configuration}

서버 구성 측면에서 다음 절차를 수행하여 올바른 컨텐츠만 크롤링되도록 할 수 있습니다.

* 인덱싱해서는 안 되는 컨텐츠의 크롤링을 차단하려면 `robots.txt` 파일을 사용하십시오.

   * 테스트 환경의 **모든** 크롤링을 차단하십시오.

* 업데이트된 URL로 새 사이트를 시작할 때 기존 SEO 등급을 잃지 않도록 301 리디렉션을 구현하십시오.
* 귀하의 사이트에 대한 favicon을 포함하십시오.
* 검색 엔진이 컨텐츠를 더 쉽게 크롤링할 수 있도록 XML 사이트 맵을 구현하십시오. 반드시 모바일 및/또는 응답형 사이트를 위한 모바일 사이트 맵을 포함하십시오.

## AEM 구성 {#aem-configurations}

이 섹션에서는 다음의 SEO 권장 사항을 따르도록 AEM을 구성하는 데 필요한 구현 절차에 대해 설명합니다.

### Sling 선택기 사용 {#using-sling-selectors}

이전에는 엔터프라이즈 웹 애플리케이션을 만들 때 쿼리 매개 변수를 사용하는 것이 일반적으로 인정받는 방법이었습니다.

최근 몇 년간의 경향은 URL을 더 읽기 쉽게 만들기 위해 이러한 매개 변수를 제거하는 것이었습니다. 많은 플랫폼에서 이렇게 하려면 웹 서버나 CDN(Content Delivery Network)에서 리디렉션을 구현해야 하지만 Sling은 이 작업을 간단하게 해줍니다. Sling 선택기는

* URL 가독성을 개선합니다.
* 페이지를 디스패처에서 캐싱할 수 있도록 하고 종종 보안을 개선합니다.
* 컨텐츠를 검색하는 일반 서블릿을 보유하는 대신 컨텐츠 주소를 바로 지정할 수 있도록 해줍니다. 따라서 저장소에 적용하는 ACL과 디스패처에 적용하는 필터의 이점을 이용할 수 있습니다.

#### 서블릿에 선택기 사용 {#using-selectors-for-servlets}

AEM에서는 서블릿을 작성할 때 두 가지 옵션을 제공합니다.

* **bin** 서블릿
* **Sling** 서블릿

다음 예는 이러한 패턴을 따르는 서블릿을 등록하는 방법과 Sling 서블릿을 사용하여 얻게 되는 혜택을 보여 줍니다.

#### Bin 서블릿(한 수준 아래로){#bin-servlets-one-level-down}

**Bin** 서블릿은 많은 개발자들이 J2EE 프로그래밍에서 익숙한 패턴을 따릅니다. 서블릿은 특정 경로에 등록되는데 AEM에서는 일반적으로 `/bin` 아래에 있으며 쿼리 문자열에서 필요한 요청 매개 변수를 추출하게 됩니다.

이 유형의 서블릿에 대한 SCR 주석은 다음과 같은 모습입니다.

```
@SlingServlet(paths = "/bin/myApp/myServlet", extensions = "json", methods = "GET")
```

그러면 `doGet` 메서드에 포함된 `SlingHttpServletRequest` 개체를 통해 쿼리 문자열에서 매개 변수를 추출합니다. 예를 들면 다음과 같습니다.

```
String myParam = req.getParameter("myParam");
```

사용된 결과 URL은 다음과 같은 모습입니다.

`https://www.mydomain.com/bin/myApp/myServlet.json?myParam=myValue`

이 접근 방식에서는 몇 가지 사항을 고려해야 합니다.

* URL 자체는 SEO 값을 잃습니다. URL은 컨텐츠 계층 구조가 아니라 프로그래밍 방식에 따른 경로를 나타내므로 검색 엔진을 포함하여 사이트에 액세스하는 사용자는 URL에서 어떠한 의미 있는 가치도 받지 못합니다.
* URL에 쿼리 매개 변수가 있으면 이는 디스패처가 응답을 캐시할 수 없음을 의미합니다.
* 이 서블릿을 보호하려면 서블릿에 사용자 지정 보안 로직을 구현해야 합니다.
* 디스패처는 `/bin/myApp/myServlet`을 노출하도록 (신중하게) 구성되어야 합니다. 단순히 `/bin`을 노출하면 사이트 방문자에게 공개되어서는 안 되는 특정 서블릿에 대한 액세스가 허용될 수 있습니다.

#### Sling 서블릿(한 수준 아래로){#sling-servlets-one-level-down}

**Sling** 서블릿을 사용하면 반대 방식으로 서블릿을 등록할 수 있습니다. 서블릿 주소를 지정하고 쿼리 매개 변수를 기반으로 서블릿이 렌더링할 컨텐츠를 지정하는 대신 원하는 컨텐츠의 주소를 지정하고 Sling 선택기를 기반으로 컨텐츠를 렌더링해야 하는 서블릿을 지정하십시오.

이 유형의 서블릿에 대한 SCR 주석은 다음과 같은 모습입니다.

```
@SlingServlet(resourceTypes = "myBrand/components/pages/myPageType", selectors = "myRenderer", extensions = "json”, methods=”GET”)
```

이 경우 URL이 주소를 지정하는 리소스(`myPageType` 리소스의 인스턴스)는 서블릿에서 자동으로 액세스할 수 있습니다. 액세스하려면 다음 내용을 호출하십시오.

```
Resource myPage = req.getResource();
```

사용된 결과 URL은 다음과 같은 모습입니다.

`https://www.mydomain.com/content/my-brand/my-page.myRenderer.json`

이 접근 방식의 장점은 다음과 같습니다.

* 사이트 계층 구조 및 페이지 이름에 있는 의미 체계로 얻은 SEO 값을 포함할 수 있습니다.
* 쿼리 매개 변수가 없으므로 디스패처가 응답을 캐시할 수 있습니다. 또한, 페이지가 활성화되어 있으면 주소가 지정된 페이지에 대한 모든 업데이트는 이 캐시를 무효화합니다.
* 사용자가 이 서블릿에 액세스하려고 하면 `/content/my-brand/my-page`에 적용되는 모든 ACL이 적용됩니다.
* 디스패처는 이미 웹 사이트를 제공하는 기능으로서 이 컨텐츠를 제공하도록 구성됩니다. 추가적인 구성은 필요하지 않습니다.

### URL 재작성 {#url-rewriting}

AEM에서 모든 웹 페이지는 `/content/my-brand/my-content` 아래에 저장됩니다. 이 방식은 저장소 데이터 관리 측면에서 유용할 수 있지만 고객이 반드시 이 방식으로 사이트를 보게 할 필요는 없으며, URL을 최대한 짧게 유지하도록 하는 SEO 지침과 이 방식이 충돌할 수도 있습니다. 또한 동일한 AEM 인스턴스와 다른 도메인 이름에서 여러 웹 사이트를 제공 중일 수도 있습니다.

이 섹션에서는 이러한 URL을 보다 읽기 쉽고 SEO에 적절한 방식으로 관리하고 사용자에게 제공하기 위해 AEM에서 사용할 수 있는 옵션들을 검토합니다.

#### 별칭 URL {#vanity-urls}

작성자가 홍보 목적으로 두 번째 위치에서 페이지에 액세스하려는 경우 페이지별로 정의된 AEM의 별칭 URL이 유용할 수 있습니다. 페이지의 별칭 URL을 추가하려면 **사이트** 콘솔에서 해당 페이지로 이동하여 페이지 속성을 편집하십시오. **기본** 탭 하단에 별칭 URL을 추가할 수 있는 섹션이 보입니다. 둘 이상의 URL을 통해 페이지에 액세스할 수 있게 하면 페이지의 SEO 값이 조각화되므로 정식 URL 태그를 페이지에 추가하여 이 문제를 방지해야 합니다.

#### 현지화된 페이지 이름 {#localized-page-names}

번역된 컨텐츠의 사용자에게 현지화된 페이지 이름을 표시하는 것이 좋습니다. 예:

* 스페인어 사용자를 다음 페이지로 이동하게 하는 것보다는
   `www.mydomain.com/es/home.html`

* 다음과 같은 URL을 사용하는 것이 좋습니다.
   `www.mydomain.com/es/casa.html`.

페이지 이름을 현지화하는 데 있어 어려움은 AEM 플랫폼에서 사용할 수 있는 많은 현지화 도구가 지속적인 컨텐츠 동기화를 위해 로케일 간 페이지 이름을 일치시켜야 한다는 것입니다.

`sling:alias` 속성을 사용하면 문제를 해결할 수 있습니다. `sling:alias`를 리소스에 속성으로 추가하여 리소스에 별칭을 허용할 수 있습니다. 앞의 예에서

* JCR의 페이지를 만든 위치:
   `…/es/home`

* 페이지를 만든 후 속성을 추가함:
   `sling:alias` = `casa`

이렇게 하면 다중 사이트 관리 프로그램과 같은 AEM 번역 도구는 다음 두 항목 간에 관계를 계속 유지할 수 있습니다.

* `/en/home`

* `/es/home`

또한 최종 사용자는 모국어로 페이지 이름과 상호 작용할 수도 있습니다.

>[!NOTE]
>
>`sling:alias` 속성은 [ 페이지 속성을 편집할 때 별칭 속성](/help/sites-authoring/editing-page-properties.md#advanced)을 사용하여 설정할 수 있습니다.

#### /etc/map {#etc-map}

표준 AEM 설치에서

* OSGi 구성
   **Apache Sling Resource Resolver Factory**
( 
`org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl`)

* 속성
   **매핑 위치**(`resource.resolver.map.location`)의

* 기본값은 `/etc/map`입니다.

이 위치에 매핑 정의를 추가하여 인바운드 요청을 매핑하거나 AEM의 페이지에서 URL을 다시 작성하거나 두 작업을 모두 수행할 수 있습니다.

새 매핑을 생성하려면 `/http` 또는 `/https`를 사용하여 이 위치에서 새 `sling:Mapping` 노드를 만드십시오. AEM은 이 노드에 설정된 `sling:match` 및 `sling:internalRedirect` 속성을 기반으로 일치하는 URL의 모든 트래픽을 `internalRedirect` 속성에 지정된 값에 리디렉션합니다.

이것이 공식 AEM 및 Sling 설명서에 정리된 접근 방법인데, 이 구현에서 제공하는 정규식 지원은 `SlingResourceResolver`를 바로 사용함으로써 사용 가능한 옵션과 비교할 때 범위가 제한됩니다. 또한 이 방식으로 매핑을 구현하면 디스패처 캐시 무효화에 문제가 발생할 수 있습니다.

이 문제가 발생하는 방법의 예는 다음과 같습니다.

1. 사용자가 웹 사이트를 방문하여 `https://www.mydomain.com/my-page.html`을 요청합니다.
1. 디스패처가 이 요청을 게시 서버에 전달합니다.
1. `/etc/map`을 사용하여 게시 서버가 이 요청을 `/content/my-brand/my-page`에 확인하고 페이지를 렌더링합니다.

1. 디스패처가 `/my-page.html`에서 응답을 캐시하고 응답을 사용자에게 반환합니다.
1. 컨텐츠 작성자가 이 페이지를 변경하고 활성화합니다.
1. 디스패처 초기화 에이전트가 `/content/my-brand/my-page`**에 대한 무효화 요청을 보냅니다.** 디스패처에는 이 경로에 캐시된 페이지가 없으므로 이전 컨텐츠는 캐시된 상태로 유지되며 시기적으로 적절하지 않게 됩니다.

캐시 무효화를 위해 짧은 URL을 긴 URL에 매핑하는 사용자 지정 발송-초기화 규칙을 구성하는 방법이 있습니다.

그러나 이를 관리하는 간단한 방법도 있습니다.

1. **SlingResourceResolver 규칙**

   웹 콘솔(예: localhost:4502/system/console/configMgr)을 사용하여 Sling Resource Resolver를 구성할 수 있습니다.

   * **Apache Sling Resource Resolver Factory**

      `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)`.
   URL을 정규식으로 단축하는 데 필요한 매핑을 빌드한 후 빌드에 포함된 OsgiConfignode인 `config.publish`에서 이러한 구성을 정의하는 것이 좋습니다.

   매핑을 `/etc/map`에서 정의하지 않고 속성 **URL 매핑**(`resource.resolver.mapping`)에 바로 지정할 수 있습니다.

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   이 간단한 예에서는 `/content/my-brand/`가 있는 모든 URL의 시작 부분에서 이 문자열을 제거합니다.

   이 작업으로 URL은 다음과 같이 변환됩니다.

   * 변환 전: `/content/my-brand/my-page.html`
   * 변환 후: `/my-page.html`

   이것은 URL을 가능한 짧게 유지하는 것이 좋다는 지침을 따릅니다.

1. **페이지에서 URL 출력 매핑**

   Apache Sling Resource Resolver에서 매핑을 정의한 후 구성 요소에서 이 매핑을 사용하여 페이지에서 출력하는 URL이 짧고 깔끔하게 해야 합니다. `ResourceResolver`의 매핑 기능을 사용하여 그렇게 할 수 있습니다.

   예를 들어 현재 페이지의 하위 페이지를 나열하는 사용자 지정 탐색 구성 요소를 구현하는 경우 다음과 같은 매핑 메서드를 사용할 수 있습니다.

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### Apache HTTP 서버 mod_rewrite {#apache-http-server-mod-rewrite}

지금까지는 구성 요소의 논리와 함께 매핑을 구현하여 URL을 Adobe 페이지에 출력할 때 이 매핑을 사용했습니다.

퍼즐의 마지막 조각은 이 단축된 URL을 디스패처에 들어올 때 처리하는 것입니다. `mod_rewrite`은 여기에서 작동합니다. `mod_rewrite`를 사용할 때 가장 큰 이점은 URL이 디스패처 모듈로 전송되기 *전에* 긴 형식으로 다시 매핑된다는 것입니다. 이는 디스패처가 게시 서버에서 긴 URL을 요청하고 적절하게 캐시할 것임을 의미합니다. 따라서 게시 서버에서 들어오는 모든 디스패처 초기화 요청은 이 컨텐츠를 무효화할 수 있습니다.

이러한 규칙을 구현하기 위해 Apache HTTP Server 구성에서 가상 호스트 아래에 `RewriteRule` 요소를 추가할 수 있습니다. 이전 예에서 단축된 URL을 확장하려는 경우 다음과 같은 규칙을 구현할 수 있습니다.

```
<VirtualHost *:80>
  ServerName www.mydomain.com
  RewriteEngine on
  RewriteRule ^/(.*)$ /content/my-brand/$1 [PT,L]
  …
</VirtualHost>
```

### 정식 URL 태그 {#canonical-url-tags}

정식 URL 태그는 컨텐츠를 색인화하는 동안 검색 엔진이 페이지를 처리하는 방식을 명확히 하기 위해 HTML 문서의 헤드에 배치된 링크 태그입니다. 이 태그가 제공하는 이점은 (다양한 버전의)페이지가 페이지의 URL에 차이가 있더라도 동일하게 색인화되도록 하는 것입니다.

예를 들어 사이트에서 프린터에 적절한 버전의 페이지를 제공하는 경우 검색 엔진은 이 페이지를 일반 버전의 페이지와 별도로 색인화할 가능성이 있습니다. 정식 태그는 검색 엔진에 이 페이지들이 동일하다고 알려줍니다.

예:

* https://www.mydomain.com/my-brand/my-page.html
* https://www.mydomain.com/my-brand/my-page.print.html

두 페이지 모두 페이지 헤드에 다음 태그를 적용합니다.

```xml
<link rel=”canonical” href=”my-brand/my-page.html”/>
```

`href`는 상대적이거나 절대적일 수 있습니다. 페이지 마크업에 코드가 포함되어야 페이지의 정식 URL을 확인하고 이 태그를 출력할 수 있습니다.

### 대소문자 구분에 대한 디스패처 구성 {#configuring-the-dispatcher-for-case-insensitivity}

가장 좋은 방법은 모든 페이지를 소문자를 사용하여 제공하는 것입니다. 그러나 사용자가 URL에서 대문자를 사용하여 웹 사이트에 액세스할 때 404 오류가 표시되는 것은 원하지 않습니다. 그렇다면 Apache HTTP Server 구성에 재작성 규칙을 추가하여 들어오는 모든 URL을 소문자로 매핑하는 것이 좋습니다. 또한 컨텐츠 작성자는 소문자로 페이지를 만들도록 교육해야 합니다.

모든 인바운드 트래픽을 소문자로 강제하도록 Apache를 구성하려면 다음 내용을 `vhost` 구성에 추가하십시오.

```xml
RewriteEngine On
RewriteMap lowercase int:tolower
```

또한 `htaccess` 파일의 맨 위에 다음 내용을 추가하십시오.

```xml
RewriteCond $1 [A-Z]
RewriteRule ^(.*)$ /${lowercase:$1} [R=301,L]
```

### 개발 환경을 보호하기 위한 robots.txt 구현 {#implementing-robots-txt-to-protect-development-environments}

검색 엔진은 사이트를 크롤링하기 전에 사이트 루트에 `robots.txt` 파일이 있는지 *확인해야* 합니다. Google, Yahoo 또는 Bing과 같은 주요 검색 엔진은 모두 이 점을 준수하지만 일부 외국 검색 엔진은 이를 준수하지 않기 때문에 여기서 강조합니다.

전체 사이트에 대한 액세스를 차단하는 가장 간단한 방법은 다음 컨텐츠로 사이트 루트에 `robots.txt`라는 파일을 배치하는 것입니다.

```xml
User-agent: *
Disallow: /
```

또는 실제 환경에서는 색인화하지 않을 특정 경로를 허용하지 않도록 선택할 수 있습니다.

`robots.txt` 파일을 사이트 루트에 배치할 때 주의해야 할 사항은 디스패처 초기화 요청이 이 파일을 지우고 URL 매핑이 Apache HTTP Server 구성에 정의된 대로 `DOCROOT`와 다른 위치에 사이트 루트를 배치할 수 있다는 것입니다. 이러한 이유로 이 파일을 사이트 루트의 작성자 인스턴스에 배치하고 게시 인스턴스에 복제하는 것이 일반적입니다.

### AEM에서 XML 사이트 맵 작성 {#building-an-xml-sitemap-on-aem}

크롤러는 웹 사이트의 구조를 더 잘 파악하기 위해 XML 사이트 맵을 사용합니다. 사이트 맵을 제공하는 것이 SEO 등급을 개선한다는 보장은 없지만, 이것은 합의된 우수 사례입니다. 사이트 맵으로 사용할 XML 파일은 웹 서버에서 수동으로 유지 관리할 수 있지만, 사이트 맵은 프로그래밍 방식으로 생성하는 것이 좋습니다. 이렇게 하면 작성자가 새 컨텐츠를 만들 때 사이트 맵이 변경 사항을 자동으로 반영하게 됩니다.

사이트 맵을 프로그래밍 방식으로 생성하려면 `sitemap.xml` 호출을 수신하는 Sling 서블릿을 등록하십시오. 그러면 서블릿은 서블릿 API를 통해 제공된 리소스를 사용하여 현재 페이지와 그 하위 페이지를 보고 XML을 출력할 수 있습니다. 그러면 XML이 디스패처에서 캐시됩니다. 이 위치는 `robots.txt` 파일의 사이트 맵 속성에서 참조되어야 합니다. 또한 새 페이지가 활성화될 때마다 이 파일을 초기화하도록 사용자 지정 초기화 규칙을 구현해야 합니다.

>[!NOTE]
>
>Sling 서블릿을 등록하여 확장자가 `sitemap`인 선택기 `xml`을 수신 대기할 수 있습니다. 이렇게 하면 다음과 같이 끝나는 URL이 요청될 때마다 서블릿이 요청을 처리하게 됩니다.
>    `/<path-to>/page.sitemap.xml`
그러면 요청에서 요청된 리소스를 가져와 JCR API를 사용하여 컨텐츠 트리의 해당 지점에서 사이트 맵을 생성할 수 있습니다.
이같은 접근 방식의 이점은 동일한 인스턴스에서 여러 사이트를 제공하는 경우입니다. `/content/siteA.sitemap.xml`에 대한 요청은 `siteA`에 대한 사이트 맵을 생성하는 반면 `/content/siteB.sitemap.xml`에 대한 요청은 추가적인 코드를 작성하지 않아도 `siteB`에 대한 사이트 맵을 생성합니다.

### 레거시 URL에 대해 301 리디렉션 생성 {#creating-redirects-for-legacy-urls}

새로운 구조로 사이트를 시작할 때 Apache HTTP Server에서 301 리디렉션을 구현하고 테스트하는 것은 다음 두 가지 이유로 중요합니다.

* 시간이 지남에 따라 레거시 URL이 SEO 값을 높였습니다. 리디렉션을 구현하면 검색 엔진이 이 값을 새 URL에 적용할 수 있습니다.
* 사이트 사용자가 이 페이지에 책갈피를 생성했을 수 있습니다. 리디렉션을 구현하면 사용자가 이전 사이트에서 방문하려는 위치와 가장 일치하는 새 사이트의 페이지로 사용자를 보낼 수 있습니다.

301 리디렉션 구현에 대한 지침과 리디렉션이 예상대로 작동하는지 테스트하는 도구에 대해서는 다음에 이어지는 추가 리소스 섹션을 확인하십시오.

## 추가 리소스 {#additional-resources}

자세한 내용은 다음 추가 자료를 참조하십시오.

* [리소스 매핑](/help/sites-deploying/resource-mapping.md)
* [https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url](https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url)
* [https://moz.com/blog/15-seo-best-practices-for-structuring-urls](https://moz.com/blog/15-seo-best-practices-for-structuring-urls)
* [https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/](https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/)
* [https://sling.apache.org/documentation/the-sling-engine/servlets.html](https://sling.apache.org/documentation/the-sling-engine/servlets.html)
* [https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
* [https://httpd.apache.org/docs/current/mod/mod_rewrite.html](https://httpd.apache.org/docs/current/mod/mod_rewrite.html)
* [https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps](https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps)
* [https://www.robotstxt.org/robotstxt.html](https://www.robotstxt.org/robotstxt.html)
* [https://www.internetmarketingninjas.com/blog/search-engine-optimization/301-redirects/](https://www.internetmarketingninjas.com/blog/search-engine-optimization/301-redirects/)
* [https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester)
* [https://adobe-consulting-services.github.io/](https://adobe-consulting-services.github.io/)
