---
title: 비디오 자산 관리
description: 비디오 에셋을 업로드, 미리 보기, 주석 달기 및 게시하는 방법에 대해 알아보십시오.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 1%

---


# 비디오 자산 관리 {#manage-video-assets}

Adobe Experience Manager Assets에서 비디오 자산을 관리하고 편집하는 방법을 알아봅니다. 또한 Dynamic Media를 사용할 수 있는 라이센스가 있는 경우 [Dynamic Media 비디오 설명서를 참조하십시오](/help/assets/video.md).

## 비디오 에셋 업로드 및 미리 보기 {#upload-and-preview-video-assets}

Adobe Experience Manager Assets는 익스텐션 MP4를 사용하여 비디오 자산에 대한 미리 보기를 생성합니다. 자산의 형식이 MP4가 아닌 경우 FFmpeg 팩을 설치하여 미리 보기를 생성합니다. FFmpeg는 OGG 및 MP4 유형의 비디오 변환을 만듭니다. 이러한 표현물은 자산 사용자 인터페이스에서 미리 볼 수 있습니다.

1. 디지털 자산 폴더 또는 하위 폴더에서 디지털 자산을 추가할 위치로 이동합니다.
1. 자산을 업로드하려면 도구 모음에서 **[!UICONTROL 만들기를]** 클릭한 다음 **[!UICONTROL 파일을 선택합니다]**. 또는 자산 영역에 직접 놓습니다. 업로드 [작업에 대한 자세한 내용은 자산](managing-assets-touch-ui.md#uploading-assets) 업로드를 참조하십시오.
1. 카드 보기에서 비디오를 미리 보려면 비디오 자산에서 **[!UICONTROL 재생]** 단추를 클릭합니다.

   ![chlimage_1-65](assets/chlimage_1-201.png)

   카드 보기에서만 비디오를 일시 중지하거나 재생할 수 있습니다. [ [!UICONTROL 재생] ] 및 [!UICONTROL [일시 정지] ] 단추는 목록 보기에서 사용할 수 없습니다.

1. 자산 세부 사항 페이지에서 비디오를 미리 보려면 카드에서 **[!UICONTROL 편집]** 아이콘을 클릭합니다.

   비디오가 브라우저의 기본 비디오 플레이어에서 재생됩니다. 비디오를 재생, 일시 정지, 볼륨 조절 및 전체 화면으로 확대/축소할 수 있습니다.

   ![chlimage_1-66](assets/chlimage_1-202.png)

## 2GB보다 큰 자산을 업로드하기 위한 구성 {#configuration-to-upload-assets-that-are-larger-than-gb}

기본적으로 Adobe Experience Manager Assets에서는 파일 크기 제한 때문에 2GB보다 큰 자산을 업로드할 수 없습니다. 그러나 CRXDE Lite로 이동하여 디렉터리 아래에 노드를 만들면 이 제한을 `/apps` 덮어쓸 수 있습니다. 노드에는 동일한 노드 이름, 디렉토리 구조 및 비교 가능한 노드 속성이 있어야 합니다.

Experience Manager Assets 구성 외에도 큰 자산을 업로드하려면 다음 구성을 변경하십시오.

* 토큰 만료 시간을 늘립니다. 웹 [!UICONTROL 콘솔에서] Adobe Granite CSRF Servlet을 참조하십시오 `https://[aem_server]:[port]/system/console/configMgr`. 자세한 내용은 [CSRF 보호를 참조하십시오](/help/sites-developing/csrf-protection.md).
* Dispatcher 구성 `receiveTimeout` 의 크기를 늘립니다. 자세한 내용은 [Experience Manager Dispatcher 구성을 참조하십시오](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options).

>[!NOTE]
>
>Experience Manager Classic 사용자 인터페이스에 2GB 파일 크기 제한이 없습니다. 또한 대형 비디오에 대한 엔드 투 엔드 워크플로우는 완벽하게 지원되지 않습니다.

더 높은 파일 크기 제한을 구성하려면 디렉토리에서 다음 단계를 `/apps` 수행합니다.

1. Adobe Experience Manager에서 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE]** Lite를클릭합니다.
1. CRXDE Lite에서 로 이동합니다 `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. 디렉토리 창을 보려면 아이콘을 `>>` 터치하십시오.
1. 도구 모음에서 **[!UICONTROL 오버레이 노드를 클릭합니다]**. 또는 컨텍스트 메뉴에서 **[!UICONTROL 오버레이 노드]** 를 선택합니다.
1. [ **[!UICONTROL 오버레이 노드]** ] 대화 상자에서 **[!UICONTROL 확인을 클릭합니다]**.

   ![chlimage_1-67](assets/chlimage_1-203.png)

1. 브라우저를 새로 고칩니다. 오버레이 노드가 `/jcr_root/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` 선택되었습니다.
1. 속성 **[!UICONTROL 탭에서]** 적절한 값을 바이트 단위로 입력하여 원하는 크기로 크기 제한을 늘립니다. 예를 들어 크기 제한을 30GB로 늘리려면 `{sizeLimit : "32212254720"}` 값을 입력합니다.

1. 도구 모음에서 모두 **[!UICONTROL 저장을 터치합니다]**.
1. Adobe Experience Manager에서 **[!UICONTROL 도구]** > 작업 **[!UICONTROL >]** 웹 콘솔 **[!UICONTROL 을 클릭합니다]**.
1. Adobe Experience Manager 웹 콘솔 번들 페이지의 테이블의 이름 열에서 **[!UICONTROL Adobe Granite Workflow 외부 프로세스 작업 핸들러를 찾아 클릭합니다]**.
1. [Adobe Granite Workflow 외부 프로세스 작업 처리기] 페이지에서 [ **[!UICONTROL 기본 시간 초과]** 및 **[!UICONTROL 최대 시간 초과]** 필드 `18000` 의 시간(초)을5시간(시간)으로 설정합니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.
1. Adobe Experience Manager에서 **[!UICONTROL 도구]** > 워크플로우 **[!UICONTROL > 모델]** 을 **[!UICONTROL 클릭합니다]**.
1. 워크플로우 모델 페이지에서 **[!UICONTROL 다이내믹 미디어 인코딩 비디오를]**&#x200B;선택한 다음 **[!UICONTROL 편집을 클릭합니다]**.
1. 워크플로우 페이지에서 **[!UICONTROL Dynamic Media 비디오 서비스 프로세스]** 구성 요소를 두 번 클릭합니다.
1. 단계 [!UICONTROL 속성] 대화 상자의 **[!UICONTROL 공통]** 탭 아래에서 **고급**&#x200B;설정을확장합니다.
1. 시간 **[!UICONTROL 초과]** 필드 `18000`에서 값 **[!UICONTROL 을 지정한 다음]** 확인을 **[!UICONTROL 클릭하여]** Dynamic Media Encode 비디오워크플로 페이지로 돌아갑니다.
1. 페이지 상단의 Dynamic Media 인코딩 비디오 페이지 제목 아래에서 **[!UICONTROL 저장을 클릭합니다]**.

## 비디오 에셋 게시 {#publish-video-assets}

비디오 에셋이 게시된 후에는 URL을 통해 웹 페이지에 포함하거나 웹 페이지에 포함되도록 할 수 있습니다. 자산 [게시를 참조하십시오](/help/assets/publishing-dynamicmedia-assets.md).

## 비디오 자산에 주석 달기 {#annotate-video-assets}

1. 자산 콘솔에서 자산 카드의 [!UICONTROL 편집] 아이콘을 클릭하여 자산 세부 사항 페이지를 표시합니다.
1. 비디오를 재생하려면 미리 보기 [!UICONTROL 아이콘을] 클릭합니다.
1. 비디오에 주석을 추가하려면 [주석] **[!UICONTROL 단추를]** 클릭합니다. 비디오의 특정 시간(프레임)에 주석이 추가됩니다. 주석을 달 때 캔버스에서 드로잉하고 드로잉에 주석을 추가할 수 있습니다. 주석이 자동으로 저장됩니다.

   ![chlimage_1-68](assets/chlimage_1-204.png)

   주석 마법사를 종료하려면 **[!UICONTROL 닫기를 클릭합니다]**.

1. 비디오의 특정 지점을 찾아서 **텍스트** 필드(초)에서 시간을 지정하고 **이동을 클릭합니다**. 예를 들어 비디오의 처음 10초를 건너뛰려면 텍스트 필드에 20을 입력합니다.

   ![chlimage_1-69](assets/chlimage_1-205.png)

1. 타임라인에서 보려면 주석을 클릭합니다. 타임라인에서 주석을 삭제하려면 삭제 **[!UICONTROL 를 클릭합니다]**.

   ![chlimage_1-70](assets/chlimage_1-206.png)
