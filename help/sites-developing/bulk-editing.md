---
title: 페이지 속성의 벌크 편집을 위한 페이지 구성
seo-title: 페이지 속성의 벌크 편집을 위한 페이지 구성
description: 페이지 속성의 벌크 편집을 통해 여러 페이지의 속성을 한 번에 편집할 수 있습니다
seo-description: 페이지 속성의 벌크 편집을 통해 여러 페이지의 속성을 한 번에 편집할 수 있습니다
uuid: 1ad403d2-4b93-4943-ae45-74bf20705b81
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: fe61ee4b-51b6-4a6f-91d8-1c02b29cc1db
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuring your Page for Bulk Editing of Page Properties {#configuring-your-page-for-bulk-editing-of-page-properties}

[페이지 속성의](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) 일괄 편집을 사용하면 여러 페이지의 속성을 한 번에 편집할 수 있습니다.

값이 다를 수 있으므로 페이지 속성은 기본적으로 벌크 편집용으로 활성화되지 않습니다. 명시적으로 허용 목록에 포함되어야 합니다(활성화). 벌크 편집에 사용할 페이지 속성을 정의할 때 다음과 같은 특정 의미를 고려해야 합니다.

* 특정 필드는 일반적으로 고유합니다.예: 페이지 제목. 한 값이 적용될 시기에 이러한 필드를 벌크 편집용으로 활성화할지 여부를 결정해야 합니다.
* 특정 필드에는 여러 값이 있을 수 있습니다. 이 경우 렌더링할 때 의미 있는 표현이 필요합니다.

   예를 들어 &quot;게시 준비&quot; 확인란을 선택합니다. 벌크 편집(예: 준비, 검토 중, 진행 중) 전에 여러 값이 있을 수 있습니다.

>[!CAUTION]
>
>페이지 속성의 벌크 편집은 다음과 같습니다.
>
>* 클래식 UI에서는 사용할 수 없습니다.
>* Live Copy 내의 페이지에는 사용할 수 없습니다.
>* 동일한 리소스 유형의 페이지에만 사용할 수 있습니다.
>



>[!NOTE]
>
>자산에 대해서도 벌크 편집을 사용할 수 있습니다. 비슷하지만 몇 가지 차이점이 있습니다. 자세한 내용은 [다중 자산의 속성 편집](/help/assets/managing-multiple-assets.md)을 참조하십시오. 스키마 편집기를 사용하여 자산에 대한 일괄 메타데이터 편집기에서 필드를 사용자 정의할 [수](/help/assets/metadata-schemas.md)있습니다.

## 필드 활성화 {#enabling-a-field}

>[!NOTE]
>
>특정 필드에는 여러 값이 있을 수 있습니다. 이 경우 렌더링할 때 의미 있는 표현이 필요합니다. 따라서 다음 필드 유형만 활성화해야 합니다.
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`
>



필드는 페이지 구성 요소에서 사용할 수 있습니다(템플릿은&#x200B;*아님* ).

1. CRXDE Lite(또는 상응하는 방법)를 사용하여 페이지 구성 요소를 엽니다.

   예를 들어,`/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >이 예에서는 인스턴스가 We.Retail 샘플 컨텐츠와 함께 실행 중인 경우, 핵심 구성 요소가 인스턴스에 설치되어 있다고 가정합니다. See the [Core Components documentation](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) for more information.

1. 정의 내에서 필수 필드로 `cq:dialog` 이동합니다.
1. 필드 노드에서 다음 속성을 정의합니다.

   * **이름**: `allowBulkEdit`
   * **유형**: `Boolean`
   * **값**: `true`
   예를 들어 표준 페이지 [기반 구성 요소의](/help/sites-authoring/default-components-foundation.md)경우:

   `/libs/foundation/components/page`

   속성은 다음 항목에 정의됩니다.

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >패스에 있는 ***어떤 것도 변경하지*** 않아야 `/libs` 합니다.
   >
   >이는 다음에 인스턴스를 업그레이드할 때 의 컨텐츠를 `/libs` 덮어쓰게 되기 때문입니다(핫픽스 또는 기능 팩을 적용할 때 덮어쓸 수 있음).
   >
   >구성 및 기타 변경에 대한 권장 방법은 다음과 같습니다.
   >
   >    1. 필요한 항목(즉, 있는 대로)을 `/libs``/apps`
   >    1. Make any changes within `/apps`


1. 업데이트를 **유지하려면** 모두 저장을 선택합니다.

