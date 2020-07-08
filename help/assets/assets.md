---
title: Introduction to [!DNL Adobe Experience Manager Assets].
description: 디지털 에셋 관리란 무엇이고 활용 사례, [!DNL Adobe Experience Manager Asset] 분석 등을 살펴볼 수 있습니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 678e91699523c22a7048bd7b344fa539b849ae8b
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 32%

---


# DAM 솔루션 [!DNL Adobe Experience Manager Assets] 으로 정보 {#administering-assets}

[!DNL Assets] 디지털 자산 관리(DAM) 툴로, [!DNL Experience Manager] 플랫폼의 일부로 기업이 디지털 자산을 관리하고 배포할 수 있습니다. 조직 전체의 사용자는 웹, 인쇄 및 디지털 배포를 위해 이미지, 비디오, 문서, 오디오 클립, 3D 파일 및 리치 미디어와 같은 다양한 유형의 디지털 에셋을 관리, 저장 및 액세스할 수 있습니다.

## 디지털 자산 관리란 무엇입니까? {#what-is-digital-asset-management}

[!DNL Assets] 조직의 주요 디지털 자산을 전사적 공유 및 배포할 수 있습니다. 조직 전체의 사용자는 웹 인터페이스(또는 CIFS 또는 WebDAV 폴더)를 통해 이미지, 그래픽, 오디오, 비디오 및 문서와 같은 디지털 자산을 저장, 관리 및 액세스할 수 있습니다.

[!DNL Assets] 의 기능을 [!DNL Experience Manager] 사용하면 다음을 수행할 수 있습니다.

* 이미지, 문서, 오디오 파일 및 비디오 파일을 다양한 파일 형식으로 추가하고 공유합니다.
* 자산을 태그, 라이트박스 또는 별(즐겨찾기)별로 그룹화하여 관리합니다. 자산에 주석을 추가합니다.
* 파일 이름, 문서의 전체 텍스트, 날짜, 문서 유형 및 태그를 검색하여 자산을 찾습니다.
* 자산에 관한 메타데이터 정보를 추가하거나 편집합니다. 메타데이터는 해당 자산에 따라 자동으로 버전이 매겨집니다. 자산 메타데이터를 가져오거나 내보낼 수 있습니다.
* 이미지 필터 추가 및 크기 조절과 같은 이미지 편집 기능을 수행합니다. WebDAV 또는 CIFS 폴더를 사용하여 여러 디지털 자산을 동시에 가져오고 내보냅니다.
* 워크플로우 및 알림을 사용하여 자산 세트를 공동 처리 및 다운로드하고 자산에 대한 액세스 권한을 관리할 수 있도록 합니다.

### [!DNL Experience Manager Assets] 는 [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] 모든 사용 사례 [!DNL Sites] 와 완벽하게 통합되고 완벽하게 작동합니다. 예를 들어 웹 페이지를 작성할 때 작성자는 컨텐츠 파인더를 통해 디지털 자산을 [!DNL Sites] 찾아 사용할 수 있습니다. 의 사용자 인터페이스 [!DNL Assets] 는 의 사용자 인터페이스와 동일합니다 [!DNL Sites]. 자세한 [내용은 사이트](/help/sites-authoring/page-authoring.md) 개요를 참조하십시오.

기본 사용자 인터페이스는 해당 인터페이스와 동일합니다 [!DNL Sites]. 자세한 [내용은 사이트](/help/sites-authoring/page-authoring.md) 개요를 참조하십시오.

### 디지털 자산 관리와 이미지 구성 요소 {#digital-asset-management-versus-image-component}

DAM 저장소에 이미지를 넣을지, 이미지 구성 요소를 사용할지를 결정할 때 이미지 수명주기를 고려하십시오.

* 이미지의 라이프사이클이 페이지의 라이프사이클과 동일하다면 이미지 구성 요소를 사용하십시오.
* If the image has a separate life cycle, for example, if you use the image twice or outside WCM, use [!DNL Assets].

## 디지털 자산이란 무엇입니까? {#what-are-digital-assets}

자산은 여러 표현물을 가질 수 있고 하위 자산(예: photoshop 파일의 레이어, PowerPoint 파일의 슬라이드, pdf의 페이지, ZIP의 파일)을 가질 수 있는 디지털 문서, 이미지, 비디오 또는 오디오입니다.

근본적으로 자산은 이진, 메타데이터, 표현물, 하위 자산이 합쳐진 것입니다. 자세한 내용은 [DAM 성능 안내서](/help/sites-deploying/assets-performance-sizing.md)를 참조하십시오.

>[!CAUTION]
>
>Uploading and/or editing a large volume of assets (particularly images) can impact the performance of your [!DNL Experience Manager] deployment.

### [!DNL Experience Manager Assets] 용어 {#aem-assets-terminology}

When working with digital assets in [!DNL Experience Manager], you need to understand the following terminology:

* **컬렉션**: 실제 위치(폴더), 공용 속성(저장된 검색 폴더) 또는 사용자 선택(lightbox 폴더)을 기반으로 한 자산 컬렉션입니다.

* **메타데이터에** 메타데이터가 [!DNL Assets] 있습니다. 예를 들어, 작성자, 만료 날짜, DRM 정보(디지털 권한 관리) 등이 있습니다. 메타데이터에 대한 액세스를 제어할 수 있습니다. [!DNL Assets] 에서는 다음과 같은 다양한 일반적인 메타데이터 스키마를 지원합니다.

   * 더블린 코어: 작성자, 설명, 날짜, 제목 등을 포함합니다.
   * IPTC: 이벤트, 모델, 위치 등을 포함합니다.
   * WCM: 페이지 속성, [!UICONTROL 설정 시간] 및 [!UICONTROL 해제 시간]등을 포함합니다.

* **태그 지정**: [!DNL Assets] 태그 지정 및 분류할 수 있습니다. 자산 [구성을 참조하십시오](/help/assets/organize-assets.md).

* **표현물**: 표현물은 자산의 이진 표현입니다. [!DNL Assets] 항상 업로드된 파일의 기본 표현을 가집니다. 자산에는 사용자 지정된 작업 흐름 단계에 의해서나 자산이 업로드될 때 만들어지는 추가적인 표현들이 있습니다. 표현물들은 크기가 다르거나 해상도가 다르거나, 워터마크가 추가로 있거나 기타 특성이 변경되었을 수 있습니다.

* **버전**: 버전 매기기를 통해 특정 시점의 디지털 자산 스냅샷을 만들 수 있습니다. 자산을 이전 버전으로 복원할 수 있습니다. See [versioning in Assets](managing-assets-touch-ui.md#asset-versioning).

* **하위 자산**: 하위 자산은 예를 들어, 파일의 레이어나 PDF 파일의 페이지 등과 같이 자산을 구성하는 [!DNL Adobe Photoshop] 자산입니다. In [!DNL Assets], you can manage sub-assets as you would assets.

### How to work with assets {#how-to-work-with-assets}

자산 또는 컬렉션에서 작업을 수행합니다. 작업을 통해 자산, 컬렉션 및 표현물을 만들거나 수정할 수 있습니다. 자산에 대해 수행하는 많은 기본 작업(하위 자산 업로드, 삭제, 업데이트, 저장)은 사전 구성된 워크플로우를 트리거합니다. These are automatically turned on in [!DNL Assets] and are described in detail in [!DNL Assets] media handlers.

이러한 사전 구성된 워크플로우로 수행할 수 있는 작업:

* 자산을 저장소에 저장하거나 저장소에서 자산을 삭제합니다.
* 자산에 대한 메타데이터 추출 및 저장; 개별 메타데이터 항목이 XMP로 저장됩니다.
* 자산에 대한 변환 및 축소판 생성; 필요한 경우 자동 크기 조정 및 자르기 기능을 사용할 수 있습니다.
* 필요한 경우 자산을 트랜스코딩합니다. 예를 들어, 모바일 및 웹용 비디오는 초당 24프레임으로 코드가 변환되고 초당 30프레임으로 비디오를 다운로드합니다. 모바일 및 웹용 오디오는 128Kbps로 코드가 변환되고 192Kbps로 오디오를 다운로드할 수 있습니다.

물론 워크플로우도 수동으로 적용할 수 있습니다. 기본 워크플로우 목록을 알려면 [ Assets 미디어 핸들러](/help/assets/media-handlers.md)를 참조하십시오.

## [!DNL Experience Manager Assets] and [!DNL MediaLibrary] {#cq-dam-vs-cq-medialibrary}

차이점 [에 대한 자세한 내용은 에셋](/help/assets/medialibrary.md) 및 미디어 라이브러리를 참조하십시오.
