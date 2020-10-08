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
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 2%

---


# 커뮤니티 구성 요소 기본 사항 {#communities-components-basics}

## 개요 {#overview}

설명서의 작성 섹션에서는 작성 편집 모드에서 AEM 사이트에 커뮤니티 기능을 추가하는 방법과 구성 요소 구성을 설명하는 방법을 설명합니다.

AEM 인스턴스와 대화형 커뮤니티 구성 요소 안내서를 사용하여 구성 요소를 [탐색할 수 있습니다](components-guide.md).

## 커뮤니티 구성 요소 액세스 {#accessing-communities-components}

페이지 컨텐츠를 작성할 때 기본 템플릿이 페이지의 디자인을 변경하도록 허용하는 경우 사이트 디자인의 일부로 구성 요소 브라우저에서 아직 사용할 수 없는 구성 요소를 활성화할 수 있습니다.

사용 가능한 커뮤니티 구성 요소는 [여기에 나와 있습니다](author-communities.md#available-communities-components).

>[!NOTE]
>
>일반 작성 정보는 페이지 작성에 대한 [빠른 안내서를 참조하십시오](../../help/sites-authoring/qg-page-authoring.md).
>
>AEM에 익숙하지 않은 경우 [기본 처리에 대한 설명서를 참조하십시오](../../help/sites-authoring/basic-handling.md).

### 디자인 모드 시작 {#entering-design-mode}

구성 요소 브라우저( **사이드킥됨)에서 커뮤니티** 구성 요소를 찾을 수 없으면 다른 커뮤니티 구성 요소를 `Design Mode` 추가하기 위해 입력해야 합니다. [필요한 클라이언트측 라이브러리](#required-clientlibs) (clientlibs)도 추가해야 할 수 있습니다.

자세한 내용은 디자인 모드에서 [구성 요소 구성을 참조하십시오](../../help/sites-authoring/default-components-designmode.md).

다음은 몇 개의 커뮤니티 구성 요소를 선택하고 구성 요소 브라우저에서 보는 이미지입니다.

![component-design](assets/component-design.png)

이제 구성 요소 브라우저에서 선택한 구성 요소를 사용할 수 있습니다.

![component-design1](assets/component-design1.png)

## 필수 Clientlibs {#required-clientlibs}

[구성 요소의 적절한 기능(JavaScript) 및 스타일(CSS)을 사용하려면 클라이언트측 라이브러리](../../help/sites-developing/clientlibs.md) (clientlibs)가 필요합니다.

페이지에 커뮤니티 구성 요소를 추가할 때, 결과가 오류이거나 예기치 않은 모양일 경우, 가장 먼저 시도해야 하는 것은 커뮤니티 구성 요소에 필요한 clientlibs를 추가하는 것입니다. 자세한 내용은 커뮤니티 구성 [요소용 Clientlibs를 참조하십시오](clientlibs.md).

### 예:처음에 클라이언트 라이브러리 없이 검토 작업.. {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ...클라이언트 라이브러리 사용 {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## 태깅 {#tagging}

많은 커뮤니티 기능을 구성하여 구성원이 게시 환경에서 입력(게시)된 컨텐츠에 태그를 지정할 수 있습니다.

태그 지정이 허용되는 경우 커뮤니티 사이트의 구성을 설정하여 게시 환경의 구성원에게 제공되는 네임스페이스를 제한할 수 있습니다. 커뮤니티 사이트 [콘솔을 참조하십시오](sites-console.md#tagging).

태그 지정을 허용하는 기능: [블로그](blog-feature.md), [일정](calendar.md), [파일 라이브러리](file-library.md), [포럼](forum.md)

태그를 사용하는 기능: [카탈로그](catalog.md), [검색](search.md), [소셜 태그 클라우드](tagcloud.md)

작성 정보:

* [태그 사용](../../help/sites-authoring/tags.md)

관리 정보:

* 태그 네임스페이스(분류) 만들기: [태그 관리](../../help/sites-administering/tags.md)
* 커뮤니티 사이트 구성:태그 지정 [참조](sites-console.md#tagging)
* [사용자 생성 컨텐츠 태그 지정](../../help/sites-authoring/tags.md)
* [태깅 지원 리소스](tag-resources.md)

개발자 정보:

* [AEM 태깅 프레임워크](../../help/sites-developing/framework.md)
* [Tagging Essentials](tag.md)

