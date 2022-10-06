---
title: 공유 큐 구성
seo-title: Configuring Shared Queues
description: 공유 큐를 사용하면 사용자 큐를 효과적으로 구성 및 관리할 수 있습니다. 공유 큐를 구성하는 방법을 알아봅니다.
seo-description: Shared Queues allow you to configure and manage user queues effectively. Learn how to configure shared queues.
uuid: 69ab611d-334b-40a5-bd2d-533d4cb25eda
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc403a60-b635-4334-9bf8-2f3d2036b2f3
exl-id: 5f4467c1-0f3f-4dc6-9bd5-98259f327295
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---

# 공유 큐 구성{#configuring-shared-queues}

공유 큐를 사용하면 사용자 큐를 효과적으로 구성 및 관리할 수 있습니다. 사용자 큐는 사용자에게 할당된 모든 작업입니다. [할 일 목록](https://help.adobe.com/en_US/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html) 추가 정보. 조직의 요구 사항에 따라 사용자 큐를 지정, 할당 취소 및 재할당할 수 있습니다. 다음 두 가지 방법으로 공유 큐를 관리할 수 있습니다.

**사용자에 대한 액세스 관리**

이 옵션을 사용하여 선택한 사용자 큐에 대한 액세스를 관리할 수 있습니다.

**사용자의 액세스 관리**

이 옵션을 사용하여 선택한 사용자에게 할당된 공유 큐를 관리할 수 있습니다.

## 선택한 사용자 큐에 대한 액세스 관리 {#managing-access-to-a-selected-user-queue}

사용자에 대한 액세스 관리 기능을 사용하면 선택한 사용자 큐에 대한 액세스를 관리할 수 있습니다. 선택한 사용자 큐에 대한 액세스 권한을 조직의 다른 사용자에게 부여하거나 취소할 수 있습니다. 예를 들어, 카라 보우먼이 자리를 비웠습니다. 사용자 액세스 관리 기능을 사용하여 큐를 Akura Danica 및 John Jacobs와 공유하여 완료할 수 있습니다. 나중에, 카라 보우먼이 사무실로 돌아오면, 아키라 다나카와 존 제이콥스의 그녀의 대기권에 대한 접근을 취소할 수 있습니다.

공유되면 사용자가 작업 공간을 사용하여 대기열에 액세스하여 이러한 작업을 완료할 수 있습니다.

>[!NOTE]
>
>Flex Workspace는 AEM Forms 릴리스에서 더 이상 사용되지 않습니다.

### 선택한 사용자 큐에 대한 액세스 구성 {#configuring-access-to-a-selected-user-queue}

1. 관리자 계정을 사용하여 관리 콘솔에 로그인합니다.
1. 선택 **서비스** > **양식 워크플로우** > **공유 큐**.

1. 사용자에 대한 액세스 관리 탭에서 공유할 대기열을 가진 사용자를 찾아서 선택합니다. 오른쪽 아래 창에는 선택한 사용자 대기열에 액세스할 수 있는 사용자 목록이 표시됩니다.
1. 왼쪽 아래 창에서 사용자를 찾아 선택합니다. 공유를 클릭합니다.
1. 저장을 클릭하여 완료합니다.

### 선택한 사용자 큐에 대한 액세스 취소 {#revoking-access-to-a-selected-user-queue}

1. 관리자 계정을 사용하여 관리 콘솔에 로그인합니다.
1. 선택 **서비스** > **양식 워크플로우** > **공유 큐**.

1. 사용자에 대한 액세스 관리 탭에서 대기열을 관리할 사용자를 찾아서 선택합니다.
1. 오른쪽 아래 창에는 선택한 사용자 대기열에 액세스할 수 있는 사용자 목록이 표시됩니다. 사용자를 선택하고 취소를 누릅니다.
1. 저장을 클릭하여 완료합니다.

## 사용자에게 할당된 큐 관리 {#managing-queues-assigned-to-a-user}

사용자별 액세스 관리 기능을 사용하면 선택한 사용자에게 할당된 대기열을 관리할 수 있습니다. 선택한 사용자에 대한 사용자 큐 액세스를 개별적으로 부여하거나 취소할 수 있습니다. 예를 들어, Akura Tanaka와 John Jacobs의 사용자 큐를 Kara Bumen에게 할당하려고 합니다. Manage Access By A User 기능을 사용하면 Kara Bowman을 검색하고 Akura Tanaka 및 John Jacobs에게 할당된 작업에 대한 액세스 권한을 부여할 수 있습니다. 나중에, 이 사용자 큐에 대한 카라 보우먼의 액세스를 취소할 수 있습니다.

할당되면 Workspace를 사용하여 사용자가 이러한 작업을 완료할 수 있습니다.

>[!NOTE]
>
>Flex Workspace는 AEM Forms 릴리스에서 더 이상 사용되지 않습니다.

### 선택한 사용자 큐에 대한 액세스 권한 부여 {#granting-access-to-a-selected-user-queue}

1. 관리자 계정을 사용하여 관리 콘솔에 로그인합니다.
1. 선택 **서비스** > **양식 워크플로우** > **공유 큐**.

1. 사용자 액세스 관리 탭에서 공유할 대기열을 가진 사용자를 찾아서 선택합니다. 오른쪽 아래 창에는 선택한 사용자 대기열에 액세스할 수 있는 사용자 목록이 표시됩니다.
1. 왼쪽 아래 창에서 선택한 사용자와 공유할 사용자 대기열을 찾아 선택합니다. 공유를 클릭합니다.
1. 저장을 클릭하여 완료합니다.

### 선택한 사용자 큐에 대한 액세스 취소 {#revoking_access_to_a_selected_user_queue-1}

1. 관리자 계정을 사용하여 관리 콘솔에 로그인합니다.
1. 선택 **서비스** > **양식 워크플로우** > **공유 큐**.

1. 사용자별 액세스 관리 탭에서 대기열을 관리할 사용자를 찾아 선택합니다.
1. 오른쪽 아래 창에는 선택한 사용자에게 할당된 사용자 큐 목록이 표시됩니다. 사용자 대기열을 선택하고 취소를 누릅니다.
1. 저장을 클릭하여 완료합니다.
