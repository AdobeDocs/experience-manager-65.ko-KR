---
title: 페이지에 워크플로 적용
description: 워크플로는 웹 사이트 콘솔에서 시작하거나 페이지를 편집할 때 사이드 킥에서 시작할 수 있습니다.
uuid: 55f6f1d7-da54-4732-b9ff-b7479622db51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 22712b73-90f2-4329-b32f-dbb7ce802d1d
exl-id: d8b604c5-a6da-47c4-9422-b519e224c7ca
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 15%

---

# 페이지에 워크플로 적용{#applying-workflows-to-pages}

워크플로를 적용할 때에는 다음 정보를 지정합니다.

* The workflow to apply.

   You can apply any workflow (that you have access to, as assigned by your AEM administrator).
* 선택적으로:

   * 워크플로우를 시작한 이유에 대한 정보를 제공하는 주석입니다.
   * 사용자의 받은 편지함에서 워크플로 인스턴스를 식별하는 데 도움이 되는 제목입니다.

>[!NOTE]
>
>AEM 관리자는 을 사용하여 워크플로를 시작할 수 있습니다. [기타 여러 방법](/help/sites-administering/workflows-starting.md).

## 워크플로우 적용 {#applying-workflows}

워크플로는 웹 사이트 콘솔에서 시작하거나 페이지를 편집할 때 사이드 킥에서 시작할 수 있습니다.

다음 **상태** 열의 **웹 사이트** 콘솔은 워크플로가 페이지에 적용되었는지 여부를 나타냅니다.

![workflowstatus](assets/workflowstatus.png)

### 웹 사이트 콘솔에서 워크플로 시작 {#starting-a-workflow-from-the-websites-console}

1. 웹 사이트 콘솔을 엽니다. ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))
1. 웹 사이트 트리에서 워크플로를 적용할 페이지의 상위 항목을 선택합니다.
1. 페이지 목록에서 페이지를 선택한 다음 워크플로 를 클릭합니다.
1. 워크플로 시작 대화 상자에서 적용할 워크플로를 선택합니다. 원할 경우 댓글과 제목을 입력합니다. 그런 다음 시작을 클릭합니다.

### 사이드 킥을 사용하여 워크플로우 시작 {#starting-a-workflow-using-sidekick}

1. 웹 사이트 콘솔을 엽니다.
1. 필요한 페이지를 엽니다.
1. 사이드 킥에서 워크플로 탭을 선택합니다.
1. 확장 **워크플로** 대화 상자 - 다음을 선택할 수 있습니다. **워크플로** 및 선택적으로 다음을 입력합니다. **워크플로우 제목** 및 **댓글**.

   ![workflowstartsidekick](assets/workflowstartsidekick.png)

1. 클릭 **워크플로우 시작** 를 클릭하여 구성한 속성을 사용하여 새 워크플로우 인스턴스를 시작하고 페이로드는 현재 페이지입니다. 이제 워크플로우가 실행 중입니다.
