---
title: 제품 피드
seo-title: 제품 피드
description: AEM 제품 피드에 대해 알아봅니다.
seo-description: AEM 제품 피드에 대해 알아봅니다.
uuid: 99eb9bdc-2717-45d4-9203-6394b7d7ddc6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 1f920892-c52e-42ca-900c-2c7ab3c503b3
exl-id: 11a3d636-040a-40bb-ad35-6b8430a81a49
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 4%

---

# 제품 피드 {#product-feed}

AEM은 [Search &amp; Promote](https://www.adobe.com/solutions/testing-targeting/searchandpromote.html)과 통합되어 다음 작업을 수행할 수 있습니다.

* 기본 저장소 구조 및 상거래 플랫폼과 독립적으로 eCommerce API를 사용합니다.
* Search &amp; Promote의 색인 커넥터 기능을 활용하여 제품 피드를 XML 형식으로 제공합니다.
* Search &amp; Promote의 원격 제어 기능을 활용하여 제품 피드의 온디맨드 또는 예약된 요청을 수행합니다
* 클라우드 서비스 구성으로 구성된 다양한 Search &amp; Promote 계정에 대한 피드 생성.

올바른 계정이 있어야 하며 [Search &amp; Promote](/help/sites-administering/search-and-promote.md#configuring-the-connection-to-search-promote)에 대한 연결을 구성해야 합니다. 또한 올바른 [데이터 센터](/help/sites-administering/search-and-promote.md#configuring-the-data-center)를 사용하고 있는지 확인하고 **원격 서버 URI **가 구성되어 있는지 확인해야 합니다.

## 제품 피드 {#set-up-the-product-feed} 설정

먼저 웹 사이트 루트와 식별자 속성을 입력해야 합니다. 이를 위해 진행되는 작업:

1. Search &amp; Promote 구성으로 이동합니다.
1. **[!UICONTROL 편집]**&#x200B;을 클릭합니다. 
1. **[!UICONTROL Index Connector 피드 구성]** 탭을 클릭합니다.
1. **[!UICONTROL 웹 사이트 루트]** 및 **[!UICONTROL 식별자 속성]**&#x200B;을 입력합니다.

   >[!NOTE]
   >
   >**[!UICONTROL 웹 사이트 루트]**&#x200B;는 eCommerce 웹 사이트의 루트입니다(예: `/content/geometrixx-outdoors/en`).
   >
   >**[!UICONTROL 식별자 속성]**&#x200B;은 제품을 고유하게 식별하는 JCR 속성입니다.`identifier`

1. **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

그런 다음 제품 피드를 생성하기 전에 웹 콘솔에서 두 개의 구성을 편집해야 합니다.

### Geometrixx {#configuring-the-day-cq-search-promote-products-crawler-implementation-for-geometrixx}에 대한 Day CQ Search &amp; Promote 제품 Crawler 구현 구성

1. [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)로 이동합니다.
1. Geometrixx ]**에 대한**[!UICONTROL &#x200B;일 CQ Search &amp; Promote 제품 Crawler 구현을 클릭합니다.
1. 이 Crawler가 연결된 Search &amp; Promote 계정 번호를 지정합니다. 이 Crawler에서 사용하는 클라우드 서비스 구성을 조회하는 데 사용됩니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

### Geometrixx {#configuring-the-day-cq-search-promote-products-feed-generator-for-geometrixx}에 대한 일 CQ Search &amp; Promote 제품 피드 생성기 구성

1. [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)로 이동합니다.
1. Geometrixx ]**용**[!UICONTROL &#x200B;일 CQ Search &amp; Promote 제품 피드 생성기를 클릭합니다.
1. 이 생성기가 연결된 Search &amp; Promote 계정 번호를 지정합니다. 이 생성기에서 사용하는 클라우드 서비스 구성을 찾는 데 사용됩니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

## 제품 피드 예약 {#schedule-the-product-feed}

예약된 피드 생성을 활성화하려면 스케줄러를 구성해야 합니다.
스케줄러는 특정 Search &amp; Promote 클라우드 서비스 구성의 하위 구성으로 구성됩니다.

1. Search &amp; Promote 구성으로 이동합니다.
1. **[!UICONTROL 스케줄러 구성]** 옆에 있는 **[!UICONTROL +]**&#x200B;을 클릭합니다.
1. 페이지 작성자가 인식할 수 있는 **[!UICONTROL 제목]**&#x200B;과 고유한 **[!UICONTROL 이름]**&#x200B;을 입력합니다.
1. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 대화 상자가 열립니다.

   ![chlimage_1-108](assets/chlimage_1-108a.png)

1. **[!UICONTROL 원격 제어 암호]**&#x200B;를 입력합니다. Search&amp;Proponote 계정에 구성한 암호입니다.

   >[!NOTE]
   >
   >Search &amp; Promote 계정의 암호가 아닙니다. Search &amp; Promote 계정에 로그인하고 **[!UICONTROL Index]**&#x200B;으로 이동한 다음 **[!UICONTROL Remote control]**&#x200B;로 이동하여 이 암호를 찾아 변경할 수 있습니다.

1. **[!UICONTROL Enable schedule]** 상자를 선택합니다.
1. **[!UICONTROL 예약]**&#x200B;을 선택합니다. 실제 피드 생성 일정입니다.
1. **[!UICONTROL 온디맨드 인덱싱]**&#x200B;을 활성화하거나 사용하지 않도록 설정하십시오. 이 기능은 Search &amp; Promote 인덱스를 수동으로 호출하는 데 사용됩니다. **[!UICONTROL 전체 제품 피드 요청]**&#x200B;이 선택된 경우 Search &amp; Promote은 전체 제품 피드를 요청합니다. 그렇지 않으면 증분 제품 피드가 요청됩니다.

   >[!NOTE]
   >
   >온디맨드 인덱싱 기능을 사용하면 Search &amp; Promote의 원격 제어 기능을 사용할 수 있습니다. 원격 인덱싱이 호출되면 인덱싱이 즉시 시작되지 않지만 원격 제어 기능을 사용하여 Search &amp; Promote에 색인 요청이 게시됩니다.

1. **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

모든 구성을 구성했으므로 구성된 웹 사이트 루트 아래에 모든 제품이 포함된 XML 페이지가 표시됩니다.[http://localhost:4502/etc/commerce/searchpromote/feed/full](http://localhost:4502/etc/commerce/searchpromote/feed/full)
