---
title: 구성원 및 그룹 관리 콘솔
seo-title: 구성원 및 그룹 관리 콘솔
description: 구성원 및 그룹 관리 콘솔에 액세스하는 방법
seo-description: 구성원 및 그룹 관리 콘솔에 액세스하는 방법
uuid: 2e93e861-a066-4189-91db-f8b784bc5aea
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ccabf301-b417-48aa-8501-8360fd9f3e36
role: Administrator
exl-id: b64e24d2-8407-484c-8216-8d328ef5fa4f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 4%

---

# 구성원 및 그룹 관리 콘솔 {#members-groups-management-consoles}

## 개요 {#overview}

AEM Communities 기능을 사용하려면 게시 환경에서 커뮤니티에 참여하기 전에 사이트 방문자를 등록하고 로그인해야 하는 경우가 많습니다. 해당 사용자 등록은 게시 환경에만 있어야 하며, 일반적으로 이를 *구성원*&#x200B;이라고 하여 작성 환경에 등록된 *사용자*&#x200B;와 구분합니다.

### 게시 {#members-users-on-publish}의 구성원(사용자)

커뮤니티 구성원 및 그룹 콘솔을 사용하여 *게시* 환경에 등록된 구성원 및 구성원 그룹은 *author* 환경에서 만들고 관리할 수 있습니다. 이 작업은 [터널 서비스](deploy-communities.md#tunnel-service-on-author)가 활성화된 경우에만 가능합니다.

### 작성자 {#users-on-author}의 사용자

*author* 환경에 등록된 사용자 및 그룹을 관리하려면 플랫폼의 보안 콘솔을 사용해야 합니다.

* 전역 탐색에서 **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 사용자]**&#x200B;를 선택합니다.
* 전역 탐색에서 **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 그룹]**&#x200B;을 선택합니다.

>[!NOTE]
>
>샘플 컨텐츠가 배포되고 활성화되어 있으면 많은 샘플 사용자가 작성자와 게시 환경 모두에 있습니다. 이러한 사용자는 [nosamplecontent runmode](../../help/sites-administering/production-ready.md)를 사용하여 실행할 때 나타나지 않습니다.

## 구성원 콘솔 {#members-console}

작성 환경에서 게시 환경에 등록된 구성원을 관리하기 위한 구성원 콘솔에 연결하려면

* 전역 탐색에서 **[!UICONTROL 탐색]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 구성원]**&#x200B;을 선택합니다.

>[!CAUTION]
>
>[터널 서비스](deploy-communities.md#tunnel-service-on-author)가 활성화되어 있지 않으면 구성원 콘솔을 사용할 수 없습니다.

![member-console1](assets/member-console1.png)

### 검색 {#search-features}

`Members` 헤더 왼쪽의 사이드 패널 아이콘을 선택하여 검색 사이드 패널을 엽니다.

![](assets/leftpanel-icon.png)


![member-console2](assets/member-console2.png)

`Members` 헤더 왼쪽의 검색 아이콘을 선택하여 검색 사이드 패널을 닫았다가 전환합니다.

### 멤버 통계 {#member-statistics}

`Views`, `Posts`, `Follows` 및 `Likes`을 표시하는 열은 사용자가 Adobe Analytics [이 활성화된 하나 이상의 커뮤니티 사이트의 구성원인 경우 업데이트됩니다](sites-console.md#analytics).

### CSV 내보내기 {#export-csv}

`Export CSV` 링크를 선택하면 스프레드시트로 가져오기에 적합한 쉼표로 구분된 값 목록으로 모든 멤버를 다운로드할 수 있습니다.

열 헤더는 다음과 같습니다

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## 새 구성원 만들기 {#create-new-member}

게시 환경에서 사용자를 만들려면 `Create Member` 을 선택합니다.

![create-member1](assets/create-member1.png)

### 일반 - 멤버 세부 정보 {#general-member-details}

대부분의 필드는 구성원이 나중에 해당 프로필을 채울 수 있는 선택 필드입니다.

* **[!UICONTROL ID]**

(*필수*) 작성 가능한 ID는 구성원의 로그인 ID입니다.
기본적으로 ID는 필수 이메일 주소 값으로 설정되어 있습니다.
*만들어진 ID는 수정되지* 않을 수 있습니다.

* **[!UICONTROL 이메일 주소]**

(*필수*) 구성원의 이메일 주소입니다.
구성원은 프로필을 업데이트할 때 전자 메일 주소를 변경할 수 있습니다.I
ID가 기본적으로 이메일 주소로 설정되면 이메일 주소가 변경될 때 ID는 *변경되지 않습니다.*

* **[!UICONTROL 암호]**

   (*필수*) 로그인 암호입니다.

* **[!UICONTROL 암호 재입력]**

   (*필수*) 확인을 위해 암호를 다시 입력합니다.

* **[!UICONTROL 사이트에 구성원 추가]**

   (*선택 사항*) 커뮤니티 사이트의 구성원 그룹에 구성원을 추가하려면 기존 커뮤니티 사이트에서 선택합니다.

* **[!UICONTROL 그룹에 구성원 추가]**

   (*선택 사항*) 기존 멤버 그룹에서 선택하여 해당 그룹에 멤버를 추가합니다.

* **[!UICONTROL 저장]**&#x200B;을 선택합니다

### 일반 - 계정 설정 {#general-account-settings}

계정 설정에서 커뮤니티 관리자가 다음을 수행할 수 있습니다.

* **[!UICONTROL 상태]**
   * 금지
구성원이 로그인할 수 없어 페이지를 보거나 로그인해야 하는 활동에 참가할 수 없습니다. 그들은 여전히 열린 커뮤니티 사이트를 익명으로 방문할 수 있습니다.

   * 금지되지 않음
구성원은 커뮤니티 사이트에 대한 전체 액세스 권한을 갖습니다.

   기본값은 `Not Banned`입니다.

* **[!UICONTROL 기여도 제한]**

   이 옵션을 선택하면 컨텐츠 게시 기능이 제한됩니다.
기본값은 기여도 제한 구성에 따라 다릅니다.
[멤버 기여도 제한](limits.md)을 참조하십시오.

* **[!UICONTROL 암호 변경]**

   기존 멤버를 수정할 때 나타나는 링크입니다. 커뮤니티 관리자가 구성원의 암호를 재설정할 수 있는 기능을 제공합니다.

### 일반 - 사진 {#general-photo}

멤버의 아바타를 제공하려면 먼저 **[!UICONTROL 이미지 업로드]**&#x200B;를 선택하고 .jpg, .png, .tif 또는 .gif의 이미지를 선택합니다. 이미지의 기본 크기는 72dpi에서 240 x 240픽셀입니다.

### 일반 - 사이트에 구성원 추가 {#general-add-member-to-sites}

구성원을 하나 이상의 커뮤니티 사이트의 구성원 그룹에 추가할 수 있습니다. 텍스트 상자에 텍스트를 입력하여 시작합니다.

### 일반 - 그룹에 구성원 추가 {#general-add-member-to-groups}

구성원이 하나 이상의 구성원 그룹에 추가될 수 있습니다. 텍스트 상자에 텍스트를 입력하여 시작합니다.

### 배지 탭 {#badges-tab}

`BADGES` 패널에서는 배지를 수동으로 할당하고 취소할 수 있습니다. 배지는 배지 뿐 아니라 지정된 역할을 위해 사용될 수 있습니다.

[점수 및 배지](implementing-scoring.md)도 참조하십시오.

![create-member2](assets/create-member2.png)

* **[!UICONTROL 배지 추가]**
   * [사용 가능한 배지](badges.md)에서 선택하려면 입력을 시작합니다. 배지를 선택한 후 구성원의 아바타와 함께 배지가 표시될 각 사이트 또는 모든 사이트를 선택합니다.
   * 여러 배지와 사이트를 선택할 수 있습니다.
* **[!UICONTROL 배지 제거]**
   * 배지 옆에 있는 휴지통 아이콘을 선택하여 제거합니다.

## 그룹 콘솔 {#groups-console}

작성 환경에서 사용할 수 있는 그룹 콘솔에서 게시 환경에 등록된 구성원 그룹을 만들고 관리할 수 있습니다. 이 기능은 특히 다음과 같은 경우에 유용합니다.
* [권한이 있는 구성원 그룹](users.md#privilegedmembersgroups)
* [지원 리소스의 그룹 기반 할당](resources.md)

그룹 콘솔에 액세스하려면
* 전역 탐색에서 **[!UICONTROL 탐색]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 그룹]**&#x200B;을 선택합니다.

>[!CAUTION]
>
>[터널 서비스](deploy-communities.md#tunnel-service-on-author)가 활성화되어 있지 않으면 그룹 콘솔을 사용할 수 없습니다.

### 새 그룹 만들기 {#create-new-group}

게시 환경에서 그룹을 만들려면 `Add Group` 을 선택합니다.

![group-console1](assets/group-console1.png)

새 게시 측 구성원 그룹을 만드는 데 필요한 필드는 다음과 같습니다.

* **[!UICONTROL ID]**

   (*필수*) 그룹 고유 ID입니다.

   *만들어진 ID는 수정되지 않을 수 있습니다.*

* **[!UICONTROL 이름]**

   (*선택 사항*) 그룹의 표시 이름입니다.

   기본값은 ID입니다.

* **[!UICONTROL 설명]**

   (*선택 사항*) 그룹의 목적과 권한에 대한 설명입니다.

* **[!UICONTROL 그룹에 구성원 추가]**

   (*선택적*) 그룹의 초기 멤버로 포함할 게시 측 구성원을 선택합니다.

* **[!UICONTROL 저장]**&#x200B;을 선택합니다

## 승인된 관리자 {#authorized-administrators}

커뮤니티 구성원 콘솔에서 구성원을 사용하여 작업할 때는 적절한 권한이 있는 사용자로 로그인하고 [터널 서비스](deploy-communities.md#tunnel-service-on-author)에서 사용하는 복제 에이전트를 올바르게 구성해야 합니다.

`admin`(으)로 로그인하지 않은 경우 로그인한 사용자는 `administrators` 사용자 그룹의 구성원이어야 합니다.

작성자](deploy-communities.md#replication-agents-on-author)의 복제 에이전트도 참조하십시오.[
