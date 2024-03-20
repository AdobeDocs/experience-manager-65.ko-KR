---
title: 쿠키 사용 구성
description: AEM은 쿠키가 웹 페이지와 함께 사용되는 방법을 구성하고 제어할 수 있는 서비스를 제공합니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 42e8d804-6b6a-432e-a651-940b9f45db4e
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 2%

---

# 쿠키 사용 구성{#configuring-cookie-usage}

AEM은 웹 페이지에서 쿠키가 사용되는 방법을 구성하고 제어할 수 있는 서비스를 제공합니다.

* 구성 가능한 서버측 서비스는 사용할 수 있는 쿠키 목록을 유지 관리합니다.
* JavaScript API를 사용하면 JavaScript 코드가 쿠키가 사용될 수 있는지 확인할 수 있습니다.

이 기능을 사용하여 페이지가 쿠키 사용에 대한 사용자의 동의를 준수하는지 확인하십시오.

## 허용된 쿠키 구성 {#configuring-allowed-cookies}

Adobe Granite 옵트아웃 서비스를 구성하여 웹 페이지에서 쿠키가 사용되는 방법을 지정합니다. 다음 표에서는 구성할 수 있는 속성에 대해 설명합니다.

서비스를 구성하려면 다음을 사용합니다. [웹 콘솔](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 또는 [저장소에 OSGi 구성 추가](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository). 다음 표에서는 두 가지 방법에 필요한 속성을 설명합니다. OSGi 구성의 경우 서비스 PID는 입니다. `com.adobe.granite.optout`.

| 속성 이름 (웹 콘솔) | OSGi 속성 이름 | 설명 |
|---|---|---|
| 옵트아웃 쿠키 | optout.cookies | 사용자의 장치에 존재하는 경우 사용자가 쿠키 사용에 동의하지 않았음을 나타내는 쿠키의 이름. |
| 옵트아웃 HTTP 헤더 | optout.headers | 존재하는 경우 사용자가 쿠키 사용에 동의하지 않았음을 나타내는 HTTP 헤더의 이름. |
| 화이트 리스트 쿠키 | optout.whitelist.cookies | 웹 사이트 기능에 필수적이며 사용자의 동의 없이 사용할 수 있는 쿠키 목록입니다. |

## 쿠키 사용 확인 {#validating-cookie-usage}

클라이언트측 JavaScript를 사용하여 Adobe Granite 옵트아웃 서비스를 호출하여 쿠키를 사용할 수 있는지 확인합니다. Granite.OptOutUtil JavaScript 개체를 사용하여 다음 작업을 수행합니다.

* 해당 사용자가 추적 목적으로 쿠키를 사용하는 것에 동의하지 않음을 나타내는 쿠키 이름 목록을 얻습니다.
* 사용할 수 있는 쿠키 목록을 얻습니다.
* 웹 브라우저에 사용자가 추적을 위한 쿠키 사용에 동의하지 않음을 나타내는 쿠키가 포함되어 있는지 여부를 확인합니다.
* 특정 쿠키를 사용할 수 있는지 여부를 결정합니다.

Granite.utils [클라이언트 라이브러리 폴더](/help/sites-developing/clientlibs.md#referencing-client-side-libraries) 은 Granite.OptOutUtil 개체를 제공합니다. 페이지 헤드 JSP에 다음 코드를 추가하여 JavaScript 라이브러리에 대한 링크를 포함합니다.

`<ui:includeClientLib categories="granite.utils" />`

예를 들어 다음 JavaScript 함수는 COOKIE_NAME 쿠키에 쓰기 전에 사용할 수 있는지 여부를 결정합니다.

```
function writeCookie(value){
   if (!Granite.OptOutUtil.maySetCookie("COOKIE_NAME"))
      return;
   if (value) {
      value = encodeURIComponent(value);
      document.cookie = "COOKIE_NAME=" + value;
   }
}
```

## Granite.OptOutUtil JavaScript 개체 {#the-granite-optoututil-javascript-object}

Granite.OptOutUtil을 사용하면 쿠키 사용이 허용되는지 여부를 확인할 수 있습니다.

### getCookieNames() 함수 {#getcookienames-function}

존재하는 경우 사용자가 쿠키 사용에 동의하지 않았음을 나타내는 쿠키 이름.

**매개변수**

없음.

**반환**

쿠키 이름의 배열입니다.

#### getWhitelistCookieNames() 함수 {#getwhitelistcookienames-function}

사용자의 동의에 관계없이 사용할 수 있는 쿠키의 이름입니다.

**매개변수**

없음.

**반환**

쿠키 이름의 배열입니다.

#### isOptedOut() 함수 {#isoptedout-function}

사용자의 브라우저에 쿠키 사용에 동의하지 않았음을 나타내는 쿠키가 포함되어 있는지 여부를 결정합니다.

**매개변수**

없음.

**반환**

부울 값 `true` 동의 없음을 나타내는 쿠키가 발견되고 값이 `false` 비동의를 나타내는 쿠키가 없는 경우.

### maySetCookie(cookieName) 함수 {#maysetcookie-cookiename-function}

사용자의 브라우저에서 특정 쿠키를 사용할 수 있는지 여부를 결정합니다. 이 함수는 `isOptedOut` 주어진 쿠키가 다음 목록에 포함되는지 여부를 확인하는 함수 `getWhitelistCookieNames` 함수는 를 반환합니다.

**매개변수**

* cookieName: 문자열 쿠키의 이름입니다.

**반환**

부울 값 `true` if `cookieName` 사용할 수 있음 또는 값 `false` if `cookieName` 을(를) 사용할 수 없습니다.
