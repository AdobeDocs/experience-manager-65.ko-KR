---
title: Adobe Experience Manager 6.5 서비스 팩 5의 새로운 기능
description: Adobe Experience Manager 6.5 서비스 팩 5의 새로운 기능
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: cc423a199e860429e85895690f6c1a81c20d1a19
workflow-type: tm+mt
source-wordcount: '1854'
ht-degree: 56%

---


# AEM 6.5 서비스 팩 5의 새로운 기능 {#aem-whats-new-service-pack-5}

Adobe Experience Manager 6.5 서비스 팩은 분기별로 새로운 기능, 고객의 요구 사항을 반영한 개선 사항, 성능 및 안정성 관련 개선 사항을 제공합니다. 분기별 전달 모델을 통해 새로운 기능과 혁신적인 기능을 손쉽게 이용하고 채택할 수 있습니다.

This article highlights the features included in the latest 6.5 Service Pack, [key features included in the previous 6.5 Service Packs](#key-features-previous-service-packs), and some of the [key releases since Experience Manager 6.5.4.0](#key-features-sice-sp3) release.

## AEM Sites {#aem-sites}

### 향상된 접근성 {#accessibility-sites}

* 텍스트 정보를 추가하여 오류 보고 개선

* 키보드 탐색 시 향상된 UI 포커스

* 향상된 텍스트 대비(광도 비율)

* 페이지 이미지에 대한 대체 속성의 일관성 개선

* 액세스 가능한 ARIA(Rich Internet Application) 레이블의 향상된 일관성

* 향상된 NVDA(Non-Visual Desktop Access) 기능

* 향상된 화면 판독기 지원

### 기타 주요 개선 사항 {#other-enhancements-sites}

* 페이지 트리를 복사하거나 붙여넣을 때 루트 페이지를 붙여넣거나 루트 페이지를 트리의 하위 페이지에 붙여넣을 수 있습니다.

* AEM Experience Fragments exported to Adobe Target workspaces now appear as unique offer types and offer sources in [!DNL Target].

* 다중 사이트 관리자 - 이제 구성 요소가 소스 페이지에서 삭제되는 경우 게시 트리거가 게시된 페이지에서 구성 요소를 삭제합니다.

* 다중 사이트 관리자 - LiveCopy의 로컬 구성 요소의 이름이 블루프린트에서 구성 요소의 이름과 동일하고 구성 요소가 블루프린트에서 롤아웃되면, 이제 _msm_moved 용어가 로컬 구성 요소의 이름에 성공적으로 추가됩니다.

## AEM Assets {#aem-assets}

### Accessibility enhancements in Assets {#assets-accessibility}

[!DNL Adobe Experience Manager] 이제 WCAG(Web Content Accessibility Guidelines)를 준수하여 에셋 기능에 더 쉽게 액세스할 수 있습니다. 다음 영역에서 액세서빌러티가 개선되었습니다.

* 화면 판독기에 최적화된 유저 인터페이스 요소, 컨트롤, 페이지 및 대화 상자

* 사용자 인터페이스 요소, 컨트롤 및 입력 양식 필드는 키보드를 사용하여 액세스할 수 있습니다.

* 일부 그래픽의 색상 및 대비를 변경하여 시각 기능이 제한적이고 색상에 대한 인식 없이도 사용자가 구별할 수 있습니다. 예를 들어, 별 등급 아이콘 색상(예: 자산 [!UICONTROL 속성] 또는 카드 보기에서 [!UICONTROL 고급] 탭 [!UICONTROL 의 등급] 섹션에서)이 적절한 대비를 위해 변경되었습니다.

![대비를 개선하기 위해 별점 등급 아이콘 색상 변경](assets/star-rating-icons.png)

### 향상된 예외 처리 {#exception-handling}

자산 사용자 인터페이스 흐름의 예외 처리가 향상되었습니다. 이전에는 자산에 차원에 대한 적절한 유형이 없는 경우, 로그에 추적이 없는 상태로 자동 잡힌 예외가 관찰되었습니다. 이 동작이 변경되었으며 모든 예외가 로그에 표시됩니다.

## [!DNL Dynamic Media] {#dynamic-media}

### 3D 지원 [!DNL Dynamic Media] {#support-for-3d}

3D 지원 [!DNL Dynamic Media] 을 통해 고객은 웹 페이지 및 애플리케이션에 3D 컨텐츠를 게시하고 추가할 수 있습니다. 여기에는 다음이 포함됩니다.

* 일반적인 3D 자산 형식 게시로 자산 URL을 생성합니다.

* Adobe Dimension을 기반으로 한 뷰어 라이브러리에서 사용할 수 있는 새로운 3D Web Viewer를 사용하여 게시된 3D 자산에 대한 대화형 [!DNL Dynamic Media] 보기

* WCM 구성 요소를 사용하여 [!DNL Experience Manager Sites] 페이지에서 3D 게시 및 [!DNL Sites] 보기

## AEM Forms {#aem-forms}

### AEM 받은 편지함 열 사용자 정의 {#customize-aem-inbox-columns}

AEM 받은 편지함을 사용자 지정하여 열의 기본 제목을 변경하고, 열의 위치를 다시 정렬하고, 워크플로우의 데이터를 기반으로 추가 열을 표시할 수 있습니다. 열을 사용자 지정할 수 있는 `administrators` 또는 `workflow-administrators` 그룹의 구성원이어야 합니다.

![AEM 받은 편지함 열 사용자 지정](assets/customize-columns.gif)

### Interactive Communications를 초안으로 저장 {#save-as-draft}

에이전트 UI를 사용하여 각 대화형 통신에 대해 하나 이상의 초안을 저장하고 나중에 초안을 검색하여 계속 작업할 수 있습니다. 보다 쉽게 식별할 수 있도록 각 초안에 다른 이름을 지정할 수 있습니다.

![초안으로 저장](assets/save-as-draft.gif)

### [!DNL Oracle WebLogic] 응용 프로그램 서버 지원 {#weblogic-support}

JEE에서 AEM Forms [!DNL Oracle WebLogic 12] 에 대한 지원이 추가되었습니다. 이전 버전에서 업그레이드하거나 [!DNL Oracle WebLogic] 12.2.1.4 이상에서 새 AEM 6.5 양식을 설정할 수 있습니다. 이후 버전은 약간 변경되었으며, 여기서 12.2.1.x의 x는 버전 번호로 대체됩니다.

### 향상된 접근성 {#accessibility-improvements}

AEM Forms에는 다음과 같은 액세서빌러티 개선 사항이 포함됩니다.

* 사용자가 적응형 양식을 HTML 양식으로 미리 보면 [!UICONTROL 문지르기 서명] 필드가 탭 포커스를 유지합니다.

* 이제 응용 양식 제출 시 표시되는 오류 메시지에 속성이 `aria-describedBy` 포함됩니다. 이 속성은 오류 메시지에서 참조되는 필드에 연결됩니다. 이 `aria-describedby` 속성은 개체를 설명하는 요소의 ID를 나타냅니다. 위젯 또는 그룹과 이를 설명하는 텍스트 간의 관계를 설정하는 데 도움이 됩니다.

* 응용 양식에 필수 필드가 있으면 ARIA 액세스 가능성 스키마의 해당 필드에 대해 필수 속성 `True` 이 설정됩니다.

### 양식 데이터 모델에서 SOAP 기반 웹 서비스를 위한 X-509 인증서 기반 인증 {#x509-based-authentication-soap}

이제 양식 데이터 모델은 SOAP 웹 서비스를 데이터 소스로 사용하면서 X-509 인증서 기반 인증을 지원합니다.

### 기타 주요 개선 사항 {#other-improvements}

* JEE Document Security의 AEM 6.5 양식은 이제 기반으로 합니다 [!DNL Apache Struts 2].

* 에 대한 지원이 [!DNL Oracle Real Applications Cluster (RAC) 19c]추가되었습니다.

## 이전 AEM 6.5 서비스 팩의 주요 기능 {#key-features-previous-service-packs}

### AEM Sites {#aem-sites-previous-service-packs}

#### 스타일 시스템 향상 (6.5.4.0) {#style-system-enhancements}

이제 향상된 스타일 시스템을 사용하여 구성 요소 대화 상자 내에서 스타일을 선택할 수 있습니다.

#### Performance improvements in various areas (6.5.4.0) {#performance-improvements}

* 사이트(`contexthub.kernel.js`) 내에서 ContextHub를 로드하고 초기화하는 데 걸리는 시간이 단축되었습니다. 따라서 사이트 방문 중에 페이지 로드 속도가 빨라졌습니다.

* 경험 구성 요소를 Sites 페이지 편집기로 드래그한 후 페이지를 새로 고치는 시간이 단축되었습니다.

* **[!UICONTROL Live Copy 개요]**&#x200B;에서 Live Copy가 200개 이상인 Sites 페이지의 항목 로드 시간이 줄었습니다.

* 불완전하거나 잘못된 URL의 처리가 개선되었습니다. 그러한 URL을 사용하면 템플릿 편집기의 속도가 느려질 수 있습니다.

### AEM Assets {#aem-assets-previous-service-packs}

#### Configure AEM Assets with Brand Portal (6.5.4.0) {#configure-assets-bp}

AEM Assets과 Brand Portal 간의 인증 채널이 변경되었습니다. 이전에는 Brand Portal이 기존 OAuth 게이트웨이를 통해 클래식 UI에 구성되었으며, 이 게이트웨이는 인증을 위해 IMS 액세스 토큰을 가져오는 데 JWT 토큰 교환을 사용합니다. 이제 AEM Assets은 Adobe I/O를 통해 Brand Portal에 구성되며, Brand Portal은 Brand Portal 임차인의 인증을 위해 IMS 토큰을 받습니다.

Brand Portal에서 AEM Assets을 구성하는 단계는 AEM 버전과 처음 구성하는 것인지 아니면 기존 구성을 업그레이드하는 것인지에 따라 다릅니다. 자세한 내용은 [Brand Portal에서 AEM Assets 구성](https://docs.adobe.com/content/help/ko-KR/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)을 참조하십시오.

#### Accessibility enhancements (6.5.4.0) {#accessibility-enhancements}

Experience Manager Assets은 다음과 같은 액세스 가능성이 개선되었습니다.

* 키보드의 화살표 키를 사용하여 확대/축소된 이미지 내에서 영역을 이동할 수 있습니다. 자세한 내용은 [키보드 키만 사용하여 자산 미리 보기](../assets/managing-assets-touch-ui.md#previewing-assets)를 참조하십시오.

* 필터 패널의 혼합 상태 확인란(중첩된 모든 확인란을 선택하지 않은 경우 첫 번째 수준의 확인란을 선택하지 않으면 나머지도 선택되지 않음)은 화면 판독기에서 읽을 수 있습니다.

* 날짜 및 시간 형식 제약 조건은 사용자가 키보드를 사용하여 날짜를 올바른 형식으로 입력할 수 있도록 날짜 필드의 필드 레이블에 제공됩니다.

   예, `On Time (MM-DD-YYYY HH:mm)`. 여기서 MM은 두 자리 형식의 월, YYYY는 연도, DD는 두 자리 형식의 날짜, HH는 24시간 군대 형식의 시간, mm은 분입니다.

* 현재 선택된 태그를 제거하기 위한 버튼의 `X` 기호가 선택한 태그의 수와 함께 화면 판독기에 표시됩니다.

#### AEM Assets 시각적 검색(6.5.2.0) {#visual-search}

Assets 사용자는 시각적으로 유사한 이미지를 검색할 수 있습니다. AEM은 사용자가 선택한 이미지와 유사한 DAM 저장소에서 스마트 태그가 지정된 이미지를 표시합니다. [시각적 검색](../assets/search-assets.md)을 참조하십시오.

### Dynamic Media {#dynamic-media-previous-service-packs}

#### Dynamic Media용 스마트 이미징 {#smart-imaging}

스마트 이미징은 각 사용자의 고유한 보기 특성을 사용하여 환경에 맞게 최적화된 적합한 이미지를 자동으로 제공하므로 향상된 성능과 참여를 제공합니다. 스마트 이미징은 기존 이미지 사전 설정에서 작동하며 마지막 전달 순간에 인텔리전스를 사용하여 브라우저 또는 네트워크 연결 속도에 따라 이미지 파일 크기를 더 줄입니다. [스마트 이미징](../assets/imaging-faq.md)을 참조하십시오.

#### Dynamic Media용 비디오 프로필에서 스마트 자르기(6.5.3.0) {#smart-crop-video}

비디오 프로필에서 사용할 수 있는 선택적 기능인 비디오 스마트 자르기는 Adobe Sensei의 인공 지능 기능을 사용하여 크기와 상관없이 업로드한 모든 적응형 비디오 또는 점진적 비디오에서 초점을 자동으로 감지하고 자르는 도구입니다. [비디오 프로필에서 스마트 자르기 사용 정보](../assets/video-profiles.md)를 참조하십시오.

### AEM Forms {#aem-forms-previous-service-packs}

#### Generate printable output in AEM Forms workflows (6.5.4.0) {#generate-printable-output}

인쇄 가능한 출력 생성 워크플로우 단계를 통해 소스 템플릿 파일을 데이터 파일과 통합할 수 있습니다. 이 통합을 통해 템플릿 파일의 다른 복사본을 인쇄하거나 저장할 수 있습니다. 이 단계에서는 PCL, PostScript, ZPL, IPL, TPCL 또는 DPL 출력을 생성합니다. 이 기능에 대한 자세한 내용은 [OSGi의 양식 중심의 워크플로우 - 단계 참조](../forms/using/aem-forms-workflow-step-reference.md)를 참조하십시오.

![인쇄 가능한 출력 생성](assets/generate-print-output-step.gif)

#### Multicolumn support for adaptive forms and interactive communications in Layout mode (6.5.4.0) {#multi-column-adaptive-forms}

이제 적용형 양식 및 대화형 커뮤니케이션에서 패널의 열 수를 정의할 수 있습니다. 레이아웃 모드로 전환하여 새로운 다중 열 옵션을 사용합니다. 자세한 내용은 [레이아웃 모드를 사용하여 구성 요소의크기 조정](../forms/using/resize-using-layout-mode.md)을 참조하십시오.

![다중 열 레이아웃](assets/multi-column-layout.gif)

#### AEM Inbox customizations (6.5.4.0) {#aem-inbox}

관리자는 새로운 관리자 컨트롤 옵션을 사용하여 다음을 수행할 수 있습니다.

* 머리글 텍스트 및 로고 사용자 지정

* 헤더에서 사용할 수 있는 탐색 링크 표시 제어

관리자 컨트롤 옵션은 관리자 또는 워크플로 관리자 그룹의 구성원에게만 표시됩니다. 이 기능에 대한 자세한 내용은 [받은 편지함](../sites-authoring/inbox.md)을 참조하십시오.

#### Rich text support in HTML5 forms (6.5.4.0) {#rich-text-support}

XFA 양식의 텍스트 필드를 HTML5 양식의 리치 텍스트 필드로 변환합니다. 자세한 내용은 [HTML5 양식의 양식 템플릿 디자인](../forms/using/designing-form-template.md)을 참조하십시오.

#### Accessibility enhancements (6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience Manager Forms는 다음과 같은 액세스 가능성이 개선되었습니다.

* 화면 판독기는 적용형 양식의 확인란, 링크, 날짜 선택기 및 날짜 입력 필드가 올바른지 알려줍니다.

* 적용형 양식의 각 페이지에는 이제 제목과 기본 랜드마크 레이블이 각각 하나씩 포함되어 있습니다.

#### AEM Forms 사용자의 받은 편지함 항목 공유 및 액세스 요청(6.5.3.0) {#share-request-access}

받은 편지함 항목을 다른 사용자와 공유할 수 있습니다. 다른 사용자가 받은 편지함 항목에 액세스할 수 있게 되면 해당 사용자는 소유권을 주장하고 공유 항목에 적절한 작업을 수행할 수 있습니다. 마찬가지로 다른 사용자의 받은 편지함 항목에 대한 액세스를 요청할 수 있습니다. [사용자의 받은 편지함 항목 공유 및 액세스 요청](../forms/using/configure-shared-queues-osgi.md)을 참조하십시오.

#### AEM Forms 사용자의 받은 편지함 항목에 대한 부재 중 설정 구성(6.5.3.0) {#configure-out-of-office}

부재 예정인 경우 해당 기간 동안 자신에게 할당된 항목에 대한 처리 방법을 지정할 수 있습니다.
부재 설정을 적용할 시작 날짜 및 시간, 종료 날짜 및 시간을 지정할 수 있습니다. 모든 항목을 받을 기본 사람을 설정할 수 있습니다. [부재 설정 구성](../forms/using/configure-out-of-office-settings.md)을 참조하십시오.

#### AEM Forms용 배치 API를 사용하여 여러 대화형 커뮤니케이션 생성(6.5.3.0) {#generate-multiple-ic}

배치 API를 사용하여 템플릿에서 여러 대화형 커뮤니케이션을 생성할 수 있습니다. 템플릿은 데이터가 없는 대화형 커뮤니케이션입니다. 배치 API는 데이터를 템플릿과 결합하여 대화형 커뮤니케이션을 생성합니다. API는 대량의 대화형 커뮤니케이션 제작 시 유용합니다. 예를 들면 여러 고객을 위한 전화 요금 청구서, 신용 카드 명세서 등이 있습니다. [AEM Forms용 배치 API를 사용하여 여러 대화형 커뮤니케이션 생성](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)을 참조하십시오.

## AEM 6.5 SP4 이후의 주요 릴리스 {#key-releases-since-last-sp}

Adobe는 2020년 3월 5일부터 2020년 6월 4일까지 핵심 AEM 제공 서비스 외부에 있는 다음 기능을 발표했습니다.

* AEM Cloud Manager [2020.3.0](https://docs.adobe.com/content/help/ko-KR/experience-manager-cloud-manager/using/release-notes/release-notes-2020-3-0.html), [2020.4.0](https://docs.adobe.com/content/help/ko-KR/experience-manager-cloud-manager/using/release-notes/release-notes-2020-4-0.html), and [2020.5.0](https://docs.adobe.com/content/help/ko-KR/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)

* [AEM Assets: 데스크탑 앱 2.0.2.0](https://docs.adobe.com/content/help/ko-KR/experience-manager-desktop-app/using/release-notes.html)

* [AEM Screens: 기능 팩 202004](https://docs.adobe.com/content/help/ko-KR/experience-manager-screens/user-guide/release-notes/release-notes-fp-202004.html)

## 유용한 리소스

* [AEM 6.5 사용 안내서](../user-guide/home.md)

* [Adobe Experience Manager 6.5의 일반적인 릴리스 노트](release-notes.md)

* [Adobe Experience Manager 6.5의 서비스 팩 릴리스 노트](sp-release-notes.md)
