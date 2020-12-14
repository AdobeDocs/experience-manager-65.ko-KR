---
title: 비디오 자산 관리
description: 비디오 에셋을 업로드, 미리 보기, 주석 달기 및  [!DNL Adobe Experience Manager]에 게시할 수 있습니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---


# 비디오 자산 관리 {#manage-video-assets}

비디오 포맷은 조직의 디지털 에셋에서 중요한 역할을 합니다. [!DNL Adobe Experience Manager] 비디오 에셋 제작 후 전체 비디오 라이프사이클을 관리할 수 있는 완벽한 솔루션 및 기능을 제공합니다.

[!DNL Adobe Experience Manager Assets]에서 비디오 에셋을 관리하고 편집하는 방법을 알아봅니다. 비디오 인코딩 및 트랜스코딩(예: FFmpeg 트랜스코딩)은 [!DNL Dynamic Media] 통합을 사용하여 수행할 수 있습니다.

## 비디오 자산 업로드 및 미리 보기 {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 확장명이 MP4인 비디오 에셋에 대한 미리 보기를 생성합니다. 에셋의 형식이 MP4가 아닌 경우 FFmpeg 팩을 설치하여 미리 보기를 생성합니다. FFmpeg는 OGG 및 MP4 유형의 비디오 변환을 만듭니다. [!DNL Assets] 사용자 인터페이스에서 변환을 미리 볼 수 있습니다.

1. 디지털 자산 폴더 또는 하위 폴더에서 디지털 자산을 추가할 위치로 이동합니다.
1. 자산을 업로드하려면 도구 모음에서 **[!UICONTROL 만들기]**&#x200B;를 클릭하고 **[!UICONTROL 파일]**&#x200B;을 선택합니다. 또는 사용자 인터페이스에서 파일을 드래그합니다. 자세한 내용은 [자산](manage-assets.md#uploading-assets) 업로드를 참조하십시오.
1. 카드 보기에서 비디오를 미리 보려면 비디오 자산에서 **[!UICONTROL 재생]** ![재생 옵션](assets/do-not-localize/play.png) 옵션을 클릭합니다. 카드 보기에서만 비디오를 일시 중지하거나 재생할 수 있습니다. 목록 보기에서는 [!UICONTROL 재생] 및 [!UICONTROL 일시 중지] 옵션을 사용할 수 없습니다.

1. 자산 세부 사항 페이지에서 비디오를 미리 보려면 카드에서 **[!UICONTROL 편집]**&#x200B;을 클릭합니다. 비디오가 브라우저의 기본 비디오 플레이어에서 재생됩니다. 비디오를 재생, 일시 정지, 볼륨 조절 및 전체 화면으로 확대/축소할 수 있습니다.

   ![비디오 재생 컨트롤](assets/video-playback-controls.png)

## 2GB {#configuration-to-upload-assets-that-are-larger-than-gb}보다 큰 자산을 업로드하기 위한 구성

기본적으로 [!DNL Assets]에서는 파일 크기 제한으로 인해 2GB보다 큰 에셋을 업로드할 수 없습니다. 그러나 CRXDE Lite으로 이동하여 `/apps` 디렉터리 아래에 노드를 만들면 이 제한을 덮어쓸 수 있습니다. 노드에는 동일한 노드 이름, 디렉토리 구조 및 이와 비교할 수 있는 노드 속성이 있어야 합니다.

[!DNL Assets] 구성 외에도 큰 자산을 업로드하려면 다음 구성을 변경하십시오.

* 토큰 만료 시간을 늘립니다. `https://[aem_server]:[port]/system/console/configMgr`의 웹 콘솔에서 [!UICONTROL Adobe Granite CSRF Servlet]을 참조하십시오. 자세한 내용은 [CSRF 보호](/help/sites-developing/csrf-protection.md)를 참조하십시오.
* Dispatcher 구성에서 `receiveTimeout`을(를) 늘립니다. 자세한 내용은 [Experience Manager 디스패처 구성](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options)을 참조하십시오.

>[!NOTE]
>
>[!DNL Experience Manager] 클래식 사용자 인터페이스에는 2GB 파일 크기 제한이 없습니다. 또한 대형 비디오에 대한 엔드 투 엔드 워크플로우는 완벽하게 지원되지 않습니다.

더 높은 파일 크기 제한을 구성하려면 `/apps` 디렉토리에서 다음 단계를 수행하십시오.

1. [!DNL Experience Manager]에서 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**&#x200B;을 클릭합니다.
1. CRXDE Lite에서 `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`으로 이동합니다. 디렉토리 창을 보려면 `>>`을 클릭합니다.
1. 도구 모음에서 **[!UICONTROL 오버레이 노드]**&#x200B;를 클릭합니다. 또는 컨텍스트 메뉴에서 **[!UICONTROL 오버레이 노드]**&#x200B;를 선택합니다.
1. **[!UICONTROL 오버레이 노드]** 대화 상자에서 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

   ![오버레이 노드](assets/overlay-node-path.png)

1. 브라우저를 새로 고칩니다. 오버레이 노드 `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`이(가) 선택됩니다.
1. **[!UICONTROL 속성]** 탭에서 원하는 크기로 크기 제한을 늘리려면 적절한 값을 바이트 단위로 입력합니다. 예를 들어 크기 제한을 30GB로 늘리려면 `32212254720` 값을 입력합니다.

1. 도구 모음에서 **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.
1. [!DNL Experience Manager]에서 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**&#x200B;을 클릭합니다.
1. [!DNL Adobe Experience Manager] [!UICONTROL 웹 콘솔 번들] 페이지의 테이블의 이름 열에서 **[!UICONTROL Adobe Granite Workflow 외부 프로세스 작업 핸들러]**&#x200B;를 찾아 클릭합니다.
1. [!UICONTROL Adobe Granite Workflow 외부 프로세스 작업 핸들러] 페이지에서 **[!UICONTROL 기본 시간 초과]** 및 **[!UICONTROL 최대 시간 초과`18000`(5시간) 필드 모두에 대한 초를 설정합니다.]** **[!UICONTROL 저장]**&#x200B;을 클릭합니다.
1. [!DNL Experience Manager]에서 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로우]** > **[!UICONTROL 모델]**&#x200B;을 클릭합니다.
1. 워크플로우 모델 페이지에서 **[!UICONTROL Dynamic Media 인코딩 비디오]**&#x200B;을 선택한 다음 **[!UICONTROL 편집]**&#x200B;을 클릭합니다.
1. 워크플로우 페이지에서 **[!UICONTROL Dynamic Media 비디오 서비스 프로세스]** 구성 요소를 두 번 클릭합니다.
1. [!UICONTROL 단계 속성] 대화 상자의 **[!UICONTROL 일반]** 탭에서 **고급 설정**&#x200B;을 확장합니다.
1. **[!UICONTROL 시간 초과]** 필드에서 `18000` 값을 지정한 다음 **[!UICONTROL 확인]**&#x200B;을 클릭하여 **[!UICONTROL Dynamic Media 비디오 인코딩]** 워크플로 페이지로 돌아갑니다.
1. 페이지 위쪽 근처에 있는 [!UICONTROL Dynamic Media 인코딩 비디오] 페이지 제목 아래에서 **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

## 비디오 자산 {#publish-video-assets} 게시

게시 후 웹 페이지에 비디오 자산을 URL로 포함하거나 자산을 직접 포함할 수 있습니다. 자세한 내용은 [Dynamic Media 자산 게시](/help/assets/publishing-dynamicmedia-assets.md)를 참조하십시오.

## 비디오 자산 {#annotate-video-assets}에 주석 추가

1. [!DNL Assets] 콘솔에서 자산 카드의 **[!UICONTROL 편집]**&#x200B;을 선택하여 자산 세부 사항 페이지를 표시합니다.
1. 비디오를 재생하려면 **[!UICONTROL 미리 보기]**&#x200B;를 클릭합니다.
1. 비디오에 주석을 추가하려면 **[!UICONTROL 주석]**&#x200B;을 클릭합니다. 비디오의 특정 시간(프레임)에 주석이 추가됩니다. 주석을 달 때 캔버스에서 그리고 그림에 주석을 추가할 수 있습니다. 주석이 자동으로 저장됩니다. 주석 마법사를 종료하려면 **[!UICONTROL 닫기]**&#x200B;를 클릭합니다.

   ![비디오 프레임에 드로잉 및 주석 추가](assets/annotate-video.png)

1. 비디오의 특정 지점을 찾아서 **text** 필드에 시간을 초 단위로 지정하고 **Jump**&#x200B;을 클릭합니다. 예를 들어 비디오 처음 20초를 건너뛰려면 텍스트 필드에 20을 입력합니다.

   ![비디오에서 지정된 초 단위로 건너뛸 시간을 찾습니다.](assets/seek-in-video.png)

1. 타임라인에서 보려면 주석을 클릭합니다. 타임라인에서 주석을 삭제하려면 **[!UICONTROL 삭제]**&#x200B;를 클릭합니다.

   ![타임라인에서 주석 및 세부 사항 보기](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [Experience Manager 자산에 있는 디지털 자산 관리](/help/assets/manage-assets.md)
>* [Experience Manager 자산의 컬렉션 관리](/help/assets/manage-collections.md)
>* [Dynamic Media 비디오 설명서](/help/assets/video.md).

