---
title: 콘텐츠 조각 맞춤화 및 확장
description: 컨텐츠 조각은 표준 자산을 확장합니다. 이를 맞춤화하는 방법에 대해 알아봅니다.
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 08c88e70-4df9-4627-8a66-1fabe3aee50b
solution: Experience Manager, Experience Manager Sites
feature: Content Fragments
role: Developer
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '2728'
ht-degree: 1%

---


# 콘텐츠 조각 맞춤화 및 확장{#customizing-and-extending-content-fragments}

컨텐츠 조각은 표준 자산을 확장합니다. 다음을 참조하십시오.

* [컨텐츠 조각 생성 및 관리](/help/assets/content-fragments/content-fragments.md) 및 [컨텐츠 조각으로 페이지 작성](/help/sites-authoring/content-fragments.md) 콘텐츠 조각에 대한 자세한 내용은 을 참조하십시오.

* [자산 관리](/help/assets/manage-assets.md) 및 [에셋 사용자 지정 및 확장](/help/assets/extending-assets.md) 표준 에셋에 대한 자세한 내용을 보려면 .

## 아키텍처 {#architecture}

기본 [구성 부분](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 콘텐츠 조각의 은 다음과 같습니다.

* A *컨텐츠 조각,*
* 1개 또는 그 이상의 *컨텐츠 요소* s,
* 하나 이상을 포함할 수 있습니다. *컨텐츠 변형* s.

조각 유형에 따라 모델 또는 템플릿 이 사용됩니다.

>[!CAUTION]
>
>[컨텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md) 는 모든 새 조각을 만드는 데 권장됩니다.
>
>컨텐츠 조각 모델은 WKND의 모든 예제에 사용됩니다.

>[!NOTE]
>
>AEM 6.3 이전에는 콘텐츠 조각이 모델이 아닌 템플릿을 기반으로 생성되었습니다.
>
>콘텐츠 조각 템플릿은 이제 더 이상 사용되지 않습니다. 조각을 만드는 데 계속 사용할 수 있지만 대신 콘텐츠 조각 모델 을 사용하는 것이 좋습니다. 조각 템플릿에 새로운 기능이 추가되지 않으며 이후 버전에서 제거됩니다.

* 컨텐츠 조각 모델:

   * 구조화된 컨텐츠를 포함하는 컨텐츠 조각을 정의하는 데 사용됩니다.
   * 콘텐츠 조각 모델은 콘텐츠 조각을 만들 때 콘텐츠 조각의 구조를 정의합니다.
   * 조각이 모델을 참조하므로 모델 변경 사항은 모든 종속 조각에 영향을 줄 수 있습니다.
   * 모델은 데이터 유형을 기반으로 합니다.
   * 새 변형을 추가하는 기능 등은 조각을 적절하게 업데이트해야 합니다.

  >[!CAUTION]
  >
  >기존 콘텐츠 조각 모델을 변경하면 종속된 조각이 영향을 받을 수 있습니다. 이로 인해 해당 조각에서 고립 속성이 발생할 수 있습니다.

* 콘텐츠 조각 템플릿:

   * 간단한 콘텐츠 조각을 정의하는 데 사용됩니다.
   * 템플릿은 콘텐츠 조각을 만들 때 콘텐츠 조각의 (기본, 텍스트 전용) 구조를 정의합니다.
   * 템플릿이 작성되면 조각에 복사됩니다. 따라서 템플릿에 대한 추가 변경 사항은 기존 조각에 반영되지 않습니다.
   * 새 변형을 추가하는 기능 등은 조각을 적절하게 업데이트해야 합니다.
   * [콘텐츠 조각 템플릿](/help/sites-developing/content-fragment-templates.md) AEM 에코시스템 내의 다른 템플릿 메커니즘(예: 페이지 템플릿 등)과 다른 방식으로 작동합니다. 따라서 이러한 요소는 별도로 고려되어야 합니다.
   * 템플릿을 기반으로 하는 경우 콘텐츠의 MIME 유형이 실제 콘텐츠에서 관리됩니다. 즉, 각 요소 및 변형은 서로 다른 MIME 유형을 가질 수 있습니다.

### 자산과 통합 {#integration-with-assets}

CFM(Content Fragment Management)은 다음과 같이 AEM Assets에 포함되어 있습니다.

* 컨텐츠 조각은 에셋입니다.
* 기존 에셋 기능을 사용합니다.
* Assets는 Assets(관리 콘솔 등)와 완전히 통합됩니다.

#### 자산에 구조화된 컨텐츠 조각 매핑 {#mapping-structured-content-fragments-to-assets}

![구조화된 자산 조각](assets/fragment-to-assets-structured.png)

구조화된 컨텐츠가 있는 컨텐츠 조각(즉, 컨텐츠 조각 모델을 기반으로 함)은 단일 자산에 매핑됩니다.

* 모든 콘텐츠는 아래에 저장됩니다. `jcr:content/data` 에셋의 노드:

   * 요소 데이터는 마스터 하위 노드 아래에 저장됩니다.
     `jcr:content/data/master`

   * 변형은 변형의 이름을 전달하는 하위 노드 아래에 저장됩니다. 예: `jcr:content/data/myvariation`

   * 각 요소의 데이터는 각 하위 노드에 요소 이름(예: 요소의 콘텐츠)을 갖는 속성으로 저장됩니다 `text` 속성으로 저장됩니다. `text` 날짜 `jcr:content/data/master`

* 메타데이터 및 관련 콘텐츠는 아래에 저장됩니다. `jcr:content/metadata`
기존 메타데이터로 간주되지 않고 에 저장되는 제목과 설명을 제외하고 `jcr:content`

#### 에셋에 단순 콘텐츠 조각 매핑 {#mapping-simple-content-fragments-to-assets}

![chlimage_1-90](assets/chlimage_1-90.png)

템플릿을 기반으로 하는 간단한 콘텐츠 조각은 기본 에셋과 (선택 사항) 하위 에셋으로 구성된 조합에 매핑됩니다.

* 조각의 모든 비콘텐츠 정보(예: 제목, 설명, 메타데이터, 구조)는 기본 자산에서만 관리됩니다.
* 조각의 첫 번째 요소 콘텐츠는 기본 에셋의 원래 렌디션에 매핑됩니다.

   * 첫 번째 요소의 변형(있는 경우)은 기본 에셋의 다른 렌디션에 매핑됩니다.

* 추가 요소(있는 경우)는 주 자산의 하위 자산에 매핑됩니다.

   * 이러한 추가 요소의 주요 내용은 각 하위 에셋의 원본 렌디션에 매핑됩니다.
   * 추가 요소의 다른 변형(해당되는 경우)은 해당 하위 에셋의 다른 표현물에 매핑됩니다.

#### 자산 위치 {#asset-location}

표준 에셋과 마찬가지로 콘텐츠 조각은 아래에 보관됩니다.

`/content/dam`

#### 자산 권한 {#asset-permissions}

자세한 내용은 을 참조하십시오. [컨텐츠 조각 - 삭제 고려 사항](/help/assets/content-fragments/content-fragments-delete.md).

#### 기능 통합 {#feature-integration}

* CFM(콘텐츠 조각 관리) 기능은 에셋 코어를 기반으로 하지만 가능한 한 독립적이어야 합니다.
* CFM은 카드/열/목록 보기의 항목에 대한 자체 구현을 제공합니다. 이러한 구현은 기존 Assets 콘텐츠 렌더링 구현에 연결됩니다.
* 콘텐츠 조각을 지원하기 위해 몇 가지 Assets 구성 요소가 확장되었습니다.

### 페이지에서 컨텐츠 조각 사용 {#using-content-fragments-in-pages}

>[!CAUTION]
>
>다음 [콘텐츠 조각 핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html) 이제 가 권장됩니다. 다음을 참조하십시오 [핵심 구성 요소 개발](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html) 을 참조하십시오.

다른 에셋 유형과 마찬가지로 AEM 페이지에서 콘텐츠 조각을 참조할 수 있습니다. AEM에서 제공하는 [**컨텐츠 조각** 핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html) - a [페이지에 콘텐츠 조각을 포함할 수 있는 구성 요소](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page). 다음을 확장할 수도 있습니다. **컨텐츠 조각** 핵심 구성 요소입니다.

* 구성 요소는 `fragmentPath` 속성을 사용하여 실제 콘텐츠 조각을 참조합니다. 다음 `fragmentPath` 속성은 다른 에셋 유형의 유사한 속성과 동일한 방식으로 처리됩니다(예: 콘텐츠 조각을 다른 위치로 이동할 때).

* 구성 요소를 사용하여 표시할 변형을 선택할 수 있습니다.
* 또한 출력을 제한하기 위해 단락 범위를 선택할 수 있습니다. 예를 들어 다중 열 출력에 사용할 수 있습니다.
* 구성 요소는 다음을 허용합니다. [중간 콘텐츠](/help/sites-developing/components-content-fragments.md#in-between-content):

   * 여기에서 구성 요소를 사용하여 참조된 조각의 단락 사이에 다른 에셋(이미지 등)을 배치할 수 있습니다.
   * 중간 콘텐츠 의 경우 다음을 수행해야 합니다.

      * 참조가 불안정할 수 있습니다. 중간 콘텐츠(페이지 작성 시 추가됨)는 옆에 있는 단락에 고정 관계가 없으며, 중간 콘텐츠의 위치가 상대 위치를 잃을 수 있기 전에 콘텐츠 조각 편집기에 새 단락을 삽입합니다
      * 검색 결과에 긍정 오류(false positive)를 방지하려면 추가 매개 변수(예: 변형 및 단락 필터)를 고려하십시오

>[!NOTE]
>
>**콘텐츠 조각 모델:**
>
>페이지의 콘텐츠 조각 모델을 기반으로 한 콘텐츠 조각을 사용하는 경우 해당 모델이 참조됩니다. 즉, 페이지를 게시할 때 모델이 게시되지 않은 경우 여기에 플래그가 지정되고 모델이 페이지와 함께 게시할 리소스에 추가됩니다.
>
>**컨텐츠 조각 템플릿:**
>
>페이지에서 콘텐츠 조각 템플릿을 기반으로 한 콘텐츠 조각을 사용하는 경우 조각을 만들 때 템플릿이 복사되었으므로 참조가 없습니다.

#### OSGi 콘솔을 사용한 구성 {#configuration-using-osgi-console}

컨텐츠 조각의 백엔드 구현은 예를 들어, 페이지에서 사용된 조각의 인스턴스를 검색할 수 있도록 하거나 혼합 미디어 컨텐츠를 관리하는 역할을 합니다. 이 구현은 조각 렌더링에 사용되는 구성 요소와 렌더링이 매개 변수화되는 방법을 알아야 합니다.

이에 대한 매개 변수는 [웹 콘솔](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)OSGi 번들의 경우 **콘텐츠 조각 구성 요소 구성**.

* **리소스 유형**
의 목록 `sling:resourceTypes` 는 콘텐츠 조각을 렌더링하는 데 사용되는 구성 요소와 배경 처리를 적용할 위치를 정의하는 데 제공될 수 있습니다.

* **참조 속성**
속성 목록은 조각에 대한 참조가 각각의 컴포넌트에 대해 저장되는 위치를 지정하도록 구성될 수 있다.

>[!NOTE]
>
>속성과 구성 요소 유형 간에는 직접 매핑되지 않습니다.
>
>AEM은 단락에서 찾을 수 있는 첫 번째 속성을 사용합니다. 그래서 당신은 속성을 신중하게 선택해야합니다.

![screenshot_2019-03-18at100941](assets/screenshot_2019-03-18at100941.png)

구성 요소가 콘텐츠 조각 백그라운드 처리와 호환되는지 확인하기 위해 수행해야 하는 몇 가지 지침이 있습니다.

* 렌더링할 요소가 정의된 속성의 이름은 다음 중 하나여야 합니다. `element` 또는 `elementNames`.

* 렌더링할 변형이 정의된 속성의 이름은 다음 중 하나여야 합니다. `variation` 또는 `variationName`.

* 여러 요소의 출력이 지원되는 경우(를 사용하여) `elementNames` 여러 요소를 지정하려면 실제 표시 모드를 속성으로 정의합니다 `displayMode`:

   * 값이 인 경우 `singleText` (그리고 구성된 요소가 하나만 있음), 요소는 중간 컨텐츠, 레이아웃 지원 등이 있는 텍스트로 렌더링됩니다. 단일 요소만 렌더링되는 조각의 기본값입니다.
   * 그렇지 않으면 훨씬 더 간단한 접근 방식(&quot;양식 보기&quot;라고 할 수 있음)이 사용됩니다. 여기에서는 중간 콘텐츠가 지원되지 않으며 조각 콘텐츠가 &quot;있는 그대로&quot; 렌더링됩니다.

* 조각이 다음에 대해 렌더링되는 경우 `displayMode` == `singleText` (암시적 또는 명시적으로) 다음 추가 속성이 적용됩니다.

   * `paragraphScope` 모든 단락을 렌더링할지 또는 단락 범위만 렌더링할지 여부를 정의합니다(값: `all` 및 `range`)

   * if `paragraphScope` == `range` 그런 다음 속성 `paragraphRange` 렌더링할 단락의 범위를 정의합니다.

### 다른 프레임워크와 통합 {#integration-with-other-frameworks}

컨텐츠 조각은 다음과 통합할 수 있습니다.

* **번역**

  콘텐츠 조각은 [AEM 번역 워크플로](/help/sites-administering/tc-manage.md). 아키텍처 수준에서 이는 다음을 의미합니다.

   * 컨텐츠 조각의 개별 번역은 실제로 별도의 조각입니다. 예를 들면 다음과 같습니다.

      * 이러한 언어 루트는 서로 다른 언어 루트 아래에 있습니다.

        `/content/dam/<path>/en/<to>/<fragment>`

        및

        `/content/dam/<path>/de/<to>/<fragment>`

      * 하지만 언어 루트 아래에서 정확히 동일한 상대 경로를 공유합니다.

        `/content/dam/<path>/en/<to>/<fragment>`

        및

        `/content/dam/<path>/de/<to>/<fragment>`

   * 규칙 기반 경로 외에, 콘텐츠 조각의 서로 다른 언어 버전 간에는 더 이상 연결되지 않습니다. UI에서 언어 변형 사이를 이동하는 수단을 제공하긴 하지만, 두 개의 개별 조각으로 처리됩니다.

  >[!NOTE]
  >
  >AEM 번역 워크플로우는 `/content`:
  >
  >* 콘텐츠 조각 모델 위치 `/conf`, 이러한 번역은 포함되지 않습니다. 다음을 수행할 수 있습니다. [UI 문자열 다국어화](/help/sites-developing/i18n-dev.md).
  >
  >* 템플릿은 조각이 암시적으로 생성되도록 복사됩니다.

* **메타데이터 스키마**

   * 콘텐츠 조각 (재)사용 [메타데이터 스키마](/help/assets/metadata-schemas.md)를 설정하는 것이 좋습니다.
   * CFM은 고유한 특정 스키마를 제공합니다.

     `/libs/dam/content/schemaeditors/forms/contentfragment`

     필요한 경우 이를 연장할 수 있습니다.

   * 각 스키마 양식은 조각 편집기와 통합됩니다.

## 콘텐츠 조각 관리 API - 서버측 {#the-content-fragment-management-api-server-side}

서버측 API를 사용하여 콘텐츠 조각에 액세스할 수 있습니다. 다음을 참조하십시오.

[com.adobe.cq.dam.cfm](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/package-summary.html)

>[!CAUTION]
>
>콘텐츠 구조에 직접 액세스하는 대신 서버측 API를 사용하는 것이 좋습니다.

### 주요 인터페이스 {#key-interfaces}

다음 세 가지 인터페이스는 진입점 역할을 할 수 있습니다.

* **조각 템플릿** ([조각 템플릿](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html))

  사용 `FragmentTemplate.createFragment()` 조각을 만드는 데 사용됩니다.

  ```
  Resource templateOrModelRsc = resourceResolver.getResource("...");
  FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
  ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
  ```

  이 인터페이스는 다음을 나타냅니다.

   * 콘텐츠 조각을 만들 콘텐츠 조각 모델 또는 콘텐츠 조각 템플릿
   * 및 (생성 후) 해당 조각의 구조 정보

  이 정보는 다음과 같습니다.

   * 기본 데이터 액세스(제목, 설명)
   * 조각 요소의 템플릿/모델에 액세스합니다.

      * 목록 요소 템플릿
      * 주어진 요소에 대한 구조 정보 가져오기
      * 요소 템플릿에 액세스( 참조) `ElementTemplate`)

   * 조각 변형에 대한 템플릿에 액세스합니다.

      * 목록 변형 템플릿
      * 주어진 변형에 대한 구조적 정보 가져오기
      * 변형 템플릿 액세스( 참조) `VariationTemplate`)

   * 초기 관련 콘텐츠 가져오기

  중요한 정보를 나타내는 인터페이스:

   * `ElementTemplate`

      * 기본 데이터(이름, 제목) 가져오기
      * 초기 요소 콘텐츠 가져오기

   * `VariationTemplate`

      * 기본 데이터(이름, 제목, 설명) 가져오기

* **컨텐츠 조각** ([ContentFragment](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

  이 인터페이스를 사용하면 추상적인 방식으로 콘텐츠 조각을 사용하여 작업할 수 있습니다.

  >[!CAUTION]
  >
  >이 인터페이스를 통해 조각에 액세스하는 것이 좋습니다. 콘텐츠 구조를 직접 변경하지 말아야 합니다.

  인터페이스는 다음과 같은 수단을 제공합니다.

   * 기본 데이터 관리(예: 이름 가져오기, 제목/설명 가져오기/설정)
   * 메타데이터 액세스
   * 액세스 요소:

      * 목록 요소
      * 이름별 요소 가져오기
      * 새 요소 만들기(참조) [주의 사항](#caveats))

      * 요소 데이터 액세스(참조) `ContentElement`)

   * 조각에 대해 정의된 목록 변형
   * 전체적으로 새 변형 만들기
   * 관련 콘텐츠 관리:

      * 컬렉션 나열
      * 컬렉션 추가
      * 컬렉션 제거

   * 조각의 모델 또는 템플릿 액세스

  조각의 주요 요소를 나타내는 인터페이스는 다음과 같습니다.

   * **컨텐츠 요소** ([ContentElement](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * 기본 데이터(이름, 제목, 설명) 가져오기
      * 콘텐츠 가져오기/설정
      * 요소의 변형 액세스:

         * 목록 변형
         * 이름별 변형 가져오기
         * 새 변형 만들기(참조) [주의 사항](#caveats))
         * 변형 제거(참조) [주의 사항](#caveats))
         * 변형 데이터 액세스(참조) `ContentVariation`)

      * 변형 해결을 위한 바로 가기(지정된 변형을 요소에 사용할 수 없는 경우 구현별 추가 폴백 논리 적용)

   * **컨텐츠 변형** ([ContentVariation](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * 기본 데이터(이름, 제목, 설명) 가져오기
      * 콘텐츠 가져오기/설정
      * 마지막으로 수정된 정보를 기반으로 한 간단한 동기화

  세 가지 인터페이스 모두( `ContentFragment`, `ContentElement`, `ContentVariation`) 확장 `Versionable` 컨텐츠 조각에 필요한 버전 관리 기능을 추가하는 인터페이스:

   * 요소의 새 버전 만들기
   * 요소의 목록 버전
   * 버전이 지정된 요소의 특정 버전 콘텐츠 가져오기

### 적응 - adaptTo() 사용 {#adapting-using-adaptto}

다음 항목을 조정할 수 있습니다.

* `ContentFragment` 을 다음과 같이 조정할 수 있습니다.

   * `Resource` - 기본 Sling 리소스. 기본 업데이트 `Resource` 직접, 을(를) 다시 빌드해야 합니다. `ContentFragment` 개체.

   * `Asset` - DAM `Asset` 콘텐츠 조각을 나타내는 추상화. `Asset` 직접, 을(를) 다시 빌드해야 합니다. `ContentFragment` 개체.

* `ContentElement` 을 다음과 같이 조정할 수 있습니다.

   * `ElementTemplate` - 요소의 구조 정보에 액세스합니다.

* `FragmentTemplate` 을 다음과 같이 조정할 수 있습니다.

   * `Resource` - `Resource` 참조된 모델 또는 복사한 원본 템플릿을 확인하는 중

      * 을(를) 통해 변경된 사항 `Resource` 에 자동으로 반영되지 않음 `FragmentTemplate`.

* `Resource` 을 다음과 같이 조정할 수 있습니다.

   * `ContentFragment`
   * `FragmentTemplate`

### 주의 사항 {#caveats}

주의해야 할 사항은 다음과 같습니다.

* API는 UI에서 지원하는 기능을 제공하도록 구현됩니다.
* 전체 API는 **아님** api JavaDoc에 별도로 명시되지 않는 한 변경 사항을 자동으로 유지합니다. 따라서 항상 각 요청의 리소스 해결자(또는 실제로 사용 중인 해결자)를 커밋해야 합니다.
* 추가 작업이 필요할 수 있는 작업:

   * 새 요소를 만들거나 제거해도 조각 템플릿 기반 단순 조각의 데이터 구조는 업데이트되지 않습니다.
   * 에서 새 변형 만들기 `ContentElement` 는 데이터 구조를 업데이트하지 않지만 에서 전역적으로 생성합니다. `ContentFragment` will).

   * 기존 변형을 제거해도 데이터 구조가 업데이트되지 않습니다.

## 콘텐츠 조각 관리 API - 클라이언트측 {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>AEM 6.5의 경우 클라이언트측 API는 내부에 있습니다.

### 추가 정보 {#additional-information}

다음을 참조하십시오.

* `filter.xml`

  다음 `filter.xml` 의 콘텐츠 조각 관리는 에셋 핵심 콘텐츠 패키지와 겹치지 않도록 구성됩니다.

## 세션 편집 {#edit-sessions}

편집 세션은 사용자가 편집기 페이지 중 하나에서 콘텐츠 조각을 열 때 시작됩니다. 사용자가 다음 중 하나를 선택하여 편집기를 떠나면 편집 세션이 종료됩니다 **저장** 또는 **취소**.

### 요구 사항 {#requirements}

편집 세션을 제어하기 위한 요구 사항은 다음과 같습니다.

* 여러 보기(= HTML 페이지)에 걸쳐 있을 수 있는 컨텐츠 조각을 편집하는 것은 원자여야 합니다.
* 또한 편집은 다음과 같아야 합니다 *트랜잭션*; 편집 세션이 끝나면 변경 사항을 커밋(저장)하거나 롤백(취소)해야 합니다.
* Edge 사례는 제대로 처리해야 합니다. 예를 들어 사용자가 URL을 수동으로 입력하거나 전역 탐색을 사용하여 페이지를 나가는 경우와 같은 상황이 포함됩니다.
* 데이터 손실을 방지하기 위해 정기적으로 자동 저장 (x분마다)을 사용해야 합니다.
* 두 사용자가 동시에 콘텐츠 조각을 편집하는 경우 서로의 변경 사항을 덮어쓰면 안 됩니다.

#### 프로세스 {#processes}

관련된 프로세스는 다음과 같습니다.

* 세션 시작

   * 콘텐츠 조각의 새 버전이 만들어집니다.
   * 자동 저장이 시작되었습니다.
   * 쿠키가 설정됩니다. 쿠키는 현재 편집된 조각을 정의하며 편집 세션이 열려 있습니다.

* 세션 완료

   * 자동 저장이 중지되었습니다.
   * 커밋 시:

      * 마지막으로 수정된 정보가 업데이트됩니다.
      * 쿠키가 제거됩니다.

   * 롤백 시:

      * 편집 세션이 시작될 때 만들어진 콘텐츠 조각의 버전이 복원됩니다.
      * 쿠키가 제거됩니다.

* 편집

   * 모든 변경 사항(자동 저장 포함)은 분리된 보호 영역이 아닌 활성 콘텐츠 조각에서 수행됩니다.
   * 따라서 이러한 변경 사항은 각 콘텐츠 조각을 참조하는 AEM 페이지에 즉시 반영됩니다

#### 액션 {#actions}

가능한 작업은 다음과 같습니다.

* 페이지 입력

   * 각 쿠키를 확인하여 편집 세션이 이미 있는지 확인합니다.

      * 존재하는 경우 현재 편집 중인 콘텐츠 조각에 대한 편집 세션이 시작되었는지 확인합니다

         * 현재 조각인 경우 세션을 다시 설정합니다.
         * 그렇지 않은 경우 이전에 편집한 콘텐츠 조각에 대한 편집을 취소하고 쿠키를 제거해 보십시오(나중에 편집 세션이 표시되지 않음).

      * 편집 세션이 존재하지 않는 경우 사용자가 처음으로 변경할 때까지 기다립니다(아래 참조).

   * 페이지에서 콘텐츠 조각이 이미 참조되었는지 확인하고 참조된 경우 적절한 정보를 표시합니다.

* 콘텐츠 변경

   * 사용자가 콘텐츠를 변경하고 편집 세션이 없을 때마다 새 편집 세션이 만들어집니다(참조) [세션 시작](#processes)).

* 페이지 나가기

   * 편집 세션이 있고 변경 사항이 지속되지 않는 경우, 사용자에게 잠재적인 콘텐츠 손실을 알리고 페이지에서 머물 수 있도록 해 주는 모달 확인 대화 상자가 표시됩니다.

## 예 {#examples}

### 예: 기존 콘텐츠 조각 액세스 {#example-accessing-an-existing-content-fragment}

이를 위해 API를 나타내는 리소스를 다음과 같이 조정할 수 있습니다.

`com.adobe.cq.dam.cfm.ContentFragment`

예:

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### 예제: 컨텐츠 조각 만들기 {#example-creating-a-new-content-fragment}

프로그래밍 방식으로 콘텐츠 조각을 만들려면 다음을 사용해야 합니다.

`com.adobe.cq.dam.cfm.ContentFragmentManager#create`

예:

```java
Resource templateOrModelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### 예: 자동 저장 간격 지정 {#example-specifying-the-auto-save-interval}

자동 저장 간격(초 단위)은 구성 관리자(ConfMgr)를 사용하여 정의할 수 있습니다.

* 노드: `<*conf-root*>/settings/dam/cfm/jcr:content`
* 속성 이름: `autoSaveInterval`
* 유형: `Long`

* 기본값: `600` (10분); 다음에서 정의됨: `/libs/settings/dam/cfm/jcr:content`

자동 저장 간격을 5분으로 설정하려면 노드의 속성을 정의해야 합니다. 예를 들면 다음과 같습니다.

* 노드: `/conf/global/settings/dam/cfm/jcr:content`
* 속성 이름: `autoSaveInterval`

* 유형: `Long`

* 값: `300` (5분은 300초와 동일)

## 콘텐츠 조각 템플릿 {#content-fragment-templates}

다음을 참조하십시오 [콘텐츠 조각 템플릿](/help/sites-developing/content-fragment-templates.md) 전체 정보.

## 페이지 작성을 위한 구성 요소 {#components-for-page-authoring}

자세한 내용은

* [핵심 구성 요소 - 콘텐츠 조각 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html) (권장)
* [콘텐츠 조각 구성 요소 - 페이지 작성을 위한 구성 요소](/help/sites-developing/components-content-fragments.md#components-for-page-authoring)
