---
title: Adobe Experience Manager 자산 정보
description: 디지털 자산 관리란 무엇이고, 사용 사례는 물론, Adobe의 Experience Manager 에셋 솔루션인지 살펴보십시오
contentOwner: AG
translation-type: tm+mt
source-git-commit: a61e1e9ffb132b59c725b2078f09641a3c2a479a
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 52%

---


# Administer assets {#administering-assets}

자산은 Experience Manager 플랫폼과 완전히 통합된 DAM(Digital Asset Management) 툴로, 기업은 디지털 자산을 공유하고 배포할 수 있습니다. 조직의 사용자는 이미지, 비디오, 문서, 오디오 클립 및 리치 미디어(예: 웹용 Flash 파일, 인쇄물 및 디지털 배포용 미디어)를 관리, 저장 및 액세스할 수 있습니다.

## 디지털 자산 관리란 무엇입니까? {#what-is-digital-asset-management}

Assets는 조직의 핵심 디지털 자산의 엔터프라이즈 범위 공유 및 분배 기능을 제공합니다. Users across an organization can store, manage, and access digital assets such as images, graphics, audio, video, and documents through a Web interface (or a CIFS or WebDAV folder).

Experience Manager과 긴밀하게 통합된 에셋 기능을 통해 다음을 수행할 수 있습니다.

* 이미지, 문서, 오디오 파일 및 비디오 파일을 다양한 파일 형식으로 추가하고 공유합니다.
* 자산을 태그, 라이트박스 또는 별(즐겨찾기)별로 그룹화하여 관리합니다. 자산에 주석을 추가합니다.
* 파일 이름, 문서의 전체 텍스트, 날짜, 문서 유형 및 태그를 검색하여 자산을 찾습니다.
* 자산에 관한 메타데이터 정보를 추가하거나 편집합니다. 메타데이터는 해당 자산에 따라 자동으로 버전이 매겨집니다. 자산 메타데이터를 가져오거나 내보낼 수 있습니다.
* 이미지 필터 추가 및 크기 조절과 같은 이미지 편집 기능을 수행합니다. WebDAV 또는 CIFS 폴더를 사용하여 여러 디지털 자산을 동시에 가져오고 내보냅니다.
* 워크플로우 및 알림을 사용하여 자산 세트를 공동 처리 및 다운로드하고 자산에 대한 액세스 권한을 관리할 수 있도록 합니다.

### Experience Manager 사이트와 통합된 Experience Manager 자산 {#aem-assets-fully-integrated-in-cq-wcm}

에셋은 사이트와 완벽하게 통합되어 모든 기능을 매끄럽게 사용할 수 있습니다. 그런 다음 웹 페이지를 작성할 때 컨텐츠 파인더를 통해 자산 저장소 내에서 관리되는 디지털 자산에 액세스할 수 있습니다.

기본 사용자 인터페이스는 사이트의 사용자 인터페이스와 동일합니다. 자세한 [내용은 사이트](/help/sites-authoring/page-authoring.md) 개요를 참조하십시오.

### 디지털 자산 관리와 이미지 구성 요소 {#digital-asset-management-versus-image-component}

DAM 저장소에 이미지를 넣을지, 이미지 구성 요소를 사용할지를 결정할 때 이미지 수명주기를 고려하십시오.

* 이미지의 라이프사이클이 페이지의 라이프사이클과 동일하다면 이미지 구성 요소를 사용하십시오.
* 이미지에 별도의 라이프사이클이 있는 경우(예: 이미지를 두 번 사용하거나 또는 WCM 외부에서 사용하는 경우)  Assets를 사용하십시오.

## 디지털 자산이란 무엇입니까? {#what-are-digital-assets}

자산은 여러 표현물을 가질 수 있고 하위 자산(예: photoshop 파일의 레이어, PowerPoint 파일의 슬라이드, pdf의 페이지, ZIP의 파일)을 가질 수 있는 디지털 문서, 이미지, 비디오 또는 오디오입니다.

근본적으로 자산은 이진, 메타데이터, 표현물, 하위 자산이 합쳐진 것입니다. 자세한 내용은 [DAM 성능 안내서](/help/sites-deploying/assets-performance-sizing.md)를 참조하십시오.

>[!CAUTION]
>
>대량의 자산(특히 이미지)을 업로드 및/또는 편집하면 Experience Manager 인스턴스의 성능에 영향을 줄 수 있습니다.

### Experience Manager 자산 용어 {#aem-assets-terminology}

Experience Manager에서 디지털 자산으로 작업하는 경우 다음 용어를 이해해야 합니다.

* **컬렉션** 실제 위치(폴더), 공용 속성(저장된 검색 폴더) 또는 사용자 선택(lightbox 폴더)을 기반으로 하는 자산의 컬렉션입니다.

* **메타데이터** 자산에는 메타데이터가 있습니다. 예를 들어, 작성자, 만료 날짜, DRM 정보(디지털 권한 관리) 등이 있습니다. 메타데이터에 대한 액세스를 제어할 수 있습니다.  Assets는 특히 다음과 같은 다양한 공통 메타데이터 스키마를 지원합니다.

   * 더블린 코어: 작성자, 설명, 날짜, 제목 등을 포함합니다.
   * IPTC: 이벤트, 모델, 위치 등을 포함합니다.
   * WCM: 페이지 속성, [!UICONTROL 설정 시간] 및 [!UICONTROL 해제 시간]등을 포함합니다.

* **태그 지정** 자산은 태그를 지정하고 분류할 수 있습니다. 태그 사용 및 태그 관리를 참조하십시오.

* **표현물** 변환은 자산의 이진 표현입니다. 자산에는 항상 업로드한 파일의 표현인 기본 표현이 있습니다. 자산에는 사용자 지정된 작업 흐름 단계에 의해서나 자산이 업로드될 때 만들어지는 추가적인 표현들이 있습니다. 표현물들은 크기가 다르거나 해상도가 다르거나, 워터마크가 추가로 있거나 기타 특성이 변경되었을 수 있습니다.

* **버전** 버전 관리 기능을 사용하면 특정 시점의 디지털 자산 스냅샷을 만들 수 있습니다. 자산을 이전 버전으로 복원할 수 있습니다. See [versioning in Assets](managing-assets-touch-ui.md#asset-versioning).

* **하위 자산** 하위 자산은 예를 들어, Adobe Photoshop 파일의 레이어나 PDF 파일의 페이지 같은 자산을 구성하는 자산입니다.  Assets에서는 하위 자산도 자산처럼 관리할 수 있습니다.

### How to work with assets {#how-to-work-with-assets}

자산 또는 컬렉션에서 작업을 수행합니다. 작업을 통해 자산, 컬렉션 및 표현물을 만들거나 수정할 수 있습니다. 자산에 대해 수행하는 많은 기본 작업(하위 자산 업로드, 삭제, 업데이트, 저장)은 사전 구성된 워크플로우를 트리거합니다. 이러한 워크플로우는 Assets에서 자동으로 켜지고,  Assets 미디어 핸들러에서 자세히 설명됩니다.

이러한 사전 구성된 워크플로우로 수행할 수 있는 작업:

* 자산을 저장소에 저장, 또는 저장소에서 자산을 삭제합니다.
* 자산에 대한 메타데이터 추출 및 저장. 개별 메타데이터 항목은 XMP로 저장됩니다.
* 필요할 경우 자동 크기 조정 및 자르기를 포함한 자산의 표현물과 썸네일을 생성합니다.
* 필요할 경우 자산의 코드를 변환합니다. 예를 들어, 모바일 및 웹용 비디오는 초당 24프레임으로 코드가 변환되고 초당 30프레임으로 비디오를 다운로드합니다. 모바일 및 웹용 오디오는 128kbps로 코드가 변환되고 192kbps로 오디오를 다운로드합니다.

물론 워크플로우도 수동으로 적용할 수 있습니다. 기본 워크플로우 목록을 알려면 [ Assets 미디어 핸들러](/help/assets/media-handlers.md)를 참조하십시오.

## Experience Manager 에셋 및 미디어 라이브러리 {#cq-dam-vs-cq-medialibrary}

차이점 [에 대한 자세한 내용은 에셋](/help/assets/medialibrary.md) 및 미디어 라이브러리를 참조하십시오.
