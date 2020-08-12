---
title: 다이내믹 미디어를 통해 CDN 캐시 무효화
description: CDN(Content Delivery Network) 캐시 컨텐츠를 무효화할 수 있으므로 캐시 만료가 기다리는 대신 다이내믹 미디어에서 제공하는 자산을 신속하게 업데이트할 수 있습니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: 9e67e252348f471c052f6c3e88aea61d7a309241
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 4%

---


# 다이내믹 미디어를 통해 CDN 캐시 무효화 {#invalidating-cdn-cache-for-dm-assets}

다이내믹 미디어 자산은 CDN(Content Delivery Network)에 의해 캐시되어 고객에게 빠르게 배달됩니다. 그러나 이러한 에셋을 업데이트할 때 해당 변경 사항이 웹 사이트에서 즉시 적용될 수 있습니다. CDN 캐시를 지우거나 무효화하면 Dynamic Media에서 제공하는 자산을 신속하게 업데이트할 수 있습니다. TTL(Time To Live) 값(기본값은 10시간)을 사용하여 캐시가 만료될 때까지 대기하지 않고 다이내믹 미디어 내에서 요청을 보내 캐시가 즉시 만료되도록 할 수 있습니다.

>[!IMPORTANT]
>
>이러한 단계는 AEM 6.5, 서비스 팩 6 이상의 Dynamic Media - Scene7 모드에만 적용됩니다. <!-- If you are using Dynamic Media in AEM 6.5, Service Pack 5 or earlier [use the steps found here](/help/assets/invalidate-cdn-cache-dm-classic.md). -->

Dynamic [Media의 캐싱 개요를 참조하십시오](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**다이내믹 미디어 자산에 대해 CDN 캐시된 컨텐츠를 무효화하려면:**

1. AEM 6.5.6 이상에서 **[!UICONTROL 도구 > 자산 > CDN 무효화를 누릅니다.]**

   ![CDN 유효성 검사 기능](/help/assets/assets-dm/cdn-invalidation-path.png)

1. CDN 무효화 페이지에서 원하는 옵션을 설정합니다.

   | 옵션 | 설명 |
   | --- | --- |
   | **[!UICONTROL CDN에서 자산 관련 이미지 사전 설정 무효화]** | 이 옵션을 선택하면 캐시 무효화를 위해 MIME 유형 및 관련 이미지 사전 설정에 상관없이 하나 이상의 Dynamic Media 자산을 선택할 수 있습니다.<br>자산을 포함하는 폴더를 하나 이상 선택할 수 있지만 Adobe에서는 이 방법을 권장하지 않습니다. 대신 개별 자산 파일을 선택해야 합니다.<br>다음 단계로 진행합니다. |
   | **[!UICONTROL 템플릿을 기반으로 한 무효화]** | 이 옵션을 선택하면 Dynamic Media 자산 및 이전에 만든 무효화 템플릿을 선택할 수 있습니다. 이 옵션을 |
   | **[!UICONTROL 자산 추가]** | 블라 |
   | **[!UICONTROL URL 추가]** | 캐시를 무효화할 다이내믹 미디어 자산에 전체 URL 경로를 수동으로 추가합니다. |

1. 
1. 다음을 **[!UICONTROL 누릅니다.]**
1. 
