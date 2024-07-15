---
title: 콘텐츠 조각 템플릿
description: 템플릿은 콘텐츠 조각을 만들 때 선택되며 기본 구조, 요소 및 변형을 새 조각에 제공합니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 1b75721c-b223-41f0-88d9-bd855b529f31
solution: Experience Manager, Experience Manager Sites
feature: Developing,Content Fragments
role: Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 3%

---

# 콘텐츠 조각 템플릿{#content-fragment-templates}

>[!CAUTION]
>
>[콘텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md)은(는) 모든 새 콘텐츠 조각을 만드는 데 권장됩니다.
>
>컨텐츠 조각 모델은 WKND의 모든 예제에 사용됩니다.

>[!NOTE]
>
>AEM 6.3 이전에는 콘텐츠 조각이 모델이 아닌 템플릿을 기반으로 생성되었습니다.
>
>콘텐츠 조각 템플릿은 이제 더 이상 사용되지 않습니다. 조각을 만드는 데 계속 사용할 수 있지만 대신 콘텐츠 조각 모델 을 사용하는 것이 좋습니다. 조각 템플릿에 새로운 기능이 추가되지 않으며 이후 버전에서 제거됩니다.

템플릿은 콘텐츠 조각을 만들 때 선택됩니다. 기본 구조, 요소 및 변형을 새 조각에 제공합니다. 콘텐츠 조각에 사용되는 템플릿은 Granite 구성 관리자의 적용을 받습니다.

기본 템플릿은 아래에 보관됩니다.

* `/libs/settings/dam/cfm/templates`

다음에서 콘텐츠 조각에 대한 사이트별 템플릿을 만들 수 있습니다.

* `/apps/settings/dam/cfm/templates`
기본 템플릿을 오버레이하거나 런타임 시 확장/변경하지 않으려는 고객별 애플리케이션 전체 템플릿을 제공하는 위치입니다.

* `/conf/global/settings/dam/cfm/templates`
런타임 시 변경해야 하는 인스턴스 전체 고객별 템플릿의 위치입니다.

우선 순위 순서는 `/conf`, `/apps`, `/libs`입니다.

>[!CAUTION]
>
>***은(는) `/libs` 경로에서 아무 것도 변경하지 말아야***&#x200B;합니다.
>
>이는 다음에 인스턴스를 업그레이드할 때 `/libs`의 콘텐츠가 덮어쓰기되기 때문입니다(핫픽스 또는 기능 팩을 적용할 때 덮어쓸 수도 있음).
>
>구성 및 기타 변경에 권장되는 방법은 다음과 같습니다.
>
>1. `/apps` 아래에 필요한 항목(즉, `/libs`에 존재하는 항목)을 다시 만듭니다.
>
>1. `/apps` 내에서 변경
>

템플릿의 기본 구조는 다음 아래에 유지됩니다.

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

구체적인 구조는 다음과 같습니다.

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
     <td>이 노드는 각 템플릿의 루트입니다. 필수 항목이며 고유한 이름이 있어야 합니다.</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>필수<br /> </p> </td>
     <td>템플릿의 제목(<strong>조각 만들기</strong> 마법사에 표시됨)입니다.</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>선택 사항</p> </td>
     <td>템플릿의 목적을 설명하는 텍스트입니다(<strong>조각 만들기</strong> 마법사에 표시됨).</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>선택 사항</p> </td>
     <td>기본적으로 새로 생성된 콘텐츠 조각에 연결해야 하는 컬렉션 경로가 있는 배열입니다.</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>required</p> </td>
     <td><p><code>true</code>, 콘텐츠 조각을 만들 때 콘텐츠 조각의 요소(마스터 요소 제외)를 나타내는 하위 자산을 만들어야 하는 경우, <em>false</em> "즉시" 만들어야 하는 경우.</p> <p><strong>참고</strong>: 현재 이 매개 변수는 <code>true</code>(으)로 설정해야 합니다.</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>required</p> </td>
     <td><p>콘텐츠 구조의 버전. 현재 지원됨:</p> <p><strong>참고</strong>: 현재 이 매개 변수는 <code>2</code>.<br />(으)로 설정해야 합니다. </p> </td>
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
     <td><code>elements</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>required</p> </td>
     <td><p>콘텐츠 조각 요소의 정의가 포함된 노드입니다. 필수 항목이며 <strong>Main</strong> 요소에 대해 자식 노드를 하나 이상 포함해야 하지만 [1...n] 하위 노드.</p> <p>템플릿을 사용하면 요소 하위 분기가 조각의 모델 하위 분기에 복사됩니다.</p> <p>첫 번째 요소(CRXDE Lite에서 볼 때)는 자동으로 <i>main</i> 요소로 간주됩니다. 노드 이름은 관련이 없으며 노드 자체에는 특별한 의미가 없습니다. 주 자산으로 표시되지만 다른 요소는 하위 자산으로 처리됩니다.</p> </td>
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
     <td>이 노드는 요소를 정의합니다. 필수 항목이며 고유한 이름이 있어야 합니다.</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>required</p> </td>
     <td>요소의 제목(조각 편집기의 요소 선택기에 표시됨)입니다.</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>선택 사항</p> <p>기본값: ""</p> </td>
     <td>요소의 초기 콘텐츠. <code>precreateElements</code><i> = </i><code>true</code>인 경우에만 사용됨</td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>선택 사항</p> <p>기본값: <code>text/html</code></p> </td>
     <td><p>요소의 초기 콘텐츠 형식. <code>precreateElements</code><i> = </i><code>true</code>인 경우에만 사용됨; 현재 지원됨:</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>required</p> </td>
     <td>요소의 내부 이름입니다. 조각 유형에 대해 고유해야 합니다.</td>
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
     <td><code>variations</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>선택 사항</p> </td>
     <td>이 선택적 노드에는 콘텐츠 조각의 초기 변형에 대한 정의가 포함되어 있습니다.</td>
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
     <td><code>&lt;<i>variation-name</i>&gt;</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>변형 노드가 있는 경우 필요합니다.</p> </td>
     <td><p>초기 변형을 정의합니다.<br /> 기본적으로 변형은 콘텐츠 조각의 모든 요소에 추가됩니다.</p> <p>변형은 각 요소와 동일한 초기 콘텐츠를 갖습니다(<code class="code">defaultContent/
       initialContentType</code> 참조).</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>required</p> </td>
     <td>변형의 제목(조각 편집기의 <strong>변형</strong> 탭(왼쪽 레일)에 표시됨)입니다.</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>선택 사항</p> <p>기본값: ""</p> </td>
     <td>변형 <span>에 대한 설명을 제공하는 텍스트입니다(조각 편집기의 <strong>변형</strong> 탭(왼쪽 레일)에 표시됨).</code></td>
    </tr>
   </tbody>
  </table>
