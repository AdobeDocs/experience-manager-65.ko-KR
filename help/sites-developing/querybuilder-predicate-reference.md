---
title: 쿼리 빌더 조건자 참조
description: Query Builder API에 대한 전체 설명 참조.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: 54b942f9-5dd9-4826-9a0a-028f2d7b8e41
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2313'
ht-degree: 2%

---

# 쿼리 빌더 조건자 참조{#query-builder-predicate-reference}

>[!CAUTION]
>
>이 페이지의 정보는 완전하지 않습니다.
>
>자세한 내용은 아래 목록을 참조하십시오. **사용 가능한 술어** Query Builder Debugger 콘솔에서 다음을 수행합니다. 예:
>* [http://localhost:4502/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)
>
>예를 들어 다음을 참조하십시오.
>
>* [http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29](http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29)

## 일반 {#general}

* [루트](#root)
* [그룹](#group)
* [orderby](#orderby)

## 술어 {#predicates}

* [부울 속성](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [날짜 비교](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [다터랑주](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [excludepaths](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [전체 텍스트](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [언어](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [주요 자산](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [memberOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [nodename](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [가공되지 않음](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [경로](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [속성](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [rangeproperty](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [상대 날짜 범위](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [유사](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [태그](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [태그](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [유형](/help/sites-developing/querybuilder-predicate-reference.md#type)

### 부울 속성 {#boolproperty}

JCR 부울 속성에서 일치합니다. 값만 수락 `true`&quot; 및 &quot; `false`&quot;. 인 경우 `false`&quot;, 속성에 값이 있는지 여부가 일치합니다.&quot; `false`또는 이 링크가 전혀 없는 경우입니다. 이 기능은 활성화된 경우에만 설정되는 부울 플래그를 확인하는 데 유용합니다.

상속된 &quot; `operation`&quot;매개 변수에는 의미가 없습니다.

패싯 추출을 지원합니다. 각각에 대한 버킷을 제공합니다. `true` 또는 `false` 값(기존 속성만 해당).

#### 속성 {#properties}

* **부울 속성**
속성에 대한 상대 경로(예: ) `myFeatureEnabled` 또는 `jcr:content/myFeatureEnabled`.

* **값**
속성을 확인할 값, &quot; `true`&quot; 또는 &quot; `false`&quot;.

### contentfragment {#contentfragment}

결과를 콘텐츠 조각으로 제한합니다.

필터링을 지원하지 않습니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-1}

* **contentfragment**
모든 값과 함께 사용하여 콘텐츠 조각을 확인할 수 있습니다.

### 날짜 비교 {#datecomparison}

두 JCR DATE 속성을 비교합니다. 같음, 같지 않음, 크거나 같음 또는 같은지 테스트할 수 있습니다.

이는 필터링 전용 술어이며 검색 색인을 사용할 수 없습니다.

#### 속성 {#properties-2}

* **property1**

  첫 번째 날짜 속성에 대한 경로입니다.

* **property2**

  두 번째 날짜 속성에 대한 경로입니다.

* **작업**

  &quot; `equals`정확히 일치하려면 &quot; `!=`같지 않음 비교의 경우 &quot; `greater`property1이 property2보다 큰 경우 &quot; `>=`property1이 property2보다 크거나 같은 경우 기본값은 &quot;입니다. `equals`&quot;.

### 다터랑주 {#daterange}

날짜/시간 간격에 대해 JCR DATE 속성과 일치합니다. 날짜 및 시간에 대해 ISO8601 형식을 사용합니다( `YYYY-MM-DDTHH:mm:ss.SSSZ`) 및 는 다음과 같은 부분 표현도 허용합니다. `YYYY-MM-DD`. 또는 UTC 시간대(UNIX® 시간 형식)에서 타임스탬프가 1970년 이후 밀리초 수로 제공될 수 있습니다.

두 타임스탬프 사이에 있는 모든 항목, 지정된 날짜보다 최신 항목 또는 오래된 항목을 찾을 수 있으며 포함 간격과 열기 간격 사이에서 선택할 수도 있습니다.

패싯 추출을 지원합니다. 버킷을 &quot;오늘&quot;, &quot;이번 주&quot;, &quot;이번 달&quot;, &quot;지난 3개월&quot;, &quot;올해&quot;, &quot;지난해&quot; 및 &quot;지난해보다 이전&quot;에 제공합니다.

필터링을 지원하지 않습니다.

#### 속성 {#properties-3}

* **속성**

  상대 경로 `DATE` 속성(예: ) `jcr:lastModified`.

* **하한**

  예를 들어 속성을 확인하기 위해 바인딩된 하한 날짜 `2014-10-01`.

* **lowerOperation**

  &quot; `>`&quot;(최신) 또는 &quot; `>=`&quot;(또는 그 이상)은 다음에 적용됩니다. `lowerBound`. 기본값은 &quot;입니다. `>`&quot;.

* **상한**

  속성을 확인할 상한값(예: ) `2014-10-01T12:15:00`.

* **upperOperation**

  &quot; `<`&quot;(이전) 또는 &quot; `<=`&quot;(또는 그 이상)은 다음에 적용됩니다. `upperBound`. 기본값은 &quot;입니다. `<`&quot;.

* **시간대**

  ISO-8601 날짜 문자열로 제공되지 않을 때 사용할 표준 시간대의 ID입니다. 기본값은 시스템의 기본 시간대입니다.

### excludepaths {#excludepaths}

해당 경로가 정규 표현식과 일치하는 결과에서 노드를 제외합니다.

이는 필터링 전용 술어이며 검색 색인을 사용할 수 없습니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-4}

* **excludepaths**

  결과 경로에 대해 일치하는 정규 표현식이며 결과에서 일치하는 정규 표현식은 제외됩니다.

### 전체 텍스트 {#fulltext}

전체 텍스트 색인에서 용어를 검색합니다.

필터링을 지원하지 않습니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-5}

* **전체 텍스트**

  전체 텍스트 검색어입니다.

* **relPath**

  속성 또는 하위 노드에서 검색할 상대 경로입니다. 이 속성은 선택 사항입니다.

### 그룹 {#group}

중첩된 조건을 빌드할 수 있습니다. 그룹은 중첩 그룹을 포함할 수 있습니다. Query Builder 쿼리의 모든 항목은 암시적으로 루트 그룹에 있으며 `p.or` 및 `p.not` 매개 변수도 마찬가지입니다.

값에 대해 두 속성 중 하나를 일치시키는 예제:

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

개념적으로 `(1_property` 또는 `2_property)`.

중첩 그룹의 예:

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

검색어 &quot;**관리**&#x200B;의 페이지 내 &quot; `/content/geometrixx/en` 또는 의 에셋에서 `/content/dam/geometrixx`.

개념적으로 `fulltext AND ( (path AND type) OR (path AND type) )`. 이러한 OR 조인은 성능을 위해 좋은 색인이 필요합니다.

#### 속성 {#properties-6}

* **p.or**

  로 설정된 경우 `true`&quot;그룹에 있는 하나의 술어만 일치해야 합니다. 기본값은 &quot;입니다. `false`&quot;, 모두 일치해야 함

* **p.not**

  로 설정된 경우 `true`&quot;, 그룹을 부정합니다(기본값:&quot;). `false`&quot;).

* **&lt;predicate>**

  중첩된 술어를 추가합니다.

* **N_&lt;predicate>**

  다음과 같이 여러 중첩된 술어를 동시에 추가합니다. `1_property, 2_property, ...`.

### hasPermission {#haspermission}

현재 세션에 지정된 항목으로 결과를 제한합니다. [JCR 권한.](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

이는 필터링 전용 술어이며 검색 색인을 사용할 수 없습니다. 패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-7}

* **hasPermission**

  현재 사용자 세션에 해당 노드가 반드시 있어야 하는 쉼표로 구분된 JCR 권한입니다. 예를 들어, `jcr:write`, `jcr:modifyAccessControl`.

### 언어 {#language}

특정 언어로 CQ 페이지를 찾습니다. 이렇게 하면 페이지 언어 속성과 종종 최상위 사이트 구조에 언어 또는 로케일을 포함하는 페이지 경로를 모두 볼 수 있습니다.

이는 필터링 전용 술어이며 검색 색인을 사용할 수 없습니다.

패싯 추출을 지원합니다. 각 고유 언어 코드에 대한 버킷을 제공합니다.

#### 속성 {#properties-8}

* **언어**

  ISO 언어 코드(예: &quot;)`de`&quot;

### 주요 자산 {#mainasset}

노드가 DAM 주 자산이고 하위 자산이 아닌지 확인합니다. 이는 기본적으로 &quot;하위 에셋&quot; 노드 내에 없는 모든 노드입니다. 이는 을(를) 확인하지 않습니다 `dam:Asset` 노드 유형. 이 술어를 사용하려면 &quot; `mainasset=true`&quot; 또는 &quot; `mainasset=false`&quot;, 더 이상의 속성이 없습니다.

이는 필터링 전용 술어이며 검색 색인을 사용할 수 없습니다.

Facet 추출을 지원하고 기본 및 하위 에셋에 대해 두 개의 버킷을 제공합니다.

#### 속성 {#properties-9}

* **주요 자산**

  부울, &quot; `true`기본 자산의 경우, &quot; `false`하위 에셋의 경우 &quot;.

### memberOf {#memberof}

특정 항목의 멤버인 항목 검색 [sling 리소스 컬렉션](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

이는 필터링 전용 술어이며 검색 색인을 사용할 수 없습니다. 패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-10}

* **memberOf**

  Sling 리소스 컬렉션 경로.

### nodename {#nodename}

JCR 노드 이름에서 일치합니다.

패싯 추출을 지원합니다. 각 고유한 노드 이름(파일 이름)에 대한 버킷을 제공합니다.

#### 속성 {#properties-11}

* **nodename**

  와일드카드를 허용하는 노드 이름 패턴: `*` = any 또는 no char, `?` = 모든 문자, `[abc]` = 대괄호로 묶인 문자만.

### 가공되지 않음 {#notexpired}

JCR DATE 속성이 현재 서버 시간보다 크거나 같은지 확인하여 항목을 일치시킵니다. &quot;&quot;에서 확인하는 데 사용할 수 있습니다. `expiresAt`&quot;like date 속성 및 아직 만료되지 않은 날짜로만 제한( `notexpired=true`) 또는 가 이미 만료된 경우( `notexpired=false`).

필터링을 지원하지 않습니다.

데이터 범위 술어와 동일한 방식으로 패싯 추출을 지원합니다.

#### 속성 {#properties-12}

* **가공되지 않음**

  부울, &quot; `true`&quot;아직 만료되지 않은 경우(미래 또는 같은 날짜),&quot; `false`만료 날짜(과거 날짜)에 대해 &quot;&quot; 값을 설정합니다(필수).

* **속성**

  에 대한 상대 경로 `DATE` 확인할 속성(필수).

### orderby {#orderby}

결과를 정렬할 수 있습니다. 여러 속성별 순서 지정이 필요한 경우 숫자 접두사를 사용하여 이 조건자를 여러 번 추가해야 합니다. 예: `1_orderby=first`, `2_oderby=second`.

#### 속성 {#properties-13}

* **orderby**

  선행 @으로 표시된 JCR 속성 이름(예: ) `@jcr:lastModified` 또는 `@jcr:content/jcr:title`또는 쿼리의 다른 조건자(예: ) `2_property`(정렬 기준)

* **sort**

  정렬 방향, 다음 중 하나 `desc`내림차순 또는 &quot; `asc`오름차순(기본값)의 경우 &quot;.

* **사례**

  로 설정된 경우 `ignore`, 이는 정렬의 대/소문자를 구분하지 않게 합니다. 즉, &quot;a&quot;가 &quot;B&quot; 앞에 옵니다. 비어 있거나 누락된 경우 정렬은 대/소문자를 구분하며, 즉 &quot;B&quot;가 &quot;a&quot; 앞에 옵니다.

### 경로 {#path}

지정된 경로 내에서 검색합니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-14}

* **path**

  경로 패턴. 정확히 일치하는지에 따라 전체 하위 트리가 일치합니다(예: 추가) `//*` xpath에서 기본 경로는 포함되지 않지만(exact=false, default), 와일드카드()를 포함할 수 있는 정확한 경로 일치만 포함합니다. `*`); self 가 설정되면, 기본 노드를 포함하는 전체 하위 트리가 검색됩니다.

* **정확**

  If `exact` 는 true/on이고, 정확한 경로는 일치해야 하지만 단순 와일드카드( `*`), 이름은 일치하지만 &quot; `/`&quot;; false(기본값)이면 모든 하위 항목이 포함됩니다(선택 사항).

* **평평해**

  직접 하위만 검색합니다(예: &quot; 추가). `/*`xpath의 &quot;&quot;(다음과 같은 경우에만 사용됨) `exact`&#39;은(는) true가 아닙니다(선택 사항).

* **자가**

  하위 트리를 검색하지만 경로로 지정된 기본 노드를 포함합니다(와일드카드 없음).

### 속성 {#property}

JCR 속성 및 해당 값에 대해 일치합니다.

패싯 추출을 지원합니다. 결과의 각 고유 속성 값에 대한 버킷을 제공합니다.

#### 속성 {#properties-15}

* **속성**

  속성에 대한 상대 경로(예: ) `jcr:title`.

* **값**

  속성을 확인할 값입니다. JCR 속성 유형을 따라 문자열 전환으로 이동합니다.

* **N_value**

  사용 `1_value`, `2_value`, ...을 사용하여 여러 값(결합)을 확인하는 방법 `OR` 기본적으로, 포함 `AND` if and=true) (5.3 이후).

* **및**

  여러 값을 결합하려면 true로 설정합니다( `N_value`) 및 (5.3 이후)를 사용하는 경우

* **작업**

  &quot;`equals`정확히 일치하려면(기본값), &quot; `unequals`같지 않음 비교의 경우 &quot; `like`를 사용하는 경우 &quot; `jcr:like` xpath 함수(선택 사항), &quot; `not`일치 항목이 없는 경우 &quot;(예: &quot;`not(@prop)`xpath에서 &quot; 값 매개 변수는 무시됩니다.) 또는 &quot; `exists`&quot; 존재 확인(값이 true일 수 있음 - 속성이 존재해야 함, 기본값 - 또는 false - 와 같음) `not`&quot;).

* **깊이**

  속성/상대 경로가 존재할 수 있는 와일드카드 수준의 수입니다(예: `property=size depth=2` node/size, node/&amp;ast;/size 및 node/&amp;ast;/&amp;ast;/size)를 확인합니다.

### rangeproperty {#rangeproperty}

간격에 대해 JCR 속성과 일치합니다. 이는 다음과 같은 선형 유형이 있는 속성에 적용됩니다. `LONG`, `DOUBLE`, 및 `DECIMAL`. 대상 `DATE`에서는 최적화된 날짜 형식 입력이 있는 daterange 술어를 참조하십시오.

하한과 상한을 정의하거나 둘 중 하나만 정의할 수 있습니다. 작업(예: &quot;보다 작음&quot; 또는 &quot;작거나 같음&quot;)은 하한과 상한에 대해서도 개별적으로 지정할 수 있습니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-16}

* **속성**

  속성에 대한 상대 경로입니다.

* **하한**

  다음에 대한 속성을 확인할 하한입니다.

* **lowerOperation**

  &quot; `>`&quot;(기본값) 또는 &quot; `>=`&quot;, 다음에 적용됩니다. `lowerValue`

* **상한**

  다음에 대한 속성을 확인할 상한입니다.

* **upperOperation**

  &quot; `<`&quot;(기본값) 또는 &quot; `<=`&quot;, 다음에 적용됩니다. `lowerValue`

* **decimal**

  &quot; `true`checked 속성이 Decimal 형식인 경우 &quot;

### 상대 날짜 범위 {#relativedaterange}

일치 `JCR DATE` 현재 서버 시간을 기준으로 한 시간 오프셋을 사용하는 날짜/시간 간격에 대한 등록 정보입니다. 다음을 지정할 수 있습니다. `lowerBound` 및 `upperBound` 밀리초 값 또는 bugzilla 구문 사용 `1s 2m 3h 4d 5w 6M 7y` (1초, 2분, 3시간, 4일, 5주, 6개월, 7년) 접두사로 &quot; &quot;를 사용합니다. `-`현재 시간 이전의 음수 오프셋을 나타냅니다. 다음을 지정하는 경우 `lowerBound` 또는 `upperBound`다른 기본값은 0으로, 현재 시간을 의미합니다.

예:

* `upperBound=1h` (및 아니요 `lowerBound`)은(는) 다음 시간 내에 아무 것이나 선택합니다
* `lowerBound=-1d` (및 아니요 `upperBound`)을 클릭하여 지난 24시간 동안 모든 항목을 선택합니다
* `lowerBound=-6M` 및 `upperBound=-3M` 6개월에서 3개월 된 모든 항목을 선택합니다.
* `lowerBound=-1500` 및 `upperBound=5500` 는 과거 1500밀리초와 향후 5500밀리초 사이의 모든 항목을 선택합니다.
* `lowerBound=1d` 및 `upperBound=2d` 모레 중에 어떤 것이든 선택하십시오.

윤년은 고려하지 않고 모든 달은 30일입니다.

필터링을 지원하지 않습니다.

데이터 범위 술어와 동일한 방식으로 패싯 추출을 지원합니다.

#### 속성 {#properties-17}

* **상한**

  밀리초 단위로 바인딩된 상한 날짜 또는 `1s 2m 3h 4d 5w 6M 7y` 현재 서버 시간을 기준으로 1초, 2분, 3시간, 4일, 5주, 6개월, 7년) 음수 오프셋에 대해 &quot;-&quot;를 사용합니다.

* **하한**

  밀리초 단위의 하한 날짜 또는 `1s 2m 3h 4d 5w 6M 7y` 현재 서버 시간을 기준으로 1초, 2분, 3시간, 4일, 5주, 6개월, 7년) 음수 오프셋에 대해 &quot;-&quot;를 사용합니다.

### 루트 {#root}

루트 조건자 그룹. 그룹의 모든 기능을 지원하며 전역 쿼리 매개 변수를 설정할 수 있습니다.

&quot;루트&quot;라는 이름은 쿼리에서 사용되지 않으며 암시적입니다.

#### 속성 {#properties-18}

* **p.offset**

  결과 페이지의 시작, 즉 건너뛸 항목의 수를 나타내는 숫자입니다.

* **p.limit**

  페이지 크기를 나타내는 숫자입니다.

* **p.guessTotal**

  권장: 비용이 많이 들 수 있는 전체 결과 합계를 계산하지 마십시오. 계산할 최대 합계를 나타내는 숫자(예: 대략적인 크기와 더 작은 결과에 대한 정확한 숫자를 사용자에게 충분히 피드백하는 숫자) 또는 &quot; `true`필요한 최소값까지만 계산하려는 경우 `p.offset` + `p.limit`.

* **발췌**

  로 설정된 경우 `true`&quot;결과에 전체 텍스트 발췌본을 포함합니다.

* **p.hits**

  (JSON 서블릿만 해당) 다음 표준 히트(ResultHitWriter 서비스를 통해 확장 가능)를 사용하여 히트가 JSON으로 기록되는 방법을 선택합니다.

   * **단순**:

     다음과 같은 최소 항목 `path`, `title`, `lastmodified`, `excerpt` (설정된 경우).

   * **전체**:

     를 사용하는 노드의 Sling JSON 렌더링 `jcr:path` 히트의 경로 표시: 기본적으로 노드의 직접 속성만 나열하므로 다음과 같은 심층 트리 포함 `p.nodedepth=N`를 0으로 지정하면 전체, 무한 하위 트리를 의미합니다. `p.acls=true` 주어진 결과 항목에 현재 세션의 JCR 권한을 포함시키려면 다음을 수행합니다(매핑: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`).

   * **선택적**:

     다음에서 지정된 속성만 `p.properties`: 상대 경로의 공백으로 구분된(URL에 &quot;+&quot; 사용) 목록입니다. 상대 경로의 깊이가 1보다 큰 경우 이 매개 변수는 하위 객체로 표시됩니다. 특수 jcr:path 속성은 히트의 경로를 포함합니다

### savedquery {#savedquery}

지속 쿼리 빌더 쿼리의 모든 술어를 현재 쿼리에 하위 그룹 술어로 포함합니다.

이 경우 추가 쿼리가 실행되지 않고 현재 쿼리가 확장됩니다.

쿼리는 를 사용하여 프로그래밍 방식으로 지속할 수 있습니다. `QueryBuilder#storeQuery()`. 형식은 여러 줄 String 속성이거나 `nt:file` 쿼리를 Java™ 속성 형식의 텍스트 파일로 포함하는 노드입니다.

저장된 쿼리의 조건자에 대한 패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-19}

* **savedquery**

  저장된 쿼리의 경로(문자열 속성 또는 `nt:file` node).

### 유사 {#similar}

JCR XPath를 사용한 유사성 검색 `rep:similar()`.

필터링을 지원하지 않습니다. 패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-20}

* **유사**
유사한 노드를 찾을 노드의 절대 경로입니다.

* **로컬**
하위 노드의 상대 경로 또는 `.` 현재 노드의 경우(선택 사항, 기본값은 임) `.`&quot;).

### 태그 {#tag}

태그 제목 경로를 지정하여 하나 이상의 태그로 태그가 지정된 컨텐츠를 검색합니다.

패싯 추출을 지원합니다. 현재 태그 제목 경로를 사용하여 각 고유 태그에 대한 버킷을 제공합니다.

#### 속성 {#properties-21}

* **태그**

  찾을 태그 제목 경로(예: &quot;자산 속성 : 방향 / 가로&quot;).

* **N_value**

  사용 `1_value`, `2_value`, ... 여러 태그( 와 결합됨)를 확인하는 방법 `OR` 기본적으로, 포함 `AND` if and=true) (5.6 이후).

* **속성**

  살펴볼 속성(또는 속성에 대한 상대 경로)(기본값) `cq:tags`&quot;)

### 태그 {#tagid}

태그 ID를 지정하여 하나 이상의 태그로 태그가 지정된 컨텐츠를 검색합니다.

패싯 추출을 지원합니다. 현재 태그 ID를 사용하여 각 고유 태그에 대한 버킷을 제공합니다.

#### 속성 {#properties-22}

* **태그**

  태그 ID를 통해 찾을 수 있음(예: &quot; `properties:orientation/landscape`&quot;.

* **N_value**

  사용 `1_value`, `2_value`, ... 여러 tagid(와 결합)를 확인하는 방법 `OR` 기본적으로, 포함 `AND` if and=true) (5.6 이후).

* **속성**

  살펴볼 속성(또는 속성에 대한 상대 경로)(기본값) `cq:tags`&quot;).

### tagsearch {#tagsearch}

키워드를 지정하여 하나 이상의 태그로 태그가 지정된 콘텐츠를 검색합니다. 이렇게 하면 먼저 제목에 이러한 키워드가 포함된 태그를 검색한 다음 이러한 키워드가 태그가 지정된 항목으로만 결과를 제한합니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#Properties-1}

* **tagsearch**

  태그 제목에서 검색할 키워드입니다.

* **속성**

  살펴볼 속성(또는 속성에 대한 상대 경로)(기본값) `cq:tags`).

* **lang**

  현지화된 특정 태그 제목에서만 검색하려면 다음을 수행하십시오(예: `de`).

* **모두**

  (bool) 전체 태그, 즉 모든 제목, 설명 등을 검색합니다. &quot;l&quot;보다 우선함 `ang`&quot;.

### 유형 {#type}

결과를 기본 노드 유형 또는 믹스인 유형인 특정 JCR 노드 유형으로 제한합니다. 해당 노드 유형의 하위 유형도 찾습니다. 저장소 검색 인덱스는 효율적인 실행을 위해 노드 유형을 포함해야 합니다.

패싯 추출을 지원합니다. 결과의 각 고유 유형에 대한 버킷을 제공합니다.

#### 속성 {#Properties-2}

* **유형**

  검색할 노드 유형 또는 믹스인 이름(예: ) `cq:Page`.
