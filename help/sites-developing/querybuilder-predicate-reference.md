---
title: Query Builder 설명 참조
seo-title: Query Builder 설명 참조
description: 쿼리 빌더 API에 대한 전체 설명 참조입니다.
seo-description: 쿼리 빌더 API에 대한 전체 설명 참조입니다.
uuid: af0e269e-7d52-4032-b22e-801c7b5dccfa
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 94a05894-743a-4ace-a292-bfee90ba9068
translation-type: tm+mt
source-git-commit: 7a96ff5cdd187291efe108d1171782bcbecfaeb0
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 3%

---


# Query Builder 설명 참조{#query-builder-predicate-reference}

## 일반 {#general}

* [루트](#root)
* [그룹](#group)
* [orderby](#orderby)

## {#predicates} 예측

* [boolproperty](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparison](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [daterange](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [제외 경로](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [전체 텍스트](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [언어](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [mainasset](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [memberOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [노네임](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [만료되지 않음](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [경로](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [속성](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [rangeproperty](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [relativedaterange](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [유사](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [tag](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [tagid](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [유형](/help/sites-developing/querybuilder-predicate-reference.md#type)

### boolproperty {#boolproperty}

JCR 부울 속성에 일치합니다. &quot; `true`&quot; 및 &quot; `false`&quot; 값만 허용합니다. &quot; `false`&quot;의 경우 속성 값이 &quot; `false`&quot;이거나 속성이 전혀 없는 경우 일치합니다. 활성화되었을 때만 설정되는 부울 플래그를 확인하는 데 유용합니다.

상속된 &quot; `operation`&quot; 매개 변수는 의미가 없습니다.

패싯 추출을 지원합니다. 각 `true` 또는 `false` 값에 대한 버킷을 제공하지만 기존 속성에 대해서만 버킷을 제공합니다.

#### 속성 {#properties}

* **속성**
의 부울 속성상대 경로(예: 
`myFeatureEnabled` 또는 `jcr:content/myFeatureEnabled`

* **값**
을 사용하여 &quot; 
`true`&quot; 또는 &quot; `false`&quot;

### contentfragment {#contentfragment}

결과를 컨텐츠 조각으로 제한합니다.

필터링을 지원하지 않습니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-1}

* **컨텐츠**
조각컨텐츠 조각을 확인하는 데 모든 값과 함께 사용할 수 있습니다.

### dateComparison {#datecomparison}

두 JCR DATE 속성을 서로 비교합니다. 동등한지, 불평등한지, 크거나 같은지 테스트할 수 있습니다.

필터링 전용 조건자이며 검색 색인을 활용할 수 없습니다.

#### 속성 {#properties-2}

* **property1**

   첫 번째 날짜 속성에 대한 경로

* **property2**

   두 번째 날짜 속성에 대한 경로

* **작업**

   &quot;`equals`&quot;은 완전 일치의 경우, &quot;a1/>&quot;, &quot;property1보다 큰 속성은 &quot;`greater`&quot;, property1은 property2보다 크거나 같은 경우 &quot;`>=`&quot;. `!=` 기본값은 &quot;`equals`&quot;입니다.

### daterange {#daterange}

날짜/시간 간격과 JCR 날짜 속성을 일치시킵니다. ISO8601을 사용합니다.
날짜 및 시간에 대한 형식( `YYYY-MM-DDTHH:mm:ss.SSSZ`)을 지정하고 `YYYY-MM-DD`와 같은 부분 표현을 허용합니다. 또는 1970년 이후 UTC 시간대(unix 시간 형식)에서 타임스탬프를 밀리초 단위로 제공할 수 있습니다.

두 개의 타임스탬프(지정된 날짜보다 최신 또는 이전 버전) 사이의 항목을 찾을 수 있으며, 포함 및 열린 간격 간을 선택할 수도 있습니다.

패싯 추출을 지원합니다. &quot;오늘&quot;, &quot;이번 주&quot;, &quot;이번 달&quot;, &quot;지난 3개월&quot;, &quot;올해&quot;, &quot;작년&quot; 및 &quot;작년보다 이전&quot; 버킷을 제공합니다.

필터링을 지원하지 않습니다.

#### 속성 {#properties-3}

* **속성**

   `DATE` 속성에 대한 상대 경로(예: `jcr:lastModified`)

* **lowerBound**

   check 속성을 확인할 날짜가 낮은 날짜(예: `2014-10-01`)

* **lowerOperation**

   &quot; `>`&quot;(최신) 또는 &quot; `>=`&quot;(최신 또는 최신))는 `lowerBound`에 적용됩니다. 기본값은 &quot; `>`&quot;입니다.

* **upperBound**

   check 속성 값(예: `2014-10-01T12:15:00`)

* **upperOperation**

   &quot; `<`&quot;(이전 버전) 또는 &quot; `<=`&quot;(위치 또는 이전 버전)이 `upperBound`에 적용됩니다. 기본값은 &quot; `<`&quot;입니다.

* **timeZone**

   ISO-8601 날짜 문자열로 제공되지 않을 때 사용할 표준 시간대 ID입니다. 기본값은 시스템의 기본 표준 시간대입니다.

### excdepaths {#excludepaths}

경로가 정규 표현식과 일치하는 결과에서 노드를 제외합니다.

필터링 전용 조건자이며 검색 색인을 활용할 수 없습니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-4}

* **제외 경로**

   결과 경로에 대해 일치된 정규 표현식으로, 결과에서 일치하는 식을 제외합니다.

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

중첩된 조건을 만들 수 있습니다. 그룹에는 중첩된 그룹이 포함될 수 있습니다. Querybuilder 쿼리의 모든 항목은 `p.or` 및 `p.not` 매개 변수를 가질 수 있는 루트 그룹에 암시적으로 포함됩니다.

값에 대해 두 속성 중 하나를 일치시키는 예:

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

개념적으로는 `(1_property` 또는 `2_property)`입니다.

중첩 그룹의 예:

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

이 항목은 `/content/geometrixx/en`의 페이지 내에서 또는 `/content/dam/geometrixx`의 자산에서 &quot;**관리**&quot; 용어를 검색합니다.

개념적으로는 `fulltext AND ( (path AND type) OR (path AND type) )`입니다. 이러한 OR 연결에는 성능에 대한 좋은 색인이 필요합니다.

#### 속성 {#properties-6}

* **p.or**

   &quot; `true`&quot;로 설정된 경우 그룹의 하나의 조건자만 일치해야 합니다. 기본값은 &quot; `false`&quot;입니다. 즉, 모든 항목이 일치해야 합니다.

* **p.not**

   &quot; `true`&quot;로 설정하면 그룹이 무효화됩니다(기본값은 &quot; `false`&quot;).

* **&lt;predicate>**

   중첩된 설명 추가

* **N_&lt;predicate>**

   `1_property, 2_property, ...`과 같이 동시에 여러 개의 중첩 예측 추가

### hasPermission {#haspermission}

현재 세션에 지정된 [JCR 권한이 있는 항목으로 결과를 제한합니다.](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

필터링 전용 조건자이며 검색 색인을 활용할 수 없습니다. 패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-7}

* **hasPermission**

   현재 사용자 세션이 해당 노드에 대해 모두 가져야 하는 쉼표로 구분된 JCR 권한예: `jcr:write`, `jcr:modifyAccessControl`

### 언어 {#language}

특정 언어로 CQ 페이지를 찾습니다. 여기서는 페이지 언어 속성과 최상위 사이트 구조의 언어 또는 로케일을 포함하는 페이지 경로를 모두 봅니다.

필터링 전용 조건자이며 검색 색인을 활용할 수 없습니다.

패싯 추출을 지원합니다. 각 고유 언어 코드에 대한 버킷을 제공합니다.

#### 속성 {#properties-8}

* **언어**

   ISO 언어 코드(예: &quot; `de`&quot;)

### mainasset {#mainasset}

노드가 하위 자산이 아닌 DAM 기본 자산인지 확인합니다. 이것은 기본적으로 &quot;하위 자산&quot; 노드 내에 없는 모든 노드입니다. 이것은 `dam:Asset` 노드 유형을 확인하지 않습니다. 이 조건자를 사용하려면 &quot; `mainasset=true`&quot; 또는 &quot; `mainasset=false`&quot;로 설정하기만 하면 추가 속성이 없습니다.

필터링 전용 조건자이며 검색 색인을 활용할 수 없습니다.

패싯 추출을 지원합니다. 기본 및 하위 자산에 대해 2개의 버킷을 제공합니다.

#### 속성 {#properties-9}

* **mainasset**

   boolean, 기본 자산의 경우 &quot; `true`&quot;, 하위 자산의 경우 &quot; `false`&quot;

### memberOf {#memberof}

특정 [sling 리소스 컬렉션](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html)의 멤버인 항목을 찾습니다.

필터링 전용 조건자이며 검색 색인을 활용할 수 없습니다. 패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-10}

* **memberOf**

   Sling 리소스 컬렉션 경로

### nodename {#nodename}

JCR 노드 이름에 일치합니다.

패싯 추출을 지원합니다. 각 고유 노드 이름(파일 이름)에 대한 버킷을 제공합니다.

#### 속성 {#properties-11}

* **노네임**

   와일드카드를 허용하는 노드 이름 패턴:`*` = 임의 또는 없음, `?` = 모든 문자, `[abc]` = 대괄호 안의 문자만

### 만료되지 않음 {#notexpired}

JCR DATE 속성이 현재 서버 시간보다 크거나 같은지 확인하여 항목을 일치시킵니다. 날짜 속성과 같이 &quot; `expiresAt`&quot;을 확인하는 데 사용할 수 있으며 아직 만료되지 않았거나( `notexpired=true`) 이미 만료된 것( `notexpired=false`)만 제한할 수 있습니다.

필터링을 지원하지 않습니다.

날짜 범위 조건자와 동일한 방식으로 패싯 추출을 지원합니다.

#### 속성 {#properties-12}

* **만료되지 않음**

   부울, 아직 만료되지 않은 경우 &quot; `true`&quot;(미래의 날짜 또는 동일한 날짜), 만료된 경우 &quot; `false`&quot;(이전 날짜)(필수)

* **속성**

   확인할 `DATE` 속성에 대한 상대 경로(필수)

### orderby {#orderby}

결과를 정렬할 수 있습니다. 여러 속성으로 순서를 지정해야 하는 경우 이 조건자를 번호 접두어(예: `1_orderby=first`, `2_oderby=second`)를 사용하여 여러 번 추가해야 합니다.

#### 속성 {#properties-13}

* **orderby**

   JCR 속성 이름(예: `@jcr:lastModified` 또는 `@jcr:content/jcr:title`)이나 쿼리의 다른 조건자(예: `2_property`)를 사용하여 정렬할 수 있습니다.

* **정렬**

   정렬 방향입니다. 내림차순은 &quot; `desc`&quot;, 오름차순은 &quot; `asc`&quot;(기본값)

* **케이스**

   &quot;a0/>&quot;로 설정하면 정렬 대소문자를 구분하지 않습니다. 즉, &quot;a&quot;가 &quot;B&quot; 앞에 옵니다.비어 있거나 제외되는 경우, 정렬은 대소문자를 구분합니다. 즉, &quot;B&quot;가 &quot;a&quot; 앞에 옵니다.`ignore`

### 경로 {#path}

지정된 경로 내에서 검색합니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-14}

* **경로**

   경로 패턴;정확히 일치에 따라 전체 하위 트리 중 하나가 일치합니다(예: xpath에 `//*`을 추가하지만 기본 경로가 포함되지 않음)(exact=false, 기본값) 또는 와일드카드( `*`)를 포함할 수 있는 정확한 경로 일치만 포함해야 합니다.자가 설정되면 기본 노드를 포함한 전체 하위 트리가 검색됩니다

* **exact**

   `exact`이 true/on이면 정확한 경로가 일치해야 하지만 &quot; `*`&quot; 이름과 일치하지만 &quot; `/`&quot;;이(가) 아닌 간단한 와일드카드( )를 포함할 수 있습니다.false(기본값)이면 모든 하위 항목이 포함됩니다(선택 사항).

* **평면**

   직접 하위만 검색합니다(예: xpath에 &quot; `/*`&quot;을 추가하는 것과 같이)(&#39; `exact`&#39;이(가) true가 아닌 경우에만 사용됨, 선택 사항).

* **self**

   하위 트리를 검색하지만 경로로 지정된 기본 노드를 포함합니다(와일드카드 없음).

### 속성 {#property}

JCR 속성 및 해당 값에 일치합니다.

패싯 추출을 지원합니다. 결과의 각 고유 속성 값에 대한 버킷을 제공합니다.

#### 속성 {#properties-15}

* **속성**

   속성에 대한 상대 경로(예: `jcr:title`)

* **정렬 단추**

   값을 참조하십시오.는 JCR 속성 유형을 문자열 변환으로 따릅니다.

* **N_value**

   `1_value`, `2_value`, ...을 사용하여 여러 값을 확인합니다(기본적으로 `OR`와 결합하고 `AND` if 및=true와 조합함)(5.3 이후).

* **및**

   여러 값( `N_value`)을 AND와 결합하기 위해 true로 설정(5.3 이후)

* **작업**

   &quot;`equals`&quot;(완전 일치)(기본값)의 경우, 불균등 비교의 경우 &quot;`unequals`&quot;, `jcr:like` xpath 함수(선택 사항)의 경우 &quot;`like`&quot;, 일치하지 않는 경우 &quot; `not`&quot;(예: xpath의 &quot;`not(@prop)`&quot;, 값 매개 변수가 무시됩니다.) 또는 존재 확인을 위한 &quot;`exists`&quot;(값이 true일 수 있습니다. 속성이 존재해야 함, 기본값 또는 false - &quot;`not`&quot;과 동일함)

* **깊이**

   속성/상대 경로가 존재할 수 있는 와일드카드 레벨 수(예: `property=size depth=2`는 노드/크기, node/&amp;ast;/size 및 node/&amp;ast;/&amp;ast;/size)

### rangeproperty {#rangeproperty}

JCR 속성을 간격과 일치시킵니다. 이것은 `LONG`, `DOUBLE` 및 `DECIMAL` 등의 선형 유형의 속성에 적용됩니다. `DATE`의 경우 최적화된 날짜 형식 입력이 있는 날짜 범위 조건자를 참조하십시오.

하한과 상선을 정의하거나 둘 중 하나만 정의할 수 있습니다. 작업(예: &quot;보다 작음&quot; 또는 &quot;더 적거나 같음&quot;)을 각각 하한 및 상한 단위로 지정할 수도 있습니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-16}

* **속성**

   속성에 대한 상대 경로

* **lowerBound**

   check 속성 하한값

* **lowerOperation**

   &quot; `>`&quot;(기본값) 또는 &quot; `>=`&quot;이 `lowerValue`에 적용됩니다.

* **upperBound**

   의 check 속성

* **upperOperation**

   &quot; `<`&quot;(기본값) 또는 &quot; `<=`&quot;이 `lowerValue`에 적용됩니다.

* **decimal**

   &quot;선택한 속성이 Decimal 유형인 경우 `true`&quot;

### relativedaterange {#relativedaterange}

현재 서버 시간을 기준으로 시간 오프셋을 사용하여 날짜/시간 간격에 대해 `JCR DATE` 속성을 일치시킵니다. 밀리초 값 또는 bugzilla 구문 `1s 2m 3h 4d 5w 6M 7y`(1초, 2분, 3시간, 4일, 5주, 6개월, 7년)을 사용하여 `lowerBound` 및 `upperBound`을 지정할 수 있습니다. 현재 시간 이전의 음수 오프셋을 나타내는 접두어는 &quot; `-`&quot;입니다. `lowerBound` 또는 `upperBound`만 지정하는 경우 다른 하나는 기본적으로 0으로 설정되며, 이것은 현재 시간을 의미합니다.

예:

* `upperBound=1h` (및 no  `lowerBound`)는 다음 시간에 원하는 항목을 선택합니다.
* `lowerBound=-1d` (및 no  `upperBound`)는 지난 24시간 동안 아무 것도 선택하지 않습니다.
* `lowerBound=-6M` 6개월에서 3개월까지  `upperBound=-3M` 어떤 것도
* `lowerBound=-1500` 이전 1500밀리초에서 앞으로 5500밀리초까지의 모든 것을  `upperBound=5500` 선택합니다.
* `lowerBound=1d` 내일 모레 어떤 것도 선택해서  `upperBound=2d` 

윤년은 고려하지 않고 모든 달은 30일입니다.

필터링을 지원하지 않습니다.

날짜 범위 조건자와 동일한 방식으로 패싯 추출을 지원합니다.

#### 속성 {#properties-17}

* **upperBound**

   현재 서버 시간을 기준으로 밀리초 단위 또는 `1s 2m 3h 4d 5w 6M 7y`(1초, 2분, 3시간, 4일, 5주, 6개월, 7년)의 상한 날짜는 음수 오프셋에 대해 &quot;-&quot;를 사용합니다.

* **lowerBound**

   현재 서버 시간에 대한 하한 날짜(밀리초 단위) 또는 `1s 2m 3h 4d 5w 6M 7y`(1초, 2분, 3시간, 4일, 5주, 6개월, 7년)(음수 오프셋에 대해 &quot;-&quot;를 사용합니다.

### 루트 {#root}

루트 설명 그룹. 그룹의 모든 기능을 지원하고 전역 쿼리 매개 변수를 설정할 수 있습니다.

&quot;root&quot; 이름은 쿼리에서 사용되지 않으며 암시적입니다.

#### 속성 {#properties-18}

* **p.offset**

   결과 페이지의 시작을 나타내는 숫자(즉, 건너뛸 항목 수)

* **p.limit**

   페이지 크기를 나타내는 숫자

* **p.guessTotal**

   권장:비용이 많이 들 수 있는 전체 결과 합계를 계산하지 마십시오.최대 계산 총계를 나타내는 숫자(예: 1000, 러프 크기에 대한 사용자 의견을 충분히 제공하고 더 작은 결과를 위해 정확한 숫자를 제공하는 숫자) 또는 필요한 최소 `p.offset` + `p.limit`까지 계산하기 위한 &quot; `true`&quot;

* **p.introduction**

   &quot; `true`&quot;로 설정된 경우 결과에 발췌한 전체 텍스트를 포함하십시오.

* **p.hits**

   (JSON 서블릿에만 해당) 이러한 표준 히트(ResultHitWriter 서비스를 통해 확장 가능)를 사용하여 히트가 JSON으로 작성되는 방식을 선택합니다.

   * **단순한**:

      `path`, `title`, `lastmodified`, `excerpt`(설정된 경우)와 같은 최소 항목

   * **전체**:

      노드의 sling JSON 렌더링(히트 경로를 나타내는 `jcr:path` 포함:기본적으로 노드의 직접 속성만 나열하고 `p.nodedepth=N`(전체 무한 하위 트리를 의미함)이 0인 더 깊은 트리를 포함합니다.지정된 결과 항목에 현재 세션의 JCR 권한을 포함하려면 `p.acls=true`을(를) 추가합니다(매핑:`create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)

   * **선택적**:

      상대 경로의 &quot;+&quot;를 사용(URL에서 사용) 목록인 `p.properties`에 지정된 속성만;상대 경로에 깊이가 1보다 크면 하위 오브젝트로 표현됩니다.특수 jcr:path 속성은 히트의 경로를 포함합니다

### savedquery {#savedquery}

하위 그룹 조건자로 현재 쿼리에 지속되는 쿼리 빌더 쿼리의 모든 설명을 포함합니다.

추가 쿼리는 실행하지 않고 현재 쿼리를 확장합니다.

쿼리는 `QueryBuilder#storeQuery()`을 사용하여 프로그래밍 방식으로 유지할 수 있습니다. 형식은 여러 줄 String 속성 또는 쿼리를 Java 속성 형식의 텍스트 파일로 포함하는 `nt:file` 노드일 수 있습니다.

저장된 쿼리의 예측자에 대한 패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-19}

* **savedquery**

   저장된 쿼리 경로(문자열 속성 또는 `nt:file` 노드)

### 유사 {#similar}

JCR XPath의 `rep:similar()`을(를) 사용한 유사성 검색

필터링을 지원하지 않습니다. 패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-20}

* **유사한 노드를 찾을 노드**
와 유사한 절대 경로

* **하위 노드 또는**
하위 노드의 상대 경로 
`.` 현재 노드의 경우(선택 사항, 기본값은 &quot;  `.`&quot;)

### 태그 {#tag}

태그 제목 경로를 지정하여 하나 이상의 태그가 지정된 컨텐츠를 검색합니다.

패싯 추출을 지원합니다. 현재 태그 제목 경로를 사용하여 각 고유 태그에 대한 버킷을 제공합니다.

#### 속성 {#properties-21}

* **tag**

   찾을 태그 제목 경로(예: &quot;자산 속성:방향/가로&quot;

* **N_value**

   `1_value`, `2_value`, ...을 사용하여 여러 태그를 확인합니다(기본적으로 `OR`와 결합되고 `AND` if 및=true와 결합됨)(5.6 이후).

* **속성**

   찾을 속성(또는 속성의 상대 경로)(기본값 &quot; `cq:tags`&quot;)

### tagid {#tagid}

태그 ID를 지정하여 하나 이상의 태그가 지정된 컨텐츠를 검색합니다.

패싯 추출을 지원합니다. 현재 태그 ID를 사용하여 각 고유 태그에 대한 버킷을 제공합니다.

#### 속성 {#properties-22}

* **tagid**

   찾을 태그 id(예: &quot; `properties:orientation/landscape`&quot;)

* **N_value**

   `1_value`, `2_value`, ...을 사용하여 여러 태그 id를 확인합니다(기본적으로 `OR`와 결합되고 `AND` if 및=true로 조합됨)(5.6 이후).

* **속성**

   찾을 속성(또는 속성의 상대 경로)(기본값 &quot; `cq:tags`&quot;)

### tagsearch {#tagsearch}

키워드를 지정하여 하나 이상의 태그가 지정된 컨텐츠를 검색합니다. 이렇게 하면 우선 제목에 이러한 키워드를 포함하는 태그를 검색한 다음, 이러한 태그가 지정된 항목만 결과를 제한할 수 있습니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#Properties-1}

* **tagsearch**

   태그 제목에서 검색할 키워드

* **속성**

   찾을 속성(또는 속성의 상대 경로)(기본값 &quot; `cq:tags`&quot;)

* **lang**

   특정 지역화된 태그 제목에서만 검색할 수 있습니다(예:&quot; `de`&quot;)

* **모두**

   (bool) 전체 태그 전체 텍스트, 즉 모든 제목, 설명 등을 검색합니다. (l `ang`&quot;보다 우선함)

### 유형 {#type}

결과를 특정 JCR 노드 유형(기본 노드 유형 또는 혼합 유형 모두)으로 제한합니다. 또한 해당 노드 유형의 하위 유형도 찾습니다. 저장소 검색 색인은 효율적인 실행을 위해 노드 유형을 포함해야 합니다.

패싯 추출을 지원합니다. 결과의 각 고유 유형에 대한 버킷을 제공합니다.

#### 속성 {#Properties-2}

* **유형**

   검색할 노드 유형 또는 믹싱 이름(예: `cq:Page`)