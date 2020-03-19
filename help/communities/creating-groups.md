---
title: 커뮤니티 그룹
seo-title: 커뮤니티 그룹
description: 커뮤니티 그룹 만들기
seo-description: 커뮤니티 그룹 만들기
uuid: c677d23d-5edb-414c-9013-130c88c2ea52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d94708ee-ca6b-420c-9536-6889d752f9de
docset: aem65
translation-type: tm+mt
source-git-commit: e8d8bf89971d3d9d5ec150308dda247aa53c77bb

---


# 커뮤니티 그룹 {#community-groups}

커뮤니티 그룹 기능은 게시 및 작성 환경에서 승인된 사용자(커뮤니티 구성원 및 작성자)가 커뮤니티 사이트 내에서 하위 커뮤니티를 동적으로 만드는 기능입니다.

이 기능은 [그룹 기능이](/help/communities/functions.md#groups-function) [커뮤니티 사이트](/help/communities/sites-console.md) 구조에 있을 때 제공됩니다.

커뮤니티 그룹 템플릿은 [](/help/communities/tools-groups.md) 커뮤니티 그룹이 동적으로 생성될 때 커뮤니티 그룹 페이지의 디자인을 제공합니다.

커뮤니티 사이트의 구조나 커뮤니티 사이트 템플릿에 기능을 추가하면 그룹 기능에 대해 하나 이상의 그룹 템플릿이 선택됩니다. 이 그룹 템플릿 목록은 커뮤니티 사이트 내에서 새 그룹을 동적으로 만드는 구성원 또는 작성자에게 표시됩니다.

## Creating a New Group {#creating-a-new-group}

새 커뮤니티 그룹을 만드는 기능은 에서 만든 그룹 기능과 같은 그룹 기능을 포함하는 커뮤니티 사이트의 존재에 의존합니다 ` [Reference Site Template](/help/communities/sites.md)`.

다음에 나오는 예는 AEM Communities 시작하기 `Reference Site Template` 자습서에 설명된 대로 에서 만든 커뮤니티 사이트를 [](/help/communities/getting-started.md) 사용합니다.

[그룹] 메뉴 항목을 선택하면 게시 시 **로드되는** 페이지입니다.

![chlimage_1-85](assets/chlimage_1-85.png)

새 그룹 **아이콘을 선택하면** 편집 대화 상자가 열립니다.

설정 **탭에서** 그룹의 기본 기능을 제공합니다.

![chlimage_1-86](assets/chlimage_1-86.png)

* **그룹 이름**

   커뮤니티 사이트에 표시할 그룹의 제목입니다.

* **설명**

   커뮤니티 사이트에 표시할 그룹에 대한 설명입니다.

* **초대**

   그룹에 가입하도록 초대할 구성원 목록입니다. 사전 입력 검색은 커뮤니티 구성원이 초대할 수 있는 제안을 제공합니다.

* **그룹 URL 이름**

   URL의 일부가 되는 그룹 페이지의 이름입니다.

* **그룹 개방**

   선택을 `Open Group` 선택하면 익명의 사이트 방문자가 컨텐츠를 볼 수 있으며 선택 취소됩니다 `Member Only Group`.

* **구성원 전용 그룹**

   선택을 `Member Only Group` 선택하면 그룹의 구성원만 컨텐츠를 볼 수 있으며 선택 취소합니다 `Open Group`.

템플릿 **탭** 아래에서는 그룹 함수가 커뮤니티 사이트의 구조 또는 커뮤니티 사이트 템플릿에 포함될 때 지정된 커뮤니티 그룹 템플릿 목록에서 선택하는 기능이 있습니다.

![chlimage_1-87](assets/chlimage_1-87.png)

이미지 **탭** 아래에서 커뮤니티 사이트의 그룹 페이지에 그룹에 대해 표시할 이미지를 업로드할 수 있습니다. 기본 스타일 시트는 이미지의 크기를 170 x 90픽셀로 조정합니다.

![chlimage_1-88](assets/chlimage_1-88.png)

[그룹 **만들기** ] 단추를 선택하면 선택한 템플릿을 기반으로 그룹에 대한 페이지가 만들어지고 멤버십에 대한 사용자 그룹이 만들어지고 그룹 페이지가 업데이트되어 새 하위 커뮤니티가 표시됩니다.

예를 들어 이미지 축소판이 업로드된 새 하위 커뮤니티인 &quot;포커스 그룹&quot;이 있는 그룹 페이지는 다음과 같이 표시됩니다(커뮤니티 그룹 관리자로 로그인됨).

![chlimage_1-89](assets/chlimage_1-89.png)

링크를 선택하면 선택한 템플릿을 기준으로 초기 모양이 있는 브라우저의 [포커스 그룹] 페이지가 열리고 기본 커뮤니티 사이트의 메뉴 아래에 하위 메뉴가 포함됩니다. `Focus Group`

![chlimage_1-90](assets/chlimage_1-90.png)

### Community Group Member List Component {#community-group-member-list-component}

이 `Community Group Member List` 구성 요소는 그룹 템플릿의 개발자가 사용하도록 만들어졌습니다.

### 추가 정보 {#additional-information}

개발자를 위한 커뮤니티 그룹 필수 [사항](/help/communities/essentials-groups.md) 페이지에서 자세한 내용을 확인할 수 있습니다.

커뮤니티 그룹과 관련된 기타 정보는 사용자 및 사용자 [그룹 관리를 참조하십시오](/help/communities/users.md).
