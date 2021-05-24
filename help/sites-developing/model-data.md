---
title: 데이터 모델링 - David Nuescheler의 모델
seo-title: 데이터 모델링 - David Nuescheler의 모델
description: David Nuescheler의 컨텐츠 모델링 권장 사항
seo-description: David Nuescheler의 컨텐츠 모델링 권장 사항
uuid: acb27e81-9143-4e0d-a37a-ba26491a841f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 39546c0a-b72f-42df-859b-98428ee0d5fb
exl-id: 6ce6a204-db59-4ed2-8383-00c6afba82b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1828'
ht-degree: 1%

---

# 데이터 모델링 - David Nuescheler의 모델{#data-modeling-david-nuescheler-s-model}

## 소스 {#source}

다음 세부 사항은 David Nuescheler에 의해 표현된 아이디어와 주석입니다.

David은 2010년 Adobe이 필요로 했던 글로벌 컨텐츠 관리 및 컨텐츠 인프라 소프트웨어의 선두 공급업체인 Day Software AG의 공동 창립자이자 CTO였습니다. 현재 Adobe의 엔터프라이즈 기술 담당 VP로 재직하고 있으며 컨텐츠 관리의 기술 표준인 JCR(Java Content Repository) API(Application Programming Interface)의 개발에도 참여하고 있습니다.

추가 업데이트는 [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel)에서도 볼 수 있습니다.

## David {#introduction-from-david}에서 소개

여러 논의에서 개발자는 JCR에서 컨텐츠 모델링에 대해 제시하는 기능 및 기능에 다소 불안함을 발견했습니다. 리포지토리에서 컨텐츠를 모델링하는 방법과 한 컨텐츠 모델이 다른 컨텐츠 모델보다 뛰어난 이유에 대한 안내서와 경험이 아직 없습니다.

관계형 세계에서는 소프트웨어 업계에서 데이터를 모델링하는 방법에 대한 경험이 많이 있지만 Dell은 여전히 컨텐츠 저장소 공간의 초기 단계에 있습니다.

저는 콘텐츠가 어떻게 모델링되어야 하는지에 대한 제 개인적인 의견을 표현함으로써 이 공백을 메우기 시작하고 싶습니다. 이것은 언젠가 개발자들 커뮤니티에 더 의미 있는 무언가를 졸업할 수 있을 것이라고 기대하며, 이것은 &quot;내 의견&quot;뿐만 아니라 더 일반적으로 적용 가능한 것이기도 합니다. 이렇게 빠르게 진화하는 첫 번째 시도를 생각해 보세요.

>[!NOTE]
>
>면책조항:이 지침들은 나의 개인적, 때로는 논란이 되는 견해를 표현한다. 나는 이 지침을 토론하고 구체화 하기를 고대하고 있다.

## 7개의 단순 규칙 {#seven-simple-rules}

### 규칙 #1:먼저 데이터를, 나중에 구조를 구성합니다. 그럴지도{#rule-data-first-structure-later-maybe}

#### 설명 {#explanation-1}

ERD 의미에서 선언된 데이터 구조에 대해 걱정하지 않는 것이 좋습니다. 처음에는

개발 중인 nt:구조화되지 않은(&amp; 친구)를 사랑하는 방법을 알아봅니다.

저는 스테파노가 이것을 꽤 많이 요약한다고 생각합니다.

내 최종적:구조가 비싸며 대부분의 경우 구조를 기본 스토리지에 명시적으로 선언할 필요가 없습니다.

애플리케이션이 기본적으로 사용하는 구조에 대한 암시적 계약이 있습니다. 블로그 게시물의 수정 날짜를 lastModified 속성에 저장한다고 가정합니다. 내 앱에서는 동일한 속성에서 수정 날짜를 다시 읽도록 자동으로 알 수 있으므로 명시적으로 선언할 필요가 없습니다.

필수 또는 유형 및 값 제약과 같은 추가적인 데이터 제약 조건은 데이터 무결성을 위해 필요한 경우에만 적용되어야 합니다.

#### 예 {#example-1}

예를 들어 &quot;blog post&quot; 노드에서 `lastModified` Date 속성을 사용하는 위의 예에서 특별한 노드 유형이 필요하다는 것을 의미하는 것은 아닙니다. 적어도 처음에는 블로그 게시물 노드에 `nt:unstructured`을 사용할 것입니다. 블로그 애플리케이션의 마지막 수정 날짜를 표시하려고 하기 때문에 (&quot;주문 기준&quot; 가능) 날짜라면 거의 신경 쓰지 않습니다. 어쨌든 블로그 작성 응용 프로그램을 통해 &quot;날짜&quot;를 지정해 놓은 상태이므로 반드시 `lastModified` 날짜가 nodetype 형태로 있음을 선언할 필요는 없습니다.

### 규칙 #2:콘텐츠 계층 구조를 만들면 안 됩니다.{#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### 설명 {#explanation-2}

컨텐츠 계층 은 매우 중요한 자산입니다. 그러니 그냥 이런 일이 없도록 디자인하세요. 노드에 대해 &quot;좋은&quot;, 사람이 읽을 수 있는 이름을 가지고 있지 않다면, 이것은 아마 재고해야 할 것입니다. 임의의 숫자가 결코 &quot;좋은 이름&quot;이 될 수 없다.

기존의 관계형 모델을 계층적 모델로 만드는 것이 매우 쉽지만, 그 과정에서 어떤 생각을 해야 합니다.

내 경험에서 액세스 제어 및 봉쇄를 고려하는 경우 일반적으로 컨텐츠 계층 구조에 좋은 영향을 줍니다. 파일 시스템인 것처럼 생각해 보십시오. 로컬 디스크에서 모델링하기 위해 파일과 폴더를 사용할 수도 있습니다.

개인적으로, 나는 처음에 많은 경우들에서 비밀 시스템보다 계층 규칙을 선호하고, 나중에 타이핑을 도입한다.

>[!CAUTION]
>
>컨텐츠 리포지토리의 구성 방식 역시 성능에 영향을 줄 수 있습니다. 최상의 성능을 위해 콘텐츠 저장소의 개별 노드에 첨부된 하위 노드의 수는 일반적으로 1&#39;000개를 초과할 수 없습니다.
>
>[CRX에서 처리할 수 있는 데이터 양은 얼마입니까?](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html) 추가 정보.

#### 예 {#example-2}

저는 다음과 같이 간단한 블로그 시스템을 모델링하고 싶습니다. 처음에는 이 시점에서 사용하는 각각의 노드 유형에도 신경 쓰지 않습니다.

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

제 생각에 명백한 것들 중 하나는 우리 모두가 더 이상의 설명없이 예시를 기반으로 컨텐츠의 구조를 이해한다는 것입니다.

처음에는 &quot;댓글&quot;을 &quot;게시물&quot;과 함께 저장하지 않는 이유는 합리적인 계층적 방식으로 적용할 액세스 제어 때문입니다.

위의 컨텐츠 모델을 사용하면 &quot;익명&quot; 사용자가 주석을 &quot;생성&quot;하도록 쉽게 허용할 수 있지만 나머지 작업 영역에 대해서는 익명 사용자를 읽기 전용 기반으로 유지할 수 있습니다.

### 규칙 #3:작업 공간은 clone(), merge() 및 update()용입니다. {#rule-workspaces-are-for-clone-merge-and-update}

#### 설명 {#explanation-3}

응용 프로그램에서 `clone()`, `merge()` 또는 `update()` 메서드를 사용하지 않는 경우 단일 작업 영역이 이동하는 것이 좋습니다.

&quot;해당 노드&quot;는 JCR 사양에 정의된 개념입니다. 기본적으로 소위 다른 작업 공간에서 동일한 컨텐츠를 나타내는 노드로 요약됩니다.

JCR은 작업 공간의 매우 추상적인 개념을 도입하여 많은 개발자들이 작업 공간으로 무엇을 해야 하는지 명확히 알 수 없게 합니다. 테스트를 위해 다음과 같은 작업 공간을 사용하겠습니다.

여러 작업 공간에 &quot;해당&quot; 노드(기본적으로 동일한 UUID를 가진 노드)가 많이 겹치는 경우 작업 공간을 사용하여 사용할 수 있습니다.

동일한 UUID를 가진 노드가 겹치지 않으면 작업 공간을 남용할 수 있습니다.

작업 공간은 액세스 제어에 사용해서는 안 됩니다. 특정 사용자 그룹에 대한 컨텐츠 가시성은 다른 작업 공간으로 구분하는 좋은 인수가 아닙니다. JCR에서는 컨텐츠 저장소에 &quot;액세스 제어&quot;를 사용하여 이 권한을 제공합니다.

작업 공간은 참조 및 쿼리의 경계입니다.

#### 예 {#example-3}

다음과 같은 작업에 작업 공간 사용:

* 프로젝트의 v1.2와 프로젝트의 v1.3 비교
* 컨텐츠의 &quot;개발&quot;, &quot;QA&quot; 및 &quot;게시된&quot; 상태

다음과 같은 작업에 작업 공간을 사용하지 마십시오.

* 사용자 홈 디렉토리
* public, private, local, ...과 같은 다양한 타겟 대상에 대한 별개의 컨텐츠입니다.
* 사용자별 메일 받은 편지함

### 규칙 #4:같은 이름의 형제자매를 주의하라.{#rule-beware-of-same-name-siblings}

#### 설명 {#explanation-4}

SNS(Same Name Sistence)는 XML을 통해 설계 및 표현되는 데이터 구조와의 호환성을 위해 사양에 도입되어 있지만, SNS는 JCR에 매우 유용하며, 리포지토리에 대한 상당한 오버헤드와 복잡성을 제공합니다.

경로 세그먼트 중 하나에 SNS가 포함된 컨텐츠 리포지토리의 모든 경로는 안정성이 훨씬 낮아지고, SNS를 제거하거나 재주문하면 다른 모든 SNS와 해당 하위 경로의 영향을 받습니다.

XML 가져오기 또는 기존 XML SNS와의 상호 작용은 필요하고도 유용할 수 있지만, SNS를 사용한 적이 없으며, &quot;녹색 필드&quot; 데이터 모델에는 절대 사용하지 않을 것입니다.

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

### 규칙 #5:참고는 해롭다고 여겨졌다.{#rule-references-considered-harmful}

#### 설명 {#explanation-5}

참조 무결성은 참조 무결성임을 의미합니다. 참조 무결성을 관리하는 저장소에 추가 비용을 추가하는 것이 아니라 컨텐츠 유연성 측면에서 비용이 많이 든다는 것을 이해하는 것이 중요합니다.

개인적으로 대롱한 참조를 처리할 수 없을 때 참조만 사용하고 경로, 이름 또는 문자열 UUID를 사용하여 다른 노드를 참조하는 경우 반드시 참조를 사용해야 합니다.

#### 예 {#example-5}

문서(a)에서 다른 문서(b)로 &quot;참조&quot;를 허용한다고 가정해 보겠습니다. 참조 등록 정보를 사용하여 이 관계를 모델링하는 경우 두 문서가 저장소 수준에 연결되어 있음을 의미합니다. 참조 속성의 대상이 존재하지 않을 수 있으므로 문서(a)를 개별적으로 내보내거나 가져올 수 없습니다. 병합, 업데이트, 복원 또는 클론과 같은 다른 작업도 영향을 받습니다.

따라서 이러한 참조를 &quot;weak-references&quot;로 모델링하거나(JCR v1.0에서 이것은 기본적으로 대상 노드의 uuid를 포함하는 문자열 속성으로 요약됨) 경로를 사용합니다. 때로 그 길은 다음으로 시작하는 것이 더 의미 있다.

참고로 매달려도 시스템이 제대로 작동하지 않는 활용 사례가 있다고 생각합니다. 하지만 제가 직접 경험한 좋은 &quot;진짜&quot;를 생각해낼 수는 없지만 간단한 예를 생각해낼 수는 없습니다.

### 규칙 #6:파일은 파일입니다.{#rule-files-are-files}

#### 설명 {#explanation-6}

컨텐츠 모델이 원격으로 *에서* 냄새가 나거나 사용하려는 파일 또는 폴더`nt:file`, `nt:folder` 및 `nt:resource`에서 확장되는 것을 노출하는 경우

내 경험에서 많은 일반 응용 프로그램은 nt:folder 및 nt:files와의 상호 작용을 허용하고 추가 메타 정보로 보강된 경우 해당 이벤트를 처리하고 표시하는 방법을 암묵적으로 알고 있습니다. 예를 들어, JCR 맨 위에 있는 CIFS 또는 WebDAV와 같은 파일 서버 구현과 직접 상호 작용은 암시적으로 설정됩니다.

나는 경험상 좋은 법칙으로 다음 것을 사용할 수 있다고 생각한다.파일 이름과 mime 유형을 저장해야 하는 경우 `nt:file`/ `nt:resource`이(가) 매우 잘 일치합니다. 여러 &quot;파일&quot;을 가질 수 있는 경우 nt:folder를 저장하기에 좋습니다.

리소스에 대한 메타 정보를 추가해야 하는 경우 &quot;author&quot; 또는 &quot;description&quot; 속성을 &quot;author&quot; 또는 &quot;description&quot; 속성으로 지정하고 `nt:file`이 아닌 `nt:resource`을 확장합니다. nt:file을 확장하거나 `nt:resource`을 자주 확장하는 경우는 거의 없습니다.

#### 예 {#example-6}

누군가 다음 위치에서 블로그 항목에 이미지를 업로드한다고 가정해 보겠습니다.

```xml
/content/myblog/posts/iphone_shipping
```

그리고 아마도 초기 장막 반응은 사진을 포함하는 이진 속성을 추가하는 것일 것입니다.

이진 속성만 사용하는 데 좋은 사용 사례가 있을 수 있지만(이름이 관련이 없고 mime 형식이 암시적이라고 가정해 보겠습니다). 이 경우 블로그 예제에 다음 구조를 사용하는 것이 좋습니다.

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### 규칙 #7:ID는 악합니다.{#rule-ids-are-evil}

#### 설명 {#explanation-7}

관계형 데이터베이스에서 ID는 관계를 표현하기 위해 필요한 방법이므로 사람들은 컨텐츠 모델에서도 ID를 사용하는 경향이 있습니다. 대부분 잘못된 이유들 때문에.

컨텐츠 모델에 &quot;Id&quot;로 끝나는 속성이 가득 찬 경우 계층 구조를 제대로 활용하지 않을 수 있습니다.

일부 노드는 라이브 주기 동안 안정적인 식별을 필요로 하는 것이 사실입니다. 생각보다 훨씬 적어요 mix:referenable은 리포지토리에 내장된 메커니즘을 제공하므로, 안정적으로 노드를 식별하는 추가적인 방법을 마련할 필요가 없습니다.

또한 항목을 경로별로 식별할 수 있으며, 대부분의 사용자가 unix 파일 시스템의 하드링크보다 &quot;symlink&quot;를 더 잘 사용할 수 있다는 점을 명심하십시오. 대부분의 애플리케이션에서 대상 노드를 참조하는 경로가 적절합니다.

더 중요한 것은 **mix**:reference가 가능한 것으로, 이 방법은 실제로 참조해야 하는 시점에 노드에 적용할 수 있습니다.

예를 들어, &quot;Document&quot; 유형의 노드를 잠재적으로 참조하려고 한다고 해서 &quot;Document&quot; 노드가 mix:reference에서 정적 방식으로 확장되어야 하는 것은 아닙니다. 이 노드는 &quot;Document&quot;의 어떤 인스턴스에도 동적으로 추가할 수 있기 때문입니다.

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
