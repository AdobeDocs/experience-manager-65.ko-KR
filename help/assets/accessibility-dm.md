---
title: 액세스 가능성 [!DNL Dynamic Media]
description: 다이내믹 미디어 및 다이내믹 미디어 뷰어의 액세스 가능성에 대해 알아봅니다.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: 383f84b1a984683b3e2ce60f1a3f2191749a1561
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# 액세스 가능성 [!DNL Dynamic Media] {#working-with-three-d-assets-dm}

[!DNL Dynamic Media] 는 저작 유저 인터페이스에서 JAWS 및 NVDA 화면 판독기와 같은 키보드 제어 및 보조 기술을 지원합니다.

## 키보드 액세스 가능성 지원 [!DNL Dynamic Media]

플러그인 [!DNL Dynamic Media] 은 플러그인이므로 [!DNL Adobe Experience Manager Assets]대부분의 키보드 컨트롤 동작은 에서와 동일합니다 [!DNL Experience Manager Assets]. 예를 들어, 의 `Cancel` 단추 [!DNL Dynamic Media] 의 초점 강조 표시 [!DNL Experience Manager Assets]는 in과 동일하게 `Spacebar` 키에 반응합니다 [!DNL Experience Manager Assets]. 자산에서 [키보드 단축키를 참조하십시오](/help/assets/accessibility.md#keyboard-shortcuts).

개별 사용자 인터페이스 요소에서 지원하는 키 입력은 [!DNL Dynamic Media] 거의 명확하고 쉽게 찾을 수 있습니다. 키보드 컨트롤 [!DNL Dynamic Media] 은 다음과 같습니다.

* 페이지에서 인터랙티브한 요소 간 `Tab` 을 탐색하기 위해 키 `Shift+Tab` 입력과 키를 사용하는 기능
탭 순서에서 다음 사용자 인터페이스 요소로 입력 포커스를 `Tab` 이동합니다.를 `Shift+Tab` 사용하면 입력 포커스가 이전 사용자 인터페이스 요소로 돌아갑니다.
초점 트래픽은 화면의 자연스러운 사용자 인터페이스 요소 위치를 따르며 왼쪽에서 오른쪽, 위에서 아래로 이동합니다. 또한 필드에 오류가 있으면 키를 눌러 포커스를 이동할 수 `Tab` 있습니다.
* 버튼, `Spacebar` 드롭다운 목록 등과 같은 표준 사용자 인터페이스 요소를 활성화하는 데 `Enter` 및키를 사용하는 기능입니다.
* 활성 요소에서 키보드 초점 강조 표시를 보는 기능 입력 포커스가 있는 사용자 인터페이스 요소는 사용자 인터페이스 요소 주위에 렌더링된 테두리로 시각적 초점 표시를 받을 수 있습니다.
* 핫스팟 편집기에서 화살표 키와 같은 일부 사용자 정의 키 입력을 사용하여 복잡한 사용자 인터페이스 요소와 상호 작용하여 핫스팟 위치를 변경할 수 있습니다.
* 대화형 비디오 편집기에서 아이콘을 사용하여 이미지를 선택하고 세그먼트에 추가할 수 `Spacebar` 있습니다. 또한 `Backspace` 키를 사용하여 [콘텐트] 탭에서 선택한 항목을 삭제할 수 **[!UICONTROL 있습니다]** . 또한 페이지에서 대화형 요소 간을 탐색하기 위해 필요에 따라 키를 `Tab` 누릅니다.
* 이미지 자르기/스마트 자르기 편집기에서 다음을 수행할 수 있습니다.
   * 화살표 키를 사용하여 프레임 크기를 자르거나 이미지 또는 둘 다의 위치를 다시 지정할 수 있습니다.
   * 첫 번째 `Tab` 정지점은 전체 이미지 프레임을 강조 표시합니다. 그런 다음 키보드의 화살표 키를 사용하여 프레임의 위치를 다시 지정할 수 있습니다.
   * 다음 네 `Tab` 정거장은 골조의 네 모퉁이이다. 프레임 모서리에 초점을 두면 모서리가 강조 표시됩니다. 키보드의 화살표 키를 사용하여 포커스가 있는 모서리를 이동할 수도 있습니다.
단일 [이미지의 스마트 자르기 또는 스마트 견본 편집을 참조하십시오.](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## 보조 기술 지원 [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] 유저 인터페이스 요소는 화면 판독기와 같은 보조 기술과 연동됩니다. 예를 들어 키보드 단축키를 사용하여 랜드마크를 탐색하거나 키보드 단축키 `D` 를 사용하여 영역을 탐색할 때 페이지의 랜드마크를 인식합니다 `R`. 제목 키보드 단축키를 사용하여 탐색할 때 제목 내레이션이 적용됩니다 `H`.

## 뷰어의 키보드 액세스 [!DNL Dynamic Media] 지원 {#keyboard-accessibility-for-dm-viewers}

모든 기본 뷰어 구성 요소는 고객의 키보드 [!DNL Dynamic Media] 접근성을 지원합니다.

Dynamic Media [Viewers 참조 안내서의 키보드 액세스 가능성 및 내비게이션을](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) 참조하십시오.

## 시청자의 보조 기술 [!DNL Dynamic Media] 지원 {#assistive-technology-support-for-dm-viewers}

모든 [!DNL Dynamic Media] 뷰어 구성 요소는 ARIA(Accessible Rich Internet Application) 역할 및 속성을 지원하여 화면 판독기와 같은 보조 기술과의 통합을 향상시킵니다.
Dynamic **Media Viewers Reference Guide의 사용자 정의 뷰어 항목에 있는 보조 기술 지원** 도움말 항목을 참조하십시오. 예를 들어 비디오 뷰어에 대한 [보조 기술 지원](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) 또는 대화형 이미지 뷰어에 대한 [보조 기술 지원을](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) 참조하십시오.

>[!MORELIKETHIS]
>
>* [Adobe 솔루션에 대한 액세스 가능성](https://www.adobe.com/accessibility.html)
>* [액세스 가능성 [!DNL Experience Manager Assets]](/help/assets/accessibility.md)

