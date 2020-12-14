---
title: 주석 사용
seo-title: 주석 사용
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


# 주석 사용 {#using-comments}

## 소개 {#introduction}

댓글 기능은 로그인한 사이트 방문자(구성원)가 사이트의 컨텐츠에 대한 자신의 의견과 지식을 공유할 수 있도록 하는 데 사용됩니다. 이 기능은 다른 기능에는 이미 있지만 웹 사이트에 추가할 수 있습니다.

이 문서에서는 다음 사항에 대해 설명합니다.

* 페이지에 `Comments` 추가
* `Comments` 구성 요소에 대한 구성 설정입니다.

>[!NOTE]
>
>댓글의 익명 게시는 지원되지 않습니다. 사이트 방문자는 등록을 하고(회원이 됨) 로그인해야 참여합니다.

### 페이지에 주석 추가 {#adding-comments-to-a-page}

작성 모드에서 페이지에 `Comments` 구성 요소를 추가하려면 구성 요소 브라우저를 사용하여

* `Communities / Comments`

주석을 달 기능을 기준으로 하는 위치 등 페이지 맨 아래에 있는 위치와 같은 위치로 드래그합니다.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](/help/communities/basics.md)을 방문하십시오.

[필수 클라이언트측 라이브러리](/help/communities/essentials-comments.md#essentials-for-client-side)가 포함되어 있는 경우 이 방법으로 `Comments` 구성 요소가 표시됩니다.

![comments-component](assets/comments-component.png)

>[!NOTE]
>
>페이지에 하나의 `Comments` 구성 요소만 있을 수 있습니다. 블로그, 일정, 포럼, QnA 및 검토와 같은 여러 커뮤니티 기능에는 이미 댓글이 포함되어 있습니다.

### 주석 구성 {#configuring-comments}

액세스할 배치된 `Comments` 구성 요소를 선택하고 편집 대화 상자를 여는 `Configure` 아이콘을 선택합니다.

![아이콘 구성](assets/configure.png)

![주석 설정](assets/commentssettings.png)

#### 주석 탭 {#comments-tab}

**주석** 탭에서 방문자가 주석을 입력하는 방법을 지정합니다.

* **답글 허용**

   이 확인란을 선택하면 구성원이 기존 댓글에 답글을 달 수 있습니다. 기본값은 선택 취소입니다.

* **페이지당 댓글**

   페이지당 표시되는 댓글 수와 표시된 답글 수를 제한합니다. 기본값은 10입니다.

* **파일 업로드 허용**

   이 확인란을 선택하면 파일 업로드 옵션이 텍스트 입력 상자로 표시됩니다. 기본값은 선택 취소입니다.

* **최대 파일 크기**

   파일 업로드 허용이 선택된 경우에만 관련성이 있습니다. 이 값은 업로드된 파일 크기를 제한합니다. 기본 제한은 10MB입니다.

* **최대 메시지 길이**

   텍스트 상자에 입력할 수 있는 최대 문자 수입니다. 기본값은 4096자입니다.

* **허용되는 파일 유형**

   파일 업로드 허용이 선택된 경우에만 관련성이 있습니다. &quot;점&quot; 구분 기호가 있는 파일 이름 확장명의 쉼표로 구분된 목록입니다. 예:.jpg, .jpeg, .png, .doc, .docx, .pdf 파일 형식을 지정하면 지정되지 않은 파일 형식을 사용할 수 없습니다. 모든 파일 형식을 사용할 수 있도록 기본값이 지정되지 않았습니다.

* **리치 텍스트 편집기**

   이 옵션이 선택되어 있으면 마크업이 적용된 주석이 입력됩니다. 기본값은 선택 취소입니다.

* **투표 허용**

   이 확인란을 선택하면 텍스트 입력 상자가 표시됩니다. 기본값은 선택 취소입니다.

* **다음 허용**

   이 확인란을 선택하면 구성원이 주석을 따르도록 할 수 있습니다. 기본값은 선택 취소입니다.

* **배지 표시**

   이 확인란을 선택하면 획득 배지와 수여된 배지가 표시됩니다. 기본값은 선택 취소입니다.

#### 사용자 중재 탭 {#user-moderation-tab}

**사용자 중재** 탭에서 게시된 댓글이 관리되는 방식을 지정합니다. 자세한 내용은 [사용자 생성 콘텐츠 중재](/help/communities/moderate-ugc.md)를 참조하십시오.

* **사전 관리**

   이 확인란을 선택하면 댓글이 게시 사이트에 표시되기 전에 승인되어야 합니다. 기본값은 선택 취소입니다.

* **댓글 삭제**

   이 확인란을 선택하면 해당 댓글을 게시한 구성원이 댓글을 삭제할 수 있습니다. 기본값은 선택 취소입니다.

* **댓글 거부**

   이 확인란을 선택하면 중재자가 댓글을 거부할 수 있습니다. 기본값은 선택 취소입니다.

* **댓글 닫기 / 다시 열기**

   이 확인란을 선택하면 중재자가 댓글을 닫고 다시 열 수 있습니다. 기본값은 선택 취소입니다.

* **댓글에 플래그 지정**

   이 확인란을 선택하면 구성원이 댓글에 부적절한 표시를 할 수 있습니다. 기본값은 선택 취소입니다.

* **플래그 이유 목록**

   이 확인란을 선택하면 멤버가 드롭다운 목록에서 선택할 수 있습니다. 이는 댓글에 부적절한 이유가 됩니다. 기본값은 선택 취소입니다.

* **사용자 지정 플래그 이유**

   이 확인란을 선택하면 구성원이 댓글에 부적절한 이유가 표시되도록 할 수 있습니다. 기본값은 선택 취소입니다.

* **관리 임계값**

   중재자에게 알림을 보내기 전에 구성원이 댓글에 플래그를 지정해야 하는 횟수를 입력합니다. 기본값은 한 번(1)입니다.

* **플래그 제한**

   공개 보기에서 주석을 숨기려면 먼저 플래그가 달린 횟수를 입력합니다. 이 숫자는 **중재 임계값**&#x200B;보다 크거나 같아야 합니다. 기본값은 5입니다.

#### 정렬 설정 탭 {#sort-settings-tab}

**정렬 설정** 탭에서 게시된 주석이 표시될 때 정렬되는 방법을 지정합니다.

* **정렬 필드**

   아래로 끌어 `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed` 또는 `Most Liked` 중 하나를 선택합니다.

* **정렬 순서**

   아래로 끌어 `Ascending` 또는 `Descending` 중 하나를 선택합니다.

### 사용자 지정 주석 유형 {#changing-to-a-custom-comment-type}으로 변경

주석 리소스 유형을 변경하면 주석 시스템은 더 이상 기본값을 사용하여 주석 인스턴스를 생성하지 않고 개발자가 사용자 정의(확장)한 주석 인스턴스가 생성됩니다.

사용자 지정 리소스 유형이 알려지면 [디자인 모드](/help/sites-authoring/default-components-designmode.md)를 입력하고 배치된 `Comments` 구성 요소를 두 번 클릭하여 추가 탭이 있는 대화 상자를 엽니다.

**리소스 유형** 탭에서 `Comments or Voting` 구성 요소의 새 인스턴스에 대한 사용자 지정 resourceType을 지정합니다.

![resource-type](assets/resource-type.png)

* **댓글 리소스 유형**

   /apps에서 확장 `comment` 구성 요소(단일 주석)의 resourceType으로 이동합니다. 예, `/apps/social/commons/components/hbs/comments/comment`

   이 리소스는 방문자가 댓글을 게시할 때 생성된 UGC의 resourceType을 식별합니다.

* **투표 리소스 유형**

   /apps에서 확장 `voting` 구성 요소의 resourceType으로 이동합니다. 예, `/apps/social/components/hbs/voting`

   이 리소스는 방문자가 투표를 게시할 때 만든 UGC의 리소스 유형을 식별합니다.

* **주석 시스템 리소스 유형**

   /apps에서 확장 `comments`구성 요소(주석 시스템)의 resourceType으로 이동합니다. 페이지 템플릿 [에 리소스(주석 노드)로 페이지에 추가되지 않고 기본 스크립트에 댓글 시스템(](/help/communities/scf.md#add-or-include-a-communities-component))이 동적으로 포함되어 있지 않으면 비워 둡니다. [{{include}} helper](/help/communities/handlebars-helpers.md#include)에 대한 자세한 내용을 참조하십시오.

### 사이트 방문자 경험 {#site-visitor-experience}

#### 중재자 및 관리자 {#moderators-and-administrators}

로그인한 사용자에게 중재자 또는 관리자 권한이 있으면 댓글을 작성한 사람에 관계없이 구성 요소의 구성에서 허용하는 중재 작업을 수행할 수 있습니다.

#### 구성원 {#members}

사이트 방문자가 로그인하면 구성에 따라 사이트 방문자가 로그인할 수 있습니다.

* 새 주석 게시
* 자신의 주석 편집
* 자신의 주석 삭제
* 다른 사람의 주석 플래그 지정

#### 익명 {#anonymous}

로그인하지 않은 사이트 방문자는 게시된 댓글만 읽고, 지원되는 경우 번역할 수 있지만 주석을 추가하거나 다른 사람의 댓글에 플래그를 지정할 수는 없습니다.

### 추가 정보 {#additional-information}

개발자를 위한 [Comments Essentials](/help/communities/essentials-comments.md) 페이지에 자세한 정보가 있을 수 있습니다.

게시된 댓글의 중재는 [사용자 생성 컨텐트 중재](/help/communities/moderate-ugc.md)를 참조하십시오.

게시된 댓글의 번역에 대해서는 [사용자 생성 컨텐트 번역](/help/communities/translate-ugc.md)을 참조하십시오.
