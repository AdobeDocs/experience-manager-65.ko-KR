---
title: AEM에서 Sling Resource Merger 사용
seo-title: AEM에서 Sling Resource Merger 사용
description: Sling Resource Merger는 리소스에 액세스하고 병합하는 서비스를 제공합니다
seo-description: Sling Resource Merger는 리소스에 액세스하고 병합하는 서비스를 제공합니다
uuid: 0a28fdc9-caea-490b-8f07-7c4a6b802e09
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ec712ba0-0fd6-4bb8-93d6-07d09127df58
exl-id: 1eed754e-9a7d-4b65-a929-757fc962614d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 3%

---

# AEM에서 Sling Resource Merger 사용{#using-the-sling-resource-merger-in-aem}

## 목적 {#purpose}

Sling Resource Merger는 리소스에 액세스하고 병합하는 서비스를 제공합니다. 이 플러그인은 두 가지 모두에 대한 차이(차이점) 메커니즘을 제공합니다.

* **[](/help/sites-developing/overlays.md)** 구성된 검색 경로를  [사용한 리소스 오버레이](/help/sites-developing/overlays.md#configuring-the-search-paths).

* **** 리소스 유형 계층 구조(속성을 통해)를 사용하여 터치 지원 UI(`cq:dialog`)에 대한 구성 요소 대화 상자의  `sling:resourceSuperType`개요입니다.

Sling Resource Merger를 사용하면 오버레이/재정의 리소스 및/또는 속성이 원래 리소스/속성과 병합됩니다.

* 사용자 지정된 정의의 컨텐츠는 원본보다 우선 순위가 높습니다(즉, *오버레이*&#x200B;또는&#x200B;*overrides*).

* 필요한 경우 사용자 지정에 정의된 [속성](#properties)은 원본에서 병합된 컨텐츠를 사용하는 방법을 나타냅니다.

>[!CAUTION]
>
>Sling 리소스 합병 및 관련 메서드는 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)에서만 사용할 수 있습니다. 이것은 또한 표준 터치 지원 UI에만 적절하다는 것을 의미합니다.특히 이 방식으로 정의된 재정의는 구성 요소의 터치 사용 대화 상자에만 적용할 수 있습니다.
>
>다른 영역(터치 지원 구성 요소 또는 클래식 UI의 다른 측면 포함)에 대한 오버레이/무시에는 적절한 노드 및 구조를 원본에서 사용자 지정을 정의할 위치로 복사하는 작업이 포함됩니다.

### AEM {#goals-for-aem} 목표

AEM에서 Sling Resource Merger를 사용하는 목적은 다음과 같습니다.

* `/libs`에서 사용자 지정 변경이 수행되지 않도록 하십시오.
* `/libs`에서 복제되는 구조를 줄입니다.

   Sling Resource Merger를 사용하는 경우 `/libs`에서 전체 구조를 복사하지 않는 것이 좋습니다. 이렇게 하면 사용자 지정(일반적으로 `/apps`)에서 너무 많은 정보가 유지됩니다. 정보를 복제하면 시스템을 어떤 식으로든 업그레이드할 때 문제가 발생할 가능성이 불필요하게 높아집니다.

>[!NOTE]
>
>무시는 검색 경로에 종속되지 않으며 `sling:resourceSuperType` 속성을 사용하여 연결을 만듭니다.
>
>그러나 AEM에서 가장 좋은 방법은 `/apps`;`/libs` 아래에서 아무 것도 변경하지 않아야 하기 때문입니다.`/apps`

>[!CAUTION]
>
>***은 `/libs` 경로에서 아무 것도 변경하지 않아야 합니다.***
>
>이는 다음 번에 인스턴스를 업그레이드할 때 `/libs` 컨텐츠를 덮어쓰게 되기 때문입니다(핫픽스 또는 기능 팩을 적용할 때 덮어쓸 수 있음).
>
>구성 및 기타 변경에 대해 권장되는 방법은 다음과 같습니다.
>
>1. `/apps` 아래에 필요한 항목(즉, `/libs`에 있는 항목)을 다시 만듭니다.
   >
   >
1. `/apps` 내에서 변경

>



### 속성 {#properties}

자원 합병은 다음 속성을 제공합니다.

* `sling:hideProperties` (  `String` 또는  `String[]`)

   숨길 속성 또는 속성 목록을 지정합니다.

   와일드카드 `*`은(는) 모두 숨깁니다.

* `sling:hideResource` ( `Boolean`)

   하위 항목을 포함하여 리소스를 완전히 숨겨야 하는지 여부를 나타냅니다.

* `sling:hideChildren` (  `String` 또는  `String[]`)

   숨길 하위 노드 또는 하위 노드 목록을 포함합니다. 노드의 속성이 유지됩니다.

   와일드카드 `*`은(는) 모두 숨깁니다.

* `sling:orderBefore` (  `String`)

   현재 노드가 앞에 위치해야 하는 동위 노드의 이름을 포함합니다.

이러한 속성은 오버레이/재정의(종종 `/apps`에 있음)에서 해당/원래 리소스/속성(`/libs`에 있음)을 사용하는 방식에 영향을 줍니다.

### 구조 만들기 {#creating-the-structure}

오버레이 또는 무시를 만들려면 대상(일반적으로 `/apps`) 아래에 동일한 구조를 사용하여 원래 노드를 다시 만들어야 합니다. 예:

* 오버레이

   * 레일에 표시된 대로 사이트 콘솔의 탐색 항목 정의는 다음과 같이 정의됩니다.

      `/libs/cq/core/content/nav/sites/jcr:title`

   * 이를 오버레이하려면 다음 노드를 만듭니다.

      `/apps/cq/core/content/nav/sites`

      그런 다음 필요에 따라 `jcr:title` 속성을 업데이트합니다.

* 오버라이드

   * 텍스트 콘솔에 대한 터치 지원 대화 상자의 정의는 다음과 같이 정의됩니다.

      `/libs/foundation/components/text/cq:dialog`

   * 이를 무시하려면 다음과 같은 노드를 만드십시오.

      `/apps/the-project/components/text/cq:dialog`

이러한 구조 중 하나를 만들려면 뼈대 구조를 다시 만들어야 합니다. 구조를 재조정하기 위해 모든 중간 노드는 `nt:unstructured` 유형일 수 있습니다(원본 노드 유형을 반영하지 않아도 됩니다.).예: `/libs`).

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
>Sling 리소스 합병(즉, 표준 터치 지원 UI를 처리할 때)을 사용할 때는 `/libs`에서 전체 구조를 복사하지 않는 것이 좋습니다. 이렇게 하면 `/apps`에 너무 많은 정보가 유지됩니다. 이렇게 하면 시스템을 어떤 식으로든 업그레이드할 때 문제가 발생할 수 있습니다.

### 사용 사례 {#use-cases}

이러한 기능은 표준 기능과 함께, 다음과 같은 작업을 수행할 수 있습니다.

* **속성 추가**

   속성은 `/libs` 정의에 존재하지 않지만 `/apps` 오버레이/재정의에서 필요합니다.

   1. `/apps` 내에 해당 노드를 만듭니다.
   1. 이 노드에서 새 속성을 만듭니다. &quot;

* **속성을 재정의합니다(자동 생성된 속성이 아님).**

   속성은 `/libs`에 정의되어 있지만, `/apps` 오버레이/무시에는 새 값이 필요합니다.

   1. `/apps` 내에 해당 노드를 만듭니다.
   1. 이 노드( / `apps` 아래)에 일치하는 속성을 만듭니다

      * 속성은 Sling Resource Resolver 구성을 기반으로 우선 순위가 지정됩니다.
      * 속성 유형을 변경할 수 있습니다.

         `/libs`에 사용된 속성 유형과 다른 속성 유형을 사용하는 경우 정의한 속성 유형이 사용됩니다.
   >[!NOTE]
   >
   >속성 유형을 변경할 수 있습니다.

* **자동 생성된 속성 재정의**

   기본적으로 자동 생성된 속성(예: `jcr:primaryType`)은 현재 `/libs` 아래의 노드 유형이 준수되도록 하기 위해 오버레이/무시를 적용하지 않습니다. 오버레이/무시를 적용하려면 `/apps`에서 노드를 다시 만들어야 합니다. 속성을 명시적으로 숨기고 재정의해야 합니다.

   1. `/apps` 아래에 원하는 `jcr:primaryType` 로 해당 노드를 만듭니다.
   1. 값이 자동 생성된 속성의 값으로 설정된 상태에서 해당 노드에 속성 `sling:hideProperties`을 만듭니다.예: `jcr:primaryType`

      이제 `/apps`에 정의된 이 속성은 `/libs`에 정의된 속성보다 우선 순위가 높습니다

* **노드 및 그 하위 항목 재정의**

   노드와 그 자식은 `/libs`에 정의되어 있지만, `/apps` 오버레이/무시에는 새 구성이 필요합니다.

   1. 다음 작업을 결합합니다.

      1. 노드의 하위 노드 숨기기(노드의 속성 유지)
      1. 속성/속성 재정의

* **속성 숨기기**

   속성은 `/libs`에 정의되어 있지만 `/apps` 오버레이/무시에는 필요하지 않습니다.

   1. `/apps` 내에 해당 노드를 만듭니다.
   1. `String` 또는 `String[]` 유형의 `sling:hideProperties` 속성을 만듭니다. 이 옵션을 사용하여 숨기거나 무시할 속성을 지정합니다. 와일드카드를 사용할 수도 있습니다. 예:

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **노드 및 해당 하위 숨기기**

   노드와 그 자식은 `/libs`에 정의되어 있지만 `/apps` 오버레이/재정의에는 필요하지 않습니다.

   1. /apps 아래에 해당 노드를 만듭니다.
   1. 속성 `sling:hideResource` 만들기

      * 유형: `Boolean`
      * 정렬 단추: `true`

* **노드의 하위 노드를 숨깁니다(노드의 속성을 유지하는 동안).**

   노드, 속성 및 하위 노드는 `/libs`에 정의됩니다. 노드 및 해당 속성은 `/apps` 오버레이/재정의에 필요하지만 일부 또는 모든 하위 노드는 `/apps` 오버레이/재정의할 필요가 없습니다.

   1. `/apps` 아래에 해당 노드를 만듭니다.
   1. `sling:hideChildren` 속성을 만듭니다.

      * 유형: `String[]`
      * 값:`/libs`에 정의된 하위 노드 목록

      와일드카드 &amp;ast;모든 하위 노드를 숨기거나 무시하는 데 사용할 수 있습니다.


* **노드 순서 변경**

   노드와 그 형제자매는 `/libs`에 정의됩니다. 노드가 `/apps` 오버레이/무시로 다시 작성되도록 새 위치가 필요합니다. 여기서 새 위치는 `/libs`의 해당 동기 노드를 기준으로 정의됩니다.

   * `sling:orderBefore` 속성을 사용합니다.

      1. `/apps` 아래에 해당 노드를 만듭니다.
      1. `sling:orderBefore` 속성을 만듭니다.

         이 옵션은 현재 노드가 앞에 위치해야 하는 노드(`/libs`에 있음)를 지정합니다.

         * 유형: `String`
         * 정렬 단추: `<before-SiblingName>`

### 코드 {#invoking-the-sling-resource-merger-from-your-code}에서 Sling 리소스 합병을 호출하는 중

Sling 리소스 합병에는 두 개의 사용자 지정 리소스 공급자(하나는 오버레이이고 다른 하나는 오버레이입니다. 마운트 지점을 사용하여 코드 내에서 이러한 각 호출을 호출할 수 있습니다.

>[!NOTE]
>
>리소스에 액세스할 때는 적절한 마운트 지점을 사용하는 것이 좋습니다.
>
>이렇게 하면 Sling Resource Merger가 호출되고 완전히 병합된 리소스가 반환됩니다( `/libs`에서 복제해야 하는 구조가 감소함).

* 오버레이:

   * 목적:검색 경로에 따라 리소스 병합
   * 마운트 지점:`/mnt/overlay`
   * 사용:`mount point + relative path`
   * 예:

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* 오버라이드:

   * 목적:슈퍼 유형에 따라 리소스 병합
   * 마운트 지점:`/mnt/overide`
   * 사용:`mount point + absolute path`
   * 예:

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### 사용 {#example-of-usage} 예

몇 가지 예는 다음과 같습니다.

* 오버레이:

   * [콘솔 사용자 지정](/help/sites-developing/customizing-consoles-touch.md)
   * [페이지 작성 사용자 지정](/help/sites-developing/customizing-page-authoring-touch.md)

* 오버라이드:

   * [페이지 속성 구성](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)
