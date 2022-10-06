---
title: 고객을 위한 사용자 인터페이스 Recommendations
seo-title: User Interface Recommendations for Customers
description: 클래식 및 터치에 적합한 사용자 인터페이스와 관련된 권장 사항 목록입니다.
seo-description: A list of recommendations related to the classic and touch-optimized user interfaces.
uuid: 9ec2c9de-a79e-4f2c-a90f-b38ba9553e07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f06d4b6-7d30-4ebc-9c6a-3bb8607a9be8
docset: aem65
exl-id: 7b71119a-ff58-47c0-aeef-a705ed8c40e0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 2%

---

# 고객을 위한 사용자 인터페이스 Recommendations{#user-interface-recommendations-for-customers}

Adobe Experience Manager에는 통합 Experience Cloud UI(터치 지원 UI라고도 함)와 클래식 UI의 두 가지 UI가 포함되어 있습니다.

이 문서는 고객이 상황에 따라 사용할 UI를 선택할 수 있도록 안내하기 위한 것입니다.

관심 조건:

* **UI(또는 표준 UI)**
기술 미리 보기로서 5.6.0에서 도입되고 후속 릴리스에서 확장되는 최신 사용자 인터페이스. 이것은 터치 지원 UI 또는 터치 UI라고 하는 Adobe Experience Cloud에 대한 통합 사용자 경험을 기반으로 합니다.

* **클래식 UI**
2008년 CQ 5.1에서 도입된 ExtJS 기술을 기반으로 한 사용자 인터페이스입니다.

* **사이트 관리자**
사이트 계층 구조(이동, 활성화, 관리 참조)를 관리하고 새 페이지를 만드는 기능.

* **페이지 작성**
페이지 컨텐츠를 추가/편집하는 기능.

* **DAM/Assets 관리**
디지털 자산(이미지, 비디오, 문서, 다운로드 포함)을 관리하는 기능.

* **ContextHub**
방문자에 대한 정보를 집계하여 다양한 용도로 사용하는 기능입니다. 사이트를 방문하는 사람을 시뮬레이션할 사용자 인터페이스를 제공합니다. AEM 6.2부터 ContextHub가 이전 기술인 Client Context를 대체했습니다.

## 일반 {#general}

지난 몇 년간 Adobe은 통합 사용자 인터페이스를 통해 모든 Adobe Experience Cloud 솔루션을 업데이트했습니다. Experience Cloud 솔루션 전체에서 사용자는 애플리케이션을 사용하고 운영하는 방법에 대한 일반적인 패턴으로 일관된 경험을 제공합니다. 릴리스마다 Adobe은 다양한 솔루션에서 일하는 고객의 피드백을 기반으로 UI의 사용자 인터페이스를 개선했습니다.

2008년에 도입되어 버전 5.0-5.6.1을 실행하는 고객이 사용하는 Adobe Experience Manager의 원래 사용자 인터페이스(이전 이름 CQ5)가 AEM 6.5에 있습니다. 따라서 고객은 동일한 사용자 인터페이스를 사용하여 6.5로 업데이트할 수 있고 새로운 기능이 있는 업데이트된 플랫폼의 이점을 누릴 수 있습니다.

Adobe은 고객이 2018/19에서 새 UI로 전환할 것을 권장합니다. 이 작업은 6.5로 업데이트하는 동안 수행할 수 있으며, 업데이트 후 별도의 프로젝트에서 수행할 수 있습니다. 이 작업에는 사용자 지정 및 구성 요소 대화 상자에 필요한 조정이 포함됩니다.

클래식 UI는 AEM 6.4에서 더 이상 사용되지 않으며, Adobe은 클래식 UI를 추가로 개선할 계획이 없습니다. 클래식 UI가 더 이상 사용되지 않는 동안에도 계속 지원됩니다.

### 규칙 및 Recommendations {#rules-and-recommendations}

다음은 Adobe Experience Manager 6.5의 제품 관리 권장 사항 목록입니다.

<table>
 <tbody>
  <tr>
   <th>내 프로젝트...</th>
   <th>추천</th>
  </tr>
  <tr>
   <td>이제 Adobe Experience Manager을 사용하기 시작합니다.</td>
   <td>기본 UI를 사용합니다.</td>
  </tr>
  <tr>
   <td><p>AEM을 잠시 사용했습니다.</p> <p>에서 해당 사이트에 대해 제품 UI를 기본적으로 사용하고 개발된 사용자 지정 구성 요소를 사용했습니다.<br /> </p> </td>
   <td>
    <ol>
     <li>6.5로 업데이트</li>
     <li>사이트 관리, 자산, UI에 기본 UI를 사용합니다. 등<br /> </li>
     <li>클래식 UI 페이지 편집기를 열려면 "페이지 편집" 작업을 구성합니다. 자세한 내용은 <a href="#selecting-your-ui">UI 선택</a>.</li>
    </ol> <p>그런 다음 두 번째 단계에서</p>
    <ol>
     <li>구성 요소 대화 상자를 업데이트하여 Coral 3 대화 상자 형식을 사용합니다. Adobe은 <a href="/help/sites-developing/modernization-tools.md">AEM 현대화 도구</a> 구성 요소를 업데이트하려면</li>
    </ol> </td>
  </tr>
  <tr>
   <td>통합과 함께 ClientContext을 사용하는 사이트를 빌드했습니다.<br /> </td>
   <td>
    <ol>
     <li>6.5로 업데이트</li>
     <li>사이트 관리, 자산, UI에 기본 UI를 사용합니다. 등</li>
     <li>클래식 UI 페이지 편집기를 열려면 "페이지 편집" 작업을 구성합니다. 자세한 내용은 <a href="#selecting-your-ui">UI 선택</a>.</li>
    </ol> <p>그런 다음 두 번째 단계에서</p>
    <ol>
     <li>구성 요소 대화 상자를 업데이트하여 Coral 3 대화 상자 형식을 사용합니다. Adobe은 <a href="/help/sites-developing/modernization-tools.md">AEM 현대화 도구</a> 구성 요소를 업데이트하려면</li>
     <li>ContextHub(ClientContext 대체)를 구성하고 ContextHub를 사용하도록 페이지 템플릿을 업데이트합니다. ContextHub에는 사용자 지정 ClientContext 저장소를 로드할 수 있는 호환성 모드가 있습니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>여러 해 동안 CQ/AEM을 사용해 왔습니다.</p> <p>광범위한 편집 대화 상자로 제품 UI(예: 사이트 관리자) 및 구성 요소를 확장했습니다.</p> </td>
   <td><p>6.5로 업데이트하고 모든 사용자에 대한 페이지 작성을 위한 기본값으로 클래식 UI를 구성합니다. 자세한 내용은 <a href="#selecting-your-ui">UI 선택</a>.</p> <p>그런 다음 프로젝트를 시작하여 사용자 지정을 적용하고 Coral 3 형식으로 구성 요소 대화 상자를 최적화합니다. 자세한 내용은 <a href="#resources-to-help">도움말 리소스</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### FAQ {#faq}

기술 자료 문서를 참조하십시오. [Touch UI 작성 FAQ](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html), 세부 사항 클래식 UI의 사용 중단 예약에 대한 정보 포함.

### UI 선택 {#selecting-your-ui}

자세한 내용은 [UI 선택](/help/sites-authoring/select-ui.md) 필요에 따라 시스템 구성에 대한 정보를 제공합니다.

### 터치 지원 UI 상태 {#touch-enabled-ui-status}

AEM 6.5에서 터치 지원 UI에 대한 개선 사항에 대한 자세한 내용은 [새로운 기능](/help/release-notes/release-notes.md#what-s-new) 를 참조하십시오.

전체 개요는 [Touch UI 기능 상태](/help/release-notes/touch-ui-features-status.md) 페이지

### 도움말 리소스 {#resources-to-help}

기본 처리에 대한 배경 정보:

* [페이지 작성](/help/sites-authoring/page-authoring.md).

자세한 개발 정보는

* [터치 지원 UI 아키텍처](/help/sites-developing/touch-ui-concepts.md).
* 를 사용하십시오 [AEM 현대화 도구](/help/sites-developing/modernization-tools.md) 구성 요소 편집 대화 상자를 클래식 UI에서 터치 지원 UI로 변환하는 방법

* [터치 지원 UI의 구조](/help/sites-developing/touch-ui-structure.md).

* [터치 지원 UI에서 콘솔 사용자 지정](/help/sites-developing/customizing-consoles-touch.md) (샘플 코드 포함).

* [터치 지원 UI에서 페이지 작성 사용자 지정](/help/sites-developing/customizing-page-authoring-touch.md) (샘플 코드 포함).

* [터치 지원 사용자 지정에 대한 AEM Gem 세션](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html).
* [Granite UI 설명서](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).
