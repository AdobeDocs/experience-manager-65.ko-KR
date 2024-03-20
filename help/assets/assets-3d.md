---
title: Dynamic Media에서 3D 자산 작업
description: Dynamic Media에서 3D 자산을 업로드, 관리, 보기 및 몰입형 환경으로 전달하는 방법을 알아봅니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
feature: 3D Assets,Asset Management
role: User, Admin
exl-id: 01c96f1e-c0e6-497d-bd7a-c0fd547a34da
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2354'
ht-degree: 2%

---

# Dynamic Media에서 3D 자산 작업 {#working-with-three-d-assets-dm}

Dynamic Media을 사용하면 3D 자산을 업로드, 관리 및 보고 몰입형 환경으로 제공할 수 있습니다.

* 원클릭 게시(사용) **[!UICONTROL 빠른 게시]** 3D 에셋의 속성(도구 모음에서 )을 클릭하여 URL을 생성합니다.
* Adobe Dimension에서 제공하는 고품질의 대화형 Dimensional 뷰어 사전 설정으로 3D 자산 보기를 최적화할 수 있습니다.
* 3D Media WCM 구성 요소를 사용하면 Adobe Experience Manager Sites 페이지에 3D 에셋을 쉽게 추가할 수 있습니다.

Dynamic Media에서 3D 자산을 사용하는 데 필요한 추가 구성은 없습니다.

![3d 신발](/help/assets/assets-dm/3d-dimensional-viewer-quickpublish-url-embed2.png) *3차원 구두 상세 정보 페이지.*

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Dynamic Media에서 지원되는 3D 형식 {#supported-three-d-file-formats-in-dm}

Dynamic Media은 다음과 같은 3D 형식을 지원합니다.

참조: [지원되는 3D 형식](/help/assets/assets-formats.md).

| 3D 파일 확장명 | 파일 포맷 | MIME 유형 | 메모 |
|---|---|---|---|
| GLB | 이진 GL 전송 | model/gltf-binary | 재료 및 텍스처를 단일 자산으로 포함합니다. |
| OBJ | WaveFront 3D 개체 파일 | application/x-tgif |  |
| STL | 스테레오리소그래피 | application/vnd.ms-pki.stl |  |
| USDZ | 범용 장면 설명 Zip 아카이브 | model/vnd.usdz+zip | *수집 전용 지원으로, 보기 또는 상호 작용을 사용할 수 없습니다.* USDZ는 Safari 및 iOS 디바이스에서 기본적으로 볼 수 있는 독점 3D 포맷입니다. |

>[!NOTE]
>
>자산의 세부 사항 페이지에서 3D Media WCM 구성 요소 및 3D 미리 보기는 최신 버전의 Chrome(97.x)과 호환되지 않습니다. 대신 3D 자산으로 작업하려면 Firefox나 Safari를 사용하거나 이전 버전의 Chrome(96.x)을 사용하십시오.

## 빠른 시작: Dynamic Media의 3D 자산 {#quick-start-three-d}

다음 단계별 워크플로 설명은 Dynamic Media - Scene7 모드에서 3D 자산을 빠르게 시작하고 실행하는 데 도움이 되도록 설계되었습니다.

>[!IMPORTANT]
>
>3D 자산은 Dynamic Media - 하이브리드 모드에서 지원되지 않습니다.

Dynamic Media에서 3D 자산으로 작업하기 전에 Experience Manager 관리자가 Dynamic Media - Scene7 모드에서 Dynamic Media Cloud Service을 이미 활성화하고 구성했는지 확인하십시오.

다음을 참조하십시오 [Dynamic Media Cloud Service 구성](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) Dynamic Media 구성 - Scene7 모드 및 [Dynamic Media 문제 해결 - Scene7 모드](/help/assets/troubleshoot-dms7.md).

1. **3D 자산 업로드**

   * [Dynamic Media에서 사용할 3D 자산 업로드](/help/assets/manage-assets.md#uploading-assets).
   * [Dynamic Media에서 업로드하도록 지원되는 3D 파일 형식](#supported-three-d-file-formats-in-dm).

1. **3D 자산 관리**

   * 3D 자산 구성 및 검색

      * [디지털 자산 구성](/help/assets/organize-assets.md#organize-digital-assets).
      * [3D 자산 검색](/help/assets/search-assets.md).
      * [사용자 지정 술어를 사용하여 검색 결과 필터링](/help/assets/search-assets.md#custompredicates).

   * 3D 자산 보기

      * [3D 자산 보기 및 상호 작용](#viewing-three-d-assets).
      * [차원 뷰어 사전 설정 관리](/help/assets/managing-viewer-presets.md).

   * 3D 자산 메타데이터 작업

      * [디지털 에셋용 메타데이터 관리](/help/assets/metadata.md).
      * [메타데이터 스키마](/help/assets/metadata-schemas.md).

1. **3D 자산 게시**

   * [정적 Dynamic Media 3D 자산 게시](#publishing-three-d-assets)
   * [차원 뷰어를 사용하여 Dynamic Media 3D 자산을 게시하는 대체 방법](#alternate-publish-methods)

## 3D 자산 보기 및 상호 작용 정보 {#viewing-three-d-assets}

이 섹션에서는 자산 세부 사항 페이지 내에서 및 Experience Manager Sites의 3D 미디어 구성 요소 내에서 두 가지 방법으로 3D 자산을 보고 상호 작용하는 방법에 대해 설명합니다.

대화형 3D 뷰어에는 특히 3D 자산을 궤도 회전, 확대/축소 및 이동할 수 있는 대화형 카메라 컨트롤 컬렉션이 포함되어 있습니다.

에셋 세부 사항 페이지 보기에서 3D 에셋을 여는 데 걸리는 시간은 여러 요인에 따라 다릅니다. 이러한 요인에는 다음과 같은 것들이 포함됩니다.

* 서버에 대한 대역폭.
* 서버 대기 시간
* 이미지의 복잡성입니다.

또한 대화식으로 카메라를 조작할 때는 워크스테이션, 노트북 또는 모바일 터치 장치와 같은 클라이언트 컴퓨터의 기능도 고려해야 합니다. 우수한 그래픽 기능을 갖춘 합리적으로 강력한 시스템은 대화형 3D 시청 환경을 더 유연하고 더 유리하게 만들 수 있습니다.

>[!TIP]
>
>뷰어 사전 설정 편집기에서 차원 뷰어 사전 설정을 열어 먼저 3D 파일을 업로드하지 않고도 3D 에셋을 탐색하는 방법을 연습할 수 있습니다. 차원 뷰어 사전 설정에는 상호 작용할 수 있는 내장 3D 자산이 있습니다.
>
>다음을 참조하십시오 [뷰어 사전 설정 관리](/help/assets/managing-viewer-presets.md).

## 자산 세부 사항 페이지에서 3D 자산을 보고 상호 작용합니다 {#viewing-three-d-assets-from-asset-details-page}

참조: [소프트웨어 인터페이스를 사용하여 에셋 미리보기](/help/assets/previewing-assets.md).

**에셋 세부 사항 페이지에서 3D 에셋을 보고 상호 작용하려면 다음 작업을 수행하십시오.**

1. 3D 자산을 Experience Manager에 업로드했는지 확인합니다.

   다음을 참조하십시오 [Dynamic Media에서 사용할 3D 자산 업로드](/help/assets/manage-assets.md#uploading-assets).

1. Experience Manager에서 **[!UICONTROL 탐색]** 페이지, 이동 **[!UICONTROL 에셋]** > **[!UICONTROL 파일]**.
1. 페이지의 오른쪽 상단 모서리 근처 **[!UICONTROL 보기]** 드롭다운 목록에서 다음을 선택합니다. **[!UICONTROL 카드 보기]**.
1. 보려는 3D 자산으로 이동합니다.
1. 3D 에셋의 카드를 선택합니다.
1. 3D 자산에 대한 세부 사항 보기 페이지에서 다음 중 하나를 수행합니다.

   | 보기 | 설명 | 마우스 동작 | 터치 스크린 동작 |
   | --- | --- | --- | --- |
   | **카메라 돌리기** | 3D 장면 및 개체 주위로 보기를 궤도 회전합니다. | 마우스 왼쪽 단추를 클릭하고 드래그합니다. | 한 손가락으로 + 드래그. |
   | **카메라 회전** | 보기를 왼쪽, 오른쪽, 위쪽 또는 아래쪽으로 회전합니다. | 마우스 오른쪽 단추를 클릭하고 드래그하십시오. | 두 손가락으로 + 드래그. |
   | **카메라 확대/축소** | 3D 장면의 영역 안과 밖으로 이동합니다. | 스크롤 휠입니다. | 손가락 두 개 조입니다. |
   | **카메라를 가운데로 다시 맞춤** | 카메라를 3D 장면의 개체에 있는 점에 다시 가운데로 맞춥니다. | 두 번 클릭합니다. | 두 번 선택합니다. |
   | **재설정** | 페이지의 오른쪽 하단 모서리 근처에서 재설정 아이콘을 선택하여 보기 대상 지점을 3D 에셋의 가운데로 복원합니다. 또한 재설정을 사용하면 카메라를 더 가깝게 또는 더 멀리 이동하여 에셋을 전체적으로 적절한 보기 크기로 표시할 수 있습니다. |   |   |
   | **전체 화면 모드** | 전체 화면 모드로 전환하려면 페이지의 오른쪽 아래 모서리에서 전체 화면 아이콘을 선택합니다. |   |   |

1. 페이지의 오른쪽 상단 모서리에서 을(를) 선택합니다. **[!UICONTROL 닫기]** 자산 페이지로 돌아갑니다.

## 3D 미디어 구성 요소 내에서 3D 자산 보기 및 상호 작용 {#interacting-with-asset-inside-three-d-media-component}

웹 페이지가 있을 때 **[!UICONTROL 편집]** 모드에서는 3D 에셋과의 상호 작용이 불가능합니다. 자산을 대화형으로 만들려면 다음을 사용할 수 있습니다. **[!UICONTROL 미리 보기]** 3D 미디어 구성 요소의 기능에 대한 전체 액세스 권한으로 페이지 편집기에서 웹 페이지를 보는 기능입니다.

>[!IMPORTANT]
>
>웹 페이지에 3D Media 구성 요소를 추가하고 구성 요소에 3D 자산을 할당한 후에만 이 작업을 수행할 수 있습니다. 다음을 참조하십시오 [웹 페이지에 3D Media 구성 요소 추가](#adding-the-three-d-media-component-to-a-web-page) 및 [3D Media 구성 요소에 3D 자산 할당](#assigning-a-three-d-asset-to-the-component).

참조: [소프트웨어 인터페이스를 사용하여 에셋 미리보기](/help/assets/previewing-assets.md).

**3D 미디어 구성 요소 내에서 3D 에셋을 보고 상호 작용하려면 다음 작업을 수행하십시오.**

1. 웹 페이지가 있는 동안 **[!UICONTROL 편집]** 모드, 다음 중 하나를 수행합니다.

   * 페이지의 오른쪽 상단 근처에서 을 선택합니다. **[!UICONTROL 미리 보기]** 입장하기 **[!UICONTROL 미리 보기]** 모드.
   * 삭제 `/editor.html` 를 입력합니다.

   ![3D 미디어 구성 요소 내부에 표시되는 3D 자산](/help/assets/assets-dm/3d-asset-in-3d-media.png)
에 표시되는 완전 대화형 3D 에셋 **[!UICONTROL 미리 보기]** 모드.

1. 다음 기간 동안 **[!UICONTROL 미리 보기]** mode에서 다음 중 하나를 수행합니다.

   | 보기 | 설명 | 마우스 동작 | 터치 스크린 동작 |
   | --- | --- | --- | --- |
   | **카메라 돌리기** | 3D 장면 및 개체 주위로 보기를 궤도 회전합니다. | 마우스 왼쪽 단추를 클릭하고 드래그합니다. | 한 손가락으로 + 드래그. |
   | **카메라 회전** | 보기를 왼쪽, 오른쪽, 위쪽 또는 아래쪽으로 회전합니다. | 마우스 오른쪽 단추를 클릭하고 드래그하십시오. | 두 손가락으로 + 드래그. |
   | **카메라 확대/축소** | 3D 장면의 영역 안과 밖으로 이동합니다. | 스크롤 휠입니다. | 손가락 두 개 조입니다. |
   | **카메라를 가운데로 다시 맞춤** | 카메라를 3D 장면의 개체에 있는 점에 다시 가운데로 맞춥니다. | 두 번 클릭합니다. | 두 번 선택합니다. |
   | **재설정** | 페이지의 오른쪽 하단 모서리 근처에서 재설정 아이콘을 선택하여 보기 대상 지점을 3D 에셋의 가운데로 복원합니다. 또한 재설정을 사용하면 카메라를 더 가깝게 또는 더 멀리 이동하여 에셋을 전체적으로 적절한 보기 크기로 표시할 수 있습니다. |   |   |
   | **전체 화면 모드** | 전체 화면 모드로 전환하려면 페이지의 오른쪽 아래 모서리에서 전체 화면 아이콘을 선택합니다. |   |   |

## 3D 미디어 구성 요소 작업 정보 {#working-with-three-d-media-component}

Dynamic Media에는 Adobe Experience Manager Sites에서 웹 페이지에서 3D 모델을 대화식으로 볼 수 있도록 하는 데 사용할 수 있는 Dynamic Media 3D Media 구성 요소가 포함되어 있습니다.

* [페이지 템플릿에 3D 미디어 구성 요소 추가](#adding-three-d-media-component-to-page-template)
* [웹 페이지에 3D Media 구성 요소 추가](#adding-the-three-d-media-component-to-a-web-page)
   * [선택 사항 - 3D 미디어 구성 요소 구성](#configuring-the-three-d-component)
* [3D Media 구성 요소에 3D 자산 할당](#assigning-a-three-d-asset-to-the-component)

## 페이지 템플릿에 3D 미디어 구성 요소 추가 {#adding-three-d-media-component-to-page-template}

1. 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL 템플릿]**.
1. 3D 구성 요소를 활성화할 페이지 템플릿으로 이동한 다음 템플릿을 선택합니다.
1. 선택 **[!UICONTROL 편집]** 템플릿을 열 수 있습니다.
1. 페이지의 오른쪽 상단 근처에 있는 드롭다운 메뉴에서 를 선택합니다. **[!UICONTROL 구조]** 아직 활성화되지 않은 경우 모드.

   ![3d-media-component-structure](/help/assets/assets-dm/3d-media-component-structure.png)

1. 에서 빈 영역 선택 **[!UICONTROL 레이아웃 컨테이너]** 영역을 선택하면 해당 영역을 선택하고 관련 도구 모음을 열 수 있습니다.
1. 도구 모음에서 **[!UICONTROL 정책]** 아이콘을 클릭하여 엽니다. **[!UICONTROL 정책 편집기]**.
1. 다음에서 **[!UICONTROL 속성]** 섹션, **[!UICONTROL 허용된 구성 요소]** 탭, 다음으로 스크롤 **[!UICONTROL Dynamic Media]**&#x200B;를 클릭한 다음 목록을 확장하고 을(를) 선택합니다 **[!UICONTROL 3D 미디어]**.
1. 선택 **[!UICONTROL 완료]** 변경 사항을 저장하고 **[!UICONTROL 정책 편집기]**.

   이제 이 템플릿을 사용하는 모든 페이지에 Dynamic Media 3D 미디어 구성 요소를 배치할 수 있습니다.

## 웹 페이지에서 3D Media 구성 요소 추가 {#adding-the-three-d-media-component-to-a-web-page}

Experience Manager을 웹 컨텐츠 관리 시스템으로 사용하는 경우 3D 미디어 구성 요소를 통해 웹 페이지에 3D 자산을 추가할 수 있습니다.

참조: [페이지에 Dynamic Media 에셋 추가](/help/assets/adding-dynamic-media-assets-to-pages.md).

**웹 페이지에서 3D Media 구성 요소를 추가하려면 다음을 수행하십시오.**

1. Experience Manager Sites을 열고 Dynamic Media 3D 미디어 구성 요소를 추가할 웹 페이지를 선택합니다.
1. 다음 항목 선택 **[!UICONTROL 편집]** (연필) 아이콘 을 사용하여 페이지를 페이지 편집기에서 열 수 있습니다. 다음을 확인합니다. **[!UICONTROL 편집]** 모드는 페이지의 오른쪽 상단 근처에서 선택됩니다.

   ![3d-media-component-add](/help/assets/assets-dm/3d-media-component-edit.png)

1. 도구 모음에서 사이드 패널 아이콘을 선택하여 패널 표시를 전환하거나 &quot;켜기&quot;합니다.

1. 사이드 패널에서 더하기 기호 아이콘을 선택하여 **[!UICONTROL 구성 요소]** 목록을 표시합니다.

   ![3d-media-component-drag-drop](/help/assets/assets-dm/3d-assets-filter.png)

1. 드래그 **[!UICONTROL 3D 미디어]** 의 구성 요소 **[!UICONTROL 구성 요소]** 3D 뷰어를 표시할 페이지의 위치를 표시합니다.

이제 구성 요소에 3D 자산을 할당할 준비가 되었습니다.

다음을 참조하십시오 [3D Media 구성 요소에 3D 자산 할당](#assigning-a-three-d-asset-to-the-component).

### 선택 사항 - 3D 미디어 구성 요소 구성 {#configuring-the-three-d-component}

1. Experience Manager Sites 페이지 편집기에서 **[!UICONTROL 3D 미디어 뷰어]** 이전에 페이지에 추가한 구성 요소입니다.
1. 다음 항목 선택 **[!UICONTROL 구성]** 아이콘(렌치)을 클릭하여 구성 요소 구성 대화 상자를 열 수 있습니다.

   ![3d-media-component-config](/help/assets/assets-dm/3d-media-component-config.png)

1. 3D 미디어 대화 상자의 뷰어 사전 설정 드롭다운 목록에서 을(를) 선택합니다 **[!UICONTROL 차원]** 차원 뷰어 사전 설정을 구성 요소에 할당합니다.

   ![3d-media-component-edit-config](/help/assets/assets-dm/3d-media-component-edit-config.png)

1. 오른쪽 상단 모서리에서 확인 표시를 선택하여 변경 사항을 저장합니다.

## 3D Media 구성 요소에 3D 자산 할당 {#assigning-a-three-d-asset-to-the-component}

웹 페이지에 3D 미디어 구성 요소를 추가한 후 3D 에셋을 할당할 수 있습니다.

다음을 참조하십시오 [웹 페이지에 3D Media 구성 요소 추가](#adding-the-three-d-media-component-to-a-web-page).

**3D 자산을 3D 미디어 구성 요소에 할당하려면 다음을 수행하십시오.**

1. Experience Manager Sites 페이지 편집기에서 **[!UICONTROL 에셋]** 아이콘 열기 **[!UICONTROL 에셋]** 사이드 패널에서.
1. 드롭다운 목록에서 을(를) 선택합니다 **[!UICONTROL 3D]** 3D 자산 파일 유형만 표시합니다.
1. 사이드 패널에서 편집 중인 페이지에서 보려는 3D 자산을 검색하거나 해당 자산으로 스크롤합니다.
1. 에셋 사이드 패널에서 3D 에셋을 드래그하여 **[!UICONTROL 3D 미디어]** 이전에 페이지에 추가한 구성 요소입니다.

   ![3D Media 구성 요소에 3D 자산 할당](/help/assets/assets-dm/3d-asset-add.png)

>[!NOTE]
>
>웹 페이지가 Experience Manager Sites에 있는 동안 **[!UICONTROL 편집]** 모드에서는 3D 미디어 구성 요소가 3D 에셋을 표시하지만 에셋과의 상호 작용은 할 수 없습니다. 자산을 대화형으로 만들려면 다음을 사용할 수 있습니다. **[!UICONTROL 미리 보기]** 3D 미디어 구성 요소의 기능에 대한 전체 액세스 권한으로 페이지 편집기에서 웹 페이지를 보는 기능입니다.

## 정적 Dynamic Media 3D 자산 게시 {#publishing-three-d-assets}

Dynamic Media은 다음과 같이 지원되는 다양한 3D 파일 형식을 허용합니다. *정적 콘텐츠* Dynamic Media. 정적 콘텐츠 는 3D 자산을 업로드하고 게시할 수 있지만 를 지원하지 않음을 의미합니다 *가변 이미징* 또는 3D 에셋과 연관된 이미지 리피팅. 그 이유는 Dynamic Media Imaging Server가 3D 형식을 인식하지 못하기 때문입니다. 따라서 Dynamic Media에 3D 자산을 게시한 후에는 복사할 수 있는 인스턴트 URL이 있습니다. 3D 에셋의 URL은 일반적인 Dynamic Media URL 구조를 따릅니다. 그러나 Dynamic Media의 기존 이미지 에셋과 달리 에셋의 URL에서는 매개 변수를 편집할 수 없습니다.

참조: [정적 자산에 대한 URL 얻기](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset).

다음에서 **[!UICONTROL 카드 보기]**, 작은 지구본 아이콘이 에셋의 이름 바로 아래에 나타나며 날짜 및 시간 왼쪽에 게시되었음을 나타냅니다. In the **[!UICONTROL List View]**, a **[!UICONTROL Published]** column indicates which assets are published or which are not.

Experience Manager을 WCM으로 사용하는 경우 이 게시 방법을 사용하여 웹 페이지에 직접 Dynamic Media 3D 자산을 추가합니다.

참조: [Dynamic Media 에셋 게시](publishing-dynamicmedia-assets.md).

참조: [페이지 게시](/help/sites-authoring/publishing-pages.md).

**정적 Dynamic Media 3D 자산을 게시하려면 다음 작업을 수행하십시오.**

1. 자산 세부 사항 페이지에서 볼 수 있도록 3D 자산(GLB, OBJ 또는 STL 파일 형식)을 엽니다.
1. 도구 모음에서 를 선택합니다. **[!UICONTROL 빠른 게시]**.

   ![3d-asset-quick-publish](/help/assets/assets-dm/3d-asset-quick-publish.png)

1. 선택 **[!UICONTROL 닫기]** 대화 상자를 종료하고 에셋 세부 정보 페이지로 돌아갑니다.
1. 3D 에셋의 파일 이름 왼쪽에 있는 드롭다운 목록에서 를 선택합니다 **[!UICONTROL 표현물]**.

   ![3d 자산 표현물](/help/assets/assets-dm/3d-asset-renditions.png)

1. 선택 **[!UICONTROL 원본]**. 3D 자산이 게시(또는 &quot;활성화&quot;)될 때 **[!UICONTROL URL]** 다음 3D 자산 조건이 모두 충족되면 페이지의 왼쪽 하단 모서리 근처에 단추가 표시됩니다.
   * 3D 자산은 지원되는 형식(GLB, OBJ, STL 및 USDZ)입니다.
   * 3D 자산이 Dynamic Media 이미지 프로덕션 시스템(IPS)에 수집되었습니다.
   * 3D 자산이 게시됩니다.

   ![3d-asset-url](/help/assets/assets-dm/3d-asset-url.png)

1. 선택 **[!UICONTROL URL]** 따라서 웹 페이지에서 복사하고 사용할 수 있는 3D 자산의 직접 프로덕션 URL을 표시할 수 있습니다.

### 차원 뷰어를 사용하여 Dynamic Media 3D 자산을 게시하는 대체 방법 {#alternate-publish-methods}

다음과 같은 두 가지 방법을 사용하여 Dynamic Media 3D 자산을 게시할 수 있습니다 *아님* Experience Manager을 WCM으로 사용합니다.

* **[!UICONTROL URL]** - 사용 **[!UICONTROL URL]** 서드파티 웹 컨텐츠 관리 시스템을 사용 중이고 차원 뷰어를 사용하여 Dynamic Media 3D 자산을 웹 페이지에 연결하려는 경우.

  다음을 참조하십시오 [웹 애플리케이션에 URL 연결](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset).

* **[!UICONTROL 포함]** - 사용 **[!UICONTROL 포함]** 차원 뷰어를 사용하여 웹 페이지에 포함된 Dynamic Media 3D 자산을 보려는 경우. You copy the embed code to the clipboard so you can paste it in your web pages. 에서는 코드를 편집할 수 없습니다. **[!UICONTROL 포함]** 대화 상자.

  다음을 참조하십시오 [웹 페이지에 Dynamic Media 비디오, 이미지 뷰어 또는 차원 뷰어 포함](/help/assets/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page).
