---
title: 비디오 자산 관리
description: 비디오 자산을 업로드, 미리 보기, 주석 달기 및  [!DNL Adobe Experience Manager]에 게시합니다.
contentOwner: AG
role: Business Practitioner
feature: 자산 관리
exl-id: 21d3e0bd-5955-470a-8ca2-4d995c17eb4c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 0%

---

# 비디오 자산 관리 {#manage-video-assets}

비디오 형식은 조직의 디지털 자산에 중요한 부분입니다. [!DNL Adobe Experience Manager] 에서는 비디오 자산이 만들어진 후 비디오 자산의 전체 라이프사이클을 관리하기 위한 성숙한 오퍼링과 기능을 제공합니다.

[!DNL Adobe Experience Manager Assets]에서 비디오 자산을 관리하고 편집하는 방법을 알아봅니다. 예를 들어 FFmpeg 코드 변환 시 [!DNL Dynamic Media] 통합을 사용하여 비디오 인코딩과 코드 변환을 수행할 수 있습니다.

## 비디오 자산 업로드 및 미리 보기 {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 에서는 확장 MP4를 사용하여 비디오 자산에 대한 미리 보기를 생성합니다. 자산의 형식이 MP4가 아닌 경우, FFmpeg 팩을 설치하여 미리 보기를 생성합니다. FFmpeg는 OGG 및 MP4 유형의 비디오 표현물을 만듭니다. [!DNL Assets] 사용자 인터페이스에서 렌디션을 미리 볼 수 있습니다.

1. 디지털 자산 폴더 또는 하위 폴더에서 디지털 자산을 추가할 위치로 이동합니다.
1. 자산을 업로드하려면 도구 모음에서 **[!UICONTROL 만들기]**&#x200B;를 클릭하고 **[!UICONTROL 파일]**&#x200B;을 선택합니다. 또는 사용자 인터페이스에서 파일을 드래그합니다. 자세한 내용은 [자산 업로드](manage-assets.md#uploading-assets)를 참조하십시오.
1. 카드 보기에서 비디오를 미리 보려면 비디오 자산에서 **[!UICONTROL 재생]** ![재생 옵션](assets/do-not-localize/play.png) 옵션을 클릭합니다. 카드 보기에서만 비디오를 일시 중지하거나 재생할 수 있습니다. [!UICONTROL 재생] 및 [!UICONTROL 일시 정지] 옵션은 목록 보기에서 사용할 수 없습니다.

1. 자산 세부 사항 페이지에서 비디오를 미리 보려면 카드에서 **[!UICONTROL 편집]**&#x200B;을 클릭합니다. 비디오는 브라우저의 기본 비디오 플레이어에서 재생됩니다. 비디오를 전체 화면으로 재생, 일시 정지, 볼륨 제어 및 확대/축소할 수 있습니다.

   ![비디오 재생 제어](assets/video-playback-controls.png)

## 2GB {#configuration-to-upload-assets-that-are-larger-than-gb}보다 큰 자산을 업로드하도록 구성

기본적으로 [!DNL Assets]에서는 파일 크기 제한으로 인해 2GB보다 큰 자산을 업로드할 수 없습니다. 그러나 CRXDE Lite으로 이동하여 `/apps` 디렉토리 아래에 노드를 만들어 이 제한을 덮어쓸 수 있습니다. 노드에는 동일한 노드 이름, 디렉토리 구조 및 이와 비교할 수 있는 노드 속성이 있어야 합니다.

[!DNL Assets] 구성 외에 다음 구성을 변경하여 큰 자산을 업로드하십시오.

* 토큰 만료 시간을 늘립니다. `https://[aem_server]:[port]/system/console/configMgr`의 웹 콘솔에서 [!UICONTROL Granite CSRF 서블릿] Adobe을 참조하십시오. 자세한 내용은 [CSRF 보호](/help/sites-developing/csrf-protection.md)를 참조하십시오.
* Dispatcher 구성에서 `receiveTimeout`을 늘립니다. 자세한 내용은 [Dispatcher 구성 Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options)를 참조하십시오.

>[!NOTE]
>
>[!DNL Experience Manager] Classic 사용자 인터페이스에는 2GB 파일 크기 제한이 없습니다. 또한 큰 비디오에 대한 종단 간 워크플로우는 완전히 지원되지 않습니다.

더 높은 파일 크기 제한을 구성하려면 `/apps` 디렉토리에서 다음 단계를 수행하십시오.

1. [!DNL Experience Manager]에서 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**&#x200B;을 클릭합니다.
1. CRXDE Lite에서 `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`(으)로 이동합니다. 디렉토리 창을 보려면 `>>` 을 클릭합니다.
1. 도구 모음에서 **[!UICONTROL 오버레이 노드]**&#x200B;를 클릭합니다. 또는 컨텍스트 메뉴에서 **[!UICONTROL 오버레이 노드]**&#x200B;를 선택합니다.
1. **[!UICONTROL 오버레이 노드]** 대화 상자에서 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

   ![오버레이 노드](assets/overlay-node-path.png)

1. 브라우저를 새로 고칩니다. 오버레이 노드 `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`이(가) 선택되어 있습니다.
1. **[!UICONTROL 속성]** 탭에서 적절한 값을 바이트 단위로 입력하여 크기 제한을 원하는 크기로 늘리십시오. 예를 들어 크기 제한을 30GB로 늘리려면 `32212254720` 값을 입력합니다.

1. 도구 모음에서 **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.
1. [!DNL Experience Manager]에서 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**&#x200B;을 클릭합니다.
1. [!DNL Adobe Experience Manager] [!UICONTROL 웹 콘솔 번들] 페이지의 테이블의 이름 열 아래에서 **[!UICONTROL Granite Workflow 외부 프로세스 작업 핸들러 Adobe]**&#x200B;를 찾아 클릭합니다.
1. [!UICONTROL Granite Workflow 외부 프로세스 작업 핸들러 Adobe] 페이지에서 **[!UICONTROL 기본 시간 초과]** 및 **[!UICONTROL 최대 시간 초과]** 필드 모두에 대한 초를 `18000`(5시간)로 설정합니다. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.
1. [!DNL Experience Manager]에서 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로우]** > **[!UICONTROL 모델]**&#x200B;을 클릭합니다.
1. 워크플로우 모델 페이지에서 **[!UICONTROL Dynamic Media 인코딩 비디오]**&#x200B;을 선택한 다음 **[!UICONTROL 편집]**&#x200B;을 클릭합니다.
1. 워크플로우 페이지에서 **[!UICONTROL Dynamic Media 비디오 서비스 프로세스]** 구성 요소를 두 번 클릭합니다.
1. [!UICONTROL 단계 속성] 대화 상자의 **[!UICONTROL 공통]** 탭에서 **고급 설정**&#x200B;을 확장합니다.
1. **[!UICONTROL 시간 초과]** 필드에서 `18000` 값을 지정한 다음 **[!UICONTROL 확인]**&#x200B;을 클릭하여 **[!UICONTROL Dynamic Media 인코딩 비디오]** 워크플로우 페이지로 돌아갑니다.
1. 페이지 상단 근처에 있는 [!UICONTROL Dynamic Media 인코딩 비디오] 페이지 제목 아래에서 **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

## 비디오 자산 게시 {#publish-video-assets}

게시 후 비디오 자산을 웹 페이지에 URL로 포함하거나 자산을 직접 포함할 수 있습니다. 자세한 내용은 [Dynamic Media 자산 게시](/help/assets/publishing-dynamicmedia-assets.md)를 참조하십시오.

## 비디오 자산에 주석 달기 {#annotate-video-assets}

1. [!DNL Assets] 콘솔에서 자산 카드의 **[!UICONTROL 편집]**&#x200B;을 선택하여 자산 세부 사항 페이지를 표시합니다.
1. 비디오를 재생하려면 **[!UICONTROL 미리 보기]**&#x200B;를 클릭하십시오.
1. 비디오에 주석을 달려면 **[!UICONTROL 주석 달기]**&#x200B;를 클릭합니다. 비디오에서 특정 시간(프레임)에 주석이 추가됩니다. 캔버스에 주석을 달 때 그림을 그리고 드로잉에 주석을 포함할 수 있습니다. 주석이 자동으로 저장됩니다. 주석 마법사를 종료하려면 **[!UICONTROL 닫기]**&#x200B;를 클릭합니다.

   ![비디오 프레임에 그리기 및 주석 달기](assets/annotate-video.png)

1. 비디오에서 특정 지점을 찾은 후 **text** 필드에 시간을 초 단위로 지정하고 **점프**&#x200B;를 클릭합니다. 예를 들어 비디오 처음 20초를 건너뛰려면 텍스트 필드에 20을 입력합니다.

   ![비디오에서 지정된 초 단위로 건너뛸 시간을 찾습니다](assets/seek-in-video.png)

1. 타임라인에서 보려면 주석을 클릭합니다. 타임라인에서 주석을 삭제하려면 **[!UICONTROL 삭제]**&#x200B;를 클릭합니다.

   ![타임라인에서 주석 및 세부 정보 보기](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [Experience Manager 자산에서 디지털 자산 관리](/help/assets/manage-assets.md)
* [Experience Manager 자산의 컬렉션 관리](/help/assets/manage-collections.md)
* [Dynamic Media 비디오 설명서](/help/assets/video.md).

