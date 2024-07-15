---
title: 커뮤니티 구성 요소에 대한 Clientlibs
description: 사용 세부 정보를 수집하고 커뮤니티 구성 요소에 대한 디버깅 도구를 사용할 수 있도록 페이지에 클라이언트측 라이브러리(clientlibs)를 추가하는 방법을 알아봅니다.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# 커뮤니티 구성 요소에 대한 Clientlibs {#clientlibs-for-communities-components}

## 소개 {#introduction}

이 설명서 섹션에서는 Communities 구성 요소용 페이지에 클라이언트측 라이브러리(clientlib)를 추가하는 방법에 대해 설명합니다.

기본 정보는 다음을 참조하십시오.

* 사용 세부 정보 및 디버깅 도구를 제공하는 [클라이언트측 라이브러리 사용](/help/sites-developing/clientlibs.md)
* SCF 구성 요소를 사용자 지정할 때 유용한 정보를 제공하는 [SCF용 Clientlibs](/help/communities/client-customize.md#clientlibs)


## Clientlib이 필요한 이유 {#why-clientlibs-are-required}

Clientlib은 구성 요소의 적절한 기능(JavaScript) 및 스타일(CSS)에 필요합니다.

기능에 대한 [커뮤니티 기능](/help/communities/functions.md)이 있는 경우 필수 clientlib을 포함하여 필요한 모든 구성 요소 및 구성이 커뮤니티 사이트에 있습니다. 작성자가 추가 구성 요소를 사용할 수 있는 경우에만 clientlib을 추가해야 합니다.

필요한 clientlib이 없으면 [페이지에 Communities 구성 요소를 추가](/help/communities/author-communities.md)하면 JavaScript 오류가 발생하고 예기치 않은 오류가 발생할 수 있습니다.

### 예 : Clientlibs 없이 리뷰를 배치했습니다 {#example-placed-reviews-without-clientlibs}

![개의 리뷰 배치](assets/placed-reviews.png)

### 예 : Clientlibs를 사용하여 리뷰 배치 {#example-placed-reviews-with-clientlibs}

![reviews-clientlibs](assets/reviews-clientlibs.png)

## 필요한 Clientlibs 식별 {#identifying-required-clientlibs}

개발자를 위한 필수 기능 정보는 필요한 clientlib을 식별합니다.

또한 AEM 인스턴스에서 [커뮤니티 구성 요소 안내서](/help/communities/components-guide.md)를 탐색하면 구성 요소에 필요한 clientlib 범주 목록에 액세스할 수 있습니다.

예를 들어 [검토 페이지](https://localhost:4502/content/community-components/en/reviews.html)의 맨 위에 나열된 필수 clientlib은 다음과 같습니다

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-reviews](assets/clientlibs-reviews.png)

## 필수 Clientlibs 추가 {#adding-required-clientlibs}

Communities 구성 요소를 페이지에 추가하려면 구성 요소에 필요한 clientlib(아직 없는 경우)을 추가해야 합니다.

커뮤니티 사이트 페이지의 기존 clientlibslist를 수정하려면 [CRXDE|Lite](#using-crxde-lite)를 사용하십시오.

[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)을(를) 사용하여 커뮤니티 사이트에 clientlib을 추가하려면:

* [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)(으)로 이동합니다.
* 구성 요소를 추가할 페이지의 `clientlibslist` 노드를 찾습니다.

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* `clientlibslist` 노드가 선택된 경우:

   * String[] 속성 `scg:requiredClientLibs`을(를) 찾습니다.
   * 문자열 배열 대화 상자에 액세스할 수 있도록 해당 `Value`을(를) 선택하십시오.

      * 필요한 경우 아래로 스크롤합니다.
      * 새 클라이언트 라이브러리를 입력하려면 +를 선택하십시오.

         * 를 반복하여 클라이언트 라이브러리를 더 추가합니다.

         * **확인**&#x200B;을 선택합니다.

   * **모두 저장**&#x200B;을 선택합니다.

>[!NOTE]
>
>사이트가 커뮤니티 사이트가 아닌 경우 사이트에 사용 중인 클라이언트 라이브러리의 존재 또는 위치를 검색해야 합니다.

[AEM Communities 시작하기](/help/communities/getting-started.md) 예제를 사용합니다. 여기서 `site-name`은(는) *참여*&#x200B;입니다. reviews 구성 요소를 추가하면 clientliblist가 다음과 같이 표시됩니다.

![review-component](assets/review-component.png)
