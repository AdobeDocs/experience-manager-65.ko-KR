---
title: 검색 기능
seo-title: Search Feature
description: 커뮤니티 사이트에 검색 추가 및 구성
seo-description: Adding and configuring Search to a Communities site
uuid: ca633456-911f-447f-881e-653533125d5f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 3acac082-efbe-4995-b374-851cb9aaf62d
exl-id: e252b0e5-a2f8-468e-ac8c-951a5b0f2e32
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 2%

---

# 검색 기능 {#search-feature}

검색 기능은 포럼 등의 다른 다양한 기능과 함께 작동하여 컨텐츠를 검색할 수 있는 기능을 제공합니다.

UGC(사용자 생성 컨텐츠)라고 하는 커뮤니티 구성원이 입력한 게시물을 검색하는 기능을 추가할 때 두 가지 구성 요소가 있습니다. [검색](#search) 및 [검색 결과](#search-results).

를 포함하는 페이지 `Search Results` 구성 요소는 검색 및 결과 표시를 모두 지원합니다.

를 포함하는 페이지 `Search` 구성 요소에서는 검색 시작 위치에 결과가 표시됩니다 `Search Results` 페이지.

검색 기능은 사이트 방문자와 구성원이 컨텐츠를 볼 수 있도록 하는 다른 기능과 함께 사용할 수 있습니다.

## 검색 {#search-features}

### 페이지에 검색 추가 {#add-search-to-a-page}

을(를) 추가하려면 `Search` 구성 요소를 페이지에 작성자 모드에서 사용하려면 구성 요소 브라우저를 사용하여 를 찾습니다 `Communities / Search` 페이지로 끌어서 놓습니다. 사용 `Search` 에는 `Search Results.`

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](basics.md).

필요한 클라이언트측 라이브러리인 경우, `cq.social.hbs.search`, 포함 예 `Search` 구성 요소가 나타납니다.

![추가 검색](assets/add-search.png)

### 추가된 검색 구성 {#configure-the-added-search}

배치된 항목을 선택합니다 `Search` 액세스하여 선택할 구성 요소 `Configure` 아이콘 편집 대화 상자를 엽니다.

![참회하](assets/configure-new.png)

아래에 **[!UICONTROL 검색 설정]** 탭에서 방문자가 쿼리를 입력할 때 검색할 경로를 지정합니다.

![검색 설정](assets/search-settings.png)

* **[!UICONTROL 경로 검색]**
항목 추가 단추를 사용하여 검색 경로를 추가하면 컨텐츠 검색이 제한됩니다. 예를 들어 검색을 특정 포럼으로 제한하려면 페이지 내에 배치된 포럼 구성 요소를 선택합니다.

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL 결과 페이지]**
결과는 브라우저를 사용하여 을 포함하는 페이지를 선택함으로써 지정된 별도의 페이지에 표시됩니다 
`Search Results` 구성 요소.

## 검색 결과 {#search-results}

### 페이지에 검색 결과 추가 {#add-search-results-to-a-page}

을(를) 추가하려면 `Search Results` 구성 요소를 페이지에 작성자 모드에서 사용하려면 구성 요소 브라우저를 사용하여 를 찾습니다

* `Communities / Search Results`

페이지로 끌어서 놓습니다. 검색 구성 요소와 달리, 동일한 페이지에 결과가 표시되므로 두 번째 페이지가 필요하지 않습니다.

웹 사이트 내에서 다른 곳에서 검색을 사용하는 경우 이 페이지에서 `Search Results` 는 `Result Page` 의 `Search`.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](basics.md).

필요한 클라이언트측 라이브러리인 경우, `cq.social.hbs.search`, 포함 예 `Search Result` 구성 요소가 표시됩니다.

![검색 결과](assets/search-result1.png)

### 추가된 검색 결과 구성 {#configure-the-added-search-result}

배치된 항목을 선택합니다 `Search Results` 액세스하여 선택할 구성 요소 `Configure` 아이콘 편집 대화 상자를 엽니다.

![구성](assets/configure-new.png)

아래에 **[!UICONTROL 검색 결과 설정]** 탭에서는 방문자가 쿼리를 입력할 때 검색에 포함된 경로를 지정할 수 있습니다.

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL 페이지당 검색 결과 수]**

   페이지당 표시되는 주제/게시물 수를 정의합니다. 기본값은 10입니다.

* **[!UICONTROL 경로 검색]**

   항목 추가 단추를 사용하여 검색 경로를 추가하면 컨텐츠 검색이 제한됩니다.

## 추가 정보 {#additional-information}

자세한 내용은 [검색 핵심 사항](search-implementation.md) 개발자를 위한 페이지입니다.
