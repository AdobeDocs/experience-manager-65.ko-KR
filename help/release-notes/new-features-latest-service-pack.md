---
title: Adobe Experience Manager 6.5 서비스 팩 5의 새로운 기능
description: Adobe Experience Manager 6.5 서비스 팩 5의 새로운 기능
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: d7276f332bece4f736d92e5723d79ffc2d27e900
workflow-type: tm+mt
source-wordcount: '1849'
ht-degree: 58%

---


# Adobe Experience Manager 6.5 서비스 팩 5의 새로운 기능 {#aem-whats-new-service-pack-5}

Adobe Experience Manager 6.5 서비스 팩은 분기별로 새로운 기능, 고객의 요청에 따라 향상된 기능, 성능, 안정성 및 보안 개선 사항을 제공합니다. 분기별 가용성을 통해 새로운 기능과 혁신적인 기능을 손쉽게 이용하고 채택할 수 있습니다.

이 문서에서는 최신 6.5 서비스 팩에 포함된 기능, [이전 6.5 서비스 팩에 포함된 주요 기능](#key-features-previous-service-packs) 및 [Experience Manager 6.5.4.0 이후 주요 릴리스](#key-releases-since-last-sp) 중 일부를 소개합니다.

## Adobe Experience Manager Sites {#aem-sites}

### 액세스 가능성 향상 {#accessibility-sites}

* 텍스트 정보를 추가하여 오류 보고 개선.

* 키보드 탐색 중 유저 인터페이스 포커스가 개선되었습니다.

* 다양한 유저 인터페이스 요소의 대비 비율이 개선되었습니다.

* 페이지 이미지에 대한 대체 속성의 일관성 개선.

* ARIA(Accessible Rich Internet Applications) 레이블의 일관성 향상.

* NVDA(Non-Visual Desktop Access) 기능 개선.

* 향상된 화면 판독기 지원.

### 기타 주요 개선 사항 {#other-enhancements-sites}

* 페이지 트리를 복사하거나 붙여넣을 때 이제 루트 페이지를 붙여넣거나 루트 페이지를 트리의 하위 페이지와 함께 붙여넣을 수 있습니다.

* [!DNL Adobe Experience Manager Experience Fragments] 이제 작업 [!DNL Adobe Target] 영역으로 내보내면 고유한 오퍼 유형과 오퍼 소스로 표시됩니다 [!DNL Target].

* 다중 사이트 관리자 - 이제 구성 요소가 소스 페이지에서 삭제된 경우 게시된 페이지에서 구성 요소가 삭제됩니다.

* Multi Site Manager - When the name of a local component in a [!UICONTROL Live Copy] is identical to the name of a component in the blueprint and the component is rolled out from the blueprint, then the term `_msm_moved` is now added to the name of the local component.

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

### Accessibility enhancements in [!DNL Assets] {#assets-accessibility}

[!DNL Experience Manager Assets] 는 이제 WCAG(Web Content Accessibility Guidelines)를 준수하여 보다 쉽게 액세스할 수 있습니다. 다음 개선 사항으로 인해 액세서빌러티가 개선되었습니다.

* 많은 유저 인터페이스 요소, 컨트롤, 페이지 및 대화 상자는 화면 판독기에 적합합니다.

* 키보드를 사용하여 많은 유저 인터페이스 요소, 컨트롤 및 입력 양식 필드에 액세스할 수 있습니다.

* 일부 사용자 인터페이스 요소의 색상 및 대비가 업데이트되어 시력이 제한된 사용자 또는 색상에 대한 인식이 없는 사용자가 이러한 사용자 인터페이스 요소를 구분할 수 있습니다. 예를 들어 별 등급 아이콘 색상(예: 자산 [!UICONTROL 속성] 또는 카드 보기에서 [!UICONTROL 고급] 탭 의 [!UICONTROL 등급] 섹션)이 적절한 대비를 위해 변경되었습니다.

   ![향상된 대비 등급 아이콘](assets/star-rating-icons.png)

### Enhanced exception handling {#exception-handling}

[!DNL Assets] 사용자 인터페이스 흐름의 예외 처리가 향상되었습니다. 자산에 차원에 대한 유형이 없는 경우, 관찰된 예외가 로그 파일에 기록됩니다.

### 3D 자산 지원 [!DNL Dynamic Media] {#support-for-3d}

Support for 3D images in [!DNL Dynamic Media] enables customers to publish and add 3D content to web pages and applications. 지원에는 다음이 포함됩니다.

* 일반적인 3D 자산 형식을 게시하고 웹 페이지 및 기타 애플리케이션에서 사용할 수 있는 자산 URL을 생성합니다.

* 게시된 3D 에셋을 대화식으로 볼 수 있는 3D Web Viewer [!DNL Adobe Dimension]를 기반으로 합니다.

* WCM 구성 요소를 사용하여 [!DNL Experience Manager Sites] 페이지에서 일반적인 3D 자산을 [!DNL Sites] 게시하고 볼 수 있습니다.

## Adobe Experience Manager Forms {#aem-forms}

### Adobe Experience Manager 받은 편지함 열 사용자 지정 {#customize-aem-inbox-columns}

You can customize an [!DNL Experience Manager] Inbox to change the default title of a column, reorder the position of a column, and display additional columns based on the data of a workflow. 또는 그룹 `administrators` 의 `workflow-administrators` 구성원은 열을 사용자 지정할 수 있습니다.

![Experience Manager 받은 편지함 열 사용자 정의](assets/customize-columns.gif)

### 대화형 커뮤니케이션을 초안으로 저장 {#save-as-draft}

에이전트 UI를 사용하여 각 대화형 커뮤니케이션에 대해 하나 이상의 초안을 저장하고 나중에 초안을 검색하여 계속 작업할 수 있습니다. 각 초안의 다른 이름을 지정하여 해당 초안을 식별할 수 있습니다.

![초안으로 저장](assets/save-as-draft.gif)

### [!DNL Oracle WebLogic] 애플리케이션 서버 지원 {#weblogic-support}

Adobe Experience Manager 양식에 대한 지원이 JEE에서 [!DNL Oracle WebLogic 12] 추가되었습니다. You can upgrade from a previous version or set up a new Experience Manager 6.5 Forms on JEE server on [!DNL Oracle WebLogic] 12.2.1.4 and later. 이후에 버전이 약간 변경되었으며, 여기서 12.2.1.x의 x는 버전 번호로 대체됩니다.

### 액세스 가능성 향상 {#accessibility-improvements}

Adobe Experience Manager 양식에는 다음과 같은 액세서빌러티 개선 사항이 포함됩니다.

* 사용자가 적응형 양식을 HTML 양식으로 미리 보면 [!UICONTROL 스크리블 서명] 필드에 탭 포커스가 유지됩니다.

* The error messages displayed on submitting an adaptive form now contain the `aria-describedBy` attribute. 이 속성은 오류 메시지에서 참조되는 필드에 첨부됩니다. `aria-describedby` 속성은 개체를 설명하는 요소의 ID를 나타냅니다. 위젯 또는 그룹과 이를 설명하는 텍스트 간의 관계를 설정하는 데 도움이 됩니다.

* 적응형 양식에 필수 필드가 있으면 ARIA 액세스 가능성 스키마의 해당 필드에 대해 필수 속성이 `True`로 설정됩니다.

### 양식 데이터 모델 {#x509-based-authentication-soap}에서 SOAP 기반 웹 서비스를 위한 X-509 인증서 기반 인증

이제 양식 데이터 모델은 SOAP 웹 서비스를 데이터 소스로 사용하면서 X-509 인증서 기반 인증을 지원합니다.

### 기타 주요 개선 사항 {#other-improvements}

* Experience Manager 6.5 Forms on JEE Document Security is now based on [!DNL Apache Struts 2].

* [!DNL Oracle Real Applications Cluster (RAC) 19c]에 대한 지원이 추가되었습니다.

## Key features in previous Experience Manager 6.5 Service Packs {#key-features-previous-service-packs}

### Experience Manager Sites {#aem-sites-previous-service-packs}

#### Style System enhancements (6.5.4.0) {#style-system-enhancements}

이제 향상된 스타일 시스템을 사용하여 구성 요소 대화 상자 내에서 스타일을 선택할 수 있습니다.

#### 다양한 영역의 성능 개선(6.5.4.0) {#performance-improvements}

* 사이트(`contexthub.kernel.js`) 내에서 ContextHub를 로드하고 초기화하는 데 걸리는 시간이 줄었습니다. 따라서 사이트 방문 중에 페이지 로드 속도가 빨라졌습니다.

* Reduced the time to refresh a page after dragging [!DNL Experience Fragments] to [!DNL Sites] Page Editor.

* Shortened the load time for entries on a [!DNL Sites] page with more than 200 live copies in **[!UICONTROL Live Copy Overview]**.

* 불완전하거나 잘못된 URL의 처리가 개선되었습니다. 이러한 URL을 사용하면 템플릿 편집기의 속도가 느려질 수 있습니다.

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

#### 구성 [!DNL Experience Manager Assets] ( [!DNL Brand Portal] 6.5.4.0) {#configure-assets-bp}

에서 사이의 인증 채널 [!DNL Experience Manager Assets] 이 [!DNL Brand Portal] 변경되었습니다. Earlier, [!DNL Brand Portal] was configured in Classic UI via Legacy OAuth Gateway, which uses the JWT token exchange to obtain an IMS Access token for authorization. [!DNL Experience Manager Assets] 이제 Adobe I/O를 [!DNL Brand Portal] 통해 임차인 인증을 위해 IMS 토큰을 조달합니다 [!DNL Brand Portal] .

The steps to configure [!DNL Experience Manager Assets] with [!DNL Brand Portal] are different depending on your [!DNL Experience Manager] version, and whether you are configuring for the first time, or upgrading the existing configurations. See [Configure Experience Manager Assets with Brand Portal](https://docs.adobe.com/content/help/ko-KR/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) for details.

#### 액세스 가능성 개선(6.5.4.0) {#accessibility-enhancements}

[!DNL Experience Manager Assets] 에는 다음과 같은 액세서빌러티 개선 사항이 포함됩니다.

* 키보드의 화살표 키를 사용하여 확대/축소된 이미지 내에서 영역을 이동할 수 있습니다. 자세한 내용은 [키보드 키만 사용하여 자산 미리 보기](../assets/managing-assets-touch-ui.md#previewing-assets)를 참조하십시오.

* 필터 패널의 혼합 상태 확인란(중첩된 모든 확인란을 선택하지 않은 경우 첫 번째 수준의 확인란을 선택하지 않으면 나머지도 선택되지 않음)은 화면 판독기에서 읽을 수 있습니다.

* 날짜 및 시간 형식 제약 조건은 사용자가 키보드를 사용하여 날짜를 올바른 형식으로 입력할 수 있도록 날짜 필드의 필드 레이블에 제공됩니다.
예, `On Time (MM-DD-YYYY HH:mm)`. 여기서 MM은 두 자리 형식의 월, YYYY는 연도, DD는 두 자리 형식의 날짜, HH는 24시간 군대 형식의 시간, mm은 분입니다.

* 이제 화면 판독기에서 선택한 태그의 수와 함께 선택한 태그를 제거할 `X` 기호를 발표합니다.

#### Visual search for [!DNL Adobe Experience Manager Assets] (6.5.2.0) {#visual-search}

[!DNL Assets] 사용자는 시각적으로 유사한 이미지를 검색할 수 있습니다. Experience Manager은 사용자가 선택한 이미지와 유사한 DAM 저장소의 스마트 태그 이미지를 표시합니다. [시각적 검색](../assets/search-assets.md)을 참조하십시오.

### Dynamic Media {#dynamic-media-previous-service-packs}

#### Dynamic Media용 스마트 이미징 {#smart-imaging}

스마트 이미징은 각 사용자의 고유한 보기 특성을 사용하여 환경에 맞게 최적화된 적합한 이미지를 자동으로 제공하므로 향상된 성능과 참여를 제공합니다. 스마트 이미징은 기존 이미지 사전 설정에서 작동하며 마지막 전달 순간에 인텔리전스를 사용하여 브라우저 또는 네트워크 연결 속도에 따라 이미지 파일 크기를 더 줄입니다. [스마트 이미징](../assets/imaging-faq.md)을 참조하십시오.

#### Dynamic Media용 비디오 프로필에서 스마트 자르기(6.5.3.0) {#smart-crop-video}

비디오 프로필에서 사용할 수 있는 선택적 기능인 비디오 스마트 자르기는 Adobe Sensei의 인공 지능 기능을 사용하여 크기와 상관없이 업로드한 모든 적응형 비디오 또는 점진적 비디오에서 초점을 자동으로 감지하고 자르는 도구입니다. [비디오 프로필에서 스마트 자르기 사용 정보](../assets/video-profiles.md)를 참조하십시오.

### Experience Manager Forms {#aem-forms-previous-service-packs}

#### Generate printable output in Experience Manager Forms workflows (6.5.4.0) {#generate-printable-output}

인쇄 가능한 출력 생성 워크플로우 단계를 통해 소스 템플릿 파일을 데이터 파일과 통합할 수 있습니다. 이 통합을 통해 템플릿 파일의 다른 복사본을 인쇄하거나 저장할 수 있습니다. 이 단계에서는 PCL, PostScript, ZPL, IPL, TPCL 또는 DPL 출력을 생성합니다. 이 기능에 대한 자세한 내용은 [OSGi의 양식 중심의 워크플로우 - 단계 참조](../forms/using/aem-forms-workflow-step-reference.md)를 참조하십시오.

![인쇄 가능한 출력 생성](assets/generate-print-output-step.gif)

#### Multi-column support for adaptive forms and interactive communications in Layout mode (6.5.4.0) {#multi-column-adaptive-forms}

이제 적용형 양식 및 대화형 커뮤니케이션에서 패널의 열 수를 정의할 수 있습니다. 레이아웃 모드로 전환하여 새로운 다중 열 옵션을 사용합니다. 자세한 내용은 [레이아웃 모드를 사용하여 구성 요소의크기 조정](../forms/using/resize-using-layout-mode.md)을 참조하십시오.

![다중 열 레이아웃](assets/multi-column-layout.gif)

#### Experience Manager 받은 편지함 사용자 지정(6.5.4.0) {#aem-inbox}

관리자는 새로운 관리자 컨트롤 옵션을 사용하여 다음을 수행할 수 있습니다.

* 머리글 텍스트 및 로고 사용자 지정.

* 헤더에서 사용할 수 있는 탐색 링크 표시 제어.

The Admin Control option is visible only to the members of the `administrators` or `workflow-administrators` group. 이 기능에 대한 자세한 내용은 [받은 편지함](../sites-authoring/inbox.md)을 참조하십시오.

#### HTML5 양식에서 리치 텍스트 지원(6.5.4.0) {#rich-text-support}

XFA 양식의 텍스트 필드를 HTML5 양식의 리치 텍스트 필드로 변환합니다. 자세한 내용은 [HTML5 양식의 양식 템플릿 디자인](../forms/using/designing-form-template.md)을 참조하십시오.

#### 액세스 가능성 개선(6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience Manager Forms는 다음과 같은 액세스 가능성이 개선되었습니다.

* 화면 판독기는 적용형 양식의 확인란, 링크, 날짜 선택기 및 날짜 입력 필드가 올바른지 알려줍니다.

* 적용형 양식의 각 페이지에는 이제 제목과 기본 랜드마크 레이블이 각각 하나씩 포함되어 있습니다.

#### Share and request access to Inbox items of an Experience Manager Forms user (6.5.3.0) {#share-request-access}

받은 편지함 항목을 다른 사용자와 공유할 수 있습니다. 다른 사용자가 받은 편지함 항목에 액세스할 수 있게 되면 해당 사용자는 소유권을 주장하고 공유 항목에 적절한 작업을 수행할 수 있습니다. 마찬가지로 다른 사용자의 받은 편지함 항목에 대한 액세스를 요청할 수 있습니다. [사용자의 받은 편지함 항목 공유 및 액세스 요청](../forms/using/configure-shared-queues-osgi.md)을 참조하십시오.

#### AEM Forms 사용자의 받은 편지함 항목에 대한 부재 중 설정 구성(6.5.3.0) {#configure-out-of-office}

부재 예정인 경우 해당 기간 동안 자신에게 할당된 항목에 대한 처리 방법을 지정할 수 있습니다.
부재 설정을 적용할 시작 날짜 및 시간, 종료 날짜 및 시간을 지정할 수 있습니다. 모든 항목을 받을 기본 사람을 설정할 수 있습니다. [부재 설정 구성](../forms/using/configure-out-of-office-settings.md)을 참조하십시오.

#### AEM Forms용 배치 API를 사용하여 여러 대화형 커뮤니케이션 생성(6.5.3.0) {#generate-multiple-ic}

배치 API를 사용하여 템플릿에서 여러 대화형 커뮤니케이션을 생성할 수 있습니다. 템플릿은 데이터가 없는 대화형 커뮤니케이션입니다. 배치 API는 데이터를 템플릿과 결합하여 대화형 커뮤니케이션을 생성합니다. API는 대량의 대화형 커뮤니케이션 제작 시 유용합니다. 예를 들면 여러 고객을 위한 전화 요금 청구서, 신용 카드 명세서 등이 있습니다. [AEM Forms용 배치 API를 사용하여 여러 대화형 커뮤니케이션 생성](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)을 참조하십시오.

## Adobe Experience Manager 6.5 SP4 이후 주요 릴리스 {#key-releases-since-last-sp}

2020년 3월 5일부터 2020년 6월 4일까지 Adobe는 서비스 팩 및 누적 수정 팩 외에 다음과 같은 내용을 발표했습니다.

* [소프트웨어 배포 포털은](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) Experience Manager 서비스 팩, 누적 수정 팩, 핫픽스 및 기능 팩을 다운로드할 수 있습니다.

* [!DNL Adobe Experience Manager Cloud Manager] [2020.3.0](https://docs.adobe.com/content/help/ko-KR/experience-manager-cloud-manager/using/release-notes/release-notes-2020-3-0.html), [2020.4.0](https://docs.adobe.com/content/help/ko-KR/experience-manager-cloud-manager/using/release-notes/release-notes-2020-4-0.html)및 [2020.5.0](https://docs.adobe.com/content/help/ko-KR/experience-manager-cloud-manager/using/release-notes/release-notes-current.html).

* [Experience Manager 데스크탑 앱 2.0.2.0](https://docs.adobe.com/content/help/ko-KR/experience-manager-desktop-app/using/release-notes.html).

* [Experience Manager 스크린: Feature Pack 202004](https://docs.adobe.com/content/help/ko-KR/experience-manager-screens/user-guide/release-notes/release-notes-fp-202004.html).

>[!MORELIKETHIS]
>
>* [Adobe Experience Manager 6.5 설명서](../user-guide/home.md)
>* [Adobe Experience Manager 6.5에 대한 일반 릴리스 노트](release-notes.md)
>* [Adobe Experience Manager 6.5용 서비스 팩 릴리스 노트](sp-release-notes.md)

