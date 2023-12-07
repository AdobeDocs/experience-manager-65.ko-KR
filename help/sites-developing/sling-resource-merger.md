---
title: AEM에서 Sling 리소스 병합 사용
description: Sling 리소스 병합은 리소스에 액세스하고 리소스를 병합하는 서비스를 제공합니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 1eed754e-9a7d-4b65-a929-757fc962614d
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1247'
ht-degree: 1%

---

# AEM에서 Sling 리소스 병합 사용{#using-the-sling-resource-merger-in-aem}

## 용도 {#purpose}

Sling 리소스 병합은 리소스에 액세스하고 리소스를 병합하는 서비스를 제공합니다. 두 가지 모두에 대해 비교(차이점 보관) 메커니즘을 제공합니다.

* **[오버레이](/help/sites-developing/overlays.md)** 을(를) 사용하는 리소스의 [구성된 검색 경로](/help/sites-developing/overlays.md#configuring-the-search-paths).

* **재정의** 터치 사용 UI에 대한 구성 요소 대화 상자(`cq:dialog`), 리소스 유형 계층 사용(속성 사용) `sling:resourceSuperType`).

Sling 리소스 병합을 사용하면 오버레이/재정의 리소스 및/또는 속성이 원래 리소스/속성과 병합됩니다.

* 맞춤화된 정의의 내용은 원래 정의(즉, 정의)보다 우선순위가 높다 *오버레이* 또는 *재정의* it).

* 필요한 경우 [속성](#properties) 사용자 지정에 정의되어 있으며 원본에서 병합된 컨텐츠가 사용되는 방식을 나타냅니다.

>[!CAUTION]
>
>Sling 리소스 병합 및 관련 메서드는 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). 즉, 표준 터치 지원 UI에만 적절합니다. 특히 이 방식으로 정의된 무시는 구성 요소의 터치 지원 대화 상자에만 적용할 수 있습니다.
>
>다른 영역(터치 지원 구성 요소 또는 클래식 UI의 다른 측면 포함)에 대한 오버레이/무시는 원래 위치에서 맞춤화가 정의될 위치로 적절한 노드 및 구조를 복사하는 작업이 포함됩니다.

### AEM 목표 {#goals-for-aem}

AEM에서 Sling 리소스 병합을 사용하는 목표는 다음과 같습니다.

* 에서 사용자 정의 변경이 수행되지 않았는지 확인합니다. `/libs`.
* 복제되는 구조 감소 `/libs`.

  Sling 리소스 병합을 사용할 때에서 전체 구조를 복사하지 않는 것이 좋습니다. `/libs` 이로 인해 사용자 지정에 너무 많은 정보가 보관됩니다(일반적으로 `/apps`). 정보를 중복하면 어떤 식으로든 시스템을 업그레이드할 때 문제가 발생할 가능성이 불필요하게 증가합니다.

>[!NOTE]
>
>재정의는 검색 경로에 종속되지 않으며 속성을 사용합니다 `sling:resourceSuperType` 연결.
>
>그러나 재정의는 종종 아래에 정의됩니다. `/apps`를 설정하는 것이 AEM의 모범 사례입니다. `/apps`; 아래에 있는 것을 변경하지 말아야 하기 때문입니다. `/libs`.

>[!CAUTION]
>
>본인 ***필수*** 의 아무 것도 변경하지 마십시오. `/libs` 경로.
>
>이는 의 콘텐츠가 `/libs` 는 다음에 인스턴스를 업그레이드할 때 덮어쓰기됩니다(또한 핫픽스 또는 기능 팩을 적용할 때 덮어쓰기될 수도 있음).
>
>구성 및 기타 변경에 권장되는 방법은 다음과 같습니다.
>
>1. 필요한 항목 다시 만들기(존재하는 그대로) `/libs`) `/apps`
>
>1. 다음 범위 내에서 변경 `/apps`
>

### 속성 {#properties}

리소스 병합은 다음 속성을 제공합니다.

* `sling:hideProperties` ( `String` 또는 `String[]`)

  숨길 속성 또는 속성 목록을 지정합니다.

  와일드카드 `*` 모두 숨깁니다.

* `sling:hideResource` ( `Boolean`)

  하위 리소스를 포함하여 리소스를 완전히 숨길지 여부를 나타냅니다.

* `sling:hideChildren` ( `String` 또는 `String[]`)

  숨길 하위 노드 또는 하위 노드 목록을 포함합니다. 노드의 속성은 유지됩니다.

  와일드카드 `*` 모두 숨깁니다.

* `sling:orderBefore` ( `String`)

  현재 노드가 앞에 배치해야 하는 형제 노드의 이름을 포함합니다.

이러한 속성은 해당/원래 리소스/속성(에서)의 방식에 영향을 줍니다. `/libs`)는 오버레이/재정의에서 사용됩니다(종종 `/apps`).

### 구조 만들기 {#creating-the-structure}

오버레이를 생성하거나 무시하려면 대상(일반적으로) 아래에 동일한 구조로 원본 노드를 다시 생성해야 합니다 `/apps`). 예:

* 오버레이

   * 레일에 표시된 Sites 콘솔의 탐색 항목 정의는 다음과 같이 정의됩니다.

     `/libs/cq/core/content/nav/sites/jcr:title`

   * 이를 오버레이하려면 다음 노드를 만듭니다.

     `/apps/cq/core/content/nav/sites`

     그런 다음 속성을 업데이트합니다. `jcr:title` 필요에 따라.

* 오버라이드

   * 텍스트 콘솔에 대한 터치 사용 대화 상자의 정의는 다음에서 정의됩니다.

     `/libs/foundation/components/text/cq:dialog`

   * 재정의하려면 다음 노드(예: )를 만듭니다.

     `/apps/the-project/components/text/cq:dialog`

이 중 하나를 생성하려면 뼈대 구조를 재생성하기만 하면 됩니다. 구조의 재생성을 단순화하기 위해 모든 중간 노드가 유형일 수 있습니다 `nt:unstructured` (원래 노드 유형을 반영하지 않아도 됩니다(예: `/libs`).

따라서 위의 오버레이 예에는 다음 노드가 필요합니다.

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
>Sling 리소스 병합을 사용할 때(즉, 표준 터치 지원 UI를 처리할 때) 전체 구조를에서 복사하지 않는 것이 좋습니다. `/libs` 그 결과 너무 많은 정보가 `/apps`. 이렇게 하면 어떤 방식으로든 시스템을 업그레이드할 때 문제가 발생할 수 있습니다.

### 사용 사례 {#use-cases}

이러한 기능과 표준 기능을 함께 사용하면 다음 작업을 수행할 수 있습니다.

* **속성 추가**

  속성이에 없음 `/libs` 정의하지만 에는 필수입니다. `/apps` 오버레이/무시.

   1. 내에서 해당 노드 만들기 `/apps`
   1. 이 노드에 새 속성을 만듭니다.&quot;

* **속성 재정의(자동 생성 속성이 아님)**

  속성은에 정의되어 있습니다. `/libs`, 그러나 에는 새 값이 필요합니다. `/apps` 오버레이/무시.

   1. 내에서 해당 노드 만들기 `/apps`
   1. 이 노드( / 아래)에서 일치하는 속성을 만듭니다. `apps`)

      * 속성은 Sling Resource Resolver 구성에 따라 우선 순위를 갖습니다.
      * 속성 유형 변경은 지원됩니다.

        에 사용된 것과 다른 속성 유형을 사용하는 경우 `/libs`를 입력하면 정의한 속성 유형이 사용됩니다.

  >[!NOTE]
  >
  >속성 유형 변경은 지원됩니다.

* **자동 생성 속성 재정의**

  기본적으로 자동 생성된 속성(예: `jcr:primaryType`)는 현재 아래에 노드 유형이 있는지 확인하기 위한 오버레이/재정의의 대상이 아닙니다. `/libs` 존중됩니다. 오버레이/무시를 적용하려면 `/apps`속성을 명시적으로 숨기고 재정의합니다.

   1. 아래에 해당 노드 만들기 `/apps` 필요한 경우 `jcr:primaryType`
   1. 속성 만들기 `sling:hideProperties` 해당 노드에서 값이 자동 생성된 속성의 값으로 설정됩니다. 예: `jcr:primaryType`

      이 속성, 아래에 정의됨 `/apps`이제 이(가) 아래에 정의된 것보다 우선합니다. `/libs`

* **노드 및 그 자식 재정의**

  노드 및 그 하위 항목이에 정의되어 있습니다. `/libs`, 하지만 새 구성은 `/apps` 오버레이/무시.

   1. 다음 작업을 결합합니다.

      1. 노드의 하위 항목 숨기기(노드의 속성 유지)
      1. 속성/속성 재정의

* **속성 숨기기**

  속성은에 정의되어 있습니다. `/libs`, 그러나 에는 필요하지 않습니다. `/apps` 오버레이/무시.

   1. 내에서 해당 노드 만들기 `/apps`
   1. 속성 만들기 `sling:hideProperties` 유형 `String` 또는 `String[]`. 이 옵션을 사용하여 숨기거나 무시할 속성을 지정합니다. 와일드카드를 사용할 수도 있습니다. 예:

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **노드 및 하위 항목 숨기기**

  노드 및 그 하위 항목이에 정의되어 있습니다. `/libs`, 그러나 에는 필요하지 않습니다. `/apps` 오버레이/무시.

   1. /apps 아래에 해당 노드 만들기
   1. 속성 만들기 `sling:hideResource`

      * 유형: `Boolean`
      * 값: `true`

* **노드의 속성을 유지하면서 노드의 하위 항목 숨기기**

  노드, 해당 속성 및 하위 항목이에 정의되어 있습니다 `/libs`. 노드 및 해당 속성은 `/apps` 오버레이/재정의하지만 일부 또는 모든 하위 노드가 `/apps` 오버레이/무시.

   1. 아래에 해당 노드 만들기 `/apps`
   1. 속성 만들기 `sling:hideChildren`:

      * 유형: `String[]`
      * 값: 하위 노드 목록(에 정의됨) `/libs`)을 사용하여 숨기거나 무시할 수 있습니다.

      와일드카드 &amp;ast;를 사용하여 모든 하위 노드를 숨기고 무시할 수 있습니다.

* **노드 순서 바꾸기**

  노드 및 해당 형제 노드는에서 정의됩니다 `/libs`. 새 위치가 필요하므로 노드가 `/apps` 오버레이/재정의 - 새 위치가 의 해당 형제 노드를 참조하여 정의됨 `/libs`.

   * 사용 `sling:orderBefore` 속성:

      1. 아래에 해당 노드 만들기 `/apps`
      1. 속성 만들기 `sling:orderBefore`:

         다음과 같이 노드를 지정합니다. `/libs`) 현재 노드가 다음 앞에 위치해야 합니다.

         * 유형: `String`
         * 값: `<before-SiblingName>`

### 코드에서 Sling 리소스 병합 호출 {#invoking-the-sling-resource-merger-from-your-code}

Sling 리소스 병합에는 두 개의 사용자 지정 리소스 공급자가 포함되어 있습니다. 하나는 오버레이에 사용되고 다른 하나는 재정의에 사용됩니다. 이러한 각 호출은 마운트 지점을 사용하여 코드 내에서 호출할 수 있습니다.

>[!NOTE]
>
>리소스에 액세스할 때는 적절한 마운트 지점을 사용하는 것이 좋습니다.
>
>이렇게 하면 Sling 리소스 병합이 호출되고 완전히 병합된 리소스가 반환되어 복제해야 하는 구조가 줄어듭니다. `/libs`).

* 오버레이:

   * 목적: 검색 경로를 기반으로 리소스 병합
   * 마운트 지점: `/mnt/overlay`
   * 사용: `mount point + relative path`
   * 예:

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* 재정의:

   * 목적: super type을 기반으로 리소스 병합
   * 마운트 지점: `/mnt/overide`
   * 사용: `mount point + absolute path`
   * 예:

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### 사용 예 {#example-of-usage}

몇 가지 예제를 다룹니다.

* 오버레이:

   * [콘솔 사용자 지정](/help/sites-developing/customizing-consoles-touch.md)
   * [페이지 작성 사용자 정의](/help/sites-developing/customizing-page-authoring-touch.md)

* 재정의:

   * [페이지 속성 구성](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)
