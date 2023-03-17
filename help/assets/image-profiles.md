---
title: Dynamic Media 이미지 프로필
description: 언샵 마스크, 스마트 자르기, 스마트 견본 또는 둘 다에 대한 설정이 포함된 이미지 프로필을 만든 다음 이미지 자산의 폴더에 프로필을 적용합니다.
uuid: 9049fab9-d2be-4118-8684-ce58f3c8c16a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: 4f9301db-edf8-480b-886c-b5e8fca5bf5c
feature: Image Profiles
role: User, Admin
exl-id: 67240ad0-1a7c-4e58-a518-1e36d771f1a1
source-git-commit: bbb64f44c80e96bafcd53277f6d753d84acf5189
workflow-type: tm+mt
source-wordcount: '3047'
ht-degree: 6%

---

# Dynamic Media 이미지 프로필 {#image-profiles}

이미지를 업로드할 때 폴더에 이미지 프로필을 적용하여 업로드 시 이미지를 자동으로 자릅니다.

>[!IMPORTANT]
>
>・ 스마트 자르기는 Dynamic Media - Scene7 모드에서만 사용할 수 있습니다.
・ 이미지 프로필은 PDF, 애니메이션 GIF 또는 INDD(Adobe InDesign) 파일에 적용할 수 없습니다.

## 자르기 옵션 {#crop-options}

이미지에서 스마트 자르기를 구현할 때 Adobe은 다음 모범 사례를 권장하고 다음 제한을 적용합니다.

| 제한 유형 | 우수 사례 | 제한 적용 |
| --- | --- | --- |
| 이미지당 스마트 자르기 수 | 5 | 100 |

참조 - [Dynamic Media 제한 사항](/help/assets/limitations.md).

<!-- CQDOC-16069 for paragraph directly below -->

스마트 자르기 좌표는 종횡비에 따라 다릅니다. 이미지 프로필의 다양한 스마트 자르기 설정의 경우 이미지 프로필에서 추가한 차원에 대해 종횡비가 동일하면 동일한 종횡비가 Dynamic Media으로 전송됩니다. Adobe은 동일한 자르기 영역을 사용할 것을 권장합니다. 이렇게 하면 이미지 프로필에 사용되는 다른 차원에 영향을 주지 않습니다.

생성하는 각 스마트 자르기 생성에는 추가 처리가 필요합니다. 예를 들어 5개 이상의 스마트 자르기 종횡비를 추가하면 자산 수집률이 느려질 수 있습니다. 또한 시스템에 대한 부하가 증가합니다. 폴더 수준에서 스마트 자르기를 적용할 수 있으므로 폴더에서 사용하는 것이 좋습니다 *전용* 필요한 위치

**이미지 프로필에서 스마트 자르기 정의 지침**
스마트 자르기 사용을 제어하고 자르기의 처리 시간 및 저장을 위해 다음 지침 및 팁을 권장합니다.

* 폭과 높이 값이 동일한 중복 스마트 자르기 프로필을 만들면 안 됩니다.
* 최종 사용이 아닌 자르기 차원을 기반으로 스마트 자르기에 이름을 지정합니다. 이렇게 하면 단일 차원이 여러 페이지에서 사용되는 중복 항목을 최적화할 수 있습니다.
* 모든 폴더 또는 모든 자산에 적용되는 일반적인 스마트 자르기 프로필 대신 특정 폴더 및 하위 폴더에 대한 페이지 기반/자산 유형 기반 이미지 프로필을 만듭니다.
* 하위 폴더에 적용하는 이미지 프로필은 폴더에 적용되는 이미지 프로필을 무시합니다.
* 모든 폴더 또는 모든 자산에 적용되는 일반적인 스마트 자르기 프로필 대신 특정 폴더 및 하위 폴더에 대한 페이지 기반/자산 유형 기반 이미지 프로필을 만듭니다.
* 하위 폴더에 적용하는 이미지 프로필은 폴더에 적용되는 이미지 프로필을 무시합니다.
* 이상적으로는 이미지당 10~15개의 스마트 자르기를 사용하여 화면 비율과 처리 시간을 최적화합니다.

<!--
* Image assets that are going to have a smart crop applied to them must be a minimum of 50 x 50 pixels or larger. CQDOC-20087
* An Image Profile that contains duplicate smart crop dimensions is not permitted. CQDOC-20087
* Duplicate named Image Profiles that have smart crop options set are not permitted. CQDOC-20087
* Create page-wise/asset type-wise Image Profiles for specific folders and subfolders instead of a common smart crop profile that is applied to all folders or all assets.
* An Image Profile that you apply to subfolders overrides an Image Profile that is applied to the folder.
* Ideally, have 10-15 smart crops per image to optimize for screen ratios and processing time. -->
<!-- * Avoid creating duplicate smart crop profiles that have the same width and height values. 
* Name smart crops based on crop dimensions, not on end usage. Doing so helps to optimize for duplicates where a single dimension is used on multiple pages. -->

선택할 이미지 자르기 옵션이 두 개 있습니다. 색상 및 이미지 색상 견본 만들기를 자동화하거나 대상 해상도의 자르기 컨텐츠를 보존하도록 선택할 수도 있습니다.

>[!IMPORTANT]
・ Adobe은 생성된 농작물과 견본이 브랜드와 값에 적절하고 적절한지 확인하기 위해 모든 농작물과 견본을 검토할 것을 권장합니다.
・ 스마트 자르기에서 CMYK 이미지 형식이 지원되지 않습니다.

| 옵션 | 사용 시기 | 설명 |
| --- | --- | --- |
| 픽셀 자르기 | 차원만 기준으로 이미지를 벌크 자르십시오. | 이 옵션을 사용하려면 **[!UICONTROL 픽셀 자르기]** 자르기 옵션 드롭다운 목록에서 클릭합니다.<br><br>이미지의 양쪽에서 자르려면 이미지의 모든 측면이나 각 측면에서 자를 픽셀 수를 입력합니다. 이미지가 잘리는 양은 이미지 파일의 ppi(인치당 픽셀) 설정에 따라 달라집니다.<br><br>이미지 프로필 픽셀 자르기는 다음과 같은 방식으로 렌더링됩니다.<br>・ 값은 위쪽, 아래쪽, 왼쪽 및 오른쪽입니다.<br>・ 왼쪽 위 부분이 고려됨 `0,0` 여기서 픽셀 자르기가 계산됩니다.<br>・ 자르기 시작 지점: 왼쪽은 X이고, 상단은 Y입니다<br>・ 가로 계산: 원래 이미지의 가로 픽셀 치수에서 [왼쪽]을 뺀 다음 [오른쪽]을 뺀 것입니다.<br>・ 세로 계산: 세로 픽셀 높이 - 위쪽 및 빼기 아래쪽<br><br>예를 들어 4000 x 3000 픽셀 이미지가 있다고 가정합니다. 값을 사용합니다. Top=250, Bottom=500, Left=300, Right=700.<br><br>(4000-300-700, 3000-250-500 또는 3000,2250)의 채우기 공간을 사용하여 왼쪽 상단(300,250) 자르기에서 |
| 스마트 자르기 | 시각적 초점을 기반으로 이미지를 벌크 자르십시오. | 스마트 자르기는 Adobe Sensei의 인공 지능 기능을 사용하여 일괄적으로 이미지 자르기를 신속하게 자동화합니다. 스마트 자르기는 화면 크기에 상관없이 의도한 관심 영역을 캡처하기 위해 모든 이미지의 초점을 자동으로 감지하고 자릅니다.</p> <p>스마트 자르기를 사용하려면 **[!UICONTROL 스마트 자르기]** 자르기 옵션 드롭다운 목록에서 응답형 이미지 자르기 오른쪽에 있는 기능을 활성화(켜기)합니다.</p> <p>일반적으로 크기가 큰, 중간 및 작음의 기본 중단점 크기는 대부분의 이미지가 모바일 및 태블릿 장치, 데스크톱 및 배너에 사용되는 전체 크기 범위를 다룹니다. 원하는 경우 큰, 중간 및 작은 의 기본 이름을 편집할 수 있습니다.</p> <p>중단점을 더 추가하려면 **[!UICONTROL 자르기 추가]** 자르기를 삭제하려면 [쓰레기통] 아이콘을 선택합니다. |
| 색상 및 이미지 견본 | 각 이미지에 대한 이미지 견본을 벌크로 생성합니다. | **참고**: 스마트 견본은 Dynamic Media Classic에서 지원되지 않습니다.<br><br>색상 또는 텍스처를 보여주는 제품 이미지에서 고품질 색상 견본을 자동으로 찾아 생성합니다.<br><br>[색상] 및 [이미지 견본]을 사용하려면 **[!UICONTROL 스마트 자르기]** [자르기 옵션] 드롭다운 목록에서 [색상] 및 [이미지 견본] 오른쪽에 있는 기능을 활성화(켜짐)합니다. [너비] 및 [높이] 텍스트 상자에 픽셀 값을 입력합니다.<br><br>모든 이미지 작물은 [표현물] 레일에서 사용할 수 있지만 색상 견본은 URL 복사 기능을 통해서만 사용됩니다. 사이트에서 견본을 렌더링하려면 직접 보는 구성 요소를 사용합니다. 이 규칙의 예외는 회전 배너입니다. Dynamic Media은 회전 배너에 사용된 견본에 대한 보기 구성 요소를 제공합니다.)<br><br>**이미지 색상 견본 사용**<br>&#x200B;이미지 색상 견본의 URL은 간단합니다. 예:<br><br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>여기서 `:Swatch` 이 자산 요청에 추가됩니다.<br><br>**색상 견본 사용**<br>&#x200B;색상 견본을 사용하려면 `req=userdata` 다음과 같이 요청합니다.<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>예를 들어 다음은 Dynamic Media Classic의 견본 자산입니다.<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>견본 자산의 해당 `req=userdata` URL:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br><br>다음 `req=userdata` 응답은 다음과 같습니다.<br>`SmartCropDef=Swatch SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br><br>을 요청할 수도 있습니다 `req=userdata` 다음 각 URL 예와 같이, XML 또는 JSON 형식으로 응답합니다.<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**참고:** 고유한 WCM 구성 요소를 만들어 색상 견본을 요청하고 `SmartSwatchColor` 24비트 RGB 16진수 값으로 표시되는 속성입니다.<br><br>참조 - [`userdata` 뷰어 참조 안내서에서](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata.html). |

## 언샵 마스크 {#unsharp-mask}

You use **[!UICONTROL Unsharp mask]** to fine-tune a sharpening filter effect on the final downsampled image. 효과의 강도, 효과의 반경(픽셀 단위 측정) 및 무시되는 조명의 임계값을 제어할 수 있습니다. 이 효과는 Adobe Photoshop의 옵션과 동일한 옵션을 사용합니다 *언샵 마스크* 필터.

>[!NOTE]
언샵 마스크는 50% 이상 다운샘플링된 PTIFF(피라미드형 tiff) 내의 축소된 표현물에만 적용됩니다. 즉, ptiff 내에서 가장 큰 크기의 표현물은 언샵 마스크의 영향을 받지 않지만 축소판과 같은 작은 크기의 표현물은 변경됩니다(그리고 언샵 마스크 표시).

in **[!UICONTROL 언샵 마스크]**&#x200B;에는 다음과 같은 필터링 옵션이 있습니다.

| 옵션 | 설명 |
| --- | --- |
| 양 | 가장자리 픽셀에 적용된 대비 양을 제어합니다. 기본값은 1.75입니다. 고해상도 이미지의 경우 최대 5로 늘릴 수 있습니다. 양을 필터 강도를 측정하는 방법으로 생각합니다. 범위는 0-5입니다. |
| 반경 | 선명하게 하기가 적용되는 가장자리 픽셀 주위의 픽셀 수를 결정합니다. 고대비 이미지의 경우 1~2를 입력합니다. 작은 값은 가장자리 픽셀만 선명하게 하고 큰 값은 넓은 폭의 픽셀을 선명하게 합니다. 정확한 값은 이미지의 크기에 따라 다릅니다. 기본값은 0.2이고, 범위는 0-250입니다. |
| 임계값 | 언샵 마스크 필터를 적용할 때 무시할 대비 범위를 결정합니다. 즉, 이 옵션은 가장자리 픽셀로 간주되고 선명하게 되기 전에 선명하게 된 픽셀이 주변 영역과 얼마나 다른지를 결정합니다. 노이즈가 발생하지 않도록 0~255 사이의 값을 사용해 보십시오. |

선명하게 하기는 [이미지 선명하게 하기](/help/assets/assets/sharpening_images.pdf).

## Dynamic Media 이미지 프로필 만들기 {#creating-image-profiles}

다른 자산 유형에 대한 고급 처리 매개 변수를 정의하려면 [자산 처리 구성](config-dms7.md#configuring-asset-processing).

자세한 내용은 [메타데이터, 이미지 및 비디오 처리 프로필](processing-profiles.md).

참조 - [처리 프로필 사용을 위한 디지털 자산 구성 우수 사례](/help/assets/organize-assets.md).

**Dynamic Media 이미지 프로필을 만들려면 다음을 수행하십시오.**

1. Adobe Experience Manager 로고를 선택하고 다음 위치로 이동합니다 **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 이미지 프로필]**.
1. 선택 **[!UICONTROL 만들기]** 이미지 프로필을 추가할 수 있습니다.
1. 프로파일 이름 및 언샵 마스크, 자르기, 견본 또는 둘 다에 대한 값을 입력합니다.

   목적에 맞는 프로필 이름을 사용하십시오. 예를 들어, 색상 견본만 생성하는 프로파일을 만들려면, 즉 스마트 자르기가 비활성화되어 있고(꺼져 있으며) 색상 및 이미지 견본이 활성화되어(켜져 있음) 프로파일 이름 &quot;스마트 색상 견본&quot;을 사용합니다.

   See also [Smart Crop and Smart Swatch Options](#crop-options) and [Unsharp Mask](#unsharp-mask).

   ![자르기](assets/crop.png)

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다. 새로 만든 프로필이 사용 가능한 프로필 목록에 나타납니다.

## Dynamic Media 이미지 프로필 편집 또는 삭제 {#editing-or-deleting-image-profiles}

1. Experience Manager 로고를 선택하고 **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 이미지 프로필]**.
1. 편집하거나 제거할 이미지 프로필을 선택합니다. 편집하려면 다음을 선택합니다 **[!UICONTROL 이미지 프로필 편집]**. 제거하려면 다음을 선택합니다 **[!UICONTROL 이미지 프로필 삭제]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. 편집할 경우 변경 사항을 저장합니다. 삭제할 경우 프로필을 제거할지 확인합니다.

## 폴더에 Dynamic Media 이미지 프로필 적용 {#applying-an-image-profile-to-folders}

이미지 프로필을 폴더에 할당하면 모든 하위 폴더는 해당 상위 폴더에서 프로필을 자동으로 상속합니다. 이 워크플로우는 한 개의 이미지 프로필만 폴더에 할당할 수 있음을 의미합니다. 따라서 자산을 업로드, 저장, 사용 및 보관하는 의 폴더 구조를 신중하게 고려하십시오.

폴더에 다른 이미지 프로필을 할당한 경우 새 프로필이 이전 프로필을 무시합니다. 이전에 기존 폴더 자산은 변경되지 않은 상태로 유지됩니다. 새 프로필은 나중에 폴더에 추가된 자산에 적용됩니다.

프로필이 할당된 폴더는 카드에 표시되는 프로필 이름을 사용하여 사용자 인터페이스에 표시됩니다.

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

이미지 프로필을 특정 폴더에 적용하거나 모든 자산에 전체적으로 적용할 수 있습니다.

나중에 변경한 기존 이미지 프로필이 이미 있는 폴더에서 자산을 재처리할 수 있습니다. 자세한 내용은 [처리 중인 프로필을 편집한 후 폴더에서 자산을 재처리합니다](processing-profiles.md#reprocessing-assets).

### 특정 폴더에 Dynamic Media 이미지 프로필 적용 {#applying-image-profiles-to-specific-folders}

내에서 폴더에 이미지 프로필을 적용할 수 있습니다 **[!UICONTROL 도구]** 메뉴 또는 폴더에 있는 경우 **[!UICONTROL 속성]**. 이 섹션에서는 두 가지 방법으로 폴더에 이미지 프로필을 적용하는 방법을 설명합니다.

Folders that have a profile already assigned to it are indicated by the display of the profile&#39;s name directly below the folder name.

나중에 변경한 기존 비디오 프로필이 이미 있는 폴더에서 자산을 재처리할 수 있습니다. 자세한 내용은 [처리 중인 프로필을 편집한 후 폴더에서 자산을 재처리합니다](processing-profiles.md#reprocessing-assets).

#### 프로필 사용자 인터페이스의 폴더에 Dynamic Media 이미지 프로필 적용 {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Experience Manager 로고를 선택하고 **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 이미지 프로필]**.
1. 폴더 또는 여러 폴더에 적용할 이미지 프로필을 선택합니다.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. 선택 **[!UICONTROL 폴더에 처리 프로필 적용]** 새로 업로드한 자산을 받는 데 사용할 폴더 또는 여러 폴더를 선택하고 을(를) 선택합니다 **[!UICONTROL 적용]**. Folders that have a profile already assigned to it are indicated by the display of the profile&#39;s name directly below the folder name.

#### 속성의 폴더에 Dynamic Media 이미지 프로필 적용 {#applying-image-profiles-to-folders-from-properties}

1. Experience League 로고를 선택하고 **[!UICONTROL 자산]**. 그런 다음 이미지 프로필을 적용할 폴더의 상위 폴더로 이동합니다.
1. 폴더에서 확인 표시를 선택하여 선택한 다음 선택합니다 **[!UICONTROL 속성]**.
1. 을(를) 선택합니다 **[!UICONTROL 이미지 프로필]** 탭. 에서 **[!UICONTROL 프로필 이름]** 드롭다운 목록에서 프로파일을 선택한 다음 **[!UICONTROL 저장 및 닫기]**. Folders that have a profile already assigned to it are indicated by the display of the profile&#39;s name directly below the folder name.

   ![chlimage_1-256](assets/chlimage_1-256.png)

### Dynamic Media 이미지 프로필을 전체적으로 적용 {#applying-an-image-profile-globally}

폴더에 프로필을 적용하는 것 외에도 Experience Manager 자산에 업로드된 모든 컨텐츠가 선택한 프로필이 적용되도록 전체적으로 프로필을 적용할 수도 있습니다.

나중에 변경한 기존 비디오 프로필이 이미 있는 폴더에서 자산을 재처리할 수 있습니다. 자세한 내용은 [처리 중인 프로필을 편집한 후 폴더에서 자산 재처리](processing-profiles.md#reprocessing-assets).

**Dynamic Media 이미지 프로필을 전체적으로 적용하려면**

1. 다음 중 하나를 수행하십시오.

   * 다음으로 이동 `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` 해당 프로파일을 적용하고 **[!UICONTROL 저장]**.

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * 다음 노드로 CRXDE Lite으로 이동합니다. `/content/dam/jcr:content`.

      속성 추가 `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` 을(를) 선택합니다. **[!UICONTROL 모두 저장]**.

      ![configure_image_profiles](assets/configure_image_profiles.png)

## 단일 이미지의 스마트 자르기 또는 스마트 견본 편집 {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!IMPORTANT]
・ 스마트 자르기는 Dynamic Media - Scene7 모드에서만 사용할 수 있습니다.

이미지의 스마트 자르기 창을 수동으로 다시 정렬하거나 크기를 조정하여 초점을 더 세분화할 수 있습니다.

스마트 자르기를 편집하고 저장하면 특정 이미지에 자르기를 사용하는 모든 위치에 변경 사항이 전파됩니다.

필요한 경우 스마트 자르기를 다시 실행하여 추가 자르기를 다시 생성할 수 있습니다.

참조 - [여러 이미지의 스마트 자르기 또는 스마트 견본 편집](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**단일 이미지의 스마트 자르기 또는 스마트 견본을 편집하려면 다음을 수행하십시오.**

1. Experience Manager 로고를 선택하고 **[!UICONTROL 자산]**&#x200B;스마트 자르기 또는 스마트 견본 이미지 프로필이 적용된 폴더로 이동합니다.

1. 폴더를 선택하여 해당 컨텐츠를 열 수 있습니다.
1. 스마트 자르기나 스마트 견본을 조정할 이미지를 선택합니다.
1. 도구 모음에서 를 선택합니다 **[!UICONTROL 스마트 자르기]**.

1. 다음 중 하나를 수행합니다.

   * 페이지의 오른쪽 위 모서리 근처에 있는 슬라이더 막대를 왼쪽 또는 오른쪽으로 드래그하여 이미지 표시를 각각 늘리거나 줄입니다.
   * 이미지에서 코너 핸들을 드래그하여 자르기나 견본의 볼 수 있는 영역의 크기를 조정합니다.
   * 이미지에서 상자/견본을 새 위치로 드래그합니다. 이미지 색상 견본만 편집할 수 있습니다. 색상 견본은 정적입니다.
   * 이미지 위에서 을 선택합니다.  **[!UICONTROL 되돌리기]** 모든 편집 내용을 실행 취소하고 원래 자르기 또는 견본을 복원하려면 다음을 수행하십시오.

1. 페이지의 오른쪽 위 모서리 근처에 있는 를 선택합니다. **[!UICONTROL 저장]**&#x200B;를 선택하고 을 선택합니다. **[!UICONTROL 닫기]** 를 입력하여 자산의 폴더로 돌아갑니다.

## 여러 이미지의 스마트 자르기 또는 스마트 견본 편집 {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

>[!IMPORTANT]
・ 스마트 자르기는 Dynamic Media - Scene7 모드에서만 사용할 수 있습니다.

스마트 자르기가 포함된 이미지 프로필을 폴더에 적용하면 해당 폴더의 모든 이미지에 자르기가 적용됩니다. 원하는 경우 다음을 수행할 수 있습니다 *수동* 여러 이미지에서 스마트 자르기 창을 재정렬하거나 크기를 조정하여 초점을 더 세분화합니다.

스마트 자르기를 편집하고 저장하면 특정 이미지에 자르기를 사용하는 모든 위치에 변경 사항이 전파됩니다.

필요한 경우 스마트 자르기를 다시 실행하여 추가 자르기를 다시 생성할 수 있습니다.

**여러 이미지의 스마트 자르기 또는 스마트 견본을 편집하려면 다음을 수행하십시오.**

1. Experience Manager 로고를 선택하고 **[!UICONTROL 자산]**&#x200B;스마트 자르기 또는 스마트 견본 이미지 프로필이 적용된 폴더로 이동합니다.
1. 폴더에서 **[!UICONTROL 추가 작업]** (...) 아이콘을 선택한 다음 **[!UICONTROL 스마트 자르기]**.

1. 설정 **[!UICONTROL 스마트 자르기 편집]** 페이지에서 다음 중 하나를 수행합니다.

   * 페이지에서 이미지 보기 크기를 조정합니다.

      중단점 이름 드롭다운 목록의 오른쪽으로 슬라이더 막대를 왼쪽 또는 오른쪽으로 드래그하여 볼 수 있는 이미지 표시의 크기를 변경합니다.

      ![edit_smart_crops-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * 중단점 이름을 기반으로 볼 수 있는 이미지 목록을 필터링합니다. 아래 예에서는 이미지가 중단점 이름 &quot;Medium&quot;에서 필터링됩니다.

      페이지의 오른쪽 위 모서리 근처에 있는 드롭다운 목록에서 표시되는 이미지에 대해 필터링할 중단점 이름을 선택합니다. (위의 이미지를 참조하십시오.)

      ![edit_smart_crops-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * 스마트 자르기 상자의 크기를 조정합니다. 다음 중 하나를 수행합니다.

      * 이미지에 스마트 자르기 또는 스마트 견본만 있는 경우 이미지에서 자르기 상자의 코너 핸들을 드래그하여 자르기의 볼 수 있는 영역 크기를 조정합니다.
      * 이미지에 스마트 자르기와 스마트 견본이 모두 있는 경우 이미지에서 자르기 상자의 코너 핸들을 드래그하여 자르기의 볼 수 있는 영역 크기를 조정합니다. 또는 이미지 아래에서 스마트 색상 견본을 선택한 다음(색상 견본은 고정됨) 자르기 상자의 코너 핸들을 드래그하여 색상 견본의 볼 수 있는 영역의 크기를 조정합니다.

      ![이미지의 스마트 자르기 크기 조정](assets/edit_smart_crops-resize.png)

   * 스마트 자르기 상자를 이동합니다. 다음 중 하나를 수행합니다.

      * 이미지에 스마트 자르기 또는 스마트 견본만 있는 경우 이미지에서 자르기 상자를 새 위치로 드래그합니다.
      * 이미지에 스마트 자르기와 스마트 견본이 모두 있는 경우 이미지에서 스마트 자르기 상자를 새 위치로 드래그합니다. 또는 이미지 아래에서 스마트 색상 견본을 선택한 다음(색상 견본은 정적) 스마트 색상 견본 자르기 상자를 새 위치로 드래그합니다.

      ![edit_smart_crops-move](assets/edit_smart_crops-move.png)

   * 모든 편집 내용을 실행 취소하고 원본 스마트 자르기 또는 스마트 견본을 복원합니다(현재 편집 세션에만 적용).

      선택 **[!UICONTROL 되돌리기]** 이미지 위에 표시됩니다.

      ![edit_smart_crops-revert](assets/edit_smart_crops-revert.png)



1. 페이지의 오른쪽 위 모서리 근처에 있는 를 선택합니다. **[!UICONTROL 저장]**&#x200B;를 선택하고 을 선택합니다. **[!UICONTROL 닫기]** 를 입력하여 자산의 폴더로 돌아갑니다.

## 폴더에서 Dynamic Media 이미지 프로필 제거 {#removing-an-image-profile-from-folders}

폴더에서 이미지 프로필을 제거하면 모든 하위 폴더는 해당 상위 폴더에서 프로필 제거를 자동으로 상속합니다. 그러나 폴더 내에서 발생한 파일의 모든 처리가 그대로 유지됩니다.

내의 폴더에서 이미지 프로필을 제거할 수 있습니다 **[!UICONTROL 도구]** 메뉴 또는 폴더에 있는 경우 **[!UICONTROL 속성]**. 이 섹션에서는 두 가지 방법으로 폴더에서 이미지 프로필을 제거하는 방법을 설명합니다.

### 프로필 사용자 인터페이스를 통해 폴더에서 Dynamic Media 이미지 프로필 제거 {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Experience Manager 로고를 선택하고 **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 이미지 프로필]**.
1. 폴더 또는 여러 폴더에서 제거할 이미지 프로필을 선택합니다.
1. 선택 **[!UICONTROL 폴더에서 처리 프로필 제거]** 프로파일을 제거할 폴더 또는 폴더를 여러 개 선택하고 **[!UICONTROL 제거]**.

   이름이 더 이상 폴더 이름 아래에 표시되지 않으므로 이미지 프로필이 더 이상 폴더에 적용되지 않았는지 확인할 수 있습니다.

### 속성을 통해 폴더에서 Dynamic Media 이미지 프로필 제거 {#removing-image-profiles-from-folders-via-properties}

1. Experience Manager 로고를 선택하고 탐색합니다 **[!UICONTROL 자산]** 이미지 프로필을 제거할 폴더로 이동합니다.
1. 폴더에서 확인 표시를 선택하여 선택한 다음 선택합니다 **[!UICONTROL 속성]**.
1. 을(를) 선택합니다 **[!UICONTROL 이미지 프로필]** 탭.
1. 에서 **[!UICONTROL 프로필 이름]** 드롭다운 목록에서 **[!UICONTROL 없음]**&#x200B;를 선택하고 을 선택합니다. **[!UICONTROL 저장 및 닫기]**.

   Folders that have a profile already assigned to it are indicated by the display of the profile&#39;s name directly below the folder name.
