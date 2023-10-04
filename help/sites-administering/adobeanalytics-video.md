---
title: Adobe Analytics를 위한 비디오 추적 구성
description: SiteCatalyst을 위한 비디오 추적 구성에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 5d51f898-b6d1-40ac-bdbf-127cda1dc777
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 2%

---

# Adobe Analytics를 위한 비디오 추적 구성{#configuring-video-tracking-for-adobe-analytics}

비디오 이벤트를 추적하는 데 사용할 수 있는 몇 가지 방법이 있는데, 그 중 두 가지 방법은 이전 버전의 Adobe Analytics에 대한 레거시 옵션입니다. 이러한 레거시 옵션은 레거시 이정표 및 레거시 초입니다.

>[!NOTE]
>
>계속하기 전에 다음을 확인하십시오. **재생 가능한 비디오** AEM 내에서 업로드되었습니다.
>
>비디오가 페이지에서 재생되는지 확인하려면 다음을 참조하십시오. **[이 자습서](/help/sites-authoring/default-components-foundation.md#video)** AEM에서 비디오 파일을 변환하는 방법에 대한 정보입니다.

다음 절차에 따라 각 메서드를 사용하여 비디오 추적을 위한 프레임워크를 설정하십시오.

>[!NOTE]
>
>새로운 구현의 경우 다음 작업을 수행하는 것이 좋습니다. **사용하지 않음** 비디오 추적에 대한 레거시 옵션입니다. 다음을 사용하십시오. **마일스톤** 메서드를 사용하십시오.

## 일반적인 단계 {#common-steps}

1. 을(를) 끌어 웹 페이지 설정 **비디오 구성 요소** 사이드 킥 및 재생 가능한 추가 **에셋으로서의 비디오** 구성 요소용

1. [Adobe Analytics 구성 및 프레임워크 만들기](/help/sites-administering/adobeanalytics.md).

   * 다음에 나오는 섹션의 예제에서는 다음 이름을 사용합니다 **my-sc-configuration** 구성 및 **videofw** 프레임워크에 사용됩니다.

1. 프레임워크 페이지에서 RSID를 선택하고 사용을 모두로 설정합니다. ([https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html](https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html))
1. Sidekick의 일반 구성 요소 카테고리에서 비디오 구성 요소를 프레임워크로 드래그합니다.
1. 추적 방법 선택:

   * [마일스톤](/help/sites-administering/adobeanalytics.md)
   * [비레거시 마일스톤](/help/sites-administering/adobeanalytics.md)
   * [이전 마일스톤](/help/sites-administering/adobeanalytics.md)
   * [레거시 초](/help/sites-administering/adobeanalytics.md)

1. 추적 메서드를 선택하면 CQ 변수 목록이 그에 따라 변경됩니다. 구성 요소를 추가로 구성하고 CQ 변수를 Adobe Analytics 속성에 매핑하는 방법에 대한 자세한 내용은 다음 섹션을 참조하십시오.

## 마일스톤 {#milestones}

마일스톤 메서드는 비디오에 대한 대부분의 정보를 추적하고 사용자 지정이 가능하며 구성이 쉽습니다.

이정표 방법을 사용하려면 시간 기반 추적 오프셋을 지정하여 이정표를 정의합니다. 비디오 재생이 이정표를 전달하면 페이지가 Adobe Analytics을 호출하여 이벤트를 추적합니다. 정의하는 각 이정표에 대해 구성 요소는 Adobe Analytics 속성에 매핑할 수 있는 CQ 변수를 만듭니다. 이러한 CQ 변수의 이름은 다음 형식을 사용합니다.

```shell
eventdata.events.milestoneXX
```

XX 접미사는 이정표를 정의하는 추적 오프셋입니다. 예를 들어 4, 8, 16, 20 및 28초의 추적 오프셋을 지정하면 다음 CQ 변수가 생성됩니다.

* `eventdata.events.milestone4`
* `eventdata.events.milestone8`
* `eventdata.events.milestone16`
* `eventdata.events.milestone20`
* `eventdata.events.milestone28`

다음 표에서는 이정표 메서드에 제공되는 기본 CQ 변수에 대해 설명합니다.

<table>
 <tbody>
  <tr>
   <th>CQ 변수</th>
   <th>Adobe Analytics 속성</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>여기에 매핑된 변수에는 <strong>사용자에게 친숙한</strong> 이름(<strong>제목</strong>DAM에 설정된 경우 비디오의 )입니다. 설정되지 않은 경우 비디오는 <strong>파일 이름</strong> 이(가) 대신 전송됩니다. 비디오 재생 시작 시 한 번만 전송됩니다.</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>여기에 매핑된 변수에는 파일 이름이 포함됩니다. eventdata.events.a.media.view와 함께 전송된 경우에만 </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>여기에 매핑된 변수에는 서버의 파일 경로가 포함됩니다. eventdata.events.a.media.view와 함께 전송된 경우에만 </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>세그먼트 이정표가 전달될 때마다 전송됩니다. </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>이정표가 트리거될 때마다 사용자가 해당 세그먼트를 시청하는 데 걸린 시간(초)도 이 이벤트와 함께 전송됩니다. 예: eventX=21<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>비디오 보기 초기화 시 전송됨</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>비디오 재생이 완료되면 전송됩니다.<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestoneX </td>
   <td>지정된 이정표가 전달되면 X는 이정표가 트리거되는 초를 나타냅니다.<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>모든 이정표에 전송됩니다. Adobe Analytics 호출에서 pev3으로 표시되며, 일반적으로 "비디오"로 전송됩니다.<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>eventdata.videoName과 정확히 일치 </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>본 세그먼트에 대한 정보를 포함합니다(예: 2).:O:4-8 </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>비디오를 설정할 수 있습니다 **사용자에게 친숙한** dam에서 편집할 비디오를 열고 를 설정하여 이름 지정 **제목** 메타데이터 필드를 원하는 이름으로 바꿉니다.

1. 추적 방법으로 이정표를 선택한 후 [추적 오프셋] 상자에 쉼표로 구분된 추적 오프셋 목록을 초 단위로 입력합니다. 예를 들어 다음 값은 비디오가 시작된 후 4, 8, 16, 20 및 28초에 이정표를 정의합니다.

   ```xml
   4,8,16,20,24
   ```

   오프셋 값은 0보다 큰 정수여야 합니다. 기본값은 `10,25,50,75`입니다.

1. CQ 변수를 Adobe Analytics 속성에 매핑하려면 ContentFinder에서 Adobe Analytics 속성을 구성 요소의 CQ 변수 옆으로 드래그합니다.

   매핑 최적화에 대한 자세한 내용은 [Adobe Analytics에서 비디오 측정](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html) 가이드.

1. [프레임워크 추가](/help/sites-administering/adobeanalytics.md) 페이지를 표시합니다.
1. 에서 설정을 테스트하려면 **미리 보기 모드**, 비디오를 재생하여 Adobe Analytics 호출을 트리거합니다.

다음에 나오는 Adobe Analytics 추적 데이터 예는 4,8,16,20 및 24의 추적 오프셋과 CQ 변수에 대한 다음 매핑을 사용한 이정표 추적에 적용됩니다.

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
>Adobe Analytics에 대한 호출을 보려면 DigitalPulse Debugger 또는 Fiddler와 같은 적절한 도구를 사용하십시오.

제공된 예를 사용하여 Adobe Analytics에 대한 호출은 DigitalPulse Debugger에서 볼 때 다음과 같이 표시되어야 합니다.

![chlimage_1-128](assets/chlimage_1-128.png)

*다음 은&#x200B;**첫 번째 호출**다음 값이 포함된 Adobe Analytics으로 변경됨:*

* *eventdata.a.media.name의 prop1 및 eVar1,*
* *contentType(비디오) 및 세그먼트(1)가 포함된 eVar2 및 eVar3과 함께 prop2-4:O:1-4)*
* *eventdata.events.a.media.view에 매핑된 event3*

![chlimage_1-129](assets/chlimage_1-129.png)

*다음 은&#x200B;**세 번째 호출**Adobe Analytics:*

* *prop1 및 eVar1에 a.media.name;이 포함되어 있습니다.*
* *세그먼트를 보았으므로 event1*
* *재생된 시간 = 4와 함께 전송된 event2*
* *eventdata.events.milestone8에 도달했으므로 event11이 전송되었습니다.*
* *eventdata.events.a.media.view가 트리거되지 않았으므로 prop2에서 4까지는 전송되지 않습니다.*

## 비 레거시 마일스톤 {#non-legacy-milestones}

비레거시 이정표 방법은 이정표가 트랙 길이의 백분율로 정의된다는 점을 제외하면 이정표 방법과 유사합니다. 공통점은 다음과 같습니다.

* 비디오 재생이 이정표를 전달하면 페이지가 Adobe Analytics을 호출하여 이벤트를 추적합니다.
* 다음 [정적 CQ 변수 집합](#cqvars) Adobe Analytics 속성을 사용한 매핑에 대해 정의됩니다.
* 정의하는 각 이정표에 대해 구성 요소는 Adobe Analytics 속성에 매핑할 수 있는 CQ 변수를 만듭니다.

이러한 CQ 변수의 이름은 다음 형식을 사용합니다.

XX 접미사는 이정표를 정의하는 추적 길이의 백분율입니다. 예를 들어 10, 25, 50 및 75의 백분율을 지정하면 다음 CQ 변수가 생성됩니다.

* `eventdata.events.milestone10`
* `eventdata.events.milestone25`
* `eventdata.events.milestone50`
* `eventdata.events.milestone75`

```shell
eventdata.events.milestoneXX
```

1. 추적 방법으로 비 레거시 이정표를 선택한 후 [추적 오프셋] 상자에 쉼표로 구분된 추적 길이 백분율 목록을 입력합니다. 예를 들어 다음 기본값은 트랙 길이의 10, 25, 50 및 75%에서 이정표를 정의합니다.

   ```xml
   10,25,50,75
   ```

   오프셋 값은 0보다 큰 정수여야 합니다.

1. CQ 변수를 Adobe Analytics 속성에 매핑하려면 ContentFinder에서 Adobe Analytics 속성을 구성 요소의 CQ 변수 옆으로 드래그합니다.

   매핑 최적화에 대한 자세한 내용은 [Adobe Analytics에서 비디오 측정](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html) 가이드.

1. [프레임워크 추가](/help/sites-administering/adobeanalytics.md) 페이지를 표시합니다.
1. 에서 설정을 테스트하려면 **미리 보기 모드**, 비디오를 재생하여 Adobe Analytics 호출을 트리거합니다.

## 이전 마일스톤 {#legacy-milestones}

이 메서드는 Milestones 메서드와 유사하지만 *추적 오프셋* 필드는 비디오 내에서 설정된 포인트 대신 백분율입니다.

>[!NOTE]
>
>추적 오프셋 필드는 1과 100 사이의 정수를 포함하는 쉼표로 구분된 목록만 허용합니다.

1. 트랙 오프셋을 설정합니다.

   * (예: 10,50,75,100)

   또한 Adobe Analytics으로 전송된 정보는 사용자 지정이 줄어듭니다. 매핑에 사용할 수 있는 변수는 3개뿐입니다.

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>여기에 매핑된 변수에는 <strong>사용자에게 친숙한</strong> 이름(<strong>제목</strong>DAM에 설정된 경우 비디오의 )이고, 제목 이 설정되지 않은 경우 비디오의 <strong>파일 이름</strong> 이(가) 대신 전송됩니다. 비디오 재생 시작 시 한 번만 전송됩니다.<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>여기에 매핑된 변수에는 파일 이름이 포함됩니다. 비디오 재생 시작 시 한 번만 전송됩니다.</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>여기에 매핑된 변수에는 서버의 파일 경로가 포함됩니다. 비디오 재생 시작 시 한 번만 전송됩니다.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>비디오를 설정할 수 있습니다 **사용자에게 친숙한** dam에서 편집할 비디오를 열고 를 설정하여 이름 지정 **제목** 메타데이터 필드를 원하는 이름으로 바꿉니다. 완료되면 변경 사항을 저장해야 합니다.

1. 이러한 변수를 prop 1~3에 매핑

   다음 **기타 관련 정보** 호출이에서 (으)로 전송됩니다. **1** 이름이 인 변수 **pev3**.

   **샘플 호출** 제공된 예제를 사용하는 Adobe Analytics의 경우 DigitalPulse Debugger에서 볼 때 다음과 같이 표시되어야 합니다.

   ![lmilestones1](assets/lmilestones1.png)

   *다음&#x200B;**pev3**호출에서 전송된 변수에는 다음 정보가 포함됩니다.*

   * *이름* - 비디오 파일 이름(*film.avi*)

   * *Length* - 비디오 파일의 길이(초 단위)(*10*)

   * *플레이어 이름* - 비디오 파일을 재생하는 데 사용되는 비디오 플레이어(*HTML5 비디오*)

   * *총 재생 시간(초)* - 비디오가 재생된 총 시간(초)(*25*)

   * *타임스탬프 시작* - 비디오 재생이 시작된 시기를 식별하는 타임스탬프(*1331035567*)

   * *재생 세션* - 재생 세션의 세부 정보. 이 필드는 사용자가 비디오와 상호 작용하는 방법을 나타냅니다. 여기에는 비디오 재생을 시작한 위치, 비디오 슬라이더를 사용하여 비디오를 진행했는지 여부, 비디오 재생을 중지한 위치 등의 데이터가 포함될 수 있습니다(*L10E24S58L58 - 비디오가 초당 중지되었습니다. 섹션 L10 중 25개를 건너뛰고 초 단위로 건너뜁니다. 48*)

## 이전(초) {#legacy-seconds}

** 레거시 초** 메서드를 사용하는 경우 Adobe Analytics 호출은 N초마다 트리거되며, 여기서 N은 추적 오프셋 필드에 지정됩니다.

1. 트랙 오프셋을 초 단위로 설정합니다.

   * 예, 6

   >[!NOTE]
   >
   >추적 오프셋 필드는 0보다 큰 정수만 허용합니다

   Adobe Analytics으로 전송되는 정보의 맞춤화가 줄어듭니다. 매핑에 사용할 수 있는 변수는 3개뿐입니다.

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>여기에 매핑된 변수에는 <strong>사용자에게 친숙한</strong> 이름(<strong>제목</strong>DAM에 설정된 경우 비디오의 )이고, 제목 이 설정되지 않은 경우 비디오의 <strong>파일 이름</strong> 이(가) 대신 전송됩니다. 비디오 재생 시작 시 한 번만 전송됩니다.<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>여기에 매핑된 변수에는 파일 이름이 포함됩니다. 비디오 재생 시작 시 한 번만 전송됩니다.</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>여기에 매핑된 변수에는 서버의 파일 경로가 포함됩니다. 비디오 재생 시작 시 한 번만 전송됩니다.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>비디오를 설정할 수 있습니다 **사용자에게 친숙한** dam에서 편집할 비디오를 열고 를 설정하여 이름 지정 **제목** 메타데이터 필드를 원하는 이름으로 바꿉니다. 완료되면 변경 사항을 저장해야 합니다.

1. 이러한 변수를 prop1, prop2 및 prop3에 매핑

   다음 **기타 관련 정보** 호출이에서 concatenated로 전송됩니다. **1** 이름이 인 변수 **pev3**.

   제공된 예를 사용하여 Adobe Analytics에 대한 호출은 DigitalPulse Debugger에서 볼 때 다음과 같이 표시되어야 합니다.

   ![초](assets/lseconds.png)

   *이 호출은 위의 레거시 이정표 호출과 유사합니다. pev3에 대한 정보를 참조하십시오.**[거기에 제공된](/help/sites-administering/adobeanalytics.md)**.*

**이 자습서에 사용된 참조:**

[0] [https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html)
