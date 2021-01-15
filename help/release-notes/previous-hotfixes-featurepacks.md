---
title: '[!DNL Adobe Experience Manager] 6.5 이전 서비스 팩 릴리스 노트.'
description: ' [!DNL Adobe Experience Manager] 6.5 서비스 팩에 대한 릴리스 노트입니다.'
contentOwner: AK
translation-type: tm+mt
source-git-commit: 0560eb8e3c127964920827609a9982acf07b515f
workflow-type: tm+mt
source-wordcount: '14944'
ht-degree: 76%

---


# 이전 서비스 팩에 포함된 핫픽스 및 기능 팩 {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## [!DNL Adobe Experience Manager] 6.5.6.0  {#experience-manager-6560}

Adobe Experience Manager 6.5.6.0은 **2019년 4월** 6.5 릴리스의 공식 출시 이후 릴리스된 새로운 기능, 주요 고객이 요청한 향상된 기능 및 성능, 안정성, 보안 개선 사항이 포함된 중요한 업데이트입니다. Adobe Experience Manager 6.5 맨 위에 설치할 수 있습니다.

Adobe Experience Manager 6.5.6.0에 도입된 주요 기능 및 개선 사항은 다음과 같습니다.

* [!UICONTROL 빠른 게시] 또는 [!UICONTROL 발행물 관리] 마법사를 사용하여 선택적으로 자산을 [!DNL Experience Manager] 또는 [!DNL Dynamic Media]에 게시하거나 게시를 취소합니다.

* [!DNL Dynamic Media] 사용자 인터페이스를 사용하여 CDN(Content Delivery Network) 캐시된 컨텐츠를 무효화합니다.

* 이제 프록시 서버를 통해 브랜드 포털에서 Experience Manager 자산에 자산 기여도 폴더를 게시하는 것도 지원됩니다.

* 이제 [!DNL Experience Manager Assets]의 개인 폴더를 삭제할 때 자동 생성된 비공개 폴더 그룹이 정리됩니다.

* 비디오 [!UICONTROL 뷰어] 사전 설정 편집기의 수정자에 대한 설명이 [!DNL Dynamic Media]에서 업데이트되었습니다.

* [!DNL Dynamic Media] 커넥터의 상태를 반영하도록 새 회사 설정이 제공됩니다.

* 사용자가 축소판만 만들고 페이지 추출 및 키워드 추출을 건너뛸 수 있도록 이전에 Dynamic Media의 `Rasterize`에서 `test` 및 `aiprocess`에 대한 기본 옵션이 `Thumbnail`로 업데이트되었습니다.

* [클라이언트에서 적응형 양식을 미리 채웁니다](../../help/forms/using/prepopulate-adaptive-form-fields.md#prefill-at-client).

* [양방향 SSL 구현을 통해 서버에서 RESTful API와 양식 데이터 모델 통합을 참조하십시오](../../help/forms/using/configure-data-sources.md).

* [번역된 적응형 양식 페이지에 대한 캐싱 기능이 향상되었습니다](../../help/forms/using/configure-adaptive-forms-cache.md).

* automated forms conversion 서비스](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html)의 [Adobe Sign 텍스트 태그 지원.

* [!DNL Automated Forms Conversion service]을(를) 사용하여 컬러 양식을 응용 양식](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html)으로 변환할 수 있습니다.[

* SMB 2 및 SMB 3 프로토콜 지원

* 내장된 저장소(Apache Jackrabbit Oak)가 버전 1.22.4으로 업데이트되었습니다.

Experience Manager 6.5.6.0에 도입된 기능과 개선 사항의 전체 목록은 [Adobe Experience Manager 6.5 서비스 팩 6의 새로운 기능](new-features-latest-service-pack.md)을 참조하십시오.

다음은 [!DNL Experience Manager] 6.5.6.0 릴리스에서 제공된 수정 사항 목록입니다.

### [!DNL Sites] {#sites-6560}

* [!DNL Sites] 또는 [!DNL Screens]에서 프로젝트를 선택하고 [!UICONTROL 관리 발행물]을 클릭합니다. 사용자 인터페이스 오류로 인해 [!UICONTROL 게시 관리] 마법사로 이동할 수 없습니다. 특히 [!UICONTROL 게시] 옵션이 작동하지 않습니다(NPR-34099).
* iParsys(상속된 단락 시스템)의 위치는 [!UICONTROL 상속 취소] 또는 [!UICONTROL 상속 비활성화] 옵션(NPR-34097)을 선택 취소한 후 원래 기본 위치로 되돌려지지 않습니다.
* `RolloutConfigManagerFactoryImpl`이(가) 롤아웃 구성을 로드할 수 없는 경우 누락된 구성을 로드하지 않습니다. 캐시된 구성(NPR-34092)을 반환합니다.
* 텍스트 핵심 구성 요소의 경우 소스 HTML 편집 옵션을 사용한 후 `em` 태그의 클래스가 제거됩니다(NPR-34081).
* Experience Manager 6.3.3에서 Experience Manager 6.5.3으로 업그레이드한 후 롤아웃 프로세스가 훨씬 더 오래 걸리고 시간 초과 오류(NPR-34049)로 롤아웃되지 않습니다.
* `htmlwriter`은 특성 값을 다시 인코딩하지 않습니다. XF 마크업에 있는 마크업은 디코딩된 속성 값(즉, `&#34` 대신 `"`)으로 내보내집니다. 내보낸 XF를 사용하는 Visual Experience Composer의 Target 측면에 문제가 발생합니다(NPR-34048).
* [!DNL Experience Manager Sites]에서 페이지를 이동할 때 기록을 향상시켜 이유 있는 버전 생성 실패를 캡처하십시오(NPR-34014).
* [!DNL Rich Text Editor]에서 모든 텍스트를 제거하면 단락 태그도 제거됩니다(NPR-33976).
* `siteadmin` 페이지(클래식 UI에서)를 열거나 새로 고치면 `New` 메뉴의 옵션이 비활성화됩니다(NPR-33949).

   ![클래식 UI에서 누락된 메뉴의 문제를 설명하는 스크린샷](assets/33949_missing_menu.png)

* [!DNL Content Fragment]은(는) `ContentFragmentUsePojo`에서 실패하므로 `TemplatedResource`으로 사용할 수 없습니다(NPR-33911).
* 동기 및 비동기 이동 작업은 동시 전송으로 인해 오류가 발생할 수 있습니다. 페이지 이동 작업은 비동기 이동으로만 제한됩니다. 페이지가 동시에 이동하는 것을 방지합니다(NPR-33875).
* [!UICONTROL 작성 ] 인스턴스에서 게시 인스턴스로 컨텐츠를 복제하는 게시 관리 작업에 오류가 발생하고 JavaScript 오류를 생성합니다(NPR-33872).
* 버전을 만들기 위해 여러 페이지 또는 자산을 선택한 경우, 새 버전은 마지막으로 선택한 페이지 또는 자산에 대해서만 만들어집니다(NPR-33866).
* Live Copy가 있는 블루프린트 페이지를 다른 폴더로 이동합니다. 원래 폴더로 이동할 때 이동 작업이 오류 없이 실패합니다(NPR-33864).
* 이동 작업을 사용하여 [!DNL Sites] 콘솔에서 웹 페이지의 이름을 변경하는 경우 마법사의 마지막 단계에서 2개의 겹쳐진 대화 상자가 표시됩니다(NPR-33831).

   ![중복 이동 대화 상자의 NPR-33831 문제를 설명하는 스크린샷](assets/33831_rename_dialog.png)

* 복사본의 [!DNL Adobe Campaign]에 대한 `cq:acLinks` 및 `cq:acUUID` 속성은 복사 및 붙여넣기 작업 중에 제거됩니다(NPR-33794).
* 분리된 상위 Live Copy의 하위 페이지에서 롤아웃을 시도하면 [!DNL Experience Manager]은(는) null 포인터 예외를 생성합니다(NPR-33676).
* 레이아웃 컨테이너를 페이지에 복사하여 다시 붙여넣을 때 레이아웃 컨테이너의 [!DNL RTE] 구성 요소가 표시되지 않습니다. [!DNL RTE] 구성 요소는 편집할 수 없지만 페이지 새로 고침 시 표시됩니다(NPR-33662).
* 서로 다른 중단점(중간 및 큼)에 대한 레이아웃 구성 요소의 크기를 조정할 때 레이아웃이 예상대로 작동하지 않습니다(NPR-33608).
* [!DNL RTE]의 인라인 편집 모드에서 이미지를 드래그하면 텍스트 구성 요소에 사용할 수 없습니다(NPR-33602).
* 페이지 이름과 동일한 이름으로 블루프린트 페이지에 구성 요소를 만들 수 있습니다. 롤아웃 시 구성 요소의 이름을 바꾸도록 `_msm_moved`이(가) 모두 전달됩니다. 구성 요소는 [!UICONTROL 단락 시스템](NPR-33535)의 끝으로 이동됩니다.
* offTime 또는 onTime이 많은 페이지 또는 자산에 설정되면 리소스를 많이 사용하므로 시작 및 종료 시 시스템이 지연됩니다(NPR-33482).
* `/content/experience-fragment`에 대한 CRUD 권한이 있는 사용자는 폴더를 삭제할 수 없습니다(NPR-33436).
* [!DNL Experience Fragments] 섹션의 상위 폴더에서 [!UICONTROL Adobe Target 내보내기 형식]에 대한 옵션으로 [!UICONTROL HTML &amp; JSON]을 선택할 수 있습니다. 이 상위 폴더의 하위 폴더에 대해 터치 가능 UI에 동일한 속성이 표시됩니다. 그러나 CRXDE에서는 `cq:adobeTargetExportFormat`에 대해 `html,json` 표시 대신 HTML만 표시합니다(NPR-33423).
* 페이지 별칭에서 게시 또는 게시 취소는 지원되지 않습니다. 그렇지 않은 경우 클레임이 표시되는 옵션을 제거합니다(NPR-33415).
* 특정 태그는 [!DNL Experience Manager]에서 한 위치에서 다른 위치로 이동할 수 있습니다. 이동 전후에 다른 페이지에 적용할 수도 있습니다. 페이지의 속성을 편집할 때 태그가 동일하더라도 편집할 수 있도록 태그가 표시되지 않습니다(NPR-33353).
* 여러 레이아웃 컨테이너가 포함된 템플릿에서 레이아웃 컨테이너를 삭제할 때 페이지 템플릿이 제대로 렌더링되지 않습니다(NPR-33347).
* 템플릿 편집기에서 `/content/` 아래에 1,000,000개 이상의 페이지에 사용되는 템플릿을 삭제하려고 합니다. 오류 메시지 없이 오류가 표시됩니다(NPR-33312).
* 앵커 포함 [!DNL Experience Manager] 페이지로 리디렉션은 URL 조각 또는 앵커 뒤에 쿼리 문자열을 제공하므로 작성자 인스턴스에서 작동하지 않습니다(NPR-34288).`PageRedirectServlets`
* `/content/campaign` 아래에 브랜드를 만들면 캠페인을 만들 수 없는 구조가 됩니다. [!UICONTROL 브랜드 ] 만들기 옵션은 크리에이티브 옵션이 없으므로  [!UICONTROL 오퍼 및 활동] 을 만들 수 없는 새로운 브랜드를   유지합니다(NPR-34113).
* 페이지의 [!DNL Live Copy]을(를) 일시 중단할 수 있으며 상속은 편집기 모드에서 보듯이 끊깁니다. 페이지 속성에서 상속을 나타내는 아이콘이 상속이 존재하며 끊기지 않았음을 잘못 나타냅니다(NPR-34017).
* 참조가 많은 페이지는 비동기적으로 이동할 수 없으며 이동 작업이 실패하는 경우가 있습니다(CQ-4297969).
* 작성하는 동안 URL에 `/` 문자가 있는 웹 페이지가 응답하지 않습니다. 작성하는 동안 구성 요소가 추가되면 CPU 사용이 증가하며 브라우저가 응답을 중지합니다(CQ-4295749).
* 찾아보기 모드에서 NVDA는 유형/크기 메뉴 옵션에서 선택한 값을 내레이팅하지 않습니다. 시각적 포커스가 선택한 요소에 없습니다. 화면 판독기를 사용하는 사용자는 검색 모드를 사용할 수 없습니다(CQ-4294993).
* 웹 페이지를 만들 때 사용자는 [!UICONTROL 컨텐트 페이지] 템플릿을 선택할 수 있습니다. [!UICONTROL 소셜 미디어] 탭에서 [!UICONTROL 기본 XF 변형]을 선택합니다. NVDA 검색 모드에서 경험 조각을 선택하려면 키보드 키(CQ-4292669)을 사용할 수 없습니다.
* handlebars 라이브러리를 더 안전한 v4.7.3(NPR-34484)로 업데이트했습니다.
* [!DNL Experience Manager Sites] 구성 요소의 다중 사이트 스크립팅 인스턴스(NPR-33925).
* 새 폴더를 만들 때 폴더 이름 필드는 저장된 사이트 간 스크립팅(GRANITE-30094)에 취약합니다.
* [!UICONTROL  시작] 페이지의 검색 결과와 경로 완료 템플릿은 사이트 간 스크립팅에 취약합니다(NPR-33719, NPR-33718).
* 비정형 노드에서 이진 속성을 만들면 이진 속성 대화 상자에서 크로스 사이트 스크립팅이 발생합니다(NPR-33717).
* CRX DE 인터페이스에서 [!UICONTROL 액세스 제어 테스트] 옵션을 사용할 때 크로스 사이트 스크립팅(NPR-33716).
* 사용자 입력은 클라이언트에 정보를 보낼 때 다양한 구성 요소에 대해 적절히 인코딩되지 않습니다(NPR-33695).
* Experience Manager 받은 편지함에 대한 달력 보기에서 사이트 간 스크립팅(NPR-33545).
* `childrenlist.html`으로 끝나는 URL은 404 응답 대신 HTML 페이지를 표시합니다. 이러한 URL은 사이트 간 스크립팅(NPR-33441)에 취약합니다.


### [!DNL Assets] {#assets-6560}

**Experience Manager Assets의 액세스 가능성이 개선되었습니다**

* 이제 사용자는 키보드 키를 사용하여 [!UICONTROL 참조] 자산 목록(NPR-34115)에 있는 대화형 사용자 인터페이스 옵션에 액세스하고 집중할 수 있습니다.

* 이제 화면 판독기가 검색 페이지에 예측자의 의도한 동작을 발표합니다(NPR-34104).

* 이제 화면 판독기 사용자를 더 잘 이해할 수 있도록 검색 페이지 및 검색 결과 페이지에 더 많은 정보가 포함된 제목이 있습니다(NPR-34093).

* 이제 화면 판독기가 자산 [!UICONTROL 속성] 페이지의 [!UICONTROL 기본] 탭에서 선택한 태그를 삭제하는 옵션을 발표합니다(NPR-33972).

* 목록 보기의 각 행에 있는 요소는 이제 화면 판독기로 동일한 행의 요소로 발표됩니다(NPR-33932).

* 이제 `Tab` 키를 사용하여 탐색할 때 사용자의 초점이 버전 미리 보기의 닫기 옵션으로 이동합니다(NPR-33863).

* 이제 Omnisearch가 닫힌 후 사용자 포커스가 검색 아이콘으로 이동합니다(NPR-33705).

* 이제 키보드 키를 사용하여 탐색할 때 향상된 대비 기능을 갖춘 실행 가능한 유저 인터페이스 옵션이 보다 눈에 띄는 시각적 포커스를 갖게 되었습니다. 키보드 사용자는 초점을 맞춘 영역을 식별할 수 있습니다(NPR-33542).

* 키보드를 사용한 드래그 기능이 이제 화면 판독기의 검색 모드에서 [!UICONTROL 메타데이터 스키마 편집기]에서 작동합니다(CQ-4296326).

* 링크 공유 대화 상자에서 찾아보기 모드에서 탐색할 때 화면 판독기가

   * 대화 상자가 로드되는 즉시 테이블 정보를 분류하지 않습니다.

   * 나열된 모든 자동 제안 항목으로 이동할 수 있습니다.

   * [!UICONTROL 이메일 주소/검색 추가](CQ-4294232)에 대해 표시되는 자동 제안 내레이션이 표시됩니다.

* 카드 보기에서 빠른 작업 아이콘을 제거하기 위해 `Esc` 키를 사용해도 더 이상 마지막 초점이 맞춰진 항목(CQ-4293554)에서 키보드 포커스를 제거하지 않습니다.

* 사용자 인터페이스에 대한 대화형 옵션의 경우 화면 판독기는 이제 아이콘의 문자 이름(CQ-4272943)이 아니라 사용자가 사용할 목적을 알려줍니다.

* 키보드 포커스가 이제 [!UICONTROL 플라이아웃], [!UICONTROL InlineZoom], [!UICONTROL Shopperable_Banner], [!UICONTROL Zoom_dark], [!UICONTROL Zoom_light], [!UICONTROL Zoom_dark_dark 자산 세부 정보 [!UICONTROL Viewers](CQ-4290605)의 ]Viewers[!DNL Dynamic Media]에서 키보드 탭 키를 사용하여 탐색할 때 a11/> 및 [!UICONTROL ZoomVertical_light] 옵션.

* [!UICONTROL 자산 ] 속성 페이지의 저장 및   닫기 옵션은 이제 키보드 키를 사용하여 액세스할 수 있습니다(NPR-34107).

* 로그인 페이지의 잘못된 사용자 이름과 암호 조합으로 인한 오류 메시지는 이제 오류가 발생할 때마다 화면 판독기에 의해 표시됩니다(NPR-33722).

* [!DNL Experience Manager] 머리글 섹션에서 찾아보기 모드로 탐색할 때 화면 판독기가 이제

   * [!UICONTROL Type to search]의 제안을 Omnisearch에서 자동으로 편집합니다.

   * [!UICONTROL 솔루션], [!UICONTROL 도움말], [!UICONTROL 받은 편지함] 및 [!UICONTROL 사용자] 옵션에 대해 확장되거나 축소된 상태.

   * 사용자가 [!UICONTROL 도움말] 옵션 아래의 [!UICONTROL 도움말 검색] 필드에서 검색 문자열을 입력할 때 표시되는 [!UICONTROL 도움말] 상태 메시지.

   ![헤더의 도움말 메뉴](assets/Help_aem_header.png)

   *그림: [!UICONTROL 도움말 ] 메뉴를   검색합니다.*

   * 잘못된 값을 [!UICONTROL 가장 대상:] 필드([!UICONTROL 사용자] 옵션 아래) 필드에 입력하고 포커스가 텍스트 필드로 올바르게 이동하는 경우 오류 메시지(NPR-33804).

   ![헤더의 사용자 메뉴](assets/User_aem_header.png)

   *그림: [!UICONTROL 헤더] 의 사용자   메뉴의 asfield로 가장합니다.*

* 이제 사용자는 다음 내의 키보드를 사용하여 포커스를 변경할 수 있습니다.

   * [!UICONTROL [링크 공유] 대화 ] 상자에서  [!UICONTROL 이메일 주소 필드를 검색/] 추가합니다.

   * [!UICONTROL 폴더 ] 속성 [!UICONTROL 의 권한 탭에서 ] 폐쇄된 사용자 그룹  의 사용자 또 [!UICONTROL 는 그룹 필드 추가] (NPR-34452).

**Experience Manager Assets에서 해결된 문제**

[!DNL Adobe Experience Manager] 6.5.6.0은 다음 문제에 대한 수정 사항을  [!DNL Assets] 제공합니다.

* 자산의 타임라인에서 선택한 주석은 강조 표시되지 않습니다(CQ-4302422).

* [!DNL Adobe InDesign] 템플릿을 사용하여 만든 마케팅 자료 자산(예: 브로셔, 전단지 및 명함)의 미리 보기에는 행 분리 및 단락 나누기(NPR-34268)가 표시되지 않습니다.

* 텍스트 추출 및 업로드된 PDF 파일에 대한 전체 텍스트 검색이 작동하지 않습니다(NPR-34164). 이 문제를 해결하려면 서비스 팩 6을 설치한 후 [!DNL sAdobe Experience Manager] 배포를 다시 시작합니다.

* 다중 페이지 자산의 타임라인에는 특정 하위 자산과 관련된 주석을 표시하지 않고 [타임라인] 보기에서 자산을 탐색할 때 모든 하위 자산에 적용된 주석이 표시됩니다(NPR-34100).

* 폴더에 JavaScript, CSS 또는 JSON 파일 형식의 리소스가 포함되어 있는 경우(NPR-34090) 자산 폴더가 [!UICONTROL 발행물 관리] 옵션을 사용하여 게시되지 않습니다.

* Omnisearch에서 적용된 태그 또는 필터를 선택 또는 제거하면 검색 시간이 늘어날 검색 쿼리가 여러 번 실행됩니다(NPR-34078).

* 워크플로우(폴더의 자산)가 진행 중이거나 보류 중인 경우 워크플로우가 완료되거나 종료될 때까지 페이지가 다시 로드됩니다. 따라서 작성자는 아래로 스크롤해야 하는 폴더의 해당 에셋에 대해 작업할 수 없습니다(NPR-33986).

* 사용자가 게시된 자산을 새 위치로 이동하면 [!UICONTROL 다시 게시] 옵션이 선택 해제되어 있어도 자산이 다시 게시됩니다. 이로 인해 게시 인스턴스에 고립된 많은 자산이 거짓말을 하게 됩니다. 그러나 기본적으로 게시된 자산에 대한 이동 작업이 자동으로 게시 취소됩니다.자산을 이동할 때 작성자가 [!UICONTROL 다시 게시] 옵션을 선택하면 이 자산이 다시 게시됩니다(NPR-33934).

* 컬렉션의 자산에 대한 [!UICONTROL 자산 이동] 페이지는 [!UICONTROL 조정/ 다시 게시] 옵션과 같은 모든 HTML 콘텐츠를 로드하지 않습니다. 따라서 사용자는 이동 작업을 완료할 수 없습니다(NPR-33860).

* 자산을 이동하고 이동한 자산의 이름과 제목에 특수 문자를 추가하면 자산의 새 위치에 추가 폴더(같은 이름의)가 만들어집니다(NPR-33826).

* [!UICONTROL 다운로드 ] 대화 상자에서   이메일 옵션  을 선택하면 에셋의 다운로드 단추가 비활성화됩니다(NPR-33730).

* 벌크 메타데이터 편집(NPR-33723)과 같은 자산에 대한 벌크 작업을 수행할 때 &#39;Request-URI too long&#39; 오류가 관찰됩니다.

* JavaScript 오류가 발견되었으며 업로드된 JSON 파일에 값(NPR-3371)에 공간 또는 특수 문자가 있는 경우 [!UICONTROL 폴더 메타데이터 스키마 양식 편집기에서 [!UICONTROL JSON 경로를 통해 추가] 기능에 의해 [!UICONTROL 드롭다운] 필드에 생성된 선택 항목을 선택하거나 삭제할 수 없습니다. 2).]

* 에셋이 [!DNL desktop app] 또는 [!DNL Adobe Asset Link]에서 [!UICONTROL 열기] 옵션을 사용하여 업데이트되고 다시 [!DNL Adobe Experience Manager](CQ-4296279)에 동기화되면 에셋의 정적 변환이 업데이트되지 않습니다.

* 열 보기에서 자산 집합에 대한 이동 작업은 해당 자산에 대해 [!UICONTROL 필터] 옵션을 사용하기 전에 선택한 자산도 이동합니다. [!UICONTROL 필터] 옵션을 사용하면 이전 선택 영역이 선택 취소됩니다(NPR-34018).

* 백슬래시는 이름에 특수 문자가 있는 자산 검색 제안에서 특수 문자 앞에 추가됩니다(NPR-33834).

* [!UICONTROL 폴더 메타데이터 스키마 양식]에서 드롭다운에 대한 규칙을 만들 때 사용자는 [!UICONTROL 필드 선택 항목] 열(CQ-4297530)에서 값을 선택할 수 없습니다.

* [!DNL Experience Manager] 6.5 서비스 팩 5 또는 이전 버전을 [!DNL Experience Manager] 6.5에 설치할 때 에셋 사용자 지정 워크플로우 모델의 런타임 복사본이 삭제됩니다(NPR-34532). `/var/workflow/models/dam` 런타임 복사본을 검색하려면 HTTP API를 사용하여 워크플로우 모델의 디자인 타임 사본을 런타임 복사본과 동기화합니다.
   `<designModelPath>/jcr:content.generate.json`.

**Dynamic Media에서 해결된 문제**

* 사용자가 비디오 프로필을 만든 후 편집에서 인코딩 설정을 정의하면 고급 자르기 설정이 비디오 프로필에서 제거됩니다(CQ-4299177).

* 사용자가 자산 세부 사항 페이지에서 사이드 레일 옵션(예: [!UICONTROL 개요], [!UICONTROL 타임라인], [!UICONTROL 뷰어]) 간을 전환하면 페이지 로드 시 에셋이 깜박입니다(NPR-34235).

* 재처리 작업에서 다음 문제가 관찰됩니다.

   * 재처리 작업에 의해 반환된 작업 핸들에 작업 ID가 없습니다.

   * 비디오 로그 파일 이름만 재처리하며 전체 경로가 아닙니다.

   * 재처리 작업에는 자산 유형을 정적으로 설정하는 옵션이 없습니다.

   * `ExcludeFromAVS` 옵션이 제공되지 않습니다(CQ-4298401).

* 이미지 프로필을 여러 종횡비(예: 11)가 있는 폴더에 추가할 때 스마트 자르기 기능이 오류로 인해 실패합니다(NPR-34082).

* DAM 자산 업데이트 워크플로우는 사용자가 Dynamic Media Scene7(CQ-4299727)으로 구성된 [!UICONTROL 도구]의 [!UICONTROL Workflow] 탭 내에서 [!UICONTROL 워크플로우 아카이브] 페이지로 스크롤할 때 실행됩니다.[!DNL Adobe Experience Manager]

* [!UICONTROL 뷰어 사전 설정 편집기]의 [!UICONTROL 비헤이비어] 탭에 있는 심볼이 지역화되지 않았습니다(CQ-4299026).

* 뷰어가 응답형 모드인 경우 기본 보기에는 뷰어에 맞지 않는 잘못된 레이아웃으로 이미지가 표시됩니다(CQ-4298293).

* [!UICONTROL Adobe Experience Manager]의 이미지 사전 설정에 대한 변경 사항은 Scene7 Publishing System(CQ-4299713)에 동기화되지 않습니다.

### [!DNL Commerce] {#commerce-6560}

* 자산을 이동할 때 제품에서 에셋에 대한 링크는 리팩토링되지 않습니다(NPR-34098).

### 플랫폼 {#platform-6560}

* 업그레이드된 Experience Manager 인스턴스에서 진단 도구를 사용하여 로그를 다운로드할 수 없습니다(NPR-34336).
* `cq-wcm-api` 기본 패키지의 특정 버전에 대한 종속성으로 인해 업그레이드에 실패했습니다(CQ-4300520).
* 기본 에이전트(게시) 구성에 대한 **[!UICONTROL 연결 시간 초과]** 및 **[!UICONTROL 소켓 시간 초과]** 설정에 대한 기본값이 지정되지 않았습니다(NPR-33707).
* `/etc/map.publish` 아래의 매핑 구성에 대한 업데이트는 사이트 페이지에 반영되지 않습니다(NPR-34015).
* [API 참조 설명서](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html) 는 패키지에 대한  `com.day.cq.tagging` 설명서를 포함하지 않습니다(CQ-4295864).

### 사용자 인터페이스 {#ui-6560}

* 브라우저 오프로드 인터페이스에 일부 작업 항목이 표시되지 않습니다(NPR-34308).
* [구성 브라우저](/help/sites-administering/configurations.md) 인터페이스에 모든 구성이 표시되지 않습니다(NPR-33644).
* 가장 가장할 사용자를 검색할 때 `Esc` 키를 누르면 사용자 목록 대신 **[!UICONTROL 사용자]** 대화 상자가 닫힙니다(NPR-34084).

### 통합 {#integrations-6560}

* 이름이 긴 활동은 [!DNL Adobe Target](NPR-34254)과 동기화되지 않습니다.

* 새 Adobe 시작 구성을 만들 때 속성을 선택하면 다음 오류 메시지가 표시됩니다(NPR-33947).

   ```javascript
   GET http://hostname:Port/libs/cq/dtm-reactor/content/configurations/createcloudconfigwizard/jcr:content/body/items/form/items/wizard/items/general/items/fixedcolumns/items/container/items/general/items/property/data.html?query=&start=0&end=25&imsConfigurationId=Adobe%20Launch&companyId=&_charset_=utf-8 400 (Bad Request)
   ```

### 번역 프로젝트 {#translation-6560}

* 사용자의 `authorizableID`에 특수 문자(NPR-33828)가 포함된 경우 번역 프로젝트가 생성되지 않습니다.

### 슬링 {#sling-6560}

* 상태 확인 및 패턴 탐지기 기능이 겹칩니다. 그 결과, Heath 검사가 제품에서 제거됩니다(NPR-33928).

### WCM {#wcm-6560}

* 기본 구성 요소 - 페이지에 기본 이미지 구성 요소를 추가하고 이미지를 참조하는 경우 `Undo` 작업이 작동하지 않습니다(NPR-34516).

* 페이지 이동 작업을 사용할 수 없습니다(CQ-4303028).

### [!DNL Communities] {#communities-6560}

* 소셜 미디어에 게시물을 공유하면 오래된 옵션인 Google+(NPR-33877)가 표시됩니다.

* 커뮤니티 구성원이 그룹 템플릿 또는 기타 그룹 기능 설정을 수정할 수 없습니다(NPR-33530).

* 이미지의 하이퍼링크 태그가 포럼 게시물에서 제대로 생성되지 않습니다(NPR-33464).

* 접근성 오류는 커뮤니티 할당 기능(NPR-33442)에서 식별됩니다.

* 관리 콘솔을 통해 추가된 커뮤니티 그룹의 기존 사용자는 커뮤니티 그룹 콘솔의 수정 사항에 대한 사용자 목록에서 제거됩니다(NPR-34315).

* `TagFilterServlet`은 잠재적으로 민감한 데이터를 노출합니다(NPR-33868).

<!--
* Tag filters are vulnerable to sensitive information disclosure (NPR-33868).
-->

### [!DNL Forms] {#forms-6560}

>[!NOTE]
>
>[!DNL Experience Manager] 서비스 팩에는 [!DNL Forms] 수정 사항이 포함되어 있지 않습니다. 이러한 수정 사항은 별도의 [!DNL Forms] 추가 기능 패키지를 사용하여 전달됩니다. 또한, JEE의 [!DNL Experience Manager Forms]에 대한 수정 사항이 포함된 누적 설치 프로그램이 릴리스됩니다. 자세한 내용은 [AEM Forms 추가 기능 설치](#install-aem-forms-add-on-package) 및 [AEM Forms JEE 설치](#install-aem-forms-jee-installer)를 참조하십시오.

[!DNL Experience Manager Forms] 6.5.6.0 Add-on 패키지를 설치한 후:

* [!DNL Experience Manager Forms] 인스턴스를 중지합니다.

* `crx-repository\launchpad\ext` 디렉토리에서 `bcpkix-1.51`, `bcmail-1.51` 및 `bcprov-1.51` JAR 파일을 삭제합니다.

* `sling.properties` 파일에서 ` sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider` 속성을 삭제합니다.

* [!DNL Experience Manager Forms] 인스턴스를 다시 시작합니다.

**적응형 양식**

* 응용 양식 조각이 누락된 경우 응용 양식이 렌더링되지 않습니다(NPR-34302).

* 적응형 양식 필드에 대한 도움말 내용 설명에 단락 HTML 태그가 표시됩니다(NPR-34116).

* **[!UICONTROL 서버에서 재유효성 검사]** 속성을 선택하면 응용 양식이 제출되지 않습니다(NPR-33876).

* **[!UICONTROL REST 끝점에 제출]** 제출 작업은 응용 양식에 대해 작동하지 않습니다(CQ-4299044).

* 접근성:필수 필드에 대한 첨부를 업로드하지 않고 적응형 양식을 제출하려고 하면 초점은 자동으로 첨부 파일 필드로 이동되지 않습니다(CQ-4298065).

* 적응형 양식의 표에 행을 추가하면 **[!UICONTROL 맨 위에 추가]** 및 **[!UICONTROL 맨 아래에 추가]** 옵션이 적절한 결과를 표시하지 않습니다(CQ-4297511).

* [!UICONTROL Value Commit] 스크립트가 제대로 트리거되지 않아 데이터가 적응형 양식으로 손실됩니다(CQ-4296874).

* 지역화된 적응형 양식에 대해 날짜 선택기가 제대로 작동하지 않습니다(NPR-34333).

* 파일 이름에 밑줄이나 공백이 있으면 응용 양식에 파일을 첨부할 수 없습니다(CQ-4301001).

* 중첩된 반복 가능한 패널이 상위 패널보다 더 많은 항목이 있는 경우 이러한 중첩 반복 가능한 패널의 모든 항목이 프리필되지 않습니다(NPR-33666).

* 적응형 양식에는 열려 있는 리소스 해상도가 있습니다. 이는 제출 실패로 이어집니다. 문제가 간헐적으로 발생합니다(CQ-4299407).

* 처음 필드 구성을 열면 속성 아이콘이 표시되지 않습니다(CQ-4296284).

* 사용자는 적응형 양식을 제출할 때 `afPath`, `afSubmissionTime` 및 `signers` 등의 제출 메타데이터를 편집할 수 있습니다. 이 문제를 해결하기 위해 클라이언트측의 양식 제출 데이터에서 메타데이터 값이 제거됩니다. 사용자는 `FormSubmitInfo` 개체를 사용하여 서버에서 이러한 값을 검색할 수 있습니다(NPR-33654).

* 사용자 입력은 클라이언트에 정보를 보낼 때 [!DNL Forms] 구성 요소에 대해 적절히 인코딩되지 않습니다(NPR-33611).

**워크플로우**

* 워크플로우 승인자가 첨부 파일을 업로드하면 첨부 파일의 이름이 `undefined`(NPR-33699)로 바뀝니다.

* [!DNL Experience Manager] 워크플로우 제거 작업에 실패하고 다음 오류 메시지가 표시됩니다(NPR-33575).

   `java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory`

* [!DNL Experience Manager Forms] 양식을 제출한 후 응답을  [!DNL Windows] 중단할 수 있습니다(NPR-34409).

* AEM 서비스 팩을 설치할 때 항목의 **To Do** 목록이 링크로 표시되지 않습니다. **To Do** 항목에 대한 텍스트에는 HTML 태그가 포함됩니다(NPR-34317).

**대화형 통신**

* 반복 가능한 중첩된 구성 요소가 있는 텍스트 문서 조각을 포함하면 대화형 통신을 저장할 수 없습니다(NPR-34095).

**서신 관리**

* 데이터 사전 값을 포함하는 텍스트 문서 조각을 수정하면 에이전트 UI가 응답을 중지합니다(NPR-33930).

* [!DNL Microsoft Word] 문서의 컨텐츠를 문자로 텍스트 문서 조각으로 복사하여 붙여넣으면 서식 문제가 발생합니다(NPR-33536).

**문서 서비스**

* 출력 및 Forms 서비스를 사용하여 XDP 파일에서 PDF 파일을 생성할 때 텍스트가 누락되거나 겹치게 됩니다(NPR-34237, CQ-4299331).

* HTML 파일을 PDF로 변환할 때 `MaxReuseCount` 속성을 구성할 수 없습니다(NPR-33470).

* Reader 확장 대화형 기능이 포함된 PDF 파일을 다운로드할 때 [!DNL Adobe Reader](NPR-33729)을 사용하여 PDF 파일에 첨부 파일을 추가할 수 없습니다.

**문서 보안**

* [!DNL Experience Manager] 서비스 팩(NPR-34310)을 설치한 후 PDF 파일에서 HSM 기반 인증서로 서명 작업을 실행할 수 없습니다.

**디자이너**

* Designer 버전 6.5.x에서 XForms를 열 수 없습니다(CQ-4295322).

* Designer를 열면 시작 화면에 잘못된 연도(CQ-4295289)이 표시됩니다.

* 서버에 [!DNL Acrobat DC]을(를) 설치하면 **[!UICONTROL 양식 배포]** 옵션이 비활성(CQ-4296304)입니다.

보안 업데이트에 대한 자세한 내용은 [Experience Manager 보안 게시판 페이지](https://helpx.adobe.com/security/products/experience-manager.html)를 참조하십시오.

## [!DNL Adobe Experience Manager] 6.5.5.0  {#experience-manager-6550}

Adobe Experience Manager 6.5.5.0은 **2019년 4월** 6.5 릴리스의 공식 출시 이후 릴리스된 새로운 기능, 주요 고객이 요청한 향상된 기능 및 성능, 안정성, 보안 개선 사항이 포함된 중요한 업데이트입니다. Adobe Experience Manager 6.5 맨 위에 설치할 수 있습니다.

[!DNL Adobe Experience Manager] 6.5.5.0에 도입된 몇 가지 주요 기능 및 개선 사항은 다음과 같습니다.

* CRXDE Lite에 대한 익명의 액세스는 허용되지 않습니다. 대신 사용자에게 로그인 화면이 표시됩니다. [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)으로 개발을 참조하십시오.

* [!DNL Adobe Experience Manager] 받은 편지함에 표시되는 열 이름을 사용자 지정합니다.

* 페이지 편집기, 코어 구성 요소, RTE 및 관리자 인터페이스와 같은 Experience Manager WCM(웹 컨텐츠 관리)의 다양한 영역에서 액세스 가능성이 개선되었습니다.

* 초안을 [!DNL Interactive Communication](으)로 저장합니다.

* JEE에서 Experience Manager Forms용 [!DNL Oracle WebLogic 12] 지원.

* [!DNL Adobe Experience Manager Assets] 사용자 인터페이스 흐름의 예외 처리가 개선되었습니다.

* Dynamic Media Scene7에 대한 게시 URL을 가져오려면 새로운 방법 `getRemoteAssetPublishURL`이 `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` 인터페이스에 추가됩니다.

* WCAG(Web Content Accessibility Guidelines)를 준수하여 [ ](#assets-6550)액세스 가능성 개선[!DNL Adobe Experience Manager Assets].

* Adobe Experience Manager와 패키지 공유 통합이 제거되었습니다.

* 내장된 저장소(Apache Jackrabbit Oak)가 버전 1.22.3으로 업데이트되었습니다.

Experience Manager 6.5 서비스 팩 5에 소개된 전체 기능, 주요 특징 및 주요 기능 목록에 대해서는 [Adobe Experience Manager 6.5 서비스 팩 5의 새로운 기능](new-features-latest-service-pack.md)을 참조하십시오.

다음은 [!DNL Experience Manager] 6.5.5.0 릴리스에서 제공된 수정 사항 목록입니다.

### [!DNL Sites] {#sites-6550}

* Experience Manager Sites는 해당 별칭에서 페이지를 게시 또는 게시 취소하는 옵션을 제공합니다. 이 옵션이 작동하지 않습니다(NPR-33415).
* 여러 템플릿이 들어 있는 템플릿에서 레이아웃 컨테이너를 삭제하면 템플릿이 올바르게 렌더링되지 않습니다(NPR-33347).
* Experience Manager Sites 페이지가 여러 Live Copy가 있는 큰 컨텐츠 세트의 일부인 경우 페이지 버전 기록 미리 보기가 로드되지 않습니다(NPR-33311).
* 이동 명령을 사용하여 Experience Manager Sites 페이지의 이름을 변경하면 페이지 제목이 업데이트되지 않습니다(NPR-33264).
* 열 보기를 통해 페이지를 이동하면 열이 사라집니다(NPR-33216).
* 언어 복사본에 있는 로컬 구성 요소의 이름이 블루프린트에서 구성 요소의 이름과 동일하고, 구성 요소가 블루프린트에서 롤아웃되면 `_msm_moved` 용어가 로컬 구성 요소의 이름에 추가되지 않습니다(NPR-33208).
* 페이지 리디렉션 서블릿은 ResourceType이 `cq:Page`가 아닌 Sites URL에 .html을 추가합니다(NPR-33176).
* 하위 트리를 붙여넣을 때 해당 하위 페이지를 붙여넣을 것인지 여부를 결정하는 옵션이 없습니다(NPR-33149).
* 구성 요소의 라이브 사용량 결과 수는 49로 제한됩니다(NPR-33058).
* 스키마에 컨텐츠 조각을 기반으로 하고 필수 텍스트 영역 또는 경로 필드를 포함하는 경우 컨텐츠 조각이 저장되지 않습니다(NPR-33007).
* 기본 경험 구성요소 구성 요소를 사용하여 사용자 지정 구성 요소를 만들고 Experience Manager Sites 페이지에서 사용하면 Experience Manager에 사용자 지정 구성 요소에 대한 참조(사용량)를 표시하지 않습니다(NPR-32852).
* 참조 수가 많은 폴더의 이름을 바꾸면 해당 폴더에 대한 많은 참조가 업데이트되지 않습니다(NPR-32765).
* 소스 편집 옵션을 활성화하면 인라인 전체 화면 옵션에는 사용할 수 있지만 리치 텍스트 편집기의 편집 대화 상자와 전체 화면 옵션에는 누락된 상태로 남게 됩니다(NPR-32763).
* 다중 필드가 있고 블루프린트의 페이지 속성에 필수 필드(예: 드롭다운 또는 경로 필드)가 포함되어 있는 경우 이러한 다중 필드가 포함된 페이지가 롤아웃되면 Live Copy의 페이지 속성이 저장되지 않습니다(NPR-32751).
* 화면 판독기에서 제목 구조를 사용하여 페이지를 탐색할 수 없습니다. 또한 구성 요소 탭에 잘못된 레이블이 있습니다(NPR-32648).
* 페이지 매김이 시작되면 경험 조각 선택기가 일부 항목을 로드하지 않습니다(NPR-32605).
* Live Copy를 읽고, 수정하고, 만들고, 삭제할 수 있는 작성자 권한이 취소됩니다. 각 작성자는 블루프린트 내에서 페이지를 이동하기 위해 읽기 및 수정 권한을 명시적으로 제공해야 했습니다(NPR-32550).
* 컨텐츠 작성자가 Adobe Analytics와 통합된 페이지에 대해 시작을 만들지 못했습니다(NPR-32548).
* 사용자가 동기화와 함께 상속을 다시 시작하면 상위 페이지의 Live Copy는 블루프린트와 동기화되지 않고 잘못된 상태를 표시합니다(NPR-32500).
* Experience Manager Sites 편집기 페이지는 로드하는 데 15초 이상 걸립니다(NPR-32413).
* 특정 필드에는 상속 취소 옵션이 표시되지 않습니다(NPR-32362).
* 경험 조각 구성 요소의 경로를 선택하고 선택 대화 상자 열기 확인란을 선택하면 경로 브라우저에서 선택한 경로로 이동되지 않습니다(NPR-32308).
* Experience Manager 6.2에서 Experience Manager 6.5로 업그레이드하는 경우 정적 템플릿의 Parsys 구성 요소가 올바르게 표시되지 않습니다. Parsys 구성 요소의 높이가 0으로 설정되고 이 구성 요소 내에 있는 구성 요소가 표시되지 않습니다(NPR-33663).
* 사용자가 동일한 페이지에서 레이아웃 컨테이너를 복사하고 붙여넣으면 레이아웃 컨테이너의 구성 요소가 표시되지 않습니다(NPR-33648).
* Dispatcher 상태 확인은 로그 파일에 `Invalid cookie header` 경고 메시지를 표시합니다(NPR-33629).
* PreferencesServlet에 XSS가 반영됩니다(NPR-33438).
* 익명의 사용자는 CRXDE Lite 기능(GRANITE-27790)에 액세스할 수 있습니다.

### [!DNL Assets] {#assets-6550}

>[!IMPORTANT]
>
>[!DNL Experience Manager desktop app]의 Windows 사용자는 [!DNL Adobe Experience Manager 6.5.5.0] 인스턴스의 DAM 저장소에 액세스하려면 [데스크탑 앱 버전 2.0.3.2](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html#whats-new-added)로 업그레이드해야 합니다. 데스크톱 앱 버전을 사용하여 [!DNL Adobe Experience Manager] 6.5.5.0 인스턴스에서 DAM 저장소에 액세스할 때 문제가 발생할 수 2.0.2.

**Experience Manager Assets의 액세스 가능성이 개선되었습니다**

* 이제 자산의 [!UICONTROL 타임라인] 패널에서 [!UICONTROL 새 버전 만들기]에 있는 버전 설명 [!UICONTROL 만들기]에 대한 클릭 가능한 옵션과 [!UICONTROL 댓글] 목록에 키보드 포커스를 둘 수 있습니다(NPR-33424).

* 이제 키보드 키를 사용하여 [!UICONTROL 보기 설정] 대화 상자에서 자산에 대한 [!UICONTROL 보기 설정] 옵션에 도달하고 설정을 변경할 수 있습니다(NPR-33420).

* 이제 콤보 상자의 목록 상자 팝업(다른 페이지의 여러 필드)에 항목이 화면 판독기에서 알릴 수 있는 옵션 목록으로 표시됩니다(NPR-33516).

* 이제 정렬 가능한 머리글의 정렬 기능(목록 보기, [!UICONTROL 타임라인] 보기 및 [!UICONTROL 게시 관리] 페이지)을 화면 판독기에서 알려주고, 열 헤더의 정렬 컨트롤은 키보드를 사용하여 액세스할 수 있습니다(NPR-32979).

* 이제 클릭 가능한 요소(예: 주석 카드, 버전 업데이트, 콤보 상자, 메뉴의 펼침 아이콘)는 키보드를 사용하여 포커스를 지정하고 작업을 수행할 수 있습니다(NPR-33514).

* 이제 [!UICONTROL 인사이트 보기]의 인사이트 아이콘(사용량, 노출 횟수 및 클릭 수) 기능(또는 작업 목적)을 화면 판독기에서 올바르게 알려줍니다(NPR-33513).

* 이제 키보드를 사용하여 읽기 전용 양식 필드(예: 자산 [!UICONTROL 속성]의 [!UICONTROL 기본] 탭에서 비활성화된 필드)에 포커스를 지정할 수 있습니다.

* 다양한 입력 필드의 레이블은 이제 텍스트 입력 시 사라졌던 자리 표시자 레이블일 뿐만 아니라 영구 레이블(따라서 액세스 가능함)입니다(NPR-33475).

* 이제 다른 제목 수준(예: 페이지 제목 및 섹션 제목)은 화면 판독기 사용자에게 서로 수준의 제목으로 인식됩니다(NPR-33471).

* 이제 키보드를 사용하여 링크 및 옵션(자산 페이지의 헤더 및 확대/축소 옵션, 폴더 탐색)과 같은 대화형 사용자 인터페이스 요소에 액세스할 수 있습니다(NPR-33468, CQ-4271412).

* 이제 [!UICONTROL 게시 관리] 페이지의 [!UICONTROL 옵션], [!UICONTROL 범위] 및 [!UICONTROL 워크플로우] 진행 상태 표시기를 화면 판독기에서 탭 대신 진행 상태 표시기로 올바르게 읽을 수 있습니다(NPR-33416).

* 별점 등급 아이콘 색상(자산 [!UICONTROL 속성] 또는 카드 보기의 [!UICONTROL 고급] 탭에 있는 [!UICONTROL 등급] 섹션처럼)이 적절하게 대비되어 변경되므로 시력이 제한된 사용자와 색상을 인식하지 못하는 사용자가 볼 수 있습니다(NPR-33414).

* 이제 키보드 키(NPR-3397)를 사용하여 자산 세부 정보 페이지의 [!UICONTROL 댓글] 필드 옆에 있는 펼침 위쪽 화살표에 액세스할 수 있습니다(NPR-33397).

* 자산 [!UICONTROL 속성]의 [!UICONTROL 태그] 대화 상자 및 왼쪽 레일 탐색(자산 사용자 인터페이스)의 확장 및 축소 상태가 화면 판독기에 올바르게 표시됩니다(NPR-33396).

* 이제 [!DNL Adobe Experience Manager] Assets에서 검색한 모든 페이지의 제목이 고유합니다(NPR-33343).

* 이제 트리 구조를 탐색할 때 트리 보기 컨트롤의 여러 요소가 화면 판독기에 올바르게 표시됩니다(NPR-33304).

* 이제 키보드 키를 사용하여 자산 세부 사항 페이지의 [!UICONTROL 타임라인] 보기에서 다른 자산 버전에 액세스할 수 있습니다(NPR-33283).

* 이제 검색 기능을 사용할 때 Omnisearch 콤보 상자에 표시되는 검색 제안 이름이 화면 판독기에 표시됩니다(NPR-33280).

* [!UICONTROL 참조 레일]에서 클릭 가능한 요소 및 [!UICONTROL 링크로 이동] 기능이 이제 클릭 가능한 요소로 화면 판독기에 표시됩니다(NPR-33278).

* [!UICONTROL 링크 공유] 대화 상자가 열리면 이 대화 상자의 테이블 구조 정보(예: 행 1, 셀 1, 테이블)가 더 이상 화면 판독기에 표시되지 않습니다(NPR-33268).

* 이제 다양한 콤보 상자 요소(예: 자산 속성의 기본 탭에서 선택 대화 상자를 여는 옵션 및 경로 필드)의 목적이 화면 판독기에 올바르게 표시됩니다(NPR-33235).

* 목록 보기 테이블의 행을 선택할 수 있다는 정보는 키보드 포커스가 화면 판독기 사용자에게 있는 경우 전달됩니다. 포인터가 행을 가리키면 화면 판독기가 정보를 알려줍니다(NPR-33234).

* 이제 [!UICONTROL 속성]의 [!UICONTROL 기본] 탭에 있는 [!UICONTROL 태그] 필드 아래에서 선택한 각 태그를 제거하는 옵션([!UICONTROL x] 있음)에서 화면 판독기에 액세스할 수 있습니다(NPR-33206).

* 이제 화면 판독기 사용자와 정상 시력을 가진 키보드 사용자가 키보드를 사용하여 날짜 선택기에 포커스를 설정하고 작업을 수행할 수 있습니다(NPR-33200).

* 이제 목록 보기와 카드 보기 간에 전환하는 토글이 화면 판독기(보기 조정)에 기능을 올바르게 표시합니다(NPR-33069).

* 이제 왼쪽 레일의 메뉴에 액세스할 수 있습니다. 메뉴를 확장하는 기능과 목적은 화면 판독기에 적절히 표시됩니다(NPR-33068).

* 이제 시각 장애가 있는 화면 판독기 사용자가 목록 상자 및 기타 여러 사용자 인터페이스 요소에 액세스할 수 있으며, 이러한 요소에 대한 다음 정보가 화면 판독기에 표시됩니다(NPR-33040).

   * 양식을 제출하기 전에 요소에 사용자 입력이 필요한지 여부.
   * 요소를 편집할 수 없는지 여부.
   * 위젯을 선택했는지 여부.

* 이제 키보드를 사용하여 필터 사이드바를 여는 옵션에 액세스할 수 있습니다(NPR-32842, CQ-4273018).

* 이제 목록 보기의 열 헤더에 있는 확인란 컨트롤에 액세스할 수 있고, 이 컨트롤을 사용하는 목적이 화면 판독기에 표시됩니다(NPR-32722, NPR-33005).

* 달력 날짜 선택기의 시간(HH) 및 분(mm) 필드에 대한 레이블은 이제 자리 표시자 레이블 대신 영구 레이블로, 사용자가 이러한 필드에 텍스트를 입력할 때 사라지지 않습니다(NPR-32720).

* 이제 벨 아이콘을 클릭하면 표시되는 알림의 링크 텍스트가 화면 판독기 사용자에게 표시되면, 화면 판독기 사용자는 탭을 사용하여 각 링크에 액세스할 수 있습니다(NPR-32645).

* 이제 키보드를 사용하여 [!UICONTROL 인사이트 보기]에서 자산 카드의 [!UICONTROL 선택], [!UICONTROL 다운로드], [!UICONTROL 속성] 및 [!UICONTROL 추가 작업] 옵션에 액세스할 수 있습니다(NPR-32609).

* 화면 판독기에서 키보드를 사용하여 액세스할 때 시각적으로 숨겨진 내용(예: 검색 결과의 헤더 메뉴 막대 컨텐츠 등)이 더 이상 표시되지 않습니다(NPR-32606).

* 이제 일정 날짜 선택기에서 다음 달 및 이전 달로 이동할 컨트롤에 대한 레이블의 용도가 화면 판독기에 표시됩니다(NPR-32604).

* 이제 별 등급 아이콘은 키보드 키를 사용하여 포커스를 설정하고 작업을 수행할 수 있습니다(NPR-32513).

* 이제 탭(볼륨 슬라이더에 포커스 지정) 및 키보드의 화살표 키(볼륨 조정)를 통해 동영상 볼륨을 제어하는 기능에 액세스할 수 있습니다(NPR-32065).

* 파일 크기 필터의 하한([!UICONTROL 부터]) 및 상한([!UICONTROL 끝]) 입력 필드의 용도가 이제 시각 장애가 있는 화면 판독기 사용자에게 표시됩니다(NPR-32064).

* 이제 [!UICONTROL 작성 및 번역] 양식의 [!UICONTROL 언어] 메뉴에서 검색 모드로 화면 판독기에 액세스할 수 있습니다(CQ-4293906).

* 이제 다음과 같은 향상된 기능을 통해 [!UICONTROL 참조] 패널에 액세스할 수 있습니다(NPR-33261, CQ-4293798).

   * 검색 모드에서 화면 판독기 포커스는 더 이상 [!UICONTROL 사이트 참조], [!UICONTROL 자산 참조], [!UICONTROL 사본] 및 [!UICONTROL 참조 양식] 섹션에 숨겨진 여러 줄 편집 필드로 이동하지 않습니다.

   * 이제 화면 판독기에 [!UICONTROL 사이트 참조] 및 [!UICONTROL 언어 복사]의 역할이 표시됩니다 .

   * 검색 모드에서 화면 판독기의 포커스는 의미 있는 시퀀스에서 여러 요소로 이동합니다.

* 이제 키보드를 사용하여 [!UICONTROL 메타데이터 스키마 편집기] 페이지와 해당 요소에 액세스할 수 있으며, 이러한 페이지는 화면 판독기에 친숙합니다(CQ-4290962, CQ-4272953).

* 선택한 태그를 제거하는 `X` 기호의 용도는 이제 선택한 태그의 수와 함께 화면 판독기에서 알려줍니다(CQ-4273017).

* 화면 판독기를 사용하는 시각 장애 사용자에 대한 혼동을 방지하기 위해 이제 화면 판독기에서 장식 아이콘 및 이미지를 무시합니다(CQ-4272944).

**Experience Manager Assets에서 해결된 문제**

[!DNL Adobe Experience Manager] 6.5.5.0 Assets은 다음 문제에 대한 수정 사항을 제공합니다.

* 컬렉션의 에셋에 대한 [!UICONTROL 워크플로우 만들기] 대화 상자에서 [!UICONTROL 시작] 옵션이 비활성화되어 워크플로우가 트리거되지 않습니다(NPR-32471).

* 메타데이터 스키마에서 계단식 팝업을 사용할 때 동안 하위 드롭다운에서 아포스트로피가 포함된 드롭다운 옵션 선택 및 저장 시 선택한 아포스트로피 옵션은 자산 [!UICONTROL 속성]을 다시 열면 사라집니다(NPR-32649).

* [!UICONTROL 자산 통찰력 동기화 작업]이 다음 항목으로 이동하는 대신 잘못된 항목(Analytics 쪽)이 나타나면 중지되고 실패합니다(NPR-32674).

* 파노라마 뷰어의 모바일 브라우저에서 기본적으로 모션 센서가 비활성화되어 있으므로 자이로스코프가 작동하지 않습니다(CQ-4272937).

* 6.5.1에 6.5.3을 설치를 할 때 [!UICONTROL 연결된 자산 구성] 마법사가 404 오류로 작동하지 않습니다(NPR-32730).

* XMP 원본에 쓰기 절차 중에 모든 사용자 지정 네임스페이스 메타데이터 속성은 구성된 네임스페이스 접두어와 반대로 사용자 지정 네임스페이스 접두어를 ns2로 변경합니다(NPR-32748).

* 지연 로드는 트리거되지 않으며 알림 받은 편지함에서 작업을 검토하도록 선택할 때 100개의 자산만 표시됩니다(NPR-32750).

* `NullPointerException`은 새로 생성된 사용자 프로필에서 노드 기본 설정이 누락되어 관찰되었습니다(SAML/SSO). 이 오류로 인해 새로 로그인한 사용자가 [!DNL Adobe Experience Manager Stock] 통합을 사용할 수 없습니다(NPR-32777).

* 10,000개 이상의 자산이 포함된 스마트 컬렉션을 열 때 순회 경고가 로그에 관찰됩니다(NPR-32980).

* Dynamic Media Scene 7 런타임 모드에서 작동 중인 [!DNL Adobe Experience Manager]에서 자산을 한 폴더에서 다른 폴더로 이동할 때 자산 이름이 소문자로 변경됩니다(NPR-32995).

* 검색 결과에서 해당 속성으로 이동한 다음 검색 결과로 돌아가 삭제한 후 검색된 자산을 삭제할 수 없습니다(NPR-32998).

* [!UICONTROL 다음] 옵션은 [!UICONTROL 자산 이동] 인터페이스에서 대상 폴더를 선택할 때 비활성화됩니다(NPR-33356).

* [!UICONTROL 다음] 옵션이 상위 노드(단일 하위 폴더가 표시되는 경우)를 선택한 다음 하위 폴더를 선택할 때 활성화되지 않습니다(NPR-33275).

* AAL(Adobe Asset Link)에서 체크인 및 체크아웃 권한은 삭제 권한이 있는 사용자에게 읽기, 만들기 또는 수정과 같은 다른 권한이 부여되더라도 비활성화됩니다(NPR-33272).

* 스마트 자르기 렌디션은 자산 다운로드 대화 상자에서 사용할 수 없습니다(NPR-33167).

* 스마트 자르기 프로필이 있는 폴더에서 PDF에 대한 렌디션 레일을 열 때 로그에 예외가 관찰됩니다(CQ-4294201).

* Experience Manager의 Dynamic Media Scene7 실행 모드에서 기본적으로 [!UICONTROL Dynamic Media 동기화 모드]가 비활성화된 경우 이미지 사전 설정이 게시되지 않습니다(CQ-4294200).

* 벌크 업로드 중 자산 처리가 중단되고 워크플로우 인스턴스에 DAM 업데이트 자산의 중단 인스턴스가 표시됩니다(CQ-4293916).

* Experience Manager에서 Dynamic Media 구성 만들기가 작동하지만 사용자 인터페이스에서 저장을 선택하면 아무 일도 발생하지 않습니다(CQ-4292442).

* Safari/Mac에서 F4V 비디오 자산 미리 보기가 점진적 재생에서 작동하지 않습니다(CQ-4289844).

* 이름에 점 `.` 문자가 있는 상위 폴더의 자산을 스마트 자르기하면 추가 폴더가 만들어집니다(CQ-4289337).

* 썸네일이 깨지고 비디오가 복사되면 비디오 처리 배너가 표시되지 않습니다(CQ-4284125).

* 빈 카메라 보기가 있는 일부 모델의 경우 Firefox에서 차원 뷰어에 빈 썸네일이 잘못 표시됩니다(CQ-4283447).

* 6.5.5.0에서 해결된 성능 문제는 다음과 같습니다(CQ-4279206).

   * 큰 바이너리를 Dynamic Media 이미지 처리 서버로 업로드하는 데 시간이 너무 오래 걸립니다.

   * Dynamic Media Scene7 아키텍처로 인해 Experience Manager에서 축소판 생성 시간이 늘어납니다.

* 자산 수가 많은 고객의 경우 Dynamic Media Scene7 마이그레이션 문제가 발생합니다(CQ-4279206).

* `setVideo`를 사용하는 경우 비디오 360 뷰어의 레이아웃이 끊어지고 `video= modifier` 사용 시 비디오가 아래로 이동합니다(CQ-4263201).

* Experience Manager SDL 패키지를 설치하는 동안 오류 메시지가 표시됩니다(NPR-33175).

* Experience Manager의 SSRF 취약성(NPR-33435).

### 플랫폼 {#platform-6550}

* `sling:match` 맵 항목이 `/etc/maps`에 작성되지 않으면 [!DNL Sling] 필터가 호출되지 않습니다(NPR-33362).
* [!DNL Apache Lucene]의 세그먼트 문제로 인해 Experience Manager에서 충돌이 발생합니다(NPR-32988).
* Experience Manager uberjar 파일에 [!DNL Jackson] 코어 패키지가 없습니다(NPR-32848).
* CRXDE Lite는 노드의 `jcr:primaryType` 속성에 대한 읽기 권한이 없는 사용자에 대한 컨텐츠를 로드하지 않습니다(NPR-32611).
* [!DNL Granite] 유지 관리 작업 스케줄러가 Experience Manager 배포 시 너무 자주 다시 초기화됩니다(CQ-4294627).
* SQL 쿼리가 오래 실행되면(예: 7시간) Experience Manager가 응답하지 않습니다(NPR-33044).

### 사용자 인터페이스 {#ui-6550}

* 라디오 단추 선택이 다중 필드에서 지속되지 않습니다(NPR-33309).
* 목록 보기에서 레이지 로딩 제한이 작동하지 않습니다(NPR-33124).
* 일치하는 항목이 없으면 Omnisearch 결과 페이지에 메시지가 표시되지 않습니다(NPR-32974).
* Omnisearch 필터는 선택한 위치를 무시하고 `/content` 노드 아래에 모든 일치 항목을 반환합니다(NPR-32849).

### 통합 {#integrations-6550}

* Adobe Target 구성 요소가 있는 페이지가 게시되면 내부 캐시가 지워집니다(NPR-33162).
* Adobe Target과의 통합이 [!DNL Windows Internet Explorer] 11에서 작동하지 않습니다(NPR-33111).
* Adobe Target을 구성할 때 [!UICONTROL 회사] 및 [!UICONTROL 보고서 세트] 필드가 보고 소스 선택 시 표시되지 않습니다(NPR-32502).
* [!DNL Adobe I/O]을(를) 사용하여 [!DNL Experience Fragments]을 내보낼 때 소스 제품과 같은 메타데이터는 Adobe Target으로 내보내지지 않습니다(NPR-32159).
* 로컬 Experience Manager 관리 그룹의 승인된 IMS 사용자는 IMS 구성을 만들거나 수정할 수 없습니다(NPR-33045).
* Adobe Launch 구성 페이지에 모든 레코드가 표시되지 않습니다(NPR-33011).
* 컨텐츠 작성자 그룹의 사용자는 JavaScript 오류로 인해 Adobe Target 구성 요소의 속성을 편집할 수 없습니다(NPR-32996).
* JSON용 크로스 사이트 스크립팅(NPR-32744).

### 번역 프로젝트 {#translation-6550}

* 번역된 태그는 타사 번역 서비스에서 Experience Manager로 가져올 수 없습니다(NPR-33154).
* 번역 구성 페이지에는 변환에 사용한 것과 다른 잘못된 번역 공급자가 표시됩니다(NPR-32971).
* 기존 번역 프로젝트에 경험 조각 폴더를 추가하면 새 프로젝트가 만들어집니다(NPR-32843).
* 번역 작업 실행 시 로그에 `NullPointerException` 오류가 표시됩니다(NPR-32628).

### WCM {#wcm-6550}

* 페이지 편집기 - [!DNL Sites] 페이지 편집기에서 키보드 전용 사용자가 헤더에서 사용할 수 있는 모든 옵션을 통해 탭 포커스를 이동하는 대신 기본 컨텐츠로 건너뛸 수 없습니다(CQ-4293883).
* 페이지 편집기 - 잘 구성 요소를 사용하고 저장된 데이터를 포함하는 패널은 [!DNL Chrome] 및 [!DNL Firefox] 버전 업데이트로 인해 표시되지 않습니다(CQ-4292995).
* MSM - 페이지에서 구성 요소를 삭제해도 페이지의 게시된 버전에서 구성 요소가 삭제되지 않습니다(CQ-4292360).

### [!DNL Brand Portal] {#assets-brand-portal-6550}

* [!DNL Brand Portal]에서 게시된 메타데이터 스키마를 제거하면 오류가 발생합니다(CQ-4292063).
* 관리자가 Adobe 개발자 콘솔을 통해 Brand Portal로 [!DNL Experience Manager Assets] 6.5.4를 구성하는 경우 [!DNL Brand Portal] 사용자는 기여 폴더의 자산을 [!DNL Brand Portal]에서 [!DNL Experience Manager]에 게시할 수 없습니다(NPR-33046).
* 충돌을 일으키는 상위 폴더가 중복 복제됩니다(NPR-33001).

### [!DNL Communities] {#communities-6550}

* 빠른 편집 메뉴 옵션을 사용하여 중재 콘솔에서 카드를 삭제할 수 없습니다(NPR-33117).
* [!UICONTROL 활동 스트림] 페이지 액세스 시 오류가 발생합니다(NPR-33146).
* 작성자 인스턴스에서 삭제된 그룹은 일부 게시 인스턴스에서 제거되지 않습니다(NPR-33199).
* 작성자는 새 그룹을 만든 후 [!DNL Internet Explorer] 11의 [!UICONTROL 커뮤니티 그룹] 섹션으로 리디렉션되지 않습니다(NPR-33205).
* Experience Manager 받은 편지함의 메시지에 액세스해도 메시지의 상태가 읽음으로 변경되지 않습니다(NPR-32764).
* [!DNL Communities] 그룹을 편집하고 썸네일 이미지를 변경해도 그룹 썸네일 이미지가 업데이트되지 않습니다(NPR-32599). 
* 사용자가 커뮤니티의 다른 사용자에게 이메일을 보낼 수 없습니다(NPR-32598).
* 사용자가 페이지를 새로 고칠 때까지 제출된 블로그가 표시되지 않습니다(NPR-32391).
* UGC(사용자 생성 컨텐츠)의 알림 및 구독 버전을 만드는 동안 소스 페이지의 잘못된 ID가 저장됩니다(CQ-4279355, CQ-4289703).
* 사이트 간 스크립팅 문제(NPR-33203).

### 워크플로우 {#workflow-6550}

* 왼쪽 레일의 [!UICONTROL 타임라인] 옵션을 로드하는 데 예상보다 시간이 더 걸립니다(NPR-32851).
* Experience Manager 인스턴스를 다시 시작하면 컬렉션에 대한 검토 작업 이메일에 잘못된 페이로드 링크가 포함되어 있습니다(NPR-32774).

### [!DNL Forms] {#forms-6550}

>[!NOTE]
>
>Experience Manager 서비스 팩에는 [!DNL Forms] 수정 사항이 포함되어 있지 않습니다. 이러한 수정 사항은 별도의 Forms 추가 기능 패키지를 사용하여 전달됩니다. 또한, JEE의 AEM Forms에 대한 수정 사항이 포함된 누적 설치 프로그램이 릴리스됩니다. 자세한 내용은 [Experience Manager Forms 추가 기능 설치](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) 및 [JEE에 Experience Manager Forms 설치](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)를 참조하십시오.

* 통신 관리: 대상 영역의 자산 순서는 편지를 제출한 후 섞입니다(NPR-33359, NPR-33153).
* 적응형 양식: 사용자가 적응형 양식을 편집할 때 [!UICONTROL 페이지 정보] 메뉴에서 사용할 수 있는 [!UICONTROL 워크플로우 시작] 옵션이 작동하지 않습니다(NPR-33004).
* 적응형 양식: 사용자가 둘 이상의 첨부 파일이 있는 적응형 양식을 저장할 수 없습니다(NPR-32997).
* 적응형 양식: 적응형 양식의 패널 레이아웃을 변경하면 오류가 발생합니다(CQ-4293880).
* 적응형 양식: 적응형 양식 사전의 문자열에 새 줄이 있으면 사전에 `&#xa;` 문자가 추가됩니다(NPR-33266).
* 적응형 양식 액세스 가능성: 사용자가 적응형 양식을 HTML 양식으로 미리 볼 때 [!UICONTROL 스크리블 서명] 필드는 탭 포커스를 유지할 수 없습니다(NPR-33159).
* 적응형 양식 액세스 가능성: 적응형 양식 제출 시 표시되는 오류 메시지는 `aria-describedBy` 속성에 연결되지 않습니다(NPR-33071).
* 적응형 양식 액세스 가능성: 적응형 양식에 필수로 표시된 필드에는 ARIA 액세스 가능성 스키마의 필수 속성이 True로 설정되어 있지 않습니다(NPR-33070).
* PDFG 서비스: 사용자가 텍스트 파일을 PDF로 변환하면 일본어 문자가 올바르게 렌더링되지 않습니다(NPR-33238).
* PDFG 서비스: `CreatePDF` 작업에서 PDF 파일을 PDF OCR 형식으로 변환하지 못했습니다(NPR-32994).
* PDFG 서비스: [!DNL OpenOffice] 문서의 200번째 인스턴스에 대해 PDF를 변환할 수 없습니다(NPR-32766). 
* 백엔드 통합: 잘못된 비활성 상태로 인해 새로 고침 토큰이 만료되므로 양식 데이터 모델 요청이 실패합니다(NPR-33169).
* 디자이너: 화면 판독기는 XDP 파일에 정의된 사용자 지정 탭 순서 대신 기본 지리적 순서에 따라 탭 순서를 실행합니다(NPR-32160).
* 디자이너: 태그 지정 옵션이 활성화된 경우 생성된 PDF 출력에서 하위 양식 테두리가 사라집니다(NPR-32778).
* GuideSOMProviderServlet과 함께 XSS를 저장함(NPR-32700).

## Adobe Experience Manager 6.5.4.0 {#experience-manager-6540}

Adobe Experience Manager 6.5.4.0은 **2019년 4월** 6.5 릴리스의 공식 출시 이후 릴리스된 새로운 기능, 주요 고객이 요청한 향상된 기능 및 성능, 안정성, 보안 개선 사항이 포함된 중요한 업데이트입니다. Adobe Experience Manager 6.5 맨 위에 설치할 수 있습니다.

Adobe Experience Manager 6.5.4.0에서 도입된 주요 기능 및 개선 사항은 다음과 같습니다.

* 이제 Adobe Experience Manager 자산이 [!DNL Adobe I/O] 콘솔을 통해 브랜드 포털로 구성됩니다.

* 이제 Adobe Experience Manager Forms 워크플로우에서 새로운 [인쇄 가능한 출력 생성](../forms/using/aem-forms-workflow-step-reference.md) 단계를 사용할 수 있습니다.

* 적용형 양식 및 대화형 커뮤니케이션용 레이아웃 모드에 대한 [다중 열을 지원](../forms/using/resize-using-layout-mode.md)합니다.

* HTML5 양식의 [리치 텍스트](../forms/using/designing-form-template.md)를 지원합니다.

* Experience Manager Assets의 [액세스 가능성이 개선](new-features-latest-service-pack.md#accessibility-enhancements)되었습니다.

* 내장된 저장소(Apache Jackrabbit Oak)가 버전 1.10.8으로 업데이트되었습니다.

* 이제 선택적 컨텐츠 하위 트리를 `content/dam`에서 사용하는 대신 *Dynamic Media - Scene7 모드*&#x200B;로 동기화할 수 있습니다.

* 이제 SOAP 웹 서비스와 양식 데이터 모델 통합을 통해 요소에 대한 선택 그룹 또는 속성을 지원합니다.

* 이제 SOAP 입력 또는 출력 및 복잡한 데이터 구조가 Dynamic Group 대체를 지원합니다.

최신 서비스 팩에 포함된 기능 및 주요 특징 의 전체 목록을 살펴보려면 [Adobe Experience Manager 6.5 서비스 팩의 새로운 기능](new-features-latest-service-pack.md)을 참조하십시오.

### 사이트 {#sites-fixes}

* Adobe Experience Manager 사이트 페이지의 URL에 콜론(`:`) 또는 백분율 기호(`%`)가 포함되어 있으면 브라우저가 응답을 중단하고 CPU 사용 스파이크(NPR-32369, NPR-31918)가 발생합니다.

* Experience Manager Sites 페이지를 열어 편집하고 구성 요소를 복사하면 일부 자리 표시자에 대해 붙여넣기 작업을 사용할 수 없습니다(NPR-32317).

* 게시 관리 마법사가 열리면 코어 구성 요소에 연결된 경험 구성 요소가 게시된 참조 목록에 표시되지 않습니다(NPR-32233).

* Touch UI의 Live Copy 개요는 클래식 UI보다 렌더링하는 데 훨씬 시간이 오래 걸립니다(NPR-32149).

* 서버 시간과 컴퓨터 시간이 다른 시간대에 있는 경우 예약된 게시 시간은 Touch UI에 서버 시간을 표시하지만 클래식 UI에서는 시스템 시간이 표시됩니다(NPR-32077).

* Experience Manager Sites에서 URL에 접미사가 붙은 페이지를 열지 못합니다(NPR-32072).

* 사용자가 컨텐츠 조각을 편집하면 삭제된 컨텐츠 조각의 변형이 복원됩니다(NPR-32062).

* 사용자는 필수 필드에 정보를 제공하지 않고 컨텐츠 조각을 저장할 수 있습니다(NPR-31988).

* kernel.js와 ui.j는 사전 컴파일되거나 캐시되지 않습니다. 이로 인해 페이지 렌더링 시간이 추가로 발생합니다(NPR-31891).

* PageEventAuditListener가 활성화되어 있으면 커밋 큐의 길이가 늘어납니다. 벌크 게시, 탐색, 벌크 자산 이동과 같은 많은 작업 성능에 영향을 줍니다(NPR-31890).

* 경험 구성 요소를 드래그할 때 응답 시간이 오래 걸립니다(NPR-31878).

* 응답형 격자의 자리 표시자에서 구성 요소를 여기로 드래그하십시오. 옵션을 선택하면 GET 요청이 전송되고 HTTP 403 오류가 발생합니다(NPR-31845).

* 동일한 폴더 내에서 컨텐츠를 이동할 때 페이지 이동 옵션이 비활성화됩니다(NPR-31840).

* 편집 가능한 템플릿 구조 모드에서 레이아웃 컨테이너의 허용된 구성 요소 목록에 잘못된 결과가 표시됩니다. 디자인 대화 상자의 구성 요소만 레이아웃 컨테이너에 표시됩니다(NPR-31816).

* 페이지에 사용자에 대한 읽기 전용 권한이 있으면 속성 열기 옵션이 sites.html에 표시되지만 editor.html에는 표시되지 않습니다(NPR-31770).

* 사용자가 만들기 버튼을 클릭하면 페이지 옵션을 사용할 수 없습니다(NPR-31756).

* Adobe Campaign에서 OOTB(기본 제공) 디자인 가져오기 구성 요소가 포함된 캠페인을 동기화할 수 없습니다(NPR-31728).

* 글머리 기호 목록을 번호 매기기 목록으로 변경하려고 하면 목록의 처음 두 항목만 변경됩니다(NPR-31636).

* 페이지가 작성되지 않은 경우 하위 노드를 선택하면 선택 대화 상자에 여전히 초기 노드가 표시됩니다. 페이지가 작성된 경우 사용자가 찾아보기를 클릭하면 페이지가 작성된 노드 대신 루트 노드로 리디렉션됩니다(NPR-31618).

* 받은 편지함 사용자 지정 워크플로에서 구성 보기 대화 상자가 제대로 작동하지 않습니다(NPR-32503 및 NPR-32492).

* 받은 편지함을 사용하여 워크플로우 정보를 보는 동안 오류 메시지가 표시됩니다(CQ-4282168).

### 자산 {#assets-6540-enhancements}

* 자산 수집 페이지에서 워크플로우를 트리거하는 버튼이 비활성화됩니다(NPR-32471).

* Dynamic Media Scene7 구성을 사용하여 Experience Manager에서 자산을 폴더 간에 이동하는 동안 이름이 없는 폴더가 SPS(Scene7 Publishing System)에 생성됩니다(NPR-32440).

* 게시된 자산이 들어 있는 폴더로 모든 자산을 이동시키는 작업이 오류로 실패합니다(NPR-32366).

* ${extension}에서 자산의 렌디션이 생성되지 않습니다(NPR-32294).

* 버전 기록 URL은 자산 속성 페이지의 참조자 필드 아래에 표시됩니다(NPR-31889).

* DAM에서 다운로드한 ZIP 파일은 WinZip을 사용하여 열 수 없습니다(NPR-32293).

* 폴더 설정을 열어 폴더 제목이나 축소판 이미지를 변경한 다음 저장하면 폴더의 원래 권한이 업데이트됩니다(NPR-32292).

* 활성화가 예약된 달력 아이콘이 이후 날짜 및 시간에 대해 예약된 자산의 상태 열(DAM 자산 목록의 클래식 UI에 있음)에 표시되지 않습니다(NPR-32291).

* 코드 조각 템플릿을 사용하여 코드 조각을 만들면 코드 조각 만들기 프로세스 중에 컬렉션 검색 시 오류가 발생합니다(NPR-32290).

* 검색 필터에서 여러 태그를 선택하면 여러 검색 쿼리가 실행됩니다(NPR-32143).

* 파일 이름이 50자를 초과하는 자산을 업로드하면 Experience Manager Assets UI에 잘린 파일 이름이 표시됩니다(NPR-32054).

* Adobe Stock에서 확인란 트리의 수준 2 확인란을 선택한 경우 첫 번째와 두 번째 확인란의 선택을 취소하면 필터 패널의 모든 확인란이 지워집니다(NPR-31919).

* Omnisearch 패싯을 사용한 파일 및 폴더를 검색하면 예외가 발생합니다(NPR-31872).

* 종속성 규칙이 해당 메타데이터 스키마 양식에 설정된 경우 필수 필드를 선택하면 메타데이터 편집기의 필수 필드 선택을 위한 필드 강조 표시가 제거되지 않습니다(NPR-31834).

* 태그 계층 구조에서 리프 수준 태그의 전체 이름이 자산 속성 페이지에 표시되지 않습니다(NPR-31820).

* Safari 브라우저의 자산 속성 페이지에서 뒤로 명령을 사용하면 오류가 발생합니다(NPR-31753).

* Omnisearch를 통해 수행한 터치 UI 검색 결과 페이지가 자동으로 스크롤되어 사용자의 스크롤 위치가 손실됩니다(NPR-31307).

* Dynamic Media Scene7 실행 모드에서 실행되는 Experience Manager의 대상 컬렉션 및 표현물 추가 버튼 이외의 작업 버튼이 PDF 자산의 자산 세부 사항 페이지에 표시되지 않습니다(CQ-4286705).

* Scene7의 일괄 업로드 프로세스를 통해 자산을 처리하는 데 시간이 너무 오래 걸립니다(CQ-4286445).

* 사용자가 Dynamic Media 클라이언트의 설정 편집기에서 변경하지 않은 경우 저장 버튼이 원격 세트를 가져오지 않습니다(CQ-4285690).

* 지원되는 3D 모델을 Experience Manager로 수집할 때 3D 자산 축소판이 도움이 되지 않습니다(CQ-4283701).

* 스마트 자르기 비디오 뷰어 사전 설정이 처리되지 않은 상태로 사전 설정 이름과 함께 배너 텍스트에 두 번 표시됩니다(CQ-4283517).

* 3D Viewer에서 업로드된 3D 모델을 미리 보기했을 때 모델의 잘못된 컨테이너 높이가 자산 세부 정보 페이지에서 확인되었습니다(CQ-4283309).

* 캐러셀 편집기가 Experience Manager Dynamic Media 하이브리드 모드로 IE 11에서 열리지 않습니다(CQ-425590).

* Chrome 및 Safari 브라우저에서 다운로드 대화 상자에 있는 이메일 드롭다운에서 키보드 포커스가 멈춥니다(NPR-32067).

* Experience Manager에서 DM 클라우드 구성을 추가하는 동안 모든 컨텐츠 동기화 확인란이 기본적으로 활성화되지 않습니다(CQ -4288533).

### 기본 UI {#foundation-ui-6540}

* 필터 패널을 사용하여 자산을 검색하는 동안 마우스 컨트롤이 기존 필터 필드에 있지 않고 이전 필터 필드로 이동합니다(NPR-32538).

* 플랫폼 태그 지정: 태그 필드에 입력하여 태그를 검색하면 루트 경계 외부에 태그가 표시되고 태그 필드의 `rootPath` 속성이 유지되지 않습니다(NPR-31895).

* 플랫폼 UI: 텍스트 필드에 잘못된 경로가 추가되면 경로 브라우저가 멈춥니다(NPR-31884).

* 페이지 선택 시 알림이 고정 메뉴 뒤로 가려집니다(NPR-31628).

### 플랫폼 {#platform-sling-6540}

* (HTL) URL의 경로 섹션에서 밑줄이 콜론을 대체합니다(NPR-32231).

### 프로젝트 {#projects-6540}

* 사용자가 하위 폴더에 프로젝트를 만들 수 있는 권한이 있어도 만들기 버튼이 표시되지 않습니다(NPR-31832).

### 프로젝트 번역 {#projects-translation-6540}

* 번역 프로젝트를 만들 때 `Apache Sling JSP Script Handler`에서 지우기 공간 옵션이 활성화되어 있으면 UI가 중단됩니다(NPR-32154).

* 변환할 태그가 번역 프로젝트에 추가될 때 오류 로그에 UI 및 의 Null 포인트 예외 오류가 관찰됩니다(NPR-31896).

### 통합 {#integrations-6540}

* Launch 라이브러리 URL 생성은 Launch API의 `path` 및 `library_name` 값만 기반으로 하고 `library_path` 값을 기반으로 하지 않습니다(NPR-31550).

* LiveFyre 관련 항목을 처리하는 동안 오류 메시지가 표시됩니다(FYR-12420).

* ReportSuitesServlet이 SSRF에 취약합니다(NPR-32156).

### WCM 템플릿 편집기 {#wcm-template-editor-6540}

* 편집 가능한 템플릿 구조 모드에서 레이아웃 컨테이너의 허용된 구성 요소 목록에 링크 버튼 구성 요소가 표시되지 않습니다(CQ-4282099).

### WCM 페이지 편집기 {#wcm-page-editor-6540}

* 오버레이를 선택한 다음 응답형 격자 구성 요소를 여기로 드래그하십시오.를 선택하면 오류가 발생합니다(CQ-4283342).

### 캠페인 타깃팅 {#campaign-targeting-6540}

* Target 클라우드 구성이 실패하고 Mbox 가져오기 요청이 실패했다는 오류가 표시됩니다(CQ-4279880).

### 브랜드 포털 {#assets-brand-portal-6540}

* 브랜드 포털 사용자는 Experience Manager 6.5.4에서 [!DNL Adobe I/O]으로 업그레이드할 때 기여도 폴더 자산을 [!DNL Assets]에 게시할 수 없습니다(CQDOC-15655). Experience Manager 6.5.4를 즉시 수정하려면 [핫픽스를 다운로드](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041)하고 작성자 인스턴스에 설치하는 것이 좋습니다.

* 메타데이터 스키마 팝업 값은 자산 속성에 표시되지 않습니다(CQ-4283287).

* 자산 속성의 MIME 유형에 따라 메타데이터 하위 스키마에 탭이 표시되지 않습니다(CQ-4283288).

* 메타데이터 스키마 게시를 취소하면 백엔드에서 스키마가 제거되더라도 오류 메시지가 표시됩니다.

* 게시된 자산에 대한 미리 보기 이미지가 표시되지 않습니다(CQ-4285886).

* 사용자가 이름에 작은 따옴표가 포함된 자산을 게시하거나 게시를 취소할 수 없습니다(CQ-4272686).

* 여러 자산을 다운로드하는 동안 약관이 표시되지 않습니다(CQ-4281224).

* 사소한 보안 취약점이 해결되었습니다.

### 커뮤니티 {#communities-6540}

* 구성원 만들기 양식이 빈 페이지로 표시됩니다(NPR-31997).

* 사용자가 작성자 인스턴스에서 Analytics 보고서를 볼 수 없습니다(NPR-30913).

### Oak 색인 지정 및 쿼리 {#oak-indexing-6540}

* JPEG 이미지가 포함된 MS Word 및 MS Excel 문서를 Tika 구문 분석기로 구문 분석하면 구문 분석되지 않고 클래스를 찾을 수 없다는 오류가 표시됩니다(NPR-31952).

### 양식 {#forms-6540}

>[!NOTE]
>
>Experience Manager 서비스 팩에는 Experience Manager Forms에 대한 수정 사항이 포함되어 있지 않습니다. 이러한 수정 사항은 별도의 Forms 추가 기능 패키지를 사용하여 전달됩니다. 또한, JEE의 Adobe Experience Manager Forms에 대한 수정 사항이 포함된 누적 설치 프로그램이 릴리스됩니다. 자세한 내용은 [Experience Manager Forms 추가 기능 설치](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) 및 [JEE에 Experience Manager Forms 설치](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)를 참조하십시오.

* 서신 관리: 게시 처리 워크플로우에 제출하면 편지에 추가 문자가 표시됩니다(NPR-32626).

* 서신 관리: 게시 처리 워크플로우에 제출하면 편지에 드롭다운 자리 표시자가 텍스트 구성 요소로 표시됩니다(NPR-32539).

* 서신 관리: 편지 템플릿에 정의된 기본값이 미리 보기 모드에서 표시되지 않습니다(NPR-32511).

* 모바일 양식: HTML 버전에서 XDP 양식을 렌더링하는 동안 제출 버튼 크기가 확장되어 표시됩니다(NPR-32514).

* 문서 서비스: 서비스 팩 2를 적용한 후 편지 및 일부 기타 페이지의 URL에 액세스하는 데 문제가 발생합니다(NPR-32508, NPR-32509).

* 문서 서비스: 서버의 트랜잭션 수가 특정 제한을 초과하는 경우 HTML을 PDF로 변환할 수 없고 [!DNL Forms] 서버에서 파일 유형 설정이 제거됩니다(NPR-32204).

* 적용형 양식: WCAG2 레벨 AA 지침에 따라 브라우저 접근성 도구가 적용형 양식의 오류를 보고합니다(NPR-32312, NPR-32309, CQ-4285439).

* 적용형 양식: Chrome 브라우저 접근성 도구가 모범 사례 오류를 보고합니다(NPR-32310).

* 적용형 양식: Experience Manager Sites 페이지에 포함된 적용형 양식을 구성하는 동안 번역 문제가 발생했습니다(NPR-32168).

* Workbench: PDF 유틸리티 서비스에 PDF 속성 가져오기 작업을 사용하는 동안 오류 메시지가 표시됩니다(NPR-32150).

* 문서 보안: DisableGlobalOfflineSynchronizationData 옵션이 True로 설정되어 보호된 PDF 파일을 오프라인으로 열 수 없습니다(NPR-32078).

* 디자이너: 태그 지정 옵션이 활성화된 경우 생성된 PDF 출력에서 하위 양식 테두리가 사라집니다(NPR-32547, NPR-31983, NPR-31950).

* 디자이너: 표에 병합된 셀이 있는 경우 출력 서비스를 사용하여 XDP 양식에서 변환된 출력 PDF 파일에 접근성 테스트를 수행하면 오류가 발생합니다(CQ-4285372).

* Foundation JEE: 클러스터에서 Experience Manager Forms 서버 연결이 끊어진 경우 캐싱 문제가 발생하여 서버에 다시 연결되지 않습니다(NPR-32412).

## Adobe Experience Manager 6.5.3.0 {#experience-manager-6530}

[!DNL Adobe Experience Manager]6.5.3.0은 **2019년 4월**&#x200B;에 6.5 릴리스의 공식 출시 이후에 발표된 성능, 안정성, 보안 및 주요 고객 수정 사항과 개선 사항을 포함하는 중요한 릴리스입니다. [!DNL Adobe Experience Manager] 6.5의 맨 위에 설치할 수 있습니다.

이 서비스 팩 릴리스의 몇 가지 주요 사항은 다음과 같습니다.

* 내장된 저장소(Apache Jackrabbit Oak)가 버전 1.10.6으로 업데이트되었습니다.

* 이제 [!DNL Experience Manager Assets]에서 Deflate64 알고리즘을 사용하여 만든 ZIP 아카이브를 지원합니다.

* 정렬 가능한 작성된 날짜에 대한 새 열이 DAM 목록 보기 및 자산 검색 결과의 목록 보기에 추가되었습니다.

* 이름 열을 기반으로 한 자산 정렬이 목록 보기에서 활성화되었습니다.

* 이제 [!DNL Dynamic Media]에서 스마트 자르기 비디오 자산을 지원합니다. 스마트 자르기는 장면의 초점을 따라 프레임을 이동하면서 비디오를 다시 자르는 머신 러닝 기반의 기능입니다.

* [!DNL Dynamic Media]에서 스마트 이미징을 지원합니다.

*  워크플로우에서 [부재 중](../forms/using/configure-out-of-office-settings.md) 환경 설정을 지정하는 기능.[!DNL Experience Manager]

*  워크플로우에서 다른 사용자와 [받은 편지함 또는 받은 편지함 항목을 공유](../forms/using/configure-shared-queues-osgi.md)하는 기능.[!DNL Experience Manager]

* [일괄 처리 모드에서 인터랙티브한 커뮤니케이션을 생성](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)하는 기능.

* ContextHub에 번들로 포함된 jQuery의 버전이 3.4.1로 업데이트되었습니다.

### 자산 {#assets-6530-enhancements}

**제품 개선 사항**

* 이제 [!DNL Experience Manager Assets]에서 Deflate64 알고리즘을 사용하여 만든 ZIP 아카이브를 지원합니다(NPR-27573).

* 정렬 가능한 새로 만든 날짜에 대한 열이 목록 보기의 DAM 목록 보기 및 자산 검색 결과에 추가되었습니다(NPR-31312).

* 목록 보기에서 [!UICONTROL 이름] 열을 사용하여 자산 목록을 정렬할 수 있습니다(NPR-31299).

* GLB, GLTF, OBJ 및 STL 자산 파일은 DAM의 [!UICONTROL 자산 세부 정보] 페이지에서 자산 미리 보기를 지원합니다(CQ-4282277).

* `ReplicationOnModifyListener` 이벤트가 [!DNL Dynamic Media]에서 청크 업로드 중 청크 노드에 대해 트리거됩니다(CQ-4281279).

* 이제 [!DNL Dynamic Media]에서 스마트 자르기 비디오 자산을 지원합니다. 스마트 자르기는 장면의 초점을 따라 프레임을 이동하면서 비디오를 다시 자르도록 하는 머신 러닝 기반의 기능입니다(CQ-4278995).

* [!DNL Dynamic Media]에서 스마트 이미징을 지원합니다(CQ-422249).

* 요청에서 쿼리 매개 변수가 전달되면 Foundation 선택기에서 검색 또는 찾아보기 보기가 기본 보기로 설정되었습니다(NPR-31601).

**수정 사항**

* 일부 PDF 문서의 메타데이터는 해당 제목을 수정할 때 업데이트되지 않고 PDF에 저장됩니다(NPR-31629).

* 파일 이름에 더하기 문자(`+`)가 있는 자산에 대해 자산 공유가 작동하지 않습니다(NPR-31547).

* 기본 검색 양식 자산 관리 검색 레일의 편집이 예상대로 작동하지 않습니다(NPR-31502).

* 자산 보기에서 Omnisearch를 사용하여 자산 검색할 때 제안이 표시되지 않습니다(NPR-31496).

* 다른 사용자가 동일한 자산을 다른 컬렉션에서 참조하는 경우 참조된 자산을 다른 위치로 이동할 때 컬렉션 내의 자산 참조는 업데이트되지 않습니다(NPR-31486).

* 중복된 IPTC 태그가 자산 메타데이터에 추가됩니다(NPR-31328).

* 필터 레일에서 검색이 트리거될 때 검색 결과 카운트가 정확하게 업데이트되지 않습니다(NPR-31316).

* 파일 유형 필터에서 두 번째 수준 확인란을 선택 취소하면 모든 확인란이 선택 취소되고 검색 막대의 텍스트가 선택한 또는 선택되지 않은 속성과 동기화되지 않습니다(NPR-31287).

* 모든 구성원(사용자/그룹)은 폴더의 멤버 섹션에서 제거할 수 없습니다. 모든 사용자를 제거하려고 하면 로그인한 사용자가 목록에 추가됩니다(NPR-31171).

* 파일 이름에 더하기 기호(`+`)가 있는 자산은 삭제할 수 없습니다(NPR-31162).

* 폴더 선택 시 상단 메뉴에 표시되는 만들기 드롭다운 메뉴는 만들기 옵션으로 &#39;폴더&#39;를 표시하지 않습니다(NPR-30877).

* 경로에 있는 Deny `jcr:removeChildNodes` 및 `jcr:removeNode`에 대한 ACL이 사용자에 대해 적용되면 폴더 선택 만들기 > 파일 업로드 작업 항목이 누락됩니다(NPR-30840).

* 특정 mp4 자산이 업로드되면 DAM 워크플로우가 부실 상태로 전환되어 나머지 모든 워크플로우가 부실 상태로 전환됩니다(NPR-30662).

* 대용량 PDF 파일(일부 GB 중)이 DAM에 업로드되고 하위 자산이 처리되는 경우 메모리 부족 오류가 발생합니다(NPR-30614).

* 자산의 벌크 이동이 실패하고 경고 메시지가 표시됩니다(NPR-30610).

* [!DNL Dynamic Media]–Scene7 모드에서 실행 중인 [!DNL Experience Manager]에서 자산을 폴더 간에 이동할 때 자산 이름이 소문자로 변경됩니다(NPR-31630).

* 원격 이미지 집합을 편집하는 동안 Scene7 회사 이름과 같은 폴더에 있는 이미지에 대한 오류가 발견되었습니다(NPR-31340).

* [!DNL Dynamic Media]참조가 포함된 자산이 게시되지 않습니다(NPR-31180).

* [!DNL Dynamic Media]7–Scene7 모드에서 [!DNL Dynamic Media Classic]으로 업로드를 완료하는 데 시간이 너무 오래 걸립니다(NPR-31048).

* 이미지 자산에 추가된 핫스팟은 자산 세부 사항 페이지의 인터랙티브 이미지 뷰어를 통해 표시되지 않습니다(NPR-30979).

* [!DNL Experience manager Assets]의 자산에 대해 수행된 작업이 Scene 7로 전달되면 대규모 슬링 작업이 생성되고 처리 중 배너가 다시 나타납니다(NPR-30947).

* 자산의 언어 사본을 만들 때 충돌이 발생하여 Scene 7로 업로드할 수 없습니다(NPR-30932).

* [!DNL Dynamic Media]–Hybrid 모드에서 실행되는 [!DNL Experience Manager]에서 다운로드한 동적 변환이 손상되었습니다(이미지 컨텐츠 유형 대신 &#39;이미지를 찾을 수 없음&#39; 컨텐츠가 있는 텍스트 유형)(NPR-30876).

* [!DNL Dynamic Media] 인코딩 비디오 워크플로우가 [!DNL Dynamic Media Classic]에서 Adobe Experience Manager의 [!DNL Dynamic Media]-Scene7 모드로 마이그레이션된 비디오의 축소판을 생성하지 못합니다(CQ-4282011).

* IpsApiException은 다른 Scene7 회사 ID를 사용하여 하나의 인스턴스에서 다른 인스턴스로 자산을 마이그레이션하는 동안 관찰되었습니다(CQ-4280548).

* 지원되는 3D 모델을 [!DNL Experience Manager]으로 수집할 때 3D 자산 축소판이 도움이 되지 않습니다(CQ-4283701).

* 3D 자산에 카메라 보기가 거의 없는 경우 스크롤 버튼이 뷰어에 표시됩니다(CQ-4283322).

* 자산 세부 사항 페이지의 DimensionalViewer에서 미리 본 업로드된 3D 모델의 컨테이너 높이가 잘못되었습니다(CQ-4283309).

* Internet Explorer 11 및 Safari에서 SmartCropVideoViewer로 비디오를 재생할 수 없습니다(CQ-4281422).

* [!DNL Dynamic Media]–Scene7 실행 모드에서 실행되는 [!DNL Experience Manager]에서 폴더 간에 여러 자산을 이동할 때 이동 단추를 사용할 수 없습니다(CQ-4280384).

* MIME 유형이 MP4 이외인 경우 자산 세부 사항에 왜곡된 비디오가 표시됩니다(CQ-4279704).

* 비디오 프로필이 있는 폴더에서 새로 수집된 비디오는 인코딩 비율이 100%로 완료된 후에도 처리 중 상태로 유지됩니다(CQ-4279389).

* 폴더에서 자산을 이동하면 이상적으로 필요한 것보다 훨씬 많은 슬링 작업(Scene 7 API 호출)이 생성됩니다(CQ-4278664).

* 이미지 집합(또는 미디어 집합)을 만들고 DAM에서 적절한 명명 규칙을 사용하여 이름을 지정하면 Scene 7에서 이미지 집합 이름이 소문자로 변경됩니다(CQ-428112).

* Scene 7 Migrator가 게시 상태를 잘못 설정합니다(CQ-4263492).

* Omnisearch를 통해 수행한 터치 UI 검색 결과 페이지가 자동으로 스크롤되어 콘텐츠 조각에서 사용자의 스크롤 위치를 잃게 됩니다(CQ-4282898).

* PDF 파일은 색인이 되어 있지 않고 내부 콘텐츠를 검색할 수 없습니다(CQ-4278916).

* 사용자 선택기로 나열되지 않은 그룹: false가 true와 같아야 함 오류가 다른 `principalName` 및 `authorizableId`를 포함하여 닫힌 사용자 그룹 추가 시 관찰됩니다(CQ-4278177).

* 자산 UI 열 보기가 특정 테넌트의 dam 루트 경로와 관계없이 모든 경로를 표시합니다(CQ-4278175).

* 자산 선택기의 검색이 예상대로 작동하지 않습니다(CQ-4275886).

* 변환 워크플로우가 실패했습니다(CQ-4271928).

* DAM 이벤트 삭제 기능은 최신(`maxSavedActivities`) 이벤트 데이터를 삭제하고 이전에 만든 데이터를 저장합니다(NPR-31336).

* Omnisearch를 통해 수행한 터치 UI 검색 결과 페이지가 자동으로 스크롤되어 사용자의 스크롤 위치가 손실됩니다(NPR-31307).

* 모두 선택한 다음 터치 UI에서 일부 항목(폴더/개별 자산)을 선택 해제할 때 작업 표시줄 및 자산 수가 업데이트되지 않습니다(NPR-31118).

* 자산에 대한 작업 세부 사항을 폴링하는 동안 [!DNL Experience Manager]에 예외가 표시됩니다(CQ-4283569).

### 사이트

* LiveCopy 상속이 끊어지면 LiveCopy 페이지에 LiveCopy 링크 대신 언어 복사 링크가 표시됩니다(NPR-30980).
* 새 블루프린트의 경우 레코드 수가 40개를 초과하는 경우 처음 40개의 레코드만 표시됩니다. 블루프린트는 나머지 레코드에 대한 빈 라인을 표시합니다(NPR-31182).
* 사용자가 메뉴의 설명 속성에 일본어 또는 한국어 문자를 추가하면 메뉴에 일본어 및 한국어 텍스트의 왜곡된 문자가 표시됩니다(NPR-31331).
* 리치 텍스트 편집기(RTE)가 포함된 테이블을 목록 항목으로 삽입할 수 없습니다(NPR-30879).
* 기본 제공되는 스캐폴딩 RTE(리치 텍스트 편집기)가 예기치 않게 인라인 글꼴 크기를 요소에 적용합니다(NPR-31284).
* 사용자가 왼쪽 레일 필드에 초점을 맞추고 키보드 단축키를 사용하여 콘텐츠를 붙여넣으면 왼쪽 레일 필드에서 복사한 콘텐츠 대신 페이지 편집기 클립보드의 콘텐츠를 붙여넣습니다(NPR-31172).
* 사용자가 다중 필드에 파일 업로드 필드를 추가하면 이미지 경로가 다중 필드 노드 대신 구성 요소 노드에 저장됩니다(NPR-30882).
* `ResponsiveGridExporter` API는 `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` 인터페이스를 반환하지 않습니다. `com.day.cq.wcm.foundation.model.impl` 패키지는 비공개 패키지로 선언됩니다(NPR-31398).

<!-- Review: NPR-31398 has fixVersion as 6530. However, it is mentioned twice in 6530 and 6520 as fixed. 
Remove one mention of this fix.
-->

* 일부 Experience Fragments가 포함된 페이지를 편집기가 아닌 모드(`editor.html` 접두사가 없고 `wcmmode=disabled`된 작성자 및 또는 게시자에서)로 열리면 HTTP 상태 오류 코드 `500`에서 요청이 종료됩니다(NPR-30743).
* 사용자는 암호를 변경하고 프로필 페이지에 액세스할 수 없습니다(NPR-31161).

### 검색 및 사용자 인터페이스 {#ui-interface-and-search}

* 검색 결과 페이지의 카드 보기에서 목록 보기로 전환하는 경우 페이지를 스크롤하려면 지연이 있습니다(NPR-31286).

* [!DNL Sites] 사용자 인터페이스의 목록 보기에서 [!UICONTROL 모두 선택] 확인란이 숨겨집니다(NPR-31614).

* 검색 결과 페이지에서 [!UICONTROL 모두 선택] 카운트가 잘못되었습니다(NPR-31120).

* 메타데이터 편집기에 존재하지 않는 태그가 표시됩니다(NPR-31119).

### 번역 {#translation}

* 번역 작업에서 기한 옵션을 선택하면 두 개의 달력 팝업이 나타납니다(NPR-31270).

### 플랫폼

* 웹 콘솔의 Mime 유형 옵션이 작동하지 않습니다(NPR-31108).

* SSO(Single Sign-On)를 구성할 때 클라이언트 인증서가 허용되지 않습니다(NPR-31165).

* Jetty 기반 HTTP 서비스에 대한 버퍼 크기 구성의 업데이트가 저장되지 않습니다(NPR-30925).

* 이제 QueryBuilder는 xpath 쿼리에서 `fn:name()` orderby를 지원합니다(NPR-31322).

* [!DNL Experience Manager] 6.3에서 업그레이드 시 중복 활성화 트리가 만들어집니다(NPR-31513).

* 전달된 요청은 슬링 인증 동안 설정된 응답 헤더를 보존하지 않습니다(NPR-30013).

* 선택기 구성 요소 내에서 검색이 작동하지 않습니다(NPR-31692).

* 서로 다른 버전의 Apache POI 및 Apache Tika 번들로 인해 ZIP 파일을 [!DNL Experience Manager Communities] 게시물에 첨부할 때 오류가 표시됩니다(NPR-31018).

* 이 `org.apache.sling.distribution.api` 번들은 구성 관리자에 숨겨져 있으므로 사용자 지정 번들에는 사용할 수 없습니다(NPR-31720).

### 프로젝트

* 달력 보기를 전환할 수 없습니다(NPR-31271).

### 브랜드 포털 {#assets-brand-portal-6530}

**제품 개선 사항**

* [!DNL Experience Manager Assets]의 자산 소싱 가져오기 워크플로우가 [!DNL Brand Portal]에서 새로 만든 자산만 [!DNL Experience Manager]으로 가져오도록 수정되었으며, 복제를 방지하기 위해 NEW 폴더에 이미 있는 자산을 건너뜁니다(CQ-4278527).

**수정 사항**

* 자산 소싱 기능에서 새 기여도 폴더를 만들 때 잘못된 아이콘이 표시됩니다(CQ-4282825).
* 새 기여도 폴더를 만들 때 기여도 폴더에 하위 폴더 하나 또는 둘 다(NEW 및 SHARED) 나타나지 않습니다(CQ-4282424).
* 사용자가 [!DNL Experience Manager] 끝의 기여도 폴더에서 새 자산을 받은 후 [!DNL Brand Portal]에서 [!DNL Brand Portal]로 기여도 폴더를 다시 게시하려고 하면 시스템에서 예외가 발생합니다(CQ-4279740).
* 기여도 폴더(중첩된 폴더) 내에 기여도 폴더를 만들 수 없으므로 복잡성을 방지할 수 있습니다(CQ-4278391).
* [!DNL Experience Manager] Admin Console.솔에서 가져온 [!DNL Brand Portal] 사용자 목록(.csv 파일)을 업로드할 때 시스템에 예외가 발생합니다. 다음 .csv 파일의 이메일, 이름 및 성 필드만 필수 필드입니다(CQ-4278390).

### 커뮤니티 {#communities-6530}

**수정 사항**

* 그룹 관리(그룹 열기/편집/게시/삭제)에 대한 빠른 링크는 커뮤니티 관리자(그룹 관리자/사이트 관리자)에 표시되지 않습니다(NPR-31627).
* 페이지를 수동으로 새로 고치거나 다시 로드하지 않는 한 제출된 블로그가 표시되지 않습니다(NPR-31599).
* 언급 기능에 사용되는 JCR 쿼리는 대/소문자를 구분하며 결과를 반환하는데 너무 오래 걸립니다(NPR-31475).
* [!DNL Experience Manager] 6.5 UberJar 파일에서 예외가 발생하고, 6.5 UberJar 파일에서 `cq-social-translation` 번들이 누락되었습니다(NPR-31186).[!DNL Experience Manager]
* Jackson Databind 라이브러리가 새로운 취약점을 해결하기 위해 버전 2.9.9.3으로 업데이트되었습니다(NPR-30967).
* 활동 및 알림 제목이 일치하지 않습니다(NPR-30941).
* 페이지 매김이 [!DNL Communities] 블로그에서 제대로 작동하지 않습니다(NPR-30914).
* Analytics 보고서가 [!DNL Experience Manager] 작성자 환경에서 채워지지 않으며 빈 페이지가 표시됩니다(NPR-30913).

### Oak {#oak}

* Lucene 인덱스 업데이트로 인해 작성자 서버가 느려집니다(NPR-31548).

### 양식 {#forms-6530}

>[!NOTE]
>
>[!DNL Experience Manager] 서비스 팩에는 [!DNL Experience Manager Forms] 수정 사항이 포함되어 있지 않습니다. 이러한 수정 사항은 별도의 Forms 추가 기능 패키지를 사용하여 전달됩니다. 또한, JEE의 [!DNL Experience Manager Forms]에 대한 수정 사항이 포함된 누적 설치 프로그램이 릴리스됩니다. 자세한 내용은 [Experience Manager Forms 추가 기능 설치](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) 및 [JEE에 Experience Manager Forms 설치](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)를 참조하십시오.

#### Forms 추가 기능 패키지 {#forms-add-on-package-6530}

**적응형 양식**

* 적응형 양식을 현지화하는 동안 문자열에 사전 키가 포함됩니다(NPR-31110).

**대화형 통신**

* **MissingNode.toString()**&#x200B;은 Jackson 라이브러리를 2.10.0으로 업그레이드한 후 부정확한 결과를 반환합니다(NPR-31549).

* 텍스트 편집기가 Microsoft Word에서 복사한 텍스트에서 공백 문자를 임의로 제거합니다(NPR-31113).

**서신 관리**

* LiveCycle ES4SP1에서 [!DNL Experience Manager] 6.5로 문자를 마이그레이션하는 동안에는 캡션 및 도구 설명이 표시되지 않습니다(NPR-31615).

* **문자를 초안으로 저장하는 동안 텍스트 흐름 형식이 더 이상 지원되지** 않습니다(NPR-30463).

**워크플로우**

* 100% CPU 사용률로 인해 OSGi 워크플로우가 실패합니다(NPR-31233).

**HTML5 양식**

* XDP 양식의 HTML5 미리 보기를 생성하면 하위 양식의 인스턴스를 추가하는 동안 깜박임이 표시됩니다(NPR-30909).

#### JEE 설치 프로그램의 양식 {#forms-jee-installer-6530}

**양식 - 문서 서비스**

* 다음 .NET 프로젝트에서 MTOM을 사용하는 SOAP 웹 서비스에는 AssemblerServiceClient 호출 및 HtmlToPDF2 메서드에 대한 예외가 표시됩니다(NPR-4281771).

* AXIS 1.4 jar에서 보안 취약점 2012-5784 및 2014-3596을 발견했으며 [AXIS1.4.1 jar](https://helpx.adobe.com/kr/aem-forms/quick-fixes/6-5/jee-patch-0014.html)(NPR-31015)에서 제공하는 수정 사항입니다.

**Foundation JEE**

* 작업 구성은 양식 호출 워크플로우 제출 작업에 대한 프로세스 이름을 로드하지 않습니다.

### 기능 팩이 포함됨 {#feature-packs-included-6530}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 고객의 경우 [!DNL Experience Manager] 서비스 팩, 누적 수정 팩 또는 기능 팩을 설치한 후 [!DNL Experience Manager Forms] 추가 기능 패키지를 설치해야 합니다.

#### 양식 - 기초 JEE {#forms-foundation-jee-feature}

* [!DNL Experience Manager]Oracle 18c에 대해 Forms가 지원됩니다(NPR-29155).

## Adobe Experience Manager 6.5.2.0 {#experience-manager-6520}

[!DNL Adobe Experience Manager][!DNL Adobe Experience Manager] 6.5.2.0은 2019년 4월에&#x200B;**6.5의 공식 출시 이후에 발표된 성능, 안정성, 보안 및 주요 고객 수정 사항과 개선 사항을 포함하는 중요한 릴리스입니다**. [!DNL Experience Manager] 6.5의 맨 위에 설치할 수 있습니다.

이 서비스 팩 릴리스의 몇 가지 주요 사항은 다음과 같습니다.

* 내장된 저장소(Apache Jackrabbit Oak)가 버전 1.10.3으로 업데이트되었습니다.
* 경험 구성요소를 [!DNL Adobe Target]의 사용자 지정 작업 공간으로 직접 내보낼 수 있는 구성 속성이 추가되었습니다.
* Assets 사용자는 시각적으로 유사한 이미지를 검색할 수 있습니다. [!DNL Experience Manager]는 사용자가 선택한 이미지와 유사한 DAM 저장소에서 스마트 태그가 지정된 이미지를 표시합니다. [시각적 검색](../assets/search-assets.md#visualsearch)을 참조하십시오.

* 원격 DAM 배포에서 문서를 가져오도록 지원을 추가하는 연결된 자산 기능이 향상되었습니다. 이제 사이트 작성자가 콘텐츠 파인더에서 지원되는 문서 유형을 검색하고 필터링할 수 있습니다. 원격 문서를 웹 페이지의 다운로드 구성 요소에 추가할 수 있습니다. [연결된 자산 사용](../assets/use-assets-across-connected-assets-instances.md)을 참조하십시오.

* 여러 값을 갖는 옵션을 지원하기 위해 추가 MIME 유형을 사용하는 EnhanceDocument 유형 필터입니다.
* 다중 리소스 지원을 위해 외부 재처리 워크플로우가 도입되었습니다.
* 복제에 기본 자산 필터를 사용하여 [!DNL Dynamic Media] 성능이 최적화되었습니다.
* DMS7에 대한 자르기/회전 자산 편집 옵션이 복원되었습니다.
* VideoPlayer에 로드 시 비디오를 음소거하는 옵션이 구현되었습니다.
* 자산 UI 열 보기에 임차인 관련 콘텐츠만 표시되도록 수정합니다.
* 검색 결과에 스타일 아코디언 변경 사항이 반영되도록 수정합니다.

### 자산

**제품 개선 사항**

* 원격 DAM 배포에서 문서를 가져오도록 지원을 추가하는 연결된 자산 기능이 향상되었습니다. 이제 사이트 작성자가 콘텐츠 파인더에서 지원되는 문서 유형을 검색하고 필터링할 수 있습니다. 원격 문서를 웹 페이지의 다운로드 구성 요소에 추가할 수 있습니다. CQ-4270245용 핫픽스. [연결된 자산 사용](/help/assets/use-assets-across-connected-assets-instances.md)을 참조하십시오.

* [!DNL Experience Manager Assets] 사용자는 시각적으로 유사한 이미지를 검색할 수 있습니다. [!DNL Experience Manager]는 사용자가 선택한 이미지와 유사한 DAM 저장소에서 스마트 태그가 지정된 이미지를 표시합니다. [시각적 검색](../assets/search-assets.md#visualsearch)을 참조하십시오.

**수정 사항**

* ACP API에서 생성된 URL 및 폴더 메타데이터의 자산 경로는 URL로 인코딩되지 않습니다. GRANITE-26198: CQ-4271814용 핫픽스
* 이름에 백분율 기호(%)가 있는 폴더로 아카이브 압축을 푼 경우 [!DNL Experience Manager Assets] 인터페이스를 사용하여 열 수 없습니다. NPR-29989: CQ-4270467용 핫픽스
* Touch UI: 게시 마법사를 관리하는 동안 post 요청 본문의 페이지 뒤에 참조가 추가되어 모든 자산이 페이지 뒤에 게시되며, 페이지가 렌더링될 때 게시 인스턴스의 일부 자산이 누락됩니다. NPR-29985: CQ-4270724용 핫픽스
* 자산 관계 해제 기능은 이름에 특수 문자(URI로 인코딩되는 문자)가 있는 관련 자산에 대해 작동하지 않습니다. NPR-30387: CQ-4274446용 핫픽스
* 콘텐츠 조각을 편집할 때 버전이 잘못된 사용자로 생성됩니다.
* 임차인 기반 시스템에서 컬렉션을 작성하는 중에 오류가 발생합니다. NPR-30114: CQ-4272948용 핫픽스
* Asset UI 열 보기는 현재 임차인의 dam 루트 경로를 준수하지 않지만 모든 임차인 dam 경로에 액세스합니다. NPR-30636: CQ-4275481용 핫픽스
* 제한된 파일 경고 창을 통해 삽입된 이미지로 가능한 XSS(교차 사이트 스크립팅) 공격을 볼 수 있습니다. NPR-30617: CQ-4270133용 핫픽스
* MultiTenant: 폴더 속성을 저장하는 임차인은 성공 메시지와 작업이 실패했음을 설명하는 오류 메시지, &quot;속성을 편집할 수 없습니다. 권한이 부족합니다.&quot;를 모두 관찰하면 혼동됩니다. NPR-30545: CQ-4275333용 핫픽스
* 자산 선택기 대화 상자에서는 자산을 선택할 수 없으므로 관련 소스 교체 기능을 사용하여 소스를 업데이트할 수 없습니다. NPR-30502: CQ-4275029용 핫픽스
* [!UICONTROL DAM 자산 업데이트] 워크플로우 - 크기가 큰 mp4 파일을 업로드할 때 사용되지 않는 상태입니다. NPR-30480: CQ-4271352용 핫픽스
* null 페이로드로 인해 모든 후속 리뷰 관련 작업이 실패하므로 리뷰 작업 만들기 기능이 작동하지 않습니다. NPR-30468: CQ-4274263용 핫픽스
* Datapower를 통한 Adobe 스마트 태그 연결 문제. NPR-30026: CQ-4269457용 핫픽스
* Assets UI 열 보기에서 레일 왼쪽에 있는 필터를 여는 동안 오류가 발생했습니다. NPR-30501: CQ-4273862용 핫픽스
* LDAP에서 동기화된 그룹을 자산 폴더의 CUG(폐쇄된 사용자 그룹) 속성에서 추가할 때 이 그룹이 저장 및 검색되지 않습니다. NPR-30615: CQ-4274689용 핫픽스
* 필터 검색 스타일 및 방향 필드는 자동 완성된 값을 검색 쿼리에 적용하지 않습니다. NPR-30620: CQ-4275724용 핫픽스
* 이름에 공백 및 &quot;&amp;&quot; 문자가 있는 폴더의 자산 공유 링크에는 일부 자산에 대해 빈 회색 카드가 표시됩니다. NPR-30557: CQ-4270187용 핫픽스
* 폴더 메타데이터 스키마 양식은 자동으로 데이터 유형을 감지하지 않으므로 양식 전송 시 관련된 TypeHint를 생성하지 않습니다. NPR-30599: CQ-4275227용 핫픽스
* 자산 자르기 및 회전 편집 옵션이 DMS7 작성 UI에서 비활성화됩니다. NPR-30118: CQ-4273221용 핫픽스
* DMS7 구성이 있는 [!DNL Experience Manager] 인스턴스에서 링크 공유 기능이 작동하지 않습니다. NPR-30080, NPR-30492: CQ-4273651용 핫픽스
* 페이지에 [!DNL Dynamic Media]–Scene7 구성 요소를 추가한 다음 페이지를 게시하면 dmscene7 구성이 매번 트리거되지 않습니다. NPR-30641: CQ-4275962용 핫픽스
* 처리 프로필당 하나의 IPS(침입 방지 시스템) 작업만 작성하도록 [!DNL Experience Manager]에 IPSJobJournal이 추가되었습니다. NPR-30490: CQ-4273614용 핫픽스
* [!DNL Dynamic Media]: 자산이 복제되지 않도록 하는 기본 필터가 게시 노드에 추가되었습니다. [!DNL Experience Manager] NPR-30538: CQ-4274678용 핫픽스
* 폴더를 페이로드로 허용하도록 여러 리소스 지원을 위한 외부 재처리 워크플로우가 도입되었습니다. 이 워크플로우는 2단계로 진행됩니다. 메타데이터 맵을 통해 다음 단계로 자산을 재처리하고, 자산 핸들이 없는 모든 자산을 단일 IPS 작업으로 S7에 다시 업로드합니다. 자세한 내용은 [!DNL Dynamic Media] Cloud Service 구성을 참조하십시오. NPR-30489: CQ-4272903용 핫픽스
* 올바른 CSV 다음에 잘못된 CSV를 업로드하면 올바른 CSV가 지워집니다. CQ-4277694, CQ-4277814용 핫픽스
* 제거할 기여도 폴더와 관련된 잘못된 아이콘입니다. CQ-4277580용 핫픽스
* 자산 기여 탭의 사용자 선택기에서 사용자 선택 시 사용자의 이름이 표에 표시되지 않고 속성 페이지의 사용자 삭제 대화 상자에 잘못된 텍스트가 표시됩니다. CQ-4277875용 핫픽스
* 사용자를 선택하고 추가를 클릭하여 사용자 선택기의 자산 기여 폴더에 기여자를 추가할 수 없습니다. CQ-4277824, CQ-4278087용 핫픽스
* 사용자 선택기에서는 소문자 사용자 이름으로 검색할 수 없습니다. CQ-4277958, CQ-4277930용 핫픽스
* 관리자가 아닌 사용자가 자산 기여 폴더의 새 폴더에 자산을 게시할 수 있습니다. CQ-4278200용 핫픽스
* DAM 사용자(관리자가 아닌 사용자)는 자산 기여 폴더에 기여자를 추가할 수 없습니다. CQ-4278192용 핫픽스
* &quot;만들기&quot; 버튼은 자산 기여 폴더에 표시됩니다. CQ-4277560용 핫픽스
* 관련성을 기준으로 검색 쿼리를 정렬하면 [!DNL InDesign] 템플릿과 함께 [!DNL InDesign] 문서가 반환됩니다. CQ-4273864용 핫픽스
* 대문자 이메일 ID가 있는 사용자는 이전에 체크아웃된 자산에 대해 체크인할 수 없습니다. CQ-4276575용 핫픽스
* 삭제 작업은 선택한 사전 설정에만 적용되며, 작업 후 화면의 목록이 자동으로 새로 고쳐지면 이미 새로 고친 다른 사전 설정이 표시됩니다. CQ-4261461용 핫픽스
* [!DNL Dynamic Media]–Hybrid 모드에서 [!DNL Dynamic Media] Cloud Services를 구성하면 [!DNL Analytics]에 빈 보고서 세트가 여러 개 생성되고, [!DNL Experience Manager]에 저장된 보고서 세트 ID가 없기 때문에 보고서 세트가 중복됩니다. CQ-4249780용 핫픽스
* [!DNL Experience Manager] Assets에서 중복된 이름으로 이름을 바꾸면 Scene7과 동기화되지 않았습니다. CQ-4276763용 핫픽스
* 사용자 생성 콘텐츠가 검색 필터 패널에 잘못 표시됩니다. CQ-4273875용 핫픽스
* TIFF 이미지에서 유사 항목 찾기 옵션을 사용할 수 없습니다. CQ-4278238용 핫픽스
* VideoPlayer에 로드 시 비디오를 음소거하는 옵션이 구현되었습니다. CQ-4266465용 핫픽스
* 뷰어 - 외부 비디오가 사용되는 경우 VideoViewer: poster=none이 제대로 작동하지 않습니다. CQ-4265536용 핫픽스
* IE11 및 MS Edge 브라우저에서 비디오 재생 중에 대기 아이콘이 표시됩니다. CQ-4251539용 핫픽스
* 3.8 SDK 및 5.13 뷰어 README 파일이 업데이트되지 않으며 이전 릴리스의 정보를 포함합니다. CQ-4273737용 핫픽스
* 콘텐츠 조각은 변경 사항을 저장하기 전에도 버전이 지정됩니다. NPR-30616: CQ-4273088용 핫픽스
* 썸네일 프로세스에서 Asset#getMetadata(String)를 Asset#getMetadataValueFromJcr(String)로 바꿉니다. NPR-30491: CQ-4273067용 핫픽스
* jpg를 업로드하면 메시지의 여러 인스턴스가 각 자산에 대해 &quot;ReplicateOnModifyWorker 복제가 업데이트&quot;되어 성능이 저하됩니다.
* 아카이브 추출 기능을 사용하여 zip 아카이브 압축을 풀면 이름에 해당 제목의 퍼센트(%)가 포함된 폴더에 문제가 발생합니다. NPR-29990: CQ-4270467용 핫픽스

### 사이트 {#sites-6520}

* LiveCopy 상속이 끊어지면 LiveCopy 페이지에 LiveCopy 링크 대신 언어 복사 링크가 표시됩니다(NPR-30980).
* 새 블루프린트의 경우 레코드 수가 40개를 초과하는 경우 처음 40개의 레코드만 표시됩니다. 블루프린트는 나머지 레코드에 대한 빈 라인을 표시합니다(NPR-31182).
* 텍스트 구성 요소의 리치 편집기(RTE) 플러그인은 일본어 및 한국어 텍스트의 왜곡된 문자를 표시합니다(NPR-31331).
* 리치 텍스트 편집기(RTE)가 포함된 테이블을 목록 항목으로 삽입할 수 없습니다(NPR-30879).
* 즉시 스캐폴딩할 수 있는 리치 텍스트 편집기(RTE)가 예기치 않게 인라인 글꼴 크기를 요소에 적용됩니다(NPR-31284).
* 사용자가 왼쪽 레일 필드에 초점을 맞추고 키보드 단축키를 사용하여 컨텐츠를 붙여넣으면 왼쪽 레일 필드에서 복사한 컨텐츠 대신 페이지 편집기 클립보드의 컨텐츠를 붙여넣습니다(NPR-31172).
* 사용자가 다중 필드에 파일 업로드 필드를 추가하면 이미지 경로가 다중 필드 노드 대신 구성 요소 노드에 저장됩니다(NPR-30882).
* `ResponsiveGridExporter` API는 `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` 인터페이스를 반환하지 않습니다. `com.day.cq.wcm.foundation.model.impl` 패키지는 비공개 패키지로 선언됩니다(NPR-31398).
* 일부 Experience Fragments가 포함된 페이지를 편집기가 아닌 모드(`editor.html` 접두사가 없고 `wcmmode=disabled`된 작성자 및 또는 게시자에서)로 열리면 HTTP 상태 오류 코드 500에서 요청이 종료됩니다(NPR-30743).

### WCM - 페이지 편집기 {#wcm-page-editor-6520}

**제품 개선 사항**

* 여러 값을 갖는 옵션을 지원하도록 추가 MIME 유형을 사용하는 EnhanceDocument 유형 필터입니다. CQ-4270694용 핫픽스

### 콘텐츠 조각 관리 {#content-fragment-management-6520}

* 콘텐츠 조각 모델 UI에 사용된 쿼리가 매우 느리므로 오류가 발생합니다. CQ-4270807용 핫픽스

### UI - 기초 {#ui-foundation}

* 사용자가 특정 사용자 인터페이스 내에서 &#39;m&#39;, &#39;p&#39;, &#39;e&#39;를 사용하지 못하도록 하는 단축키 트리거입니다. NPR-30355: GRANITE-26346용 핫픽스
* [!DNL Experience Manager Assets] 검색 UI를 닫으면 왼쪽 레일이 컨텐츠 선택 사항으로 재설정되지 않아 사용자가 이후에 필터 레일을 다시 열 수 없습니다. NPR-30509: CQ-4274716용 핫픽스
* 다중 임차인 환경: [!DNL Experience Manager Assets] UI 최상위 탐색을 사용할 수 없으며 JavaScript 오류가 발생합니다. NPR-30104: GRANITE-26344용 핫픽스

### 번역 {#translation-6520}

* 번역 문제 - 일부 구성 요소만 기계 번역을 사용하여 번역됩니다. NPR-30079: CQ-4273764용 핫픽스

### 플랫폼 {#platform-6520}

* [!DNL Experience Manager] 기본 메일 발송자가 TLS v1.2를 통해 원격 SMTP 서버로 메일을 전송할 수 없습니다. NPR-30476: GRANITE-26605용 핫픽스

### 프로젝트 {#projects-6520}

* dam:folderThumbnailPaths 값이 새로 고쳐지지 않으며, 폴더 내의 자산을 삭제한 후에도 이전 썸네일이 표시됩니다. NPR-30424: CQ-4273667용 핫픽스
* 이동 옵션을 완료할 때 자산의 제목과 이름은 변경되지 않은 상태로 유지됩니다. NPR-30647: CQ-4276265용 핫픽스

### 커뮤니티 {#communities-6520}

* 사용자 동기화 진단은 완전히 손상되어 작동하지 않습니다. NPR-30004, NPR-29943: CQ-4270287, CQ-4271348용 핫픽스

### 슬링 {#sling}

* 6.3.3.2에서 6.5로 인스턴스를 업그레이드하면 OSGi 구성이 중복됩니다. NPR-30130: CQ-4274016용 핫픽스

### 통합

* 사용자 지정 콘텐츠는 인스턴스를 다시 시작할 때까지 게시 인스턴스에 올바르게 표시되지 않습니다. NPR-30377: CQ-4273706용 핫픽스
* 웹 사이트에서 Launch를 구성할 때 라이브러리 주소에는 앞에 슬래시(/)가 추가되어 매번 수동으로 작업해야 합니다. NPR-30694: CQ-4275501용 핫픽스

### 양식 {#forms-6520}

>[!NOTE]
>
>[!DNL Experience Manager] 서비스 팩에는 [!DNL Experience Manager Forms] 수정 사항이 포함되어 있지 않습니다. 이러한 수정 사항은 별도의 [!DNL Forms] 추가 기능 패키지를 사용하여 전달됩니다. 또한, JEE의 [!DNL Experience Manager Forms]에 대한 수정 사항이 포함된 누적 설치 프로그램이 릴리스됩니다. 자세한 내용은 [Experience Manager Forms 추가 기능 설치](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) 및 [JEE에 Experience Manager Forms 설치](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)를 참조하십시오.

[!DNL Experience Manager] 6.5.2.0 Forms의 주요 기능은 다음과 같습니다.

* `RenderAtClient` Forms OSGi용 API의 `PDFFormRenderOptions`에 &#39;자동&#39; 설정이 추가되었습니다. [!DNL Experience Manager]

#### Forms 추가 기능 패키지

**백엔드 통합**

* 호스팅된 AWS의 로드 균형 조정된 URL을 사용하여 양식 데이터 모델을 구성할 수 없습니다. NPR-30123: CQ-4273359용 핫픽스
* WSDL(웹 서비스 정의 언어)을 사용하여 FDM(양식 데이터 모델)을 만드는 동안 `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type` 오류 메시지가 반환됩니다. NPR-30477: CQ-4272921용 핫픽스

**서신 관리**

* 콘솔에서 다음 오류가 발생하여 간헐적으로 CCR UI(통신 UI) 변환 만들기가 실패합니다.
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**대화형 통신**

* 양식 데이터 모델에 필수로 표시된 필드가 CCR UI(Create Correspondence UI)에 필수로 표시됩니다. NPR-30623: CQ-4274902용 핫픽스

**양식 - 워크플로우**

* 감시 폴더의 매핑되지 않은 출력 변수로 인해 호출이 실패합니다. CQ-4264451용 핫픽스

**HTML5 양식**

* 사용자 지정 코드 또는 프로젝트가 두 번째로 배포되면 페이지가 렌더링되지 않고 다음 오류가 발생합니다. .

   `org.apache.sling.scripting.sightly.SightlyException.`

   NPR-30539: CQ-4272509용 핫픽스

* 검색 모드에서 비시각적 데스크탑 액세스를 사용하여 HTML5 양식을 읽을 때 Chrome 브라우저는 양식 디자인에서 각 SVG(규모 가변적인 벡터 그래픽) 앞에 있는 &quot;그래픽&quot;을 읽습니다. NPR-30449: CQ-4274732용 핫픽스

#### Forms JEE 설치 프로그램

**양식 - 문서 보안**

* 타임스탬프가 포함된 서명이 적용되지 않고 ALC-DSC-003-000: com.adobe.idp.dsc.DSCInvocationException: 호출 오류가 발생합니다. NPR-30820: CQ-4275852용 핫픽스

**양식 - 문서 서비스**

* SubmitURL에 앰퍼샌드(&amp;)가 포함된 경우 renderpdf 서블릿에 대한 POST 요청이 수행될 때 로그에 구문 분석 오류가 표시됩니다. NPR-30865: CQ-4278232용 핫픽스

**양식 - 기초 JEE**

* HTMLtoPDF 서비스가 JMX 콘솔에 maxReuseCount를 표시하지 않습니다. NPR-30134, NPR-30304: CQ-4273763용 핫픽스
* [!DNL Experience Manager Forms] Workbench에서 웹 서비스를 호출하여 웹 서비스 연결을 추가하거나 편집하면 ClassNotFoundException org.apache.axis.message.SOAPBodyElement 오류가 발생합니다. NPR-30105: CQ-4273217용 핫픽스

### 기능 팩이 포함됨

>[!NOTE]
>
>[!DNL Experience Manager Forms] 고객의 경우 [!DNL Experience Manager] 서비스 팩, 누적 수정 팩 또는 기능 팩을 설치한 후 [!DNL Experience Manager Forms] 추가 기능 패키지를 설치해야 합니다.

#### 사이트 {#sites-feature-packs-included}

* 경험 구성요소를 [!DNL Adobe Target]의 사용자 지정 작업 공간으로 직접 내보낼 수 있는 구성 속성이 추가되었습니다. NPR-29189: CQ-4249782용 핫픽스

#### 양식 - 문서 서비스 {#forms-document-services-1}

* `RenderAtClient` OSGi용 API의 `PDFFormRenderOptions`에 &#39;자동&#39; 설정이 추가되었습니다. [!DNL Experience Manager Forms] NPR-30759: CQ-4278193용 핫픽스

## Adobe Experience Manager 6.5.1.0 {#experience-manager-6510}

[!DNL Adobe Experience Manager][!DNL Adobe Experience Manager] 6.5.1.0은 2019년 4월에&#x200B;*6.5의 공식 출시 이후에 발표된 성능, 안정성, 보안 및 주요 고객 수정 사항과 개선 사항을 포함하는 중요한 릴리스입니다.*[!DNL Experience Manager] 6.5의 맨 위에 설치할 수 있습니다.

이 서비스 팩 릴리스의 몇 가지 주요 사항은 다음과 같습니다.

* 사용자 지정 속성으로 이벤트를 추적할 때 dynamic-UI-state 포함을 활성화했습니다.
* [!DNL Dynamic Media]–Scene7 모드에 360도 비디오 자산의 배송에 대한 지원이 포함되었습니다.
* 리치 텍스트 편집기의 스타일 플러그인을 통해 *일본어 자동 줄 바꿈* 기능이 활성화되었습니다. 자세한 내용은 [일본어 자동 줄바꿈 구성](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)을 참조하십시오.

### 자산

* S3 다중 부분 지원에 대한 DAM DMGateway 인터페이스가 업데이트되었습니다. NPR-29740: CQ-4226303용 핫픽스
* [!DNL Experience Manager] 6.5로 업그레이드한 후 변환 미리 보기를 수행하면 `Only empty tenantId is currently supported` 오류가 발생합니다. NPR-29986: CQ-4272353에 대한 핫픽스
* 작업을 삭제할 수 있는 삭제 대화 상자가 표시되지 않습니다. NPR-29720: CQ-4271074용 핫픽스
* 속성 페이지에서 자산 제목을 추가한 후 사용자가 페이지를 닫으려고 하면 [!DNL Experience Manager]에 속성 페이지가 다시 열립니다. NPR-29627: CQ-4264929용 핫픽스
* VersioningTimelineEventProvider는 nt: 버전 유형의 노드와 함께 루트 버전을 제공해야 합니다. GRANITE-26063용 핫픽스
* [!DNL Experience Manager] DM-Scene7 모드에서 360 구형 비디오를 업로드하고 재생하는 기능이 구현되었습니다. CQ-4265131용 핫픽스
* 소스가 편집되면 Live copy가 올바르지 않은 상태를 검색합니다. CQ-4265451용 핫픽스
* [!DNL Experience Manager Assets]에 대한 다중 사이트 관리자 지원이 활성화되었습니다. CQ-4271453, CQ-4268621, CQ-4257491용 핫픽스
* [!DNL Experience Manager] 인터페이스는 타임라인 내역에서 자산의 현재 버전에 대한 추가 항목을 표시하여 [!DNL Adobe Asset Link]의 최신 체크인 설명을 표시해야 합니다. CQ-4262864용 핫픽스
* 속성이 누락된 경우 콘텐츠 조각 타임라인에 오류 메시지가 표시됩니다. CQ-4272560용 핫픽스
* 전체 화면으로 확장하는 경우 Scene 7 비디오 플레이어에 문제가 발생합니다. CQ-4266700용 핫픽스
* ZoomVerticalViewer: 단일 이미지 자산을 사용하는 경우 이동 버튼이 표시되지 않습니다. CQ-4264795용 핫픽스
* Live Copy에서 하위 노드를 삭제하려면 liveRelationship을 분리해야 합니다. CQ-4270395용 핫픽스
* 메타데이터 스키마에는 글로벌 구성의 항목만 포함되어 있고 활성 임차인의 항목이 없습니다. formPath URL 값은 변경된 경우에도 기본값으로 되돌아 갑니다. NPR-29945: CQ-4262898용 핫픽스
* [!DNL Brand Portal]에 이미지 사전 설정 게시가 실패하고 500 오류 코드가 표시됩니다. NPR-29510: CQ-4268659용 핫픽스

### 사이트

* 빈 속성 및 여러 속성이 롤아웃 중에 블루프린트에서 전파되지 않습니다. Live Copy를 블루프린트로 재설정해도 구성 요소에 대해 작동하지 않습니다. NPR-29253: CQ-4264928, CQ-4264926, CQ-4267722용 핫픽스
* CoralUI가 `Multifield`에서 사용되는 경우 multifield 수준이 아닌 구성 요소 수준에서 `fileReferenceParameter`를 저장합니다. NPR-29537: CQ-4266129용 핫픽스
* 일본어 [!DNL Experience Manager] 텍스트 구성 요소 및 텍스트 편집기의 개선 사항입니다. NPR-29785: CQ-4265090용 핫픽스
* 타임워프를 사용하여 복원된 페이지는 버전 지정 시 올바른 그림을 참조해야 합니다. NPR-29431: CQ-4262638용 핫픽스
* 스타일 시스템 노드를 상위에서 하위로 상속하는 데 문제가 있습니다. NPR-29516: CQ-4270330용 핫픽스
* [!DNL Facebook] 인증에 소셜 게시를 설정하는 동안 오류 메시지가 표시됩니다. NPR-29211: CQ-4266630용 핫픽스
* 콘텐츠 조각의 렌더링된 썸네일에 날짜 및 시간 필드에 대한 내부 달력 표현이 표시됩니다. NPR-29531: CQ-4269362용 핫픽스
* Coral2 구현에서 권한 탭을 열면 버튼이 표시되지 않습니다. CQ-4269419용 핫픽스

### 상거래

* 전자 상거래를 위해 레이지 콘텐츠 마이그레이션을 실행할 때의 ConstraintViolationException입니다. NPR-29247: CQ-4264383용 핫픽스

### 콘텐츠 조각 관리

* 달러 `($)` 및 여는 중괄호 `({)` 문자가 있는 콘텐츠 조각을 열 때 구문 분석 오류가 발생합니다. CQ-4270266용 핫픽스

### 경험 구성요소

* [!DNL Experience Manager] 경험 구성 요소를 [!DNL Adobe Target]으로 내보냅니다. CQ-4265469용 핫픽스
* 스마트 이미지를 사용한 타겟으로 경험 구성요소 내보내기가 실패합니다. CQ-4269606용 핫픽스

* 사용자가 카드 보기에서 Omnisearch를 통해 환경 조각을 이동하려고 하면 막다른 상황에 놓이게 됩니다. CQ-4263848용 핫픽스

### WCM - 페이지 편집기

* 올바르지 않은 선택기를 사용할 때 XSS(교차 사이트 스크립팅)이 반영됩니다. CQ-4270397용 핫픽스

### 복제

* 사용자가 제공한 데이터는 `cq/replication/components/agent` 구성 요소에서 출력에 이스케이프되지 않으므로, 저장된 XSS(교차 사이트 스크립팅)에 취약성이 발생합니다. CQ-4266263용 핫픽스

### 워크플로우

* 대화 상자 참가자의 달력 선택기 필드가 손상되었습니다. NPR-29727: CQ-4270423용 핫픽스

### WCM - SPA 편집기

* 원격 끝점에서 사전 렌더링된 콘텐츠 가져오기를 사용하도록 설정되었습니다. CQ-4270238용 핫픽스
* 서버 측에 렌더링된 SPA 템플릿 페이지를 열 때 로그에 경고가 표시됩니다. CQ-4270238용 핫픽스

### WCM - MSM

* [!DNL Experience Manager] 6.4.3으로 업그레이드하면 다중 사이트 관리자가 롤아웃하는 데 시간이 오래 걸립니다. CQ-4271410용 핫픽스

### 통합

* BrightEdge 자격 증명이 실패하고 연결 오류가 발생합니다. NPR-29168: CQ-4265872용 핫픽스

* [!DNL Experience Manager] 실행 구성을 편집하고 저장하려고 하면 예외 메시지가 표시됩니다. NPR-29176: CQ-4265782/CQ-4266153용 핫픽스

### 사용자 인터페이스

* 기초 추적 API의 특정 이벤트를 추적하는 동안 dynamic-UI-states를 사용자 지정 특성으로 추적하는 지원이 추가되었습니다. GRANITE-26283용 핫픽스
* 제출 버튼에 추적 기능을 설정할 수 없습니다. GRANITE-26326용 핫픽스
* 마법사가 버튼에 추적 기능을 설정할 수 없습니다. NPR-29995, NPR-30025: CQ-4264289용 핫픽스

### 커뮤니티

* 구성원 프로필 페이지의 드롭다운에서 새 배지를 정렬할 수 없습니다. NPR-29381: CQ-4267987용 핫픽스
* 중정자 권한이 없는 방문자 및 구성원은 URL을 붙여넣어 승인되지 않은/보류 중인 게시물을 볼 수 있습니다. NPR-29724: CQ-4271124, CQ-4271441용 핫픽스
* 커뮤니티에 대한 사용자 로그인에서 최대 40~50초의 높은 응답 시간이 관찰됩니다. NPR-29677: CQ-4269444용 핫픽스

### 복제

* 복제 에이전트 구성 요소는 중요한 정보를 권한이 없는 사용자에게 공개하는 취약성이 있습니다. NPR-29611: GRANITE-25070용 핫픽스

* [!DNL Brand Portal]에 복제할 때마다 OAuth 중에 세션 누수가 발생합니다. NPR-30001: GRANITE-26196용 핫픽스

### 프로젝트

* [!DNL Experience Manager] Author /content/dam/mac 폴더에서 [!DNL Brand Portal]로 [!DNL Experience Manager Assets]이 게시되지 않습니다. NPR-29819: CQ-4271118용 핫픽스

### 플랫폼

* HtmlLibraryManager가 캐시 무효화에 대한 crx-quickstart의 모든 콘텐츠를 삭제합니다. NPR-29863: GRANITE-26197용 핫픽스

### Felix

* Java11을 사용할 때 메모리 사용량 세부 사항이 시스템 콘솔에 표시되지 않습니다\. NPR-29669

### 양식

[!DNL Experience Manager Forms] 6.5.1.0의 주요 기능은 다음과 같습니다.

* OSGi만 해당: 출력 및 양식 서비스에 새 속성 `PAGECOUNT`가 추가되었습니다.

* OSGI만 해당: 양식 서비스를 사용한 정적 PDF 작성을 지원하도록 설정되었습니다.
* 관리자 및 루트 사용자에 대해 XMLForm.exe에 대한 권한을 사용하도록 설정했습니다.
* Dynamics On-Premise 통합을 위해 ADFS v3.0을 지원하도록 설정했습니다.

#### Forms 추가 기능 패키지

**백엔드 통합**

* 보호된 WSDL(Web Service Definition Language)을 가져오지 못했습니다. NPR-29944: CQ-4270777용 핫픽스
* [!DNL Experience Manager Forms]가 IBM WebSphere에 설치된 경우 SOAP를 기반으로 한 양식 데이터 모델을 작성할 수 없습니다. CQ-4251134용 핫픽스
* Microsoft Dynamics On-Premise 통합을 위한 ADFS(Active Directory Federation Service) v3.0에 대한 지원이 활성화되었습니다. CQ-4270586용 핫픽스
* 데이터 소스의 제목이 변경되면 양식 데이터 모델에 업데이트된 제목이 표시되지 않습니다. CQ-4265599용 핫픽스
* 엔티티 또는 속성의 이름에 하이픈이나 공백을 사용하는 경우 표현식이 그러한 엔티티 및 속성을 평가하지 못합니다. CQ-4225129용 핫픽스

* 콜론이 기본 문자열 출력에 있으면 올바르지 않은 출력이 관찰됩니다. CQ-4260825용 핫픽스

* REST API 출력에서 콘텐츠가 예상되지 않더라도 양식 데이터 모델의 호출 작업으로 인해 오류가 발생합니다. CQ-4268828용 핫픽스

**적응형 양식**

* 레이지 로딩 중에 응용 양식 조각에 새 인스턴스를 추가할 수 없습니다. NPR-29818: CQ-4269875용 핫픽스
* 구성 요소가 레코드 템플릿 문서에 대한 오류를 기록하거나 표시하지 않는지 확인합니다. CQ-4272999용 핫픽스
* 응용 양식에 대한 레이아웃 편집기를 비활성화하는 지원이 추가되었습니다. CQ-4270810용 핫픽스
* [!DNL Experience Manager] 6.5에서 적용형 양식에 대한 확인 단계가 복원되었습니다. CQ-4269583용 핫픽스

* 적용형 양식 필드 유효성 검사 오류로 [!DNL Adobe Sign]이 중단되었습니다. CQ-4269463용 핫픽스
* [!DNL Experience Manager Forms] 인스턴스에 적용형 양식 조각이 20개 이상 있고 모든 양식 조각의 이름이 동일한 문자열로 시작하는 경우 검색 결과에 최근에 작성된 조각 20개만 반환되거나 아무것도 반환되지 않습니다. CQ-4264414, CQ-4264914용 핫픽스

* 응용 양식 앱이 큰 데이터 세트에서 사용되는 경우 성능 문제가 발생합니다. CQ-4235310용 핫픽스

* 게시 인스턴스에서 익명 계정을 통해 액세스한 경우 GuideRuntime 스크립트가 로드되지 않습니다. CQ-4268679용 핫픽스

**양식 - 대화형 통신**

* 대화형 통신 템플릿에 허용되는 구성 요소 목록의 머리글 및 바닥글 구성 요소가 나열되지 않습니다. CQ-4237895용 핫픽스
* 이미지 필드를 포함하는 대화형 통신 인쇄 템플릿을 작성하면 차트 제목이 공백으로 설정됩니다. CQ-4264772용 핫픽스
* 차트의 선 색상이 삭제되는 경우 정의되지 않음으로 설정됩니다. CQ-4264762용 핫픽스
* 문서 조각에서 수행한 레이아웃 레이어 변경 사항은 변경 사항을 계속 동기화할 경우 사라집니다. CQ-4266054용 핫픽스
* 텍스트 필드에 바인딩된 문서 조각 내의 양식 데이터 모델 요소는 상속 아이콘이 표시되지 않으며 바인딩을 허용합니다. CQ-4261089용 핫픽스
* 인쇄 채널 렌더링 API에 API의 매개 변수로 데이터를 전달하는 옵션이 없습니다. CQ-4263540용 핫픽스
* 문자열 필드/변수에 대한 바인딩 형식이 텍스트 조각에서 없음/데이터 모델 개체로 변경되면 에이전트가 편집 가능 확인란이 선택 취소되므로 에이전트 설정이 표시되지 않습니다. CQ-4261953용 핫픽스
* 에이전트 UI 제출 시 결과 웹 데이터 json 파일은 상속이 취소된 바인딩되지 않은 필드에 대한 정보를 저장합니다. CQ-4265621용 핫픽스

**양식 - 워크플로우**

* 응용 양식 앱의 보낼 편지함에서 양식을 다시 제출하면 데이터가 손실됩니다. NPR-28345: CQ-4260929용 핫픽스
* 변수가 아닌 사례에 대해 저장하는 동안 문서가 닫히지 않습니다. CQ-4269784용 핫픽스
* 응용 양식 앱에서 Microsoft Windows 8.1에 대한 지원이 삭제되었습니다. CQ-4265274용 핫픽스
* 2MB 이상의 이미지가 [!DNL Experience Manager Forms] 앱의 Android 버전에서 양식에 대한 필드 수준의 첨부 파일로 첨부된 경우 앱이 충돌합니다. CQ-4265578용 핫픽스

* 작업 지정에서 대화형 통신 인쇄 채널에 대한 미리 채우기 옵션이 활성화되었습니다. CQ-4265577용 핫픽스
* 사용자는 작업이 지정된 그룹의 구성원이 될 때까지 공유 작업을 볼 수 없습니다. CQ-4248733용 핫픽스
* 응용 양식 앱에서 JEE 애플리케이션 저장 또는 제출은 Windows에서 차단됩니다. CQ-4268704용 핫픽스
* 양식 데이터 모델 변수와 연관된 양식 데이터 모델이 표시되지 않습니다. CQ-4266554용 핫픽스
* 변수 지원을 사용한 문서 기호의 상태 변수를 지원하지 않습니다. CQ-4266312용 핫픽스
* 모음 문자로 인해 작업 영역에서 제출되지 않습니다. CQ-4263172용 핫픽스
* 업그레이드된 설정에서, 워크플로우가 편집을 위해 열려 있는 경우 감시 폴더 UI(사용자 인터페이스)의 워크플로우 이름 대신 오류가 표시됩니다. CQ-4238579용 핫픽스

**양식 - 관리**

* xsd 또는 schema.json이 아닌 확장이 업로드되면 업로드가 발생하지 않고 오류 메시지가 생성되지 않습니다. CQ-4266716용 핫픽스

**양식 - 서신 관리**

* [!DNL Experience Manager Forms] 6.5 CCR UI(Create Correspondence UI)에서 [!DNL Experience Manager Forms] 6.3으로 작성된 서신을 열지 못합니다. CQ-4266392에 대한 핫픽스
* DDE 데이터 유형이 숫자 유형인 경우 XDP의 Sum 함수가 작동하지 않습니다. CQ-4227403용 핫픽스
* 자산이 게시될 때 마지막 수정 시간이 업데이트되지 않으므로 메모리 내 캐시 무효화 로직의 문자가 업데이트됩니다. CQ-4250465용 핫픽스
* 문서 조각, DD 및 문자를 게시할 수 없습니다. CQ-4272893용 핫픽스

#### Forms JEE 설치 프로그램

**PDF 생성기**

* 64비트 JDK로 인해 CAD 파일이 PDF로 변환되지 않습니다. NPR-29924, NPR-29925: CQ-4272113용 핫픽스
* HTMLtoPDF 변환을 위해 PhantomJS 이름이 WebToPDF로 대체되었습니다. NPR-29933: CQ-4234545용 핫픽스
* zip 파일을 PDF로 변환하는 중에 오류가 발생했습니다. CQ-4268628용 핫픽스

**양식 - 디자이너**

* [!DNL Experience Manager Forms Designer]를 사용하여 작성된 정적 PDF에서 전체 액세스 가능성 검사를 수행하면 누락된 언어 속성으로 인해 기본 언어 검사가 실패합니다. CQ-4272923, CQ-4271002용 핫픽스

**양식 - 문서 보안**

* HSM(하드웨어 보안 모듈)을 사용한 디지털 서명이 Java 11 및 Java 8이 설치된 OSGi Linux에서 작동하지 않습니다\. NPR-29838: CQ-4270441용 핫픽스
* HSM(하드웨어 보안 모듈)을 사용한 디지털 서명이 JEE Linux 및 모든 지원 앱 서버(예: JBoss 및 Websphere)에서 작동하지 않습니다. NPR-29839: CQ-4266721용 핫픽스
* PAdES(PDF 고급 전자 서명)를 사용하여 PDF에서 서명을 확인하면 InvalidOperationException이 생성됩니다. NPR-29842: CQ-4244837용 핫픽스
* Office 2019에 대한 문서 보안 확장 지원이 추가되었습니다\. CQ-4254369, CQ-4259764용 핫픽스

**양식 - 문서 서비스**

* 양식 필드에 모양 사전이 없기 때문에 PDF가 PDF/A-1b로 변환되지 않습니다. NPR-29940: CQ-4269618용 핫픽스

* OSGi: 렌더링 중에 생성된 페이지 수를 확인할 수 없습니다. NPR-28922: CQ-4270870용 핫픽스
* [!DNL Experience Manager Forms OSGi]에서 양식 서비스를 사용하는 정적 PDF에 대한 지원을 사용하도록 설정되었습니다. NPR-28572: CQ-4270869용 핫픽스
* XMLForm.exe에 대한 권한을 변경할 수 없습니다. NPR-29828, NPR-29237: Q-4267080용 핫픽스
* [!DNL Experience Manager Forms] 서버의 출력 모듈에서 작성된 정적 PDF가 언어 속성/태그를 작성된 문서의 언어로 채우지 않습니다. NPR-27332: CQ-4271002용 핫픽스

**양식 - 기초 JEE**

* 최종 아티팩트에서 사용할 수 없는 pdfg_srt로 인해 설치 프로그램에 오류가 발생합니다. NPR-29854: CQ-4270137용 핫픽스
* LCBackupMode.sh가 작동하지 않습니다. NPR-29840: CQ-4269424용 핫픽스
* WebSphere의 UI(사용자 인터페이스)에서 UDP 포트 참조를 제거해야 합니다. CQ-4264782용 핫픽스

### 기능 팩이 포함됨

#### 자산 - 포함

* [!DNL Experience Manager Assets]에 대한 다중 사이트 관리자 지원이 활성화되었습니다. 자세한 내용은 [Experience Manager Assets에 MSM을 사용하여 자산 재사용](https://docs.adobe.com/content/help/en/experience-manager-65/assets/using/reuse-assets-using-msm.html)을 참조하십시오. NPR-29199: CQ-4259922용 핫픽스

#### 사이트 - 포함

* [!DNL Experience Manager] 경험 구성 요소를 [!DNL Adobe Target]으로 내보냅니다. 자세한 내용은 [경험 구성요소 링크 재작성기 공급자 - HTML](https://helpx.adobe.com/kr/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML)을 참조하십시오. CQ-4265469용 핫픽스

#### 양식 - 문서 서비스 - 포함

* OSGi만 해당: 출력 및 양식 서비스에 새 속성 PAGECOUNT가 추가되었습니다.. NPR-28922: CQ-4270870용 핫픽스
* OSGI만 해당: 양식 서비스를 사용한 정적 PDF 작성을 지원하도록 설정되었습니다. NPR-28572: CQ-4270869용 핫픽스
* 관리자 및 루트 사용자에 대해 XMLForm.exe에 대한 권한을 사용하도록 설정했습니다. NPR-29237: CQ-4267080용 핫픽스

### OSGi 번들 및 콘텐츠 패키지

다음 텍스트 문서에는 [!DNL Experience Manager] 6.5.1.0에 포함된 OSGi 번들 및 컨텐츠 패키지 목록이 나와 있습니다.

[!DNL Experience Manager] 6.5.1.0에 포함된 OSGi 번들 목록

[파일 가져오기](assets/6_5-bundle-list.txt)

[!DNL Experience Manager] 6.5.1.0에 포함된 컨텐츠 패키지 목록

[파일 가져오기](assets/6_5-content-package-list.txt)
