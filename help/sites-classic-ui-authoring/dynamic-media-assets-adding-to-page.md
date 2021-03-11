---
title: 페이지에 Dynamic Media 자산 추가
description: 웹 사이트에서 사용하는 자산에 Dynamic Media 기능을 추가하기 위해 Dynamic Media 또는 대화형 미디어 구성 요소를 페이지에 바로 추가할 수 있습니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
translation-type: tm+mt
source-git-commit: 4090b1641467c6fb02b2fcce4df97b9fd5da4e2f
workflow-type: tm+mt
source-wordcount: '1685'
ht-degree: 92%

---


# 페이지에 Dynamic Media 자산 추가{#adding-dynamic-media-assets-to-pages}

웹 사이트에서 사용하는 자산에 Dynamic Media 기능을 추가하기 위해 **[!UICONTROL Dynamic Media]** 또는 **[!UICONTROL 대화형 미디어]** 구성 요소를 페이지에 바로 추가할 수 있습니다. 이렇게 하려면 [!UICONTROL 디자인] 모드를 시작하고 Dynamic Media 구성 요소를 활성화합니다. 그런 다음이 구성 요소를 페이지에 추가하고 자산을 구성 요소에 추가할 수 있습니다. Dynamic Media 및 인터랙티브 미디어 구성 요소는 편리하게도 이미지를 추가할지 아니면 비디오를 추가할지 여부와 그에 따라 사용 가능한 옵션이 달라집니다.

AEM을 WCM으로 사용하는 경우 페이지에 직접 Dynamic Media 자산을 추가합니다.

>[!NOTE]
>
>이미지 맵은 회전 배너에 즉시 사용할 수 있습니다.

## 페이지에 Dynamic Media 구성 요소 추가 {#adding-a-dynamic-media-component-to-a-page}

[!UICONTROL Dynamic Media] 또는 [!UICONTROL 대화형 미디어] 구성 요소를 페이지에 추가하는 것은 페이지에 구성 요소를 추가하는 것과 같습니다. [!UICONTROL Dynamic Media] 및 [!UICONTROL I대화형 미디어] 구성 요소는 다음 섹션에서 자세히 설명합니다.

페이지에 Dynamic Media 구성 요소/뷰어를 추가하려면 다음을 수행하십시오.

1. AEM에서 Dynamic Media 구성 요소를 추가할 페이지를 엽니다.
1. 사용 가능한 Dynamic Media 구성 요소가 없을 경우, [!UICONTROL 사이드 킥]의 눈금자를 클릭하여 **[!UICONTROL 디자인]** 모드로 전환하고 **[!UICONTROL 편집]** ParSys를 클릭한 다음, **[!UICONTROL Dynamic Media]**&#x200B;를 선택하여 Dynamic Media 구성 요소를 사용 가능하게 만드십시오.

   >[!NOTE]
   >
   >자세한 내용은 [디자인 모드에서 구성 요소 구성](/help/sites-authoring/default-components-designmode.md)을 참조하십시오.

1. [!UICONTROL 사이드 킥]에서 연필 아이콘을 클릭하여 **[!UICONTROL 편집]** 모드로 돌아갑니다.
1. **[!UICONTROL Dynamic Media]** 또는 **[!UICONTROL 대화형 미디어]** 구성 요소를 사이드 킥의 **[!UICONTROL 기타]** 그룹에서 원하는 위치의 페이지로 드래그합니다.
1. **[!UICONTROL 편집]**&#x200B;을 클릭하여 구성 요소를 엽니다.
1. [](#dynamic-media-component)필요에 따라 구성 요소를 편집하고 **[!UICONTROL 확인]**&#x200B;을 클릭하여 변경 내용을 저장합니다.

## Dynamic Media 구성 요소 {#dynamic-media-components}

[!UICONTROL Dynamic Media] 및 [!UICONTROL 대화형 미디어]는 Dynamic Media 아래의 [!UICONTROL 사이드 킥]에서 사용할 수 있습니다.**** 대화형 비디오, 대화형 이미지 또는 회전 메뉴 세트와 같은 대화형 자산에 **[!UICONTROL 대화형 미디어]** 구성 요소를 사용합니다. 다른 모든 Dynamic Media 구성 요소의 경우 **[!UICONTROL Dynamic Media]** 구성 요소를 사용하십시오.

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>이러한 구성 요소는 기본적으로 사용할 수 없으며 사용하기 전에 디자인 모드에서 선택해야 합니다. [디자인 모드에서 사용할 수 있게 되면](/help/sites-authoring/default-components-designmode.md) 다른 AEM 구성 요소에서처럼 페이지에 구성 요소를 추가할 수 있습니다. 

### Dynamic Media 구성 요소 {#dynamic-media-component}

Dynamic Media 구성 요소는 편리하게도 이미지를 추가하는지 아니면 비디오를 추가하는지에 따라 사용 가능한 선택 사항이 달라집니다. 이 구성 요소는 이미지 사전 설정, 이미지 세트와 같은 이미지 기반 뷰어, 스핀 세트, 혼합 미디어 세트 및 비디오를 지원합니다. 또한 뷰어는 응답형입니다. 즉, 화면 크기가 스크린의 크기에 따라 자동으로 변경됩니다. 모든 뷰어는 HTML5 기반 뷰어입니다.

>[!NOTE]
>
>[!UICONTROL Dynamic Media] 구성 요소를 추가하고 **[!UICONTROL Dynamic Media 설정]**&#x200B;이 비어 있거나 자산을 제대로 추가할 수 없는 경우, 다음을 확인하십시오.
>
>* [Dynamic Media를 활성화](/help/assets/config-dynamic.md)했습니다. Dynamic Media는 기본적으로 비활성화됩니다.
>* 이미지에 피라미드형 tiff 파일이 있습니다. Dynamic Media이 활성화되기 전에 가져온 이미지에는 피라미드형 tiff 파일이 없습니다.

>



#### 이미지 작업 시 {#when-working-with-images}

[!UICONTROL Dynamic Media] 구성 요소를 사용하면 이미지 세트, 스핀 세트 및 혼합 미디어 세트를 포함한 다이내믹 이미지를 추가할 수 있습니다. 확대하거나 축소할 수 있고, 해당하는 경우 스핀 세트 내의 이미지를 회전하거나 다른 유형의 세트에서 이미지를 선택할 수 있습니다.

구성 요소에서 바로 뷰어 사전 설정, 이미지 사전 설정 또는 이미지 형식을 구성할 수도 있습니다. 이미지가 응답하도록 하기 위해 중단점을 설정하거나 응답형 이미지 사전 설정을 적용할 수 있습니다.

![chlimage_1-72](assets/chlimage_1-72a.png)

구성 요소에서 **[!UICONTROL 편집]**&#x200B;을 클릭한 다음, **[!UICONTROL Dynamic Media 설정]**&#x200B;을 클릭하여 다음의 Dynamic Media 설정을 편집할 수 있습니다.

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>기본적으로 Dynamic Media 이미지 구성 요소는 적응형입니다. 고정 크기로 설정하려면 **[!UICONTROL 고급]** 탭의 구성 요소에서 **[!UICONTROL 폭]** 및 **[!UICONTROL 높이]** 속성을 설정하십시오.

**[!UICONTROL 뷰어 사전 설정]** - 드롭다운 메뉴에서 기존 뷰어 사전 설정을 선택합니다. 보려는 뷰어 사전 설정이 표시되지 않을 경우 표시되도록 설정해야 할 수 있습니다. [뷰어 사전 설정 관리](/help/assets/managing-viewer-presets.md)를 참조하십시오. 이미지 사전 설정을 사용 중일 때는 뷰어 사전 설정을 선택할 수 없고 그 반대의 경우도 마찬가지입니다.

이미지 세트, 스핀 세트 또는 혼합 미디어 세트를 보는 경우 사용할 수 있는 유일한 선택 사항입니다. 표시되는 뷰어 사전 설정은 편리하게도 적절한 뷰어 사전 설정만 표시됩니다.

**[!UICONTROL 이미지 사전 설정]** - 드롭다운 메뉴에서 기존 이미지 사전 설정을 선택합니다. 보려는 이미지 사전 설정이 표시되지 않을 경우 표시되도록 설정해야 할 수 있습니다. [이미지 사전 설정 관리](/help/assets/managing-image-presets.md)를 참조하십시오. 이미지 사전 설정을 사용 중일 때는 뷰어 사전 설정을 선택할 수 없고 그 반대의 경우도 마찬가지입니다.

이미지 세트, 스핀 세트 또는 혼합 미디어 세트를 보는 경우에는 이 선택 사항을 사용할 수 없습니다.

**[!UICONTROL 이미지 수정자]** - 추가적인 이미지 명령을 제공하여 이미지 효과를 변경할 수 있습니다. 이러한 내용은 [이미지 사전 설정 관리](/help/assets/managing-viewer-presets.md) 및 [명령 참조](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html)에 설명되어 있습니다.

이미지 세트, 스핀 세트 또는 혼합 미디어 세트를 보는 경우에는 이 선택 사항을 사용할 수 없습니다.

**[!UICONTROL 중단점]** - 응답형 사이트에서 이 자산을 사용하는 경우 페이지 중단점을 추가해야 합니다. 이미지 중단점은 쉼표(,)로 구분해야 합니다. 이 선택 사항은 이미지 사전 설정에 정의된 높이나 폭이 없는 경우에 작동합니다.

이미지 세트, 스핀 세트 또는 혼합 미디어 세트를 보는 경우에는 이 선택 사항을 사용할 수 없습니다.

구성 요소에서 **[!UICONTROL 편집]**&#x200B;을 클릭하여 다음 [!UICONTROL 고급 설정]을 편집할 수 있습니다.

**[!UICONTROL 제목]** - 이미지의 제목을 변경합니다.

**[!UICONTROL 대체 텍스트]** - 그래픽이 꺼진 사용자의 이미지에 제목을 추가합니다.

이미지 세트, 스핀 세트 또는 혼합 미디어 세트를 보는 경우에는 이 선택 사항을 사용할 수 없습니다.

**[!UICONTROL URL, 여는 위치]** - 링크를 열 자산을 설정할 수 있습니다. **[!UICONTROL URL]** 및 **[!UICONTROL 여는 위치]**&#x200B;를 설정하여 같은 창에서 열지 또는 새 창에서 열지를 지정합니다.

이미지 세트, 스핀 세트 또는 혼합 미디어 세트를 보는 경우에는 이 선택 사항을 사용할 수 없습니다.

**[!UICONTROL 폭과 높이]** - 이미지의 크기를 고정하려면 값을 픽셀 단위로 입력하십시오. 이 값을 공백으로 두면 자산이 적응형으로 설정됩니다.

#### 비디오 작업 시 {#when-working-with-video}

[!UICONTROL Dynamic Media] 구성 요소를 사용하여 웹 페이지에 다이내믹 비디오를 추가하십시오. 구성 요소를 편집할 때 페이지에서 비디오를 재생하기 위해 사전 설정된 비디오 뷰어 사전 설정을 사용하도록 선택할 수 있습니다.

![chlimage_1-74](assets/chlimage_1-74a.png)

구성 요소에서 **[!UICONTROL 편집]**&#x200B;을 클릭하여 다음 [!UICONTROL Dynamic Media 설정]을 편집할 수 있습니다.

>[!NOTE]
>
>기본적으로 Dynamic Media 비디오 구성 요소는 적응형입니다. 고정 크기로 설정하려면 **[!UICONTROL 고급]** 탭에서 **[!UICONTROL 폭]** 및 **[!UICONTROL 높이]**&#x200B;로 구성 요소를 설정하십시오.

**[!UICONTROL 뷰어 사전 설정]** - 드롭다운 메뉴에서 기존 비디오 뷰어 사전 설정을 선택합니다. 보려는 뷰어 사전 설정이 표시되지 않을 경우 표시되도록 설정해야 할 수 있습니다. [뷰어 사전 설정 관리](/help/assets/managing-viewer-presets.md)를 참조하십시오. 

구성 요소에서 **[!UICONTROL 편집]**&#x200B;을 클릭하여 다음 [!UICONTROL 고급] 설정을 편집할 수 있습니다.

**[!UICONTROL 제목]** - 비디오의 제목을 변경합니다.

**[!UICONTROL 폭과 높이]** - 비디오의 크기를 고정하려면 값을 픽셀 단위로 입력하십시오. 이 값을 공백으로 두면 적응형으로 설정됩니다.

#### 보안 비디오 제공 방법 {#how-to-delivery-secure-video}

AEM 6.2에서 [FP-13480](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480)을 설치하면 비디오가 보안 SSL 연결(HTTPS)을 통해 제공되는지 아니면 비보안 연결(HTTP)을 통해 제공되는지를 제어할 수 있습니다. 기본적으로, 비디오 제공 프로토콜은 포함 웹 페이지의 프로토콜에서 자동으로 상속됩니다. 웹 페이지가 HTTPS를 통해 로드되는 경우 비디오도 HTTPS를 통해 제공됩니다. 또한 반대로, 웹 페이지가 HTTP에 있는 경우에는 비디오가 HTTP를 통해 제공됩니다. 대부분의 경우 이러한 기본 동작은 정상적이며 구성을 변경할 필요가 없습니다. 그러나 비디오 제공 URL 경로의 끝이나 포함 코드 조각에 있는 다른 뷰어 구성 매개 변수 목록에 `VideoPlayer.ssl=on`을 추가하여 이 기본 동작을 무시함으로써 보안 비디오 제공을 강제 적용할 수 있습니다.

보안 비디오 제공과 URL 경로에 있는 `VideoPlayer.ssl` 구성 속성에 대한 자세한 내용은 뷰어 참조 가이드의 [보안 비디오 제공](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-viewer-20-securevideodelivery.html)을 참조하십시오. 비디오 뷰어 이외에 혼합 비디오 뷰어와 대화형 비디오 뷰어에 보안 비디오를 게재할 수 있습니다.

### 대화형 미디어 구성 요소 {#interactive-media-component}

대화형 미디어 구성 요소는 핫스팟이나 이미지 맵과 같은 상호 작용이 있는 자산을 위한 것입니다. 대화형 이미지, 대화형 비디오 또는 회전 배너가 있는 경우 **[!UICONTROL 대화형 미디어]** 구성 요소를 사용하십시오.

[!UICONTROL 대화형 미디어] 구성 요소는 편리하게도 이미지를 추가하는지 아니면 비디오를 추가하는지에 따라 사용 가능한 선택 사항이 달라집니다. 또한 뷰어는 응답형입니다. 즉, 화면 크기가 스크린의 크기에 따라 자동으로 변경됩니다. 모든 뷰어는 HTML5 기반 뷰어입니다.

![chlimage_1-75](assets/chlimage_1-75a.png)

구성 요소에서 **[!UICONTROL 편집]**&#x200B;을 클릭하여 다음 **[!UICONTROL 일반]** 설정을 편집할 수 있습니다.

**[!UICONTROL 뷰어 사전 설정]** - 드롭다운 메뉴에서 기존 뷰어 사전 설정을 선택합니다. 보려는 뷰어 사전 설정이 표시되지 않을 경우 표시되도록 설정해야 할 수 있습니다. 뷰어 사전 설정을 사용하려면 먼저 게시해야 합니다. 뷰어 사전 설정 관리를 참조하십시오.

**[!UICONTROL 제목]** - 비디오의 제목을 변경합니다.

**[!UICONTROL 폭과 높이]** - 비디오의 크기를 고정하려면 값을 픽셀 단위로 입력하십시오. 이 값을 공백으로 두면 적응형으로 설정됩니다.

구성 요소에서 **[!UICONTROL 편집]**&#x200B;을 클릭하여 다음 **[!UICONTROL 장바구니에 추가]** 설정을 편집할 수 있습니다.

**[!UICONTROL 제품 자산 표시]** - 기본적으로 이 값이 선택되어 있습니다. 제품 자산은 상거래 모듈에 정의된 제품의 이미지를 보여줍니다. 제품 자산을 표시하지 않도록 하려면 확인 표시를 지우십시오.

**[!UICONTROL 제품 가격 표시]** - 기본적으로 이 값이 선택되어 있습니다. 제품 가격은 상거래 모듈에 정의된 항목 가격을 보여줍니다. 제품 가격을 표시하지 않도록 하려면 확인 표시를 지우십시오.

**[!UICONTROL 제품 양식 표시]** - 기본적으로 이 값이 선택되어 있지 않습니다. 제품 양식에는 크기 및 색상과 같은 모든 제품 변형이 포함됩니다. 제품 변형을 표시하지 않도록 하려면 확인 표시를 지우십시오.
