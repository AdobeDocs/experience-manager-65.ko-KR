---
title: 파노라마 이미지
description: Dynamic Media에서 파노라마 이미지를 사용하여 작업하는 방법을 알아봅니다.
uuid: ced3e5bd-93c8-4d5f-a397-1380d4d0a5e7
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 632a9074-b747-49a1-a57d-1f42bba1f4e9
docset: aem65
translation-type: tm+mt
source-git-commit: 10dae6e9f49e93d2f4923cee754c1d23d9d4b25e
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# 파노라마 이미지{#panoramic-images}

이 섹션에서는 [파노라마 이미지] 뷰어를 사용하여 회의실, 속성, 위치 또는 조경의 몰입형 360° 보기 경험을 위해 구형 파노라마 이미지를 렌더링하는 작업에 대해 설명합니다.

[뷰어 사전 설정 관리](/help/assets/managing-viewer-presets.md)도 참조하십시오.

![panoramic-image2](assets/panoramic-image2.png)

## 파노라마 이미지 뷰어에 사용할 자산 업로드 {#uploading-assets-for-use-with-the-panoramic-image-viewer}

업로드된 자산이 파노라마 이미지 뷰어와 함께 사용할 구형 파노라마 이미지로 자격을 갖추려면 자산에 다음 중 하나 또는 둘 다가 있어야 합니다.

* 2 종횡비
CRXDE Lite의 기본 종횡비 설정(2의 경우)은 다음과 같이 재정의할 수 있습니다.
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* `equirectangular` 또는 `spherical`와 `panorama`, 또는 `spherical` 및 `panoramic` 키워드로 태그되었습니다. [태그 사용](/help/sites-authoring/tags.md)을 참조하십시오.

종횡비와 키워드 기준은 모두 자산 세부 사항 페이지 및 `Panoramic Media` WCM 구성 요소의 파노라마 에셋에 적용됩니다.

파노라마 이미지 뷰어에 사용할 에셋을 업로드하려면 [에셋 업로드](/help/assets/manage-assets.md#uploading-assets)를 참조하십시오.

## Dynamic Media Classic 구성 {#configuring-dynamic-media-classic-scene}

Panoric Image 뷰어가 AEM 내에서 제대로 작동하려면 Panoramic Image 뷰어 사전 설정을 Dynamic Media Classic 및 Dynamic Media Classic 관련 메타데이터와 동기화해야 JCR에서 뷰어 사전 설정이 업데이트됩니다. 이를 수행하려면 다음 방법으로 Dynamic Media Classic을 구성하십시오.

1. [각 회사 계정에 대한 Dynamic Media ](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) Classic 인스턴스에 로그인합니다.

1. 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 설정 > 응용 프로그램 설정 > 게시 설정 > 이미지 서버를 클릭합니다.]**
1. 이미지 서버 게시 페이지의 맨 위에 있는 **[!UICONTROL 게시 컨텍스트]** 드롭다운 메뉴에서 **[!UICONTROL 이미지 제공.]**

1. 동일한 이미지 서버 게시 페이지에서 **[!UICONTROL 요청 특성 제목을 찾습니다.]**
1. 요청 속성 머리글 아래에서 **[!UICONTROL 응답 이미지 크기 제한을 찾습니다.]** 그런 다음 연관된 폭 및 높이 필드에서 파노라마 이미지의 허용 가능한 최대 이미지 크기를 늘립니다.

   Dynamic Media Classic은 25,000,000픽셀로 제한됩니다. 2:1 종횡비를 가진 이미지의 최대 허용 크기는 7000 x 3500입니다. 그러나 일반적인 데스크탑 화면의 경우 4096 x 2048픽셀로도 충분합니다.

   >[!NOTE]
   >
   >허용되는 최대 이미지 크기에 해당하는 이미지만 지원됩니다. 크기 제한을 초과하는 이미지에 대한 요청은 403 응답을 가져옵니다.

1. 속성 요청 머리글 아래에서 다음을 수행합니다.

   * 요청 난독화 모드를 **[!UICONTROL 비활성화됨으로 설정합니다.]**
   * 요청 잠금 모드를 **[!UICONTROL 비활성화됨으로 설정합니다.]**

   이러한 설정은 AEM에서 `Panoramic Media` WCM 구성 요소를 사용하는 데 필요합니다.

1. 이미지 서버 게시 페이지 하단의 왼쪽에서 **[!UICONTROL 저장을 클릭합니다.]**

1. 오른쪽 아래 모서리에서 **[!UICONTROL 닫기를 클릭합니다.]**

### 파노라마 미디어 WCM 구성 요소 {#troubleshooting-the-panoramic-media-wcm-component} 문제 해결

WCM의 파노라마 미디어 구성 요소에 이미지를 드롭했고 구성 요소 자리 표시자가 축소된 경우 다음 문제를 해결하려고 할 수 있습니다.

* 403 금지 오류가 발생하는 경우 요청한 이미지 크기가 너무 커서 발생할 수 있습니다. [Dynamic Media Classic 구성](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene)에서 **[!UICONTROL 응답 이미지 크기 제한]** 설정을 검토하십시오.

* 자산에 대한 &quot;잘못된 잠금&quot; 또는 페이지에 표시된 &quot;구문 분석 오류&quot;의 경우 요청 난독화 모드 및 요청 잠금 모드를 선택하여 이 잠금이 해제되었는지 확인합니다.
* 잘못된 캔버스 오류의 경우 이미지 자산에 대한 이전 요청에 대해 규칙 세트 정의 파일 경로를 설정하고 CTN을 무효화합니다.
* 이미지 요청이 지원되는 제한보다 크게 길어질 경우 **[!UICONTROL JPEG 인코딩 속성 > 품질]** 설정이 비어 있지 않은지 확인하십시오. **[!UICONTROL Quality]** 필드의 일반적인 설정은 `95`입니다. [이미지 서버 게시] 페이지에서 설정을 찾을 수 있습니다. 페이지에 액세스하려면 [Dynamic Media Classic 구성](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene)을 참조하십시오.

## 파노라마 이미지 미리 보기 {#previewing-panoramic-images}

[자산 미리 보기](/help/assets/previewing-assets.md)를 참조하십시오.

## 파노라마 이미지 게시 {#publishing-panoramic-images}

[자산 게시](/help/assets/publishing-dynamicmedia-assets.md)를 참조하십시오.
