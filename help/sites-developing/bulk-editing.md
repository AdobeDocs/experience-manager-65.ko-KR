---
title: 페이지 속성의 벌크 편집을 위한 페이지 구성
seo-title: Configuring your Page for Bulk Editing of Page Properties
description: 페이지 속성을 벌크 편집하면 여러 페이지의 속성을 한 번에 편집할 수 있습니다
seo-description: Bulk editing of page properties lets you edit the properties of multiple pages at once
uuid: 1ad403d2-4b93-4943-ae45-74bf20705b81
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: fe61ee4b-51b6-4a6f-91d8-1c02b29cc1db
exl-id: 1787e643-fc8e-40e0-8e14-97b222a7c320
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 24%

---

# 페이지 속성의 벌크 편집을 위한 페이지 구성 {#configuring-your-page-for-bulk-editing-of-page-properties}

[페이지 속성의 일괄 편집](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages)을 통해 한 번에 여러 페이지의 속성을 편집할 수 있습니다.

값이 다를 수 있으므로 페이지 속성은 기본값으로 벌크 편집을 활성화하지 않습니다. 명시적으로 허용(활성화)되어야 합니다. 일괄 편집에 사용할 수 있는 페이지 속성을 정의할 때 다음과 같은 특정 영향을 고려해야 합니다.

* 특정 필드는 일반적으로 고유합니다(예: 페이지 제목). 하나의 값이 적용될 때 일괄 편집에 이러한 필드를 활성화하는 것이 중요한지 여부를 결정합니다.
* 특정 필드에는 여러 값이 있을 수 있습니다. 렌더링할 때 의미 있는 표현이 필요합니다.

  예를 들어 &quot;게시 준비&quot;를 나타내는 확인란입니다. 이 값에는 대량 편집 전에 몇 가지 값이 있을 수 있습니다(예: 준비, 검토 중, 진행 중).

>[!CAUTION]
>
>페이지 속성의 일괄 편집에는 다음과 같은 특징이 있습니다.
>
>* 클래식 UI에서는 사용할 수 없습니다.
>* Live Copy 내의 페이지에는 사용할 수 없습니다.
>* 리소스 유형이 동일한 페이지에만 사용할 수 있습니다.
>

>[!NOTE]
>
>에셋에 대해서도 벌크 편집을 사용할 수 있습니다. 비슷하지만 몇 가지 차이점이 있습니다. 다음을 참조하십시오 [여러 에셋의 속성 편집](/help/assets/metadata.md) 전체 정보. 에셋용 벌크 메타데이터 편집기에서 필드를 사용자 지정하려면 [스키마 편집기](/help/assets/metadata-schemas.md).

## 필드 활성화 {#enabling-a-field}

>[!NOTE]
>
>특정 필드에는 여러 값이 있을 수 있습니다. 렌더링할 때 의미 있는 표현이 필요합니다. 이러한 이유로 다음 필드 유형만 활성화해야 합니다.
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`
>

필드는 페이지 구성 요소에서 활성화됩니다(*아님* (템플릿에서):

1. CRXDE Lite(또는 이와 동등한 방법)를 사용하여 페이지 구성 요소를 엽니다.

   예를 들어`/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >이 예제에서는 핵심 구성 요소가 인스턴스에 설치되어 있다고 가정합니다. 이 경우 인스턴스가 We.Retail 샘플 콘텐츠로 실행되는 경우입니다. 다음을 참조하십시오. [핵심 구성 요소 설명서](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 추가 정보.

1. `cq:dialog` 정의 내에서 필수 필드로 이동합니다.
1. 필드 노드에서 다음 속성을 정의합니다.

   * **이름**: `allowBulkEdit`
   * **유형**: `Boolean`
   * **값**: `true`

   (예: 표준 페이지) [기초 구성 요소](/help/sites-authoring/default-components-foundation.md):

   `/libs/foundation/components/page`

   속성은 다음에 정의됩니다.

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >본인 ***필수*** 의 아무 것도 변경하지 마십시오. `/libs` 경로.
   >
   >이는 의 콘텐츠가 `/libs` 는 다음에 인스턴스를 업그레이드할 때 덮어쓰기됩니다(또한 핫픽스 또는 기능 팩을 적용할 때 덮어쓰기될 수도 있음).
   >
   >구성 및 기타 변경에 권장되는 방법은 다음과 같습니다.
   >
   >    1. 필요한 항목 다시 만들기(존재하는 그대로) `/libs`) `/apps`
   >    1. 다음 범위 내에서 변경 `/apps`

1. **모두 저장**&#x200B;을 선택하여 업데이트 내용을 유지합니다.
