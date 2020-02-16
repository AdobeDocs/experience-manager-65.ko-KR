---
title: SEO 및 URL 관리 우수 사례
seo-title: SEO 및 URL 관리 우수 사례
description: AEM 구현에서 이를 달성하기 위한 SEO 우수 사례 및 권장 사항에 대해 알아봅니다.
seo-description: AEM 구현에서 이를 달성하기 위한 SEO 우수 사례 및 권장 사항에 대해 알아봅니다.
uuid: 943e76c4-bd88-4b52-bb43-db375eb89d23
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
discoiquuid: 7c8f2cec-870b-41a8-8d98-70e29b495587
docset: aem65
translation-type: tm+mt
source-git-commit: c623724df8d849f4cc01f5dc134c775dc24dafc7

---


# SEO 및 URL 관리 우수 사례{#seo-and-url-management-best-practices}

많은 마케터에게 SEO 파섹 따라서 SEO 문제는 많은 AEM 프로젝트에서 해결해야 합니다.

이 문서에서는 먼저 AEM [구현에서 이러한 사항을 달성하기 위한 일부 SEO 우수 사례](#seo-best-practices) 및 권장 사항에 대해 설명합니다. 그런 다음 이 문서에서는 첫 번째 섹션에서 언급한 보다 [복잡한 구현 단계](#aem-configurations) 중 일부를 자세히 살펴봅니다.

## SEO 우수 사례 {#seo-best-practices}

이 섹션에서는 일반적인 SEO 우수 사례에 대해 설명합니다.

### URL {#urls}

URL에 대한 일반적인 우수 사례가 있습니다.

AEM 프로젝트에서 URL을 평가할 때 다음 사항을 스스로에게 물어보십시오.

&quot;사용자가 이 URL을 보고 페이지에 있는 컨텐츠가 없는 경우 이 페이지가 무엇인지 설명할 수 있습니까?&quot;

답변이 예인 경우 검색 엔진에서 URL이 제대로 작동할 가능성이 높습니다.

다음은 SEO용 URL을 구성하는 방법에 대한 일반적인 팁입니다.

* 하이픈을 사용하여 단어를 구분합니다.

   * 하이픈(-)을 구분 기호로 사용하여 페이지의 이름을 지정합니다.
   * 낙타의 경우, 밑줄 및 공백을 사용하지 마십시오.

* 가능하면 쿼리 매개 변수를 사용하지 마십시오. 필요한 경우 두 개 이하로 제한합니다.

   * 사용 가능한 경우 디렉토리 구조를 사용하여 정보 아키텍처를 지정합니다.
   * 디렉토리 구조가 옵션이 아닌 경우 쿼리 문자열이 아닌 URL에서 Sling 선택기를 사용하십시오. 사용자가 제공하는 SEO 값 외에도 슬링 선택기는 디스패처에 대해 페이지를 캐시하도록 합니다.

* 사람이 읽을 수 있는 URL이 많을수록 좋습니다.url에 키워드가 있으면 값이 증가합니다.

   * 페이지에서 선택기를 사용하는 경우 의미 체계 값을 제공하는 선택기를 선호합니다.
   * 사람이 URL을 읽을 수 없는 경우 검색 엔진도 읽을 수 없습니다.
   * 예:
      `mybrand.com/products/product-detail.product-category.product-name.html`
는 `mybrand.com/products/product-detail.1234.html`

* 검색 엔진이 사이트의 SEO 값을 세분화하므로 가능한 한 하위 도메인을 피하십시오.

   * 대신 첫 번째 수준 하위 경로를 사용하십시오. 예를 들어, 대신 를 `es.mybrand.com/home.html`사용합니다 `www.mybrand.com/es/home.html`.

   * 이 지침에 따라 컨텐츠가 표시되는 방식과 일치하도록 콘텐츠 계층 구조를 계획하십시오.

* URL의 키워드 효과는 URL의 길이와 키워드 위치가 증가하면 감소합니다. 짧을 수록 좋다.

   * AEM에서 제공하는 URL 단축 기법 및 기능을 사용하여 불필요한 URL 조각을 제거합니다.
   * 예를 들어, 를 `mybrand.com/en/myPage.html` 사용하는 것이 좋습니다 `mybrand.com/content/my-brand/en/myPage.html`.

* 표준 URL 사용

   * 다른 경로나 다른 매개 변수 또는 선택기에서 URL을 제공할 수 있는 경우 페이지에서 `rel=canonical` 태그를 사용해야 합니다.

   * AEM 템플릿의 코드에 포함할 수 있습니다.

* 가능하면 페이지 제목과 URL을 일치시킵니다.

   * 컨텐츠 작성자는 이 방법을 따라야 합니다.

* URL 요청에서 지원 사례 알림

   * 모든 인바운드 요청을 소문자로 다시 작성하도록 디스패처를 구성합니다.
   * 컨텐츠 작성자가 소문자로 모든 페이지를 만들도록 교육합니다.

* 각 페이지가 하나의 프로토콜에서만 제공되는지 확인합니다.

   * 때때로 사용자가 체크아웃이나 로그인 양식과 같은 페이지가 있는 페이지에 도달할 `http` 때까지 사이트가 `https`전달됩니다. 이 페이지에서 연결할 때 사용자가 `http` 페이지로 돌아가서 이 페이지에 액세스할 수 `https`있으면 검색 엔진에서 이 두 개의 개별 페이지로 추적합니다.

   * 현재 Google은 `https` 페이지보다 페이지를 선호합니다 `http` . 이러한 이유로 전체 사이트를 보다 손쉽게 제공할 수 `https`있습니다.

### 서버 구성 {#server-configuration}

서버 구성 측면에서 다음 단계를 수행하여 올바른 컨텐츠만 크롤링되도록 할 수 있습니다.

* 인덱싱할 수 없는 모든 컨텐츠의 크롤링을 차단하려면 `robots.txt` 파일을 사용합니다.

   * 테스트 환경에서 **모든** 크롤링 차단

* 업데이트된 URL을 사용하여 새 사이트를 시작할 때 301 리디렉션을 구현하여 기존 SEO 등급이 손실되지 않도록 합니다.
* 사이트에 파비콘 포함
* XML 사이트 맵을 구현하여 검색 엔진이 보다 손쉽게 컨텐츠를 크롤할 수 있도록 합니다. 모바일 및/또는 반응형 사이트용 모바일 사이트 맵을 포함해야 합니다.

## AEM Configurations {#aem-configurations}

이 섹션에서는 이러한 SEO 권장 사항을 따르도록 AEM을 구성하는 데 필요한 구현 단계에 대해 설명합니다.

### Sling 선택기 사용 {#using-sling-selectors}

이전에는, 쿼리 매개 변수를 사용하는 것이 엔터프라이즈 웹 애플리케이션을 구축할 때 일반적으로 허용되는 방식이었습니다.

최근 몇 년 동안 URL을 보다 읽기 쉽게 만들기 위해 이러한 URL을 제거하게 되었습니다. 많은 플랫폼에서 이 작업은 웹 서버 또는 CDN(Content Delivery Network)에서 리디렉션을 구현해야 하지만 Sling은 이를 간단합니다. Sling 선택기:

* URL 가독성 향상
* 페이지를 디스패처에 캐싱할 수 있으며 보안을 향상시킬 수 있습니다.
* 컨텐츠를 검색하는 일반 서블릿을 보유하는 대신 컨텐츠를 직접 처리할 수 있습니다. This grants you the benefit of ACL that you apply to your repository and filters that you apply on the dispatcher.

#### 서블릿에 선택기 사용 {#using-selectors-for-servlets}

AEM에서는 서비스를 작성할 때 두 가지 옵션을 제공합니다.

* **bin** servlets
* **Sling** servlets

다음 예는 이러한 패턴을 따르는 서블릿과 Sling 서블릿을 사용하여 얻을 수 있는 혜택을 등록하는 방법을 보여 줍니다.

#### Bin servlets (one level down) {#bin-servlets-one-level-down}

**Bin** servlets는 많은 개발자가 J2EE 프로그래밍에 사용하는 패턴을 따릅니다. 서블릿은 특정 경로에 등록되며, AEM의 경우 대개 아래에 `/bin`있으며, 필요한 요청 매개 변수를 쿼리 문자열에서 추출합니다.

이 유형의 서블릿에 대한 SCR 주석은 다음과 같이 표시됩니다.

```
@SlingServlet(paths = "/bin/myApp/myServlet", extensions = "json", methods = "GET")
```

그런 다음 `SlingHttpServletRequest` `doGet` 메서드에 포함된 객체를 통해 쿼리 문자열에서 매개 변수를 추출합니다.예를 들면 다음과 같습니다.

```
String myParam = req.getParameter("myParam");
```

사용된 결과 URL은 다음과 같습니다.

`https://www.mydomain.com/bin/myApp/myServlet.json?myParam=myValue`

다음 방법으로 고려해야 할 몇 가지 사항이 있습니다.

* URL 자체에서 SEO 값이 손실됩니다. 검색 엔진을 포함하여 사이트에 액세스하는 사용자는 URL에서 의미 값을 받지 않습니다. URL은 콘텐츠 계층 구조가 아닌 프로그래밍 경로를 나타냅니다.
* URL에 쿼리 매개 변수가 있으면 디스패처가 응답을 캐시할 수 없음을 의미합니다.
* 이 서블릿의 보안을 설정하려면 서블릿에 사용자 지정 보안 로직을 구현해야 합니다.
* 디스패처가 노출되도록(주의 깊게) 구성해야 합니다 `/bin/myApp/myServlet`. 간단히 노출하면 사이트 방문자에게 열지 말아야 하는 특정 서블릿에 액세스할 수 `/bin` 있습니다.

#### Sling servlets (one level down) {#sling-servlets-one-level-down}

**Sling** servlets를 사용하여 반대로 서블릿을 등록할 수 있습니다. 서블릿을 지정하고 쿼리 매개 변수를 기반으로 렌더링할 서블릿을 지정하는 대신, 원하는 컨텐츠를 처리하고 Sling 선택기를 기반으로 컨텐츠를 렌더링할 서블릿을 지정합니다.

이 유형의 서블릿에 대한 SCR 주석은 다음과 같이 표시됩니다.

```
@SlingServlet(resourceTypes = "myBrand/components/pages/myPageType", selectors = "myRenderer", extensions = "json”, methods=”GET”)
```

이 경우 URL 주소(리소스 인스턴스)가 서블릿에서 자동으로 액세스할 수 있는 `myPageType` 리소스입니다. 이 프로그램에 액세스하려면

```
Resource myPage = req.getResource();
```

사용된 결과 URL은 다음과 같습니다.

`https://www.mydomain.com/content/my-brand/my-page.myRenderer.json`

이 방법의 이점은 다음과 같습니다.

* 사이트 계층 구조 및 페이지 이름에 있는 의미 체계로 얻은 SEO 값을 구울 수 있습니다.
* 쿼리 매개 변수가 없으므로 디스패처는 응답을 캐시할 수 있습니다. 또한, 주소 지정 페이지에 대한 모든 업데이트는 페이지를 활성화하면 이 캐시를 무효화합니다.
* 사용자가 이 서블릿에 액세스하려고 하면 적용되는 모든 ACL이 `/content/my-brand/my-page` 적용됩니다.
* 디스패처는 이미 이 컨텐츠를 웹 사이트 제공 기능으로 제공하도록 구성됩니다. 추가 구성은 필요하지 않습니다.

### URL 다시 작성 {#url-rewriting}

AEM에서 모든 웹 페이지는 아래에 저장됩니다 `/content/my-brand/my-content`. 이 기능은 저장소 데이터 관리의 관점에서 유용할 수 있지만 고객이 사이트를 원하는 방법은 아니며 SEO 지침과 상충하여 URL을 최대한 짧게 유지할 수 있습니다. 또한 동일한 AEM 인스턴스에서 다른 도메인 이름에서 여러 웹 사이트를 제공할 수 있습니다.

이 섹션에서는 이러한 URL을 관리하고 보다 읽기 쉽고 SEO 친화적으로 사용자에게 표시하기 위해 AEM에서 사용할 수 있는 옵션을 검토합니다.

#### 별칭 URL {#vanity-urls}

작성자가 홍보 목적으로 두 번째 위치에서 페이지에 액세스하려는 경우 페이지별로 정의된 AEM의 별칭 URL이 유용할 수 있습니다. 페이지에 대한 별칭 URL을 추가하려면 사이트 콘솔에서 해당 페이지로 **이동하여** 페이지 속성을 편집합니다. 기본 탭 아래쪽에 **별칭** URL을 추가할 수 있는 섹션이 표시됩니다. 두 개 이상의 URL을 통해 페이지에 액세스할 수 있으면 페이지의 SEO 값이 달라지므로 이 문제를 방지하려면 표준 URL 태그를 페이지에 추가해야 합니다.

#### 현지화된 페이지 이름 {#localized-page-names}

번역된 컨텐츠 사용자에게 현지화된 페이지 이름을 표시할 수 있습니다. 예:

* 스페인어를 사용하는 사용자가 다음 항목으로 이동하지 않고
   `www.mydomain.com/es/home.html`

* URL은 다음과 같은 것이 좋습니다.
   `www.mydomain.com/es/casa.html`.

페이지 이름을 현지화해야 하는 문제는 AEM 플랫폼에서 사용할 수 있는 많은 현지화 도구가 컨텐츠를 동기화하기 위해 로케일 간에 페이지 이름이 일치하는지 여부에 따라 달라집니다.

이 `sling:alias` 숙박 시설에서는 저희 케이크도 먹고 먹을 수 있습니다. `sling:alias` 리소스에 대한 별칭 이름을 허용하기 위해 속성으로 추가할 수 있습니다. 이전 예제에서 다음과 같은 결과가 있습니다.

* JCR의 페이지:
   `…/es/home`

* 그런 다음 속성을 추가합니다.
   `sling:alias` = `casa`

이렇게 하면 다중 사이트 관리자와 같은 AEM 번역 도구가 다음 간의 관계를 계속 유지할 수 있습니다.

* `/en/home`

* `/es/home`

또한 최종 사용자가 기본 언어로 페이지 이름과 상호 작용할 수 있습니다.

>[!NOTE]
>
>페이지 `sling:alias` 속성을 편집할 때 별칭 [속성을 사용하여 속성을 설정할 수 있습니다](/help/sites-authoring/editing-page-properties.md#advanced).

#### /etc/map {#etc-map}

표준 AEM 설치:

* for the OSGi configuration
   **Apache Sling Resource Resolver Factory**( `org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl`)

* 속성
   **매핑 위치** ( `resource.resolver.map.location`)

* defaults to `/etc/map`.

매핑 정의를 이 위치에 추가하여 인바운드 요청을 매핑하거나, AEM의 페이지에서 URL을 다시 작성하거나, 둘 모두를 매핑할 수 있습니다.

새 매핑을 만들려면 또는 아래의 이 위치에 새 `sling:Mapping` 노드를 `/http` 만듭니다 `/https`. 이 노드에 설정된 `sling:match` 및 `sling:internalRedirect` 속성을 기반으로 AEM은 일치하는 URL에 대한 모든 트래픽을 `internalRedirect` 속성에 지정된 값으로 리디렉션합니다.

이 방법이 공식 AEM 및 Sling 설명서에 설명된 접근 방식이지만, 이 구현에서 제공하는 정규 표현식 지원은 `SlingResourceResolver` 직접 를 사용하여 사용할 수 있는 옵션과 비교할 때 범위가 제한됩니다. 또한 이러한 방식으로 매핑을 구현하면 디스패처 캐시 무효화 문제가 발생할 수 있습니다.

다음은 이 문제가 발생하는 방법의 예입니다.

1. 사용자가 웹 사이트 방문 및 요청 `https://www.mydomain.com/my-page.html`
1. 디스패처는 이 요청을 게시 서버로 전달합니다.
1. 을 `/etc/map``/content/my-brand/my-page` 사용하면 게시 서버가 이 요청을 확인하고 페이지를 렌더링합니다.

1. 디스패처는 에서 응답을 캐싱하고 `/my-page.html` 사용자에게 응답을 반환합니다.
1. 컨텐츠 작성자는 이 페이지를 변경하고 활성화합니다.
1. 디스패처 플러시 에이전트가 에 대한 무효화 요청을 `/content/my-brand/my-page`**보냅니다.**디스패처가 이 경로에 캐시된 페이지를 가지고 있지 않으므로 이전 컨텐츠는 캐시된 상태로 유지되며 만료되지 않습니다.

캐시 무효화를 위해 더 짧은 URL을 더 긴 URL에 매핑하는 사용자 지정 디스패치 플러시 규칙을 구성하는 방법이 있습니다.

그러나 다음과 같은 간단한 방법으로 관리할 수 있습니다.

1. **SlingResourceResolver 규칙**

   웹 콘솔(예: localhost:4502/system/console/configMgr)을 사용하여 Sling 리소스 확인자를 구성할 수 있습니다.

   * **Apache Sling Resource Resolver Factory**
      `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)`.
   URL을 정규 표현식으로 단축하는 데 필요한 매핑을 작성한 다음 `config.publish`빌드에 포함된 OsgiConfignode에서 이러한 구성을 정의하는 것이 좋습니다.

   에서 매핑을 정의하지 `/etc/map`않고 속성 URL 매핑()에 직접 **할당할 수** 있습니다 `resource.resolver.mapping`.

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   이 간단한 예제에서는 URL이 있는 URL의 `/content/my-brand/` 시작 부분에서 제거됩니다.

   이렇게 하면 URL이 변환됩니다.

   * 시작 시간:`/content/my-brand/my-page.html`
   * 그냥 `/my-page.html`
   이는 URL을 가능한 한 짧게 유지하는 권장 방법과 일치합니다.

1. **페이지에 URL 출력 매핑**

   Apache Sling 리소스 확인자에서 매핑을 정의한 후에는 구성 요소에서 이러한 매핑을 사용하여 페이지에서 출력하는 URL이 짧거나 깔끔한지 확인해야 합니다. 이 작업은 의 지도 기능을 사용하여 수행할 수 `ResourceResolver`있습니다.

   예를 들어, 현재 페이지의 하위 항목을 나열하는 사용자 지정 탐색 구성 요소를 구현하는 경우 다음과 같이 매핑 방법을 사용할 수 있습니다.

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### Apache HTTP Server mod_rewrite {#apache-http-server-mod-rewrite}

지금까지 URL을 페이지에 출력할 때 이러한 매핑을 사용하기 위해 구성 요소의 로직과 매핑을 구현했습니다.

퍼즐의 마지막 조각은 이러한 단축된 URL을 처리하는데, 이 URL이 디스패처에 들어올 때, 즉 `mod_rewrite` 재생이 됩니다. URL을 사용할 `mod_rewrite` 때 가장 큰 이점은 URL을 디스패처 모듈로 보내기 *전에* 긴 형식으로 다시 매핑된다는 것입니다. 즉, 디스패처가 게시 서버에서 긴 URL을 요청하고 그에 따라 캐시합니다. 따라서 게시 서버에서 들어오는 모든 디스패처 플러시 요청은 이 컨텐츠를 성공적으로 무효화할 수 있습니다.

이러한 규칙을 구현하려면 Apache HTTP Server 구성에서 가상 호스트 아래에 `RewriteRule` 요소를 추가할 수 있습니다. 이전 예제에서 축약된 URL을 확장하려는 경우 다음과 같은 규칙을 구현할 수 있습니다.

```
<VirtualHost *:80>
  ServerName www.mydomain.com
  RewriteEngine on
  RewriteRule ^/(.*)$ /content/my-brand/$1 [PT,L]
  …
</VirtualHost>
```

### 표준 URL 태그 {#canonical-url-tags}

표준 URL 태그는 컨텐츠를 색인화하는 동안 검색 엔진이 페이지를 처리하는 방법을 명확히 하기 위해 HTML 문서의 헤드에 삽입된 링크 태그입니다. 페이지 URL에 차이가 있을 수 있는 경우에도 페이지의 (다른 버전)이 동일한 색인으로 인덱싱되도록 하는 것이 좋습니다.

예를 들어 사이트가 프린터에 적합한 페이지 버전을 제공하려는 경우 검색 엔진은 잠재적으로 이 페이지를 일반 버전의 페이지와 별도로 색인화합니다. 표준 태그는 검색 엔진에 동일한 것으로 알려줍니다.

예:

* https://www.mydomain.com/my-brand/my-page.html
* https://www.mydomain.com/my-brand/my-page.print.html

두 태그 모두 페이지 헤드에 다음 태그를 적용합니다.

```xml
<link rel=”canonical” href=”my-brand/my-page.html”/>
```

상대 또는 절대일 `href` 수 있습니다. 페이지 마크업에 코드가 포함되어야 페이지의 표준 URL을 확인하고 이 태그를 출력할 수 있습니다.

### 대/소문자 구문의 발송자 구성 {#configuring-the-dispatcher-for-case-insensitivity}

가장 좋은 방법은 소문자를 사용하여 모든 페이지를 제공하는 것입니다. 그러나 사용자가 URL에서 대문자를 사용하여 웹 사이트에 액세스할 때 404가 되는 것을 원하지 않습니다. 이러한 이유로 Apache HTTP Server 구성에 다시 작성 규칙을 추가하여 들어오는 모든 URL을 소문자로 매핑하는 것이 좋습니다. 또한 컨텐츠 작성자는 소문자로 페이지를 만들도록 교육해야 합니다.

모든 인바운드 트래픽을 소문자로 강제 수행하도록 Apache를 구성하려면 다음을 `vhost` 구성에 추가합니다.

```xml
RewriteEngine On
RewriteMap lowercase int:tolower
```

또한 `htaccess` 파일 맨 위에 다음을 추가합니다.

```xml
RewriteCond $1 [A-Z]
RewriteRule ^(.*)$ /${lowercase:$1} [R=301,L]
```

### 개발 환경을 보호하기 위해 robots.txt 구현 {#implementing-robots-txt-to-protect-development-environments}

검색 엔진은 *사이트 크롤링 전에 사이트 루트에* `robots.txt` 파일이 있는지 확인해야 합니다. Google, Yahoo 또는 Bing과 같은 주요 검색 엔진이 모두 이를 존중하지만 일부 외국 검색 엔진은 그렇지 않기 때문에 여기에서 강조해야 합니다.

전체 사이트에 대한 액세스를 차단하는 가장 간단한 방법은 사이트 `robots.txt` 루트에 다음 컨텐츠가 포함된 파일을 배치하는 것입니다.

```xml
User-agent: *
Disallow: /
```

또는 라이브 환경에서 색인을 원하지 않는 특정 경로를 허용하지 않도록 선택할 수 있습니다.

사이트 루트에 `robots.txt` 파일을 배치할 때의 주의점은 디스패처 플러시 요청이 이 파일을 지울 수 있고 URL 매핑은 Apache HTTP Server 구성에 정의된 `DOCROOT` 것과 다른 위치에 사이트 루트를 가져올 수 있다는 것입니다. 이러한 이유로 이 파일을 사이트 루트의 작성자 인스턴스에 배치하고 게시 인스턴스에 복제하는 것이 일반적입니다.

### AEM에서 XML 사이트 맵 작성 {#building-an-xml-sitemap-on-aem}

크롤러는 XML 사이트 맵을 사용하여 웹 사이트의 구조를 보다 잘 파악합니다. 사이트맵을 제공하면 SEO 순위가 향상될 것이라는 보장은 없지만, 이것은 합의된 우수 사례이다. 사이트 맵으로 사용할 XML 파일을 웹 서버에서 수동으로 유지 관리할 수 있지만, 사이트 맵을 프로그래밍 방식으로 생성하는 것이 좋습니다. 이렇게 하면 작성자가 새 컨텐츠를 만들 때 사이트 맵이 변경 사항을 자동으로 반영하게 됩니다.

사이트 맵을 프로그래밍 방식으로 생성하려면 `sitemap.xml` 호출을 위해 Sling 서블릿을 등록합니다. 그러면 서블릿은 서블릿 API를 통해 제공된 리소스를 사용하여 현재 페이지와 그 하위 페이지를 보고 XML을 출력할 수 있습니다. 그러면 XML이 디스패처에서 캐시됩니다. 이 위치는 `robots.txt` 파일의 sitemap 속성에서 참조되어야 합니다. 또한 새 페이지가 활성화될 때마다 이 파일을 플러시하도록 사용자 지정 플러시 규칙을 구현해야 합니다.

>[!NOTE]
>
>Sling Servlet을 등록하여 `sitemap` 확장자를 수신할 수 `xml`있습니다. 이렇게 하면 서블릿이 URL이 요청될 때마다 다음을 통해 요청을 처리합니다.
>    `/<path-to>/page.sitemap.xml`
그런 다음 요청에서 요청된 리소스를 가져와 JCR 파섹 API를 사용하여 컨텐츠 트리의 해당 지점에서 사이트 맵을 생성할 수 있습니다.
이와 같은 접근 방식의 이점은 동일한 인스턴스에서 여러 사이트를 제공하는 경우입니다. 요청을 `/content/siteA.sitemap.xml` 하면 `siteA` 추가 코드를 작성하지 않고도 사이트 맵을 생성할 `/content/siteB.sitemap.xml` 수 `siteB` 있습니다.

### 이전 URL에 대해 301 리디렉션 만들기 {#creating-redirects-for-legacy-urls}

새 구조로 사이트를 실행할 때 Apache HTTP Server에서 301 리디렉션을 구현하고 테스트하는 것은 두 가지 이유로 중요합니다.

* 이전 URL은 시간에 따라 SEO 값을 높였습니다. 리디렉션을 구현하여 검색 엔진은 이 값을 새 URL에 적용할 수 있습니다.
* 사이트 사용자가 이러한 페이지에 대한 책갈피를 만들었을지도 모릅니다. 리디렉션을 구현하면 사용자를 새 사이트의 페이지로 안내하여 이전 사이트에 연결하려는 위치와 가장 가깝게 일치시킬 수 있습니다.

301 리디렉션을 구현하는 방법에 대한 지침과 리디렉션이 예상대로 작동하는지 테스트할 수 있는 도구에 대해 아래의 추가 리소스 섹션을 확인하십시오.

## 추가 리소스 {#additional-resources}

자세한 내용은 다음 추가 리소스를 참조하십시오.

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

