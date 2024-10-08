---
title: 커뮤니티 문제 해결
description: 알려진 문제 및 우려 사항을 포함하여 커뮤니티 문제 해결에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: ef4f4108-c485-4e2e-a58f-ff64eee9937e
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# 커뮤니티 문제 해결 {#troubleshooting}

이 섹션에는 커뮤니티 문제 해결 시 발생하는 일반적인 문제와 알려진 문제가 포함되어 있습니다.

## 알려진 문제 {#known-issues}

### Dispatcher 재가져오기 실패 {#dispatcher-refetch-fails}

최신 버전의 Jetty와 함께 Dispatcher 4.1.5를 사용하는 경우 요청이 시간 초과될 때까지 기다린 후 다시 가져오기를 수행하면 &quot;원격 서버에서 응답을 받을 수 없음&quot;이 발생할 수 있습니다.

Dispatcher 4.1.6 이상을 사용하면 이 문제가 해결됩니다.

### CQ 5.4에서 업그레이드한 후 포럼 Post에 액세스할 수 없음 {#cannot-access-forum-post-after-upgrading-from-cq}

CQ 5.4에 포럼을 만들고 주제를 게시한 다음 사이트를 AEM 5.6.1 이상으로 업그레이드한 경우 기존 게시물을 보려고 하면 페이지에 오류가 발생할 수 있습니다.

패턴 문자 &#39;a&#39;가 잘못되었습니다.
이 서버의 `/content/demoforums/forum-test.html`에 요청을 제공할 수 없으며 로그에 다음 항목이 포함되어 있습니다.

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

문제는 com.day.cq.commons.date.RelativeTimeFormat의 형식 문자열이 5.4와 5.5 사이에서 변경되어 &quot;ago&quot;에 대한 &quot;a&quot;가 더 이상 허용되지 않는다는 것입니다.

따라서 RelativeTimeFormat() API를 사용하는 모든 코드는 변경해야 합니다.

* 보낸 사람: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* 받는 사람: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

실패는 작성자와 Publish에서 다릅니다. 작성자의 경우 자동으로 실패하고 포럼 주제가 표시되지 않습니다. Publish에서 페이지에 오류가 발생합니다.

자세한 내용은 [com.day.cq.commons.date.RelativeTimeFormat](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) API를 참조하십시오.

## 일반적인 문제 {#common-concerns}

### 로그의 경고: 핸들바가 더 이상 사용되지 않음 {#warning-in-logs-handlebars-deprecated}

시작할 때(처음이 아니라 그 이후마다) 다음 경고가 로그에 표시될 수 있습니다.

* `11.04.2014 08:38:07.223 WARN [FelixStartLevel]com.github.jknack.handlebars.Handlebars Helper 'i18n'`이(가) `com.adobe.cq.social.handlebars.I18nHelper@15bac645`(으)로 대체되었습니다.

[SCF](scf.md#handlebarsjavascripttemplatinglanguage)에서 사용하는 `jknack.handlebars.Handlebars`에 자체 i18n 도우미 유틸리티가 포함되어 있으므로 이 경고는 무시해도 됩니다. 시작할 때 AEM 관련 [i18n 도우미](handlebars-helpers.md#i-n)(으)로 대체됩니다. 이 경고는 기존 도우미의 재정의를 확인하기 위해 서드파티 라이브러리에서 생성됩니다.

### 로그의 경고: OakResourceListener processOsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

여러 소셜 커뮤니티 포럼 주제를 게시하면 OakResourceListener processOsgiEventQueue에서 엄청난 양의 경고 및 정보 로그가 발생할 수 있습니다.

이러한 경고는 무시해도 됩니다.

```xml
23.04.2014 14:21:18.900 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.frq/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.908 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.prx/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
```

### 로그 오류: IndexElementFactory에 대한 NoClassDefFoundError {#error-in-logs-noclassdeffounderror-for-indexelementfactory}

AEM 5.6.1을 최신 cq-socialcommunities-pkg-1.4.x 또는 AEM 6.0으로 업그레이드하면 로그 파일에 오류가 발생합니다. 이 문제는 시작 중에 발생하며, 재시작 시 표시되지 않는 오류로 인해 자체적으로 해결됩니다.

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
