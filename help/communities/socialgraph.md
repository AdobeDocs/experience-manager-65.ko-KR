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
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---

# 소셜 그래프 사용 {#using-social-graph}

## 소개 {#introduction}

커뮤니티 구성원이 [활동](activities.md)을 따르고 따를 수 있는 기능은 두 가지 구성 요소를 통해 설정됩니다.`Follow` 및 `Following`.

`Follow` 구성 요소는 다른 리소스와 연결되어 있어야 하며 이 연결은 이미 커뮤니티 구성원 및 기능에 대해 설정되어 있습니다.

`Following` 구성 요소는 현재 멤버를 따르거나 현재 멤버가 뒤에 오는 멤버를 나열합니다. 구성원 간의 관계에 대한 이 소셜 그래프는 [커뮤니티 사이트](overview.md#communitiessites)에 대해 설정된 사용자 프로필에 포함되어 있습니다.

## 페이지에 다음 추가 {#adding-following-to-a-page}

작성자 모드의 페이지에 `Following` 구성 요소를 추가하려면 구성 요소 `Communities / Following`을 찾아 소셜 그래프가 나타나는 페이지에 배치합니다.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](basics.md)을 방문하십시오.

필요한 [클라이언트 측 라이브러리](essentials-socialgraph.md#essentials-for-client-side)가 포함된 경우 이 방법으로 `Following` 구성 요소가 표시됩니다.

![다음](assets/following.png)

## 다음 {#configuring-following} 구성

현재 속성을 설정하여 구성 요소에 `follows` 관계가 표시되는지 또는 `following` 관계가 표시되는지를 확인해야 합니다.

## 추가 정보 {#additional-information}

개발자를 위한 [Social Graph Essentials](essentials-socialgraph.md) 페이지에서 자세한 내용을 볼 수 있습니다.
