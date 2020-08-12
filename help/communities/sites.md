---
title: 사이트 템플릿
seo-title: 사이트 템플릿
description: 사이트 템플릿 콘솔에 액세스하는 방법
seo-description: 사이트 템플릿 콘솔에 액세스하는 방법
uuid: d2f7556e-7e43-424e-82f1-41790aeb2d98
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 202d7dba-2b34-431d-b10f-87775632807f
translation-type: tm+mt
source-git-commit: 6ab91667ad668abf80ccf1710966169b3a187928
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 4%

---


# 사이트 템플릿 {#site-templates}

사이트 템플릿 콘솔은 커뮤니티 그룹에 대한 관심 기능을 중점적으로 다루는 [그룹 템플릿](tools-groups.md) 콘솔과 매우 유사합니다.

>[!NOTE]
>
>작성 환경에서만 사용할 수 있는 [커뮤니티 사이트](sites-console.md), [커뮤니티 사이트 템플릿](sites.md), [커뮤니티 그룹 템플릿](tools-groups.md) 및 [커뮤니티 기능](functions.md) 의 콘솔입니다.


## 사이트 템플릿 콘솔 {#site-templates-console}

작성 환경에서 커뮤니티 사이트 콘솔에 도달하려면 다음을 수행하십시오.

* 전역 탐색에서: **[!UICONTROL 도구 > 커뮤니티 > 사이트 템플릿]**

이 콘솔에는 [커뮤니티 사이트를](sites-console.md) 만들 수 있는 템플릿이 표시되며 새 사이트 템플릿을 만들 수 있습니다.

![site-template](assets/site-template.png)

## 사이트 템플릿 작성 {#create-site-template}

새 사이트 템플릿 만들기를 시작하려면 을 선택합니다 `Create`.

그러면 3개의 하위 패널이 포함된 사이트 편집기 패널이 표시됩니다.

### Basic info {#basic-info}

![site-template-basicinfo](assets/site-template-basicinfo.png)

기본 정보 패널에서 이름, 설명 및 템플릿 활성화 또는 비활성화 여부를 구성합니다.

* **[!UICONTROL 커뮤니티 사이트 템플릿 이름]**

   템플릿 이름 ID입니다.

* **[!UICONTROL 커뮤니티 사이트 템플릿 설명]**

   템플릿 설명입니다.

* **[!UICONTROL 비활성화/활성화]**

   템플릿의 참조 여부를 제어하는 전환 스위치입니다.

### 썸네일 {#thumbnail}

![site-thumbnail](assets/site-thumbnail.png)

(선택 사항) 커뮤니티 사이트 작성자에게 이름 및 설명과 함께 축소판을 표시하려면 이미지 업로드 아이콘을 선택합니다.

### 구조 {#structure}

![사이트 구조](assets/site-structure.png)

커뮤니티 기능을 추가하려면 사이트 메뉴 링크가 표시되어야 하는 순서대로 오른쪽에서 왼쪽으로 드래그합니다. 사이트를 만드는 동안 스타일이 템플릿에 적용됩니다.

예를 들어 홈 페이지를 원하는 경우 라이브러리에서 페이지 함수를 드래그하여 템플릿 빌더 아래에 놓습니다. 그러면 페이지 구성 대화 상자가 열립니다. 구성 대화 상자에 대한 자세한 내용은 [함수 콘솔을](functions.md) 참조하십시오.

이 템플릿을 기반으로 한 커뮤니티 사이트에서 원하는 다른 커뮤니티 기능을 계속 드래그 앤 드롭합니다.

페이지 함수는 빈 페이지를 제공합니다. 그룹 기능은 커뮤니티 사이트 내에서 그룹 사이트(하위 커뮤니티)를 만드는 기능을 제공합니다.

>[!CAUTION]
>
>그룹 함수는 사이트 구조의 *첫 번째* 함수이거나 유일한 ** 함수여야 합니다.
>
>페이지 함수 [](functions.md#page-function)등 다른 모든 함수를 먼저 포함하여 나열해야 합니다.


![사이트 편집기](assets/site-editor.png)

### 그룹 기능에 대한 그룹 템플릿 {#group-templates-for-groups-function}

사이트 템플릿에서 그룹 기능을 포함할 경우, 게시 환경에서 새 그룹을 만들 때 허용되는 그룹 템플릿 선택 항목의 사양이 구성에 필요합니다.

>[!CAUTION]
>
>Groups 함수는 사이트 구조의 *첫 번째* 함수이거나 유일한 ** 함수여야 합니다.


![사이트 함수](assets/site-functions.png)

둘 이상의 커뮤니티 그룹 템플릿을 선택하면 실제로 커뮤니티에서 새 그룹을 만들 때 그룹 관리자에게 선택 사항이 제공됩니다.

![site-function](assets/site-functions1.png)

## 사이트 템플릿 편집{#edit-site-template}

기본 [사이트 템플릿 콘솔에서](#site-templates-console)사이트 템플릿을 볼 때 편집할 기존 사이트 템플릿을 선택할 수 있습니다.

이 프로세스는 사이트 템플릿 [을 만드는 것과 동일한 패널을 제공합니다](#create-site-template).
