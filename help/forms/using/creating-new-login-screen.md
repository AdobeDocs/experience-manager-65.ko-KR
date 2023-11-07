---
title: 로그인 화면 만들기
description: AEM Forms 작업 영역 또는 Forms Manager와 같은 LiveCycle 모듈의 로그인 페이지를 수정하는 방법
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 5cb906b6-6a3c-498c-94f5-27a9071ea934
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 7%

---

# 로그인 화면 만들기{#creating-a-new-login-screen}

AEM Forms 로그인 화면을 사용하는 모든 AEM Forms 모듈의 로그인 화면을 수정할 수 있습니다. 예를 들어 수정 사항은 Forms Manager 및 AEM Forms 작업 공간 의 로그인 화면에 모두 영향을 줍니다.

## 전제 조건 {#prerequisite}

1. 에 로그인합니다 `/lc/crx/de` 관리자 권한으로.
1. 다음 작업을 수행합니다.

   1. 계층 구조 복제: / `/libs/livecycle/core/content` 위치: `/apps/livecycle/core/content`.

      동일한 (노드/폴더) 속성 및 액세스 제어를 유지합니다.

   1. 컨텐츠 폴더를 복사합니다.

      시작: `/libs/livecycle/core`

      끝: `/apps/livecycle/core`.

   1. 콘텐츠 삭제 `/apps/livecycle/core` 폴더를 삭제합니다.

1. 다음 작업을 수행합니다.

   1. 계층 구조 복제: / `/libs/livecycle/core/components/login` 위치: `/apps/livecycle/core/components/login`. 동일한 (노드/폴더) 속성 및 액세스 제어를 유지합니다.

   1. 구성 요소 폴더 복사: 부터 `/libs/livecycle/core` 끝 `/apps/livecycle/core`.

   1. 폴더의 컨텐츠를 삭제합니다. `/apps/livecycle/core/components/login`.

### 새 로케일 추가 {#adding-a-new-locale}

1. 다음을 복사합니다. `i18n` 폴더:

   * 변환 전: `/libs/livecycle/core/components/login`
   * 끝 `/apps/livecycle/core/components/login`

1. 내의 모든 폴더 삭제 `i18n` 하나만 제외하고 `en`.

1. 폴더에서 `en`, 다음 작업을 수행합니다.

   1. 지원할 로케일 이름으로 폴더 이름을 변경합니다. 예: `ar`

   1. 속성 변경 `jcr:language` 값: 까지 `ar`(용) `ar` 폴더가 있어야 합니다).

   >[!NOTE]
   >
   >locale이 언어-국가 코드 조합인 경우, 예: `ar-DZ`을 클릭한 다음 폴더 이름 및 속성 값을 로 변경합니다. `ar-DZ`.

1. 복사 `login.jsp`:

   * 변환 전: `/libs/livecycle/core/components/login`
   * 끝 `/apps/livecycle/core/components/login`

1. 다음에 대한 코드 조각을 수정합니다. `/apps/livecycle/core/components/login/login.jsp`:

***로케일은 언어 코드입니다.***

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

1. 복사 `i18n` 폴더:

   * 변환 전: `/libs/livecycle/core/components/login`
   * 끝 `/apps/livecycle/core/components/login`

1. 이제 속성 값을 수정합니다 `sling:message` 텍스트를 변경할 노드(원하는 로케일 코드 폴더 아래)의 입니다. 번역은 의 값에 언급된 키를 통해 수행됩니다. `sling:key` 노드의 속성입니다.

1. 새 키-값 쌍을 추가하려면 다음 작업을 수행합니다. 다음 스크린샷에서 예를 확인하십시오.

   1. 유형의 노드 만들기 `sling:MessageEntry`를 클릭하거나 모든 로케일 폴더에서 기존 노드를 복사하고 이름을 변경합니다.
   1. 복사 `login.jsp` :

      * 변환 전: `/libs/livecycle/core/components/login`

      * 끝 `/apps/livecycle/core/components/login`

   1. 수정 `/apps/livecycle/core/components/login/login.jsp` 를 눌러 새로 추가된 텍스트를 통합합니다.

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

1. 복사 `login` 노드:

   * 변환 전: `/libs/livecycle/core/content`
   * 끝 `/apps/livecycle/core/content`

1. 파일 삭제 `login.js` 및 `jquery-1.8.0.min.js`: 노드에서 `/apps/livecycle/core/content/login.`
1. CSS 파일의 스타일을 수정합니다.
1. 새 스타일을 추가하려면:

   1. 새 스타일 추가 `/apps/livecycle/core/content/login/login.css`
   1. 복사 `login.jsp`

      * 변환 전: `/libs/livecycle/core/components/login`

      * 끝 `/apps/livecycle/core/components/login`

   1. 수정 `/apps/livecycle/core/components/login/login.jsp` 새로 추가된 스타일을 통합합니다.


예:

* 다음에 추가 `/apps/livecycle/core/content/login/login.css`.

```
css.newLoginContentArea {
    width: 700px;
    padding: 100px 0px 0px 100px;
   }
```

* 에서 다음 수정 `/apps/livecycle/core/components/login.jsp`.


  ```jsp
  <div class="loginContentArea">
  ```

  끝

  ```jsp
  <div class="newLoginContentArea">
  ```

>[!NOTE]
>
>에 기존 이미지가 있는 경우 `/apps/livecycle/core/content/login` (다음에서 복사됨) `/libs/livecycle/core/content/login`)을 제거한 다음 CSS에서 해당 참조를 제거합니다.

### 새 이미지 추가 {#add-new-images}

1. 새 스타일을 추가하거나 기존 스타일을 수정하는 단계(위에 설명된)를 따릅니다.
1. 새 이미지 추가 `/apps/livecycle/core/content/login`. 이미지를 추가하려면:

   1. WebDAV 클라이언트를 설치합니다.
   1. 다음으로 이동 `/apps/livecycle/core/content/login` webDAV 클라이언트를 사용하는 폴더입니다. 자세한 내용은 다음을 참조하십시오. [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ko-KR).

   1. 새 이미지를 추가합니다.

1. 에서 새 스타일 추가 `/apps/livecycle/core/content/login/login.css,` 에 추가된 새 이미지에 해당 `/apps/livecycle/core/content/login`.
1. 에서 새 스타일 사용 `login.jsp` 위치: `/apps/livecycle/core/components`.

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
