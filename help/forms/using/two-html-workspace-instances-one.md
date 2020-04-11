---
title: 하나의 서버에서 두 개의 AEM Forms 작업 영역 인스턴스 호스팅
seo-title: 하나의 서버에서 두 개의 AEM Forms 작업 영역 인스턴스 호스팅
description: LC 관리자가 HTML WS를 사용자 지정하여 서로 다른 URL을 통해 액세스할 수 있는 단일 서버에 두 개의 인스턴스를 호스팅할 수 있는 방법입니다.
seo-description: LC 관리자가 HTML WS를 사용자 지정하여 서로 다른 URL을 통해 액세스할 수 있는 단일 서버에 두 개의 인스턴스를 호스팅할 수 있는 방법입니다.
uuid: 0584f512-6b92-4418-b71c-93605cfa1927
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 1254a7c2-2c67-4661-803e-afd53e817916
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 하나의 서버에서 두 개의 AEM Forms 작업 영역 인스턴스 호스팅 {#hosting-two-aem-forms-workspace-instances-on-one-server}

AEM Forms의 기본 설치 및 설정을 통해 서버에서 하나의 AEM Forms 작업 영역만 사용할 수 있습니다. 그러나 단일 AEM Forms 서버에 두 개의 서로 다른 AEM Forms 작업 영역 인스턴스를 호스팅해야 할 수 있습니다. 두 인스턴스는 다른 URL로 액세스할 수 있습니다.

AEM Forms 관리자는 작업 영역을 사용자 지정하여 두 개의 다른 URL을 만들고 동일한 서버에서 두 개의 작업 영역을 사용할 수 있도록 합니다. 이 사용자 지정 아티클에서는 두 작업 영역에 `https://'[server]:[port]'/lc/ws` 및 에서 액세스할 수 `https://'[server]:[port]':/lc/ws2`있다고 가정합니다.

다음 단계에 따라 AEM Forms 작업 영역을 구성합니다.

1. 서버에 AEM Forms 작업 영역의 개발 패키지를 설치합니다. 개발 [패키지를](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)만드는 방법은 개발 패키지를 참조하십시오.
1. CRXDE Lite에 액세스하여 관리자로 로그인합니다 `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. /content에 노드를 복사하고 /content에 붙여 넣습니다. 노드 이름을 ws2로 변경합니다. 모두 **[!UICONTROL 저장을 클릭합니다]**. 이 노드의 속성에서 값을 ws2 `sling:resourceType` 로 변경합니다. 모두 **[!UICONTROL 저장을 클릭합니다]**.

1. /libs에서 폴더를 복사하고 /apps에 붙여 넣습니다. 폴더 이름을 ws2로 변경합니다. 모두 **[!UICONTROL 저장을 클릭합니다]**.
1. 에서 `GET.jsp` 다음 코드를 `/apps/ws2`변경합니다. 다음 항목 바꾸기

   ```
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

   다음 코드로

   ```
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. 에서 `registry.js` 템플릿 경로를 변경하여 에서 템플릿을 `/apps/ws2/js``/apps/ws2/js/runtime/templates`참조합니다. 다음 코드 바꾸기

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

   다음 코드로

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

1. 에서 및 `userinfo.js` 에서 문자열을 `/apps/ws2/js/runtime/models` 로 `/apps/ws2/js/runtime/views``/lc/content/ws` `lc/content/ws2`변경합니다.

1. 에서 `/apps/ws2/js/runtime/services/service.js`함수의 경로를 `getLocalizationData` 다음으로 변경합니다 `/lc/apps/ws2/Locale.html`.

1. 새 `pdf.html` 작업 영역을 참조하려면 의 경로를 `pdf.html` 변경합니다 `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. 새 `pdf.html` 작업 영역을 참조하려면 의 및 의 경로를 `pdf.html` 변경하고, `WsNextAdapter.swf` 및 에서 경로를 `startprocess.html``taskdetails.html`변경합니다 `processinstancehistory.html` `/apps/ws2/js/runtime/templates`.

1. 폴더를 `/etc/map/ws` 복사하여 에 붙여넣을 수 `/etc/map`있습니다. 새 폴더의 이름을 ws2로 변경합니다. 모두 저장을 클릭합니다.

1. 의 `ws2`속성에서 값을 `sling:redirect` 로 `content/ws2`변경합니다.

1. 의 값을 `sling:match` 다음으로 `^[^/\||]/[^/\||]/ws2$`변경합니다.
