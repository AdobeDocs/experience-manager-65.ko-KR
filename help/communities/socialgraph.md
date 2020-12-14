---
title: 소셜 그래프 사용
seo-title: 소셜 그래프 사용
description: 페이지에 다음 구성 요소 추가
seo-description: 페이지에 다음 구성 요소 추가
uuid: 8be6334b-e6c9-40bc-90a8-750b98419470
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 0ce57ab1-e4c6-4c38-963d-556eef8757f2
translation-type: tm+mt
source-git-commit: 1429a099288f038510cb0a194fb55632297ef371
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---


# 소셜 그래프 사용 {#using-social-graph}

## 소개 {#introduction}

다음 두 구성 요소를 통해 [활동](activities.md)과(와) 함께 커뮤니티 멤버가 수행할 수 있습니다.`Follow` 및 `Following`.

`Follow` 구성 요소는 다른 리소스와 연결되어 있어야 하며 이 연결은 이미 커뮤니티 구성원 및 기능에 대해 설정되어 있습니다.

`Following` 구성 요소에는 현재 구성원을 팔로우하거나 현재 구성원이 뒤에 오는 멤버가 나열됩니다. 구성원 간의 관계에 대한 이 소셜 그래프는 [커뮤니티 사이트](overview.md#communitiessites)에 대해 설정된 사용자 프로필에 포함됩니다.

## {#adding-following-to-a-page} 페이지에 다음 추가

작성 모드에서 페이지에 `Following` 구성 요소를 추가하려면 구성 요소 `Communities / Following`을 찾아 소셜 그래프가 표시되어야 하는 페이지에 배치합니다.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](basics.md)을 방문하십시오.

[필수 클라이언트측 라이브러리](essentials-socialgraph.md#essentials-for-client-side)가 포함될 때 `Following` 구성 요소가 표시되는 방식입니다.

![following](assets/following.png)

## 다음 {#configuring-following} 구성

현재, 구성 요소에 `follows` 관계가 표시되는지 또는 `following` 관계가 표시되는지 확인하기 위해 속성을 설정해야 합니다.

## 추가 정보 {#additional-information}

개발자를 위한 [Social Graph Essentials](essentials-socialgraph.md) 페이지에 자세한 내용이 표시될 수 있습니다.
