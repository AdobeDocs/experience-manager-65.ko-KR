---
title: Dynamic Media에서 핫링크 보호 활성화
description: Dynamic Media에서 핫링크 보호를 활성화하는 방법에 대한 정보입니다.
uuid: 5f93bc27-5edd-4143-8701-87896c52f0af
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: a70aa448-0f58-4ed2-9381-afcc76fa827f
role: Business Practitioner, Administrator
exl-id: 698e8bdb-9b31-49ab-8560-26b05109bb23
feature: 구성
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Dynamic Media {#activating-hotlink-protection-in-dynamic-media}에서 핫링크 보호 활성화

핫 링크는 타사 웹 사이트에서 HTML 코드를 사용하여 웹 사이트의 이미지를 표시하는 경우입니다. 방문자의 브라우저가 사용자의 서버에서 직접 그림을 액세스하고 있으므로 사진이 요청될 때마다 대역폭을 사용합니다. Hotlink *보호*&#x200B;는 다른 웹 사이트가 웹 페이지에서 사진, css 또는 JavaScript에 직접 연결되지 않도록 하는 방법입니다. 이러한 종류의 차드는 Dynamic Media 계정에서 불필요한 대역폭 사용을 줄이는 데 도움이 됩니다.

[Adobe ](https://helpx.adobe.com/support.html) 지원에서CDN(Content Delivery Network) 수준에서 레퍼러 필터를 구성하여 Dynamic Media 컨텐츠가 도메인에 대해 허용된 웹 사이트 목록의 웹 사이트에만 제공되도록 할 수 있습니다.

>[!NOTE]
>
>이 기능을 사용하려면 Adobe Experience Manager Dynamic Media과 함께 번들로 제공되는 기본 CDN을 사용해야 합니다. 다른 모든 사용자 지정 CDN은 이 기능에서 지원되지 않습니다. 핫링크 보호를 활성화하려면 관리자가 Dynamic Media 계정에 대한 구성 변경을 요청하려면 Adobe 고객 지원 지원 티켓을 만들어야 합니다. 핫 링크 보호 활성화를 위한 추가 비용은 없습니다.
