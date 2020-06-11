---
title: Adobe Experience Manager 6.5 이전 서비스 팩 릴리스 노트
description: Adobe Experience Manager 6.5 서비스 팩 3 이하에 대한 릴리스 노트입니다.
contentOwner: AK
translation-type: tm+mt
source-git-commit: b2b8178f96d1e0a551a58ba649443aa03f0608ac
workflow-type: tm+mt
source-wordcount: '8094'
ht-degree: 90%

---


# 이전 서비스 팩에 포함된 핫픽스 및 기능 팩 {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## Adobe Experience Manager 6.5.4.0 {#experience-manager-6540}

Adobe Experience Manager 6.5.4.0은 **2019년 4월** 6.5 릴리스의 공식 출시 이후 릴리스된 새로운 기능, 주요 고객이 요청한 향상된 기능 및 성능, 안정성, 보안 개선 사항이 포함된 중요한 업데이트입니다. Adobe Experience Manager 6.5 위에 설치할 수 있습니다.

Adobe Experience Manager 6.5.4.0에 도입된 주요 기능 및 개선 사항은 다음과 같습니다.

* Adobe Experience Manager Assets는 이제 Adobe I/O 콘솔을 통해 브랜드 포털로 구성됩니다.

* A new [Generate printable Output](../forms/using/aem-forms-workflow-step-reference.md) step is now available for Adobe Experience Manager Forms workflows.

* 적용형 양식 및 대화형 커뮤니케이션용 레이아웃 모드에 대한 [다중 열을 지원](../forms/using/resize-using-layout-mode.md)합니다.

* HTML5 양식의 [리치 텍스트](../forms/using/designing-form-template.md)를 지원합니다.

* Experience Manager Assets의 [액세스 가능성이 개선](new-features-latest-service-pack.md#accessibility-enhancements)되었습니다.

* 내장된 저장소(Apache Jackrabbit Oak)가 버전 1.10.8으로 업데이트되었습니다.

* 이제 선택적 컨텐츠 하위 트리를 `content/dam`에서 사용하는 대신 *Dynamic Media - Scene7 모드*&#x200B;로 동기화할 수 있습니다.

* 이제 SOAP 웹 서비스와 양식 데이터 모델 통합을 통해 요소에 대한 선택 그룹 또는 속성을 지원합니다.

* 이제 SOAP 입력 또는 출력 및 복잡한 데이터 구조가 Dynamic Group 대체를 지원합니다.

최신 서비스 팩에 포함된 기능 및 주요 특징 [의 전체 목록을 살펴보려면 Adobe Experience Manager 6.5 서비스 팩의 새로운 기능을 참조하십시오](new-features-latest-service-pack.md).

### 사이트 {#sites-fixes}

* Adobe Experience Manager Sites 페이지의 URL에 콜론(`:`) 또는 백분율 기호(`%`)가 포함되어 있으면 브라우저가 응답을 중단하고 CPU 사용 스파이크(NPR-32369, NPR-31918)가 발생합니다.

* Experience Manager Sites 페이지를 열어 편집하고 구성 요소를 복사해도 일부 자리 표시자에 대해 붙여넣기 작업을 수행할 수 없습니다(NPR-32317).

* 게시 관리 마법사가 열리면 코어 구성 요소에 연결된 경험 구성 요소가 게시된 참조 목록에 표시되지 않습니다(NPR-32233).

* Touch UI의 Live Copy 개요는 클래식 UI보다 렌더링하는 데 훨씬 시간이 오래 걸립니다(NPR-32149).

* 서버 시간과 컴퓨터 시간이 다른 시간대에 있는 경우 예약된 게시 시간은 Touch UI에 서버 시간을 표시하지만 클래식 UI에서는 시스템 시간이 표시됩니다(NPR-32077).

* Experience Manager Sites에서 URL에 접미어를 붙인 페이지를 열지 못했습니다(NPR-32072).

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

* 지원되는 3D 모델을 Experience Manager로 인제스트할 경우 3D 자산 축소판은 도움이 되지 않습니다(CQ-4283701).

* 스마트 자르기 비디오 뷰어 사전 설정이 처리되지 않은 상태로 사전 설정 이름과 함께 배너 텍스트에 두 번 표시됩니다(CQ-4283517).

* 3D Viewer에서 업로드된 3D 모델을 미리 보기했을 때 모델의 잘못된 컨테이너 높이가 자산 세부 정보 페이지에서 확인되었습니다(CQ-4283309).

* 캐러셀 편집기가 Experience Manager Dynamic Media 하이브리드 모드로 IE 11에서 열리지 않습니다(CQ-425590).

* Chrome 및 Safari 브라우저에서 다운로드 대화 상자에 있는 이메일 드롭다운에서 키보드 포커스가 멈춥니다(NPR-32067).

* Experience Manager에서 DM 클라우드 구성을 추가하려고 하는 동안 모든 콘텐츠 동기화 확인란이 기본적으로 활성화되어 있지 않습니다(CQ-4288533).

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

* Brand Portal users are not able to publish contribution folder assets to [!DNL Assets] on upgrading to Adobe I/O on Experience Manager 6.5.4 (CQDOC-15655). For an immediate fix on Experience Manager 6.5.4, it is recommended to [download the hotfix](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041) and install on your author instance.

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
>Experience Manager Service Pack에는 Experience Manager Forms에 대한 수정 사항이 포함되어 있지 않습니다. 이러한 수정 사항은 별도의 Forms 추가 기능 패키지를 사용하여 전달됩니다. 또한 JEE에서 Adobe Experience Manager Forms에 대한 수정 사항이 포함된 누적 설치 프로그램이 출시됩니다. 자세한 내용은 [Experience Manager Forms 추가 기능 설치](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) 및 [JEE에 Experience Manager Forms 설치](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)를 참조하십시오.

* 서신 관리: 게시 처리 워크플로우에 제출하면 편지에 추가 문자가 표시됩니다(NPR-32626).

* 서신 관리: 게시 처리 워크플로우에 제출하면 편지에 드롭다운 자리 표시자가 텍스트 구성 요소로 표시됩니다(NPR-32539).

* 서신 관리: 편지 템플릿에 정의된 기본값이 미리 보기 모드에서 표시되지 않습니다(NPR-32511).

* 모바일 양식: HTML 버전에서 XDP 양식을 렌더링하는 동안 제출 버튼 크기가 확장되어 표시됩니다(NPR-32514).

* 문서 서비스: 서비스 팩 2를 적용한 후 편지 및 일부 기타 페이지의 URL에 액세스하는 데 문제가 발생합니다(NPR-32508, NPR-32509).

* Document Services: If the number of transactions on a server exceeds a specific limit, the HTML to PDF conversion fails and the file type settings are removed from [!DNL Forms] server (NPR-32204).

* 적용형 양식: WCAG2 레벨 AA 지침에 따라 브라우저 접근성 도구가 적용형 양식의 오류를 보고합니다(NPR-32312, NPR-32309, CQ-4285439).

* 적용형 양식: Chrome 브라우저 접근성 도구가 모범 사례 오류를 보고합니다(NPR-32310).

* 적응형 양식: Experience Manager Sites 페이지에 포함된 적응형 양식을 구성하는 동안 번역 문제가 발생했습니다(NPR-32168).

* Workbench: PDF 유틸리티 서비스에 PDF 속성 가져오기 작업을 사용하는 동안 오류 메시지가 표시됩니다(NPR-32150).

* 문서 보안: DisableGlobalOfflineSynchronizationData 옵션이 True로 설정되어 보호된 PDF 파일을 오프라인으로 열 수 없습니다(NPR-32078).

* 디자이너: 태그 지정 옵션이 활성화된 경우 생성된 PDF 출력에서 하위 양식 테두리가 사라집니다(NPR-32547, NPR-31983, NPR-31950).

* 디자이너: 표에 병합된 셀이 있는 경우 출력 서비스를 사용하여 XDP 양식에서 변환된 출력 PDF 파일에 접근성 테스트를 수행하면 오류가 발생합니다(CQ-4285372).

* 재단 JEE: Experience Manager Forms 서버가 클러스터에서 연결이 끊긴 경우 캐싱 문제로 인해 서버가 서버에 다시 연결되지 않습니다(NPR-32412).

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

* 만들어진 날짜에 대한 새 열(정렬 가능)이 목록 보기의 DAM 목록 보기 및 자산 검색 결과에 추가됩니다(NPR-31312).

* 목록 보기에서 [!UICONTROL 이름] 열(NPR-31299)을 사용하여 자산 목록을 정렬할 수 있습니다.

* The GLB, GLTF, OBJ, and STL files can be previewed in [!UICONTROL Asset Details] page in DAM (CQ-4282277).

* `ReplicationOnModifyListener` 이벤트가 [!DNL Dynamic Media]에서 청크 업로드 중 청크 노드에 대해 트리거됩니다(CQ-4281279).

* 이제 [!DNL Dynamic Media]에서 스마트 자르기 비디오 자산을 지원합니다. 스마트 자르기는 장면의 초점을 따라 프레임을 이동하면서 비디오를 다시 자르도록 하는 머신 러닝 기반의 기능입니다(CQ-4278995).

* [!DNL Dynamic Media]에서 스마트 이미징을 지원합니다(CQ-422249).

* 요청(NPR-31601)에서 쿼리 매개 변수가 전달되면 검색 또는 찾아보기 보기가 기본 보기로 설정된 경우,

**수정 사항**

* 일부 PDF 문서의 제목이 수정될 때 일부 PDF 문서의 메타데이터는 업데이트되지 않고 PDF에 저장됩니다(NPR-31629).

* 파일 이름(NPR-31547)에 더하기 문자(`+`)가 있는 자산에 대해 자산 공유가 작동하지 않습니다.

* 기본 검색 양식 자산 관리 * 검색 레일의 편집이 예상대로 작동하지 않습니다(NPR-31502).

<!-- Review: Check if this seemingly stray asterisk is needed there or not.
-->

* 자산 보기에서 Omnisearch를 사용하여 자산 검색(NPR-31496)할 때는 제안이 표시되지 않습니다.

* 다른 사용자가 동일한 자산을 다른 컬렉션에서 참조하는 경우 참조된 자산을 다른 위치로 이동할 때 컬렉션 내의 자산 참조는 업데이트되지 않습니다(NPR-31486).

* 중복된 IPTC 태그가 자산 메타데이터에 추가됩니다(NPR-31328).

* 필터 레일에서 검색이 트리거될 때 검색 결과 카운트가 정확하게 업데이트되지 않습니다(NPR-31316).

* 파일 유형 필터에서 두 번째 수준 확인란을 선택 해제하면 모든 확인란이 선택 취소되고 검색 막대의 텍스트가 선택한 속성이나 선택 취소된 속성과 동기화되지 않습니다(NPR-31287).

* 모든 구성원(사용자/그룹)은 폴더의 멤버 섹션에서 제거할 수 없습니다. 모든 사용자를 제거하려고 하면 로그인한 사용자가 목록에 추가됩니다(NPR-31171).

* Assets with a plus symbol (`+`) in the file name cannot be deleted (NPR-31162).

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

* DAM Event Purge deletes the latest (`maxSavedActivities`) event data and holds the data created earlier (NPR-31336).

* Omnisearch를 통해 수행한 터치 UI 검색 결과 페이지가 자동으로 스크롤되어 사용자의 스크롤 위치가 손실됩니다(NPR-31307).

* 모두 선택한 다음 터치 UI에서 일부 항목(폴더/개별 자산)을 선택 해제할 때 작업 표시줄 및 자산 수가 업데이트되지 않습니다(NPR-31118).

* 자산에 대한 작업 세부 사항을 폴링하는 동안 [!DNL Experience Manager]에 예외가 표시됩니다(CQ-4283569).

### 사이트 {#sites}

* LiveCopy 상속이 끊어지면 LiveCopy 페이지에 LiveCopy 링크 대신 언어 복사 링크가 표시됩니다(NPR-30980).
* 새 블루프린트의 경우 레코드 수가 40개를 초과하는 경우 처음 40개의 레코드만 표시됩니다. 블루프린트는 나머지 레코드에 대한 빈 라인을 표시합니다(NPR-31182).
* 사용자가 메뉴의 설명 속성에 일본어 또는 한국어 문자를 추가하면 메뉴에 일본어 및 한국어 텍스트의 왜곡된 문자가 표시됩니다(NPR-31331).
* 리치 텍스트 편집기(RTE)가 포함된 테이블을 목록 항목으로 삽입할 수 없습니다(NPR-30879).
* 기본 제공되는 스캐폴딩 RTE(리치 텍스트 편집기)가 예기치 않게 인라인 글꼴 크기를 요소에 적용합니다(NPR-31284).
* 사용자가 왼쪽 레일 필드에 초점을 맞추고 키보드 단축키를 사용하여 콘텐츠를 붙여넣으면 왼쪽 레일 필드에서 복사한 콘텐츠 대신 페이지 편집기 클립보드의 콘텐츠를 붙여넣습니다(NPR-31172).
* 사용자가 다중 필드에 파일 업로드 필드를 추가하면 이미지 경로가 다중 필드 노드 대신 구성 요소 노드에 저장됩니다(NPR-30882).
* The `ResponsiveGridExporter` API does not return `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` interface. The `com.day.cq.wcm.foundation.model.impl` package is declared as a private package (NPR-31398).

<!-- Review: NPR-31398 has fixVersion as 6530. However, it is mentioned twice in 6530 and 6520 as fixed. 
Remove one mention of this fix.
-->

* When a page containing some Experience Fragments is opened in non-editor mode (either in Author without the `editor.html` prefix and `wcmmode=disabled`, or in Publisher)., the request ends in HTTP status error code `500` (NPR-30743).
* 사용자는 암호를 변경하고 프로필 페이지에 액세스할 수 없습니다(NPR-31161).

### 검색 및 사용자 인터페이스 {#search-ui-interface}

* 카드 보기에서 검색 결과 페이지의 목록 보기로 전환할 때 페이지를 스크롤하기 전에 지연이 있습니다(NPR-31286).

* The [!UICONTROL Select All] checkbox is hidden in the list view on [!DNL Sites] user interface (NPR-31614).

* The [!UICONTROL Select All] count on a search result page is incorrect (NPR-31120).

* 메타데이터 편집기에 존재하지 않는 태그가 표시됩니다(NPR-31119).

### 번역 {#translation}

* 번역 작업에서 기한 옵션을 선택하면 두 개의 달력 팝업이 나타납니다(NPR-31270).

### 플랫폼 {#platform}

* 웹 콘솔의 Mime 유형 옵션이 작동하지 않습니다(NPR-31108).

* SSO(Single Sign-On)를 구성할 때 클라이언트 인증서가 허용되지 않습니다(NPR-31165).

* Jetty 기반 HTTP 서비스에 대한 버퍼 크기 구성의 업데이트가 저장되지 않습니다(NPR-30925).

* 이제 QueryBuilder는 xpath 쿼리에서 ``fn:name()`` orderby를 지원합니다(NPR-31322).

* [!DNL Experience Manager] 6.3에서 업그레이드 시 중복 활성화 트리가 만들어집니다(NPR-31513).

* 전달된 요청은 슬링 인증 동안 설정된 응답 헤더를 보존하지 않습니다(NPR-30013).

* 선택기 구성 요소 내에서 검색이 작동하지 않습니다(NPR-31692).

* 서로 다른 버전의 Apache POI 및 Apache Tika 번들로 인해 ZIP 파일을 [!DNL Experience Manager Communities] 게시물에 첨부할 때 오류가 표시됩니다(NPR-31018).

* 이 ``org.apache.sling.distribution.api`` 번들은 구성 관리자에 숨겨져 있으므로 사용자 지정 번들에는 사용할 수 없습니다(NPR-31720).

### 프로젝트 {#projects}

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

### 자산 {#assets}

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
* 텍스트 구성 요소의 RTE(Rich Text Editor) 플러그인은 일본어 및 한국어 텍스트에 대해 왜곡된 문자를 표시합니다(NPR-31331).
* 리치 텍스트 편집기(RTE)가 포함된 테이블을 목록 항목으로 삽입할 수 없습니다(NPR-30879).
* RTE(Rich Text Editor)가 기본 스캐폴딩인 인라인 글꼴 크기를 요소에 적용합니다. 예기치 않게(NPR-31284)
* 사용자가 왼쪽 레일 필드에 초점을 맞추고 키보드 단축키를 사용하여 컨텐츠를 붙여넣을 때 왼쪽 레일 필드에서 복사한 내용(NPR-31172) 대신 페이지 편집기 클립보드의 내용을 붙여넣습니다.
* 사용자가 다중 필드에 파일 업로드 필드를 추가하면 이미지 경로가 다중 필드 노드 대신 구성 요소 노드에 저장됩니다(NPR-30882).
* The `ResponsiveGridExporter` API does not return `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` interface. The `com.day.cq.wcm.foundation.model.impl` package is declared as private package (NPR-31398).
* When a page containing some Experience Fragments is opened in non-editor mode (either in Author without the `editor.html` prefix and `wcmmode=disabled`, or in Publisher), the request ends in HTTP status error code 500 (NPR-30743).

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

### 통합 {#integration}

* 사용자 지정 콘텐츠는 인스턴스를 다시 시작할 때까지 게시 인스턴스에 올바르게 표시되지 않습니다. NPR-30377: CQ-4273706용 핫픽스
* 웹 사이트에서 Launch를 구성할 때 라이브러리 주소에는 앞에 슬래시(/)가 추가되어 매번 수동으로 작업해야 합니다. NPR-30694: CQ-4275501용 핫픽스

### 양식 {#forms-6520}

>[!NOTE]
>
>[!DNL Experience Manager] 서비스 팩에는 [!DNL Experience Manager Forms] 수정 사항이 포함되어 있지 않습니다. 이러한 수정 사항은 별도의 [!DNL Forms] 추가 기능 패키지를 사용하여 전달됩니다. 또한, JEE의 [!DNL Experience Manager Forms]에 대한 수정 사항이 포함된 누적 설치 프로그램이 릴리스됩니다. 자세한 내용은 [Experience Manager Forms 추가 기능 설치](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) 및 [Experience Manager Forms JEE 설치 프로그램 설치](#forms-jee-installer)를 참조하십시오.

[!DNL Experience Manager] 6.5.2.0 Forms의 주요 기능은 다음과 같습니다.

* `RenderAtClient` Forms OSGi용 API의 `PDFFormRenderOptions`에 &#39;자동&#39; 설정이 추가되었습니다. [!DNL Experience Manager]

#### Forms 추가 기능 패키지 {#forms-add-on-package}

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

#### Forms JEE 설치 프로그램 {#forms-jee-installer}

**양식 - 문서 보안**

* 타임스탬프가 포함된 서명이 적용되지 않고 ALC-DSC-003-000: com.adobe.idp.dsc.DSCInvocationException: 호출 오류가 발생합니다. NPR-30820: CQ-4275852용 핫픽스

**양식 - 문서 서비스**

* SubmitURL에 앰퍼샌드(&amp;)가 포함된 경우 renderpdf 서블릿에 대한 POST 요청이 수행될 때 로그에 구문 분석 오류가 표시됩니다. NPR-30865: CQ-4278232용 핫픽스

**양식 - 기초 JEE**

* HTMLtoPDF 서비스가 JMX 콘솔에 maxReuseCount를 표시하지 않습니다. NPR-30134, NPR-30304: CQ-4273763용 핫픽스
* [!DNL Experience Manager Forms] Workbench에서 웹 서비스를 호출하여 웹 서비스 연결을 추가하거나 편집하면 ClassNotFoundException org.apache.axis.message.SOAPBodyElement 오류가 발생합니다. NPR-30105: CQ-4273217용 핫픽스

### 기능 팩이 포함됨 {#feature-packs-included}

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

* [!DNL Experience Manager Assets]에 대한 다중 사이트 관리자 지원이 활성화되었습니다. 자세한 내용은 [Experience Manager Assets에 MSM을 사용하여 자산 재사용](https://helpx.adobe.com/kr/experience-manager/6-5/help/assets/reuse-assets-using-msm.html)을 참조하십시오. NPR-29199: CQ-4259922용 핫픽스

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
