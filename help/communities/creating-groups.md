---
title: 커뮤니티 그룹
description: 커뮤니티 그룹 만들기
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
source-git-commit: e33816b3b8d190e185d2b23dad3a05aca272f01c
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 3%

---

# 커뮤니티 그룹 {#community-groups}

커뮤니티 그룹 기능은 게시 및 작성 환경의 승인된 사용자(커뮤니티 구성원 및 작성자)가 커뮤니티 사이트 내에서 하위 커뮤니티를 동적으로 만들 수 있는 기능입니다.

이 기능은 다음과 같은 경우에 존재합니다. [그룹 기능](/help/communities/functions.md#groups-function) 이(가)에 있습니다. [커뮤니티 사이트](/help/communities/sites-console.md) 구조입니다.

A [커뮤니티 그룹 템플릿](/help/communities/tools-groups.md) 은 커뮤니티 그룹이 동적으로 만들어질 때 커뮤니티 그룹 페이지의 디자인을 제공합니다.

커뮤니티 사이트의 구조나 커뮤니티 사이트 템플릿에 기능을 추가하면 그룹 기능에 대해 하나 이상의 그룹 템플릿이 선택됩니다. 이 그룹 템플릿 목록은 커뮤니티 사이트 내에서 그룹을 동적으로 만드는 구성원 또는 작성자에게 표시됩니다.

## 새 그룹 만들기 {#creating-a-new-group}

커뮤니티 그룹을 만들 수 있는 기능은 (으)로 만든 것과 같이 그룹 기능을 포함하는 커뮤니티 사이트의 존재에 의존합니다. [참조 사이트 템플릿](/help/communities/sites.md).

다음 예제에서는 다음에서 만든 커뮤니티 사이트를 사용합니다. `Reference Site Template` 에 설명된대로 [AEM Communities 시작하기](/help/communities/getting-started.md) 튜토리얼.

이 페이지는 게시 시 다음과 같은 경우에 로드됩니다. **그룹** 메뉴 항목이 선택되었습니다.

![새 그룹](assets/new-group.png)

다음을 선택하면 **새 그룹** 아이콘, 편집 대화 상자가 열립니다.

아래 **설정** 탭에서는 그룹의 기본 기능을 제공합니다.

![group-settings](assets/group-settings.png)

* **그룹 이름**

  커뮤니티 사이트에 표시할 그룹의 제목입니다. 그룹 이름에 밑줄(_) 및 리소스 및 구성과 같은 키워드를 사용하지 마십시오.

* **설명**

  커뮤니티 사이트에 표시할 그룹에 대한 설명입니다.

* **초대**

  그룹에 초대할 구성원 목록입니다. 미리 입력 검색은 초대할 커뮤니티 구성원에 대한 제안을 제공합니다.

* **그룹 URL 이름**

  URL의 일부가 되는 그룹 페이지의 이름입니다.

* **그룹 개방**

  선택 `Open Group` 익명의 사이트 방문자가 컨텐츠를 볼 수 있음을 나타내며 선택을 취소합니다 `Member Only Group`.

* **구성원 전용 그룹**

  선택 `Member Only Group` 그룹의 멤버만 컨텐츠를 볼 수 있음을 나타내고 선택을 취소합니다 `Open Group`.

아래 **템플릿** 탭에서는 커뮤니티 그룹 템플릿 목록에서 선택할 수 있습니다. 이러한 템플릿은 그룹 기능이 커뮤니티 사이트의 구조 또는 커뮤니티 사이트 템플릿에 포함된 경우 지정됩니다.

![group-template](assets/group-template.png)

아래 **이미지** 탭에서 커뮤니티 사이트의 그룹 페이지에 그룹에 대해 표시할 이미지를 업로드할 수 있습니다. 기본 스타일시트는 이미지 크기를 170 x 90픽셀로 지정합니다.

![group-image](assets/group-image.png)

다음을 선택: **그룹 만들기**, 선택한 템플릿을 기반으로 그룹의 페이지가 만들어지고 멤버십에 대한 사용자 그룹이 만들어지며 그룹 페이지가 업데이트되어 새 하위 커뮤니티가 표시됩니다.

예를 들어 이미지 썸네일이 업로드된 &quot;포커스 그룹&quot;이라는 새 하위 커뮤니티가 있는 그룹 페이지가 다음과 같이 표시됩니다(여전히 커뮤니티 그룹 관리자로 로그인됨).

![group-page](assets/group-page.png)

선택 `Focus Group` 링크는 선택한 템플릿을 기반으로 초기 모양을 가지는 브라우저에서 [포커스 그룹] 페이지를 엽니다. 이 페이지에는 주 커뮤니티 사이트의 메뉴 아래에 하위 메뉴가 있습니다.

![open-group-page](assets/open-group-page.png)

### 커뮤니티 그룹 구성원 목록 구성 요소 {#community-group-member-list-component}

다음 `Community Group Member List` 구성 요소는 그룹 템플릿 개발자용으로 만들어졌습니다.

### 추가 정보 {#additional-information}

자세한 내용은 [커뮤니티 그룹 기본 사항](/help/communities/essentials-groups.md) 개발자용 페이지입니다.

커뮤니티 그룹과 관련된 기타 정보는 다음을 참조하십시오. [사용자 및 사용자 그룹 관리](/help/communities/users.md).
