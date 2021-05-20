---
title: 파노라마 이미지
description: Dynamic Media에서 파노라마 이미지로 작업하는 방법을 알아봅니다.
uuid: ced3e5bd-93c8-4d5f-a397-1380d4d0a5e7
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 632a9074-b747-49a1-a57d-1f42bba1f4e9
docset: aem65
feature: 파노라마 이미지,자산 관리
role: Business Practitioner, Administrator
exl-id: 4d6fbeb1-94db-4154-9e41-b76033fb4398
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---

# 파노라마 이미지{#panoramic-images}

이 섹션에서는 공간, 속성, 위치 또는 조경의 몰입형 360° 보기 환경을 위해 파노라마 뷰어를 사용하여 구형 파노라마 이미지를 렌더링하는 방법에 대해 설명합니다.

또한 [뷰어 사전 설정 관리](/help/assets/managing-viewer-presets.md)를 참조하십시오.

![파노라마 이미지2](assets/panoramic-image2.png)

## 파노라마 이미지 뷰어에서 사용할 자산 업로드 {#uploading-assets-for-use-with-the-panoramic-image-viewer}

업로드된 자산이 파노라마 이미지 뷰어와 함께 사용할 구형 파노라마 이미지로 분류되도록 하려면 자산에 다음 중 하나 또는 둘 다 있어야 합니다.

* 2 종횡비입니다.
CRXDE Lite에서 다음과 같은 기본 종횡비 설정 2를 무시할 수 있습니다.
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* `equirectangular` 또는 `spherical`와 `panorama`, 또는 `spherical` 및 `panoramic` 키워드가 태그되었습니다. [태그 사용](/help/sites-authoring/tags.md)을 참조하십시오.

종횡비와 키워드 기준은 모두 자산 세부 사항 페이지와 `Panoramic Media` WCM 구성 요소의 파노라마 자산에 적용됩니다.

파노라마 이미지 뷰어에서 사용할 자산을 업로드하려면 [자산 업로드](/help/assets/manage-assets.md#uploading-assets)를 참조하십시오.

## Dynamic Media Classic 구성 {#configuring-dynamic-media-classic-scene}

파노라마 이미지 뷰어가 AEM 내에서 제대로 작동하려면 JCR에서 뷰어 사전 설정이 업데이트되도록 Dynamic Media Classic 및 Dynamic Media Classic 관련 메타데이터와 파노라마 이미지 뷰어 사전 설정을 동기화해야 합니다. 이를 수행하려면 다음 방법으로 Dynamic Media Classic을 구성하십시오.

1. [Dynamic Media Classic 데스크탑 응용 프로그램](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)을 연 다음 계정에 로그인합니다.

1. 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 설정 > 애플리케이션 설정 > 게시 설정 > 이미지 서버를 클릭합니다.]**
1. 이미지 서버 게시 페이지의 맨 위에 있는 **[!UICONTROL 게시 컨텍스트]** 드롭다운 메뉴에서 **[!UICONTROL 이미지 제공]**&#x200B;을 선택합니다.

1. 동일한 이미지 서버 게시 페이지에서 **[!UICONTROL 요청 속성 제목을 찾습니다.]**
1. 요청 속성 제목 아래에서 **[!UICONTROL 회신 이미지 크기 제한을 찾습니다.]** 그런 다음 연결된 너비 및 높이 필드에서 파노라마 이미지에 사용할 수 있는 최대 이미지 크기를 늘립니다.

   Dynamic Media Classic의 제한 픽셀은 25,000,000픽셀입니다. 2:1 종횡비를 갖는 이미지의 최대 허용 크기는 7000 x 3500입니다. 그러나 일반적인 데스크탑 화면의 경우 4096 x 2048 픽셀로도 충분합니다.

   >[!NOTE]
   >
   >허용되는 최대 이미지 크기에 해당하는 이미지만 지원됩니다. 크기 제한을 초과하는 이미지에 대한 요청은 403 응답을 생성합니다.

1. 요청 속성 제목 아래에서 다음을 수행합니다.

   * 요청 난독화 모드를 **[!UICONTROL 비활성화로 설정합니다.]**
   * 요청 잠금 모드를 **[!UICONTROL 비활성화로 설정합니다.]**

   이러한 설정은 AEM에서 `Panoramic Media` WCM 구성 요소를 사용하는 데 필요합니다.

1. [이미지 서버 게시] 페이지 하단의 왼쪽의 **[!UICONTROL 저장.]**

1. 오른쪽 아래 모서리에서 **[!UICONTROL 닫기.]**

### 파노라마 미디어 WCM 구성 요소 문제 해결 {#troubleshooting-the-panoramic-media-wcm-component}

이미지를 WCM의 파노라마 미디어 구성 요소에 끌어다 놓고 구성 요소 자리 표시자가 축소된 경우 다음 문제를 해결할 수 있습니다.

* 403 금지된 오류가 발생한 경우 요청된 이미지 크기가 너무 커서 오류가 발생했을 수 있습니다. [Dynamic Media Classic 구성](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene)에서 **[!UICONTROL 회신 이미지 크기 제한]** 설정을 검토하십시오.

* 자산에 대한 &quot;잘못된 잠금&quot; 또는 페이지에 표시된 &quot;구문 분석 오류&quot; 표시에 대해서는 요청 난독화 모드 및 요청 잠금 모드 를 선택하여 비활성화되어 있는지 확인하십시오.
* 오염된 캔버스 오류의 경우 이미지 자산에 대한 이전 요청에 대해 규칙 세트 정의 파일 경로 를 설정하고 CTN을 무효화합니다.
* 이미지 요청의 크기가 지원되는 제한보다 큰 경우 이미지 요청이 발생하면 **[!UICONTROL JPEG 인코딩 속성 > 품질]** 설정이 비어 있지 않은지 확인하십시오. **[!UICONTROL Quality]** 필드에 대한 일반적인 설정은 `95`입니다. [이미지 서버 게시] 페이지에서 설정을 찾을 수 있습니다. 페이지에 액세스하려면 [Dynamic Media Classic 구성](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene)을 참조하십시오.

## 파노라마 이미지 미리 보기 {#previewing-panoramic-images}

[자산 미리 보기](/help/assets/previewing-assets.md)를 참조하십시오.

## 파노라마 이미지 게시 {#publishing-panoramic-images}

[자산 게시](/help/assets/publishing-dynamicmedia-assets.md)를 참조하십시오.
