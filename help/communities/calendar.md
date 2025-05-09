---
title: 달력 기능
description: 달력 기능이 달력 형식으로 커뮤니티 이벤트 정보를 제공하는 방법에 대해 알아봅니다.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: c9b34b00-525d-4ca3-bd18-11bb7ce66787
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 0%

---

# 달력 기능 {#calendar-feature}

## 소개 {#introduction}

달력 기능은 모든 사이트 방문자 또는 로그인한 사이트 방문자(커뮤니티 구성원)에게만 달력 형식으로 커뮤니티 이벤트 정보를 제공하는 기능을 지원하며, 승인된 구성원만 이벤트를 추가할 수 있습니다.

이 설명서 섹션에서는 다음을 설명합니다.

* AEM 사이트에 달력 기능 추가
* `Calendar` 구성 요소에 대한 구성 설정

## 페이지에 달력 추가 {#adding-a-calendar-to-a-page}

작성자 모드에서 페이지에 `Calendar` 구성 요소를 추가하려면 구성 요소 브라우저를 사용하여 찾습니다

* `Communities / Calendar`

그리고 사용자가 검토할 수 있는 기능을 기준으로 하는 위치와 같이, 페이지를 제자리에 드래그합니다.

필요한 정보는 [커뮤니티 구성 요소 기본 사항](/help/communities/basics.md)을 참조하세요.

[필수 클라이언트측 라이브러리](/help/communities/calendar-basics-for-developers.md#essentials-for-client-side)가 포함된 경우 `Calendar` 구성 요소가 표시되는 방식입니다.

![calendar-component](assets/calendar-component.png)

### 달력 구성 {#configuring-calendar}

배치된 `Calendar` 구성 요소를 선택하여 편집 대화 상자를 여는 `Configure` 아이콘에 액세스하고 선택합니다.

![구성](assets/configure-new.png)

![configure-calendar](assets/configure-calendar1.png)

#### 설정 탭 {#settings-tab}

**설정** 탭에서 태그를 일정 항목에 적용할 수 있는지 여부를 지정합니다.

* **페이지당 이벤트**

  페이지당 표시되는 이벤트 수를 정의합니다. 기본값은 10입니다.

* **중재됨**

  선택하면 달력 이벤트 및 댓글이 게시 사이트에 표시되기 전에 게시를 승인해야 합니다. 기본값은 선택 취소되어 있습니다.

* **닫힘**

  선택하면 캘린더에 새 이벤트 항목과 주석이 닫힙니다. 기본값은 선택 취소되어 있습니다.

* **리치 텍스트 편집기**

  선택하면 달력 이벤트 및 주석을 마크업과 함께 입력할 수 있습니다. 기본값은 선택되어 있습니다.

* **태그 지정 허용**

  선택하면 구성원이 게시하는 이벤트에 태그 레이블을 추가할 수 있습니다(**태그 필드** 탭 참조). 기본값은 선택되어 있습니다.

* **파일 업로드 허용**

  선택하면 일정 이벤트나 주석에 첨부 파일을 추가할 수 있습니다. 기본값은 선택되어 있습니다.

* **다음 허용**

  선택하면 구성원이 캘린더에 게시된 이벤트를 따르도록 허용합니다. 기본값은 선택되어 있습니다.

* **최대 파일 크기**

  `Allow File Uploads`을(를) 선택한 경우에만 관련이 있습니다. 이 필드는 업로드된 파일의 크기(바이트)를 제한합니다. 기본값은 104857600(10Mb)입니다.

* **허용되는 파일 형식**

  `Allow File Uploads`을(를) 선택한 경우에만 관련이 있습니다. &quot;점&quot; 구분 기호가 있는 쉼표로 구분된 파일 확장자 목록입니다. 예: .jpg, .jpeg, .png, .doc, .docx, .pdf 지정된 파일 유형이 있으면 지정되지 않은 파일 유형을 업로드할 수 없습니다. 기본값은 모든 파일 형식이 허용되도록 지정되지 않습니다.

* **이미지 첨부 파일 최대 크기**

  [파일 업로드 허용]이 선택된 경우에만 해당됩니다. 업로드된 이미지 파일에 포함할 수 있는 최대 바이트 수입니다. 기본값은 2097152 **&#x200B; &#x200B;**(2Mb)입니다.

* **허용되는 표지 이미지 형식**

  구분 기호가 &quot;점&quot;인 쉼표로 구분된 이미지 파일 확장자 목록입니다. 기본값은 `.jpg,.jpeg,.png,.gif,.bmp`입니다.

* **스레드된 회신 허용**

  선택하면 달력 이벤트에 게시된 댓글에 대한 답글을 허용합니다. 기본값은 선택되어 있습니다.

* **사용자가 댓글 및 이벤트를 삭제하도록 허용**

  선택하면 구성원이 게시한 댓글 및 달력 이벤트를 삭제할 수 있습니다. 기본값은 선택되어 있습니다.

* **투표 허용**

  선택하면 달력 이벤트에 투표 기능을 포함합니다. 기본값은 선택되어 있습니다.

* **탐색 표시**

  이벤트 페이지에 탐색 표시를 표시합니다. 기본값은 선택되어 있습니다.

* **날짜 범위 필터**

  현재 날짜에 추가되는 일 수를 정의하여 페이지 필터를 나열하는 달력 이벤트의 &quot;종료&quot; 값을 계산합니다. 기본 번호는 30입니다.

* **추천 콘텐츠 허용**

  선택하면 해당 아이디어는 [추천 콘텐츠](/help/communities/featured.md)(으)로 식별됩니다. 기본값은 선택 취소되어 있습니다.

**사용자 중재** 탭에서 게시된 주제 및 답글(사용자가 생성한 콘텐츠)을 관리하는 방법을 지정합니다. 자세한 내용은 [사용자 생성 콘텐츠 중재](/help/communities/moderate-ugc.md)를 참조하십시오.

#### 사용자 중재 탭 {#user-moderation-tab}

* **게시물 거부**

  선택하면 신뢰할 수 있는 구성원 중재자가 게시물을 거부하고 해당 게시물이 공개 포럼에 표시되지 않도록 할 수 있습니다. 기본값은 선택되어 있습니다.

* **이벤트 닫기/다시 열기**

  선택하면 신뢰할 수 있는 구성원 중재자가 이벤트를 닫아 추가 편집 및 댓글을 남길 수 있으며 이벤트를 다시 열 수도 있습니다. 기본값은 선택되어 있습니다.

* **게시물 플래그 지정**

  선택하면 구성원이 다른 사람의 이벤트나 댓글에 부적절한 플래그를 지정할 수 있습니다. 기본값은 선택되어 있습니다.

* **이유 목록 플래그 지정**

  선택하면 멤버가 드롭다운 목록에서 이벤트나 댓글을 부적절한 것으로 플래그 지정한 이유를 선택할 수 있습니다. 기본값은 선택 취소되어 있습니다.

* **사용자 지정 플래그 이유**

  선택하면 구성원이 이벤트나 댓글을 부적절한 것으로 플래그를 지정하는 이유를 직접 입력할 수 있습니다. 기본값은 선택 취소되어 있습니다.

* **중재 임계값**

  중재자에게 알림을 보내기 전에 구성원에게 이벤트나 댓글에 플래그를 지정해야 하는 횟수를 입력합니다. 기본값은 1(1회)입니다.

* **플래그 지정 제한**

  공개 보기에서 숨기려면 먼저 이벤트나 댓글에 플래그를 지정해야 하는 횟수를 입력합니다. -1로 설정하면 플래그가 지정된 항목이나 댓글이 공개 보기에서 숨겨지지 않습니다. 그렇지 않으면 이 숫자는 중재 임계값보다 크거나 같아야 합니다. 기본값은 5입니다.

#### 태그 필드 탭 {#tag-field-tab}

**태그 필드** 탭에서 **설정** 탭에서 허용되는 경우 적용할 수 있는 태그는 선택한 네임스페이스에 따라 제한됩니다.

* **허용되는 네임스페이스**

  **설정** 탭에서 `Allow Tagging`을(를) 선택한 경우 관련성이 있습니다. 적용할 수 있는 태그는 선택된 네임스페이스 카테고리 내의 태그로 제한됩니다. 네임스페이스 목록에는 &quot;표준 태그&quot;(기본 네임스페이스)와 &quot;모든 태그 포함&quot;이 포함됩니다. 기본값은 선택 안 함으로, 모든 네임스페이스가 허용됩니다.

* **제안 한도**

  포럼에 게시하는 구성원에 대한 제안으로 표시할 태그 수를 입력합니다. 기본값은 **-**&#x200B;1(제한 없음)입니다.

>[!NOTE]
>
>태그 네임스페이스(분류법)를 추가하는 방법을 배울 수 있는 [태그 관리](/help/sites-administering/tags.md)를 방문하십시오.

#### 번역 탭 {#translation-tab}

**번역** 탭에서 커뮤니티 사이트에 대해 번역을 사용하도록 설정한 경우 특정 게시물이 아닌 전체 스레드(이벤트 및 댓글)를 번역하도록 번역을 설정할 수 있습니다.

* **모두 번역**

  선택하면 이벤트 및 댓글이 사용자의 기본 언어로 번역됩니다. 기본값은 선택되어 있습니다.

## 사이트 방문자 경험 {#site-visitor-experience}

게시 환경에서 달력 기능은 기본 날짜 범위가 있는 검색 필드와 해당 범위에 속하는 모든 달력 이벤트를 표시합니다.

달력 이벤트를 선택하면 달력 이벤트 세부 사항, 설명 및 주석이 표시됩니다.

다른 기능은 사이트 방문자가 중재자, 관리자, 커뮤니티 구성원, 권한이 있는 구성원 또는 익명인지 여부에 따라 다릅니다.

### 중재자 및 관리자 {#moderators-and-administrators}

로그인한 사용자에게 중재자 또는 관리자 권한이 있으면 이벤트에 게시된 모든 일정 이벤트 및 댓글에 대해 [중재 작업](/help/communities/moderate-ugc.md)(구성 요소의 구성에서 허용된 경우)을 수행할 수 있습니다.

![중재자-보기](assets/moderators-view.png)

#### 구성원 {#members}

로그인한 사용자가 커뮤니티 구성원 또는 [권한이 있는 구성원](/help/communities/users.md#privileged-members-group)(구성에 따라 다름)이면 `New Event`을(를) 선택하여 새 일정 이벤트를 만들고 게시할 수 있습니다.

특히 다음과 같은 경우가 있습니다.

* 달력 이벤트 만들기
* 달력 이벤트에 대한 댓글 Post
* 자신의 캘린더 이벤트 또는 댓글 편집
* 자신의 캘린더 이벤트 또는 댓글 삭제
* 다른 사람의 일정 이벤트 또는 댓글에 플래그 지정

![create-event](assets/configure-calendar2.png)

![이벤트-게시물](assets/configure-calendar3.png)

#### 익명 {#anonymous}

로그인하지 않은 사이트 방문자는 게시된 달력 이벤트만 읽고, 지원되는 경우 번역만 할 수 있으며, 이벤트나 댓글을 추가하거나 다른 사람의 이벤트나 댓글에 플래그를 지정하지 않을 수 있습니다.

![익명 사용자 보기](assets/anonymous-user-view1.png)

## 추가 정보 {#additional-information}

자세한 내용은 개발자를 위한 [Calendar Essentials](/help/communities/calendar-basics-for-developers.md) 페이지에서 확인할 수 있습니다.

일정 이벤트 및 댓글의 중재에 대해서는 [사용자 생성 콘텐츠 중재](/help/communities/moderate-ugc.md)를 참조하십시오.

일정 이벤트 및 댓글에 태그를 지정하려면 [사용자 생성 콘텐츠에 태그 지정](/help/communities/tag-ugc.md)을 참조하세요.

일정 이벤트 및 댓글의 번역은 [사용자 생성 콘텐츠 번역](/help/communities/translate-ugc.md)을 참조하세요.
