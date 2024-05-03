---
title: 하나의 서버에서 두 개의 AEM Forms 작업 공간 인스턴스 호스팅
description: LC 관리자가 서로 다른 URL을 통해 액세스할 수 있는 단일 서버에 두 개의 인스턴스를 호스팅하도록 HTML WS를 사용자 지정할 수 있는 방법.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 32a546fc-e33f-46f9-ac3b-45eca0e12239
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---

# 하나의 서버에서 두 개의 AEM Forms 작업 공간 인스턴스 호스팅 {#hosting-two-aem-forms-workspace-instances-on-one-server}

AEM Forms의 기본 설치 및 설정을 사용하면 서버에서 하나의 AEM Forms 작업 영역만 사용할 수 있습니다. 그러나 단일 AEM Forms 서버에서 AEM Forms 작업 영역의 두 개의 다른 인스턴스를 호스팅해야 할 수 있습니다. 두 인스턴스는 다른 URL로 액세스할 수 있습니다.

AEM Forms 관리자는 작업 영역을 사용자 정의하여 두 개의 다른 URL을 만들고 동일한 서버에서 두 개의 작업 영역을 사용할 수 있도록 합니다. 이 사용자 지정 문서에서는에서 두 작업 공간에 액세스할 수 있다고 가정할 수 있습니다. `https://'[server]:[port]'/lc/ws` 및 `https://'[server]:[port]':/lc/ws2`.

다음 단계에 따라 AEM Forms 작업 영역을 구성합니다.

1. 서버에 AEM Forms 작업 공간 개발 패키지를 설치합니다. 다음을 참조하십시오 [개발 패키지](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)를 참조하십시오.
1. 에 액세스하여 CRXDE Lite에 관리자로 로그인합니다. `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. 노드를 /content에 복사하고 /content에 붙여넣습니다. 노드의 이름을 ws2로 바꿉니다. 클릭 **[!UICONTROL 모두 저장]**. 이 노드의 속성에서 값 변경 `sling:resourceType` ws2로 이동합니다. 클릭 **[!UICONTROL 모두 저장]**.

1. 폴더를 /libs에서 복사하고 /apps에 붙여넣습니다. 폴더 이름을 ws2로 바꿉니다. 클릭 **[!UICONTROL 모두 저장]**.
1. 위치 `GET.jsp` 위치: `/apps/ws2`를 사용하여 다음 코드를 변경합니다. 다음 항목 바꾸기

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

1. 위치 `registry.js` 위치: `/apps/ws2/js`, 다음 위치의 템플릿을 참조하도록 템플릿 경로 변경 `/apps/ws2/js/runtime/templates`. 다음 코드 바꾸기

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

1. 위치 `userinfo.js` 위치: `/apps/ws2/js/runtime/models` 및 `/apps/ws2/js/runtime/views`, 문자열 변경 `/lc/content/ws` 끝 `lc/content/ws2`.

1. 위치 `/apps/ws2/js/runtime/services/service.js`, 경로 변경 `getLocalizationData` 가리킬 함수 `/lc/apps/ws2/Locale.html`.

1. 을(를) 참조하려면 `pdf.html` 새 작업 영역의 경로 변경 `pdf.html` 위치: `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. 을(를) 참조하려면 `pdf.html` 새 작업 영역의 경로 변경 `pdf.html` 및 `WsNextAdapter.swf` 위치: `startprocess.html`, `taskdetails.html`, 및 `processinstancehistory.html` 위치: `/apps/ws2/js/runtime/templates`.

1. 복사 `/etc/map/ws` 폴더 및 붙여넣기 위치 `/etc/map`. 새 폴더의 이름을 ws2로 바꿉니다. 모두 저장을 클릭합니다.

1. 속성: `ws2`, 값 변경 `sling:redirect` 끝 `content/ws2`.

1. 값 변경 `sling:match` 끝 `^[^/\||]/[^/\||]/ws2$`.
