---
title: 의 릴리스 정보 [!DNL Adobe Experience Manager] 6.5
description: 에 대한 릴리스 정보, 새로운 기능, 설치 방법 및 자세한 변경 목록을 확인하십시오. [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
exl-id: fed4e110-9415-4740-aba1-75da522039a9
source-git-commit: 1077aeabacb1dbb489dbc7222c45da0a35b8cf16
workflow-type: tm+mt
source-wordcount: '3777'
ht-degree: 13%

---

# [!DNL Adobe Experience Manager] 6.5 최신 서비스 팩 릴리스 노트 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=7yhrWb&nav=MTVfe0U0RjdDQUM3LTZCQ0EtNDk1Qy04Mjc1LTM2MUJEMzE1OEVGN30 -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, June 1, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 버전 | 6.5.17.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2023년 5월 25일 목요일 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 다운로드 URL | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 에 포함된 항목 [!DNL Experience Manager] 6.5.17.0 {#what-is-included-in-aem-6517}

[!DNL Experience Manager] 6.5.17.0에는 2019년 4월 6.5의 최초 출시 이후 릴리스된 새로운 기능, 주요 고객 요청 개선 사항, 버그 수정 사항 및 성능, 안정성, 보안 개선 사항이 포함되어 있습니다. [이 서비스 팩 설치](#install) 날짜 [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

이 릴리스의 몇 가지 주요 기능 및 개선 사항은 다음과 같습니다.

* **검색 환경 개선 사항** - 이제 검색 결과에 표시되는 자산에 대해 다음 작업을 빠르게 수행할 수 있습니다.
   * 워크플로 만들기
   * 버전 만들기
   * 자산 연결 또는 연결 해제

  해당 작업을 수행하기 위해 자산 위치로 이동하여 자산 속성을 볼 필요가 없습니다.
* **Dynamic Media _스냅샷_**- 테스트 이미지 또는 Dynamic Media URL 실험을 통해 여러 이미지 수정자의 출력과 파일 크기(WebP 및 AVIF 게재 포함), 네트워크 대역폭 및 디바이스 픽셀 비율에 대한 스마트 이미징 최적화를 확인합니다. [Dynamic Media 스냅샷](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html)을 참조하십시오.
* **Dynamic Media을 사용한 DASH 스트리밍** - Dynamic Media 비디오 게재의 적응형 스트리밍을 위해 시작된 새로운 프로토콜(DASH - HTTP를 통한 동적 적응형 스트리밍) 지원(CMAF가 활성화됨). 현재 모든 지역에서 사용할 수 있습니다. [지원 티켓을 통해 활성화됨](/help/assets/video.md#enable-dash-on-your-account-enable-dash).
* **Experience Manager Sites 및 컨텐츠 조각과 에셋 차세대 Dynamic Media 통합** - 이제 Experience Manager Assets as a Cloud Service 차세대 Dynamic Media 사용자는 Experience Manager Sites 6.5의 온-프레미스 또는 Managed Services 인스턴스를 통해 작성 및 전달하기 위해 이러한 클라우드 호스팅 자산을 사용할 수 있습니다.

**AEM Forms**

* **[AEM 페이지 편집기 내 적응형 양식](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)**: 이제 AEM 페이지 편집기를 사용하여 여러 양식을 빠르게 만들고 사이트 페이지에 추가할 수 있습니다. 이 기능을 통해 콘텐츠 작성자는 동적 비헤이비어, 유효성 검사, 데이터 통합, 기록 문서 생성 및 비즈니스 프로세스 자동화 등 적응형 양식 구성 요소의 기능을 사용하여 Sites 페이지에서 원활한 데이터 캡처 경험을 만들 수 있습니다. 다음과 같은 작업을 수행할 수 있습니다.
   * AEM Sites 편집기 또는 경험 조각에서 양식 구성 요소를 적응형 양식 컨테이너 구성 요소로 드래그 앤 드롭하여 적응형 양식을 만듭니다.
   * AEM Sites 편집기 내의 적응형 Forms 마법사를 사용하여 모든 Sites 페이지와 독립적인 양식을 만들 수 있으므로 여러 페이지에서 이러한 양식을 자유롭게 재사용할 수 있습니다.
   * Sites 페이지에 여러 양식을 추가하여 사용자 경험을 간소화하고 더 많은 유연성을 제공합니다.
* **[Experience Manager Forms에서 reCAPTCHA Enterprise 지원](/help/forms/using/captcha-adaptive-forms.md)**: 기존 Google reCAPTCHA v2 지원 외에도 Experience Manager Forms의 reCAPTCHA Enterprise 지원이 추가되어 사기 행위 및 스팸에 대한 보호 기능이 강화되었습니다.
* **[Experience Manager Forms을 통한 Adobe Acrobat Sign for Government 지원](/help/forms/using/adobe-sign-integration-adaptive-forms.md)**: 이제 AEM Forms이 Adobe Acrobat Sign for Government(FedRAMP 준수)와 통합되었습니다. 이 통합은 정부 관련 계정(정부 부서 및 기관)에 대한 적응형 양식 제출을 통해 전자 서명에 대한 고급 수준의 규정 준수 및 보안을 제공합니다. Adobe Acrobat Sign for Government와의 통합을 통해 Adobe 파트너 및 정부 고객은 적응형 Forms에서 전자 서명을 사용하여 가장 미션 크리티컬하고 민감한 비즈니스 제품군 중 일부를 수행할 수 있습니다. 이러한 추가적인 보안 계층을 통해 모든 전자 서명은 FedRAMP Moderate 규정을 완벽하게 준수할 수 있으므로 Adobe 정부 고객에게 안심할 수 있습니다.
* **[데이터 교환을 위해 Experience Manager Forms과 Salesforce 통합 활성화](/help/forms/using/oauth2-client-credentials-flow-for-server-to-server-integration.md)**: OAuth 2.0 클라이언트 자격 증명 플로우를 사용하여 Experience Manager Forms과 Salesforce 애플리케이션 간의 통합을 구성합니다. 이 기능을 통해 안전하고 직접적인 애플리케이션 인증 및 권한 부여가 가능하며 사용자 개입 없이 원활한 통신이 가능합니다.
* **워크플로우 엔진의 최적화 및 향상된 기능**: 워크플로 인스턴스 수를 최소화하여 워크플로 엔진의 성능을 높입니다. 에 더하여 `COMPLETED` 및 `RUNNING` 상태 값, 워크플로우는 다음 세 가지 새 상태 값도 지원합니다. `ABORTED`, `SUSPENDED`, 및 `FAILED`.


<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets]{#assets-6517}

* 40개 이상의 PDF을 동시에 게시하는 경우 [!DNL Experience Manager] 응답이 중지되어 잠시 동안 사용할 수 없게 됩니다. (ASSETS-21789)
* 테스트 사용자로 로그인한 경우 에셋의 속성을 클릭하면 특정 에셋과 관련된 에셋을 볼 수 없습니다. (ASSETS-21648)
* 를 사용하여 에셋을 편집하는 동안 `Desktop Actions`, 한 번에 5개 이상의 에셋을 체크 인하려고 하는 경우, `Limit Reached` 오류가 표시되고 선택한 에셋이 체크아웃됩니다. (ASSETS-21121)
* 컬렉션에서 이름별로 자산을 정렬할 수 없습니다. (ASSETS-20924)
* 이미지 형식 유형의 에셋에 대해 차원을 설정할 수 없습니다. (ASSETS-20835)
* 링크를 공유하는 동안 이메일 주소 검색/추가 필드의 툴팁 텍스트와 배경에 적절한 대비 비율이 표시되지 않습니다. (ASSETS-17347)
* 를 확장할 때 `Notifications`, 단락 간격으로 인해 텍스트가 제대로 표시되지 않습니다. (ASSETS-17345)
* 컬렉션에서 에셋을 복사할 때, `Public Collection` 확인란이 적절하게 표시되지 않습니다. (ASSETS-17343)
* 요소는 역할 없이 ARIA 속성을 사용합니다. (ASSETS-17325,ASSETS-17323)
* 를 확장할 때 링크를 설명하지 않음 `Notifications`. (ASSETS-17283)
* 를 탐색하고 확장할 때 [!DNL Smart Crop] 버튼의 경우, 콘텐츠는 목록처럼 표시되지만 무순서 목록으로 표시되지 않습니다. 그 결과, 스크린 리더는 무순서 목록을 인식하지 못하고 일반 텍스트로 읽는다. (ASSETS-17247)
* 다음 `Sort By` 레이블이 해당 드롭다운과 연결되어 있지 않습니다. 따라서 화면 판독기에서 드롭다운 옵션을 인식하지 못합니다. (ASSETS-17239)
* 를 사용하여 사용자를 추가하려고 할 때 키보드 Tab 또는 화살표 키를 사용하여 앞이나 뒤로 이동할 수 없음 `Add user` 콤보 상자. (ASSETS-17233)
* 화면 판독기가 워크플로 단계에 대한 정보를 올바르게 전달하지 않습니다(ASSETS-17285).
* 다음으로 이동 시 `Saved Searches` 콤보 상자, 이름과 역할 모두에 할당된 레이블이 없습니다. (ASSETS-17329)
* 탐색 시 `Collection` 텍스트를 마우스로 가리키기 *구성원*, 텍스트가 표시된 대로 표시되지 않습니다. 그 결과 화면 판독기는 제목 텍스트를 인식하지 못하고 일반 텍스트로 읽습니다. (ASSETS-17245)
* 액세스할 수 없음 `View Settings` 키보드에서 아래로 또는 위로 스크롤하는 키를 사용하는 옵션입니다. (ASSETS-17257)
* 검색 필터를 사용하여 발견된 여러 개의 선택한 자산에 대한 워크플로우를 트리거할 수 없습니다. (ASSETS-7689)
* 검색 결과에서 에셋(또는 여러 에셋)을 선택하면 관련 또는 관계 해제 옵션이 표시되지 않습니다. 그러나 그렇지 않으면 옵션을 사용할 수 있습니다. (ASSETS-7679)
* 검색 필터 패널은 로그인 후 한 번만 열리며 검색 페이지를 종료하고 검색을 다시 실행할 경우 열리지 않습니다. (ASSETS-7671)
* 링크를 공유하는 동안 이메일 콤보 상자에 적절한 대비 비율이 표시되지 않습니다. (ASSETS-17349)

<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST 
* When you select any file in a Collection and click `Download`, and then navigate to the email checkbox and expand it, regular text and email link is not recognizable due to background color. (ASSETS-17349) 
* When you navigate to `Smart Crop` option, the screen reader does not announce the expand or collapse state of the button. (ASSETS-17335)-->

## [!DNL Assets] - [!DNL Dynamic Media]{#dm-6517}

* Dynamic Media 클라우드 구성이 이미 있으면 Dynamic Media에 대한 연결이 끊어집니다. (ASSETS-23057)
* Dynamic Media 비디오가 많고 해결된 폴더를 탐색하는 동안 폴더 카드 보기에서 문제를 로드하지 못하는 동안 성능이 향상되었습니다. (ASSETS-23016)
* 미리 보기 토큰이에서 제거됨 `error.log` 보안 테스트 서버에서 보안 콘텐츠를 요청하는 데 사용할 수 있습니다. (ASSETS-22685)
* PDF 축소판 렌더링으로 그림자를 추가합니다. PDF 썸네일 렌더링 문제를 해결하기 위해 Gibson 라이브러리 버전 4.0.1680232194이 업그레이드되었습니다. (ASSETS-22585)
* Dynamic Media 하이브리드 모드는 이제 New Relic 에이전트 버전 8.0.1과 호환됩니다(ASSETS-22578).
* 이제 Experience Manager 시 Dynamic Media 파일을 미리 볼 때 Experience Manager ACL(액세스 제어 목록)이 유지됩니다. (ASSETS-21628)
* 사용자가 아래쪽 화살표 키 또는 Tab 키를 사용하여 탐색하려고 할 때 화면 판독기가 숨겨진 요소로 이동하지 않습니다. (ASSETS-5617)
* 이미지 프로필 사용자 인터페이스가 이름, 차원, 치수가 같거나 둘 다 같은 스마트 자르기에 대해 제한됩니다. (ASSETS-16997)
* 이제 이미지 프로필 사용자 인터페이스의 스마트 자르기에 대해 기본 너비 및 높이가 50픽셀로 설정됩니다. (ASSETS-16997)

## [!DNL Commerce]{#commerce-6517}

* 이동된 태그는 수집된 가비지 수집이지만 여전히 다음 제품에서 참조됩니다. `/var`. (CQ-4351337)

## [!DNL Forms]{#forms-6517}

* AEM 6.5.15.0 서비스 팩으로 업데이트한 후 HTML 5 양식이 작동하지 않거나 IE 호환성 모드의 Edge 브라우저에서 제대로 로드되지 않습니다. (FORMS-8526, FORMS-8523)
* 사용자가 AEM 6.5.16.0 서비스 팩을 적용하면 규칙 편집기가 열리지 않습니다. (FORMS-8290)
* Numeric Box 구성 요소에 최대 자릿수 유효성 검사가 적용되면 실패합니다. (FORMS-7938)
* 대화형 통신 문을 만드는 동안 PDF의 차트 구성 요소가 제대로 생성되지 않습니다. (FORMS-7827, FORMS-8297)
* Java™ 가비지 수집이 Experience Manager Forms OSGi 서버에서 오래된 일반 힙을 지울 수 없습니다. (FORMS-8207)
* 사용자가 Experience Manager 6.5.16.0 서비스 팩으로 업그레이드할 때 제출 후 CRX 메타데이터 속성이 누락됩니다. (FORMS-8205)
* 사용자가 적응형 양식에서 날짜 선택기 구성 요소를 비활성화해도 여전히 편집할 수 있습니다. (FORMS-7804)
* Experience Manager 6.5.16.0 Forms 서비스 팩에서 사용자가 정책 세트 코디네이터를 편집하려고 하면 관리자 문서 게시자가 항상 선택 취소된 상태로 유지됩니다. (FORMS-7775, FORMS-8599)
* 사용자가 Experience Manager 6.5.16.0 서비스 팩으로 업그레이드하면 변환해야 하는 문자열을 처리하는 &quot;GuideNode.externalize&quot; 메서드가 작동하지 않습니다. (FORMS-7709)
* 다음에서 `Assign task` 단계: 사용자가 &quot;알림 이메일 보내기&quot;를 선택하고 워크플로우를 호출하면 수신된 이메일에 텍스트가 제대로 표시되지 않습니다. 수신된 이메일의 텍스트 대신 물음표가 수신됩니다. (FORMS-7675)
* 기록 문서가 부분적으로 현지화되고 있습니다. (FORMS-7674, FORMS-7573)
* 특정 권한이 할당된 경우에도 사용자는 정책 집합을 편집할 수 없습니다. (FORMS-7665)
* 에서 사용자가 `forms-users` 그룹이 양식을 만들려고 하면 Experience Manager Forms 인스턴스가 충돌합니다. (FORMS-7629)
* 사용자가 적응형 양식에서 재설정, 저장 또는 제출 버튼을 클릭하면 화면에 메시지가 표시되지 않습니다. (FORMS-7524)
* Experience Manager 6.5.16.0 서비스 팩에서 PDFG 변환 성능을 개선하기 위해 절전 모드 간격을 구성할 수 있습니다. (FORMS-6752)
* 전환 옵션은 동일하게 유지되지만 사용자가 커서를 약간 드래그해도 필드의 가시성이 변경됩니다. (FORMS-6728)
* 사용자가 Experience Manager 6.5.15.0 서비스 팩으로 업그레이드하면 적응형 양식이 Internet Explorer에서 렌더링될 때 리디렉션이 작동하지 않습니다. (FORMS-6725)
* Experience Manager 디자이너가 만든 PDF 양식의 모든 배경 개체에 대한 PAC 2021 도구에서 오류를 다음과 같이 반환합니다. `Path object not tagged`. (FORMS-6707)
* 사용자가 받은 편지함에서 필터를 적용하면 오류가 발생합니다 `NullPointerException` 오류. (FORMS-6706)
* 사용자가 참조된 조각이 있는 템플릿(.tds) 파일을 가져오면 Experience Manager 디자이너가 충돌합니다. (FORMS-6702)
* Experience Manager Forms Designer 6.5에서 출력 서비스를 사용하여 정적 PDF을 만드는 경우 다음과 같은 오류가 발생합니다. `OCCD (optional content configuration dictionary) contains AS key`. (FORMS-6691)
* 사용자가 간단한 워크플로우를 만들고 간단한 변수를 추가하면 `set variable mapping` 오류가 발생했습니다. (FORMS-5819)
* 사용자가 출력 서비스를 사용하여 PDF을 생성하려고 할 때 가 로 표시되더라도 `PDF/A-1a`, 를 사용한 준수 확인`Preflight` 서비스 실패. (LC-3920837)
* Experience Manager 6.5.16.0 서비스 팩을 설치한 후 Experience Manager 디자이너를 열 수 없습니다. (LC-3921000)
* 사용자가 확인란과 라디오 단추를 추가할 때 PDF 표준에 따라 태그 트리의 구조가 생성되지 않습니다. (LC-3920838)
* 출력 서비스를 통해 PDF의 임베드 및 서브셋팅을 사용하여 정적 PDF을 생성하는 경우, 결과 글꼴에는 임베드된 글꼴만 포함됩니다. (LC-3920963)
* 히브리어 텍스트가 RTL 형식으로 잘못 표시됩니다. (LC-3919632)
* 사용자가 JBoss® 턴키 서버에서 Experience Manager 6.5.16.0 서비스 팩으로 업그레이드할 때 서명 서비스가 호출되지 않습니다. 발생한 오류는 다음과 같습니다. `java.lang.ClassCastException: com.adobe.xfa.TextNode cannot be cast to com.adobe.xfa.Element`. (FORMS-7833)
* Experience Manager 6.5.14.0 서비스 팩으로 업그레이드한 후 Workbench에서 한 위치에서 다른 위치로 CRX 노드를 이동하는 프로세스가 작동하지 않습니다. 오류는 다음과 같이 발생합니다 `ALC-CRX-30000-000: com.adobe.ep.crx.client.exceptions.CRCException: ALC-CRX-030-000-[Internal Server Error]`. (FORMS-7713)
* 사용자가 Experience Manager 6.5.16.0 서비스 팩으로 업데이트할 때에는 `Usage Rights` 적용되지 않습니다. (FORMS-7892)
* 사용자가 PDF 문서를 생성하려고 할 때 PDF/A-1b 유효성 검사가 실패합니다. (FORMS-7615)
* 사용자가 `Configure` 옵션 `Form Container` 구성 요소, 브라우저가 응답하지 않습니다. (FORMS-7605)
* 사용자가 Experience Manager Forms 6.5.16.0 서비스 팩으로 업데이트하고 를 변경하려고 할 때 `LicenseType` 끝 `Production`, 변경 사항이 반영되지 않습니다. (FORMS-7594)
* 사용자가 다음을 구성하는 PDF으로 LCA 프로세스를 호출하려고 하면 `Chinese Full Width Characters`에 문제가 발생합니다. `ValidateForm` 프로세스. (FORMS-7464)
* Experience Manager Forms Designer에서 XMLFM은 XDP 기반 템플릿에 대해 문자, A4 및 A5와 같이 서로 다른 용지 크기로 ZPL 출력을 생성합니다. (FORMS-7898)

## 통합{#integrations-6517}

* Adobe Target IMS 구성을 레거시 클라우드 구성에서 사용자 자격 증명 구성으로 전환할 때 `connectedWhen` 속성은 변경되지 않습니다. 이 문제는 구성이 여전히 IMS 기반인 것처럼 모든 호출을 실행합니다. (CQ-4352810)
* 추가 중 `modifyProperties` 권한 대상 `fd-cloudservice` Adobe Sign 구성에 대한 시스템 사용자입니다. (FORMS-6164)
* Adobe Target과 통합된 Experience Manager을 사용하여 AB 테스트 활동을 만들 때 이 활동과 연관된 대상을 Target에 동기화하지 않습니다. (NPR-40085)

## Oak{#oak-6517}

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

1. 에서 다음 두 폴더를 삭제합니다. `crx-quickstart/repository/`

   * `cache`
   * `diff-cache`

1. 서비스 팩을 설치하거나 Experience Manager을 as a Cloud Service으로 다시 시작합니다.
의 새 폴더 `cache` 및 `diff-cache` 이(가) 자동으로 만들어지므로 더 이상 과 관련된 예외가 발생하지 않습니다. `mvstore` 다음에서 `error.log`.

## Platform{#platform-6517}

* Experience Manager Tag Management 사용자 인터페이스(/aem/tags/)에서 네임스페이스 및 태그는 생성된 순서대로 표시됩니다. 그러나 네임스페이스와 태그가 많은 경우 네임스페이스를 보고 관리하는 기능이 어렵습니다. 이 문제는 다른 방법으로 정렬할 수 없기 때문입니다. (NPR-39620)
* 축소 js가 일부 클라이언트 라이브러리에서 작동하지 않기 때문에 Google 종료 버전을 업데이트해야 합니다. (NPR-40043)

## [!DNL Sites]{#sites-6517}

* LinkCheckerTransformer의 성능 저하. (SITES-11661)
* 페이지의 언어 사본이 예상대로 업데이트되지 않았습니다. (SITES-11191)
* 캠페인이 아닌 페이지 호출 열기 `targeteditor.html` 불필요하게. 제거 `targeteditor` 필요하지 않은 경우 를 호출합니다. (SITES-12469)
* 주석이 있는 페이지에 대해서는 라이브 카피를 만들 수 없습니다. (SITES-12154)
* Experience Manager 6.5.16에서 페이지 롤아웃이 작동하지 않습니다. (SITES-12008)
* 메모리 부족, 다음과 같은 이유로 높은 가비지 수집 활동 `NotificationManagerImpl`. `NotificationManager` Experience Manager 6.5로 번들 업그레이드. (SITES-11440)
* 서비스 팩 17을 차단하던 WCM IT 테스트를 수정했습니다. (SITES-13089)
* 서블릿에서 사이트 참조 검색이 실패합니다. (SITES-10901)

### [!DNL Sites] - 관리 사용자 인터페이스{#sites-adminui-6517}

* 썸네일 이미지 선택기의 미리 보기 창을 닫을 수 없습니다. (SITES-10459)

### [!DNL Sites] - [!DNL Content Fragments]{#sites-contentfragments-6517}

* Polaris 서비스 개체(URL, 자격 증명, 콜백 등)에 연결하기 위한 구성입니다. (SITES-12149)
* 사용 `SemanticDataType.REFERENCE` 은(는) &quot;Remote-Asset-ID&quot;를 지원해야 합니다. (SITES-12127)
* Polaris 자산 선택기를 컨텐츠 조각 편집기에 통합합니다. (SITES-12125)
* 메타데이터 서비스 끝점에 액세스하려면 필수 http 헤더가 필요합니다. (SITES-13068)
* 6.5의 GraphQL 구현은 Cloud Service(기본)과 일치하지 않습니다. 식별된 문제가 해결되었습니다. (SITES-13096)
* GraphQL 페이징/정렬 및 하이브리드 필터링은 Experience Manager 6.5/AMS에서 사용할 수 있어야 합니다. (SITES-9154)

### [!DNL Sites] - 핵심 구성 요소{#sites-core-components-6517}

* 속성 `cq-msm-lockable` 기초 페이지 구성 요소에 잘못된 리디렉션 값이 있습니다. (SITES-10904)
* 원격 자산 선택기는 항상 IMS 스테이징 환경으로 리디렉션합니다. (SITES-13433)

### [!DNL Sites] - [!DNL Experience Fragments]{#sites-experiencefragments-6517}

* Adobe Target으로 내보낼 때 경험 조각에서 외부화 구성을 선택하면 잘못된 외부화된 URL이 전송됩니다. (SITES-12402)
* 포괄적이지 않은 용어를 제거하고, 포괄적 용어 지침을 적용합니다. (SITES-11244)

### [!DNL Sites] - 페이지 편집기{#sites-pageeditor-6517}

* Experience Manager 콘텐츠 파인더 사이드 레일에 설정된 캐러셀에 대해 썸네일이 표시되지 않습니다. (SITES-8593)

## 슬링{#sling-6517}

* 슬링 `ResourceMerger` 가상 경로를 제공하면 많은 양의 CPU를 소모하여 서비스 거부를 초래합니다. (NPR-40338)

## 번역 프로젝트{#translation-6517}

<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST * The `translationrules.xml` is sorted poorly when adding a rule to a property by way of the translation configuration user interface. (NPR-40431) -->
* 사용자가 필수가 아닌 필드를 구성하지 않으면 언어 사본이 생성되지 않습니다. (NPR-40036)

## 사용자 인터페이스{#ui-6517}

* 페이지 속성의 취소 버튼이 비활성화되어 있으므로 사이트 관리자 사용자 인터페이스로 이동해야 합니다. (NPR-40501)

<!-- ## WCM{#wcm-6517}

* TEXT -->

## 워크플로{#workflow-6517}

* 워크플로 콘솔 변경 사항. (NPR-40502)
* `SegmentNotfound errors` 클래스에서 리소스 확인자가 닫히지 않아 발생하는 프로덕션 작성자 인스턴스의 로그 `com.day.cq.workflow.impl.email.EMailNotificationServic`. (NPR-40187)
* 닫히지 않은 A `ResourceResolver` 예외가 기록됩니다. (ASSETS-22495)
* 대규모 PSD/PDF 시 Experience Manager 작성자가 충돌함 `DocumentAncestors` 메타데이터 속성이 업로드됩니다. (ASSETS-22966)
* 클래스의 세션 누수 `InboxSharingCache` 포함 `user-reader-service`. (CQ-4352513)
* 워크플로 개시자 참가자 선택기 단계에 참가자 단계의 사용자 및 그룹이 나열되면 미완료 사용자 및 그룹 목록이 표시됩니다. 이 문제는 한 그룹이 다른 그룹의 구성원이기도 할 때 발생했습니다. (NPR-40055)
* 향상된 워크플로우 제거. (NPR-40459)

## 설치 [!DNL Experience Manager] 6.5.17.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.17.0을 사용하려면 [!DNL Experience Manager] 6.5. 참조 [업그레이드 설명서](/help/sites-deploying/upgrade.md) 자세한 지침은 을 참조하십시오. <!-- UPDATE FOR EACH NEW RELEASE -->
* 서비스 팩은 Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip)에서 다운로드할 수 있습니다.
* MongoDB 및 여러 인스턴스가 포함된 배포에서 다음을 설치합니다. [!DNL Experience Manager] 패키지 관리자를 사용하는 작성자 인스턴스 중 하나에서 6.5.17.0.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe은 를 제거하거나 제거하지 않는 것이 좋습니다. [!DNL Experience Manager] 6.5.17.0 패키지. 따라서 팩을 설치하기 전에 `crx-repository` 혹시라도 돌려주셔야 할 것 같은데요 <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### 서비스 팩 설치 [!DNL Experience Manager] 6.5{#install-service-pack}

1. 인스턴스가 업데이트 모드에 있는 경우(인스턴스가 이전 버전에서 업데이트된 경우) 설치 전에 인스턴스를 다시 시작하십시오. Adobe은 인스턴스의 현재 가동 시간이 높을 경우 다시 시작할 것을 권장합니다.

1. 설치하기 전에 스냅샷 또는 새 백업을 [!DNL Experience Manager] 인스턴스.

1. 에서 서비스 팩 다운로드 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. 패키지 관리자를 열고 를 선택합니다 **[!UICONTROL 패키지 업로드]** 패키지를 업로드합니다. 자세한 내용은 [패키지 관리자](/help/sites-administering/package-manager.md).

1. 패키지를 선택한 다음 를 선택합니다 **[!UICONTROL 설치]**.

1. S3 커넥터를 업데이트하려면 서비스 팩을 설치한 후 인스턴스를 중지하고 기존 커넥터를 설치 폴더에 있는 새 이진 파일로 바꾼 다음 인스턴스를 다시 시작하십시오. 다음을 참조하십시오 [Amazon S3 데이터 저장소](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>패키지 관리자 UI에 대한 대화 상자가 서비스 팩을 설치하는 동안 종료되는 경우가 있습니다. 배포에 액세스하기 전에 오류 로그가 안정될 때까지 기다리는 것이 좋습니다. 업데이터 번들 제거와 관련된 특정 로그를 기다린 후 설치가 성공했는지 확인합니다. 일반적으로 이 문제는에서 발생합니다. [!DNL Safari] 브라우저이지만 모든 브라우저에서 간헐적으로 발생할 수 있습니다.

**자동 설치**

를 사용하여 자동으로 설치할 수 있는 두 가지 방법이 있습니다 [!DNL Experience Manager] 6.5.17.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* 서버가 온라인 상태일 때 패키지를 `../crx-quickstart/install` 폴더에 넣습니다. 패키지가 자동으로 설치됩니다.
* [패키지 관리자에서 HTTP API](/help/sites-administering/package-manager.md#package-share)를 사용합니다. 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

>[!NOTE]
>
>Experience Manager 6.5.17.0은 Bootstrap 설치를 지원하지 않습니다. <!-- UPDATE FOR EACH NEW RELEASE -->

**설치 확인**

이 릴리스에서 사용할 수 있는 인증된 플랫폼을 확인하려면 다음을 참조하십시오. [기술 요구 사항](/help/sites-deploying/technical-requirements.md).

1. 제품 정보 페이지(`/system/console/productinfo`) 업데이트된 버전 문자열을 표시합니다 `Adobe Experience Manager (6.5.17.0)` 아래에 [!UICONTROL 설치된 제품]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 모든 OSGI 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]**&#x200B;이거나 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 콘솔 사용: `/system/console/bundles`).

1. OSGi 번들 `org.apache.jackrabbit.oak-core` 는 버전 1.22.15 이상입니다(웹 콘솔 사용: `/system/console/bundles`). <!-- NPR-40398 for 6.5.17.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### 서비스 팩 설치 [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Experience Manager Forms에 서비스 팩을 설치하는 방법은 다음을 참조하십시오. [Experience Manager Forms 서비스 팩 설치 지침](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### Experience Manager 콘텐츠 조각용 GraphQL 인덱스 패키지 설치{#install-aem-graphql-index-add-on-package}

GraphQL을 사용하는 고객은 [GraphQL 인덱스 패키지 1.1.1로 Experience Manager 컨텐츠 조각](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

이렇게 하면 필요한 인덱스 정의가 실제로 사용하는 기능을 기반으로 추가할 수 있습니다.

이 패키지를 설치하지 않으면 GraphQL 쿼리가 느려지거나 실패할 수 있습니다.

>[!NOTE]
>
>이 패키지는 인스턴스당 한 번만 설치하십시오. 모든 서비스 팩으로 다시 설치할 필요는 없습니다.

### UberJar{#uber-jar}

에 대한 UberJar [!DNL Experience Manager] 6.5.17.0은 [Maven Central 저장소](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.17/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Maven 프로젝트에서 UberJar를 사용하려면 [uberJar 사용 방법](/help/sites-developing/ht-projects-maven.md) 프로젝트 POM에 다음 종속성을 포함하십시오. <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.17</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar 및 기타 관련 아티팩트는 공개 Maven 저장소 Adobe 대신 Maven 중앙 저장소에서 사용할 수 있습니다(`repo.adobe.com`). 기본 UberJar 파일의 이름이 로 바뀝니다. `uber-jar-<version>.jar`. 그래서, `classifier`, 포함 `apis` 값으로, 을 사용합니다. `dependency` 태그에 가깝게 배치하십시오.

## 이제 사용되지 않는 기능{#removed-deprecated-features}

아래는 에서 더 이상 사용되지 않는 것으로 표시된 기능 및 기능 목록입니다 [!DNL Experience Manager] 6.5.7.0. 기능은 처음에는 더 이상 사용되지 않는 것으로 표시되며 이후 릴리스에서 제거됩니다. 대체 옵션이 제공됩니다.

배포에서 기능 또는 기능을 사용하는지 검토합니다. 또한 대체 옵션을 사용하도록 구현을 변경할 계획입니다.

| 영역 | 특별 포함 | 대체 |
|---|---|---|
| 통합 | 화면 **[!UICONTROL Experience Manager Cloud Services 옵트인]** 은(는) 다음 이후 더 이상 사용되지 않습니다: [!DNL Experience Manager] 및 [!DNL Adobe Target] 통합이에서 업데이트되었습니다. [!DNL Experience Manager] 6.5. 통합은 Adobe Target Standard API를 지원합니다. API는 Adobe IMS 및 [!DNL Adobe I/O Runtime]. Adobe Launch가 제공하는 악기 역할의 성장을 지원합니다 [!DNL Experience Manager] 분석 및 개인화를 위한 페이지에서, 옵트인 마법사는 기능적으로 관련이 없습니다. | 시스템 연결, Adobe IMS 인증 및 [!DNL Adobe I/O Runtime] 다음을 통한 통합 [!DNL Experience Manager] 클라우드 서비스. |
| 커넥터 | Microsoft® SharePoint 2010 및 Microsoft® SharePoint 2013용 Adobe JCR 커넥터는 더 이상 사용되지 않습니다. [!DNL Experience Manager] 6.5. | N/A |

## 알려진 문제{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* 콘텐츠 모델에 대해 사용자 지정 API 이름을 사용했을 수 있는 GraphQL 쿼리를 콘텐츠 모델의 기본 이름을 대신 사용하도록 업데이트합니다.

* GraphQL 쿼리는 `damAssetLucene` 색인 대신 `fragments` 색인입니다. 이 작업으로 인해 GraphQL 쿼리가 실패하거나 실행하는 데 시간이 오래 걸릴 수 있습니다.

  문제를 해결하려면 `damAssetLucene` 다음 두 속성을 포함하도록 을 구성해야 합니다.

   * `contentFragment`
   * `model`

  색인 정의를 변경한 후에는 리인덱싱이 필요합니다(`reindex` = `true`).

  이러한 단계 후에는 GraphQL 쿼리가 더 빨리 수행됩니다.

* 다음으로: [!DNL Microsoft® Windows Server 2019] 은(는) 을 지원하지 않습니다. [!DNL MySQL 5.7] 및 [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] 은(는) 다음에 대한 턴키 설치를 지원하지 않습니다. [!DNL Experience Manager Forms 6.5.10.0].

* 업그레이드 시 [!DNL Experience Manager] 6.5.0 - 6.5.4에서 Java™ 11의 최신 서비스 팩까지 인스턴스가 제공됩니다. `RRD4JReporter` 의 예외 `error.log` 파일. 예외를 중지하려면 인스턴스를 [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 사용자는 의 계층 구조에서 폴더의 이름을 변경할 수 있습니다. [!DNL Assets] 중첩된 폴더 게시 위치 [!DNL Brand Portal]. 단, 폴더의 제목은에서 업데이트되지 않습니다. [!DNL Brand Portal] 루트 폴더가 다시 게시될 때까지.

* 사용자가 적응형 양식에서 처음으로 필드를 구성하도록 선택하면 구성 저장 옵션이 속성 브라우저에 표시되지 않습니다. 동일한 편집기에서 적응형 양식의 다른 필드 일부를 구성하도록 선택하면 문제가 해결됩니다.

* 설치 중에 다음 오류 및 경고 메시지가 표시될 수 있습니다. [!DNL Experience Manager] 6.5.x.x:
   * &quot;Adobe Target 통합이에서 구성된 경우 [!DNL Experience Manager] target Standard API(IMS 인증)를 사용한 다음 경험 조각을 Target으로 내보내면 잘못된 오퍼 유형이 생성됩니다. Target은 &quot;경험 조각&quot;/소스 &quot;Adobe Experience Manager&quot; 유형 대신 &quot;HTML&quot;/소스 &quot;Adobe Target Classic&quot; 유형으로 여러 오퍼를 만듭니다.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: granite/operations/maintenance에 유지 관리 창이 없습니다.
   * SUM, MAX 및 MIN과 같은 집계 함수를 사용하는 경우 적용형 양식 서버측 유효성 검사가 실패합니다(CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance에 유지 관리 창이 없습니다.
   * 쇼퍼블 배너 뷰어를 통해 자산을 미리 볼 때 Dynamic Media 대화형 이미지의 핫스팟이 표시되지 않습니다.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : 등록 변경이 등록 취소를 완료할 때까지 기다리는 동안 시간이 초과되었습니다.

* 콘텐츠 조각, 사이트 또는 페이지를 이동, 삭제 또는 게시하려고 할 때 배경 쿼리가 실패하여 콘텐츠 조각 참조를 가져올 때 문제가 있습니다. 즉, 기능이 작동하지 않습니다.
올바른 작업을 위해 인덱스 정의 노드에 다음 속성을 추가해야 합니다 `/oak:index/damAssetLucene` (리인덱싱이 필요하지 않음):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* JBoss® 7.1.4 플랫폼에서 사용자가 Experience Manager 6.5.16.0 이상의 서비스 팩을 설치하면 `adobe-livecycle-jboss.ear` 배포가 실패합니다.
* 1.8.0_281 이상의 JDK 버전은 WebLogic JEE 서버에서 지원되지 않습니다.
* AEM 6.5.15부터 Rhino JavaScript Engine은 ```org.apache.servicemix.bundles.rhino``` 번들에 새로운 호스팅 동작이 있습니다. 엄격 모드를 사용하는 스크립트(```use strict;```)는 변수를 올바르게 선언해야 합니다. 그렇지 않으면 런타임 오류가 발생하는 대신 실행되지 않습니다.

## OSGi 번들 및 콘텐츠 패키지가 포함됨{#osgi-bundles-and-content-packages-included}

다음 텍스트 문서는에 포함된 OSGi 번들 및 콘텐츠 패키지 목록입니다. [!DNL Experience Manager] 6.5.17.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager 6.5.17.0에 포함된 OSGi 번들 목록](/help/release-notes/assets/65170_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.17.0에 포함된 컨텐츠 패키지 목록](/help/release-notes/assets/65170_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 제한된 웹 사이트{#restricted-sites}

이러한 웹 사이트는 고객만 사용할 수 있습니다. 고객이고 액세스 권한이 필요한 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [Adobe 고객 지원 문의](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 제품 페이지](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 설명서](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ko-KR)
>* [Adobe 우선 순위 제품 업데이트](https://www.adobe.com/kr/subscription/priority-product-update.html) 구독
