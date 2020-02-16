---
title: 비디오 자산 관리
description: 비디오 에셋을 업로드, 미리 보기, 주석 달기 및 게시하는 방법에 대해 알아봅니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# 비디오 자산 관리 {#manage-video-assets}

AEM(Adobe Experience Manager) 자산에서 비디오 자산을 관리하고 편집하는 방법을 알아봅니다. 또한 Dynamic Media 사용 허가를 받은 경우 Dynamic Media [비디오 설명서를](/help/assets/video.md)참조하십시오.

## 비디오 에셋 업로드 및 미리 보기 {#upload-and-preview-video-assets}

Adobe Experience Manager Assets는 익스텐션 MP4를 사용하여 비디오 자산에 대한 미리 보기를 생성합니다. 자산의 형식이 MP4가 아닌 경우 FFmpeg 팩을 설치하여 미리 보기를 생성합니다. FFmpeg는 OGG 및 MP4 유형의 비디오 변환을 만듭니다. AEM 자산 사용자 인터페이스에서 이러한 변환을 미리 볼 수 있습니다.

1. 디지털 자산 폴더 또는 하위 폴더에서 디지털 자산을 추가할 위치로 이동합니다.
1. 자산을 업로드하려면 도구 모음에서 **[!UICONTROL 만들기를]** 클릭하거나 탭한 다음 파일을 **[!UICONTROL 선택합니다]**. 또는 자산 영역에 직접 놓습니다. 업로드 [작업에 대한 자세한 내용은 자산](managing-assets-touch-ui.md#uploading-assets) 업로드를 참조하십시오.
1. 카드 보기에서 비디오를 미리 보려면 비디오 **[!UICONTROL 자산에서]** 재생 단추를 누릅니다.

   ![chlimage_1-65](assets/chlimage_1-201.png)

   카드 보기에서만 비디오를 일시 중지하거나 재생할 수 있습니다. 목록 [!UICONTROL 보기에서는] [재생  및 [일시 중지] ] 단추를 사용할 수 없습니다.

1. 자산 세부 사항 페이지에서 비디오를 미리 보려면 카드에서 **[!UICONTROL 편집]** 아이콘을 클릭하거나 탭합니다.

   비디오가 브라우저의 기본 비디오 플레이어에서 재생됩니다. 비디오를 재생, 일시 중지, 볼륨 조절 및 전체 화면으로 확대/축소할 수 있습니다.

   ![chlimage_1-66](assets/chlimage_1-202.png)

## 2GB보다 큰 자산을 업로드하기 위한 구성 {#configuration-to-upload-assets-that-are-larger-than-gb}

기본적으로 Experience Manager Assets에서는 파일 크기 제한 때문에 2GB보다 큰 자산을 업로드할 수 없습니다. 그러나 CRXDE Lite로 이동하여 `/apps` 디렉토리 아래에 노드를 만들면 이 제한을 덮어쓸 수 있습니다. 노드에는 동일한 노드 이름, 디렉토리 구조 및 이와 비교할 수 있는 노드 속성이 있어야 합니다.

Experience Manager Assets 구성 외에 다음 구성을 변경하여 큰 자산을 업로드하십시오.

* 토큰 만료 시간을 늘립니다. 웹 [!UICONTROL 콘솔에서 Adobe Granite] CSRF Servlet을 참조하십시오 `https://[aem_server]:[port]/system/console/configMgr`. 자세한 내용은 CSRF [보호를](/help/sites-developing/csrf-protection.md)참조하십시오.
* Dispatcher `receiveTimeout` 구성에서 을 늘립니다. 자세한 내용은 Experience Manager [Dispatcher 구성을](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options)참조하십시오.

>[!NOTE]
>
>AEM Classic 사용자 인터페이스에 2GB 파일 크기 제한이 없습니다. 또한 대형 비디오에 대한 전체 워크플로우는 완벽하게 지원되지 않습니다.

더 높은 파일 크기 제한을 구성하려면 `/apps` 디렉토리에서 다음 단계를 수행하십시오.

1. AEM에서 도구 > **[!UICONTROL 일반]** **[!UICONTROL >]** CRXDE **[!UICONTROL Lite를]**&#x200B;누릅니다.
1. CRXDE Lite에서 로 `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`이동합니다. 디렉토리 창을 보려면 `>>` 아이콘을 터치하십시오.
1. 도구 모음에서 Overlay Node를 **[!UICONTROL 누릅니다]**. 또는 컨텍스트 **[!UICONTROL 메뉴에서]** 오버레이 노드를 선택합니다.
1. [오버레이 **[!UICONTROL 노드]** ] 대화 상자에서 확인을 **[!UICONTROL 누릅니다]**.

   ![chlimage_1-67](assets/chlimage_1-203.png)

1. 브라우저를 새로 고칩니다. 오버레이 노드가 `/jcr_root/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` 선택됩니다.
1. 속성 **[!UICONTROL 탭에서]** 적절한 값을 바이트 단위로 입력하여 원하는 크기로 크기 제한을 늘립니다. 예를 들어 크기 제한을 30GB로 늘리려면 `{sizeLimit : "32212254720"}` 값을 입력합니다.

1. 도구 모음에서 모두 **[!UICONTROL 저장을 터치합니다]**.
1. AEM에서 도구 > **[!UICONTROL 작업]** **[!UICONTROL >]** 웹 **[!UICONTROL 콘솔을]**&#x200B;누릅니다.
1. Adobe Experience Manager 웹 콘솔 번들 페이지의 테이블의 이름 열에서 Adobe Granite Workflow 외부 프로세스 **[!UICONTROL 작업 핸들러를 찾아 탭합니다]**.
1. Adobe [Granite Workflow 외부 프로세스 작업 처리기] 페이지에서 [기본 시간 초과] 및 [ **[!UICONTROL 최대 시간 초과]** ] **[!UICONTROL 필드의]** 시간 `18000` (5시간)을 설정합니다.
1. 저장을 **[!UICONTROL 누릅니다]**.
1. AEM에서 도구 > **[!UICONTROL 워크플로우]** > **[!UICONTROL 모델을]** 탭 **[!UICONTROL 합니다]**.
1. 워크플로우 모델 페이지에서 다이내믹 미디어 인코딩 **[!UICONTROL 비디오를]**&#x200B;선택한 다음 편집을 **[!UICONTROL 누릅니다]**.
1. 워크플로우 페이지에서 Dynamic Media 비디오 서비스 **[!UICONTROL 프로세스 구성 요소를 두 번]** 누릅니다.
1. [ [!UICONTROL 단계 속성] ] 대화 상자의 [공용] **[!UICONTROL 탭에서]** [고급 **설정]을**&#x200B;확장합니다.
1. 시간 **[!UICONTROL 초과]** 필드에서 값을 `18000`지정한 다음 확인을 탭하여 **[!UICONTROL Dynamic Media]** 비디오 인코딩 **[!UICONTROL 워크플로우 페이지로]** 돌아갑니다.
1. 페이지 상단의 Dynamic Media 인코딩 비디오 페이지 제목 아래에 있는 저장을 **[!UICONTROL 탭합니다]**.

## 비디오 에셋 게시 {#publish-video-assets}

비디오 에셋이 게시되면 URL을 통해 웹 페이지에 포함하거나 웹 페이지에 임베드할 수 있습니다. 자산 [게시를](/help/assets/publishing-dynamicmedia-assets.md)참조하십시오.

## 비디오 자산에 주석 추가 {#annotate-video-assets}

1. 자산 콘솔에서 자산 카드의 [!UICONTROL 편집] 아이콘을 클릭하거나 탭하여 자산 세부 사항 페이지를 표시합니다.
1. 비디오를 재생하려면 미리 보기 [!UICONTROL 아이콘을 클릭하거나 탭합니다] .
1. 비디오에 주석을 달려면 [주석] **[!UICONTROL 단추를]** 클릭합니다. 비디오의 특정 시간(프레임)에 주석이 추가됩니다. 주석을 달 때 캔버스에서 드로잉하고 드로잉에 주석을 포함할 수 있습니다. 주석이 자동으로 저장됩니다.

   ![chlimage_1-68](assets/chlimage_1-204.png)

   주석 마법사를 종료하려면 닫기를 **[!UICONTROL 클릭합니다]**.

1. 비디오의 특정 지점으로 이동하여 **텍스트** 필드에서 시간(초)을 지정하고 이동을 **클릭합니다**. 예를 들어 비디오 처음 10초를 건너뛰려면 텍스트 필드에 20을 입력합니다.

   ![chlimage_1-69](assets/chlimage_1-205.png)

1. 타임라인에서 보려면 주석을 클릭합니다. 타임라인에서 주석을 삭제하려면 삭제를 **[!UICONTROL 클릭합니다]**.

   ![chlimage_1-70](assets/chlimage_1-206.png)
