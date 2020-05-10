---
title: PDF 래스터라이저를 사용하여 PDF 파일의 변환을 생성할 수 있습니다.
description: 의 Adobe PDF 래스터라이저 라이브러리를 사용하여 고품질 축소판과 변환을 생성할 수 [!DNL Adobe Experience Manager]있습니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5f3af7041029a1b4dd1cbb4c65bd488b62c7e10c
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---


# Use PDF Rasterizer {#using-pdf-rasterizer}

컨텐츠 중심 PDF 또는 AI 파일을 업로드하는 경우 기본 변환 [!DNL Adobe Experience Manager Assets]으로 인해 정확한 출력이 생성되지 않을 수 있습니다. Adobe의 PDF 래스터라이저 라이브러리를 사용하면 기본 라이브러리의 출력 결과와 비교하여 보다 안정적이고 정확한 출력물을 생성할 수 있습니다. Adobe에서는 다음 시나리오에 PDF 래스터라이저 라이브러리를 사용하는 것이 좋습니다.

* 컨텐츠가 많은 AI 파일 또는 PDF 파일
* 기본적으로 생성되지 않는 축소판이 포함된 AI 파일 및 PDF 파일
* PMS(Pantone Matching System) 색상이 있는 AI 파일

PDF 래스터라이저를 사용하여 생성된 축소판 및 미리 보기는 기본 출력 품질과 비교하여 더 우수하므로 여러 디바이스에서 일관된 보기 경험을 제공할 수 있습니다. Adobe PDF 래스터라이저 라이브러리는 색상 공간 변환을 지원하지 않습니다. 소스 파일의 색상 공간에 관계없이 항상 RGB로 출력합니다.

1. 패키지 공유에서 배포 시 PDF 래스터라이저 패키지 [!DNL Experience Manager] 를 [설치합니다](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/product/assets/aem-assets-pdf-rasterizer-pkg).

   >[!NOTE]
   >
   >PDF 래스터라이저 라이브러리는 Windows 및 Linux에서만 사용할 수 있습니다.

1. 의 워크플로우 [!DNL Assets] 콘솔에 액세스합니다 `https://[aem_server]:[port]/workflow`. DAM 자산 [!UICONTROL 업데이트 워크플로우를] 엽니다.

1. 기본 방법을 사용하여 PDF 파일 및 AI 파일에 대한 축소판 및 웹 변환 생성을 방지하려면 다음 단계를 수행합니다.

   * [ **[!UICONTROL 프로세스 축소판]** ] `application/pdf` 단계를 `application/postscript` 열고 필요한 경우 [축소판 ** 탭 아래의 [MIME 형식]** 건너뛰기 **]** 필드에서 추가 또는추가합니다.
   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * 웹 **[!UICONTROL 지원 이미지]** 탭에서 `application/pdf` 사용자 요구 사항에 따라 목록 `application/postscript` 에 **[!UICONTROL 추가하거나]** 건너뜁니다.
   ![이미지 형식에 대한 축소판 처리를 건너뛸 구성](assets/web_enabled_imageskiplist.png)

1. PDF/ **[!UICONTROL AI 이미지 미리 보기 변환]** 래스터화 단계를 열고 미리 보기 이미지 표현물의 기본 생성을 건너뛸 MIME 유형을 제거합니다. 예를 들어 MIME 유형 `application/pdf`을 `application/postscript`제거하거나 MIME 유형 `application/illustrator` 목록에서 **[!UICONTROL MIME 유형]** 을 제거합니다.

   ![process_arguments](assets/process_arguments.png)

1. 사이드 패널에서 **[!UICONTROL PDF 래스터라이저 핸들러]** 단계를 **[!UICONTROL 프로세스 축소판]** 단계 아래로 드래그합니다.
1. PDF 래스터라이저 **[!UICONTROL 처리기 단계에 대해 다음 인수를]** 구성합니다.

   * MIME 형식: `application/pdf` or `application/postscript`
   * 명령: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * 축소판 크기 추가: 319:319, 140:100, 48:48. 필요한 경우 사용자 정의 축소판 구성을 추가합니다.
   명령에 대한 명령줄 인수에는 `PDFRasterizer` 다음을 포함할 수 있습니다.

   * `-d`: 텍스트, 벡터 아트워크 및 이미지의 매끄러운 렌더링을 가능하게 하는 플래그. 고품질의 이미지를 만들 수 있습니다. 그러나 이 매개 변수를 포함하면 명령이 느리게 실행되고 이미지 크기가 커집니다.

   * `-p`: 페이지 번호. 기본값은 모든 페이지입니다. 모든 페이지를 표시하려면 을(를) 사용하십시오 `*`.

   * `-s`: 최대 이미지 크기(높이 또는 너비). 각 페이지에 대해 DPI로 변환됩니다. 페이지 크기가 다른 경우 각 페이지의 크기가 서로 다를 수 있습니다. 기본값은 실제 페이지 크기입니다.

   * `-t`: 출력 이미지 유형입니다. 유효한 형식은 JPEG, PNG, GIF 및 BMP입니다. 기본값은 JPEG입니다.

   * `-i`: 입력 PDF의 경로 필수 매개 변수입니다.

   * `-h`: 도움말


1. 중간 변환을 삭제하려면 생성된 변환 **[!UICONTROL 삭제를 선택합니다]**.
1. PDF 래스터라이저가 웹 변환을 생성하도록 하려면 [웹 변환 **[!UICONTROL 생성]을 선택합니다]**.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. [웹 사용 이미지] **[!UICONTROL 탭에서 설정을]** 지정합니다.

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. 워크플로우를 저장합니다.
1. PDF 래스터라이저가 PDF 라이브러리를 사용하여 PDF 페이지를 처리할 수 있도록 하려면 워크플로우 콘솔에서 **[!UICONTROL DAM Process Subasset]** 모델을 엽니다.
1. 사이드 패널에서 PDF 래스터라이저 처리기 단계를 웹 지원 이미지 변환 **[!UICONTROL 만들기 단계 아래로]** 드래그합니다.
1. PDF 래스터라이저 **[!UICONTROL 처리기 단계에 대해 다음 인수를]** 구성합니다.

   * MIME 형식: `application/pdf` or `application/postscript`

   * 명령: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * 축소판 크기 추가: `319:319`, `140:100`, `48:48`. 필요에 따라 사용자 정의 축소판 구성을 추가합니다.
   명령에 대한 명령줄 인수에는 `PDFRasterizer` 다음을 포함할 수 있습니다.

   * `-d`: 텍스트, 벡터 아트워크 및 이미지의 매끄러운 렌더링을 가능하게 하는 플래그. 고품질의 이미지를 만들 수 있습니다. 그러나 이 매개 변수를 포함하면 명령이 느리게 실행되고 이미지 크기가 커집니다.

   * `-p`: 페이지 번호. 기본값은 모든 페이지입니다. `*` 는 모든 페이지를 나타냅니다.

   * `-s`: 최대 이미지 크기(높이 또는 너비). 각 페이지에 대해 DPI로 변환됩니다. 페이지 크기가 다른 경우 각 페이지의 크기가 서로 다를 수 있습니다. 기본값은 실제 페이지 크기입니다.

   * `-t`: 출력 이미지 유형입니다. 유효한 형식은 JPEG, PNG, GIF 및 BMP입니다. 기본값은 JPEG입니다.

   * `-i`: 입력 PDF의 경로 필수 매개 변수입니다.

   * `-h`: 도움말


1. 중간 변환을 삭제하려면 생성된 변환 **[!UICONTROL 삭제를 선택합니다]**.
1. PDF 래스터라이저가 웹 변환을 생성하도록 하려면 [웹 변환 **[!UICONTROL 생성]을 선택합니다]**.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. [웹 사용 이미지] **[!UICONTROL 탭에서 설정을]** 지정합니다.

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. 워크플로우를 저장합니다.
1. PDF 또는 AI 파일을 업로드합니다 [!DNL Experience Manager Assets]. PDF 래스터라이저는 파일의 축소판과 웹 변환을 생성합니다.
