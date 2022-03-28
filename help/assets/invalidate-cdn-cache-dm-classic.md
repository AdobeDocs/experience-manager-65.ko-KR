---
title: Dynamic Media Classic을 통해 컨텐츠 전달 네트워크 캐시를 무효화합니다.
description: CDN(Content Delivery Network) 캐시 콘텐츠를 무효화하면 캐시가 만료될 때까지 기다리는 대신 Dynamic Media Classic에서 제공하는 자산을 빠르게 업데이트할 수 있습니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: CDN Cache,Dynamic Media Classic
role: User, Admin
exl-id: 7020343a-b556-4091-9717-93fcc55e623b
source-git-commit: b61157b0e9afa49ef72150ae0c1703a959d154be
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 13%

---

# Dynamic Media Classic을 통해 컨텐츠 전달 네트워크 캐시를 무효화합니다. {#invalidating-your-cdn-cached-content}

Dynamic Media 자산은 CDN(Content Delivery Network)에서 캐시하여 빠른 배달을 제공합니다. 그러나 자산을 업데이트할 때에는 이러한 변경 사항을 즉시 적용할 수 있습니다. CDN 캐시 콘텐츠를 무효화하면 캐시가 만료될 때까지 기다리지 않고 Dynamic Media에서 전달하는 자산을 빠르게 업데이트할 수 있습니다.

>[!NOTE]
>
>이 기능을 사용하려면 Adobe Experience Manager Dynamic Media과 함께 번들로 제공되는 기본 CDN을 사용해야 합니다. 다른 모든 사용자 지정 CDN은 이 기능에서 지원되지 않습니다.

>[!IMPORTANT]
>
>다음 단계는 Adobe Experience Manager 6.5, 서비스 팩 5(Experience Manager 6.5.5) 또는 이전 버전의 Dynamic Media에만 적용됩니다.<br>Experience Manager 6.5, 서비스 팩 6(Experience Manager 6.5.6) 이상에서 Dynamic Media을 사용하는 경우 [Dynamic Media을 통해 CDN 캐시 무효화](/help/assets/invalidate-cdn-cache-dynamic-media.md).

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**Dynamic Media Classic을 통해 CDN 캐시를 무효화하려면 다음을 수행하십시오.**

1. 를 엽니다. [Dynamic Media Classic 데스크탑 애플리케이션](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html#system-requirements-dmc-app)그런 다음 계정에 로그인합니다.

   자격 증명과 로그온은 프로비저닝 시 Adobe에서 제공되었습니다. 이 정보가 없는 경우 Adobe 고객 지원 센터에 문의하십시오.

1. 페이지의 오른쪽 위 모서리 근처에 있는 위치로 이동합니다. **[!UICONTROL 설정]** > **[!UICONTROL 애플리케이션 설정]** > **[!UICONTROL 일반 설정]**.
1. 응용 프로그램 일반 설정 페이지의 서버 그룹 머리글 아래에서 **[!UICONTROL CDN 무효화 템플릿]** 텍스트 상자

1. CDN(Content Delivery Network) 캐시를 무효화하는 데 사용되는 템플릿을 지정합니다.

   예를 들어 이미지 사전 설정 또는 수정자 등의 이미지 URL을 `<ID>`다음 예와 같이 특정 이미지 ID 대신

   `https://server.com/is/image/Company/<ID>?$product$`

   템플릿에 `<ID>`을 입력한 다음 Dynamic Media이 채워집니다 `https://<server>/is/image` 여기서 `<server>` 일반 설정에 정의된 게시 서버 이름입니다. &lt;id> 은 무효화하도록 선택한 자산입니다.

1. 페이지의 오른쪽 아래 모서리에서 을(를) 선택합니다. **[!UICONTROL 닫기]**.
1. Dynamic Media Classic 사용자 인터페이스에서 자산을 한 개 이상 선택한 다음 **[!UICONTROL 파일]** > **[!UICONTROL CDN 무효화]**. 만든 템플릿과 선택한 자산에서 생성된 하나 이상의 URL 목록이 표시됩니다. 응용 프로그램 일반 설정 아래의 &quot;게시된 서버 이름&quot; 아래에 나열된 서버 URL을 사용합니다.

   예를 들어 이전 단계에서 CDN 무효화 템플릿 을 설정한 경우 이름이 인 단일 이미지 자산 이미지를 선택했다고 가정합니다. `Backpack_B`. 로 이동할 때 **[!UICONTROL 파일]** > **[!UICONTROL CDN 무효화]**&#x200B;를 입력하면 CDN 무효화 사용자 인터페이스에 다음 생성 URL이 표시됩니다.

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. URL 목록 상자에서 **[!UICONTROL 계속]** 를 눌러 각 특정 URL에 대한 캐시를 지웁니다. URL을 편집하거나 URL 목록 상자에 URL을 입력하거나 붙여넣어 URL을 추가할 수 있습니다. cdn 무효화 템플릿을 미리 설정할 필요가 없습니다.

   선택한 후 **[!UICONTROL 계속]**&#x200B;에 표시기가 표시되어 캐시를 지우는 데 걸리는 시간을 예상할 수 있습니다.

   여러 자산을 선택한 경우, **[!UICONTROL 파일]** > **[!UICONTROL CDN 무효화]**, 저장된 자산에서 각 자산 참조 **[!UICONTROL 템플릿 URL]**. 따라서 다음을 정의할 수 있습니다 **[!UICONTROL CDN 무효화 템플릿]** 는 웹 사이트에서 참조되는 각 URL 이미지 사전 설정(예: 제품 세부 사항 및 검색 결과)을 참조합니다. Then, when you select one or images for invalidation from cache, the URLs automatically populate the interface.

   >[!NOTE]
   >
   >자산을 선택한 다음 **[!UICONTROL 파일]** > **[!UICONTROL CDN 무효화]**, Dynamic Media은 CDN 템플릿을 무효화하여 CDN(Content Delivery Network)에서 무효화할 URL을 자동으로 만듭니다. If there is nothing in the **[!UICONTROL CDN Invalidate Template]** text box, then you get a blank URL list. Caching at the CDN is not asset-based; it is URL-based. Therefore, it is necessary to be aware of the complete URLs that are on your website. After you determine those URLs, you can add them to the **[!UICONTROL Invalidate CDN Template]** text box earlier in the steps. Then, you can select those assets, and invalidate the URLs in one step.
   >
   >또 다른 옵션은 전체 URL을 **[!UICONTROL CDN 무효화]** 목록. 이 방법을 따르면, **[!UICONTROL 파일 > CDN 무효화]** 선택 사항입니다.
