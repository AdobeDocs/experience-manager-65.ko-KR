---
title: 커뮤니티 구성 요소 오버레이
seo-title: Overlay communities components
description: 커뮤니티 구성 요소 오버레이
seo-description: Overlay communities components
uuid: 872f7006-959a-49d2-b025-3a5abb7c6dca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 502c0916-6c54-440c-be8c-eae56001fa26
docset: aem65
exl-id: 18376805-c2ed-439a-abc7-e9657afe8baf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# 커뮤니티 구성 요소 오버레이 {#overlay-communities-components}

의 의도 [오버레이](/help/communities/client-customize.md#overlays) 기본 컴포넌트는 컴포넌트에 대한 모든 상대 참조에 대해 전체적으로 컴포넌트의 모양이나 동작을 변경하는 것입니다. /libs 폴더에서 검색하기 전에 sling의 특성을 사용하여 /apps 폴더로 확인합니다. 따라서 구성 요소의 경로는 /apps 폴더에 있지 않고 /libs 폴더에 있다는 점을 제외하고 기본 구성 요소의 경로와 동일합니다.

## 예 {#example}

**오버레이 주석 구성 요소**

주석 기능을 수정하여 웹 사이트의 디자인과 일치되도록 하거나 주석 헤더를 변경하여 더 이상 댓글에 대한 아바타가 표시되지 않도록 한다고 가정합니다. 아바타를 숨기는 솔루션은 CSS를 사용하거나, 여기에 설명된 대로 앱의 header.jsp를 오버레이하여 아바타가 포함된 HTML이 클라이언트로 전송되지 않도록 합니다.

주석을 오버레이하려면 다음을 수행해야 합니다.

1. [댓글 페이지](/help/communities/overlay-create-comments-page.md)
1. [노드 만들기](/help/communities/overlay-create-nodes.md)
1. [모양 변경](/help/communities/overlay-alter-appearance.md)

**오버레이 알림 이메일**

이메일 알림 메시지를 사용자 정의한다고 가정할 경우 다음을 수행하여 다음을 수행할 수 있습니다. [오버레이](/help/communities/client-customize.md#overlays) 의 템플릿 **/libs/settings/community/templates/email/html**.

예를 들어, 언급 이메일 알림을 수정하려면(ugc가 생성된 특정 커뮤니티 구성 요소에 대해) **if** 동사 조건 **언급** 을 활성화할 구성 요소의 템플릿에서 **@mentions** 지원.

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

블로그 댓글에 @mention에 대한 이메일 알림 템플릿을 수정하려면 다음 위치에서 즉시 템플릿을 사용하십시오. `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
