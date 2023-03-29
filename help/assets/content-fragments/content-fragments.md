---
title: 콘텐츠 조각을 사용하여 작업
description: AEM(Adobe Experience Manager)의 컨텐츠 조각을 사용하여 헤드리스 게재에 적합한 페이지에 구애받지 않고 컨텐츠를 디자인, 작성, 조정 및 사용할 수 있는 방법을 알아봅니다.
feature: Content Fragments
role: User
exl-id: 0ee883c5-0cea-46b7-a759-600b8ea3bc3e
source-git-commit: ad0f0bd8b0c230e002c734adca87da22bfa3a7cd
workflow-type: tm+mt
source-wordcount: '1989'
ht-degree: 94%

---

# 콘텐츠 조각을 사용하여 작업 {#working-with-content-fragments}

Adobe Experience Manager(AEM)을 사용하면 컨텐츠 조각을 사용하여 디자인, 만들기, 조정 및 조정할 수 있습니다 [페이지에 영향을 받지 않는 컨텐츠 게시](/help/sites-authoring/content-fragments.md) 이를 통해 헤드리스 게재에 이상적인 여러 위치/여러 채널에서 사용할 수 있는 컨텐츠를 준비할 수 있습니다.

콘텐츠 조각에는 구조화된 콘텐츠가 포함되어 있습니다.

* 이는 최종 조각의 구조를 사전 정의하는 [콘텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md)을 기반으로 합니다.
* 구조의 범위는 다음과 같습니다.
   * 기본
      * 여러 줄이 있는 단일 텍스트 필드를 예로 들 수 있습니다.
      * 페이지 작성 시 사용할 간단한 콘텐츠를 준비하는 데 사용할 수 있습니다.
   * 복합
      * 텍스트, 숫자, 부울, 데이터 및 시간 등 다양한 데이터 유형의 여러 필드 조합입니다.
      * 페이지 작성을 위해 보다 구조화된 콘텐츠를 준비하거나 애플리케이션에 게재하는 데 사용할 수 있습니다.
   * 중첩
      * 사용 가능한 참조 데이터 유형을 사용하면 콘텐츠를 중첩할 수 있습니다.
      * 주로 애플리케이션에 게재하는 데 사용됩니다.

AEM 핵심 구성 요소의 Sling Model(JSON) 내보내기 기능을 사용하여 콘텐츠 조각을 JSON 형식으로 게재할 수도 있습니다. 이 게재 형식을 사용하면

* 구성 요소를 사용하여 게재할 조각의 요소를 관리할 수 있습니다.
* API 게재에 사용되는 페이지에서 여러 콘텐츠 조각 핵심 구성 요소를 추가하여 벌크 게재를 수행할 수 있습니다.

이 페이지 및 다음 페이지에서는 콘텐츠 조각 생성, 구성, 관리 및 사용을 위한 작업을 다룹니다.

* [인스턴스에 대해 콘텐츠 조각 기능 활성화](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [콘텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md) - 모델 활성화, 생성 및 정의
* [콘텐츠 조각 관리](/help/assets/content-fragments/content-fragments-managing.md) - 콘텐츠 조각 생성 후 편집, 게시 및 참조
* [변형 - 조각 콘텐츠 작성](/help/assets/content-fragments/content-fragments-variations.md) - 조각 콘텐츠를 작성 및 마스터의 변형 만들기
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md) - 조각에 Markdown 구문 사용
* [관련 콘텐츠 사용](/help/assets/content-fragments/content-fragments-assoc-content.md) - 관련 콘텐츠 추가
* [메타데이터 - 조각 속성](/help/assets/content-fragments/content-fragments-metadata.md) - 조각 속성 보기 및 편집
* 사용 [컨텐츠 조각을 GraphQL과 함께 사용하여 컨텐츠를 전달합니다](/help/assets/content-fragments/content-fragments-graphql.md) 을 사용하도록 선택할 수 있습니다. 이 작업에 도움이 되도록 미리 볼 수 있습니다 [JSON 출력](/help/assets/content-fragments/content-fragments-json-preview.md).

>[!NOTE]
>
>이들 페이지는 다음과 함께 읽을 수 있습니다.
>
>* [콘텐츠 조각을 사용하여 페이지 작성](/help/sites-authoring/content-fragments.md)
>* [콘텐츠 조각 사용자 정의 및 확장](/help/sites-developing/customizing-content-fragments.md)
>* [콘텐츠 조각 렌더링용 구성 요소 구성](/help/sites-developing/content-fragments-config-components-rendering.md)
>* [AEM Assets HTTP API의 콘텐츠 조각 지원](/help/assets/assets-api-content-fragments.md)
>* [콘텐츠 조각과 함께 사용하기 위한 AEM GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)


커뮤니케이션 채널의 수는 매년 증가하고 있습니다. 일반적으로 채널은 다음 중 하나로서 게재 메커니즘을 나타냅니다.

* 물리적 채널 - 예: 데스크탑, 모바일
* 실제 채널에서의 게재 형태 - 예: 데스크탑의 &quot;제품 세부 정보 페이지&quot;, &quot;제품 범주 페이지&quot; 또는 모바일의 &quot;모바일 웹&quot;, &quot;모바일 앱&quot;

그러나 대개 모든 채널에 대해 동일한 콘텐츠를 사용하고 싶지 않을 것이므로 특정 채널에 따라 콘텐츠를 최적화해야 합니다.

콘텐츠 조각을 사용하면

* 다양한 채널에서 효율적으로 타겟 대상자에게 도달하는 방법을 고려할 수 있습니다.
* 채널 중립적인 에디토리얼 콘텐츠를 만들고 관리할 수 있습니다.
* 다양한 채널을 위한 콘텐츠 풀을 빌드할 수 있습니다.
* 특정 채널에 맞는 콘텐츠 변형을 디자인할 수 있습니다.
* 에셋(혼합 미디어 조각)을 삽입하여 텍스트에 이미지를 추가합니다.
* 데이터의 복잡성을 반영하도록 중첩된 콘텐츠를 만듭니다.

그런 다음 이러한 콘텐츠 조각을 취합하여 다양한 채널에서 경험을 제공할 수 있습니다.

>[!NOTE]
>
>**콘텐츠 조각** 및 **[경험 조각](/help/sites-authoring/experience-fragments.md)**&#x200B;은 AEM 내의 다양한 기능입니다.
>* **콘텐츠 조각**&#x200B;은 텍스트, 숫자 및 날짜 등 구조화된 데이터에 액세스하는 데 사용할 수 있는 에디토리얼 콘텐츠입니다. 정의 및 구조를 갖지만 추가적인 시각적 디자인 및/또는 레이아웃을 포함하지 않는 순수 콘텐츠입니다.
>* **경험 조각**&#x200B;은 전체적으로 배치된 콘텐츠, 즉 웹 페이지 조각입니다.
>
>경험 조각은 콘텐츠 조각 형태로 콘텐츠를 포함할 수 있지만 반대로는 불가능합니다.
>
>자세한 내용은 [AEM의 콘텐츠 조각 및 경험 조각 이해](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments)를 참조하십시오.

>[!NOTE]
>
>AEM 6.3 이전에는 모델 대신 템플릿을 사용하여 컨텐츠 조각을 만들었습니다. 템플릿은 더 이상 새 조각을 만드는 데 사용할 수 없지만 그러한 템플릿으로 만든 조각은 계속 지원됩니다.

## 콘텐츠 조각 및 콘텐츠 서비스 {#content-fragments-and-content-services}

AEM Content Services는 웹 페이지에 초점을 두지 않고 AEM에서 콘텐츠 설명 및 게재를 일반화하기 위해 디자인되었습니다.

모든 클라이언트가 사용할 수 있는 표준화된 방법을 사용하여 기존 AEM 웹 페이지가 아닌 채널에 콘텐츠를 게재할 수 있습니다. 이러한 채널에는 다음과 같은 것들이 포함될 수 있습니다.

* SPA (Single Page Applications)
* 기본 모바일 애플리케이션
* AEM 외부에 있는 기타 채널 및 터치포인트

게재는 JSON 내보내기를 사용하여 JSON 형식으로 이루어집니다.

AEM 콘텐츠 조각을 사용하여 구조화된 콘텐츠를 설명하고 관리할 수 있습니다. 구조화된 콘텐츠는 텍스트, 숫자 데이터, 부울, 날짜 및 시간 등을 포함하여 다양한 콘텐츠 유형을 포함할 수 있는 모델에서 정의됩니다.

그런 다음 AEM 핵심 구성 요소의 JSON 내보내기 기능과 함께 이 구조화된 콘텐츠를 사용하여 AEM 페이지 이외의 채널에 AEM 콘텐츠를 게재할 수 있습니다.

<!--
>[!NOTE]
>
>See [Headless and AEM](/help/implementing/developing/headless/introduction.md) for an introduction to Headless Development for AEM Sites.
-->

>[!NOTE]
>
>AEM은 조각 콘텐츠 번역도 지원합니다.

<!--
>[!NOTE]
>
>AEM also supports the translation of fragment content. See [Translating Assets](/help/assets/translate-assets.md) for further information.
-->

## 콘텐츠 유형 {#content-type}

콘텐츠 조각은

* **자산**&#x200B;으로 저장됩니다.

   * 컨텐츠 조각(및 그 변형)은 **자산** 콘솔에서 만들고 유지 관리할 수 있습니다.
   * 컨텐츠 조각 편집기에서 작성 및 편집됩니다.

* [콘텐츠 조각 구성 요소(참조 구성 요소)를 통해 페이지 편집기](/help/sites-authoring/content-fragments.md)에서 사용됩니다.

   * **콘텐츠 조각** 구성 요소는 페이지 작성자가 사용할 수 있습니다. 따라서 페이지 작성자가 HTML 또는 JSON 형식으로 필요한 콘텐츠 조각을 참조하고 게재할 수 있습니다.

* [AEM GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)를 사용하여 액세스할 수 있습니다.

콘텐츠 조각은 다음과 같은 콘텐츠 구조입니다.

* 레이아웃이나 디자인이 없습니다(일부 텍스트 형식 지정은 리치 텍스트 모드에서 가능).
* 하나 이상의 [구성 부분](#constituent-parts-of-a-content-fragment)을 포함합니다.
* [이미지를 포함하거나 이미지에 연결](#fragments-with-visual-assets)할 수 있습니다.
* 페이지에서 참조할 때 [중간적인 콘텐츠](#in-between-content-when-page-authoring-with-content-fragments)를 사용할 수 있습니다.

* 게재 메커니즘(즉, 페이지, 채널)에 독립적입니다.

### 시각적 에셋이 있는 조각 {#fragments-with-visual-assets}

작성자가 콘텐츠를 더 잘 제어할 수 있도록 이미지를 콘텐츠 조각에 추가하거나 콘텐츠 조각과 통합할 수 있습니다.

에셋은 각각 고유한 장점이 있는 여러 가지 방법으로 콘텐츠 조각에 사용할 수 있습니다.

* 조각에 **에셋 삽입**(혼합 미디어 조각)

   * 조각의 필수 부분입니다([콘텐츠 조각의 구성 성분 부분](#constituent-parts-of-a-content-fragment) 참조).
   * 에셋의 위치를 정의합니다.
   * 자세한 내용은 조각 편집기에서 [조각에 에셋 삽입](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)을 참조하십시오.

   >[!NOTE]
   >
   >콘텐츠 조각 자체에 삽입된 시각적 에셋은 선행하는 단락에 첨부됩니다. 조각을 페이지에 추가하면 이러한 에셋이 중간적 콘텐츠가 추가될 때 해당 단락과 관련하여 이동됩니다.

* **관련 콘텐츠**

   * 조각에 연결되어 있지만 조각의 고정 부분이 아닙니다([콘텐츠 조각의 구성 성분 부분](#constituent-parts-of-a-content-fragment) 참조).
   * 위치에 대해 어느 정도 유연합니다.
   * 페이지에서 조각을 사용할 때(중간적 콘텐츠로서) 쉽게 사용할 수 있습니다.
   * 자세한 내용은 [관련 콘텐츠](/help/assets/content-fragments/content-fragments-assoc-content.md)를 참조하십시오.

* 페이지 편집기의 **에셋 브라우저**&#x200B;에서 사용할 수 있는 에셋

   * 에셋을 유연하게 선택할 수 있습니다.
   * 위치에 대해 어느 정도 유연합니다.
   * 특정 조각에 대해 동의되는 개념을 제공하지 않습니다.

<!--
  * See [Assets Browser](/help/sites-authoring/environment-tools.md#assets-browser) for more information.
-->

### 콘텐츠 조각을 구성하는 부분 {#constituent-parts-of-a-content-fragment}

콘텐츠 조각 에셋은 다음 부분으로 구성됩니다(직접 또는 간접적으로).

* **조각 요소**

   * 요소는 콘텐츠를 포함하는 데이터 필드와 관련이 있습니다.
   * 콘텐츠 모델을 사용하여 콘텐츠 조각을 생성합니다. 모델에 지정된 요소(필드)는 조각의 구조를 정의합니다. 이러한 요소(필드)는 다양한 데이터 유형일 수 있습니다.

* **조각 단락**

   * 개별 엔티티로 구분된 텍스트 블록(종종 여러 줄)입니다.

   * [리치 텍스트](/help/assets/content-fragments/content-fragments-variations.md#rich-text) 및 [Markdown](/help/assets/content-fragments/content-fragments-variations.md#markdown) 모드에서 단락 서식을 헤더로 지정할 수 있습니다. 이렇게 하면 해당 단락과 그다음 단락이 한 단위로 묶입니다.

   * 페이지 작성 중 콘텐츠를 제어할 수 있도록 해 줍니다.

* **조각에 삽입된 에셋(혼합 미디어 조각)**

   * 실제 조각에 삽입되고 조각의 내부 콘텐츠로 사용된 에셋 (이미지)
   * 조각의 단락 시스템에 임베드됩니다.
   * [페이지에서 조각을 사용/참조](/help/sites-authoring/content-fragments.md)할 때 형식을 지정할 수 있습니다.
   * 조각 편집기를 사용해야 조각에 추가, 조각에서 삭제 또는 조각 내에서 이동할 수 있습니다. 페이지 편집기에서는 이러한 작업을 수행할 수 없습니다.
   * [조각 편집기에서 리치 텍스트 형식](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)을 사용해야 조각에 추가, 조각에서 삭제 또는 조각 내에서 이동할 수 있습니다.
   * 여러 줄 텍스트 요소(임의의 조각 유형)에만 추가할 수 있습니다.
   * 선행하는 텍스트(단락)에 첨부됩니다.

      >[!CAUTION]
      >
      >에셋을 일반 텍스트 형식으로 전환하여 (실수로) 조각에서 제거할 수 있습니다.

      >[!NOTE]
      >
      >에셋은 페이지에서 조각을 사용할 때 [추가적인(중간적) 콘텐츠](/help/sites-authoring/content-fragments.md#using-associated-content)로도 추가할 수 있습니다. 이때 에셋은 관련 콘텐츠를 사용하거나 에셋 브라우저의 에셋을 사용합니다.

* **관련 콘텐츠**

   * 조각의 외부 콘텐츠지만 조각에 대한 에디토리얼 관련 연관성이 있는 콘텐츠입니다. 일반적으로 이미지, 비디오 또는 기타 조각입니다.
   * 컬렉션 내의 개별 에셋은 페이지에 추가될 때 페이지 편집기에서 조각에 사용할 수 있습니다. 이는 특정 채널의 요구 사항에 따라 이러한 에셋을 선택할 수 있음을 의미합니다.
   * 에셋은 [컬렉션을 통해 조각에 연결](/help/assets/content-fragments/content-fragments-assoc-content.md)됩니다. 연결된 컬렉션은 작성자가 페이지를 작성할 때 사용할 에셋을 결정할 수 있도록 해 줍니다.

      * 컬렉션은 기본 콘텐츠로 조각과 연결되거나 작성자에 의해 조각 작성 도중 조각과 연결될 수 있습니다.
      * [에셋(DAM) 컬렉션](/help/assets/manage-collections.md)은 조각과 관련된 콘텐츠의 기초입니다.
   * 원할 경우 조각 자체를 컬렉션에 추가하여 추적을 지원할 수도 있습니다.

* **조각 메타데이터**

   * [에셋 메타데이터 스키마](/help/assets/metadata-schemas.md)를 사용합니다.
   * 다음 경우에 태그를 만들 수 있습니다.

      * 조각을 만들고 작성할 때
      * 또는 나중에:

         * 콘솔에서 조각 **속성**&#x200B;을 보거나/편집하여
         * 조각 편집기에 있을 때 **메타데이터**&#x200B;를 편집하여

   >[!CAUTION]
   >
   >메타데이터 처리 프로필은 콘텐츠 조각에 적용되지 않습니다.

* **마스터**

   * 조각의 필수 부분

      * 모든 콘텐츠 조각에는 하나의 마스터 인스턴스가 있습니다.
      * 마스터는 삭제할 수 없습니다.
   * 마스터는 **[변형](/help/assets/content-fragments/content-fragments-variations.md)** 아래의 조각 편집기에서 액세스할 수 있습니다.
   * 마스터는 그러한 변형이 아니라 모든 변형의 기초입니다.


* **변형**

   * 에디토리얼 목적에 맞는 조각 텍스트의 표현물은 채널과 관련을 지을 수 있지만, 의무적이지는 않으며, 임시적 로컬 수정용일 수도 있습니다.
   * **마스터**&#x200B;의 사본으로 만들어지지만 필요에 따라 편집할 수 있습니다. 일반적으로 변형 간에 콘텐츠가 겹치게 됩니다.
   * 조각 작성 중에 정의할 수 있습니다.
   * 조각 내에 저장되므로 콘텐츠 사본 살포를 방지할 수 있습니다.
   * 마스터 콘텐츠가 업데이트된 경우 변형을 마스터와 [동기화](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master)할 수 있습니다.
   * [요약](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text)하여 텍스트를 사전 정의된 길이로 신속히 자를 수 있습니다.
   * 조각 편집기의 [변형](/help/assets/content-fragments/content-fragments-variations.md) 탭에서 사용할 수 있습니다.

### 콘텐츠 조각을 사용하여 페이지 작성 시 중간 콘텐츠 {#in-between-content-when-page-authoring-with-content-fragments}

중간 콘텐츠는

* 콘텐츠 조각을 사용하여 작업할 때 페이지 편집기에서 사용할 수 있습니다.
* 페이지에서 조각을 사용/참조한 후 [조각의 플로우 내에 추가된 추가적인 콘텐츠](/help/sites-authoring/content-fragments.md#adding-in-between-content)입니다.
* [콘텐츠 조각을 사용하여 작업할 때 페이지 편집기](/help/sites-authoring/content-fragments.md)에서 사용할 수 있습니다.
* 중간적 콘텐츠는 어떤 조각에든 추가할 수 있으며, 이 경우 요소는 하나만 표시됩니다.
* 연결된 콘텐츠는 적절한 브라우저에서 에셋 및/또는 구성 요소처럼 사용할 수 있습니다.

>[!CAUTION]
>
>중간 콘텐츠는 페이지 콘텐츠이며, 콘텐츠 조각에 저장되지 않습니다.

### 조각에 필요한 사항 {#required-by-fragments}

콘텐츠 조각을 만드는 데 필요한 사항은 다음과 같습니다.

* **콘텐츠 모델**

   * [구성 브라우저를 사용하여 활성화](/help/assets/content-fragments/content-fragments-configuration-browser.md)됩니다.
   * [도구를 사용하여 생성](/help/assets/content-fragments/content-fragments-models.md)됩니다.
   * [조각 생성](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments)에 필요합니다.
   * 조각의 구조(제목, 콘텐츠 요소, 태그 정의)를 정의합니다.
   * 콘텐츠 모델 정의에는 제목과 하나의 데이터 요소가 필요하며, 기타 모든 항목은 선택 사항입니다.
   * 기본 콘텐츠(해당되는 경우)를 정의할 수 있습니다.
   * 작성자는 조각 콘텐츠를 작성할 때 정의된 구조를 변경할 수 없습니다.
   * 종속 콘텐츠 조각을 만든 후 모델을 변경하면 해당 콘텐츠 조각에 영향을 줄 수 있습니다.

페이지 작성에 콘텐츠 조각을 사용하려면 다음 사항이 필요합니다.

* **콘텐츠 조각 구성 요소**

   * 조각을 HTML 및/또는 JSON 형식으로 게재하는 데 중요합니다.
   * [페이지에서 조각을 참조](/help/sites-authoring/content-fragments.md)하는 데 필요합니다.
   * 채널처럼 조각의 레이아웃 및 게재를 담당합니다.
   * 조각은 레이아웃을 정의하고 일부 또는 모든 요소/변형 및 관련 콘텐츠를 게재하기 위해 하나 이상의 전용 구성 요소를 필요로 합니다.
   * 작성 중인 페이지에 조각을 드래그하면 필요한 구성 요소가 자동으로 연결됩니다.

## 사용 예 {#example-usage}

요소 및 변형을 포함한 조각을 사용하여 여러 채널용의 일관된 콘텐츠를 만들 수 있습니다. 조각을 디자인할 때에는 어디에 사용될 것인지 고려해야 합니다.
