---
title: 커뮤니티 구성 요소 기본 사항
description: 편집 모드에서 AEM 사이트에 커뮤니티 기능을 추가하고 구성 요소를 구성합니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: eb5ce76a-bf28-4540-bc2d-3b5ecb8286f2
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 1%

---

# 커뮤니티 구성 요소 기본 사항 {#communities-components-basics}

## 개요 {#overview}

설명서의 작성 섹션에서는 작성자 편집 모드에서 AEM 사이트에 커뮤니티 기능을 추가하고 구성 요소 구성을 설명하는 방법에 대해 설명합니다.

AEM 인스턴스와 대화형 [커뮤니티 구성 요소 안내서](components-guide.md)를 사용하여 구성 요소를 탐색할 수 있습니다.

## 커뮤니티 구성 요소 액세스 {#accessing-communities-components}

페이지 콘텐츠를 작성할 때 기본 템플릿에서 페이지 디자인을 변경할 수 있는 경우, 사이트 디자인의 일부로서 구성 요소 브라우저에서 아직 사용할 수 없는 구성 요소를 활성화할 수 있습니다.

[사용 가능한 커뮤니티 구성 요소](author-communities.md#available-communities-components)의 목록을 참조하십시오.

>[!NOTE]
>
>일반 작성 정보는 [페이지 작성에 대한 빠른 안내](../../help/sites-authoring/qg-page-authoring.md)를 참조하십시오.
>
>AEM에 익숙하지 않은 경우 [기본 처리](../../help/sites-authoring/basic-handling.md)에 대한 설명서를 참조하십시오.

### 디자인 모드 시작 {#entering-design-mode}

구성 요소 브라우저(sidekick)에서 **커뮤니티** 구성 요소를 찾을 수 없으면 `Design Mode`을(를) 입력하여 다른 커뮤니티 구성 요소를 추가해야 합니다. [필요한 클라이언트측 라이브러리](#required-clientlibs)(clientlibs)도 추가해야 할 수 있습니다.

자세한 내용은 [디자인 모드에서 구성 요소 구성](../../help/sites-authoring/default-components-designmode.md)을 참조하십시오.

다음은 몇 가지 커뮤니티 구성 요소를 선택하고 구성 요소 브라우저에서 보는 이미지입니다.

![구성 요소 디자인](assets/component-design.png)

이제 구성 요소 브라우저에서 선택한 구성 요소를 사용할 수 있습니다.

![component-design1](assets/component-design1.png)

## 필수 Clientlibs {#required-clientlibs}

구성 요소의 적절한 기능(JavaScript)과 스타일(CSS)에는 [클라이언트측 라이브러리](../../help/sites-developing/clientlibs.md)(clientlibs)가 필요합니다.

페이지에 Communities 구성 요소를 추가할 때 결과가 오류 또는 예기치 않은 모양인 경우 먼저 Communities 구성 요소에 필요한 clientlib을 추가하는 것입니다. 자세한 내용은 [커뮤니티 구성 요소에 대한 Clientlibs](clientlibs.md)를 참조하십시오.

### 예: 처음에 클라이언트 라이브러리 없이 검토를 배치했습니다. {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ... 클라이언트 라이브러리 사용 {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## 태그 지정 {#tagging}

구성원이 게시 환경에 입력(게시)된 콘텐츠에 태그를 지정할 수 있도록 많은 커뮤니티 기능이 구성될 수 있습니다.

태깅이 허용되는 경우 게시 환경의 구성원에게 표시되는 네임스페이스를 제한하도록 커뮤니티 사이트의 구성을 설정할 수 있습니다. [커뮤니티 사이트 콘솔](sites-console.md#tagging)을 참조하세요.

태깅을 허용하는 기능: [블로그](blog-feature.md), [달력](calendar.md), [파일 라이브러리](file-library.md), [포럼](forum.md)

태그를 사용하는 기능: [검색](search.md), [소셜 태그 클라우드](tagcloud.md)

작성 정보의 경우:

* [태그 사용](../../help/sites-authoring/tags.md)

관리 정보의 경우:

* 태그 네임스페이스(분류법)를 만드는 중: [태그 관리](../../help/sites-administering/tags.md)
* 커뮤니티 사이트 구성: [태그 지정](sites-console.md#tagging) 참조
* [사용자 생성 컨텐츠 태깅](../../help/sites-authoring/tags.md)

개발자 정보:

* [AEM 태그 지정 프레임워크](../../help/sites-developing/framework.md)
* [태그 지정 기본 사항](tag.md)
