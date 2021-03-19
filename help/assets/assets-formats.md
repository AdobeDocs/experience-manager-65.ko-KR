---
title: 지원되는 파일 형식 및 MIME 형식
description: 파일 형식 및 MIME 유형은  [!DNL Assets] and [!DNL Dynamic Media] 에서 지원하며 각 형식에 대해 지원되는 기능입니다.
contentOwner: AG
role: 비즈니스 전문가, 관리자
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '1582'
ht-degree: 10%

---


# [!DNL Adobe Experience Manager Assets] {#assets-supported-formats}에서 지원되는 형식

[!DNL Experience Manager Assets] 다양한 파일 형식을 지원하며 각 기능은 서로 다른 MIME 유형에 대한 다양한 지원을 제공합니다. [!DNL Assets]을(를) 다른 표준을 준수하는 DAM(디지털 자산 관리) 솔루션 및 데스크탑 소프트웨어와 통합하려면 Adobe [!DNL Extensible Metadata Platform](XMP)을 사용하십시오.

지원 수준을 이해하려면 범례를 사용합니다.

| 지원 수준 | 설명 |
| :-----------: | ------------------------------ |
| ✓ | 지원됨 |
| * | 추가 기능 지원 |
| - | 해당 없음 |

## [!DNL Experience Manager] {#supported-raster-image-formats}에서 지원되는 래스터 이미지 형식

[!DNL Assets]에서 지원되는 래스터 이미지 형식은 다음과 같습니다.

| 형식 | 저장 용량 | 메타데이터 관리 | 메타데이터 추출 | 축소판 생성 | 편집 | 메타데이터 원본에 쓰기 | 인사이트 |
| ------------ | :------: | :-----------------: | :-----------------: | :------------------: | :------: | :----------------: | :------: |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| PNM | ✓ | ✓ | - | - | - | - | ✓ |
| PGM | ✓ | ✓ | - | - | - | - | ✓ |
| PBM | ✓ | ✓ | - | - | - | - | ✓ |
| PPM | ✓ | ✓ | - | - | - | - | ✓ |
| PSD ‡ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | - | ✓ | - |
| PICT | - | - | - | - | - | - | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ | - | - | - |

병합된 ‡ 이미지가 PSD 파일에서 추출됩니다. Adobe Photoshop에서 생성되며 PSD 파일에 포함되어 있는 이미지입니다. 설정에 따라 병합된 이미지가 실제 이미지이거나 아닐 수 있습니다.

[!DNL Dynamic Media]에서 지원되는 래스터 이미지 형식은 다음과 같습니다.

| 형식 | 업로드<br>(입력 형식) | <br> 이미지<br> 사전 설정<br> 만들기(출력 형식) | 미리 보기<br> 동적<br> 변환 | <br> 동적<br> 변환 전달 | <br> dynamic<br> 변환 다운로드 |
|---|:---:|:---:|:---:|:---:|:---:|
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | - | - | - | - |
| PSD ‡ | ✓ | - | - | - | - |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ | - | - | - | - |

병합된 ‡ 이미지가 PSD 파일에서 추출됩니다. Adobe Photoshop에서 생성되며 PSD 파일에 포함되어 있는 이미지입니다. 설정에 따라 병합된 이미지가 실제 이미지이거나 아닐 수 있습니다.

위의 정보 이외에 다음을 고려하십시오.

* EPS 파일에 대한 지원은 래스터 이미지에만 적용됩니다. 예를 들어 EPS 벡터 이미지에 대한 축소판 생성은 기본적으로 지원되지 않습니다. 지원을 추가하려면 [ImageMagick](best-practices-for-imagemagick.md)을 구성합니다. 추가 기능을 사용하도록 타사 도구를 통합하려면 [명령줄 기반 미디어 핸들러](media-handlers.md#command-line-based-media-handler)를 참조하십시오.

* 메타데이터 원본에 대해서는 PSB 파일 형식이 `NComm` 처리기에 추가될 때 작동합니다.

* [!DNL Dynamic Media]을 사용하여 EPS 파일에 대한 동적 변환을 미리 보고 생성하려면 [Adobe Illustrator(AI), Postscript(EPS) 및 PDF 파일 형식을 참조하십시오.](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* EPS 파일의 경우 PS-Adobe(PostScript Document Structuring Convention) 버전 3.0 이상에서 메타데이터 원본에 대한 지원이 지원됩니다.

## 지원되는 3D 형식 {#support-3d-formats}

다음 3D 형식 목록이 지원됩니다.

Dynamic Media에서 [3D 자산 작업을 참조하십시오.](/help/assets/assets-3d.md)

| 형식 | 저장 용량 | 버전 관리 | 워크플로우 | 게시 | 액세스 제어 | 축소판 미리 보기 | 3D 미리 보기 | Dynamic Media 전달 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ |  | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ |  | ✓ | - | ✓ | - |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |

## Dynamic Media {#unsupported-image-formats-dynamic-media}에서 지원되지 않는 래스터 이미지 형식

다음 목록은 Dynamic Media에서 지원되지 *않는 래스터 이미지 파일 형식의 하위 유형에 대해 설명합니다.*

Dynamic Media](https://helpx.adobe.com/experience-manager/kb/detect-unsupported-assets-for-dynamic-media.html)에 대해 지원되지 않는 파일 형식 감지를 참조하십시오.[

* IDAT 청크 크기가 100MB보다 큰 PNG 파일.
* PSB 파일.
* CMYK, RGB, 회색 음영 또는 비트맵 이외의 색상 공간이 있는 PSD 파일은 지원되지 않습니다. DuoTone, Lab 및 인덱스 색상 공간은 지원되지 않습니다.
* 비트 심도가 16보다 큰 PSD 파일
* 부동 소수점 데이터가 있는 TIFF 파일
* Lab 색상 공간이 있는 TIFF 파일

<!-- Topic commented out for now as of March 31, 2020. The topic may still need adjustment so it can be published live, or it may be moved into a KB article instead. Just waiting on feedback in CQDOC-15657. - Rick
## Unsupported raster image formats in Dynamic Media (#unsupported-image-formats-dynamic-media)

The following table describes the sub-types of raster image formats that are *not* supported in Dynamic Media. The table also describes suggested methods you can use to detect such files.

| Format | What is unsupported? | Suggested detection method |
|---|---|---|
| JPEG  | Files where the initial three bytes is incorrect. | To identify a JPEG file, its initial three bytes must be `ff d8 ff`. If they are anything else, then it is not classified as a JPEG.<br>&bull; There is no software tool that can help with this issue.<br>&bull; A small C++/java program which reads the initial three bytes of a file should be able to detect these types of files.<br>&bull; It may be better to track the source of such files and look at the tool generating the file. |
| PNG |  Files that have an IDAT chunk size greater than 100 MB. | You can detect this issue using [libpng](http://www.libpng.org/pub/png/libpng.html) in C++. |
| PSB |  | Use exiftool if the file type is PSB.<br>Example in an ExifTool log:<br>1. File type: `PSB` |
| PSD | Files with a color space other than CMYK, RGB, Grayscale, or Bitmap are not supported.<br>DuoTone, Lab, and Indexed color spaces are not supported. | Use ExifTool if Color mode is Duotone.<br>Example in an ExifTool log:<br>1. Color mode: `Duotone` |
|  | Files with abrupt endings. | Adobe is unable to detect this condition. Also, such files cannot be opened with Adobe PhotoShop. Adobe suggests you examine the tool that was used to create such a file and troubleshoot at the source. |
|  | Files that have a bit depth greater than 16. | Use ExifTool if the bit depth is greater than 16.<br>Example in an ExifTool log:<br>1. Bit depth: `32` |
|  | File that have Lab color space. | Use exiftool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
| TIFF | Files that have floating point data. That is, a TIFF file with 32-bit depth is not supported. | Use ExifTool if the MIME type is `image/tiff` and the SampleFormat has `Float` in its value. Example in an ExifTool log:<br>1. MIME type: `image/tiff`<br>Sample format: `Float #`<br>2. MIME type: `image/tiff`<br>Sample format: `Float; Float; Float; Float` |
|  | Files that have Lab color space. | Use ExifTool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
-->

## 지원되는 PDF 래스터라이저 라이브러리 {#supported-pdf-rasterizer-library}

Adobe PDF 래스터라이저 라이브러리는 콘텐트를 많이 사용하는 [!DNL Adobe Illustrator] 및 PDF 파일의 고품질 축소판과 미리 보기를 생성합니다. Adobe에서는 다음 항목에 PDF 래스터라이저 라이브러리를 사용하는 것이 좋습니다.

* 많은 리소스를 필요로 하는 AI/PDF 파일을 처리할 수 있습니다.
* 축소판이 기본적으로 생성되지 않는 AI/PDF 파일.
* PMS(Pantone Matching System) 색상이 있는 AI 파일

[PDF 래스터라이저 사용](aem-pdf-rasterizer.md)을 참조하십시오.

## 지원되는 이미지 코드 변환 라이브러리 {#supported-image-transcoding-library}

Adobe 이미징 트랜스코딩 라이브러리는 인코딩, 트랜스코딩, 리샘플링 및 크기 조정과 같은 핵심 이미지 처리 기능을 수행하는 이미지 처리 솔루션입니다.

이미징 코드 변환 라이브러리는 JPG/JPEG, PNG(8비트 및 16비트), GIF, BMP, TIFF/Compressed TIFF(32비트 TIFF 파일 및 PTIFF 파일 제외), ICO 및 ICN MIME 유형을 지원합니다.

[이미징 코드 변환 라이브러리](imaging-transcoding-library.md)를 참조하십시오.

## 지원되는 Camera Raw {#supported-camera-raw}

[!DNL Adobe Camera Raw] 라이브러리를 사용하면 [!DNL Assets]이(가) 원시 이미지를 인제스트할 수 있습니다. [Camera Raw 지원](camera-raw.md)을 참조하십시오.

## 지원되는 [!DNL Assets] 문서 형식 {#supported-document-formats}

자산 관리 기능에 지원되는 문서 형식은 다음과 같습니다.

| 형식 | 저장 용량 | [메타데이터 관리](metadata.md) | 전체 텍스트<br> 추출 | [메타데이터 추출](metadata.md) | 축소판<br> 생성 | [하위 자산 추출](managing-linked-subassets.md) | [메타데이터 원본에 쓰기](xmp-writeback.md) | [연결된 자산](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ | - |
| DOC | ✓ | ✓ | ✓ | ✓ | - | - | - | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | - | - | - | ✓ |
| ODT | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| RTF | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| TXT | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| XLS | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | - | - | - | ✓ |
| ODS | ✓ | ✓ | ✓ | - | - | - | - | - |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| ODP | ✓ | ✓ | ✓ | - | - | - | - | - |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ | - |
| PS | ✓ | ✓ | - | - | - | - | - | - |
| QXP | ✓ | ✓ | - | - | - | - | - | - |
| EPUB | ✓ | ✓ | - | ✓ | ✓ | - | - | - |

## Dynamic Media {#supported-document-formats-dynamic-media}에서 지원되는 문서 형식

| 형식 | 업로드<br>(입력 형식) | <br> 이미지<br> 사전 설정<br> 만들기(출력 형식) | 미리 보기<br> 동적<br> 변환 | <br> 동적<br> 변환 전달 | <br> dynamic<br> 변환 다운로드 |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | - | - | - | - |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | - | - | - | - |

위의 기능 외에 다음 사항을 고려하십시오.

* Dynamic Media을 사용하여 PDF 파일에 대한 동적 변환을 생성하려면 [Adobe Illustrator(AI), Postscript(EPS) 및 PDF 파일 형식을 참조하십시오.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Dynamic Media을 사용하여 AI 파일에 대한 동적 변환을 미리 보고 생성하려면 [Adobe Illustrator(AI), Postscript(EPS) 및 PDF 파일 형식을 참조하십시오.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Dynamic Media을 사용하여 INDD 파일에 대한 동적 변환을 생성하려면 [InDesign(INDD) 파일 형식](../assets/managing-image-presets.md#indesign-indd-file-format)을(를) 참조하십시오.

## 지원되는 멀티미디어 형식 {#supported-multimedia-formats}

|  | 저장 용량 | 메타데이터 관리 | 메타데이터 추출 | 축소판 생성 | FFmpeg 트랜스코딩 |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ | - | - | * |
| MIDI | ✓ | ✓ | - | - | * |
| 3GP | ✓ | ✓ | - | - | * |
| MP3 | ✓ | ✓ | ✓ | - | * |
| MPG | ✓ | ✓ | - | - | * |
| OGA | ✓ | ✓ | - | - | * |
| OGG | ✓ | ✓ | - | - | * |
| RA | ✓ | ✓ | - | - | * |
| WAV | ✓ | ✓ | - | - | * |
| WMA | ✓ | ✓ | - | - | * |
| DVI | ✓ | ✓ | - | * | * |
| FLV | ✓ | ✓ | - | * | * |
| M4V | ✓ | ✓ | - | * | * |
| MPEG | ✓ | ✓ | - | * | * |
| OGV | ✓ | ✓ | - | * | * |
| MOV | ✓ | ✓ | - | * | * |
| WMV | ✓ | ✓ | - | * | * |
| SWF | ✓ | ✓ | - | - | - |

## {#supported-input-video-formats-for-dynamic-media-transcoding} 트랜스코딩에 대해 Dynamic Media에서 지원되는 입력 비디오 형식

| 비디오 파일 확장명 | 컨테이너 | 권장 비디오 코덱입니다. | 지원되지 않는 비디오 코덱입니다. |
|---|---|---|---|
| MP4 | MPEG-4 | H264/AVC(모든 프로파일) | - |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 &amp; HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV(DV25), Apple PhotoJPEG, Sorenson, Avid HD, Avid AVR | Apple Intermediate, Apple Animation |
| FLV, F4V | Adobe Flash | H264/AVC, Flix VP6, H263, Sorenson | SWF(벡터 애니메이션 파일) |
| WMV | Windows Media 9 | WMV3(v9), WMV2(v8), WMV1(v7), GoToMeeting(G2M2, G2M3, G2M4) | Microsoft Screen(MSS2), Microsoft Photo Story(WVP2) |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | - |
| M4V | Apple iTunes | H264/AVC | - |
| AVI | A/V 인터리브 | XVID, DIVX, HDV, MiniDV(DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3(IV30), MJPEG, Microsoft Video 1(MS-CRAM) |
| WebM | WebM | Google VP8 | - |
| OGV, OGG | Ogg | Theora, VP3, Dirac | - |
| MXF | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro | - |
| MTS | AVCHD | H264/AVC | - |
| MKV | Matroska | H264/AVC | - |
| R3D, RM | Red Raw 비디오 | MJPEG 2000 | - |
| RAM, RM | RealVideo | 지원되지 않음 | Real G2(RV20), Real 8(RV30), Real 10(RV40) |
| FLAC | 기본 Flac | 무손실 오디오 코덱입니다. | - |
| MJ2 | 모션 JPEG 2000 | Motion JPEG 2000 코덱입니다. | - |

## 지원되는 아카이브 형식 {#supported-archive-formats}

지원되는 아카이브 포맷 및 일반적인 DAM 워크플로우의 적용 사례는 다음 표에 나와 있습니다.

| 형식 | 저장 용량 | 버전 관리 | 워크플로우 | 게시 | 액세스 제어 | Dynamic Media 전달 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## 지원되는 기타 형식 {#other-supported-formats}

몇 가지 특정 파일 형식에 대한 일반적인 DAM 기능의 적용 방법은 아래에 설명되어 있습니다.

| 형식 | 저장 용량 | 버전 관리 | 워크플로우 | 게시 | 액세스 제어 | Dynamic Media 전달 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript(자체 배달 도메인으로 구성된 경우) | - | - | - | - | - | ✓ |

>[!NOTE]
>
>JavaScript 파일을 업로드하고 배포하는 것이 안전하거나 안전하지 않을 수 있습니다. 필요한 경우 오버레이를 사용하여 사용자가 JS 파일을 업로드하지 못하도록 할 수 있습니다.

## 지원되는 MIME 유형 {#supported-mime-types}

기본적으로 [!DNL Experience Manager]은 파일 확장명을 사용하여 파일 유형을 감지합니다. [!DNL Experience Manager] 파일의 내용에서 검색할 수 있습니다. 후자의 경우 [!DNL Experience Manager] 웹 콘솔에서 [!UICONTROL 일 CQ DAM MIME 유형 서비스]에서 [!UICONTROL 내용] 옵션에서 MIME 감지를 선택합니다.

지원되는 MIME 유형 목록은 `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`의 CRXDE Lite에서 사용할 수 있습니다.

| 파일 확장명 | MIME 유형/인터넷 미디어 유형 | 기본 jobParam 값 | 허용되는 jobParam 값 |
|---|---|---|---|
| 이미지 | 이미지/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | 기본 jobParam은 모든 이미지 MIME 유형 자산에 적용됩니다.<ul><li>[knockoutBackgroundOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-knockout-background-options.html)</li><li>[manualCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-manual-crop-options.html)</li><li>[autoColorCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-color-crop-options.html)</li><li>[autoTransparentCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-transparent-crop-options.html)</li><li>[colorManagementOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-color-management-options.html)</li><li>[autoSetCreationOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-set-creation-options.html)</li><li>[emailSetting](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/sting-constants/r-email-settings.html)</li><li>[xmpKeywords](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-xmp-keywords.html)</li><li>[unsharpMaskOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-unsharp-mask-options.html)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| 3GP | 비디오/3gpp |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li> [illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html)</li></ul> |
| AIFF | 오디오/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| BMP | image/bmp |  |  |
| CSS | 텍스트/css |  |  |
| 문서 | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>애플리케이션/eps</li><li>application/x-eps</li><li>이미지/eps</li><li>image/x-eps</li></ul> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | 이미지/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| M4V | video/x-m4v |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPEG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-pdf-options.html) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | image/png |  |  |
| PPT | application/vnd.ms-powerpoint |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li>[illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options.html)</li><li>[photoshopLayerOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-layer-options.html)</li></ul> |
| RTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF / TIFF | image/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | 비디오/dvd |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| VTT | 텍스트/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| XLS | application/vnd.ms-excel |  |  |
| ZIP | application/zip |  |  |

>[!MORELIKETHIS]
>
>* [MIME 유형 기반 자산 및 Dynamic Media Classic 업로드 작업 매개 변수 지원을 활성화합니다](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).
>* [업로드 작업 매개 변수 지원을 위해 MIME 유형 기반](config-dynamic.md) 구성

