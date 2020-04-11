---
title: 새 로그인 화면 만들기
seo-title: 새 로그인 화면 만들기
description: AEM Forms 작업 영역 또는 Forms Manager와 같이 LiveCycle 모듈의 로그인 페이지를 수정하는 방법입니다.
seo-description: AEM Forms 작업 영역 또는 Forms Manager와 같이 LiveCycle 모듈의 로그인 페이지를 수정하는 방법입니다.
uuid: 2d4a72f4-cc9a-412d-856d-0fca75f1272b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 35497785-263d-44b1-9ee4-85921997295b
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 새 로그인 화면 만들기{#creating-a-new-login-screen}

AEM Forms 로그인 화면을 사용하는 모든 AEM Forms 모듈의 로그인 화면을 수정할 수 있습니다. 예를 들어 수정 사항은 Forms Manager와 AEM Forms 작업 영역의 로그인 화면에 영향을 줍니다.

## 전제 조건 {#prerequisite}

1. 관리자 권한으로 `/lc/crx/de` 로그인합니다.
1. 다음 작업을 수행합니다.

   1. 계층 구조 복제:에 `/libs/livecycle/core/content` 있는 `/apps/livecycle/core/content`경우 동일한(노드/폴더) 속성과 액세스 제어를 유지 관리합니다.

   1. 콘텐트 폴더 복사:에서 `/libs/livecycle/core` 로 `/apps/livecycle/core`이동

   1. 폴더의 컨텐츠를 `/apps/livecycle/core` 삭제합니다.

1. 다음 작업을 수행합니다.

   1. 계층 구조 복제:에 `/libs/livecycle/core/components/login` 있는 `/apps/livecycle/core/components/login`경우 동일한(노드/폴더) 속성과 액세스 제어를 유지 관리합니다.

   1. 구성 요소 폴더를 복사합니다.에서 `/libs/livecycle/core` 로 `/apps/livecycle/core`이동

   1. 폴더의 컨텐츠를 삭제합니다. `/apps/livecycle/core/components/login`Adobe

### 새 로케일 추가 {#adding-a-new-locale}

1. 폴더 `i18n` 복사:

   * 시작 시간:`/libs/livecycle/core/components/login`
   * 끝 `/apps/livecycle/core/components/login`

1. 예를 들어, 폴더 `i18n` 하나를 제외한 모든 폴더를 삭제합니다 `en`.
1. 폴더에서 다음 작업을 `en`수행합니다.

   1. 폴더의 이름을 지원할 로케일 이름으로 변경합니다. 예, `ar`.
   1. 속성 `jcr:language` 값을 `ar`( `ar` 폴더의 경우)으로 변경합니다.
   >[!NOTE]
   >
   >로케일이 언어 국가 코드 조합인 `ar-DZ`경우 폴더 이름과 속성 값을 로 변경합니다 `ar-DZ`.

1. 복사 `login.jsp`:

   * 시작 시간:`/libs/livecycle/core/components/login`
   * 끝 `/apps/livecycle/core/components/login`

1. 다음 코드 조각을 `/apps/livecycle/core/components/login/login.jsp`수정합니다.

   ***로케일은 언어 코드입니다.***

   ```
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   
   To
   
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().startsWith("ar")) {
               browserLocale = "ar";
               break;
           }
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   ```

   ***로케일은 언어 국가 코드입니다.***

   ```
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   
   To
   
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().equalsIgnoreCase("ar-DZ")) {
               browserLocale = "ar-DZ";
               break;
           }
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   ```

   ***기본 로케일을 변경하려면***

   ```
   String browserLocale = "en";
   for(int i=0; i<locales.length; i++)
   
   To
   
   String browserLocale = "ar";
   for(int i=0; i<locales.length; i++)
   ```

### 새 텍스트 추가 또는 기존 텍스트 수정 {#adding-new-text-or-modifying-existing-text}

1. 폴더 `i18n` 복사:

   * 시작 시간:`/libs/livecycle/core/components/login`
   * 끝 `/apps/livecycle/core/components/login`

1. 이제 텍스트를 변경할 노드(원하는 로케일 코드 폴더 아래) `sling:message` 의 속성 값을 수정합니다. 번역은 노드의 `sling:key` 속성 값에 언급된 키를 통해 수행됩니다.
1. 새 키-값 쌍을 추가하려면 다음 작업을 수행하십시오. 스크린샷에서 다음 예제를 확인하십시오.

   1. 모든 로케일 폴더 아래에 유형 노드를 `sling:MessageEntry`만들거나 기존 노드를 복사하여 이름을 변경합니다.
   1. 복사 `login.jsp` :

      * 시작 시간:`/libs/livecycle/core/components/login`

      * 끝 `/apps/livecycle/core/components/login`
   1. 새로 추가된 텍스트를 `/apps/livecycle/core/components/login/login.jsp` 통합하도록 수정합니다.
   ![새 키-값 쌍 추가](assets/capture_new.png)

   ```
   div class="loginContent">
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   
   To
   
   div class="loginContent">
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("My Welcome Message") %></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

### 새 스타일 추가 또는 기존 스타일 수정 {#adding-new-style-or-modifying-existing-style}

1. Copy `login` node:

   * 시작 시간:`/libs/livecycle/core/content`
   * 끝 `/apps/livecycle/core/content`

1. 파일 삭제 `login.js` 및 `jquery-1.8.0.min.js`노드에서 `/apps/livecycle/core/content/login.`
1. CSS 파일에서 스타일을 수정합니다.
1. 새 스타일을 추가하려면:

   1. 새 스타일 추가 `/apps/livecycle/core/content/login/login.css`
   1. 복사 `login.jsp`

      * 시작 시간:`/libs/livecycle/core/components/login`

      * 끝 `/apps/livecycle/core/components/login`
   1. 새로 추가된 스타일을 `/apps/livecycle/core/components/login/login.jsp` 통합하도록 수정합니다.


1. 예:

   * 다음을 `/apps/livecycle/core/content/login/login.css`추가합니다.

   ```css
   .newLoginContentArea {
    width: 700px;
    padding: 100px 0px 0px 100px;
   }
   ```

   * /apps/livecycle/core/components/login.jsp에서 다음을 수정합니다.

   ```
   <div class="loginContentArea">
   
   To
   
   <div class="newLoginContentArea">
   ```

>[!NOTE]
>
>의 기존 이미지(복사한 이미지) `/apps/livecycle/core/content/login` 가 `/libs/livecycle/core/content/login`제거되면 CSS에서 해당 참조를 제거합니다.

### 새 이미지 추가 {#add-new-images}

1. 새 스타일 추가 또는 기존 스타일 수정(위에 설명됨)의 단계를 따릅니다.
1. 에서 새 이미지를 `/apps/livecycle/core/content/login`추가합니다. 이미지를 추가하려면:

   1. WebDAV 클라이언트를 설치합니다.
   1. webDAV 클라이언트를 사용하여 `/apps/livecycle/core/content/login` 폴더로 이동합니다. 자세한 내용은 다음을 참조하십시오.https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html [](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

   1. 새 이미지 추가

1. 에 추가된 새 이미지에 `/apps/livecycle/core/content/login/login.css,` 해당하는 새 스타일을 추가할 수 `/apps/livecycle/core/content/login`있습니다.
1. 에서 새로운 스타일을 `login.jsp` 사용합니다 `/apps/livecycle/core/components`.
1. 예:

   * 다음을 `/apps/livecycle/core/content/login/login.css`

   ```css
   .newLoginContainerBkg {
    background-image: url(my_Bg.gif);
    background-repeat: no-repeat;
    background-position: left top;
    width: 727px;
   }
   ```

   * /apps/livecycle/core/components/login.jsp에서 다음을 수정합니다.

   ```
   <div class="loginContainerBkg">
   
   To
   
   <div class="newLginContainerBkg">
   ```
