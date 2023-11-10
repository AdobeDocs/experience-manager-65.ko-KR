---
title: 의 릴리스 정보 [!DNL Adobe Experience Manager] 6.5
description: 에 대한 릴리스 정보, 새로운 기능, 설치 방법 및 자세한 변경 목록을 확인하십시오. [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
source-git-commit: e4e2e8b58c0283182b2fbd4262a4ef9b607dac26
workflow-type: tm+mt
source-wordcount: '3429'
ht-degree: 7%

---

# [!DNL Adobe Experience Manager] 6.5 최신 서비스 팩 릴리스 노트 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 버전 | 6.5.19.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2023년 11월 23일 목요일 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 다운로드 URL | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 에 포함된 항목 [!DNL Experience Manager] 6.5.19.0 {#what-is-included-in-aem-6519}

[!DNL Experience Manager] 6.5.19.0에는 2019년 4월 6.5의 최초 출시 이후 릴리스된 새로운 기능, 주요 고객 요청 개선 사항, 버그 수정 사항 및 성능, 안정성, 보안 개선 사항이 포함되어 있습니다. [이 서비스 팩 설치](#install) 날짜 [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

이 릴리스의 몇 가지 주요 기능 및 개선 사항은 다음과 같습니다.

**주요 기능**

* A

**주요 개선 사항**

* S

**사용되지 않는 기능**

* AEM의 ActiveMQ는 더 이상 사용되지 않습니다. ActiveMQ는 두 AEM Publish 인스턴스 간의 통신에 사용되었습니다. Adobe은 이제 고객이 로드 밸런서를 사용할 것을 권장합니다.

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## 서비스 팩 19의 문제가 해결되었습니다. {#fixed-issues}

### [!DNL Sites]{#sites-6519}

* U

#### 접근성{#sites-accessibility-6519}

* AEM Sites 페이지에서 페이지를 200% 확대하면 링크가 연결됩니다 **[!UICONTROL 언어 복사]** 및 **[!UICONTROL CSV 보고서]** 참조 레일에서 가 사라집니다. (SITES-11011) 정상

#### 관리 사용자 인터페이스{#sites-adminui-6519}

* AEM Screens 채널 **[!UICONTROL 미리 보기]** 기능이 대시보드에서 작동하거나 표시되지 않습니다. (SITES-15730) 중요
* 페이지 이동 작업 중에 사용자 인터페이스가 참조를 표시할 수 없지만 자동으로 다시 게시됨을 나타내면 참조가 다시 게시됩니다 *아님* 다시 게시됨. (SITES-16435) 메이저
* 서비스 팩 16 또는 17이 있는 AEM 6.5에서 &quot;워크플로우&quot; 열이 활성화된 사이트의 목록 보기에서 해당 열의 항목을 기준으로 목록을 정렬할 수 없습니다. 정렬이 수행되지 않습니다. (SITES-15385) 메이저
* 리디렉션 페이지 템플릿의 경우 리디렉션 필드가 필수입니다. 그러나 필수 필드에 대한 유효성 검사가 적용되지 않거나 다음 두 시나리오에서 작동하지 않습니다. 필수 리디렉션 값 없이 페이지가 만들어지면 리디렉션 페이지를 만들 수 없습니다. 키보드 단축키를 사용하여 탐색할 때는 유효성 검사가 작동하지 않으며 필드가 유효하지 않은 것으로 표시되면 진행되지 않습니다. (SITES-15903) 정상
* 일부 **수신 링크** 이(가) 의 표시된 수에 포함되지 않았습니다. **참조** 패널. 예를 들어 패널에 **수신 링크(6)** 하지만 실제로 9개의 들어오는 링크들이 있었습니다. (SITES-14816) 정상

#### 클래식 UI{#sites-classicui-6519}

* SITES-15827에 핫픽스를 설치한 후 단어 사이에 공백이 있는 대화 상자 제목이 로 대체되었습니다 `" "`. 줄 바꿈도 제거 중입니다. (SITES-16089) 메이저
* 이제 인코딩된 대화 상자 제목으로 인해 제목이 이중 인코딩됩니다. (SITES-15841) 정상
* 서비스 팩 6.5.16에서 6.5.17로 AEM 서버를 업데이트하면 클래식 UI 대화 상자 제목이 이중 인코딩되었습니다. (SITES-15634) 정상

#### [!DNL Content Fragments]{#sites-contentfragments-6519}

* 내부 서버 오류 메시지가 콘텐츠 조각 편집기에 나타납니다. (SITES-13550) 중요
* 의 업데이트 `org.json` npr-41291의 방식으로 라이브러리에서 데이터 오류 변환 발생 `DefaultDataTypeConverter` / `cfm-impl` 번들. 데이터 유형 전환은 보다 유연해야 합니다. (SITES-16473) 정상
* &quot;호환되지 않는 콘텐츠로 인해 이 콘텐츠 조각 버전을 현재 버전과 비교할 수 없습니다.&quot; 오류 팝업 메시지를 가져옵니다. 콘텐츠 조각은 비교할 수 있어야 하지만 그렇지 않습니다. (SITES-16317) 정상
* 에서 자산 선택기 JS URL을 변경했습니다.
  `https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js`
끝
  `https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js` (SITES-16068) 정상
* CFM-Polaris 통합을 위해 새로운 Polaris 메타데이터 API 응답 스키마를 조정합니다. (SITES-15166) 정상
* 선택한 콘텐츠 조각을 참조하는 모든 콘텐츠 조각이 나열되어야 합니다. 대신 콘텐츠 조각 참조 패널의 에셋 참조에 0개의 참조가 표시됩니다. (SITES-15036) 정상

#### 핵심 백엔드{#sites-core-backend-6519}

* 개선 `StyleImpl`. (SITES-15164) 정상

<!--#### Core Components{#sites-core-components-6519}

* A -->

#### Campaign 통합{#sites-campaign-integration-6519}

* 서명 구성 요소(`/apps/fpl/components/campaign/signature`), 링크 외부화가 작동하지 않았습니다. 이미지 태그 위의 HTML 주석을 제거한 경우 도메인이 이미지 소스에 추가되지 않았습니다. 이 문제는 스테이징 환경이 아닌 프로덕션 환경의 서명 구성 요소에서만 발견되었습니다. (SITES-16120) 정상

<!--#### Experience Fragments{#sites-experiencefragments-6519}

* A -->

#### 기초 구성 요소 (기존){#sites-foundation-components-legacy-6519}

* Adobe Experience Manager(AEM) Sites 검색 구성 요소가 사용자 인터페이스를 중단합니다. (SITES-15087) 정상

#### GraphQL 쿼리 편집기{#sites-graphql-query-editor-6519}

* GraphQL Editor 사용자 인터페이스에서는 쿼리 수가 많은 경우(예: 25개 이상) 모든 지속 쿼리를 스크롤할 수 없습니다. (SITES-16008) 메이저
* GraphQL 편집기에서 지속 쿼리의 게시 상태를 저장하지 않습니다. GraphQL 편집기에 게시 취소 버튼이 표시되지만, 지속된 쿼리가 게시되었음을 나타내는 아이콘이 표시되지 않습니다. 페이지를 새로 고치면 지속 쿼리가 게시되지 않은 것으로 표시됩니다. (SITES-15858) 메이저

#### 론치{#sites-launches-6519}

* 다음 이유로 인해 저장소의 변경 사항이 저장되지 않음 `Oak0001` 여러 페이지를 편집하거나 콘텐츠를 작성할 때 충돌합니다. 이러한 이벤트에서 재시도를 수행하는 것은 일반적이지만, 이는 발생하지 않습니다. (SITES-14840) 메이저

#### MSM - 라이브 카피{#sites-msm-live-copies-6519}

* MSM 롤아웃 버튼은 터치 그래픽 사용자 인터페이스에서 작동하지 않습니다. (SITES-16991) 메이저
* 라이브 카피를 만들거나 경험 조각을 롤아웃할 때 경험 조각 내에서 링크 참조가 업데이트되지 않습니다. (SITES-15460) 정상

#### 페이지 편집기{#sites-pageeditor-6519}

* 에셋 유형 필터에서 여러 문서 파일 유형 선택이 페이지 콘솔에서 작동하지 않습니다. 특정 파일 유형의 결과를 사용할 수 있어도 결과를 찾을 수 없습니다. 따라서 작성자가 여러 문서를 필터링할 수 없습니다. 여러 문서 유형을 사용해야 하며 한 번에 하나씩 필터링해야 합니다. (SITES-14047) 메이저
* AEM 6.5.17 및 AEM 6.5.18에서 인스턴스를 업그레이드한 후 페이지 편집기 내에서 을 선택합니다. **[!UICONTROL 페이지 게시]**&#x200B;가 없는 URL로 리디렉션됩니다. 사용자는 게시 마법사로 리디렉션되어야 합니다. (SITES-15856) 정상
* (SITES-15704) 정상
* 운영 체제의 클립보드에서 붙여넣는 동안 AEM 클립보드에서 중복 복사됩니다. (SITES-15704) 정상
* 에셋에서 선택 **[!UICONTROL 문서]**, 다음 아래 **[!UICONTROL 필터 유형]**, 선택 **[!UICONTROL Microsoft® Word]** 또는 **[!UICONTROL Microsoft® Excel]** 두 유형의 파일이 모두 있어도 결과를 표시하지 않습니다. (SITES-14837) 정상

### [!DNL Assets]{#assets-6519}

* Experience Manager 또는 Brand Portal에 게시할 자산을 구분할 수 없습니다. [NPR-41320]
* 공용 폴더를 만들거나 저장하면 관리 대시보드에 세 개의 그룹이 만들어집니다. [ASSETS-26700]
* 검색 패널에서 확인란을 선택하고 둘 중 하나를 선택 취소하면 모든 확인란이 선택 취소됩니다. [ASSETS-26377]

#### [!DNL Dynamic Media]{#assets-dm-6519}

* 에셋이 AEM에 업로드되면 `update_asset` 워크플로우가 트리거됩니다. 워크플로우가 완료되지 않습니다. 워크플로 인스턴스를 보면 워크플로가 제품 업로드 단계까지 완료됩니다. 다음 단계는 scene7 일괄 업로드입니다. 사용자는 Dynamic Media Classic 앱에서 자산이 Scene7에 있음을 볼 수 있습니다. (ASSETS-30443) 위험
* 사용자 지정 서블릿(API 끝점)이 잘못된 Dynamic Media(Scene7) 파일 이름을 반환하고 있습니다. 에셋을 삭제하고 동일한 이름의 에셋으로 대체할 때 발생합니다. 사용자 지정 서블릿은 이전 Dynamic Media(Scene7) 파일 이름을 반환하고 있지만 &quot;jcr&quot; API 호출은 올바른 파일 이름을 반환합니다. (ASSETS-29476) 주
* 폴더 수준에서 동기화가 꺼진 후에도 로그에 &quot;Scene7 ReplicateOnModifyListener&quot; 트리거가 표시됩니다. 다음 `ReplicateOnModifyListener/Worker` 비 Dynamic Media 폴더 자산 및 컨텐츠 조각에 대한 처리를 건너뜁니다. (ASSETS-26705) 주
* 고대비 흑백 모드의 드롭다운 요소(컨텐츠 전용, 보기, 추가 옵션)에 초점이 표시되지 않으면 시력이 낮은 사람이 영향을 받습니다. (ASSETS-25759) 정상
* 페이지의 텍스트에 대한 광도 대비율 이 4.5:1 미만인 경우 시력이 낮은 사람이 영향을 받습니다. (ASSETS-25756) 정상
* 화면 판독기에서 데이터를 제출한 후 표시된 팝업 메시지에 내레이션이 적용되지 않습니다. (ASSETS-25755) 정상
* 랜드마크/영역 단축키를 사용하여 탐색할 때 화면 판독기가 페이지의 랜드마크(Dynamic Media, 비디오 인코딩 프로필 만들기)를 인식하지 못합니다 `D/R`. (ASSETS-25752) 정상
* 랜드마크/영역 단축키를 사용하여 탐색할 때 화면 판독기가 페이지에서 여러 랜드마크를 인식하지 못합니다(Dynamic Media; 대화형 비디오 만들기) `D/R`. (ASSETS-25750) 정상
* 화면 판독기(NVDA/JAWS/내레이터)가 의 랜드마크를 인식하지 못합니다. **에셋 편집** 단축키를 사용하여 탐색하는 동안 페이지 `D/R`. (ASSETS-25744) 정상
* 사용자가 empty/false 비동기 작업 메시지를 가져오지만 연결된 자산이 게시되었습니다. (ASSETS-29342) TRIVIAL

### [!DNL Forms]{#forms-6519}

의 수정 사항 [!DNL Experience Manager] Forms은 예약한 후 1주일 후에 별도의 추가 기능 패키지를 통해 제공됩니다 [!DNL Experience Manager] 서비스 팩 릴리스 날짜. 이 경우 AEM 6.5.19.0 Forms 추가 기능 패키지 릴리스가 2023년 11월 30일 목요일에 예정되어 있습니다. Forms 수정 사항 및 개선 사항 목록은 릴리스를 게시하는 이 섹션에 추가됩니다.

* 액세스 제어 목록 추가 `fd-cloudservice` 아래에서 Microsoft® 구성을 읽거나 업데이트할 수 있는 사용자 `cloudconfigs/microsoftoffice`. (FORMS-11142) 정상

<!--LEFT BULLET LIST HERE IN CASE OF REUSE BY FORMS IN THE FUTURE 
* **Document Services**
  * text
* **Adaptive Forms** 
  * text
* **Accessibility**
  * text
* **Interactive Communications**
  * text -->

<!--### Commerce{#commerce-6519}

* A -->

### Foundation{#foundation-6519}

* 언어 루트 수준에서 언어 사본을 만들어도 페이지의 경로가 조정되지 않습니다. 언어 루트가 아닌 그 아래의 페이지에 대한 언어 사본이 작성된 경우 경로가 올바르게 변경되었습니다. (NPR-41364) 메이저
* &quot;상대적 날짜 표시&quot; 도구 설명은 키보드에서 Esc(Esc)를 눌러야만 닫을 수 있습니다. 사용자가 사용자 인터페이스의 일부를 선택하면 툴팁이 닫힙니다. (NPR-41394) 정상
* 지역화되지 않은 문자열 `Something went wrong while adding the private key.` 에서 잘못된 개인 키 파일을 추가할 때 **사용자 편집** > **키 저장소**. (NPR-41366) 정상
* 아이콘은 AEM 6.5 환경에서 Microsoft® SharePoint 및 Microsoft® One Drive에 필요합니다. (NPR-41354) 정상
* 현지화되지 않은 &quot;UserId/Password 불일치&quot; 문자열 **보안** > **사용자** > **만들기** 대화 상자. (NPR-41245) 정상
* 팝오버 코드와 이벤트 핸들러가 두 번 로드되어 사용자가 만든 Coral3 기반 사용자 인터페이스가 끊어집니다. (NPR-41171) 정상
* AEM Sites 콘솔에서 &quot;모두 선택&quot;을 사용한 후에는 선택 해제가 제대로 작동하지 않습니다. (NPR-41304) 마이너

<!--#### Content distribution{#foundation-content-distribution-6519}

* T -->

#### 통합{#integrations-6519}

* AEM 이메일 캠페인의 SMS 링크가 올바르게 작성되지 않습니다. 여기에는 HTML 앵커 요소가 포함되어 있습니다. (NPR-41211) 메이저
* 계정 구성 화면에서 사용된 문구는 새 자격 증명 유형을 사용하지 않아야 합니다. (NPR-41210) 정상
* 에서 Analytics 보고서 가져오기 스케줄러 이동 `ManagedPollConfig` 슬링 작업. 서로 다른 두 개의 분석 프레임워크가 서로 다른 보고서 세트를 사용하여 서로 다른 두 사이트에 연결된 경우 `ManagedPollConfig` 이 중 하나만 설문 조사합니다. (NPR-41209) 정상
* 값이 기본값으로 재설정되면 이전에 선택한 일정 버튼이 활성 상태로 유지됩니다. AEM의 컨텐츠 인사이트 대시보드에서 기본적으로 시간대는 주로 설정되며 컨텐츠 인사이트를 주별 데이터로 표시합니다. 이제 사용자가 시간, 일, 월 및 년과 같은 다른 시간대 옵션을 선택하면 선택한 값에 따라 데이터가 변경됩니다. 그러나 값이 재설정되면 기본적으로 표시되는 시간대는 주이지만 이전에 선택한 시간대 옵션이 선택됩니다. (NPR-41246) 마이너

#### Oak{#oak-6519}

* 비동기 인덱싱이 지연될 경우 AEM에 대한 쓰기 제한 속도를 계산하는 백포트 유틸리티입니다. (NPR-40985) 메이저

#### Platform{#foundation-platform-6519}

* 대괄호가 있는 QueryBuilder 쿼리가 xpath 로 잘못 변환됩니다. (NPR-41298) 정상

<!--#### Replication{#foundation-replication-6519}

* R -->

<!--#### Sling{#foundation-sling-6519}

* W -->

#### 번역 프로젝트{#foundation-translation-6519}

* 페이지 &quot;A&quot;의 언어 사본을 만드는 동안 참조된 페이지, 경험 조각, 콘텐츠 조각 및 에셋의 언어 사본을 자동으로 만들어야 합니다. 또한 새 경로에 있는 페이지 &quot;A&quot;의 새로 만든 언어 사본에는 해당 참조가 페이지, 경험 조각, 콘텐츠 조각 및 에셋의 새로 만든 각각의 언어 사본으로 업데이트되어야 합니다. (NPR-41076) 정상

<!--#### User interface{#foundation-ui-6519}

* A -->

<!--#### WCM{#wcm-6519}

* A -->

#### 워크플로{#foundation-workflow-6519}

* 받은 편지함에서 작업을 완료할 수 없습니다. 작업을 완료하고 작업을 선택하려고 할 때 드롭다운 메뉴에 &quot;정의되지 않은&quot; 값만 표시됩니다. 즉, 사용자가 AEM 6.5.18 서비스 팩을 적용할 수 없습니다. (NPR-41402) 메이저
* 받은 편지함에서 작업을 완료할 수 없습니다. zip 파일, 에셋 보고서, 이동(성공 또는 실패) 또는 에셋 만료에 대한 작업을 완료하려고 할 때 드롭다운 목록에 값이 없음(&quot;정의되지 않음&quot;만 해당). (NPR-41305) 메이저
* 사용자가 선택할 때 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > 인스턴스, 실행 중인 워크플로우를 선택한 다음 를 선택합니다 **[!UICONTROL 페이로드 보기]**&#x200B;로 설정하면 500개의 오류 페이지가 표시됩니다. (NPR-41325) 정상


## 설치 [!DNL Experience Manager] 6.5.18.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.19.0을 사용하려면 [!DNL Experience Manager] 6.5. 참조 [업그레이드 설명서](/help/sites-deploying/upgrade.md) 자세한 지침은 을 참조하십시오. <!-- UPDATE FOR EACH NEW RELEASE -->
* 서비스 팩은 Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip)에서 다운로드할 수 있습니다.
* MongoDB 및 여러 인스턴스가 포함된 배포에서 다음을 설치합니다. [!DNL Experience Manager] 패키지 관리자를 사용하는 작성자 인스턴스 중 하나에서 6.5.19.0.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe은 를 제거하거나 제거하지 않는 것이 좋습니다. [!DNL Experience Manager] 6.5.19.0 패키지. 따라서 팩을 설치하기 전에 `crx-repository` 혹시라도 돌려주셔야 할 것 같은데요 <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### 서비스 팩 설치 [!DNL Experience Manager] 6.5{#install-service-pack}

1. 인스턴스가 업데이트 모드에 있는 경우(인스턴스가 이전 버전에서 업데이트된 경우) 설치 전에 인스턴스를 다시 시작하십시오. Adobe은 인스턴스의 현재 가동 시간이 높을 경우 다시 시작할 것을 권장합니다.

1. 설치하기 전에 스냅샷 또는 새 백업을 [!DNL Experience Manager] 인스턴스.

1. 에서 서비스 팩 다운로드 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. 패키지 관리자를 열고 를 선택합니다 **[!UICONTROL 패키지 업로드]** 패키지를 업로드합니다. 자세한 내용은 [패키지 관리자](/help/sites-administering/package-manager.md).

1. 패키지를 선택한 다음 를 선택합니다 **[!UICONTROL 설치]**.

1. S3 커넥터를 업데이트하려면 서비스 팩을 설치한 후 인스턴스를 중지하고 기존 커넥터를 설치 폴더에 있는 새 이진 파일로 바꾼 다음 인스턴스를 다시 시작하십시오. 다음을 참조하십시오 [Amazon S3 데이터 저장소](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>패키지 관리자 UI에 대한 대화 상자가 서비스 팩을 설치하는 동안 종료되는 경우가 있습니다. 배포에 액세스하기 전에 오류 로그가 안정될 때까지 기다리는 것이 좋습니다. 업데이터 번들 제거와 관련된 특정 로그를 기다린 후 설치가 성공했는지 확인합니다. 일반적으로 이 문제는에서 발생합니다. [!DNL Safari] 브라우저이지만 모든 브라우저에서 간헐적으로 발생할 수 있습니다.

**자동 설치**

를 사용하여 자동으로 설치할 수 있는 두 가지 방법이 있습니다 [!DNL Experience Manager] 6.5.19.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* 서버가 온라인 상태일 때 패키지를 `../crx-quickstart/install` 폴더에 넣습니다. 패키지가 자동으로 설치됩니다.
* [패키지 관리자에서 HTTP API](/help/sites-administering/package-manager.md#package-share)를 사용합니다. 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

>[!NOTE]
>
>Experience Manager 6.5.19.0은 Bootstrap 설치를 지원하지 않습니다. <!-- UPDATE FOR EACH NEW RELEASE -->

**설치 확인**

이 릴리스에서 사용할 수 있는 인증된 플랫폼을 확인하려면 다음을 참조하십시오. [기술 요구 사항](/help/sites-deploying/technical-requirements.md).

1. 제품 정보 페이지(`/system/console/productinfo`) 업데이트된 버전 문자열을 표시합니다 `Adobe Experience Manager (6.5.19.0)` 아래에 [!UICONTROL 설치된 제품]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 모든 OSGI 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]**&#x200B;이거나 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 콘솔 사용: `/system/console/bundles`).

1. OSGi 번들 `org.apache.jackrabbit.oak-core` 는 버전 1.22.16 이상입니다(웹 콘솔 사용: `/system/console/bundles`). <!-- NPR-41010 for 6.5.18.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### 서비스 팩 설치 [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Experience Manager Forms에 서비스 팩을 설치하는 방법은 다음을 참조하십시오. [Experience Manager Forms 서비스 팩 설치 지침](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>AEM 6.5 빠른 시작에서 사용할 수 있는 적응형 Forms 기능은 탐색 및 평가 목적으로만 설계되었습니다. 프로덕션 사용을 위해서는 적응형 Forms 기능에 적절한 라이선스가 필요하므로 AEM Forms에 대한 유효한 라이선스를 얻는 것이 필수적입니다.

### Experience Manager 콘텐츠 조각용 GraphQL 인덱스 패키지 설치{#install-aem-graphql-index-add-on-package}

GraphQL을 사용하는 고객은 [GraphQL 인덱스 패키지 1.1.1로 Experience Manager 컨텐츠 조각](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

이렇게 하면 필요한 인덱스 정의가 실제로 사용하는 기능을 기반으로 추가할 수 있습니다.

이 패키지를 설치하지 않으면 GraphQL 쿼리가 느려지거나 실패할 수 있습니다.

>[!NOTE]
>
>이 패키지는 인스턴스당 한 번만 설치하십시오. 모든 서비스 팩으로 다시 설치할 필요는 없습니다.

### UberJar{#uber-jar}

에 대한 UberJar [!DNL Experience Manager] 6.5.19.0은 [Maven Central 저장소](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.18/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Maven 프로젝트에서 UberJar를 사용하려면 [uberJar 사용 방법](/help/sites-developing/ht-projects-maven.md) 프로젝트 POM에 다음 종속성을 포함하십시오. <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.19</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar 및 기타 관련 아티팩트는 공개 Maven 저장소 Adobe 대신 Maven 중앙 저장소에서 사용할 수 있습니다(`repo.adobe.com`). 기본 UberJar 파일의 이름이 로 바뀝니다. `uber-jar-<version>.jar`. 그래서, `classifier`, 포함 `apis` 값으로, 을 사용합니다. `dependency` 태그에 가깝게 배치하십시오.

## 이제 사용되지 않는 기능과 제거된 기능{#removed-deprecated-features}

다음을 참조하십시오 [사용이 중단되거나 제거된 기능](/help/release-notes/deprecated-removed-features.md/).

## 알려진 문제{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* **서비스 팩 18(6.5.19.0)로 업그레이드한 후 페이지 편집기에서 페이지 게시가 작동하지 않음**

  <!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0--> AEM 6.5.0.0—6.5.17.0의 인스턴스를 AEM 6.5.19.0으로 업그레이드한 후 **페이지 게시** 페이지 편집기 내에서 존재하지 않는 URL로 리디렉션됩니다.

  이 문제를 해결하려면 다음 중 하나를 수행하십시오.

   * 다음 &quot;path&quot; 속성을 제거합니다.

     `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

   * 올바른 URL을 브라우저에 바로 붙여넣습니다.

     `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html`



* **Oak 관련**
서비스 팩 13 이상부터 지속성 캐시에 영향을 주는 다음 오류 로그가 나타나기 시작했습니다.

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  또는

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  이 예외를 해결하려면 다음을 수행합니다.

   1. 에서 다음 두 폴더를 삭제합니다. `crx-quickstart/repository/`

      * `cache`
      * `diff-cache`

   1. 서비스 팩을 설치하거나 Experience Manager을 as a Cloud Service으로 다시 시작합니다.
의 새 폴더 `cache` 및 `diff-cache` 이(가) 자동으로 만들어지므로 더 이상 과 관련된 예외가 발생하지 않습니다. `mvstore` 다음에서 `error.log`.

* 콘텐츠 모델의 기본 이름을 대신 사용하도록 콘텐츠 모델에 대해 사용자 지정 API 이름을 사용했을 수 있는 GraphQL 쿼리를 업데이트합니다.

* GraphQL 쿼리는 `damAssetLucene` 색인 대신 `fragments` 색인입니다. 이 작업으로 인해 GraphQL 쿼리가 실패하거나 실행하는 데 시간이 오래 걸릴 수 있습니다.

  문제를 해결하려면 `damAssetLucene` 다음 두 속성을 포함하도록 구성해야 합니다. `/indexRules/dam:Asset/properties`:

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  색인 정의를 변경한 후에는 리인덱싱이 필요합니다(`reindex` = `true`).

  이러한 단계 후에는 GraphQL 쿼리가 더 빨리 수행됩니다.

* 콘텐츠 조각, 사이트 또는 페이지를 이동, 삭제 또는 게시하려고 할 때 배경 쿼리가 실패하여 콘텐츠 조각 참조를 가져올 때 문제가 있습니다. 즉, 기능이 작동하지 않습니다.
올바른 작업을 위해 인덱스 정의 노드에 다음 속성을 추가해야 합니다 `/oak:index/damAssetLucene` (리인덱싱이 필요하지 않음):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* 업그레이드 시 [!DNL Experience Manager] 6.5.0 - 6.5.4에서 Java™ 11의 최신 서비스 팩까지 인스턴스가 제공됩니다. `RRD4JReporter` 의 예외 `error.log` 파일. 예외를 중지하려면 인스턴스를 [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 사용자는 의 계층 구조에서 폴더의 이름을 변경할 수 있습니다. [!DNL Assets] 중첩된 폴더 게시 위치 [!DNL Brand Portal]. 단, 폴더의 제목은에서 업데이트되지 않습니다. [!DNL Brand Portal] 루트 폴더가 다시 게시될 때까지.

* 설치 중에 다음과 같은 오류 및 경고 메시지가 표시될 수 있습니다. [!DNL Experience Manager] 6.5.x.x:
   * &quot;Adobe Target 통합이에서 구성된 경우 [!DNL Experience Manager] target Standard API(IMS 인증)를 사용한 다음 경험 조각을 Target으로 내보내면 잘못된 오퍼 유형이 생성됩니다. 경험 조각/소스 &quot;Adobe Experience Manager&quot; 유형 대신 Target은 &quot;HTML&quot;/소스 &quot;Adobe Target Classic&quot; 유형으로 여러 오퍼를 만듭니다.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: granite/operations/maintenance에 유지 관리 창이 없습니다.
   * SUM, MAX 및 MIN과 같은 집계 함수를 사용하는 경우 적용형 양식 서버측 유효성 검사가 실패합니다(CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance에 유지 관리 창이 없습니다.
   * 쇼퍼블 배너 뷰어를 통해 자산을 미리 볼 때 Dynamic Media 대화형 이미지의 핫스팟이 표시되지 않습니다.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : 등록 변경이 등록 취소를 완료할 때까지 기다리는 동안 시간이 초과되었습니다.

* AEM 6.5.15부터 Rhino JavaScript Engine은 ```org.apache.servicemix.bundles.rhino``` 번들에 새로운 호스팅 동작이 있습니다. 엄격 모드를 사용하는 스크립트(```use strict;```) 변수를 올바르게 선언해야 합니다. 그렇지 않으면 런타임 오류가 발생하는 대신 실행되지 않습니다.

### AEM Forms의 알려진 문제

#### 지원되는 플랫폼

* 1.8.0_281 이상의 JDK 버전은 WebLogic JEE 서버에서 지원되지 않습니다. (FORMS-8498, CQDOC-20383)
* 다음으로: [!DNL Microsoft® Windows Server 2019] 은(는) 을 지원하지 않습니다. [!DNL MySQL 5.7] 및 [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] 은(는) 다음에 대한 턴키 설치를 지원하지 않습니다. [!DNL Experience Manager Forms 6.5.10.0]. (CQDOC-18312)
* JDK 11.0.20은 JEE 설치 관리자에서 AEM Forms을 설치할 수 없습니다. JEE 설치 프로그램에 AEM Forms을 설치하려면 JDK 11.0.19 이하 버전만 지원됩니다. (FORMS-10659)

#### 설치

* JBoss® 7.1.4 플랫폼에서 사용자가 Experience Manager 6.5.16.0 이상의 서비스 팩을 설치하면 `adobe-livecycle-jboss.ear` 배포가 실패합니다. (CQ-4351522, CQDOC-20159)
* Windows Server 2022에서 AEM Forms 6.5.18.0 JBoss® Turnkey 전체 설치 관리자 환경으로 업그레이드한 후 Java™ 11을 사용하여 출력 클라이언트 응용 프로그램 코드를 컴파일할 때 다음 컴파일 오류가 발생할 수 있습니다.

  ```
  error: error reading [AEM_Forms_Installation_dir]\sdk\client-libs\common\adobe-output-client.jar; java.net.URISyntaxException: 
  Illegal character in path at index 70: file:/[AEM_Forms_Installation_dir]/sdk/client-libs/common/${clover.jar.name} 1 error
  ```

  이 문제를 해결하려면 다음 단계를 수행하십시오.
   1. 다음으로 이동 `[AEM_Forms_Installation_dir]\sdk\client-libs\common\` 및 압축 풀기 `adobe-output-client.jar` 을(를) 추출하려면 `Manifest.mf` 파일.
   1. 업데이트 `Manifest.mf` 항목을 제거하여 파일 `${clover.jar.name}` class-path 속성에서 가져옵니다.

      >[!NOTE]
      >
      > 즉석 편집 도구(예: 7-zip)를 사용하여 `Manifest.mf` 파일.

   1. 업데이트된 을 저장합니다. `Manifest.mf` 다음에서 `adobe-output-client.jar` 보관.
   1. 수정된 내용 저장 `adobe-output-client.jar` 파일을 만들고 설치 프로그램을 다시 실행하십시오. (CQDOC-20878)
* AEM 서비스 팩 6.5.19.0 전체 설치 관리자를 설치한 후 JBoss® 턴키를 사용하여 JEE에서 EAR 배포가 실패합니다.
문제를 해결하려면 `<AEM_Forms_Installation_dir>\jboss\bin\standalone.bat` 파일 및 업데이트 `Adobe_Adobe_JAVA_HOME` 끝 `Adobe_JAVA_HOME` 구성 관리자를 실행하기 전에 발생하는 모든 발생 횟수. (CQDOC-20803)

#### 적응형 양식

* 적응형 양식이 게시되면 정책을 포함한 모든 종속 항목은 수정 사항이 없더라도 다시 게시됩니다. (FORMS-10454)
* 사용자가 적응형 양식에서 처음으로 필드를 구성하도록 선택하면 구성 저장 옵션이 속성 브라우저에 표시되지 않습니다. 동일한 편집기에서 적응형 양식의 다른 필드 일부를 구성하도록 선택하면 문제가 해결됩니다.
* 리디렉션 URL이 적응형 양식의 안내서 컨테이너에 설정되면 인라인 서명 작동이 중지됩니다. (FORMS-10493)
* 모든 기록 문서(DoR) 템플릿을 게시할 수 없습니다. 영어 로케일 기반 DoR 템플릿과 관련 Forms 기반 DoR 템플릿만 게시됩니다. (FORMS-10535)

#### 대화형 통신

* AEM 서비스 팩 18로 업그레이드한 후에는 편집 모드에서 큰 인라인 이미지가 있는 대화형 통신을 열 수 없습니다. (FORMS-10578) 이 문제를 해결하려면 다음 단계를 수행하십시오.

   1. 다운로드 [Hotfix-FORMS-10578](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) SD 링크에서.
   1. 핫픽스 아카이브 파일을 추출하여 Experience Manager 패키지(.zip)와 번들(.jar) 파일을 가져올 수 있습니다.
   1. 패키지 관리자를 통해 패키지(.zip)를 업로드하고 설치합니다.
   1. 구성 관리자 번들을 엽니다. `https://server:host/system/console/bundles`번들(.jar)을 업로드하고 설치합니다.

## OSGi 번들 및 콘텐츠 패키지가 포함됨{#osgi-bundles-and-content-packages-included}

다음 텍스트 문서는에 포함된 OSGi 번들 및 콘텐츠 패키지 목록입니다. [!DNL Experience Manager] 6.5.19.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager 6.5.19.0에 포함된 OSGi 번들 목록](/help/release-notes/assets/65180_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.19.0에 포함된 컨텐츠 패키지 목록](/help/release-notes/assets/65180_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 제한된 웹 사이트{#restricted-sites}

이러한 웹 사이트는 고객만 사용할 수 있습니다. 고객이고 액세스 권한이 필요한 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [Adobe 고객 지원 문의](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 제품 페이지](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 설명서](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* [Adobe 우선 순위 제품 업데이트](https://www.adobe.com/kr/subscription/priority-product-update.html) 구독
