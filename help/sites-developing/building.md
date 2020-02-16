---
title: AEM 애플리케이션에 태그 지정 작성
seo-title: AEM 애플리케이션에 태그 지정 작성
description: 사용자 지정 AEM 애플리케이션 내에서 태그를 사용하여 프로그래밍 방식으로 작업하거나 태그 확장
seo-description: 사용자 지정 AEM 애플리케이션 내에서 태그를 사용하여 프로그래밍 방식으로 작업하거나 태그 확장
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# AEM 애플리케이션에 태그 지정 작성{#building-tagging-into-an-aem-application}

이 페이지에서는 사용자 지정 AEM 애플리케이션 내에서 태그를 프로그래밍 방식으로 작업하거나 태그를 확장하기 위해

* [Tagging API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

그리고

* [Tagging 프레임워크](/help/sites-developing/framework.md)

태그 지정에 대한 관련 정보는 다음을 참조하십시오.

* [태그](/help/sites-administering/tags.md) 관리를 참조하십시오.
* [태그](/help/sites-authoring/tags.md) 사용을 참조하십시오.

## Tagging API 개요 {#overview-of-the-tagging-api}

AEM에서 [태그 지정 프레임워크를](/help/sites-developing/framework.md) 구현하면 JCR API를 사용하여 태그 및 태그 컨텐츠를 관리할 수 있습니다. TagManager를 사용하면 `cq:tags` 문자열 배열 속성에 값으로 입력된 태그가 중복되지 않고, 기존 태그가 아닌 태그를 가리키는 TagID가 제거되고, 이동되거나 병합된 태그에 대한 TagID가 업데이트됩니다. TagManager는 잘못된 변경 사항을 되돌리는 JCR 관측 리스너를 사용합니다. 기본 클래스는 com.day.cq.ta [태깅](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) 패키지에 있습니다.

* JcrTagManagerFactory - JCR 기반 JavaScript 구현의 `TagManager`구현을 반환합니다. Tagging API의 참조 구현입니다.
* `TagManager` - 경로 및 이름별로 태그를 확인하고 만들 수 있습니다.
* `Tag` - 태그 개체를 정의합니다.

### JCR 기반 TagManager 가져오기 {#getting-a-jcr-based-tagmanager}

TagManager 인스턴스를 검색하려면 JCR이 있어야 `Session` 하며 `getTagManager(Session)`다음을 호출해야 합니다.

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

일반적인 Sling 컨텍스트에서는 다음을 `TagManager` 기준으로 적용할 수도 `ResourceResolver`있습니다.

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### 태그 개체 검색 {#retrieving-a-tag-object}

A `Tag` 는 기존 태그를 `TagManager`확인하거나 새 태그를 만들어

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

JCR 기반 구현의 경우, JCR `Tags` 에 매핑되는 `Nodes`경우 리소스(예: `adaptTo` `/etc/tags/default/my/tag`다음과 같은)가 있는 경우 Sling의 메커니즘을 직접 사용할 수 있습니다.

```java
Tag tag = resource.adaptTo(Tag.class);
```

태그는 *a 리소스에서 *로 변환할 수 있지만(노드는 아님), 태그는 *와 노드 모두로 변환할 수 있습니다.

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>Sling `Node` 메서드를 구현하지 `Tag` 않기 때문에 에서 에 직접 적용할 `Node` `Adaptable.adaptTo(Class)` 수 없습니다.

### 태그 가져오기 및 설정 {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### 태그 검색 {#searching-for-tags}

```java
// Searching for the Resource objects that are tagged with the tag object:
Iterator<Resource> it = tag.find();

// Retrieving the usage count of the tag object:
long count = tag.getCount();

// Searching for the Resource objects that are tagged with the tagID String:
 RangeIterator<Resource> it = tagManager.find(tagID);
```

>[!NOTE]
>
>유효한 `RangeIterator` 사용 방법은 다음과 같습니다.
>
>`com.day.cq.commons.RangeIterator`

### 태그 삭제 {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### 태그 복제 {#replicating-tags}

태그는 다음과 같은 유형이므로 태그와 함께 복제 서비스( `Replicator`)를 사용할 수 `nt:hierarchyNode`있습니다.

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## 클라이언트 측의 태그 지정 {#tagging-on-the-client-side}

`CQ.tagging.TagInputField` 는 태그 입력을 위한 양식 위젯입니다. 기존 태그, 자동 완성 및 기타 많은 기능을 포함하는 팝업 메뉴가 있습니다. xtype `tags`입니다.

## 태그 가비지 수집기 {#the-tag-garbage-collector}

태그 가비지 수집기는 숨겨지고 사용하지 않는 태그를 정리하는 백그라운드 서비스입니다. 숨겨진 태그와 사용하지 않는 태그는 `/etc/tags` `cq:movedTo` 속성이 있고 컨텐트 노드에서 사용되지 않는 아래에 있는 태그입니다. 이 태그는 카운트가 0입니다. 이 레이지 삭제 프로세스를 사용하면 컨텐츠 노드(즉, `cq:tags` 속성)를 이동 또는 병합 작업의 일부로 업데이트할 필요가 없습니다. 속성 `cq:tags` 참조는 페이지 속성 대화 상자를 통해 `cq:tags` 속성이 업데이트되면 자동으로 업데이트됩니다.

태그 가비지 수집기는 기본적으로 하루에 한 번 실행됩니다. 다음 위치에서 구성할 수 있습니다.

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## 태그 검색 및 태그 목록 {#tag-search-and-tag-listing}

태그 및 태그 목록 검색은 다음과 같이 작동합니다.

* TagID를 검색하면 속성이 TagID로 `cq:movedTo` 설정되고 TagID를 통해 이어지는 태그를 `cq:movedTo` 검색합니다.

* 태그 제목 검색은 `cq:movedTo` 속성이 없는 태그만 검색합니다.

## Tags in Different Languages {#tags-in-different-languages}

태그 관리 설명서의 다른 언어로 태그 관리 섹션에서 태그를 [다른](/help/sites-administering/tags.md#managing-tags-in-different-languages)언어로 정의할 `title`수 있습니다. 언어 감지 속성이 태그 노드에 추가됩니다. 이 속성은 프랑스어 번역과 `jcr:title.<locale>`같은 형식을 `jcr:title.fr` 갖습니다. `<locale>` 는 소문자 ISO 로케일 문자열과 &quot;-&quot; 대신 &quot;_&quot;를 사용해야 합니다. 예를 들면 다음과 같습니다. `de_ch`Adobe

Animals **태그가** Products **** 페이지에 추가되면 `stockphotography:animals` 값이 /content/geometrixx/en/products/jcr:content `cq:tags` 노드의 속성에 추가됩니다. 변환은 태그 노드에서 참조됩니다.

서버측 API에 지역화된 `title`관련 방법이 있습니다.

* [com.day.cq.taging.Tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle(로케일)
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle(로케일)
   * getTitlePath(로케일)

* [com.day.cq.taging.TagManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath, Locale)
   * createTagByTitle(String tagTitlePath, Locale)
   * resolveByTitle(문자열 tagTitlePath, 로케일)

AEM에서 언어는 페이지 언어 또는 사용자 언어로 가져올 수 있습니다.

* jsp에서 페이지 언어를 검색하려면 다음을 수행합니다.

   * `currentPage.getLanguage(false)`

* jsp에서 사용자 언어를 검색하려면 다음을 수행합니다.

   * `slingRequest.getLocale()`

`currentPage` JSP에서 `slingRequest` &lt;cq:definedObjects> [](/help/sites-developing/taglib.md) 태그를 통해 사용할 수 있습니다.

태깅의 경우, 현지화는 페이지 언어, 사용자 언어 또는 다른 언어로 태그를 표시할 `titles`수 있으므로 컨텍스트에 따라 달라집니다.

### 태그 편집 대화 상자에 새 언어 추가 {#adding-a-new-language-to-the-edit-tag-dialog}

다음 절차에서는 새 언어(핀란드어)를 태그 편집 **대화 상자에 추가하는 방법에 대해** 설명합니다.

1. CRXDE **에서**&#x200B;노드의 다중 값 `languages` 속성을 `/etc/tags`편집합니다.

1. 핀란드어 로케일을 나타내는 `fi_fi` - 을 추가하고 변경 내용을 저장합니다.

이제 태그 지정 콘솔에서 태그를 편집할 때 페이지 속성의 태그 대화 상자와 태그 **편집** 대화 상자에서 새 언어(핀란드어)를 사용할 수 **있습니다** .

>[!NOTE]
>
>새 언어는 AEM에서 인식되는 언어 중 하나가 되어야 합니다. 즉, 아래 `/libs/wcm/core/resources/languages`노드로 사용할 수 있어야 합니다.

