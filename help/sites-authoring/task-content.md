---
title: 작업
seo-title: Working with Tasks
description: 작업은 컨텐츠에 대해 수행할 일의 항목들을 나타내며 프로젝트에서 현재 작업의 완료 수준을 판별하는 데 사용됩니다
seo-description: Tasks represent items of work to be done on content and are used in projects to determine the level of completeness of current tasks
uuid: df4efb3f-8298-4159-acfe-305ba6b46791
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: 1b79d373-73f4-4228-b309-79e74d191f3e
exl-id: a0719745-8d67-44bc-92ba-9ab07f31f8d2
source-git-commit: 200b47070b7ead54ee54eea504bd960d4e0731d9
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 41%

---


# 작업 {#working-with-tasks}

작업은 컨텐츠와 관련하여 수행할 작업 항목을 나타냅니다. 작업이 할당되면, 할당된 작업은 Workflow 받은 편지함에 나타납니다. 작업 항목은 **유형** 열.

작업은 프로젝트의 완료 수준을 판별하는 데에도 사용됩니다.

## 프로젝트 진행 상태 추적 {#tracking-project-progress}

**작업** 타일로 표시되는 프로젝트 내의 활성/완료 작업을 보고 프로젝트 진행 상태를 추적할 수 있습니다. 프로젝트 진행 상태는 다음 항목을 통해 판별할 수 있습니다.

* **작업 타일:** 프로젝트의 전체 진행 상태가 프로젝트 세부 정보 페이지에서 사용할 수 있는 작업 타일에 표시됩니다.

* **작업 목록:** 작업 타일을 클릭하면 작업 목록이 표시됩니다. This list has detailed information about all the tasks related to the project.

두 옵션 모두 작업 타일에서 직접 만드는 작업과 워크플로우 작업을 나열합니다.

### 작업 타일 {#task-tile}

프로젝트에 관련 작업이 있으면 프로젝트 내에 작업 타일이 표시됩니다. 작업 타일에는 프로젝트의 현재 상태가 표시됩니다. 이 타일은 워크플로우 내의 기존 작업을 기반으로 하며 이후에 워크플로우가 진행될 때 생성되는 작업은 포함하지 않습니다. 작업 타일에는 다음 정보가 표시됩니다.

* 완료된 작업의 비율
* 활성 작업의 비율
* 기한이 초과된 작업의 비율

![작업 타일](assets/project-tile-tasks.png)

### 프로젝트에서 작업 보기 또는 수정 {#viewing-or-modifying-the-tasks-in-a-project}

진행률 추적 외에 프로젝트에 대한 자세한 정보를 보거나 수정할 수도 있습니다.

#### 작업 목록 {#task-list}

작업 타일의 오른쪽 하단에 있는 줄임표 단추를 클릭하여 프로젝트와 관련된 작업에서 필터링된 받은 편지함을 표시합니다. 기한, 할당자, 우선 순위 및 상태와 같은 메타데이터와 함께 작업 세부 사항이 표시됩니다.

![프로젝트 작업 받은 편지함](assets/project-tasks.png)

#### 작업 세부 사항 {#task-details}

특정 작업에 대한 자세한 내용을 보려면 받은 편지함에서 작업을 탭하거나 클릭하여 선택하고 탭하거나 클릭합니다 **열기** 클릭합니다.

![작업 세부 사항](assets/project-task-detail.png)

다른 탭을 통해 작업에 대한 세부 사항을 보거나 편집하거나 추가할 수 있습니다.

* **작업** - 일반 작업 정보
* **프로젝트 정보** - 작업이 연결된 프로젝트의 요약
* **워크플로우 정보** - 작업이 연결된 워크플로우의 요약(해당하는 경우)
* **댓글** - 작업 자체에 대한 일반적인 의견

### 작업 추가 {#adding-tasks}

프로젝트에 새 작업을 추가할 수 있습니다. 그런 다음 작업 타일에 나타나고 알림 받은 편지함에서 사용할 수 있으므로 처리되지 않은 작업을 인지할 수 있습니다.

작업을 추가하려면 다음을 수행하십시오.

1. 프로젝트에서 를 찾습니다 **작업** 타일
1. 타일 오른쪽 상단에 있는 아래쪽 V자형 화살표를 탭하거나 클릭하고 을 선택합니다 **작업 만들기**.
1. 에서 **작업 추가** 창에서 우선 순위, 담당자 및 기한 등의 작업 세부 정보를 제공합니다.

   ![작업 추가](assets/project-add-task.png)

1. 탭 또는 클릭 **제출**.

## 받은 편지함에서 작업 {#working-with-tasks-in-the-inbox}

프로젝트 자체에서 프로젝트 작업에 액세스하는 대신 받은 편지함에서 직접 액세스할 수 있습니다. 받은 편지함은 프로젝트 전체의 작업에 대한 개요를 제공하므로 전체 워크플로우를 이해할 수 있습니다.

받은 편지함에서 작업을 열고 작업 상태를 설정할 수 있습니다. 작업은 사용자가 속한 사용자 그룹에 할당되면 사용자의 받은 편지함에도 나타납니다. 이 경우, 그룹의 아무 구성원이나 작업을 수행하고 작업을 완료할 수 있습니다.

![받은 편지함](assets/project-inbox.png)

작업을 완료하려면 작업을 선택하고 **완료** 클릭합니다. 작업에 정보를 추가한 다음 **완료**&#x200B;를 클릭합니다. 자세한 내용은 [받은 편지함](/help/sites-authoring/inbox.md)을 참조하십시오.
