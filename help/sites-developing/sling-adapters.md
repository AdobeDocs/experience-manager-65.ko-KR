---
title: Sling 어댑터 사용
seo-title: Sling 어댑터 사용
description: Sling은 어댑터 패턴을 제공하여 적응형 인터페이스를 구현하는 개체를 편리하게 변환합니다
seo-description: Sling은 어댑터 패턴을 제공하여 적응형 인터페이스를 구현하는 개체를 편리하게 변환합니다
uuid: 07f66a33-072d-49e1-8e67-8b80a6a9072a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: c081b242-67e4-4820-9bd3-7e4495df459e
translation-type: tm+mt
source-git-commit: 36cc5ca0de9ae2933a0d7585a00f26cc984d24db
workflow-type: tm+mt
source-wordcount: '2350'
ht-degree: 1%

---


# Sling 어댑터 사용{#using-sling-adapters}

[어댑터 ](https://sling.apache.org) 패턴을  [슬링고프하여 ](https://sling.apache.org/site/adapters.html) 어댑터  [](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) 인터페이스를 구현하는 개체를 편리하게변환합니다. 이 인터페이스에서는 인수를 통해 전달되는 클래스 유형으로 개체를 변환할 일반 [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) 메서드를 제공합니다.

예를 들어 리소스 개체를 해당 노드 개체로 변환하려면 다음을 수행하면 됩니다.

```java
Node node = resource.adaptTo(Node.class);
```

## 사용 사례 {#use-cases}

다음과 같은 사용 사례가 있습니다.

* 구현별 개체를 가져옵니다.

   예를 들어 일반 [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) 인터페이스의 JCR 기반 구현은 기본 JCR [`Node`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html)에 대한 액세스를 제공합니다.

* 내부 컨텍스트 개체를 전달해야 하는 개체의 바로 가기 만들기

   예를 들어, JCR 기반 [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html)은 요청의 [`JCR Session`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html)에 대한 참조를 보유하며, 이 참조는 [`PageManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) 또는 [`UserManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html)과 같은 요청 세션을 기반으로 하는 많은 개체에 필요합니다.

* 서비스에 바로 가기

   드문 경우이지만 `sling.getService()`도 간단합니다.

### Null 반환 값 {#null-return-value}

`adaptTo()` null을 반환할 수 있습니다.

다음과 같은 여러 가지 이유가 있습니다.

* 구현에서 대상 유형을 지원하지 않음
* 이 케이스를 처리하는 어댑터 팩터리가 활성 상태가 아닙니다(예: 서비스 참조가 없기 때문에)
* 내부 조건 실패
* 서비스를 사용할 수 없습니다.

Null 케이스를 정상적으로 처리하는 것이 중요합니다. jsp 렌더링의 경우 jsp가 실패할 경우 빈 컨텐츠가 발생할 수 있습니다.

### {#caching} 캐싱

성능을 개선하기 위해 구현은 `obj.adaptTo()` 호출에서 반환된 개체를 캐시할 수 있습니다. `obj`이 동일한 경우 반환된 개체가 동일합니다.

이 캐싱은 모든 `AdapterFactory` 기반 사례에 대해 수행됩니다.

그러나 일반 규칙이 없습니다. 개체가 새 인스턴스나 기존 인스턴스일 수 있습니다. 이는 두 행동 중 하나에 의존할 수 없음을 의미합니다. 따라서 특히 `AdapterFactory` 내에서 이 시나리오에서 개체가 다시 사용된다는 것은 중요합니다.

### 작동 방식 {#how-it-works}

다음과 같은 다양한 방법으로 `Adaptable.adaptTo()`을(를) 구현할 수 있습니다.

* 목적 자체로는;메서드 자체를 구현하고 특정 개체에 매핑을 수행합니다.
* 임의의 개체를 매핑할 수 있는 [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html)에 의해.

   개체는 여전히 `Adaptable` 인터페이스를 구현해야 하며 [`SlingAdaptable`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/adapter/SlingAdaptable.html)(중앙 어댑터 관리자에게 `adaptTo` 호출을 전달합니다.)

   이를 통해 `Resource`과 같은 기존 클래스에 대한 `adaptTo` 메커니즘에 연결할 수 있습니다.

* 두 가지 조합입니다.

첫 번째 경우 javadocs는 `adaptTo-targets`이(가) 가능한 것을 나타낼 수 있습니다. 그러나 JCR 기반 리소스와 같은 특정 하위 클래스의 경우 이는 종종 불가능합니다. 후자의 경우, `AdapterFactory`의 구현은 일반적으로 번들의 개인 클래스의 일부이므로 클라이언트 API에 노출되거나 javadocs에 나열되지 않습니다. 이론적으로, [OSGi](/help/sites-deploying/configuring-osgi.md) 서비스 런타임에서 모든 `AdapterFactory` 구현에 액세스하여 &quot;adaptables&quot;(소스 및 대상) 구성을 볼 수 있지만 서로 매핑하지는 않을 수 있습니다. 결국, 이것은 문서화되어야 하는 내부 로직에 따라 다릅니다. 따라서 이 참조

## 참조 {#reference}

### 슬링 {#sling}

[**리소스**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) 는 다음과 같습니다.

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">노드</a></td>
   <td>JCR 노드 기반 리소스이거나 노드를 참조하는 JCR 속성일 경우</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">속성</a></td>
   <td>JCR 속성 기반 리소스인 경우.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">항목</a></td>
   <td>JCR 기반 리소스인 경우(노드 또는 속성)</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api//java/util/Map.html">맵</a></td>
   <td>JCR 노드 기반 리소스(또는 기타 리소스 지원 값 맵)인 경우 속성의 맵을 반환합니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>JCR 노드 기반 리소스(또는 기타 리소스 지원 값 맵)인 경우 속성의 편리한 맵을 반환합니다. 또한 <br /> <code><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceUtil.html#getvaluemap%28org.apache.sling.api.resource.resource%29">ResourceUtil.getValueMap(Resource)</a></code>(null 대/소문자 처리 등)을 사용하여(더욱 단순한) 달성할 수 있습니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td>
   <td>속성을 찾을 때 리소스 계층을 고려하도록 하는 <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>의 확장입니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">수정 가능 값 맵</a></td>
   <td>해당 노드에서 속성을 수정할 수 있는 <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>의 확장입니다.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>파일 리소스의 바이너리 컨텐츠를 반환합니다(JCR-node 기반 리소스이고 노드 유형이 <code>nt:file</code> 또는 <code>nt:resource</code>;번들 리소스인 경우;파일 컨텐츠(파일 시스템 리소스인 경우) 또는 바이너리 JCR 속성 리소스의 데이터입니다.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>리소스(JCR 노드 기반 리소스인 경우 이 노드의 저장소 URL;번들 리소스인 경우 jar bundle URL;파일 시스템 리소스인 경우 파일 URL).</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/File.html">파일</a></td>
   <td>파일 시스템 리소스인 경우</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>이 리소스가 sling에 등록된 스크립트(예: jsp 파일)인 경우</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/products/servlet/2.2/javadoc/javax/servlet/Servlet.html">서블릿</a></td>
   <td>이 리소스가 Sling에 등록된 스크립트(예: jsp 파일)이거나 Servlet 리소스인 경우</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Double.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html"></a><br /> <a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html">StringBooleanLongDoubleCalendarValueString[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html">Boolean[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html">Long[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html">Calendar[]</a><br /> <a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Value[]</a></td>
   <td>JCR 속성 기반 리소스인 경우 값을 반환합니다(값이 적절함).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">레이블리소스</a></td>
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
   <td>dam:Asset 노드 리소스인 경우</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Rendition.html">렌디션</a></td>
   <td>dam:Asset 변환(dam:Assert의 변환 폴더 아래에 nt:file)인 경우</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/Tag.html">태그</a></td>
   <td><code>cq:Tag</code> 노드 리소스인 경우</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>JCR 기반 리소스이고 사용자에게 UserManager에 액세스할 권한이 있는 경우 JCR 세션을 기반으로 합니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">승인 가능 대상</a></td>
   <td>권한 부여됨은 사용자 및 그룹의 공통 기본 인터페이스입니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">사용자</a></td>
   <td>사용자는 인증 및 가장할 수 있는 특별한 승인 대상입니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/SimpleSearch.html">단순 검색</a></td>
   <td>리소스 아래에서 검색하거나 setSearchIn()(JCR 기반 리소스인 경우)을 사용합니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>지정된 페이지/워크플로우 페이로드 노드에 대한 워크플로우 상태입니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html">복제 상태</a></td>
   <td>지정된 리소스 또는 해당 jcr:content 하위 노드에 대한 복제 상태입니다(먼저 선택됨).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/connector/ConnectorResource.html">ConnectorResource</a></td>
   <td>JCR 노드 기반 리소스인 경우 특정 유형에 대해 조정된 커넥터 리소스를 반환합니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">구성</a></td>
   <td><code>cq:ContentSyncConfig</code> 노드 리소스인 경우</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>이 값이 <code>cq:ContentSyncConfig</code> 노드 리소스 아래에 있는 경우</td>
  </tr>
 </tbody>
</table>

[**ResourceResolution**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceResolver.html) 이 다음 항목에 맞게 조정됩니다.

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">세션</a></td>
   <td>요청의 JCR 세션(JCR 기반 리소스 확인자(기본값)입니다.</td>
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
   <td>JCR 세션을 기반으로 하는 경우, JCR 기반 리소스 확인자입니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>JCR 세션을 기반으로 하는 경우, JCR 기반 리소스 확인자입니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">UserManager</a></td>
   <td>UserManager는 사용자 및 그룹과 같이 권한이 부여된 개체를 유지 관리하기 위한 액세스 및 방법을 제공합니다. UserManager는 특정 세션에 바인딩됩니다.
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
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html">Externalizer</a></td>
   <td>절대 URL을 외부화하는 경우, 요청 개체를 사용하지 않는 경우에도 해당됩니다.<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequestt**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletRequest.html) 는 다음 항목에 연결합니다.

타겟이 아직 없지만 Adaptable을 구현하며 사용자 지정 AdapterFactory에서 소스로 사용할 수 있습니다.

[**SlingHttpServletResponseadapts**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletResponse.html) 대상:

<table>
 <tbody>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br /> (XML)</td>
   <td>이것이 슬링 리셀러 응답이라면</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[페이지](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html)** 는 다음 항목에 맞게 조정됩니다.

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">리소스</a><br /> </td>
   <td>페이지의 리소스입니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">레이블리소스</a></td>
   <td>레이블이 지정된 리소스(== this).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">노드</a></td>
   <td>페이지의 노드입니다.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>페이지 리소스를 조정할 수 있는 모든 것</td>
  </tr>
 </tbody>
</table>

**[구성 ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html)** 요소 어댑터:

| [리소스](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 구성 요소의 리소스입니다. |
|---|---|
| [레이블리소스](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html) | 레이블이 지정된 리소스(== this). |
| [노드](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 구성 요소의 노드입니다. |
| ... | 구성 요소의 리소스를 조정할 수 있는 모든 것 |

**[템플릿](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html)** 은 다음과 같은 용도로 사용됩니다.

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">리소스</a><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>템플릿의 리소스입니다.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">레이블리소스</a></td>
   <td>레이블이 지정된 리소스(== this).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">노드</a></td>
   <td>이 템플릿의 노드입니다.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>템플릿 리소스를 조정할 수 있는 모든 것</td>
  </tr>
 </tbody>
</table>

#### 보안 {#security}

**권한 부여 가능**, 사용자  **** 및  **** 그룹은 다음 항목에 적용됩니다.

| [노드](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 사용자/그룹 홈 노드를 반환합니다. |
|---|---|
| [복제 상태](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html) | 사용자/그룹 홈 노드에 대한 복제 상태를 반환합니다. |

#### DAM {#dam}

**자산** 은 다음과 같습니다.

| [리소스](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 자산의 리소스. |
|---|---|
| [노드](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 자산의 노드입니다. |
| ... | 자산의 리소스를 조정할 수 있는 모든 것. |

#### 태깅 {#tagging}

**태그는** 다음 항목에 맞게 조정됩니다.

| [리소스](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 태그의 리소스. |
|---|---|
| [노드](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 태그의 노드입니다. |
| ... | 태그의 리소스에 적용할 수 있는 모든 것 |

#### 기타 {#other}

또한 Sling / JCR / OCM은 사용자 지정 OCM([개체 컨텐트 매핑](https://jackrabbit.apache.org/object-content-mapping.html)) 개체에 대해 ` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)`을(를) 제공합니다.
