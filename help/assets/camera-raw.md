---
title: '[!DNL Adobe Camera Raw] 지원.'
description: '[!DNL Adobe Experience Manager Assets]에서 [!DNL Adobe Camera Raw] 지원을 활성화하는 방법을 알아봅니다.'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# Camera Raw를 사용하여 이미지 처리 {#camera-raw-support}

CR2, NEF 및 RAF와 같은 Raw 파일 포맷을 처리하고 JPEG 포맷으로 이미지를 렌더링할 수 있습니다. [!DNL Adobe Camera Raw] 이 기능은 패키지 공유를 통해 [!DNL Adobe Experience Manager Assets] 사용할 수 있는 Camera Raw 패키지 [](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) 사용 시 지원됩니다.

>[!NOTE]
>
>이 기능은 JPEG 변환만 지원합니다. Windows 64비트, Mac OS 및 RHEL 7.x에서 지원됩니다.

에서 [!DNL Camera Raw] 지원을 활성화하려면 [!DNL Experience Manager Assets]다음 단계를 수행하십시오.

1. 패키지 [공유에서 Camera Raw 패키지를](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) 다운로드합니다.
1. 액세스 `https://[aem_server]:[port]/workflow`. DAM 자산 **[!UICONTROL 업데이트 워크플로우를]** 엽니다.
1. [프로세스 **[!UICONTROL 축소판] 단계를]** 엽니다.
1. [축소판] 탭에서 다음 구성을 **[!UICONTROL 제공합니다]** .

   * **[!UICONTROL 축소판]**: `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL MIME 유형 건너뛰기]**: `skip:image/dng, skip:image/x-raw-(.*)`
   ![chlimage_1-128](assets/chlimage_1-334.png)

1. 웹 **[!UICONTROL 사용 이미지]** 탭의 목록 **[!UICONTROL 건너뛰기]** 필드에서 `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`을지정합니다.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. 사이드 패널에서 축소판 **[!UICONTROL 작성]** 단계 아래에 Camera Raw/DNG 핸들러 **[!UICONTROL 단계를]** 추가합니다.
1. Camera **[!UICONTROL Raw/DNG 핸들러]** 단계에서 [인수] **[!UICONTROL 탭에 다음 구성을 추가합니다]** .

   * **[!UICONTROL MIME 유형]**: `image/dng` 및 `image/x-raw-(.*)`
   * **[!UICONTROL Command]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`
   ![chlimage_1-130](assets/chlimage_1-336.png)

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

>[!NOTE]
>
>위의 구성이 Camera RAW 및 DNG 처리 단계 **[!UICONTROL 구성을 사용하여 샘플 DAM 업데이트 자산과 동일한지 확인합니다]** .

이제 Camera Raw 파일을 AEM Assets로 가져올 수 있습니다. Camera RAW 패키지를 설치하고 필요한 작업 과정을 구성하면 **[!UICONTROL [이미지 조정]** ] 옵션이 사이드 창 목록에 나타납니다.

![chlimage_1-131](assets/chlimage_1-337.png)

*그림:사이드 창의 옵션.*

![chlimage_1-132](assets/chlimage_1-338.png)

*그림:옵션을 사용하여 이미지를 간단하게 편집할 수 있습니다.*

편집 내용을 [!DNL Camera Raw] 이미지에 저장하면 이미지에 대한 새 변환이 `AdjustedPreview.jpg` 생성됩니다. 다른 이미지 유형을 제외하고 [!DNL Camera Raw]변경 사항이 모든 변환에 반영됩니다.

## 모범 사례, 알려진 문제 및 제한 사항 {#best-practices}

기능에는 다음과 같은 제한 사항이 있습니다.

* 이 기능은 JPEG 변환만 지원합니다. Windows 64비트, Mac OS 및 RHEL 7.x에서 지원됩니다.
* RAW 및 DNG 포맷에는 메타데이터 원본에 대한 지원이 지원되지 않습니다.
* 라이브러리에는 한 번에 처리할 수 있는 총 픽셀 수에 대한 제한이 있습니다 [!DNL Camera Raw] . 현재, 파일의 긴 쪽에서 최대 65,000픽셀이나 어떤 기준이든 먼저 발견된 512MP를 처리할 수 있습니다.
