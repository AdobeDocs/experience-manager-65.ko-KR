---
title: 워크플로에 대한 액세스 관리
description: 워크플로우의 시작 및 참여를 허용(또는 비활성화)하도록 사용자 계정에 따라 액세스 제어 목록을 구성하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: cc54d637-d66c-49d2-99ee-00d96f1a74e0
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 4%

---

# 워크플로에 대한 액세스 관리{#managing-access-to-workflows}

워크플로우를 시작(또는 비활성화)하고 참여하도록 사용자 계정에 따라 ACL을 구성합니다.

## 워크플로우에 필요한 사용자 권한 {#required-user-permissions-for-workflows}

다음과 같은 경우 워크플로우에 대한 작업을 수행할 수 있습니다.

* `admin` 계정으로 작업 중입니다.
* 계정이 기본 그룹 `workflow-users`에 할당되었습니다.

   * 이 그룹은 사용자가 워크플로우 작업을 수행하는 데 필요한 모든 권한을 갖습니다.
   * 계정이 이 그룹에 있으면 시작한 워크플로우에만 액세스할 수 있습니다.

* 계정이 기본 그룹 `workflow-administrators`에 할당되었습니다.

   * 이 그룹은 권한이 있는 사용자가 워크플로우를 모니터링하고 관리하는 데 필요한 모든 권한을 갖습니다.
   * 계정이 이 그룹에 있으면 모든 워크플로우에 액세스할 수 있습니다.

>[!NOTE]
>
>최소 요구 사항입니다. 특정 단계를 수행하려면 계정이 할당된 참가자 또는 할당된 그룹의 구성원이어야 합니다.

## 워크플로우에 대한 액세스 구성 {#configuring-access-to-workflows}

워크플로 모델은 사용자가 워크플로와 상호 작용하는 방법을 제어하기 위한 기본 액세스 제어 목록(ACL)을 상속합니다. 워크플로에 대한 사용자 액세스를 사용자 정의하려면 워크플로 모델 노드가 포함된 폴더의 저장소에서 ACL(액세스 제어 목록)을 수정합니다.

* [/var/workflow/models에 특정 워크플로우 모델에 대한 ACL 적용](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)
* [/var/workflow/models에 하위 폴더를 만들고 여기에 ACL 을 적용합니다](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)

>[!NOTE]
>
>CRXDE Lite을 사용하여 ACL을 구성하는 방법에 대한 자세한 내용은 [액세스 권한 관리](/help/sites-administering/user-group-ac-admin.md#access-right-management)를 참조하십시오.

### /var/workflow/models에 특정 워크플로우 모델에 대한 ACL 적용 {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

워크플로 모델이 `/var/workflow/models` 내에 저장되어 있으면 해당 워크플로와 관련된 특정 ACL을 다음 폴더에 할당할 수 있습니다.

1. 웹 브라우저에서 CRXDE Lite을 엽니다(예: [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. 노드 트리에서 워크플로 모델 폴더의 노드를 선택합니다.

   `/var/workflow/models`

1. **액세스 제어** 탭을 클릭합니다.
1. **로컬 액세스 제어 정책**(**액세스 제어 목록**) 테이블에서 더하기 아이콘을 클릭하여 **항목 추가**&#x200B;를 실행하십시오.
1. **새 항목 추가** 대화 상자에서 다음 속성을 사용하여 ACE를 추가합니다.

   * **사용자**: `content-authors`
   * **유형**: `Deny`
   * **권한**: `jcr:read`
   * **rep:glob**: 특정 워크플로우에 대한 참조

   ![wf-108](assets/wf-108.png)

   이제 **액세스 제어 목록** 테이블에 `prototype-wfm-01` 워크플로 모델의 `content-authors`에 대한 제한이 포함됩니다.

   ![wf-109](assets/wf-109.png)

1. **모두 저장**&#x200B;을 클릭합니다.

   `content-authors` 그룹의 구성원은 `prototype-wfm-01` 워크플로를 더 이상 사용할 수 없습니다.

### /var/workflow/models에 하위 폴더를 만들고 여기에 ACL 을 적용합니다 {#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

[개발 팀에서 하위 폴더에 워크플로를 만들 수 있음](/help/sites-developing/workflows-models.md#creating-a-new-workflow)

`/var/workflow/models`

아래에 저장된 DAM 워크플로우와 비교

`/var/workflow/models/dam/`

그런 다음 폴더 자체에 ACL을 추가할 수 있습니다.

1. 웹 브라우저에서 CRXDE Lite을 엽니다(예: [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. 노드 트리에서 워크플로 모델 폴더의 개별 폴더에 대한 노드를 선택합니다. 예를 들면 다음과 같습니다.

   `/var/workflow/models/prototypes`

1. **액세스 제어** 탭을 클릭합니다.
1. **적용 가능한 액세스 제어 정책** 테이블에서 더하기 아이콘을 클릭하여 항목을 **추가**&#x200B;합니다.
1. **로컬 액세스 제어 정책**(**액세스 제어 목록**) 테이블에서 더하기 아이콘을 클릭하여 **항목 추가**&#x200B;를 실행하십시오.
1. **새 항목 추가** 대화 상자에서 다음 속성을 사용하여 ACE를 추가합니다.

   * **사용자**: `content-authors`
   * **유형**: `Deny`
   * **권한**: `jcr:read`

   >[!NOTE]
   >
   >[특정 워크플로 모델에 대한 ACL을 /var/workflow/models에 적용](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)할 때와 마찬가지로 rep:glob을 포함하여 특정 워크플로에 대한 액세스를 제한할 수 있습니다.

   ![wf-110](assets/wf-110.png)

   이제 **액세스 제어 목록** 테이블에 `prototypes` 폴더의 `content-authors`에 대한 제한이 포함됩니다.

   ![wf-111](assets/wf-111.png)

1. **모두 저장**&#x200B;을 클릭합니다.

   `content-authors` 그룹의 구성원은 `prototypes` 폴더의 모델을 더 이상 사용할 수 없습니다.
