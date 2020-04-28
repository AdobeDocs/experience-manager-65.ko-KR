---
title: 소셜 구성 요소 프레임워크
seo-title: 소셜 구성 요소 프레임워크
description: SCF(소셜 구성 요소 프레임워크)는 Communities 구성 요소를 구성, 사용자 정의 및 확장하는 프로세스를 단순화합니다.
seo-description: SCF(소셜 구성 요소 프레임워크)는 Communities 구성 요소를 구성, 사용자 정의 및 확장하는 프로세스를 단순화합니다.
uuid: 23b4418d-b91c-46fc-bf42-1154ef79fe5a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d7b5b5e3-2d84-4a6b-bcc2-d490882ff3ed
translation-type: tm+mt
source-git-commit: 6d425dcec4fab19243be9acb41c25b531a84ea74

---


# 소셜 구성 요소 프레임워크 {#social-component-framework}

SCF(소셜 구성 요소 프레임워크)는 서버측 및 클라이언트측 모두에서 Communities 구성 요소를 구성, 사용자 정의 및 확장하는 프로세스를 단순화합니다.

프레임워크의 이점

* **기능**:80%의 사용 사례를 사용자 요구에 맞게 변경할 필요 없이 즉시 통합할 수 있습니다.
* **스킨 변경이 가능한**&#x200B;경우:CSS 스타일링을 위해 HTML 속성을 일관되게 사용합니다.
* **확장 가능**:구성 요소 구현은 객체 지향적이고 비즈니스 로직에 대한 경미이며, 서버에서 증가분 비즈니스 로그인을 쉽게 추가할 수 있습니다.
* **유연성**:쉽게 오버레이되고 사용자 정의된 간단한 로직이 없는 JavaScript 템플릿.
* **액세스 가능**:HTTP API는 모바일 앱을 비롯한 모든 클라이언트의 게시를 지원합니다.
* **휴대용**:모든 기술을 기반으로 구축된 웹 페이지에 통합/임베드

인터랙티브한 커뮤니티 구성 요소 안내서를 [](components-guide.md)사용하여 작성자 또는 게시 인스턴스를 살펴볼 수 있습니다.

## 개요 {#overview}

SCF에서 구성 요소는 SocialComponent POJO, Handlebars JS 템플릿(구성 요소 렌더링용) 및 CSS(구성 요소의 스타일 지정)로 구성됩니다.

핸들바 JS 템플릿은 모델/뷰 JS 구성 요소를 확장하여 클라이언트의 구성 요소와의 사용자 상호 작용을 처리할 수 있습니다.

구성 요소가 데이터 수정을 지원해야 하는 경우 SocialComponent API의 구현을 작성하여 기존 웹 애플리케이션의 모델/데이터 개체와 유사한 데이터의 편집/저장을 지원할 수 있습니다. 또한 작업 요청 처리, 비즈니스 논리 수행 및 모델/데이터 개체에서 API를 호출하는 데 작업(컨트롤러)과 작업 서비스를 추가할 수 있습니다.

SocialComponent API를 확장하여 뷰 레이어 또는 HTTP 클라이언트에 대해 클라이언트가 요구하는 데이터를 제공할 수 있습니다.

### 클라이언트를 위해 페이지를 렌더링하는 방법 {#how-pages-are-rendered-for-client}

![chlimage_1-25](assets/chlimage_1-25.png)

### 구성 요소 사용자 정의 및 확장 {#component-customization-and-extension}

구성 요소를 사용자 정의하거나 확장하려면 /apps 디렉토리에 오버레이 및 확장자만 작성하여 향후 릴리스로 업그레이드하는 과정을 간소화합니다.

* 스키닝:
   * CSS만 [편집해야](client-customize.md#skinning-css)합니다.
* 룩앤필:
   * JS 템플릿 및 CSS를 변경합니다.
* Look, Feel 및 UX:
   * JS 템플릿, CSS를 변경하고 Javascript를 [확장/무시합니다](client-customize.md#extending-javascript).
* JS 템플릿 또는 GET 끝점에 사용할 수 있는 정보를 수정하려면:
   * SocialComponent를 [확장합니다](server-customize.md#socialcomponent-interface).
* 작업 중에 사용자 정의 처리를 추가하려면:
   * OperationExtension [을 작성합니다](server-customize.md#operationextension-class).
* 새 사용자 지정 작업을 추가하려면:
   * 새 Sling [게시물 작업을 만듭니다](server-customize.md#postoperation-class).
   * 필요에 따라 기존 [OperationServices](server-customize.md#operationservice-class) 사용
   * 필요에 따라 클라이언트 쪽에서 작업을 호출하는 Javascript 코드를 추가합니다.

## 서버측 프레임워크 {#server-side-framework}

프레임워크는 API를 제공하여 서버의 기능에 액세스하고 클라이언트와 서버 간의 상호 작용을 지원합니다.

### Java API {#java-apis}

Java API 파섹

기본 클래스는 서버측 사용자 정의 [페이지에 설명되어](server-customize.md) 있습니다.

UGC [를](srp.md) 사용하는 방법에 대한 자세한 내용은 스토리지 리소스 제공업체 개요를 참조하십시오.

### HTTP API {#http-api}

HTTP API 파섹 또한 HTTP API를 통해 커뮤니티 사이트는 클라이언트 없이 서비스로 실행되므로 프레임워크 구성 요소를 모든 기술을 기반으로 구축된 웹 페이지에 통합할 수 있습니다.

### HTTP API - 요청 가져오기 {#http-api-get-requests}

모든 SocialComponent에 대해 프레임워크는 HTTP 기반 API 끝점을 제공합니다. 끝점은 &#39;.social.json&#39; 선택기 + 확장명을 사용하여 GET 요청을 리소스로 전송하여 액세스합니다. Sling을 사용하면 요청이 `DefaultSocialGetServlet`담당자에게 전달됩니다.

**`DefaultSocialGetServlet`**

1. 리소스(resourceType)를 `SocialComponentFactoryManager` SocialComponentFactory에 전달하면 리소스를 `SocialComponent` 나타내는 SocialComponentFactory를 선택할 수 있습니다.

1. 공품을 호출하고 자원 및 요청을 처리할 `SocialComponent` 수 있는 능력을 받습니다.
1. 요청을 처리하고 결과의 JSON 표현을 반환하는 `SocialComponent`호출을 호출합니다.
1. 클라이언트에 대한 JSON 응답을 반환합니다.

**`GET Request`**

기본 GET 서블릿은 SocialComponent가 사용자 정의 가능한 JSON으로 응답하는 .social.json 요청을 수신합니다.

![chlimage_1-26](assets/chlimage_1-26.png)

### HTTP API - POST 요청 {#http-api-post-requests}

GET(읽기) 작업 외에도 프레임워크는 끝점 패턴을 정의하여 만들기, 업데이트 및 삭제를 비롯한 구성 요소에서 다른 작업을 수행할 수 있도록 합니다. 이러한 끝점은 HTTP 상태 코드 또는 JSON 응답 개체를 사용하여 입력을 받아들이고 응답하는 HTTP API입니다.

이 프레임워크 끝점 패턴을 사용하면 CUD 작업을 확장 가능하고 재사용 및 안정적으로 수행할 수 있습니다.

**`POST Request`**

모든 SocialComponent 작업에 대한 Sling POST:연산이 있습니다. 각 작업의 비즈니스 논리 및 유지 관리 코드는 HTTP API를 통해 또는 OSGi 서비스로 다른 곳에서 액세스할 수 있는 OperationService에 래핑됩니다. 후크는 적용 전/후 동작에 대한 지원 연결 가능 작업 확장을 제공합니다.

![chlimage_1-27](assets/chlimage_1-27.png)

### SRP(Storage Resource Provider) {#storage-resource-provider-srp}

[커뮤니티 콘텐츠 저장소에](working-with-srp.md)저장된 UGC 처리에 대한 자세한 내용은 다음을 참조하십시오.

* [스토리지 리소스 공급자 개요](srp.md) - 소개 및 저장소 사용 개요.
* [SRP 및 UGC Essentials](srp-and-ugc.md) - SRP API 유틸리티 메서드 및 예.
* [SRP를 사용하여 UGC에](accessing-ugc-with-srp.md) 액세스 - 코딩 지침

### 서버측 사용자 정의 {#server-side-customizations}

서버측에서 [커뮤니티 구성 요소의 비즈니스](server-customize.md) 로직과 작동 방식을 사용자 지정하는 방법에 대한 자세한 내용은 서버측 사용자 지정을 참조하십시오.

## Handlebars JS 템플릿 언어 {#handlebars-js-templating-language}

새로운 프레임워크에서 더욱 눈에 띄는 변화 중 하나는 서버-클라이언트 렌더링을 위한 [널리 사용되는 오픈 소스 기술인 HBS(Handlebars JS 템플릿 언어)](https://www.handlebarsjs.com/)사용을 의미합니다.

HBS는 클라이언트측 렌더링을 지원하기 때문에 HBS 스크립트를 간단하고 로직이 필요 없으며 서버와 클라이언트 모두에서 컴파일되고, 오버레이와 사용자 정의가 간편하며, 클라이언트 UX와 자연스럽게 바인딩됩니다.

프레임워크에서는 SocialComponents [를](handlebars-helpers.md) 개발할 때 유용한 여러 Handlebars 도움말을 제공합니다.

서버에서 Sling이 GET 요청을 확인하면 요청에 응답하는 데 사용할 스크립트를 식별합니다. 스크립트가 HBS 템플릿(.hbs)인 경우 Sling은 요청을 핸들바 엔진에 위임합니다. 그러면 핸들바 엔진은 해당 SocialComponentFactory에서 SocialComponent를 가져와 컨텍스트를 작성하고 HTML을 렌더링합니다.

### 액세스 제한 없음 {#no-access-restriction}

HBS(Handlebars) 템플릿 파일(.hbs)은 .jsp 및 .html 템플릿 파일과 유사하지만 클라이언트 브라우저와 서버에서 렌더링하는 데 사용할 수 있습니다. 따라서 클라이언트측 템플릿을 요청하는 클라이언트 브라우저는 서버로부터 .hbs 파일을 수신하게 됩니다.

이렇게 하려면 모든 사용자가 Sling 검색 경로에 있는 모든 HBS 템플릿(/libs/ 또는 /apps 아래에 있는 모든 .hbs 파일)을 작성자 또는 게시에서 가져올 수 있어야 합니다.

.hbs 파일에 대한 HTTP 액세스는 금지되지 않을 수 있습니다.

### 커뮤니티 구성 요소 추가 또는 포함 {#add-or-include-a-communities-component}

대부분의 Communities 구성 요소를 Sling 지정 가능 *리소스로* 추가해야 합니다. 일부 Communities 구성 요소를 기존 리소스 이외의 리소스로 템플릿에 *포함할* 수 있으므로 UGC(사용자 생성 컨텐츠)를 작성할 위치의 동적 포함 및 사용자 지정을 허용할 수 있습니다.

두 경우 모두 구성 요소의 [필수 클라이언트 라이브러리도](clientlibs.md) 있어야 합니다.

**구성 요소 추가**

구성 요소를 추가하면 구성 요소 브라우저(사이드킥의)에서 작성 편집 모드로 페이지로 드래그하는 경우와 같이 리소스(구성 요소)의 인스턴스를 추가하는 프로세스를 의미합니다.

결과는 JCR 하위 노드(Sling addressable)의 단락 아래에 있습니다.

**구성 요소 포함**

구성 요소를 포함한다는 것은 스크립팅 언어 사용과 같이 템플릿 내에서 [&quot;존재하지 않는&quot; 리소스](srp.md#for-non-existing-resources-ners) (JCR 노드 없음)에 대한 참조를 추가하는 프로세스를 의미합니다.

AEM 6.1부터 구성 요소가 추가되는 대신 동적으로 포함되는 경우, 작성 *design *mode에서 구성 요소의 속성을 편집할 수 있습니다.

일부 AEM Communities 구성 요소만 동적으로 포함될 수 있습니다. 다음과 같습니다.

* [댓글](essentials-comments.md)
* [등급](rating-basics.md)
* [검토](reviews-basics.md)
* [투표](essentials-voting.md)

커뮤니티 구성 [요소](components-guide.md) 가이드를 사용하면 포함 가능한 구성 요소를 추가할 수 있습니다.

**handlebars 템플릿** 언어를 사용할 때, 비기존 리소스는 resourceType을 지정하여 [include helper](handlebars-helpers.md#include) 를 사용하여 포함됩니다.

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**JSP를**&#x200B;사용할 때 리소스는 cq:include [](../../help/sites-developing/taglib.md#lt-cq-include)태그를 사용하여 포함됩니다.

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>템플릿에 구성 요소를 추가하거나 포함하는 대신 페이지에 동적으로 추가하려면 구성 요소 [사이드로드를 참조하십시오](sideloading.md).


### Handlebars Helpers {#handlebars-helpers}

SCF [에서](handlebars-helpers.md) 사용할 수 있는 사용자 지정 도움말의 목록과 설명은 SCF Handlebars Helpers를 참조하십시오.

## 클라이언트측 프레임워크 {#client-side-framework}

### Model-View Javascript Framework {#model-view-javascript-framework}

이 프레임워크에는 풍부하고 인터랙티브한 [구성 요소를 쉽게 개발할 수 있도록](https://www.backbonejs.org/)모델 뷰 JavaScript 프레임워크인 Backon.js의 확장이 포함되어 있습니다. 객체 지향적인 특성은 확장 가능한/재사용 가능한 프레임워크를 지원합니다. 클라이언트와 서버 간의 통신은 HTTP API를 통해 간소화됩니다.

프레임워크는 서버측 핸들바 템플릿을 활용하여 클라이언트에 대한 구성 요소를 렌더링합니다. 모델은 HTTP API에서 생성된 JSON 응답을 기반으로 합니다. 보기는 Handlebars 템플릿으로 생성된 HTML에 바인딩되며 상호 작용을 제공합니다.

### CSS 규칙 {#css-conventions}

다음은 CSS 클래스를 정의하고 사용하기 위한 권장 규칙입니다.

* 명확하게 이름이 지정된 CSS 클래스 선택기 이름을 사용하고 &#39;heading&#39;, &#39;image&#39; 등과 같은 일반 이름은 사용하지 마십시오.
* CSS 스타일시트가 페이지의 다른 요소 및 스타일과 잘 작동하도록 특정 클래스 선택기 스타일을 정의합니다. 예를 들어,`.social-forum .topic-list .li { color: blue; }`
* CSS 클래스를 유지하여 스타일을 지정할 수 있으며 JavaScript 기반의 UX를 위한 CSS 클래스와 별도로 지정할 수 있습니다.

### 클라이언트측 사용자 정의 {#client-side-customizations}

클라이언트측에서 커뮤니티 구성 요소의 모양과 동작을 사용자 정의하려면 다음 [정보가](client-customize.md)포함된 클라이언트측 사용자 지정을 참조하십시오.

* [오버레이](client-customize.md#overlays)
* [익스텐션](client-customize.md#extensions)
* [HTML 마크업](client-customize.md#htmlmarkup)
* [CSS 스키닝](client-customize.md#skinning-css)
* [Javascript 확장](client-customize.md#extending-javascript)
* [SCF용 Clientlibs](client-customize.md#clientlibs-for-scf)

## Feature and Component Essentials {#feature-and-component-essentials}

개발자를 위한 필수 정보는 기능 [및 구성 요소 필수](essentials.md) 섹션에 설명되어 있습니다.

추가 개발자 정보는 코딩 지침 [섹션에서 찾을 수](code-guide.md) 있습니다.

## 문제 해결 {#troubleshooting}

일반적인 문제 및 알려진 문제는 문제 해결 [섹션에 설명되어](troubleshooting.md) 있습니다.

