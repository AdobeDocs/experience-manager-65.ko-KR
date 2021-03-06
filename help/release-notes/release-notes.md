---
title: 용 릴리스 노트 [!DNL Adobe Experience Manager] 6.5
description: '"[!DNL Adobe Experience Manager] 6.5 노트는 릴리스 정보, 새로운 기능, 설치 방법 및 상세 변경 목록을 설명합니다."'
mini-toc-levels: 3
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: 9f957175573eeb2b40d79a5087dc3034c56819cc
workflow-type: tm+mt
source-wordcount: '3742'
ht-degree: 14%

---

# [!DNL Adobe Experience Manager] 6.5 최신 서비스 팩 릴리스 노트 {#aem-service-pack-release-notes}

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 버전 | 6.5.13.0 |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2022년 5월 26일 |
| 다운로드 URL | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.13.0.zip) |

## 에 포함된 사항 [!DNL Experience Manager] 6.5.13.0 {#what-is-included-in-aem}

[!DNL Experience Manager] 6.5.13.0에는 2019년 4월에 6.5의 초기 가용성 이후 릴리스된 새로운 기능, 주요 고객이 요청한 향상된 기능 및 성능, 안정성, 보안 개선 사항이 포함됩니다. [이 서비스 팩 설치](#install) on [!DNL Experience Manager] 6.5.

에 도입된 주요 기능 및 개선 사항 [!DNL Adobe Experience Manager] 6.5.13.0:

* 적응형 양식에서 보이지 않는 CAPTCHA를 사용합니다. 이제 보이지 않는 CAPTCHA를 사용하여 의심스러운 활동의 경우에만 CAPTCHA 문제를 표시할 수 있습니다. 의심스러운 활동이 없으면 CAPTCHA 문제가 표시되지 않습니다. Adobe Campaign은 확인란 요구 사항 없이 사람 양식을 완성했는지 평가하고 사용자 지정 노력을 줄이고 최종 사용자 경험을 개선하는 데 도움이 됩니다. (NPR-38500)

* REST 끝점에 대한 양식 데이터 모델 사후 처리에서 응답 헤더를 가져오도록 지원이 추가되었습니다. (NPR-38275)

* 이제 적응형 양식 번역 파일을 생성할 때 생성된 XLIFF 파일의 동일한 텍스트 시퀀스는 해당 적응형 양식의 구성 요소 시퀀스와 동일합니다. (NPR-37700)

* 적응형 양식을 현지화하고 기본 언어 텍스트를 변경하는 경우에도 다른 모든 언어에 대해 전체 번역이 누락됩니다. 이 문제는에서 수정되었습니다. [!DNL Experience Manager] 6.5.13.0. (NPR-37189)

* Forms의 접근성 개선:

   * 계속적이고 연결된 엔티티로 테이블의 머리글과 본문을 인식할 수 있도록 화면 판독기에 대한 지원이 추가되었습니다. 화면 판독기가 테이블을 제대로 탐색하는 데 도움이 됩니다. (NPR-37139)
   * 대화 상자가 열릴 때까지 HTML 작업 공간 탐색을 중지하도록 화면 판독기에 대한 지원을 추가했습니다. (NPR-37134)
   * Forms 디자이너에서 하이퍼링크의 화면 Reader 텍스트를 지정하는 기능이 추가되었습니다.(NPR-36221)

다음 버그 수정, 주요 기능 및 개선 사항이 [!DNL Experience Manager] 6.5.13.0:

<!-- The following issues are fixed in [!DNL Experience Manager] 6.5.13.0: -->

## [!DNL Assets] {#assets-6513}

* 읽기 전용 드롭다운 필드를 편집하려고 하면 드롭다운 값이 비어 있는 상태로 재설정됩니다. (NPR-38389)
* 비디오 파일에 오디오가 없는 경우 사용자가 비디오(.mp4) 자산을 수집할 수 없습니다. DAM 자산 업데이트 워크플로우가 실패하고 오류 메시지가 표시됩니다. (NPR-38116)
* 자산 이동 마법사를 사용하여 자산이 포함된 폴더를 이동하면 워크플로우가 실패하고 오류 메시지가 표시됩니다. (NPR-38061)
* FLV 비디오 프로필에 대해 FFmpeg 코드 변환 워크플로가 실패했습니다. (CQ-4343249)
* 업데이트 후 [!DNL Experience Manager] 6.5 SP10에서 자산 메타데이터 편집기가 제대로 작동하지 않습니다. (CQ-4341359)
* 게시로 적용된 검색 필터와 함께 저장된 스마트 컬렉션을 열면 검색 필터가 자동으로 게시되지 않음으로 변경됩니다. (CQ-4341191)
* 언어 전환 시 **[!UICONTROL 사용자 환경 설정]**, 레이블 **[!UICONTROL 정렬 기준]**, 드롭다운 단추 및 자산 홈 페이지의 정렬 옵션 내의 다른 옵션은 선택한 언어로 반영되지 않습니다. (CQ-4339306)
* 의 드롭다운 필드에 규칙을 추가할 때 **[!UICONTROL 메타데이터 스키마]**, **[!UICONTROL 종속적]** 목록에 드롭다운의 필드 레이블이 반영되지 않습니다. (ASSETS-9442)
* 자산 메타데이터 비활성화 드롭다운에서 값을 유지하지 않습니다. (ASSETS-8918)
* 을 사용하여 자산을 볼 때 **[!UICONTROL 더 자세히]** 옵션 **[!UICONTROL 열]** 보기, 잘못된 주석이 표시됩니다. (ASSETS-8851)
* 다른 버전으로 중복 자산을 만들 때 표현물이 생성되지 않습니다. (ASSETS-8607)

* 관리자가 아닌 사용자는 다른 사용자가 이미 체크 아웃한 자산을 게시할 수 있습니다. (NPR-38128)
* Chrome 97에서 차원 뷰어가 작동하지 않습니다. (CQ-4340456)
* 자산 다운로드 단추가 자산 세부 사항 페이지에 전체 메뉴를 표시하지 않습니다. (CQ-4336703)
* 링크 공유를 사용할 때 링크 공유 창의 일부 문자열이 현지화되지 않습니다. (CQ-4330540)
* 게시 관리에서 항목을 추가할 때 선택한 항목의 수를 반영하는 문자열이 현지화되지 않습니다. (CQ-4330491)

### [!DNL Dynamic Media] {#dynamic-media-6513}

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Zero day exploit with the Java™ Spring Core Framework (CVE-2022-22963) impacting Experience Manager 6.5.12. (ASSETS-9031) -->
* AEM 작성자의 Dynamic Media 자산에 대한 토큰 기반 보안 미리 보기. (ASSETS-4995)
* 에서 Dynamic Media용 이미지 사전 설정을 만들 때 [!DNL Experience Manager]의 경우 허용되는 최대 픽셀은 사용자 인터페이스에서 2000x2000픽셀로 제한됩니다. 너비나 높이 중 하나에 대해 값이 2001픽셀로 증가하면 **[!UICONTROL 저장]** 단추가 비활성화되었습니다. (ASSETS-5691)
* 특정 파일 형식이 Dynamic Media에 업로드되지 않도록 할 수 있습니다. (ASSETS-5693)
* 액세스 가능성 - 이미지 사전 설정 사용자 인터페이스에서 대체 속성이 이미지에 구현되지 않으면 화면 판독기에 의존하는 시각적으로 문제가 있는 사용자에게 영향을 받습니다. (ASSETS-9817)
* 액세스 가능성 - 화면 판독기는 아래쪽 화살표 모드로 이동할 때 &quot;타임라인 세그먼트&quot; 및 &quot;작업&quot; 탭에 있는 이미지에 대해 레이블이 지정되지 않은 이미지에 대해 나레이션할 때 영향을 받습니다. (ASSETS-5651)
* 액세스 가능성 - 화면 판독기는 (찾아보기/커서) 모드를 사용하여 탐색하는 동안 비디오 플레이어의 &quot;EmailLink&quot; 대화 상자에서 &quot;이메일 보내기&quot; 단추에 대해 수사적 이름(이메일 보내기)에 대해 내레이션하지 않으므로 영향을 받습니다. (ASSETS-5641)
* 접근성 - 키보드에서 TAB 키를 사용하여 탐색하는 동안 이미지 세트 편집기 페이지에서 &quot;실행 취소&quot; 단추를 호출한 후 나타나는 &quot;재실행&quot; 단추로 키보드 포커스가 이동하지 않습니다. (ASSETS-5582)
* 액세스 가능성 - 화면 판독기에 의존하는 사용자는 속성 제목 아래에 있는 이미지 세트 이미지에 대체 속성이 제공되지 않으므로 영향을 받습니다. (ASSETS-5576)
* 접근성 - 화면 판독기에서 제목 역할에 대해 내레이션이 적용되지 않습니다 `Cannot save this set` 텍스트 `Cannot save this set` 머리글 바로 가기 키를 사용하여 탐색하는 동안 경고 `H`및 아래쪽 화살표 키 (ASSETS-5569)
* 액세스 가능성 - 화면 판독기에 의존하는 사용자는 양식을 탐색하는 데 영향을 받습니다. NVDA가 &quot;폭 및 높이&quot; 스핀 컨트롤에 대한 레이블 정보에 내레이션이 없는 경우 양식 컨트롤에 대한 정보를 이해하는 데 어려움이 있습니다. NVDA 양식 모드 &#39;F&#39;로 탐색하는 동안 응답형 이미지 자르기 헤더 아래에 표시되는 컨트롤입니다. (ASSETS-5393)
* 사이트에서 Dynamic Media 구성 요소를 추가하고 페이지를 게시한 후 새로 추가된 Dynamic Media 자산은 게시된 페이지에 표시되지 않고 미리 보기 페이지에서도 볼 수 있습니다. 이 문제는 이미지 및 비디오 자산 유형 모두에 대해 발생했습니다. (ASSETS-9467)

## 상거래 {#commerce-6513}

* &quot;everyone&quot;에는 jcr:write가 있습니다. `/content/usergenerated/etc/commerce/smartlists`. (NPR-35230)
* 상거래 제품의 로컬 정렬이 더 이상 작동하지 않습니다. (CQ-4343750)
* 속성을 변경한 후 검색 결과 페이지에서 제품을 빠르게 게시할 수 없습니다. (CQ-4343318)

## CRX {#crx-6513}

* 특수 문자가 있는 경우 패키지를 다운로드할 수 없습니다 `+` ( 패키지 이름) 아래에 그룹화됩니다. (NPR-38102)

## [!DNL Forms] {#forms-65130}

<!-- * When you use the prefill service to fill an adaptive form that contains a fragment and the fragment contains a Text box that supports rich text, the form fails to submit, and the following error occurs:

  `[AF] [AEM-AF-901-004]: Encountered an internal error while submitting the form.` (NPR-38542) -->

* 라디오 단추, 확인란 및 파일 업로드 구성 요소가 독일어 언어로 올바르게 번역되지 않습니다. (NPR-38527)
* PDF417 바코드 인코딩에서 생성한 [!DNL Experience Manager] 라디오 단추 그룹에 대한 Forms이 잘못되었습니다. (NPR-38525)
* 적응형 양식 제출 시 다음 오류가 발생합니다.
   `WARN [10.172.114.236 [1650871578492] POST /lc/content/forms/af/public/DHS-3754-ENG/jcr:content/guideContainer.af.internalsubmit.jsp HTTP/1.1] com.adobe.aemds.guide.internal.impl.utils.SubmitDataCollector TemplateKey not found in merge json:cq:responsive` (NPR-38520)
* 레코드 문서에서 숨김 필드 제외 옵션이 작동하지 않습니다. (NPR-38512)
* 사이트 페이지에 Forms 컨테이너 구성 요소를 추가한 후 사용자가 다른 사이트 페이지로 이동할 수 없으며 사이트 페이지가 중단되는 경우가 있습니다. 문제가 간헐적으로 나타납니다. (NPR-38506)
* 사용자는 적용한 후 적응형 Forms에서 텍스트가 겹치는 경험을 합니다 [!DNL Experience Manager] 6.5 서비스 팩 11. (NPR-38376, CQ-4342472)
* 사용자는 적응형 양식 패널을 새로운 응답형 레이아웃으로 이동할 때 예외가 발생합니다. (NPR-38369)
* 클라이언트 라이브러리에 대해 ECMASCRIPT 6(ES6) 지원을 사용할 수 없습니다 ` /libs/fd/expeditor/clientlibs/view`. (NPR-38358)
* 를 사용하는 경우 [!DNL Experience Manager] 히브리어로 이메일을 보내는 워크플로우에서 사용자 끝에 받은 이메일에는 히브리어 텍스트 대신 물음표(??)가 포함됩니다(NPR-38296).
* 사용자가 임의로 로그아웃됨 [!DNL Experience Manager] 게시 인스턴스 및 적응형 양식을 제출하지 못했습니다. 이 문제가 [!DNL Experience Manager] Dispatcher를 사용하는 인스턴스입니다. (NPR-38285)
* Adobe Launch의 규칙에 getFormDataString 옵션을 사용하여 적응형 양식 데이터를 캡처하면 옵션이 적응형 Forms 데이터를 반환하지 않습니다. (NPR-38283)
* [!DNL Experience Manager] 6.5 Forms에서 사용 중단된 java.acl.Group 관련 API와 error.log 파일에 다음 오류 메시지가 표시됩니다.
   ` *WARN* [default task-36] org.apache.jackrabbit.oak.spi.security.principal.AclGroupDeprecation use of deprecated java.acl.Group-related API - this method is going to be removed in future Oak releases - see OAK-7358 for details` (NPR-38282)
* 독일어 Forms에서 만든 영어 또는 다른 언어로 번역되지 않습니다. (NPR-38280)
* 지역화된 버전의 적응형 양식을 사용하는 경우 해당 Document of Record(DoR)가 현지화되지 않습니다. (NPR-38235)
* 전자 메일 전송 단계를 사용하여 전자 메일과 함께 첨부 파일을 전송하는 경우 첨부 파일은 워크플로우 단계에 지정된 이름을 유지하지 않습니다. (NPR-38216)
* 새 버전의 편지가 게시되면 사용자는 이전 버전의 편지용 초안을 열 수 없습니다. (NPR-38215, CQ-4342515)
* 적응형 양식 규칙으로 구성된 단추 클릭에서 AEM Forms JEE 서비스 SOAP 엔드포인트 서비스 메서드를 호출할 때 다음 예외로 인해 SOAP 서비스가 실패합니다.
   `ERROR* [0:0:0:0:0:0:0:1 [1624362360493] POST /content/forms/af/testsoapwsdl/jcr:content/guideContainer.af.dermis HTTP/1.1] com.adobe.aemds.guide.addon expeditor.servlet.ExpEditorServiceManager Error while making web service related call java.lang.Exception: createSOAPParam: JSONException`
* com.adobe.fd.pdfutenability.services.PDFUfabilityService#convertPDFtoXDP를 사용하여 PDF을 XDP 형식으로 변환하는 경우 잘못된 XDP 파일이 반환됩니다. (NPR-38140, CQ-4342099)
* 여러 사용자가 서신 관리를 사용하여 서로 다른 문자를 생성하는 경우 미리 볼 때 일부 사용자에게 잘못된 문자가 표시됩니다. (NPR-38134)
* SITES 페이지에 포함된 AEM Forms 구성 요소는 값이 %이고 W3C HTML 유효성 검사로서 유효하지 않은 width 속성을 사용합니다. HTML 유효성 검사 중에 사용자에게 잘못된 구문 분석 오류가 발생했습니다. (NPR-38124)
* 적응형 양식의 대부분의 OOTB 테마에 대한 라디오 단추 및 확인란 항목은 탭 순서의 일부가 아닙니다(NPR-38108)
* 사용자가 워크플로우를 실행하는 동안 주석 섹션에 HTML 태그를 추가하면 HTML 태그가 렌더링됩니다. (NPR-37591)
* 새 XDP 파일이 포함된 문자를 가져오고 게시할 때 게시 인스턴스에서 문자가 미리 표시되지 않습니다. 그러나 동일한 CMP 파일을 사용하여 편지를 가져와서 두 번째로 게시한 경우 편지를 미리 보기합니다. (CQ-4343599)
* 데이터 준비 프로세스 속성이 설정된 양식이 HTML 작업 공간에서 렌더링되지 않습니다. (CQ-4343294)
* Forms 6.5 Designer로 작성된 정적 PDF forms의 경우 PDF 액세스 가능성이 오류로 실패합니다 `Tab order entry in page with annotations not set to "S"`. (CQ-4343117)
* AEMForms-6.5.0-0038(log4jv2.16) 패치를 적용한 후 OCR을 사용하여 PDFG 서비스를 사용하여 이미지를 PDF으로 변환할 수 없습니다. (CQ-4342450)
* 바코드 SSCC-18에 대해 잘못된 값이 표시됩니다. Forms 서버에서는 바코드의 오른쪽 부분에 있는 값을 생략합니다. (CQ-4342400)
* Microsoft® Word 파일을 Forms Designer로 가져올 수 없습니다. 사용자에게 오류가 발생합니다 `Word (version XP or onwards) could not be found on the machine`. (CQ-4342146)
* Forms 6.5 Designer에서 Forms 6.1 Designer로 만든 양식을 열고 텍스트 상자를 편집하면 단락 간격이 지정된 공간을 초과합니다. 스페이스에 대한 이전 설정이 모두 제거되고 텍스트 상자의 수동 재서식이 필요합니다. (CQ-4341899)
* 사용자가 작업 제거 스케줄러에서 사용자 지정 시간을 설정할 수 없습니다. (CQ-4339192)
* 사용자가 끝점 관리 UI에서 구성을 업데이트할 수 없으며 오류가 발생했습니다 ` Uncaught ReferenceError: updateEndpoint_required is not defined`. (CQ-4331523)
* 잘못된 태그의 경우 오류 메시지의 정상 처리가 예상대로 작동하지 않습니다. (NPR-38106 및 CQ-4337173)

>[!NOTE]
>
>* [!DNL Experience Manager Forms] 는 예약된 후 1주일 후에 추가 기능 패키지를 출시합니다 [!DNL Experience Manager] 서비스 팩 릴리스 날짜입니다.


## Granite {#granite-6513}

* Omnisearch는 읽기 권한이 없는 사용자에 대한 결과를 반환합니다. (NPR-38373)
* 에 ES6 활성화 `/libs/granite/configurations/clientlibs/confbrowser`. (NPR-38300)

## 통합 {#integrations-6513}

* 사용되지 않는 UserInfoServlet에서 테스트 및 Target 서비스의 리소스 확인자 세션이 누출되었습니다. (NPR-38112)

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * AEM‑OP‑13 ‑ HTTP Parameter Pollution in `com.day.cq.searchpromote.impl.servlet`. (NPR-38033) -->
<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Analytics 2.0 IMS support added to Experience Manager 6.5. (NPR-37914) -->

## Oak 색인 지정 및 쿼리 {#oak-6513}

* 6.5.13.0용 Oak 버전이 이제 1.22.11으로 업데이트되었습니다. (NPR-38084) -->

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Create a CFP based on latest 6.5.12 and update Oak-related bundle versions. (NPR-38144) -->

## 플랫폼 {#platform-6513}

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * RTC : Universal XSS through cq-rewriter HtmlParser. (NPR-38064) -->
* 업그레이드 종속성 `org.apache.httpcomponents.httpclient` in [!DNL Experience Manager] 6.5. (NPR-37999)
* 경로 필드 제안으로 인해 높은 작성자 로드. (CQ-4341826)
* 사용자가 프로젝트를 카드 보기에서 달력 보기로 변경할 때 페이지를 새로 고쳐야 합니다. (CQ-4340368)
* 권한 제한으로 인해 태그가 유실됩니다. (CQ-4339543)
* 경로 선택의 검색 및 필터에서 보고된 여러 문제가 작동하지 않습니다. (CQ-4339402)
* 6.5에서 DTM 사용 중지 - Launch for Omega Instrumentation으로 전환하고 Gainsight 지원을 추가합니다. (CQ-4337809)
* 설정된 경로 필드 필터 속성을 기반으로 경로 필드 구성 요소 검색 함수를 제한합니다. (CQ-4309556)
* [!DNL Experience Manager] 플랫폼 6.5: 중국어 로케일 이름 지정 수정 사항. (CQ-4308978)
* Launch for Omega Instrumentation으로 전환합니다. (NPR-38377)
* [!DNL Experience Manager] 플랫폼 6.5: 중국어 로케일 이름 지정 수정 사항입니다. (CQ-4308978)

## 복제 {#replication-6513}

* 작성자에서 게시자로 사용자 노드를 게시하지 못했습니다. (NPR-38005)

## [!DNL Sites] {#sites-6513}

### 관리자 {#sites-admin-6513}

* 페이지를 이동할 때 문제를 일으킬 수 있는 SP 12에 도입된 회귀 문제를 수정합니다. (SITES-5298)

### 클래식 사용자 인터페이스 {#sites-classicui-6513}

* RTE: 새 이미지를 기존 이미지 위로 드래그하면 업데이트된 이미지가 표시되지 않습니다. (NPR-38141)

<!-- version 2 of description above * Updated Image is not visible When a new image is dragged on top of an existing image the updated image is not visible in RTE - Classic UI. (NPR-38141) -->

### 콘텐츠 조각 {#sites-contentfragments-6513}

* 하위 구성에서 컨텐츠 조각 모델 생성을 지원합니다. (NPR-38054)

<!-- version 2 of description above * The Configuration Manager now allows you to set the Content Fragment Model config on a sub-config folder. (NPR-38054) -->
* 컨텐츠 조각 모델에서 &#39;고유 필드&#39; 유효성 검사를 사용할 때 성능을 개선합니다. (NPR-38142)

<!-- version 2 of description above * The unique field validation query is now fixed. (NPR-38142) -->
* 컨텐츠 조각 모델 편집기를 열 때 응답 시간을 개선합니다. 자산에 조각이 여러 개 있는 고객이 를 열 때 오류를 볼 수 있습니다. (SITES-6284)

<!-- version 2 of description above * If the customer is trying to access the editor of the content fragment models, they get a query error because of too many fragments on the dam. (SITES-6284) -->
* 컨텐츠 조각 모델 편집기 오류를 일으킬 수 있는 6.5.11에서 6.5.12로 업데이트할 때 발생하는 회귀 문제를 수정합니다. (SITES-5088 및 SITES-4967)

<!-- version 2 of description above * Paths were getting deleted when AEM 6.5.12.0 was installed on existing 6.5.11.0 instance. (SITES-5088)
* Apple 6.5.10 system crashing when using CF model editor, due to erroneous feature toggle check. (SITES-4967) -->
* 컨텐츠 조각 모델 편집기 사용자 인터페이스의 현지화를 개선합니다. (NPR-38126)

<!-- version 2 of description above * Some strings in the Content Fragment Model editor are not localized. (NPR-38126) -->
* 작성자 서버를 Dispatcher와 함께 사용할 때 컨텐츠 조각 편집기를 닫으면 오류가 발생할 수 있는 문제를 수정했습니다. (NPR-38205)

<!-- version 2 of description above * Update of Content Fragment references is returning an invalid JSON response via Dispatcher. (NPR-38205) -->
* RTE 필드에서 유효성 검사를 사용할 때 모델을 저장할 수 없던 문제를 수정했습니다. (NPR-38210)

<!--version 2 of description above * Content Fragment Model Rich Text Validation Prevents Blocks Saving a Content Fragment Model. (NPR-38210) -->
* 부울 속성이 &#39;Property Name&#39;을 표시하는 대신 &quot;title&quot;에 필드 텍스트가 표시되지 않는 컨텐츠 조각 문제입니다. (NPR-38244)
* Postman을 통해 쿼리 변수를 사용하여 지속된 쿼리를 실행하는 동안 오류가 발생했습니다. (NPR-38251, NPR-38057)
<!--version 2 of description above * An unexpected error message is coming in Postman, when executing the graphQL persisted query having query variables. (NPR-38251) -->
* 컨텐츠 조각 구성 요소: &#39;머리글을 단락으로 처리&#39; 옵션의 회귀 현상이 6.5 SP7이었던 것으로 수정되었습니다. (NPR-38055)

<!--version 2 of description above * After applying SP11 to the Publish instance of AEM 6.5.6, the display result of the Content Fragment set in the published page changes. (NPR-38055) -->
* 자산 검색 오류를 일으킬 수 있는 6.5.11에 도입된 회귀를 수정합니다. (SITES-4784)

<!--version 2 of description above * Adapt external index package to use selection Policy (fragment versus asset index). (SITES-4784) -->
* 사용 **[!UICONTROL 편집]** 검색 결과에서 `Not Found` 오류가 발생했습니다. (NPR-37810)

<!--version 2 of description above * When editing Content Fragment from the Assets Search Rail results page, it throws 'Not Found' error. (NPR-37810) -->

### ContentHub {#sites-contenthub-6513}

* Context Hub UI 모델이 하드 페이지를 새로 고치지 않으면 제대로 렌더링되지 않습니다. (NPR-38212)

### 이메일 편집기 {#sites-emaileditor-6513}

* 예정된 이메일 핵심 구성 요소 릴리스에 대한 지원 활성화 [https://github.com/adobe/aem-core-email-components](https://github.com/adobe/aem-core-email-components). (NPR-38445 및 NPR-38204)

<!-- version 2 of description above * Allow new email templated under campaign and ambit. (NPR-38445) * The "Approve for Adobe Campaign" workflow was only running for pages which are of type or extending the resource types: "mcm/neolane/components/newsletter", "mcm/campaign/components/newsletter" and "mcm/campaign/components/campaign_newsletterpage". (NPR-38204) -->

### 경험 조각 {#sites-experiencefragments-6513}

* 경험 조각에 대한 참조에서 페이지로 이동 작업을 사용하는 경우 잘못된 페이지가 열립니다. (NPR-38062)
* XF 템플릿에서 오는 레이아웃 속성은 페이지 측에서 관찰되지 않습니다. (NPR-38214)
* XF 참조 계산 성능이 향상되었습니다. (NPR-38269)

<!-- version 2 of description above * Job queue configuration is incorrect - The OSGi configuration for the reference updater job queue has not been ported back to 6.5. This issue leads to jobs being run in the main queue, which has a higher priority and allows more jobs to run in parallel. This flow can lead to CPU exhaustion. (NPR-38269) -->

### 페이지 편집기 {#sites-pageeditor-6513}

* 에 inlineEditing 또는 dropTarget 기능이 없는 구성 요소에 대한 실행 취소를 개선합니다. `cq:editConfig`. (NPR-38361)

<!-- version 2 of the description above * When out of the box components that don't have inlineEditing or dropTarget feature in the _cq_editConfig file (navigation, breadcrumb, embed) are deleted > undeleted (by way of Undo), all configurations are lost and empty placeholder reappears. Component must be reconfigured from scratch. (NPR-38361) -->
* 스타일 시스템 드롭다운이 구성 요소를 사용하는 구성 요소에 대해 구성 요소의 컨텍스트 대신 페이지 맨 위에 배치되었을 수 있습니다 `cq:editConfig` &quot;AFTERED: REFRESH_PAGE&quot;. 이제 이 문제가 해결되었습니다. (NPR-38384)

<!-- version 2 of description above* When selecting a style option on a component, the Styles box shifts to the upper left corner of the screen, rather than staying put below the style icon. Happens for components that have  cq:editConfig “afteredit: REFRESH_PAGE”. (NPR-38384) -->
* 중첩된 레이아웃 컨테이너에 추가할 때 텍스트 구성 요소가 잘못 정렬되었습니다. (NPR-38193)
* 구성 요소에 대한 스타일 시스템 구성이 없을 때 빈 스타일 탭이 표시되었습니다. 이제 구성이 없을 때 탭이 숨겨집니다. (NPR-38218)
<!-- version 2 of description above * Style tab is blank on components without styles/policies. (NPR-38218) -->
* 속성 `useLegacyResponsiveBehaviour` 는 인증된 경우에만 작동합니다. (NPR-37996)
* jquery-ui를 최신 버전으로 업그레이드하면 편집기가 중단됩니다. (SITES-5647)

### 보안 {#sites-security-6513}

* 사용자 그룹 관리 사용자 인터페이스가 특히 20명의 사용자가 있는 그룹에서 사용자를 제거하지 못한 경우가 있습니다. (NPR-38041)

<!--version 2 of description above * Cannot remove users from user groups. (NPR-38041) -->

### SEO {#sites-seo-6513}

* Sitemap Generator 및 Canonical 태그는 .html 없이 URL에 대한 지원을 추가합니다. (CIF-2647)
* noindex 구성을 사용하여 대체 언어를 제거하는 지원을 추가합니다. (CIF-2496)
* 거의 동일한 컨텐츠가 있는 페이지의 기본 표준 URL을 덮어쓸 사용자 지정 URL을 제공할 지원을 추가합니다. (CIF-2747)

### SPA 편집기 및 SDK {#sites-spa-sdk-6513}

* 6.5.13부터 SPA Editor를 통해 JCR에서 컨테이너 구성 요소 노드를 더 이상 만들지 않아도 됩니다. A `virtual container` 는 SDK를 통해 저장하기 전에 생성됩니다. (SITES-5762)

<!-- version 2 of description above * Virtual container support - Adding a child component to a virtual container that is not yet present in the database implies the creation of a node to represent the container in content structure. (SITES-5762) -->

### 템플릿 편집기 {#sites-templateeditor-6513}

* 변경된 템플릿을 게시하는 것이 일부 종속성을 게시하지 않던 회귀 문제를 수정했습니다. (NPR-38274)

<!-- version 2 of description above * Template changes do not get published until you publish a page that uses that template. (NPR-38274) -->
* TemplateResource valueMap에서는 ValueMap API에 따라 딥 읽기를 허용합니다. (NPR-38439)

## 슬링 {#sling-6513}

<!-- OBSOLETE BASED ON CQDOC-19400 * Memory leak in `DiscoveryLiteDescriptor`. (NPR-38288) -->
* 업데이트 `sling-javax.activation` SLING-8777의 수정 사항이 포함된 번들. (NPR-38077)

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Security issues reported under `org.apache.sling.scripting.jst`. (NPR-38067) -->

## 번역 프로젝트 {#translation-6513}

* 참조된 페이지/xf에 대해 여러 개의 론치가 만들어집니다. (NPR-38263)
* 서비스 팩 10 이후 번역 프로젝트에 페이지를 추가하는 동작이 변경되었습니다. 번역 프로젝트에 새로 만든 페이지가 없습니다 [ex: test-page-women-2] 목록에서 새로 만든 페이지의 상위 항목을 선택한 경우 [새로 만든 페이지가 바로 아님]. (NPR-38256)
* 추가 `cq:isTranslationLaunch` 번역 프로젝트에서 만든 론치의 속성. (NPR-38224)
* 자산이 있는 참조된 XF가 있는 페이지에 대해 Launch가 만들어집니다. (NPR-38199)
* [!DNL Experience Manager] 번역 메모리 업데이트가 작동하지 않습니다. (NPR-38196)
* 에 ES6 활성화 `/libs/cq/gui/components/projects/admin/translation/job/addcontent/clientlibs.js`. (NPR-38306)
* 의 번역에 대한 최신 18n 패키지 [!DNL Experience Manager] 6.5. (CQ-4339505)

## 사용자 인터페이스 {#ui-6513}

* 업데이트 대상 `favicon.ico` Experience Manager에 사용됩니다. (CQ-4315324)
* 시작 페이지 > 도구 섹션에 있는 경우 [!DNL Experience Manager] 아이콘, [!DNL Experience Manager] 탐색 화면이 표시됩니다. (NPR-38417)
* 에 ES6 활성화 `/libs/granite/ui/references/clientlibs/coral/references`. (NPR-38303)
* 에 ES6 활성화 `/libs/granite/datavisualization/clientlibs/d3-3.x`. (NPR-38302)
<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * AEM‑OP‑09 ‑ Persistent cross‑site scripting selecting paths in templates. (NPR-38301) -->
* Touch UI의 날짜 선택기가 한국어로 표시됩니다. (NPR-38079)
* 라디오 단추 선택 값을 로드하는 필드를 다시 정렬할 때 다중 필드로 대화 상자를 작성합니다. (NPR-38063)

## WCM {#wcm-6513}

* [!DNL Experience Manager] MCM(캠페인) 6.5: 중국어 로케일 이름 지정 수정 사항. (CQ-4308973)
* com.day.cq.wcm.workflow.impl.WcmWorkflowServiceImpl.autoSubmitPageAfterModification에서 ResourceResolver가 닫히지 않았습니다(NPR-38286)

## 설치 [!DNL Experience Manager] 6.5.13.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback -->

* [!DNL Experience Manager] 6.5.13.0 필요 [!DNL Experience Manager] 6.5. 참조: [업그레이드 설명서](/help/sites-deploying/upgrade.md) 자세한 지침
* 서비스 팩은 Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 다운로드할 수 있습니다.
* MongoDB 및 여러 인스턴스가 포함된 배포에서 을 설치합니다. [!DNL Experience Manager] 패키지 관리자를 사용하는 작성자 인스턴스 중 하나에 대한 6.5.13.0.

>[!NOTE]
>
>Adobe은 [!DNL Experience Manager] 6.5.13.0 패키지.

### 서비스 팩 설치 [!DNL Experience Manager] 6.5 {#install-service-pack}

1. 인스턴스가 업데이트 모드(이전 버전에서 인스턴스가 업데이트되었을 때)인 경우 설치하기 전에 인스턴스를 다시 시작합니다. Adobe은 인스턴스에 대한 현재 가동 시간이 높은 경우 다시 시작할 것을 권장합니다.

1. 설치하기 전에 스냅샷 또는 새 백업 [!DNL Experience Manager] 인스턴스.

1. 에서 서비스 팩 다운로드 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.13.0.zip).

1. 패키지 관리자를 열고 **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭하여 패키지를 업로드합니다. 자세한 내용은 [패키지 관리자](/help/sites-administering/package-manager.md).

1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

1. S3 커넥터를 업데이트하려면 서비스 팩을 설치한 후 인스턴스를 중지하고 기존 커넥터를 설치 폴더에 제공된 새 이진 파일로 바꾸고 인스턴스를 다시 시작합니다. 자세한 내용은 [Amazon S3 데이터 저장소](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>패키지 관리자 UI에 대한 대화 상자가 서비스 팩을 설치하는 동안 종료되는 경우가 있습니다. 배포에 액세스하기 전에 오류 로그가 안정될 때까지 기다리는 것이 좋습니다. 업데이터 번들 제거와 관련된 특정 로그를 기다린 후 설치가 성공했는지 확인합니다. 일반적으로 이 문제는 [!DNL Safari] 브라우저이지만 모든 브라우저에서 간헐적으로 발생할 수 있습니다.

**자동 설치**

자동으로 설치하는 데 사용할 수 있는 방법에는 두 가지가 있습니다 [!DNL Experience Manager] 6.5.13.0.

* 서버가 온라인 상태일 때 패키지를 `../crx-quickstart/install` 폴더에 넣습니다. 패키지가 자동으로 설치됩니다.
* [패키지 관리자에서 HTTP API](/help/sites-administering/package-manager.md#package-share)를 사용합니다. 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

>[!NOTE]
>
>[!DNL Experience Manager] 6.5.13.0 은 Bootstrap 설치를 지원하지 않습니다.

**설치 확인**

이번 릴리스에서 사용할 수 있는 인증된 플랫폼을 확인하려면 [기술 요구 사항](/help/sites-deploying/technical-requirements.md).

1. 제품 정보 페이지(`/system/console/productinfo`)에는 [!UICONTROL 설치된 제품] 아래에 업데이트된 버전 문자열 `Adobe Experience Manager (6.5.13.0)`이 표시됩니다.

1. 모든 OSGI 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]**&#x200B;이거나 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 콘솔 사용: `/system/console/bundles`).

1. OSGi 번들 `org.apache.jackrabbit.oak-core` 버전 1.22.3 이상(웹 콘솔 사용: `/system/console/bundles`).


### 설치 [!DNL Experience Manager] Forms 추가 기능 패키지 {#install-aem-forms-add-on-package}

>[!NOTE]
>
>을 사용하지 않는 경우 건너뜁니다 [!DNL Experience Manager] Forms. 의 수정 사항 [!DNL Experience Manager] Forms은 예약된 후 1주일 후에 별도의 추가 기능 패키지를 통해 전달됩니다 [!DNL Experience Manager] 서비스 팩 릴리스.

1. 를 설치했는지 확인합니다. [!DNL Experience Manager] 서비스 팩.
1. 운영 체제에 대한 [AEM Forms 릴리스](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates)에 나열된 해당 양식 추가 기능 패키지를 다운로드합니다.
1. [AEM Forms 추가 기능 패키지 설치](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)에 설명된 대로 양식 추가 기능 패키지를 설치합니다.
1. Experience Manager 6.5 Forms에서 문자를 사용하는 경우 [최신 AEMFD 호환성 패키지](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates).

### 설치 [!DNL Experience Manager] JEE의 Forms {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE에서 AEM Forms를 사용하지 않는 경우 건너뜁니다. 의 수정 사항 [!DNL Experience Manager] 별도의 설치 프로그램을 통해 JEE의 Forms이 전달됩니다.

용 누적 설치 프로그램 설치에 대한 자세한 정보 [!DNL Experience Manager] JEE의 Forms 및 배포 후 구성은 다음을 참조하십시오. [릴리스 노트](jee-patch-installer-65.md).

>[!NOTE]
>
>누적 설치 관리자를 설치한 후 [!DNL Experience Manager] Forms on JEE에서, 최신 Forms 추가 기능 패키지를 설치하고, Forms 추가 기능 패키지를 목록에서 삭제합니다 `crx-repository\install` 폴더를 만들고 서버를 다시 시작합니다.

### UberJar {#uber-jar}

용 UberJar [!DNL Experience Manager] 6.5.13.0은 [Maven 중앙 저장소](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.13/)(https://)

Maven 프로젝트에서 UberJar를 사용하려면 [Uberjar 사용 방법](/help/sites-developing/ht-projects-maven.md)을 참조하여 프로젝트 POM에 다음 종속성을 포함하십시오.

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.13</version>
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
| 통합 | 다음 **[!UICONTROL AEM 클라우드 서비스 옵트인]** 화면은 다음부터 사용되지 않습니다 [!DNL Experience Manager] 및 [!DNL Adobe Target] 통합이에서 업데이트됨 [!DNL Experience Manager] 6.5. 통합은 Adobe Target Standard API를 지원합니다. API는 Adobe IMS 및 [!DNL Adobe I/O]. 이 플러그인은 Adobe Launch가 악기 역할을 계속 수행할 수 있도록 지원합니다 [!DNL Experience Manager] 분석 및 개인화를 위한 페이지인 옵트인 마법사는 기능적으로 관련이 없습니다. | 시스템 연결, Adobe IMS 인증 및 구성 [!DNL Adobe I/O] 해당 [!DNL Experience Manager] 클라우드 서비스. |
| 커넥터 | Microsoft® SharePoint 2010 및 Microsoft® SharePoint 2013용 Adobe JCR Connector는 더 이상 사용되지 않습니다 [!DNL Experience Manager] 6.5. | 해당 없음 |

## 알려진 문제 {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THE LIST.
 -->

<!-- VULNERABILITY ISSUE - REMOVED MAY 23, 2022 AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * If you are using Content Fragments and GraphQL, Adobe recommends that you install the following packages on top of 6.5.12.0:

  * [AEM 6.5.12 Sites HotFix-NPR-38144](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Faem-service-pkg-6.5.12.0-NPR-38144-B0002.zip) (this hot fix replaces SP12, but can be installed on top of SP12) -->

* [GraphQL 색인 패키지 1.0.3이 있는 AEM 컨텐츠 조각](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.3.zip)

* 로서의 [!DNL Microsoft® Windows Server 2019] 을 지원하지 않음 [!DNL MySQL 5.7] 및 [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] 에 대한 턴키 설치를 지원하지 않습니다. [!DNL AEM Forms 6.5.10.0].

* 를 업그레이드하는 경우 [!DNL Experience Manager] 인스턴스(6.5에서 6.5.10.0 버전)를 `RRD4JReporter` 의 예외 `error.log` 파일. 문제를 해결하려면 인스턴스를 다시 시작합니다.

* 설치하는 경우 [!DNL Experience Manager] 6.5 서비스 팩 10 또는 이전 서비스 팩 [!DNL Experience Manager] 6.5, 자산 사용자 지정 워크플로우 모델의 런타임 사본(에서 생성) `/var/workflow/models/dam`)이 삭제됩니다.
런타임 복사본을 검색하려면 Adobe에서 HTTP API를 사용하여 사용자 지정 워크플로우 모델의 디자인 타임 사본을 해당 런타임 복사와 동기화하는 것이 좋습니다.
   `<designModelPath>/jcr:content.generate.json`.

* 사용자는 의 계층 구조에서 폴더의 이름을 바꿀 수 있습니다 [!DNL Assets] 중첩된 폴더를 [!DNL Brand Portal]. 그러나 폴더의 제목은에서 업데이트되지 않습니다 [!DNL Brand Portal] 루트 폴더를 다시 게시할 때까지 .

* 사용자가 적응형 양식에서 처음으로 필드를 구성하도록 선택하면 구성 저장 옵션이 속성 브라우저에 표시되지 않습니다. 동일한 편집기에서 적응형 양식의 다른 필드 일부를 구성하도록 선택하면 문제가 해결됩니다.

* 설치 중에 다음 오류 및 경고 메시지가 표시될 수 있습니다 [!DNL Experience Manager] 6.5.x.x:
   * Adobe Target 통합이 [!DNL Experience Manager] target Standard API(IMS 인증)를 사용한 다음, 경험 조각을 Target으로 내보내면 잘못된 오퍼 유형이 생성됩니다. 경험 조각/소스 Adobe Experience Manager 유형 대신 Target은 HTML/소스 Adobe Target Classic 유형으로 여러 가지 오퍼를 작성합니다.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: granite/operations/maintenance에 유지 관리 창이 없습니다.
   * SUM, MAX 및 MIN과 같은 집계 함수를 사용하는 경우 적용형 양식 서버측 유효성 검사가 실패합니다(CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance에 유지 관리 창이 없습니다.
   * 쇼퍼블 배너 뷰어를 통해 자산을 미리 볼 때 Dynamic Media 대화형 이미지의 핫스팟이 표시되지 않습니다.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : 등록 변경으로 등록 취소를 완료할 때까지 기다리는 중 시간이 초과되었습니다.

* 컨텐츠 조각 또는 사이트/페이지 를 이동/삭제/게시하려고 할 때 백그라운드 쿼리가 실패하여 컨텐츠 조각 참조를 가져오면 문제가 발생합니다. 즉, 기능이 작동하지 않습니다.
올바른 작업을 수행하려면 인덱스 정의 노드에 다음 속성을 추가해야 합니다 `/oak:index/damAssetLucene` (재색인화가 필요 없음):

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## OSGi 번들 및 컨텐츠 패키지가 포함됨 {#osgi-bundles-and-content-packages-included}

다음 텍스트 문서에는 다음 항목에 포함된 OSGi 번들 및 컨텐츠 패키지 목록이 나와 있습니다. [!DNL Experience Manager] 6.5.13.0:

* [Experience Manager 6.5.13.0에 포함된 OSGi 번들 목록](/help/release-notes/assets/65130_bundles.txt)

* [Experience Manager 6.5.13.0에 포함된 컨텐츠 패키지 목록](/help/release-notes/assets/65130_packages.txt)

## 제한된 웹 사이트 {#restricted-sites}

이러한 웹 사이트는 고객만 사용할 수 있습니다. 액세스가 필요한 고객의 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [Adobe 고객 지원 문의](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 제품 페이지](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 설명서](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ko-KR)
>* [Adobe 우선 순위 제품 업데이트](https://www.adobe.com/kr/subscription/priority-product-update.html) 구독

