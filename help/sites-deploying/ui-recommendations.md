---
title: 고객을 위한 사용자 인터페이스 권장 사항
description: 클래식 및 터치에 적합한 사용자 인터페이스와 관련된 권장 사항 목록입니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
docset: aem65
exl-id: 7b71119a-ff58-47c0-aeef-a705ed8c40e0
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 8f638eb384bdca59fb6f4f8990643e64f34622ce
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---

# 고객을 위한 사용자 인터페이스 권장 사항{#user-interface-recommendations-for-customers}

Adobe Experience Manager에는 통합 Experience Cloud UI(터치 지원 UI라고도 함)와 클래식 UI의 두 가지 UI가 제공됩니다.

이 문서는 고객이 상황에 따라 사용할 UI를 선택할 수 있도록 안내하기 위한 것입니다.

관심 약관:

* **UI(또는 표준 UI)**
5.6.0에서 기술 미리 보기로 도입되고 후속 릴리스에서 확장된 최신 사용자 인터페이스입니다. 이는 이전에 터치 지원 UI 또는 터치 UI로 알려졌던 Adobe Experience Cloud에 대한 통합 사용자 경험을 기반으로 합니다.

* **클래식 UI**
2008년 CQ 5.1과 함께 도입된 ExtJS 기술을 기반으로 한 사용자 인터페이스입니다.

* **사이트 관리자**
사이트 계층 구조(이동, 활성화, 관리되는 참조)를 관리하고 새 페이지를 만드는 기능입니다.

* **페이지 작성**
페이지 콘텐츠를 추가/편집하는 기능입니다.

* **DAM/Assets 관리자**
디지털 에셋(이미지, 비디오, 문서, 다운로드 포함)을 관리하는 기능입니다.

* **ContextHub**
방문자에 대한 정보를 집계하여 다양한 용도로 사용하는 기능입니다. 사이트를 방문하는 사용자를 시뮬레이션할 수 있는 사용자 인터페이스를 제공합니다. AEM 6.2부터 ContextHub는 이전 기술인 Client Context를 대체했습니다.

## 일반 {#general}

지난 몇 년 동안 Adobe은 통합 사용자 인터페이스로 모든 Adobe Experience Cloud 솔루션을 업데이트했습니다. Experience Cloud 솔루션 전반의 사용자는 애플리케이션 사용 및 운영 방법에 대한 일반적인 패턴을 통해 일관된 경험을 누릴 수 있습니다. Adobe은 릴리스가 나올 때마다 다양한 솔루션에서 작업 중인 고객의 피드백을 기반으로 사용자 인터페이스를 개선했습니다.

2008년에 출시되고 버전 5.0-5.6.1을 실행하는 고객이 사용하는 Adobe Experience Manager(이전 이름: CQ5)의 원래 사용자 인터페이스는 AEM 6.5에 있습니다. 이를 통해 고객은 6.5로 업데이트할 수 있으며 동일한 사용자 인터페이스를 계속 사용하면서도 새로운 기능을 갖춘 업데이트된 플랫폼의 이점을 누릴 수 있습니다.

Adobe은 2018/19에 새로운 UI로 전환할 것을 권장합니다. 이 작업은 6.5로 업데이트하는 동안 또는 업데이트 후 별도의 프로젝트에서 수행할 수 있으며, 여기에는 사용자 지정 및 구성 요소 대화 상자에 필요한 조정이 포함됩니다.

클래식 UI는 AEM 6.4에서 더 이상 사용되지 않으며, Adobe은 클래식 UI를 더 이상 개선할 계획이 없습니다. 클래식 UI는 더 이상 사용되지 않는 동안 완전히 지원됩니다.

### 규칙 및 권장 사항 {#rules-and-recommendations}

다음은 Adobe Experience Manager 6.5용 제품 관리의 권장 사항 목록입니다.

<table>
 <tbody>
  <tr>
   <th>내 프로젝트...</th>
   <th>권장 사항</th>
  </tr>
  <tr>
   <td>Adobe Experience Manager을 사용하기 시작했습니다.</td>
   <td>기본 UI를 사용합니다.</td>
  </tr>
  <tr>
   <td><p>이(가) 한동안 AEM을 사용했습니다.</p> <p>이(가) 제품 UI를 즉시 사용하고 사이트에 대한 사용자 지정 구성 요소를 개발했습니다.<br /> </p> </td>
   <td>
    <ol>
     <li>6.5로 업데이트</li>
     <li>사이트 관리, 에셋 등에 기본 UI를 사용합니다. 등<br /> </li>
     <li>클래식 UI 페이지 편집기를 열려면 "페이지 편집" 작업을 구성하십시오. <a href="#selecting-your-ui">내 UI 선택</a>을 참조하세요.</li>
    </ol> <p>그런 다음 두 번째 단계에서:</p>
    <ol>
     <li>코랄 3 대화 상자 형식을 사용하도록 구성 요소 대화 상자를 업데이트합니다. Adobe에서는 <a href="/help/sites-developing/modernization-tools.md">AEM 현대화 도구</a>를 사용하여 구성 요소를 업데이트할 것을 권장합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>이(가) ClientContext과 통합을 사용하는 사이트를 빌드했습니다.<br /> </td>
   <td>
    <ol>
     <li>6.5로 업데이트</li>
     <li>사이트 관리, 에셋 등에 기본 UI를 사용합니다. 등</li>
     <li>클래식 UI 페이지 편집기를 열려면 "페이지 편집" 작업을 구성하십시오. <a href="#selecting-your-ui">내 UI 선택</a>을 참조하세요.</li>
    </ol> <p>그런 다음 두 번째 단계에서:</p>
    <ol>
     <li>코랄 3 대화 상자 형식을 사용하도록 구성 요소 대화 상자를 업데이트합니다. Adobe에서는 <a href="/help/sites-developing/modernization-tools.md">AEM 현대화 도구</a>를 사용하여 구성 요소를 업데이트할 것을 권장합니다.</li>
     <li>ContextHub(ClientContext의 대체)를 구성하고 ContextHub를 사용하도록 페이지 템플릿을 업데이트합니다. ContextHub에는 사용자 지정 ClientContext 스토어를 로드할 수 있는 호환성 모드가 있습니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>은(는) 수년간 CQ/AEM을 사용했습니다.</p> <p>는 제품 UI를 확장했으며(예: 사이트 관리자) 광범위한 편집 대화 상자를 통해 구성 요소를 빌드했습니다.</p> </td>
   <td><p>6.5로 업데이트하고 모든 사용자의 페이지 작성에 대한 기본값으로 클래식 UI를 구성합니다. <a href="#selecting-your-ui">내 UI 선택</a>을 참조하세요.</p> <p>그런 다음 프로젝트를 시작하여 맞춤화를 적용하고 구성 요소 대화 상자를 코랄 3 형식으로 최적화합니다. <a href="#resources-to-help">도움이 될 리소스</a>.<br />를 참조하세요. </p> </td>
  </tr>
 </tbody>
</table>

### UI 선택 {#selecting-your-ui}

필요에 따라 시스템을 구성하는 방법은 [UI 선택](/help/sites-authoring/select-ui.md)을 참조하십시오.

### 터치 지원 UI 상태 {#touch-enabled-ui-status}

AEM 6.5에서 터치 사용 UI에 향상된 기능에 대한 자세한 내용은 릴리스 정보에서 [새로운 기능](/help/release-notes/release-notes.md#what-s-new)을 참조하십시오.

전체 개요는 [Touch UI 기능 상태](/help/release-notes/touch-ui-features-status.md) 페이지를 참조하십시오.

### 도움말 리소스 {#resources-to-help}

기본 처리에 대한 배경 정보:

* [페이지 작성](/help/sites-authoring/page-authoring.md).

자세한 개발 정보는 다음을 참조하십시오.

* [터치 사용 UI 아키텍처](/help/sites-developing/touch-ui-concepts.md).
* [AEM 현대화 도구](/help/sites-developing/modernization-tools.md)를 사용하여 구성 요소 편집 대화 상자를 클래식 UI에서 터치 사용 UI로 변환합니다.

* [터치 사용 UI 구조](/help/sites-developing/touch-ui-structure.md).

* [터치 사용 UI에서 콘솔 사용자 지정](/help/sites-developing/customizing-consoles-touch.md)(샘플 코드 포함).

* [터치 사용 UI에서 페이지 작성 사용자 지정](/help/sites-developing/customizing-page-authoring-touch.md)(샘플 코드 포함).

* [Granite UI 설명서](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).
