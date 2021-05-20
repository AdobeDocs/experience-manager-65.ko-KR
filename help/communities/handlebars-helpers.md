---
title: SCF Handlebars Helpers
seo-title: SCF Handlebars Helpers
description: Handlebars 도우미 메서드를 사용하여 SCF와 작업할 수 있습니다
seo-description: Handlebars 도우미 메서드를 사용하여 SCF와 작업할 수 있습니다
uuid: 9c514199-871e-4b68-8147-2052d2eeda15
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8b6c1697-d693-41f4-8337-f41658465107
exl-id: bfb95cae-4b0f-4521-a113-042dc4005a63
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 2%

---

# SCF Handlebars 도우미 {#scf-handlebars-helpers}

| **[⇐ 기능 핵심 사항](essentials.md)** | **[서버 측 사용자 지정 ⇒](server-customize.md)** |
|---|---|
|  | **[클라이언트측 사용자 지정 ⇒](client-customize.md)** |

Handlebars Helper(helper)는 SCF 구성 요소 작업을 용이하게 하기 위해 Handlebars 스크립트에서 호출할 수 있는 메서드입니다.

구현에는 클라이언트측 및 서버측 정의가 포함됩니다. 개발자가 사용자 지정 helper를 만들 수도 있습니다.

AEM Communities과 함께 제공되는 사용자 지정 SCF 도우미는 [클라이언트 라이브러리](../../help/sites-developing/clientlibs.md)에 정의됩니다.

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>[최신 커뮤니티 기능 팩](deploy-communities.md#latestfeaturepack)을 설치하십시오.

## 생략 {#abbreviate}

maxWords 및 maxLength 속성을 따르는 약식 문자열을 반환하는 도우미.

축약할 문자열은 컨텍스트로 제공됩니다. 제공된 컨텍스트가 없으면 빈 문자열이 반환됩니다.

먼저 컨텍스트를 maxLength로 트리밍한 다음 컨텍스트를 단어로 잘라서 maxWords로 줄입니다.

safeString을 true로 설정하면 반환된 문자열이 SafeString입니다.

### 매개 변수 {#parameters}

* **컨텍스트**:문자열

   (선택 사항) 기본값은 빈 문자열입니다

* **maxLength**:숫자

   (선택 사항) 기본값은 컨텍스트 길이입니다.

* **maxWords**:숫자

   (선택 사항) 기본값은 트림된 문자열의 단어 수입니다.

* **safeString**:부울

   (선택 사항) true이면 Handlebars.SafeString() 을 반환합니다. 기본값은 false입니다.

### 예 {#examples}

```
{{abbreviate subject maxWords=2}}

/*
If subject =
    "AEM Communities - Site Creation Wizard"

Then abbreviate would return
    "AEM Communities".
*/
```

```
{{{abbreviate message safeString=true maxLength=30}}}

/*
If message =
    "The goal of AEM Communities is to quickly create a community engagement site."

Then abbreviate would return
    "The goal of AEM Communities is"
*/
```

## 컨텐츠 로드 자세히 {#content-loadmore}

두 개의 범위를 div 아래에 추가하는 도우미가, 전체 텍스트에 대해 하나씩, 덜 사용되는 텍스트에 대해 하나씩, 두 보기 간에 전환할 수 있습니다.

### 매개 변수 {#parameters-1}

* **컨텍스트**:문자열

   (선택 사항) 기본값은 빈 문자열입니다.

* **numChars**:숫자

   (선택 사항) 전체 텍스트를 표시하지 않을 때 표시할 문자 수입니다. 기본값은 100입니다.

* **추가 텍스트**:문자열

   (선택 사항) 표시할 텍스트가 더 있음을 나타내는 텍스트입니다. 기본값은 &quot;자세히&quot;입니다.

* **줄임표 텍스트**:문자열

   (선택 사항) 숨겨진 텍스트가 있음을 나타내는 텍스트입니다. 기본값은 &quot;...&quot;입니다.

* **safeString**:부울

   (선택 사항) 결과를 반환하기 전에 Handlebars.SafeString()을 적용할지 여부를 나타내는 부울 값입니다. 기본값은 false입니다.

### 예 {#example}

```
{{content-loadmore  context numChars=32  moreText="go on"  ellipsesText="..." }}

/*
If context =
    "Here is the initial less content and this is more content."

Then content-loadmore would return
    "Here is the initial less content<span class="moreelipses">...</span> <span class="scf-morecontent"><span>and this is more content.</span>  <a href="" class="scf-morelink" evt="click=toggleContent">go on</a></span>"
*/
```

## DateUtil {#dateutil}

형식이 지정된 날짜 문자열을 반환하는 도우미.

### 매개 변수 {#parameters-2}

* **컨텍스트**:숫자

   (선택 사항) 1970년 1월 1일부터 오프셋(epoch)인 밀리초 값입니다. 기본값은 현재 날짜입니다.

* **형식**:문자열

   (선택 사항) 적용할 날짜 형식입니다. 기본값은 &quot;YYYY-MM-DDTHH:mm:ss.ssZ&quot;이며, 결과는 &quot;2015-03-18T18:17:13-07:00&quot;으로 표시됩니다

### 예 {#examples-1}

```
{{dateUtil this.memberSince format="dd MMM yyyy, hh:mm"}}

// returns "18 Mar 2015, 18:17"
```

```
{{dateUtil this.birthday format="MM-DD-YYYY"}}

// returns "03-18-2015"
```

## 다음과 같음 {#equals}

같음 조건자에 따라 콘텐츠를 반환하는 도우미.

### 매개 변수 {#parameters-3}

* **lvalue**:문자열

   비교할 왼쪽 값입니다.

* **값**:문자열

   비교할 오른쪽 값입니다.

### 예 {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
{{else}}
  <div>They are NOT equal!</div>
{{/equals}}
```

## If-wcm-mode {#if-wcm-mode}

문자열로 구분된 모드 목록에 대해 [WCM 모드](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html)의 현재 값을 테스트하는 블록 도우미입니다.

### 매개 변수 {#parameters-4}

* **컨텍스트**:문자열

   (선택 사항) 번역할 문자열입니다. 기본값이 제공되지 않을 경우 필수입니다.

* **모드**:문자열

   (선택 사항) 설정되어 있는 경우 테스트할 [WCM 모드](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html)를 쉼표로 구분한 목록입니다.

### 예 {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{{else}}
 ...
{{/if-wcm-mode}}
```

## i18n {#i-n}

이 도우미는 Handlebars 도우미 &#39;i18n&#39;을 무시합니다.

[JavaScript 코드에서 문자열 다국어화](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code)를 참조하십시오.

### 매개 변수 {#parameters-5}

* **컨텍스트**:문자열

   (선택 사항) 번역할 문자열입니다. 기본값이 제공되지 않을 경우 필수입니다.

* **기본값**:문자열

   (선택 사항) 번역할 기본 문자열입니다. 제공된 컨텍스트가 없는 경우 필요합니다.

* **댓글**:문자열

   (선택 사항) 번역 힌트입니다

### 예 {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## 포함 {#include}

템플릿에 구성 요소를 존재하지 않는 리소스로 포함할 도우미.

이를 통해 JCR 노드로 추가된 리소스에 대해 가능한 것보다 프로그래밍 방식으로 리소스를 사용자 지정할 수 있습니다. [커뮤니티 구성 요소 추가 또는 포함](scf.md#add-or-include-a-communities-component)을 참조하십시오.

일부 Communities 구성 요소만 포함할 수 있습니다. AEM 6.1의 경우, 포함하는 항목은 [댓글](essentials-comments.md), [등급](rating-basics.md), [review](reviews-basics.md) 및 [투표](essentials-voting.md)입니다.

서버측에만 해당하는 이 도우미는 JSP 스크립트의 [cq:include](../../help/sites-developing/taglib.md)와 유사한 기능을 제공합니다.

### 매개 변수 {#parameters-6}

* **컨텍스트**:문자열 또는 개체

   (상대 경로를 제공하지 않는 한 선택 사항입니다)

   `this` 을 사용하여 현재 컨텍스트를 전달합니다.

   `this.id` 을 사용하여 요청된 resourceType을 렌더링하기 위해 `id`에서 리소스를 가져옵니다.

* **resourceType**:문자열

   (선택 사항) 리소스 유형은 기본적으로 컨텍스트의 리소스 유형으로 설정됩니다.

* **템플릿**:문자열

   구성 요소 스크립트의 경로입니다.

* **경로**:문자열

   (필수) 리소스의 경로입니다. 경로가 상대적이면 컨텍스트를 제공해야 하며, 그렇지 않으면 빈 문자열이 반환됩니다.

* **authoringDisabled**:부울

   (선택 사항) 기본값은 false입니다. 내부용입니다.

### 예 {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

여기에는 `this.id` + /comments에 새 주석 구성 요소가 포함됩니다.

## IncludeClientLib {#includeclientlib}

js, css 또는 테마 라이브러리일 수 있는 AEM html 클라이언트 라이브러리를 포함하는 도우미. js 및 css와 같은 다양한 유형의 여러 포함을 위해 이 태그를 Handlebars 스크립트에서 여러 번 사용해야 합니다.

서버측에만 해당하는 이 도우미는 JSP 스크립트의 [ui:includeClientLib](../../help/sites-developing/taglib.md)와 유사한 기능을 제공합니다.

### 매개 변수 {#parameters-7}

* **카테고리**:문자열

   (선택 사항) 쉼표로 구분된 클라이언트 라이브러리 카테고리 목록입니다. 여기에는 지정된 카테고리에 대한 모든 Javascript 및 CSS 라이브러리가 포함됩니다. 요청에서 테마 이름이 추출됩니다.

* **테마**:문자열

   (선택 사항) 쉼표로 구분된 클라이언트 라이브러리 카테고리 목록입니다. 여기에는 지정된 카테고리에 대한 모든 테마 관련 라이브러리(CSS와 JS 모두)가 포함됩니다. 요청에서 테마 이름이 추출됩니다.

* **js**:문자열

   (선택 사항) 쉼표로 구분된 클라이언트 라이브러리 카테고리 목록입니다. 여기에는 지정된 카테고리에 대한 모든 Javascript 라이브러리가 포함됩니다.

* **css**:문자열

   (선택 사항) 쉼표로 구분된 클라이언트 라이브러리 카테고리 목록입니다. 여기에는 지정된 카테고리의 모든 CSS 라이브러리가 포함됩니다.

### 예 {#examples-2}

```
// all: js + theme (theme-js + css)
{{includeClientLib categories="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/socialgraph.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/socialgraph.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// only js libs
{{includeClientLib js="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/socialgraph.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// theme only (theme-js + css)
{{includeClientLib theme="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// css only
{{includeClientLib css="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/socialgraph.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
```

## Pretty-time {#pretty-time}

시간 도우미에서 일정 날짜 형식이 표시되는 마감 지점까지 경과된 시간을 표시합니다.

예:

* 12시간 전
* 7일 전

### 매개 변수 {#parameters-8}

* **컨텍스트**:숫자

   과거에 &#39;지금&#39;에 비교할 시간입니다. 시간은 1970년 1월 1일(epoch)부터 오프셋된 밀리초 값으로 표시됩니다.

* **daysCutoff**:숫자

   실제 날짜로 전환하기 전 일 수입니다. 기본값은 60입니다.

### 예 {#example-5}

```
{{pretty-time this.published daysCutoff=7}}

/*
Depending on how long in the past, may return

  "3 minutes ago"

  "3 hours ago"

  "3 days ago"
*/
```

## Xss-html {#xss-html}

XSS를 방지하는 데 도움이 되도록 HTML 요소 컨텐츠에 대한 소스 문자열을 인코딩하는 도우미.

참고:유효성 검사기가 아니며, 특성 값을 쓰는 데 사용할 수 없습니다.

### 매개 변수 {#parameters-9}

* **컨텍스트**:개체

   인코딩할 HTML입니다.

### 예 {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

XSS를 방지하기 위해 HTML 속성 값에 쓸 소스 문자열을 인코딩하는 도우미입니다.

참고:이것은 유효성 검사기가 아니며, 실행 가능한 속성(href, src, 이벤트 핸들러)을 쓰는 데 사용할 수 없습니다.

### 매개 변수 {#parameters-10}

* **컨텍스트**:개체

   인코딩할 HTML입니다.

### 예 {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

XSS를 방지하기 위해 JavaScript 문자열 컨텐츠에 쓸 소스 문자열을 인코딩하는 도우미.

참고:유효성 검사기가 아니며, 임의 JavaScript에 쓰는 데 사용할 수 없습니다.

### 매개 변수 {#parameters-11}

* **컨텍스트**:개체

   인코딩할 HTML입니다.

### 예 {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

XSS를 방지하기 위해 HTML href 또는 srce 속성 값으로 쓸 URL을 가릴 수 있는 도우미입니다.

참고:빈 문자열을 반환할 수 있습니다

### 매개 변수 {#parameters-12}

* **컨텍스트**:개체

   가릴 URL입니다.

### 예 {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Handlebars.js 기본 개요 {#handlebars-js-basic-overview}

[Handlebars.js 설명서](https://handlebarsjs.com/expressions.html)의 도우미 기능에 대한 빠른 개요:

* Handlebars 도우미 호출은 간단한 식별자(도우미의 *name*)이며, 그 뒤에는 0개 이상의 공백으로 구분된 매개 변수가 옵니다.
* 매개 변수는 간단한 문자열, 숫자, 부울 또는 JSON 개체일 수 있으며, 마지막 매개 변수로서 선택적 키-값 쌍(해시 인수) 시퀀스가 있을 수 있습니다.
* 해시 인수의 키는 단순 식별자여야 합니다.
* 해시 인수의 값은 Handlebars 표현식입니다.단순 식별자, 경로 또는 문자열
* 현재 컨텍스트 `this`은 항상 Handlebars 도우미가 사용할 수 있습니다.
* 컨텍스트는 문자열, 숫자, 부울 또는 JSON 데이터 개체일 수 있습니다.
* 현재 컨텍스트 내에 중첩된 개체를 `this.url` 또는 `this.id` 과 같은 컨텍스트로 전달할 수 있습니다(단순 및 블록 도움말의 다음 예 참조).

* 블록 도우미는 템플릿의 모든 위치에서 호출할 수 있는 함수입니다. 매번 다른 컨텍스트에서 템플릿 블록을 0회 이상 호출할 수 있습니다. 여기에는 {{#*name*}}과 {{/*name*}} 사이의 컨텍스트가 포함됩니다.

* Handlebars는 &#39;options&#39;라는 이름의 지원자에게 최종 매개 변수를 제공합니다. 특수 개체 &#39;options&#39;에는 다음이 포함됩니다

   * 선택적 개인 데이터(options.data)
   * 호출에서 선택적 키-값 속성(options.hash)
   * 자체 호출 기능(options.fn())
   * 자체의 역수를 호출하는 기능(options.inverse())

* 도우미에서 반환된 HTML 문자열 컨텐츠는 SafeString인 것이 좋습니다.

### Handlebars.js 설명서의 간단한 도우미 예제:{#an-example-of-a-simple-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link_to', function(title, options) {
    return new Handlebars.SafeString('<a href="/posts' + this.url + '">' + title + "!</a>");
});

var context = {posts: [
    {url: "/hello-world",
      body: "Hello World!"}
  ] };

// when link_to is called, posts is the current context
var source = '<ul>{{#posts}}<li>{{{link_to "Post"}}}</li>{{/posts}}</ul>'

var template = Handlebars.compile(source);

template(context);
```

이 렌더링됩니다.

&lt;ul>
&lt;li>&lt;a href=&quot;/posts/hello-world&quot;>포스트!&lt;/a>&lt;/li>
&lt;/ul>

### Handlebars.js 설명서의 블록 도우미의 예:{#an-example-of-a-block-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link', function(options) {
    return new Handlebars.SafeString('<a href="/people/' + this.id + '">' + options.fn(this) + '</a>');
});

var data = { "people": [
  { "name": "Alan", "id": 1 },
  { "name": "Yehuda", "id": 2 }
]};

// when link is called, people is the current context
var source = "<ul>{{#people}}<li>{{#link}}{{name}}{{/link}}</li>{{/people}}</ul>";

var template = Handlebars.compile(source);

template(data);
```

이 렌더링됩니다.
&lt;ul>
&lt;li>&lt;a href=&quot;/people/1&quot;>Alan&lt;/a>&lt;/li>
&lt;li>&lt;a href=&quot;/people/2&quot;>Yhuda&lt;/a>&lt;/li>
&lt;/ul>

## 사용자 지정 SCF 도우미 {#custom-scf-helpers}

사용자 지정 도우미는 특히 데이터를 전달할 때 서버측뿐만 아니라 클라이언트측에도 구현해야 합니다. SCF의 경우, 페이지가 요청될 때 서버가 주어진 구성 요소에 대한 HTML을 생성하므로 대부분의 템플릿은 서버 측에서 컴파일되고 렌더링됩니다.

### 서버측 사용자 지정 도우미 {#server-side-custom-helpers}

서버 측에 사용자 지정 SCF 도우미를 구현하고 등록하려면 Java 인터페이스 [TemplateHelper](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html)을 구현하고 [OSGi Service](../../help/sites-developing/the-basics.md#osgi) 로 만든 다음 OSGi 번들의 일부로 설치하십시오.

예:

### FooTextHelper.java {#footexthelper-java}

```java
/** Custom Handlebars Helper */

package com.my.helpers;

import java.io.IOException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

import com.adobe.cq.social.handlebars.api.TemplateHelper;
import com.github.jknack.handlebars.Options;

@Service
@Component
public class FooTextHelper implements TemplateHelper<String>{

    @Override
    public CharSequence apply(String context, Options options) throws IOException {
        return "foo-" + context;
    }

    @Override
    public String getHelperName() {
        return "foo-text";
    }

    @Override
    public Class<String> getContextType() {
        return String.class;
    }
}
```

>[!NOTE]
>
>서버측을 위해 만들어진 도우미도 클라이언트측에 대해 만들어야 합니다.
>
>구성 요소는 로그인한 사용자에 대해 클라이언트측에서 다시 렌더링되고, 클라이언트측 도우미가 없으면 구성 요소가 사라집니다.

### 클라이언트측 사용자 지정 도우미 {#client-side-custom-helpers}

클라이언트측 도움말은 `Handlebars.registerHelper()`을 호출하여 등록된 Handlebars 스크립트입니다.
예:

### custom-helpers.js {#custom-helpers-js}

```
function(Handlebars, SCF, $CQ) {

    Handlebars.registerHelper('foo-text', function(context, options) {
        if (!context) {
            return "";
        }
        return "foo-" + context;
    });

})(Handlebars, SCF, $CQ);
```

사용자 지정 클라이언트측 도움말을 사용자 지정 클라이언트 라이브러리에 추가해야 합니다.
clientlib은 다음 조건을 충족해야 합니다.

* `cq.social.scf`에 대한 종속성을 포함하십시오.
* Handlebars가 로드된 후 로드합니다.
* [included](clientlibs.md)이어야 합니다.

참고:scf 도우미는 `/etc/clientlibs/social/commons/scf/helpers.js`에 정의됩니다.

| **[⇐ 기능 핵심 사항](essentials.md)** | **[서버 측 사용자 지정 ⇒](server-customize.md)** |
|---|---|
|  | **[클라이언트측 사용자 지정 ⇒](client-customize.md)** |
