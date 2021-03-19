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
role: 관리자
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 4%

---


# 구성원 및 그룹 관리 콘솔 {#members-groups-management-consoles}

## 개요 {#overview}

AEM Communities 기능은 게시 환경에서 커뮤니티에 참여하기 전에 사이트 방문자가 등록되고 로그인해야 하는 경우가 많습니다. 사용자 등록은 게시 환경에만 존재해야 하며 작성 환경에 등록된 *사용자*&#x200B;와 구분하기 위해 일반적으로 *구성원*&#x200B;이라고 합니다.

### 게시 {#members-users-on-publish}의 구성원(사용자)

커뮤니티 구성원 및 그룹 콘솔을 사용하면 *게시* 환경에 등록된 구성원 및 구성원 그룹을 *작성자* 환경에서 만들고 관리할 수 있습니다. 이것은 [터널 서비스](deploy-communities.md#tunnel-service-on-author)가 활성화된 경우에만 가능합니다.

### 작성자 {#users-on-author}의 사용자

*author* 환경에 등록된 사용자 및 그룹을 관리하려면 플랫폼의 보안 콘솔을 사용해야 합니다.

* 전역 탐색에서 **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 사용자]**&#x200B;를 선택합니다.
* 전역 탐색에서 **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 그룹]**&#x200B;을 선택합니다.

>[!NOTE]
>
>샘플 컨텐츠를 배포하고 사용할 수 있게 되면 많은 샘플 사용자가 작성자 및 게시 환경 모두에 존재합니다. 이러한 사용자는 [nosampleconcontent runmode](../../help/sites-administering/production-ready.md)로 실행할 때 표시되지 않습니다.

## 구성원 콘솔 {#members-console}

작성 환경에서 게시 환경에 등록된 구성원을 관리하기 위한 구성원 콘솔에 액세스하려면:

* 전역 탐색에서 **[!UICONTROL 탐색]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 구성원]**&#x200B;을 선택합니다.

>[!CAUTION]
>
>[터널 서비스](deploy-communities.md#tunnel-service-on-author)가 활성화되지 않으면 구성원 콘솔을 사용할 수 없습니다.

![member-console1](assets/member-console1.png)

### 검색 {#search-features}

`Members` 헤더의 왼쪽에 있는 사이드 패널 아이콘을 선택하여 검색 사이드 패널 열기를 전환합니다.

![](assets/leftpanel-icon.png)


![member-console2](assets/member-console2.png)

`Members` 헤더의 왼쪽에 있는 검색 아이콘을 선택하여 닫힌 검색 사이드 패널을 전환합니다.

### 구성원 통계 {#member-statistics}

`Views`, `Posts`, `Follows` 및 `Likes`을(를) 표시하는 열은 사용자가 Adobe Analytics [이(가) 활성화된 하나 이상의 커뮤니티 사이트 구성원인 경우에 업데이트됩니다.](sites-console.md#analytics).

### CSV 내보내기 {#export-csv}

`Export CSV` 링크를 선택하면 스프레드시트로 가져오는 데 적합한 쉼표로 구분된 값 목록으로 모든 멤버를 다운로드할 수 있습니다.

열 헤더는

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## 새 구성원 만들기 {#create-new-member}

게시 환경에서 사용자를 만들려면 `Create Member`을 선택합니다.

![create-member1](assets/create-member1.png)

### 일반 - 구성원 세부 정보 {#general-member-details}

대부분의 필드는 멤버가 나중에 프로필에서 채울 수 있는 선택 필드입니다.

* **[!UICONTROL ID]**

(*필수*) 권한이 부여된 ID는 구성원의 로그인 ID입니다.
기본적으로 ID는 필요한 이메일 주소 값으로 설정됩니다.
*만들어진 ID는 수정되지 않을 수 있습니다*.

* **[!UICONTROL 이메일 주소]**

(*필수*) 회원의 이메일 주소입니다.
회원은 프로필을 업데이트할 때 이메일 주소를 변경할 수 있습니다.I
ID의 기본값이 이메일 주소로 지정되면 이메일 주소가 변경되면 ID는 *변경되지 않습니다*.

* **[!UICONTROL 암호]**

   (*필수*) 로그인 암호입니다.

* **[!UICONTROL 암호 재입력]**

   (*필수*) 확인을 위해 암호를 다시 입력합니다.

* **[!UICONTROL 사이트에 구성원 추가]**

   (*선택적*) 커뮤니티 사이트의 구성원 그룹에 구성원을 추가하려면 기존 커뮤니티 사이트에서 선택합니다.

* **[!UICONTROL 그룹에 구성원 추가]**

   (*선택적*) 해당 그룹에 구성원을 추가하려면 기존 구성원 그룹 중에서 선택합니다.

* **[!UICONTROL 저장]**&#x200B;을 선택합니다

### 일반 - 계정 설정 {#general-account-settings}

계정 설정에서 커뮤니티 관리자가 다음을 수행할 수 있습니다.

* **[!UICONTROL 상태]**
   * 금지
회원이 로그인할 수 없으므로 페이지를 보거나 로그인이 필요한 활동에 참여할 수 없습니다. 그들은 여전히 공개 커뮤니티 사이트를 익명으로 방문할 수도 있다.

   * 금지되지 않음
회원은 커뮤니티 사이트에 대한 모든 액세스 권한을 가집니다.

   기본값은 `Not Banned`입니다.

* **[!UICONTROL 기여도 제한]**

   이 확인란을 선택하면 회원의 컨텐츠 게시 권한이 제한됩니다.
기본값은 기여도 제한의 구성에 따라 다릅니다.
[멤버 기여도 제한](limits.md)을 참조하십시오.

* **[!UICONTROL 암호 변경]**

   기존 구성원을 수정할 때 나타나는 링크입니다. 커뮤니티 관리자가 구성원의 암호를 재설정할 수 있는 기능을 제공합니다.

### 일반 - 사진 {#general-photo}

멤버에 대한 아바타를 제공하려면 **[!UICONTROL 이미지 업로드]**&#x200B;를 선택하고 .jpg, .png, .tif 또는 .gif 형식의 이미지를 선택합니다. 이미지의 기본 크기는 72dpi의 240 x 240픽셀입니다.

### 일반 - 사이트에 구성원 추가 {#general-add-member-to-sites}

구성원을 하나 이상의 커뮤니티 사이트 구성원 그룹에 추가할 수 있습니다. 텍스트 상자에 텍스트를 입력하여 시작합니다.

### 일반 - 그룹에 구성원 추가 {#general-add-member-to-groups}

구성원을 하나 이상의 구성원 그룹에 추가할 수 있습니다. 텍스트 상자에 텍스트를 입력하여 시작합니다.

### 배지 탭 {#badges-tab}

`BADGES` 패널에서는 배지를 수동으로 할당하고 취소할 수 있습니다. 배지는 일반적으로 획득한 배지뿐만 아니라 지정된 역할용일 수 있습니다.

[채점 및 배지](implementing-scoring.md)도 참조하십시오.

![create-member2](assets/create-member2.png)

* **[!UICONTROL 배지 추가]**
   * [사용 가능한 배지](badges.md)에서 선택할 수 있도록 입력을 시작합니다. 배지가 선택되면 각 사이트 또는 모든 사이트를 선택하여 배지가 회원의 아바타와 함께 표시되어야 합니다.
   * 여러 배지와 사이트를 선택할 수 있습니다.
* **[!UICONTROL 배지 제거]**
   * 배지 옆에 있는 휴지통 아이콘을 선택하여 제거합니다.

## 그룹 콘솔 {#groups-console}

작성 환경에서 사용할 수 있는 그룹 콘솔에서는 게시 환경에 등록된 구성원 그룹을 만들고 관리할 수 있습니다. 이 기능은 특히 다음과 같은 경우에 유용합니다.
* [권한 있는 구성원 그룹](users.md#privilegedmembersgroups)
* [지원 리소스의 그룹 기반 할당](resources.md)

그룹 콘솔에 액세스하려면
* 전역 탐색에서 **[!UICONTROL 탐색]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 그룹]**&#x200B;을 선택합니다.

>[!CAUTION]
>
>[터널 서비스](deploy-communities.md#tunnel-service-on-author)가 활성화되지 않은 경우 그룹 콘솔을 사용할 수 없습니다.

### 새 그룹 만들기 {#create-new-group}

게시 환경에서 그룹을 만들려면 `Add Group`을 선택합니다.

![group-console1](assets/group-console1.png)

새 게시 측 구성원 그룹을 만드는 데 필요한 필드는 다음과 같습니다.

* **[!UICONTROL ID]**

   (*필수*) 그룹 고유 ID입니다.

   *만들어진 ID는 수정되지 않을 수 있습니다.*

* **[!UICONTROL 이름]**

   (*선택적*) 그룹의 표시 이름입니다.

   기본값은 ID입니다.

* **[!UICONTROL 설명]**

   (*선택적*) 그룹의 목적과 권한에 대한 설명입니다.

* **[!UICONTROL 그룹에 구성원 추가]**

   (*선택적*) 그룹의 초기 멤버로 포함할 게시 측 구성원을 선택합니다.

* **[!UICONTROL 저장]**&#x200B;을 선택합니다

## 허가된 관리자 {#authorized-administrators}

커뮤니티 구성원 콘솔에서 구성원을 사용하여 작업할 때는 적절한 권한이 있는 사용자로 로그인하고 [터널 서비스](deploy-communities.md#tunnel-service-on-author)에서 사용하는 복제 에이전트가 올바르게 구성되도록 로그인해야 합니다.

`admin`으로 로그인하지 않은 경우 로그인한 사용자는 `administrators` 사용자 그룹의 구성원이어야 합니다.

작성자](deploy-communities.md#replication-agents-on-author)의 복제 에이전트를 참조하십시오.[
