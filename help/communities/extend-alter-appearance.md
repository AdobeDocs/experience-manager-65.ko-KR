---
title: 모양 변경(HBS)
seo-title: 모양 변경
description: HBS 스크립트 수정
seo-description: HBS 스크립트 수정
uuid: cff24505-dbb3-4312-9b1b-c1693b8d1c98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e0da09b3-725d-4ed1-9273-2532132f6918
docset: aem65
translation-type: tm+mt
source-git-commit: 570c970c328ded828680baeb1b04ab4361a36226
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---


# 모양 변경(HBS) {#alter-the-appearance-hbs}

이제 응용 프로그램 디렉터리(/apps)의 사용자 지정 주석 시스템에 대한 구성 요소가 제대로 사용되고, resourceSuperType이 기본 주석 시스템 및 등록된 사용자 지정 모델/보기를 참조하므로 구현을 수정할 수 있습니다.

간단한 데모에서는 댓글을 게시한 로그인한 사용자의 아바타가 제거됩니다.

>[!NOTE]
>
>확장을 사용하려면 웹 사이트의 댓글 시스템 인스턴스(/content)가 해당 resourceType을 사용자 지정 주석 시스템으로 설정해야 합니다.


## HBS 스크립트 수정 {#modify-the-hbs-scripts}

CRXDE Lite [사용](/help/sites-developing/developing-with-crxde-lite.md):

* Open [/apps/custom/components/comments/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * 댓글 게시물에 대한 아바타가 포함된 태그에 주석 추가(~ 줄 21):

      ```
        <!--
         <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
         -->
      ```

* Open [/apps/custom/components/comments/**comments.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * 다음 주석 항목에 대한 아바타가 포함된 태그에 주석 추가(~ 줄 44):

      ```
        <!--
         <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
         -->
      ```

* 모두 **저장 선택**

### 사용자 정의 앱 복제 {#replicate-custom-app}

애플리케이션을 수정한 후에는 사용자 지정 구성 요소를 다시 복제해야 합니다.

이를 위한 한 가지 방법은 다음과 같습니다.

* 주 메뉴에서

   * 도구 **[!UICONTROL > 작업]** **** > **[!UICONTROL 복제를]**&#x200B;선택합니다.
   * 트리 **[!UICONTROL 활성화를 선택합니다]**.
   * 설정 `Start Path` 을 `/apps/custom`참조하십시오.
   * [ **[!UICONTROL 수정된 항목만]을 선택 취소합니다]**.
   * 활성화 **[!UICONTROL 단추를]** 선택합니다.

### 게시된 샘플 페이지에서 수정된 주석 보기 {#view-modified-comment-on-published-sample-page}

[동일한 사용자로 로그인되어 있는 게시 인스턴스에서 경험을](/help/communities/extend-sample-page.md#publish-sample-page) 계속 진행하면 이제 아바타를 제거하기 위한 수정 사항을 보기 위해 게시 환경에서 페이지를 새로 고칠 수 있습니다.

![view-modified-content](assets/view-modified-content.png)

### 샘플 주석 확장 패키지 {#sample-comment-extension-package}

이 튜토리얼에서 만든 사용자 지정 댓글 응용 프로그램의 패키지가 첨부됩니다.

[파일 가져오기](assets/sample-comment-extension-6-1-fp3.zip)
