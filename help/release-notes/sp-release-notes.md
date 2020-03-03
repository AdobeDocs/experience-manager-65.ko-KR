---
title: AEM 6.5 서비스 팩 릴리스 노트
description: Adobe Experience Manager 6.5 서비스 팩 3에 대한 릴리스 노트입니다.
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
translation-type: tm+mt
source-git-commit: 9f4a460c7f64d86e35e950e512ed5b6cda1cbf2a

---


# Adobe Experience Manager 6.5 서비스 팩 릴리스 노트 {#aem-service-pack-release-notes}

## 릴리스 정보 {#release-information}

| 제품 | **Adobe Experience Manager 6.5** |
|---|---|
| 버전 | 6.5.3.0 |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2019년 12월 12일 |
| 다운로드 URL | [패키지 공유](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.3.0) |

## Adobe Experience Manager 6.5.3.0에 포함된 제품 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.3.0 is an important release that includes performance, stability, security, and key customer fixes and enhancements released since the general availability of 6.5 release in **April 2019**. AEM(Adobe Experience Manager) 6.5 맨 위에 설치할 수 있습니다.

이 서비스 팩 릴리스의 몇 가지 주요 사항은 다음과 같습니다.

* 내장된 저장소(Apache Jackrabbit Oak)가 버전 1.10.6로 업데이트되었습니다.

* Experience Manager Assets는 이제 Deflate 64 알고리즘을 사용하여 만든 ZIP 아카이브를 지원합니다.

* 정렬 가능한 작성된 날짜에 대한 새 열이 DAM 목록 보기 및 자산 검색 결과에 목록 보기에 추가되었습니다.

* 이름 열을 기반으로 한 자산 정렬이 목록 보기에서 활성화되었습니다.

* 이제 Dynamic Media에서 스마트 자르기 비디오 에셋을 지원합니다. 스마트 자르기는 장면의 초점을 따라 프레임을 이동하면서 비디오를 다시 자르는 기계 학습 중심 기능입니다.

* Dynamic Media는 스마트 이미징을 지원합니다.

* AEM 워크플로우에서 [부재 중](../forms/using/configure-out-of-office-settings.md) 환경 설정을 지정하는 기능

* AEM 워크플로우에서 다른 사용자와 받은 편지함 또는 받은 편지함 항목을 [](../forms/using/configure-shared-queues-osgi.md) 공유하는 기능

* 일괄 처리 모드에서 [인터랙티브한 커뮤니케이션을 생성할 수 있습니다](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

* ContextHub에 번들로 포함된 jQuery의 버전이 3.4.1로 업데이트되었습니다.

### 변경 사항 목록 {#list-of-changes}

#### 자산 {#assets-6530-enhancements}

**제품 개선 사항**

* Experience Manager Assets는 이제 Deflate 64 알고리즘을 사용하여 만든 ZIP 아카이브를 지원합니다(NPR-27573).

* 정렬 가능한 새로 만든 날짜에 대한 열이 목록 보기의 DAM 목록 보기 및 자산 검색 결과에 추가되었습니다(NPR-31312).

* 이름 열을 기반으로 한 자산 정렬이 목록 보기에서 허용되었습니다(NPR-31299).

* GLB, GLTF, OBJ 및 STL 자산 파일은 DAM의 자산 세부 정보 페이지에서 자산 미리 보기를 지원합니다(CQ 파섹-428277).

* ReplicationOnModifyListener 이벤트는 Dynamic Media에서 청크 업로드 중 청크 노드에 대해 트리거됩니다(CQ-4281279).

* 이제 Dynamic Media에서 스마트 자르기 비디오 에셋을 지원합니다. 스마트 자르기는 장면의 초점(CQ-4278995)을 따라 프레임을 이동하면서 비디오를 다시 자르도록 하는 머신 러닝 기반의 기능입니다.

* Dynamic Media는 스마트 이미징을 지원합니다(CQ-422249).

* 요청(NPR-31601)에서 쿼리 매개 변수가 전달되면 Foundation 선택기에서 검색/찾아보기 보기가 기본 보기로 설정되었습니다.

**수정 사항**

* 일부 PDF 문서의 메타데이터는 해당 제목을 수정할 때 업데이트되지 않고 PDF에 저장됩니다(NPR-31629).

* 이름에 더하기 &#39;+&#39; 문자가 있는 자산에 대해 에셋 공유가 작동하지 않습니다(NPR-31547).

* 기본 검색 양식 자산 관리 * 검색 레일의 편집이 예상대로 작동하지 않습니다(NPR-31502).

* 자산 보기에서 Omnisearch를 사용하여 자산 검색(NPR-31496)할 때 제안이 표시되지 않습니다.

* 다른 사용자가 동일한 자산을 다른 컬렉션에서 참조하는 경우, 컬렉션 내의 자산 참조는 참조된 자산을 다른 위치로 이동할 때 업데이트되지 않습니다(NPR-31486).

* 중복된 IPTC 태그가 자산 메타데이터에 추가됩니다(NPR-31328).

* 필터 레일에서 검색이 트리거될 때 오른쪽 상단 모서리의 검색 결과 카운트가 정확하게 업데이트되지 않습니다(NPR-31316).

* 파일 유형 필터에서 두 번째 수준 확인란을 선택 취소하면 모든 확인란이 선택 취소되고 검색 막대의 텍스트가 선택한/선택되지 않은 속성과 동기화되지 않습니다(NPR-31287).

* 모든 구성원(사용자/그룹)은 폴더의 멤버 섹션에서 제거할 수 없습니다.모든 사용자를 제거하려고 하면 로그인한 사용자가 목록에 추가됩니다(NPR-31171).

* 파일 이름에 더하기 &#39;+&#39; 기호가 있는 자산은 삭제할 수 없습니다(NPR-31162).

* 폴더 선택 시 상단 메뉴에 표시되는 만들기 드롭다운 메뉴는 만들기 옵션으로 &#39;폴더&#39;를 표시하지 않습니다(NPR-30877).

* Deny jcr:removeChildNodes 및 jcr:removeNode에 대한 ACL이 사용자에 대해 적용되면 폴더 선택 만들기 > 파일 업로드 작업 항목이 누락됩니다(NPR-30840).

* 특정 mp4 에셋이 업로드되면 DAM 워크플로우가 부실 상태로 전환되어 나머지 모든 워크플로우가 부실 상태로 전환됩니다(NPR-30662).

* 대용량 PDF 파일(몇 GB)이 DAM에 업로드되고 하위 자산이 처리되는 경우 메모리 부족 오류가 발생합니다(NPR-30614).

* 자산의 벌크 이동이 실패하고 경고 메시지가 표시됩니다(NPR-30610).

* Dynamic Media Scene 7 런타임 모드에서 실행 중인 AEM에서 자산을 한 폴더에서 다른 폴더로 이동할 때 자산 이름이 소문자로 변경됩니다(NPR-31630).

* 원격 이미지 집합을 편집하는 동안 Scene 7 회사 이름과 같은 폴더에 있는 이미지에 대한 오류가 발견되었습니다(NPR-31340).

* 참조가 포함된 Dynamic Media 에셋이 게시되지 않습니다(NPR-31180).

* AEM Dynamic Media - Scene 7 런타임 모드에서 Scene 7로의 업로드를 완료하는 데 너무 오래 걸립니다(NPR-31048).

* 이미지 자산에 추가된 핫스팟은 자산 세부 사항 페이지의 대화형 이미지 뷰어를 통해 표시되지 않습니다(NPR-30979).

* AEM Assets의 자산에 대해 수행된 작업이 Scene 7로 전달되면 대규모 스링 작업이 생성되고 처리 배너가 다시 나타납니다(NPR-30947).

* 자산 및 자산의 언어 사본을 만들 때 충돌이 발생합니다(NPR-30932).

* Dynamic Media Hybrid 모드에서 실행되는 AEM에서 다운로드한 동적 표현물은 끊겼습니다(이미지 컨텐츠 유형 대신 &#39;이미지를 찾을 수 없음&#39; 컨텐츠가 있는 텍스트 유형)(NPR-30876).

* Dynamic Media 인코딩 비디오 워크플로에서 Scene 7에서 Dynamic Media - Scene 7 실행 모드로 마이그레이션된 비디오의 축소판을 생성하지 못합니다(CQ-4282011).

* IpsApiException은 다른 Scene 7 회사 ID를 사용하여 한 인스턴스에서 다른 인스턴스로 자산을 마이그레이션하는 동안 관찰되었습니다(CQ-4280548).

* 지원되는 3D 모델을 AEM으로 인제스트할 때 3D 자산 축소판은 도움이 되지 않습니다(CQ-4283701).

* 3D 자산에 카메라 보기가 거의 없는 경우 스크롤 단추가 뷰어에 표시됩니다(CQ-4283322).

* 자산 세부 사항 페이지의 DimensionalViewer에서 미리 본 업로드된 3D 모델의 컨테이너 높이가 잘못되었습니다(CQ-4283309).

* Internet Explorer 11 및 Safari에서 SmartCropVideoViewer로 비디오를 재생할 수 없습니다(CQ-4281422).

* Dynamic Media - scene7 런타임 모드에서 실행되는 AEM에서 한 폴더에서 다른 폴더로 여러 자산을 이동할 때 이동 단추를 사용할 수 없습니다(CQ-4280384).

* MIME 유형이 MP4(CQ-4279704)가 아닌 경우 자산 세부 사항에서 왜곡된 비디오가 표시됩니다.

* 비디오 프로필이 있는 폴더에서 새로 인제스트된 비디오는 인코딩 비율이 100%로 완료된 후에도 처리 상태로 유지됩니다(CQ-4279389).

* 폴더에서 에셋을 이동하면 가장 이상 필요한 많은 sling 작업(Scene 7 API 호출)이 생성됩니다(CQ-4278664).

* 이미지 집합(또는 mediaset)을 만들고 DAM에서 적절한 이름 지정 규칙을 사용하여 이름을 지정하면 Scene 7에서 이미지 집합 이름이 소문자로 변경됩니다(CQ-428112).

* Scene 7 Migrator가 게시 상태를 잘못 설정합니다(CQ-4263492).

* Omnisearch를 통해 수행한 터치 UI 검색 결과 페이지는 자동으로 스크롤되어 컨텐츠 조각에서 사용자의 스크롤 위치를 잃게 됩니다(CQ-4282898).

* PDF 파일은 색인이 되어 있지 않고 내용 내부는 검색 가능하지 않습니다(CQ-4278916).

* &quot;사용자 선택기로 목록에 없는 그룹:[false]가 0과 같아야 함&quot;이 `principalName` 표시되고 `authorizableId` (CQ-4278177)가 닫힌 사용자 그룹을 추가할 때 관찰됩니다.

* 자산 UI 열 보기는 특정 테넌트의 dam 루트 경로에 관계없이 모든 경로를 표시합니다(CQ-4278175).

* 자산 선택기의 검색이 예상대로 작동하지 않습니다(CQ-4275886).

* 변환 워크플로우가 실패했습니다(CQ-4271928).

* DAM 이벤트 삭제 기능은 최신(maxSavedActivities) 이벤트 데이터를 삭제하고 이전에 만든 데이터를 저장합니다(NPR-31336).

* 터치 UI 검색(Omnisearch를 통해 수행) 결과 페이지가 자동으로 스크롤되어 사용자의 스크롤 위치가 손실됩니다(NPR-31307).

* 작업 표시줄 및 자산 수가 모두 선택한 다음 터치 UI에서 일부 항목(폴더/개별 자산)을 선택 해제할 때 업데이트되지 않습니다(NPR-31118).

* 자산에 대한 작업 세부 사항을 폴링하는 동안 AEM에 예외가 표시됩니다(CQ-4283569).

* DAM 파섹

#### 사이트 {#sites}

* LiveCopy 상속이 끊어지면 LiveCopy 페이지에 LiveCopy 링크(NPR-30980) 대신 언어 복사 링크가 표시됩니다.
* 새 블루프린트의 경우 레코드 수가 40개를 초과하는 경우 처음 40개의 레코드만 표시됩니다. 블루프린트는 나머지 레코드(NPR-31182)에 대한 빈 라인을 표시합니다.
* 사용자가 메뉴의 description 속성에 일본어 또는 한국어 문자를 추가하면 메뉴에 일본어 및 한국어 텍스트의 왜곡된 문자가 표시됩니다. (NPR-31331).
* RTE(Rich Text Editor)에서는 포함된 테이블을 목록 항목으로 삽입할 수 없습니다(NPR-30879).
* RTE(Rich Text Editor)를 스캐폴딩하는 즉시 사용 가능합니다. 예기치 않게 요소에 인라인 글꼴 크기를 적용합니다(NPR-31284).
* 사용자가 왼쪽 레일 필드에 초점을 맞추고 키보드 단축키를 사용하여 컨텐츠를 붙여넣으면 왼쪽 레일 필드에서 복사한 컨텐츠 대신 페이지 편집기 클립보드의 컨텐츠를 붙여넣습니다(NPR-31172).
* 사용자가 다중 필드에 파일 업로드 필드를 추가하면 이미지 경로가 다중 필드 노드(NPR-30882) 대신 구성 요소 노드에 저장됩니다.
* ResponsiveGridExporter API는 com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter 인터페이스를 반환하지 않습니다. com.day.cq.wcm.foundation.model.impl 패키지는 개인 패키지로 선언됩니다(NPR-31398).
* 일부 ExperienceFragments가 포함된 페이지가 비편집기 모드에서 열리면( `editor.html` 접두사와 접두사가 없는 작성자 `wcmmode=disabled`또는 게시자에서) HTTP 상태 오류 코드 500(NPR-30743)으로 요청이 끝납니다.
* 사용자는 암호를 변경하고 프로필 페이지에 액세스할 수 없습니다(NPR-31161).
* 사용자 데이터가 있는 JavaScript 파일은 서버측에서 생성됩니다(NPR-30822).
* AEM 제작 UI를 사용하면 외부 콘텐츠를 사용하여 피싱을 할 수 있습니다(NPR-29745).
* AEM 6.5 메타데이터 편집기의 표현식 언어 삽입 취약성(NPR-31017)

#### 검색 및 사용자 인터페이스 {#search-ui-interface}

* 검색 결과 페이지의 [카드] 보기에서 목록 보기로 전환하는 경우 페이지를 스크롤하기 전에 지연이 있습니다(NPR-31286).

* 사이트 UI의 목록 보기(NPR-31614)에서 모두 선택 확인란이 숨겨집니다.

* 검색 결과 페이지에서 모두 선택 카운트가 잘못되었습니다(NPR-31120).

* 메타데이터 편집기에는 존재하지 않는 태그가 표시됩니다(NPR-31119).

#### 번역 {#translation}

* 번역 작업에서 기한 옵션을 선택하면 두 개의 달력 팝업이 나타납니다(NPR-31270).

#### 플랫폼 {#platform}

* 웹 콘솔의 Mime 유형 옵션이 작동하지 않습니다(NPR-31108).

* 단일 사인온을 구성할 때 클라이언트 인증서가 허용되지 않습니다(NPR-31165).

* Jetty 기반 HTTP 서비스에 대한 버퍼 크기 구성의 업데이트가 저장되지 않습니다(NPR-30925).

* 이제 QueryBuilder는 xpath ``fn:name()`` 쿼리에서 orderby를 지원합니다(NPR-31322).

* AEM 6.3에서 업그레이드 시 복제 활성화 트리가 만들어집니다(NPR-31513).

* 전달된 요청은 슬링 인증 동안 설정된 응답 헤더를 보존하지 않습니다(NPR-30013).

* 피커 구성 요소 내에서 검색이 작동하지 않습니다(NPR-31692).

* 서로 다른 버전의 Apache POI 및 Apache Tika 번들(NPR-31018)으로 인해 ZIP 파일을 AEM Communities 게시물에 첨부할 때 오류가 표시됩니다.

* 이 ``org.apache.sling.distribution.api`` 번들은 구성 관리자에 숨겨져 있으므로 사용자 지정 번들(NPR-31720)에는 사용할 수 없습니다.

#### 프로젝트 {#projects}

* 달력 보기를 전환할 수 없습니다(NPR-31271).

#### 브랜드 포털 {#assets-brand-portal}

**제품 개선 사항**

* AEM 자산의 자산 소싱 가져오기 워크플로우가 브랜드 포털에서 AEM으로 새로 만든 자산만 가져오도록 수정되었으며, 복제를 방지하기 위해 NEW 폴더에 이미 존재하는 자산을 건너뜁니다(CQ 파섹-4278527).

**수정 사항**

* 자산 소싱 기능에서 새 기여도 폴더를 만들 때 잘못된 아이콘이 표시됩니다(CQ-4282825).
* 새 기여도 폴더를 만들 때 기여도 폴더(NEW 및 SHARED 파섹)에 하위 폴더 하나 또는 둘 다 나타나지 않습니다(CQ-4282424).
* 사용자가 브랜드 포털 끝의 기여도 폴더에서 새 자산을 받은 후 AEM에서 브랜드 포털로 기여도 폴더를 다시 게시하려고 하면 시스템에서 예외가 발생합니다(CQ-4279740).
* 기여도 폴더(중첩된 폴더) 내에 기여도 폴더를 만들면 복잡하지 않습니다(CQ-4278391).
* AEM 관리 콘솔에서 가져온 브랜드 포털 사용자 목록(.csv 파일)을 업로드할 때 예외가 발생합니다. .csv 파일의 이메일, FirstName 및 LastName 필드만 필수 필드입니다(CQ-4278390).

#### 커뮤니티 {#communities}

**수정 사항**

* 그룹 관리(그룹 열기/편집/게시/삭제)에 대한 빠른 링크는 커뮤니티 관리자(그룹 관리자/사이트 관리자)(NPR-31627)에게 표시되지 않습니다.
* 페이지를 수동으로 새로 고치거나 다시 로드하지 않는 한 제출된 블로그는 표시되지 않습니다(NPR-31599).
* &quot;언급&quot; 기능에 사용되는 JCR 쿼리는 대/소문자를 구분하며 결과를 반환하는데 너무 오래 걸립니다(NPR-31475).
* AEM 6.5 UberJar 파일에서 예외가 발생하고, AEM 6.5 UberJar 파일에서 `cq-social-translation` 번들이 누락되었습니다(NPR-31186).
* Jackson Databind 라이브러리가 새로운 취약점(NPR-30967)을 해결하기 위해 버전 2.9.9.3으로 업데이트되었습니다.
* 활동 및 알림 제목이 일치하지 않습니다(NPR-30941).
* 페이지 매김이 커뮤니티 블로그에서 제대로 작동하지 않습니다(NPR-30914).
* Analytics 보고서가 AEM 작성자 환경에서 채워지지 않으며 빈 페이지가 표시됩니다(NPR-30913).

#### Oak {#oak}

* 작성자 서버가 느려지는 Lucene 인덱스 업데이트(NPR-31548).

#### 양식 {#forms-6530}

>[!NOTE]
>
>AEM 서비스 팩에는 AEM Forms에 대한 수정 사항이 포함되어 있지 않습니다. 이러한 수정 사항은 별도의 Forms 추가 기능 패키지를 사용하여 전달됩니다. 또한, JEE의 AEM Forms에 대한 수정 사항이 포함된 누적 설치 프로그램이 릴리스됩니다. For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

##### Forms 추가 기능 패키지 {#forms-add-on-package-6530}

**적응형 양식**

* 적응형 양식을 현지화하는 동안 문자열에 사전 키가 포함됩니다(NPR-31110).

**대화형 통신**

* **MissingNode.toString()** 은 Jackson 라이브러리를 2.10.0으로 업그레이드한 후 부정확한 결과를 반환합니다(NPR-31549).

* 텍스트 편집기는 Microsoft Word에서 복사한 텍스트에서 공백 문자를 임의로 제거합니다(NPR-31113).

**서신 관리**

* LiveCycle ES4SP1에서 AEM 6.5(NPR-31615)로 문자를 마이그레이션하는 동안에는 캡션 및 도구 설명이 표시되지 않습니다.

* **문자를 초안으로 저장하는 동안 텍스트 흐름 형식이 더 이상 지원되지** 않습니다(NPR-30463).

**워크플로우**

* 100% CPU 사용률(NPR-31233)으로 인해 OSGi 워크플로우가 실패합니다.

**HTML5 양식**

* XDP 양식의 HTML5 미리 보기를 생성하면 하위 양식의 인스턴스를 추가하는 동안 깜박임이 표시됩니다(NPR-30909).

##### JEE 설치 관리자의 양식 {#forms-jee-installer-6530}

**양식 - 문서 서비스**

* .NET 프로젝트에서 MTOM을 사용하는 SOAP 웹 서비스에는 AssemblerServiceClient 호출 및 HtmlToPDF2 메서드(NPR-4281771)에 대한 예외가 표시됩니다.

**Foundation JEE**

* 작업 구성은 양식 호출 워크플로우 제출 작업(NPR-31478)에 대한 프로세스 이름을 로드하지 않습니다.
* JEE의 AEM Forms 사용자는 .lca 파일을 가져오거나 관리 콘솔에서 LDAP를 설정하는 동안 다음과 같은 오류가 발생합니다.

   `com.ibm.ws.webcontainer.filter.FilterInstanceWrapper doFilter SRVE8109W: Uncaught exception thrown by filter um: java.lang.NoClassDefFoundError: org/apache/commons/io/IOUtils at org.apache.commons.fileupload.util.Streams.copy`

   `Error 500: javax.servlet.ServletException: java.lang.NoClassDefFoundError: org.apache.commons.io.IOUtils` (NPR-30931)


### 기능 팩이 포함됨 {#feature-packs-included-6530}

>[!NOTE]
>
>AEM Forms 고객의 경우 AEM 서비스 팩, 누적 수정 팩 또는 기능 팩을 설치한 후 AEM Forms 추가 기능 패키지를 설치해야 합니다.

#### 양식 - 기초 JEE {#forms-foundation-jee-feature}

* Oracle 18c(NPR-29155)에 대한 AEM Forms 지원.

## Install 6.5.3.0 {#install}

**설치 요구 사항**

* AEM 6.5.3.0 requires AEM 6.5. Check [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* 서비스 팩은 Adobe Package Share에서 다운로드할 수 있고, Adobe Package Share는 AEM 6.5 인스턴스에서 직접 액세스할 수 있습니다.
* MongoDB 및 여러 인스턴스가 포함된 배포에서 패키지 관리자를 사용하여 작성자 인스턴스 중 하나에 AEM 6.5.3.0을 설치합니다.
* 서비스 팩을 설치하기 전에 AEM 인스턴스의 스냅샷 또는 새 백업이 있는지 확인하십시오.
* 설치하기 전에 인스턴스를 다시 시작합니다. 이 작업은 인스턴스가 여전히 업데이트 모드인 경우(및 인스턴스가 이전 버전에서 업데이트된 경우)에만 필요하지만 인스턴스가 오랫동안 실행 중인 경우 권장됩니다.

>[!CAUTION]
>
>AEM 6.5.3.0 패키지를 삭제하거나 제거하지 않는 것이 좋습니다.

### 패키지 공유를 통해 서비스 팩 설치 {#install-service-pack-via-package-share}

기존 AEM 6.5 인스턴스에 서비스 팩을 설치하려면 다음 단계를 수행하십시오.

1. Login to Package Share from within AEM or directly from your browser and download the [AEM 6.5.3.0 package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.3.0).

1. 패키지 관리자를 사용하여 다운로드한 패키지를 설치합니다.

>[!NOTE]
>
>**패키지 관리자 UI의 대화 상자가 6.5.3.0 설치 중에 종료되는 경우가 있습니다.**
>
>따라서 인스턴스에 액세스하기 전에 오류 로그가 안정화될 때까지 기다리는 것이 좋습니다. 사용자는 Updater 번들 제거와 관련된 특정 로그가 생성된 후에 설치가 성공적으로 수행되었는지 확인해야 합니다. 일반적으로 Safari에서 발생하지만, 브라우저에서는 간헐적으로 발생할 수 있습니다.

**자동 설치**

실행 중인 인스턴스에 AEM 6.5.3.0을 자동으로 설치하는 두 가지 방법이 있습니다.

A. 서버가 실행되는 동안 패키지를 ..*서버를 온라인으로 사용할 수 있는 동안 /crx-quickstart/install* 폴더. 패키지가 자동으로 설치됩니다.

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) - make sure that you use cmd=install&amp;recursive=true - so the nested packages  are  installed.

>[!NOTE]
>
>AEM 6.5.3.0은 부트스트랩 설치를 지원하지 않습니다.

**설치 확인**

1. 제품 정보 페이지(/system/console/ productinfo)에는 설치된 제품 `Adobe Experience Manager, Version 6.5.3.0` 아래에 업데이트된 버전 문자열이 표시됩니다.

1. All  OSGi  bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: /system/console/bundles).
1. OSGI 번들 org.apache.jackrabbit.oak-core는 버전 1.10.6 이상(웹 콘솔 사용:/system/console/bundles).

In order to see what platforms are certified to run with this release, please refer to the [Technical Requirements](/help/sites-deploying/technical-requirements.md).

### Install AEM Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>AEM Forms를 사용하지 않는 경우 건너뜁니다. AEM Forms의 수정 사항은 별도의 추가 기능 패키지를 통해 전달됩니다.

>[!NOTE]
>
>AEM 6.5.3.0 includes a new version of [AEM Forms Compatibility package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/AEM-FORMS-6.5.3.0-COMPAT). 이전 버전의 AEM Forms 호환성 패키지를 사용하고 AEM 6.5.3.0으로 업데이트하는 경우 최신 버전의 AEM Forms 호환성 패키지 설치 후 양식 추가 기능 패키지를 설치합니다.

1. AEM 서비스 팩을 설치했는지 확인합니다.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Install AEM Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE에서 AEM Forms를 사용하지 않는 경우 건너뜁니다. JEE의 AEM Forms에 있는 수정 사항은 별도의 설치 관리자를 통해 제공됩니다.

For information about installing the cumulative installer for AEM Forms on JEE and post-deployment configuration, see the [release notes for patch 0007](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0007.html).

#### Workbench 설치 프로그램

전체 설치 프로그램이므로 파일 크기는 패치 버전에 비해 큽니다. 새 Workbench 버전을 설치하기 전에 이전 Workbench 버전을 제거하십시오.

## UberJar {#uber-jar}

The UberJar for AEM 6.5.3.0 is available in the [Adobe Public Maven repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.3/).

To use UberJar in a Maven project, refer to the article, [How to use UberJar](/help/sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.3.0</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## 더 이상 사용되지 않는 기능 {#removed-deprecated-features}

이 섹션에는 AEM 6.5.3.0에서 더 이상 사용되지 않는 것으로 표시된 기능 및 기능이 나열됩니다.향후 릴리스에서 제거될 예정인 기능은 사용할 대체 옵션과 함께 먼저 더 이상 사용되지 않도록 설정됩니다.

고객은 현재 배포에서 해당 기능을 사용하는지 여부를 검토하고 대체 옵션을 사용하도록 구현을 변경할 계획을 수립하는 것이 좋습니다.

| 영역 | 기능 | 대체 |
|---|---|---|
| 통합 | The **[!UICONTROL AEM Cloud Services Opt-In]** screen has been deprecated. AEM 및 Target 통합이 AEM 6.5에서 업데이트되어 Adobe IMS 및 I/O를 통한 인증을 사용하는 Target Standard API와 분석 및 개인화를 위한 AEM 페이지를 구현하기 위한 Adobe Launch의 역할이 증가함에 따라, 옵트인 마법사는 기능적으로 사용할 수 없게 되었습니다. | 해당 AEM 클라우드 서비스를 통해 시스템 연결, Adobe IMS 인증 및 Adobe I/O 통합 구성 |

## 알려진 문제 {#known-issues}

* AEM **6.5.3.0을 설치한 후 연결된 자산 구성** 마법사가 404 오류 메시지를 반환하는 경우, 패키지 관리자를 사용하여 **cq-remotedam-client-ui-content** 및 **cq-remotedam-client-ui-components** 패키지를 수동으로 다시 설치합니다.
* AEM 6.5.x.x를 설치하는 동안 다음 오류 및 경고 메시지가 표시될 수 있습니다.
   * &quot;Target 표준 API(IMS 인증)를 사용하여 AEM에 Target 통합이 구성된 경우 환경 조각을 Target으로 내보내면 잘못된 오퍼 유형이 생성됩니다. &quot;경험 조각&quot;/소스 &quot;Adobe Experience Manager&quot; 유형 대신 Target은 &quot;HTML&quot;/소스 &quot;Adobe Target Classic&quot; 유형으로 여러 가지 오퍼를 작성합니다.
   * com.adobe.granite.maintenance.impl.TaskScheduler: granite/operations/maintenance에 유지 관리 창이 없습니다.
   * SUM, MAX 및 MIN과 같은 집계 함수를 사용하는 경우 적응형 양식 서버측 유효성 검사가 실패합니다. CQ-4274424
   * com.adobe.granite.maintenance.impl.TaskScheduler - granite/operations/maintenance에 유지 관리 창이 없습니다.
   * 쇼퍼블 배너 뷰어를 통해 자산을 미리 보는 동안 Dynamic Media 대화형 이미지의 핫스팟이 표시되지 않습니다.

## OSGi 번들 및 콘텐츠 패키지가 설치됨 {#osgi-bundles-and-content-packages-included}

다음 텍스트 문서에는 AEM 6.5.3.0에 포함된 OSGi 번들 및 콘텐츠 패키지 목록이 나와 있습니다.

AEM 6.5.3.0에 포함된 OSGi 번들 목록

[파일 가져오기](assets/6530_bundles.txt)

AEM 6.5.3.0에 포함된 컨텐츠 패키지 목록

[파일 가져오기](assets/sp_6530_packages.txt)

## Helpful Resources {#helpful-resources}

* [AEM 6.5 릴리스 노트](/help/release-notes/release-notes.md)
* [AEM 제품 페이지](https://www.adobe.com/marketing/experience-manager.html)
* [AEM 6.5 설명서](https://helpx.adobe.com/support/experience-manager/6-5.html)
* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

## 제한된 사이트 {#restricted-sites}

다음 사이트는 고객만 사용할 수 있습니다. 액세스가 필요한 고객의 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [고객 지원](https://daycare.day.com/public/contact.html)문의 지원 포털에 액세스하는 방법에 대한 자세한 내용은 [지원 포털](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)액세스를 참조하십시오.
