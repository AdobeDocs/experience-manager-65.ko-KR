---
title: 샘플 페이지에 주석 추가
seo-title: 샘플 페이지에 주석 추가
description: 페이지에 사용자 지정 댓글 추가
seo-description: 페이지에 사용자 지정 댓글 추가
uuid: ab258960-6de2-4943-80a7-e72904c0fd8e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a5040371-3bc2-43bc-a103-7175c4c6252d
docset: aem65
exl-id: d4295a77-b931-4bc8-b3b4-eec42fdcfc56
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# 샘플 페이지에 주석 추가 {#add-comment-to-sample-page}

사용자 지정 주석 시스템의 구성 요소가 애플리케이션 디렉토리(/apps)에 배치되었으므로 확장 구성 요소를 사용할 수 있습니다. 영향을 받을 웹 사이트의 주석 시스템 인스턴스는 resourceType을 사용자 지정 주석 시스템으로 설정하고 필요한 모든 클라이언트 라이브러리를 포함해야 합니다.

## 필요한 Clientlibs 식별 {#identify-required-clientlibs}

확장 주석에는 기본 댓글의 스타일 및 기능에 필요한 클라이언트 라이브러리도 필요합니다.

[커뮤니티 구성 요소 안내서](/help/communities/components-guide.md)는 필요한 클라이언트 라이브러리를 식별합니다. 구성 요소 안내서 로 이동하여 설명 구성 요소를 확인합니다. 예를 들면 다음과 같습니다.

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

주석이 렌더링되고 제대로 작동하는 데 필요한 세 개의 클라이언트 라이브러리를 확인합니다. 확장 주석이 참조되는 위치와 [확장된 Comments&#39; 클라이언트 라이브러리](/help/communities/extend-create-components.md#create-a-client-library-folder)( `apps.custom.comments`)가 참조되는 위치에 이러한 설명을 포함해야 합니다.

![comments-component1](assets/comments-component1.png)

### 페이지에 사용자 지정 댓글 추가 {#add-custom-comments-to-a-page}

페이지당 주석 시스템은 하나만 있을 수 있으므로 짧은 [샘플 페이지 만들기](/help/communities/create-sample-page.md) 자습서에 설명된 대로 샘플 페이지를 만드는 것이 더 쉽습니다.

만들어진 후에는 디자인 모드로 전환하고 사용자 지정 구성 요소 그룹을 사용하여 `Alt Comments` 구성 요소를 페이지에 추가할 수 있도록 합니다.

주석이 표시되고 제대로 작동하려면 주석용 클라이언트 라이브러리를 페이지의 clientlibslist에 추가해야 합니다([Clientlibs for Communities Components](/help/communities/clientlibs.md) 참조).

#### 샘플 페이지 {#comments-clientlibs-on-sample-page}의 댓글 Clientlibs

![comments-clientlibs-crxde](assets/comments-clientlibs-crxde.png)

#### 작성자:샘플 페이지에 대한 대체 주석 {#author-alt-comment-on-sample-page}

![alt-comment](assets/alt-comment.png)

#### 작성자:샘플 페이지 주석 노드 {#author-sample-page-comments-node}

`/content/sites/sample/en/jcr:content/content/primary/comments`에서 샘플 페이지에 대한 주석 노드의 속성을 보고 CRXDE에서 resourceType을 확인할 수 있습니다.

![verify-comment-crxde](assets/verify-comment-crxde.png)

#### 샘플 페이지 게시 {#publish-sample-page}

사용자 지정 구성 요소가 페이지에 추가되면 (re) [페이지를 게시](/help/communities/sites-console.md#publishing-the-site)해야 합니다.

#### 게시:샘플 페이지에 대한 대체 주석 {#publish-alt-comment-on-sample-page}

사용자 지정 응용 프로그램과 샘플 페이지를 모두 게시한 후 주석을 입력할 수 있습니다. [데모 사용자](/help/communities/tutorials.md#demo-users) 또는 관리자로 로그인하면 주석을 게시할 수 있습니다.

다음은 aaron.mcdonald@mailinator.com 댓글 게시입니다.

![publish-alt-comment](assets/publish-alt-comment.png)

![publish-alt-comment1](assets/publish-alt-comment1.png)

확장 구성 요소가 기본 모양에서 올바르게 작동하므로 이제 모양을 수정할 차례입니다.
