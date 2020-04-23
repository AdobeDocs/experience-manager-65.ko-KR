---
title: SCF Handlebars Helpers
seo-title: SCF Handlebars Helpers
description: Handlebars Helper 메서드를 사용하여 SCF 작업 촉진
seo-description: Handlebars Helper 메서드를 사용하여 SCF 작업 촉진
uuid: 9c514199-871e-4b68-8147-2052d2eeda15
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8b6c1697-d693-41f4-8337-f41658465107
translation-type: tm+mt
source-git-commit: 0270cee1970b5b092361c2f1ad4a117795465311

---


# SCF Handlebars Helpers {#scf-handlebars-helpers}

| **[Feature ⇐ Essentials](essentials.md)** | **[서버측 맞춤화 =](server-customize.md)** |
|---|---|
|  | **[클라이언트측 맞춤화 =](client-customize.md)** |

Handlebars Helpers(helpers)는 SCF 구성 요소 작업을 용이하게 하기 위해 핸들바 스크립트에서 호출할 수 있는 메서드입니다.

구현에는 클라이언트측과 서버측 정의가 포함됩니다. 또한 개발자는 맞춤형 도움말을 만들 수 있습니다.

AEM Communities를 사용하여 배달되는 사용자 지정 SCF 도우미는 [클라이언트 라이브러리에 정의됩니다](../../help/sites-developing/clientlibs.md).

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>반드시 [최신 커뮤니티 기능 팩을](deploy-communities.md#latestfeaturepack)설치하십시오.


## 약어 {#abbreviate}

maxWords 및 maxLength 속성을 따르는 축약된 문자열을 반환하는 도우미입니다.

축약할 문자열은 컨텍스트로 제공됩니다. 제공된 컨텍스트가 없으면 빈 문자열이 반환됩니다.

먼저 컨텍스트가 maxLength로 트리밍된 다음 컨텍스트가 단어로 슬라이스되어 maxWords로 줄어듭니다.

safeString이 true로 설정된 경우 반환된 문자열은 SafeString입니다.

### 매개 변수 {#parameters}

* **컨텍스트**:문자열

   (선택 사항) 기본값은 빈 문자열입니다.

* **maxLength**:숫자

   (선택 사항) 기본값은 컨텍스트의 길이입니다.

* **maxWords**:숫자

   (선택 사항) 기본값은 트리밍된 문자열의 단어 수입니다.

* **safeString**:부울

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

## 컨텐츠 추가 {#content-loadmore}

두 보기 사이를 전환할 수 있는 기능을 사용하여 div 아래에 두 개의 범위를 추가하는 도우미, 하나는 전체 텍스트에 대해, 다른 하나는 적은 텍스트에 대해 추가합니다.

### 매개 변수 {#parameters-1}

* **컨텍스트**:문자열

   (선택 사항) 기본값은 빈 문자열입니다.

* **numChars**:숫자

   (선택 사항) 전체 텍스트를 표시하지 않을 때 표시할 문자 수입니다. 기본값은 100입니다.

* **moreText**:문자열

   (선택 사항) 표시할 텍스트가 더 있음을 나타내는 텍스트입니다. 기본값은 &quot;more&quot;입니다.

* **ellipsesText**:문자열

   (선택 사항) 숨겨진 텍스트가 있음을 나타내는 표시할 텍스트입니다. 기본값은 &quot;...&quot;입니다.

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

형식이 지정된 날짜 문자열을 반환하는 도우미입니다.

### 매개 변수 {#parameters-2}

* **컨텍스트**:숫자

   (선택 사항) 1970년 1월 1일(epoch)부터 초 값 오프셋입니다. 기본값은 현재 날짜입니다.

* **형식**:문자열

   (선택 사항) 적용할 날짜 형식입니다. 기본값은 &quot;YYYY-MM-DDTHH:mm:ss.ssZ&quot;이며 그 결과는 &quot;2015-03-18T18:17:13-07:00&quot;으로 나타납니다.

### 예 {#examples-1}

```
{{dateUtil this.memberSince format="dd MMM yyyy, hh:mm"}}

// returns "18 Mar 2015, 18:17"
```

```
{{dateUtil this.birthday format="MM-DD-YYYY"}}

// returns "03-18-2015"
```

## Equals {#equals}

동일도 조건에 따라 콘텐츠를 반환하는 도우미입니다.

### 매개 변수 {#parameters-3}

* **lvalue**:문자열

   비교할 왼쪽 값입니다.

* **rvalue**:문자열

   비교할 오른쪽 값.

### 예 {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
{{else}}
  <div>They are NOT equal!</div>
{{/equals}}
```

## If-wcm-mode {#if-wcm-mode}

WCM 모드의 현재 값을 [문자열로 구분된 모드](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) 목록에 대해 테스트하는 블록 도우미입니다.

### 매개 변수 {#parameters-4}

* **컨텍스트**:문자열

   (선택 사항) 변환할 문자열입니다. 기본값이 제공되지 않는 경우에 필요합니다.

* **모드**:문자열

   (선택 사항) 설정할 경우 테스트할 WCM [모드의](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) 쉼표로 구분된 목록입니다.

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

JavaScript [코드에서 문자열 국제화를 참조하십시오](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code).

### 매개 변수 {#parameters-5}

* **컨텍스트**:문자열

   (선택 사항) 변환할 문자열입니다. 기본값이 제공되지 않는 경우에 필요합니다.

* **기본값**:문자열

   (선택 사항) 변환할 기본 문자열입니다. 제공된 컨텍스트가 없는 경우 필요합니다.

* **주석**:문자열

   (선택 사항) 번역 힌트

### 예 {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## Include {#include}

템플릿에 존재하지 않는 리소스로 구성 요소를 포함할 도우미입니다.

이렇게 하면 리소스를 프로그래밍 방식으로 보다 손쉽게 사용자 정의할 수 있으므로 JCR 노드로 추가된 리소스에 대해 할 수 있습니다. 커뮤니티 [구성 요소 추가 또는 포함을 참조하십시오](scf.md#add-or-include-a-communities-component).

일부 Communities 구성 요소만 포함할 수 있습니다. AEM 6.1의 경우 [댓글](essentials-comments.md), [평점](rating-basics.md), [평가](reviews-basics.md)및 [투표 포함 가능한](essentials-voting.md)댓글입니다.

서버측에 적합한 이 도우미는 JSP 스크립트용 [cq:include](../../help/sites-developing/taglib.md) 기능과 유사한 기능을 제공합니다.

### 매개 변수 {#parameters-6}

* **컨텍스트**:문자열 또는 개체

   (선택 사항, 상대 경로를 제공하지 않는 한)

   현재 컨텍스트를 전달하는 `this` 데 사용합니다.

   요청된 resourceType을 렌더링하기 `this.id` 위해 에서 리소스를 `id` 얻는 데 사용합니다.

* **resourceType**:문자열

   (선택 사항) 리소스 유형은 컨텍스트의 리소스 유형으로 기본값이 됩니다.

* **템플릿**:문자열

   구성 요소 스크립트 경로.

* **경로**:문자열

   (필수) 리소스의 경로입니다. 경로가 상대적이면 컨텍스트를 제공해야 하며 그렇지 않으면 빈 문자열이 반환됩니다.

* **authoringDisabled**:부울

   (선택 사항) 기본값은 false입니다. 내부 전용입니다.

### 예 {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

여기에는 `this.id` + /comments에 새 주석 구성 요소가 포함됩니다.

## IncludeClientLib {#includeclientlib}

js, css 또는 테마 라이브러리가 될 수 있는 AEM html 클라이언트 라이브러리를 포함하는 도우미입니다. js 및 css와 같은 다양한 유형의 여러 포함의 경우 이 태그를 Handlebars 스크립트에서 여러 번 사용해야 합니다.

서버 쪽에만 해당하는 이 도우미는 JSP 스크립트용 [ui:includeClientLib](../../help/sites-developing/taglib.md) 기능과 유사한 기능을 제공합니다.

### 매개 변수 {#parameters-7}

* **카테고리**:문자열

   (선택 사항) 쉼표로 구분된 클라이언트 라이브러리 카테고리 목록입니다. 여기에는 지정된 범주에 대한 모든 Javascript 및 CSS 라이브러리가 포함됩니다. 요청에서 테마 이름이 추출됩니다.

* **테마**:문자열

   (선택 사항) 쉼표로 구분된 클라이언트 라이브러리 카테고리 목록입니다. 여기에는 지정된 범주에 대한 모든 테마 관련 라이브러리(CSS 및 JS 모두)가 포함됩니다. 요청에서 테마 이름이 추출됩니다.

* **js**:문자열

   (선택 사항) 쉼표로 구분된 클라이언트 라이브러리 카테고리 목록입니다. 여기에는 지정된 범주에 대한 모든 Javascript 라이브러리가 포함됩니다.

* **css**:문자열

   (선택 사항) 쉼표로 구분된 클라이언트 라이브러리 카테고리 목록입니다. 여기에는 지정된 범주에 대한 모든 CSS 라이브러리가 포함됩니다.

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

일반 날짜 형식이 표시된 이후 마감 지점까지 경과된 시간을 표시하는 도우미입니다.

예:

* 12시간 전
* 7일 전

### 매개 변수 {#parameters-8}

* **컨텍스트**:숫자

   &#39;지금&#39;과 비교할 과거의 시간. 시간은 1970년 1월 1일(epoch)부터 밀리초 값 오프셋으로 표현됩니다.

* **daysCutoff**:숫자

   실제 날짜로 전환하기 전의 일 수입니다. 기본값은 60입니다.

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

XSS를 방지하기 위해 HTML 요소 컨텐츠에 대한 소스 문자열을 인코딩하는 도우미입니다.

참고:이것은 유효성 검사기가 아니며 특성 값을 쓰는 데 사용할 수 없습니다.

### 매개 변수 {#parameters-9}

* **컨텍스트**:개체

   인코딩할 HTML입니다.

### 예 {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

XSS를 방지하기 위해 HTML 속성 값에 쓸 소스 문자열을 인코딩하는 도우미.

참고:이것은 유효성 검사기가 아니며 실행 가능한 특성(href, src, 이벤트 핸들러)을 쓰는 데 사용할 수 없습니다.

### 매개 변수 {#parameters-10}

* **컨텍스트**:개체

   인코딩할 HTML입니다.

### 예 {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

JavaScript 문자열 컨텐츠에 기록할 소스 문자열을 인코딩하여 XSS를 방지하는 데 도움이 되는 도우미입니다.

참고:이것은 유효성 검사기가 아니며 임의의 JavaScript에 쓰는 데 사용되지 않습니다.

### 매개 변수 {#parameters-11}

* **컨텍스트**:개체

   인코딩할 HTML입니다.

### 예 {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

XSS를 방지하기 위해 HTML href 또는 srce 속성 값으로 쓸 URL을 가리기 위한 도우미입니다.

참고:빈 문자열을 반환할 수 있습니다.

### 매개 변수 {#parameters-12}

* **컨텍스트**:개체

   문서의 기밀 정보 가리기 URL입니다.

### 예 {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Handlebars.js 기본 개요 {#handlebars-js-basic-overview}

Handlebars.js 설명서의 [](https://handlebarsjs.com/expressions.html)도우미 함수에 대한 빠른 개요:

* Handlebars 도우미 호출은 간단한 식별자(헬퍼 *이름* )와 0개 이상의 공백으로 구분된 매개 변수입니다.
* 매개 변수는 간단한 문자열, 숫자, 부울 또는 JSON 개체일 수 있으며 마지막 매개 변수로서 선택적 키-값 쌍(해시 인수) 시퀀스가 될 수 있습니다.
* 해시 인수의 키는 단순 식별자여야 합니다.
* 해시 인수의 값은 Handlebars 식입니다.단순 식별자, 경로 또는 문자열.
* 현재 컨텍스트는 `this`항상 핸들바 도우미가 사용할 수 있습니다.
* 컨텍스트는 문자열, 숫자, 부울 또는 JSON 데이터 객체일 수 있습니다.
* 또는 같은 현재 컨텍스트 내에 중첩된 개체를 컨텍스트로 전달할 수 `this.url` `this.id` 있습니다(단순 및 블록 도움말의 다음 예 참조).

* 블록 도우미는 템플릿의 아무 곳에서나 호출할 수 있는 함수입니다. 템플릿 블록을 매번 다른 컨텍스트에서 0회 이상 호출할 수 있습니다. 여기에는 {{#*name*}}과(와) {{/*name*}} 사이의 컨텍스트가 포함되어 있습니다.

* handlebars는 &#39;options&#39;라는 이름의 도우미에 대한 최종 매개 변수를 제공합니다. 특수 개체 &#39;options&#39;에는

   * 선택적 개인 데이터(options.data)
   * 호출의 선택적 키 값 속성(options.hash)
   * 자체 호출 기능(options.fn())
   * (options.inverse()) 자체 역함수를 호출하는 기능

* 도우미에서 반환되는 HTML 문자열 내용은 SafeString인 것이 좋습니다.

### Handlebars.js 설명서의 간단한 도우미 예: {#an-example-of-a-simple-helper-from-handlebars-js-documentation}

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

렌더링할 대상:

&lt;ul>&lt;li>&lt;a href=&quot;/posts/hello-world&quot;>게시물!&lt;/a>&lt;/li>&lt;/ul>

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
var source = "<ul>{{#people}}<li>{{#link}}{{name}}{{/link}}</li>{{/people}}</ul>";

var template = Handlebars.compile(source);

template(data);
```

렌더링할 대상:&lt;ul>&lt;li>&lt;a href=&quot;/people/1&quot;>Alan&lt;/a>&lt;/li>&lt;a href=&quot;/people/2&quot;>Yhuda&lt;/a>&lt;/li>&lt;/ul>

## 사용자 지정 SCF 도움말 {#custom-scf-helpers}

사용자 지정 도우미는 특히 데이터를 전달할 때 서버측 및 클라이언트측에서 구현되어야 합니다. SCF의 경우, 페이지가 요청될 때 서버가 해당 구성 요소에 대한 HTML을 생성하므로 대부분의 템플릿이 서버측에서 컴파일되고 렌더링됩니다.

### 서버측 사용자 지정 도우미 {#server-side-custom-helpers}

서버측에서 사용자 지정 SCF 도우미를 구현하고 등록하려면 Java 인터페이스 TemplateHelper [를](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html)구현하면 [OSGi 서비스로](../../help/sites-developing/the-basics.md#osgi) 지정하고 OSGi 번들의 일부로 설치합니다.

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
>서버측을 위해 만든 도우미도 클라이언트측에서 만들어야 합니다.
>
>구성 요소는 로그인한 사용자에 대해 클라이언트측에서 다시 렌더링되며, 클라이언트측 도우미가 없으면 구성 요소가 사라집니다.


### 클라이언트측 사용자 지정 도움말 도우미 {#client-side-custom-helpers}

클라이언트측 도우미는 호출로 등록된 핸들바 스크립트입니다 `Handlebars.registerHelper()`.
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
clientlib은 다음을 수행해야 합니다.

* 종속성을 `cq.social.scf`포함합니다.
* Handlebars가 로드된 후 로드됩니다.
* 포함되어 [있습니다](clientlibs.md).

참고:scf 도움말은 에 정의되어 `/etc/clientlibs/social/commons/scf/helpers.js`있습니다.

| **[Feature ⇐ Essentials](essentials.md)** | **[서버측 맞춤화 =](server-customize.md)** |
|---|---|
|  | **[클라이언트측 맞춤화 =](client-customize.md)** |

