---
title: SCF Handlebars 도우미
description: SCF와 작업할 수 있도록 Handlebars 도우미 메서드
topic-tags: developing
content-type: reference
exl-id: bfb95cae-4b0f-4521-a113-042dc4005a63
source-git-commit: db0e9d6105484b37e2e21e49bf0f95cef9da2a62
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 2%

---

# SCF Handlebars 도우미 {#scf-handlebars-helpers}

| **[⇐ 기능 기본 사항](essentials.md)** | **[서버측 사용자 지정 ⇒](server-customize.md)** |
|---|---|
|   | **[클라이언트측 사용자 지정 ⇒](client-customize.md)** |

Handlebars 도우미(도우미)는 SCF 구성 요소로 작업할 수 있도록 Handlebars 스크립트에서 호출할 수 있는 메서드입니다.

구현에는 클라이언트측과 서버측 정의가 포함됩니다. 개발자가 사용자 정의 도우미를 만드는 것도 가능합니다.

AEM Communities과 함께 제공되는 사용자 지정 SCF 도우미는 [클라이언트 라이브러리](../../help/sites-developing/clientlibs.md):

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>다음을 설치하십시오. [최신 Communities 기능 팩](deploy-communities.md#latestfeaturepack).

## 약어 {#abbreviate}

maxWords 및 maxLength 속성을 따르는 축약된 문자열을 반환하는 도우미입니다.

축약할 문자열이 컨텍스트로 제공됩니다. 제공된 컨텍스트가 없으면 빈 문자열이 반환됩니다.

먼저 컨텍스트를 maxLength로 트림한 다음 컨텍스트를 단어로 잘라내고 maxWords로 줄입니다.

safeString이 true로 설정되면 반환되는 문자열은 SafeString입니다.

### 매개변수 {#parameters}

* **컨텍스트**: 문자열

  (선택 사항) 기본값은 빈 문자열입니다

* **maxLength**: 숫자

  (선택 사항) 기본값은 컨텍스트 길이입니다.

* **maxWords**: 숫자

  (선택 사항) 기본값은 트림된 문자열의 단어 수입니다.

* **safeString**: 부울

  (선택 사항) true인 경우 Handlebars.SafeString()을 반환합니다. 기본값은 false입니다.

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

## Content-loadmore {#content-loadmore}

두 보기 사이를 전환할 수 있는 기능을 사용하여 div 아래에 두 개의 범위를 추가하는 도우미. 하나는 전체 텍스트에, 다른 하나는 덜 텍스트에.

### 매개변수 {#parameters-1}

* **컨텍스트**: 문자열

  (선택 사항) 기본값은 빈 문자열입니다.

* **numChars**: 숫자

  (선택 사항) 전체 텍스트를 표시하지 않을 때 표시할 문자 수입니다. 기본값은 100입니다.

* **추가 텍스트**: 문자열

  (선택 사항) 표시할 텍스트가 더 있음을 나타내는 표시할 텍스트입니다. 기본값은 &quot;more&quot;입니다.

* **줄임표 텍스트**: 문자열

  (선택 사항) 숨겨진 텍스트를 나타내는 표시할 텍스트입니다. 기본값은 &quot;...&quot;입니다.

* **safeString**: 부울

  (선택 사항) 결과를 반환하기 전에 Handlebars.SafeString()을 적용할지 여부를 나타내는 부울 값. 기본값은 false입니다.

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

형식이 지정된 날짜 문자열을 반환하는 도우미입니다.

### 매개변수 {#parameters-2}

* **컨텍스트**: 숫자

  (선택 사항) 1970년 1월 1일부터 오프셋된 밀리초 값(epoch). 기본값은 현재 날짜입니다.

* **형식**: 문자열

  (선택 사항) 적용할 날짜 형식입니다. 기본값은 &quot;입니다.`YYYY-MM-DDTHH:mm:ss.sssZ`&quot;&quot;이고 결과는 &quot;&quot;로 표시됩니다.`2015-03-18T18:17:13-07:00`&quot;

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

같음 조건에 따라 콘텐츠를 반환할 도우미.

### 매개변수 {#parameters-3}

* **lvalue**: 문자열

  비교할 왼쪽 값입니다.

* **rvalue**: 문자열

  비교할 오른쪽 값.

### 예 {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
`{{else}}`
  <div>They are NOT equal!</div>
{{/equals}}
```

## If-wcm 모드 {#if-wcm-mode}

의 현재 값을 테스트하는 블록 도우미 [WCM 모드](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) 문자열로 구분된 모드 목록.

### 매개변수 {#parameters-4}

* **컨텍스트**: 문자열

  (선택 사항) 번역할 문자열입니다. 기본값이 제공되지 않은 경우 필수입니다.

* **모드**: 문자열

  (선택 사항) 쉼표로 구분된 목록 [WCM 모드](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) 을 클릭하여 테스트를 수행합니다.

### 예 {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{else}}
 ...
`{{/if-wcm-mode}}`
```

## i18n {#i-n}

이 헬퍼는 Handlebars 도우미 &#39;i18n&#39;을 재정의합니다.

참조: [JavaScript 코드의 문자열 다국어화](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code).

### 매개변수 {#parameters-5}

* **컨텍스트**: 문자열

  (선택 사항) 번역할 문자열입니다. 기본값이 제공되지 않은 경우 필수입니다.

* **기본값**: 문자열

  (선택 사항) 번역할 기본 문자열입니다. 제공된 컨텍스트가 없는 경우 필수입니다.

* **댓글**: 문자열

  (선택 사항) 번역 힌트

### 예 {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## 포함 {#include}

구성 요소를 템플릿에 존재하지 않는 리소스로 포함하는 도우미.

이 메서드를 사용하면 JCR 노드로 추가된 리소스에 대해 가능한 것보다 쉽게 리소스를 프로그래밍 방식으로 사용자 지정할 수 있습니다. 다음을 참조하십시오 [커뮤니티 구성 요소 추가 또는 포함](scf.md#add-or-include-a-communities-component).

일부 Communities 구성 요소만 포함할 수 있습니다. <!-- OBSOLETE/OLD  NEED TO UPDATE FOR 6.5  For AEM 6.1, those that are includable are [comments](essentials-comments.md), [rating](rating-basics.md), [reviews](reviews-basics.md), and [voting](essentials-voting.md). -->

서버측에만 적합한 이 도우미는 다음과 유사한 기능을 제공합니다. [cq:include](../../help/sites-developing/taglib.md) jsp 스크립트용

### 매개변수 {#parameters-6}

* **컨텍스트**: 문자열 또는 개체

  (상대 경로를 제공하지 않는 경우 선택 사항)

  사용 `this` 를 클릭하여 현재 컨텍스트를 전달합니다.

  사용 `this.id` 다음 위치에 리소스를 획득하려면 `id` 요청한 resourceType 렌더링에 사용됩니다.

* **resourceType**: 문자열

  (선택 사항) 리소스 유형은 기본적으로 컨텍스트의 리소스 유형으로 설정됩니다.

* **템플릿**: 문자열

  구성 요소 스크립트 경로.

* **경로**: 문자열

  (필수) 리소스 경로입니다. 경로가 상대적인 경우 컨텍스트를 제공해야 하며, 그렇지 않으면 빈 문자열이 반환됩니다.

* **작성 사용 안 함**: 부울

  (선택 사항) 기본값은 false입니다. 내부 전용입니다.

### 예 {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

다음 위치에 새 주석 구성 요소 포함 `this.id` + /comments.

## IncludeClientLib {#includeclientlib}

js, css 또는 테마 라이브러리일 수 있는 AEM html 클라이언트 라이브러리를 포함하는 도우미입니다. 다른 유형의 여러 포함(예: js 및 css)의 경우 Handlebars 스크립트에서 이 태그를 여러 번 사용해야 합니다.

서버측에만 적합한 이 도우미는 다음과 유사한 기능을 제공합니다. [ui:includeClientLib](../../help/sites-developing/taglib.md) jsp 스크립트용

### 매개변수 {#parameters-7}

* **카테고리**: 문자열

  (선택 사항) 쉼표로 구분된 클라이언트 라이브러리 범주의 목록입니다. 지정된 범주에 대한 모든 JavaScript 및 CSS 라이브러리를 포함합니다. 요청에서 테마 이름이 추출됩니다.

* **테마**: 문자열

  (선택 사항) 쉼표로 구분된 클라이언트 라이브러리 범주의 목록입니다. 지정된 카테고리에 대한 모든 테마 관련 라이브러리(CSS 및 JS 모두)를 포함합니다. 요청에서 테마 이름이 추출됩니다.

* **js**: 문자열

  (선택 사항) 쉼표로 구분된 클라이언트 라이브러리 범주의 목록입니다. 지정된 범주에 대한 모든 JavaScript 라이브러리를 포함합니다.

* **css**: 문자열

  (선택 사항) 쉼표로 구분된 클라이언트 라이브러리 범주의 목록입니다. 지정된 카테고리의 모든 CSS 라이브러리를 포함합니다.

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

## 프리타임 {#pretty-time}

컷오프 시점까지 경과된 시간을 표시하는 헬퍼이며, 그 후 정규 날짜 형식이 표시됩니다.

예:

* 12시간 전
* 7일 전

### 매개변수 {#parameters-8}

* **컨텍스트**: 숫자

  &#39;지금&#39;에 비교하기 위한 과거의 시간. 시간은 1970년 1월 1일(epoch)부터 오프셋된 밀리초의 값으로 표현된다.

* **daysCut**: 숫자

  실제 날짜로 전환하기 전 일 수. 기본값은 60입니다.

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

XSS를 방지하는 데 도움이 되도록 HTML 요소 컨텐츠에 대한 소스 문자열을 인코딩하는 도우미입니다.

참고: 이 헬퍼는 유효성 검사기가 아니므로 속성 값을 작성하는 데 사용할 수 없습니다.

### 매개변수 {#parameters-9}

* **컨텍스트**: 개체

  인코딩할 HTML.

### 예 {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

XSS를 방지하기 위해 HTML 속성 값에 쓰기 위한 소스 문자열을 인코딩하는 도우미입니다.

참고: 이 헬퍼는 유효성 검사기가 아니므로 실행 가능한 속성(href, src, 이벤트 핸들러)을 작성하는 데 사용할 수 없습니다.

### 매개변수 {#parameters-10}

* **컨텍스트**: 개체

  인코딩할 HTML.

### 예 {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

XSS를 방지하는 데 도움이 되도록 JavaScript 문자열 컨텐츠에 작성하기 위한 소스 문자열을 인코딩하는 도우미입니다.

참고: 이 헬퍼는 유효성 검사기가 아니며 임의의 JavaScript에 쓰는 데 사용할 수 없습니다.

### 매개변수 {#parameters-11}

* **컨텍스트**: 개체

  인코딩할 HTML.

### 예 {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

XSS를 방지하기 위해 HTML href 또는 소스 속성 값으로 작성하기 위한 URL을 살균하는 도우미입니다.

참고: 이 헬퍼는 빈 문자열을 반환할 수 있습니다.

### 매개변수 {#parameters-12}

* **컨텍스트**: 개체

  살균할 URL입니다.

### 예 {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Handlebars.js 기본 개요 {#handlebars-js-basic-overview}

* Handlebars 도우미 호출은 단순 식별자입니다(다음 식별자). *이름* 뒤에 0개 이상의 공백으로 구분된 매개 변수가 옵니다.
* 매개 변수는 간단한 문자열, 숫자, 부울 또는 JSON 개체일 수 있으며 마지막 매개 변수로서 키-값 쌍의 선택적 시퀀스(해시 인수)입니다.
* 해시 인수의 키는 단순 식별자여야 합니다.
* 해시 인수의 값은 단순 식별자, 경로 또는 문자열과 같은 Handlebars 표현식입니다.
* 현재 컨텍스트, `this`는 Handlebars 도우미에서 항상 사용할 수 있습니다.
* 컨텍스트는 문자열, 숫자, 부울 또는 JSON 데이터 개체일 수 있습니다.
* 현재 컨텍스트 내에 중첩된 객체를 컨텍스트로 전달할 수 있습니다. 예: `this.url` 또는 `this.id` (단순 및 블록 도우미의 다음 예 참조)

* 블록 도우미는 템플릿의 어디에서든 호출할 수 있는 함수입니다. 매번 다른 컨텍스트로 템플릿의 블록을 0회 이상 호출할 수 있습니다. 다음 사이에 컨텍스트가 포함됩니다. `{{#*name*}}` 및 `{{/*name*}}`.

* Handlebars는 &#39;options&#39;라는 도우미에 최종 매개 변수를 제공합니다. &quot;options&quot; 특수 객체에는 다음이 포함됩니다

   * 개인 데이터(선택 사항)(options.data)
   * 호출의 선택적 키 값 속성(options.hash)
   * 자체 호출 기능(options.fn())
   * 자신의 역(options.inverse())을 호출하는 기능

* 도우미에서 반환된 HTML 문자열 콘텐츠는 SafeString인 것이 좋습니다.

### Handlebars.js 설명서의 간단한 도우미의 예: {#an-example-of-a-simple-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link_to', function(title, options) {
    return new Handlebars.SafeString('<a href="/posts' + this.url + '">' + title + "!</a>");
});

var context = {posts: [
    {url: "/hello-world",
      body: "Hello World!"}
  ] };

// when link_to is called, posts is the current context
var source = '<ul>`{{#posts}}`<li>{{{link_to "Post"}}}</li>`{{/posts}}`</ul>'

var template = Handlebars.compile(source);

template(context);
```

렌더링됨:

&lt;ul>
&lt;li>&lt;a href=&quot;/posts/hello-world&quot;>게시물!&lt;/a>&lt;/li>
&lt;/ul>

### Handlebars.js 설명서의 블록 도우미의 예: {#an-example-of-a-block-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link', function(options) {
    return new Handlebars.SafeString('<a href="/people/' + this.id + '">' + options.fn(this) + '</a>');
});

var data = { "people": [
  { "name": "Alan", "id": 1 },
  { "name": "Yehuda", "id": 2 }
]};

// when link is called, people is the current context
var source = "<ul>`{{#people}}`<li>`{{#link}}``{{name}}``{{/link}}`</li>`{{/people}}`</ul>";

var template = Handlebars.compile(source);

template(data);
```

렌더링됨:
&lt;ul>
&lt;li>&lt;a href=&quot;/people/1&quot;>앨런&lt;/a>&lt;/li>
&lt;li>&lt;a href=&quot;/people/2&quot;>예후다&lt;/a>&lt;/li>
&lt;/ul>

## 사용자 지정 SCF 도우미 {#custom-scf-helpers}

특히 데이터를 전달할 때 서버측과 클라이언트측에 사용자 정의 도우미를 구현해야 합니다. SCF의 경우, 페이지가 요청될 때 서버가 주어진 구성 요소에 대한 HTML을 생성하므로 대부분의 템플릿이 서버측에서 컴파일되고 렌더링됩니다.

### 서버측 사용자 정의 도우미 {#server-side-custom-helpers}

서버측에서 사용자 지정 SCF 도우미를 구현하고 등록하려면 Java™ 인터페이스를 구현하면 됩니다 [TemplateHelper](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html), 다음 항목으로 설정 [OSGi 서비스](../../help/sites-developing/the-basics.md#osgi) OSGi 번들의 일부로 설치합니다.

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
>서버측에서 생성된 도우미는 클라이언트측에서도 생성되어야 합니다.
>
>로그인한 사용자에 대해 구성 요소가 클라이언트측에서 다시 렌더링되고, 클라이언트측 헬퍼를 찾을 수 없는 경우 구성 요소가 사라집니다.

### 클라이언트측 사용자 정의 도우미 {#client-side-custom-helpers}

클라이언트측 헬퍼는 를 호출하여 등록된 Handlebars 스크립트입니다 `Handlebars.registerHelper()`.
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

사용자 지정 클라이언트 라이브러리에 사용자 지정 클라이언트측 도우미를 추가해야 합니다.
clientlib은 다음과 같아야 합니다.

* 다음에 대한 종속성 포함 `cq.social.scf`.
* Handlebars가 로드된 후 로드합니다.
* Be [포함됨](clientlibs.md).

참고: SCF 도우미는 `/etc/clientlibs/social/commons/scf/helpers.js`.

| **[⇐ 기능 기본 사항](essentials.md)** | **[서버측 사용자 지정 ⇒](server-customize.md)** |
|---|---|
|   | **[클라이언트측 사용자 지정 ⇒](client-customize.md)** |
