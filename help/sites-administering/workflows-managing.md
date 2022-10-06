---
title: 워크플로에 대한 액세스 관리
seo-title: Managing Access to Workflows
description: 워크플로우에 대한 액세스를 관리하는 방법을 알아봅니다.
seo-description: Learn how to manage access to Workflows.
uuid: 58f79b89-fe56-4565-a869-8179c1ac68de
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5150867a-02a9-45c9-b2fd-e536b60ffa8c
exl-id: cc54d637-d66c-49d2-99ee-00d96f1a74e0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 2%

---

# 워크플로에 대한 액세스 관리{#managing-access-to-workflows}

워크플로우에 시작(또는 비활성화)하고 참여할 수 있도록 사용자 계정에 따라 ACL을 구성합니다.

## 워크플로우에 대한 필수 사용자 권한 {#required-user-permissions-for-workflows}

워크플로우에 대한 작업은 다음 경우에 수행할 수 있습니다.

* 당신은 `admin` account
* 계정이 기본 그룹에 할당되었습니다. `workflow-users`:

   * 이 그룹은 사용자가 워크플로우 작업을 수행하는 데 필요한 모든 권한을 보유합니다.
   * 계정이 이 그룹에 있으면 시작된 워크플로우에만 액세스할 수 있습니다.

* 계정이 기본 그룹에 할당되었습니다. `workflow-administrators`:

   * 이 그룹은 권한이 있는 사용자가 워크플로우를 모니터링하고 관리하는 데 필요한 모든 권한을 보유합니다.
   * 계정이 이 그룹에 있으면 모든 워크플로우에 액세스할 수 있습니다.

>[!NOTE]
>
>최소 요구 사항입니다. 특정 단계를 수행하려면 계정이 지정된 참가자 또는 지정된 그룹의 구성원이어야 합니다.

## 워크플로우에 대한 액세스 구성 {#configuring-access-to-workflows}

워크플로우 모델은 사용자가 워크플로우와 상호 작용할 수 있는 방법을 제어하는 기본 ACL(액세스 제어 목록)을 상속합니다. 워크플로우에 대한 사용자 액세스를 사용자 정의하려면 워크플로우 모델 노드가 포함된 폴더의 저장소에서 ACL(액세스 제어 목록)을 수정합니다.

* [/var/workflow/models에 특정 워크플로우 모델에 대한 ACL 적용](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)
* [/var/workflow/models에서 하위 폴더를 만들고 ACL을 해당 폴더에 적용합니다](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)

>[!NOTE]
>
>CRXDE Lite을 사용하여 ACL 구성에 대한 자세한 내용은 [액세스 권한 관리](/help/sites-administering/user-group-ac-admin.md#access-right-management).

### /var/workflow/models에 특정 워크플로우 모델에 대한 ACL 적용 {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

워크플로우 모델이 내에 저장되는 경우 `/var/workflow/models` 그런 다음 폴더에 해당 워크플로우에만 관련된 특정 ACL을 할당할 수 있습니다.

1. 웹 브라우저에서 CRXDE Lite 열기(예: [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. 노드 트리에서 워크플로우 모델 폴더의 노드를 선택합니다.

   `/var/workflow/models`

1. 을(를) 클릭합니다. **액세스 제어** 탭.
1. 에서 **로컬 액세스 제어 정책** (**액세스 제어 목록**) 표를 만들 때 더하기 아이콘을 클릭하여 **항목 추가**.
1. 에서 **새 항목 추가** 대화 상자에서 다음 속성을 사용하여 새 ACE를 추가합니다.

   * **주체**: `content-authors`
   * **유형**: `Deny`
   * **권한**: `jcr:read`
   * **rep:glob**: 특정 워크플로우에 대한 참조

   ![wf-108](assets/wf-108.png)

   다음 **액세스 제어 목록** 이제 테이블에 `content-authors` on `prototype-wfm-01` 워크플로우 모델.

   ![wf-109](assets/wf-109.png)

1. 클릭 **모두 저장**.

   다음 `prototype-wfm-01` 워크플로우는 더 이상 `content-authors` 그룹에 속해 있어야 합니다.

### /var/workflow/models에서 하위 폴더를 만들고 ACL을 해당 폴더에 적용합니다 {#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

사용자 [개발 팀은 하위 폴더에서 워크플로우를 만들 수 있습니다](/help/sites-developing/workflows-models.md#creating-a-new-workflow) 의

`/var/workflow/models`

에 저장된 DAM 워크플로우와 비교

`/var/workflow/models/dam/`

그런 다음 폴더 자체에 ACL을 추가할 수 있습니다.

1. 웹 브라우저에서 CRXDE Lite 열기(예: [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. 노드 트리에서 워크플로우 모델 폴더의 개별 폴더에 대한 노드를 선택합니다. 예:

   `/var/workflow/models/prototypes`

1. 을(를) 클릭합니다. **액세스 제어** 탭.
1. 에서 **적용 가능한 액세스 제어 정책** 표, 더하기 아이콘 을 클릭하여 **추가** 항목.
1. 에서 **로컬 액세스 제어 정책** (**액세스 제어 목록**) 표를 만들 때 더하기 아이콘을 클릭하여 **항목 추가**.
1. 에서 **새 항목 추가** 대화 상자에서 다음 속성을 사용하여 새 ACE를 추가합니다.

   * **주체**: `content-authors`
   * **유형**: `Deny`
   * **권한**: `jcr:read`

   >[!NOTE]
   >
   >과 함께 [/var/workflow/models에 특정 워크플로우 모델에 대한 ACL 적용](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models) rep:glob를 포함하여 특정 워크플로우에 대한 액세스를 제한할 수 있습니다.

   ![wf-110](assets/wf-110.png)

   다음 **액세스 제어 목록** 이제 테이블에 `content-authors` on `prototypes` 폴더를 입력합니다.

   ![wf-111](assets/wf-111.png)

1. 클릭 **모두 저장**.

   의 모델 `prototypes` 더 이상 폴더를 `content-authors` 그룹에 속해 있어야 합니다.
