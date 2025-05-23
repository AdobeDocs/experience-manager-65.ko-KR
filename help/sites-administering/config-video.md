---
title: 비디오 구성 요소 구성
description: Adobe Experience Manager의 비디오 구성 요소를 사용하여 사전 정의된 기본 비디오 에셋을 페이지에 배치하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 9c97f99e-d6ef-4817-8b2a-201ab22f2b38
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---

# 비디오 구성 요소 구성 {#configure-the-video-component}

[비디오 구성 요소](/help/sites-authoring/default-components-foundation.md#video)를 사용하면 미리 정의된 기본 비디오 자산을 페이지에 배치할 수 있습니다.

적절한 코드 변환이 일어나도록 관리자가 FFmpeg를 별도로 설치합니다. [FFmpeg 설치 및 AEM 구성](#install-ffmpeg)을 참조하십시오. 관리자는 또한 [비디오 프로필을 구성](#configure-video-profiles)하여 HTML5 요소와 함께 사용할 수 있습니다.

>[!CAUTION]
>
>이 기초 구성 요소는 더 이상 사용되지 않습니다. Adobe은 대신 [핵심 구성 요소 임베드 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/embed.html?lang=ko)를 사용할 것을 권장합니다.

>[!CAUTION]
>
>이 구성 요소는 더 이상 프로젝트 수준의 광범위한 사용자 지정 없이는 즉시 사용할 수 없습니다.

## 비디오 프로필 구성 {#configure-video-profiles}

HTML5 요소를 사용하려면 비디오 프로필을 정의합니다. 여기서 선택한 것은 순서대로 사용됩니다. 액세스하려면 [디자인 모드](/help/sites-authoring/default-components-designmode.md)(클래식 UI만 해당)를 사용하고 **[!UICONTROL 프로필]** 탭을 선택하십시오.

![chlimage_1-317](assets/chlimage_1-317.png)

이 대화 상자에서 [!UICONTROL 재생], [!UICONTROL Flash] 및 [!UICONTROL 고급]에 대한 비디오 구성 요소와 매개 변수의 디자인을 구성할 수도 있습니다.

## FFmpeg 설치 및 AEM 구성 {#install-ffmpeg}

Video 구성 요소는 비디오 트랜스코딩을 위한 타사 오픈 소스 제품 FFmpeg에 의존합니다. [https://ffmpeg.org/](https://ffmpeg.org/)에서 다운로드했습니다. FFmpeg를 설치한 후 특정 오디오 코덱과 특정 런타임 옵션을 사용하도록 AEM을 구성합니다.

**Windows**&#x200B;에서 FFmpeg를 설치하려면 다음 단계를 수행하십시오.

1. 컴파일된 바이너리를 `ffmpeg.zip`(으)로 다운로드합니다.
1. 폴더에 보관 해제.
1. 시스템 환경 변수 `PATH`을(를) &lt;*your-ffmpeg-location*>`\bin`(으)로 설정합니다.
1. AEM을 다시 시작합니다.

**macOS X**&#x200B;에 FFmpeg를 설치하려면 다음 단계를 수행하십시오.

1. [developer.apple.com/xcode](https://developer.apple.com/xcode/)에서 사용할 수 있는 Xcode를 설치하십시오.
1. [X11](https://support.apple.com/en-us/100724)을(를) 가져오려면 [XQuartz](https://www.xquartz.org)에서 사용할 수 있는 설치를 설치하십시오.
1. [www.macports.org](https://www.macports.org/)에서 사용할 수 있는 MacPorts를 설치하십시오.
1. 콘솔에서 `sudo port install ffmpeg` 명령을 실행하고 화면에 표시되는 안내를 따릅니다. `FFmpeg` 실행 파일의 경로가 `PATH` 시스템 변수에 추가되었는지 확인하십시오.

미리 컴파일된 버전을 사용하여 **macOS X 10.6**&#x200B;에 FFmpeg를 설치하려면 다음 단계를 따르십시오.

1. 미리 컴파일된 버전을 다운로드합니다.
1. `/usr/local` 디렉터리에 보관을 해제하십시오.
1. 콘솔에서 `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`을(를) 실행합니다. 경로를 적절하게 변경합니다.

**AEM을 구성**&#x200B;하려면 다음 단계를 따르십시오.

>[!NOTE]
>
>이러한 단계는 코덱을 추가로 사용자 정의해야 하는 경우에만 필요합니다.

1. 웹 브라우저에서 [!UICONTROL CRXDE Lite]을 엽니다. [http://localhost:4502/crx/de](http://localhost:4502/crx/de)에 액세스합니다.
2. `/libs/settings/dam/video/format_aac/jcr:content` 노드를 선택하고 노드 속성이 다음과 같은지 확인하십시오.

   * `audioCodec`은(는) `aac`입니다.
   * `customArgs`은(는) `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`입니다.

3. 구성을 사용자 지정하려면 `/apps/settings/` 노드에 오버레이를 만들고 `/conf/global/settings/` 노드 아래에서 동일한 구조를 이동합니다. `/libs` 노드에서 편집할 수 없습니다. 예를 들어 오버레이 경로 `/libs/settings/dam/video/fullhd-bp`을(를) 만들려면 `/conf/global/settings/dam/video/fullhd-bp`에 경로를 만드십시오.

   >[!NOTE]
   >
   >수정해야 하는 속성뿐만 아니라 전체 프로필 노드를 오버레이하고 편집합니다. 이러한 리소스는 SlingResourceMerger를 통해 확인되지 않습니다.

4. 속성을 변경한 경우 **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

>[!NOTE]
>
>AEM 인스턴스를 업그레이드할 때 기본 기본 워크플로우 모델에 대한 변경 사항은 유지되지 않습니다. Adobe은 수정된 워크플로우 모델을 편집하기 전에 복사하는 것을 권장합니다. 예를 들어 [!UICONTROL DAM 자산 업데이트] 모델에서 FFmpeg 코드 변환 단계를 편집하기 전에 기본 제공 [!UICONTROL DAM 자산 업데이트] 모델을 복사하여 업그레이드 전에 있었던 비디오 프로필 이름을 선택합니다. 그런 다음 `/apps` 노드를 오버레이하여 AEM에서 기본 제공 모델에 대한 사용자 지정 변경 사항을 검색할 수 있도록 할 수 있습니다.
