---
title: 워크플로우 시작
seo-title: 워크플로우 시작
description: AEM에서 워크플로우를 시작하는 방법을 알아봅니다.
seo-description: AEM에서 워크플로우를 시작하는 방법을 알아봅니다.
uuid: 0648d335-ecce-459d-95fd-3d4d76181b32
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: e9ab4796-a050-40de-b073-af7d33cff009
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 워크플로우 시작{#starting-workflows}

워크플로우 관리 시 다양한 방법을 사용하여 워크플로우를 시작할 수 있습니다.

* 수동:

   * 워크플로우 [모델에서](#workflow-models).
   * 워크플로우 패키지를 사용하여 [일괄 처리](#workflow-packages-for-batch-processing).

* 자동:

   * 노드 변경에 대한 응답으로;launcher [사용](#workflows-launchers).

>[!NOTE]
>
>다른 메서드는 작성자도 사용할 수 있습니다.자세한 내용은 다음을 참조하십시오.
>
>* ](/help/sites-authoring/workflows-applying.md)페이지에 워크플로우 적용[
>* [DAM 자산에 워크플로우를 적용하는 방법](/help/assets/assets-workflow.md)
>* [AEM 양식](https://helpx.adobe.com/aem-forms/6-2/aem-workflows-submit-process-form.html)
>* [번역 프로젝트](/help/sites-administering/tc-manage.md)
>



## 워크플로우 모델 {#workflow-models}

워크플로우 모델 콘솔에 나열된 모델 [중 하나를](/help/sites-administering/workflows.md#workflow-models-and-instances) 기반으로 워크플로우를 시작할 수 있습니다. 제목 및/또는 댓글도 추가할 수 있지만 필수 정보는 페이로드뿐입니다.

## 워크플로우 방사기 {#workflows-launchers}

Workflow Launcher는 변경된 노드의 위치 및 리소스 유형에 따라 컨텐츠 저장소의 변경 사항을 모니터링하여 워크플로우를 시작합니다.

론쳐를 **사용하여** 다음을 수행할 수 있습니다.

* 특정 노드에 대해 이미 시작된 워크플로우를 참조하십시오.
* 특정 노드/노드 유형이 생성/수정/제거되면 시작할 워크플로우를 선택합니다.
* 기존 워크플로우-노드 관계를 제거합니다.

모든 노드에 대해 실행 관리자를 만들 수 있습니다. 그러나 특정 노드에 대한 변경 사항은 워크플로우를 실행하지 않습니다. 다음 경로 아래의 노드를 변경해도 워크플로우가 실행되지 않습니다.

* `/var/workflow/instances`
* 분기에서 임의의 위치에 있는 모든 Workflow-inbox 노드 `/home/users`
* `/tmp`
* `/var/audit`
* `/var/classes`
* `/var/eventing`
* `/var/linkchecker`
* `/var/mobile`
* `/var/statistics`

   * 예외:아래 노드를 변경하면 `/var/statistics/tracking` 워크플로우가 *시작됩니다* .

표준 설치에는 다양한 정의가 포함되어 있습니다. 디지털 자산 관리 및 소셜 공동 작업 작업에 사용됩니다.

![wf-100](assets/wf-100.png)

## 일괄 처리를 위한 워크플로우 패키지 {#workflow-packages-for-batch-processing}

워크플로우 패키지는 처리를 위한 페이로드로 워크플로우에 전달되어 여러 리소스를 처리할 수 있는 패키지입니다.

워크플로우 패키지:

* 에는 리소스 세트(예: 페이지, 자산)에 대한 링크가 포함되어 있습니다.
* 작성 날짜, 패키지를 생성한 사용자 및 간단한 설명과 같은 패키지 정보를 보관합니다.
* 은 특수 페이지 템플릿을 사용하여 정의됩니다.이러한 페이지에서는 사용자가 패키지의 리소스를 지정할 수 있습니다.
* 여러 번 사용할 수 있습니다.
* 워크플로우 인스턴스가 실제로 실행 중일 때 사용자가 변경(리소스 추가 또는 제거)할 수 있습니다.

## Starting a Workflow from the Models Console {#starting-a-workflow-from-the-models-console}

1. 도구, **워크플로우** , **모델**&#x200B;등을 사용하여 모델 **콘솔로**&#x200B;이동한 **다음**&#x200B;모델모델로 이동합니다.
1. 콘솔 보기에 따라 워크플로우를 선택합니다.필요한 경우 검색(왼쪽 위)을 사용할 수도 있습니다.

   ![wf-103](assets/wf-103.png)

   >[!NOTE]
   >
   >임시 **[표시기는](/help/sites-developing/workflows.md#transient-workflows)**워크플로우 내역이 지속되지 않는 워크플로우를 보여줍니다.

1. 도구 **모음에서 워크플로우** 시작을 선택합니다.
1. 워크플로우 실행 대화 상자가 열려 다음을 지정할 수 있습니다.

   * **페이로드**

      페이지, 노드, 자산, 패키지 등의 리소스를 사용할 수 있습니다.

   * **제목**

      이 인스턴스를 식별하는 데 도움이 되는 선택적 제목입니다.

   * **주석**

      이 인스턴스의 세부 사항을 나타내는 데 도움이 되는 선택적 주석입니다.
   ![wf-104](assets/wf-104.png)

## 실행 관리자 구성 만들기 {#creating-a-launcher-configuration}

1. 도구, **워크플로우** , **방사기를**&#x200B;사용하여 Workflow **Launcher**&#x200B;콘솔로 **이동한 다음** Launcher로 이동합니다.
1. 만들기를 **선택한**&#x200B;다음 **실행** 추가 대화 상자를 엽니다.

   ![wf-105](assets/wf-105.png)

   * **이벤트 유형**

      워크플로우를 시작할 이벤트 유형:

      * 작성일
      * 수정됨
      * 제거됨
   * **Noetype**

      워크플로우 실행 프로그램이 적용되는 노드의 유형입니다.

   * **경로**

      워크플로우 실행 프로그램이 적용되는 경로입니다.

   * **모드 실행**

      워크플로우 실행 프로그램이 적용되는 서버 유형입니다. [ **작성자**], [게시 **]**&#x200B;또는 [ **작성 및 게시]를 선택합니다**.

   * **조건**

      평가 시 워크플로우가 실행되는지 여부를 결정하는 노드 값에 대한 조건 목록입니다. 예를 들어 다음 조건을 사용하면 노드에 사용자 값이 있는 속성 이름이 있을 때 워크플로우가 시작됩니다.

      name==사용자

   * **기능**

      활성화할 기능 목록입니다. 드롭다운 선택기를 사용하여 필요한 기능을 선택합니다.

   * **비활성화된 기능**
   비활성화할 기능 목록입니다. 드롭다운 선택기를 사용하여 필요한 기능을 선택합니다.

   * **워크플로우 모델**

      정의된 조건 아래의 Nodetype 및/또는 경로에서 이벤트 유형이 발생할 때 시작되는 워크플로우입니다.

   * **설명**

      실행 프로그램 구성을 설명하고 식별하기 위한 자체 텍스트입니다.

   * **활성화**

      워크플로우 실행 프로그램의 활성화 여부를 제어합니다.

      * 구성 **속성이** 만족되면 워크플로우를 시작하려면 활성화를 선택합니다.
      * 워크플로우가 **실행되지** 않을 경우 비활성화(구성 속성이 만족될 때에도 제외)를 선택합니다.
   * **제외 목록**

      워크플로우의 트리거 여부를 결정할 때 제외할 JCR 이벤트(즉, 무시)를 지정합니다.

      이 시작 관리자 속성은 쉼표로 구분된 항목 목록입니다.&quot;

      * `property-name` 지정된 속성 이름에 트리거된 모든 `jcr` 이벤트를 무시합니다.&quot;
      * `event-user-data:<*someValue*>` api(https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/observation/ObservationManager.html#setUserData(java.lang.String)를 통해 `*<someValue*`> `user-data` 설정된 이벤트를 [ 무시합니다 `ObservationManager`].
      예:

      `jcr:lastModified,dc:modified,dc:format,jcr:lastModifiedBy,imageMap,event-user-data:changedByWorkflowProcess`

      이 기능은 제외 항목을 추가하여 다른 워크플로우 프로세스에서 트리거된 모든 변경 사항을 무시하는 데 사용할 수 있습니다.

      `event-user-data:changedByWorkflowProcess`





1. [ **만들기**]를 선택하여 시작 관리자를 만들고 콘솔로 돌아갑니다.

   적절한 이벤트가 발생하면 실행 프로그램이 트리거되고 워크플로우가 시작됩니다.

## 실행 관리자 구성 관리 {#managing-a-launcher-configuration}

론치 구성을 만든 후 동일한 콘솔을 사용하여 인스턴스를 선택한 다음 속성 보기(및 편집) **** 또는 삭제를 **선택할 수 있습니다**.
