---
title: 작업에 대한 탭 사용자 정의
seo-title: 작업에 대한 탭 사용자 정의
description: AEM Forms 작업 영역에서 작업 탭 이름을 사용자 지정하는 방법
seo-description: AEM Forms 작업 영역에서 작업 탭 이름을 사용자 지정하는 방법
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# 작업 {#customizing-tabs-for-a-task} 탭 사용자 지정

`Start Process` Uber 보기의 `Start Process` 구성 요소와 `ToDo` Uber 보기의 `Task Details` 구성 요소에 대한 탭 이름을 사용자 지정할 수 있습니다.

1. AEM Forms 작업 공간 사용자 지정에 대한 [일반 절차](/help/forms/using/generic-steps-html-workspace-customization.md)를 따르십시오.
1. `translation.json` 파일에서 `tabname`의 값을 변경합니다.

   예를 들어, 영어의 `/apps/ws/locales/en-US/translation.json`을 다음과 같이 변경하십시오.

   * 시작 프로세스에서 시작된 작업의 경우 `"startprocess" : {}` 블록에서 다음 코드 조각을 사용하십시오.

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
