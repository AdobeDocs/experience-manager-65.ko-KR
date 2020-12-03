---
title: 데이터 모델링 - David Nuescheler의 모델
seo-title: 데이터 모델링 - David Nuescheler의 모델
description: David Nuescheler의 컨텐츠 모델링 추천
seo-description: David Nuescheler의 컨텐츠 모델링 추천
uuid: acb27e81-9143-4e0d-a37a-ba26491a841f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 39546c0a-b72f-42df-859b-98428ee0d5fb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1828'
ht-degree: 1%

---


# 데이터 모델링 - David Nuescheler의 모델{#data-modeling-david-nuescheler-s-model}

## 소스 {#source}

다음은 David Nuescheler가 표현한 아이디어와 주석입니다.

David은 글로벌 컨텐츠 관리 및 컨텐츠 인프라 소프트웨어 부문의 선두 공급업체인 Day Software AG의 공동 창립자이자 CTO로 2010년 Adobe에 의해 요청되었습니다. 현재 Adobe의 기업 기술 담당 부사장 겸 최고인자로 컨텐츠 관리의 기술 표준인 JSR-170(Java Content Repository) API)를 개발하고 있습니다.

추가 업데이트는 [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel)에서도 확인할 수 있습니다.

## David {#introduction-from-david}의 소개

여러 가지 논의에서, 개발자는 JCR이 컨텐트 모델링에 대해 제시한 특징과 기능에 다소 불안하다는 것을 알게 되었다. 저장소에서 컨텐츠를 모델링하는 방법과 하나의 컨텐츠 모델이 다른 컨텐츠 모델과 비교하여 뛰어난 이유에 대한 가이드와 경험도 아직 없습니다.

관계형 환경에서 소프트웨어 업계는 데이터를 모델링하는 방법에 대한 많은 경험을 보유하고 있지만, Adobe는 여전히 컨텐츠 저장소 영역의 초기 단계에 있습니다.

저는 컨텐츠가 어떻게 모델링되어야 하는지에 대한 제 개인적인 의견을 표현함으로써 이 공백을 메우기 시작하고 싶습니다. 이것은 언젠가 개발자들이 &quot;내 의견&quot;뿐만 아니라 더 일반적으로 적용 가능한 어떤 것으로, 좀 더 의미 있는 무언가를 만들어낼 수 있기를 바랍니다. 그래서 이것을 빨리 발전시키는 것을 고려하십시오.

>[!NOTE]
>
>부인:이 지침들은 나의 개인적인, 때로는 논란이 되는 의견들을 나타낸다. 나는 이 가이드라인에 대해 토론하고 이를 개선하기를 고대하고 있다.

## 7개의 간단한 규칙 {#seven-simple-rules}

### 규칙 #1:데이터, 구조 그럴지도{#rule-data-first-structure-later-maybe}

#### 설명 {#explanation-1}

ERD의 선언된 데이터 구조에 대해 걱정하지 않는 것이 좋습니다. 처음에는

개발 시 비정형(&amp; 친구)을 선호하는 방법을 학습합니다.

저는 스테파노가 이 점을 꽤 많이 요약한다고 생각합니다.

내 수익:구조는 비용이 많이 들고 대부분의 경우 기본 스토리지에 구조를 명시적으로 선언할 필요가 없습니다.

응용 프로그램이 본질적으로 사용하는 구조에 대한 암시적 계약이 있습니다. 마지막으로 마지막으로 수정한 속성에 블로그 게시물의 수정 날짜를 저장한다고 가정합니다. My App은 동일한 속성에서 수정 날짜를 다시 읽는 것을 자동으로 인식하므로 명시적으로 선언할 필요가 없습니다.

필수 또는 유형 및 값 제약과 같은 추가 데이터 제약 조건은 데이터 통합적인 이유로 필요한 경우에만 적용되어야 합니다.

#### 예 {#example-1}

위의 예: &quot;blog post&quot; 노드에서 `lastModified` Date 속성을 사용하는 예제는 특수 nodetype이 필요하다는 의미는 아닙니다. 최소한 처음에는 블로그 게시물 노드에 대해 `nt:unstructured`을(를) 사용할 것입니다. 블로그애플리케이션에 마지막 수정 날짜(주문했을 수도 있음)를 표시하려고 하는데, 날짜인지 전혀 신경 쓰지 않습니다. 어쨌든 내 블로그 작성 응용 프로그램이 &quot;날짜&quot;를 거기에 넣을 것을 암시적으로 믿기 때문에, 정말로 `lastModified` 날짜가 ndetype 형식으로 있음을 선언할 필요가 없습니다.

### 규칙 #2:콘텐츠 계층 구조 개선{#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### 설명 {#explanation-2}

콘텐츠 계층 구조는 매우 중요한 자산입니다. 그러니 그냥 그렇게 하지 말고 디자인하세요. 만약 여러분이 한 노드에 대해 &quot;좋은&quot;, 사람이 읽을 수 있는 이름을 가지고 있지 않다면, 그것은 아마 여러분이 재고해야 할 어떤 것입니다. 임의의 숫자가 &quot;좋은 이름&quot;은 거의 아니다.

기존의 관계형 모델을 계층적 모델로 신속하게 배치하는 것은 매우 간단할 수 있지만, 이러한 프로세스에 몇 가지 생각을 적용해야 합니다.

내 경험에서 액세스 제어 및 컨테인먼트를 고려할 때 일반적으로 컨텐츠 계층 구조에 적합한 요인이 됩니다. 파일 시스템이라고 생각하면 됩니다. 로컬 디스크에 모델링하기 위해 파일과 폴더를 사용할 수도 있습니다.

개인적으로 저는 처음에 많은 경우들에서 비밀 시스템보다 계층 규칙을 선호하고, 나중에 타이핑을 도입합니다.

>[!CAUTION]
>
>콘텐츠 저장소의 구조화 방식도 성능에 영향을 줄 수 있습니다. 최상의 성능을 위해 콘텐츠 저장소의 개별 노드에 연결된 하위 노드의 수는 일반적으로 1000개를 초과할 수 없습니다.
>
>[CRX에서 처리할 수 있는 데이터의 양을 참조하십시오.](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html) 를 참조하십시오.

#### 예 {#example-2}

저는 다음과 같이 간단한 블로깅 시스템을 모델링할 것입니다. 처음에는 이 시점에서 사용하는 각각의 노트에 관심이 없습니다.

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

저는 우리 모두가 추가적인 설명 없이 예시를 기반으로 컨텐츠의 구조를 이해한다는 것이 분명해지고 있다고 생각합니다.

처음에 예상치 못한 점은 &quot;댓글&quot;을 &quot;게시물&quot;에 저장하지 않았던 이유입니다. 이는 제가 합리적으로 계층적 방식으로 적용할 액세스 제어 때문입니다.

위의 컨텐츠 모델을 사용하면 &quot;익명&quot; 사용자가 &quot;주석을 작성&quot;할 수 있지만 익명 사용자는 작업 영역의 나머지 부분에 대해 읽기 전용으로 유지할 수 있습니다.

### 규칙 #3:작업 영역은 clone(), merge() 및 update()용입니다. {#rule-workspaces-are-for-clone-merge-and-update}

#### 설명 {#explanation-3}

애플리케이션에서 `clone()`, `merge()` 또는 `update()` 메서드를 사용하지 않는 경우 단일 작업 영역이 이동하는 것이 가장 좋은 방법입니다.

&quot;해당 노드&quot;는 JCR 사양에 정의된 개념입니다. 기본적으로, 서로 다른 소위 작업 영역에서 동일한 컨텐츠를 나타내는 노드로 압축됩니다.

JCR은 작업 영역의 매우 추상적인 개념을 도입하여 많은 개발자들이 작업 영역을 어떻게 사용하는지 명확히 알 수 있도록 합니다. 테스트하기 위해 다음과 같은 작업 영역을 사용할 것을 제안합니다.

여러 작업 영역에 &quot;해당&quot; 노드(기본적으로 동일한 UUID를 가진 노드)가 상당히 겹치는 경우 작업 영역을 사용할 수 있습니다.

동일한 UUID가 있는 노드가 겹치지 않으면 작업 영역을 남용할 수 있습니다.

액세스 제어에는 작업 영역을 사용할 수 없습니다. 특정 사용자 그룹에 대한 컨텐츠의 가시성은 다른 작업 영역으로 컨텐츠를 구분하기 위한 좋은 인수가 아닙니다. JCR은 이에 대해 제공하기 위해 컨텐츠 저장소에 &quot;액세스 제어&quot;를 제공합니다.

작업 영역은 참조 및 쿼리의 경계입니다.

#### 예 {#example-3}

다음과 같은 작업 영역 사용:

* 프로젝트의 v1.2와 프로젝트의 v1.3 비교
* 컨텐츠의 &quot;개발&quot;, &quot;QA&quot; 및 &quot;게시된&quot; 상태

다음과 같은 작업에 작업 영역을 사용하지 마십시오.

* 사용자 홈 디렉토리
* 공개, 비공개, 로컬, 등과 같은 다양한 대상 대상을 위한 고유한 컨텐츠..
* 다른 사용자를 위한 메일 상자

### 규칙 #4:동종 형제들을 조심해라.{#rule-beware-of-same-name-siblings}

#### 설명 {#explanation-4}

SNS(Same Name Sistence)는 XML을 통해 설계되고 표현되는 데이터 구조를 호환하여 JCR에 매우 유용한 반면 SNS는 저장소에 대한 높은 간접비와 복잡성을 동반합니다.

경로 세그먼트 중 하나에 SNS를 포함하는 컨텐츠 저장소의 모든 경로는 훨씬 덜 안정화되며, SNS를 제거하거나 재정렬하면 다른 모든 SNS와 해당 하위 그룹의 경로에 영향을 줍니다.

XML을 가져오거나 기존 XML SNS와 상호 작용하는 경우 유용할 수 있지만 SNS를 사용한 적이 없으며 &quot;녹색 필드&quot; 데이터 모델에서는 절대 사용하지 않을 것입니다.

#### 예 {#example-4}

사용

```xml
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping
```

instead

```xml
/content/blog[1]/post[1]
/content/blog[1]/post[2]
```

### 규칙 5:유해하다고 생각되는 참조들.{#rule-references-considered-harmful}

#### 설명 {#explanation-5}

참조는 참조 무결성을 나타냅니다. 참조 무결성을 관리하는 저장소에 대한 추가 비용을 추가하는 것이 아니라 컨텐츠 유연성 측면에서 비용이 많이 든다는 점을 이해하는 것이 중요합니다.

개인적으로 나는 매끄러운 참조를 처리할 수 없고 다른 노드를 참조하기 위해 경로, 이름 또는 문자열 UUID를 사용할 수 없을 때만 참조를 사용하는 것을 확신한다.

#### 예 {#example-5}

문서(a)에서 다른 문서(b)에 대한 &quot;참조&quot;를 허용한다고 가정합니다. 참조 속성을 사용하여 이 관계를 모델링하는 경우 두 문서가 저장소 수준에 연결되어 있음을 의미합니다. (a) 참조 속성의 대상이 없을 수 있으므로 문서를 개별적으로 내보내거나 가져올 수 없습니다. 병합, 업데이트, 복원 또는 클론과 같은 다른 작업도 영향을 받습니다.

따라서 이러한 참조를 &quot;weak-references&quot;로 모델링하거나(JCR v1.0에서 이것은 기본적으로 대상 노드의 uuid를 포함하는 문자열 속성으로 압축됩니다) 경로를 간단히 사용할 수 있습니다. 때때로 그 길은 시작하기에 더 의미가 있다.

예를 들자면 시스템이 제대로 작동하지 못하는 경우도 있다고 생각합니다. 하지만 제가 직접 경험한 좋은 &quot;진짜&quot;를 생각해낼 수는 없습니다.

### 규칙 #6:파일은 파일입니다.{#rule-files-are-files}

#### 설명 {#explanation-6}

컨텐츠 모델에서 원격으로 *에서* 냄새가 나는 파일 또는 `nt:file`, `nt:folder` 및 `nt:resource`에서 확장하려는 폴더와 같은 것을 노출하는 경우

내 경험에서 많은 일반 애플리케이션은 nt:folder 및 nt:files와의 상호 작용을 허용하며 추가 메타 정보로 이러한 이벤트를 처리하고 표시하는 방법을 알고 있습니다. 예를 들어 JCR 상단에 있는 CIFS 또는 WebDAV와 같은 파일 서버 구현과의 직접적인 상호 작용은 암묵적으로 이루어집니다.

내 생각에, 경험상 좋은 법칙은 다음과 같다.파일 이름과 mime 형식을 저장해야 하는 경우 `nt:file`/ `nt:resource`은 매우 일치합니다. 여러 개의 &quot;파일&quot;을 가질 수 있는 경우 nt:folder는 이러한 파일을 저장하기에 좋습니다.

리소스에 대한 메타 정보를 추가해야 하는 경우, &quot;author&quot; 또는 &quot;description&quot; 속성을 &quot;a1/>이 아닌 `nt:resource`을(를) 확장합니다. `nt:file` nt:file을 확장하거나 `nt:resource`을(를) 자주 확장하는 경우는 거의 없습니다.

#### 예 {#example-6}

다음과 같은 블로그 항목에 이미지를 업로드하려고 한다고 가정합니다.

```xml
/content/myblog/posts/iphone_shipping
```

그리고 초기 직감적 반응은 사진을 포함하는 이진 속성을 추가하는 것일 수도 있습니다.

이진 속성만 사용할 수 있는 좋은 사용 사례가 있지만(이름이 관련이 없고 mime 형식이 암시적이라고 가정함) 이 경우 블로그 예제에 대해 다음 구조를 권장합니다.

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### 규칙 #7:ID는 악합니다.{#rule-ids-are-evil}

#### 설명 {#explanation-7}

관계형 데이터베이스 ID는 관계를 표현하는 데 필요한 수단이므로 사람들은 컨텐츠 모델에서도 이러한 ID를 사용하는 경향이 있습니다. 대부분 잘못된 이유로.

콘텐츠 모델에 &quot;Id&quot;로 끝나는 속성이 가득 차 있는 경우 계층을 제대로 활용하지 못할 수 있습니다.

어떤 노드들은 그들의 라이브 주기 동안 안정적인 식별이 필요한 것은 사실이다. 생각보다 훨씬 적습니다 mix:reference는 저장소에 내장된 이러한 메커니즘을 제공하므로, 안정적으로 노드를 식별할 수 있는 추가적인 방법을 찾을 필요가 없습니다.

또한 항목을 경로로 식별할 수 있으며, 대부분의 사용자가 unix 파일 시스템의 하드 링크보다 &quot;symlinks&quot;를 더 잘 이해할 수 있다는 점을 염두에 두십시오. 대부분의 애플리케이션에서 대상 노드를 참조하는 경로는 적절합니다.

더 중요한 것은, 이 매개 변수가 **mix**:reference이므로 실제로 참조해야 하는 시점에 노드에 적용할 수 있습니다.

예를 들어, &quot;Document&quot; 유형의 노드를 잠재적으로 참조하고 싶었기 때문에 &quot;Document&quot; 노디트라는 유형이 &quot;Document&quot;의 모든 인스턴스에 동적으로 추가할 수 있으므로 혼합:참조 범위를 정적인 방식으로 확장해야 하는 것은 아닙니다.

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

