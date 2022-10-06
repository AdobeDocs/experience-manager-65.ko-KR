---
title: 커뮤니티 구성 요소용 Clientlibs
seo-title: Clientlibs for Communities Components
description: Communities용 클라이언트 측 라이브러리
seo-description: Client-side libraries for Communities
uuid: d2a9f986-96cf-4ee8-81e6-36a96f45ddcb
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 68ce47c8-a03f-40d6-a7f3-2cc64aee0594
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# 커뮤니티 구성 요소용 Clientlibs {#clientlibs-for-communities-components}

## 소개 {#introduction}

설명서의 이 섹션에서는 커뮤니티 구성 요소의 페이지에 클라이언트측 라이브러리(clientlibs)를 추가하는 방법을 설명합니다.

기본 정보를 보려면 를 방문하십시오.

* [클라이언트측 라이브러리 사용](/help/sites-developing/clientlibs.md) 사용 세부 사항 및 디버깅 도구를 제공합니다.
* [SCF용 Clientlibs](/help/communities/client-customize.md#clientlibs) SCF 구성 요소를 사용자 지정할 때 유용한 정보를 제공합니다.


## Clientlibs가 필요한 이유 {#why-clientlibs-are-required}

Clientlibs는 구성 요소의 적절한 작동(JavaScript) 및 스타일(CSS)에 필요합니다.

가 있는 경우 [커뮤니티 기능](/help/communities/functions.md) 기능의 경우 필수 clientlibs를 포함한 필요한 모든 구성 요소 및 구성이 커뮤니티 사이트에 있을 것입니다. 작성자가 추가 구성 요소를 사용할 수 있어야 clientlibs를 추가해야 합니다.

필요한 clientlibs가 없으면 [페이지에 커뮤니티 구성 요소 추가](/help/communities/author-communities.md) 예기치 않은 모양일 뿐만 아니라 javascript 오류가 발생할 수 있습니다.

### 예 : Clientlibs 없이 평가된 항목 {#example-placed-reviews-without-clientlibs}

![평가](assets/placed-reviews.png)

### 예 : Clientlibs를 사용하여 검토함 {#example-placed-reviews-with-clientlibs}

![reviews-clientlibs](assets/reviews-clientlibs.png)

## 필수 Clientlibs 식별 {#identifying-required-clientlibs}

개발자를 위한 필수 기능 정보는 필요한 clientlibs를 식별합니다.

또한 AEM 인스턴스에서 [커뮤니티 구성 요소 안내서](/help/communities/components-guide.md) 구성 요소에 필요한 clientlib 카테고리 목록에 대한 액세스 권한을 제공합니다.

예를 들어, 맨 위의 [검토 페이지](https://localhost:4502/content/community-components/en/reviews.html) 나열된 필수 clientlibs는 다음과 같습니다

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs 검토](assets/clientlibs-reviews.png)

## 필수 Clientlibs 추가 {#adding-required-clientlibs}

페이지에 Communities 구성 요소를 추가하려면, 아직 없는 경우 구성 요소에 필요한 clientlibs를 추가해야 합니다.

사용 [CRXDE|Lite](#using-crxde-lite) 커뮤니티 사이트 페이지에 대한 기존 clientlibslist를 수정하려면

를 사용하여 커뮤니티 사이트에 대한 clientlib을 추가하려면 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* 찾아보기 [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de).
* 을(를) 찾습니다 `clientlibslist` 구성 요소를 추가할 페이지의 노드:

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* 사용 `clientlibslist` 노드 선택:

   * 문자열 찾기[] 속성 `scg:requiredClientLibs`.
   * 선택 `Value` 문자열 배열 대화 상자에 액세스합니다.

      * 필요한 경우 아래로 스크롤합니다.
      * 새 클라이언트 라이브러리를 입력하려면 + 를 선택합니다.

         * 이 단계를 반복하여 클라이언트 라이브러리를 더 추가합니다.

         * 선택 **확인**.
   * 선택 **모두 저장**.


>[!NOTE]
>
>사이트가 커뮤니티 사이트가 아닌 경우, 사이트에 대해 사용 중인 클라이언트 라이브러리의 존재 또는 위치를 검색해야 합니다.

사용 [AEM Communities 시작하기](/help/communities/getting-started.md) 예, 여기서 `site-name` is *참여*: 검토 구성 요소를 추가할 때 clientliblist가 표시되는 방식입니다.

![review-component](assets/review-component.png)
