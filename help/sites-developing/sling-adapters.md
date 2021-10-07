---
title: Sling 어댑터 사용
seo-title: Using Sling Adapters
description: Sling은 어댑터 패턴을 제공하여 적응형 인터페이스를 구현하는 개체를 간편하게 번역합니다
seo-description: Sling offers an Adapter pattern to conveniently translate objects that implement the Adaptable interface
uuid: 07f66a33-072d-49e1-8e67-8b80a6a9072a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: c081b242-67e4-4820-9bd3-7e4495df459e
exl-id: 6465e2c4-28e5-4fc8-8cca-7b632f10ba5a
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '2318'
ht-degree: 13%

---

# Sling 어댑터 사용{#using-sling-adapters}

[](https://sling.apache.org) Slingoffers와  [어댑터 ](https://sling.apache.org/site/adapters.html) 패턴을 사용하여 Adaptableinterface를 구현하는 개체를 간편하게  [](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) 변환합니다. 이 인터페이스는 개체를 인수로 전달되는 클래스 형식으로 변환하는 제네릭 [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) 메서드를 제공합니다.

예를 들어 Resource 개체를 해당 Node 개체로 변환하려면 다음을 간단히 수행할 수 있습니다.

```java
Node node = resource.adaptTo(Node.class);
```

## 사용 사례 {#use-cases}

다음과 같은 사용 사례가 있습니다.

* 구현별 개체를 가져옵니다.

   예를 들어 일반 [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) 인터페이스의 JCR 기반 구현에서는 기본 JCR [`Node`](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html)에 액세스할 수 있습니다.

* 내부 컨텍스트 개체를 전달해야 하는 개체의 바로 가기 만들기

   예를 들어 JCR 기반 [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html)은 요청의 [`JCR Session`](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html)에 대한 참조를 보유하며, 이 참조는 [`PageManager`](https://helpx.adobe.com/kr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) 또는 [`UserManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html)과 같이 해당 요청 세션을 기반으로 작동하는 많은 개체에 필요합니다.

* 서비스에 대한 바로 가기.

   드문 경우입니다. `sling.getService()` 도 간단합니다.

### Null 반환 값 {#null-return-value}

`adaptTo()` null을 반환할 수 있습니다.

다음과 같은 여러 가지 이유가 있습니다.

* 구현은 target 유형을 지원하지 않습니다
* 이 케이스를 처리하는 어댑터 팩터리가 활성 상태가 아닙니다(예: 서비스 참조가 누락되어)
* 내부 조건이 실패했습니다.
* 서비스를 사용할 수 없습니다.

null 케이스를 적절하게 처리하는 것이 중요합니다. jsp 렌더링의 경우 컨텐츠가 비어 있는 경우 jsp에 오류가 발생할 수 있습니다.

### 캐싱 {#caching}

성능을 향상시키기 위해 구현은 `obj.adaptTo()` 호출에서 반환된 개체를 캐시할 수 있습니다. `obj` 이 동일하면 반환된 개체가 동일합니다.

이 캐싱은 모든 `AdapterFactory` 기반 사례에 대해 수행됩니다.

그러나 일반 규칙이 없습니다. 개체가 새 인스턴스이거나 기존 인스턴스일 수 있습니다. 즉, 두 동작에 의존할 수 없습니다. 따라서 이 시나리오에서는 특히 `AdapterFactory` 내에서 해당 개체가 다시 사용할 수 있는 것이 중요합니다.

### 작동 방법 {#how-it-works}

`Adaptable.adaptTo()`을 구현할 수 있는 방법에는 여러 가지가 있습니다.

* 개체 자체에 의해; 메서드 자체를 구현하고 특정 객체에 매핑합니다.
* 임의의 개체를 매핑할 수 있는 [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html)에 의해 결정됩니다.

   개체는 여전히 `Adaptable` 인터페이스를 구현해야 하며, [`SlingAdaptable`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/adapter/SlingAdaptable.html)(`adaptTo` 호출을 중앙 어댑터 관리자에 전달)를 확장해야 합니다.

   이렇게 하면 `Resource` 등의 기존 클래스에 대한 `adaptTo` 메커니즘에 후크를 사용할 수 있습니다.

* 둘 다 조합입니다.

첫 번째 경우 javadocs에 가능한 `adaptTo-targets`이 무엇인지 지정할 수 있습니다. 그러나 JCR 기반 리소스와 같은 특정 하위 클래스의 경우 이 작업이 불가능한 경우가 많습니다. 후자의 경우, `AdapterFactory` 구현은 일반적으로 번들의 개인 클래스의 일부이며, 따라서 클라이언트 API에 노출되거나 javadocs에 나열되지 않습니다. 이론적으로, [OSGi](/help/sites-deploying/configuring-osgi.md) 서비스 런타임에서 모든 `AdapterFactory` 구현에 액세스하여 &quot;adaptables&quot;(소스 및 타겟) 구성을 볼 수 있지만 서로 매핑하지는 않을 수 있습니다. 결국, 이것은 문서화되어야 하는 내부 논리에 따라 다릅니다. 따라서 이 참조는

## 참조 {#reference}

### 슬링 {#sling}

[****](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) 리소스는 다음과 같습니다.

<table>
 <tbody>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">노드</a></td>
   <td>JCR 노드 기반 리소스이거나 노드를 참조하는 JCR 속성입니다.</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">속성</a></td>
   <td>JCR 속성 기반 리소스인 경우.</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">항목</a></td>
   <td>JCR 기반 리소스(노드 또는 속성)인 경우</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api//java/util/Map.html">맵</a></td>
   <td>JCR 노드 기반 리소스(또는 기타 리소스 지원 값 맵)인 경우 속성 맵을 반환합니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>JCR 노드 기반 리소스(또는 기타 리소스 지원 값 맵)인 경우 속성의 사용하기 쉬운 맵을 반환합니다. <br /> <code><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceUtil.html#getvaluemap%28org.apache.sling.api.resource.resource%29">ResourceUtil.getValueMap(Resource)</a></code>(null 케이스 등을 처리)를 사용하여 (보다 간단하게) 구현할 수도 있습니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">상속 값 맵</a></td>
   <td>속성을 찾을 때 리소스 계층 구조를 고려할 수 있는 <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>의 확장입니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">수정 가능한 값 맵</a></td>
   <td>해당 노드의 속성을 수정할 수 있는 <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>의 확장입니다.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/InputStream.html">입력 스트림</a></td>
   <td>파일 리소스의 이진 컨텐츠 반환(JCR 노드 기반 리소스이고 노드 유형이 <code>nt:file</code> 또는 <code>nt:resource</code>;인 경우) 번들 리소스인 경우 파일 시스템 리소스인 경우 파일 컨텐츠나 바이너리 JCR 속성 리소스의 데이터입니다.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>리소스(JCR 노드 기반 리소스인 경우 이 노드의 저장소 URL)에 대한 URL을 반환합니다. 번들 리소스인 경우 jar 번들 URL 파일 시스템 리소스인 경우 파일 URL).</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/File.html">파일</a></td>
   <td>파일 시스템 리소스인 경우</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>이 리소스가 sling에 스크립트 엔진이 등록된 스크립트(예: jsp 파일)인 경우</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/products/servlet/2.2/javadoc/javax/servlet/Servlet.html">서블릿</a></td>
   <td>이 리소스가 sling에 스크립트 엔진이 등록되거나 서블릿 리소스인 스크립트(예: jsp 파일)인 경우</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Double.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html"></a><br /> <a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html">StringBooleanLongDoubleCalendarValueString[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html">부울[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html">Long[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html">달력[]</a><br /> <a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">값[]</a></td>
   <td>JCR 속성 기반 리소스인 경우 값을 반환합니다(및 값이 일치함).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>JCR 노드 기반 리소스인 경우</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html">페이지</a></td>
   <td>JCR 노드 기반 리소스이고 노드가 <code>cq:Page</code>(또는 <code>cq:PseudoPage</code>)인 경우</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html">구성 요소</a></td>
   <td><code>cq:Component</code> 노드 리소스인 경우</td>
  </tr>  
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Design.html">디자인</a></td>
   <td>디자인 노드인 경우(<code>cq:Page</code>).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html">템플릿</a></td>
   <td><code>cq:Template</code> 노드 리소스인 경우</td>
  </tr>  
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/Blueprint.html">블루프린트</a></td>
   <td><code>cq:Template</code> 노드 리소스인 경우</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Asset.html">자산</a></td>
   <td>dam:Asset 노드 리소스입니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Rendition.html">렌디션</a></td>
   <td>dam:Asset 렌디션인 경우 dam:Assert의 렌디션 폴더 아래에 nt:file</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/Tag.html">태그</a></td>
   <td><code>cq:Tag</code> 노드 리소스인 경우</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>JCR 기반 리소스이고 사용자가 UserManager에 액세스할 권한이 있는 경우 JCR 세션을 기반으로 합니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">승인 가능 대상</a></td>
   <td>Authorizable은 사용자 및 그룹의 공통 기본 인터페이스입니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">사용자</a></td>
   <td>사용자는 인증 및 가장할 수 있는 특별한 승인 가능 사용자입니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/SimpleSearch.html">SimpleSearch</a></td>
   <td>JCR 기반 리소스인 경우 리소스 아래에서 검색합니다(또는 setSearchIn()).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>지정된 페이지/워크플로우 페이로드 노드에 대한 워크플로우 상태입니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html">복제 상태</a></td>
   <td>지정된 리소스 또는 jcr:content 하위 노드에 대한 복제 상태(먼저 선택됨).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/connector/ConnectorResource.html">ConnectorResource</a></td>
   <td>JCR 노드 기반 리소스인 경우 특정 유형에 맞게 조정된 커넥터 리소스를 반환합니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">구성</a></td>
   <td><code>cq:ContentSyncConfig</code> 노드 리소스인 경우</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>이 값이 <code>cq:ContentSyncConfig</code> 노드 리소스 미만이면</td>
  </tr>
 </tbody>
</table>

[****](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceResolver.html) ResourceResolver는 다음 항목에 맞게 조정됩니다.

<table>
 <tbody>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">Session</a></td>
   <td>JCR 기반 리소스 확인자(기본값)인 경우 요청의 JCR 세션입니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">ComponentManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Designer.html">디자이너</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>JCR 기반 리소스 확인자인 경우 JCR 세션을 기반으로 합니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>JCR 기반 리소스 확인자인 경우 JCR 세션을 기반으로 합니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">UserManager</a></td>
   <td>UserManager는 사용자 및 그룹과 같은 권한 있는 개체를 유지 관리할 수 있는 액세스 및 수단을 제공합니다. UserManager가 특정 세션에 바인딩되어 있습니다.
   </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">승인 가능 대상</a> </td>
   <td>현재 사용자입니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">사용자</a><br /> </td>
   <td>현재 사용자입니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html">외부 도우미</a></td>
   <td>절대 URL을 표면화하기 위해, 요청 개체가 있더라도<br /> </td>
  </tr>
 </tbody>
</table>

[****](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletRequest.html) SlingHttpServletRequestions는 다음에 적용됩니다.

대상이 아직 없지만 Adaptable을 구현하고 사용자 지정 AdapterFactory에서 소스로 사용할 수 있습니다.

[****](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletResponse.html) SlingHttpServletResponsets는 다음에 적응합니다.

<table>
 <tbody>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br /> (XML)</td>
   <td>sling 재작성기 응답인 경우</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html)** 페이지는 다음 항목에 맞게 조정됩니다.

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">리소스</a><br /> </td>
   <td>페이지의 리소스.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>레이블이 지정된 리소스(==).</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">노드</a></td>
   <td>페이지의 노드입니다.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>페이지의 리소스를 조정할 수 있는 모든 것입니다.</td>
  </tr>
 </tbody>
</table>

**[](https://helpx.adobe.com/kr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html)** 구성 요소는 다음과 같습니다.

| [리소스](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 구성 요소의 리소스입니다. |
|---|---|
| [LabeledResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html) | 레이블이 지정된 리소스(==). |
| [노드](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 구성 요소의 노드입니다. |
| ... | 구성 요소의 리소스에 적용할 수 있는 모든 것입니다. |

**[](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html)** 템플릿에서는 다음에 맞게 조정됩니다.

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">리소스</a><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>템플릿의 리소스입니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>레이블이 지정된 리소스(==).</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">노드</a></td>
   <td>이 템플릿의 노드입니다.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>템플릿의 리소스를 조정할 수 있는 모든 것입니다.</td>
  </tr>
 </tbody>
</table>

#### 보안 {#security}

**작성 가능**,  **** 사용자 및 그룹 **** 은 다음 항목에 적응:

| [노드](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 사용자/그룹 홈 노드를 반환합니다. |
|---|---|
| [복제 상태](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html) | 사용자/그룹 홈 노드에 대한 복제 상태를 반환합니다. |

#### DAM {#dam}

**** 자산은 다음과 같습니다.

| [리소스](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 자산의 리소스입니다. |
|---|---|
| [노드](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 자산의 노드입니다. |
| ... | 자산의 리소스를 조정할 수 있는 모든 것입니다. |

#### 태깅 {#tagging}

**** 태그는 다음 항목에 맞게 조정됩니다.

| [리소스](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 태그의 리소스. |
|---|---|
| [노드](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 태그의 노드입니다. |
| ... | 태그의 리소스에 적용할 수 있는 모든 것입니다. |

#### 기타 {#other}

또한 Sling / JCR / OCM은 사용자 지정 OCM([개체 컨텐츠 매핑](https://jackrabbit.apache.org/object-content-mapping.html)) 개체용 ` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)`도 제공합니다.
