---
title: PDF 래스터라이저 기능을 사용하여 표현물을 생성합니다
description: Adobe PDF Rasterizer 라이브러리를 사용하여 고품질 축소판 및 렌디션을 생성합니다.
contentOwner: AG
role: Developer, Admin
feature: Developer Tools,Renditions
exl-id: 6f365d6b-3972-4885-8766-5889e24289f1
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# PDF 래스터라이저 사용 {#using-pdf-rasterizer}

컨텐츠가 많은 대용량 PDF 또는 AI 파일을 [!DNL Adobe Experience Manager Assets]인 경우 기본 라이브러리가 정확한 출력을 생성하지 못할 수 있습니다. Adobe의 PDF 래스터라이저 라이브러리는 기본 라이브러리의 출력과 비교할 때 보다 안정적이고 정확한 출력을 생성할 수 있습니다. Adobe은 다음 시나리오에 PDF 래스터라이저 라이브러리를 사용하는 것이 좋습니다.

Adobe은 다음 경우 PDF 래스터라이저 라이브러리를 사용하는 것이 좋습니다.

* 컨텐츠가 많은 대용량 AI 파일 또는 PDF 파일.
* 기본적으로 생성되지 않는 축소판이 있는 AI 파일 및 PDF 파일.
* PMS(Pantone Matching System) 색상이 있는 AI 파일입니다.

PDF 래스터라이저 기능을 사용하여 생성된 미리 보기 및 미리 보기는 기본 출력보다 품질이 향상되므로 여러 장치에서 일관된 보기 환경을 제공합니다. Adobe PDF Rasterizer 라이브러리는 색상 공간 변환을 지원하지 않습니다. 소스 파일의 색상 공간에 관계없이 항상 RGB으로 출력됩니다.

1. PDF 래스터라이저 패키지를 [!DNL Adobe Experience Manager] 배포 위치 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-pdf-rasterizer-pkg-4.4.zip).

   >[!NOTE]
   >
   >PDF 래스터라이저 라이브러리는 Windows 및 Linux에서만 사용할 수 있습니다.

1. 액세스 권한 [!DNL Assets] 워크플로우 콘솔 `https://[aem_server]:[port]/workflow`. 열기 [!UICONTROL DAM 자산 업데이트] 워크플로우.

1. 기본 방법을 사용하여 PDF 파일 및 AI 파일에 대한 축소판 및 웹 렌디션이 생성되지 않도록 하려면 다음 단계를 수행합니다.

   * 를 엽니다. **[!UICONTROL 프로세스 축소판]** 단계 및 추가 `application/pdf` 또는 `application/postscript` 에서 **[!UICONTROL Mime 유형 건너뛰기]** 아래의 필드 **[!UICONTROL 축소판 그림]** 필요한 경우 탭합니다.

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * 에서 **[!UICONTROL 웹 사용 이미지]** 탭, 추가 `application/pdf` 또는 `application/postscript` 아래에 **[!UICONTROL 목록 건너뛰기]** 요구 사항에 따라 다릅니다.

   ![이미지 형식에 대한 축소판 처리를 건너뛰도록 구성](assets/web_enabled_imageskiplist.png)

1. 를 엽니다. **[!UICONTROL PDF/AI 이미지 미리 보기 렌디션 래스터화]** 단계를 수행하고, 미리 보기 이미지 표현물의 기본 생성을 건너뛸 MIME 유형을 제거합니다. 예를 들어 MIME 유형을 제거합니다 `application/pdf`, `application/postscript`, 또는 `application/illustrator` 에서 **[!UICONTROL MIME 유형]** 목록.

   ![process_arguments](assets/process_arguments.png)

1. 을(를) 드래그합니다. **[!UICONTROL PDF 래스터라이저 처리기]** 사이드 패널에서 다음 위치로 이동 **[!UICONTROL 프로세스 축소판]** 단계.
1. 에 대해 다음 인수를 구성합니다 **[!UICONTROL PDF 래스터라이저 처리기]** 단계:

   * MIME 유형: `application/pdf` 또는 `application/postscript`
   * 명령: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 축소판 크기 추가: 319:319, 140:100, 48:48. 필요한 경우 사용자 정의 축소판 구성을 추가합니다.

   에 대한 명령줄 인수 `PDFRasterizer` 명령에는 다음을 포함할 수 있습니다.

   * `-d`: 텍스트, 벡터 아트워크 및 이미지를 원활하게 렌더링할 수 있는 플래그입니다. 더 나은 품질의 이미지를 만듭니다. 그러나 이 매개 변수를 포함하면 명령이 느리게 실행되고 이미지 크기가 증가합니다.

   * `-s`: 최대 이미지 차원(높이 또는 너비)입니다. 각 페이지의 DPI로 변환됩니다. 페이지의 크기가 다른 경우 각 페이지의 크기가 서로 다른 양만큼 커질 수 있습니다. 기본값은 실제 페이지 크기입니다.

   * `-t`: 출력 이미지 유형입니다. 유효한 유형은 JPEG, PNG, GIF 및 BMP입니다. 기본값은 JPEG입니다.

   * `-i`: 입력 PDF 경로. 필수 매개 변수입니다.

   * `-h`: 도움말


1. 중간 변환을 삭제하려면 **[!UICONTROL 생성된 표현물 삭제]**.
1. Laterizer에서 웹 변환을 생성하도록 하려면 다음을 선택합니다 **[!UICONTROL 웹 표현물 생성]**.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. 에서 설정을 지정합니다. **[!UICONTROL 웹 사용 이미지]** 탭.

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. 워크플로우를 저장합니다.
1. PDF 래스터라이저 기능을 사용하여 PDF 라이브러리로 PDF 페이지를 처리하려면 **[!UICONTROL DAM 프로세스 하위 자산]** 모델 [!UICONTROL 워크플로우] 콘솔.
1. 사이드 패널에서 PDF 래스터라이저 처리기 단계를 **[!UICONTROL 웹 지원 이미지 표현물 만들기]** 단계.
1. 에 대해 다음 인수를 구성합니다 **[!UICONTROL PDF 래스터라이저 처리기]** 단계:

   * MIME 유형: `application/pdf` 또는 `application/postscript`
   * 명령: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 축소판 크기 추가: `319:319`, `140:100`, `48:48`. 필요에 따라 사용자 정의 축소판 구성을 추가합니다.

   에 대한 명령줄 인수 `PDFRasterizer` 명령에는 다음을 포함할 수 있습니다.

   * `-d`: 텍스트, 벡터 아트워크 및 이미지를 원활하게 렌더링할 수 있는 플래그입니다. 더 나은 품질의 이미지를 만듭니다. 그러나 이 매개 변수를 포함하면 명령이 느리게 실행되고 이미지 크기가 증가합니다.

   * `-s`: 최대 이미지 차원(높이 또는 너비)입니다. 각 페이지의 DPI로 변환됩니다. 페이지의 크기가 다른 경우 각 페이지의 크기가 서로 다른 양만큼 커질 수 있습니다. 기본값은 실제 페이지 크기입니다.

   * `-t`: 출력 이미지 유형입니다. 유효한 유형은 JPEG, PNG, GIF 및 BMP입니다. 기본값은 JPEG입니다.

   * `-i`: 입력 PDF 경로. 필수 매개 변수입니다.

   * `-h`: 도움말


1. 중간 변환을 삭제하려면 **[!UICONTROL 생성된 표현물 삭제]**.
1. Laterizer에서 웹 변환을 생성하도록 하려면 다음을 선택합니다 **[!UICONTROL 웹 표현물 생성]**.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. 에서 설정을 지정합니다. **[!UICONTROL 웹 사용 이미지]** 탭.

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. 워크플로우를 저장합니다.
1. PDF 파일 또는 AI 파일을 [!DNL Experience Manager Assets]. PDF Rasterizer는 파일의 축소판과 웹 변환을 생성합니다.
