---
title: 작업 요약 창에 정보 표시
description: AEM Forms 작업 영역에서는 작업을 요약하거나 다른 웹 페이지를 표시하도록 작업 요약 창을 구성할 수 있습니다.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 0b3087fe-a3fb-4eac-ad4b-c123526e8195
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 작업 요약 창에 정보 표시 {#displaying-information-in-the-task-summary-pane}

AEM Forms 작업 영역에서 작업을 열면 작업 요약 창에 작업 요약이 표시될 수 있습니다. 작업에 대한 이러한 추가 및 관련 정보는 AEM Forms 작업 영역의 최종 사용자에게 더 많은 가치를 부여합니다.

AEM Forms 작업 영역을 사용하면 작업 요약 창에 원하는 웹 페이지를 표시할 수 있습니다. 워크벤치를 사용하여 작업 요약 창을 표시하는 프로세스를 생성할 수 있습니다.

1. 워크벤치에서 태스크 지정 프로세스를 생성합니다. 작업 할당 작업에 대한 자세한 내용은 [Workbench 도움말](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/)의 서비스 참조 항목을 참조하십시오.

   >[!NOTE]
   >
   >TaskSummary URL이 있으면 양식 보기 대신 기본적으로 작업 요약 보기가 열립니다. 이 경우 사용자가 할당 작업에서 &#39;최대화 모드에서 양식 열기&#39; 옵션을 활성화해도 최대화 모드에서 양식이 열리지 않습니다.

1. 작업 요약 URL 필드를 구성합니다. 리터럴 값, 템플릿, 변수 또는 XPath 표현식을 지정할 수 있습니다.
1. 다음은 작업 요약 페이지에 정보를 표시하는 예제입니다.

   * `https://'[server]:[port]'/lc/crx/de`의 CRXDE Lite 환경에 로그인합니다.
   * `Create a node`**SampleSummary** ` under `/content` with type `nt:unstructured`. In the properties of this node, add `sling:resourceType` of type String and value `SampleSummary`. In the Access Control List of this node, add an entry for `PERM_WORKSPACE_USER` allowing `jcr:read` privileges.`
   * `/apps`의 `Create a folder`**SampleSummary**. `/apps/SampleSummary`의 액세스 제어 목록에서 `jcr:readprivileges`을(를) 허용하는 `PERM_WORKSPACE_USER`의 항목을 추가하십시오.
   * `Create a file `html.esp` at `/apps/SampleSummary`. For example, add the following lines in `html.esp`.`

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

   * 작업 할당 단계에서 작업 요약 URL의 값을 `/lc/content/SampleSummary.html`(으)로 설정합니다.
   * 이 작업 할당 단계와 연결된 작업이 AEM Forms 작업 영역에서 열리면 `/apps/SampleSummary`의 `html.esp`이(가) 작업 요약 창에 렌더링됩니다.
