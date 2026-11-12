---
title: '[!DNL Adobe Experience Manager] 6.5 릴리스 정보'
description: '[!DNL Adobe Experience Manager] 6.5에 대한 릴리스 정보, 새로운 기능, 설치 방법 및 자세한 변경 사항 목록을 확인합니다.'
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
contentOwner: Rick Brough
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: ed762d86-a04b-452b-a08f-86359bb8ff27
    internal-label: Configuration and operations
subfeature_v2:
  - id: c21ccc2b-e0c8-4853-bf41-f12259ed93f8
    internal-label: Release information
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: d777049ff8873ab60b286ec268fd544dc61fb038
workflow-type: tm+mt
source-wordcount: '7172'
ht-degree: 3%
---
# [!DNL Adobe Experience Manager] 6.5 최신 서비스 팩 릴리스 노트 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!--
DO NOT DELETE THIS HIDDEN NOTE!      DO NOT DELETE THIS HIDDEN NOTE!
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section.
-->

## 릴리스 요약 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 버전 | 6.5.26.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2026년 11월 12일 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 다운로드 URL | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.26.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |


<!-- REWRITE AI GENERATED SUMMARY OF NOTES BELOW FOR EACH NEW SERVICE PACK RELEASE -->

Experience Manager 6.5.26.0에는 새로운 기능, 주요 고객 요청 개선 사항 및 버그 수정 사항이 포함되어 있습니다. 또한 2019년 4월 이후 제공되는 6.5 기반 위에 구축된 접근성, 현지화, 성능, 안정성 및 보안 개선 사항이 포함되어 있습니다.

서비스 팩 26의 주요 사항은 다음과 같습니다.

* 보안. 메타데이터 편집기의 서버측 템플릿 삽입 취약점과 Coral UI 서블릿의 XSS(크로스 사이트 스크립팅) 위반에 대한 두 가지 중요한 수정 사항이 해결되었습니다.
* C2PA 규정 준수. 이제 Assets은 C2PA 자격 증명을 감지하고 자산 업데이트 워크플로우가 생성하는 렌디션에 서명합니다. 서명은 각 인스턴스에서 로컬로 실행되며 전용 또는 고객 소유 서명 인프라는 지원되지 않습니다.
* 접근성. 25개 이상의 수정 사항이 페이지 편집기 및 사이트 콘솔이 WCAG 대비, 키보드 및 화면 판독기 요구 사항을 충족하는 데 도움이 됩니다.
* 현지화. 수십 개의 수정 사항이 Sites, Assets, 보안 및 작업 전반에 걸쳐 문자열을 번역하고 레이아웃 문제를 수정합니다.
* 신뢰성. 게시 인스턴스, MSM 롤아웃, 리치 텍스트 편집기 도구 모음 작업 및 클래식 UI의 페이지 활성화에 대한 GraphQL 잠금 경합 문제를 해결합니다.
* 분석. Launch 통합에서는 2026년 8월 31일 Analytics 1.4 서비스 종료에 앞서 Adobe Analytics 2.0 API를 사용합니다.


<!-- UPDATE FOR EACH NEW RELEASE -->

## 서비스 팩 26의 문제, 개선 사항 및 개선 사항이 수정되었습니다. {#fixed-issues}

<!-- 6.5.25.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->


### [!DNL Sites]{#sites-6526}

#### 접근성 {#sites-accessibility-6526}

* 작성자는 키보드만 사용하여 구성 요소를 추가, 이동 및 제거할 수 있습니다. 드래그 앤 드롭 상호 작용에는 포인터가 필요하므로 WCAG 2.1.1 키보드 기준에 실패했습니다. 이제 편집기에서 키보드 작동 가능한 해당 항목으로 구성 요소 삽입 팝업, 잘라내기 및 붙여넣기, 삭제 를 제공합니다. (SITES-25359)

* 작성자는 이제 텍스트 구성 요소 인라인 메뉴에서 활성 형식(&quot;T&quot;) 버튼을 볼 수 있습니다. 작성자가 굵게 또는 기울임꼴 서식을 적용한 후 단추 아이콘이 어두운 회색 배경에 대해 어두운 상태를 유지했으며 WCAG 2.1 AA 최소 명암비 4.5:1을 놓쳤습니다. 업데이트된 CSS는 아이콘을 가볍게 하여 이전 서비스 팩이 제공했던 대비를 복원합니다. (SITES-51864)

* 이제 이미지 드롭다운에서 단락을 선택하면 페이지 편집기의 Assets 탭에 구성 요소 선택 드롭다운에 번역된 문자열이 표시됩니다. 이전에는 현지화 리소스가 부족하여 문자열 &quot;OTHER&quot;가 영어로 표시되었습니다. 업데이트된 사전은 모든 로케일에서 번역을 제공합니다. (SITES-24525)




* 이제 페이지 편집기의 ContextHub iframe에는 설명 제목 속성이 있습니다. 이전에는 `contexthub-ui-iframe` 요소에 제목이 없으므로 포커스를 이동할 때 화면 판독기 사용자가 해당 요소를 식별하지 못했습니다. 이제 캔버스, 사이드 레일 및 레이아웃 미리 보기를 포함하여 모든 편집기 페이지 및 보기에 제목이 표시됩니다. (SITES-24650)
* 사이트 콘솔 필터 레일의 필터 버튼은 저장된 검색 및 검색 디렉토리 선택 필드 위에 표시되는 레이블을 추가하지 않습니다. 감사에 따르면 포커스가 버튼을 떠날 때, 키를 누를 때 또는 버튼을 클릭할 때 레이블이 표시된다고 보고했습니다. 테스트가 비헤이비어를 재현하지 못했으므로 변경할 필요가 없습니다. (SITES-24706)
* 이제 사이트 콘솔 앱 탐색의 링크가 더 선명하게 표시됩니다. 링크 텍스트는 4.5:1 대비를 충족했지만 글꼴 두께가 얇고 크기가 작아 링크를 쉽게 볼 수 없었습니다. 글꼴 무게가 더 크고 크기가 클수록 시각 장애가 있는 사용자는 텍스트를 더 쉽게 읽을 수 있습니다. (SITES-24723)
* 화면 판독기에서 더 이상 사용자 환경 설정 모달의 툴팁 콘텐츠 앞에 &quot;공백&quot;이 표시되지 않습니다. 이전에는 정보 아이콘이 `aria-labelledby` 참조와 함께 `role="tooltip"`을(를) 사용했으므로 NVDA가 먼저 빈 레이블을 읽습니다. 이제 아이콘에서 `role="button"` 및 `aria-label`의 &quot;정보&quot;를 사용하며, 변경 사항은 패턴을 공유하는 Coral 양식 구성 요소에 적용됩니다. (SITES-24732)
* 삭제 모달의 삭제 버튼은 이제 4.5:1의 WCAG 1.4.3 대비 요구 사항을 충족합니다. 이전에는 작성자가 항목을 선택하고 작업 도구 모음에서 삭제 를 클릭한 후 빨간색 배경의 흰색 텍스트에 3.9:1의 비율이 제공되었습니다. 어두운 단추 색상을 사용하면 시각 장애가 있는 작성자가 레이블을 읽을 수 있습니다. (SITES-24772)
* 이제 사이트 콘솔 참조 레일의 참조 머리글에서 `div` 대신 제목 요소를 사용합니다. 이전에는 화면 판독기에서 텍스트를 제목으로 알리지 못했으므로 사용자가 제목으로 탐색하지 못했습니다. 초기 참조 보기의 위쪽에 머리글도 나타납니다. (SITES-24967)
* 사이트 콘솔 필터 레일의 아코디언 버튼에 대한 포커스 표시기가 이제 WCAG 1.4.11 대비 요구 사항 3:1을 충족합니다. 이전에는 파란색 표시기가 배경에 대해 2.3:1의 비율을 나타내어 키보드 사용자에게는 태그 아코디언 버튼을 찾기 어려웠습니다. 업데이트된 색상은 키보드 사용자에게 선명한 포커스 큐를 제공합니다. (SITES-24986)
* 사이트 콘솔 필터 레일의 라디오 버튼에 대한 포커스 표시기가 이제 WCAG 1.4.11 대비 요구 사항 3:1을 충족합니다. 이전에는 옅은 파란색 표시기가 배경에 대해 1.7:1의 비율을 보였다. 이제 키보드 사용자는 수정된 날짜 아코디언에서 자신의 위치를 추적할 수 있습니다. (SITES-24987)
* 페이지 편집기 측면 레일의 경로 및 태그 필드 옆에 있는 선택 버튼은 더 이상 확인란 아이콘을 사용하지 않습니다. 이전에는 아이콘이 전환을 제안했지만 버튼을 활성화하면 트리 디렉터리가 포함된 모달이 열렸습니다. 이제 선택 버튼이 해당 기능을 올바르게 전달하며, 이미지 및 티저 모달에도 동일하게 적용됩니다. (SITES-25210)
* 이제 화면 판독기에서 페이지 편집기 측면 레일의 에셋 썸네일 이미지를 건너뜁니다. 이전에는 각 이미지에 표시되는 에셋 이름이 중복되는 대체 텍스트가 있으므로 사용자는 동일한 텍스트를 두 번 들었습니다. 빈 `alt` 특성은 이미지를 장식용으로 표시하고 카드 제목에 이름을 유지합니다. (SITES-25213)
* 화면 판독기는 사이드 레일 구성 요소 목록을 목록으로 인식합니다. 감사에서 관련 없는 요소로 항목을 보고했지만 테스트에서 마크업이 목록 요소와 목록 항목을 사용하는지 확인했습니다. 코드를 변경할 필요가 없습니다. (SITES-25214)
* 페이지 편집기 측면 레일의 구성 요소에 대한 정보 아이콘은 더 크고 쉽게 볼 수 있습니다. 이전에는 아이콘에서 약 12px의 매우 작은 크기를 사용했으며, 이 크기는 시각 장애가 있는 사용자가 보기 어려운 크기입니다. 이제 아이콘은 중간 크기를 사용합니다(SITES-25217).
* 이제 주석 모달의 견본 버튼에 대한 포커스 표시기가 버튼에서 두드러집니다. 이전에는 표시기가 견본 색상과 일치했습니다. 이 때문에 키보드 사용자는 어떤 단추에 초점이 있는지 확인하기 어려웠습니다. 오프셋은 표시기에 배경에 대한 충분한 대비를 제공하고 명확하게 보이도록 합니다. (SITES-25253)
* 타임워프 모달의 날짜 필드는 더 이상 `aria-haspopup="dialog"`을(를) 전달하지 않습니다. 이전에는 필드에 대화 상자가 열리지 않음에도 불구하고 대화 상자가 열린다고 화면 판독기가 발표했습니다. 속성을 제거하면 화면 판독기 사용자에게 정확한 정보가 제공됩니다. (SITES-25263)
* 인구 통계 도구 모음의 텍스트 레이블(예: &quot;권장&quot;)이 WCAG 1.4.3 대비 요구 사항 4.5:1을 충족합니다. 이전에는 어두운 회색 배경의 회색 텍스트가 [미리 보기] 모드에서 2.8:1의 비율을 제공했습니다. 배경에 따라 텍스트가 더 어둡거나 밝으면 모든 레이블을 읽을 수 있습니다. (SITES-25307)
* 인구 통계 도구 모음의 Commerce, 사용자 및 장치 버튼에 대한 포커스 표시기가 이제 WCAG 1.4.11 대비 요구 사항 3:1을 충족합니다. 이전에는 표시기가 도구 모음 배경에 대해 1.9:1의 비율을 보였습니다. 이제 키보드 사용자는 자신의 위치를 추적할 수 있습니다. (SITES-25308)
* 작성자가 인구 통계 도구 모음 텍스트 필드에 입력하는 텍스트가 이제 4.5:1이라는 WCAG 1.4.3 대비 요구 사항을 충족합니다. 이전에는 회색 배경의 흰색 텍스트로 미리 보기 모드의 프로필 드롭다운 `displayName` 필드와 같은 필드에서 2.9:1의 비율이 생성되었습니다. 업데이트된 색상은 시각 장애가 있는 작성자가 입력 값을 읽을 수 있도록 합니다. (SITES-25318)
* 이제 [티저], [이미지] 및 [슬라이드] 대화 상자의 확인란에 포커스가 도달하면 화면 판독기에서 설명 툴팁을 읽습니다. 이전에는 텍스트가 확인란과 프로그래밍 방식으로 연결되지 않아 사용자가 지침을 듣지 못했습니다. 이제 `aria-describedby` 특성은 각 확인란을 해당 설명에 연결합니다. (SITES-25364)
* 이제 화면 판독기에 리치 텍스트 편집기에서 활성화된 단락 형식 버튼이 표시됩니다. 이전에는 목록에서 선택 사항을 선택하면 보조 기술에 현재 선택 사항이 표시되지 않았습니다. 이제 활성 단추는 `aria-current="true"`을(를) 포함하고 활성 하이퍼링크 대상 옵션은 `aria-selected="true"`을(를) 포함합니다. (SITES-25367)
* 이제 사이트 콘솔 목록 보기의 테이블 헤더에 있는 정렬 버튼이 WCAG 1.4.11 대비 요구 사항 3:1을 충족합니다. 이전에는 밝은 회색 아이콘이 머리글 배경에 대해 1.5:1의 비율을 표시했습니다. 아이콘 색상이 어두우면 시각 장애가 있는 작성자가 버튼을 볼 수 있습니다. (SITES-25372)
* 포커스를 필터 필드로 이동하면 페이지 편집기 측면 레일의 Assets 탭이 더 이상 다시 로드되지 않습니다. 이전에는 빈 필드에 탭하면 다시 로드가 트리거되었으며 화면 판독기에서 매번 로드 메시지를 발표했습니다. 이제 필터 값을 변경하고 Enter 키를 누른 후에만 탭이 다시 로드됩니다. (SITES-25377)
* 주석 모달에서 선택한 견본 아이콘이 3:1의 WCAG 1.4.11 대비 요구 사항을 충족합니다. 기존에는 흰색 체크 표시가 노란색, 주황색, 녹색 색상 견본에 대해 1.58:1로 낮은 비율을 보였다. 업데이트된 아이콘은 시각 장애가 있는 작성자에게 명확한 표시기를 제공합니다. (SITES-25523)
* 페이지 편집기 사이드 패널의 구성 요소 목록은 더 이상 키보드 포커스를 받지 않습니다. 키보드 사용자는 콘텐츠 창의 컨트롤로 구성 요소를 선택하고 이동할 수 있으므로 사이드 패널 목록에서 해당 기능이 반복됩니다. 구성 요소 필터 아래에 있는 메모는 키보드 사용자에게 컨트롤을 찾을 위치를 알려 줍니다. (SITES-40752)


#### 관리 사용자 인터페이스{#sites-adminui-6526}


#### 클래식 UI{#sites-classicui-6526}

* 작성자는 클래식 UI 사이트 콘솔(`siteadmin.html`)에서 페이지를 다시 활성화할 수 있습니다. 이전에는 추적 스크립트가 실패하여 클릭 처리기가 중지되었으므로 페이지 활성화 버튼이 &quot;로드 중&quot; 회전자를 무기한 표시했으며 복제를 트리거하지 않았습니다. 이제 클릭 처리기가 오류 없이 실행되고 활성화를 완료합니다. (SITES-52165)
* 이제 인도네시아 언어 코드가 언어 복사 속성에 ID로 표시됩니다. 이전에는 참조 레일에서 인도네시아어 언어 루트 아래의 페이지에 대한 이전 코드 IN을 표시했습니다. cq-wcm-core 번들 업데이트는 값을 수정하므로 코드가 ISO 표준과 일치합니다. (SITES-4491)

<!--
#### Component Console{#sites-component-console-6526}



#### [!DNL Content Fragments]{#sites-contentfragments-6526}



#### [!DNL Content Fragments] - Admin{#sites-admin-6526}
-->


#### [!DNL Content Fragments] - 조각 편집기{#sites-fragments-editor-6526}

* 콘텐츠 조각 편집기의 각 다중 필드 참조에 대해 콘텐츠 조각 편집 버튼이 즉시 표시됩니다. 이전에는 작성자가 상위 조각을 저장할 때까지 버튼이 표시되지 않았고 경로 브라우저를 연 후에도 아무 작업도 수행되지 않았습니다. 이제 편집기는 첫 번째 렌더링에 대해 작업 목록을 빌드하므로 작성자는 추가 단계 없이 참조된 조각을 엽니다. (SITES-43733)

* 중국어, 일본어 및 한국어 문자는 더 이상 콘텐츠 조각 만들기 대화 상자 자리 표시자에서 기울임꼴로 표시되지 않습니다. 이전에는 기울임꼴 스타일이 **Assets** > **파일** 아래의 한중일 문자에 적용되어 텍스트를 읽기 어려웠습니다. 업데이트된 스타일은 CJK 언어에 대한 이탤릭체를 건너뜁니다. (SITES-43548)
* 콘텐츠 조각 편집기는 Granite UI 업데이트 후 필드를 올바르게 확인합니다. 최근 Granite UI가 변경되어 회귀가 발생했으므로 편집기 클라이언트 라이브러리는 더 이상 새 유효성 검사 동작과 일치하지 않습니다. 조정된 라이브러리와 테스트는 불일치를 해결합니다. (SITES-46650)


#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6526}

* 이제 컨텐츠 조각의 GraphQL 쿼리는 OpenAPI Assets을 사용하여 Dynamic Media에 대한 RemoteRef 참조를 인식합니다. 이전에는 AEM 6.5 Sites에서 AEM as a Cloud Service Assets을 사용할 때 &quot;지속 쿼리 유효성 검사 오류&quot; 때문에 쿼리가 실패하고 에셋 데이터가 반환되지 않았습니다. 이제 응답에는 저장소 ID 및 에셋 ID가 포함되므로 클라이언트가 게재 URL을 작성할 수 있습니다. (SITES-48507)

* 게시 인스턴스는 GraphQL 트래픽이 많은 동안 응답형으로 유지됩니다. `GraphQLServiceImpl`의 잠금 경합 시 스키마 메서드에서 요청 처리 스레드가 지연되어 요청이 느려지고 다시 시작해야 합니다. 향상된 동기화 기능은 성능 제한을 해결하고 사이트 및 모바일 앱의 가용성을 유지합니다. (SITES-48699)

* GraphQL 엔드포인트 페이지의 메시지는 페이지를 다시 로드한 후에도 현지화된 상태로 유지됩니다. 이전에는 엔드포인트를 만들고 삭제할 때 &quot;엔드포인트를 찾을 수 없음&quot; 메시지가 언어로 표시되었지만 다시 로드한 후 영어로 되돌아갔습니다. 이제 페이지는 모든 방문에 대해 번역된 문자열을 로드합니다. (SITES-43586)


<!--
#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6526}
-->


#### [!DNL Content Fragments] - 모델 및 모델 편집기{#sites-models-model-editor-6526}

* 구성 이름에 &quot;español テスト&quot;와 같은 현지화된 문자가 포함된 경우 콘텐츠 조각 모델의 썸네일이 **도구** > **일반** > **콘텐츠 조각 모델**&#x200B;에 표시됩니다. 이전에는 문자에서 경로에 오류가 발생하여 업로드된 썸네일이 표시되지 않았습니다. 업데이트된 처리는 이름을 올바르게 인코딩합니다. (SITES-39242)

* 이제 콘텐츠 조각 모델 편집기 캔버스의 필드 레이블 문자열이 사용자의 언어로 표시됩니다. 이전에는 작성자가 구성 요소를 캔버스로 드래그한 후에도 레이블이 영어로 유지되었으며, 모델을 저장하고 다시 연 후에만 번역되었습니다. 이제 레이블이 속성 패널과 일치하도록 즉시 번역됩니다. (SITES-45383)


<!--
#### [!DNL Content Fragments] - REST API{#sites-restapi-6526}

#### ContextHub{#sites-contexthub-6526}
-->


#### 핵심 백엔드{#sites-core-backend-6526}

* 이제 온-오프-타임을 통해 예약된 페이지 활성화가 필요한 경우에만 실행됩니다. `OnOffTriggerProcessor`은(는) 이전에 복제 및 캐시 무효화를 너무 자주 트리거하여 작성자가 콘텐츠를 수동으로 다시 게시하도록 했습니다. 백포트된 수정 사항은 불필요한 처리를 제거하고 신뢰할 수 있는 예약된 게시를 복원합니다. (SITES-48483)

* 파일 업로드는 다중 필드의 차세대 자산 관리에서 원격 자산에 대해 작동합니다. 이전에는 작성자가 다중 필드 내의 필드에 대한 원격 자산을 선택할 때 업로드가 실패했습니다. 핵심 구성 요소 업데이트는 업로드 흐름을 복원하므로 필드에서 에셋을 수락합니다. (SITES-44266)


#### 핵심 구성 요소{#sites-core-components-6526}

* 원격 자산 선택기는 각 다중 필드 항목의 이미지를 별도로 유지합니다. 이전에는 하나의 다중 필드 항목에서 이미지를 선택하면 다른 모든 항목에 적용되었으며 원격 자산 참조가 저장되지 않았습니다. 이제 각 항목에 고유한 선택 항목이 있고 대화 상자를 저장한 후에도 참조가 유지됩니다. (SITES-42376)

* 이 릴리스에는 Commerce, 핵심 구성 요소, 기초 구성 요소(이전), 실행 및 MSM 라이브 카피에 대한 백포트 수정 사항이 포함되어 있습니다. 이 수정 사항에서는 보안 취약점, XSS(크로스 사이트 스크립팅) 위반, 파일 업로드 동작 및 라이브 카피 동작을 해결합니다. 백포트는 AEM as a Cloud Service에서 이전에 제공된 수정 사항에 따라 AEM 6.5 및 AEM 6.5 LTS를 제공합니다. (SITES-43738)


<!--
#### Campaign integration{#sites-campaign-integration-6526}

#### ContentHub {#sites-contenthub-6526}

#### Crosswalk {#sites-crosswalk-6526}

#### Experience Fragments{#sites-experiencefragments-6526}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-6526}
-->


#### 헤드리스 - 관리자 {#sites-headless-admin-6526}

개선 사항: 이제 Headless 관리자의 미리보기 보기가 선택한 변형 경로를 미리보기 구성 요소에 전달합니다. 이 변경 사항으로 여러 변형이 있는 콘텐츠 조각 미리보기가 올바른 변형의 콘텐츠를 로드하게 됩니다. `draftFragmentIds` 배열에 변형 매개 변수가 포함되어 있습니다. (SITES-42714)


#### 론치{#sites-launches-6526}

* 이제 홍보된 시작에 대한 타임라인 항목이 사용자의 언어로 표시됩니다. 이전에는 작성자가 론치를 홍보하고 Sites에서 사이트에 대한 타임라인을 연 후에도 &quot;만든 버전&quot;과 &quot;론치를 홍보하기 전&quot; 문자열이 영어로 유지되었습니다. 업데이트된 리소스는 모든 로케일의 번역을 제공합니다. (SITES-13389)
* 론치 필터 패널에 있는 론치 Source 자리 표시자의 경로 선택 이 완전히 표시됩니다. 이전에는 텍스트가 필드에 맞지 않아 프랑스어, 이탈리아어 및 포르투갈어와 같이 현지화된 인터페이스에서 잘렸습니다. 업데이트된 레이아웃은 전체 자리 표시자를 표시합니다. (SITES-42792)
* 도구 > 사이트 > 실행 의 라이브 날짜 열에는 더 이상 독일어, 프랑스어, 스페인어, 이탈리아어, 포르투갈어(브라질) 및 중국어 번체 로케일에서 AM 또는 PM이 표시되지 않습니다. 이전에는 열에서 해당 로케일과 일치하지 않는 12시간 형식을 사용했습니다. 이제 열에 24시간 형식이 표시됩니다. (SITES-43178)


<!--
#### Link Checker{#sites-link-checker-6526}
-->


#### 현지화{#sites-localization-6526}

* **도구** > **작업** 아래의 상태 보고서 페이지의 문자열이 사용자의 언어로 표시됩니다. 이전에는 리소스 검색 경로, 유지 관리, 복제 큐, 로그 오류, 활성 번들 및 요청 성능에 대한 메시지가 영어로 유지되었습니다. 업데이트된 i18n 리소스는 번역을 제공하고 대체 파일이 문자열을 사용할 수 있도록 합니다. (NPR-44279)

* 이제 &quot;수동으로 추가 옵션을 선택하면 &#39;JSON 경로&#39; 설정이 무시됩니다.&quot; 오류 메시지가 **도구** > **Assets** > **메타데이터 스키마** 콘솔에 사용자 언어로 표시됩니다. 이전에는 작성자가 드롭다운 요소를 추가하고, JSON 경로를 통해 추가 를 선택하고, 수동으로 추가 로 전환한 후에도 메시지가 영어로 유지되었습니다. 업데이트된 리소스는 번역을 제공합니다. (ASSETS-31575)
* 이제 **Assets** > **관리** 태그의 &quot;홍보된&quot; 문자열이 사용자의 언어로 표시됩니다. 이전에는 [홍보]를 선택한 후 스마트 태그를 마우스로 가리키면 문자열이 영어로 유지되었습니다. 업데이트된 리소스는 모든 로케일에서 번역을 제공합니다. (ASSETS-36070)
* 추가 단추 레이블이 **폴더 속성** > **자산 기여도**&#x200B;의 단추와 더 이상 겹치지 않습니다. 이전에는 &quot;에셋 기여도&quot; 설정이 있는 폴더를 만든 후 독일어, 이탈리아어 및 포르투갈어 인터페이스에서 텍스트가 버튼과 충돌했습니다. 업데이트된 스타일은 더 긴 번역된 레이블에 충분한 공간을 제공합니다. (ASSETS-36746)
* 이제 Assets 목록 보기의 열 제목이 일본어 인터페이스에 가로로 표시됩니다. 이전에는 제목이 **Assets** > **파일** 아래의 목록 보기와 콘텐츠 조각 편집기의 카드 보기에 세로로 표시되었습니다. 업데이트된 `cq-dam-content` 패키지는 텍스트 방향을 수정합니다(ASSETS-43105).
* 이제 Assets 열 보기의 게시 상태 &quot;나중에 예약됨&quot;이 사용자의 언어로 표시됩니다. 이전에는 작성자가 자산을 선택하고, **게시 관리**&#x200B;를 선택하고, **나중에** 옵션을 선택하고, 날짜를 추가하고, 게시한 후에도 문자열이 영어로 유지되었습니다. 업데이트된 `cq-dam-content` 패키지는 모든 로케일에서 번역을 제공합니다. (ASSETS-43307)
* 이제 **스마트 태그 구성** 탭의 문자열이 프랑스어 및 포르투갈어(브라질)용으로 모두 표시됩니다. 이전에는 **도구** > **클라우드 서비스** > **스마트 태그**&#x200B;에서 **만들기**&#x200B;를 클릭한 후 텍스트가 잘렸습니다. 툴팁 없이 텍스트를 읽으려면 충분한 공간을 제공하는 CSS 업데이트를 사용하십시오. (ASSETS-68045)
* 이제 Assets 관리 검색 레일의 &quot;다중 경로 값 속성 조건자&quot; 문자열이 사용자 언어로 표시됩니다. 이전에는 관리자가 **도구** > **일반** > **검색** 양식에서 검색 양식을 편집하고 조건자를 양식으로 드래그하면 문자열이 영어로 유지되었습니다. 업데이트된 `cq-dam-content` 패키지가 번역을 제공합니다(CQ-4336103).
* 프로젝트 보기의 Aria 레이블이 이제 사용자의 언어로 표시됩니다. 이전에는 각 프로젝트 타일의 작업 버튼에 액세스 가능한 이름이 없었고, 타일 구성 작업에서는 형제 레이블이 현지화된 동안 하드 코딩된 영어 레이블을 사용했습니다. 업데이트된 타일 스크립트는 두 작업에 대해 현지화된 레이블을 제공합니다. (CQ-4352359)
* 이름에 중국어, 일본어 또는 한국어 문자가 있는 스마트 컬렉션이 이제 올바르게 저장됩니다. 이전에는 이름에 CJK 문자가 포함된 경우 &quot;**Assets** > **파일** > **필터**&#x200B;에서 컬렉션을 저장하지 못했습니다. &quot;검색 저장 실패 - 잘못된 요청, 중복된 컬렉션은 사용할 수 없습니다.&quot; 이제 중복 검사는 노드 이름이 아닌 컬렉션 제목을 비교하므로 다른 CJK 제목을 가진 컬렉션이 더 이상 충돌하지 않습니다. (GRANITE-62592)
* 이제 **보안** > **사용자** > **만들기**&#x200B;의 국가/지역 드롭다운에서 사용자의 언어로 이름을 알파벳순으로 정렬합니다. 이전에는 영어 순으로 정렬된 이름과 현지화된 이름이 표시되었기 때문에 일본어와 같은 로케일에서 국가가 순서가 맞지 않는 것으로 나타났습니다. 업데이트된 `com.adobe.granite.security.content` 번들은 로케일 인식 규칙을 사용하여 정렬됩니다. (GRANITE-67789)
* **도구** > **작업** > **유지 관리**&#x200B;의 AuditLog 유지 관리 작업에 대한 면책조항이 이제 사용자의 언어로 표시됩니다. 이전에는 감사 로그 삭제 및 준수 요구 사항에 대한 경고가 주간 유지 관리 창에서 사용자가 면책조항 아이콘을 클릭한 후에도 영어로 유지되었습니다. 업데이트된 리소스는 모든 로케일에서 번역을 제공합니다. (NPR-44189)
* 이제 **보안** > **권한** > **감사 보기**&#x200B;의 권한 이름이 사용자 언어로 표시됩니다. 이전에는 번역본이 없어 이름이 영어로 표시됐다. 업데이트된 `com.adobe.granite.platform.i18n` 번들이 해당 번들을 제공합니다. (NPR-44477)
* 이제 **보안** > **Adobe IMS 구성**&#x200B;의 상태 확인 대화 상자가 사용자의 언어로 표시됩니다. 이전에는 번역이 누락되었기 때문에 대화 상자에 현지화된 인터페이스에 영어 문자열이 표시되었습니다. 업데이트된 `com.adobe.granite.platform.i18n` 번들이 해당 번들을 제공합니다. (NPR-44479)
* **도구** > **작업** > **진단** 아래의 사용자 동기화 진단 도구의 문자열이 이제 사용자의 언어로 표시됩니다. 이전에는 도구가 현지화된 인터페이스에서 영어 텍스트를 표시했습니다. 업데이트된 `com.adobe.granite.platform.i18n` 번들이 번역을 제공합니다. (NPR-44481)
* 이제 구성 흐름에 사용자에게 친숙한 오류 메시지가 사용자 언어로 표시됩니다. 이전에는 AEM 구성 페이지에서 오류가 발생하면 기술 텍스트나 번역되지 않은 텍스트가 생성되었습니다. 업데이트된 `com.adobe.granite.ui.content` 번들은 오류를 처리하고 지역화된 메시지를 제공합니다. (NPR-44840)
* **보안** > **그룹**&#x200B;에서 삭제된 그룹의 속성을 변경하면 표시되는 오류 메시지가 사용자의 언어로 표시됩니다. 이전에는 현지화된 인터페이스에 대해 메시지가 영어로 유지되었습니다. 업데이트된 `com.adobe.granite.security.content` 번들이 번역을 제공합니다. (NPR-44841)
* 오류 메시지 &quot;그룹에 변경 사항을 저장할 때 문제가 발생했습니다!&quot; 이제 **보안** > **그룹** > **그룹 편집** 콘솔에서 사용자의 언어로 표시됩니다. 이전에는 현지화된 인터페이스에 대해 메시지가 영어로 유지되었습니다. 업데이트된 `com.adobe.granite.security.content` 번들이 번역을 제공합니다. (NPR-44842)
* 받은 편지함 아이콘 오류 메시지에 중국어, 일본어 및 한국어 문자가 더 이상 이탤릭체로 표시되지 않습니다. 이전에는 이탤릭체 스타일이 문자를 왜곡하여 텍스트를 읽기 어렵게 만들었습니다. 업데이트된 `com.adobe.granite.ui.coralui3` 번들은 해당 언어의 스타일을 제거합니다. (NPR-44843)
* **작업** > **모니터링**&#x200B;의 숫자는 이제 사용자의 로케일 형식을 따릅니다. 이전에는 페이지에 인터페이스 언어와 관계없이 고정된 형식의 숫자가 표시되었습니다. 업데이트된 `com.adobe.granite.monitoring.dashboard` 번들은 올바른 구분 기호와 형식을 적용합니다. (NPR-44844)
* 이제 쿼리 설명 탭에 &quot;Query Builder 디버거 도구&quot;가 표시됩니다. 사용자 언어로 링크됩니다. 이전에는 문자열이 외부화되지 않았기 때문에 현지화된 인터페이스에서 링크 텍스트가 누락되었습니다. 업데이트된 `com.adobe.granite.monitoring.dashboard` 번들이 이 번들을 복원합니다. (NPR-44845)
* 이제 Query Builder 디버거 도구 대화 상자의 텍스트가 쿼리 설명 탭에 사용자 언어로 표시됩니다. 이전에는 일부 문자열이 외부화되지 않아 영어로 유지되었습니다. 업데이트된 `cq-platform-content` 번들이 번역을 제공합니다. (NPR-44846)
* 이제 일관성 검사 결과 페이지의 텍스트가 사용자의 언어로 표시됩니다. 이전에는 외부화되지 않아 여러 문자열이 영어로 표시되었습니다. 업데이트된 `com.adobe.granite.operations.ui.core` 번들이 번역을 제공합니다. (NPR-44847)
* 이제 모니터링 차트에 사용자의 언어로 월 및 주 레이블이 표시됩니다. 이전에는 레이블이 영어로 하드 코딩되었으므로 차트가 인터페이스 로케일을 무시했습니다. 업데이트된 `com.adobe.granite.monitoring.dashboard` 번들은 문자열을 외부화하고, 이제 번역이 나타납니다. (NPR-44848)
* 이제 **보안** > **사용자** > **만들기**&#x200B;의 국가/지역 드롭다운에서 항목을 올바르게 정렬합니다. 이전에는 일부 언어에서 현지화된 국가 이름이 잘못된 순서로 표시되었습니다. 업데이트된 `com.adobe.granite.security.content` 번들은 로케일 인식 정렬을 적용합니다. (NPR-44942)
* 이제 버튼 구성 요소 대화 상자의 도구 설명이 사용자의 언어로 표시됩니다. 이전에는 현지화 서비스에 문자열이 있어도 단추 텍스트, 링크, 아이콘, HTML ID 및 `aria-label` 필드에 대한 정보 텍스트가 영어로 유지되었습니다. 업데이트된 사전은 지원되는 모든 로케일에서 번역을 제공합니다. (SITES-7579)
* 이제 콘텐츠 조각 목록 구성 요소의 속성 섹션에 있는 도구 설명이 사용자의 언어로 표시됩니다. 이전에는 콘텐츠 조각 모델, 태그, 최대 항목 수, 상위 경로, 정렬 순서 및 정렬 기준 필드에 대한 정보 텍스트가 영어로 유지되었습니다. 업데이트된 사전은 지원되는 모든 로케일에 대한 번역을 제공합니다. (SITES-14969)
* 이제 템플릿 편집기의 핵심 구성 요소에 대한 도움말 링크를 통해 현지화된 설명서 페이지가 제공됩니다. 이전에는 구성 요소 구성 대화 상자에서 도움말을 선택하면 인터페이스 언어와 관계없이 영어 페이지가 열렸습니다. 업데이트된 URL이 이제 해당 로케일에 대한 페이지로 사용자를 보냅니다. (SITES-15058)
* 이제 콘텐츠 조각 대화 상자의 정보 도구 설명이 사용자의 언어로 표시됩니다. 이전에는 단일 텍스트 요소 및 다중 요소 모드와 콘텐츠 조각 경로에 대한 도구 설명 텍스트가 영어로 유지되었습니다. 업데이트된 사전은 모든 로케일에 대한 번역을 제공합니다. (SITES-17333)
* 이제 템플릿 편집기 구성 요소 정책 편집기의 오류 메시지가 사용자 언어로 표시됩니다. 이전에는 작성자가 구성 요소 정책을 편집하거나 새 정책을 만들 때 &quot;리소스 {}을(를) 수정할 수 없음&quot; 및 &quot;노드를 만들 수 없음&quot;이라는 메시지가 영어로 유지되었습니다. 업데이트된 리소스는 지원되는 모든 로케일에 대한 번역을 제공합니다. (SITES-17475)
* 이제 이미지 드롭다운에서 단락을 선택하면 페이지 편집기의 Assets 탭에 구성 요소 선택 드롭다운에 번역된 문자열이 표시됩니다. 이전에는 현지화 리소스가 부족하여 문자열 &quot;OTHER&quot;가 영어로 표시되었습니다. 업데이트된 사전은 모든 로케일에서 번역을 제공합니다. (SITES-21481)
* 페이지 편집기 구성 요소 대화 상자의 정보 도구 설명에 더 이상 추가 줄 바꿈이 표시되지 않습니다. 이전에는 PDF Viewer 및 진행률 표시줄과 같은 구성 요소에 대한 도구 설명이 여러 로케일에서 어색하게 줄바꿈되었습니다. 이제 도구 설명이 올바르게 줄 바꿈되고 단어 하이픈이 예상대로 작동합니다. (SITES-38567)
* 이제 도구 설명 &quot;텍스트 편집기를 종료하려면 Esc 키를 누르십시오&quot;가 텍스트 구성 요소 구성 대화 상자의 사용자 언어로 표시됩니다. 이전에는 현지화 리소스에 문자열이 없으므로 문자열이 영어로 표시되었습니다. 이제 도구 설명이 모든 로케일로 변환됩니다. (SITES-43186)
* 이제 템플릿 편집기의 STRUCTURE 레이블이 사용자 언어로 표시됩니다. 이전에는 현지화 리소스에서 문자열이 누락되었기 때문에 작성자가 적응형 양식 템플릿을 열 때 레이블이 영어로 유지되었습니다. 이제 레이블이 모든 로케일로 변환됩니다. (SITES-43599)


#### MSM - Live Copy{#sites-msm-live-copies-6526}

* MSM 롤아웃 대화 상자는 업그레이드 후 라이브 카피 목록을 다시 로드합니다. 이전에는 `AsyncOperationServlet.doGet`의 `NullPointerException`이(가) 회전판에서 대화 상자를 중지했으므로 작성자가 대상 로케일을 선택하거나 롤아웃을 시작하지 못했습니다. 업데이트된 `com.adobe.granite.jobs.async` 번들이 누락된 작업 데이터를 처리하고 요청을 완료합니다. (SITES-43116)
* 블루프린트 페이지의 편집 가능한 도구 모음에서 롤아웃이 다시 작동합니다. `MSM.Rollout` 클라이언트 라이브러리가 로드되지 않았기 때문에 도구 모음 작업이 &quot;정의되지 않은 속성을 읽을 수 없음(&#39;doRollout&#39; 읽기)&quot;으로 실패했습니다. 이제 업데이트된 페이지에 라이브러리가 로드되므로 롤아웃 작업이 시작되고 변경 사항이 라이브 카피에 도달합니다. (SITES-46052)

* 블루프린트 페이지 및 하위 페이지의 일괄 비활성화 시 더 이상 중복 롤아웃 이벤트가 전송되지 않습니다. 한 요청에서 상위 및 하위 페이지를 비활성화하면 복제 시스템에서 3개가 아닌 5개의 이벤트를 내보내고 각 하위 페이지가 두 번 롤아웃되었습니다. 이제 롤아웃 관리자의 중복 제거가 페이지당 하나의 롤아웃을 제출하므로 라이브 카피는 중복 패키지를 받지 않습니다. (SITES-44988)


#### 페이지 편집기{#sites-pageeditor-6526}

* 선택한 스타일은 목록을 스크롤한 후 페이지 편집기 스타일 선택 대화 상자에서 강조 표시된 상태로 유지됩니다. 이전에는 스타일을 선택하면 강조 표시되었지만 스크롤 막대를 클릭하면 강조 표시가 사라졌습니다. 이 회귀는 SP22 이후에 시작되었으며 이제 대화 상자가 선택한 상태를 계속 표시합니다. (SITES-30874)

* 작성자는 상위 및 하위 구성 요소가 서로 다른 응답형 중단점을 정의할 때 레이아웃 모드에서 페이지를 편집할 수 있습니다. 이전에 cq:responsive/phone 너비를 생략한 구성 요소에 TypeError가 발생하여 getResponsiveCssClasses 함수가 실패했습니다. 이제 함수가 사용 가능한 값으로 다시 돌아가 렌더링을 계속합니다. (SITES-46681)
* 이제 사용자 지정 자르기 비율은 여러 이미지 드롭 타겟이 있는 구성 요소에 대해 하이브리드 인라인 편집 모드에서 로드됩니다. 이전에는 이미지 편집기에서 모든 드롭 대상에 대해 하나의 일반 ipeConfig를 초기화했으므로 편집기에서 기본 비율만 표시하고 각 대상의 aspectRatios를 무시했습니다. 이제 편집기에서 선택한 드롭 대상에 대한 구성을 읽을 때 자르기는 인라인 및 전체 화면 보기 모두에 적용됩니다. (SITES-45771)
* 리치 텍스트 편집기에서 백스페이스를 눌러도 텍스트에 추가 인라인 스타일이 추가되지 않습니다. 굵게 텍스트 뒤에 줄바꿈을 제거하면 굵게 태그에 style=&quot;font-size: 0.8125rem; background-color: transparent;&quot;가 추가되었다고 고객이 보고했습니다. 최신 서비스 팩에 대한 테스트에서 동작을 재현하지 못했으므로 변경할 필요가 없습니다. (SITES-15883)


<!--
#### Replication{#sites-replication-6526}
-->


#### 서식 있는 텍스트 편집기{#sites-rte-6526}

* 리치 텍스트 편집기 도구 모음 단추는 응답형 보기 및 레이아웃 모드에서 작동합니다. 이전에는 클릭하면 버튼이 강조 표시되었지만 선택 사항이 변경되지 않고 대화 상자가 열리지 않았습니다. 업데이트된 편집기 스크립트는 형식을 적용하며, 편집 모드의 동작과 일치합니다. (SITES-44233)
* 작성자는 텍스트 구성 요소에 통화 및 상표 기호를 손실하지 않고 추가할 수 있습니다. 특수 문자 플러그인은 기호를 삽입했지만 편집기와 게시된 출력 모두에서 공백으로 표시됩니다. 수정된 처리는 각 기호를 입력된 대로 렌더링합니다. (SITES-46532)
* 리치 텍스트 편집기 도구 모음의 전체 화면 아이콘은 편집기를 다시 확장합니다. 이전에는 핵심 텍스트 구성 요소에서 아이콘을 클릭해도 아무 작업도 수행되지 않았으며 편집기는 인라인 크기로 유지되었습니다. 이제 작성자는 인라인 및 대화 상자 편집 시 긴 양식 콘텐츠를 위한 집중 작업 영역을 갖게 됩니다. (SITES-46396)


#### 사이트 관리자 UI{#sites-admin-ui-6526}

자산을 이전 버전으로 되돌리면 이제 카드 썸네일이 새로 고쳐집니다. 타임라인 클라이언트 라이브러리의 URL 인코딩 변경으로 인해 경로가 일치하지 않으므로 카드 조회가 실패하고 썸네일이 오래된 상태로 남아 있습니다. 인코딩된 경로와 원시 경로를 일치시키면 새로 고침이 복원됩니다. (SITES-46590)

<!--
#### Universal editor {#sites-universal-editor-6526}
-->

#### 워크플로우 확장 {#sites-workflow-extensions-6526}

이제 페이로드 보기에서 게시를 관리하는 워크플로용 Touch UI 패키지 편집기가 여러 페이지에 대해 시작됩니다. 이전에는 작성자가 Touch UI에서 워크플로를 시작했지만 더 이상 사용되지 않는 클래식 UI 패키지 편집기가 열렸습니다. 이제 작성자가 Touch UI를 종료하지 않고 페이로드를 검사합니다. (SITES-40928)


### [!DNL Assets] {#assets-6526}

* 개선 사항: AEM Assets 6.5에는 생성 AI 콘텐츠에 대한 C2PA(콘텐츠 보호 및 신뢰성) 준수를 위한 Coalition 지원이 포함되어 있습니다. 에셋 업데이트 워크플로우는 C2PA 자격 증명을 감지하고 메타데이터를 추출하며, 워크플로가 다시 생성하는 렌디션에 서명합니다. 서명은 각 AEM 인스턴스에서 로컬로 실행되므로 고객은 전용 서명 인프라가 필요하지 않습니다. (ASSETS-75868)

* 설명서 개선 사항: 새 공개 설명서에서는 C2PA 규정 준수를 유지하면서 자산 처리 파이프라인을 사용자 지정하는 방법을 설명합니다. 이 설명서에서는 렌디션 단계 전에 C2PA 자격 증명 감지 단계를 배치하는 방법과 각 AEM 인스턴스에서 로컬로 서명하는 방법을 다룹니다. 설명서에는 전용 또는 고객 소유 서명 인프라에 대한 제한 사항도 나와 있습니다. (ASSETS-76100)
* 이제 AEM 6.5 SP26 환경의 링크를 마우스로 가리키면 셸 헤더의 도움말 드롭다운이 열려 있습니다. 이전에는, 포인터가 목록에 들어오면 드롭다운이 닫히므로 작성자가 설명서, 커뮤니티 또는 지원 링크를 클릭하지 못했습니다. 업데이트된 `com.adobe.granite.ui.content` 번들은 포커스 검사를 연기하므로 포커스가 완전히 나갈 때만 메뉴가 닫힙니다. (ASSETS-65676)

<!--
#### [!DNL Dynamic Media]{#assets-dm-6526}
-->

### [!DNL Forms]{#forms-6526}

* 새로운 기능: 리치 텍스트 목록의 접근성 태그 지원. 이전에는 템플릿이 특정 구조를 따르는 경우에만 액세스 가능성 태그 트리에 목록 태그가 표시되었습니다. 이 요청은 기능을 제공하는 관련 티켓의 복제본으로 마감되었습니다. (LC-3923202)


<!--
#### Forms JEE {#forms-jee-6526}

#### Forms Designer {#forms-designer-6526}
-->


### 기초 {#foundation-6526}

* 이제 **보안** > **사용자** > **만들기** 사용자 대화 상자의 &quot;국가/지역&quot; 문자열이 사용자의 언어로 표시됩니다. 이전에는 레이블이 현지화된 인터페이스에 대해 영어로 유지되었습니다. 업데이트된 `com.adobe.granite.security.content` 번들이 번역을 제공합니다. (NPR-43882)
* 이제 AEM 6.5 SP26 환경의 링크를 마우스로 가리키면 셸 헤더의 도움말 드롭다운이 열려 있습니다. 이전에는, 포인터가 목록에 들어오면 드롭다운이 닫히므로 작성자가 설명서, 커뮤니티 또는 지원 링크를 클릭하지 못했습니다. 업데이트된 `com.adobe.granite.ui.content` 번들은 포커스 검사를 연기하므로 포커스가 완전히 나갈 때만 메뉴가 닫힙니다. (NPR-44686)
* 개선 사항: 이제 `HtmlLibraryManagerImpl` 쿼리에 노드 유형 태그가 포함되어 있어 쿼리에 항상 필요한 인덱스가 사용됩니다. 또한 이 서비스는 클라이언트 라이브러리를 찾지 못할 때 오류를 기록하여 관리자에게 문제를 알립니다. 업데이트는 서비스 팩의 `com.adobe.granite.clientlibs` 번들 버전에 영향을 줍니다. (NPR-44698)


<!--
#### Apache Felix {#foundation-apachefelix-6526}
-->


#### 인증 {#foundation-authentication-6526}

사용자 편집기에서 저장 및 닫기 는 이제 현재 검색의 검색 결과로 돌아갑니다. 이전에는 작성자가 Omnisearch에서 두 번째 사용자를 검색하고, 속성을 편집하고, 저장 및 닫기를 클릭하면 페이지가 대신 첫 번째 사용자의 속성을 열었습니다. 업데이트된 UserProperties.js 스크립트는 예상 탐색을 복원합니다. (NPR-44774)

<!--
#### Campaign{#foundation-campaign-6526}

#### Cloud Services{#foundation-cloudservices-6526}

#### Communities {#foundation-communities-6526}

#### Content distribution{#foundation-content-distribution-6526}

#### Adobe CRX {#foundation-crx-6526}
-->


#### Granite{#foundation-granite-6526}

* 이제 Assets Omnisearch 필터의 &quot;콘텐츠 조각 모델&quot; 자리 표시자가 완전히 표시됩니다. 이전에는 Assets으로 이동하여 필터 또는 검색 아이콘을 클릭한 다음 콘텐츠 조각 모델 필드를 확장하면 텍스트가 잘렸습니다. 업데이트된 스타일링은 자리 표시자에게 충분한 공간을 제공합니다. (GRANITE-54387)
* 이제 셸 헤더 링크 위로 포인터를 이동하면 해당 셸 헤더의 도움말 드롭다운이 열려 있습니다. 이전에는, 포인터가 Documentation, Community 및 지원 링크 목록을 입력하자마자 드롭다운이 닫혀 마우스로 링크에 연결할 수 없었습니다. 이제 포커스 핸들러가 다음 애니메이션 프레임으로의 확인을 연기하므로 마우스를 가져도 더 이상 메뉴에서 포커스가 나갈 때 카운트되지 않습니다. (GRANITE-70978)

<!--
#### Jetty{#foundation-jetty-6526}
-->

#### Launch 통합{#foundation-launch-integrations-6526}

개선 사항: Adobe Experience Manager Launch와 Adobe Analytics 통합에서는 Analytics 2.0 API를 사용합니다. Analytics 1.4 API는 2026년 8월 31일에 사용이 종료됩니다. 마이그레이션은 해당 날짜 이후에도 보고 및 Launch 통합이 계속 작동합니다. (CQ-4365074, CQ-4365080)

<!--
#### Localization{#foundation-localization-6526}

#### Oak {#foundation-oak-6526}
-->

#### Platform{#foundation-platform-6526}

* 이제 AEM 로그인 페이지의 바닥글에 있는 도움말 링크에 작업 페이지가 열립니다. 이전에는 링크가 더 이상 존재하지 않는 marketing.adobe.com URL을 가리켰습니다. 이제 바닥글 구성에서 [Adobe Experience Manager 설명서](https://experienceleague.adobe.com/en/docs/experience-manager) URL을 사용합니다. (NPR-44388)
* 개선 사항: AEM에서 이메일을 보낼 때 고객이 SMTP 대신 Microsoft Graph API를 요청함. 다른 티켓이 이미 Graph API 흐름을 구현하기 때문에 티켓이 중복으로 해결되었습니다. OAuth 2.0을 사용하는 SMTP는 SMTP 기본 인증에서 이동해야 하는 고객에게 계속 사용할 수 있습니다. (GRANITE-57478)

* 이제 유효 권한 대화 상자의 문자열이 **도구** > **일반** > **구성** 브라우저에서 올바르게 정렬됩니다. 이전에는 폴더를 선택하고, 속성을 클릭한 다음, 유효 권한을 클릭한 후에 문자열 하나가 줄 밖에 표시되었습니다. 맞춤을 복원하도록 레이아웃 규칙을 업데이트했습니다. (CQ-4359166)


#### 프로젝트 {#foundation-projects-6526}

이제 i18n 사전 선택 대화 상자의 &quot;루트 디렉터리 선택&quot; 문자열이 모두 표시됩니다. 이전에는 번역 프로젝트를 만들고 i18n 사전을 추가한 후 현지화된 여러 인터페이스에서 텍스트가 잘렸습니다. 업데이트된 `cq-projects-translation-content` 패키지는 문자열에 충분한 공간을 제공합니다. (CQ-4355405)

<!--
#### Security{#foundation-security-6526}

#### Sling{#foundation-sling-6526}

#### SPA editor {#foundation-spa-editor-6526}
-->


#### 번역{#foundation-translation-6526}

이제 목록 구성 요소의 스타일 옵션이 사용자의 언어로 표시됩니다. 이전에는 블록 및 그리드 같은 문자열이 작성자가 경험 조각에 목록 구성 요소를 추가한 후 스타일 메뉴에서 영어로 유지되었습니다. 업데이트된 리소스는 한국어, 중국어 간체 및 중국어 번체 인터페이스를 비롯한 번역본을 제공합니다. (CQ-4349666)

<!--
#### User interface{#foundation-ui-6526}

#### WCM{#foundation-wcm-6526}
-->

#### 워크플로{#foundation-workflow-6526}

개선 사항: 이제 Touch UI 페이지 편집기에서 콘텐츠 트리를 렌더링하고 워크플로우 패키지 페이지에서 리소스 정의 구성 요소 편집을 지원합니다. 이전에는 **게시 관리** > **나중에 게시**&#x200B;에서 만드는 `/etc/workflow/packages/` 아래의 페이지에 왼쪽 패널에 콘텐츠 트리가 표시되지 않았으며 작성자는 리소스 정의 구성 요소를 편집하지 못했습니다. 이제 승인자는 Touch UI에서 워크플로 페이로드 내의 페이지 및 에셋을 검사하여 클래식 UI 동작과 일치합니다. (GRANITE-65620)

## [!DNL Experience Manager] 6.5.26.0 설치{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.26.0에는 [!DNL Experience Manager] 6.5가 필요합니다. 자세한 지침은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하세요. <!-- UPDATE FOR EACH NEW RELEASE -->
* 서비스 팩은 Adobe [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.26.0.zip)에서 다운로드할 수 있습니다.
* MongoDB 및 여러 인스턴스가 있는 배포에서 패키지 관리자를 사용하여 작성자 인스턴스 중 하나에 [!DNL Experience Manager] 6.5.26.0을(를) 설치합니다.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> [!DNL Experience Manager] 6.5.26.0 패키지를 제거하거나 제거하지 않는 것이 좋습니다. 필요한 경우 롤백하려면 팩을 설치하기 전에 `crx-repository`의 백업을 만듭니다. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### [!DNL Experience Manager] 6.5에 서비스 팩 설치{#install-service-pack}

1. 인스턴스가 업데이트 모드에 있는 경우(인스턴스가 이전 버전에서 업데이트된 경우) 설치 전에 인스턴스를 다시 시작하십시오. Adobe은 인스턴스의 현재 가동 시간이 높을 경우 다시 시작할 것을 권장합니다.

1. 설치하기 전에 [!DNL Experience Manager] 인스턴스의 스냅숏 또는 새 백업을 만듭니다.

1. [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.26.0.zip)에서 서비스 팩을 다운로드합니다. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 패키지 관리자를 연 다음 **[!UICONTROL 패키지 업로드]**&#x200B;를 선택하여 패키지를 업로드합니다. 자세한 내용은 [패키지 관리자](/help/sites-administering/package-manager.md)를 참조하세요.

1. 패키지를 선택한 다음 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

1. S3 커넥터를 업데이트하려면 서비스 팩을 설치한 후 인스턴스를 중지하고 기존 커넥터를 설치 폴더에 있는 새 이진 파일로 바꾼 다음 인스턴스를 다시 시작하십시오. [Amazon S3 데이터 저장소](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)를 참조하세요.

>[!NOTE]
>
>패키지 관리자 UI의 대화 상자가 서비스 팩을 설치하는 동안 종료되는 경우가 있습니다. Adobe에서는 배포에 액세스하기 전에 오류 로그 변경이 중지될 때까지 기다리는 것이 좋습니다. 업데이터 번들 제거와 관련된 특정 로그를 기다린 후 설치가 성공했는지 확인합니다. 이 문제는 [!DNL Safari] 브라우저에서 발생하지만 어떤 브라우저에서도 발생할 수 있습니다.

**자동 설치**

[!DNL Experience Manager] 6.5.26.0.<!-- UPDATE FOR EACH NEW RELEASE -->을(를) 설치하는 데 사용할 수 있는 두 가지 메서드가 있습니다.

* 서버가 온라인 상태일 때 패키지를 `../crx-quickstart/install` 폴더에 넣습니다. 패키지가 자동으로 설치됩니다.
* 패키지 관리자에서 [HTTP API 사용](/help/sites-administering/package-manager.md#package-share). 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

>[!NOTE]
>
>Experience Manager 6.5.26.0은(는) Bootstrap 설치를 지원하지 않습니다. <!-- UPDATE FOR EACH NEW RELEASE -->

**설치 확인**

이 릴리스에서 사용할 수 있는 인증된 플랫폼에 대해서는 [기술 요구 사항](/help/sites-deploying/technical-requirements.md)을 참조하세요.

1. 제품 정보 페이지(`/system/console/productinfo`)에는 [!UICONTROL 설치된 제품]에 업데이트된 버전 문자열 `Adobe Experience Manager (6.5.26.0)`이(가) 표시됩니다. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 모든 OSGI 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]**&#x200B;이거나 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 콘솔 사용: `/system/console/bundles`).

1. OSGi 번들 `org.apache.jackrabbit.oak-core`은(는) 버전 1.22.20 이상입니다(웹 콘솔 사용: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### [!DNL Experience Manager] Forms용 서비스 팩 설치{#install-aem-forms-add-on-package}

Experience Manager Forms에 서비스 팩을 설치하는 방법은 [Experience Manager Forms 서비스 팩 설치 지침](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)을 참조하십시오.

>[!NOTE]
>
>[AEM 6.5 QuickStart](https://experienceleague.adobe.com/ko/docs/experience-manager-65/content/implementing/deploying/deploying/deploy)에서 사용 가능한 적응형 양식 기능은 탐색 및 평가 목적으로만 사용하도록 설계되었습니다. 프로덕션 용도로 사용하려면 적응형 양식 기능에 적절한 라이선싱이 필요하므로 AEM Forms에 대해 유효한 라이선스를 확보해야 합니다.

### Experience Manager 컨텐츠 조각용 GraphQL 인덱스 패키지 설치{#install-aem-graphql-index-add-on-package}

GraphQL을 사용하는 고객은 GraphQL 색인 패키지 1.1.1[&#128279;](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip)에 Experience Manager 콘텐츠 조각을 설치해야 합니다.

이 옵션을 사용하면 사용된 기능을 기반으로 필요한 색인 정의를 추가할 수 있습니다.

이 패키지를 설치하지 않으면 GraphQL 쿼리가 느려지거나 실패합니다.

>[!NOTE]
>
>이 패키지는 인스턴스당 한 번만 설치하십시오. 모든 서비스 팩으로 다시 설치할 필요는 없습니다.

### UberJar{#uber-jar}

[!DNL Experience Manager] 6.5.26.0에 대한 UberJar를 [Maven 중앙 저장소](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.26/)에서 사용할 수 있습니다. <!-- CHECK FOR UPDATE EACH NEW RELEASE FROM MADHULIKA SINGH -->

Maven 프로젝트에서 UberJar를 사용하려면 [UberJar 사용 방법](/help/sites-developing/ht-projects-maven.md)을 참조하여 프로젝트 POM에 다음 종속성을 포함하십시오. <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.26</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar 및 기타 관련 아티팩트는 Adobe Public Maven 저장소(`repo.adobe.com`) 대신 Maven Central Repository에서 사용할 수 있습니다. 기본 UberJar 파일의 이름이 `uber-jar-<version>.jar`(으)로 바뀝니다. 따라서 `dependency` 태그에 대한 값으로 `apis`을(를) 가진 `classifier`이(가) 없습니다.



## 더 이상 사용되지 않는 기능과 제거된 기능{#removed-deprecated-features}

AEM 6.5에서 더 이상 사용되지 않거나 제거된 모든 기능에 대한 자세한 목록은 [사용되지 않거나 제거된 기능](/help/release-notes/deprecated-removed-features.md)을 참조하십시오.

### AEM Assets REST API의 콘텐츠 조각 지원 {#cf-support-assets-rest-api}

AEM 6.5 LTS SP2가 콘텐츠 조각 및 모델 관리를 위한 최신 OpenAPI를 제공하므로 AEM Assets REST API의 이전 콘텐츠 조각 지원 엔드포인트는 이제 더 이상 사용되지 않습니다.

Adobe은 서비스 종료 공지가 있을 때까지 이러한 이전 끝점을 계속 사용할 수 있도록 합니다. Adobe에서는 더 이상 사용되지 않는 엔드포인트에 대한 추가 개선 사항을 계획하지 않습니다.

### SPA 편집기 {#spa-editor}

[SPA 편집기](/help/sites-developing/spa-overview.md)는 AEM 6.5의 릴리스 6.5.25부터 새 프로젝트에 대해 더 이상 사용되지 않습니다. SPA 편집기는 기존 프로젝트에 대해 계속 지원되지만 새 프로젝트에 사용해서는 안 됩니다.

AEM에서 헤드리스 콘텐츠를 관리하기 위한 권장 편집기는 다음과 같습니다.

* 시각적 편집을 위한 [범용 편집기](/help/sites-developing/universal-editor/introduction.md)
* 양식 기반 편집을 위한 [콘텐츠 조각 편집기](/help/sites-developing/universal-editor/introduction.md)

## 알려진 문제{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

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

  1. `crx-quickstart/repository/`에서 다음 두 폴더 삭제

     * `cache`
     * `diff-cache`

  1. 서비스 팩을 설치하거나 Experience Manager as a Cloud Service을 다시 시작합니다.
     `cache` 및 `diff-cache`에 대한 새 폴더가 자동으로 만들어지고 `error.log`에서 더 이상 `mvstore`과(와) 관련된 예외가 발생하지 않습니다.

* 콘텐츠 모델의 기본 이름을 대신 사용하도록 콘텐츠 모델에 대해 사용자 지정 API 이름을 사용한 GraphQL 쿼리를 업데이트합니다.

* GraphQL 쿼리에서 `fragments` 인덱스 대신 `damAssetLucene` 인덱스를 사용합니다. 이 작업으로 인해 GraphQL 쿼리가 실패하거나 실행하는 데 시간이 오래 걸립니다.

  문제를 해결하려면 `/indexRules/dam:Asset/properties` 아래에 다음 두 속성을 포함하도록 `damAssetLucene`을(를) 구성해야 합니다.

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

  인덱스 정의를 변경한 후에는 리인덱싱이 필요합니다(`reindex` = `true`).

  이 단계 후에 GraphQL 쿼리는 향상된 속도로 수행됩니다.

* 콘텐츠 조각, 사이트 또는 페이지를 이동, 삭제 또는 게시하려고 할 때 콘텐츠 조각 참조를 가져올 때 문제가 있습니다. 백그라운드 쿼리가 실패하고 기능이 작동하지 않습니다.
올바른 작업을 위해 인덱스 정의 노드 `/oak:index/damAssetLucene`에 다음 속성을 추가해야 합니다(리인덱싱이 필요하지 않음).

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* [!DNL Experience Manager] 인스턴스를 6.5.0 - 6.5.4에서 Java™ 11의 최신 서비스 팩으로 업그레이드하는 경우 `error.log` 파일에 `RRD4JReporter` 예외가 표시됩니다. 예외를 중지하려면 [!DNL Experience Manager]의 인스턴스를 다시 시작하십시오. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 사용자는 [!DNL Assets]에서 폴더 이름을 바꾸고 중첩된 폴더를 [!DNL Brand Portal]에 게시할 수 있습니다. 그러나 루트 폴더가 다시 게시될 때까지 폴더의 제목이 [!DNL Brand Portal]에서 업데이트되지 않습니다.

* [!DNL Experience Manager] 6.5.x.x를 설치하는 동안 다음 오류 및 경고 메시지가 나타납니다.
  * &quot;Target Standard API(IMS 인증)를 사용하여 [!DNL Experience Manager]에서 Adobe Target 통합이 구성된 경우 경험 조각을 Target으로 내보내면 잘못된 오퍼 유형이 생성됩니다. Target에서는 &quot;경험 조각&quot;/소스 &quot;Adobe Experience Manager&quot; 유형 대신 &quot;HTML&quot;/소스 &quot;Adobe Target Classic&quot; 유형의 여러 오퍼를 만듭니다.
  * `com.adobe.granite.maintenance.impl.TaskScheduler`: `granite/operations/maintenance`에 유지 관리 창이 없습니다.
  * SUM, MAX 및 MIN과 같은 집계 함수를 사용하는 경우 적용형 양식 서버측 유효성 검사가 실패합니다(CQ-4274424).
  * `com.adobe.granite.maintenance.impl.TaskScheduler` : `granite/operations/maintenance`에 유지 관리 창이 없습니다.
  * 쇼퍼블 배너 뷰어를 통해 자산을 미리 볼 때 Dynamic Media 대화형 이미지의 핫스팟이 표시되지 않습니다.
  * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : 등록 변경이 등록 취소를 완료할 때까지 기다리는 동안 시간이 초과되었습니다.

* AEM 6.5.15부터 `org.apache.servicemix.bundles.rhino` 번들에서 제공한 Rhino JavaScript 엔진에 새로운 호스팅 동작이 있습니다. 엄격 모드(`use strict;`)를 사용하는 스크립트는 올바른 변수를 선언해야 합니다. 그렇지 않으면 실행되지 않고 결국 런타임 오류가 발생합니다.

* 공식 업데이트 패키지를 통해 태그 지정 관련 표준 콘텐츠를 설치하면 `/content/cq:tags` 노드의 언어 속성이 기본값으로 재설정됩니다. 이 작업은 서비스 팩, 보안 서비스 팩, 확장 기능 팩, 누적 기능 팩, 패치 등에 적용됩니다. 따라서 설치하기 전에 속성에 추가해야 합니다.

### AEM Sites의 알려진 문제 {#known-issues-aem-sites-6526}

<!--
* Known issue with a hotfix available for AEM Foundation {#known-issue-foundation-hotfix-6526}

  After you upgrade from an earlier service pack to Experience Manager 6.5.26.0, the OSGi version ordering for CRXDE Lite can prevent Experience Manager from selecting the intended bundle. An earlier service pack contains a higher CRXDE Lite version than the artifact that Service Pack 26 includes (`com.adobe.granite.crxde-lite-1.1.44-CQ651-B00024`).
  
  To resolve this issue, download and install the hotfix [cq-6.5.26-hotfix-GRANITE-76725.zip](https://artifactory.corp.adobe.com/ui/native/maven-aem-release-local/com/adobe/cq/hotfix/cq-6.5.26-hotfix-GRANITE-76725/1.0/cq-6.5.26-hotfix-GRANITE-76725.zip). The hotfix updates CRXDE Lite to `com.adobe.granite.crxde-lite-1.1.44-CQ651-B0026`, and it contains a version change only, with no code or functional changes. (GRANITE-76725)
-->

* 큰 조각 트리에 대한 DoS 보호로 인해 콘텐츠 조각-미리보기가 실패합니다. 기본 GraphQL 쿼리 실행기 구성 옵션에 대한 [KB 문서 보기](https://experienceleague.adobe.com/ko/docs/experience-cloud-kcs/kbarticles/ka-23945)&#x200B;(SITES-17934)

### AEM Forms의 알려진 문제 {#known-issues-aem-forms-6526}

* `bindref`을(를) 사용하는 **첨부 파일** 필드가 포함된 양식이 **작업 할당** 단계를 통해 AEM Workflow에 제출되면 첨부 파일이 표시되지 않습니다. 따라서 작업이 받은 편지함에서 열리면 나타나지 않습니다. 파일이 저장소에 올바르게 저장되지만 작업 할당 단계 UI에 첨부 파일이 표시되지 않습니다. (FORMS-23722)

* 디지털 서명된 PDF이 AEM Forms JEE Workspace의 작업에 연결되면 업로드가 업로드 상태에서 멈춘 상태로 유지되거나 &quot;잘못된 파일&quot; 오류와 함께 실패합니다. 따라서 더 크고 서명된 PDF 첨부 파일을 작업에 추가할 수 없습니다. 이 문제는 이후 버전에서 수정되었습니다. 버전에 대한 핫픽스는 Adobe 지원 센터에 문의하십시오. (FORMS-28517)

#### 핫픽스에 대한 알려진 문제 사용 가능 {#aem-forms-issues-with-hotfixes}

다음 문제에는 다운로드 및 설치에 사용할 수 있는 핫픽스가 있습니다. [핫픽스를 다운로드하여 설치](/help/release-notes/aem-forms-hotfix.md)하여 다음 문제를 해결할 수 있습니다.

* AEM Forms JEE 서비스 팩 21(6.5.21.0)을 설치한 후 `<AEM_Forms_Installation>/lib/caching/lib` 폴더 아래에서 Geode jars `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)`의 중복 항목을 찾으면 다음 단계를 수행하여 문제를 해결합니다(FORMS-14926).

  1. 로케이터가 실행 중인 경우 중지합니다.
  1. AEM 서버를 중지합니다.
  1. `<AEM_Forms_Installation>/lib/caching/lib`(으)로 이동합니다.
  1. `geode-*-1.15.1.2.jar`을(를) 제외한 모든 Geode 패치 파일을 제거합니다. `version 1.15.1.2`이(가) 있는 Geode jar만 있는지 확인합니다.
  1. 관리 모드에서 명령 프롬프트를 엽니다.
  1. `geode-*-1.15.1.2.jar` 파일을 사용하여 Geode 패치를 설치합니다.

## OSGi 번들 및 콘텐츠 패키지 포함됨{#osgi-bundles-and-content-packages-included}

다음 zip 파일에는 이 [!DNL Experience Manager] 6.5 서비스 팩 릴리스에 포함된 OSGi 번들 및 콘텐츠 패키지를 나열하는 텍스트 문서가 포함되어 있습니다.

* [Experience Manager에 포함된 OSGi 번들 목록 6.5.26.0](/help/release-notes/assets/65260-bundles.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager에 포함된 콘텐츠 패키지 목록 6.5.26.0](/help/release-notes/assets/65260-packages.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->

## 제한된 웹 사이트{#restricted-sites}

이러한 웹 사이트는 고객만 사용할 수 있습니다. 고객이시며 액세스 권한이 필요한 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [Adobe 고객 지원 센터](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience#)에 문의하십시오.

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 제품 페이지](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 설명서](https://experienceleague.adobe.com/ko/docs/experience-manager-65)
>* [Adobe 우선 순위 제품 업데이트 구독](https://www.adobe.com/kr/subscription/priority-product-update.html)




