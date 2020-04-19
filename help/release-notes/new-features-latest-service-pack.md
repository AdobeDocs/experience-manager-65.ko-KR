---
title: Adobe Experience Manager 6.5 서비스 팩 4의 새로운 기능
description: Adobe Experience Manager 6.5 서비스 팩 4의 새로운 기능
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Adobe Experience Manager 6.5 서비스 팩 4의 새로운 기능 {#aem-whats-new-service-pack-4}

Adobe Experience Manager (6.5)를 사용하면 분기별 서비스 팩 릴리스를 통해 새로운 기능과 지속적으로 향상된 기능을 이용할 수 있습니다. 이 방법을 사용하면 혁신적인 기능을 손쉽게 채택할 수 있습니다.

Experience Manager 서비스 팩 4(6.5.4.0)는 중요한 업데이트입니다. 여기에는 2019년 4월 AEM 6.5 릴리스 이후 릴리스된 모든 새로운 기능, 주요 고객이 요청한 개선 사항, 성능, 안정성 및 보안 개선 사항이 포함됩니다. AEM 6.5 이상 릴리스에 서비스 팩을 설치할 수 있습니다.

이 문서에서는 최신 6.5 서비스 팩에 포함된 기능, 이전 6.5 서비스 팩에 포함된 [주요 기능](#key-features-previous-service-packs)및 Experience Manager 6.5.3.0 이후 [주요 릴리스 중 일부를](#key-features-sice-sp3)소개합니다.

## AEM Sites {#aem-sites}

### 스타일 시스템 향상

이제 향상된 스타일 시스템을 사용하여 구성 요소 대화 상자 내에서 스타일을 선택할 수 있습니다.

### 다양한 영역의 성능 개선 {#performance-improvements}

* 사이트(`contexthub.kernel.js`) 내에서 ContextHub를 로드하고 초기화하는 데 걸리는 시간이 단축되었습니다. 따라서 사이트 방문 중에 페이지 로드 속도가 빨라졌습니다.

* 경험 구성 요소를 Sites 페이지 편집기로 드래그한 후 페이지를 새로 고치는 시간이 단축되었습니다.

* **[!UICONTROL Live Copy 개요]**&#x200B;에서 Live Copy가 200개 이상인 Sites 페이지의 항목 로드 시간이 줄었습니다.

* 불완전하거나 잘못된 URL의 처리가 개선되었습니다. 그러한 URL을 사용하면 템플릿 편집기의 속도가 느려질 수 있습니다.

## AEM Assets {#aem-assets}

### Brand Portal에서 AEM Assets 구성 {#configure-assets-bp}

AEM Assets과 Brand Portal 간의 인증 채널이 변경되었습니다. 이전에는 Brand Portal이 기존 OAuth 게이트웨이를 통해 클래식 UI에 구성되었으며, 이 게이트웨이는 인증을 위해 IMS 액세스 토큰을 가져오는 데 JWT 토큰 교환을 사용합니다. 이제 AEM Assets은 Adobe I/O를 통해 Brand Portal에 구성되며, Brand Portal은 Brand Portal 임차인의 인증을 위해 IMS 토큰을 받습니다.

Brand Portal에서 AEM Assets을 구성하는 단계는 AEM 버전과 처음 구성하는 것인지 아니면 기존 구성을 업그레이드하는 것인지에 따라 다릅니다. 자세한 내용은 [Brand Portal에서 AEM Assets 구성](https://docs.adobe.com/content/help/ko-KR/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)을 참조하십시오.


### 알려진 문제 {#known-issues-bp}

* Brand Portal 사용자는 AEM 6.5.4에서 Adobe I/O로 업그레이드할 때 기여도 폴더 자산을 AEM Assets에 게시할 수 없습니다.

### 액세스 가능성 개선 {#accessibility-enhancements}

Experience Manager Assets은 다음과 같은 액세스 가능성이 개선되었습니다.

* 키보드의 화살표 키를 사용하여 확대/축소된 이미지 내에서 영역을 이동할 수 있습니다. 자세한 내용은 [키보드 키만 사용하여 자산 미리 보기](../assets/managing-assets-touch-ui.md#previewing-assets)를 참조하십시오.

* 필터 패널의 혼합 상태 확인란(중첩된 모든 확인란을 선택하지 않은 경우 첫 번째 수준의 확인란을 선택하지 않으면 나머지도 선택되지 않음)은 화면 판독기에서 읽을 수 있습니다.

* 날짜 및 시간 형식 제약 조건은 사용자가 키보드를 사용하여 날짜를 올바른 형식으로 입력할 수 있도록 날짜 필드의 필드 레이블에 제공됩니다.

   예, `On Time (MM-DD-YYYY HH:mm)`. 여기서 MM은 두 자리 형식의 월, YYYY는 연도, DD는 두 자리 형식의 날짜, HH는 24시간 군대 형식의 시간, mm은 분입니다.

* 현재 선택된 태그를 제거하기 위한 버튼의 `X` 기호가 선택한 태그의 수와 함께 화면 판독기에 표시됩니다.

## AEM 양식 {#aem-forms}

### AEM Forms 워크플로우에서 인쇄 가능한 출력 생성 {#generate-printable-output}

인쇄 가능한 출력 생성 워크플로우 단계를 통해 소스 템플릿 파일을 데이터 파일과 통합할 수 있습니다. 이 통합을 통해 템플릿 파일의 다른 복사본을 인쇄하거나 저장할 수 있습니다. 이 단계에서는 PCL, PostScript, ZPL, IPL, TPCL 또는 DPL 출력을 생성합니다. 이 기능에 대한 자세한 내용은 [OSGi의 양식 중심의 워크플로우 - 단계 참조](../forms/using/aem-forms-workflow-step-reference.md)를 참조하십시오.

![인쇄 가능한 출력 생성](assets/generate-print-output-step.gif)

### 레이아웃 모드에서 적용형 양식 및 대화형 커뮤니케이션에 대한 다중 열 지원 {#multi-column-adaptive-forms}

이제 적용형 양식 및 대화형 커뮤니케이션에서 패널의 열 수를 정의할 수 있습니다. 레이아웃 모드로 전환하여 새로운 다중 열 옵션을 사용합니다. 자세한 내용은 [레이아웃 모드를 사용하여 구성 요소의크기 조정](../forms/using/resize-using-layout-mode.md)을 참조하십시오.

![다중 열 레이아웃](assets/multi-column-layout.gif)

### AEM 받은 편지함 사용자 지정 {#aem-inbox}

관리자는 새로운 관리자 컨트롤 옵션을 사용하여 다음을 수행할 수 있습니다.

* 머리글 텍스트 및 로고 사용자 지정

* 헤더에서 사용할 수 있는 탐색 링크 표시 제어

관리자 컨트롤 옵션은 관리자 또는 워크플로 관리자 그룹의 구성원에게만 표시됩니다. 이 기능에 대한 자세한 내용은 [받은 편지함](../sites-authoring/inbox.md)을 참조하십시오.

### HTML5 양식에서 리치 텍스트 지원 {#rich-text-support}

XFA 양식의 텍스트 필드를 HTML5 양식의 리치 텍스트 필드로 변환합니다. 자세한 내용은 [HTML5 양식의 양식 템플릿 디자인](../forms/using/designing-form-template.md)을 참조하십시오.

### 액세스 가능성 개선 {#forms-accessibility-enhancements-6540}

Experience Manager Forms는 다음과 같은 액세스 가능성이 개선되었습니다.

* 화면 판독기는 적용형 양식의 확인란, 링크, 날짜 선택기 및 날짜 입력 필드가 올바른지 알려줍니다.

* 적용형 양식의 각 페이지에는 이제 제목과 기본 랜드마크 레이블이 각각 하나씩 포함되어 있습니다.

## 이전 AEM 6.5 서비스 팩의 주요 기능 {#key-features-previous-service-packs}

### Smart Imaging for Dynamic Media {#smart-imaging}

스마트 이미징은 각 사용자의 고유한 보기 특성을 사용하여 환경에 맞게 최적화된 적합한 이미지를 자동으로 제공하므로 향상된 성능과 참여를 제공합니다. 스마트 이미징은 기존 이미지 사전 설정에서 작동하며 마지막 전달 순간에 인텔리전스를 사용하여 브라우저 또는 네트워크 연결 속도에 따라 이미지 파일 크기를 더 줄입니다. [스마트 이미징](../assets/imaging-faq.md)을 참조하십시오.

### 다이내믹 미디어용 비디오 프로파일의 스마트 자르기(6.5.3.0) {#smart-crop-video}

비디오 프로파일에서 사용할 수 있는 고급 비디오 자르기(선택 사항) - Adobe Sensei의 인공 지능 기능을 사용하여 크기와 상관없이 업로드한 모든 적응형 비디오 또는 점진적 비디오에서 초점을 자동으로 감지하고 자를 수 있는 도구입니다. 비디오 [프로파일에서](../assets/video-profiles.md)스마트 자르기 사용을 참조하십시오.

### AEM Assets 시각적 검색(6.5.2.0) {#visual-search}

Assets 사용자는 시각적으로 유사한 이미지를 검색할 수 있습니다. AEM은 사용자가 선택한 이미지와 유사한 DAM 저장소에서 스마트 태그가 지정된 이미지를 표시합니다. [시각적 검색](../assets/search-assets.md)을 참조하십시오.

### AEM Forms 사용자의 받은 편지함 항목 공유 및 액세스 요청(6.5.3.0) {#share-request-access}

받은 편지함 항목을 다른 사용자와 공유할 수 있습니다. 다른 사용자가 받은 편지함 항목에 액세스할 수 있게 되면 해당 사용자는 소유권을 주장하고 공유 항목에 적절한 작업을 수행할 수 있습니다. 마찬가지로 다른 사용자의 받은 편지함 항목에 대한 액세스를 요청할 수 있습니다. [사용자의 받은 편지함 항목 공유 및 액세스 요청](../forms/using/configure-shared-queues-osgi.md)을 참조하십시오.

### AEM Forms 사용자의 받은 편지함 항목에 대한 부재 중 설정 구성(6.5.3.0) {#configure-out-of-office}

부재 예정인 경우 해당 기간 동안 자신에게 할당된 항목에 대한 처리 방법을 지정할 수 있습니다.
부재 설정을 적용할 시작 날짜 및 시간, 종료 날짜 및 시간을 지정할 수 있습니다. 모든 항목을 받을 기본 사람을 설정할 수 있습니다. [부재 설정 구성](../forms/using/configure-out-of-office-settings.md)을 참조하십시오.

### AEM Forms용 배치 API를 사용하여 여러 대화형 커뮤니케이션 생성(6.5.3.0) {#generate-multiple-ic}

배치 API를 사용하여 템플릿에서 여러 대화형 커뮤니케이션을 생성할 수 있습니다. 템플릿은 데이터가 없는 대화형 커뮤니케이션입니다. 배치 API는 데이터를 템플릿과 결합하여 대화형 커뮤니케이션을 생성합니다. API는 대량의 대화형 커뮤니케이션 제작 시 유용합니다. 예를 들면 여러 고객을 위한 전화 요금 청구서, 신용 카드 명세서 등이 있습니다. [AEM Forms용 배치 API를 사용하여 여러 대화형 커뮤니케이션 생성](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)을 참조하십시오.

## AEM 6.5 SP3 이후의 주요 릴리스 {#key-features-since-sp3}

2019년 12월 12일부터 2020년 3월 5일까지 Adobe는 코어 AEM 자료 외에 다음 기능을 발표했습니다.

* AEM Cloud Manager 2020.1.0 및 2020.2.0

   파이프라인 상태와 다양한 단계에 대한 로그 다운로드 기능을 개선합니다. 다음을 참조하십시오.

   * [Cloud Manager 2020.1.0](https://docs.adobe.com/content/help/ko-KR/experience-manager-cloud-manager/using/release-notes/release-notes-2020-1-0.html)


   * [Cloud Manager 2020.2.0](https://docs.adobe.com/content/help/ko-KR/experience-manager-cloud-manager/using/release-notes/release-notes-2020-2-0.html)


* AEM Cloud Manager CLI 업데이트

   명령줄 도구를 사용하여 Cloud Manager 작업을 자동화합니다. [GitHub](https://github.com/adobe/aio-cli-plugin-cloudmanager/releases)를 참조하십시오.

* AEM Sites: Project Archetype 23

   새 AEM 프로젝트를 시작하는 가장 좋은 방법입니다. Archetype 23은 [SPA용 Project Archetype 및 일반 사이트](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-23)를 하나로 병합하고 프런트 엔드 개발을 시작할 수 있도록 기본 테마를 제공합니다.

* AEM Sites: WKND 참조 사이트

   AEM을 사용하여 사이트를 구축하는 방법에 대한 우수 사례가 포함된 [새로운 참조 프로젝트](https://www.wknd.site/)입니다. 업데이트된 [WKND 자습서](https://helpx.adobe.com/kr/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)를 참조하여 자세히 알아보십시오. [GitHub](https://github.com/adobe/aem-guides-wknd/releases)에서 최신 코드를 가져올 수 있습니다.

* AEM Sites: Commerce CIF 코어 구성 요소 0.7.0 및 0.9.0

   AEM Sites를 Magento Commerce와 통합합니다. [상거래에 중점을 둔 전용 코어 구성 요소 및 Project Archetype 확장](https://github.com/adobe/aem-core-cif-components/releases)을 참조하십시오.

* AEM Assets: 데스크탑 앱 2.0.1.1

   [자산에 대한 데스크탑 액세스 권한 얻기](https://docs.adobe.com/content/help/ko-KR/experience-manager-desktop-app/using/release-notes.html)를 참조하십시오.

* AEM Screens: 기능 팩 202001

   AEM 내에서 직접 디지털 사이니지가 가능합니다. 최신 기능 팩으로 향상된 기능을 설치하여 [여러 미디어 플레이어에서 동기식으로 재생](https://docs.adobe.com/content/help/ko-KR/experience-manager-screens/user-guide/release-notes/release-notes-fp-202001.html)할 수 있습니다.

## 유용한 리소스

* [AEM 6.5 사용 안내서](../user-guide/home.md)

* [Adobe Experience Manager 6.5의 일반적인 릴리스 노트](release-notes.md)

* [Adobe Experience Manager 6.5의 서비스 팩 릴리스 노트](sp-release-notes.md)
