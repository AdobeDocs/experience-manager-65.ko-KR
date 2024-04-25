---
title: 구성원 및 그룹 관리 콘솔
description: 멤버 및 그룹 관리 콘솔에 액세스하는 방법
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: b64e24d2-8407-484c-8216-8d328ef5fa4f
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---


# 구성원 및 그룹 관리 콘솔 {#members-groups-management-consoles}

## 개요 {#overview}

AEM Communities 기능은 종종 게시 환경에서 커뮤니티에 참여하기 전에 사이트 방문자를 등록하고 로그인해야 합니다. 사용자 등록은 게시 환경에만 있어야 하며 일반적으로 다음과 같이 합니다. *구성원* 이들을 구별하다 *사용자* 작성자 환경에 등록되었습니다.

### 게시의 구성원(사용자) {#members-users-on-publish}

커뮤니티 구성원 및 그룹 콘솔 사용,에 등록된 구성원 및 구성원 그룹 *게시* 환경에서 환경을 만들고 관리할 수 있습니다. *작성자* 환경. 이는 [터널 업무](deploy-communities.md#tunnel-service-on-author) 이(가) 활성화되었습니다.

### 작성자의 사용자 {#users-on-author}

에 등록된 사용자 및 그룹 관리 *작성자* 환경에서는 플랫폼의 보안 콘솔을 사용해야 합니다.

* 전역 탐색에서 을 선택합니다. **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 사용자]**.
* 전역 탐색에서 을 선택합니다. **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 그룹]**.

>[!NOTE]
>
>샘플 콘텐츠가 배포되고 활성화되면 많은 샘플 사용자가 작성자 및 게시 환경 모두에 존재합니다. 이 사용자는 을(를) 사용하여 실행할 때 표시되지 않습니다. [nosamplecontent 실행 모드](../../help/sites-administering/production-ready.md).

## 구성원 콘솔 {#members-console}

작성 환경에서 게시 환경에 등록된 멤버를 관리하기 위해 멤버 콘솔에 도달하려면 다음을 수행합니다.

* 전역 탐색에서 을 선택합니다. **[!UICONTROL 탐색]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 구성원]**

>[!CAUTION]
>
>다음과 같은 경우에는 구성원 콘솔을 사용할 수 없습니다. [터널 업무](deploy-communities.md#tunnel-service-on-author) 이(가) 활성화되지 않았습니다.

![구성원 콘솔](assets/member-console1.png)

### 검색 {#search-features}

왼쪽의 사이드 패널 아이콘을 선택합니다. `Members` 헤더를 클릭하여 검색 사이드 패널을 엽니다.

![검색 사이드 패널 아이콘](assets/leftpanel-icon.png)


![구성원 콘솔에 대한 필터 옵션](assets/member-console2.png)

왼쪽의 검색 아이콘을 선택합니다. `Members` 머리글 : 검색 사이드 패널이 닫혀 있는 것을 전환합니다.

### 멤버 통계 {#member-statistics}

표시되는 열 `Views`, `Posts`, `Follows` 및 `Likes` 사용자가 Adobe Analytics을 사용하는 하나 이상의 커뮤니티 사이트에 속해 있는 경우 업데이트됩니다 [활성화됨](sites-console.md#analytics).

### CSV 내보내기 {#export-csv}

선택 `Export CSV` 링크를 클릭하면 스프레드시트로 가져오기에 적합한 쉼표로 구분된 값 목록으로 모든 멤버가 다운로드됩니다.

열 머리글은 다음과 같습니다

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## 새 구성원 만들기 {#create-new-member}

선택 `Create Member` 게시 환경에서 사용자를 만듭니다.

![새 멤버 생성 창](assets/create-member1.png)

### 일반 - 멤버 세부 정보 {#general-member-details}

대부분의 필드는 구성원이 나중에 프로필에서 채울 수 있는 선택 필드입니다.

* **[!UICONTROL ID]**

(*필수*) 승인 가능 ID는 구성원의 로그인 ID입니다.
기본적으로 ID는 필수 이메일 주소 값으로 설정됩니다.
*만든 ID는 수정할 수 없습니다*.

* **[!UICONTROL 이메일 주소]**

(*필수*) 회원의 이메일 주소입니다.
회원은 프로필을 업데이트할 때 이메일 주소를 변경할 수 있습니다.I ID가 이메일 주소로 기본 설정된 경우 ID는 *아님* 이메일 주소가 변경되면 를 변경합니다.

* **[!UICONTROL 암호]**

  (*필수*) 로그인 암호입니다.

* **[!UICONTROL 암호 재입력]**

  (*필수*) 확인을 위해 암호를 다시 입력합니다.

* **[!UICONTROL 사이트에 구성원 추가]**

  (*선택 사항*) 기존 커뮤니티 사이트에서 선택하여 커뮤니티 사이트의 구성원 그룹에 구성원을 추가합니다.

* **[!UICONTROL 그룹에 구성원 추가]**

  (*선택 사항*) 기존 구성원 그룹에서 선택하여 해당 그룹에 구성원을 추가합니다.

* 선택 **[!UICONTROL 저장]**

### 일반 - 계정 설정 {#general-account-settings}

계정 설정에서 커뮤니티 관리자는 다음과 같은 작업을 수행할 수 있습니다.

* **[!UICONTROL 상태]**
   * 금지됨 구성원이 로그인할 수 없어 페이지를 보거나 로그인이 필요한 활동에 참여할 수 없습니다. 이들은 여전히 익명으로 공개된 커뮤니티 사이트를 방문할 수 있습니다.

   * 금지되지 않음 구성원이 커뮤니티 사이트에 전체 액세스할 수 있습니다.

  기본값은 입니다 `Not Banned`.

* **[!UICONTROL 기여도 제한]**

  선택하면 콘텐츠를 게시할 수 있는 구성원의 기능이 제한됩니다.
기본값은 기여도 제한의 구성에 따라 다릅니다.
다음을 참조하십시오 [구성원 기여도 제한](limits.md).

* **[!UICONTROL 암호 변경]**

  기존 멤버를 수정할 때 표시되는 링크 커뮤니티 관리자가 구성원의 암호를 재설정할 수 있는 기능을 제공합니다.

### 일반 - 사진 {#general-photo}

멤버에 대한 아바타를 제공하려면 다음을 선택하여 시작합니다. **[!UICONTROL 이미지 업로드]** .jpg, .png, .tif 또는 .gif 형식의 이미지를 선택합니다. 이미지의 기본 크기는 72dpi에서 240 x 240픽셀입니다.

### 일반 - 사이트에 구성원 추가 {#general-add-member-to-sites}

구성원을 하나 이상의 커뮤니티 사이트 구성원 그룹에 추가할 수 있습니다. 텍스트 상자에 텍스트를 입력하여 시작합니다.

### 일반 - 그룹에 구성원 추가 {#general-add-member-to-groups}

구성원을 하나 이상의 구성원 그룹에 추가할 수 있습니다. 텍스트 상자에 텍스트를 입력하여 시작합니다.

### 배지 탭 {#badges-tab}

다음 `BADGES` 패널은 배지를 수동으로 할당하고 해지하는 기능을 제공합니다. 배지는 할당된 역할에 대해 지정될 수 있으며 일반적으로 습득되는 배지입니다.

참조: [채점 및 배지](implementing-scoring.md).

![멤버십 설정 편집 창](assets/create-member2.png)

* **[!UICONTROL 배지 추가]**
   * 다음에서 선택하려면 입력을 시작합니다. [사용 가능한 배지](badges.md). 배지를 선택한 후에는 각 사이트 또는 배지가 멤버의 아바타와 함께 표시되어야 하는 모든 사이트를 선택합니다.
   * 여러 개의 배지와 사이트를 선택할 수 있습니다.
* **[!UICONTROL 배지 제거]**
   * 배지 옆에 있는 휴지통 아이콘을 선택하여 제거합니다.

## 그룹 콘솔 {#groups-console}

작성 환경에서 사용할 수 있는 그룹 콘솔을 사용하여 게시 환경에 등록된 구성원 그룹을 만들고 관리할 수 있습니다. 이는 다음 경우에 특히 유용합니다. [권한이 있는 구성원 그룹](users.md#privilegedmembersgroups).

그룹 콘솔에 액세스하려면:
* 전역 탐색에서 을 선택합니다. **[!UICONTROL 탐색]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 그룹]**.

>[!CAUTION]
>
>이 경우 그룹 콘솔을 사용할 수 없습니다. [터널 업무](deploy-communities.md#tunnel-service-on-author) 이(가) 활성화되지 않았습니다.

### 새 그룹 만들기 {#create-new-group}

선택 `Add Group` 게시 환경에서 그룹을 만듭니다.

![새 그룹 만들기 창](assets/group-console1.png)

게시측 구성원 그룹을 만드는 데 필요한 필드는 다음과 같습니다.

* **[!UICONTROL ID]**

  (*필수*) 그룹 고유 ID입니다.

  *만든 ID는 수정할 수 없습니다.*

* **[!UICONTROL 이름]**

  (*선택 사항*) 그룹의 표시 이름입니다.

  기본값은 ID입니다.

* **[!UICONTROL 설명]**

  (*선택 사항*) 그룹의 목적 및 권한에 대한 설명입니다.

* **[!UICONTROL 그룹에 구성원 추가]**

  (*선택 사항*) 그룹의 초기 멤버로 포함할 게시측 멤버를 선택합니다.

* 선택 **[!UICONTROL 저장]**

## 권한 있는 관리자 {#authorized-administrators}

커뮤니티 구성원 콘솔에서 구성원으로 작업하는 경우 적절한 권한이 있는 사용자로 및 가 사용하는 복제 에이전트에 대해 로그인해야 합니다. [터널 업무](deploy-communities.md#tunnel-service-on-author) 올바르게 구성해야 합니다.

다음으로 로그인하지 않은 경우 `admin`을 지정하면 로그인한 사용자가 `administrators` 사용자 그룹.

참조: [작성자의 복제 에이전트](deploy-communities.md#replication-agents-on-author).
