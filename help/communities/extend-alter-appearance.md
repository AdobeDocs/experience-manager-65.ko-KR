---
title: 모양 변경(HBS)
description: HBS 스크립트를 편집하여 모양(HBS)을 변경하는 방법에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 27e1bff3-385e-4ced-87af-54044b7e8812
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# 모양 변경(HBS) {#alter-the-appearance-hbs}

기본 댓글 시스템을 참조하는 resourceSuperType과 사용자 지정 모델/보기가 등록된 응용 프로그램 디렉터리(/apps)의 사용자 지정 댓글 시스템에 대한 구성 요소가 준비되었으므로 구현을 편집할 수 있습니다.

간단한 시연을 위해 댓글을 게시하는 로그인한 사용자의 아바타가 표시되는 시각적 기능을 제거합니다.

>[!NOTE]
>
>확장을 사용하려면 영향을 받는 웹 사이트의 댓글 시스템 인스턴스(/content)가 해당 resourceType을 사용자 지정 댓글 시스템으로 설정해야 합니다.

## HBS 스크립트 수정 {#modify-the-hbs-scripts}

[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) 사용:

* [/apps/custom/components/comments/comment/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs) 열기

   * 댓글 게시물에 대한 아바타가 포함된 태그를 주석 처리합니다(~ 21행).

     ```
       <!--
        <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
        -->
     ```

* [/apps/custom/components/comments/**comments.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs) 열기

   * 다음 댓글 항목의 아바타가 포함된 태그를 주석 처리합니다(~ 44행).

     ```
       <!--
        <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
        -->
     ```

* **모두 저장** 선택

### 사용자 지정 앱 복제 {#replicate-custom-app}

애플리케이션이 수정되면 사용자 지정 구성 요소를 다시 복제해야 합니다.

이렇게 하는 한 가지 방법은 다음과 같습니다.

* 메인 메뉴에서

   * **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 복제]**&#x200B;를 선택합니다.
   * **[!UICONTROL 트리 활성화]**&#x200B;를 선택하십시오.
   * `Start Path`을(를) `/apps/custom`(으)로 설정합니다.
   * **[!UICONTROL 수정된 항목만]**&#x200B;을 선택 취소합니다.
   * **[!UICONTROL 활성화]** 단추를 선택하십시오.

### 게시된 샘플 페이지에서 수정된 댓글 보기 {#view-modified-comment-on-published-sample-page}

[게시 인스턴스에서 계속 ](/help/communities/extend-sample-page.md#publish-sample-page) 환경을 사용하면서 동일한 사용자로 로그인되어 있습니다. 이제 게시 환경에서 페이지를 새로 고쳐 아바타를 제거하는 수정 내용을 볼 수 있습니다.

![수정된 콘텐츠 보기](assets/view-modified-content.png)

### 샘플 주석 확장 패키지 {#sample-comment-extension-package}

이 자습서에서 만든 사용자 지정 주석 애플리케이션 패키지가 첨부되었습니다.

[파일 가져오기](assets/sample-comment-extension-6-1-fp3.zip)
