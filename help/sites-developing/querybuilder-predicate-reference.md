---
title: 쿼리 빌더 술어 참조
seo-title: Query Builder Predicate Reference
description: Query Builder API에 대한 전체 설명 참조입니다.
seo-description: Complete predicate reference for the Query Builder API.
uuid: af0e269e-7d52-4032-b22e-801c7b5dccfa
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 94a05894-743a-4ace-a292-bfee90ba9068
exl-id: 54b942f9-5dd9-4826-9a0a-028f2d7b8e41
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '2310'
ht-degree: 3%

---

# 쿼리 빌더 술어 참조{#query-builder-predicate-reference}

## 일반 {#general}

* [루트](#root)
* [그룹](#group)
* [orderby](#orderby)

## 설명 {#predicates}

* [부울 속성](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparison](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [daterange](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [제외 경로](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [전체 텍스트](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [언어](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [유지 관리](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [memberOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [노네임](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [만료되지 않음](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [경로](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [속성](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [rangeproperty](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [relativedaterange](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [유사](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [태그](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [tagid](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [유형](/help/sites-developing/querybuilder-predicate-reference.md#type)

### 부울 속성 {#boolproperty}

JCR 부울 속성에 대해 일치합니다. 값은 &quot; `true`&quot; 및 &quot; `false`&quot;. 의 경우 `false`&quot;. 속성에 &quot; 값이 있으면 일치합니다. `false`또는 전혀 존재하지 않는 경우 이 기능은 활성화되었을 때만 설정되는 부울 플래그를 확인하는 데 유용합니다.

상속된 &quot; `operation`매개 변수에는 의미가 없습니다.

패싯 추출을 지원합니다. 은 각 `true` 또는 `false` 값을 지정한 경우 이해할 수 있도록 해줍니다.

#### 속성 {#properties}

* **부울 속성**
속성에 대한 상대 경로(예: 
`myFeatureEnabled` 또는 `jcr:content/myFeatureEnabled`

* **value**
속성을 확인할 값, 
`true`&quot; 또는 &quot; `false`&quot;

### contentfragment {#contentfragment}

결과를 컨텐츠 조각으로 제한합니다.

필터링을 지원하지 않습니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-1}

* **contentfragment**
값과 함께 사용하여 컨텐츠 조각을 확인할 수 있습니다.

### dateComparison {#datecomparison}

두 JCR 날짜 속성을 서로 비교합니다. 같음, 같지 않음, 크거나 같음 여부를 테스트할 수 있습니다.

필터링 전용 조건이며 검색 색인을 활용할 수 없습니다.

#### 속성 {#properties-2}

* **property1**

   첫 번째 날짜 속성의 경로

* **property2**

   두 번째 날짜 속성의 경로입니다

* **작업**

   &quot; `equals`&quot; 정확히 일치하려면 &quot; `!=`&quot; 비같음 비교의 경우 &quot; `greater`&quot; property1이 property2보다 큰 경우 &quot; `>=`속성1이 property2보다 크거나 같음 &quot;입니다. 기본값은 &quot; 입니다. `equals`&quot;.

### daterange {#daterange}

날짜/시간 간격에 대해 JCR 날짜 속성을 일치시킵니다. 날짜 및 시간에 ISO8601 형식을 사용합니다( `YYYY-MM-DDTHH:mm:ss.SSSZ`) 및 는 다음과 같은 부분 표현을 허용합니다 `YYYY-MM-DD`. 또는 타임스탬프를 UTC 시간대(unix 시간 형식)에서 1970년부터 밀리초 수로 제공할 수 있습니다.

두 개의 타임스탬프(지정된 날짜보다 최신 또는 이전 항목) 사이의 항목을 찾고, 포함 및 열기 간격 중에서 선택할 수도 있습니다.

패싯 추출을 지원합니다. 에서는 &quot;오늘&quot;, &quot;이번 주&quot;, &quot;이번 달&quot;, &quot;지난 3개월&quot;, &quot;올해&quot;, &quot;작년&quot; 및 &quot;작년보다 이전&quot; 버킷을 제공합니다.

필터링을 지원하지 않습니다.

#### 속성 {#properties-3}

* **속성**

   에 대한 상대 경로 `DATE` 속성(예: `jcr:lastModified`

* **lowerBound**

   예를 들어, check 속성에 바인딩된 보다 낮은 날짜 `2014-10-01`

* **lowerOperation**

   &quot; `>`&quot;(최신) 또는 &quot; `>=`&quot;(또는 그 이상)은 `lowerBound`. 기본값은 &quot; 입니다. `>`&quot;.

* **upperBound**

   예를 들어 속성을 확인하도록 상한을 지정합니다. `2014-10-01T12:15:00`

* **upperOperation**

   &quot; `<`&quot; (이전) 또는 &quot; `<=`&quot;(또는 그 이상)은 `upperBound`. 기본값은 &quot; 입니다. `<`&quot;.

* **timeZone**

   ISO-8601 날짜 문자열로 제공되지 않을 때 사용할 시간대 ID입니다. 기본값은 시스템의 기본 시간대입니다.

### 제외 경로 {#excludepaths}

경로가 정규 표현식과 일치하는 결과에서 노드를 제외합니다.

필터링 전용 조건이며 검색 색인을 활용할 수 없습니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-4}

* **제외 경로**

   결과 경로에 대해 일치하는 정규 표현식에서 결과에서 일치하는 항목을 제외합니다.

### 전체 텍스트 {#fulltext}

전체 텍스트 색인에서 용어를 검색합니다.

필터링을 지원하지 않습니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-5}

* **전체 텍스트**

   전체 텍스트 검색어

* **relPath**

   속성 또는 하위 노드에서 검색할 상대 경로입니다. 이 속성은 선택 사항입니다.

### 그룹 {#group}

중첩된 조건을 만들 수 있습니다. 그룹에는 중첩된 그룹이 포함될 수 있습니다. QueryBuilder 쿼리의 모든 항목이 암시적으로 루트 그룹에 있으며 이는 `p.or` 및 `p.not` 매개 변수도 참조하십시오.

값에 대해 두 속성 중 하나를 일치시키는 예:

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

검색어 &quot;**관리**&quot; `/content/geometrixx/en` 또는 의 자산 `/content/dam/geometrixx`.

개념적으로 `fulltext AND ( (path AND type) OR (path AND type) )`. 이러한 OR 조인은 성능에 좋은 인덱스가 필요합니다.

#### 속성 {#properties-6}

* **p.또는**

   을(를) &quot;로 설정합니다. `true`&quot;, 그룹의 술어는 하나만 일치해야 합니다. 기본값은 &quot;입니다. `false`&quot;, 즉 모두 일치해야 함

* **p.not**

   을(를) &quot;로 설정합니다. `true`&quot;, 이 값은 그룹을 무효화합니다(기본값은 &quot; `false`&quot;)

* **&lt;predicate>**

   중첩 설명 추가

* **N_&lt;predicate>**

   과 같이 여러 중첩 설명을 동시에 추가합니다. `1_property, 2_property, ...`

### hasPermission {#haspermission}

현재 세션에 지정된 항목이 있는 항목으로 결과를 제한합니다 [JCR 권한.](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

필터링 전용 조건이며 검색 색인을 활용할 수 없습니다. 패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-7}

* **hasPermission**

   해당 노드에 대해 현재 사용자 세션이 모두 가져야 하는 쉼표로 구분된 JCR 권한 예 `jcr:write`, `jcr:modifyAccessControl`

### 언어 {#language}

특정 언어로 CQ 페이지를 찾습니다. 여기서는 페이지 언어 속성과 페이지 경로 모두를 살펴봅니다. 페이지 경로는 최상위 사이트 구조의 언어나 로케일을 종종 포함합니다.

필터링 전용 조건이며 검색 색인을 활용할 수 없습니다.

패싯 추출을 지원합니다. 은 각 고유 언어 코드에 대한 버킷을 제공합니다.

#### 속성 {#properties-8}

* **언어**

   ISO 언어 코드(예: &quot;) `de`&quot;

### 유지 관리 {#mainasset}

노드가 하위 자산이 아니라 DAM 주 자산인지 확인합니다. 이것은 기본적으로 &quot;하위 자산&quot; 노드 내에 없는 모든 노드입니다. 이 옵션을 선택하면 `dam:Asset` 노드 유형입니다. 이 설명을 사용하려면 &quot; `mainasset=true`&quot; 또는 &quot; `mainasset=false`&quot;더 이상 속성이 없습니다.

필터링 전용 조건이며 검색 색인을 활용할 수 없습니다.

패싯 추출을 지원합니다. 은 기본 및 하위 자산에 대해 2개의 버킷을 제공합니다.

#### 속성 {#properties-9}

* **유지 관리**

   부울, &quot; `true`&quot; 기본 자산의 경우 &quot; `false`하위 자산

### memberOf {#memberof}

특정 항목의 멤버인 항목을 찾습니다. [sling 리소스 컬렉션](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

필터링 전용 조건이며 검색 색인을 활용할 수 없습니다. 패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-10}

* **memberOf**

   Sling 리소스 컬렉션 경로

### 노네임 {#nodename}

JCR 노드 이름에 일치합니다.

패싯 추출을 지원합니다. 은 각 고유한 노드 이름(파일 이름)에 대한 버킷을 제공합니다.

#### 속성 {#properties-11}

* **노네임**

   와일드카드를 사용할 수 있는 노드 이름 패턴: `*` = 임의 또는 문자 없음 `?` = any char, `[abc]` = 대괄호로 묶인 문자만

### 만료되지 않음 {#notexpired}

JCR DATE 속성이 현재 서버 시간보다 크거나 같은지 확인하여 항목과 일치합니다. 이를 사용하여 &quot; `expiresAt`&quot; 날짜 속성과 비슷하며 아직 만료되지 않은 속성( `notexpired=true`) 또는 이미 만료된 파일( `notexpired=false`).

필터링을 지원하지 않습니다.

daterange 설명과 동일한 방식으로 면 추출을 지원합니다.

#### 속성 {#properties-12}

* **만료되지 않음**

   부울, &quot; `true`&quot; 아직 만료되지 않은 경우(미래 또는 같은 날짜), &quot; `false`&quot; 만료됨(과거 날짜)(필수)

* **속성**

   의 상대 경로 `DATE` 확인할 속성(필수)

### orderby {#orderby}

결과를 정렬할 수 있습니다. 여러 속성별 순서가 필요한 경우 다음과 같이 숫자 접두어를 사용하여 이 조건자를 여러 번 추가해야 합니다 `1_orderby=first`, `2_oderby=second`.

#### 속성 {#properties-13}

* **orderby**

   선행 @(예: )로 표시된 JCR 속성 이름 `@jcr:lastModified` 또는 `@jcr:content/jcr:title`또는 쿼리의 다른 조건자(예: `2_property`, 정렬 대상

* **정렬**

   정렬 방향: `desc`&quot; 내림차순 또는 &quot; `asc`오름차순(기본값)

* **사례**

   을(를) &quot;로 설정합니다. `ignore`&quot;은 대소문자를 구분하지 않게 합니다. 즉, &quot;a&quot;가 &quot;B&quot; 앞에 옵니다. 비어 있거나 비워 두면 대소문자를 구분합니다. 즉, &quot;B&quot;가 &quot;a&quot; 앞에 옵니다.

### 경로 {#path}

지정된 경로 내에서 검색합니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-14}

* **경로**

   경로 패턴; 완전 하위 트리는 정확히 일치하고 `//*` xpath에는 기본 경로가 포함되지 않지만 exact=false, default) 또는 와일드카드( `*`); 자체 설정되면 기본 노드를 포함하는 전체 하위 트리가 검색됩니다

* **정확히**

   if `exact` 가 true/on이면 정확한 경로가 일치해야 하지만, 단순 와일드카드( `*`), 이름이 일치하지만 &quot; `/`&quot;; false(기본값)이면 모든 하위 항목이 포함됩니다(선택 사항).

* **평면**

   직접 하위 항목만 검색합니다(예: &quot; 추가 `/*`&quot; in xpath (xpath에서) ( &#39; `exact`&#39; 는 true가 아닙니다. 선택 사항입니다)

* **self**

   하위 트리를 검색하지만 경로로 지정된 기본 노드를 포함합니다(와일드카드 없음).

### 속성 {#property}

JCR 속성 및 해당 값에 일치합니다.

패싯 추출을 지원합니다. 은 결과에서 각 고유 속성 값에 대한 버킷을 제공합니다.

#### 속성 {#properties-15}

* **속성**

   속성에 대한 상대 경로(예: `jcr:title`

* **정렬 단추**

   속성을 확인하는 값입니다. 는 JCR 속성 유형을 문자열 전환으로 따릅니다

* **N_value**

   사용 `1_value`, `2_value`, ... 여러 값(과 결합됨)을 확인하는 데 사용됩니다. `OR` 기본적으로 `AND` if 및=true)(5.3 이후)

* **및**

   여러 값을 결합하려면 true로 설정합니다( `N_value`) 및 AND(5.3 이후)

* **작업**

   &quot;`equals`&quot; 정확히 일치하려면(기본값), &quot; `unequals`&quot; 비같음 비교의 경우 &quot; `like`&quot; `jcr:like` xpath 함수(선택 사항), &quot; `not`&quot; 를 입력합니다(예: &quot;`not(@prop)`&quot; xpath에서 값 매개 변수는 무시됩니다.) 또는 &quot; `exists`&quot; 존재 확인을 위해(값은 true일 수 있음 - 속성이 있어야 함, 기본값 - 또는 false - 와 동일함 `not`&quot;)

* **깊이**

   속성/상대 경로가 존재할 수 있는 와일드카드 레벨 수(예: `property=size depth=2` 노드/크기, node/&amp;ast;/size and node/&amp;ast;/&amp;ast;/size)를 확인합니다.

### rangeproperty {#rangeproperty}

JCR 속성과 간격을 일치시킵니다. 이는 다음과 같은 선형 유형을 사용하는 속성에 적용됩니다. `LONG`, `DOUBLE` 및 `DECIMAL`. 대상 `DATE` 날짜 형식 입력이 최적화된 날짜 범위 설명을 참조하십시오.

하한을 정의하거나 상한을 정의하거나 그 중 하나만을 정의할 수 있습니다. 작업(예: &quot;less than&quot; 또는 &quot;lower or equals&quot;)도 각각 하한 및 상한(하한)에 대해 지정할 수 있습니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-16}

* **속성**

   속성의 상대 경로

* **lowerBound**

   하한값 검사 속성

* **lowerOperation**

   &quot; `>`&quot; (기본값) 또는 &quot; `>=`&quot;, 이 `lowerValue`

* **upperBound**

   속성 확인 시 상한을 설정할 수 있습니다.

* **upperOperation**

   &quot; `<`&quot; (기본값) 또는 &quot; `<=`&quot;, 이 `lowerValue`

* **십진수**

   &quot; `true`&quot;선택된 속성이 Decimal 형식이면

### relativedaterange {#relativedaterange}

일치 `JCR DATE` 현재 서버 시간을 기준으로 시간 오프셋을 사용하는 날짜/시간 간격에 대한 속성입니다. 다음을 지정할 수 있습니다 `lowerBound` 및 `upperBound` 밀리초 값 또는 bugzilla 구문 사용 `1s 2m 3h 4d 5w 6M 7y` (1초, 2분, 3시간, 4일, 5주, 6개월, 7년) 접두사가 &quot; `-`&quot;을 눌러 현재 시간 이전의 음수 오프셋을 나타냅니다. 다음과 같은 경우에만 `lowerBound` 또는 `upperBound`를 입력하면 다른 하나는 기본적으로 0으로 설정되며, 이것은 현재 시간을 의미합니다.

예:

* `upperBound=1h` (및 아니요) `lowerBound`)을 선택하면 다음 시간 안에 아무 것도 선택됩니다
* `lowerBound=-1d` (및 아니요) `upperBound`)을 선택하면 지난 24시간 동안 아무 것도 선택됩니다
* `lowerBound=-6M` 및 `upperBound=-3M` 6개월에서 3개월까지 어떤 것도 선택할 수 있습니다
* `lowerBound=-1500` 및 `upperBound=5500` 과거 1500밀리초와 향후 5500밀리초 사이의 항목을 선택할 수 있습니다
* `lowerBound=1d` 및 `upperBound=2d` 내일 모레 어떤 것을 선택해도

윤년은 고려하지 않고 모든 달은 30일입니다.

필터링을 지원하지 않습니다.

daterange 설명과 동일한 방식으로 면 추출을 지원합니다.

#### 속성 {#properties-17}

* **upperBound**

   밀리초 단위로 바인딩된 상위 날짜 `1s 2m 3h 4d 5w 6M 7y` 현재 서버 시간을 기준으로 한 1초, 2분, 3시간, 4일, 5주, 6개월, 7년)은 음수 오프셋을 사용하려면 &quot;-&quot;를 사용하십시오

* **lowerBound**

   밀리초 이하로 바인딩된 날짜 `1s 2m 3h 4d 5w 6M 7y` 현재 서버 시간을 기준으로 한 1초, 2분, 3시간, 4일, 5주, 6개월, 7년)은 음수 오프셋을 사용하려면 &quot;-&quot;를 사용하십시오

### 루트 {#root}

루트 설명 그룹입니다. 그룹의 모든 기능을 지원하고 글로벌 쿼리 매개 변수를 설정할 수 있도록 해줍니다.

&quot;root&quot;라는 이름은 쿼리에 사용되지 않고 암시적으로 사용됩니다.

#### 속성 {#properties-18}

* **p.offset**

   결과 페이지의 시작을 나타내는 숫자(즉, 건너뛸 항목 수)

* **p.limit**

   페이지 크기를 나타내는 숫자

* **p.guessTotal**

   권장 사항: 비용이 많이 들 수 있는 전체 결과 합계를 계산하지 마십시오. 최대 계산할 최대 총계를 나타내는 숫자(예: 1000, 대략적인 크기와 더 작은 결과를 위한 정확한 숫자를 사용자에게 제공하는 숫자) 또는 &quot; `true`&quot;을 사용하여 필요한 최소값만 카운트합니다. `p.offset` + `p.limit`

* **p.intract**

   을(를) &quot;로 설정합니다. `true`&quot;, 결과에 전체 텍스트 발췌문을 포함합니다

* **p.hits**

   (JSON 서블릿에 대해서만) 히트가 JSON으로 기록되는 방식을 선택하고 이러한 표준 방식(ResultHitWriter 서비스를 통해 확장 가능)을 사용합니다.

   * **단순한**:

      다음과 같은 항목 `path`, `title`, `lastmodified`, `excerpt` (설정된 경우)

   * **전체**:

      노드의 sling JSON 렌더링, `jcr:path` 히트의 경로를 나타냅니다. 기본적으로 노드의 직접 속성을 나열하고 `p.nodedepth=N`과 함께 0은 전체 무한 하위 트리를 의미합니다. 추가 `p.acls=true` 지정된 결과 항목에 현재 세션의 JCR 권한을 포함하려면 다음을 수행하십시오. `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)

   * **선택적**:

      에 지정된 속성만 `p.properties`: 상대 경로의 목록으로 구분된 공간(URL에서 &quot;+&quot; 사용) 목록입니다. 상대 경로에 깊이가 1보다 큰 경우 하위 개체로 표시됩니다. 특수 jcr:path 속성은 히트의 경로를 포함합니다

### savedquery {#savedquery}

하위 그룹 조건자로 현재 쿼리에 지속되는 querybuilder 쿼리의 모든 설명을 포함합니다.

추가 쿼리는 실행되지 않고 현재 쿼리를 확장합니다.

쿼리는 `QueryBuilder#storeQuery()`. 형식은 여러 줄 String 속성이나 `nt:file` 쿼리를 Java 속성 형식의 텍스트 파일로 포함하는 노드입니다.

저장된 쿼리의 조건자에 대한 패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-19}

* **savedquery**

   저장된 쿼리의 경로(문자열 속성 또는 `nt:file` node)

### 유사 {#similar}

JCR XPath를 사용한 유사성 검색 `rep:similar()`.

필터링을 지원하지 않습니다. 패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-20}

* **유사**
유사한 노드를 찾을 노드의 절대 경로

* **로컬**
하위 노드 또는 
`.` 현재 노드의 경우(선택 사항, 기본값은 &quot; 임) `.`&quot;)

### 태그 {#tag}

태그 제목 경로를 지정하여 하나 이상의 태그가 지정된 콘텐츠를 검색합니다.

패싯 추출을 지원합니다. 는 현재 태그 제목 경로를 사용하여 각 고유 태그에 대한 버킷을 제공합니다.

#### 속성 {#properties-21}

* **태그**

   찾을 태그 제목 경로(예: &quot;자산 속성 : 방향/가로&quot;

* **N_value**

   사용 `1_value`, `2_value`, ... 여러 태그( 와 결합) 확인 `OR` 기본적으로 `AND` if 및=true)(5.6 이후)

* **속성**

   찾을 속성(또는 속성의 상대 경로)(기본값 &quot; `cq:tags`&quot;)

### tagid {#tagid}

태그 ID를 지정하여 하나 이상의 태그가 지정된 콘텐츠를 검색합니다.

패싯 추출을 지원합니다. 는 현재 태그 ID를 사용하여 각 고유 태그에 대한 버킷을 제공합니다.

#### 속성 {#properties-22}

* **tagid**

   찾을 태그 id(예: &quot; &quot;) `properties:orientation/landscape`&quot;

* **N_value**

   사용 `1_value`, `2_value`, .. 여러 태그 id(와 결합됨)를 확인합니다. `OR` 기본적으로 `AND` if 및=true)(5.6 이후)

* **속성**

   찾을 속성(또는 속성의 상대 경로)(기본값 &quot; `cq:tags`&quot;)

### tagsearch {#tagsearch}

키워드를 지정하여 하나 이상의 태그가 지정된 콘텐츠를 검색합니다. 이렇게 하면 우선 제목에 이러한 키워드가 포함된 태그를 검색한 다음, 이러한 태그가 지정된 항목만 결과로 제한합니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#Properties-1}

* **tagsearch**

   태그 제목에서 검색할 키워드

* **속성**

   찾을 속성(또는 속성의 상대 경로)(기본값 &quot; `cq:tags`&quot;)

* **lang**

   현지화된 특정 태그 제목에서만 검색할 수 있습니다(예: &quot; `de`&quot;)

* **모두**

   (bool) 전체 태그 전체 텍스트, 즉 모든 제목, 설명 등을 검색합니다. (&quot;l&quot;보다 우선함) `ang`&quot;)

### 유형 {#type}

결과를 특정 JCR 노드 유형, 기본 노드 유형 또는 mixin 유형으로 제한합니다. 이렇게 하면 해당 노드 유형의 하위 유형도 찾을 수 있습니다. 저장소 검색 색인은 효율적인 실행을 위해 노드 유형을 포함해야 합니다.

패싯 추출을 지원합니다. 에서는 결과에서 각 고유 유형에 대한 버킷을 제공합니다.

#### 속성 {#Properties-2}

* **유형**

   검색할 노드 유형 또는 mixin 이름(예: `cq:Page`
