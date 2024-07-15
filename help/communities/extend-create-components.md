---
title: 구성 요소 만들기
description: 댓글 및 댓글 구성 요소로 구성된 댓글 시스템을 사용하여 구성 요소를 확장하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 2e02db9f-294d-4d4a-92da-3ab1d38416ab
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# 구성 요소 만들기  {#create-the-components}

구성 요소 확장의 예에서는 두 구성 요소로 구성된 주석 시스템을 사용합니다.

* 주석 - 페이지에 배치된 구성 요소인 포괄적인 주석 시스템
* 댓글 - 게시된 댓글의 인스턴스를 캡처하는 구성 요소입니다.

특히 게시된 댓글의 모양을 사용자 지정하는 경우 두 구성 요소를 모두 배치해야 합니다.

>[!NOTE]
>
>사이트 페이지당 하나의 주석 시스템만 허용됩니다.
>
>많은 Communities 기능에는 확장된 댓글 시스템을 참조하도록 resourceType을 수정할 수 있는 댓글 시스템이 이미 포함되어 있습니다.

## 주석 구성 요소 만들기 {#create-the-comments-component}

이 지침은 구성 요소 브라우저(사이드 킥)에서 구성 요소를 사용할 수 있도록 `.hidden` 이외의 **그룹** 값을 지정합니다.

자동 생성된 JSP 파일이 삭제되는 것은 기본 HBS 파일이 대신 사용되기 때문입니다.

1. **CRXDE|Lite**([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)) 탐색

1. 사용자 정의 응용 프로그램의 위치를 만듭니다.

   * `/apps` 노드 선택

      * **폴더 만들기** 이름 **[!UICONTROL 사용자 지정]**

   * `/apps/custom` 노드 선택

      * **[!UICONTROL 구성 요소]**(이)라는 이름의 **폴더 만들기**

1. `/apps/custom/components` 노드 선택

   * **[!UICONTROL 만들기 > 구성 요소...]**

      * **레이블**: *댓글*
      * **제목**: *대체 댓글*
      * **설명**: *대체 댓글 스타일*
      * **슈퍼 유형**: *social/commons/components/hbs/comments*
      * **그룹**: *사용자 지정*

   * **[!UICONTROL 다음]** 선택
   * **[!UICONTROL 다음]** 선택
   * **[!UICONTROL 다음]** 선택
   * **[!UICONTROL 확인]** 선택

1. 만든 노드를 확장합니다. `/apps/custom/components/comments`
1. **[!UICONTROL 모두 저장]** 선택
1. `comments.jsp`을(를) 마우스 오른쪽 단추로 클릭
1. **[!UICONTROL 삭제]** 선택
1. **[!UICONTROL 모두 저장]** 선택

![구성 요소 만들기](assets/create-component.png)

### 하위 주석 구성 요소 만들기 {#create-the-child-comment-component}

이러한 지침은 **그룹**&#x200B;을(를) `.hidden`(으)로 설정하므로 상위 구성 요소만 페이지 내에 포함되어야 합니다.

자동 생성된 JSP 파일이 삭제되는 것은 기본 HBS 파일이 대신 사용되기 때문입니다.

1. `/apps/custom/components/comments` 노드로 이동
1. 노드를 마우스 오른쪽 버튼으로 클릭합니다.

   * **[!UICONTROL 만들기]** > **[!UICONTROL 구성 요소...]** 선택

      * **레이블**: *댓글*
      * **제목**: *대체 댓글*
      * **설명**: *대체 댓글 스타일*
      * **슈퍼 유형**: *social/commons/components/hbs/comments/comment*
      * **그룹**: `*.hidden*`

   * **[!UICONTROL 다음]** 선택
   * **[!UICONTROL 다음]** 선택
   * **[!UICONTROL 다음]** 선택
   * **[!UICONTROL 확인]** 선택

1. 만든 노드를 확장합니다. `/apps/custom/components/comments/comment`
1. **[!UICONTROL 모두 저장]** 선택
1. `comment.jsp`을(를) 마우스 오른쪽 단추로 클릭
1. **[!UICONTROL 삭제]** 선택
1. **[!UICONTROL 모두 저장]** 선택

![create-child-component](assets/create-child-component.png)

![create-component-crxde](assets/create-component-crxde.png)

### 기본 HBS 스크립트 복사 및 수정 {#copy-and-modify-the-default-hbs-scripts}

[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) 사용:

* `comments.hbs` 복사

   * [/libs/social/commons/components/hbs/comments에서](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * 대상: [/apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* `comments.hbs`을(를) 편집할 대상:

   * `data-scf-component` 특성 값 변경(~20행):

      * 출처: `social/commons/components/hbs/comments`
      * 대상: `/apps/custom/components/comments`

   * 사용자 지정 댓글 구성 요소를 포함하도록 수정합니다(~75행).

      * `{{include this resourceType='social/commons/components/hbs/comments/comment'}}` 바꾸기
      * `{{include this resourceType='/apps/custom/components/comments/comment'}}` 사용

* `comment.hbs` 복사

   * [/libs/social/commons/components/hbs/comments/comments에서](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * 대상: [/apps/custom/components/comments/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* `comment.hbs`을(를) 편집할 대상:

   * data-scf-component 특성의 값을 변경합니다(~ 19행).

      * 출처: `social/commons/components/hbs/comments/comment`
      * 대상: `/apps/custom/components/comments/comment`

* `/apps/custom` 노드 선택
* **[!UICONTROL 모두 저장]** 선택

## 클라이언트 라이브러리 폴더 만들기 {#create-a-client-library-folder}

이 클라이언트 라이브러리를 포함하지 않으려면 기본 주석 시스템의 clientlib에 대한 범주 값을 사용할 수 있습니다(`cq.social.author.hbs.comments`). 그러나 기본 구성 요소의 모든 인스턴스에 대해서도 이 clientlib을 포함해야 합니다.

[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) 사용:

* `/apps/custom/components/comments` 노드 선택
* **[!UICONTROL 노드 만들기]** 선택

   * **이름**: `clientlibs`
   * **유형**: `cq:ClientLibraryFolder`
   * **[!UICONTROL 속성]** 탭에 추가:

      * **이름** `categories` **유형** `String` **값** `cq.social.author.hbs.comments` `Multi`
      * **이름** `dependencies` **유형** `String` **값** `cq.social.scf` `Multi`

* **[!UICONTROL 모두 저장]** 선택
* `/apps/custom/components/comments/clientlib`의 노드를 선택한 상태에서 다음 세 개의 파일을 만듭니다.

   * **이름**: `css.txt`
   * **이름**: `js.txt`
   * **이름**: customcommentsystem.js

* `js.txt`의 콘텐츠로 &#39;customcommentsystem.js&#39;를 입력하십시오.
* **[!UICONTROL 모두 저장]** 선택

![comments-clientlibs](assets/comments-clientlibs.png)

## SCF 모델 및 뷰 등록 {#register-the-scf-model-view}

SCF 구성 요소를 확장(재정의)할 때 resourceType은 다릅니다. 오버레이는 `/libs` 전에 `/apps`을(를) 통해 검색하여 resourceType이 동일하게 유지되도록 하는 상대 검색 메커니즘을 사용합니다. SCF JS 모델을 등록하고 사용자 지정 resourceType에 대한 보기를 위해 클라이언트 라이브러리에 JavaScript을 작성해야 하는 이유입니다.

`customcommentsystem.js`의 콘텐츠로 다음 텍스트를 입력하십시오.

### customcommentsystem.js {#customcommentsystem-js}

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

* **[!UICONTROL 모두 저장]** 선택

## 앱 Publish {#publish-the-app}

게시 환경에서 확장 구성 요소를 경험하려면 사용자 지정 구성 요소를 복제해야 합니다.

이렇게 하는 한 가지 방법은 다음과 같습니다.

* 전역 탐색에서,

   * **[!UICONTROL 도구]** > **[!UICONTROL 배포]** > **[!UICONTROL 복제]** 선택
   * **[!UICONTROL 트리 활성화]** 선택
   * `Start Path`을(를) `/apps/custom`(으)로 설정
   * **[!UICONTROL 수정된 항목만]** 선택 취소
   * **[!UICONTROL 활성화]** 단추 선택
