---
title: 모양 변경
seo-title: 모양 변경
description: 스크립트 수정
seo-description: 스크립트 수정
uuid: 30555b9f-da29-4115-9ed5-25f80a247bd6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c9d31ed8-c105-453b-bd3c-4660dfd81272
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# 모양 {#alter-the-appearance} 변경

## 스크립트 {#modify-the-script} 수정

comment.hbs 스크립트는 각 댓글에 대한 전체 HTML을 만듭니다.

게시된 각 주석 옆에 아바타를 표시하지 않으려면:

1. `libs`에서 `apps`로 `comment.hbs`복사

   1. 선택 `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. **[!UICONTROL 복사]** 선택
   1. 선택 `/apps/social/commons/components/hbs/comments/comment`
   1. **[!UICONTROL 붙여넣기]** 선택

1. 오버레이된 `comment.hbs` 열기

   * `/apps/social/commons/components/hbs/comments/comment folder`에서 `comment.hbs` 노드를 두 번 클릭합니다.

1. 다음 줄을 찾아 삭제하거나 주석을 답니다.

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

행을 삭제하거나 `<!--` 및 `-->`로 둘러싸서 주석을 답니다. 또한 &#39;xxx&#39; 캐릭터는 아바타가 있었던 위치를 시각적으로 나타내는 표시로 추가됩니다.

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### 오버레이 {#replicate-the-overlay} 복제

복제 도구를 사용하여 오버레이된 주석 구성 요소를 게시 인스턴스에 푸시합니다.

>[!NOTE]
>
>보다 강력한 복제 형식은 패키지 관리자에서 패키지를 만들고 [activate](/help/sites-administering/package-manager.md#replicating-packages)합니다. 패키지를 내보내고 보관할 수 있습니다.

전역 탐색에서 **[!UICONTROL 도구]** > **[!UICONTROL 배포]** > **[!UICONTROL 복제]**&#x200B;를 선택하고 **[!UICONTROL 트리 활성화]**&#x200B;를 클릭합니다.

시작 경로에 `/apps/social/commons`을 입력하고 **[!UICONTROL 활성화]**&#x200B;를 선택합니다.

![verify-content-template](assets/verify-content-template.png)

### 결과 보기 {#view-results}

게시 인스턴스에 관리자로 로그인하는 경우(예: https://localhost:4503/crx/de as admin/admin), 오버레이된 구성 요소가 있는지 확인할 수 있습니다.

로그아웃한 후 `aaron.mcdonald@mailinator.com/password`으로 다시 로그인하고 페이지를 새로 고치면 게시된 댓글이 더 이상 아바타로 표시되지 않고 간단한 &#39;xxx&#39;가 표시됩니다.

![create-template-component](assets/create-template-component.png)

