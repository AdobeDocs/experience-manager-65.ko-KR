---
title: 페이지 템플릿 - 정적
seo-title: 페이지 템플릿 - 정적
description: 템플릿은 페이지를 만드는 데 사용되며 선택한 범위 내에서 사용할 수 있는 구성 요소를 정의합니다.
seo-description: 템플릿은 페이지를 만드는 데 사용되며 선택한 범위 내에서 사용할 수 있는 구성 요소를 정의합니다.
uuid: 7a473c19-9565-476e-9e54-ab179da04d71
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cfd90e8f-9b9b-4d0b-be31-828469b961de
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# 페이지 템플릿 - 정적{#page-templates-static}

템플릿은 페이지를 만드는 데 사용되며 선택한 범위 내에서 사용할 수 있는 구성 요소를 정의합니다. 템플릿은 만들 페이지와 동일한 구조를 가지지만 실제 컨텐츠가 없는 노드의 계층입니다.

각 템플릿은 사용할 수 있는 구성 요소 선택 사항을 제공합니다.

* 템플릿은 구성 요소로 [구성됩니다](/help/sites-developing/components.md).
* 구성 요소는 위젯을 사용하고 액세스를 허용하며 이러한 위젯은 컨텐츠를 렌더링하는 데 사용됩니다.

>[!NOTE]
>
>[편집 가능한 템플릿은](/help/sites-developing/page-templates-editable.md) 사용 가능하며 가장 유연하고 최신 기능을 위해 권장되는 템플릿 유형입니다.

## 템플릿의 속성 및 하위 노드 {#properties-and-child-nodes-of-a-template}

템플릿은 cq:Template 유형의 노드이며 다음 속성과 자식 노드를 포함합니다.

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
   <td>현재 템플릿을 참조하십시오. 템플릿은 cq:Template 노드 유형입니다.<br /> </td>
  </tr>
  <tr>
   <td> allowedChildren </td>
   <td> String[]</td>
   <td>Path of a template that is allowed to be a child of this template.<br /> </td>
  </tr>
  <tr>
   <td> allowedParents</td>
   <td> String[]</td>
   <td>Path of a template that is allowed to be a parent of this template.<br /> </td>
  </tr>
  <tr>
   <td> allowedPaths</td>
   <td> String[]</td>
   <td>이 템플릿을 기반으로 할 수 있는 페이지의 경로입니다.<br /> </td>
  </tr>
  <tr>
   <td> jcr:created</td>
   <td> 날짜</td>
   <td>템플릿 작성 날짜.<br /> </td>
  </tr>
  <tr>
   <td> jcr:description</td>
   <td> 문자열</td>
   <td>템플릿에 대한 설명입니다.<br /> </td>
  </tr>
  <tr>
   <td> jcr:title</td>
   <td> 문자열</td>
   <td>Title of the template.<br /> </td>
  </tr>
  <tr>
   <td> 순위</td>
   <td> 긴</td>
   <td>템플릿의 등급입니다. 사용자 인터페이스에 템플릿을 표시하는 데 사용됩니다.<br /> </td>
  </tr>
  <tr>
   <td> jcr:content</td>
   <td> cq:PageContent</td>
   <td>템플릿의 컨텐츠를 포함하는 노드입니다.<br /> </td>
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

페이지를 만들려면 템플릿을 사이트 트리의 해당 위치에 복사해야 합니다(노드 트리 `/apps/<myapp>/template/<mytemplate>`).웹 사이트 탭을 사용하여 페이지를 만들면 **이렇게** 됩니다.

또한 이 복사 작업은 페이지의 초기 컨텐츠(일반적으로 최상위 컨텐츠 전용)와 페이지 렌더링에 사용되는 페이지 구성 요소의 경로(하위 노드 jcr:content의 모든 것)인 sling:resourceType 속성을 제공합니다.

## 템플릿 구성 방법 {#how-templates-are-structured}

고려해야 할 두 가지 측면이 있습니다.

* 템플릿 자체의 구조
* 템플릿을 사용할 때 생성된 컨텐츠의 구조

### 템플릿 구조 {#the-structure-of-a-template}

템플릿은 cq:Template 유형의 노드 아래에 **만들어집니다**.

![screen_shot_2012-02-13at63646pm](assets/screen_shot_2012-02-13at63646pm.png)

특히 다음과 같은 다양한 속성을 설정할 수 있습니다.

* **jcr:title** - 템플릿의 제목;을 클릭합니다.
* **jcr:description** - 템플릿에 대한 설명;을 클릭합니다.

이 노드에는 결과 페이지의 컨텐츠 노드의 기초로 사용되는 jcr:content(cq:PageContent) 노드가 포함되어 있습니다.이 참조는 새 페이지의 실제 컨텐츠를 렌더링하는 데 사용할 구성 요소인 sling:resourceType을 사용하여 참조합니다.

![screen_shot_2012-02-13at64010pm](assets/screen_shot_2012-02-13at64010pm.png)

이 구성 요소는 새 페이지를 만들 때 컨텐츠의 구조와 디자인을 정의하는 데 사용됩니다.

![screen_shot_2012-02-13at64137pm](assets/screen_shot_2012-02-13at64137pm.png)

### 템플릿으로 제작한 컨텐츠 {#the-content-produced-by-a-template}

템플릿은 유형 페이지를 만드는 데 사용됩니다(앞에서 언급한 `cq:Page` 것처럼 페이지는 특별한 구성 요소 유형임). 각 AEM 페이지에는 구조화된 노드가 `jcr:content`있습니다. 다음과 같습니다.

* 의 유형이 cq:PageContent임
* 은 정의된 컨텐츠 정의를 포함하는 구조화된 노드 유형입니다.
* 컨텐츠 렌더링에 사용되는 슬링 스크립트를 `sling:resourceType` 포함하는 구성 요소를 참조하는 속성이 있습니다.

### 기본 템플릿 {#default-templates}

AEM에는 즉시 사용할 수 있는 다양한 기본 템플릿이 포함되어 있습니다. 경우에 따라 템플릿을 그대로 사용할 수도 있습니다. 이 경우 템플릿을 웹 사이트에 사용할 수 있어야 합니다.

예를 들어 AEM에는 콘텐츠 페이지 및 홈 페이지를 비롯한 여러 템플릿이 포함되어 있습니다.

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

대부분의 경우 기존 템플릿을 가져와 직접 사용할 수 있도록 새 템플릿을 개발할 수 있습니다. 자세한 [내용은 페이지 템플릿](#developing-page-templates) 개발을 참조하십시오.

웹 사이트에 대한 기존 템플릿을 활성화하고 웹 사이트 **콘솔에서 웹 사이트** 바로 아래에 페이지를 만들 때 페이지 만들기 **대화** 상자에 **표시하려면** 템플릿 노드의allowedPaths 속성을 다음으로 설정합니다. **/content(/)*)?**

## 템플릿 디자인 적용 방법 {#how-template-designs-are-applied}

디자인 모드를 사용하여 UI에서 스타일을 [정의하면](/help/sites-authoring/default-components-designmode.md)디자인이 스타일이 정의된 컨텐츠 노드의 정확한 경로로 유지됩니다.

>[!CAUTION]
>
>디자인 모드를 통해서만 디자인을 적용할 [것을 권장합니다](/help/sites-authoring/default-components-designmode.md).
>
>예를 들어, CRX DE에서 디자인을 수정하는 것은 좋지 않으며, 그러한 디자인의 애플리케이션은 예상 동작과 다를 수 있습니다.

디자인 모드를 사용해서만 디자인이 적용되는 경우 다음 섹션, 디자인 [경로 해상도](/help/sites-developing/page-templates-static.md#design-path-resolution), [의사 결정 트리](/help/sites-developing/page-templates-static.md#decision-tree)및 [예는](/help/sites-developing/page-templates-static.md#example) 적용되지않습니다.

### 디자인 패스 해상도 {#design-path-resolution}

정적 템플릿을 기반으로 컨텐츠를 렌더링할 때 AEM은 컨텐츠 계층 구조의 탐색을 기반으로 컨텐츠에 가장 연관성 높은 디자인과 스타일을 적용하려고 시도합니다.

AEM 파섹

* 디자인 모드에서 디자인이 정의된 경우와 같이 컨텐츠 노드의 전체 및 정확한 경로에 대한 디자인이 있는 경우 해당 디자인을 사용합니다.
* 상위의 컨텐츠 노드에 대한 디자인이 있으면 해당 디자인을 사용합니다.
* 컨텐츠 노드의 경로에 노드에 대한 디자인이 있으면 해당 디자인을 사용합니다.

마지막 두 경우, 적용 가능한 디자인이 두 개 이상 있을 경우 컨텐츠 노드에 가장 가까운 디자인을 사용하십시오.

### 의사 결정 트리 {#decision-tree}

디자인 경로 해상도 [로직을 그래픽으로 표시합니다](/help/sites-developing/page-templates-static.md#design-path-resolution) .

![design_path_resolution](assets/design_path_resolution.png)

### 예 {#example}

디자인이 노드에 적용될 수 있는 간단한 컨텐츠 구조를 다음과 같이 생각해 보십시오.

`/root/branch/leaf`

다음 표에서는 AEM에서 디자인을 선택하는 방법에 대해 설명합니다.

<table>
 <tbody>
  <tr>
   <td><strong>디자인 찾기<br /> </strong></td>
   <td><strong>Designs Exist For<br /> </strong></td>
   <td><strong>선택한 디자인<br /> </strong></td>
   <td><strong>주석</strong></td>
  </tr>
  <tr>
   <td><code class="code">leaf
      </code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> <p><code>leaf</code></p> </td>
   <td><code>leaf</code></td>
   <td>가장 정확한 일치 항목은 항상 수행됩니다.<br /> </td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> </td>
   <td><code>branch</code></td>
   <td>나무 아래에서 가장 가까운 매치로 다시 내려가라.</td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><code>root</code></td>
   <td><code>root</code></td>
   <td>다른 모든 것이 실패한다면 남은 것을 가져가라.<br /> </td>
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
   <td><p>정확히 일치하는 것이 없으면 나무 아래에 있는 것을 가져가세요.</p> <p>이는 항상 적용 가능하지만 트리 위쪽은 너무 구체적일 수 있다는 가정입니다.<br /> </p> </td>
  </tr>
 </tbody>
</table>

## 페이지 템플릿 개발 {#developing-page-templates}

AEM 페이지 템플릿은 단순히 새 페이지를 만드는 데 사용되는 모델입니다. 필요한 속성(주로 sling:resourceType)을 사용하여 편집 및 렌더링을 허용하도록 설정하여 초기 컨텐츠를 거의 또는 필요한 만큼 포함할 수 있습니다.

### 새 템플릿 만들기(기존 템플릿 기반) {#creating-a-new-template-based-on-an-existing-template}

새 템플릿을 처음부터 완전히 만들 수 있지만 기존 템플릿을 복사하여 업데이트하면 시간과 노력을 절약할 수 있습니다. 예를 들어 Geometrixx 내의 템플릿을 사용하여 시작할 수 있습니다.

기존 템플릿을 기반으로 새 템플릿을 만들려면:

1. 기존 템플릿(가능한 한 원하는 것과 가깝게 정의되는 것)을 새 노드에 복사합니다.

   템플릿은 일반적으로 **/apps/&lt;website-name>/templates/&lt;template-name>에 저장됩니다**.

   >[!NOTE]
   >
   >사용 가능한 템플릿 목록은 새 페이지의 위치 및 각 템플릿에 지정된 배치 제한에 따라 달라집니다. 템플릿 [가용성을 참조하십시오](#templateavailibility).

1. 새 **역할을 반영하도록 새 템플릿 노드의 jcr:title** 속성을 변경합니다. 해당되는 경우 jcr: **description** 을 업데이트할 수도 있습니다. 페이지의 템플릿 가용성을 적절히 변경해야 합니다.

   >[!NOTE]
   >
   >웹 사이트 콘솔에서 웹 사이트 바로 아래에 페이지를 만들 때 페이지 **만들기** 대화 **** 상자에 **템플릿을** 표시하려면 `allowedPaths` 템플릿노드의속성을 다음으로 설정합니다. `/content(/.*)?`

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. 템플릿 기반이 되는 구성 요소를 복사하여(템플릿 내의 **jcr:content** 노드의 sling:resourceType **속성으로 표시됨)** 새 인스턴스를 만듭니다.

   구성 요소는 일반적으로 **/apps/&lt;website-name>/components/&lt;component-name>에 저장됩니다**.

1. 새 **구성 요소의 jcr:title** 및 **jcr:description** 을 업데이트합니다.
1. 템플릿 선택 목록에 새 축소판 그림을 표시하려면 thumbnail.png를 바꿉니다(크기 128 x 98px).
1. 템플릿 **jcr:content** 노드의 sling:resourceType을 **** 업데이트하여 새 구성 요소를 참조합니다.
1. 템플릿 및/또는 기본 구성 요소의 기능 또는 디자인을 추가로 변경합니다.

   >[!NOTE]
   >
   >/apps/&lt;website>/templates/&lt;template-name> **** 노드에 대한 변경 사항은 템플릿 인스턴스에 영향을 줍니다(선택 목록에서처럼).
   /apps/&lt;website>/components/&lt;component-name> **** 노드에 대한 변경 사항은 템플릿이 사용될 때 생성된 컨텐츠 페이지에 영향을 줍니다.

   이제 새 템플릿을 사용하여 웹 사이트 내에서 페이지를 만들 수 있습니다.

>[!NOTE]
편집기 클라이언트 라이브러리는 컨텐츠 페이지에 `cq.shared` 네임스페이스가 있다고 가정하고, 없으면 JavaScript 오류가 `Uncaught TypeError: Cannot read property 'shared' of undefined` 발생합니다.
모든 샘플 컨텐츠 페이지에 `cq.shared`포함되어 있으므로 이를 기반으로 하는 모든 컨텐츠가 자동으로 포함됩니다 `cq.shared`. 그러나 샘플 컨텐츠를 기반으로 하지 않고 컨텐츠 페이지를 처음부터 새로 만들려면 `cq.shared` 네임스페이스를 포함해야 합니다.
자세한 [내용은 클라이언트측 라이브러리](/help/sites-developing/clientlibs.md) 사용을 참조하십시오.

## 기존 템플릿 사용 가능 {#making-an-existing-template-available}

이 예에서는 특정 컨텐츠 경로에 템플릿을 사용하는 방법을 보여 줍니다. 새 페이지를 만들 때 페이지 작성자가 사용할 수 있는 템플릿은 템플릿 가용성에 정의된 논리로 [결정됩니다](/help/sites-developing/templates.md#template-availability).

1. CRXDE Lite에서 뉴스레터 템플릿과 같이 페이지에 사용할 템플릿으로 이동합니다.
1. 사용 가능한 `allowedPaths` 템플릿에 [사용된 속성 및 기타 속성을 변경합니다](/help/sites-developing/templates.md#template-availability). 예를 들어 `allowedPaths`:즉, `/content/geometrixx-outdoors/[^/]+(/.*)?` 이 템플릿은 모든 경로에서 사용할 수 `/content/geometrixx-outdoors`있습니다.

   ![chlimage_1-89](assets/chlimage_1-89.png)
