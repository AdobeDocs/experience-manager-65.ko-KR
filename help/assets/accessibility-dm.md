---
title: Dynamic Media의 액세스 가능성
description: Dynamic Media 및 Dynamic Media 뷰어의 액세스 가능성 지원에 대한 자세한 내용
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: e95f26cc1a084358b6bcb78605e3acb98f257b66
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---


# [!DNL Dynamic Media] {#working-with-three-d-assets-dm}의 액세스 가능성

[!DNL Dynamic Media] 저작 유저 인터페이스에서 JAWS 및 NVDA 화면 판독기와 같은 키보드 제어 및 보조 기술을 지원합니다.

## [!DNL Dynamic Media]의 키보드 접근성 지원

[!DNL Dynamic Media]은(는) [!DNL Adobe Experience Manager Assets]의 플러그인이기 때문에 대부분의 키보드 제어 동작은 [!DNL Experience Manager Assets]의 경우와 동일합니다. 예를 들어 [!DNL Dynamic Media]의 `Cancel` 버튼은 [!DNL Experience Manager Assets]에서와 동일한 초점 강조 표시를 가지며 [!DNL Experience Manager Assets]에서와 같이 `Spacebar` 키에 응답합니다. 에셋](/help/assets/accessibility.md#keyboard-shortcuts)의 [키보드 단축키를 참조하십시오.

[!DNL Dynamic Media]의 개별 사용자 인터페이스 요소에서 지원하는 키 입력은 대부분의 경우 명확하고 쉽게 찾을 수 있습니다. [!DNL Dynamic Media]의 키보드 컨트롤은 다음과 같습니다.

* `Tab` 및 `Shift+Tab` 키 입력을 사용하여 페이지에서 대화형 요소 간을 탐색할 수 있습니다.
`Tab`을 사용하면 입력 포커스를 탭 순서의 다음 사용자 인터페이스 요소로 이동합니다.`Shift+Tab`을(를) 사용하면 입력 포커스가 이전 사용자 인터페이스 요소로 돌아갑니다.
초점 순차는 화면의 자연스러운 유저 인터페이스 요소 위치를 따르며 왼쪽에서 오른쪽, 위에서 아래로 이동합니다. 또한 필드에 오류가 있으면 `Tab`을 눌러 포커스를 이동할 수 있습니다.
* `Spacebar` 및 `Enter` 키를 사용하여 단추, 드롭다운 목록 등과 같은 표준 사용자 인터페이스 요소를 활성화할 수 있습니다.
* 활성 요소에서 키보드 포커스를 강조 표시하는 기능을 확인할 수 있습니다. 입력 포커스가 있는 사용자 인터페이스 요소는 사용자 인터페이스 요소 주위에 렌더링된 테두리로 시각적 포커스를 받을 수 있습니다.
* 핫스팟 편집기에서 화살표 키와 같은 사용자 정의 키 입력을 사용하여 복잡한 사용자 인터페이스 요소와 상호 작용하여 핫스팟의 위치를 변경할 수 있습니다.
* 대화형 비디오 편집기에서 `Spacebar`을 사용하여 이미지를 선택하고 세그먼트에 추가할 수 있습니다. 또한 `Backspace` 키를 사용하여 **[!UICONTROL 컨텐트]** 탭에서 선택한 항목을 삭제할 수 있습니다. 또한 `Tab`을 누르면 페이지에서 대화형 요소 간을 탐색할 수 있습니다.
* 이미지 자르기/스마트 자르기 편집기에서 다음을 수행할 수 있습니다.
   * 화살표 키를 사용하여 프레임 크기를 자르거나 이미지를 다시 배치하거나 두 가지 모두 배치할 수 있습니다.
   * 첫 번째 `Tab` 중지는 전체 이미지 프레임을 강조 표시합니다. 키보드의 화살표 키를 사용하여 프레임의 위치를 다시 지정할 수 있습니다.
   * 다음 4개의 `Tab` 정지는 프레임의 4개 모퉁이입니다. 프레임 모서리에 포커스가 있으면 모퉁이가 강조 표시됩니다. 키보드의 화살표 키를 사용하여 포커스가 있는 모퉁이를 이동할 수 있습니다.
자세한 내용은 [단일 이미지의 스마트 자르기 또는 스마트 견본 편집](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image) 참조

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## [!DNL Dynamic Media] {#assistive-technology-support-for-dm}의 보조 기술 지원

[!DNL Dynamic Media] 유저 인터페이스 요소는 화면 판독기와 같은 보조 기술과 연동됩니다. 예를 들어 키보드 단축키 `D` 또는 키보드 단축키 `R`를 사용하여 랜드마크를 탐색할 때 페이지의 랜드마크를 인식합니다. 제목 키보드 단축키 `H`을 사용하여 탐색할 때 제목이 나레이션됩니다.

## [!DNL Dynamic Media] 뷰어 {#keyboard-accessibility-for-dm-viewers}에서 키보드 액세스 가능성 지원

모든 기본 [!DNL Dynamic Media] 뷰어 구성 요소는 고객의 키보드 액세스 가능성을 지원합니다.

Dynamic Media 뷰어 참조 안내서의 [키보드 액세스 가능성 및 탐색](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html)을 참조하십시오.

## [!DNL Dynamic Media] 뷰어에서 보조 기술 지원 {#assistive-technology-support-for-dm-viewers}

모든 [!DNL Dynamic Media] 뷰어 구성 요소는 ARIA(Accessible Rich Internet Application) 역할 및 속성을 지원하여 화면 판독기와 같은 보조 기술과의 통합을 향상시킵니다.
Dynamic Media 뷰어 참조 안내서의 사용자 정의 뷰어 항목의 **보조 기술 지원** 도움말 항목을 참조하십시오. 예를 들어 비디오 뷰어의 경우 [보조 기술 지원](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) 또는 대화형 이미지 뷰어의 [보조 기술 지원](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only)을 참조하십시오.

>[!MORELIKETHIS]
>
>* [Adobe 솔루션에 대한 액세스 가능성](https://www.adobe.com/accessibility.html)
>* [액세스 가능성 [!DNL Experience Manager Assets]](/help/assets/accessibility.md)

