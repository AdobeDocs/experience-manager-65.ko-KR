---
title: 게시된 사이트 경험
seo-title: Experience the Published Site
description: 게시된 사이트 로 이동하여 활성화
seo-description: Browse to a published site for enablement
uuid: 1bfefa8a-fd9c-4ca8-b2ff-add79776c8ae
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 26715b94-e2ea-4da7-a0e2-3e5a367ac1cd
exl-id: 801416ed-d321-45a2-8032-8935094a4d44
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 2%

---

# 게시된 사이트 경험 {#experience-the-published-site}


**[⇐ 지원 리소스 만들기 및 할당](resource.md)**

## 게시할 때 새 사이트 찾아보기 {#browse-to-new-site-on-publish}

새로 만든 커뮤니티 사이트 및 해당 지원 리소스 및 학습 경로가 게시되었으므로 사용 자습서 사이트를 체험할 수 있습니다.

먼저 사이트를 만들 때 표시되는 URL로 탐색하고, 예를 들어 게시 서버에서

* 작성자 URL = [http://localhost:4502/content/sites/enable/en.html](http://localhost:4502/content/sites/enable/en.html)
* 게시 URL = [http://localhost:4503/content/sites/enable/en.html](http://localhost:4503/content/sites/enable/en.html)

만약 [기본 홈 페이지가 설정됨](enablement-create-site.md#changethedefaulthomepage)로 이동한 다음 [http://localhost:4503/](http://localhost:4503/) 사이트를 실행해야 합니다.

게시된 사이트에 처음 도달하면 사이트 방문자는 일반적으로 아직 로그인하지 않으며 익명 상태가 됩니다.

**http://localhost:4503/content/sites/enable/en.html**

![enablement-login](assets/enablement-login.png)

## 익명 사이트 방문자 {#anonymous-site-visitor}

익명의 사이트 방문자에게 이 개인 지원 커뮤니티 사이트에 대한 로그인 페이지가 즉시 표시됩니다. facebook 또는 Twitter으로 자체 등록하거나 로그인할 수 있는 옵션이 없습니다.

이 홈 페이지에는 다음 네 가지 메뉴 항목이 표시됩니다. `Assignments, Ski Catalog, What's New` 및 `Discussions`하지만 로그인하지 않으면 아무 것도 연결할 수 없습니다.

>[!NOTE]
>
>사이트 방문자가 자체 등록할 수 없도록 하지 않고 지원 사이트에 대한 익명 액세스 권한을 부여할 수 있습니다.
>
>사용 리소스가 `show in catalog` 및 `allow anonymous access`를 입력하면 익명 사이트 방문자가 카탈로그에서 리소스를 볼 수 있습니다.

### JCR에 대한 익명 액세스 방지 {#prevent-anonymous-access-on-jcr}

하지만 알려진 제한은 jcr 컨텐츠 및 json 을 통해 커뮤니티 사이트 컨텐츠를 익명 방문자에게 노출합니다 **[!UICONTROL 익명 액세스 허용]** 사이트 컨텐츠에 대해 이 비활성화되어 있습니다. 그러나 해결 방법으로 Sling 제한을 사용하여 이 동작을 제어할 수 있습니다.

jcr 컨텐츠 및 json 을 통해 익명의 사용자가 커뮤니티 사이트의 컨텐츠를 액세스하지 못하도록 보호하려면 다음 단계를 수행합니다.

1. AEM 작성자 인스턴스에서 https://으로 이동합니다.&lt;host>:&lt;port>/editor.html/content/site/&lt;sitename>.html

   >[!NOTE]
   >
   >현지화된 사이트로 이동하지 마십시오.

1. 이동 **[!UICONTROL 페이지 속성]**.

   ![page-properties](assets/page-properties.png)

1. 이동 **[!UICONTROL 고급]** 탭.
1. 활성화 **[!UICONTROL 인증 요구 사항]**.

   ![사이트 인증](assets/site-authentication.png)

1. 로그인 페이지의 경로를 추가합니다. (예: `/content/......./GetStarted`)
1. 페이지를 게시합니다.

## 등록된 멤버 {#enrolled-member}

이 경험은 사용자에 의존합니다 `Riley Taylor` 및 `Sidney Croft` 계속 [생성됨](enablement-setup.md#publishcreateenablementmembers) 및 [할당됨](resource.md#settings) 변환 후 *스키 레슨* 에서 멤버십에 대한 학습 경로 *커뮤니티 스키 클래스* 그룹에 속해 있어야 합니다.

을 사용하여 로그인

* `Username: riley`
* `Password: password`

사용자 프로필이 자체 등록을 통해 생성되지 않은 경우, 구성원이 처음으로 로그인하면 해당 프로필 페이지가 표시되므로 필요한 경우 확인 및 수정할 수 있습니다.

다음에 구성원이 로그인하면 첫 번째 메뉴 항목으로 식별되는 홈 페이지가 표시됩니다.

![등록 멤버](assets/enrolled-member.png)

### 할당 {#assignments}

[지정] 페이지는 구성원이 특별히 지정된 모든 학습 경로 및 지원 리소스를 표시하는 페이지입니다.

각 할당에서는 다음과 같은 기본 정보를 제공합니다.

* 배정 유형
* 새 할당인지 여부
* 이름
* 발령 유형과 관련된 세부 정보
* 배정 담당자, 전문가 및 작성자(제공된 경우)

할당 유형은 카드의 왼쪽 위 모서리에 아이콘으로 표시됩니다. 로드 이미지는 포함된 지원 리소스 수가 있는 학습 경로를 위한 것입니다.

![assignment1](assets/assignment1.png)

선택 *스키 레슨* 학습 경로에서 참조하는 두 활성 리소스가 표시됩니다.

![assignment2](assets/assignment2.png)

선택 *스키 레슨 1* 사용 리소스의 세부 사항 페이지를 엽니다.

세부 사항 페이지에서 구성원은 다음과 같은 내용을 배울 수 있습니다. [비율](rating.md) 단원과 추가 [댓글](comments.md). 모든 멤버 활동이 사이트의 새로운 기능 섹션에 반영됩니다.

사용 리소스와 상호 작용은 작성 환경에서 액세스할 수 있는 보고서 섹션에 기록됩니다.

![assignment3](assets/assignment3.png)

### 스키 카탈로그 {#ski-catalog}

Ski Catalog 페이지는 의 태그가 지정된 지원 리소스의 카탈로그입니다 `Tutorial` 네임스페이스. 둘 *스키 레슨* 리소스에는 `Skiing` 태그 이외의 다른 태그가 있는 경우 `All` 또는 `Tutorial: Sports / Skiing` 이 선택되면 아무 것도 표시되지 않습니다.

구성원이 직접 또는 학습 경로를 통해 지원 리소스를 할당받지 않은 경우 카탈로그 내에 있는 지원 리소스와 상호 작용하고 주석 및 등급을 통해 피드백을 제공할 수 있습니다.

![스키 카탈로그](assets/ski-catalog.png)

### 토론 {#discussions}

지원 리소스에 대한 평가 및 주석 달기 외에도[활성화됨](enablement-create-site.md#step33asettings)), 사이트 템플릿 `Enablement Tutorial` 가 생성되면 [포럼 함수](functions.md#forum-function) (제목: `Discussions)`.

을(를) 선택합니다 `Discussions`항목을 연결 및 게시합니다.

로그인하여 Sidney Croft로 로그인하여(시드니 / 암호) 질문에 답하고, 이 항목을 따르세요.

인라인 중재 외에 소셜 미디어에서 주제를 공유하거나 항목을 이메일로 보내는 옵션이 있습니다.

![토론](assets/discussions.png)

### 새로운 기능 {#what-s-new}

다음 `What's New` 메뉴 항목은 [활동 스트림 함수](functions.md#activity-stream-function) 이 커뮤니티 사이트의 구조에 있습니다.

여전히 Sidney로 로그인되어 있는 경우 `What's New` 링크를 클릭하여 활동을 표시합니다.

![whats-new-menu](assets/whats-new-menu.png)

## 신뢰할 수 있는 커뮤니티 구성원 {#trusted-community-member}

이 경험은 ` [Quinn Harper](enablement-setup.md#publishcreateenablementmembers)` 의 역할이 할당되었습니다. [중재자](enablement-create-site.md#moderation) 및 [자원 연락처](resource.md#settings).

을 사용하여 로그인

* `Username: quinn`
* `Password: password`

로그인하면 새로운 메뉴 항목이 있습니다. `Administration`: 구성원에게 중재자 역할이 부여되었기 때문에 나타납니다.

![trusted-member-homepage](assets/trusted-member-homepage.png)

홈 페이지는 첫 번째 메뉴 항목 지정(지정)으로 식별됩니다. 퀸은 중재자 및 지원 리소스 연락처이며 지원 리소스 또는 학습 경로에 등록되어 있지 않으므로 표시할 항목이 없습니다.

### 관리 {#administration}

두 학습자의 활동이란 `Riley Taylor` 및 `Sidney Croft`. 을(를) 선택하여 `Administration` 조정 콘솔에 액세스하기 위해 링크를 클릭하면 [벌크 중재 콘솔](moderation.md) 게시물을 중재합니다.

사이드 패널 아이콘을 선택하면 커뮤니티 컨텐츠를 검색하는 데 사용되는 필터를 열 수 있습니다.

주석 카드 위로 마우스를 가져가면 중재 작업이 표시됩니다.

![관리](assets/administration.png)

## 작성자에 대한 보고서 {#reports-on-author}

학습자 및 지원 리소스에 대한 보고에 액세스하는 방법에는 두 가지가 있습니다.

작성자에서 다음 위치로 이동합니다 **커뮤니티, [리소스 콘솔](resources.md)**&#x200B;인 경우 지원 리소스를 관리하고 커뮤니티 사이트를 선택하면 보고서를 생성할 수 있습니다

* 모든 지원 리소스 및 학습 경로
* 특정 지원 리소스 또는 학습 경로 하나

로 이동합니다 **커뮤니티, [보고서 콘솔](reports.md)**&#x200B;및 를 사용하여 다음에 따라 보고서를 생성합니다.

* 지원 리소스 및 학습 경로에 할당
* 특정 기간 동안 커뮤니티 사이트에 게시물
* 특정 기간 동안의 커뮤니티 사이트 보기(사이트 방문)

* 게시물 및 보기는 모든 컨텐츠 또는 특정 컨텐츠에 해당될 수 있습니다.

   * 포럼
   * 포럼 주제
   * QnA
   * QnA 질문
   * 블로그
   * 블로그 항목
   * 달력
   * 달력 이벤트

### 리소스 콘솔 {#resources-console}

약간의 활동 및 게시용 리소스와 상호 작용만 있으면 작성자에 대한 보고서를 볼 수 있습니다.

* 작성자에서 관리 권한으로 로그인합니다.
* 기본 메뉴에서 다음으로 이동합니다 **[!UICONTROL 커뮤니티]** > **[!UICONTROL 리소스]**.
* 을(를) 선택합니다 `Enablement Tutorial` 사이트.
* 을(를) 선택합니다 `Report` 아이콘 을 클릭하여 모든 리소스를 요약할 수 있습니다.
* 리소스를 선택한 다음 `Report` 아이콘 사용)을 클릭하여 제품에서 사용할 수 있습니다.

표시되는 데 1~12시간이 걸릴 수 있는 Adobe Analytics의 데이터를 표시하기에는 너무 이른 것 같습니다. 그러나 기본 SCORM 보고는 이미 사용할 수 있습니다.

#### 스키 레슨 자원 보고서 {#ski-lessons-resource-report}

![스키 레슨 보고서](assets/ski-lessons-report.png)

#### 스키 레슨 사용 보고서 {#ski-lessons-user-report}

* 선택 **[!UICONTROL 커뮤니티 > 리소스]**

* 카드 열기 `Enablement Tutorial`
* 카드 열기 `Ski Lessons`
* 선택 `Report > User Report`

![스키레슨-사용자 보고서](assets/ski-lessons-user-report.png)

### 보고서 콘솔 {#reports-console}

보고서 콘솔을 사용하면

* **지정** 사용 가능한 모든 커뮤니티 사이트
* **보기 횟수** 모든 커뮤니티 사이트
* **게시물** 모든 커뮤니티 사이트

발령에 대한 보고서의 경우

* 작성자에서 관리 권한으로 로그인합니다.
* 다음으로 이동 **[!UICONTROL 커뮤니티]** > **[!UICONTROL 보고서]** > **[!UICONTROL 지정 보고서]**.
* 선택 **[!UICONTROL 사이트]** 풀다운 메뉴에서 `Enablement Tutorial`).

* 선택 **[!UICONTROL 그룹]** (선택) `Community Ski Class`)

* 선택 **[!UICONTROL 배정]** (선택) `Ski Lessons`)

* 선택 **[!UICONTROL 생성]**

![보고서 지정](assets/report-assignment.png)

보기에 대한 보고서의 경우:

* 작성자에서 관리 권한으로 로그인합니다.
* 다음으로 이동 **[!UICONTROL 커뮤니티]** > **[!UICONTROL 보고서]** > **[!UICONTROL 보기 보고서]**.
* 선택 **사이트** 풀다운 메뉴에서 `Enablement Tutorial`).

* 선택 **[!UICONTROL 컨텐츠 유형]** (선택) `all`).

* 선택 **[!UICONTROL 날짜 범위]** (선택) `Last 7 days`).

* 선택 **[!UICONTROL 생성]**.

![보고서 보기 수](assets/report-views.png)

**[⇐ 지원 리소스 만들기 및 할당](resource.md)**
