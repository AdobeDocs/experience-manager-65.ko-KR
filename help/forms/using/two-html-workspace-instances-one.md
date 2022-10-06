---
title: 하나의 서버에서 두 개의 AEM Forms 작업 공간 인스턴스 호스팅
seo-title: Hosting two AEM Forms workspace instances on one server
description: LC 관리자가 다른 URL을 통해 액세스할 수 있는 단일 서버에서 두 개의 인스턴스를 호스팅하도록 HTML WS를 사용자 지정하는 방법
seo-description: How LC administrators can customize HTML WS to host two instances on a single server accessible via different URLs.
uuid: 0584f512-6b92-4418-b71c-93605cfa1927
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 1254a7c2-2c67-4661-803e-afd53e817916
exl-id: 32a546fc-e33f-46f9-ac3b-45eca0e12239
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 하나의 서버에서 두 개의 AEM Forms 작업 공간 인스턴스 호스팅 {#hosting-two-aem-forms-workspace-instances-on-one-server}

AEM Forms의 기본 설치 및 설정을 사용하면 서버에서 하나의 AEM Forms 작업 영역만 사용할 수 있습니다. 그러나 단일 AEM Forms 서버에 두 개의 서로 다른 AEM Forms 작업 공간 인스턴스를 호스팅해야 할 수 있습니다. 두 인스턴스는 다른 URL에서 액세스할 수 있습니다.

AEM Forms 관리자는 작업 공간을 사용자 지정하여 두 개의 서로 다른 URL을 만들고 두 개의 작업 공간을 동일한 서버에서 사용할 수 있도록 합니다. 이 사용자 지정 문서에서 두 작업 공간은 `https://'[server]:[port]'/lc/ws` 및 `https://'[server]:[port]':/lc/ws2`.

다음 단계에 따라 AEM Forms 작업 공간을 구성하십시오.

1. 서버에 AEM Forms 작업 공간의 개발 패키지를 설치합니다. 자세한 내용은 [개발 패키지](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)만들기 지침은 를 참조하십시오.
1. 관리자로 CRXDE Lite에 액세스하여 로그인합니다 `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. /content에 노드를 복사하여 /content에 붙여넣습니다. 노드 이름을 ws2로 변경합니다. 클릭 **[!UICONTROL 모두 저장]**. 이 노드의 속성에서 값을 `sling:resourceType` 를 ws2로 설정합니다. 클릭 **[!UICONTROL 모두 저장]**.

1. /libs에서 폴더를 복사하여 /apps에 붙여넣습니다. 폴더 이름을 ws2로 변경합니다. 클릭 **[!UICONTROL 모두 저장]**.
1. in `GET.jsp` at `/apps/ws2`를 설정하는 경우 다음 코드를 변경합니다. 다음 내용을 바꿉니다

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

   다음 코드와 함께

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. in `registry.js` at `/apps/ws2/js`, 템플릿 경로를 변경하여 의 템플릿을 참조합니다. `/apps/ws2/js/runtime/templates`. 다음 코드를 바꿉니다

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

   다음 코드와 함께

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

1. in `userinfo.js` at `/apps/ws2/js/runtime/models` 및 `/apps/ws2/js/runtime/views`, 문자열 변경 `/lc/content/ws` to `lc/content/ws2`.

1. in `/apps/ws2/js/runtime/services/service.js`에서 경로를 변경합니다. `getLocalizationData` 을 가리키도록 함수 `/lc/apps/ws2/Locale.html`.

1. 을 참조하려면 `pdf.html` 새 작업 공간에서 경로 변경 `pdf.html` in `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. 을 참조하려면 `pdf.html` 새 작업 공간에서 경로 변경 `pdf.html` 및 `WsNextAdapter.swf` in `startprocess.html`, `taskdetails.html`, 및 `processinstancehistory.html` at `/apps/ws2/js/runtime/templates`.

1. 복사 `/etc/map/ws` 폴더 및 붙여넣기 `/etc/map`. 새 폴더의 이름을 ws2로 변경합니다. 모두 저장을 클릭합니다.

1. 의 속성에서 `ws2`, 값 변경 `sling:redirect` to `content/ws2`.

1. 값 변경 `sling:match` to `^[^/\||]/[^/\||]/ws2$`.
