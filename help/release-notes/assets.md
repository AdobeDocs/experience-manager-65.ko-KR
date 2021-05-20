---
title: ' [!DNL Adobe Experience Manager Assets] 6.5의 릴리스 노트.'
description: ' [!DNL Adobe Experience Manager] 6.5 [!DNL Assets]에 대한 새 기능 및 개선 사항입니다.'
exl-id: 6d9c9f09-ea42-43fb-98f7-12ce82d308bf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 93%

---

# [!DNL Adobe Experience Manager Assets] 릴리스 노트  {#aem-assets-release-notes}

다음은 [!DNL Adobe Experience Manager] 6.5 [!DNL Assets] 릴리스의 주요 기능입니다.

## [!DNL Adobe Creative Cloud] 및 광고 워크플로우와 통합{#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager]는 광고 및 마케팅 또는 비즈니스 팀이 밀접하게 협력하는 워크플로우에서 [!DNL Adobe Creative Cloud]와 통합하고 자산을 공유하는 다양한 방법을 제공합니다. [!DNL Experience Manager] 6.5는 통합 과정에서 지속적으로 개선되고 더 많은 기회를 노출하며 기존 방법을 간소화합니다.

컨텐츠 속도 사용 사례를 최상으로 지원하기 위해 활용할 수 있는 [!DNL Experience Manager] 6.5의 특정 기능 및 통합 관련 사항을 숙지하고 있어야 합니다.

### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link]는 컨텐츠 작성 프로세스에서 광고 팀과 마케터 간의 협업을 강화합니다. 광고 팀은 친숙한 앱을 종료하지 않고 [!DNL Experience Manager Assets]에 저장된 컨텐츠에 액세스할 수 있습니다. 광고 팀은 [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] 및 [!DNL Adobe InDesign] 앱에서 앱 내 패널을 사용하여 자산을 원활하게 탐색, 검색, 체크아웃 및 체크인할 수 있습니다.

[!DNL Adobe Asset Link]는 [Creative Cloud for Enterprise](https://www.adobe.com/kr/creativecloud/business/enterprise.html) 제품의 일부입니다. [!DNL Experience Manager] 배포의 필수 구성을 포함한 자세한 정보는 [Adobe Asset Link](https://helpx.adobe.com/kr/enterprise/using/adobe-asset-link.html)를 참조하십시오.

![Adobe Photoshop에서 자산 검색](assets/asset_search_photoshop.png)

### [!DNL Adobe Stock] 통합 {#stock}

조직은 [!DNL Experience Manager Assets] 내에서 [!DNL Adobe Stock] 엔터프라이즈 플랜을 사용하여 라이선스가 있는 자산이 귀사의 광고 및 마케팅 프로젝트에 폭넓게 사용 가능한지 확인할 수 있습니다. [!DNL Adobe Stock]의 강력한 DAM 기능을 사용하여 Experience Manager에 저장된 [!DNL Experience Manager] 자산을 빠르게 찾고, 미리 보고, 라이선스를 제공할 수 있습니다.

[!DNL Adobe Stock] 서비스는 디자이너와 기업의 모든 광고 프로젝트를 위해 고품질로 큐레이팅된 로열티가 없는 수백만 장의 사진, 벡터, 일러스트레이션, 비디오, 템플릿 및 3D 자산에 대한 액세스를 제공합니다.

자세한 정보는 [Experience Manager 자산에서 Adobe Stock 자산 사용](/help/assets/aem-assets-adobe-stock.md)을 참조하십시오.

![Experience Manager Assets 내에서 Adobe Stock 이미지 및 라이선스 미리 보기](assets/stock_image_preview_license_options.png)

*그림: [!DNL Experience Manager Assets] 내의 [!DNL Adobe Stock] 이미지 및 라이선스 미리 보기.*

![Experience Manager에서 라이선스가 있는 Adobe Stock 이미지 검색 및 필터링](assets/aem-search-filters2.jpg)

*그림: [!DNL Adobe Stock]에서 라이선스가 부여된* 이미지 검색 및 필터링.[!DNL Experience Manager]

### [!DNL Adobe InDesign]에서 동적 참조 {#dynamic-references-in-indesign}

[!DNL Adobe InDesign] 파일에 사용된 [!DNL Experience Manager Assets]이 동적입니다. 참조된 자산이 저장소에서 이동하면 참조가 자동으로 업데이트됩니다. 자세한 내용은 [조합 자산을 관리하는 방법](/help/assets/managing-linked-subassets.md)을 참조하십시오.

## Brand Portal 기능 {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal]은 승인된 자산을 외부 공급업체/에이전시 및 내부 비즈니스 사용자가 간편하게 구매하고 효과적으로 제어하며 장치 간에 안전하게 분배할 수 있도록 지원합니다. 자산 공유의 효율성을 향상시키고 자산의 시장 출시 시간을 가속화하며 비준수 사용량 및 무단 액세스의 위함을 방지하는 데 도움이 됩니다.

자세한 내용은 ](https://helpx.adobe.com/kr/experience-manager/brand-portal/using/whats-new.html)Brand Portal의 새로운 기능[을 참조하십시오.

## 연결된 자산 {#connectedassets}

대기업에서는 웹 사이트를 구축하는 데 필요한 인프라를 분배할 수 있습니다. 간혹 웹 사이트 작성 기능과 필수 디지털 자산이 다른 사일로에 상주하는 경우가 있습니다.

[!DNL Experience Manager Sites]는 웹 페이지를 구축하는 기능을 제공하며, [!DNL Experience Manager Assets]은 웹 사이트에 필요한 자산을 제공하는 DAM(디지털 자산 관리) 시스템입니다. [!DNL Experience Manager]는 이제 [!DNL Sites] 및 [!DNL Assets]을 통합하여 위의 사용 사례를 지원합니다. [연결된 자산 기능을 구성하고 사용하는 방법](/help/assets/use-assets-across-connected-assets-instances.md)을 참조하십시오.

![다른 [!DNL Experience Manager] 배포의 [!DNL Sites] 페이지에 있는 [!DNL Experience Manager] 배포의 자산을 드래그합니다.](assets/connected-assets-drag-and-drop-only.gif)

*그림: 다른 [!DNL Experience Manager] 배포의 [!DNL Sites] 페이지에 있는 [!DNL Experience Manager] 배포의 자산을 드래그합니다.*

## Dynamic Media {#dynamic-media}

[!DNL Dynamic Media]는 [!DNL Experience Manager Assets]에서 향상된 리치 미디어 작성 및 전달 기능을 제공하여 몰입 및 맞춤화된 최신 경험을 제공합니다. 고품질의 단일 마스터 자산을 업로드 및 고급 클라우드 렌더링 및 뷰어를 통해 모든 리디렉션의 조합을 제공하여 조직의 미디어 전략을 지원할 수 있습니다.

새 [!DNL Dynamic Media] 기능에 대한 자세한 내용은 [Dynamic Media 릴리스 노트](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html)를 참조하십시오.

### 360 비디오 지원 {#video-support}

최첨단 뷰어를 통해 [!DNL Experience Manager]에서 Video 360 파일을 직접 관리하여 데스크탑, 모바일 및 VR 헤드셋에 VR 경험을 제공할 수 있습니다. 자세한 내용은 [Video 360 사용하기](/help/assets/360-video.md)를 참조하십시오.

### 사용자 정의 비디오 축소판 {#custom-video-thumbnails}

비디오 자체 또는 DAM에 저장된 기타 컨텐츠의 프레임을 사용하여 비디오 자산의 썸네일을 사용자 지정할 수 있습니다. 자세한 내용은 [비디오 썸네일 정보](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode)를 참조하십시오.

### 액세스 가능성 개선 {#accessibility-enhancements}

이제 [!DNL Dynamic Media] 뷰어에는 Aria 지원, 화면 판독기 및 대체 텍스트와 같은 향상된 액세스 가능성에 대한 지원이 포함되어 있습니다. 자세한 내용은 [Dynamic Media 뷰어 릴리스 노트](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html)를 참조하십시오.

## 검색 환경 개선 {#experience-enhancement-for-searching}

[!DNL Experience Manager] 6.5에서는 마케터가 검색 결과 페이지에서 원하는 자산을 더 빨리 발견할 수 있습니다. 검색 패싯은 검색 필터를 적용하기 전에도 자산 수로 업데이트됩니다. 필터에 대한 예상 수를 확인하면 사용자가 검색 결과를 효율적으로 탐색할 수 있습니다. 자세한 내용은 [Experience Manager에서 자산 검색](../assets/search-assets.md)을 참조하십시오.

![검색 패싯에서 검색 결과를 필터링하지 않고 자산 수를 확인합니다](/help/assets/assets/asset_search_results_in_facets_filters.png)

*그림: 검색 패싯에서 검색 결과를 필터링하지 않고 자산 수 확인.*

## 유용성 개선 {#usability-enhancement}

이제 폴더 내 또는 검색 결과에서 한 번에 로드된 모든 자산을 선택할 수 있습니다. 여러 자산을 신속하게 관리하는 데 도움이 됩니다. 이 확인란은 [!DNL Experience Manager] 인터페이스에 표시되는 자산뿐만 아니라 시나리오에 맞는 모든 자산, 즉 검색 결과를 선택합니다.

![두 선택 옵션을 사용하여 한 번의 클릭으로 모든 자산을 선택합니다.](assets/select-all-in-aem-assets.gif)

*그림: 모두 선택 옵션을 사용하여 한 번의 클릭으로 모든 자산 선택.*

## 메타데이터 개선 사항 {#metadata-enhancements}

[!DNL Assets]을 사용하면 폴더 속성 페이지에 표시되는 레이아웃 및 메타데이터를 정의하는 자산 폴더에 대한 메타데이터 스키마를 생성할 수 있습니다. 이제 폴더 메타데이터 스키마를 기존 폴더에 지정하거나 새 폴더를 생성할 때 지정할 수 있습니다. 자세한 내용은 [폴더 메타데이터 스키마](/help/assets/metadata-config.md#folder-metadata-schema)를 참조하십시오.

계단식 메타데이터를 지정할 때 형식에 수동으로 입력하는 대신 런타임 시 JSON 파일에서 선택 항목을 로드할 수 있습니다. 자세한 내용은 [계단식 메타데이터](/help/assets/metadata-schemas.md#cascading-metadata)을 참조하십시오.

## 보고 개선 사항 {#reporting-enhancements}

컨텐츠 조각 및 링크 공유는 지금 다운로드된 보고서에 포함됩니다. 자세한 정보는 [자산 보고서](/help/assets/asset-reports.md)를 참조하십시오.
