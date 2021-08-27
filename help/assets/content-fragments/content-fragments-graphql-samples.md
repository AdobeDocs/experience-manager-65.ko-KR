---
title: AEM에서 GraphQL을 사용하는 방법 학습 - 샘플 컨텐츠 및 쿼리
description: 샘플 컨텐츠 및 쿼리를 탐색하여 GraphQL과 AEM을 함께 사용하여 헤더없이 컨텐츠를 제공하는 방법을 알아봅니다.
feature: Content Fragments,GraphQL API
source-git-commit: 94145c6428f61e31f6784a3d6ea67aa8d81cedd6
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 6%

---

# AEM에서 GraphQL을 사용하는 방법 학습 - 샘플 컨텐츠 및 쿼리 {#learn-graphql-with-aem-sample-content-queries}

샘플 컨텐츠 및 쿼리를 탐색하여 GraphQL과 AEM을 함께 사용하여 헤더없이 컨텐츠를 제공하는 방법을 알아봅니다.

>[!NOTE]
>
>이 페이지는 다음과 함께 읽어야 합니다.
>
>* [컨텐츠 조각](/help/assets/content-fragments/content-fragments.md)
>* [콘텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md)
>* [컨텐츠 조각에 사용할 AEM GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)


GraphQL 쿼리 및 AEM 컨텐츠 조각으로 작동하는 방식을 시작하려면 몇 가지 실용적인 예를 볼 수 있습니다.

도움이 필요하면 다음을 참조하십시오.

* [샘플 컨텐츠 조각 구조](#content-fragment-structure-graphql)

* 및 일부 [샘플 GraphQL 쿼리](#graphql-sample-queries)은 샘플 컨텐츠 조각 구조(컨텐츠 조각 모델 및 관련 컨텐츠 조각)를 기반으로 합니다.


## GraphQL - 샘플 컨텐츠 조각 구조를 사용하는 샘플 쿼리 {#graphql-sample-queries-sample-content-fragment-structure}

샘플 결과와 함께 쿼리 만들기 그림에 대해서는 다음 샘플 쿼리를 참조하십시오.

>[!NOTE]
>
>인스턴스에 따라 AEM GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface)에 포함된 [Graph *i* QL 인터페이스에 직접 액세스하여 쿼리를 제출하고 테스트할 수 있습니다.
>
>예를 들어,`http://localhost:4502/content/graphiql.html`

>[!NOTE]
>
>샘플 쿼리는 GraphQL](#content-fragment-structure-graphql)에 사용할 [샘플 컨텐츠 조각 구조를 기반으로 합니다

### 샘플 쿼리 - 사용 가능한 모든 스키마 및 데이터 유형 {#sample-all-schemes-datatypes}

이렇게 하면 사용 가능한 모든 스키마에 대한 모든 `types`이 반환됩니다.

**샘플 쿼리**

```xml
{
  __schema {
    types {
      name
      description
    }
  }
}
```

**샘플 결과**

```xml
{
  "data": {
    "__schema": {
      "types": [
        {
          "name": "AdventureModel",
          "description": null
        },
        {
          "name": "AdventureModelArrayFilter",
          "description": null
        },
        {
          "name": "AdventureModelFilter",
          "description": null
        },
        {
          "name": "AdventureModelResult",
          "description": null
        },
        {
          "name": "AdventureModelResults",
          "description": null
        },
        {
          "name": "AllFragmentModels",
          "description": null
        },
        {
          "name": "ArchiveRef",
          "description": null
        },
        {
          "name": "ArrayMode",
          "description": null
        },
        {
          "name": "ArticleModel",
          "description": null
        },

...more results...

        {
          "name": "__EnumValue",
          "description": null
        },
        {
          "name": "__Field",
          "description": null
        },
        {
          "name": "__InputValue",
          "description": null
        },
        {
          "name": "__Schema",
          "description": "A GraphQL Introspection defines the capabilities of a GraphQL server. It exposes all available types and directives on the server, the entry points for query, mutation, and subscription operations."
        },
        {
          "name": "__Type",
          "description": null
        },
        {
          "name": "__TypeKind",
          "description": "An enum describing what kind of type a given __Type is"
        }
      ]
    }
  }
}
```

### 샘플 쿼리 - 모든 도시에 대한 모든 정보 {#sample-all-information-all-cities}

모든 도시에 대한 모든 정보를 검색하려면 매우 기본적인 쿼리를 사용할 수 있습니다.
**샘플 쿼리**

```xml
{
  cityList {
    items
  }
}
```

실행될 때 시스템이 모든 필드를 포함하도록 쿼리를 자동으로 확장합니다.

```xml
{
  cityList {
    items {
      _path
      name
      country
      population
    }
  }
}
```

**샘플 결과**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/basel",
          "name": "Basel",
          "country": "Switzerland",
          "population": 172258
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/bucharest",
          "name": "Bucharest",
          "country": "Romania",
          "population": 1821000
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-francisco",
          "name": "San Francisco",
          "country": "USA",
          "population": 883306
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-jose",
          "name": "San Jose",
          "country": "USA",
          "population": 1026350
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/stuttgart",
          "name": "Stuttgart",
          "country": "Germany",
          "population": 634830
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/zurich",
          "name": "Zurich",
          "country": "Switzerland",
          "population": 415367
        }
      ]
    }
  }
}
```

### 샘플 쿼리 - 모든 도시의 이름 {#sample-names-all-cities}

`city`스키마에 있는 모든 항목의 `name`을 반환하기 위한 간단한 쿼리입니다.

**샘플 쿼리**

```xml
query {
  cityList {
    items {
      name
    }
  }
}
```

**샘플 결과**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Basel"
        },
        {
          "name": "Berlin"
        },
        {
          "name": "Bucharest"
        },
        {
          "name": "San Francisco"
        },
        {
          "name": "San Jose"
        },
        {
          "name": "Stuttgart"
        },
        {
          "name": "Zurich"
        }
      ]
    }
  }
}
```

### 샘플 쿼리 - 단일 특정 도시 조각 {#sample-single-specific-city-fragment}

저장소의 특정 위치에 단일 조각 항목의 세부 사항을 반환하기 위한 쿼리입니다.

**샘플 쿼리**

```xml
{
  cityByPath (_path: "/content/dam/sample-content-fragments/cities/berlin") {
    item {
      _path
      name
      country
      population
     categories
    }
  }
}
```

**샘플 결과**

```xml
{
  "data": {
    "cityByPath": {
      "item": {
        "_path": "/content/dam/sample-content-fragments/cities/berlin",
        "name": "Berlin",
        "country": "Germany",
        "population": 3669491,
        "categories": [
          "city:capital",
          "city:emea"
        ]
      }
    }
  }
}
```

### 샘플 쿼리 - 명명된 변형을 가진 모든 도시 {#sample-cities-named-variation}

`city` 베를린에 대해 &quot;Berlin Center&quot;(`berlin_centre`)라는 새 변형을 만드는 경우 쿼리를 사용하여 변형의 세부 정보를 반환할 수 있습니다.

**샘플 쿼리**

```xml
{
  cityList (variation: "berlin_center") {
    items {
      _path
      name
      country
      population
      categories
    }
  }
}
```

**샘플 결과**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491,
          "categories": [
            "city:capital",
            "city:emea"
          ]
        }
      ]
    }
  }
}
```

### 샘플 질의 - 회사 CEO 및 직원의 전체 상세내역 {#sample-full-details-company-ceos-employees}

중첩된 조각의 구조를 사용하여 이 쿼리는 회사 CEO와 모든 해당 직원의 전체 세부 정보를 반환합니다.

**샘플 쿼리**

```xml
query {
  companyList {
    items {
      name
      ceo {
        _path
        name
        firstName
        awards {
        id
          title
        }
      }
      employees {
       name
        firstName
       awards {
         id
          title
        }
      }
    }
  }
}
```

**샘플 결과**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Apple Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Marsh",
              "firstName": "Duke",
              "awards": []
            },
            {
              "name": "Caulfield",
              "firstName": "Max",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                }
              ]
            }
          ]
        },
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/adam-smith",
            "name": "Smith",
            "firstName": "Adam",
            "awards": []
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        },
        {
          "name": "NextStep Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe",
              "awards": []
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham",
              "awards": []
            }
          ]
        }
      ]
    }
  }
}
```

### 샘플 쿼리 - &quot;Job&quot; 또는 &quot;Smith&quot;라는 이름을 가진 모든 개인 {#sample-all-persons-jobs-smith}

이 옵션은 `Jobs` 또는 `Smith` 이름이 있는 모든 항목에 대해 모든 `persons`을 필터링합니다.

**샘플 쿼리**

```xml
query {
  personList(filter: {
    name: {
      _logOp: OR
      _expressions: [
        {
          value: "Jobs"
        },
        {
          value: "Smith"
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

**샘플 결과**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Jobs",
          "firstName": "Steve"
        }
      ]
    }
  }
}
```

### 샘플 쿼리 - &quot;Job&quot;이라는 이름이 없는 모든 개인 {#sample-all-persons-not-jobs}

이 옵션은 `Jobs` 또는 `Smith` 이름이 있는 모든 항목에 대해 모든 `persons`을 필터링합니다.

**샘플 쿼리**

```xml
query {
  personList(filter: {
    name: {
      _expressions: [
        {
          value: "Jobs"
          _operator: EQUALS_NOT
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

**샘플 결과**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Lincoln",
          "firstName": "Abraham"
        },
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Slade",
          "firstName": "Cutter"
        },
        {
          "name": "Marsh",
          "firstName": "Duke"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Croft",
          "firstName": "Lara"
        },
        {
          "name": "Caulfield",
          "firstName": "Max"
        }
      ]
    }
  }
}
```

### 샘플 쿼리 - `_path`이(가) 특정 접두사로 시작하는 모든 모험 {#sample-wknd-all-adventures-cycling-path-filter}

모든 `adventures` 여기서 `_path`은 특정 접두사(`/content/dam/wknd/en/adventures/cycling`)로 시작합니다.

**샘플 쿼리**

```xml
query {
  adventureList(
    filter: {
      _path: {
        _expressions: [
        {
          value: "/content/dam/wknd/en/adventures/cycling"
         _operator: STARTS_WITH
        }]
       }
    })
    {
    items {
      _path
    }
  }
}
```

**샘플 결과**

```xml
{
  "data": {
    "adventureList": {
      "items": [
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-southern-utah/cycling-southern-utah"
        },
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-tuscany/cycling-tuscany"
        }
      ]
    }
  }
}
```

### 샘플 쿼리 - 400000과 999999 사이의 모집단이 있는 독일 또는 스위스에 있는 모든 도시 {#sample-all-cities-d-ch-population}

여기서는 필드 조합이 필터링됩니다. `AND`(암시적)은 `population`범위를 선택하는 데 사용되고 `OR`(명시적)은 필요한 도시를 선택하는 데 사용됩니다.

**샘플 쿼리**

```xml
query {
  cityList(filter: {
    population: {
      _expressions: [
        {
          value: 400000
          _operator: GREATER_EQUAL
        }, {
          value: 1000000
          _operator: LOWER
        }
      ]
    },
    country: {
      _logOp: OR
      _expressions: [
        {
          value: "Germany"
        }, {
          value: "Switzerland"
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**샘플 결과**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Stuttgart",
          "population": 634830,
          "country": "Germany"
        },
        {
          "name": "Zurich",
          "population": 415367,
          "country": "Switzerland"
        }
      ]
    }
  }
}
```

### 샘플 쿼리 - 사례에 상관없이 이름에 SAN이 있는 모든 도시 {#sample-all-cities-san-ignore-case}

이 쿼리는 사례에 관계없이 이름에 `SAN`이 있는 모든 도시에 대해 상호 작용합니다.

**샘플 쿼리**

```xml
query {
  cityList(filter: {
    name: {
      _expressions: [
        {
          value: "SAN"
          _operator: CONTAINS
          _ignoreCase: true
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**샘플 결과**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA"
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA"
        }
      ]
    }
  }
}
```

### 샘플 쿼리 - 한 번 이상 발생해야 하는 항목이 있는 배열에 필터링 {#sample-array-item-occur-at-least-once}

이 쿼리 필터는 항목(`city:na`)이 한 번 이상 있어야 하는 배열의 필터입니다.

**샘플 쿼리**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          value: "city:na"
          _apply: AT_LEAST_ONCE
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**샘플 결과**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA",
          "categories": [
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### 샘플 쿼리 - 정확한 배열 값으로 필터링 {#sample-array-exact-value}

이 쿼리는 정확한 배열 값을 필터링합니다.

**샘플 쿼리**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          values: [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**샘플 결과**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### 중첩된 컨텐츠 조각에 대한 샘플 쿼리 - &quot;Smith&quot;라는 이름을 가진 직원이 하나 이상 있는 모든 회사입니다 {#sample-companies-employee-smith}

이 쿼리는 `name` &quot;Smith&quot;의 `person`에 대한 필터링을 보여 주고, 두 중첩 조각(`company` 및 `employee`에서 정보를 반환합니다.

**샘플 쿼리**

```xml
query {
  companyList(filter: {
    employees: {
      _match: {
        name: {
          _expressions: [
            {
              value: "Smith"
            }
          ]
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
      }
    }
  }
}
```

**샘플 결과**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "NextStep Inc.",
          "ceo": {
            "name": "Jobs",
            "firstName": "Steve"
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe"
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham"
            }
          ]
        }
      ]
    }
  }
}
```

### 중첩된 컨텐츠 조각에 대한 샘플 쿼리 - 모든 직원이 &quot;Gamestar&quot; 상을 수상한 모든 회사 {#sample-all-companies-employee-gamestar-award}

이 쿼리는 세 개의 중첩 조각( `company`, `employee` 및 `award`)에 대한 필터링을 보여줍니다.

**샘플 쿼리**

```xml
query {
  companyList(filter: {
    employees: {
      _apply: ALL
      _match: {
        awards: {
          _match: {
            id: {
              _expressions: [
                {
                  value: "GS"
                  _operator:EQUALS
                }
              ]
            }
          }
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
        awards {
          id
          title
        }
      }
    }
  }
}
```

**샘플 결과**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "name": "Smith",
            "firstName": "Adam"
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        }
      ]
    }
  }
}
```

### 메타데이터에 대한 샘플 쿼리 - GB라는 이름의 시상식에 대한 메타데이터 나열 {#sample-metadata-awards-gb}

이 쿼리는 세 개의 중첩 조각( `company`, `employee` 및 `award`)에 대한 필터링을 보여줍니다.

**샘플 쿼리**

```xml
query {
  awardList(filter: {
      id: {
        _expressions: [
          {
            value:"GB"
          }
        ]
    }
  }) {
    items {
      _metadata {
        stringMetadata {
          name,
          value
        }
      }
      id
      title
    }
  }
}
```

**샘플 결과**

```xml
{
  "data": {
    "awardList": {
      "items": [
        {
          "_metadata": {
            "stringMetadata": [
              {
                "name": "title",
                "value": "Gameblitz Award"
              },
              {
                "name": "description",
                "value": ""
              }
            ]
          },
          "id": "GB",
          "title": "Gameblitz"
        }
      ]
    }
  }
}
```

## WKND 프로젝트를 사용하는 샘플 쿼리 {#sample-queries-using-wknd-project}

이러한 샘플 쿼리는 WKND 프로젝트를 기반으로 합니다. 여기에는 다음 항목이 있습니다.

* 컨텐츠 조각 모델은 다음 위치에서 사용할 수 있습니다.
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* 컨텐츠 조각(및 기타 컨텐츠)은 다음 위치에서 사용할 수 있습니다.
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`

>[!NOTE]
>
>결과가 광범위할 수 있으므로 그들은 이곳에서 재생되지 않는다.

### 지정된 속성을 사용하여 특정 모델의 모든 컨텐츠 조각에 대한 샘플 쿼리 {#sample-wknd-all-model-properties}

이 샘플 쿼리 인터페이스:

* `article` 유형의 모든 컨텐츠 조각에 대해
* ( `path` 및 `author` 속성 사용)

**샘플 쿼리**

```xml
{
  articleList {
    items {
      _path
      author
    }
  }
}
```

### 메타데이터에 대한 샘플 쿼리 {#sample-wknd-metadata}

이 쿼리 상호 작용:

* `adventure` 유형의 모든 컨텐츠 조각에 대해
* 메타데이터

**샘플 쿼리**

```xml
{
  adventureList {
    items {
      _path,
      _metadata {
        stringMetadata {
          name,
          value
        }
        stringArrayMetadata {
          name,
          value
        }
        intMetadata {
          name,
          value
        }
        intArrayMetadata {
          name,
          value
        }
        floatMetadata {
          name,
          value
        }
        floatArrayMetadata {
          name,
          value
        }
        booleanMetadata {
          name,
          value
        }
        booleanArrayMetadata {
          name,
          value
        }
        calendarMetadata {
          name,
          value
        }
        calendarArrayMetadata {
          name,
          value
        }
      }
    }
  }
}
```

### 주어진 모델의 단일 컨텐츠 조각에 대한 샘플 쿼리 {#sample-wknd-single-content-fragment-of-given-model}

이 샘플 쿼리 인터페이스:

* 특정 경로에 있는 `article` 유형의 단일 컨텐츠 조각
   * 컨텐츠 내의 모든 형식은 다음과 같습니다.
      * HTML
      * Markdown
      * 일반 텍스트
      * JSON

**샘플 쿼리**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures") {
    item {
        _path
        author
        main {
          html
          markdown
          plaintext
          json
        }
    }
  }
}
```

### 모델의 컨텐츠 조각 모델에 대한 샘플 쿼리 {#sample-wknd-content-fragment-model-from-model}

이 샘플 쿼리 인터페이스:

* 단일 컨텐츠 조각용
   * 기본 컨텐츠 조각 모델의 세부 사항

**샘플 쿼리**

```xml
{
  adventureByPath(_path: "/content/dam/wknd/en/adventures/riverside-camping-australia/riverside-camping-australia") {
    item {
      _path
      adventureTitle
      _model {
        _path
        title
      }
    }
  }
}
```

### 중첩 컨텐츠 조각에 대한 샘플 쿼리 - 단일 모델 유형{#sample-wknd-nested-fragment-single-model}

이 쿼리 상호 작용:

* 특정 경로에 있는 `article` 유형의 단일 컨텐츠 조각
   * 내에서 참조된(중첩된) 조각의 경로 및 작성자입니다

>[!NOTE]
>
>필드 `referencearticle`에 데이터 유형이 `fragment-reference`입니다.

**샘플 쿼리**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/skitouring/skitouring") {
    item {
        _path
        author
        referencearticle {
          _path
          author
      }
    }
  }
}
```

### 중첩 컨텐츠 조각에 대한 샘플 쿼리 - 여러 모델 유형{#sample-wknd-nested-fragment-multiple-model}

이 쿼리 상호 작용:

* `bookmark` 유형의 여러 컨텐츠 조각에 대해
   * 를 사용하여 특정 모델 유형의 다른 조각에 대한 조각 참조 `article` 및 `adventure`

>[!NOTE]
>
>`fragments` 필드에 `fragment-reference` 데이터 유형이 있습니다. 모델 `Article`, `Adventure`이 선택되어 있습니다.

```xml
{
  bookmarkList {
    items {
        fragments {
          ... on ArticleModel {
            _path
            author
          }
          ... on AdventureModel {
            _path
            adventureTitle
          }
        }
     }
  }
}
```

### 컨텐츠 참조가 있는 특정 모델의 컨텐츠 조각에 대한 샘플 쿼리{#sample-wknd-fragment-specific-model-content-reference}

이 쿼리에는 두 가지 맛이 있습니다.

1. 모든 컨텐츠 참조를 반환하려면 다음을 수행하십시오.
1. `attachments` 유형의 특정 컨텐츠 참조를 반환하려면

다음 쿼리는 다음과 같이 질문합니다.

* `bookmark` 유형의 여러 컨텐츠 조각에 대해
   * 다른 조각에 대한 컨텐츠 참조 사용

#### 프리페치된 참조가 있는 여러 컨텐츠 조각에 대한 샘플 쿼리 {#sample-wknd-multiple-fragments-prefetched-references}

다음 쿼리는 `_references` 을 사용하여 모든 컨텐츠 참조를 반환합니다.

```xml
{
  bookmarkList {
     _references {
         ... on ImageRef {
          _path
          type
          height
        }
        ... on MultimediaRef {
          _path
          type
          size
        }
        ... on DocumentRef {
          _path
          type
          author
        }
        ... on ArchiveRef {
          _path
          type
          format
        }
    }
    items {
        _path
    }
  }
}
```

#### 첨부 파일이 있는 여러 컨텐츠 조각에 대한 샘플 쿼리 {#sample-wknd-multiple-fragments-attachments}

다음 쿼리는 `content-reference` 유형의 모든 `attachments` - 특정 필드(하위 그룹)를 반환합니다.

>[!NOTE]
>
>필드 `attachments`에 데이터 형식 `content-reference`이 있으며, 여러 양식이 선택되어 있습니다.

```xml
{
  bookmarkList {
    items {
      attachments {
        ... on PageRef {
          _path
          type
        }
        ... on ImageRef {
          _path
          width
        }
        ... on MultimediaRef {
          _path
          size
        }
        ... on DocumentRef {
          _path
          author
        }
        ... on ArchiveRef {
          _path
          format
        }
      }
    }
  }
}
```

### RTE 인라인 참조가 있는 단일 컨텐츠 조각에 대한 샘플 쿼리 {#sample-wknd-single-fragment-rte-inline-reference}

이 쿼리 상호 작용:

* 특정 경로에 있는 `bookmark` 유형의 단일 컨텐츠 조각
   * 내에서 RTE 인라인 참조

>[!NOTE]
>
>RTE 인라인 참조는 `_references`에서 하이드레이션됩니다.

**샘플 쿼리**

```xml
{
  bookmarkByPath(_path: "/content/dam/wknd/en/bookmarks/skitouring") {
    item {
      _path
      description {
        json
      }
    }
    _references {
      ... on ArticleModel {
        _path
      }
      ... on AdventureModel {
        _path
      }
      ... on ImageRef {
        _path
      }
      ... on MultimediaRef {
        _path
      }
      ... on DocumentRef {
        _path
      }
      ... on ArchiveRef {
        _path
      }
    }
  }
}
```

### 주어진 모델의 단일 컨텐츠 조각 변형에 대한 샘플 쿼리 {#sample-wknd-single-fragment-given-model}

이 쿼리 상호 작용:

* 특정 경로에 있는 `article` 유형의 단일 컨텐츠 조각
   * 그 내에서 변형과 관련된 데이터는 다음과 같습니다. `variation1`

**샘플 쿼리**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures", variation: "variation1") {
    item {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### 지정된 모델의 여러 컨텐츠 조각의 명명된 변형에 대한 샘플 쿼리 {#sample-wknd-variation-multiple-fragment-given-model}

이 쿼리 상호 작용:

* 특정 변형이 있는 `article` 유형의 컨텐츠 조각에 대해 다음을 수행합니다. `variation1`

**샘플 쿼리**

```xml
{
  articleList (variation: "variation1") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### 지정된 로케일의 여러 컨텐츠 조각에 대한 샘플 쿼리 {#sample-wknd-multiple-fragments-given-locale}

이 쿼리 상호 작용:

* `fr` 로케일 내의 `article` 유형의 컨텐츠 조각에 대해 설명합니다.

**샘플 쿼리**

```xml
{ 
  articleList (_locale: "fr") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

## 샘플 컨텐츠 조각 구조(GraphQL에서 사용됨) {#content-fragment-structure-graphql}

샘플 쿼리는 을 사용하는 다음 구조를 기반으로 합니다.

* 하나 이상의 [샘플 컨텐츠 조각 모델](#sample-content-fragment-models-schemas) - GraphQL 스키마 기준을 형성합니다

* [위의 ](#sample-content-fragments) 모델을 기반으로 하는 샘플 컨텐츠 조각

### 샘플 컨텐츠 조각 모델(스키마) {#sample-content-fragment-models-schemas}

샘플 쿼리는 다음 컨텐츠 모델 및 상호 관계(참조 ->)를 사용합니다.

* [회사](#model-company)
 ->  [개인](#model-person)
     ->  [포상](#model-award)

* [도시](#model-city)

#### 회사 {#model-company}

회사를 정의하는 기본 필드는 다음과 같습니다.

| 필드 이름 | 데이터 유형 | 참조 |
|--- |--- |--- |
| 회사 이름 | 한 줄 텍스트 |  |
| CEO | 조각 참조(단일) | [개인](#model-person) |
| 직원 | 조각 참조(multifield) | [개인](#model-person) |

#### 개인 {#model-person}

개인을 정의하는 필드이며 사원이 될 수도 있습니다.

| 필드 이름 | 데이터 유형 | 참조 |
|--- |--- |--- |
| 이름 | 한 줄 텍스트 |  |
| 이름 | 한 줄 텍스트 |  |
| 수상 | 조각 참조(multifield) | [수상](#model-award) |

#### 수상 {#model-award}

포상을 정의하는 필드는 다음과 같습니다.

| 필드 이름 | 데이터 유형 | 참조 |
|--- |--- |--- |
| 바로 가기/ID | 한 줄 텍스트 |  |
| 제목 | 한 줄 텍스트 |  |

#### 도시 {#model-city}

도시를 정의하는 필드는 다음과 같습니다.

| 필드 이름 | 데이터 유형 | 참조 |
|--- |--- |--- |
| 이름 | 한 줄 텍스트 |  |
| 국가 | 한 줄 텍스트 |  |
| 모집단 | 번호 |  |
| 카테고리 | 태그 |  |

### 샘플 컨텐츠 조각 {#sample-content-fragments}

다음 조각은 해당 모델에 사용됩니다.

#### 회사 {#fragment-company}

| 회사 이름 | CEO | 직원 |
|--- |--- |--- |
| Apple | 스티브 잡스 | 듀크 마쉬<br>Max Caulfield |
|  리틀 포니 | 아담 스미스 | 라라 크로프트<br>커터 슬래드 |
| NextStep Inc. | 스티브 잡스 | 조 스미스<br>아베 링컨 |

#### 개인 {#fragment-person}

| 이름 | 이름 | 수상 |
|--- |--- |--- |
| 링컨 |  아베 |  |
| 스미스 | Adam |   |
| 슬래드 |  커터 |  Gamerblicz<br>Gamestar |
| 마시 |  듀크 |   |   |
|  스미스 |  조 |   |
| 크로프트 |  라라 | 가메스타르 |
| 콜필드 |  최대 |  게임블리츠 |
|  작업 |  스티브 |   |

#### 수상 {#fragment-award}

| 바로 가기/ID | 제목 |
|--- |--- |
| GB | 게임블리츠 |
|  GS | 가메스타르 |
|  OSC | 오스카 |

#### 도시 {#fragment-city}

| 이름 | 국가 | 모집단 | 카테고리 |
|--- |--- |--- |--- |
| Basel | 스위스 | 172258 | city:emea |
| 베를린 | 독일 | 3669491 | city:capital<br>city:emea |
| 부카레스트 | 루마니아 | 1821000 |  city:capital<br>city:emea |
| San Francisco |  미국 |  883306 |  city:beach<br>city:na |
| 산 호세 |  미국 |  102635 |  city:na |
| 슈투트가르트 |  독일 |  634830 |  city:emea |
|  취리히 |  스위스 |  415367 |  city:capital<br>city:emea |
