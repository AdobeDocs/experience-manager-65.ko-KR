---
title: 컨텍스트 내 중재
seo-title: 컨텍스트 내 중재
description: 중재자 작업을 수행하는 방법
seo-description: 중재자 작업을 수행하는 방법
uuid: 282a8bea-2822-4e5c-b9f4-4d9a5380d895
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ee104f6f-123b-4a6e-9031-849fc1318cc5
role: Administrator
exl-id: 47b3c19c-5228-4b72-b78c-7ed71b308921
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 1%

---

# 컨텍스트 내 중재 {#in-context-moderation}

AEM Communities의 경우 커뮤니티 컨텐츠가 게시된 페이지에서 바로 관리자 및 신뢰할 수 있는 커뮤니티 구성원이 조정을 수행할 수 있습니다.

[중재 콘솔](moderation.md)을 사용하는 경우, 컨텐츠에 대해 표시되는 정보에는 게시된 페이지에 대한 링크가 포함되어 있어 컨텍스트 내에서 중재할 때 사용할 수 있는 추가 중재 작업에 액세스할 수 있습니다.

## 중재 작업 {#moderation-actions}

중재 개요([중재 작업](moderate-ugc.md#moderation-actions)에 대한 설명)를 방문하십시오.

## 중재 UI {#moderation-ui}

게시 인스턴스의 조정자에게 표시되는 UI는 UGC(사용자 생성 컨텐츠)를 게시하고 관리하기 위한 대화 상자에 포함되어 있습니다. UI의 요소는 사이트 방문자의 상태에 따라 결정됩니다.

1. 컨텐츠를 게시한 멤버입니다.
1. 신뢰할 수 있는 멤버 조정자입니다.
1. 관리자
1. 로그인되었지만 관리자, 중재자 및 컨텐츠 작성자가 아닙니다.
1. 로그인하지 않았습니다.

## 예 {#example}

[AEM Communities 시작하기](getting-started.md)에 생성된 [Geometrixx Engage](http://localhost:4503/content/sites/engage/en.html) 사이트를 사용하면 아래에서 보듯이 게시 환경에서 다양한 중재 활동을 수행할 포럼의 스레드를 빠르게 설정할 수 있습니다.

Aaron McDonald (aaron.mcdonald@mailinator.com)은 사이트를 만들 때 커뮤니티 참여 중재자 그룹에 추가하여 신뢰할 수 있는 커뮤니티 구성원으로 식별되었습니다.

Rebekah Larsen(rebekah.larsen@trashymail.com)은 [구성원 콘솔](members.md)을 사용하여 community-engage-members 그룹의 구성원으로 추가할 수 있습니다.

커뮤니티 사용자 그룹에 대한 자세한 내용은 [사용자 및 사용자 그룹 관리](users.md)를 참조하십시오.

### 포럼 게시물 {#create-the-forum-posts} 만들기

* Rebekah Larsen으로 로그인(rebekah.larsen@trashymail.com)

   * 포럼 선택
   * 새 게시물 선택
   * 제목 입력

      Humming Bird Feeder의 꿀을 변경하는 시기

   * 본문 입력

      나는 벌새 공급기를 매년 매기는데 성공하지 못했다. 하루나 이틀 후에 온 것 같은데, 그게 다예요. 일주일에 한 번 변경하는데 너무 긴 가요? 더 빨리 바꿔야 하나요?

   * 게시물 선택
   * 로그아웃 선택

* Aaron McDonald로 로그인(aaron.mcdonald@mailinator.com)

   * 포럼 선택
   * Hummingbird 주제에 대해 자세히 읽기를 선택합니다
   * 답글을 게시할 댓글 입력

      일주일에 한 번 갈아입고 5월부터 10월까지 받습니다

   * 회신 선택
   * 로그아웃 선택

* 앤드류 쉐퍼로 로그인(andrew.schaeffer@trashymail.com)

   * 포럼 선택
   * Hummingbird 주제에 대해 자세히 읽기를 선택합니다
   * 답글을 게시할 댓글 입력

      나는 꿀과 피드를 판다 - https://my.viral.url/을 방문해라

   * 회신 선택
   * 로그아웃 선택

### 익명 사이트 방문자(#5) {#anonymous-site-visitor}

다음은 (5)에서 로그인하지 않은 사이트 방문자가 보는 포럼 보기입니다.

익명 사이트 방문자는 포럼만 볼 수 있지만 콘텐츠를 게시하거나 중재 작업을 수행하지 않습니다.

![community-forum-visitor](assets/community-forum-visitor.png)

### 새 멤버(#4) {#new-member}

작성자는 관리자로 로그인하고 [구성원 콘솔](members.md)을 사용하여 커뮤니티 참여 구성원 그룹의 새 구성원으로 Boyd Larsen(boyd.larsen@dodgit.com)을 추가한 다음 로그아웃하십시오.

게시 시 Boyd Larsen으로 로그인하고 `Forum` 을 선택한 다음 Hummingbird 게시물에 대해 `Read more` 을 선택하여 스레드에 액세스합니다.

알림:

* 보이드는 포럼에 참석하지 않았다.
* Body는 아무 것도 삭제할 수 없습니다.
* Boyd가 로그인되어 있고 회신 또는 플래그 콘텐츠를 지정할 수 있습니다.

Andrew가 게시한 컨텐츠에 플래그를 지정하려면 Boyd를 선택합니다.

로그아웃

![community-forum-member](assets/community-forum-member.png)

### 관리자(#3) {#administrator}

관리자(관리자)로 로그인하고 포럼을 선택한 다음 게시물에 대해 자세히 읽기를 선택하여 스레드에 액세스합니다.

알림:

* 관리자는 플래그 지정, 삭제, 편집, 거부, 잘라내기, 닫기, 고정, 기능을 지정할 수 있습니다.
* 관리자는 관리를 선택하여 관리 콘솔에 액세스할 수 있습니다.

![community-admin-forum](assets/community-admin-forum.png)

관리 메뉴 항목을 선택하여 게시 환경에서 [중재 콘솔](moderation.md)에 액세스합니다.

관리자는 Geometrixx 참여 커뮤니티 사이트의 컨텐츠뿐만 아니라 모든 중재 가능한 컨텐츠가 표시됩니다.

검색 필터는 열기 또는 닫기를 전환하는 사이드 패널입니다.

로그아웃.

![moderation-console-publish](assets/moderation-console-publish.png)

### 커뮤니티 중재자(#2) {#community-moderator}

커뮤니티 중재자인 Aaron McDonald(aaron.mcdonal@mailinator.com)으로 로그인하고 포럼을 선택하여 스레드에 액세스한 다음 벌새 게시물에 대해 자세히 알아보십시오.

알림:

* Aaron은 자신의 글을 회신, 삭제, 편집 또는 거부할 수 있습니다.
* Aaron은 다른 컨텐츠에 플래그 지정/허용, 회신, 삭제, 편집, 거부 할 수도 있습니다.
* 아론은 포럼 주제를 잘라서 자신이 온건한 포럼으로 옮길 수 있다.
* Aaron은 관리 를 선택하여 중재 콘솔에 액세스할 수 있습니다.

![커뮤니티 포럼-중재자](assets/community-forum-moderator.png)

관리 메뉴 항목을 선택하여 게시 환경에서 [중재 콘솔](moderation.md)에 액세스합니다.

커뮤니티 중재자의 경우 Geometrixx Engage 커뮤니티 사이트의 중재 가능한 컨텐츠만 표시됩니다.

커뮤니티 중재자에게는 관리자와 동일한 옵션이 있지만(이미지는 검색 사이드바가 닫혀 있음), 다른 AEM 콘솔에 액세스할 수 없습니다.

로그아웃.

![중재자 액세스](assets/moderator-access.png)

### 컨텐츠 작성자(#1) {#content-author}

스레드를 시작한 커뮤니티 멤버인 Rebekah Larsen(rebekah.larsen@mailinator.com)으로 로그인하고 포럼을 선택하여 스레드에 액세스한 다음 벌새 게시물에 대해 자세히 알아보십시오.

알림:

* Rebekah는 자신의 게시물을 삭제하거나 편집할 수 있습니다.
* 또한 Rebekah는 다른 컨텐츠에 회신 또는 플래그를 지정할 수도 있습니다.
* 중재 콘솔에 액세스할 수 없습니다.

![community-forum-author](assets/community-forum-author.png)
