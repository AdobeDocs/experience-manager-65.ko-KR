---
title: AEM Forms 작업 영역 사용자 지정을 위한 일반 단계
seo-title: AEM Forms 작업 영역 사용자 지정을 위한 일반 단계
description: AEM Forms 작업 영역 사용자 인터페이스를 사용자 정의하는 방법을 참조하십시오.
seo-description: AEM Forms 작업 영역 사용자 인터페이스를 사용자 정의하는 방법을 참조하십시오.
uuid: da6310b4-1c58-468d-85c6-975fd2c141f9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: dd3218c4-2bb2-40fc-9141-5823b0ea4224
docset: aem65
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---


# AEM Forms 작업 영역 사용자 지정을 위한 일반 단계{#generic-steps-for-aem-forms-workspace-customization}

사용자 지정을 수행하는 일반적인 단계는 다음과 같습니다.

1. `https://'[server]:[port]'/lc/crx/de/index.jsp`에 액세스하여 CRXDE Lite에 로그인합니다.
1. `/apps`에 `ws`이라는 폴더가 없는 경우 폴더를 만듭니다. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.
1. `/apps/ws`으로 이동하여 **[!UICONTROL 액세스 제어]** 탭으로 이동합니다.
1. **[!UICONTROL 액세스 제어]** 목록에서 **[!UICONTROL +]**&#x200B;을 클릭하여 새 항목을 추가합니다. **[!UICONTROL +]**&#x200B;을 다시 클릭합니다.
1. **PERM_WORKSPACE_USER** 주체를 검색하고 선택합니다.

   ![HTML 작업 영역을 사용자 지정하기 위한 일반 단계의 일부로 PERM_WORKSPACE_USER 주도자를 선택합니다.](assets/perm_workspace_user.png)

1. `jcr:read` 권한을 주체에 지정합니다.
1. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.
1. `/libs/ws` 폴더의 `GET.jsp` 및 `html.jsp` 파일을 `/apps/ws` 폴더로 복사합니다.
1. `/apps/ws` 폴더의 `/libs/ws/locales` 폴더를 복사합니다. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.
1. 아래와 같이 `GET.jsp` 파일에서 참조와 상대 경로를 업데이트하고 **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

   ```javascript
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. CSS 사용자 정의에 대해서는 다음을 수행합니다.

   1. `/apps/ws` 폴더로 이동하여 `css`라는 새 폴더를 만듭니다.

   1. `css`폴더 폴더에서 `newStyle.css`라는 새 파일을 만듭니다.

   1. `/apps/ws/html`.jsp를 열고

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/jquery-ui.css"/>
   ```

   끝

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/newStyle.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/jquery-ui.css"/>
   ```

   >[!NOTE]
   >
   >위에서 보듯이 newStyle.css 항목 뒤에 사용자 정의 CSS 파일의 항목을 배치합니다.

1. /apps/ws/html.jsp 파일에서

   ```jsp
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   끝

   ```jsp
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. 다음을 수행합니다.

   1. `/apps/ws`에 `js`이라는 폴더를 만듭니다. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

   1. `/apps/ws/js`에 `libs`이라는 폴더를 만듭니다. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

   1. `/apps/ws/js/libs`에 `jqueryui`이라는 폴더를 만듭니다. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

   1. `/libs/ws/js/libs/jqueryui/jquery.ui.datepicker-ja.js`을(를) `/apps/ws/js/libs/jqueryui`에 복사합니다. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

1. HTML 사용자 정의에 대해서는 다음을 수행합니다.

   1. `/apps/ws/js` 아래에서 `runtime` 폴더를 만듭니다. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

   1. `/apps/ws/js/runtime` 아래에서 `templates` 폴더를 만듭니다. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

   1. `/libs/ws/js/main.js`을(를) `/apps/ws/js/main.js`에 복사합니다.

   1. /libs/ws/js/registry.js을 `/apps/ws/js/registry.js`에 복사합니다.

1. **[!UICONTROL 모두 저장]**&#x200B;을 클릭하고, 캐시를 지우고 AEM Forms 작업 영역을 새로 고칩니다.

   URL `https://'[server]:[port]'/lc/ws`에 액세스하고 관리자/암호 자격 증명으로 로그인합니다. 브라우저가 `https://'[server]:[port]'/lc/apps/ws/index.html`으로 리디렉션됩니다.
