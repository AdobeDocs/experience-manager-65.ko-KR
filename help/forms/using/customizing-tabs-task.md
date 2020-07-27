---
title: 작업의 탭 사용자 정의
seo-title: 작업의 탭 사용자 정의
description: LiveCycle AEM Forms 작업 영역에서 작업 탭 이름을 사용자 지정하는 방법
seo-description: LiveCycle AEM Forms 작업 영역에서 작업 탭 이름을 사용자 지정하는 방법
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# 작업의 탭 사용자 정의 {#customizing-tabs-for-a-task}

Uber 보기에서 구성 요소 `Start Process` 의 탭 이름 `Start Process` 및 Uber 보기의 `Task Details` 구성 요소 `ToDo` 를 사용자 지정할 수 있습니다.

1. AEM Forms 작업 공간 사용자 [지정에 대한 일반 단계를 따릅니다](/help/forms/using/generic-steps-html-workspace-customization.md).
1. 파일의 값 `tabname`을 `translation.json` 변경합니다.

   예를 들어 영어 `/apps/ws/locales/en-US/translation.json` 를 다음으로 변경합니다.

   * 시작 프로세스에서 시작된 작업의 경우 `"startprocess" : {}` 블록의 다음 코드 조각을 사용하십시오.

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * To-do 작업의 경우 `"todo" : {}` 블록의 다음 코드 조각을 사용하십시오.

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
   >지원되는 모든 언어에 해당하는 키-값 쌍을 추가합니다.
