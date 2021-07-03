---
title: 페이지에 Dynamic Media Classic 기능 추가
description: Adobe Experience Manager 페이지에 Dynamic Media Classic 기능 및 구성 요소를 추가하는 방법을 알아봅니다.
uuid: aa5a4735-bfec-43b8-aec0-a0c32bff134f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: managing-assets
discoiquuid: e7b95732-a571-48e8-afad-612059cdbde7
feature: Dynamic Media Classic
role: User, Admin
exl-id: 815f577d-4774-4830-8baf-0294bd085b83
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '2849'
ht-degree: 19%

---

# 페이지에 Dynamic Media Classic 기능 추가 {#adding-scene-features-to-your-page}

[Adobe Dynamic Media ](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html) Classic은 풍부한 미디어 자산을 관리, 개선, 게시 및 웹, 모바일, 이메일 및 인터넷에 연결된 디스플레이 및 인쇄에 제공하기 위한 호스팅 솔루션입니다.

다양한 뷰어에서 Dynamic Media Classic에 게시된 Experience Manager 자산을 볼 수 있습니다.

* 확대/축소
* 플라이아웃
* 비디오
* 이미지 템플릿
* 이미지

Experience Manager에서 Dynamic Media Classic으로 직접 디지털 자산을 게시할 수 있으며, Dynamic Media Classic에서 Experience Manager으로 디지털 자산을 게시할 수 있습니다.

이 문서에서는 Experience Manager에서 Dynamic Media Classic으로 디지털 자산을 게시하고 반대로 게시하는 방법에 대해 설명합니다. 뷰어도 자세히 설명되어 있습니다. Dynamic Media Classic에 대한 Experience Manager 구성에 대한 내용은 [Dynamic Media Classic과 Experience Manager](/help/sites-administering/scene7.md) 통합을 참조하십시오.

[이미지 맵 추가](image-maps.md)도 참조하십시오.

Experience Manager에서 비디오 구성 요소를 사용하는 방법에 대한 자세한 내용은 [비디오](video.md)를 참조하십시오.

>[!NOTE]
>
>Dynamic Media Classic 자산이 제대로 표시되지 않으면 Dynamic Media이 [비활성화](config-dynamic.md#disabling-dynamic-media)인지 확인한 다음 페이지를 새로 고치십시오.

## 자산에서 Dynamic Media Classic에 수동으로 게시 {#manually-publishing-to-scene-from-assets}

다음과 같이 Dynamic Media Classic에 디지털 자산을 게시할 수 있습니다.

* [자산 콘솔의 클래식 사용자 인터페이스에서](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [자산의 클래식 사용자 인터페이스에서](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [CQ Target 폴더 외부의 클래식 사용자 인터페이스에서](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>Experience Manager은 Dynamic Media Classic에 비동기적으로 게시합니다. **[!UICONTROL 게시]**&#x200B;를 클릭하면 자산이 Dynamic Media Classic에 게시되는 데 몇 초 걸립니다.


## Dynamic Media Classic 구성 요소 {#scene-components}

다음 Dynamic Media Classic 구성 요소는 Experience Manager에서 사용할 수 있습니다.

* 확대/축소
* 플라이아웃(확대/축소)
* 이미지 템플릿
* 이미지
* 비디오

>[!NOTE]
>
>이러한 구성 요소는 기본적으로 사용할 수 없으며 사용하기 전에 **[!UICONTROL 디자인]** 모드에서 선택해야 합니다.

**[!UICONTROL 디자인]** 모드에서 사용할 수 있게 되면 다른 Experience Manager 구성 요소처럼 페이지에 구성 요소를 추가할 수 있습니다. Dynamic Media Classic에 아직 게시되지 않은 자산은 동기화된 폴더 또는 페이지에 있거나 Dynamic Media Classic 클라우드 구성이 있는 경우 Dynamic Media Classic에 게시됩니다.

>[!NOTE]
>
>사용자 지정 뷰어를 만들고 개발하려고 하며 컨텐츠 파인더를 사용하는 경우 `allowfullscreen` 매개 변수를 명시적으로 추가해야 합니다.

### Flash 뷰어 지원 중단 알림 {#flash-viewers-end-of-life-notice}

2017년 1월 31일부터 Adobe Dynamic Media Classic은 Flash 뷰어 플랫폼에 대한 지원을 종료했습니다.

<!-- For more information about this important change, see [Flash Viewer End-of-Life FAQs](https://docs.adobe.com/content/docs/en/aem/6-1/administer/integration/marketing-cloud/scene7/flash-eol.html). -->

### 페이지에 Dynamic Media Classic(Scene7) 구성 요소 추가 {#adding-a-scene-component-to-a-page}

페이지에 Dynamic Media Classic(Scene7) 구성 요소를 추가하는 것은 페이지에 구성 요소를 추가하는 것과 같습니다. Dynamic Media Classic 구성 요소는 다음 섹션에서 자세히 설명합니다.

**페이지에 Dynamic Media Classic(Scene7) 구성 요소를 추가하려면:**

1. Experience Manager에서 **[!UICONTROL Dynamic Media Classic(Scene7)]** 구성 요소를 추가할 페이지를 엽니다.

1. 사용 가능한 Dynamic Media Classic 구성 요소가 없는 경우 **[!UICONTROL 디자인]** 모드를 클릭하고, 파란색 테두리가 있는 구성 요소를 탭하고 **[!UICONTROL 상위]** 아이콘을 탭한 다음, **[!UICONTROL 구성]** 아이콘을 탭합니다. **[!UICONTROL Parsys(디자인)]**&#x200B;에서 모든 Dynamic Media Classic 구성 요소를 선택하여 사용 가능하게 만들고 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. **[!UICONTROL 편집]**&#x200B;을 클릭하여 **[!UICONTROL 편집]** 모드로 돌아갈 수 있습니다.

1. 사이드 킥의 Dynamic Media Classic 그룹에서 원하는 위치의 페이지로 구성 요소를 끌어옵니다.

1. 구성 요소를 열 수 있도록 **[!UICONTROL 구성]** 아이콘을 클릭합니다.

1. 필요에 따라 구성 요소를 편집하고 **[!UICONTROL 확인]**&#x200B;을 클릭하여 변경 내용을 저장합니다.
1. 컨텐츠 브라우저에서 페이지에 추가한 Dynamic Media Classic 구성 요소로 이미지나 비디오를 드래그합니다.

   >[!NOTE]
   >
   >Touch UI에서만 이미지나 비디오를 페이지에 배치한 Dynamic Media Classic 구성 요소에 끌어다 놓아야 합니다. Dynamic Media Classic 구성 요소를 선택하고 편집한 다음, 자산을 선택할 수 없습니다.

### 응답형 사이트에 대화형 보기 경험 추가 {#adding-interactive-viewing-experiences-to-a-responsive-website}

자산에 대한 응답형 디자인은 자산이 표시되는 위치에 따라 조정됨을 의미합니다. 응답형 디자인을 통해 여러 장치에 동일한 자산을 효과적으로 표시할 수 있습니다.

또한 [웹 페이지를 위한 응답형 디자인](/help/sites-developing/responsive.md)을 참조하십시오.

**응답형 사이트에 대화형 보기 환경을 추가하려면:**

1. Experience Manager에 로그인하고 [구성된 Adobe Dynamic Media Classic Cloud Services](/help/sites-administering/scene7.md#configuring-scene-integration)이 있고 Dynamic Media Classic 구성 요소가 사용 가능한지 확인하십시오.

   >[!NOTE]
   >
   >Dynamic Media Classic 구성 요소를 사용할 수 없는 경우 디자인 모드](/help/sites-authoring/default-components-designmode.md)로 활성화하려면 [을 확인하십시오.

1. **[!UICONTROL Dynamic Media Classic]** 구성 요소가 활성화된 웹 사이트에서 **[!UICONTROL Image]** 구성 요소를 페이지로 드래그합니다.
1. 구성 요소를 선택하고 구성 아이콘을 누릅니다.
1. **[!UICONTROL Dynamic Media Classic 설정]** 탭에서 중단점을 조정합니다.

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. 뷰어가 그에 따라 크기가 조정되는지와 모든 상호 작용이 데스크톱, 태블릿 및 모바일에 최적화되어 있는지 확인합니다.

### 모든 Dynamic Media Classic 구성 요소에 공통되는 설정 {#settings-common-to-all-scene-components}

구성 옵션은 다르지만 모든 [!UICONTROL Dynamic Media Classic] 구성 요소에는 다음과 같은 공통점이 있습니다.

* **[!UICONTROL 파일 참조]** - 참조할 파일을 찾아 봅니다. 파일 참조는 자산 URL을 표시하며, 반드시 URL 명령 및 매개 변수를 포함하는 전체 Dynamic Media Classic URL일 필요는 없습니다. Dynamic Media Classic URL 명령 및 매개 변수는 이 필드에 추가할 수 없습니다. 대신 구성 요소의 해당 기능을 통해 추가합니다.
* **[!UICONTROL 너비]** - 너비를 설정할 수 있습니다.
* **[!UICONTROL 높이]** - 높이를 설정할 수 있습니다.

예를 들어, **[!UICONTROL Zoom]** 구성 요소를 열 때 Dynamic Media Classic 구성 요소를 열어(두 번 클릭) 이러한 구성 옵션을 설정합니다.

![chlimage_1-226](assets/chlimage_1-226.png)

### 확대/축소 {#zoom}

**[!UICONTROL +]** 단추를 누르면 HTML5 확대/축소 구성 요소가 더 큰 이미지를 표시합니다.

자산의 맨 아래에는 확대/축소 도구가 있습니다. 확대하려면 **[!UICONTROL +]**&#x200B;을 누릅니다.줄이려면 **[!UICONTROL -]**&#x200B;를 누릅니다. **[!UICONTROL x]** 또는 확대/축소 재설정 화살표를 탭하면 이미지가 가져온 원래 크기로 돌아갑니다. 전체 화면으로 만들려면 대각선 화살표를 누릅니다. 구성 요소를 구성할 수 있도록 **[!UICONTROL 편집]**&#x200B;을 누릅니다. 이 구성 요소를 사용하여 모든 [!UICONTROL Dynamic Media Classic] 구성 요소](#settings-common-to-all-scene-components)에 공통되는 [설정을 구성할 수 있습니다.

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### 플라이아웃 {#flyout}

HTML5 **[!UICONTROL 플라이아웃]** 구성 요소에서 자산은 분할 화면으로 표시됩니다.자산을 지정된 크기로 둡니다.오른쪽에는 확대/축소 부분이 표시됩니다. 구성 요소를 구성할 수 있도록 **[!UICONTROL 편집]**&#x200B;을 누릅니다. 이 구성 요소를 사용하여 모든 Dynamic Media Classic 구성 요소에 공통되는 [설정을 구성할 수 있습니다](#settings-common-to-all-scene-components).

>[!NOTE]
>
>**[!UICONTROL 플라이아웃]** 구성 요소가 사용자 지정 크기를 사용하는 경우 해당 사용자 지정 크기가 사용되고 구성 요소의 응답형 설정이 비활성화됩니다.
>
>**[!UICONTROL Flyout]** 구성 요소가 기본 크기를 사용하는 경우, **[!UICONTROL 디자인 보기]**&#x200B;에 설정된 대로 기본 크기가 사용되며, 구성 요소는 구성 요소의 응답형 설정이 활성화되면서 페이지 레이아웃 크기를 수용하도록 확장됩니다. 구성 요소의 응답형 설정에 대한 제한이 있습니다. 응답형 설정이 있는 **[!UICONTROL 플라이아웃]** 구성 요소를 사용하는 경우 전체 페이지 늘리기를 함께 사용하지 마십시오. 그렇지 않으면 **[!UICONTROL 플라이아웃]**&#x200B;이 페이지의 오른쪽 테두리를 넘어갈 수 있습니다.

![chlimage_1-228](assets/chlimage_1-228.png)

### 이미지 {#image}

Dynamic Media Classic **[!UICONTROL 이미지]** 구성 요소를 사용하면 Dynamic Media Classic 수정자, 이미지 또는 뷰어 사전 설정 및 선명하게 하기 등의 Dynamic Media Classic 기능을 이미지에 추가할 수 있습니다. Dynamic Media Classic **[!UICONTROL 이미지]** 구성 요소는 특수 Dynamic Media Classic 기능이 있는 Experience Manager에 있는 다른 이미지 구성 요소와 유사합니다. 이 예의 이미지에는 Dynamic Media Classic URL 수정자, `&op_invert=1`이 적용되어 있습니다.

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL 제목, 대체 텍스트]**  - 고급  **** 탭에서 이미지에 제목을 추가하고, 그래픽을 해제한 사용자를 위한 대체 텍스트를 추가합니다.

**[!UICONTROL URL, 여는 위치]**  - 링크를 열 자산을 설정할 수 있습니다. **[!UICONTROL URL]**&#x200B;을 설정하고 **[!UICONTROL 여는 위치]**&#x200B;에 같은 창에서 열지 또는 새 창에서 열지를 지정합니다.

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL 뷰어 사전 설정]**  - 드롭다운 메뉴에서 기존 뷰어 사전 설정을 선택합니다. 보려는 뷰어 사전 설정이 표시되지 않을 경우 표시되도록 설정해야 합니다. [뷰어 사전 설정 관리](/help/assets/managing-viewer-presets.md)를 참조하십시오. 이미지 사전 설정을 사용하고 있고 반대로 뷰어 사전 설정을 선택할 수는 없습니다.

**[!UICONTROL Dynamic Media Classic 구성]**  - SPS에서 활성 이미지 사전 설정을 가져오는 데 사용할 Dynamic Media Classic 구성을 선택합니다.

**[!UICONTROL 이미지 사전 설정]**  - 드롭다운 메뉴에서 기존 이미지 사전 설정을 선택합니다. 보려는 이미지 사전 설정이 표시되지 않을 경우 표시되도록 설정해야 합니다. [이미지 사전 설정 관리](/help/assets/managing-image-presets.md)를 참조하십시오. 이미지 사전 설정을 사용하고 있고 반대로 뷰어 사전 설정을 선택할 수는 없습니다.

**[!UICONTROL 출력 형식]**  - 이미지의 출력 형식(예: jpeg)을 선택하십시오. 선택한 출력 형식에 따라 추가 구성 옵션이 있습니다. [이미지 사전 설정 우수 사례](/help/assets/managing-image-presets.md#image-preset-options)를 참조하십시오.

**[!UICONTROL 선명도]**  - 이미지를 선명하게 하려는 방법을 선택하십시오. 선명하게 하기는 [이미지 사전 설정 우수 사례](/help/assets/managing-image-presets.md#image-preset-options) 및 [선명하게 하기 우수 사례](/help/assets/assets/sharpening_images.pdf)에 자세히 설명되어 있습니다.

**[!UICONTROL URL 수정자]**  - 추가 Dynamic Media Classic 이미지 명령을 제공하여 이미지 효과를 변경할 수 있습니다. 이러한 명령은 [이미지 사전 설정](/help/assets/managing-image-presets.md) 및 [명령 참조](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html)에 설명되어 있습니다.

**[!UICONTROL 중단점]**  - 웹 사이트가 응답형인 경우 중단점을 조정할 수 있습니다. 중단점은 쉼표(,)로 구분해야 합니다.

### 이미지 템플릿 {#image-template}

[Dynamic Media Classic 이미지 템플릿](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/template-basics/quick-start-template-basics.html) 은 Dynamic Media Classic으로 가져온 계층화된 Photoshop 컨텐츠입니다. 여기서 컨텐츠 및 속성은 가변성을 위해 매개 변수화됩니다. **[!UICONTROL 이미지 템플릿]** 구성 요소를 사용하면 이미지를 가져오고 Experience Manager에서 텍스트를 동적으로 변경할 수 있습니다. 또한 클라이언트 컨텍스트의 값을 사용하도록 **[!UICONTROL 이미지 템플릿]** 구성 요소를 구성할 수 있으므로 각 사용자는 개인화된 방식으로 이미지를 경험하게 됩니다.

구성 요소를 구성하려면 **[!UICONTROL 편집]**&#x200B;을 누릅니다. 모든 Dynamic Media Classic 구성 요소에 공통되는 [설정](#settings-common-to-all-scene-components) 및 이 섹션에 설명된 기타 설정을 구성할 수 있습니다.

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL 파일 참조, 너비, 높이]**  - 모든 ScDynamic Media Classic7 구성 요소에 공통인 설정을 참조하십시오.

>[!NOTE]
>
>Dynamic Media Classic URL 명령 및 매개 변수를 파일 참조 URL에 직접 추가할 수 없습니다. **[!UICONTROL 매개 변수]** 패널의 구성 요소 UI에서만 정의할 수 있습니다.

**[!UICONTROL 제목, 대체 텍스트]**  - Dynamic Media Classic 이미지 템플릿 탭에서 이미지에 제목을 추가하고, 그래픽을 해제한 사용자를 위한 대체 텍스트를 추가합니다.

**[!UICONTROL URL, 여는 위치]**  - 링크를 열 자산을 설정할 수 있습니다. URL을 설정하고 여는 위치에 같은 창에서 열지 또는 새 창에서 열지를 지정합니다.

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL 매개 변수 패널]**  - 이미지를 가져올 때 매개 변수는 이미지의 정보로 미리 채워집니다. 동적으로 변경할 수 있는 컨텐츠가 없는 경우 이 창은 비어 있습니다.

![chlimage_1-233](assets/chlimage_1-233.png)

#### 동적으로 텍스트 변경 {#changing-text-dynamically}

텍스트를 동적으로 변경하려면 필드에 새 텍스트를 입력하고 **[!UICONTROL 확인]**&#x200B;을 클릭하십시오. 이 예에서 **[!UICONTROL 가격]**&#x200B;은 현재 $50이며 배송비는 99센트입니다.

![chlimage_1-234](assets/chlimage_1-234.png)

이미지의 텍스트가 변경됩니다. 필드 옆에 있는 **[!UICONTROL 재설정]**&#x200B;을 탭하여 텍스트를 원래 값으로 재설정할 수 있습니다.

![chlimage_1-235](assets/chlimage_1-235.png)

#### 클라이언트 컨텍스트 값을 반영하도록 텍스트 변경 {#changing-text-to-reflect-the-value-of-a-client-context-value}

필드를 클라이언트 컨텍스트 값에 연결하려면 **[!UICONTROL 선택]**&#x200B;을 눌러 클라이언트 컨텍스트 메뉴를 열고 클라이언트 컨텍스트를 선택한 다음 **[!UICONTROL 확인]**&#x200B;을 누릅니다. 이 예제에서 이름은 프로필의 형식이 지정된 이름과 연결되어 변경됩니다.

![chlimage_1-236](assets/chlimage_1-236.png)

텍스트는 현재 로그인한 사용자의 이름을 반영합니다. 필드 옆에 있는 **[!UICONTROL 재설정]**&#x200B;을 클릭하여 텍스트를 원래 값으로 재설정할 수 있습니다.

![chlimage_1-237](assets/chlimage_1-237.png)

#### Dynamic Media Classic 이미지 템플릿을 링크로 지정 {#making-the-scene-image-template-a-link}

1. Dynamic Media Classic **[!UICONTROL 이미지 템플릿]** 구성 요소가 있는 페이지에서 **[!UICONTROL 편집]**&#x200B;을 탭합니다.
1. **[!UICONTROL URL]** 필드에 이미지를 탭할 때 사용자가 이동하는 URL을 입력합니다. **[!UICONTROL 여는 위치]** 필드에서 대상을 새 창 또는 동일한 창 중 어떤 창에서 열지를 선택합니다.

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. **[!UICONTROL 확인]**&#x200B;을 누릅니다.

### 비디오 구성 요소 {#video-component}

Dynamic Media Classic **[!UICONTROL 비디오]** 구성 요소(사이드 킥의 Dynamic Media Classic 섹션에서 사용 가능)는 장치 및 대역폭 검색을 사용하여 각 화면에 올바른 비디오를 제공합니다. 이 구성 요소는 HTML5 비디오 플레이어로, 채널 간에 사용할 수 있는 단일 뷰어입니다.

응용 비디오 세트, 단일 MP4 비디오 또는 단일 F4V 비디오에 사용할 수 있습니다.

비디오가 Dynamic Media Classic 통합에 따라 작동하는 방식에 대한 자세한 내용은 [비디오](s7-video.md)를 참조하십시오. 또한 [Dynamic Media Classic 비디오 구성 요소와 기본 비디오 구성 요소](s7-video.md)를 참조하십시오.

![chlimage_1-239](assets/chlimage_1-239.png)

### 비디오 구성 요소의 알려진 제한 사항 {#known-limitations-for-the-video-component}

Adobe DAM 및 WCM은 기본 소스 비디오가 업로드되었는지를 표시합니다. 다음과 같은 프록시 자산은 표시되지 않습니다.

* Dynamic Media Classic 인코딩 표현물
* Dynamic Media Classic 응용 비디오 세트

Dynamic Media Classic 비디오 구성 요소에서 응용 비디오 세트를 사용할 때는 비디오 크기에 맞게 구성 요소의 크기를 조정해야 합니다.

## Dynamic Media Classic 컨텐츠 브라우저 {#scene-content-browser}

Dynamic Media Classic 컨텐츠 브라우저를 사용하면 Dynamic Media Classic의 컨텐츠를 Experience Manager에서 직접 볼 수 있습니다. 컨텐츠 브라우저에 액세스하려면 **[!UICONTROL 컨텐츠 파인더]**&#x200B;에서 터치에 적합한 사용자 인터페이스에서 **[!UICONTROL Dynamic Media Classic]** 을 선택하거나, 클래식 사용자 인터페이스에서 **[!UICONTROL S7]** 아이콘을 선택하십시오. 기능은 두 사용자 인터페이스에서 동일합니다.

구성이 여러 개인 경우 기본적으로 Experience Manager에 [기본 구성](/help/sites-administering/scene7.md#configuring-a-default-configuration)이 표시됩니다. 드롭다운 메뉴의 Dynamic Media Classic 콘텐츠 브라우저에서 직접 다른 구성을 선택할 수 있습니다.

>[!NOTE]
>
>* 온디맨드 폴더의 자산은 Dynamic Media Classic 콘텐츠 브라우저에 표시되지 않습니다.
>* [보안 미리 보기가 활성화되면 Dynamic Media Classic에 게시된 자산과 게시되지 않은 자산이 모두 Dynamic Media Classic 컨텐츠 브라우저에 표시됩니다.](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)
>* 컨텐츠 브라우저에 **[!UICONTROL Dynamic Media Classic]** 또는 **[!UICONTROL S7]** 아이콘이 옵션으로 표시되지 않는 경우 [Dynamic Media Classic이 Experience Manager](/help/sites-administering/scene7.md)에서 작동하도록 구성해야 합니다.
>* 비디오의 경우 Dynamic Media Classic 컨텐츠 브라우저는 다음을 지원합니다.

   >
   >   
   * 응용 비디오 세트: 여러 화면 간에 원활하게 재생되는 데 필요한 모든 비디오 표현물의 컨테이너
   >   * 단일 MP4 비디오
   >   * 단일 F4V 동영상


### 터치에 적합한 UI에서 컨텐츠 찾아보기 {#browsing-content-in-the-touch-optimized-ui}

터치에 적합한 UI 또는 클래식 UI에서 컨텐츠 브라우저에 액세스할 수 있습니다. 현재 터치에 적합한 기능에는 다음과 같은 제한이 있습니다.

* Dynamic Media Classic의 FXG 및 Flash 자산은 지원되지 않습니다.

세 번째 드롭다운 메뉴에서 **[!UICONTROL Dynamic Media Classic]**&#x200B;을 선택하여 Dynamic Media Classic 자산을 찾아봅니다. Dynamic Media Classic/Experience Manager 통합을 구성하지 않은 경우 Dynamic Media Classic이 목록에 표시되지 않습니다.

>[!NOTE]
>
>* Dynamic Media Classic 컨텐츠 브라우저는 약 100개의 자산을 로드하고 이름별로 정렬합니다.
>* 보안 미리 보기 서버가 설정된 경우 브라우저에서는 해당 미리 보기 서버를 사용하여 미리 보기 및 자산을 렌더링합니다.

>



![chlimage_1-240](assets/chlimage_1-240.png)

또한 브라우저에서 자산을 마우스로 가리키면 확인 정보, 크기, 수정 이후 일 수 및 파일 이름을 찾을 수 있습니다.

![chlimage_1-241](assets/chlimage_1-241.png)

* 응용 비디오 세트 및 템플릿의 경우 미리 보기에 대한 크기 정보가 생성되지 않습니다.
* 응용 비디오 세트의 경우 미리 보기에 대한 해상도가 생성되지 않습니다.

### 컨텐츠 브라우저로 Dynamic Media Classic 자산 검색 {#searching-for-scene-assets-with-the-content-browser}

Dynamic Media Classic에서 자산을 검색하는 것은 Experience Manager 자산에서 자산을 검색하는 것과 비슷합니다. 그러나 검색할 때 자산을 Experience Manager으로 직접 가져오지 않고 Dynamic Media Classic 시스템에서 자산의 원격 보기가 표시됩니다.

클래식 UI 또는 터치에 적합한 UI를 사용하여 자산을 보고 검색할 수 있습니다. 인터페이스에 따라, 검색 방식이 약간 다릅니다.

UI에서 검색할 때 다음 기준(터치에 적합한 UI에서 여기에 표시됨)에 따라 필터링할 수 있습니다.

**[!UICONTROL 키워드 입력]**  - 이름별로 자산을 검색할 수 있습니다. 검색할 때 파일 이름의 시작 문자를 입력합니다. 예를 들어, &quot;swimming&quot;이라는 단어를 입력하면 해당 문자가 해당 순서로 시작되는 모든 자산 파일 이름이 검색됩니다. 자산을 찾으려면 용어를 입력한 후 Enter 키를 누릅니다.

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL 폴더/경로]**  - 표시되는 폴더의 이름은 선택한 구성에 따라 다릅니다. 폴더 아이콘을 탭하고 하위 폴더를 선택하여 하위 레벨로 드릴다운한 다음 확인 표시를 탭하여 선택할 수 있습니다.

키워드를 입력하고 폴더를 선택하면 Experience Manager은 해당 폴더와 하위 폴더를 검색합니다. 그러나 검색 시 키워드를 입력하지 않는 경우 폴더를 선택하면 해당 폴더의 자산만 표시되고 하위 폴더는 포함되지 않습니다.

기본적으로 Experience Manager은 선택한 폴더와 모든 하위 폴더를 검색합니다.

![chlimage_1-243](assets/chlimage_1-243.png)

**[!UICONTROL 자산 유형]**  - Dynamic Media  **[!UICONTROL Classic]** 컨텐츠를 찾아보려면 Dynamic Media Classic을 선택합니다. 이 옵션은 Dynamic Media Classic이 구성된 경우에만 사용할 수 있습니다.

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL 구성]**  -  [!UICONTROL Cloud Services]에 둘 이상의 Dynamic Media Classic 구성이 정의되어 있는 경우 여기에서 선택할 수 있습니다. 결과적으로 폴더는 선택한 구성에 따라 변경됩니다.

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL 자산 유형]**  - Dynamic Media Classic 브라우저 내에서 다음 중 하나를 포함하도록 결과를 필터링할 수 있습니다.이미지, 템플릿, 비디오 및 응용 비디오 세트입니다. 자산 유형을 선택하지 않으면 기본적으로 Experience Manager은 모든 자산 유형을 검색합니다.

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* 클래식 UI에서 **Flash** 및 **FXG**&#x200B;를 검색할 수도 있습니다. 터치에 적합한 UI에서 이러한 유형에 대한 필터링은 지원되지 않습니다.
   >
   >
* 비디오를 검색할 때 단일 표현물을 검색합니다. 결과는 원래 표현물(&amp;ast;.mp4만) 및 인코딩된 표현물을 반환합니다.
>* 응용 비디오 세트를 검색할 때 폴더 및 모든 하위 폴더를 검색하지만 검색에 키워드를 추가한 경우에만 해당됩니다. 키워드를 추가하지 않은 경우 Experience Manager이 하위 폴더를 검색하지 않습니다.

>



**[!UICONTROL 게시 상태]**  - 게시 상태에 따라 자산을 필터링할 수 있습니다. **** 게시 취소 또는  **[!UICONTROL 게시됨]**. **[!UICONTROL 게시 상태]**&#x200B;를 선택하지 않으면 기본적으로 Experience Manager은 모든 게시 상태를 검색합니다.

![chlimage_1-247](assets/chlimage_1-247.png)
