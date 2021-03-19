---
title: 메타데이터 개념 이해
description: 자산을 쉽게 분류하고 구성할 수 있는 메타데이터의 필요성과 유형에 대해 알아봅니다.
contentOwner: AG
role: 비즈니스 전문가, 관리자
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '2734'
ht-degree: 0%

---


# 메타데이터 개념 이해 {#why-we-need-metadata}

메타데이터는 데이터에 대한 데이터를 의미합니다. 이러한 점에서 데이터는 디지털 자산, 즉 이미지를 나타냅니다. 메타데이터는 효율적인 에셋 관리를 위해 매우 중요합니다.

메타데이터는 자산에 사용할 수 있는 모든 데이터의 수집이지만 해당 이미지에 반드시 포함되지는 않습니다. 메타데이터의 몇 가지 예는 다음과 같습니다.

* 자산의 이름입니다.
* 마지막 수정 시간 및 날짜
* 저장소에 저장된 자산의 크기입니다.
* 포함된 폴더의 이름입니다.
* 관련 자산 또는 적용된 태그.

위의 메타데이터 속성은 사용자가 모든 자산을 볼 수 있도록 [!DNL Experience Manager]이(가) 자산에 대해 관리할 수 있는 기본 메타데이터 속성입니다. 예를 들어 마지막으로 수정한 날짜별로 자산을 정렬하는 것은 최근에 추가한 자산을 검색하려고 할 때 유용합니다.

다음과 같이 높은 수준의 데이터를 디지털 자산에 추가할 수 있습니다.

* 에셋 유형(이미지, 비디오, 오디오 클립 또는 문서입니까?).
* 자산의 소유자입니다.
* 자산의 제목입니다.
* 자산에 대한 설명입니다.
* 자산에 지정된 태그.

추가 메타데이터는 자산을 더 분류하는 데 도움이 되며, 디지털 정보의 양이 증가함에 따라 유용합니다. 파일 이름만 기준으로 수백 개의 파일을 관리할 수 있습니다. 그러나 이 방법은 확장 가능하지 않습니다. 관련된 사람의 수와 관리되는 자산의 수가 증가하는 것은 짧습니다.

메타데이터가 추가되면, 에셋은

* 접근성 향상 - 시스템과 사용자는 손쉽게 찾을 수 있습니다.
* 관리가 더 쉬워짐 - 동일한 속성 세트를 사용하여 자산을 쉽게 찾을 수 있고 변경 사항을 적용할 수 있습니다.
* 완료 - 더 많은 메타데이터가 포함된 추가 정보 및 컨텍스트를 자산에 전달합니다.

이러한 이유로 [!DNL Assets]은 디지털 에셋에 대한 메타데이터를 만들고, 관리하고 교환하는 적절한 방법을 제공합니다.

## 메타데이터 유형 {#types-of-metadata}

메타데이터의 두 가지 기본 유형은 기술 메타데이터와 설명 메타데이터입니다.

기술 메타데이터는 디지털 에셋을 처리하는 소프트웨어 애플리케이션에 유용하며 수동으로 유지 관리해서는 안 됩니다. [!DNL Experience Manager Assets] 그리고 기타 소프트웨어는 기술 메타데이터를 자동으로 결정하며 에셋이 수정되면 메타데이터가 변경될 수 있습니다. 에셋의 사용 가능한 기술 메타데이터는 대개 에셋의 파일 유형에 따라 달라집니다. 기술 메타데이터의 몇 가지 예는 다음과 같습니다.

* 파일의 크기입니다.
* 이미지의 Dimension(높이 및 폭)입니다.
* 오디오 또는 비디오 파일의 비트 전송률입니다.
* 이미지의 해상도(세부 수준).

설명 메타데이터는 애플리케이션 도메인과 관련된 메타데이터입니다. 예를 들어 자산이 만들어지는 비즈니스입니다. 설명 메타데이터를 자동으로 결정할 수 없습니다. 수동 또는 반자동 생성됩니다. 예를 들어 GPS 지원 카메라는 위도와 경도를 자동으로 추적하고 이미지에 지리 태그를 추가할 수 있습니다.

설명 메타데이터 정보를 수동으로 만드는 데 소요되는 비용이 높습니다. 따라서 소프트웨어 시스템과 조직 간의 메타데이터 교환을 용이하게 하기 위해 표준이 마련되었습니다. [!DNL Experience Manager Assets] 메타데이터 관리에 대한 모든 관련 표준을 지원합니다.

## 인코딩 표준 {#encoding-standards}

파일에 메타데이터를 포함하는 다양한 방법이 있습니다. 다양한 인코딩 표준이 지원됩니다.

* XMP:[!DNL Assets]에서 추출된 메타데이터를 저장소 내에 저장하는 데 사용됩니다.
* ID3:오디오 및 비디오 파일의 경우
* Exif:이미지 파일에 사용할 수 있습니다.
* 기타/레거시:[!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel] 등에서.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP)은 모든 메타데이터 관리에 사용되는 개방형  [!DNL Experience Manager Assets] 표준입니다. 표준은 모든 파일 형식에 포함할 수 있는 범용 메타데이터 인코딩을 제공합니다. Adobe과 다른 회사는 XMP 표준을 지원하므로 리치 컨텐츠 모델을 제공합니다. XMP 표준 및 [!DNL Experience Manager Assets] 사용자는 강력한 플랫폼을 사용하여 구축할 수 있습니다. 자세한 내용은 [XMP](https://www.adobe.com/products/xmp.html)을 참조하십시오.

### ID3 {#id}

이러한 ID3 태그에 저장된 데이터는 컴퓨터 또는 휴대용 MP3 플레이어에서 디지털 오디오 파일을 재생할 때 표시됩니다.

ID3 태그는 MP3 파일 형식용으로 디자인되었습니다. 형식에 대한 추가 정보:

* ID3 태그는 MP3 및 mp3PRO 파일에서 작동합니다.
* WAV에는 태그가 없습니다.
* WMA에는 오픈 소스 구현을 허용하지 않는 전용 태그가 있습니다.
* Ogg Vorbis는 Ogg 컨테이너에 포함된 Xiph 주석을 사용합니다.
* AAC는 독점 태그 지정 형식을 사용합니다.

### Exif {#exif}

Exif(Ex교환할 수 있는 이미지 파일 형식)는 디지털 사진 분야에서 가장 널리 사용되는 메타데이터 형식입니다. JPEG, TIFF, RIFF 및 WAV와 같은 다양한 파일 포맷으로 메타데이터 속성의 고정된 용어를 임베드할 수 있는 방법을 제공합니다. Exif는 메타데이터를 메타데이터 이름 및 메타데이터 값의 쌍으로 저장합니다. 이러한 메타데이터 이름-값-쌍은 태그라고도 하며, [!DNL Experience Manager]의 태깅과 혼동하지 않도록 합니다. 최신 디지털 카메라는 Exif 메타데이터를 생성하고 이를 지원하는 최신 그래픽 소프트웨어를 제공합니다. Exif 형식은 특히 이미지에 대한 메타데이터 관리를 위한 가장 일반적인 분모입니다.

Exif의 주요 제한 사항은 BMP, GIF 또는 PNG와 같이 널리 사용되는 몇 가지 이미지 파일 형식이 지원되지 않는다는 것입니다.

Exif에서 정의한 메타데이터 필드는 일반적으로 기술적 사항이며 설명 메타데이터 관리에 제한된 사용 방식입니다. 이러한 이유로 [!DNL Experience Manager Assets]은 Exif 속성의 매핑을 [공통 메타데이터 스키마](metadata-schemas.md)에 제공하고 [XMP](xmp-writeback.md)에 제공합니다.

### 기타 메타데이터 {#other-metadata}

파일에서 포함할 수 있는 기타 메타데이터에는 [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel] 등이 포함됩니다.

## 메타데이터 스키마 이해 {#metadata-schemata}

메타데이터 스키마는 다양한 응용 프로그램에서 사용할 수 있는 메타데이터 속성 정의의 사전 정의된 세트입니다. 속성은 항상 자산과 연결되어 있습니다. 즉, 속성이 &#39;정보&#39;임을 의미합니다.

또한 필요에 맞는 메타데이터가 없는 경우 자체 메타데이터 스키마를 디자인할 수도 있습니다. 기존 정보를 복제하지 마십시오. 조직 내에서 구성 요소를 구분하면 메타데이터를 쉽게 공유할 수 있습니다. [!DNL Experience Manager] 에서는 가장 인기 있는 메타데이터 스키마 기본 목록을 제공합니다. 이 목록을 사용하면 메타데이터 전략을 바로 시작하고 필요한 메타데이터 속성을 신속하게 선택할 수 있습니다.

지원되는 메타데이터 구성표는 아래에 나열되어 있습니다.

### 표준 메타데이터 {#standard-metadata}

* DC - [!DNL Dublin Core]은 중요하고 널리 사용되는 메타데이터 세트입니다.
* DICOM - 의료 분야의 디지털 이미징 및 커뮤니케이션
* `Iptc4xmpCore` 및  `iptc4xmpExt` - International Press Communications Standard에는 많은 주제 관련 메타데이터가 포함되어 있습니다.
* RDF - 리소스 설명 프레임워크 - 일반 의미 웹 메타데이터용.
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ` - 기본 작업 티켓을 참조하십시오.

### 응용 프로그램별 메타데이터 {#application-specific-metadata}

애플리케이션별 메타데이터에는 기술 및 설명 메타데이터가 포함됩니다. 이러한 메타데이터를 사용하는 경우 다른 응용 프로그램에서 메타데이터를 사용할 수 없을 수 있습니다. 예를 들어 다른 이미지 렌더링 응용 프로그램이 [!DNL Adobe Photoshop] 메타데이터에 액세스할 수 없을 수 있습니다. 응용 프로그램별 속성을 표준 속성으로 변경하는 워크플로우 단계를 만들 수 있습니다.

* ACDSee - [!DNL ACDSee] 프로그램에서 관리하는 메타데이터. [www.acdsee.com/](https://www.acdsee.com/)을(를) 참조하십시오.
* 앨범 - [!DNL Adobe Photoshop Album].
* CQ - [!DNL Experience Manager Assets]에서 사용됩니다.
* DAM - [!DNL Experience Manager Assets]에서 사용됩니다.
* DEX - [Optima SC Description explorer](http://www.optimasc.com/products/dex/index.html)는 Windows 운영 체제에 대한 메타데이터 및 파일 관리를 위한 도구 모음입니다.
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* Microsoft Photo 및 MP - Microsoft Photo.
* PDF 및 PDF/X.
* Photoshop 및 psAux - [!DNL Adobe Photoshop].

### Digital Rights Management(DRM) 메타데이터 {#digital-rights-management-metadata}

* 참조 - [!DNL Creative Commons].
* [!DNL XMPRights].
* PLUS - [사진 라이센스 범용 시스템](https://www.useplus.com).
* 프리즘 - [업계 표준 메타데이터에 대한 게시 요구 사항](https://www.idealliance.org/prism-metadata).
* PRL - 프리즘 권리 언어.
* PUR - 프리즘 사용 권리.
* `xmpPlus` - XMP과 PLUS 통합

### 포토그래피 특정 메타데이터 {#photography-specific-metadata}

* Exif - GPS 위치를 비롯한 카메라의 기술 정보.
* CRS - [!DNL Camera Raw] 스키마.
* `iptc4xmpCore` 및 `iptc4xmpExt`.
* TIFF - 이미지 메타데이터(TIFF 이미지뿐만 아니라).

### 인쇄 관련 메타데이터 {#print-specific-metadata}

* PDF 및 PDF/X - Adobe PDF 및 타사 애플리케이션
* 프리즘 - [업계 표준 메타데이터에 대한 게시 요구 사항](https://www.idealliance.org/prism-metadata).
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG` - 페이지 텍스트를 위한 XMP 메타데이터

### 멀티미디어 관련 메타데이터 {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` - 미디어 관리.

## 메타데이터 스키마 참조 {#metadata-schemata-reference}

다음 참조에는 속성 및 해당 정의 목록뿐만 아니라 특정 메타데이터 스키마에 대한 정보(알파벳순)도 포함됩니다.

### 더블린 코어 {#dublin-core}

더블린 코어 메타데이터는 자산을 쉽게 찾을 수 있도록 자산을 설명하는 표준 규칙 세트를 제공합니다. [!DNL Assets]에서 더블린 코어는 비디오, 사운드, 이미지 및 문서를 비롯한 디지털 에셋을 설명합니다.

단순 더블린 코어 메타데이터 요소 세트(DCMES)에는 다음 표에 나열된 15개의 메타데이터 요소가 포함되어 있습니다. 각 더블린 코어 요소는 선택 사항이며 반복될 수 있습니다. 미디어 유형별 메타데이터와 마찬가지로 더블린 코어 메타데이터 정보를 추가하거나 삭제할 수 있습니다.

DCMES 외에도 Dublin Core Initiative에서 만든 기타 메타데이터 요소가 있습니다. 자세한 내용은 [Dublin Core initiative](https://dublincore.org/)을 참조하십시오.

| 속성 | 설명 |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| contributor | 컨텐트에 대한 증여를 담당하는 개인 또는 회사. |
| 적용 | 자산이 적용되는 지리적 위치 또는 기간. |
| creator | 컨텐츠 작성을 담당하는 사람 또는 회사. |
| 날짜 | 자산과 관련된 날짜 또는 기간. |
| 설명 | 자산에 대한 자세한 정보입니다. |
| format | 자산의 파일 형식, 실제 미디어 또는 크기입니다. [!DNL Experience Manager] 자산 `dc:format` 의 MIME 유형을 나타내는 데 사용됩니다. |
| 식별자 | 자산에 대한 고유한 참조입니다. |
| 언어 | 자산의 언어(예: 영어의 경우 `en`). |
| publisher | 자산을 사용할 수 있게 만드는 담당자 또는 회사. |
| 관계 | 관련 자산. |
| 권리 | 이 자산에 대한 권한이 있는 사람에 대한 정보입니다. |
| source | 자산이 파생되는 관련 자산. |
| subject | 자산의 주제. |
| 제목 | 자산의 이름입니다. |
| 유형 | 자산의 특성 또는 장르입니다. |

### IPTC {#iptc}

국제 언론 통신 통신 위원회(IPTC)는 전 세계의 뉴스 기관들의 컨소시엄이다 - 그것의 목표 중 하나는 기술 기준을 개발하고 유지하는 것이다. IPTC는 사진 작가가 거의 보편적으로 인정하는 이미지에 대한 일련의 사진 메타데이터 표준을 정의했습니다. 이러한 메타데이터 표준은 1990년대에 만들어진 IIM(IPTC Information Interchange Model)으로 알려진 광범위한 표준의 일부였습니다.

IPTC 헤더 정보가 대부분 XMP으로 대체되었지만, XMP에 대해 IPTC 핵심 스키마 및 확장 스키마를 사용할 수 있습니다. 이미지 프로그램에서 XMP 및 IPTC 속성이 모두 동기화됩니다.

## 메타데이터 기반의 워크플로우 {#metadata-driven-workflows}

메타데이터 기반의 워크플로우를 사용하면 일부 프로세스를 자동화할 수 있으므로 효율성을 향상시킬 수 있습니다. 메타데이터 중심의 워크플로우에서 워크플로우 관리 시스템은 워크플로우를 읽고 그 결과 사전 정의된 작업을 수행합니다. 예를 들어 메타데이터 기반의 워크플로우를 사용할 수 있는 방법 중 일부를 다음과 같이 제공합니다.

* 워크플로우는 이미지에 제목이 있는지 여부를 확인할 수 있습니다. 그렇지 않으면 제목 추가에 알립니다.
* 워크플로우는 자산에 대한 저작권 공지가 배포를 허용하는지 여부를 확인할 수 있습니다. 따라서, 시스템은 자산을 한 서버나 다른 서버로 보냅니다.
* 워크플로우는 사전 정의된 필수 메타데이터 또는 *잘못된* 메타데이터가 있는 자산이 없는 자산을 확인할 수 있습니다.

## XMP 메타데이터 {#xmp-metadata}

XMP(Extensible Metadata Platform)은 모든 메타데이터 관리에 대해 [!DNL Adobe Experience Manager Assets]이 사용하는 메타데이터 표준입니다. XMP은 다양한 응용 프로그램에 대한 메타데이터를 생성, 처리 및 교환하기 위한 표준 형식을 제공합니다.

모든 파일 포맷에 임베드할 수 있는 범용 메타데이터 인코딩 외에도 XMP은 풍부한 [컨텐츠 모델](#xmp-core-concepts)을 제공하며 Adobe](#advantages-of-xmp) 및 다른 회사에서 지원하는 [이므로 XMP 사용자가 [!DNL Assets]과(와) 함께 사용하는 사용자는 강력한 플랫폼을 사용하여 구축할 수 있습니다.

[XMP 사양](https://www.adobe.com/devnet/xmp.html)은 Adobe에서 사용할 수 있습니다.

### XMP 소개{#what-is-xmp}

Adobe은 XMP 표준을 Adobe Acrobat 소프트웨어 제품의 일부로 처음 도입했습니다. 그 이후 XMP은 널리 채택되었다. [!DNL Assets] 기본적으로 XMP은 Adobe을 기반으로 하는 확장 가능한 메타데이터 플랫폼을 지원합니다. XMP은 표준화된 및 독점 메타데이터를 디지털 자산에 처리 및 저장하는 표준입니다. XMP은 여러 애플리케이션이 메타데이터와 효과적으로 작업할 수 있는 일반적인 표준으로 설계되었습니다.

예를 들어 프로덕션 전문가는 Adobe 애플리케이션의 내장된 XMP 지원을 사용하여 다양한 파일 포맷에 정보를 전달할 수 있습니다. [!DNL Assets] 리포지토리는 XMP 메타데이터를 추출하여 컨텐츠 라이프사이클을 관리하는 데 사용하고 자동화 워크플로우를 만드는 기능을 제공합니다.

XMP은 데이터 모델, 스토리지 모델 및 스키마를 제공하여 메타데이터가 정의, 생성 및 처리되는 방식을 표준화합니다. 이러한 모든 개념이 이 섹션에 설명되어 있습니다.

EXIF, ID3 또는 Microsoft Office의 모든 기존 메타데이터는 자동으로 XMP으로 변환되므로 제품 카탈로그 등 고객별 메타데이터 스키마를 지원하도록 확장할 수 있습니다.

XMP의 메타데이터는 일련의 속성으로 구성됩니다. 이러한 속성은 항상
리소스라고 하는 특정 엔티티즉, 속성은 리소스에 대해 &quot;정보&quot;입니다. XMP의 경우 리소스는 항상 자산입니다.

### XMP 에코시스템 {#xmp-ecosystem}

XMP은 정의된 메타데이터 항목 집합에 사용할 수 있는 [메타데이터](https://en.wikipedia.org/wiki/Metadata) 모델을 정의합니다. XMP은 또한 사진 촬영, [스캔한](https://en.wikipedia.org/wiki/Image_scanner)에서 사진 편집 단계(예: [자르기](https://en.wikipedia.org/wiki/Cropping_%28image%29) 또는 색상 조정)를 통해 최종 이미지로 어셈블하는 등 여러 처리 단계를 거칠 때 리소스의 내역을 기록하는 데 유용한 기본 속성에 대해 특정 [스키마](https://en.wikipedia.org/wiki/XML_schema)를 정의합니다. XMP을 사용하면 각 소프트웨어 프로그램 또는 디바이스에서 자신의 정보를 디지털 리소스에 추가할 수 있으며 이러한 정보는 최종 디지털 파일로 보관할 수 있습니다.

XMP은 대부분 일반적으로 [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework)(RDF)의 하위 집합을 사용하여 시리얼라이즈 및 저장하며, 이 프레임워크는 다시 [XML](https://en.wikipedia.org/wiki/XML)로 표현됩니다.

### XMP {#advantages-of-xmp}의 이점

XMP은 다른 인코딩 표준 및 구성표에 비해 다음과 같은 이점이 있습니다.

* XMP 기반의 메타데이터는 매우 강력하고 세부적으로 정의됩니다.
* XMP에서는 하나의 속성에 여러 값을 사용할 수 있습니다.
* XMP은 표준화된 인코딩을 제공하므로 메타데이터를 손쉽게 교환할 수 있습니다.
* XMP은 확장 가능합니다. 자산에 추가 정보를 추가할 수 있습니다.

XMP 표준은 확장 가능하도록 설계되었으며, XMP 데이터에 사용자 정의 유형의 메타데이터를 추가할 수 있습니다. 반면에 EXIF에는 확장할 수 없는 고정 속성 목록이 있습니다.

>[!NOTE]
>
>XMP에서는 일반적으로 이진 데이터 형식을 포함할 수 없습니다. 이진 데이터를 XMP에 가져오려면 축소판 이미지와 같은 XML 호환 형식으로 인코딩해야 합니다(예: `Base64`).

### XMP 개념 {#xmp-core-concepts}

다음 섹션에서는 네임스페이스, 스키마, 속성 및 값, 언어 대체 요소 등 XMP의 핵심 개념에 대해 설명합니다.

#### 네임스페이스 및 스키마 {#namespaces-and-schemata}

XMP 스키마는 공통 XML 네임스페이스에 포함된 속성 이름 세트입니다.
데이터 유형 및 설명 정보. XMP 스키마는 XML 네임스페이스 URI로 식별됩니다. 네임스페이스를 사용하면 이름이 같지만 의미가 다른 여러 스키마에 있는 속성 간 충돌이 방지됩니다.

예를 들어, 독립적으로 디자인된 2개의 스키마에 있는 `Creator` 속성은 자산을 만든 사람을 의미하거나 자산을 만든 응용 프로그램(예: Adobe Photoshop)을 의미할 수 있습니다.

#### 속성 및 값 {#properties-and-values}

XMP에는 하나 이상의 스키마에 있는 속성이 포함될 수 있습니다. 예를 들어 많은 Adobe 응용 프로그램에서 사용하는 일반적인 하위 집합은 다음을 포함할 수 있습니다.

* 더블린 코어 스키마:`dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`.
* XMP 기본 스키마:`xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`.
* XMP 권한 관리 스키마:`xmpRights:WebStatement`, `xmpRights:Marked`.
* XMP 미디어 관리 스키마:`xmpMM:DocumentID`.

#### 언어 대체 요소 {#language-alternatives}

XMP에서는 텍스트 속성에 `xml:lang` 속성을 추가하여 텍스트 언어를 지정할 수 있습니다.

## IPTC 메타데이터 {#support-for-iptc-metadata} 사용

[!DNL Adobe Experience Manager Assets]이(가) [!DNL Adobe Bridge] 및 다른 [!DNL Adobe Creative Cloud] 앱을 통해 자산에 추가된 IPTC 메타데이터, 크리에이티브 등급 및 키워드를 지원하는 방법을 알아봅니다.

[!DNL Adobe Experience Manager Assets] 에서는 자산을 설명하는 데 널리 사용되는 IPTC 메타데이터 표준을 지원합니다. 이러한 방식으로 [!DNL Assets]은 사진 작가, 크리에이티브 에이전시, 도서관, 박물관 등을 비롯한 다양한 파티 간에 이미지를 보다 효과적으로 활용할 수 있습니다.

에셋의 기본 메타데이터 스키마는 이제 IPTC 코어 및 IPTC 확장 메타데이터 스키마를 통합하여 포괄적인 메타데이터 속성을 정의하여 사용자가 이미지에 표시된 사람, 위치 및 제품에 대한 정확하고 안정적인 데이터를 추가할 수 있습니다. 또한 이미지 만들기와 관련된 날짜, 이름 및 식별자, 권한 정보를 표현하는 유연한 방법을 지원합니다.

이제 자산에 대한 속성 페이지에는 편집 가능한 필드에 IPTC 코어 및 IPTC 확장 메타데이터를 표시하는 별도의 탭이 포함되어 있습니다.

1. [!DNL Assets] 사용자 인터페이스에서 이미지를 선택합니다.
1. 도구 모음에서 **[!UICONTROL 속성]**&#x200B;을 클릭합니다.
1. 자산에 대한 IPTC 메타데이터를 보려면 **[!UICONTROL IPTC]** 탭을 클릭합니다.
1. 필요에 따라 IPTC 메타데이터 속성을 편집합니다.

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. 자산에 대한 IPTC 확장 메타데이터를 보려면 **[!UICONTROL IPTC 확장]** 탭을 클릭합니다.
1. 필요에 따라 IPTC 확장 메타데이터 속성을 편집합니다.
1. **[!UICONTROL 저장 및 닫기]**&#x200B;를 클릭하여 변경 내용을 저장합니다.

### 크리에이티브 등급 지원 {#creative-rating-support}

속성 페이지에는 개별 사용자 등급 및 집계 등급을 표시하는 것 외에도 Adobe Bridge 및 기타 Creative Apps를 통해 자산에 할당된 등급이 표시됩니다

이러한 등급은 **[!UICONTROL 고급]** 탭 내의 **[!UICONTROL 크리에이티브 등급]** 섹션 아래에 있습니다.

이 등급은 읽기 전용 속성이며 1-5 범위의 범위입니다. 검색 패널에서 크리에이티브 등급을 기준으로 자산을 검색할 수 있습니다.

하지만 이 속성은 현재 사용자가 수행한 사용자 지정 변경 사항과 충돌하지 않도록 색인화되지 않았습니다.

### 키워드 지원 {#keyword-support}

[!UICONTROL 속성] 페이지의 **[!UICONTROL IPTC]** 탭에는 Adobe Bridge 및 다른 Adobe Creative Cloud 앱을 통해 자산에 추가된 키워드도 표시됩니다. 이러한 키워드를 편집하고 **[!UICONTROL IPTC]** 탭에서 키워드를 더 추가할 수도 있습니다.

![키워드](assets/keywords-in-iptc-tab.png)
