---
title: AEM 6.5 서비스 팩 릴리스 노트
description: Adobe Experience Manager 6.5 서비스 팩 5에 대한 릴리스 노트입니다.
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: d51577195e969ff8af31be49159ff575e3654cc9
workflow-type: tm+mt
source-wordcount: '4476'
ht-degree: 23%

---


# Adobe Experience Manager 6.5 서비스 팩 릴리스 노트 {#aem-service-pack-release-notes}

## 릴리스 정보 {#release-information}

| 제품 | **Adobe Experience Manager 6.5** |
|---|---|
| 버전 | 6.5.5.0 |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2020년 6월 4일 |
| 다운로드 URL | [패키지 공유](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.5.0), [소프트웨어 배포 ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip) |

## Adobe Experience Manager 6.5.5.0에 포함된 제품 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.5.0은 **2019년 4월** 6.5 릴리스의 공식 출시 이후 릴리스된 새로운 기능, 주요 고객이 요청한 향상된 기능 및 성능, 안정성, 보안 개선 사항이 포함된 중요한 업데이트입니다. AEM(Adobe Experience Manager) 6.5 맨 위에 설치할 수 있습니다.

AEM 6.5.5.0에 도입된 몇 가지 주요 기능 및 개선 사항은 다음과 같습니다.

* AEM 받은 편지함에 표시되는 열 이름 사용자 지정

* 페이지 편집기, 핵심 구성 요소, RTE 및 관리 사용자 인터페이스와 같은 AEM Web Content Management(WCM)의 다양한 영역에서 액세스 가능성 개선

* Interactive Communication을 초안으로 저장

* JEE에서 AEM Forms [!DNL Oracle WebLogic 12] 에 대한 지원.

* 이제 자산 사용자 인터페이스 흐름에서 예외 처리가 [!DNL Adobe Experience Manager] 개선되었습니다.

* Dynamic Media Scene7에 대한 게시 URL을 가져오기 위해 `getRemoteAssetPublishURL` `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` 인터페이스에 새 메서드가 추가되었습니다.

* [WCAG](#assets-6550-changes) (Web Content Accessibility Guidelines)를 준수하는 에셋의 액세서빌러티 개선 [!DNL Adobe Experience Manager] 사항.

* Adobe Experience Manager와 패키지 공유 통합 제거

* 내장된 저장소(Apache Jackrabbit Oak)가 버전 1.22.3으로 업데이트되었습니다.

For complete list of features, key highlights, key features introduced in AEM 6.5 service pack 5, see [What&#39;s new in Adobe Experience Manager 6.5 Service Pack 5](new-features-latest-service-pack.md) .

다음은 [!DNL Experience Manager] 6.5.5.0 릴리스에서 제공되는 수정 사항 목록입니다.

### 사이트 {#sites-6550}

* AEM Sites는 해당 별칭에서 페이지를 게시 또는 게시 취소하는 옵션을 제공합니다. 옵션이 작동하지 않습니다(NPR-33415).
* 여러 템플릿이 들어 있는 템플릿에서 레이아웃 컨테이너를 삭제하면 템플릿이 올바르게 렌더링되지 않습니다(NPR-33347).
* AEM Sites 페이지가 여러 Live-Copy가 있는 큰 컨텐츠 세트의 일부인 경우 페이지 버전 내역 미리 보기가 로드되지 않습니다(NPR-33311).
* 이동 명령을 사용하여 AEM Sites 페이지의 이름을 변경해도 페이지 제목이 업데이트되지 않습니다(NPR-33264).
* 열 보기를 통해 페이지를 이동하면 열이 사라집니다(NPR-33216).
* 언어 복사본에 있는 로컬 구성 요소의 이름이 블루프린트에서 구성 요소의 이름과 동일하고 구성 요소가 블루프린트에서 롤아웃되면 _msm_moved 용어가 로컬 구성 요소의 이름에 추가되지 않습니다(NPR-33208).
* 페이지 리디렉션 서블릿은 ResourceType이 cq:Page(NPR-33176)가 아닌 AEM Sites URL에 .html을 추가합니다.
* 하위 트리를 붙여넣을 때 해당 하위 페이지를 붙여넣을 것인지 여부를 결정하는 옵션이 없습니다(NPR-33149).
* 구성 요소의 라이브 사용 결과 수는 49번으로 제한됩니다(NPR-33058).
* 스키마에 컨텐츠 조각을 기반으로 하고 필수 텍스트 영역 또는 경로 필드를 포함하는 경우 컨텐츠 조각을 저장할 수 없습니다(NPR-33007).
* 즉시 사용 가능한 경험 조각 구성 요소를 사용하여 사용자 지정 구성 요소를 만들고 AEM Sites 페이지에서 사용하는 경우, AEM은 사용자 지정 구성 요소의 참조(사용)를 표시하지 않습니다(NPR-32852).
* 많은 수의 참조가 있는 폴더의 이름을 바꾸면 해당 폴더에 대한 많은 참조가 업데이트되지 않습니다(NPR-32765).
* 소스 편집 옵션을 활성화하면 인라인 전체 화면 옵션에는 사용할 수 있지만 리치 텍스트 편집기의 편집 대화 상자와 전체 화면 옵션에는 없는 상태로 유지됩니다(NPR-32763).
* 다중 필드가 있고 블루프린트의 페이지 속성에 필수 필드(예: 드롭다운 또는 경로 필드)가 포함되어 있는 경우, 이러한 다중 필드가 포함된 페이지가 롤아웃되면 Live Copy의 페이지 속성이 저장되지 않습니다. (NPR-32751)
* 화면 판독기는 머리글 구조를 사용하여 페이지를 탐색할 수 없습니다. 또한 구성 요소 탭에 잘못된 레이블이 있습니다(NPR-32648).
* 페이지 지정이 시작되면 경험 조각 선택기가 일부 항목을 로드하지 않습니다(NPR-32605).
* Live Copy를 읽고, 수정하고, 만들고, 삭제할 수 있는 작성자 권한이 취소됩니다. 각 작성자는 블루프린트 내에서 페이지를 이동할 수 있는 읽기 및 수정 권한을 명시적으로 제공해야 했습니다(NPR-32550).
* 컨텐츠 작성자가 Adobe Analytics(NPR-32548)와 통합된 페이지에 대해 론치를 만들지 못했습니다.
* 사용자가 동기화와 함께 상속을 다시 시작할 때 상위 페이지의 Live Copy는 블루프린트와 동기화하지 않고 잘못된 상태(NPR-32500)를 표시합니다.
* AEM Sites 편집기 페이지를 로드하는 데 15초 이상 걸립니다(NPR-32413).
* 특정 필드에는 상속 취소 옵션이 표시되지 않습니다(NPR-32362).
* 경험 조각 구성 요소의 경로를 선택하고 선택 대화 상자 열기 확인란을 선택하면 경로 브라우저에서 선택한 경로로 이동하지 않습니다(NPR-32308).
* AEM 6.2에서 AEM 6.5로 업그레이드하는 경우 정적 템플릿의 Parsys 구성 요소가 올바르게 표시되지 않습니다. Parsys 구성 요소의 높이는 0으로 설정되며 구성 요소 내의 구성 요소는 보이지 않습니다. (NPR-33663).
* 사용자가 동일한 페이지에서 레이아웃 컨테이너를 복사하고 붙여넣을 때 레이아웃 컨테이너의 구성 요소는 표시되지 않습니다(NPR-33648).
* 발송자 상태 확인은 로그 파일에 `Invalid cookie header` 경고 메시지를 표시합니다(NPR-33629).

### 자산 {#assets-6550-changes}

Experience Manager Assets의 **액세스 가능성이 개선되었습니다**

* 이제 에셋의 타임라인 패널에서 새 버전 [!UICONTROL 만들기] (NPR-33424)를 사용하여 [!UICONTROL 버전] 주석 [!UICONTROL 을 만드는] 데 키보드 [!UICONTROL 초점을 주석] 목록 및 클릭 가능한 옵션을 사용할 수있습니다(NPR-33424).

* 이제 키보드 키를 사용하여 [설정 [!UICONTROL 보기] ] 대화 상자에서 에셋에 대한 [설정  보기] 옵션에 도달하고 설정을 변경할 수 있습니다(NPR-33420).

* 이제 콤보 상자의 목록 상자 드롭다운(여러 페이지의 여러 필드)에 항목이 화면 판독기에서 알릴 수 있는 옵션 목록으로 표시됩니다(NPR-33516).

* 이제 정렬 가능한 머리글(목록 보기, [!UICONTROL 타임라인] 보기 및 [!UICONTROL 게시] 관리 페이지)의 정렬 기능이 화면 판독기로 발표되고 열 머리글의 정렬 컨트롤은 키보드를 사용하여 액세스할 수 있습니다(NPR-32979).

* 이제 클릭 가능한 요소(예: 주석 카드, 버전 업데이트, 콤보 상자, 메뉴 V자 아이콘)는 키보드를 사용하여 포커스를 지정하고 작업을 수행할 수 있습니다(NPR-33514).

* 이제 인사이트 보기의 인사이트 아이콘(사용, 노출 및 클릭)의 기능(또는 작업 목적)이 [!UICONTROL 화면 판독기] (NPR-33513)에 의해 올바르게 표시됩니다.

* 이제 키보드(NPR-33493, CQ-4273031)를 사용하여 읽기 전용 양식 필드(예: 자산 [!UICONTROL 속성의] 기본 탭 [!UICONTROL 에서]비활성화된 필드)에 포커스를 둘 수 있습니다.

* 다양한 입력 필드의 레이블은 이제 텍스트 입력 시 사라졌던 자리 표시자 레이블만이 아니라 영구 레이블입니다(NPR-33475).

* 이제 화면 판독기 사용자에게 서로 다른 수준의 머리글로 인식되는 페이지 제목 및 섹션 머리글 수준(예:)이 다르게 인식됩니다(NPR-33471).

* 이제 키보드(NPR-33468, CQ-4271412)를 사용하여 링크 및 옵션(자산 페이지의 머리글과 확대/축소 옵션, 폴더 탐색)과 같은 대화형 사용자 인터페이스 요소에 액세스할 수 있습니다.

* 이제 [!UICONTROL 발행물]관리 페이지의 옵션 [!UICONTROL ,]범위 [!UICONTROL 및] 워크플로우 [!UICONTROL 진행률 표시기가 탭 대신] 진행률 표시기로 화면 판독기에서 올바르게 읽힐 수 있습니다(NPR-33416).

* 별점 등급 아이콘(자산 [!UICONTROL 속성] 또는 카드 보기에서 [!UICONTROL 고급] 탭 [!UICONTROL 의 등급] 섹션에서)의 색상이 변경되어 시력이 제한된 사용자와 색상 인식 없이 적절한 대비를 할 수 있습니다(NPR-33414).

* 이제 키보드 키(NPR-3397)를 사용하여 자산 세부 정보 페이지의 [!UICONTROL 댓글] 필드 옆에 있는 Chevron 위쪽 화살표를 액세스할 수 있습니다.

* 자산 속성 [!UICONTROL 및 왼쪽 레일 탐색]  (자산 사용자 인터페이스에서)에 대한 태그 대화 상자의 확장 및 축소 상태가 화면 판독기(NPR-3396)에 의해 올바르게 표시됩니다.

* 이제 자산에 있는 모든 검색 [!DNL Adobe Experience Manager] 페이지의 제목이 고유합니다(NPR-33343).

* 트리 구조를 탐색하는 동안 트리 보기 컨트롤의 다양한 요소가 화면 판독기에 의해 올바르게 표시됩니다(NPR-33304).

* 이제 키보드 키(NPR-33283)를 사용하여 [!UICONTROL 타임라인] 보기에서 자산 세부 사항 페이지에 있는 다른 버전의 에셋에 액세스할 수 있습니다.

* 이제 Omnisearch 콤보 상자에 나타나는 검색 제안 이름이 검색 기능을 사용하는 동안 화면 판독기에 의해 발표됩니다(NPR-33280).

* 클릭 가능한 요소 및 [!UICONTROL 참조 레일에] 연결 [!UICONTROL 으로 이동] 기능이 이제 클릭 가능한 요소(NPR-33278)로 화면 판독기에 의해 발표됩니다.

* 대화 상자가 열리면 [링크 [!UICONTROL 공유] ] 대화 상자의 표 구조 정보(예: 행 1, 셀 1, 표)가 더 이상 화면 판독기에서 표시되지 않습니다(NPR-33268).

* 이제 다양한 콤보 상자 요소의 목적(예: 자산 속성의 기본 탭에서 선택 대화 상자를 여는 옵션 및 경로)이 화면 판독기(NPR-33235)에 의해 올바르게 표시됩니다.

* 목록 보기 테이블의 행을 선택할 수 있다는 정보는 키보드 포커스가 스크린 리더 사용자에게 전달됩니다. 이 정보는 마우스가 행에서 마우스로 가리키면 발표됩니다(NPR-33234).

* 옵션( [!UICONTROL x][!UICONTROL ) - Properties의] Basic [!UICONTROL 탭] 에서 Tags [!UICONTROL 필드 아래에 선택한 각 태그를 제거하는 옵션(] x포함)이 이제 화면 판독기(NPR-33206)에 액세스할 수 있습니다.

* 이제 화면 판독기 사용자와 시력이 있는 키보드 사용자(NPR-33200)가 달력 날짜 선택기를 사용하여 포커스를 설정하고 실행 가능하게 합니다.

* 이제 목록 보기와 카드 보기 간 전환 시 화면 판독기(보기 조정)에 기능이 올바르게 표시됩니다(NPR-33069).

* 이제 왼쪽 레일의 메뉴에 액세스할 수 있습니다. 메뉴를 확장하는 기능과 목적은 화면 판독기(NPR-33068)에 의해 적절히 발표됩니다.

* 화면 판독기 사용자가 목록 상자 및 기타 여러 사용자 인터페이스 요소에 액세스할 수 있으며 이러한 요소에 대한 다음 정보가 화면 판독기(NPR-33040)에 의해 발표됩니다.

   * 양식을 제출하기 전에 요소에 사용자 입력이 필요한지 여부
   * 요소를 편집할 수 없는지 여부.
   * 위젯을 선택했는지 여부

* 이제 키보드를 사용하여 필터 사이드바를 여는 옵션을 이용할 수 있습니다(NPR-32842, CQ-4273018).

* 이제 목록 보기의 열 헤더의 확인란 컨트롤에 액세스할 수 있으며 이 컨트롤을 사용하는 목적이 화면 판독기(NPR-32722, NPR-33005)에 의해 발표됩니다.

* 달력 날짜 선택기의 시간(HH) 및 분(mm) 필드에 대한 레이블은 이제 자리 표시자 레이블 대신 영구 레이블로, 사용자가 이러한 필드에 텍스트를 입력할 때 사라지지 않습니다(NPR-32720).

* 이제 벨 아이콘을 클릭한 후 표시되는 알림의 링크 텍스트가 화면 판독기 사용자에게 알려지며, 화면 판독기 사용자는 탭을 사용하여 각 링크에 액세스할 수 있습니다(NPR-32645).

* [!UICONTROL 선택], [!UICONTROL 다운로드], [!UICONTROL 속성]및 [!UICONTROL 더 많은 작업] 옵션을  선택할 수 있습니다.

* 화면 판독기에서 키보드를 사용하여 액세스할 때 시각적으로 숨겨진 내용(검색 결과의 헤더 메뉴 막대 컨텐츠 등)이 더 이상 표시되지 않습니다(NPR-32606).

* 이제 일정 날짜 선택기에서 다음 달 및 이전 달로 이동할 컨트롤에 대한 레이블의 용도를 화면 판독기로 발표했습니다(NPR-32604).

* 이제 스타 등급 아이콘은 키보드 키(NPR-32513)를 사용하여 포커스가 설정되고 실행 가능합니다.

* 이제 탭(볼륨 슬라이더에 주력) 및 화살표 키(볼륨 조정)를 통해 비디오 볼륨을 제어하는 기능을 이용할 수 있습니다(NPR-32065).

* 파일 크기 필터의 하한([!UICONTROL 부터]) 및 상한([!UICONTROL 끝]) 입력 필드의 용도가 비시안형 스크린 리더 사용자(NPR-32064)에게 발표됩니다.

* 이제 [!UICONTROL 만들기] 및 번역 [!UICONTROL 양식의 언어] 메뉴를 검색 모드에서 화면 판독기(CQ-4293906)가 액세스할 수 있습니다.

* 이제 [!UICONTROL 참조] 패널에 액세스할 수 있는 기능은 다음과 같습니다(NPR-33261, CQ-4293798).

   * 검색 모드에서 화면 판독기 포커스는 더 이상 [ [!UICONTROL 사이트 참조]], [ [!UICONTROL 자산 참조]], [ [!UICONTROL 복사본]] 및 [양식 참조] 섹션 아래의 숨겨진 다중 선 편집 필드로 이동하지  않습니다.

   * 이제 화면 판독기가 사이트 참조 및 [!UICONTROL 언어 복사] 요소의 역할을 [!UICONTROL 발표합니다] .

   * 검색 모드에서 화면 판독기의 초점은 의미 있는 시퀀스에서 다양한 요소로 이동합니다.

* [!UICONTROL 메타데이터 스키마 편집기] 페이지 및 해당 요소는 이제 키보드를 사용하여 액세스할 수 있으며 화면 판독기에 적합합니다(CQ-4290962, CQ-4272953).

* 현재 선택한 태그를 제거하는 옵션의 [!UICONTROL x] 아이콘 용도와 선택한 태그 수도 함께 표시됩니다(CQ-4273017).

* 화면 판독기를 사용하는 비시인의 사용자에게 혼동을 방지하기 위해 이제 장식 아이콘 및 이미지가 화면 판독기에서 무시됩니다(CQ-4272944).

**Experience Manager Assets에서 해결된 문제**

[!DNL Adobe Experience Manager] 6.5.5.0 자산은 다음 문제에 대한 수정 사항을 제공합니다.

* [!UICONTROL 컬렉션의 에셋에] 대한 워크플로우  만들기 대화 상자에서 시작 옵션을 사용할 수 없으므로 워크플로우가 트리거되지 않습니다(NPR-32471).

* 메타데이터 스키마에서 계단식 드롭다운을 사용하는 동안, 하위 드롭다운에서 아포스트로피가 포함된 드롭다운 옵션을 선택 및 저장할 때, 선택한 아포스트로피 옵션이 자산 속성 [!UICONTROL 을] 다시 열고 사라집니다(NPR-32649).

* [!UICONTROL 자산 통찰력 동기화] 작업이 다음 항목으로 이동하는 대신 잘못된 항목(Analytics 쪽)이 나타나면 중지되고 실패합니다(NPR-32674).

* 파노라마 뷰어의 모바일 브라우저에서 기본적으로 모션 센서가 비활성화되므로 Gyroscope가 작동하지 않습니다(CQ-4272937).

* [!UICONTROL 6.5.1에 6.5.3 설치(NPR-32730)를 할 때 연결된 에셋 구성] 마법사가 404 오류로 작동하지 않습니다.

* XMP 원본에 쓰기 프로세스 동안 모든 사용자 지정 네임스페이스 메타데이터 속성은 구성된 네임스페이스 접두어(NPR-32748)와 반대로 사용자 지정 네임스페이스 접두어를 ns2로 변경합니다.

* 지연 로드는 트리거되지 않으며 알림 받은 편지함에서 작업을 검토하도록 선택할 때 100개의 자산만 표시됩니다(NPR-32750).

* `NullPointerException` 는 새로 생성된 사용자 프로필(SAML/SSO)에서 노드 기본 설정이 누락되어 관찰되었습니다. 이 오류로 인해 새로 로그인한 사용자가 [!DNL Adobe Experience Manager Stock] 통합을 사용할 수 없습니다(NPR-32777).

* 10,000개 이상의 에셋이 포함된 스마트 컬렉션을 열 때 트래픽 경고가 로그에 관찰됩니다(NPR-32980).

* Asset names are changed to lowercase when moving assets from one folder to another in [!DNL Adobe Experience Manager] working on Dynamic Media Scene7 runmode (NPR-32995).

* 검색 결과에서 해당 속성으로 이동한 다음 검색 결과로 돌아가 삭제한 후 검색된 자산을 삭제할 수 없습니다(NPR-32998).

* [!UICONTROL 다음] 옵션은 자산 이동 [!UICONTROL 인터페이스에서 대상 폴더를 선택할 때 비활성화되어] 있습니다(NPR-33356).

* [!UICONTROL 다음] 옵션은 상위 노드(단일 하위 폴더가 표시되는 경우)를 선택한 다음 하위 폴더를 선택할 때 활성화되지 않습니다(NPR-33275).

* AAL(Adobe Asset Link)에서 AAL(체크 인 및 체크 아웃)은 삭제 권한이 있는 사용자에게 읽기, 만들기 또는 수정과 같은 다른 권한이 허용된다고 해도 비활성화됩니다(NPR-33272).

* 스마트 자르기 변환은 자산 다운로드 대화 상자에서 사용할 수 없습니다(NPR-33167).

* 스마트 자르기 프로필이 있는 폴더 아래의 PDF에 대한 변환 레일을 열 때 로그에 예외가 관찰됩니다(CQ-4294201).

* Dynamic Media Scene7 실행 모드의 AEM에서 기본적으로 [!UICONTROL 다이내믹 미디어 동기화 모드를] 비활성화한 경우 이미지 사전 설정은 게시되지 않습니다(CQ-4294200).

* 벌크 업로드가 중단되는 동안 에셋 처리가 중단되고 워크플로우 인스턴스에 DAM 업데이트 에셋의 고정 인스턴스가 표시됩니다(CQ-4293916).

* AEM에서 다이내믹 미디어 구성을 만드는 것은 작동하지만 사용자 인터페이스에서 저장을 선택하면 아무 일도 일어나지 않습니다(CQ-4292442).

* Safari/Mac에서 f4v 비디오 에셋 미리 보기가 점진적 재생에서 작동하지 않습니다(CQ-4289844).

* 상위 폴더 안에 있는 이름의 점 `.` 문자가 포함된 자산을 스마트 자르기에 추가 폴더가 만들어집니다(CQ-4289337).

* 축소판이 깨지고 비디오가 복사되면 비디오 처리 배너가 표시되지 않습니다(CQ-4284125).

* 빈 카메라 뷰가 있는 일부 모델의 경우 Firefox에서 차원 뷰어가 빈 축소판을 잘못 표시합니다(CQ-4283447).

* 6.5.5.0에서 해결된 성능 문제는 다음과 같습니다(CQ-4279206).

   * 큰 바이너리를 Dynamic Media 이미지 처리 서버로 업로드하는 데 시간이 너무 오래 걸립니다.

   * Dynamic Media Scene7 아키텍처로 인해 AEM에서 축소판 생성 시간이 증가합니다.

* 자산 수가 많은 고객의 경우 다이내믹 미디어 Scene7 마이그레이션 문제가 발생합니다(CQ-4279206).

* 비디오 360 뷰어의 레이아웃 `setVideo` 을 사용하는 경우 끊어지고 비디오가 사용 시 아래로 이동합니다( `video= modifier` CQ-4263201).

* AEM SDL 패키지(NPR-33175)를 설치하는 동안 오류 메시지가 표시됩니다.

### 플랫폼 {#platform-6550}

* 맵 항목 [!DNL Sling] 이 (NPR-33362)에서 만들어진 경우 `sling:match` 필터가 호출되지 `/etc/maps` 않습니다.
* 세그먼트 문제로 인해 AEM이 [!DNL Apache Lucene] 충돌합니다(NPR-32988).
* [!DNL Jackson] 코어 패키지가 AEM uber jar 파일에 없습니다(NPR-32848).
* CRXDE Lite는 노드의 속성에 대한 읽기 권한이 없는 사용자에 대한 컨텐츠를 `jcr:primaryType` 로드하지 않습니다(NPR-32611).
* [!DNL Granite] 유지 관리 작업 스케줄러는 AEM 배포 시 너무 자주 다시 초기화됩니다(CQ-4294627).
* 예를 들어 7시간 동안 SQL 쿼리가 더 오래 실행되면 AEM이 응답을 중지합니다(NPR-33044).

### 사용자 인터페이스 {#ui-6550}

* 다중 필드에서 라디오 단추 선택이 지속되지 않습니다(NPR-3309).
* 목록 보기(NPR-33124)에서 레이지 로드 제한이 작동하지 않습니다.
* 일치하는 항목이 없으면 Omnisearch 결과 페이지에 메시지가 표시되지 않습니다(NPR-32974).
* Omnisearch 필터는 선택한 위치를 무시하고 있는 노드 아래에 `/content` 있는 모든 일치 항목을 반환합니다(NPR-32849).

### 통합 {#integrations-6550}

* Adobe Target 구성 요소가 있는 페이지가 게시되면 내부 캐시가 지워집니다(NPR-33162).
* Adobe Target과의 통합이 [!DNL Windows Internet Explorer] 11에서 작동하지 않습니다(NPR-3311).
* Adobe Target을 구성할 때 [!UICONTROL 회사] 및 [!UICONTROL 보고서 세트] 필드가 보고 소스 선택 시 나타나지 않습니다(NPR-32502).
* Adobe I/O를 사용하여 경험 조각을 내보낼 때 소스 제품과 같은 메타데이터는 Adobe Target으로 내보내지지 않습니다(NPR-32159).
* 로컬 AEM 관리 그룹의 승인된 IMS 사용자는 IMS 구성을 만들거나 수정할 수 없습니다(NPR-33045).
* Adobe Launch 구성 페이지에 모든 레코드가 표시되지 않습니다(NPR-33011).
* 컨텐츠 작성자 그룹의 사용자는 JavaScript 오류(NPR-32996)로 인해 Adobe Target 구성 요소의 속성을 편집할 수 없습니다.

### 번역 프로젝트 {#translation-6550}

* 번역된 태그는 타사 번역 서비스에서 AEM으로 가져올 수 없습니다(NPR-33154).
* 번역 구성 페이지에는 변환에 사용한 것과 다른 잘못된 번역 공급자가 표시됩니다(NPR-32971).
* 기존 번역 프로젝트에 경험 조각 폴더를 추가하면 새 프로젝트가 만들어집니다(NPR-32843).
* 번역 작업 실행 시 로그에 오류가 `NullPointerException` 표시됩니다(NPR-32628).

### WCM {#wcm-6550}

* 페이지 편집기 - [!DNL Sites] 페이지 편집기는 키보드 전용 사용자가 머리글에서 사용할 수 있는 모든 옵션을 통해 탭 포커스를 이동하는 대신 기본 컨텐츠로 건너뛸 수 있도록 허용하지 않습니다(CQ-4293883).
* 페이지 편집기 - 잘 구성 요소를 사용하고 저장된 데이터를 포함하는 패널은 [!DNL Chrome] 및 [!DNL Firefox] 버전 업데이트(CQ-4292995)로 인해 표시되지 않습니다.
* MSM - 페이지에서 구성 요소를 삭제해도 페이지의 게시된 버전에서 구성 요소가 삭제되지 않습니다(CQ-4292360).

### 브랜드 포털 {#assets-brand-portal-6550}

* 게시된 메타데이터 스키마를 제거하면 오류가 [!DNL Brand Portal] 발생합니다(CQ-4292063).
* 관리자가 Adobe 개발자 콘솔을 통해 브랜드 포털로 [!DNL Experience Manager Assets] 6.5.4를 구성하는 경우 [!DNL Brand Portal] 사용자는 기여도 폴더의 자산을 에서 까지 게시할 수 [!DNL Brand Portal] 없습니다 [!DNL Experience Manager]. (NPR-33046).
* 충돌을 일으키는 상위 폴더의 복제 복제(NPR-33001).

### 커뮤니티 {#communities-6550}

* 빠른 편집 메뉴 옵션을 사용하여 중재 콘솔에서 카드를 삭제할 수 없습니다(NPR-33117).
* 활동 스트림 [!UICONTROL 페이지] 액세스 시 오류가 발생합니다(NPR-33146).
* 작성자 인스턴스에서 삭제된 그룹은 일부 게시 인스턴스에서 제거되지 않습니다(NPR-33199).
* 작성자는 새 그룹을 만든 후 [!UICONTROL 11일(NPR-33205)에 있는] 커뮤니티 그룹 [!DNL Internet Explorer] 섹션으로 리디렉션되지 않습니다.
* AEM 받은 편지함에서 메시지에 액세스해도 메시지의 상태가 읽음으로 변경되지 않습니다(NPR-32764).
* 그룹을 편집하고 축소판 이미지를 변경해도 그룹 축소판 이미지가 업데이트되지 않습니다(NPR-32599). [!DNL Communities]
* 사용자가 커뮤니티의 다른 사용자에게 이메일을 보낼 수 없습니다(NPR-32598).
* 사용자가 페이지를 새로 고칠 때까지 제출된 블로그는 표시되지 않습니다(NPR-32391).
* UGC(사용자 생성 콘텐츠)의 알림 및 구독 버전을 만드는 동안 소스 페이지의 잘못된 ID가 저장됩니다(CQ-4279355, CQ-4289703).

### 워크플로우 {#workflow-6550}

* 왼쪽 레일의 [!UICONTROL 타임라인] 옵션을 로드하는 데 예상보다 시간이 더 걸립니다(NPR-32851).
* AEM 인스턴스를 다시 시작한 후 컬렉션에 대한 검토 작업에 대한 이메일에 잘못된 페이로드 링크(NPR-32774)가 포함되어 있습니다.

### 양식 {#forms-6550}

>[!NOTE]
>
>AEM 서비스 팩에는 AEM Forms에 대한 수정 사항이 포함되어 있지 않습니다. 이러한 수정 사항은 별도의 Forms 추가 기능 패키지를 사용하여 전달됩니다. 또한, JEE의 AEM Forms에 대한 수정 사항이 포함된 누적 설치 프로그램이 릴리스됩니다. 자세한 내용은 [AEM Forms 추가 기능 설치](#install-aem-forms-add-on-package) 및 [AEM Forms JEE 설치](#install-aem-forms-jee-installer)를 참조하십시오.

* 통신 관리: 대상 영역의 자산 순서는 편지를 제출한 후 섞입니다(NPR-33359, NPR-33153).
* 적응형 양식: 사용자가 적응형 양식을 편집할 때 [!UICONTROL 페이지 정보] 메뉴에서 사용할 수 있는 워크플로우  시작 옵션이 작동하지 않습니다(NPR-33004).
* 적응형 양식: 사용자가 둘 이상의 첨부 파일로 응용 양식을 저장할 수 없습니다(NPR-32997).
* 적응형 양식: 적응형 양식의 패널 레이아웃을 변경하면 오류가 발생합니다(CQ-4293880).
* 적응형 양식: 적응형 양식 사전의 문자열에 새 줄이 있으면 사전에 `&#xa;` 문자가 추가됩니다(NPR-33266).
* 적응형 양식 접근성: 사용자가 적응형 양식을 HTML 양식으로 미리 볼 때 [!UICONTROL 문지르기 서명] 필드는 탭 초점을 유지할 수 없습니다(NPR-33159).
* 적응형 양식 접근성: 응용 양식 제출 시 표시되는 오류 메시지는 `aria-describedBy` 속성에 연결되지 않습니다(NPR-33071).
* 적응형 양식 접근성: 적응형 양식의 필수로 표시된 필드에는 ARIA 액세서빌러티 스키마의 필수 속성이 True로 설정되어 있지 않습니다(NPR-33070).
* PDFG 서비스: 사용자가 텍스트 파일을 PDF로 변환하면 일본어 문자가 올바르게 렌더링되지 않습니다(NPR-33238).
* PDFG 서비스: `CreatePDF` PDF 파일을 PDF OCR 포맷으로 변환하지 못했습니다(NPR-32994).
* PDFG 서비스: 문서의 200번째 인스턴스에 대해 PDF를 변환할 수 없습니다(NPR-32766). [!DNL OpenOffice]
* 백엔드 통합: 잘못된 비활성 상태(NPR-33169)로 인해 새로 고침 토큰이 만료되면 양식 데이터 모델 요청이 실패합니다.
* 디자이너: 화면 판독기는 XDP 파일에 정의된 사용자 지정 탭 순서 대신 기본 지리적 순서를 기반으로 탭 순서를 실행합니다(NPR-32160).
* 디자이너: 태그 지정 옵션을 활성화하면 생성된 PDF 출력(NPR-32778)에서 하위 폼 테두리가 사라집니다.

## 6.5.5.0 설치 {#install}

**설치 요구 사항**

* AEM 6.5.5.0을 사용하려면 AEM 6.5가 필요합니다. 세부 지침은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 확인합니다.
* 서비스 팩은 Adobe Package Share에서 다운로드할 수 있고, Adobe Package Share는 AEM 6.5 인스턴스에서 직접 액세스할 수 있습니다.
* MongoDB 및 여러 인스턴스가 포함된 배포에서 패키지 관리자를 사용하여 작성자 인스턴스 중 하나에 AEM 6.5.5.0을 설치합니다.
* 설치하기 전에 AEM 인스턴스의 스냅샷 또는 새 백업을 만듭니다.
* 설치하기 전에 인스턴스를 다시 시작합니다. 이 작업은 인스턴스가 여전히 업데이트 모드인 경우(및 인스턴스가 이전 버전에서 업데이트된 경우)에만 필요하지만 인스턴스가 오랫동안 실행 중인 경우 권장됩니다.

>[!NOTE]
>
>AEM 6.5.5.0 패키지를 삭제하거나 제거하지 않는 것이 좋습니다.

### 서비스 팩 설치 {#install-service-pack}

기존 AEM 6.5 인스턴스에 서비스 팩을 설치하려면 다음 단계를 수행하십시오.

1. 패키지 [공유](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.5.0) 또는 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip) 링크를 클릭하여 패키지를 다운로드합니다.

1. 패키지 [관리자를](http://localhost:4502/crx/packmgr/index.jsp) 열고 **패키지** 업로드를 클릭하여 패키지를 업로드합니다.

1. 패키지 이름을 선택하고 [설치]를 **클릭합니다**.

>[!NOTE]
>
>**패키지 관리자 UI의 대화 상자가 6.5.5.0 설치 중에 종료되는 경우가 있습니다.**
>
>따라서 인스턴스에 액세스하기 전에 오류 로그가 안정화될 때까지 기다리는 것이 좋습니다. 사용자는 Updater 번들 제거와 관련된 특정 로그가 생성된 후에 설치가 성공적으로 수행되었는지 확인해야 합니다. 일반적으로 Safari에서 발생하지만, 브라우저에서는 간헐적으로 발생할 수 있습니다.

**자동 설치**

실행 중인 인스턴스에 AEM 6.5.5.0을 자동으로 설치하는 두 가지 방법이 있습니다.

A. 서버가 온라인으로 제공되는 동안 패키지를 `../crx-quickstart/install ` 폴더에 넣습니다. 패키지가 자동으로 설치됩니다.

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/ko-KR/crx/2-3/how_to/package_manager.html) - make sure that you use `cmd=install&recursive=true` - so the nested packages  are  installed.

>[!NOTE]
>
>AEM 6.5.5.0은 부트스트랩 설치를 지원하지 않습니다.

**설치 확인**

1. 제품 정보 페이지(/system/console/ productinfo)에는 설치된 제품 아래에 업데이트된 버전 문자열 `Adobe Experience Manager, Version 6.5.5.0`이 표시됩니다.

1. 모든 OSGI 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]**&#x200B;이거나 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 콘솔 사용: /system/console/bundles).
1. The OSGI bundle `org.apache.jackrabbit.oak-core` is on version 1.10.6 or higher (Use Web Console: `/system/console/bundles`).

이 릴리스에서 실행하도록 인증된 플랫폼을 보려면 [기술 요구 사항](/help/sites-deploying/technical-requirements.md)을 참조하십시오.

### AEM Forms 추가 기능 패키지 설치 {#install-aem-forms-add-on-package}

>[!NOTE]
>
>AEM Forms를 사용하지 않는 경우 건너뜁니다. AEM Forms의 수정 사항은 별도의 추가 기능 패키지를 통해 전달됩니다.

1. AEM 서비스 팩을 설치했는지 확인합니다.
1. 운영 체제에 대한 [AEM Forms 릴리스](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html)에 나열된 해당 양식 추가 기능 패키지를 다운로드합니다.
1. [AEM Forms 추가 기능 패키지 설치](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)에 설명된 대로 양식 추가 기능 패키지를 설치합니다.

### JEE에 AEM Forms 설치 {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE에서 AEM Forms를 사용하지 않는 경우 건너뜁니다. 별도의 설치 프로그램을 통해 JEE의 AEM Forms 수정 사항이 전달됩니다.

JEE의 AEM Forms용 누적 설치 프로그램 설치 및 배포 후 구성에 대한 자세한 내용은 [패치 0014에 대한 릴리스 노트](https://helpx.adobe.com/kr/aem-forms/quick-fixes/6-5/jee-patch-0014.html)를 참조하십시오.

### UberJar {#uber-jar}

AEM 6.5.5.0용 UberJar는 [Adobe Public Maven 저장소](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.5/)에서 사용할 수 있습니다.

Maven 프로젝트에서 UberJar를 사용하려면 문서 [Uberjar 사용 방법](/help/sites-developing/ht-projects-maven.md)을 참조하여 프로젝트 POM에 다음 종속성을 포함하십시오.

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.5</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## 이제 사용되지 않는 기능 {#removed-deprecated-features}

이 섹션에는 AEM 6.5.5.0에서 더 이상 사용되지 않는 것으로 표시된 기능이 나와 있습니다. 이후 릴리스에서 제거될 예정인 기능은 먼저 사용 중지로 설정되고 사용할 대체 옵션이 제공됩니다.

고객은 현재 배포에서 기능을 사용할지 검토하고 대체 옵션을 사용할 수 있도록 구현 변경을 계획하는 것이 좋습니다.

| 영역 | 기능 | 대체 |
|---|---|---|
| 통합 | **[!UICONTROL AEM 클라우드 서비스 옵트인]** 화면은 더 이상 사용되지 않습니다. AEM 6.5에서 Adobe IMS 및 I/O를 통해 인증을 사용하는 Target 표준 API를 지원하고 분석 및 개인 설정을 위해 AEM 페이지를 계측하는 Adobe Launch의 늘어나는 역할을 지원하도록 AEM 및 Target 통합이 업데이트되어 옵트인 마법사가 기능상 무관해졌습니다. | 해당 AEM 클라우드 서비스를 통해 시스템 연결, Adobe IMS 인증 및 Adobe I/O 통합 구성 |

## 알려진 문제 {#known-issues}

* 11과 함께 [!DNL Experience Manager] [!DNL Java] 6.5.5.0을 설치하는 경우 서비스 팩을 설치한 후 서버를 다시 시작합니다. 서비스 팩 [!DNL Java] 8을 설치하는 경우 다시 시작할 필요가 없습니다.

* 계층 구조의 폴더 [!DNL Experience Manager Assets] 가 에서 이름이 변경되고 에셋이 포함된 중첩된 폴더가 게시되는 경우 루트 폴더가 다시 게시될 [!DNL Brand Portal][!DNL Brand Portal] 때까지 폴더의 제목이 업데이트되지 않습니다.

* 버전 83의 업데이트로 인해 패키지 빌드에 문제가 발생했습니다. [!DNL chrome] 사용 가능한 기타 브라우저(예: [!DNL Internet Explorer] 및 기타 AEM [!DNL Firefox]표준 패키지 설치 옵션)를 사용하여 문제를 해결하십시오.

* TLS v1.2를 사용하는 통신만 허용하므로 AEM 기본 메일 보낸 사람을 사용하여 원격 SMTP 서버로 이메일을 보낼 수 없습니다. 번들을 제거하고 번들을 새로 고쳐 문제를 해결하십시오. `javax.mail:mail:1.5.0-b01` `system/console`

* 사용자가 적응형 양식에서 처음으로 필드를 구성하도록 선택하면 구성 저장 옵션이 속성 브라우저에 표시되지 않습니다. 동일한 편집기에서 응용 양식의 다른 필드 일부를 구성하도록 선택하면 문제가 해결됩니다.

* [!UICONTROL 연결된 자산 구성] 마법사가 설치 후 404 오류 메시지를 반환하는 경우 패키지 관리자를 사용하여 `cq-remotedam-client-ui-content` 및 `cq-remotedam-client-ui-components` 패키지를 수동으로 다시 설치합니다.

* AEM 6.5.x.x를 설치하는 동안 다음 오류 및 경고 메시지가 표시될 수 있습니다.
   * Target 표준 API(IMS 인증)를 사용하여 AEM에 Target 통합이 구성된 경우 환경 조각을 Target으로 내보내면 잘못된 오퍼 유형이 생성됩니다. 경험 조각/소스 Adobe Experience Manager 유형 대신 Target은 HTML/소스 Adobe Target Classic 유형으로 여러 가지 오퍼를 작성합니다.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: granite/operations/maintenance에 유지 관리 창이 없습니다.
   * SUM, MAX 및 MIN과 같은 집계 함수를 사용하는 경우 적용형 양식 서버측 유효성 검사가 실패합니다. CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance에 유지 관리 창이 없습니다.
   * 쇼퍼블 배너 뷰어를 통해 자산을 미리 보는 동안 Dynamic Media 대화형 이미지의 핫스팟이 표시되지 않습니다.

## OSGi 번들 및 콘텐츠 패키지가 설치됨 {#osgi-bundles-and-content-packages-included}

다음 텍스트 문서에는 AEM 6.5.5.0에 포함된 OSGi 번들 및 컨텐츠 패키지가 나열되어 있습니다.

* [AEM 6.5.5.0에 포함된 OSGi 번들 목록](assets/6550_bundles.txt)

* [AEM 6.5.5.0에 포함된 콘텐츠 패키지 목록](assets/6550_packages.txt)

## 제한된 사이트 {#restricted-sites}

다음 사이트는 고객만 사용할 수 있습니다. 액세스가 필요한 고객의 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [고객 지원에 문의하기](https://docs.adobe.com/content/help/en/customer-one/using/home.html)
지원 포털에 액세스하는 방법에 대한 자세한 내용은 [지원 포털에 액세스](https://helpx.adobe.com/kr/experience-manager/kb/accessing-aem-support-portal.html)를 참조하십시오.

>[!MORELIKETHIS]
>
>* [AEM 6.5 릴리스 노트](/help/release-notes/release-notes.md)
>* [AEM 제품 페이지](https://www.adobe.com/kr/solutions/web-experience-management.html)
>* [AEM 6.5 설명서](https://helpx.adobe.com/kr/support/experience-manager/6-5.html)
>* [Adobe 우선 순위 제품 업데이트](https://www.adobe.com/subscription/priority-product-update.html) 구독

