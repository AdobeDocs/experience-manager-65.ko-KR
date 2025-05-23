---
title: 공유 큐 구성
description: 공유 대기열을 사용하면 사용자 대기열을 효과적으로 구성하고 관리할 수 있습니다. 공유 대기열을 구성하는 방법에 대해 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5f4467c1-0f3f-4dc6-9bd5-98259f327295
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# 공유 큐 구성{#configuring-shared-queues}

공유 대기열을 사용하면 사용자 대기열을 효과적으로 구성하고 관리할 수 있습니다. 사용자 큐는 사용자에게 할당된 모든 작업입니다. 자세한 내용은 [할 일 목록](https://help.adobe.com/en_US/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html)을 참조하세요. 조직의 요구 사항에 따라 사용자 대기열을 할당, 할당 해제 및 재할당할 수 있습니다. 다음 두 가지 방법으로 공유 대기열을 관리할 수 있습니다.

**사용자에 대한 액세스 관리**

이 옵션을 사용하여 선택한 사용자 대기열에 대한 액세스를 관리할 수 있습니다.

**사용자의 액세스 관리**

이 옵션을 사용하여 선택한 사용자에게 할당된 공유 대기열을 관리할 수 있습니다.

## 선택한 사용자 대기열에 대한 액세스 관리 {#managing-access-to-a-selected-user-queue}

사용자 액세스 관리 기능을 사용하면 선택한 사용자 대기열에 대한 액세스를 관리할 수 있습니다. 선택한 사용자 대기열에 대한 액세스 권한을 조직의 다른 사용자에게 부여하거나 취소할 수 있습니다. 예를 들어, 카라 보우먼은 실직 상태이다. 사용자 액세스 관리 기능을 사용하면 Kara의 대기열을 Akira Tanaka 및 John Jacobs와 공유하여 완료할 수 있습니다. 나중에 카라가 사무실로 돌아오면 다나카 아키라, 존 제이콥스로부터 받은 대기열 접속을 취소할 수 있습니다.

공유되면 사용자는 Workspace을 사용하여 큐에 액세스하여 이러한 작업을 완료할 수 있습니다.

>[!NOTE]
>
>Flex Workspace은 AEM Forms 릴리스에서 더 이상 사용되지 않습니다.

### 선택한 사용자 대기열에 대한 액세스 구성 {#configuring-access-to-a-selected-user-queue}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인합니다.

1. 관리자 계정을 사용하여 관리 콘솔에 로그인합니다.
1. **서비스** > **Forms Workflow** > **공유 큐**&#x200B;를 선택합니다.

1. 사용자 액세스 관리 탭에서 공유하려는 대기열의 사용자를 찾아 선택합니다. 언제든지 오른쪽 아래 창에 선택한 사용자 대기열에 액세스할 수 있는 사용자 목록이 표시됩니다.
1. 왼쪽 하단 창에서 사용자를 찾아 선택합니다. 공유를 클릭합니다.
1. 저장 을 클릭하여 완료합니다.

### 선택한 사용자 대기열에 대한 액세스 취소 {#revoking-access-to-a-selected-user-queue}

1. 관리자 계정을 사용하여 관리 콘솔에 로그인합니다.
1. **서비스** > **Forms Workflow** > **공유 큐**&#x200B;를 선택합니다.

1. 사용자 액세스 관리 탭에서 관리할 대기열의 사용자를 찾아 선택합니다.
1. 오른쪽 아래 창에는 선택한 사용자 대기열에 액세스할 수 있는 사용자 목록이 표시됩니다. 사용자를 선택하고 취소 를 클릭합니다.
1. 저장 을 클릭하여 완료합니다.

## 사용자에게 할당된 대기열 관리 {#managing-queues-assigned-to-a-user}

사용자별 액세스 관리 기능을 사용하면 선택한 사용자에게 할당된 대기열을 관리할 수 있습니다. 사용자 대기열에 대한 액세스 권한을 선택한 사용자에게 개별적으로 부여하거나 취소할 수 있습니다. 예를 들어 Akira Tanaka 및 John Jacobs 사용자 대기열을 Kara Bowman에게 할당하려고 합니다. 사용자별 액세스 관리 기능을 사용하여 Kara Bowman을 검색하고 Akira Tanaka 및 John Jacobs에게 할당된 작업에 대한 액세스 권한을 부여할 수 있습니다. 나중에 이러한 사용자 대기열에 대한 Kara Bowman의 액세스를 취소할 수 있습니다.

할당되면 사용자는 Workspace을 사용하여 이러한 작업을 완료할 수 있습니다.

>[!NOTE]
>
>Flex Workspace은 AEM Forms 릴리스에서 더 이상 사용되지 않습니다.

### 선택한 사용자 대기열에 대한 액세스 권한 부여 {#granting-access-to-a-selected-user-queue}

1. 관리자 계정을 사용하여 관리 콘솔에 로그인합니다.
1. **서비스** > **Forms Workflow** > **공유 큐**&#x200B;를 선택합니다.

1. 사용자 액세스 관리 탭에서 공유하려는 대기열의 사용자를 찾아 선택합니다. 언제든지 오른쪽 아래 창에 선택한 사용자 대기열에 액세스할 수 있는 사용자 목록이 표시됩니다.
1. 왼쪽 하단 창에서 선택한 사용자와 공유할 사용자 대기열을 찾아 선택합니다. 공유를 클릭합니다.
1. 저장 을 클릭하여 완료합니다.

### 선택한 사용자 대기열에 대한 액세스 취소 {#revoking_access_to_a_selected_user_queue-1}

1. 관리자 계정을 사용하여 관리 콘솔에 로그인합니다.
1. **서비스** > **Forms Workflow** > **공유 큐**&#x200B;를 선택합니다.

1. 사용자별 액세스 관리 탭에서 관리할 대기열의 사용자를 찾아 선택합니다.
1. 오른쪽 아래 창에는 선택한 사용자에게 할당된 사용자 대기열 목록이 표시됩니다. 사용자 대기열을 선택하고 취소를 누릅니다.
1. 저장 을 클릭하여 완료합니다.
