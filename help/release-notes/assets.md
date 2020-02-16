---
title: AEM Assets 릴리스 노트
description: Adobe Experience Manager 6.5 자산에 대한 새로운 기능과 개선 사항입니다.
uuid: f785029d-e0fd-494f-b215-7b4caca4e806
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 1ab34a42-2f0e-4b05-a7b6-2fc8dca07ef5
docset: aem65
translation-type: tm+mt
source-git-commit: 95d9ed8a0ccfa7651b83058d337511dd6b15665f

---


# AEM Assets 릴리스 노트{#aem-assets-release-notes}

다음은 AEM 6.5 자산 릴리스의 주요 기능입니다.

## Adobe Creative Cloud 및 광고 워크플로우와 통합 {#integration-with-adobe-creative-cloud-and-creative-workflows}

AEM에서는 광고 및 마케팅 또는 비즈니스 팀이 밀접하게 협력하는 워크플로우에서 Adobe Creative Cloud와 통합하고 자산을 공유하는 다양한 방법을 제공합니다. AEM 6.5는 통합 과정에서 지속적으로 개선되고 더 많은 기회를 노출하며 기존 방법을 간소화합니다.

컨텐츠 속도 사용 사례를 최상으로 지원하기 위해 활용할 수 있는 AEM 6.5의 특정 기능 및 통합 관련 사항을 숙지하고 있어야 합니다.

### Adobe Asset Link {#aal}

Adobe Asset Link는 컨텐츠 작성 프로세스에서 광고 소재와 마케터 간의 협업을 강화합니다. 광고 팀은 친숙한 앱을 종료하지 않고 Adobe Experience Manager Assets(AEM Assets)에 저장된 컨텐츠에 액세스할 수 있습니다. Photoshop, Illustrator, InDesign 앱에서 앱 내 패널을 사용하여 자산을 원활하게 탐색, 검색, 체크아웃 및 체크인할 수 있습니다.

Adobe Asset Link는 [Creative Cloud for enterprise](https://www.adobe.com/creativecloud/business/enterprise.html) 오퍼링의 일부입니다. AEM 배포의 필수 구성을 포함한 자세한 정보는 [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)를 참조하십시오.

![자산 검색 Photoshop](assets/asset_search_photoshop.png)

### Adobe Stock 통합 {#stock}

조직은 AEM Assets 내에서 Adobe Stock 엔터프라이즈 플랜을 사용하여 라이선스가 부여된 자산을 크리에이티브 및 마케팅 프로젝트에 광범위하게 사용할 수 있도록 할 수 있습니다. AEM의 강력한 DAM 기능을 사용하여 AEM에 저장된 Adobe Stock 자산을 빠르게 찾고, 미리 보고, 라이센스를 제공할 수 있습니다.

Adobe Stock 서비스는 디자이너와 기업의 모든 광고 프로젝트를 위해 고품질로 큐레이팅된 로열티가 없는 수백만 장의 사진, 벡터, 일러스트레이션, 비디오, 템플릿 및 3D 자산에 대한 액세스를 제공합니다.

자세한 정보는 [AEM Assets에서 Adobe Stock 자산 사용](/help/assets/aem-assets-adobe-stock.md)을 참조하십시오.

![AEM Assets 내에서 Adobe Stock 이미지 및 라이센스 미리 보기](assets/stock_image_preview_license_options.png)

AEM Assets 내에서 Adobe Stock 이미지 및 라이센스 미리 보기

![AEM에서 라이센스가 있는 Adobe Stock 이미지를 검색 및 필터링](assets/aem-search-filters2.jpg)

AEM에서 라이센스가 있는 Adobe Stock 이미지를 검색 및 필터링

### Dynamic references in Adobe InDesign {#dynamic-references-in-indesign}

Adobe InDesign 파일에 사용된 AEM Assets은 동적입니다. 참조된 자산이 JCR 계층에서 이동하면 참조가 자동으로 업데이트됩니다. 자세한 내용은 [복합 자산 관리](/help/assets/managing-linked-subassets.md)를 참조하십시오.

## Brand Portal 기능 {#brand-portal-capabilities}

AEM Assets Brand Portal은 승인된 자산을 외부 공급업체/에이전시 및 내부 비즈니스 사용자가 간편하게 구매하고 효과적으로 제어하며 디바이스 간에 안전하게 분배할 수 있도록 지원합니다. 자산 공유의 효율성을 향상시키고 자산의 시장 출시 시간을 가속화하며 비준수 사용량 및 무단 액세스의 위함을 방지하는 데 도움이 됩니다.

자세한 내용은 ](https://helpx.adobe.com/experience-manager/brand-portal/using/whats-new.html)Brand Portal의 새로운 기능[을 참조하십시오.

## 연결된 자산 {#connectedassets}

대기업에서는 웹 사이트를 구축하는 데 필요한 인프라를 분배할 수 있습니다. 간혹 웹 사이트 작성 기능과 필수 디지털 자산이 다른 사일로에 상주하는 경우가 있습니다.

AEM Sites는 웹 페이지를 구축하는 기능을 제공하며, AEM Assets은 웹 사이트에 필요한 자산을 제공하는 디지털 자산 관리(DAM) 시스템입니다. AEM은 AEM Sites 및 AEM Assets를 통합하여 위의 사용 사례를 지원합니다.

자세한 정보는 [연결된 자산에서 자산 사용](/help/assets/use-assets-across-connected-assets-instances.md)을 참조하십시오.

![AEM 인스턴스의 DAM 자산을 다른 AEM 인스턴스에 있는 사이트 페이지로 끌어다 놓기](assets/connected-assets-drag-and-drop-only.gif)

AEM 인스턴스의 DAM 자산을 다른 AEM 인스턴스에 있는 사이트 페이지로 끌어다 놓기

## 다이내믹 미디어 {#dynamic-media}

Dynamic Media는 AEM Assets에서 향상된 리치 미디어 작성 및 전달 기능을 제공하여 몰입 및 맞춤화된 최신 경험을 제공합니다. 고품질의 단일 마스터 자산을 업로드 및 고급 클라우드 렌더링 및 뷰어를 통해 모든 리디렉션의 조합을 제공하여 조직의 미디어 전략을 지원할 수 있습니다.

새 Dynamic Media 기능에 대한 자세한 내용은 [Dynamic Media 릴리스 노트](https://marketing.adobe.com/resources/help/en_US/s7/release_notes/)를 참조하십시오.

### Video 360 지원 {#video-support}

Dynamic Media의 최첨단 뷰어를 통해 AEM에서 Video 360 파일을 직접 관리하여 데스크탑, 모바일 및 VR 헤드셋에 VR 경험을 제공할 수 있습니다. 자세한 내용은 [Video 360 사용하기](/help/assets/360-video.md)를 참조하십시오.

### 사용자 지정 비디오 썸네일 {#custom-video-thumbnails}

비디오 자체 또는 DAM에 저장된 기타 컨텐츠의 프레임을 사용하여 비디오 자산의 썸네일을 사용자 지정할 수 있습니다. 자세한 내용은 [비디오 썸네일 정보](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode)를 참조하십시오.

### 액세스 가능성 개선 {#accessibility-enhancements}

이제 Dynamic Media 뷰어에는 Aria 지원, 화면 리더기 및 Alt-text와 같은 향상된 액세스 가능성에 대한 지원이 포함되어 있습니다. 자세한 내용은 [Dynamic Media 뷰어 릴리스 노트](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/index.html)를 참조하십시오.

## 검색 환경 개선 {#search-experience-enhancement}

AEM 6.5 이상 버전에서 마케터는 검색 결과 페이지에서 원하는 자산을 보다 빠르게 검색할 수 있습니다. 검색 패싯은 검색 필터를 적용하기 전에도 자산 수로 업데이트됩니다. 필터에 대한 예상 수를 확인하면 사용자가 검색 결과를 효율적으로 탐색할 수 있습니다. 자세한 내용은 AEM에서 [자산 검색을 참조하십시오](../assets/search-assets.md).

![검색 패싯에서 검색 결과를 필터링하지 않고 자산 수를 확인합니다](/help/assets/assets/asset_search_results_in_facets_filters.png)

검색 패싯에서 검색 결과를 필터링하지 않고 자산 수를 확인합니다.

## 유용성 개선 {#usability-enhancement}

이제 폴더 내 또는 검색 결과에서 한 번에 모든 자산을 선택할 수 있습니다. 여러 자산을 신속하게 관리하는 데 도움이 됩니다. 이 확인란은 AEM 인터페이스에 표시되는 자산뿐만 아니라 시나리오에 맞는 모든 자산, 즉 검색 결과를 선택합니다.

![[모두 선택] 옵션을 사용하여 한 번의 클릭으로 모든 자산 선택](assets/select-all-in-aem-assets.gif)

[모두 선택] 옵션을 사용하여 한 번의 클릭으로 모든 자산 선택

## 메타데이터 개선 사항 {#metadata-enhancements}

자산을 사용하면 [폴더 속성] 페이지에 표시되는 레이아웃 및 메타데이터를 정의하는 자산 폴더에 대한 메타데이터 스키마를 생성할 수 있습니다. 이제 폴더 메타데이터 스키마를 기존 폴더에 지정하거나 새 폴더를 생성할 때 지정할 수 있습니다. 자세한 내용은 [폴더 메타데이터 스키마](/help/assets/folder-metadata-schema.md)를 참조하십시오.

계단식 메타데이터를 지정할 때 형식에 수동으로 입력하는 대신 런타임 시 JSON 파일에서 선택 항목을 로드할 수 있습니다. 자세한 내용은 [계단식 메타데이터](/help/assets/cascading-metadata.md)를 참조하십시오.

## 보고 개선 사항 {#reporting-enhancements}

컨텐츠 조각 및 링크 공유는 지금 [자산 다운로드됨] 보고서에 포함됩니다. 자세한 정보는 [자산 보고서](/help/assets/asset-reports.md)를 참조하십시오.
