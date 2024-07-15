---
title: 작업에 대한 탭 맞춤화
description: LiveCycle AEM Forms 작업 영역에서 작업의 탭 이름을 맞춤화하는 방법
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# 작업에 대한 탭 맞춤화 {#customizing-tabs-for-a-task}

`Start Process` Uber 보기의 `Start Process` 구성 요소와 `ToDo` Uber 보기의 `Task Details` 구성 요소에 대한 탭 이름을 사용자 지정할 수 있습니다.

1. [AEM Forms 작업 영역 사용자 지정에 대한 일반 단계](/help/forms/using/generic-steps-html-workspace-customization.md)를 따릅니다.
1. `translation.json` 파일에서 `tabname`의 값을 변경합니다.

   예를들어 영어에 대한 `/apps/ws/locales/en-US/translation.json`을(를) 다음과 같이 변경합니다.

   * 시작 프로세스에서 시작된 작업의 경우 `"startprocess" : {}` 블록에서 다음 코드 조각을 사용하십시오.

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * 할 일 작업의 경우 `"todo" : {}` 블록의 다음 코드 조각을 사용하십시오.

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
