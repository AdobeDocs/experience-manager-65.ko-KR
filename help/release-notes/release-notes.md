---
title: 용 릴리스 노트 [!DNL Adobe Experience Manager] 6.5
description: 릴리스 정보, 새로운 기능, 사용 방법 설치 및 다음에 대한 자세한 변경 목록을 찾습니다. [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
source-git-commit: f53dbe7d51ff976f8d79702a86527f984aa00997
workflow-type: tm+mt
source-wordcount: '2983'
ht-degree: 10%

---

# [!DNL Adobe Experience Manager] 6.5 최신 서비스 팩 릴리스 노트 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=WRAZ43&nav=MTVfezk2OTJDQTNFLUI4QTQtNDY2RS05NEVCLUQ5QjcyNEVENkJDNn0 -->

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 버전 | 6.5.16.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2023년 2월 23일 목요일 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 다운로드 URL | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]be/packages/cq650/servicepack/aem-service-pkg-6.5.16.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 에 포함된 사항 [!DNL Experience Manager] 6.5.16.0 {#what-is-included-in-aem-6516}

[!DNL Experience Manager] 6.5.16.0에는 2019년 4월에 6.5의 초기 가용성 이후 릴리스된 새로운 기능, 주요 고객이 요청한 향상된 기능, 버그 수정 사항, 성능, 안정성 및 보안 개선 사항이 포함되어 있습니다. [이 서비스 팩 설치](#install) on [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Dynamic Media의 주요 개선 사항은 다음과 같습니다.

Dynamic Media 비디오 게재에서 적응형 비트율 스트리밍을 위해(CMAF 포함) 새로운 프로토콜 DASH(HTTP를 통한 동적 적응형 스트리밍) 지원을 시작했습니다 [일반 미디어 응용 프로그램 형식] 활성화됨).

* 응용 스트리밍(DASH/HLS)을 사용하면 비디오에 대한 최종 사용자 보기 환경을 향상시킬 수 있습니다.
* DASH는 응용 비디오 스트리밍을 위한 국제 표준 프로토콜이며 업계에서 널리 사용되고 있습니다.
* 현재 북미에서(지원 티켓을 통해 지원 가능) 제공되며, 아시아 태평양 및 유럽-중동 지역에서 곧 제공될 예정입니다.

자세한 내용은 [계정에서 DASH 사용](/help/assets/video.md#enable-dash).

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6516}

* 연결된 자산: 원격 DAM의 이미지에 대한 스마트 자르기 옵션을 활성화하고 이미지를 폴더에 업로드하고 폴더를 로컬 사이트에 동기화하면 로컬 사이트 배포에서 폴더가 열리지 않습니다. (NPR-39912)
* 이름별로 컬렉션을 정렬하는 동안 목록 보기가 제대로 작동하지 않습니다(ASSETS-19401)
* 대형 미디어 파일(JPEG)이 컬렉션에 업로드되면 Experience Manager이 응답하지 않습니다. (ASSETS-19387)
* 자산의 위치가 적절하게 렌더링되지 않으므로 컨텐츠 트리 창에서 표시된 자산 이름이 잘못되었습니다. (ASSETS-18870)
* 링크를 사용하여 컬렉션을 공유하는 동안 URL의 데이터가 카드 보기 셔플 과 목록 보기 간에 일치하지 않습니다. (ASSETS-18758)
* 폴더 유형에서 필터를 사용하여 omnisearch를 수행하면 검색 결과가 일치하지 않습니다. (ASSETS-18227)
* 다음 `dam:size` XMP 원본에 쓰기 후 속성이 업데이트되지 않으므로 잘못된 정보가 반환됩니다 `/platform/path/to/asset.jpg;resource=metadata` API. (ASSETS-17631)
* 모든 Experience Manager 인스턴스에서 리소스 확인자가 닫히지 않았습니다. (ASSETS-16904)
* 을(를) 지정했더라도 자산에 대한 버전을 만들 수 없습니다 `create` 및 `modify` 사용 권한. (ASSETS-15956)
* 다음 `move` 자산을 한 지점에서 다른 지점으로 이동하는 동안 단추가 임의로 비활성화됩니다. (ASSETS-14889)
* 텍스트가 제목 태그 내에 정의되어 있지 않고 일반 텍스트로 정의되어 있으므로 화면 판독기에서 제목을 식별할 수 없습니다. (ASSETS-6924)
* 이미지 아래에 있는 대체 텍스트는 필수가 아니지만 이미지 아래에 표시되는 텍스트는 반복되며 `Type` 속성을 사용합니다. (ASSETS-6915)


## [!DNL Assets] - [!DNL Dynamic Media] {#dm-6516}

* 양식 요소에 레이블이 없습니다. NVDA 및 JAWS와 같은 화면 판독기에서 양식 레이블 정보가 제대로 표시되지 않습니다. (CQ-4344078)
* 드롭다운이 `Escape` 키보드에서 키가 사용됩니다. (CQ-4344077)
* 잘못된 입력이 지정된 후 인라인 오류 제안에 대해 나타나는 정보 아이콘(&quot;i&quot;)은 키보드를 사용하여 액세스할 수 없습니다. (CQ-4344076)
* `getManifestURI` JCR 속성이 `toString` 대신 `getString`. (ASSETS-18674)
* SmartCrop 비디오 구성 요소가 올바르게 작동하지 않습니다. 구성 요소가 스트리밍 대신 재생을 수행하고 있으며 VTT 호출이 실패하고 404 오류가 발생합니다. (ASSETS-18468)
* 선택 **[!UICONTROL 속성]** 자산의 뷰어 페이지에서 null 포인터 예외가 발생합니다. (ASSETS-18420)
* [!DNL Experience Manager] 다음을 포함하는 DASH 스트리밍에 대한 사용자 인터페이스 변경 사항:
   * 비디오 프로필 편집기에 표시되는 CMAF(Common Media Application Format) 필드가 있습니다.
   * 비디오 업로드 프로세스가 있는 경우 CMAF 플래그를 전송합니다.
   * 옵션 **[!UICONTROL 자동]**, **[!UICONTROL hls]**, 및 **[!UICONTROL 대시]** 이제 뷰어 사전 설정 편집기의 재생 드롭다운 목록에서 을 사용할 수 있습니다 **[!UICONTROL 비헤이비어]** 탭.
(ASSETS-17428)
* 탐색에서 **[!UICONTROL 자산]** > **[!UICONTROL 파일]** > **[!UICONTROL 만들기]** > **[!UICONTROL 회전판 세트]**&#x200B;과 같은 경우 그림 아이콘이 &quot;슬라이드 1&quot; 텍스트 문자열과 겹칩니다. (ASSETS-18578)
* 게시되지 않은 자산이 다시 게시됩니다. (ASSETS-16428)
* Experience Manager 작성자가 로드 문제로 인해 다운되어 합성 경고가 생성됩니다. (ASSETS-15937)
* Dynamic Media 일반 설정 페이지에서 번역되지 않은 오류 메시지가 표시됩니다 `Failed to fetch data` 이 나타납니다. (ASSETS-15617)

## [!DNL Forms] {#forms-6516}

### [!DNL Forms] 주요 기능 {#forms-features-6516}

* [헤드리스 적응형 Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) 개발자는 기존의 그래픽 사용자 인터페이스를 사용하지 않고 API를 통해 액세스 및 상호 작용할 수 있는 대화형 양식을 작성, 게시 및 관리할 수 있습니다.

* [응용 Forms 핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) 는 Adobe Experience Manager WCM 코어 구성 요소의 기초 위에 구축된 24개의 오픈 소스 BEM 준수 구성 요소 세트입니다. 이러한 구성 요소는 오픈 소스이며 개발자들이 조직의 특정 요구 사항에 맞게 이러한 구성 요소를 쉽게 사용자 지정하고 확장할 수 있는 기능을 제공합니다. 사용자 지정 능력을 가진 모든 사용자 [WCM 코어 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/authoring.html?lang=en) 이러한 구성 요소를 쉽게 사용자 지정하고 스타일을 지정할 수 있습니다.

* 이제 OSGi의 Reader 확장 서비스는 Adobe Acrobat Reader에서 데이터를 가져오거나 내보낼 수 있도록 PDF에 대한 사용 권한을 가져오고 내보낼 수 있는 별도의 옵션을 제공합니다. (NPR-39909)

### [!DNL Forms] 수정 사항 {#forms-fixes-6516}

* 사용 시 **작업 할당** 지정된 작업에 대한 알림을 전송하는 단계에는 지정된 개인에게 1개 대신 2개의 이메일이 전송됩니다. (NPR-40078)
* 사용자가 표 헤더를 숨기면 이전에 설정한 열 너비가 설정 해제되고 모든 열이 동일한 너비를 유지합니다. (NPR-40063)
* 관리 사용자의 기본 암호를 `admin`를 호출하고 `Prepare Adobe Experience Manager Server For DSC deployment` AEM Forms JEE 서비스 팩 확인 시 실패합니다. (NPR-40062), (NPR-39387)
* OutputService 및 AssemblerService API에서 PDF 양식을 PDF/A로 변환하지 못했습니다(NPR-39990)
* AssemblerService에서 PDF을 PDF/A로 변환할 수 없습니다. 사용자가 PDF을 PDF/A로 변환하면 다음 오류가 발생합니다. `PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Summary" ignoreUnusedResources="true" allowCertificationSignatures="true"> <Violation count="6" key="PDFA_CS_001_NOT_DEVICE_INDEPENDENT" description="ColorSpace is not device independent`. (NPR-39956)
* GuideSubmitServlet API 호출에 서버측 유효성 검사가 실패하면 클라이언트에 전송된 응답에서 오류가 반환되지 않습니다. (NPR-39925)
* Windows 서버의 AEM 6.5.15.0 서비스 팩으로 업그레이드한 후 사용자에게 여러 오류 메시지가 표시되고 이메일 서비스가 작동하지 않습니다.(NPR-39919)
* AEM 6.5.14.0으로 업그레이드하고 importData 서비스를 사용하여 PDF을 XML과 병합하는 경우 다음 오류가 발생합니다. `Caused by: java.lang.NoSuchMethodError: com.adobe.xfa.form.FormModel.isXFABarcode(Lcom/adobe/xfa/Node;)Ljava/lang/Boolean`.(NPR-39807)
* 사용자가 설치될 때 **문서 보안 사무소** 확장: 다음 문제가 발생합니다.
   * Microsoft® Excel이 자주 충돌합니다.
   * 보안 문서를 여는 동안 **문서 보안 사무소** 확장이 컴퓨터에 설치되어 있지 않습니다. 사용자에게 보안 확장을 다운로드하고 설치하도록 지시합니다. (NPR-39768)
* 사용자가 AEM 6.5.15.0 서비스 팩으로 업그레이드한 후 PostScript-to-Pdf 변환이 작동하지 않습니다. (NPR-39765), (NPR-39764)
* 사용자가 적응형 양식을 연 후 투어 화면을 열려고 하면 NullPointer 예외로 인해 실패합니다.`[172.17.0.1[1662032923933]GET/libs/fd/af/content/editors/form/tour/content.htmlHTTP/1.1]com.day.cq.wcm.core.impl.WCMDebugFilterException:org.apache.sling.api.scripting.ScriptEvaluationException:"` (NPR-39654)
* Windows에서는 사용자가 고대비 검정 설정을 활성화하면 브라우저에서 HTML 미리 보기로 렌더링될 때 HTML5 Forms 컨텐츠가 불명확해집니다. (NPR-39018)
* 사용자가 메타데이터를 추가하려고 하면 초안 구성 요소와 제출 구성 요소 모두에 대해 저장 단추가 작동하지 않습니다.(CQ-4349601)
* AEM 6.5.15.0 서비스 팩으로 업그레이드한 후 상대 URL의 리디렉션이 더 이상 시각적 편집기에서 작동하지 않습니다. (NPR-39947)
* 사용자가 AEM 6.5.15.0 서비스 팩으로 업그레이드할 때 리디렉션이 Internet Explorer에서 작동하지 않습니다. (CQ-4351745)
* 사용자가 AEM 6.5.15.0 서비스 팩으로 업그레이드하면 HTML 제목 태그가 인식되지 않습니다. 제목 태그의 HTML 코드는 HTML 양식에 텍스트로 표시됩니다. (NPR-39915)
* 사용자가 적응형 양식을 제출하려고 하면 일반적으로 오류가 발생합니다. `ERROR [10.207.64.167 [1668589530607] POST /app/LS4/content/forms/af/revalidate/jcr:content/guideContainer.af.submit.jsp HTTP/1.1]`( NPR-39809)
* 사용자가 를 사용하여 기록 문서를 미리 볼 때 **이메일 보내기** 제출 작업이 올바르게 표시되지 않습니다. 편지 템플릿은 레코드 문서의 미리 보기에 포함됩니다. (CQ-4352155)
* 사용자가 Microsoft Edge 브라우저에서 적응형 양식을 IE 호환성 모드로 HTML으로 미리 보면 제대로 표시되지 않습니다.(CQ-4352216)
* 사전은 변환을 사용하려면 밑줄 또는 하이픈과 같은 특수 문자가 있는 새 로케일을 포함해야 합니다. (NPR-40088)

AEM 6.5.16.0 Forms 추가 기능 서비스 팩을 설치한 후 고객은 아래에 나열된 문제에 직면했습니다. 따라서, [AEM 6.5.16.0 Forms 추가 기능 서비스 팩 - 6.0.914](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 가 출시되었습니다. Adobe은 업데이트된 서비스 팩을 사용할 것을 권장합니다.
* 사용자가 forms-users 그룹에 있는 사용자로 적응형 양식을 작성하려고 하면 템플릿을 선택하는 옵션이 표시되지 않고 다음과 유사한 오류가 발생합니다. 내부 서버 오류: java.base/java.util.stream.ReferencePipeline$2$1.accept(ReferencePipeline.java:176) at.java.base/java.util.stream.ReferencePipeline$2$1.accept(ReferencePipeline.java:176)at.adobe.aem.formsyndocuments.servlet.테마ClientDataSourceServlet.lambda$getThemeClientLibCategoryListList$3(JointJava.3ReferenceReatorReteratorReferenceReator3.3Java.3ReferenceReteratorName.3Name(ReferenceReferenceReferenceReferenceReferenceReferenceReferenceReferenceReferenceReferenceHostReferenceReferenceReferenceReator)의 javaReferenceReferenceName.3) (FORMS-7629)
* 코드 편집기 규칙에서 변경한 사항이 저장되지 않습니다.(FORMS.-7532)

## 통합 {#integrations-6516}

* Experience Manager 6.5에서 Adobe Search &amp; Promote 코드 및 종속성을 제거합니다. Adobe Search &amp; Promote은 2022년 9월 서비스 종료에 도달했습니다. 자세한 내용은 [Adobe Search &amp; Promote 서비스 종료 공지](https://experienceleague.adobe.com/docs/discontinued/using/search-promote.html?lang=en). (NPR-39706)

## [!DNL Sites] {#sites-6516}

* 현재 `cq-wcm-core` artifactory 릴리스에는 POM이 없습니다. (SITES-10983)
* 롤아웃 미리 보기 작업에는 만들 페이지가 나열되지 않아야 합니다. (SITES-10355, CQ-4266213)
* MSM 분리 후 롤아웃은 분리된 페이지를 다시 만듭니다. (SITES-9841)
* 론치를 만드는 것은 시간 제한; 사용자는 요청 시간이 초과되기 전에 로드 화면에서 몇 분을 기다려야 합니다. (SITES-9051)
* 페이지 롤아웃 사용자 인터페이스에 존재하지 않는 상위 페이지 경로가 표시됩니다. 성공 메시지가 있는 페이지를 롤아웃할 수 있지만 상위 페이지가 처음에 롤아웃되지 않아 하위 페이지가 롤아웃되지 않습니다. (SITES-8621)

### [!DNL Sites] - 핵심 구성 요소 {#sites-core-components-6516}

* 이메일 페이지에서 링크 처리를 중앙 집중화하여 모델 사용자 지정이 더 이상 필요하지 않게 합니다. (SITES-9002)

### [!DNL Sites] - 관리 사용자 인터페이스 {#sites-adminui-6516}

* CSV 내보내기가 선택한 페이지 아래에 모든 페이지를 내보내지는 않습니다. (SITES-9390)

### [!DNL Sites] - [!DNL Content Fragments] {#sites-contentfragments-6516}

* 컨텐츠 조각의 JSON을 인쇄할 수 없습니다. 이유는 컨텐츠 조각의 미리 보기 페이지를 열 때 GraphQL 쿼리를 생성할 수 없기 때문입니다. (SITES-8619)
* 컨텐츠 조각 모델 편집기를 다시 열면 모두 **[!UICONTROL 날짜 및 시간]** 필드의 기본값은 날짜 및 시간 유형으로 설정됩니다. (SITES-8401)

### [!DNL Sites] - [!DNL Experience Fragments] {#sites-experiencefragments-6516}

* 템플릿이 허용된 템플릿 아래에 나열되더라도 경험 조각을 다른 폴더로 이동할 수 없습니다. (SITES-8601)
* (SITES-7989)


### [!DNL Sites] - 페이지 편집기 {#sites-pageeditor-6516}

* 작성 모드에서 페이지 렌더링을 많이 만드는 SITES-8464에서 수행한 리소스 확인자 개선 사항에 대한 종속성을 업데이트합니다 `TemplatedResourceImpl` 개체. (SITES-9350)


## 슬링 {#sling-6516}

* 시작 시 Experience Manager이 교착 상태에 있습니다. (NPR-39832)
* Experience Manager 버전 저장소에 별칭 경로가 많이 있으면 Experience Manager을 시작할 수 없습니다. (NPR-38955)


## 번역 프로젝트 {#translation-6516}

* in `MicrosoftTranslationServiceImpl`, 쿼리 문자열 매개 변수 `Category` 은 올바르지 않습니다. (NPR-39828)
* 번역 프로젝트를 만들면 오류가 표시됩니다 *기본 페이지 리소스가 없습니다.*; 번역 프로젝트가 생성되지 않습니다. (NPR-39762)
* 휴먼 번역 커넥터를 사용하는 번역 프로젝트에 만기 날짜를 설정할 수 없습니다. (NPR-39593)

## 사용자 인터페이스 {#ui-6516}

* 더 작은 해상도로 변경하면 DatePicker가 표시되지 않고 AM/PM 선택이 표시 또는 변경되지 않습니다. (NPR-39948)
* Js(JavaScript의 최소 최소화)를 사용하는 경우 구문 분석 오류로 인해 축소를 처리하지 않습니다. (NPR-39650)
* 태그 필드 (`/libs/cq/gui/components/coral/common/form/tagfield`)이 타임라인과 충돌합니다. (CQ-4350751)


## WCM {#wcm-6516}

* 롤아웃 미리 보기 작업에는 만들 페이지가 나열되지 않아야 합니다. (CQ-4266213, SITES-10355)

## 워크플로 {#workflow-6516}

* 편집 가능한 워크플로우 모델 수동 삭제 `/conf` 편집 가능한 모델 없이 느린 런타임 모델 인스턴스를 둡니다. (CQ-4349365)


## 설치 [!DNL Experience Manager] 6.5.16.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.16.0 필요 [!DNL Experience Manager] 6.5. 참조: [업그레이드 설명서](/help/sites-deploying/upgrade.md) 자세한 지침 <!-- UPDATE FOR EACH NEW RELEASE -->
* 서비스 팩은 Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 다운로드할 수 있습니다.
* MongoDB 및 여러 인스턴스가 포함된 배포에서 을 설치합니다. [!DNL Experience Manager] 패키지 관리자를 사용하는 작성자 인스턴스 중 하나에 대한 6.5.16.0.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe은 제거 또는 제거를 권장하지 않습니다 [!DNL Experience Manager] 6.5.16.0 패키지. 따라서 팩을 설치하기 전에 `crx-repository` 반납해야 할 경우를 대비해서 <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for AEM Forms, see [AEM Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### 서비스 팩 설치 [!DNL Experience Manager] 6.5 {#install-service-pack}

1. 인스턴스가 업데이트 모드(이전 버전에서 인스턴스가 업데이트되었을 때)인 경우 설치하기 전에 인스턴스를 다시 시작합니다. Adobe은 인스턴스에 대한 현재 가동 시간이 높은 경우 다시 시작할 것을 권장합니다.

1. 설치하기 전에 스냅샷 또는 새 백업 [!DNL Experience Manager] 인스턴스.

1. 에서 서비스 팩 다운로드 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. 패키지 관리자를 연 다음 **[!UICONTROL 패키지 업로드]** 를 눌러 패키지를 업로드합니다. 자세한 내용은 [패키지 관리자](/help/sites-administering/package-manager.md).

1. 패키지를 선택한 다음 을 선택합니다 **[!UICONTROL 설치]**.

1. S3 커넥터를 업데이트하려면 서비스 팩을 설치한 후 인스턴스를 중지하고 기존 커넥터를 설치 폴더에 제공된 새 이진 파일로 바꾸고 인스턴스를 다시 시작합니다. 자세한 내용은 [Amazon S3 데이터 저장소](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>패키지 관리자 UI에 대한 대화 상자가 서비스 팩을 설치하는 동안 종료되는 경우가 있습니다. 배포에 액세스하기 전에 오류 로그가 안정될 때까지 기다리는 것이 좋습니다. 업데이터 번들 제거와 관련된 특정 로그를 기다린 후 설치가 성공했는지 확인합니다. 일반적으로 이 문제는 [!DNL Safari] 브라우저이지만 모든 브라우저에서 간헐적으로 발생할 수 있습니다.

**자동 설치**

자동으로 설치하는 데 사용할 수 있는 방법에는 두 가지가 있습니다 [!DNL Experience Manager] 6.5.16.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* 서버가 온라인 상태일 때 패키지를 `../crx-quickstart/install` 폴더에 넣습니다. 패키지가 자동으로 설치됩니다.
* [패키지 관리자에서 HTTP API](/help/sites-administering/package-manager.md#package-share)를 사용합니다. 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

>[!NOTE]
>
>Experience Manager 6.5.16.0은 Bootstrap 설치를 지원하지 않습니다. <!-- UPDATE FOR EACH NEW RELEASE -->

**설치 확인**

이번 릴리스에서 사용할 수 있는 인증된 플랫폼을 확인하려면 [기술 요구 사항](/help/sites-deploying/technical-requirements.md).

1. 제품 정보 페이지(`/system/console/productinfo`)에 업데이트된 버전 문자열 표시 `Adobe Experience Manager (6.5.16.0)` 아래에 [!UICONTROL 설치된 제품]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 모든 OSGI 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]**&#x200B;이거나 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 콘솔 사용: `/system/console/bundles`).

1. OSGi 번들 `org.apache.jackrabbit.oak-core` 버전 1.22.14 이상(웹 콘솔 사용: `/system/console/bundles`). <!-- NPR-39939 for 6.5.16.0 --> <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### 용 서비스 팩 설치 [!DNL Experience Manager] Forms {#install-aem-forms-add-on-package}

AEM Forms에 서비스 팩을 설치하는 방법은 [AEM Forms 서비스 팩 설치 지침](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### Experience Manager 컨텐츠 조각용 GraphQL 인덱스 패키지 설치 {#install-aem-graphql-index-add-on-package}

GraphQL을 사용하는 고객은 [GraphQL 색인 패키지 1.0.5가 있는 AEM 컨텐츠 조각](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip).

이렇게 하면 실제로 사용하는 기능을 기반으로 필요한 인덱스 정의를 추가할 수 있습니다.

이 패키지를 설치하지 못하면 GraphQL 쿼리가 느려지거나 실패할 수 있습니다.

>[!NOTE]
>
>이 패키지는 인스턴스당 한 번만 설치해야 합니다. 모든 서비스 팩과 함께 다시 설치할 필요는 없습니다.

### UberJar {#uber-jar}

용 UberJar [!DNL Experience Manager] 6.5.16.0은 [Maven 중앙 저장소](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>Experience Manager 6.5.16.0에서 UberJar 버전(6.5.15.0)은 이전 릴리스와 동일하게 유지됩니다.


Maven 프로젝트에서 UberJar를 사용하려면 다음을 참조하십시오 [uberJar 사용 방법](/help/sites-developing/ht-projects-maven.md) 프로젝트 POM에 다음 종속성을 포함하십시오. <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.15</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar 및 기타 관련 가공물은 Adobe Public Maven 저장소(`repo.adobe.com`). 기본 UberJar 파일의 이름이 `uber-jar-<version>.jar`. 그래서, 아무것도 없어 `classifier`, 사용 `apis` 값으로서, `dependency` 태그에 가깝게 포함했습니다.

## 이제 사용되지 않는 기능 {#removed-deprecated-features}

다음은 사용 중단되는 것으로 표시된 기능 및 기능 목록입니다 [!DNL Experience Manager] 6.5.7.0. 기능은 처음에 더 이상 사용되지 않음으로 표시되고 이후 릴리스에서 이후에 제거됩니다. 다른 옵션이 제공됩니다.

배포에서 기능 또는 기능을 사용하는지 검토합니다. 또한 대체 옵션을 사용하도록 구현을 변경할 계획입니다.

| 영역 | 특별 포함 | 대체 |
|---|---|---|
| 통합 | 다음 **[!UICONTROL AEM 클라우드 서비스 옵트인]** 화면은 다음부터 사용되지 않습니다 [!DNL Experience Manager] 및 [!DNL Adobe Target] 통합이에서 업데이트됨 [!DNL Experience Manager] 6.5. 통합은 Adobe Target Standard API를 지원합니다. API는 Adobe IMS 및 [!DNL Adobe I/O Runtime]. 이 플러그인은 Adobe Launch가 악기 역할을 계속 수행할 수 있도록 지원합니다 [!DNL Experience Manager] 분석 및 개인화를 위한 페이지인 옵트인 마법사는 기능적으로 관련이 없습니다. | 시스템 연결, Adobe IMS 인증 및 구성 [!DNL Adobe I/O Runtime] 해당 [!DNL Experience Manager] 클라우드 서비스. |
| 커넥터 | Microsoft® SharePoint 2010 및 Microsoft® SharePoint 2013용 Adobe JCR Connector는 더 이상 사용되지 않습니다 [!DNL Experience Manager] 6.5. | N/A |

## 알려진 문제 {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* 컨텐츠 모델의 사용자 지정 API 이름을 사용한 GraphQL 쿼리를 대신 기본 컨텐츠 모델의 이름을 사용하도록 업데이트하십시오.

* GraphQL 쿼리는 `damAssetLucene` 인덱스 대신 `fragments` 색인입니다. 이로 인해 GraphQL 쿼리가 실패하거나 실행하는 데 시간이 오래 걸릴 수 있습니다.

   문제를 해결하려면 `damAssetLucene` 다음 두 속성을 포함하도록 구성해야 합니다.

   * `contentFragment`
   * `model`

   인덱스 정의를 변경한 후 재색인화가 필요합니다(`reindex` = `true`).

   이 단계 후에 GraphQL 쿼리가 더 빨리 수행되어야 합니다.

* 로서의 [!DNL Microsoft®® Windows Server 2019] 을 지원하지 않음 [!DNL MySQL 5.7] 및 [!DNL JBoss®® EAP 7.1], [!DNL Microsoft®® Windows Server 2019] 에 대한 턴키 설치를 지원하지 않습니다. [!DNL AEM Forms 6.5.10.0].

* 업그레이드 [!DNL Experience Manager] 인스턴스: 6.5.0 - 6.5.4에서 Java™ 11의 최신 서비스 팩으로 `RRD4JReporter` 의 예외 `error.log` 파일. 예외를 중지하려면 인스턴스를 다시 시작합니다. [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 사용자는 의 계층 구조에서 폴더의 이름을 바꿀 수 있습니다 [!DNL Assets] 중첩된 폴더를 [!DNL Brand Portal]. 그러나 폴더의 제목은에서 업데이트되지 않습니다 [!DNL Brand Portal] 루트 폴더를 다시 게시할 때까지 .

* 사용자가 적응형 양식에서 처음으로 필드를 구성하도록 선택하면 구성 저장 옵션이 속성 브라우저에 표시되지 않습니다. 동일한 편집기에서 적응형 양식의 다른 필드 일부를 구성하도록 선택하면 문제가 해결됩니다.

* 설치 중에 다음 오류 및 경고 메시지가 표시될 수 있습니다 [!DNL Experience Manager] 6.5.x.x:
   * Adobe Target 통합이 [!DNL Experience Manager] target Standard API(IMS 인증)를 사용한 다음, 경험 조각을 Target으로 내보내면 잘못된 오퍼 유형이 생성됩니다. 경험 조각/소스 Adobe Experience Manager 유형 대신 Target은 &quot;HTML&quot;/소스 &quot;Adobe Target Classic&quot; 유형으로 여러 가지 오퍼를 작성합니다.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: granite/operations/maintenance에 유지 관리 창이 없습니다.
   * SUM, MAX 및 MIN과 같은 집계 함수를 사용하는 경우 적용형 양식 서버측 유효성 검사가 실패합니다(CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance에 유지 관리 창이 없습니다.
   * 쇼퍼블 배너 뷰어를 통해 자산을 미리 볼 때 Dynamic Media 대화형 이미지의 핫스팟이 표시되지 않습니다.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : 등록 변경이 등록되지 않을 때까지 기다리는 동안 시간이 초과되었습니다.

* 컨텐츠 조각 또는 사이트/페이지 를 이동/삭제/게시하려고 할 때 백그라운드 쿼리가 실패하여 컨텐츠 조각 참조를 가져오면 문제가 발생합니다. 즉, 기능이 작동하지 않습니다.
올바른 작업을 수행하려면 인덱스 정의 노드에 다음 속성을 추가해야 합니다 `/oak:index/damAssetLucene` (재색인화가 필요하지 않음):

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

* AEM Forms에서 POP3 프로토콜은 Microsoft® Office 365용 전자 메일 끝점에서 작동하지 않습니다.
* JBoss® 7.1.4 플랫폼에서 AEM 6.5.16.0 서비스 팩을 설치할 때 `adobe-livecycle-jboss.ear` 배포에 실패했습니다.

## OSGi 번들 및 컨텐츠 패키지가 포함됨 {#osgi-bundles-and-content-packages-included}

다음 텍스트 문서에는 다음 항목에 포함된 OSGi 번들 및 컨텐츠 패키지 목록이 나와 있습니다. [!DNL Experience Manager] 6.5.16.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager 6.5.16.0에 포함된 OSGi 번들 목록](/help/release-notes/assets/65160_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.16.0에 포함된 컨텐츠 패키지 목록](/help/release-notes/assets/65160_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 제한된 웹 사이트 {#restricted-sites}

이러한 웹 사이트는 고객만 사용할 수 있습니다. 액세스가 필요한 고객인 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [Adobe 고객 지원 문의](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 제품 페이지](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 설명서](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ko-KR)
>* [Adobe 우선 순위 제품 업데이트](https://www.adobe.com/kr/subscription/priority-product-update.html) 구독

