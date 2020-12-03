---
title: 컨텐츠 조각 렌더링용 구성 요소 구성
seo-title: 컨텐츠 조각 렌더링용 구성 요소 구성
description: 컨텐츠 조각 렌더링용 구성 요소 구성
seo-description: 컨텐츠 조각 렌더링용 구성 요소 구성
uuid: 3f5aaf36-e6a7-4a3c-b305-e35ebcc98d0d
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 2aef9048-9d6e-4f5d-b443-5e73f8066d76
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 9%

---


# 컨텐츠 조각 렌더링용 구성 요소 구성{#content-fragments-configuring-components-for-rendering}

콘텐츠 조각 렌더링과 관련된 [고급 서비스](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration)가 여러 개 있습니다. 이러한 서비스를 사용하려면 이러한 구성 요소의 리소스 유형이 컨텐츠 조각 프레임워크에 대해 알고 있어야 합니다.

이 작업은 [OSGi 서비스 - 컨텐츠 조각 구성 요소 구성](#osgi-service-content-fragment-component-configuration)을 구성하여 수행됩니다.

>[!CAUTION]
>
>아래에 설명된 [고급 서비스](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration)가 필요하지 않은 경우 이 구성을 무시할 수 있습니다.

>[!CAUTION]
>
>기본 구성 요소를 확장하거나 사용하는 경우 구성을 변경하지 않는 것이 좋습니다.

>[!CAUTION]
>
>컨텐츠 조각 API만 사용하는 구성 요소를 처음부터 작성할 수 있습니다(고급 서비스 없음). 그러나 이러한 경우 적절한 처리를 처리하도록 구성 요소를 개발해야 합니다.
>
>따라서 핵심 구성 요소를 사용하는 것이 좋습니다.

## {#definition-of-advanced-services-that-need-configuration} 구성이 필요한 고급 서비스의 정의

구성 요소를 등록해야 하는 서비스는 다음과 같습니다.

* 게시 중에 올바르게 종속성 결정(즉, 조각 및 모델이 마지막 게시 이후 변경된 경우 페이지와 함께 자동으로 게시되도록 확인).
* 전체 텍스트 검색에서 컨텐츠 조각 지원.
* *중간 컨텐츠의 관리/처리.*
* *혼합 미디어 자산의 관리/처리.*
* 참조된 조각에 대한 디스패처가 플러시됩니다(조각을 포함하는 페이지가 다시 게시되는 경우).
* 단락 기반 렌더링 사용

이러한 기능 중 하나 이상이 필요한 경우(일반적으로) 처음부터 새로 개발하는 대신 기본 기능을 사용하는 것이 더 쉽습니다.

## OSGi 서비스 - 컨텐츠 조각 구성 요소 구성 {#osgi-service-content-fragment-component-configuration}

구성은 OSGi 서비스 **컨텐츠 조각 구성 요소 구성**&#x200B;에 바인딩되어야 합니다.

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>자세한 내용은 [OSGi](/help/sites-deploying/configuring-osgi.md) 구성을 참조하십시오.

예:

![cfm-01](assets/cfm-01.png)

OSGi 구성은 다음과 같습니다.

<table>
 <tbody>
  <tr>
   <td>레이블</td>
   <td>OSGi 구성<br /> </td>
   <td>설명</td>
  </tr>
  <tr>
   <td><strong>리소스 유형</strong></td>
   <td><code>dam.cfm.component.resourceType</code></td>
   <td>등록할 리소스 유형;예:<br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>참조 속성</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>조각에 대한 참조를 포함하는 속성의 이름예:<code>fragmentPath</code> 또는 <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>요소 속성</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>렌더링할 요소의 이름이 들어 있는 속성의 이름입니다.예:<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>변화 속성</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>렌더링할 변형의 이름이 포함된 속성의 이름입니다.예:<code>variationName</code></td>
  </tr>
 </tbody>
</table>

일부 기능(예: 단락 범위만 렌더링하려면)의 경우 다음 규칙을 준수해야 합니다.

<table>
 <tbody>
  <tr>
   <td>속성 이름</td>
   <td>설명</td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p><em>단일 요소 렌더링 모드</em>인 경우 출력할 단락 범위를 정의하는 문자열 속성입니다.</p> <p>형식:</p>
    <ul>
     <li><code>1</code> 또는 <code>1-3</code> 또는 <code>1-3;6;7-8</code> 또는 <code>*-3;5-*</code></li>
     <li><code>paragraphScope</code>이(가) <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p><em>단일 요소 렌더링 모드</em>에 있을 경우 단락을 출력하는 방법을 정의하는 문자열 속성입니다.</p> <p>값:</p>
    <ul>
     <li><code>all</code> :모든 단락을 렌더링합니다.</li>
     <li><code>range</code> :를 사용하여 <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>머리글(예: <code>h1</code>, <code>h2</code>, <code>h3</code>)이 단락(<code>true</code>)으로 계산되거나(<code>false</code>)으로 계산되지 않으면 정의하는 부울 속성입니다.</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>이후 6.5 마일스톤에서 변경될 수 있습니다.

## 예 {#example}

예를 들어, 다음(기본 AEM 인스턴스에서)을 참조하십시오.

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

여기에는 다음이 포함됩니다.

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```

