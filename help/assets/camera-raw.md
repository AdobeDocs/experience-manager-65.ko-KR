---
title: '[!DNL Adobe Camera Raw] 지원.'
description: ' [!DNL Adobe Experience Manager Assets]에서  [!DNL Adobe Camera Raw] 지원을 활성화하는 방법에 대해 학습합니다.'
contentOwner: AG
role: 관리자
feature: 개발자 도구
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 3%

---


# {#camera-raw-support}을 Camera Raw 사용하여 이미지 처리

[!DNL Adobe Camera Raw] 지원을 사용하여 CR2, NEF 및 RAF와 같은 원시 파일 형식을 처리하고 JPEG 형식으로 이미지를 렌더링할 수 있습니다. 이 기능은 소프트웨어 배포에서 사용할 수 있는 [Camera Raw 패키지](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg)를 사용하여 [!DNL Adobe Experience Manager Assets]에서 지원됩니다.

>[!NOTE]
>
>이 기능은 JPEG 변환만 지원합니다. Windows 64비트, Mac OS 및 RHEL 7.x에서 지원됩니다.

[!DNL Experience Manager Assets]에서 [!DNL Camera Raw] 지원을 활성화하려면 다음 단계를 수행합니다.

1. 소프트웨어 배포에서 [Camera Raw 패키지](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg)를 다운로드합니다.
1. 액세스 `https://[aem_server]:[port]/workflow`. **[!UICONTROL DAM 자산 업데이트]** 작업 과정을 엽니다.
1. **[!UICONTROL 축소판 처리]** 단계를 엽니다.
1. **[!UICONTROL 축소판]** 탭에서 다음 구성을 제공합니다.

   * **[!UICONTROL 축소판]**:  `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL MIME 유형 건너뛰기]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. **[!UICONTROL 웹 사용 이미지]** 탭의 **[!UICONTROL 목록 건너뛰기]** 필드에서 `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`를 지정합니다.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. 사이드 패널에서 **[!UICONTROL 축소판 만들기]** 단계 아래 **[!UICONTROL Camera Raw/DNG 핸들러]** 단계를 추가합니다.
1. **[!UICONTROL Camera Raw/DNG 핸들러]** 단계에서 **[!UICONTROL 인수]** 탭에 다음 구성을 추가합니다.

   * **[!UICONTROL MIME 유형]**: `image/dng` and  `image/x-raw-(.*)`
   * **[!UICONTROL Command]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

>[!NOTE]
>
>위의 구성이 **[!UICONTROL Sample DAM Update Asset With 및 DNG Handling Step]** 구성과 동일한지 Camera Raw 확인하십시오.

이제 Camera Raw 파일을 에셋으로 가져올 수 있습니다. 패키지를 Camera Raw 설치하고 필요한 작업 과정을 구성하면 측면 창 목록에 **[!UICONTROL 이미지 조정]** 옵션이 나타납니다.

![chlimage_1-131](assets/chlimage_1-337.png)

*그림:사이드 창의 옵션.*

![chlimage_1-132](assets/chlimage_1-338.png)

*그림:이미지를 작은 크기로 편집하려면 옵션을 사용합니다.*

편집 내용을 [!DNL Camera Raw] 이미지에 저장하면 이미지에 대한 새 변환 `AdjustedPreview.jpg`이 생성됩니다. [!DNL Camera Raw]을 제외한 다른 이미지 유형의 경우 변경 내용이 모든 변환에 반영됩니다.

## 우수 사례, 알려진 문제 및 제한 사항 {#best-practices}

이 기능에는 다음과 같은 제한 사항이 있습니다.

* 이 기능은 JPEG 변환만 지원합니다. Windows 64비트, Mac OS 및 RHEL 7.x에서 지원됩니다.
* 메타데이터 원본에 쓰기는 RAW 및 DNG 형식에 대해 지원되지 않습니다.
* [!DNL Camera Raw] 라이브러리에는 한 번에 처리할 수 있는 전체 픽셀에 대한 제한이 있습니다. 현재 파일 긴 쪽에서는 최대 65,000픽셀 또는 어떤 기준이든 먼저 발생할 수 있는 512MP를 처리할 수 있습니다.
