---
title: AEM을 통해 GraphQL을 사용하는 방법 알아보기 - 샘플 콘텐츠 및 쿼리
description: AEM으로 GraphQL을 사용하여 샘플 콘텐츠 및 쿼리 탐색을 통해 콘텐츠를 Headless 방식으로 제공하는 방법을 배웁니다.
feature: Content Fragments,GraphQL API
exl-id: 91c5f61c-9c15-4d72-9b9b-0c23f31e7cdc
source-git-commit: bb5d39277db10fd8d3b436c8d1f40d9d2010adee
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 93%

---

# AEM을 통해 GraphQL을 사용하는 방법 알아보기 - 샘플 콘텐츠 및 쿼리 {#learn-graphql-with-aem-sample-content-queries}

AEM으로 GraphQL을 사용하여 샘플 콘텐츠 및 쿼리 탐색을 통해 콘텐츠를 Headless 방식으로 제공하는 방법을 배웁니다.

>[!NOTE]
>
>이 페이지는 다음과 함께 읽어야 합니다.
>
>* [콘텐츠 조각](/help/assets/content-fragments/content-fragments.md)
>* [콘텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md)
>* [콘텐츠 조각과 함께 사용하기 위한 AEM GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)


GraphQL 쿼리를 시작하고 이들 쿼리가 AEM 콘텐츠 조각과 함께 작동하는 방법을 알아보려면 몇 가지 실제 사례를 살펴보는 것이 도움이 됩니다.

도움이 필요하면 다음을 참조하십시오.

* [샘플 콘텐츠 조각 구조](#content-fragment-structure-graphql)

* 일부 [샘플 GraphQL 쿼리](#graphql-sample-queries), 샘플 콘텐츠 조각 구조(콘텐츠 조각 모델 및 관련 콘텐츠 조각)를 기반으로 합니다.


## GraphQL - 샘플 콘텐츠 조각 구조를 사용하는 샘플 쿼리 {#graphql-sample-queries-sample-content-fragment-structure}

샘플 결과와 더불어 쿼리 만들기에 대한 설명은 이 샘플 쿼리를 참조하십시오.

>[!NOTE]
>
>인스턴스에 따라 쿼리를 제출하고 테스트하기 위해 [AEM GraphQL API에 포함되어 있는 GraphiQL 인터페이스](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface)에 직접 액세스할 수 있습니다.
>
>예를 들어`http://localhost:4502/content/graphiql.html`

>[!NOTE]
>
>샘플 쿼리는 [GraphQL과 함께 사용하기 위한 샘플 콘텐츠 조각 구조](#content-fragment-structure-graphql)를 기반으로 합니다.

### 샘플 쿼리 - 사용 가능한 모든 스키마 및 데이터 형식 {#sample-all-schemes-datatypes}

사용 가능한 모든 스키마에 대한 모든 `types`이 반환됩니다.

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

**샘플 결과**:

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

모든 도시에 대한 모든 정보를 검색하려면 다음과 같은 매우 기본적인 쿼리를 사용하면 됩니다.
**샘플 쿼리**

```xml
{
  cityList {
    items
  }
}
```

실행되면 시스템은 모든 필드를 포함하도록 쿼리를 자동으로 확장합니다.

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

**샘플 결과**:

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

`city` 스키마에 있는 모든 항목의 `name`을 반환하는 간단한 쿼리입니다.

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

**샘플 결과**:

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

저장소의 특정 위치에 있는 단일 조각 항목의 세부 정보를 반환하는 쿼리입니다.

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

**샘플 결과**:

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

### 샘플 쿼리 - 이름이 붙은 변형이 있는 모든 도시 {#sample-cities-named-variation}

`city` Berlin에 대해 “Berlin Centre”(`berlin_centre`)라는 이름이 붙은 새 변형을 만드는 경우 쿼리를 사용하여 변형의 세부 정보를 반환할 수 있습니다.

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

**샘플 결과**:

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

### 샘플 쿼리 - 모든 도시의 이름 City Break로 태그 지정됨 {#sample-names-all-cities-tagged-city-breaks}

다음과 같은 경우:

* 다음과 같은 다양한 태그를 만듭니다. `Tourism` : `Business`, `City Break`, `Holiday`
* 다양한 유형의 기본 변형에 할당 `City` 인스턴스

그런 다음 쿼리를 사용하여 `name` 및 `tags`의 모든 게시물에 도시 브레이크로 태그가 지정됨 `city`스키마.

**샘플 쿼리**

```xml
query {
  cityList(
    includeVariations: true,
    filter: {_tags: {_expressions: [{value: "tourism:city-break", _operator: CONTAINS}]}}
  ){
    items {
      name,
      _tags
    }
  }
}
```

**샘플 결과**:

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Berlin",
          "_tags": [
            "tourism:city-break",
            "tourism:business"
          ]
        },
        {
          "name": "Zurich",
          "_tags": [
            "tourism:city-break",
            "tourism:business"
          ]
        }
      ]
    }
  }
}
```

### 샘플 쿼리 - 회사 CEO 및 직원의 전체 세부 정보 {#sample-full-details-company-ceos-employees}

중첩된 조각의 구조를 사용하여 이 쿼리는 회사 CEO와 모든 직원의 전체 세부 정보를 반환합니다.

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

**샘플 결과**:

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

### 샘플 쿼리 - 이름이 “Jobs” 또는 “Smith”인 모든 사람 {#sample-all-persons-jobs-smith}

이름이 `Jobs` 또는 `Smith`인 모든 `persons`가 필터링됩니다.

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

**샘플 결과**:

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

### 샘플 쿼리 - 이름이 “Jobs”가 아닌 모든 사람 {#sample-all-persons-not-jobs}

이름이 `Jobs` 또는 `Smith`인 모든 `persons`가 필터링됩니다.

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

**샘플 결과**:

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

### 샘플 쿼리 - `_path`가 특정 접두사로 시작하는 모든 모험 {#sample-wknd-all-adventures-cycling-path-filter}

`_path`가 특정 접두사로 시작하는 `adventures`(`/content/dam/wknd/en/adventures/cycling`).

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

**샘플 결과**:

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

### 샘플 쿼리 - 독일 또는 스위스에 위치한 인구 400000~999999의 모든 도시 {#sample-all-cities-d-ch-population}

여기에서는 필드를 조합하여 필터링됩니다. An `AND`(묵시적)는 `population`범위를 선택하는 데 사용되며, `OR`(명시적)는 필요한 도시를 선택하는 데 사용됩니다.

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

**샘플 결과**:

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

### 샘플 쿼리 - 대소문자에 관계없이 이름에 SAN이 있는 모든 도시 {#sample-all-cities-san-ignore-case}

이 쿼리는 대소문자에 관계없이 이름에 `SAN`이 있는 모든 도시에 대한 정보를 얻습니다.

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

**샘플 결과**:

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

### 샘플 쿼리 - 적어도 한 번은 발생해야 하는 항목이 있는 배열 필터링 {#sample-array-item-occur-at-least-once}

이 쿼리는 적어도 한 번은 발생해야 하는 항목(`city:na`)이 있는 배열을 필터링합니다.

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

**샘플 결과**:

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

### 샘플 쿼리 - 정확한 배열 값 필터링 {#sample-array-exact-value}

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

**샘플 결과**:

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

### 중첩된 콘텐츠 조각에 대한 샘플 쿼리 - 이름이 “Smith”인 직원이 한 명 이상 있는 모든 회사 {#sample-companies-employee-smith}

이 쿼리는 `name`이 “Smith”인 모든 `person`에 대한 필터링을 보여 주고, 두 가지 중첩된 조각(`company` 및 `employee`)에서 정보를 반환합니다.

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

**샘플 결과**:

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

### 중첩된 콘텐츠 조각에 대한 샘플 쿼리 - 모든 직원이 “Gamestar“ 상을 수상한 모든 회사 {#sample-all-companies-employee-gamestar-award}

이 쿼리는 세 가지 중첩된 조각(`company`, `employee`, `award`)에 대한 필터링을 보여 줍니다.

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

**샘플 결과**:

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

### 메타데이터에 대한 샘플 쿼리 - GB라는 제목의 상에 대한 메타데이터 나열 {#sample-metadata-awards-gb}

이 쿼리는 세 가지 중첩된 조각(`company`, `employee`, `award`)에 대한 필터링을 보여 줍니다.

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

**샘플 결과**:

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

이러한 샘플 쿼리는 WKND 프로젝트를 기반으로 합니다. 여기에는 다음이 있습니다.

* 콘텐츠 조각 모델은 다음에서 사용할 수 있습니다.
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* 콘텐츠 조각(및 기타 콘텐츠)은 다음에서 사용할 수 있습니다.
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`

>[!NOTE]
>
>결과가 광범위해질 수 있으므로 여기에서 재현하지는 않습니다.

### 지정된 속성을 가진 특정 모델의 모든 콘텐츠 조각에 대한 샘플 쿼리 {#sample-wknd-all-model-properties}

이 샘플 쿼리는 다음에 대한 정보를 얻습니다.

* `article` 유형의 모든 콘텐츠 조각
* `path` 및 `author` 속성 포함.

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

이 쿼리는 다음에 대한 정보를 얻습니다.

* `adventure` 유형의 모든 콘텐츠 조각
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

### 주어진 모델의 단일 콘텐츠 조각에 대한 샘플 쿼리 {#sample-wknd-single-content-fragment-of-given-model}

이 샘플 쿼리는 다음에 대한 정보를 얻습니다.

* 특정 경로에서 `article` 유형의 단일 콘텐츠 조각
   * 그 안에 있는 모든 형식의 콘텐츠:
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

### 모델의 콘텐츠 조각 모델에 대한 샘플 쿼리 {#sample-wknd-content-fragment-model-from-model}

이 샘플 쿼리는 다음에 대한 정보를 얻습니다.

* 단일 콘텐츠 조각
   * 기본 콘텐츠 조각 모델의 세부 정보

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

### 중첩된 콘텐츠 조각에 대한 샘플 쿼리 - 단일 모델 유형{#sample-wknd-nested-fragment-single-model}

이 쿼리는 다음에 대한 정보를 얻습니다.

* 특정 경로에서 `article` 유형의 단일 콘텐츠 조각
   * 그 안에 있는 참조된(중첩된) 조각의 경로 및 작성자

>[!NOTE]
>
>`referencearticle` 필드에는 `fragment-reference` 데이터 형식이 있습니다.

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

### 중첩된 콘텐츠 조각에 대한 샘플 쿼리 - 복수 모델 유형{#sample-wknd-nested-fragment-multiple-model}

이 쿼리는 다음에 대한 정보를 얻습니다.

* `bookmark` 유형의 복수 콘텐츠 조각
   * 특정 모델 유형 `article` 및 `adventure`의 다른 조각에 대한 조각 참조 포함

>[!NOTE]
>
>`fragments` 필드에는 `fragment-reference` 데이터 유형이 있습니다. `Article`, `Adventure` 모델이 선택되어 있습니다.

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

### 콘텐츠 참조가 있는 특정 모델의 콘텐츠 조각에 대한 샘플 쿼리{#sample-wknd-fragment-specific-model-content-reference}

이 쿼리에는 다음과 같은 두 가지 버전이 있습니다.

1. 모든 콘텐츠 참조 반환.
1. `attachments` 유형의 특정 콘텐츠 참조 반환.

이들 쿼리는 다음에 대한 정보를 얻습니다.

* `bookmark` 유형의 복수 콘텐츠 조각
   * 다른 조각에 대한 콘텐츠 참조 포함

#### 프리페치된 참조가 포함된 복수 콘텐츠 조각에 대한 샘플 쿼리 {#sample-wknd-multiple-fragments-prefetched-references}

다음 쿼리는 `_references`를 사용하여 모든 콘텐츠 참조를 반환합니다.

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

#### 첨부 파일이 포함된 복수 콘텐츠 조각에 대한 샘플 쿼리 {#sample-wknd-multiple-fragments-attachments}

다음 쿼리는 `content-reference` 유형의 특정 필드(하위 그룹)인 모든 `attachments`을 반환합니다.

>[!NOTE]
>
>`attachments` 필드에는 `content-reference` 데이터 형식이 있고, 다양한 형태가 선택되어 있습니다.

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

### RTE 인라인 참조가 포함된 단일 콘텐츠 조각에 대한 샘플 쿼리 {#sample-wknd-single-fragment-rte-inline-reference}

이 쿼리는 다음에 대한 정보를 얻습니다.

* 특정 경로에서 `bookmark` 유형의 단일 콘텐츠 조각
   * 그 안에 있는 RTE 인라인 참조

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

### 주어진 모델의 단일 콘텐츠 조각 변형에 대한 샘플 쿼리 {#sample-wknd-single-fragment-given-model}

이 쿼리는 다음에 대한 정보를 얻습니다.

* 특정 경로에서 `article` 유형의 단일 콘텐츠 조각
   * 그 안에 있는 변형: `variation1`과 관련된 데이터

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

### 주어진 모델의 복수 콘텐츠 조각의 이름이 붙은 변형에 대한 샘플 쿼리 {#sample-wknd-variation-multiple-fragment-given-model}

이 쿼리는 다음에 대한 정보를 얻습니다.

* 특정 변형: `variation1`이 포함된 `article` 유형의 콘텐츠 조각

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

### 주어진 모델의 여러 콘텐츠 조각 및 해당 변형에 대한 샘플 쿼리 {#sample-wknd-multiple-fragment-variations-given-model}

이 쿼리는 다음에 대한 정보를 얻습니다.

* 유형의 콘텐츠 조각 `article` 및 모든 변형

**샘플 쿼리**

```xml
query {
  articleList(
    includeVariations: true  ){
    items {
      _variation
      _path
      _tags
      _metadata {
        stringArrayMetadata {
          name
          value
        }
      }
    }
  }
}
```

### 특정 태그가 첨부된 특정 모델의 콘텐츠 조각 변형에 대한 샘플 쿼리{#sample-wknd-fragment-variations-given-model-specific-tag}

이 쿼리는 다음에 대한 정보를 얻습니다.

* 유형의 콘텐츠 조각 `article` 하나 이상의 변형 포함(태그 포함) `WKND : Activity / Hiking`

**샘플 쿼리**

```xml
{
  articleList(
    includeVariations: true,
    filter: {_tags: {_expressions: [{value: "wknd:activity/hiking", _operator: CONTAINS}]}}
  ){
    items {
      _variation
      _path
      _tags
      _metadata {
        stringArrayMetadata {
          name
          value
        }
      }
    }
  }
}
```

### 주어진 로케일의 복수 콘텐츠 조각에 대한 샘플 쿼리 {#sample-wknd-multiple-fragments-given-locale}

이 쿼리는 다음에 대한 정보를 얻습니다.

* `fr` 로케일 안에 있는 `article` 유형의 콘텐츠 조각

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

## 샘플 콘텐츠 조각 구조 (GraphQL과 함께 사용) {#content-fragment-structure-graphql}

샘플 쿼리는 다음 구조를 기반으로 합니다. 사용:

* 하나 이상의 [샘플 콘텐츠 조각 구조 모델](#sample-content-fragment-models-schemas) - GraphQL 스키마의 기반 형성

* 위 모델을 기반으로 하는 [샘플 콘텐츠 모델](#sample-content-fragments)

### 샘플 콘텐츠 조각 모델 (스키마) {#sample-content-fragment-models-schemas}

샘플 쿼리의 경우 다음 콘텐츠 모델 및 해당 상호 관계를 사용합니다(참조 ->):

* [회사](#model-company)
-> [사람](#model-person)
    -> [상](#model-award)

* [도시](#model-city)

#### 회사 {#model-company}

회사를 정의하는 기본 필드는 다음과 같습니다.

| 필드 이름 | 데이터 형식 | 참조 |
|--- |--- |--- |
| 회사 이름 | 한 줄 텍스트 |  |
| CEO | 조각 참조 (단일) | [개인](#model-person) |
| 직원 | 조각 참조 (다중 필드) | [개인](#model-person) |

#### 개인 {#model-person}

직원일 수도 있는 사람을 정의하는 필드입니다.

| 필드 이름 | 데이터 형식 | 참조 |
|--- |--- |--- |
| 이름 | 한 줄 텍스트 |  |
| 이름 | 한 줄 텍스트 |  |
| 상 | 조각 참조 (다중 필드) | [상](#model-award) |

#### 상 {#model-award}

상을 정의하는 필드는 다음과 같습니다.

| 필드 이름 | 데이터 형식 | 참조 |
|--- |--- |--- |
| 단축키/ID | 한 줄 텍스트 |  |
| 제목 | 한 줄 텍스트 |  |

#### 도시 {#model-city}

도시를 정의하는 필드는 다음과 같습니다.

| 필드 이름 | 데이터 형식 | 참조 |
|--- |--- |--- |
| 이름 | 한 줄 텍스트 |  |
| 국가 | 한 줄 텍스트 |  |
| 인구 | 숫자 |  |
| 범주 | 태그 |  |

### 샘플 콘텐츠 조각 {#sample-content-fragments}

다음 조각이 적절한 모델에 사용됩니다.

#### 회사 {#fragment-company}

| 회사 이름 | CEO | 직원 |
|--- |--- |--- |
| Apple | Steve Jobs | Duke Marsh<br>Max Caulfield |
|  Little Pony Inc. | Adam Smith | Lara Croft<br>Cutter Slade |
| NextStep Inc. | Steve Jobs | Joe Smith<br>Abe Lincoln |

#### 개인 {#fragment-person}

| 이름 | 이름 | 상 |
|--- |--- |--- |
| Lincoln |  Abe |  |
| Smith | Adam |   |
| Slade |  Cutter |  Gameblitz<br>Gamestar |
| Marsh |  Duke |   |   |
|  Smith |  Joe |   |
| Croft |  Lara | Gamestar |
| Caulfield |  Max |  Gameblitz |
|  Jobs |  Steve |   |

#### 상 {#fragment-award}

| 단축키/ID | 제목 |
|--- |--- |
| GB | Gameblitz |
|  GS | Gamestar |
|  OSC | Oscar |

#### 도시 {#fragment-city}

| 이름 | 국가 | 인구 | 범주 |
|--- |--- |--- |--- |
| 바젤 | 스위스 | 172258 | city:emea |
| 베를린 | 독일 | 3669491 | city:capital<br>city:emea |
| 부쿠레슈티 | 루마니아 | 1821000 |  city:capital<br>city:emea |
| 샌프란시스코 |  미국 |  883306 |  city:beach<br>city:na |
| 새너제이 |  미국 |  102635 |  city:na |
| 슈투트가르트 |  독일 |  634830 |  city:emea |
|  취리히 |  스위스 |  415367 |  city:capital<br>city:emea |
