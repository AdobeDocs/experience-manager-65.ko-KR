---
title: 커뮤니티 구성 요소 기본 사항
seo-title: 커뮤니티 구성 요소 기본 사항
description: 편집 모드에서 AEM 사이트에 커뮤니티 기능 추가 및 구성 요소 구성
seo-description: 편집 모드에서 AEM 사이트에 커뮤니티 기능 추가 및 구성 요소 구성
uuid: c017a7c5-40d1-4592-9317-96fd727dac86
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 21714581-7645-4b47-a9b0-9f1424013240
exl-id: eb5ce76a-bf28-4540-bc2d-3b5ecb8286f2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 2%

---

# 커뮤니티 구성 요소 기본 사항 {#communities-components-basics}

## 개요 {#overview}

설명서의 작성 섹션에서는 작성자 편집 모드에서 AEM 사이트에 커뮤니티 기능을 추가하는 방법과 구성 요소 구성을 설명합니다.

구성 요소는 AEM 인스턴스와 대화형 [커뮤니티 구성 요소 안내서](components-guide.md)를 사용하여 탐색할 수 있습니다.

## 커뮤니티 구성 요소 {#accessing-communities-components} 액세스

페이지 컨텐츠를 작성할 때 기본 템플릿으로 페이지의 디자인을 변경할 수 있는 경우 구성 요소 브라우저에서 사이트 디자인의 일부로 아직 사용할 수 없는 구성 요소를 활성화할 수 있습니다.

사용 가능한 커뮤니티 구성 요소는 [여기](author-communities.md#available-communities-components)에 나열되어 있습니다.

>[!NOTE]
>
>일반 작성 정보는 [페이지 작성에 대한 빠른 안내서를 참조하십시오](../../help/sites-authoring/qg-page-authoring.md).
>
>AEM에 익숙하지 않은 경우 [기본 처리](../../help/sites-authoring/basic-handling.md)에서 설명서를 참조하십시오.

### 디자인 모드 시작 {#entering-design-mode}

**Communities** 구성 요소가 구성 요소 브라우저(사이드킥을)에 없으면 `Design Mode`를 입력하여 다른 커뮤니티 구성 요소를 추가해야 합니다. [필요한 클라이언트 측 라이브러리](#required-clientlibs) (clientlibs)도 추가해야 할 수 있습니다.

자세한 내용은 [디자인 모드에서 구성 요소 구성](../../help/sites-authoring/default-components-designmode.md)을 참조하십시오.

다음은 몇 개의 커뮤니티 구성 요소를 선택하고 구성 요소 브라우저에서 보는 이미지입니다.

![구성 요소 디자인](assets/component-design.png)

이제 선택한 구성 요소를 구성 요소 브라우저에서 사용할 수 있습니다.

![component-design1](assets/component-design1.png)

## 필수 Clientlibs {#required-clientlibs}

[구성 요소의 적절한 작동(JavaScript) 및 스타일 지정(CSS)에 클라이언트 측 라이브러리](../../help/sites-developing/clientlibs.md) (clientlibs)가 필요합니다.

페이지에 Communities 구성 요소를 추가할 때 결과가 오류이거나 예기치 않은 모양일 경우 먼저 Communities 구성 요소에 필요한 clientlibs를 추가해 보십시오. 자세한 내용은 [Clientlibs for Communities 구성 요소](clientlibs.md)를 참조하십시오.

### 예:처음에 클라이언트 라이브러리 없이 검토함.. {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ...및 클라이언트 라이브러리 {#and-with-client-libraries} 사용

![clientlibs2](assets/clientlibs2.png)

## 태깅 {#tagging}

많은 커뮤니티 기능을 구성원이 게시 환경에 입력(게시된)된 컨텐츠에 태그를 지정할 수 있도록 구성할 수 있습니다.

태깅이 허용되면 커뮤니티 사이트의 구성을 설정하여 게시 환경의 구성원에게 제공되는 네임스페이스를 제한할 수 있습니다. [커뮤니티 사이트 콘솔](sites-console.md#tagging)을 참조하십시오.

태깅을 허용하는 기능:[블로그](blog-feature.md), [달력](calendar.md), [파일 라이브러리](file-library.md), [포럼](forum.md)

태그를 사용하는 기능:[카탈로그](catalog.md), [검색](search.md), [소셜 태그 클라우드](tagcloud.md)

작성 정보:

* [태그 사용](../../help/sites-authoring/tags.md)

관리 정보:

* 태그 네임스페이스(분류) 만들기:[태그 관리](../../help/sites-administering/tags.md)
* 커뮤니티 사이트 구성:[태깅](sites-console.md#tagging) 참조
* [사용자 생성 컨텐츠에 태깅](../../help/sites-authoring/tags.md)
* [태깅 지원 리소스](tag-resources.md)

개발자 정보:

* [AEM 태깅 프레임워크](../../help/sites-developing/framework.md)
* [태깅 핵심 사항](tag.md)
