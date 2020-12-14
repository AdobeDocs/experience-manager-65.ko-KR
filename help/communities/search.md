---
title: 검색 기능
seo-title: 검색 기능
description: 커뮤니티 사이트에 검색 추가 및 구성
seo-description: 커뮤니티 사이트에 검색 추가 및 구성
uuid: ca633456-911f-447f-881e-653533125d5f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 3acac082-efbe-4995-b374-851cb9aaf62d
translation-type: tm+mt
source-git-commit: 6ab91667ad668abf80ccf1710966169b3a187928
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 2%

---


# 검색 기능 {#search-feature}

검색 기능은 포럼과 같은 다양한 기타 기능과 연동되므로 컨텐츠를 검색할 수 있습니다.

커뮤니티 구성원이 입력한 게시물(사용자 생성 컨텐츠(UGC)을 검색하는 기능을 추가하면 다음과 같은 2가지 구성 요소가 있습니다.[검색](#search) 및 [검색 결과](#search-results).

`Search Results` 구성 요소를 포함하는 페이지는 검색 및 결과 표시를 모두 지원합니다.

`Search` 구성 요소를 포함하는 페이지는 `Search Results` 페이지에 결과가 나타나는 검색을 시작할 수 있는 위치를 제공합니다.

검색 기능은 사이트 방문자와 구성원이 컨텐츠를 볼 수 있도록 하는 다른 모든 기능과 함께 사용할 수 있습니다.

## 검색 {#search-features}

### {#add-search-to-a-page} 페이지에 검색 추가

작성 모드에서 페이지에 `Search` 구성 요소를 추가하려면 구성 요소 브라우저를 사용하여 `Communities / Search`을(를) 찾아 페이지에 제자리로 드래그합니다. `Search`을(를) 사용하려면 `Search Results.`에 대한 두 번째 페이지가 필요합니다.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](basics.md)을 방문하십시오.

필요한 클라이언트측 라이브러리 `cq.social.hbs.search`이(가) 포함되어 있으면 `Search` 구성 요소가 표시되는 방법입니다.

![add-search](assets/add-search.png)

### 추가된 검색 구성 {#configure-the-added-search}

액세스할 배치된 `Search` 구성 요소를 선택하고 편집 대화 상자를 여는 `Configure` 아이콘을 선택합니다.

![고백](assets/configure-new.png)

**[!UICONTROL 검색 설정]** 탭에서 방문자가 쿼리를 입력했을 때 검색할 경로를 지정합니다.

![검색 설정](assets/search-settings.png)

* **[!UICONTROL 검색]**
경로항목 추가 단추를 사용하여 검색 경로를 추가하면 컨텐츠 검색이 제한됩니다. 예를 들어 검색을 특정 포럼으로 제한하려면 페이지 내에 있는 포럼 구성 요소를 선택합니다.

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL 결과]**
페이지검색 결과는 브라우저를 사용하여 
`Search Results` 구성 요소.

## 검색 결과 {#search-results}

### 페이지 {#add-search-results-to-a-page}에 검색 결과 추가

작성 모드에서 페이지에 `Search Results` 구성 요소를 추가하려면 구성 요소 브라우저를 사용하여

* `Communities / Search Results`

페이지로 드래그하여 배치합니다. 검색 구성 요소와 달리, 같은 페이지에 결과가 표시되므로 두 번째 페이지가 필요하지 않습니다.

웹 사이트 내의 다른 곳에서 검색을 사용하는 경우 `Search Results`이 있는 이 한 페이지가 `Search`의 모든 인스턴스에 대해 `Result Page`으로 구성될 수 있습니다.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](basics.md)을 방문하십시오.

필요한 클라이언트측 라이브러리 `cq.social.hbs.search`이(가) 포함되어 있으면 `Search Result` 구성 요소가 다음과 같이 표시됩니다.

![검색 결과](assets/search-result1.png)

### 추가된 검색 결과 구성 {#configure-the-added-search-result}

액세스할 배치된 `Search Results` 구성 요소를 선택하고 편집 대화 상자를 여는 `Configure` 아이콘을 선택합니다.

![configure](assets/configure-new.png)

**[!UICONTROL 검색 결과 설정]** 탭에서 방문자가 쿼리를 입력했을 때 검색에 포함할 경로를 지정할 수 있습니다.

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL 페이지당 검색 결과 수]**

   페이지당 표시되는 항목/게시물 수를 정의합니다. 기본값은 10입니다.

* **[!UICONTROL 검색 경로]**

   [항목 추가] 단추를 사용하여 검색 경로를 추가하면 컨텐츠 검색이 제한됩니다.

## 추가 정보 {#additional-information}

개발자를 위한 [필수 항목 검색](search-implementation.md) 페이지에서 자세한 내용을 확인할 수 있습니다.
