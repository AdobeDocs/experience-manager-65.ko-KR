---
title: 커뮤니티 기능
seo-title: Community Functions
description: 커뮤니티 기능 콘솔에 액세스하는 방법 알아보기
seo-description: Learn how to access the Community Functions console
uuid: d3d70134-f318-4709-a673-b01a3467d980
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 91833914-b811-4355-a97d-e1a9cb7441f1
docset: aem65
role: Admin
exl-id: 2395c895-c611-43ac-abb6-c2bc4b4a41f4
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '2224'
ht-degree: 6%

---

# 커뮤니티 기능{#community-functions}

커뮤니티 경험에서 예상되는 기능 유형은 잘 알려져 있습니다. 커뮤니티 기능은 커뮤니티 기능으로 사용할 수 있습니다. 기본적으로 구성 요소를 작성자 모드로 페이지에 추가하는 것 이상의 작업을 필요로 하는 커뮤니티 기능을 구현하기 위해 미리 배선된 하나 이상의 페이지입니다. 구성 요소는 의 구조를 정의하는 데 사용되는 빌딩 블록입니다. [커뮤니티 사이트 템플릿](/help/communities/sites.md) 커뮤니티 사이트 출처 [생성됨](/help/communities/sites-console.md).

커뮤니티 사이트가 생성되면 표준을 사용하여 결과 페이지에 콘텐츠를 추가할 수 있습니다 [AEM 작성 모드](/help/sites-authoring/editing-content.md). 커뮤니티 기능 콘솔에서 볼 수 있듯이 다양한 커뮤니티 기능을 사용할 수 있습니다.

>[!NOTE]
>
>만들기 위한 콘솔 [커뮤니티 사이트](/help/communities/sites-console.md), [커뮤니티 사이트 템플릿](/help/communities/sites.md), [커뮤니티 그룹 템플릿](/help/communities/tools-groups.md), 및 [커뮤니티 기능](/help/communities/functions.md) 는 작성 환경에서만 사용됩니다.

## 커뮤니티 기능 콘솔 {#community-functions-console}

작성 환경에서 커뮤니티 기능 콘솔에 도달하려면 다음을 수행하십시오.

* 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 커뮤니티 기능]**.

![community-functions](assets/community-functions.png)

## 사전 빌드된 함수 {#pre-built-functions}

다음은 AEM Communities과 함께 제공되는 기능에 대한 간략한 설명입니다. 각 함수에는 와(과) 쉽게 통합되는 기능에 함께 연결된 커뮤니티 구성 요소가 포함된 하나 이상의 AEM 페이지가 포함되어 있습니다. [커뮤니티 사이트 템플릿](/help/communities/sites.md).

커뮤니티 사이트 템플릿은 로그인, 사용자 프로필, 알림, 메시지, 사이트 메뉴, 검색, 테마 설정, 브랜딩 기능 등을 포함하는 커뮤니티 사이트 구조를 제공합니다.

### 제목 및 URL 설정 {#title-and-url-settings}

**제목** 및 **URL** 는 모든 커뮤니티 기능에 공통되는 속성입니다.

커뮤니티 기능을 커뮤니티 사이트 템플릿에 추가하거나 추가할 때 [수정 중](/help/communities/sites-console.md#modifying-site-properties) 커뮤니티 사이트의 구조에서는 제목 및 URL을 구성할 수 있도록 기능의 대화 상자가 열립니다.

#### 구성 기능 세부 사항 {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **제목**

   (*필수*) 사이트의 기능 메뉴에 나타나는 텍스트입니다

* **URL**

   (*필수*) URI를 생성하는 데 사용되는 이름입니다. 이름은 [이름 지정 규칙](/help/sites-developing/naming-conventions.md) AEM 및 JCR에서 적용합니다.

예를 들어 다음 작업을 수행하여 생성된 사이트를 사용합니다. [시작](/help/communities/getting-started.md) 자습서, 있는 경우

* 제목 = 웹 페이지
* URL = 페이지

그런 다음 페이지의 URL은 https://localhost:4503/content/sites/engage/en/page.html입니다.

그리고 페이지에 대한 메뉴 링크가 다음과 같이 표시됩니다.

![engage-page](assets/engage-page.png)

### 활동 스트림 기능 {#activity-stream-function}

활동 스트림 함수는 [활동 스트림 구성 요소](/help/communities/activities.md) 모든 보기(모든 활동, 사용자 활동 및 다음)가 선택된 경우. 참조: [활동 스트림 Essentials](/help/communities/essentials-activities.md) 개발자용.

템플릿에 추가되면 다음 대화 상자가 열립니다.

#### 구성 기능 세부 사항 {#configuration-function-details-1}

![function-details](assets/function-details.png)

* [제목 및 URL 설정](#title-and-url-settings)

* **&quot;내 활동&quot; 보기 표시**

   선택하면 현재 구성원이 커뮤니티 내에서 생성한 활동을 기반으로 활동을 필터링하는 탭이 활동 페이지에 포함됩니다. 기본값이 선택되어 있습니다.

* **&quot;모든 활동&quot; 보기 표시**

   선택하면 활동 페이지에 현재 구성원이 액세스할 수 있는 커뮤니티 내에서 생성된 모든 활동이 포함된 탭이 포함됩니다. 기본값이 선택되어 있습니다.

* **&quot;뉴스피드&quot; 보기 표시**

   선택하면 활동 페이지에 현재 멤버가 따르는 활동을 기반으로 활동을 필터링하는 탭이 포함됩니다. 기본값이 선택되어 있습니다.

### 블로그 기능 {#blog-function}

블로그 기능은 [블로그 구성 요소](/help/communities/blog-feature.md) 태깅, 파일 업로드, 팔로우, 구성원이 자체 편집, 투표 및 중재하도록 구성되었습니다. 참조: [블로그 기본 사항](/help/communities/blog-developer-basics.md) 개발자용.

템플릿에 추가되면 다음 대화 상자가 열립니다.

![blog-component](assets/blog-component.png)

* [제목 및 URL 설정](#title-and-url-settings)

* **권한이 있는 구성원 허용**

   선택한 경우, 블로그에서는 권한이 있는 구성원만 [권한이 있는 구성원 그룹](/help/communities/users.md#privileged-members-group). 선택하지 않으면 모든 커뮤니티 멤버가 만들 수 있습니다. 기본값은 선택 해제되어 있습니다.

* **파일 업로드 허용**

   선택한 경우 블로그에는 구성원이 파일을 업로드할 수 있는 기능이 포함됩니다. 기본값이 선택되어 있습니다.

* **스레드된 회신 허용**

   선택하지 않으면 블로그에 기사에 대한 답변(댓글)을 허용하지만 댓글에 대한 답변은 허용되지 않습니다. 기본값이 선택되어 있습니다.

* **특별 포함된 컨텐츠 허용**

   선택한 경우 블로그는 다음과 같이 식별됩니다. [특별 포함된 컨텐츠](/help/communities/featured.md). 기본값이 선택되어 있습니다.

### 달력 기능 {#calendar-function}

calendar 함수는 [달력 구성 요소](/help/communities/calendar.md) 태깅을 허용하도록 구성되었습니다. 참조: [달력 기본 사항](/help/communities/calendar-basics-for-developers.md) 개발자용.

템플릿에 추가되면 다음 대화 상자가 열립니다.

![calendar-details](assets/calendar-details.png)

* [제목 및 URL 설정](#title-and-url-settings)

* **고정 허용**

   선택하면 포럼에서 주제 답글을 댓글 목록의 시작 부분에 고정할 수 있습니다. 기본값이 선택되어 있습니다.

* **권한이 있는 구성원 허용**

   선택한 경우, 블로그에서는 권한이 있는 구성원만 [권한이 있는 구성원 그룹](/help/communities/users.md#privileged-members-group). 선택하지 않으면 모든 커뮤니티 멤버가 만들 수 있습니다. 기본값은 선택 해제되어 있습니다.

* **파일 업로드 허용**

   선택한 경우 블로그에는 구성원이 파일을 업로드할 수 있는 기능이 포함됩니다. 기본값이 선택되어 있습니다.

* **스레드된 회신 허용**

   선택하지 않으면 블로그에 기사에 대한 답변(댓글)을 허용하지만 댓글에 대한 답변은 허용되지 않습니다. 기본값이 선택되어 있습니다.

* **특별 포함된 컨텐츠 허용**

   선택한 경우 해당 콘텐츠는 (으)로 식별됩니다. [특별 포함된 컨텐츠](/help/communities/featured.md). 기본값이 선택되어 있습니다.

### 특별 포함된 컨텐츠 기능 {#featured-content-function}

주요 콘텐츠 함수는 [특별 포함된 컨텐츠 구성 요소](/help/communities/featured.md) 주석을 추가 및 삭제할 수 있도록 구성되었습니다.

구성 요소별로 콘텐츠 기능 사용이 허용되거나 허용되지 않을 수 있습니다(참조). [블로그 기능](#blog-function), [달력 기능](#calendar-function), [포럼 기능](#forum-function), [관념화 기능](#ideation-function), 및 [QnA 기능](#qna-function)).

템플릿에 추가되면 유일한 구성은 [제목 및 URL 설정](#title-and-url-settings).

### 파일 라이브러리 기능 {#file-library-function}

파일 라이브러리 함수는 [파일 라이브러리 구성 요소](/help/communities/file-library.md) 주석을 추가 및 삭제할 수 있도록 구성되었습니다.

템플릿에 추가되면 유일한 구성은 [제목 및 URL 설정](#title-and-url-settings).

### 포럼 기능 {#forum-function}

포럼 함수는 [포럼 구성 요소](/help/communities/forum.md) 태깅, 파일 업로드, 팔로우, 구성원이 자체 편집, 투표 및 중재하도록 구성되었습니다.

템플릿에 추가되면 다음 대화 상자가 열립니다.

#### 구성 기능 세부 사항 {#configuration-function-details-2}

![forum-component1](assets/forum-component1.png)

* [제목 및 URL 설정](#title-and-url-settings)

* **고정 허용**

   선택하면 포럼에서 주제 답글을 댓글 목록의 시작 부분에 고정할 수 있습니다. 기본값이 선택되어 있습니다.

* **권한이 있는 구성원 허용**

   이 옵션을 선택하면 포럼에서는 권한이 있는 구성원만 항목을 선택하여 게시할 수 있습니다. [권한이 있는 구성원 그룹](/help/communities/users.md#privileged-members-group). 선택하지 않으면 모든 커뮤니티 회원이 게시할 수 있습니다. 기본값은 선택 해제되어 있습니다.

* **파일 업로드 허용**

   이 옵션을 선택하면 포럼에 구성원이 파일을 업로드할 수 있습니다. 기본값이 선택되어 있습니다.

* **스레드된 회신 허용**

   선택하지 않으면 포럼에서 주제에 대한 댓글을 달 수 있지만, 해당 댓글에 대한 댓글은 회신할 수 없습니다. 기본값이 선택되어 있습니다.

* **특별 포함된 컨텐츠 허용**

   선택하면 구성 요소의 콘텐츠가 로 식별됩니다. [특별 포함된 컨텐츠](/help/communities/featured.md). 기본값이 선택되어 있습니다.

### 그룹 기능 {#groups-function}

>[!CAUTION]
>
>groups 함수는 *아님* 다음이 되어야 합니다. *처음도 아니고* 사이트의 구조 또는 커뮤니티 사이트 템플릿에서 작동합니다.
>
>기타 모든 함수(예: ) [페이지 기능](#page-function)를 포함해야 하며 먼저 나열되어야 합니다.

그룹 기능은 커뮤니티 구성원이 게시 환경의 커뮤니티 사이트 내에 하위 커뮤니티를 만들 수 있는 기능을 제공합니다.

다음에 종속 [설정](/help/communities/sites-console.md#groupmanagement) 에 그룹 함수가 포함된 경우 [커뮤니티 사이트 템플릿](/help/communities/sites.md), 그룹은 공개 또는 비공개일 수 있으며, 커뮤니티 그룹이 실제로 생성될 때(예: 게시 환경에서) 템플릿을 선택하도록 하나 이상의 커뮤니티 그룹 템플릿을 구성할 수 있습니다. A [커뮤니티 그룹 템플릿](/help/communities/tools-groups.md) 그룹 페이지에 대해 만들 커뮤니티 기능(예: 포럼 및 캘린더)을 지정합니다.

커뮤니티 그룹을 만들면 구성원을 할당하거나 가입할 수 있는 새 그룹에 대해 구성원 그룹이 동적으로 만들어집니다. 자세한 내용은 [사용자 및 사용자 그룹 관리](/help/communities/users.md).

커뮤니티 기준 [기능 팩 1](/help/communities/deploy-communities.md#latestfeaturepack), 커뮤니티 그룹은 작성 환경에서 [커뮤니티 사이트의 그룹 콘솔](/help/communities/groups.md), 및 를 활성화할 경우 게시 환경에서 만들 수 있습니다.

템플릿에 추가되면 다음 대화 상자가 열립니다.

![group-template-config](assets/group-template-config.png)

* [제목 및 URL 설정](#title-and-url-settings)

* **그룹 템플릿 선택**

   (게시 환경의) 새 커뮤니티 그룹의 향후 작성자가 선택할 수 있는 하나 이상의 활성화된 그룹 템플릿을 선택할 수 있는 드롭다운입니다.

* **권한이 있는 구성원 허용**

   이 옵션을 선택하면 포럼에서는 권한이 있는 구성원만 항목을 선택하여 게시할 수 있습니다. [권한이 있는 구성원 보안 그룹](/help/communities/users.md#privileged-members-group). 선택하지 않으면 모든 커뮤니티 회원이 게시할 수 있습니다. 기본값은 선택 해제되어 있습니다.

* **게시 작성 허용**

   선택한 경우 권한이 있는 커뮤니티 구성원이 게시 환경에서 그룹을 만들 수 있습니다. 선택을 취소하면 커뮤니티 사이트의 그룹 콘솔의 작성 환경에서만 새 그룹(하위 커뮤니티)을 만들 수 있습니다.
기본값이 선택되어 있습니다.

### 관념화 기능 {#ideation-function}

관념화 함수는 페이지가 1개인 페이지입니다 [관념화 구성 요소](/help/communities/ideation-feature.md).

템플릿에 추가되면 템플릿에 대한 기본 표시 설정과 기본 제목 및 URL 이름을 지정하는 다음 대화 상자가 열립니다.

![관념화 함수](assets/ideation-function.png)

* [제목 및 URL 설정](#title-and-url-settings)

* **권한이 있는 구성원 허용**

   이 옵션을 선택하면 포럼에서는 권한이 있는 구성원만 항목을 선택하여 게시할 수 있습니다. [권한이 있는 구성원 보안 그룹](/help/communities/users.md#privileged-members-group). 선택하지 않으면 모든 커뮤니티 회원이 게시할 수 있습니다. 기본값은 선택 해제되어 있습니다.

* **파일 업로드 허용**

   이 옵션을 선택하면 구성원이 파일을 업로드할 수 있는 기능이 아이디어에 포함됩니다. 기본값이 선택되어 있습니다.

* **스레드된 회신 허용**

   이 옵션을 선택하지 않으면 주제에 대한 답글(댓글)은 허용되지만 댓글에 대한 답글은 허용되지 않습니다. 기본값이 선택되어 있습니다.

* **특별 포함된 컨텐츠 허용**

   선택한 경우 해당 콘텐츠는 (으)로 식별됩니다. [특별 포함된 컨텐츠](/help/communities/featured.md). 기본값이 선택되어 있습니다.

### 리더보드 기능 {#leaderboard-function}

리더보드 함수는 1개가 있는 페이지입니다. [리더보드 구성 요소](/help/communities/enabling-leaderboard.md).

**참고**: 리더보드 구성 요소에 추가 구성이 필요합니다. *이후* 커뮤니티 사이트는 리더보드 기능이 포함된 커뮤니티 템플릿에서 만듭니다. 리더보드 구성 요소 지정 [규칙](/help/communities/enabling-leaderboard.md#rules-tab), 이는 의 구성에 따라 다릅니다. [채점 및 배지](/help/communities/implementing-scoring.md) 커뮤니티 사이트용.

템플릿에 추가되면 템플릿에 대한 기본 표시 설정과 기본 제목 및 URL 이름을 지정하는 다음 대화 상자가 열립니다.

![리더보드 대화 상자](assets/leaderboard-dialog.png)

* [제목 및 URL 설정](#title-and-url-settings)

* **배지 표시**

   선택하면 배지 아이콘에 대한 열이 순위표에 포함됩니다.
기본값은 선택 해제되어 있습니다.

* **배지 이름 표시**

   선택하면 배지 이름에 대한 열이 순위표에 포함됩니다.
기본값은 선택 해제되어 있습니다.

* **아바타 표시**

   선택하면 멤버의 아바타 이미지가 리더보드에 포함되며 멤버 프로필에 대한 이름 링크 옆에 있습니다.
기본값은 선택 해제되어 있습니다.

### 페이지 기능 {#page-function}

페이지 기능은 로그인, 메뉴, 알림, 메시지, 테마 및 브랜딩과 같은 커뮤니티 사이트의 기능에 연결된 커뮤니티 사이트에 빈 페이지를 추가합니다. 콘텐츠는 를 사용하여 페이지에 추가됩니다. [표준 AEM 작성 모드](/help/sites-authoring/editing-content.md).

템플릿에 추가되면 유일한 구성은 [제목 및 URL 설정](#title-and-url-settings).

### QnA 기능 {#qna-function}

QnA 함수는 [QnA 구성 요소](/help/communities/working-with-qna.md) 태깅, 파일 업로드, 팔로우, 구성원이 자체 편집, 투표 및 중재하도록 구성되었습니다.

템플릿에 추가될 때 구성을 통해 권한이 있는 멤버에 제한을 적용할 수 있습니다.

![qna-dialog](assets/qna-dialog.png)

* [제목 및 URL 설정](#title-and-url-settings)

* **고정 허용**

   선택하면 포럼에서 주제 답글을 댓글 목록의 시작 부분에 고정할 수 있습니다. 기본값이 선택되어 있습니다.

* **권한이 있는 구성원 허용**

   선택한 경우, QnA 포럼은 다음을 선택할 수 있도록 함으로써 권한이 있는 구성원만 질문을 게시할 수 있도록 합니다. [권한이 있는 구성원 그룹](/help/communities/users.md#privileged-members-group). 선택하지 않으면 모든 커뮤니티 회원이 게시할 수 있습니다. 기본값은 선택 해제되어 있습니다.

* **파일 업로드 허용**

   선택하면 QnA 포럼에 구성원이 파일을 업로드할 수 있습니다. 기본값이 선택되어 있습니다.

* **스레드된 회신 허용**

   선택하지 않으면 QnA 포럼에서 게시된 질문에 대한 댓글(답변)을 허용하지만 답변에 대한 답변은 허용되지 않습니다. 기본값이 선택되어 있습니다.

* **특별 포함된 컨텐츠 허용**

   선택한 경우 해당 콘텐츠는 (으)로 식별됩니다. [특별 포함된 컨텐츠](/help/communities/featured.md). 기본값이 선택되어 있습니다.

## 커뮤니티 기능 만들기 {#create-community-function}

커뮤니티 기능을 만들 수 있는 기능은 `Create Community Function` 커뮤니티 기능 콘솔의 맨 위에 있는 아이콘입니다. 작성자 편집 모드로 열어 동일한 AEM 블루프린트를 기반으로 한 여러 함수를 만든 다음 고유하게 사용자 지정할 수 있습니다.

![커뮤니티 기능 만들기](assets/create-community-function.png)

### 커뮤니티 기능 이름 {#community-function-name}

![function-name](assets/function-name.png)

커뮤니티 기능 이름 패널에서 이름, 설명 및 기능의 활성화/비활성화 여부가 구성됩니다.

* **커뮤니티 기능 이름**

   표시 및 저장에 사용되는 함수 이름입니다.

* **커뮤니티 기능 설명**

   표시할 함수 설명입니다.

* **사용 안 함/사용**

   함수를 참조할 수 있는지 여부를 제어하는 토글 스위치입니다.

### AEM 블루프린트 {#aem-blueprint}

![aem 블루프린트](assets/aem-blueprint.png)

다음에서 `AEM Blueprint` panel을 통해 커뮤니티 기능의 기본 구현인 블루프린트를 선택할 수 있다.

커뮤니티 기능은 로그인, 사용자 프로필, 알림, 메시지, 사이트 메뉴, 검색, 테마 및 브랜딩 기능을 포함하여 커뮤니티 사이트에 포함하기 위해 미리 연결된 하나 이상의 페이지를 포함하는 미니 사이트입니다. 함수가 만들어지면 다음을 수행할 수 있습니다. [함수 열기](#open-community-function) 작성자 편집 모드에서 페이지 또는 구성 요소 설정을 사용자 지정합니다.

커뮤니티 기능은 다음으로 구현됨: [live copy](/help/sites-administering/msm.md#live-copies) / [블루프린트](/help/sites-administering/msm-livecopy.md#creatingablueprint)에서 만든 모든 커뮤니티 사이트 페이지에 영향을 주는 함수에 대한 변경 사항을 롤아웃할 수 있습니다. [커뮤니티 사이트 템플릿](/help/communities/sites.md) 또는 [커뮤니티 그룹 템플릿](/help/communities/tools-groups.md) 거기에는 기능이 포함되어 있습니다. 상위 블루프린트에서 페이지의 연결을 해제하여 페이지 수준을 수정할 수도 있습니다.

참조: [다중 사이트 관리자](/help/sites-administering/msm.md).

### 썸네일 {#thumbnail}

![함수 썸네일](assets/funtion-thumbnail.png)

[썸네일] 패널에서 이미지를 업로드하여 [커뮤니티 기능 콘솔](#community-functions-console).

## 커뮤니티 기능 열기 {#open-community-function}

![개방 함수](assets/open-function.png)

다음 항목 선택 `Open Community Function` 페이지 콘텐츠를 작성하고 기능 구성 요소의 구성을 수정하기 위한 작성자 편집 모드에 들어가는 아이콘.

### 구성 요소 구성 {#configuring-components}

커뮤니티 기능은 AEM 블루프린트의 라이브 카피로 구현되며 자세한 내용은 아래에 문서화되어 있습니다. [다중 사이트 관리자](/help/sites-administering/msm.md).

페이지 콘텐츠를 작성할 수 있을 뿐만 아니라 구성 요소를 구성할 수도 있습니다.

생성된 커뮤니티 사이트의 페이지에 구성 요소를 구성하는 경우 취소해야 할 수 있습니다 [상속](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) 구성 요소를 구성합니다. 구성이 완료되면 상속을 다시 설정해야 합니다.

구성에 대한 자세한 내용은 다음을 참조하십시오. [커뮤니티 구성 요소](/help/communities/author-communities.md) 작성자용.

## 커뮤니티 기능 편집 {#edit-community-function}

![편집 기능](assets/edit-function.png)

다음 항목 선택 `Edit Community Function` 아이콘을 클릭하여 동일한 패널을 사용하여 함수의 속성을 편집합니다. [커뮤니티 기능 만들기](#create-community-function), 함수 활성화 또는 비활성화 포함.
