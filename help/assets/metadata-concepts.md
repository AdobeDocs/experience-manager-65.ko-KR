---
title: 메타데이터 개념 이해
description: 에셋을 보다 쉽게 분류하고 구성할 수 있는 메타데이터의 요구 사항과 유형에 대해 알아봅니다.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 312fff5f-39c1-48c1-aa99-40feb72c2f59
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '2717'
ht-degree: 9%

---

# 메타데이터 개념 이해 {#why-we-need-metadata}

메타데이터는 데이터에 대한 데이터를 의미합니다. 이와 관련하여 데이터는 디지털 자산, 즉 이미지를 나타냅니다. 메타데이터는 효율적인 자산 관리에 있어 매우 중요합니다.

메타데이터는 에셋에 사용할 수 있는 모든 데이터의 집합이지만 해당 이미지에 반드시 포함되지는 않습니다. 메타데이터의 일부 예는 다음과 같습니다.

* 에셋 이름.
* 마지막으로 수정한 시간 및 날짜입니다.
* 저장소에 저장된 에셋의 크기입니다.
* 포함된 폴더의 이름입니다.
* 관련 에셋 또는 적용된 태그.

위의 항목은 [!DNL Experience Manager] 는 사용자가 모든 에셋을 볼 수 있도록 에셋을 관리할 수 있습니다. 예를 들어 최근에 추가된 에셋을 검색하려고 할 때 마지막 수정 날짜별로 에셋을 정렬하는 것이 유용합니다.

디지털 에셋에 높은 수준의 데이터를 추가할 수 있습니다. 예를 들면 다음과 같습니다.

* 에셋 유형(이미지, 비디오, 오디오 클립 또는 문서)입니다.
* 에셋 소유자.
* 에셋 제목
* 에셋에 대한 설명.
* 자산에 할당된 태그.

더 많은 메타데이터는 에셋을 더 세부적으로 분류하는 데 도움이 되며 디지털 정보의 양이 증가할 때 유용합니다. 파일 이름만 기준으로 수백 개의 파일을 관리할 수 있습니다. 그러나 이 접근 방식은 확장할 수 없습니다. 관련된 사람의 수와 관리하는 자산의 수가 증가하면 부족하다.

메타데이터를 추가하면 자산이 다음과 같이 되기 때문에 디지털 자산의 가치가 증가합니다.

* 접근성 향상 - 시스템과 사용자가 쉽게 찾을 수 있습니다.
* 관리 용이성 - 동일한 속성 세트를 가진 자산을 더 쉽게 찾고 변경 사항을 적용할 수 있습니다.
* 최대 효율 - 자산은 더 많은 메타데이터로 더 많은 정보와 컨텍스트를 전달합니다.

이러한 이유로, [!DNL Assets] 은 디지털 에셋에 대한 메타데이터를 생성하고, 관리하고, 교환할 수 있는 적절한 수단을 제공합니다.

## 메타데이터 유형 {#types-of-metadata}

두 가지 기본 메타데이터 유형은 기술 메타데이터와 설명 메타데이터입니다.

기술 메타데이터는 디지털 에셋을 처리하는 소프트웨어 애플리케이션에 유용하며 수동으로 유지해서는 안 됩니다. [!DNL Experience Manager Assets] 및 기타 소프트웨어는 자동으로 기술 메타데이터를 결정하고 에셋이 수정되면 메타데이터가 변경될 수 있습니다. 에셋의 사용 가능한 기술 메타데이터는 에셋의 파일 유형에 따라 크게 달라집니다. 기술 메타데이터의 몇 가지 예는 다음과 같습니다.

* 파일 크기입니다.
* 이미지의 Dimension(높이 및 너비).
* 오디오 또는 비디오 파일의 비트 전송률입니다.
* 이미지의 해상도(세부 정보 수준)입니다.

설명 메타데이터는 에셋이 속한 비즈니스 등 애플리케이션 도메인과 관련된 메타데이터입니다. 설명 메타데이터는 자동으로 확인할 수 없습니다. 수동 또는 반자동으로 생성됩니다. 예를 들어 GPS 지원 카메라는 위도와 경도를 자동으로 추적하고 이미지에 지오태그를 추가할 수 있습니다.

수사적 메타데이터 정보를 수동으로 생성하는 비용이 많이 듭니다. 따라서 소프트웨어 시스템 및 조직 간의 메타데이터 교환을 쉽게 하기 위해 표준이 수립됩니다. [!DNL Experience Manager Assets] 는 메타데이터 관리를 위한 모든 관련 표준을 지원합니다.

## 인코딩 표준 {#encoding-standards}

파일에 메타데이터를 임베드하는 방법은 다양합니다. 다양한 인코딩 표준이 지원됩니다.

* XMP: 사용한 사람 [!DNL Assets] 저장소에서 추출된 메타데이터를 저장합니다.
* ID3: 오디오 및 비디오 파일용.
* Exif: 이미지 파일용.
* 기타/기존: 부터 [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel]등.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP)은에서 사용하는 개방형 표준입니다. [!DNL Experience Manager Assets] 모든 메타데이터 관리. 이 표준은 모든 파일 형식에 임베드할 수 있는 범용 메타데이터 인코딩을 제공합니다. Adobe 및 기타 기업은 XMP standard가 풍부한 콘텐츠 모델을 제공하므로 이를 지원합니다. XMP standard 및 의 사용자 [!DNL Experience Manager Assets] 구축할 강력한 플랫폼이 있습니다. 자세한 내용은 [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

이러한 ID3 태그에 저장된 데이터는 컴퓨터 또는 휴대용 MP3 플레이어에서 디지털 오디오 파일을 재생할 때 표시됩니다.

ID3 태그는 MP3 파일 형식을 위해 설계되었습니다. 형식에 대한 추가 정보:

* ID3 태그는 MP3 및 mp3PRO 파일에서 작동합니다.
* WAV에 태그가 없습니다.
* WMA에는 오픈 소스 구현을 허용하지 않는 독점 태그가 있습니다.
* Ogg Vorbis는 Ogg 컨테이너에 포함된 Xiph 주석을 사용합니다.
* AAC는 고유한 태그 지정 형식을 사용합니다.

### Exif {#exif}

Exif(교환 이미지 파일 형식)는 디지털 사진에서 사용되는 가장 인기 있는 메타데이터 형식입니다. JPEG, TIFF, RIFF 및 WAV와 같은 다양한 파일 형식으로 메타데이터 속성에 대한 고정 어휘를 임베드하는 방법을 제공합니다. Exif는 메타데이터를 메타데이터 이름과 메타데이터 값의 쌍으로 저장합니다. 이러한 메타데이터 이름-값-쌍을 의 태그와 혼동하지 않도록 태그라고도 합니다 [!DNL Experience Manager]. 최신 디지털 카메라는 Exif 메타데이터를 만들고 최신 그래픽 소프트웨어가 이를 지원합니다. Exif 형식은 특히 이미지에 대한 메타데이터 관리에 사용되는 가장 낮은 공통 분모입니다.

Exif의 주요 제한 사항은 BMP, GIF 또는 PNG와 같은 일부 인기 있는 이미지 파일 형식이 지원되지 않는다는 것입니다.

Exif에서 정의한 메타데이터 필드는 일반적으로 기술적 성격으로 설명 메타데이터 관리에 제한적으로 사용됩니다. 이러한 이유로, [!DNL Experience Manager Assets] exif 속성 매핑을 제공합니다. [일반 메타데이터 스키마](metadata-schemas.md) 및 대상 [XMP](xmp-writeback.md).

### 기타 메타데이터 {#other-metadata}

파일에서 임베드할 수 있는 기타 메타데이터는 다음과 같습니다. [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel]등.

## 메타데이터 스키마 이해 {#metadata-schemata}

메타데이터 스키마는 다양한 애플리케이션에서 사용할 수 있는 사전 정의된 메타데이터 속성 정의 세트입니다. 속성은 항상 자산과 연결되어 있습니다. 즉, 속성은 리소스에 대한 &#39;정보&#39;입니다.

필요에 맞는 메타데이터 스키마가 없는 경우 고유한 메타데이터 스키마를 디자인할 수도 있습니다. 기존 정보를 복제하지 마십시오. 조직 내에서 스키마를 분리하면 메타데이터를 더 쉽게 공유할 수 있습니다. [!DNL Experience Manager] 는 가장 인기 있는 메타데이터 스키마의 기본 목록을 제공합니다. 이 목록을 사용하면 메타데이터 전략을 빠르게 시작하고 필요한 메타데이터 속성을 빠르게 선택할 수 있습니다.

지원되는 메타데이터 스키마 목록은 다음과 같습니다.

### 표준 메타데이터 {#standard-metadata}

* DC - [!DNL Dublin Core] 는 중요하고 널리 사용되는 메타데이터 세트입니다.
* DICOM - 디지털 이미징 및 의학 커뮤니케이션.
* `Iptc4xmpCore` 및 `iptc4xmpExt` - 국제 언론 통신 표준에는 많은 주제별 메타데이터가 포함되어 있습니다.
* RDF - 리소스 설명 프레임워크 - 일반 시맨틱 웹 메타데이터용.
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ` - 기본 구인 티켓.

### 애플리케이션별 메타데이터 {#application-specific-metadata}

애플리케이션별 메타데이터에는 기술적 메타데이터와 기술적 메타데이터가 포함됩니다. 이러한 메타데이터를 사용하는 경우 다른 응용 프로그램에서 해당 메타데이터를 사용하지 못할 수 있습니다. 예를 들어, 다른 이미지 렌더링 애플리케이션은 액세스하지 못할 수 있다 [!DNL Adobe Photoshop] 메타데이터. 응용 프로그램별 속성을 표준 속성으로 변경하는 워크플로 단계를 만들 수 있습니다.

* ACDSee - 메타데이터를에서 관리 [!DNL ACDSee] 프로그램. 다음을 참조하십시오 [www.acdsee.com/](https://www.acdsee.com/).
* 앨범 - [!DNL Adobe Photoshop Album].
* CQ - 사용 [!DNL Experience Manager Assets].
* DAM - 사용 [!DNL Experience Manager Assets].
* DEX - [!DNL Optima SC Description explorer] 는 Windows 운영 체제용 메타데이터 및 파일 관리를 위한 도구 모음입니다.
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto 및 MP - Microsoft 사진.
* PDF 및 PDF/X
* Photoshop 및 psAux - [!DNL Adobe Photoshop].

### Digital Rights Management(DRM) 메타데이터 {#digital-rights-management-metadata}

* 참조 - [!DNL Creative Commons].
* [!DNL XMPRights]
* 플러스 - [Picture Licensing Universal System](https://www.useplus.com).
* 프리즘 - [업계 표준 메타데이터에 대한 게시 요구 사항](https://www.idealliance.org/prism-metadata).
* PRL - PRISM Rights 언어.
* PUR - 프리즘 사용 권한.
* `xmpPlus` - PLUS와 XMP 통합.

### 사진별 메타데이터 {#photography-specific-metadata}

* Exif - GPS 위치를 포함한 카메라의 기술 정보.
* CRS - [!DNL Camera Raw] 스키마.
* `iptc4xmpCore` 및 `iptc4xmpExt`.
* TIFF - 이미지 메타데이터(TIFF 이미지에만 해당되지 않음).

### 인쇄별 메타데이터 {#print-specific-metadata}

* PDF 및 PDF/X - Adobe PDF 및 타사 애플리케이션.
* 프리즘 - [업계 표준 메타데이터에 대한 게시 요구 사항](https://www.idealliance.org/prism-metadata).
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG` - 페이징된 텍스트에 대한 XMP 메타데이터

### 멀티미디어별 메타데이터 {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` - 미디어 관리.

## 메타데이터 스키마 참조 {#metadata-schemata-reference}

다음 참조에는 특정 메타데이터 스키마(알파벳순으로)와 속성 목록 및 해당 정의에 대한 정보가 포함됩니다.

### 더블린 코어 {#dublin-core}

더블린 코어 메타데이터는 에셋을 쉽게 찾을 수 있도록 설명하는 표준화된 규칙 세트를 제공합니다. 위치 [!DNL Assets], 더블린 코어는 비디오, 사운드, 이미지 및 문서를 포함한 디지털 에셋에 대해 설명합니다.

단순 더블린 코어 메타데이터 요소 집합(DCMES)은 다음 표에 나열된 15개의 메타데이터 요소를 포함한다. 각 더블린 코어 요소는 선택 사항이며 반복될 수 있습니다. 미디어 유형별 메타데이터와 마찬가지로 더블린 코어 메타데이터 정보를 추가하거나 삭제할 수 있습니다.

DCMES 외에도, 더블린 코어 이니셔티브에 의해 생성된 다른 메타데이터 요소들이 있다. 다음을 참조하십시오. [더블린 코어 이니셔티브](https://dublincore.org/) 추가 정보.

| 속성 | 설명 |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| 참여자 | 콘텐츠에 대한 기여를 담당하는 사람 또는 회사. |
| 범위 | 자산이 포함하는 지리적 위치 또는 기간입니다. |
| 작성자 | 콘텐츠 작성을 담당하는 사람 또는 회사. |
| 날짜 | 자산과 연계된 날짜 또는 기간. |
| 설명 | 에셋에 대한 자세한 정보입니다. |
| 형식 | 에셋의 파일 형식, 물리적 매체 또는 차원입니다. [!DNL Experience Manager] 사용 `dc:format` 에셋의 MIME 유형을 나타냅니다. |
| 식별자 | 에셋에 대한 고유한 참조. |
| 언어 | 자산의 언어(예: `en` 영어). |
| 게시자 | 에셋을 사용할 수 있도록 만드는 담당자 또는 회사입니다. |
| 관계 | 관련 에셋. |
| 권한 | 이 자산에 대한 권한이 있는 사용자에 대한 정보입니다. |
| source | 에셋이 파생된 관련 에셋. |
| 제목 | 에셋의 주제입니다. |
| 제목 | 에셋의 이름입니다. |
| 유형 | 에셋의 특성 또는 장르. |

### IPTC {#iptc}

IPTC(International Press Telecommunications Council)는 전 세계 뉴스 통신사의 컨소시엄으로, 기술 표준을 개발하고 유지하는 것이 그 목표 중 하나입니다. IPTC는 사진 작가들 사이에서 거의 보편적으로 받아들여지는 이미지에 대한 사진 메타데이터 표준의 집합을 정의했다. 이러한 메타데이터 표준은 1990년대에 작성된 IPTC 정보 교환 모델(IIM)로 알려진 광범위한 표준의 일부였습니다.

IPTC 헤더 정보는 대부분 XMP으로 대체되었지만 XMP에 대해 IPTC 코어 스키마와 확장 스키마를 사용할 수 있습니다. 이미지 프로그램에서는 XMP 및 IPTC 속성이 모두 동기화됩니다.

## 메타데이터 기반 워크플로 {#metadata-driven-workflows}

메타데이터 기반 워크플로를 만들면 일부 프로세스를 자동화하여 효율성을 향상시킬 수 있습니다. 메타데이터 기반 워크플로에서 워크플로 관리 시스템은 워크플로를 읽고 그 결과 사전 정의된 몇 가지 작업을 수행합니다. 예를 들어 메타데이터 기반 워크플로를 사용할 수 있는 몇 가지 방법은 다음과 같습니다.

* 워크플로우는 이미지에 제목이 있는지 여부를 확인할 수 있습니다. 그렇지 않으면 시스템에서 제목을 추가하도록 알립니다.
* 워크플로우는 자산에 대한 저작권 고지가 배포를 허용하는지 여부를 확인할 수 있습니다. 따라서 시스템은 자산을 한 서버 또는 다른 서버로 전송합니다.
* 워크플로우는 사전 정의된 필수 메타데이터가 없는 에셋 또는 *잘못됨* 메타데이터.

## XMP 메타데이터 {#xmp-metadata}

XMP(Extensible Metadata Platform)은 다음에 의해 사용되는 메타데이터 표준입니다. [!DNL Adobe Experience Manager Assets] 모든 메타데이터 관리. XMP은 다양한 애플리케이션에 대한 메타데이터를 생성하고, 처리하고, 교환할 수 있는 표준 포맷을 제공합니다.

모든 파일 형식에 임베드할 수 있는 범용 메타데이터 인코딩을 제공하는 것 외에도 XMP에서는 다양한 기능을 제공합니다 [콘텐츠 모델](#xmp-core-concepts) 및 [Adobe에서 지원](#advantages-of-xmp) 및 기타 회사가 XMP의 사용자를 [!DNL Assets] 구축할 강력한 플랫폼이 있습니다.

다음 [XMP 사양](https://www.adobe.com/devnet/xmp.html) Adobe에서 사용할 수 있습니다.

### XMP란? {#what-is-xmp}

Adobe은 Adobe Acrobat 소프트웨어 제품의 일부로 XMP 표준을 처음 도입했습니다. 이후 XMP 표준이 널리 채택되고 있다. [!DNL Assets] 는 기본적으로 XMP - Adobe을 선두로 하는 확장 가능한 메타데이터 플랫폼을 지원합니다. XMP은 디지털 자산에서 표준화되고 독점 메타데이터를 처리하고 저장하는 표준입니다. XMP은 여러 애플리케이션이 메타데이터를 사용하여 효과적으로 작업할 수 있도록 하는 공통 표준으로 설계되었습니다.

예를 들어 프로덕션 전문가는 Adobe 애플리케이션 내의 기본 제공 XMP 지원을 사용하여 여러 파일 형식에 걸쳐 정보를 전달합니다. [!DNL Assets] 저장소는 XMP 메타데이터를 추출하고 이를 사용하여 콘텐츠 라이프사이클을 관리하고 자동화 워크플로를 만들 수 있는 기능을 제공합니다.

XMP은 데이터 모델, 스토리지 모델 및 스키마를 제공하여 메타데이터의 정의, 생성 및 처리 방법을 표준화합니다. 이 개념들은 모두 이 섹션에서 다룹니다.

EXIF, ID3 또는 Microsoft Office의 모든 기존 메타데이터는 자동으로 XMP으로 변환되며, 이를 제품 카탈로그와 같은 고객별 메타데이터 스키마를 지원하도록 확장할 수 있습니다.

XMP의 메타데이터는 속성 세트로 구성됩니다. 이러한 속성은 항상 리소스라고 하는 특정 엔티티와 연결됩니다. 즉, 속성은 리소스 &quot;정보&quot;입니다. XMP이 있는 경우 리소스는 항상 자산입니다.

### XMP 에코시스템 {#xmp-ecosystem}

XMP defines a [metadata](https://en.wikipedia.org/wiki/Metadata) model that can be used with any defined set of metadata items. XMP also defines particular [schemas](https://en.wikipedia.org/wiki/XML_schema) for basic properties useful for recording the history of a resource as it passes through multiple processing steps, from being photographed, [scanned](https://en.wikipedia.org/wiki/Image_scanner), or authored as text, through photo editing steps (such as [cropping](https://en.wikipedia.org/wiki/Cropping_%28image%29) or color adjustment), to assembly into a final image. XMP allows each software program or device along the way to add its own information to a digital resource, which can then be retained in the final digital file.

XMP is most commonly serialized and stored using a subset of the [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF), which is in turn expressed in [XML](https://en.wikipedia.org/wiki/XML).

### XMP의 장점 {#advantages-of-xmp}

XMP은 다른 인코딩 표준 및 스키마타에 비해 다음과 같은 이점이 있습니다.

* XMP 기반 메타데이터는 매우 강력하고 세분화되었습니다.
* XMP을 사용하면 하나의 속성에 대해 여러 값을 가질 수 있습니다.
* XMP에는 메타데이터를 쉽게 교환할 수 있는 표준화된 인코딩이 있습니다.
* XMP은 확장 가능합니다. 에셋에 추가 정보를 추가할 수 있습니다.

XMP standard는 확장 가능하도록 설계되어 사용자 지정 메타데이터 유형을 XMP 데이터에 추가할 수 있습니다. 반면 EXIF에는 확장될 수 없는 고정 속성 목록이 있습니다.

>[!NOTE]
>
>XMP에서는 일반적으로 이진 데이터 형식을 포함할 수 없습니다. 이진 데이터(예: 썸네일 이미지)를 XMP으로 전달하려면 다음과 같이 XML에 친숙한 형식으로 인코딩해야 합니다 `Base64`.

### XMP 개념 {#xmp-core-concepts}

다음 섹션에서는 네임스페이스 및 스키마, 속성 및 값, 언어 대체 요소 등 XMP의 핵심 개념에 대해 설명합니다.

#### 네임스페이스 및 스키마 {#namespaces-and-schemata}

XMP 스키마는 데이터 형식 및 설명 정보를 포함하는 일반적인 XML 네임스페이스의 속성 이름 집합입니다. XMP 스키마는 XML 네임스페이스 URI로 식별됩니다. 네임스페이스를 사용하면 이름은 같지만 의미가 다른 여러 스키마의 속성 간 충돌을 방지할 수 있습니다.

예를 들어 `Creator` 독립적으로 디자인된 두 개의 스키마의 속성은 에셋을 만든 사람을 의미할 수 있으며, 에셋을 만든 애플리케이션(예: Adobe Photoshop)을 의미할 수도 있습니다.

#### 속성 및 값 {#properties-and-values}

XMP은 하나 이상의 스키마에서 속성을 포함할 수 있습니다. 예를 들어 많은 Adobe 애플리케이션에서 사용하는 일반적인 하위 집합은 다음과 같습니다.

* 더블린 코어 스키마: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`.
* XMP 기본 스키마: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`.
* XMP 권한 관리 스키마: `xmpRights:WebStatement`, `xmpRights:Marked`.
* XMP 미디어 관리 스키마: `xmpMM:DocumentID`.

#### 언어 대체 요소 {#language-alternatives}

XMP을 통해 다음을 추가할 수 있습니다. `xml:lang` 속성을 텍스트 속성에 추가하여 텍스트의 언어를 지정합니다.

## IPTC 메타데이터 작업 {#support-for-iptc-metadata}

방법 알아보기 [!DNL Adobe Experience Manager Assets] 는 을 통해 에셋에 추가된 IPTC 메타데이터, 크리에이티브 등급 및 키워드를 지원합니다. [!DNL Adobe Bridge] 및 기타 [!DNL Adobe Creative Cloud] 앱.

[!DNL Adobe Experience Manager Assets] 는 자산을 설명하는 데 널리 사용되는 IPTC 메타데이터 표준을 지원합니다. 이쪽으로, [!DNL Assets] 사진 작가, 광고 기획사, 도서관, 박물관 등 다양한 당사자들 사이에서 이미지 수용을 강화합니다.

에셋의 기본 메타데이터 스키마에는 IPTC 코어 및 IPTC 확장 메타데이터 스키마가 통합되어 있어 사용자가 이미지에 표시된 사람, 위치 및 제품에 대한 정확하고 신뢰할 수 있는 데이터를 추가할 수 있는 포괄적인 메타데이터 속성을 정의할 수 있습니다. 또한 이미지 만들기와 관련된 날짜, 이름 및 식별자와 유연한 권한 정보 표현 방법을 지원합니다.

이제 에셋에 대한 속성 페이지에 별도의 탭이 포함되어 있어 편집 가능한 필드에 IPTC 코어 및 IPTC 확장 프로그램 메타데이터를 표시할 수 있습니다.

1. 다음에서 [!DNL Assets] 사용자 인터페이스에서 이미지를 선택합니다.
1. 클릭 **[!UICONTROL 속성]** 을 클릭합니다.
1. 다음을 클릭합니다. **[!UICONTROL IPTC]** 탭으로 이동하여 에셋의 IPTC 메타데이터를 봅니다.
1. 필요에 따라 IPTC 메타데이터 속성을 편집합니다.

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. 다음을 클릭합니다. **[!UICONTROL IPTC 확장]** 탭으로 이동하여 에셋에 대한 IPTC 확장 메타데이터를 봅니다.
1. 필요에 따라 IPTC 확장 메타데이터 속성을 편집합니다.
1. 클릭 **[!UICONTROL 저장 및 닫기]** 변경 내용을 저장합니다.

### 크리에이티브 등급 지원 {#creative-rating-support}

이제 개별 사용자 등급 및 집계 등급을 표시할 뿐만 아니라 속성 페이지에 Adobe Bridge 및 기타 Creative Apps를 통해 자산에 할당된 등급이 표시됩니다

These ratings are available under **[!UICONTROL Creative Rating]** section within the **[!UICONTROL Advanced]** tab.

이 등급은 읽기 전용 속성이며 1~5 사이의 범위입니다. 검색 패널에서 크리에이티브 등급 을 기반으로 에셋을 검색할 수 있습니다.

그러나 이 속성은 현재 사용자가 변경한 사용자 지정 사항과의 충돌을 방지하기 위해 색인화되지 않습니다.

### 키워드 지원 {#keyword-support}

다음 **[!UICONTROL IPTC]** 의 탭 [!UICONTROL 속성] 또한 페이지는 Adobe Bridge 및 기타 Adobe Creative Cloud 앱을 통해 자산에 추가된 키워드를 표시합니다. 또한 이러한 키워드를 편집하고 **[!UICONTROL IPTC]** 탭.

![키워드](assets/keywords-in-iptc-tab.png)
