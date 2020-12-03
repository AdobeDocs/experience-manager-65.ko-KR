---
title: 페이지 템플릿 - 정적
seo-title: 페이지 템플릿 - 정적
description: 템플릿은 페이지를 만드는 데 사용되고 선택한 범위 내에서 사용할 수 있는 구성 요소를 정의합니다
seo-description: 템플릿은 페이지를 만드는 데 사용되고 선택한 범위 내에서 사용할 수 있는 구성 요소를 정의합니다
uuid: 7a473c19-9565-476e-9e54-ab179da04d71
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cfd90e8f-9b9b-4d0b-be31-828469b961de
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 8%

---


# 페이지 템플릿 - 정적{#page-templates-static}

템플릿은 페이지를 만드는 데 사용되고 선택한 범위 내에서 사용할 수 있는 구성 요소를 정의합니다. 템플릿은 만들 페이지와 동일한 구조를 가지지만 실제 컨텐츠가 없는 노드 계층 구조입니다.

각 템플릿에는 사용할 수 있는 구성 요소 선택 사항이 표시됩니다.

* 템플릿은 [구성 요소](/help/sites-developing/components.md);으로 구성됩니다.
* 구성 요소는 위젯을 사용하고 액세스를 허용하며, 이러한 위젯은 컨텐츠를 렌더링하는 데 사용됩니다.

>[!NOTE]
>
>[편집 가능한 템플릿](/help/sites-developing/page-templates-editable.md) 을 사용할 수 있으며 가장 유연하고 최신 기능을 위해 권장되는 템플릿 유형입니다.

## 템플릿 {#properties-and-child-nodes-of-a-template}의 속성 및 하위 노드

템플릿은 cq:Template 유형의 노드이며 다음 속성과 하위 노드를 포함합니다.

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
   <td>현재 템플릿을 참조하십시오. 템플릿은 cq:Template 노드 형식입니다.<br /> </td>
  </tr>
  <tr>
   <td> allowedChildren </td>
   <td> String[]</td>
   <td>이 템플릿의 자식일 수 있는 템플릿의 경로입니다.<br /> </td>
  </tr>
  <tr>
   <td> allowedParents</td>
   <td> 문자열[]</td>
   <td>이 템플릿의 상위 템플릿으로 사용할 수 있는 템플릿의 경로입니다.<br /> </td>
  </tr>
  <tr>
   <td> allowedPaths</td>
   <td> 문자열[]</td>
   <td>이 템플릿을 기반으로 할 수 있는 페이지의 경로입니다.<br /> </td>
  </tr>
  <tr>
   <td> jcr:created</td>
   <td> 날짜</td>
   <td>템플릿 생성 날짜입니다.<br /> </td>
  </tr>
  <tr>
   <td> jcr:description</td>
   <td> 문자열</td>
   <td>템플릿에 대한 설명입니다.<br /> </td>
  </tr>
  <tr>
   <td> jcr:title</td>
   <td> 문자열</td>
   <td>템플릿의 제목입니다.<br /> </td>
  </tr>
  <tr>
   <td> 순위</td>
   <td> 긴</td>
   <td>템플릿의 등급. 사용자 인터페이스에 템플릿을 표시하는 데 사용됩니다.<br /> </td>
  </tr>
  <tr>
   <td> jcr:content</td>
   <td> cq:PageContent</td>
   <td>템플릿의 콘텐츠를 포함하는 노드입니다.<br /> </td>
  </tr>
  <tr>
   <td> thumbnail.png</td>
   <td> nt:파일</td>
   <td>템플릿의 축소판입니다.<br /> </td>
  </tr>
  <tr>
   <td> icon.png</td>
   <td> nt:파일</td>
   <td>템플릿의 아이콘입니다.<br /> </td>
  </tr>
 </tbody>
</table>

템플릿은 페이지의 기준입니다.

페이지를 만들려면 템플릿을 사이트 트리의 해당 위치에 복사해야 합니다(node-tree `/apps/<myapp>/template/<mytemplate>`).이 작업은 페이지가 **웹 사이트** 탭을 사용하여 만들어지면 발생합니다.

또한 이 복사 작업은 페이지의 초기 컨텐츠(일반적으로 최상위 컨텐츠 전용) 및 페이지 렌더링에 사용되는 페이지 구성 요소의 경로(하위 노드 jcr:content)인 sling:resourceType 속성을 제공합니다.

## 템플릿 구성 방법 {#how-templates-are-structured}

고려해야 할 두 가지 측면이 있습니다.

* 템플릿 자체의 구조
* 템플릿을 사용할 때 생성된 컨텐츠의 구조

### 템플릿 {#the-structure-of-a-template} 구조

템플릿은 **cq:Template** 유형의 노드 아래에 만들어집니다.

![screen_shot_2012-02-13at63646pm](assets/screen_shot_2012-02-13at63646pm.png)

다양한 속성을 설정할 수 있습니다. 특히

* **jcr:title** - 템플릿의 title;을 클릭합니다.
* **jcr:description** - template;을 클릭합니다.

이 노드에는 결과 페이지의 컨텐츠 노드의 기초로 사용되는 jcr:content(cq:PageContent) 노드가 포함되어 있습니다.이 참조는 새 페이지의 실제 컨텐츠를 렌더링하는 데 사용할 구성 요소인 sling:resourceType을 사용합니다.

![screen_shot_2012-02-13at64010pm](assets/screen_shot_2012-02-13at64010pm.png)

이 구성 요소는 새 페이지를 만들 때 컨텐츠의 구조와 디자인을 정의하는 데 사용됩니다.

![screen_shot_2012-02-13at64137pm](assets/screen_shot_2012-02-13at64137pm.png)

### 템플릿 {#the-content-produced-by-a-template}에 의해 생성된 컨텐트

템플릿은 `cq:Page` 유형의 페이지를 만드는 데 사용됩니다(앞에서 언급했듯이 페이지는 구성 요소의 특수 유형임). 각 AEM 페이지에는 구조화된 노드 `jcr:content`이(가) 있습니다. 이 기능은

* 은 cq:PageContent 유형임
* 은 정의된 컨텐츠 정의를 포함하는 구조화된 노드 유형입니다.
* 컨텐츠 렌더링에 사용되는 sling 스크립트를 포함하는 구성 요소를 참조하는 속성 `sling:resourceType`이 있습니다.

### 기본 템플릿 {#default-templates}

AEM에는 기본적으로 제공되는 다양한 기본 템플릿이 포함되어 있습니다. 경우에 따라 템플릿을 그대로 사용할 수도 있습니다. 이 경우 웹 사이트에서 템플릿을 사용할 수 있어야 합니다.

예를 들어 AEM에는 컨텐츠 페이지 및 홈 페이지를 비롯한 여러 템플릿이 포함되어 있습니다.

| **제목** | **구성 요소** | **위치** | **목적** |
|---|---|---|---|
| 홈페이지 | 홈 페이지 | geometrixx | Geometrixx 홈 페이지 템플릿입니다. |
| 컨텐트 페이지 | contentpage | geometrixx | Geometrixx 컨텐트 페이지 템플릿입니다. |

#### 기본 템플릿 표시 {#displaying-default-templates}

저장소의 모든 템플릿 목록을 보려면 다음과 같이 진행하십시오.

1. CRXDE Lite에서 **도구** 메뉴를 열고 **쿼리**&#x200B;를 클릭합니다.

1. 쿼리 탭에서 다음을 수행합니다.
1. **Type**&#x200B;으로 **XPath**&#x200B;를 선택합니다.

1. **쿼리** 입력 필드에 다음 문자열을 입력합니다.
//element(*, cq:Template)

1. **실행**&#x200B;을 클릭합니다. 결과 상자에 목록이 표시됩니다.

대부분의 경우 기존 템플릿을 가져와 직접 사용할 수 있도록 새 템플릿을 개발할 수 있습니다. 자세한 내용은 [페이지 템플릿 개발](#developing-page-templates)을 참조하십시오.

웹 사이트에 대한 기존 템플릿을 활성화하고 **웹 사이트** 콘솔의 **웹 사이트** 아래에 페이지를 만들 때 **페이지 만들기** 대화 상자에 표시하려면 템플릿 노드의 allowedPaths 속성을 다음으로 설정합니다.**/content(/)*)?**

## 템플릿 디자인이 적용되는 방법 {#how-template-designs-are-applied}

[디자인 모드](/help/sites-authoring/default-components-designmode.md)를 사용하여 UI에서 스타일이 정의되면 디자인이 스타일이 정의되는 컨텐츠 노드의 정확한 경로로 유지됩니다.

>[!CAUTION]
>
>Adobe은 [디자인 모드](/help/sites-authoring/default-components-designmode.md)를 통해서만 디자인을 적용할 것을 권장합니다.
>
>예를 들어, CRX DE에서 디자인을 수정하는 것은 좋지 않으며, 그러한 디자인의 애플리케이션은 예상 동작과 다를 수 있습니다.

디자인이 디자인 모드에서만 적용되는 경우, 다음 섹션인 [디자인 경로 해상도](/help/sites-developing/page-templates-static.md#design-path-resolution), [의사 결정 트리](/help/sites-developing/page-templates-static.md#decision-tree) 및 [예제](/help/sites-developing/page-templates-static.md#example)를 적용할 수 없습니다.

### 디자인 경로 해상도 {#design-path-resolution}

정적 템플릿을 기반으로 컨텐츠를 렌더링할 때 AEM은 컨텐츠 계층 구조의 탐색을 기반으로 컨텐츠에 가장 연관성 높은 디자인과 스타일을 적용하려고 시도합니다.

AEM은 다음 순서로 컨텐트 노드에 대해 가장 관련성이 높은 스타일을 결정합니다.

* 컨텐츠 노드의 전체 경로 및 정확한 경로에 대한 디자인이 있는 경우(디자인 모드에서 디자인이 정의된 경우와 마찬가지로) 해당 디자인을 사용합니다.
* 상위의 컨텐츠 노드에 대한 디자인이 있으면 해당 디자인을 사용하십시오.
* 컨텐츠 노드의 경로에 노드에 대한 디자인이 있는 경우 해당 디자인을 사용합니다.

마지막 두 경우, 적용 가능한 디자인이 두 개 이상 있을 경우 컨텐츠 노드에 가장 가까운 디자인을 사용하십시오.

### 의사 결정 트리 {#decision-tree}

이것은 [디자인 경로 해상도](/help/sites-developing/page-templates-static.md#design-path-resolution) 로직을 그래픽으로 나타낸 것입니다.

![design_path_resolution](assets/design_path_resolution.png)

### 예 {#example}

디자인이 노드 중 하나에 적용될 수 있는 간단한 컨텐츠 구조를 다음과 같이 생각해 보십시오.

`/root/branch/leaf`

다음 표에서는 AEM에서 디자인을 선택하는 방법에 대해 설명합니다.

<table>
 <tbody>
  <tr>
   <td><strong>디자인 찾기<br /> </strong></td>
   <td><strong>디자인 존재 대상<br /> </strong></td>
   <td><strong>선택한 디자인<br /> </strong></td>
   <td><strong>주석</strong></td>
  </tr>
  <tr>
   <td><code class="code">leaf
      </code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> <p><code>leaf</code></p> </td>
   <td><code>leaf</code></td>
   <td>가장 정확한 검색은 항상 수행됩니다.<br /> </td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> </td>
   <td><code>branch</code></td>
   <td>나무에서 가장 가까운 매치 아래로 내려가세요.</td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><code>root</code></td>
   <td><code>root</code></td>
   <td>다른 모든 작업이 실패할 경우 남은 항목을 가져옵니다.<br /> </td>
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
   <td><p>정확히 일치하는 것이 없으면 나무 아래에 있는 것을 고르세요.</p> <p>이는 항상 적용할 수 있지만 트리 위쪽에서는 너무 구체적일 수 있다는 가정입니다.<br /> </p> </td>
  </tr>
 </tbody>
</table>

## 페이지 템플릿 개발 {#developing-page-templates}

AEM 페이지 템플릿은 단순히 새 페이지를 만드는 데 사용되는 모델입니다. 필요한 속성(주로 sling:resourceType)을 사용하여 편집하고 렌더링할 수 있도록 설정하여 초기 컨텐츠 거의 또는 필요한 만큼 이를 포함할 수 있습니다.

### 새 템플릿 만들기(기존 템플릿 기반) {#creating-a-new-template-based-on-an-existing-template}

새 템플릿을 처음부터 완전히 만들 수는 있지만 기존 템플릿을 복사하여 업데이트하면 시간과 노력을 절약할 수 있습니다. 예를 들어 Geometrixx 내의 템플릿을 사용하여 시작할 수 있습니다.

기존 템플릿을 기반으로 새 템플릿을 만들려면 다음을 수행하십시오.

1. 기존 템플릿을 새 노드에 복사합니다(가능한 한 가깝게 수행하려는 정의가 있는 경우).

   템플릿은 보통 **/apps/&lt;website-name>/templates/&lt;template-name>**&#x200B;에 저장됩니다.

   >[!NOTE]
   >
   >사용 가능한 템플릿 목록은 새 페이지의 위치와 각 템플릿에 지정된 배치 제한에 따라 다릅니다. [템플릿 가용성](#templateavailibility)을 참조하십시오.

1. 새 역할을 반영하도록 새 템플릿 노드의 **jcr:title**&#x200B;을 변경합니다. 해당하는 경우 **jcr:description**&#x200B;을 업데이트할 수도 있습니다. 페이지의 템플릿 가용성을 적절히 변경해야 합니다.

   >[!NOTE]
   >
   >**웹 사이트** 콘솔의 **웹 사이트** 바로 아래에 페이지를 만들 때 **페이지 만들기 대화 상자에 템플릿을 표시하려면 템플릿 노드의 `allowedPaths` 속성을 다음으로 설정하십시오.`/content(/.*)?`**

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. 템플릿 기반이 되는 구성 요소를 복사하여 새 인스턴스를 만듭니다(템플릿 내 **jcr:content** 노드의 **sling:resourceType** 속성으로 표시됨).

   구성 요소는 일반적으로 **/apps/&lt;website-name>/components/&lt;component-name>**&#x200B;에 저장됩니다.

1. 새 구성 요소의 **jcr:title** 및 **jcr:description**&#x200B;을 업데이트합니다.
1. 템플릿 선택 목록(크기 128 x 98px)에 새 축소판 그림을 표시하려면 thumbnail.png를 대체합니다.
1. 템플릿의 **jcr:content** 노드의 **sling:resourceType**&#x200B;을 업데이트하여 새 구성 요소를 참조합니다.
1. 템플릿 및/또는 기본 구성 요소의 기능 또는 디자인을 추가로 변경합니다.

   >[!NOTE]
   >
   >**/apps/&lt;website>/templates/&lt;template-name>** 노드에 대한 변경 사항은 템플릿 인스턴스(선택 목록)에 영향을 줍니다.
   **/apps/&lt;website>/components/&lt;component-name>** 노드에 대한 변경 사항은 템플릿이 사용될 때 만든 컨텐츠 페이지에 영향을 줍니다.

   이제 새 템플릿을 사용하여 웹 사이트 내에서 페이지를 만들 수 있습니다.

>[!NOTE]
편집기 클라이언트 라이브러리는 컨텐츠 페이지에 `cq.shared` 네임스페이스가 존재한다고 가정하고, 없으면 JavaScript 오류 `Uncaught TypeError: Cannot read property 'shared' of undefined`이 발생합니다.
모든 샘플 컨텐츠 페이지에는 `cq.shared`이(가) 포함되어 있으므로 이를 기반으로 하는 모든 컨텐츠에 자동으로 `cq.shared`이(가) 포함됩니다. 그러나 샘플 컨텐츠를 기준으로 하지 않고 직접 컨텐츠 페이지를 만드는 경우 `cq.shared` 네임스페이스를 포함해야 합니다.
자세한 내용은 [클라이언트측 라이브러리 사용](/help/sites-developing/clientlibs.md)을 참조하십시오.

## 기존 템플릿을 사용할 수 있게 만들기 {#making-an-existing-template-available}

이 예에서는 특정 컨텐츠 경로에 템플릿을 사용할 수 있는 방법을 보여 줍니다. 새 페이지를 만들 때 페이지 작성자가 사용할 수 있는 템플릿은 [템플릿 가용성](/help/sites-developing/templates.md#template-availability)에 정의된 논리로 결정됩니다.

1. CRXDE Lite에서 페이지에 사용할 템플릿(예: 뉴스레터 템플릿)으로 이동합니다.
1. `allowedPaths` 속성 및 [템플릿 available](/help/sites-developing/templates.md#template-availability)에 사용되는 기타 속성을 변경합니다. 예: `allowedPaths`:`/content/geometrixx-outdoors/[^/]+(/.*)?`은 이 템플릿이 `/content/geometrixx-outdoors` 아래의 모든 경로에서 허용됨을 의미합니다.

   ![chlimage_1-89](assets/chlimage_1-89.png)
