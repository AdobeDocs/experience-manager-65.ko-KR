---
title: AEM에서 Sling Resource Merger 사용
seo-title: AEM에서 Sling Resource Merger 사용
description: Sling Resource Combination은 리소스에 액세스하고 병합하는 서비스를 제공합니다.
seo-description: Sling Resource Combination은 리소스에 액세스하고 병합하는 서비스를 제공합니다.
uuid: 0a28fdc9-caea-490b-8f07-7c4a6b802e09
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ec712ba0-0fd6-4bb8-93d6-07d09127df58
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 3%

---


# AEM에서 Sling Resource Merger 사용{#using-the-sling-resource-merger-in-aem}

## 목적 {#purpose}

Sling Resource Combination은 리소스에 액세스하고 병합하는 서비스를 제공합니다. 두 가지 모두에 대해 차이점(차이) 메커니즘을 제공합니다.

* **[구성된](/help/sites-developing/overlays.md)** 검색 경로를 사용하여  [리소스 오버레이입니다](/help/sites-developing/overlays.md#configuring-the-search-paths).

* **터치** 지원 UI(`cq:dialog`)에 대한 구성 요소 대화 상자의 개요(속성 `sling:resourceSuperType`을 통해) 리소스 유형 계층 구조를 사용합니다.

Sling 리소스 합병에서 오버레이/재정의 리소스 및/또는 속성은 원래 리소스/속성과 병합됩니다.

* 사용자 지정된 정의의 내용이 원본보다 우선 순위가 높습니다(즉, *오버레이* 또는&#x200B;*오버레이가* 오버라이드).

* 필요한 경우 사용자 정의에 정의된 [속성](#properties)은 원본에서 병합된 콘텐트를 사용하는 방법을 나타냅니다.

>[!CAUTION]
>
>Sling 리소스 합병 및 관련 메서드는 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)에서만 사용할 수 있습니다. 이는 표준 터치 지원 UI에만 해당됨을 의미합니다.이 방식으로 정의된 특정 오버라이드는 구성 요소의 터치 활성화 대화 상자에만 적용할 수 있습니다.
>
>다른 영역(터치 지원 구성 요소 또는 클래식 UI의 다른 측면 포함)에 대한 오버레이/오버라이드는 적절한 노드 및 구조를 원본에서 사용자 정의 정의 정의 정의 위치로 복사하는 것을 포함합니다.

### AEM 목표 {#goals-for-aem}

AEM에서 Sling 리소스 합병을 사용하는 목표는 다음과 같습니다.

* 사용자 지정 변경 내용이 `/libs`에서 수행되지 않는지 확인합니다.
* `/libs`에서 복제된 구조를 줄입니다.

   Sling 리소스 합병을 사용할 때는 `/libs`에서 전체 구조를 복사하는 것이 좋습니다. 이렇게 하면 사용자 지정(일반적으로 `/apps`)에 너무 많은 정보가 저장될 수 있습니다. 정보를 중복하면 시스템을 어떤 식으로든 업그레이드할 때 문제 발생 가능성이 불필요하게 높아집니다.

>[!NOTE]
>
>오버라이드는 검색 경로에 종속되지 않으며 `sling:resourceSuperType` 속성을 사용하여 연결을 만듭니다.
>
>그러나 AEM의 우수 사례는 `/apps`;에서 사용자 지정을 정의하는 것이므로, 대체는 종종 `/apps` 아래에 정의됩니다.이것은 `/libs` 아래의 항목을 변경할 수 없기 때문입니다.

>[!CAUTION]
>
>***은(는) `/libs` 경로에서 아무 것도 변경하지 않아야 합니다.***
>
>이는 다음 번에 인스턴스를 업그레이드할 때 `/libs`의 콘텐트가 덮어쓰기되기 때문입니다(핫픽스 또는 기능 팩을 적용할 때 덮어쓰여질 수 있음).
>
>구성 및 기타 변경 사항에 대한 권장 방법은 다음과 같습니다.
>
>1. `/apps` 아래의 필수 항목(즉, `/libs`에 존재하는 항목)을 다시 만듭니다.
   >
   >
1. `/apps` 내에서 변경

>



### 속성 {#properties}

리소스 병합은 다음 속성을 제공합니다.

* `sling:hideProperties` (  `String` 또는  `String[]`)

   숨길 속성 또는 속성 목록을 지정합니다.

   와일드카드 `*`은 모두 숨깁니다.

* `sling:hideResource` ( `Boolean`)

   하위 항목을 포함하여 리소스를 완전히 숨길지 여부를 나타냅니다.

* `sling:hideChildren` (  `String` 또는  `String[]`)

   숨길 하위 노드 또는 하위 노드 목록을 포함합니다. 노드의 속성이 유지됩니다.

   와일드카드 `*`은 모두 숨깁니다.

* `sling:orderBefore` ( `String`)

   현재 노드를 앞에 배치할 형제 노드의 이름을 포함합니다.

이러한 속성은 오버레이/override(종종 `/apps`에 있음)에 해당/원래 리소스/속성(`/libs`에서)이 사용되는 방식에 영향을 줍니다.

### {#creating-the-structure} 구조 만들기

오버레이 또는 오버라이드를 만들려면 대상(일반적으로 `/apps`) 아래에 동일한 구조로 원래 노드를 다시 만들어야 합니다. 예:

* 오버레이

   * 레일에 표시되는 사이트 콘솔에 대한 탐색 항목의 정의는 다음과 같습니다.

      `/libs/cq/core/content/nav/sites/jcr:title`

   * 이를 오버레이하려면 다음 노드를 만드십시오.

      `/apps/cq/core/content/nav/sites`

      그런 다음 필요에 따라 `jcr:title` 속성을 업데이트합니다.

* 재정의

   * 텍스트 콘솔에 대한 터치 지원 대화 상자의 정의는 다음과 같이 정의됩니다.

      `/libs/foundation/components/text/cq:dialog`

   * 이 노드를 재정의하려면 다음과 같은 노드를 만드십시오.

      `/apps/the-project/components/text/cq:dialog`

이러한 구조 중 하나를 만들려면 뼈대 구조를 다시 만들어야 합니다. 구조를 간소화하기 위해 모든 중간 노드는 `nt:unstructured` 유형일 수 있습니다(원래 노드 유형을 반영하지 않아도 됩니다.예: `/libs`).

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
>Sling 리소스 합병을 사용하는 경우(즉, 표준 터치 지원 UI를 처리할 때) `/libs`에서 전체 구조를 복사하는 것은 권장되지 않습니다. 이로 인해 `/apps`에 너무 많은 정보가 저장될 수 있습니다. 이렇게 하면 시스템을 업그레이드할 때 문제가 발생할 수 있습니다.

### 사용 사례 {#use-cases}

표준 기능과 함께 다음과 같은 작업을 수행할 수 있습니다.

* **속성 추가**

   속성이 `/libs` 정의에 없지만 `/apps` 오버레이/override에 필요합니다.

   1. `/apps` 내에 해당 노드를 만듭니다.
   1. 이 노드 &quot;

* **속성 재정의(자동으로 생성된 속성이 아님)**

   속성은 `/libs`에 정의되어 있지만 `/apps` 오버레이/override에 새 값이 필요합니다.

   1. `/apps` 내에 해당 노드를 만듭니다.
   1. 이 노드에서 일치하는 속성을 만듭니다(/ `apps` 아래).

      * 속성은 Sling 리소스 확인자 구성을 기반으로 우선 순위가 지정됩니다.
      * 속성 유형 변경이 지원됩니다.

         `/libs`에 사용된 것과 다른 속성 유형을 사용하는 경우 정의한 속성 유형이 사용됩니다.
   >[!NOTE]
   >
   >속성 유형 변경이 지원됩니다.

* **자동 생성 속성 재정의**

   기본적으로 자동 생성된 속성(예: `jcr:primaryType`)은 현재 `/libs` 아래에 있는 노드 유형이 존중되도록 오버레이/override의 적용을 받지 않습니다. 오버레이/재정의를 적용하려면 `/apps`에서 노드를 다시 만들어야 하며, 속성을 명시적으로 숨기고 재정의해야 합니다.

   1. 원하는 `jcr:primaryType`과 함께 `/apps` 아래에 해당 노드를 만듭니다.
   1. 자동으로 생성된 속성의 값으로 설정된 값을 사용하여 해당 노드에 속성 `sling:hideProperties`을 만듭니다.예를 들어 `jcr:primaryType`

      이제 `/apps`에 정의된 이 속성은 `/libs` 아래에 정의된 속성보다 우선합니다.

* **노드 및 그 하위 재정의**

   노드 및 그 자식은 `/libs`에 정의되어 있지만 `/apps` 오버레이/재정의에는 새 구성이 필요합니다.

   1. 다음 작업 결합:

      1. 노드의 하위 항목 숨기기(노드의 속성 유지)
      1. 속성/속성 재정의

* **속성 숨기기**

   속성은 `/libs`에 정의되어 있지만 `/apps` 오버레이/override에는 필요하지 않습니다.

   1. `/apps` 내에 해당 노드를 만듭니다.
   1. `String` 또는 `String[]` 유형의 `sling:hideProperties` 속성을 만듭니다. 숨거나 무시할 속성을 지정합니다. 와일드카드를 사용할 수도 있습니다. 예:

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **노드 및 그 하위 숨기기**

   노드 및 그 자식은 `/libs`에 정의되어 있지만 `/apps` 오버레이/override에는 필요하지 않습니다.

   1. /apps 아래에 해당 노드 만들기
   1. 속성 `sling:hideResource` 만들기

      * 유형: `Boolean`
      * 정렬 단추: `true`

* **노드의 하위 항목 숨기기(노드의 속성을 유지하는 동안)**

   노드, 해당 속성 및 하위 항목은 `/libs`에 정의됩니다. 노드 및 해당 속성은 `/apps` overlay/override에 필요하지만 일부 또는 모든 하위 노드가 `/apps` overlay/override에 필요하지 않습니다.

   1. `/apps` 아래에 해당 노드를 만듭니다.
   1. 속성 `sling:hideChildren`을(를) 만듭니다.

      * 유형: `String[]`
      * 값:`/libs`에 정의된 자식 노드 목록(&lt;a0/>에 정의) 숨기기/무시

      와일드카드 정선(&amp;M);ast;모든 하위 노드를 숨기거나 무시하는 데 사용할 수 있습니다.


* **노드 순서 변경**

   노드 및 그 형제자매는 `/libs`에 정의됩니다. 노드를 `/apps` overlay/override에 다시 만들어야 합니다. 여기서 새 위치는 `/libs`의 해당 동기 노드에 대한 참조에 정의됩니다.

   * `sling:orderBefore` 속성을 사용합니다.

      1. `/apps` 아래에 해당 노드를 만듭니다.
      1. 속성 `sling:orderBefore`을(를) 만듭니다.

         이 값은 현재 노드를 앞에 배치할 노드(예: `/libs`)를 지정합니다.

         * 유형: `String`
         * 정렬 단추: `<before-SiblingName>`

### 코드 {#invoking-the-sling-resource-merger-from-your-code}에서 Sling 리소스 합병 호출

Sling 리소스 합병에는 2개의 사용자 지정 리소스 공급자(오버레이용 공급자 및 오버라이드에 대한 사용자 지정 리소스 공급자)가 포함됩니다. 마운트 지점을 사용하여 코드 내에서 각 코드를 호출할 수 있습니다.

>[!NOTE]
>
>리소스에 액세스할 때는 적절한 마운트 지점을 사용하는 것이 좋습니다.
>
>이렇게 하면 Sling 리소스 합병이 호출되고 완전히 병합된 리소스가 반환됩니다(이 경우 `/libs`에서 복제해야 하는 구조가 감소됨).

* 오버레이:

   * 목적:검색 경로에 따라 리소스 병합
   * 마운트 지점:`/mnt/overlay`
   * 사용법:`mount point + relative path`
   * 예:

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* 재정의:

   * 목적:슈퍼 유형에 따라 리소스 병합
   * 마운트 지점:`/mnt/overide`
   * 사용법:`mount point + absolute path`
   * 예:

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### {#example-of-usage} 사용 예

몇 가지 예는 다음과 같습니다.

* 오버레이:

   * [콘솔 사용자 지정](/help/sites-developing/customizing-consoles-touch.md)
   * [페이지 작성 사용자 지정](/help/sites-developing/customizing-page-authoring-touch.md)

* 재정의:

   * [페이지 속성 구성](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)

