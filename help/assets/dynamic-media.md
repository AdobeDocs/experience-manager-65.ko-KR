---
title: Dynamic Media를 사용하여 작업
description: Dynamic Media을 사용하여 웹, 모바일 및 소셜 사이트에서 사용할 자산을 제공하는 방법을 알아봅니다.
uuid: 4dc0f436-d20e-4e8b-aeff-5515380fa44d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
discoiquuid: a8063d43-923a-42ac-9a16-0c7fadd8f73f
role: User, Admin
exl-id: f8a80b22-b1a6-475f-b3f1-b2f47822f21d
feature: Collaboration,Asset Management
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 21%

---

# Dynamic Media 작업 {#working-with-dynamic-media}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html)는 다양한 시각적 머천다이징 및 마케팅 자산을 웹, 모바일 및 소셜 사이트에 맞게 자동으로 크기를 조정하여 주문형으로 제공하는 데 도움이 됩니다. 기본 소스 자산 세트를 사용하면 Dynamic Media는 글로벌, 확장 가능 및 성능 최적화 네트워크를 통해 실시간으로 다양한 유형의 풍부한 컨텐츠를 생성하고 전달합니다.

Dynamic Media은 확대/축소, 360도 회전 및 비디오를 비롯한 대화형 보기 환경을 제공합니다. Dynamic Media은 디지털 캠페인 관리 프로세스를 간소화하고 간소화하기 위해 Adobe Experience Manager 디지털 에셋 관리(Assets) 솔루션의 워크플로를 고유하게 통합합니다.

<!-- >ARTICLE IS MISSING. GIVES 404 [!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## Dynamic Media으로 수행할 수 있는 작업 {#what-you-can-do-with-dynamic-media}

Dynamic Media을 사용하면 자산을 게시하기 전에 관리할 수 있습니다. 일반적으로 에셋으로 작업하는 방법은에 자세히 설명되어 있습니다 [디지털 에셋으로 작업](manage-assets.md). 일반적인 주제에는 에셋 업로드, 다운로드, 편집 및 게시, 속성 보기 및 편집, 에셋 검색 등이 있습니다.

Dynamic Media 전용 기능에는 다음이 포함됩니다.

* [회전 배너](carousel-banners.md)
* [이미지 세트](image-sets.md)
* [대화형 이미지](interactive-images.md)
* [대화형 비디오](interactive-videos.md)
* [혼합 미디어 세트](mixed-media-sets.md)
* [파노라마 이미지](panoramic-images.md)

* [스핀 세트](spin-sets.md)
* [비디오](video.md)
* [Dynamic Media 자산 전송](delivering-dynamic-media-assets.md)
* [에셋 관리](managing-assets.md)
* [빠른 보기를 사용하여 사용자 정의 팝업 제작](custom-pop-ups.md)

참조: [Dynamic Media 설정](administering-dynamic-media.md).

>[!NOTE]
>
>Dynamic Media 사용과 Dynamic Media Classic과 Adobe Experience Manager 통합 간의 차이점을 이해하려면 다음을 참조하십시오. [Dynamic Media Classic 통합 대 Dynamic Media](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media).

## Dynamic Media 활성화됨 대 Dynamic Media 비활성화됨 {#dynamic-media-on-versus-dynamic-media-off}

다음 특성에 의해 Dynamic Media이 활성화(켜짐)되었는지 여부를 알 수 있습니다.

* 다이내믹 렌디션은 에셋을 다운로드하거나 미리 볼 때 사용할 수 있습니다.
* 이미지 세트, 스핀 세트, 혼합 미디어 세트를 사용할 수 있습니다.
* PTIFF 렌디션이 생성됩니다.

이미지 에셋을 선택하면 Dynamic Media의 에셋 보기가 달라집니다 [활성화됨](config-dynamic.md#enabling-dynamic-media). Dynamic Media은 on-demand HTML5 뷰어를 사용합니다.

### 동적 변환 {#dynamic-renditions}

이미지 및 뷰어 사전 설정과 같은 동적 변환(아래) **[!UICONTROL 동적]**) Dynamic Media이 활성화되면 사용할 수 있습니다.

![chlimage_1-358](assets/chlimage_1-358.png)

### 이미지 세트, 스핀 세트, 혼합 미디어 세트 {#image-sets-spins-sets-mixed-media-sets}

Dynamic Media이 활성화된 경우 이미지 세트, 스핀 세트 및 혼합 미디어 세트를 사용할 수 있습니다.

![chlimage_1-359](assets/chlimage_1-359.png)

### PTIFF 표현물 {#ptiff-renditions}

Dynamic Media 활성화 에셋에는 다음이 포함됩니다 `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### 자산 보기 변경 {#asset-views-change}

Dynamic Media이 활성화되면 `+` 및 `-` 단추. 클릭/탭하여 특정 영역을 확대할 수도 있습니다. 되돌리기 를 사용하면 원래 버전으로 이동할 수 있으며 대각선 화살표를 클릭하여 이미지를 전체 화면으로 만들 수 있습니다. Dynamic Media이 활성화된 형태는 다음과 같습니다.

![chlimage_1-361](assets/chlimage_1-361.png)

Dynamic Media이 비활성화되면 확대/축소하고 원래 크기로 되돌릴 수 있습니다.

![chlimage_1-362](assets/chlimage_1-362.png)
