---
title: 작업 탭 사용자 정의
description: LiveCycle AEM Forms workspace에서 작업의 탭 이름을 사용자 정의하는 방법
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 9%
---
# 작업 탭 사용자 정의 {#customizing-tabs-for-a-task}

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
