---
title: AEM Forms 작업 공간 사용자 정의에 대한 일반 단계
description: Adobe Experience Manager Forms 작업 영역 사용자 인터페이스를 맞춤화하는 방법
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 45e50b47-1b36-4937-9e1a-cc7bfb953861
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms, Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 9%

---

# AEM Forms 작업 공간 사용자 정의에 대한 일반 단계 {#generic-steps-for-aem-forms-workspace-customization}

사용자 정의를 수행하는 일반 단계는 다음과 같습니다.

1. 에 액세스하여 CRXDE Lite에 로그인 `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. 만들기 `sling:Folder` 이름이 지정된 폴더 `ws` 위치: `/apps`: 존재하지 않는 경우입니다. 을(를) 만들려면 `sling:Folder` 폴더를 마우스 오른쪽 단추로 클릭하고 `apps` 폴더 및 선택 **[!UICONTROL 만들기]** > **[!UICONTROL 노드 만들기]**. 이름을 다음으로 지정 `ws`, 다음으로 유형 선택 `sling:Folder`, 및 클릭 **[!UICONTROL 확인]**. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.
1. 다음으로 이동 `/apps/ws`로 이동한 다음 **[!UICONTROL 액세스 제어]** 탭.
1. 다음 항목 선택 **[!UICONTROL 저장소]** 옵션을 선택합니다. 다음에서 **[!UICONTROL 액세스 제어]** 목록, 클릭 **[!UICONTROL +]** 항목을 추가합니다. 클릭 **[!UICONTROL +]** 다시.
1. 검색 및 선택 **PERM_WORKSPACE_USER** 교장 선생님

   ![HTML 작업 영역을 사용자 정의하는 일반 단계의 일부로 PERM_WORKSPACE_USER 주도자를 선택합니다.](assets/perm_workspace_user.png)

1. 제공 `jcr:read` 사용자 권한.
1. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.
1. 다음을 복사합니다. `GET.jsp`, `index`, 및 `html.jsp` 파일 위치: `/libs/ws` 폴더 위치: `/apps/ws` 폴더를 삭제합니다.
1. 다음을 복사합니다. `/libs/ws/locales` 폴더의 폴더 `/apps/ws` 폴더를 삭제합니다. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.
1. 에서 참조 및 상대 경로 업데이트 `GET.jsp` 파일(아래 참조)을 클릭하고 **[!UICONTROL 모두 저장]**.

   ```javascript
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. CSS 사용자 정의에 대해 다음을 수행합니다.

   1. 다음 위치로 이동 `/apps/ws` 폴더 및 (이)라는 폴더 만들기 `css`.

   1. 다음에서 `css` 폴더, 다음 이름의 파일 만들기 `newStyle.css`.

   1. 열기 `/apps/ws/html`.jsp 및 변경

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/jquery-ui.css"/>
   ```

   대상

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/newStyle.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/jquery-ui.css"/>
   ```

   >[!NOTE]
   >
   >위에 표시된 대로 style.css 항목 뒤에 사용자 정의 CSS 파일의 항목을 배치합니다.

1. /apps/ws/html.jsp 파일에서

   ```jsp
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   대상

   ```jsp
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. 다음 작업을 수행합니다.

   1. 다음 이름의 폴더 만들기 `js` 위치: `/apps/ws`. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

   1. 다음 이름의 폴더 만들기 `libs` 위치: `/apps/ws/js`. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

   1. 복사 `/libs/ws/js/libs/jqueryui` 폴더 위치: `/apps/ws/js/libs`. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

1. HTML 사용자 정의에 대해 다음을 수행합니다.

   1. 아래 `/apps/ws/js`, 폴더 만들기 `runtime`. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

   1. 아래 `/apps/ws/js/runtime`, 폴더 만들기 `templates`. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

   1. 복사 `/libs/ws/js/main.js` 끝 `/apps/ws/js/main.js`.

   1. /libs/ws/js/registry.js을 다음으로 복사 `/apps/ws/js/registry.js`.

1. 클릭 **[!UICONTROL 모두 저장]**&#x200B;를 클릭하고 캐시를 지운 다음 AEM Forms 작업 영역을 새로 고칩니다.

   URL 액세스 `https://'[server]:[port]'/lc/ws` 관리자/암호 자격 증명으로 로그인합니다. 브라우저가 로 리디렉션됩니다. `https://'[server]:[port]'/lc/apps/ws/index.html`.
