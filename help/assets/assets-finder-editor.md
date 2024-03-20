---
title: 자산 편집기 페이지 만들기 및 구성
description: 사용자 지정 에셋 편집기 페이지를 만들고 여러 에셋을 동시에 편집하는 방법을 알아봅니다.
contentOwner: AG
role: User, Admin
feature: Developer Tools,Asset Management
exl-id: 53e310a9-c511-447a-91bd-8c5b2760dc03
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2088'
ht-degree: 1%

---

# 자산 편집기 페이지 만들기 및 구성 {#creating-and-configuring-asset-editor-pages}

이 문서에서는 다음 사항에 대해 설명합니다.

* 사용자 지정된 자산 편집기 페이지를 만드는 이유
* 메타데이터를 보고 편집하고 에셋에 대한 작업을 수행할 수 있는 WCM 페이지인 에셋 편집기 페이지를 만들고 사용자 지정하는 방법입니다.
* 여러 자산을 동시에 편집하는 방법

<!-- TBD: Add UICONTROL tags. Need PM review. Flatten the structure a bit. Re-write to remove Geometrixx mentions and to adhere to 6.5 default samples. -->

>[!NOTE]
>
>자산 공유는 오픈 소스 참조 구현으로 사용할 수 있습니다. 다음을 참조하십시오 [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/). 공식적으로 지원되지 않습니다.

## 자산 편집기 페이지를 만들고 구성하는 이유는 무엇입니까? {#why-create-and-configure-asset-editor-pages}

Digital Asset Management 는 더 많은 시나리오에서 사용되고 있습니다. 전문 교육을 받은 소규모 사용자 그룹(예: 사진가 또는 분류학자)을 위한 소규모 솔루션에서 비즈니스 사용자, WCM 작성자 및 저널리스트와 같은 더 크고 다양한 사용자 그룹으로 이동할 때 의 강력한 사용자 인터페이스 [!DNL Adobe Experience Manager Assets] 은 너무 많은 정보를 제공할 수 있습니다. 이해 당사자는 특정 사용자 인터페이스 또는 애플리케이션에 관련성이 있는 디지털 에셋에 액세스하도록 요청하기 시작합니다.

이러한 자산 중심 애플리케이션은 직원들이 무역 박람회 방문 또는 공공 웹사이트의 프레스 센터에서 사진을 업로드할 수 있는 인트라넷의 간단한 사진 갤러리가 될 수 있습니다. 자산 중심 애플리케이션은 장바구니, 체크아웃 및 확인 프로세스를 포함한 완전한 솔루션으로도 확장할 수 있습니다.

에셋 중심 애플리케이션을 만들면 코딩이 필요 없고 사용자 그룹과 해당 요구 사항에 대한 지식과 사용 중인 메타데이터에 대한 지식만 있으면 되는 구성 프로세스가 됩니다. 을 사용하여 만든 자산 중심 애플리케이션 [!DNL Assets] 확장 가능: 중간 정도의 코딩 노력을 사용하여 자산을 검색, 보기 및 수정하기 위한 재사용 가능한 구성 요소를 만들 수 있습니다.

의 자산 중심 애플리케이션 [!DNL Experience Manager] 특정 에셋에 대한 자세한 보기를 가져오는 데 사용할 수 있는 에셋 편집기 페이지로 구성됩니다. 에셋에 액세스하는 사용자에게 필요한 권한이 있는 경우 에셋 편집기 페이지에서 메타데이터를 편집할 수도 있습니다.

<!--
## Create and configure an Asset Share page {#creating-and-configuring-an-asset-share-page}

You customize the DAM Finder functionality and create pages that have all the functionality you require, which are called Asset Share pages. To create an Asset Share page, you add the page using the Geometrixx Asset Share template and then you customize the actions users can perform on that page, determine how viewers see the assets, and decide how users can build their queries.

Here are some use cases for creating a customized Asset Share page:

* Press Center for Journalists.
* Image Search Engine for internal business users.
* Image Database for website users.
* Media Tagging Interface for metadata editors.

### Create an Asset Share page {#creating-an-asset-share-page}

To create an Asset Share page, you can either create it when you are working on web sites or from the digital asset manager.

>[!NOTE]
>
>By default, when you create an Asset Share page from **New** in the digital asset manager, an Asset viewer and Asset editor are automatically created for you.

To create an new Asset Share page in the **Websites** console:

1. In the **Websites** tab, navigate to the place where you want to create an asset share page and click **New**.

1. Select the **Asset Share** page and click **Create**. The new page is created and the asset share page is listed in the **Websites** tab.

![dam8](assets/dam8.png)

The basic page created using the Geometrixx DAM Asset Share template looks as follows:

![screen_shot_2012-04-18at115456am](assets/screen_shot_2012-04-18at115456am.png)

To customize your Asset Share page, you use elements from the sidekick and you also edit query builder properties. The page **Geometrixx Press Center** is a customized version of a page based on this template:

![screen_shot_2012-04-19at123048pm](assets/screen_shot_2012-04-19at123048pm.png)

To create an asset share page by way of the digital asset manager:

1. In the digital asset manager, in **New**, select **New Asset Share**.
1. In the **Title**, enter the name of the asset share page. If desired, enter a name for the URL.

   ![screen_shot_2012-04-19at23626pm](assets/screen_shot_2012-04-19at23626pm.png)

1. Double-click the asset share page to open it and configure the page.

   ![screen_shot_2012-04-19at24114pm](assets/screen_shot_2012-04-19at24114pm.png)

   By default, when you create an Asset Share page from **New**, an Asset viewer and Asset editor are automatically created for you.

#### Customize actions {#customizing-actions}

You can determine what actions users can perform on selected digital assets from a selection of predefined actions.

To add actions to the Asset Share page:

1. In the Asset Share page that you want to customize, click **Actions** in the sidekick.

The following actions are available:

 | Action | Description |
 |---|---|
 | [!UICONTROL Delete Action] | Users can delete the selected assets. |
 | [!UICONTROL Download Action] | Lets users download selected assets to their computers. |
 | [!UICONTROL Lightbox Action] | Saves assets to a "lightbox"   where you can perform other actions on them. This comes in handy when working   with assets across multiple pages. The lightbox can also be used as a   shopping cart for assets. |
 | [!UICONTROL Move Action] | Users can move the asset to another   location |
 | [!UICONTROL Tags Action] | Lets users add tags to selected assets |
 | [!UICONTROL View Asset Action] | Opens the asset in the Asset editor for   user manipulation. |

1. Drag the appropriate action to the **Actions** area on the page. Doing so creates a button that is used to execute that action.

![chlimage_1-159](assets/chlimage_1-387.png)

#### Determine how search results are presented {#determining-how-search-results-are-presented}

You determine how results are displayed from a predefined list of lenses.

To change how search results are viewed:

1. In the Asset Share page that you want to customize, click Search.

![chlimage_1](assets/assetshare3.png)

1. Drag the appropriate lens to the top center of the page. In the Press Center, the lenses are already available. Users press the appropriate lens icon to display search results as desired.

The following lenses are available:

| Lens | Description |
|---|---|
| **[!UICONTROL List Lens]** |Presents the assets in a list fashion with details. |
| **[!UICONTROL Mosaic Lens]** |Presents assets in a mosaic fashion. |

#### Mosaic Lens {#mosaic-lens}

![chlimage_1-160](assets/chlimage_1-388.png)

#### List Lens {#list-lens}

![chlimage_1-161](assets/chlimage_1-389.png)

#### Customize the Query Builder {#customizing-the-query-builder}

The query builder lets you enter search terms and create content for the Asset Share page. When you edit the query builder, you also get to determine how many search results are displayed per page, which asset editor opens when you double-click an asset, the path the query searches, and customizes nodetypes.

To customize the query builder:

1. In the Asset Share page that you want to customize, click **Edit** in the Query Builder. By default, the **General** tab opens.
1. Select the number of results per page, the path of the asset editor (if you have a customized asset editor) and the Actions title.

![screen_shot_2012-04-23at15055pm](assets/screen_shot_2012-04-23at15055pm.png)

1. Click the **Paths** tab. Enter a path or multiple paths that the search will run. These paths are overwritten if the user uses the Paths predicate.

![screen_shot_2012-04-23at15150pm](assets/screen_shot_2012-04-23at15150pm.png)

1. Enter another node type, if desired.

1. In the **Query Builder URL** field, you can override or wrap the query builder and enter the new servlet URLs with the existing query builder component. In the **Feed URL** field, you can override the Feed URL as well.

![screen_shot_2012-04-23at15313pm](assets/screen_shot_2012-04-23at15313pm.png)

1. In the **Text** field, enter the text you want to appear for results and page numbers of results. Click **OK** when finished making changes.

![screen_shot_2012-04-23at15300pm](assets/screen_shot_2012-04-23at15300pm.png)

#### Add predicates {#adding-predicates}

Experience Manager Assets includes several predicates that you can add to the Asset Share page. These let your users further narrow searches. In some cases, they may override a query builder parameter (for example, the Path parameter).

To add predicates:

1. In the Asset Share page that you want to customize, click **Search**.

![assetshare3](assets/assetshare3.png)

1. Drag the appropriate predicates to the Asset Share page underneath the query builder. Doing so creates the appropriate fields.

![assetshare4](assets/assetshare4.png)

The following predicates are available:

| Predicate | Description |
|---|---|
| **[!UICONTROL Date Predicate]** |Lets users search for assets that were modified before and after certain dates. |
| **[!UICONTROL Options Predicate]** |The site owner can specify a property to search for (as in the property predicate, for example, cq:tags) and a content tree to populate the options from (for example, the tag tree). Doing so generates a list of options where the users can select the values (tags) that the selected property (tag property) should have. This predicate lets you build list controls like the list of tags, file types, image orientations, and so on. It is great for a fixed set of options. |
| **[!UICONTROL Path Predicate]** |Lets users define the path and subfolders, if desired. |
| **[!UICONTROL Property Predicate]** |The site owner specifies a property to search for, for example, tiff:ImageLength and the user can then enter a value, for example, 800. This returns all images that are 800 pixels high. Useful predicate if your property can have arbitrary values. |

For more information, see the [predicate Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html).

1. To configure the predicate further, double-click it. For example, when you open the Path Predicate, you need to assign the root path.

![screen_shot_2012-04-23at15640pm](assets/screen_shot_2012-04-23at15640pm.png)
-->

## 자산 편집기 페이지 만들기 및 구성 {#creating-and-configuring-an-asset-editor-page}

에셋 편집기를 사용자 정의하여 사용자가 디지털 에셋을 보고 편집할 수 있는 방법을 결정할 수 있습니다. 이렇게 하려면 자산 편집기 페이지를 만든 다음 사용자가 해당 페이지에서 수행할 수 있는 보기 및 작업을 사용자 지정합니다.

>[!NOTE]
>
>DAM 자산 편집기에 사용자 지정 필드를 추가하려면 새로 추가합니다 `cq:Widget` 노드 대상 `/apps/dam/content/asseteditors.`

### 자산 편집기 페이지 만들기 {#creating-the-asset-editor-page}

자산 편집기 페이지를 만들 때 좋은 방법은 자산 공유 페이지 바로 아래에 페이지를 만드는 것입니다.

자산 편집기 페이지를 만들려면 다음 작업을 수행하십시오.

1. 다음에서 **[!UICONTROL 웹 사이트]** 탭에서 에셋 편집기 페이지를 만들 위치로 이동하여 **신규**.
1. 선택 **Geometrixx 자산 편집기** 및 클릭 **만들기**. 새 페이지가 만들어지고에 페이지가 나열됩니다. **웹 사이트** 탭.

![screen_shot_2012-04-23at15858pm](assets/screen_shot_2012-04-23at15858pm.png)

Geometrixx 에셋 편집기 템플릿을 사용하여 만든 기본 페이지는 다음과 같습니다.

![assetshare5](assets/assetshare5.png)

자산 편집기 페이지를 사용자 지정하려면 사이드 킥의 요소를 사용하십시오. 에서 액세스되는 자산 편집기 페이지 **Geometrixx 프레스 센터** 는 이 템플릿을 기반으로 하는 페이지의 사용자 지정 버전입니다.

![assetshare6](assets/assetshare6.png)

#### 자산 공유 페이지에서 열 자산 편집기 설정 {#setting-which-asset-editor-opens-from-an-asset-share-page}

사용자 지정된 에셋 편집기 페이지를 만든 후 에셋을 더블 클릭하면 만든 사용자 지정된 에셋 공유가 사용자 지정된 편집기 페이지에서 에셋을 여십시오.

자산 편집기 페이지를 설정하려면 다음을 수행하십시오.

1. Asset Share 페이지에서 **편집** 쿼리 빌더 옆에 있습니다.

![screen_shot_2012-04-23at20123pm](assets/screen_shot_2012-04-23at20123pm.png)

1. 다음을 클릭합니다. **일반** 아직 선택하지 않은 경우 탭합니다.

1. 다음에서 **자산 편집기 경로** 필드에서 에셋 공유 페이지에서 에셋을 열 에셋 편집기 경로를 입력하고 를 클릭합니다 **확인**.

![screen_shot_2012-04-23at21653pm](assets/screen_shot_2012-04-23at21653pm.png)

#### 자산 편집기 구성 요소 추가 {#adding-asset-editor-components}

페이지에 구성 요소를 추가하여 자산 편집기의 기능을 결정합니다.

자산 편집기 구성 요소를 추가하려면:

1. 사용자 지정할 자산 편집기 페이지에서 을 선택합니다 **자산 편집기** 사이드 킥에서. 사용 가능한 모든 에셋 편집기 구성 요소가 표시됩니다.

>[!NOTE]
>
>사용자 지정할 수 있는 내용은 사용 가능한 구성 요소에 따라 다릅니다. 구성 요소를 활성화하려면 디자인 모드로 이동하여 활성화해야 하는 구성 요소를 선택합니다.

1. 사이드 킥에서 구성 요소를 자산 편집기로 드래그하고 구성 요소 대화 상자에서 편집을 수행합니다. 구성 요소는 다음 표에 설명되어 있으며 다음의 세부 지침에 설명되어 있습니다.

>[!NOTE]
>
>에셋 편집기 페이지를 디자인할 때 읽기 전용이거나 편집 가능한 구성 요소를 만듭니다. 사용자는 연필 이미지가 해당 구성 요소에 표시되면 필드를 편집할 수 있다는 것을 알고 있습니다. 기본적으로 대부분의 구성 요소는 읽기 전용으로 설정됩니다.

| 구성 요소 | 설명 |
|---|---|
| **[!UICONTROL 메타데이터 양식] 및 [!UICONTROL 메타데이터 텍스트 필드]** | 에셋에 메타데이터를 더 추가하고, 해당 에셋에서 제출 등의 작업을 수행할 수 있습니다. |
| **[!UICONTROL 하위 자산]** | 하위 자산을 사용자 지정할 수 있습니다. |
| **태그** | 사용자가 태그를 선택하고 에셋에 추가할 수 있습니다. |
| **[!UICONTROL 썸네일]** | 에셋의 썸네일, 해당 파일 이름을 표시하고 대체 텍스트를 추가할 수 있습니다. 여기에서 자산 편집기 작업을 추가할 수도 있습니다. |
| **[!UICONTROL 제목]** | 사용자 정의할 수 있는 자산 제목을 표시합니다. |

![screen_shot_2012-04-23at22743pm](assets/screen_shot_2012-04-23at22743pm.png)

#### 메타데이터 양식 및 텍스트 필드 - 메타데이터 구성 요소 보기 구성 {#metadata-form-and-text-field-configuring-the-view-metadata-component}

메타데이터 양식은 시작 및 종료 작업을 포함하는 양식입니다. 그 사이에 를 입력합니다. **텍스트** 필드. 다음을 참조하십시오 [Forms](/help/sites-authoring/default-components-foundation.md#form-component) 양식 작업에 대한 자세한 내용을 참조하십시오.

1. 다음을 클릭하여 시작 작업 만들기 **편집** 를 입력합니다. 원하는 경우 상자 제목을 입력할 수 있습니다. 기본적으로 상자 제목은 입니다. **메타데이터**. 검증용 JavaScript 클라이언트 코드를 생성하려면 클라이언트 검증(Client Validation) 확인란을 선택합니다.

![screen_shot_2012-04-23at22911pm](assets/screen_shot_2012-04-23at22911pm.png)

1. 을(를) 클릭하여 종료 작업을 만듭니다. **편집** 를 입력합니다. 예를 들어 다음을 만들 수 있습니다 **[!UICONTROL 제출]** 사용자가 메타데이터 변경 사항을 제출할 수 있도록 허용하는 옵션입니다. 선택적으로 다음을 추가할 수 있습니다. **재설정** 메타데이터를 원래 상태로 재설정하는 옵션입니다.

![screen_shot_2012-04-23at23138pm](assets/screen_shot_2012-04-23at23138pm.png)

1. 다음 사이 **양식 시작** 및 **양식 끝**&#x200B;메타데이터 텍스트 필드를 양식으로 드래그합니다. 사용자는 이러한 텍스트 필드에 메타데이터를 채우고, 다른 작업을 제출하거나 완료할 수 있습니다.

1. 필드 이름을 두 번 클릭합니다. 예: **제목** 메타데이터 필드를 열고 변경합니다. 다음에서 **일반** 의 탭 **구성 요소 편집** 창에서는 네임스페이스와 필드 레이블 및 유형을 정의합니다(예: `dc:title`.

![screen_shot_2012-04-23at23305pm](assets/screen_shot_2012-04-23at23305pm.png)

다음을 참조하십시오 [에셋 사용자 지정 및 확장](/help/assets/extending-assets.md) 메타데이터 양식에서 사용할 수 있는 네임스페이스를 수정하는 방법에 대해 설명합니다.

1. 다음을 클릭합니다. **제한** 탭. 여기에서 필드가 필요한지 여부를 선택하고 필요한 경우 제한을 추가할 수 있습니다.

![screen_shot_2012-04-23at23435pm](assets/screen_shot_2012-04-23at23435pm.png)

1. 다음을 클릭합니다. **표시** 탭. 여기에서 메타데이터 필드에 새 너비 및 행 수를 입력할 수 있습니다. 다음 항목 선택 **필드가 읽기 전용입니다.** 사용자가 메타데이터를 편집할 수 있도록 허용하는 확인란입니다.

![screen_shot_2012-04-23at23446pm](assets/screen_shot_2012-04-23at23446pm.png)

다음은 다양한 필드가 있는 메타데이터 양식의 예입니다.

![메타데이터](assets/chlimage_1-390.png)

그런 다음 에셋 편집기 페이지에서 메타데이터 필드(편집할 수 있는 경우)에 값을 입력하고 종료 작업(예: 변경 사항 제출)을 수행할 수 있습니다.

#### 하위 자산 {#sub-assets}

하위 에셋 구성 요소를 사용하여 하위 에셋을 보고 선택할 수 있습니다. 아래에 표시되는 이름을 확인할 수 있습니다. [주 자산](/help/assets/assets.md#what-are-digital-assets) 및 하위 에셋입니다.

기본 에셋 및 하위 에셋의 제목을 변경할 수 있는 하위 에셋 대화 상자를 열 수 있도록 하위 에셋 구성 요소를 더블 클릭합니다. 기본값은 해당 필드 아래에 나타납니다.

![screen_shot_2012-04-23at23907pm](assets/screen_shot_2012-04-23at23907pm.png)

다음은 채워진 Sub Assets 구성 요소의 예입니다.

![screen_shot_2012-04-23at24442pm](assets/screen_shot_2012-04-23at24442pm.png)

예를 들어 하위 에셋을 선택하는 경우 구성 요소에 적절한 페이지가 표시되고 상자 제목이 하위 에셋에서 동위 멤버로 변경되는 방법에 주목합니다.

![screen_shot_2012-04-23at24552pm](assets/screen_shot_2012-04-23at24552pm.png)

#### 태그 {#tags}

태그 구성 요소는 사용자가 기존 태그를 에셋에 할당할 수 있는 구성 요소입니다. 이는 나중에 조직과 검색에서 도움이 됩니다. 이 구성 요소를 읽기 전용으로 만들 수 있으므로 사용자는 태그를 추가할 수 없고 보기만 할 수 있습니다.

![screen_shot_2012-04-23at25031pm](assets/screen_shot_2012-04-23at25031pm.png)

원하는 경우 태그에서 제목을 변경하고 할당된 네임스페이스를 선택할 수 있는 태그 대화 상자를 열 수 있도록 태그 구성 요소를 두 번 클릭합니다. 이 필드를 편집할 수 있게 하려면 **[!UICONTROL 편집 숨기기]** 확인란. 기본적으로 태그는 편집할 수 있습니다.

![screen_shot_2012-04-23at24731pm](assets/screen_shot_2012-04-23at24731pm.png)

사용자가 태그를 편집할 수 있는 경우 연필을 클릭하여 태그 드롭다운 메뉴에서 태그를 선택하여 추가할 수 있습니다.

![screen_shot_2012-04-23at25150pm](assets/screen_shot_2012-04-23at25150pm.png)

다음은 채워진 태그 구성 요소입니다.

![screen_shot_2012-04-23at25244pm](assets/screen_shot_2012-04-23at25244pm.png)

#### 썸네일 {#thumbnail}

썸네일 구성 요소는 자산에 선택한 썸네일이 표시되는 위치입니다(대부분의 형식에서 썸네일이 자동으로 추출됨). 또한 구성 요소에 파일 이름이 표시되고, [수정할 수 있는 작업](/help/assets/assets-finder-editor.md#adding-asset-editor-actions).

![screen_shot_2012-04-23at25452pm](assets/screen_shot_2012-04-23at25452pm.png)

대체 텍스트를 변경할 수 있는 썸네일 대화 상자를 열 수 있도록 썸네일 구성 요소를 두 번 클릭합니다. 기본적으로 썸네일 대체 텍스트는 다음과 같습니다. **다운로드하려면 클릭** 에셋.

![screen_shot_2012-04-23at25604pm](assets/screen_shot_2012-04-23at25604pm.png)

다음은 채워진 썸네일 구성 요소의 예입니다.

![screen_shot_2012-04-23at34815pm](assets/screen_shot_2012-04-23at34815pm.png)

#### 제목 {#title}

제목 구성 요소에는 에셋의 제목과 설명이 표시됩니다.

기본적으로 읽기 전용 모드이므로 사용자가 편집할 수 없습니다. 편집할 수 있게 하려면 구성 요소를 두 번 클릭하고 **편집 단추 숨기기** 확인란. 또한 여러 에셋의 제목을 입력합니다.

![screen_shot_2012-04-23at35100pm](assets/screen_shot_2012-04-23at35100pm.png)

제목을 편집할 수 있는 경우 연필을 클릭하여 제목과 설명을 추가할 수 있습니다. **자산 속성** 창. 또한 날짜 및 시간을 선택하여 에셋을 켜거나 끌 수 있습니다.

편집 시 [!UICONTROL 제목], 사용자는 **제목**, **설명**, 및 입력 **날짜** 및 **해제 시간** 에셋을 켜거나 끕니다.

![screen_shot_2012-04-23at35241pm](assets/screen_shot_2012-04-23at35241pm.png)

다음은 채워진 제목 구성 요소의 예입니다.

![chlimage_1-164](assets/chlimage_1-392.png)

#### 자산 편집기 작업 추가 {#adding-asset-editor-actions}

사전 정의된 여러 작업에서 사용자가 선택한 디지털 에셋에 대해 수행할 수 있는 작업을 결정할 수 있습니다.

자산 편집기 페이지에 작업을 추가하려면 다음 작업을 수행하십시오.

1. 사용자 지정할 자산 편집기 페이지에서 **자산 편집기** 사이드 킥에서.

![screen_shot_2012-04-23at35515pm](assets/screen_shot_2012-04-23at35515pm.png)

다음 작업을 사용할 수 있습니다.

| 작업 | 설명 |
|---|---|
| [!UICONTROL 다운로드] | 사용자가 선택한 자산을 컴퓨터에 다운로드할 수 있습니다. |
| [!UICONTROL 편집자] | 사용자가 이미지를 편집할 수 있습니다(대화형 편집). |
| [!UICONTROL Lightbox] | 자산을 다른 작업을 수행할 수 있는 &quot;lightbox&quot;에 저장합니다. 여러 페이지의 에셋으로 작업할 때 유용합니다. |
| [!UICONTROL 잠금] | 사용자가 자산을 잠글 수 있습니다. 이 기능은 기본적으로 활성화되어 있지 않으므로 구성 요소 목록에서 활성화해야 합니다. |
| [!UICONTROL 참조] | 자산을 사용 중인 페이지에 표시하려면 이 아이콘을 클릭합니다. |
| [!UICONTROL 버전 관리] | 에셋의 버전을 만들고 복원할 수 있습니다. |

1. 적절한 작업을 **작업** 페이지의 영역입니다. 페이지에서 드래그한 작업을 실행하는 데 사용되는 옵션을 만듭니다.

![chlimage_1-165](assets/chlimage_1-393.png)

## 자산 편집기 페이지를 사용하여 자산 다중 편집 {#multi-editing-assets-with-the-asset-editor-page}

포함 [!DNL Experience Manager Assets], 여러 에셋을 한 번에 변경할 수 있습니다. 에셋을 선택한 후 태그와 메타데이터를 동시에 변경할 수 있습니다.

에셋 편집기 페이지를 사용하여 에셋을 다중 편집하려면 다음과 같이 하십시오.

1. Geometrixx 열기 **프레스 센터** 페이지:
   `https://localhost:4502/content/geometrixx/en/company/press.html`

1. 에셋 선택:

   * Windows에서: `Ctrl + click` 각 에셋.
   * Mac에서: `Cmd + click` 각 에셋.

   에셋 범위를 선택하려면 첫 번째 에셋을 클릭한 다음 `Shift + click` 마지막 자산입니다.

1. 클릭 **메타데이터 편집** 다음에서 **작업** 필드 (페이지의 왼쪽 부분).
1. Geometrixx **Press Center 자산 편집기** 페이지가 새 탭에서 열립니다. 에셋의 메타데이터는 다음과 같이 표시됩니다.

   * 모든 에셋에는 적용되지 않고 일부 에셋에만 적용되는 태그는 기울임꼴로 표시됩니다.
   * 모든 에셋에 적용되는 태그는 일반 글꼴로 표시됩니다.
   * 태그 이외의 메타데이터: 필드 값은 선택한 모든 에셋에 대해 동일한 경우에만 표시됩니다.

1. 클릭 **다운로드** 원본 렌디션이 포함된 ZIP 파일을 다운로드하려면 다음 작업을 수행하십시오.
1. 다음 옆에 있는 태그 편집 옵션을 클릭합니다. **태그** 필드.

   * 모든 에셋에는 적용되지 않고 일부 에셋에만 적용되는 태그에는 회색 배경이 있습니다.
   * 모든 에셋에 적용되는 태그에는 흰색 배경이 있습니다.

   다음과 같은 작업을 수행할 수 있습니다.

   * 클릭 `x` 를 클릭하여 모든 에셋에 대한 태그를 제거합니다.
   * 클릭 `+` 를 클릭하여 모든 에셋에 태그를 추가합니다.
   * 다음을 클릭합니다. **화살표** 태그를 선택하여 모든 에셋에 새 태그를 추가합니다.

   클릭 **확인** 을 눌러 변경 사항을 양식에 씁니다. 상자 옆에 있는 상자 **태그** 필드는 자동으로 선택됩니다.

1. 설명 필드를 편집합니다. 예를 들어 를 다음과 같이 설정합니다.

   `This is a common description`

   필드를 편집할 때 해당 값은 양식을 제출할 때 선택한 에셋의 기존 값을 덮어씁니다.

   참고: 필드를 편집할 때 필드 옆에 있는 상자가 자동으로 선택됩니다.

1. 클릭 **메타데이터 업데이트** 양식을 제출하고 모든 에셋에 대한 변경 사항을 저장합니다.

   참고: 선택한 메타데이터만 수정됩니다.
