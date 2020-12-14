---
title: Adobe Analytics에 대한 비디오 추적 구성
seo-title: Adobe Analytics에 대한 비디오 추적 구성
description: SiteCatalyst에 대한 비디오 추적 구성에 대해 알아봅니다.
seo-description: SiteCatalyst에 대한 비디오 추적 구성에 대해 알아봅니다.
uuid: 5a862f05-abfa-42a2-ad40-4c1c32f1bd75
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: a18ddac1-9e4c-4857-9cb3-4d5eeb8dd9ec
docset: aem65
translation-type: tm+mt
source-git-commit: 90c99e527a40bb663d4f32d8746b46cf34a2319f
workflow-type: tm+mt
source-wordcount: '1766'
ht-degree: 1%

---


# Adobe Analytics{#configuring-video-tracking-for-adobe-analytics}에 대한 비디오 추적 구성

비디오 이벤트를 추적하는 데 사용할 수 있는 방법에는 몇 가지가 있으며, 이중 2가지는 이전 버전의 Adobe Analytics에 대한 레거시 옵션입니다. 이전 옵션은 다음과 같습니다.이전 이정표 및 이전 초.

>[!NOTE]
>
>계속하기 전에 AEM 내에 **재생 가능한 비디오**&#x200B;가 업로드되었는지 확인하십시오.
>
>비디오가 페이지에서 재생되도록 하려면 AEM에서 비디오 파일을 트랜스코딩하는 방법에 대한 자세한 내용은 **[이 자습서](/help/sites-authoring/default-components-foundation.md#video)**&#x200B;를 참조하십시오.

각 메서드를 사용하여 비디오 추적에 대한 프레임워크를 설정하려면 다음 절차를 따르십시오.

>[!NOTE]
>
>새 구현의 경우 **비디오 추적에 기존 옵션을 사용하지 않는 것이 좋습니다.** 대신 **마일스톤** 메서드를 사용하십시오.

## 일반적인 단계 {#common-steps}

1. 사이드 킥에서 **비디오 구성 요소**&#x200B;를 드래그하고 재생 가능한 **비디오를 구성 요소에 대한 자산**&#x200B;으로 추가하여 웹 페이지를 설정합니다.

1. [Adobe Analytics 구성 및 프레임워크를 만듭니다](/help/sites-administering/adobeanalytics.md).

   * 다음 섹션의 예에서는 구성에 **my-sc-configuration**, 프레임워크에 대해 **videofw** 이름을 사용합니다.

1. 프레임워크 페이지에서 RSID를 선택하고 사용을 모두 로 설정합니다. ([https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html](https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html))
1. 사이드 킥의 일반 구성 요소 카테고리에서 비디오 구성 요소를 프레임워크로 드래그합니다.
1. 추적 방법 선택:

   * [마일스톤](/help/sites-administering/adobeanalytics.md)
   * [비레거시 마일스톤](/help/sites-administering/adobeanalytics.md)
   * [이전 이정표](/help/sites-administering/adobeanalytics.md)
   * [이전 초](/help/sites-administering/adobeanalytics.md)

1. 추적 방법을 선택하면 CQ 변수 목록이 그에 따라 변경됩니다. 구성 요소를 추가로 구성하고 CQ 변수를 Adobe Analytics 속성에 매핑하는 방법에 대한 자세한 내용은 다음 섹션을 참조하십시오.

## 마일스톤 {#milestones}

Milestones 메서드는 비디오에 대한 대부분의 정보를 추적하며, 사용자 지정이 가능하며 구성하기가 쉽습니다.

마일스톤 방법을 사용하려면 시간 기반 트랙 오프셋을 지정하여 마일스톤을 정의합니다. 비디오 재생이 이정표를 통과하면 페이지에서 Adobe Analytics을 호출하여 이벤트를 추적합니다. 정의한 각 이정표에 대해 구성 요소는 Adobe Analytics 속성에 매핑할 수 있는 CQ 변수를 만듭니다. 이러한 CQ 변수의 이름은 다음 형식을 사용합니다.

```shell
eventdata.events.milestoneXX
```

XX 접미사는 이정표를 정의하는 트랙 오프셋입니다. 예를 들어 4, 8, 16, 20 및 28초로 트랙 오프셋을 지정하면 다음 CQ 변수가 생성됩니다.

* `eventdata.events.milestone4`
* `eventdata.events.milestone8`
* `eventdata.events.milestone16`
* `eventdata.events.milestone20`
* `eventdata.events.milestone28`

다음 표에서는 마일스톤 메서드에 제공된 기본 CQ 변수에 대해 설명합니다.

<table>
 <tbody>
  <tr>
   <th>CQ 변수</th>
   <th>Adobe Analytics 속성</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>이 변수에 매핑되는 변수에는 DAM에 설정된 경우 비디오의 <strong>사용자 친화적인</strong> 이름(<strong>제목</strong>)이 포함됩니다.이 값이 설정되지 않으면 비디오의 <strong>파일 이름</strong>이 대신 전송됩니다. 비디오 재생 시작 시 한 번만 전송됨.</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>이 변수에 매핑되는 변수에는 파일 이름이 포함됩니다. eventdata.events.a.media.view와 함께 전송된 것만 </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>이 변수에 매핑되는 변수에는 서버의 파일 경로가 포함됩니다. eventdata.events.a.media.view와 함께 전송된 것만 </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>세그먼트 마일스톤이 전달될 때마다 전송 </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>이정표가 트리거될 때마다 전송되는 시간(초)도 이 이벤트와 함께 전송됩니다. 예: eventX=21<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>비디오 보기를 초기화할 때 전송됨</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>비디오 재생이 완료되면 전송<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestoneX </td>
   <td>지정된 이정표가 통과되면 X는 이정표가 트리거되는 두 번째 시점을(<br />에서) 나타냅니다. </td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>모든 이정표에 전송;는 Adobe Analytics 호출에서 pev3로 표시되며, 일반적으로 "video"<br />으로 전송됩니다. </td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>eventdata.videoName과 정확히 일치합니다. </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>2:O:4-8과 같이 본 세그먼트에 대한 정보를 포함합니다. </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>DAM에서 편집할 비디오를 열고 **제목** 메타데이터 필드를 원하는 이름으로 설정하여 비디오의 **사용자 친화적인** 이름을 설정할 수 있습니다.

1. 추적 방법으로 마일스톤을 선택한 후 [오프셋 추적] 상자에 추적 오프셋의 쉼표로 구분된 목록을 초 단위로 입력합니다. 예를 들어 다음 값은 비디오가 시작된 후 4, 8, 16, 20 및 28초로 마일스톤을 정의합니다.

   ```xml
   4,8,16,20,24
   ```

   오프셋 값은 0보다 큰 정수여야 합니다. 기본값은 `10,25,50,75`입니다.

1. CQ 변수를 Adobe Analytics 속성에 매핑하려면 구성 요소의 CQ 변수 옆에 있는 ContentFinder에서 Adobe Analytics 속성을 드래그합니다.

   매핑 최적화에 대한 자세한 내용은 Adobe Analytics](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html) 안내서의 [비디오 측정 설명서를 참조하십시오.

1. [페이지에 ](/help/sites-administering/adobeanalytics.md) 프레임워크를 추가합니다.
1. **미리 보기 모드**&#x200B;에서 설정을 테스트하려면 비디오를 재생하여 Adobe Analytics 호출을 트리거하십시오.

이후 4,8,16,20 및 24의 추적 오프셋을 사용하여 마일스톤 추적에 적용되는 Adobe Analytics 추적 데이터 예제와 CQ 변수에 대한 다음 매핑을 참조하십시오.

<table>
 <tbody>
  <tr>
   <th>CQ 변수</th>
   <th>Adobe Analytics 속성</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>prop2</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>prop3 </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>prop4</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>event1</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>event2<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>event3</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>event4<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestone4</td>
   <td>event10</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone8</td>
   <td>event11</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone16</td>
   <td>event12</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone20</td>
   <td>event13</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone24</td>
   <td>event14</td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>eVar3</td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>eVar1, prop1 </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>eVar2</td>
  </tr>
 </tbody>
</table>

이 예에서 비디오 구성 요소는 프레임워크 페이지에 다음과 같이 표시됩니다.

![video1](assets/video1.png)

>[!NOTE]
>
>Adobe Analytics에 대한 호출을 보려면 DigitalPulse Debugger 또는 Fiddler와 같은 적절한 도구를 사용합니다.

제공된 예제를 사용하는 Adobe Analytics 호출은 DigitalPulse Debugger에서 볼 때 다음과 같아야 합니다.

![chlimage_1-128](assets/chlimage_1-128.png)

*다음 값을 포함하는 Adobe Analytics에&#x200B;**처음**호출됩니다.*

* *prop1 및 eVar1 for events.a.media.name,*
* *prop2-4, contentType(비디오) 및 세그먼트(1:O:1-4)를 포함하는 eVar2 및 eVar3과 함께 사용*
* *event3. events.a.media.view에 매핑되었습니다.*

![chlimage_1-129](assets/chlimage_1-129.png)

*Adobe Analytics에&#x200B;**대해 세**번째 호출입니다.*

* *prop1 및 eVar1에는 a.media.name;*
* *event1 - 세그먼트를 보았으므로*
* *재생된 시간과 함께 전송된 event2 = 4*
* *event11이 전송되어 eventdata.events.milestone8에 도달했습니다.*
* *prop2를 4로 보내지 않음(eventdata.events.a.media.view가 트리거되지 않았으므로)*

## 비레거시 마일스톤 {#non-legacy-milestones}

비레거시 마일스톤 메서드는 이정표가 트랙 길이의 백분율을 사용하여 정의되어 있다는 점을 제외하고 마일스톤 메서드와 유사합니다. 일반적인 것은 다음과 같습니다.

* 비디오 재생이 이정표를 통과하면 페이지에서 Adobe Analytics을 호출하여 이벤트를 추적합니다.
* Adobe Analytics 속성을 사용하여 매핑하도록 정의된 CQ 변수](#cqvars)의 [정적 집합.
* 정의한 각 이정표에 대해 구성 요소는 Adobe Analytics 속성에 매핑할 수 있는 CQ 변수를 만듭니다.

이러한 CQ 변수의 이름은 다음 형식을 사용합니다.

XX 접미사는 이정표를 정의하는 트랙 길이의 백분율입니다. 예를 들어 백분율을 10, 25, 50 및 75로 지정하면 다음 CQ 변수가 생성됩니다.

* `eventdata.events.milestone10`
* `eventdata.events.milestone25`
* `eventdata.events.milestone50`
* `eventdata.events.milestone75`

```shell
eventdata.events.milestoneXX
```

1. 추적 방법으로 비레거시 이정표를 선택한 후 [오프셋 추적] 상자에 트랙 길이의 백분율을 쉼표로 구분된 목록을 입력합니다. 예를 들어 다음 기본값은 트랙 길이의 10, 25, 50 및 75%에서 마일스톤을 정의합니다.

   ```xml
   10,25,50,75
   ```

   오프셋 값은 0보다 큰 정수여야 합니다.

1. CQ 변수를 Adobe Analytics 속성에 매핑하려면 구성 요소의 CQ 변수 옆에 있는 ContentFinder에서 Adobe Analytics 속성을 드래그합니다.

   매핑 최적화에 대한 자세한 내용은 Adobe Analytics](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html) 안내서의 [비디오 측정 설명서를 참조하십시오.

1. [페이지에 ](/help/sites-administering/adobeanalytics.md) 프레임워크를 추가합니다.
1. **미리 보기 모드**&#x200B;에서 설정을 테스트하려면 비디오를 재생하여 Adobe Analytics 호출을 트리거하십시오.

## 이전 마일스톤 {#legacy-milestones}

이 메서드는 *추적 오프셋* 필드에 지정된 마일스톤이 비디오 내의 설정 지점 대신 백분율이라는 점에서 Milestones 메서드와 유사합니다.

>[!NOTE]
>
>추적 오프셋 필드는 1과 100 사이의 정수를 포함하는 쉼표로 구분된 목록만 허용합니다.

1. 트랙 오프셋을 설정합니다.

   * e.g.10,50,75,100

   또한 Adobe Analytics으로 전송된 정보는 사용자 정의 가능하지 않습니다.매핑에 사용할 수 있는 변수는 3개뿐입니다.

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>이 변수에 매핑되는 변수에는 DAM에 설정된 경우 비디오의 <strong>사용자 친화적인</strong> 이름(<strong>제목</strong>)이 포함됩니다.제목을 설정하지 않으면 비디오의 <strong>파일 이름</strong>이 대신 전송됩니다. 비디오 재생 시작 시 한 번만 전송됨<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>이 변수에 매핑되는 변수에는 파일 이름이 포함됩니다. 비디오 재생 시작 시 한 번만 전송됨.</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>이 변수에 매핑되는 변수에는 서버의 파일 경로가 포함됩니다. 비디오 재생 시작 시 한 번만 전송됨.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>DAM에서 편집할 비디오를 열고 **제목** 메타데이터 필드를 원하는 이름으로 설정하여 비디오의 **사용자 친화적인** 이름을 설정할 수 있습니다. 완료되면 변경 내용을 저장해야 합니다.

1. 이러한 변수를 prop 1-3에 매핑

   호출의 **나머지 관련 정보**&#x200B;는 **a4/>pev3**&#x200B;이라는 이름의 한&#x200B;**변수로 전송됩니다.**

   **DigitalPulse** Debugger에서 볼 때 제공된 예제를 사용하여 Adobe Analytics에 대한 샘플 호출은 다음과 같습니다.

   ![마일스톤1](assets/lmilestones1.png)

   *호출에서&#x200B;**전송된**pev3 변수에는 다음 정보가 포함됩니다.*

   * *이름*  - 비디오 파일의 이름(*film.avi*)

   * *길이*  - 비디오 파일의 길이(초)(*100*)

   * *플레이어 이름*  - 비디오 파일을 재생하는 데 사용되는 비디오 플레이어(*HTML5 비디오*)

   * *총 재생*  시간(초) - 비디오가 재생된 총 시간(*25*)

   * *시작 타임스탬프*  - 비디오 재생이 시작된 시기를 식별하는 타임스탬프(*1331035567*)

   * *재생 세션*  - 재생 세션의 세부 정보입니다. 이 필드는 사용자가 비디오와 상호 작용한 방법을 나타냅니다. 여기에는 비디오 재생을 시작한 위치, 비디오 슬라이더를 사용하여 비디오를 진행했는지 여부, 비디오 재생을 중단한 위치(*L10E24S58L58 - 비디오 재생 시간(초)과 같은 데이터가 포함될 수 있습니다. L10 섹션 25를 건너뛰고 초 단위로 건너뛰었습니다. 48*)

## 이전 초 {#legacy-seconds}

이전 초** 메서드를 사용할 때 Adobe Analytics 호출은 N번째 초마다 트리거되며 여기서 N은 추적 오프셋 필드에 지정됩니다.

1. 트랙 오프셋을 원하는 시간(초)으로 설정합니다.

   * 예: 6
   >[!NOTE]
   >
   >추적 오프셋 필드에는 0보다 큰 정수만 사용할 수 있습니다.

   Adobe Analytics으로 전송된 정보는 사용자 지정이 덜 가능합니다. 매핑에는 3개의 변수만 사용할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>이 변수에 매핑되는 변수에는 DAM에 설정된 경우 비디오의 <strong>사용자 친화적인</strong> 이름(<strong>제목</strong>)이 포함됩니다.제목을 설정하지 않으면 비디오의 <strong>파일 이름</strong>이 대신 전송됩니다. 비디오 재생 시작 시 한 번만 전송됨<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>이 변수에 매핑되는 변수에는 파일 이름이 포함됩니다. 비디오 재생 시작 시 한 번만 전송됨.</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>이 변수에 매핑되는 변수에는 서버의 파일 경로가 포함됩니다. 비디오 재생 시작 시 한 번만 전송됨.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>DAM에서 편집할 비디오를 열고 **제목** 메타데이터 필드를 원하는 이름으로 설정하여 비디오의 **사용자 친화적인** 이름을 설정할 수 있습니다. 완료되면 변경 내용을 저장해야 합니다.

1. 이러한 변수를 prop1, prop2 및 prop3에 매핑

   호출에서 나머지 관련 정보&#x200B;**는** a4/>pev3 **이라는 이름의 하나** 변수로 전송됩니다.****

   제공된 예제를 사용하는 Adobe Analytics 호출은 DigitalPulse Debugger에서 볼 때 다음과 같아야 합니다.

   ![lseconds](assets/lseconds.png)

   *호출은 위의 레거시 마일스톤 호출과 유사합니다.](/help/sites-administering/adobeanalytics.md)**에 제공된 pev3**[에 대한 정보를 참조하십시오.*

**이 자습서에 사용된 참조:**

[0] [https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html)
