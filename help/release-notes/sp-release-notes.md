---
title: AEM 6.5 서비스 팩 릴리스 노트
description: Adobe Experience Manager 6.5 서비스 팩 4에 대한 릴리스 노트입니다.
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: a83def358e026b516add577f968dcc709357e458

---


# Adobe Experience Manager 6.5 서비스 팩 릴리스 노트 {#aem-service-pack-release-notes}

## 릴리스 정보 {#release-information}

| 제품 | **Adobe Experience Manager 6.5** |
|---|---|
| 버전 | 6.5.4.0 |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2020년 3월 05일 |
| 다운로드 URL | [PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.4.0), [Software Distribution(Beta)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.4.zip) |

## Adobe Experience Manager 6.5.4.0에 포함된 제품 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.4.0은 2019년 4월 6.5 릴리스의 공식 출시 이후 릴리스된 새로운 기능, 주요 고객의 요구 사항 개선 사항 및 성능, 안정성, 보안 개선 사항이 포함된 중요한 **업데이트입니다**. AEM(Adobe Experience Manager) 6.5 맨 위에 설치할 수 있습니다.

AEM 6.5.4.0에 도입된 몇 가지 주요 기능 및 개선 사항은 다음과 같습니다.

* 이제 AEM Assets는 Adobe I/O 콘솔을 통해 브랜드 포털로 구성됩니다.

* 이제 AEM [Forms 워크플로우에서](../forms/using/aem-forms-workflow-step-reference.md) 인쇄 가능한 출력 생성 단계를 사용할 수 있습니다.

* [적응형 양식 및 인터랙티브한 커뮤니케이션을 위한 레이아웃 모드에 대한 다중 열 지원](../forms/using/resize-using-layout-mode.md) .

* HTML5 [양식의 리치](../forms/using/designing-form-template.md) 텍스트 지원.

* [Adobe Experience Manager Assets의 접근성 향상](new-features-latest-service-pack.md#accessibility-enhancements) .

* 내장된 저장소(Apache Jackrabbit Oak)가 버전 1.10.8으로 업데이트되었습니다.

* 이제 선택적 컨텐츠 하위 트리를 Dynamic Media *- Scene7 모드로* 동기화할 수 있습니다(사용 가능한 모든 항목 `content/dam`).

* 이제 SOAP 웹 서비스와 양식 데이터 모델 통합을 통해 요소의 선택 그룹 또는 특성을 지원합니다.

* 이제 SOAP 입력 또는 출력 및 복잡한 데이터 구조가 동적 그룹 대체를 지원합니다.

이전 AEM 6.5 서비스 팩에 도입된 전체 기능, 주요 특징 및 주요 기능은 [Adobe Experience Manager 6.5 서비스 팩 4의 새로운 기능을 참조하십시오](new-features-latest-service-pack.md).

### 사이트 {#sites-fixes}

* AEM Sites 페이지의 URL에 콜론(:)이 포함되어 있는 경우) 또는 백분율 기호(%), 기본 브라우저 응답이 중지되고 CPU 사이클에 스파이크가 표시됩니다(NPR-32369, NPR-31918).

* AEM Sites 페이지를 열어 편집하고 구성 요소를 복사하면 일부 자리 표시자에 대해 붙여넣기 작업을 사용할 수 없습니다(NPR-32317).

* 게시 관리 마법사가 열리면 핵심 구성 요소에 연결된 경험 조각은 게시된 참조 목록에 표시되지 않습니다(NPR-32233).

* 터치 UI의 Live Copy 개요는 클래식 UI보다 렌더링하는 데 훨씬 오래 걸립니다(NPR-32149).

* 서버 시간 및 컴퓨터 시간이 다른 시간대에 있을 경우, 예약된 게시 시간은 Touch UI에 서버 시간을 표시하지만 클래식 UI에서는 시스템 시간이 표시됩니다(NPR-32077).

* AEM Sites에서 URL에 접미어가 붙은 페이지를 열지 못했습니다(NPR-32072).

* 사용자가 컨텐츠 조각을 편집할 때 삭제된 컨텐츠 조각 변형이 복원됩니다(NPR-32062).

* 사용자는 필수 필드에 정보를 제공하지 않고 컨텐츠 조각을 저장할 수 있습니다(NPR-31988).

* kernel.js 및 ui.js는 사전 준수되거나 캐시되지 않습니다. 이로 인해 페이지 렌더링 시간이 추가로 발생합니다(NPR-31891).

* PageEventAuditListener가 활성화되면 커밋 큐의 길이가 늘어납니다. 벌크 게시, 탐색, 벌크 자산 이동(NPR-31890)과 같은 많은 작업의 성능에 영향을 줍니다.

* 경험 조각을 드래그하면 높은 응답 시간이 관찰됩니다(NPR-31878).

* 응답형 그리드의 자리 표시자에서 구성 요소를 여기로 드래그하십시오 옵션을 선택하면 GET 요청이 전송되고 HTTP 403 오류(NPR-31845)가 발생합니다.

* 동일한 폴더 내에서 컨텐츠를 이동할 때 페이지 이동 옵션이 비활성화됩니다(NPR-31840).

* 편집 가능한 템플릿 구조 모드에서 레이아웃 컨테이너의 허용된 구성 요소 목록에 잘못된 결과가 표시됩니다. 디자인 대화 상자가 있는 구성 요소만 레이아웃 컨테이너에 표시됩니다(NPR-31816).

* 페이지에 사용자에 대한 읽기 전용 권한이 있으면 속성 열기 옵션이 sites.html에서는 볼 수 있지만 editor.html에서는 볼 수 없습니다(NPR-31770).

* 사용자가 [만들기] 단추를 클릭하면 페이지 옵션을 사용할 수 없습니다(NPR-31756).

* OOTB(즉시 사용 가능) 디자인 가져오기 구성 요소를 포함하는 Adobe 캠페인에서 캠페인을 동기화할 수 없습니다(NPR-31728).

* 글머리 기호 목록을 번호 매기기 목록으로 변경하려고 하면 목록의 처음 두 항목만 변경됩니다(NPR-31636).

* 페이지가 작성되지 않고 하위 노드가 선택되면 선택 대화 상자에 초기 노드가 표시됩니다. 페이지가 작성되고 사용자가 찾아보기를 클릭하면 페이지가 작성된 노드 대신 루트 노드로 리디렉션됩니다(NPR-31618).

* 받은 편지함 사용자 정의 워크플로 기능(NPR-32503 및 NPR-32492)에서 구성 보기 대화 상자가 제대로 작동하지 않습니다.

* 받은 편지함을 사용하여 워크플로우 정보를 보는 동안 오류 메시지가 표시됩니다(CQ-4282168).

### 자산 {#assets-6540-enhancements}

* 자산 수집 페이지에서 워크플로우를 트리거하는 단추가 비활성화되었습니다(NPR-32471).

* Dynamic Media Scene7 구성(NPR-32440)을 사용하여 Experience Manager에서 자산을 한 폴더에서 다른 폴더로 이동하는 동안 이름이 없는 폴더가 SPS(Scene7 Publishing System)에 생성됩니다.

* 게시된 자산이 들어 있는 폴더로 모든 자산을 이동시키는 작업이 오류(NPR-32366)로 인해 실패했습니다.

* ${extension}의 자산에 대한 변환 생성 실패(NPR-32294).

* 버전 내역 URL은 자산 속성 페이지의 참조자 필드(NPR 파섹-31889) 아래에 표시됩니다.

* DAM에서 다운로드한 ZIP 파일은 WinZip을 사용하여 열 수 없습니다(NPR-32293).

* 폴더 설정을 열어 폴더 제목이나 축소판 이미지를 변경한 다음 저장하면 폴더의 원래 권한이 업데이트됩니다(NPR-32292).

* 활성화가 예약된 달력 아이콘이 이후 날짜 및 시간(NPR-32291)으로 예약된 자산의 상태 열(DAM 자산 목록의 클래식 UI에 있음)에 표시되지 않습니다.

* 코드 조각 만들기 프로세스 동안 코드 조각 템플릿을 사용하여 코드 조각 만들기에 오류가 발생합니다(NPR-32290).

* 검색 필터에서 여러 태그를 선택하면 여러 검색 쿼리가 실행됩니다(NPR-32143).

* 파일 이름이 50자를 초과하는 에셋이 업로드되면 Experience Manager Assets UI에서 잘린 파일 이름이 표시됩니다(NPR-32054).

* Adobe Stock의 확인란 트리의 수준 2 확인란을 선택하면 필터 패널의 모든 확인란이 지워집니다(NPR-31919).

* Omnisearch 패싯을 사용한 파일 및 폴더 검색에서 예외가 발생합니다(NPR-31872).

* 종속성 규칙이 해당 메타데이터 스키마 양식(NPR-31834)으로 설정된 경우 메타데이터 편집기에서 필수 필드 선택을 위한 필드 강조 표시는 제거되지 않습니다.

* 태그 계층 구조에서 리프 수준 태그의 전체 이름이 자산 속성 페이지에 표시되지 않습니다(NPR-31820).

* Safari 브라우저의 자산 속성 페이지에서 뒤로 명령을 사용하면 오류가 발생합니다(NPR-31753).

* Omnisearch를 통해 수행한 터치 UI 검색 결과 페이지가 자동으로 스크롤되어 사용자의 스크롤 위치가 손실됩니다(NPR-31307).

* PDF 자산의 자산 세부 사항 페이지에는 Dynamic Media Scene7 실행 모드에서 실행되는 Experience Manager의 [컬렉션으로] 및 [변환 추가] 단추를 제외한 작업 단추가 표시되지 않습니다(CQ-4286705).

* Scene7의 일괄 업로드 프로세스를 통해 자산을 처리하는 데 시간이 너무 오래 걸립니다(CQ-4286445).

* 사용자가 Dynamic Media Client의 설정 편집기에서 변경하지 않은 경우 [저장] 단추가 [원격 세트]를 가져오지 않습니다(CQ-4285690).

* 지원되는 3D 모델을 AEM으로 인제스트할 때 3D 자산 축소판은 도움이 되지 않습니다(CQ-4283701).

* 스마트 자르기 비디오 뷰어 사전 설정이 처리되지 않은 상태로 배너 텍스트에 사전 설정 이름과 함께 두 번 나타납니다(CQ-4283517).

* 자산의 세부 정보 페이지에서 업로드된 3D 모델에서 미리 본 업로드된 3D 모델의 컨테이너 높이가 잘못 관찰되었습니다(CQ-4283309).

* Carousel Editor가 Experience Manager Dynamic Media Hybrid 모드의 IE 11에서 열리지 않습니다(CQ-425590).

* Chrome 및 Safari 브라우저에서 다운로드 대화 상자의 이메일 드롭다운에서 키보드 포커스가 멈춥니다(NPR-32067).

* AEM에서 DM 클라우드 구성을 추가하려는 동안 모든 콘텐츠 동기화 확인란이 기본적으로 활성화되어 있지 않습니다(CQ 파섹-4288533).

### 기본 UI {#foundation-ui-6540}

* 필터 패널을 사용하여 자산을 검색하는 동안 기존 필터 필드에 있지 않고 마우스 컨트롤을 이전 필터 필드로 이동합니다(NPR-32538).

* 플랫폼 태그 지정:태그 필드에 입력하여 태그를 검색하면 루트 경계 밖에 있는 태그가 표시되고 태그 필드의 `rootPath` 속성이 유지되지 않습니다(NPR-31895).

* 플랫폼 UI:텍스트 필드에 잘못된 경로가 추가되면 경로 브라우저가 닫힙니다(NPR-31884).

* 페이지 선택 시 고정 메뉴 뒤에 알림이 표시됩니다(NPR-31628).

### 플랫폼 {#platform-sling-6540}

* (HTL) 밑줄이 URL의 경로 섹션에서 색상을 바꿉니다(NPR-32231).

### 프로젝트 {#projects-6540}

* 사용자가 하위 폴더에 프로젝트를 만들 수 있는 권한이 있어도 만들기 단추가 표시되지 않습니다(NPR-31832).

### 프로젝트 번역 {#projects-translation-6540}

* 번역 프로젝트를 만들면 에서 공간 트리밍 옵션이 활성화되면 UI가 중단됩니다( `Apache Sling JSP Script Handler` NPR-32154).

* 변환할 태그가 번역 프로젝트에 추가될 때(NPR-31896) UI의 오류 및 오류 로그의 Null 점 예외가 관찰됩니다.

### 통합 {#integrations-6540}

* 시작 라이브러리 URL 생성은 Launch API의 `path` 및 `library_name` 값만 기반으로 하며 `library_path` 값을 기반으로 하지 않습니다(NPR-31550).

* LiveFyre 관련 항목을 처리하는 동안 오류 메시지가 표시됩니다(FYR-12420).

### WCM 템플릿 편집기 {#wcm-template-editor-6540}

* 편집 가능한 템플릿 구조 모드에서 레이아웃 컨테이너의 허용된 구성 요소 목록에 링크 단추 구성 요소가 표시되지 않습니다(CQ-4282099).

### WCM Page Editor {#wcm-page-editor-6540}

* 오버레이를 선택한 다음 응답형 그리드를 선택하는 경우 오류가 발생합니다. 구성 요소를 여기로 드래그하십시오(CQ-4283342).

### Campaign Targeting {#campaign-targeting-6540}

* Target 클라우드 구성이 실패하여 mbox 가져오기 요청이 실패했습니다(CQ-4279880).

### 브랜드 포털 {#assets-brand-portal}

* 브랜드 포털 사용자는 AEM 6.5.4에서 Adobe I/O로 업그레이드할 때 기여도 폴더 자산을 AEM 자산에 게시할 수 없습니다(CQDOC-15655).

   이 문제는 다음 서비스 팩 AEM 6.5.5에서 해결됩니다.

   AEM 6.5.4에 대한 즉각적인 수정 사항은 핫픽스를 [다운로드하고](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041) 작성자 인스턴스에 설치하는 것이 좋습니다.


* 메타데이터 스키마 드롭다운 값은 자산 속성에 표시되지 않습니다(CQ 파섹-4283287).

* 메타데이터 하위 스키마는 자산 속성의 MIMETYPE을 기준으로 탭을 표시하지 않습니다(CQ-4283288).

* 백엔드에서 스키마가 제거되더라도 메타데이터 스키마 게시 취소는 오류 메시지를 채웁니다.

* 게시된 자산에 대해 미리 보기 이미지가 표시되지 않습니다(CQ-4285886).

* 사용자가 이름에 작은 따옴표가 포함된 자산을 게시하거나 게시 취소할 수 없습니다(CQ-4272686).

* 여러 자산을 다운로드하는 동안 약관이 표시되지 않습니다(CQ-4281224).

* 사소한 보안 취약점이 해결되었습니다.

### 커뮤니티 {#communities}

* 멤버 만들기 양식이 빈 페이지로 표시됩니다(NPR-31997).

* 사용자가 작성자 인스턴스에서 Analytics 보고서를 볼 수 없습니다(NPR-30913).

### Oak- 인덱싱 및 쿼리 {#oak-indexing-6540}

* JPEG 이미지가 포함된 MS Word 및 MS Excel 문서, Tika 구문 분석기로 구문 분석하면 구문 분석되지 않고 클래스가 찾을 수 없음 오류가 발생합니다(NPR-31952).

### 양식 {#forms-6530}

>[!NOTE]
>
>AEM 서비스 팩에는 AEM Forms에 대한 수정 사항이 포함되어 있지 않습니다. 이러한 수정 사항은 별도의 Forms 추가 기능 패키지를 사용하여 전달됩니다. 또한, JEE의 AEM Forms에 대한 수정 사항이 포함된 누적 설치 프로그램이 릴리스됩니다. 자세한 내용은 [AEM Forms 추가 기능 설치](#install-aem-forms-add-on-package) 및 [AEM Forms JEE 설치](#install-aem-forms-jee-installer)를 참조하십시오.

* 통신 관리:게시물 프로세스 워크플로우에 제출하면 서신에 추가 문자가 표시됩니다(NPR-32626).

* 통신 관리:편지는 포스트 프로세스 워크플로우에 제출한 후 드롭다운 자리 표시자를 텍스트 구성 요소로 표시합니다(NPR-32539).

* 통신 관리:문자 템플릿에 정의된 기본값은 미리 보기 모드에서 표시되지 않습니다(NPR-32511).

* 모바일 양식:HTML 버전에서 XDP 양식을 렌더링하는 동안 제출 단추 크기가 확장되어 표시됩니다(NPR-32514).

* 문서 서비스:서비스 팩 2를 적용한 후 편지 및 일부 기타 페이지의 URL 액세스 문제(NPR-32508, NPR-32509).

* 문서 서비스:서버의 트랜잭션 수가 특정 제한을 초과하는 경우 HTML에서 PDF로의 변환이 실패하고 AEM Forms 서버(NPR-32204)에서 파일 유형 설정이 제거됩니다.

* 적응형 양식:WCAG2 레벨 AA 지침에 따라 브라우저 액세서빌러티 도구가 적응형 양식의 실패를 보고합니다(NPR-32312, NPR-32309, CQ-4285439).

* 적응형 양식:Chrome 브라우저 액세서빌러티 도구는 모범 사례 오류를 보고합니다(NPR-32310).

* 적응형 양식:AEM Sites 페이지에 포함된 적응형 양식을 구성하는 동안 번역 문제가 발생했습니다(NPR-32168).

* 워크벤치:PDF 유틸리티 서비스에 대해 PDF 속성 가져오기 작업을 사용하는 동안 오류 메시지가 표시됩니다(NPR-32150).

* Document Security:DisableGlobalOfflineSynchronizationData 옵션이 True(NPR-32078)로 설정되어 보호된 PDF 파일을 오프라인으로 열 수 없습니다.

* 디자이너:태그 지정 옵션을 활성화하면 생성된 PDF 출력(NPR-32547, NPR-31983, NPR-31950)에서 하위 양식 테두리가 사라집니다.

* 디자이너:표에 병합된 셀이 있는 경우 출력 서비스를 사용하여 XDP 양식에서 변환된 출력 PDF 파일에 대해 액세서빌러티 테스트가 실패합니다(CQ-4285372).

* Foundation JEE:AEM Forms 서버의 클러스터 연결이 끊어진 경우 캐싱 문제가 발생하여 서버가 서버에 다시 연결되지 않습니다(NPR-32412).

## Install 6.5.4.0 {#install}

**설치 요구 사항**

* AEM 6.5.4.0 requires AEM 6.5. Check [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* 서비스 팩은 Adobe Package Share에서 다운로드할 수 있고, Adobe Package Share는 AEM 6.5 인스턴스에서 직접 액세스할 수 있습니다.
* MongoDB 및 여러 인스턴스가 포함된 배포에서 패키지 관리자를 사용하여 작성자 인스턴스 중 하나에 AEM 6.5.4.0을 설치합니다.
* 서비스 팩을 설치하기 전에 AEM 인스턴스의 스냅샷 또는 새 백업이 있는지 확인하십시오.
* 설치하기 전에 인스턴스를 다시 시작합니다. 이 작업은 인스턴스가 여전히 업데이트 모드인 경우(및 인스턴스가 이전 버전에서 업데이트된 경우)에만 필요하지만 인스턴스가 오랫동안 실행 중인 경우 권장됩니다.

>[!CAUTION]
>
>AEM 6.5.4.0 패키지를 삭제하거나 제거하지 않는 것이 좋습니다.

### 패키지 공유를 통해 서비스 팩 설치 {#install-service-pack-via-package-share}

기존 AEM 6.5 인스턴스에 서비스 팩을 설치하려면 다음 단계를 수행하십시오.

1. Login to Package Share from within AEM or directly from your browser and download the [AEM 6.5.4.0 package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.4.0).

1. 패키지 관리자를 사용하여 다운로드한 패키지를 설치합니다.

>[!NOTE]
>
>**패키지 관리자 UI의 대화 상자가 6.5.4.0 설치 중에 종료되는 경우가 있습니다.**
>
>따라서 인스턴스에 액세스하기 전에 오류 로그가 안정화될 때까지 기다리는 것이 좋습니다. 사용자는 Updater 번들 제거와 관련된 특정 로그가 생성된 후에 설치가 성공적으로 수행되었는지 확인해야 합니다. 일반적으로 Safari에서 발생하지만, 브라우저에서는 간헐적으로 발생할 수 있습니다.

**자동 설치**

실행 중인 인스턴스에 AEM 6.5.4.0을 자동으로 설치하는 두 가지 방법이 있습니다.

A. 서버가 실행되는 동안 패키지를 ..*서버를 온라인으로 사용할 수 있는 동안 /crx-quickstart/install* 폴더. 패키지가 자동으로 설치됩니다.

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) - make sure that you use cmd=install&amp;recursive=true - so the nested packages  are  installed.

>[!NOTE]
>
>AEM 6.5.4.0은 부트스트랩 설치를 지원하지 않습니다.

**설치 확인**

1. 제품 정보 페이지(/system/console/ productinfo)에는 설치된 제품 `Adobe Experience Manager, Version 6.5.4.0` 아래에 업데이트된 버전 문자열이 표시됩니다.

1. All  OSGi  bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: /system/console/bundles).
1. OSGI 번들 org.apache.jackrabbit.oak-core는 버전 1.10.6 이상(웹 콘솔 사용:/system/console/bundles).

In order to see what platforms are certified to run with this release, please refer to the [Technical Requirements](/help/sites-deploying/technical-requirements.md).

### Install AEM Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>AEM Forms를 사용하지 않는 경우 건너뜁니다. AEM Forms의 수정 사항은 별도의 추가 기능 패키지를 통해 전달됩니다.

>[!NOTE]
>
>AEM 6.5.4.0 includes a new version of [AEM Forms Compatibility package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/AEM-FORMS-6.5.3.0-COMPAT). 이전 버전의 AEM Forms 호환성 패키지를 사용하고 AEM 6.5.4.0으로 업데이트하는 경우 최신 버전의 AEM Forms 호환성 패키지 설치 후 양식 추가 기능 패키지를 설치합니다.

1. AEM 서비스 팩을 설치했는지 확인합니다.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Install AEM Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE에서 AEM Forms를 사용하지 않는 경우 건너뜁니다. JEE의 AEM Forms에 있는 수정 사항은 별도의 설치 관리자를 통해 제공됩니다.

For information about installing the cumulative installer for AEM Forms on JEE and post-deployment configuration, see the [release notes for patch 0011](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0011.html).

#### Workbench 설치 프로그램

전체 설치 프로그램이므로 파일 크기는 패치 버전에 비해 큽니다. 새 Workbench 버전을 설치하기 전에 이전 Workbench 버전을 제거하십시오.

### UberJar {#uber-jar}

The UberJar for AEM 6.5.4.0 is available in the [Adobe Public Maven repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.4/).

To use UberJar in a Maven project, refer to the article, [How to use UberJar](/help/sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.4</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## 이제 사용되지 않는 기능 {#removed-deprecated-features}

이 섹션에는 AEM 6.5.4.0에서 더 이상 사용되지 않는 것으로 표시된 기능 및 기능이 나열됩니다.향후 릴리스에서 제거될 예정인 기능은 사용할 대체 옵션과 함께 먼저 더 이상 사용되지 않도록 설정됩니다.

고객은 현재 배포에서 해당 기능을 사용하는지 여부를 검토하고 대체 옵션을 사용하도록 구현을 변경할 계획을 수립하는 것이 좋습니다.

| 영역 | 기능 | 대체 |
|---|---|---|
| 통합 | The **[!UICONTROL AEM Cloud Services Opt-In]** screen has been deprecated. AEM 및 Target 통합이 AEM 6.5에서 업데이트되어 Adobe IMS 및 I/O를 통한 인증을 사용하는 Target Standard API와 분석 및 개인화를 위한 AEM 페이지를 구현하기 위한 Adobe Launch의 역할이 증가함에 따라, 옵트인 마법사는 기능적으로 사용할 수 없게 되었습니다. | 해당 AEM 클라우드 서비스를 통해 시스템 연결, Adobe IMS 인증 및 Adobe I/O 통합 구성 |

## 알려진 문제 {#known-issues}

* 연결된 **에셋 구성** 마법사가 설치 후 404 오류 메시지를 반환하는 경우 패키지 관리자를 사용하여 **cq-remotedam-client-ui-content** 및 **cq-remotedam-client-ui-components** 패키지를 수동으로 다시 설치합니다.
* AEM 6.5.x.x를 설치하는 동안 다음 오류 및 경고 메시지가 표시될 수 있습니다.
   * &quot;Target 표준 API(IMS 인증)를 사용하여 AEM에 Target 통합이 구성된 경우 환경 조각을 Target으로 내보내면 잘못된 오퍼 유형이 생성됩니다. &quot;경험 조각&quot;/소스 &quot;Adobe Experience Manager&quot; 유형 대신 Target은 &quot;HTML&quot;/소스 &quot;Adobe Target Classic&quot; 유형으로 여러 가지 오퍼를 작성합니다.
   * com.adobe.granite.maintenance.impl.TaskScheduler: granite/operations/maintenance에 유지 관리 창이 없습니다.
   * SUM, MAX 및 MIN과 같은 집계 함수를 사용하는 경우 적응형 양식 서버측 유효성 검사가 실패합니다. CQ-4274424
   * com.adobe.granite.maintenance.impl.TaskScheduler - granite/operations/maintenance에 유지 관리 창이 없습니다.
   * 쇼퍼블 배너 뷰어를 통해 자산을 미리 보는 동안 Dynamic Media 대화형 이미지의 핫스팟이 표시되지 않습니다.

## OSGi bundles and content packages included {#osgi-bundles-and-content-packages-included}

다음 텍스트 문서에는 AEM 6.5.4.0에 포함된 OSGi 번들 및 콘텐츠 패키지 목록이 나와 있습니다.

AEM 6.5.4.0에 포함된 OSGi 번들 목록

[파일 가져오기](assets/6540_bundles.txt)

AEM 6.5.4.0에 포함된 콘텐츠 패키지 목록

[파일 가져오기](assets/6540_packages.txt)

## Restricted sites {#restricted-sites}

다음 사이트는 고객만 사용할 수 있습니다. 액세스가 필요한 고객의 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [고객 지원](https://daycare.day.com/public/contact.html)문의 지원 포털에 액세스하는 방법에 대한 자세한 내용은 [지원 포털](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)액세스를 참조하십시오.

>[!MORE 좋아요]
>
>* [AEM 6.5 릴리스 노트](/help/release-notes/release-notes.md)
>* [AEM 제품 페이지](https://www.adobe.com/solutions/web-experience-management.html)
>* [AEM 6.5 설명서](https://helpx.adobe.com/support/experience-manager/6-5.html)
>* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

