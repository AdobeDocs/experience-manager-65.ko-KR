---
title: AEM 태그 지정 프레임워크
description: 컨텐츠에 태그를 지정하고 AEM 태깅 인프라 사용
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
feature: Tagging
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 0%

---


# AEM 태그 지정 프레임워크 {#aem-tagging-framework}

태깅을 사용하면 컨텐츠를 분류하고 구성할 수 있습니다. 태그는 네임스페이스와 분류법으로 분류할 수 있습니다. 태그 사용에 대한 자세한 내용은 다음을 참조하십시오.

* 문서 보기 [태그 사용](/help/sites-authoring/tags.md) 콘텐츠 작성자로 콘텐츠에 태그를 지정하는 방법에 대한 자세한 정보.
* 문서 보기 [태그 관리](/help/sites-administering/tags.md) 태그 작성 및 관리 방법과 컨텐츠 태그가 적용되는 항목에 대한 관리자 관점

이 문서에서는 AEM에서 태그 지정을 지원하는 기본 프레임워크와 개발자로 사용하는 방법에 대해 중점적으로 다룹니다.

## 소개 {#introduction}

콘텐츠에 태그를 지정하고 AEM 태그 지정 인프라를 사용하려면 다음을 수행하십시오.

* 태그는 유형의 노드로 있어야 합니다. `[cq:Tag](#tags-cq-tag-node-type)` 다음 아래에 [분류 루트 노드.](#taxonomy-root-node)

* 태그가 지정된 컨텐츠 노드 `NodeType` 다음을 포함해야 합니다. [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin.
* 다음 [`TagID`](#tagid) 이(가) 컨텐츠 노드의 [`cq:tags`](#tagged-content-cq-tags-property) 속성 및 가 유형의 노드로 확인됨 ` [cq:Tag](#tags-cq-tag-node-type)`.

## 태그 : cq:Tag 노드 유형  {#tags-cq-tag-node-type}

태그의 선언은 유형의 노드에서 저장소에 캡처됩니다 `cq:Tag`.

태그는 간단한 단어일 수 있습니다(예: `sky`) 또는 계층 분류를 나타냅니다(예: `fruit/apple`: 제네릭을 모두 의미합니다 `fruit` 및 보다 구체적임 `apple`).

태그는 고유한 TagID로 식별됩니다.

태그에는 제목, 현지화된 제목 및 설명과 같은 선택적 메타 정보가 있습니다. 존재하는 경우 제목은 TagID 대신 사용자 인터페이스에 표시되어야 합니다.

태깅 프레임워크는 작성자와 사이트 방문자가 사전 정의된 특정 태그만 사용하도록 제한하는 기능도 제공합니다.

### 태그 특성 {#tag-characteristics}

* 노드 유형: `cq:Tag`n
* 노드 이름은 의 구성 요소입니다 [태그 ID](#tagid).
* 다음 [태그 ID](#tagid) 항상 포함 [네임스페이스입니다.](#tag-namespace)
* 다음 `jcr:title` 속성(UI에 표시할 제목)은 선택 사항입니다.
* 다음 `jcr:description` 속성은 선택 사항입니다.
* 하위 노드를 포함하는 경우 태그를 라고 합니다. [컨테이너 태그.](#container-tags)
* 태그는 라는 기본 경로 아래의 저장소에 저장됩니다. [분류 루트 노드.](#taxonomy-root-node)

태그는 단순히 JCR 노드이므로 노드 이름은 [JCR 명명 규칙.](naming-conventions.md)

### 태그 ID {#tagid}

TagID는 저장소의 태그 노드로 확인되는 경로를 식별합니다.

일반적으로 TagID는 네임스페이스로 시작하는 줄임 표기 TagID이거나 [분류 루트 노드.](#taxonomy-root-node)

컨텐츠에 태그가 지정되어 있지만 아직 존재하지 않는 경우 `[cq:tags](#tagged-content-cq-tags-property)` 속성이 콘텐츠 노드에 추가되고 TagID가 속성의 `String` 배열 값.

TagID는 [네임스페이스](#tag-namespace) 뒤에 로컬 TagID가 옵니다. [컨테이너 태그](#container-tags) 에는 분류법의 계층 구조 순서를 나타내는 하위 태그가 있습니다. 하위 태그를 사용하여 모든 로컬 TagID와 동일한 태그를 참조할 수 있습니다. 예를 들어 콘텐츠에 태그 지정 `fruit` 다음과 같은 하위 태그가 있는 컨테이너 태그인 경우에도 허용됩니다. `fruit/apple` 및 `fruit/banana`.

### 분류 루트 노드 {#taxonomy-root-node}

분류 루트 노드는 저장소의 모든 태그에 대한 기본 경로입니다. 분류법 루트 노드는 유형의 노드가 아니어야 합니다. `cq:Tag`.

AEM에서 기본 경로는 `/content/cq:tags` 및 루트 노드는 유형이 있습니다. `cq:Folder`.

### 태그 네임스페이스 {#tag-namespace}

네임스페이스를 사용하면 항목을 그룹화할 수 있습니다. 가장 일반적인 사용 사례는 사이트당(예: 공개, 내부 및 포털) 또는 더 큰 애플리케이션(예: WCM, Assets, 커뮤니티)당 네임스페이스입니다. 그러나 네임스페이스는 다양한 다른 요구 사항에 사용할 수 있습니다. 네임스페이스는 사용자 인터페이스에서 현재 콘텐츠에 적용 가능한 태그의 하위 집합(즉, 특정 네임스페이스의 태그)만 표시하기 위해 사용됩니다.

태그의 네임스페이스는 분류 하위 트리의 첫 번째 수준이며, 이 트리는 바로 아래에 있는 노드입니다. [분류 루트 노드](#taxonomy-root-node). 네임스페이스는 유형의 노드입니다. `cq:Tag` 부모가 다음이 아님 `cq:Tag` 노드 유형.

모든 태그에는 네임스페이스가 있습니다. 네임스페이스를 지정하지 않으면 태그는 기본 네임스페이스인 TagID에 할당됩니다 `default` 제목 포함 `Standard Tags`, 즉 `/content/cq:tags/default`.

### 컨테이너 태그 {#container-tags}

컨테이너 태그는 유형의 노드입니다. `cq:Tag` 임의 개수의 하위 노드를 포함하여 사용자 지정 메타데이터로 태그 모델을 향상시킬 수 있습니다.

또한 분류법의 컨테이너 태그(또는 슈퍼 태그)는 모든 하위 태그의 하위 태그 역할을 합니다. (예: 태그된 콘텐츠) `fruit/apple` 태그된 것으로 간주됩니다. `fruit` 또한. 즉, 태그 지정된 콘텐츠 검색 `fruit` 태그된 콘텐츠도 찾을 수 있음 `fruit/apple`.

### TagID 확인 {#resolving-tagids}

TagID에 콜론(`:`), 콜론은 슬래시( )로 더 구분되는 태그 또는 하위 분류법에서 네임스페이스를 분리합니다.`/`). TagID에 콜론이 없으면 기본 네임스페이스가 암시됩니다.

태그의 표준 및 유일한 위치는 아래와 같습니다 `/content/cq:tags`.

를 가리키지 않는 기존 패스 또는 패스를 참조하는 태그 `cq:Tag` 노드가 유효하지 않은 것으로 간주되어 무시됩니다.

다음 표는 일부 샘플 TagID, 해당 요소 및 TagID가 저장소의 절대 경로로 확인되는 방법을 보여 줍니다.

| 태그 ID | 네임스페이스 | 로컬 ID | 컨테이너 태그 | 리프 태그 | 저장소 절대 태그 경로 |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`, `apple` | `braeburn` | `/content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | 없음 | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | 없음 | 없음 | 없음, 네임스페이스 | `/content/cq:tags/dam` |
| `/content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `/content/cq:tags/category/car` |

### 태그 제목의 현지화 {#localization-of-tag-title}

태그에 선택적 제목 문자열 가 포함된 경우( `jcr:title`) 속성을 추가하여 표시할 제목을 현지화할 수 있습니다 `jcr:title.<locale>`.

자세한 내용은 다음 문서를 참조하십시오.

* [다른 언어로 된 태그](/help/sites-developing/building.md#tags-in-different-languages): API 사용에 대해 설명합니다.
* [다른 언어로 태그 관리](/help/sites-administering/tags.md#managing-tags-in-different-languages)- 태깅 콘솔 사용에 대해 설명합니다.

### 액세스 제어 {#access-control}

태그는 아래의 저장소에 노드로 존재합니다 [분류 루트 노드](#taxonomy-root-node). 저장소에서 적절한 ACL을 설정하여 작성자 및 사이트 방문자가 주어진 네임스페이스에서 태그를 만들 수 있도록 허용하거나 거부할 수 있습니다.

또한 특정 태그나 네임스페이스에 대한 읽기 권한을 거부하면 특정 콘텐츠에 태그를 적용하는 기능이 제어됩니다.

일반적인 방법은 다음과 같습니다.

* 허용 `tag-administrators` 모든 네임스페이스에 대한 그룹/역할 쓰기 액세스(추가/수정 `/content/cq:tags`). 이 그룹은 AEM과 함께 제공됩니다.
* 사용자/작성자가 읽을 수 있어야 하는 모든 네임스페이스(대부분 모든 네임스페이스)에 대한 읽기 액세스를 허용합니다.
* 사용자/작성자가 태그를 사용자/작성자가 자유롭게 정의할 수 있는 해당 네임스페이스에 대한 쓰기 액세스 권한 부여(아래에 노드 추가) `/content/cq:tags/some_namespace`)

## 태그 지정 가능 콘텐츠 : cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

애플리케이션 개발자가 컨텐츠 유형에 태깅을 첨부할 경우 노드의 등록([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html))에는 다음 항목이 포함되어야 합니다. `cq:Taggable` mixin 또는 `cq:OwnerTaggable` mixin.

다음 `cq:OwnerTaggable` mixin: 상속 위치 `cq:Taggable`는 소유자/작성자에 의해 컨텐츠가 분류될 수 있음을 나타내기 위한 것입니다. AEM에서는 의 속성일 뿐입니다 `cq:PageContent` 노드. 다음 `cq:OwnerTaggable` mixin은 태깅 프레임워크에서 필요하지 않습니다.

>[!NOTE]
>
>집계된 콘텐츠 항목의 최상위 노드(또는 해당 노드)에서만 태그를 활성화하는 것이 좋습니다 `jcr:content` node). 예를 들면 다음과 같습니다.
>
>* 페이지 (`cq:Page`) 여기서 `jcr:content`노드가 유형임 `cq:PageContent` 다음을 포함: `cq:Taggable` mixin
>* 에셋 ( `cq:Asset`) 여기서 `jcr:content/metadata` 노드에는 항상 `cq:Taggable` mixin
>

### 노드 유형 표기법(CND) {#node-type-notation-cnd}

노드 유형 정의는 저장소에 CND 파일로 존재합니다. CND 표기법은 JCR 설명서의 일부로 정의됩니다 [여기](https://jackrabbit.apache.org/jcr/node-type-notation.html).

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

## 태그가 지정된 컨텐츠: cq:tags 속성 {#tagged-content-cq-tags-property}

다음 `cq:tags` 속성이 `String` 작성자 또는 사이트 방문자가 콘텐츠에 적용할 때 하나 이상의 TagID를 저장하는 데 사용되는 배열입니다. 속성은 로 정의된 노드에 추가되는 경우에만 의미를 갖습니다. `[cq:Taggable](#taggable-content-cq-taggable-mixin)` mixin.

>[!NOTE]
>
>AEM 태그 지정 기능을 사용하려면 사용자 지정 개발 애플리케이션에서 이외의 태그 속성을 정의하면 안 됩니다. `cq:tags`.

## 태그 이동 및 병합 {#moving-and-merging-tags}

다음은 를 사용하여 태그를 이동하거나 병합할 때 저장소의 효과에 대한 설명입니다 [태깅 콘솔](/help/sites-administering/tags.md):

* 태그 A를 이동하거나 아래의 태그 B에 병합할 때 `/content/cq:tags`:

   * 태그 A가 삭제되지 않고 `cq:movedTo` 속성.
   * 태그 B가 만들어지고(이동이 있는 경우) `cq:backlinks` 속성.

* `cq:movedTo` 태그 B를 가리킵니다.

   * 이 속성은 태그 A가 태그 B로 이동되었거나 병합되었음을 의미합니다. 태그 B를 이동하면 그에 따라 이 속성이 업데이트됩니다. 따라서 태그 A는 숨겨지며 태그 A를 가리키는 콘텐츠 노드의 태그 ID를 확인하기 위해 저장소에만 보관됩니다. 태그 가비지 수집기는 더 이상 콘텐츠 노드가 이들을 가리키지 않으면 태그 A와 같은 태그를 제거합니다.

   * 에 대한 특수 값 `cq:movedTo` 속성은 입니다. `nirvana`. 태그가 삭제되지만 가 포함된 하위 태그가 있으므로 저장소에서 제거할 수 없을 때 적용됩니다 `cq:movedTo` 그건 보관해야 합니다.

  >[!NOTE]
  >
  >다음 `cq:movedTo` 다음 조건 중 하나가 충족되는 경우에만 속성이 이동되거나 병합된 태그에 추가됩니다.
  >
  >1. 태그는 콘텐츠에 사용됨(참조가 있음을 의미함) 또는
  >1. 태그에 이미 이동된 하위 항목이 있습니다.

* `cq:backlinks` 는 참조를 다른 방향으로 유지합니다. 즉, 태그 B로 이동되거나 태그 B와 병합된 모든 태그의 목록을 유지합니다. 이는 대부분 다음을 유지하는 데 필요합니다. `cq:movedTo` 태그 B가 이동/병합/삭제되거나 태그 B가 활성화된 최신 속성입니다. 이 경우 모든 해당 백링크 태그도 활성화되어야 합니다.

  >[!NOTE]
  >
  >다음 `cq:backlinks` 다음 조건 중 하나가 충족되는 경우에만 속성이 이동되거나 병합된 태그에 추가됩니다.
  >
  >1. 태그는 콘텐츠에 사용됨(참조가 있음을 의미함) 또는
  >1. 태그에 이미 이동된 하위 항목이 있습니다.

* 읽기 `cq:tags` 컨텐츠 노드의 속성에는 다음 확인이 포함됩니다.

   1. 아래에 일치하는 항목이 없는 경우 `/content/cq:tags`, 태그가 반환되지 않습니다.

   1. 태그에 `cq:movedTo` 속성이 설정되면 참조된 태그 ID가 연결됩니다.

      * 이 단계는 팔로우하는 태그에 가 있는 한 반복됩니다 `cq:movedTo` 속성.

   1. 뒤에 오는 태그에 가 없는 경우 `cq:movedTo` 속성을 지정하면 태그를 읽습니다.

* 태그를 이동하거나 병합할 때 변경 사항을 게시하려면 `cq:Tag` 노드 및 모든 해당 백링크를 복제해야 합니다. 이 작업은 태그 관리 콘솔에서 태그가 활성화되면 자동으로 수행됩니다.

* 페이지의 향후 업데이트 `cq:tags` 속성은 자동으로 이전 참조를 정리합니다. API를 통해 이동된 태그를 확인하면 대상 태그가 반환되어 대상 태그 ID가 제공되므로 이 작업이 트리거됩니다.

>[!NOTE]
>
>태그의 이동은 태그의 마이그레이션과 다릅니다.

## 태그 마이그레이션 {#tags-migration}

Adobe Experience Manager 6.4부터 태그는 `/content/cq:tags` 반면 이전 버전에서는 `/etc/tags`.

6.4 이전 버전에서 AEM 시스템을 업그레이드할 때마다 태그만 로 마이그레이션해야 합니다. `/content/cq:tags`. 다음을 참조하십시오 [AEM 6.5의 일반적인 저장소 재구성](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags) 추가 정보.
