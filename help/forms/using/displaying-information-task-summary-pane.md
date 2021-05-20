---
title: 작업 요약 창에 정보 표시
seo-title: 작업 요약 창에 정보 표시
description: AEM Forms 작업 영역에서 작업을 요약하거나 다른 웹 페이지를 표시하도록 작업 요약 창을 구성할 수 있습니다.
seo-description: AEM Forms 작업 영역에서 작업을 요약하거나 다른 웹 페이지를 표시하도록 작업 요약 창을 구성할 수 있습니다.
uuid: 2fcc3d9f-0ec2-4250-8dc1-9746fd72ea60
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 90d0f584-b598-4b21-85d7-31da5f13d404
exl-id: 0b3087fe-a3fb-4eac-ad4b-c123526e8195
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# 작업 요약 창에 정보 표시 {#displaying-information-in-the-task-summary-pane}

AEM Forms 작업 영역에서 작업을 열면 작업 요약 창에 작업 요약이 표시됩니다. 이 추가 및 관련 정보는 AEM Forms workspace의 최종 사용자에게 더 많은 값을 추가합니다.

AEM Forms 작업 공간에서는 작업 요약 창에 원하는 웹 페이지를 표시할 수 있습니다. 워크벤치를 사용하여 작업 요약 창을 표시하는 프로세스를 만들 수 있습니다.

1. 워크벤치에서 태스크 지정 프로세스를 생성합니다. 작업 할당 작업에 대한 자세한 내용은 [Workbench 도움말](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/)의 서비스 참조 항목을 참조하십시오.

   >[!NOTE]
   >
   >TaskSummary URL이 있으면 Task Summary 보기가 폼 보기 대신 기본적으로 열립니다. 이 경우 사용자가 작업 할당에서 &#39;최대화된 모드로 양식 열기&#39; 옵션을 활성화해도 양식이 최대화된 모드로 열리지 않습니다.

1. 작업 요약 URL 필드를 구성합니다. 리터럴 값, 템플릿, 변수 또는 XPath 표현식을 지정할 수 있습니다.
1. 작업 요약 페이지에 정보를 표시하는 예는 다음과 같습니다.

   * `https://'[server]:[port]'/lc/crx/de`에서 CRXDE Lite 환경에 로그인합니다.
   * `Create a node`**SampleSummary** ` under `/` with type `content:`. In the properties of this node, add `unstructuredsling:` of type String and value ``. In the Access Control List of this node, add an entry for `resourceTypeSampleSummaryPERM_WORKSPACE_` allowing `USERjcr:read` privileges.`
   * `Create a folder`**** SampleSummary  `/apps`. `/apps/SampleSummary` 액세스 제어 목록에서 `jcr:readprivileges`를 허용하는 `PERM_WORKSPACE_USER`에 대한 항목을 추가합니다.
   * `Create a file `html.esp` at `/apps/`. For example, add the following lines in `SampleSummary html.esp`.`

   ```html
   <html>
       <body>
           <h1>Sample Summary</h1>
           <br/>
           <p>Hello Sir!
               <br/>
               This is sample summary page for this task.
           </p>
       </body>
   </html>
   ```

   * 작업 할당 단계에서 작업 요약 url 값을 `/lc/content/SampleSummary.html` 로 설정합니다.
   * 이 작업 할당 단계와 연결된 작업이 AEM Forms 작업 영역에서 열리면 `/apps/SampleSummary`의 `html.esp`이 작업 요약 창에 렌더링됩니다.
