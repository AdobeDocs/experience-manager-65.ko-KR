---
title: 프로젝트
seo-title: Projects
description: 프로젝트를 사용하면 리소스를 하나의 엔티티로 그룹화하여 공통, 공유 환경에서 프로젝트를 쉽게 관리할 수 있습니다.
seo-description: Projects let you group resources into one entity whose common, shared environment makes it easy to manage your projects
uuid: 4b5b9d78-d515-46af-abe2-882da0a1c8ae
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: dee7ac7c-ca86-48e9-8d95-7826fa926c68
docset: aem65
exl-id: 632c0608-2ab8-4a5b-8251-cd747535449b
source-git-commit: 85e993000c016240c0fbf398ec8192990e60eee6
workflow-type: tm+mt
source-wordcount: '1366'
ht-degree: 33%

---


# 프로젝트 {#projects}

프로젝트를 사용하면 리소스를 하나의 엔티티로 그룹화할 수 있습니다. 공통되는 공유 환경을 사용하면 프로젝트 관리가 쉬워집니다. 프로젝트와 연결할 수 있는 리소스 유형은 AEM에서 타일이라고 합니다. 타일에는 다음에 자세히 설명된 대로 프로젝트 및 팀 정보, 자산, 워크플로우 및 기타 정보 유형이 포함될 수 있습니다. [프로젝트 타일.](#project-tiles)

사용자는

* 프로젝트 만들기 및 삭제
* 컨텐츠 및 자산 폴더를 프로젝트에 연결
* 프로젝트에서 컨텐츠 링크 제거

## 액세스 요구 사항 {#access-requirements}

Project는 표준 AEM 기능을 제공하며 추가 설정이 필요하지 않습니다.

그러나 프로젝트의 사용자가 프로젝트를 만들거나, 작업/워크플로우를 만들거나, 팀을 보고 관리할 때와 같이 프로젝트를 사용하는 동안 다른 사용자/그룹을 보려면 해당 사용자에게는 읽기 액세스 권한이 있어야 합니다 `/home/users` 및 `/home/groups`.

이렇게 하는 가장 쉬운 방법은 **projects-users** 그룹 읽기 액세스 권한 `/home/users` 및 `/home/groups`.

## 프로젝트 콘솔 {#projects-console}

프로젝트 콘솔은 AEM 내 프로젝트를 액세스하고 관리하는 곳입니다.

![프로젝트 콘솔](assets/screen-shot_2019-03-05at125110.png)

프로젝트 콘솔은 AEM의 다른 콘솔과 유사하며 개별 프로젝트에 대해 많은 작업을 허용하고 프로젝트 보기를 조정할 수 있습니다.

### 모드 전환 {#modes}

레일 선택기를 사용하여 콘솔 모드 간에 변경할 수 있습니다.

![레일 선택기](assets/projects-rail.png)

#### 컨텐츠 전용 {#content-only}

컨텐츠 전용 은 콘솔을 열 때의 기본 모드입니다. 모든 프로젝트를 표시합니다.

#### 타임라인 {#timeline}

타임라인 보기를 사용하면 개별 프로젝트를 선택하고 해당 프로젝트에서 활동을 볼 수 있습니다. 레일 선택기 또는 핫키 사용 `alt+1` 을 클릭하여 이 보기로 변경합니다.

![타임라인 모드](assets/project-timeline.png)

### 보기 전환 {#views}

보기 선택기를 사용하여 프로젝트를 큰 타일로 보기(기본값), 목록으로 보기 또는 달력에서 변경할 수 있습니다.

![보기](assets/projects-views.png)

### 보기 필터링 {#filter}

필터를 사용하여 모든 프로젝트와 활성 상태인 프로젝트 간에 전환할 수 있습니다.

![필터](assets/projects-filter.png)

### 프로젝트 선택 및 보기 {#selecting}

마우스를 프로젝트 타일 위로 가져간 다음 확인 표시를 클릭하여 프로젝트를 선택합니다.

세부 사항으로 드릴다운하려면 해당 프로젝트를 클릭하여 세부 정보를 확인합니다.

### 새 프로젝트 만들기 {#creating}

클릭 **만들기** 새 프로젝트를 추가하려면

## 프로젝트 타일 {#project-tiles}

프로젝트는 함께 관리할 다양한 유형의 정보로 구성됩니다. 이 정보는 서로 다르게 표시됩니다 **타일**.

다음 타일을 프로젝트와 연결할 수 있습니다.

* [에셋](#assets)
* [자산 컬렉션](#asset-collections)
* [경험](#experiences)
* [링크](#links)
* [프로젝트 정보](#project-info)
* [팀](#team)
* [랜딩 페이지](#landing-pages)
* [이메일](#emails)
* [워크플로우](#workflows)
* [론치](#launches)
* [작업](#tasks)

타일의 오른쪽 상단에 있는 드롭다운 메뉴를 클릭하여 타일에 데이터를 더 추가합니다.

타일의 오른쪽 하단에 있는 줄임표 단추를 클릭하여 타일의 데이터를 연결된 콘솔에서 엽니다.

### 에셋 {#assets}

**자산** 타일에서는 특정 프로젝트에 사용하는 모든 자산을 수집할 수 있습니다.

![자산 타일](assets/project-tile-assets.png)

타일에서 바로 자산을 업로드할 수 있습니다.

### 자산 컬렉션 {#asset-collections}

자산과 유사하게 [자산 컬렉션](/help/assets/manage-collections.md)도 프로젝트에 바로 추가할 수 있습니다. [자산]에서 컬렉션을 정의합니다.

![자산 수집 타일](assets/project-tile-asset-collection.png)

Add a collection by clicking **Add Collection** and selecting the appropriate collection from the list.

### 경험 {#experiences}

다음 **경험** 타일 을 통해 프로젝트에 모바일 앱, 웹 사이트 또는 게시를 추가할 수 있습니다.

![경험 타일](assets/project-tile-experiences.png)

아이콘은 표시되는 경험의 종류를 나타냅니다.

* 웹 사이트
* 모바일 애플리케이션

### 링크 {#links}

다음 **링크** 타일을 사용하면 외부 링크를 프로젝트와 연결할 수 있습니다.

![링크 타일](assets/project-tile-links.png)

링크 이름을 알아채기 쉬운 이름으로 지정할 수도 있고 썸네일을 변경할 수도 있습니다.

### 프로젝트 정보 {#project-info}

다음 **프로젝트 정보** 타일은 설명, 프로젝트 상태(비활성 또는 활성), 기한 및 구성원을 포함하여 프로젝트에 대한 일반 정보를 제공합니다. 또한 메인 프로젝트 페이지에 표시되는 프로젝트 썸네일을 추가할 수도 있습니다.

![프로젝트 정보 타일](assets/project-tile-info.png)

### 번역 작업 {#translation-job}

다음 **번역 작업** 타일은 번역을 시작하는 위치와 번역 상태가 표시되는 곳입니다.

![번역 작업 타일](assets/project-tile-translation.png)

번역을 설정하려면 문서를 참조하십시오 [번역 프로젝트 만들기](/help/assets/translation-projects.md)

### 팀 {#team}

이 타일에서는 프로젝트 팀의 구성원을 지정할 수 있습니다. 편집 시에는 팀 구성원의 이름을 입력하고 사용자 역할을 지정할 수 있습니다.

![팀 타일](assets/project-tile-team.png)

팀에서 팀 구성원을 추가하고 삭제할 수 있습니다. 또한 팀 구성원에게 지정된 [사용자 역할](#userroles)을 편집할 수도 있습니다.

### 랜딩 페이지 {#landing-pages}

****&#x200B;랜딩 페이지 타일을 사용하면 새 랜딩 페이지를 요청할 수 있습니다.

![랜딩 페이지 타일](assets/project-tile-landing.png)

이 워크플로우는 문서에 설명되어 있습니다[랜딩 페이지 워크플로우 만들기.](/help/sites-authoring/projects-with-workflows.md#request-landing-page-workflow)

### 이메일 {#emails}

이메일에 대한 요청을 관리하는 데 도움이 되는 **이메일** 타일은 이 템플릿은 **이메일 요청** 워크플로우.

![이메일 타일](assets/project-tile-email.png)

자세한 내용은 [이메일 요청 워크플로우](/help/sites-authoring/projects-with-workflows.md#request-email-workflow)에 설명되어 있습니다.

### 워크플로우 {#workflows}

프로젝트에 대한 워크플로우를 시작할 수 있습니다. 실행 중인 워크플로우가 있으면 워크플로우의 상태가 **워크플로우** 타일.

![워크플로우 타일](assets/project-tile-workflows.png)

만드는 프로젝트에 따라 사용할 수 있는 워크플로우가 다릅니다.

이에 대해서는 [프로젝트 워크플로우 작업](/help/sites-authoring/projects-with-workflows.md)에 설명되어 있습니다.

### 론치 {#launches}

다음 **론치** 타일에는 [Launch 요청 워크플로우입니다.](/help/sites-authoring/projects-with-workflows.md)

![론치 타일](assets/project-tile-launches.png)

### 작업 {#tasks}

작업을 사용하면 워크플로우를 포함하여 프로젝트 관련 작업의 상태를 모니터링할 수 있습니다. 작업은 다음 위치에서 자세히 다룹니다. [작업](/help/sites-authoring/task-content.md).

![작업 타일](assets/project-tile-tasks.png)

## 프로젝트 템플릿 {#project-templates}

템플릿은 프로젝트를 시작하는 토대 역할을 합니다. AEM에서는 이러한 표준 프로젝트 템플릿을 제공합니다.

* **미디어 프로젝트** - 미디어 관련 활동을 위한 참조 샘플 프로젝트입니다. 여기에는 여러 미디어 관련 프로젝트 역할이 포함되며 미디어 컨텐츠와 관련된 워크플로우가 포함됩니다.
* **[제품 사진 촬영 프로젝트](/help/sites-authoring/managing-product-information.md)** - eCommerce 관련 제품 사진을 관리하기 위한 참조 샘플입니다.
* **[번역 프로젝트](/help/sites-administering/translation.md)** - 번역 관련 활동을 관리하기 위한 참조 샘플입니다. 여기에는 기본 역할이 포함되며 번역 관리를 위한 워크플로우가 포함되어 있습니다.
* **단순 프로젝트** - 다른 카테고리에 맞지 않는 모든 프로젝트에 대한 참조 샘플입니다. 여기에는 3개의 기본 역할과 4개의 일반 AEM 워크플로우가 포함되어 있습니다.

선택한 템플릿에 따라 제공된 사용자 역할 및 워크플로우와 같은 프로젝트 내에서 사용할 수 있는 다양한 옵션이 있습니다.

## 프로젝트의 사용자 역할 {#user-roles-in-a-project}

다른 사용자 역할은 프로젝트 템플릿에서 정의되며 다음의 두 가지 주요 이유로 사용됩니다.

1. 권한: 사용자 역할은 나열된 세 가지 범주 중 하나에 속합니다. 관찰자, 편집자, 소유자 예를 들어, 사진사나 카피라이터는 편집자와 동일한 권한을 갖습니다. 권한은 사용자가 프로젝트의 컨텐츠에 수행할 수 있는 작업을 결정합니다.
1. 워크플로우: 워크플로우는 프로젝트에서 작업을 지정할 사용자를 결정합니다. 작업은 프로젝트 역할과 연결할 수 있습니다. 예를 들어, 작업을 사진사에게 할당하여 사진사 역할이 있는 모든 팀 구성원이 작업을 받게 합니다.

모든 프로젝트는 보안 및 제어 권한을 관리할 수 있도록 다음과 같은 기본 역할을 지원합니다.

| 역할 | 설명 | 권한 | 그룹 구성원 |
|---|---|---|---|
| 관찰자 | 이 역할의 사용자는 프로젝트 상태를 포함하여 프로젝트 세부 사항을 볼 수 있습니다. | 프로젝트에 대한 읽기 전용 권한 | `workflow-users` 그룹 |
| 편집자 | 이 역할의 사용자는 프로젝트 컨텐츠를 업로드하고 편집할 수 있습니다. | 프로젝트, 관련 메타데이터 및 관련 자산에 대한 읽기 및 쓰기 액세스 권한<br>촬영 목록 업로드, 사진 촬영, 자산 검토 및 승인 권한<br>쓰기 권한 `/etc/commerce`<br>특정 프로젝트에 대한 권한 수정 | `workflow-users` 그룹 |
| 소유자 | 이 역할의 사용자는 프로젝트를 만들고, 프로젝트에서 작업을 시작하고, 승인된 자산을 프로덕션 폴더로 이동할 수 있습니다. 소유자가 프로젝트의 다른 모든 작업을 보고 수행할 수도 있습니다. | 쓰기 권한 `/etc/commerce` | `dam-users` 프로젝트를 만들 수 있는 그룹<br>`project-administrators` 그룹을 사용하여 프로젝트를 만들고 자산을 이동할 수 있습니다 |

크리에이티브 프로젝트의 경우 사진사와 같은 추가 역할도 제공됩니다. 이러한 역할을 사용하여 특정 프로젝트의 사용자 지정 역할을 파생시킬 수 있습니다.

### 자동 그룹 만들기 {#auto-group-creation}

When you create the project and add users to the various roles, groups associated with the project are automatically created to manage associated permissions.

For example, a project called Myproject would have three groups **Myproject Owners**, **Myproject Editors**, **Myproject Observers**.

프로젝트가 삭제되면 해당 그룹은 적절한 옵션을 선택한 경우에만 삭제됩니다 [프로젝트를 삭제할 때](/help/sites-authoring/touch-ui-managing-projects.md#deleting-a-project) 관리자는 **도구** > **보안** > **그룹**.

## 추가 리소스 {#additional-resources}

프로젝트 사용에 대한 자세한 내용은 다음 추가 문서를 참조하십시오.

* [프로젝트 관리](/help/sites-authoring/touch-ui-managing-projects.md)
* [작업](/help/sites-authoring/task-content.md)
* [프로젝트 워크플로를 사용하여 작업](/help/sites-authoring/projects-with-workflows.md)
* [크리에이티브 프로젝트 및 PIM 통합](/help/sites-authoring/managing-product-information.md)
