---
title: 작업에 대한 탭 맞춤화
description: LiveCycle AEM Forms 작업 영역에서 작업의 탭 이름을 맞춤화하는 방법
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
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
