---
title: 비디오 구성 요소 구성
seo-title: Configure the Video component
description: 비디오 구성 요소를 구성하는 방법에 대해 알아봅니다.
seo-description: Learn how to configure the Video Component.
uuid: f4755a13-08ea-4096-a951-46a590f8d766
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: a1efef3c-0e4b-4a17-bcad-e3cc17adbbf7
exl-id: 9c97f99e-d6ef-4817-8b2a-201ab22f2b38
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# 비디오 구성 요소 구성 {#configure-the-video-component}

다음 [비디오 구성 요소](/help/sites-authoring/default-components-foundation.md#video) 사전 정의된 기본 제공(OOTB) 비디오 에셋을 페이지에 배치할 수 있습니다.

적절한 코드 변환 작업을 위해 관리자는 FFmpeg를 별도로 설치합니다. 다음을 참조하십시오 [FFmpeg 설치 및 AEM 구성](#install-ffmpeg). 관리자 [비디오 프로필 구성](#configure-video-profiles) HTML5 요소와 함께 사용됩니다.

>[!CAUTION]
>
>이 기초 구성 요소는 더 이상 사용되지 않습니다. Adobe은 를 활용할 것을 권장합니다. [핵심 구성 요소의 임베디드 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/embed.html) 대신,

>[!CAUTION]
>
>이 구성 요소는 더 이상 프로젝트 수준의 광범위한 사용자 지정 없이는 즉시 사용할 수 없습니다.

## 비디오 프로필 구성 {#configure-video-profiles}

HTML5 요소를 사용하려면 비디오 프로필을 정의합니다. 여기서 선택한 것은 순서대로 사용됩니다. 액세스하려면 다음을 사용하십시오. [디자인 모드](/help/sites-authoring/default-components-designmode.md) (클래식 UI만 해당) **[!UICONTROL 프로필]** 탭:

![chlimage_1-317](assets/chlimage_1-317.png)

이 대화 상자에서 비디오 구성 요소의 디자인과 의 매개 변수를 구성할 수도 있습니다. [!UICONTROL 재생], [!UICONTROL Flash], 및 [!UICONTROL 고급].

## FFmpeg 설치 및 AEM 구성 {#install-ffmpeg}

Video 구성 요소는 비디오 트랜스코딩을 위한 타사 오픈 소스 제품 FFmpeg에 의존합니다. 다운로드 위치: [https://ffmpeg.org/](https://ffmpeg.org/). FFmpeg를 설치한 후 특정 오디오 코덱과 특정 런타임 옵션을 사용하도록 AEM을 구성합니다.

FFmpeg를 설치하려면 **Windows**, 다음 단계를 수행합니다.

1. 컴파일된 바이너리를 다음으로 다운로드 `ffmpeg.zip`.
1. 폴더에 보관 해제.
1. 시스템 환경 변수 설정 `PATH` 대상 &lt;*your-ffmpeg-location*>`\bin`.
1. AEM을 다시 시작합니다.

FFmpeg를 설치하려면 **Mac**, 다음 단계를 수행합니다.

1. 사용 가능한 Xcode 설치 위치 [developer.apple.com/xcode](https://developer.apple.com/xcode/).
1. 다음에서 사용 가능한 설치: [XQuartz](https://www.xquartz.org) 다운로드하려면 [-](https://support.apple.com/en-us/HT201341).
1. 다음에서 사용할 수 있는 MacPort 설치 [www.macports.org](https://www.macports.org/).
1. 콘솔에서 을 실행합니다. `sudo port install ffmpeg` 명령을 실행하고 화면의 지시를 따릅니다. 의 경로가 `FFmpeg` 실행 파일이 `PATH` 시스템 변수입니다.

FFmpeg를 설치하려면 **Mac OS X 10.6**, 미리 컴파일된 버전을 사용하여 다음 단계를 따르십시오.

1. 미리 컴파일된 버전을 다운로드합니다.
1. 아카이브 해제 `/usr/local` 디렉토리.
1. 콘솔에서 을(를) 실행합니다 `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`. 경로를 적절하게 변경합니다.

종료 **AEM 구성**, 다음 단계를 수행합니다.

>[!NOTE]
>
>이러한 단계는 코덱을 추가로 사용자 정의해야 하는 경우에만 필요합니다.

1. 열기 [!UICONTROL CRXDE Lite] 을 클릭합니다. 액세스 [http://localhost:4502/crx/de](http://localhost:4502/crx/de).
2. 다음 항목 선택 `/libs/settings/dam/video/format_aac/jcr:content` 노드 를 만들고 노드 속성이 다음과 같은지 확인합니다.

   * `audioCodec` 은(는) `aac`.
   * `customArgs` 은(는) `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. 구성을 사용자 정의하려면 의에 오버레이를 만듭니다. `/apps/settings/` 노드 및 아래에서 동일한 구조 이동 `/conf/global/settings/` 노드. 에서 편집할 수 없습니다. `/libs` 노드. 예를 들어 를 오버레이 경로로 `/libs/settings/dam/video/fullhd-bp`, 다음 위치에 생성 `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >수정해야 하는 속성뿐만 아니라 전체 프로필 노드를 오버레이하고 편집합니다. 이러한 리소스는 SlingResourceMerger를 통해 확인되지 않습니다.

4. 속성 중 하나를 변경한 경우 **[!UICONTROL 모두 저장]**.

>[!NOTE]
>
>AEM 인스턴스를 업그레이드할 때 기본 OOTB(기본 제공) 워크플로우 모델에 대한 변경 사항은 유지되지 않습니다. Adobe은 수정된 워크플로우 모델을 편집하기 전에 복사하는 것을 권장합니다. 예를 들어 OOTB를 복사합니다 [!UICONTROL DAM 자산 업데이트] 에서 FFmpeg 코드 변환 단계를 편집하기 전에 모델을 만듭니다. [!UICONTROL DAM 자산 업데이트] 모델 을 사용하여 업그레이드 전에 있었던 비디오 프로필 이름을 선택할 수 있습니다. 그런 다음 를 오버레이할 수 있습니다. `/apps` AEM이 OOTB 모델에 대한 사용자 지정 변경 사항을 검색할 수 있도록 해 주는 노드입니다.
