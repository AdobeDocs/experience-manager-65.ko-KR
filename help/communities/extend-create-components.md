---
title: 구성 요소 만들기
seo-title: 구성 요소 만들기
description: 주석 구성 요소 만들기
seo-description: 주석 구성 요소 만들기
uuid: ea6e00d4-1db7-40ef-ae49-9ec55df58adf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 83c4f18a-d7d6-4090-88c7-41a9075153b5
translation-type: tm+mt
source-git-commit: 230c700d87d82d248b7d0bbc45c69c5c2b0e3ff8
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 4%

---


# 구성 요소 만들기  {#create-the-components}

구성 요소 확장 예제는 두 구성 요소로 구성된 주석 시스템을 사용합니다

* 댓글 - 페이지에 배치된 구성 요소인 포함 주석 시스템입니다.
* 댓글 - 게시된 댓글의 인스턴스를 캡처하는 구성 요소입니다.

게시된 댓글의 모양을 사용자 정의하는 경우 두 구성 요소를 모두 배치해야 합니다.

>[!NOTE]
>
>사이트 페이지당 하나의 주석 시스템만 허용됩니다.
>
>많은 커뮤니티 기능에는 이미 확장된 주석 시스템을 참조하도록 resourceType을 수정할 수 있는 주석 시스템이 포함되어 있습니다.


## 주석 구성 요소 만들기 {#create-the-comments-component}

이러한 지침은 구성 요소 브라우저 **에서 구성 요소를 사용할 수 있도록 다른 그룹** `.hidden` 값을 지정합니다(사이드 킥됨).

자동 생성된 JSP 파일의 삭제는 기본 HBS 파일이 대신 사용되기 때문입니다.

1. CRXDE| **Lite** (http://localhost:4502/crx/de/index.jsp)으로[이동](http://localhost:4502/crx/de/index.jsp)

1. 사용자 정의 응용 프로그램의 위치를 만듭니다.

   * 노드 `/apps` 선택

      * **사용자 지정 폴더** 만들기 ****
   * 노드 `/apps/custom` 선택

      * **이름이 지정된 폴더** 구성 **[!UICONTROL 요소 만들기]**


1. 노드 `/apps/custom/components` 선택

   * **[!UICONTROL 만들기 > 구성 요소..]**

      * **레이블**: *comments*
      * **제목**: *대체 주석*
      * **설명**: *대체 주석 스타일*
      * **슈퍼 유형**: *social/commons/components/hbs/comments*
      * **그룹**: *사용자 지정*
   * **[!UICONTROL 다음]**&#x200B;을 선택합니다
   * **[!UICONTROL 다음]**&#x200B;을 선택합니다
   * **[!UICONTROL 다음]**&#x200B;을 선택합니다
   * 확인 **[!UICONTROL 선택]**


1. 방금 생성된 노드를 확장합니다. `/apps/custom/components/comments`
1. 모두 **[!UICONTROL 저장 선택]**
1. 마우스 오른쪽 단추 클릭 `comments.jsp`
1. 삭제 **[!UICONTROL 선택]**
1. 모두 **[!UICONTROL 저장 선택]**

![chlimage_1-70](assets/chlimage_1-70.png)

### 하위 주석 구성 요소 만들기 {#create-the-child-comment-component}

이러한 지침 **은** 상위 구성 요소만 페이지 내에 포함되도록 그룹을 `.hidden` 설정합니다.

자동 생성된 JSP 파일의 삭제는 기본 HBS 파일이 대신 사용되기 때문입니다.

1. 노드를 `/apps/custom/components/comments` 탐색합니다.
1. 노드를 마우스 오른쪽 단추로 클릭합니다.

   * **[!UICONTROL 만들기] > 구성 **[!UICONTROL 요소...를 선택합니다.]**

      * **레이블**: *comment*
      * **제목**: *대체 주석*
      * **설명**: *대체 주석 스타일*
      * **슈퍼 유형**: *social/commons/components/hbs/comments/comment*
      * **그룹**: `*.hidden*`
   * **[!UICONTROL 다음]**&#x200B;을 선택합니다
   * **[!UICONTROL 다음]**&#x200B;을 선택합니다
   * **[!UICONTROL 다음]**&#x200B;을 선택합니다
   * 확인 **[!UICONTROL 선택]**


1. 방금 생성된 노드를 확장합니다. `/apps/custom/components/comments/comment`
1. 모두 **[!UICONTROL 저장 선택]**
1. 마우스 오른쪽 단추 클릭 `comment.jsp`
1. 삭제 **[!UICONTROL 선택]**
1. 모두 **[!UICONTROL 저장 선택]**

![chlimage_1-71](assets/chlimage_1-71.png)

![chlimage_1-72](assets/chlimage_1-72.png)

### 기본 HBS 스크립트 복사 및 수정 {#copy-and-modify-the-default-hbs-scripts}

CRXDE [Lite 사용](../../help/sites-developing/developing-with-crxde-lite.md):

* 복사 `comments.hbs`

   * 보낸 사람/libs/social/commons/components/hbs/comments [](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * to/apps/custom/components/comments [](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* 편집 `comments.hbs` 대상:

   * 속성(~line 20)의 `data-scf-component` 값을 변경합니다.

      * 시작 `social/commons/components/hbs/comments`
      * 끝 `/apps/custom/components/comments`
   * 사용자 지정 주석 구성 요소(~line 75)를 포함하도록 수정합니다.

      * 바꾸기 `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * 사용 `{{include this resourceType='/apps/custom/components/comments/comment'}}`


* 복사 `comment.hbs`

   * 보낸 사람/libs/social/commons/components/hbs/comments/comment [](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * to/apps/custom/components/comments/comment [](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* 편집 `comment.hbs` 대상:

   * data-scf-component 속성(~ line 19) 값 변경

      * 시작 `social/commons/components/hbs/comments/comment`
      * 끝 `/apps/custom/components/comments/comment`

* 노드 `/apps/custom` 선택
* 모두 **[!UICONTROL 저장 선택]**

## 클라이언트 라이브러리 폴더 만들기 {#create-a-client-library-folder}

이 클라이언트 라이브러리를 명시적으로 포함할 필요가 없도록 하기 위해 기본 주석 시스템의 clientlib에 대한 카테고리 값을 사용할 수 있습니다( `cq.social.author.hbs.comments`). 그러나 이 clientlib은 기본 구성 요소의 모든 인스턴스에도 포함됩니다.

CRXDE [Lite 사용](../../help/sites-developing/developing-with-crxde-lite.md):

* 노드 `/apps/custom/components/comments` 선택
* 노드 **[!UICONTROL 만들기 선택]**

   * **이름**: `clientlibs`
   * **유형**: `cq:ClientLibraryFolder`
   * 속성 **[!UICONTROL 탭에]** 추가:

      * **이름** `categories` **유형** `String` **값** `cq.social.author.hbs.comments` `Multi`
      * **이름** `dependencies` **유형** `String` **값** `cq.social.scf` `Multi`

* 모두 **[!UICONTROL 저장 선택]**
* 노드 `/apps/custom/components/comments/clientlib`를 선택한 상태에서 3개의 파일을 만듭니다.

   * **이름**: `css.txt`
   * **이름**: `js.txt`
   * **이름**: customcomments.js

* &#39;customcomments system.js&#39;를 `js.txt`
* 모두 **[!UICONTROL 저장 선택]**

![chlimage_1-73](assets/chlimage_1-73.png)

## SCF 모델 및 보기 등록 {#register-the-scf-model-view}

SCF 구성 요소를 확장(재정의)할 때 resourceType은 다릅니다(오버레이하면 resourceType이 동일하게 유지되도록 `/apps` 이전에 검색하는 상대 검색 메커니즘을 `/libs` 사용할 수 있습니다). 이 때문에 클라이언트 라이브러리에서 JavaScript를 작성하여 SCF JS 모델을 등록하고 사용자 지정 resourceType에 대한 보기를 작성해야 합니다.

다음 텍스트를 컨텐츠로 입력합니다 `customcommentsystem.js`.

### customcomments.js {#customcommentsystem-js}

```xml
(function($CQ, _, Backbone, SCF) {
    "use strict";

    var CustomComment = SCF.Components["social/commons/components/hbs/comments/comment"].Model;
    var CustomCommentView = SCF.Components["social/commons/components/hbs/comments/comment"].View;

    var CustomCommentSystem = SCF.Components["social/commons/components/hbs/comments"].Model;
    var CustomCommentSystemView = SCF.Components["social/commons/components/hbs/comments"].View;

    SCF.registerComponent('/apps/custom/components/comments/comment', CustomComment, CustomCommentView);
    SCF.registerComponent('/apps/custom/components/comments', CustomCommentSystem, CustomCommentSystemView);

})($CQ, _, Backbone, SCF);
```

* 모두 **[!UICONTROL 저장 선택]**

## 앱 게시 {#publish-the-app}

게시 환경에서 확장 구성 요소를 경험하려면 사용자 지정 구성 요소를 복제해야 합니다.

방법 중 하나는

* 전역 탐색에서

   * Select **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]**
   * 트리 **[!UICONTROL 활성화 선택]**
   * 설정 `Start Path` 대상 `/apps/custom`
   * 수정된 **[!UICONTROL 항목만 선택 취소]**
   * 활성화 **[!UICONTROL 단추]** 선택

