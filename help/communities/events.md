---
title: OSGi Events for Communities 구성 요소
description: 비동기 리스너를 트리거할 수 있는 OSGi 이벤트가 전송됩니다
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8049d797-e758-44c2-a89b-51d2b2fca8dc
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 5%

---

# OSGi Events for Communities 구성 요소  {#osgi-events-for-communities-components}

## 개요 {#overview}

구성원이 Communities 기능과 상호 작용하면 비동기 리스너, 좋아요 알림 또는 게임화(점수 매기기 및 배지)를 트리거할 수 있는 OSGi 이벤트가 전송됩니다.

구성 요소의 [SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) 인스턴스 는 에 대해 `topic`발생하는 이벤트를 `actions` 기록합니다. SocialEvent에는 작업과 연결된 를 `verb` 반환하는 메서드가 포함되어 있습니다. 와 사이에는 `actions` n-1 *관계가 있습니다*`verbs`.

릴리스에서 제공되는 Communities 구성 요소의 경우 다음 표에서는 사용 가능한 각 `topic` 구성 요소에 대해 정의된 구성 요소에 대해 설명합니다`verbs`.

## 주제 및 동사 {#topics-and-verbs}

[달력 구성 요소](calendar-basics-for-developers.md)
SocialEvent `topic`= com/adobe/cq/social/calendar

| **동사** | **설명** |
|---|---|
| 올리기 | 멤버 구성원이 달력 이벤트를 만듭니다. |
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
| 첨부 | 멤버 업로드 |
| 업데이트 | 멤버 업데이트 폴더 또는 파일 |
| 삭제 | 멤버 삭제 폴더 또는 파일 |

[포럼 구성 요소](essentials-forum.md)
SocialEvent `topic`= com/adobe/cq/social/포럼

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
| 올리기 | 멤버 블로그 기사 작성 |
| 추가 | 블로그 기사에서 멤버 댓글 |
| 업데이트 | 멤버 블로그 기사 또는 댓글이 편집됨 |
| 삭제 | 멤버 블로그 기사 또는 댓글이 삭제되었습니다. |

[Q&amp;A 구성 요소](qna-essentials.md)
SocialEvent `topic` = com/adobe/cq/social/qna

| **동사** | **설명** |
|---|---|
| 올리기 | 멤버 만들기 QnA 질문 |
| 추가 | 멤버 만들기 QnA 답변 |
| 업데이트 | 멤버 QnA 질문 또는 답변이 편집됨 |
| 선택 | 멤버 답변이 선택되었습니다. |
| 선택을 취소 | 멤버의 답변이 선택 해제되었습니다. |
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
| 부적절한 항목으로 표시 | 멤버 컨텐츠에 플래그가 지정됨 |
| 부적절한 항목으로 플래그 해제 | 구성원의 콘텐츠에 플래그가 지정되지 않음 |
| ACCEPT | 구성원의 콘텐츠가 중재자에 의해 승인되었습니다. |
| 닫기 | 멤버 닫기, 편집 및 답글에 댓글 닫기 |
| 열기 | 댓글을 다시 여는 멤버 |

## 사용자 지정 구성 요소에 대한 이벤트 {#events-for-custom-components}

사용자 지정 구성 요소의 경우 [SocialEvent 추상 클래스를](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) 확장하여 에 대해 발생하는 구성 요소의 이벤트를 `actions`기록해야 합니다 `topic`.

사용자 지정 이벤트 가 메서드를 `getVerb()` 재정의하여 `verb`각 `action`. 작업에 대해 반환되는 것은 `verb` 일반적으로 사용되는 것(예 `POST`: )이거나 구성 요소에 특화된 것(예 `ADD RATING`: )일 수 있습니다. 와 사이에는 `actions`n-1 *관계가 있습니다*`verbs`.

>[!NOTE]
>
>사용자 지정 확장이 제품의 기존 구현보다 낮은 등급으로 등록되었는지 확인합니다.

### 사용자 지정 구성 요소 이벤트에 대한 의사 Code {#pseudo-code-for-custom-component-event}

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

## 활동 스트림 데이터 필터링에 대한 샘플 EventListener {#sample-eventlistener-to-filter-activity-stream-data}

활동 스트림에 표시되는 내용을 수정하기 위해 이벤트를 수신할 수 있습니다.

다음 의사 코드 샘플은 활동 스트림에서 댓글 구성 요소에 대한 DELETE 이벤트를 제거합니다.

### EventListener에 대한 의사 코드 {#pseudo-code-for-eventlistener}

최신 기능 팩](deploy-communities.md#latestfeaturepack)이 필요합니다[.

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
