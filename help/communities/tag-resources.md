---
title: 태깅 지원 리소스
seo-title: 태깅 지원 리소스
description: 활성 리소스 태깅을 통해 구성원이 카탈로그를 검색할 때 리소스 및 학습 경로를 필터링할 수 있습니다
seo-description: 활성 리소스 태깅을 통해 구성원이 카탈로그를 검색할 때 리소스 및 학습 경로를 필터링할 수 있습니다
uuid: daf8a4f4-486b-498c-99e9-d1533a830e64
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c012d639-c6e6-4f73-bbd8-78a4baa38c17
translation-type: tm+mt
source-git-commit: 2fcd87cd1def7fc265ba40c83b50db86618f3b70
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---


# 태깅 지원 리소스 {#tagging-enablement-resources}

## 개요 {#overview}

활성 리소스 태깅을 통해 구성원이 카탈로그를 검색할 때 리소스와 학습 경로를 필터링할 수 [있습니다](functions.md#catalog-function).

본질적으로:

* [각 카탈로그에 대한 태그 네임스페이스](../../help/sites-administering/tags.md#creating-a-namespace) 만들기

   * [태그 권한 설정](../../help/sites-administering/tags.md#setting-tag-permissions)
   * 커뮤니티 멤버만(폐쇄된 커뮤니티)

      * 커뮤니티 사이트의 [구성원 그룹에 대한 읽기 액세스 허용](users.md#publish-group-roles)
   * 로그인 또는 익명(개방형 커뮤니티) 사이트 방문자

      * 그룹에 대한 읽기 액세스 `Everyone` 허용
   * [태그 게시](../../help/sites-administering/tags.md#publishing-tags)



* [커뮤니티 사이트의 태그 범위 정의](sites-console.md#tagging)

   * [사이트 구조에 존재하는 카탈로그 구성](functions.md#catalog-function)

      * 카탈로그 인스턴스에 태그를 추가하여 UI 필터에 표시된 태그 목록을 제어할 수 있습니다.
      * 사전 [필터를 추가하여](catalog-developer-essentials.md#pre-filters)카탈로그의 포함 리소스를 제한할 수 있습니다.

* [커뮤니티 사이트 게시](sites-console.md#publishing-the-site)
* [활성 리소스에](resources.md#create-a-resource) 태그를 적용하여 일괄적으로 필터링할 수 있습니다.
* [활성 리소스 게시](resources.md#publish)

## 커뮤니티 사이트 태그 {#community-site-tags}

커뮤니티 사이트를 만들거나 편집할 때 [태그 지정 설정은](sites-console.md#tagging) 기존 태그 네임스페이스의 하위 집합을 선택하여 사이트의 기능에 사용할 수 있는 태그의 범위를 설정합니다.

언제든지 태그를 만들어 커뮤니티 사이트에 추가할 수 있지만 데이터베이스를 디자인하는 것과 유사하게 택소노미를 미리 디자인하는 것이 좋습니다. 태그 [사용을 참조하십시오](../../help/sites-authoring/tags.md).

나중에 기존 커뮤니티 사이트에 태그를 추가할 때 사이트 구조의 카탈로그 기능에 새 태그를 추가하기 전에 편집을 저장해야 합니다.

커뮤니티 사이트의 경우 사이트가 게시되고 태그가 게시된 후 커뮤니티 구성원에 대한 읽기 액세스를 활성화해야 합니다. 태그 [권한 설정을 참조하십시오](../../help/sites-administering/tags.md#setting-tag-permissions).

다음은 관리자가 그룹에 대한 읽기 권한을 적용할 때 CRXDE에 표시되는 방식 `/etc/tags/ski-catalog` 입니다 `Community Enable Members`.

![site-tags](assets/site-tags.png)

## 카탈로그 태그 네임스페이스 {#catalog-tag-namespaces}

카탈로그 기능은 태그를 사용하여 자신을 정의합니다. 커뮤니티 사이트에서 카탈로그 기능을 구성할 때 선택할 태그 네임스페이스 세트는 커뮤니티 사이트에 대해 설정된 태그 네임스페이스의 범위에 의해 정의됩니다.

카탈로그 함수에는 카탈로그의 필터 UI에 나열된 태그를 정의하는 태그 설정이 포함됩니다. &quot;모든 네임스페이스&quot; 설정은 커뮤니티 사이트에서 선택한 태그 네임스페이스의 범위를 나타냅니다.

![catalog-namespace](assets/catalog-namespace.png)

## 활성 리소스에 태그 적용 {#applying-tags-to-enablement-resources}

선택하면 활성 리소스 및 학습 경로가 모든 카탈로그에 `Show in Catalog` 표시됩니다. 리소스 및 학습 경로에 태그를 추가하면 카탈로그 UI에서 필터링할 뿐만 아니라 특정 카탈로그에 대한 사전 필터링을 수행할 수 있습니다.

사전 필터를 만들어 활성 리소스 및 특정 카탈로그에 대한 학습 경로 [를 제한합니다](catalog-developer-essentials.md#pre-filters).

카탈로그 UI를 사용하면 방문자가 해당 카탈로그에 나타나는 리소스 및 학습 경로 목록에 태그 필터를 적용할 수 있습니다.

활성 리소스에 태그를 적용하는 관리자는 분류와 카탈로그와 관련된 태그 네임스페이스와 분류법에 대해 알아야 합니다.

예를 들어 이름이 지정된 카탈로그에 `ski-catalog` 네임스페이스를 만들고 설정한 경우 두 개의 하위 태그 `Ski Catalog`가 있을 수 있습니다. `lesson-1` 및 `lesson-2`.

따라서 다음 중 하나로 태그된 활성 리소스

* 스키 카탈로그:레슨-1
* 스키 카탈로그:레슨-2

활성 리소스가 게시된 `Ski Catalog` 후에 표시됩니다.

![basic-info](assets/applytags-basicinfo.png)

## 게시할 때 카탈로그 보기 {#viewing-catalog-on-publish}

작성 환경에서 모든 것이 설정되고 게시되면 카탈로그를 사용하여 역량 강화 리소스를 찾는 경험이 게시 환경에서 발생할 수 있습니다.

태그 네임스페이스가 드롭다운에 나타나지 않으면 게시 환경에서 권한이 제대로 설정되었는지 확인하십시오.

태그 네임스페이스가 추가되고 누락된 경우 태그 및 사이트가 다시 게시되었는지 확인하십시오.

카탈로그를 볼 때 태그를 선택한 후 활성 리소스가 나타나지 않는 경우, 카탈로그 네임스페이스의 태그가 활성 리소스에 적용되었는지 확인하십시오.

![카탈로그 보기](assets/viewcatalog.png)

