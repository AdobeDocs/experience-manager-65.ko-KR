---
title: 컨텐츠 조각 사용자 지정 및 확장
seo-title: Customizing and Extending Content Fragments
description: 컨텐츠 조각은 표준 자산을 확장합니다.
seo-description: A content fragment extends a standard asset.
uuid: f72c3a23-9b0d-4fab-a960-bb1350f01175
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d0770bee-4be5-4a6a-8415-70fdfd75015c
docset: aem65
exl-id: 08c88e70-4df9-4627-8a66-1fabe3aee50b
source-git-commit: e68f6203d7629cab16e59778ce64908f943d5b3f
workflow-type: tm+mt
source-wordcount: '2789'
ht-degree: 1%

---


# 컨텐츠 조각 사용자 지정 및 확장{#customizing-and-extending-content-fragments}

컨텐츠 조각은 표준 자산을 확장합니다. 다음을 참조하십시오.

* [컨텐츠 조각 만들기 및 관리](/help/assets/content-fragments/content-fragments.md) 및 [컨텐츠 조각으로 페이지 작성](/help/sites-authoring/content-fragments.md) 컨텐츠 조각에 대한 자세한 정보.

* [자산 관리](/help/assets/manage-assets.md) 및 [자산 사용자 지정 및 확장](/help/assets/extending-assets.md) 표준 자산에 대한 추가 정보.

## 아키텍처 {#architecture}

기본 [구성 부분](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 컨텐츠 조각의 유형은 다음과 같습니다.

* A *컨텐츠 조각,*
* 하나 이상으로 구성 *콘텐츠 요소* s,
* 하나 이상의 *컨텐츠 변형* s.

조각 유형에 따라 모델 또는 템플릿도 사용됩니다.

>[!CAUTION]
>
>[컨텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md) 새 조각을 모두 만드는 데 권장됩니다.
>
>컨텐츠 조각 모델은 WKND의 모든 예에 사용됩니다.

>[!NOTE]
>
>AEM 6.3 이전 컨텐츠 조각은 모델 대신 템플릿을 기반으로 작성되었습니다.
>
>컨텐츠 조각 템플릿은 이제 더 이상 사용되지 않습니다. 조각을 만드는 데에는 여전히 사용할 수 있지만, 대신 컨텐츠 조각 모델 을 사용하는 것이 좋습니다. 조각 템플릿에 새로운 기능이 추가되지 않으며, 향후 버전에서 제거됩니다.

* 컨텐츠 조각 모델:

   * 구조화된 컨텐츠를 포함하는 컨텐츠 조각을 정의하는 데 사용됩니다.
   * 컨텐츠 조각 모델은 컨텐츠 조각을 만들 때 컨텐츠 조각의 구조를 정의합니다.
   * 조각은 모델을 참조합니다. 따라서 모델 변경 사항은 모든 종속 조각에 영향을 줄 수/있을 것입니다.
   * 모델은 데이터 유형을 기반으로 합니다.
   * 새 변형 등을 추가하는 함수는 그에 따라 조각을 업데이트해야 합니다.

   >[!CAUTION]
   >
   >기존 컨텐츠 조각 모델을 변경하면 종속된 조각이 영향을 받을 수 있습니다. 이로 인해 해당 조각에서 고아 속성이 생길 수 있습니다.

* 컨텐츠 조각 템플릿:

   * 단순 컨텐츠 조각을 정의하는 데 사용됩니다.
   * 템플릿은 컨텐츠 조각을 만들 때 컨텐츠 조각의 (기본, 텍스트 전용) 구조를 정의합니다.
   * 템플릿이 생성되면 조각에 복사됩니다. 따라서 템플릿에 대한 추가 변경 사항은 기존 조각에 반영되지 않습니다.
   * 새 변형 등을 추가하는 함수는 그에 따라 조각을 업데이트해야 합니다.
   * [컨텐츠 조각 템플릿](/help/sites-developing/content-fragment-templates.md) 는 AEM 에코시스템(예: 페이지 템플릿 등) 내의 다른 템플릿 메커니즘과 다른 방식으로 작동합니다. 따라서 별도로 고려해야 합니다.
   * 템플릿을 기준으로 할 때 컨텐츠의 MIME 유형은 실제 컨텐츠에서 관리됩니다. 즉, 각 요소와 변형에는 다른 MIME 유형이 있을 수 있습니다.

### 자산과 통합 {#integration-with-assets}

CFM(컨텐츠 조각 관리)은 다음 방법으로 AEM Assets에 포함되어 있습니다.

* 컨텐츠 조각은 자산입니다.
* 기존 자산 기능을 사용합니다.
* 자산(관리 콘솔 등)과 완전히 통합됩니다.

#### 구조화된 컨텐츠 조각을 자산에 매핑 {#mapping-structured-content-fragments-to-assets}

![자산 간 구조](assets/fragment-to-assets-structured.png)

구조화된 컨텐츠(즉, 컨텐츠 조각 모델 기반)가 있는 컨텐츠 조각은 단일 자산에 매핑됩니다.

* 모든 컨텐츠는 `jcr:content/data` 자산의 노드:

   * 요소 데이터는 마스터 하위 노드 아래에 저장됩니다.
      `jcr:content/data/master`

   * 변형은 변형의 이름을 전달하는 하위 노드 아래에 저장됩니다. 예 `jcr:content/data/myvariation`

   * 각 요소의 데이터는 각 하위 노드에 요소 이름을 사용하는 속성으로 저장됩니다. 예: 요소의 컨텐츠 `text` 는 속성으로 저장됩니다. `text` on `jcr:content/data/master`

* 메타데이터 및 관련 컨텐츠는 아래에 저장됩니다 `jcr:content/metadata`
일반 메타데이터로 간주되지 않고 
`jcr:content`

#### 단순 컨텐츠 조각을 자산에 매핑 {#mapping-simple-content-fragments-to-assets}

![chlimage_1-90](assets/chlimage_1-90.png)

템플릿 기반의 단순 컨텐츠 조각은 기본 자산 및 (선택 사항) 하위 자산으로 구성된 컴포지션에 매핑됩니다.

* 조각의 모든 비컨텐츠 정보(예: 제목, 설명, 메타데이터, 구조)는 기본 자산에서만 관리됩니다.
* 조각의 첫 번째 요소의 컨텐츠는 기본 자산의 원래 표현물에 매핑됩니다.

   * 첫 번째 요소의 변형(있는 경우)은 기본 자산의 다른 표현물에 매핑됩니다.

* 추가 요소(있는 경우)가 기본 자산의 하위 자산에 매핑됩니다.

   * 이러한 추가 요소의 주요 컨텐츠는 각 하위 자산의 원래 표현물에 매핑됩니다.
   * 추가 요소의 다른 변형(해당하는 경우)은 각 하위 자산의 다른 표현물에 매핑됩니다.

#### 자산 위치 {#asset-location}

표준 자산과 마찬가지로 컨텐츠 조각도 다음 위치에 유지됩니다.

`/content/dam`

#### 자산 권한 {#asset-permissions}

자세한 내용은 [컨텐츠 조각 - 삭제 고려 사항](/help/assets/content-fragments/content-fragments-delete.md).

#### 기능 통합 {#feature-integration}

* CFM(컨텐츠 조각 관리) 기능은 자산 코어를 기반으로 구축되지만 가능한 한 독립적인 것이어야 합니다.
* CFM은 카드/열/목록 보기의 항목에 대한 자체 구현을 제공합니다. 이러한 플러그인은 기존 자산 콘텐츠 렌더링 구현에 연결됩니다.
* 여러 자산 구성 요소가 컨텐츠 조각에 맞게 확장되었습니다.

### 페이지에서 컨텐츠 조각 사용 {#using-content-fragments-in-pages}

>[!CAUTION]
>
>다음 [컨텐츠 조각 코어 구성 요소](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html) 이제 이 권장됩니다. 자세한 내용은 [핵심 구성 요소 개발](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) 자세한 내용

컨텐츠 조각은 다른 자산 유형처럼 AEM 페이지에서 참조할 수 있습니다. AEM에서 [**컨텐츠 조각** 코어 구성 요소](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html) - a [페이지에 컨텐츠 조각을 포함할 수 있는 구성 요소](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page). 확장도 가능합니다 **컨텐츠 조각** 코어 구성 요소입니다.

* 구성 요소는 `fragmentPath` 실제 컨텐츠 조각을 참조하는 속성입니다. 다음 `fragmentPath` 속성은 다른 자산 유형의 속성과 유사한 방식으로 처리됩니다. 예를 들어 컨텐츠 조각을 다른 위치로 이동할 때.

* 구성 요소로 표시할 변형을 선택할 수 있습니다.
* 또한 출력을 제한하기 위해 다양한 단락을 선택할 수 있습니다. 예를 들어 다중 열 출력에 사용할 수 있습니다.
* 구성 요소는 [중간 컨텐츠](/help/sites-developing/components-content-fragments.md#in-between-content):

   * 구성 요소로 다른 자산(이미지 등)을 배치할 수 있습니다. 를 반환합니다.
   * 중간 컨텐츠의 경우 다음을 수행해야 합니다.

      * 불안정한 참고의 가능성을 인식하다. 중간 컨텐츠(페이지를 작성할 때 추가됨)에는 옆에 배치된 단락과 고정된 관계가 없으며 중간 컨텐츠의 위치가 상대 위치를 잃게 되기 전에 새 단락(컨텐츠 조각 편집기에서)을 삽입합니다
      * 검색 결과에 긍정 오류가 발생하지 않도록 추가 매개 변수(예: 변형 및 단락 필터)를 고려합니다

>[!NOTE]
>
>**컨텐츠 조각 모델:**
>
>페이지에서 컨텐츠 조각 모델을 기반으로 한 컨텐츠 조각을 사용할 때 모델이 참조됩니다. 즉, 페이지를 게시할 때 모델이 게시되지 않은 경우 이 플래그가 지정되고 모델이 페이지와 함께 게시될 리소스에 추가됩니다.
>
>**컨텐츠 조각 템플릿:**
>
>페이지에서 컨텐츠 조각 템플릿을 기반으로 한 컨텐츠 조각을 사용할 때 조각을 만들 때 템플릿이 복사되어 참조가 없습니다.

#### OSGi 콘솔을 사용한 구성 {#configuration-using-osgi-console}

컨텐츠 조각의 백엔드 구현은 예를 들어 페이지에서 사용되는 조각의 인스턴스를 검색 가능하게 하거나 혼합 미디어 컨텐츠를 관리하는 책임이 있습니다. 이 구현은 조각 렌더링에 사용되는 구성 요소와 렌더링이 매개 변수화되는 방법을 알고 있어야 합니다.

이에 대한 매개 변수는 [웹 콘솔](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), OSGi 번들 **컨텐츠 조각 구성 요소 구성**.

* **리소스 유형**
목록 
`sling:resourceTypes` 컨텐츠 조각 렌더링에 사용되는 구성 요소와 배경 처리를 적용해야 하는 위치를 정의하는 데 제공될 수 있습니다.

* **참조 속성**
속성 목록을 구성하여 각 구성 요소에 대해 조각 참조가 저장되는 위치를 지정할 수 있습니다.

>[!NOTE]
>
>속성과 구성 요소 유형 간에는 직접 매핑이 없습니다.
>
>AEM에서는 단락에 있는 첫 번째 속성을 사용합니다. 따라서 속성을 신중하게 선택해야 합니다.

![스크린샷_2019-03-18at100941](assets/screenshot_2019-03-18at100941.png)

구성 요소가 컨텐츠 조각 백그라운드 처리와 호환되는지 확인하기 위해 따라야 할 몇 가지 지침이 있습니다.

* 렌더링할 요소를 정의하는 속성의 이름은 다음 중 하나여야 합니다 `element` 또는 `elementNames`.

* 렌더링할 변형을 정의하는 속성의 이름은 다음 중 하나여야 합니다 `variation` 또는 `variationName`.

* 여러 요소의 출력이 지원되는 경우 `elementNames` 여러 요소를 지정하려면 실제 디스플레이 모드가 등록 정보별로 정의됩니다 `displayMode`:

   * 값이 `singleText` (그리고 구성된 요소는 하나만 있음) 요소가 중간 컨텐츠, 레이아웃 지원 등이 있는 텍스트로 렌더링됩니다. 단일 요소만 렌더링되는 조각의 기본값입니다.
   * 그렇지 않으면 중간 컨텐츠가 지원되지 않고 조각 컨텐츠가 &quot;있는 그대로&quot; 렌더링되는 훨씬 간단한 방법이 사용됩니다(&quot;양식 보기&quot;라고 할 수 있음).

* 조각이 용 렌더링되는 경우 `displayMode` == `singleText` (암시적 또는 명시적으로) 다음과 같은 추가 속성이 재생됩니다.

   * `paragraphScope` 모든 단락을 렌더링할지 또는 단락 범위만 렌더링할지를 정의합니다(값: `all` 및 `range`)

   * if `paragraphScope` == `range` 그런 다음 속성을 사용합니다 `paragraphRange` 렌더링할 단락 범위를 정의합니다

### 다른 프레임워크와의 통합 {#integration-with-other-frameworks}

컨텐츠 조각은 다음과 통합할 수 있습니다.

* **번역**

   컨텐츠 조각은 [AEM 번역 워크플로우](/help/sites-administering/tc-manage.md). 아키텍처 수준에서, 이것은 다음을 의미합니다.

   * 컨텐츠 조각의 개별 번역은 실제로 별도의 조각입니다. 예:

      * 다른 언어 루트 아래에 있습니다.

         `/content/dam/<path>/en/<to>/<fragment>`

         및

         `/content/dam/<path>/de/<to>/<fragment>`

      * 하지만 언어 루트 아래에 정확히 동일한 상대 경로를 공유합니다.

         `/content/dam/<path>/en/<to>/<fragment>`

         및

         `/content/dam/<path>/de/<to>/<fragment>`
   * 규칙 기반 경로 외에 컨텐츠 조각의 다른 언어 버전 간에 더 이상 연결할 수 없습니다. 언어 변형을 탐색하는 수단을 UI에서 제공하지만 두 개의 개별 조각으로 처리됩니다.
   >[!NOTE]
   >
   >AEM 번역 워크플로우는에서 작동합니다. `/content`:
   >
   >* 컨텐츠 조각 모델은 `/conf`에는 이러한 번역이 포함되지 않습니다. 다음을 수행할 수 있습니다 [UI 문자열 다국어화](/help/sites-developing/i18n-dev.md).
   >
   >* 템플릿이 복사되어 조각을 생성되므로 이것은 암시적입니다.


* **메타데이터 스키마**

   * 컨텐츠 조각(재)은 [메타데이터 스키마](/help/assets/metadata-schemas.md), 표준 자산으로 정의할 수 있습니다.
   * CFM은 고유한 특정 스키마를 제공합니다.

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      필요한 경우 확장할 수 있습니다.

   * 각 스키마 양식은 조각 편집기와 통합됩니다.

## 컨텐츠 조각 관리 API - 서버측 {#the-content-fragment-management-api-server-side}

서버측 API를 사용하여 컨텐츠 조각에 액세스할 수 있습니다. 다음을 참조하십시오.

[com.adobe.cq.dam.cfm](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/package-summary.html)

>[!CAUTION]
>
>컨텐츠 구조에 직접 액세스하는 대신 서버측 API를 사용하는 것이 좋습니다.

### 주요 인터페이스 {#key-interfaces}

다음 세 개의 인터페이스가 시작 지점으로 사용될 수 있습니다.

* **조각 템플릿** ([조각 템플릿](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html))

   사용 `FragmentTemplate.createFragment()` 새 조각을 생성하기 위한 것입니다.

   ```
   Resource templateOrModelRsc = resourceResolver.getResource("...");
   FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
   ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
   ```

   이 인터페이스는 다음을 나타냅니다.

   * 컨텐츠 조각을 생성할 컨텐츠 조각 모델 또는 컨텐츠 조각 템플릿
   * 및 (생성 후) 해당 조각의 구조적 정보

   이 정보에는 다음이 포함될 수 있습니다.

   * 기본 데이터 액세스(제목, 설명)
   * 조각 요소에 대한 템플릿/모델에 액세스합니다.

      * 목록 요소 템플릿
      * 주어진 요소에 대한 구조적 정보 가져오기
      * 요소 템플릿에 액세스합니다. 자세한 내용은 `ElementTemplate`)
   * 조각의 변형에 대한 템플릿에 액세스합니다.

      * 변형 템플릿 나열
      * 주어진 변형에 대한 구조적 정보 가져오기
      * 변형 템플릿에 액세스( `VariationTemplate`)
   * 초기 관련 컨텐츠 가져오기

   중요한 정보를 나타내는 인터페이스:

   * `ElementTemplate`

      * 기본 데이터 가져오기(이름, 제목)
      * 초기 요소 콘텐츠 가져오기
   * `VariationTemplate`

      * 기본 데이터 가져오기(이름, 제목, 설명)






* **컨텐츠 조각** ([컨텐츠 조각](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   이 인터페이스를 사용하면 컨텐츠 조각을 추상적으로 사용할 수 있습니다.

   >[!CAUTION]
   >
   >이 인터페이스를 통해 조각에 액세스하는 것이 좋습니다. 컨텐츠 구조를 직접 변경하지 않아야 합니다.

   인터페이스는 다음 방법을 제공합니다.

   * 기본 데이터 관리(예: 이름 가져오기; get/set title/description)
   * 메타데이터 액세스
   * 액세스 요소:

      * 목록 요소
      * 이름별로 요소 가져오기
      * 새 요소 만들기( [경고](#caveats))

      * 요소 데이터에 액세스( `ContentElement`)
   * 조각에 대해 정의된 목록 변형
   * 새로운 변형을 전체적으로 만들기
   * 관련 컨텐츠 관리:

      * 컬렉션 나열
      * 컬렉션 추가
      * 컬렉션 제거
   * 조각의 모델 또는 템플릿에 액세스

   조각의 주요 요소를 나타내는 인터페이스는 다음과 같습니다.

   * **콘텐츠 요소** ([ContentElement](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * 기본 데이터 가져오기(이름, 제목, 설명)
      * 콘텐츠 가져오기/설정
      * 요소의 변형에 액세스합니다.

         * 목록 변형
         * 이름별로 변형 가져오기
         * 새 변형 만들기( [경고](#caveats))
         * 변형 제거(참조) [경고](#caveats))
         * 변형 데이터에 액세스( `ContentVariation`)
      * 변형 해결을 위한 바로 가기(지정된 변형을 요소에 사용할 수 없는 경우 몇 가지 추가 구현별 폴백 논리 적용)
   * **컨텐츠 변형** ([컨텐츠 변형](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * 기본 데이터 가져오기(이름, 제목, 설명)
      * 콘텐츠 가져오기/설정
      * 마지막 수정된 정보를 기반으로 간단한 동기화

   세 개의 인터페이스 모두 ( `ContentFragment`, `ContentElement`, `ContentVariation`) 확장 `Versionable` 인터페이스: 컨텐츠 조각에 필요한 버전 관리 기능을 추가합니다.

   * 요소의 새 버전 만들기
   * 요소의 버전 나열
   * 버전이 지정된 요소의 특정 버전의 콘텐츠를 가져옵니다







### 적용 - adaptTo() 사용 {#adapting-using-adaptto}

다음을 적용할 수 있습니다.

* `ContentFragment` 다음을 적용할 수 있습니다.

   * `Resource` - 기본 Sling 리소스 기본 `Resource` 직접, 재구축 필요 `ContentFragment` 개체.

   * `Asset` - DAM `Asset` 컨텐츠 조각을 나타내는 추상화 업데이트 `Asset` 직접, 재구축 필요 `ContentFragment` 개체.

* `ContentElement` 다음을 적용할 수 있습니다.

   * `ElementTemplate` - 요소의 구조적 정보에 액세스하기 위한 것입니다.

* `FragmentTemplate` 다음을 적용할 수 있습니다.

   * `Resource` - `Resource` 참조된 모델 또는 복사한 원래 템플릿 확인

      * 를 통해 `Resource` 에 자동으로 반영되지 않습니다 `FragmentTemplate`.

* `Resource` 다음을 적용할 수 있습니다.

   * `ContentFragment`
   * `FragmentTemplate`

### 경고 {#caveats}

다음과 같이 명시해야 합니다.

* API는 UI에서 지원하는 기능을 제공하기 위해 구현됩니다.
* 전체 API는 **not** 는 변경 사항을 자동으로 유지합니다(API JavaDoc에 별도로 언급되지 않는 경우). 따라서 항상 각 요청의 리소스 확인자(또는 실제로 사용 중인 해결자)를 커밋해야 합니다.
* 추가 작업이 필요할 수 있는 작업:

   * 새 요소를 만들거나 제거해도 단순 조각의 데이터 구조가 업데이트되지 않습니다(조각 템플릿을 기반으로 함).
   * 에서 새 변형 만들기 `ContentElement` 는 데이터 구조를 업데이트하지 않습니다(그러나 전역적으로 만들기 `ContentFragment` 사용할 수 없습니다.

   * 기존 변형을 제거하면 데이터 구조가 업데이트되지 않습니다.

## 컨텐츠 조각 관리 API - 클라이언트측 {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>AEM 6.5의 경우 클라이언트측 API는 내부입니다.

### 추가 정보 {#additional-information}

다음을 참조하십시오.

* `filter.xml`

   다음 `filter.xml` 컨텐츠 조각 관리의 경우 자산 핵심 컨텐츠 패키지와 겹치지 않도록 구성됩니다.

## 세션 편집 {#edit-sessions}

사용자가 편집기 페이지 중 하나에서 컨텐츠 조각을 열면 편집 세션이 시작됩니다. 사용자가 다음 중 하나를 선택하여 편집기를 벗어나면 편집 세션이 끝납니다 **저장** 또는 **취소**.

### 요구 사항 {#requirements}

편집 세션을 제어하기 위한 요구 사항은 다음과 같습니다.

* 여러 보기(= HTML 페이지)에 걸쳐 있을 수 있는 컨텐츠 조각을 편집하는 것은 원자여야 합니다.
* 편집 작업도 수행해야 합니다 *트랜잭션*; 편집 세션이 끝날 때 변경 내용을 커밋(저장)하거나 롤백하거나(취소됨)해야 합니다.
* 에지 사례는 올바르게 처리해야 합니다. 이러한 정보에는 사용자가 수동으로 URL을 입력하거나 전역 탐색을 사용하여 페이지를 나가는 경우와 같은 경우가 포함됩니다.
* 데이터 손실을 방지하기 위해 x분마다(주기적으로 자동 저장)을 사용할 수 있어야 합니다.
* 두 사용자가 동시에 컨텐츠 조각을 편집하는 경우 서로 다른 사용자의 변경 사항을 덮어쓰지 않아야 합니다.

#### 프로세스 {#processes}

관련 프로세스는 다음과 같습니다.

* 세션 시작

   * 컨텐츠 조각의 새 버전이 만들어집니다.
   * 자동 저장 이 시작됩니다.
   * 쿠키가 설정됨; 이들은 현재 편집된 조각을 정의하며 편집 세션이 열려 있음을 정의합니다.

* 세션 종료

   * 자동 저장이 중지됩니다.
   * 커밋 시:

      * 마지막으로 수정한 정보가 업데이트됩니다.
      * 쿠키가 제거됩니다.
   * 롤백 시:

      * 편집 세션이 시작될 때 생성된 컨텐츠 조각의 버전이 복원됩니다.
      * 쿠키가 제거됩니다.


* 편집

   * 모든 변경 사항(자동 저장 포함)은 분리된 보호 영역이 아니라 활성 컨텐츠 조각에서 수행됩니다.
   * 따라서 이러한 변경 사항은 각 컨텐츠 조각을 참조하는 AEM 페이지에 즉시 반영됩니다

#### 작업 {#actions}

가능한 작업은 다음과 같습니다.

* 페이지 입력

   * 편집 세션이 이미 있는지 확인합니다. 를 눌러 각 쿠키를 확인합니다.

      * 있을 경우 현재 편집 중인 컨텐츠 조각에 대해 편집 세션이 시작되었는지 확인합니다

         * 현재 조각이 있으면 세션을 다시 설정합니다.
         * 그렇지 않은 경우 이전에 편집한 컨텐츠 조각에 대한 편집을 취소하고 쿠키를 제거합니다(나중에 편집 세션 없음).
      * 편집 세션이 없는 경우 사용자가 첫 번째 변경 작업을 기다립니다(아래 참조).
   * 컨텐츠 조각이 페이지에서 이미 참조되어 있는지 확인하고, 있는 경우 적절한 정보를 표시합니다.



* 콘텐츠 변경

   * 사용자가 컨텐츠를 변경하고 편집 세션이 없을 때마다 새 편집 세션이 만들어집니다(참조 [세션 시작](#processes)).

* 페이지 종료

   * 편집 세션이 있고 변경 사항이 지속되지 않은 경우 손실된 컨텐츠를 사용자에게 알리고 해당 컨텐츠를 페이지에 유지할 수 있도록 양식 확인 대화 상자가 표시됩니다.

## 예 {#examples}

### 예: 기존 컨텐츠 조각 액세스 {#example-accessing-an-existing-content-fragment}

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

### 예: 새 컨텐츠 조각 만들기 {#example-creating-a-new-content-fragment}

프로그래밍 방식으로 새 컨텐츠 조각을 생성하려면 다음을 사용해야 합니다.

`com.adobe.cq.dam.cfm.ContentFragmentManager#create`

예:

```java
Resource templateOrModelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### 예: 자동 저장 간격 지정 {#example-specifying-the-auto-save-interval}

자동 저장 간격(초 단위 측정)은 구성 관리자(ConfMgr)를 사용하여 정의할 수 있습니다.

* 노드: `<*conf-root*>/settings/dam/cfm/jcr:content`
* 속성 이름: `autoSaveInterval`
* 유형: `Long`

* 기본값: `600` (10분) 다음에 정의되어 있습니다. `/libs/settings/dam/cfm/jcr:content`

5분의 자동 저장 간격을 설정하려면 노드에서 속성을 정의해야 합니다. 예:

* 노드: `/conf/global/settings/dam/cfm/jcr:content`
* 속성 이름: `autoSaveInterval`

* 유형: `Long`

* 값: `300` (5분은 300초와 같습니다.)

## 컨텐츠 조각 템플릿 {#content-fragment-templates}

자세한 내용은 [컨텐츠 조각 템플릿](/help/sites-developing/content-fragment-templates.md) 자세한 내용

## 페이지 작성용 구성 요소 {#components-for-page-authoring}

자세한 내용은

* [핵심 구성 요소 - 컨텐츠 조각 구성 요소](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html) (권장)
* [컨텐츠 조각 구성 요소 - 페이지 작성을 위한 구성 요소](/help/sites-developing/components-content-fragments.md#components-for-page-authoring)
