---
title: AEM에서 Sling Resource Merger 사용
seo-title: Using the Sling Resource Merger in AEM
description: Sling Resource Merger는 리소스에 액세스하고 병합하는 서비스를 제공합니다
seo-description: The Sling Resource Merger provides services to access and merge resources
uuid: 0a28fdc9-caea-490b-8f07-7c4a6b802e09
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ec712ba0-0fd6-4bb8-93d6-07d09127df58
exl-id: 1eed754e-9a7d-4b65-a929-757fc962614d
source-git-commit: c07fa148054b69b0da7bb402ef96a50d0895abfa
workflow-type: tm+mt
source-wordcount: '1254'
ht-degree: 3%

---

# AEM에서 Sling Resource Merger 사용{#using-the-sling-resource-merger-in-aem}

## 용도 {#purpose}

Sling Resource Merger는 리소스에 액세스하고 병합하는 서비스를 제공합니다. 이 플러그인은 두 가지 모두에 대한 차이(차이점) 메커니즘을 제공합니다.

* **[오버레이](/help/sites-developing/overlays.md)** 다음을 사용하여 리소스 [구성된 검색 경로](/help/sites-developing/overlays.md#configuring-the-search-paths).

* **무시** 터치 지원 UI에 대한 구성 요소 대화 상자(`cq:dialog`), 리소스 유형 계층 구조 사용(속성을 통해) `sling:resourceSuperType`).

Sling Resource Merger를 사용하면 오버레이/재정의 리소스 및/또는 속성이 원래 리소스/속성과 병합됩니다.

* 사용자 지정된 정의의 컨텐츠는 원래 컨텐츠(즉, *오버레이* 또는 *무시* 참조).

* 필요한 경우 [속성](#properties) 사용자 지정에 정의된 내용은 원본에서 병합된 콘텐츠를 사용하는 방법을 나타냅니다.

>[!CAUTION]
>
>Sling Resource Merger 및 관련 메서드는 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). 이것은 또한 터치 지원 표준 UI에만 적절하다는 것을 의미합니다. 특히 이 방식으로 정의된 재정의는 구성 요소의 터치 사용 대화 상자에만 적용할 수 있습니다.
>
>다른 영역(터치 지원 구성 요소 또는 클래식 UI의 다른 측면 포함)에 대한 오버레이/무시에는 적절한 노드 및 구조를 원본에서 사용자 지정을 정의할 위치로 복사하는 작업이 포함됩니다.

### AEM 목표 {#goals-for-aem}

AEM에서 Sling Resource Merger를 사용하는 목적은 다음과 같습니다.

* 사용자 지정 변경 사항이 작성되지 않았는지 확인합니다. `/libs`.
* 복제된 구조를 줄입니다. `/libs`.

   Sling Resource Merger를 사용하는 경우에는 전체 구조를 `/libs` 따라서 사용자 지정(일반적으로 `/apps`). 정보를 복제하면 시스템을 어떤 식으로든 업그레이드할 때 문제가 발생할 가능성이 불필요하게 높아집니다.

>[!NOTE]
>
>무시는 검색 경로에 종속되지 않으며 속성을 사용합니다 `sling:resourceSuperType` 를 클릭하여 연결을 만듭니다.
>
>그러나 무시는 종종 `/apps`를 설정하는 것이 좋습니다. `/apps`; 이 문제는 아래의 내용을 변경하지 않아야 하기 때문입니다 `/libs`.

>[!CAUTION]
>
>사용자 ***반드시*** 에서 아무것도 변경하지 않음 `/libs` 경로.
>
>왜냐하면 `/libs` 는 다음에 인스턴스를 업그레이드할 때 덮어쓰여지며, 핫픽스 또는 기능 팩을 적용할 때 덮어쓸 수 있습니다.
>
>구성 및 기타 변경에 대해 권장되는 방법은 다음과 같습니다.
>
>1. 필요한 항목(즉, 가 존재함에 따라)을 다시 만듭니다 `/libs`) 아래의 `/apps`
>
>1. 내에서 변경 `/apps`

>


### 속성 {#properties}

자원 합병은 다음 속성을 제공합니다.

* `sling:hideProperties` ( `String` 또는 `String[]`)

   숨길 속성 또는 속성 목록을 지정합니다.

   와일드카드 `*` 은 모두 숨깁니다.

* `sling:hideResource` ( `Boolean`)

   하위 항목을 포함하여 리소스를 완전히 숨겨야 하는지 여부를 나타냅니다.

* `sling:hideChildren` ( `String` 또는 `String[]`)

   숨길 하위 노드 또는 하위 노드 목록을 포함합니다. 노드의 속성이 유지됩니다.

   와일드카드 `*` 은 모두 숨깁니다.

* `sling:orderBefore` ( `String`)

   현재 노드가 앞에 위치해야 하는 동위 노드의 이름을 포함합니다.

이러한 속성은 해당/원래 리소스/속성(원본 `/libs`)은 오버레이/재정의(종종 `/apps`).

### 구조 만들기 {#creating-the-structure}

오버레이 또는 무시를 만들려면 대상(일반적으로 해당 구조)에서 원래 노드를 다시 만들어야 합니다 `/apps`). 예:

* 오버레이

   * 레일에 표시된 대로 사이트 콘솔의 탐색 항목 정의는 다음과 같이 정의됩니다.

      `/libs/cq/core/content/nav/sites/jcr:title`

   * 이를 오버레이하려면 다음 노드를 만듭니다.

      `/apps/cq/core/content/nav/sites`

      그런 다음 속성을 업데이트합니다 `jcr:title` 필요한 경우.

* 오버라이드

   * 텍스트 콘솔에 대한 터치 지원 대화 상자의 정의는 다음과 같이 정의됩니다.

      `/libs/foundation/components/text/cq:dialog`

   * 이를 무시하려면 다음과 같은 노드를 만드십시오.

      `/apps/the-project/components/text/cq:dialog`

이러한 구조 중 하나를 만들려면 뼈대 구조를 다시 만들어야 합니다. 구조를 단순화하기 위해 모든 중간 노드들이 유형일 수 있다 `nt:unstructured` (원래 노드 유형을 반영하지 않아도 됩니다.) 예: `/libs`).

따라서 위의 오버레이 예에서 다음 노드가 필요합니다.

```shell
/apps
  /cq
    /core
      /content
        /nav
          /sites
```

>[!NOTE]
>
>Sling 리소스 합병(즉, 표준 터치 지원 UI를 처리할 때)을 사용할 때는 전체 구조를 `/libs` 따라서 너무 많은 정보가 `/apps`. 이렇게 하면 시스템을 어떤 식으로든 업그레이드할 때 문제가 발생할 수 있습니다.

### 사용 사례 {#use-cases}

이러한 기능은 표준 기능과 함께, 다음과 같은 작업을 수행할 수 있습니다.

* **속성 추가**

   속성이 `/libs` 정의이지만, 는 `/apps` 오버레이/재정의.

   1. 내에서 해당 노드 만들기 `/apps`
   1. 이 노드에서 새 속성을 만듭니다. &quot;

* **속성을 재정의합니다(자동 생성된 속성이 아님).**

   속성은 다음에서 정의됩니다. `/libs`그러나 에서는 새 값이 필요합니다. `/apps` 오버레이/재정의.

   1. 내에서 해당 노드 만들기 `/apps`
   1. 이 노드( / 아래)에 일치하는 속성을 만듭니다. `apps`)

      * 속성은 Sling Resource Resolver 구성을 기반으로 우선 순위가 지정됩니다.
      * 속성 유형을 변경할 수 있습니다.

         에 사용된 속성과 다른 속성 유형을 사용하는 경우 `/libs`를 지정하면 정의한 속성 유형이 사용됩니다.
   >[!NOTE]
   >
   >속성 유형을 변경할 수 있습니다.

* **자동 생성된 속성 재정의**

   기본적으로 자동 생성된 속성(예: `jcr:primaryType`)의 경우 현재 노드 유형이 `/libs` 은 존중 받습니다. 오버레이/무시를 적용하려면 `/apps`를 사용하여 속성을 명시적으로 숨기고 재정의합니다.

   1. 아래에 해당 노드를 만듭니다. `/apps` 원하는 대로 `jcr:primaryType`
   1. 속성 만들기 `sling:hideProperties` 해당 노드에서 자동 생성된 속성의 값으로 설정된 값이 있습니다. 예 `jcr:primaryType`

      에 정의된 이 속성 `/apps`이제 에 정의된 것보다 우선합니다. `/libs`

* **노드 및 그 하위 항목 재정의**

   노드 및 그 하위는 `/libs`그러나 에서는 새 구성이 필요합니다. `/apps` 오버레이/재정의.

   1. 다음 작업을 결합합니다.

      1. 노드의 하위 노드 숨기기(노드의 속성 유지)
      1. 속성/속성 재정의

* **속성 숨기기**

   속성은 다음에서 정의됩니다. `/libs`, 에는 필요하지 않습니다. `/apps` 오버레이/재정의.

   1. 내에서 해당 노드 만들기 `/apps`
   1. 속성 만들기 `sling:hideProperties` 유형 `String` 또는 `String[]`. 이 옵션을 사용하여 숨기거나 무시할 속성을 지정합니다. 와일드카드를 사용할 수도 있습니다. 예:

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **노드 및 해당 하위 숨기기**

   노드 및 그 하위는 `/libs`, 에는 필요하지 않습니다. `/apps` 오버레이/재정의.

   1. /apps 아래에 해당 노드를 만듭니다.
   1. 속성 만들기 `sling:hideResource`

      * 유형: `Boolean`
      * 정렬 단추: `true`

* **노드의 하위 노드를 숨깁니다(노드의 속성을 유지하는 동안).**

   노드, 속성 및 하위는 `/libs`. 노드 및 속성은 `/apps` 오버레이/재정의하지만 일부 또는 모든 하위 노드는 `/apps` 오버레이/재정의.

   1. 아래에 해당 노드를 만듭니다. `/apps`
   1. 속성 만들기 `sling:hideChildren`:

      * 유형: `String[]`
      * 값: 하위 노드 목록( `/libs`) 숨기기/무시

      와일드카드(&amp;A); 모든 하위 노드를 숨기거나 무시하는 데 사용할 수 있습니다.


* **노드 순서 변경**

   노드와 그 동위 멤버는 `/libs`. 노드가 `/apps` 오버레이/재정의. 여기서 새 위치는 의 해당 동기 노드를 기준으로 정의됩니다 `/libs`.

   * 를 사용하십시오 `sling:orderBefore` 속성:

      1. 아래에 해당 노드를 만듭니다. `/apps`
      1. 속성 만들기 `sling:orderBefore`:

         노드(과 같이)를 지정합니다 `/libs`) 현재 노드를 앞에 배치해야 합니다.

         * 유형: `String`
         * 정렬 단추: `<before-SiblingName>`

### 코드에서 Sling 리소스 합병을 호출하는 중 {#invoking-the-sling-resource-merger-from-your-code}

Sling 리소스 합병에는 두 개의 사용자 지정 리소스 공급자(하나는 오버레이이고 다른 하나는 오버레이입니다. 마운트 지점을 사용하여 코드 내에서 이러한 각 호출을 호출할 수 있습니다.

>[!NOTE]
>
>리소스에 액세스할 때는 적절한 마운트 지점을 사용하는 것이 좋습니다.
>
>이렇게 하면 Sling Resource Merger가 호출되고 완전히 병합된 리소스가 반환됩니다(복제해야 하는 구조를 줄임). `/libs`).

* 오버레이:

   * 목적: 검색 경로에 따라 리소스 병합
   * 마운트 지점: `/mnt/overlay`
   * 사용: `mount point + relative path`
   * 예:

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* 오버라이드:

   * 목적: 슈퍼 유형에 따라 리소스 병합
   * 마운트 지점: `/mnt/overide`
   * 사용: `mount point + absolute path`
   * 예:

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### 사용 예 {#example-of-usage}

몇 가지 예는 다음과 같습니다.

* 오버레이:

   * [콘솔 사용자 지정](/help/sites-developing/customizing-consoles-touch.md)
   * [페이지 작성 사용자 지정](/help/sites-developing/customizing-page-authoring-touch.md)

* 오버라이드:

   * [페이지 속성 구성](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)
