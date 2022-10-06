---
title: 검토 및 검토 요약 사용(표시)
seo-title: Using Reviews and Reviews Summary (Display)
description: 페이지에 검토 및 검토 요약 구성 요소 추가
seo-description: Adding the Reviews and Reviews Summary components to a page
uuid: bd1ccee7-b26b-4a27-b1ea-89609f5080af
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: bf4e7809-8def-4647-aaa6-3ac36865511f
exl-id: 170414a6-c40b-4ad2-9294-7c2266850c3d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 3%

---

# 검토 및 검토 요약 사용(표시) {#using-reviews-and-reviews-summary-display}

다음 `Reviews` 구성 요소는 [댓글](comments.md) 및 [등급](rating.md) 구성 요소를 사용할 수 있습니다.

다음 `Reviews Summary (Display)` 구성 요소는 의 활성 또는 닫힌 인스턴스에 대한 요약을 제공합니다 `Reviews` 구성 요소를 사용하여 사이트의 다른 곳에 표시됩니다.

>[!NOTE]
>
>검토의 익명 게시는 지원되지 않습니다. 사이트 방문자는 등록(구성원 자격)하고 로그인해야 참여합니다. 로그인한 방문자는 언제든지 검토를 업데이트할 수 있습니다.

## 페이지에 검토 추가 {#adding-a-review-to-a-page}

을(를) 추가하려면 `Reviews` 구성 요소를 페이지에 작성자 모드에서 사용하려면 구성 요소 브라우저를 사용하여 를 찾습니다 `Communities / Reviews` 사용자가 검토할 기능을 기준으로 하는 위치와 같이 페이지에 드래그합니다.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](basics.md).

이 [필수 클라이언트 측 라이브러리](reviews-basics.md#essentials-for-client-side) 포함된 경우, 다음과 같이 하십시오 `Reviews` 구성 요소가 나타납니다.

![만들기 검토](assets/create-review.png)

## 검토 구성 {#configuring-reviews}

배치된 항목을 선택합니다 `Reviews` 액세스하여 선택할 구성 요소 `Configure` 아이콘 편집 대화 상자를 엽니다.

![configure-new](assets/configure-new.png)

아래에 **[!UICONTROL 허용된 등급]** 탭에서 구성원에게 표시할 전체 등급 목록을 지정합니다. 첫 번째 등급은 의 평균 등급을 제공하는 등급이므로 전체/일반 등급이어야 합니다 `Review Summary (Display)` 구성 요소. 기본 구성의 다음 두 등급에는 &quot;1위&quot; 또는 &quot;2위&quot; 이외의 다른 제목이 지정됩니다.

![허용 등급](assets/configure-review1.png)

* **[!UICONTROL 허용된 등급]**

   구성원이 선택할 수 있는 등급 목록입니다.

   위쪽 화살표, 아래쪽 화살표 및 삭제 단추를 사용하여 표시되는 선택 사항을 수정합니다.

   클릭 **[!UICONTROL 항목 추가]** 다른 등급 선택을 추가합니다.

아래에 **[!UICONTROL 필요한 등급]** 탭에서 다음 목록의 항목을 다시 입력합니다 **[!UICONTROL 허용된 등급]** 그것은 정격 되어야 한다. 항목이 허용된 등급 탭에서만 지정된 경우 구성원이 제출한 경우 표시되지 않은 상태로 둘 수 있습니다.

웹 사이트에서는 필수 등급이 별표로 표시됩니다. 항목이 필수 항목이고 표시 안 함을 남겨두면 구성원에게 메시지가 표시되고 필요한 등급을 모두 표시할 때까지 제출이 거부됩니다.

![필수 등급](assets/configure-review2.png)

* **[!UICONTROL 필수 등급]**

   필요한 등급을 나타내는 허용된 등급의 하위 집합입니다.

   위쪽 화살표, 아래쪽 화살표 및 삭제 단추를 사용하여 표시되는 선택 사항을 수정합니다.

   클릭 **[!UICONTROL 항목 추가]** 다른 응답 선택을 추가합니다.

>[!NOTE]
>
>항목이 **[!UICONTROL 필요한 등급]** 탭에서 지정되지 않은 탭 **[!UICONTROL 허용된 등급]** 탭한 다음, 계산할 항목에 포함되지 않습니다.

아래에 **[!UICONTROL 검토]** 탭에서 검토 처리 방법을 지정합니다.

![리뷰 수](assets/configure-review3.png)

* **[!UICONTROL 답글 허용]**

   이 옵션을 선택하면 답글을 검토하도록 허용합니다. 기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 닫힘]**

   이 옵션을 선택하면 검토가 닫히고 새 검토 및 답글이 표시됩니다. 기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 파일 업로드 허용]**

   이 옵션을 선택하면 검토를 위해 첨부 파일을 업로드할 수 있습니다. 기본값은 선택 취소되어 있습니다.

* **최대 파일 크기**

   관련성이 있는 경우에만 **[!UICONTROL 파일 업로드 허용]** 이(가) 선택되어 있습니다. 이 필드는 업로드된 파일의 크기(바이트)를 제한합니다. 기본값은 10MB입니다.

* **[!UICONTROL 최대 메시지 길이]**

   텍스트 상자에 입력할 수 있는 최대 문자 수입니다. 기본값은 4096자입니다.

* **[!UICONTROL 허용되는 파일 유형]**

   관련성이 있는 경우에만 **[!UICONTROL 파일 업로드 허용]** 이(가) 선택되어 있습니다. 점이 구분되어 있는 쉼표로 구분된 파일 확장자 목록입니다. 예: .jpg, .jpeg, .png, .doc, .docx, .pdf 파일 유형을 지정하면 지정되지 않은 파일 유형이 허용되지 않습니다. 기본값은 지정되지 않아서 모든 파일 유형이 허용됩니다.

* **[!UICONTROL 리치 텍스트 편집기]**

   이 확인란을 선택하면 게시물에 마크업이 있을 수 있습니다. 기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 투표 허용]**

   이 옵션을 선택하면 항목의 투표 기능을 포함합니다. 기본값은 선택 취소되어 있습니다.

아래에 **[!UICONTROL 사용자 중재]** 탭에서 게시된 검토 관리 방법을 지정합니다. 자세한 내용은 [사용자가 생성한 컨텐츠 중재](moderate-ugc.md).

![user-moderation](assets/configure-review4.png)

* **[!UICONTROL 사전 관리]**

   이 확인란을 선택하면 게시 사이트에 표시되기 전에 검토를 승인해야 합니다. 기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 리뷰 삭제]**

   이 옵션을 선택하면 리뷰를 게시한 멤버가 리뷰를 삭제할 수 있습니다. 기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 리뷰 거부]**

   이 확인란을 선택하면 중재자가 검토를 거부할 수 있습니다. 기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 리뷰 닫기/다시 열기]**

   이 옵션을 선택하면 중재자가 검토를 닫고 다시 열 수 있습니다. 기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 리뷰 플래그 지정]**

   이 옵션을 선택하면 구성원이 검토를 부적절한 것으로 플래그를 지정할 수 있습니다. 기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 플래그 이유 목록]**

   이 옵션을 선택하면 구성원이 드롭다운 목록에서 검토를 선택해야 합니다. 검토 플래그 지정은 부적절합니다. 기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 사용자 지정 플래그 이유]**

   이(가) 선택된 경우, 구성원이 검토 결과를 부적절한 것으로 표시할 고유한 사유를 입력할 수 있도록 허용합니다. 기본값은 선택 취소되어 있습니다.

* **[!UICONTROL 관리 임계값]**

   중재자에게 통지하기 전에 구성원이 검토에 플래그를 지정해야 하는 횟수를 입력합니다. 기본값은 1회(1)입니다.

* **[!UICONTROL 플래그 지정 제한]**

   검토가 공개 보기에서 숨겨지기 전에 플래그를 지정해야 하는 횟수를 입력합니다. 이 숫자는 다음보다 크거나 같아야 합니다 **[!UICONTROL 중재 임계값]**. 기본값은 5입니다.

### 페이지에 검토 요약(표시) 추가 {#adding-a-review-summary-display-to-a-page}

을(를) 추가하려면 `Reviews Summary (Display)` 구성 요소를 페이지에 작성자 모드에서 찾아 구성 요소를 찾습니다

* `Communities / Reviews Summary (Display)`

활성 검토나 닫힌 검토의 요약이 표시되는 페이지로 끌어서 놓습니다.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](basics.md).

이 [필수 클라이언트 측 라이브러리](reviews-basics.md#essentials-for-client-side) 포함된 경우, 다음과 같이 하십시오 `Reviews Summary (Display)`구성 요소가 나타납니다.

![검토 요약](assets/configure-review5.png)

>[!NOTE]
>
>&quot;평균&quot;은 요약되는 검토의 허용된 등급 탭에 나열된 첫 번째 항목에 대한 투표를 반영합니다.

### 검토 요약 구성(표시) {#configuring-reviews-summary-display}

배치된 항목을 선택합니다 `Reviews Summary (Display)` 액세스하여 선택할 구성 요소 `Configure` 아이콘 편집 대화 상자를 엽니다.

![구성](assets/configure-new.png)

아래에 **[!UICONTROL 검토 요약]** 탭

![검토 요약](assets/configure-review6.png)

* `Review Path`

   의 배치된 인스턴스를 입력하거나 찾아봅니다. `reviews`요약할 구성 요소입니다(예: [Geometrixx 참여 사이트,](getting-started.md) 경로는 다음과 같습니다.

   `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

   이 확인란을 선택하면 요약 중인 검토에 있는 각 별 등급 수를 나타내는 막대 그래프의 표시를 포함합니다. 기본값은 선택 취소되어 있습니다.

### 사용자 지정 검토 유형으로 변경 {#changing-to-a-custom-review-type}

검토 구성 요소는 댓글 시스템을 사용합니다.

주석 리소스 유형을 변경하면 주석 시스템은 더 이상 기본값을 사용하여 주석의 인스턴스를 생성하지 않고 개발자가 사용자 지정(확장)한 인스턴스를 생성합니다.

사용자 정의 리소스 유형을 알려면 다음을 입력합니다. [디자인 모드](../../help/sites-authoring/default-components-designmode.md) 그리고 위치를 두 번 클릭합니다 `Comments` 추가 탭이 있는 대화 상자를 여는 구성 요소입니다.

아래에 **[!UICONTROL 리소스 유형]** 탭에서 `Comments or Voting` 구성 요소:

![댓글 투표](assets/configure-review7.png)

* **[!UICONTROL 댓글 리소스 유형]**

   확장의 resourceType으로 이동합니다. `comment`/apps 의 구성 요소(단일 주석)입니다. (예: `/apps/social/commons/components/hbs/comments/comment`)

   이 리소스는 방문자가 댓글을 게시할 때 생성된 UGC의 resourceType을 식별합니다.

* **[!UICONTROL 투표 리소스 유형]**

   확장의 resourceType으로 이동합니다. `voting`/apps의 구성 요소입니다. (예: `/apps/social/components/hbs/voting`)

   이 리소스는 방문자가 투표를 게시할 때 생성된 UGC의 리소스 유형을 식별합니다.

* **[!UICONTROL 댓글 시스템 리소스 유형]**

   확장의 resourceType으로 이동합니다. `comments`/apps 의 구성 요소(주석 시스템)입니다. 페이지 템플릿을 제외하고 비워 둡니다. [동적으로 포함](scf.md#add-or-include-a-communities-component) 페이지에 리소스(주석 노드)로 추가되지 않고, 기본 스크립트의 주석 시스템 을 사용하십시오. 자세한 내용은 [{{include}} 도우미](handlebars-helpers.md#include).

## 사이트 방문자 경험 {#site-visitor-experience}

### 중재자 및 관리자 {#moderators-and-administrators}

로그인한 사용자에게 중재자 또는 관리자 권한이 있는 경우 검토를 작성한 사람에 관계없이 구성 요소의 구성에서 허용하는 중재 작업을 수행할 수 있습니다.

### 구성원 {#members}

사이트 방문자가 로그인하면 구성에 따라 다음 경우가 발생할 수 있습니다.

* 새 검토 게시
* 자체 검토 편집
* 자체 검토 삭제
* 다른 사용자의 검토 주석 플래그 지정

멤버당 하나의 등급만 허용됩니다. 회원은 언제든지 등급을 변경할 수 있습니다.

### 익명 {#anonymous}

로그인하지 않은 사이트 방문자는 게시된 검토만 읽고, 지원되는 경우 번역하거나, 등급 또는 검토를 추가할 수 없거나, 다른 사용자의 검토 주석에 플래그를 지정할 수 있습니다.

## 추가 정보 {#additional-information}

자세한 내용은 [검토 핵심 사항](reviews-basics.md) 개발자를 위한 페이지입니다.

게시된 댓글 조정에 대해서는 [사용자가 생성한 컨텐츠 중재](moderate-ugc.md).

게시된 댓글 번역에 대해서는 [사용자가 생성한 컨텐츠 번역](translate-ugc.md).
