---
title: AEM 내 AI 어시스턴트 구성
description: Adobe Experience Manager에서 Admin Console을 사용하여 AI 어시스턴트를 설정하고 구성하는 방법에 대해 알아봅니다.
solution: Experience Manager
feature: Authoring, AI Assistant, AI Tools
role: Admin, Developer, User
exl-id: 06824b3d-f912-4922-8fb6-ee2ca04c6326
autotag-review: '2026-05-18T18:35:37.980Z'
TQID: 'https://experienceleague.adobe.com/5YTQUJbJPlJuxToS6AVhJww1KQ20tuOlRoCVquyfSng'
product_v2:
  - id: e14eb250-3c22-4a07-9061-a78112b2b826
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
feature_v2:
  - id: ac5ecfc1-cc78-4ecc-a90a-0362685062ce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
source-git-commit: 9c96b6744c7af2f061b4dfbf403560047485f9b5
workflow-type: tm+mt
source-wordcount: 1202
ht-degree: 98%

---

# AEM 내 AI 어시스턴트 구성 {#aem-ai-asst-admin-setup}

<!-- An Administrator must configure access, permissions, and settings before users in their organization can use the features in AI Assistant in AEM. -->

<!-- badge: label="Beta" type="Positive" -->

AEM(Adobe Experience Manager) 내 AI 어시스턴트를 사용하려면 AI 어시스턴트를 통해 제품 지식에 액세스할 수 있는 권한이 필요합니다. 이 권한은 기본적으로 켜져 있습니다.

제품 정보에 액세스할 수 있는 사용자를 제어하려면 Adobe ID과 연결된 이메일 주소에서 [aemaiassistant@adobe.com](mailto:aemaiassistant@adobe.com)으로 이메일을 보내십시오. Adobe가 사용자 수준 액세스 제어를 활성화할 수 있습니다. 활성화되면 관리자는 아래에 설명된 단계에 따라 사용자 수준 액세스 권한을 부여할 수 있습니다.

사용자 수준 액세스 제어를 요청한 경우 조직은 Adobe Admin Console을 통해 옵트인해야 합니다. 제품 관리자는 사용자 그룹을 생성(또는 선택)하고 새로운 “AI 어시스턴트” 권한을 부여합니다. 해당 그룹에 추가된 모든 사용자는 AEM에서 즉시 AI 어시스턴트를 사용할 수 있습니다. 회사 전체의 가용성을 목표로 하는 경우, 관리자는 해당 그룹에 모든 사용자를 할당하기만 하면 됩니다.

직원의 입장에서는 조직 내 Adobe Experience Manager의 제품 관리자를 식별하고 AI 지원 사용자 그룹에 추가할 것을 요청하는 등 프로세스가 간단합니다. 해당 그룹에 나타나면 다음에 로그인할 때 어시스턴트 아이콘이 자동으로 나타납니다.

관리자는 일반적인 Cloud Manager 거버넌스를 염두에 두어야 합니다. Admin Console에서 제품 관리자 권한을 보유하여 프로필을 만들거나 사용자 그룹을 관리하거나 권한을 편집합니다. 사용자가 어시스턴트의 기본 제공 **지원 티켓 만들기** 기능도 필요한 경우 동일한 개인 또는 그룹에 표준 **지원 관리자** 역할(표준 Admin Console 역할)을 추가합니다.

AEM 내 AI 어시스턴트의 구성 프로세스는 다음 단계로 구성됩니다.

1. [Adobe Admin Console에서 새 제품 프로필 만들기](#create-profile).
1. [AI 어시스턴트 제품 지식 권한 활성화](#enable-permission).
1. [새 사용자 그룹 만들기(또는 기존 사용자 그룹 사용)](#create-user-group).
1. [사용자 그룹에 사용자 추가](#add-users).
1. [사용자 그룹에 제품 프로필 할당](#assign-product-profile).

**사전 요구 사항**

시작하기 전에 다음 전제 조건을 충족했는지 확인합니다.

* Adobe Admin Console 내 최소한 제품 관리자 권한이 있어야 합니다.
* 조직의 사용자 관리 구조를 이해하고 있습니다.

**구성 고려 사항**

* 처리 시간: Cloud Manager에서 만든 리소스는 권한 구성을 위해 Admin Console에 표시되는 데 최대 2분이 걸릴 수 있습니다.
* 여러 프로필: 사용자는 여러 프로필에 속할 수 있으며 할당된 모든 프로필에서 권한이 결합됩니다.
* 조직 범위: 일부 권한은 모든 프로그램에 대해 조직 수준에서 적용될 수 있습니다.
* 사전 정의된 프로필: Admin Console에서 사전 정의된 권한 프로필을 삭제하지 마십시오.


## 1 - Adobe Admin Console에서 새 제품 프로필 만들기{#create-profile}

1. Experience Platform 설명서에 있는 [Adobe Admin Console에서 새 제품 프로필 만들기](https://experienceleague.adobe.com/ko/docs/experience-platform/access-control/ui/create-profile)의 자세한 지침을 따르십시오.

1. 새 제품 프로필을 만들 때 AI 어시스턴트에 대해 다음과 같이 제안된 값을 사용할 수 있습니다.

   | 텍스트 필드 | 제안 값 |
   | --- | --- |
   | 제품 프로필 이름 | `AI Assistant in AEM`(또는 선호하는 설명적인 이름) |
   | 표시 이름(선택 사항) | `AI Assistant` |
   | 설명(선택 사항) | `Product profile for managing AI Assistant in AEM access` |
   | 알림 | 조직의 환경 설정을 기반으로 구성 |


## 2 - AI 어시스턴트 제품 지식 권한 활성화{#enable-permission}

제품 프로필에 사용자 정의 권한을 할당하는 프로세스는 표준 Adobe Cloud Manager 사용자 정의 권한 워크플로를 따릅니다.

참조 문서: [새 제품 프로필에 사용자 정의 권한 할당](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions).

1. Admin Console에서 새로 만든 제품 프로필(`AI Assistant in AEM`)의 이름을 클릭합니다

   ![스크린샷](/help/assets/assets-ai/ai-assistant-console.png)

1. 편집 가능한 권한 목록을 보려면 **권한** 탭을 클릭합니다.

1. 테이블 목록에서 `AI Assistant Product Knowledge` 권한을 찾습니다.

   ![Admin Console의 AI 어시스턴트 권한 탭](/help/assets/assets-ai/ai-assistant-permission.png)

1. 권한 이름 오른쪽에서 ![연필 아이콘 또는 편집 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg)을 클릭합니다.

1. **AI 어시스턴트에 대한 권한 편집** 페이지에서 **AI 어시스턴트 제품 지식** 토글을 켭니다.

   ![AI 어시스턴트 제품 지식 토글 옵션에 대한 권한 페이지 편집](/help/assets/assets-ai/ai-assistant-prod-knowledge.png)

1. 페이지의 오른쪽 하단에 있는 **저장**&#x200B;을 클릭합니다.

   이제 제품 프로필에 AI 어시스턴트 제품 지식 권한이 활성화되어 있습니다.


## 3 - 새 사용자 그룹 만들기(또는 기존 사용자 그룹 사용).{#create-user-group}

1. 다음 중 하나를 수행하십시오.

>[!BEGINTABS]

>[!TAB 새 사용자 그룹 만들기]

1. Admin Console에서 **사용자** > **사용자 그룹**&#x200B;을 클릭합니다.

   ![사용자 그룹](/help/assets/assets-ai/ai-assistant-user-groups.png)

1. **사용자 그룹** 페이지에서 **새 사용자 그룹**&#x200B;을 클릭합니다.

   ![사용자 그룹 페이지의 새 사용자 그룹 버튼](/help/assets/assets-ai/ai-assistant-new-user-group.png)

1. **새 사용자 그룹 만들기** 페이지에서 다음 정보를 제공합니다.

   | 옵션 | 제안 값 |
   | --- | --- |
   | 사용자 그룹 이름 | `AI Assistant in AEM`(또는 기본 이름) |
   | 설명(선택 사항) | `User group for managing AI Assistant in AEM access` |

   ![새 사용자 그룹 페이지 만들기](/help/assets/assets-ai/ai-assistant-create-new-user-group.png)

1. 페이지의 오른쪽 하단에 있는 **저장**&#x200B;을 클릭합니다.

>[!TAB 기존 사용자 그룹 사용]

기존 AEM 사용자 그룹이 AI 어시스턴트 액세스 요구 사항을 충족하는 경우 새 그룹을 만드는 대신 사용할 수 있습니다.

>[!ENDTABS]

## 4 - 사용자 그룹에 사용자 추가{#add-users}

1. 다음 중 하나를 수행하십시오.

>[!BEGINTABS]

>[!TAB 개별 사용자 추가]

1. **사용자 그룹** 페이지의 **그룹 이름** 테이블에서 새로 만든 사용자 그룹 이름이나 기존 사용자 그룹 이름을 클릭합니다.

   ![테이블의 AEM 사용자 그룹 이름에 AI 어시스턴트를 표시하는 사용자 그룹 페이지](/help/assets/assets-ai/ai-assistant-user-group-name-in-table.png)

1. **AEM 내 AI 어시스턴트**&#x200B;에 대한 **사용자 그룹** 페이지에서 **사용자** 탭을 클릭한 다음 **사용자 추가**&#x200B;를 클릭합니다.

   ![AEM 사용자 그룹 페이지의 AI 도우미에 사용자 탭과 사용자 추가 버튼이 표시됨](/help/assets/assets-ai/ai-assistant-add-users.png)

1. **`Add users to this user group`** 페이지에서 AEM 내 AI 어시스턴트에 액세스해야 하는 사용자를 검색하여 선택합니다.

   ![이 사용자 그룹 페이지에 사용자 추가](/help/assets/assets-ai/ai-assistant-add-users-to-this-group.png)

1. 페이지의 오른쪽 하단에 있는 **저장**&#x200B;을 클릭합니다.
1. 이제 [사용자 그룹에 제품 프로필 할당](#assign-product-profile).

>[!TAB 사용자 일괄 추가]

Admin Console에서 일괄 업로드 기능을 사용할 수 있습니다.

1. 사용자 정보가 포함된 CSV 파일을 준비합니다.
1. 효율적인 대량 추가를 위해 **`Add users by CSV`** 옵션을 사용합니다.
1. 이제 [사용자 그룹에 제품 프로필 할당](#assign-product-profile).

>[!ENDTABS]


## 5 - 사용자 그룹에 제품 프로필 할당{#assign-product-profile}

이 단계는 사용자 그룹에 제품 프로필을 할당하기 위한 표준 Adobe Admin Console 워크플로를 따릅니다.

참조 문서: [기업 사용자의 제품 프로필 관리](https://helpx.adobe.com/kr/enterprise/using/manage-product-profiles.html)

1. [4 - 사용자 그룹에 사용자 추가](#add-users)에서 AEM 내 AI 어시스턴트 사용자 그룹에 있는 동안 **할당된 제품 프로필** 탭을 클릭합니다.
1. **프로필 할당**&#x200B;을 클릭합니다.

   ![할당된 제품 프로필 탭이 선택된 AEM 내 AI 어시스턴트 사용자 그룹 페이지](/help/assets/assets-ai/ai-assistant-assign-profile.png)

1. **제품 및 프로필 할당** 페이지의 **제품 프로필 선택** 대화 상자에서 **AI 어시스턴트** 제품 프로필을 검색하여 선택합니다.

   ![“제품 및 프로필 할당” 페이지에서 “제품 프로필 선택” 대화 상자와 “AI 어시스턴트” 제품 프로필이 선택됨](/help/assets/assets-ai/ai-assistant-select-product-profile.png)

1. 대화 상자의 오른쪽 하단 근처에서 **적용**&#x200B;을 클릭합니다.
1. **제품 및 프로필 할당** 페이지의 오른쪽 하단 근처에서 **저장**&#x200B;을 클릭합니다.

   ![AEM 사용자 그룹의 AI 어시스턴트에 할당된 AI 어시스턴트 제품 프로필이 표시됨](/help/assets/assets-ai/ai-assistant-profile-assigned-to-user-group.png)


## 구성 확인

* 제품 프로필에 할당된 사용자 그룹의 올바른 수가 표시되는지 확인합니다.
* 사용자 그룹에 올바른 사용자 수가 표시되는지 확인합니다.
* AI 어시스턴트 제품 지식 권한이 활성화되어 있고 올바르게 구성되어 있는지 확인합니다.


## 구성 테스트

할당된 그룹의 사용자가 다음 작업을 수행하도록 합니다.

1. AEM에 로그인합니다.
2. AI 어시스턴트 기능에 액세스할 수 있는지 확인합니다.
3. AI 어시스턴트의 기능을 테스트하여 제대로 활성화되었는지 확인합니다.

## 추가 참조

* [AEM 내 AI 어시스턴트](/help/ai-assistant-in-aem.md)
* [Adobe Experience Platform 액세스 제어](https://experienceleague.adobe.com/ko/docs/experience-platform/access-control/ui/overview)
<!-- * [Cloud Manager Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md) -->
