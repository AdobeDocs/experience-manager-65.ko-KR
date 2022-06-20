---
title: 비디오 에셋 관리
description: 에서 비디오 자산 업로드, 미리 보기, 주석 달기 및 게시 [!DNL Adobe Experience Manager].
contentOwner: AG
role: User
feature: Asset Management
exl-id: 21d3e0bd-5955-470a-8ca2-4d995c17eb4c
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 8%

---

# 비디오 에셋 관리 {#manage-video-assets}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-video-assets.html?lang=en) |
| AEM 6.5 | 이 문서 |
| AEM 6.4 | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/managing-video-assets.html?lang=en) |

비디오 형식은 조직의 디지털 자산에 중요한 부분입니다. [!DNL Adobe Experience Manager] 에서는 비디오 자산이 만들어진 후 비디오 자산의 전체 라이프사이클을 관리하기 위한 성숙한 오퍼링과 기능을 제공합니다.

에서 비디오 자산을 관리하고 편집하는 방법을 알아봅니다 [!DNL Adobe Experience Manager Assets]. 예를 들어, FFmpeg 코드 변환 코딩 등의 비디오 인코딩과 코드 변환이 [!DNL Dynamic Media] 통합.

## 비디오 자산 업로드 및 미리 보기 {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 에서는 확장 MP4를 사용하여 비디오 자산에 대한 미리 보기를 생성합니다. 자산의 형식이 MP4가 아닌 경우, FFmpeg 팩을 설치하여 미리 보기를 생성합니다. FFmpeg는 OGG 및 MP4 유형의 비디오 표현물을 만듭니다. 에서 표현물을 미리 볼 수 있습니다 [!DNL Assets] 사용자 인터페이스.

1. 디지털 자산 폴더 또는 하위 폴더에서 디지털 자산을 추가할 위치로 이동합니다.
1. 자산을 업로드하려면 **[!UICONTROL 만들기]** 도구 모음에서 **[!UICONTROL 파일]**. 또는 사용자 인터페이스에서 파일을 드래그합니다. 자세한 내용은 [자산 업로드](manage-assets.md#uploading-assets) 자세한 내용
1. 카드 보기에서 비디오를 미리 보려면 **[!UICONTROL 재생]** ![재생 옵션](assets/do-not-localize/play.png) 옵션 을 클릭합니다. 카드 보기에서만 비디오를 일시 중지하거나 재생할 수 있습니다. 다음 [!UICONTROL 재생] 및 [!UICONTROL 일시 정지] 목록 보기에서는 옵션을 사용할 수 없습니다.

1. 자산 세부 사항 페이지에서 비디오를 미리 보려면 **[!UICONTROL 편집]** 카드 위에 비디오는 브라우저의 기본 비디오 플레이어에서 재생됩니다. 비디오를 전체 화면으로 재생, 일시 정지, 볼륨 제어 및 확대/축소할 수 있습니다.

   ![비디오 재생 제어](assets/video-playback-controls.png)

## 2GB보다 큰 자산을 업로드하도록 구성 {#configuration-to-upload-assets-that-are-larger-than-gb}

기본적으로 [!DNL Assets] 에서는 파일 크기 제한으로 인해 2GB보다 큰 자산을 업로드할 수 없습니다. 그러나 CRXDE Lite으로 이동하여 아래에 노드를 만들어 이 제한을 덮어쓸 수 있습니다 `/apps` 디렉토리. 노드에는 동일한 노드 이름, 디렉토리 구조 및 이와 비교할 수 있는 노드 속성이 있어야 합니다.

추가 [!DNL Assets] 구성, 다음 구성을 변경하여 큰 자산을 업로드하십시오.

* 토큰 만료 시간을 늘립니다. 자세한 내용은 [!UICONTROL Adobe Granite CSRF 서블릿] 웹 콘솔에서 `https://[aem_server]:[port]/system/console/configMgr`. 자세한 내용은 [CSRF 보호](/help/sites-developing/csrf-protection.md).
* 를 늘립니다 `receiveTimeout` 참조하십시오. 자세한 내용은 [Experience Manager Dispatcher 구성](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options).

>[!NOTE]
>
>다음 [!DNL Experience Manager] 클래식 사용자 인터페이스에는 2GB 파일 크기 제한이 없습니다. 또한 큰 비디오에 대한 종단 간 워크플로우는 완전히 지원되지 않습니다.

더 높은 파일 크기 제한을 구성하려면 `/apps` 디렉토리.

1. in [!DNL Experience Manager]를 클릭합니다. **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**.
1. CRXDE Lite에서 `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. 디렉토리 창을 보려면 `>>`.
1. 도구 모음에서 **[!UICONTROL 오버레이 노드]**. Alternatively, select **[!UICONTROL Overlay Node]** from the context menu.
1. 에서 **[!UICONTROL 오버레이 노드]** 대화 상자 **[!UICONTROL 확인]**.

   ![오버레이 노드](assets/overlay-node-path.png)

1. 브라우저를 새로 고칩니다. 오버레이 노드 `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` 이 선택되어 있습니다.
1. 에서 **[!UICONTROL 속성]** 탭에서 적절한 값(바이트)을 입력하여 크기 제한을 원하는 크기로 늘립니다. 예를 들어 크기 제한을 30GB로 늘리려면 를 입력합니다. `32212254720` 값.

1. 도구 모음에서 **[!UICONTROL 모두 저장]**.
1. in [!DNL Experience Manager]를 클릭합니다. **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**.
1. 설정 [!DNL Adobe Experience Manager] [!UICONTROL 웹 콘솔 번들] 페이지의 테이블의 이름 열 아래에서 를 찾은 다음 **[!UICONTROL Adobe Granite Workflow 외부 프로세스 작업 처리기]**.
1. 설정 [!UICONTROL Adobe Granite Workflow 외부 프로세스 작업 처리기] 페이지에서 두 시간 모두에 대한 초 수를 설정합니다. **[!UICONTROL 기본 시간 초과]** 및 **[!UICONTROL 최대 시간 초과]** 필드 대상 `18000` (5시간). **[!UICONTROL 저장]**&#x200B;을 클릭합니다.
1. in [!DNL Experience Manager]를 클릭합니다. **[!UICONTROL 도구]** > **[!UICONTROL 워크플로우]** > **[!UICONTROL 모델]**.
1. 워크플로우 모델 페이지에서 을 선택합니다 **[!UICONTROL Dynamic Media 인코딩 비디오]**&#x200B;를 클릭한 다음 **[!UICONTROL 편집]**.
1. 워크플로우 페이지에서 **[!UICONTROL Dynamic Media 비디오 서비스 프로세스]** 구성 요소.
1. In the [!UICONTROL Step Properties] dialog box, under the **[!UICONTROL Common]** tab, expand **Advanced Settings**.
1. 에서 **[!UICONTROL 시간 초과]** 필드, 값 지정 `18000`를 클릭한 다음 **[!UICONTROL 확인]** 로 돌아가기 **[!UICONTROL Dynamic Media 인코딩 비디오]** 워크플로우 페이지.
1. 페이지 상단 근처에 있는 [!UICONTROL Dynamic Media 인코딩 비디오] 페이지 제목 **[!UICONTROL 저장]**.

## 비디오 자산 게시 {#publish-video-assets}

게시 후 비디오 자산을 웹 페이지에 URL로 포함하거나 자산을 직접 포함할 수 있습니다. 자세한 내용은 [Dynamic Media 자산 게시](/help/assets/publishing-dynamicmedia-assets.md).

## 비디오 자산에 주석 달기 {#annotate-video-assets}

1. 에서 [!DNL Assets] 콘솔, 선택 **[!UICONTROL 편집]** 자산 카드의 자산 세부 사항 페이지를 표시합니다.
1. 비디오를 재생하려면 **[!UICONTROL 미리 보기]**.
1. 비디오에 주석을 달려면 **[!UICONTROL 주석 달기]**. 비디오에서 특정 시간(프레임)에 주석이 추가됩니다. 캔버스에 주석을 달 때 그림을 그리고 드로잉에 주석을 포함할 수 있습니다. 주석이 자동으로 저장됩니다. 주석 마법사를 종료하려면 **[!UICONTROL 닫기]**.

   ![비디오 프레임에 그리기 및 주석 달기](assets/annotate-video.png)

1. Seek to a specific point in the video, specify the time in seconds in the **text** field and click **Jump**. For example, to skip the first 20 seconds of video, enter 20 in the text field.

   ![비디오에서 지정된 초 단위로 건너뛸 시간을 찾습니다](assets/seek-in-video.png)

1. 타임라인에서 보려면 주석을 클릭합니다. 타임라인에서 주석을 삭제하려면 **[!UICONTROL 삭제]**.

   ![타임라인에서 주석 및 세부 정보 보기](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [Experience Manager Assets에서 디지털 자산 관리](/help/assets/manage-assets.md)
>* [Experience Manager Assets에서 컬렉션 관리](/help/assets/manage-collections.md)
>* [Dynamic Media 비디오 설명서](/help/assets/video.md).

