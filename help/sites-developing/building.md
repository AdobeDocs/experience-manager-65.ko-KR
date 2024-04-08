---
title: AEM 애플리케이션에 태깅 작성
description: 프로그래밍 방식으로 사용자 지정 AEM 애플리케이션 내에서 태그를 사용하거나 태그를 확장하십시오
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
feature: Tagging
exl-id: d885520d-d0ed-45fa-8511-faa2495d667a
solution: Experience Manager, Experience Manager Sites
source-git-commit: f22f51b4d65abf4cf1f6e04952f873eca5119727
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 0%

---

# AEM 애플리케이션에 태깅 작성{#building-tagging-into-an-aem-application}

프로그래밍 방식으로 태그를 사용하거나 사용자 지정 AEM 응용 프로그램 내에서 태그를 확장하기 위해 이 페이지에서는

* [태그 지정 API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/tagging/package-summary.html)

와 상호 작용합니다.

* [태깅 프레임워크](/help/sites-developing/framework.md)

태그 지정에 대한 관련 정보는 를 참조하십시오.

* [태그 관리](/help/sites-administering/tags.md) 태그 작성 및 관리 방법과 컨텐츠 태그가 적용되는 항목에 대한 정보입니다.
* [태그 사용](/help/sites-authoring/tags.md) 콘텐츠에 태그 지정에 대한 자세한 내용을 참조하십시오.

## 태깅 API 개요 {#overview-of-the-tagging-api}

의 구현 [태깅 프레임워크](/help/sites-developing/framework.md) AEM에서는 JCR API 를 사용하여 태그 및 태그 컨텐츠를 관리할 수 있습니다. TagManager는 태그에 값으로 입력된 태그가 `cq:tags` 문자열 배열 속성은 복제되지 않으며, 존재하지 않는 태그를 가리키는 TagID를 제거하고, 이동되거나 병합된 태그에 대해 TagID를 업데이트합니다. TagManager는 잘못된 변경 사항을 모두 되돌리는 JCR 관찰 리스너를 사용합니다. 기본 클래스는 [com.day.cq.tagging](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/package-summary.html) 패키지:

* JcrTagManagerFactory - 의 JCR 기반 구현을 반환합니다. `TagManager`. 태깅 API의 참조 구현입니다.
* `TagManager` - 경로 및 이름별로 태그를 해결하고 만들 수 있습니다.
* `Tag` - 태그 개체를 정의합니다.

### JCR 기반 TagManager 가져오기 {#getting-a-jcr-based-tagmanager}

TagManager 인스턴스를 검색하려면 JCR이 있어야 합니다 `Session` 및 호출 `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

일반적인 Sling 컨텍스트에서 `TagManager` 다음에서 `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Tag 개체 검색 {#retrieving-a-tag-object}

A `Tag` 를 통해 검색할 수 있습니다. `TagManager`기존 태그를 해결하거나 태그를 만들어 다음을 수행합니다.

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

JCR 기반 구현의 경우, `Tags` JCR로 `Nodes`, Sling의 `adaptTo` 리소스가 있는 경우 메커니즘(예: `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

태그는 *에서 (노드가 아닌) 리소스 *로만 *변환할 수 있지만 태그는 *에서 노드 및 리소스 *로 *변환할 수 있습니다.

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>에서 직접 적용 `Node` 끝 `Tag` 은(는) 다음과 같은 이유로 불가능 합니다. `Node` Sling을 구현하지 않습니다 `Adaptable.adaptTo(Class)` 메서드를 사용합니다.

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
>유효 `RangeIterator` 을(를) 사용하는 방법은 다음과 같습니다.
>
>`com.day.cq.commons.RangeIterator`

### 태그 삭제 {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### 태그 복제 {#replicating-tags}

복제 서비스( `Replicator`태그가 유형이므로 태그가 있는 ) `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## 클라이언트측 태깅 {#tagging-on-the-client-side}

양식 위젯 `CQ.tagging.TagInputField` 는 태그를 입력하기 위한 것입니다. 기존 태그에서 선택할 수 있는 팝업 메뉴가 있으며, 자동 완성 및 기타 다양한 기능을 포함합니다. xtype은 입니다. `tags`.

## 태그 가비지 수집기 {#the-tag-garbage-collector}

태그 가비지 수집기는 숨겨진 태그와 사용되지 않은 태그를 정리하는 백그라운드 서비스입니다. 숨겨진 태그와 사용하지 않은 태그는 아래 태그입니다. `/content/cq:tags` 이(가) 있습니다. `cq:movedTo` 속성 및 는 콘텐츠 노드에서 사용되지 않으며, 카운트가 0입니다. 이 지연 삭제 프로세스를 사용하여 콘텐츠 노드(즉, `cq:tags` 이동 또는 병합 작업의 일부로 업데이트할 필요가 없습니다. 의 참조 `cq:tags` 속성은 다음 경우에 자동으로 업데이트됩니다. `cq:tags` 속성은 예를 들어 페이지 속성 대화 상자를 통해 업데이트됩니다.

태그 가비지 수집기는 기본적으로 하루에 한 번 실행됩니다. 다음 위치에서 구성할 수 있습니다.

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## 태그 검색 및 태그 목록 {#tag-search-and-tag-listing}

태그 검색 및 태그 목록은 다음과 같이 작동합니다.

* TagID 검색은 속성이 있는 태그를 검색합니다 `cq:movedTo` 를 TagID로 설정하고 를 통해 `cq:movedTo` 태그 ID.

* 태그 제목 검색은 가 없는 태그만 검색합니다 `cq:movedTo` 속성.

## 다른 언어로 된 태그 {#tags-in-different-languages}

태그 관리 설명서의 섹션에 설명된 대로 [다른 언어로 태그 관리](/help/sites-administering/tags.md#managing-tags-in-different-languages), 태그 `title`다른 언어로 정의할 수 있습니다. 그런 다음 언어 구분 속성이 태그 노드에 추가됩니다. 이 속성은 형식을 갖습니다. `jcr:title.<locale>`, 예: `jcr:title.fr` 프랑스어 번역. 다음 `<locale>` 은(는) 소문자 ISO 로케일 문자열이어야 하며, &quot;-&quot; 대신 &quot;_&quot;를 사용합니다. 예: `de_ch`.

다음의 경우 **동물** 태그가 다음에 추가됩니다 **제품** 페이지, 값 `stockphotography:animals` 이 속성에 추가됩니다 `cq:tags` /content/geometrixx/en/products/jcr:content 노드의 입니다. 번역은 태그 노드에서 참조됩니다.

서버측 API가 현지화되었습니다. `title`-관련 메서드:

* [com.day.cq.tagging.Tag](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle(로케일)
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle(로케일)
   * getTitlePath(로케일)

* [com.day.cq.tagging.TagManager](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath, Locale)
   * createTagByTitle(String tagTitlePath, Locale)
   * resolveByTitle(String tagTitlePath, Locale)

AEM에서 언어는 페이지 언어 또는 사용자 언어에서 가져올 수 있습니다.

* jsp에서 페이지 언어를 검색하려면 다음을 수행하십시오.

   * `currentPage.getLanguage(false)`

* jsp에서 사용자 언어를 검색하려면 다음을 수행하십시오.

   * `slingRequest.getLocale()`

다음 `currentPage` 및 `slingRequest` 를 통해 JSP에서 사용할 수 있습니다. [&lt;cq:definedobjects>](/help/sites-developing/taglib.md) 태그에 가깝게 배치하십시오.

태깅의 경우 현지화는 컨텍스트에 따라 태그로 달라집니다 `titles`페이지 언어, 사용자 언어 또는 다른 언어로 표시할 수 있습니다.

### 태그 편집 대화 상자에 새 언어 추가 {#adding-a-new-language-to-the-edit-tag-dialog}

다음 절차에서는 언어(핀란드어)를 **태그 편집** 대화 상자:

1. 위치 **CRXDE**, 다중 값 속성 편집 `languages` 노드의 `/content/cq:tags`.

1. 추가 `fi_fi` - 핀란드어 로케일을 나타내며 변경 사항을 저장합니다.

이제 페이지 속성의 태그 대화 상자 및 에서 새 언어(핀란드어)를 사용할 수 있습니다 **태그 편집** 에서 태그를 편집할 때 표시되는 대화 상자 **태깅** 콘솔.

>[!NOTE]
>
>새 언어는 AEM에서 인식하는 언어 중 하나여야 합니다. 즉, 아래 노드로 사용할 수 있어야 합니다 `/libs/wcm/core/resources/languages`.

>[!CAUTION]
>
>공식 업데이트 패키지(서비스 팩, 보안 서비스 팩, 확장 기능 팩, 누적 기능 팩, 패치 등)를 통해 태깅 관련 기본 제공 콘텐츠를 설치하면 의 언어 속성이 재설정됩니다. `/content/cq:tags` 노드를 기본값으로 설정합니다. 따라서 설치하기 전에 속성에서 추가해야 합니다.
