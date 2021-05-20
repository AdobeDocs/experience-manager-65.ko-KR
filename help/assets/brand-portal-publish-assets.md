---
title: 자산을 Brand Portal에 게시
seo-title: 자산을 Brand Portal에 게시
description: Brand Portal에 자산을 게시하고 게시 취소하는 방법을 알아봅니다.
seo-description: Brand Portal에 자산을 게시하고 게시 취소하는 방법을 알아봅니다.
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
feature: Brand Portal
role: Business Practitioner
exl-id: 76652a16-cad6-4e95-9e66-41efec452b03
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 44%

---

# 자산을 Brand Portal에 게시 {#publish-assets-to-brand-portal}

Adobe Experience Manager(AEM) Assets 관리자는 자산 및 폴더를 조직의 AEM Assets Brand Portal 인스턴스에 게시(또는 게시 워크플로우를 나중 날짜/시간으로 예약)할 수 있습니다. 하지만 먼저 Brand Portal에서 AEM Assets를 구성해야 합니다. 자세한 내용은 [Brand Portal에서 AEM Assets 구성](/help/assets/configure-aem-assets-with-brand-portal.md)을 참조하십시오.

복제가 성공하면 자산, 폴더 및 컬렉션을 Brand Portal에 게시할 수 있습니다. Brand Portal에 자산을 게시하려면 다음 단계를 수행합니다.

>[!NOTE]
>
>AEM 작성자가 초과 리소스를 차지하지 않도록 가급적이면 피크가 아닌 시간에, 시차 게시를 수행하는 것이 좋습니다.

1. Assets 콘솔에서 게시하려는 자산/폴더를 선택하고 도구 모음에서 **[!UICONTROL 빠른 게시]** 옵션을 클릭합니다.

   또는 Brand Portal에 게시할 자산을 선택합니다.

   ![publish2bp-2](assets/publish2bp.png)

1. 자산을 Brand Portal에 게시하려면 다음 두 가지 옵션을 사용할 수 있습니다.
   * [자산을 즉시 게시](#publish-to-bp-now)
   * [나중에 자산 게시](#publish-to-bp-now)

## 지금 자산 게시 {#publish-to-bp-now}

선택한 자산을 Brand Portal에 게시하려면 다음 중 하나를 수행하십시오.

* 도구 모음에서 **[!UICONTROL 빠른 게시]**&#x200B;를 선택합니다. 그런 다음 메뉴에서 **[!UICONTROL Brand Portal에 게시]**&#x200B;를 선택합니다.

* 도구 모음에서 **[!UICONTROL 게시 관리]**&#x200B;를 선택합니다.

   1. 그런 다음 **[!UICONTROL 작업]** Brand Portal에 게시&#x200B;]**를 선택하고**[!UICONTROL &#x200B;예약&#x200B;]**에서**[!UICONTROL &#x200B;지금&#x200B;]**을 선택합니다.**[!UICONTROL  **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   2. **[!UICONTROL 범위]** 내에서 선택 내용을 확인하고 **[!UICONTROL Brand Portal에 게시]**&#x200B;를 클릭합니다.

자산이 Brand Portal에 게시하기 위한 큐에 올라갔음을 나타내는 메시지가 나타납니다. Brand Portal 인터페이스에 로그인하여 게시된 자산을 확인합니다.

## 나중에 자산 게시 {#publish-to-bp-later}

나중 날짜 또는 시간에 Brand Portal에 자산을 게시하는 일정을 예약하려면,

1. 게시할 자산/폴더를 선택한 후 맨 위의 도구 모음에서 **[!UICONTROL 게시 관리]**&#x200B;를 선택합니다.

1. **[!UICONTROL 게시 관리]** 페이지에서 **[!UICONTROL Brand Portal에 게시]**&#x200B;를 선택하고 **[!UICONTROL 예약]**&#x200B;에서 **[!UICONTROL 나중에]**&#x200B;을 선택합니다.****

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. **[!UICONTROL 활성화 날짜]**&#x200B;를 선택하고 시간을 지정합니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

1. **활성화 날짜**&#x200B;를 선택하고 시간을 지정합니다. **다음**&#x200B;을 클릭합니다.

1. **[!UICONTROL 워크플로우]**&#x200B;에서 **[!UICONTROL 워크플로우 제목]**&#x200B;을 지정합니다. **[!UICONTROL 나중에 게시]**&#x200B;를 클릭합니다.

   ![publishworkflow](assets/publishworkflow.png)

이제 Brand Portal에 로그인하여 게시된 자산을 Brand Portal 인터페이스에서 사용할 수 있는지 확인합니다.

![bp_landing_page](assets/bp_landing_page.png)
