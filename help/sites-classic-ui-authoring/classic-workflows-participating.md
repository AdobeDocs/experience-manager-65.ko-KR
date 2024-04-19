---
title: 워크플로에 참여
description: 워크플로는 일반적으로 페이지나 자산에 대해 사람이 활동을 수행해야 하는 단계를 포함합니다. 워크플로는 활동을 수행할 사용자 또는 그룹을 선택하고 해당 사용자 또는 그룹에 작업 항목을 지정합니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 2f1a3a73-7a20-48c7-8f3e-54252f5fb71c
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 39%

---

# 워크플로에 참여{#participating-in-workflows}

워크플로는 일반적으로 페이지나 자산에 대해 사람이 활동을 수행해야 하는 단계를 포함합니다. 워크플로는 활동을 수행할 사용자 또는 그룹을 선택하고 해당 사용자 또는 그룹에 작업 항목을 지정합니다.

## 작업 항목 처리 중 {#processing-your-work-items}

다음 작업을 수행하여 작업 항목을 처리할 수 있습니다.

* **완료**

  워크플로가 다음 단계로 진행될 수 있도록 하는 항목을 완료할 수 있습니다.

* **위임**

  하나의 단계가 사용자에게 지정되었지만 어떠한 이유로 작업을 수행할 수 없는 경우, 다른 사용자 또는 그룹에 해당 단계를 위임할 수 있습니다.

  위임에 사용할 수 있는 사용자는 작업 항목이 지정된 사용자에게 따라 다릅니다.

   * 작업 항목이 그룹에 지정된 경우 그룹 구성원을 사용할 수 있습니다.
   * 작업 항목이 그룹에 할당된 후 사용자에게 위임된 경우 그룹 멤버와 그룹을 사용할 수 있습니다.
   * 작업 항목이 단일 사용자에게 지정된 경우에는 작업 항목을 위임할 수 없습니다.

* **뒤로 이동**

  단계 또는 일련의 단계를 반복해야 하는 경우, 다시 돌아갈 수 있습니다. 워크플로우에서 이전에 발생한 단계를 선택하여 다시 처리할 수 있습니다. 워크플로가 사용자가 지정한 단계로 돌아가서 그 단계에서부터 진행됩니다.

## 워크플로우에 참여 {#participating-in-a-workflow}

### 할당된 워크플로우 작업 알림 {#notifications-of-assigned-workflow-actions}

작업 항목이 할당되면(예: **콘텐츠 승인**) 다양한 경고 및/또는 알림이 표시됩니다.

* 다음 **상태** 웹 사이트 콘솔의 열은 페이지가 워크플로우에 있는 시기를 나타냅니다.

  ![워크플로 상태-1](assets/workflowstatus-1.png)

* 사용자 또는 사용자가 속한 그룹에 워크플로우의 일부로 작업 항목이 할당되면 해당 작업 항목이 AEM Workflow 받은 편지함에 나타납니다.

  ![workflowinbox](assets/workflowinbox.png)

### 참가자 단계 완료 {#completing-a-participant-step}

표시된 작업을 수행한 후 작업 항목을 완료할 수 있으므로 워크플로우를 계속할 수 있습니다. 다음 절차에 따라 작업 항목을 완료합니다.

1. 워크플로 단계를 선택하고 **완료** 단추를 클릭합니다.
1. 그 결과로 표시되는 대화 상자에서 **다음 단계**: 즉, 다음에 실행할 단계입니다. 드롭다운 목록에 모든 적절한 대상이 표시됩니다. A **댓글** 을 입력할 수도 있습니다.

   ![workflowcomplete](assets/workflowcomplete.png)

   나열된 단계 수는 워크플로우 모델의 디자인에 따라 다릅니다.

1. 클릭 **확인** 작업을 확인합니다.

### 참가자 단계 위임 {#delegating-a-participant-step}

다음 절차를 사용하여 작업 항목을 위임합니다.

1. 다음을 클릭합니다. **위임** 단추를 클릭합니다.
1. 대화 상자에서 드롭다운 목록을 사용하여 **사용자** 을 눌러 작업 항목을 로 위임할 수 있습니다. 다음을 추가할 수도 있습니다. **댓글**.

   ![workflowdelegate](assets/workflowdelegate.png)

1. 클릭 **확인** 작업을 확인합니다.

### 참가자 단계에서 뒤로 이동 수행 {#performing-step-back-on-a-participant-step}

다음 절차를 사용하여 뒤로 돌아갑니다.

1. 맨 위 탐색 막대에서 뒤로 이동 단추를 클릭합니다.
1. 그 결과로 나타나는 대화 상자에서 이전 단계, 즉 워크플로에서 이전에 발생한 단계이지만 다음 단계에서 실행할 단계를 선택합니다. 드롭다운 목록에 모든 적절한 대상이 표시됩니다.

   ![screen_shot_2018-08-10at155325](assets/screen_shot_2018-08-10at155325.jpg)

1. 확인 을 클릭하여 작업을 확인합니다.
