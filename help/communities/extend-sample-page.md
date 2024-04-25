---
title: 샘플 페이지에 주석 추가
description: 웹 사이트의 댓글 시스템 인스턴스가 리소스 유형을 사용자 지정 댓글 시스템으로 설정하고 필요한 모든 클라이언트 라이브러리를 포함하도록 설정하는 방법에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d4295a77-b931-4bc8-b3b4-eec42fdcfc56
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# 샘플 페이지에 주석 추가  {#add-comment-to-sample-page}

이제 사용자 지정 주석 시스템의 구성 요소가 애플리케이션 디렉터리(/apps)에 있으므로 확장된 구성 요소를 사용할 수 있습니다. 영향을 받는 웹 사이트의 댓글 시스템 인스턴스는 resourceType을 사용자 지정 댓글 시스템으로 설정하고 필요한 모든 클라이언트 라이브러리를 포함해야 합니다.

## 필요한 Clientlib 식별 {#identify-required-clientlibs}

기본 Comments의 스타일 및 기능에 필요한 클라이언트 라이브러리는 확장 Comments에도 필요합니다.

다음 [커뮤니티 구성 요소 안내서](/help/communities/components-guide.md) 는 필요한 클라이언트 라이브러리를 식별합니다. 구성 요소 안내서 로 이동하여 설명 구성 요소를 확인합니다. 예를 들면 다음과 같습니다.

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

주석이 렌더링되고 제대로 작동하는 데 필요한 세 개의 클라이언트 라이브러리를 확인합니다. 확장된 Comments를 참조하는 위치에 포함되어야 하며 [확장 주석의 클라이언트 라이브러리](/help/communities/extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`).

![comments-component1](assets/comments-component1.png)

### 페이지에 사용자 정의 주석 추가 {#add-custom-comments-to-a-page}

페이지당 하나의 주석 시스템만 있을 수 있으므로 간단한 설명에 따라 샘플 페이지를 만드는 것이 더 쉽습니다 [샘플 페이지 만들기](/help/communities/create-sample-page.md) 튜토리얼.

만들어지면 디자인 모드로 전환하고 사용자 지정 구성 요소 그룹을 사용하여 `Alt Comments` 페이지에 추가할 구성 요소입니다.

주석이 표시되고 제대로 작동하려면 주석의 클라이언트 라이브러리를 페이지의 clientlibslist에 추가해야 합니다( 참조) [커뮤니티 구성 요소에 대한 Clientlibs](/help/communities/clientlibs.md)).

#### 샘플 페이지의 설명 Clientlibs {#comments-clientlibs-on-sample-page}

![comments-clientlibs-crxde](assets/comments-clientlibs-crxde.png)

#### 작성자: 샘플 페이지에 대한 대체 댓글 {#author-alt-comment-on-sample-page}

![alt-주석](assets/alt-comment.png)

#### 작성자: 샘플 페이지 주석 노드 {#author-sample-page-comments-node}

다음 위치에서 샘플 페이지에 대한 설명 노드의 속성을 보고 CRXDE에서 resourceType을 확인할 수 있습니다. `/content/sites/sample/en/jcr:content/content/primary/comments`.

![verify-comment-crxde](assets/verify-comment-crxde.png)

#### 샘플 페이지 게시 {#publish-sample-page}

사용자 지정 구성 요소가 페이지에 추가되면 (재)해야 합니다 [페이지 게시](/help/communities/sites-console.md#publishing-the-site).

#### 게시: 샘플 페이지의 Alt 주석 {#publish-alt-comment-on-sample-page}

사용자 지정 응용 프로그램과 샘플 페이지를 모두 게시한 후 주석을 입력할 수 있습니다. 로그인할 때 다음 중 하나를 사용하여 [데모 사용자](/help/communities/tutorials.md#demo-users) 관리자 또는 댓글을 게시하는 것이 가능합니다.

여기 aaron.mcdonald@mailinator.com 댓글을 게시하는 것이 있습니다.

![publish-alt-comment](assets/publish-alt-comment.png)

![publish-alt-comment1](assets/publish-alt-comment1.png)

이제 확장 구성 요소가 기본 모양새에서 올바르게 작동하는 것처럼 보이므로 모양새를 수정해야 합니다.
