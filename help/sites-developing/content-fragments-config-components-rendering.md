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
exl-id: 9ef9ae75-cd8c-4adb-9bcb-e951d200d492
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 9%

---

# 컨텐츠 조각 렌더링용 구성 요소 구성{#content-fragments-configuring-components-for-rendering}

컨텐츠 조각 렌더링과 관련된 몇 가지 [고급 서비스](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration)가 있습니다. 이러한 서비스를 사용하려면 이러한 구성 요소의 리소스 유형이 컨텐츠 조각 프레임워크에 알려져야 합니다.

이 작업은 [OSGi 서비스 - 컨텐츠 조각 구성 요소 구성](#osgi-service-content-fragment-component-configuration)을 구성하여 수행합니다.

>[!CAUTION]
>
>아래 설명된 [고급 서비스](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration)가 필요하지 않으면 이 구성을 무시할 수 있습니다.

>[!CAUTION]
>
>기본 구성 요소를 확장하거나 사용하는 경우에는 구성을 변경하지 않는 것이 좋습니다.

>[!CAUTION]
>
>고급 서비스 없이 컨텐츠 조각 API만 사용하는 구성 요소를 처음부터 작성할 수 있습니다. 그러나 이러한 경우 적절한 처리를 수행하기 위해 구성 요소를 개발해야 합니다.
>
>따라서 코어 구성 요소를 사용하는 것이 좋습니다.

## {#definition-of-advanced-services-that-need-configuration} 구성이 필요한 고급 서비스의 정의

구성 요소를 등록해야 하는 서비스는 다음과 같습니다.

* 게시 중 종속성을 올바르게 확인합니다(즉, 마지막 게시 이후 변경된 경우 조각과 모델을 페이지에 자동으로 게시할 수 있는지 확인합니다.).
* 전체 텍스트 검색에서 컨텐츠 조각을 지원합니다.
* *중간 컨텐츠의 관리/처리.*
* *혼합 미디어 자산의 관리/처리.*
* 참조된 조각에 대한 디스패처 플러시(조각을 포함하는 페이지가 다시 게시되는 경우).
* 단락 기반 렌더링 사용.

이러한 기능 중 하나 이상이 필요한 경우(일반적으로) 처음부터 새로 개발하는 대신 기본 기능을 사용하는 것이 더 쉽습니다.

## OSGi 서비스 - 컨텐츠 조각 구성 요소 구성 {#osgi-service-content-fragment-component-configuration}

구성은 OSGi 서비스 **컨텐츠 조각 구성 요소 구성**&#x200B;에 바인딩해야 합니다.

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>자세한 내용은 [OSGi](/help/sites-deploying/configuring-osgi.md) 구성 을 참조하십시오.

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
   <td>등록할 리소스 유형예<br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>참조 속성</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>조각에 대한 참조가 포함된 속성의 이름예<code>fragmentPath</code> 또는 <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>요소 속성</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>렌더링할 요소의 이름이 포함된 속성의 이름입니다.예<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>변화 속성</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>렌더링할 변형의 이름이 포함된 속성의 이름입니다.예<code>variationName</code></td>
  </tr>
 </tbody>
</table>

일부 기능(예: 단락 범위만 렌더링하려면)의 경우 다음과 같은 일부 규칙을 준수해야 합니다.

<table>
 <tbody>
  <tr>
   <td>속성 이름</td>
   <td>설명</td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p><em>단일 요소 렌더링 모드</em>에 있는 경우 출력할 단락의 범위를 정의하는 문자열 속성입니다.</p> <p>형식:</p>
    <ul>
     <li><code>1</code> 또는 <code>1-3</code> 또는 <code>1-3;6;7-8</code> 또는 <code>*-3;5-*</code></li>
     <li><code>paragraphScope</code>이 <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p><em>단일 요소 렌더링 모드</em>에 있는 경우 단락을 출력하는 방법을 정의하는 문자열 속성입니다.</p> <p>값:</p>
    <ul>
     <li><code>all</code> :모든 단락을 렌더링합니다.</li>
     <li><code>range</code> :에서 제공하는 단락 범위를 렌더링합니다. <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>제목(예: <code>h1</code>, <code>h2</code>, <code>h3</code>)이 단락(<code>true</code>)으로 계산되는지(<code>false</code>)가 계산되는지를 정의하는 부울 속성입니다</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>이 작업은 이후 6.5 이정표에서 변경될 수 있습니다.

## 예 {#example}

예를 들어, 다음 (기본 제공 AEM 인스턴스에서)을 참조하십시오.

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

여기에는 다음 항목이 포함되어 있습니다.

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```
