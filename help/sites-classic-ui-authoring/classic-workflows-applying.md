---
title: 페이지에 워크플로 적용
description: 워크플로는 웹 사이트 콘솔에서 시작하거나, 페이지를 편집할 때 Sidekick에서 시작할 수 있습니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: d8b604c5-a6da-47c4-9422-b519e224c7ca
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 15%

---

# 페이지에 워크플로 적용{#applying-workflows-to-pages}

워크플로를 적용할 때에는 다음 정보를 지정합니다.

* 적용할 워크플로.

  AEM 관리자가 할당한 대로 액세스할 수 있는 워크플로를 적용할 수 있습니다.
* 선택적으로:

   * 워크플로우를 시작한 이유에 대한 정보를 제공하는 주석입니다.
   * 사용자의 받은 편지함에서 워크플로 인스턴스를 식별하는 데 도움이 되는 제목입니다.

>[!NOTE]
>
>AEM 관리자는 [다른 여러 방법](/help/sites-administering/workflows-starting.md)을 사용하여 워크플로를 시작할 수 있습니다.

## 워크플로우 적용 {#applying-workflows}

워크플로는 웹 사이트 콘솔에서 시작하거나, 페이지를 편집할 때 Sidekick에서 시작할 수 있습니다.

**웹 사이트** 콘솔의 **상태** 열은 워크플로가 페이지에 적용되었는지 여부를 나타냅니다.

![workflowstatus](assets/workflowstatus.png)

### 웹 사이트 콘솔에서 워크플로 시작 {#starting-a-workflow-from-the-websites-console}

1. 웹 사이트 콘솔을 엽니다. ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))
1. 웹 사이트 트리에서 워크플로를 적용할 페이지의 상위 항목을 선택합니다.
1. 페이지 목록에서 페이지를 선택한 다음 워크플로 를 클릭합니다.
1. 워크플로 시작 대화 상자에서 적용할 워크플로를 선택합니다. 원할 경우 댓글과 제목을 입력합니다. 그런 다음 시작을 클릭합니다.

### Sidekick을 사용하여 워크플로우 시작 {#starting-a-workflow-using-sidekick}

1. 웹 사이트 콘솔을 엽니다.
1. 필요한 페이지를 엽니다.
1. Sidekick에서 워크플로 탭을 선택합니다.
1. **워크플로** 대화 상자를 확장하여 **워크플로**&#x200B;를 선택하고 **워크플로 제목** 및 **설명**&#x200B;을 선택적으로 입력할 수 있습니다.

   ![workflowstartsidekick](assets/workflowstartsidekick.png)

1. **워크플로 시작**&#x200B;을 클릭하여 구성한 속성과 현재 페이지를 페이로드로 새 워크플로 인스턴스를 시작합니다. 이제 워크플로우가 실행 중입니다.
