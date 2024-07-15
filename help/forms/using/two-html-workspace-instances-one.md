---
title: 하나의 서버에서 두 개의 AEM Forms 작업 공간 인스턴스 호스팅
description: LC 관리자가 서로 다른 URL을 통해 액세스할 수 있는 단일 서버에 두 개의 인스턴스를 호스팅하도록 HTML WS를 사용자 지정할 수 있는 방법.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 32a546fc-e33f-46f9-ac3b-45eca0e12239
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---

# 하나의 서버에서 두 개의 AEM Forms 작업 공간 인스턴스 호스팅 {#hosting-two-aem-forms-workspace-instances-on-one-server}

AEM Forms의 기본 설치 및 설정을 사용하면 서버에서 하나의 AEM Forms 작업 영역만 사용할 수 있습니다. 그러나 단일 AEM Forms 서버에서 AEM Forms 작업 영역의 두 개의 다른 인스턴스를 호스팅해야 할 수 있습니다. 두 인스턴스는 다른 URL로 액세스할 수 있습니다.

AEM Forms 관리자는 작업 영역을 사용자 정의하여 두 개의 다른 URL을 만들고 동일한 서버에서 두 개의 작업 영역을 사용할 수 있도록 합니다. 이 사용자 지정 문서에서는 `https://'[server]:[port]'/lc/ws` 및 `https://'[server]:[port]':/lc/ws2`에서 두 작업 영역에 액세스할 수 있다고 가정할 수 있습니다.

다음 단계에 따라 AEM Forms 작업 영역을 구성합니다.

1. 서버에 AEM Forms 작업 공간 개발 패키지를 설치합니다. 만들기 지침은 [개발 패키지](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)를 참조하세요.
1. `https://'[server]:[port]'/lc/crx/de/index.jsp`에 액세스하여 CRXDE Lite에 관리자로 로그인합니다.
1. 노드를 /content에 복사하고 /content에 붙여넣습니다. 노드의 이름을 ws2로 바꿉니다. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다. 이 노드의 속성에서 `sling:resourceType`의 값을 ws2로 변경합니다. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

1. 폴더를 /libs에서 복사하고 /apps에 붙여넣습니다. 폴더 이름을 ws2로 바꿉니다. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.
1. `/apps/ws2`의 `GET.jsp`에서 다음 코드를 변경합니다. 다음 항목 바꾸기

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" /><html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" />
   ```

   다음 코드를 사용하여

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. `/apps/ws2/js`의 `registry.js`에서 `/apps/ws2/js/runtime/templates`의 템플릿을 참조하도록 템플릿 경로를 변경하십시오. 다음 코드 바꾸기

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/libs/ws/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

   다음 코드를 사용하여

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/apps/ws2/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

1. `userinfo.js`(`/apps/ws2/js/runtime/models` 및 `/apps/ws2/js/runtime/views`)에서 문자열 `/lc/content/ws`을(를) `lc/content/ws2`(으)로 변경하십시오.

1. `/apps/ws2/js/runtime/services/service.js`에서 `/lc/apps/ws2/Locale.html`을(를) 가리키도록 `getLocalizationData` 함수의 경로를 변경하십시오.

1. 새 Workspace의 `pdf.html`을(를) 참조하려면 `/apps/ws2/js/runtime/views/forms/pdftaskform.js`에서 `pdf.html`의 경로를 변경하십시오.

1. 새 Workspace의 `pdf.html`을(를) 참조하려면 `/apps/ws2/js/runtime/templates`에서 `startprocess.html`, `taskdetails.html`, `processinstancehistory.html`의 `pdf.html` 및 `WsNextAdapter.swf` 경로를 변경하십시오.

1. `/etc/map/ws` 폴더를 복사하여 `/etc/map`에 붙여넣습니다. 새 폴더의 이름을 ws2로 바꿉니다. 모두 저장을 클릭합니다.

1. `ws2`의 속성에서 `sling:redirect`의 값을 `content/ws2`(으)로 변경합니다.

1. `sling:match`의 값을 `^[^/\||]/[^/\||]/ws2$`(으)로 변경합니다.
