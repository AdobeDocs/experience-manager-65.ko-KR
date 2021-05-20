---
title: 컬렉션을 Brand Portal에 게시
seo-title: 컬렉션을 Brand Portal에 게시
description: Brand Portal에 컬렉션을 게시하고 게시 취소하는 방법을 알아봅니다.
seo-description: Brand Portal에 컬렉션을 게시하고 게시 취소하는 방법을 알아봅니다.
uuid: 7de58548-4cfa-4a94-bac7-9e914dee9042
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 90e3fd0e-9bc3-4aff-8c7b-7408f5b940e8
docset: aem65
feature: Brand Portal
role: Business Practitioner
exl-id: 8f426012-d9ec-418e-8ab6-78e4aeff7538
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 36%

---

# 컬렉션을 Brand Portal에 게시 {#publish-collections-to-brand-portal}

AEM(Adobe Experience Manager) Assets 관리자는 조직의 AEM Assets Brand Portal 인스턴스에 컬렉션을 게시할 수 있습니다. 그러나 먼저 AEM Assets을 Brand Portal과 통합해야 합니다. 자세한 내용은 [Brand Portal에서 AEM Assets 구성](/help/assets/configure-aem-assets-with-brand-portal.md)을 참조하십시오.

AEM Assets에서 원래 컬렉션을 차후에 수정하는 경우 컬렉션을 다시 게시하기 전까지는 변경 내용이 Brand Portal에 반영되지 않습니다. 이 특성은 진행 중인 작업 변경 사항을 Brand Portal에서 사용할 수 없도록 합니다. 관리자가 게시한 승인된 변경 사항만 Brand Portal에서 사용할 수 있습니다.

>[!NOTE]
>
>컨텐츠 조각은 Brand Portal에 게시할 수 없습니다. 따라서 AEM 작성자에서 컨텐츠 조각을 선택하는 경우 **Brand Portal에 게시** 작업을 사용할 수 없습니다.
>
>컨텐츠 조각이 포함된 컬렉션이 AEM 작성자에서 Brand Portal으로 게시되면 컨텐츠 조각을 제외한 폴더의 모든 컨텐츠가 Brand Portal 인터페이스에 복제됩니다.

## 컬렉션을 Brand Portal {#publish-a-collection-to-brand-portal}에 게시

1. AEM Assets UI에서 AEM 로고를 클릭합니다.
1. **탐색** 페이지에서 **자산 > 컬렉션**&#x200B;으로 이동합니다.
1. 컬렉션 콘솔에서 Brand Portal에 게시하려는 컬렉션을 선택합니다.

   ![select_collection](assets/select_collection.png)

1. 도구 모음에서 **Brand Portal에 게시**&#x200B;를 클릭합니다.
1. 확인 대화 상자에서 **게시**&#x200B;를 클릭합니다.
1. 확인 메시지를 닫습니다.
1. 관리자로 Brand Portal에 로그인합니다. 게시된 컬렉션은 컬렉션 콘솔에서 사용할 수 있습니다.

   ![게시된 컬렉션](assets/published_collection.png)

## 컬렉션 게시 취소 {#unpublish-collections}

AEM Assets에서 Brand Portal으로 게시하는 컬렉션을 게시 취소할 수 있습니다. 원래 컬렉션을 게시 취소한 후에는 Brand Portal 사용자가 해당 복사본을 더 이상 사용할 수 없습니다.

1. AEM Assets 인스턴스의 컬렉션 콘솔에서 게시를 취소하려는 컬렉션을 선택합니다.

   ![select_collection-1](assets/select_collection-1.png)

1. 도구 모음에서 **Brand Portal에서 제거** 아이콘을 클릭합니다.
1. 대화 상자에서 **게시 취소**&#x200B;를 클릭합니다.
1. 확인 메시지를 닫습니다. 컬렉션이 Brand Portal 인터페이스에서 제거됩니다.
