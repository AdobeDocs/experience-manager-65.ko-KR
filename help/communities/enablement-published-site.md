---
title: 게시된 사이트 경험
seo-title: 게시된 사이트 경험
description: 활성화를 위해 게시된 사이트 찾아보기
seo-description: 활성화를 위해 게시된 사이트 찾아보기
uuid: 1bfefa8a-fd9c-4ca8-b2ff-add79776c8ae
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 26715b94-e2ea-4da7-a0e2-3e5a367ac1cd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---



# 게시된 사이트 경험 {#experience-the-published-site}


**[활성 ⇐ 리소스 만들기 및 할당](resource.md)**

## 게시 시 새 사이트 찾아보기 {#browse-to-new-site-on-publish}

새로 만든 커뮤니티 사이트와 역량 강화 리소스 및 학습 경로가 게시되었으므로 지원 자습서 사이트를 경험할 수 있습니다.

먼저 사이트를 만들 때 표시되는 URL을 탐색하고 게시 서버(예:

* 작성자 URL = [http://localhost:4502/content/sites/enable/en.html](http://localhost:4502/content/sites/enable/en.html)
* 게시 URL = [http://localhost:4503/content/sites/enable/en.html](http://localhost:4503/content/sites/enable/en.html)

기본 홈 페이지가 설정된 [경우 http://localhost:4503/](enablement-create-site.md#changethedefaulthomepage)에서 [사이트를](http://localhost:4503/) 탐색하면 됩니다.

게시된 사이트에 처음 도달하면 사이트 방문자는 일반적으로 로그인되지 않고 익명으로 방문됩니다.

**http://localhost:4503/content/sites/enable/en.html**

![chlimage_1-432](assets/chlimage_1-433.png)

## 익명의 사이트 방문자 {#anonymous-site-visitor}

익명의 사이트 방문자는 이 비공개 활성 커뮤니티 사이트에 대한 로그인 페이지가 즉시 표시됩니다. Facebook 또는 Twitter에 직접 등록하거나 로그인할 수 있는 옵션은 없습니다.

이 홈 페이지에는 다음 네 가지 메뉴 항목이 표시됩니다.로그인 `Assignments, Ski Catalog, What's New` 없이는 연결할 수 `Discussions`없습니다.

>[!NOTE]
>
>사이트 방문자가 직접 등록할 수 없도록 하지 않고 활성 사이트에 대한 익명 액세스 권한을 부여할 수 있습니다.
>활성 리소스가 로 설정되어 `show in catalog` 있는 `allow anonymous access`경우 익명 사이트 방문자가 카탈로그의 리소스를 볼 수 있습니다.

### JCR에서 익명 액세스 차단 {#prevent-anonymous-access-on-jcr}

알려진 제한은 사이트 컨텐츠에 대해 익명 액세스를 **[!UICONTROL 허용하지만 jcr 컨텐츠 및 json을 통해 커뮤니티 사이트 컨텐츠를 익명의 방문자에게 노출합니다]** . 그러나 이 동작은 [스링 제한]을 사용하여 해결할 수 있습니다.

jcr 컨텐츠 및 json을 통해 익명의 사용자가 커뮤니티 사이트의 컨텐츠를 액세스하지 못하도록 보호하려면 다음 단계를 따르십시오.

1. AEM 작성자 인스턴스에서 https://&lt;host>:&lt;port>/editor.html/content/site/&lt;sitename>.html로 이동합니다.

   >[!NOTE]
   >
   >현지화된 사이트로 이동하지 마십시오.

1. 페이지 **[!UICONTROL 속성으로 이동합니다]**.

   ![page-properties-1](assets/page-properties-1.png)

1. 고급 **[!UICONTROL 탭으로]** 이동합니다.
1. Enable **[!UICONTROL Authentication Requirement]**.

   ![site-authentication-1](assets/site-authentication-1.png)

1. 로그인 페이지의 경로를 추가합니다. 예, `/content/......./GetStarted`.
1. 페이지를 게시합니다.

## 등록된 회원 {#enrolled-member}

이 경험은 Ski Lessons `Riley Taylor` 를 만들고 `Sidney Croft`[Ski LessonsLearning Path를](enablement-setup.md#publishcreateenablementmembers) 만들고 [Companies Ski Class CommunityGroup의 멤버십을 통해 사용자에게](resource.md#settings) 할당되는 ** ** 것에 의존합니다.

다음으로 로그인

* `Username: riley`
* `Password: password`

사용자 프로필이 직접 등록을 통해 만들어지지 않은 경우, 멤버가 처음 로그인하면 프로필 페이지가 표시되어 필요에 따라 확인하고 수정할 수 있습니다.

다음에 멤버가 로그인하면 첫 번째 메뉴 항목으로 식별되는 홈 페이지가 표시됩니다.

![chlimage_1-434](assets/chlimage_1-434.png)

### 할당 {#assignments}

[할당] 페이지는 멤버가 특별히 할당된 모든 학습 경로 및 활성 리소스를 표시하는 페이지입니다.

각 할당은 에 대한 기본 정보를 제공합니다.

* 할당 유형
* 새 할당인지 여부
* 이름
* 지정 유형과 관련된 세부 사항
* 담당자, 전문가 및 작성자(제공된 경우) 할당

할당의 유형은 카드의 왼쪽 상단에 있는 아이콘으로 표시됩니다. 로드의 이미지는 포함된 활성 리소스 수가 있는 학습 경로를 위한 것입니다.

![chlimage_1-435](assets/chlimage_1-435.png)

스키 *레슨을* 선택하면 학습 경로에서 참조하는 두 가지 활성 리소스가 표시됩니다.

![chlimage_1-436](assets/chlimage_1-436.png)

스키 *레슨 1을* 선택하면 활성 리소스의 세부 정보 페이지가 열립니다.

세부 사항 페이지에서 회원은 학습, 강의 [평가](rating.md) 및 [주석을](comments.md)추가할 수 있습니다. 모든 회원 활동은 사이트의 새로운 기능 섹션에 반영됩니다.

활성 리소스와의 상호 작용은 작성 환경에서 액세스할 수 있는 보고서 섹션에 설명되어 있습니다.

![chlimage_1-437](assets/chlimage_1-437.png)

### 스키 카탈로그 {#ski-catalog}

[스키 카탈로그] 페이지는 `Tutorial` 네임스페이스의 태그가 지정된 활성 리소스 카탈로그입니다. 두 *가지 스키* 레슨 `Skiing` 리소스에는 `All` 태그가 지정되어 있으므로 다른 태그가 `Tutorial: Sports / Skiing` 또는 선택되어있으면 아무 것도 표시되지 않습니다.

멤버가 직접 또는 학습 경로를 통해 역량 강화 리소스가 할당되지 않은 경우 카탈로그 내에 있는 활성 리소스와 상호 작용하고 의견 및 등급을 통해 피드백을 제공할 수 있습니다.

![chlimage_1-438](assets/chlimage_1-438.png)

### 토론 {#discussions}

역량 강화 리소스([활성화](enablement-create-site.md#step33asettings)시)에 대한 등급 및 주석 달기 외에 `Enablement Tutorial` 만들어진 커뮤니티 사이트 템플릿에는 [포럼 기능](functions.md#forum-function) (제목이 `Discussions)`포함됩니다.

링크를 `Discussions`선택하고 항목을 게시합니다.

로그아웃 및 Sidney Croft로 로그인하여 질문에 답하고, 항목을 팔로우하십시오.

인라인 중재 외에도 소셜 미디어에서 항목을 공유하거나 항목을 이메일로 보내는 옵션이 있습니다.

![chlimage_1-439](assets/chlimage_1-439.png)

### 새로운 기능 {#what-s-new}

메뉴 `What's New` 항목은 이 커뮤니티 사이트 구조에서 [활동 스트림 기능이](functions.md#activity-stream-function) 제공된 제목입니다.

여전히 Sidney로 로그인되어 있는 경우 활동을 표시할 `What's New` 링크를 선택합니다.

![chlimage_1-440](assets/chlimage_1-440.png)

## 신뢰할 수 있는 커뮤니티 구성원 {#trusted-community-member}

이 경험에서는 중재자 ` [Quinn Harper](enablement-setup.md#publishcreateenablementmembers)` 및 [리소스 연락처의](enablement-create-site.md#moderation) [](resource.md#settings)역할이 할당되었다고 가정합니다.

다음으로 로그인

* `Username: quinn`
* `Password: password`

로그인하면 새로운 메뉴 항목이 `Administration`있는데, 이는 멤버가 중재자의 역할을 했기 때문입니다.

![chlimage_1-441](assets/chlimage_1-441.png)

홈 페이지는 첫 번째 메뉴 항목인 할당으로 식별됩니다. Quinn은 중재자 및 역량 강화 리소스 담당자이고 활성 리소스 또는 학습 경로에 등록되어 있지 않으므로 표시할 항목이 없습니다.

### 관리 {#administration}

두 명의 학습자의 활동, 중재 콘솔에 액세스할 수 있는 `Riley Taylor` 링크 `Sidney Croft. By s`선택, Quinn은 `Administration`일괄 중재 콘솔을 [사용하여 게시물을 중재할 수 있습니다](moderation.md) .

사이드 패널 아이콘을 선택하면 커뮤니티 컨텐츠를 검색하는 데 사용되는 필터가 열립니다.

댓글 카드 위로 마우스를 가져가면 중재 작업이 표시됩니다.

![chlimage_1-442](assets/chlimage_1-442.png)

## 작성자에 대한 보고서 {#reports-on-author}

수강생 및 역량 강화 리소스에 대한 보고에 액세스하는 방법에는 두 가지가 있습니다.

작성자는 커뮤니티, **리소스[콘솔로](resources.md)**이동하여 활성 리소스를 관리하고 커뮤니티 사이트를 선택한 후

* 모든 역량 강화 리소스 및 학습 경로
* 특정 역량 강화 리소스 또는 학습 경로

커뮤니티, **보고서[콘솔로](reports.md)**이동하고

* 역량 강화 리소스 및 학습 경로 지정
* 특정 기간 동안 커뮤니티 사이트에 게시물 게시
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

게시 중인 리소스와 약간의 활동 및 상호 작용을 통해 작성자에 대한 보고서를 보는 것은 그만한 가치가 있습니다.

* 작성자
* 관리자 권한으로 로그인
* 주 메뉴에서 커뮤니티 > **[!UICONTROL 리소스로 이동합니다.]**
* 사이트 `Enablement Tutorial` 선택
* 모든 리소스의 요약 `Report`아이콘을 선택합니다.
* 리소스를 선택한 다음 해당 리소스에 대한 보고서의 `Report`아이콘을 선택합니다.

Adobe Analytics의 데이터를 표시하기에는 너무 이르며, 이 데이터는 1~12시간이 걸릴 수 있습니다. 그러나 기본 SCORM 보고는 이미 사용할 수 있습니다.

#### 스키 강의 리소스 보고서 {#ski-lessons-resource-report}

![chlimage_1-443](assets/chlimage_1-443.png)

#### 스키 강의 사용자 보고서 {#ski-lessons-user-report}

* 커뮤니티 **[!UICONTROL > 리소스 선택]**

* 카드 열기 `Enablement Tutorial`
* 카드 열기 `Ski Lessons`
* `select Report, User Report`

![chlimage_1-444](assets/chlimage_1-444.png)

### 보고서 콘솔 {#reports-console}

보고서 콘솔에서는

* **모든 역량 강화** 커뮤니티 사이트에 대한 할당
* **모든** 커뮤니티 사이트 보기
* **모든** 커뮤니티 사이트에 대한 게시물

할당에 대한 보고서의 경우:

* 작성자
* 관리자 권한으로 로그인
* 커뮤니티 > **[!UICONTROL 보고서 > 할당 보고서로 이동합니다.]**
* 풀다운 **[!UICONTROL 메뉴에서]** 사이트 선택(선택 `Enablement Tutorial`)

* 그룹 **[!UICONTROL 선택]** (선택 `Community Ski Class`)

* 할당 **[!UICONTROL 선택]** (선택 `Ski Lessons`)

* 생성 **[!UICONTROL 선택]**

![chlimage_1-445](assets/chlimage_1-445.png)

보기에 대한 보고서의 경우:

* 작성자
* 관리자 권한으로 로그인
* 커뮤니티 > **[!UICONTROL 보고서 > 보기 보고서로 이동합니다.]**
* 풀다운 **메뉴에서&#x200B;**사이트 선택(선택`Enablement Tutorial`)

* 컨텐츠 **[!UICONTROL 유형]** 선택(선택 `all`)

* **[!UICONTROL 날짜 범위]** 선택(선택 `Last 7 days`)

* 생성 **[!UICONTROL 선택]**

![chlimage_1-446](assets/chlimage_1-446.png)

**[활성 ⇐ 리소스 만들기 및 할당](resource.md)**
