---
title: AEM Assets를 사용하여 지원되는 다양한 파일 형식을 처리하기 위한 우수 사례입니다.
description: AEM Assets를 사용하여 지원되는 다양한 파일 유형을 처리하는 우수 사례입니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 31234518537ca4a0b7ff36e8d52a3b7b1b8fe4f7

---


# 자산 파일 형식 우수 사례 {#assets-file-format-best-practices}

AEM Assets는 사용자의 다양한 파일 지원 요구 사항을 충족하기 위해 많은 독점적 및 타사 파일 형식 라이브러리를 지원합니다. 지원되는 Adobe 라이브러리에는 Adobe Camera Raw, Gibson, Adobe PDF 래스터라이저 및 Adobe InDesign Server가 있습니다. 또한 AEM Assets는 ImageMagick, TwelyMonkeys 등을 비롯한 타사 라이브러리를 지원합니다.

For the supported file formats, see [Assets supported formats](/help/assets/assets-formats.md).

>[!TIP]
>
>Adobe Managed Services(AMS)에서 Adobe Experience Manager를 사용하는 경우 대용량 PSD 또는 PSB 파일을 처리할 계획인 경우 Adobe 지원 센터에 문의하십시오. Adobe 고객 지원 센터 담당자와 협력하여 AMS 배포에 대한 이러한 모범 사례를 구현하고 Adobe의 독점 포맷에 적합한 최상의 툴과 모델을 선택할 수 있습니다. Adobe Experience Manager는 3000 x 23000픽셀이 넘는 매우 고해상도 PSB 파일을 처리하지 못할 수 있습니다.

## Adobe Camera Raw 라이브러리 {#adobe-camera-raw-library}

최적의 성능을 위해 RAW 및 DNG 파일에 Adobe Camera Raw 라이브러리를 사용하는 것이 좋습니다.

Adobe Camera Raw 라이브러리는 CMYK 색상 프로파일을 입력으로 지원합니다. 그러나 RGB 색상 공간에서 출력을 생성하고 JPEG 포맷에서만 출력을 지원합니다. 소스 파일 색상 공간(예: CMYK)은 축소판에 유지되지 않습니다.

자세한 내용은 Camera Raw [지원을](/help/assets/camera-raw.md)참조하십시오.

## Adobe PDF 래스터라이저 라이브러리 {#adobe-pdf-rasterizer-library}

최상의 결과를 얻으려면 다음 파일에 Adobe PDF 래스터라이저 라이브러리를 사용하는 것이 좋습니다.

* 컨텐츠가 많은 대용량 PDF 파일
* 축소판이 있는 AI 파일이 즉시 생성되지 않음
* 별색(PMS) 색상이 있는 AI 파일의 경우

PDF 래스터라이저를 사용하여 생성된 축소판과 미리 보기는 기본 래스터 출력과 비교하여 품질이 더 좋습니다. Adobe PDF 래스터라이저 라이브러리는 색상 공간 변환을 지원하지 않습니다. 소스 PDF 파일의 색상 공간에 관계없이 Adobe PDF 래스터라이저는 RGB 출력만 생성합니다.

## Adobe InDesign Server {#adobe-indesign-server}

Adobe에서는 Adobe InDesign Server를 사용하여 IDML 및 HTML과 같은 Adobe InDesign 전용 변환을 추출하는 것이 좋습니다. 자세한 내용은 Adobe InDesign [에서 AEM 자산을 참조로 추가를 참조하십시오](/help/assets/managing-linked-subassets.md#refai).

## Dynamic Media  {#dynamic-media}

Dynamic Media는 글로벌, 확장 및 성능 최적화 네트워크를 통해 다양한 유형의 리치 컨텐츠를 실시간으로 생성 및 전달합니다. 인터랙티브한 보기 경험을 제공하고 디지털 캠페인 관리 프로세스를 간소화합니다. 다이내믹 미디어 활성화에 대한 자세한 내용은 다이내믹 미디어 [구성을 참조하십시오](/help/assets/config-dynamic.md).

현재 Dynamic Media는 파일당 최대 20GB의 컨텐츠를 지원할 수 있습니다.

## ImageMagick 라이브러리 {#imagemagick-library}

다음 시나리오에서는 ImageMagick 라이브러리를 사용하는 것이 좋습니다.

* EPS 파일에 대한 축소판 변환을 생성하려면
* 이미지 프로필 정보를 보존하려면
* 투명도를 유지하려면
* PSD 및 PSB 파일을 처리하려면

AEM에서 ImageMagic 라이브러리를 설정하는 방법에 대해 알아보려면 ImageMagick [사용을 참조하십시오](/help/assets/media-handlers.md#an-example-using-imagemagick). 최적 사용을 보려면 ImageMagick [구성을 위한 우수 사례를 참조하십시오](/help/assets/best-practices-for-imagemagick.md).

## 이미지 트랜스코딩 라이브러리 {#image-transcoding-library}

Adobe Imaging Transcoding Library는 이미지 인코딩, 트랜스코딩, 리샘플링, 크기 조정 등 핵심 이미지 처리 기능을 수행하는 이미지 처리 솔루션입니다.

이미징 트랜스코딩 라이브러리는 다음과 같은 MIME 유형을 지원합니다.

* JPG/JPEG
* PNG(8비트 및 16비트)
* GIF
* BMP
* TIFF/Compressed TIFF(32비트 Tiff 및 PTliffs 제외).
* ICO
* ICN

자세한 내용은 이미지 [트랜스코딩 라이브러리를 참조하십시오](/help/assets/imaging-transcoding-library.md).
