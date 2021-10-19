---
title: 중첩된 그룹 작성
seo-title: Authoring Nested Groups
description: 중첩 그룹 만들기
seo-description: Create nested groups
uuid: b377dc1b-bbb6-41c9-b0fc-8281e1410685
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 752235d2-21ac-46d2-82ed-5fec09c645e9
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
source-git-commit: 1074843a0105df39382b64defe66fc262986b9c9
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 4%

---

# 중첩된 그룹 작성{#authoring-nested-groups}

## 작성자에 대한 그룹 만들기 {#creating-groups-on-author}

AEM 작성자 인스턴스의 전역 탐색에서 다음을 수행합니다.

* 선택 **[!UICONTROL 커뮤니티]** > **[!UICONTROL Sites]**.
* 선택 **[!UICONTROL 폴더 참여]** 열려고
* 사용할 카드를 선택합니다 **[!UICONTROL 시작하기 자습서]** 영어 사이트.

   * 카드 이미지를 선택합니다.
   * 작업 *not* 아이콘을 선택합니다.

결과는 [그룹 콘솔](/help/communities/groups.md):

![create-group](assets/create-group.png)

그룹 함수는 그룹 인스턴스가 만들어진 폴더로 표시됩니다. 그룹 폴더를 선택하여 엽니다. 게시할 때 만든 그룹이 표시됩니다.

![create-new-group](assets/create-new-group.png)

## 주 아트 그룹 만들기 {#create-main-arts-group}

참여용 사이트 구조에 그룹 기능이 포함되어 있으므로 이 그룹을 만들 수 있습니다. 사이트의 `Reference Template` 기본값은 활성화된 그룹 템플릿을 선택할 수 있도록 하는 것입니다. 따라서 이 새 그룹에 대해 선택한 템플릿은 다음과 같습니다 `Reference Group`.

이러한 콘솔은 커뮤니티 사이트 콘솔과 유사합니다.

* 선택 **[!UICONTROL 그룹 만들기]**

* **커뮤니티 그룹 템플릿**:

   * **[!UICONTROL 커뮤니티 그룹 제목]**: 예술
   * **[!UICONTROL 커뮤니티 그룹 설명]**: 다양한 예술 그룹의 상위 그룹
   * **[!UICONTROL 커뮤니티 그룹 루트]**: *기본값으로 둡니다.*
   * **[!UICONTROL 추가 사용 가능한 커뮤니티 그룹 언어]**: 사용 가능한 커뮤니티 그룹 언어를 선택하려면 드롭다운 메뉴를 사용합니다. 이 메뉴에는 상위 커뮤니티 사이트가 생성된 모든 언어가 표시됩니다. 사용자는 이러한 언어 중에서 선택하여 이 단일 단계에서 여러 로케일에 그룹을 만들 수 있습니다. 동일한 그룹은 각 커뮤니티 사이트의 그룹 콘솔에서 지정된 여러 언어로 생성됩니다.
   * **[!UICONTROL 커뮤니티 그룹 이름]**: 예술
   * **[!UICONTROL 템플릿]**: 선택할 드롭다운 `Reference Group`
   * **[!UICONTROL 다음]**&#x200B;을 선택합니다

![중첩된 커뮤니티 그룹](assets/parent-to-nestedgroup.png)

다음 설정을 사용하여 다른 패널을 계속 진행합니다.

* **[!UICONTROL 디자인]**

   * 디자인을 변경하거나 기본 상위 사이트의 디자인을 허용합니다.
   * **[!UICONTROL 다음]**&#x200B;을 선택합니다.

* **[!UICONTROL 설정]**

   * **[!UICONTROL 중재]**

      * 비워 둡니다(상위 사이트에서 상속).
   * **[!UICONTROL 멤버십]**

      * 기본값 사용 `Optional Membership.`

      * **[!UICONTROL 썸네일]**
         * `optional.*`
      * **[!UICONTROL 다음]**&#x200B;을 선택합니다.



* **[!UICONTROL 만들기]**&#x200B;를 선택합니다.

### 아트 그룹 내에 그룹 중첩 {#nesting-groups-within-arts-group}

다음 `groups` 폴더에는 이제 두 개의 그룹이 있습니다(페이지를 새로 고침).

![그룹 중첩](assets/create-community-group.png)

#### 그룹 게시 {#publish-group}

내에서 중첩된 그룹을 만들기 전에 `arts` 그룹을 마우스로 가리키면 `arts` 카드를 선택하고 게시 아이콘을 선택하여 게시합니다.

![publish-site](assets/publish-site.png)

그룹이 게시되었는지 확인할 때까지 기다립니다.

![그룹 게시](assets/group-published.png)

다음 `arts` 그룹도 포함해야 합니다 `groups` 폴더가 비어 있고 새 그룹을 만들 수 있는 폴더가 비어 있습니다. 아트 그룹 폴더로 이동하고 각각 다른 멤버 자격 설정을 사용하여 3개의 중첩 그룹을 만듭니다.

1. **[!UICONTROL 시각적]**

   * 제목: `Visual Arts`
   * 이름: `visual`
   * 템플릿: `Reference Group`
   * 멤버십: 선택 `Optional Membership`모든 구성원에게 열려 있는 공개 그룹입니다.

1. **[!UICONTROL 청각]**

   * 제목: `Auditory Arts`
   * 이름: `auditory`
   * 템플릿: `Reference Group`
   * 멤버십: 선택 `Required Membership`: 구성원이 참여할 수 있는 열린 그룹입니다.

1. **[!UICONTROL 역사]**

   * 제목: `Art History`
   * 이름: `history`
   * 템플릿: `Reference Group`
   * 멤버십: 선택 `Restricted Membership`: 초대받은 구성원에게만 표시되는 비밀 그룹입니다. 예를 들어, 초대 [데모 사용자](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

페이지를 새로 고쳐 세 개의 중첩 그룹(하위 커뮤니티)을 모두 확인합니다.

커뮤니티 사이트 콘솔에서 중첩 그룹으로 이동하려면 다음을 수행하십시오.

* 선택 **[!UICONTROL 폴더 참여]**
* 선택 **[!UICONTROL 시작하기 자습서 카드]**
* 선택 **[!UICONTROL 그룹]** 폴더
* 선택 **[!UICONTROL 예술 카드]**
* 선택 **[!UICONTROL 그룹]** 폴더

![create-new-group2](assets/create-new-group2.png)

## 게시 그룹 {#publishing-groups}

![publish-site](assets/publish-site.png)

기본 커뮤니티 사이트를 게시한 후:

* 각 그룹을 개별적으로 게시:

   * 그룹이 게시되었는지 확인을 기다리는 중입니다.

* 내에 중첩된 그룹을 게시하기 전에 상위 그룹을 게시합니다.

   * 모든 그룹은 하향식으로 게시해야 합니다.

![그룹 게시](assets/group-published.png)

## 게시할 때의 경험 {#experience-on-publish}

로그인할 때(예: [데모 사용자](/help/communities/tutorials.md#demo-users) 다음 용도로 사용됩니다.

* 미술/기록 그룹 구성원: emily.andrews@mailinator.com/password
   * 제한된(비밀) 그룹인 예술/기록이 보입니다.
   * 선택적(공개) 그룹을 볼 수 있습니다.
   * 제한된(열린) 그룹에 가입할 수 있습니다.

* 그룹 관리자: aaron.mcdonald@mailinator.com/password

   * 선택적(공개) 그룹을 볼 수 있습니다.
   * 제한된(열린) 그룹에 가입할 수 있습니다.
   * 제한된(비밀) 그룹을 볼 수 없습니다.

커뮤니티 액세스 [구성원 및 그룹 콘솔](/help/communities/members.md) 작성자가 커뮤니티 그룹에 해당하는 다양한 구성원 그룹에 다른 사용자를 추가할 때.
