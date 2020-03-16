---
title: Adobe Experience Manager 6.5 서비스 팩 4의 새로운 기능
description: Adobe Experience Manager 6.5 서비스 팩 4의 새로운 기능
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: ed756d785864131c2e031aec4331388bc057576b

---


# Adobe Experience Manager 6.5 서비스 팩 4의 새로운 기능 {#aem-whats-new-service-pack-4}

AEM(Adobe Experience Manager) 6.5는 올해 분기별 서비스 팩을 통해 기능과 지속적인 개선을 제공합니다. 새로운 접근 방식을 통해 혁신적인 기능을 보다 신속하게 채택할 수 있게 됨으로써 고객에게 많은 이점을 제공합니다.

최신 AEM 서비스 팩 4(6.5.4.0)는 2020년 **3월 5일에 릴리스됩니다**. 이 문서에서는 AEM 여정을 더욱 풍성하게 만들기 위한 최신 서비스 팩 기능을 소개합니다.

## AEM Sites {#aem-sites}

### 다양한 영역의 성능 개선 {#performance-improvements}

* 사이트(contexthub.kernel.js)에서 ContextHub를 로드하고 초기화하는 데 걸리는 시간이 단축되었습니다. 사이트 방문 중에 페이지 로드가 빨라집니다.

* 경험 조각을 사이트 페이지 편집기로 드래그 앤 드롭한 후 페이지를 새로 고치는 시간을 줄였습니다.

* Live Copy 개요에서 200개 이상의 Live Copy를 사용하여 사이트 페이지에 대한 항목을 로드하는 시간을 단축했습니다.

* 불완전하거나 잘못된 URL의 처리가 개선되었습니다. 이러한 URL을 사용하면 템플릿 편집기의 속도가 느려질 수 있습니다.

또한 AEM 6.5.4.0에는 스타일 시스템 개선 사항이 포함되어 있습니다. 이제 구성 요소 대화 상자 내에서 스타일을 선택할 수 있습니다.

## AEM Assets {#aem-assets}

### Adobe I/O 콘솔을 통해 브랜드 포털과 통합 {#assets-integration-bp}

이제 Adobe I/O 콘솔을 통해 브랜드 포털에서 AEM 자산을 구성할 수 있습니다. Adobe I/O 콘솔은 브랜드 포털 임차인의 승인을 위해 IMS 토큰을 조달합니다. 이전에는 AEM 자산이 기존 OAuth 게이트웨이를 통해 클래식 UI의 브랜드 포털로 구성되었습니다. 기존 OAuth 게이트웨이를 사용하는 구성은 2020년 4월 6일까지 지원됩니다. 통합을 수정하지 않으면 기존 구성이 계속 작동합니다.

새 통합을 만들거나 통합 설정을 Adobe I/O 콘솔로 업그레이드할 수 있습니다.

### Accessibility enhancements {#accessibility-enhancements}

Experience Manager Assets에는 다음과 같은 액세서빌러티 개선 사항이 포함되어 있습니다.

* 키보드의 화살표 키를 사용하여 확대된 이미지 내에서 영역을 이동하고 이동할 수 있습니다. 자세한 내용은 키보드 키만 [사용하여 에셋](../assets/managing-assets-touch-ui.md#previewing-assets)미리 보기를 참조하십시오.

* [필터] 패널의 혼합 상태 확인란(중첩된 모든 항목을 선택하지 않으면 첫 번째 수준의 확인란이 선택되지 않고 하나씩 제공)은 화면 판독기에서 읽을 수 있습니다.

* 날짜 및 시간 형식 제약 조건은 사용자가 키보드를 사용하여 날짜를 올바른 형식으로 입력할 수 있도록 날짜 필드의 필드 레이블에 제공됩니다.

   예, `On Time (MM-DD-YYYY HH:mm)`. 여기서 MM은 두 자리 형식의 월이고, YYYY는 연도이고, DD는 두 자리 형식의 날, HH는 24시간 군 형식으로 시간, mm은 분입니다.

* 이제 선택한 태그 수와 함께 현재 선택한 태그를 제거하는 단추의 `X` 기호가 화면 판독기에 표시됩니다.

## AEM 양식 {#aem-forms}

### AEM Forms 워크플로우에서 인쇄 가능한 출력 생성 {#generate-printable-output}

소스 템플릿 파일의 여러 복사본을 인쇄하거나 저장하고 여러 레코드가 있는 데이터 파일과 통합하려는 경우 AEM Forms에서 새로운 인쇄 가능한 출력 생성 워크플로우 단계를 사용할 수 있습니다. 예를 들어 인쇄 시 다른 이름으로 소스 양식을 인쇄하려면 데이터 파일에 해당 이름을 지정하여 표준 템플릿 파일과 통합할 수 있습니다.

도구 > 워크플로우 **>** 모델 **[!UICONTROL >]** 모델 **[!UICONTROL >]** 생성 ******[!UICONTROL 및 생성]** 인쇄를 위한 검색 생성인쇄 가능한 출력 생성 워크플로우 단계를 사용하여 이 기능을 활용할 수 있습니다.

![인쇄 가능한 출력 생성](assets/generate-print-output-demo.gif)

이 기능에 대한 자세한 내용은 OSGi - [Step Reference에서 양식 중심의 워크플로우를 참조하십시오](../forms/using/aem-forms-workflow-step-reference.md).

### 레이아웃 모드에서 적응형 양식 및 인터랙티브한 커뮤니케이션을 위한 다중 열 지원 {#multi-column-adaptive-forms}

이제 적응형 양식 및 인터랙티브한 커뮤니케이션에서 패널의 열 수를 정의할 수 있습니다.

레이아웃 모드로 전환하면 새 옵션을 찾을 수 있습니다. 다중 열 형식으로 변환할 패널을 누르고, 상위 패널을 선택하고 다중 열 아이콘을 눌러 패널의 열 수를 정의합니다.

![다중 열 레이아웃](assets/multi-column-layout.gif)

자세한 내용은 레이아웃 모드를 사용하여 구성 [요소의](../forms/using/resize-using-layout-mode.md)크기를 조정하십시오.

### AEM 받은 편지함 사용자 정의 {#aem-inbox}

AEM 헤더에서 사용할 수 있는 옵션을 사용자 정의해야 한다고 생각하십니까? 이제 새로운 서비스 팩 릴리스에서 관리 제어 옵션이 도입되어 **[!UICONTROL 가능합니다]** .

**머리글 텍스트 사용자 지정**

이제 워크플로우 관리자는 원하는 머리글 텍스트를 지정할 수 있습니다.

보기 선택기(도구 모음의 오른쪽 **[!UICONTROL 상단에 있음) > 관리 제어에서 새로운 머리글 텍스트]** 사용자 지정 옵션을 찾을 **[!UICONTROL 수 있습니다]**.

**로고 사용자 정의**

이제 워크플로우 관리자는 머리글 텍스트 맞춤화와 마찬가지로 원하는 머리글 로고를 지정할 수 있습니다.

보기 선택기 > 관리 **[!UICONTROL 컨트롤에서]** 새로운 로고 사용자 지정 옵션을 찾을 수 **[!UICONTROL 있습니다]**.

이 기능에 대한 자세한 내용은 받은 편지함을 [참조하십시오](../sites-authoring/inbox.md).

### 사용자 탐색 제어 {#user-navigation-control}

이제 워크플로우 관리자는 사용자가 자신의 역할에 따라 제한된 모드에서 AEM에서 작동하도록 할 수 있습니다. 관리자는 헤더에서 사용할 수 있는 탐색 옵션의 표시를 제어하여 사용자가 워크플로우 작성 모드 또는 다른 솔루션 링크로 전환하도록 제한할 수 있습니다.

보기 선택기 > **[!UICONTROL 관리 컨트롤에서 새로운 내비게이션 옵션]** 숨기기를 **[!UICONTROL 확인하십시오]**.

이 기능에 대한 자세한 내용은 받은 편지함을 [참조하십시오](../sites-authoring/inbox.md).

### HTML5 양식의 다양한 텍스트 지원 {#rich-text-support}

이제 텍스트 필드에 렌더링된 HTML5 양식에 서식 옵션 목록이 표시됩니다. 필드에 적절한 설정을 적용하려면 양식 디자이너에서 텍스트 필드의 형식을 정의해야 합니다.

이 기능을 사용하려면 양식 디자이너의 디자인 **[!UICONTROL 보기에서 텍스트]** 필드를 누릅니다. 필드 **[!UICONTROL 탭의]** 필드 **[!UICONTROL 형식]** 드롭다운 목록에서 **[!UICONTROL 서식]** 텍스트를 선택하여설정을 적용합니다.

자세한 내용은 HTML5 [양식의](../forms/using/designing-form-template.md)양식 템플릿 디자인을 참조하십시오.

## 주요 특징

AEM 6.5 서비스 팩 4의 새로운 기능 외에도 다음과 같은 주요 내용이 포함되어 있습니다.

* 이제 선택적 컨텐츠 하위 트리를 Dynamic Media *- Scene7 모드로* 동기화할 수 있습니다(사용 가능한 모든 항목 `content/dam`).

* 이제 SOAP 웹 서비스와 양식 데이터 모델 통합을 통해 요소의 선택 그룹 또는 특성을 지원합니다.

* 이제 SOAP 입력 또는 출력 및 복잡한 데이터 구조가 동적 그룹 대체를 지원합니다.

## 이전 AEM 6.5 서비스 팩의 주요 기능

### 다이내믹 미디어를 위한 스마트 이미징 {#smart-imaging}

스마트 이미징은 각 사용자의 고유한 보기 특성을 활용하여 경험에 맞게 최적화된 이미지를 자동으로 제공하여 향상된 성능과 참여를 유도합니다. 스마트 이미징은 기존 이미지 사전 설정과 연동되며 전달 마지막 순간에 지능적인 기능을 사용하여 브라우저 또는 네트워크 연결 속도에 따라 이미지 파일 크기를 더욱 줄일 수 있습니다. 스마트 [이미징을 참조하십시오](../assets/imaging-faq.md).

### AEM 자산에 대한 시각적 검색 {#visual-search}

Assets 사용자는 시각적으로 유사한 이미지를 검색할 수 있습니다. AEM은 사용자가 선택한 이미지와 유사한 DAM 저장소에서 스마트 태그가 지정된 이미지를 표시합니다. See [Visual search](../assets/search-assets.md).

### 사용자의 받은 편지함 항목 공유 및 액세스 요청 {#share-request-access}

받은 편지함 항목을 다른 사용자와 공유할 수 있습니다. 다른 사용자가 받은 편지함 항목에 액세스할 수 있게 되면, 사용자는 공유 항목에 대해 해당 작업을 요청하고 수행할 수 있습니다. 마찬가지로 다른 사용자로부터 받은 편지함 항목에 대한 액세스를 요청할 수 있습니다. 사용자의 [받은 편지함 항목 공유 및 액세스 요청을](../forms/using/configure-shared-queues-osgi.md)참조하십시오.

### 받은 편지함 항목에 대한 부재 중 설정 구성 {#configure-out-of-office}

사무실 밖에 있을 계획인 경우 해당 기간 동안 사용자에게 할당된 항목에 대해 어떤 일이 일어나는지 지정할 수 있습니다.
시작 날짜, 시간, 종료 날짜 및 시간을 지정할 수 있습니다. 모든 항목을 보낼 기본 사람을 설정할 수 있습니다. Office [외 설정](../forms/using/configure-out-of-office-settings.md)구성을 참조하십시오.

### 일괄 처리 API를 사용하여 인터랙티브한 여러 커뮤니케이션 생성 {#generate-multiple-ic}

배치 API를 사용하여 템플릿에서 여러 대화형 통신을 생성할 수 있습니다. 템플릿은 데이터가 없는 대화형 통신입니다. 배치 API는 데이터를 템플릿과 결합하여 대화형 통신을 생성합니다. API는 인터랙티브한 커뮤니케이션의 대량 제작 시 유용합니다. 예를 들어, 전화 요금, 여러 고객을 위한 신용 카드 명세서 등이 있습니다. 배치 [API를 사용하여 여러 대화형 통신 생성을 참조하십시오](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

### 적응형 양식의 표준 유효성 검사 오류 메시지 {#standard-validation}

적응형 양식을 사용자 정의 서비스와 통합하여 데이터 유효성 검사를 수행할 수 있습니다. 입력 값이 유효성 검사 기준을 충족하지 않고 서버가 반환하는 유효성 검사 오류 메시지가 표준 메시지 형식이면 오류 메시지가 필드 수준에서 표시됩니다. 입력 값이 유효성 검사 기준을 충족하지 않고 서버 유효성 검사 오류 메시지가 표준 메시지 형식이 아닌 경우 적응형 양식은 유효성 검사 오류 메시지를 표준 형식으로 변환하여 양식의 필드 수준에서 표시할 수 있는 메커니즘을 제공합니다. 적응형 [양식에](../forms/using/standard-validation-error-messages-adaptive-forms.md)대한 표준 유효성 검사 오류 메시지를 참조하십시오.

## AEM 6.5 SP3 이후의 주요 릴리스

2019년 12월 12일부터 2020년 3월 5일 사이에 Adobe는 핵심 AEM 제공 서비스 이외의 다음 기능을 발표했습니다.

* AEM Cloud Manager 2020.1.0 및 2020.2.0Cloud Manager에 대한 월별 개선 사항, 파이프라인 상태 개선 및 다양한 단계에 대한 로그 다운로드 기능에 초점을 맞춘 지난 두 릴리스. 여기에서 전체 릴리스 정보를 참조하십시오.
   * [Cloud Manager 2020.1.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-1-0.html)

   * [Cloud Manager 2020.2.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)

* AEM Cloud Manager CLI 업데이트 명령줄 도구를 사용하여 Cloud Manager 작업을 자동화합니다. GitHub에 가입하여 CLI를 지속적으로 확장하고 [있습니다](https://github.com/adobe/aio-cli-plugin-cloudmanager/releases).

* AEM Sites:프로젝트 원형 23새 AEM 프로젝트를 시작하는 가장 좋은 방법입니다. Tranype 23을 [통해 SPA용 프로젝트 원형과 일반 사이트를 하나로](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-23)통합함으로써 프런트 엔드 개발을 시작하는 기본 테마를 제공합니다.

* AEM Sites:WKND 참조 사이트AEM을 사용하여 사이트를 구축하는 방법에 대한 모범 사례를 제공하는 [새로운 참조 프로젝트](https://www.wknd.site/) . 완전히 업데이트된 WKND 자습서를 [읽고 GitHub에서 코드를](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html) 캡처하여 자세한 내용을 [살펴보십시오](https://github.com/adobe/aem-guides-wknd/releases).

* AEM Sites:Commerce CIF Core Components 0.7.0 및 0.9.0AEM Sites 및 Magento Commerce 통합. Macromedia는 상거래에 초점을 맞춰 전용 코어 구성 요소 및 프로젝트 [원형형을 지속적으로 확장하고 있습니다](https://github.com/adobe/aem-core-cif-components/releases).

* AEM 자산:데스크탑 앱 2.0.1.1
   [데스크탑에서 에셋에 액세스](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html)

* AEM Screens:Feature Pack 202001AEM 내에서 직접 디지털 서명 최신 Feature Pack을 사용하면 향상된 최신 기능을 활용할 수 있습니다. 이번에는 여러 미디어 플레이어에서 [동기 재생을](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202001.html)활성화할 수 있습니다.

## 유용한 리소스

* [AEM 6.5 사용자 안내서](../user-guide/capabilities.md)

* [Adobe Experience Manager 6.5의 일반적인 릴리스 노트](release-notes.md)

* [Adobe Experience Manager 6.5용 서비스 팩 릴리스 노트](sp-release-notes.md)
