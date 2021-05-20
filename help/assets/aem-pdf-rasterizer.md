---
title: PDF 래스터라이저 기능을 사용하여 표현물을 생성합니다
description: Adobe PDF Rasterizer 라이브러리를 사용하여 고품질 축소판 및 렌디션을 생성합니다.
contentOwner: AG
role: Developer, Administrator
feature: 개발자 도구,표현물
exl-id: 6f365d6b-3972-4885-8766-5889e24289f1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---

# PDF 래스터라이저 사용 {#using-pdf-rasterizer}

컨텐츠가 많은 대용량 PDF 또는 AI 파일을 [!DNL Adobe Experience Manager Assets]에 업로드하면 기본 라이브러리가 정확한 출력을 생성하지 않을 수 있습니다. Adobe의 PDF 래스터라이저 라이브러리는 기본 라이브러리의 출력과 비교할 때 보다 안정적이고 정확한 출력을 생성할 수 있습니다. Adobe은 다음 시나리오에 PDF 래스터라이저 라이브러리를 사용하는 것이 좋습니다.

Adobe은 다음과 같은 경우 PDF 래스터라이저 라이브러리를 사용하는 것이 좋습니다.

* 컨텐츠가 많은 AI 파일 또는 PDF 파일
* 기본적으로 생성되지 않는 축소판이 있는 AI 파일 및 PDF 파일.
* PMS(Pantone Matching System) 색상을 사용하는 AI 파일입니다.

PDF Rasterizer를 사용하여 생성된 축소판 및 미리 보기는 기본 출력보다 품질이 향상되므로 여러 장치에서 일관된 보기 환경을 제공합니다. Adobe PDF Rasterizer 라이브러리는 색상 공간 변환을 지원하지 않습니다. 소스 파일의 색상 공간에 관계없이 항상 RGB로 출력됩니다.

1. [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/aem-assets-pdf-rasterizer-pkg)에서 [!DNL Adobe Experience Manager] 배포에 PDF 래스터라이저 패키지를 설치합니다.

   >[!NOTE]
   >
   >PDF 래스터라이저 라이브러리는 Windows 및 Linux에서만 사용할 수 있습니다.

1. `https://[aem_server]:[port]/workflow`에서 [!DNL Assets] 워크플로우 콘솔에 액세스합니다. [!UICONTROL DAM 자산 업데이트] 워크플로우를 엽니다.

1. 기본 방법을 사용하여 PDF 파일과 AI 파일에 대한 축소판 및 웹 렌디션이 생성되지 않도록 하려면 다음 단계를 수행합니다.

   * **[!UICONTROL 축소판 처리]** 단계를 열고 **[!UICONTROL 축소판 그림]** 탭 아래의 `application/pdf` 또는 `application/postscript` 필드를 필요에 따라 추가합니다.****

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * **[!UICONTROL 웹 지원 이미지]** 탭에서 요구 사항에 따라 **[!UICONTROL 목록 건너뛰기]** 아래에 `application/pdf` 또는 `application/postscript`을 추가합니다.

   ![이미지 형식에 대한 축소판 처리를 건너뛰도록 구성](assets/web_enabled_imageskiplist.png)

1. **[!UICONTROL PDF/AI 이미지 미리 보기 표현물 래스터화]** 단계를 열고 미리 보기 이미지 표현물의 기본 생성을 건너뛸 MIME 유형을 제거합니다. 예를 들어 **[!UICONTROL MIME 유형]** 목록에서 MIME 유형 `application/pdf`, `application/postscript` 또는 `application/illustrator`을 제거합니다.

   ![process_arguments](assets/process_arguments.png)

1. **[!UICONTROL PDF 래스터라이저 처리기]** 단계를 사이드 패널에서 **[!UICONTROL 축소판 처리]** 단계 아래로 드래그합니다.
1. **[!UICONTROL PDF 래스터라이저 처리기]** 단계에 대해 다음 인수를 구성합니다.

   * MIME 유형:`application/pdf` 또는 `application/postscript`
   * 명령: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 축소판 크기 추가:319:319, 140:100, 48:48. 필요한 경우 사용자 정의 축소판 구성을 추가합니다.

   `PDFRasterizer` 명령에 대한 명령줄 인수에는 다음이 포함될 수 있습니다.

   * `-d`:텍스트, 벡터 아트워크 및 이미지를 원활하게 렌더링할 수 있는 플래그입니다. 더 나은 품질의 이미지를 만듭니다. 그러나 이 매개 변수를 포함하면 명령이 느리게 실행되고 이미지 크기가 증가합니다.

   * `-s`:최대 이미지 차원(높이 또는 너비)입니다. 각 페이지의 DPI로 변환됩니다. 페이지의 크기가 다른 경우 각 페이지의 크기가 서로 다른 양만큼 커질 수 있습니다. 기본값은 실제 페이지 크기입니다.

   * `-t`:출력 이미지 유형입니다. 유효한 유형은 JPEG, PNG, GIF 및 BMP입니다. 기본값은 JPEG입니다.

   * `-i`:입력 PDF의 경로입니다. 필수 매개 변수입니다.

   * `-h`: 도움말


1. 중간 변환을 삭제하려면 **[!UICONTROL 생성된 변환 삭제]**&#x200B;를 선택합니다.
1. PDF Rasterizer에서 웹 표현물을 생성하도록 하려면 **[!UICONTROL 웹 표현물 생성]**&#x200B;을 선택합니다.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. **[!UICONTROL 웹 지원 이미지]** 탭에서 설정을 지정합니다.

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. 워크플로우를 저장합니다.
1. PDF Rasterizer에서 PDF 라이브러리를 사용하여 PDF 페이지를 처리할 수 있도록 하려면 **[!UICONTROL DAM Process Subasset]** 모델을 [!UICONTROL Workflow] 콘솔에서 엽니다.
1. 사이드 패널에서 **[!UICONTROL 웹이 활성화된 이미지 표현물 만들기]** 단계의 PDF 래스터라이저 처리기 단계를 드래그합니다.
1. **[!UICONTROL PDF 래스터라이저 처리기]** 단계에 대해 다음 인수를 구성합니다.

   * MIME 유형:`application/pdf` 또는 `application/postscript`
   * 명령: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 축소판 크기 추가:`319:319`, `140:100`, `48:48`. 필요에 따라 사용자 정의 축소판 구성을 추가합니다.

   `PDFRasterizer` 명령에 대한 명령줄 인수에는 다음이 포함될 수 있습니다.

   * `-d`:텍스트, 벡터 아트워크 및 이미지를 원활하게 렌더링할 수 있는 플래그입니다. 더 나은 품질의 이미지를 만듭니다. 그러나 이 매개 변수를 포함하면 명령이 느리게 실행되고 이미지 크기가 증가합니다.

   * `-s`:최대 이미지 차원(높이 또는 너비)입니다. 각 페이지의 DPI로 변환됩니다. 페이지의 크기가 다른 경우 각 페이지의 크기가 서로 다른 양만큼 커질 수 있습니다. 기본값은 실제 페이지 크기입니다.

   * `-t`:출력 이미지 유형입니다. 유효한 유형은 JPEG, PNG, GIF 및 BMP입니다. 기본값은 JPEG입니다.

   * `-i`:입력 PDF의 경로입니다. 필수 매개 변수입니다.

   * `-h`: 도움말


1. 중간 변환을 삭제하려면 **[!UICONTROL 생성된 변환 삭제]**&#x200B;를 선택합니다.
1. PDF Rasterizer에서 웹 표현물을 생성하도록 하려면 **[!UICONTROL 웹 표현물 생성]**&#x200B;을 선택합니다.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. **[!UICONTROL 웹 지원 이미지]** 탭에서 설정을 지정합니다.

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. 워크플로우를 저장합니다.
1. PDF 파일 또는 AI 파일을 [!DNL Experience Manager Assets]에 업로드합니다. PDF Rasterizer는 파일의 축소판과 웹 변환을 생성합니다.
