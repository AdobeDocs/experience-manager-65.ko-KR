---
title: 고객을 위한 사용자 인터페이스 권장 사항
seo-title: 고객을 위한 사용자 인터페이스 권장 사항
description: 클래식 및 터치에 적합한 사용자 인터페이스와 관련된 권장 사항 목록입니다.
seo-description: 클래식 및 터치에 적합한 사용자 인터페이스와 관련된 권장 사항 목록입니다.
uuid: 9ec2c9de-a79e-4f2c-a90f-b38ba9553e07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f06d4b6-7d30-4ebc-9c6a-3bb8607a9be8
docset: aem65
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c

---


# 고객을 위한 사용자 인터페이스 권장 사항{#user-interface-recommendations-for-customers}

Adobe Experience Manager에는 통합된 Experience Cloud UI(터치 지원 UI라고도 함)와 클래식 UI가 포함되어 있습니다.

이 문서는 고객이 상황에 따라 사용할 UI를 선택할 수 있도록 하기 위한 것입니다.

관심 조건:

* **UI(또는 표준 UI)**&#x200B;기술 미리 보기로서 5.6.0에서 도입되고 이후 릴리스에서 확장되었던 최신 사용자 인터페이스입니다. Adobe Experience Cloud의 통합 사용자 환경을 기반으로 하며, 이전에 터치 지원 UI 또는 터치 UI로 알려져 있습니다.

* **2008**&#x200B;년 CQ 5.1에서 소개된 ExtJS 기술을 기반으로 하는 클래식 UI 사용자 인터페이스.

* **사이트**&#x200B;관리 기능을 사용하여 사이트 계층 구조(이동, 활성화, 관리 참조)를 관리하고 새 페이지를 만들 수 있습니다.

* **페이지**&#x200B;작성 기능을 사용하여 페이지의 컨텐츠를 추가/편집합니다.

* **DAM/Assets**&#x200B;디지털 자산(이미지, 비디오, 문서, 다운로드 포함)을 관리하는 기능

* **ContextHub**&#x200B;기능을 사용하여 방문자에 대한 정보를 집계하고 다양한 용도로 사용할 수 있습니다. 사이트를 방문하는 사람을 시뮬레이션하기 위한 사용자 인터페이스를 제공합니다. AEM 6.2를 시작하면 ContextHub이 이전 기술인 Client Context를 대체했습니다.

## 일반 {#general}

지난 몇 년 동안 Adobe는 통합된 유저 인터페이스를 통해 모든 Adobe Experience Cloud 솔루션을 업데이트했습니다. Adobe Experience Cloud 솔루션 사용자에게는 애플리케이션 사용 및 운영 방법에 대한 일반적인 패턴이 지속적으로 제공됩니다. Adobe는 모든 릴리스를 통해 다양한 솔루션을 사용하는 고객의 의견을 바탕으로 유저 인터페이스를 개선했습니다.

2008년에 도입되어 버전 5.0-5.6.1을 실행하는 고객이 사용하는 Adobe Experience Manager(이전의 CQ5)의 원래 사용자 인터페이스는 AEM 6.5에 있습니다.따라서 고객은 6.5로 업데이트할 수 있으며, 동일한 유저 인터페이스를 계속 사용하면서 새로운 기능을 갖춘 업데이트된 플랫폼의 혜택을 받을 수 있습니다.

Adobe는 고객이 2018년/19년에 새로운 UI로 전환할 계획을 수립하는 것을 권장합니다. 이 작업은 6.5로 업데이트하는 동안 또는 업데이트 후 별도의 프로젝트에서 수행할 수 있습니다. 이 작업에는 사용자 지정 및 구성 요소 대화 상자에 필요한 조정 사항이 포함됩니다.

클래식 UI는 AEM 6.4에서 더 이상 사용되지 않으며, Adobe는 클래식 UI를 추가로 개선할 계획이 없습니다. 클래식 UI가 더 이상 사용되지 않는 동안에도 계속 지원됩니다.

### 규칙 및 권장 사항 {#rules-and-recommendations}

다음은 Adobe Experience Manager 6.5용 제품 관리의 추천 목록입니다.

<table>
 <tbody>
  <tr>
   <th>내 프로젝트...</th>
   <th>추천</th>
  </tr>
  <tr>
   <td>Adobe Experience Manager를 사용하기 시작합니다.</td>
   <td>기본 UI를 사용합니다.</td>
  </tr>
  <tr>
   <td><p>AEM을 잠시 사용했습니다.</p> <p>즉시 사용 가능한 제품 UI를 사용했으며 사이트에 대한 사용자 정의 구성 요소를 개발했습니다.<br /> </p> </td>
   <td>
    <ol>
     <li>6.5로 업데이트</li>
     <li>사이트 관리, 자산 등에 기본 UI 사용.. 등이 됩니다.<br /> </li>
     <li>"페이지 편집" 동작을 구성하여 클래식 UI 페이지 편집기를 엽니다. See <a href="#selecting-your-ui">Selecting Your UI</a>.</li>
    </ol> <p>그런 다음 두 번째 단계에서 다음을 수행합니다.</p>
    <ol>
     <li>구성 요소 대화 상자를 업데이트하여 Coral 3 대화 상자 형식을 사용합니다. Adobe에서는 대화 상자 변환 <a href="/help/sites-developing/dialog-conversion.md">도구를 사용하여</a> 구성 요소를 업데이트하는 것이 좋습니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>통합으로 ClientContext를 사용하는 사이트를 만들었습니다.<br /> </td>
   <td>
    <ol>
     <li>6.5로 업데이트</li>
     <li>사이트 관리, 자산 등에 기본 UI 사용.. 등이 됩니다.</li>
     <li>"페이지 편집" 동작을 구성하여 클래식 UI 페이지 편집기를 엽니다. See <a href="#selecting-your-ui">Selecting Your UI</a>.</li>
    </ol> <p>그런 다음 두 번째 단계에서 다음을 수행합니다.</p>
    <ol>
     <li>구성 요소 대화 상자를 업데이트하여 Coral 3 대화 상자 형식을 사용합니다. Adobe에서는 대화 상자 변환 <a href="/help/sites-developing/dialog-conversion.md">도구를 사용하여</a> 구성 요소를 업데이트하는 것이 좋습니다.</li>
     <li>ContextHub(ClientContext 대체)을 구성하고 ContextHub를 사용하도록 페이지 템플릿을 업데이트합니다. ContextHub에는 사용자 지정 ClientContext 저장소를 로드할 수 있는 호환성 모드가 있습니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>수년 동안 CQ/AEM을 사용했습니다.</p> <p>확장된 편집 대화 상자를 사용하여 제품 UI(예: 사이트 관리자)와 구성 요소를 만들었습니다.</p> </td>
   <td><p>6.5로 업데이트하고 모든 사용자에 대한 페이지 작성의 기본값으로 클래식 UI를 구성합니다. See <a href="#selecting-your-ui">Selecting Your UI</a>.</p> <p>그런 다음 프로젝트를 시작하여 사용자 지정을 적용하고 구성 요소 대화 상자를 Coral 3 형식으로 최적화합니다. 도움말을 <a href="#resources-to-help">참조하십시오</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### FAQ {#faq}

자세한 내용은 기술 자료 문서, [Touch UI 작성](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html)FAQ를 참조하십시오.클래식 UI의 사용 중단 일정에 대한 정보를 포함합니다.

### Selecting Your UI {#selecting-your-ui}

필요에 [따라](/help/sites-authoring/select-ui.md) 시스템을 구성하는 방법은 UI 선택을 참조하십시오.

### 터치 지원 UI 상태 {#touch-enabled-ui-status}

AEM 6.5에서 터치 지원 UI에 대한 개선 사항에 대한 자세한 내용은 릴리스 [노트의 새로운](/help/release-notes/release-notes.md#what-s-new) 기능을 참조하십시오.

전체 개요는 Touch UI [기능 상태 페이지를](/help/release-notes/touch-ui-features-status.md) 참조하십시오

### 도움말 리소스 {#resources-to-help}

기본 처리에 대한 배경 정보:

* [페이지 작성](/help/sites-authoring/page-authoring.md).

자세한 개발 정보:

* [터치 지원 UI 아키텍처](/help/sites-developing/touch-ui-concepts.md).
* 대화 [상자 변환 도구를](/help/sites-developing/dialog-conversion.md) 사용하여 구성 요소 편집 대화 상자를 클래식 UI에서 터치 지원 UI로 변환합니다.

* [터치 지원 UI의 구조입니다](/help/sites-developing/touch-ui-structure.md).

* [터치 지원 UI에서 콘솔을 사용자](/help/sites-developing/customizing-consoles-touch.md) 지정합니다(샘플 코드 포함).

* [터치 지원 UI에서 페이지 작성 사용자](/help/sites-developing/customizing-page-authoring-touch.md) 지정(샘플 코드 포함)

* [터치 지원 사용자](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html)지정에 대한 AEM Gem 세션.
* [[MOCK] Granite UI documentation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).

