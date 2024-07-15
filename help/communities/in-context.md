---
title: 컨텍스트 내 중재
description: 관리자와 신뢰할 수 있는 커뮤니티 구성원이 Adobe Experience Manager 커뮤니티에서 중재자 작업을 수행하는 방법에 대해 알아봅니다.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 47b3c19c-5228-4b72-b78c-7ed71b308921
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# 컨텍스트 내 중재 {#in-context-moderation}

AEM Communities의 경우 커뮤니티 콘텐츠가 게시된 게시된 게시된 페이지에서 관리자 및 신뢰할 수 있는 커뮤니티 구성원이 직접 중재를 수행할 수 있습니다.

[중재 콘솔](moderation.md)을 사용하는 경우 콘텐츠에 표시되는 정보에는 컨텍스트 내에서 중재할 때 사용할 수 있는 추가 중재 작업에 액세스할 수 있도록 게시된 페이지에 대한 링크가 포함되어 있습니다.

## 중재 작업 {#moderation-actions}

[중재 동작](moderate-ugc.md#moderation-actions)에 대한 설명은 중재 개요를 참조하세요.

## 중재 UI {#moderation-ui}

게시 인스턴스에서 중재자에게 표시되는 UI는 UGC(사용자 생성 컨텐츠)를 게시 및 관리하기 위한 대화 상자에 포함되어 있습니다. UI의 요소는 사이트 방문자의 상태(상태 여부)에 따라 결정됩니다.

1. 콘텐츠를 게시한 멤버입니다.
1. 신뢰할 수 있는 구성원 중재자입니다.
1. 관리자.
1. 로그인되어 있지만 관리자, 중재자 또는 콘텐츠 작성자는 로그인되어 있지 않습니다.
1. 로그인되지 않았습니다.

## 예 {#example}

[AEM Communities을 시작](getting-started.md)할 때 만든 [Geometrixx 참여](http://localhost:4503/content/sites/engage/en.html) 사이트를 사용하면 포럼에서 스레드를 설정하여 Publish 환경에서 다양한 중재 활동을 경험할 수 있습니다. 아래를 참조하십시오.

Aaron McDonald(`aaron.mcdonald@mailinator.com`)가 사이트를 만들 때 커뮤니티 참여 중재자 그룹에 추가되어 신뢰할 수 있는 커뮤니티 구성원으로 확인되었습니다.

Rebekah Larsen(`rebekah.larsen@trashymail.com`)은 [구성원 콘솔](members.md)을 사용하여 커뮤니티 참여 구성원 그룹의 구성원으로 추가할 수 있습니다.

커뮤니티 사용자 그룹에 대한 자세한 내용은 [사용자 및 사용자 그룹 관리](users.md)를 참조하십시오.

### 포럼 게시물 만들기 {#create-the-forum-posts}

* Rebekah Larsen(rebekah.larsen@trashymail.com)으로 로그인

   * 포럼 선택
   * 새 Post 선택
   * 제목 입력

     Humming Bird Feeder에서 꿀을 교체하는 시기

   * 본문 입력

     나는 매년 벌새 먹이통을 매달아 놓았을 때 그다지 성공하지 못했다. 하루 이틀 오는 것 같은데 그게 다예요. 1주일에 한 번 바꾸면 너무 긴 건가요? 더 빨리 바꿔야 하나요?

   * Post 선택
   * 로그아웃 선택

* Aaron McDonald(aaron.mcdonald@mailinator.com)로 로그인합니다.

   * 포럼 선택
   * Hummingbird 주제에 대해 자세히 보기 를 선택합니다.
   * Post 회신에 대한 댓글 입력

     나는 일주일에 한 번 교체하고 5월부터 10월까지 받아.

   * 답변 선택
   * 로그아웃 선택

* Andrew Schaeffer(andrew.schaeffer@trashymail.com)로 로그인

   * 포럼 선택
   * Hummingbird 주제에 대해 자세히 보기 를 선택합니다.
   * Post 회신에 대한 댓글 입력

     나는 꿀과 피더를 판매합니다 - https://my.viral.url/ 방문

   * 답변 선택
   * 로그아웃 선택

### 익명 사이트 방문자(#5) {#anonymous-site-visitor}

다음은 (5)에 로그인하지 않은 사이트 방문자가 본 포럼의 보기입니다.

익명 사이트 방문자는 포럼을 볼 수만 있고 콘텐츠를 게시하거나 중재 작업을 수행할 수 없습니다.

![community-forum-visitor](assets/community-forum-visitor.png)

### 새 구성원(#4) {#new-member}

작성자의 경우 관리자로 로그인하고 [구성원 콘솔](members.md)을 사용하여 Boyd Larsen(boyd.larsen@dodgit.com)을 커뮤니티 참여 구성원 그룹의 새 구성원으로 추가한 다음 로그아웃합니다.

게시 시 Boyd Larsen으로 로그인하고 `Forum`을(를) 선택한 다음 벌새 게시물에 대해 `Read more`을(를) 선택하여 스레드에 액세스합니다.

알림:

* 보이드는 포럼에 참가하지 않았다.
* 보이드는 아무것도 삭제할 수 없습니다.
* Boid가 로그인되어 있고 콘텐츠를 회신하거나 플래그를 지정할 수 있습니다.

Boid가 Andrew가 게시한 콘텐츠에 플래그를 지정하려면 Flag를 선택합니다.

로그아웃

![커뮤니티 포럼 구성원](assets/community-forum-member.png)

### 관리자(#3) {#administrator}

관리자(관리자)로 로그인하고 포럼 을 선택하여 스레드에 액세스한 다음 게시물에 대해 자세히 읽어보십시오.

알림:

* 관리자는 플래그 지정, 삭제, 편집, 거부, 잘라내기, 닫기, 고정, 기능을 사용할 수 있습니다.
* 관리자는 관리 를 선택하여 중재 콘솔에 액세스할 수 있습니다.

![community-admin-forum](assets/community-admin-forum.png)

Publish 환경에서 [중재 콘솔](moderation.md)에 액세스할 수 있도록 관리 메뉴 항목을 선택하십시오.

관리자의 경우, Geometrixx 참여 커뮤니티 사이트의 콘텐츠뿐만 아니라 중재 가능한 모든 콘텐츠가 표시됩니다.

검색 필터는 열거나 닫는 사이드 패널입니다.

로그아웃.

![moderation-console-publish](assets/moderation-console-publish.png)

### 커뮤니티 중재자(#2) {#community-moderator}

커뮤니티 중재자인 Aaron McDonald(`aaron.mcdonal@mailinator.com`)로 로그인하고 포럼 을 선택하여 스레드에 액세스한 다음 벌새 게시물에 대해 자세히 읽어보십시오.

알림:

* Aaron은 자신의 게시물에 대해 답변, 삭제, 편집 또는 부인할 수 있습니다.
* Aaron은 다른 콘텐츠에 플래그 지정/허용, 회신, 삭제, 편집, 거부 등의 작업을 수행할 수도 있습니다.
* Aaron은 자신이 중재하는 다른 포럼으로 옮기기 위해 포럼 주제를 잘라낼 수 있다.
* Aaron은 관리 를 선택하여 중재 콘솔에 액세스할 수 있습니다.

![커뮤니티 포럼 중재자](assets/community-forum-moderator.png)

Publish 환경에서 [중재 콘솔](moderation.md)에 액세스할 수 있도록 관리 메뉴 항목을 선택하십시오.

커뮤니티 중재자의 경우 Geometrixx 참여 커뮤니티 사이트의 중재 가능한 콘텐츠만 표시됩니다.

커뮤니티 중재자에는 관리자와 동일한 옵션(이미지가 검색 사이드바를 닫은 상태로 전환됨)이 있지만 다른 AEM 콘솔에는 액세스할 수 없습니다.

로그아웃.

![중재자 액세스](assets/moderator-access.png)

### 콘텐츠 작성자(#1) {#content-author}

스레드를 시작한 커뮤니티 멤버인 Rebekah Larsen(`rebekah.larsen@mailinator.com`)으로 로그인하고 포럼 을 선택하여 스레드에 액세스한 다음 벌새 게시물에 대해 자세히 알아보십시오.

알림:

* 레베카는 자신의 게시물을 삭제하거나 편집할 수 있습니다.
* Rebekah는 다른 콘텐츠에 회신하거나 플래그를 지정할 수도 있습니다.
* 중재 콘솔에 액세스할 수 없습니다.

![커뮤니티 포럼 작성자](assets/community-forum-author.png)
