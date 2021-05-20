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
exl-id: 27e1bff3-385e-4ced-87af-54044b7e8812
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# 모양(HBS) {#alter-the-appearance-hbs} 변경

애플리케이션 디렉토리(/apps)의 사용자 지정 주석 시스템에 대한 구성 요소가 배치되었으므로, resourceSuperType이 기본 주석 시스템을 참조하고 사용자 지정 모델/보기가 등록된 상태로 구현을 수정할 수 있습니다.

간단한 데모에서는 댓글을 게시한 로그인한 사용자의 아바타가 제거됩니다.

>[!NOTE]
>
>확장을 사용하려면 웹 사이트에서 주석 시스템의 인스턴스가 영향을 받을(/content)의 인스턴스를 resourceType을 사용자 지정 주석 시스템으로 설정해야 합니다.

## HBS 스크립트 {#modify-the-hbs-scripts} 수정

[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) 사용:

* [/apps/custom/components/comments/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs) 열기

   * 주석 게시물에 대한 아바타가 포함된 태그를 주석 처리합니다(~ 21행).

      ```
        <!--
         <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
         -->
      ```

* [/apps/custom/components/comments/**comments.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs) 열기

   * 다음 주석 항목(~ 44행)에 대한 아바타가 포함된 태그를 주석 처리하십시오.

      ```
        <!--
         <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
         -->
      ```

* **모두 저장** 선택

### 사용자 지정 앱 복제 {#replicate-custom-app}

애플리케이션이 수정된 후에는 사용자 지정 구성 요소를 다시 복제해야 합니다.

한 가지 방법은 다음과 같습니다.

* 주 메뉴에서

   * **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 복제]**&#x200B;를 선택합니다.
   * **[!UICONTROL 트리 활성화]**&#x200B;를 선택합니다.
   * `Start Path` 을 `/apps/custom`(으)로 설정합니다.
   * **[!UICONTROL Only Modified]** 선택 취소합니다.
   * **[!UICONTROL 활성화]** 단추를 선택합니다.

### 게시된 샘플 페이지에서 수정된 주석 보기 {#view-modified-comment-on-published-sample-page}

[여전히 동일한 ](/help/communities/extend-sample-page.md#publish-sample-page) 사용자로 로그인한 게시 인스턴스에서 경험을 계속 진행합니다. 이제 게시 환경에서 페이지를 새로 고쳐 아바타를 제거할 수 있는 수정 사항을 볼 수 있습니다.

![view-modified-content](assets/view-modified-content.png)

### 샘플 주석 확장 패키지 {#sample-comment-extension-package}

이 자습서에서 만든 사용자 정의 댓글 응용 프로그램 패키지가 첨부됩니다.

[파일 가져오기](assets/sample-comment-extension-6-1-fp3.zip)
