---
title: 워크플로우에 대한 액세스 관리
seo-title: 워크플로우에 대한 액세스 관리
description: 워크플로우에 대한 액세스를 관리하는 방법을 알아봅니다.
seo-description: 워크플로우에 대한 액세스를 관리하는 방법을 알아봅니다.
uuid: 58f79b89-fe56-4565-a869-8179c1ac68de
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5150867a-02a9-45c9-b2fd-e536b60ffa8c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 워크플로우에 대한 액세스 관리{#managing-access-to-workflows}

사용자 계정에 따라 워크플로우의 시작 및 참여를 허용(또는 비활성화)하도록 ACL을 구성합니다.

## 워크플로우에 필요한 사용자 권한 {#required-user-permissions-for-workflows}

다음과 같은 경우 워크플로우에 대한 작업을 수행할 수 있습니다.

* 계정 사용 `admin` 중
* 계정이 기본 그룹에 `workflow-users`할당되었습니다.

   * 이 그룹은 사용자가 워크플로우 작업을 수행하는 데 필요한 모든 권한을 보유합니다.
   * 계정이 이 그룹에 있으면 시작된 워크플로우에만 액세스할 수 있습니다.

* 계정이 기본 그룹에 `workflow-administrators`할당되었습니다.

   * 이 그룹은 권한이 있는 사용자가 워크플로우를 모니터링하고 관리하는 데 필요한 모든 권한을 보유합니다.
   * 계정이 이 그룹에 있으면 모든 워크플로우에 액세스할 수 있습니다.

>[!NOTE]
>
>다음은 최소 요구 사항입니다. 또한 특정 단계를 수행하려면 계정이 지정된 참가자 또는 지정된 그룹의 구성원이어야 합니다.

## 워크플로우에 대한 액세스 권한 구성 {#configuring-access-to-workflows}

워크플로우 모델은 기본 ACL(액세스 제어 목록)을 상속하여 사용자가 워크플로우와 상호 작용할 수 있는 방법을 제어합니다. 워크플로우에 대한 사용자 액세스를 사용자 정의하려면 워크플로우 모델 노드가 들어 있는 폴더의 저장소에서 ACL(액세스 제어 목록)을 수정합니다.

* [/var/workflow/models에 특정 워크플로우 모델에 대한 ACL 적용](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)
* [/var/workflow/models에서 하위 폴더를 만들고 ACL을 해당 폴더에 적용](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)

>[!NOTE]
>
>CRXDE Lite를 사용하여 ACL 구성에 대한 자세한 내용은 액세스 권한 [관리를 참조하십시오](/help/sites-administering/user-group-ac-admin.md#access-right-management).

### /var/workflow/models에 특정 워크플로우 모델에 대한 ACL 적용 {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

워크플로우 모델이 내부에 저장된 `/var/workflow/models` 경우 해당 워크플로우와 관련된 특정 ACL을 폴더에 할당할 수 있습니다.

1. 웹 브라우저에서 CRXDE Lite를 엽니다(예: http://localhost:4502/crx/de [](http://localhost:4502/crx/de)).
1. 노드 트리에서 워크플로우 모델 폴더의 노드를 선택합니다.

   `/var/workflow/models`

1. 액세스 제어 **탭을** 클릭합니다.
1. 로컬 **액세스 제어 정책** (**액세스 제어 목록**) 테이블에서 더하기 아이콘을 클릭하여 항목 **추가를**&#x200B;클릭합니다.
1. 새 **항목 추가** 대화 상자에서 다음 속성이 있는 새 ACE를 추가합니다.

   * **주체**: `content-authors`
   * **유형**: `Deny`
   * **권한**: `jcr:read`
   * **rep:glob**:특정 워크플로우에 대한 참조
   ![wf-108](assets/wf-108.png)

   이제 **액세스 제어** 목록 표에 `content-authors` 워크플로우 모델에 대한 `prototype-wfm-01` 제한이 포함됩니다.

   ![wf-109](assets/wf-109.png)

1. 모두 **저장을 클릭합니다**.

   더 `prototype-wfm-01` 이상 그룹의 구성원이 워크플로우를 사용할 수 없습니다 `content-authors` .

### /var/workflow/models에서 하위 폴더를 만들고 ACL을 해당 폴더에 적용 {#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

개발 [](/help/sites-developing/workflows-models.md#creating-a-new-workflow) 팀은

`/var/workflow/models`

DAM 워크플로우와 비교할 수 있습니다.

`/var/workflow/models/dam/`

그런 다음 폴더 자체에 ACL을 추가할 수 있습니다.

1. 웹 브라우저에서 CRXDE Lite를 엽니다(예: http://localhost:4502/crx/de [](http://localhost:4502/crx/de)).
1. 노드 트리에서 워크플로우 모델 폴더의 개별 폴더에 대한 노드를 선택합니다.예를 들면 다음과 같습니다.

   `/var/workflow/models/prototypes`

1. 액세스 제어 **탭을** 클릭합니다.
1. 적용 가능한 **액세스 제어 정책** 테이블에서 더하기 아이콘을 클릭하여 **항목을** 추가합니다.
1. 로컬 **액세스 제어 정책** (**액세스 제어 목록**) 테이블에서 더하기 아이콘을 클릭하여 항목 **추가를**&#x200B;클릭합니다.
1. 새 **항목 추가** 대화 상자에서 다음 속성이 있는 새 ACE를 추가합니다.

   * **주체**: `content-authors`
   * **유형**: `Deny`
   * **권한**: `jcr:read`
   >[!NOTE]
   >
   >특정 워크플로우 [모델에 대한 ACL을 /var/workflow/models에](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models) 적용하는 경우와 마찬가지로 rep:glob를 포함하여 특정 워크플로우에 대한 액세스를 제한할 수 있습니다.

   ![wf-110](assets/wf-110.png)

   이제 **액세스 제어** 목록 표에 `content-authors` 폴더에 대한 `prototypes` 제한이 포함됩니다.

   ![wf-111](assets/wf-111.png)

1. 모두 **저장을 클릭합니다**.

   더 이상 `prototypes` 폴더의 모델을 `content-authors` 그룹 구성원이 사용할 수 없습니다.

