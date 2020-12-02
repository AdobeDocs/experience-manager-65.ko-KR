---
title: 컨텐츠 조각으로 페이지 작성
seo-title: 컨텐츠 조각으로 페이지 작성
description: AEM 컨텐츠 조각을 사용하여 페이지에 구애받지 않고 컨텐츠를 디자인, 작성, 조정 및 사용 가능
seo-description: AEM 컨텐츠 조각을 사용하여 페이지에 구애받지 않고 컨텐츠를 디자인, 작성, 조정 및 사용 가능
uuid: 987de428-8354-4b23-a552-3ea415122184
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 4049a7a5-4b33-4462-a25f-3c0daeb6a8a9
docset: aem65
translation-type: tm+mt
source-git-commit: 74f259d579bcf8d7a9198f93ef667288787a4493
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 100%

---


# 컨텐츠 조각으로 페이지 작성{#page-authoring-with-content-fragments}

AEM(Adobe Experience Manager) 컨텐츠 조각은 [페이지와 독립된 자산으로 작성 및 관리](/help/assets/content-fragments/content-fragments.md)됩니다.

변형(채널별로 가능)과 함께 이 조각을 사용하여 채널 중립적인 컨텐츠를 만들 수 있습니다. 그런 다음 컨텐츠 페이지를 작성할 때 이러한 조각과 해당 변형을 사용할 수 있습니다.

업데이트된 JSON Exporter와 함께 구조화된 컨텐츠 조각을 사용하여 AEM 페이지 이외의 채널에 컨텐츠 서비스를 통해 AEM 컨텐츠를 제공할 수도 있습니다.

>[!NOTE]
>
>**컨텐츠 조각** 및 **[경험 조각](/help/sites-authoring/experience-fragments.md)**&#x200B;은 AEM 내의 다양한 기능입니다.
>
>* **컨텐츠 조각**&#x200B;은 편집 가능한 컨텐츠이며, 주로 텍스트나 관련 이미지입니다. 또한 디자인과 레이아웃이 없는 순수 컨텐츠입니다.
>* **경험 조각**&#x200B;은 전체적으로 배치된 컨텐츠, 즉 웹 페이지 조각입니다.

>
>
경험 조각은 컨텐츠 조각 형태로 컨텐츠를 포함할 수 있지만 반대로는 불가능합니다.

>[!CAUTION]
>
>이 페이지는 [컨텐츠 조각에서 사용](/help/assets/content-fragments/content-fragments.md) 및 관련 페이지와 함께 읽어야 합니다. 기본 용어 및 개념뿐 아니라 조각 생성과 관리를 소개합니다.

컨텐츠 조각을 사용하여 다음을 수행할 수 있습니다.

* **마케팅 및 캠페인 전략**

   * 중앙에서 관리되는 컨텐츠 조각을 통해 컨텐츠를 검토합니다.

* **Creative 프로그램**

   * 컨텐츠 조각과 관련된 컬렉션을 통해 Creative 자산을 추적합니다.

* **사본 작성자**

   * AEM 컨텐츠 조각 편집기에서 작성합니다.
   * 컨텐츠 변형을 만들 수 있습니다.
   * 관련 컨텐츠를 컨텐츠 조각과 연결할 수 있습니다.
   * 버전 관리/워크플로우를 사용할 수 있습니다.
   * 컨텐츠 조각을 공유할 수 있습니다.
   * 번역을 중앙에서 관리할 수 있습니다.

* **제작자 및 과정 관리자**

   * AEM에서 작성하여 사전 정의된 조각 및 변형에서 선택합니다.
   * 사본 작성자와 크리에이티브가 중앙에서 관리되는 조각 및 자산을 업데이트할 때 항상 최신으로 유지되는 조각 및 관련 컨텐츠를 사용할 수 있습니다.
   * 관련성에 대해 조정되는 관련 미디어 컨텐츠를 사용할 수 있습니다.
   * 임시 컨텐츠 변형이 조각에서 중앙 관리되는 상태로 유지되도록 하면서 그러한 변형을 즉석으로 만들 수 있습니다.

## 페이지에 컨텐츠 조각 추가 {#adding-a-content-fragment-to-your-page}

1. 편집할 페이지를 엽니다.

1. **구성 요소** 브라우저 또는 **새 구성 요소 삽입**&#x200B;에서 **컨텐츠 조각** 구성 요소를 추가합니다.

1. 다음을 수행할 수 있습니다.

   * **자산** 브라우저를 열고 **컨텐츠 조각**&#x200B;을 필터링합니다(기본값은 이미지). 그런 다음 필수 조각을 구성 요소 인스턴스에 드래그합니다.

   * 컨텐츠 조각 구성 요소를 선택한 다음, 도구 모음에서 **구성**&#x200B;을 선택하십시오. 대화 상자에서 선택 대화 상자를 열어 필요한 **컨텐츠 조각**&#x200B;을 찾아 선택할 수 있습니다.
   >[!NOTE]
   >
   >다른 방법은 특정 컨텐츠 조각을 페이지로 직접 드래그하는 것입니다. 이 경우 관련 구성 요소(컨텐츠 조각)가 자동으로 만들어집니다.

1. 처음에는 **주** 요소 및 **마스터**(변형)의 컨텐츠가 표시됩니다. 필요에 따라 [다른 요소 및/또는 변형을 선택](#selecting-the-element-or-variation)할 수 있습니다.

   ![cfm-6420-01](assets/cfm-6420-01.png)

   >[!NOTE]
   >
   >추가 편집 기능에 대한 자세한 정보는 다음을 참조하십시오.
   >
   >
   >
   >    * [응답형 레이아웃](/help/sites-authoring/responsive-layout.md)
   >    * [페이지 컨텐츠 편집](/help/sites-authoring/editing-content.md)


### 요소 또는 변형 선택 {#selecting-the-element-or-variation}

조각의 **구성** 대화 상자를 열어 현재 페이지에서 사용할 조각을 구성합니다. 이 대화 상자는 사용된 구성 요소에 따라 달라질 수 있습니다.

적절한 구성 대화 상자에서 다음을 포함하여 사용 가능한 매개 변수를 선택할 수 있습니다.

* **콘텐츠 조각**

   사용할 조각을 지정합니다.

* **표시 모드**:

   * **단일 텍스트 요소**

   * **여러 요소**

* **요소**

   * 기본 **기본**&#x200B;은 항상 사용할 수 있습니다.
   * 해당 템플릿을 사용하여 조각을 생성한 경우 선택이 가능합니다.

   >[!NOTE]
   >
   >사용할 수 있는 요소는 사용된 템플릿에 따라 다릅니다.

* **변형**

   * 기본 **마스터**&#x200B;는 항상 사용할 수 있습니다.
   * 조각에 대해 변형을 만든 경우 선택이 가능합니다.

* **단락**: 포함할 단락 범위를 지정합니다.

   * **모두**
   * **범위**: 예를 들어, `1`, `3-5`, `9-*`

      * **제목을 소유자의 단락으로 처리**

* **제목을 소유자의 단락으로 처리**

### 조각 편집기에 대한 빠른 연결 {#quick-connection-to-fragment-editor}

구성 요소 도구 모음에서 **편집** 아이콘을 사용하여 자산을 편집할 조각 소스를 열 수 있습니다. 이 경우 [컨텐츠 조각을 편집하고 관리](/help/assets/content-fragments/content-fragments.md)할 수 있습니다.

>[!CAUTION]
>
>조각 소스를 편집하면 해당 컨텐츠 조각을 참조하는 모든 페이지에 영향을 줍니다.

### 중간 컨텐츠 추가  {#adding-in-between-content}

특정 컨텐츠 조각이 페이지에 추가되면 조각의 각 HTML 단락 사이(및 상단/하단)에 **구성 요소를 여기로 드래그하십시오.** 자리 표시자가 있습니다.

이렇게 하면 루트 조각을 변경하지 않고도 조각 컨텐츠 [사이(즉, 중간 컨텐츠)](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments)(사용 가능한 모든 지점)에 컨텐츠를 더 추가할 수 있습니다.

중간 컨텐츠에서 다음 작업을 수행할 수 있습니다.

* [구성 요소 브라우저](/help/sites-authoring/author-environment-tools.md#components-browser)에서 구성 요소를 추가합니다.
* [자산 브라우저](/help/sites-authoring/author-environment-tools.md#assets-browser)에서 자산을 추가합니다.
* 중간 컨텐츠 소스로 [연관된 컨텐츠](#using-associated-content)를 사용합니다.

>[!CAUTION]
>
>중간 컨텐츠는 페이지 컨텐츠이며, 컨텐츠 조각에 저장되지 않습니다.

![cfm-6420-02](assets/cfm-6420-02.png)

>[!NOTE]
>
>또한 조각 자체에 [시각적 자산(이미지)을 삽입](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)할 수도 있습니다.
>
>조각 자체에 삽입된 시각적 자산은 조각의 이전 단락에 첨부됩니다. 즉, 시각적 자산과 이전 단락 간에 중간 컨텐츠를 배치할 수 없음을 의미합니다.

>[!CAUTION]
>
>중간 컨텐츠를 페이지의 컨텐츠 조각에 추가한 후에 기존 컨텐츠 조각(즉, 컨텐츠 조각 편집기에서)의 구조를 변경하면 잘못된/예기치 않은 결과가 나타날 수 있습니다.
>
>이 경우 중간 컨텐츠가 그대로 유지됩니다. 
>
>* 중간 구성 요소는 조각 플로우의 구성 요소 순서 내에서 절대 위치에 있습니다. 조각 내의 단락 컨텐츠가 변경되더라도 이 위치는 변경되지 않습니다.
>
>  
중간 단락은 옆에 배치된(조각) 단락과 문맥적 관계가 없으므로 상대적 위치가 변경된 것처럼 보일 수 있습니다.
>* 두 단락 구조가 충돌하지 않는 경우에는 중간 컨텐츠가 내부에 여전히 있어도 표시되지 않습니다.

>



### 관련 컨텐츠 사용  {#using-associated-content}

[관련 컨텐츠](/help/assets/content-fragments/content-fragments-assoc-content.md)를 [컨텐츠 조각](/help/assets/content-fragments/content-fragments.md)과 연결한 경우 이러한 자산은 사이드 패널에서 사용할 수 있습니다(조각을 컨텐츠 페이지에 배치한 후에). 연관된 컨텐츠는 [중간 컨텐츠](#adding-in-between-content)의 특별한 컨텐츠 소스입니다.

>[!NOTE]
>
>[시각적 자산(예: 이미지)](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)을 조각 및/또는 페이지에 추가하는 다양한 방법이 있습니다.

>[!NOTE]
>
>한 페이지에 여러 개의 컨텐츠 조각이 있는 경우 **관련 컨텐츠** 탭에 모든 조각에 적합한 자산이 표시됩니다.

관련 컨텐츠가 있는 조각을 페이지에 추가하면 새 탭(**관련 컨텐츠**)이 사이드 패널에서 열립니다.

여기서 자산을 필요한 위치(기존 구성 요소 또는 해당 구성 요소를 만들 필수 위치)로 드래그할 수 있습니다.

![cfm-6420-03](assets/cfm-6420-03.png)

### 조각에 삽입된 자산 {#assets-inserted-into-the-fragment}

자산(예: 이미지)이 조각 자체에 삽입된 경우, 페이지 편집기에서 이러한 자산을 편집하는 옵션은 제한됩니다.  <!-- Removed link as it was a 404 on helpx -->

예를 들어, 이미지의 경우 다음 작업을 수행할 수 있습니다.

* 이미지를 자르고 회전하거나 뒤집습니다.
* 제목 또는 대체 텍스트를 추가합니다.
* 크기를 지정합니다.
* 레이아웃을 구성할 수도 있습니다.

이동, 복사, 삭제와 같은 기타 변경 사항은 조각 편집기에서 작성해야 합니다.

### 게시 {#publishing}

게시된 웹 페이지에서 조각을 사용할 수 있도록 조각을 게시해야 합니다.

* [자산 콘솔에서 조각을 만든](/help/assets/content-fragments/content-fragments.md#publishingandreferencingafragment) 후에 조각을 게시할 수 있습니다.
* *게시 취소된 조각*&#x200B;을 게시 중인 페이지에서 사용하는 경우 그때 조각이 게시될 수도 있습니다.

