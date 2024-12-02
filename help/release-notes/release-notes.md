---
title: ' [!DNL Adobe Experience Manager] 6.5 릴리스 정보'
description: ' [!DNL Adobe Experience Manager] 6.5에 대한 릴리스 정보, 새로운 기능, 설치 방법 및 자세한 변경 목록을 찾으십시오.'
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 36238364383c380269812641acc66e452e2362ba
workflow-type: tm+mt
source-wordcount: '6089'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager] 6.5 최신 서비스 팩 릴리스 노트 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 버전 | 6.5.22.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2024년 11월 21일 목요일 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 다운로드 URL | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## [!DNL Experience Manager] 6.5.22.0에 포함된 항목 {#what-is-included-in-aem-6522}

[!DNL Experience Manager] 6.5.22.0에는 새로운 기능, 주요 고객 요청 개선 사항 및 버그 수정 사항이 포함되어 있습니다. 또한 2019년 4월 6.5의 최초 출시 이후 발표된 성능, 안정성 및 보안 개선 사항이 포함되어 있습니다. [!DNL Experience Manager] 6.5에서 [이 서비스 팩을 설치](#install)합니다.

<!-- UPDATE FOR EACH NEW RELEASE -->

## 주요 기능 및 개선 사항

### Forms {#forms-sp22}

이번 릴리스의 주요 기능 및 개선 사항은 다음과 같습니다.

* [hCaptcha](/help/forms/using/integrate-adaptive-forms-hcaptcha.md) 및 [Cloudfare Turnstile Captcha 서비스](/help/forms/using/integrate-adaptive-forms-turnstile.md): AEM Forms에서는 다음 Captcha 서비스를 지원합니다.
   * Captcha는 확인란 위젯으로 사용자에게 도전하여 봇, 스팸 및 자동 남용으로부터 양식을 보호합니다. 인간 사용자만 진행하도록 보장해 온라인 거래에 대한 보안을 강화한다.
   * Cloudflare Turnstile은 자동화된 봇, 악의적인 공격, 스팸 및 원치 않는 자동화된 트래픽으로부터 양식을 보호하기 위한 보안 조치를 제공합니다. 양식 제출을 허용하기 전에 양식 제출에 대한 확인란을 표시하여 사람인지 확인합니다.

* 적응형 양식 버전 관리:
   * [적응형 양식의 여러 버전 만들기](/help/forms/using/add-versioning-reviews-comments.md): 이제 사용자가 기존 양식의 변형을 쉽게 관리할 수 있습니다. 이에 따라 간소화된 단일 워크플로 내에서 버전 제어가 단순화되고, 양식 최적화를 위한 비교가 용이해집니다.
   * [적응형 Forms 비교](/help/forms/using/compare-forms-core-components.md): 이제 사용자는 두 양식을 쉽게 비교하여 차이점을 식별할 수 있습니다. 팀원이 수정본을 비교하고 변경 사항을 효율적으로 논의할 수 있도록 하여 원활한 공동 작업을 촉진합니다.

* [대화형 통신 일괄 처리 API](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/interactive-communications/create-interactive-communication#output-format-print-channel)에서 글꼴 임베딩을 사용하도록 설정할 수 있는 지원이 추가되었습니다. 이제 대화형 통신에 일괄 처리 API를 통해 생성된 PDF에 Adobe Ming 및 Adobe Myungjo 글꼴을 포함할 수 있는 지원이 포함됩니다. 이러한 개선된 기능은 글꼴 하위 집합을 사용하는 경우에도 생성된 문서에서 정확한 텍스트 렌더링을 보장하여 PDF 출력에서 다국어 콘텐츠에 대한 향상된 지원을 제공합니다.

* [PDF 접근성을 위한 목차 API](/help/forms/using/aem-document-services-programmatically.md#auto-tag-pdf-documents-auto-tag-api): 이제 OSGi의 AEM Forms에서 새로운 TOC Tag API를 지원하여 접근성 표준에 대한 PDF을 향상합니다. 보조 기술을 가진 사용자가 PDF에 보다 쉽게 액세스할 수 있도록 해줍니다.

* [조각 XDP 확인](/help/forms/using/assembler-service.md#resolve-references-on-crx-repository-resolve-references-on-crx-repository): 이제 OSGi의 AEM Forms이 기본 XDP에서 참조되고 AEM CRX 저장소에 저장된 조각 XDP를 확인합니다.

* [PDF/A 규정 준수 개선 사항](/help/forms/developing/pdf-a-documents.md#converting-documents-to-pdfa-documents-converting-documents-to-pdf-a-documents): 이제 PDF은 보관용으로 PDF/A 형식(1a, 2a, 3a)으로 전환하면서 접근성을 보장하고 이러한 표준 준수를 확인할 수 있습니다.

* **정적 PDF 문서의 글꼴 자동 크기 조정 지원**: AEM Forms Designer, OutputService 및 FormsService는 이제 정적 PDF의 글꼴 자동 크기 조정을 지원합니다. 텍스트 필드, 숫자 필드, 암호 필드 또는 날짜/시간 필드와 같은 필드의 템플릿에서 글꼴 크기 0을 언급하는 경우 필드 자체의 크기를 변경하지 않고 글꼴 크기가 이러한 필드 내에서 자동으로 조정됩니다. 기능을 사용하려면 사용자가 사용자 지정 xci에 플래그를 전달합니다. `<behaviorOverride>patch-LC-3921991:1</behaviorOverride>`.

<!-- * _6.5.21.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

### Sites {#sites}

[이제 기능 팩의 응용 프로그램에서 headless 사용 사례에 대해 AEM 6.5에서 유니버설 편집기](/help/sites-developing/universal-editor/introduction.md)를 사용할 수 있습니다.

### [!DNL Assets]

이제 IPTC 탭에서 [!UICONTROL 대체 텍스트] 및 [!UICONTROL 확장 설명] 텍스트 필드를 지원합니다. (ASSETS-34918)

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## 서비스 팩 22의 문제가 해결되었습니다. {#fixed-issues}


### [!DNL Sites]{#sites-6522}


#### 접근성 {#sites-accessibility-6522}

* 주석 견본 선택기 단추에 액세스 가능한 이름이 없습니다. 즉, 화면 판독기를 사용하면 새로운 16진수 값을 입력한 후 선택할 단추에 대해 사람이 인식할 수 있는 이름이 없습니다. (SITES-11992)
* 왼쪽 레일 메뉴의 다음 요소는 목록처럼 표시되지만 화면 판독기에 이와 같이 표시되지 않습니다.

   * Site
   * Live Copy
   * 실행
   * 언어 복사
   * 폴더
   * CSV 보고서(SITES-2874)

* AEM Core Web Content Management를 사용하려면 리치 텍스트 편집기에서 하이퍼링크에 대한 접근성 레이블이 필요합니다. 텍스트 구성 요소에서 하이퍼링크를 사용하는 경우 앵커 태그에는 `aria-label` 특성이 포함되어야 화면 판독기에서 접근성을 위해 링크 텍스트를 정확하게 읽고 전달할 수 있습니다. (SITES-11511)
* AEM에서 목록 보기의 테이블 헤더에 있는 대화형 요소에는 필수 &quot;버튼&quot; 역할이 없습니다. 따라서 NVDA 화면 판독기는 제목, 이름, 수정됨, 게시됨, 미리보기, 템플릿, 작업, 워크플로우 테이블 헤더에 대한 예상 단추 역할을 알리지 않습니다. NVDA와 같은 보조 기술과의 호환성을 위해서는 테이블 헤더의 각 대화형 요소에 &quot;버튼&quot; 역할을 할당해야 합니다. (SITES-10962)


#### 관리 사용자 인터페이스{#sites-adminui-6522}

* AEM의 일부 인스턴스에서 버전 미리 보기 및 비교 기능이 여러 페이지에서 예상대로 작동하지 않았습니다. 특히:

   * **미리 보기 문제:** 페이지 버전을 미리 보려고 하면 처음에 오류가 나타납니다. 다시 시도하면 미리보기가 빈 페이지로 표시됩니다.
   * **버전 비교 문제:** &quot;현재 항목에 비교&quot; 기능은 버전 간의 차이점을 강조 표시하지 않고 현재 버전만 표시합니다. (SITES-23988)

* 복사 및 붙여넣기 작업 중에 `plaintext`(으)로 설정된 `defaultPasteMode`을(를) 사용할 때 예기치 않은 `<br>` 태그가 RTE(리치 텍스트 편집기) 필드에 나타납니다. 이 문제로 인해 동일한 콘텐츠에 대해 서로 다른 마크업이 생성되므로 고객의 번역 메모리에서 동일한 텍스트 콘텐츠가 두 번 번역됩니다. (SITES-23606)
* AEM 6.5.20.0에서 **게시 관리** 기능에 기능 문제가 발생했습니다. 노드를 선택하고 나중에 게시하도록 예약할 때 하위 노드를 포함하려고 할 때 &quot;선택한 항목에 대한 하위 리소스를 검색하지 못했습니다&quot; 오류 메시지가 나타날 수 있습니다. 이 문제로 인해 **하위 항목 포함** 옵션의 사용이 차단되어 의도한 콘텐츠 계층 구조가 완전히 게시되지 않았습니다. (SITES-23000)
* 템플릿이 게시 인스턴스에 성공적으로 복제되었는데도 템플릿의 &quot;게시된&quot; 타임스탬프가 작성자 환경에서 업데이트되지 않았습니다. 작성자 인스턴스의 타임스탬프가 최신 게시를 반영하도록 예상되었지만 이 업데이트가 의도한 대로 발생하지 않았습니다. (SITES-21585)
* AEM 작성 환경에서 들어오는 링크의 수가 일치하지 않습니다. 왼쪽 레일은 클래식 UI에 비해 링크가 더 적었습니다. 또한 합법적인 일부 수신 링크도 작동하지 않습니다. (SITES-24837)
* AEM의 타임라인 보기에서 페이지 버전을 볼 때 매우 긴 로드 시간이 보고되었습니다. 버전을 표시하는 데 최대 19분이 소요되었습니다. 이 문제는 AEM 6.4.8에서 6.5.18로 업그레이드한 이후 계속 발생했으며 이로 인해 워크플로우 효율성이 크게 저하되었습니다. (SITES-22468 및 SITES-22467)

<!-- #### Classic UI{#sites-classicui-6522} 

* A -->


#### [!DNL Content Fragments]{#sites-contentfragments-6522}

* 업그레이드된 AEM 6.5.17에서 콘텐츠 조각을 저장하면 다음 오류가 발생했습니다. *오류: 콘텐츠 조각을 저장할 수 없습니다.*(SITES-22993)
* AEM의 게시자에서 `ContentFragmentModelOmniSearchHandler`의 닫히지 않은 리소스 확인자로 문제가 확인되었습니다. (SITES-24903)


#### [!DNL Content Fragments] - 관리자{#sites-admin-6522}

이메일 알림에서 링크를 클릭하면 사용자가 기본 에셋 뷰어 또는 편집기로 이동합니다. 워크플로우의 에셋이 콘텐츠 조각으로 결정된 경우에도 콘텐츠 조각 편집기 대신 이 작업을 수행합니다. (SITES-24338)


#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6522}

여러 줄 텍스트 필드 항목과 함께 컨텐츠 조각을 사용하는 경우 GraphQL을 사용하여 쿼리할 때 생성된 마크업이 HTML에 지정된 형식을 유지하지 않았습니다. 예를 들어 목록 뒤에 새 줄이 없습니다. 마지막 단락이 목록의 일부가 된 영향이 있었습니다. (SITES-23233)


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6522}

* A


#### [!DNL Content Fragments] - REST API{#sites-restapi-6522}

* A -->

#### 핵심 백엔드{#sites-core-backend-6522}

* AEM 작성자 인스턴스에 대해 `SegmentNotFoundException`개의 반복 오류가 보고되었습니다. 작성자를 다시 시작하면 문제가 일시적으로 해결되었지만 더 이상 발생하지 않도록 장기간 수정해야 했습니다. (SITES-22573)
* AEM Sites의 타임라인 기능, 특히 주석에서 누락된 `cq:lastModified` 속성을 처리하는 것과 관련하여 문제가 발생했습니다. AEM 6.5.20을 적용한 후에는 기존 콘텐츠에 누락된 속성에 대한 수정이 필요한지 또는 속성 없이 올바르게 작동하도록 타임라인이 업데이트되었는지 불확실성이 있었습니다. (SITES-21861)


#### 핵심 구성 요소{#sites-core-components-6522}

* AEM 6.5.18에서 6.5.21로 업그레이드한 후 구성 요소의 라이브 사용을 확인하는 기능에서 문제가 발견되었습니다. 라이브 사용량 페이지에서 추가 항목을 스크롤하려고 할 때 UI에 &quot;추가 항목 로드&quot;가 표시되었는데도 테이블이 더 많은 결과를 로드하지 못했습니다. (SITES-23919)
* 두 개의 탭이 포함된 AEM 구성 요소 대화 상자의 필수 필드 유효성 검사에서 문제가 보고되었습니다. 탭 1에는 리치 텍스트 편집기(RTE) 및 텍스트 필드가 포함되었으며 탭 2에는 경로 필드 및 텍스트 필드가 있습니다. 모든 필드가 필수(`required=true`)로 표시되지만 모든 필수 필드를 채운 후에도 탭 1에서 오류 알림이 올바르게 유지되지 않습니다. 반면 탭 2의 오류는 예상대로 지워졌습니다. (SITES-23243)
* AEM 6.5.21로 마이그레이션한 후 HTML 템플릿 언어 `data-sly-include` 문이 더 이상 예상대로 작동하지 않습니다. 특히 `appendPath` 및 `prependPath` 표현식을 지원하지 않습니다. 따라서 마이그레이션 전에 포함된 리소스의 출력이 올바르게 작동했더라도 제대로 렌더링되지 않았습니다. 이 문제로 인해 경로 조작을 위해 이러한 표현식을 사용하는 리소스에 대한 렌더링 오류가 발생했습니다. (GRANITE-52970)


<!-- #### Campaign integration{#sites-campaign-integration-6522}

* A -->


#### 경험 조각{#sites-experiencefragments-6522}

* 경험 조각은 목록 보기에서 **제목** 열 헤더를 클릭했을 때 예상대로 제목별로 정렬되지 않습니다. 화면이 빠르게 깜박이지만 정렬되지는 않습니다. (SITES-23706)

* AEM 6.5.17에서 기본 기능을 사용하여 페이지 구성 요소를 경험 조각으로 변환할 때 문제가 발생했습니다. 전환 후 경험 조각이 사용된 페이지에 올바르게 표시되더라도 편집하는 동안 경험 조각이 비어 있는 것으로 표시됩니다. 구성 요소 노드가 루트/컨테이너 노드 외부에 배치되면서 템플릿의 구조를 위반하는 잘못된 노드 생성으로 문제가 발생했습니다. 조각의 편집성을 복원하려면 구성 요소 노드를 올바른 루트/컨테이너 노드로 수동으로 이동해야 합니다. (SITES-22974)

* AEM 6.5.11에서 6.5.20으로 마이그레이션한 후 경험 조각의 클라우드 구성이 올바르게 저장되지 않았습니다. 구성이 `crx/de`에 저장된 것으로 표시되었지만 구성 콘솔을 다시 열 때 지속성에 문제가 있음을 나타내는 구성이 표시되지 않습니다. (SITES-22287)


<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6522}

* A -->


#### 론치{#sites-launches-6522}

AEM 프로덕션에서 태그 지정 필터를 사용하여 경험 조각 에셋을 추가할 때 사용자가 선택할 수 있지만 **언어 사본 만들기**&#x200B;를 선택한 후 오류가 발생했습니다. 예상 동작은 태깅 필터에서 선택한 경험 조각 에셋이 번역 프로젝트에 추가되어야 하는 것입니다. (SITES-24152)

#### 링크 확인{#sites-link-checker-6522}

HTTP 클라이언트가 기본 인증 전에 NTLM을 시도하므로 LinkCheckerTask가 인증에 실패하여 프록시가 여러 번 실패한 후 사용자를 차단합니다. 대신 LinkCheckerTask 서비스가 올바르게 작동할 수 있도록 하기 위해 시스템은 기본 인증을 사용하여 프록시를 인증해야 합니다. (SITES-25034)


#### MSM - 라이브 카피{#sites-msm-live-copies-6522}

* SEO Robots 태그를 기본 복사본에 적용하고 Live Copy 페이지로 롤아웃하면 값이 `crx/de`에 올바르게 표시됩니다. 하지만 이 값은 라이브 카피 페이지의 페이지 속성 아래의 사용자 인터페이스에 반영되지 않았습니다. (SITES-23475)
* 사용자 인터페이스를 통해 론치를 홍보하려고 할 때 론치와 관련된 오류가 발생했습니다. 론치 홍보 마법사가 비어 있어 홍보 프로세스가 완료되지 못했습니다. (SITES-19718)
* 라이브 카피를 만들고 롤아웃을 수행하려고 시도한 후 AEM의 경험 조각에서 문제가 발생했습니다. 사용자가 롤아웃 화면에서 경험 조각 관리 화면으로 다시 이동하는 동안 `NotFound` 오류가 발생하는 문제가 발생했습니다. (SITES-21933)


#### 페이지 편집기{#sites-pageeditor-6522}

* 실행 취소 단추를 사용하면 텍스트가 마지막 버전으로 변경될 뿐만 아니라 구성 요소의 위치도 변경됩니다. (SITES-17465)
* 복사된 컨테이너 구성 요소를 붙여넣으면 두 번 시각적으로 표시되어 페이지에 세 개의 인스턴스가 발생합니다. 그러나 페이지를 새로 고친 후 중복 항목이 사라져 일시적인 시각적 결함일 수 있습니다. (SITES-21890)
* 키보드의 Tab 키 또는 Shift+Tab 키를 사용하여 구성 요소 왼쪽 창을 탐색하는 동안 여러 텍스트 요소가 시각적 및 탭 모드에서 모두 명확하게 표시되지 않았습니다. 이 문제는 접근성에 영향을 주어 키보드 탐색 중에 이러한 구성 요소를 식별하거나 상호 작용하기 어렵게 했습니다. (SITES-2266)

#### 복제{#sites-replication-6522}

AEM 6.5.18과 6.5.19에서 상위 페이지를 비활성화하면 각 하위 페이지에 대해 여러 비활성화 요청이 생성되었습니다. 이 문제로 인해 GraphQL 엔드포인트의 벌크 게시 취소도 중단되었습니다. (NPR-42075 및 NPR42010)


### [!DNL Assets]{#assets-6522}

* 연결된 Assets 기능을 사용하는 동안 AEM Assets에서 수행한 업데이트는 AEM Sites 환경에 반영되지 않습니다. (ASSETS-42344)
* Experience Manager 내에서 자산을 한 위치에서 다른 위치로 이동할 때 자산 게시 상태에 문제가 발생합니다. (ASSETS-41158)
* API를 사용하여 자산을 업로드하면 `unclosed resource resolver` 오류 메시지가 표시됩니다. (ASSETS-41049)
* Adobe Experience Manager, 서비스 팩 21로 업그레이드한 후 `AssetReferenceResolverImpl` 참조 쿼리에 문제가 있습니다. (ASSETS-40384)
* AEM 버전 6.5.19에서는 검색 패널 결과에서 한 가지 옵션을 제거하는 동안 사용 가능한 다른 모든 확인란도 선택 취소합니다. (ASSETS-37335)
* 일괄 메타데이터 내보내기 작업을 수행하는 동안 정크 값이 Excel 출력에 표시됩니다. (ASSETS-37260)
* AEM 버전 6.5.19에서 SVG 파일을 UTF-8 포맷으로 업로드할 때 출력이 흐리게 표시됩니다. (ASSETS-36616)
* 연결된 Assets 구성 내에 `Fetch original rendition for Dynamic Media Connected Assets` 옵션이 없습니다. (ASSETS-41726)
* 필수 필드에 대한 값을 정의하지 않아도 자산 속성이 저장됩니다. (ASSETS-37914)
* 에셋의 처리 상태가 실패 또는 메타데이터 실패인 경우 캡션 및 오디오 트랙 UI가 제대로 작동하지 않습니다. (ASSETS-37281)
* 에셋 메타데이터를 저장하고 편집하려고 하면 언어 이름이 표시되지 않습니다. (ASSETS-37281)

#### [!DNL Dynamic Media]{#assets-dm-6522}

프로덕션 문제로 인해 Dynamic Media에 비디오를 업로드하지 못하여 사용자 인터페이스에 프로세스 실패 오류가 표시되면서 마이그레이션 프로세스가 중단되었습니다. (ASSETS-36038)

<!--

### [!DNL Forms]{#forms-6522}

Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.22.0 Forms add-on package release is scheduled for Thursday, November 28, 2024. A list of Forms fixes and enhancements is added to this section post the release.

-->

### Forms {#forms-bug-fixes-sp22}

* AEM Forms에 저장된 초안의 첨부 파일에 대해 생성된 URL이 구성된 Apache Sling Resource Resolver Factory 매핑을 반영하지 않습니다. (FORMS-16949)
* AEM Forms 서비스 팩 19(6.5.19.0)의 사용자가 문자를 미리 볼 때 공백이 없고 &#39;&#39;x&#39; 문자가 일부 위치에 표시되므로 콘텐츠가 제대로 정렬되지 않습니다. (FORMS-16670)
* AEM Forms 서비스 팩 18(6.5.18.0)의 사용자가 CIF 프로토콜을 사용하여 파일을 인쇄하려고 할 때 실패하고 다음과 같은 오류가 표시됩니다. (FORMS-16629)
  `ALC-OUT-001-401: Unknown error while printing using CIFS on the Printer: \\\\\\\\NSMVPLUETEST01\\\\TH_Test`
* 사용자가 AEM Forms 서비스 팩 17(6.5.17.0)에서 AEM Forms 서비스 팩 20(6.5.20.0)으로 업그레이드할 때 규칙 편집기 아이콘이 양식 컨테이너 수준에 표시되지 않습니다. (FORMS-16430)
* 사용자가 AEM Forms 서비스 팩 17(6.5.17.0)에서 AEM Forms 서비스 팩 21(6.5.21.0)로 업그레이드할 때 수정된 적응형 양식 제출 URL 경로가 작동하지 않습니다. (FORMS15894)
* AEM Forms 서비스 팩 19(6.5.19.0)에서 `creation date and modification date mismatch with timezone` 오류가 있는 특정 파일에 대해 AEM Forms 6.5 PDF/A 유효성 검사가 실패하고, 준수 검사에 대한 Acrobat Pro PDF/A 유효성 검사에서 원활하게 실행됩니다. (FORMS-15840)
* 사용자가 OSGi의 AEM Forms 서비스 팩 15(6.5.15.0)에서 사이트 페이지의 &quot;초안 및 제출&quot; 구성 요소를 사용하여 양식 초안을 삭제하면 삭제가 실패합니다. (FORMS-15755)
* 사용자에게 999개가 넘는 항목이 있는 SharePoint 목록이 있고 양식에 첨부 파일이 포함되어 있으면 양식 제출이 실패합니다. (FORMS-15057)
* 사용자가 시작 날짜 및 종료 날짜로 레이블이 지정된 두 개의 날짜 선택기 구성 요소를 사용할 때, 종료 날짜가 시작 날짜보다 빠르지 않은지 확인하는 유효성 검사 규칙을 추가하고 사용자 지정 스크립트 유효성 검사 메시지를 설정한 후 종료 날짜가 시작 날짜보다 빠를 경우 유효성 검사가 트리거되지 않습니다. (FORMS-14757)
* 사용자가 적응형 양식의 테이블에서 표시 및 숨기기 기능을 사용하면 필드 크기가 줄어듭니다. 필드 크기는 행 추가 및 제거 시 자체적으로 수정됩니다. (FORMS-14756)
* 사용자가 AEM Forms 서비스 팩 19(6.5.19.0)에서 양식을 인쇄할 때 일부 양식이 서버에서 올바르게 렌더링되지 않아 인쇄 프로세스 중에 오류가 발생합니다. (FORMS14734)
* 사용자가 AEM Forms 서비스 팩 15(6.5.15.0)에서 AEM Forms 서비스 팩 19(6.5.19.0)로 업데이트하고 특정 변수가 숫자로 설정되고 사용자 지정 표시 패턴이 num{$zzz,zz9.99}(으)로 설정된 양식을 사용할 때 미리보기 및 에이전트 UI에서 패턴이 올바르게 렌더링되지 않습니다. (FORMS-14694)
* 사용자가 저장된 데이터 xml이 있는 대화형 통신에서 문자를 미리 보면 문자가 AEM UI의 &quot;로드 중&quot; 상태에서 멈춥니다. 동일한 XML을 사용하여 편지 미리 보기를 다시 해도 잘 작동합니다. (FORMS-14521)
* AEM Forms 서비스 팩 20(6.5.20.0)의 사용자가 적응형 양식의 &#39;이메일 보내기&#39; 제출 액션 단추를 사용하여 첨부 파일이 있는 이메일을 보내면 첨부 파일 이름이 인라인이 아닌 다음 줄에 나타납니다. (FORMS-14426)
* PDF이 AEM Forms에서 글머리 기호 목록이 기본 &quot;디스크&quot; 스타일로 설정된 PDF을 생성하면 Adobe Acrobat의 접근성 도구에서 접근성 검사를 실패합니다. 글머리 기호 및 사각형 스타일이 포함된 목록은 접근성 검사를 통과합니다. (FORMS-13802, LC-3922179)
* 사용자가 독립형 RHEL8 JBoss 설정에서 AEMForms-6.5.0-0065에서 AEMForms-6.5.0-0087로 업그레이드할 때 LiveCycle 서비스 컨테이너와 연결하지 못합니다. (FORMS-15907) ·
* JEE의 AEM Forms에서 사용자가 이전에 제출한 양식을 선택하고 새 양식 프로세스를 시작할 때 AEM Workspace에서 미리 채워진 데이터 프로세스가 있는 양식은 이전 양식에 수동으로 입력된 필드를 유지하지 않고 이전에 제출된 모든 데이터를 지우고 미리 채워진 데이터로 대체합니다. (FORMS-15376)
* AEM Forms 서비스 팩 20(6.5.20.0)에서 사용자가 PDFG 서비스를 사용하여 Tiff 파일을 PDF으로 변환할 때 다음 오류와 함께 실패합니다. (FORMS-14879) 입력 이미지 파일을 PDF으로 변환하는 동안 ALC-PDG-011-028-Error 가 발생했습니다. com/sun/image/codec/jpeg/JPEGCodec
* AEM Forms on JEE jar 파일의 업그레이드: 이제 다음과 같은 다양한 AEM Forms JEE 작업에서 종속성 확인 및 기능을 개선하기 위해 `commons-collections:commons-collections:jar` 라이브러리가 포함됩니다.
   * 작업 처리 및 오류 처리를 개선하기 위한 어셈블러 작업 개선 사항.
   * PDF Generator(PDFG) 작업을 개선하여 문서 생성 및 전환을 위한 작업을 더욱 원활하게 수행할 수 있습니다.
   * 버전 간의 안정적인 전환을 보장하면서 업그레이드 프로세스를 개선하기 위한 LC-업그레이드 작업 개선.
   * 문서 처리 및 향상된 권한 관리 기능을 보호하기 위한 Rights Management 작업 개선 사항입니다.
   * 보다 안정적인 작업 처리 및 시스템 관리를 위한 프로세스 관리 작업 개선.


#### XMLFM {#forms-xmlfm-sp22}

* AEM Forms 서비스 팩 21(6.5.21.0)에서 사용자가 XMLFM을 사용하여 PDF에 비표준 태그를 추가하면 문서가 PDF 사양 요구 사항을 준수하지 못합니다. (LC-3922484)
* 사용자가 AEM Forms 서비스 팩 20의 출력 서비스(6.5.20.0)를 사용하여 PDF을 생성하면 CORBA.COMM_FAILURE로 실패하고 `15:04:35,973 ERROR [com.adobe.formServer.PA.XMLFormAgentWrapper] (default task-14) ALCOUT-002-013: XMLFormFactory, PAexecute failure: "org.omg.CORBA.COMM_FAILURE"` 오류가 표시됩니다. 접근성 역할 &quot;참조&quot;가 XDP 템플릿의 하위 양식에서 제외되면 서비스가 정상적으로 전달됩니다. 그러나 508 규정 준수를 위해서는 이 역할이 필요합니다. (LC-3922402)
* 사용자가 XFA 양식을 AcroForm PDF으로 변환할 때 실패합니다. (LC-3922363)
* AEM Forms 서비스 팩 19(6.5.19.0)에서 사용자가 명명되지 않은 하위 양식으로 XDP를 만들면 명명되지 않은 하위 양식에 대해 FS_DATA_SOM이 비어 있는 것으로 표시됩니다. (LC-3922034)

#### Forms Designer {#forms-designer-sp22}

* 사용자가 AEM Forms Designer 버전 6.5.21.0에서 조각 폴더를 선택하여 조각 라이브러리를 열면 충돌합니다. (LC-3922439)
* 사용자가 32비트 AEM Forms Designer 버전 6.5.20.0을 제거하고 AEM Forms Designer 버전 6.5.21.0을 설치하면 Forms Designer을 시작할 수 없습니다. 오류 로그에 JRE(Java Runtime Environment)에 대한 메모리 할당이 충분하지 않은 것으로 표시됩니다. (LC-3922404)
* 사용자가 AEM Forms Designer 버전 6.5.20.0을 설치한 후 매크로 옵션이 메뉴에 나타나지 않고 기본 &#39;접근성 검사&#39; 매크로만 나타나고 실행되지 않습니다. (LC-3922321)
* 사용자가 AEM Forms Designer 버전 6.5.20.0에서 XDP를 생성하는 새 템플릿 위치를 추가하면 Forms Designer이 충돌합니다. (LC-3922316)
* 사용자가 AEM Forms 6.5 서비스 팩 15(6.5.15.0) OSGI에서 ExportData 메서드를 사용하여 출력을 생성하면 불완전하고 잘못된 데이터가 생성됩니다. (LC-3922340)


<!-- #### [!DNL Adaptive Forms] {#forms-6522}

* A


#### [!DNL Forms Designer] {#forms-designer-6522}

* A -->


### Foundation {#foundation-6522}

AEM Assets 콘솔에서 DITA 문서의 순서를 변경하려고 할 때 문제가 발생했습니다. 경로 브라우저 대화 상자 맨 위에 있는 이동 경로에 루트 상위 항목에 대한 노드 제목 대신 노드 이름이 잘못 표시됩니다. 이동 경로 내에서 항목을 선택한 후에만 올바른 노드 제목이 나타나며 이는 일시적인 표시 오류를 나타냅니다. (NPR-42106)


<!-- #### Apache Felix {#foundation-apachefelix-6522}


* A

#### Campaign{#foundation-campaign-6522}

* A


#### Cloud Services{#foundation-cloudservices-6522}

* A -->


#### 커뮤니티 {#foundation-communities-6522}

AEM 6.5.19에서 6.5.20으로 업그레이드한 후 `UgcSearch` 호출 후 `Connection evic` 스레드가 제대로 닫히지 않는 문제가 발생했습니다. 프로덕션 환경에서 관찰되는 이 문제는 이러한 스레드가 시간이 지남에 따라 지속되고 누적되어 성능에 영향을 줄 수 있습니다. (NPR-42019)


<!-- #### Content distribution{#foundation-content-distribution-6522}

* A -->


#### CRX {#foundation-crx-6522}

* 정렬이 CRX 패키지 관리자의 왼쪽 메뉴에서 **그룹**&#x200B;에 따라 작동하지 않습니다. (GRANITE-53277)
* AEM의 패키지 관리자는 기본적으로 더 낮은 패키지 버전의 설치를 제한하지만 이전 버전의 강제 설치를 허용합니다. 그러나 강제 설치 옵션을 사용하면 표준 파이프라인을 통한 향후 설치를 방해할 수 있습니다. 예를 들어 버전 1.21이 설치되어 있고 버전 1.24가 추가되면 설치가 성공하여 두 버전이 모두 나열됩니다. 그러나 버전 1.22 이상 1.24를 설치하려고 하면 파이프라인을 통해 실패하지만 강제로 설치되면 작동하여 모든 버전을 나열합니다. 마찬가지로, 파이프라인에서 다운그레이드를 허용하지 않으므로 버전 1.24가 이미 있는 경우 버전 1.23 설치가 차단됩니다. (GRANITE-53263)


#### Granite{#foundation-granite-6522}

* CURL 명령을 사용하여 AEM에 스냅샷 패키지를 설치하고 있었습니다. 설치하는 동안 JCR 설치 프로그램은 OSGI 설치 관리자를 통해 패키지를 스캔하여 추가 OSGI 번들 또는 구성이 필요하지 않은지 확인합니다. 패키지 버전에 &quot;SNAPSHOT&quot;이 포함된 경우 OSGI 설치 관리자가 VLT를 트리거하여 해당 스냅샷 패키지를 생성했습니다. 그러나 각 AEM 작성자 인스턴스는 자체 OSGI 설치 관리자를 실행하므로 두 인스턴스가 동시에 스냅샷 생성을 시도하여 저장소 내에서 세션 충돌이 발생할 수 있습니다. (NPR-42003)
* `ScriptDependencyResolver`에 AEM 6.5.21과 잠금 경합이 있습니다. (GRANITE-53181)
* AEM을 6.5.21로 업그레이드한 후 `data-sly-use`과 같이 상대 경로를 HTL(Sightly) 구문에 사용할 때 문제가 발생했습니다. (GRANITE-53080)


#### 통합{#foundation-integrations-6522}

* Cloud Service 사용자 인터페이스에 대한 법적 속성 문을 추가했습니다. (FORMS-16373)
* **fd-cloudservice** 사용자가 hCaptcha 및 Turnstile 구성에 액세스할 수 있는 읽기 권한을 추가하여 captcha 렌더링 및 유효성 검사에 필요한 클라이언트 ID 및 클라이언트 암호를 검색할 수 있도록 합니다. 또한 이러한 구성에 대한 액세스를 관리하기 위해 액세스 제어 목록 모델을 구현했습니다. (FORMS-16360)


#### 현지화{#foundation-localization-6522}

![Hammer 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) 도구 > **보안** > ![사용자 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_User_18_N.svg) **사용자**&#x200B;에서 사용자 관리 페이지의 **상태** 열에 있는 데이터가 세로로 표시되었습니다. (GRANITE-48304)


<!-- #### Oak {#foundation-oak-6522}

* A -->


#### Platform{#foundation-platform-6522}

* AEM 6.5.18에 도입된 엔터프라이즈 정보 관리 추적으로 인해 제품 채택 점수를 계산하는 데 예외 항목이 발생했습니다. Adobe 지표 라이브러리는 Omega 추적 라이브러리에서 제공한 사용자 데이터를 덮어써서 이 문제를 일으켰습니다. 그 결과 2024년 2월부터 많은 AEM Sites 및 AEM Assets 고객의 채택 점수가 0점으로 하락했습니다. (CQ-4358438)
* 프로덕션 환경에서 가비지 수집기가 태그를 잘못 처리하는 문제가 발견되었습니다. 특히 태그를 이동하거나 이름을 변경하면 가비지 수집기가 `cq:MovedTo` 속성을 업데이트하지 못해 태그가 페이지에서 사라집니다. (CQ-4358293)
* AEM 6.5.19의 ContextHub 문제로 인해 컨텍스트 경로가 AEM 인스턴스에 추가될 때 세그먼트가 잘못 해결되었습니다. 이 문제는 특히 페이지 구성 요소에 의해 생성된 JavaScript 오브젝트 내의 URL 필드에 영향을 미쳤습니다. 여기서 필요한 컨텍스트 경로 접두어가 누락되었습니다. 이 생략으로 인해 세그먼트가 예상대로 작동하지 않았습니다. (SITES-21852)
* `commons-collections-3.2.2-adobe-2` 라이브러리를 사용하도록 AEM 빠른 시작을 업데이트했습니다. 업데이트를 통해 애플리케이션이 계속 원활하게 실행될 수 있습니다. (NPR-42150)
* AEM 6.5의 SMTP OAuth2 설정은 AEM as a Cloud Service에서 사용되는 설정과 크게 다릅니다. 구성을 간소화하고 일관성을 보장하기 위해 AEM 6.5의 설정은 AEM as a Cloud Service에서 사용되는 표준과 일치해야 했습니다. (GRANITE-53273)
* ![나침반 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Compass_18_N.svg) > ![프로젝트 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Project_18_N.svg) 프로젝트를 클릭한 후 마우스 포인터를 ![왼쪽 레일 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg) ![아래쪽 화살표 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) 위로 가져가면 도구 설명 텍스트 &quot;콘텐츠만&quot; 앞에 심각한 악센트가 나타납니다. (CQ-4356633)

#### 보안{#foundation-security-6522}

* AEM의 오래된 JSAFE 암호화 라이브러리(버전 6.0.0)에서 문제가 발생했습니다. JSAFE 버전 6.2.5의 패치 번들은 AEM 6.5.22에 포함되어 있습니다. (NPR-42006)
* XSS 확인 중에 허용된 프로토콜의 유효성을 검사할 때 처리기는 &quot;http&quot; 및 &quot;https&quot;와 비교합니다. 그러나 URL 개체의 `protocol` 속성은 `http:` 및 `https:`과 같은 후행 콜론으로 이러한 값을 반환했습니다. 이 불일치로 인해 유효성 검사 문제가 발생했습니다. 정확한 구문 분석을 위해 콜론을 설명하거나 비교 논리를 적절하게 조정하는 데 프로토콜 검사가 필요합니다.  (NPR-42119)
* IBM® WebSphere® Liberty Profile 및 Semeru Java 8.0에 AEM 6.5.21(이전 버전은 AEM 6.5.19)을 설치한 후 페이지를 열 수 없었습니다. 오류 로그에 다른 번들이 필요한 서블릿 버전과 관련된 문제가 표시되었습니다. 이 문제를 해결하려면 `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`에 대한 종속성이 문제와 관련되어 있으므로 되돌려야 합니다. (NPR-42116)
* 여러 브라우저에서 쿠키에 대한 사이트 간 액세스를 허용하는 데 사용되는 **SameSite=None** 쿠키에 대한 지원을 단계적으로 중단하고 있습니다. 또는 **분할된 쿠키**&#x200B;를 도입하고 있습니다. 이러한 쿠키는 쿠키가 사용되는 컨텍스트에 따라 스토리지를 격리하므로 사이트 간 추적을 방지하고 포함된 타사 컨텐츠와 같은 특정 파티션 내에서 쿠키가 작동할 수 있도록 하여 개인정보 및 보안을 향상시킵니다. (GRANITE-51953)


<!-- #### Sling{#foundation-sling-6522}

* A -->


#### 번역{#foundation-translation-6522}

* 핵심 구성 요소의 최근 변경 사항에 대한 지원을 기본 번역 규칙에 추가했습니다. (NPR-42029)
* AEM Forms에서 XLIFF 파일을 내보내는 중 문제가 발견되었습니다. **선택 항목을 XLIFF로 내보내기(문자열만)** 옵션을 사용할 때 구성 요소 시퀀스가 일관되게 유지되지 않았습니다. 그러나 특정 언어에 대해 XLIFF를 내보낼 때는 시퀀스가 올바르게 유지됩니다. 문제를 입증하기 위해 두 개의 파일이 제공되었습니다. **DE-CH_Export.xliff**(올바른 시퀀스) 및 **String_Export.xliff**(잘못된 시퀀스). (NPR-42118)


#### 사용자 인터페이스{#foundation-ui-6522}

* `coralui-component-dialog`이(가) `cq-dialog-actions`의 배치를 변경했습니다. AEM의 대화 상자 내 작업 버튼의 레이아웃이나 동작에 영향을 미칠 수 있습니다. (NPR-42294)
* AEM의 색상 피커 기능이 제대로 작동하지 않습니다. 액세스하면 빈 모달이 표시되어 색상을 선택할 수 없습니다. 이 문제는 AEM 6.5.20을 스테이지 환경에 설치한 후 시작되었습니다. 업데이트에 대해 색상 선택기가 올바르게 *이전*&#x200B;에 작동했습니다. (NPR-42163)
* ![망치 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) **도구** > **워크플로** > **모델** > 모델 선택 > **워크플로 시작**&#x200B;에서 찾아보기 아이콘이 **워크플로 실행** 대화 상자의 페이로드 필드에 없습니다. (NPR-42162)


<!-- #### WCM{#foundation-wcm-6522}

* A


#### Workflow{#foundation-workflow-6522}

* A -->


## [!DNL Experience Manager] 6.5.22.0 설치{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.22.0에는 [!DNL Experience Manager] 6.5가 필요합니다. 자세한 지침은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하세요. <!-- UPDATE FOR EACH NEW RELEASE -->
* 서비스 팩을 Adobe [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip)에서 다운로드할 수 있습니다.
* MongoDB 및 여러 인스턴스가 있는 배포에서 패키지 관리자를 사용하여 작성자 인스턴스 중 하나에 [!DNL Experience Manager] 6.5.22.0을(를) 설치합니다.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe은 [!DNL Experience Manager] 6.5.22.0 패키지를 제거하거나 제거하지 않는 것이 좋습니다. 따라서 팩을 설치하기 전에 `crx-repository`을(를) 롤백해야 하는 경우 백업을 만들어야 합니다. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### [!DNL Experience Manager] 6.5에 서비스 팩 설치{#install-service-pack}

1. 인스턴스가 업데이트 모드에 있는 경우(인스턴스가 이전 버전에서 업데이트된 경우) 설치 전에 인스턴스를 다시 시작하십시오. Adobe은 인스턴스의 현재 가동 시간이 높을 경우 다시 시작할 것을 권장합니다.

1. 설치하기 전에 [!DNL Experience Manager] 인스턴스의 스냅숏 또는 새 백업을 만듭니다.

1. [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip)에서 서비스 자루를 다운로드합니다. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 패키지 관리자를 연 다음 **[!UICONTROL 패키지 업로드]**&#x200B;를 선택하여 패키지를 업로드합니다. 자세한 내용은 [패키지 관리자](/help/sites-administering/package-manager.md)를 참조하세요.

1. 패키지를 선택한 다음 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

1. S3 커넥터를 업데이트하려면 서비스 팩을 설치한 후 인스턴스를 중지하고 기존 커넥터를 설치 폴더에 있는 새 이진 파일로 바꾼 다음 인스턴스를 다시 시작하십시오. [Amazon S3 데이터 저장소](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)를 참조하세요.

>[!NOTE]
>
>패키지 관리자 UI의 대화 상자가 서비스 팩을 설치하는 동안 종료되는 경우가 있습니다. 배포에 액세스하기 전에 오류 로그가 안정될 때까지 기다리는 것이 좋습니다. 업데이터 번들 제거와 관련된 특정 로그를 기다린 후 설치가 성공했는지 확인합니다. 일반적으로 이 문제는 [!DNL Safari] 브라우저에서 발생하지만 모든 브라우저에서 간헐적으로 발생할 수 있습니다.

**자동 설치**

[!DNL Experience Manager] 6.5.22.0.<!-- UPDATE FOR EACH NEW RELEASE -->을(를) 설치하는 데 사용할 수 있는 두 가지 메서드가 있습니다.

* 서버가 온라인 상태일 때 패키지를 `../crx-quickstart/install` 폴더에 넣습니다. 패키지가 자동으로 설치됩니다.
* 패키지 관리자에서 [HTTP API 사용](/help/sites-administering/package-manager.md#package-share). 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

>[!NOTE]
>
>Experience Manager 6.5.22.0은 Bootstrap 설치를 지원하지 않습니다. <!-- UPDATE FOR EACH NEW RELEASE -->

**설치 확인**

이 릴리스에서 사용할 수 있는 인증된 플랫폼을 확인하려면 [기술 요구 사항](/help/sites-deploying/technical-requirements.md)을 참조하세요.

1. 제품 정보 페이지(`/system/console/productinfo`)에는 [!UICONTROL 설치된 제품]에 업데이트된 버전 문자열 `Adobe Experience Manager (6.5.22.0)`이(가) 표시됩니다. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 모든 OSGI 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]**&#x200B;이거나 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 콘솔 사용: `/system/console/bundles`).

1. OSGi 번들 `org.apache.jackrabbit.oak-core`은(는) 버전 1.22.20 이상입니다(웹 콘솔 사용: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### [!DNL Experience Manager] Forms용 서비스 팩 설치{#install-aem-forms-add-on-package}

Experience Manager Forms에 서비스 팩을 설치하는 방법은 [Experience Manager Forms 서비스 팩 설치 지침](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)을 참조하십시오.

>[!NOTE]
>
>[AEM 6.5 QuickStart](https://experienceleague.adobe.com/ko/docs/experience-manager-65/content/implementing/deploying/deploying/deploy)에서 사용 가능한 적응형 양식 기능은 탐색 및 평가 목적으로만 사용하도록 설계되었습니다. 프로덕션 용도로 사용하려면 적응형 양식 기능에 적절한 라이선싱이 필요하므로 AEM Forms에 대해 유효한 라이선스를 확보해야 합니다.

### Experience Manager 콘텐츠 조각용 GraphQL 인덱스 패키지 설치{#install-aem-graphql-index-add-on-package}

GraphQL을 사용하는 고객은 GraphQL 색인 패키지 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip)을(를) 사용하여 [Experience Manager 콘텐츠 조각을 설치해야 합니다.

이렇게 하면 필요한 인덱스 정의가 실제로 사용하는 기능을 기반으로 추가할 수 있습니다.

이 패키지를 설치하지 않으면 GraphQL 쿼리가 느려지거나 실패할 수 있습니다.

>[!NOTE]
>
>이 패키지는 인스턴스당 한 번만 설치하십시오. 모든 서비스 팩으로 다시 설치할 필요는 없습니다.

### UberJar{#uber-jar}

[!DNL Experience Manager] 6.5.22.0용 UberJar를 [Maven 중앙 저장소](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.22/)에서 사용할 수 있습니다. <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Maven 프로젝트에서 UberJar를 사용하려면 [UberJar 사용 방법](/help/sites-developing/ht-projects-maven.md)을 참조하여 프로젝트 POM에 다음 종속성을 포함하십시오. <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.22</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar 및 기타 관련 아티팩트는 공개 Maven 저장소(`repo.adobe.com`) Adobe 대신 Maven 중앙 저장소에서 사용할 수 있습니다. 기본 UberJar 파일의 이름이 `uber-jar-<version>.jar`(으)로 바뀝니다. 따라서 `dependency` 태그에 대한 값으로 `apis`을(를) 가진 `classifier`이(가) 없습니다.


## 이제 사용되지 않는 기능과 제거된 기능{#removed-deprecated-features}

[사용되지 않거나 제거된 기능](/help/release-notes/deprecated-removed-features.md/)을 참조하세요.

## 알려진 문제{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.-->

<!-- * **Page publishing not working in Page Editor after upgrading to Service Pack 18 (6.5.18.0)** -->

<!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0 -->
<!-- After you upgrade an instance of AEM 6.5.0.0&mdash;6.5.17.0 to AEM 6.5.19.0, when you click **Publish Page** inside the Page Editor, you are redirected to a URL that does not exist.

  To work around this issue, do one of the following:

  * Remove the following "path" property.

       `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

  * Paste the correct URL directly into the browser.

       `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html` -->


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

   1. 서비스 팩을 설치하거나 Experience Manager as a Cloud Service 를 다시 시작합니다.
`cache` 및 `diff-cache`의 새 폴더가 자동으로 만들어지고 `error.log`에서 더 이상 `mvstore`과(와) 관련된 예외가 발생하지 않습니다.

* 콘텐츠 모델의 기본 이름을 대신 사용하도록 콘텐츠 모델에 대해 사용자 지정 API 이름을 사용했을 수 있는 GraphQL 쿼리를 업데이트합니다.

* GraphQL 쿼리에서 `fragments` 인덱스 대신 `damAssetLucene` 인덱스를 사용할 수 있습니다. 이 작업으로 인해 GraphQL 쿼리가 실패하거나 실행하는 데 시간이 오래 걸릴 수 있습니다.

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

  이러한 단계 후에는 GraphQL 쿼리가 더 빨리 수행됩니다.

* 콘텐츠 조각, 사이트 또는 페이지를 이동, 삭제 또는 게시하려고 할 때 콘텐츠 조각 참조를 가져올 때 문제가 있습니다. 백그라운드 쿼리가 실패합니다. 즉, 기능이 작동하지 않습니다.
올바른 작업을 위해 인덱스 정의 노드 `/oak:index/damAssetLucene`에 다음 속성을 추가해야 합니다(리인덱싱이 필요하지 않음).

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* [!DNL Experience Manager] 인스턴스를 6.5.0 - 6.5.4에서 Java™ 11의 최신 서비스 팩으로 업그레이드하는 경우 `error.log` 파일에 `RRD4JReporter` 예외가 표시됩니다. 예외를 중지하려면 [!DNL Experience Manager]의 인스턴스를 다시 시작하십시오. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 사용자는 [!DNL Assets]의 계층 구조에서 폴더의 이름을 바꾸고 중첩된 폴더를 [!DNL Brand Portal]에 게시할 수 있습니다. 그러나 루트 폴더가 다시 게시될 때까지 폴더의 제목이 [!DNL Brand Portal]에서 업데이트되지 않습니다.

* [!DNL Experience Manager] 6.5.x.x를 설치하는 동안 다음 오류 및 경고 메시지가 표시될 수 있습니다.
   * &quot;Target Standard API(IMS 인증)를 사용하여 [!DNL Experience Manager]에서 Adobe Target 통합이 구성된 경우 경험 조각을 Target으로 내보내면 잘못된 오퍼 유형이 생성됩니다. 경험 조각/소스 &quot;Adobe Experience Manager&quot; 유형 대신 Target은 &quot;HTML&quot;/소스 &quot;Adobe Target Classic&quot; 유형으로 여러 오퍼를 만듭니다.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: `granite/operations/maintenance`에 유지 관리 창이 없습니다.
   * SUM, MAX 및 MIN과 같은 집계 함수를 사용하는 경우 적용형 양식 서버측 유효성 검사가 실패합니다(CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : `granite/operations/maintenance`에 유지 관리 창이 없습니다.
   * 쇼퍼블 배너 뷰어를 통해 자산을 미리 볼 때 Dynamic Media 대화형 이미지의 핫스팟이 표시되지 않습니다.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : 등록 변경이 등록 취소를 완료할 때까지 기다리는 동안 시간이 초과되었습니다.

* AEM 6.5.15부터 ```org.apache.servicemix.bundles.rhino``` 번들에서 제공한 Rhino JavaScript 엔진에 새로운 호스팅 동작이 있습니다. 엄격 모드(```use strict;```)를 사용하는 스크립트는 올바른 변수를 선언해야 합니다. 그렇지 않으면 실행되지 않고 결국 런타임 오류가 발생합니다.

* 공식 업데이트 패키지를 통해 태그 지정 관련 기본 제공 콘텐츠를 설치하면 `/content/cq:tags` 노드의 언어 속성이 기본값으로 재설정됩니다. 이 작업은 서비스 팩, 보안 서비스 팩, 확장 기능 팩, 누적 기능 팩, 패치 등에 적용됩니다. 따라서 설치하기 전에 속성에서 추가해야 합니다.

### AEM Sites의 알려진 문제 {#known-issues-aem-sites-6522}

* 큰 조각 트리에 대한 DoS 보호로 인해 콘텐츠 조각-미리보기가 실패합니다. 기본 GraphQL 쿼리 실행기 구성 옵션에 대한 [KB 문서 보기](https://experienceleague.adobe.com/ko/docs/experience-cloud-kcs/kbarticles/ka-23945)(SITES-17934)


### AEM Forms의 알려진 문제 {#known-issues-aem-forms-6522}

* AEM Forms JEE 서비스 팩 21(6.5.21.0)을 설치한 후 `<AEM_Forms_Installation>/lib/caching/lib` 폴더(FORMS-14926) 아래에 Geode jars `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)`의 중복 항목이 있는 경우 다음 단계를 수행하여 문제를 해결하십시오.

   1. 로케이터가 실행 중인 경우 중지합니다.
   1. AEM 서버를 중지합니다.
   1. `<AEM_Forms_Installation>/lib/caching/lib`(으)로 이동합니다.
   1. `geode-*-1.15.1.2.jar`을(를) 제외한 모든 Geode 패치 파일을 제거합니다. `version 1.15.1.2`이(가) 있는 Geode jar만 있는지 확인합니다.
   1. 관리자 모드에서 명령 프롬프트를 엽니다.
   1. `geode-*-1.15.1.2.jar` 파일을 사용하여 Geode 패치를 설치합니다.

* 사용자가 저장된 XML 데이터를 사용하여 초안 문자를 미리 보려고 하면 일부 특정 문자에 대해 `Loading` 상태로 중단됩니다. 핫픽스를 다운로드하여 설치하려면 [Adobe Experience Manager Forms 핫픽스](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) 문서를 참조하십시오. (FORMS-14521)

* AEM Forms 서비스 팩 6.5.21.0으로 업그레이드한 후 `PaperCapture` 서비스가 PDF에서 OCR(광학 문자 인식) 작업을 수행하지 못했습니다. 이 서비스는 PDF 또는 로그 파일의 형태로 출력을 생성하지 않습니다. 핫픽스를 다운로드하여 설치하려면 [Adobe Experience Manager Forms 핫픽스](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) 문서를 참조하십시오. (CQDOC-21680)

* AEM 6.5 Forms 서비스 팩 18 또는 19에서 서비스 팩 20 또는 21로 업그레이드한 사용자에게 JSP 컴파일 오류가 발생했습니다. 이 오류로 인해 적응형 양식을 열거나 만들 수 없습니다. 또한 다른 AEM 인터페이스에 문제가 발생했습니다. 이러한 인터페이스에는 페이지 편집기, AEM Forms UI, 워크플로우 편집기 및 시스템 개요 UI가 포함되었습니다. (FORMS-15256)

  이러한 문제가 발생하면 다음 단계를 수행하여 해결하십시오.
   1. CRXDE의 `/libs/fd/aemforms/install/` 디렉터리로 이동합니다.
   1. 이름이 `com.adobe.granite.ui.commons-5.10.26.jar`인 번들을 삭제합니다.
   1. AEM 서버를 다시 시작합니다.

* Forms 추가 기능을 사용하여 AEM Forms 서비스 팩 20(6.5.20.0)으로 업데이트한 후 자격 증명 기반 인증을 사용하여 레거시 Adobe Analytics Cloud 서비스에 의존하는 구성이 작동하지 않습니다. 이 문제로 인해 분석 규칙이 올바르게 실행되지 못했습니다. 핫픽스를 다운로드하여 설치하려면 [Adobe Experience Manager Forms 핫픽스](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) 문서를 참조하십시오. (FORMS-15428)

* 사용자가 JEE 서버에서 AEM Forms 서비스 팩 20(6.5.20.0)으로 업데이트하고 출력 서비스를 사용하여 PDF을 생성하는 경우 PDF이 접근성 문제로 렌더링됩니다. 핫픽스를 다운로드하여 설치하려면 [Adobe Experience Manager Forms 핫픽스](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) 문서를 참조하십시오. (LC-3922112)
* 사용자가 JEE의 출력 서비스를 사용하여 태그가 지정된 PDF을 생성하면 &quot;부적절한 구조 경고&quot;가 표시됩니다. 핫픽스를 다운로드하여 설치하려면 [Adobe Experience Manager Forms 핫픽스](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) 문서를 참조하십시오. (LC-3922038)
* AEM Forms JEE에서 양식을 제출하면 반복되는 XML 요소의 인스턴스가 데이터에서 제거됩니다. 핫픽스를 다운로드하여 설치하려면 [Adobe Experience Manager Forms 핫픽스](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) 문서를 참조하십시오. (LC-3922017)
* Linux® 환경의 사용자가 HTML에서 적응형 양식(JEE의)을 렌더링할 때 제대로 렌더링되지 않습니다. 핫픽스를 다운로드하여 설치하려면 [Adobe Experience Manager Forms 핫픽스](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) 문서를 참조하십시오. (LC-3921957)
* 사용자가 AEM Forms JEE의 출력 서비스를 사용하여 XTG 파일을 PostScript 형식으로 변환할 때 오류가 발생하여 실패합니다. `AEM_OUT_001_003: Unexpected Exception: PAExecute Failure: XFA_RENDER_FAILURE`. 핫픽스를 다운로드하여 설치하려면 [Adobe Experience Manager Forms 핫픽스](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) 문서를 참조하십시오. (LC-3921720)
* JEE 서버에서 AEM Forms 서비스 팩 18(6.5.18.0)으로 업그레이드한 후 사용자가 양식을 제출할 때 HTML5를 렌더링하지 못하거나 PDF forms 및 XMLFM이 충돌합니다. 핫픽스를 다운로드하여 설치하려면 [Adobe Experience Manager Forms 핫픽스](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) 문서를 참조하십시오. (LC-3921718)
* 대화형 통신 에이전트 UI의 인쇄 미리 보기에서 통화 기호(예: 달러 기호 $)가 모든 필드 값에 대해 일관되지 않게 표시됩니다. 999까지의 값에 대해 표시되지만 1000 이상의 값에 대해서는 누락됩니다. (FORMS-16557)
* 대화형 통신에서 중첩된 레이아웃 조각의 XDP에 대한 수정 사항은 IC 편집기에 반영되지 않습니다. (FORMS-16575)
* 대화형 통신 에이전트 UI의 인쇄 미리 보기에서 일부 계산된 값이 올바르게 표시되지 않습니다. (FORMS-16603)
* [인쇄 미리 보기]에서 편지를 보면 내용이 변경됩니다. 즉, 공백이 일부 사라지고 특정 문자가 &#39;x&#39;로 대체됩니다. (FORMS-15681)
* 사용자가 WebLogic 14c 인스턴스를 구성할 때 JBoss에서 실행되는 JEE의 AEM Forms 서비스 팩 21(6.5.21.0)에 있는 PDFG 서비스가 SLF4J 라이브러리와 관련된 클래스 로더 충돌로 인해 실패합니다. 오류는 다음과 같이 표시됩니다(CQDOC-22178).

  ```java
  Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
  the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
  @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
  (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
  have different Class objects for the type org/slf4j/ILoggerFactory used in the signature
  ```

## OSGi 번들 및 콘텐츠 패키지가 포함됨{#osgi-bundles-and-content-packages-included}

다음 텍스트 문서에는 이 [!DNL Experience Manager] 6.5 서비스 팩 릴리스에 포함된 OSGi 번들 및 컨텐츠 패키지 목록이 나와 있습니다.

* [Experience Manager 6.5.22.0에 포함된 OSGi 번들 목록](/help/release-notes/assets/65220-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.22.0에 포함된 콘텐츠 패키지 목록](/help/release-notes/assets/65220-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 제한된 웹 사이트{#restricted-sites}

이러한 웹 사이트는 고객만 사용할 수 있습니다. 고객이고 액세스 권한이 필요한 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [Adobe 고객 지원 센터에 문의](https://experienceleague.adobe.com/en/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 제품 페이지](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 설명서](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [Adobe 우선 순위 제품 업데이트 구독](https://www.adobe.com/kr/subscription/priority-product-update.html)
