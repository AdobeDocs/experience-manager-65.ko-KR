---
title: 오버레이 커뮤니티 구성 요소
description: 구성 요소에 대한 모든 상대 참조에 대해 구성 요소의 모양이나 동작을 전체적으로 변경할 수 있도록 기본 구성 요소를 오버레이하는 방법에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 18376805-c2ed-439a-abc7-e9657afe8baf
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# 오버레이 커뮤니티 구성 요소 {#overlay-communities-components}

의 의도 [오버레이](/help/communities/client-customize.md#overlays) 기본 구성 요소는 구성 요소에 대한 모든 상대 참조에 대해 구성 요소의 모양이나 동작을 전체적으로 변경하는 것입니다. /libs 폴더에서 검색하기 전에 sling 특성에 따라 /apps 폴더로 해결됩니다. 따라서 구성 요소에 대한 경로는 /libs 폴더가 아닌 /apps 폴더에 있다는 점을 제외하면 기본 구성 요소에 대한 경로와 동일합니다.

## 예 {#example}

**오버레이 주석 구성 요소**

댓글에 대한 아바타가 더 이상 표시되지 않도록 댓글 헤더를 변경하여 웹 사이트의 디자인과 일치하도록 댓글 기능을 수정하려는 경우 아바타를 숨기는 솔루션은 CSS를 사용하거나, 여기에 설명된 대로 apps 폴더에 header.jsp를 오버레이하므로 아바타가 포함된 HTML이 클라이언트로 전송되지 않습니다.

댓글을 오버레이하려면 다음을 수행해야 합니다.

1. [댓글 만들기 페이지](/help/communities/overlay-create-comments-page.md)
1. [노드 만들기](/help/communities/overlay-create-nodes.md)
1. [모양 변경](/help/communities/overlay-alter-appearance.md)

**오버레이 알림 이메일**

이메일 알림 메시지를 사용자 정의하려는 경우 다음 작업을 수행할 수 있습니다. [오버레이](/help/communities/client-customize.md#overlays) 의 템플릿 `/libs/settings/community/templates/email/html`.

예를 들어 언급 이메일 알림(UGC가 생성된 특정 커뮤니티 구성 요소의 경우)을 편집하려고 한다고 가정합니다. 이러한 경우 **if** 동사 조건 **언급** 를 활성화한 구성 요소의 템플릿에서 **@mentions** 지원.

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

블로그 댓글에 추가할 이메일 알림 @mention을 수정하려면 의 기본 템플릿을 배치합니다. `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
