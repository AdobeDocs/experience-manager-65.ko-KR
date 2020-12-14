---
title: 중첩된 그룹 작성
seo-title: 중첩된 그룹 작성
description: 중첩된 그룹 만들기
seo-description: 중첩된 그룹 만들기
uuid: b377dc1b-bbb6-41c9-b0fc-8281e1410685
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 752235d2-21ac-46d2-82ed-5fec09c645e9
docset: aem65
translation-type: tm+mt
source-git-commit: 5d196d1f6d5f94f2d3ef0d4461cfe38562f8ba8c
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 4%

---


# 중첩된 그룹 작성{#authoring-nested-groups}

## 작성자 {#creating-groups-on-author}에 그룹 만들기

AEM 작성자 인스턴스의 전역 탐색:

* **[!UICONTROL 커뮤니티]** > **[!UICONTROL 사이트]**&#x200B;를 선택합니다.
* **[!UICONTROL 참여 폴더]**&#x200B;를 선택하여 엽니다.
* **[!UICONTROL 시작하기 자습서]** 영어 사이트의 카드를 선택합니다.

   * 카드 이미지를 선택합니다.
   * *아이콘을 선택하지 말고*&#x200B;하십시오.

그 결과 [그룹 콘솔](/help/communities/groups.md)에 도달합니다.

![create-group](assets/create-group.png)

groups 함수는 그룹 인스턴스가 생성되는 폴더로 표시됩니다. 열 그룹 폴더를 선택합니다. 게시에서 만든 그룹이 표시됩니다.

![create-new-group](assets/create-new-group.png)

## 기본 아트 그룹 만들기 {#create-main-arts-group}

참여를 위한 사이트 구조에 그룹 함수가 포함되어 있으므로 이 그룹을 만들 수 있습니다. 사이트의 `Reference Template`에 있는 함수의 구성은 활성화된 그룹 템플릿을 선택할 수 있도록 기본적으로 설정되어 있습니다. 따라서 이 새 그룹에 대해 선택한 템플릿은 `Reference Group`입니다.

이러한 콘솔은 커뮤니티 사이트 콘솔과 유사합니다.

* **[!UICONTROL 그룹 만들기]**&#x200B;를 선택합니다.

* **커뮤니티 그룹 템플릿**:

   * **[!UICONTROL 커뮤니티 그룹 제목]**:예술.
   * **[!UICONTROL 커뮤니티 그룹 설명]**:다양한 아트 그룹의 상위 그룹입니다.
   * **[!UICONTROL 커뮤니티 그룹 루트]**: *기본값으로 두십시오*.
   * **[!UICONTROL 추가 사용 가능한 커뮤니티 그룹 언어]**:드롭다운 메뉴를 사용하여 사용 가능한 커뮤니티 그룹 언어를 선택합니다. 메뉴에는 상위 커뮤니티 사이트를 만든 모든 언어가 표시됩니다. 사용자는 이러한 언어 중에서 선택하여 이 단일 단계에서 여러 로케일에 그룹을 만들 수 있습니다. 동일한 그룹이 각 커뮤니티 사이트의 그룹 콘솔에서 지정된 여러 언어로 만들어집니다.
   * **[!UICONTROL 커뮤니티 그룹 이름]**:예술.
   * **[!UICONTROL 템플릿]**:아래로 이동하여 선택  `Reference Group.`
   * **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![중첩된 커뮤니티 그룹](assets/parent-to-nestedgroup.png)

다음 설정을 사용하여 다른 패널을 계속 진행합니다.

* **[!UICONTROL 디자인]**

   * 디자인을 변경하거나 기본 상위 사이트의 디자인을 허용합니다.
   * **[!UICONTROL 다음]**&#x200B;을 선택합니다.

* **[!UICONTROL 설정]**

   * **[!UICONTROL 중재]**

      * 비워 둡니다(상위 사이트에서 상속).
   * **[!UICONTROL 멤버십]**

      * 기본 `Optional Membership.` 사용

      * **[!UICONTROL 썸네일]**
         * `optional.*`
      * **[!UICONTROL 다음]**&#x200B;을 선택합니다.



* **[!UICONTROL 만들기]**&#x200B;를 선택합니다.

### 아트 그룹 내에 그룹 중첩 {#nesting-groups-within-arts-group}

이제 `groups` 폴더에 2개의 그룹이 있습니다(페이지 새로 고침).

![그룹 중첩](assets/create-community-group.png)

#### 그룹 게시 {#publish-group}

`arts` 그룹 내에 중첩된 그룹을 만들기 전에 `arts` 카드 위로 마우스를 가져간 다음 게시할 게시 아이콘을 선택합니다.

![게시 사이트](assets/publish-site.png)

그룹이 게시되었는지 확인할 때까지 기다립니다.

![그룹 게시](assets/group-published.png)

`arts` 그룹에도 `groups` 폴더가 있어야 하지만 비어 있고 새 그룹을 만들 수 있는 폴더가 있어야 합니다. 아트 그룹 폴더로 이동하여 각각 다른 멤버십 설정으로 3개의 중첩 그룹을 만듭니다.

1. **[!UICONTROL 시각적 요소]**

   * 제목: `Visual Arts`
   * 이름: `visual`
   * 템플릿: `Reference Group`
   * 멤버십:공개 그룹인 `Optional Membership`을 선택하고 모든 구성원에 대해 엽니다.

1. **[!UICONTROL 청각]**

   * 제목: `Auditory Arts`
   * 이름: `auditory`
   * 템플릿: `Reference Group`
   * 멤버십:구성원이 가입할 수 있는 열린 그룹 `Required Membership`을 선택합니다.

1. **[!UICONTROL 역사]**

   * 제목: `Art History`
   * 이름: `history`
   * 템플릿: `Reference Group`
   * 멤버십:초대된 구성원만 볼 수 있는 비밀 그룹 `Restricted Membership`을 선택합니다. 예를 들어 [데모 사용자](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`를 초대합니다.

페이지를 새로 고쳐 세 개의 중첩된 그룹(하위 커뮤니티)을 모두 봅니다.

커뮤니티 사이트 콘솔에서 중첩된 그룹으로 이동하려면 다음을 수행하십시오.

* **[!UICONTROL 참여 폴더]** 선택
* **[!UICONTROL 시작하기 자습서 카드]** 선택
* **[!UICONTROL 그룹]** 폴더 선택
* **[!UICONTROL 아트 카드]** 선택
* **[!UICONTROL 그룹]** 폴더 선택

![create-new-group2](assets/create-new-group2.png)

## 게시 그룹 {#publishing-groups}

![게시 사이트](assets/publish-site.png)

기본 커뮤니티 사이트를 게시한 후:

* 각 그룹을 개별적으로 게시:

   * 그룹이 게시되었다는 확인을 기다리는 중입니다.

* 다음 내에 중첩된 그룹을 게시하기 전에 상위 그룹을 게시합니다.

   * 모든 그룹은 하향식 방식으로 게시되어야 합니다.

![그룹 게시](assets/group-published.png)

## 게시 시 경험 {#experience-on-publish}

로그인하면 다음과 같이 [데모 사용자](/help/communities/tutorials.md#demo-users)가 다음에 사용되는 경우와 같이 서로 다른 그룹을 경험할 수 있습니다.

* 미술/작업 내역 그룹 구성원:emily.andrews@mailinator.com/password
   * 제한적(비밀) 그룹, 예술/내역이 표시됩니다.
   * 선택적(공개) 그룹을 볼 수 있습니다.
   * 제한된(열린) 그룹에 가입할 수 있습니다.

* 그룹 관리자:aaron.mcdonald@mailinator.com/password

   * 선택적(공개) 그룹을 볼 수 있습니다.
   * 제한된(열린) 그룹에 가입할 수 있습니다.
   * 제한된(비밀) 그룹을 볼 수 없습니다.

작성자의 커뮤니티 [구성원 및 그룹 콘솔](/help/communities/members.md)에 액세스하여 커뮤니티 그룹에 해당하는 다양한 구성원 그룹에 다른 사용자를 추가합니다.

