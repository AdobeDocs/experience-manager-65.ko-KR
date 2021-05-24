---
title: 페이지 속성의 벌크 편집을 위한 페이지 구성
seo-title: 페이지 속성의 벌크 편집을 위한 페이지 구성
description: 페이지 속성의 벌크 편집을 사용하면 여러 페이지의 속성을 한 번에 편집할 수 있습니다
seo-description: 페이지 속성의 벌크 편집을 사용하면 여러 페이지의 속성을 한 번에 편집할 수 있습니다
uuid: 1ad403d2-4b93-4943-ae45-74bf20705b81
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: fe61ee4b-51b6-4a6f-91d8-1c02b29cc1db
exl-id: 1787e643-fc8e-40e0-8e14-97b222a7c320
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 13%

---

# 페이지 속성의 벌크 편집을 위한 페이지 구성 {#configuring-your-page-for-bulk-editing-of-page-properties}

[페이지 속성의 벌크 ](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) 편집여러 페이지의 속성을 한 번에 편집할 수 있도록 해줍니다.

다른 값이 있을 수 있으므로 페이지 속성이 기본값으로 벌크 편집용으로 활성화되지 않습니다. 명시적으로 허용되어야 합니다(활성화됨). 벌크 편집에 사용할 수 있는 페이지 속성을 정의할 때는 다음과 같은 특정 의미를 고려해야 합니다.

* 특정 필드는 일반적으로 고유합니다.예: 페이지 제목. 이러한 필드를 벌크 편집에 사용할 수 있도록 하는 것이 어떤 의미인지 결정해야 합니다. 이때 하나의 값이 적용됩니다.
* 특정 필드에는 여러 값이 있을 수 있습니다. 이 경우 렌더링 시 의미 있는 표현이 필요합니다.

   예를 들어 &quot;게시 준비&quot;를 나타내는 확인란이 있습니다. 벌크 편집 전에 여러 값이 있을 수 있습니다(예: 준비, 검토 중, 진행 중).

>[!CAUTION]
>
>페이지 속성의 벌크 편집은 다음과 같습니다.
>
>* 클래식 UI에서는 사용할 수 없습니다.
>* Live Copy 내의 페이지에는 사용할 수 없습니다.
>* 리소스 유형이 동일한 페이지에만 사용할 수 있습니다.

>



>[!NOTE]
>
>벌크 편집은 자산에 대해서도 사용할 수 있습니다. 비슷하지만 몇 가지 차이점이 있습니다. 자세한 내용은 [다중 자산의 속성 편집](/help/assets/metadata.md)을 참조하십시오. [스키마 편집기](/help/assets/metadata-schemas.md)를 사용하여 자산에 대한 벌크 메타데이터 편집기에서 필드를 사용자 지정할 수 있습니다.

## 필드 {#enabling-a-field} 활성화

>[!NOTE]
>
>특정 필드에는 여러 값이 있을 수 있습니다. 이 경우 렌더링 시 의미 있는 표현이 필요합니다. 이러한 이유로 다음 필드 유형만 활성화해야 합니다.
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`

>



필드는 페이지 구성 요소에서 사용할 수 있습니다(*템플릿에 이 아님).*

1. CRXDE Lite(또는 그에 상응하는 메서드)를 사용하여 페이지 구성 요소를 엽니다.

   예를 들어,`/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >이 예에서는 인스턴스에 코어 구성 요소가 설치되어 있다고 가정합니다. 이 경우 인스턴스가 We.Retail 샘플 컨텐츠로 실행 중입니다. 자세한 내용은 [핵심 구성 요소 설명서](https://docs.adobe.com/content/help/ko-KR/experience-manager-core-components/using/introduction.html)를 참조하십시오.

1. `cq:dialog` 정의 내에서 필요한 필드로 이동합니다.
1. 필드 노드에서 다음 속성을 정의합니다.

   * **이름**: `allowBulkEdit`
   * **유형**: `Boolean`
   * **값**:  `true`

   예를 들어, 표준 페이지 [기본 구성 요소](/help/sites-authoring/default-components-foundation.md)의 경우:

   `/libs/foundation/components/page`

   속성은 다음에 정의되어 있습니다.

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >***은 `/libs` 경로에서 아무 것도 변경하지 않아야 합니다.***
   >
   >이는 다음 번에 인스턴스를 업그레이드할 때 `/libs` 컨텐츠를 덮어쓰게 되기 때문입니다(핫픽스 또는 기능 팩을 적용할 때 덮어쓸 수 있음).
   >
   >구성 및 기타 변경에 대해 권장되는 방법은 다음과 같습니다.
   >
   >    1. `/apps` 아래에 필요한 항목(즉, `/libs`에 있는 항목)을 다시 만듭니다.
   >    1. `/apps` 내에서 변경


1. 업데이트를 유지하려면 **모두 저장**&#x200B;을 선택하십시오.
