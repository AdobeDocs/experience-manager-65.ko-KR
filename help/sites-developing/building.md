---
title: AEM 애플리케이션에 태깅 작성
seo-title: AEM 애플리케이션에 태깅 작성
description: 프로그래밍 방식으로 사용자 지정 AEM 애플리케이션 내에서 태그를 사용하거나 태그를 확장하는 작업을 합니다
seo-description: 프로그래밍 방식으로 사용자 지정 AEM 애플리케이션 내에서 태그를 사용하거나 태그를 확장하는 작업을 합니다
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
feature: 태깅
exl-id: d885520d-d0ed-45fa-8511-faa2495d667a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 2%

---

# AEM 애플리케이션에 태깅 작성{#building-tagging-into-an-aem-application}

사용자 지정 AEM 애플리케이션 내에서 태그를 프로그래밍 방식으로 사용하거나 태그를 확장하는 목적으로 이 페이지에서는

* [태깅 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

와 상호 작용함

* [태깅 프레임워크](/help/sites-developing/framework.md)

태깅에 대한 관련 정보는 다음을 참조하십시오.

* [태그 ](/help/sites-administering/tags.md) 관리 를 참조하십시오.
* [컨텐츠 ](/help/sites-authoring/tags.md) 태깅 정보에 대해서는 Tags 사용을 참조하십시오.

## 태깅 API {#overview-of-the-tagging-api} 개요

AEM에서 [태깅 프레임워크](/help/sites-developing/framework.md)를 구현하면 JCR API 를 사용하여 태그 및 태그 컨텐츠를 관리할 수 있습니다. TagManager를 사용하면 `cq:tags` 문자열 배열 속성에 값으로 입력한 태그가 중복되지 않고 기존 태그가 아닌 태그를 가리키는 TagID가 제거되고 이동되거나 병합된 태그의 TagID가 업데이트됩니다. TagManager는 잘못된 변경 사항을 되돌리는 JCR 관찰 리스너를 사용합니다. 기본 클래스는 [com.day.cq.tagging](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) 패키지에 있습니다.

* JcrTagManagerFactory - `TagManager`의 JCR 기반 구현을 반환합니다. 태깅 API의 참조 구현입니다.
* `TagManager` - 경로 및 이름으로 태그를 확인하고 만들 수 있습니다.
* `Tag` - 태그 개체를 정의합니다.

### JCR 기반 TagManager {#getting-a-jcr-based-tagmanager} 가져오기

TagManager 인스턴스를 검색하려면 JCR `Session`이 있어야 하고 `getTagManager(Session)`를 호출해야 합니다.

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

일반적인 Sling 컨텍스트에서 `ResourceResolver`의 `TagManager`에 적응할 수도 있습니다.

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### 태그 개체 {#retrieving-a-tag-object} 검색

`Tag`은(는) 기존 태그를 확인하거나 새 태그를 만들어 `TagManager`을 통해 검색할 수 있습니다.

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

`Tags`을 JCR `Nodes`에 매핑하는 JCR 기반 구현의 경우, 리소스가 있는 경우(예: `/content/cq:tags/default/my/tag`) Sling의 `adaptTo` 메커니즘을 직접 사용할 수 있습니다.

```java
Tag tag = resource.adaptTo(Tag.class);
```

태그는 *에서 *로(노드가 아님) 변환하기만 할 수 있지만 *로 변환할 수 있는 노드는 노드와 리소스 중 하나입니다.

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>`Node`에서 Sling `Adaptable.adaptTo(Class)` 메서드를 구현하지 않으므로 `Node`에서 `Tag`에 직접 적용할 수 없습니다.

### 태그 {#getting-and-setting-tags} 가져오기 및 설정

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
>사용할 유효한 `RangeIterator`:
>
>`com.day.cq.commons.RangeIterator`

### 태그 삭제 {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### 태그 복제 중 {#replicating-tags}

태그는 `nt:hierarchyNode` 유형이므로 태그와 함께 복제 서비스( `Replicator`)를 사용할 수 있습니다.

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## 클라이언트 측의 태깅 {#tagging-on-the-client-side}

`CQ.tagging.TagInputField` 는 태그를 입력하는 양식 위젯입니다. 기존 태그에서 선택할 수 있는 팝업 메뉴가 있고 자동 완성 및 기타 많은 기능이 포함되어 있습니다. xtype은 `tags`입니다.

## 태그 가비지 수집기 {#the-tag-garbage-collector}

태그 가비지 수집기는 숨겨지고 사용하지 않는 태그를 정리하는 백그라운드 서비스입니다. 숨겨진 태그와 사용하지 않은 태그는 `cq:movedTo` 속성이 있고 컨텐츠 노드에서 사용되지 않는 `/content/cq:tags` 아래의 태그입니다. 개수는 0입니다. 이 지연 삭제 프로세스를 사용하면 컨텐츠 노드(즉, `cq:tags` 속성)를 이동 또는 병합 작업의 일부로 업데이트할 필요가 없습니다. `cq:tags` 속성의 참조는 `cq:tags` 속성이 업데이트될 때(예: 페이지 속성 대화 상자를 통해) 자동으로 업데이트됩니다.

태그 가비지 수집기는 기본적으로 하루에 한 번 실행됩니다. 다음 위치에서 구성할 수 있습니다.

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## 태그 검색 및 태그 목록 {#tag-search-and-tag-listing}

태그 검색 및 태그 목록은 다음과 같이 작동합니다.

* TagID를 검색하면 `cq:movedTo` 속성이 TagID로 설정되고 `cq:movedTo` TagID를 따르는 태그가 검색됩니다.

* 태그 제목 검색은 `cq:movedTo` 속성이 없는 태그만 검색합니다.

## 다른 언어 태그 {#tags-in-different-languages}

태그 관리 설명서에 설명된 대로 [다른 언어로 태그 관리](/help/sites-administering/tags.md#managing-tags-in-different-languages) 섹션에서 `title` 태그를 다른 언어로 정의할 수 있습니다. 그런 다음 언어 구분 속성이 태그 노드에 추가됩니다. 이 속성은 `jcr:title.<locale>` 형식을 갖습니다(예: ).프랑스어 번역을 위한 `jcr:title.fr` 입니다. `<locale>` 소문자 ISO 로케일 문자열이어야 하며, 예를 들어, &quot;-&quot; 대신 &quot;_&quot;를 사용해야 합니다. `de_ch`.

**Animals** 태그가 **Products** 페이지에 추가되면 `stockphotography:animals` 값이 /content/geometrixx/en/products/jcr:content 노드의 `cq:tags` 속성에 추가됩니다. 번역이 태그 노드에서 참조됩니다.

서버측 API가 현지화된 `title` 관련 메서드:

* [com.day.cq.tagging.Tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle(로케일)
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle(로케일)
   * getTitlePath(로케일)

* [com.day.cq.tagging.TagManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath, 로케일)
   * createTagByTitle(String tagTitlePath, 로케일)
   * resolveByTitle(String tagTitlePath, 로케일)

AEM에서 언어는 페이지 언어나 사용자 언어로 가져올 수 있습니다.

* JSP에서 페이지 언어를 검색하려면 다음을 수행하십시오.

   * `currentPage.getLanguage(false)`

* JSP에서 사용자 언어를 검색하려면 다음을 수행하십시오.

   * `slingRequest.getLocale()`

`currentPage` 및  `slingRequest` 는 태그를 통해 JSP에서 사용할 수  [&lt;cq:definedobjects>](/help/sites-developing/taglib.md) 있습니다.

태깅의 경우 현지화는 태그 `titles`이 페이지 언어, 사용자 언어 또는 다른 언어로 표시될 수 있으므로 컨텍스트에 따라 다릅니다.

### 태그 편집 대화 상자에 새 언어 추가 {#adding-a-new-language-to-the-edit-tag-dialog}

다음 절차에서는 **태그 편집** 대화 상자에 새 언어(핀란드어)를 추가하는 방법에 대해 설명합니다.

1. **CRXDE**&#x200B;에서 `/content/cq:tags` 노드의 다중 값 속성 `languages`을 편집합니다.

1. 핀란드의 로케일을 나타내는 `fi_fi` 을 추가하고 변경 내용을 저장합니다.

이제 **Tagging** 콘솔에서 태그를 편집할 때 페이지 속성의 태그 대화 상자 및 **태그 편집** 대화 상자에서 새 언어(핀란드어)를 사용할 수 있습니다.

>[!NOTE]
>
>새 언어는 AEM에서 인식하는 언어 중 하나여야 합니다. 즉, `/libs/wcm/core/resources/languages` 아래의 노드로 사용할 수 있어야 합니다.
