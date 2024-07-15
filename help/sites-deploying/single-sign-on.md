---
title: 단일 사인온
description: Adobe Experience Manager(AEM) 인스턴스에 대한 SSO(Single Sign-On)를 구성하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring, Security
content-type: reference
feature: Security
exl-id: 7d2e4620-c3a5-4f5a-9eb6-42a706479d41
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---

# 단일 사인온 {#single-sign-on}

SSO(Single Sign-On)를 사용하면 인증 자격 증명(사용자 이름 및 암호 등)을 한 번 제공한 후 여러 시스템에 액세스할 수 있습니다. 별도의 시스템(신뢰할 수 있는 인증자라고도 함)이 인증을 수행하고 Experience Manager에게 사용자 자격 증명을 제공합니다. Experience Manager은 사용자에 대한 액세스 권한을 확인하고 적용합니다(즉, 사용자가 액세스할 수 있는 리소스를 결정합니다).

SSO 인증 처리기 서비스(`com.adobe.granite.auth.sso.impl.SsoAuthenticationHandler`)는 신뢰할 수 있는 인증자가 제공하는 인증 결과를 처리합니다. SSO 인증 처리기는 다음 위치에서 SSO 식별자(SSID)를 특수 속성의 값으로 이 순서로 검색합니다.

1. 요청 헤더
1. 쿠키
1. 요청 매개 변수

값이 발견되면 검색이 완료되고 이 값이 사용됩니다.

다음 두 서비스를 구성하여 SSID 를 저장하는 속성의 이름을 인식합니다.

* 로그인 모듈입니다.
* SSO 인증 서비스입니다.

두 서비스에 대해 동일한 속성 이름을 지정합니다. `Repository.login`에 제공된 `SimpleCredentials`에 특성이 포함되어 있습니다. 속성의 값은 상관없고 무시되며, 속성의 존재만으로도 중요하고 검증된다.

## SSO 구성 {#configuring-sso}

AEM 인스턴스에 대한 SSO를 구성하려면 [SSO 인증 처리기](/help/sites-deploying/osgi-configuration-settings.md#adobegranitessoauthenticationhandler)를 구성합니다.

1. AEM을 사용하여 작업할 때 이러한 서비스에 대한 구성 설정을 관리할 수 있는 방법에는 몇 가지가 있습니다. 자세한 내용 및 권장 사례를 보려면 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)을 참조하십시오.

   예를 들어 NTLM 세트의 경우:

   * **경로:**(예: `/`)
   * **헤더 이름**: `LOGON_USER`
   * **ID 형식**: `^<DOMAIN>\\(.+)$`

     여기서 `<*DOMAIN*>`은(는) 고유한 도메인 이름으로 대체됩니다.

   CoSign의 경우:

   * **경로:**(예: `/`)
   * **헤더 이름**: remote_user
   * **ID 형식:** 현재 상태

   SiteMinder의 경우:

   * **경로:**(예: `/`)
   * **헤더 이름:** SM_USER
   * **ID 형식**: 현재 상태

1. SSO(Single Sign-On)가 인증을 포함하여 필요에 따라 작동하는지 확인합니다.

>[!CAUTION]
>
>SSO가 구성된 경우 사용자가 AEM에 직접 액세스할 수 없는지 확인하십시오.
>
>사용자가 SSO 시스템의 에이전트를 실행하는 웹 서버를 통과해야 하므로 어떤 사용자도 헤더, 쿠키 또는 매개 변수를 직접 전송할 수 없으므로 이러한 정보는 외부에서 전송되면 에이전트가 필터링하여 AEM에서 사용자를 신뢰할 수 있습니다.
>
>웹 서버를 통하지 않고 AEM 인스턴스에 직접 액세스할 수 있는 모든 사용자는 이름이 알려진 경우 헤더, 쿠키 또는 매개 변수를 전송하여 사용자 역할을 할 수 있습니다.
>
>또한 헤더, 쿠키 및 요청 매개 변수 이름 중 SSO 설정에 필요한 이름만 구성해야 합니다.
>

>[!NOTE]
>
>SSO(Single Sign-On)는 종종 [LDAP](/help/sites-administering/ldap-config.md)와 함께 사용됩니다.

>[!NOTE]
>
>Microsoft® IIS(인터넷 정보 서버)에서 [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)도 사용하는 경우 다음에서 추가 구성이 필요합니다.
>
>* `disp_iis.ini`
>* IIS
>
>`disp_iis.ini` 집합:
>자세한 내용은 [Microsoft® Internet Information Server에 Dispatcher 설치](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install.html#microsoft-internet-information-server)를 참조하십시오.
>
>* `servervariables=1`(IIS 서버 변수를 요청 헤더로 원격 인스턴스에 전달함)
>* `replaceauthorization=1`(&quot;Basic&quot; 이외의 &quot;Authorization&quot;이라는 헤더를 &quot;Basic&quot;에 해당하는 헤더로 바꾸기)
>
>IIS에서:
>
>* **익명 액세스 사용 안 함**
>
>* **통합 Windows 인증 사용**
>

Felix 콘솔의 **인증자** 옵션을 사용하여 콘텐츠 트리의 모든 섹션에 적용되는 인증 처리기를 확인할 수 있습니다. 예:

`http://localhost:4502/system/console/slingauth`

경로와 가장 일치하는 핸들러를 먼저 쿼리합니다. 예를 들어 `/` 경로에 대해 handler-A를 구성하고 `/content` 경로에 대해 handler-B를 구성한 경우 `/content/mypage.html`에 대한 요청이 먼저 handler-B를 쿼리합니다.

![screen_shot_2012-02-15at21006pm](assets/screen_shot_2012-02-15at21006pm.png)

### 예 {#example}

쿠키 요청(URL `http://localhost:4502/libs/wcm/content/siteadmin.html` 사용)의 경우:

```xml
GET /libs/cq/core/content/welcome.html HTTP/1.1
Host: localhost:4502
Cookie: TestCookie=admin
```

다음 구성 사용:

* **경로**: `/`

* **헤더 이름**: `TestHeader`

* **쿠키 이름**: `TestCookie`

* **매개 변수 이름**: `TestParameter`

* **ID 형식**: `AsIs`

응답은 다음과 같습니다.

```xml
HTTP/1.1 200 OK
Connection: Keep-Alive
Server: Day-Servlet-Engine/4.1.24
Content-Type: text/html;charset=utf-8
Date: Thu, 23 Aug 2012 09:58:39 GMT
Transfer-Encoding: chunked

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "https://www.w3.org/TR/html4/strict.dtd">
<html>
<head>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <title>Welcome to Adobe&reg; CQ5</title>
....
```

이는 다음 요청에도 작동합니다.
`http://localhost:4502/libs/cq/core/content/welcome.html?TestParameter=admin`

또는 다음 curl 명령을 사용하여 `TestHeader` 헤더를 `admin:`(으)로 보낼 수 있습니다
`curl -D - -H "TestHeader: admin" http://localhost:4502/libs/cq/core/content/welcome.html`

>[!NOTE]
>
>브라우저에서 요청 매개 변수를 사용할 때 CSS 없이 일부 HTML만 표시됩니다. 이것은 HTML의 모든 요청이 요청 매개 변수 없이 수행되기 때문입니다.

## AEM 로그아웃 링크 제거 {#removing-aem-sign-out-links}

SSO를 사용하는 경우 로그인 및 로그아웃이 외부에서 처리되므로 AEM의 자체 로그아웃 링크를 더 이상 적용할 수 없어 제거해야 합니다.

시작 화면의 로그아웃 링크는 다음 단계를 사용하여 제거할 수 있습니다.

1. `/apps/cq/core/components/welcome/welcome.jsp`에 `/libs/cq/core/components/welcome/welcome.jsp` 오버레이
1. jsp에서 다음 부분을 제거합니다.

   `<a href="#" onclick="signout('<%= request.getContextPath() %>');" class="signout"><%= i18n.get("sign out", "welcome screen") %>`

오른쪽 상단의 사용자 개인 메뉴에서 사용할 수 있는 로그아웃 링크를 제거하려면 다음 단계를 따르십시오.

1. `/apps/cq/ui/widgets/source/widgets/UserInfo.js`에 `/libs/cq/ui/widgets/source/widgets/UserInfo.js` 오버레이

1. 파일에서 다음 부품을 제거합니다.

   ```
   menu.addMenuItem({
       "text":CQ.I18n.getMessage("Sign out"),
       "cls": "cq-userinfo-logout",
       "handler": this.logout
   });
   menu.addSeparator();
   ```
