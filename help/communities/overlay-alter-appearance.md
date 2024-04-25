---
title: 모양 변경
description: Adobe Experience Manager Communities에서 각 댓글에 대한 전체 HTML을 작성하는 Comment.hbs 스크립트를 편집하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: cb8f6967-216c-46d3-a7ba-068b0f5e3b94
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# 모양 변경 {#alter-the-appearance}

## 스크립트 수정 {#modify-the-script}

다음 `comment.hbs` 스크립트는 각 댓글에 대한 전체 HTML 생성을 담당합니다.

게시된 각 댓글 옆에 아바타를 표시하지 않으려면:

1. 복사 `comment.hbs`출처: `libs`끝 `apps`

   1. 선택 `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. 선택 **[!UICONTROL 복사]**
   1. 선택 `/apps/social/commons/components/hbs/comments/comment`
   1. 선택 **[!UICONTROL 붙여넣기]**

1. 오버레이된 를 엽니다. `comment.hbs`

   * 노드 두 번 클릭 `comment.hbs` 위치: `/apps/social/commons/components/hbs/comments/comment folder`

1. 다음 줄을 찾아 삭제하거나 주석 처리합니다.

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

선을 삭제하거나 다음으로 둘러싸기 `<!--` 및 `-->` 그래서 당신은 그들을 언급합니다. 또한 아바타가 어디에 있었을 지에 대한 시각적 표시기로 &#39;xxx&#39; 문자가 추가되고 있습니다.

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### 오버레이 복제 {#replicate-the-overlay}

복제 도구를 사용하여 오버레이된 주석 구성 요소를 게시 인스턴스에 푸시합니다.

>[!NOTE]
>
>보다 강력한 복제 형식은 패키지 관리자에서 패키지를 만들고 [활성화](/help/sites-administering/package-manager.md#replicating-packages) 그래. 패키지를 내보내고 보관할 수 있습니다.

전역 탐색에서 을 선택합니다. **[!UICONTROL 도구]** > **[!UICONTROL 배포]** > **[!UICONTROL 복제]** 및 클릭 **[!UICONTROL 트리 활성화]**.

시작 경로에 를 입력합니다. `/apps/social/commons` 및 선택 **[!UICONTROL 활성화]**.

![verify-content-template](assets/verify-content-template.png)

### 결과 보기 {#view-results}

게시 인스턴스에 관리자로 로그온하는 경우(예: https://localhost:4503/crx/de as admin/admin) 오버레이된 구성 요소가 있는지 확인할 수 있습니다.

로그오프한 다음 다음으로 로그온하는 경우 `aaron.mcdonald@mailinator.com/password` 페이지를 새로 고치면 아바타가 게시된 댓글과 함께 표시되지 않습니다. 대신 간단한 &#39;xxx&#39;가 표시됩니다.

![create-template-component](assets/create-template-component.png)
