---
title: '[!DNL Adobe Experience Manager]에서 디지털 자산의 메타데이터를 관리할 수 있습니다.'
description: 메타데이터 유형과 [!DNL Adobe Experience Manager Assets]를 통해 자산을 위한 메타데이터를 관리하여 자산을 보다 손쉽게 분류하고 구성할 수 있는 방법을 살펴볼 수 있습니다. [!DNL Experience Manager]를 사용하면 메타데이터를 기반으로 자산을 자동으로 구성하고 처리할 수 있습니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# 디지털 자산의 메타데이터 관리 {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] 모든 자산에 대한 메타데이터를 유지합니다. 이를 통해 보다 손쉽게 에셋을 분류하고 구성할 수 있으며 특정 에셋을 찾는 사람도 지원할 수 있습니다. 업로드된 파일에서 메타데이터를 추출할 수 있는 기능을 [!DNL Experience Manager Assets]통해 메타데이터 관리는 크리에이티브 워크플로우와 통합됩니다. 에셋으로 메타데이터를 유지 및 관리할 수 있으므로 메타데이터를 기반으로 에셋을 자동으로 구성하고 처리할 [!DNL Experience Manager Assets] 수 있습니다.

* [XMP 메타데이터](xmp.md).
* [메타데이터를](meta-edit.md)편집하거나 추가하는 방법
* [메타데이터 스키마 참조](meta-ref.md).

## 메타데이터가 필요한 이유 {#why-we-need-metadata}

메타데이터는 데이터에 대한 데이터를 의미합니다. 이러한 점에서 데이터는 디지털 자산, 즉 이미지를 나타냅니다. 메타데이터는 효율적인 에셋 관리를 위해 매우 중요합니다.

메타데이터는 자산에 사용할 수 있는 모든 데이터의 집합이지만 해당 이미지에 반드시 포함되어 있지는 않습니다. 메타데이터의 일부 예는 다음과 같습니다.

* 자산의 이름입니다.
* 마지막 수정 날짜 및 시간
* 저장소에 저장된 자산의 크기입니다.
* 포함된 폴더의 이름입니다.
* 관련 자산 또는 적용된 태그

이러한 속성은 자산에 대해 관리할 [!DNL Experience Manager] 수 있는 기본 메타데이터 등록 정보로서, 사용자는 마지막 수정 날짜별로 정렬된 모든 자산을 볼 수 있습니다. 이는 최근 저장소에 추가된 자산을 검색하려고 할 때 유용합니다.

다음과 같이 고급 데이터를 디지털 자산에 추가할 수 있습니다.

* 자산 유형(이미지, 비디오, 오디오 클립 또는 문서입니까?).
* 자산의 소유자입니다.
* 자산의 제목입니다.
* 자산에 대한 설명입니다.
* 자산에 지정된 태그.

더 많은 메타데이터는 자산을 더 분류하는 데 도움이 되며 디지털 정보의 양이 증가함에 따라 유용합니다. 파일 이름만 기준으로 수백 개의 파일을 관리할 수 있습니다. 그러나 관련된 사람의 수와 관리되는 에셋 수가 증가하면 이러한 접근 방식은 확장 가능하고 빠르게 떨어지지 않습니다.

메타데이터가 추가되면, 에셋은

* 보다 손쉽게 액세스 가능 - 시스템과 사용자가 손쉽게 찾을 수 있습니다.
* 간편해진 관리 - 동일한 속성 세트를 사용하여 보다 손쉽게 에셋을 찾을 수 있고 변경 사항을 적용할 수 있습니다.
* 더 완성도 - 자산에 추가한 메타데이터가 많을수록 더 많은 정보와 컨텍스트가 포함됩니다.

이러한 이유로 [!DNL Assets] 디지털 자산에 대한 메타데이터를 제작, 관리 및 교환할 수 있는 적절한 방법을 제공합니다.

## 메타데이터 유형 {#types-of-metadata}

두 가지 기본 메타데이터 유형은 기술 메타데이터와 설명 메타데이터입니다.

기술 메타데이터는 디지털 자산을 처리하는 소프트웨어 애플리케이션에 유용하며 수동으로 유지해서는 안 됩니다. [!DNL Experience Manager Assets] 및 기타 소프트웨어는 기술 메타데이터를 자동으로 결정하며 에셋이 수정되면 메타데이터가 변경될 수 있습니다. 자산의 사용 가능한 기술 메타데이터는 대개 자산의 파일 유형에 따라 달라집니다. 기술 메타데이터의 몇 가지 예는 다음과 같습니다.

* 파일의 크기입니다.
* 이미지의 크기(높이 및 폭)입니다.
* 오디오 또는 비디오 파일의 비트 전송률입니다.
* 이미지의 해상도(세부 수준).

설명 메타데이터는 애플리케이션 도메인과 관련된 메타데이터입니다. 예를 들어, 자산이 시작되는 비즈니스. 설명 메타데이터는 자동으로 결정할 수 없습니다. 수동 또는 반자동 생성됩니다. 예를 들어 GPS 지원 카메라는 위도와 경도를 자동으로 추적하고 이미지에 지리 태그를 추가할 수 있습니다.

수사적 메타데이터 정보를 작성하는 데 필요한 수작업에 소요되는 많은 비용 때문에 소프트웨어 시스템 및 조직 전체에서 메타데이터를 간편하게 교환할 수 있는 기준이 마련되었습니다.

[!DNL Experience Manager Assets] 은 메타데이터 관리에 대한 모든 관련 표준을 지원합니다.

메타데이터의 중요성과 메타데이터를 만드는 데 필요한 수동 작업이 중요하므로 보다 손쉽게 교환할 수 있는 표준이 마련되었습니다.

## 인코딩 표준 {#encoding-standards}

파일에 메타데이터를 임베드하는 다양한 방법이 있습니다. 다양한 인코딩 표준이 지원됩니다.

* XMP:추출된 메타데이터를 저장소 내에 저장하는 [!DNL Assets] 데 사용됩니다.
* ID3:for audio and video files.
* Exif:for image files.
* 기타/레거시:출처: [!DNL Microsoft Word][!DNL PowerPoint], [!DNL Excel]and so on.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP)는 모든 메타데이터 관리에 사용되는 개방형 [!DNL Experience Manager Assets] 표준입니다. 표준은 모든 파일 포맷에 임베드할 수 있는 범용 메타데이터 인코딩을 제공합니다. Adobe와 다른 회사는 리치 컨텐츠 모델을 제공하므로 XMP 표준을 지원합니다. XMP 표준과 XMP 사용자는 강력한 플랫폼을 [!DNL Experience Manager Assets] 사용하여 구축할 수 있습니다. 자세한 내용은 XMP를 [참조하십시오](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

이러한 ID3 태그에 저장된 데이터는 컴퓨터 또는 휴대용 MP3 플레이어에서 디지털 오디오 파일을 재생할 때 표시됩니다.

ID3 태그는 MP3 파일 포맷용으로 설계되었습니다. 형식에 대한 추가 정보:

* ID3 태그는 MP3 및 mp3PRO 파일에서 작동합니다.
* WAV에는 태그가 없습니다.
* WMA에는 오픈 소스 구현을 허용하지 않는 전용 태그가 있습니다.
* Ogg Vorbis는 Ogg 컨테이너에 포함된 Xiph 주석을 사용합니다.
* AAC는 독점적인 태그 지정 형식을 사용합니다.

### Exif {#exif}

Exchange 이미지 파일 형식(Exif)은 디지털 사진 작업에 가장 많이 사용되는 메타데이터 형식입니다. JPEG, TIFF, RIFF 및 WAV와 같은 다양한 파일 포맷으로 메타데이터 속성의 고정 용어를 임베드할 수 있는 방법을 제공합니다. Exif는 메타데이터를 메타데이터 이름 및 메타데이터 값의 쌍으로 저장합니다. 이러한 메타데이터 이름-값 쌍은 태그라고도 하며 에서 태깅과 혼동하지 않도록 [!DNL Experience Manager]합니다. Exif는 최신 디지털 카메라에서 자동으로 제작되고 최신 그래픽 소프트웨어를 통해 지원되므로 메타데이터 관리를 위한 가장 일반적인 분모로 볼 수 있습니다.

Exif의 주요 제한 사항은 BMP, GIF 또는 PNG와 같이 널리 사용되는 몇 가지 이미지 파일 형식이 지원되지 않는다는 것입니다.

일반적으로 Exif에서 정의한 메타데이터 필드는 기술적으로 정의되며 수사적 메타데이터 관리를 위해 제한된 용도로 사용됩니다. 이러한 이유로 [!DNL Experience Manager Assets] Exif 속성을 [일반적인 메타데이터 구성표와 XMP에](metadata-schemas.md) 매핑하는 [기능을 제공합니다](xmp-writeback.md).

### 기타 메타데이터 {#other-metadata}

파일에서 포함할 수 있는 기타 메타데이터에는 Microsoft Word, PowerPoint, Excel 등이 있습니다.

## 메타데이터 스키마 {#metadata-schemata}

메타데이터 스키마는 다양한 애플리케이션에서 사용할 수 있는 메타데이터 속성 정의의 사전 정의된 세트입니다. 속성은 항상 자산과 연결되어 있습니다. 즉, 속성이 &#39;정보&#39;임을 의미합니다.

또한 필요에 맞는 메타데이터가 없는 경우 고유한 메타데이터 스키마를 디자인할 수 있습니다. 기존 정보를 복제하지 마십시오. 조직 내에서 스키마를 구분하면 메타데이터를 쉽게 공유할 수 있습니다. [!DNL Experience Manager] 가장 인기 있는 메타데이터 스키마 기본 목록을 제공합니다. 이 목록을 사용하면 메타데이터 전략을 바로 시작하고 필요한 메타데이터 속성을 신속하게 선택할 수 있습니다.

지원되는 메타데이터 스키마가 아래에 나열되어 있습니다.

### 표준 메타데이터 {#standard-metadata}

* dc - [!DNL Dublin Core] 가장 중요하고 널리 사용되는 메타데이터 세트입니다.
* DICOM - 의료 분야의 디지털 이미징 및 커뮤니케이션
* Iptc4xmpCore &amp; iptc4xmpExt - International Press Communications Standard에는 여러 제목별 메타데이터가 포함되어 있습니다.
* rdf - 리소스 설명 프레임워크 - 일반 의미론적 웹 메타데이터용
* xmp - [!DNL Extensible Metadata Platform].
* xmpBJ - 기본 작업 티켓.

### 애플리케이션별 메타데이터 {#application-specific-metadata}

애플리케이션별 메타데이터에는 기술 및 설명 메타데이터가 포함됩니다. 이러한 경우 다른 응용 프로그램에서 메타데이터를 사용할 수 없을 수 있습니다. 예를 들어 [!DNL Adobe Photoshop] 메타데이터가 있는 자산이 있고 다른 이미지 렌더링 응용 프로그램이 메타데이터에 액세스하려고 하면 메타데이터에 액세스할 수 없을 수 있습니다. 자산에 애플리케이션별 메타데이터가 많이 있는 경우 애플리케이션별 속성을 표준 속성으로 변경하는 워크플로우 단계를 만들 수 있습니다.

* ACDSee - [!DNL ACDSee] 프로그램에서 관리하는 메타데이터 www.acdsee.com [를 참조하십시오](https://www.acdsee.com/).
* 앨범 - [!DNL Adobe Photoshop Album]Album.
* cq - 에서 [!DNL Experience Manager Assets]사용됩니다.
* dam - 에 의해 [!DNL Experience Manager Assets]사용됩니다.
* dex - SC 설명 탐색기를 최적화합니다.
* crs - Adobe Photoshop Camera Raw.
* lr - [!DNL Adobe Lightroom]a.
* mediapro - IView MediaPro
* Microsoft Photo &amp; MP - Microsoft Photo.
* pdf 및 pdfx
* photoshop &amp; psAux - [!DNL Adobe Photoshop]를 참조하십시오.

### 디지털 권한 관리 메타데이터 {#digital-rights-management-metadata}

* 참조 - [!DNL Creative Commons].
* [!DNL XMPRights].
* plus - [Picture Licensing Universal System](https://www.useplus.com).
* 프리즘 - https://www.idealliance.org/prism-metadata Publishing Requirements for Industry Standard Metadata.
* PRL - 프리즘 권한 언어.
* PUR - 프리즘 사용 권한.
* xmpPlus - PLUS와 XMP의 통합

### 사진별 메타데이터 {#photography-specific-metadata}

* Exif - GPS 위치를 비롯한 카메라의 기술 정보입니다.
* CRS - [!DNL Camera Raw] 스키마.
* Iptc4xmpCore 및 iptc4xmpExt.
* TIFF - 이미지 메타데이터(TIFF 이미지에만 국한되지 않음)

### 인쇄별 메타데이터 {#print-specific-metadata}

* pdf 및 pdfx - Adobe PDF 및 타사 애플리케이션
* 프리즘 - [www.prismstandard.org](https://www.prismstandard.org) 업계 표준 메타데이터에 대한 게시 요구 사항
* xmp.
* xmpPG - 페이지 지정된 텍스트에 대한 XMP 메타데이터

### 멀티미디어별 메타데이터 {#multimedia-specific-metadata}

* xmpDM - [!DNL Dynamic Media]XMP
* xmpMM - 미디어 관리.

## 메타데이터 기반의 워크플로우 {#metadata-driven-workflows}

메타데이터 중심의 워크플로우를 만들면 일부 프로세스를 자동화하여 효율성을 높일 수 있습니다. 메타데이터 중심의 워크플로우에서 워크플로우 관리 시스템은 워크플로우를 읽고 그 결과 미리 정의된 일부 작업을 수행합니다. 예를 들어, 메타데이터 중심의 워크플로우를 사용할 수 있는 방법 중 몇 가지를 제공합니다.

* 워크플로우는 이미지에 제목이 있는지 여부를 확인할 수 있습니다. 그렇지 않으면 제목 추가에 대한 알림이 표시됩니다.
* 워크플로우는 자산에 대한 저작권 공지가 배포를 허용하는지 여부를 확인할 수 있습니다. 따라서 시스템은 자산을 한 서버 또는 다른 서버로 보냅니다.
* 워크플로우는 사전 정의된 필수 메타데이터 또는 *잘못된* 메타데이터가 있는 자산을 확인하지 않고 자산을 확인할 수 있습니다.
