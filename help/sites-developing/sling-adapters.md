---
title: Sling 어댑터 사용
description: Sling은 어댑터 패턴을 제공하여 적응형 인터페이스를 구현하는 개체를 편리하게 번역할 수 있습니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 6465e2c4-28e5-4fc8-8cca-7b632f10ba5a
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1317'
ht-degree: 4%

---

# Sling 어댑터 사용{#using-sling-adapters}

[Sling](https://sling.apache.org)은(는) [적응성](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) 인터페이스를 구현하는 개체를 편리하게 번역할 수 있는 [어댑터 패턴](https://sling.apache.org/documentation/the-sling-engine/adapters.html)을(를) 제공합니다. 이 인터페이스는 개체를 인수로 전달되는 클래스 형식으로 변환하는 일반 [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) 메서드를 제공합니다.

예를 들어 리소스 객체를 해당 노드 객체로 변환하려면 다음과 같이 하면 됩니다.

```java
Node node = resource.adaptTo(Node.class);
```

## 사용 사례 {#use-cases}

다음과 같은 사용 사례가 있습니다.

* 구현별 개체를 가져옵니다.

  예를 들어 제네릭 [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) 인터페이스의 JCR 기반 구현은 기본 JCR [`Node`](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html)에 대한 액세스를 제공합니다.

* 내부 컨텍스트 객체를 전달해야 하는 객체의 바로 가기 작성.

  예를 들어 JCR 기반 [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html)에는 요청의 [`JCR Session`](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html)에 대한 참조가 있으며, 이는 [`PageManager`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/PageManager.html) 또는 [`UserManager`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/security/UserManager.html)과 같이 해당 요청 세션을 기반으로 작동하는 많은 개체에 필요합니다.

* 서비스 바로 가기.

  드문 경우이지만 `sling.getService()`도 간단합니다.

### Null 반환 값 {#null-return-value}

`adaptTo()`이(가) null을 반환합니다.

여기에는 다음과 같은 다양한 원인이 있습니다.

* 구현이 target 유형을 지원하지 않습니다.
* 이 사례를 처리하는 어댑터 팩토리가 활성화되지 않았습니다(예: 서비스 참조가 누락됨).
* 내부 조건 실패
* 서비스를 사용할 수 없음

null 케이스를 품위 있게 처리하는 것이 중요합니다. jsp 렌더링의 경우 컨텐츠가 비어 있는 경우 jsp가 실패해도 수용할 수 있습니다.

### 캐싱 {#caching}

성능을 향상시키기 위해 구현에서는 `obj.adaptTo()` 호출에서 반환된 개체를 캐싱할 수 있습니다. `obj`이(가) 동일하면 반환된 개체가 동일합니다.

이 캐싱은 모든 `AdapterFactory` 기반 사례에 대해 수행됩니다.

그러나 일반 규칙은 없습니다. 객체는 새 인스턴스이거나 기존 인스턴스일 수 있습니다. 이는 두 동작 중 하나에 의존할 수 없음을 의미합니다. 따라서 이 시나리오에서는 개체를 다시 사용할 수 있어야 합니다(특히 `AdapterFactory` 내부에서).

### 작동 방식 {#how-it-works}

`Adaptable.adaptTo()`을(를) 구현할 수 있는 방법에는 여러 가지가 있습니다.

* 객체 자체, 메소드 자체를 구현하고 특정 객체에 매핑.
* 임의의 개체를 매핑할 수 있는 [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html)까지

  개체는 여전히 `Adaptable` 인터페이스를 구현해야 하며 [`SlingAdaptable`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/adapter/SlingAdaptable.html)을(를) 확장해야 합니다(`adaptTo` 호출을 중앙 어댑터 관리자에 전달).

  이를 통해 `Resource`과(와) 같은 기존 클래스에 대한 `adaptTo` 메커니즘에 후크를 연결할 수 있습니다.

* 둘의 조합.

첫 번째 경우 Java™ 문서에는 `adaptTo-targets`이(가) 가능한 내용이 표시될 수 있습니다. 그러나 JCR 기반 리소스와 같은 특정 하위 클래스의 경우 이러한 작업이 불가능한 경우가 많습니다. 후자의 경우 `AdapterFactory`의 구현은 일반적으로 번들의 전용 클래스에 속하므로 클라이언트 API에 노출되지 않으며 Java™ 문서에 나열되지 않습니다. 이론적으로는 [OSGi](/help/sites-deploying/configuring-osgi.md) 서비스 런타임에서 모든 `AdapterFactory` 구현에 액세스하여 &quot;적응성&quot;(소스 및 타겟) 구성을 볼 수 있지만 서로 매핑하지는 않을 수 있습니다. 결국 이는 내부 논리에 따라 달라지는데 이를 반드시 문서화해야 한다. 따라서 이 참조입니다.

## 참조 {#reference}

### 슬링 {#sling}

[**리소스**](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html)은(는) 다음 항목에 적응합니다.

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">노드</a></td>
   <td>JCR 노드 기반 리소스 또는 노드를 참조하는 JCR 속성인 경우</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">속성</a></td>
   <td>JCR 속성 기반 리소스인 경우</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">항목</a></td>
   <td>JCR 기반 리소스(노드 또는 속성)인 경우</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Map.html">맵</a></td>
   <td>JCR 노드 기반 리소스(또는 다른 리소스 지원 값 맵)인 경우 속성 맵을 반환합니다.</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>JCR 노드 기반 리소스(또는 다른 리소스 지원 값 맵)인 경우 사용하기 편리한 속성 맵을 반환합니다. <br /> <code><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ResourceUtil.html">ResourceUtil.getValueMap(Resource)</a></code>을(를) 사용하여(더 간단하게) 달성할 수도 있습니다(null 사례 등을 처리).</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">상속 값 맵</a></td>
   <td>속성을 찾을 때 리소스 계층 구조를 고려할 수 있도록 하는 <a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>의 확장입니다.</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">수정 가능한 값 맵</a></td>
   <td>해당 노드의 속성을 수정할 수 있는 <a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>의 확장입니다</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/InputStream.html">입력 스트림</a></td>
   <td>파일 리소스의 이진 콘텐츠(JCR 노드 기반 리소스이고 노드 유형이 <code>nt:file</code> 또는 <code>nt:resource</code>인 경우, 번들 리소스인 경우, 파일 시스템 리소스인 경우, 파일 콘텐츠) 또는 이진 JCR 속성 리소스의 데이터를 반환합니다.</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>리소스에 대한 URL 반환(JCR 노드 기반 리소스인 경우 이 노드의 저장소 URL, 번들 리소스인 경우 jar 번들 URL, 파일 시스템 리소스인 경우 파일 URL)</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/File.html">파일</a></td>
   <td>파일 시스템 리소스인 경우</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>이 리소스가 스크립트 엔진이 sling에 등록된 스크립트(예: jsp 파일)인 경우</td>
  </tr>
  <tr>
   <td><a href="https://www.oracle.com/java/technologies/servlet-technology.html">서블릿</a></td>
   <td>이 리소스가 스크립트 엔진이 sling에 등록된 스크립트(예: jsp 파일)이거나 서블릿 리소스인 경우.</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">문자열</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">부울</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">긴</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Double.html">이중</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">달력</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">값</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">문자열[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">부울[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">긴[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">달력[]</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">값[]</a></td>
   <td>JCR 속성 기반 리소스인 경우(값이 적절한 경우) 값을 반환합니다.</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>JCR 노드 기반 리소스인 경우</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html">페이지</a></td>
   <td>JCR 노드 기반 리소스이고 노드가 <code>cq:Page</code>(또는 <code>cq:PseudoPage</code>)인 경우</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/components/Component.html">구성 요소</a></td>
   <td><code>cq:Component</code> 노드 리소스인 경우</td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/designer/Design.html">디자인</a></td>
   <td>디자인 노드(<code>cq:Page</code>)인 경우</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Template.html">템플릿</a></td>
   <td><code>cq:Template</code> 노드 리소스인 경우</td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/Blueprint.html">블루프린트</a></td>
   <td><code>cq:Template</code> 노드 리소스인 경우</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/dam/api/Asset.html">자산</a></td>
   <td>dam:Asset 노드 리소스인 경우</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/dam/api/Rendition.html">렌디션</a></td>
   <td>dam:Asset 렌디션(dam:Assert의 렌디션 폴더 아래에 있는 nt:file)인 경우</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/tagging/Tag.html">태그</a></td>
   <td><code>cq:Tag</code> 노드 리소스인 경우</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>JCR 세션 기반: JCR 기반 리소스이고 사용자가 UserManager에 액세스할 수 있는 권한이 있는 경우</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">승인 가능 대상</a></td>
   <td>승인 가능 대상은 사용자 및 그룹의 공통 기본 인터페이스입니다.</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/User.html">사용자</a></td>
   <td>사용자는 인증되고 가장될 수 있는 특별한 승인 가능 대상입니다.</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/search/SimpleSearch.html">SimpleSearch</a></td>
   <td>JCR 기반 리소스인 경우 리소스 아래에서 검색하거나 setSearchIn() 사용</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>지정된 페이지/워크플로 페이로드 노드의 워크플로 상태</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/replication/ReplicationStatus.html">ReplicationStatus</a></td>
   <td>지정된 리소스 또는 해당 jcr:content 하위 노드의 복제 상태(먼저 선택됨)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/connector/ConnectorResource.html">ConnectorResource</a></td>
   <td>JCR-노드 기반 리소스인 경우, 특정 유형에 대해 조정된 커넥터 리소스를 반환합니다.</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/config/package-summary.html">구성</a></td>
   <td><code>cq:ContentSyncConfig</code> 노드 리소스인 경우</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td><code>cq:ContentSyncConfig</code> 노드 리소스 미만인 경우</td>
  </tr>
 </tbody>
</table>

[**ResourceResolver**](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ResourceResolver.html)은(는) 다음 항목에 적응합니다.

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">세션</a></td>
   <td>요청의 JCR 세션(JCR 기반 리소스 확인자인 경우)(기본값)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">구성 요소 관리자</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/designer/Designer.html">Designer</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>JCR 세션 기반, JCR 기반 리소스 확인자인 경우</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>JCR 세션 기반, JCR 기반 리소스 확인자인 경우</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">UserManager</a></td>
   <td>UserManager는 승인 가능한 객체(사용자 및 그룹)에 대한 액세스 권한과 유지 관리 수단을 제공합니다. UserManager는 특정 세션에 바인딩되어 있습니다
   </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">승인 가능</a> </td>
   <td>현재 사용자</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/User.html">사용자</a><br /> </td>
   <td>현재 사용자</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/Externalizer.html">Externalizer</a></td>
   <td>절대 URL을 외부화하는 경우 요청 개체 <br />이(가) 없어도 </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest**](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/SlingHttpServletRequest.html)은(는) 다음 항목에 적용됩니다.

아직 대상이 없지만 는 적응성을 구현하며 사용자 지정 AdapterFactory에서 소스로 사용할 수 있습니다.

[**SlingHttpServletResponse**](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/SlingHttpServletResponse.html)은(는) 다음 항목에 적응합니다.

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br />(XML)</td>
   <td>Sling 재작성기 응답인 경우</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[페이지](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html)**&#x200B;은(는) 다음 항목에 적응합니다.

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html">리소스</a><br /> </td>
   <td>페이지의 리소스</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>레이블이 지정된 리소스(==)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">노드</a></td>
   <td>페이지의 노드</td>
  </tr>
  <tr>
   <td>...</td>
   <td>페이지의 리소스를 조정할 수 있는 모든 작업</td>
  </tr>
 </tbody>
</table>

**[구성 요소](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/components/Component.html)**&#x200B;은(는) 다음 항목에 적응합니다.

| [리소스](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) | 구성 요소의 리소스. |
|---|---|
| [LabeledResource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/LabeledResource.html) | 레이블이 지정된 리소스(이 ==)입니다. |
| [노드](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 구성 요소의 노드. |
| ... | 구성 요소 리소스의 모든 것을 적용할 수 있습니다. |

**[템플릿](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Template.html)**&#x200B;은(는) 다음 항목에 적응합니다.

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html">리소스</a><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>템플릿의 리소스</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>레이블이 지정된 리소스(==)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">노드</a></td>
   <td>이 템플릿의 노드</td>
  </tr>
  <tr>
   <td>...</td>
   <td>템플릿 리소스의 모든 것을 적용할 수 있습니다.</td>
  </tr>
 </tbody>
</table>

#### 보안 {#security}

**승인 가능**, **사용자 및 &#x200B;** 그룹**&#x200B;이(가) 다음에 적용됩니다.

| [노드](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 사용자/그룹 홈 노드를 반환합니다. |
|---|---|
| [복제 상태](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/replication/ReplicationStatus.html) | 사용자/그룹 홈 노드에 대한 복제 상태를 반환합니다. |

#### DAM {#dam}

**자산**&#x200B;이(가) 다음에 적응함:

| [리소스](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) | 에셋의 리소스입니다. |
|---|---|
| [노드](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 에셋의 노드. |
| ... | 에셋의 리소스를 조정할 수 있는 모든 작업. |

#### 태그 지정 {#tagging}

**태그**&#x200B;은(는) 다음 항목에 적응합니다.

| [리소스](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) | 태그의 리소스. |
|---|---|
| [노드](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 태그의 노드. |
| ... | 태그의 리소스에 맞는 모든 항목을 조정할 수 있습니다. |

#### 기타 {#other}

또한 Sling/JCR/OCM은 사용자 지정 OCM([개체 콘텐츠 매핑](https://jackrabbit.apache.org/jcr/object-content-mapping.html)) 개체에 대해 ` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)`을(를) 제공합니다.
