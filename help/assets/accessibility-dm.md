---
title: Dynamic Media에서의 접근성
description: Dynamic Media 및 Dynamic Media Viewer의 접근성 지원에 대해 알아봅니다.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: User, Admin
exl-id: bbdb800c-b6f8-4506-b8ac-daf64edcd6c0
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---

# 에서의 접근성 [!DNL Dynamic Media] {#working-with-three-d-assets-dm}

[!DNL Dynamic Media] 는 작성 사용자 인터페이스에서 키보드 제어와 JAWS 및 NVDA 화면 판독기와 같은 보조 기술을 지원합니다.

## 의 키보드 접근성 지원 [!DNL Dynamic Media]

이유 [!DNL Dynamic Media] 은(는) 다음에 대한 플러그인입니다. [!DNL Adobe Experience Manager Assets], 대부분의 키보드 제어 동작은 에서와 같습니다 [!DNL Experience Manager Assets]. 예를 들어 `Cancel` 단추 입력 [!DNL Dynamic Media] 과 동일한 포커스 강조 표시 있음 [!DNL Experience Manager Assets]및 이에 대한 응답 `Spacebar` 의 키 [!DNL Experience Manager Assets]. 다음을 참조하십시오 [자산의 키보드 단축키](/help/assets/accessibility.md#keyboard-shortcuts).

의 개별 사용자 인터페이스 요소에서 지원하는 키 입력 [!DNL Dynamic Media] 명확하고 쉽게 찾을 수 있습니다. 의 키보드 제어 [!DNL Dynamic Media] 은(는) 다음에 대해 설명합니다.

* 사용 기능 `Tab` 및 `Shift+Tab` 페이지의 대화형 요소 사이를 이동하는 키 입력.
사용 `Tab` 탭 순서에서 다음 사용자 인터페이스 요소로 입력 포커스를 전환합니다. `Shift+Tab` 입력 포커스를 이전 사용자 인터페이스 요소로 다시 가져옵니다.
포커스 트래버스는 화면의 자연어 사용자 인터페이스 요소 위치를 따라가며 왼쪽에서 오른쪽으로, 위에서 아래로 이동합니다. 또한 오류가 있는 필드는 을 누를 수 있습니다. `Tab` 포커스를 이동합니다.
* 사용 기능 `Spacebar` 및 `Enter` 단추 및 드롭다운 목록과 같은 표준 사용자 인터페이스 요소를 활성화하는 키.
* 활성 요소에서 키보드 포커스 강조 표시를 확인하는 기능. 입력 포커스를 갖는 사용자 인터페이스 요소는 사용자 인터페이스 요소 주위에 렌더링된 경계로서 시각적 포커스 표시를 수신한다.
* 핫스팟 편집기에서 화살표 키와 같은 사용자 지정 키 입력을 사용하여 복잡한 사용자 인터페이스 요소와 상호 작용하여 핫스팟의 위치를 변경할 수 있습니다.
* 대화형 비디오 편집기에서 `Spacebar` 이미지를 선택하여 세그먼트에 추가합니다. 또한 `Backspace` 선택한 항목을 삭제할 키 **[!UICONTROL 콘텐츠]** 탭. 또한 누르기 `Tab` 는 페이지의 대화형 요소 사이를 탐색하기 위해 원하는 대로 작동합니다.
* 이미지 자르기/스마트 자르기 편집기에서 다음 작업을 수행할 수 있습니다.
   * 화살표 키를 사용하여 프레임 크기를 자르거나 이미지 위치를 변경하거나 둘 다 수행합니다.
   * 첫 번째 `Tab` [정지]를 선택하면 전체 이미지 프레임이 강조 표시됩니다. 그런 다음 키보드의 화살표 키를 사용하여 프레임의 위치를 변경할 수 있습니다.
   * 다음 4개 `Tab` 정지점은 프레임의 네 모서리입니다. 프레임 모서리에 포커스를 놓으면 코너가 강조 표시됩니다. 키보드의 화살표 키를 사용하여 포커스가 있는 모서리를 이동할 수 있습니다.
다음을 참조하십시오 [단일 이미지의 스마트 자르기 또는 스마트 색상 견본 편집](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## 의 보조 기술 지원 [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] 사용자 인터페이스 요소는 화면 판독기와 같은 보조 기술과 함께 작동합니다. 예를 들어 키보드 단축키를 사용하여 랜드마크를 탐색할 때 페이지의 랜드마크를 인식합니다 `D` 또는 키보드 단축키를 사용하는 지역 `R`. 또한 제목 키보드 단축키를 사용하여 탐색할 때 제목의 내레이션이 적용됩니다 `H`.

## 의 키보드 접근성 지원 [!DNL Dynamic Media] 뷰어 {#keyboard-accessibility-for-dm-viewers}

기본 제공 [!DNL Dynamic Media] 뷰어 구성 요소는 고객을 위한 키보드 접근성을 지원합니다.

다음을 참조하십시오 [키보드 접근성 및 탐색](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) ( Dynamic Media 뷰어 참조 안내서)를 참조하십시오.

## 의 보조 기술 지원 [!DNL Dynamic Media] 뷰어 {#assistive-technology-support-for-dm-viewers}

모두 [!DNL Dynamic Media] 뷰어 구성 요소는 ARIA(Accessible Rich Internet Applications) 역할 및 속성을 지원하여 화면 판독기와 같은 보조 기술과의 통합을 향상시킵니다.
다음을 참조하십시오. **보조 기술 지원** Dynamic Media 뷰어 참조 안내서의 뷰어 사용자 지정 항목에 있는 도움말 항목입니다. 예를 들어 다음을 참조하십시오. [보조 기술 지원](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) 비디오 뷰어용 또는 [보조 기술 지원](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) 대화형 이미지 뷰어용.

## Dynamic Media의 자막 지원 {#closed-caption-support}

Dynamic Media은 자막이 있는 비디오 및 적응형 비디오 세트 배달을 지원합니다. 캡션은 비디오 콘텐츠 위에 표시되어야 합니다.

다음을 참조하십시오 [Dynamic Media의 비디오 - 비디오에 폐쇄 캡션 또는 자막 추가](/help/assets/video.md#adding-captions-to-video).

>[!MORELIKETHIS]
>
>* [Adobe 솔루션에 대한 접근성](https://www.adobe.com/accessibility.html)
>* [에서의 접근성 [!DNL Experience Manager Assets]](/help/assets/accessibility.md)
