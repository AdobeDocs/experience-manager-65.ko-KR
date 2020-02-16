---
title: 브랜드 포털에 컬렉션 게시
seo-title: 브랜드 포털에 컬렉션 게시
description: Brand Portal에 컬렉션을 게시하고 게시 취소하는 방법을 알아봅니다.
seo-description: Brand Portal에 컬렉션을 게시하고 게시 취소하는 방법을 알아봅니다.
uuid: 7de58548-4cfa-4a94-bac7-9e914dee9042
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 90e3fd0e-9bc3-4aff-8c7b-7408f5b940e8
docset: aem65
translation-type: tm+mt
source-git-commit: 9c73abc3291f2847c705cb649d2993fb186b0993

---


# Publish collections to Brand Portal {#publish-collections-to-brand-portal}

AEM(Adobe Experience Manager) 자산 관리자는 컬렉션을 조직의 AEM Assets 브랜드 포털 인스턴스에 게시할 수 있습니다. 그러나 먼저 AEM 자산을 브랜드 포털과 통합해야 합니다. 자세한 내용은 브랜드 포털과 [AEM 자산 통합 구성을 참조하십시오](/help/assets/brand-portal-configuring-integration.md).

AEM Assets에서 원본 컬렉션을 이후에 수정하는 경우, 컬렉션을 다시 게시하기 전까지 변경 내용이 브랜드 포털에 반영되지 않습니다. 이러한 특성을 통해 브랜드 포털에서 진행 중인 변경 사항을 사용할 수 없습니다. 관리자가 게시한 승인된 변경 사항만 브랜드 포털에서 사용할 수 있습니다.

>[!NOTE]
>
>콘텐츠 조각을 브랜드 포털에 게시할 수 없습니다. 따라서 AEM 작성자에서 컨텐츠 조각을 선택하는 경우 브랜드 포털에 **게시** 작업을 사용할 수 없습니다.
>
>콘텐츠 조각이 포함된 컬렉션이 AEM 작성자에서 브랜드 포털로 게시되면 콘텐츠 조각을 제외한 폴더의 모든 콘텐츠가 브랜드 포털 인터페이스에 복제됩니다.

## 브랜드 포털에 컬렉션 게시 {#publish-a-collection-to-brand-portal}

1. AEM 자산 UI에서 AEM 로고를 클릭합니다.
1. 탐색 **페이지에서** 자산 > **컬렉션으로 이동합니다**.
1. 컬렉션 콘솔에서 브랜드 포털에 게시할 컬렉션을 선택합니다.

   ![select_collection](assets/select_collection.png)

1. 도구 모음에서 브랜드 포털에 **게시를 클릭합니다**.
1. 확인 대화 상자에서 게시를 **클릭합니다**.
1. 확인 메시지를 닫습니다.
1. Brand Portal에 관리자로 로그인합니다. 게시된 컬렉션은 컬렉션 콘솔에서 사용할 수 있습니다.

   ![게시된 컬렉션](assets/published_collection.png)

## 컬렉션 게시 취소 {#unpublish-collections}

AEM 자산에서 브랜드 포털에 게시하는 컬렉션을 게시 취소할 수 있습니다. 원본 컬렉션을 게시 취소한 후에는 해당 복사본을 더 이상 브랜드 포털 사용자가 사용할 수 없습니다.

1. AEM 자산 인스턴스의 컬렉션 콘솔에서 게시 취소할 컬렉션을 선택합니다.

   ![select_collection-1](assets/select_collection-1.png)

1. 도구 모음에서 브랜드 포털에서 **제거 아이콘을 클릭합니다** .
1. 대화 상자에서 게시 취소를 **클릭합니다**.
1. 확인 메시지를 닫습니다. 컬렉션은 브랜드 포털 인터페이스에서 제거됩니다.

