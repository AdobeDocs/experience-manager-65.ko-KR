---
title: 그룹 템플릿
seo-title: 그룹 템플릿
description: 그룹 템플릿 콘솔에 액세스하는 방법
seo-description: 그룹 템플릿 콘솔에 액세스하는 방법
uuid: 4cf20c91-32b0-4051-a98d-44e4eb50a231
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e9bfbbce-93fc-455c-a2f7-4ee44e63c03f
docset: aem65
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054

---


# 그룹 템플릿 {#group-templates}

그룹 템플릿 콘솔은 사이트 템플릿 [콘솔과](/help/communities/sites.md) 유사합니다. 두 제품 모두 미리 연결된 페이지 및 커뮤니티 사이트를 구성하는 기능에 대한 청사진입니다. 차이점은 사이트 템플릿은 기본 커뮤니티를 위한 것이며 그룹 템플릿은 커뮤니티 그룹을 위한 것이며 기본 커뮤니티 내에 중첩된 하위 커뮤니티를 위한 것입니다.

커뮤니티 그룹은 Groups 함수를 [](/help/communities/functions.md#groups-function) 포함하여 사이트 템플릿에 통합됩니다(템플릿에서 첫 번째 또는 유일한 함수가 아닐 수 있음).

커뮤니티 [기능 팩 1부터](/help/communities/deploy-communities.md#latestfeaturepack)그룹 기능을 그룹 템플릿 내에 포함하여 그룹을 중첩할 수 있습니다.

새 커뮤니티 그룹을 만들기 위한 작업이 수행되면 그룹의 템플릿(구조)이 선택됩니다. 선택 사항은 사이트 또는 그룹 템플릿에 추가할 때 그룹 함수가 어떻게 구성되었는지에 따라 다릅니다.

>[!NOTE]
>
>커뮤니티 사이트 [만들기,](/help/communities/sites-console.md)커뮤니티 사이트 템플릿 [,](/help/communities/sites.md)커뮤니티 그룹 템플릿 [및](/help/communities/tools-groups.md) 커뮤니티 기능 [](/help/communities/functions.md) 은 작성 환경에서만 사용할 수 있는 콘솔입니다.


## 그룹 템플릿 콘솔 {#group-templates-console}

AEM 작성자 환경의 그룹 템플릿 콘솔에 액세스하려면:

* 도구 **선택| 커뮤니티| 그룹 템플릿,** 전역 탐색

이 콘솔에는 [커뮤니티 사이트를](/help/communities/sites-console.md) 만들 수 있는 템플릿이 표시되며 새 그룹 템플릿을 만들 수 있습니다.

![커뮤니티 그룹 템플릿](assets/groups-template.png)

## 그룹 템플릿 작성 {#create-group-template}

새 그룹 템플릿 만들기를 시작하려면 을 `Create`선택합니다.

이렇게 하면 3개의 하위 패널이 포함된 사이트 편집기 패널이 표시됩니다.

### 기본 정보 {#basic-info}

![chlimage_1-137](assets/chlimage_1-137.png)

[기본 정보] 패널에서 이름, 설명 및 템플릿이 활성화되었는지 또는 비활성화되었는지 여부가 구성됩니다.

* **새 그룹 템플릿 이름**

   템플릿 이름 ID입니다.

* **설명**

   템플릿 설명입니다.

* **비활성화/활성화**

   템플릿을 참조할 수 있는지 여부를 제어하는 전환 스위치입니다.

#### 썸네일 {#thumbnail}

![chlimage_1-138](assets/chlimage_1-138.png)

(선택 사항) 이미지 업로드 아이콘을 선택하여 커뮤니티 사이트 작성자에게 이름 및 설명과 함께 축소판을 표시합니다.

#### 구조 {#structure}

>[!CAUTION]
>
>AEM 6.1 Communities FP4 이전 버전에서 작업하는 경우 그룹 기능을 그룹 템플릿에 추가하지 마십시오.
>
>중첩된 그룹 기능은 Communities FP1 [에서](/help/communities/communities.md#latestfeaturepack)사용할 수 있습니다.
>
>템플릿의 첫 번째 함수나 유일한 함수로 그룹 함수를 추가할 수 없습니다.


![그룹 템플릿 편집기](assets/template-editor.png)

커뮤니티 기능을 추가하려면 사이트 메뉴 링크가 표시되는 순서대로 오른쪽에서 왼쪽으로 드래그합니다. 사이트를 만드는 동안 스타일이 템플릿에 적용됩니다.

예를 들어 포럼을 원하는 경우 라이브러리에서 포럼 함수를 드래그하여 템플릿 빌더 아래에 놓습니다. 그러면 포럼 구성 대화 상자가 열립니다. 구성 대화 상자에 대한 자세한 내용은 [기능 콘솔을](/help/communities/functions.md) 참조하십시오.

이 템플릿을 기반으로 하는 하위 커뮤니티 사이트(그룹)에 대해 원하는 다른 모든 커뮤니티 기능을 드래그하여 놓습니다.

![드래그 함수](assets/dragfunctions.png)

원하는 기능을 모두 템플릿 빌더 영역에 놓고 구성했으면 오른쪽 **위** 모서리에서 저장을 선택합니다.

## 그룹 템플릿 편집{#edit-group-template}

기본 그룹 템플릿 콘솔에서 [](#group-templates-console)커뮤니티 그룹을 볼 때 편집할 기존 그룹 템플릿을 선택할 수 있습니다.

그룹 템플릿을 편집해도 템플릿에서 이미 만든 커뮤니티 사이트에는 영향을 주지 않습니다. 대신 커뮤니티 사이트의 [구조를 직접](/help/communities/sites-console.md#modify-structure)편집할 수 있습니다.

이 프로세스에서는 그룹 템플릿을 [만드는 것과 동일한 패널을 제공합니다](#create-group-template).
