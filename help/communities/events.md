---
title: 커뮤니티 구성 요소에 대한 OSGi 이벤트
seo-title: 커뮤니티 구성 요소에 대한 OSGi 이벤트
description: 비동기 수신기를 트리거할 수 있는 OSGi 이벤트가 전송됩니다.
seo-description: 비동기 수신기를 트리거할 수 있는 OSGi 이벤트가 전송됩니다.
uuid: 317e2add-689d-4c99-ae38-0703b6649cb7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 25b7ac08-6cdc-4dd5-a756-d6169b86f9ab
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 4%

---


# 커뮤니티 구성 요소에 대한 OSGi 이벤트 {#osgi-events-for-communities-components}

## 개요 {#overview}

구성원이 커뮤니티 기능과 상호 작용하면 알림 또는 게임(점수 및 배지)과 같은 비동기 수신기를 트리거할 수 있는 OSGi 이벤트가 전송됩니다.

구성 요소의 [SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) 인스턴스는 `topic`에 대해 발생하는 `actions`로 이벤트를 기록합니다. SocialEvent에는 작업과 연관된 `verb`을(를) 반환하는 메서드가 포함되어 있습니다. `actions`과 `verbs` 사이에 *n-1* 관계가 있습니다.

릴리스에서 제공되는 커뮤니티 구성 요소의 경우 다음 표에서는 각 `topic`에 대해 정의된 `verbs`에 대해 설명합니다.

## 항목 및 동사 {#topics-and-verbs}

[달력 ](calendar-basics-for-developers.md)
구성 요소SocialEvent  `topic`= com/adobe/cq/social/calendar

| **동사** | **설명** |
|---|---|
| POST | 구성원이 달력 이벤트를 만듭니다. |
| 추가 | 달력 이벤트의 멤버 댓글 |
| 업데이트 | 회원의 달력 이벤트 또는 댓글이 편집되었습니다. |
| 삭제 | 회원의 달력 이벤트 또는 댓글이 삭제됨 |

[댓글 ](essentials-comments.md)
구성 요소SocialEvent  `topic`= com/adobe/cq/social/comment

| **동사** | **설명** |
|---|---|
| POST | 구성원이 댓글을 만듭니다. |
| 추가 | 댓글 달기 |
| 업데이트 | 회원의 댓글이 편집되었습니다. |
| 삭제 | 구성원의 댓글이 삭제됨 |

[파일 라이브러리 ](essentials-file-library.md)
구성 요소SocialEvent  `topic`= com/adobe/cq/social/fileLibrary

| **동사** | **설명** |
|---|---|
| POST | 구성원이 폴더를 만듭니다. |
| 첨부 | 구성원이 파일 업로드 |
| 업데이트 | 구성원이 폴더 또는 파일을 업데이트합니다. |
| 삭제 | 구성원이 폴더 또는 파일을 삭제합니다. |

[포럼 ](essentials-forum.md)
구성 요소SocialEvent  `topic`= com/adobe/cq/social/forum

| **동사** | **설명** |
|---|---|
| POST | 회원이 포럼 주제 작성 |
| 추가 | 포럼 주제에 대한 멤버 답글 |
| 업데이트 | 회원의 포럼 주제 또는 답변이 편집됨 |
| 삭제 | 회원의 포럼 주제 또는 답글이 삭제됨 |

[Journal ](blog-developer-basics.md)
ComponentSocialEvent  `topic`= com/adobe/cq/social/journal

| **동사** | **설명** |
|---|---|
| POST | 회원이 블로그 아티클을 만듭니다. |
| 추가 | 블로그 아티클에 대한 멤버 의견 |
| 업데이트 | 회원의 블로그 기사 또는 댓글이 편집되었습니다. |
| 삭제 | 구성원의 블로그 기사 또는 댓글이 삭제됨 |

[QnA ](qna-essentials.md)
ComponentSocialEvent  `topic` = com/adobe/cq/social/qna

| **동사** | **설명** |
|---|---|
| POST | 구성원이 QnA 질문을 만듭니다. |
| 추가 | 구성원이 QnA 대답을 만듭니다. |
| 업데이트 | 구성원의 QnA 질문이나 답변이 편집됨 |
| 선택 | 구성원 답변 선택 |
| 선택 취소 | 구성원 답변 선택 취소 |
| 삭제 | 멤버의 QnA 질문이나 답변이 삭제되었습니다. |

[평가 ](reviews-basics.md)
구성 요소SocialEvent  `topic`= com/adobe/cq/social/review

| **동사** | **설명** |
|---|---|
| POST | 멤버가 검토 작업 |
| 업데이트 | 구성원 검토 편집 |
| 삭제 | 구성원 검토 삭제 |

[등급 ](rating-basics.md)
구성 요소SocialEvent  `topic`= com/adobe/cq/social/tally

| **동사** | **설명** |
|---|---|
| 등급 추가 | 회원의 컨텐츠가 등급 상승되었습니다. |
| 등급 제거 | 회원의 컨텐츠가 등급이 낮았습니다. |

[투표 ](essentials-voting.md)
구성 요소SocialEvent  `topic`= com/adobe/cq/social/tally

| **동사** | **설명** |
|---|---|
| 투표 추가 | 회원의 컨텐츠가 투표되었습니다. |
| 투표 제거 | 회원의 컨텐츠가 부결되었다 |

**중재 지원 구성**
요소SocialEvent  `topic`= com/adobe/cq/social/moderation

| **동사** | **설명** |
|---|---|
| 거부 | 회원의 컨텐츠가 거부됨 |
| 기가 부적절한 | 구성원 컨텐츠가 플래그 지정됨 |
| 부적절한 플래그 해제 | 멤버의 컨텐츠가 플래그 해제됨 |
| 수락 | 중재자가 회원에게 컨텐츠 승인 |
| 닫기 | 멤버는 편집 및 답글에 대한 댓글을 닫습니다. |
| OPEN | 구성원 주석 다시 열기 |

## 사용자 지정 구성 요소에 대한 이벤트 {#events-for-custom-components}

사용자 지정 구성 요소의 경우 [SocialEvent 개요 클래스](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html)를 확장하여 구성 요소의 이벤트를 `topic`에 대해 발생하는 `actions`로 기록해야 합니다.

사용자 지정 이벤트는 각 `action`에 대해 적절한 `verb`이 반환되도록 `getVerb()` 메서드를 재정의합니다. 작업에 대해 반환되는 `verb`은 일반적으로 사용되는 하나(예: `POST`) 또는 구성 요소에 특화된 하나(예: `ADD RATING`)일 수 있습니다. `actions`과 `verbs` 사이에 *n-1* 관계가 있습니다.

>[!NOTE]
>
>사용자 지정 확장이 제품의 기존 구현보다 낮은 등급으로 등록되었는지 확인합니다.

### 사용자 지정 구성 요소 이벤트 {#pseudo-code-for-custom-component-event}에 대한 의사 코드

[org.osgi.service.event.Event](https://osgi.org/javadoc/r4v41/org/osgi/service/event/Event.html);
[com.adobe.cq.sosocial.scf.core.SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html);
[com.adobe.granite.activitystreams.ObjectTypes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ObjectTypes.html);
[com.adobe.granite.activitystreams.Verbs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/Verbs.html);

```java
package com.mycompany.recipe;

import org.osgi.service.event.Event;
import com.adobe.cq.social.scf.core.SocialEvent;
import com.adobe.granite.activitystreams.ObjectTypes;
import com.adobe.granite.activitystreams.Verbs;

/*
 * The Recipe type, passed to RecipeEvent(), would be a custom Recipe class
 * that extends either
 * com.adobe.cq.social.scf.SocialComponent
 * or
 * com.adobe.cq.social.scf.SocialCollectionComponent
 * See https://docs.adobe.com/docs/en/aem/6-2/develop/communities/scf/server-customize.html
 */

/**
 * Defines events that are triggered on a custom component, "Recipe".
 */
public class RecipeEvent extends SocialEvent<RecipeEvent.RecipeActions> {

    private static final long serialVersionUID = 1L;
    protected static final String PARENT_PATH = "PARENT_PATH";

    /**
     * The event topic suffix for Recipe events
     */
    public static final String RECIPE_TOPIC = "recipe";

    /**
     * @param recipe - the recipe resource on which the event was triggered
     * @param userId - the user id of the user who triggered the action
     * @param action - the recipe action that triggered this event
     */
    public RecipeEvent(final Recipe recipe, final String userId, final RecipeEvent.RecipeActions action) {
        String recipePath = recipe.getResource().getPath();
        String parentPath = (recipe.getParentComponent() != null) ?
                             recipe.getParentComponent().getResource().getPath() :
                             recipe.getSourceComponentId();
        this(recipePath, userId, parentPath, action);
    }

    /**
     * @param recipePath - the path to the recipe resource (jcr node) on which the event was triggered
     * @param userId - the user id of the user who triggered the action
     * @param parentPath - the path to the parent node of the recipe resource
     * @param action - the recipe action that triggered this event
     */
    public RecipeEvent(final String recipePath, final String userId, final String parentPath) {
        super(RECIPE_TOPIC, recipePath, userId, action,
              new BaseEventObject(recipePath, ObjectTypes.ARTICLE),
              new BaseEventObject(parentPath, ObjectTypes.COLLECTION),
              new HashMap<String, Object>(1) {
            private static final long serialVersionUID = 1L;
            {
                if (parentPath != null) {
                    this.put(PARENT_PATH, parentPath);
                }

            }
        });
    }

    private RecipeEvent (final Event event) {
      super(event);
    }

    /**
     * List of available recipe actions that can trigger a recipe event.
     */
    public static enum RecipeActions implements SocialEvent.SocialActions {
        RecipeAdded,
        RecipeModified,
        RecipeDeleted;

        @Override
        public String getVerb() {
            switch (this) {
                case RecipeAdded:
                    return Verbs.POST;
                case RecipeModified:
                    return Verbs.UPDATE;
                case RecipeDeleted:
                    return Verbs.DELETE;
                default:
                    throw new IllegalArgumentException("Unsupported action");
            }
        }
    }

}
```

## 활동 스트림 데이터를 필터링하는 샘플 EventListener {#sample-eventlistener-to-filter-activity-stream-data}

활동 스트림에 나타나는 내용을 수정하기 위해 이벤트를 들을 수 있습니다.

다음 의사 코드 샘플은 활동 스트림에서 댓글 구성 요소에 대한 DELETE 이벤트를 제거합니다.

### EventListener {#pseudo-code-for-eventlistener}에 대한 의사 코드

[최신 기능 팩](deploy-communities.md#latestfeaturepack)이 필요합니다.

```java
package my.company.comments;

import java.util.Collections;
import java.util.Map;

import org.apache.commons.lang.StringUtils;
import org.apache.felix.scr.annotations.Activate;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Modified;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.commons.osgi.PropertiesUtil;
import org.osgi.service.component.ComponentContext;

import com.adobe.cq.social.activitystreams.listener.api.ActivityStreamProviderExtension;
import com.adobe.cq.social.commons.events.CommentEvent.CommentActions;
import com.adobe.cq.social.scf.core.SocialEvent;

@Service
@Component(metatype = true, label = "My Comment Delete Event Filter",
        description = "Prevents comment DELETE events from showing up in activity streams")
public class CommentDeleteEventActivityFilter implements ActivityStreamProviderExtension {

    @Property(name = "ranking", intValue = 10)
    protected int ranking;

    @Activate
    public void activate(final ComponentContext ctx) {
        ranking = PropertiesUtil.toInteger(ctx.getProperties().get("ranking"), 10);
    }

    @Modified
    public void update(final Map<String, Object> props) {
        ranking = PropertiesUtil.toInteger(props.get("ranking"), 10);
    }

    @Override
    public boolean evaluate(final SocialEvent<?> evt, final Resource resource) {
        if (evt.getAction() != null && evt.getAction() instanceof SocialEvent.SocialActions) {
            final SocialEvent.SocialActions action = evt.getAction();
            if (StringUtils.equals(action.getVerb(), CommentActions.DELETED.getVerb())) {
                return false;
            }
        }
        return true;
    }

    @Override
    public Map<String, ? extends Object> getActivityProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public Map<String, ? extends Object> getActorProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public String getName() {
        return "My Comment Delete Event Filter";
    }

    @Override
    public Map<String, ? extends Object> getObjectProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    /* Ensure a custom extension is registered with a ranking lower than any existing implementation in the product. */
    @Override
    public int getRanking() {
        return this.ranking;
    }

    @Override
    public Map<String, ? extends Object> getTargetProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public String[] getStreamProviderPid() {
        return new String[]{"*"};
    }

}
```

