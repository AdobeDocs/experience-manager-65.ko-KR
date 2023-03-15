---
title: 터치 UI로 마이그레이션
seo-title: Migration to the Touch UI
description: 터치 UI로 마이그레이션
seo-description: Migration to the Touch UI
uuid: 47c43b56-532b-4ada-8503-04d66bab3564
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: b315720f-e9b8-4063-99e2-1b9aa6bba460
docset: aem65
exl-id: 33dc1ee7-1e34-43d8-9265-c66535f5e002
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 10%

---

# 터치 UI로 마이그레이션{#migration-to-the-touch-ui}

버전 6.0부터 Adobe Experience Manager(AEM)에 다음과 같은 새로운 사용자 인터페이스가 도입되었습니다. *터치 지원 UI* (간단히 다음과 같이 알려짐) *touch UI*). Adobe Marketing Cloud 및 전체 Adobe 사용자 인터페이스 지침에 맞게 조정됩니다. 이 UI는 이라는 레거시 데스크탑 기반 인터페이스를 사용하는 AEM의 표준 UI가 되었습니다. *클래식 UI*.

클래식 UI가 있는 AEM을 사용하고 있는 경우 인스턴스를 마이그레이션하기 위한 조치를 취해야 합니다. 이 페이지는 개별 리소스에 대한 링크를 제공하여 발판 역할을 하기 위한 것입니다.

>[!NOTE]
>
>이러한 마이그레이션 프로젝트는 인스턴스에 중요한 영향을 줄 수 있습니다. 다음을 참조하십시오 [프로젝트 관리 - 우수 사례](/help/managing/best-practices.md) 을 참조하십시오.

## 기본 사항 {#the-basics}

마이그레이션할 때 클래식 UI와 Touch UI의 다음(주요) 차이점에 유의해야 합니다.

<table>
 <tbody>
  <tr>
   <td>클래식 UI</td>
   <td>터치 활성화 UI</td>
  </tr>
  <tr>
   <td>는 JCR 저장소에 노드 구조로 설명되어 있습니다. UI의 요소를 나타내는 모든 노드를 라고 합니다. <em>ExtJS 위젯</em> 클라이언트측에서 렌더링한 <code>ExtJS</code>.</td>
   <td>JCR 저장소에서도 노드 구조로 설명됩니다. 단, 이 경우 모든 노드는 렌더링을 담당하는 Sling 리소스 유형(Sling 구성 요소)을 참조합니다. 따라서 UI는 (기본적으로) 서버측에서 렌더링됩니다.</td>
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
     <li>명령형 부품은 리스너를 사용하여 직접 포함되거나 clientlibs에서 관리됩니다.</li>
    </ul> </td>
   <td><p>Javascript 위치:</p>
    <ul>
     <li>필수 부분은 대화 상자 정의, 즉 책임 분리에 포함될 수 없습니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>이벤트 처리:</p>
    <ul>
     <li>대화 상자 위젯은 Javascript 코드를 직접 참조합니다.</li>
    </ul> </td>
   <td><p>이벤트 처리:</p>
    <ul>
     <li>Javascript는 대화 상자 이벤트를 관찰합니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>클라이언트가 수행한 렌더링:
    <ul>
     <li>클라이언트가 동적으로 UI 구성 요소를 만듭니다.</li>
     <li>서버에서 (JSON으로) 클라이언트 요청 (풀) 구성 요소 정의.</li>
    </ul> </td>
   <td>서버에서 수행한 렌더링:
    <ul>
     <li>클라이언트가 관련 UI와 함께 페이지를 요청합니다.</li>
     <li>서버는 Coral UI 구성 요소를 사용하여 UI를 HTML 문서로 전송(푸시)합니다.<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

즉, 클래식 UI에서 Touch UI로 UI 섹션을 마이그레이션하는 것은 *ExtJS 위젯* (으)로 *Sling 구성 요소*. 이를 쉽게 하기 위해 터치 UI는 UI에 대한 일부 Sling 구성 요소(Granite UI 구성 요소라고 함)를 이미 제공하고 있는 Granite UI 프레임워크를 기반으로 합니다.

시작하기 전에 상태 및 관련 권장 사항을 확인하십시오.

* [Touch UI 기능 상태](/help/release-notes/touch-ui-features-status.md)
* [고객을 위한 사용자 인터페이스 Recommendations](/help/sites-deploying/ui-recommendations.md)

Touch UI 개발의 기본 사항은 견고한 기반을 제공합니다.

* [AEM 터치 지원 UI의 개념](/help/sites-developing/touch-ui-concepts.md)
* [AEM 터치 지원 UI의 구조](/help/sites-developing/touch-ui-structure.md)

## 페이지 작성 마이그레이션 {#migrating-page-authoring}

대화 상자는 구성 요소 마이그레이션 시 중요한 요소입니다.

* [AEM 구성 요소 개발](/help/sites-developing/developing-components.md) (터치 지원 UI 사용)
* [클래식 구성 요소에서 마이그레이션](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [AEM 현대화 도구](/help/sites-developing/modernization-tools.md) - 클래식 UI 구성 요소의 대화 상자를 touch UI로 변환하는 데 도움이 됩니다.

   * Touch UI에는 &quot;Touch UI 래퍼&quot; 내에서 클래식 UI 대화 상자를 여는 호환성 레이어가 있지만, 이 기능은 제한적이며 장기적으로는 권장되지 않습니다.

* [Touch UI에서 대화 상자 필드 맞춤화](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [새로운 Granite UI 필드 구성 요소 만들기](/help/sites-developing/granite-ui-component.md)
* [페이지 작성 사용자 지정](/help/sites-developing/customizing-page-authoring-touch.md) (터치 지원 UI 사용)

## 콘솔 마이그레이션 {#migrating-consoles}

콘솔을 구성할 수도 있습니다.

* [콘솔 사용자 지정](/help/sites-developing/customizing-consoles-touch.md) (터치 지원 UI의 경우)

## 관련 고려 사항 {#related-considerations}

Touch UI로의 마이그레이션과 직접 관련이 없지만, 권장되는 연습 방법이므로 동시에 고려할 만한 관련 문제가 있습니다.

* [템플릿](/help/sites-developing/templates.md) - [편집 가능한 템플릿](/help/sites-developing/page-templates-editable.md)
* [코어 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
* [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)

>[!NOTE]
>
>참조: [개발 - 우수 사례](/help/sites-developing/best-practices.md).

## 추가 리소스 {#further-resources}

AEM 개발에 대한 전체 정보는 아래의 리소스 컬렉션을 참조하십시오.

* [개발 사용 안내서](/help/sites-developing/home.md)
* [Granite UI 설명서](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [AEM 6.5 Sites Tutorials 및 비디오](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/overview.html)
* [AEM Sites 개발 시작하기 - WKND 튜토리얼](/help/sites-developing/getting-started.md)
* [AEM Gems](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html)
* [AEM 현대화 도구](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>AEM 현대화 도구는 커뮤니티 활동으로, Adobe이 지원하거나 보증하지 않습니다.
