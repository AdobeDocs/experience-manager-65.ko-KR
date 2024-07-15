---
title: 검색
description: AEM의 작성 환경에서는 리소스 유형에 따라 콘텐츠를 검색하기 위한 다양한 메커니즘을 제공합니다.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 1f46a57f-4966-4dd1-8c99-c0740718ae76
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 13%

---

# 검색{#searching}

AEM의 작성 환경에서는 리소스 유형에 따라 콘텐츠를 검색하기 위한 다양한 메커니즘을 제공합니다.

>[!NOTE]
>
>작성 환경 외부에서 [쿼리 빌더](/help/sites-developing/querybuilder-api.md) 및 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)과 같은 다른 메커니즘을 검색할 수도 있습니다.

## 검색 기본 사항 {#search-basics}

검색 패널에 액세스하려면 해당 콘솔의 왼쪽 창 상단에 있는 **검색** 탭을 클릭합니다.

![chlimage_1-101](assets/chlimage_1-101.png)

검색 패널을 사용하면 모든 웹 사이트 페이지를 검색할 수 있습니다. 여기에는 다음에 대한 필드 및 위젯이 포함되어 있습니다.

* **전체 텍스트**: 지정된 텍스트를 검색합니다.
* **다음 날짜 이후/이전에 수정됨**: 특정 날짜 사이에 변경된 페이지만 검색합니다.
* **템플릿**: 지정된 템플릿을 기준으로 해당 페이지만 검색
* **태그**: 지정된 태그가 있는 페이지만 검색

>[!NOTE]
>
>인스턴스가 [Lucene 검색](/help/sites-deploying/queries-and-indexing.md)에 대해 구성된 경우 **전체 텍스트**&#x200B;에서 다음을 사용할 수 있습니다.
>
>* [와일드카드](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Wildcard_Searches)
>* [부울 연산자](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boolean_operators)
>
>* [정규 표현식](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Regexp_Searches)
>* [필드 그룹화](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Field_Grouping)
>* [증폭](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boosting_a_Term)
>

창 맨 아래에 있는 **검색**&#x200B;을 클릭하여 검색을 실행하십시오. 검색 조건을 지우려면 **재설정**&#x200B;을 클릭하세요.

## 필터 {#filter}

다양한 위치에서 드릴다운하고 보기를 세분화하기 위해 필터를 설정(및 지우기)할 수 있습니다.

![chlimage_1-102](assets/chlimage_1-102.png)

## 찾기 및 바꾸기 {#find-and-replace}

**웹 사이트** 콘솔에서 **찾기 및 바꾸기** 메뉴 옵션을 사용하면 웹 사이트의 섹션에서 여러 문자열 인스턴스를 검색하고 바꿀 수 있습니다.

1. 찾기 및 바꾸기 작업을 수행할 루트 페이지 또는 폴더를 선택합니다.
1. **도구**&#x200B;를 선택한 다음 **찾기 및 바꾸기**&#x200B;를 선택합니다.

   ![screen_shot_2012-02-15at120346pm](assets/screen_shot_2012-02-15at120346pm.png)

1. **찾기 및 바꾸기** 대화 상자는 다음을 수행합니다.

   * 찾기 작업이 시작되어야 하는 루트 경로를 확인합니다.
   * 찾을 용어 정의
   * 대체해야 하는 용어를 정의합니다.
   * 검색에서 대/소문자를 구분해야 하는지 여부를 나타냅니다.
   * 전체 단어만 찾을 수 있는지 여부를 나타냅니다(그렇지 않은 경우 하위 문자열도 찾을 수 있음).

   **미리 보기**&#x200B;를 클릭하면 용어가 발견된 위치가 나열됩니다. 대체할 특정 인스턴스를 선택/지울 수 있습니다.

   ![screen_shot_2012-02-15at120719pm](assets/screen_shot_2012-02-15at120719pm.png)

1. 실제로 모든 인스턴스를 바꾸려면 **바꾸기**&#x200B;를 클릭하십시오. 작업을 확인하는 메시지가 표시됩니다.

찾기 및 바꾸기 서블릿의 기본 범위는 다음 속성을 포함합니다.

* `jcr:title`
* `jcr:description`
* `jcr:text`
* `text`

Apache Felix 웹 관리 콘솔을 사용하여 범위를 변경할 수 있습니다(예: `https://localhost:4502/system/console/configMgr`). `CQ WCM Find Replace Servlet (com.day.cq.wcm.core.impl.servlets.FindReplaceServlet)`을(를) 선택하고 필요에 따라 범위를 구성합니다.

>[!NOTE]
>
>표준 AEM 설치에서 찾기와 바꾸기는 Lucene을 사용하여 검색 기능을 제공합니다.
>
>Lucene은 최대 16k 길이의 문자열 속성을 인덱싱합니다. 이 값을 초과하는 문자열은 검색되지 않습니다.
