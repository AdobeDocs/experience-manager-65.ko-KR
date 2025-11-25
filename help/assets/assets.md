---
title: ' [!DNL Adobe Experience Manager Assets] 소개'
description: Experience Manager에서 디지털 자산을 작성하고, 관리하며, 처리하고, 배포합니다. 이 안내서에서는 모범 사례, 접근성 기능 및 AEM 6.5 자산 사용 방법에 대해 설명합니다.
hide: true
feature: Asset Management
role: Leader, Developer, User
exl-id: 68239634-a2e8-414e-a866-cd8082641ee8
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 4%

---


# DAM 솔루션으로서의 [!DNL Adobe Experience Manager Assets] 정보 {#administering-assets}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/assets/overview) |
| AEM 6.5 | 이 문서 |

AEM [!DNL Assets]은(는) [!DNL Experience Manager] 플랫폼의 일부이며 기업이 디지털 자산을 관리하고 배포할 수 있도록 해 주는 DAM(디지털 자산 관리) 도구입니다. 조직의 사용자는 웹, 인쇄 및 디지털 배포에 사용할 이미지, 비디오, 문서, 오디오 클립, 3D 파일 및 리치 미디어와 같은 다양한 유형의 디지털 자산을 관리, 저장 및 액세스할 수 있습니다.

## Digital Asset Management 소개 {#what-is-digital-asset-management}

[!DNL Assets]은(는) 조직의 주요 디지털 자산을 전사적으로 공유하고 배포합니다. 조직의 사용자는 웹 인터페이스(또는 CIFS 또는 WebDAV 폴더)를 통해 이미지, 그래픽, 오디오, 비디오 및 문서와 같은 디지털 자산을 저장, 관리 및 액세스할 수 있습니다.

[!DNL Assets]의 [!DNL Experience Manager] 기능을 사용하면 다음 작업을 수행할 수 있습니다.

* 이미지, 문서, 오디오 파일 및 비디오 파일을 다양한 파일 형식으로 추가 및 공유할 수 있습니다.
* 태그, Lightbox 또는 별(즐겨찾기)로 그룹화하여 자산을 관리합니다. 자산에 주석을 추가합니다.
* 파일 이름, 문서의 전체 텍스트, 날짜, 문서 유형 및 태그를 검색하여 자산을 찾습니다.
* 에셋의 메타데이터 정보를 추가하거나 편집합니다. 메타데이터는 해당 에셋과 함께 자동으로 버전이 지정됩니다. 에셋 메타데이터를 가져오거나 내보낼 수 있습니다.
* 이미지 필터 크기 조절 및 추가와 같은 이미지 편집 기능을 수행합니다. WebDAV 또는 CIFS 폴더를 사용하여 여러 디지털 에셋을 동시에 가져오거나 내보냅니다.
* 워크플로우 및 알림을 사용하여 모든 에셋 세트의 공동 처리 및 다운로드를 허용하고 에셋에 대한 액세스 권한을 관리합니다.

### [!DNL Experience Manager Assets]이(가) [!DNL Experience Manager Sites]과(와) 통합되었습니다. {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets]은(는) [!DNL Sites]과(와) 완전히 통합되며 모든 사용 사례에 대해 원활하게 작동합니다. 예를 들어 웹 페이지를 작성할 때 [!DNL Sites] 작성자는 콘텐츠 파인더를 통해 디지털 자산을 찾아 사용할 수 있습니다. [!DNL Assets]의 사용자 인터페이스가 [!DNL Sites]의 사용자 인터페이스와 같습니다. 자세한 내용은 [사이트 개요](/help/sites-authoring/page-authoring.md)를 참조하십시오.

기본 사용자 인터페이스는 [!DNL Sites]과(와) 동일합니다. 자세한 내용은 [사이트 개요](/help/sites-authoring/page-authoring.md)를 참조하십시오.

### 디지털 자산 관리 및 이미지 구성 요소 {#digital-asset-management-versus-image-component}

이미지를 DAM 저장소에 저장할지 또는 이미지 구성 요소를 사용할지 여부를 결정할 때 이미지 라이프사이클을 고려하십시오.

* 이미지에 페이지와 같은 주기가 있는 경우 이미지 구성 요소를 사용합니다.
* 이미지에 별도의 수명 주기가 있는 경우, 예를 들어 이미지를 두 번 사용하거나 WCM 외부에서 사용하는 경우 [!DNL Assets]을(를) 사용하십시오.

## 디지털 자산이란? {#what-are-digital-assets}

에셋은 디지털 문서, 이미지, 비디오, 오디오 또는 그 일부로, 다양한 표현물을 가질 수 있습니다. 하위 자산(예: Photoshop 파일의 레이어, PowerPoint 파일의 슬라이드, pdf의 페이지, ZIP에 있는 파일)도 있을 수 있습니다.

에셋은 기본적으로 바이너리와 메타데이터, 렌디션과 하위 에셋입니다. 자세한 내용은 [DAM 성능 안내서](/help/sites-deploying/assets-performance-sizing.md)를 참조하십시오.

>[!CAUTION]
>
>대량의 자산(특히 이미지)을 업로드하거나 편집하면 [!DNL Experience Manager] 배포의 성능에 영향을 줄 수 있습니다.

### [!DNL Experience Manager Assets] 용어 {#aem-assets-terminology}

[!DNL Experience Manager]에서 디지털 에셋으로 작업할 때 다음 용어를 이해하는 것이 좋습니다.

* **컬렉션**: 실제 위치(폴더), 일반 속성(저장된 검색 폴더) 또는 사용자 선택(Lightbox 폴더)을 기반으로 하는 에셋의 컬렉션입니다.

* **메타데이터** [!DNL Assets]에 작성자, 만료 날짜 및 DRM 정보(Digital Rights Management)와 같은 메타데이터가 있습니다. 메타데이터가 액세스 제어 하에 있습니다. [!DNL Assets]은(는) 기본적으로 다음과 같은 다양한 일반 메타데이터 스키마를 지원합니다.

   * 더블린 코어: 작성자, 설명, 날짜, 주제 등을 포함합니다.
   * IPTC: 이벤트, 모델, 위치 등을 포함합니다.
   * WCM: 페이지 속성, [!UICONTROL 설정 시간] 및 [!UICONTROL 해제 시간] 등을 포함합니다.

* **태그 지정**: [!DNL Assets]에 태그를 지정하고 분류할 수 있습니다. [자산 구성](/help/assets/organize-assets.md)을 참조하세요.

* **렌디션**: 렌디션은 에셋의 이진 표현입니다. [!DNL Assets]은(는) 항상 업로드된 파일의 기본 표현을 사용합니다. 예를 들어 사용자 지정된 워크플로우 단계에 의해 또는 에셋을 업로드할 때 만들어지는 추가 표현을 얼마든지 사용할 수 있습니다. 렌디션의 크기가 다르고 해상도가 다르고 워터마크가 추가되거나 다른 특성이 변경될 수 있습니다.

* **버전**: 버전 관리를 수행하면 특정 시점에 디지털 에셋의 스냅숏이 만들어집니다. 자산을 이전 버전으로 복원할 수 있습니다. [버전 관리 [!DNL Assets]](manage-assets.md#asset-versioning)를 참조하십시오.

* **하위 자산**: 하위 자산은 자산을 구성하는 자산입니다(예: [!DNL Adobe Photoshop] 파일의 레이어 또는 PDF 파일의 페이지). [!DNL Assets]에서 에셋과 마찬가지로 하위 에셋을 관리할 수 있습니다.

### 디지털 에셋으로 작업하는 방법 {#how-to-work-with-assets}

에셋 또는 컬렉션에 대해 작업을 수행합니다. 작업은 에셋, 컬렉션 및 변환을 만들거나 수정할 수 있습니다. 에셋에 대해 수행하는 많은 기본 작업(하위 에셋 업로드, 삭제, 업데이트, 저장)은 사전 구성된 워크플로우를 트리거합니다. 이러한 기능은 [!DNL Assets]에서 자동으로 켜지며 [!DNL Assets] 미디어 처리기에 자세히 설명되어 있습니다.

이러한 사전 구성된 워크플로우로 수행할 수 있는 작업은 다음과 같습니다.

* 저장소에 에셋을 저장하거나 저장소에서 에셋을 삭제합니다.
* 에셋의 메타데이터를 추출하고 저장합니다. 개별 메타데이터 항목은 XMP으로 저장됩니다.
* 필요한 경우 자동 크기 조정 및 자르기를 포함하여 에셋의 렌디션 및 썸네일을 생성합니다.
* 필요한 경우 에셋을 코드 변환합니다. 예를 들어 모바일 및 웹 사용용 비디오는 초당 24프레임으로 트랜스코딩되고, 초당 30프레임으로 비디오를 다운로드합니다. 모바일 및 웹 사용을 위한 오디오는 128Kbps로 트랜스코딩되고, 다운로드를 위한 오디오는 192Kbps로 트랜스코딩됩니다.

워크플로우를 수동으로 적용할 수도 있습니다. 기본 워크플로 목록은 [Assets 미디어 핸들러](media-handlers.md)를 참조하십시오.

## [!DNL Experience Manager Assets] 및 [!DNL Media Library] {#cq-dam-vs-cq-medialibrary}

차이점에 대한 자세한 내용은 [Assets 및 미디어 라이브러리](medialibrary.md)를 참조하십시오.

>[!MORELIKETHIS]
>
>* [비디오 소개 - 최신 DAM으로 Experience Manager Assets](https://www.youtube.com/watch?v=PBwQqZgC-yo)
>* [메타데이터 개념 이해](/help/assets/metadata-concepts.md)
