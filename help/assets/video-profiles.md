---
title: 비디오 프로필
description: Dynamic Media에는 이미 사전 정의된 응용 비디오 인코딩 프로필이 포함되어 있습니다. 이 기본 프로필의 설정은 고객에게 최상의 시청 환경을 제공하도록 최적화되었습니다. 비디오에 스마트 자르기를 추가할 수도 있습니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
docset: aem65
feature: Video Profiles
role: User, Admin
mini-toc-levels: 3
exl-id: b290fac2-7259-45d7-b733-70419d632b07
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '3770'
ht-degree: 8%

---

# 비디오 프로필 {#video-profiles}

Dynamic Media에는 이미 사전 정의된 응용 비디오 인코딩 프로필이 포함되어 있습니다. 이 기본 프로필의 설정은 고객에게 최상의 시청 환경을 제공하도록 최적화되었습니다. 응용 비디오 인코딩 프로필을 사용하여 기본 소스 비디오를 인코딩하면 재생 중에 비디오 플레이어가 고객의 인터넷 연결 속도에 따라 비디오 스트림의 품질을 자동으로 조정합니다. 이 기능을 적응형 비트율 스트리밍이라고 합니다.

다음은 비디오의 품질을 결정하는 다른 요소입니다.

* **업로드된 기본 소스 비디오의 해상도**

  MP4 영상이 240p 또는 360p와 같이 낮은 해상도로 녹화된 경우 고화질로 스트리밍할 수 없습니다.

* **비디오 플레이어 크기**

  기본적으로 응용 비디오 인코딩 프로필의 &quot;너비&quot;는 &quot;자동&quot;으로 설정됩니다. 다시 말하지만 재생 중에는 플레이어 크기에 따라 최상의 품질이 사용됩니다.

다음을 참조하십시오 [비디오 인코딩에 대한 우수 사례](/help/assets/video.md#best-practices-for-encoding-videos).

참조: [처리 프로필 사용을 위한 디지털 자산 구성 우수 사례](/help/assets/organize-assets.md).

>[!NOTE]
>
>비디오의 메타데이터 및 관련 비디오 이미지 썸네일을 생성하려면 비디오 자체가 Dynamic Media의 인코딩 프로세스를 거쳐야 합니다. Adobe Experience Manager에서 **[!UICONTROL Dynamic Media 인코딩 비디오]** Dynamic Media을 활성화하고 비디오 클라우드 서비스를 설정한 경우 워크플로는 비디오를 인코딩합니다. This workflow captures workflow process history and failure information. 다음을 참조하십시오 [비디오 인코딩 및 YouTube 게시 진행 모니터링](/help/assets/video.md#monitoring-video-encoding-and-youtube-publishing-progress). Dynamic Media을 활성화하고 비디오 클라우드 서비스를 설정한 경우 **[!UICONTROL Dynamic Media 인코딩 비디오]** 워크플로우는 비디오를 업로드할 때 자동으로 적용됩니다. (Dynamic Media을 사용하지 않는 경우 **[!UICONTROL DAM 자산 업데이트]** 워크플로가 적용됩니다.)
>
>메타데이터는 에셋을 검색할 때 유용합니다. 썸네일은 인코딩 중에 생성되는 정적 비디오 이미지입니다. 카드 보기, 검색 결과 보기 및 에셋 목록 보기에서 비디오를 시각적으로 식별하는 데 도움이 되도록 Experience Manager 시스템에서 요구하고 사용자 인터페이스에 사용됩니다. 인코딩된 비디오의 렌디션 아이콘(페인트 팔레트)을 선택하면 생성된 썸네일을 볼 수 있습니다.

비디오 프로필 작성이 완료되면 폴더 또는 여러 폴더에 적용합니다. 다음을 참조하십시오 [폴더에 비디오 프로필 적용](#applying-a-video-profile-to-folders).

다른 자산 유형에 대한 고급 처리 매개 변수를 정의하려면 다음을 참조하십시오. [자산 처리 구성](/help/assets/config-dms7.md#configuring-asset-processing).

참조: [메타데이터, 이미지 및 비디오 처리용 프로필](processing-profiles.md).

## 응용 비디오 인코딩 사전 설정 {#adaptive-video-encoding-presets}

다음 표에서는 모바일 및 태블릿 장치와 데스크탑 컴퓨터에 대한 응용 비디오 스트리밍에 대한 모범 사례 인코딩 프로필을 식별합니다. 모든 종횡비 비디오에 이러한 사전 설정을 사용할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>비디오 형식 코덱</strong></td>
   <td><strong>비디오 크기 - 너비(픽셀)</strong></td>
   <td><strong>비디오 크기 - 높이(픽셀)</strong></td>
   <td><strong>종횡비를 유지하시겠습니까?</strong></td>
   <td><strong>비디오 비트율(Kbps)</strong></td>
   <td><strong>비디오 프레임 속도(Fps)</strong></td>
   <td><strong>오디오 코덱</strong></td>
   <td><strong>오디오 비트율(Kbps)</strong></td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>360</td>
   <td>예</td>
   <td>730</td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>540</td>
   <td>예</td>
   <td>2000<br /> </td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>720<br /> </td>
   <td>예</td>
   <td>3000<br /> </td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
 </tbody>
</table>

## 비디오 프로필에서 스마트 자르기 사용 정보 {#about-smart-crop-video}

비디오 프로필에서 사용할 수 있는 선택적 기능인 비디오용 스마트 자르기는 Adobe Sensei에서 인공 지능의 기능을 사용하는 도구입니다. 크기에 상관없이 업로드한 모든 응용 비디오 또는 점진적 비디오에서 초점을 자동으로 감지하고 자릅니다.

스마트 자르기에 지원되는 비디오 형식에는 MP4, MKV, MOV, AVI, FLV 및 WMV가 포함됩니다.

스마트 자르기에 지원되는 최대 비디오 파일 크기는 다음 기준입니다.

* 5분 동안 지속됩니다.
* 초당 30프레임(FPS).
* 300MB의 파일 크기입니다.

Adobe Sensei은 9000프레임으로 제한됩니다. 즉, 30FPS로 5분. 비디오의 FPS가 더 높으면 지원되는 최대 비디오 지속 시간이 줄어듭니다. 예를 들어 60FPS 비디오는 Adobe Sensei 및 스마트 자르기에서 지원되려면 2분 30초 정도 있어야 합니다.

![비디오용 스마트 자르기](assets/smart-crop-video.png)

>[!IMPORTANT]
>
>비디오 스마트 자르기가 작동하려면 비디오 프로필에 비디오 인코딩 사전 설정을 하나 이상 포함해야 합니다.

비디오에 스마트 자르기를 사용하려면 적응형 또는 점진적 비디오 인코딩 프로필을 만듭니다. 프로필의 일부로 **[!UICONTROL 스마트 자르기 비율]** 사전 정의된 종횡비를 선택하는 도구입니다. 예를 들어 비디오 인코딩 사전 설정을 정의한 후 종횡비가 16×9인 &quot;모바일 가로&quot; 정의와 종횡비가 9×16인 &quot;모바일 세로&quot; 정의를 추가할 수 있습니다. 선택할 수 있는 기타 양상 또는 자르기 비율에는 1×1, 4×3 및 4×5가 포함됩니다.

![스마트 자르기로 비디오 인코딩 프로필 편집](assets/edit-smart-crop-video2.png)

의 맨 오른쪽에 있는 슬라이더를 사용하여 비디오 프로필에서 비디오 스마트 자르기를 켜거나 끌 수 있습니다 **[!UICONTROL 스마트 자르기 비율]** 을 참조하십시오.

비디오 프로필을 만들어 저장한 후 원하는 폴더에 적용할 수 있습니다.

다음을 참조하십시오 [특정 폴더에 비디오 프로필 적용](#applying-video-profiles-to-specific-folders) 또는 [비디오 프로필을 전체적으로 적용](#applying-a-video-profile-globally).

참조: [이미지에 대한 스마트 자르기](image-profiles.md).

## 적응형 비트율 스트리밍을 위한 비디오 프로필 만들기 {#creating-a-video-encoding-profile-for-adaptive-streaming}

Dynamic Media에는 이미 사전 정의된 응용 비디오 인코딩 프로필(MP4 H.264에 대한 비디오 업로드 설정 그룹)이 포함되어 있으며 이는 최상의 보기 환경에 최적화되어 있습니다. 비디오를 업로드할 때 이 프로필을 사용할 수 있습니다.

그러나 이 사전 정의된 프로필이 사용자의 요구를 충족하지 않으면 고유한 응용 비디오 인코딩 프로필을 만들도록 선택할 수 있습니다. 설정을 사용할 때 **[!UICONTROL 적응형 스트리밍을 위한 인코딩]** - 우수 사례로서, 프로필에 추가하는 모든 인코딩 사전 설정은 모든 비디오가 동일한 종횡비를 가지도록 유효성이 검사됩니다. 또한, 인코딩된 비디오는 스트리밍을 위해 설정된 멀티-비트율로 취급된다.

비디오 인코딩 프로필을 만들 때 대부분의 인코딩 옵션이 사용자를 돕기 위해 권장되는 기본 설정으로 미리 채워집니다. 그러나 권장 기본값 이외의 값을 선택하면 재생 중 비디오 품질이 저하되고 기타 성능 문제가 발생할 수 있습니다.

따라서 프로필의 모든 MP4 H.264 비디오 인코딩 사전 설정에 대해 다음 값이 프로필의 개별 인코딩 사전 설정에서 동일한지 확인하여 적응형 비트율 스트리밍을 가능하게 합니다.

* 비디오 형식 코덱 - MP4 H.264(.mp4)
* 오디오 코덱
* 오디오 비트율
* 종횡비 유지
* 2회 인코딩
* 상수 비트율
* H264 프로필
* 오디오 샘플링 속도

값이 같지 않으면 그대로 프로필을 계속 만들 수 있습니다. 단, 적응형 비트율 스트리밍은 불가능합니다. 대신 사용자는 단일 비트 전송률 스트리밍을 경험합니다. 프로필의 개별 인코딩 사전 설정에서 동일한 값을 사용하도록 인코딩 설정을 편집하는 것이 좋습니다. (다음의 경우 비디오 프로필/사전 설정 편집기는 적응형 비디오 인코딩 설정의 패리티를 적용합니다.) **[!UICONTROL 적응형 스트리밍을 위한 인코딩]** 이(가) 활성화되었습니다.

참조: [점진적 스트리밍을 위한 비디오 인코딩 프로필 만들기](#creating-a-video-encoding-profile-for-progressive-streaming).

참조: [비디오 인코딩에 대한 우수 사례](/help/assets/video.md#best-practices-for-encoding-videos).

다른 자산 유형에 대한 고급 처리 매개 변수를 정의하려면 다음을 참조하십시오. [자산 처리 구성](/help/assets/config-dms7.md#configuring-asset-processing).

**적응형 비트율 스트리밍을 위한 비디오 프로필을 만들려면**,

1. Experience Manager 로고를 선택하고 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]** > **[!UICONTROL 비디오 프로필]**.
1. 선택 **[!UICONTROL 만들기]** 비디오 프로필을 추가합니다.

1. 프로필의 이름과 설명을 입력합니다.
1. 비디오 인코딩 사전 설정 만들기/편집 페이지에서 다음을 선택합니다. **[!UICONTROL 비디오 인코딩 사전 설정 추가]**.
1. 다음에서 **[!UICONTROL 기본]** 탭에서 비디오 및 오디오 옵션을 설정합니다.
선택한 비디오 형식 코덱에 따라 추가 설명 또는 권장 설정을 보려면 각 옵션 옆에 있는 정보 아이콘을 선택합니다.
1. 비디오 크기 제목에서 **[!UICONTROL 종횡비 유지]** 이(가) 선택되었습니다.
1. 비디오 프레임 크기 해상도를 픽셀 단위로 설정합니다. 사용 **[!UICONTROL 자동]** 소스 종횡비(폭 대 높이 비율)와 일치하도록 자동으로 비율이 조정되는 값입니다. 예를 들어 Auto x 480 또는 640 x Auto가 있습니다.

1. 다음 중 하나를 수행하십시오.

   * 다음에서 **[!UICONTROL 폭]** 필드, 입력 **[!UICONTROL auto]**. 다음에서 **[!UICONTROL 높이]** 필드에 값을 픽셀 단위로 입력합니다.

   * 비디오 크기를 시각화하려면 오른쪽에 있는 정보 아이콘(i)을 선택합니다 **[!UICONTROL 높이]** 를 눌러 [크기 계산기] 페이지를 엽니다. 사용 **[!UICONTROL 크기 계산기]** 원하는 비디오 치수(파란색 상자로 표시됨)를 설정합니다. 선택 **[!UICONTROL X]** 작업을 마치면 오른쪽 상단 모서리에 있습니다.

1. (선택 사항) **[!UICONTROL 고급]** 탭을 클릭하고 다음을 확인합니다. **[!UICONTROL 기본값 사용]** 확인란이 선택되어 있습니다(권장). 또는 고급 비디오 및 오디오 설정을 수정합니다.
1. 페이지의 오른쪽 상단 모서리에서 을(를) 선택합니다. **[!UICONTROL 저장]** 사전 설정을 저장합니다.
1. 다음 중 하나를 수행하십시오.
   * 4~10단계를 반복하여 인코딩 사전 설정을 추가로 만듭니다. (응용 비디오 스트리밍에는 두 개 이상의 비디오 사전 설정이 필요합니다.)
   * 다음 단계로 진행합니다.

1. (선택 사항) 이 프로필이 적용되는 비디오에 비디오 스마트 자르기를 추가하려면 다음을 수행하십시오.
   * 비디오 프로필 편집 페이지의 스마트 자르기 비율 머리글 오른쪽에서 을 선택합니다. **[!UICONTROL 새로 추가]**.
   * 이름 필드에 자르기 비율을 쉽게 식별할 수 있도록 이름을 입력합니다.
   * 다음에서 **[!UICONTROL 자르기 비율]** 드롭다운 목록에서 사용할 비율을 선택합니다.

1. 다음 중 하나를 수행하십시오.

   * 필요에 따라 새 자르기 비율을 계속 추가합니다.
   * 다음 단계로 진행합니다.

1. 페이지의 오른쪽 상단 모서리에서 을(를) 선택합니다. **[!UICONTROL 저장]** 다시 클릭하여 프로필을 저장합니다.

이제 비디오가 포함된 폴더에 프로필을 적용할 수 있습니다. 다음을 참조하십시오 [폴더에 비디오 프로필 적용](#applying-a-video-profile-to-folders) 또는 [비디오 프로필을 전체적으로 적용](#applying-a-video-profile-globally).

## 점진적 스트리밍을 위한 비디오 프로필 만들기 {#creating-a-video-encoding-profile-for-progressive-streaming}

옵션을 사용하지 않기로 선택한 경우 **[!UICONTROL 적응형 스트리밍을 위한 인코딩]**: 프로필에 추가하는 모든 인코딩 사전 설정은 단일 비트율 스트리밍 또는 점진적 비디오 전송을 위한 개별 비디오 표현물로 처리됩니다. Also, there is no validation to ensure that all the video renditions have the same aspect ratio.

실행 중인 모드에 따라 지원되는 비디오 형식 코덱은 다음과 같습니다.

* Dynamic Media-Scene7 모드: H.264(.mp4)
* Dynamic Media-하이브리드 모드: H.264(.mp4), WebM

참조: [적응형 비트율 스트리밍을 위한 비디오 인코딩 프로필 만들기](#creating-a-video-encoding-profile-for-adaptive-streaming).

참조: [비디오 인코딩에 대한 우수 사례](/help/assets/video.md#best-practices-for-encoding-videos).

다른 자산 유형에 대한 고급 처리 매개 변수를 정의하려면 다음을 참조하십시오. [자산 처리 구성](/help/assets/config-dms7.md#configuring-asset-processing).

**점진적 스트리밍을 위한 비디오 프로필을 만들려면 다음 작업을 수행하십시오.**

1. Experience Manager 로고를 선택하고 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]** > **[!UICONTROL 비디오 프로필]**.
1. 선택 **[!UICONTROL 만들기]** 비디오 프로필을 추가합니다.
1. 프로필의 이름과 설명을 입력합니다.
1. 비디오 인코딩 사전 설정 만들기/편집 페이지에서 다음을 선택합니다. **[!UICONTROL 비디오 인코딩 사전 설정 추가]**.
1. 다음에서 **[!UICONTROL 기본]** 탭에서 비디오 및 오디오 옵션을 설정합니다.
선택한 비디오 형식 코덱에 따라 추가 설명 또는 권장 설정을 보려면 각 옵션 옆에 있는 정보 아이콘을 선택합니다.
1. (선택 사항) 비디오 크기 제목에서 선택을 취소합니다 **[!UICONTROL 종횡비 유지]**.
1. 다음 작업을 수행합니다.
   * 다음에서 **[!UICONTROL 폭]** 필드, 입력 **[!UICONTROL auto]**.
   * 다음에서 **[!UICONTROL 높이]** 필드에 값을 픽셀 단위로 입력합니다.
비디오의 크기를 시각화하려면 높이의 정보 아이콘을 선택하여 **[!UICONTROL 크기 계산기]** 페이지를 가리키도록 업데이트하는 중입니다. 사용 **[!UICONTROL 크기 계산기]** 원하는 비디오 차원 (파란색 상자)을 추가로 설정하는 페이지입니다. 완료되면 대화 상자의 오른쪽 상단 모서리에서 을 선택합니다 **[!UICONTROL X]**.
1. (선택 사항) 다음 중 하나를 수행합니다.

   * 다음 항목 선택 **[!UICONTROL 고급]** 탭을 클릭하고 **[!UICONTROL 기본값 사용]** 확인란이 선택되어 있습니다(권장).

   * 지우기 **[!UICONTROL 기본값 사용]** 확인란을 선택하고 원하는 비디오 설정과 오디오 설정을 지정합니다.
선택한 비디오 형식 코덱에 따라 추가 설명 또는 권장 설정을 보려면 각 옵션 옆에 있는 정보 아이콘을 선택합니다.

1. 페이지의 오른쪽 상단 모서리에서 을(를) 선택합니다. **[!UICONTROL 저장]** 사전 설정을 저장합니다.
1. 다음 중 하나를 수행하십시오.

   * 4~9단계를 반복하여 인코딩 사전 설정을 추가로 만듭니다.
   * 다음 단계로 진행합니다.

1. (선택 사항) 이 프로필이 적용되는 비디오에 비디오 스마트 자르기를 추가하려면 다음을 수행하십시오.

   * 비디오 프로필 편집 페이지의 스마트 자르기 비율 머리글 오른쪽에서 을 선택합니다. **[!UICONTROL 새로 추가]**.
   * 이름 필드에 자르기 비율을 쉽게 식별할 수 있도록 이름을 입력합니다.
   * 다음에서 **[!UICONTROL 자르기 비율]** 드롭다운 목록에서 사용할 비율을 선택합니다.

1. 다음 중 하나를 수행하십시오.

   * 필요에 따라 새 자르기 비율을 계속 추가합니다.
   * 다음 단계로 진행합니다.

1. 페이지의 오른쪽 상단 모서리에서 을(를) 선택합니다. **[!UICONTROL 저장]** 을 클릭하여 프로필을 저장합니다.

이제 비디오가 포함된 폴더에 프로필을 적용할 수 있습니다. 다음을 참조하십시오 [폴더에 비디오 프로필 적용](#applying-a-video-profile-to-folders) 또는 [비디오 프로필을 전체적으로 적용](#applying-a-video-profile-globally).

## 사용자가 추가한 비디오 인코딩 매개 변수 사용 {#using-custom-added-video-encoding-parameters}

기존 비디오 인코딩 프로필을 편집하여 Experience Manager에서 비디오 프로필을 만들거나 편집할 때 사용자 인터페이스에서 볼 수 없는 고급 비디오 인코딩 매개 변수를 활용할 수 있습니다. minBitrate 및 maxBitrate와 같은 하나 이상의 고급 매개 변수를 기존 프로필에 추가합니다.

**사용자가 추가한 비디오 인코딩 매개 변수를 사용하려면:**

1. Experience Manager 로고를 선택한 다음 로 이동합니다. **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**.
1. CRXDE Lite 페이지의 왼쪽에 있는 탐색기 패널에서 다음과 같이 이동합니다.

   `/conf/global/settings/dam/dm/presets/video/*name_of_video_encoding_profile_to_edit`

1. In the panel on the lower-right side of the page, from the Properties tab, specify the **[!UICONTROL Name]**, **[!UICONTROL Type]**, and **[!UICONTROL Value]** of the parameter you want to use.

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
   <td>인코딩에 사용할 H.264 수준입니다. 일반적으로 이 매개 변수는 사용 중인 인코딩 설정을 기반으로 자동으로 결정됩니다.</td>
   <td><code>String</code></td>
   <td><p>10 * h264 level</p> <p>예를 들어, 3.0 = 30, 1.3 = 13)</p> <p>기본값이 없습니다.</p> </td>
  </tr>
  <tr>
   <td><code>keyframe</code></td>
   <td>키프레임 사이의 대상 프레임 수입니다. 2~10초마다 키프레임을 생성할 수 있도록 이 값을 계산합니다. 예를 들어 초당 30프레임인 경우 키프레임 간격은 60-300이어야 합니다.<br /> <br /> 낮은 키프레임 간격은 적응형 비디오 인코딩을 위한 스트림 찾기 및 스트림 전환 동작을 개선하고, 움직임이 많은 비디오의 품질을 향상시킬 수도 있습니다. 그러나 키프레임은 파일 크기를 늘리기 때문에 낮은 키프레임 간격은 일반적으로 주어진 비트율로 전반적인 비디오 품질이 저하됩니다.</td>
   <td><code>String</code></td>
   <td><p>양수입니다.</p> <p>기본값은 300입니다.</p> <p>DASH 또는 HLS의 권장 값은 60-90입니다. 비디오에 DASH를 사용하려면 먼저 계정에서 활성화해야 합니다. 다음을 참조하십시오 <a href="/help/assets/video.md#enable-dash">계정에서 DASH 활성화</a>.)</p> </td>
  </tr>
  <tr>
   <td><code>minBitrate</code></td>
   <td><p>가변 비트율 인코딩을 허용하는 최소 비트율(Kbps/초)입니다.</p> <p>이 매개 변수는 다음과 같은 경우에만 적용됩니다.<strong> 상수 비트율 사용</strong> 비디오 인코딩 프로필을 만들거나 편집할 때 고급 탭에서 이 선택 해제됩니다.</p> <p>참조: <a href="/help/assets/video.md#bitrate">비트율</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>양수, Kbps.</p> <p>기본값이 없습니다.</p> </td>
  </tr>
  <tr>
   <td><code>maxBitrate</code></td>
   <td><p>가변 비트율 인코딩을 허용하는 최대 비트율(Kbps)입니다.</p> <p>이 매개 변수는 다음과 같은 경우에만 적용됩니다.<strong> 상수 비트율 사용</strong> 비디오 인코딩 프로필을 만들거나 편집할 때 고급 탭에서 이 선택 해제됩니다.</p> <p>참조: <a href="/help/assets/video.md#bitrate">비트율</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>양수, Kbps.</p> <p>기본값이 없습니다. 하지만 권장 값은 인코딩 비트율의 최대 2배입니다.</p> </td>
  </tr>
  <tr>
   <td><code>audioBitrateCustom</code></td>
   <td>값을 다음으로 설정 <code>true</code> 오디오 코덱에서 지원하는 경우 오디오 스트림에 대해 상수 비트율을 강제 적용합니다.</td>
   <td><code>String</code></td>
   <td><p><code>true</code>/<code>false</code></p> <p>기본값은 입니다 <code>false</code>.</p> <p>DASH 또는 HLS에 대한 권장 값은 입니다. <code>false</code>. 비디오에 DASH를 사용하려면 먼저 계정에서 활성화해야 합니다. 다음을 참조하십시오 <a href="/help/assets/video.md#enable-dash">계정에서 DASH 활성화</a>.)</p> <p> </p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-516](assets/chlimage_1-516.png)

1. 페이지의 오른쪽 아래 모서리 근처에서 을 선택합니다. **[!UICONTROL 추가]**.
1. 다음 중 하나를 수행하십시오.

   * 3단계와 4단계를 반복하여 비디오 인코딩 프로필에 다른 매개 변수를 추가합니다.
   * 페이지의 왼쪽 상단 모서리 근처에서 을 선택합니다. **[!UICONTROL 모두 저장]**.

1. CRXDE Lite 페이지의 왼쪽 상단 모서리에서 **[!UICONTROL 다시 홈으로]** 아이콘으로 Experience Manager 돌아갑니다.

### 비디오 프로필 편집 {#editing-a-video-encoding-profile}

만든 비디오 프로필을 편집하여 해당 프로필 내에서 비디오 사전 설정을 추가, 편집 또는 삭제할 수 있습니다.

기본적으로 사전 정의된 기본 항목은 편집할 수 없습니다 **[!UICONTROL 응용 비디오 인코딩]** Dynamic Media과 함께 제공된 프로필입니다. 대신 프로필을 쉽게 복사하여 새 이름으로 저장할 수 있습니다. 그런 다음 복사한 프로필에서 원하는 사전 설정을 편집할 수 있습니다.

참조: [비디오 인코딩에 대한 우수 사례](/help/assets/video.md#best-practices-for-encoding-videos).

다른 자산 유형에 대한 고급 처리 매개 변수를 정의하려면 다음을 참조하십시오. [자산 처리 구성](/help/assets/config-dms7.md#configuring-asset-processing).

**비디오 프로필을 편집하려면:**

1. Experience Manager 로고를 선택하고 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]** > **[!UICONTROL 비디오 프로필]**.
1. 비디오 프로필 페이지에서 비디오 프로필 이름 하나를 확인합니다.
1. 도구 모음에서 를 선택합니다. **[!UICONTROL 편집]**.
1. 비디오 인코딩 프로필 페이지에서 원하는 대로 이름과 설명을 편집합니다.
1. 우수 사례로서, **[!UICONTROL 적응형 비트율 스트리밍을 위한 인코딩]** 확인란이 선택되어 있습니다.
적응형 비트율 스트리밍에 대한 설명을 보려면 정보 아이콘을 선택합니다. 점진적 비디오 프로필을 편집하는 경우 이 확인란을 선택하지 마십시오.
1. 비디오 인코딩 사전 설정 제목 아래에서 프로필을 구성하는 비디오 인코딩 사전 설정을 추가, 편집 또는 삭제합니다.

   에서 각 옵션 옆에 있는 정보 아이콘을 선택합니다. **[!UICONTROL 기본]** 및 **[!UICONTROL 고급]** 선택한 비디오 형식 코덱에 따른 추가 설명 또는 권장 설정에 대한 탭입니다.

1. 페이지의 오른쪽 상단 모서리에서 을(를) 선택합니다. **[!UICONTROL 저장]**.

### 비디오 프로필 복사 {#copying-a-video-encoding-profile}

1. Experience Manager 로고를 선택하고 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]** > **[!UICONTROL 비디오 프로필]**.
1. 비디오 프로필 페이지에서 비디오 프로필 이름 하나를 확인합니다.
1. 도구 모음에서 를 선택합니다. **[!UICONTROL 복사]**.
1. 비디오 인코딩 프로필 페이지에서 프로필의 새 이름을 입력합니다.
1. As a best practice, ensure that the **[!UICONTROL Encode for adaptive streaming]** check box is selected. 적응형 비트율 스트리밍에 대한 설명을 보려면 정보 아이콘을 선택합니다. (If you are copying a progressive video profile, do not select the check box.)

   Dynamic Media - 하이브리드 모드에서 WebM 비디오 사전 설정이 비디오 프로필의 일부인 경우 **[!UICONTROL 적응형 스트리밍을 위한 인코딩]** 모든 사전 설정은 MP4여야 하므로 사용할 수 없습니다.
1. 비디오 인코딩 사전 설정 제목 아래에서 프로필을 구성하는 비디오 인코딩 사전 설정을 추가, 편집 또는 삭제합니다.

   기본 및 고급 탭에서 권장 설정 및 설명을 보려면 각 옵션 옆에 있는 정보 아이콘을 선택합니다.

1. 페이지의 오른쪽 상단 모서리에서 을(를) 선택합니다. **[!UICONTROL 저장]**.

### 비디오 프로필 삭제 {#deleting-a-video-encoding-profile}

1. Experience Manager 로고를 선택하고 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]** > **[!UICONTROL 비디오 프로필]**.
1. 비디오 프로필 페이지에서 하나 이상의 비디오 프로필 이름을 확인합니다.
1. 도구 모음에서 를 선택합니다. **[!UICONTROL 삭제]**.
1. 선택 **[!UICONTROL 확인]**.

## 폴더에 비디오 프로필 적용 {#applying-a-video-profile-to-folders}

폴더에 비디오 프로필을 할당하면 하위 폴더는 자동으로 상위 폴더에서 프로필을 상속합니다. 이 규칙은 하나의 비디오 프로필만 폴더에 할당할 수 있음을 의미합니다. 따라서 에셋을 업로드, 저장, 사용 및 보관하는 의 폴더 구조를 신중하게 고려하십시오.

폴더에 다른 비디오 프로필을 할당하면 새 프로필이 이전 프로필을 재정의합니다. 이전의 기존 폴더 자산은 변경되지 않습니다. 새 프로필은 나중에 폴더에 추가되는 에셋에 적용됩니다.

프로필이 할당된 폴더는 카드 이름에서 프로필 이름의 모양으로 사용자 인터페이스에 표시됩니다.

![chlimage_1-517](assets/chlimage_1-517.png)

비디오 프로필을 특정 폴더에 적용하거나 모든 에셋에 전역적으로 적용할 수 있습니다.

나중에 변경한 기존 비디오 프로필이 이미 있는 폴더에서 에셋을 재처리할 수 있습니다. 다음을 참조하십시오 [처리 중인 프로필을 편집한 후 폴더에서 에셋 재처리](processing-profiles.md#reprocessing-assets).

### 특정 폴더에 비디오 프로필 적용 {#applying-video-profiles-to-specific-folders}

You can apply a video profile to a folder from within the **[!UICONTROL Tools]** menu or if you are in the folder, from the **[!UICONTROL Properties]**. This section describes how to apply video profiles to folders both ways.

Folders that have a profile already assigned to it are indicated by the display of the profile&#39;s name directly below the folder name.

참조: [처리 중인 프로필을 편집한 후 폴더에서 에셋 재처리](processing-profiles.md#reprocessing-assets).

#### 프로필 사용자 인터페이스를 통해 폴더에 비디오 프로필 적용 {#applying-video-profiles-to-folders-by-way-of-the-profiles-user-interface}

1. Experience Manager 로고를 선택하고 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]** > **[!UICONTROL 비디오 프로필]**.
1. 폴더 또는 여러 폴더에 적용할 비디오 프로필을 선택합니다.
1. 선택 **[!UICONTROL 폴더에 프로필 적용]** 새로 업로드한 자산을 받는 데 사용할 폴더 또는 여러 폴더를 선택하고 을(를) 선택합니다 **[!UICONTROL 적용]**. 이미 프로필이 할당된 폴더는에 있는 동안 폴더 이름 바로 아래에 프로필 이름이 표시됩니다. **[!UICONTROL 카드 보기]**.
다음을 수행할 수 있습니다. [비디오 프로필 처리 작업 진행 상황 모니터링](#monitoring-the-progress-of-an-encoding-job).

#### 속성에서 폴더에 비디오 프로필 적용 {#applying-video-profiles-to-folders-from-properties}

1. Experience Manager 로고를 선택하고 다음으로 이동 **[!UICONTROL 에셋]** 그런 다음 비디오 프로필을 적용할 폴더로 이동합니다.
1. 폴더에서 확인 표시를 선택하여 선택한 다음 을 선택합니다 **[!UICONTROL 속성]**.
1. 다음 항목 선택 **[!UICONTROL 비디오 프로필]** 탭을 클릭하고 드롭다운 메뉴에서 프로필을 선택한 다음 를 선택합니다. **[!UICONTROL 저장 및 닫기]**. Folders that have a profile already assigned to it are indicated by the display of the profile&#39;s name directly below the folder name.

   ![chlimage_1-518](assets/chlimage_1-518.png)
다음을 수행할 수 있습니다. [비디오 프로필 처리 작업 진행 상황 모니터링](#monitoring-the-progress-of-an-encoding-job).

### 비디오 프로필을 전체적으로 적용 {#applying-a-video-profile-globally}

폴더에 프로필을 적용하는 것 외에도, 모든 폴더의 Experience Manager Assets에 업로드된 모든 컨텐츠에 선택한 프로필이 적용되도록 전역적으로 적용할 수도 있습니다.

참조: [처리 중인 프로필을 편집한 후 폴더에서 에셋 재처리](processing-profiles.md#reprocessing-assets).

**비디오 프로필을 전역적으로 적용하려면:**

* 다음 CRXDE Lite으로 이동합니다. `/content/dam/jcr:content`. 속성 추가 `videoProfile:/libs/settings/dam/video/dynamicmedia/<name of video encoding profile>` 및 선택 **[!UICONTROL 모두 저장]**.

  ![chlimage_1-519](assets/chlimage_1-519.png)
* 다음을 수행할 수 있습니다. [비디오 프로필 처리 작업 진행 상황 모니터링](#monitoring-the-progress-of-an-encoding-job).

## 비디오 프로필 처리 작업 진행 상황 모니터링 {#monitoring-the-progress-of-an-encoding-job}

비디오 프로필 처리 작업의 진행 상황을 시각적으로 모니터링할 수 있도록 처리 표시기(또는 진행률 표시줄)가 표시됩니다.

다음을 볼 수도 있습니다. `error.log` 인코딩 작업의 진행 상황을 모니터링하거나, 인코딩이 완료되었는지 확인하거나, 작업 오류를 확인할 수 있는 파일입니다. 다음 `error.log` 다음에서 찾음: `logs` Experience Manager 인스턴스가 설치된 폴더입니다.

## 폴더에서 비디오 프로필 제거 {#removing-a-video-profile-from-folders}

폴더에서 비디오 프로필을 제거하면 모든 하위 폴더는 자동으로 상위 폴더에서 프로필 제거를 상속합니다. 그러나 폴더 내에서 발생한 모든 파일 처리는 그대로 유지됩니다.

You can remove a video profile from a folder from within the **[!UICONTROL Tools]** menu or if you are in the folder, from the **[!UICONTROL Folder Settings]**. This section describes how to remove video profiles from folders both ways.

### 프로필 사용자 인터페이스를 통해 폴더에서 비디오 프로필 제거 {#removing-video-profiles-from-folders-by-way-of-the-profiles-user-interface}

1. Experience Manager 로고를 선택하고 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]** > **[!UICONTROL 비디오 프로필]**.
1. 폴더 또는 여러 폴더에서 제거할 비디오 프로필을 선택합니다.
1. 선택 **[!UICONTROL 폴더에서 프로필 제거]** 에서 프로필을 제거하는 데 사용할 폴더 또는 여러 폴더를 선택하고 **[!UICONTROL 제거]**.

   이름이 더 이상 폴더 이름 아래에 표시되지 않으므로 비디오 프로필이 더 이상 폴더에 적용되지 않는지 확인할 수 있습니다.

### 속성을 통해 폴더에서 비디오 프로필 제거 {#removing-video-profiles-from-folders-by-way-of-properties}

1. Experience Manager 로고를 선택하고 다음으로 이동 **[!UICONTROL 에셋]** 그런 다음 비디오 프로필을 제거할 폴더로 이동합니다.
1. 폴더에서 확인 표시를 선택한 다음 을 선택합니다 **[!UICONTROL 속성]**.
1. 다음 항목 선택 **[!UICONTROL 비디오 프로필]** 탭하고 선택 **[!UICONTROL 없음]** 드롭다운 메뉴에서 다음을 선택합니다. **[!UICONTROL 저장 및 닫기]**. Folders that have a profile already assigned to it are indicated by the display of the profile&#39;s name directly below the folder name.
