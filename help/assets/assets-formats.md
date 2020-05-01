---
title: 자산 지원 형식
description: AEM 자산 및 Dynamic Media에서 지원하는 파일 형식 및 각 형식에 지원되는 기능의 목록입니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 134530e6e4cabc31342fc3136ec3218ba5acea4a

---


# 지원되는 자산 형식 {#assets-supported-formats}

AEM Assets는 다양한 파일 형식을 지원하며 각 기능은 다양한 MIME 유형을 지원합니다.

AEM Assets를 다른 표준을 준수하는 DAM(Digital Asset Management) 솔루션 및 데스크탑 소프트웨어와 통합하려면 Adobe의 XMP(Extensible Metadata Platform)를 사용하십시오.

지원 수준을 이해하려면 범례를 사용합니다.

| 지원 수준 | 설명 |
|:---:|---|
| ✓ | 지원됨 |
| * | 추가 기능 지원 |
| − | 해당 사항 없음 |

## AEM 자산에서 지원되는 래스터 이미지 포맷 {#supported-raster-image-formats}

| 형식 | 저장 용량 | 메타데이터 관리 | 메타데이터 추출 | 축소판 생성 | 편집 | 메타데이터 원본에 쓰기 | 인사이트 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| PNM | ✓ | ✓ |  |  |  |  | ✓ |
| PGM | ✓ | ✓ |  |  |  |  | ✓ |
| PBM | ✓ | ✓ |  |  |  |  | ✓ |
| PPM | ✓ | ✓ |  |  |  |  | ✓ |
| PSD ‡ | ✓ | ✓ | ✓ | ✓ |  |  | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ |  | ✓ |  |
| PICT |  |  |  |  |  |  | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ |  |  |  |

병합된 ‡ 이미지는 PSD 파일에서 추출됩니다. 이 이미지는 Adobe Photoshop에서 생성되며 PSD 파일에 포함되어 있습니다. 설정에 따라 병합된 이미지가 실제 이미지이거나 아닐 수 있습니다.

## 다이내믹 미디어에서 지원되는 래스터 이미지 포맷(#supported-raster-image-formats-dynamic-media)

| 형식 | 업로드<br> (입력 형식) | 이미지<br> 사전 설정<br> 만들기<br> (출력 형식) | 동적<br> 변환 미리<br> 보기 | 동적<br> 표현물<br> 전달 | 동적<br> 변환<br> 다운로드 |
|---|:---:|:---:|:---:|:---:|:---:|
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ |  |  |  |  |
| PSD **** | ✓ |  |  |  |  |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ |  |  |  |  |

**병합된 이미지‡이 PSD 파일에서 추출됩니다.** 이 이미지는 Adobe Photoshop에서 생성되며 PSD 파일에 포함되어 있습니다. 설정에 따라 병합된 이미지가 실제 이미지이거나 아닐 수 있습니다.

위의 정보 이외에 다음을 고려하십시오.

* EPS 파일에 대한 지원은 래스터 이미지에만 적용됩니다. 예를 들어 EPS 벡터 이미지에 대한 축소판 생성은 기본적으로 지원되지 않습니다. 지원을 추가하려면 ImageMagick을 [구성합니다](best-practices-for-imagemagick.md). 타사 도구를 통합하여 추가 기능을 활성화하려면 [명령줄 기반 미디어 핸들러를 참조하십시오](media-handlers.md#command-line-based-media-handler).

* PSB 파일 형식이 핸들러에 추가될 때 메타데이터 원본에 대해 `NComm` 작동합니다.

* Dynamic Media를 사용하여 EPS 파일에 대한 동적 변환을 미리 보고 생성하려면 [Adobe Illustrator(AI), Postscript(EPS) 및 PDF 파일 형식을 참조하십시오.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* EPS 파일의 경우 PS-Adobe(PostScript Document Structuring Convention) 버전 3.0 이상에서 메타데이터 원본에 대한 지원이 지원됩니다.

## Dynamic Media에서 지원되지 않는 래스터 이미지 형식(#unsupported-image-formats-dynamic-media)

다음 목록은 Dynamic Media에서 지원되지 *않는* 래스터 이미지 파일 포맷의 하위 유형에 대해 설명합니다.

* IDAT 청크 크기가 100MB보다 큰 PNG 파일
* PSB 파일.
* CMYK, RGB, 회색 음영 또는 비트맵 이외의 색상 공간이 있는 PSD 파일은 지원되지 않습니다. DuoTone, Lab 및 Indexed 색상 공간은 지원되지 않습니다.
* 16보다 비트 심도가 높은 PSD 파일
* 부동 소수점 데이터가 있는 TIFF 파일
* Lab 색상 공간이 있는 TIFF 파일

<!-- Topic commented out for now as of March 31, 2020. The topic may still need adjustment so it can be published live, or it may be moved into a KB article instead. Just waiting on feedback in CQDOC-15657. - Rick
## Unsupported raster image formats in Dynamic Media (#unsupported-image-formats-dynamic-media)

The following table describes the sub-types of raster image formats that are *not* supported in Dynamic Media. The table also describes suggested methods you can use to detect such files.

| Format | What is unsupported? | Suggested detection method |
|---|---|---|
| JPEG  | Files where the initial three bytes is incorrect. | To identify a JPEF file, its initial three bytes must be `ff d8 ff`. If they are anything else, then it is not classified as a JPEG.<br>&bull; There is no software tool that can help with this issue.<br>&bull; A small C++/java program which reads the initial three bytes of a file should be able to detect these types of files.<br>&bull; It may be better to track the source of such files and look at the tool generating the file. |
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

Adobe PDF 래스터라이저 라이브러리는 컨텐츠 집약적이고 규모가 큰 Adobe Illustrator 및 PDF 파일에 대한 고품질 축소판과 미리 보기를 생성합니다. PDF 래스터라이저 라이브러리를 사용하는 것이 좋습니다.

* 처리해야 하는 리소스가 많은 AI/PDF 파일
* 축소판이 기본적으로 생성되지 않는 AI/PDF 파일
* PMS(Pantone Matching System) 색상이 있는 AI 파일

See [Using PDF Rasterizer](aem-pdf-rasterizer.md).

## 지원되는 이미지 트랜스코딩 라이브러리 {#supported-image-transcoding-library}

Adobe Imaging Transcoding 라이브러리는 인코딩, 트랜스코딩, 리샘플링 및 크기 조정과 같은 핵심 이미지 처리 기능을 수행하는 이미지 처리 솔루션입니다.

이미징 트랜스코딩 라이브러리는 JPG/JPEG, PNG(8비트 및 16비트), GIF, BMP, TIFF/Compressed TIFF(32비트 TIFF 파일 및 PTIFF 파일 제외), ICO 및 ICN MIME 유형을 지원합니다.

See [Imaging Transcoding Library](imaging-transcoding-library.md).

## 지원되는 Camera Raw {#supported-camera-raw}

Adobe Camera Raw 라이브러리를 사용하면 AEM Assets에서 Raw 이미지를 인제스트할 수 있습니다. See [Camera Raw support](camera-raw.md).

## 지원되는 자산 문서 형식 {#supported-document-formats}

자산 관리 기능에 지원되는 문서 형식은 다음과 같습니다.

<!--
DO NOT PUBLISH THIS TABLE -- Removing it as it got malformed during GitHub migration.

| Format | Storage | Metadata management | Metadata extraction | Thumbnail generation | Interactive editing | Metadata writeback | [Insights](touch-ui-asset-insights.md) | [Connected Assets](use-assets-across-connected-assets-instances.md) |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | &#10003; | &#10003; | | &#10003; | &#10003; | &#10003; | &#10003; | |
| DOC | &#10003; | &#10003; | &#10003; | &#10003; | | | | &#10003; |
| DOCX | &#10003; | &#10003; | &#10003; | &#10003; | | | | &#10003; |
| ODT | &#10003; | &#10003; | &#10003; | | | | | &#10003; |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; |
| HTML | &#10003; | &#10003; | &#10003; | | | | | &#10003; |
| RTF | &#10003; | &#10003; | &#10003; | | | | | &#10003; |
| TXT | &#10003; | &#10003; | &#10003; | | | | | &#10003; |
| XLS | &#10003; | &#10003; | &#10003; | | | | | &#10003; |
| XLSX | &#10003; | &#10003; | &#10003; | &#10003; | | | | &#10003; |
| ODS | &#10003; | &#10003; | &#10003; | | | | | |
| PPT | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | | &#10003; |
| PPTX | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | | &#10003; |
| ODP | &#10003; | &#10003; | &#10003; | | | | | |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | &#10003; | &#10003; | | &#10003; | &#10003; | &#10003; | &#10003; | |
| PS | &#10003; | &#10003; | | | | | | |
| QXP | &#10003; | &#10003; | | | | | | |
| EPUB | &#10003; | &#10003; | | &#10003; | &#10003; | | | |
-->

| 형식 | 저장 용량 | [메타데이터 관리](metadata.md) | 전체 텍스트<br> 추출 | [메타데이터 추출](metadata.md) | 축소판<br> 생성 | [하위 자산 추출](managing-linked-subassets.md) | [메타데이터 원본에 쓰기](xmp-writeback.md) | [연결된 자산](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |  |
| DOC | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| ODT | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| RTF | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| TXT | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| XLS | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| ODS | ✓ | ✓ | ✓ |  |  |  |  |  |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| ODP | ✓ | ✓ | ✓ |  |  |  |  |  |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |  |
| PS | ✓ | ✓ |  |  |  |  |  |  |
| QXP | ✓ | ✓ |  |  |  |  |  |  |
| EPUB | ✓ | ✓ |  | ✓ | ✓ |  |  |  |

## Dynamic Media에서 지원되는 문서 포맷(#supported-document-formats-dynamic-media)

| 형식 | 업로드<br> (입력 형식) | 이미지<br> 사전 설정<br> 만들기<br> (출력 형식) | 동적<br> 변환 미리<br> 보기 | 동적<br> 표현물<br> 전달 | 동적<br> 변환<br> 다운로드 |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ |  |  |  |  |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ |  |  |  |  |

위의 기능 외에 다음을 고려하십시오.

* Dynamic Media를 사용하여 PDF 파일에 대한 동적 변환을 생성하려면 [Adobe Illustrator(AI), Postscript(EPS) 및 PDF 파일 형식을 참조하십시오.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Dynamic Media를 사용하여 AI 파일에 대한 동적 변환을 미리 보고 생성하려면 [Adobe Illustrator(AI), Postscript(EPS) 및 PDF 파일 형식을 참조하십시오.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Dynamic Media를 사용하여 INDD 파일에 대한 동적 변환을 생성하려면 [InDesign(INDD) 파일 형식을 참조하십시오](../assets/managing-image-presets.md#indesign-indd-file-format).

## 지원되는 멀티미디어 포맷 {#supported-multimedia-formats}

|  | 저장 용량 | 메타데이터 관리 | 메타데이터 추출 | 축소판 생성 | FFMPEG 트랜스코딩 |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ |  | − | * |
| MIDI | ✓ | ✓ |  | − | * |
| 3GP | ✓ | ✓ |  | − | * |
| MP3 | ✓ | ✓ | ✓ | − | * |
| MPG | ✓ | ✓ |  | − | * |
| OGA | ✓ | ✓ |  | − | * |
| OGG | ✓ | ✓ |  | − | * |
| RA | ✓ | ✓ |  | − | * |
| WAV | ✓ | ✓ |  | − | * |
| WMA | ✓ | ✓ |  | − | * |
| DVI | ✓ | ✓ |  | * | * |
| FLV | ✓ | ✓ |  | * | * |
| M4V | ✓ | ✓ |  | * | * |
| MPEG | ✓ | ✓ |  | * | * |
| OGV | ✓ | ✓ |  | * | * |
| MOV | ✓ | ✓ |  | * | * |
| WMV | ✓ | ✓ |  | * | * |
| SWF | ✓ | ✓ |  |  |  |

## Dynamic Media에서 트랜스코딩에 지원되는 입력 비디오 포맷 {#supported-input-video-formats-for-dynamic-media-transcoding}

| 비디오 파일 확장자 | 컨테이너 | 권장 비디오 코덱스 | 지원되지 않는 비디오 코덱입니다. |
|---|---|---|---|
| MP4 | MPEG-4 | H264/AVC(모든 프로필) |  |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 &amp; HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV(DV25), Apple PhotoJPEG, Sorenson, Avid DNHD, Avid AVR | Apple Intermediate, Apple Animation |
| FLV, F4V | Adobe Flash | H264/AVC, Flix VP6, H263, Sorenson | SWF(벡터 애니메이션 파일) |
| WMV | Windows Media 9 | WMV3(v9), WMV2(v8), WMV1(v7), GoToMeeting (G2M2, G2M3, G2M4) | Microsoft Screen(MSS2), Microsoft Photo Story(WVP2) |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 |  |
| M4V | Apple iTunes | H264/AVC |  |
| AVI | A/V 인터리브 | XVID, DIVX, HDV, MiniDV(DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3(IV30), MJPEG, Microsoft Video 1(MS-CRAM) |
| WebM | WebM | Google VP8 |  |
| OGV, OGG | Ogg | Theora, VP3, Dirac |  |
| MXF | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro |  |
| MTS | AVCHD | H264/AVC |  |
| MKV | 마트로스카 | H264/AVC |  |
| R3D, RM | Red Raw 비디오 | MJPEG 2000 |  |
| RAM, RM | RealVideo | 지원되지 않음 | Real G2(RV20), Real 8(RV30), Real 10(RV40) |
| FLAC | 기본 Flac | 무손실 오디오 코덱입니다. |  |
| MJ2 | 모션 JPEG 2000 | 모션 JPEG 2000 코덱입니다. |  |

## 지원되는 아카이브 포맷 {#supported-archive-formats}

지원되는 아카이브 포맷 및 일반 DAM 워크플로우의 적용 가능성.

| 형식 | 저장 용량 | 버전 관리 | 워크플로우 | 게시 | 액세스 제어 | 다이내믹 미디어 전달 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## 기타 지원되는 포맷 {#other-supported-formats}

기타 몇 가지 파일 포맷에 대한 일반적인 DAM 워크플로우의 적용 방법은 아래 표에 설명되어 있습니다. Dynamic Media Delivery를 제외한 저장소, 버전 관리, ACL, 워크플로우, 게시 및 메타데이터 관리와 같은 일반적인 DAM 기능이 모든 파일에 대해 지원됩니다.

| 형식 | 저장 용량 | 버전 관리 | 워크플로우 | 게시 | 액세스 제어 | 다이내믹 미디어 전달 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript(고유한 배달 도메인으로 구성된 경우) |  |  |  |  |  | ✓ |

## Supported MIME types {#supported-mime-types}

기본적으로 AEM은 파일 확장명을 사용하여 파일 유형을 감지합니다. AEM은 파일의 내용에서 검색할 수 있습니다. 후자의 경우, AEM 웹 콘솔 [!UICONTROL 의] 일 CQ DAM MIME 유형 서비스에서  컨텐트에서 MIME 감지 옵션을 선택합니다.

지원되는 MIME 유형 목록은 에서 CRXDE Lite를 참조하십시오 `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`.

| 파일 확장자 | MIME 유형/인터넷 미디어 유형 | 기본 jobParam 값 | 허용되는 jobParam 값 |
|---|---|---|---|
| 이미지 | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | 기본 jobParam은 모든 이미지 MIME 유형 자산에 적용됩니다.<ul><li>[knockoutBackgroundOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_knockout_background_options.html)</li><li>manualCropOptions</li><li>[autoColorCropOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_auto_color_crop_options)</li><li>[autoTransparentCropOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_auto_transparent_crop_options)</li><li>[colorManagementOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_color_management_options.html)</li><li>[autoSetCreationOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_auto_set_creation_options.html)</li><li>[emailSetting](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/string_constants/index.html?f=r_email_settings)</li><li>[xmpKeywords](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_xmp_keywords)</li><li>[unsharpMaskOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_unsharp_mask_options.html)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| 3GP | video/3gpp |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_exclude_master_video_from_avs) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_post_script_options.html)</li><li> [illustratorOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_illustrator_options.html)</li></ul> |
| AIFF | 오디오/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| BMP | image/bmp |  |  |
| CSS | 텍스트/css |  |  |
| DOC | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>애플리케이션/eps</li><li>application/x-eps</li><li>이미지/eps</li><li>image/x-eps</li></ul> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | image/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| M4V | video/x-m4v |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MPEG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MPG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_pdf_options) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | image/png |  |  |
| PPT | application/vnd.ms-powerpoint |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_post_script_options)</li><li>[illustratorOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_illustrator_options)</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_photoshop_options)</li><li>[photoshopLayerOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_photoshop_layer_options.html)</li></ul> |
| RTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF/TIFF | image/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | 비디오/dvd |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| VTT | 텍스트/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| XLS | application/vnd.ms-excel |  |  |
| ZIP | application/zip |  |  |

>[!MORELIKETHIS]
>
>* [MIME 유형 기반 자산/Scene7 업로드 작업 매개 변수 지원을 활성화합니다](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).
>* [업로드 작업 매개 변수 지원을 위해 MIME 형식 기반 구성을 참조하십시오](config-dynamic.md).

