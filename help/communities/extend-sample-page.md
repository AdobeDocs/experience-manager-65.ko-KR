---
title: 샘플 페이지에 주석 추가
seo-title: 샘플 페이지에 주석 추가
description: 페이지에 사용자 지정 주석 추가
seo-description: 페이지에 사용자 지정 주석 추가
uuid: ab258960-6de2-4943-80a7-e72904c0fd8e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a5040371-3bc2-43bc-a103-7175c4c6252d
docset: aem65
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# 샘플 페이지에 주석 추가 {#add-comment-to-sample-page}

사용자 정의 주석 시스템의 구성 요소가 응용 프로그램 디렉토리(/apps)에 배치되었으므로 확장 구성 요소를 사용할 수 있습니다. 영향을 받을 웹 사이트의 주석 시스템 인스턴스는 resourceType을 사용자 지정 주석 시스템으로 설정하고 필요한 모든 클라이언트 라이브러리를 포함해야 합니다.

## 필수 클라이언트 식별 {#identify-required-clientlibs}

기본 댓글의 스타일 및 기능에 필요한 클라이언트 라이브러리는 확장된 댓글에도 필요합니다.

커뮤니티 구성 [요소 안내서는](/help/communities/components-guide.md) 필요한 클라이언트 라이브러리를 식별합니다. 구성 요소 안내서로 이동하여 주석 구성 요소를 봅니다. 예:

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

주석을 렌더링하고 제대로 작동하려면 세 개의 클라이언트 라이브러리를 확인하십시오. 확장된 주석을 참조하고 [확장된 댓글 클라이언트 라이브러리](/help/communities/extend-create-components.md#create-a-client-library-folder) `apps.custom.comments`()를 참조해야 합니다.

![chlimage_1-79](assets/chlimage_1-79.png)

### 페이지에 사용자 정의 주석 추가 {#add-custom-comments-to-a-page}

페이지당 하나의 주석 시스템만 있을 수 있으므로 짧은 샘플 페이지 만들기 [자습서에 설명된 대로 샘플 페이지를 만드는 것이](/help/communities/create-sample-page.md) 쉽습니다.

구성 요소가 만들어지면 디자인 모드로 전환하고 사용자 지정 구성 요소 그룹을 사용하여 페이지에 `Alt Comments` 구성 요소를 추가할 수 있습니다.

주석이 제대로 표시되고 작동하려면, 댓글용 클라이언트 라이브러리를 페이지의 clientlibslist에 추가해야 합니다(커뮤니티 구성 요소의 [클라이언트 라이브러리 참조](/help/communities/clientlibs.md)).

#### 샘플 페이지의 댓글 클라이언트 {#comments-clientlibs-on-sample-page}

![샘플 페이지의 댓글 클라이언트](assets/chlimage_1-80.png)

#### 작성자:샘플 페이지의 대체 주석 {#author-alt-comment-on-sample-page}

![샘플 페이지의 대체 주석](assets/chlimage_1-81.png)

#### 작성자:샘플 페이지 주석 노드 {#author-sample-page-comments-node}

의 샘플 페이지에 대한 주석 노드의 속성을 확인하여 CRXDE에서 resourceType을 확인할 수 `/content/sites/sample/en/jcr:content/content/primary/comments`있습니다.

![chlimage_1-82](assets/chlimage_1-82.png)

#### 게시 샘플 페이지 {#publish-sample-page}

사용자 지정 구성 요소가 페이지에 추가되면 페이지를 [게시해야](/help/communities/sites-console.md#publishing-the-site)합니다.

#### 게시:샘플 페이지의 대체 주석 {#publish-alt-comment-on-sample-page}

사용자 지정 응용 프로그램과 샘플 페이지를 모두 게시한 후 주석을 입력할 수 있습니다. 데모 사용자 [](/help/communities/tutorials.md#demo-users) 또는 관리자를 사용하여 로그인하면 댓글을 게시할 수 있습니다.

다음은 aaron.mcdonald@mailinator.com댓글 게시입니다.

![chlimage_1-83](assets/chlimage_1-83.png)![chlimage_1-84](assets/chlimage_1-84.png)

확장 구성 요소가 기본 모양으로 올바르게 작동하므로 이제 모양을 수정할 때입니다.