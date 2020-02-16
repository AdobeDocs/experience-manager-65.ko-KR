---
title: 문제 해결
seo-title: 문제 해결
description: 알려진 문제를 포함한 커뮤니티 문제 해결
seo-description: 알려진 문제를 포함한 커뮤니티 문제 해결
uuid: 99225430-fa2a-4393-ae5a-18b19541c358
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cdb2d80a-2fbf-4ee6-b89b-b5d74e6d3bfc
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 문제 해결 {#troubleshooting}

이 섹션에는 일반적인 문제와 알려진 문제가 포함되어 있습니다.

## 알려진 문제 {#known-issues}

### 발송자 참조 실패 {#dispatcher-refetch-fails}

Dispatcher 4.1.5를 최신 버전의 Jetty와 함께 사용하는 경우 요청이 시간 초과될 때까지 기다린 후 레퍼트로 인해 &#39;원격 서버로부터 응답을 받을 수 없습니다&#39;가 발생할 수 있습니다.

Dispatcher 4.1.6 이상을 사용하면 이 문제가 해결됩니다.

### CQ 5.4에서 업그레이드 후 포럼 게시물에 액세스할 수 없음 {#cannot-access-forum-post-after-upgrading-from-cq}

CQ 5.4에서 포럼이 만들어졌고 게시된 항목이 사이트를 AEM 5.6.1 이상으로 업그레이드한 경우 기존 게시물을 보려고 하면 페이지에 오류가 발생할 수 있습니다.

이 서버의 /content/demoforums/forum-test.html에 요청을 제공할 수 없는 패턴 문자 &#39;a&#39;가 잘못되었습니다.

그리고 로그에는 다음이 포함됩니다.

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

문제는 com.day.cq.commons.date.RelativeTimeFormat의 형식 문자열이 5.4에서 5.5 사이에 변경되었으므로 &quot;ago&quot;의 &quot;a&quot;가 더 이상 허용되지 않습니다.

따라서 RelativeTimeFormat() API를 사용하는 모든 코드는

* 시작: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* 끝: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

작성자 및 게시에서 오류가 다릅니다. 작성자는 자동으로 실패하며 포럼 주제가 표시되지 않습니다. 게시하면 페이지에 오류가 발생합니다.

자세한 [내용은 com.day.cq.commons.date.RelativeTimeFormat](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) API를 참조하십시오.

## 일반적인 우려 사항 {#common-concerns}

### 로그인 경고:사용되지 않는 handlebars {#warning-in-logs-handlebars-deprecated}

시작 중(1일 제외 - 이후 모든 항목) 로그에 다음 경고가 표시될 수 있습니다.

* 11.04.2014 08:38: **07.223 WARN** WARN []FelixStartLevelcom.github.jknack.handlebars.Handlebars Helper &#39;i18n&#39;이 &#39;com.adobe.cq.social.handlebars.I18nHelper@15bac645&#39;으로 대체되었습니다.

이 경고는 jknack.handlebars.Handlebars로 안전하게 무시될 수 있습니다. SCF에서 사용되는 [Handlebars](scf.md#handlebarsjavascripttemplatinglanguage)는 자체 i18n 도우미 유틸리티를 제공합니다. 시작할 때 AEM 관련 i18n [도우미로](handlebars-helpers.md#i-n)대체됩니다. 이 경고는 기존 도우미의 재정의를 확인하기 위해 타사 라이브러리에서 생성합니다.

### 로그인 경고:OakResourceListener 프로세스OsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

여러 소셜 커뮤니티 포럼 주제를 게시하면 OakResourceListener processOsgiEventQueue에서 대량의 경고 및 정보 로그가 발생할 수 있습니다.

이러한 경고는 안전하게 무시될 수 있습니다.

```xml
23.04.2014 14:21:18.900 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.frq/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.908 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.prx/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
```

### 로그 오류:IndexElementFactory에 대한 NoClassDefFoundError {#error-in-logs-noclassdeffounderror-for-indexelementfactory}

AEM 5.6.1 GA를 최신 cq-socialcommunities-pkg-1.4.x 또는 AEM 6.0으로 업그레이드하면 시작 중에 로그 파일에서 오류가 발생하고 재시작 시 나타나지 않는 오류가 확인됩니다.

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
