---
title: ' [!DNL Adobe Experience Manager Assets] 소개.'
description: 디지털 자산 관리란 무엇이고, 사용 사례 및  [!DNL Adobe Experience Manager Asset] 상품.
contentOwner: AG
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 36%

---


# [!DNL Adobe Experience Manager Assets]을(를) DAM 솔루션 {#administering-assets} 소개

[!DNL Assets] 은 플랫폼의 필수 구성 요소인 DAM(Digital Asset Management) 툴로 기업이 디지털 에셋을  [!DNL Experience Manager] 관리하고 배포할 수 있습니다. 조직 전반의 사용자는 웹, 인쇄 및 디지털 배포를 위해 이미지, 비디오, 문서, 오디오 클립, 3D 파일 및 리치 미디어와 같은 다양한 유형의 디지털 에셋을 관리, 저장 및 액세스할 수 있습니다.

## 디지털 자산 관리란 무엇입니까? {#what-is-digital-asset-management}

[!DNL Assets] 조직의 주요 디지털 자산을 전사적 공유 및 배포할 수 있습니다. 조직 전반의 사용자는 웹 인터페이스(또는 CIFS 또는 WebDAV 폴더)를 통해 이미지, 그래픽, 오디오, 비디오 및 문서와 같은 디지털 자산을 저장, 관리 및 액세스할 수 있습니다.

[!DNL Assets] 의 기능을  [!DNL Experience Manager] 사용하면 다음을 수행할 수 있습니다.

* 이미지, 문서, 오디오 파일 및 비디오 파일을 다양한 파일 형식으로 추가하고 공유합니다.
* 자산을 태그, 라이트박스 또는 별표(즐겨찾기)별로 그룹화하여 관리합니다. 자산에 주석을 추가합니다.
* 파일 이름, 문서의 전체 텍스트, 날짜, 문서 유형 및 태그를 검색하여 자산을 찾습니다.
* 자산에 관한 메타데이터 정보를 추가하거나 편집합니다. 메타데이터는 해당 자산에 따라 자동으로 버전이 매겨집니다. 자산 메타데이터를 가져오거나 내보낼 수 있습니다.
* 이미지 필터 추가 및 크기 조절과 같은 이미지 편집 기능을 수행합니다. WebDAV 또는 CIFS 폴더를 사용하여 여러 디지털 자산을 동시에 가져오고 내보냅니다.
* 워크플로우 및 알림을 사용하여 자산 세트를 공동 처리 및 다운로드하고 자산에 대한 액세스 권한을 관리할 수 있도록 합니다.

### [!DNL Experience Manager Assets] 는  [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] 완벽하게 통합되어 모든  [!DNL Sites] 사용 사례와 매끄럽게 연동됩니다. 예를 들어 웹 페이지를 작성할 때 [!DNL Sites] 작성자는 컨텐츠 파인더를 통해 디지털 자산을 찾고 사용할 수 있습니다. [!DNL Assets]의 사용자 인터페이스는 [!DNL Sites]의 사용자 인터페이스와 동일합니다. 자세한 내용은 [사이트 개요](/help/sites-authoring/page-authoring.md)를 참조하십시오.

기본 사용자 인터페이스는 [!DNL Sites]의 사용자 인터페이스와 동일합니다. 자세한 내용은 [사이트 개요](/help/sites-authoring/page-authoring.md)를 참조하십시오.

### 디지털 자산 관리와 이미지 구성 요소 {#digital-asset-management-versus-image-component}

이미지를 DAM 저장소에 넣을지 이미지 구성 요소를 사용할지를 결정할 때 이미지 라이프사이클을 고려하십시오.

* 이미지의 라이프사이클이 페이지의 라이프사이클과 동일하다면 이미지 구성 요소를 사용하십시오.
* 이미지에 별도의 라이프 사이클이 있는 경우(예: 이미지를 두 번 사용하거나 WCM 외부에서 사용하는 경우) [!DNL Assets]을 사용합니다.

## 디지털 자산이란 무엇입니까? {#what-are-digital-assets}

자산은 디지털 문서, 이미지, 비디오 또는 오디오(또는 그 일부)로서 여러 표현물을 가질 수 있고 하위 자산(예: photoshop 파일의 레이어, PowerPoint 파일의 슬라이드, pdf의 페이지, ZIP에 있는 파일)을 가질 수 있습니다.

근본적으로 자산은 이진, 메타데이터, 표현물, 하위 자산이 합쳐진 것입니다. 자세한 내용은 [DAM 성능 안내서](/help/sites-deploying/assets-performance-sizing.md)를 참조하십시오.

>[!CAUTION]
>
>대량의 자산(특히 이미지)을 업로드 및/또는 편집하는 것은 [!DNL Experience Manager] 배포의 성능에 영향을 줄 수 있습니다.

### [!DNL Experience Manager Assets] 용어  {#aem-assets-terminology}

[!DNL Experience Manager]에서 디지털 자산으로 작업하는 경우 다음 용어를 이해해야 합니다.

* **컬렉션**:실제 위치(폴더), 공통 속성(저장된 검색 폴더) 또는 사용자 선택(라이트박스 폴더)에 따라 자산 컬렉션입니다.

* **메타데이터** [!DNL Assets] 메타데이터 사용;작성자, 만료 날짜, DRM 정보(Digital Rights Management) 등과 같은 일반적인 정보를 제공합니다. 메타데이터에 대한 액세스를 제어할 수 있습니다. [!DNL Assets] 에서는 다음과 같은 다양한 공통 메타데이터 스키마를 기본적으로 지원합니다.

   * 더블린 코어: 작성자, 설명, 날짜, 제목 등을 포함합니다.
   * IPTC: 이벤트, 모델, 위치 등을 포함합니다.
   * WCM:페이지 속성 포함, [!UICONTROL On Time] 및 [!UICONTROL Off Time] 등이 있습니다.

* **태그 지정**: [!DNL Assets] 태그를 지정하고 분류할 수 있습니다. [자산 구성](/help/assets/organize-assets.md)을 참조하십시오.

* **표현물**:표현물은 자산의 이진 표현입니다. [!DNL Assets] 항상 업로드된 파일의 표현인 기본 표현을 가집니다. 자산에는 사용자 지정된 작업 흐름 단계에 의해서나 자산이 업로드될 때 만들어지는 추가적인 표현들이 있습니다. 표현물들은 크기가 다르거나 해상도가 다르거나, 워터마크가 추가로 있거나 기타 특성이 변경되었을 수 있습니다.

* **버전**:버전 매기기를 통해 특정 시점의 디지털 자산 스냅샷을 만들 수 있습니다. 자산을 이전 버전으로 복원할 수 있습니다. 자산](manage-assets.md#asset-versioning)에서 [버전 매기기를 참조하십시오.

* **하위 자산**:하위 자산은 예를 들어, 파일의 레이어나 PDF 파일의  [!DNL Adobe Photoshop] 페이지와 같이 자산을 구성하는 자산입니다. [!DNL Assets]에서는 자산처럼 하위 자산을 관리할 수 있습니다.

### 자산 {#how-to-work-with-assets} 사용 방법

자산 또는 컬렉션에서 작업을 수행합니다. 작업을 통해 자산, 컬렉션 및 표현물을 만들거나 수정할 수 있습니다. 자산에 대해 수행하는 많은 기본 작업(하위 자산 업로드, 삭제, 업데이트, 저장) - 사전 구성된 워크플로우를 트리거합니다. 이러한 속성은 [!DNL Assets]에서 자동으로 켜져 있으며 [!DNL Assets] 미디어 핸들러에서 자세히 설명합니다.

이러한 사전 구성된 워크플로우로 수행할 수 있는 작업:

* 자산을 저장소에 저장하거나 저장소에서 자산을 삭제합니다.
* 에셋에 대한 메타데이터를 추출하고 저장합니다.개별 메타데이터 항목이 XMP으로 저장됩니다.
* 에셋에 대한 표현물과 축소판을 생성합니다.필요한 경우 자동 크기 조정 및 자르기 작업이 가능합니다.
* 필요한 경우 자산을 코드 변환합니다. 예를 들어, 모바일 및 웹용 비디오는 초당 24프레임으로 코드가 변환되고 초당 30프레임으로 비디오를 다운로드합니다. 모바일 및 웹용 오디오는 128Kbps로 코드 변환되고 192Kbps로 오디오를 다운로드할 수 있습니다.

물론 워크플로우도 수동으로 적용할 수 있습니다. 기본 워크플로우 목록을 알려면 [ Assets 미디어 핸들러](/help/assets/media-handlers.md)를 참조하십시오.

## [!DNL Experience Manager Assets] 및 [!DNL MediaLibrary] {#cq-dam-vs-cq-medialibrary}

차이점에 대한 자세한 내용은 [자산 및 MediaLibrary](/help/assets/medialibrary.md)을 참조하십시오.
