---
title: 용 릴리스 노트 [!DNL Adobe Experience Manager] 6.5
description: 릴리스 정보, 새로운 기능, 사용 방법 설치 및 다음에 대한 자세한 변경 목록을 찾습니다. [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: 0bd7c444bf0424b60c11b7171b7ea7ae9d7f3926
workflow-type: tm+mt
source-wordcount: '2624'
ht-degree: 14%

---

# [!DNL Adobe Experience Manager] 6.5 최신 서비스 팩 릴리스 노트 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession&cid=a915e87c-369a-480c-9daf-d13efc766798 -->

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 버전 | 6.5.14.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2022년 8월 25일 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 다운로드 URL | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.14.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 에 포함된 사항 [!DNL Experience Manager] 6.5.14.0 {#what-is-included-in-aem-6514}

[!DNL Experience Manager] 6.5.14.0에는 2019년 4월에 6.5의 초기 가용성 이후 릴리스된 새로운 기능, 주요 고객이 요청한 향상된 기능, 버그 수정 사항, 성능, 안정성 및 보안 개선 사항이 포함되어 있습니다. [이 서비스 팩 설치](#install) on [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_

* Added support for password reset for Dynamic Media Classic users within Experience Manager. (ASSETS-10298) -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6514}

* PDF 파일에 대한 태그를 추가하거나 볼 수 없습니다. (NPR-38452)
* 연결된 자산을 구성하고, 구성을 저장하고, 구성 페이지를 다시 열고, 이미 저장된 구성을 테스트할 때 테스트 연결이 실패합니다. (NPR-38507)
* 숫자 사용자 ID를 가진 사용자를 컬렉션에 추가할 수 없습니다. (NPR-38538)
* Experience Manager이 작성자 인스턴스에 설치된 FFmpeg를 처리하지 못합니다. (NPR-38568)
* PDF 처리가 `NoClassDefFoundError` 오류 메시지. (NPR-38741)
* 에 대한 자산 보고서를 만드는 동안 사용자 지정 열 아래의 추가 단추가 올바르게 표시되지 않습니다 `de_DE` 로케일. (ASSETS-10641)
* 중복 자산을 Digital Asset Management 저장소에 업로드하고 Experience Manager이 중복 자산을 감지하여 삭제하는 옵션을 제공하면 원본 자산도 저장소에서 삭제됩니다. (ASSETS-10826)
* 여러 필드에 특수 문자를 지정할 때 Experience Manager이 폴더 메타데이터를 올바르게 저장하지 않습니다. (ASSETS-10721)
* 를 클릭할 때까지 자산 속성을 저장할 수 없습니다 **[!UICONTROL 저장 및 닫기]** 두 번 (ASSETS-12040)
* 화면 판독기는 `Relate` 버튼을 클릭합니다. 하지만, `Relate` 단추에는 하위 메뉴가 포함되어 있으며 확장하거나 축소할 수 있습니다. (ASSETS-6938)
* 필수 ARIA(Accessible Rich Internet Applications) 속성 `aria-expanded` 대상 `role="combo box"` 이(가) 없습니다. (ASSETS-6928)
* 카드 보기의 기본 파일 탐색 영역에서 텍스트 컨텐츠를 **[!UICONTROL 정렬 기준]** 배경 색상에 대한 대비 비율이 4.5:1 이상이면 안 됩니다. (ASSETS-6926)
* Experience Manager이 **[!UICONTROL 워크플로우 모델 선택]** 워크플로우 모델을 만드는 동안 드롭다운 목록을 필수 필드로 표시합니다. (ASSETS-6871)

>[!NOTE]
>
>2022년 9월 1일부터 새로운 Experience Manager Assets 온-프레미스 고객은 스마트 컨텐츠 서비스를 사용할 수 없습니다. 이 기능이 이미 활성화되어 있는 기존 On-Premise 및 Adobe Managed Services 고객에게 영향을 주지 않습니다.

### [!DNL Dynamic Media] {#dynamic-media-6514}

* Experience Manager 내에서 Dynamic Media Classic 사용자에 대한 암호 재설정 지원을 추가합니다. (ASSETS-10298)
* 투명한 배경이 있는 이미지에 대해 생성된 스마트 자르기는 흰색 배경이 있습니다. (ASSETS-13148)
* Dynamic Media은 EPS 파일에 대한 축소판을 생성하지 않습니다. (ASSETS-10959)
* 업로드 매개 변수가 누락되어 Dynamic Media 계정에 자산이 업로드되지 않습니다. (ASSETS-13165)
* 이름이 127자보다 큰 자산을 Dynamic Media에 업로드할 수 있습니다. (ASSETS-9991)
* Experience Manager 6.5.14.0에서 Dynamic Media Viewer용 JavaScript ES6(ECMAScript 6) 지원. (NPR-38393)
* Dynamic Media에서 옵션 구성 **[!UICONTROL 일반 설정]** 및 **[!UICONTROL 게시 설정]** 관리자가 아닌 사용자가 액세스할 수 없습니다. (ASSETS-8628)
* Dynamic Media **[!UICONTROL 일반 설정]** 페이지에 이미 구성된 업로드 매개 변수가 올바르게 표시되지 않습니다. (ASSETS-10245)
* 설정 생성/업데이트가 실패하는 경우 Experience Manager 사용자 인터페이스에 오류 메시지가 표시되지 않습니다. (ASSETS-10264)
* 편집 가능한 템플릿의 컨테이너 중 하나에 저장된 정책을 적용하여 Dynamic Media 구성 요소를 추가할 수 없습니다. (ASSETS-11044)
* 잘못된 작업 핸들이 있는 자산에서 Dynamic Media 자산 재처리 워크플로우를 실행한 후 자산이 Dynamic Media 계정에 업로드되지 않습니다. (ASSETS-12084, ASSETS-9877)
* 화면 판독기 사용자는 `title` 속성이 `<frame>` 및 `<iframe>` 에서 **[!UICONTROL 검색할 유형]** 대화 상자 (ASSETS-5483)
* 화면 판독기에서 관련 및 의미 있는 `alt=` 값은 아래에 있는 여러 이미지에 제공해야 합니다. **[!UICONTROL 자산]** 왼쪽 창의 머리글입니다. (ASSETS-5644)
* 화면 판독기가 읽지 않음 **[!UICONTROL 음소거]** 및 **[!UICONTROL 음소거 해제]** Dynamic Media 구성 요소를 사용하여 비디오에 표시되는 단추. (ASSETS-10169)

## 상거래 {#commerce-6514}

* 전자 상거래 제품이 열 헤더를 사용하여 정렬되지 않고 사용 중입니다 _원격_ 정렬 모드; 대신 상거래 제품은 _로컬_ 정렬 모드. (CQ-4343750, NPR-38498)

## [!DNL Forms] {#forms-6514}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] 는 예약된 후 1주일 후에 추가 기능 패키지를 출시합니다 [!DNL Experience Manager] 서비스 팩 릴리스 날짜입니다. 이 경우 추가 기능 패키지는 2022년 9월 1일 목요일에 릴리스됩니다. 또한 Forms 수정 사항 및 개선 사항 목록이 이 섹션에 추가됩니다.


## 통합 {#integrations-6514}

* JavaScript ES6(ECMAScript6 모드 이상) 컴파일 지원을 활성화하여 `/libs/cq/analytics/widgets.js` 라이브러리. (NPR-38433)
* JavaScript ES6(ESMAScript6 모드 이상) 컴파일 지원을 활성화하여 `/libs/cq/testandtarget/clientlibs/testandtarget/util.js` 라이브러리. (NPR-38435)
* 에 더 많은 콘텐츠가 있습니다 `/content/campaigns`를 호출하면 `targeteditor.html` (`/libs/cq/personalization/touch-ui/content/targeteditor.html`)은 페이지 편집기를 열 때 사용됩니다. (NPR-38663)

## 플랫폼 {#platform-6514}

* 업데이트를 배포하기 위해 패키지 관리자에 로그온할 수 없습니다. (NPR-38646)
* 자산 태그 선택기 사용자 인터페이스에서 태그는 작성된 순서대로 나타납니다. 하지만 태그가 많은 경우 태그를 정렬할 수 없으므로 보고 관리하는 것은 어렵습니다. (CQ-4344279)
* 사용자가 관리자 또는 을 사용하는 다른 사람에게 가장될 때 사용자 인터페이스에서 알림을 만듭니다 **[!UICONTROL 가장 대상]** 필드. (CQ-4345288)
* 스마트 컬렉션에서 저장된 검색을 사용하여 필터링할 때 모든 자산이 표시되었습니다. (CQ-4345326)
* 에 대해 잘못 선택한 자산 수가 표시됩니다 **[!UICONTROL 컬렉션에 추가]** when **[!UICONTROL 모두 선택]** 이 선택되어 있습니다. (CQ-4345424)
* 을(를) 사용하는 동안 예외 메시지가 발생했습니다. **[!UICONTROL 가장 대상]** 그룹 또는 존재하지 않는 사용자가 있는 필드. (CQ-4346098)

## [!DNL Sites] {#sites-6514}

* Experience Manager을 6.5.12.0에서 6.5.13.0으로 업그레이드하는 동안 예기치 않은 경로 삭제가 발생했습니다. (NPR-38532)

### 접근성 {#access-6514}

* Experience Manager Sites에서 **[!UICONTROL 표시 형식 전환 및 표시 설정 조정]** 단추를 누른 다음 **[!UICONTROL 목록 보기]**, **[!UICONTROL 드래그 앤 드롭]** 단추에 액세스 가능한 이름이 없습니다. (SITES-2863, NPR-38760)
* 화면 판독기는 다음과 같은 액세스 가능한 이름을 알려주어야 합니다 `Show description for Archive` 또는 `Show description for mini shopping cart`. 그러나 현재 액세스 가능한 이름은 `Info Circle button show description` 대상 _모두_ 도구 설명 정보 단추. (SITES-3104)
* 에 inlineEditing 또는 dropTarget 기능이 없는 구성 요소에 대한 실행 취소를 개선합니다. `cq:editConfig`. (NPR-38361) <!-- version 2 (old) of the description above * When out of the box components that don't have inlineEditing or dropTarget feature in the _cq_editConfig file (navigation, breadcrumb, embed) are deleted > undeleted (by way of Undo), all configurations are lost and empty placeholder reappears. Component must be reconfigured from scratch. (NPR-38361) -->
* 스타일 시스템 드롭다운이 구성 요소를 사용하는 구성 요소에 대해 구성 요소의 컨텍스트 대신 페이지 맨 위에 배치되었을 수 있습니다 `cq:editConfig` &quot;AFTERED: REFRESH_PAGE&quot;. (NPR-38384) <!-- version 2 (old) of description above* When selecting a style option on a component, the Styles box shifts to the upper left corner of the screen, rather than staying put below the style icon. Happens for components that have  cq:editConfig "afteredit: REFRESH_PAGE". (NPR-38384) -->
* 중첩된 레이아웃 컨테이너에 추가할 때 텍스트 구성 요소가 잘못 정렬되었습니다. (NPR-38193)
* 구성 요소에 대한 스타일 시스템 구성이 없을 때 빈 스타일 탭이 표시되었습니다. 구성이 없을 때 이제 탭이 숨겨집니다. (NPR-38218) <!-- version 2 (old) of description above * Style tab is blank on components without styles/policies. (NPR-38218) -->
* 속성 `useLegacyResponsiveBehaviour` 는 인증된 경우에만 작동합니다. (NPR-37996)
* jquery-ui를 최신 버전으로 업그레이드하면 편집기가 중단됩니다. (SITES-5647)

### [!DNL Content Fragments] {#sites-contentfragments-6514}

* 컨텐츠 조각 열거형 필드 유효성 검사는 컨텐츠 조각을 처음 로드할 때 발생합니다. (SITES-7140)
* 컨텐츠 조각 편집기의 리치 텍스트 편집기에서 Campaign 개인화 필드를 추가해야 합니다. (NPR-38526)
* 컨텐츠 조각 편집기에서 새 컨텐츠 조각을 만들거나 편집할 때 Dispatcher를 통해 컨텐츠 조각 모델이 저장되지 않습니다. 또한 컨텐츠 조각 편집기가 닫히지 않고 브라우저 로그에 오류가 표시됩니다. (NPR-38691)
* 영구 쿼리 유효성 검사 오류입니다. (NPR-38523)
* 컨텐츠 조각 대화 상자의 **[!UICONTROL 속성]**, **[!UICONTROL 컨텐츠 조각]** 선택 팝업에서는 필드가 저장된 경로를 유지하지 않습니다. (NPR-38632)
* 컨텐츠 조각 모델을 만들고 드롭다운 유형의 열거형 필드를 추가하는 경우 올바른 유효성 검사 _`is required`_실패. (NPR-38237)

### 핵심 구성 요소 {#sites-corecomponents-6514}

* 새 페이지 이메일 구성 요소를 편집하면서 클래식 사용자 인터페이스로 강요하면 안 됩니다 `/etc`. (NPR-38648)

### 페이지 편집기 {#sites-pageeditor-6514}

* 구성 요소의 크기를 원하는 개수의 열로 조정할 수 없습니다. (NPR-38688)

### 템플릿 편집기 {#sites-templateeditor-6514}

* 누락 **[!UICONTROL 삭제]** 및 **[!UICONTROL 잘라내기]** 편집 가능한 템플릿의 메뉴 모음에 있는 단추 `cq:actions` 속성이 사용자 지정되었습니다. (NPR-38521)
* 구성 요소에 다른 구성 요소가 포함되어 있으면 **[!UICONTROL 삭제]** 메뉴 모음에서 단추가 없습니다. (NPR-38585)

## 슬링 {#sling-6514}

* 모듈의 메모리 누출로 인해 프로덕션에서 열린 파일 수가 증가했습니다 `DiscoveryLiteDescriptor` in `org.apache.sling.discovery.commons`, 버전 1.0.20. (NPR-38288)
* Experience Manager에서 **[!UICONTROL 작업]** > **[!UICONTROL 진단]**&#x200B;를 선택하면 오류가 발생합니다. **[!UICONTROL 다운로드 상태 ZIP]** > **[!UICONTROL 다운로드]**. (NPR-38514)

## 번역 프로젝트 {#translation-6514}

* 상위 페이지에서 참조로 추가된 하위 페이지용 Launch가 `isDeep` 속성이 `false`. (NPR-38531)

## 사용자 인터페이스 {#ui-6514}

* 사용 시 **[!UICONTROL 모두 선택]** > **[!UICONTROL 빠른 게시]**, Experience Manager이 일부 자산을 게시하거나 게시할 자산 수를 표시하지 않았습니다. **[!UICONTROL 카드]** 보기 또는 **[!UICONTROL 목록]** 보기. (NPR-38546)
* 에 대해 잘못된 선택한 자산 수가 표시됩니다 **[!UICONTROL 컬렉션에 추가]** in **[!UICONTROL 모두 선택]** 예 (NPR-38633)
* 비활성화된 사용자는 여전히 컬렉션 및 프로젝트에 추가할 수 있습니다. (NPR-38651)
* 검색 양식을 저장하지 않고 필터를 삭제하면 오류가 발생합니다. (NPR-38698)
* 사용자의 세션은 `ModifiableValueMap` 직접 그룹 구성원을 설정하기 위한 그룹의 인스턴스입니다. (NPR-38710)

## 워크플로 {#workflow-6514}

* JavaScript ES6(ESMAScript6 모드 이상) 컴파일 지원을 활성화하여 `/libs/cq/inbox/gui/components/inbox/clientlibs/commons.js` 라이브러리. (NPR-38304)
* 워크플로우가 실행되고 프로세스 단계가 완료되면 동일한 주석이 여러 번 반복됩니다. (NPR-38364)

## 설치 [!DNL Experience Manager] 6.5.14.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.14.0 필요 [!DNL Experience Manager] 6.5. 참조: [업그레이드 설명서](/help/sites-deploying/upgrade.md) 자세한 지침 <!-- UPDATE FOR EACH NEW RELEASE -->
* 서비스 팩은 Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 다운로드할 수 있습니다.
* MongoDB 및 여러 인스턴스가 포함된 배포에서 을 설치합니다. [!DNL Experience Manager] 패키지 관리자를 사용하는 작성자 인스턴스 중 하나에 대한 6.5.14.0.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!NOTE]
>
>Adobe은 [!DNL Experience Manager] 6.5.14.0 패키지. <!-- UPDATE FOR EACH NEW RELEASE -->

### 서비스 팩 설치 [!DNL Experience Manager] 6.5 {#install-service-pack}

1. 인스턴스가 업데이트 모드(이전 버전에서 인스턴스가 업데이트되었을 때)인 경우 설치하기 전에 인스턴스를 다시 시작합니다. Adobe은 인스턴스에 대한 현재 가동 시간이 높은 경우 다시 시작할 것을 권장합니다.

1. 설치하기 전에 스냅샷 또는 새 백업 [!DNL Experience Manager] 인스턴스.

1. 에서 서비스 팩 다운로드 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.14.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. 패키지 관리자를 연 다음 **[!UICONTROL 패키지 업로드]** 를 눌러 패키지를 업로드합니다. 자세한 내용은 [패키지 관리자](/help/sites-administering/package-manager.md).

1. 패키지를 선택한 다음 을 선택합니다 **[!UICONTROL 설치]**.

1. S3 커넥터를 업데이트하려면 서비스 팩을 설치한 후 인스턴스를 중지하고 기존 커넥터를 설치 폴더에 제공된 새 이진 파일로 바꾸고 인스턴스를 다시 시작합니다. 자세한 내용은 [Amazon S3 데이터 저장소](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>패키지 관리자 UI에 대한 대화 상자가 서비스 팩을 설치하는 동안 종료되는 경우가 있습니다. 배포에 액세스하기 전에 오류 로그가 안정될 때까지 기다리는 것이 좋습니다. 업데이터 번들 제거와 관련된 특정 로그를 기다린 후 설치가 성공했는지 확인합니다. 일반적으로 이 문제는 [!DNL Safari] 브라우저이지만 모든 브라우저에서 간헐적으로 발생할 수 있습니다.

**자동 설치**

자동으로 설치하는 데 사용할 수 있는 방법에는 두 가지가 있습니다 [!DNL Experience Manager] 6.5.14.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* 서버가 온라인 상태일 때 패키지를 `../crx-quickstart/install` 폴더에 넣습니다. 패키지가 자동으로 설치됩니다.
* [패키지 관리자에서 HTTP API](/help/sites-administering/package-manager.md#package-share)를 사용합니다. 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

>[!NOTE]
>
>Experience Manager 6.5.14.0은 Bootstrap 설치를 지원하지 않습니다. <!-- UPDATE FOR EACH NEW RELEASE -->

**설치 확인**

이번 릴리스에서 사용할 수 있는 인증된 플랫폼을 확인하려면 [기술 요구 사항](/help/sites-deploying/technical-requirements.md).

1. 제품 정보 페이지(`/system/console/productinfo`)에 업데이트된 버전 문자열 표시 `Adobe Experience Manager (6.5.14.0)` 아래에 [!UICONTROL 설치된 제품]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 모든 OSGI 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]**&#x200B;이거나 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 콘솔 사용: `/system/console/bundles`).

1. OSGi 번들 `org.apache.jackrabbit.oak-core` 버전 1.22.12 이상(웹 콘솔 사용: `/system/console/bundles`). <!-- NPR-38747 -->


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

용 UberJar [!DNL Experience Manager] 6.5.13.0은 [Maven 중앙 저장소](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.13/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>Experience Manager 6.5.14.0에서 UberJar 버전(6.5.13.0)은 이전 릴리스와 동일하게 유지됩니다.

Maven 프로젝트에서 UberJar를 사용하려면 다음을 참조하십시오 [uberJar 사용 방법](/help/sites-developing/ht-projects-maven.md) 프로젝트 POM에 다음 종속성을 포함하십시오. <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

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
| 통합 | 다음 **[!UICONTROL AEM 클라우드 서비스 옵트인]** 화면은 다음부터 사용되지 않습니다 [!DNL Experience Manager] 및 [!DNL Adobe Target] 통합이에서 업데이트됨 [!DNL Experience Manager] 6.5. 통합은 Adobe Target Standard API를 지원합니다. API는 Adobe IMS 및 [!DNL Adobe I/O Runtime]. 이 플러그인은 Adobe Launch가 악기 역할을 계속 수행할 수 있도록 지원합니다 [!DNL Experience Manager] 분석 및 개인화를 위한 페이지인 옵트인 마법사는 기능적으로 관련이 없습니다. | 시스템 연결, Adobe IMS 인증 및 구성 [!DNL Adobe I/O Runtime] 해당 [!DNL Experience Manager] 클라우드 서비스. |
| 커넥터 | Microsoft® SharePoint 2010 및 Microsoft® SharePoint 2013용 Adobe JCR Connector는 더 이상 사용되지 않습니다 [!DNL Experience Manager] 6.5. | 해당 없음 |

## 알려진 문제 {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THE LIST.
 -->

* [GraphQL 색인 패키지 1.0.3이 있는 AEM 컨텐츠 조각](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.3.zip)

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

다음 텍스트 문서에는 다음 항목에 포함된 OSGi 번들 및 컨텐츠 패키지 목록이 나와 있습니다. [!DNL Experience Manager] 6.5.14.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager 6.5.14.0에 포함된 OSGi 번들 목록](/help/release-notes/assets/65140_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.14.0에 포함된 컨텐츠 패키지 목록](/help/release-notes/assets/65140_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 제한된 웹 사이트 {#restricted-sites}

이러한 웹 사이트는 고객만 사용할 수 있습니다. 액세스가 필요한 고객의 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [Adobe 고객 지원 문의](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 제품 페이지](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 설명서](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ko-KR)
>* [Adobe 우선 순위 제품 업데이트](https://www.adobe.com/kr/subscription/priority-product-update.html) 구독

