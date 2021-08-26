---
title: '[!DNL Experience Manager] 6.5 서비스 팩 릴리스 노트'
description: ' [!DNL Adobe Experience Manager] 6.5 서비스 팩 10에 관한 릴리스 노트'
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: 861f5f4ae87da106bc42895e03bc42c0b17bd9fc
workflow-type: tm+mt
source-wordcount: '3652'
ht-degree: 11%

---

# [!DNL Adobe Experience Manager] 6.5 서비스 팩 릴리스 노트 {#aem-service-pack-release-notes}

## 릴리스 노트 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 버전 | 6.5.10.0 |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2021년 8월 26일 |
| 다운로드 URL | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip) |

## [!DNL Adobe Experience Manager] 6.5.10.0에 포함된 제품 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.10.0에는 2019년 4월 6.5 릴리스의 공식 출시 이후 릴리스된 새로운 기능, 주요 고객이 요청한 향상된 기능 및 성능, 안정성, 보안 개선 사항이 포함됩니다. 서비스 팩이 [!DNL Adobe Experience Manager] 6.5에 설치됩니다.

[!DNL Adobe Experience Manager] 6.5.10.0에 도입된 주요 기능 및 개선 사항은 다음과 같습니다.

* **향상된  [!DNL Content Fragment] 모델 및 편집기**: 이제 중첩된 모델을 사용하여 구조화된 컨텐츠에 대해 복잡한 사용자 지정 모델을 만들 수  [!DNL Content Fragment] 있습니다. 컨텐츠 구조는 하위 조각으로 모델링된 기본 요소로 모듈화됩니다. 높은 수준 조각이 이러한 하위 조각을 참조합니다. 고급 유효성 검사 규칙과 같은 더 많은 데이터 유형 개선 사항은 [!DNL Content Fragments] 을 사용하여 컨텐츠 모델링의 유연성을 더욱 향상시킵니다. [!DNL Experience Manager] [!DNL Content Fragment] 편집기는 구조 트리 보기 및 조각 계층을 통한 탭 탐색 표시 탐색과 같은 향상된 기능을 사용하여 공통 편집기 세션에서 중첩된 조각 구조를 지원합니다.

* **GraphQL API 대상[!DNL Content Fragments]**: 새로운 GraphQL API는 구조화된 컨텐츠를 JSON 형식으로 제공하는 표준 방법입니다. GraphQL 쿼리를 사용하면 클라이언트가 경험을 렌더링하기 위해 관련 콘텐츠 항목만 요청할 수 있습니다. 이러한 선택을 통해 클라이언트 측에서 컨텐츠 구문 분석이 필요한 컨텐츠 over-delivery(HTTP REST API의 경우 가능성)가 제거됩니다. GraphQL 스키마는 [!DNL Content Fragment] 모델에서 파생되며 API 응답은 JSON 형식으로 이루어집니다. [!DNL Experience Manager]에서 [!DNL Cloud Service], [GraphQL 쿼리는](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html#persisted-queries-caching)을 지속하고 캐시 친화적인 GET 요청을 처리합니다. 아직 [!DNL Experience Manager] 6.5.10.0에서는 사용할 수 없습니다.

* **계층 관리 및 향후 미리 보기**: 이제 사용자에게는 론치에서 페이지를 추가 및 제거하는 기능을  [!DNL Experience Manager] 포함하여 론치의 컨텐츠 구조에 액세스할 수 있는 인터페이스가 제공됩니다. 이 기능은 향후 게시를 위해 타깃팅된 컨텐츠 버전을 작성할 수 있도록 [!DNL Experience Manager] 론치의 유연성을 향상시킵니다. [타임워프 기능](/help/sites-authoring/working-with-page-versions.md#timewarp) 을 사용하면 향후 컨텐츠 상태로 론치를 미리 볼 수 있습니다.

* **연결된 자산**:  [!DNL Experience Manager] 기능 [!DNL Connected Assets] 을 해당 핵심 구성 요소에서  [!DNL Dynamic Media] 이미지 사용으로 확장합니다. [연결된 자산 사용](/help/assets/use-assets-across-connected-assets-instances.md)을 참조하십시오.

* **링크 공유 옵션을 사용하여 자산 또는 표현물을 다운로드합니다**. 자산 및 컬렉션을 링크로 공유할 때 사용자는 원본 자산의 다운로드를 허용할지, 렌디션을 허용할지 또는 공유 링크를 사용하여 둘 다 다운로드하도록 허용할지를 선택할 수 있습니다. 또한 링크를 통해 공유된 자산을 다운로드하는 사용자는 원본 자산만, 표현물만 또는 두 가지 모두를 다운로드할 수 있습니다.

* **생성된 하위 자산 제한**: 관리자는 PDF, PowerPoint, InDesign 및 Keynote 파일과 같은 복합 자산에 대해  [!DNL Experience Manager] 생성되는 하위 자산 수를 제한할 수 있습니다. [조합 자산 관리](/help/assets/managing-linked-subassets.md#generate-subassets)를 참조하십시오.

* **Camera Raw 지원**:  [!DNL Camera Raw] v10.4 [!DNL Adobe Camera Raw] 를 지원하는 새 패키지를 사용할 수 있습니다.  [를  [!DNL Camera Raw]](/help/assets/camera-raw.md)사용하여 이미지 처리를 참조하십시오.

* 내장된 저장소(Apache Jackrabbit Oak)가 1.22.8.

* **접근성 개선**:

   * [!DNL Dynamic Media] 에서는 뷰어에 대해 많은 액세스 가능성이 개선되었습니다. [[!DNL Dynamic Media] 업데이트](#dynamic-media-65100)를 참조하십시오.

   * Platform은 몇 가지 액세스 가능성이 개선되었습니다. [플랫폼 업데이트](#platform-65100)를 참조하십시오.

* **사용자 환경 개선 사항**:

   * [!DNL Experience Manager] 컨텐츠 작성자가 파일 구조를 탐색하지 않고도 폴더 아래에 모든 컨텐츠 모델의 목록을 직접 표시합니다. 이제 이 기능을 사용하려면 클릭이 적고 작성 효율성이 향상됩니다.

   * [!DNL Sites] 편집기의 경로 필드를 사용하면 작성자가 [!DNL Content Finder]에서 자산을 드래그할 수 있습니다.

[!DNL Experience Manager] 6.5.10.0에 도입된 모든 기능 및 개선 사항 목록은 [6.5 서비스 팩 10](new-features-latest-service-pack.md)의 새로운 기능 을 참조하십시오. [!DNL Adobe Experience Manager] 

다음은 [!DNL Experience Manager] 6.5.10.0 릴리스에서 제공된 수정 사항 목록입니다.

### [!DNL Sites] {#sites-65100}

* 컨텐츠 조각 편집기의 **[!UICONTROL 속성]** 탭 아래에 있는 **[!UICONTROL 기본값]** 필드에 입력할 때 포커스가 다른 필드로 이동합니다(NPR-36992).

* 지정된 경로 아래에 [!DNL Content Fragment] 모델을 필터링하는 동안 [!DNL Content Fragment] 모델에 대해서만 경로 및 노드를 반환하는 대신 `cq:Template`가 있는 모든 노드를 반환합니다(SITES-1453).[!DNL Experience Manager]
* [!DNL Content Fragments] 폴더  `null` 상태로 를 반환합니다(SITES-1157).
* [!DNL Experience Manager] 사용자가 모델을 비활성화하고 활성화하지  [!DNL Content Fragment] 않도록 합니다(SITES-1088).
* 사용자가 [!DNL Content Fragments] 또는 미디어 자산을 이동, 이름 변경 또는 삭제하면 참조된 [!DNL Content Fragments]이 자동으로 업데이트되지 않습니다(SITES-196).
* 한 페이지에서 다른 페이지에 구성 요소를 붙여넣으면 JavaScript 오류가 발생합니다(NPR-37030).
* 페이지 속성을 빠르게 보면 다른 페이지에 대한 페이지 속성 이 열립니다(NPR-37025).
* 컨텐츠 조각을 사용하면 컨텐츠 조각이 자신을 참조할 수 있습니다. 선택기가 작업을 지원하지 않습니다(NPR-36993).
* 서비스 팩 9로 업그레이드한 후 일부 사용자는 Experience Manager에서 폴더를 이동할 수 없으며 로그에 오류가 표시됩니다(SITES-1481).
* 편집 모드의 레이아웃 컨테이너에서 구성 요소의 너비를 조정하는 동안 깜박임이 관찰됩니다(NPR-36961).
* 론치 홍보 시, 판촉된 론치의 변경 사항은 다른 론치에 두 번 롤아웃됩니다. 사용자가 이중 롤아웃된 론치를 홍보하면 두 개의 컨텐츠가 소스 페이지에 반영됩니다(NPR-36893).
* [!DNL Experience Manager] 이미지 코어 구성 요소를 사용하여 페이지에 이미지를 추가하거나 기초 이미지 구성 요소를 사용하여 크기를 조정하는 경우 투명도가 있는 일부 PNG 이미지에 회색 테두리를 추가합니다(NPR-36879).
* [!DNL Experience Manager Sites] 템플릿이 많은 관리자 UI가 있으면 탐색 속도가 느려집니다(NPR-36870).
* 서비스 팩 9로 업그레이드하면 일부 구성 요소가 작성되지 않습니다. 이 문제로 인해 [!DNL Sites] 사용자가 새 페이지를 만들 수 없습니다(NPR-36857).
* `ContextHubImpl` 메서드는 닫히지 않은 `ResourceResolver`을 만듭니다. 이로 인해 오래 실행되는 `ResourceResolver`에 대한 경고 메시지가 표시되고 서비스가 때때로 예기치 않은 결과를 반환합니다(NPR-36853).
* 블루프린트 페이지 속성에서 단일 Live Copy를 동기화할 때 다른 모든 Live Copy도 동기화됩니다(NPR-36829, NPR-36522).
* XLS MIME 유형만 사용하는 경우 파일 업로드 기능이 예상대로 작동하지 않습니다(NPR-36785).
* 파스칼 대/소문자를 사용하는 새 태그는 [!DNL Content Fragments] 내의 태그 필드에 표시되지 않습니다(NPR-36742).
* [!DNL Content Fragment]을 추가할 때 단일 텍스트 요소 옵션을 사용하면 텍스트가 누락되고 목록 및 중첩 목록과 관련된 홀수 서식이 만들어집니다(NPR-36565).
* 작성자가 페이지의 구성 요소에 주석을 달고, 구성 요소를 삭제하고, 삭제 작업에 대한 실행 취소를 수행하면 사이트 콘솔에서 페이지의 타임라인 데이터를 확인하려고 할 때 오류가 발생합니다(NPR-36528).
* 페이지 속성 벌크 편집기의 [!UICONTROL 저장 및 닫기] 옵션은 변경 사항을 저장하지만 편집기를 닫지는 않습니다(NPR-36527).
* 사용자가 새 텍스트 구성 요소를 페이지에 끌어다 놓으려고 하면 구성 요소가 즉시 사라집니다(NPR-36442).
* 사용자가 공간(시스템에 없는 태그)이 포함된 온디맨드 태그에 입력하고 enter 키를 누르면 태그가 필드 아래에 나타납니다. 그러나 [!DNL Content Fragment] 이 저장되고 다시 열면 온디맨드 태그가 표시되지 않습니다(NPR-36441).
* Dispatcher를 통해 인스턴스에 액세스하면 템플릿을 삭제할 수 없습니다(NPR-36385).
* 페이지를 이동할 때 변경 사항을 렌더링하려면 브라우저를 수동으로 새로 고쳐야 합니다(NPR-36381).
* 구성 요소를 선택할 때 Ctrl+X 또는 Ctrl+C(Mac의 경우 Command+X 또는 Command+C)를 사용하여 구성 요소를 잘라내거나 복사할 수 있습니다. 다른 구성 요소를 클릭하면 도구 모음을 사용하여 붙여넣을 수 있지만 키보드(Ctrl+V 또는 Command+V)는 붙여넣을 수 없습니다(NPR-36379).
* 사용자가 가위 아이콘을 사용하여 구성 요소를 잘라내어 다른 위치로 이동하려고 하면 콘솔 오류가 발생합니다. 또한 구성 요소를 한 개만 붙여넣을 경우 이동됩니다(NPR-36378).
* [!DNL Experience Manager] wcm 또는 알림에 색인이 없는 쿼리가 있으면 성능이 저하됩니다(NPR-36303).
* 작성자가 삭제된 상속된 구성 요소에서 상속을 복원할 때 사용 가능한 옵션은 모든 페이지 컨텐츠를 동기화하는 것입니다. 상속이 한 구성 요소에서만 복원되는 경우에도 컨텐츠 작성자는 전체 페이지를 동기화해야 합니다. 전체 동기화를 수행하면 원치 않는 콘텐츠가 동기화될 수 있습니다(NPR-34456, CQ-4310183).
* 작성자 인스턴스에서 구성 요소의 라이브 사용량 이 모든 발생을 표시하지 않습니다. 일부 구성 요소는 1000개 이상의 페이지에서 사용되지만 보고서에는 약 40페이지만 표시됩니다(CQ-4323724).
* 하위 페이지가 많은 사이트 구조가 있는 경우 열 보기에서 하위 페이지를 로드하는 데 Experience Manager 6.4.8.2와 비교하여 Experience Manager 6.5.8에서 더 많은 시간이 소요됩니다(CQ-4322766).
* &#39;페이지 롤아웃&#39; 옵션에서 &#39;모두&#39;가 작동하지 않습니다(NPR-37070).
* 페이지의 기존 v3 구성 요소 버전을 열 때 페이지 속성 대화 상자가 열리지 않고 `NullPointerException`이 기록됩니다(SITES-1830).

### [!DNL Assets] {#assets-65100}

다음 문제가 [!DNL Assets]에서 해결되었습니다.

* 폴더를 이동한 후 게시 인스턴스에서 `jcr:title` 속성 값이 업데이트되지 않습니다. 작성자 내에서 폴더 이름을 변경하고 다시 게시해도 게시 인스턴스에서 같은 `jcr:title` 속성 값이 업데이트되지 않습니다(NPR-36369).

* 두 개 이상의 자산을 선택하고 하나 이상의 메타데이터 필드를 편집하면 Safari 브라우저의 오류 코드 500으로 저장 작업이 실패합니다(NPR-36413).

* 잘못된 날짜 포맷으로 인해 벌크 메타데이터 가져오기에 실패합니다(NPR-36428).

* [!UICONTROL 속성] 페이지에서 메타데이터를 업데이트하도록 선택한 경우 스키마에서 제공하는 옵션이 많으면 인터페이스가 느리게 응답합니다(NPR-36430).

* [!UICONTROL 만료 상태] 설명을 사용한 검색 필터가 작동하지 않습니다(NPR-36436).

* [!UICONTROL 폴더 메타데이터] 속성의 여러 필드에 대한 팝업 메뉴에 마지막으로 선택한 값이 표시되지 않습니다(NPR-36937, CQ-4314429).

* 파일 및 폴더를 검색할 때 사용자가 필터를 적용하고 [!UICONTROL 파일 및 폴더]를 선택하면 파일만 표시되지만 폴더는 표시되지 않습니다(CQ-4319543, NPR-36627).

* 도구 모음 옵션은 폴더 내에서 동일한 컬렉션을 선택하고 검색 결과에서 선택되면 다릅니다(NPR-36620).

* [!UICONTROL 빠른 게시] 옵션은 검색 결과 페이지에서 사용할 수 없습니다(NPR-36904, CQ-4317748).

* 사용자가 확장을 지정하지 않고 자산의 Live Copy를 만들면 Live Copy 파일을 다운로드한 후에는 사용할 수 없습니다(NPR-36903, CQ-4326305).

* 사용자가 하위 폴더의 소유자로 추가되면 사용자는 상위 폴더의 소유자 권한도 부여받아 상위의 다른 하위 폴더도 갖게 됩니다. 또한 사용자를 제거하려고 할 때 상위 폴더의 소유자로 제거되지 않습니다. (NPR-36801, CQ-4323737).

* [!DNL Experience Manager] powerPoint 프레젠테이션과 같은 복합 자산에 대한 하위 자산을 만들려고 하면 메모리 부족 예외가 발생합니다(NPR-36668).

* 게시된 사이트 페이지에서 이미 사용된 자산을 이동하면 게시할 옵션이 선택되어 있지 않더라도 사이트 페이지가 다시 게시됩니다(NPR-36636, CQ-4323500).

* Apache Tika MIME 유형 탐지 기능을 사용하는 경우 `AssetManager.createAsset` 메서드를 사용하여 업로드한 자산은 임시 디렉터리에 `apache-tika-*.tmp` 파일이라는 임시 파일을 둡니다. 이 임시 파일은 사용 가능한 모든 디스크 공간을 사용합니다(NPR-36545).

* 모든 DRM 보호 자산이 다운로드되고 특정 자산을 다운로드할 사용자 선택이 수행되지 않습니다(CQ-4327422).

* 사용자 인터페이스에서 자산을 `pathfield`(으)로 드래그할 수 없습니다(NPR-36849).

* 열 보기에서 자산을 선택하면 자산 세부 사항 패널이 사라집니다(NPR-36667).

### [!DNL Dynamic Media] {#dynamic-media-65100}

**접근성 개선**

[!DNL Dynamic Media Viewers]에서는 다음과 같은 액세스 가능성이 개선되었습니다.

* 이제 화면 판독기에서 검색할 자리 표시자 텍스트에 나레이션을 지정하고 링크 대화 상자로 자산 공유 시 필수 필드로 이메일 주소를 추가하고, [!UICONTROL 이 필드] 도구 설명을 채우십시오(CQ-4327761).

* 이제 화면 판독기에서 키보드를 사용하여 사용자 인터페이스 필드에 액세스할 때 [!UICONTROL 이미지 사전 설정 편집기]에 있는 다양한 필드의 이름과 목적에 대해 올바르게 내레이션합니다(CQ-4325677).

* 이제 키보드 포커스가 [!UICONTROL 리치 미디어 유형] 옵션의 자산 선택기에서 [!UICONTROL 뷰어 사전 설정] 대화 상자의 검색 탭으로 적절하게 이동합니다(CQ-4324736).

* 키보드 키를 사용하여 양식 모드로 이동할 때 화면 판독기는 [!UICONTROL 이미지 사전 설정]의 [!UICONTROL 만들기] 탭에서 증가 및 감소 옵션에 해당하는 레이블을 내레이션합니다(CQ-4323900).

* 이제 화면 판독기에 링크로 자산 공유 대화 상자에 [!UICONTROL 이메일 주소] 검색 및 추가 옵션이 표시됩니다(CQ-4323352).

* 키보드 키를 사용하여 자산을 탐색할 때 도구 모음에 키보드 포커스가 유지됩니다(CQ-4322037).

* 이제 화면 판독기는 [!UICONTROL 이미지 처리 프로필 편집] 페이지에서 [!UICONTROL 응답형 이미지 자르기] 옵션을 선택한 후 새로 추가한 [!UICONTROL 편집] 필드 정보에 나레이션합니다(CQ-4290734).

* [!UICONTROL 이미지 사전 설정 편집] 및 [!UICONTROL 대화형 비디오 만들기] 페이지에서 화면 판독기는 이제 제목 키보드 단축키 를 사용하여 페이지를 탐색할 때 페이지 머리글을 적절히 알려줍니다(CQ-4290730)(CQ-4290701).

* 이제 화면 판독기에서 다음 페이지를 탐색할 때 랜드마크 및 영역 단축키를 사용하여 화면의 다양한 영역(예: 오른쪽 패널 영역, 왼쪽 패널, 작업 도구 모음, 뷰어 도구 모음 랜드마크 및 확대/축소 가능한 이미지 랜드마크)을 인식할 수 있습니다.

   * [!UICONTROL 뷰어 사전 설정 편집기] (CQ-4290729)

   * [!UICONTROL 이미지 세트 편집기] (CQ-4290710)

   * [!UICONTROL 대화형 비디오 만들기] (CQ-4290702).

* 이제 화면 판독기에서 아래쪽 화살표 키를 사용하여 탐색할 때 비디오 프레임에 공유 옵션의 이름이 표시됩니다(CQ-4290728).

* 이제 화면 판독기에서 [!UICONTROL 뷰어 사전 설정 편집기]에 있는 [!UICONTROL Sprite] 및 [!UICONTROL 배경] 탭의 다양한 옵션에 대한 이름을 나레이션합니다(CQ-4290727).

* [!UICONTROL Width] 필드를 편집하는 필드와 같은 필수 필드는 [!UICONTROL 비디오 인코딩 편집] 페이지의 [!UICONTROL Basic] 탭에 별표 기호(*)가 있습니다(CQ-4290725).

* 이제 화면 판독기에 [!UICONTROL 이미지 프로필] 페이지의 옵션에 대한 레이블이 표시됩니다(CQ-4290723).

* 이제 Windows 사용자는 포커스가 CSS 편집기에 있을 때 [!UICONTROL 뷰어 사전 설정 편집기]에서 확장된 CSS 편집기를 탐색할 수 있습니다(CQ-4290720).

* 양식 모드로 탐색할 때 [!UICONTROL 이미지 사전 설정 편집]의 [!UICONTROL 기본] 탭에서 화면 판독기에서 이제 다양한 편집 필드 및 옵션에 대한 레이블에 내레이션이 적용됩니다(CQ-4290717).

* 이제 화면 판독기는 자산의 세부 사항 페이지에서 왼쪽 탐색 영역에서 사용자 인터페이스 옵션에 대한 역할 및 상태(선택 또는 선택되지 않음)에 내레이션합니다(CQ-4290709).

* 이제 화면 판독기에서 이미지에 대한 상태(선택 또는 선택되지 않음)를 올바르게 내레이트하고 이미지에 대한 링크를 [!UICONTROL 대화형 비디오 만들기] 페이지의 [!UICONTROL Content] 탭에서 전환합니다(CQ-4290707).

* 이제 화면 판독기는 [!UICONTROL 대화형 비디오 만들기] 페이지에서 아래쪽 화살표 키를 사용하여 탐색할 때 비디오 타임라인 배율에서 다양한 세그먼트의 이름, 역할 및 상태에 대해 올바르게 내레이션합니다(CQ-4290706).

* 이제 화면 판독기는 [!UICONTROL 대화형 비디오 만들기] 페이지에서 옵션을 탐색할 때 이름, 역할 및 기본 상태(선택 또는 선택되지 않음)와 속성에 내레이션이 적용됩니다(CQ-4290704).

* 이제 화면 판독기는 [!UICONTROL 게시] 페이지를 탐색할 때 [!UICONTROL 모든 자산] 및 [!UICONTROL 모든 컬렉션] 옵션에 있는 옵션의 이름, 역할 및 기본 상태(선택 또는 선택되지 않음)에 내레이션합니다(CQ-4290705).

* [!UICONTROL 대화형 비디오 만들기] 페이지에서 지원되지 않는 비디오 형식(MP4 제외)을 업로드하면 Experience Manager이 오류 메시지를 표시하고 알려줍니다(CQ-4290700).

* [!UICONTROL 대화형 비디오 만들기] 페이지의 타임라인 배율에 있는 숫자(초)의 대비가 이제 필요한 최소 광도 비율을 충족하므로 색상 인식이 제한된 사용자가 쉽게 읽을 수 있습니다(CQ-4290699).

* 이제 화면 판독기에 [!UICONTROL 대화형 비디오 만들기] 페이지를 탐색할 때 [!UICONTROL 제품 이름] 필드에 대한 레이블이 표시됩니다(CQ-4290697).

**해결된 문제**

다음 버그 수정 사항은 [!DNL Dynamic Media]에서 사용할 수 있습니다.

* `dynamicmedia_scene7` 실행 모드가 활성화되고 동기화가 비활성화되면 [!DNL Experience Manager]에 업로드된 비디오가 `Process failed`에 표시됩니다(CQ-4327791).

### 플랫폼 {#platform-65100}

이 서비스 팩에는 다음과 같은 향상된 기능이 제공됩니다.

* 사용자가 트리 보기에서 항목을 선택하면 화면 판독기에 선택 사항과 맨 위에 표시되는 도구 모음 옵션이 표시됩니다(NPR-36504).
* 광도 비율이 필요한 최소 4.5:1 비율을 충족하므로 일부 텍스트 및 컨트롤 이름은 비전 문제가 있는 사용자가 쉽게 읽을 수 있습니다(NPR-36503).
* 사용자가 달력 컨트롤을 사용하면 화면 판독기에서 설명 날짜, 월 및 요일 정보에 내레이션이 적용됩니다. 사용자가 달력 단축키를 사용하면 화면 판독기에 날짜, 월 및 연도의 변경 내용이 내레이션됩니다(NPR-36498).
* 엄격한 모드를 사용하지 않고 ECMAScript 6 기능을 사용하여 사용자 지정 JavaScript `Clientlibs`을 실행하도록 지원합니다. 특히 `emitUseStrict` 플래그가 `GCCScriptProcessor`에 추가됩니다(NPR-36411).

다음 버그 수정이 이 서비스 팩의 일부입니다.

* 사용자 지정 상태 검사가 예약보다 더 자주 실행됩니다(NPR-36985).
* `Resourceresolver map` 메서드는 별칭 페이지에 대해 잘못된 결과를 반환합니다(NPR-36767).
* [!DNL Experience Manager] 워크플로우 로드로 인해 시작 지연이 발생합니다(NPR-36615).

### 통합 {#integrations-65100}

* 기본 MongoDB 노드가 다른 노드로 전환되면 Experience Manager이 응답하지 않습니다(NPR-36566).
* [!DNL Sling content distribution] 컬렉션 구성원 삭제 작업을 수행할 때 실패합니다(NPR-36521, CQ-4323578).

### 사용자 인터페이스 {#user-interface-65100}

* **[!UICONTROL 참조]** 사이드 패널은 자산 및 사이트 참조를 표시하지 않습니다(GRANITE-35078, GRANITE-34892).

### 번역 프로젝트 {#translation-65100}

* 다중 번역 프로젝트의 언어 복사본에 추가 하위 페이지가 삭제됩니다(NPR-36622).

### 워크플로우 {#workflow-65100}

* 서버가 부재 중 메시지를 받으면 메모리 경고를 보고하고 응답을 중지합니다(NPR-36768).

### [!DNL Communities] {#communities-65100}

* 커뮤니티 사이트 페이지가 익명의 게스트 사용자에 대해 `LoggedIn` 상태로 열립니다(NPR-36908).

* **[!UICONTROL 커뮤니티]** > **[!UICONTROL 아이디어]** > **[!UICONTROL 댓글]** 페이지에 페이지가 두 개 이상 있는 경우 페이지 탐색 기능이 작동하지 않습니다(NPR-36541).

<!--
Need to verify with Engineering, the status is currently showing as Resolved
-->


<!--
### [!DNL Brand Portal] {#brandportal-65100}

*
-->

### [!DNL Forms] {#forms-65100}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] 는 예정된  [!DNL Experience Manager] 서비스 팩 릴리스 날짜로부터 1주일 후에 추가 기능 패키지를 출시합니다.


### 상거래 {#commerce-65100}

* **[!UICONTROL 게시됨 By]** 필드의 값이 열 보기에서 잘못되었습니다(NPR-36902).
* 카탈로그가 롤아웃되면 새 제품이 수정된 제품으로 잘못 표시됩니다(NPR-36666).
* 삭제된 제품을 다시 만들 때 제품 페이지가 다시 만들어지지 않습니다(NPR-36665).
* 수정된 페이지가 업데이트되지만 연결된 해당 제품이 카탈로그 롤아웃 시 업데이트되지 않습니다(CQ-4321409, NPR-36422).
* **[!UICONTROL 나중에 게시]** 및 **[!UICONTROL 나중에 게시 취소]** 워크플로우가 작동하지 않습니다(CQ-4327679).

보안 업데이트에 대한 자세한 내용은 [[!DNL Experience Manager] 보안 게시판 페이지](https://helpx.adobe.com/security/products/experience-manager.html)를 참조하십시오.

## 6.5.10.0 설치 {#install}

**설치 요구 사항 및 추가 정보**

* Experience Manager 6.5.10.0을 사용하려면 Experience Manager 6.5가 필요합니다. 세부 지침은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하십시오.
* 서비스 팩은 Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 다운로드할 수 있습니다.
* MongoDB 및 여러 인스턴스가 포함된 배포에서 패키지 관리자를 사용하여 작성자 인스턴스 중 하나에 Experience Manager 6.5.10.0을 설치합니다.

>[!NOTE]
>
>Adobe에서는 [!DNL Adobe Experience Manager] 6.5.10.0 패키지를 삭제하거나 제거하지 않는 것이 좋습니다.

### 서비스 팩 설치 {#install-service-pack}

[!DNL Adobe Experience Manager] 6.5 인스턴스에 서비스 팩을 설치하려면 다음 단계를 수행하십시오.

1. 인스턴스가 업데이트 모드(이전 버전에서 인스턴스가 업데이트되었을 때)인 경우 설치하기 전에 인스턴스를 다시 시작합니다. Adobe은 인스턴스에 대한 현재 가동 시간이 높은 경우 다시 시작할 것을 권장합니다.

1. 설치하기 전에 스냅샷 또는 [!DNL Experience Manager] 인스턴스의 새 백업을 만듭니다.

1. [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip)에서 서비스 팩을 다운로드하십시오.

1. 패키지 관리자를 열고 **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭하여 패키지를 업로드합니다. 자세한 내용은 [패키지 관리자](/help/sites-administering/package-manager.md)를 참조하십시오.

1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

1. S3 커넥터를 업데이트하려면 서비스 팩을 설치한 후 인스턴스를 중지하고 기존 커넥터를 설치 폴더에 제공된 새 이진 파일로 바꾸고 인스턴스를 다시 시작합니다. [Amazon S3 데이터 저장소](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)를 참조하십시오.

>[!NOTE]
>
>패키지 관리자 UI에 대한 대화 상자가 서비스 팩을 설치하는 동안 종료되는 경우가 있습니다. 배포에 액세스하기 전에 오류 로그가 안정될 때까지 기다리는 것이 좋습니다. 업데이터 번들 제거와 관련된 특정 로그를 기다린 후 설치가 성공했는지 확인합니다. 일반적으로 이 문제는 [!DNL Safari] 브라우저에서 발생하지만 모든 브라우저에서 간헐적으로 발생할 수 있습니다.

**자동 설치**

작업 인스턴스에 [!DNL Experience Manager] 6.5.10.0을 자동으로 설치하는 두 가지 방법이 있습니다.

A. 서버가 온라인 상태일 때 패키지를 `../crx-quickstart/install` 폴더에 넣습니다. 패키지가 자동으로 설치됩니다.

B. [패키지 관리자에서 HTTP API](/help/sites-administering/package-manager.md#package-share)를 사용합니다. 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

>[!NOTE]
>
>Adobe Experience Manager 6.5.10.0은 Bootstrap 설치를 지원하지 않습니다.

**설치 확인**

1. 제품 정보 페이지(`/system/console/productinfo`)에는 [!UICONTROL 설치된 제품] 아래에 업데이트된 버전 문자열 `Adobe Experience Manager (6.5.10.0)`이 표시됩니다.

1. 모든 OSGI 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]**&#x200B;이거나 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 콘솔 사용: `/system/console/bundles`).

1. OSGi 번들 `org.apache.jackrabbit.oak-core`은 버전 1.22.3 이상에 있습니다(웹 콘솔 사용: `/system/console/bundles`)

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

Experience Manager 6.5.10.0용 UberJar는 [Maven 중앙 저장소](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.10/)에서 사용할 수 있습니다.

Maven 프로젝트에서 UberJar를 사용하려면 [Uberjar 사용 방법](/help/sites-developing/ht-projects-maven.md)을 참조하여 프로젝트 POM에 다음 종속성을 포함하십시오.

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.10.0</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar 및 기타 관련 가공물은 Adobe Public Maven 저장소(`repo.adobe.com`) 대신 Maven 중앙 저장소에서 사용할 수 있습니다. 기본 UberJar 파일의 이름이 `uber-jar-<version>.jar`로 변경되었습니다. 따라서 `dependency` 태그에 대해 `apis` 값이 있는 `classifier`이 없습니다.

## 이제 사용되지 않는 기능 {#removed-deprecated-features}

다음은 [!DNL Experience Manager] 6.5.7.0에서 더 이상 사용되지 않는 것으로 표시된 기능 및 기능 목록입니다. 기능은 처음에 더 이상 사용되지 않으며 이후 릴리스에서 이후에 제거됩니다. 다른 옵션이 제공됩니다.

배포에서 기능 또는 기능을 사용하는지 검토합니다. 또한 대체 옵션을 사용하도록 구현을 변경할 계획입니다.

| 영역 | 기능 | 대체 |
|---|---|---|
| 통합 | **[!UICONTROL AEM 클라우드 서비스 옵트인]** 화면은 [!DNL Experience Manager] 및 [!DNL Adobe Target] 통합이 Experience Manager 6.5에서 업데이트되므로 더 이상 사용되지 않습니다. 통합은 Adobe Target Standard API를 지원합니다. API는 Adobe IMS 및 [!DNL Adobe I/O]을 통해 인증을 사용하고, 분석 및 개인화를 위해 [!DNL Experience Manager] 페이지를 계측하는 Adobe Launch의 늘어나는 역할을 지원하며, 옵트인 마법사가 기능상 무관합니다. | 각각의 [!DNL Experience Manager] 클라우드 서비스를 통해 시스템 연결, Adobe IMS 인증 및 [!DNL Adobe I/O] 통합을 구성합니다. |
| 커넥터 | Microsoft® SharePoint 2010 및 Microsoft® SharePoint 2013용 Adobe JCR 커넥터는 Experience Manager 6.5에서 더 이상 사용되지 않습니다. | N/A |

## 알려진 문제 {#known-issues}

* [!DNL Experience Manager] 인스턴스를 6.5에서 6.5.10.0 버전으로 업그레이드하는 경우 `error.log` 파일에서 `RRD4JReporter` 예외를 볼 수 있습니다. 문제를 해결하려면 인스턴스를 다시 시작합니다.

* [!DNL Experience Manager] 6.5 서비스 팩 10 또는 이전 서비스 팩을 [!DNL Experience Manager] 6.5에 설치하는 경우 자산 사용자 지정 워크플로우 모델(`/var/workflow/models/dam`에서 만들어짐)의 런타임 복사본이 삭제됩니다.
런타임 복사본을 검색하려면 Adobe에서 HTTP API를 사용하여 사용자 지정 워크플로우 모델의 디자인 타임 사본을 해당 런타임 복사와 동기화하는 것이 좋습니다.
   `<designModelPath>/jcr:content.generate.json`.

* 사용자는 [!DNL Assets]에서 계층 구조의 폴더의 이름을 변경하고 중첩된 폴더를 [!DNL Brand Portal]에 게시할 수 있습니다. 그러나 루트 폴더가 다시 게시될 때까지 폴더의 제목이 [!DNL Brand Portal]에서 업데이트되지 않습니다.

* 사용자가 적응형 양식에서 처음으로 필드를 구성하도록 선택하면 구성 저장 옵션이 속성 브라우저에 표시되지 않습니다. 동일한 편집기에서 적응형 양식의 다른 필드 일부를 구성하도록 선택하면 문제가 해결됩니다.

* 6.5.x.x Experience Manager 설치 중에 다음 오류 및 경고 메시지가 표시될 수 있습니다.
   * Target Standard API(IMS 인증)를 사용하여 Experience Manager에 Adobe Target 통합이 구성된 경우 환경 조각을 Target으로 내보내면 잘못된 오퍼 유형이 생성됩니다. 경험 조각/소스 Adobe Experience Manager 유형 대신 Target은 HTML/소스 Adobe Target Classic 유형으로 여러 가지 오퍼를 작성합니다.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: granite/operations/maintenance에 유지 관리 창이 없습니다.
   * SUM, MAX 및 MIN과 같은 집계 함수를 사용하는 경우 적용형 양식 서버측 유효성 검사가 실패합니다(CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance에 유지 관리 창이 없습니다.
   * 쇼퍼블 배너 뷰어를 통해 자산을 미리 볼 때 Dynamic Media 대화형 이미지의 핫스팟이 표시되지 않습니다.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : 등록 변경으로 등록 취소를 완료할 때까지 기다리는 중 시간이 초과되었습니다.

## OSGi 번들 및 컨텐츠 패키지가 포함됨 {#osgi-bundles-and-content-packages-included}

다음 텍스트 문서에는 [!DNL Experience Manager] 6.5.10.0에 포함된 OSGi 번들 및 컨텐츠 패키지 목록이 나와 있습니다.

* [Experience Manager 6.5.10.0에 포함된 OSGi 번들 목록](assets/65100_bundles.txt)

* [Experience Manager 6.5.10.0에 포함된 컨텐츠 패키지 목록](assets/65100_packages.txt)

## 제한된 웹 사이트 {#restricted-sites}

이러한 웹 사이트는 고객만 사용할 수 있습니다. 액세스가 필요한 고객의 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [Adobe 고객 지원 센터에 문의하는 방법](https://experienceleague.adobe.com/docs/customer-one/using/home.html)을 참조하십시오.

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5 릴리스 노트](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] 제품 페이지](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 설명서](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ko-KR)
>* [Adobe 우선 순위 제품 업데이트](https://www.adobe.com/subscription/priority-product-update.html) 구독

