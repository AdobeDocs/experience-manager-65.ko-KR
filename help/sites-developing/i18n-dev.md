---
title: UI 문자열 다국어화
description: Java&trade; 및 JavaScript API를 사용하면 문자열을 국제화할 수 있습니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
exl-id: bc5b1cb7-a011-42fe-8759-3c7ee3068aad
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 0%

---

# UI 문자열 다국어화 {#internationalizing-ui-strings}

Java™ 및 JavaScript API를 사용하면 다음 유형의 리소스에서 문자열을 국제화할 수 있습니다.

* Java™ 소스 파일.
* JSP 스크립트.
* 클라이언트측 라이브러리 또는 페이지 소스의 JavaScript.
* 대화 상자 및 구성 요소 구성 속성에 사용되는 JCR 노드 속성 값입니다.

다국어화 및 현지화 프로세스에 대한 개요는 [구성 요소 다국어화](/help/sites-developing/i18n.md)를 참조하십시오.

## Java™ 및 JSP 코드의 문자열 다국어화 {#internationalizing-strings-in-java-and-jsp-code}

`com.day.cq.i18n` Java™ 패키지를 사용하면 UI에 지역화된 문자열을 표시할 수 있습니다. `I18n` 클래스는 Adobe Experience Manager(AEM) 사전에서 지역화된 문자열을 검색하는 `get` 메서드를 제공합니다. `get` 메서드의 유일한 필수 매개 변수는 영어의 문자열 리터럴입니다. UI의 기본 언어는 영어입니다. 다음 예제에서는 `Search`을(를) 현지화합니다.

`i18n.get("Search");`

영어에서 문자열 식별은 ID가 문자열을 식별하고 런타임 시 문자열을 참조하는 데 사용되는 일반적인 국제화 프레임워크와 다릅니다. 영어 문자열 리터럴을 사용하면 다음과 같은 이점이 있습니다.

* 코드는 쉽게 이해할 수 있습니다.
* 기본 언어의 문자열은 항상 사용할 수 있습니다.

### 사용자 언어 확인 {#determining-the-user-s-language}

사용자가 선호하는 언어를 결정하는 방법에는 두 가지가 있습니다.

* 인증된 사용자의 경우 사용자 계정의 환경 설정에서 언어를 결정합니다.
* 요청한 페이지의 로케일.

사용자 계정의 언어 속성이 더 신뢰할 수 있으므로 선호되는 방법입니다. 그러나 이 방법을 사용하려면 사용자가 로그인해야 합니다.

#### I18n Java™ 개체 만들기 {#creating-the-i-n-java-object}

I18n 클래스는 두 개의 생성자를 제공합니다. 사용자의 기본 언어를 결정하는 방법에 따라 사용할 생성자가 결정됩니다.

사용자 계정에 지정된 언어로 문자열을 표시하려면 `com.day.cq.i18n.I18n)`을(를) 가져온 후 다음 생성자를 사용하십시오.

```java
I18n i18n = new I18n(slingRequest);
```

생성자는 `SlingHTTPRequest`을(를) 사용하여 사용자의 언어 설정을 검색합니다.

페이지 로케일을 사용하여 언어를 결정하려면 먼저 요청된 페이지의 언어에 대한 ResourceBundle 을 가져옵니다.

```java
Locale pageLang = currentPage.getLanguage(false);
ResourceBundle resourceBundle = slingRequest.getResourceBundle(pageLang);
I18n i18n = new I18n(resourceBundle);
```

#### 문자열 다국어화 {#internationalizing-a-string}

문자열을 다국어화하려면 `I18n` 개체의 `get` 메서드를 사용하십시오. `get` 메서드의 유일한 필수 매개 변수는 국제화할 문자열입니다. 문자열은 Translator 사전의 문자열과 일치합니다. get 메서드는 사전에서 문자열을 검색하고 현재 언어에 대한 번역을 반환합니다.

`get` 메서드의 첫 번째 인수는 다음 규칙을 준수해야 합니다.

* 값은 문자열 리터럴이어야 합니다. `String` 형식의 변수를 사용할 수 없습니다.
* 문자열 리터럴은 한 줄에 표현해야 합니다.
* 문자열은 대/소문자를 구분합니다.

```xml
i18n.get("Enter a search keyword");
```

#### 번역 힌트 사용 {#using-translation-hints}

국제화된 문자열의 [번역 힌트](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings)를 지정하여 사전에 있는 중복 문자열을 구분하십시오. `get` 메서드의 두 번째 선택적 매개 변수를 사용하여 번역 힌트를 제공하십시오. 번역 힌트는 사전에 있는 항목의 주석 속성과 정확히 일치해야 합니다.

예를 들어, 사전에는 `Request` 문자열이 동사로 한 번, 명사로 한 번 두 번 포함되어 있습니다. 다음 코드에는 `get` 메서드의 인수로 번역 힌트가 포함되어 있습니다.

```java
i18n.get("Request","A noun, as in a request for a web page");
```

#### 현지화된 문장에 변수 포함 {#including-variables-in-localized-sentences}

문장에 컨텍스트 의미를 만들려면 지역화된 문자열에 변수를 포함하십시오. 예를 들어 웹 애플리케이션에 로그인하면 홈 페이지에 &quot;다시 관리자를 시작합니다&quot;라는 메시지가 표시됩니다. 받은 편지함에 메시지가 두 개 있습니다.&quot; 페이지 컨텍스트에 따라 사용자 이름과 메시지 수가 결정됩니다.

[사전에서](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings) 변수가 문자열에 대괄호로 묶인 인덱스로 표시됩니다. 변수의 값을 `get` 메서드의 인수로 지정하십시오. 인수는 번역 힌트 다음에 배치되며 인덱스는 인수의 순서에 해당합니다.

```xml
i18n.get("Welcome back {0}. You have {1} messages.", "user name, number of messages", user.getDisplayName(), numItems);
```

국제화된 문자열 및 번역 힌트는 사전의 문자열 및 주석과 정확히 일치해야 합니다. 두 번째 인수로 `null` 값을 제공하여 지역화 힌트를 생략할 수 있습니다.

#### 정적 Get 메서드 사용 {#using-the-static-get-method}

`I18N` 클래스는 몇 개의 문자열을 현지화해야 하는 경우 유용한 정적 `get` 메서드를 정의합니다. 정적 메서드에는 개체의 `get` 메서드에 대한 매개 변수 외에 사용자의 기본 언어를 결정하는 방법에 따라 사용 중인 `SlingHttpRequest` 개체 또는 `ResourceBundle`이(가) 필요합니다.

* 사용자의 언어 기본 설정 사용: SlingHttpRequest 를 첫 번째 매개 변수로 제공합니다.

  `I18n.get(slingHttpRequest, "Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`
* 페이지 언어 사용: ResourceBundle을 첫 번째 매개 변수로 제공합니다.

  `I18n.get(resourceBundle,"Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`

### JavaScript 코드의 문자열 다국어화 {#internationalizing-strings-in-javascript-code}

JavaScript API를 사용하면 클라이언트의 문자열을 현지화할 수 있습니다. [Java™ 및 JSP](#internationalizing-strings-in-java-and-jsp-code) 코드와 마찬가지로 JavaScript API를 사용하면 지역화할 문자열을 식별하고 지역화 힌트를 제공하며 지역화된 문자열에 변수를 포함할 수 있습니다.

`granite.utils` [클라이언트 라이브러리 폴더](/help/sites-developing/clientlibs.md)에서 JavaScript API를 제공합니다. API를 사용하려면 페이지에 이 클라이언트 라이브러리 폴더를 포함하십시오. 지역화 함수에서 `Granite.I18n` 네임스페이스를 사용합니다.

지역화된 문자열을 제공하기 전에 `Granite.I18n.setLocale` 함수를 사용하여 로케일을 설정하십시오. 함수에는 인수로 로케일의 언어 코드가 필요합니다.

```
Granite.I18n.setLocale("fr");
```

지역화된 문자열을 표시하려면 `Granite.I18n.get` 함수를 사용하십시오.

```
Granite.I18n.get("string to localize");
```

다음 예제에서는 문자열 &quot;Welcome back&quot;을 국제화합니다.

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("string to localize", [variables], "localization hint");
```

함수 매개 변수는 Java™ I18n.get 메서드와 다릅니다.

* 첫 번째 매개 변수는 현지화할 문자열 리터럴입니다.
* 두 번째 매개 변수는 문자열 리터럴에 삽입할 값의 배열입니다.
* 세 번째 매개 변수는 현지화 힌트입니다.

다음 예제에서는 JavaScript을 사용하여 &quot;Welcome back Administrator&quot;를 현지화합니다. 받은 편지함에 메시지가 두 개 있습니다.&quot; 문장:

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("Welcome back {0}. You have {1} new messages in your inbox.", [username, numMsg], "user name, number of messages");
```

### JCR 노드에서 문자열 다국어화 {#internationalizing-strings-from-jcr-nodes}

UI 문자열은 종종 JCR 노드 속성을 기반으로 합니다. 예를 들어 페이지의 `jcr:title` 속성은 일반적으로 페이지 코드에서 `h1` 요소의 콘텐츠로 사용됩니다. `I18n` 클래스는 이러한 문자열을 현지화하는 `getVar` 메서드를 제공합니다.

다음 예제 JSP 스크립트는 저장소에서 `jcr:title` 속성을 검색하고 페이지에 지역화된 문자열을 표시합니다.

```java
<% title = properties.get("jcr:title", String.class);%>
<h1><%=i18n.getVar(title) %></h1>
```

#### JCR 노드에 대한 번역 힌트 지정 {#specifying-translation-hints-for-jcr-nodes}

Java™ API의 [번역 힌트](#using-translation-hints)와(과) 유사하게, 번역에 중복 문자열을 구별하는 번역 힌트를 제공할 수 있습니다. 번역 힌트를 국제화된 속성을 포함하는 노드의 속성으로 제공합니다. 힌트 속성의 이름은 `_commentI18n` 접미사를 사용하는 국제화된 속성 이름의 이름으로 구성됩니다.

`${prop}_commentI18n`

예를 들어 `cq:page` 노드에는 현지화되는 jcr:title 속성이 있습니다. 힌트는 jcr:title_commentI18n이라는 속성의 값으로 제공됩니다.

### 다국어화 범위 테스트 {#testing-internationalization-coverage}

UI에서 모든 문자열을 국제화했는지 테스트합니다. 다루고 있는 문자열을 보려면 사용자 언어를 zz_ZZ로 설정하고 웹 브라우저에서 UI를 엽니다. 국제화된 문자열은 다음 형식의 스텁 번역과 함께 표시됩니다.

`USR_*Default-String*_尠`

다음 이미지는 AEM 홈 페이지에 대한 스텁 번역을 보여 줍니다.

![chlimage_1](assets/chlimage_1a.jpeg)

사용자의 언어를 설정하려면 사용자 계정에 대한 환경 설정 노드의 언어 속성을 구성합니다.

사용자의 환경 설정 노드에는 다음과 같은 경로가 있습니다.

`/home/users/<letter>/<hash>/preferences`

![chlimage_1-1](assets/chlimage_1-1a.jpeg)
