---
title: '[!DNL Adobe Experience Manager]에서 디지털 자산에 대한 메타데이터를 관리합니다.'
description: 메타데이터 유형과 [!DNL Adobe Experience Manager Assets]를 통해 자산을 위한 메타데이터를 관리하여 자산을 보다 손쉽게 분류하고 구성할 수 있는 방법을 살펴볼 수 있습니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# Manage metadata for digital assets {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] 모든 자산에 대한 메타데이터를 유지합니다. 이를 통해 보다 쉽게 에셋을 분류하고 구성할 수 있으며 특정 에셋을 찾는 사람이 여기에 포함됩니다. 업로드된 파일에서 메타데이터를 추출할 수 있는 기능을 [!DNL Experience Manager Assets]통해 메타데이터 관리는 크리에이티브 워크플로우와 통합됩니다. 에셋을 사용하여 임의의 메타데이터를 유지 및 관리할 수 있으므로 메타데이터를 기반으로 에셋을 자동으로 구성하고 처리할 [!DNL Experience Manager Assets] 수 있습니다.

* [XMP 메타데이터](xmp.md)
* [메타데이터를 편집하거나 추가하는 방법](meta-edit.md)
* [메타데이터 스키마 참조](meta-ref.md)

## 메타데이터가 필요한 이유 {#why-we-need-metadata}

메타데이터는 데이터에 대한 데이터를 의미합니다. 이러한 점에서 데이터는 처리하고 있는 자산(예: 이미지)을 나타냅니다. 메타데이터는 사용자가 보다 효율적으로 자산을 관리할 수 있도록 하기 때문에 중요합니다.

메타데이터는 이 이미지에 사용할 수 있는 모든 데이터의 집합이지만, 예를 들어, 다음 이미지에 반드시 포함되지는 않습니다.

* 자산의 이름
* 마지막으로 수정한 시간 및 날짜
* 저장소에 저장된 이미지의 크기
* 포함된 폴더의 이름

이러한 속성은 자산에 대해 관리할 [!DNL Experience Manager] 수 있는 기본 메타데이터 등록 정보로서, 사용자는 마지막 수정 날짜별로 정렬된 모든 자산을 볼 수 있습니다. 이는 최근 저장소에 추가된 자산을 검색하려고 할 때 유용합니다.

다음과 같이 고급 데이터를 디지털 자산에 추가할 수 있습니다.

* 자산 유형(이미지, 비디오, 오디오 클립 또는 문서입니까?)
* 자산의 소유자
* 자산의 제목
* 자산의 설명
* 자산에 지정된 태그

더 많은 메타데이터는 자산을 더 분류하는 데 도움이 되며 디지털 정보의 양이 증가함에 따라 유용합니다. 단 한 사람이 파일 이름을 기반으로 수백 개의 파일 목록을 관리할 수 있지만, 이 방법은 관련된 사람의 수와 관리되는 자산의 수가 증가할 때 부족합니다.

메타데이터가 자산에 추가되면 자산이

* 접근성 향상 - 보다 손쉽게 검색
* 간편해진 관리 - 동일한 속성 세트를 사용하여 보다 손쉽게 에셋을 찾을 수 있고 변경 사항을 적용할 수 있습니다.
* 보다 복잡함 - 자산에 추가한 메타데이터가 많을수록 메타데이터 관리가 더 중요해집니다

이러한 이유로 [!DNL Assets] 디지털 자산에 대한 메타데이터를 제작, 관리 및 교환할 수 있는 적절한 방법을 제공합니다.

## 메타데이터 기본 사항 {#metadata-basics}

메타데이터는 가져오기(인제스트)되면 자산에서 추출됩니다. 또한 메타데이터를 추가하면 자산을 더 분류할 수 있습니다.

이 섹션에서는 메타데이터 및 인코딩 표준의 유형을 다룹니다.

### 메타데이터 유형 {#types-of-metadata}

다음과 같은 두 가지 기본 유형의 메타데이터가 있습니다.

* 기술 메타데이터
* 설명 메타데이터

#### 기술 메타데이터 {#technical-metadata}

기술 메타데이터는 디지털 자산을 처리하는 소프트웨어 애플리케이션에 유용하며 수동으로 유지해서는 안 됩니다. 기술 메타데이터는 [!DNL Experience Manager Assets] 및 기타 소프트웨어에 의해 자동으로 결정되며 에셋이 수정되면 변경될 수 있습니다. 자산의 사용 가능한 기술 메타데이터는 대개 자산의 파일 유형에 따라 달라집니다. 기술 메타데이터의 예는 다음과 같습니다.

* 파일 크기
* 이미지의 크기(높이 및 폭)
* 오디오 또는 비디오 파일의 비트 전송률
* 이미지의 해상도(세부 수준)

#### 설명 메타데이터 {#descriptive-metadata}

설명 메타데이터는 애플리케이션 도메인과 관련된 메타데이터입니다. 예를 들어, 자산이 시작되는 비즈니스. 설명 메타데이터는 자동으로 결정할 수 없습니다. 수동 또는 반자동 생성되어야 합니다. 예를 들어 GPS 지원 카메라는 이미지를 촬영한 위도와 경도를 자동으로 추적하고 이 정보를 이미지의 메타데이터에 추가할 수 있습니다.

수사적 메타데이터 정보를 작성하는 데 필요한 수작업에 소요되는 많은 비용 때문에 소프트웨어 시스템 및 조직 전체에서 메타데이터를 간편하게 교환할 수 있는 기준이 마련되었습니다.

[!DNL Experience Manager Assets] 은 메타데이터 관리에 대한 모든 관련 표준을 지원합니다.

메타데이터의 중요성과 메타데이터를 만드는 데 필요한 수동 작업이 중요하므로 보다 손쉽게 교환할 수 있는 표준이 마련되었습니다.

### 인코딩 표준 {#encoding-standards}

메타데이터는 파일에 임베드할 수 있는 다양한 방법이 있습니다. 다양한 인코딩 표준이 지원됩니다.

* XMP:추출된 메타데이터를 저장소 내에 저장하는 [!DNL Assets] 데 사용됩니다.
* ID3:for audio and video files.
* EXIF:for image files.
* 기타/레거시:Microsoft Word, PowerPoint, Excel 등에서 사용할 수 있습니다.

#### XMP {#xmp}

XMP는 확장 가능한 메타데이터 플랫폼을 의미하며 모든 메타데이터 관리에 사용되는 메타데이터 표준입니다. [!DNL Experience Manager Assets] XMP는 모든 파일 포맷에 임베드할 수 있는 범용 메타데이터 인코딩을 제공할 뿐만 아니라 Adobe 및 다른 회사에서 지원하는 리치 컨텐츠 모델을 제공하므로 XMP 사용자는 강력한 플랫폼을 통해 구축할 수 [!DNL Experience Manager Assets] 있습니다.

#### ID3 {#id}

이러한 ID3 태그에 저장된 데이터는 컴퓨터 또는 휴대용 MP3 플레이어에서 디지털 오디오 파일을 재생할 때 표시됩니다.

ID3 태그는 MP3 파일 포맷용으로 설계되었습니다. 형식에 대한 추가 정보:

* ID3 태그는 MP3 및 MP3pro 파일에서 작동합니다.
* WAV에는 태그가 없습니다.
* WMA에는 오픈 소스 구현을 허용하지 않는 전용 태그가 있습니다.
* Ogg Vorbis는 Ogg 컨테이너에 포함된 Xiph 주석을 사용합니다.
* AAC는 독점적인 태그 지정 형식을 사용합니다.

#### EXIF {#exif}

EXIF는 Exchangeable 이미지 파일 포맷을 의미하며 디지털 사진 작업에 가장 많이 사용되는 메타데이터 포맷입니다. JPEG, TIFF, RIFF 및 WAV와 같은 다양한 파일 형식으로 메타데이터 속성의 고정 용어를 포함하는 방법을 제공합니다.

EXIF의 주요 제한 사항은 BMP, GIF 또는 PNG와 같이 널리 사용되는 다른 이미지 파일 형식에서는 지원되지 않는다는 것입니다.

EXIF는 메타데이터를 메타데이터 이름 및 메타데이터 값의 쌍으로 저장합니다. 이러한 메타데이터 이름-값 쌍은 태그라고도 하며 에서 태깅과 혼동하지 않도록 [!DNL Experience Manager]합니다.

EXIF는 최신 디지털 카메라에서 자동으로 제작되고 최신 그래픽 소프트웨어를 통해 지원되므로 메타데이터 관리를 위한 가장 낮은 공통 분모로 간주할 수 있습니다.

EXIF로 정의된 대부분의 메타데이터 필드는 기술적으로 매우 유용하며 설명적인 메타데이터 관리를 위해 제한된 용도로만 사용됩니다. 이러한 이유로 [!DNL Assets] EXIF 속성을 [일반적인 메타데이터 구성표와 XMP로](metadata-schemas.md) 매핑하는 기능을 [통해](xmp-writeback.md)메타데이터 관리를 [!DNL Assets] 위해 사용되는 강력한 메타데이터 형식을 제공합니다.

#### 기타 메타데이터 {#other-metadata}

파일에서 포함할 수 있는 기타 메타데이터에는 Microsoft Word, PowerPoint, Excel 등이 있습니다.

## 메타데이터 스키마 {#metadata-schemata}

메타데이터 스키마는 다양한 애플리케이션에서 사용할 수 있는 메타데이터 속성 정의의 사전 정의된 세트입니다. 속성은 항상 자산과 연결되어 있습니다. 즉, 속성은 리소스에 대한 것입니다.

또한 필요에 맞는 메타데이터 스키마를 설계할 수도 있습니다. 단, 이미 존재하는 구성 요소를 복제하지 마십시오. 조직 내에서 스키마를 구분하면 조직 간에 메타데이터를 쉽게 공유할 수 있습니다.

[!DNL Experience Manager] 은 가장 널리 사용되는 메타데이터 스키마 목록을 제공하므로 메타데이터 전략을 바로 시작하고 이미 정의된 스키마에서 필요한 메타데이터 속성을 선택할 수 있습니다.

지원되는 메타데이터 스키마가 다음 섹션에 나열되어 있습니다.

### 표준 메타데이터 {#standard-metadata}

* dc - Dublin Core - 가장 중요하고 널리 사용되는 메타데이터 집합
* DICOM - 의료 분야의 디지털 이미징 및 커뮤니케이션
* Iptc4xmpCore &amp; iptc4xmpExt - International Press Communications Standard - 다양한 분야별 메타데이터
* rdf - 리소스 설명 프레임워크 - 일반 의미론적 웹 메타데이터
* xmp - 확장 가능한 메타데이터 플랫폼
* xmpBJ - 기본 작업 티켓

### 애플리케이션별 메타데이터 {#application-specific-metadata}

>[!NOTE]
>
>애플리케이션별 메타데이터에는 기술 및 설명 메타데이터가 포함됩니다. 이러한 경우 다른 응용 프로그램에서 메타데이터를 사용할 수 없을 수 있습니다. 예를 들어 Adobe Photoshop 메타데이터가 있는 에셋을 보유하고 있고 다른 이미지 렌더링 응용 프로그램이 메타데이터에 액세스하려고 하는 경우 해당 메타데이터에 액세스할 수 없을 수 있습니다.
>
>자산에 애플리케이션별 메타데이터가 많이 있는 경우 애플리케이션별 속성을 표준 메타데이터로 변경하는 워크플로우 단계를 만들 수 있습니다.

* acdsee - ACDSee 프로그램 www.acdsee.com [/](https://www.acdsee.com/)
* album - Adobe Photoshop Album
* cq - [!DNL Experience Manager Assets]
* dam - 사용 [!DNL Experience Manager Assets]
* dex - SC 설명 탐색기 최적화
* crs - Adobe Photoshop Camera Raw
* lr - Adobe Lightroom
* mediapro - IView MediaPro
* MicrosoftPhoto 및 MP - Microsoft Photo
* pdf amd pdfx
* photoshop &amp; psAux - Adobe Photoshop

### 디지털 권한 관리 메타데이터 {#digital-rights-management-metadata}

* cc - creative commons
* xmpRights
* plus - Picture Licensing Universal System - https://www.useplus.com/
* 프리즘 - https://www.idealliance.org/prism-metadata Standard 메타데이터에 대한 게시 요구 사항
* prl - 프리즘 권한 언어
* pur - 프리즘 사용 권한
* xmpPlus - PLUS와 XMP 통합

### 포토그래피 특정 메타데이터 {#photography-specific-metadata}

* exif - GPS 위치 등 카메라의 많은 기술 정보
* crs - photoshop camera raw
* Iptc4xmpCore 및 iptc4xmpExt
* TIFF - 이미지 메타데이터(TIFF 이미지 전용 아님)

### 인쇄별 메타데이터 {#print-specific-metadata}

* pdf 및 pdfx - Adobe PDF 및 타사 애플리케이션
* 프리즘 - [www.prismstandard.org](https://www.prismstandard.org) 업계 표준 메타데이터를 위한 게시 요구 사항
* xmp
* xmpPG - 페이지 지정된 텍스트의 xmp

### 멀티미디어별 메타데이터 {#multimedia-specific-metadata}

* xmpDM - Dynamic Media
* xmpMM - 미디어 관리

## 메타데이터 중심의 워크플로우 {#metadata-driven-workflows}

메타데이터 중심의 워크플로우를 만들면 일부 프로세스를 자동화하여 효율성을 높일 수 있습니다. 메타데이터 중심의 워크플로우에서 워크플로우 관리 시스템은 워크플로우를 읽고 그 결과 미리 정의된 일부 작업을 수행합니다.

예를 들어, 메타데이터 중심의 워크플로우를 사용할 수 있는 방법 중 몇 가지를 제공합니다.

* 워크플로우는 이미지에 제목이 있는지 여부를 확인할 수 있습니다. 그렇지 않으면 특정 사용자에게 제목을 추가하도록 알립니다.
* 워크플로우는 자산에 대한 저작권 공지가 배포를 허용하는지 여부를 확인할 수 있습니다. 그런 경우, 시스템이 자산을 하나의 서버로 전송합니다. 그렇지 않으면 시스템이 자산을 다른 서버로 보냅니다.
