---
title: 소셜 구성 요소 프레임워크
description: SCF(소셜 구성 요소 프레임워크)를 사용하면 커뮤니티 구성 요소를 구성, 사용자 지정 및 확장하는 프로세스를 단순화할 수 있습니다
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 5ca58bc3-8505-4d91-9cd1-6b2e2671f1be
source-git-commit: e161c37544c3391607cbe495644f3353b9f77fe3
workflow-type: tm+mt
source-wordcount: '1478'
ht-degree: 0%

---

# 소셜 구성 요소 프레임워크 {#social-component-framework}

SCF(소셜 구성 요소 프레임워크)를 사용하면 서버측과 클라이언트측 모두에서 커뮤니티 구성 요소를 구성, 사용자 지정 및 확장하는 프로세스를 단순화할 수 있습니다.

프레임워크의 이점:

* **기능**: 사용 사례의 80%에 대해 사용자 정의가 거의 또는 전혀 없는 즉시 사용 가능한 통합
* **스킨 가능**: CSS 스타일링을 위한 HTML 속성을 일관되게 사용합니다.
* **확장 가능**: 구성 요소 구현은 개체 지향적이며 비즈니스 논리에 유연하므로 서버에서 증분 비즈니스 로그인을 쉽게 추가할 수 있습니다.
* **유연성**: 간편하게 오버레이하고 사용자 정의할 수 있는 간단한 논리 없는 JavaScript 템플릿입니다.
* **액세스 가능**: HTTP API는 모바일 앱을 포함하여 모든 클라이언트의 게시를 지원합니다.
* **휴대용**: 모든 기술을 기반으로 구축된 웹 페이지에 통합/임베드

대화형 기능을 사용하여 작성자 또는 게시 인스턴스에서 탐색 [커뮤니티 구성 요소 안내서](components-guide.md).

## 개요 {#overview}

SCF에서 구성 요소는 SocialComponent POJO, Handlebars JS Template(구성 요소를 렌더링함) 및 CSS(구성 요소의 스타일을 지정함)로 구성됩니다.

Handlebars JS 템플릿은 모델/보기 JS 구성 요소를 확장하여 클라이언트의 구성 요소와 사용자 상호 작용을 처리할 수 있습니다.

구성 요소가 데이터 수정을 지원해야 하는 경우 기존 웹 애플리케이션의 모델/데이터 개체와 유사한 데이터의 편집/저장을 지원하도록 SocialComponent API의 구현을 작성할 수 있습니다. 또한 작업 요청을 처리하고 비즈니스 논리를 수행하며 모델/데이터 개체에 대한 API를 호출하기 위해 작업(컨트롤러) 및 작업 서비스를 추가할 수 있습니다.

SocialComponent API는 클라이언트가 보기 계층 또는 HTTP 클라이언트에 필요한 데이터를 제공하도록 확장될 수 있습니다.

### 클라이언트용 페이지 렌더링 방법 {#how-pages-are-rendered-for-client}

![scf 페이지 렌더링](assets/scf-overview.png)

### 구성 요소 사용자 지정 및 확장 {#component-customization-and-extension}

구성 요소를 사용자 정의하거나 확장하려면 /apps 디렉토리에 오버레이 및 확장만 작성하여 향후 릴리스로 업그레이드하는 프로세스를 간소화합니다.

* 스키닝의 경우:
   * 만 [CSS 편집 필요](client-customize.md#skinning-css).
* 디자인:
   * JS 템플릿 및 CSS를 변경합니다.
* 모양, 느낌 및 UX의 경우:
   * JS 템플릿, CSS 및 [JavaScript 확장/재정의](client-customize.md#extending-javascript).
* JS 템플릿 또는 GET 엔드포인트에서 사용할 수 있는 정보를 수정하려면 다음을 수행합니다.
   * 확장 [소셜 구성 요소](server-customize.md#socialcomponent-interface).
* 작업 중 사용자 정의 처리를 추가하려면 다음을 수행합니다.
   * 쓰기 [작업 확장](server-customize.md#operationextension-class).
* 사용자 지정 작업을 추가하려면:
   * 새로 만들기 [Sling Post 작업](server-customize.md#postoperation-class).
   * 기존 항목 사용 [OperationServices](server-customize.md#operationservice-class) 필요한 경우.
   * 필요에 따라 클라이언트측에서 작업을 호출하는 JavaScript 코드를 추가합니다.

## 서버측 프레임워크 {#server-side-framework}

프레임워크는 서버의 기능에 액세스하고 클라이언트와 서버 간의 상호 작용을 지원하는 API를 제공합니다.

### Java™ API {#java-apis}

Java™ API는 쉽게 상속되거나 하위 클래스화되는 추상 클래스 및 인터페이스를 제공합니다.

기본 클래스는에 설명되어 있습니다. [서버측 사용자 지정](server-customize.md) 페이지를 가리키도록 업데이트하는 중입니다.

방문 [저장소 리소스 공급자 개요](srp.md) ugc 작업에 대해 알아봅니다.

### HTTP API {#http-api}

HTTP API는 PhoneGap 앱, 기본 앱 및 기타 통합 및 매쉬업에 대한 간편한 사용자 지정 및 클라이언트 플랫폼 선택을 지원합니다. 또한 HTTP API를 사용하면 커뮤니티 사이트를 클라이언트 없이 서비스로 실행할 수 있으므로 프레임워크 구성 요소를 모든 기술에 구축된 웹 페이지에 통합할 수 있습니다.

### HTTP API - GET 요청 {#http-api-get-requests}

모든 SocialComponent에 대해 프레임워크는 HTTP 기반 API 끝점을 제공합니다. 끝점은 &#39;.social.json&#39; 선택기 + 확장을 사용하여 리소스에 GET 요청을 전송하여 액세스됩니다. Sling을 사용하여 요청은 로 전달됩니다. `DefaultSocialGetServlet`.

**`DefaultSocialGetServlet`**

1. 리소스(resourceType)를 `SocialComponentFactoryManager` 및 은(는) 다음을 선택할 수 있는 SocialComponentFactory를 받습니다. `SocialComponent` 리소스를 나타냅니다.

1. 팩토리를 호출하고 `SocialComponent` 리소스 및 요청을 처리할 수 있습니다.
1. 호출 `SocialComponent`요청을 처리하고 결과의 JSON 표현을 반환합니다.
1. 클라이언트에 JSON 응답을 반환합니다.

**`GET Request`**

기본 GET 서블릿은 SocialComponent가 사용자 지정 가능한 JSON으로 응답하는 .social.json 요청을 수신합니다.

![scf 프레임워크](assets/scf-framework.png)

### HTTP API - POST 요청 {#http-api-post-requests}

GET(읽기) 작업 외에도 프레임워크는 구성 요소에서 만들기, 업데이트 및 삭제를 비롯한 다른 작업을 활성화하는 엔드포인트 패턴을 정의합니다. 이러한 끝점은 입력을 수락하고 HTTP 상태 코드 또는 JSON 응답 개체로 응답하는 HTTP API입니다.

이 프레임워크 엔드포인트 패턴을 통해 CUD 작업을 확장, 재사용 및 테스트할 수 있습니다.

**`POST Request`**

모든 SocialComponent 작업에 대한 Sling POST:작업이 있습니다. 각 작업에 대한 비즈니스 논리 및 유지 관리 코드는 HTTP API를 통해 또는 다른 곳에서 OSGi 서비스로 액세스할 수 있는 OperationService에 래핑됩니다. 전/후 작업에 대한 플러그형 작업 확장을 지원하는 후크가 제공됩니다.

![scf-post-request](assets/scf-post-request.png)

### 저장소 리소스 제공자(SRP) {#storage-resource-provider-srp}

에 저장된 UGC 처리에 대해 알아보려면 [커뮤니티 콘텐츠 저장소](working-with-srp.md)를 참조하십시오.

* [저장소 리소스 공급자 개요](srp.md) - 소개 및 저장소 사용 개요.
* [SRP 및 UGC 필수 패키지](srp-and-ugc.md) - SRP API 유틸리티 메서드 및 예제.
* [SRP를 사용하여 UGC에 액세스](accessing-ugc-with-srp.md) - 코딩 지침

### 서버측 사용자 지정 {#server-side-customizations}

방문 [서버측 사용자 지정](server-customize.md) 서버측에서 Communities 구성 요소의 비즈니스 논리 및 동작을 사용자 지정하는 방법에 대한 정보입니다.

## Handlebars JS 템플릿 언어 {#handlebars-js-templating-language}

새 프레임워크에서 보다 눈에 띄는 변화 중 하나는 `Handlebars JS` (HBS)서버 클라이언트 렌더링에 널리 사용되는 오픈 소스 기술인 템플릿 언어.

HBS 스크립트는 간단하고 논리를 사용하지 않으며, 서버와 클라이언트에서 컴파일하고, 오버레이와 맞춤화가 쉽고, HBS가 클라이언트측 렌더링을 지원하므로 클라이언트 UX와 자연스럽게 바인딩됩니다.

프레임워크는 다음과 같은 몇 가지 기능을 제공합니다 [Handlebars 도우미](handlebars-helpers.md) 소셜 구성 요소를 개발할 때 유용합니다.

서버에서 Sling은 GET 요청을 확인하면 요청에 응답하는 데 사용되는 스크립트를 식별합니다. 스크립트가 HBS 템플릿(.hbs)인 경우 Sling은 요청을 Handlebars 엔진에 위임합니다. 그런 다음 Handlebars 엔진은 적절한 SocialComponentFactory에서 SocialComponent를 가져와서 컨텍스트를 빌드하고 HTML을 렌더링합니다.

### 액세스 제한 없음 {#no-access-restriction}

Handlebars(HBS) 템플릿 파일(.hbs)은 클라이언트 브라우저와 서버 모두에서 렌더링하는 데 사용할 수 있다는 점을 제외하면 .jsp 및 .html 템플릿 파일과 유사합니다. 따라서 클라이언트측 템플릿을 요청하는 클라이언트 브라우저는 서버로부터 .hbs 파일을 수신하게 됩니다.

이를 위해서는 작성자 또는 게시의 모든 사용자가 sling 검색 경로의 모든 HBS 템플릿(/libs/ 또는 /apps 아래의 모든 .hbs 파일)을 가져올 수 있어야 합니다.

.hbs 파일에 대한 HTTP 액세스를 금지할 수 없습니다.

### 커뮤니티 구성 요소 추가 또는 포함 {#add-or-include-a-communities-component}

대부분의 커뮤니티 구성 요소는 다음과 같아야 합니다. *추가됨* Sling 주소 지정 가능 리소스. Communities 구성 요소 중 선택된 일부는 다음과 같습니다. *포함됨* 사용자 생성 컨텐츠(UGC)를 작성할 위치를 동적으로 포함 및 사용자 지정할 수 있도록 해주는 존재하지 않는 리소스로서의 템플릿.

두 경우 모두 구성 요소는 [필수 클라이언트 라이브러리](clientlibs.md) 도 있어야 합니다.

**구성 요소 추가**

구성 요소 추가는 구성 요소 브라우저(사이드 킥)에서 작성자 편집 모드의 페이지로 드래그한 경우와 같이 리소스(구성 요소)의 인스턴스를 추가하는 프로세스를 의미합니다.

그 결과 Sling 주소 지정 가능한 par 노드 아래에 JCR 하위 노드가 있습니다.

**구성 요소 포함**

구성 요소를 포함한다는 것은 다음에 대한 참조를 추가하는 프로세스를 의미합니다. [&quot;존재하지 않는&quot; 리소스](srp.md#for-non-existing-resources-ners) (JCR 노드 없음) 템플릿 내에서 사용할 수 있습니다(예: 스크립팅 언어 사용).

Adobe Experience Manager(AEM) 6.1부터 구성 요소가 추가되는 대신 동적으로 포함되면 작성자에서 구성 요소의 속성을 편집할 수 있습니다 *디자인* 모드.

AEM Communities 구성 요소 중 선택한 일부만 동적으로 포함될 수 있습니다. 이는 다음과 같습니다.

* [댓글](essentials-comments.md)
* [등급](rating-basics.md)
* [리뷰](reviews-basics.md)
* [투표](essentials-voting.md)

다음 [커뮤니티 구성 요소 안내서](components-guide.md) 포함 가능한 구성 요소를 추가에서 포함으로 전환할 수 있습니다.

**Handlebars 사용 시** 언어 템플릿을 만드는 경우 [도우미 포함](handlebars-helpers.md#include) resourceType을 지정하여

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**JSP 사용 시**&#x200B;태그를 사용하여 리소스가 포함됩니다 [cq:include](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>구성 요소를 템플릿에 추가하거나 포함하는 대신 페이지에 동적으로 추가하려면 다음을 참조하십시오. [구성 요소 사이드로드](sideloading.md).

### Handlebars 도우미 {#handlebars-helpers}

다음을 참조하십시오 [SCF Handlebars 도우미](handlebars-helpers.md) SCF에서 사용할 수 있는 사용자 지정 도우미 목록 및 설명입니다.

## 클라이언트측 프레임워크 {#client-side-framework}

### 모델 보기 JavaScript 프레임워크 {#model-view-javascript-framework}

프레임워크는 의 확장을 포함합니다. [Backbone.js](https://backbonejs.org/): 풍부한 대화형 구성 요소의 개발을 용이하게 하는 모델 보기 JavaScript 프레임워크입니다. 객체 지향 속성은 확장/재사용 가능한 프레임워크를 지원합니다. 클라이언트와 서버 간의 통신은 HTTP API를 통해 간소화됩니다.

프레임워크는 서버측 Handlebars 템플릿을 사용하여 클라이언트의 구성 요소를 렌더링합니다. 이 모델은 HTTP API에서 생성된 JSON 응답을 기반으로 합니다. 보기는 Handlebars 템플릿에서 생성된 HTML에 바인딩되며 상호 작용을 제공합니다.

### CSS 규칙 {#css-conventions}

다음은 CSS 클래스를 정의하고 사용하기 위한 권장 규칙입니다.

* 명확하게 네임스페이스가 지정된 CSS 클래스 선택기 이름을 사용하고 &#39;heading&#39; 및 &#39;image&#39;와 같은 일반 이름을 사용하지 마십시오.
* CSS 스타일 시트가 페이지의 다른 요소 및 스타일과 잘 작동하도록 특정 클래스 선택기 스타일을 정의합니다. 예를 들어`.social-forum .topic-list .li { color: blue; }`
* 스타일링을 위한 CSS 클래스는 JavaScript로 구동되는 UX의 CSS 클래스와 구분됩니다.

### 클라이언트측 사용자 지정 {#client-side-customizations}

클라이언트측에서 Communities 구성 요소의 모양과 동작을 사용자 지정하려면 을 참조하십시오. [클라이언트측 사용자 지정](client-customize.md), 다음에 대한 정보가 포함됩니다.

* [오버레이](client-customize.md#overlays)
* [확장](client-customize.md#extensions)
* [HTML 마크업](client-customize.md#htmlmarkup)
* [CSS 스키닝](client-customize.md#skinning-css)
* [JavaScript 확장](client-customize.md#extending-javascript)
* [SCF용 Clientlibs](client-customize.md#clientlibs-for-scf)

## 기능 및 구성 요소 기본 사항 {#feature-and-component-essentials}

개발자를 위한 필수 정보는 [기능 및 구성 요소 기본 사항](essentials.md) 섹션.

추가 개발자 정보는 [코딩 지침](code-guide.md) 섹션.

## 문제 해결 {#troubleshooting}

일반적인 문제 및 알려진 문제는에 설명되어 있습니다 [문제 해결](troubleshooting.md) 섹션.
