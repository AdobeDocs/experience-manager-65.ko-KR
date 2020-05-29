---
title: 비디오 구성 요소 구성
seo-title: 비디오 구성 요소 구성
description: 비디오 구성 요소를 구성하는 방법을 알아봅니다.
seo-description: 비디오 구성 요소를 구성하는 방법을 알아봅니다.
uuid: f4755a13-08ea-4096-a951-46a590f8d766
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: a1efef3c-0e4b-4a17-bcad-e3cc17adbbf7
translation-type: tm+mt
source-git-commit: 44dbabeeea4e4e8d17cc69a2d8ea791c98be2bd2
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 6%

---


# 비디오 구성 요소 구성 {#configure-the-video-component}

비디오 구성 요소 [](/help/sites-authoring/default-components-foundation.md#video) 를 사용하면 사전 정의된 OOTB(기본 제공) 비디오 요소를 페이지에 배치할 수 있습니다.

변환이 올바르게 수행되려면 관리자가 FFmpeg를 [설치하고 AEM을](#install-ffmpeg) 별도로 구성해야 합니다. HTML5 요소와 함께 사용하도록 [비디오 프로필을 구성](#configure-video-profiles)할 수도 있습니다.

## 비디오 프로필 구성 {#configure-video-profiles}

HTML5 요소에 사용할 비디오 프로필을 정의할 수도 있습니다. 여기서 선택한 것들은 순서대로 사용됩니다. 액세스하려면 [디자인 모드](/help/sites-authoring/default-components-designmode.md) (클래식 UI만 해당)를 사용하고 **[!UICONTROL 프로필]** 탭을 선택합니다.

![chlimage_1-317](assets/chlimage_1-317.png)

또한 비디오 구성 요소 및 [!UICONTROL 재생], [!UICONTROL Flash]및 [!UICONTROL 고급 매개 변수의 디자인을 구성할 수]있습니다.

## FFmpeg 설치 및 AEM 구성 {#install-ffmpeg}

The Video Component relies on the third-party open-source product FFmpeg for proper transcoding of videos that can be downloaded from [https://ffmpeg.org/](https://ffmpeg.org/). FFmpeg를 설치한 후에는 특정 오디오 코덱과 특정 런타임 옵션을 사용하도록 AEM을 구성해야 합니다.

**플랫폼용 FFmpeg를 설치하려면**:

* **Windows:**

   1. 컴파일된 바이너리를 `ffmpeg.zip`
   1. 폴더의 압축을 해제합니다.
   1. 시스템 환경 변수 `PATH` 를 `<*your-ffmpeg-locatio*n>\bin`
   1. AEM을 다시 시작합니다.

* **Mac OS X:**

   1. Xcode 설치([https://developer.apple.com/technologies/tools/xcode.html](https://developer.apple.com/technologies/tools/xcode.html))
   1. XQuartz/X11을 설치합니다.
   1. MacPorts 설치([https://www.macports.org/](https://www.macports.org/))
   1. 콘솔에서 다음 명령을 실행하고 지침을 따릅니다.

      `sudo port install ffmpeg`

      `FFmpeg` AEM에서 명령줄을 통해 인식할 수 `PATH` 있도록 설정되어 있어야 합니다.

* **OS X 10.6용 사전 컴파일 버전 사용:**

   1. 미리 컴파일된 버전을 다운로드합니다.
   1. Extract it to the `/usr/local` directory.
   1. 터미널에서 다음을 실행합니다.

      `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`

**AEM을 구성하려면**:

>[!NOTE]
>
>이러한 단계는 코덱을 추가로 사용자 정의해야 하는 경우에만 필요합니다.

1. Open [!UICONTROL CRXDE Lite] in your web browser. ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))
2. 노드를 `/libs/settings/dam/video/format_aac/jcr:content` 선택하고 노드 속성이 다음과 같은지 확인합니다.

   * audioCodec:

      ```
       aac
      ```

   * customArgs:

      ```
       -flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8
      ```

3. 구성을 사용자 정의하려면 노드에서 오버레이를 만들고 노드 아래에 `/apps/settings/` 동일한 구조를 `/conf/global/settings/` 이동합니다. 노드에서 편집할 수 `/libs` 없습니다. 예를 들어 경로를 오버레이하려면 `/libs/settings/dam/video/fullhd-bp`에서 만듭니다 `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >수정이 필요한 속성뿐만 아니라 전체 프로필 노드를 오버레이하고 편집합니다. 이러한 리소스는 SlingResourceCombination을 통해 해결되지 않습니다.

4. If you changed either of the properties, click **[!UICONTROL Save All]**.

>[!NOTE]
>
>AEM 인스턴스를 업그레이드할 때 OOTB 워크플로우 모델은 유지되지 않습니다. OOTB 워크플로우 모델을 편집하기 전에 복사하는 것이 좋습니다. 예를 들어 [!UICONTROL DAM 자산] 업데이트 모델의 FFmpeg 트랜스코딩 단계를 편집하기 전에 OOTB [!UICONTROL DAM 자산] 업데이트 모델을 복사하여 업그레이드 전에 존재했던 비디오 프로필 이름을 선택합니다. 그런 다음 AEM이 OOTB 모델에 대한 사용자 지정 변경 사항을 검색할 수 있도록 노드를 `/apps` 오버레이할 수 있습니다.

