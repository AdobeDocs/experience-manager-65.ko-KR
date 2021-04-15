---
title: '[!DNL Experience Manager] 6.5 서비스 팩 릴리스 노트'
description: ' [!DNL Adobe Experience Manager] 6.5 서비스 팩 8에 대한 릴리스 노트'
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
translation-type: tm+mt
source-git-commit: 9b23e9d5bbdbdde864ce71f434d6536439067f82
workflow-type: tm+mt
source-wordcount: '3413'
ht-degree: 17%

---

# [!DNL Adobe Experience Manager] 6.5 서비스 팩 릴리스 노트  {#aem-service-pack-release-notes}

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 버전 | 6.5.8.0 |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2021년 3월 11일 |
| 다운로드 URL | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip) |

<!-- TBD: Update the SD link when SP8 is available. Same link is duplicated below in install -->

## [!DNL Adobe Experience Manager] 6.5.8.0 {#what-s-included-in-aem}에 포함된 항목

[!DNL Adobe Experience Manager] 6.5.8.0에는 2019년 4월 6.5 릴리스 이후 릴리스된 새로운 기능, 고객의 요청에 따라 향상된 주요 기능, 성능, 안정성 및 보안 기능이 포함되어 있습니다. 서비스 팩이 [!DNL Adobe Experience Manager] 6.5에 설치되어 있습니다.

[!DNL Adobe Experience Manager] 6.5.8.0에 도입된 주요 기능 및 개선 사항은 다음과 같습니다.

<!-- TBD:
* Using the Connected Assets functionality, it is now possible to connect up to 3 [!DNL Sites] instances with 1 [!DNL Assets] instances. The configuration user interface now allows the administrators to provide the details of these [!DNL Sites] instances. -->

* 이제 [연결된 자산 기능](/help/assets/use-assets-across-connected-assets-instances.md)을 사용할 때 자산을 사용하는 모든 [!DNL Sites] 페이지의 목록을 볼 수 있습니다. 자산에 대한 이러한 참조는 자산의 [!UICONTROL 속성] 페이지에서 사용할 수 있습니다. 이를 통해 관리자, 마케터 및 라이브러리에서는 자산 사용량을 전체적으로 볼 수 있으므로 추적, 관리 및 브랜드 일관성을 향상시킬 수 있습니다.

* 웹 페이지에서 참조되는 자산을 삭제하면 [!DNL Experience Manager] [에 경고](/help/assets/use-assets-across-connected-assets-instances.md#asset-usage-references)가 표시됩니다. 참조된 자산을 강제로 삭제하거나 자산의 [!DNL Properties] 페이지에 표시되는 참조를 확인하고 수정할 수 있습니다. 참조를 클릭하면 로컬 및 원격 [!DNL Sites] 페이지가 열립니다.

* [!UICONTROL 이름], [!UICONTROL 마지막 수정 날짜,] 및 [!UICONTROL 마지막 롤아웃 날짜] 속성을 사용하여 롤아웃에 사용할 수 있는 Live Copy 페이지를 정렬합니다.

* 내장된 저장소(Apache Jackrabbit Oak)가 1.22.6. <!-- TBD: Mention the version -->

[!DNL Experience Manager] 6.5.8.0에 도입된 기능과 개선 사항의 전체 목록은 [서비스 팩 8](new-features-latest-service-pack.md)의 새로운 기능을 참조하십시오. [!DNL Adobe Experience Manager] 

다음은 [!DNL Experience Manager] 6.5.8.0 릴리스에서 제공된 수정 사항 목록입니다.

### [!DNL Sites] {#sites-6580}

* 페이지가 블루프린트로 이동되면 링크 대상이 업데이트되지 않습니다(NPR-35724).
* 티젠 기반 플레이어는 특정 브라우저에서 인증되지 않습니다. 이 문제는 samesite=none 속성을 지원하지 않는 브라우저에서 발생합니다(NPR-35589).
* 잠금 해제된 응답형 컨테이너는 허용된 구성 요소를 표시하지 않습니다(NPR-35565).
* 새로 추가된 페이지의 Live Copy를 만들 때 언어 마스터는 각 도메인에 대해 2개의 복사본을 만듭니다(NPR-35545).
* `org.apache.felix.scr.impl.ComponentRegistry` 타이머로 인해 많은 스레드가 차단된 경우 SCR 구성 요소 레지스트리의 교착 상태가 해결되었습니다. 따라서 [!DNL Experience Manager]은(는) 무기한 응답을 중지합니다(GRANITE-33125,FELIX-6252).
* 사이드 레일에서 특정 자산을 검색할 때 일부 검색되지 않은 자산이 결과에 포함됩니다(NPR-35524).
* Experience Manager 인스턴스에 대해 SSL을 활성화하면 컨텍스트 경로가 제거됩니다(NPR-35477).
* 목록을 만들고, 일부 텍스트를 첫 번째 요소로 추가하고, 표를 두 번째 요소로 추가하고, 표 내에 목록을 추가하면 상위 목록이 왜곡됩니다(NPR-35465).
* 연속 목록 항목에 서로 다른 플러그인을 사용하면 목록 항목에 추가 <br> 태그가 추가됩니다(NPR-35464).
* 두 단락 사이에 목록을 배치하면 목록에 표를 추가할 수 없습니다(NPR-35356).
* AEM 6.3에서 AEM 6.5로 AEM 인스턴스 업그레이드를 시작하면 업그레이드 인스턴스를 시작하는 데 시간이 더 오래 걸립니다(NPR-35323).
* 대괄호()를 포함하는 AEM 자산을 복제할 때. 이름으로 복제가 실패합니다(GRANITE-27004, NPR-35315).
* 리치 텍스트 편집기에 제목을 추가하면 단락 단추가 비활성화됩니다(NPR-35256).
* 기존 목록에 항목을 추가하면 다음 축소 가능 또는 전환 목록이 삭제됩니다(NPR-35206).
* [페이지 롤아웃] 옵션을 선택하면 사용 가능한 모든 Live Copy가 있는 대화 상자가 나타나고 자동 롤아웃이 수행됩니다. 페이지의 Live Copy는 사용자 작업 없이 모든 지역에 롤아웃됩니다(NPR-35138).
* 하위 포함 옵션을 사용하는 경우 게시 관리 옵션에 모든 페이지가 나열되지는 않습니다. 22페이지만 나열됩니다(NPR-35086).
* 정책을 편집해도 텍스트 구성 요소는 정책 변경 사항을 유지하지 않습니다(NPR-35070).
* 번호가 같은 항목의 경우 번호 매기기를 1부터 시작해야 하지만 번호 매기기 목록에서 일부 항목을 들여쓰면 모든 항목의 번호가 동일하게 유지됩니다(CQ-4313011).
* 축소가 활성화되면 페이지 또는 구성 요소를 편집할 수 없습니다. AEM 6.5 서비스 팩 7(CQ-4311133)을 설치한 후 문제가 시작되었습니다.
* 옴니 검색 및 자산 필터가 관련 없거나 결과가 없습니다(CQ-4312322, NPR-35793).
* 여러 페이지가 동시에 클라이언트 라이브러리에 액세스하면 HTML 라이브러리 관리자가 클라이언트 라이브러리를 로드하지 못합니다. 이로 인해 페이지가 잘못 렌더링됩니다(NPR-35538).
* [!DNL Experience Manager]에서 SSL을 설정하면 컨텍스트 경로가 자동으로 제거됩니다(NPR-35294).
* 패키지 관리자는 로그아웃 옵션(NPR-35160)을 클릭한 후 사용자를 로그아웃하지 않습니다.

### [!DNL Assets] {#assets-6580}

[!DNL Adobe Experience Manager] 6.5.8.0 [!DNL Assets] 는 다음 문제를 수정하고 다음 개선 사항을 제공합니다.

* 이전 버전의 에셋을 복원하면 OSGi 콘솔에서 이벤트 DamEvent.Type RESTORED가 트리거되지 않습니다(NPR-35789).
* `IndexWriter.merge` 스마트 태그 지정 기능으로 큰 색인 `OutOfMemoryError` 과  `/oak:index/lucene`   `/oak:index/ntBaseLucene` 인덱스가 생성되므로 오류 발생(NPR-35651)
* 이름에 멀티바이트 문자가 포함된 [!UICONTROL 자산 기여도] 유형 폴더를 저장하려 할 때 오류 메시지가 표시됩니다(NPR-35605).
* 계단식 메타데이터 하위 유형 필드를 사용하는 경우 잘못된 &#39;이 필드를 채우십시오&#39; 오류가 발생합니다(NPR-35643).
* 기존 에셋을 [!DNL Assets] 사용자 인터페이스에서 드래그하고 새 버전을 만들면 메타데이터의 변경 내용이 지속되지 않습니다(NPR-34940).
* 계단식 메뉴에 대한 메타데이터 스키마 편집기에서 규칙을 만들 때 [!UICONTROL 종속적 기준] 옵션이 동일한 이름을 반복합니다(NPR-35596).
* 유사성 검색은 [!UICONTROL 자산 관리자 검색 레일](NPR-35588)을 편집한 후 작동하지 않습니다.
* 폴더 내에서 [!UICONTROL 필터]를 클릭하여 왼쪽 레일에서 자산 검색을 여는 경우 [!UICONTROL 상태] > [!UICONTROL 체크아웃] > [!UICONTROL 체크 아웃한]의 필터가 작동하지 않습니다(NPR-35530).
* 에셋의 모든 스마트 태그를 삭제하고 변경 내용을 저장하려고 하면 태그가 제거되지 않습니다. 하지만 사용자 인터페이스는 변경 사항이 저장되었음을 나타냅니다(NPR-35519).
* 사용자는 주문 가능한 폴더의 목록 보기에서 자산을 다시 정렬하거나 정렬할 수 없습니다(NPR-35516).
* 기본 메타데이터 스키마를 편집하는 경우 자산의 [!UICONTROL 속성] 페이지의 태그 필드가 텍스트 필드로 변경됩니다. 이 변경 사항을 통해 모르는 사용자가 온디맨드 태그를 추가할 수 있으며 태그는 저장소의 문자열로 저장됩니다(NPR-35478).
* 자산을 다운로드할 때, 올바른 이메일 주소가 없는 이름을 제공하면 다운로드 옵션을 사용할 수 없습니다. 그러나 다운로드 대화 상자의 다른 옵션을 선택하면 단추가 활성화되지만 전자 메일이 전송되지 않습니다(NPR-35365).
* 사용자는 [!DNL Adobe InDesign]의 에셋을 편집한 후 로그인 에셋을 확인할 수 없으며 권한 부족에 대한 오류를 수신합니다(NPR-35341).
* handlebars JavaScript 라이브러리는 v4.7.6(NPR-35333)로 업그레이드됩니다.
* 벌크 메타데이터 편집 및 항목 선택 취소 작업을 시작할 때 단일 항목을 선택할 때까지 메타데이터 편집기 인터페이스가 예상대로 작동되지 않습니다(NPR-35144).
* `assets.html` 페이지(CQ-4312311) 내에서 클릭하면 글로벌 탐색이 올바른 콘솔을 열지 않습니다.
* [!DNL Assets] 은 RGB 변환이 있는 자산에 대한 RGB 변환을 표시하지 않습니다(CQ-4310190).
* 메뉴의 [!UICONTROL 관계] 옵션이 [!UICONTROL 속성] 페이지(CQ-4310188)에 제대로 표시되지 않습니다.
* 자산을 검색하고 Smart Collection을 만드는 데 문서에 대한 파일 유형 필터를 사용하는 경우 컬렉션에 액세스할 때 필터가 적용되지 않습니다. 대신 모든 유형의 에셋이 검색에 표시됩니다(NPR-35759).
* [!DNL Assets] 사용자 인터페이스에서 Lightbox에 자산을 드래그하여 추가할 수 없습니다(NPR-35901).
* 이름 지정 충돌을 해결한 후 기존 자산의 새 버전을 만들면 원래 자산의 메타데이터를 덮어씁니다(CQ-4313594).
* 검색 필터 또는 조건자를 사용하여 자산 검색을 필터링하고, 보거나 편집할 자산을 열고, 검색 결과 페이지로 돌아가면 필터가 작동하지 않습니다. 검색된 모든 자산이 필터링되지 않은 상태로 나열됩니다(NPR-35913).

#### [!DNL Dynamic Media] {#dynamic-media-6580}

* RESS 이미지 사전 설정에 대한 URL 옵션은 자산 세부 사항 페이지에서 활성화됩니다. 이제 다이내믹 표현물 섹션에서 RESS 이미지 사전 설정을 선택하면 자산 세부 사항 페이지에서 URL 및 RESS 옵션을 모두 사용할 수 있습니다. (CQ-4311241)
* 대화형 미디어 구성 요소 - 사용자가 선택적 게시 구성을 가진 [!DNL Experience Manager]이(가) 있는 경우 대화형 비디오가 작동하지 않습니다(CQ-4311054).
* 폴더 간에 에셋을 이동하는 경우 API를 통해 [!DNL Experience Manager]과 [!DNL Dynamic Media–Scene7] 간의 동기화가 매우 느립니다(CQ-4310001).
* Omnisearch를 사용할 경우 로그 크기가 크게 증가합니다(CQ-4309153).
* 선택적 동기화가 활성화되어 있고 자산이 동기화 폴더로 복사(이동되지 않음)되면 예상대로 동기화되지 않습니다(CQ-4307122).
* DM에 자동으로 게시되는 업로드된 자산의 경우 상태가 AEM에 게시됨으로 표시되지 않습니다. 또한 Dynamic Media 게시 상태 열에는 올바른 게시된 상태가 표시되지 않습니다(CQ-4306415).
* 자산이 [!DNL Experience Manager]에 게시되고 활성화 시 [!DNL Dynamic Media]에 게시하도록 설정된 경우 `scene7FileStatus` 메타데이터 값이 예상대로 업데이트되지 않습니다(CQ-4308269).
* 비디오 프로필을 편집할 때 [!DNL Experience Manager]은(는) 비디오 사전 설정에 설정된 높이 및 비트 전송률 값을 표시하지 않습니다. 필드가 비어 있습니다(CQ-4311828).

### [!DNL Commerce] {#commerce-6580}

* 상거래의 모든 제품에 대한 사용자 지정 태그를 만들 수 없습니다(CQ-4310682).

* 제품 자산 참조 업데이트는 ProductAssetListener 스레드가 JCR에 대한 커밋을 완료할 때까지 복제 스레드가 대기 상태로 유지되도록 합니다(NPR-35269).

### 플랫폼 {#platform-6580}

* 탭이 없는 Coral Tab View 구성 요소를 사용한 다음 Foundation 유효성 검사기를 트리거하면 다음 오류가 발생합니다(NPR-35636).

   ```TXT
    Uncaught TypeError: Cannot set property 'invalid' of undefined
     at enable (foundation.js:10703)
     at foundation.js:10710
   ```

* 이름에 쉼표를 포함하는 노드의 Delete 이벤트에 대해 SCD 전달 복제가 실패합니다(NPR-35191).

* AEM 6.5.7으로 업그레이드하면 빌드가 실패합니다. 이유는, 이전 버전이나 잭슨 코어가 uber-jar (GRANITE-33006)에 포함되어 있지 않기 때문입니다.

### 사용자 인터페이스 {#ui-6580}

* 자산 콘솔의 폴더에 있는 문서의 카드 보기에서 목록 보기로 전환하면 정렬이 제대로 작동하지 않습니다(NPR-35842).

* 텍스트 구성 요소의 텍스트에 하이퍼링크를 지정하면 검색 기능에 적절한 결과가 표시되지 않습니다(NPR-35849).

* 필수 항목으로 표시된 숨김 필드에 값을 제공하지 않으면 구성 요소를 저장할 수 없습니다(NPR-35219).

### 통합 {#integrations-6580}

* IMS 테넌트 ID 및 Target 클라이언트 코드에 대해 다른 값을 사용하는 경우 [!DNL Experience Manager]이(가) [!DNL Adobe Target]과(와) 통합되지 않습니다(NPR-35342).

### 번역 프로젝트 {#translation-6580}

* [!DNL Experience Manager]에서 번역 작업을 내보내거나 가져올 때 발생하는 문제(NPR-35259).

### 캠페인 {#campaign-6580}

* Touch UI에서 즉시 사용 가능한 템플릿을 사용하여 캠페인 페이지를 만들고 페이지 속성 대화 상자에서 이메일 탭을 열면 제목과 본문 필드에 대한 개인화 변수가 비활성화된 상태로 유지됩니다(CQ-4312388).

### [!DNL Communities] {#communities-6580}

* 커뮤니티 그룹에 페이지 구조를 추가하면 탐색 표시의 [!UICONTROL 그룹] 제목이 첫 번째 [!UICONTROL 페이지](NPR-35803)의 제목으로 변경됩니다.
* 중재자와 달리 표준 커뮤니티 구성원은 초안 게시물에 액세스하고 편집할 수 없습니다(NPR-35339).
* 색인화가 완료될 때까지 커뮤니티 사이트를 다운시키는 `DSRPReindexServlet`의 액세스 제어 및 서비스 거부(DoS) 기능이 끊겼습니다(NPR-35591).
* [!UICONTROL 관리자] 필드에서 [!UICONTROL 모든 사용자]를 제거해도 실제로 백엔드에서 제거되지 않습니다(NPR-35592, NPR-35611).
* 입력한 텍스트가 부분 일치(NPR-35666)인 경우 [!UICONTROL 메시지 작성] 구성 요소는 결과를 반환하지 않습니다.

* **[!UICONTROL 태그 추가]**&#x200B;를 선택하여 새 블로그에 태그를 추가하려고 할 때 성능 저하 및 둔화를 확인할 수 있습니다. 성능을 향상시키려면 [!DNL Software Distribution]에서 사용할 수 있는 [cqTagLucene-0.0.1.zip 핫픽스](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cqTagLucene-0.0.1.zip)를 설치하십시오.

### [!DNL Brand Portal] {#brandportal-6580}

* [!UICONTROL 자산 기여도] 유형 폴더에 멤버를 추가하면 사용자 인터페이스에 [!UICONTROL 사용자 또는 그룹 추가] 캡션이 표시됩니다. 단, 브랜드 포털 활성 사용자만 지원되고 그룹은 지원되지 않습니다(NPR-35332).

### [!DNL Forms] {#forms-6580}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 예약된  [!DNL Experience Manager] 서비스 팩 릴리스 날짜 이후 1주일 후에 추가 기능 패키지를 릴리스합니다.

**적응형 양식**

* 반복 가능한 행이 있는 표를 응용 양식에 있는 여러 인스턴스가 있는 반복 가능한 패널에 삽입하면 테이블이 항상 패널의 첫 번째 인스턴스에 추가됩니다(NPR-35635).

* 탭 포커스가 응용 형식으로 한 번 확인한 후 CAPTCHA 구성 요소에 다시 도달하면 [!DNL Experience Manager Forms]에 `Provide Captcha phrase to proceed` 오류 메시지(NPR-35539)가 표시됩니다.

**대화형 통신**

* 번역된 양식을 제출하면 제출 메시지가 영어로 표시되고 해당 언어로 번역되지 않습니다(NPR-35808).

* 첨부된 XDP 또는 문서 조각에 숨기기 조건을 포함하면 대화형 통신이 로드되지 못합니다(NPR-35745).

**서신 관리**

* 편지를 편집할 때 조건이 있는 모듈을 로드하는 데 시간이 더 오래 걸립니다(NPR-35325).

* 편지에 포함되지 않은 왼쪽 탐색 창에서 자산을 선택한 다음 다음 자산을 선택하면 파란색 강조 표시가 이전에 선택한 자산에서 제거되지 않습니다(NPR-35851).

* 문자로 텍스트 필드를 편집할 때 [!DNL Experience Manager Forms]에 `Text Edit Failed` 오류 메시지가 표시됩니다(CQ-4313770).

**워크플로우**

* iOS용 [!DNL Experience Manager Forms] 모바일 응용 프로그램에서 응용 양식을 열려고 하면 응용 프로그램이 응답하기 위해 중지됩니다(CQ-4314825).

* HTML 작업 영역의 [!UICONTROL To-do] 탭에는 HTML 문자가 표시됩니다(NPR-35298).

**XMLFM**

* 출력 서비스를 사용하여 XML 문서를 생성할 때 일부 XML 파일에 대해 `OutputServiceException` 오류가 발생합니다(CQ-4311341, CQ-4313893).

* 글머리 기호 첫 번째 문자에 위 첨자 속성을 적용하면 글머리 기호 크기가 작아집니다(CQ-4306476).

* 출력 서비스를 사용하여 생성된 PDF forms에는 테두리가 포함되지 않습니다(CQ-4312564).

**디자이너**

* [!DNL Experience Manager Forms] Designer에서 XDP 파일을 열면 designer.log 파일이 XDP 파일과 동일한 폴더에 생성됩니다(CQ-4309427, CQ-4310865).

**HTML5 양식**

* [!DNL iOS 14.1 or 14.2]에 대한 [!DNL Safari] 웹 브라우저의 응용 형식으로 확인란을 선택하면 추가 필드가 표시되지 않습니다(NPR-35652).

**Forms 관리**

* XDP 파일을 CRX 저장소에 성공적으로 업로드했음을 나타내는 확인 메시지가 없습니다(NPR-35546).

**문서 보안**

* AdminUI의 [!UICONTROL 정책 편집] 옵션에 대해 여러 문제가 보고되었습니다(NPR-35747).

보안 업데이트에 대한 자세한 내용은 [Experience Manager 보안 게시판 페이지](https://helpx.adobe.com/security/products/experience-manager.html)를 참조하십시오.

## 6.5.8.0 설치 {#install}

**설정 요구 사항 및 자세한 정보**

* Experience Manager 6.5.8.0에는 Experience Manager 6.5가 필요합니다. 자세한 지침은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하십시오.
* 서비스 팩은 Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 다운로드할 수 있습니다.
* MongoDB와 여러 인스턴스가 포함된 배포에서는 패키지 관리자를 사용하여 작성자 인스턴스 중 하나에 Experience Manager 6.5.8.0을 설치합니다.

>[!NOTE]
>
>Adobe에서는 [!DNL Adobe Experience Manager] 6.5.8.0 패키지를 제거하거나 제거할 것을 권장하지 않습니다.

### 서비스 팩 {#install-service-pack} 설치

[!DNL Adobe Experience Manager] 6.5 인스턴스에 서비스 팩을 설치하려면 다음 단계를 수행합니다.

1. 인스턴스가 업데이트 모드인 경우 설치 전에 인스턴스를 다시 시작합니다(이전 버전에서 인스턴스가 업데이트된 경우임). Adobe에서는 인스턴스에 대한 현재 가동 시간이 높은 경우 다시 시작하는 것이 좋습니다.

1. 설치하기 전에 스냅샷 또는 [!DNL Experience Manager] 인스턴스의 새 백업을 만듭니다.

1. [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip)에서 서비스 팩을 다운로드합니다.

1. 패키지 관리자를 열고 **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭하여 패키지를 업로드합니다. 자세한 내용은 [패키지 관리자](/help/sites-administering/package-manager.md)를 참조하십시오.

1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

1. S3 커넥터를 업데이트하려면 서비스 팩 설치 후 인스턴스를 중지하고, 기존 커넥터를 설치 폴더에 제공된 새 이진 파일로 바꾼 후 인스턴스를 다시 시작합니다. [Amazon S3 데이터 저장소](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)를 참조하십시오.

>[!NOTE]
>
>패키지 관리자 UI에 대한 대화 상자가 서비스 팩을 설치하는 동안 종료되는 경우가 있습니다. 배포에 액세스하기 전에 오류 로그가 안정될 때까지 기다리는 것이 좋습니다. 업데이터 번들 제거와 관련된 특정 로그를 기다린 후 설치가 성공했는지 확인합니다. 일반적으로 이러한 작업은 [!DNL Safari]에서 발생하지만 모든 브라우저에서 간헐적으로 발생할 수 있습니다.

**자동 설치**

작업 인스턴스에 Adobe Experience Manager 6.5.8.0을 자동으로 설치하는 두 가지 방법이 있습니다.

A. 서버가 온라인 상태일 때 패키지를 `../crx-quickstart/install` 폴더에 넣습니다. 패키지가 자동으로 설치됩니다.

B. [패키지 관리자에서 HTTP API](/help/sites-administering/package-manager.md#package-share)를 사용합니다. 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

>[!NOTE]
>
>Adobe Experience Manager 6.5.8.0은 Bootstrap 설치를 지원하지 않습니다.

**설치 확인**

1. 제품 정보 페이지(`/system/console/productinfo`)에는 [!UICONTROL 설치된 제품] 아래에 업데이트된 버전 문자열 `Adobe Experience Manager (6.5.8.0)`이 표시됩니다.

1. 모든 OSGI 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]**&#x200B;이거나 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 콘솔 사용: `/system/console/bundles`).

1. OSGi 번들 `org.apache.jackrabbit.oak-core`은 버전 1.22.3 이상입니다(웹 콘솔 사용:`/system/console/bundles`).

이번 릴리스에서 사용할 수 있는 인증된 플랫폼을 확인하려면 [기술 요구 사항](/help/sites-deploying/technical-requirements.md)을 참조하십시오.

### Adobe Experience Manager Forms 추가 기능 패키지 설치 {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Experience Manager Forms을 사용하지 않는 경우 건너뜁니다. Experience Manager Forms의 수정 사항은 예약된 [!DNL Experience Manager] 서비스 팩 릴리스 이후 1주일 후에 별도의 추가 기능 패키지를 통해 제공됩니다.

1. Adobe Experience Manager 서비스 팩을 설치했는지 확인합니다.
1. 운영 체제에 대한 [AEM Forms 릴리스](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html)에 나열된 해당 양식 추가 기능 패키지를 다운로드합니다.
1. [AEM Forms 추가 기능 패키지 설치](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)에 설명된 대로 양식 추가 기능 패키지를 설치합니다.

>[!NOTE]
>
>AEM 6.5.8.0에는 [AEM Forms 호환성 패키지](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases)의 새 버전이 포함되어 있습니다. 이전 버전의 AEM Forms 호환성 패키지를 사용하고 AEM 6.5.8.0으로 업데이트하는 경우 Forms Add-On 패키지의 패키지 설치 후 최신 버전의 패키지를 설치합니다.

### JEE에 Adobe Experience Manager Forms 설치 {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE에서 AEM Forms를 사용하지 않는 경우 건너뜁니다. 별도의 설치 프로그램을 통해 JEE의 Adobe Experience Manager Forms 수정 사항이 전달됩니다.

JEE에 Forms Experience Manager용 누적 설치 프로그램 및 배포 후 구성에 대한 자세한 내용은 [릴리스 노트](jee-patch-installer-65.md)를 참조하십시오.

>[!NOTE]
>
>JEE에 Forms Experience Manager용 누적 설치 프로그램을 설치한 후 최신 Forms 추가 기능 패키지를 설치하고 `crx-repository\install` 폴더에서 Forms 추가 기능 패키지를 삭제하고 서버를 다시 시작합니다.

### UberJar {#uber-jar}

Experience Manager 6.5.8.0용 UberJar는 [Maven Central 리포지토리](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.8/)에서 사용할 수 있습니다.

Maven 프로젝트에서 UberJar를 사용하려면 [Uberjar 사용 방법](/help/sites-developing/ht-projects-maven.md)을 참조하여 프로젝트 POM에 다음 종속성을 포함하십시오.

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.8</version>
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
| 통합 | **[!UICONTROL AEM 클라우드 서비스 옵트인]** 화면은 더 이상 사용되지 않습니다. Experience Manager 6.5에서 업데이트되어 Adobe IMS 및 I/O를 통한 인증을 사용하는 Adobe Target Standard API와 분석 및 개인화를 위한 Experience Manager 페이지를 구현하기 위한 Adobe Launch의 역할이 증가하면서 옵트인 마법사는 기능적으로 사용할 수 없게 되었습니다. | 해당 Experience Manager 클라우드 서비스를 통해 시스템 연결, Adobe IMS 인증 및 [!DNL Adobe I/O] 통합을 구성합니다. |
| 커넥터 | Adobe JCR Connector for Microsoft SharePoint 2010 및 Microsoft SharePoint 2013은 Experience Manager 6.5에서 더 이상 사용하지 않습니다. | N/A |

## 알려진 문제 {#known-issues}

* [!DNL Experience Manager] 인스턴스를 6.5에서 6.5.8.0 버전으로 업그레이드하는 경우 `error.log` 파일에서 `RRD4JReporter` 예외를 볼 수 있습니다. 인스턴스를 다시 시작하여 문제를 해결합니다.

* [!DNL Experience Manager] 6.5에 [!DNL Experience Manager] 6.5 서비스 팩 5 또는 이전 서비스 팩을 설치하는 경우, `/var/workflow/models/dam`에서 만든 자산 사용자 지정 워크플로우 모델의 런타임 복사본이 삭제됩니다.
런타임 복사본을 검색하려면 HTTP API를 사용하여 사용자 지정 워크플로우 모델의 디자인 타임 사본을 해당 런타임 복사본과 동기화하는 것이 좋습니다.
   `<designModelPath>/jcr:content.generate.json`.

* [!UICONTROL 규칙 정의] 대화 상자를 사용하여 [!UICONTROL 폴더 메타데이터 스키마 Forms 편집기] 및 [!UICONTROL 메타데이터 스키마 Forms 편집기]에서 계단식 규칙을 편집하고 만들 때 문제가 발생하면 Adobe 고객 지원 센터에 문의하십시오. 이미 만들고 저장한 규칙이 예상대로 작동합니다.

* 계층 구조의 한 폴더의 이름이 [!DNL Experience Manager Assets]에서 변경되고 자산이 있는 중첩된 폴더가 [!DNL Brand Portal]에 게시되는 경우 루트 폴더가 다시 게시될 때까지 폴더의 제목이 [!DNL Brand Portal]에서 업데이트되지 않습니다.

* 사용자가 적응형 양식에서 처음으로 필드를 구성하도록 선택하면 구성 저장 옵션이 속성 브라우저에 표시되지 않습니다. 동일한 편집기에서 적응형 양식의 다른 필드 일부를 구성하도록 선택하면 문제가 해결됩니다.

* [!UICONTROL 연결된 자산 구성] 마법사가 설치 후 404 오류 메시지를 반환하는 경우 패키지 관리자를 사용하여 `cq-remotedam-client-ui-content` 및 `cq-remotedam-client-ui-components` 패키지를 수동으로 다시 설치합니다.

* Experience Manager 6.5.x.x를 설치하는 동안 다음 오류 및 경고 메시지가 표시될 수 있습니다.
   * &quot;Adobe Target 통합이 Target Standard API(IMS 인증)를 사용하여 Experience Manager에 구성된 경우 경험 조각을 Target으로 내보내면 잘못된 오퍼 유형이 생성됩니다. 경험 조각/소스 Adobe Experience Manager 유형 대신 Target은 HTML/소스 Adobe Target Classic 유형으로 여러 가지 오퍼를 작성합니다.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: granite/operations/maintenance에 유지 관리 창이 없습니다.
   * SUM, MAX 및 MIN과 같은 집계 함수를 사용하는 경우 적응형 양식 서버측 유효성 검사가 실패합니다(CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance에 유지 관리 창이 없습니다.
   * 쇼퍼블 배너 뷰어를 통해 자산을 미리 볼 때 Dynamic Media 대화형 이미지의 핫스팟이 표시되지 않습니다.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :레지스트리 변경 완료 대기 시간 제한.

## OSGi 번들 및 콘텐츠 패키지가 설치됨 {#osgi-bundles-and-content-packages-included}

다음 텍스트 문서에는 [!DNL Experience Manager] 6.5.8.0에 포함된 OSGi 번들 및 컨텐츠 패키지가 나열됩니다.

* [Experience Manager 6.5.8.0에 포함된 OSGi 번들 목록](assets/6580_bundles.txt)

* [Experience Manager 6.5.8.0에 포함된 컨텐츠 패키지 목록](assets/6580_packages.txt)

## 제한된 웹 사이트 {#restricted-sites}

이러한 웹 사이트는 고객에게만 제공됩니다. 액세스가 필요한 고객의 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* Adobe 고객 지원 센터](https://experienceleague.adobe.com/docs/customer-one/using/home.html)에 문의하는 방법을 참조하십시오.[

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5 릴리스 노트](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] 제품 페이지](https://www.adobe.com/kr/marketing/experience-manager.html)
>* [[!DNL Experience Manager] 6.5 설명서](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* [Adobe 우선 순위 제품 업데이트](https://www.adobe.com/subscription/priority-product-update.html) 구독

