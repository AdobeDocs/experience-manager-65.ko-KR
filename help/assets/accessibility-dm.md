---
title: Dynamic Media에서의 접근성
description: Dynamic Media 및 Dynamic Media Viewer의 접근성 지원에 대해 알아봅니다.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: User, Admin
exl-id: bbdb800c-b6f8-4506-b8ac-daf64edcd6c0
source-git-commit: 01de1d5064f5ebf00acd2fe9f138d852f41f7273
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 1%

---

# [!DNL Dynamic Media]에서의 접근성  {#working-with-three-d-assets-dm}

[!DNL Dynamic Media] 는 작성 사용자 인터페이스에서 키보드 제어와 JAWS 및 NVDA 화면 판독기와 같은 보조 기술을 지원합니다.

## 에서 키보드 액세스 가능성 지원 [!DNL Dynamic Media]

왜냐면 [!DNL Dynamic Media] 은(는) [!DNL Adobe Experience Manager Assets]에서는 대부분의 키보드 제어 동작이 와 동일합니다 [!DNL Experience Manager Assets]. 예: `Cancel` 버튼 [!DNL Dynamic Media] 과 동일한 포커스 강조 표시가 있습니다. [!DNL Experience Manager Assets], 및에 반응함 `Spacebar` 에 키 [!DNL Experience Manager Assets]. 자세한 내용은 [자산의 키보드 단축키](/help/assets/accessibility.md#keyboard-shortcuts).

의 개별 사용자 인터페이스 요소에서 지원하는 키 입력 [!DNL Dynamic Media] 명확하고 발견하기 쉽습니다. 의 키보드 제어 [!DNL Dynamic Media] 은 다음 사항에 대한 것입니다.

* 사용 기능 `Tab` 및 `Shift+Tab` 페이지에서 대화형 요소 간을 탐색하기 위한 키 입력.
사용 `Tab` 입력 포커스를 탭 순서의 다음 사용자 인터페이스 요소로 이동합니다. 사용 `Shift+Tab` 입력 포커스를 이전 사용자 인터페이스 요소로 다시 가져옵니다.
초점 순번은 화면의 자연어 사용자 인터페이스 요소 위치를 따르며, 왼쪽에서 오른쪽, 위에서 아래로 이동합니다. 또한 필드에 오류가 있으면 키를 누를 수 있습니다 `Tab` 포커스를 이동합니다.
* 사용 기능 `Spacebar` 및 `Enter` 키 - 단추 및 드롭다운 목록과 같은 표준 사용자 인터페이스 요소를 활성화합니다.
* 활성 요소에서 키보드 포커스를 강조 표시하는 기능을 제공합니다. 입력 포커스가 있는 사용자 인터페이스 요소는 사용자 인터페이스 요소 주위에 렌더링되는 테두리로 시각적 포커스 표시를 수신한다.
* 핫스팟 편집기에서 화살표 키와 같은 일부 사용자 지정 키 입력을 사용하여 복잡한 사용자 인터페이스 요소와 상호 작용하여 핫스팟 위치를 변경할 수 있습니다.
* 대화형 비디오 편집기에서 `Spacebar` 이미지를 선택하여 세그먼트에 추가합니다. 또한 `Backspace` 키를 사용하여 **[!UICONTROL 컨텐츠]** 탭. 또한 `Tab` 페이지에서 대화형 요소 간을 탐색하기 위해 원하는 대로 작동합니다.
* 이미지 자르기/스마트 자르기 편집기에서 다음을 수행할 수 있습니다.
   * 화살표 키를 사용하여 프레임 크기를 자르거나 이미지 위치 변경 또는 둘 다를 선택합니다.
   * 첫 번째 `Tab` stop은 전체 이미지 프레임을 강조 표시합니다. 그런 다음 키보드에서 화살표 키를 사용하여 프레임 위치를 변경할 수 있습니다.
   * 다음 4개 `Tab` 정차는 프레임의 네 코너입니다. 프레임 모서리에 포커스를 놓으면 모서리가 강조 표시됩니다. 키보드의 화살표 키를 사용하여 포커스가 있는 모서리를 이동할 수도 있습니다.
자세한 내용은 [단일 이미지의 스마트 자르기 또는 스마트 견본 편집](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## 에서 보조 기술 지원 [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] 사용자 인터페이스 요소는 화면 판독기와 같은 보조 기술과 함께 작동합니다. 예를 들어 키보드 단축키를 사용하여 랜드마크를 탐색할 때 페이지의 랜드마크를 인식합니다 `D` 키보드 단축키를 사용하는 영역 또는 `R`. 또한 제목 키보드 단축키를 사용하여 탐색할 때 제목 내레이션이 적용됩니다 `H`.

## 에서 키보드 액세스 가능성 지원 [!DNL Dynamic Media] 뷰어 {#keyboard-accessibility-for-dm-viewers}

모든 기본 제공 [!DNL Dynamic Media] 뷰어 구성 요소는 고객을 위한 키보드 액세스 가능성을 지원합니다.

자세한 내용은 [키보드 액세스 가능성 및 탐색](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) ( Dynamic Media Viewers 참조 안내서).

## 에서 보조 기술 지원 [!DNL Dynamic Media] 뷰어 {#assistive-technology-support-for-dm-viewers}

모두 [!DNL Dynamic Media] 뷰어 구성 요소는 ARIA(Accessible Rich Internet Applications) 역할 및 속성을 지원하여 화면 판독기와 같은 보조 기술과의 통합을 개선합니다.
자세한 내용은 **보조 기술 지원** Dynamic Media Viewers 참조 안내서의 사용자 지정 뷰어 항목의 도움말 항목입니다. 예를 들어 [보조 기술 지원](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) 비디오 뷰어용 또는 [보조 기술 지원](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) 대화형 이미지 뷰어용.

## Dynamic Media에서 닫힌 캡션 지원 {#closed-caption-support}

Dynamic Media에서는 자막을 사용하여 비디오 및 응용 비디오 세트 제공을 지원합니다. 비디오 컨텐츠 위에 캡션을 표시해야 합니다.

자세한 내용은 [Dynamic Media의 비디오 - 비디오에 자막 또는 자막 추가](/help/assets/video.md#adding-captions-to-video).

>[!MORELIKETHIS]
>
>* [Adobe 솔루션에 대한 접근성](https://www.adobe.com/accessibility.html)
>* [ [!DNL Experience Manager Assets]](/help/assets/accessibility.md)에서의 접근성

