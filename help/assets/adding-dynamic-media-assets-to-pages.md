---
title: 페이지에 Dynamic Media 자산 추가
description: Adobe Experience Manager의 페이지에 Dynamic Media 구성 요소를 추가하는 방법
uuid: b5e982f5-fa1c-478a-bcb3-a1ef980df201
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 97a5f018-8255-4b87-9d21-4a0fdf740e4d
docset: aem65
translation-type: tm+mt
source-git-commit: 863c3292d272ba4c80a80645262919e55870a437
workflow-type: tm+mt
source-wordcount: '3100'
ht-degree: 27%

---


# 페이지에 Dynamic Media 자산 추가{#adding-dynamic-media-assets-to-pages}

웹 사이트에서 사용하는 자산에 Dynamic Media 기능을 추가하려면 페이지에 직접 **Dynamic Media**, **대화형 미디어**, **파노라마 미디어** 또는 **비디오 360 미디어** 구성 요소를 추가할 수 있습니다. 이렇게 하려면 레이아웃 모드로 전환하고 Dynamic Media 구성 요소를 활성화합니다. 그런 다음이 구성 요소를 페이지에 추가하고 자산을 구성 요소에 추가할 수 있습니다. Dynamic Media 구성 요소는 편리하게도 이미지를 추가하는지 아니면 비디오를 추가하는지 여부와 그에 따라 사용 가능한 구성 옵션이 달라집니다.

Adobe Experience Manager을 WCM으로 사용하는 경우 페이지에 바로 Dynamic Media 자산을 추가합니다. WCM에 제3자를 사용하는 경우 [link](/help/assets/linking-urls-to-yourwebapplication.md) 또는 [embed](/help/assets/embed-code.md) 에셋을 참조하십시오. 응답형 제3자 웹 사이트는 응답형 사이트[에 최적화된 이미지 제공을 참조하십시오.](/help/assets/responsive-site.md)

>[!NOTE]
>
>Experience Manager의 페이지에 자산을 추가하기 전에 자산을 게시해야 합니다. [Dynamic Media 자산 게시](/help/assets/publishing-dynamicmedia-assets.md)를 참조하십시오.

## 페이지에 Dynamic Media 구성 요소 추가 {#adding-a-dynamic-media-component-to-a-page}

3D 미디어, Dynamic Media, 대화형 미디어, 파노라마 미디어, 스마트 자르기 비디오 또는 비디오 360 미디어 구성 요소를 페이지에 추가하는 것은 페이지에 구성 요소를 추가하는 것과 같습니다. Dynamic Media 구성 요소는 다음 섹션에 설명되어 있습니다.

1. Experience Manager에서 Dynamic Media 구성 요소를 추가할 페이지를 엽니다.
1. 페이지 왼쪽의 패널에서(사이드 패널의 표시를 전환해야 할 수 있음) **[!UICONTROL 구성 요소]** 아이콘을 클릭합니다.
1. **[!UICONTROL 구성 요소]** 머리글 아래의 드롭다운 목록에서 **[!UICONTROL Dynamic Media.]**

   사용 가능한 Dynamic Media 구성 요소 목록이 없는 경우 사용하려는 Dynamic Media 구성 요소를 활성화해야 합니다. [Dynamic Media 구성 요소 활성화](#enabling-dynamic-media-components)를 참조하십시오.

   ![6_5_360video_wcmcomponent](/help/assets/assets/6_5_360video_wcmcomponent.png)

1. 사용할 **[!UICONTROL Dynamic Media]** 구성 요소를 드래그하여 페이지의 원하는 위치에 놓습니다.

1. 마우스 포인터를 구성 요소 바로 위에 놓습니다. 구성 요소가 파란색 상자로 둘러싸인 경우 한 번 탭하여 구성 요소의 도구 모음을 표시합니다. **[!UICONTROL 구성(렌치)]** 아이콘을 누릅니다.

   ![6_5_360video_wcmcomponentconfigure](/help/assets/assets/6_5_360video_wcmcomponentconfigure.png)

1. 페이지에 배치한 Dynamic Media 구성 요소에 따라 구성 대화 상자가 열립니다. [필요한 구성 요소의 ](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components) 옵션을 설정합니다.

   아래 예제는 Dynamic Media **[!UICONTROL Video 360 Media]** 구성 요소 대화 상자와 뷰어 사전 설정 드롭다운 목록에서 사용할 수 있는 옵션을 보여줍니다.

   ![비디오 360 미디어 구성 요소](assets/6_5_360video_wcmcomponentviewerpreset.png)

   Dynamic Media Video 360 미디어 구성 요소.

1. 완료되면 대화 상자의 오른쪽 상단에 있는 체크 표시를 눌러 변경 사항을 저장합니다.

### Dynamic Media 구성 요소 {#enabling-dynamic-media-components} 활성화

페이지에 추가할 수 있는 Dynamic Media 구성 요소가 없는 경우 먼저 사용할 구성 요소를 활성화해야 합니다.

1. Experience Manager에서 Dynamic Media 구성 요소를 추가할 페이지를 엽니다.
1. 페이지 상단 근처의 도구 모음 왼쪽의 페이지 정보 아이콘을 누른 다음 드롭다운 목록에서 **[!UICONTROL 템플릿 편집]**&#x200B;을 누릅니다.

   ![편집 템플릿](/help/assets/assets-dm/edit-template.png)

1. 페이지 상단 근처의 도구 모음 오른쪽에 있는 드롭다운 목록에서 **[!UICONTROL 구조를 누릅니다.]**

   ![정책](/help/assets/assets-dm/structure-mode.png)

1. 페이지 하단 근처에 있는 **[!UICONTROL 레이아웃 컨테이너]**&#x200B;를 눌러 해당 도구 모음을 연 다음 정책 아이콘을 누릅니다.
1. **[!UICONTROL 레이아웃 컨테이너]** 페이지의 **[!UICONTROL 속성]** 머리글 아래에서 **[!UICONTROL 허용된 구성 요소]** 탭이 선택되어 있는지 확인합니다.

   ![허용된 구성 요소](/help/assets/assets-dm/allowed-components.png)

1. **[!UICONTROL Dynamic Media.]**&#x200B;이 표시될 때까지 스크롤합니다.
1. **[!UICONTROL Dynamic Media]**&#x200B;의 왼쪽에 있는 > 아이콘을 눌러 목록을 확장하고 활성화할 Dynamic Media 구성 요소를 선택합니다.

   ![Dynamic Media 구성 요소 목록](/help/assets/assets-dm/dm-components-select.png)

1. **[!UICONTROL 레이아웃 컨테이너]** 페이지의 오른쪽 위 모서리 근처에 있는 완료(확인 표시) 아이콘을 탭합니다.

1. 페이지 위쪽 근처 도구 모음 오른쪽의 드롭다운 목록에서 **[!UICONTROL 초기 컨텐츠]**&#x200B;를 누른 다음 [Dynamic Media 구성 요소를 평소대로 페이지](#adding-a-dynamic-media-component-to-a-page)에 추가합니다.

## Dynamic Media 구성 요소 지역화 {#localizing-dynamic-media-components}

다음 두 가지 방법 중 하나로 Dynamic Media 구성 요소를 현지화할 수 있습니다.

* 사이트의 웹 페이지 내에서 **[!UICONTROL 속성]**&#x200B;을 열고 **[!UICONTROL 고급]** 탭을 선택합니다. 현지화를 위해 원하는 언어를 선택합니다.

   ![chlimage_1-172](assets/chlimage_1-538.png)

* 사이트 선택기에서 원하는 페이지 또는 페이지 그룹을 선택합니다. **[!UICONTROL 속성]**&#x200B;을 누르고 **[!UICONTROL 고급]** 탭을 선택합니다. 현지화를 위해 원하는 언어를 선택합니다.

   >[!NOTE]
   >
   >현재 **[!UICONTROL 언어]** 메뉴에서 사용할 수 있는 일부 언어에는 토큰이 할당되지 않았습니다.

## Dynamic Media 구성 요소 {#dynamic-media-components}

Dynamic Media 구성 요소는 **[!UICONTROL 구성 요소]** 아이콘을 누른 다음 **[!UICONTROL Dynamic Media에서 필터링할 때 사용할 수 있습니다.]**

사용할 수 있는 Dynamic Media 구성 요소는 다음과 같습니다.

* **[!UICONTROL Dynamic Media]**  - 이미지, 비디오, e카탈로그 및 스핀 세트와 같은 에셋에 사용합니다.
* **[!UICONTROL 인터랙티브한 미디어]**  - 인터랙티브한 비디오, 인터랙티브한 이미지 또는 회전 메뉴 세트와 같은 인터랙티브한 자산에 사용합니다.
* **[!UICONTROL 파노라마 미디어]**  - 파노라마 이미지 또는 파노라마 VR 이미지 자산에 사용합니다.
* **[!UICONTROL 비디오 360 미디어]**  - 360 비디오 및 360 VR 비디오 에셋에 사용합니다.

>[!NOTE]
>
>이러한 구성 요소는 기본적으로 사용할 수 없으며 사용하기 전에 템플릿 편집기를 통해 사용할 수 있어야 합니다. [템플릿 편집기](/help/sites-authoring/templates.md#editing-templates-template-authors)에서 사용할 수 있게 되면 다른 Experience Manager 구성 요소처럼 구성 요소를 페이지에 추가할 수 있습니다.

![6_5_dynamicmediawcmcomponents](assets/6_5_dynamicmediawcmcomponents.png)

### Dynamic Media 구성 요소 {#dynamic-media-component}

Dynamic Media 구성 요소는 스마트합니다.이미지를 추가하는지 아니면 비디오를 추가하는지에 따라 다양한 옵션이 제공됩니다. 이 구성 요소는 이미지 사전 설정, 이미지 세트와 같은 이미지 기반 뷰어, 스핀 세트, 혼합 미디어 세트 및 비디오를 지원합니다. 또한 뷰어는 반응형으로 작동하며 화면 크기는 화면 크기에 따라 자동으로 변경됩니다. 모든 뷰어는 HTML5 뷰어입니다.

>[!NOTE]
>
>웹 페이지에 다음이 있는 경우:
>
>* 동일한 페이지에서 사용되는 Dynamic Media 구성 요소의 여러 인스턴스.
>* 각 인스턴스는 동일한 자산 유형을 사용합니다.

>
>
해당 페이지의 각 Dynamic Media 구성 요소에 다른 뷰어 사전 설정을 할당할 수는 없습니다.
>
>그러나 페이지 내에서 동일한 유형의 자산을 사용하는 모든 Dynamic Media 구성 요소에 대해 동일한 뷰어 사전 설정을 사용할 수 있습니다.

Dynamic Media 구성 요소를 추가하고 **[!UICONTROL Dynamic Media 설정]**&#x200B;이 비어 있거나 자산을 제대로 추가할 수 없는 경우, 다음을 확인하십시오.

* [Dynamic Media를 활성화](/help/assets/config-dynamic.md)했습니다. Dynamic Media는 기본적으로 비활성화됩니다.
* 이미지에 피라미드형 tiff 파일이 있습니다. 다이내믹 미디어를 활성화하기 전에 가져온 이미지에는 피라미드형 tiff 파일이 없습니다.

#### 이미지 작업 시 {#when-working-with-images}

Dynamic Media 구성 요소를 사용하면 이미지 세트, 스핀 세트 및 혼합 미디어 세트를 포함한 다이내믹 이미지를 추가할 수 있습니다. 확대하거나 축소할 수 있고, 해당하는 경우 스핀 세트 내의 이미지를 회전하거나 다른 유형의 세트에서 이미지를 선택할 수 있습니다.

구성 요소에서 바로 뷰어 사전 설정, 이미지 사전 설정 또는 이미지 형식을 구성할 수도 있습니다. 이미지가 응답하도록 하기 위해 중단점을 설정하거나 응답형 이미지 사전 설정을 적용할 수 있습니다.

*구성 요소에서&#x200B;**[!UICONTROL 편집]**아이콘을 누른 다음&#x200B;**[!UICONTROL Dynamic Media 설정을 눌러 다음 Dynamic Media 설정을 편집해야 합니다.]***

![dm-settings-image-preset](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>기본적으로 Dynamic Media 이미지 구성 요소는 적응형입니다. 고정 크기로 설정하려면 **[!UICONTROL 너비]** 및 **[!UICONTROL 높이와 함께**[!UICONTROL &#x200B;고급&#x200B;]**탭의 구성 요소에서 설정합니다.]**

* **[!UICONTROL 뷰어 사전]** 설정 - 드롭다운 메뉴에서 기존 뷰어 사전 설정을 선택합니다. 보려는 뷰어 사전 설정이 표시되지 않을 경우 표시되도록 설정해야 할 수 있습니다. 뷰어 사전 설정 관리를 참조하십시오. 이미지 사전 설정을 사용 중일 때는 뷰어 사전 설정을 선택할 수 없고 그 반대의 경우도 마찬가지입니다.

   이미지 세트, 스핀 세트 또는 혼합 미디어 세트를 보는 경우 사용할 수 있는 유일한 선택 사항입니다. 표시되는 뷰어 사전 설정은 편리하게도 적절한 뷰어 사전 설정만 표시됩니다.

* **[!UICONTROL 뷰어 수정자]** - 뷰어 수정자는 이름=값 쌍의 형식을 &amp; 구분 기호와 함께 사용하고 뷰어 참조 안내서에 설명된 대로 뷰어를 변경할 수 있습니다. 뷰어 수정자의 예는 비디오 축소판의 다른 이미지를 설정하고 닫힌 캡션/자막 파일을 비디오와 연결하는 `posterimage=img.jpg&caption=text.vtt,1`입니다.

* **[!UICONTROL 이미지 사전 설정]** - 드롭다운 메뉴에서 기존 이미지 사전 설정을 선택합니다. 보려는 이미지 사전 설정이 표시되지 않을 경우 표시되도록 설정해야 할 수 있습니다. 이미지 사전 설정 관리를 참조하십시오. 이미지 사전 설정을 사용 중일 때는 뷰어 사전 설정을 선택할 수 없고 그 반대의 경우도 마찬가지입니다.

   이미지 세트, 스핀 세트 또는 혼합 미디어 세트를 보는 경우에는 이 선택 사항을 사용할 수 없습니다.

* **[!UICONTROL 이미지 수정자]** - 추가 이미지 명령을 제공하여 이미지 효과를 적용할 수 있습니다. 이러한 내용은 이미지 사전 설정 및 이미지 제공 명령 참조에 설명되어 있습니다.

   이미지 세트, 스핀 세트 또는 혼합 미디어 세트를 보는 경우에는 이 선택 사항을 사용할 수 없습니다.

* **[!UICONTROL 중단점]** - 응답형 사이트에서 이 자산을 사용하는 경우 이미지 중단점을 추가해야 합니다. 이미지 중단점은 쉼표(,)로 구분해야 합니다. 이 선택 사항은 이미지 사전 설정에 정의된 높이나 폭이 없는 경우에 작동합니다.

   이미지 세트, 스핀 세트 또는 혼합 미디어 세트를 보는 경우에는 이 선택 사항을 사용할 수 없습니다.

   구성 요소에서 **[!UICONTROL 편집]**&#x200B;을 눌러 다음 고급 설정을 편집할 수 있습니다.

* **[!UICONTROL 제목]** - 이미지의 제목을 변경합니다.

* **[!UICONTROL 대체 텍스트]** - 그래픽을 해제한 사용자를 위해 이미지에 제목을 추가합니다.

   이미지 세트, 스핀 세트 또는 혼합 미디어 세트를 보는 경우에는 이 선택 사항을 사용할 수 없습니다.

* **[!UICONTROL URL, 여는 위치]** - 링크를 열도록 자산을 설정할 수 있습니다. URL을 설정하고 여는 위치에 같은 창에서 열지 또는 새 창에서 열지를 지정합니다.

   이미지 세트, 스핀 세트 또는 혼합 미디어 세트를 보는 경우에는 이 선택 사항을 사용할 수 없습니다.

* **[!UICONTROL 너비]** - 이미지의 크기를 고정하려면 값을 픽셀 단위로 입력합니다. 이 값을 공백으로 두면 자산이 적응형으로 설정됩니다.

* **[!UICONTROL 높이]** - 이미지의 크기를 고정하려면 값을 픽셀 단위로 입력합니다. 이 값을 공백으로 두면 자산이 적응형으로 설정됩니다.


#### 비디오 작업 시 {#when-working-with-video}

Dynamic Media 구성 요소를 사용하여 웹 페이지에 다이내믹 비디오를 추가하십시오. 구성 요소를 편집할 때 페이지에서 비디오를 재생하기 위해 사전 설정된 비디오 뷰어 사전 설정을 사용하도록 선택할 수 있습니다.

![chlimage_1-173](assets/chlimage_1-540.png)

구성 요소에서 **[!UICONTROL 편집]**&#x200B;을 클릭하여 다음 Dynamic Media 설정을 편집해야 합니다.

>[!NOTE]
>
>기본적으로 Dynamic Media 비디오 구성 요소는 적응형입니다. 고정 크기로 설정하려면 **[!UICONTROL 고급]** 탭에서 **[!UICONTROL 폭]** 및 **[!UICONTROL 높이]**&#x200B;로 구성 요소를 설정하십시오.

* **[!UICONTROL 뷰어 사전]** 설정 - 드롭다운 메뉴에서 기존 비디오 뷰어 사전 설정을 선택합니다. 보려는 뷰어 사전 설정이 표시되지 않을 경우 표시되도록 설정해야 할 수 있습니다. 뷰어 사전 설정 관리를 참조하십시오.

* **[!UICONTROL 뷰어 수정자]**—뷰어 수정자는 이름=값 쌍의 형식을 &amp; 구분 기호와 함께 사용하고 Adobe 뷰어 참조 안내서에 설명된 대로 뷰어를 변경할 수 있습니다. 뷰어 수정자의 예는 `posterimage=img.jpg&caption=text.vtt,1`입니다.

   예를 들어 뷰어 수정자를 사용하여 다음을 수행할 수 있습니다.

   * 캡션 파일을 비디오와 연결:[캡션][https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html)
   * 탐색 파일을 비디오와 연결:[내비게이션][https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html)

   구성 요소에서 **[!UICONTROL 편집]**&#x200B;을 클릭하여 다음 고급 설정을 편집할 수 있습니다.

* **[!UICONTROL 제목]** - 비디오 제목을 변경합니다.

* **[!UICONTROL 너비]** - 이미지의 크기를 고정하려면 값을 픽셀 단위로 입력합니다. 이 값을 공백으로 두면 자산이 적응형으로 설정됩니다.

* **[!UICONTROL 높이]** - 이미지의 크기를 고정하려면 값을 픽셀 단위로 입력합니다. 이 값을 공백으로 두면 자산이 적응형으로 설정됩니다.

#### 스마트 자르기 작업 시 {#when-working-with-smart-crop}

Dynamic Media 구성 요소를 사용하여 웹 페이지에 스마트 자르기 이미지 자산을 추가합니다. 구성 요소를 편집할 때 페이지에서 비디오를 재생하기 위해 사전 설정된 비디오 뷰어 사전 설정을 사용하도록 선택할 수 있습니다.

[이미지 프로필](/help/assets/image-profiles.md)도 참조하십시오.

![dm-settings-smart-crop](assets/dm-settings-smart-crop.png)

구성 요소에서 **[!UICONTROL 편집]**&#x200B;을 클릭하여 다음 Dynamic Media 설정을 편집해야 합니다.

>[!NOTE]
>
>기본적으로 Dynamic Media 이미지 구성 요소는 적응형입니다. 고정 크기로 설정하려면 **[!UICONTROL 너비]** 및 **[!UICONTROL 높이와 함께**[!UICONTROL &#x200B;고급&#x200B;]**탭의 구성 요소에서 설정합니다.]**

* **[!UICONTROL 이미지 수정자]** - 추가 이미지 명령을 제공하여 이미지 효과를 적용할 수 있습니다. 이러한 내용은 이미지 사전 설정 및 이미지 제공 명령 참조에 설명되어 있습니다.

   이미지 세트, 스핀 세트 또는 혼합 미디어 세트를 보는 경우에는 이 선택 사항을 사용할 수 없습니다.

   구성 요소에서 **[!UICONTROL 편집]**&#x200B;을 클릭하여 다음 고급 설정을 편집할 수 있습니다.

* **[!UICONTROL 제목]** - 스마트 자르기 이미지의 제목을 변경합니다.

* **[!UICONTROL 대체 텍스트]** - 그래픽을 해제한 사용자를 위해 스마트 자르기 이미지에 제목을 추가합니다.

   이미지 세트, 스핀 세트 또는 혼합 미디어 세트를 보는 경우에는 이 선택 사항을 사용할 수 없습니다.

* **[!UICONTROL URL, 여는 위치]** - 링크를 열도록 자산을 설정할 수 있습니다. URL을 설정하고 여는 위치에 같은 창에서 열지 또는 새 창에서 열지를 지정합니다.

   이미지 세트, 스핀 세트 또는 혼합 미디어 세트를 보는 경우에는 이 선택 사항을 사용할 수 없습니다.

* **[!UICONTROL 너비]** - 이미지의 크기를 고정하려면 값을 픽셀 단위로 입력합니다. 이 값을 공백으로 두면 자산이 적응형으로 설정됩니다.

* **[!UICONTROL 높이]** - 이미지의 크기를 고정하려면 값을 픽셀 단위로 입력합니다. 이 값을 공백으로 두면 자산이 적응형으로 설정됩니다.

### 대화형 미디어 구성 요소 {#interactive-media-component}

대화형 미디어 구성 요소는 핫스팟이나 이미지 맵과 같은 상호 작용이 있는 자산을 위한 것입니다. 대화형 이미지, 대화형 비디오 또는 회전 배너가 있는 경우 **[!UICONTROL 대화형 미디어]** 구성 요소를 사용하십시오.

인터랙티브 미디어 구성 요소는 스마트합니다.이미지를 추가하는지 아니면 비디오를 추가하는지에 따라 다양한 옵션이 제공됩니다. 또한 뷰어는 반응형으로 작동하며 화면 크기는 화면 크기에 따라 자동으로 변경됩니다. 모든 뷰어는 HTML5 뷰어입니다.

>[!NOTE]
>
>웹 페이지에 다음이 있는 경우:
>
>* 동일한 페이지에서 사용되는 대화형 미디어 구성 요소의 여러 인스턴스.
>* 각 인스턴스는 동일한 자산 유형을 사용합니다.

>
>
해당 페이지의 각 Interactive Media 구성 요소에 다른 뷰어 사전 설정을 할당할 수는 없습니다.
>
>그러나 페이지 내에서 동일한 유형의 자산을 사용하는 모든 대화형 미디어 구성 요소에 대해 동일한 뷰어 사전 설정을 사용할 수 있습니다.

![chlimage_1-174](assets/chlimage_1-541.png)

구성 요소에서 **[!UICONTROL 편집]**&#x200B;을 탭하여 다음 **[!UICONTROL 일반]** 설정을 편집할 수 있습니다.

* **[!UICONTROL 뷰어 사전]** 설정 - 드롭다운 메뉴에서 기존 뷰어 사전 설정을 선택합니다. 보려는 뷰어 사전 설정이 표시되지 않을 경우 표시되도록 설정해야 할 수 있습니다. 뷰어 사전 설정을 사용하려면 먼저 게시해야 합니다. 뷰어 사전 설정 관리를 참조하십시오.

* **[!UICONTROL 제목]** - 비디오 제목을 변경합니다.

* **[!UICONTROL 너비]** - 이미지의 크기를 고정하려면 값을 픽셀 단위로 입력합니다. 이 값을 공백으로 두면 자산이 적응형으로 설정됩니다.

* **[!UICONTROL 높이]** - 이미지의 크기를 고정하려면 값을 픽셀 단위로 입력합니다. 이 값을 공백으로 두면 자산이 적응형으로 설정됩니다.

   구성 요소에서 **[!UICONTROL 편집]**&#x200B;을 클릭하여 다음 **[!UICONTROL 장바구니에 추가]** 설정을 편집할 수 있습니다.

* **[!UICONTROL 제품 자산 표시]** - 기본적으로 이 값이 선택됩니다. 제품 자산은 상거래 모듈에 정의된 제품의 이미지를 보여줍니다. 제품 자산을 표시하지 않도록 하려면 확인 표시를 지우십시오.

* **[!UICONTROL 제품 가격]** 표시 - 기본적으로 이 값이 선택됩니다. 제품 가격은 상거래 모듈에 정의된 항목 가격을 보여줍니다. 제품 가격을 표시하지 않도록 하려면 확인 표시를 지우십시오.

* **[!UICONTROL 제품 양식]** 표시 - 기본적으로 이 값은 선택되어 있지 않습니다. 제품 양식에는 크기 및 색상과 같은 모든 제품 변형이 포함됩니다. 제품 변형을 표시하지 않도록 하려면 확인 표시를 지우십시오.

### 파노라마 미디어 구성 요소 {#panoramic-media-component}

파노라마 미디어 구성 요소는 구형 파노라마 이미지인 자산을 위한 것입니다. 이러한 이미지는 회의실, 속성, 위치 또는 가로의 360° 보기 환경을 제공합니다. 이미지가 구형 파노라마의 자격을 얻으려면 다음 중 하나 또는 둘 다 있어야 합니다.

* 2:1 종횡비.
* `equirectangular` 또는 (`spherical` + `panorama`) 또는 (`spherical` + `panoramic`) 키워드로 태그가 지정됩니다. [태그 사용](/help/sites-authoring/tags.md)을 참조하십시오.

종횡비와 키워드 기준은 모두 자산 세부 사항 페이지와 **[!UICONTROL 파노라마 미디어]** WCM 구성 요소에 대한 파노라마 자산에 적용됩니다.

>[!NOTE]
>
>웹 페이지에 다음이 있는 경우:
>
>* 동일한 페이지에서 사용 중인 **[!UICONTROL 파노라마 미디어]** 구성 요소의 여러 인스턴스가 있습니다.
>* 각 인스턴스는 동일한 자산 유형을 사용합니다.

>
>
해당 페이지의 각 **[!UICONTROL 파노라마 미디어]** 구성 요소에 다른 뷰어 사전 설정을 할당할 수 없습니다.
>
>그러나 페이지 내에서 동일한 유형의 자산을 사용하는 모든 파노라마 미디어 구성 요소에 대해 동일한 뷰어 사전 설정을 사용할 수 있습니다.

![panasonic-media-viewer-preset](assets/panoramic-media-viewer-preset.png)

구성 요소에서 **[!UICONTROL 구성]**&#x200B;을 탭하여 다음 설정을 편집할 수 있습니다.

* **[!UICONTROL 뷰어 사전]** 설정 - 뷰어 사전 설정 드롭다운 메뉴에서 기존 뷰어를 선택합니다.

찾고 있는 뷰어 사전 설정이 표시되지 않는 경우 게시되었는지 확인하십시오. 뷰어 사전 설정을 사용하려면 먼저 게시해야 합니다. [뷰어 사전 설정 관리](/help/assets/managing-viewer-presets.md)를 참조하십시오. 

### 비디오 360 미디어 구성 요소 {#video-media-component}

**[!UICONTROL Video 360 Media]** 구성 요소를 사용하여 회의실, 속성, 위치, 가로 또는 의료 절차의 매력적인 보기 경험을 위해 웹 페이지에 동일한 사각형 비디오를 렌더링합니다.

평면 디스플레이에서 재생하는 동안 사용자가 보기 각도를 제어할 수 있습니다.모바일 디바이스에서 재생하는 경우 일반적으로 내장된 자이로스코프 컨트롤을 활용할 수 있습니다.

뷰어에는 360개의 비디오 에셋 전달에 대한 기본 지원이 포함되어 있습니다. 기본적으로 보거나 재생하는 데 추가 구성이 필요하지 않습니다. .mp4, .mkv 및 .mov와 같은 표준 비디오 확장을 사용하여 360개의 비디오를 제공할 수 있습니다. 가장 일반적인 코덱은 H.264입니다.

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

구성 요소에서 **[!UICONTROL 구성]**&#x200B;을 탭하여 다음 설정을 편집할 수 있습니다.

* **[!UICONTROL 뷰어 사전]** 설정 - 뷰어 사전 설정 드롭다운 메뉴에서 기존 뷰어를 선택합니다. 가상 현실 안경을 사용하는 최종 사용자를 위해 Video360VR을 사용합니다. 기본 비디오 재생 컨트롤과 소셜 미디어 기능이 포함되어 있습니다. 기본 비디오 재생 컨트롤이 포함된 Video360_social을 사용합니다. 비디오 렌더링은 스테레오 모드에서 수행됩니다. 수동 관점제어 기능은 꺼져 있지만 자이로스코프 제어 기능은 켜져 있습니다. 소셜 미디어 기능이 없습니다.

찾고 있는 뷰어 사전 설정이 표시되지 않는 경우 게시되었는지 확인하십시오. 뷰어 사전 설정을 사용하려면 먼저 게시해야 합니다. [뷰어 사전 설정 관리](/help/assets/managing-viewer-presets.md)를 참조하십시오. 

### HTTP/2를 사용하여 Dynamic Media 에셋 {#using-http-to-delivery-dynamic-media-assets} 전달

HTTP/2는 브라우저와 서버의 통신 방식을 향상시키는 업데이트된 새로운 웹 프로토콜입니다. 정보를 빠르게 전송할 수 있고 필요한 처리 능력을 줄일 수 있습니다. 이제 Dynamic Media 에셋 배달을 HTTP/2를 통해 더 나은 응답 및 로드 시간을 제공할 수 있습니다.

Dynamic Media 계정으로 HTTP/2를 사용하는 시작에 대한 자세한 내용은 [HTTP2 콘텐츠 제공](/help/assets/http2.md)을 참조하십시오.

>[!MORELIKETHIS]
>
>* [AEM Dynamic Media에서 비디오 플레이어 사용](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-video-player-feature-video-use.html)
>* [AEM Dynamic Media에서 대화형 비디오 사용](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-interactive-video-feature-video-use.html)
>* [AEM Dynamic Media을 사용한 자산 뷰어 이해](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-viewer-feature-video-understand.html)
>* [AEM Dynamic Media에서 사용자 정의 비디오 축소판 사용](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-video-thumbnails-feature-video-use.html)
>* [AEM Dynamic Media의 색상 관리 이해](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-color-management-technical-video-setup.html)
>* [AEM Dynamic Media에서 이미지 선명하게 하기 사용](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-image-sharpening-feature-video-use.html)

