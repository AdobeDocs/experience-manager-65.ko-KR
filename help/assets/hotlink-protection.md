---
title: Dynamic Media에서 핫링크 보호 활성화
description: Dynamic Media에서 핫 링크 보호를 활성화하는 방법에 대한 정보입니다.
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
role: User, Admin
exl-id: 698e8bdb-9b31-49ab-8560-26b05109bb23
feature: Configuration
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Dynamic Media에서 핫링크 보호 활성화 {#activating-hotlink-protection-in-dynamic-media}

핫 연결은 서드파티 웹 사이트가 HTML 코드를 사용하여 웹 사이트의 이미지를 표시하는 것입니다. 방문자의 브라우저가 서버에서 바로 액세스하고 있으므로 그림이 요청될 때마다 대역폭을 사용합니다. 핫링크 *보호*&#x200B;는 다른 웹 사이트가 웹 페이지의 사진, CSS 또는 JavaScript에 직접 링크되지 않도록 하는 방법입니다. 이러한 종류의 실드는 Dynamic Media 계정에서 불필요한 대역폭 사용을 줄이는 데 도움이 됩니다.

[Experience Manager 고객 지원 센터](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support)는 CDN(Content Delivery Network) 수준에서 레퍼러 필터를 구성하여 도메인에 대해 허용된 웹 사이트 목록의 웹 사이트에만 Dynamic Media 콘텐츠가 제공되도록 할 수 있습니다.

>[!NOTE]
>
>이 기능을 사용하려면 Adobe Experience Manager Dynamic Media과 번들로 제공되는 기본 CDN을 사용해야 합니다. 다른 모든 사용자 지정 CDN은 이 기능에서 지원되지 않습니다. 핫링크 보호를 활성화하려면 관리자는 Adobe 고객 지원 지원 티켓을 만들어 Dynamic Media 계정에 대한 구성 변경을 요청해야 합니다. 핫 링크 보호를 활성화하는 데 드는 추가 비용은 없습니다.
