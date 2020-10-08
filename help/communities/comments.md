---
title: 댓글 사용
seo-title: 댓글 사용
description: 댓글 기능을 사용하면 로그인한 사이트 방문자가 자신의 의견과 지식을 공유할 수 있습니다
seo-description: 댓글 기능을 사용하면 로그인한 사이트 방문자가 자신의 의견과 지식을 공유할 수 있습니다
uuid: 40acd962-846c-483c-b789-aab3a7d2b31b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 216cfb3e-777e-4773-afba-749debdca000
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 5%

---


# 댓글 사용 {#using-comments}

## 소개 {#introduction}

댓글 기능은 로그인 사이트 방문자(구성원)가 사이트의 컨텐츠에 대한 자신의 의견과 지식을 공유할 수 있도록 하는 데 사용됩니다. 이 기능은 다른 기능에는 이미 있지만 웹 사이트에 추가할 수 있습니다.

이 문서에서는 다음 사항에 대해 설명합니다.

* 페이지 `Comments` 에 추가.
* 구성 요소의 구성 `Comments` 설정.

>[!NOTE]
>
>댓글의 익명 게시는 지원되지 않습니다. 사이트 방문자는 등록(회원이 되기)하고 로그인해야 참여합니다.

### 페이지에 주석 추가 {#adding-comments-to-a-page}

작성 모드에서 페이지에 `Comments` 구성 요소를 추가하려면 구성 요소 브라우저를 사용하여

* `Communities / Comments`

사용자가 주석을 달 수 있는 기능과 관련된 위치 또는 페이지 하단에 있는 위치와 같이 페이지에 드래그합니다.

필요한 정보를 보려면 커뮤니티 구성 요소 [기본 사항을 방문하십시오](/help/communities/basics.md).

필요한 [클라이언트측 라이브러리가](/help/communities/essentials-comments.md#essentials-for-client-side) 포함된 경우 구성 요소가 표시되는 `Comments` 방식입니다.

![comments-component](assets/comments-component.png)

>[!NOTE]
>
>한 페이지에 하나의 `Comments` 구성 요소만 있을 수 있습니다. 블로그, 일정, 포럼, QnA 및 검토와 같은 여러 커뮤니티 기능에는 이미 댓글이 포함되어 있습니다.

### 주석 구성 {#configuring-comments}

액세스할 배치된 `Comments` 구성 요소를 선택하고 편집 대화 상자를 여는 `Configure` 아이콘을 선택합니다.

![구성 아이콘](assets/configure.png)

![댓글 설정](assets/commentssettings.png)

#### 댓글 탭 {#comments-tab}

댓글 **탭** 아래에서 방문자가 댓글을 입력하는 방법을 지정합니다.

* **답글 허용**

   이 확인란을 선택하면 구성원이 기존 주석에 응답할 수 있습니다. 기본값은 선택 취소입니다.

* **페이지당 댓글**

   페이지당 표시되는 댓글 수와 표시된 답글 수를 제한합니다. 기본값은 10입니다.

* **파일 업로드 허용**

   이 확인란을 선택하면 파일 업로드 옵션이 텍스트 입력 상자로 표시됩니다. 기본값은 선택 취소입니다.

* **최대 파일 크기**

   파일 업로드 허용이 선택된 경우에만 관련성이 있습니다. 이 값은 업로드된 파일 크기를 제한합니다. 기본 제한은 10MB입니다.

* **최대 메시지 길이**

   텍스트 상자에 입력할 수 있는 최대 문자 수입니다. 기본값은 4096자입니다.

* **허용되는 파일 유형**

   파일 업로드 허용이 선택된 경우에만 관련성이 있습니다. &quot;점&quot; 구분 기호가 있는 파일 이름 확장자의 쉼표로 구분된 목록입니다. 예:.jpg, .jpeg, .png, .doc, .docx, .pdf. 파일 형식을 지정한 경우 지정되지 않은 파일 형식을 사용할 수 없습니다. 모든 파일 유형이 허용되도록 기본값이 지정되지 않았습니다.

* **리치 텍스트 편집기**

   이 확인란을 선택하면 마크업에 댓글이 입력됩니다. 기본값은 선택 취소입니다.

* **투표 허용**

   이 확인란을 선택하면 위 또는 아래 투표 옵션이 텍스트 입력 상자로 표시됩니다. 기본값은 선택 취소입니다.

* **다음 허용**

   이 확인란을 선택하면 구성원이 댓글을 달 수 있습니다. 기본값은 선택 취소입니다.

* **배지 표시**

   이 확인란을 선택하면 획득 배지와 수여된 배지가 표시됩니다. 기본값은 선택 취소입니다.

#### 사용자 중재 탭 {#user-moderation-tab}

사용자 중재 **탭** 아래에서 게시된 댓글이 관리되는 방식을 지정합니다. 자세한 내용은 사용자 생성 [컨텐츠 중재를 참조하십시오](/help/communities/moderate-ugc.md).

* **사전 관리**

   이 확인란을 선택하면 댓글이 게시 사이트에 표시되기 전에 승인되어야 합니다. 기본값은 선택 취소입니다.

* **댓글 삭제**

   이 확인란을 선택하면 댓글을 게시한 구성원이 댓글을 삭제할 수 있습니다. 기본값은 선택 취소입니다.

* **댓글 거부**

   이 확인란을 선택하면 중재자가 댓글을 거부할 수 있습니다. 기본값은 선택 취소입니다.

* **댓글 닫기 / 다시 열기**

   이 확인란을 선택하면 중재자가 댓글을 닫고 다시 열 수 있습니다. 기본값은 선택 취소입니다.

* **댓글에 플래그 지정**

   이 확인란을 선택하면 구성원이 댓글에 부적절한 표시를 할 수 있습니다. 기본값은 선택 취소입니다.

* **플래그 이유 목록**

   이 확인란을 선택하면 멤버가 드롭다운 목록에서 선택할 수 있습니다. 이는 댓글에 대한 플래그 지정이 부적절하다는 이유를 나타냅니다. 기본값은 선택 취소입니다.

* **사용자 지정 플래그 이유**

   이 확인란을 선택하면 구성원이 댓글에 대한 자신의 이유를 부적절한 것으로 입력할 수 있습니다. 기본값은 선택 취소입니다.

* **관리 임계값**

   중재자에게 알리기 전에 구성원이 댓글에 플래그를 지정해야 하는 횟수를 입력합니다. 기본값은 한 번(1)입니다.

* **플래그 지정 제한**

   댓글이 공개 보기에서 숨겨지기 전에 플래그가 달린 횟수를 입력합니다. 이 숫자는 중재 임계값보다 **크거나 같아야 합니다**. 기본값은 5입니다.

#### 정렬 설정 탭 {#sort-settings-tab}

정렬 설정 **탭** 아래에서, 표시할 때 게시된 댓글이 정렬되는 방식을 지정합니다.

* **정렬 필드**

   아래로 끌어 하나 `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed`또는 `Most Liked`.

* **정렬 순서**

   또는 중 하나를 선택하려면 아래로 `Ascending` 당기십시오 `Descending`.

### 사용자 지정 댓글 유형으로 변경 {#changing-to-a-custom-comment-type}

주석 리소스 유형을 변경하면 댓글 시스템에서 더 이상 기본값을 사용하여 주석 인스턴스를 생성하지 않고 개발자가 사용자 정의(확장)한 주석을 생성합니다.

사용자 지정 리소스 유형이 알려지면 [디자인 모드를](/help/sites-authoring/default-components-designmode.md) `Comments` 입력하고 배치된 구성 요소를 두 번 클릭하여 추가 탭이 있는 대화 상자를 엽니다.

리소스 **유형** 탭에서 구성 요소의 새 인스턴스에 대한 사용자 지정 resourceType을 `Comments or Voting` 지정합니다.

![resource-type](assets/resource-type.png)

* **댓글 리소스 유형**

   /apps의 확장 구성 요소(단일 주석)의 resourceType으로 `comment` 이동합니다. 예, `/apps/social/commons/components/hbs/comments/comment`

   이 리소스는 방문자가 댓글을 게시할 때 생성된 UGC의 resourceType을 식별합니다.

* **투표 리소스 유형**

   /apps의 확장 구성 `voting` 요소의 resourceType으로 이동합니다. 예, `/apps/social/components/hbs/voting`

   이 리소스는 방문자가 투표를 게시할 때 생성된 UGC의 리소스 유형을 식별합니다.

* **주석 시스템 리소스 유형**

   /apps에서 확장 `comments`구성 요소(댓글 시스템)의 resourceType으로 이동합니다. 페이지 템플릿에 리소스(주석 노드)로 페이지에 추가되지 않고 기본 스크립트에 주석 시스템이 [동적으로](/help/communities/scf.md#add-or-include-a-communities-component) 포함되지 않는 한 비워 둡니다. 자세한 내용은 [{{include}} 헬퍼에 대한 정보를 참조하십시오](/help/communities/handlebars-helpers.md#include).

### 사이트 방문자 경험 {#site-visitor-experience}

#### 중재자 및 관리자 {#moderators-and-administrators}

로그인한 사용자에게 중재자 또는 관리자 권한이 있으면 댓글을 작성한 사람에 관계없이 구성 요소의 구성에서 허용하는 중재 작업을 수행할 수 있습니다.

#### 구성원 {#members}

사이트 방문자가 로그인하면 구성에 따라 로그인할 수 있습니다

* 새 댓글 게시
* 자신의 주석 편집
* 자신의 주석 삭제
* 다른 사람의 주석 플래그 지정

#### 익명 {#anonymous}

로그인하지 않은 사이트 방문자는 게시된 댓글만 읽을 수 있고, 지원되는 경우 번역할 수 있으며, 댓글을 추가하거나 다른 사람의 주석에 플래그를 지정할 수는 없습니다.

### 추가 정보 {#additional-information}

개발자를 위한 주석 필수 [사항](/help/communities/essentials-comments.md) 페이지에는 자세한 정보가 나와 있습니다.

게시된 댓글의 중재를 보려면 사용자 생성 [컨텐트 중재를 참조하십시오](/help/communities/moderate-ugc.md).

게시된 댓글의 번역에 대해서는 사용자 생성 컨텐츠 [번역을 참조하십시오](/help/communities/translate-ugc.md).
