---
title: 터치 UI로 마이그레이션
seo-title: 터치 UI로 마이그레이션
description: 터치 UI로 마이그레이션
seo-description: 터치 UI로 마이그레이션
uuid: 47c43b56-532b-4ada-8503-04d66bab3564
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: b315720f-e9b8-4063-99e2-1b9aa6bba460
docset: aem65
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 13%

---


# 터치 UI로 마이그레이션{#migration-to-the-touch-ui}

버전 6.0부터 Adobe Experience Manager(AEM)은 *터치 지원 UI*(단순히 *터치 UI*&#x200B;라고도 함)라는 새로운 사용자 인터페이스를 도입했습니다. Adobe Marketing Cloud 및 전체 Adobe 사용자 인터페이스 지침에 따라 제공됩니다. 이것은 *클래식 UI*&#x200B;라고 하는 레거시 데스크톱 기반 인터페이스를 사용하는 AEM의 표준 UI가 되었습니다.

클래식 UI와 함께 AEM을 사용하고 있는 경우 인스턴스를 마이그레이션하기 위한 조치를 취해야 합니다. 이 페이지는 개별 리소스에 대한 링크를 제공하여 도약대 역할을 합니다.

>[!NOTE]
>
>이러한 마이그레이션 프로젝트는 인스턴스에 중요한 영향을 줄 수 있습니다. 권장 지침은 [프로젝트 관리 - 우수 사례](/help/managing/best-practices.md)를 참조하십시오.

## 기본 사항 {#the-basics}

마이그레이션할 때는 클래식 UI와 터치 UI의 다음(주요) 차이점을 알고 있어야 합니다.

<table>
 <tbody>
  <tr>
   <td>클래식 UI</td>
   <td>터치 활성화 UI</td>
  </tr>
  <tr>
   <td>JCR 저장소에 노드 구조로 설명되어 있습니다. UI의 요소를 나타내는 모든 노드를 <em>ExtJS 위젯</em>이라고 하며 <code>ExtJS</code>로 클라이언트측에서 렌더링합니다.</td>
   <td>JCR 저장소에 노드 구조로도 설명되어 있습니다. 그러나 이 경우 모든 노드가 렌더링을 담당하는 Sling 리소스 유형(Sling 구성 요소)을 참조합니다. 따라서 UI는 (기본적으로) 서버측에서 렌더링됩니다.</td>
  </tr>
  <tr>
   <td><p><code>sling:resourceType</code></p>
    <ul>
     <li>사용되지 않음</li>
    </ul> </td>
   <td><code>sling:resourceType</code>
    <ul>
     <li>사용됨</li>
     <li>예<br /> <code>cq/gui/components/authoring/dialog</code><br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>대화 상자 노드:</p>
    <ul>
     <li>이름: <code>dialog</code></li>
     <li>jcr:primaryType: <code>cq:Dialog</code></li>
    </ul> </td>
   <td><p>대화 상자 노드:</p>
    <ul>
     <li>이름: <code>cq:dialog</code></li>
     <li>jcr:primaryType: <code>nt:unstructured</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Javascript 위치:</p>
    <ul>
     <li>필수 부분은 리스너를 사용하여 직접 포함되거나 clientlibs에서 관리됩니다.</li>
    </ul> </td>
   <td><p>Javascript 위치:</p>
    <ul>
     <li>필수 부분은 대화 상자 정의에 포함할 수 없습니다.책임의 분리.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>이벤트 처리:</p>
    <ul>
     <li>대화 상자 위젯은 Javascript 코드를 직접 참조합니다.</li>
    </ul> </td>
   <td><p>이벤트 처리:</p>
    <ul>
     <li>Javascript는 대화 이벤트를 관찰합니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>클라이언트가 수행하는 렌더링:
    <ul>
     <li>클라이언트는 UI 구성 요소를 동적으로 만듭니다.</li>
     <li>서버에서 클라이언트 요청(가져오기) 구성 요소 정의(JSON)를 참조하십시오.</li>
    </ul> </td>
   <td>서버에서 렌더링 수행:
    <ul>
     <li>클라이언트는 관련 UI와 함께 페이지를 요청합니다.</li>
     <li>서버는 UI를 HTML 문서로 전송(푸시)합니다.Coral UI 구성 요소 사용<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

즉, UI의 섹션을 클래식 UI에서 터치 UI로 마이그레이션하는 것은 *ExtJS 위젯*&#x200B;을 *Sling 구성 요소*&#x200B;으로 포팅하는 것을 의미합니다. 이 작업을 쉽게 하기 위해 터치 UI는 UI에 대한 일부 Sling 구성 요소(예: [화강암 UI 구성 요소])를 이미 제공하는 [granite UI] 프레임워크를 기반으로 합니다.

시작하기 전에 상태 및 관련 권장 사항을 확인하십시오.

* [터치 UI 기능 상태](/help/release-notes/touch-ui-features-status.md)
* [고객을 위한 사용자 인터페이스 Recommendations](/help/sites-deploying/ui-recommendations.md)

터치 UI를 개발하기 위한 기본 사항은 견고한 기반을 제공합니다.

* [AEM 터치 지원 UI의 개념](/help/sites-developing/touch-ui-concepts.md)
* [AEM 터치 지원 UI의 구조](/help/sites-developing/touch-ui-structure.md)

## 페이지 작성 마이그레이션 {#migrating-page-authoring}

구성 요소를 마이그레이션할 때 대화 상자는 주요 요소입니다.

* [AEM 구성 요소](/help/sites-developing/developing-components.md)  개발(터치 지원 UI 사용)
* [클래식 구성 요소에서 마이그레이션](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [대화 상자 전환](/help/sites-developing/dialog-conversion.md)  도구 - 클래식 UI 구성 요소의 대화 상자를 터치 UI로 변환하는 데 도움이 됩니다.

   * 터치 UI에 &quot;터치 UI 래퍼&quot; 내에서 클래식 UI 대화 상자를 여는 호환성 레이어가 있지만 기능이 제한되어 있으므로 장기적으로 사용하지 않는 것이 좋습니다.

* [Touch UI에서 대화 상자 필드 사용자 정의](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [새로운 Granite UI 필드 구성 요소 만들기](/help/sites-developing/granite-ui-component.md)
* [페이지 작성 사용자](/help/sites-developing/customizing-page-authoring-touch.md)  지정(터치 지원 UI 사용)

## 콘솔 마이그레이션 {#migrating-consoles}

콘솔을 사용자 정의할 수도 있습니다.

* [콘솔 사용자](/help/sites-developing/customizing-consoles-touch.md)  지정(터치 지원 UI의 경우)

## 관련 고려 사항 {#related-considerations}

터치 UI로의 마이그레이션과 직접적으로 관련이 없지만, 동시에 고려할 가치가 있는 관련 문제가 있습니다. 이는 권장 사항이기도 합니다.

* [템플릿](/help/sites-developing/templates.md)  -  [편집 가능한 템플릿](/help/sites-developing/page-templates-editable.md)
* [코어 구성 요소](https://docs.adobe.com/content/help/ko-KR/experience-manager-core-components/using/introduction.html)
* [HTL](https://docs.adobe.com/content/help/ko-KR/experience-manager-htl/using/overview.html)

>[!NOTE]
>
>[개발 - 우수 사례](/help/sites-developing/best-practices.md)도 참조하십시오.

## 추가 리소스 {#further-resources}

AEM 개발에 대한 자세한 내용은

* [개발 사용 안내서](/help/sites-developing/home.md)
* [Granite UI 설명서](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [AEM 6.5 사이트 Tutorials 및 비디오](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/overview.html)
* [AEM Sites 개발 시작 - WKND 자습서](/help/sites-developing/getting-started.md)
* [AEM Gems](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html)
* [AEM 현대화 도구](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>AEM 현대화 툴은 커뮤니티 활동이며 Adobe에 의해 지원되거나 보증되지 않습니다.

