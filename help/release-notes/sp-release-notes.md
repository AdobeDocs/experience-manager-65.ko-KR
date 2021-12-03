---
title: '[!DNL Experience Manager] 6.5 서비스 팩 릴리스 노트'
description: 에 관한 릴리스 노트 [!DNL Adobe Experience Manager] 6.5 서비스 팩 11
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: c7fdfeae785ad044437d065a8da6bdcbaf00d4c4
workflow-type: tm+mt
source-wordcount: '3674'
ht-degree: 11%

---

# [!DNL Adobe Experience Manager] 6.5 서비스 팩 릴리스 노트 {#aem-service-pack-release-notes}

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 버전 | 6.5.11.0 |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2021년 11월 25일 |
| 다운로드 URL | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip) |

## 에 포함된 사항 [!DNL Adobe Experience Manager] 6.5.11.0 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.11.0에는 2019년 4월 6.5 릴리스의 공식 출시 이후 릴리스된 새로운 기능, 주요 고객이 요청한 향상된 기능 및 성능, 안정성, 보안 개선 사항이 포함됩니다. 서비스 팩이 [!DNL Adobe Experience Manager] 6.5.

에 도입된 주요 기능 및 개선 사항 [!DNL Adobe Experience Manager] 6.5.11.0:

* 여러 줄 텍스트 데이터 유형에 대한 다중 필드 지원이 추가되었습니다.

* 사용자가 동일한 경로에서 여러 비동기 작업을 트리거하지 않도록 백그라운드에서 현재 실행 중인 비동기 작업을 인식하도록 개선 사항.

* SEO용으로 사이트맵을 자동으로 생성하는 방법은 [SEO 인덱스 패키지](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/sites-seo-index-content-1.0.0.zip). 에서는 사이트 맵, 대체 URL, 로봇 메타 태그 등을 [!DNL Core Components].

* 사용자 경험 개선 사항은 폴더에 있는 자산 수를 표시합니다. 폴더에 있는 1000개 이상의 자산의 경우, [!DNL Assets] 1000 이상을 표시합니다.

* 이제 카드 및 열 보기에서 정렬 옵션을 렌더링할 수 있습니다.

* 이제 다음을 사용할 수 있습니다 [!DNL Dynamic Media] 일반 설정을 구성하는 것이 아니라 [!DNL Dynamic Media Classic] 데스크탑 응용 프로그램입니다. 자세한 내용은 [Dynamic Media 일반 설정 구성](/help/assets/dm-general-settings.md).

* 이제 다음을 사용할 수 있습니다 [!DNL Dynamic Media] 를 선택하는 대신 게시 설정을 구성하려면 [!DNL Dynamic Media Classic] 데스크탑 응용 프로그램입니다. 자세한 내용은 [Dynamic Media 게시 설정 구성](/help/assets/dm-publish-settings.md).

* 내장된 저장소(Apache Jackrabbit Oak)가 1.22.9.

다음은 [!DNL Experience Manager] 6.5.11.0 릴리스에서 제공된 수정 사항 목록입니다.

### [!DNL Sites] {#sites-65110}

GraphQL에서 컨텐츠 조각을 사용하여 헤드리스 컨텐츠 게재에 액세스하고 향상된 컨텐츠 조각 모델 및 편집기 기능을 사용하려면 [인덱스 정의 패키지](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.0.0.zip), 및 다음 비동기 AEM 색인 정의를 다시 색인화합니다.

* /oak:index/assetPrefixNodename

* /oak:index/fragments

* /oak:index/graphqlConfig


다음 문제는에서 수정되었습니다 [!DNL Sites]:

* 컨텐츠 조각을 만드는 템플릿은 컨텐츠 조각을 만들 때 표시되지 않습니다(SITES-3365).

* 정규 표현식 및 [!UICONTROL 고유] 에서 필드 옵션이 작동하지 않습니다. [!UICONTROL appsUrl] 컨텐츠 조각 편집기의 모델(SITES-1823).

* 구성에 추가됨 `/apps/system` 노드 대신 `/libs` 이전 서비스 팩을 설치할 때(SITES-3203).

* 이전 서비스 팩 설치 시 컨텐츠 조각을 사용하는 기능이 평소대로 작동하지 않습니다(SITES-3151).

* 에서 정렬이 작동하지 않습니다. [!UICONTROL 컨텐츠 조각 모델] 콘솔(SITES-2722).

* GraphiQL이 모델(스키마)을 로드하지 않고 끝점 JSON에 대한 오류가 발생합니다(SITES-2428).

* 에 추가된 열거형 필드 형식 [!UICONTROL 컨텐츠 조각 모델] 에 표시되지 않음 [!UICONTROL 컨텐츠 조각 모델 편집기] (SITES-2391).

* 태그 데이터 유형은 특정 데이터 유형을 지원하지 않습니다(SITES-2390).

* [!UICONTROL 컨텐츠 조각 Rest API] 가 오래된 태그 값을 내보냅니다(SITES-2386).

* 탐색 표시의 화살표가 컨텐츠 조각 편집기에서 제대로 정렬되지 않습니다(SITES-2341).

* 컨텐츠 조각 참조 검색이 큰 데이터 세트에 대해 느려집니다(SITES-2147).

* [!UICONTROL CopyUrl] 옵션은 [!UICONTROL 컨텐츠 조각 편집기] (SITES-2007).

* 관련 모델과 함께 컨텐츠 조각을 게시하고 모델이 브레이크 변경 사항을 도입하면 경고가 표시되지 않습니다(SITES-1988).

* 컨텐츠 조각 모델의 URL 편집은 컨텐츠 조각 모델을 편집하는 다른 사용 사례에 대해 다릅니다(SITES-1980).

* 인라인을 사용하여 제목이 같은 두 개의 컨텐츠 조각을 만들 때 [!UICONTROL 새 컨텐츠 조각] 작업을 수행하면 마법사가 동일한 조각 경로(SITES-1978)를 반환합니다.

* 자동 완료가에서 작동하지 않음 [!UICONTROL 컨텐츠 조각 모델] 검색 패싯(SITES-1976).

* 컨텐츠 조각에 중첩된 조각의 대규모 계층이 포함되어 있는 경우, [!UICONTROL 컨텐츠 조각 편집기] 사이드 패널을 로드할 때 응답하지 않습니다(SITES-1974).

* 조각 선택기 경로에서 전역 검색이 작동하지 않습니다(SITES-1973).

* 컨텐츠 조각을 이동할 때 참조가 업데이트되었습니다(SITES-1897).

* 페이지를 만드는 옵션이 카드 보기 및 열 보기에 없습니다(NPR-37549).

* Launch 페이지에서 구성 요소를 재정렬할 때 Launch를 승격해도 구성 요소의 재정렬이 유지되지 않습니다(NPR-37539).

* 목록에서 모든 항목을 선택하는 옵션이 롤아웃 페이지에서 작동하지 않습니다(NPR-37443).

* 여러 페이지를 활성화하면 에 대한 새 JCR 세션이 열립니다 `wcm-workflow-service` 사용자(NPR-37417).

* 사이트 콘솔의 폴더에서 이동 작업이 실패하고 &quot;선택한 항목에 대한 실행 정보를 검색하지 못했습니다.&quot; 오류 메시지가 표시됩니다(NPR-37340).

* 블루프린트에 대한 축소판을 생성하고 Live Copy로 롤아웃할 때 Live Copy의 축소판 이후 탭의 상속이 끊어집니다(NPR-37190).

* Live Copy를 표시하는 필터 조건부가 모든 Live Copy를 표시하지 않습니다(NPR-37126).

* 복제 이벤트는 작성자에서 복제 이벤트 핸들러를 호출할 때 삭제하도록 표시된 모든 상위 및 하위 페이지 목록을 반환하지 않습니다(NPR-37123).

* 벌크 편집기를 사용하여 여러 값을 갖는 속성을 저장할 때 쉼표로 구분된 문자열이 배열의 첫 번째 요소로 저장됩니다(NPR-37089).

* 구성 요소 레이아웃 크기 조정이 모바일 레이아웃에서 작동하지 않습니다(NPR-37086).

* 롤아웃 구성을 추가한 후 페이지 속성을 저장할 때 새 노드가 Live Copy 수준에서 잘못 생성됩니다(NPR-37084).

* 사용자는 새 마스터 페이지에 대한 페이지 속성을 사용하여 라이브 카피를 만들거나 롤아웃할 수 없습니다(SITES-3442).

* 속성 수준에서 상속을 취소할 때 태그 속성이 제대로 작동하지 않으므로 제목 및 닫기 옵션 대신 태그가 태그 이름을 표시해도 태그가 완전히 제거되지 않습니다(NPR-36831).

* 모든 항목을 선택 취소하는 옵션이 작동하지 않고 헤더가 테이블의 첫 번째 행과 겹치기 때문에 라이브 카피 목록을 표시하는 페이지가 표시됩니다(NPR-37070).

* 워크플로우에 사용된 사용자 지정 대화 상자의 대화 상자의 유효성을 검사하려고 할 때 브라우저 콘솔에서 오류가 발생하여 Experience Manager이 실패합니다(GRANITE-35049).

에서는 다음과 같은 액세스 가능성이 개선되었습니다. [!DNL Adobe Experience Manager Sites]:

* 이제 화면 판독기에서 의 역할을 알려줍니다 [!UICONTROL 사이트 참조] 및 [!UICONTROL 언어 복사] 옵션(SITES-1791).

* 이제 브라우저 모드 초점의 순서가 사용자 인터페이스의 다양한 옵션에서 순차적으로 이동합니다(SITES-1791).

* 이제 화면 판독기에서 선택한 트리 항목이 선택된 상태인지 여부를 내레이션하고 작업 영역이 표시된다는 것을 사용자에게 알려줍니다(SITES-2109).

* 이제 필터 선택 또는 페이지 검색 시 로드 표시기가 있으면 화면 판독기에서 알려줍니다(SITES-1790).

* 이제 화면 판독기는 [!UICONTROL 필터] 옵션이 왼쪽 레일에 검색 결과를 반환하지 않습니다(SITES-1599).

* 검색 모드에서 탐색할 때 화면 판독기는 Enter 키를 누르면 컨텐츠 페이지의 역할과 선택한 페이지의 상태에 내레이션합니다(SITES-1579).

* 이제 다음의 경우 화면 판독기에 내레이션이 적용됩니다. [!UICONTROL 참고 추가] 옵션이 선택되어 있습니다(SITES-1573).

* 이제 양식 필드에 자리 표시자와 다른 시각적 레이블이 지정되므로, 화면 판독기 사용자가 필드 값을 입력할 때 적절히 안내됩니다(SITES-1258).

### [!DNL Assets] {#assets-65110}

다음과 같은 액세스 가능성이 개선되었습니다. [!DNL Assets]:

* 의 카드 보기에서 [!DNL Assets] 저장소, 사용 시 `Tab` 초점에 대한 빠른 작업을 여는 첫 번째 항목으로 포커스를 이동하는 키는 화면 판독기에서 포커스가 있는 항목의 이름을 알려줍니다.
* in [!DNL Dynamic Media] [!UICONTROL 뷰어 사전 설정 편집기][그림자 색상] 및 [테두리 색상]이 없으면 비활성화된 속성을 사용하여 입력을 사용할 수 없습니다. 키보드 사용자가 입력에 포커스를 둘 수 없으며 화면 판독기에서 제어 상태를 사용하지 않도록 설정했다고 알리지 않습니다.
* in [!DNL Dynamic Media]인터페이스에서 새로운 비디오 인코딩 프로필 을(를) 만들기 위해 [!UICONTROL 스마트 자르기 비율] 옵션 은 액세서빌러티 레이블이 지정되므로 화면 판독기에서 이를 적절히 알려줍니다.

* 이제 참조 목록 컨트롤에 액세스할 수 있습니다 [!DNL Experience Manager Assets] 키보드 사용.

다음 문제는에서 수정되었습니다 [!DNL Assets]:

* 기여자 그룹의 사용자가 DAM 자산 저장소로 이동하는 경우 예외 가능 `POST` 컬렉션을 만들기 위해 요청이 트리거됩니다. 이 `POST` 요청이 실패하고 로그에 오류가 반영됩니다(NPR-37171).

* 중첩된 폴더 구조의 블루프린트의 Live Copy를 만들 때 소스 폴더의 수정된 속성이 Live Copy 폴더에서 업데이트되지 않습니다(NPR-37449).

* 여러 자산을 선택하고 메타데이터 필드 값을 수정할 때 자산을 저장해도 값이 유지되지 않습니다. 또한 메타데이터 변경 사항이 적용되지 않습니다(NPR-37341).

* 여러 자산을 선택하고 속성을 수정할 때 사용자 지정 속성(드롭다운) 값이 기본값으로 재정의됩니다(NPR-36437).

* 브로셔, 플라이어 및 InDesign 템플릿에 대해 잘못된 PDF 표현물이 생성됩니다(NPR-36433).

* 저장 [!DNL Adobe Target] 활동 포함 [!DNL Experience Manager] 경우에 따라 타깃팅 모드가 실패합니다 [!DNL Adobe Analytics] 보고서 지표가 참조됩니다(NPR-37167).

* 대/소문자 도메인 이름을 혼합하여 이메일을 사용하는 사용자가 자산을 체크 아웃하면 사용자가 체크 아웃한 자산에 자산이 표시되지 않습니다. [!DNL Asset Link] (CQ-4329266).

<!-- Add 
* [!DNL Adobe Asset Link] is not able to access the digital assets even when the [!DNL Creative Cloud] and [!DNL Experience Management] entitlements are provided by two different organizations. -->

* 업로드 시 생성된 사용자 지정 메타데이터가 있는 비디오를 페이지에 추가하면 네임스페이스가 등록된 경우에도 알 수 없는 네임스페이스에 대한 오류가 표시됩니다(CQ-4331471).

* in [!DNL Assets]이면 [!DNL Launcher] 이 비활성화되어 있으면 수동으로 트리거할 때 메타데이터 원본에 쓰기 작업이 작동하지 않습니다(CQ-4329082).

### [!DNL Dynamic Media] {#dynamic-media-65110}

다음 버그 수정은에서 사용할 수 있습니다. [!DNL Dynamic Media]:

* 에서 자산이 업데이트되지 않음 [!DNL Dynamic Media] 에서 자산 버전을 복원할 때 [!DNL Experience Manager] (NPR-37421).

* PDF 파일 게시에 ECatalog가 게시되지 않습니다(CQ-4329886).

* 구성 요소가 기본 설정을 사용하는 경우 게시된 페이지를 열 때 3D 자산이 로드되지 않습니다(CQ-4329205).

* 대형 리포지토리의 경우 PDF 자산 처리 문제(CQ-4328711).

* PDF 처리 오류가 [!DNL Experience Manager] 에 장애가 발생한 경우 [!DNL Scene7] (CQ-4331145).

* 사용자가 .MOV 자산에 대한 기본 메타데이터 속성을 볼 수 없습니다(CQ-4332546).

* .MXF 비디오 파일을에 업로드할 수 없습니다. [!DNL Dynamic Media] 사용 [!DNL Experience Manager] (CQ-4329709).

* 사용자 지정 회사 루트가 설정될 때 문제를 업로드합니다(CQ-4332800).

* in [!DNL Experience Manager] 사용자 지정 런처를 포함하는 설정 `ActivationModel` 워크플로우에서 PDF 파일 업로드 시 메모리 문제로 인해 Experience Manager이 충돌합니다. (CQ-4330512).

* 의 성능 문제 `DamEventRecorder` (CQ-4334072).

* 쇼퍼블 비디오 하이퍼링크(연결된 URL)에 특수 문자가 포함된 경우 뷰어에서 대상 URL을 인코딩하고 결과를 잘못된 제품 페이지로 만듭니다(CQ-4331639).

* 비디오 프로필 페이지에서 사용자가 페이지 로드 즉시 비디오 프로필을 선택하면 도구 모음 옵션이 사라집니다(CQ-4308521).

* JCR 동시 쓰기로 인한 DM 자산 처리 실패(CQ-4333489).

* 사용자의 비디오 프로필 루트에 비디오 프로필 루트 노드에 정의된 사용자 지정 액세스 정책이 있는 경우 비디오 프로필 페이지에 액세스할 수 없습니다(CQ-4332941).

* 확대/축소 가능한 이미지에서 바로 가기 키(&#39;+&#39;, &#39;-&#39;) 또는 &#39;Esc&#39; 키를 사용하면 화면 판독기에 포커스가 트랩됩니다(CQ-4290719).

* 사용자가 양식 모드 바로 가기 키(&#39;F&#39;)를 클릭하면 화면 판독기가 [!UICONTROL 포함 크기] 메뉴 단추 [!UICONTROL 포함 가져오기] 코드 대화 상자(CQ-4290929).

* 키보드 탐색을 사용하여 전자 메일 링크 팝업 창을 열 때 &#39;받는 사람&#39; 및 &#39;보낸 사람&#39; 필드에 대한 사용자 인터페이스에 표시되는 오류 제안은 설명적이지 않습니다(CQ-4290930).

* 전자 메일 링크 대화 상자로 이동할 때 화면 판독기는 아래쪽 화살표 및 양식 모드 바로 가기 키(&#39;F&#39;)를 사용하여 새로 추가한 편집 필드에 대한 레이블 정보에 내레이션이 적용되지 않습니다(CQ-4290934).

* 전자 메일 링크 대화 상자로 이동할 때 화면 판독기는 &#39;받는 사람&#39; 및 &#39;보낸 사람&#39; 필수 필드에 대한 시각적 별표(*) 기호를 반영하지 않습니다(CQ-4290935).

* 사용자는 단축키 (&#39;D&#39;, &#39;R&#39;)를 사용하여 랜드마크 및 지역을 식별할 수 없습니다(CQ-4312118).

<!-- Anuj to check if this section is required or not. We have an enh. in CIF area that is mentioned. It is added above and not part of this bug fix section.
-->

### 상거래 {#commerce-65110}

* 를 사용할 때 [!UICONTROL 나중에 게시] 옵션을 선택하면 사용자 인터페이스가 상태를 [!UICONTROL 게시 보류 중] (CQ-4334229).

* 폴더 게시를 취소하면 해당 폴더의 제품이 완전히 게시 취소되지 않고 제품이 게시자에서 제거되지만 작성자 인스턴스에 계속 있습니다(CQ-4332731).

### 플랫폼 {#platform-65110}

* 사용자가 다중 필드 옵션에 대한 다시 정렬 아이콘을 클릭하면 사용자 인터페이스에서 스크롤 막대가 사라집니다(CQ-4331100).

* 업그레이드 후 사용자가 Workplace 로그인 컨테이너 구성 요소를 열면 사용자 인터페이스에 대화 상자의 헤더가 표시되지 않습니다(CQ-4316173).

### 통합 {#integrations-65110}

* 저장 [!DNL Adobe Target] 활동 포함 [!DNL Experience Manager] 경우에 따라 타깃팅 모드가 실패합니다 [!DNL Adobe Analytics] 보고서 지표가 참조됩니다(NPR-37167).

### 프로젝트 {#projects-65110}

* 에서 업그레이드할 때 [!DNL Experience Manager] 6.5.8.0에서 버전 6.5.9.0으로, 설치에서 속성을 덮어씁니다. `/content/dam/projects`. 폴더의 지정된 메타데이터 스키마 및 속성을 기본값으로 재설정합니다(NPR-37124).

### 사용자 인터페이스 {#user-interface-65110}

* 모델을 나타내는 폴더 아이콘이 잘못되었습니다(NPR-37176).

* 사용자가 경로 필드 브라우저를 사용하여 검색하거나 탐색할 때 잘못된 노드가 표시됩니다(NPR-37175).

* 게시 인스턴스에서 들어오는 요청이 몇 분 동안 차단됩니다(NPR-37169).

* 사용자 지정 워크플로우의 대화 상자에서 다중 필드 속성을 추가할 때 대화 상자가 진행되지 않고 사용자가 대화 상자를 닫을 수 없습니다(NPR-37075).

### 번역 프로젝트 {#translation-65110}

* 예외 없이 번역 론치의 자동 프로모션이 실패합니다(NPR-37528).

* 경험 조각을 번역해도 URL의 언어 사본에 대한 참조가 업데이트되지 않습니다(NPR-37522).

* 언어 루트 구조의 경로와 일치하지 않는 경로에 경험 조각을 만들면 해당 페이지를 번역 프로젝트에 추가하면 빈 오류 메시지가 표시됩니다(NPR-37425).

* 경험 조각이 포함된 페이지(영어)를 수정하고 번역용으로 전송하면 이미 번역된 경험 조각이 영어 컨텐츠로 덮어쓰여집니다(NPR-37283).

* 번역 공급자 필터가 제대로 작동하지 않습니다(NPR-37186).

* 경험 조각 및 아코디언 구성 요소가 샘플 사이트 컨텐츠에 대해 기본적으로 번역되지 않습니다(NPR-37170).

* 로 업그레이드한 후 [!DNL Experience Manager] 6.5.9.0에서 번역 프로젝트에 페이지를 추가하면 빈 오류 메시지가 표시됩니다(NPR-37105).

* launch 내에서 페이지를 추가할 때 비슷한 이름을 갖는 번역 페이지가 프로젝트에 포함되지 않습니다(NPR-37082).

* 변환기 인터페이스를 사용하여 양식 사전을 .xliff 파일로 내보낼 때 내보낸 파일의 필드 순서가 잘못되었습니다(NPR-37048).

* 번역 프로젝트에서 상위 페이지를 롤아웃하면 언어별 하위 페이지가 삭제됩니다(NPR-36998).

* 번역 프로젝트를 만들 때, 페이지의 순환 참조에 의해 론치가 트리거되어 오류가 발생합니다(CQ-4332982).

* 번역된 경험 조각 및 페이지의 경험 조각 링크에는 론치 참조가 포함되어 있습니다(NPR-37649).

### 슬링 {#sling-65110}

* 새 패키지를 업로드할 때 MapEntries 맵의 메모리 별칭이 제거됩니다(NPR-37067).

### 워크플로 {#workflow-65110}

* `Deactivate` 메서드 `InboxOmniSearchHandler` null 포인터 예외를 표시합니다(NPR-37533).

### [!DNL Communities] {#communities-65110}

* 사용자가 페이지에 주석을 추가할 수 없습니다. `Post` 오류 코드 500으로 인해 작업이 실패합니다(NPR-37156).

* 애플리케이션을 배포할 때 SyncManager의 긴 실행 세션으로 인해 세그먼트를 찾을 수 없음 예외가 관찰됩니다(NPR-37351).

* 사용자가 포럼 토론 게시물에서 스레드 응답을 볼 수 없습니다(NPR-37083).




<!--
Need to verify with Engineering, the status is currently showing as Resolved
-->


<!--
### [!DNL Brand Portal] {#brandportal-65110}

*

-->

### [!DNL Forms] {#forms-65110}


>[!NOTE]
>
>* [!DNL Experience Manager Forms] 는 예약된 후 1주일 후에 추가 기능 패키지를 출시합니다 [!DNL Experience Manager] 서비스 팩 릴리스 날짜입니다.


**적응형 양식**

* 액세스 가능성 - `Wizard` 적응형 양식의 패널에 대한 레이아웃에는 Aria 레이블과 역할이 없습니다(NPR-37613).

* 적응형 양식의 날짜 필드에 대한 유효성 검사가 예상대로 작동하지 않습니다(NPR-37556).

* 확인란 및 라디오 단추 구성 요소에 대한 레이블 텍스트가 길면 텍스트가 적절히 맞지 않습니다(NPR-37294).

* AEM Forms 컨테이너 구성 요소의 감사 메시지에 스타일 변경 사항을 적용할 때 변경 사항이 소스 적응형 양식에 복제되지 않습니다(NPR-37284).

* 값의 차이 `Switch` 사용자 인터페이스 및 백엔드에 있는 구성 요소입니다(NPR-37268).

* 키보드 키를 사용하여 `Submit` 옵션을 선택하고 키를 누릅니다 `Enter` 키를 사용하면 적응형 양식을 여러 번 제출할 수 있습니다(CQ-4333993).

* 첨부 파일 구성 요소에 대한 제거 작업이 예상대로 작동하지 않습니다(NPR-37376).

* 필드에 대한 레이블이 다양한 언어로 해석되는 적응형 양식에서 1000자를 초과하는 경우 사전이 레이블의 번역을 검색하지 못합니다(CQ-4329290).

**문서 서비스**

* 어셈블러 서비스를 사용하는 동안 오류가 표시됩니다(NPR-37606).

   ```TXT
     500 Internal Server Error
   ```

* 문서 첨부 파일이 어셈블러 서비스에 전달되면 다음 예외가 표시됩니다(NPR-37582).

   ```TXT
     com.adobe.livecycle.assembler.client.ProcessingException: ⁪: Failed to execute the DDX
   ```

* PDF 문서를 PDF-A/1B PDF 문서로 변환한 후 데이터에서 닫는 괄호가 누락되었습니다(NPR-37608).

**HTML5 양식**

* AEM 6.5.10.0을 설치하면 XDP 양식에 대한 HTML 미리 보기가 작동하지 않습니다(NPR-37503, CQ-4331926).

* 여러 언어로 HTML 5 양식으로 PDF forms을 마이그레이션하는 동안 텍스트가 겹치는 문제가 발생합니다(NPR-37173).

**편지**

* 편지를 제출하고 HTML 보기에서 다시 열면 텍스트 문서 조각의 위치가 동일하게 유지되지 않습니다(NPR-37307).

**양식 워크플로우**

* 포함된 컨테이너 워크플로우의 경우, 을(를) 선택한 후에도 여러 워크플로우 완료 이메일을 받게 됩니다 `Notify on Complete of Container Workflow` 옵션(NPR-37280).

**Foundation JEE**

* AEM 6.5 Forms 서비스 팩 9를 설치한 후 CRX 저장소 URL을 더 이상 사용할 수 없습니다(NPR-37592).


보안 업데이트에 대한 자세한 내용은 [[!DNL Experience Manager] 보안 게시판 페이지](https://helpx.adobe.com/security/products/experience-manager.html).

## 6.5.11.0 설치 {#install}

**설치 요구 사항 및 추가 정보**

* Experience Manager 6.5.11.0을 사용하려면 Experience Manager 6.5가 필요합니다. [업그레이드 설명서](/help/sites-deploying/upgrade.md) 자세한 지침
* 서비스 팩은 Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 다운로드할 수 있습니다.
* MongoDB 및 여러 인스턴스가 포함된 배포에서 패키지 관리자를 사용하여 작성자 인스턴스 중 하나에 Experience Manager 6.5.11.0을 설치합니다.

>[!NOTE]
>
>Adobe은 [!DNL Adobe Experience Manager] 6.5.11.0 패키지.

### 서비스 팩 설치 {#install-service-pack}

서비스 팩을 설치하려면 [!DNL Adobe Experience Manager] 6.5 인스턴스를 사용하여 다음 단계를 수행합니다.

1. 인스턴스가 업데이트 모드(이전 버전에서 인스턴스가 업데이트되었을 때)인 경우 설치하기 전에 인스턴스를 다시 시작합니다. Adobe은 인스턴스에 대한 현재 가동 시간이 높은 경우 다시 시작할 것을 권장합니다.

1. 설치하기 전에 스냅샷 또는 새 백업 [!DNL Experience Manager] 인스턴스.

1. 에서 서비스 팩 다운로드 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip).

1. 패키지 관리자를 열고 **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭하여 패키지를 업로드합니다. 자세한 내용은 [패키지 관리자](/help/sites-administering/package-manager.md).

1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

1. S3 커넥터를 업데이트하려면 서비스 팩을 설치한 후 인스턴스를 중지하고 기존 커넥터를 설치 폴더에 제공된 새 이진 파일로 바꾸고 인스턴스를 다시 시작합니다. 자세한 내용은 [Amazon S3 데이터 저장소](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>패키지 관리자 UI에 대한 대화 상자가 서비스 팩을 설치하는 동안 종료되는 경우가 있습니다. 배포에 액세스하기 전에 오류 로그가 안정될 때까지 기다리는 것이 좋습니다. 업데이터 번들 제거와 관련된 특정 로그를 기다린 후 설치가 성공했는지 확인합니다. 일반적으로 이 문제는 [!DNL Safari] 브라우저이지만 모든 브라우저에서 간헐적으로 발생할 수 있습니다.

**자동 설치**

자동으로 설치하는 두 가지 방법이 있습니다 [!DNL Experience Manager] 작업 인스턴스의 6.5.11.0:

A. 서버가 온라인 상태일 때 패키지를 `../crx-quickstart/install` 폴더에 넣습니다. 패키지가 자동으로 설치됩니다.

B. [패키지 관리자에서 HTTP API](/help/sites-administering/package-manager.md#package-share)를 사용합니다. 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

>[!NOTE]
>
>Adobe Experience Manager 6.5.11.0은 Bootstrap 설치를 지원하지 않습니다.

**설치 확인**

1. 제품 정보 페이지(`/system/console/productinfo`)에는 [!UICONTROL 설치된 제품] 아래에 업데이트된 버전 문자열 `Adobe Experience Manager (6.5.11.0)`이 표시됩니다.

1. 모든 OSGI 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]**&#x200B;이거나 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 콘솔 사용: `/system/console/bundles`).

1. OSGi 번들 `org.apache.jackrabbit.oak-core` 버전 1.22.3 이상(웹 콘솔 사용: `/system/console/bundles`).

이번 릴리스에서 사용할 수 있는 인증된 플랫폼을 확인하려면 [기술 요구 사항](/help/sites-deploying/technical-requirements.md)을 참조하십시오.

<!-- 

### Install Adobe Experience Manager Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Skip if you are not using Experience Manager Forms. Fixes in Experience Manager Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

1. Ensure that you have installed the Adobe Experience Manager Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>Experience Manager 6.5.10.0 includes a new version of [AEM Forms Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). If you are using an older version of AEM Forms Compatibility Package and updating to Experience Manager 6.5.10.0, install the latest version of the package post installation of Forms Add-On Package.

### Install Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Skip if you are not using AEM Forms on JEE. Fixes in Adobe Experience Manager Forms on JEE are delivered through a separate installer.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes](jee-patch-installer-65.md).

>[!NOTE]
>
>After installing the cumulative installer for Experience Manager Forms on JEE, install the latest Forms add-on package, delete the Forms add-on package from the `crx-repository\install` folder, and restart the server.

-->

### UberJar {#uber-jar}

Experience Manager 6.5.11.0용 UberJar는 [Maven 중앙 저장소](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.11/).

Maven 프로젝트에서 UberJar를 사용하려면 [Uberjar 사용 방법](/help/sites-developing/ht-projects-maven.md)을 참조하여 프로젝트 POM에 다음 종속성을 포함하십시오.

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.11</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar 및 기타 관련 가공물은 Adobe Public Maven 저장소(`repo.adobe.com`). 기본 UberJar 파일의 이름이 `uber-jar-<version>.jar`. 그래서, 아무것도 없어 `classifier`, 사용 `apis` 값으로서, `dependency` 태그에 가깝게 포함했습니다.

## 이제 사용되지 않는 기능 {#removed-deprecated-features}

다음은 사용 중단되는 것으로 표시된 기능 및 기능 목록입니다 [!DNL Experience Manager] 6.5.7.0. 기능은 처음에 더 이상 사용되지 않음으로 표시되고 이후 릴리스에서 이후에 제거됩니다. 다른 옵션이 제공됩니다.

배포에서 기능 또는 기능을 사용하는지 검토합니다. 또한 대체 옵션을 사용하도록 구현을 변경할 계획입니다.

| 영역 | 기능 | 대체 |
|---|---|---|
| 통합 | 다음 **[!UICONTROL AEM 클라우드 서비스 옵트인]** 화면은 다음부터 사용되지 않습니다 [!DNL Experience Manager] 및 [!DNL Adobe Target] 통합이 Experience Manager 6.5에서 업데이트되었습니다. 통합이 Adobe Target Standard API를 지원합니다. API는 Adobe IMS를 통한 인증 및 [!DNL Adobe I/O] 및 은 인스트루먼트에 대한 Adobe Launch의 늘어나는 역할을 지원합니다 [!DNL Experience Manager] 분석 및 개인화를 위한 페이지인 옵트인 마법사는 기능적으로 관련이 없습니다. | 시스템 연결, Adobe IMS 인증 및 구성 [!DNL Adobe I/O] 해당 [!DNL Experience Manager] 클라우드 서비스. |
| 커넥터 | Microsoft® SharePoint 2010 및 Microsoft® SharePoint 2013용 Adobe JCR 커넥터는 Experience Manager 6.5에서 더 이상 사용되지 않습니다. | N/A |

## 알려진 문제 {#known-issues}

* AEM 6.5 서비스 팩 11을 설치하고 상태 ZIP 파일을 다운로드하려고 하면 Experience Manager에서 손상된 파일을 다운로드합니다. 다운로드 및 설치 [AEM Sites SEO 색인 패키지](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/sites-seo-index-content-1.0.0.zip) 문제를 해결하기 위해 ZIP 파일을 다운로드하기 전에 AEM 인스턴스에 로그인합니다.

* 로서의 [!DNL Microsoft Windows Server 2019] 을 지원하지 않음 [!DNL MySQL 5.7] 및 [!DNL JBoss EAP 7.1], [!DNL Microsoft Windows Server 2019] 에 대한 턴키 설치를 지원하지 않습니다. [!DNL AEM Forms 6.5.10.0].

* 를 업그레이드하는 경우 [!DNL Experience Manager] 인스턴스(6.5에서 6.5.10.0 버전)를 `RRD4JReporter` 의 예외 `error.log` 파일. 문제를 해결하려면 인스턴스를 다시 시작합니다.

* 설치하는 경우 [!DNL Experience Manager] 6.5 서비스 팩 10 또는 이전 서비스 팩 [!DNL Experience Manager] 6.5, 자산 사용자 지정 워크플로우 모델의 런타임 사본(에서 생성) `/var/workflow/models/dam`)이 삭제됩니다.
런타임 복사본을 검색하려면 Adobe에서 HTTP API를 사용하여 사용자 지정 워크플로우 모델의 디자인 타임 사본을 해당 런타임 복사와 동기화하는 것이 좋습니다.
   `<designModelPath>/jcr:content.generate.json`.

* 사용자는 의 계층 구조에서 폴더의 이름을 바꿀 수 있습니다 [!DNL Assets] 중첩된 폴더를 [!DNL Brand Portal]. 그러나 폴더의 제목은에서 업데이트되지 않습니다 [!DNL Brand Portal] 루트 폴더를 다시 게시할 때까지 .

* 사용자가 적응형 양식에서 처음으로 필드를 구성하도록 선택하면 구성 저장 옵션이 속성 브라우저에 표시되지 않습니다. 동일한 편집기에서 적응형 양식의 다른 필드 일부를 구성하도록 선택하면 문제가 해결됩니다.

* 6.5.x.x Experience Manager 설치 중에 다음 오류 및 경고 메시지가 표시될 수 있습니다.
   * Target Standard API(IMS 인증)를 사용하여 Experience Manager에 Adobe Target 통합이 구성된 경우 환경 조각을 Target으로 내보내면 잘못된 오퍼 유형이 생성됩니다. 경험 조각/소스 Adobe Experience Manager 유형 대신 Target은 HTML/소스 Adobe Target Classic 유형으로 여러 가지 오퍼를 작성합니다.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: granite/operations/maintenance에 유지 관리 창이 없습니다.
   * SUM, MAX 및 MIN과 같은 집계 함수를 사용하는 경우 적용형 양식 서버측 유효성 검사가 실패합니다(CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance에 유지 관리 창이 없습니다.
   * 쇼퍼블 배너 뷰어를 통해 자산을 미리 볼 때 Dynamic Media 대화형 이미지의 핫스팟이 표시되지 않습니다.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : 등록 변경으로 등록 취소를 완료할 때까지 기다리는 중 시간이 초과되었습니다.

## OSGi 번들 및 컨텐츠 패키지가 포함됨 {#osgi-bundles-and-content-packages-included}

다음 텍스트 문서에는 다음 항목에 포함된 OSGi 번들 및 컨텐츠 패키지 목록이 나와 있습니다. [!DNL Experience Manager] 6.5.11.0:

* [Experience Manager 6.5.11.0에 포함된 OSGi 번들 목록](assets/65110_bundles.txt)

* [Experience Manager 6.5.11.0에 포함된 컨텐츠 패키지 목록](assets/65110_packages.txt)

## 제한된 웹 사이트 {#restricted-sites}

이러한 웹 사이트는 고객만 사용할 수 있습니다. 액세스가 필요한 고객의 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* 자세한 내용은 [Adobe 고객 지원에 문의하는 방법](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5 릴리스 노트](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] 제품 페이지](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 설명서](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ko-KR)
>* [Adobe 우선 순위 제품 업데이트](https://www.adobe.com/kr/subscription/priority-product-update.html) 구독

