---
title: Adobe Analytics 및 Experience Platform 태그와 Dynamic Media Viewer 통합
description: Experience Platform 태그 및 Dynamic Media 뷰어 5.13용 Dynamic Media 뷰어 확장에 대해 알아봅니다. Adobe Analytics 및 Experience Platform Tags 고객이 Experience Platform Tags 구성에서 Dynamic Media Viewer와 관련된 이벤트 및 데이터를 사용할 수 있도록 해줍니다.
mini-toc-levels: 3
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
feature: Viewers
role: User, Admin, Developer
exl-id: 161dfe22-bc1c-4b60-8ab6-a19407a39e2e
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '6677'
ht-degree: 5%

---

# Adobe Analytics 및 Experience Platform 태그와 Dynamic Media Viewer 통합 {#integrating-dynamic-media-viewers-with-adobe-analytics-and-adobe-launch}

## Adobe Analytics 및 Experience Platform 태그와 Dynamic Media Viewer 통합이란 무엇입니까? {#what-is-dynamic-media-viewers-integration-with-adobe-analytics-and-adobe-launch}

<!-- Leave this hidden path here; it points to the topic source from Sasha https://wiki.corp.adobe.com/pages/viewpage.action?spaceKey=~oufimtse&title=Dynamic+Media+Viewers+integration+with+Adobe+Launch -->

Experience Platform 태그 및 Dynamic Media 뷰어 5.13용 *Dynamic Media 뷰어* 확장 기능을 사용하면 Adobe Analytics 및 Experience Platform 태그 고객이 Experience Platform 태그 구성에서 Dynamic Media 뷰어에 대한 이벤트 및 데이터를 사용할 수 있습니다.

이 통합은 Adobe Analytics을 사용하여 웹 사이트에서 Dynamic Media 뷰어 사용을 추적할 수 있음을 의미합니다. 동시에 Adobe 또는 서드파티의 다른 Experience Platform 태그 확장과 함께 뷰어가 노출하는 이벤트 및 데이터를 사용할 수 있습니다.

Adobe 확장 또는 타사 확장에 대한 자세한 내용은 Experience Platform 태그 사용 안내서의 [Adobe 확장](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/overview)을 참조하십시오.

**이 항목은 다음을 위한 것입니다.** 사이트 관리자, Experience Platform의 개발자 및 작업 중인 사람.

### 통합의 제한 사항 {#limitations-of-the-integration}

* Dynamic Media 뷰어에 대한 Experience Platform 태그 통합이 Experience Manager 작성자 노드에서 작동하지 않습니다. WCM 페이지는 게시될 때까지 추적할 수 없습니다.
* Dynamic Media 뷰어에 대한 Experience Platform 태그 통합은 자산 세부 사항 페이지의 &quot;URL&quot; 단추를 사용하여 뷰어 URL을 가져오는 &quot;팝업&quot; 작업 모드에서는 지원되지 않습니다.
* Experience Platform 태그 통합은 기존 뷰어 Analytics 통합과 동시에 사용할 수 없습니다(`config2=` 매개 변수 사용).
* 비디오 추적 지원은 [추적 개요](https://experienceleague.adobe.com/en/docs/media-analytics/using/tracking/track-core-overview)에 설명된 대로 &quot;코어 재생&quot; 추적으로만 제한됩니다. 특히 QoS, 광고, 챕터/세그먼트 또는 오류 추적이 지원되지 않습니다.
* *Dynamic Media 뷰어* 확장을 사용하는 데이터 요소에 대해서는 데이터 요소에 대한 저장소 기간 구성이 지원되지 않습니다. 저장소 기간은 **[!UICONTROL 없음]**(으)로 설정해야 합니다.

### 통합에 대한 사용 사례 {#use-cases-for-the-integration}

Experience Platform 태그와 통합하기 위한 주요 사용 사례는 Adobe Experience Manager Assets과 Adobe Experience Manager Sites을 모두 사용하는 고객입니다. 이러한 시나리오에서는 Experience Manager 작성자 노드와 Experience Platform Tags 간에 표준 통합을 설정한 다음 Sites 인스턴스를 Experience Platform Tags 속성과 연결할 수 있습니다. 이후 Sites 페이지에 추가된 모든 Dynamic Media WCM 구성 요소는 뷰어의 데이터 및 이벤트를 추적합니다.

[Experience Manager Sites에서 Dynamic Media 뷰어 추적](#tracking-dynamic-media-viewers-in-aem-sites)을 참조하세요.

통합이 지원하는 보조 사용 사례는 Experience Manager Assets 전용 또는 Dynamic Media Classic을 사용하는 고객입니다. 이러한 경우 뷰어에 대한 포함 코드를 가져와 웹 사이트 페이지에 추가합니다. 그런 다음 Experience Platform Tags에서 Experience Platform Tags 라이브러리 프로덕션 URL을 가져와 웹 페이지 코드에 수동으로 추가합니다.

[포함 코드를 사용하여 Dynamic Media 뷰어 추적](#tracking-dynamic-media-viewers-using-embed-code)을 참조하세요.

<!-- Path on internal wiki [About tracking Dynamic Media viewers using embed code](https://wiki.corp.adobe.com/display/~oufimtse/Dynamic+Media+Viewers+integration+with+Adobe+Launch#DynamicMediaViewersintegrationwithAdobeLaunch-TrackingDynamicMediaViewersusingEmbedcode). -->

## 통합에서 데이터 및 이벤트 추적이 작동하는 방식 {#how-data-and-event-tracking-works-in-the-integration}

통합에서는 Dynamic Media 뷰어 추적의 두 가지 독립적이고 분리된 유형(*Adobe Analytics* 및 *오디오 및 비디오용 Adobe Analytics*)을 사용합니다.

### Adobe Analytics을 사용한 추적 기본 정보  {#about-tracking-using-adobe-analytics}

Adobe Analytics을 사용하면 최종 사용자가 웹 사이트에서 Dynamic Media 뷰어와 상호 작용할 때 수행하는 작업을 추적할 수 있습니다. Adobe Analytics을 사용하면 뷰어별 데이터를 추적할 수도 있습니다. 예를 들어, 자산 이름, 발생한 확대/축소 작업 및 비디오 재생 작업과 함께 보기 로드 이벤트를 추적하고 기록할 수 있습니다.

Experience Platform 태그에서 *데이터 요소* 및 *규칙*&#x200B;의 개념이 함께 작동하여 Adobe Analytics 추적을 사용하도록 설정합니다.

#### Experience Platform 태그의 데이터 요소 정보 {#about-data-elements-in-adobe-launch}

Experience Platform Tags의 Data Element는 값이 웹 페이지 또는 Dynamic Media 뷰어 데이터의 상태에 따라 정적으로 정의되거나 동적으로 계산되는 명명된 속성입니다.

데이터 요소 정의에 사용할 수 있는 옵션은 Experience Platform 태그 속성에 설치된 확장 목록에 따라 다릅니다. &quot;코어&quot; 확장은 사전 설치되어 있으며 모든 구성에서 즉시 사용할 수 있습니다. 이 &quot;코어&quot; 확장을 사용하면 쿠키, JavaScript 코드, 쿼리 문자열 및 기타 다양한 소스에서 가져온 데이터 요소를 정의할 수 있습니다.

Adobe Analytics 추적의 경우 [확장 설치 및 설정](#installing-and-setup-of-extensions)에 설명된 대로 몇 가지 확장을 더 설치해야 합니다. Dynamic Media 뷰어 확장 기능은 Dynamic Viewer 이벤트의 인수인 데이터 요소를 정의하는 기능을 추가합니다. 예를 들어 뷰어 유형 또는 로드 시 뷰어에서 보고하는 자산 이름, 최종 사용자가 확대/축소할 때 보고되는 확대/축소 수준 등을 참조할 수 있습니다.

Dynamic Media 뷰어 확장 기능은 데이터 요소 값을 자동으로 최신 상태로 유지합니다.

데이터 요소를 정의한 후 데이터 요소 선택기 위젯을 사용하여 Experience Platform Tags UI의 다른 위치에서 데이터 요소를 사용할 수 있습니다. 특히, Dynamic Media 뷰어 추적을 위해 정의된 데이터 요소는 규칙에서 Adobe Analytics 확장의 변수 설정 작업에서 참조됩니다(아래 참조).

[데이터 요소](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/data-elements)를 참조하십시오.

#### Experience Platform 태그의 규칙 정보 {#about-rules-in-adobe-launch}

Experience Platform Tags의 규칙은 규칙을 구성하는 세 가지 영역(*이벤트*, *조건* 및 *작업*)을 정의하는 독립적인 구성입니다.

* *이벤트*(if) 규칙을 트리거할 시기를 Experience Platform 태그에 알립니다.
* *조건*(if)은(는) 규칙을 트리거할 때 허용하거나 허용하지 않는 다른 제한 사항을 Experience Platform Tags에 알려줍니다.
* *작업*(그런 다음) 규칙이 트리거될 때 수행할 작업을 Experience Platform Tags에 알립니다.

이벤트, 조건 및 작업 섹션에서 사용할 수 있는 옵션은 Experience Platform 태그 속성에 설치된 확장에 따라 다릅니다. *Core* 확장이 미리 설치되어 있으며 모든 구성에서 즉시 사용할 수 있습니다. 확장은 기본 브라우저 수준 작업과 같은 이벤트에 대한 몇 가지 옵션을 제공합니다. 이러한 작업에는 포커스 변경, 키 누르기 및 양식 제출이 포함됩니다. 쿠키 값, 브라우저 유형 등과 같은 조건에 대한 옵션도 포함되어 있습니다. 작업의 경우 사용자 지정 코드 옵션만 사용할 수 있습니다.

Adobe Analytics 추적을 위해 [확장 설치 및 설정](#installing-and-setup-of-extensions)에 설명된 대로 다른 확장 몇 개를 설치해야 합니다. 특히:

* Dynamic Media 뷰어 확장 기능은 지원되는 이벤트 목록을 뷰어 로드, 에셋 교체, 확대 및 비디오 재생과 같은 Dynamic Media 뷰어와 관련된 이벤트로 확장합니다.
* Adobe Analytics 확장은 추적 서버로 데이터를 보내는 데 필요한 두 가지 작업으로 지원되는 작업 목록을 확장합니다. *변수 설정* 및 *비콘 보내기*.

Dynamic Media 뷰어를 추적하려면 다음 유형을 사용할 수 있습니다.

* Dynamic Media 뷰어 확장, 코어 확장 또는 기타 확장의 이벤트.
* 규칙 정의의 조건. 또는 조건 영역을 비워둘 수 있습니다.

작업 섹션에서 *변수 설정* 작업이 필요합니다. 이 작업은 Adobe Analytics에 추적 변수를 데이터로 채우는 방법을 알려 줍니다. 동시에 *변수 설정* 작업은 추적 서버로 아무 것도 보내지 않습니다.

*변수 설정* 동작 뒤에는 *비콘 보내기* 동작이 와야 합니다. *비콘 보내기* 작업은 실제로 Analytics 추적 서버로 데이터를 보냅니다. *변수 설정* 및 *비콘 보내기* 작업은 모두 Adobe Analytics 확장에서 가져옵니다.

[규칙](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules)을 참조하세요.

#### 샘플 구성 {#sample-configuration}

Experience Platform Tags 내의 다음 샘플 구성은 뷰어 로드 시 에셋 이름을 추적하는 방법을 보여 줍니다.

1. **[!UICONTROL 데이터 요소]** 탭에서 Dynamic Media 뷰어 확장에서 `AssetName` 이벤트의 `asset` 매개 변수를 참조하는 데이터 요소 `LOAD`을(를) 정의합니다.

   ![image2019-11](assets/image2019-11.png)

1. **[!UICONTROL 규칙]** 탭에서 *TrackAssetOnLoad* 규칙을 정의합니다.

   이 규칙에서 **[!UICONTROL 이벤트]** 필드는 Dynamic Media 뷰어 확장의 **[!UICONTROL LOAD]** 이벤트를 사용합니다.

   ![image2019-22](assets/image2019-22.png)

1. 작업 구성에는 Adobe Analytics 확장의 두 가지 작업 유형이 있습니다.

   *변수 설정*. 선택한 분석 변수를 `AssetName` 데이터 요소의 값에 매핑합니다.

   Adobe Analytics에 추적 정보를 보내는 *비콘 보내기*.

   ![image2019-3](assets/image2019-3.png)

1. 결과 규칙 구성은 다음과 같습니다.

   ![image2019-4](assets/image2019-4.png)

### 오디오 및 비디오용 Adobe Analytics 정보 {#about-adobe-analytics-for-audio-and-video}

Experience Cloud 계정이 오디오 및 비디오용 Adobe Analytics을 사용하도록 구독되면 *Dynamic Media 뷰어* 확장 설정에서 비디오 추적을 사용하도록 설정하는 것으로 충분합니다. Adobe Analytics에서 비디오 지표를 사용할 수 있게 되었습니다. 비디오 추적은 Adobe Media Analytics for Audio 및 Video 확장의 존재 여부에 따라 다릅니다.

[확장 설치 및 설정](#installing-and-setup-of-extensions)을 참조하세요.

현재 비디오 추적은 [추적 개요](https://experienceleague.adobe.com/en/docs/media-analytics/using/tracking/track-core-overview)에 설명된 대로 &quot;코어 재생&quot; 추적으로만 지원됩니다. 특히 QoS, 광고, 챕터/세그먼트 또는 오류 추적이 지원되지 않습니다.

## Dynamic Media 뷰어 확장 사용 {#using-the-dynamic-media-viewers-extension}

[통합을 위한 사용 사례](#use-cases-for-the-integration)에서 언급한 바와 같이, Experience Manager Sites의 새로운 Experience Platform 태그 통합과 포함 코드를 사용하여 Dynamic Media 뷰어를 추적할 수 있습니다.

### Experience Manager Sites에서 Dynamic Media 뷰어 추적 {#tracking-dynamic-media-viewers-in-aem-sites}

Experience Manager Sites에서 Dynamic Media 뷰어를 추적하려면 [모든 통합 조각 구성](#configuring-all-the-integration-pieces) 섹션에 나열된 모든 단계를 수행해야 합니다. 특히 IMS 구성 및 Experience Platform Tags Cloud 구성을 만들어야 합니다.

적절한 구성에 따라 Dynamic Media에서 지원하는 WCM 구성 요소를 사용하여 Sites 페이지에 추가하는 모든 Dynamic Media 뷰어는 Adobe Analytics 또는 비디오용 Adobe Analytics에 데이터를 자동으로 추적하거나 두 가지 모두에 대해 추적합니다.

<!-- To be reviewed and updated although this is found live in the Experience ManageraaCS version:
See [Adding Dynamic Media Assets to Pages using Adobe Sites](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html).
-->

### 포함 코드를 사용하여 Dynamic Media 뷰어 추적 {#tracking-dynamic-media-viewers-using-embed-code}

Experience Manager Sites을 사용하지 않거나 Experience Manager Sites 외부의 웹 페이지에 Dynamic Media 뷰어를 임베드하지 않은 고객 또는 두 고객 모두 여전히 Experience Platform 태그 통합을 사용할 수 있습니다.

[Adobe Analytics 구성](#configuring-adobe-analytics-for-the-integration) 및 [Experience Platform 태그 구성](#configuring-adobe-launch-for-the-integration) 섹션에서 구성 단계를 완료합니다. 그러나 Experience Manager 관련 구성 단계는 필요하지 않습니다.

적절한 구성에 따라 Dynamic Media 뷰어를 사용하여 웹 페이지에 Experience Platform 태그 지원을 추가할 수 있습니다.

Experience Platform 태그 라이브러리 포함 코드를 사용하는 방법에 대한 자세한 내용은 [Experience Platform 태그 포함 코드 추가](https://experienceleague.adobe.com/en/docs/platform-learn/implement-in-websites/configure-tags/add-embed-code)를 참조하십시오.

<!-- To be reviewed and updated although this is found live in the Experience ManageraaCS version:
See [Embedding the Video or Image Viewer on a Web Page](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html) to learn more about how to use the embed code feature of Experience Manager Dynamic Media.
-->

**포함 코드를 사용하여 Dynamic Media 뷰어 추적:**

1. Dynamic Media 뷰어를 포함할 웹 페이지를 준비했습니다.
1. 먼저 Experience Platform 태그에 로그인하여 Experience Platform 태그 라이브러리의 포함 코드를 가져옵니다([Experience Platform 태그 구성](#configuring-adobe-launch-for-the-integration) 참조).
1. **[!UICONTROL 속성]**&#x200B;을 선택한 다음 **[!UICONTROL 환경]** 탭을 선택합니다.
1. 웹 페이지의 환경과 관련된 환경 수준을 선택합니다. 그런 다음 **[!UICONTROL 설치]** 열에서 상자 아이콘을 선택합니다.
1. **[!UICONTROL 웹 설치 지침]** 대화 상자에서 주변의 `<script/>` 태그와 함께 전체 Experience Platform 태그 라이브러리 포함 코드를 복사합니다.

## Dynamic Media 뷰어 확장에 대한 참조 안내서 {#reference-guide-for-the-dynamic-media-viewers-extension}

### Dynamic Media 뷰어 구성 정보 {#about-the-dynamic-media-viewers-configuration}

아래 조건이 참인 경우 Dynamic Media 뷰어 확장 기능은 Experience Platform 태그 라이브러리와 자동으로 통합됩니다.

* Experience Platform 태그 라이브러리 전역 개체(`_satellite`)가 페이지에 있습니다.
* Dynamic Media 뷰어 확장 함수 `_dmviewers_v001()`이(가) `_satellite`에 정의되어 있습니다.

* `config2=` 뷰어 매개 변수가 지정되지 않았습니다. 즉, 뷰어가 이전 Analytics 통합을 사용하지 않습니다.

또한 뷰어 구성에서 `launch=0` 매개 변수를 지정하여 뷰어에서 Experience Platform Tags 통합을 명시적으로 비활성화하는 옵션이 있습니다. 이 매개 변수의 기본값은 `1`입니다.

### Dynamic Media 뷰어 확장 구성 {#configuring-the-dynamic-media-viewers-extension}

Dynamic Media 뷰어 확장에 대한 유일한 구성 옵션은 **[!UICONTROL 오디오 및 비디오용 Adobe Media Analytics 활성화]**&#x200B;입니다.

이 옵션을 선택하고(활성화) 오디오 및 비디오 확장 기능용 Adobe Media Analytics가 설치 및 구성되면 비디오 재생 지표가 오디오 및 비디오 솔루션용 Adobe Analytics으로 전송됩니다. 이 옵션을 비활성화하면 비디오 추적이 꺼집니다.

Adobe Media Analytics for Audio and Video 확장 설치 없이 *이 옵션을 사용하도록 설정한 경우 이 옵션은 효과가 없습니다.*

![image2019-7-22_12-4-23](assets/image2019-7-22_12-4-23.png)

### Dynamic Media 뷰어 확장의 데이터 요소 정보 {#about-data-elements-in-the-dynamic-media-viewers-extension}

The only Data Element type that the Dynamic Media Viewers extension provides is **[!UICONTROL Viewer Event]** from the **[!UICONTROL Data Element Type]** drop-down list.

선택하면 데이터 요소 편집기에서 두 개의 필드가 있는 양식을 렌더링합니다.

* **[!UICONTROL DM viewers event data type]** - a drop-down list that identifies all viewer events that are supported by the Dynamic Media Viewers extension which have arguments, plus a special **[!UICONTROL COMMON]** item. A **[!UICONTROL COMMON]** item represents a list of event parameters that are common to all type of events sent by the viewers.
* **[!UICONTROL 추적 매개 변수]** - 선택한 Dynamic Media 뷰어 이벤트의 인수.

![image2019-7-22_12-5-46](assets/image2019-7-22_12-5-46.png)

각 뷰어 유형별 지원되는 이벤트 목록은 [Dynamic Media 뷰어 참조 안내서](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers#viewers-aem-assets-dmc)를 참조하십시오. 특정 뷰어 섹션으로 이동한 다음 Adobe Analytics 추적 지원 하위 섹션을 선택하십시오. 현재 Dynamic Media 뷰어 참조 안내서에서는 이벤트 인수를 문서화하지 않습니다.

이제 Dynamic Media 뷰어 *데이터 요소*&#x200B;의 수명 주기를 고려하십시오. 이러한 데이터 요소의 값은 해당 Dynamic Media 뷰어 이벤트가 페이지에서 발생한 후에 채워집니다. 예를 들어 데이터 요소가 **[!UICONTROL LOAD]** 이벤트와 그 &quot;asset&quot; 인수를 가리킨다고 가정합니다. 이 경우 뷰어가 **[!UICONTROL LOAD]** 이벤트를 처음 실행한 후 이러한 데이터 요소의 값이 올바른 데이터를 받습니다. 데이터 요소가 **[!UICONTROL ZOOM]** 이벤트와 그 &quot;scale&quot; 인수를 가리키는 경우 뷰어가 **[!UICONTROL ZOOM]** 이벤트를 처음으로 보낼 때까지 해당 데이터 요소의 값은 비어 있습니다.

Similarly, the values of Data Elements get automatically updated when the viewer sends a corresponding event on the page. The value update happens even if the particular event is not specified in the Rule configuration. 예를 들어 데이터 요소 **[!UICONTROL ZoomScale]**&#x200B;이(가) ZOOM 이벤트의 &quot;scale&quot; 매개 변수에 대해 정의되어 있다고 가정합니다. 하지만 규칙 구성에 있는 유일한 규칙은 **[!UICONTROL LOAD]** 이벤트에 의해 트리거됩니다. 사용자가 뷰어 내에서 확대/축소를 실행할 때마다 **[!UICONTROL ZoomScale]** 값이 계속 업데이트됩니다.

모든 Dynamic Media 뷰어는 웹 페이지에서 고유한 식별자를 가집니다. 데이터 요소는 값 자체와 값을 채운 뷰어를 추적합니다. 예를 들어 같은 페이지에 여러 뷰어가 있고 **[!UICONTROL LOAD]** 이벤트와 &quot;asset&quot; 인수를 가리키는 **[!UICONTROL AssetName]** 데이터 요소가 있다고 가정해 봅시다. **[!UICONTROL AssetName]** 데이터 요소는 페이지에 로드된 각 뷰어와 연결된 자산 이름의 컬렉션을 유지 관리합니다.

데이터 요소가 반환하는 정확한 값은 컨텍스트에 따라 다릅니다. Dynamic Media 뷰어 이벤트에 의해 트리거된 규칙에서 데이터 요소가 요청되면 규칙을 시작한 뷰어에 대해 데이터 요소 값이 반환됩니다. 또한 데이터 요소는 다른 일부 Experience Platform 태그 확장의 이벤트에 의해 트리거된 규칙에서 요청됩니다. 이때 데이터 요소의 값은 이 데이터 요소를 마지막으로 업데이트한 뷰어에서 가져옵니다.

**다음 샘플 설정을 고려하십시오.**

* Dynamic Media 확대/축소 뷰어가 두 개인 웹 페이지입니다. *viewer1* 및 *viewer2*.

* **[!UICONTROL ZoomScale]** 데이터 요소는 **[!UICONTROL ZOOM]** 이벤트와 해당 &quot;scale&quot; 인수를 가리킵니다.
* 다음을 포함하는 **[!UICONTROL TrackPan]** 규칙:

   * Dynamic Media 뷰어 **[!UICONTROL PAN]** 이벤트를 트리거로 사용합니다.
   * **[!UICONTROL ZoomScale]** 데이터 요소의 값을 Adobe Analytics으로 보냅니다.

* 다음을 포함하는 **[!UICONTROL TrackKey]** 규칙:

   * 코어 Experience Platform 태그 확장의 키 누름 이벤트를 트리거로 사용합니다.
   * **[!UICONTROL ZoomScale]** 데이터 요소의 값을 Adobe Analytics으로 보냅니다.

이제 최종 사용자가 두 명의 뷰어가 있는 웹 페이지를 로드한다고 가정합니다. *viewer1*&#x200B;에서는 50% 배율로 확대되고 *viewer2*&#x200B;에서는 25% 배율로 확대됩니다. *viewer1*&#x200B;에서 이미지를 패닝하고 마지막으로 키보드에서 키를 선택합니다.

최종 사용자의 활동으로 인해 Adobe Analytics에 다음과 같은 두 개의 추적 호출이 수행됩니다.

* 사용자가 **[!UICONTROL viewer1]**&#x200B;에서 패닝하면 *TrackPan* 규칙이 트리거되므로 첫 번째 호출이 발생합니다. 이 호출은 **[!UICONTROL ZoomScale]** 데이터 요소의 값으로 50%를 전송합니다. 데이터 요소는 규칙이 *viewer1*&#x200B;에 의해 트리거되고 해당 크기 값을 가져온다는 것을 알고 있기 때문입니다.
* 두 번째 호출은 사용자가 키보드에서 키를 누를 때 **[!UICONTROL TrackKey]** 규칙이 트리거되기 때문에 발생합니다. 규칙이 뷰어에 의해 트리거되지 않았으므로 이 호출은 25%를 **[!UICONTROL ZoomScale]** 데이터 요소의 값으로 보냅니다. 따라서 데이터 요소는 최신 값을 반환합니다.

위에 설정된 샘플은 데이터 요소 값의 수명에도 영향을 줍니다. Dynamic Media 뷰어에서 관리하는 데이터 요소의 값은 뷰어 자체가 웹 페이지에 배치된 후에도 Experience Platform 태그 라이브러리 코드에 저장됩니다. 이 기능은 비 Dynamic Media 뷰어 확장에 의해 트리거되고 이러한 데이터 요소를 참조하는 규칙이 있는 경우 데이터 요소가 마지막으로 알려진 값을 반환함을 의미합니다. 뷰어가 웹 페이지에 더 이상 존재하지 않는 경우에도 마찬가지입니다.

어떤 경우든 Dynamic Media 뷰어에 의해 구동되는 데이터 요소 값은 로컬 저장소 또는 서버에 저장되지 않습니다. 대신 클라이언트측 Experience Platform 태그 라이브러리에만 보관됩니다. 이러한 데이터 요소의 값은 웹 페이지가 다시 로드될 때 사라집니다.

일반적으로 데이터 요소 편집기는 [저장 기간 선택](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/data-elements#create-a-data-element)을 지원합니다. 그러나 Dynamic Media 뷰어 확장을 사용하는 데이터 요소는 **[!UICONTROL 없음]**&#x200B;의 저장 유지 시간 옵션만 지원합니다. 사용자 인터페이스에서 다른 값을 설정할 수 있지만 이 경우에는 데이터 요소 동작이 정의되지 않습니다. 확장은 데이터 요소의 값을 자체적으로 관리합니다. 즉, 전체 뷰어 수명 주기 동안 뷰어 이벤트 인수의 값을 유지 관리하는 데이터 요소입니다.

### Dynamic Media 뷰어 확장의 규칙 정보 {#about-rules-in-the-dynamic-media-viewers-extension}

규칙 편집기에서 확장 기능은 이벤트 편집기에 대한 새 구성 옵션을 추가합니다. 또한 편집기에서는 사전 구성된 데이터 요소를 사용하는 대신 작업 편집기에서 이벤트 매개 변수를 직접 참조하는 옵션을 바로 사용할 수 있습니다.

#### 이벤트 편집기 정보 {#about-the-events-editor}

이벤트 편집기에서 Dynamic Media 뷰어 확장은 **[!UICONTROL 뷰어 이벤트]**&#x200B;라는 **[!UICONTROL 이벤트 유형]**&#x200B;을(를) 추가합니다.

선택하면 이벤트 편집기에서 드롭다운 **[!UICONTROL Dynamic Media 뷰어 이벤트]**&#x200B;를 렌더링하여 Dynamic Media 뷰어에서 지원하는 사용 가능한 모든 이벤트를 나열합니다.

![image2019-8-2_15-13-1](assets/image2019-8-2_15-13-1.png)

#### 작업 편집기 정보 {#about-the-actions-editor}

Dynamic Media 뷰어 확장 기능을 사용하면 Dynamic Media 뷰어의 이벤트 매개 변수를 사용하여 Adobe Analytics 확장의 변수 설정 편집기에서 Analytics 변수에 매핑할 수 있습니다.

이를 수행하는 가장 간단한 방법은 다음의 두 단계 프로세스를 완료하는 것입니다.

* 먼저 하나 이상의 데이터 요소를 정의합니다. 여기서 각 데이터 요소는 Dynamic Media 뷰어 이벤트의 매개 변수를 나타냅니다.
* 마지막으로 Adobe Analytics 확장의 변수 설정 편집기에서 **[!UICONTROL 데이터 요소]** 선택 아이콘(스택형 디스크 3개)을 선택하여 데이터 요소 선택 대화 상자를 연 다음 데이터 요소를 선택합니다.

![image2019-7-10_20-41-52](assets/image2019-7-10_20-41-52.png)

It is possible, however, to use an alternative approach and bypass Data Element creation. Dynamic Media 뷰어 이벤트에서 인수를 직접 참조할 수 있습니다. Analytics 변수 할당의 **[!UICONTROL 값]** 입력 필드에 이벤트 인수의 정규화된 이름을 입력합니다. 퍼센트(%) 기호로 둘러싸야 합니다. 예:

`%event.detail.dm.LOAD.asset%`

![image2019-7-12_19-2-35](assets/image2019-7-12_19-2-35.png)

데이터 요소 사용과 직접 이벤트 인수 참조 간에는 중요한 차이가 있습니다. 데이터 요소의 경우 변수 설정 작업을 트리거하는 이벤트는 중요하지 않습니다. 규칙을 트리거하는 이벤트는 Dynamic Viewer와 관련이 없을 수 있습니다. 예를 들어 코어 확장에서 웹 페이지를 선택합니다. 그러나 직접 인수 참조를 사용할 때는 규칙을 트리거하는 이벤트가 참조하는 이벤트 인수에 해당하는지 확인하는 것이 중요합니다.

For example, referencing `%event.detail.dm.LOAD.asset%` returns the correct asset name if the Rule is triggered by the **[!UICONTROL LOAD]** event of the Dynamic Media Viewer extension. However, it returns an empty value for any other event.

다음 표에는 Dynamic Media 뷰어 이벤트와 지원되는 인수가 나열되어 있습니다.

<table>
 <tbody>
  <tr>
   <td>뷰어 이벤트 이름</td>
   <td>인수 참조</td>
  </tr>
  <tr>
   <td><code>COMMON</code></td>
   <td><code>%event.detail.dm.objID%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.compClass%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.instName%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.timeStamp%</code></td>
  </tr>
  <tr>
   <td><code>BANNER</code><br /> </td>
   <td><code>%event.detail.dm.BANNER.asset%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.label%</code></td>
  </tr>
  <tr>
   <td><code>HREF</code></td>
   <td><code>%event.detail.dm.HREF.rollover%</code></td>
  </tr>
  <tr>
   <td><code>ITEM</code></td>
   <td><code>%event.detail.dm.ITEM.rollover%</code></td>
  </tr>
  <tr>
   <td><code>LOAD</code></td>
   <td><code>%event.detail.dm.LOAD.applicationname%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.asset%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.company%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.sdkversion%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewertype%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewerversion%</code></td>
  </tr>
  <tr>
   <td><code>METADATA</code></td>
   <td><code>%event.detail.dm.METADATA.length%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.METADATA.type%</code></td>
  </tr>
  <tr>
   <td><code>MILESTONE</code></td>
   <td><code>%event.detail.dm.MILESTONE.milestone%</code></td>
  </tr>
  <tr>
   <td><code>PAGE</code></td>
   <td><code>%event.detail.dm.PAGE.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.PAGE.label%</code></td>
  </tr>
  <tr>
   <td><code>PAUSE</code></td>
   <td><code>%event.detail.dm.PAUSE.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>PLAY</code></td>
   <td><code>%event.detail.dm.PLAY.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SPIN</code></td>
   <td><code>%event.detail.dm.SPIN.framenumber%</code></td>
  </tr>
  <tr>
   <td><code>STOP</code></td>
   <td><code>%event.detail.dm.STOP.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SWAP</code></td>
   <td><code>%event.detail.dm.SWAP.asset%</code></td>
  </tr>
  <tr>
   <td><code>SWATCH</code></td>
   <td><code>%event.detail.dm.SWATCH.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.SWATCH.label%</code></td>
  </tr>
  <tr>
   <td><code>TARG</code></td>
   <td><code>%event.detail.dm.TARG.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.TARG.label%</code></td>
  </tr>
  <tr>
   <td><code>ZOOM</code></td>
   <td><code>%event.detail.dm.ZOOM.scale%</code></td>
  </tr>
 </tbody>
</table>

## 모든 통합 부분 구성 {#configuring-all-the-integration-pieces}

**시작하기 전에**

Adobe에서는 이 섹션 전에 모든 설명서를 충분히 검토하여 전체 통합을 이해할 것을 권장합니다.

이 섹션에서는 Dynamic Media 뷰어를 오디오 및 비디오용 Adobe Analytics 및 Adobe Analytics과 통합하는 데 필요한 구성 단계에 대해 설명합니다. Experience Platform Tags에서 다른 용도로 Dynamic Media 뷰어 확장을 사용할 수 있지만 이러한 시나리오는 이 설명서에서 다루지 않습니다.

다음 Adobe 제품을 사용하여 통합을 구성합니다.

* Adobe Analytics - 추적 변수 및 보고서를 구성하는 데 사용됩니다.
* Experience Platform 태그 - 속성, 하나 이상의 규칙 및 하나 이상의 데이터 요소를 정의하여 뷰어 추적을 활성화하는 데 사용됩니다.

또한 이 통합 솔루션을 Experience Manager Sites과 함께 사용하는 경우 다음 구성도 수행해야 합니다.

* [!DNL Adobe Developer Console] - Experience Platform 태그에 대한 통합이 만들어졌습니다.
* Experience Manager 작성자 노드 - IMS 구성 및 Experience Platform Tags 클라우드 구성

구성의 일부로, Adobe Experience Cloud에서 Adobe Analytics 및 Experience Platform 태그가 이미 활성화되어 있는 회사에 액세스할 수 있어야 합니다.

## 통합을 위한 Adobe Analytics 구성 {#configuring-adobe-analytics-for-the-integration}

Adobe Analytics을 구성하면 통합에 대해 다음과 같이 설정됩니다.

* 보고서 세트 가 배치되어 선택되어 있습니다.
* Analytics 변수는 추적 데이터를 받는 데 사용할 수 있습니다.
* Adobe Analytics에서 수집된 데이터를 보는 데 보고서를 사용할 수 있습니다.

[Analytics 구현 가이드](https://experienceleague.adobe.com/en/docs/analytics/implementation/home)도 참조하세요.

**통합을 위해 Adobe Analytics을 구성하려면:**

1. Experience Cloud [홈 페이지](https://experience.adobe.com/#/home)에서 Adobe Analytics에 액세스해 보세요. 메뉴 표시줄에서 페이지의 오른쪽 상단 근처에 있는 **[!UICONTROL 솔루션]** 아이콘(세 개의 점 테이블)을 선택한 다음 **[!UICONTROL Analytics]**&#x200B;을 선택합니다.

   ![2019-07-22_18-08-47](assets/2019-07-22_18-08-47.png)

   이제 보고서 세트를 선택합니다.

### 보고서 세트 선택 {#selecting-a-report-suite}

1. Near the upper-right corner of the Adobe Analytics page, to the right of the **[!UICONTROL Search Reports]** field, select the correct report suite from the drop-down list. If there are multiple report suites available and you are unsure which one to use, contact your Adobe Analytics administrator who can help you select which report suite to use.

   아래 스크린샷에서 사용자가 *DynamicMediaViewersExtensionDoc*(이)라는 보고서 세트를 만들고 드롭다운 목록에서 선택했습니다. 보고서 세트 이름은 예제 이름일 뿐입니다. 최종적으로 선택하는 보고서 세트의 이름은 사용자가 결정합니다.

   사용 가능한 보고서 세트가 없는 경우 구성을 계속 진행하려면 먼저 사용자 또는 Adobe Analytics 관리자가 보고서 세트를 만들어야 합니다.

   [보고서 및 보고서 세트](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/report-suites-admin) 및 [보고서 세트 만들기](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite)를 참조하십시오.

   Adobe Analytics의 보고서 세트는 **[!UICONTROL 관리자]** > **[!UICONTROL 보고서 세트]**&#x200B;에서 관리됩니다.

   ![2019-07-22_18-09-49](assets/2019-07-22_18-09-49.png)

   이제 Adobe Analytics 변수를 설정합니다.

### Adobe Analytics 변수 설정 {#setting-up-adobe-analytics-variables}

1. 웹 페이지에서 Dynamic Media 뷰어 동작을 추적하는 데 사용할 Adobe Analytics 변수를 하나 이상 지정합니다.

   Adobe Analytics에서 지원하는 모든 유형의 변수를 사용할 수 있습니다. 변수 유형(예: 사용자 지정 트래픽 [props], 전환 [eVar])에 대한 결정은 Analytics 구현의 특정 요구 사항에 의해 결정됩니다.

   [prop 및 eVar 개요](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/evar#vars)를 참조하십시오.

   이 설명서에서는 웹 페이지에서 작업이 발생한 후 몇 분 안에 Analytics 보고서에서 사용할 수 있으므로 사용자 지정 트래픽(props) 변수만 사용됩니다.

   새 사용자 지정 트래픽 변수를 활성화하려면 Adobe Analytics의 도구 모음에서 **[!UICONTROL 관리자]** > **[!UICONTROL 보고서 세트]**(으)로 이동하십시오.

1. **[!UICONTROL 보고서 세트 관리자]** 페이지에서 올바른 보고서를 선택한 다음 도구 모음에서 **[!UICONTROL 설정 편집]** > **[!UICONTROL 트래픽]** > **[!UICONTROL 트래픽 변수]**(으)로 이동합니다.
1. 사용되지 않는 변수를 선택하고 설명적인 이름(**[!UICONTROL Viewer 자산(prop 30)]**)을 지정한 다음 Enabled 열에서 콤보 상자를 &quot;Enabled&quot;로 변경합니다.

   다음 스크린샷은 뷰어에서 사용하는 자산 이름을 추적하기 위한 사용자 지정 트래픽 변수(**[!UICONTROL prop30]**)의 예입니다.

   ![image2019-6-26_23-6-59](assets/image2019-6-26_23-6-59.png)

1. 변수 목록의 맨 아래에서 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

### 보고서 설정 {#setting-up-a-report}

1. 일반적으로 Adobe Analytics에서 보고서 설정은 특정 프로젝트 요구 사항에 의해 결정됩니다. 따라서 세부 보고서 설정은 이 통합의 범위를 벗어납니다.

   하지만 [Adobe Analytics 변수 설정](#setting-up-adobe-analytics-variables)에서 사용자 지정 트래픽 변수를 설정한 후에는 Adobe Analytics에서 사용자 지정 트래픽 보고서를 자동으로 사용할 수 있다는 사실을 아는 것만으로도 충분합니다.

   예를 들어 **[!UICONTROL 뷰어 자산(prop 30)]** 변수에 대한 보고서는 **[!UICONTROL 사용자 지정 트래픽]** > **[!UICONTROL 사용자 지정 트래픽 21-30]** > **[!UICONTROL 뷰어 자산(prop 30)]**&#x200B;의 보고서 메뉴에서 사용할 수 있습니다.

   Visiting this report right after **[!UICONTROL Viewer asset (prop 30)]** creation shows no data; that is expected at this point in the integration.

   ![image2019-6-26_23-12-49](assets/image2019-6-26_23-12-49.png)

## 통합을 위한 Experience Platform 태그 구성 {#configuring-adobe-launch-for-the-integration}

Experience Platform 태그를 구성하면 통합에 대해 다음과 같이 설정됩니다.

* 모든 구성을 함께 유지하기 위한 새 속성 만들기.
* 확장 설치 및 설정. 속성에 설치된 모든 확장의 클라이언트측 코드가 라이브러리에 함께 컴파일됩니다. 이 라이브러리는 나중에 웹 페이지에서 사용됩니다.
* 데이터 요소 및 규칙 구성 이 구성은 Dynamic Media 뷰어에서 캡처할 데이터, 추적 논리를 트리거할 시기 및 Adobe Analytics에서 뷰어의 데이터를 보낼 위치를 정의합니다.
* 라이브러리 게시.

**통합을 위해 Experience Platform 태그를 구성하려면:**

1. Experience Cloud [홈 페이지](https://experience.adobe.com/#/home)에서 Experience Platform 태그에 액세스해 보십시오. 메뉴 표시줄에서 페이지의 오른쪽 상단 근처에 있는 **[!UICONTROL 솔루션]** 아이콘(세 개의 점 테이블)을 선택한 다음 **[!UICONTROL 태그]**&#x200B;를 선택합니다.

   ![image2019-7-8_15-38-44](assets/image2019-7-8_15-38-44.png)

### Experience Platform Tags에서 속성 만들기 {#creating-a-property-in-adobe-launch}

Experience Platform Tags의 속성은 모든 설정을 함께 유지하는 명명된 구성입니다. 구성 설정 라이브러리가 생성되고 다른 환경 수준(개발, 스테이징 및 프로덕션)에 게시됩니다.

[태그 속성 만들기](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/configure-tags)도 참조하세요.

1. Experience Platform 태그에서 **[!UICONTROL 새 속성]**&#x200B;을 선택합니다.
1. In the **[!UICONTROL Create Property]** dialog box, in the **[!UICONTROL Name]** field, type a descriptive name, such as the title of your website. 예, `DynamicMediaViewersProp.`
1. **[!UICONTROL 도메인]** 필드에 웹 사이트의 도메인을 입력합니다.
1. **[!UICONTROL 고급 옵션]** 드롭다운에서 사용할 확장(이 경우 **[!UICONTROL Dynamic Media 뷰어]**)이 아직 릴리스되지 않은 경우 *확장 개발에 대한 구성(나중에 수정할 수 없음)*&#x200B;을 사용하도록 설정하십시오.

   ![image2019-7-8_16-3-47](assets/image2019-7-8_16-3-47.png)

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

   새로 만든 속성을 선택한 다음 *확장 설치 및 설정*&#x200B;을 진행합니다.

### 확장 설치 및 설정 {#installing-and-setup-of-extensions}

Experience Platform 태그에서 사용 가능한 모든 확장은 **[!UICONTROL 확장]** > **[!UICONTROL 카탈로그]** 아래에 나열됩니다.

확장을 설치하려면 **[!UICONTROL 설치]**&#x200B;를 선택합니다. 필요한 경우 1회 확장 구성을 수행한 다음 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

필요한 경우 다음 확장을 설치 및 구성해야 합니다.

* (필수) *Experience Cloud ID 서비스* 확장.

추가 구성이 필요하지 않습니다. 제안된 값에 동의하십시오. 완료되면 **[!UICONTROL 저장]**&#x200B;을 선택하십시오.

[Adobe Experience Cloud ID 서비스 확장](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/id-service/overview)을 참조하십시오.

* (필수) *Adobe Analytics* 확장

이 확장을 구성하려면 Adobe Analytics의 **[!UICONTROL 관리자]** > **[!UICONTROL 보고서 세트]**, **[!UICONTROL 보고서 세트 ID]** 열 헤더에서 보고서 세트 ID를 찾아야 합니다.

데모용으로만 **[!UICONTROL DynamicMediaViewersExtensionDoc]** 보고서 세트의 보고서 세트 ID가 다음 스크린샷에서 사용됩니다. 이 ID는 [이전 보고서 세트 선택](#selecting-a-report-suite)에서 만들고 사용했습니다.

![image2019-7-8_16-45-34](assets/image2019-7-8_16-45-34.png)

On the Install Extension page, enter the Report Suite ID in the **[!UICONTROL Development Report Suites]** field, the **[!UICONTROL Staging Report Suites]** field, and the **[!UICONTROL Production Report Suites]** field.

![image2019-7-8_16-47-40](assets/image2019-7-8_16-47-40.png)

*비디오 추적을 사용할 경우에만 다음 항목을 구성하십시오.*

**[!UICONTROL 확장 설치]** 페이지에서 **[!UICONTROL 일반]**&#x200B;을 확장한 다음 추적 서버를 지정하십시오. 추적 서버는 템플릿 `<trackingNamespace>.sc.omtrdc.net`을(를) 따릅니다. 여기서 `<trackingNamespace>`은(는) 프로비저닝 전자 메일에서 가져온 정보입니다.

**[!UICONTROL 저장]**&#x200B;을 선택합니다.

[Adobe Analytics 확장](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/analytics/overview)을 참조하세요.

* (선택 사항, 비디오 추적이 필요한 경우에만 필수) *오디오 및 비디오용 Adobe Media Analytics* 확장

추적 서버 필드를 입력합니다. *오디오 및 비디오용 Adobe Media Analytics* 확장 프로그램의 추적 서버가 Adobe Analytics에 사용되는 추적 서버와 다릅니다. `<trackingNamespace>.hb.omtrdc.net` 템플릿을 따릅니다. 여기서 `<trackingNamespace>`은(는) 프로비저닝 전자 메일의 정보입니다.

다른 모든 필드는 선택 사항입니다.

[Adobe Media Analytics for Audio 및 Video 확장](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/media-analytics/overview)을(를) 참조하십시오.

* (필수) *Dynamic Media 뷰어* 확장

Select **[!UICONTROL enable Adobe Analytics for Video]** to enable (turn on) Video Heartbeat tracking.

이 문서를 작성하면 *Dynamic Media 뷰어* 확장 기능은 개발을 위해 Experience Platform 태그 속성을 만든 경우에만 사용할 수 있습니다.

[Experience Platform 태그에서 속성 만들기](#creating-a-property-in-adobe-launch)를 참조하십시오.

확장을 설치하고 설정하면 최소한 다음 5개의 확장(비디오를 추적하지 않는 경우 4개)이 Extensions > Installed 영역에 나열됩니다.

![image2019-7-22_12-7-36](assets/image2019-7-22_12-7-36.png)

### 데이터 요소 및 규칙 설정 {#setting-up-data-elements-and-rules}

Experience Platform 태그에서 Dynamic Media 뷰어를 추적하는 데 필요한 데이터 요소 및 규칙을 만듭니다.

Experience Platform 태그를 사용한 추적에 대한 개요는 [통합에서 데이터 및 이벤트 추적 작동 방식](#how-data-and-event-tracking-works-in-the-integration)을 참조하십시오.

뷰어 로드 시 에셋 이름을 추적하는 방법을 보여 주는 Experience Platform Tags의 샘플 구성에 대해서는 [샘플 구성](#sample-configuration)을 참조하십시오.

확장 기능에 대한 자세한 내용은 [Dynamic Media 뷰어 확장 구성](#configuring-the-dynamic-media-viewers-extension)을 참조하십시오.

### 라이브러리 게시 {#publishing-a-library}

Experience Platform 태그 구성(설정된 속성, 확장, 규칙 및 데이터 요소 포함)을 변경하려면 이러한 변경 내용을 *게시*&#x200B;해야 합니다. Experience Platform 태그의 게시는 속성 구성 아래의 게시 탭에서 수행됩니다.

Experience Platform 태그에는 잠재적으로 여러 개발 환경, 하나의 스테이징 환경 및 하나의 프로덕션 환경이 있을 수 있습니다. 기본적으로 Experience Manager의 Experience Platform 태그 클라우드 구성은 Experience Manager 작성자 노드를 Experience Platform 태그의 스테이지 환경으로 지정합니다. Experience Manager Publish 노드는 Experience Platform 태그의 프로덕션 환경을 가리킵니다. 즉, 기본 Experience Manager 설정을 사용하여 Experience Platform 태그 라이브러리를 스테이징 환경에 게시해야 합니다. 이렇게 하면 Experience Manager 작성자에서 사용할 수 있습니다. 그런 다음 Experience Manager 게시에서 사용할 수 있도록 프로덕션 환경에 게시할 수 있습니다.

Experience Platform 태그 환경에 대한 자세한 내용은 [환경](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/environments/environments)을 참조하십시오.

라이브러리 게시에는 다음 두 단계가 포함됩니다.

* 필요한 모든 변경 사항(새 변경 사항 및 업데이트)을 라이브러리에 포함하여 새 라이브러리를 추가하고 빌드합니다.
* 다른 환경 수준(개발에서 스테이징 및 프로덕션으로)을 통해 라이브러리 위로 이동합니다.

#### 새 라이브러리 추가 및 빌드 {#adding-and-building-a-new-library}

1. Experience Platform Tags에서 처음 게시 탭을 열면 라이브러리 목록이 비어 있습니다.

   왼쪽 열에서 **[!UICONTROL 새 라이브러리 추가]**&#x200B;를 선택합니다.

   ![image2019-7-15_14-43-17](assets/image2019-7-15_14-43-17.png)

1. 새 라이브러리 만들기 페이지의 **[!UICONTROL 이름]** 필드에 새 라이브러리를 설명하는 이름을 입력합니다. 예:

   *DynamicMediaViewersLib*

   환경 드롭다운 목록에서 환경 레벨을 선택합니다. 처음에는 개발 수준만 선택할 수 있습니다. 페이지의 왼쪽 아래에서 **[!UICONTROL 변경된 모든 리소스 추가]**&#x200B;를 선택합니다.

   ![image2019-7-15_14-49-41](assets/image2019-7-15_14-49-41.png)

1. 페이지의 오른쪽 상단 모서리에서 **[!UICONTROL 개발을 위한 저장 및 빌드]**&#x200B;를 선택합니다.

   몇 분 후에 라이브러리가 만들어지고 사용할 준비가 되었습니다.

   ![image2019-7-15_15-3-34](assets/image2019-7-15_15-3-34.png)

   >[!NOTE]
   >
   >다음에 Experience Platform 태그 구성을 변경할 때 **[!UICONTROL 속성]** 구성 아래의 **[!UICONTROL 게시]** 탭으로 이동한 다음 이전에 만든 라이브러리를 선택합니다.
   >
   >
   >라이브러리 게시 화면에서 **[!UICONTROL 변경된 모든 리소스 추가]**&#x200B;를 선택한 다음 **[!UICONTROL 개발을 위한 저장 및 빌드]**&#x200B;를 선택합니다.

#### 환경 수준에서 라이브러리 위로 이동 {#moving-a-library-up-through-environment-levels}

1. 새 라이브러리가 추가되면 개발 환경에서 찾을 수 있습니다. 스테이징 환경 수준(제출됨 열에 해당)으로 이동하려면 라이브러리의 드롭다운 메뉴에서 **[!UICONTROL 승인을 위해 제출]**&#x200B;을 선택합니다.

   ![image2019-7-15_15-52-37](assets/image2019-7-15_15-52-37.png)

1. 확인 대화 상자에서 **[!UICONTROL 제출]**&#x200B;을 선택합니다.

   라이브러리가 Submitted 열로 이동한 후 라이브러리의 드롭다운 메뉴에서 **[!UICONTROL 스테이징을 위한 빌드]**&#x200B;를 선택합니다.

   ![image2019-7-15_15-54-37](assets/image2019-7-15_15-54-37.png)

1. 스테이징 환경에서 프로덕션 환경(게시됨 열)으로 라이브러리를 이동하려면 유사한 프로세스를 따릅니다.

   먼저 드롭다운 메뉴에서 **[!UICONTROL 게시 승인]**&#x200B;을 선택합니다.

   ![image2019-7-15_16-7-39](assets/image2019-7-15_16-7-39.png)

1. 드롭다운 메뉴에서 **[!UICONTROL Build &amp; Publish to Production]**&#x200B;을 선택합니다.

   ![image2019-7-15_16-8-9](assets/image2019-7-15_16-8-9.png)

   Experience Platform Tags의 게시 프로세스에 대한 자세한 내용은 [게시](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/overview)를 참조하십시오.

## 통합을 위한 Adobe Experience Manager 구성 {#configuring-adobe-experience-manager-for-the-integration}

사전 요구 사항:

* Experience Manager은 작성자 및 게시 인스턴스를 모두 실행합니다.
* Experience Manager 작성자 노드가 Dynamic Media - Scene7 실행 모드(dynamicmedia_s7)로 설정됨
* Experience Manager Sites에서 Dynamic Media WCM 구성 요소를 사용할 수 있습니다.

Experience Manager 구성은 다음 두 가지 주요 단계로 구성됩니다.

* Experience Manager IMS 구성
* Experience Platform 태그 클라우드 구성

### Experience Manager IMS 구성 {#configuring-aem-ims}

1. Experience Manager 작성자에서 **[!UICONTROL 도구]** 아이콘(hammer)을 선택한 다음 **[!UICONTROL 보안]** > **[!UICONTROL Adobe IMS 구성]**&#x200B;으로 이동합니다.

   ![2019-07-25_11-52-58](assets/2019-07-25_11-52-58.png)

1. Adobe IMC 구성 페이지의 왼쪽 상단 모서리에서 **[!UICONTROL 만들기]**&#x200B;를 선택합니다.
1. **[!UICONTROL Adobe IMS 기술 계정 구성]** 페이지의 **[!UICONTROL 클라우드 솔루션]** 드롭다운 목록에서 **[!UICONTROL Experience Platform 태그]**&#x200B;를 선택합니다.
1. **[!UICONTROL 새 인증서 만들기]**&#x200B;를 사용하도록 설정한 다음 텍스트 필드에 인증서에 대한 의미 있는 값을 입력합니다. 예: *AdobeLaunchIMSCert*. **[!UICONTROL 인증서 만들기]**&#x200B;를 선택합니다.

   다음 정보 메시지가 표시됩니다.

   *올바른 액세스 토큰을 검색하려면 새 인증서의 공개 키가 Adobe Developer Console의 기술 계정에 추가됩니다.*

   정보 대화 상자를 닫으려면 **[!UICONTROL 확인]**&#x200B;을 선택합니다.

   ![2019-07-25_12-09-24](assets/2019-07-25_12-09-24.png)

1. 공개 키 파일(&#42;.crt)을 로컬 시스템에 다운로드하려면 **[!UICONTROL 공개 키 다운로드]**&#x200B;를 선택하십시오.

   >[!NOTE]
   >
   >이 시점에서 ***열어 두기*** **[!UICONTROL Adobe IMS 기술 계정 구성]** 페이지를 엽니다. ***페이지를 닫지 않음*** 및 ***다음을 선택하지 않음***. 이 페이지의 뒷부분에서 다시 시작하려 합니다.

   ![2019-07-25_12-52-24](assets/2019-07-25_12-52-24.png)

1. 새 브라우저 탭에서 [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/integrations)&#x200B;(으)로 이동합니다.

1. 오른쪽 상단 근처에 있는 **[!UICONTROL Adobe Developer Console 통합]** 페이지에서 **[!UICONTROL 새 통합]**&#x200B;을 선택합니다.
1. **[!UICONTROL 새 통합 만들기]** 대화 상자에서 **[!UICONTROL API 액세스]** 라디오 단추가 선택되어 있는지 확인한 다음 **[!UICONTROL 계속]**&#x200B;을 선택합니다.

   ![2019-07-25_13-04-20](assets/2019-07-25_13-04-20.png)

1. 두 번째 **[!UICONTROL 새 통합 만들기]** 페이지에서 **[!UICONTROL Experience Platform 태그 API]** 라디오 단추를 활성화(켜기)하십시오. 페이지의 오른쪽 아래 모서리에서 **[!UICONTROL 계속]**&#x200B;을 선택합니다.

   ![2019-07-25_13-13-54](assets/2019-07-25_13-13-54.png)

1. 세 번째 **[!UICONTROL 새 통합 만들기]** 페이지에서 다음을 수행합니다.

   * **[!UICONTROL 이름]** 필드에 수사적 이름을 입력합니다. 예: *DynamicMediaViewersIO*.

   * **[!UICONTROL 설명]** 필드에 통합에 대한 설명을 입력합니다.

   * **[!UICONTROL 공개 키 인증서]** 영역에서 이전에 이 단계에서 다운로드한 공개 키 파일(&#42;.crt)을 업로드합니다.

   * **[!UICONTROL Experience Platform Tags API에 대한 역할 선택]** 제목에서 **[!UICONTROL 관리자]**&#x200B;를 선택합니다.

   * **[!UICONTROL Experience Platform Tags API에 대한 제품 프로필을 하나 이상 선택]** 제목에서 **[!UICONTROL Tags - &lt;your_company_name>]**&#x200B;이라는 제품 프로필을 선택합니다.

   ![2019-07-25_13-49-18](assets/2019-07-25_13-49-18.png)

1. **[!UICONTROL 통합 만들기]**&#x200B;를 선택합니다.
1. **[!UICONTROL 통합 생성됨]** 페이지에서 **[!UICONTROL 통합 세부 정보로 계속]**&#x200B;을 선택합니다.

   ![2019-07-25_14-16-33](assets/2019-07-25_14-16-33.png)

1. 다음과 유사한 통합 세부 정보 페이지 ****&#x200B;이(가) 나타납니다.

   >[!NOTE]
   >
   >***Leave open this Integration details page***. **[!UICONTROL 개요]** 및 **[!UICONTROL JWT]** 탭의 다양한 정보가 잠시 후 필요합니다.

   ![2019-07-25_14-35-30](assets/2019-07-25_14-35-30.png)

   통합 세부 정보 페이지.

1. Return to the **[!UICONTROL Adobe IMS Technical Account Configuration]** page that you left open previously. 페이지의 오른쪽 상단 모서리에서 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 **[!UICONTROL Adobe IMS 기술 계정 구성]** 창에서 **[!UICONTROL 계정]** 페이지를 엽니다.

   (이전에 페이지를 닫은 경우 Experience Manager 작성자로 돌아간 다음 **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL Adobe IMS 구성]**&#x200B;으로 이동합니다. **[!UICONTROL 만들기]**&#x200B;를 선택합니다. **[!UICONTROL 클라우드 솔루션]** 드롭다운 목록에서 **[!UICONTROL Experience Platform 태그]**&#x200B;를 선택합니다. **[!UICONTROL 인증서]** 드롭다운 목록에서 이전에 만든 인증서의 이름을 선택합니다.

   ![2019-07-25_20-57-50](assets/2019-07-25_20-57-50.png)

   Adobe IMS 기술 계정 구성 - 인증서 페이지.

1. **[!UICONTROL 계정]** 페이지에는 이전 단계의 통합 세부 정보 페이지에서 정보를 사용하여 입력해야 하는 5개의 필드가 있습니다.

   ![2019-07-25_20-42-45](assets/2019-07-25_20-42-45.png)

   Adobe IMS 기술 계정 구성 - 계정 페이지.

1. **[!UICONTROL 계정]** 페이지에서 다음 필드를 입력하십시오.

   * **[!UICONTROL 제목]** - 설명 계정 제목을 입력합니다.
   * **[!UICONTROL 인증 서버]** - 이전에 열었던 통합 세부 정보 페이지로 돌아갑니다. **[!UICONTROL JWT]** 탭을 선택합니다. 아래 강조 표시된 대로 경로 없이 서버 이름을 복사합니다.

   **[!UICONTROL 계정]** 페이지로 돌아가서 해당 필드에 이름을 붙여 넣으십시오.
예: `https://ims-na1.adobelogin.com/`
(서버 이름은 예제일 뿐입니다)

   ![2019-07-25_15-01-53](assets/2019-07-25_15-01-53.png)

   통합 세부 정보 페이지 - JWT 탭

1. **[!UICONTROL API Key]** - Return to the Integration details page. **[!UICONTROL 개요]** 탭을 선택한 다음 **[!UICONTROL API 키(클라이언트 ID)]** 필드 오른쪽에서 **[!UICONTROL 복사]**&#x200B;를 선택합니다.

   Return to the **[!UICONTROL Account]** page, then paste the key into the respective field.

   ![2019-07-25_14-35-333](assets/2019-07-25_14-35-333.png)

   통합 세부 정보 페이지.

1. **[!UICONTROL 클라이언트 암호]** - 통합 세부 정보 페이지로 돌아갑니다. **[!UICONTROL 개요]** 탭에서 **[!UICONTROL 클라이언트 암호 검색]**&#x200B;을 선택합니다. **[!UICONTROL 클라이언트 암호]** 필드 오른쪽에서 **[!UICONTROL 복사]**&#x200B;를 선택합니다.

   Return to the **[!UICONTROL Account]** page, then paste the key into the respective field.

1. **[!UICONTROL 페이로드]** - 통합 세부 정보 페이지로 돌아갑니다. **[!UICONTROL JWT]** 탭의 JWT 페이로드 필드에서 전체 JSON 개체 코드를 복사합니다.

   Return to the **[!UICONTROL Account]** page, then paste the code into the respective field.

   ![2019-07-25_21-59-12](assets/2019-07-25_21-59-12.png)

   통합 세부 정보 페이지 - JWT 탭

   모든 필드가 채워진 [계정] 페이지는 다음과 유사합니다.

   ![2019-07-25_22-08-30](assets/2019-07-25_22-08-30.png)

1. **[!UICONTROL 계정]** 페이지의 오른쪽 상단 모서리에서 **[!UICONTROL 만들기]**&#x200B;를 선택합니다.

   Experience Manager IMS가 구성되면 **[!UICONTROL Adobe IMS 구성]**&#x200B;에 새 IMSAccount가 나열됩니다.

   ![image2019-7-15_14-17-54](assets/image2019-7-15_14-17-54.png)

## 통합을 위해 Experience Platform Tags Cloud 구성 {#configuring-adobe-launch-cloud-for-the-integration}

1. Experience Manager 작성자의 왼쪽 상단 모서리에서 **[!UICONTROL 도구]** 아이콘(hammer)을 선택한 다음 **[!UICONTROL 클라우드 서비스]** > **[!UICONTROL Experience Platform 태그 구성]**(으)로 이동합니다.

   ![2019-07-26_12-10-38](assets/2019-07-26_12-10-38.png)

1. **[!UICONTROL Experience Platform 태그 구성]** 페이지의 왼쪽 패널에서 Experience Platform 태그 구성을 적용할 Experience Manager 사이트를 선택합니다.

   샘플 목적으로만 아래 스크린샷에서 **`We.Retail`** 사이트가 선택됩니다.

   ![2019-07-26_12-20-06](assets/2019-07-26_12-20-06.png)

1. 페이지의 왼쪽 상단 모서리 근처에서 **[!UICONTROL 만들기]**&#x200B;를 선택합니다.
1. **[!UICONTROL Experience Platform 태그 구성 만들기]** 창의 **[!UICONTROL 일반]** 페이지(1/3페이지)에서 다음 필드를 채우십시오.

   * **[!UICONTROL 제목]** - 설명 구성 제목을 입력합니다. 예: `We.Retail Tags cloud configuration`

   * **[!UICONTROL 연결된 Adobe IMS 구성]** - [Experience Manager IMS 구성](#configuring-aem-ims)에서 이전에 만든 IMS 구성을 선택합니다.

   * **[!UICONTROL 회사]** - **[!UICONTROL 회사]** 드롭다운 목록에서 Experience Cloud 회사를 선택합니다. 목록이 자동으로 채워집니다.

   * **[!UICONTROL 속성]** - 속성 드롭다운 목록에서 이전에 만든 Experience Platform Tags 속성을 선택합니다. 목록이 자동으로 채워집니다.

   모든 필드를 완료한 후에는 **[!UICONTROL 일반]** 페이지가 다음과 비슷하게 표시됩니다.

   ![image2019-7-15_14-34-23](assets/image2019-7-15_14-34-23.png)

1. 왼쪽 상단 모서리 근처에서 **[!UICONTROL 다음]**&#x200B;을 선택합니다.
1. **[!UICONTROL Experience Platform 태그 구성 만들기]** 창의 **[!UICONTROL 스테이징]** 페이지(2/3페이지)에서 다음 필드를 채우십시오.

   **[!UICONTROL 라이브러리 URI]**(Uniform Resource Identifier) 필드에서 Experience Platform Tags 라이브러리의 스테이징 버전 위치를 확인합니다. Experience Manager이 이 필드를 자동으로 채웁니다.

   샘플 목적으로만, 이 단계에서는 Adobe CDN에 배포된 Experience Platform Tags 라이브러리를 사용합니다.

   >[!NOTE]
   >
   >자동으로 채워진 라이브러리 URI(Uniform Resource Identifier)의 형식이 잘못되지 않았는지 확인합니다. 필요한 경우 URI가 프로토콜 관련 URI를 나타내도록 수정합니다. 즉, 이중 슬래시에서 시작됩니다.
   >
   >
   >예: `//assets.adobetm.com/launch-xxxx`.

   **[!UICONTROL 스테이징]** 페이지는 다음과 비슷하게 표시됩니다. **[!UICONTROL 보관]** 및 **[!UICONTROL 라이브러리를 비동기적으로 로드]** 옵션이 ***설정되지 않음*** 설정됨:

   ![image2019-7-15_15-21-8](assets/image2019-7-15_15-21-8.png)

1. 오른쪽 상단 모서리에서 **[!UICONTROL 다음]**&#x200B;을(를) 선택합니다.
1. 필요한 경우 **[!UICONTROL Experience Platform 태그 구성 만들기]** 창의 **[!UICONTROL 프로덕션]** 페이지(3/3페이지)에서 이전 **[!UICONTROL 스테이징]** 페이지에서 수행한 방법과 유사하게 자동으로 채워진 프로덕션 URI를 수정합니다.
1. 오른쪽 상단 모서리에서 **[!UICONTROL 만들기]**&#x200B;를 선택합니다.

   이제 새 Experience Platform 태그 클라우드 구성이 만들어지고 웹 사이트 옆에 다음 예제와 유사하게 나열됩니다.

1. 새 Experience Platform 태그 클라우드 구성을 선택합니다(구성 제목을 선택하면 왼쪽에 확인 표시가 표시됨). 도구 모음에서 **[!UICONTROL 게시]**&#x200B;를 선택합니다.

   ![image2019-7-15_15-47-6](assets/image2019-7-15_15-47-6.png)

현재 Experience Manager 작성자는 Experience Platform 태그와 Dynamic Media Viewer 통합을 지원하지 않습니다.

그러나 Experience Manager 게시 노드에서 지원됩니다. Experience Platform Tags Cloud Configuration의 기본 설정을 사용하여 Experience Manager 게시 노드는 Experience Platform Tags의 프로덕션 환경을 사용합니다. 따라서 테스트 중에 매번 Experience Platform 태그 라이브러리 업데이트를 개발에서 프로덕션 환경까지 푸시해야 합니다.

이 제한을 해결할 수 있습니다. 위의 Experience Manager 게시 노드에 대한 Experience Platform Tags Cloud 구성에서 플랫폼 태그 라이브러리의 개발 또는 스테이징 URL을 지정합니다. 이렇게 하면 Experience Manager 게시 노드가 Experience Platform 태그 라이브러리의 개발 또는 스테이징 버전을 사용하게 됩니다.

Experience Platform Tags Cloud 구성 설정에 대한 자세한 내용은 [을(를) 통해 Experience Manager과 Experience Platform 태그 통합 [!DNL Adobe Developer Console]](https://experienceleague.adobe.com/en/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview)을(를) 참조하십시오.
