---
title: 파일 라이브러리 기능
seo-title: 파일 라이브러리 기능
description: 파일 라이브러리 기능을 사용하면 로그인한 사이트 방문자가 파일을 업로드, 관리 및 다운로드할 수 있습니다
seo-description: 파일 라이브러리 기능을 사용하면 로그인한 사이트 방문자가 파일을 업로드, 관리 및 다운로드할 수 있습니다
uuid: e78a90bd-f1d3-44f8-98eb-1498a55e8217
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ea2b23af-49c3-409b-a041-43c42d846f21
docset: aem65
exl-id: 05cfaab5-a12d-475f-9095-a9fb13571d0a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 8%

---

# 파일 라이브러리 기능{#file-library-feature}

## 소개 {#introduction}

파일 라이브러리 기능은 커뮤니티 사이트 내에서 파일을 업로드, 관리 및 다운로드할 수 있는 로그인 사이트 방문자(커뮤니티 구성원)를 위한 공간을 제공합니다.

설명서의 이 섹션에서는 다음 사항에 대해 설명합니다.

* AEM 사이트에 파일 라이브러리 기능 추가.
* `File Library` 구성 요소에 대한 구성 설정입니다.

### 페이지에 파일 라이브러리 추가 {#adding-a-file-library-to-a-page}

작성자 모드의 페이지에 `File Library` 구성 요소를 추가하려면 구성 요소를 찾습니다.

* `Communities / File Library`

페이지로 끌어서 놓습니다.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](/help/communities/basics.md)을 방문하십시오.

필요한 [클라이언트 측 라이브러리](/help/communities/essentials-file-library.md#essentials-for-client-side)가 포함된 경우 이 방법으로 `File Library` 구성 요소가 표시됩니다.

![file-library1](assets/file-library1.png)

### 파일 라이브러리 구성 {#configuring-file-library}

액세스할 배치된 `File Library` 구성 요소를 선택하고 편집 대화 상자를 여는 `Configure` 아이콘을 선택합니다.

![configure-new](assets/configure-new.png)

![file-library2](assets/file-library2.png)

#### 댓글 탭 {#comments-tab}

**댓글** 탭에서 업로드된 파일에 대한 주석이 표시되는 여부와 방법을 지정합니다.

* **파일에 대한 주석 허용**

   이 확인란을 선택하면 업로드된 파일에 대한 주석을 허용합니다. 기본값은 선택 취소되어 있습니다.

* **페이지당 댓글**

   표시된 답글 수와 페이지당 표시되는 댓글 수를 제한합니다. 기본값은 **10**&#x200B;입니다.

* **최대 파일 크기**

   이 값은 업로드된 파일 크기를 제한합니다. 기본 제한은 104857600(10Mb)입니다.

* **최대 메시지 길이**

   텍스트 상자에 입력할 수 있는 최대 문자 수입니다. 기본값은 4096자입니다.

* **허용되는 파일 유형**

   점이 구분되어 있는 쉼표로 구분된 파일 확장자 목록입니다. 예 :.jpg, .jpeg, .png, .doc, .docx, .pdf 파일 유형을 지정하면 지정되지 않은 파일 유형이 허용되지 않습니다. 모든 파일 형식이 허용되도록 기본값이 지정되지 않았습니다.

* **리치 텍스트 편집기**

   이 옵션을 선택하면 마크업에 주석을 입력할 수 있습니다. 기본값은 선택 취소되어 있습니다.

* **댓글 삭제**

   이 확인란을 선택하면 사용자가 자신의 주석을 삭제할 수 있습니다. 기본값이 선택되어 있습니다.

* **태깅 허용**

   이 확인란을 선택하면 파일에 태그를 추가하는 기능이 활성화됩니다. 기본값은 선택 취소되어 있습니다.

* **허용되는 네임스페이스**

   태깅 허용 을 선택하면 사용 가능한 태그는 선택한 네임스페이스로 제한됩니다. 아무것도 선택하지 않으면 모든 것이 허용됩니다. 기본값은 모든 네임스페이스입니다.

* **제안 한도**

   태깅 허용 을 선택하면 이 설정은 표시할 제안된 태그의 수를 제한합니다. -1로 설정하면 제한이 없습니다. 기본값은 -1입니다.

* **투표 허용**

   이 옵션을 선택하면 파일에 대한 유권자 권한이 활성화됩니다. 기본값은 선택 취소되어 있습니다.

* **다음 허용**

   이 확인란을 선택하면 구성원이 새 게시물의 [notified](/help/communities/notifications.md)가 될 수 있는 블로그 문서에 다음 기능을 포함하십시오. 기본값은 선택 취소되어 있습니다.

* **언급 활성화**

   활성화된 경우 등록된 커뮤니티 사용자가 등록된 다른 구성원을 식별하고(이름, 성, 사용자 이름 사용) 일반적인 @user-name 구문을 사용하여 태그를 지정할 수 있습니다. 태그가 지정된 사용자는 언급 관련 알림을 받습니다.

* **최대 언급 수**

   게시물에서 허용되는 최대 언급 수를 제한합니다. 기본값은 10입니다.

* **UI 언급 패턴**

   등록된 사용자를 게시물에 태그 지정(@mention)할 허용된 패턴 문자열을 지정합니다. 예: ~{{familyName}}{{givenName}}.

* **스레드된 회신 허용**

   이 확인란을 선택하면 게시된 댓글에 답글을 허용합니다. 기본값은 선택 취소되어 있습니다.

#### 사용자 중재 탭 {#user-moderation-tab}

**사용자 중재** 탭 아래에서, 댓글이 허용된 경우 댓글의 조정을 구성합니다.

* **사전 관리**

   이 확인란을 선택하면 게시 사이트에 주석이 표시되기 전에 승인해야 합니다. 기본값은 선택 취소되어 있습니다.

* **댓글 삭제**

   이 확인란을 선택하면 댓글을 게시한 방문자에게 댓글을 삭제할 수 있는 기능이 제공됩니다. 기본값이 선택되어 있습니다.

* **댓글 거부**

   이 옵션을 선택하면 신뢰할 수 있는 멤버 중재자가 주석을 거부할 수 있습니다. 기본값은 선택 취소되어 있습니다.

* **댓글 닫기 / 다시 열기**

   이 옵션을 선택하면 신뢰할 수 있는 멤버 중재자가 주석을 닫고 다시 열 수 있습니다. 기본값은 선택 취소되어 있습니다.

* **댓글에 플래그 지정**

   이 확인란을 선택하면 방문자가 댓글을 부적절한 것으로 플래그를 지정할 수 있습니다. 기본값은 선택 취소되어 있습니다.

* **플래그 이유 목록**

   이 확인란을 선택하면 방문자가 드롭다운 목록에서 선택할 수 있습니다. 댓글에 대한 플래그 지정 이유가 부적절한 것으로 표시됩니다. 기본값은 선택 취소되어 있습니다.

* **사용자 지정 플래그 이유**

   이 확인란을 선택하면 방문자가 댓글에 대한 플래그 지정 이유가 부적절한 것으로 입력할 수 있습니다. 기본값은 선택 취소되어 있습니다.

* **관리 임계값**

   중재자에게 알리기 전에 방문자가 댓글에 플래그를 지정해야 하는 횟수를 입력합니다. 기본값은 한 번(**1**)입니다.

* **플래그 지정 제한**

   공개 보기에서 주석이 숨겨지기 전에 플래그를 지정해야 하는 횟수를 입력합니다. 이 숫자는 **중재 임계값**&#x200B;보다 크거나 같아야 합니다. 기본값은 5입니다.

### 정렬 설정 탭 {#sort-settings-tab}

정렬 기준

기본값으로 설정

### 추가 정보 {#additional-information}

개발자를 위한 [파일 라이브러리 필수 패키지](/help/communities/essentials-file-library.md) 페이지에서 자세한 정보를 찾을 수 있습니다.

게시된 항목 및 댓글에 대한 중복을 보려면 [사용자 생성 콘텐츠 중재](/help/communities/moderate-ugc.md)를 참조하십시오.

게시된 항목 및 댓글에 태깅하려면 [사용자 생성 컨텐츠 태깅](/help/communities/tag-ugc.md)을 참조하십시오.
