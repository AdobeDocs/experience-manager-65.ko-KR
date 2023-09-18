---
title: 사이트 템플릿
description: 사이트 템플릿 콘솔에 액세스하는 방법
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 05a944a3-adb1-47b4-b4a5-15bac91c995e
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 4%

---

# 사이트 템플릿 {#site-templates}

사이트 템플릿 콘솔은 [그룹 템플릿](tools-groups.md) 콘솔 : 커뮤니티 그룹에 관심 있는 기능에 중점을 둡니다.

>[!NOTE]
>
>만들기 위한 콘솔 [커뮤니티 사이트](sites-console.md), [커뮤니티 사이트 템플릿](sites.md), [커뮤니티 그룹 템플릿](tools-groups.md), 및 [커뮤니티 기능](functions.md) 는 작성 환경에서만 사용됩니다.

## 사이트 템플릿 콘솔 {#site-templates-console}

작성 환경에서 커뮤니티 사이트 콘솔에 도달하려면 다음 작업을 수행하십시오.

* 전역 탐색에서: **[!UICONTROL 도구 > 커뮤니티 > 사이트 템플릿]**

이 콘솔에는 [커뮤니티 사이트](sites-console.md) 를 만들고 새 사이트 템플릿을 만들 수 있습니다.

![site-template](assets/site-template.png)

## 사이트 템플릿 작성 {#create-site-template}

사이트 템플릿 만들기를 시작하려면 다음을 선택합니다. `Create`.

이렇게 하면 세 개의 하위 패널이 포함된 사이트 편집기 패널이 열립니다.

### 기본 정보 {#basic-info}

![site-template-basicinfo](assets/site-template-basicinfo.png)

기본 정보 패널에는 이름, 설명 및 템플릿의 활성화/비활성화 여부가 구성되어 있습니다.

* **[!UICONTROL 커뮤니티 사이트 템플릿 이름]**

  템플릿 이름 ID입니다.

* **[!UICONTROL 커뮤니티 사이트 템플릿 설명]**

  템플릿 설명입니다.

* **[!UICONTROL 사용 안 함/사용]**

  템플릿을 참조할 수 있는지 여부를 제어하는 토글 스위치입니다.

### 썸네일 {#thumbnail}

![사이트 썸네일](assets/site-thumbnail.png)

(선택 사항) 이미지 업로드 아이콘을 선택하여 커뮤니티 사이트 작성자에게 이름 및 설명과 함께 썸네일을 표시합니다.

### 구조 {#structure}

![사이트 구조](assets/site-structure.png)

커뮤니티 기능을 추가하려면 사이트 메뉴 링크가 표시되는 순서로 오른쪽에서 왼쪽으로 끕니다. 사이트 생성 중 스타일이 템플릿에 적용됩니다.

예를 들어, 홈 페이지를 원하는 경우 라이브러리에서 페이지 함수를 드래그하여 템플릿 빌더 아래에 놓습니다. 그러면 페이지 구성 대화 상자가 열립니다. 다음을 참조하십시오. [함수 콘솔](functions.md) 구성 대화 상자에 대한 정보를 제공합니다.

이 템플릿을 기반으로 커뮤니티 사이트에 원하는 다른 커뮤니티 기능을 계속 끌어서 놓습니다.

page 함수는 빈 페이지를 제공합니다. 그룹 기능을 사용하면 커뮤니티 사이트 내에 그룹 사이트(하위 커뮤니티)를 만들 수 있습니다.

>[!CAUTION]
>
>Groups 함수는 *처음도 아니고 유일한 것도 아님* 사이트 구조에서 작동합니다.
>
>기타 모든 함수(예: ) [페이지 기능](functions.md#page-function)를 포함해야 하며 먼저 나열되어야 합니다.

![사이트 편집기](assets/site-editor.png)

### 그룹 기능에 대한 그룹 템플릿 {#group-templates-for-groups-function}

사이트 템플릿에 그룹 기능을 포함할 때 구성에서는 게시 환경에 새 그룹을 만들 때 허용되는 그룹 템플릿 선택 사항의 지정이 필요합니다.

>[!CAUTION]
>
>Groups 함수는 *처음도 아니고 유일한 것도 아님* 사이트 구조에서 작동합니다.

![사이트 함수](assets/site-functions.png)

둘 이상의 커뮤니티 그룹 템플릿을 선택하면 커뮤니티에서 실제로 그룹을 만들 때 그룹 관리자에게 선택 사항이 제공됩니다.

![site-function](assets/site-functions1.png)

## 사이트 템플릿 편집 {#edit-site-template}

기본 사이트에서 사이트 템플릿을 볼 때 [사이트 템플릿 콘솔](#site-templates-console)을(를) 통해 편집할 기존 사이트 템플릿을 선택할 수 있습니다.

이 프로세스는 과 동일한 패널을 제공합니다. [사이트 템플릿 만들기](#create-site-template).
