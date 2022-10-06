---
title: AEM 태그 지정 프레임워크
seo-title: AEM Tagging Framework
description: 컨텐츠에 태그를 지정하고 AEM 태깅 인프라를 활용
seo-description: Tag content and leverage the AEM Tagging infrastructure
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
feature: Tagging
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
source-git-commit: 4db9279f2d15f2e08939ba453ae8ddbbc3c3d69f
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 0%

---

# AEM 태그 지정 프레임워크 {#aem-tagging-framework}

컨텐츠에 태그를 지정하고 AEM 태깅 인프라를 활용하려면 다음과 같이 하십시오.

* 태그는 유형의 노드로 존재해야 합니다 ` [cq:Tag](#tags-cq-tag-node-type)` 아래에 [분류 루트 노드](#taxonomy-root-node)

* 태그가 지정된 콘텐츠 노드의 NodeType에는 [ `cq:Taggable`](#taggable-content-cq-taggable-mixin) 혼합
* 다음 [TagID](#tagid) 컨텐츠 노드의 [ `cq:tags`](#tagged-content-cq-tags-property) 속성 및 가 유형의 노드로 확인됨 ` [cq:Tag](#tags-cq-tag-node-type)`

## 태그 : cq:태그 노드 유형  {#tags-cq-tag-node-type}

태그의 선언은 유형 노드의 저장소에 캡처됩니다 `cq:Tag.`

태그는 단순한 단어(예: 하늘)이거나 계층적 분류법(예: 과일/apple, 일반 과일 및 보다 구체적인 apple)을 나타낼 수 있습니다.

태그는 고유한 TagID로 식별됩니다.

태그에는 제목, 현지화된 제목 및 설명과 같은 선택적 메타 정보가 있습니다. 제목이 있으면 TagID 대신 사용자 인터페이스에 표시되어야 합니다.

또한 태깅 프레임워크는 작성자와 사이트 방문자가 사전 정의된 특정 태그만 사용하도록 제한하는 기능을 제공합니다.

### 태그 특성 {#tag-characteristics}

* 노드 유형은 `cq:Tag`
* 노드 이름은 의 구성 요소입니다 ` [TagID](#tagid)`
* a ` [TagID](#tagid)` 항상 포함 [namespace](#tag-namespace)

* 옵션 `jcr:title` 속성(UI에 표시할 제목)

* 옵션 `jcr:description` 속성

* 하위 노드를 포함할 때에는 [컨테이너 태그](#container-tags)
* 는 [분류 루트 노드](#taxonomy-root-node)

### 태그 ID {#tagid}

TagID는 저장소의 태그 노드로 확인되는 경로를 식별합니다.

일반적으로 TagID는 네임스페이스로 시작하는 축약형 TagID이거나 [분류 루트 노드](#taxonomy-root-node).

컨텐츠에 태그를 지정할 때 태그가 아직 없는 경우 ` [cq:tags](#tagged-content-cq-tags-property)` 속성이 content 노드에 추가되고 TagID가 속성의 String 배열 값에 추가됩니다.

TagID는 [namespace](#tag-namespace) 다음에 로컬 TagID가 옵니다. [컨테이너 태그](#container-tags) 분류에서 계층적 순서를 나타내는 하위 태그가 있습니다. 하위 태그를 사용하여 로컬 TagID와 동일한 태그를 참조할 수 있습니다. 예를 들어 &quot;과일&quot;, &quot;과일/apple&quot; 및 &quot;과일/바나나&quot;와 같은 하위 태그가 있는 컨테이너 태그인 경우에도 &quot;과일&quot;을 사용하여 콘텐츠에 태그를 지정할 수 있습니다.

### 분류 루트 노드 {#taxonomy-root-node}

분류 루트 노드는 저장소의 모든 태그에 대한 기본 경로입니다. 분류 루트 노드는 *not* 유형의 노드임 `  cq   :Tag`.

AEM에서 기본 경로는 입니다. `/content/  cq   :tags` 그리고 루트 노드는 유형이 됩니다. `  cq   :Folder`.

### 태그 네임스페이스 {#tag-namespace}

네임스페이스를 통해 항목을 그룹화할 수 있습니다. 가장 일반적인 사용 사례는 (웹)사이트당(예: 공개, 내부 및 포털) 또는 더 큰 애플리케이션(예: WCM, Assets, Communities)당 네임스페이스를 갖는 것이지만 다른 다양한 요구 사항에 네임스페이스를 사용할 수 있습니다. 네임스페이스는 사용자 인터페이스에서 현재 컨텐츠에 적용할 수 있는 태그의 하위 집합(예: 특정 네임스페이스의 태그)만 표시하는 데 사용됩니다.

태그의 네임스페이스는 분류법 하위 트리의 첫 번째 수준이며, 이 하위 트리는 [분류 루트 노드](#taxonomy-root-node). 네임스페이스는 유형의 노드입니다 `cq:Tag` 해당 부모가 아님 `cq:Tag`노드 유형입니다.

모든 태그에는 네임스페이스가 있습니다. 지정된 네임스페이스가 없으면 태그가 TagID인 기본 네임스페이스에 할당됩니다 `default` (제목: `Standard Tags),`그건 `/content/cq:tags/default.`

### 컨테이너 태그 {#container-tags}

컨테이너 태그는 유형의 노드입니다 `cq:Tag` 에는 임의 개수의 하위 노드 및 유형이 포함되어 있으므로 사용자 지정 메타데이터로 태그 모델을 향상시킬 수 있습니다.

또한 분류법의 컨테이너 태그(또는 수퍼 태그)는 모든 하위 태그의 하위 합계로 사용됩니다. 예를 들어, 과일/apple 태그가 지정된 컨텐츠도 과일에 태그가 지정된 것으로 간주됩니다. 예를 들어, 과일로 태그가 지정된 컨텐츠의 검색도 과일/apple 태그가 지정된 내용을 찾을 수 있습니다.

### TagID 해결 {#resolving-tagids}

태그 ID에 콜론 &quot;:&quot;이 포함되어 있으면 콜론은 태그 또는 하위 분류에서 네임스페이스를 분리하며 이 다음 슬래시 &quot;/&quot;로 구분됩니다. 태그 ID에 콜론이 없는 경우 기본 네임스페이스가 암시됩니다.

태그의 표준 및 전용 위치는 /content/cq:tags 아래에 있습니다.

cq:Tag 노드를 가리키지 않는 비기존 경로 또는 경로를 참조하는 태그는 잘못된 것으로 간주되며 무시됩니다.

다음 표는 일부 샘플 TagID, 해당 요소 및 TagID가 저장소의 절대 경로로 확인되는 방법을 보여줍니다.

다음 표는 일부 샘플 TagID, 해당 요소 및 TagID가 저장소의 절대 경로로 확인되는 방법을 보여줍니다.

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
   <td>댐:과일/사과/버번</td>
   <td>dam</td>
   <td>과일/사과/베번</td>
   <td>과일, 사과</td>
   <td>브레인</td>
   <td>/content/cq:tags/dam/furice/apple/breburn</td>
  </tr>
  <tr>
   <td>색상/빨강</td>
   <td>기본값</td>
   <td>색상/빨강</td>
   <td>컬러</td>
   <td>빨간색</td>
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
   <td>dam</td>
   <td>(없음)</td>
   <td>(없음)</td>
   <td>(없음, 네임스페이스)</td>
   <td>/content/cq:tags/dam</td>
  </tr>
  <tr>
   <td>/content/cq:tags/category/car</td>
   <td>카테고리</td>
   <td>자동차</td>
   <td>자동차</td>
   <td>자동차</td>
   <td>/content/cq:tags/category/car</td>
  </tr>
 </tbody>
</table>

### 태그 제목 현지화 {#localization-of-tag-title}

태그에 선택적 제목 문자열( `jcr:title`) 속성을 추가하여 표시할 제목을 현지화할 수 있습니다 `jcr:title.<locale>`.

자세한 내용은

* [다른 언어의 태그](/help/sites-developing/building.md#tags-in-different-languages) - API의 사용을 설명합니다.
* [다른 언어로 태그 관리](/help/sites-administering/tags.md#managing-tags-in-different-languages) - 태깅 콘솔의 사용을 설명합니다.

### 액세스 제어 {#access-control}

태그는 저장소의 [분류 루트 노드](#taxonomy-root-node). 작성자 및 사이트 방문자가 주어진 네임스페이스에서 태그를 만들 수 있도록 허용 또는 거부하는 것은 리포지토리에서 적절한 ACL을 설정하여 수행할 수 있습니다.

또한 태그 또는 네임스페이스에 대한 읽기 권한을 거부하면 특정 콘텐츠에 태그를 적용하는 기능을 제어할 수 있습니다.

일반적인 방법은 다음과 같습니다.

* 허용 `tag-administrators` 모든 네임스페이스에 대한 그룹/역할 쓰기 액세스 권한( `/content/cq:tags`). 이 그룹에는 기본적으로 AEM이 포함되어 있습니다.

* 사용자/작성자가 읽을 수 있어야 하는 모든 네임스페이스에 대한 읽기 액세스 권한을 부여합니다(대부분 모두).
* 사용자/작성자가 사용자/작성자가 태그를 자유롭게 정의할 수 있는 네임스페이스에 대한 쓰기 액세스 권한을 허용(아래에 add_node)합니다. `/content/cq:tags/some_namespace`)

## 타깃팅 가능한 컨텐츠 : cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

애플리케이션 개발자가 컨텐츠 유형에 태깅을 첨부하려면 노드의 등록([CND](https://jackrabbit.apache.org/node-type-notation.html))에는 를 포함해야 합니다. `cq:Taggable` mixin 또는 `cq:OwnerTaggable` 믹신

다음 `cq:OwnerTaggable` 에서 상속하는 mixin `cq:Taggable`은(는) 컨텐츠가 소유자/작성자에 의해 분류될 수 있음을 나타내기 위한 것입니다. AEM에서 이 속성은 `cq:PageContent` 노드 아래에 있어야 합니다. 다음 `cq:OwnerTaggable` 태깅 프레임워크에서는 mixin이 필요하지 않습니다.

>[!NOTE]
>
>집계된 컨텐츠 항목의 최상위 노드(또는 jcr:content 노드)에서만 태그를 활성화하는 것이 좋습니다. 해당 예는 다음과 같습니다.
>
>* 페이지 ( `cq:Page`)에서 `jcr:content`node는 type입니다. `cq:PageContent` 여기에는 `cq:Taggable` 믹신
>
>* 자산 ( `cq:Asset`)에서 `jcr:content/metadata` 노드에는 항상 가 있습니다 `cq:Taggable` 믹신
>


### 노드 유형 표기법(CND) {#node-type-notation-cnd}

노드 유형 정의는 저장소에 CND 파일로 있습니다. CND 표기법은 JCR 설명서의 일부로 정의됩니다 [여기](https://jackrabbit.apache.org/node-type-notation.html).

AEM에 포함된 노드 유형에 대한 필수 정의는 다음과 같습니다.

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

## 태그가 지정된 콘텐츠: cq:tags 속성 {#tagged-content-cq-tags-property}

다음 `cq:tags` 속성은 작성자 또는 사이트 방문자가 컨텐츠에 적용할 때 하나 이상의 TagID를 저장하는 데 사용되는 문자열 배열입니다. 속성은 `[cq:Taggable](#taggable-content-cq-taggable-mixin)` 믹신

>[!NOTE]
>
>AEM 태그 지정 기능을 활용하려면 사용자 정의 개발 애플리케이션에서 `cq:tags`.

## 태그 이동 및 병합 {#moving-and-merging-tags}

다음은 를 사용하여 태그를 이동하거나 병합할 때 리포지토리의 효과에 대한 설명입니다 [태깅 콘솔](/help/sites-administering/tags.md):

* 태그 A를 아래의 태그 B로 이동하거나 병합하는 경우 `/content/cq:tags`:

   * 태그 A는 삭제되지 않고 `cq:movedTo` 속성을 사용합니다.
   * 태그 B가 만들어져서(이동의 경우) `cq:backlinks` 속성을 사용합니다.

* `cq:movedTo` 태그 B를 가리킵니다. 이 속성은 태그 A가 태그 B로 이동되거나 병합되었음을 의미합니다. 태그 B를 이동하면 이 속성이 그에 따라 업데이트됩니다. 따라서 태그 A는 숨겨져 있으며, 태그 A를 가리키는 컨텐츠 노드의 태그 ID를 확인하기 위해 저장소에만 유지됩니다. 태그 가비지 수집기는 태그 A와 같은 태그를 더 이상 컨텐츠 노드가 가리키지 않으면 제거합니다.
에 대한 특수 값 `cq:movedTo` property `nirvana`: 태그가 삭제될 때 적용되지만, `cq:movedTo` 그건 보관해야 합니다

   >[!NOTE]
   >
   >다음 `cq:movedTo` 속성은 다음 조건 중 하나가 충족되는 경우에만 이동되거나 병합된 태그에 추가됩니다.
   > 1. 태그는 컨텐츠에 사용됩니다(참조자가 있음). OR에
   > 1. 태그에 이미 이동된 하위 항목이 있습니다.


* `cq:backlinks` 는 참조를 다른 방향으로 유지합니다. 즉, 태그 B로 이동하거나 병합된 모든 태그의 목록을 유지합니다. 이 작업은 주로 `cq:movedTo`태그 B가 이동/병합/삭제되거나 태그 B가 활성화될 때까지의 속성. 이 경우 모든 백링크 태그도 활성화해야 합니다.

   >[!NOTE]
   >
   >다음 `cq:backlinks` 속성은 다음 조건 중 하나가 충족되는 경우에만 이동되거나 병합된 태그에 추가됩니다.
   >
   > 1. 태그는 컨텐츠에 사용됩니다(참조 있음). 또는 >
   > 1. 태그에 이미 이동된 하위 항목이 있습니다.


* 읽기 `cq:tags` 컨텐츠 노드의 속성에는 다음 해결 방법이 포함됩니다.

   1. 아래에 일치하는 항목이 없으면 `/content/cq:tags`, 태그가 반환되지 않습니다.
   1. 태그에 `cq:movedTo` 속성 세트, 참조된 태그 ID가 따릅니다.
이 단계는 뒤에 오는 태그에 `cq:movedTo` 속성을 사용합니다.

   1. 다음에 나오는 태그에 `cq:movedTo` 속성, 태그를 읽습니다.

* 태그가 이동되거나 병합될 때 변경 내용을 게시하려면 `cq:Tag` 노드 및 모든 백링크가 복제되어야 합니다. 이 작업은 태그가 태그 관리 콘솔에서 활성화되면 자동으로 수행됩니다.

* 페이지의 `cq:tags` 속성은 &quot;이전&quot; 참조를 자동으로 정리합니다. API를 통해 이동한 태그를 확인하면 대상 태그가 반환되어 대상 태그 ID가 제공되므로 트리거됩니다.

>[!NOTE]
>
>태그 이동은 태그 마이그레이션과 다릅니다.

## 태그 마이그레이션 {#tags-migration}

Experience Manager 6.4 이상 태그는 `/content/cq:tags`: 이전에 `/etc/tags`. 그러나 Adobe Experience Manager이 이전 버전에서 업그레이드된 시나리오에서는 태그가 이전 위치 아래에 여전히 있습니다 `/etc/tags`. 업그레이드된 시스템 태그는 `/content/cq:tags`.

>[!NOTE]
>
>태그 페이지의 페이지 속성에서 태그 ID(`geometrixx-outdoors:activity/biking`) 내의 아무 곳에나 삽입할 수 있습니다. `/etc/tags/geometrixx-outdoors/activity/biking`).
>
>태그를 나열하려면, `com.day.cq.tagging.servlets.TagListServlet` 사용할 수 있습니다.

>[!NOTE]
>
>태그 관리자 API를 리소스로 사용하는 것이 좋습니다.

### 업그레이드된 AEM 인스턴스가 TagManager API를 지원하는 경우 {#upgraded-instance-support-tagmanager-api}

1. 구성 요소가 시작될 때 TagManager API는 업그레이드된 AEM 인스턴스인지 여부를 감지합니다. 업그레이드된 시스템에서 태그는 아래에 저장됩니다. `/etc/tags`.

1. 그런 다음 TagManager API는 API가 를 사용함을 의미하는 이전 호환성 모드에서 실행됩니다 `/etc/tags` 를 기본 경로로 사용합니다. 없는 경우 새 위치를 사용합니다 `/content/cq:tags`.

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

스크립트는 `/etc/tags` 값 `cq:movedTo/cq:backLinks` 속성을 사용합니다. 그런 다음 가져온 결과 세트를 반복하여 를 확인합니다. `cq:movedTo` 및 `cq:backlinks` 속성 값 `/content/cq:tags` 경로( `/etc/tags` 가 값에서 감지되었습니다.

### 업그레이드된 AEM 인스턴스가 클래식 UI에서 실행되는 경우 {#upgraded-instance-runs-classic-ui}

>[!NOTE]
>
>클래식 UI는 다운타임 없이 사용할 수 있으며 새 태그 기본 경로를 지원하지 않습니다. 다음보다 클래식 UI를 사용하려면 `/etc/tags` 을(를) 만든 후 다음을 수행해야 합니다. `cq-tagging` 구성 요소를 다시 시작합니다.

TagManager API에서 지원되고 클래식 UI에서 실행되는 업그레이드된 AEM 인스턴스의 경우:

1. 이전 태그 기본 경로에 대한 참조가 있으면 `/etc/tags` 는 tagId 또는 새 태그 위치를 사용하여 바꿉니다 `/content/cq:tags`, 태그를 새 위치로 마이그레이션할 수 있습니다 `/content/cq:tags` crx에서 구성 요소를 다시 시작합니다.

1. 태그를 새 위치로 마이그레이션한 후 위에 언급된 스크립트를 실행합니다.
