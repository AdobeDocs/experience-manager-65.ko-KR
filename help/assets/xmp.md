---
title: AEM 자산에서 XMP 메타데이터 지원
description: 메타데이터 관리를 위해 AEM 자산에서 사용하는 XMP(Extensible Metadata Platform) 메타데이터 표준에 대해 알아봅니다. XMP는 다양한 애플리케이션에서 메타데이터를 작성, 처리 및 교환하기 위한 표준 형식을 제공합니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# XMP 메타데이터 {#xmp-metadata}

XMP(Extensible Metadata Platform)는 모든 메타데이터 관리를 위해 AEM 자산에서 사용하는 메타데이터 표준입니다. XMP는 다양한 애플리케이션에서 메타데이터를 작성, 처리 및 교환하기 위한 표준 형식을 제공합니다.

모든 파일 포맷에 임베드할 수 있는 범용 메타데이터 인코딩을 제공하는 것 외에도 XMP는 리치 [컨텐츠 모델을](xmp.md#xmp-core-concepts) 제공하고 Adobe 및 다른 회사에서 [지원되므로 AEM 자산과](xmp.md#advantages-of-xmp) 함께 XMP 사용자는 강력한 플랫폼을 사용하여 구축할 수 있습니다.

XMP [사양은](https://www.adobe.com/devnet/xmp.html) Adobe에서 제공됩니다.

## XMP 소개 {#what-is-xmp}

AEM Assets는 기본적으로 Adobe가 주도하는 확장 가능한 메타데이터 플랫폼인 XMP를 지원합니다. XMP 파섹 XMP 파섹

예를 들어 프로덕션 전문가는 Adobe 애플리케이션에서 내장된 XMP 지원을 사용하여 다양한 파일 포맷에 정보를 전달할 수 있습니다. AEM Assets 리포지토리는 XMP 메타데이터를 추출하여 이를 사용하여 콘텐츠 라이프사이클을 관리하고 자동화 워크플로우를 만드는 기능을 제공합니다.

XMP는 데이터 모델, 스토리지 모델 및 스키마를 제공하여 메타데이터가 정의, 생성 및 처리되는 방식을 표준화합니다. 이러한 모든 개념은 이 섹션에서 다룹니다.

EXIF, ID3 또는 Microsoft Office의 모든 기존 메타데이터는 XMP로 자동 변환되므로 제품 카탈로그와 같은 고객별 메타데이터 스키마를 지원하도록 확장할 수 있습니다.

XMP의 메타데이터는 속성 세트로 구성됩니다. 이러한 속성은 항상 리소스라고 하는 특정 엔티티와 연결됩니다.즉, 속성은 리소스에서 &quot;정보&quot;입니다. XMP의 경우 리소스는 항상 자산입니다.

### Adobe {#adobe}

Adobe는 XMP 표준을 Adobe Acrobat 소프트웨어 제품의 일부로 처음 도입했습니다. 그 이후로, XMP 표준은 널리 채택되었다.

### XMP 에코시스템 {#xmp-ecosystem}

XMP는 정의된 메타데이터 항목 집합과 함께 사용할 수 있는 [메타데이터](https://en.wikipedia.org/wiki/Metadata) 모델을 정의합니다. 또한 XMP는 사진 촬영, [스캔](https://en.wikipedia.org/wiki/XML_schema) 또는 텍스트로 제작, 사진 편집 단계( [자르기](https://en.wikipedia.org/wiki/Image_scanner)또는 색상 조정 등)에서 최종 이미지를 결합하는 등 다양한 처리 단계를 거칠 때 리소스의 내역을 기록하는 데 유용한 기본 속성에 대한 특정 [스키마를](https://en.wikipedia.org/wiki/Cropping_%28image%29) 정의합니다. XMP를 사용하면 각 소프트웨어 프로그램 또는 디바이스에서 자신의 정보를 디지털 리소스에 추가할 수 있으며, 이를 최종 디지털 파일로 저장할 수 있습니다.

XMP는 XML로 표현되는 W3C [RDF](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium) ( [Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) )의 하위 집합을 사용하여 [가장 일반적으로 시리얼라이즈 및](https://en.wikipedia.org/wiki/XML)저장됩니다.

## XMP의 이점 {#advantages-of-xmp}

XMP는 다른 인코딩 표준 및 구성표에 비해 다음과 같은 이점이 있습니다.

* XMP 기반의 메타데이터는 매우 강력하고 세밀하게 조정됩니다.
* XMP를 사용하면 하나의 속성에 여러 값을 사용할 수 있습니다.
* XMP 파섹
* XMP는 확장 가능합니다. 자산에 추가 정보를 추가할 수 있습니다.

### 확장 가능 {#extensible}

XMP 표준은 XMP 데이터에 사용자 정의 유형의 메타데이터를 추가할 수 있도록 설계되어 있습니다. 반면 EXIF는 확장될 수 없는 고정 속성 목록이 있습니다.

>[!NOTE]
>
>일반적으로 XMP에서는 이진 데이터 형식을 포함할 수 없습니다. 이진 데이터를 XMP로 가져오려면 축소판 이미지와 같은 XML 친화적인 형식으로 인코딩해야 합니다 `Base64`.

## XMP 코어 개념 {#xmp-core-concepts}

다음 섹션에서는 네임스페이스, 스키마, 속성 및 값, 언어 대체 요소 등 XMP의 핵심 개념을 설명합니다.

### 네임스페이스 및 스키마 {#namespaces-and-schemata}

XMP 스키마는 데이터 유형 및 설명 정보를 포함하는 공통 XML 네임스페이스의 속성 이름 세트입니다. XMP 스키마는 XML 네임스페이스 URI로 식별됩니다. 네임스페이스를 사용하면 이름이 같지만 의미가 다른 여러 스키마에서 속성 간 충돌을 방지할 수 있습니다.

예를 들어, 독립적으로 디자인된 두 스키마의 `Creator` 속성은 자산을 만든 사람이나 자산을 만든 응용 프로그램(예: Adobe Photoshop)을 의미할 수 있습니다.

### 속성 및 값 {#properties-and-values}

XMP에는 하나 이상의 스키마에서 생성된 속성이 포함될 수 있습니다.

예를 들어 많은 Adobe 애플리케이션에서 사용되는 일반적인 하위 세트에는 다음이 포함될 수 있습니다.

* 더블린 코어 스키마:dc:title, dc:creator, dc:subject, dc:format, dc:rights
* XMP 기본 스키마:xmp:CreateDate, xmp:CreatorTool, xmp:ModifyDate, xmp:metadataDate
* XMP 권한 관리 스키마:xmpRights:WebStatement, xmpRights:Marked
* XMP 미디어 관리 스키마:xmpMM:DocumentID

### 언어 대체 요소 {#language-alternatives}

XMP에서는 텍스트 속성에 속성을 추가하여 텍스트 언어를 지정할 수 있는 기능을 제공합니다. `xml:lang`
