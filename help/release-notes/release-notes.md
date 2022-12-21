---
title: 용 릴리스 노트 [!DNL Adobe Experience Manager] 6.5
description: 릴리스 정보, 새로운 기능, 사용 방법 설치 및 다음에 대한 자세한 변경 목록을 찾습니다. [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
exl-id: 38227a66-f2a9-4909-9297-1eced4ed6e8c
source-git-commit: e73a65569963a5f60f7a4670998ada29deeb26b8
workflow-type: tm+mt
source-wordcount: '4036'
ht-degree: 10%

---

# [!DNL Adobe Experience Manager] 6.5 최신 서비스 팩 릴리스 노트 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession&cid=a915e87c-369a-480c-9daf-d13efc766798 -->

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 버전 | 6.5.15.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2022년 11월 24일 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 다운로드 URL | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 에 포함된 사항 [!DNL Experience Manager] 6.5.15.0 {#what-is-included-in-aem-6515}

[!DNL Experience Manager] 6.5.15.0에는 2019년 4월에 6.5의 초기 가용성 이후 릴리스된 새로운 기능, 주요 고객이 요청한 향상된 기능, 버그 수정 사항, 성능, 안정성 및 보안 개선 사항이 포함되어 있습니다. [이 서비스 팩 설치](#install) on [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_

* Added support for password reset for Dynamic Media Classic users within Experience Manager. (ASSETS-10298) -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6515}

* Experience Manager에서 자산 이동이 실패하는 경우 자산의 이름을 변경할 수 있습니다. (NPR-38753)
* 에서 자산을 보는 동안 [!UICONTROL 목록 보기]의 일부 제목이 누락되었습니다. (CQ-4345746)
* 화면 판독기는 [!UICONTROL 관계] 단추를 클릭합니다. (ASSETS-6938)
* 화면 판독기에서 폴더 목록이 있는 자산 탐색 페이지의 폴더 아이콘을 잘못 감지합니다. (ASSETS-6936)
* 컬렉션을 복사하는 동안 이미지에 빈 항목이 없습니다 `alt` attribute 또는 role=&quot;presentation&quot; 그 결과, 이미지는 화면 판독기 사용자에게 노출됩니다. (ASSETS-6932)
* 자산에 주석을 달 때 표시되는 텍스트에는 4가 없습니다:5:배경색과 비교하여 1개의 대비 비율. (ASSETS-6931)
* 자산 속성 페이지의 IPTC 탭에서 페이지 너비를 조정하면 페이지 컨텐츠가 제대로 맞지 않고 가로 스크롤이 됩니다. (ASSETS-6929)
* 자산을 필터링할 때 [!UICONTROL min] 및 [!UICONTROL max] 값이 입력되면 필드가 사라집니다. (ASSETS-6925)
* Experience Manager 컬렉션에서 화면 판독기는 [!UICONTROL 이메일] 다운로드 화면의 필드. (ASSETS-6923)
* 요소에 주석을 추가하는 동안 대체 텍스트가 누락되었습니다. (ASSETS-6922)
* 텍스트가 날짜 선택기 필드에 시간 및 분 단위로 작성되면 텍스트 오류 메시지가 표시되지 않습니다. 오류는 빨간색 색으로만 식별됩니다. (ASSETS-6852, ASSETS-6921, ASSETS-6920, ASSETS-6907)
* 의 대체 텍스트 `[role='img']` 에서 파일 필터가 누락되었습니다. (ASSETS-6919)
* 에 대한 잘못된 화면 판독기 알림 [!UICONTROL 만들기] 하위 메뉴 아래의 제품에서 사용할 수 있습니다. (ASSETS-6916)
* Experience Manager 컬렉션에서 제거 단추 `X` 화면 판독기에 대해 알릴 텍스트가 없습니다. (ASSETS-6912)
* Experience Manager에서 색상 대비 분석기를 사용하는 동안 달력 위젯의 날짜 선택기에서 현재 날짜와 선택한 날짜 간에 색상 차이가 없습니다. 인접한 색상에 비해 3:1의 명암비가 부족합니다. (ASSETS-6911)
* Experience Manager 파일에서 다음 옵션 중 하나를 선택합니다 [!UICONTROL 예약] 게시 관리의 라디오 단추에는 라디오 단추 옵션 이름 및 상태가 화면 판독기에 표시됩니다. 하지만, **예약** 레이블이 표시되지 않습니다. (ASSETS-6908, ASSETS-6906)
* 정렬 아이콘에 대한 대체 텍스트가 누락되었습니다. (ASSETS-6904)
* 자산 속성 페이지에서 필드 이름 `Person` iptc 확장 탭 레이블은 화면 판독기에 표시되지 않습니다. 화면 판독기는 편집 가능한 필드와 현재 빈 필드만 발표하지만 레이블 이름은 발표하지 않습니다. (ASSETS-6903, ASSETS-6848)
* 키보드를 사용하여 주석 도구를 표시할 수 없습니다. 마우스를 사용하여 이미지를 그려 주석 도구를 표시합니다. (ASSETS-6899)
* Experience Manager 컬렉션에서 **고급** 탭에는 경계와 인접한 색상 간의 잘못된 대비가 표시됩니다. (ASSETS-6895)
* 자산을 편집하는 동안 일부 요소에 대해 잘못된 ARIA 속성 값이 표시됩니다. (ASSETS-6894)
* 화면 판독기에서 워크플로우를 만드는 동안 제목을 올바르게 식별하지 못합니다. (ASSETS-6892)
* 컬렉션을 복사하는 동안 SVG 이미지 제거 단추 `X` role=&quot;img&quot;인 경우 role=&quot;presentation&quot;이 없습니다. 그 결과, 이미지는 화면 판독기 사용자에게 노출됩니다. (ASSETS-6890)
* 에서 **기본** 자산 속성의 탭에 있는 화면 판독기는 태그 필드의 확장 또는 축소 상태를 적절히 알리지 않습니다. (ASSETS-6889)
* 다음 **기본** 자산 속성 아래의 탭에 중복된 ID가 있는 페이지가 포함됩니다. (ASSETS-6888)
* 텍스트 상자에 값을 지정하면 워크플로우를 만드는 동안 제목을 정의하는 텍스트 필드의 레이블이 사라집니다. (ASSETS-6887)
* 링크를 공유하는 동안 수신자 목록은 제목이 있는 데이터 표로 표시되지만 화면 판독기 사용자에게 데이터 표로 의미상 식별되지 않습니다. (ASSETS-6886)
* 에 빈 필드를 나타내는 오류 메시지가 표시되지 않습니다. `Add Email Address` 필드. 오류는 색상을 사용해서만 표시됩니다. (ASSETS-6885, ASSETS-6843)
* 자리 표시자 텍스트, 경로 및 대체 텍스트에는 배경색에 비해 4.5:1 이상의 명암비가 없습니다. (ASSETS-6884, ASSETS-6865)
* 스마트 컬렉션을 저장하는 동안 일부 ARIA 속성에 대한 값이 잘못되었습니다. (ASSETS-6882)
* Smart Collection을 저장할 때 일부 레이블은 화면 판독기와 적절하게 연결되지 않습니다. (ASSETS-6881)
* 자산 속성의 IPTC 탭에서 화면 판독기는 키워드 양식 필드에 대한 레이블을 알리지 않습니다. (ASSETS-6879)
* Experience Manager 컬렉션에서 [!UICONTROL 이메일] 필드를 필수 필드로 식별하지 않으며, 값을 지정하지 않으면 오류 메시지가 표시되지 않습니다. (ASSETS-6877)
* Experience Manager 파일에서 오류 메시지가 표시되지 않습니다. **링크 공유** 화면이 표시됩니다. `Add Email Address`. 오류는 색상을 사용해야만 식별됩니다. (ASSETS-6876, ASSETS-6875)
* [!UICONTROL 자르기 및 맵] 자산을 편집하는 동안 옵션에 프로그래밍 방식의 이름이 없습니다. (ASSETS-6874)
* 필터 텍스트에 배경색과 비교하여 4.5:1 계약 비율이 없습니다. (ASSETS-6873)
* 기본 탐색 페이지의 폴더 이름에 대한 텍스트에는 배경색에 대한 대비 4.5:1 대비가 없습니다. (ASSETS-6872)
* 를 수행하는 동안 [!UICONTROL 복사] 컬렉션 작업, **[!UICONTROL 사용자 추가]** 콤보 상자 양식 컨트롤이 표시되는 레이블과 올바르게 연결되어 있지 않습니다. (ASSETS-6870)
* 화면 판독기는 [!UICONTROL 만들기] 단추 하위 메뉴 옵션. (ASSETS-6869)
* 범위, 워크플로우 및 시간대 옵션은 배경색상에 비해 4.5:1 대비율이 없습니다. (ASSETS-6868)
* 화면 판독기에서 의 축소 상태를 잘못 알려줍니다 **타임라인** 열. (ASSETS-6864)
* 스마트 컬렉션을 저장하는 동안 일부 ARIA 역할에 대한 하위 요소가 누락되었습니다. (ASSETS-6862)
* 자산을 공유하는 동안 에 필요한 ARIA 속성 `Search/Add Email Address` 필드가 지정되지 않았습니다. (ASSETS-6860)
* 다음 **맵** 키보드를 사용하여 대화 상자를 표시할 수 없습니다. 대신 맵 대화 상자를 표시하려면 마우스 클릭이 필요합니다. (ASSETS-6859)
* 자산 속성 페이지의 기본 탭에서 일부 ARIA 역할에 대한 하위 요소가 누락되었습니다. (ASSETS-6858)
* 자산 속성의 IPTC 탭에서 사용할 수 있는 빈 텍스트 입력 필드는 인접 색상에 비해 3:1 대비율이 없습니다. (ASSETS-6854, ASSETS-6847)
* 의 프로필 아이콘 **타임라인** 섹션이 화면 판독기에서 잘못 감지되었습니다. (ASSETS-6850)
* 화면 판독기는 자산 속성의 기본 탭에서 사용할 수 있는 검토 상태 콤보 상자가 읽기 전용 필드임을 알리지 않습니다. (ASSETS-6849)
* 화면 판독기는 모두 선택 및 주석 확인란의 레이블을 적절히 알리지 않습니다. (ASSETS-6846)
* 키보드 포커스는 `About Adobe Experience Manager` 선택 사항은 **도움말 표시** 메뉴 아래의 제품에서 사용할 수 있습니다. (ASSETS-6845)
* 카드 보기에서 키보드 화살표 키를 사용하여 폴더 목록을 탐색하는 동안 화면 판독기에서 선택한 폴더를 올바르게 알리지 않습니다. (ASSETS-6844)
* Experience Manager에 PDF을 업로드하는 동안 메모리 사용량이 지속적으로 증가하고 있습니다. (ASSETS-16889)
* 워크플로우가 .ZIP 파일을 Assets의 폴더 이름으로 변환하면 .ZIP 파일 이름의 대/소문자가 유지되지 않습니다. (ASSETS-16712)
* Brand Portal에서 Experience Manager 6.5로 전환하는 동안 필터를 처음 적용할 때 사용자 설명 필터가 적절한 결과를 표시하지 않습니다. (ASSETS-15932)
* 비디오에 주석을 달 수 없습니다. (ASSETS-15217)
* **게시 관리** 복제 액세스 권한이 없는 사용자에 대해 옵션이 사라집니다. `READ` 및 `WRITE` 액세스 `ETC` 및 `VAR`. (ASSETS-15007)
* 속성 페이지의 로드 시간은 여러 참조가 있는 자산에 대해 증가합니다. (ASSETS-14182)
* Brand Portal에서 이미지 게시를 취소하면 Experience Manager이 Dynamic Media에서도 해당 이미지를 게시 취소하므로 라이브 웹 사이트에 이미지가 표시되지 않습니다. (ASSETS-14118)
* Dynamic Media의 스마트 자르기 카드에 XSS 문제가 있습니다. (ASSETS-14212, ASSETS-14208, ASSETS-13704)
* Dynamic Media의 뷰어 사전 설정에서 XSS 문제가 발생합니다. (ASSETS-13822)
* AEM에서 DM 자산을 미리 보는 동안 사용자 액세스를 확인합니다. (CQ-4314757)


## 상거래 {#commerce-6515}

* 저장소 페이지를 만들지 못했습니다. 전체 카탈로그 롤아웃 프로세스를 중지합니다. (CQ-4347181)

## [!DNL Forms] {#forms-6515}

### 주요 기능 {#keyfeatures}

* 이제 AEM Forms 디자이너를 사용할 수 있습니다. [스페인어 로케일](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html). (LC-3920051)
* 이제 다음을 사용할 수 있습니다 [Microsoft® Office 365 메일 서버 프로토콜(SMTP 및 IMAP)을 인증하는 OAuth2](/help/forms/using/oauth2-support-for-mail-service.md). (NPR-35177)
* 다음을 설정할 수 있습니다 [서버에서 유효성 검사](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#enabling-server-side-validation-br) 서버 쪽의 레코드 문서에서 제외하기 위해 숨겨진 필드를 식별하는 true 속성입니다. (NPR-38149)
* AEM Forms Designer에는 32비트 버전의 Visual C++ 2019 재배포 가능(x86)이 필요합니다.  (NPR-36690)

### 수정 사항 {#fixes}

* 적응형 양식의 데이터 비활성화 속성이 전환되면 라디오 단추 및 확인란 그룹의 모양이 변경되지 않습니다. (NPR-39368)
* 적응형 양식이 번역되면 일부 번역이 누락되고 올바르게 표시되지 않습니다. (NPR-39367)
* 페이지의 속성을 숨김으로 설정하면 페이지가 양식 세트에서 제거되지 않습니다. (NPR-39325)
* [기록 문서]에서 페이지 끝에 있는 동적 각주 섹션이 없습니다. (NPR-39322)
* 적응형 양식에 대해 레코드 문서가 생성되면 라디오 단추와 확인란에 세로 정렬만 허용됩니다. 라디오 단추와 확인란에 대한 가로 정렬을 설정할 수 없습니다. (NPR-39321)
* Correspondence Management를 배포한 후 여러 사용자가 양식에 액세스하려고 하면 org.apache.sling.i18n.impl.JcrResourceBundle.loadPotentialLanguageRoot가 병목 현상을 일으켜 스레드의 대다수가 타격을 받습니다. 서버의 로드가 매우 적은 경우에도 종종 다양한 양식 페이지 요청이 각각 로드되는 데 1분 이상 걸립니다. (NPR-39176, CQ-4347710)
* 적응형 양식의 지연 로드 적응형 양식 조각에서 리치 텍스트 필드를 사용하는 경우 다음 오류 중 일부가 발생합니다.
   * 컨텐츠를 편집하거나 리치 텍스트 필드에 아무 것도 추가할 수 없습니다.
   * 리치 텍스트에 적용된 표시 패턴이 적용되지 않습니다. 
   * 양식 제출 시 최소 필드 길이에 대한 오류 메시지가 표시되지 않습니다.
   * 이 리치 텍스트 필드의 컨텐츠는 생성된 제출-XML에 여러 번 포함됩니다. (NPR-39168)
* 적응형 양식에서 날짜 선택기 옵션을 사용하면 값을 올바른 형식으로 변환하지 못합니다. (NPR-39156)
* 적응형 양식을 HTML 양식으로 미리 보는 동안 일부 하위 양식이 상위 양식과 겹치기 때문에 제대로 렌더링되지 않습니다. (NPR-39046)
* 패널에 숨겨진 테이블이 있고 적응형 양식이 표 형식으로 렌더링되는 경우 첫 번째 탭의 필드가 올바르게 표시되지 않습니다. (NPR-39025)
* 다음 `Body` 태그가 OOTB(기본 제공) 템플릿에 없습니다. (NPR-39022)
* 기록 문서는 적응형 양식의 언어로 생성되지 않습니다. 항상 영어로 생성됩니다. (NPR-39020)
* 적응형 양식에 여러 패널이 있고 일부 패널이 기본 제공 패널을 사용하는 경우 **파일 첨부** 구성 요소, `Error occurred while draft saving` 오류가 발생합니다. (NPR-38978)
* When `=` 적응형 양식의 확인란, 드롭다운 목록 또는 라디오 단추 필드에 기호가 사용되고 레코드 문서가 생성됩니다 `=` 생성된 기록 문서에 기호가 표시되지 않습니다.(NPR-38859)
* 6.5.11.0 서비스 팩 업그레이드 후 알림 배치 처리 오류 수가 여러 배로 증가합니다. (NPR-39636)
* 테스트 데이터를 제공하지 않으면 에이전트 UI에서 서신 관리 문자가 로드되지 않습니다. (CQ-4348702)
* 사용자가 IBM® WebSphere®를 사용하여 배포된 AEM Forms에서 AEM Forms 서비스 팩 14(SP14)를 적용하면 데이터베이스를 초기화하는 동안 부트스트래핑이 실패하고 `java.lang.NoClassDefFoundError:org/apache/log4j/Logger` 오류가 발생합니다.(NPR-39414)
* OSGi 서버의 AEM Form에서 문서 서비스 API를 사용하여 PDF을 인증하면 오류가 발생하여 실패합니다. com.adobe.fd.signatures.truststore.errors.exception.CredentialRetrievalException: AEM-DSS-311-003. (NPR-38855)
* 사용자가 AEM 6.3 Forms에서 문자를 렌더링하기 위해 래퍼 서비스를 사용하려고 하면 `java.lang.reflect.UndeclaredThrowableException` 오류가 발생합니다. (CQ-4347259)
* XDP를 HTML5 양식으로 렌더링하면 마스터 페이지의 컨텐츠가 적응형 양식의 개체 배치와 관계없이 먼저 렌더링됩니다. (CQ-4345218)
* 대상 서버의 응용 프로그램 구성은 **가져오기가 완료되면 구성을 덮어씁니다.** 응용 프로그램을 가져올 때 옵션이 선택되어 있지 않습니다. (NPR-39044)
* 사용자가 구성 관리자를 사용하여 커넥터 구성을 업데이트하려고 하면 실패합니다.(CQ-4347077)
* 사용자가 관리자 사용자의 기본 암호를 변경한 후 JEE 패치에서 AEM Form을 실행하려고 하면 예외가 발생합니다 `com.adobe.livecycle.lcm.core.LCMException[ALC-LCM-200-003]: Failed to whitelist the classes` 발생합니다. (CQ-4348277)
* AEM 디자이너에서 캡션이 없는 양식 필드는 확인란을 포함하는 테이블 셀에 배치됩니다.(LC-3920410)
* 사용자가 AEM Forms 디자이너에서 도움말을 열려고 하면 제대로 표시되지 않습니다. (CQ-4341996)

## [!DNL Sites] {#sites-6515}

* Experience Manager Sites 론치 콘솔이 비어 있습니다. (NPR-39188)
* 페이지가 이동하는 동안 참조가 있는 페이지도 활성화되어야 할 때 참조가 조정되지 않았습니다. (NPR-39061)
* 상위 컨테이너를 사용하여 레이아웃 컨테이너를 숨기지 않으면 레이아웃 변경 사항이 중첩된 컨테이너 내의 모든 구성 요소에 적용되지 않습니다. (NPR-39041)
* 이제 컨텐츠가 320픽셀 너비의 다른 컨텐츠와 더 이상 겹치지 않습니다. (SITES-8885)
* 대화 상자를 닫은 후 포커스가 추가되었습니다. (SITES-8885)

### 접근성 {#access-6515}

<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The scrollable region of the Page Editor did not have keyboard access. (SITES-2936) -->
<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The color input field of the Page Editor is not labeled or visible on the screen. (SITES-2925) -->
<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The iframe in the Page Editor is missing a title attribute; it must have an accessible name. (SITES-2894) -->
* 다음 **[!UICONTROL 주석]** 단추에 액세스 가능성 이름이 없습니다. (SITES-2892)
* ACTIVE 사용자 인터페이스 구성 요소의 상태(**[!UICONTROL 잘라내기]**, **[!UICONTROL 복사]**, **[!UICONTROL 붙여넣기]**, **[!UICONTROL 구성 요소 삽입]**, **[!UICONTROL 그룹]**&#x200B;등)에는 내부 또는 외부 인접 배경이 있는 광도 대비 비율이 3~1개 이상 없습니다. (SITES-8889, SITES-8756, SITES-8885)
* 상태 메시지가 자동으로 표시되지 않습니다. (SITES-8889, SITES-8756, SITES-8885)
* 텍스트 컨텐츠의 대비 비율은 4.5:1이 아닙니다. (SITES-8756, SITES-8885)
* 링크 또는 단추 텍스트에 마우스로 가리키거나 초점이 맞춰진 대비 비율이 4.5:1이 부족합니다. (SITES-8756, SITES-8885)

### [!DNL Content Fragments] {#sites-contentfragments-6515}

* GraphQL에서 예외가 발생합니다. 예를 들어 컨텐츠 조각에서 변형 태그를 가져올 수 없습니다. &#39;electric&#39;이라는 이름의 변형이 없습니다. 이 문제는 `getVariationTags` 예외를 발생시키는 비기존 변형에 대해. (SITES-8898)
* 제목 순서를 목록 보기에서 오름차순과 내림차순으로 정렬하고, 순서 A, C, B가 있는 제목을 표시합니다(SITES-7585)
* 컨텐츠 조각 변형에 대한 태깅 지원을 추가했습니다. (SITES-8168)
* 불필요했던 Experience Manager 6.5에서 Odin 특정 코드를 식별하고 제거했습니다. (SITES-3574)
* 컨텐츠 조각 편집기 사용자 인터페이스에서 언어 사본 조각을 게시할 때 관련 참조가 영어 폴더에 게시되었습니다. (NPR-39182)
* 날짜 필드가 날짜로 미리 채워집니다. (NPR-39124)
* 라디오 단추 옵션을 두 번째로 선택한 태그가 사라졌습니다. (NPR-39071)

### Fluid XP {#sites-fluidxp-6515}

* 클라이언트 라이브러리에 대해 ES6 컴파일 지원 사용 `/libs/cq/gui/components/siteadmin/admin/restoretree/clientlibs/restoretree.js`. (NPR-39067)
* 컨텐츠 조각 모델의 Multifield는 유효성 검사가 되더라도 발생하므로 비우고 저장할 수 없습니다 **[!UICONTROL 필수 여부]** 이 선택되어 있지 않습니다. (NPR-39063)
* 다음 중 한 방법으로 **[!UICONTROL 복사]** 또는 **[!UICONTROL Livecopy]** 작업, `cq:targetMetadata` 정보가 잘못 복제되었습니다. 이 기능으로 인해 Experience Manager에 있는 두 개 이상의 경험 조각이 target에서 내보낸 동일한 오퍼를 가리키게 되었습니다. (NPR-38970)
* 트리 복원 작업에 따라 메시지가 표시됩니다 `Un-publication pending. #0 in the queue` 은 처음에 게시되지 않은 페이지의 사용자 인터페이스에 표시됩니다. (NPR-38847)

### 페이지 편집기 {#sites-pageeditor-6515}

* 실행 취소 는 구성 요소에 추가된 텍스트의 마지막 변경 내용을 삭제하지 않았습니다. 대신 페이지를 새로 고치면 전체 구성 요소가 삭제되었습니다. (SITES-8597)
* 업그레이드 `jquery-ui` 최신 버전으로 이동해도 페이지 편집기가 제대로 작동하지 않습니다. (NPR-38596)
* 이제 컨텐츠가 320픽셀 너비의 다른 컨텐츠와 더 이상 겹치지 않습니다. (SITES-8756)
* 대화 상자를 닫은 후 포커스가 추가되었습니다(SITES-8756).

## 슬링 {#sling-6515}

* `Repoinit` 그룹 이름이 문자열로 처리되었으며 따옴표가 지원되지 않으므로 사용자 이름에 공백이 있는 그룹을 만들거나 관리할 수 없습니다. (SLING-10952)
* 로그에 오류 메시지와 예외가 실수로 입력되었습니다. (NPR-39024)

## 번역 프로젝트 {#translation-6515}

* 대상 페이지가 프로젝트 패널을 통해 업데이트된 언어 복사본에 대한 번역 작업에 추가되었습니다. 소스 페이지가 업데이트되지 않았습니다. (NPR-39278)
* 번역 프로젝트의 모든 페이지에 대한 미리 보기를 생성하는 동안 번역 프로세스가 실패했습니다. (NPR-39059)
* 언어 로캘이 없는 경우 이벤트에 대한 참조 규칙이 구성되면 로케일 폴더에 생성됩니다. (NPR-39054)

## 사용자 인터페이스 {#ui-6515}

* 파일 내에서 JavaScript 오류가 발생합니다 `multifield.js` 컨텐츠 조각 모델 편집기의 컨텐츠 조각 모델 및 컨텐츠 조각 편집기의 특정 필드에 대해 설명합니다. (NPR-39350)

## 워크플로 {#workflow-6515}

* Experience Manager 6.5.11에서 성공적으로 실행된 워크플로우는 Experience Manager의 6.5.13에서 일관되게 실행되지 않았습니다. (NPR-39023)

## 설치 [!DNL Experience Manager] 6.5.15.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.15.0 필요 [!DNL Experience Manager] 6.5. 참조: [업그레이드 설명서](/help/sites-deploying/upgrade.md) 자세한 지침 <!-- UPDATE FOR EACH NEW RELEASE -->
* 서비스 팩은 Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 다운로드할 수 있습니다.
* MongoDB 및 여러 인스턴스가 포함된 배포에서 을 설치합니다. [!DNL Experience Manager] 패키지 관리자를 사용하는 작성자 인스턴스 중 하나에 대한 6.5.15.0.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
>Adobe은 제거 또는 제거를 권장하지 않습니다 [!DNL Experience Manager] 6.5.15.0 패키지. 따라서 팩을 설치하기 전에 `crx-repository` 반납해야 할 경우를 대비해서 <!-- UPDATE FOR EACH NEW RELEASE -->

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

자동으로 설치하는 데 사용할 수 있는 방법에는 두 가지가 있습니다 [!DNL Experience Manager] 6.5.15.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* 서버가 온라인 상태일 때 패키지를 `../crx-quickstart/install` 폴더에 넣습니다. 패키지가 자동으로 설치됩니다.
* [패키지 관리자에서 HTTP API](/help/sites-administering/package-manager.md#package-share)를 사용합니다. 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

>[!NOTE]
>
>Experience Manager 6.5.15.0은 Bootstrap 설치를 지원하지 않습니다. <!-- UPDATE FOR EACH NEW RELEASE -->

**설치 확인**

이번 릴리스에서 사용할 수 있는 인증된 플랫폼을 확인하려면 [기술 요구 사항](/help/sites-deploying/technical-requirements.md).

1. 제품 정보 페이지(`/system/console/productinfo`)에 업데이트된 버전 문자열 표시 `Adobe Experience Manager (6.5.15.0)` 아래에 [!UICONTROL 설치된 제품]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 모든 OSGI 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]**&#x200B;이거나 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 콘솔 사용: `/system/console/bundles`).

1. OSGi 번들 `org.apache.jackrabbit.oak-core` 버전 1.22.13 이상(웹 콘솔 사용: `/system/console/bundles`). <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### 설치 [!DNL Experience Manager] Forms 추가 기능 패키지 {#install-aem-forms-add-on-package}

>[!NOTE]
>
>을 사용하지 않는 경우 건너뜁니다 [!DNL Experience Manager] Forms.

<!-- 
Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.
-->

1. 를 설치했는지 확인합니다. [!DNL Experience Manager] 서비스 팩.
1. 운영 체제에 대한 [AEM Forms 릴리스](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates)에 나열된 해당 양식 추가 기능 패키지를 다운로드합니다.
1. [AEM Forms 추가 기능 패키지 설치](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)에 설명된 대로 양식 추가 기능 패키지를 설치합니다.
1. Experience Manager 6.5 Forms에서 문자를 사용하는 경우 [최신 AEMFD 호환성 패키지](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates).

### 설치 [!DNL Experience Manager] JEE의 Forms {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE에서 AEM Forms를 사용하지 않는 경우 건너뜁니다. 의 수정 사항 [!DNL Experience Manager] 별도의 설치 프로그램을 통해 JEE의 Forms이 전달됩니다.

JBoss EAP 7.4.0 이외의 애플리케이션 서버를 사용하는 JEE 환경의 모든 AEM Forms에 대해 다음 단계를 수행합니다.
1. 설치 [AEM Forms JEE 패치](jee-patch-installer-65.md). 에는 JEE에서 AEM 6.5 Forms의 모든 구성 요소에 대한 모든 고정 문제가 포함되어 있습니다.
1. 설치 [JEE 서비스 팩 15의 AEM 6.5 Forms용 조각](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar). 조각은 AEM 서비스 팩 15(6.5.15.0)을 설치하는 데 필요한 종속성을 추가합니다.
1. 조각을 설치한 후 애플리케이션 서버가 안정화될 때까지 기다립니다.
1. [Experience Manager 6.5에 서비스 팩 설치](#install-service-pack).

   >[!NOTE]
   >
   >최신 버전을 설치하는 경우 [AEM 서비스 팩(6.5.15.0)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)설치하기 전에 [JEE 서비스 팩 15의 AEM 6.5 Forms용 조각](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) jee 환경의 AEM 6.5 Forms에서 CRX/bundle 및 시작 페이지의 작동이 중지되고 서비스를 사용할 수 없는 오류가 발생합니다. 문제를 해결하려면 작업을 수행합니다 [여기에 나열됨](/help/forms/using/aem-service-pack-installation-solution.md).
1. 설치 [최신 Forms 추가 기능 패키지](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)에서 Forms 추가 기능 패키지를 삭제합니다. `crx-repository\install` 폴더를 만들고 서버를 다시 시작합니다.

### UberJar {#uber-jar}

용 UberJar [!DNL Experience Manager] 6.5.15.0은 [Maven 중앙 저장소](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

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

| 영역 | 기능 | 대체 |
|---|---|---|
| 통합 | 다음 **[!UICONTROL AEM 클라우드 서비스 옵트인]** 화면은 다음부터 사용되지 않습니다 [!DNL Experience Manager] 및 [!DNL Adobe Target] 통합이에서 업데이트됨 [!DNL Experience Manager] 6.5. 통합은 Adobe Target Standard API를 지원합니다. API는 Adobe IMS 및 [!DNL Adobe I/O Runtime]. 이 플러그인은 Adobe Launch가 악기 역할을 계속 수행할 수 있도록 지원합니다 [!DNL Experience Manager] 분석 및 개인화를 위한 페이지인 옵트인 마법사는 기능적으로 관련이 없습니다. | 시스템 연결, Adobe IMS 인증 및 구성 [!DNL Adobe I/O Runtime] 해당 [!DNL Experience Manager] 클라우드 서비스. |
| 커넥터 | Microsoft® SharePoint 2010 및 Microsoft® SharePoint 2013용 Adobe JCR Connector는 더 이상 사용되지 않습니다 [!DNL Experience Manager] 6.5. | N/A |

## 알려진 문제 {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->

* [GraphQL 색인 패키지 1.0.5가 있는 AEM 컨텐츠 조각](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip)
이 패키지는 GraphQL을 사용하는 고객을 위해 필요합니다. 따라서 실제로 사용하는 기능을 기반으로 필요한 인덱스 정의를 추가할 수 있습니다.

* 로서의 [!DNL Microsoft® Windows Server 2019] 을 지원하지 않음 [!DNL MySQL 5.7] 및 [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] 에 대한 턴키 설치를 지원하지 않습니다. [!DNL AEM Forms 6.5.10.0].

* 를 업그레이드하는 경우 [!DNL Experience Manager] 인스턴스(6.5에서 6.5.10.0 버전)를 `RRD4JReporter` 의 예외 `error.log` 파일. 문제를 해결하려면 인스턴스를 다시 시작합니다.

* 설치하는 경우 [!DNL Experience Manager] 6.5 서비스 팩 10 또는 이전 서비스 팩 [!DNL Experience Manager] 6.5, 자산 사용자 지정 워크플로우 모델의 런타임 사본(에서 생성) `/var/workflow/models/dam`)이 삭제됩니다.
런타임 복사본을 검색하려면 Adobe에서 HTTP API를 사용하여 사용자 지정 워크플로우 모델의 디자인 타임 사본을 해당 런타임 복사와 동기화하는 것이 좋습니다.
   `<designModelPath>/jcr:content.generate.json`.

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

## OSGi 번들 및 컨텐츠 패키지가 포함됨 {#osgi-bundles-and-content-packages-included}

다음 텍스트 문서에는 다음 항목에 포함된 OSGi 번들 및 컨텐츠 패키지 목록이 나와 있습니다. [!DNL Experience Manager] 6.5.15.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager 6.5.15.0에 포함된 OSGi 번들 목록](/help/release-notes/assets/65150_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.15.0에 포함된 컨텐츠 패키지 목록](/help/release-notes/assets/65150_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 제한된 웹 사이트 {#restricted-sites}

이러한 웹 사이트는 고객만 사용할 수 있습니다. 액세스가 필요한 고객의 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [Adobe 고객 지원 문의](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 제품 페이지](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 설명서](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ko-KR)
>* [Adobe 우선 순위 제품 업데이트](https://www.adobe.com/kr/subscription/priority-product-update.html) 구독

