---
title: 주석 사용
seo-title: Using Comments
description: 댓글 기능을 통해 로그인한 사이트 방문자가 자신의 의견과 지식을 공유할 수 있습니다
seo-description: Comments feature lets signed-in site visitors share their opinions and knowledge
uuid: 40acd962-846c-483c-b789-aab3a7d2b31b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 216cfb3e-777e-4773-afba-749debdca000
docset: aem65
exl-id: 30baebd9-13c5-4fde-a494-85601abc32a5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 5%

---

# 주석 사용 {#using-comments}

## 소개 {#introduction}

주석 기능은 로그인한 사이트 방문자(구성원)가 사이트에 있는 콘텐츠에 대한 의견 및 지식을 공유할 수 있도록 하는 데 사용됩니다. 이 기능은 다른 기능에 이미 있는 경우가 많지만 웹 사이트에 추가될 수 있습니다.

이 문서에서는 다음 사항을 설명합니다.

* 추가 중 `Comments` 을 클릭하여 페이지를 만듭니다.
* 에 대한 구성 설정 `Comments` 구성 요소.

>[!NOTE]
>
>댓글의 익명 게시는 지원되지 않습니다. 사이트 방문자가 참여하려면 등록(회원 가입)하고 로그인해야 합니다.

### 페이지에 주석 추가 {#adding-comments-to-a-page}

을(를) 추가하려면 `Comments` 구성 요소를 페이지에 추가하려면 작성자 모드에서 구성 요소 브라우저를 사용하여

* `Communities / Comments`

및 를 페이지에 드래그하여 사용자가 댓글을 달 수 있는 기능을 기준으로 한 위치, 페이지 맨 아래로 끕니다.

필요한 정보는 다음을 참조하십시오. [커뮤니티 구성 요소 기본 사항](/help/communities/basics.md).

다음의 경우 [필수 클라이언트측 라이브러리](/help/communities/essentials-comments.md#essentials-for-client-side) 포함됩니다. 이렇게 하면 `Comments` 구성 요소가 표시됩니다.

![comments-component](assets/comments-component.png)

>[!NOTE]
>
>하나만 `Comments` 구성 요소가 페이지에 있을 수 있습니다. 일부 Communities 기능에는 블로그, 캘린더, 포럼, QnA 및 리뷰와 같은 댓글이 이미 포함되어 있습니다.

### 주석 구성 {#configuring-comments}

배치된 을(를) 선택합니다 `Comments` 에 액세스하고 선택할 구성 요소 `Configure` 편집 대화 상자를 여는 아이콘.

![구성 아이콘](assets/configure.png)

![주석 설정](assets/commentssettings.png)

#### 주석 탭 {#comments-tab}

아래 **댓글** 탭에서 방문자가 주석을 입력하는 방법을 지정합니다.

* **답글 허용**

   선택하면 구성원이 기존 댓글에 회신할 수 있습니다. 기본값은 선택 해제되어 있습니다.

* **페이지당 댓글**

   페이지당 표시되는 댓글 수와 표시되는 답글 수를 제한합니다. 기본값은 10입니다.

* **파일 업로드 허용**

   선택하면 파일을 업로드하는 옵션이 텍스트 입력 상자와 함께 표시됩니다. 기본값은 선택 해제되어 있습니다.

* **최대 파일 크기**

   [파일 업로드 허용]이 선택된 경우에만 해당됩니다. 이 값은 업로드되는 파일 크기를 제한합니다. 기본 제한은 10MB입니다.

* **최대 메시지 길이**

   텍스트 상자에 입력할 수 있는 최대 문자 수. 기본값은 4096자입니다.

* **허용되는 파일 유형**

   [파일 업로드 허용]이 선택된 경우에만 해당됩니다. &quot;점&quot; 구분 기호가 있는 쉼표로 구분된 파일 이름 확장자 목록입니다. 예: .jpg, .jpeg, .png, .doc, .docx, .pdf 파일 유형을 지정하면 지정하지 않은 파일 유형은 허용되지 않습니다. 기본값은 모든 파일 형식이 허용되도록 지정되지 않습니다.

* **리치 텍스트 편집기**

   선택하면 주석이 마크업과 함께 입력됩니다. 기본값은 선택 해제되어 있습니다.

* **투표 허용**

   선택하면 위 또는 아래로 투표할 수 있는 옵션이 텍스트 입력 상자와 함께 표시됩니다. 기본값은 선택 해제되어 있습니다.

* **다음 허용**

   선택하면 구성원이 주석을 따를 수 있도록 허용합니다. 기본값은 선택 해제되어 있습니다.

* **배지 표시**

   선택하면 획득 및 수여된 배지가 표시되도록 허용합니다. 기본값은 선택 해제되어 있습니다.

#### 사용자 중재 탭 {#user-moderation-tab}

아래 **사용자 중재** 탭에서 게시된 댓글을 관리하는 방법을 지정합니다. 자세한 내용은 [사용자 생성 컨텐츠 중재](/help/communities/moderate-ugc.md).

* **사전 관리**

   선택하면 게시 사이트에 댓글이 표시되기 전에 승인되어야 합니다. 기본값은 선택 해제되어 있습니다.

* **댓글 삭제**

   선택하면 댓글을 게시한 회원에게 삭제 권한이 제공된다. 기본값은 선택 해제되어 있습니다.

* **댓글 거부**

   선택하면 중재자의 댓글 거부를 허용합니다. 기본값은 선택 해제되어 있습니다.

* **댓글 닫기 / 다시 열기**

   선택하면 중재자가 댓글을 닫거나 다시 열 수 있습니다. 기본값은 선택 해제되어 있습니다.

* **댓글에 플래그 지정**

   선택하면 구성원이 주석을 부적절한 항목으로 표시하도록 허용합니다. 기본값은 선택 해제되어 있습니다.

* **플래그 이유 목록**

   선택하면 구성원이 드롭다운 목록에서 주석을 부적절한 것으로 플래그를 지정하는 이유를 선택할 수 있습니다. 기본값은 선택 해제되어 있습니다.

* **사용자 지정 플래그 이유**

   선택하면 구성원이 주석을 부적절한 것으로 플래그 지정한 이유를 직접 입력할 수 있습니다. 기본값은 선택 해제되어 있습니다.

* **관리 임계값**

   댓글에 구성원이 플래그를 지정해야 중재자에게 알림이 표시되는 횟수를 입력합니다. 기본값은 1회입니다.

* **플래그 지정 제한**

   공개 보기에서 숨겨지기 전에 댓글에 플래그를 지정해야 하는 횟수를 입력합니다. 이 숫자는 보다 크거나 같아야 합니다. **중재 임계값**. 기본값은 5입니다.

#### 정렬 설정 탭 {#sort-settings-tab}

아래 **정렬 설정** 탭에서는 표시된 게시한 댓글을 어떻게 정렬할지 지정합니다.

* **정렬 필드**

   아래로 끌어서 다음 중 하나를 선택합니다. `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed`, 또는 `Most Liked`.

* **정렬 순서**

   아래로 끌어서 다음 중 하나를 선택합니다. `Ascending` 또는 `Descending`.

### 사용자 지정 주석 유형으로 변경 {#changing-to-a-custom-comment-type}

주석 리소스 유형을 변경하면 주석 시스템은 더 이상 기본값을 사용하여 주석 인스턴스를 생성하지 않고 개발자가 사용자 지정(확장)한 주석 인스턴스를 생성합니다.

사용자 지정 리소스 유형을 알고 나면 [디자인 모드](/help/sites-authoring/default-components-designmode.md) 배치된 을 두 번 클릭합니다. `Comments` 추가 탭이 있는 대화 상자를 여는 구성 요소입니다.

아래 **리소스 유형** 탭에서 새 인스턴스의 사용자 지정 resourceType을 `Comments or Voting` 구성 요소:

![리소스 유형](assets/resource-type.png)

* **댓글 리소스 유형**

   확장의 resourceType으로 이동 `comment` /apps의 구성 요소(단일 댓글)입니다. 예, `/apps/social/commons/components/hbs/comments/comment`

   이 리소스는 방문자가 댓글을 게시할 때 생성된 UGC의 resourceType을 식별합니다.

* **투표 리소스 유형**

   확장의 resourceType으로 이동 `voting` /apps의 구성 요소입니다. 예, `/apps/social/components/hbs/voting`

   이 리소스는 방문자가 투표를 게시할 때 만든 UGC의 리소스 유형을 식별합니다.

* **주석 시스템 리소스 유형**

   확장의 resourceType으로 이동 `comments`/apps의 구성 요소(댓글 시스템). 페이지 템플릿이 아니면 비워 둡니다. [동적으로 포함](/help/communities/scf.md#add-or-include-a-communities-component) 페이지에 리소스(댓글 노드)로 추가되지 않고 기본 스크립트의 댓글 시스템. 자세한 내용은 다음을 참조하십시오. [{{include}} 도우미](/help/communities/handlebars-helpers.md#include).

### 사이트 방문자 경험 {#site-visitor-experience}

#### 중재자 및 관리자 {#moderators-and-administrators}

로그인한 사용자에게 중재자 또는 관리자 권한이 있는 경우 댓글을 작성한 사람에 관계없이 구성 요소의 구성에서 허용하는 중재 작업을 수행할 수 있습니다.

#### 구성원 {#members}

사이트 방문자가 로그인한 경우 구성에 따라 다를 수 있습니다

* 새 댓글 게시
* 자신의 댓글 편집
* 자신의 댓글 삭제
* 다른 사람의 의견에 플래그 지정

#### 익명 {#anonymous}

로그인하지 않은 사이트 방문자는 게시된 댓글만 읽고 지원되는 경우 번역할 수 있지만 댓글을 추가하거나 다른 사람의 댓글에 플래그를 지정할 수는 없습니다.

### 추가 정보 {#additional-information}

자세한 내용은 [댓글 기본 사항](/help/communities/essentials-comments.md) 개발자용 페이지입니다.

게시한 댓글의 중재에 대해서는 [사용자 생성 컨텐츠 중재](/help/communities/moderate-ugc.md).

게시된 댓글의 번역은 다음을 참조하십시오. [사용자 생성 콘텐츠 번역](/help/communities/translate-ugc.md).
