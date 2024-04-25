---
title: 리뷰 및 리뷰 요약 사용(표시)
description: 리뷰 및 리뷰 요약 구성 요소를 페이지에 추가하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 170414a6-c40b-4ad2-9294-7c2266850c3d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 0%

---

# 리뷰 및 리뷰 요약 사용(표시) {#using-reviews-and-reviews-summary-display}

다음 `Reviews` 구성 요소가 [댓글](comments.md) 및 [등급](rating.md) 사용할 준비가 된 구성 요소입니다.

다음 `Reviews Summary (Display)` 구성 요소는 의 활성 또는 닫힌 인스턴스에 대한 요약을 제공합니다. `Reviews` 사이트의 다른 위치에 표시할 구성 요소입니다.

>[!NOTE]
>
>검토의 익명 게시는 지원되지 않습니다. 사이트 방문자가 참여하려면 등록(회원 가입)하고 로그인해야 합니다. 로그인한 방문자는 언제든지 리뷰를 업데이트할 수 있습니다.

## 페이지에 검토 추가 {#adding-a-review-to-a-page}

을(를) 추가하려면 `Reviews` 구성 요소를 페이지에 추가하려면 작성자 모드에서 구성 요소 브라우저를 사용하여 `Communities / Reviews` 를 드래그하여 사용자가 검토할 수 있는 기능에 상대적인 위치와 같은 페이지에 배치합니다.

필요한 정보는 다음을 참조하십시오. [커뮤니티 구성 요소 기본 사항](basics.md).

다음의 경우 [필수 클라이언트측 라이브러리](reviews-basics.md#essentials-for-client-side) 포함됩니다. 이렇게 하면 `Reviews` 구성 요소가 표시됩니다.

![create-review](assets/create-review.png)

## 리뷰 구성 {#configuring-reviews}

배치된 을(를) 선택합니다 `Reviews` 에 액세스하고 선택할 수 있는 구성 요소 `Configure` 편집 대화 상자를 여는 아이콘.

![새로 구성](assets/configure-new.png)

아래 **[!UICONTROL 허용된 등급]** 탭에서 구성원에게 표시할 전체 등급 목록을 지정합니다. 첫 번째 등급은 의 평균 등급을 제공하는 등급이므로 전체/일반 등급이어야 합니다. `Review Summary (Display)` 구성 요소. 기본 구성의 다음 두 등급에는 &quot;Subrating 1&quot; 또는 &quot;Subrating 2&quot; 이외의 다른 제목을 지정해야 합니다.

![허용 등급](assets/configure-review1.png)

* **[!UICONTROL 허용된 등급]**

  구성원이 선택할 수 있는 등급 목록입니다.

  위쪽 화살표, 아래쪽 화살표 및 삭제 버튼을 사용하여 표시되는 선택 사항을 수정합니다.

  클릭 **[!UICONTROL 항목 추가]** 다른 등급 선택을 추가합니다.

아래 **[!UICONTROL 필수 등급]** 탭, 목록에서 항목 재입력 **[!UICONTROL 허용된 등급]** 등급 지정에 필요합니다. 항목이 허용된 등급 탭에만 지정되는 경우 구성원이 제출했을 때 표시 해제될 수 있습니다.

웹 사이트에서 필수 등급은 별표로 표시됩니다. 항목이 필수이고 표시 해제된 상태로 남아 있는 경우 구성원에게 메시지가 표시되고 필요한 모든 등급이 표시될 때까지 제출이 거부됩니다.

![필수 등급](assets/configure-review2.png)

* **[!UICONTROL 필수 등급]**

  필요한 등급을 나타내는 허용된 등급의 하위 집합입니다.

  위쪽 화살표, 아래쪽 화살표 및 삭제 버튼을 사용하여 표시되는 선택 사항을 수정합니다.

  클릭 **[!UICONTROL 항목 추가]** 다른 응답 선택을 추가합니다.

>[!NOTE]
>
>항목을 입력한 경우 **[!UICONTROL 필수 등급]** 에 지정되지 않은 탭 **[!UICONTROL 허용된 등급]** 탭으로 설정하면 평가할 항목에 포함되지 않습니다.

아래 **[!UICONTROL 리뷰]** 탭에서 검토 처리 방법을 지정합니다.

![리뷰](assets/configure-review3.png)

* **[!UICONTROL 답변 허용]**

  선택하면 리뷰에 답글을 허용합니다. 기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 종료됨]**

  선택하면 검토는 새 검토 및 답글로 닫힙니다. 기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 파일 업로드 허용]**

  선택하면 검토를 위해 첨부 파일을 업로드할 수 있습니다. 기본값은 선택 취소되어 있습니다.

* **최대 파일 크기**

  다음과 같은 경우에만 관련됨 **[!UICONTROL 파일 업로드 허용]** 이(가) 선택되었습니다. 이 필드는 업로드된 파일의 크기(바이트)를 제한합니다. 기본값은 10MB입니다.

* **[!UICONTROL 최대 메시지 길이]**

  텍스트 상자에 입력할 수 있는 최대 문자 수. 기본값은 4096자입니다.

* **[!UICONTROL 허용되는 파일 유형]**

  다음과 같은 경우에만 관련됨 **[!UICONTROL 파일 업로드 허용]** 이(가) 선택되었습니다. &quot;점&quot; 구분 기호가 있는 쉼표로 구분된 파일 확장자 목록입니다. 예: .jpg, .jpeg, .png, .doc, .docx, .pdf 파일 유형을 지정하면 지정하지 않은 파일 유형은 허용되지 않습니다. 기본값은 모든 파일 형식이 허용되도록 지정되지 않습니다.

* **[!UICONTROL 리치 텍스트 편집기]**

  선택하면 게시물에 마크업을 입력할 수 있습니다. 기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 투표 허용]**

  선택하는 경우 주제에 대한 투표 기능을 포함합니다. 기본값은 선택 취소되어 있습니다.

아래 **[!UICONTROL 사용자 중재]** 탭에서 게시된 리뷰를 관리하는 방법을 지정합니다. 자세한 내용은 [사용자 생성 컨텐츠 중재](moderate-ugc.md).

![user-moderation](assets/configure-review4.png)

* **[!UICONTROL 사전 중재]**

  선택하면 게시 사이트에 표시되기 전에 검토를 승인해야 합니다. 기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 리뷰 삭제]**

  선택하면 리뷰를 게시한 회원이 삭제할 수 있습니다. 기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 리뷰 거부]**

  선택하면 중재자의 리뷰 거부 허용. 기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 리뷰 닫기 / 다시 열기]**

  선택하면 중재자가 리뷰를 닫았다가 다시 열 수 있습니다. 기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 리뷰 플래그 지정]**

  선택하면 구성원이 리뷰를 부적절한 항목으로 표시하도록 허용합니다. 기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 플래그 이유 목록]**

  선택하면 멤버가 드롭다운 목록에서 검토를 부적절한 항목으로 플래그를 지정하는 이유를 선택할 수 있습니다. 기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 사용자 지정 플래그 이유]**

  선택하면 멤버가 검토 플래그 지정에 대한 자신의 이유를 부적절한 항목으로 입력할 수 있습니다. 기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 중재 임계값]**

  중재자에게 통지하기 전에 구성원이 리뷰에 플래그를 지정해야 하는 횟수를 입력합니다. 기본값은 1회입니다.

* **[!UICONTROL 플래그 지정 제한]**

  공개 보기에서 숨겨지기 전에 검토에 플래그를 지정해야 하는 횟수를 입력합니다. 이 숫자는 보다 크거나 같아야 합니다. **[!UICONTROL 중재 임계값]**. 기본값은 5입니다.

### 페이지에 검토 요약(표시) 추가 {#adding-a-review-summary-display-to-a-page}

을(를) 추가하려면 `Reviews Summary (Display)` 구성 요소를 페이지에 추가하려면 작성자 모드에서 구성 요소를 찾습니다.

* `Communities / Reviews Summary (Display)`

그리고 현재 검토 또는 종료된 검토의 요약이 표시될 페이지로 드래그합니다.

필요한 정보는 다음을 참조하십시오. [커뮤니티 구성 요소 기본 사항](basics.md).

다음의 경우 [필수 클라이언트측 라이브러리](reviews-basics.md#essentials-for-client-side) 포함됩니다. 이렇게 하면 `Reviews Summary (Display)`구성 요소가 표시됩니다.

![review-요약](assets/configure-review5.png)

>[!NOTE]
>
>&quot;평균&quot;은 요약되고 있는 검토의 허용된 등급 탭에 나열된 첫 번째 항목에 대한 투표를 반영합니다.

### 리뷰 구성 요약(표시) {#configuring-reviews-summary-display}

배치된 을(를) 선택합니다 `Reviews Summary (Display)` 에 액세스하고 선택할 수 있는 구성 요소 `Configure` 편집 대화 상자를 여는 아이콘.

![구성](assets/configure-new.png)

아래 **[!UICONTROL 리뷰 요약]** 탭

![review-요약](assets/configure-review6.png)

* `Review Path`

  의 배치된 인스턴스를 입력하거나 찾습니다. `reviews` 예를 들어 의 웹 페이지에 가 추가된 경우 요약할 수 있는 구성 요소 [Geometrixx 참여 사이트,](getting-started.md) 경로는 다음과 같습니다.

  `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

  선택하는 경우, 요약되는 리뷰에 별 등급이 몇 개나 있는지를 나타내는 막대 그래프 표시를 포함합니다. 기본값은 선택 취소되어 있습니다.

### 사용자 정의 검토 유형으로 변경 {#changing-to-a-custom-review-type}

리뷰 구성 요소는 댓글 시스템 을 사용합니다.

주석 리소스 유형을 변경하면 주석 시스템은 더 이상 기본값을 사용하여 주석 인스턴스를 생성하지 않고 개발자가 사용자 지정(확장)한 주석 인스턴스를 생성합니다.

사용자 지정 리소스 유형을 알고 있는 경우 다음을 입력합니다. [디자인 모드](../../help/sites-authoring/default-components-designmode.md) 배치된 을 두 번 클릭합니다. `Comments` 추가 탭이 있는 대화 상자를 여는 구성 요소.

아래 **[!UICONTROL 리소스 유형]** 탭에서 새 인스턴스의 사용자 지정 resourceType을 `Comments or Voting` 구성 요소:

![의견 투표](assets/configure-review7.png)

* **[!UICONTROL 댓글 리소스 유형]**

  확장의 resourceType으로 이동 `comment`/apps의 구성 요소(단일 댓글)입니다. 예: `/apps/social/commons/components/hbs/comments/comment`

  이 리소스는 방문자가 댓글을 게시할 때 생성된 UGC의 resourceType을 식별합니다.

* **[!UICONTROL 투표 리소스 유형]**

  확장의 resourceType으로 이동 `voting`/apps의 구성 요소입니다. 예: `/apps/social/components/hbs/voting`

  이 리소스는 방문자가 투표를 게시할 때 만든 UGC의 리소스 유형을 식별합니다.

* **[!UICONTROL 주석 시스템 리소스 유형]**

  확장의 resourceType으로 이동 `comments`/apps의 구성 요소(댓글 시스템). 페이지 템플릿이 아니면 비워 둡니다. [동적으로 포함](scf.md#add-or-include-a-communities-component) 페이지에 리소스(댓글 노드)로 추가되지 않고 기본 스크립트의 댓글 시스템. 자세한 내용은 다음을 참조하십시오. [`{{include}}` 도우미](handlebars-helpers.md#include).

## 사이트 방문자 경험 {#site-visitor-experience}

### 중재자 및 관리자 {#moderators-and-administrators}

로그인한 사용자에게 중재자 또는 관리자 권한이 있는 경우 검토 작성자에 관계없이 구성 요소의 구성에서 허용하는 중재 작업을 수행할 수 있습니다.

### 구성원 {#members}

사이트 방문자가 로그인하면 구성에 따라 다음과 같은 작업을 수행할 수 있습니다.

* 새 리뷰 게시
* 자체 리뷰 편집
* 자신의 리뷰 삭제
* 다른 사람의 리뷰 댓글에 플래그 지정

구성원당 하나의 등급만 허용됩니다. 회원은 언제든지 등급을 변경할 수 있습니다.

### 익명 {#anonymous}

로그인하지 않은 사이트 방문자는 게시된 리뷰를 읽고, 지원되는 경우 번역만 할 수 있지만 평점 또는 리뷰를 추가하거나 다른 방문자의 리뷰 댓글에 플래그를 지정할 수는 없습니다.

## 추가 정보 {#additional-information}

자세한 내용은 [Essentials 검토](reviews-basics.md) 개발자용 페이지입니다.

게시한 댓글의 중재에 대해서는 [사용자 생성 컨텐츠 중재](moderate-ugc.md).

게시된 댓글의 번역은 다음을 참조하십시오. [사용자 생성 콘텐츠 번역](translate-ugc.md).
