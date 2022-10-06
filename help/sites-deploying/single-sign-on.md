---
title: 단일 사인온
seo-title: Single Sign On
description: AEM 인스턴스에 대한 SSO(Single Sign On)를 구성하는 방법을 배웁니다.
seo-description: Learn how to configure Single Sign On (SSO) for an AEM instance.
uuid: b8dcb28e-4604-4da5-b8dd-4e1e2cbdda18
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring, Security
content-type: reference
discoiquuid: 86e8dc12-608d-4aff-ba7a-5524f6b4eb0d
feature: Configuring
exl-id: 7d2e4620-c3a5-4f5a-9eb6-42a706479d41
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---

# 단일 사인온 {#single-sign-on}

SSO(Single Sign On)를 사용하면 사용자가 인증 자격 증명(예: 사용자 이름 및 암호)을 한 번 제공한 후 여러 시스템에 액세스할 수 있습니다. 별도의 시스템(신뢰할 수 있는 인증자)에서 인증을 수행하고 Experience Manager 자격 증명을 제공합니다. Experience Manager은 사용자에 대한 액세스 권한을 확인하고 적용합니다(즉, 사용자가 액세스할 수 있는 리소스를 결정합니다).

SSO 인증 처리기 서비스( `com.adobe.granite.auth.sso.impl.SsoAuthenticationHandler`)은 신뢰할 수 있는 인증자가 제공하는 인증 결과를 처리합니다. SSO 인증 핸들러는 이 순서로 다음 위치에 있는 특수 속성 값으로 ssid(SSO 식별자)를 검색합니다.

1. 요청 헤더
1. 쿠키
1. 요청 매개 변수

값이 있으면 검색이 완료되고 이 값이 사용됩니다.

ssid를 저장하는 속성의 이름을 인식하도록 다음 두 서비스를 구성합니다.

* 로그인 모듈입니다.
* SSO 인증 서비스입니다.

두 서비스에 대해 동일한 속성 이름을 지정해야 합니다. 속성은 `SimpleCredentials` 에 제공됩니다 `Repository.login`. 속성 값은 무관하고 무시되며, 단지 속성 존재 여부가 중요하며 확인됩니다.

## SSO 구성 {#configuring-sso}

AEM 인스턴스에 대한 SSO를 구성하려면 다음을 구성해야 합니다 [SSO 인증 처리기](/help/sites-deploying/osgi-configuration-settings.md#adobegranitessoauthenticationhandler):

1. AEM을 사용하여 작업하는 경우 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 몇 가지가 있습니다. 참조 [OSGi 구성](/help/sites-deploying/configuring-osgi.md) 자세한 내용 및 권장 지침

   예를 들어 NTLM 세트의 경우:

   * **경로:** 필요한 경우 예 `/`
   * **헤더 이름**: `LOGON_USER`
   * **ID 형식**: `^<DOMAIN>\\(.+)$`

      위치 `<*DOMAIN*>` 은 사용자의 도메인 이름으로 대체됩니다.
   CoSign의 경우:

   * **경로:** 필요한 경우 예 `/`
   * **헤더 이름**: remote_user
   * **ID 형식:** 그대로

   SiteMinder의 경우:

   * **경로:** 필요한 경우 예 `/`
   * **헤더 이름:** SM_USER
   * **ID 형식**: 그대로



1. 단일 사인온이 필요에 따라 작동하는지 확인합니다. 권한 부여 포함.

>[!CAUTION]
>
>SSO가 구성된 경우 사용자가 AEM에 직접 액세스할 수 없는지 확인합니다.
>
>SSO 시스템의 에이전트를 실행하는 웹 서버를 사용자가 통과하도록 함으로써, 에이전트가 외부로부터 전송된 경우 이러한 정보를 필터링하므로 사용자가 AEM에서 사용자를 신뢰할 수 있는 헤더, 쿠키 또는 매개 변수를 직접 전송할 수 없도록 합니다.
>
>웹 서버를 거치지 않고 직접 AEM 인스턴스에 액세스할 수 있는 모든 사용자는 이름이 알려진 경우 헤더, 쿠키 또는 매개 변수를 전송하여 어떤 사용자로도 작동할 수 있습니다.
>
>또한 헤더, 쿠키 및 요청 매개 변수 이름의 경우 SSO 설정에 필요한 항목만 구성해야 합니다.

>[!NOTE]
>
>단일 사인온은 종종 와 함께 사용됩니다 [LDAP](/help/sites-administering/ldap-config.md).

>[!NOTE]
>
>또한 [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) 는 Microsoft IIS(인터넷 정보 서버)를 사용하여 다음에 추가 구성이 필요합니다.
>
>* `disp_iis.ini`
>* IIS
>
>in `disp_iis.ini` 설정:
>자세한 내용은 [Microsoft Internet Information Server로 Dispatcher 설치](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html#microsoft-internet-information-server) 자세한 내용)
>
>* `servervariables=1` (IIS 서버 변수를 요청 헤더로 원격 인스턴스에 전달)
>* `replaceauthorization=1` (Basic이 아닌 &quot;Authorization&quot;이라는 헤더를 &quot;Basic&quot;에 해당하는 항목으로 바꿉니다.)
>
>IIS에서:
>
>* disable **익명 액세스**
>
>* 활성화 **통합 Windows 인증**
>


를 사용하여 컨텐츠 트리의 모든 섹션에 적용할 인증 핸들러를 확인할 수 있습니다 **인증자** Felix Console 옵션 예:

`http://localhost:4502/system/console/slingauth`

경로가 가장 일치하는 처리기는 먼저 쿼리됩니다. 예를 들어 경로에 대해 handler-A를 구성하는 경우 `/` 및 경로에 대한 handler-B `/content`, 및에 요청 `/content/mypage.html` 은 처리기-B를 먼저 쿼리합니다.

![screen_shot_2012-02-15at21006pm](assets/screen_shot_2012-02-15at21006pm.png)

### 예 {#example}

쿠키 요청(URL 사용) `http://localhost:4502/libs/wcm/content/siteadmin.html`):

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

다음과 같은 요청을 하는 경우에도 작동합니다.
`http://localhost:4502/libs/cq/core/content/welcome.html?TestParameter=admin`

또는 다음 curl 명령을 사용하여 `TestHeader` 헤더 대상 `admin:`
`curl -D - -H "TestHeader: admin" http://localhost:4502/libs/cq/core/content/welcome.html`

>[!NOTE]
>
>브라우저에서 요청 매개 변수를 사용하는 경우 CSS가 없는 일부 HTML만 표시됩니다. 이것은 HTML의 모든 요청이 요청 매개 변수 없이 수행되기 때문입니다.

## AEM 로그아웃 링크 제거 {#removing-aem-sign-out-links}

SSO를 사용할 때 로그인 및 로그아웃이 외부에서 처리되므로 AEM 자체 로그아웃 링크를 더 이상 적용할 수 없으므로 제거해야 합니다.

시작 화면의 로그아웃 링크는 다음 단계를 사용하여 제거할 수 있습니다.

1. 오버레이 `/libs/cq/core/components/welcome/welcome.jsp` to `/apps/cq/core/components/welcome/welcome.jsp`
1. jsp에서 다음 부품을 제거합니다.

   `<a href="#" onclick="signout('<%= request.getContextPath() %>');" class="signout"><%= i18n.get("sign out", "welcome screen") %>`

오른쪽 상단 모서리의 사용자 개인 메뉴에서 사용할 수 있는 로그아웃 링크를 제거하려면 다음 단계를 수행하십시오.

1. 오버레이 `/libs/cq/ui/widgets/source/widgets/UserInfo.js` to `/apps/cq/ui/widgets/source/widgets/UserInfo.js`

1. 파일에서 다음 부품을 제거합니다.

   ```
   menu.addMenuItem({
       "text":CQ.I18n.getMessage("Sign out"),
       "cls": "cq-userinfo-logout",
       "handler": this.logout
   });
   menu.addSeparator();
   ```
