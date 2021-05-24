---
title: Admin Console
seo-title: Admin Console
description: AEM에서 사용할 수 있는 Admin Console을 사용하는 방법을 알아봅니다.
seo-description: AEM에서 사용할 수 있는 Admin Console을 사용하는 방법을 알아봅니다.
uuid: 82ab5267-2f2a-4772-85d5-678d883a0294
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6dbe82c2-7a25-49ab-a980-3635f0344817
docset: aem65
exl-id: d4de517e-50bc-4ca5-89b1-295d259fd5bb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 2%

---

# Admin Console{#admin-consoles}

기본적으로 관리 콘솔을 통해 클래식 UI로 전환하는 기능이 비활성화됩니다. 따라서 특정 콘솔 아이콘 위에 마우스를 올려 놓으면 클래식 UI에 액세스할 수 있는 팝업 아이콘이 더 이상 표시되지 않습니다.

`/libs/cq/core/content/nav`에 클래식 UI 버전이 있는 모든 콘솔은 마우스로 가리키면 **클래식 UI** 옵션이 콘솔 아이콘 위에 다시 표시되도록 개별적으로 다시 활성화할 수 있습니다.

이 예에서는 사이트 콘솔에 대한 클래식 UI를 다시 활성화합니다.

1. CRXDE Lite을 사용하여 클래식 UI를 다시 활성화할 Admin Console에 해당하는 노드를 찾습니다. 다음 위치에서 찾을 수 있습니다.

   `/libs/cq/core/content/nav`

   예

   [ `https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. 클래식 UI를 다시 활성화할 콘솔에 해당하는 노드를 선택합니다. 이 예에서는 사이트 콘솔에 대한 클래식 UI를 다시 활성화합니다.

   `/libs/cq/core/content/nav/sites`

1. **오버레이 노드** 옵션을 사용하여 오버레이를 만듭니다.예:

   * **경로**: `/apps/cq/core/content/nav/sites`
   * **오버레이 위치**: `/apps/`
   * **일치 노드 유형**:활성(확인란 선택)

1. 오버레이된 노드에 다음 부울 속성을 추가합니다.

   `enableDesktopOnly = {Boolean}true`

1. **클래식 UI** 옵션은 Admin Console에서 팝업 옵션으로 다시 사용할 수 있습니다.

   ![](assets/syui-01-2019-02-27-15-16-55.png)

클래식 UI 버전에 대한 액세스를 다시 활성화할 모든 콘솔에 대해 이 단계를 반복합니다.
