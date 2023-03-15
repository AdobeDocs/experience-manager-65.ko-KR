---
title: 페이지 속성 보기 사용자 지정
seo-title: Customizing Views of Page Properties
description: 모든 페이지에는 필요에 따라 편집할 수 있는 속성 세트가 있습니다
seo-description: Every page has a set of properties that you can edit as required
uuid: cbfca6e6-cb9e-43b1-8889-09a7cc9f8a51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6f8e08d1-831e-441a-ad1a-f5c8788f32d7
exl-id: 292874bf-2ee6-4638-937c-f8f26c93ca65
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 3%

---

# 페이지 속성 보기 사용자 지정{#customizing-views-of-page-properties}

모든 페이지에는 [속성](/help/sites-authoring/editing-page-properties.md) 는 사용자가 보고 편집할 수 있습니다. 일부는 페이지를 만들 때 필요하고(보기 만들기), 일부는 나중에 보고 편집할 수 있습니다(보기 편집). 이러한 페이지 속성은 대화 상자에서 정의하고 사용할 수 있습니다. ( `cq:dialog`)을 클릭하여 제품에서 사용할 수 있습니다.

>[!CAUTION]
>
>페이지 속성의 보기 맞춤화는 클래식 UI에서 사용할 수 없습니다.

모든 페이지 속성의 기본 상태는 다음과 같습니다.

* 만들기 보기에서 숨겨짐(예: **페이지 만들기** wizard)

* 편집 보기에서 사용할 수 있습니다(예: **속성 보기**)

변경이 필요한 경우 필드를 구체적으로 구성해야 합니다. 이 작업은 적절한 노드 속성을 사용하여 수행됩니다.

* 만들기 보기에서 사용할 수 있는 페이지 속성(예: **페이지 만들기** 마법사):

   * 이름: `cq:showOnCreate`
   * 유형: `Boolean`

* 편집 보기에서 사용할 수 있는 페이지 속성(예: **보기**/**편집**) **속성** 옵션):

   * 이름: `cq:hideOnEdit`
   * 유형: `Boolean`

예를들어, 아래에 그룹화된 필드에 대한 설정을 **기타 제목 및 설명** 다음에 있음 **기본** 기초 페이지 구성 요소에 대한 탭입니다. 다음 화면에 표시됩니다. **페이지 만들기** 다음으로 마법사: `cq:showOnCreate` 이(가) (으)로 설정되었습니다. `true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>다음을 참조하십시오. [페이지 속성 확장 자습서](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) 페이지 속성 맞춤화에 대한 안내서입니다.

## 페이지 속성 구성 {#configuring-your-page-properties}

페이지 구성 요소의 대화 상자를 구성하고 적절한 노드 속성을 적용하여 사용 가능한 필드를 구성할 수도 있습니다.

예를 들어 기본적으로 [**페이지 만들기** 마법사](/help/sites-authoring/managing-pages.md#creating-a-new-page) 아래에 그룹화된 필드를 표시합니다. **기타 제목 및 설명**. 이를 숨기려면 다음을 구성합니다.

1. 아래에 페이지 구성 요소 만들기 `/apps`.
1. 재정의 만들기(사용) *대화 상자 차이* 에서 제공 [Sling 리소스 병합](/help/sites-developing/sling-resource-merger.md))에 사용됩니다. `basic` 섹션(예: 페이지 구성 요소):

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >참조로서 다음을 참조하십시오.
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   하지만, 당신은 ***필수*** 의 아무 것도 변경하지 마십시오. `/libs` 경로.
   이는 의 콘텐츠가 `/libs` 는 다음에 인스턴스를 업그레이드할 때 덮어쓰기됩니다(또한 핫픽스 또는 기능 팩을 적용할 때 덮어쓰기될 수도 있음).
   구성 및 기타 변경에 권장되는 방법은 다음과 같습니다.
   1. 필요한 항목(예:에 존재하는 대로)을 다시 생성합니다. `/libs`) `/apps`
   1. 다음 범위 내에서 변경 `/apps`


1. 설정 `path` 속성 `basic` 기본 탭의 재정의를 지정합니다(다음 단계도 참조). 예:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. 재정의 만들기 `basic` - `moretitles` 섹션에 있는 마지막 항목이 될 필요가 없습니다. 예:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. 적절한 노드 속성을 적용합니다.

   * **이름**: `cq:showOnCreate`
   * **유형**: `Boolean`
   * **값**: `false`

   다음 **기타 제목 및 설명** 섹션이 **페이지 만들기** 마법사.

>[!NOTE]
라이브 카피와 함께 사용할 페이지 속성을 구성할 때에는 다음을 참조하십시오. [페이지 속성에서 MSM 잠금 구성](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) 을 참조하십시오.

## 페이지 속성의 샘플 구성 {#sample-configuration-of-page-properties}

이 샘플은 대화 상자 비교 기술을 [Sling 리소스 병합](/help/sites-developing/sling-resource-merger.md); 사용 포함 [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties). 또한 두 가지 사용 방법을 보여 줍니다 `cq:showOnCreate` 및 `cq:hideOnEdit`.

GITHUB의 코드

GitHub에서 이 페이지의 코드를 확인할 수 있습니다

* [GitHub에서 aem-authoring-extension-page-dialog 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
