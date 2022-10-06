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
feature: Panoramic Images,Asset Management
role: User, Admin
exl-id: 4d6fbeb1-94db-4154-9e41-b76033fb4398
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 4%

---

# 파노라마 이미지{#panoramic-images}

이 섹션에서는 공간, 속성, 위치 또는 조경의 몰입형 360° 보기 환경을 위해 파노라마 뷰어를 사용하여 구형 파노라마 이미지를 렌더링하는 방법에 대해 설명합니다.

참조 - [뷰어 사전 설정 관리](/help/assets/managing-viewer-presets.md).

![파노라마 이미지2](assets/panoramic-image2.png)

## 파노라마 이미지 뷰어에서 사용할 자산을 업로드합니다 {#uploading-assets-for-use-with-the-panoramic-image-viewer}

업로드된 자산이 파노라마 이미지 뷰어와 함께 사용할 구형 파노라마 이미지로 분류되도록 하려면 자산에 다음 중 하나 또는 둘 다 있어야 합니다.

* 2 종횡비입니다.
CRXDE Lite에서 다음과 같은 기본 종횡비 설정 2를 무시할 수 있습니다.
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* 키워드가 태그됨 `equirectangular`, 또는 `spherical`및 `panorama`, 또는 `spherical` 및 `panoramic`. 자세한 내용은 [태그 사용](/help/sites-authoring/tags.md).

Both the aspect ratio and keyword criteria apply to panoramic assets for the asset details page and the `Panoramic Media` WCM component.

파노라마 이미지 뷰어에 사용할 자산을 업로드하려면 를 참조하십시오 [자산 업로드](/help/assets/manage-assets.md#uploading-assets).

## Dynamic Media Classic 구성 {#configuring-dynamic-media-classic-scene}

Adobe Experience Manager 내에서 파노라마 이미지 뷰어가 제대로 작동하려면 내에서 파노라마 이미지 뷰어 사전 설정을 Dynamic Media Classic 및 Dynamic Media Classic 관련 메타데이터와 동기화하여 뷰어 사전 설정이 JCR에서 업데이트되도록 하십시오. 이 동기화를 수행하려면 다음과 같이 Dynamic Media Classic을 구성하십시오.

1. 를 엽니다. [Dynamic Media Classic 데스크탑 애플리케이션](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)그런 다음 계정에 로그인합니다.

1. 페이지의 오른쪽 위 모서리 근처에 있는 를 선택합니다. **[!UICONTROL 설정]** > **[!UICONTROL 애플리케이션 설정]** > **[!UICONTROL 게시 설정]** > **[!UICONTROL 이미지 서버]**.
1. 이미지 서버 게시 페이지의 **[!UICONTROL 게시 컨텍스트]** 상단 근처에 있는 드롭다운 메뉴에서 **[!UICONTROL 이미지 제공]**.

1. 동일한 이미지 서버 게시 페이지에서 제목을 찾습니다 **[!UICONTROL 요청 속성]**.
1. 요청 속성 제목 아래에서 를 찾습니다. **[!UICONTROL 회신 이미지 크기 제한]**. 그런 다음 연결된 너비 및 높이 필드에서 파노라마 이미지에 사용할 수 있는 최대 이미지 크기를 늘립니다.

   Dynamic Media Classic은 25,000,000픽셀로 제한됩니다. 2:1 종횡비를 갖는 이미지의 최대 허용 크기는 7000 x 3500입니다. 그러나 일반적인 데스크탑 화면의 경우 4096 x 2048 픽셀로도 충분합니다.

   >[!NOTE]
   >
   >허용되는 최대 이미지 크기에 해당하는 이미지만 지원됩니다. 크기 제한을 초과하는 이미지에 대한 요청은 403 응답을 생성합니다.

1. 요청 속성 제목 아래에서 다음을 수행합니다.

   * 요청 난독화 모드를 로 설정 **[!UICONTROL 비활성화됨]**.
   * 요청 잠금 모드를 로 설정 **[!UICONTROL 비활성화됨]**.

   이러한 설정은 `Panoramic Media` Experience Manager의 WCM 구성 요소입니다.

1. [이미지 서버 게시] 페이지 하단의 왼쪽의 를 선택합니다 **[!UICONTROL 저장]**.

1. 오른쪽 아래 모서리에서 을(를) 선택합니다. **[!UICONTROL 닫기]**.

### 파노라마 미디어 WCM 구성 요소 문제 해결 {#troubleshooting-the-panoramic-media-wcm-component}

이미지를 WCM의 파노라마 미디어 구성 요소에 끌어다 놓고 구성 요소 자리 표시자가 축소된 경우 다음 문제를 해결하십시오.

* 403 금지된 오류가 발생하는 경우 요청한 이미지 크기가 너무 커서 발생할 수 있습니다. 를 검토합니다. **[!UICONTROL 회신 이미지 크기 제한]** 설정 [Dynamic Media Classic 구성](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

* 자산에 대한 &quot;잘못된 잠금&quot; 또는 페이지에 표시된 &quot;구문 분석 오류&quot; 표시에 대해서는 요청 난독화 모드 및 요청 잠금 모드 를 선택하여 비활성화되어 있는지 확인하십시오.
* 오염된 캔버스 오류에 대해 이미지 자산에 대한 이전 요청에 대해 규칙 세트 정의 파일 경로 를 설정하고 CTN을 무효화합니다.
* 지원되는 제한보다 크기가 큰 이미지 요청 이후에 이미지 품질이 낮은 경우 **[!UICONTROL JPEG 인코딩 속성 > 품질]** 설정이 비어 있지 않습니다. 에 대한 일반적인 설정 **[!UICONTROL 품질]** 필드: `95`. [이미지 서버 게시] 페이지에서 설정을 찾을 수 있습니다. 페이지에 액세스하려면 다음을 참조하십시오 [Dynamic Media Classic 구성](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

## 파노라마 이미지 미리 보기 {#previewing-panoramic-images}

자세한 내용은 [자산 미리 보기](/help/assets/previewing-assets.md).

## 파노라마 이미지 게시 {#publishing-panoramic-images}

자세한 내용은 [자산 게시](/help/assets/publishing-dynamicmedia-assets.md).
