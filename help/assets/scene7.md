---
title: 페이지에 Dynamic Media 클래식 기능 추가
description: AEM 페이지에 Dynamic Media Classic 기능 및 구성 요소를 추가하는 방법을 알아봅니다.
uuid: aa5a4735-bfec-43b8-aec0-a0c32bff134f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: managing-assets
discoiquuid: e7b95732-a571-48e8-afad-612059cdbde7
translation-type: tm+mt
source-git-commit: 7e9dcebc654e63e171e2baacfe53081f58676f8d
workflow-type: tm+mt
source-wordcount: '2862'
ht-degree: 26%

---


# 페이지에 Dynamic Media 클래식 기능 추가 {#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic](https://help.adobe.com/en_US/scene7/using/WS26AB0D9A-F51C-464e-88C8-580A5A82F810.html) 은 리치 미디어 에셋을 관리, 향상, 게시 및 웹, 모바일, 이메일 및 인터넷에 연결된 디스플레이와 인쇄물로 전달하는 호스팅 솔루션입니다.

다양한 뷰어에서 Dynamic Media Classic에 게시된 AEM 자산을 볼 수 있습니다.

* 확대/축소
* 플라이아웃
* 비디오
* 이미지 템플릿
* 이미지

AEM에서 Dynamic Media Classic으로 디지털 자산을 직접 게시할 수 있으며, Dynamic Media Classic에서 AEM으로 디지털 자산을 게시할 수 있습니다.

이 문서에서는 AEM의 디지털 자산을 Dynamic Media Classic으로 또는 그 반대로 게시하는 방법에 대해 설명합니다. 뷰어도 자세히 설명되어 있습니다. Dynamic Media Classic용 AEM 구성에 대한 자세한 내용은 AEM과 [Dynamic Media Classic 통합을 참조하십시오](/help/sites-administering/scene7.md).

[이미지 맵 추가](image-maps.md)도 참조하십시오.

For more information on using video components with AEM, see [Video](video.md).

>[!NOTE]
>
>If Dynamic Media Classic assets do not display properly, make sure that Dynamic media is [disabled](config-dynamic.md#disabling-dynamic-media) and then refresh the page.

## 자산에서 Dynamic Media Classic에 수동으로 게시 {#manually-publishing-to-scene-from-assets}

다음과 같이 디지털 자산을 Dynamic Media Classic에 게시할 수 있습니다.

* [자산 콘솔의 클래식 사용자 인터페이스](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [자산의 클래식 사용자 인터페이스](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [CQ Target 폴더 외부의 클래식 사용자 인터페이스](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>AEM은 비동기적으로 Dynamic Media Classic에 게시합니다. After you click **[!UICONTROL Publish]**, it may take several seconds for your asset to publish to Dynamic Media Classic.


## Dynamic Media 클래식 구성 요소 {#scene-components}

다음 Dynamic Media Classic 구성 요소를 AEM에서 사용할 수 있습니다.

* 확대/축소
* 플라이아웃(확대/축소)
* 이미지 템플릿
* 이미지
* 비디오

>[!NOTE]
>
>These components are not available by default and need to be selected in **[!UICONTROL Design]** mode before using.

After they are made available in **[!UICONTROL Design]** mode, you can add the components to your page like any other AEM component. Dynamic Media Classic에 아직 게시되지 않은 자산은 동기화된 폴더 또는 페이지에 있거나 Dynamic Media Classic 클라우드 구성이 있는 경우 Dynamic Media Classic에 게시됩니다.

>[!NOTE]
>
>If you are creating and developing custom viewers and using the Content Finder, you need to explicity add the **[!UICONTROL allowfullscreen]** parameter.

### Flash 뷰어 지원 중단 알림 {#flash-viewers-end-of-life-notice}

2017년 1월 31일부터 Adobe Dynamic Media Classic은 Flash 뷰어 플랫폼에 대한 지원을 중단했습니다.

이 중요 변경 사항에 대한 자세한 내용은 [Flash 뷰어 지원 종료 FAQ](https://docs.adobe.com/content/docs/kr/aem/6-1/administer/integration/marketing-cloud/scene7/flash-eol.html)를 참조하십시오.

### Adding a Dynamic Media Classic component (Scene7) to a page {#adding-a-scene-component-to-a-page}

Dynamic Media 클래식(Scene7) 구성 요소를 페이지에 추가하는 것은 페이지에 구성 요소를 추가하는 것과 같습니다. Dynamic Media 클래식 구성 요소는 다음 섹션에 자세히 설명되어 있습니다.

**Dynamic Media Classic(Scene7) 구성 요소를 페이지에 추가하려면**

1. AEM에서 Dynamic Media Classic(Scene7) 구성 요소를 추가할 페이지를 엽니다.

1. 사용 가능한 Dynamic Media Classic 구성 요소가 없으면 **[!UICONTROL 디자인]** 모드를 클릭하고 파란색 테두리가 있는 구성 요소를 탭하고 **[!UICONTROL 상위]** 아이콘을 누른 다음 **[!UICONTROL 구성]** 아이콘을누릅니다. Parsys( **[!UICONTROL Design)]**&#x200B;에서 모든 Dynamic Media Classic 구성 요소를 선택하여 사용 가능하게 만들고 확인을 **[!UICONTROL 클릭합니다.]**

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. 편집 **[!UICONTROL 을]** 클릭하여 **[!UICONTROL 편집]** 모드로 돌아갑니다.

1. 사이드 킥의 Dynamic Media 클래식 그룹에서 원하는 위치의 페이지로 구성 요소를 드래그합니다.

1. Click the **[!UICONTROL Configuration]** icon to open the component.

1. 필요에 따라 구성 요소를 편집하고 **[!UICONTROL 확인]**&#x200B;을 클릭하여 변경 내용을 저장합니다.
1. 컨텐츠 브라우저의 이미지나 비디오를 페이지에 추가한 Dynamic Media Classic 구성 요소로 드래그합니다.

   >[!NOTE]
   >
   >터치 UI에서만 페이지에 배치한 Dynamic Media Classic 구성 요소에 이미지나 비디오를 끌어다 놓아야 합니다. Dynamic Media Classic 구성 요소를 선택 및 편집한 다음 자산 선택은 지원되지 않습니다.

### Adding interactive viewing experiences to a responsive site {#adding-interactive-viewing-experiences-to-a-responsive-website}

자산이 응답형으로 디자인되어 자산이 표시되는 위치에 따라 조정됩니다. 응답형 디자인을 통해 여러 장치에 동일한 자산을 효과적으로 표시할 수 있습니다.

웹 페이지용 [반응형 디자인을 참조하십시오](/help/sites-developing/responsive.md).

**반응형 사이트에 대화형 보기 환경을 추가하려면**

1. Log in to AEM, and ensure that you have [configured Adobe Dynamic Media Classic Cloud Services](/help/sites-administering/scene7.md#configuring-scene-integration) and that Dynamic Media Classic components are available.

   >[!NOTE]
   >
   >Dynamic Media Classic 구성 요소를 사용할 수 없는 경우 디자인 모드 [를 통해 활성화해야 합니다](/help/sites-authoring/default-components-designmode.md).

1. In a website with the **[!UICONTROL Dynamic Media Classic]** components enabled, drag an **[!UICONTROL Image]** component to the page.
1. 구성 요소를 선택하고 구성 아이콘을 누릅니다.
1. Dynamic Media **[!UICONTROL 클래식 설정]** 탭에서 중단점을 조정합니다.

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. 뷰어가 그에 따라 크기가 조정되는지와 모든 상호 작용이 데스크톱, 태블릿 및 모바일에 최적화되어 있는지 확인합니다.

### 모든 Dynamic Media Classic 구성 요소에 공통되는 설정 {#settings-common-to-all-scene-components}

Although configuration options vary, the following are common to all [!UICONTROL Dynamic Media Classic] components:

* **[!UICONTROL 파일 참조]** - 참조할 파일을 찾습니다. 파일 참조는 자산 URL을 보여주며 URL 명령 및 매개 변수를 포함하는 전체 Dynamic Media 클래식 URL일 필요는 없습니다. 이 필드에 Dynamic Media 클래식 URL 명령 및 매개 변수를 추가할 수 없습니다. 구성 요소의 해당 기능을 통해 추가해야 합니다.
* **[!UICONTROL 너비]** - 너비를 설정할 수 있습니다.
* **[!UICONTROL 높이]** - 높이를 설정할 수 있습니다.

You set these configuration options by opening (double-clicking) a Dynamic Media Classic component, for example, when you open a **[!UICONTROL Zoom]** component:

![chlimage_1-226](assets/chlimage_1-226.png)

### 확대/축소 {#zoom}

The HTML5 Zoom component displays a larger image when you press the **[!UICONTROL +]** button.

자산의 맨 아래에는 확대/축소 도구가 있습니다. 확대하려면 **[!UICONTROL +]** 를 누릅니다. 을 눌러 **[!UICONTROL 축소합니다]** . Tapping the **[!UICONTROL x]** or the reset zoom arrow brings the image back to the original size it was imported as. 대각선 화살표를 눌러 전체 화면으로 만듭니다. Tap **[!UICONTROL Edit]** to configure the component. With this component, you can configure [settings common to all [!UICONTROL Dynamic Media Classic] components](#settings-common-to-all-scene-components).

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### 플라이아웃 {#flyout}

In the HTML5 **[!UICONTROL Flyout]** component, the asset is shown as split screen; left the asset in the specified size; right the zoom portion is displayed. Tap **[!UICONTROL Edit]** to configure the component. With this component, you can configure [settings common to all Dynamic Media Classic components](#settings-common-to-all-scene-components).

>[!NOTE]
>
>If your **[!UICONTROL Flyout]** component uses a custom size, then that custom size is used and responsive setup of the component is disabled.
>
>If your **[!UICONTROL Flyout]** component uses the default size, as set in the **[!UICONTROL Design View]**, then the default size is used and the component stretches to accomodate the page layout size with responsive setup of the component enabled. 그러나 구성 요소의 응답형 설정에 대한 제한은 있습니다. When the you use the **[!UICONTROL Flyout]** component with responsive setup, you should not use it with full page stretch. Otherwise, the **[!UICONTROL Flyout]** may extend beyond the page&#39;s right border.

![chlimage_1-228](assets/chlimage_1-228.png)

### 이미지 {#image}

Dynamic Media Classic **[!UICONTROL 이미지]** 구성 요소를 사용하면 Dynamic Media Classic 수정자, 이미지 또는 뷰어 사전 설정 및 선명하게 하기 등과 같은 Dynamic Media Classic 기능을 이미지에 추가할 수 있습니다. Dynamic Media Classic **[!UICONTROL 이미지]** 구성 요소는 특수 Dynamic Media Classic 기능이 있는 AEM의 다른 이미지 구성 요소와 유사합니다. 이 예에서 이미지에는 Dynamic Media Classic URL 수정자가 `&op_invert=1` 적용되어 있습니다.

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL 제목, 대체 텍스트]** - **[!UICONTROL 고급]** 탭에서 이미지에 제목을 추가하고 그래픽을 해제한 사용자를 위한 대체 텍스트를 추가합니다.

**[!UICONTROL URL, 열기]** - 링크를 열 자산을 설정할 수 있습니다. **[!UICONTROL URL]**&#x200B;을 설정하고 **[!UICONTROL 여는 위치]**&#x200B;에 같은 창에서 열지 또는 새 창에서 열지를 지정합니다.

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL 뷰어 사전 설정]** - 드롭다운 메뉴에서 기존 뷰어 사전 설정을 선택합니다. 보려는 뷰어 사전 설정이 표시되지 않을 경우 표시되도록 설정해야 할 수 있습니다. [뷰어 사전 설정 관리](/help/assets/managing-viewer-presets.md)를 참조하십시오. 이미지 사전 설정을 사용 중일 때는 뷰어 사전 설정을 선택할 수 없고 그 반대의 경우도 마찬가지입니다.

**[!UICONTROL Dynamic Media 클래식 구성]** - SPS에서 활성 이미지 사전 설정을 가져오는 데 사용할 Dynamic Media 클래식 구성을 선택합니다.

**[!UICONTROL 이미지 사전 설정]** - 드롭다운 메뉴에서 기존 이미지 사전 설정을 선택합니다. 보려는 이미지 사전 설정이 표시되지 않을 경우 표시되도록 설정해야 할 수 있습니다. [이미지 사전 설정 관리](/help/assets/managing-image-presets.md)를 참조하십시오. 이미지 사전 설정을 사용 중일 때는 뷰어 사전 설정을 선택할 수 없고 그 반대의 경우도 마찬가지입니다.

**[!UICONTROL 출력 형식]** - 이미지의 출력 형식(예: jpeg)을 선택합니다. 선택한 출력 형식에 따라 추가 구성 옵션이 있을 수 있습니다. [이미지 사전 설정 우수 사례](/help/assets/managing-image-presets.md#image-preset-options)를 참조하십시오.

**[!UICONTROL 선명하게 하기]** - 이미지를 선명하게 할 방법을 선택합니다. 선명하게 하기는 [이미지 사전 설정 우수 사례](/help/assets/managing-image-presets.md#image-preset-options) 및 [선명하게 하기 우수 사례](/help/assets/assets/s7_sharpening_images.pdf)에 자세히 설명되어 있습니다.

**[!UICONTROL URL 수정자]** - 추가 Dynamic Media Classic 이미지 명령을 제공하여 이미지 효과를 변경할 수 있습니다. 이러한 내용은 [이미지 사전 설정](/help/assets/managing-image-presets.md) 및 [명령 참조](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html)에 설명되어 있습니다.

**[!UICONTROL 중단점]** - 웹 사이트가 응답형인 경우 중단점을 조정하려고 합니다. 중단점은 쉼표(,)로 구분해야 합니다.

### 이미지 템플릿 {#image-template}

[Dynamic Media Classic Image Templates](https://docs.adobe.com/help/en/dynamic-media-classic/using/template-basics/quick-start-template-basics.html) 는 Dynamic Media Classic으로 가져온 레이어로 구성된 Photoshop 컨텐츠로, 여기서 컨텐츠와 속성은 가변성을 위해 매개 변수화되었습니다. **[!UICONTROL 이미지 템플릿]** 구성 요소를 사용하여 이미지를 가져오고 AEM에서 텍스트를 동적으로 변경할 수 있습니다. 또한 클라이언트 컨텍스트의 값을 사용하도록 **[!UICONTROL 이미지 템플릿]** 구성 요소를 구성할 수 있으므로 각 사용자는 개인화된 방식으로 이미지를 경험하게 됩니다.

Tap **[!UICONTROL Edit]** to configure the component. You can configure [settings common to all Dynamic Media Classic components](#settings-common-to-all-scene-components) as well as other settings described in this section.

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL 파일 참조, 너비, 높이]** - 모든 ScDynamic Media Classic 7 구성 요소에 공통인 설정을 참조하십시오.

>[!NOTE]
>
>Dynamic Media 클래식 URL 명령 및 매개 변수를 파일 참조 URL에 직접 추가할 수 없습니다. **[!UICONTROL 매개 변수]** 패널의 구성 요소 UI에서만 정의할 수 있습니다.

**[!UICONTROL 제목, 대체 텍스트]** - Dynamic Media의 클래식 이미지 템플릿 탭에서 이미지에 제목을 추가하고 그래픽을 해제한 사용자를 위한 대체 텍스트를 추가합니다.

**[!UICONTROL URL, 열기]** - 링크를 열 자산을 설정할 수 있습니다. URL을 설정하고 여는 위치에 같은 창에서 열지 또는 새 창에서 열지를 지정합니다.

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL 매개 변수 패널]** - 이미지를 가져올 때 매개 변수가 이미지의 정보로 미리 채워집니다. 동적으로 변경할 수 있는 컨텐츠가 없는 경우 이 창은 비어 있습니다.

![chlimage_1-233](assets/chlimage_1-233.png)

#### 동적으로 텍스트 변경 {#changing-text-dynamically}

텍스트를 동적으로 변경하려면 필드에 새 텍스트를 입력하고 **[!UICONTROL 확인을 클릭하십시오.]** 이 예에서 **[!UICONTROL 가격]**&#x200B;은 현재 $50이며 배송비는 99센트입니다.

![chlimage_1-234](assets/chlimage_1-234.png)

이미지의 텍스트가 변경됩니다. You can reset the text back to the original value by tapping **[!UICONTROL Reset]** next to the field.

![chlimage_1-235](assets/chlimage_1-235.png)

#### 클라이언트 컨텍스트 값을 반영하도록 텍스트 변경 {#changing-text-to-reflect-the-value-of-a-client-context-value}

To link a field to a client context value, tap **[!UICONTROL Select]** to open the client-context menu, select the client context, and tap **[!UICONTROL OK.]** 이 예제에서 이름은 프로필의 형식이 지정된 이름과 연결되어 변경됩니다.

![chlimage_1-236](assets/chlimage_1-236.png)

텍스트는 현재 로그인한 사용자의 이름을 반영합니다. 필드 옆에 있는 **[!UICONTROL 재설정]**&#x200B;을 클릭하여 텍스트를 원래 값으로 재설정할 수 있습니다.

![chlimage_1-237](assets/chlimage_1-237.png)

#### Dynamic Media 클래식 이미지 템플릿을 링크로 만들기 {#making-the-scene-image-template-a-link}

1. Dynamic Media의 클래식 **[!UICONTROL 이미지 템플릿]** 구성 요소가 있는 페이지에서 편집을 **[!UICONTROL 누릅니다.]**
1. In the **[!UICONTROL URL]** field, enter the URL that users go to when the image is tapped. In the **[!UICONTROL Open in]** field, select whether you want the target to open (a new window or same window).

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. 확인을 **[!UICONTROL 누릅니다.]**

### 비디오 구성 요소 {#video-component}

The Dynamic Media Classic **[!UICONTROL Video]** component (available from the Dynamic Media Classic section of the sidekick) uses device and bandwidth detection to serve the right video to each screen. 이 구성 요소는 HTML5 비디오 플레이어로, 채널 간에 사용할 수 있는 단일 뷰어입니다.

응용 비디오 세트, 단일 MP4 비디오 또는 단일 F4V 비디오에 사용할 수 있습니다.

See [Video](s7-video.md) for more information on how videos work with Dynamic Media Classic integration. 또한 Dynamic Media 클래식 비디오 구성 요소 [와 기본 비디오 구성 요소를 참조하십시오](s7-video.md).

![chlimage_1-239](assets/chlimage_1-239.png)

### 비디오 구성 요소의 알려진 제한 사항 {#known-limitations-for-the-video-component}

Adobe DAM 및 WCM은 기본 소스 비디오가 업로드되었는지를 표시합니다. 다음과 같은 프록시 자산은 표시되지 않습니다.

* Dynamic Media 클래식 인코딩 변환
* Dynamic Media 클래식 응용 비디오 세트

Dynamic Media Classic 비디오 구성 요소와 함께 응용 비디오 세트를 사용하는 경우 비디오 크기에 맞게 구성 요소의 크기를 조정해야 합니다.

## Dynamic Media 클래식 컨텐츠 브라우저 {#scene-content-browser}

Dynamic Media Classic 컨텐츠 브라우저를 사용하면 AEM에서 직접 Dynamic Media Classic의 컨텐츠를 볼 수 있습니다. To access the content browser, in the **[!UICONTROL Content Finder]**, select **[!UICONTROL Dynamic Media Classic]** in the touch-optimized user interface or the **[!UICONTROL S7]** icon in the classic user interface. 기능은 두 사용자 인터페이스에서 동일합니다.

다중 구성이 있는 경우, 기본적으로 AEM은 [기본 구성](/help/sites-administering/scene7.md#configuring-a-default-configuration)을 표시합니다. 드롭다운 메뉴의 Dynamic Media Classic 컨텐츠 브라우저에서 직접 다른 구성을 선택할 수 있습니다.

>[!NOTE]
>
>* 임시 폴더에 있는 자산은 Dynamic Media Classic 컨텐츠 브라우저에 나타나지 않습니다.
>* [ [보안 미리 보기]가 활성화되면](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)Dynamic Media Classic의 게시된 자산과 게시 취소된 자산이 모두 Dynamic Media Classic 콘텐츠 브라우저에 표시됩니다.
>* If you do not see **[!UICONTROL Dynamic Media Classic]** or the **[!UICONTROL S7]** icon as an option in the content browser, you need to [configure Dynamic Media Classic to work with AEM](/help/sites-administering/scene7.md).
>* 비디오의 경우 Classic 컨텐츠 브라우저가 지원하는 Dynamic Media:
   >   * 응용 비디오 세트: 여러 화면 간에 원활하게 재생되는 데 필요한 모든 비디오 표현물의 컨테이너
   >   * 단일 MP4 비디오
   >   * 단일 F4V 비디오


### Browsing content in the touch-optimized UI {#browsing-content-in-the-touch-optimized-ui}

터치에 적합한 UI 또는 클래식 UI에서 컨텐츠 브라우저에 액세스할 수 있습니다. 현재 터치에 적합한 기능에는 다음과 같은 제한이 있습니다.

* Dynamic Media Classic의 FXG 및 Flash 에셋은 지원되지 않습니다.

세 번째 드롭다운 메뉴에서 **[!UICONTROL Dynamic Media Classic]** 을 선택하여 Dynamic Media Classic 에셋을 찾아봅니다. Dynamic Media Classic/AEM 통합을 구성하지 않은 경우 Dynamic Media Classic이 목록에 표시되지 않습니다.

>[!NOTE]
>
>* Dynamic Media Classic 컨텐츠 브라우저는 약 100개의 에셋을 로드하고 이름별로 정렬합니다.
>* 보안 미리 보기 서버가 설정된 경우 브라우저에서 미리 보기 서버를 사용하여 축소판과 자산을 렌더링합니다.

>



![chlimage_1-240](assets/chlimage_1-240.png)

또한 브라우저에서 자산 위로 마우스를 가져가면 해상도 정보, 크기, 수정 후 일 수 및 파일 이름을 검색할 수 있습니다.

![chlimage_1-241](assets/chlimage_1-241.png)

* 응용 비디오 세트 및 템플릿의 경우 축소판의 크기 정보가 생성되지 않습니다.
* 응용 비디오 세트의 경우 축소판의 해상도가 생성되지 않습니다.

### 컨텐츠 브라우저를 사용하여 Dynamic Media Classic 자산 검색 {#searching-for-scene-assets-with-the-content-browser}

Dynamic Media Classic 자산 검색은 AEM으로 직접 가져오는 대신 Dynamic Media Classic 시스템에서 자산의 원격 보기를 실제로 보고 있다는 점을 제외하고 AEM 자산 검색과 유사합니다.

클래식 UI 또는 터치에 적합한 UI를 사용하여 자산을 보고 검색할 수 있습니다. 인터페이스에 따라, 검색 방식이 약간 다릅니다.

UI에서 검색할 때 다음 기준(터치에 적합한 UI에서 여기에 표시됨)에 따라 필터링할 수 있습니다.

**[!UICONTROL 키워드]** 입력 - 이름별로 자산을 검색할 수 있습니다. 키워드를 검색할 때 파일 이름의 시작 문자를 입력합니다. 예를 들어, &quot;swimming&quot;이라는 단어를 입력하면 해당 문자가 해당 순서로 시작되는 모든 자산 파일 이름이 검색됩니다. 자산을 찾으려면 용어를 입력한 후 Enter 키를 누르십시오.

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL 폴더/경로]** - 나타나는 폴더의 이름은 선택한 구성을 기반으로 합니다. 폴더 아이콘을 탭하고 하위 폴더를 선택한 다음 확인 표시를 눌러 하위 레벨로 드릴다운할 수 있습니다.

키워드를 입력하고 폴더를 선택하는 경우, AEM은 해당 폴더 및 하위 폴더를 검색합니다. 그러나 검색 시 키워드를 입력하지 않을 경우 폴더를 선택하면 해당 폴더의 자산만 표시되고 하위 폴더는 포함되지 않습니다.

기본적으로 AEM은 선택한 폴더 및 모든 하위 폴더를 검색합니다.

![chlimage_1-243](assets/chlimage_1-243.png)

**[!UICONTROL 자산 유형]** - Dynamic Media **[!UICONTROL Classic]** 내용을 찾아보려면 Dynamic Media Classic을 선택합니다. 이 옵션은 Dynamic Media Classic이 구성된 경우에만 사용할 수 있습니다.

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL 구성]** - [!UICONTROL Cloud Service]에 두 개 이상의 Dynamic Media Classic 구성이 정의된 경우 여기에서 선택할 수 있습니다. 결과적으로 폴더는 선택한 구성에 따라 변경됩니다.

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL 자산 유형]** - Dynamic Media Classic 브라우저 내에서 결과를 필터링하여 다음을 포함할 수 있습니다. 이미지, 템플릿, 비디오 및 적응형 비디오 세트 자산 유형을 선택하지 않으면 기본적으로 AEM은 모든 자산 유형을 검색합니다.

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* 클래식 UI에서 **Flash** 및 **FXG**&#x200B;를 검색할 수도 있습니다. 현재는 터치에 적합한 UI에서 이러한 항목을 필터링할 수 없습니다.
   >
   >
* 비디오를 검색할 때 단일 표현물을 검색합니다. 결과는 원래 변환(&amp;ast;.mp4만)과 인코딩된 변환을 반환합니다.
>* 응용 비디오 세트를 검색할 때 폴더 및 모든 하위 폴더가 검색되지만, 검색에 키워드를 추가한 경우에만 검색됩니다. 키워드를 추가하지 않은 경우 AEM이 하위 폴더를 검색하지 않습니다.

>



**[!UICONTROL 게시 상태]** - 게시 상태를 기반으로 자산에 대해 필터링할 수 있습니다. **[!UICONTROL 게시 취소]** 또는 **[!UICONTROL 게시됨.]** 게시 상태를 선택하지 않으면 기본적으로 **[!UICONTROL AEM은]**&#x200B;모든 게시 상태를 검색합니다.

![chlimage_1-247](assets/chlimage_1-247.png)

