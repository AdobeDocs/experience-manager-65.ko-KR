---
title: 커뮤니티 구성 요소에 대한 OSGi 이벤트
seo-title: OSGi Events for Communities Components
description: 비동기 리스너를 트리거할 수 있는 OSGi 이벤트가 전송됩니다
seo-description: OSGi events are sent that can trigger asynchronous listeners
uuid: 317e2add-689d-4c99-ae38-0703b6649cb7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 25b7ac08-6cdc-4dd5-a756-d6169b86f9ab
exl-id: 8049d797-e758-44c2-a89b-51d2b2fca8dc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 4%

---

# 커뮤니티 구성 요소에 대한 OSGi 이벤트  {#osgi-events-for-communities-components}

## 개요 {#overview}

구성원이 커뮤니티 기능과 상호 작용할 때 알림 또는 게임화(점수 및 배지)와 같은 비동기 리스너를 트리거할 수 있는 OSGi 이벤트가 전송됩니다.

구성 요소 [SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) 인스턴스는 이벤트를 다음으로 기록합니다. `actions` 다음 기간 동안 발생 `topic`. SocialEvent에는 를 반환하는 메서드가 포함되어 있습니다. `verb` 작업과 연결되었습니다. 다음 항목이 있습니다. *-* 다음 사이의 관계 `actions` 및 `verbs`.

릴리스에 제공된 Communities 구성 요소의 경우 다음 표에서는 다음을 설명합니다. `verbs` 각각에 대해 정의됨 `topic` 사용할 수 있습니다.

## 주제 및 동사 {#topics-and-verbs}

[달력 구성 요소](calendar-basics-for-developers.md)
SocialEvent `topic`= com/adobe/cq/social/calendar

| **동사** | **설명** |
|---|---|
| POST | 구성원이 캘린더 이벤트를 만듭니다. |
| 추가 | 일정 이벤트에 대한 구성원 댓글 |
| 업데이트 | 구성원의 일정 이벤트 또는 댓글이 편집되었습니다. |
| 삭제 | 구성원의 일정 이벤트 또는 댓글이 삭제되었습니다. |

[주석 구성 요소](essentials-comments.md)
SocialEvent `topic`= com/adobe/cq/social/comment

| **동사** | **설명** |
|---|---|
| POST | 구성원이 주석을 만듭니다. |
| 추가 | 댓글에 대한 구성원 답글 |
| 업데이트 | 멤버의 주석이 편집되었습니다. |
| 삭제 | 구성원의 댓글이 삭제되었습니다. |

[파일 라이브러리 구성 요소](essentials-file-library.md)
SocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **동사** | **설명** |
|---|---|
| POST | 구성원이 폴더를 만듭니다. |
| 첨부 | 구성원이 파일을 업로드합니다. |
| 업데이트 | 구성원이 폴더 또는 파일을 업데이트합니다. |
| 삭제 | 구성원이 폴더 또는 파일을 삭제합니다. |

[포럼 구성 요소](essentials-forum.md)
SocialEvent `topic`= com/adobe/cq/social/forum

| **동사** | **설명** |
|---|---|
| POST | 구성원이 포럼 주제를 만듭니다. |
| 추가 | 포럼 주제에 대한 구성원 답글 |
| 업데이트 | 회원의 포럼 주제 또는 답글이 편집되었습니다. |
| 삭제 | 회원의 포럼 주제 또는 답글이 삭제되었습니다. |

[저널 구성 요소](blog-developer-basics.md)
SocialEvent `topic`= com/adobe/cq/social/journal

| **동사** | **설명** |
|---|---|
| POST | 구성원이 블로그 문서를 만듭니다. |
| 추가 | 블로그 기사에 대한 구성원 댓글 |
| 업데이트 | 멤버의 블로그 문서 또는 댓글이 편집되었습니다. |
| 삭제 | 멤버의 블로그 문서나 댓글이 삭제되었습니다. |

[QnA 구성 요소](qna-essentials.md)
SocialEvent `topic` = com/adobe/cq/social/qna

| **동사** | **설명** |
|---|---|
| POST | 멤버가 QnA 질문을 만듭니다. |
| 추가 | 멤버가 QnA 답변을 만듭니다. |
| 업데이트 | 멤버의 Q&amp;A 질문 또는 답변이 편집되었습니다. |
| 선택 | 멤버의 답변이 선택됨 |
| 선택 취소 | 멤버의 답변이 선택 해제되었습니다. |
| 삭제 | 멤버의 Q&amp;A 질문 또는 답변이 삭제되었습니다. |

[리뷰 구성 요소](reviews-basics.md)
SocialEvent `topic`= com/adobe/cq/social/review

| **동사** | **설명** |
|---|---|
| POST | 멤버가 리뷰를 만듭니다. |
| 업데이트 | 구성원의 리뷰가 편집됨 |
| 삭제 | 구성원의 검토 삭제됨 |

[등급 구성 요소](rating-basics.md)
SocialEvent `topic`= com/adobe/cq/social/tally

| **동사** | **설명** |
|---|---|
| 등급 추가 | 구성원의 콘텐츠가 등급이 올라갔습니다. |
| 등급 제거 | 구성원의 콘텐츠가 평가 중단되었습니다. |

[투표 구성 요소](essentials-voting.md)
SocialEvent `topic`= com/adobe/cq/social/tally

| **동사** | **설명** |
|---|---|
| 투표 추가 | 구성원의 콘텐츠가 투표에 부쳐졌습니다. |
| 투표 제거 | 구성원의 콘텐츠가 부결되었습니다. |

**중재 활성화 구성 요소**
SocialEvent `topic`= com/adobe/cq/social/moderation

| **동사** | **설명** |
|---|---|
| 거부 | 구성원의 콘텐츠가 거부되었습니다. |
| 부적절한 항목으로 표시 | 멤버의 컨텐츠에 플래그가 지정되었습니다. |
| 부적절한 항목으로 플래그 해제 | 구성원의 콘텐츠에 플래그가 지정되지 않음 |
| ACCEPT | 구성원의 콘텐츠가 중재자에 의해 승인되었습니다. |
| 닫기 | 구성원이 댓글을 닫아 편집 및 답글 작성 |
| 열기 | 구성원이 주석을 다시 엽니다. |

## 사용자 지정 구성 요소에 대한 이벤트 {#events-for-custom-components}

사용자 지정 구성 요소의 경우 [SocialEvent 추상 클래스](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) 구성 요소의 이벤트를 다음으로 기록하려면 d를 확장해야 합니다. `actions`다음 기간 동안 발생 `topic`.

사용자 지정 이벤트는 메서드를 재정의합니다. `getVerb()` 그래서 적절한 `verb`다음에 대해 반환됩니다 `action`. 다음 `verb` 작업에 대해 반환되는 항목은 일반적으로 사용되는 항목(예: `POST`) 또는 구성 요소용으로 특수 제작된 것(예: `ADD RATING`). 다음 항목이 있습니다. *-* 다음 사이의 관계 `actions`및 `verbs`.

>[!NOTE]
>
>사용자 지정 확장이 제품의 기존 구현보다 낮은 순위로 등록되었는지 확인합니다.

### 사용자 지정 구성 요소 이벤트에 대한 의사 코드 {#pseudo-code-for-custom-component-event}

[org.osgi.service.event.Event](https://osgi.org/javadoc/r4v41/org/osgi/service/event/Event.html);
[com.adobe.cq.social.scf.core.SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html);
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

## 활동 스트림 데이터를 필터링할 샘플 EventListener {#sample-eventlistener-to-filter-activity-stream-data}

활동 스트림에 나타나는 것을 수정하기 위한 목적으로 이벤트를 들을 수 있다.

다음 의사 코드 샘플은 활동 스트림에서 Comments 구성 요소에 대한 DELETE 이벤트를 제거합니다.

### EventListener용 의사 코드 {#pseudo-code-for-eventlistener}

필요 [최신 기능 팩](deploy-communities.md#latestfeaturepack).

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
