---
title: AEM Forms 작업 영역 사용자 지정을 위한 일반 단계
seo-title: AEM Forms 작업 영역 사용자 지정을 위한 일반 단계
description: AEM Forms 작업 영역 사용자 인터페이스 사용자 정의를 시작하는 방법.
seo-description: AEM Forms 작업 영역 사용자 인터페이스 사용자 정의를 시작하는 방법.
uuid: da6310b4-1c58-468d-85c6-975fd2c141f9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: dd3218c4-2bb2-40fc-9141-5823b0ea4224
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# AEM Forms 작업 영역 사용자 지정을 위한 일반 단계{#generic-steps-for-aem-forms-workspace-customization}

사용자 지정을 수행하는 일반적인 단계는 다음과 같습니다.

1. CRXDE Lite에 액세스하여 로그인합니다 `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. 이름이 `ws`없는 경우 `/apps`에 있는 폴더를 만듭니다. 모두 **[!UICONTROL 저장을 클릭합니다]**.
1. 액세스 제어 `/apps/ws`탭으로 이동하여 **[!UICONTROL 해당 탭으로 이동합니다]** .
1. 액세스 **[!UICONTROL 제어]** 목록에서 **[!UICONTROL +]** 을 클릭하여 새 항목을 추가합니다. 다시 **[!UICONTROL +]** 클릭합니다.
1. PERM_WORKSPACE_ **USER Principal을 검색하고** 선택합니다.

   ![HTML 작업 영역을 사용자 정의하려면 일반 단계의 일부로 PERM_WORKSPACE_USER 주체를 선택합니다.](assets/perm_workspace_user.png)

1. 교감에 대한 `jcr:read` 권한 부여.
1. 모두 **[!UICONTROL 저장을 클릭합니다]**.
1. `GET.jsp` 폴더에서 `html.jsp`폴더로 `/libs/ws``/apps/ws` 및 파일을 복사합니다.
1. 폴더의 `/libs/ws/locales` 폴더를 `/apps/ws` 복사합니다. 모두 **[!UICONTROL 저장을 클릭합니다]**.
1. 아래와 같이 `GET.jsp` 파일에서 참조와 상대 경로를 업데이트하고 모두 **[!UICONTROL 저장을 클릭합니다]**.

   ```
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. CSS 사용자 정의에 대해 다음을 수행합니다.

   1. 폴더를 `/apps/ws` 탐색하고 새 폴더를 만듭니다(이름이 `css`표시됨).

   1. 폴더 `css`폴더에서 새 파일 이름을 `newStyle.css`만듭니다.

   1. Open `/apps/ws/html`.jsp and change from

   ```css
   <link lang="en" rel="stylesheet" type="text/css" href="css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/jquery-ui.css"/>
   ```

   끝

   ```css
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/newStyle.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/jquery-ui.css"/>
   ```

   >[!NOTE]
   >
   >위에서 보듯이 newStyle.css 항목 뒤에 사용자 정의 CSS 파일의 항목을 배치합니다.

1. /apps/ws/html.jsp 파일에서

   ```css
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   끝

   ```css
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. 다음을 수행합니다.

   1. 에 `js`있는 폴더를 만듭니다 `/apps/ws`. 모두 **[!UICONTROL 저장을 클릭합니다]**.

   1. 에 `libs`있는 폴더를 만듭니다 `/apps/ws/js`. 모두 **[!UICONTROL 저장을 클릭합니다]**.

   1. 에 `jqueryui`있는 폴더를 만듭니다 `/apps/ws/js/libs`. 모두 **[!UICONTROL 저장을 클릭합니다]**.

   1. 복사 `/libs/ws/js/libs/jqueryui/jquery.ui.datepicker-ja.js` 대상 `/apps/ws/js/libs/jqueryui`. 모두 **[!UICONTROL 저장을 클릭합니다]**.

1. HTML 사용자 지정에 대해 다음을 수행합니다.

   1. 아래에서 `/apps/ws/js`이름을 가진 폴더를 만듭니다 `runtime`. 모두 **[!UICONTROL 저장을 클릭합니다]**.

   1. 아래에서 `/apps/ws/js/runtime`이름을 가진 폴더를 만듭니다 `templates`. 모두 **[!UICONTROL 저장을 클릭합니다]**.

   1. 복사 `/libs/ws/js/main.js` 대상 `/apps/ws/js/main.js`.

   1. /libs/ws/js/registry.js을 에 `/apps/ws/js/registry.js`복사합니다.

1. 모두 **[!UICONTROL 저장]**, 캐시 지우기 및 AEM Forms 작업 영역 새로 고침을 클릭합니다.

   URL에 액세스하고 관리자/암호 자격 증명으로 `https://'[server]:[port]'/lc/ws` 로그인합니다. 브라우저가 로 리디렉션됩니다 `https://'[server]:[port]'/lc/apps/ws/index.html`.
