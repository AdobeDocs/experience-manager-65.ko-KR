---
title: AEM 6.5 서비스 팩 릴리스 노트
description: Adobe Experience Manager 6.5 서비스 팩 4에 대한 릴리스 노트입니다.
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
mini-toc-levels: 1
translation-type: ht
source-git-commit: 9daad219d885c1c6972ace0b247f3537dcdc38a9

---


# Adobe Experience Manager 6.5 서비스 팩 릴리스 노트 {#aem-service-pack-release-notes}

## 릴리스 정보 {#release-information}

| 제품 | **Adobe Experience Manager 6.5** |
|---|---|
| 버전 | 6.5.4.0 |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2020년 3월 5일 |
| 다운로드 URL | [PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.4.0), [소프트웨어 배포(베타)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.4.zip) |

## Adobe Experience Manager 6.5.4.0에 포함된 제품 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.4.0은 **2019년 4월** 6.5 릴리스의 공식 출시 이후 릴리스된 새로운 기능, 주요 고객이 요청한 향상된 기능 및 성능, 안정성, 보안 개선 사항이 포함된 중요한 업데이트입니다. AEM(Adobe Experience Manager) 6.5 맨 위에 설치할 수 있습니다.

AEM 6.5.4.0에 도입된 몇 가지 주요 기능 및 개선 사항은 다음과 같습니다.

* 이제 AEM Assets은 Adobe I/O 콘솔을 통해 Brand Portal에 구성됩니다.

* 이제 AEM Forms 워크플로우에서 새로운 [인쇄 가능한 출력 생성](../forms/using/aem-forms-workflow-step-reference.md) 단계를 사용할 수 있습니다.

* 적용형 양식 및 대화형 커뮤니케이션용 레이아웃 모드에 대한 [다중 열을 지원](../forms/using/resize-using-layout-mode.md)합니다.

* HTML5 양식의 [리치 텍스트](../forms/using/designing-form-template.md)를 지원합니다.

* Experience Manager Assets의 [액세스 가능성이 개선](new-features-latest-service-pack.md#accessibility-enhancements)되었습니다.

* 내장된 저장소(Apache Jackrabbit Oak)가 버전 1.10.8으로 업데이트되었습니다.

* 이제 선택적 컨텐츠 하위 트리를 `content/dam`에서 사용하는 대신 *Dynamic Media - Scene7 모드*&#x200B;로 동기화할 수 있습니다.

* 이제 SOAP 웹 서비스와 양식 데이터 모델 통합을 통해 요소에 대한 선택 그룹 또는 속성을 지원합니다.

* 이제 SOAP 입력 또는 출력 및 복잡한 데이터 구조가 Dynamic Group 대체를 지원합니다.

이전 AEM 6.5 서비스 팩에 소개된 전체 기능, 주요 특징 및 주요 기능 목록에 대해서는 [Adobe Experience Manager 6.5 서비스 팩 4의 새로운 기능](new-features-latest-service-pack.md)을 참조하십시오.

### 사이트 {#sites-fixes}

* AEM Sites 페이지의 URL에 콜론(:) 또는 백분율 기호(%)가 포함되어 있는 경우 기본 브라우저가 응답을 중지하고 CPU 사이클에 스파이크가 표시됩니다(NPR-32369, NPR-31918).

* AEM Sites 페이지를 열어 편집하고 구성 요소를 복사하면 일부 자리 표시자에 대해 붙여넣기 작업을 사용할 수 없습니다(NPR-32317).

* 게시 관리 마법사가 열리면 코어 구성 요소에 연결된 경험 구성 요소가 게시된 참조 목록에 표시되지 않습니다(NPR-32233).

* Touch UI의 Live Copy 개요는 클래식 UI보다 렌더링하는 데 훨씬 시간이 오래 걸립니다(NPR-32149).

* 서버 시간과 컴퓨터 시간이 다른 시간대에 있는 경우 예약된 게시 시간은 Touch UI에 서버 시간을 표시하지만 클래식 UI에서는 시스템 시간이 표시됩니다(NPR-32077).

* AEM Sites에서 URL에 접미사가 붙은 페이지를 열지 못합니다(NPR-32072).

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

* 지원되는 3D 모델을 AEM으로 수집할 때 3D 자산 축소판이 도움이 되지 않습니다(CQ-4283701).

* 스마트 자르기 비디오 뷰어 사전 설정이 처리되지 않은 상태로 사전 설정 이름과 함께 배너 텍스트에 두 번 표시됩니다(CQ-4283517).

* 3D Viewer에서 업로드된 3D 모델을 미리 보기했을 때 모델의 잘못된 컨테이너 높이가 자산 세부 정보 페이지에서 확인되었습니다(CQ-4283309).

* 캐러셀 편집기가 Experience Manager Dynamic Media 하이브리드 모드로 IE 11에서 열리지 않습니다(CQ-425590).

* Chrome 및 Safari 브라우저에서 다운로드 대화 상자에 있는 이메일 드롭다운에서 키보드 포커스가 멈춥니다(NPR-32067).

* AEM에서 DM 클라우드 구성을 추가하는 동안 모든 컨텐츠 동기화 확인란이 기본적으로 활성화되지 않습니다(CQ 파섹-4288533).

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

### 브랜드 포털 {#assets-brand-portal}

* Brand Portal 사용자는 AEM 15655에서 Adobe I/O로 업그레이드할 때 기여도 폴더 자산을 AEM Assets에 게시할 수 없습니다(CQDOC-15655).

   이 문제는 다음 서비스 팩 AEM 6.5.5에서 수정됩니다.

   AEM 6.5.4를 즉시 수정하려면 [핫픽스를 다운로드](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041)하고 작성자 인스턴스에 설치하는 것이 좋습니다.


* 메타데이터 스키마 드롭다운 값은 자산 속성에 표시되지 않습니다(CQ 파섹-4283287).

* 자산 속성의 MIME 유형에 따라 메타데이터 하위 스키마에 탭이 표시되지 않습니다(CQ-4283288).

* 메타데이터 스키마 게시를 취소하면 백엔드에서 스키마가 제거되더라도 오류 메시지가 표시됩니다.

* 게시된 자산에 대한 미리 보기 이미지가 표시되지 않습니다(CQ-4285886).

* 사용자가 이름에 작은 따옴표가 포함된 자산을 게시하거나 게시를 취소할 수 없습니다(CQ-4272686).

* 여러 자산을 다운로드하는 동안 약관이 표시되지 않습니다(CQ-4281224).

* 사소한 보안 취약점이 해결되었습니다.

### 커뮤니티 {#communities}

* 구성원 만들기 양식이 빈 페이지로 표시됩니다(NPR-31997).

* 사용자가 작성자 인스턴스에서 Analytics 보고서를 볼 수 없습니다(NPR-30913).

### Oak 색인 지정 및 쿼리 {#oak-indexing-6540}

* JPEG 이미지가 포함된 MS Word 및 MS Excel 문서를 Tika 구문 분석기로 구문 분석하면 구문 분석되지 않고 클래스를 찾을 수 없다는 오류가 표시됩니다(NPR-31952).

### 양식 {#forms-6530}

>[!NOTE]
>
>AEM 서비스 팩에는 AEM Forms에 대한 수정 사항이 포함되어 있지 않습니다. 이러한 수정 사항은 별도의 Forms 추가 기능 패키지를 사용하여 전달됩니다. 또한, JEE의 AEM Forms에 대한 수정 사항이 포함된 누적 설치 프로그램이 릴리스됩니다. 자세한 내용은 [AEM Forms 추가 기능 설치](#install-aem-forms-add-on-package) 및 [AEM Forms JEE 설치](#install-aem-forms-jee-installer)를 참조하십시오.

* 서신 관리: 게시 처리 워크플로우에 제출하면 편지에 추가 문자가 표시됩니다(NPR-32626).

* 서신 관리: 게시 처리 워크플로우에 제출하면 편지에 드롭다운 자리 표시자가 텍스트 구성 요소로 표시됩니다(NPR-32539).

* 서신 관리: 편지 템플릿에 정의된 기본값이 미리 보기 모드에서 표시되지 않습니다(NPR-32511).

* 모바일 양식: HTML 버전에서 XDP 양식을 렌더링하는 동안 제출 버튼 크기가 확장되어 표시됩니다(NPR-32514).

* 문서 서비스: 서비스 팩 2를 적용한 후 편지 및 일부 기타 페이지의 URL에 액세스하는 데 문제가 발생합니다(NPR-32508, NPR-32509).

* 문서 서비스: 서버의 트랜잭션 수가 특정 제한을 초과하는 경우 HTML을 PDF로 변환할 수 없고 AEM Forms 서버에서 파일 유형 설정이 제거됩니다(NPR-32204).

* 적용형 양식: WCAG2 레벨 AA 지침에 따라 브라우저 접근성 도구가 적용형 양식의 오류를 보고합니다(NPR-32312, NPR-32309, CQ-4285439).

* 적용형 양식: Chrome 브라우저 접근성 도구가 모범 사례 오류를 보고합니다(NPR-32310).

* 적용형 양식: AEM Sites 페이지에 포함된 적용형 양식을 구성하는 동안 번역 문제가 발생했습니다(NPR-32168).

* Workbench: PDF 유틸리티 서비스에 PDF 속성 가져오기 작업을 사용하는 동안 오류 메시지가 표시됩니다(NPR-32150).

* 문서 보안: DisableGlobalOfflineSynchronizationData 옵션이 True로 설정되어 보호된 PDF 파일을 오프라인으로 열 수 없습니다(NPR-32078).

* 디자이너: 태그 지정 옵션이 활성화된 경우 생성된 PDF 출력에서 하위 양식 테두리가 사라집니다(NPR-32547, NPR-31983, NPR-31950).

* 디자이너: 표에 병합된 셀이 있는 경우 출력 서비스를 사용하여 XDP 양식에서 변환된 출력 PDF 파일에 접근성 테스트를 수행하면 오류가 발생합니다(CQ-4285372).

* Foundation JEE: 클러스터에서 AEM Forms 서버 연결이 끊어진 경우 캐싱 문제가 발생하여 서버에 다시 연결되지 않습니다(NPR-32412).

## 6.5.4.0 설치 {#install}

**설치 요구 사항**

* AEM 6.5.4.0을 사용하려면 AEM 6.5가 필요합니다. 세부 지침은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 확인합니다.
* 서비스 팩은 Adobe Package Share에서 다운로드할 수 있고, Adobe Package Share는 AEM 6.5 인스턴스에서 직접 액세스할 수 있습니다.
* MongoDB 및 여러 인스턴스가 포함된 배포에서 패키지 관리자를 사용하여 작성자 인스턴스 중 하나에 AEM 6.5.4.0을 설치합니다.
* 서비스 팩을 설치하기 전에 AEM 인스턴스의 스냅샷 또는 새 백업이 있는지 확인하십시오.
* 설치하기 전에 인스턴스를 다시 시작합니다. 이 작업은 인스턴스가 여전히 업데이트 모드인 경우(및 인스턴스가 이전 버전에서 업데이트된 경우)에만 필요하지만 인스턴스가 오랫동안 실행 중인 경우 권장됩니다.

>[!CAUTION]
>
>AEM 6.5.4.0 패키지를 삭제하거나 제거하지 않는 것이 좋습니다.

### 패키지 공유를 통해 서비스 팩 설치 {#install-service-pack-via-package-share}

기존 AEM 6.5 인스턴스에 서비스 팩을 설치하려면 다음 단계를 수행하십시오.

1. AEM 내에서 또는 브라우저 내에서 직접 패키지 공유에 로그인하여 [AEM 6.5.4.0 패키지](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.4.0)를 다운로드합니다.

1. 패키지 관리자를 사용하여 다운로드한 패키지를 설치합니다.

>[!NOTE]
>
>**패키지 관리자 UI의 대화 상자가 6.5.4.0 설치 중에 종료되는 경우가 있습니다.**
>
>따라서 인스턴스에 액세스하기 전에 오류 로그가 안정화될 때까지 기다리는 것이 좋습니다. 사용자는 Updater 번들 제거와 관련된 특정 로그가 생성된 후에 설치가 성공적으로 수행되었는지 확인해야 합니다. 일반적으로 Safari에서 발생하지만, 브라우저에서는 간헐적으로 발생할 수 있습니다.

**자동 설치**

실행 중인 인스턴스에 AEM 6.5.4.0을 자동으로 설치하는 두 가지 방법이 있습니다.

A. 서버가 실행되는 동안 패키지를 ..*/crx-quickstart/install* 폴더에 배치합니다. 패키지가 자동으로 설치됩니다.

B. [패키지 관리자에서 HTTP API](https://docs.adobe.com/content/docs/ko-KR/crx/2-3/how_to/package_manager.html)를 사용하여cmd=install&amp;recursive=true를 사용하는지 확인합니다. 이 경우 중첩된 패키지가 설치됩니다.

>[!NOTE]
>
>AEM 6.5.4.0은 부트스트랩 설치를 지원하지 않습니다.

**설치 확인**

1. 제품 정보 페이지(/system/console/ productinfo)에는 설치된 제품 아래에 업데이트된 버전 문자열 `Adobe Experience Manager, Version 6.5.4.0`이 표시됩니다.

1. 모든 OSGI 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]**&#x200B;이거나 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 콘솔 사용: /system/console/bundles).
1. OSGI 번들 org.apache.jackrabbit.oak-core는 버전 1.10.6 이상에 있습니다(웹 콘솔 사용: /system/console/bundles).

이 릴리스에서 실행하도록 인증된 플랫폼을 보려면 [기술 요구 사항](/help/sites-deploying/technical-requirements.md)을 참조하십시오.

### AEM Forms 추가 기능 패키지 설치 {#install-aem-forms-add-on-package}

>[!NOTE]
>
>AEM Forms를 사용하지 않는 경우 건너뜁니다. AEM Forms의 수정 사항은 별도의 추가 기능 패키지를 통해 전달됩니다.

>[!NOTE]
>
>AEM 6.5.4.0에는 [AEM Forms 호환성 패키지](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/AEM-FORMS-6.5.3.0-COMPAT)의 새 버전이 포함되어 있습니다. 이전 버전의 AEM Forms 호환성 패키지를 사용 중이고 AEM 6.5.4.0으로 업데이트하는 경우, Forms 추가 기능 패키지 설치 후 AEM Forms 호환성 패키지의 최신 버전을 설치합니다.

1. AEM 서비스 팩을 설치했는지 확인합니다.
1. 운영 체제에 대한 [AEM Forms 릴리스](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html)에 나열된 해당 양식 추가 기능 패키지를 다운로드합니다.
1. [AEM Forms 추가 기능 패키지 설치](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)에 설명된 대로 양식 추가 기능 패키지를 설치합니다.

### JEE에 AEM Forms 설치 {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE에서 AEM Forms를 사용하지 않는 경우 건너뜁니다. 별도의 설치 프로그램을 통해 JEE의 AEM Forms 수정 사항이 전달됩니다.

JEE의 AEM Forms용 누적 설치 프로그램 설치 및 배포 후 구성에 대한 자세한 내용은 [패치 0011에 대한 릴리스 노트](https://helpx.adobe.com/kr/aem-forms/quick-fixes/6-5/jee-patch-0011.html)를 참조하십시오.

#### Workbench 설치 프로그램

전체 설치 프로그램이므로 파일 크기는 패치 버전에 비해 큽니다. 새 Workbench 버전을 설치하기 전에 이전 Workbench 버전을 제거하십시오.

### UberJar {#uber-jar}

AEM 6.5.4.0용 UberJar는 [Adobe Public Maven 저장소](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.4/)에서 사용할 수 있습니다.

Maven 프로젝트에서 UberJar를 사용하려면 문서 [Uberjar 사용 방법](/help/sites-developing/ht-projects-maven.md)을 참조하여 프로젝트 POM에 다음 종속성을 포함하십시오.

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.4</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

**com.fasterxml.jackson.core.async** 패키지를 포함하는 업데이트된 6.5.4.0용 UberJar 버전은 [Adobe Public Maven 저장소](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.4-1.0/)에서 사용할 수 있습니다.

업데이트된 버전의 UberJar를 사용하는 경우 프로젝트 POM에 다음 종속성을 포함하십시오.

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version> 6.5.4-1.0</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## 이제 사용되지 않는 기능 {#removed-deprecated-features}

이 섹션에는 AEM 6.5.4.0에서 더 이상 사용되지 않는 것으로 표시된 기능이 나와 있습니다. 이후 릴리스에서 제거될 예정인 기능은 먼저 사용 중지로 설정되고 사용할 대체 옵션이 제공됩니다.

고객은 현재 배포에서 기능을 사용할지 검토하고 대체 옵션을 사용할 수 있도록 구현 변경을 계획하는 것이 좋습니다.

| 영역 | 기능 | 대체 |
|---|---|---|
| 통합 | **[!UICONTROL AEM 클라우드 서비스 옵트인]** 화면은 더 이상 사용되지 않습니다. AEM 6.5에서 Adobe IMS 및 I/O를 통해 인증을 사용하는 Target 표준 API를 지원하고 분석 및 개인 설정을 위해 AEM 페이지를 계측하는 Adobe Launch의 늘어나는 역할을 지원하도록 AEM 및 Target 통합이 업데이트되어 옵트인 마법사가 기능상 무관해졌습니다. | 해당 AEM 클라우드 서비스를 통해 시스템 연결, Adobe IMS 인증 및 Adobe I/O 통합 구성 |

## 알려진 문제 {#known-issues}

* **연결된 자산 구성** 마법사가 설치 후 404 오류 메시지를 반환하는 경우 패키지 관리자를 사용하여 **cq-remotedam-client-ui-content** 및 **cq-remotedam-client-ui-components** 패키지를 수동으로 다시 설치합니다.
* AEM 6.5.x.x를 설치하는 동안 다음 오류 및 경고 메시지가 표시될 수 있습니다.
   * Target 표준 API(IMS 인증)를 사용하여 AEM에 Target 통합이 구성된 경우 환경 조각을 Target으로 내보내면 잘못된 오퍼 유형이 생성됩니다. 경험 조각/소스 Adobe Experience Manager 유형 대신 Target은 HTML/소스 Adobe Target Classic 유형으로 여러 가지 오퍼를 작성합니다.
   * com.adobe.granite.maintenance.impl.TaskScheduler: granite/operations/maintenance에 유지 관리 창이 없습니다.
   * SUM, MAX 및 MIN과 같은 집계 함수를 사용하는 경우 적용형 양식 서버측 유효성 검사가 실패합니다. CQ-4274424
   * com.adobe.granite.maintenance.impl.TaskScheduler - granite/operations/maintenance에 유지 관리 창이 없습니다.
   * 쇼퍼블 배너 뷰어를 통해 자산을 미리 보는 동안 Dynamic Media 대화형 이미지의 핫스팟이 표시되지 않습니다.

## OSGi 번들 및 콘텐츠 패키지가 설치됨 {#osgi-bundles-and-content-packages-included}

다음 텍스트 문서에는 AEM 6.5.4.0에 포함된 OSGi 번들 및 콘텐츠 패키지 목록이 나와 있습니다.

AEM 6.5.4.0에 포함된 OSGi 번들 목록

[파일 가져오기](assets/6540_bundles.txt)

AEM 6.5.4.0에 포함된 콘텐츠 패키지 목록

[파일 가져오기](assets/6540_packages.txt)

## 제한된 사이트 {#restricted-sites}

다음 사이트는 고객만 사용할 수 있습니다. 액세스가 필요한 고객의 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [고객 지원에 문의하기](https://daycare.day.com/public/contact.html)
지원 포털에 액세스하는 방법에 대한 자세한 내용은 [지원 포털에 액세스](https://helpx.adobe.com/kr/experience-manager/kb/accessing-aem-support-portal.html)를 참조하십시오.

>[!MORE 좋아요]
>
>* [AEM 6.5 릴리스 노트](/help/release-notes/release-notes.md)
>* [AEM 제품 페이지](https://www.adobe.com/kr/solutions/web-experience-management.html)
>* [AEM 6.5 설명서](https://helpx.adobe.com/kr/support/experience-manager/6-5.html)
>* [Adobe 우선 순위 제품 업데이트](https://www.adobe.com/subscription/priority-product-update.html) 구독

