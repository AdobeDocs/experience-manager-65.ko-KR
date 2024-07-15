---
title: 지원되는 파일 형식을 처리하는 우수 사례
description: ' [!DNL Experience Manager Assets]을(를) 사용하여 지원되는 다양한 파일 형식을 처리하는 우수 사례입니다.'
contentOwner: AG
role: Admin
feature: Asset Management,Developer Tools
exl-id: da080f12-4cf7-4c26-901b-cd40d9c00bcb
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# Assets 파일 형식 우수 사례 {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets]은(는) 사용자의 다양한 파일 지원 요구 사항을 충족하기 위해 많은 독점 및 타사 파일 형식 라이브러리를 지원합니다. 지원되는 Adobe 라이브러리에는 [!DNL Adobe Camera Raw], Gibson, Adobe PDF Rasterizer 및 [!DNL Adobe InDesign Server]이(가) 있습니다. 또한 [!DNL Experience Manager Assets]은(는) [!DNL ImageMagick], [!DNL TwelveMonkeys] 등을 비롯한 서드파티 라이브러리를 지원합니다.

지원되는 파일 형식은 [Assets 지원 형식](/help/assets/assets-formats.md)을 참조하십시오.

>[!TIP]
>
>Adobe Managed Services(AMS)에서 [!DNL Experience Manager]을(를) 사용하는 경우 많은 대용량 PSD 또는 PSB 파일을 처리할 계획이면 Adobe 고객 지원 센터에 문의하십시오. Adobe 고객 지원 담당자와 협력하여 AMS 배포에 이러한 모범 사례를 구현하고 Adobe의 고유 형식에 가장 적합한 도구와 모델을 선택하십시오. [!DNL Experience Manager]은(는) 30000 x 23000 픽셀보다 큰 고해상도 PSB 파일을 처리하지 못할 수 있습니다.

## [!DNL Adobe Camera Raw] 라이브러리 {#adobe-camera-raw-library}

Adobe 최적의 성능을 위해 RAW 및 DNG 파일에 [!DNL Adobe Camera Raw] 라이브러리를 사용하는 것이 좋습니다.

[!DNL Adobe Camera Raw] 라이브러리가 CMYK 색상 프로필을 입력으로 지원합니다. 그러나 RGB 색상 공간에서 출력을 생성하고 JPEG 형식으로만 출력을 지원합니다. 썸네일의 소스 파일 색상 공간(예: CMYK)은 유지하지 않습니다.

Camera Raw 자세한 내용은 [지원](/help/assets/camera-raw.md)을 참조하십시오.

## Adobe PDF 래스터라이저 라이브러리 {#adobe-pdf-rasterizer-library}

Adobe 최상의 결과를 얻으려면 다음 파일에 Adobe PDF 래스터라이저 라이브러리를 사용하는 것이 좋습니다.

* 무겁고 컨텐츠 집약적인 PDF 파일
* 썸네일이 포함된 AI 파일이 즉시 생성되지 않음
* 별색(PMS) 색상이 있는 AI 파일의 경우

[PDF 래스터라이저]를 사용하여 생성된 축소판 및 미리 보기는 기본 래스터 출력에 비해 품질이 향상됩니다. Adobe PDF 래스터라이저 라이브러리는 색상 공간 변환을 지원하지 않습니다. Adobe PDF 래스터라이저는 소스 PDF 파일의 색상 공간에 관계없이 RGB 출력만 생성합니다.

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe은 [!DNL Adobe InDesign Server]을(를) 사용하여 IDML 및 HTML과 같은 [!DNL Adobe InDesign]별 변환을 추출할 것을 권장합니다. 자세한 내용은 [Adobe InDesign에서 참조로 Experience Manager 에셋 추가](/help/assets/managing-linked-subassets.md#refai)를 참조하십시오.

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media]은(는) 글로벌, 확장 가능 및 성능 최적화 네트워크를 통해 실시간으로 다양한 유형의 풍부한 콘텐츠를 생성하고 전달합니다. 대화형 보기 경험을 제공하고 디지털 캠페인 관리 프로세스를 간소화합니다. [!DNL Dynamic Media] 사용에 대한 자세한 내용은 [Dynamic Media 구성](/help/assets/config-dynamic.md)을 참조하십시오.

현재 [!DNL Dynamic Media]은(는) 파일당 최대 15GB의 콘텐츠를 지원할 수 있습니다.

## ImageMagick 라이브러리 {#imagemagick-library}

Adobe은 다음 시나리오에서 ImageMagick 라이브러리를 사용할 것을 권장합니다.

* EPS 파일에 대한 썸네일 변환을 생성하려면 다음을 수행합니다.
* 이미지 프로필 정보를 유지합니다.
* 투명도를 유지합니다.
* PSD 및 PSB 파일을 처리합니다.

[!DNL Experience Manager]에서 [!DNL ImageMagick] 라이브러리를 설정하는 방법은 [ImageMagick 사용](/help/assets/media-handlers.md#an-example-using-imagemagick)을 참조하십시오. 최적의 사용을 위해 [ImageMagick 구성을 위한 모범 사례](/help/assets/best-practices-for-imagemagick.md)를 참조하세요.

## 이미지 코드 변환 라이브러리 {#image-transcoding-library}

Adobe 이미징 코드 변환 라이브러리는 이미지 인코딩, 코드 변환, 리샘플링, 크기 조정 등의 핵심 이미지 처리 기능을 수행하는 이미지 처리 솔루션입니다.

이미징 코드 변환 라이브러리는 다음 MIME 유형을 지원합니다.

* JPG/JPEG
* PNG(8비트 및 16비트)
* GIF
* BMP
* TIFF/압축 TIFF(32비트 Tiff 및 PTiff 제외).
* ICO
* ICN

자세한 내용은 [이미징 코드 변환 라이브러리](/help/assets/imaging-transcoding-library.md)를 참조하십시오.
