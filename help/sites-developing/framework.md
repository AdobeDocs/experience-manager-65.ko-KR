---
title: AEM Tagging Framework
seo-title: AEM Tagging Framework
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
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# AEM Tagging Framework{#aem-tagging-framework}

컨텐츠에 태그를 지정하고 AEM Tagging 인프라를 활용하려면

* 태그는 ` [cq:Tag](#tags-cq-tag-node-type)` 분류 루트 노드 [아래에 유형 노드로 존재해야 합니다.](#taxonomy-root-node)

* 태그가 지정된 컨텐츠 노드의 NodeType에는 [ `cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin이 포함되어야 합니다.
* TagID [는](#tagid) 컨텐츠 노드의 [ 속성에 추가되고 유형 `cq:tags`](#tagged-content-cq-tags-property) 노드로 확인됩니다 ` [cq:Tag](#tags-cq-tag-node-type)`

## 태그:cq:태그 노드 유형 {#tags-cq-tag-node-type}

태그의 선언은 저장소에서 유형 노드의 `cq:Tag.`

태그는 단순한 단어(예: 하늘)이거나 계층 분류(예: 과일/apple)를 나타낼 수 있습니다. 즉, 일반 과일과 보다 구체적인 사과를 모두 의미합니다.

태그는 고유한 TagID로 식별됩니다.

태그에는 제목, 지역화된 제목 및 설명과 같은 메타 정보가 선택 사항입니다. 제목은 TagID 대신 사용자 인터페이스에 표시되어야 합니다(있을 경우).

태깅 프레임워크에서는 작성자 및 사이트 방문자가 사전 정의된 특정 태그만 사용하도록 제한할 수 있습니다.

### 태그 특성 {#tag-characteristics}

* node type is `cq:Tag`
* node name is a component of ` [TagID](#tagid)`
* 항상 ` [TagID](#tagid)` 네임스페이스를 [포함합니다.](#tag-namespace)

* 선택 `jcr:title` 속성(UI에 표시할 제목)

* 선택적 `jcr:description` 속성

* 하위 노드를 포함할 때는 [컨테이너 태그라고 합니다.](#container-tags)
* 는 [분류 루트 노드라는 기본 경로 아래의 저장소에 저장됩니다.](#taxonomy-root-node)

### 태그 ID {#tagid}

TagID 파섹

일반적으로 TagID는 네임스페이스로 시작하는 축약형 TagID이거나 [분류 루트 노드에서](#taxonomy-root-node)시작하는 절대 TagID일 수 있습니다.

컨텐츠에 태그를 지정하면 해당 컨텐츠가 아직 없으면 ` [cq:tags](#tagged-content-cq-tags-property)` 속성이 컨텐츠 노드에 추가되고 TagID가 속성의 문자열 배열 값에 추가됩니다.

TagID는 [네임스페이스와](#tag-namespace) 로컬 TagID로 구성됩니다. [컨테이너 태그에는](#container-tags) 분류법의 계층 순서를 나타내는 하위 태그가 있습니다. 하위 태그를 사용하여 로컬 TagID와 동일한 태그를 참조할 수 있습니다. 예를 들어 &quot;과일&quot;과 같은 하위 태그가 포함된 컨테이너 태그인 경우에도 &quot;과일&quot;을 사용하여 컨텐츠에 태깅할 수 있습니다.

### 분류 루트 노드 {#taxonomy-root-node}

분류 루트 노드는 저장소의 모든 태그에 대한 기본 경로입니다. 분류 루트 노드는 유형 노드가 *아니어야* 합니다 `  cq   :Tag`.

AEM에서 기본 경로는 `/content/  cq   :tags` 이고 루트 노드는 유형입니다 `  cq   :Folder`.

### 태그 네임스페이스 {#tag-namespace}

네임스페이스로 여러 항목을 그룹화할 수 있습니다. 가장 일반적인 사용 사례는 (웹) 사이트당(예: 공개, 내부 및 포털) 또는 더 큰 애플리케이션(예: WCM, 자산, 커뮤니티)당 네임스페이스를 갖는 것이지만, 네임스페이스는 다양한 기타 요구 사항에 사용할 수 있습니다. 네임스페이스는 사용자 인터페이스에서 현재 컨텐츠에 적용할 수 있는 태그의 하위 집합(즉, 특정 네임스페이스의 태그)만 표시하는 데 사용됩니다.

태그의 네임스페이스는 분류 하위 트리에서 첫 번째 레벨이며, [분류 루트 노드](#taxonomy-root-node)바로 아래에 있는 노드입니다. 네임스페이스는 부모가 `cq:Tag` 노드 유형이 `cq:Tag`아닌 유형의 노드입니다.

모든 태그에는 네임스페이스가 있습니다. 네임스페이스를 지정하지 않으면 태그가 기본 네임스페이스에 지정되며, 이 네임스페이스는 TagID `default` (Title is `Standard Tags),`that `/content/cq:tags/default.`

### 컨테이너 태그 {#container-tags}

컨테이너 태그는 자식 노드의 수와 유형을 `cq:Tag` 포함하는 유형의 노드로서, 이를 통해 사용자 지정 메타데이터로 태그 모델을 개선할 수 있습니다.

또한 택소노미의 컨테이너 태그(또는 super 태그)는 모든 하위 태그의 하위 합계로 사용됩니다.예를 들어, 과일/apple 태그가 지정된 컨텐츠도 과일로 태그되는 것으로 간주됩니다. 예를 들어, 과일 태그가 지정된 컨텐츠를 검색하면 과일/apple 태그가 지정된 컨텐츠도 검색됩니다.

### 태그 ID 확인 {#resolving-tagids}

태그 ID에 콜론 &quot;:&quot;이 포함되어 있으면 콜론은 태그 또는 하위 분류법에서 네임스페이스를 분리한 다음 일반 슬래시 &quot;/&quot;로 구분합니다. 태그 ID에 콜론이 없는 경우 기본 네임스페이스는 암시됩니다.

태그의 표준 및 전용 위치는 /content/cq:tags 아래에 있습니다.

cq:Tag 노드를 가리키지 않는 비기존 경로 또는 경로를 참조하는 태그는 잘못된 것으로 간주되며 무시됩니다.

다음 표는 일부 샘플 TagID, 해당 요소 및 TagID가 저장소의 절대 경로로 어떻게 확인하는지를 보여줍니다.

다음 표는 일부 샘플 TagID, 해당 요소 및 TagID가 저장소의 절대 경로로 어떻게 확인하는지를 보여줍니다.다음 표는 일부 샘플 TagID, 해당 요소 및 TagID가 저장소의 절대 경로로 어떻게 확인하는지를 보여줍니다.

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
   <td>댐:과일/사과/브레이번</td>
   <td>dam</td>
   <td>과일/사과/뇌</td>
   <td>과일, 사과</td>
   <td>브레인</td>
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
   <td>dam</td>
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

### 태그 제목 현지화 {#localization-of-tag-title}

태그에 선택적 제목 문자열( `jcr:title`)이 포함되어 있으면 속성을 추가하여 표시할 제목을 현지화할 수 `jcr:title.<locale>`있습니다.

자세한 내용은

* [다른 언어의](/help/sites-developing/building.md#tags-in-different-languages) 태그 - API의 사용을 설명합니다.
* [다른 언어로](/help/sites-administering/tags.md#managing-tags-in-different-languages) 태그 관리 - 태그 지정 콘솔 사용을 설명합니다.

### 액세스 제어 {#access-control}

태그는 [분류 루트 노드](#taxonomy-root-node)아래의 저장소에 노드로 존재합니다. 작성자와 사이트 방문자가 주어진 네임스페이스에 태그를 만들 수 있도록 허용하거나 거부하려면 저장소에서 적절한 ACL을 설정하여 수행할 수 있습니다.

또한 태그 또는 네임스페이스에 대한 읽기 권한을 거부하면 특정 컨텐츠에 태그를 적용하는 기능을 제어할 수 있습니다.

일반적인 방법은 다음과 같습니다.

* 모든 네임스페이스에 `tag-administrators` 그룹/역할 쓰기 액세스 허용(아래에서 추가/수정 `/content/cq:tags`). 이 그룹에는 AEM 특별 버전이 포함되어 있습니다.

* 사용자/작성자가 읽을 수 있어야 하는 모든 네임스페이스에 대한 읽기 액세스 권한을 부여할 수 있습니다(대부분 모두).
* 사용자/작성자가 태그를 자유롭게 정의해야 하는 네임스페이스에 대한 사용자/작성자 쓰기 액세스 허용(아래 add_node `/content/cq:tags/some_namespace`)

## 태그 가능한 컨텐츠:cq:태그 지정 가능한 믹싱 {#taggable-content-cq-taggable-mixin}

애플리케이션 개발자가 컨텐츠 유형에 태깅을 첨부하려면 노드의 등록([CND](https://jackrabbit.apache.org/node-type-notation.html))에 `cq:Taggable` 믹스인 또는 `cq:OwnerTaggable` 혼합이 포함되어야 합니다.

에서 상속되는 `cq:OwnerTaggable` 혼합은 컨텐츠가 소유자/작성자에 의해 분류될 수 있음을 나타내는 `cq:Taggable`것입니다. AEM에서는 `cq:PageContent` 노드의 속성만 해당됩니다. 태깅 프레임워크에서는 `cq:OwnerTaggable` 혼합이 필요하지 않습니다.

>[!NOTE]
>
>집계된 컨텐츠 항목의 최상위 노드(또는 jcr:content 노드)에서만 태그를 활성화하는 것이 좋습니다. 예:
>
>* pages ( `cq:Page`) where the `jcr:content`node is of `cq:PageContent` the type that including the `cq:Taggable` mixin.
   >
   >
* 자산( `cq:Asset`). `jcr:content/metadata` 노드에 항상 `cq:Taggable` 혼합이 있는 경우
>



### 노드 유형 표기법(CND) {#node-type-notation-cnd}

CND 파일로 저장소에 노드 유형 정의가 있습니다. CND 표기법은 [여기에서](https://jackrabbit.apache.org/node-type-notation.html)JCR 설명서의 일부로 정의됩니다.

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

이 `cq:tags` 속성은 작성자 또는 사이트 방문자가 컨텐츠에 적용할 때 하나 이상의 TagID를 저장하는 데 사용되는 문자열 배열입니다. 이 속성에는 ` [cq:Taggable](#taggable-content-cq-taggable-mixin)` mixin으로 정의된 노드에 추가할 때만 의미가 있습니다.

>[!NOTE]
>
>AEM 태그 지정 기능을 활용하려면 사용자 지정 개발 응용 프로그램이 태그 속성을 `cq:tags`정의하지 않아야 합니다.

## 태그 이동 및 병합 {#moving-and-merging-tags}

다음은 태깅 콘솔을 [사용하여 태그를 이동하거나 병합할 때 저장소의 효과에 대한](/help/sites-administering/tags.md)설명입니다.

* 태그 A가 다음 아래에서 태그 B로 이동 또는 병합되는 `/content/cq:tags`경우

   * 태그 A는 삭제되지 않고 `cq:movedTo` 속성을 가져옵니다.
   * 태그 B가 만들어지고(이동의 경우) `cq:backlinks` 속성을 가져옵니다.

* `cq:movedTo` 태그 B를 가리킵니다.이 속성은 태그 A가 태그 B로 이동 또는 병합되었음을 의미합니다.태그 B를 이동하면 그에 따라 이 속성이 업데이트됩니다. 태그 A는 숨겨진 상태로 보관되어 태그 A를 가리키는 컨텐츠 노드의 태그 ID만 확인합니다.태그 가비지 수집기는 태그 A와 같은 태그를 더 이상 가리키지 않고 제거합니다.
속성에 대한 특수 값은 `cq:movedTo` 다음과 `nirvana`같습니다.태그가 삭제될 때 적용되지만 보관해야 하는 하위 태그가 있기 때문에 저장소에서 제거할 수 `cq:movedTo` 없습니다.

   >[!NOTE]
   >
   >이 `cq:movedTo` 속성은 다음 조건 중 하나가 충족되는 경우에만 이동되거나 병합된 태그에만 추가됩니다.
   > 1. 태그가 컨텐츠에 사용됨(즉, 참조가 있음) OR
   > 1. 태그에 이미 이동한 하위 항목이 있습니다.


* `cq:backlinks` 참조를 다른 방향으로 유지합니다. 즉, 태그 B로 이동하거나 병합한 모든 태그 목록이 유지됩니다.태그 B가 이동/병합/삭제될 때나 태그 B가 활성화될 때 `cq:movedTo`속성을 최신 상태로 유지하는 데 필요합니다. 이 경우 모든 배경 링크 태그도 활성화해야 합니다.

   >[!NOTE]
   >
   >이 `cq:backlinks` 속성은 다음 조건 중 하나가 충족되는 경우에만 이동되거나 병합된 태그에만 추가됩니다.
   > 1. 태그가 컨텐츠에 사용됨(즉, 참조가 있음) OR
   > 1. 태그에 이미 이동한 하위 항목이 있습니다.


* 컨텐츠 노드의 `cq:tags` 속성을 읽으면 다음 해결 방법이 포함됩니다.

   1. 일치하는 항목이 없으면 `/content/cq:tags`태그가 반환되지 않습니다.
   1. 태그에 `cq:movedTo` 속성 집합이 있으면 참조된 태그 ID가 따릅니다.
이 단계는 뒤에 오는 태그에 `cq:movedTo` 속성이 있으면 반복됩니다.

   1. 다음 태그에 `cq:movedTo` 속성이 없으면 태그가 읽혀집니다.

* 태그를 이동하거나 병합할 때 변경 내용을 게시하려면 `cq:Tag` 노드와 모든 백링크를 복제해야 합니다.태그 관리 콘솔에서 태그가 활성화되면 자동으로 수행됩니다.

* 나중에 페이지 `cq:tags` 속성이 업데이트되면 &quot;이전&quot; 참조가 자동으로 정리됩니다. API를 통해 이동한 태그를 확인하면 대상 태그가 반환되어 대상 태그 ID가 제공되기 때문에 트리거됩니다.
