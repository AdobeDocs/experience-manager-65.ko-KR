---
title: Adobe Experience Manager Assets 릴리스 노트
description: Adobe Experience Manager 6.5 자산에 대한 새로운 기능과 개선 사항입니다.
translation-type: tm+mt
source-git-commit: a6f95e04fd5b8ed28beaa12e9fd170ed495397b8

---


# Adobe Experience Manager Assets 릴리스 노트 {#aem-assets-release-notes}

다음은 Adobe Experience Manager 6.5 Assets 릴리스의 주요 기능과 주요 기능입니다.

## Integration with [!DNL Adobe Creative Cloud] and creative workflows {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager] 크리에이티브 및 마케팅 또는 비즈니스 팀이 긴밀하게 협업하는 워크플로우에서 사용할 수 있도록 다양한 방법으로 에셋을 통합하고 [!DNL Adobe Creative Cloud] 공유할 수 있습니다. [!DNL Experience Manager] 6.5는 통합 과정에서 지속적으로 개선되고 더 많은 기회를 노출하며 기존 방법을 간소화합니다.

Read on to know the specific capabilities and integrations of [!DNL Experience Manager] 6.5 that you can leverage to best support your content velocity use cases.

### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] 컨텐츠 제작 과정에서 크리에이티브 담당자와 마케터 간의 공동 작업을 강화할 수 있습니다. Creatives can access content stored in [!DNL Experience Manager Assets], without leaving the apps that they are most familiar with. Creatives can seamlessly browse, search, check out, and check in assets using the in-app panel in [!DNL Adobe Photoshop], [!DNL Adobe Illustrator], and [!DNL Adobe InDesign] apps.

[!DNL Adobe Asset Link] 는 Creative Cloud [for enterprise](https://www.adobe.com/kr/creativecloud/business/enterprise.html) 솔루션에 포함되어 있습니다. For more information about it, including necessary configuration of your [!DNL Experience Manager] deployment, see [Adobe Asset Link](https://helpx.adobe.com/kr/enterprise/using/adobe-asset-link.html).

![Adobe Photoshop에서 에셋 검색](assets/asset_search_photoshop.png)

### [!DNL Adobe Stock] 통합 {#stock}

Your organization can use its [!DNL Adobe Stock] enterprise plan within [!DNL Experience Manager Assets] to ensure that licensed assets are broadly available for your creative and marketing projects. You can quickly find, preview, and license [!DNL Adobe Stock] assets that are saved in Experience Manager, using the powerful DAM capabilities of [!DNL Experience Manager].

[!DNL Adobe Stock] 서비스는 디자이너와 기업의 모든 광고 프로젝트를 위해 고품질로 큐레이팅된 로열티가 없는 수백만 장의 사진, 벡터, 일러스트레이션, 비디오, 템플릿 및 3D 자산에 대한 액세스를 제공합니다.

For more info, see [Use [!DNL Adobe Stock] assets in Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md).

![Experience Manager Assets에서 Adobe Stock 이미지 및 라이선스 미리 보기](assets/stock_image_preview_license_options.png)

*그림:이미지[!DNL Adobe Stock]및 라이선스를 미리 볼 수[!DNL Experience Manager Assets]있습니다.*

![Experience Manager에서 라이선스가 부여된 Adobe Stock 이미지 검색 및 필터링](assets/aem-search-filters2.jpg)

*그림:에서 라이선스가 부여된[!DNL Adobe Stock]이미지를 검색하고 필터링합니다[!DNL Experience Manager].*

### 동적 참조 [!DNL Adobe InDesign]{#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] 동적으로 [!DNL Adobe InDesign] 파일에 사용됩니다. 참조된 자산이 저장소에서 이동하면 참조가 자동으로 업데이트됩니다. 자세한 내용은 복합 자산을 관리하는 [방법을 참조하십시오](/help/assets/managing-linked-subassets.md).

## Brand Portal 기능 {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] 승인된 자산을 손쉽게 확보, 효과적으로 제어 및 다양한 디바이스에서 외부 공급업체/에이전시 및 내부 비즈니스 사용자에게 안전하게 배포할 수 있습니다. 자산 공유의 효율성을 향상시키고 자산의 시장 출시 시간을 가속화하며 비준수 사용량 및 무단 액세스의 위함을 방지하는 데 도움이 됩니다.

자세한 내용은 ](https://helpx.adobe.com/experience-manager/brand-portal/using/whats-new.html)Brand Portal의 새로운 기능[을 참조하십시오.

## 연결된 자산 {#connectedassets}

대기업에서는 웹 사이트를 구축하는 데 필요한 인프라를 분배할 수 있습니다. 간혹 웹 사이트 작성 기능과 필수 디지털 자산이 다른 사일로에 상주하는 경우가 있습니다.

[!DNL Experience Manager Sites] 웹 페이지를 만드는 기능을 제공하며 웹 사이트에 필요한 자산을 제공하는 DAM(Digital Asset Management) 시스템입니다. [!DNL Experience Manager Assets] [!DNL Experience Manager] 이제 [!DNL Sites] 및 를 통합하여 위의 사용 사례를 지원합니다 [!DNL Assets]. 연결된 에셋 기능을 [구성하고 사용하는](/help/assets/use-assets-across-connected-assets-instances.md)방법을 살펴보십시오.

![다른 [!DNL Experience Manager] [!DNL Sites] [!DNL Experience Manager] 배포의 페이지에 있는 배포의 자산을 드래그합니다.](assets/connected-assets-drag-and-drop-only.gif)

*그림:다른[!DNL Experience Manager][!DNL Sites][!DNL Experience Manager]배포의 페이지에 있는 배포의 자산을 드래그합니다.*

## Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] 매력적이고 개인화된 첨단 경험을 제공하기 [!DNL Experience Manager Assets] 위해 향상된 리치 미디어 저작 및 전달 기능을 제공합니다. 하나의 고품질 마스터 에셋을 업로드하고 고급 클라우드 렌더링 및 뷰어를 사용하여 조직의 미디어 전략을 지원하기 위해 모든 변환을 즉석에서 제공할 수 있습니다.

For more details on new [!DNL Dynamic Media] features see [Dynamic Media Release Notes](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/release-notes/s7rn2017.html).

### Video 360 지원 {#video-support}

Manage your 360-video files directly in [!DNL Experience Manager] using the cutting edge viewers to deliver VR-experiences to desktops, mobile and VR-headsets. 자세한 내용은 [Video 360 사용하기](/help/assets/360-video.md)를 참조하십시오.

### 사용자 지정 비디오 썸네일 {#custom-video-thumbnails}

비디오 자체 또는 DAM에 저장된 기타 컨텐츠의 프레임을 사용하여 비디오 자산의 썸네일을 사용자 지정할 수 있습니다. 자세한 내용은 [비디오 썸네일 정보](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode)를 참조하십시오.

### 액세스 가능성 개선 {#accessibility-enhancements}

[!DNL Dynamic Media] 이제 뷰어는 Aria 지원, 화면 판독기 및 Alt-text와 같은 향상된 액세스 가능성 기능을 지원합니다. 자세한 내용은 [Dynamic Media 뷰어 릴리스 노트](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/home.html)를 참조하십시오.

## 검색 환경 개선 {#search-experience-enhancement}

[!DNL Experience Manager] 6.5 이상 버전에서 마케터는 원하는 자산을 검색 결과 페이지에서 보다 빠르게 찾을 수 있습니다. 검색 패싯은 검색 필터를 적용하기 전에도 자산 수로 업데이트됩니다. 필터에 대한 예상 수를 확인하면 사용자가 검색 결과를 효율적으로 탐색할 수 있습니다. 자세한 내용은 Experience Manager에서 [자산 검색을 참조하십시오](../assets/search-assets.md).

![검색 패싯에서 검색 결과를 필터링하지 않고 자산 수를 확인합니다](/help/assets/assets/asset_search_results_in_facets_filters.png)

*그림:검색 패싯에서 검색 결과를 필터링하지 않고 자산 수를 참조하십시오.*

## 유용성 개선 {#usability-enhancement}

이제 폴더 내의 로드된 모든 에셋을 선택하거나 검색 결과에서 한 번에 선택할 수 있습니다. 여러 자산을 신속하게 관리하는 데 도움이 됩니다. The check box selects all the assets that fits the scenario, say a search result and not just the assets that are visible in the [!DNL Experience Manager] interface.

![모두 선택 옵션을 사용하여 한 번의 클릭으로 로드된 모든 자산을 선택합니다.](assets/select-all-in-aem-assets.gif)

*그림:모두 선택 옵션을 사용하여 한 번의 클릭으로 로드된 모든 자산을 선택합니다.*

## 메타데이터 개선 사항 {#metadata-enhancements}

[!DNL Assets] 폴더 속성 페이지에 표시되는 레이아웃 및 메타데이터를 정의하는 자산 폴더의 메타데이터 스키마를 만들 수 있습니다. 이제 폴더 메타데이터 스키마를 기존 폴더에 지정하거나 새 폴더를 생성할 때 지정할 수 있습니다. 자세한 내용은 [폴더 메타데이터 스키마](/help/assets/folder-metadata-schema.md)를 참조하십시오.

계단식 메타데이터를 지정할 때 형식에 수동으로 입력하는 대신 런타임 시 JSON 파일에서 선택 항목을 로드할 수 있습니다. 자세한 내용은 [계단식 메타데이터](/help/assets/cascading-metadata.md)를 참조하십시오.

## 보고 개선 사항 {#reporting-enhancements}

이제 컨텐츠 조각 및 링크 공유가 다운로드된 보고서에 포함됩니다. 자세한 정보는 [자산 보고서](/help/assets/asset-reports.md)를 참조하십시오.
