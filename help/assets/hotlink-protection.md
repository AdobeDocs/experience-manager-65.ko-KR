---
title: Dynamic Media에서 핫 링크 보호 활성화
description: Dynamic Media에서 핫 링크 보호를 활성화하는 방법에 대한 정보입니다.
uuid: 5f93bc27-5edd-4143-8701-87896c52f0af
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: a70aa448-0f58-4ed2-9381-afcc76fa827f
translation-type: tm+mt
source-git-commit: 787f3b4cf5835b7e9b03e3f4e6f6597084adec8c
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Dynamic Media {#activating-hotlink-protection-in-dynamic-media}에서 핫 링크 보호 활성화

핫 링크는 타사 웹 사이트에서 HTML 코드를 사용하여 웹 사이트의 이미지를 표시할 때 사용됩니다. 방문자의 브라우저가 서버에서 직접 그림을 액세스하고 있으므로 사진이 요청될 때마다 대역폭을 사용합니다. Hotlink *protection*&#x200B;은 다른 웹 사이트에서 웹 페이지의 사진, css 또는 JavaScript에 직접 연결할 수 없도록 하는 방법입니다. 이러한 유형의 방패드는 Dynamic Media 계정에서 불필요한 대역폭 사용을 줄이는 데 도움이 됩니다.

[Adobe ](https://helpx.adobe.com/support.html) 지원도메인 허용 웹 사이트 목록의 웹 사이트에만 Dynamic Media 컨텐츠가 제공되도록 CDN(Content Delivery Network) 수준에서 레퍼러 필터를 구성할 수 있습니다.

>[!NOTE]
>
>이 기능을 사용하려면 Adobe Experience Manager Dynamic Media에 번들로 제공되는 기본 CDN을 사용해야 합니다. 다른 모든 사용자 지정 CDN은 이 기능에서 지원되지 않습니다. 핫 링크 보호를 활성화하려면 관리자가 Adobe 고객 지원 티켓을 만들어 Dynamic Media 계정에 구성 변경을 요청해야 합니다. 핫 링크 보호 활성화를 위한 추가 비용은 없습니다.
