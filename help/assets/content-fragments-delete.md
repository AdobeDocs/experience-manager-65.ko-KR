---
title: 컨텐츠 조각 - 삭제 고려 사항
seo-title: 컨텐츠 조각 - 삭제 고려 사항
description: 컨텐츠 조각 - 삭제 고려 사항
seo-description: 컨텐츠 조각 - 삭제 고려 사항
uuid: e7ac1809-159f-4d02-ad30-dc6c246e8a04
contentOwner: aheimoz
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: ec21237f-9186-49b4-8039-99df4db7c14a
docset: aem65
translation-type: tm+mt
source-git-commit: 6edecebec6d64a30fd05887a56d81f80863c5213

---


# 컨텐츠 조각 - 삭제 고려 사항{#content-fragments-delete-considerations}

## 권한 - 삭제 또는 삭제 안 함 {#permissions-delete-or-not-delete}

컨텐츠를 삭제하는 기능은 강력하지만 잠재적으로 민감하므로 이러한 권한이 배포되는 방식을 제한하고 제어해야 하는 많은 업계에서 매우 중요합니다.

삭제 권한과 관련하여 컨텐츠 조각은 다음 두 가지 수준에서 고려해야 합니다.

1. **컨텐츠 조각을 단일 엔티티로 사용합니다.**

   * **사용 사례**:컨텐츠 조각을 편집/업데이트해야 하는 **사용자이며 전체 조각을**&#x200B;삭제합니다.
   * **권한**:삭제 [권한은 사용자](/help/sites-administering/security.md#actions) 및/또는 그룹 관리를 통해 [할당할 수 있습니다](/help/sites-administering/security.md#managing-permissions).

1. **컨텐츠 조각을 구성하는 여러 하위 엔티티;예: 변형, 하위 노드.**

   컨텐츠 조각 편집기의 기본 작업을 수행하려면 이러한 일시적인 하위 요소를 삭제할 수 있어야 합니다. 예를 들어 변형을 조작할 때또한 메타데이터를 편집하거나 관련 컨텐츠를 관리할 때 가능합니다.

   * **사용 사례**:전체 조각을 삭제할 수 **없는 컨텐츠 조각을**&#x200B;편집/업데이트해야 하는 사용자입니다.
   * **권한**:편집기 [기능에 필요한 권한만](/help/assets/content-fragments-delete.md#permissions-required-for-editor-functionality-only)참조하십시오.

>[!NOTE]
>
>사용자에게 삭제 [권한이 없는](/help/sites-administering/security.md#actions) 경우 컨텐츠 조각 편집기는 *읽기 전용* 모드로 작동합니다.

>[!NOTE]
>
>AEM [에서 사용자 관리 작업을 감사하는 방법을 참조하십시오](/help/sites-administering/audit-user-management-operations.md).

## 편집기 기능에만 필요한 권한 {#permissions-required-for-editor-functionality-only}

컨텐츠 조각을 전체 조각을 **삭제하지**&#x200B;못하도록 컨텐츠 조각을 편집/업데이트해야 하는 사용자는 컨텐츠 조각 편집기의 기본 작업을 수행하려면 임시 하위 요소를 삭제할 수 있어야 하므로 특정 권한을 할당해야 합니다.

예를 들어 변형을 조작할 때또한 메타데이터를 편집하거나 관련 컨텐츠를 관리할 때 가능합니다.

>[!NOTE]
>
>컨텐츠 조각을 편집/업데이트하는 데 필요한 삭제 권한은 사용자 및/또는 그룹 관리를 통해 [할당된 삭제 권한에 포함됩니다](/help/sites-administering/security.md#managing-permissions).

조각을 편집/업데이트하는 데 필요한 권한은 컨텐츠 조각을 포함하는 노드 또는 적절한 상위 노드(아래의 임의 수준 `/content/dam`)에 적용해야 합니다. 이러한 상위 노드에 할당되면 해당 분기 내의 모든 노드에 권한이 적용됩니다.

예를 들어 다음과 같은 모든 컨텐츠 조각을 저장할 폴더

* `/content/dam/contentfragments`

>[!CAUTION]
>
>모든 컨텐츠 조각이 여기에 저장되므로 에 대한 권한을 설정할 `/content/dam` 수도 있습니다.
>
>그러나 이 작업은 *모든* 다른 자산 유형에도 동일한 삭제 권한을 적용합니다.

특정 사용자 및/또는 그룹이 컨텐츠 조각을 편집/업데이트할 수 있도록 허용하기 위한 권한 사전 요구 사항은 다음과 같습니다.

>[!NOTE]
>
>이 목록에는 삭제 권한뿐만 아니라 필요한 모든 권한이 표시됩니다.

* 컨텐츠 조각 노드 또는 폴더의 경우:

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* 모든 컨텐츠 조각 `jcr:content`노드의 경우:

   * `jcr:addChildNodes`, `jcr:modifyProperties` 및 `jcr:removeChildNodes`

* 모든 컨텐츠 조각 아래 `jcr:content` 모든 노드의 경우:

   * `jcr:addChildNodes`, `jcr:modifyProperties` 및 `jcr:removeChildNodes`, `jcr:removeNode`

이러한 `remove` 권한은 CRXDE Lite 내에서 액세스 제어 목록을 사용하여 [관리되어야 합니다](/help/sites-administering/user-group-ac-admin.md#access-right-management).

CRXDE Lite에서 또는 사용자 관리 콘솔을 사용하여 `add` 및 `modify` 권한을 관리할 수도 있습니다.

예를 들어, 그룹에 대한 `remove` 권한 정의 `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)

