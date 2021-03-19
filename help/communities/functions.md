---
title: 커뮤니티 기능
seo-title: 커뮤니티 기능
description: 커뮤니티 기능 콘솔에 액세스하는 방법 살펴보기
seo-description: 커뮤니티 기능 콘솔에 액세스하는 방법 살펴보기
uuid: d3d70134-f318-4709-a673-b01a3467d980
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 91833914-b811-4355-a97d-e1a9cb7441f1
docset: aem65
role: 관리자
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2459'
ht-degree: 6%

---


# 커뮤니티 기능{#community-functions}

커뮤니티 경험에서 예상되는 기능 유형은 잘 알려져 있습니다. 커뮤니티 기능은 커뮤니티 기능으로 사용할 수 있습니다. 기본적으로 이 구성 요소는 작성 모드에서 페이지에 구성 요소를 추가하는 것 이상의 것이 필요한 커뮤니티 기능을 구현하기 위해 미리 연결된 하나 이상의 페이지입니다. 커뮤니티 사이트가 [만들어진 ](/help/communities/sites-console.md)커뮤니티 사이트 템플릿](/help/communities/sites.md)의 구조를 정의하는 데 사용되는 구성 블록입니다.[

커뮤니티 사이트가 만들어지면 표준 [AEM 제작 모드](/help/sites-authoring/editing-content.md)를 사용하여 결과 페이지에 컨텐츠가 추가될 수 있습니다. 커뮤니티 기능 콘솔에서 볼 수 있는 것처럼 다양한 커뮤니티 기능을 사용할 수 있습니다.

>[!NOTE]
>
>[커뮤니티 사이트](/help/communities/sites-console.md), [커뮤니티 사이트 템플릿](/help/communities/sites.md), [커뮤니티 그룹 템플릿](/help/communities/tools-groups.md) 및 [커뮤니티 함수](/help/communities/functions.md)를 만드는 콘솔은 작성 환경에서만 사용할 수 있습니다.

## 커뮤니티 기능 콘솔 {#community-functions-console}

작성 환경의 커뮤니티 함수 콘솔에 도달하려면 다음을 수행하십시오.

* **[!UICONTROL 도구]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 커뮤니티 함수]**&#x200B;로 이동합니다.

![community-functions](assets/community-functions.png)

## 미리 작성된 함수 {#pre-built-functions}

다음은 AEM Communities과 함께 제공되는 기능에 대한 간략한 설명입니다. 각 기능에는 [커뮤니티 사이트 템플릿](/help/communities/sites.md)에 쉽게 통합되는 기능에 연결된 커뮤니티 구성 요소가 포함된 하나 이상의 AEM 페이지가 포함되어 있습니다.

커뮤니티 사이트 템플릿은 로그인, 사용자 프로필, 알림, 메시지, 사이트 메뉴, 검색, 테마 및 브랜딩 기능을 포함한 커뮤니티 사이트의 구조를 제공합니다.

### 제목 및 URL 설정 {#title-and-url-settings}

**제목** 및  **** URL은 모든 커뮤니티 함수에 공통으로 사용되는 속성입니다.

커뮤니티 사이트 템플릿에 커뮤니티 함수가 추가되거나 [modifying](/help/communities/sites-console.md#modifying-site-properties) 커뮤니티 사이트의 구조를 수정할 때 추가된 경우, 제목 및 URL을 구성할 수 있도록 함수의 대화 상자가 열립니다.

#### 구성 기능 세부 사항 {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **제목**

   (*필수*) 사이트의 기능 메뉴에 나타나는 텍스트입니다.

* **URL**

   (*필수*) URI를 생성하는 데 사용되는 이름입니다. 이름은 AEM 및 JCR에서 지정한 [이름 지정 규칙](/help/sites-developing/naming-conventions.md)을 준수해야 합니다.

예를 들어 [시작하기](/help/communities/getting-started.md) 자습서(

* 제목 = 웹 페이지
* URL = 페이지

그런 다음 페이지의 URL은 https://localhost:4503/content/sites/engage/en/page.html입니다.

페이지의 메뉴 링크가 다음과 같이 표시됩니다.

![참여 페이지](assets/engage-page.png)

### 활동 스트림 기능 {#activity-stream-function}

활동 스트림 함수는 모든 보기(모든 활동, 사용자 활동 및 다음)가 선택된 [활동 스트림 구성 요소](/help/communities/activities.md)가 있는 페이지입니다. 개발자용 [Activity Stream Essentials](/help/communities/essentials-activities.md)도 참조하십시오.

템플릿에 추가하면 다음 대화 상자가 열립니다.

#### 구성 기능 세부 사항 {#configuration-function-details-1}

![함수 세부 정보](assets/function-details.png)

* [제목 및 URL 설정](#title-and-url-settings)

* **&quot;내 활동&quot; 보기 표시**

   이 옵션을 선택하면 활동 페이지에 현재 구성원이 커뮤니티 내에서 생성한 활동을 기준으로 하는 탭이 포함됩니다. 기본값이 선택됩니다.

* **&quot;모든 활동&quot; 보기 표시**

   이 옵션을 선택하면 활동 페이지에 현재 구성원이 액세스할 수 있는 커뮤니티 내에서 생성된 모든 활동이 포함된 탭이 포함됩니다. 기본값이 선택됩니다.

* **&quot;뉴스피드&quot; 보기 표시**

   이 옵션을 선택하면 활동 페이지에 현재 구성원이 팔로우하는 활동을 필터링하는 탭이 포함됩니다. 기본값이 선택됩니다.

### 지정 기능 {#assignments-function}

assignments 함수는 지원](/help/communities/overview.md#enablement-community)에 대한 [커뮤니티 사이트를 정의하는 기본 기능입니다. 커뮤니티 구성원에게 역량 강화 리소스를 할당할 수 있습니다. 개발자용 [Assignments Essentials](/help/communities/essentials-assignments.md)도 참조하십시오.

이 함수는 [지원 추가 기능](/help/communities/enablement.md)의 기능으로 사용할 수 있습니다. 역량 강화 Add-On은 제작 환경에서 사용할 수 있는 추가 라이선스가 필요합니다.

템플릿에 추가되면 [제목 및 URL 설정](#title-and-url-settings)에 대한 구성만 됩니다.

### 블로그 기능 {#blog-function}

블로그 함수는 태그 지정, 파일 업로드, 팔로잉, 자체 편집, 투표 및 중재를 위해 [블로그 구성 요소](/help/communities/blog-feature.md)가 구성된 페이지입니다. 개발자용 [Blog Essentials](/help/communities/blog-developer-basics.md)도 참조하십시오.

템플릿에 추가하면 다음 대화 상자가 열립니다.

![blog-component](assets/blog-component.png)

* [제목 및 URL 설정](#title-and-url-settings)

* **권한이 있는 구성원 허용**

   이 옵션을 선택하면 권한 멤버는 [권한이 있는 구성원 그룹](/help/communities/users.md#privileged-members-group)을 선택하여 아티클을 만들 수 있습니다. 선택하지 않으면 모든 커뮤니티 멤버가 만들 수 있습니다. 기본값은 선택 취소입니다.

* **파일 업로드 허용**

   이 옵션을 선택하면 멤버가 파일을 업로드할 수 있습니다. 기본값이 선택됩니다.

* **스레드된 회신 허용**

   선택하지 않으면 블로그에 아티클에 대한 답글(댓글)이 허용되지만 댓글에 대한 답글은 허용되지 않습니다. 기본값이 선택됩니다.

* **특별 포함된 컨텐츠 허용**

   이 옵션을 선택하면 해당 블로그는 [주요 컨텐츠](/help/communities/featured.md)로 식별됩니다. 기본값이 선택됩니다.

### 달력 기능 {#calendar-function}

달력 함수는 태그 지정을 허용하도록 [달력 구성 요소](/help/communities/calendar.md)가 구성된 페이지입니다. 개발자용 [Calendar Essentials](/help/communities/calendar-basics-for-developers.md)도 참조하십시오.

템플릿에 추가하면 다음 대화 상자가 열립니다.

![달력 세부 사항](assets/calendar-details.png)

* [제목 및 URL 설정](#title-and-url-settings)

* **고정 허용**

   선택하는 경우 포럼에서는 댓글 목록의 시작 부분에 주제 응답을 고정시킬 수 있습니다. 기본값이 선택됩니다.

* **권한이 있는 구성원 허용**

   이 옵션을 선택하면 권한 멤버는 [권한이 있는 구성원 그룹](/help/communities/users.md#privileged-members-group)을 선택하여 아티클을 만들 수 있습니다. 선택하지 않으면 모든 커뮤니티 멤버가 만들 수 있습니다. 기본값은 선택 취소입니다.

* **파일 업로드 허용**

   이 옵션을 선택하면 멤버가 파일을 업로드할 수 있습니다. 기본값이 선택됩니다.

* **스레드된 회신 허용**

   선택하지 않으면 블로그에 아티클에 대한 답글(댓글)이 허용되지만 댓글에 대한 답글은 허용되지 않습니다. 기본값이 선택됩니다.

* **특별 포함된 컨텐츠 허용**

   이 옵션을 선택하면 해당 컨텐츠가 [주요 컨텐츠](/help/communities/featured.md)로 식별됩니다. 기본값이 선택됩니다.

### 카탈로그 기능 {#catalog-function}

카탈로그 함수는 [역량 강화 커뮤니티](/help/communities/overview.md#enablement-community) 구성원이 할당되지 않은 지원 리소스를 검색할 수 있는 기능을 제공합니다. 개발자용 [Tagging Enablement Resources](/help/communities/tag-resources.md) 및 [Catalog Essentials](/help/communities/catalog-developer-essentials.md)을 참조하십시오.

커뮤니티 사이트의 모든 활성 리소스 및 학습 경로는 속성 ` [Show in Catalog](/help/communities/resources.md)`이 true로 설정된 경우 모든 카탈로그에 표시됩니다. 리소스와 학습 경로를 명시적으로 포함하려면 카탈로그에 [pre-filter](/help/communities/catalog-developer-essentials.md#pre-filters)를 적용해야 합니다.

템플릿에 추가하면 구성이 사이트 방문자에게 제공되는 태그 필터를 구성하는 데 사용되는 태그 네임스페이스를 지정할 수 있습니다.

![카탈로그 함수](assets/catalog-function.png)

* [제목 및 URL 설정](#title-and-url-settings)

* **[모든 네임스페이스] 선택**

   선택한 태그 네임스페이스는 카탈로그에서 나열되는 활성 리소스 목록을 필터링하기 위해 방문자가 선택할 수 있는 태그를 정의합니다.
이 옵션을 선택하면 커뮤니티 사이트에 대해 허용되는 모든 태그 네임스페이스를 사용할 수 있습니다.
선택 해제하면 커뮤니티 사이트에 대해 허용되는 하나 이상의 네임스페이스를 선택할 수 있습니다.
기본값이 선택됩니다.

### 주요 컨텐츠 함수 {#featured-content-function}

주요 컨텐츠 함수는 주석을 추가 및 삭제할 수 있도록 [주요 컨텐츠 구성 요소](/help/communities/featured.md)가 구성된 페이지입니다.

구성 요소별로 기능 컨텐츠 기능을 허용하거나 허용되지 않을 수 있습니다([블로그 함수](#blog-function), [달력 함수](#calendar-function), [포럼 함수](#forum-function), [아이디어 함수](#ideation-function) 및 [Qa 함수](#qna-function) 참조).

템플릿에 추가되면 [제목 및 URL 설정](#title-and-url-settings)에 대한 구성만 됩니다.

### 파일 라이브러리 기능 {#file-library-function}

파일 라이브러리 함수는 주석을 추가 및 삭제할 수 있도록 [파일 라이브러리 구성 요소](/help/communities/file-library.md)가 구성된 페이지입니다.

템플릿에 추가되면 [제목 및 URL 설정](#title-and-url-settings)에 대한 구성만 됩니다.

### 포럼 기능 {#forum-function}

포럼 함수는 태그 지정, 파일 업로드, 팔로잉, 자체 편집, 투표 및 중재를 위해 구성된 [포럼 구성 요소](/help/communities/forum.md)가 포함된 페이지입니다.

템플릿에 추가하면 다음 대화 상자가 열립니다.

#### 구성 기능 세부 사항 {#configuration-function-details-2}

![forum-component1](assets/forum-component1.png)

* [제목 및 URL 설정](#title-and-url-settings)

* **고정 허용**

   선택하는 경우 포럼에서는 댓글 목록의 시작 부분에 주제 응답을 고정시킬 수 있습니다. 기본값이 선택됩니다.

* **권한이 있는 구성원 허용**

   이 옵션을 선택하면 권한 구성원이 [권한이 있는 구성원 그룹](/help/communities/users.md#privileged-members-group)을 선택하여 항목을 게시할 수 있습니다. 선택하지 않으면 모든 커뮤니티 구성원이 게시할 수 있습니다. 기본값은 선택 취소입니다.

* **파일 업로드 허용**

   이 옵션을 선택하면 멤버가 파일을 업로드할 수 있습니다. 기본값이 선택됩니다.

* **스레드된 회신 허용**

   이 옵션을 선택하지 않으면 포럼에 주제에 대한 댓글이 허용되지만 해당 댓글에 대한 답글은 허용되지 않습니다. 기본값이 선택됩니다.

* **특별 포함된 컨텐츠 허용**

   이 옵션을 선택하면 구성 요소의 컨텐츠가 [주요 컨텐츠](/help/communities/featured.md)로 식별됩니다. 기본값이 선택됩니다.

### 그룹 함수 {#groups-function}

>[!CAUTION]
>
>그룹 함수는 *이 아닌*&#x200B;가&#x200B;*첫 번째 함수이거나 사이트의 구조나 커뮤니티 사이트 템플릿에 있는 유일한* 함수여야 합니다.
>
>[페이지 함수](#page-function)와 같은 다른 함수는 먼저 포함되고 나열되어야 합니다.

그룹 함수는 커뮤니티 구성원이 게시 환경의 커뮤니티 사이트 내에서 하위 커뮤니티를 만들 수 있는 기능을 제공합니다.

그룹 함수가 [커뮤니티 사이트 템플릿](/help/communities/sites.md)에 포함될 때 [설정](/help/communities/sites-console.md#groupmanagement)에 따라 그룹은 공개 또는 비공개 그룹일 수 있으며 커뮤니티 그룹이 실제로 생성될 때 템플릿 선택(예: 게시 환경)을 제공하도록 하나 이상의 커뮤니티 그룹 템플릿을 구성할 수 있습니다. [커뮤니티 그룹 템플릿](/help/communities/tools-groups.md)은 포럼 및 달력과 같이 그룹 페이지에 대해 만든 커뮤니티 기능을 지정합니다.

커뮤니티 그룹이 만들어지면 새 그룹에 대해 구성원 그룹이 동적으로 생성되며, 이 그룹에 구성원을 할당하거나 참여할 수 있습니다. 자세한 내용은 [사용자 및 사용자 그룹 관리](/help/communities/users.md)를 참조하십시오.

커뮤니티 [기능 팩 1](/help/communities/deploy-communities.md#latestfeaturepack)의 경우, 커뮤니티 그룹은 [커뮤니티 사이트의 그룹 콘솔](/help/communities/groups.md)을 사용하여 작성 환경에서 생성되며, 활성화되면 게시 환경에서 만들 수 있습니다.

템플릿에 추가하면 다음 대화 상자가 열립니다.

![group-template-config](assets/group-template-config.png)

* [제목 및 URL 설정](#title-and-url-settings)

* **그룹 템플릿 선택**

   게시 환경에서 새 커뮤니티 그룹의 향후 작성자가 선택할 수 있는 하나 이상의 활성화된 그룹 템플릿을 선택할 수 있는 드롭다운 목록입니다.

* **권한이 있는 구성원 허용**

   이 옵션을 선택하면 권한 구성원이 [권한이 있는 구성원 보안 그룹](/help/communities/users.md#privileged-members-group)을 선택하여 항목을 게시할 수 있습니다. 선택하지 않으면 모든 커뮤니티 구성원이 게시할 수 있습니다. 기본값은 선택 취소입니다.

* **게시 작성 허용**

   이 옵션을 선택하면 승인된 커뮤니티 구성원이 게시 환경에서 그룹을 만들 수 있습니다. 이 옵션을 선택 해제하면 커뮤니티 사이트의 그룹 콘솔에서 작성 환경에서만 새 그룹(하위 커뮤니티)을 만들 수 있습니다.
기본값이 선택됩니다.

### 관념화 기능 {#ideation-function}

관념화 함수는 [관념화 구성 요소](/help/communities/ideation-feature.md)가 하나 있는 페이지입니다.

템플릿에 추가하면 기본 제목 및 URL 이름과 템플릿의 기본 표시 설정을 지정하는 다음 대화 상자가 열립니다.

![관념화 함수](assets/ideation-function.png)

* [제목 및 URL 설정](#title-and-url-settings)

* **권한이 있는 구성원 허용**

   이 옵션을 선택하면 권한 구성원이 [권한이 있는 구성원 보안 그룹](/help/communities/users.md#privileged-members-group)을 선택하여 항목을 게시할 수 있습니다. 선택하지 않으면 모든 커뮤니티 구성원이 게시할 수 있습니다. 기본값은 선택 취소입니다.

* **파일 업로드 허용**

   이 옵션을 선택하면 멤버가 파일을 업로드할 수 있습니다. 기본값이 선택됩니다.

* **스레드된 회신 허용**

   이 옵션을 선택하지 않으면 주제에 대한 답글(댓글)을 허용하지만 댓글에 대한 답글은 허용되지 않습니다. 기본값이 선택됩니다.

* **특별 포함된 컨텐츠 허용**

   이 옵션을 선택하면 해당 컨텐츠가 [주요 컨텐츠](/help/communities/featured.md)로 식별됩니다. 기본값이 선택됩니다.

### 리더보드 기능 {#leaderboard-function}

leaderboard 함수는 [리더보드 구성 요소](/help/communities/enabling-leaderboard.md)가 하나 있는 페이지입니다.

**참고**:Leaderboard 기능을 포함하는 커뮤니티 템플릿에서 커뮤니티 사이트를 만든  ** 후 Leaderboard 구성 요소를 추가로 구성해야 합니다. 커뮤니티 사이트에 대한 [점수 지정 및 배지](/help/communities/implementing-scoring.md)의 구성에 따라 달라지는 리드 보드 구성 요소의 [규칙](/help/communities/enabling-leaderboard.md#rules-tab)을 지정합니다.

템플릿에 추가하면 기본 제목 및 URL 이름과 템플릿의 기본 표시 설정을 지정하는 다음 대화 상자가 열립니다.

![leaderboard dialog](assets/leaderboard-dialog.png)

* [제목 및 URL 설정](#title-and-url-settings)

* **배지 표시**

   이 옵션을 선택하면 배지 아이콘의 열이 리더보드에 포함됩니다.
기본값은 선택 취소입니다.

* **배지 이름 표시**

   이 옵션을 선택하면 배지 이름의 열이 리더보드에 포함됩니다.
기본값은 선택 취소입니다.

* **아바타 표시**

   이 옵션을 선택하면 멤버의 아바타 이미지가 구성원 프로필에 대한 이름 링크 옆에 있는 리드 보드에 포함됩니다.
기본값은 선택 취소입니다.

### 페이지 기능 {#page-function}

페이지 함수는 커뮤니티 사이트의 기능에 연결된 빈 페이지를 커뮤니티 사이트에 추가합니다.로그인, 메뉴, 알림, 메시지, 테마 및 브랜딩. 컨텐츠는 [표준 AEM 제작 모드](/help/sites-authoring/editing-content.md)를 사용하여 페이지에 추가됩니다.

템플릿에 추가되면 [제목 및 URL 설정](#title-and-url-settings)에 대한 구성만 됩니다.

### QnA 기능 {#qna-function}

QnA 함수는 태그 지정, 파일 업로드, 팔로잉, 자체 편집, 투표 및 중재를 위해 구성된 [QnA 구성 요소](/help/communities/working-with-qna.md)가 포함된 페이지입니다.

템플릿에 추가하면 권한이 있는 구성원에게 제한을 허용합니다.

![qna-dialog](assets/qna-dialog.png)

* [제목 및 URL 설정](#title-and-url-settings)

* **고정 허용**

   선택하는 경우 포럼에서는 댓글 목록의 시작 부분에 주제 응답을 고정시킬 수 있습니다. 기본값이 선택됩니다.

* **권한이 있는 구성원 허용**

   선택하는 경우 QnA 포럼은 [권한이 있는 구성원 그룹](/help/communities/users.md#privileged-members-group)을 선택하여 권한이 있는 구성원에게 질문을 게시할 수 있도록 허용합니다. 선택하지 않으면 모든 커뮤니티 구성원이 게시할 수 있습니다. 기본값은 선택 취소입니다.

* **파일 업로드 허용**

   이 옵션을 선택하면 멤버가 파일을 업로드할 수 있는 기능이 QnA 포럼에 포함됩니다. 기본값이 선택됩니다.

* **스레드된 회신 허용**

   이 옵션을 선택하지 않으면 게시된 질문에 대한 댓글(답변)을 허용하지만 답변에 대한 응답은 허용되지 않습니다. 기본값이 선택됩니다.

* **특별 포함된 컨텐츠 허용**

   이 옵션을 선택하면 해당 컨텐츠가 [주요 컨텐츠](/help/communities/featured.md)로 식별됩니다. 기본값이 선택됩니다.

## 커뮤니티 기능 만들기 {#create-community-function}

커뮤니티 함수 콘솔 상단에 있는 `Create Community Function` 아이콘을 선택하면 커뮤니티 기능을 만들 수 있습니다. 동일한 AEM Blueprint를 기반으로 하는 여러 함수를 만든 다음 작성자 편집 모드에서 열어 고유하게 사용자 정의할 수 있습니다.

![create-community-function](assets/create-community-function.png)

### 커뮤니티 기능 이름 {#community-function-name}

![function-name](assets/function-name.png)

커뮤니티 기능 이름 패널에서 이름, 설명 및 함수의 활성화 또는 비활성화 여부가 구성됩니다.

* **커뮤니티 기능 이름**

   표시 및 저장에 사용되는 함수 이름입니다.

* **커뮤니티 기능 설명**

   표시할 함수 설명입니다.

* **비활성화/활성화**

   함수 참조 여부를 제어하는 전환 스위치입니다.

### AEM 블루프린트 {#aem-blueprint}

![aem 블루프린트](assets/aem-blueprint.png)

`AEM Blueprint` 패널에서 커뮤니티 함수의 기본 구현인 블루프린트를 선택할 수 있습니다.

커뮤니티 함수는 로그인, 사용자 프로필, 알림, 메시지, 사이트 메뉴, 검색, 테마 및 브랜딩 기능을 포함하여 커뮤니티 사이트에 포함할 수 있도록 미리 연결된 하나 이상의 페이지가 포함되어 있는 미니 사이트입니다. 함수가 만들어지면 작성 편집 모드에서 [ 함수](#open-community-function)를 열고 페이지 또는 구성 요소 설정을 사용자 지정할 수 있습니다.

커뮤니티 함수는 [블루프린트](/help/sites-administering/msm-livecopy.md#creatingablueprint)의 [live copy](/help/sites-administering/msm.md#live-copies)로 구현되므로 해당 함수를 포함하는 [커뮤니티 사이트 템플릿](/help/communities/sites.md) 또는 [커뮤니티 그룹 템플릿](/help/communities/tools-groups.md)에서 만든 모든 커뮤니티 사이트 페이지에 영향을 주는 기능에 대한 변경 사항을 롤아웃할 수 있습니다. 페이지 수준을 수정하기 위해 상위 블루프린트에서 페이지 연결을 해제할 수도 있습니다.

[다중 사이트 관리자](/help/sites-administering/msm.md)도 참조하십시오.

### 썸네일 {#thumbnail}

![funtion-thumbnail](assets/funtion-thumbnail.png)

축소판 패널에서 이미지를 업로드하여 [커뮤니티 기능 콘솔](#community-functions-console)에 표시할 수 있습니다.

## 커뮤니티 기능 열기 {#open-community-function}

![open-function](assets/open-function.png)

페이지 컨텐츠를 작성하고 기능 구성 요소의 구성을 수정할 수 있는 작성자 편집 모드를 입력하려면 `Open Community Function` 아이콘을 선택합니다.

### 구성 요소 구성 {#configuring-components}

커뮤니티 함수는 AEM Blueprint의 Live Copy로 구현되며, 세부 사항은 [다중 사이트 관리자](/help/sites-administering/msm.md) 아래에 문서화됩니다.

페이지 컨텐츠를 작성하는 것뿐만 아니라 구성 요소를 구성할 수도 있습니다.

만들어진 커뮤니티 사이트의 페이지에 구성 요소를 구성하는 경우 구성 요소를 구성하기 위해 [상속](/help/sites-administering/msm-livecopy.md#changing-live-copy-content)을 취소해야 할 수 있습니다. 구성이 완료되면 상속을 다시 설정해야 합니다.

구성 세부 사항을 보려면 작성자를 위해 [커뮤니티 구성 요소](/help/communities/author-communities.md)를 방문하십시오.

## 커뮤니티 기능 편집 {#edit-community-function}

![편집 함수](assets/edit-function.png)

`Edit Community Function` 아이콘을 선택하여 [커뮤니티 함수](#create-community-function)와 동일한 패널을 사용하여 함수의 속성을 편집합니다(함수 활성화 또는 비활성화 포함).
