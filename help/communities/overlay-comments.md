---
title: 커뮤니티 구성 요소 오버레이
seo-title: 커뮤니티 구성 요소 오버레이
description: 커뮤니티 구성 요소 오버레이
seo-description: 커뮤니티 구성 요소 오버레이
uuid: 872f7006-959a-49d2-b025-3a5abb7c6dca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 502c0916-6c54-440c-be8c-eae56001fa26
docset: aem65
translation-type: tm+mt
source-git-commit: 48afa2146d0dcbab4beaa1044645c269b49fd7ff
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# 오버레이 커뮤니티 구성 요소 {#overlay-communities-components}

기본 구성 요소를 오버레이하는 [의 의도는 구성 요소에 대한 모든 상대 참조에 대해 구성 요소의 모양 또는 동작을 전역적으로 변경하는 것입니다. ](/help/communities/client-customize.md#overlays) /libs 폴더에서 검색하기 전에 /apps 폴더로 확인하는 슬링의 특성에 의존합니다. 따라서 구성 요소의 경로는 /apps 폴더에 있지 않고 /libs 폴더에 있다는 점을 제외하고 기본 구성 요소의 경로와 동일합니다.

## 예 {#example}

**오버레이 주석 구성 요소**

주석 기능을 수정하면 댓글에 대한 아바타가 더 이상 표시되지 않도록 주석 헤더를 변경하여 웹 사이트의 디자인과 일치한다고 가정합니다. 아바타를 숨기는 방법은 CSS를 사용하거나, 여기에 설명된 대로, 아바타가 포함된 HTML이 클라이언트에 전송되지 않도록 앱 폴더에 header.jsp를 오버레이하는 것입니다.

주석을 오버레이하려면 다음을 수행해야 합니다.

1. [댓글 페이지](/help/communities/overlay-create-comments-page.md)
1. [노드 만들기](/help/communities/overlay-create-nodes.md)
1. [모양 변경](/help/communities/overlay-alter-appearance.md)

**오버레이 알림 이메일**

이메일 알림의 메시지를 사용자 정의하려는 경우 [오버레이](/help/communities/client-customize.md#overlays)에서 **/libs/settings/community/templates/email/html**&#x200B;의 템플릿을 사용할 수 있다고 가정합니다.

예를 들어 언급 이메일 알림을 수정하려면(ugc가 생성된 특정 커뮤니티 구성 요소의 경우) **@mentions** 지원을 활성화한 구성 요소의 템플릿에 동사 **mention**&#x200B;에 대한 **if** 조건을 추가합니다.

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

블로그 댓글에 있는 @mention에 대한 이메일 알림 템플릿을 수정하려면 다음 위치에서 기본 템플릿을 활용하십시오.`/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
