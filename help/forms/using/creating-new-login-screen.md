---
title: 로그인 화면 만들기
description: AEM Forms 작업 영역 또는 Forms Manager와 같은 LiveCycle 모듈의 로그인 페이지를 수정하는 방법
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 5cb906b6-6a3c-498c-94f5-27a9071ea934
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 3%

---

# 로그인 화면 만들기{#creating-a-new-login-screen}

AEM Forms 로그인 화면을 사용하는 모든 AEM Forms 모듈의 로그인 화면을 수정할 수 있습니다. 예를 들어 수정 사항은 Forms Manager 및 AEM Forms 작업 공간 의 로그인 화면에 모두 영향을 줍니다.

## 전제 조건 {#prerequisite}

1. 관리자 권한으로 `/lc/crx/de`에 로그인합니다.
1. 다음 작업을 수행합니다.

   1. `/apps/livecycle/core/content`에 있는 `/libs/livecycle/core/content`의 계층 구조를 복제합니다.

      동일한 (노드/폴더) 속성 및 액세스 제어를 유지합니다.

   1. 컨텐츠 폴더를 복사합니다.

      보낸 사람: `/libs/livecycle/core`

      받는 사람: `/apps/livecycle/core`.

   1. `/apps/livecycle/core` 폴더의 내용을 삭제합니다.

1. 다음 작업을 수행합니다.

   1. `/apps/livecycle/core/components/login`에 있는 `/libs/livecycle/core/components/login`의 계층 구조를 복제합니다. 동일한 (노드/폴더) 속성 및 액세스 제어를 유지합니다.

   1. 구성 요소 폴더를 `/libs/livecycle/core`에서 `/apps/livecycle/core`(으)로 복사합니다.

   1. `/apps/livecycle/core/components/login` 폴더의 내용을 삭제합니다.

### 새 로케일 추가 {#adding-a-new-locale}

1. `i18n` 폴더 복사:

   * 변환 전: `/libs/livecycle/core/components/login`
   * `/apps/livecycle/core/components/login`에

1. `i18n` 내의 폴더 중 하나를 제외한 모든 폴더를 삭제합니다. `en`.

1. `en` 폴더에서 다음 작업을 수행합니다.

   1. 지원할 로케일 이름으로 폴더 이름을 변경합니다. 예: `ar`

   1. 속성 `jcr:language` 값을 `ar` 폴더의 `ar`(으)로 변경합니다.

   >[!NOTE]
   >
   >locale이 언어-국가 코드 조합인 경우(예: `ar-DZ`) 폴더 이름과 속성 값을 `ar-DZ`(으)로 변경합니다.

1. `login.jsp` 복사:

   * 변환 전: `/libs/livecycle/core/components/login`
   * `/apps/livecycle/core/components/login`에

1. `/apps/livecycle/core/components/login/login.jsp`에 대해 다음 코드 조각을 수정합니다.

***로케일은 언어 코드입니다***

```jsp
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
```

끝

```jsp
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

```jsp
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
```

끝

```jsp
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

```jsp
   String browserLocale = "en";
   for(int i=0; i<locales.length; i++)

   To

   String browserLocale = "ar";
   for(int i=0; i<locales.length; i++)
```

### 새 텍스트 추가 또는 기존 텍스트 수정 {#adding-new-text-or-modifying-existing-text}

1. `i18n` 폴더 복사:

   * 변환 전: `/libs/livecycle/core/components/login`
   * `/apps/livecycle/core/components/login`에

1. 이제 텍스트를 변경할 노드의 `sling:message` 속성 값(원하는 로케일 코드 폴더 아래)을 수정합니다. 변환은 노드의 `sling:key` 속성 값에 언급된 키를 통해 수행됩니다.

1. 새 키-값 쌍을 추가하려면 다음 작업을 수행합니다. 다음 스크린샷에서 예를 확인하십시오.

   1. 모든 로케일 폴더에서 `sling:MessageEntry` 유형의 노드를 만들거나 기존 노드를 복사하고 이름을 바꾸십시오.
   1. `login.jsp` 복사:

      * 변환 전: `/libs/livecycle/core/components/login`

      * `/apps/livecycle/core/components/login`에

   1. `/apps/livecycle/core/components/login/login.jsp`을(를) 수정하여 새로 추가된 텍스트를 통합합니다.

   ![새 키-값 쌍 추가](assets/capture_new.png)

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

   끝

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("My Welcome Message") %></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

### 새 스타일 추가 또는 기존 스타일 수정 {#adding-new-style-or-modifying-existing-style}

1. `login` 노드 복사:

   * 변환 전: `/libs/livecycle/core/content`
   * `/apps/livecycle/core/content`에

1. `/apps/livecycle/core/content/login.` 노드에서 `login.js` 및 `jquery-1.8.0.min.js` 파일을 삭제합니다.
1. CSS 파일의 스타일을 수정합니다.
1. 새 스타일을 추가하려면:

   1. `/apps/livecycle/core/content/login/login.css`에 새 스타일 추가
   1. `login.jsp` 복사

      * 변환 전: `/libs/livecycle/core/components/login`

      * `/apps/livecycle/core/components/login`에

   1. `/apps/livecycle/core/components/login/login.jsp`을(를) 수정하여 새로 추가된 스타일을 통합합니다.


예:

* `/apps/livecycle/core/content/login/login.css`에 다음 내용을 추가하십시오.

```
css.newLoginContentArea {
    width: 700px;
    padding: 100px 0px 0px 100px;
   }
```

* `/apps/livecycle/core/components/login.jsp`에서 다음을 수정합니다.


  ```jsp
  <div class="loginContentArea">
  ```

  끝

  ```jsp
  <div class="newLoginContentArea">
  ```

>[!NOTE]
>
>`/apps/livecycle/core/content/login`의 기존 이미지(`/libs/livecycle/core/content/login`에서 복사됨)가 제거되면 CSS에서 해당 참조를 제거하십시오.

### 새 이미지 추가 {#add-new-images}

1. 새 스타일을 추가하거나 기존 스타일을 수정하는 단계(위에 설명된)를 따릅니다.
1. `/apps/livecycle/core/content/login`에 새 이미지를 추가합니다. 이미지를 추가하려면:

   1. WebDAV 클라이언트를 설치합니다.
   1. webDAV 클라이언트를 사용하여 `/apps/livecycle/core/content/login` 폴더로 이동합니다. 자세한 내용은 [WebDAV 액세스](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=ko)를 참조하십시오.

   1. 새 이미지를 추가합니다.

1. `/apps/livecycle/core/content/login`에 추가된 새 이미지에 해당하는 새 스타일을 `/apps/livecycle/core/content/login/login.css,`에 추가합니다.
1. `login.jsp`의 `/apps/livecycle/core/components`에서 새 스타일을 사용합니다.

예:


```css
.newLoginContainerBkg {

 background-image: url(my_Bg.gif);
 background-repeat: no-repeat;
 background-position: left top;
 width: 727px;
}
```


    * /apps/livecycle/core/components/login.jsp에서 다음을 수정합니다.

```jsp
<div class="loginContainerBkg">
```

끝

```jsp
<div class="newLginContainerBkg">
```
