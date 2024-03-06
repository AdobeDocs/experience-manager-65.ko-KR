---
title: 데이터 모델링 - David Nuescheler의 모델
description: David Nuescheler의 콘텐츠 모델링 권장 사항
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 6ce6a204-db59-4ed2-8383-00c6afba82b4
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 0%

---

# 데이터 모델링 - David Nuescheler의 모델{#data-modeling-david-nuescheler-s-model}

## 소스 {#source}

다음의 세부 사항은 David Nuescheler가 표현한 아이디어와 주석이다.

David은 2010년 Adobe이 인수한 글로벌 컨텐츠 관리 및 컨텐츠 인프라 소프트웨어의 선두 공급업체인 Day Software AG의 공동 설립자이자 CTO였습니다. David은 현재 Adobe의 엔터프라이즈 기술 부문 동료 겸 부사장으로서, 컨텐츠 관리 기술 표준인 Java™ JCR(Content Repository) API(Application Programming Interface) 인 JSR-170의 개발도 주도하고 있습니다.

추가 업데이트는에서 확인할 수 있습니다. [https://cwiki.apache.org/confluence/display/jackrabbit/DavidsModel](https://cwiki.apache.org/confluence/display/jackrabbit/DavidsModel).

## David 소개 {#introduction-from-david}

다양한 토론에서 콘텐츠 모델링 시 JCR이 제공하는 기능과 성능에 대해 개발자들이 다소 불편하다는 것을 알게 되었습니다. 리포지토리에서 콘텐츠를 모델링하는 방법과 한 콘텐츠 모델이 다른 모델보다 나은 이유에 대한 안내서와 경험은 아직 없습니다.

관계형 환경에서는 소프트웨어 산업이 데이터를 모델링하는 방법에 대한 경험이 있지만 컨텐츠 리포지토리 공간에는 아직 초기 단계입니다.

콘텐츠를 어떻게 모델링해야 하는지에 대한 나의 의견을 표현하는 것으로 이 공백을 메우기 시작하고자 한다. 제 희망은 이것이 언젠가는 개발자의 공동체에 더 의미 있는 무언가로 발전할 수 있기를 바라며, 그것은 단지 &quot;나의 의견&quot;이 아니라 더 일반적으로 적용 가능한 어떤 것입니다. 그러니 빨리 진화하는 제 첫 번째 시도에 대해 생각해 보세요.

>[!NOTE]
>
>면책조항: 이 지침은 개인적이고 때로는 논란의 여지가 있는 견해를 나타냅니다. 이러한 지침에 대해 토론하고 이를 구체화할 수 있기를 기대합니다.

## 일곱 가지 간단한 규칙 {#seven-simple-rules}

### 규칙 #1: 먼저 데이터를 구조화하고 나중에 구조화합니다. 그럴지도. {#rule-data-first-structure-later-maybe}

#### 설명 {#explanation-1}

ERD 의미의 선언된 데이터 구조에 대해서는 걱정하지 않는 것이 좋습니다. 처음에는.

개발 과정에서 nt:unstructured(&amp; friends)를 사랑하는 방법을 배웁니다.

결론적으로, 구조는 비용이 많이 들고 기본 스토리지에 구조를 명시적으로 선언할 필요가 없는 경우가 많습니다.

애플리케이션이 기본적으로 사용하는 구조에 대한 암묵적 계약이 있습니다. 블로그 게시물의 수정 날짜를 lastModified 속성에 저장한다고 가정해 보겠습니다. 내 앱은 동일한 속성에서 수정 날짜를 다시 읽어야 한다는 것을 자동으로 인식하므로 명시적으로 선언할 필요가 없습니다.

필수 또는 유형 및 값 제한과 같은 추가 데이터 제한은 데이터 무결성을 위해 필요한 경우에만 적용해야 합니다.

#### 예 {#example-1}

를 사용하는 위의 예 `lastModified` 날짜 속성(예: &quot;블로그 게시물&quot; 노드)은 특수 노드 유형이 필요하다는 것을 의미하지는 않습니다. I wouldn&#39;t sure use `nt:unstructured` 적어도 처음에는 블로그 게시물 노드의 경우입니다. 내 블로그 응용 프로그램에서, 내가 할 일은 어쨌든 lastModified 날짜를 표시 하는 것입니다 (아마도 &quot;order by&quot;) 나는 그것이 날짜인지 전혀 상관 없습니다. 나는 암묵적으로 내 블로그 쓰기 응용 프로그램을 믿고 거기에 &quot;날짜&quot;를 넣기 때문에, 실제로 의 존재를 선언할 필요가 없습니다 `lastModified` 노드 유형 형식의 날짜.

### 규칙 #2: 콘텐츠 계층 구조를 구동합니다. 이렇게 하지 마십시오. {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### 설명 {#explanation-2}

콘텐츠 계층 구조는 중요한 자산입니다. 그런 일이 일어나도록 내버려 두지 말고, 그것을 설계하라. 사람이 인식할 수 있는 &quot;좋은&quot; 이름이 없는 노드의 경우 재고해야 할 사항입니다. 임의의 숫자는 &quot;좋은 이름&quot;이 아닙니다.

기존의 관계적 모델을 위계적 모델에 신속하게 투입하는 것이 수월할 수 있지만, 그 과정에서 어떤 사고를 넣어야 한다.

내 경험에 따르면, 액세스 제어 및 컨테인먼트가 콘텐츠 계층 구조를 위한 좋은 드라이버라고 생각하는 경우 파일 시스템인 것처럼 생각하십시오. 파일 및 폴더를 사용하여 로컬 디스크에서 모델링할 수도 있습니다.

개인적으로는 처음에는 노드 입력 시스템보다 계층 규칙을 선호하고 나중에 입력을 소개합니다.

>[!CAUTION]
>
>콘텐츠 저장소의 구성 방식은 성능에도 영향을 줄 수 있습니다. 최상의 성능을 위해 컨텐츠 저장소의 개별 노드에 연결된 하위 노드 수는 1,000개를 초과할 수 없습니다.
>
>다음을 참조하십시오 [CRX가 처리할 수 있는 데이터의 양은?](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html)

#### 예 {#example-2}

간단한 블로그 시스템을 다음과 같이 모델링하겠습니다. 처음에는 현재 사용하는 각 노드 유형에 대해서도 신경 쓰지 않습니다.

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

더 이상의 설명 없이 사례에 근거하여 내용의 구조를 이해하는 것이 명백해지는 것 중 하나라고 생각한다.

처음에 예상하지 못했던 것은 &quot;게시물&quot;에 &quot;댓글&quot;을 저장하지 않는 이유입니다. 이 게시물은 합리적으로 계층적인 방식으로 적용하고자 하는 액세스 제어에 기인합니다.

위의 콘텐츠 모델을 사용하면 &quot;익명&quot; 사용자가 주석을 &quot;만들기&quot;할 수 있지만 나머지 작업 영역에 대해서는 익명 사용자를 읽기 전용으로 유지할 수 있습니다.

### 규칙 #3: 작업 공간은 clone(), merge() 및 update()에 사용됩니다. {#rule-workspaces-are-for-clone-merge-and-update}

#### 설명 {#explanation-3}

를 사용하지 않는 경우 `clone()`, `merge()` 또는 `update()` 단일 작업 영역을 사용하는 것이 아마도 애플리케이션의 방법입니다.

&quot;해당 노드&quot;는 JCR 사양에 정의된 개념입니다. 기본적으로 동일한 콘텐츠를 나타내는 노드로 전달되며, 이러한 콘텐츠는 서로 다른 작업 공간에 있습니다.

JCR은 많은 개발자들이 작업 영역을 어떻게 해야 할지 명확하지 않은 추상적인 작업 공간 개념을 도입했습니다. 작업 공간 사용을 테스트하기 위해 다음 사항에 적용하는 것을 제안합니다.

여러 작업 영역에서 &quot;해당&quot; 노드(기본적으로 동일한 UUID를 가진 노드)가 상당히 겹치는 경우 작업 영역을 유용하게 사용할 수 있을 것입니다.

동일한 UUID를 사용하는 노드가 겹치지 않으면 작업 영역을 악용할 수 있습니다.

액세스 제어에 작업 영역을 사용하지 마십시오. 특정 사용자 그룹에 대한 컨텐츠를 표시하는 것은 여러 작업 공간을 구분하는 좋은 인수가 아닙니다. JCR은 이를 위해 콘텐츠 저장소에 있는 &quot;액세스 제어&quot; 기능을 제공합니다.

작업공간은 참조 및 쿼리의 경계입니다.

#### 예 {#example-3}

다음과 같은 작업에 작업 공간 사용:

* 프로젝트의 v1.2와 프로젝트의 v1.3 비교
* 콘텐츠의 &quot;개발&quot;, &quot;QA&quot; 및 &quot;게시됨&quot; 상태

다음과 같은 작업을 위해 작업 공간을 사용하지 마십시오.

* 사용자 홈 디렉터리
* public, private, local, ...과 같은 다양한 타겟 대상을 위한 고유한 콘텐츠
* 다른 사용자용 메일 받은 편지함

### 규칙 #4: 동일한 이름 형제 항목에 주의하십시오. {#rule-beware-of-same-name-siblings}

#### 설명 {#explanation-4}

SNS(Same Name Sidelines)가 사양에 도입되어 XML을 위해 설계되고 표현된 데이터 구조와의 호환성을 허용하므로 JCR에 유용합니다. 그러나 SNS는 저장소에 대한 오버헤드와 복잡성을 수반합니다.

경로 세그먼트 중 하나에 SNS가 포함된 콘텐츠 저장소의 경로는 훨씬 덜 안정적입니다. SNS를 제거하거나 순서를 변경하는 경우 다른 모든 SNS와 자녀의 경로에 영향을 미칩니다.

XML을 가져오거나 기존 XML과 상호 작용하기 위해 SNS가 필요하고 유용할 수 있지만 &quot;녹색 필드&quot; 데이터 모델에 SNS를 사용한 적이 없습니다(의도한 적이 없음).

#### 예 {#example-4}

사용

```xml
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping
```

대신

```xml
/content/blog[1]/post[1]
/content/blog[1]/post[2]
```

### 규칙 #5: 참조는 유해한 것으로 간주됩니다. {#rule-references-considered-harmful}

#### 설명 {#explanation-5}

참조는 참조 무결성을 의미합니다. 참조는 참조 무결성을 관리하는 저장소에 추가 비용을 추가할 뿐만 아니라 콘텐츠 유연성의 관점에서 비용이 많이 든다는 것을 이해하는 것이 중요합니다.

개인적으로, 나는 매달린 참조를 처리할 수 없을 때에만 참조를 사용하고, 그렇지 않으면 경로, 이름 또는 문자열 UUID를 사용하여 다른 노드를 참조합니다.

#### 예 {#example-5}

문서(a)에서 다른 문서(b)로의 &quot;참조&quot;를 허용한다고 가정해 보겠습니다. 참조 등록 정보를 사용하여 이 관계를 모델링하면 두 문서가 저장소 수준에서 연결됩니다. 참조 속성의 대상이 존재하지 않을 수 있으므로 문서 (a)를 개별적으로 내보내기/가져올 수 없습니다. 병합, 업데이트, 복원 또는 클론 작업과 같은 다른 작업도 영향을 받습니다.

따라서 이러한 참조를 &quot;약한 참조&quot;로 모델링하거나(JCR v1.0에서 이것은 기본적으로 대상 노드의 uuid를 포함하는 문자열 속성으로 요약됨) 경로를 사용합니다. 때로는 이 길이 다음으로 시작하기에 더 의미가 있습니다.

참조가 흔들리면 시스템이 실제로 작동하지 않는 사용 사례가 있다고 생각하지만 직접 경험한 것에서 좋은 &#39;실제&#39;하면서도 간단한 예를 떠올릴 수는 없다.

### 규칙 #6: 파일은 파일입니다. {#rule-files-are-files}

#### 설명 {#explanation-6}

콘텐츠 모델이 파일이나 폴더와 같은 냄새라도 원격으로 발생하는 것을 노출하면 를 사용(또는 확장)하려고 합니다 `nt:file`, `nt:folder`, 및 `nt:resource`.

경험상 많은 일반 애플리케이션은 nt:folder 및 nt:files와의 상호 작용을 묵시적으로 허용하며 추가 메타 정보로 보강된 경우 이러한 이벤트를 처리하고 표시하는 방법을 알고 있습니다. 예를 들어 JCR 위에 있는 CIF 또는 WebDAV와 같은 파일 서버 구현과 직접적인 상호 작용은 암시적이 됩니다.

내 생각엔 다음과 같은 방법을 사용할 수 있을 것 같다: 파일 이름과 mime 유형을 저장해야 한다면 `nt:file`/ `nt:resource` 잘 어울리네요 여러 &quot;파일&quot;이 있을 수 있는 경우 nt:folder를 저장하는 것이 좋습니다.

리소스에 대한 메타 정보를 추가해야 하는 경우 &quot;작성자&quot; 또는 &quot;설명&quot; 속성을 예로 들면 을 확장합니다. `nt:resource` 아님 `nt:file`. nt:file은 거의 확장하지 않고 자주 확장합니다. `nt:resource`.

#### 예 {#example-6}

누군가가 다음 위치의 블로그 항목에 이미지를 업로드한다고 가정해 보겠습니다.

```xml
/content/myblog/posts/iphone_shipping
```

그리고 아마도 초기 장 반응은 그림을 포함하는 이항성을 추가하는 것일 것이다.

이진 속성(이름이 무관하고 mime 유형이 암시적이라고 가정할 경우)을 사용하는 데 적합한 사용 사례가 있지만, 이 경우 블로그 예제에 다음 구조를 사용하는 것이 좋습니다.

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### 규칙 #7: ID는 악의입니다. {#rule-ids-are-evil}

#### 설명 {#explanation-7}

관계형 데이터베이스에서 ID는 관계를 표현하는 데 필요한 수단이므로 사용자는 컨텐츠 모델에서도 ID를 사용하는 경향이 있습니다. 대부분 잘못된 이유로.

콘텐츠 모델이 &quot;ID&quot;로 끝나는 속성으로 가득 찬 경우 계층 구조를 제대로 사용하지 않는 것일 수 있습니다.

일부 노드는 라이브 사이클 전체에서 안정적인 식별이 필요한 것이 사실입니다. 하지만 생각보다 적습니다. 그러나 `mix:referenceable` 에는 이러한 메커니즘이 저장소에 내장되어 있으므로 안정적인 방식으로 노드를 식별할 수 있는 추가 수단을 마련할 필요가 없습니다.

항목은 경로로 식별할 수 있습니다. 또한 UNIX® 파일 시스템의 하드 링크보다 대부분의 사용자에게 &quot;심볼릭 링크&quot;가 훨씬 더 유용한 만큼 대부분의 애플리케이션이 타겟 노드를 참조하는 경로도 의미가 있습니다.

더 중요한 것은 **mix**:referenceable : 실제로 참조해야 하는 시점에 노드에 적용할 수 있음을 의미합니다.

따라서 &quot;Document&quot; 유형의 노드를 잠재적으로 참조하고자 한다고 해서 &quot;Document&quot; 노드 유형이에서 확장되어야 하는 것은 아닙니다. `mix:referenceable` 정적 방식으로. 이는 &quot;문서&quot;의 모든 인스턴스에 동적으로 추가될 수 있기 때문입니다.

#### 예 {#example-7}

사용:

```xml
/content/myblog/posts/iphone_shipping/attachments/front.jpg
```

대신:

```xml
[Blog]
-- blogId
-- author
[Post]
-- postId
-- blogId
-- title
-- text
-- date
[Attachment]
-- attachmentId
-- postId
-- filename
+ resource (nt:resource)
```
