---
title: 소셜 그래프 사용
seo-title: Using Social Graph
description: 페이지에 다음 구성 요소 추가
seo-description: Adding a Following component to a page
uuid: 8be6334b-e6c9-40bc-90a8-750b98419470
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 0ce57ab1-e4c6-4c38-963d-556eef8757f2
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---

# 소셜 그래프 사용 {#using-social-graph}

## 소개 {#introduction}

커뮤니티 회원이 팔로우할 수 있는 기능 [활동](activities.md) 및 는 다음 두 가지 구성 요소를 통해 설정됩니다. `Follow` 및 `Following`.

다음 `Follow` 구성 요소는 다른 리소스와 연결되어 있어야 하며 커뮤니티 구성원 및 기능에 대해 이 연결이 이미 설정되어 있습니다.

다음 `Following` 구성 요소는 현재 멤버 다음에 오는 멤버나 현재 멤버가 뒤에 오는 멤버를 나열합니다. 구성원 간의 관계에 대한 이 소셜 그래프는 다음에 대해 설정된 사용자 프로필에 포함됩니다 [커뮤니티 사이트](overview.md#communitiessites).

## 페이지에 다음 추가 {#adding-following-to-a-page}

를 추가하려는 경우 `Following` 구성 요소를 페이지에 추가하려면 작성자 모드에서 구성 요소를 찾습니다. `Communities / Following` 소셜 그래프가 표시될 위치에 끌어서 놓습니다.

필요한 정보는 다음을 참조하십시오. [커뮤니티 구성 요소 기본 사항](basics.md).

다음의 경우 [필수 클라이언트측 라이브러리](essentials-socialgraph.md#essentials-for-client-side) 포함됩니다. 이렇게 하면 `Following` 구성 요소가 표시됩니다.

![팔로잉](assets/following.png)

## 다음 구성 {#configuring-following}

현재 속성을 설정하여 구성 요소가 를 표시하는지 여부를 확인해야 합니다. `follows` 관계 또는 `following` 관계.

## 추가 정보 {#additional-information}

자세한 내용은 [소셜 그래프 기본 사항](essentials-socialgraph.md) 개발자용 페이지입니다.
