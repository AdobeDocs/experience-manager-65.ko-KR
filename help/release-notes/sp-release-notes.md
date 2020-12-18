---
title: '[!DNL Adobe Experience Manager] 6.5 서비스 팩 릴리스 노트'
description: ' [!DNL Adobe Experience Manager] 6.5 서비스 팩 7에 대한 릴리스 노트'
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 30701cfdb36e5caf606e31564179a632b0de9fb5
workflow-type: tm+mt
source-wordcount: '4243'
ht-degree: 20%

---


# [!DNL Adobe Experience Manager] 6.5 서비스 팩 릴리스 노트  {#aem-service-pack-release-notes}

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 버전 | 6.5.7.0 |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2020년 11월 26일 |
| 다운로드 URL | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip) |

<!-- TBD: Update the SD link when SP7 is available. -->

## [!DNL Adobe Experience Manager] 6.5.7.0 {#what-s-included-in-aem}에 포함된 제품

[!DNL Adobe Experience Manager] 6.5.7.0은 2019년 4월 6.5 릴리스 이후 릴리스된 새로운 기능, 주요 고객의 요구 사항 개선 사항, 성능, 안정성 및 보안 개선 사항이 포함된 중요한 업데이트입니다. 서비스 팩이 [!DNL Adobe Experience Manager] 6.5에 설치되어 있습니다.

[!DNL Adobe Experience Manager] 6.5.7.0에 도입된 주요 기능 및 개선 사항은 다음과 같습니다.

* [!UICONTROL 이름], [!UICONTROL 마지막 수정 날짜,] 및 [!UICONTROL 마지막 롤아웃 날짜] 속성을 사용하여 롤아웃에 사용할 수 있는 Live Copy 페이지를 정렬합니다.

* 페이지 이동 및 MSM 롤아웃을 비동기 작업으로 수행하여 런타임 성능에 대한 영향을 줄일 수 있습니다.

* 사용자는 카드 및 열 보기에서 디지털 자산을 정렬할 수 있습니다.

* [!DNL Assets] 다양한 액세서빌러티 향상 기능을  [!DNL Dynamic Media] 제공합니다. 향상된 기능은 키보드 탐색, 화면 판독기 사용 및 유사한 보조 기술(AT)을 사용할 수 있도록 하는 것과 관련이 있습니다. [[!DNL Assets] 개선 사항](#assets-6570) 및 [[!DNL Dynamic Media] 개선 사항](#dynamic-media-6570)을 참조하십시오.

* [양식 데이터 모델 HTTP 클라이언트 ](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration) 구성을 통해 성능을 최적화할 수 있습니다.

* [레이아웃 모드에서 각 구성 요소에 대한 ](../../help/forms/using/resize-using-layout-mode.md#resize-components) 재설정 옵션 사용 가능

* [!DNL Experience Manager] 6.5 서비스 팩 7 Forms은 다음 제품의 성능을 향상시킵니다.

   * 적응형 양식을 제출할 때 서버에서 필드 값의 유효성을 검사합니다.

   * [!DNL Automated Forms Conversion service]을(를) 사용하여 PDF 양식을 적응형 양식으로 변환

* 내장된 저장소(Apache Jackrabbit Oak)가 버전 1.22.5으로 업데이트되었습니다.

[!DNL Experience Manager] 6.5.7.0에 도입된 기능과 개선 사항의 전체 목록은 [서비스 팩 7](new-features-latest-service-pack.md)의 새로운 기능을 참조하십시오. [!DNL Adobe Experience Manager] 

다음은 [!DNL Experience Manager] 6.5.7.0 릴리스에서 제공된 수정 사항 목록입니다.

### [!DNL Sites] {#sites-6570}

* 페이지에 대해 [!UICONTROL 타임랩] 옵션을 열고 타임라인 사이드 레일 옵션을 연 상태로 유지하고 [!UICONTROL 사이트] 콘솔로 이동하면 `Failed to Load` 오류가 발생합니다(NPR-34951).

* [!UICONTROL 타임랩] 옵션은 선택한 날짜 및 시간 범위(NPR-34951)에 대한 이미지를 표시하지 않습니다.

* 필터가 컨텐츠 조각을 포함하는 페이지에서 `getHeader()`을 호출하면 `java.lang.AbstractMethodError` 오류가 발생합니다(NPR-34942).

* 페이지의 경로에 여러 내용 하위 문자열이 포함되어 있으면 미리 보기가 렌더링되지 않고 버전 비교 기능도 실패합니다(NPR-34740).

* 구성 요소의 `String` 유형 레이블 속성에 대한 숫자 값을 설정할 때 구성 요소를 삭제하고 삭제 작업을 실행 취소할 수 있습니다. 그러나 삭제를 취소하면 레이블 속성이 `String`에서 `Long`(NPR-34739)로 변경됩니다.

* 잠긴 레이아웃이 있는 템플릿을 기반으로 한 경험 조각을 페이지에 추가할 때 다음 예외가 발생합니다(NPR-34632).

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.mozilla.javascript.EcmaError: TypeError: Cannot call method "getChildren" of null
   ```

* 폴더를 이동하면 탐색 문제가 발생하고 다음 오류가 발생합니다(NPR-34554).

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript. org.apache.jackrabbit.oak.query.RuntimeNodeTraversalException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped
   ```

* 새 에셋을 만들고 게시하고 새 위치로 이동하면 `Request to complete move operation` 워크플로우가 만들어지고 결과적으로 취소된 상태가 됩니다. 새 자산을 업로드하고 `move` 작업을 실행하면 보류 중인 상태로 `Request to complete move operation` 작업 과정이 만들어집니다(NPR-34543).

* [!DNL Experience Manager] 6.5.2 환경에서 [!DNL Target] Standard로 경험 조각을 내보낼 때 작업 공간 속성을 [!DNL Target] Standard에 사용할 수 없으므로 API 호출이 실패합니다(NPR-34557).

* [!UICONTROL 게시] 옵션이 사라지므로 사용자는 [!UICONTROL 발행물 관리] 옵션을 통해 페이지를 게시할 수 없습니다(NPR-34542).

* 텍스트에 일부 스타일을 추가하면 텍스트에 `<div>` 태그가 추가되고 더 이상 텍스트에 스타일을 적용할 수 없습니다(NPR-34531).

* 팝업 메뉴에서 항목을 선택하고 필요한 파일을 업데이트할 때 다른 메뉴에 빈 필수 필드가 있으므로 대화 상자 값을 저장할 수 없습니다(NPR-34529).

* 사용자 지정 템플릿에서 페이지를 만들고 블루프린트 계층 내에서 이동하면, 페이지에서 일찍 삭제된 구성 요소가 Live Copy 계층 내에 페이지에 표시됩니다(NPR-34527).

* 아티클 스타일이 콘텐츠에 적용되면 이를 제거할 수 없습니다(NPR-34486).

* 경험 조각의 모든 Live Copy 및 사본은 동일한 [!DNL Adobe Target] 오퍼 ID를 가리킵니다(NPR-34469).

* 글머리 기호 목록 항목이 번호 매기기 목록(NPR-34455) 외에 표시됩니다.

* 소스에 비교 옵션은 소스 페이지와 편집한 페이지 버전 간의 차이를 표시하지 않습니다(NPR-34285).

* 페이지를 삭제할 때 버전 관리 세부 사항을 구성할 수 없습니다(NPR-34159).

* 사용자가 [!UICONTROL 선택 영역 열기] 대화 상자 옵션을 선택하면 키보드 포커스가 페이지에 있는 숨겨진 제어(CQ-4307779, CQ-4293601)으로 이동합니다.

* 작성자에서 게시된 폴더를 이동하면 게시 인스턴스(CQ-4305144)에 따라 폴더 경로가 업데이트되지 않습니다.

* 사용자가 [!UICONTROL 모두 선택] 옵션에서 `Enter` 키를 선택하면 키보드 포커스가 [!UICONTROL 컨트롤 만들기] 옵션(CQ-4293599)으로 이동하지 않습니다.

* `Esc` 키를 선택하면 포커스가 상위 컨트롤(CQ-4293593, CQ-4293590)으로 복원되지 않습니다.

* [!DNL Sites] UI 및 핵심 구성 요소에 대한 WCAG 준수 개선(CQ-4293448).

*  페이지  에 대해 확대/축소 및  [!DNL Sites Editor] 확장 기능이비활성화됩니다(CQ-4282353).

* [오른쪽으로 회전] 옵션을 사용하면 화면 판독기에서 현재 회전 또는 뒤집기 상태 내레이션이 중지됩니다(CQ-4282128).

* 완료 및 구성 취소 대화 상자 단추에 두 개 이상의 탭 정지(CQ-4274601)이 있습니다.

* 동일한 수준에서 비슷한 이름의 페이지를 이동할 수 없습니다(NPR-35041).

* 지우기(x) 옵션을 선택한 후에는 키보드 포커스가 [!UICONTROL 필터] 필드(CQ-4293581)으로 이동하지 않습니다.

* [!DNL Experience Manager] 6.5.6.0으로 업그레이드하면 상속된 단락 시스템의 동작이 변경되고 제대로 작동하지 않습니다(NPR-35117).

* 키보드 사용자는 [!DNL AEM Sites] 페이지에서 [!UICONTROL 작업] 섹션을 선택한 후 탭 포커스를 적절한 순서로 이동할 수 없습니다(CQ-4307786).

* 컨텐츠 조각을 편집할 때 RTE 도구 모음의 링크 대상 메뉴 목록에서 옵션을 선택하면 컨텐츠 조각 작성자 대화 상자가 깜박이기 시작합니다(CQ-4305532).

* 키보드 사용자는 아래쪽 화살표 키(CQ-4295097)을 사용하여 [!UICONTROL 구성 요소 추가] 드롭다운 목록에서 옵션을 선택할 수 없습니다.

* 탭 초점은 [!DNL Sites] 페이지의 [!UICONTROL 자산] 탭에 있는 달력 메뉴에서 날짜를 선택할 때 적절한 순서로 이동하지 않습니다(CQ-4293600).

* 사이트 페이지를 편집할 때 사용할 수 있는 링크 또는 텍스트 옵션을 삭제한 후 탭 포커스는 키보드 사용자의 다음 또는 이전 옵션으로 이동하지 않습니다(CQ-4293597).

* 키보드 사용자는 사용 가능한 옵션을 보고 `Esc` 키(CQ-4293592)을 누른 후 탭 포커스를 [!UICONTROL 작업] 섹션의 추가 옵션으로 다시 이동할 수 없습니다.

* [!UICONTROL 편집] 모드에서 이미지에 대해 [!UICONTROL 회전] 옵션을 활성화하면 회전 시 남는 대신 탭 포커스가 키보드 사용자에 대해 [!UICONTROL 다시 실행] 옵션(CQ-4293587)으로 이동합니다.

* [!UICONTROL 링크 및 작업] 탭에서 사용할 수 있는 [!UICONTROL 선택 항목 열기] 대화 상자에서 탭 포커스가 [!UICONTROL 취소] 옵션(CQ-4293579) 다음에 페이지의 숨겨진 요소로 이동합니다.

* 키보드 사용자가 이미지를 편집할 때 [!UICONTROL Finish] 옵션으로 이동하고 Enter 키를 누르면 화면 판독기가 완료를 알리지 않습니다(CQ-4282351).

* 화면 판독기 및 키보드 사용자는 [!UICONTROL 링크 및 작업] 대화 상자에서 사용할 수 있는 위로 이동 및 아래로 이동 옵션을 사용할 수 없습니다(CQ-4281120).

* 키보드 사용자는 [!UICONTROL 속성] 페이지의 닫기(X) 옵션으로 이동한 후 탭 초점을 복원할 수 없습니다(CQ-4293581, NPR-34653).

### [!DNL Assets] {#assets-6570}

[!DNL Adobe Experience Manager] 6.5.7.0 [!DNL Assets] 는 다음 문제를 수정하고 다음 개선 사항을 제공합니다.

* 이 릴리스의 [!DNL Experience Manager Assets]에 있는 액세스 가능성에 대해 다음 개선 사항이 수행됩니다. 자세한 내용은  [!DNL Assets]](/help/assets/accessibility.md)의 [액세스 가능성 기능을 참조하십시오.

   * 키보드를 사용하여 타임라인을 탐색할 때 `Esc` 키는 포커스를 잃지 않고 [!UICONTROL 모두 표시] 옵션을 축소할 수 있습니다(CQ-4293598).
   * 키보드 탭 키를 사용하여 탐색할 때 추가된 태그에서 마지막 태그를 제거한 후 태그 필드에 포커스가 유지됩니다(NPR-35109).
   * [!DNL Experience Manager] 이제 구성 요소에는 화면 판독기에서 사용할 이름, 역할 및 값에 대한 적절한 정보가 포함됩니다(NPR-34255).
   * 유형/크기 콤보 상자, 링크 콤보 상자, 언어 콤보 상자 또는 텍스트 편집 상자를 삭제하면 키보드 포커스가 다음 또는 이전 사용자 인터페이스 요소 또는 보다 관련 사용자 인터페이스 요소(CQ-4293585)으로 돌아갑니다.
   * 포인터를 옵션 위에 놓으면 선택 및 다운로드와 같은 팁이 나타납니다. 화면 돋보기를 사용하는 사용자는 이러한 팁으로 인해 파일 축소판을 볼 수 없습니다. 이제 `Escape` 키를 사용하여 옵션을 제거한 후 포커스를 유지할 수 있습니다. (CQ-4293554).
   * 페이지에 있는 그리드에서 격자 셀을 선택하면 스크린에 나타나는 작업 표시줄(CQ-4282127)으로 포커스가 이동합니다.
   * [!DNL Experience Manager] 홈 페이지(CQ-4282072)에 있는 모든 솔루션에 대한 링크에 시각적 단서(밑줄 및 V자 아이콘)가 표시되므로 시각적 사용자는 일반 텍스트와 링크를 차별화할 수 있습니다.

* 다음 사용자 환경 개선 사항은 [!DNL Assets]에서 수행됩니다.

   * 카드 보기 및 열 보기에서 자산 정렬을 활성화합니다(NPR-35097).

* 6.5로 업그레이드한 후 자산 HTTP API를 사용하여 JSON 파일이 생성된 경우 파일에 사용된 인코딩 관련 문제가 있습니다(NPR-35129).

* 컬렉션 만들기(컬렉션 만들기 옵션을 사용할 수 없음) 권한이 없는 그룹의 사용자는 URL `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/collections/createcollectionwizard.html/content/dam/collections?contentPath=/content/dam/collections`(NPR-35115)에 직접 액세스하여 컬렉션을 만들 수 있습니다.

* 이름별로 정렬하면 검색된 자산이 대/소문자를 구분하여 정렬됩니다. 이렇게 하면 검색 결과에서 대소문자를 기준으로 정렬된 2개의 목록이 만들어집니다(NPR-35068).

* 편집기에서 컨텐츠 조각을 열면 경고 메시지(`Invalid value specified for a metadata property`)가 오류 로그에 기록됩니다(NPR-35012).

* 관리자 권한이 없는 사용자는 [Experience Manager] 데스크탑 앱을 사용하여 만료된 자산을 편집할 수 있습니다. (NPR-34993).

* 동일한 자산을 자산 사용자 인터페이스에서 드래그하고 새 버전을 만들면 메타데이터의 변경 내용이 지속되지 않습니다(NPR-34940).

* 컬렉션을 편집할 때 사용자는 컬렉션의 제목을 삭제하고 변경 내용을 저장할 수 있습니다(NPR-34889).

* 중복 이미지를 업로드할 때 삭제 옵션이 표시됩니다. 삭제를 선택하면 이미지가 업로드됩니다. DAM 자산 업데이트 워크플로우도 트리거됩니다(NPR-34744).

* [!DNL Adobe InDesign]과 함께 [!DNL Adobe Asset Link]을 사용하는 경우 검색 결과에 폴더 및 컬렉션이 포함되지 않고 자산만 포함됩니다(NPR-34699, CQ-4303666).

* 카드 보기에 포인터를 두면 (자동) 카드에서 사용할 수 있는 빠른 작업에 초점을 맞춰 화면 스크롤이 수행됩니다(NPR-34514).

* 여러 자산의 속성을 일괄적으로 편집할 때 [!UICONTROL 저장] 옵션을 선택하면 벌크 편집기 보기가 닫고 기본 [!DNL Assets] 페이지로 리디렉션됩니다. 이 동작은 [!UICONTROL 저장 및 닫기] 옵션의 비헤이비어와 동일하며 예상되지 않습니다(NPR-34546).

* 스마트 컬렉션은 저장 후 올바른 사용자 인터페이스 설정이 없습니다. 쿼리는 제대로 저장되지만 인터페이스는 항상 마지막으로 추가된 옵션 설명(NPR-34539)을 표시합니다.

* 에셋을 [!DNL Experience Manager]에 추가할 때 네임스페이스 없는 메타데이터는 가져오지 않습니다(NPR-34530).

* 폴더의 자산을 드래그하여 이동시키는 경우 사용자 인터페이스에는 Lightbox] 및 [!UICONTROL 컬렉션에 놓기 옵션도 표시됩니다]. [!UICONTROL  이동 작업이 취소되더라도 사용자 인터페이스는 이후 두 옵션(NPR-34526)을 계속 표시합니다.

* 컬렉션 페이지에 `%>` 기호가 표시됩니다(NPR-34499).

* 열 보기에서 모든 자산이 표시되기 전에 위쪽 및 아래쪽으로 스크롤할 때 [!DNL Assets]은 중복된 폴더 및 자산 이름을 표시합니다(NPR-34464).

* 공개 폴더를 만든 후 바로 비공개 폴더를 만드는 경우 공용 폴더는 비공개 폴더 설정(NPR-34415)을 사용합니다.

* 카드 보기에서는 카드가 알파벳순으로 나열되지 않으며 카드를 알파벳순으로 정렬할 수 없습니다(NPR-34234).

* 계단식 규칙을 다시 열 때 사용자 인터페이스에 선택 사항이 유지되지 않습니다(CQ-4301452).

#### [!DNL Dynamic Media] {#dynamic-media-6570}

* [!DNL Dynamic Media](CQ-4290306)의 액세서빌러티를 위해 다음 개선 사항이 수행됩니다. 자세한 내용은  [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)의 [액세스 가능성 기능을 참조하십시오.

   * 화면 판독기(JAWS, 내레이터)는 [임베드 크기] 메뉴 옵션(CQ-4290927)에서 메뉴 항목의 이름, 역할 및 상태를 나레이션합니다.
   * 사용자는 `Tab` 키(CQ-4290926)을 사용하여 이메일 링크 대화 상자를 탐색할 수 있습니다.
   * 화면 판독기의 향상된 기능(CQ-4290623, CQ-4290622)을 통해 비디오 인코딩 프로필을 만드는 워크플로우는 사용자에게 더 적합합니다.
   * `Tab` 키를 사용하여 탐색할 때 포커스는 워크플로우의 적절한 사용자 인터페이스 요소로 이동하여 대화형 비디오를 만듭니다(CQ-4290621, CQ-4290620, CQ-4290619).
   * 웹 표준을 준수하도록 게시 페이지, 자산 편집 페이지, 스마트 자르기 편집 페이지 및 이미지 세트 편집기 페이지가 개선되었습니다. 이제 AT(보조 기술) 사용자는 이러한 페이지를 쉽게 탐색하고 이미지(CQ-4290617, CQ-4290616, CQ-4290613, CQ-4290612, CQ-4290610, CQ-4290614)을 자르는 등의 작업을 수행할 수 있습니다.
   * 사용자가 키보드를 사용하여 탐색할 수 있도록 뷰어가 개선되었습니다(CQ-4290615).
   * 키보드 및 화면 판독기 사용자는 자르기 기능을 사용할 수 있습니다(CQ-4290609).
   * 키보드 사용자는 핫스팟을 보다 잘 관리할 수 있습니다(CQ-4290604, CQ-4290603).

* 회사 이름과 폴더 이름이 동일한 경우(NPR-31340) [!DNL Experience Manager]에서 원격 이미지 집합을 편집할 수 없습니다.

* 핫스팟을 [!DNL Dynamic Media] 이미지에 추가한 후 또는 [!DNL Dynamic Media] 비디오 또는 [!DNL Experience Fragment] 이미지를 편집한 후 출력물을 미리 보기할 때 z-인덱스 순서가 잘못되었습니다(CQ-4307267).

* [!DNL Dynamic Media] 혼합 미디어 집합을 다시 처리할 때 동기화가 실패합니다(CQ-4307184).

* 자산이 [!DNL Dynamic Media]에 대한 자동 동기화가 구성된 폴더로 이동되면 자산이 동기화되지 않습니다(CQ-4307122).

* [!DNL Dynamic Media] 비디오가 기본 HTML5 비디오 컨트롤을 사용하여 iOS 장치에서 재생되지 않습니다(CQ-4306977, CQ-4306727).

* SmartCrop이 적용된 이미지를 다운로드할 수 없습니다(CQ-4304558).

* Dynamic Media에 폴더를 선택적으로 게시할 수 없습니다(CQ-4304526).

* [!DNL Experience Manager]에서 비디오 파일의 게시를 취소해도 구성된 Scene7 배포에서 응용 비디오 세트의 게시를 취소하지 않습니다(CQ-4304405).

* 파노라마 미디어 구성 요소에 파노라마 이미지 자산을 추가하고 페이지를 새로 고치면 `Uncaught ReferenceError: $ is not defined` 오류가 발생합니다(CQ-4302810).

* [!UICONTROL 뷰어 사전 설정 편집기]에서 [!UICONTROL PanoramicImage/PanoramicImage_VR] 사전 설정을 편집할 때 `PanoramicView` 구성 요소에서 `PANORAMICVIEW_AUTOROTATE` 수정자 레이블을 사용할 수 없습니다(CQ-4302443).

* 비디오가 MixedMediaSet(CQ-4298161)에서 첫 번째 비디오가 아닌 경우 비디오 캡션이 표시되지 않습니다.

* iPhone 모바일 장치의 HTML5 전자 카탈로그 뷰어는 페이지를 회전하거나 페이지를 넘길 수 없습니다(CQ-4296611).

* 모바일 디바이스에서 색상 견본을 스크롤할 때 색상 견본은 몇 초 동안 표시 영역 오른쪽 및 밖으로 스크롤하여 보기로 다시 스크롤합니다(CQ-4296439).

* 뷰어 사전 설정 기본 레코드가 만들어지면 CSS 및 아트웍이 게시되지 않고 뷰어 사전 설정만 게시됩니다(CQ-4262205).

* [!UICONTROL 대화형 비디오/이미지] 구성 요소에서 지정된 핫스팟에 대한 경험 조각을 연결하려고 하면 선택한 경험 조각 경로가 표시되지 않습니다. 대신 경로 필드에서 빈 값을 반환합니다(NPR-35146, CQ-4298136).

* IVV 편집기에서 경험 조각을 미리 볼 수 없습니다(CQ-4308560).

* 이미지에 핫스팟을 추가하고 경험 조각을 선택하면 경험 조각(CQ-4307455)의 하위 폴더와 변형을 선택할 수 없습니다.

* 이미지가 아닌 자산은 업로드 후 게시됨으로 표시되지 않습니다(CQ-4306415).

#### [!DNL Experience Manager] 3D 에셋  {#three-d-assets-6570}

* `DAM CQ MIME Type` 서비스는 잘못된 MIME 형식을 3D 자산에 적용하여 잘못된 렌더링을 초래합니다(NPR-34731).

### [!DNL Commerce] {#commerce-6570}

* 상거래 제품 컬렉션 사용자 인터페이스는 컬렉션 내 제품 15개 이상(NPR-34502)을 나열하지 않습니다.

### 플랫폼 {#platform-6570}

* HTTPS를 통한 HTTP 세션이 무효화되지 않습니다(NPR-35083).
* 사용자 인터페이스에서 일별 또는 주별 유지 관리 작업을 시작할 때 `NullPointerException`이 반환됩니다(NPR-34953).
* W3C 유효성 검사기는 호환 클라이언트 라이브러리 JavaScript 파일에 대한 경고를 보고합니다(NPR-34898).
* `AudienceOmniSearchHandler` 함수는 사용되지 않는 인덱스(NPR-34870)를 사용합니다.
* Experience Manager에서 로그아웃해도 쿠키가 지워지지 않습니다(NPR-34743).
* 태그 이름에 특수 문자(NPR-34357)가 포함된 경우 `TagManager` API의 `findByTitle` 함수가 작동하지 않습니다.
* 사용자 동기화 패키지를 가져오는 프로세스가 실패했습니다(NPR-34399).
* `Coral.Masonry` 구성 요소에 `ariaLabel` 및 `ariaLabelledby` 속성에 대한 지원을 추가했습니다(GRANITE-29962).
* 최신 핵심 구성 요소 패키지(CQ-4306788)을 설치한 후 컨텐츠 조각이 있는 페이지에 대해 디스패처 캐시가 새로 고쳐지지 않습니다.
* 인용 부호(`"`)가 있는 지역화된 태그 이름이 사용자 인터페이스에 제대로 표시되지 않습니다(CQ-4305439).

### 사용자 인터페이스 {#ui-6570}

* 구성 요소 속성의 [!UICONTROL Link to] 필드에 지정된 문자열과 일치하지 않는 자동 완성 제안이 표시됩니다(NPR-34865).

* AEM은 2일 간 배포되는 일일 유지 관리 창을 예약할 때 다음 오류 메시지를 표시합니다(NPR-35280).

   ```TXT
   ERROR The start time must precede (be less than) the end time
   ```

### 통합 {#integrations-6570}

* 기존 [!DNL Adobe Launch] 구성을 편집하지 못했습니다(NPR-35045).
* IMS 구성 및 [!DNL Adobe Target Standard] 환경(NPR-34555)을 사용하는 경우 [!DNL Experience Fragments]을(를) [!DNL Adobe Target]으로 내보낼 수 없습니다.
* 폴더에서 [!UICONTROL 대상자] 페이지로 이동(NPR-35151)할 때 [!UICONTROL 대상] 페이지가 나타납니다(NPR-35151).

### 슬링 {#sling-6570}

* 기본 로그인 상태 확인은 존재하지 않는 사용자의 자격 증명을 검증합니다(NPR-34686).

### 번역 프로젝트 {#translation-6570}

* [!DNL Experience Manager]에서 번역 프로젝트를 취소하면 취소 요청이 번역 공급자에게 전송되지 않습니다(NPR-34433).

### [!DNL Communities] {#communities-6570}

* 제품에서 불공평한 용어의 모든 인스턴스는 승인된 용어(NPR-34311)로 대체됩니다.
* [!DNL Google+] 소셜 공유 옵션 목록에서 제거됩니다(NPR-33877).

### [!DNL Brand Portal] {#brandportal-6570}

* 사용자 인터페이스는 [!UICONTROL 목록 보기]에서 자산을 선택할 때 응답하지 않습니다(NPR-34728).

### [!DNL Forms] {#forms-6570}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 예약된  [!DNL Experience Manager] 서비스 팩 릴리스 날짜 이후 1주일 후에 추가 기능 패키지를 릴리스합니다.

>[!NOTE]
>
>[!DNL Experience Manager] 서비스 팩에는 [!DNL Forms] 수정 사항이 포함되어 있지 않습니다. 이러한 수정 사항은 별도의 [!DNL Forms] 추가 기능 패키지를 사용하여 전달됩니다. 또한, JEE의 [!DNL Experience Manager Forms]에 대한 수정 사항이 포함된 누적 설치 프로그램이 릴리스됩니다. 자세한 내용은 [AEM Forms 추가 기능 설치](#install-aem-forms-add-on-package) 및 [AEM Forms JEE 설치](#install-aem-forms-jee-installer)를 참조하십시오.

**적응형 양식**

* [!DNL Experience Manager] 서비스 팩 6를 적용한 후 클래식 UI를 사용하여 적응형 양식을 편집할 수 없습니다(NPR-35126).

* PDF를 적응형 양식으로 변환하는 경우 탭 형식의 레이아웃에서 양식 데이터 모델을 사용하여 중첩된 패널의 값을 설정할 수 없습니다. 또한 코드 편집기를 사용하여 정적 배열에서 라디오 단추 그룹의 값을 동적으로 설정할 때 문제가 발생합니다(NPR-35062).

* 적응형 양식의 텍스트 필드 구성 요소에 일본어 문자를 입력하면 최대 35자 제한(NPR-35039)보다 많은 문자를 지정할 수 있습니다.

* 적응형 양식에는 양식을 제출한 후 표시되는 **[!UICONTROL 감사 인사]** 페이지에 `owner` 및 `status`과 같은 원치 않는 매개 변수가 표시됩니다(NPR-34989).

* [!UICONTROL 첨부 파일] 구성 요소에 대한 [!UICONTROL 파일 선택] 대화 상자에는 지원되지 않는 파일 형식과 응용 양식 제출 중 오류가 발생하는 선택 항목이 표시됩니다(NPR-34970).

* 양식 앞에 텍스트를 포함하는 [!DNL Experience Manager Sites] 페이지에 적응형 양식을 삽입하면 커서 포커스가 양식 앞에 있는 텍스트 대신 양식으로 바로 이동합니다(NPR-34947).

*  6.2 데이터 XML 파일을 사용하여 적응형 양식을 미리  [!DNL Experience Manager] 채우기 위한 [데이터 옵션]을 사용하여 미리 보기는 제대로 작동하지 않습니다(NPR-35087).

* 적응형 양식의 데이터 사전을 업데이트할 때 양식은 적응형 양식이 캐시된 값을 반환하도록 변환되지 않습니다(NPR-34845).

* 조각이 캐시 무효화로 인해 응용 형식으로 로드하는 데 시간이 더 오래 걸립니다(NPR-34567).

* 탭 탐색은 적응형 양식의 화면 판독기에 맞게 작동하지 않습니다(NPR-34544).

**서신 관리**

* 부동 유형을 포함하는 숫자 데이터로 XML 태그의 값을 초안으로 저장할 수 없습니다(NPR-35050).

* ES3에서 에셋을 마이그레이션할 때, 자산은 편집할 수 없는 기본 조건 2개를 포함합니다(NPR-34972).

* 문자로 데이터 사전을 편집할 때 [!UICONTROL Lented Content] 섹션에는 유용한 정보 대신 회전하는 직사각형이 표시됩니다(NPR-34853).

**대화형 통신**

* [!DNL Forms] 추가 기능 패키지를 설치한 후 사용할 수 있는 대화형 통신에 대한 롤아웃 구성 이름은 표준 롤아웃 구성 이름(NPR-34976)을 복제합니다.

**문서 보안**

* 새 문서 보안 정책을 저장할 때 Experience Manager Forms은 `Relative validity period is required` 오류 메시지를 표시합니다(NPR-34679).

* 새 문서 보안 정책을 저장할 때 Experience Manager Forms은 `Invalid filed value.Numeric value is required` 오류 메시지를 표시합니다(NPR-34678).

* Document Security에서 PDF 2.0 문서를 보호할 수 없습니다(CQ-4305851).

보안 업데이트에 대한 자세한 내용은 [Experience Manager 보안 게시판 페이지](https://helpx.adobe.com/security/products/experience-manager.html)를 참조하십시오.

## 6.5.7.0 설치 {#install}

**설정 요구 사항 및 자세한 정보**

* AEM 6.5.7.0을 사용하려면 AEM 6.5가 필요합니다. 세부 지침은[업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하십시오.
* 서비스 팩은 Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 다운로드할 수 있습니다.
* MongoDB 및 여러 인스턴스가 포함된 배포에서 패키지 관리자를 사용하여 작성자 인스턴스 중 하나에 AEM 6.5.7.0을 설치합니다.

>[!NOTE]
>
>Adobe에서는 [!DNL Adobe Experience Manager] 6.5.7.0 패키지를 제거하거나 제거할 것을 권장하지 않습니다.

### 서비스 팩 설치 {#install-service-pack}

기존 Adobe Experience Manager 6.5 인스턴스에 서비스 팩을 설치하려면 다음 단계를 수행하십시오.

1. 인스턴스가 업데이트 모드인 경우 설치 전에 인스턴스를 다시 시작합니다(이전 버전에서 인스턴스가 업데이트된 경우임). Adobe에서는 인스턴스에 대한 현재 가동 시간이 높은 경우 다시 시작하는 것이 좋습니다.

1. 설치하기 전에 스냅샷 또는 [Experience Manager] 인스턴스의 새 백업을 만듭니다.

1. [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip)에서 서비스 팩을 다운로드합니다.

1. 패키지 관리자를 열고 **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭하여 패키지를 업로드합니다. 자세한 내용은 [패키지 관리자](/help/sites-administering/package-manager.md)를 참조하십시오.

1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

1. S3 커넥터를 업데이트하려면 서비스 팩 설치 후 인스턴스를 중지하고, 기존 커넥터를 설치 폴더에 제공된 새 이진 파일로 바꾼 후 인스턴스를 다시 시작합니다. [Amazon S3 데이터 저장소](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)를 참조하십시오.

>[!NOTE]
>
>패키지 관리자 UI에 대한 대화 상자가 서비스 팩을 설치하는 동안 종료되는 경우가 있습니다. 배포에 액세스하기 전에 오류 로그가 안정될 때까지 기다리는 것이 좋습니다. 업데이터 번들 제거와 관련된 특정 로그를 기다린 후 설치가 성공했는지 확인합니다. 일반적으로 이러한 작업은 [!DNL Safari]에서 발생하지만 모든 브라우저에서 간헐적으로 발생할 수 있습니다.

**자동 설치**

작업 인스턴스에 Adobe Experience Manager 6.5.7.0을 자동으로 설치하는 두 가지 방법이 있습니다.

A. 서버가 온라인 상태일 때 패키지를 `../crx-quickstart/install` 폴더에 넣습니다. 패키지가 자동으로 설치됩니다.

B. [패키지 관리자에서 HTTP API](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html)를 사용합니다. 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

>[!NOTE]
>
>Adobe Experience Manager 6.5.7.0은 Bootstrap 설치를 지원하지 않습니다.

**설치 확인**

1. 제품 정보 페이지(`/system/console/productinfo`)에는 [!UICONTROL 설치된 제품] 아래에 업데이트된 버전 문자열 `Adobe Experience Manager (6.5.7.0)`이 표시됩니다.

1. 모든 OSGI 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]**&#x200B;이거나 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 콘솔 사용: `/system/console/bundles`).

1. OSGi 번들 `org.apache.jackrabbit.oak-core`은 버전 1.22.3 이상입니다(웹 콘솔 사용:`/system/console/bundles`).

이번 릴리스에서 사용할 수 있는 인증된 플랫폼을 확인하려면 [기술 요구 사항](/help/sites-deploying/technical-requirements.md)을 참조하십시오.

### Adobe Experience Manager Forms 추가 기능 패키지 설치 {#install-aem-forms-add-on-package}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 예약된  [!DNL Experience Manager] 서비스 팩 릴리스 날짜 이후 1주일 후에 추가 기능 패키지를 릴리스합니다.

>[!NOTE]
>
>AEM Forms를 사용하지 않는 경우 건너뜁니다. Adobe Experience Manager Forms의 수정 사항은 별도의 추가 기능 패키지를 통해 전달됩니다.

1. Adobe Experience Manager 서비스 팩을 설치했는지 확인합니다.
1. 운영 체제에 대한 [AEM Forms 릴리스](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html)에 나열된 해당 양식 추가 기능 패키지를 다운로드합니다.
1. [AEM Forms 추가 기능 패키지 설치](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)에 설명된 대로 양식 추가 기능 패키지를 설치합니다.

### JEE에 Adobe Experience Manager Forms 설치 {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE에서 AEM Forms를 사용하지 않는 경우 건너뜁니다. 별도의 설치 프로그램을 통해 JEE의 Adobe Experience Manager Forms 수정 사항이 전달됩니다.

JEE에 Forms Experience Manager용 누적 설치 프로그램 및 배포 후 구성에 대한 자세한 내용은 [릴리스 노트](jee-patch-installer-65.md)를 참조하십시오.

### UberJar {#uber-jar}

Experience Manager 6.5.7.0용 UberJar는 [Maven Central 리포지토리](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.7/)에서 사용할 수 있습니다.

Maven 프로젝트에서 UberJar를 사용하려면 [Uberjar 사용 방법](/help/sites-developing/ht-projects-maven.md)을 참조하여 프로젝트 POM에 다음 종속성을 포함하십시오.

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.7</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar 및 기타 관련 아티팩트는 Adobe Public Maven 리포지토리(`repo.adobe.com`) 대신 Maven Central Repository에서 사용할 수 있습니다. 기본 UberJar 파일의 이름이 `uber-jar-<version>.jar`로 변경되었습니다. 따라서 `dependency` 태그의 값으로 `apis`가 있는 `classifier`이 없습니다.

## 이제 사용되지 않는 기능 {#removed-deprecated-features}

다음은 [!DNL Experience Manager] 6.5.7.0으로 더 이상 사용되지 않는 것으로 표시된 기능 및 기능 목록입니다. 기능은 처음에 사용되지 않고 이후 릴리스에서 제거됨으로 표시됩니다. 일반적으로 대체 옵션이 제공됩니다.

배포에서 기능이나 기능을 사용하는지 검토합니다. 또한 대체 옵션을 사용하도록 구현을 변경할 계획입니다.

| 영역 | 기능 | 대체 |
|---|---|---|
| 통합 | **[!UICONTROL AEM 클라우드 서비스 옵트인]** 화면은 더 이상 사용되지 않습니다. AEM 6.5에서 Adobe IMS 및 I/O를 통해 인증을 사용하는 Target 표준 API를 지원하고 분석 및 개인 설정을 위해 AEM 페이지를 계측하는 Adobe Launch의 늘어나는 역할을 지원하도록 AEM 및 Target 통합이 업데이트되어 옵트인 마법사가 기능상 무관해졌습니다. | 해당 AEM 클라우드 서비스를 통해 시스템 연결, Adobe IMS 인증 및 Adobe I/O 통합 구성. |
| 커넥터 | Microsoft SharePoint 2010 및 Microsoft SharePoint 2013 Adobe JCR Connector는 AEM 6.5에서 더 이상 사용하지 않습니다. | N/A |

## 알려진 문제 {#known-issues}

* Experience Manager 6.5.7.0 설치 중 `error.log` 파일에서 다음 오류를 무시합니다.

   ```TXT
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy(1314)] : Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy(1316)] : Could not load implementation object class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy(1315)] : Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy)
   ```

* [!DNL Experience Manager] 인스턴스를 6.5에서 6.5.7.0 버전으로 업그레이드하는 경우 `error.log` 파일에서 `RRD4JReporter` 예외를 볼 수 있습니다. 인스턴스를 다시 시작하여 문제를 해결합니다.

* [!DNL Experience Manager] 6.5에 [!DNL Experience Manager] 6.5 서비스 팩 5 또는 이전 서비스 팩을 설치하는 경우, `/var/workflow/models/dam`에서 만든 자산 사용자 지정 워크플로우 모델의 런타임 복사본이 삭제됩니다.
런타임 복사본을 검색하려면 HTTP API를 사용하여 사용자 지정 워크플로우 모델의 디자인 타임 사본을 해당 런타임 복사본과 동기화하는 것이 좋습니다.
   `<designModelPath>/jcr:content.generate.json`.

* [!UICONTROL 규칙 정의] 대화 상자를 사용하여 [!UICONTROL 폴더 메타데이터 스키마 Forms 편집기] 및 [!UICONTROL 메타데이터 스키마 Forms 편집기]에서 계단식 규칙을 편집하고 만들 때 문제가 발생하면 Adobe 고객 지원 센터에 문의하십시오. 이미 만들고 저장한 규칙이 예상대로 작동합니다.

* 계층 구조의 한 폴더의 이름이 [!DNL Experience Manager Assets]에서 변경되고 자산이 있는 중첩된 폴더가 [!DNL Brand Portal]에 게시되는 경우 루트 폴더가 다시 게시될 때까지 폴더의 제목이 [!DNL Brand Portal]에서 업데이트되지 않습니다.

* 사용자가 적응형 양식에서 처음으로 필드를 구성하도록 선택하면 구성 저장 옵션이 속성 브라우저에 표시되지 않습니다. 동일한 편집기에서 적응형 양식의 다른 필드 일부를 구성하도록 선택하면 문제가 해결됩니다.

* [!UICONTROL 연결된 자산 구성] 마법사가 설치 후 404 오류 메시지를 반환하는 경우 패키지 관리자를 사용하여 `cq-remotedam-client-ui-content` 및 `cq-remotedam-client-ui-components` 패키지를 수동으로 다시 설치합니다.

* AEM 6.5.x.x를 설치하는 동안 다음 오류 및 경고 메시지가 표시될 수 있습니다.
   * Target 표준 API(IMS 인증)를 사용하여 AEM에 Target 통합이 구성된 경우 환경 조각을 Target으로 내보내면 잘못된 오퍼 유형이 생성됩니다. 경험 조각/소스 Adobe Experience Manager 유형 대신 Target은 HTML/소스 Adobe Target Classic 유형으로 여러 가지 오퍼를 작성합니다.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: granite/operations/maintenance에 유지 관리 창이 없습니다.
   * SUM, MAX 및 MIN과 같은 집계 함수를 사용하는 경우 적용형 양식 서버측 유효성 검사가 실패합니다. CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance에 유지 관리 창이 없습니다.
   * 쇼퍼블 배너 뷰어를 통해 자산을 미리 볼 때 Dynamic Media 대화형 이미지의 핫스팟이 표시되지 않습니다.

## OSGi 번들 및 콘텐츠 패키지가 설치됨 {#osgi-bundles-and-content-packages-included}

다음 텍스트 문서에는 AEM 6.5.7.0에 포함된 OSGi 번들 및 컨텐츠 패키지 목록이 나와 있습니다.

* [AEM 6.5.7.0에 포함된 OSGi 번들 목록](assets/6570_bundles.txt)

* [AEM 6.5.7.0에 포함된 콘텐츠 패키지 목록](assets/6570_packages.txt)

## 제한된 웹 사이트 {#restricted-sites}

이러한 웹 사이트는 고객에게만 제공됩니다. 액세스가 필요한 고객의 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* 고객 지원 센터](https://experienceleague.adobe.com/docs/customer-one/using/home.html)에 문의하는 방법을 참조하십시오.[

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5 릴리스 노트](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] 제품 페이지](https://www.adobe.com/kr/marketing/experience-manager.html)
>* [[!DNL Experience Manager] 6.5 설명서](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* [Adobe 우선 순위 제품 업데이트](https://www.adobe.com/subscription/priority-product-update.html) 구독

