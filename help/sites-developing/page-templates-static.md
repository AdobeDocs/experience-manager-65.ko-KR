---
title: 페이지 템플릿 - 정적
description: 템플릿을 사용하여 페이지를 만들고 선택한 범위 내에서 사용할 수 있는 구성 요소를 정의합니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: b934ac41-78b9-497f-ba95-b05ef1e5660e
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 2%

---

# 페이지 템플릿 - 정적{#page-templates-static}

템플릿은 페이지를 만드는 데 사용되며, 선택한 범위 내에서 사용할 수 있는 구성 요소를 정의합니다. 템플릿은 만들 페이지와 구조가 동일하지만 실제 컨텐츠는 없는 노드의 계층입니다.

각 템플릿에는 사용할 수 있는 구성 요소 선택 사항이 표시됩니다.

* 템플릿은 다음으로 구성됩니다. [구성 요소](/help/sites-developing/components.md);
* 구성 요소는 위젯을 사용하고 이에 대한 액세스를 허용하며, 위젯은 콘텐츠를 렌더링하는 데 사용됩니다.

>[!NOTE]
>
>[편집 가능한 템플릿](/help/sites-developing/page-templates-editable.md) 또한 를 사용할 수 있으며, 대부분의 유연성과 최신 기능을 제공하는 권장 템플릿 유형입니다.

## 템플릿의 속성 및 하위 노드 {#properties-and-child-nodes-of-a-template}

템플릿은 cq:Template 유형의 노드이며, 다음 속성과 하위 노드를 포함합니다.

<table>
 <tbody>
  <tr>
   <td><strong>이름 <br /> </strong></td>
   <td><strong>유형 <br /> </strong></td>
   <td><strong>설명 <br /> </strong></td>
  </tr>
  <tr>
   <td>. <br /> </td>
   <td> cq:Template</td>
   <td>현재 템플릿입니다. 템플릿은 노드 유형 cq:Template입니다.<br /> </td>
  </tr>
  <tr>
   <td> allowedChildren </td>
   <td> String[]</td>
   <td>이 템플릿의 하위 템플릿으로 사용할 수 있는 템플릿 경로<br /> </td>
  </tr>
  <tr>
   <td> allowedParents</td>
   <td> String[]</td>
   <td>이 템플릿의 상위가 되도록 허용되는 템플릿의 경로입니다.<br /> </td>
  </tr>
  <tr>
   <td> allowedPath</td>
   <td> String[]</td>
   <td>이 템플릿을 기반으로 할 수 있는 페이지의 경로입니다.<br /> </td>
  </tr>
  <tr>
   <td> jcr:created</td>
   <td> 날짜</td>
   <td>템플릿 생성일.<br /> </td>
  </tr>
  <tr>
   <td> jcr:description</td>
   <td> 문자열</td>
   <td>템플릿에 대한 설명입니다.<br /> </td>
  </tr>
  <tr>
   <td> jcr:title</td>
   <td> 문자열</td>
   <td>템플릿 제목<br /> </td>
  </tr>
  <tr>
   <td> 등급</td>
   <td> Long</td>
   <td>템플릿의 등급. 사용자 인터페이스에 템플릿을 표시하는 데 사용됩니다.<br /> </td>
  </tr>
  <tr>
   <td> jcr:content</td>
   <td> cq:PageContent</td>
   <td>템플릿의 콘텐츠가 포함된 노드<br /> </td>
  </tr>
  <tr>
   <td> thumbnail.png</td>
   <td> nt:file</td>
   <td>템플릿의 축소판입니다.<br /> </td>
  </tr>
  <tr>
   <td> icon.png</td>
   <td> nt:file</td>
   <td>템플릿의 아이콘.<br /> </td>
  </tr>
 </tbody>
</table>

템플릿은 페이지의 기초입니다.

페이지를 만들려면 템플릿을 복사해야 합니다(노드 트리) `/apps/<myapp>/template/<mytemplate>`)를 사이트 트리의 해당 위치에 추가합니다. 이렇게 하는 것은 페이지를 **웹 사이트** 탭.

또한 이 복사 작업은 페이지에 초기 콘텐츠(일반적으로 최상위 수준의 콘텐츠만 해당) 및 속성 sling:resourceType을 제공합니다. sling:resourceType은 페이지를 렌더링하는 데 사용되는 페이지 구성 요소의 경로(하위 노드 jcr:content에 있는 모든 항목)입니다.

## 템플릿 구성 방법 {#how-templates-are-structured}

고려해야 할 두 가지 측면이 있습니다.

* 템플릿 자체의 구조
* 템플릿 사용 시 생성되는 콘텐츠 구조

### 템플릿의 구조 {#the-structure-of-a-template}

템플릿은 유형의 노드 아래에 만들어집니다. **cq:Template**.

![screen_shot_2012-02-13at63646pm](assets/screen_shot_2012-02-13at63646pm.png)

다양한 속성을 설정할 수 있습니다. 특히

* **jcr:title** - 템플릿 제목이며 페이지를 만들 때 대화 상자에 표시됩니다.
* **jcr:description** - 템플릿에 대한 설명. 페이지를 만들 때 대화 상자에 표시됩니다.

이 노드에는 결과 페이지의 콘텐츠 노드의 기반으로 사용되는 jcr:content(cq:PageContent) 노드가 포함되어 있습니다. 이 노드는 새 페이지의 실제 콘텐츠를 렌더링하는 데 사용되는 구성 요소인 sling:resourceType을 사용하여 을 참조합니다.

![screen_shot_2012-02-13at64010pm](assets/screen_shot_2012-02-13at64010pm.png)

이 구성 요소를 사용하여 새 페이지를 만들 때 콘텐츠의 구조 및 디자인을 정의합니다.

![screen_shot_2012-02-13at64137pm](assets/screen_shot_2012-02-13at64137pm.png)

### 템플릿에서 생성된 콘텐츠 {#the-content-produced-by-a-template}

템플릿은 유형의 페이지를 만드는 데 사용됩니다. `cq:Page` (앞에서 언급했듯이 페이지는 특별한 유형의 구성 요소입니다.) 각 AEM 페이지에는 구조화된 노드가 있습니다 `jcr:content`. 이를 통해 다음이 가능합니다.

* 은(는) cq:PageContent 유형입니다
* 정의된 콘텐츠 정의를 포함하는 구조화된 노드 유형입니다.
* 에 속성이 있음 `sling:resourceType` 콘텐츠 렌더링에 사용되는 sling 스크립트가 있는 구성 요소를 참조하려면

### 기본 템플릿 {#default-templates}

AEM에는 즉시 사용할 수 있는 다양한 기본 템플릿이 제공됩니다. 경우에 따라 템플릿을 그대로 사용할 수 있습니다. 이 경우 웹 사이트에서 템플릿을 사용할 수 있는지 확인해야 합니다.

예를 들어 AEM에는 contentpage 및 홈 페이지를 포함한 여러 템플릿이 제공됩니다.

| **제목** | **구성 요소** | **위치** | **목적** |
|---|---|---|---|
| 홈 페이지 | homepage | geometrixx | Geometrixx 홈페이지 템플릿. |
| 컨텐츠 페이지 | contentpage | geometrixx | Geometrixx 컨텐츠 페이지 템플릿입니다. |

#### 기본 템플릿 표시 {#displaying-default-templates}

저장소의 모든 템플릿 목록을 보려면 다음과 같이 진행하십시오.

1. CRXDE Lite에서 **도구** 메뉴 및 클릭 **쿼리**.

1. 쿼리 탭에서
1. 다음으로: **유형**, 선택 **XPath**.

1. 다음에서 **쿼리** 입력 필드에 다음 문자열을 입력합니다. //element(&#42;, cq:Template)

1. 클릭 **실행**. 목록이 결과 상자에 표시됩니다.

일반적으로 기존 템플릿을 가져와 새로운 템플릿을 개발하여 사용할 수 있습니다. 다음을 참조하십시오 [페이지 템플릿 개발](#developing-page-templates) 추가 정보.

웹 사이트에 대한 기존 템플릿을 활성화하고 이 템플릿을 **페이지 만들기** 페이지를 만들 때 아래에 있는 대화 상자 **웹 사이트** 다음에서 **웹 사이트** 콘솔에서 템플릿 노드의 allowedPaths 속성을 다음으로 설정합니다. **/content(/.&#42;)?**

## 템플릿 디자인 적용 방법 {#how-template-designs-are-applied}

UI에 스타일을 정의하는 경우 [디자인 모드](/help/sites-authoring/default-components-designmode.md), 디자인은 스타일이 정의되는 콘텐츠 노드의 정확한 경로에서 지속됩니다.

>[!CAUTION]
>
>Adobe은 다음 작업을 통해서만 디자인을 적용할 것을 권장합니다. [디자인 모드](/help/sites-authoring/default-components-designmode.md).
>
>예를 들어 CRXDE Lite에서 디자인을 수정하는 것은 모범 사례가 아니며, 이러한 디자인의 적용은 예상되는 비헤이비어와 다를 수 있습니다.

디자인이 디자인 모드로만 적용되는 경우 다음 섹션을 참조하십시오. [디자인 경로 해상도](/help/sites-developing/page-templates-static.md#design-path-resolution), [의사 결정 트리](/help/sites-developing/page-templates-static.md#decision-tree)및 [예](/help/sites-developing/page-templates-static.md#example) 적용할 수 없습니다.

### 디자인 경로 해상도 {#design-path-resolution}

정적 템플릿을 기반으로 콘텐츠를 렌더링할 때 AEM은 콘텐츠 계층 구조 순회를 기반으로 콘텐츠에 가장 관련성이 높은 디자인과 스타일을 적용하려고 합니다.

AEM은 콘텐츠 노드에 대해 가장 관련성이 높은 스타일을 다음 순서로 결정합니다.

* 디자인 모드에서 디자인을 정의할 때와 같이 컨텐츠 노드의 전체적이고 정확한 경로에 대한 디자인이 있는 경우 해당 디자인을 사용합니다.
* 상위 노드의 콘텐츠 노드에 대한 디자인이 있는 경우 해당 디자인을 사용합니다.
* 컨텐츠 노드의 경로에 있는 노드에 대한 디자인이 있는 경우 해당 디자인을 사용합니다.

마지막 두 가지 경우 적용 가능한 디자인이 두 개 이상인 경우 콘텐츠 노드에 가장 가까운 디자인을 사용합니다.

### 의사 결정 트리 {#decision-tree}

다음은 를 그래픽으로 표현한 것입니다. [디자인 경로 해상도](/help/sites-developing/page-templates-static.md#design-path-resolution) 논리.

![design_path_resolution](assets/design_path_resolution.png)

### 예 {#example}

디자인이 모든 노드에 적용될 수 있는 다음과 같은 간단한 콘텐츠 구조를 고려하십시오.

`/root/branch/leaf`

다음 표에서는 AEM에서 디자인을 선택하는 방법을 설명합니다.

<table>
 <tbody>
  <tr>
   <td><strong>디자인 찾기<br /> </strong></td>
   <td><strong>설계 대상<br /> </strong></td>
   <td><strong>디자인 선택됨<br /> </strong></td>
   <td><strong>댓글</strong></td>
  </tr>
  <tr>
   <td><code class="code">leaf
      </code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> <p><code>leaf</code></p> </td>
   <td><code>leaf</code></td>
   <td>가장 정확한 일치는 항상 가져갑니다.<br /> </td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> </td>
   <td><code>branch</code></td>
   <td>트리에서 가장 가까운 하위로 떨어집니다.</td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><code>root</code></td>
   <td><code>root</code></td>
   <td>다른 작업이 모두 실패하면 남은 항목을 가져옵니다.<br /> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><code>branch</code></td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>branch</code></p> <p><code class="code">leaf
       </code></p> </td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>root</code></p> <p><code class="code">branch
       </code></p> </td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>root</code></p> <p><code class="code">leaf
       </code></p> </td>
   <td><code>root</code></td>
   <td><p>정확히 일치하는 것이 없으면 나무에서 아래쪽에 있는 것을 타세요.</p> <p>가정은 이것이 항상 적용 가능하지만, 더 멀리 올라가는 것은 너무 구체적일 수 있다는 것이다.<br /> </p> </td>
  </tr>
 </tbody>
</table>

## 페이지 템플릿 개발 {#developing-page-templates}

AEM 페이지 템플릿은 페이지를 만드는 데 사용되는 모델일 뿐입니다. 필요한 초기 콘텐츠를 필요한 만큼 적게 또는 많이 포함할 수 있습니다. 초기 콘텐츠의 역할은 올바른 초기 노드 구조를 만드는 것이며, 필요한 속성(주로 sling:resourceType)은 편집 및 렌더링을 허용하도록 설정됩니다.

### 템플릿 만들기(기존 템플릿 기반) {#creating-a-new-template-based-on-an-existing-template}

새 템플릿은 처음부터 완전히 만들 수 있지만, 종종 기존 템플릿을 대신 복사하고 업데이트하여 시간과 노력을 절약할 수 있습니다. 예를 들어 Geometrixx 내의 템플릿을 사용하여 시작할 수 있습니다.

기존 템플릿을 기반으로 템플릿을 만들려면 다음 작업을 수행하십시오.

1. 기존 템플릿(달성하고자 하는 목표에 가능한 한 가까운 정의를 사용하는 것이 좋음)을 새 노드에 복사합니다.

   템플릿은에 저장됩니다. **/apps/&lt;website-name>/templates/&lt;template-name>**.

   >[!NOTE]
   >
   >사용 가능한 템플릿 목록은 새 페이지의 위치와 각 템플릿에 지정된 배치 제한에 따라 다릅니다. 다음을 참조하십시오 [템플릿 가용성](#templateavailibility).

1. 변경 **jcr:title** 새 역할을 반영할 새 템플릿 노드의 입니다. 다음을 업데이트할 수도 있습니다. **jcr:description** 필요한 경우. 페이지의 템플릿 가용성을 적절하게 변경해야 합니다.

   >[!NOTE]
   >
   >템플릿을 **페이지 만들기** 페이지를 만들 때 아래에 있는 대화 상자 **웹 사이트** 다음에서 **웹 사이트** 콘솔, 설정 `allowedPaths` 템플릿 노드의 속성: `/content(/.*)?`

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. 템플릿의 기반이 되는 구성 요소를 복사합니다( 는 로 나타남). **sling:resourceType** 의 속성 **jcr:content** 인스턴스를 생성할 수 있습니다.

   구성 요소는에 저장됩니다. **/apps/&lt;website-name>/components/&lt;component-name>**.

1. 업데이트 **jcr:title** 및 **jcr:description** 새 구성 요소
1. 템플릿 선택 목록(크기 128 x 98px)에 새 축소판 그림을 표시하려면 thumbnail.png를 바꿉니다.
1. 업데이트 **sling:resourceType** / 템플릿 **jcr:content** 새 구성 요소를 참조할 노드입니다.
1. 템플릿, 기본 구성 요소 또는 둘 다의 기능이나 디자인을 추가로 변경합니다.

   >[!NOTE]
   >
   >에 대한 변경 사항 **/apps/&lt;website>/templates/&lt;template-name>** 노드는 선택 목록에서와 같이 템플릿 인스턴스에 영향을 줍니다.
   >
   >
   에 대한 변경 사항 **/apps/&lt;website>/components/&lt;component-name>** 노드는 템플릿 사용 시 작성된 콘텐츠 페이지에 영향을 줍니다.

   이제 새 템플릿을 사용하여 웹 사이트 내에서 페이지를 만들 수 있습니다.

>[!NOTE]
>
편집기 클라이언트 라이브러리는 `cq.shared` 컨텐츠 페이지의 네임스페이스 및 네임스페이스가 없는 경우 JavaScript 오류가 발생합니다 `Uncaught TypeError: Cannot read property 'shared' of undefined` 결과.
>
모든 샘플 콘텐츠 페이지에는 다음이 포함되어 있습니다. `cq.shared`, 따라서 이를 기반으로 하는 모든 컨텐츠는 자동으로 다음을 포함합니다 `cq.shared`. 그러나 샘플 콘텐츠를 기반으로 하지 않고 처음부터 고유한 콘텐츠 페이지를 만들려는 경우에는 다음을 포함해야 합니다. `cq.shared` 네임스페이스입니다.
>
다음을 참조하십시오 [클라이언트측 라이브러리 사용](/help/sites-developing/clientlibs.md) 추가 정보.

## 기존 템플릿 사용 가능 {#making-an-existing-template-available}

이 예에서는 특정 콘텐츠 경로에 템플릿을 사용할 수 있도록 허용하는 방법을 보여 줍니다. 페이지를 만들 때 페이지 작성자가 사용할 수 있는 템플릿은에 정의된 논리에 의해 결정됩니다. [템플릿 가용성](/help/sites-developing/templates.md#template-availability).

1. CRXDE Lite에서 페이지에 사용할 템플릿(예: 뉴스레터 템플릿)으로 이동합니다.
1. 변경 `allowedPaths` 다음에 사용되는 속성 및 기타 속성 [템플릿 가용성](/help/sites-developing/templates.md#template-availability). 예를 들어, `allowedPaths`: `/content/geometrixx-outdoors/[^/]+(/.*)?` 은(는) 이 템플릿이 아래의 모든 경로에서 허용됨을 의미합니다 `/content/geometrixx-outdoors`.

   ![chlimage_1-89](assets/chlimage_1-89.png)
