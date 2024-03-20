---
title: 지원되는 파일 형식 및 MIME 유형
description: 에서 지원하는 파일 형식 및 MIME 유형 [!DNL Assets] 및 [!DNL Dynamic Media] 각 형식에 대해 지원되는 기능을 사용할 수 있습니다.
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Asset Management,Renditions
exl-id: a4bcf67b-54f4-4681-9e42-fd4753acde1a
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1872'
ht-degree: 25%

---

# 에서 지원되는 형식 [!DNL Adobe Experience Manager Assets] {#assets-supported-formats}

[!DNL Experience Manager Assets] 는 다양한 파일 형식을 지원하며 각 기능은 다양한 MIME 유형에 대해 다양한 지원을 제공합니다. 통합하려면 [!DNL Assets] 다른 표준 준수 디지털 에셋 관리(DAM) 솔루션 및 데스크탑 소프트웨어와 함께 Adobe [!DNL Extensible Metadata Platform] (XMP).

범례를 사용하여 지원 수준을 이해할 수 있습니다.

| 지원 수준 | 설명 |
| :-----------: | ------------------------------ |
| ✓ | 지원됨 |
| &#42; | 추가 기능 지원 |
| − | 해당되지 않음 |

## 에서 지원되는 래스터 이미지 형식 [!DNL Experience Manager] {#supported-raster-image-formats}

에서 지원되는 래스터 이미지 형식 [!DNL Assets] 은(는)

| 형식 | 스토리지 | 메타데이터 관리 | 메타데이터 추출 | 썸네일 생성 | 편집 | 메타데이터 원본에 쓰기 | Insights |
| ------------ | :------: | :-----------------: | :-----------------: | :------------------: | :------: | :----------------: | :------: |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| PNM | ✓ | ✓ | − | − | − | − | ✓ |
| PGM | ✓ | ✓ | − | − | − | − | ✓ |
| PBM | ✓ | ✓ | − | − | − | − | ✓ |
| PPM | ✓ | ✓ | − | − | − | − | ✓ |
| PSD ‡ | ✓ | ✓ | ✓ | ✓ | − | − | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | − | ✓ | − |
| PICT | − | − | − | − | − | − | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ | − | − | − |

‡ 병합된 이미지가 PSD 파일에서 추출됩니다. Adobe Photoshop에서 생성되고 PSD 파일에 포함된 이미지입니다. 설정에 따라 병합된 이미지가 실제 이미지가 될 수도 있고 그렇지 않을 수도 있습니다.

위의 정보 외에 다음 사항을 고려하십시오.

* EPS 파일에 대한 지원은 래스터 이미지에만 적용됩니다. 예를 들어 EPS 벡터 이미지에 대한 썸네일 생성은 기본적으로 지원되지 않습니다. 지원을 추가하려면 [imageMagick 구성](best-practices-for-imagemagick.md). 타사 도구를 통합하여 추가 기능을 활성화하려면 다음을 참조하십시오 [명령줄 기반 미디어 핸들러](media-handlers.md#command-line-based-media-handler).

* 메타데이터 원본에 쓰기 기능은 PSB 파일 형식이에 추가될 때 작동합니다. `NComm` 핸들러입니다.

* EPS 파일의 경우, 메타데이터 원본에 쓰기 기능은 PostScript Document Structuring Convention(PS-Adobe) 버전 3.0 이상에서 지원됩니다.

## 지원되는 3D 형식 {#support-3d-formats}

다음 3D 형식 목록이 지원됩니다.

참조: [Dynamic Media에서 3D 자산 작업](/help/assets/assets-3d.md)

| 형식 | 스토리지 | 버전 관리 | 워크플로 | 게시 | 액세스 제어 | 썸네일 미리보기 | 3D 미리 보기 | Dynamic Media 게재 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | | ✓ | ✓ | − | − |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | | ✓ | − | ✓ | − |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | − | − | ✓ |

## 지원되는 PDF 래스터라이저 라이브러리 {#supported-pdf-rasterizer-library}

Adobe PDF 래스터라이저 라이브러리는 고품질 썸네일을 생성하고 대용량 및 콘텐츠 집약형 미리 보기를 생성합니다 [!DNL Adobe Illustrator] 및 PDF 파일을 내보낼 수 있습니다. Adobe은 다음에 대해 PDF 래스터라이저 라이브러리를 사용할 것을 권장합니다.

* 처리할 리소스가 많은 콘텐츠 중심의 AI/PDF 파일.
* 기본적으로 썸네일이 생성되지 않는 AI/PDF 파일.
* PMS(Pantone Matching System) 색상이 있는 AI 파일.

다음을 참조하십시오 [PDF 래스터라이저 사용](aem-pdf-rasterizer.md).

## 지원되는 이미지 코드 변환 라이브러리 {#supported-image-transcoding-library}

Adobe 이미징 코드 변환 라이브러리는 인코딩, 코드 변환, 리샘플링 및 크기 조정과 같은 핵심 이미지 처리 기능을 수행하는 이미지 처리 솔루션입니다.

이미징 코드 변환 라이브러리는 JPG/JPEG, PNG(8비트 및 16비트), GIF, BMP, TIFF/압축 TIFF(32비트 TIFF 파일 및 PTIFF 파일 제외), ICO 및 ICN MIME 유형을 지원합니다.

다음을 참조하십시오 [이미징 코드 변환 라이브러리](imaging-transcoding-library.md).

## Camera Raw 지원 {#supported-camera-raw}

다음 [!DNL Adobe Camera Raw] 라이브러리 사용 [!DNL Assets] 원시 이미지를 수집합니다. 다음을 참조하십시오 [Camera Raw 지원](camera-raw.md).

## 지원됨 [!DNL Assets] 문서 형식 {#supported-document-formats}

자산 관리 기능에 대해 지원되는 문서 형식은 다음과 같습니다.

| 형식 | 스토리지 | [메타데이터 관리](metadata.md) | 전체 텍스트<br> 추출 | [메타데이터 추출](metadata.md) | 축소판<br> 생성 | [하위 자산 추출](managing-linked-subassets.md) | [메타데이터 원본에 쓰기](xmp-writeback.md) | [연결된 자산](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | − |
| DOC | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| ODT | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| RTF | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| TXT | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| XLS | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| ODS | ✓ | ✓ | ✓ | − | − | − | − | − |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| ODP | ✓ | ✓ | ✓ | − | − | − | − | − |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | − |
| PS | ✓ | ✓ | − | − | − | − | − | − |
| QXP | ✓ | ✓ | − | − | − | − | − | − |
| EPUB | ✓ | ✓ | − | ✓ | ✓ | − | − | − |

## 지원되는 멀티미디어 형식 {#supported-multimedia-formats}

| | 스토리지 | 메타데이터 관리 | 메타데이터 추출 | 썸네일 생성 | FFmpeg 코드 변환 |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ | − | − | &#42; |
| MIDI | ✓ | ✓ | − | − | &#42; |
| 3GP | ✓ | ✓ | − | − | &#42; |
| MP3 | ✓ | ✓ | ✓ | − | &#42; |
| 마일 | ✓ | ✓ | − | − | &#42; |
| OGA | ✓ | ✓ | − | − | &#42; |
| OGG | ✓ | ✓ | − | − | &#42; |
| RA | ✓ | ✓ | − | − | &#42; |
| WAV | ✓ | ✓ | − | − | &#42; |
| WMA | ✓ | ✓ | − | − | &#42; |
| DVI | ✓ | ✓ | − | &#42; | &#42; |
| FLV | ✓ | ✓ | − | &#42; | &#42; |
| M4V | ✓ | ✓ | − | &#42; | &#42; |
| MPEG | ✓ | ✓ | − | &#42; | &#42; |
| OGV | ✓ | ✓ | − | &#42; | &#42; |
| MOV | ✓ | ✓ | − | &#42; | &#42; |
| WMV | ✓ | ✓ | − | &#42; | &#42; |
| SWF | ✓ | ✓ | − | − | − |

## 지원되는 아카이브 형식 {#supported-archive-formats}

다음 표에서는 지원되는 아카이브 형식 및 일반 DAM 워크플로의 적용 가능성에 대해 설명합니다.

| 형식 | 스토리지 | 버전 관리 | 워크플로 | 게시 | 액세스 제어 | Dynamic Media 게재 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## 기타 지원되는 형식 {#other-supported-formats}

몇 가지 특정 파일 형식에 대한 일반적인 DAM 기능의 적용 가능성은 아래에 설명되어 있습니다.

| 형식 | 스토리지 | 버전 관리 | 워크플로 | 게시 | 액세스 제어 | Dynamic Media 게재 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript(자체 게재 도메인으로 구성된 경우) | − | − | − | − | − | ✓ |

>[!NOTE]
>
>JavaScript 파일을 업로드하고 배포하는 것은 안전하거나 안전하지 않을 수 있습니다. 필요한 경우 오버레이를 사용하여 사용자가 JS 파일을 업로드하지 못하도록 할 수 있습니다.

## 지원되는 MIME 유형 {#supported-mime-types}

기본적으로, [!DNL Experience Manager] 는 파일 확장명을 사용하여 파일 유형을 검색합니다. [!DNL Experience Manager] 는 파일의 내용에서 이를 감지할 수 있습니다. 후자의 경우 를 선택합니다. [!UICONTROL 컨텐츠에서 MIME 감지] 의 옵션 [!UICONTROL 일별 CQ DAM Mime 유형 서비스] 다음에서 [!DNL Experience Manager] 웹 콘솔.

지원되는 MIME 유형 목록은 다음 CRXDE Lite에서 사용할 수 있습니다. `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`.

| 파일 확장명 | MIME 유형/인터넷 미디어 유형 | 기본 jobParam 값 | 허용된 jobParam 값 |
|---|---|---|---|
| 이미지 | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | 기본 jobParam은 모든 이미지 MIME 유형 자산에 적용됩니다.<ul><li>[녹아웃 배경 옵션](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-knockout-background-options.html)</li><li>[manualCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-manual-crop-options.html)</li><li>[자동 색상 자르기 옵션](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-color-crop-options.html)</li><li>[자동 투명 자르기 옵션](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-transparent-crop-options.html)</li><li>[colorManagementOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-color-management-options.html)</li><li>[autoSetCreateOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-set-creation-options.html)</li><li>[emailSettings](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/sting-constants/r-email-settings.html)</li><li>[xmpKeywords](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-xmp-keywords.html)</li><li>[unsharpMaskOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-unsharp-mask-options.html)</li></ul> |
| 3G2 | video/3gpp2 | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| 3GP | video/3gpp | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| AAC | audio/x-aac | | |
| AFM | application/x-font-type1 | | |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScript 옵션](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li> [illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html)</li></ul> |
| AIFF | audio/x-aiff | | |
| AVI | video/x-msvideo | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| BMP | image/bmp | | |
| CSS | text/css | | |
| DOC | application/msword | | |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li></ul> | | |
| F4V | video/x-f4v | | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash | | |
| FLV | video/x-flv | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| FPX | image/vnd.fpx | | |
| GIF | image/gif | | |
| ICC | application/vnd.iccprofile | | |
| ICM | application/vnd.iccprofile | | |
| INDD | application/x-indesign | | |
| JPEG | image/jpeg | | |
| JPG | image/jpeg | | |
| M2V | video/mpeg | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| M4V | video/x-m4v | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| MOV | video/quicktime | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| MP3 | audio/mpeg | | |
| MP4 | video/mp4 | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| MPEG | video/mpeg | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| 마일 | video/mpeg | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| MTS | model/vnd.mts | | |
| OGV | video/ogg | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| OTF | application/x-font-otf | | |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-pdf-options.html) |
| PFB | application/x-font-type1 | | |
| PFM | application/x-font-type1 | | |
| PICT | image/x-pict | | |
| PNG | image/png | | |
| PPT | application/vnd.ms-powerpoint | | |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScript 옵션](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li>[illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options.html)</li><li>[photoshopLayerOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-layer-options.html)</li></ul> |
| RTF | application/rtf | | |
| SVG | image/svg+xml | | |
| SWF | application/x-shockwave-flash | | |
| TAR | application/x-tar | | |
| TIF / TIFF | image/tiff | | |
| TTC | application/x-font-ttf | | |
| TTF | application/x-font-ttf | | |
| VOB | 비디오/dvd | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| VTT | text/vtt | | |
| WAV | audio/x-wav | | |
| WEBM | video/webm | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| WMA | audio/x-ms-wma | | |
| WMV | video/x-ms-wmv | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| XLS | application/vnd.ms-excel | | |
| ZIP | application/zip | | |

## Dynamic Media - 코드 변환에 지원되는 입력 비디오 형식 {#supported-input-video-formats-for-dynamic-media-transcoding}

| 비디오 파일 확장명 | 컨테이너 | 권장 비디오 코덱 | 지원되지 않는 비디오 코덱 |
|---|---|---|---|
| AVI | A/V 인터리브 | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3(IV30), MJPEG, Microsoft® 비디오 1(MS-CRAM) |
| FLV, F4V | Adobe Flash | H264/AVC, Flix VP6, H263, Sorenson | SWF(벡터 애니메이션 파일) |
| M4V | Apple iTunes | H264/AVC | − |
| MKV | 마트로스카 | H264/AVC | − |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 &amp; HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, Apple 애니메이션 |
| MP4 | - | H264/AVC(모든 프로필) | − |
| MPG, VOB, M2V, MP2 | - | - | − |
| MXF ‡ | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro | − |
| OGV, OGG | Ogg | Theora, VP3, Dirac | − |
| WebM | WebM | Google V8 | − |
| WMV | 윈도 미디어 | WMV3(v9), WMV2(v8), WMV1(v7), GoToMeeting(G2M2, G2M3, G2M4) | Microsoft® 화면(MSS2), Microsoft® 사진 스토리(WVP2) |

‡ 이 비디오 형식은 아직 Dynamic Media의 대화형 비디오와 함께 사용하거나 Experience Manager Assets의 주석과 함께 사용할 수 없습니다.

## Dynamic Media - 지원되는 문서 형식 {#supported-document-formats-dynamic-media}

| 형식 | 업로드<br> (입력 형식) | 만들기<br> 이미지<br> 사전 설정<br> (출력 형식) | 미리 보기<br> 동적<br> 렌디션 | 제공<br> 동적<br> 렌디션 | 다운로드<br> 동적<br> 렌디션 |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | − | − | − | − |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | − | − | − | − |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) (아래 참고 참조) | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>보안 PDF의 경우 업로드만 지원됩니다.

위의 기능 외에 다음 사항을 고려하십시오.

* Dynamic Media을 사용하여 PDF 파일에 대한 동적 변환을 생성하려면 다음을 참조하십시오. [Adobe Illustrator(AI), Postscript(EPS) 및 PDF 파일 형식](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Dynamic Media을 사용하여 AI 파일에 대한 동적 변환을 미리 보고 생성하려면 다음을 참조하십시오. [Adobe Illustrator(AI), Postscript(EPS) 및 PDF 파일 형식](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Dynamic Media을 사용하여 INDD 파일에 대한 동적 변환을 생성하려면 다음을 참조하십시오. [InDesign(INDD) 파일 형식](../assets/managing-image-presets.md#indesign-indd-file-format).

## Dynamic Media - 지원되는 래스터 이미지 형식 {#supported-raster-image-formats-dynamic-media}

| 형식 | 업로드 (입력 형식) | 이미지 사전 설정 만들기(출력 형식) | 동적 렌디션 미리 보기 | 동적 렌디션 전달 | 동적 렌디션 다운로드 | 이 형식을 지원하는 형식 설정 |
|---|:---:|:---:|:---:|:---:|:---:| --- |
| AVIF | − | − | − | ✓ | − | − |
| BMP | ✓ | − | − | − | − | [이미지](/help/assets/image-sets.md), [혼합 미디어](/help/assets/mixed-media-sets.md), 및 [회전](/help/assets/spin-sets.md) |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| HEIC | − | − | − | ✓ | − | − |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [이미지](/help/assets/image-sets.md), [혼합 미디어](/help/assets/mixed-media-sets.md), 및 [회전](/help/assets/spin-sets.md) |
| PICT | ✓ | − | − | − | − | − |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [이미지](/help/assets/image-sets.md), [혼합 미디어](/help/assets/mixed-media-sets.md), 및 [회전](/help/assets/spin-sets.md) |
| PSD ‡ | ✓ | − | − | − | − | − |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [이미지](/help/assets/image-sets.md), [혼합 미디어](/help/assets/mixed-media-sets.md), 및 [회전](/help/assets/spin-sets.md) |
| WEBP | − | − | − | ✓ | − | − |
<!-- AVIF, HEIC, and WebP added to table above on March 4, 2024 based on CQDOC-21294 -->

‡ 병합된 이미지가 PSD 파일에서 추출됩니다. Adobe Photoshop에서 생성되고 PSD 파일에 포함된 이미지입니다. 설정에 따라 병합된 이미지가 실제 이미지가 될 수도 있고 그렇지 않을 수도 있습니다.

* EPS 파일에 대한 지원은 래스터 이미지에만 적용됩니다. 예를 들어 EPS 벡터 이미지에 대한 썸네일 생성은 기본적으로 지원되지 않습니다. 지원을 추가하려면 [imageMagick 구성](best-practices-for-imagemagick.md). 타사 도구를 통합하여 추가 기능을 활성화하려면 다음을 참조하십시오 [명령줄 기반 미디어 핸들러](media-handlers.md#command-line-based-media-handler).

* 사용 [!DNL Dynamic Media] EPS 파일에 대한 동적 변환을 미리 보고 생성하려면 다음을 참조하십시오. [Adobe Illustrator(AI), Postscript(EPS) 및 PDF 파일 형식](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* EPS 파일의 경우, 메타데이터 원본에 쓰기 기능은 PostScript Document Structuring Convention(PS-Adobe) 버전 3.0 이상에서 지원됩니다.

## Dynamic Media - 지원되지 않는 래스터 이미지 형식 {#unsupported-image-formats-dynamic-media}

다음 목록은 다음과 같은 래스터 이미지 파일 형식의 하위 유형을 설명합니다. *아님* Dynamic Media에서 지원됩니다.

참조: [Dynamic Media에서 지원되지 않는 파일 형식 감지](https://helpx.adobe.com/experience-manager/kb/detect-unsupported-assets-for-dynamic-media.html) 기술 자료 문서입니다.

* IDAT 청크 크기가 100MB보다 큰 PNG 파일입니다.
* PSB 파일
* CMYK, RGB, 회색 음영 또는 비트맵 이외의 색상 공간이 있는 PSD 파일은 지원되지 않습니다. DuoTone, Lab 및 Indexed 색상 공간은 지원되지 않습니다.
* 비트 깊이가 16보다 큰 PSD 파일입니다.
* 부동 소수점 데이터가 있는 TIFF 파일입니다.
* Lab 색상 공간이 있는 TIFF 파일입니다.

<!-- Topic commented out for now as of March 31, 2020. The topic may still need adjustment so it can be published live, or it may be moved into a KB article instead. Just waiting on feedback in CQDOC-15657. - Rick
## Unsupported raster image formats in Dynamic Media (#unsupported-image-formats-dynamic-media)

The following table describes the sub-types of raster image formats that are *not* supported in Dynamic Media. The table also describes suggested methods you can use to detect such files.

| Format | What is unsupported? | Suggested detection method |
|---|---|---|
| JPEG  | Files where the initial three bytes is incorrect. | To identify a JPEG file, its initial three bytes must be `ff d8 ff`. If they are anything else, then it is not classified as a JPEG.<br>&bull; There is no software tool that can help with this issue.<br>&bull; A small C++/java program which reads the initial three bytes of a file should be able to detect these types of files.<br>&bull; It may be better to track the source of such files and look at the tool generating the file. |
| PNG |  Files that have an IDAT chunk size greater than 100 MB. | You can detect this issue using [libpng](https://www.libpng.org/pub/png/libpng.html) in C++. |
| PSB |  | Use exiftool if the file type is PSB.<br>Example in an ExifTool log:<br>1. File type: `PSB` |
| PSD | Files with a color space other than CMYK, RGB, Grayscale, or Bitmap are not supported.<br>DuoTone, Lab, and Indexed color spaces are not supported. | Use ExifTool if Color mode is Duotone.<br>Example in an ExifTool log:<br>1. Color mode: `Duotone` |
|  | Files with abrupt endings. | Adobe is unable to detect this condition. Also, such files cannot be opened with Adobe PhotoShop. Adobe suggests you examine the tool that was used to create such a file and troubleshoot at the source. |
|  | Files that have a bit depth greater than 16. | Use ExifTool if the bit depth is greater than 16.<br>Example in an ExifTool log:<br>1. Bit depth: `32` |
|  | File that have Lab color space. | Use exiftool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
| TIFF | Files that have floating point data. That is, a TIFF file with 32-bit depth is not supported. | Use ExifTool if the MIME type is `image/tiff` and the SampleFormat has `Float` in its value. Example in an ExifTool log:<br>1. MIME type: `image/tiff`<br>Sample format: `Float #`<br>2. MIME type: `image/tiff`<br>Sample format: `Float; Float; Float; Float` |
|  | Files that have Lab color space. | Use ExifTool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
-->

## Dynamic Media - 지원되는 3D 형식 {#supported-three-d-file-formats-in-dm}

Dynamic Media은 다음과 같은 3D 형식을 지원합니다.

참조: [Dynamic Media에서 3D 자산 작업](/help/assets/assets-3d.md).

| 3D 파일 확장명 | 파일 포맷 | MIME 유형 | 메모 |
|---|---|---|---|
| GLB | 이진 GL 전송 | model/gltf-binary | 재료 및 텍스처를 단일 자산으로 포함합니다. |
| OBJ | WaveFront 3D 개체 파일 | application/x-tgif |  |
| STL | 스테레오리소그래피 | application/vnd.ms-pki.stl |  |
| USDZ | 범용 장면 설명 Zip 아카이브 | model/vnd.usdz+zip | *수집 전용 지원으로, 보기 또는 상호 작용을 사용할 수 없습니다.* USDZ는 Safari 및 iOS 디바이스에서 기본적으로 볼 수 있는 독점 3D 포맷입니다. |

>[!MORELIKETHIS]
>
>* [MIME 유형 기반 에셋 및 Dynamic Media Classic 업로드 작업 매개 변수 지원 활성화](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).
>* [업로드 작업 매개 변수 지원에 대한 MIME 유형 기반 구성](config-dynamic.md).
