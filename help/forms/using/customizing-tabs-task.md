---
title: 작업에 대한 탭 맞춤화
seo-title: Customizing tabs for a task
description: LiveCycle AEM Forms 작업 영역에서 작업의 탭 이름을 맞춤화하는 방법
seo-description: How-to customize the names of the tabs for your tasks, in LiveCycle AEM Forms workspace.
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# 작업에 대한 탭 맞춤화 {#customizing-tabs-for-a-task}

다음에 대한 탭 이름을 사용자 지정할 수 있습니다. `Start Process` 의 구성 요소 `Start Process` Uber 보기 및 `Task Details` 의 구성 요소 `ToDo` Uber 뷰입니다.

1. 다음 [AEM Forms 작업 공간 사용자 정의에 대한 일반 단계](/help/forms/using/generic-steps-html-workspace-customization.md).
1. 값 변경 `tabname`다음에서 `translation.json` 파일.

   예: 변경 `/apps/ws/locales/en-US/translation.json` (영어) 를 참조하십시오.

   * 시작 프로세스에서 시작된 작업의 경우 `"startprocess" : {}` 차단합니다.

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * 할 일의 작업에 대해 `"todo" : {}` 차단합니다.

   ```json
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
   >지원되는 모든 언어에 대해 해당 키-값 쌍을 추가합니다.
