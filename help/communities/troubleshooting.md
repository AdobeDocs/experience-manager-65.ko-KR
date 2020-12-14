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
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 1%

---


# 문제 해결 {#troubleshooting}

이 섹션에는 일반적인 문제와 알려진 문제가 포함되어 있습니다.

## 알려진 문제 {#known-issues}

### 디스패처 레퍼치가 {#dispatcher-refetch-fails} 실패

Dispatcher 4.1.5을 최신 버전의 Jetty와 함께 사용할 때 요청이 시간 초과될 때까지 기다린 후 레퍼트로 인해 &#39;원격 서버로부터 응답을 받을 수 없습니다.&#39;가 발생할 수 있습니다.

Dispatcher 4.1.6 이상을 사용하면 이 문제가 해결됩니다.

### CQ 5.4에서 업그레이드 후 포럼 게시물에 액세스할 수 없음 {#cannot-access-forum-post-after-upgrading-from-cq}

CQ 5.4에서 포럼이 만들어졌고 게시한 항목이 AEM 5.6.1 이상으로 업그레이드된 경우 기존 게시물을 보려고 하면 페이지에 오류가 발생할 수 있습니다.

잘못된 패턴 문자 &#39;a&#39;
이 서버의 `/content/demoforums/forum-test.html`에 요청을 제공할 수 없으며 로그에 다음이 포함됩니다.

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

문제는 com.day.cq.commons.date.RelativeTimeFormat의 형식 문자열이 5.4에서 5.5 사이에 변경되었으므로 &quot;ago&quot;의 &quot;a&quot;가 더 이상 허용되지 않습니다.

따라서 RelativeTimeFormat() API를 사용하는 모든 코드는 다음과 같이 변경해야 합니다.

* 시작: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* 끝: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

작성자 및 게시 시 오류가 다릅니다. 작성자는 자동으로 실패하며 포럼 항목을 표시하지 않습니다. 게시하면 페이지에 오류가 표시됩니다.

자세한 내용은 [com.day.cq.commons.date.RelativeTimeFormat](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) API를 참조하십시오.

## 일반적인 문제 {#common-concerns}

### 로그인 경고:Handlebars 더 이상 사용되지 않음 {#warning-in-logs-handlebars-deprecated}

시작 시(1일이 아니라 1일 이후 모든 항목) 로그에 다음 경고가 표시될 수 있습니다.

* `11.04.2014 08:38:07.223 WARN [FelixStartLevel]com.github.jknack.handlebars.Handlebars Helper 'i18n'` 의  `com.adobe.cq.social.handlebars.I18nHelper@15bac645`

이 경고는 [SCF](scf.md#handlebarsjavascripttemplatinglanguage)에서 사용하는 `jknack.handlebars.Handlebars`에 자체 i18n 도우미 유틸리티가 함께 제공되므로 안전하게 무시될 수 있습니다. 시작할 때 AEM 관련 [i18n 도우미](handlebars-helpers.md#i-n)로 대체됩니다. 이 경고는 기존 도우미의 재정의를 확인하기 위해 제3자 라이브러리에 의해 생성됩니다.

### 로그인 경고:OakResourceListener processOsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

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

### 로그 오류:IndexElementFactory {#error-in-logs-noclassdeffounderror-for-indexelementfactory}에 대한 NoClassDefFoundError

AEM 5.6.1 GA를 최신 cq-socialcommunities-pkg-1.4.x 또는 AEM 6.0으로 업그레이드하면 시작 중에 로그 파일에서 오류가 발생하고 다시 시작할 때 나타나지 않는 오류가 발생하는 것으로 확인됩니다.

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
