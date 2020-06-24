---
title: 콘텐츠 조각 - 삭제 고려 사항
seo-title: 콘텐츠 조각 - 삭제 고려 사항
description: 콘텐츠 조각 - 삭제 고려 사항
seo-description: 콘텐츠 조각 - 삭제 고려 사항
uuid: e7ac1809-159f-4d02-ad30-dc6c246e8a04
contentOwner: aheimoz
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: ec21237f-9186-49b4-8039-99df4db7c14a
docset: aem65
translation-type: tm+mt
source-git-commit: a430c4de89bde3b907d342106465d3b5a7c75cc8
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 4%

---


# 콘텐츠 조각 - 삭제 고려 사항{#content-fragments-delete-considerations}

## 권한 - 삭제 또는 삭제 안 함 {#permissions-delete-or-not-delete}

이러한 권한이 배포되는 방식을 제한하고 제어해야 하는 많은 업계에서 컨텐츠 삭제 기능은 강력하지만 잠재적으로 민감할 수 있습니다.

삭제 권한과 관련하여 컨텐츠 조각은 두 가지 수준으로 간주되어야 합니다.

1. **컨텐츠 조각을 단일 엔티티로 사용합니다.**

   * **사용 사례**: 컨텐츠 조각을 편집/업데이트해야 하는 사용자 **및 전체 조각을 삭제해야 합니다**.
   * **권한**: 사용자 [및](/help/sites-administering/security.md#actions) /또는 그룹 관리를 [통해 삭제 권한을 할당할 수 있습니다](/help/sites-administering/security.md#managing-permissions).

1. **컨텐츠 조각을 구성하는 여러 하위 엔티티 예: variations, sub-nodes.**

   컨텐츠 조각 편집기의 기본 작업을 수행하려면 이러한 임시 하위 요소를 삭제할 수 있어야 합니다. 예를 들어 변형을 조작할 때 또한 메타데이터를 편집하거나 관련 컨텐츠를 관리할 때도 마찬가지입니다.

   * **사용 사례**: 전체 조각을 삭제할 수 **없는 컨텐츠 조각을 편집/업데이트해야 하는 사용자입니다**.
   * **권한**: 편집기 [기능에만 필요한 권한을 참조하십시오](/help/assets/content-fragments/content-fragments-delete.md#permissions-required-for-editor-functionality-only).

>[!NOTE]
>
>사용자에게 [삭제](/help/sites-administering/security.md#actions) 권한이 없는 경우 컨텐츠 조각 편집기는 *읽기 전용* 모드로 작동합니다.

>[!NOTE]
>
>AEM [에서 사용자 관리 작업을 감사하는 방법을 참조하십시오](/help/sites-administering/audit-user-management-operations.md).

## 편집기 기능에 필요한 권한만 {#permissions-required-for-editor-functionality-only}

컨텐츠 조각을 편집/업데이트해야 하는 사용자는 전체 조각을 삭제할 수 **없도록**&#x200B;허용하지 않고 특정 권한을 할당해야 합니다. 컨텐츠 조각 편집기의 기본 작업을 수행하려면 일시적으로 임시 하위 요소를 삭제할 수 있어야 합니다.

예를 들어 변형을 조작할 때 또한 메타데이터를 편집하거나 관련 컨텐츠를 관리할 때도 마찬가지입니다.

>[!NOTE]
>
>컨텐츠 조각을 편집/업데이트하는 데 필요한 삭제 권한은 사용자 및/또는 그룹 관리를 통해 [할당된 삭제 권한에 포함됩니다](/help/sites-administering/security.md#managing-permissions).

조각을 편집/업데이트하는 데 필요한 권한은 컨텐츠 조각을 포함하는 노드 또는 적절한 상위 노드(하위 수준에 관계없이)에 적용해야 `/content/dam`합니다. 이러한 상위 노드에 할당되면 해당 분기 내의 모든 노드에 권한이 적용됩니다.

예를 들어 다음과 같은 모든 컨텐츠 조각을 포함하는 폴더

* `/content/dam/contentfragments`

>[!CAUTION]
>
>모든 컨텐츠 조각 `/content/dam` 이 여기에 저장되므로 권한을 설정할 수도 있습니다.
>
>하지만 이 작업은 *다른 모든* 자산 유형에도 동일한 삭제 권한을 적용합니다.

특정 사용자 및/또는 그룹이 컨텐츠 조각을 편집/업데이트할 수 있도록 허용하기 위한 권한 사전 요구 사항은 다음과 같습니다.

>[!NOTE]
>
>이 목록에는 삭제 권한뿐만 아니라 필요한 모든 권한이 표시됩니다.

* 컨텐츠 조각 노드 또는 폴더의 경우:

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* 모든 컨텐츠 조각 `jcr:content`노드의 경우:

   * `jcr:addChildNodes`, `jcr:modifyProperties` `jcr:removeChildNodes`

* 모든 컨텐츠 조각 아래 `jcr:content` 의 모든 노드에 대해:

   * `jcr:addChildNodes`, `jcr:modifyProperties` and `jcr:removeChildNodes`, `jcr:removeNode`

이러한 `remove` 권한은 CRXDE Lite [에서 액세스 제어 목록을 사용하여 관리되어야 합니다](/help/sites-administering/user-group-ac-admin.md#access-right-management).

CRXDE Lite에서 또는 사용자 관리 콘솔을 사용하여 `add` 및 `modify` 권한을 관리할 수도 있습니다.

예를 들어, 그룹에 대한 `remove` 권한 정의 `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)

