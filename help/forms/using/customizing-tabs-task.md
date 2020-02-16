---
title: 작업에 대한 탭 사용자 정의
seo-title: 작업에 대한 탭 사용자 정의
description: LiveCycle AEM Forms 작업 영역에서 작업에 대한 탭 이름을 사용자 지정하는 방법.
seo-description: LiveCycle AEM Forms 작업 영역에서 작업에 대한 탭 이름을 사용자 지정하는 방법.
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 작업에 대한 탭 사용자 정의 {#customizing-tabs-for-a-task}

Uber 보기에서 구성 요소에 대한 탭 이름을 사용자 지정할 수 `Start Process` 있으며 `Start Process` Uber 보기에서 구성 요소를 `Task Details` 사용자 지정할 `ToDo` 수 있습니다.

1. AEM [Forms 작업 영역 사용자 지정에](/help/forms/using/generic-steps-html-workspace-customization.md)대한 일반 단계를 수행합니다.
1. 파일의 값을 `tabname`변경합니다 `translation.json` .

   예를 들어, 영어에 `/apps/ws/locales/en-US/translation.json` 대해 다음을 변경합니다.

   * 시작 프로세스에서 시작된 작업의 경우 `"startprocess" : {}` 블록의 다음 코드 조각을 사용합니다.

   ```
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * To-do 작업의 경우 `"todo" : {}` 블록의 다음 코드 조각을 사용합니다.

   ```
   "tabname" : {
               "summary" : "Bird's-eye view",
               "history" : "Past",
               "form" : "Form",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Notes"
   }
   ```

   >[!NOTE]
   >
   >지원되는 모든 언어에 해당하는 키-값 쌍을 추가합니다.

[지원 문의](https://www.adobe.com/account/sign-in.supportportal.html)
