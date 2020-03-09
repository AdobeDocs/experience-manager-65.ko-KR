---
title: Adobe Experience Manager 6.5 서비스 팩 4의 새로운 기능
description: Adobe Experience Manager 6.5 서비스 팩 4의 새로운 기능
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 93521f102596a7f5cb247ddc430626d352338ce8

---


# Adobe Experience Manager 6.5 서비스 팩 4의 새로운 기능 {#aem-whats-new-service-pack-4}

2020년 Adobe Experience Manager(AEM) 6.5는 분기별 서비스 팩에 대한 기능과 지속적으로 향상된 기능을 제공합니다. 고객은 이러한 새로운 방식을 통해 혁신을 신속하게 채택할 수 있습니다.

최신 AEM 서비스 팩 4(6.5.4.0)는 2020년 **3월 5일에 릴리스됩니다**. 이 문서에서는 AEM 여정을 더욱 풍성하게 만들기 위한 최신 서비스 팩 기능을 소개합니다.

## AEM Sites {#aem-sites}

### 다양한 영역의 성능 개선 {#performance-improvements}

* 사이트(contexthub.kernel.js)에서 ContextHub를 로드하고 초기화하는 데 걸리는 시간이 단축되었습니다. 사이트 방문 중에 페이지를 더 빠르게 로드합니다.

* 페이지 편집기의 캔버스에서 경험 조각을 드래그 앤 드롭한 후 페이지를 새로 고치는 시간을 줄였습니다.

* Live Copy 개요에서 사이트에 Live Copy가 200개 이상 있을 때 항목을 로드하는 시간을 단축했습니다.

* 템플릿 편집기에서 템플릿 편집기의 속도가 느려질 수 있는 불완전하거나 잘못된 URL의 처리를 개선했습니다.

또한 AEM 6.5 SP4에는 스타일 시스템 개선 사항이 포함되어 있습니다. 이제 구성 요소 대화 상자 내에서 스타일을 선택할 수도 있습니다.


## AEM Assets {#aem-assets}

### Adobe I/O 콘솔을 통해 브랜드 포털과 통합 {#assets-integration-bp}

이제 AEM Assets는 Adobe I/O를 통해 브랜드 포털로 구성되어 브랜드 포털 임차인의 승인을 위해 IMS 토큰을 구매합니다. 이전에는 레거시 OAuth 게이트웨이를 통해 클래식 UI에서 구성되었습니다.

기존 OAuth와의 새로운 통합은 2020년 4월 6일 이후로 지원되지 않으며 Adobe I/O 콘솔로 전환하게 됩니다. 통합을 수정하지 않으면 기존 구성이 계속 작동합니다.

새 통합을 만들거나 통합 설정을 Adobe I/O 콘솔로 업그레이드할 수 있습니다.

### Accessibility enhancements {#accessibility-enhancements}

* 이제 혼합 상태 확인란에 &quot;혼합&quot; 값과 함께 아리아 체크 속성이 추가되어 화면 판독기에 표시됩니다.

* 이제 확대/축소된 이미지 주위로 이동하기 위한 패스 기반의 제스처와는 별도로 키보드 기반의 컨트롤이 지원됩니다.

* 날짜 형식 제한이 키보드 전용 사용자가 날짜를 수동으로 입력할 수 있도록 필드 레이블에 제공되었습니다.

* Alt 속성이 장식 아이콘에 추가되고 role=img 속성이 제거되었으므로 이러한 아이콘과 이미지가 화면 판독기 사용자에게 노출되지 않습니다.

* Alt 속성은 화면 판독기 사용자가 탭 위에 있을 때 표시할 아이콘을 닫기 위해 추가되었습니다.

## AEM 양식 {#aem-forms}

### AEM Forms 워크플로우에서 인쇄 가능한 출력 생성 {#generate-printable-output}

소스 템플릿 파일의 여러 복사본을 인쇄하여 여러 레코드가 있는 데이터 파일과 통합하려는 경우 AEM Forms에서 새로운 인쇄 가능한 출력 생성 워크플로우 단계를 사용할 수 있습니다. 예를 들어 인쇄 시 다른 이름으로 소스 양식을 인쇄하려면 데이터 파일에 해당 이름을 지정하여 표준 템플릿 파일과 통합할 수 있습니다.

도구 > 워크플로우 **>** 모델 **[!UICONTROL >]** 모델 **[!UICONTROL >]** 생성 ******[!UICONTROL 및 생성]** 인쇄를 위한 검색 생성인쇄 가능한 출력 생성 워크플로우 단계를 사용하여 이 기능을 활용할 수 있습니다.

![인쇄 가능한 출력 생성](assets/generate-print-output-demo.gif)

이 기능에 대한 자세한 내용은 OSGi - [Step Reference에서 양식 중심의 워크플로우를 참조하십시오](../forms/using/aem-forms-workflow-step-reference.md).

### 레이아웃 모드에서 적응형 양식 및 인터랙티브한 커뮤니케이션을 위한 다중 열 지원 {#multi-column-adaptive-forms}

이제 적응형 양식 및 인터랙티브한 커뮤니케이션에서 패널의 열 수를 정의할 수 있습니다.

레이아웃 모드로 전환하여 새 옵션을 찾을 수 있고, 다중 열 형식으로 변환할 패널을 누르고, 상위 항목을 선택하고, 다음 그림에 설명된 대로 다중 열 아이콘을 눌러 패널의 열 수를 정의할 수 있습니다.

![다중 열 레이아웃](assets/multi-column-layout.gif)

자세한 내용은 레이아웃 모드를 사용하여 구성 [요소의](../forms/using/resize-using-layout-mode.md)크기를 조정하십시오.

### AEM 받은 편지함 사용자 정의 {#aem-inbox}

AEM 헤더에서 사용할 수 있는 옵션을 사용자 정의해야 한다고 생각하십니까? 이제 새로운 서비스 팩 릴리스에 관리 제어 옵션이 도입되어 **[!UICONTROL 가능합니다]** .

**머리글 텍스트 사용자 지정**

이제 **워크플로우 관리자** 그룹에 속한 사용자는 맨 위에 있는 머리글 텍스트를 원하는 텍스트로 사용자 정의하여 기존 Adobe Experience Manager **[!UICONTROL 텍스트를 바꿀 수 있습니다]** .

보기 선택기(도구 모음의 오른쪽 **[!UICONTROL 상단에 있음) > 관리 제어에서 새로운 머리글 텍스트]** 사용자 지정 옵션을 찾을 **[!UICONTROL 수 있습니다]**.

**로고 사용자 정의**

머리글 텍스트 맞춤화와 마찬가지로 **워크플로우 관리자** 그룹에 속한 사용자는 원하는 로고로 맨 위에 있는 로고를 사용자 정의할 수 있습니다.

보기 선택기 > 관리 **[!UICONTROL 컨트롤에서]** 새로운 로고 사용자 지정 옵션을 찾을 수 **[!UICONTROL 있습니다]**.

이 기능에 대한 자세한 내용은 받은 편지함을 [참조하십시오](../sites-authoring/inbox.md).

### 사용자 탐색 제어 {#user-navigation-control}

워크플로우 관리자 **** 그룹에 속한 사용자는 자신의 역할에 따라 제한된 모드에서 사용자가 AEM에서 작동하도록 할 수 있습니다. 관리자는 헤더에서 사용할 수 있는 탐색 옵션의 표시를 제어하고 사용자가 워크플로우 작성 모드로 전환하도록 제한하거나 도움말 또는 기타 솔루션 링크로 이동할 수 있습니다.

보기 선택기 > **[!UICONTROL 관리 컨트롤에서 새로운 내비게이션 옵션]** 숨기기를 **[!UICONTROL 확인하십시오]**.

이 기능에 대한 자세한 내용은 받은 편지함을 [참조하십시오](../sites-authoring/inbox.md).

### HTML5 양식의 다양한 텍스트 지원 {#rich-text-support}

이제 텍스트 필드에 렌더링된 HTML5 양식에 서식 옵션 목록이 표시됩니다. 필드에 적절한 설정을 적용하려면 양식 디자이너에서 텍스트 필드의 필드 형식을 정의해야 합니다.

이 기능을 사용하려면 양식 디자이너의 디자인 **[!UICONTROL 보기에서 텍스트]** 필드를 누릅니다. 필드 **[!UICONTROL 탭의]** 필드 **[!UICONTROL 형식]** 드롭다운 목록에서 **[!UICONTROL 서식]** 텍스트를 선택하여설정을 적용합니다. 이제 텍스트 필드에 HTML5 형식으로 렌더링할 때 서식 옵션이 표시됩니다.

자세한 내용은 HTML5 [양식의](../forms/using/designing-form-template.md)양식 템플릿 디자인을 참조하십시오.

## 주요 특징

새로운 기능 외에도 AEM 6.5 서비스 팩 4에는 다음 주요 내용이 포함되어 있습니다.

* 이제 선택적 컨텐츠 하위 트리만 모든 하위 트리가 *아닌 Scene7 모드로* 동기화할 수 `content/dam`있습니다.

* 이제 SOAP 웹 서비스를 사용한 양식 데이터 모델 통합은 요소에 대한 선택 그룹 또는 특성을 지원합니다.

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

* AEM Sites:WKND 참조 사이트AEM을 사용하여 사이트를 구축하는 방법에 대한 모범 사례를 제공하는 [새로운 참조 프로젝트](https://www.wknd.site/) . 완전히 업데이트된 WKND 튜토리얼을 [](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html) 읽고 GitHub에서 코드를 [살펴보십시오](https://github.com/adobe/aem-guides-wknd/releases).

* AEM Sites:Commerce CIF Core Components 0.7.0 및 0.9.0AEM Sites 및 Magento Commerce 통합. Macromedia는 상거래에 초점을 맞춰 전용 코어 구성 요소 및 프로젝트 [원형형을 지속적으로 확장하고 있습니다](https://github.com/adobe/aem-core-cif-components/releases).

* AEM 자산:데스크탑 앱 2.0.1.1
   [데스크탑에서 에셋에 액세스](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html)

* AEM Screens:Feature Pack 202001AEM 내에서 직접 디지털 서명 최신 Feature Pack을 사용하면 향상된 최신 기능을 활용할 수 있습니다. 이번에는 여러 미디어 플레이어에서 [동기 재생을](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202001.html)활성화할 수 있습니다.

## 유용한 리소스

* [AEM 6.5 사용자 안내서](../user-guide/capabilities.md)

* [Adobe Experience Manager 6.5의 일반적인 릴리스 노트](release-notes.md)

* [Adobe Experience Manager 6.5용 서비스 팩 릴리스 노트](sp-release-notes.md)
