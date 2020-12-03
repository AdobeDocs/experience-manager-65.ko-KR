---
title: AEM 태깅 프레임워크
seo-title: AEM 태깅 프레임워크
description: 컨텐츠에 태그를 지정하고 AEM Tagging 인프라 활용
seo-description: 컨텐츠에 태그를 지정하고 AEM Tagging 인프라 활용
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1915'
ht-degree: 1%

---


# AEM 태깅 프레임워크 {#aem-tagging-framework}

컨텐츠에 태그를 지정하고 AEM Tagging 인프라를 활용하려면

* 태그는 [분류 루트 노드](#taxonomy-root-node) 아래에 ` [cq:Tag](#tags-cq-tag-node-type)` 유형의 노드로 있어야 합니다.

* 태그가 지정된 콘텐츠 노드의 NodeType에는 [ `cq:Taggable`](#taggable-content-cq-taggable-mixin) 믹신이 포함되어야 합니다.
* [TagID](#tagid)가 컨텐트 노드의 [ `cq:tags`](#tagged-content-cq-tags-property) 속성에 추가되고 ` [cq:Tag](#tags-cq-tag-node-type)` 유형의 노드로 확인됩니다.

## 태그:cq:태그 노드 유형 {#tags-cq-tag-node-type}

태그의 선언이 저장소에서 `cq:Tag.` 유형의 노드에 캡처됩니다

태그는 단순한 단어(예: 하늘)이거나 계층 분류(예: 과일/apple)를 나타낼 수 있습니다. 예를 들어 일반 과일과 보다 구체적인 apple을 모두 의미합니다.

태그는 고유한 TagID로 식별됩니다.

태그에는 제목, 지역화된 제목 및 설명과 같은 메타 정보가 선택 사항입니다. 제목은 TagID가 아닌 사용자 인터페이스에 표시되어야 합니다.

태깅 프레임워크에서는 작성자 및 사이트 방문자가 사전 정의된 특정 태그만 사용하도록 제한하는 기능도 제공합니다.

### 태그 특성 {#tag-characteristics}

* node type is `cq:Tag`
* node name is a component of ` [TagID](#tagid)`
* ` [TagID](#tagid)`에는 항상 [namespace](#tag-namespace)가 포함됩니다.

* 선택 사항 `jcr:title` 속성(UI에 표시할 제목)

* 선택 사항 `jcr:description` 속성

* 하위 노드를 포함하는 경우 [컨테이너 태그](#container-tags)로 참조됩니다.
* 는 [분류 루트 노드](#taxonomy-root-node)라는 기본 경로 아래의 저장소에 저장됩니다.

### 태그 ID {#tagid}

TagID는 저장소의 태그 노드로 해결하는 경로를 식별합니다.

일반적으로 TagID는 네임스페이스로 시작하는 축약형 TagID이거나 [분류 루트 노드](#taxonomy-root-node)부터 시작하는 절대 TagID일 수 있습니다.

컨텐츠에 태그를 지정하면 아직 존재하지 않으면 ` [cq:tags](#tagged-content-cq-tags-property)` 속성이 컨텐츠 노드에 추가되고 TagID가 속성의 String 배열 값에 추가됩니다.

TagID는 [namespace](#tag-namespace) 다음에 로컬 TagID로 구성됩니다. [분류](#container-tags) 에서 계층 순서를 나타내는 컨테이너 태그입니다. 하위 태그를 사용하여 로컬 TagID와 동일한 태그를 참조할 수 있습니다. 예를 들어 &quot;과일&quot; 및 &quot;과일/바나나&quot;와 같은 하위 태그가 포함된 컨테이너 태그라도 &quot;과일&quot;이 포함된 컨텐츠에 태깅할 수 있습니다.

### 분류 루트 노드 {#taxonomy-root-node}

분류 루트 노드는 저장소의 모든 태그에 대한 기본 경로입니다. 분류 루트 노드는 *이 아닌*&#x200B;이어야 합니다.`  cq   :Tag`

AEM에서 기본 경로는 `/content/  cq   :tags`이고 루트 노드는 `  cq   :Folder` 형식입니다.

### 태그 네임스페이스 {#tag-namespace}

네임스페이스를 통해 여러 항목을 그룹화할 수 있습니다. 가장 일반적인 사용 사례는 (웹) 사이트당(예: 공개, 내부 및 포털) 또는 더 큰 응용 프로그램(예: WCM, 자산, 커뮤니티)당 네임스페이스를 갖는 것이지만 다른 다양한 요구 사항에 네임스페이스를 사용할 수 있습니다. 네임스페이스는 사용자 인터페이스에서 현재 컨텐츠에 적용할 수 있는 태그의 하위 집합(즉, 특정 네임스페이스의 태그)만 표시하는 데 사용됩니다.

태그의 네임스페이스는 분류 하위 트리에서 첫 번째 레벨이며, 분류법 루트 노드[ 바로 아래의 노드입니다. ](#taxonomy-root-node) 네임스페이스는 상위 항목이 `cq:Tag`노드 유형이 아닌 `cq:Tag` 유형의 노드입니다.

모든 태그에는 네임스페이스가 있습니다. 네임스페이스를 지정하지 않으면 태그가 기본 네임스페이스에 지정되며, 이 네임스페이스는 TagID `default`(제목이 `Standard Tags),`이고, `/content/cq:tags/default.`

### 컨테이너 태그 {#container-tags}

컨테이너 태그는 임의 개수와 유형의 하위 노드를 포함하는 `cq:Tag` 유형의 노드로서, 사용자 지정 메타데이터로 태그 모델을 향상시킬 수 있습니다.

또한 택소노미의 컨테이너 태그(또는 super 태그)는 모든 하위 태그의 하위 합계로 사용됩니다.예를 들어, 과일/apple 태그가 지정된 컨텐츠에 과일도 태그가 지정된 것으로 간주됩니다. 예를 들어, 과일 태그가 지정된 컨텐츠를 검색하면 과일/apple 태그가 지정된 컨텐츠도 검색됩니다.

### TagID를 확인하는 중 {#resolving-tagids}

태그 ID에 콜론 &quot;:&quot;이 포함된 경우 콜론은 네임스페이스를 태그 또는 하위 분류에서 분리한 다음 일반 슬래시 &quot;/&quot;로 구분됩니다. 태그 ID에 콜론이 없는 경우 기본 네임스페이스가 묵시적으로 사용됩니다.

태그의 표준 및 전용 위치는 /content/cq:tags 아래에 있습니다.

cq:Tag 노드를 가리키지 않는 기존 경로 또는 경로를 참조하는 태그는 잘못된 것으로 간주되며 무시됩니다.

다음 표는 일부 샘플 TagID, 해당 요소 및 TagID가 저장소의 절대 경로로 어떻게 확인하는지를 보여줍니다.

다음 표는 일부 샘플 TagID, 해당 요소 및 TagID가 저장소의 절대 경로로 어떻게 확인하는지를 보여줍니다.
다음 표는 일부 샘플 TagID, 해당 요소 및 TagID가 저장소의 절대 경로로 어떻게 확인하는지를 보여줍니다.

<table>
 <tbody>
  <tr>
   <td><strong>태그 ID<br /> </strong></td>
   <td><strong>네임스페이스</strong></td>
   <td><strong>로컬 ID</strong></td>
   <td><strong>컨테이너 태그</strong></td>
   <td><strong>리프 태그</strong></td>
   <td><strong>저장소<br /> 절대 태그 경로</strong></td>
  </tr>
  <tr>
   <td>댐:과일/사과/뇌</td>
   <td>댐</td>
   <td>과일/사과/뇌</td>
   <td>과일, 사과</td>
   <td>뇌</td>
   <td>/content/cq:tags/dam/fruit/apple/brereburn</td>
  </tr>
  <tr>
   <td>색상/빨강</td>
   <td>기본값</td>
   <td>색상/빨강</td>
   <td>컬러</td>
   <td>red</td>
   <td>/content/cq:tags/default/color/red</td>
  </tr>
  <tr>
   <td>하늘</td>
   <td>기본값</td>
   <td>하늘</td>
   <td>(없음)</td>
   <td>하늘</td>
   <td>/content/cq:tags/default/sky</td>
  </tr>
  <tr>
   <td>dam:</td>
   <td>댐</td>
   <td>(없음)</td>
   <td>(없음)</td>
   <td>(none, 네임스페이스)</td>
   <td>/content/cq:tags/dam</td>
  </tr>
  <tr>
   <td>/content/cq:tags/category/car</td>
   <td>category</td>
   <td>자동차</td>
   <td>자동차</td>
   <td>자동차</td>
   <td>/content/cq:tags/category/car</td>
  </tr>
 </tbody>
</table>

### 태그 제목 {#localization-of-tag-title} 현지화

태그에 선택적 제목 문자열( `jcr:title`)이 포함되어 있으면 속성 `jcr:title.<locale>`을 추가하여 표시할 제목을 현지화할 수 있습니다.

자세한 내용은

* [다른 언어의](/help/sites-developing/building.md#tags-in-different-languages)  태그 - API의 사용을 설명합니다.
* [태그 관리 콘솔 사용을](/help/sites-administering/tags.md#managing-tags-in-different-languages)  설명하는 여러 언어로 태그 관리

### 액세스 제어 {#access-control}

태그는 [분류 루트 노드](#taxonomy-root-node) 아래의 저장소에 노드로 존재합니다. 작성자와 사이트 방문자가 주어진 네임스페이스에 태그를 만들 수 있도록 허용하거나 거부하려면 저장소에서 적절한 ACL을 설정하여 이를 수행할 수 있습니다.

또한 태그 또는 네임스페이스에 대한 읽기 권한을 거부하면 특정 콘텐츠에 태그를 적용하는 기능이 제어됩니다.

일반적인 방법은 다음과 같습니다.

* `tag-administrators` 그룹/역할 쓰기 액세스 허용(`/content/cq:tags`에서 추가/수정). 이 그룹에는 최신 AEM이 포함되어 있습니다.

* 사용자/작성자가 읽을 수 있어야 하는 모든 네임스페이스에 대한 읽기 권한을 부여할 수 있습니다(대부분 모두).
* 사용자/작성자가 사용자/작성자가 태그를 자유롭게 정의해야 하는 네임스페이스에 대한 쓰기 액세스 허용(`/content/cq:tags/some_namespace` 아래에 add_node)

## 태그가능 컨텐츠:cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

애플리케이션 개발자가 컨텐트 유형에 태깅을 첨부하려면 노드의 등록([CND](https://jackrabbit.apache.org/node-type-notation.html))에 `cq:Taggable` 믹싱 또는 `cq:OwnerTaggable` 믹신이 포함되어야 합니다.

`cq:Taggable`에서 상속되는 `cq:OwnerTaggable` 혼합은 컨텐츠가 소유자/작성자에 의해 분류될 수 있음을 나타내기 위한 것입니다. AEM에서는 `cq:PageContent` 노드의 속성만 나타냅니다. 태그 프레임워크에는 `cq:OwnerTaggable` 혼합이 필요하지 않습니다.

>[!NOTE]
>
>집계된 컨텐츠 항목(또는 jcr:content 노드)의 최상위 노드에서만 태그를 활성화하는 것이 좋습니다. 예:
>
>* 페이지( `cq:Page`). 여기서 `jcr:content`노드는 `cq:Taggable` 믹싱을 포함하는 `cq:PageContent` 형식입니다.
   >
   >
* 자산( `cq:Asset`). 여기서 `jcr:content/metadata` 노드에는 항상 `cq:Taggable` 믹신이 있습니다.

>



### 노드 유형 표기법(CND) {#node-type-notation-cnd}

CND 파일로 저장소에 노드 유형 정의가 있습니다. CND 표기법은 JCR 설명서 [여기](https://jackrabbit.apache.org/node-type-notation.html)의 일부로 정의됩니다.

AEM에 포함된 노드 유형에 대한 기본 정의는 다음과 같습니다.

```xml
[cq:Tag] > mix:title, nt:base
    orderable
    - * (undefined) multiple
    - * (undefined)
    + * (nt:base) = cq:Tag version

[cq:Taggable]
    mixin
    - cq:tags (string) multiple

[cq:OwnerTaggable] > cq:Taggable
    mixin
```

## 태그 있는 컨텐츠:cq:tags 속성 {#tagged-content-cq-tags-property}

`cq:tags` 속성은 작성자 또는 사이트 방문자가 컨텐츠에 적용할 때 하나 이상의 TagID를 저장하는 데 사용되는 문자열 배열입니다. 속성은 `[cq:Taggable](#taggable-content-cq-taggable-mixin)` 혼합으로 정의된 노드에 추가될 때만 의미가 있습니다.

>[!NOTE]
>
>AEM 태그 지정 기능을 활용하려면 사용자 지정 개발 응용 프로그램이 `cq:tags` 이외의 태그 속성을 정의해서는 안 됩니다.

## 태그 이동 및 병합 {#moving-and-merging-tags}

다음은 [태깅 콘솔](/help/sites-administering/tags.md)을 사용하여 태그를 이동 또는 병합할 때 저장소의 효과에 대한 설명입니다.

* 태그 A가 `/content/cq:tags` 아래의 태그 B로 이동 또는 병합될 때:

   * 태그 A는 삭제되지 않고 `cq:movedTo` 속성을 가져옵니다.
   * 태그 B가 만들어지고(이동 시) `cq:backlinks` 속성을 가져옵니다.

* `cq:movedTo` 태그 B를 가리킵니다. 이 속성은 태그 A가 태그 B로 이동 또는 병합되었음을 의미합니다. 태그 B를 이동하면 이 속성이 그에 따라 업데이트됩니다. 따라서 태그 A는 숨겨지고 태그 A를 가리키는 컨텐츠 노드의 태그 ID만 확인하기 위해 보관됩니다. 태그 가비지 수집기는 태그 A와 같은 태그를 더 이상 컨텐츠 노드가 가리키지 않게 합니다.
`cq:movedTo` 속성에 대한 특수 값은 `nirvana`입니다.태그가 삭제될 때 적용되지만 보관해야 하는 `cq:movedTo`의 하위 태그가 있기 때문에 저장소에서 제거할 수 없습니다.

   >[!NOTE]
   >
   >`cq:movedTo` 속성은 다음 조건 중 하나가 충족되는 경우에만 이동되거나 병합된 태그에만 추가됩니다.
   > 1. 태그는 컨텐츠에 사용됩니다(즉, 참조가 있음) OR
   > 1. 태그에 이미 이동한 하위 항목이 있습니다.


* `cq:backlinks` 참조를 다른 방향으로 유지합니다. 즉, 태그 B로 이동했거나 태그 B와 병합한 모든 태그의 목록을 유지합니다. 태그 B가 이동/병합/삭제되거나 태그 B가 활성화된 경우  `cq:movedTo`속성을 최신 상태로 유지하는 데 주로 필요합니다. 이 경우 모든 배경 링크 태그도 활성화해야 합니다.

   >[!NOTE]
   >
   >`cq:backlinks` 속성은 다음 조건 중 하나가 충족되는 경우에만 이동되거나 병합된 태그에만 추가됩니다.
   >
   > 1. 태그는 컨텐츠에 사용됩니다(즉, 참조가 있음) OR    >
   > 1. 태그에 이미 이동한 하위 항목이 있습니다.


* 콘텐트 노드의 `cq:tags` 속성을 읽으면 다음 해결 방법이 포함됩니다.

   1. `/content/cq:tags` 아래에 일치하는 태그가 없으면 반환되지 않습니다.
   1. 태그에 `cq:movedTo` 속성 집합이 있으면 참조된 태그 ID가 따릅니다.
이 단계는 뒤에 나오는 태그에 `cq:movedTo` 속성이 있으면 반복됩니다.

   1. 뒤에 오는 태그에 `cq:movedTo` 속성이 없으면 태그가 읽혀집니다.

* 태그를 이동하거나 병합할 때 변경 내용을 게시하려면 `cq:Tag` 노드 및 모든 해당 백링크가 복제되어야 합니다.태그 관리 콘솔에서 태그가 활성화되면 자동으로 수행됩니다.

* 나중에 페이지의 `cq:tags` 속성이 업데이트되어 &quot;이전&quot; 참조가 자동으로 정리됩니다. API를 통해 이동한 태그를 확인하면 대상 태그가 반환되므로 대상 태그 ID가 제공되기 때문에 트리거됩니다.

>[!NOTE]
>
>태그 이동은 태그 마이그레이션과 다릅니다.

## 태그 마이그레이션 {#tags-migration}

Experience Manager 6.4부터 태그는 `/content/cq:tags` 아래에 저장되며 이전에 `/etc/tags` 아래에 저장되었습니다. 하지만 Adobe Experience Manager이 이전 버전에서 업그레이드된 시나리오에서 태그는 여전히 이전 위치 `/etc/tags` 아래에 있습니다. 업그레이드된 시스템 태그는 `/content/cq:tags` 아래에서 마이그레이션해야 합니다.

>[!NOTE]
>
>태그 페이지의 페이지 속성에서 태그 기준 경로(예: `/etc/tags/geometrixx-outdoors/activity/biking`)를 하드 코딩하는 대신 태그 ID(`geometrixx-outdoors:activity/biking`)를 사용하는 것이 좋습니다.
>
>태그를 나열하려면 `com.day.cq.tagging.servlets.TagListServlet`을(를) 사용할 수 있습니다.

>[!NOTE]
>
>태그 관리자 API를 리소스로 사용하는 것이 좋습니다.

### 업그레이드된 AEM 인스턴스가 TagManager API {#upgraded-instance-support-tagmanager-api}를 지원하는 경우

1. 구성 요소가 시작될 때 TagManager API는 업그레이드된 AEM 인스턴스인지 여부를 감지합니다. 업그레이드된 시스템에서 태그는 `/etc/tags` 아래에 저장됩니다.

1. 그런 다음 TagManager API는 이전 버전과의 호환성 모드에서 실행되며, 이는 API가 기본 경로로 `/etc/tags`을 사용함을 의미합니다. 그렇지 않으면 새 위치 `/content/cq:tags`을 사용합니다.

1. 태그 위치를 업데이트합니다.

1. 태그를 새 위치로 마이그레이션한 후 다음 스크립트를 실행합니다.

```java
import org.apache.sling.api.resource.*
import javax.jcr.*

ResourceResolverFactory resourceResolverFactory = osgi.getService(ResourceResolverFactory.class);
ResourceResolver resolver = resourceResolverFactory.getAdministrativeResourceResolver(null);
Session session = resolver.adaptTo(Session.class);

def queryManager = session.workspace.queryManager;
def statement = "/jcr:root/content/cq:tags//element(*, cq:Tag)[jcr:contains(@cq:movedTo,\'/etc/tags\') or jcr:contains(@cq:backlinks,\'/etc/tags\')]";
def query = queryManager.createQuery(statement, "xpath");

println "query = ${query.statement}\n";

def tags = query.execute().getNodes();


tags.each { node ->
  def tagPath = node.path;
  println "tag = ${tagPath}";

  if(node.hasProperty("cq:movedTo") && node.getProperty("cq:movedTo").getValue().toString().startsWith("/etc/tags"))
    {
     def movedTo = node.getProperty("cq:movedTo").getValue().toString();

     println "cq:movedTo = ${movedTo} \n";

     movedTo = movedTo.replace("/etc/tags","/content/cq:tags");
     node.setProperty("cq:movedTo",movedTo);
     } else if(node.hasProperty("cq:backlinks")){

     String[] backLinks = node.getProperty("cq:backlinks").getValues();
     int count = 0;

     backLinks.each { value ->
             if(value.startsWith("/etc/tags")){
                     println "cq:backlinks = ${value}\n";
                     backLinks[count] = value.replace("/etc/tags","/content/cq:tags");
    }
             count++;
     }

    node.setProperty("cq:backlinks",backLinks);
  }
}
session.save();

println "---------------------------------Success-------------------------------------"
```

스크립트는 `cq:movedTo/cq:backLinks` 속성 값에 `/etc/tags`이 있는 모든 태그를 가져옵니다. 그런 다음 가져온 결과 세트를 반복하여 `cq:movedTo` 및 `cq:backlinks` 속성 값을 `/content/cq:tags` 경로(값에서 `/etc/tags`이 검색된 경우)로 확인합니다.

### 업그레이드된 AEM 인스턴스가 클래식 UI {#upgraded-instance-runs-classic-ui}에서 실행되는 경우

>[!NOTE]
>
>클래식 UI는 다운타임을 제로 준수하지 않으며 새 태그 기본 경로를 지원하지 않습니다. `/etc/tags`이 아닌 클래식 UI를 사용하려면 `cq-tagging` 구성 요소를 다시 시작해야 합니다.

TagManager API에서 지원하고 클래식 UI에서 실행되는 업그레이드된 AEM 인스턴스의 경우:

1. 이전 태그 기반 경로 `/etc/tags`에 대한 참조가 tagId 또는 새 태그 위치 `/content/cq:tags`를 사용하여 대체되면 태그를 CRX의 새 위치 `/content/cq:tags`로 마이그레이션하고 구성 요소를 다시 시작할 수 있습니다.

1. 태그를 새 위치로 마이그레이션한 후 위에 언급된 스크립트를 실행합니다.
