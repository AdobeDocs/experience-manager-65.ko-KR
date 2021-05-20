---
title: 비디오 프로필
description: Dynamic Media에는 이미 사전 정의된 응용 비디오 인코딩 프로필이 포함되어 있습니다. 이 기본 프로필의 설정은 고객에게 최상의 보기 경험을 제공하도록 최적화되었습니다. 비디오에 스마트 자르기를 추가할 수도 있습니다.
uuid: 26a20984-db63-41e9-b16c-6e164b7596a0
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: 3b8791c8-2c97-42b7-b4a9-e1157ac9ea02
docset: aem65
feature: 비디오 프로필
role: Business Practitioner, Administrator
exl-id: b290fac2-7259-45d7-b733-70419d632b07
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3709'
ht-degree: 3%

---

# 비디오 프로필 {#video-profiles}

Dynamic Media에는 이미 사전 정의된 응용 비디오 인코딩 프로필이 포함되어 있습니다. 이 기본 프로필의 설정은 고객에게 최상의 보기 경험을 제공하도록 최적화되었습니다. 응용 비디오 인코딩 프로필을 사용하여 기본 소스 비디오를 인코딩할 때 재생 중에 비디오 플레이어는 고객의 인터넷 연결 속도에 따라 비디오 스트림의 품질을 자동으로 조정합니다. 이를 적응형 스트리밍이라고 합니다.

다음은 비디오의 품질을 결정하는 다른 요소입니다.

* **업로드된 기본 소스 비디오의 해상도**

   MP4 비디오가 240p 또는 360p와 같은 낮은 해상도로 기록된 경우 고화질로 스트리밍될 수 없습니다.

* **비디오 플레이어 크기**

   기본적으로 응용 비디오 인코딩 프로필의 &quot;너비&quot;는 &quot;자동&quot;으로 설정됩니다. 재생 중에 가장 좋은 품질은 플레이어의 크기에 따라 사용됩니다.

[비디오 인코딩에 대한 우수 사례](/help/assets/video.md#best-practices-for-encoding-videos)를 참조하십시오.

또한 [처리 프로필 사용을 위한 디지털 자산을 구성하는 우수 사례](/help/assets/organize-assets.md)를 참조하십시오.

>[!NOTE]
>
>비디오의 메타데이터 및 관련 비디오 이미지 축소판을 생성하려면 비디오 자체가 Dynamic Media의 인코딩 프로세스를 진행해야 합니다. AEM에서 **[!UICONTROL Dynamic Media 인코딩 비디오]** 워크플로우는 Dynamic Media을 활성화하고 비디오 클라우드 서비스를 설정한 경우 비디오를 인코딩합니다. 이 워크플로우는 워크플로우 프로세스 기록 및 실패 정보를 캡처합니다. [비디오 인코딩 및 YouTube 게시 진행률 모니터링](/help/assets/video.md#monitoring-video-encoding-and-youtube-publishing-progress)을 참조하십시오. Dynamic Media을 활성화하고 비디오 클라우드 서비스를 설정한 경우 비디오를 업로드할 때 **[!UICONTROL Dynamic Media 인코딩 비디오]** 워크플로우가 자동으로 적용됩니다. (Dynamic Media을 사용하지 않는 경우 **[!UICONTROL DAM 자산 업데이트]** 워크플로우가 적용됩니다.)
>
>메타데이터는 자산을 검색할 때 유용합니다. 미리 보기는 인코딩 중에 생성되는 정적 비디오 이미지입니다. 이 변수는 AEM 시스템에 필요하며 카드 보기, 검색 결과 보기 및 자산 목록 보기에서 비디오를 시각적으로 식별하는 데 도움이 되는 사용자 인터페이스에 사용됩니다. 인코딩된 비디오의 [표현물] 아이콘(페인터의 팔레트)을 탭하면 생성된 축소판을 볼 수 있습니다.

비디오 프로필 만들기를 완료하면 이 프로필을 폴더 또는 여러 폴더에 적용합니다. [폴더에 비디오 프로필 적용](#applying-a-video-profile-to-folders)을 참조하십시오.

다른 자산 유형에 대한 고급 처리 매개 변수를 정의하려면 [자산 처리 구성](/help/assets/config-dms7.md#configuring-asset-processing)을 참조하십시오.

메타데이터, 이미지 및 비디오 처리를 위한 프로필](processing-profiles.md)도 참조하십시오.[

## 응용 비디오 인코딩 사전 설정 {#adaptive-video-encoding-presets}

다음 표에서는 모바일 및 태블릿 장치, 데스크탑 컴퓨터로 응용 비디오 스트리밍을 위한 인코딩 프로필을 식별하는 우수 사례를 식별합니다. 모든 종횡비 비디오에 이러한 사전 설정을 사용할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>비디오 형식 코덱</strong></td>
   <td><strong>비디오 크기 - 너비(px)</strong></td>
   <td><strong>비디오 크기 - 높이(px)</strong></td>
   <td><strong>종횡비를 유지하시겠습니까?</strong></td>
   <td><strong>비디오 비트율(Kbps)</strong></td>
   <td><strong>비디오 프레임 속도(Fps)</strong></td>
   <td><strong>오디오 코덱</strong></td>
   <td><strong>오디오 비트율(Kbps)</strong></td>
  </tr>
  <tr>
   <td><p>MP4 H.264(mp4)</p> </td>
   <td>auto</td>
   <td>360</td>
   <td>예</td>
   <td>730년</td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128년</td>
  </tr>
  <tr>
   <td><p>MP4 H.264(mp4)</p> </td>
   <td>자동</td>
   <td>540년</td>
   <td>예</td>
   <td>2000<br /> </td>
   <td>30</td>
   <td>돌비 HE-AAC</td>
   <td>128년</td>
  </tr>
  <tr>
   <td><p>MP4 H.264(mp4)</p> </td>
   <td>자동</td>
   <td>720<br /> </td>
   <td>예</td>
   <td>3000<br /> </td>
   <td>30</td>
   <td>돌비 HE-AAC</td>
   <td>128년</td>
  </tr>
 </tbody>
</table>

## 비디오 프로필에서 스마트 자르기 사용 정보 {#about-smart-crop-video}

비디오 프로필에서 사용할 수 있는 선택적 기능인 비디오 스마트 자르기는 Adobe Sensei의 인공 지능 기능을 사용하여 크기와 상관없이 업로드한 모든 적응형 비디오 또는 점진적 비디오에서 초점을 자동으로 감지하고 자르는 도구입니다.

스마트 자르기에 지원되는 비디오 형식에는 MP4, MKV, MOV, AVI, FLV 및 WMV가 포함됩니다.

스마트 자르기에 대해 지원되는 최대 비디오 파일 크기는 다음 기준입니다.

* 5분 동안.
* 초당 30프레임(FPS)입니다.
* 300MB 파일 크기

Adobe Sensei은 현재 9,000프레임으로 제한됩니다. 즉, 30FPS로 5분 비디오에 FPS가 더 높으면 지원되는 최대 비디오 지속 시간이 줄어듭니다. 예를 들어 60FPS 비디오는 Adobe 센사이 및 스마트 자르기에서 지원하려면 2분 30초여야 합니다.

![비디오용 스마트 자르기](assets/smart-crop-video.png)

>[!IMPORTANT]
>
>비디오 스마트 자르기가 작동하려면 비디오 프로필에 하나 이상의 비디오 인코딩 사전 설정을 포함해야 합니다.

비디오에 스마트 자르기를 사용하려면 응용 또는 점진적 비디오 인코딩 프로필을 만듭니다. 프로필의 일부로 **[!UICONTROL 스마트 자르기 비율]** 도구를 사용하여 사전 정의된 종횡비를 선택합니다. 예를 들어 비디오 인코딩 사전 설정을 정의한 후 종횡비가 16x9이고 종횡비가 9x16인 &quot;모바일 세로&quot; 정의를 추가할 수 있습니다. 선택할 수 있는 기타 종횡비 또는 자르기 비율은 1x1, 4x3 및 4x5입니다.

![스마트 자르기로 비디오 인코딩 프로필 편집](assets/edit-smart-crop-video2.png)

사용자 인터페이스에서 슬라이더를 사용하여 비디오 프로필의 비디오 스마트 자르기를 켜거나 끕니다. **[!UICONTROL 스마트 자르기 비율]**

비디오 프로필을 만들고 저장한 후에 원하는 폴더에 적용할 수 있습니다.

[특정 폴더에 비디오 프로필 적용](#applying-video-profiles-to-specific-folders) 또는 [전체적으로 비디오 프로필 적용](#applying-a-video-profile-globally)을 참조하십시오.

[이미지용 스마트 자르기](image-profiles.md)도 참조하십시오.

## 적응형 스트리밍을 위한 비디오 프로필 만들기 {#creating-a-video-encoding-profile-for-adaptive-streaming}

Dynamic Media에는 이미 최고의 보기 환경에 최적화된 MP4 H.264-용 비디오 업로드 설정 그룹인 사전 정의된 응용 비디오 인코딩 프로필이 포함되어 있습니다. 비디오를 업로드할 때 이 프로필을 사용할 수 있습니다.

그러나 사전 정의된 이 프로필이 사용자의 요구 사항을 충족하지 못하는 경우 자체 응용 비디오 인코딩 프로필을 만들도록 선택할 수 있습니다. 응용 스트리밍에 대해 **[!UICONTROL 인코딩 설정을 사용하는 경우 프로필에 추가하는 모든 우수 사례 인코딩 사전 설정이 유효한지 확인하여 모든 비디오의 종횡비가 동일한지 확인합니다.]** 또한, 인코딩된 비디오는 스트리밍을 위한 멀티 비트율 세트로 처리된다.

비디오 인코딩 프로필을 만들면 대부분의 인코딩 옵션이 권장 기본 설정으로 미리 채워져 있는 것을 볼 수 있습니다. 그러나 권장 기본값 이외의 값을 선택하는 경우 재생 중 비디오 품질이 저하되고 다른 성능 문제가 발생할 수 있습니다.

따라서 프로필의 모든 MP4 H.264 비디오 인코딩 사전 설정에 대해 다음 값의 유효성을 검사하여 프로필의 개별 인코딩 사전 설정에서 동일한지 확인하여 적응형 스트리밍을 수행할 수 있습니다.

* 비디오 포맷 코덱을 - MP4 H.264(.mp4)
* 오디오 코덱
* 오디오 비트율
* 비율 유지
* 2개의 패스 인코딩
* 상수 비트율
* H264 프로필
* 오디오 샘플링 속도

값이 동일하지 않으면 프로파일을 그대로 계속 생성할 수 있습니다. 그러나 적응형 스트리밍은 불가능합니다. 대신, 사용자는 단일 비트율 스트리밍을 경험하게 됩니다. 프로필의 개별 인코딩 사전 설정에서 동일한 값을 사용하도록 인코딩 설정을 편집하는 것이 좋습니다. (응용 스트리밍을 위해 인코딩이 활성화된 경우 비디오 프로필/사전 설정 편집기는 응용 비디오 인코딩 설정의 패리티를 적용해야 합니다.)

또한 [점진적 스트리밍을 위한 비디오 인코딩 프로필 만들기](#creating-a-video-encoding-profile-for-progressive-streaming)를 참조하십시오.

또한 [비디오 인코딩에 대한 우수 사례](/help/assets/video.md#best-practices-for-encoding-videos)를 참조하십시오.

다른 자산 유형에 대한 고급 처리 매개 변수를 정의하려면 [자산 처리 구성](/help/assets/config-dms7.md#configuring-asset-processing)을 참조하십시오.

**적응형 스트리밍을 위한 비디오 프로필을 만들려면**,

1. AEM 로고를 탭하고 **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 비디오 프로필로 이동합니다.]**
1. **[!UICONTROL 만들기]**&#x200B;를 클릭하거나 탭하여 새 비디오 프로필을 추가합니다.

1. 프로필의 이름과 설명을 입력합니다.
1. 비디오 인코딩 사전 설정 만들기/편집 페이지에서 **[!UICONTROL 비디오 인코딩 사전 설정 추가를 누릅니다.]**
1. **[!UICONTROL 기본]** 탭에서 비디오 및 오디오 옵션을 설정합니다.
각 옵션 옆에 있는 정보 아이콘을 탭하여 선택한 비디오 형식 코덱에 따른 추가적인 설명 또는 권장 설정을 제공합니다.
1. 비디오 크기 제목 아래에서 **[!UICONTROL 비율 유지]**&#x200B;가 선택되어 있는지 확인합니다.
1. 비디오 프레임 크기 해상도를 픽셀 단위로 설정합니다. 소스 종횡비(폭과 높이 비율)에 맞게 자동으로 크기를 조절하려면 **[!UICONTROL 자동]** 값을 사용하십시오. 예를 들어, 자동 x 480 또는 640 x Auto가 있습니다.

1. 다음 중 하나를 수행하십시오.

   * **[!UICONTROL Width]** 필드에 **[!UICONTROL auto를 입력합니다.]** 높이  **** 필드에 값을 픽셀 단위로 입력합니다.

   * 비디오 크기를 시각화하는 데 도움이 되도록 **[!UICONTROL 높이]** 오른쪽에 있는 정보 아이콘(i)을 탭하여 크기 계산기 페이지를 엽니다. **[!UICONTROL 크기 계산기]**&#x200B;를 사용하여 원하는 비디오 차원(파란색 상자로 표시됨)을 설정합니다. 완료되면 오른쪽 위 모서리에서 **[!UICONTROL X]**&#x200B;을 탭합니다.

1. (선택 사항) **[!UICONTROL 고급]** 탭을 탭하고 **[!UICONTROL 기본값 사용]** 확인란이 선택되어 있는지 확인합니다(권장). 또는 고급 비디오 및 오디오 설정을 수정합니다.
1. 페이지의 오른쪽 위 모서리에서 **[!UICONTROL 저장]**&#x200B;을 눌러 사전 설정을 저장합니다.
1. 다음 중 하나를 수행하십시오.
   * 4-10단계를 반복하여 추가 인코딩 사전 설정을 만듭니다. (응용 비디오 스트리밍에는 둘 이상의 비디오 사전 설정이 필요합니다.)
   * 다음 단계로 진행합니다.

1. (선택 사항) 이 프로필이 적용될 비디오에 비디오 스마트 자르기를 추가하려면 다음을 수행하십시오.
   * 비디오 프로필 편집 페이지의 스마트 자르기 비율 머리글 오른쪽에 있는 **[!UICONTROL 새로 추가]**&#x200B;를 탭합니다.
   * 이름 필드에 쉽게 식별할 수 있는 자르기 비율의 이름을 입력합니다.
   * **[!UICONTROL 자르기 비율]** 드롭다운 목록에서 사용할 비율을 선택합니다.

1. 다음 중 하나를 수행하십시오.

   * 필요에 따라 새 자르기 비율을 계속 추가합니다.
   * 다음 단계로 진행합니다.

1. 페이지의 오른쪽 위 모서리에서 **[!UICONTROL 저장]**&#x200B;을 다시 눌러 프로필을 저장합니다.

이제 프로필이 포함된 폴더에 프로필을 적용할 수 있습니다. [폴더](#applying-a-video-profile-to-folders) 또는 [전체적으로 비디오 프로필 적용](#applying-a-video-profile-globally)을 참조하십시오.

## 점진적 스트리밍을 위한 비디오 프로필 만들기 {#creating-a-video-encoding-profile-for-progressive-streaming}

적응형 스트리밍에 대해 **[!UICONTROL 인코딩]** 옵션을 사용하지 않도록 선택하는 경우, 프로필에 추가하는 모든 인코딩 사전 설정이 단일 비트율 스트리밍 또는 점진적 비디오 전달을 위한 개별 비디오 표현물로 처리된다는 점에 유의하십시오. 또한 모든 비디오 표현물이 동일한 종횡비를 가지는지 확인할 수 있는 유효성 검사가 없습니다.

실행 중인 모드에 따라 지원되는 비디오 형식 코덱은 다음과 같습니다.

* Dynamic Media-Scene7 모드:H.264(.mp4)
* Dynamic Media-하이브리드 모드:H.264(.mp4), WebM

응용 스트리밍을 위한 비디오 인코딩 프로필 만들기](#creating-a-video-encoding-profile-for-adaptive-streaming)를 참조하십시오.[

또한 [비디오 인코딩에 대한 우수 사례](/help/assets/video.md#best-practices-for-encoding-videos)를 참조하십시오.

다른 자산 유형에 대한 고급 처리 매개 변수를 정의하려면 [자산 처리 구성](/help/assets/config-dms7.md#configuring-asset-processing)을 참조하십시오.

**점진적 스트리밍을 위한 비디오 프로필을 만들려면:**

1. AEM 로고를 탭하고 **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 비디오 프로필로 이동합니다.]**
1. **[!UICONTROL 만들기]**&#x200B;를 눌러 새 비디오 프로필을 추가합니다.
1. 프로필의 이름과 설명을 입력합니다.
1. 비디오 인코딩 사전 설정 만들기/편집 페이지에서 **[!UICONTROL 비디오 인코딩 사전 설정 추가를 누릅니다.]**
1. **[!UICONTROL 기본]** 탭에서 비디오 및 오디오 옵션을 설정합니다.
각 옵션 옆에 있는 정보 아이콘을 탭하여 선택한 비디오 형식 코덱에 따른 추가적인 설명 또는 권장 설정을 제공합니다.
1. (선택 사항) 비디오 크기 제목 아래에서 **[!UICONTROL 종횡비 유지를 선택 취소합니다.]**
1. 다음을 수행합니다.
   * **[!UICONTROL Width]** 필드에 **[!UICONTROL auto.]**&#x200B;를 입력합니다.
   * **[!UICONTROL 높이]** 필드에 값을 픽셀 단위로 입력합니다.
비디오 크기를 시각화하는 데 도움이 되도록 높이 정보 아이콘을 탭하여 **[!UICONTROL 크기 계산기]** 페이지를 엽니다. **[!UICONTROL 크기 계산기]** 페이지를 사용하여 원하는 비디오 차원(파란색 상자)을 추가로 설정합니다. 완료되면 대화 상자의 오른쪽 상단 모서리에서 **[!UICONTROL X.]**&#x200B;를 누릅니다
1. (선택 사항) 다음 중 하나를 수행합니다.

   * **[!UICONTROL 고급]** 탭을 탭하고 **[!UICONTROL 기본값 사용]** 확인란이 선택되어 있는지 확인합니다(권장).

   * **[!UICONTROL 기본값 사용]** 확인란을 선택 취소하고 원하는 비디오 설정과 오디오 설정을 지정합니다.
각 옵션 옆에 있는 정보 아이콘을 탭하여 선택한 비디오 형식 코덱에 따른 추가적인 설명 또는 권장 설정을 제공합니다.

1. 페이지의 오른쪽 위 모서리에서 **[!UICONTROL 저장]**&#x200B;을 눌러 사전 설정을 저장합니다.
1. 다음 중 하나를 수행하십시오.

   * 4-9단계를 반복하여 추가 인코딩 사전 설정을 만듭니다.
   * 다음 단계로 진행합니다.

1. (선택 사항) 이 프로필이 적용될 비디오에 비디오 스마트 자르기를 추가하려면 다음을 수행하십시오.

   * 비디오 프로필 편집 페이지의 스마트 자르기 비율 머리글 오른쪽에 있는 **[!UICONTROL 새로 추가]**&#x200B;를 탭합니다.
   * 이름 필드에 쉽게 식별할 수 있는 자르기 비율의 이름을 입력합니다.
   * **[!UICONTROL 자르기 비율]** 드롭다운 목록에서 사용할 비율을 선택합니다.

1. 다음 중 하나를 수행하십시오.

   * 필요에 따라 새 자르기 비율을 계속 추가합니다.
   * 다음 단계로 진행합니다.

1. 페이지의 오른쪽 위 모서리에서 **[!UICONTROL 저장]**&#x200B;을 눌러 프로필을 저장합니다.

이제 프로필이 포함된 폴더에 프로필을 적용할 수 있습니다. [폴더](#applying-a-video-profile-to-folders) 또는 [전체적으로 비디오 프로필 적용](#applying-a-video-profile-globally)을 참조하십시오.

## 사용자가 추가한 비디오 인코딩 매개 변수 사용 {#using-custom-added-video-encoding-parameters}

기존 비디오 인코딩 프로필을 편집하여 AEM에서 비디오 프로필을 만들거나 편집할 때 사용자 인터페이스에 없는 고급 비디오 인코딩 매개 변수를 이용할 수 있습니다. 사용자 지정으로 minBitrate 및 maxBitrate와 같은 고급 매개 변수를 기존 프로필에 하나 이상 추가합니다.

**사용자가 추가한 비디오 인코딩 매개 변수를 사용하려면 다음을 수행하십시오**.

1. AEM 로고를 탭한 다음 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite으로 이동합니다.]**
1. CRXDE Lite 페이지의 왼쪽에 있는 탐색기 패널에서 다음 위치로 이동합니다.

   `/conf/global/settings/dam/dm/presets/video/*name_of_video_encoding_profile_to_edit`

1. 페이지의 오른쪽 하단에 있는 패널에서 속성 탭에서 사용할 매개 변수의 **[!UICONTROL 이름]**, **[!UICONTROL 유형]** 및 **[!UICONTROL 값]**&#x200B;을 지정합니다.

   다음 고급 매개 변수를 사용할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>이름</strong></td>
   <td><strong>설명</strong><br /> </td>
   <td><strong>유형</strong><br /> </td>
   <td><strong>값</strong></td>
  </tr>
  <tr>
   <td><code>h264Level</code></td>
   <td>인코딩에 사용할 H.264 수준입니다. 일반적으로 사용하는 인코딩 설정에 따라 자동으로 결정됩니다.</td>
   <td><code>String</code></td>
   <td><p>10 * h264 수준</p> <p>예를 들어 3.0 = 30, 1.3 = 13)</p> <p>기본값이 없습니다.</p> </td>
  </tr>
  <tr>
   <td><code>keyframe</code></td>
   <td>키프레임 사이의 대상 프레임 수입니다. 2-10초마다 키프레임을 생성하려면 이 값을 계산합니다. 예를 들어, 초당 30프레임에서 키프레임 간격은 60-300이어야 합니다.<br /> <br /> 키프레임 간격이 낮을수록 적응형 비디오 인코딩에 대한 스트림 찾기 및 스트림 전환 동작이 향상되며, 동작이 많은 비디오의 품질이 향상됩니다. 그러나 키프레임은 파일의 크기를 늘리므로 키프레임 간격이 낮을수록 일반적으로 지정된 비트율이 전체 비디오 품질이 저하됩니다.</td>
   <td><code>String</code></td>
   <td><p>양수입니다.</p> <p>기본값은 300입니다.</p> <p>HLS(HTTP Live Streaming)에 권장되는 값은 60-90입니다.</p> </td>
  </tr>
  <tr>
   <td><code>minBitrate</code></td>
   <td><p>가변 비트율 인코딩을 허용하는 최소 비트율(Kbps/초)입니다.</p> <p>이 매개 변수는 비디오 인코딩 프로필을 만들거나 편집할 때 고급 탭에서<strong> 고정 비트율 사용</strong> 이 선택 해제된 경우에만 적용됩니다.</p> <p><a href="/help/assets/video.md#bitrate">Bitrate</a>도 참조하십시오.</p> </td>
   <td><code>String</code></td>
   <td><p>양수입니다(Kbps).</p> <p>기본값이 없습니다.</p> </td>
  </tr>
  <tr>
   <td><code>maxBitrate</code></td>
   <td><p>가변 비트율 인코딩을 허용하는 최대 비트율(Kbps)입니다.</p> <p>이 매개 변수는 비디오 인코딩 프로필을 만들거나 편집할 때 고급 탭에서<strong> 고정 비트율 사용</strong> 이 선택 해제된 경우에만 적용됩니다.</p> <p><a href="/help/assets/video.md#bitrate">Bitrate</a>도 참조하십시오.</p> </td>
   <td><code>String</code></td>
   <td><p>양수입니다(Kbps).</p> <p>기본값이 없습니다. 그러나 권장되는 값은 인코딩 비트율의 최대 2배입니다.</p> </td>
  </tr>
  <tr>
   <td><code>audioBitrateCustom</code></td>
   <td>오디오 코덱에서 지원하는 경우 오디오 스트림에 대해 상수 비트율을 강제 수행하려면 값을 <code>true</code> 로 설정하십시오.</td>
   <td><code>String</code></td>
   <td><p><code>true</code>/<code>false</code></p> <p>기본값은 <code>false</code>입니다.</p> <p>HLS(HTTP Live Streaming)에 권장되는 값은 <code>false</code>입니다.</p> <p> </p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-516](assets/chlimage_1-516.png)

1. 페이지의 오른쪽 아래 모서리 근처에 있는 **[!UICONTROL 추가.]**
1. 다음 중 하나를 수행하십시오.

   * 3~4단계를 반복하여 비디오 인코딩 프로필에 다른 매개 변수를 추가합니다.
   * 페이지의 왼쪽 위 모서리 근처에 있는 **[!UICONTROL 모두 저장.]**

1. CRXDE Lite 페이지의 왼쪽 위 모서리에서 **[!UICONTROL 뒤로 홈]** 아이콘을 탭하여 AEM으로 돌아갑니다.

### 비디오 프로필 편집 {#editing-a-video-encoding-profile}

해당 프로필 내에서 비디오 사전 설정을 추가, 편집 또는 삭제하기 위해 만든 모든 비디오 프로필을 편집할 수 있습니다.

기본적으로 Dynamic Media과 함께 제공된 사전 정의된 기본 제공 **[!UICONTROL 응용 비디오 인코딩]** 프로필을 편집할 수 없습니다. 대신 프로필을 쉽게 복사하여 새 이름으로 저장할 수 있습니다. 그런 다음 복사한 프로필에서 원하는 사전 설정을 편집할 수 있습니다.

또한 [비디오 인코딩에 대한 우수 사례](/help/assets/video.md#best-practices-for-encoding-videos)를 참조하십시오.

다른 자산 유형에 대한 고급 처리 매개 변수를 정의하려면 [자산 처리 구성](/help/assets/config-dms7.md#configuring-asset-processing)을 참조하십시오.

**비디오 프로필을 편집하려면 다음을 수행하십시오**.

1. AEM 로고를 탭하고 **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 비디오 프로필로 이동합니다.]**
1. 비디오 프로필 페이지에서 비디오 프로필 이름 하나를 선택합니다.
1. 도구 모음에서 **[!UICONTROL 편집.]**
1. 비디오 인코딩 프로필 페이지에서 원하는 이름과 설명을 편집합니다.
1. 적응형 스트리밍에 대해 **[!UICONTROL 인코딩]** 확인란이 선택되어 있는지 확인하는 것이 좋습니다.
적응형 스트리밍에 대한 설명을 보려면 정보 아이콘을 누릅니다. (점진적 비디오 프로필을 편집하는 경우 이 확인란을 선택하지 마십시오.)
1. 비디오 인코딩 사전 설정 제목 아래에서 프로필을 구성하는 비디오 인코딩 사전 설정을 추가, 편집 또는 삭제합니다.

   선택한 비디오 형식 코덱에 따른 추가적인 설명 또는 권장 설정을 보려면 **[!UICONTROL 기본]** 및 **[!UICONTROL 고급]** 탭의 각 옵션 옆에 있는 정보 아이콘을 탭하십시오.

1. 페이지의 오른쪽 위 모서리에서 **[!UICONTROL 저장.]**

### 비디오 프로필 복사 {#copying-a-video-encoding-profile}

1. AEM 로고를 탭하고 **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 비디오 프로필로 이동합니다.]**
1. 비디오 프로필 페이지에서 비디오 프로필 이름 하나를 선택합니다.
1. 도구 모음에서 **[!UICONTROL 복사.]**
1. 비디오 인코딩 프로필 페이지에서 프로필의 새 이름을 입력합니다.
1. 적응형 스트리밍에 대해 **[!UICONTROL 인코딩]** 확인란이 선택되어 있는지 확인하는 것이 좋습니다. 적응형 스트리밍에 대한 설명을 보려면 정보 아이콘을 누릅니다. (점진적 비디오 프로필을 복사하는 경우 확인란을 선택하지 마십시오.)

   Dynamic Media - 하이브리드 모드에서 WebM 비디오 사전 설정이 비디오 프로필의 일부인 경우 모든 사전 설정이 MP4여야 하므로 **[!UICONTROL 적응형 스트리밍에 인코딩]**&#x200B;을 사용할 수 없습니다.
1. 비디오 인코딩 사전 설정 제목 아래에서 프로필을 구성하는 비디오 인코딩 사전 설정을 추가, 편집 또는 삭제합니다.

   권장 설정 및 설명을 보려면 기본 및 고급 탭의 각 옵션 옆에 있는 정보 아이콘을 누릅니다.

1. 페이지의 오른쪽 위 모서리에서 **[!UICONTROL 저장.]**

### 비디오 프로필 삭제 {#deleting-a-video-encoding-profile}

1. AEM 로고를 탭하고 **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 비디오 프로필로 이동합니다.]**
1. 비디오 프로필 페이지에서 하나 이상의 비디오 프로필 이름을 선택합니다.
1. 도구 모음에서 **[!UICONTROL 삭제]**&#x200B;를 누릅니다.
1. **[!UICONTROL 확인]**

## 폴더에 비디오 프로필 적용 {#applying-a-video-profile-to-folders}

비디오 프로필을 폴더에 할당하면 모든 하위 폴더는 상위 폴더에서 프로필을 자동으로 상속받습니다. 즉, 폴더에 하나의 비디오 프로필만 할당할 수 있습니다. 따라서 자산을 업로드, 저장, 사용 및 보관하는 의 폴더 구조를 신중하게 고려하십시오.

폴더에 다른 비디오 프로필을 할당한 경우 새 프로필이 이전 프로필을 무시합니다. 이전에 기존 폴더 자산은 변경되지 않은 상태로 유지됩니다. 새 프로필은 나중에 폴더에 추가된 자산에 적용됩니다.

프로필이 할당된 폴더는 카드 이름에 표시되는 프로필의 이름으로 사용자 인터페이스에 표시됩니다.

![chlimage_1-517](assets/chlimage_1-517.png)

특정 폴더에 비디오 프로필을 적용하거나 모든 자산에 전체적으로 적용할 수 있습니다.

나중에 변경한 기존 비디오 프로필이 이미 있는 폴더에서 자산을 재처리할 수 있습니다. [폴더의 자산에 대한 처리 프로필을 편집한 후 재처리](processing-profiles.md#reprocessing-assets)를 참조하십시오.

### 특정 폴더에 비디오 프로필 적용 {#applying-video-profiles-to-specific-folders}

**[!UICONTROL 도구]** 메뉴 내에서 또는 폴더에 있는 경우 **[!UICONTROL 속성에서 폴더에 비디오 프로필을 적용할 수 있습니다.]** 이 섹션에서는 두 가지 방법으로 폴더에 비디오 프로필을 적용하는 방법을 설명합니다.

프로필이 이미 할당된 폴더는 폴더 이름 바로 아래에 프로필 이름이 표시되어 표시됩니다.

처리 중인 프로필을 편집한 후 폴더에서 자산 재처리](processing-profiles.md#reprocessing-assets)도 참조하십시오.[

#### 프로필 사용자 인터페이스 {#applying-video-profiles-to-folders-by-way-of-the-profiles-user-interface}을 통해 폴더에 비디오 프로필 적용

1. AEM 로고를 탭하고 **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 비디오 프로필로 이동합니다.]**
1. 폴더 또는 여러 폴더에 적용할 비디오 프로필을 선택합니다.
1. **[!UICONTROL 폴더에 프로필 적용]**&#x200B;을 탭하고 새로 업로드한 자산을 받는 데 사용할 폴더 또는 여러 폴더를 선택하고 **[!UICONTROL 적용 을 탭합니다.]** 프로필이 이미 할당된 폴더는  **[!UICONTROL 카드 보기에서 폴더 이름 바로 아래에 프로필 이름이 표시되어 표시됩니다.]**
비디오  [프로필 처리 작업의 진행 상태를 모니터링할 수 있습니다](#monitoring-the-progress-of-an-encoding-job).

#### 속성 {#applying-video-profiles-to-folders-from-properties}의 폴더에 비디오 프로필 적용

1. AEM 로고를 탭하거나 클릭하고 **[!UICONTROL 자산]**&#x200B;으로 이동한 다음, 비디오 프로필을 적용할 폴더로 이동합니다.
1. 폴더에서 확인 표시를 눌러 선택한 다음 **[!UICONTROL 속성]**&#x200B;을 누릅니다.
1. **[!UICONTROL 비디오 프로필]** 탭을 선택하고 드롭다운 메뉴에서 프로필을 선택한 다음 **[!UICONTROL 저장 및 닫기 를 클릭합니다.]** 프로필이 이미 할당된 폴더는 폴더 이름 바로 아래에 프로필 이름이 표시되어 표시됩니다.

   ![chlimage_1-518](assets/chlimage_1-518.png)
비디오  [프로필 처리 작업의 진행 상태를 모니터링할 수 있습니다](#monitoring-the-progress-of-an-encoding-job).

### 전역 {#applying-a-video-profile-globally} 비디오 프로필 적용

폴더에 프로필을 적용하는 것 외에도 폴더에 업로드된 모든 컨텐츠가 선택한 프로필이 적용되도록 전체적으로 프로필을 적용할 수도 있습니다.

처리 중인 프로필을 편집한 후 폴더에서 자산 재처리](processing-profiles.md#reprocessing-assets)도 참조하십시오.[

**비디오 프로필을 전체적으로** 적용하려면

* 다음 노드로 CRXDE Lite으로 이동합니다.`/content/dam/jcr:content` `videoProfile:/libs/settings/dam/video/dynamicmedia/<name of video encoding profile>` 속성을 추가하고 **[!UICONTROL 모두 저장.]**

   ![chlimage_1-519](assets/chlimage_1-519.png)
* [비디오 프로필 처리 작업의 진행 상황을 모니터링할 수 있습니다](#monitoring-the-progress-of-an-encoding-job).

## 비디오 프로필 처리 작업 {#monitoring-the-progress-of-an-encoding-job} 진행 상태 모니터링

비디오 프로필 처리 작업의 진행 상태를 시각적으로 모니터링할 수 있도록 처리 표시기(또는 진행률 표시줄)가 표시됩니다.

또한 `error.log` 파일을 보고 인코딩 작업의 진행 상황을 모니터링하거나 인코딩이 완료되었는지 확인하거나 작업 오류를 확인할 수 있습니다. `error.log`은 AEM 인스턴스가 설치된 `logs` 폴더에 있습니다.

## 폴더 {#removing-a-video-profile-from-folders}에서 비디오 프로필 제거

폴더에서 비디오 프로필을 제거하면 모든 하위 폴더는 해당 상위 폴더에서 프로필 제거를 자동으로 상속합니다. 그러나 폴더 내에서 발생한 파일의 모든 처리가 그대로 유지됩니다.

**[!UICONTROL 도구]** 메뉴 내에서 또는 폴더에 있는 경우 **[!UICONTROL 폴더 설정에서 비디오 프로필을 제거할 수 있습니다.]** 이 섹션에서는 두 가지 방법으로 폴더에서 비디오 프로필을 제거하는 방법을 설명합니다.

### 프로필 사용자 인터페이스 {#removing-video-profiles-from-folders-by-way-of-the-profiles-user-interface} 를 통해 폴더에서 비디오 프로필 제거

1. AEM 로고를 탭하고 **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 비디오 프로필로 이동합니다.]**
1. 폴더 또는 여러 폴더에서 제거할 비디오 프로필을 선택합니다.
1. **[!UICONTROL 폴더에서 프로필 제거]**&#x200B;를 탭하고 프로필을 제거하는 데 사용할 폴더 또는 여러 폴더를 선택하고 **[!UICONTROL 제거.]**&#x200B;를 탭합니다.

   이름이 더 이상 폴더 이름 아래에 표시되지 않으므로 비디오 프로필이 더 이상 폴더에 적용되지 않았는지 확인할 수 있습니다.

### {#removing-video-profiles-from-folders-by-way-of-properties} 속성을 사용하여 폴더에서 비디오 프로필 제거

1. AEM 로고를 탭하거나 클릭하고 **[!UICONTROL 자산]**&#x200B;으로 이동한 다음, 비디오 프로필을 제거할 폴더로 이동합니다.
1. 폴더에서 확인 표시를 탭하거나 클릭하여 선택한 다음, **[!UICONTROL 속성.]**
1. **[!UICONTROL 비디오 프로필]** 탭을 선택하고 드롭다운 메뉴에서 **[!UICONTROL 없음]**&#x200B;을 선택하고 **[!UICONTROL 저장 및 닫기 를 클릭합니다.]** 프로필이 이미 할당된 폴더는 폴더 이름 바로 아래에 프로필 이름이 표시되어 표시됩니다.
