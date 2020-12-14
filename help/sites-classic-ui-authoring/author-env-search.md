---
title: 검색
seo-title: 검색
description: AEM의 작성 환경에서는 리소스 유형에 따라 컨텐츠를 검색하기 위한 다양한 메커니즘을 제공합니다.
seo-description: AEM의 작성 환경에서는 리소스 유형에 따라 컨텐츠를 검색하기 위한 다양한 메커니즘을 제공합니다.
uuid: 6dd3df4d-6040-4230-8373-fc028687b675
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 8d32960c-47c3-4e92-b02e-ad4d8fea7b2d
docset: aem65
translation-type: tm+mt
source-git-commit: 4dc4a518c212555b7833ac27de02087a403d3517
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 87%

---


# 검색{#searching}

AEM의 작성 환경에서는 리소스 유형에 따라 컨텐츠를 검색하기 위한 다양한 메커니즘을 제공합니다.

>[!NOTE]
>
>작성 환경 외부에서도 [Query Builder](/help/sites-developing/querybuilder-api.md) 및 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)와 같은 다른 메커니즘을 사용하여 검색할 수도 있습니다.

## 검색 기본 사항 {#search-basics}

검색 패널에 액세스하려면 해당 콘솔의 왼쪽 창 상단에 있는 **검색** 탭을 클릭합니다.

![chlimage_1-101](assets/chlimage_1-101.png)

검색 패널을 사용하면 모든 웹 사이트 페이지를 검색할 수 있습니다.여기에는 다음에 대한 필드와 위젯이 포함되어 있습니다.

* **전체 텍스트**: 지정된 텍스트 검색
* **수정 이후/이전**: 특정 날짜 사이에 변경된 페이지만 검색
* **템플릿**: 지정된 템플릿을 기반으로 하는 페이지만 검색
* **태그**: 지정된 태그가 있는 페이지만 검색

>[!NOTE]
>
>[Lucene 검색](/help/sites-deploying/queries-and-indexing.md)에 대한 인스턴스가 구성된 경우 **전체 텍스트**&#x200B;에 다음을 사용할 수 있습니다.
>
>* [와일드카드](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Wildcard_Searches)
>* [부울 연산자](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boolean_operators)

   >
   >
* [정규 표현식](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Regexp_Searches)
>* [필드 그룹화](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Field_Grouping)
>* [증폭](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boosting_a_Term)

>



창 하단에서 **검색**&#x200B;을 클릭하여 검색을 실행합니다. 검색 조건을 지우려면 **재설정**&#x200B;을 클릭합니다.

## 필터 {#filter}

다양한 위치에서 필터를 설정하여(그리고 지워서) 보기를 드릴다운 및 미세 조정할 수 있습니다.

![chlimage_1-102](assets/chlimage_1-102.png)

## 찾기 및 바꾸기 {#find-and-replace}

**웹 사이트** 콘솔에서 **찾기 및 바꾸기** 메뉴 옵션을 사용하여 웹 사이트 섹션 내에서 문자열을 반복하여 찾거나 바꿀 수 있습니다.

1. 찾기 및 바꾸기를 실행할 위치(루트 페이지 또는 폴더)를 선택합니다.
1. **도구** 를 선택한 후 **찾기 및 바꾸기**&#x200B;를 선택합니다.

   ![screen_shot_2012-02-15at120346pm](assets/screen_shot_2012-02-15at120346pm.png)

1. **찾기 및 바꾸기** 대화 상자에서 다음을 수행합니다.

   * 찾기를 시작할 루트 경로를 확인합니다.
   * 찾을 단어를 정의합니다.
   * 바꿀 단어를 정의합니다.
   * 대/소문자를 구분하여 검색할지를 지정합니다.
   * 단어 단위로만 찾을지 아니면 부분 문자열도 찾을지를 지정합니다.

   **미리 보기**&#x200B;를 클릭하면 해당 용어가 검색된 위치가 나열됩니다.바꿀 특정 인스턴스를 선택하거나 취소할 수 있습니다.

   ![screen_shot_2012-02-15at120719pm](assets/screen_shot_2012-02-15at120719pm.png)

1. **바꾸기**&#x200B;를 클릭하면 모든 인스턴스가 실제로 대체됩니다. 작업을 확인하는 메시지가 나타납니다.

찾기 및 바꾸기 서블릿의 기본 범위에는 다음과 같은 속성이 포함됩니다.

* `jcr:title`
* `jcr:description`
* `jcr:text`
* `text`

Apache Felix 웹 관리 콘솔(예: `https://localhost:4502/system/console/configMgr`)을 사용하여 범위를 변경할 수 있습니다. `CQ WCM Find Replace Servlet (com.day.cq.wcm.core.impl.servlets.FindReplaceServlet)`을 선택하고 필요에 따라 범위를 구성합니다.

>[!NOTE]
>
>표준 AEM 설치 환경에서 찾기 및 바꾸기는 Lucene을 사용하여 검색합니다.
>
>Lucene은 최대 16k 길이의 문자열 속성을 인덱싱합니다. 이 길이를 초과하는 문자열은 검색되지 않습니다.
