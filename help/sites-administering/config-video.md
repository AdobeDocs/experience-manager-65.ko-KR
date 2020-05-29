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
source-git-commit: 071f4a292343f0ad52ca3700c95bf60f03c307cc
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# 비디오 구성 요소 구성 {#configure-the-video-component}

비디오 구성 요소 [](/help/sites-authoring/default-components-foundation.md#video) 를 사용하면 사전 정의된 특별(OOTB) 비디오 자산을 페이지에 배치할 수 있습니다.

변환이 올바르게 수행되려면 관리자가 FFmpeg를 별도로 설치합니다. FFmpeg [설치 및 AEM 구성을 참조하십시오](#install-ffmpeg). Administrators also [Configure Video Profiles](#configure-video-profiles) for use with HTML5 elements.

## 비디오 프로필 구성 {#configure-video-profiles}

HTML5 요소를 사용하려면 비디오 프로필을 정의합니다. 여기서 선택한 것들은 순서대로 사용됩니다. 액세스하려면 [디자인 모드](/help/sites-authoring/default-components-designmode.md) (클래식 UI만 해당)를 사용하고 **[!UICONTROL 프로필]** 탭을 선택합니다.

![chlimage_1-317](assets/chlimage_1-317.png)

이 대화 상자에서 비디오 구성 요소의 디자인 및 [!UICONTROL 재생], [!UICONTROL Flash]및 [!UICONTROL 고급 매개 변수]를 구성할 수도있습니다.

## FFmpeg 설치 및 AEM 구성 {#install-ffmpeg}

비디오 구성 요소는 비디오 트랜스코딩에 타사 오픈 소스 제품 FFmpeg를 사용합니다. https://ffmpeg.org/에서 [다운로드하십시오](https://ffmpeg.org/). FFmpeg를 설치한 후 특정 오디오 코덱과 특정 런타임 옵션을 사용하도록 AEM을 구성합니다.

Windows에 FFmpeg를 **설치하려면 다음**&#x200B;단계를 수행하십시오.

1. 컴파일된 바이너리를 다른 이름으로 다운로드합니다 `ffmpeg.zip`.
1. 폴더에 보관하지 않습니다.
1. 시스템 환경 변수 `PATH` 를 &lt;*your-ffmpeg-location*>으로 설정합니다`\bin`.
1. AEM을 다시 시작합니다.

Mac OS **X에 FFmpeg를**&#x200B;설치하려면 다음 단계를 수행하십시오.

1. developer.apple.com/xcode에서 Xcode를 [설치합니다](hhttps://developer.apple.com/xcode/).
1. XQuartz에 [설치할](https://www.xquartz.org) 수 있으므로 [X11을 이용할 수 있습니다](https://support.apple.com/en-us/HT201341).
1. www.macports.org에서 MacPorts를 [설치합니다](https://www.macports.org/).
1. 콘솔에서 실행 `sudo port install ffmpeg` 명령을 수행하고 화면 상의 지침을 따릅니다. 실행 파일의 경로가 시스템 변수에 `FFmpeg` 추가되어 있는지 `PATH` 확인합니다.

미리 컴파일된 버전을 사용하여 **Mac OS X 10.6에** FFmpeg를 설치하려면 다음 단계를 수행하십시오.

1. 미리 컴파일된 버전을 다운로드합니다.
1. 디렉토리에 보관하지 `/usr/local` 않습니다.
1. 콘솔에서 실행을 참조하십시오 `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`. 경로를 적절하게 변경합니다.

AEM을 **구성하려면**&#x200B;다음 단계를 따르십시오.

>[!NOTE]
>
>이러한 단계는 코덱을 추가로 사용자 정의해야 하는 경우에만 필요합니다.

1. Open [!UICONTROL CRXDE Lite] in your web browser. http://localhost:4502/crx/de [에 액세스합니다](http://localhost:4502/crx/de).
2. 노드를 `/libs/settings/dam/video/format_aac/jcr:content` 선택하고 노드 속성이 다음과 같은지 확인합니다.

   * `audioCodec` 은(는) `aac`으로 설정되어 있습니다.
   * `customArgs` 은(는) `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`으로 설정되어 있습니다.

3. 구성을 사용자 정의하려면 노드에서 오버레이를 만들고 노드 아래에 `/apps/settings/` 동일한 구조를 `/conf/global/settings/` 이동합니다. 노드에서 편집할 수 `/libs` 없습니다. 예를 들어 경로를 오버레이하려면 `/libs/settings/dam/video/fullhd-bp`에서 만듭니다 `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >수정이 필요한 속성뿐만 아니라 전체 프로필 노드를 오버레이하고 편집합니다. 이러한 리소스는 SlingResourceCombination을 통해 해결되지 않습니다.

4. If you changed either of the properties, click **[!UICONTROL Save All]**.

>[!NOTE]
>
>AEM 인스턴스를 업그레이드할 때 기본 기본 OOTB(기본 특별) 워크플로우 모델에 대한 변경 사항은 유지되지 않습니다. 수정된 워크플로우 모델을 편집하기 전에 복사하는 것이 좋습니다. 예를 들어 [!UICONTROL DAM 자산] 업데이트 모델의 FFmpeg 트랜스코딩 단계를 편집하기 전에 OOTB [!UICONTROL DAM 자산] 업데이트 모델을 복사하여 업그레이드 전에 존재했던 비디오 프로필 이름을 선택합니다. 그런 다음 AEM이 OOTB 모델에 대한 사용자 지정 변경 사항을 검색할 수 있도록 노드를 `/apps` 오버레이할 수 있습니다.
