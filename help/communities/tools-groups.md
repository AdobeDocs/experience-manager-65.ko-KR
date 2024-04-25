---
title: 그룹 템플릿
description: 커뮤니티 사이트를 구성하는 미리 배선된 페이지 및 기능 세트의 그룹 템플릿 콘솔에 액세스하는 방법에 대해 알아봅니다.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: aed2c3f2-1b5e-4065-8cec-433abb738ef5
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 2%

---

# 그룹 템플릿 {#group-templates}

그룹 템플릿 콘솔은 [사이트 템플릿](/help/communities/sites.md) 콘솔. 두 페이지 모두 커뮤니티 사이트를 구성하는 미리 배선된 페이지 및 기능 세트의 블루프린트입니다. 사이트 템플릿은 기본 커뮤니티를 위한 것이고 그룹 템플릿은 기본 커뮤니티 내에 중첩된 하위 커뮤니티인 커뮤니티 그룹을 위한 것입니다.

커뮤니티 그룹은 다음을 포함하여 사이트 템플릿에 통합됩니다 [그룹 기능](/help/communities/functions.md#groups-function) (템플릿에서 첫 번째 기능도 아니고 유일한 기능도 아닐 수 있음).

커뮤니티 기준 [기능 팩 1](/help/communities/deploy-communities.md#latestfeaturepack), 그룹 템플릿 내에 그룹 함수를 포함하여 그룹을 중첩할 수 있습니다.

커뮤니티 그룹을 만들기 위한 작업을 수행하는 순간 그룹의 템플릿(구조)이 선택됩니다. 선택 사항은 사이트 또는 그룹 템플릿에 추가될 때 그룹 기능을 구성한 방법에 따라 다릅니다.

>[!NOTE]
>
>만들기 위한 콘솔 [커뮤니티 사이트](/help/communities/sites-console.md), [커뮤니티 사이트 템플릿](/help/communities/sites.md), [커뮤니티 그룹 템플릿](/help/communities/tools-groups.md), 및 [커뮤니티 기능](/help/communities/functions.md) 는 작성 환경에서만 사용됩니다.

## 그룹 템플릿 콘솔 {#group-templates-console}

AEM Author 환경의 그룹 템플릿 콘솔에 도달하려면 다음을 수행하십시오.

* 선택 **도구 | 커뮤니티 | 그룹 템플릿,** 전역 탐색에서.

이 콘솔에는 [커뮤니티 사이트](/help/communities/sites-console.md) 를 만들고 새 그룹 템플릿을 만들 수 있습니다.

![커뮤니티 그룹 템플릿](assets/groups-template.png)

## 그룹 템플릿 작성 {#create-group-template}

그룹 템플릿 만들기를 시작하려면 다음을 선택합니다. `Create`.

이렇게 하면 세 개의 하위 패널이 포함된 사이트 편집기 패널이 표시됩니다.

### 기본 정보 {#basic-info}

![site-basic-info](assets/site-basic-info.png)

기본 정보 패널에는 이름, 설명 및 템플릿의 활성화/비활성화 여부가 구성되어 있습니다.

* **새 그룹 템플릿 이름**

  템플릿 이름 ID입니다.

* **설명**

  템플릿 설명입니다.

* **사용 안 함/사용**

  템플릿을 참조할 수 있는지 여부를 제어하는 토글 스위치입니다.

#### 썸네일 {#thumbnail}

![사이트 썸네일](assets/site-thumbnail.png)

(선택 사항) 이미지 업로드 아이콘을 선택하여 커뮤니티 사이트 작성자에게 이름 및 설명과 함께 썸네일을 표시합니다.

#### 구조 {#structure}

>[!CAUTION]
>
>AEM 6.1 Communities FP4 또는 이전 버전에서 작업하는 경우 그룹 템플릿에 그룹 함수를 추가하지 마십시오.
>
>중첩 그룹 기능은 커뮤니티에서 사용할 수 있습니다 [FP1](/help/communities/communities.md#latestfeaturepack).
>
>여전히 그룹 함수를 템플릿에 첫 번째 또는 유일한 함수로 추가할 수 없습니다.

![그룹 템플릿 편집기](assets/template-editor.png)

커뮤니티 기능을 추가하려면 사이트 메뉴 링크가 표시되는 순서로 오른쪽에서 왼쪽으로 끕니다. 사이트 생성 중 스타일이 템플릿에 적용됩니다.

예를 들어 포럼을 원하는 경우 라이브러리에서 포럼 함수를 드래그하여 템플릿 빌더 아래에 놓습니다. 그러면 포럼 구성 대화 상자가 열립니다. 다음을 참조하십시오. [함수 콘솔](/help/communities/functions.md) 구성 대화 상자에 대한 정보를 제공합니다.

이 템플릿을 기반으로 하위 커뮤니티 사이트(그룹)에 대해 원하는 다른 커뮤니티 기능을 계속 드래그하여 놓습니다.

![드래그 함수](assets/dragfunctions.png)

원하는 기능을 모두 템플릿 빌더 영역에 삭제하고 구성했으면 을 선택합니다. **저장** 오른쪽 상단에 있습니다.

## 그룹 템플릿 편집 {#edit-group-template}

기본에서 커뮤니티 그룹을 볼 때 [그룹 템플릿 콘솔](#group-templates-console)을(를) 통해 편집할 기존 그룹 템플릿을 선택할 수 있습니다.

그룹 템플릿을 편집해도 해당 템플릿에서 이미 만든 커뮤니티 사이트에는 영향을 주지 않습니다. 다음과 같이 직접 [커뮤니티 사이트 편집](/help/communities/sites-console.md#modify-structure)의 구조를 대신 사용합니다.

이 프로세스는 과 동일한 패널을 제공합니다. [그룹 템플릿 만들기](#create-group-template).
