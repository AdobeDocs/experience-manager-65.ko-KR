---
title: '[!DNL Adobe Experience Manager] 6.5 서비스 팩 릴리스 노트.'
description: Release notes specific to [!DNL Adobe Experience Manager] 6.5 Service Pack 6.
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: b23b66e9d57742f6771bc4b26753a47b334e06bc
workflow-type: tm+mt
source-wordcount: '4557'
ht-degree: 23%

---


# [!DNL Adobe Experience Manager] 6.5 서비스 팩 릴리스 노트 {#aem-service-pack-release-notes}

## 릴리스 정보 {#release-information}

| 제품 | Adobe Experience Manager 6.5 |
| -------- | ---------------------------- |
| 버전 | 6.5.6.0 |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2020년 9월 03일 |
| 다운로드 URL | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.6-1.0.zip) |

## Adobe Experience Manager 6.5.6.0에 포함된 제품 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.6.0은 **2019년 4월** 6.5 릴리스의 공식 출시 이후 릴리스된 새로운 기능, 주요 고객이 요청한 향상된 기능 및 성능, 안정성, 보안 개선 사항이 포함된 중요한 업데이트입니다. Adobe Experience Manager 6.5 맨 위에 설치할 수 있습니다.

Adobe Experience Manager 6.5.6.0에 도입된 주요 기능 및 개선 사항은 다음과 같습니다.

* 빠른 게시 [!DNL Experience Manager] 또는 게시 관리 [!DNL Dynamic Media] 마법사를 사용하여 선택적으로 자산 [!UICONTROL 을 게시하거나 게시] 를 [!UICONTROL 취소할 수] 있습니다.

* 사용자 [!DNL Dynamic Media] 인터페이스를 사용하여 CDN(Content Delivery Network) 캐시된 컨텐츠를 무효화합니다.

* 이제 프록시 서버를 통해 브랜드 포털에서 Experience Manager 자산에 자산 기여도 폴더를 게시하는 것도 지원됩니다.

* 이제 개인 폴더의 자동 생성 그룹이 비공개 폴더를 삭제할 때 정리됩니다 [!DNL Experience Manager Assets].

* 비디오 [!UICONTROL 뷰어] 사전 설정 편집기의 수정자에 대한 설명은 에서 업데이트되었습니다 [!DNL Dynamic Media].

* 커넥터의 상태를 반영하도록 새 회사 설정이 [!DNL Dynamic Media] 제공됩니다.

* 사용자가 축소판만 만들고 페이지 추출 및 키워드 추출 `test` 을 건너뛸 수 있도록 Dynamic Media `aiprocess` `Thumbnail``Rasterize` 의 이전 버전에서 기본 옵션을 로 업데이트하고 업데이트합니다.

* [클라이언트에서 응용 양식을 미리 채웁니다](../../help/forms/using/prepopulate-adaptive-form-fields.md#prefill-at-client).

* [양방향 SSL 구현을 통해 서버에서 RESTful API와 양식 데이터 모델 통합](../../help/forms/using/configure-data-sources.md)

* [번역된 적응형 양식 페이지에 대한 캐싱 기능이 향상되었습니다](../../help/forms/using/configure-adaptive-forms-cache.md).

* 자동화된 Forms 전환 서비스에서 [Adobe Sign 텍스트 태그 지원](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html).

* 색상 있는 양식을 [적응형 양식으로](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html) 변환할 수 있도록 지원합니다 [!DNL Automated Forms Conversion service].

* SMB 2 및 SMB 3 프로토콜 지원

* 내장된 저장소(Apache Jackrabbit Oak)가 버전 1.22.4으로 업데이트되었습니다.

Experience Manager 6.5.6.0에 도입된 기능과 개선 사항의 전체 목록은 Adobe Experience Manager 6.5 서비스 팩 6의 [새로운 기능을 참조하십시오](new-features-latest-service-pack.md).

다음은 [!DNL Experience Manager] 6.5.6.0 릴리스에서 제공된 수정 사항 목록입니다.

### [!DNL Sites] {#sites-6560}

* 또는 [!DNL Sites] 에서 프로젝트를 선택하고 [!DNL Screens]관리 발행물을 클릭합니다 . 사용자 인터페이스 오류로 인해 게시 [!UICONTROL 관리] 마법사를 진행할 수 없습니다. 특히 [!UICONTROL 게시] 옵션이 작동하지 않습니다(NPR-34099).
* 상속 [!UICONTROL 취소] 또는 상속 옵션 비활성화(NPR-34097)를 선택 취소한 후 iParsys(상속된 단락 시스템)의 위치가 원래 기본 위치로 되돌려지지  않습니다.
* 롤아웃 구성 `RolloutConfigManagerFactoryImpl` 을 로드할 수 없는 경우 누락된 구성을 로드하지 않습니다. 캐시된 구성을 반환합니다(NPR-34092).
* 텍스트 코어 구성 요소에서 소스 HTML 편집 옵션을 사용한 후 태그의 `em` 클래스가 제거됩니다(NPR-34081).
* Experience Manager 6.3.3에서 Experience Manager 6.5.3으로 업그레이드한 후, 롤아웃 프로세스는 훨씬 더 오래 걸리고 시간 초과 오류(NPR-34049)로 롤아웃 실패.
* 속성 값을 다시 인코딩하지 `htmlwriter` 않습니다. XF 마크업에 있는 마크업은 디코딩된 속성 값(즉, `"` 대신)으로 내보내집니다 `&#34`. 내보낸 XF를 사용하는 Visual Experience Composer의 Target에 문제가 발생합니다(NPR-34048).
* 페이지를 이동할 때 이유 [!DNL Experience Manager Sites]로 버전 생성 실패를 캡처하기 위해 로깅을 개선하십시오(NPR-34014).
* 모든 텍스트를 제거하면 단락 태그도 제거됩니다(NPR-33976). [!DNL Rich Text Editor]
* 페이지(클래식 UI에서)를 `siteadmin` 열거나 새로 고치면 `New` 메뉴의 옵션이 비활성화됩니다(NPR-33949).

   ![클래식 UI에서 메뉴 누락 문제를 설명하는 스크린샷](assets/33949_missing_menu.png)

* A는 실패 [!DNL Content Fragment] 로 사용할 수 `TemplatedResource` `ContentFragmentUsePojo` 없습니다(NPR-33911).
* 동기 및 비동기 이동 작업은 동시 전송으로 인해 오류를 초래할 수 있습니다. 페이지 이동 작업은 동기 이동으로만 제한됩니다. 페이지 동시 이동을 방지합니다(NPR-33875).
* [!UICONTROL 게시] 관리 작업을 통해 작성자에서 게시 인스턴스로 컨텐츠를 복제하지 못하고 JavaScript 오류를 생성합니다(NPR-33872).
* 버전을 만들기 위해 여러 페이지 또는 자산을 선택한 경우, 새 버전은 마지막으로 선택한 페이지 또는 자산에 대해서만 만들어집니다(NPR-33866).
* Live Copy가 있는 블루프린트 페이지를 다른 폴더로 이동합니다. 원래 폴더로 이동할 때 이동 작업이 오류 없이 실패합니다(NPR-33864).
* [콘솔]에서 웹 페이지의 이름을 변경하는 데 이동 작업을 사용하면 마법사의 마지막 단계에서 겹치는 대화 상자 두 개를 [!DNL Sites] 표시합니다(NPR-33831).

   ![중복 이동 대화 상자의 NPR-33831 문제를 설명하는 스크린샷](assets/33831_rename_dialog.png)

* 복사본의 `cq:acLinks` 및 `cq:acUUID` [!DNL Adobe Campaign] 속성은 복사 및 붙여넣기 작업 중 제거됩니다(NPR-33794).
* 분리된 상위 Live Copy의 하위 페이지에서 롤아웃을 시도하면 [!DNL Experience Manager] null 포인터 예외를 생성합니다(NPR-33676).
* 레이아웃 컨테이너의 [!DNL RTE] 구성 요소는 레이아웃 컨테이너를 복사하여 페이지에 다시 붙여넣을 때 표시되지 않습니다. 구성 요소는 편집할 수 없지만 페이지 새로 고침 시 표시됩니다(NPR-33662). [!DNL RTE]
* 서로 다른 중단점(중간 및 큰)에 대한 레이아웃 구성 요소의 크기를 조정할 때 레이아웃이 예상대로 작동하지 않습니다(NPR-33608).
* 인라인 편집 모드에서 이미지 [!DNL RTE]를 드래그하면 텍스트 구성 요소에 사용할 수 없습니다(NPR-33602).
* 페이지 이름과 동일한 이름으로 블루프린트 페이지에 구성 요소를 만들 수 있습니다. 롤아웃 중에 구성 요소 `_msm_moved` 의 이름을 바꾸어야 합니다. 구성 요소는 [!UICONTROL 단락 시스템] (NPR-33535)의 끝으로 이동합니다.
* offTime 또는 onTime이 여러 페이지 또는 자산에 설정되어 있을 때, 시작 및 종료 시 리소스를 많이 사용하므로 시스템이 느려집니다(NPR-33482).
* CRUD 권한이 있는 사용자가 폴더를 삭제할 수 `/content/experience-fragment` 없습니다(NPR-33436).
* 섹션의 상위 폴더에서 [!UICONTROL Adobe Target 내보내기 형식] 옵션으로 [!UICONTROL HTML &amp; JSON을 선택할] 수 [!DNL Experience Fragments] 있습니다. 이 상위 폴더의 하위 폴더에 대해 터치 활성화 UI에 동일한 속성이 표시됩니다. 그러나 CRXDE에서는 `cq:adobeTargetExportFormat``html,json` 표시되는 대신 HTML만 표시합니다(NPR-33423).
* 페이지 별칭에서 게시 또는 게시 취소는 지원되지 않습니다. 그렇지 않은 것으로 보이는 옵션을 제거합니다(NPR-33415).
* 특정 태그는 한 위치에서 다른 위치로 이동할 수 있습니다 [!DNL Experience Manager]. 또한 이동 전후에 다른 페이지에 적용할 수도 있습니다. 페이지의 속성을 편집할 때 태그가 동일하더라도 편집할 태그가 표시되지 않습니다(NPR-33353).
* 여러 레이아웃 컨테이너가 포함된 템플릿에서 레이아웃 컨테이너를 삭제하면 페이지 템플릿이 제대로 렌더링되지 않습니다(NPR-33347).
* 템플릿 편집기에서 아래에 10000개 이상의 페이지가 사용되는 템플릿을 삭제하려고 합니다 `/content/`. 오류 메시지 없이 오류가 표시됩니다(NPR-33312).
* 앵커 [!DNL Experience Manager] `PageRedirectServlets` 가 있는 페이지로 리디렉션은 URL 조각 또는 앵커 뒤에 쿼리 문자열을 삽입하므로 작성자 인스턴스에서 작동하지 않습니다(NPR-34288).
* 캠페인을 만들 수 없는 구조가 `/content/campaign` 됩니다. [!UICONTROL 브랜드] 만들기 옵션은 [!UICONTROL 만들기] 옵션(NPR-34113)이 없으므로 [!UICONTROL 오퍼 및 활동] 을 만들 수없는새 브랜드에 적용됩니다.
* 페이지 [!DNL Live Copy] 를 일시 중단할 수 있으며 상속은 편집기 모드에서 보듯이 끊깁니다. 페이지 속성에서, 상속을 나타내는 아이콘은 상속이 존재하며 끊어지지 않았음을 잘못 나타냅니다(NPR-34017).
* 참조가 많은 페이지는 비동기식으로 이동할 수 없으며 이동 작업이 실패하는 경우가 있습니다(CQ-4297969).
* 작성하는 동안 URL에 `/` 문자가 포함된 웹 페이지가 응답하지 않습니다. 작성하는 동안 구성 요소가 추가되면 CPU 사용이 증가하고 브라우저가 응답을 중지합니다(CQ-4295749).
* 검색 모드에서는 유형/크기 메뉴 옵션에서 선택한 값을 내레이트하지 않습니다. 시각적 포커스가 선택한 요소에 있지 않습니다. 화면 판독기를 사용하는 사용자는 찾아보기 모드를 사용할 수 없습니다(CQ-4294993).
* 웹 페이지를 만들 때 사용자는 컨텐츠 페이지 [!UICONTROL 템플릿을 선택할 수] 있습니다. 소셜 [!UICONTROL 미디어] 탭에서 기본 설정 XF [!UICONTROL 변형을 선택합니다]. NVDA 검색 모드에서 경험 조각을 선택하려면 키보드 키를 사용할 수 없습니다(CQ-4292669).
* handlebars 라이브러리를 더 안전한 v4.7.3(NPR-34484)으로 업데이트했습니다.

### [!DNL Assets] {#assets-6560}

**Experience Manager Assets의 액세스 가능성이 개선되었습니다**

* 이제 사용자는 키보드 키를 사용하여 에셋 [!UICONTROL 참조] 목록(NPR-34115)의 인터랙티브한 유저 인터페이스 옵션에 액세스하고 집중할 수 있습니다.

* 이제 화면 판독기가 검색 페이지에서 설명 메시지의 의도된 동작을 발표합니다(NPR-34104).

* 이제 검색 페이지 및 검색 결과 페이지에 화면 판독기 사용자를 더 잘 이해할 수 있는 정보가 포함된 제목이 추가되었습니다(NPR-34093).

* 이제 화면 판독기가 자산 [!UICONTROL 속성] 페이지의 [!UICONTROL 기본] 탭에서 선택한 태그를 삭제할 수 있는 옵션을 발표합니다(NPR-33972).

* 이제 목록 보기의 각 행에 있는 요소가 화면 판독기에서 동일한 행의 요소로 선언됩니다(NPR-33932).

* 이제 `Tab` 키를 사용하여 탐색할 때 사용자의 포커스가 버전 미리 보기의 닫기 옵션으로 이동합니다(NPR-33863).

* 이제 Omnisearch가 닫힌 후 사용자 포커스가 검색 아이콘으로 이동합니다(NPR-33705).

* 이제 실행 가능한 유저 인터페이스 옵션이 키보드 키를 사용하여 탐색할 때 향상된 대비 기능을 사용하여 보다 눈에 잘 띄는 초점을 갖게 되었습니다. 키보드 사용자는 초점을 맞춘 영역을 식별할 수 있습니다(NPR-33542).

* 키보드를 사용하는 드래그 기능이 이제 화면 판독기의 검색 모드에서 [!UICONTROL 메타데이터 스키마] 편집기에서 작동합니다(CQ-4296326).

* 링크 공유 대화 상자에서 찾아보기 모드에서 탐색할 때 화면 판독기가

   * 대화 상자가 로드되는 즉시 테이블 정보를 분류하지 않습니다.

   * 나열된 모든 자동 제안 항목으로 이동할 수 있습니다.

   * 이메일 주소/검색 [!UICONTROL 추가에 대해 표시되는 자동 제안] 내레이션이 표시됩니다(CQ-4294232).

* 카드 보기에서 빠른 작업 아이콘을 제거하기 위해 `Esc` 키를 사용해도 마지막 초점을 맞춘 항목에서 키보드 포커스가 제거되는 문제가 해결되었습니다(CQ-4293554).

* 사용자 인터페이스에 대한 대화형 옵션의 경우 화면 판독기는 이제 아이콘의 문자 이름이 아닌 해당 목적을 알립니다(CQ-4272943).

* 이제 키보드 포커스를 [!UICONTROL 플라이아웃], [!UICONTROL Shopperable][!UICONTROL , Zoom]_Dark [!UICONTROL , Zoom_darkDark가 움직이며 Zoom_lightZoomLightlight, Zoom_zoomLightCumeline으로 이동하도록 성공Keyboard focus를 사용하여 탭합니다. SpiboxSpirindesign의 에셋의 세부 정보를 사용하여 키를 탐색할 때Spyline에서를 사용하여 키보드 포커스를 탐색하는 경우SpandronSpandroidSpandroidSpiranSpirnCumeline에서를를의 기본에서]  [!DNL Dynamic Media] , SpiranSpirn의 기본의 기본의 기본의 기본를를에서 사용자를를를를를 사용자를에서에서SpandroidSpandroidSpandroid를q-4290605).

* [!UICONTROL 자산 속성] 페이지의 저장 [!UICONTROL 및 닫기] 옵션은 키보드 키(NPR-34107)를 사용하여 액세스할 수 있습니다.

* 이제 로그인 페이지의 잘못된 사용자 이름과 암호 조합으로 인한 오류 메시지가 오류가 발생할 때마다 화면 판독기에서 알려줍니다(NPR-33722).

* 헤더 [!DNL Experience Manager] 섹션에서 검색 모드로 탐색할 때 화면 판독기에서 이제

   * Omnisearch에서 검색할 [!UICONTROL 유형] 제안 자동 편집

   * [ [!UICONTROL 솔루션]], [도움말 , [받은 편지함]] 및 [ [!UICONTROL 사용자]옵션]에 대한 상태가 확장되거나 축소되는 경우 [!UICONTROL 는] 옵션으로 표시됩니다.

   * 사용자가 도움말 [!UICONTROL 검색] 옵션 아래의 도움말 [!UICONTROL 필드] 에서 검색 문자열을 입력할 때 표시되는 도움말 [!UICONTROL 상태] 메시지.

   ![헤더의 도움말 메뉴](assets/Help_aem_header.png)

   *그림: [!UICONTROL 도움말] 메뉴에서 [!UICONTROL 도움말] 검색*

   * 잘못된 값이 사용자 [!UICONTROL 옵션 아래의 가장 대상] 필드  에 입력되고 포커스가 텍스트 필드로 올바르게 이동하는 경우 오류 메시지(NPR-33804).

   ![헤더의 사용자 메뉴](assets/User_aem_header.png)

   *그림: [!UICONTROL 헤더의] 사용자  메뉴의 가장 대상 필드*

* 이제 사용자는 다음 내의 키보드를 사용하여 포커스를 변경할 수 있습니다.

   * [!UICONTROL [링크 공유] 대화 상자의 [이메일 주소] 검색/ [!UICONTROL 추가]] 필드

   * [!UICONTROL 폴더 속성] 의 [!UICONTROL 권한] 탭 [!UICONTROL 에 있는 폐쇄된 사용자 그룹] 아래의 사용자 또는 그룹 [!UICONTROL 필드] 추가(NPR-34452).

**Experience Manager Assets에서 해결된 문제**

[!DNL Adobe Experience Manager] 6.5.6.0 [!DNL Assets] 은 다음 문제에 대한 수정 사항을 제공합니다.

* 자산의 타임라인에서 주석을 선택하면 강조 표시되지 않습니다(CQ-4302422).

* 템플릿을 사용하여 만든 마케팅 자료 자산(예: 브로셔, 전단지 및 명함)의 미리 보기에는 라인 구분과 단락 나누기가 표시되지 않습니다(NPR-34268). [!DNL Adobe InDesign]

* 텍스트 추출 및 업로드된 PDF 파일에 대한 전체 텍스트 검색이 작동하지 않습니다(NPR-34164). 이를 해결하려면 서비스 팩 6을 설치한 후 배포를 다시 [!DNL sAdobe Experience Manager] 시작하십시오.

* 다중 페이지 자산의 타임라인에는 특정 하위 자산에 대한 주석을 표시하는 대신 타임라인 보기에서 자산을 검색할 때 모든 하위 자산에 적용된 주석이 표시됩니다(NPR-34100).

* 폴더에 JavaScript, CSS 또는 JSON 파일 형식(NPR-34090)의 리소스가 포함되어 있는 경우 [!UICONTROL 자산] 폴더가 게시 관리 옵션을 사용하여 게시되지 않습니다.

* Omnisearch에서 적용된 태그 또는 필터를 선택 해제하거나 제거하면 검색 시간이 늘어날 검색 쿼리를 여러 번 실행합니다(NPR-34078).

* 워크플로우(폴더의 자산)가 진행 중이거나 보류 중인 경우 워크플로우가 완료되거나 종료될 때까지 페이지가 다시 로드됩니다. 따라서 작성자는 아래로 스크롤해야 하는 폴더의 해당 에셋에 대해 작업할 수 없습니다(NPR-33986).

* 사용자가 게시된 자산을 새 위치로 이동하면 [다시 게시] 옵션이 선택 해제되어 있어도 자산이 [!UICONTROL 다시] 게시됩니다. 이로 인해 게시 인스턴스에 많은 고아 자산이 배치됩니다. 하지만 기본적으로 게시된 자산에 대한 이동 작업이 자동으로 게시 취소됩니다.이 자산은 작성자가 자산을 이동할 때 [!UICONTROL 재게시] 옵션을 선택하면 다시 게시됩니다(NPR-33934).

* 컬렉션의 자산에 대한 [!UICONTROL 자산] 이동 페이지는 조정 [!UICONTROL /재게시] 옵션과 같은 일부 HTML 콘텐츠를 로드하지않습니다. 따라서 사용자는 이동 작업을 완료할 수 없습니다(NPR-33860).

* 자산을 이동하고 이동한 자산의 이름과 제목에 특수 문자를 추가하면 자산의 새 위치에 추가 폴더(같은 이름)가 만들어집니다(NPR-33826).

* [!UICONTROL [] 다운로드] 대화 상자(NPR-33730)에서 [ [!UICONTROL 이메일] ] [!UICONTROL 옵션] 을 선택하면 자산에 대한 다운로드단추가 비활성화됩니다.

* 벌크 메타데이터 편집(NPR-33723)과 같은 자산에서 벌크 작업을 수행할 때 &#39;Request-URI too long&#39; 오류가 발생합니다.

* JavaScript 오류가 발견되었으며, 업로드된 JSON 파일에 [!UICONTROL 공간 또는 특수 문자(NPR-33712)가 있는 경우, 사용자는] 폴더 메타데이터 스키마 양식 편집기에서 [!UICONTROL JSON 경로] 기능을 통해 추가 기능을 통해 드롭다운 [!UICONTROL 필드에서 생성된 선택 사항을 선택하거나 삭제할 수 없습니다].

* 자산의 정적 표현물은 에서 [!UICONTROL 열기] 옵션 [!DNL desktop app] 을 사용하여 [!DNL Adobe Asset Link] 자산을 업데이트하거나 [!DNL Adobe Experience Manager] 다음으로(CQ-4296279)으로 다시 동기화될 때업데이트되지않습니다.

* 열 보기에서는 자산 세트에 대한 이동 작업도 해당 자산에 대해 [!UICONTROL 필터] 옵션을 사용하기 전에 선택한 자산을 이동합니다. 필터 옵션 [!UICONTROL 을 사용하면] 이전 선택 사항이 선택 취소됩니다(NPR-34018).

* 백슬래시는 이름에 특수 문자가 있는 자산의 검색 제안에서 특수 문자 앞에 추가됩니다(NPR-33834).

* 폴더 메타데이터 스키마 양식 [!UICONTROL 에서 드롭다운에 대한 규칙을 만들 때 사용자는]필드 선택  열에서 값을 선택할 수 없습니다(CQ-4297530).

* 6.5 서비스 팩 5 또는 이전 버전(NPR-34532)을 설치할 때 `/var/workflow/models/dam`만든 에셋 사용자 정의 워크플로우 모델의 런타임 사본이 [!DNL Experience Manager] [!DNL Experience Manager] 삭제됩니다. 런타임 사본을 검색하려면 HTTP API를 사용하여 워크플로우 모델의 디자인 타임 사본을 런타임 복사본과 동기화합니다.
   `<designModelPath>/jcr:content.generate.json`.

**다이내믹 미디어에서 해결된 문제**

* 사용자가 비디오 프로필을 만든 후 편집 내용에서 인코딩 설정을 정의하면 스마트 자르기 설정이 비디오 프로필에서 제거됩니다(CQ-4299177).

* 사용자가 자산 세부 사항 페이지(NPR-34235)에서 사이드 레일 옵션( [!UICONTROL 예:]개요 [!UICONTROL ,]타임라인 [!UICONTROL ,]뷰어)을 전환하면 에셋이 페이지 로드 시 깜박입니다.

* 재처리 작업에서 다음 문제가 관찰됩니다.

   * 재처리 작업에 의해 반환된 작업 핸들에 작업 ID가 없습니다.

   * 비디오 로그의 파일 이름만 재처리하며 전체 경로가 아닙니다.

   * 재처리 작업에는 자산 유형을 정적으로 설정하는 옵션이 없습니다.

   * `ExcludeFromAVS` 옵션이 제공되지 않습니다(CQ-4298401).

* 이미지 프로필을 여러 종횡비(예: 11)가 있는 폴더에 추가할 때 스마트 자르기 기능이 실패하므로 오류가 발생합니다(NPR-34082).

* DAM 자산 업데이트 워크플로우는 사용자가 Dynamic Media Scene7으로 구성된 [!UICONTROL 도구] 의 워크플로우 [!UICONTROL 탭] 에서 [!UICONTROL 워크플로우][!DNL Adobe Experience Manager] 페이지에서아래로 스크롤할 때트리거됩니다(CQ-429727).

* 뷰어 사전 설정 편집기의 [!UICONTROL 동작] 탭 [!UICONTROL 의 심볼은] 지역화되지 않습니다(CQ-4299026).

* 뷰어가 응답형 모드인 경우 기본 보기에는 뷰어에 맞지 않는 잘못된 레이아웃으로 이미지가 표시됩니다(CQ-4298293).

* Adobe Experience Manager의 이미지 사전 설정 변경 사항은 [!UICONTROL Scene7] Publishing System(CQ-4299713)과 동기화되지 않습니다.

### [!DNL Commerce] {#commerce-6560}

* 자산을 이동할 때 제품에서 에셋으로 연결되는 링크는 리팩토링되지 않습니다(NPR-34098).

### 플랫폼 {#platform-6560}

* 업그레이드된 Experience Manager 인스턴스에서 진단 도구를 사용하여 로그를 다운로드할 수 없습니다(NPR-34336).
* 특정 버전의 `cq-wcm-api` foundation 패키지에 종속되어 오류로 인해 업그레이드에 실패했습니다(CQ-4300520).
* 기본 에이전트(게시) 구성에 대한 **[!UICONTROL 연결 시간]** 제한 **[!UICONTROL 및]** 소켓 시간초과설정에 대한 기본값이 지정되지 않았습니다(NPR-33707).
* 아래의 매핑 구성에 대한 업데이트는 사이트 페이지에 `/etc/map.publish` 반영되지 않습니다(NPR-34015).
* [API 참조 설명서에는 패키지](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html) 관련 `com.day.cq.tagging` 설명서가 포함되어 있지 않습니다(CQ-4295864).

### 사용자 인터페이스 {#ui-6560}

* 오프로드 브라우저 인터페이스에는 일부 작업 항목이 표시되지 않습니다(NPR-34308).
* 구성 [브라우저](/help/sites-administering/configurations.md) 인터페이스에 모든 구성이 표시되지 않습니다(NPR-33644).
* 가장 `Esc` 가장할 사용자를 검색할 때 키를 누르면 사용자 목록 대신 **[!UICONTROL 사용자]** 대화 상자가 닫힙니다(NPR-34084).

### 통합 {#integrations-6560}

* 이름이 긴 활동은 [!DNL Adobe Target] (NPR-34254)와 동기화되지 않습니다.

### 번역 프로젝트 {#translation-6560}

* 사용자의 특수 문자(NPR-33828)가 `authorizableID` 포함된 경우 번역 프로젝트가 생성되지 않습니다.

### 슬링 {#sling-6560}

* 상태 확인 및 패턴 탐지기 기능이 중복되었습니다. 그 결과, Heath 검사가 제품에서 제거됩니다(NPR-33928).

### WCM {#wcm-6560}

* 기본 구성 요소 - 페이지에 기초 이미지 구성 요소를 추가하고 이미지를 참조할 때 `Undo` 작업이 작동하지 않습니다(NPR-34516).

* 페이지 이동 작업을 사용할 수 없습니다(CQ-4303028).

### [!DNL Communities] {#communities-6560}

* 소셜 미디어에서 게시물을 공유하면 오래된 옵션인 Google+(NPR-33877)가 표시됩니다.

* 커뮤니티 구성원이 그룹 템플릿 또는 기타 그룹 기능 설정을 수정할 수 없습니다(NPR-33530).

* 이미지의 하이퍼링크 태그가 포럼 게시물에서 제대로 생성되지 않습니다(NPR-33464).

* 접근성 오류는 커뮤니티 할당 기능(NPR-33442)에서 식별됩니다.

* 관리 콘솔을 통해 추가된 커뮤니티 그룹의 기존 사용자는 커뮤니티 그룹 콘솔의 수정 사항에 대한 사용자 목록에서 제거됩니다(NPR-34315).

<!--
* Tag filters are vulnerable to sensitive information disclosure (NPR-33868).
-->

### [!DNL Forms] {#forms-6560}

>[!NOTE]
>
>[!DNL Experience Manager] 서비스 팩에는 [!DNL Forms] 수정 사항이 포함되어 있지 않습니다. 이러한 수정 사항은 별도의 [!DNL Forms] 추가 기능 패키지를 사용하여 전달됩니다. 또한, JEE의 [!DNL Experience Manager Forms]에 대한 수정 사항이 포함된 누적 설치 프로그램이 릴리스됩니다. 자세한 내용은 [AEM Forms 추가 기능 설치](#install-aem-forms-add-on-package) 및 [AEM Forms JEE 설치](#install-aem-forms-jee-installer)를 참조하십시오.

6. [!DNL Experience Manager Forms] 5.6.0 Add-on 패키지를 설치한 후:

* Stop the [!DNL Experience Manager Forms] instance.

* 디렉토리에서 `bcpkix-1.51`JAR 파일 `bcmail-1.51`및 `bcprov-1.51` JAR 파일을 `crx-repository\launchpad\ext` 삭제합니다.

* 파일에서` sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider` 속성을 `sling.properties` 삭제합니다.

* 인스턴스를 다시 [!DNL Experience Manager Forms] 시작합니다.

**적응형 양식**

* 응용 양식 조각이 누락된 경우 응용 양식이 렌더링되지 않습니다(NPR-34302).

* 적응형 양식 필드에 대한 도움말 내용 설명에 단락 HTML 태그가 표시됩니다(NPR-34116).

* 서버에서 **[!UICONTROL 재유효성 검사]** 속성을 선택하면 응용 양식이 제출되지 않습니다(NPR-33876).

* REST에 **[!UICONTROL 제출 종단점]** 제출 작업은 응용 양식에 대해 작동하지 않습니다(CQ-4299044).

* 접근성:필수 필드에 대한 첨부를 업로드하지 않고 적응형 양식을 제출하려고 하면 초점은 자동으로 첨부 필드로 이동하지 않습니다(CQ-4298065).

* 적응형 양식의 표에 행을 추가할 때 맨 위에 ******[!UICONTROL 추가 및 맨 아래에]** 추가옵션은 적절한 결과를 표시하지 않습니다(CQ-4297511).

* 값 [!UICONTROL 커밋] 스크립트가 잘못 트리거되어 적응형 양식의 데이터가 손실됩니다(CQ-4296874).

* 지역화된 적응형 양식에 대해 날짜 선택기가 제대로 작동하지 않습니다(NPR-34333).

* 파일 이름에 밑줄이나 공백이 있으면 응용 양식에 파일을 첨부할 수 없습니다(CQ-4301001).

* 중첩된 반복 가능한 패널에 상위 패널보다 더 많은 항목이 있는 경우 이러한 중첩 반복 가능한 패널의 모든 항목이 미리 채우기 실패(NPR-33666).

* 적응형 양식에는 열려 있는 리소스 해상도가 있습니다. 이로 인해 제출 실패가 발생합니다. 문제가 간헐적으로 발생합니다(CQ-4299407).

* 처음 필드 구성을 열면 속성 아이콘이 표시되지 않습니다(CQ-4296284).

**워크플로우**

* 워크플로우 승인자가 첨부를 업로드하면 첨부의 이름이 `undefined` (NPR-33699)로 바뀝니다.

* [!DNL Experience Manager] 워크플로우 제거 작업에 실패하고 다음 오류 메시지가 표시됩니다(NPR-33575).

   `java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory`

* [!DNL Experience Manager Forms] 앱을 [!DNL Windows] 중지하면 양식을 제출한 후에 응답이 중지됩니다(NPR-34409).

* AEM 서비스 팩을 설치하면 항목 **To Do** 목록이 링크로 표시되지 않습니다. 할 일 항목 **에** 대한 텍스트에는 HTML 태그가 포함됩니다(NPR-34317).

**대화형 통신**

* 반복 가능한 구성 요소가 중첩된 텍스트 문서 조각을 포함하는 경우 대화형 통신을 저장할 수 없습니다(NPR-34095).

**서신 관리**

* 데이터 사전 값이 포함된 텍스트 문서 조각을 수정하면 에이전트 UI가 응답을 중지합니다(NPR-33930).

* 문서의 컨텐츠를 [!DNL Microsoft Word] 텍스트 문서 조각으로 복사하여 문자로 붙여넣으면 서식 문제가 발생합니다(NPR-33536).

**문서 서비스**

* 출력 및 Forms 서비스를 사용하여 XDP 파일에서 PDF 파일을 생성할 때 텍스트가 누락되거나 겹치게 됩니다(NPR-34237, CQ-429931).

* HTML 파일을 PDF로 변환하는 경우 속성을 구성할 수 `MaxReuseCount` 없습니다(NPR-33470).

* Reader 확장 대화형 기능이 포함된 PDF 파일을 다운로드하는 경우 [!DNL Adobe Reader] (NPR-33729)를 사용하여 PDF 파일에 첨부 파일을 추가할 수 없습니다.

**문서 보안**

* 서비스 팩(NPR-34310)을 설치한 후 PDF 파일에서 HSM 기반 인증서로 서명 작업을 실행할 수 [!DNL Experience Manager] 없습니다.

**디자이너**

* Designer 버전 6.5.x에서 XForms를 열 수 없습니다(CQ-4295322).

* Designer를 열면 시작 화면이 잘못된 연도를 표시합니다(CQ-4295289).

* 서버에 설치할 때 [양식 [!DNL Acrobat DC] 배포 **** ] 옵션이 비활성(CQ-4296304)입니다.

보안 업데이트에 대한 자세한 내용은 [Experience Manager 보안 게시판 페이지를 참조하십시오](https://helpx.adobe.com/security/products/experience-manager.html).

## 6.5.6.0 설치 {#install}

**설치 요구 사항**

* AEM 6.5.6.0을 사용하려면 AEM 6.5가 필요합니다. 세부 지침은[업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하십시오.
* 서비스 팩은 Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 다운로드할 수 있습니다.
* MongoDB 및 여러 인스턴스가 포함된 배포에서 패키지 관리자를 사용하여 작성자 인스턴스 중 하나에 AEM 6.5.6.0을 설치합니다.
* 설치하기 전에 AEM 인스턴스의 스냅샷 또는 새 백업을 만듭니다.
* 설치하기 전에 인스턴스를 다시 시작합니다. 이 작업은 인스턴스가 여전히 업데이트 모드인 경우(및 인스턴스가 이전 버전에서 업데이트된 경우)에만 필요하지만 인스턴스가 오랫동안 실행 중인 경우 권장됩니다.

>[!NOTE]
>
>Adobe Experience Manager 6.5.6.0 패키지를 삭제하거나 제거하지 않는 것이 좋습니다.

### 서비스 팩 설치 {#install-service-pack}

기존 Adobe Experience Manager 6.5 인스턴스에 서비스 팩을 설치하려면 다음 단계를 수행하십시오.

1. Download the service pack from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.6-1.0.zip).

1. 패키지 관리자를 열고 **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭하여 패키지를 업로드합니다. 사용 방법은 [패키지 관리자](https://docs.adobe.com/content/help/ko-KR/experience-manager-65/administering/contentmanagement/package-manager.html)를 참조하십시오.

1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

>[!NOTE]
>
>알려진 문제로 인해 업데이트된 서비스 팩 패키지를 사용할 수 있습니다. 패키지를 설치하는 것이 좋습니다.

>[!NOTE]
>
>패키지 관리자 UI에 대한 대화 상자가 서비스 팩을 설치하는 동안 종료되는 경우가 있습니다. 배포에 액세스하기 전에 오류 로그가 안정될 때까지 기다리는 것이 좋습니다. 업데이터 번들 제거와 관련된 특정 로그를 기다린 후 설치가 성공했는지 확인합니다. 일반적으로 이러한 작업은 [!DNL Safari]에서 발생하지만 모든 브라우저에서 간헐적으로 발생할 수 있습니다.

**자동 설치**

작업 인스턴스에 Adobe Experience Manager 6.5.6.0을 자동으로 설치하는 두 가지 방법이 있습니다.

A. 서버가 온라인 상태일 때 패키지를 `../crx-quickstart/install` 폴더에 넣습니다. 패키지가 자동으로 설치됩니다.

B. [패키지 관리자에서 HTTP API](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html)를 사용합니다. 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

>[!NOTE]
>
>Adobe Experience Manager 6.5.6.0은 Bootstrap 설치를 지원하지 않습니다.

**설치 확인**

1. 제품 정보 페이지(`/system/console/productinfo`)에는 [!UICONTROL 설치된 제품] 아래에 업데이트된 버전 문자열 `Adobe Experience Manager (6.5.6.0)`이 표시됩니다.

1. 모든 OSGI 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]**&#x200B;이거나 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 콘솔 사용: `/system/console/bundles`).

1. The OSGi bundle `org.apache.jackrabbit.oak-core` is version 1.22.3 or later (Use Web Console: `/system/console/bundles`).

이번 릴리스에서 사용할 수 있는 인증된 플랫폼을 확인하려면 [기술 요구 사항](/help/sites-deploying/technical-requirements.md)을 참조하십시오.

### Adobe Experience Manager Forms 추가 기능 패키지 설치 {#install-aem-forms-add-on-package}

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

JEE의 Experience Manager Forms용 누적 설치 프로그램 설치 및 배포 후 구성에 대한 자세한 내용은 [패치 0018에 대한 릴리스 노트](jee-patch-installer-65.md)를 참조하십시오.

### UberJar {#uber-jar}

The UberJar for Experience Manager 6.5.6.0 is available in the [Maven Central repository](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.6-1.0/).

Maven 프로젝트에서 UberJar를 사용하려면 [Uberjar 사용 방법](/help/sites-developing/ht-projects-maven.md)을 참조하여 프로젝트 POM에 다음 종속성을 포함하십시오.

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.6-1.0</version>  
      <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>이 릴리스부터 UberJar 및 기타 관련 아티팩트는 Adobe Public Maven 리포지토리(repo.adobe.com) 대신 Maven Central Repository에서 사용할 수 있습니다. 기본 UberJar 파일의 이름이 로 변경되었습니다 `uber-jar-<version>.jar`. 그 결과, 태그 `classifier`에 대한 값 `apis` 이 없는 `dependency` 것으로 나타났습니다.

## 이제 사용되지 않는 기능 {#removed-deprecated-features}

이 섹션에는 Experience Manager 6.5.6.0에서 더 이상 사용되지 않는 것으로 표시된 기능 및 기능이 나열됩니다. 향후 릴리스에서 제거될 예정인 기능은 먼저 더 이상 사용되지 않도록 설정되며, 사용할 대체 옵션이 있습니다.

고객은 현재 배포에서 기능을 사용할지 검토하고 대체 옵션을 사용할 수 있도록 구현 변경을 계획하는 것이 좋습니다.

| 영역 | 기능 | 대체 |
|---|---|---|
| 통합 | **[!UICONTROL AEM 클라우드 서비스 옵트인]** 화면은 더 이상 사용되지 않습니다. AEM 6.5에서 Adobe IMS 및 I/O를 통해 인증을 사용하는 Target 표준 API를 지원하고 분석 및 개인 설정을 위해 AEM 페이지를 계측하는 Adobe Launch의 늘어나는 역할을 지원하도록 AEM 및 Target 통합이 업데이트되어 옵트인 마법사가 기능상 무관해졌습니다. | 해당 AEM 클라우드 서비스를 통해 시스템 연결, Adobe IMS 인증 및 Adobe I/O 통합 구성. |
| 커넥터 | Microsoft SharePoint 2010 및 Microsoft SharePoint 2013 Adobe JCR Connector는 AEM 6.5에서 더 이상 사용되지 않습니다. | N/A |

## 알려진 문제 {#known-issues}

* 보안 상태 검사가 작동하지 않고 시스템에 다음 오류 메시지가 표시되는 경우
   `message: Could not verify users and could not test system account logins.`
문제를 해결하려면 다음 단계를 수행하십시오.
   1. https://&lt;*hostname*>:&lt;*port*>/system/console/configMgr로 이동합니다.

   1. `hc.impl`을 검색합니다. 

   1. 서비스 [!UICONTROL 매핑에서]을 클릭하고 `+` 지정합니다 `com.adobe.granite.repository.hc.impl=[user-reader-service]`.

   1. Click [!UICONTROL Save] to save the configuration.

* 6.5에 [!DNL Experience Manager] 6.5 서비스 팩 5 또는 이전 서비스 팩을 설치하는 경우, 사용자 지정 워크플로우 모델(에서 생성)의 런타임 복사본 [!DNL Experience Manager] `/var/workflow/models/dam`이 삭제됩니다.
런타임 복사본을 검색하려면 HTTP API를 사용하여 사용자 지정 워크플로우 모델의 디자인 시간 사본을 해당 런타임 복사본과 동기화하는 것이 Adobe에서 제안합니다.
   `<designModelPath>/jcr:content.generate.json`.

* 규칙 정의 대화 상자를 사용하여 [!UICONTROL 폴더 메타데이터 스키마 Forms 편집기] 및 [!UICONTROL 메타데이터 스키마 Forms 편집기에서] 계단식 규칙을 편집하고 만들 때 문제가 발생하면 Adobe 지원 [!UICONTROL 에] 문의하십시오. 이미 만들어지고 저장된 규칙은 예상대로 작동합니다.

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

다음 텍스트 문서에는 AEM 6.5.6.0에 포함된 OSGi 번들 및 컨텐츠 패키지 목록이 나와 있습니다.

* [AEM 6.5.6.0에 포함된 OSGi 번들 목록](assets/6560_bundles.txt)

* [AEM 6.5.6.0에 포함된 콘텐츠 패키지 목록](assets/6560_packages.txt)

## 제한된 사이트 {#restricted-sites}

다음 사이트는 고객만 사용할 수 있습니다. 액세스가 필요한 고객의 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [고객 지원에 문의하기](https://docs.adobe.com/content/help/ko-KR/customer-one/using/home.html)
지원 포털에 액세스하는 방법에 대한 자세한 내용은 [지원 포털에 액세스](https://helpx.adobe.com/kr/experience-manager/kb/accessing-aem-support-portal.html)를 참조하십시오.

>[!MORELIKETHIS]
>
>* [AEM 6.5 릴리스 노트](/help/release-notes/release-notes.md)
>* [AEM 제품 페이지](https://www.adobe.com/kr/marketing/experience-manager.html)
>* [AEM 6.5 설명서](https://helpx.adobe.com/kr/support/experience-manager/6-5.html)
>* [Adobe 우선 순위 제품 업데이트](https://www.adobe.com/subscription/priority-product-update.html) 구독

