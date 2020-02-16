---
title: 컨텐츠 조각 템플릿
seo-title: 컨텐츠 조각 템플릿
description: 컨텐츠 조각을 만들 때 템플릿이 선택되고 기본 구조, 요소 및 변형으로 새 조각을 제공합니다
seo-description: 컨텐츠 조각을 만들 때 템플릿이 선택되고 기본 구조, 요소 및 변형으로 새 조각을 제공합니다
uuid: d147bac8-b710-40ed-9664-decb5ffcf8e7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: a975ea2e-5e24-4a96-bd62-63bb98836ff2
docset: aem65
translation-type: tm+mt
source-git-commit: 0dc96f07e45ccbfea4edc87431677ada5b1bfa8c

---


# 컨텐츠 조각 템플릿{#content-fragment-templates}

>[!CAUTION]
>
>[이제 컨텐츠 조각 모델을](/help/assets/content-fragments-models.md) 모든 조각을 만드는 데 권장합니다.
>
>컨텐츠 조각 모델은 We.Retail의 모든 예에 사용됩니다.

컨텐츠 조각을 만들 때 템플릿이 선택됩니다. 기본 구조, 요소 및 변형과 함께 새 조각을 제공합니다. 컨텐츠 조각에 사용되는 템플릿은 [granite 구성 관리자]의 적용을 받습니다.

기본 템플릿은 다음과 같이 유지됩니다.

* `/libs/settings/dam/cfm/templates`

다음 아래에서 컨텐츠 조각에 대한 사이트별 템플릿을 만들 수 있습니다.

* `/apps/settings/dam/cfm/templates`
기본 템플릿을 오버레이하거나 런타임 시 확장/변경되어서는 안 되는 애플리케이션별 템플릿을 제공하는 위치입니다.

* `/conf/global/settings/dam/cfm/templates`
런타임 시 변경해야 하는 인스턴스 전체 고객별 템플릿의 위치입니다.

우선 순위는 (내림차순) `/conf``/apps`, `/libs`입니다.

>[!CAUTION]
>
>패스에 있는 ***어떤 것도 변경하지*** 않아야 `/libs` 합니다.
>
>이는 다음에 인스턴스를 업그레이드할 때 의 컨텐츠를 `/libs` 덮어쓰게 되기 때문입니다(핫픽스 또는 기능 팩을 적용할 때 덮어쓸 수 있음).
>
>구성 및 기타 변경에 대한 권장 방법은 다음과 같습니다.
>
>1. 필요한 항목(즉, 있는 대로)을 `/libs``/apps`
   >
   >
1. Make any changes within `/apps`
>



템플릿의 기본 구조는 다음과 같습니다.

```xml
conf
  global
    settings
      dam
        cfm
          templates
            <template-name>
              ...
```

특정 구조를 사용하여 다음을 수행할 수 있습니다.

```xml
+ <template-name>
    - jcr:primaryType
    - jcr:title
    - jcr:description
    - initialAssociatedContent
    - precreateElements
    - version
    + elements
        - jcr:primaryType
        + <element-name>
            - jcr:primaryType
            - jcr:title
            - defaultContent
            - initialContentType
            - name
        ... + other element definitions
    + variations
        - jcr:primaryType
        + <variation-name>
            - jcr:primaryType
            - jcr:title
            - jcr:description
            - name
        ... + other variation definitions
```

노드 및 해당 속성에 대한 자세한 내용은 다음과 같습니다.

* **템플릿**

   <table>
   <tbody>
    <tr>
     <th>이름</th>
     <th>유형</th>
     <th>값</th>
    </tr>
    <tr>
     <td><code>&lt;<em>template-name</em>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>이 노드는 각 템플릿의 루트입니다. 필수 사항이며 고유한 이름을 가져야 합니다.</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>required<br /> </p> </td>
     <td>템플릿의 제목(조각 만들기 <strong>마법사에 표시됨</strong> ).</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>옵션</p> </td>
     <td>템플릿의 용도를 설명하는 텍스트입니다(조각 만들기 <strong>마법사에 표시됨</strong> ).</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>옵션</p> </td>
     <td>기본적으로 새로 만든 콘텐츠 조각에 연결해야 하는 컬렉션 경로가 있는 배열입니다.</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>required</p> </td>
     <td><p><code>true</code>, 컨텐츠 조각을 만들 때 컨텐츠 조각의 요소(마스터 요소 제외)를 나타내는 하위 자산을 만들어야 하는 경우;" <em>on the fly"를 만들어야 하는 경우 false</em> .</p> <p><strong>참고</strong>:현재 이 매개 변수는 로 설정해야 <code>true</code>합니다.</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>required</p> </td>
     <td><p>콘텐츠 구조의 버전;현재 지원됨:</p> <p><strong>참고</strong>:현재 이 매개 변수는 로 설정해야 <code>2</code>합니다.<br /> </p> </td>
    </tr>
   </tbody>
  </table>

* **요소**

   <table>
   <tbody>
    <tr>
     <th>이름</th>
     <th>유형</th>
     <th>값</th>
    </tr>
    <tr>
     <td><code>elements</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>required</p> </td>
     <td><p>컨텐츠 조각 요소의 정의를 포함하는 노드입니다. 필수 항목이며 Main 요소에 대해 하나 이상의 하위 노드를 포함해야 <strong>하지만</strong> [1...n] 하위 노드.</p> <p>템플릿을 사용하면 요소 하위 분기가 조각의 모델 하위 분기로 복사됩니다.</p> <p>첫 번째 요소(CRXDE Lite에서 보듯이)는 자동으로 <i>주</i> 요소로 간주됩니다.노드 이름은 사용할 수 없으며, 노드 자체에는 주 자산으로 표현된다는 사실 이외에 특별한 의미가 없습니다.다른 요소는 하위 자산으로 처리됩니다.</p> </td>
    </tr>
   </tbody>
  </table>

* **요소 이름**

   <table>
   <tbody>
    <tr>
     <th>이름</th>
     <th>유형</th>
     <th>값</th>
    </tr>
    <tr>
     <td><code>&lt;<i>element-name</i>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>이 노드는 요소를 정의합니다. 필수 사항이며 고유한 이름을 가져야 합니다.</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>required</p> </td>
     <td>요소의 제목(조각 편집기의 요소 선택기에 표시됨).</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>옵션</p> <p>기본값: ""</p> </td>
     <td>요소의 초기 컨텐츠;= <code>precreateElements</code><i> 인 경우에만 사용됨 </i><code>true</code></td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>옵션</p> <p>기본값: <code>text/html</code></p> </td>
     <td><p>요소의 초기 컨텐츠 유형;if <code>precreateElements</code><i> = </i><code>true</code>;현재 지원됨:</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>required</p> </td>
     <td>요소의 내부 이름;는 조각 유형에 대해 고유해야 합니다.</td>
    </tr>
   </tbody>
  </table>

* **변형**

   <table>
   <tbody>
    <tr>
     <th>이름</th>
     <th>유형</th>
     <th>값</th>
    </tr>
    <tr>
     <td><code>variations</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>옵션</p> </td>
     <td>이 선택적 노드에는 컨텐츠 조각의 초기 변형 정의가 포함됩니다.</td>
    </tr>
   </tbody>
  </table>

* **변형 이름**

   <table>
   <tbody>
    <tr>
     <th>이름</th>
     <th>유형</th>
     <th>값</th>
    </tr>
    <tr>
     <td><code>&lt;<i>variation-name</i>&gt;</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>변형 노드가 있으면 필요합니다.</p> </td>
     <td><p>초기 변형을 정의합니다.<br /> 변형은 기본적으로 컨텐츠 조각의 모든 요소에 추가됩니다.</p> <p>변형은 각 요소와 동일한 초기 컨텐츠를 갖게 됩니다( 참조 <code class="code">defaultContent/
       initialContentType</code>).</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>required</p> </td>
     <td>변형 제목(조각 편집기의 변형 <strong>탭(왼쪽 레일</strong> )에 표시됨)</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>옵션</p> <p>기본값: ""</p> </td>
     <td>변형 설명을 제공하는 텍스트입니다(조각 편집기의 변형 <span>탭( <strong>왼쪽 레일</strong> )에 표시됨).</code></td>
    </tr>
   </tbody>
  </table>
