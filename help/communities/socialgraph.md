---
title: 소셜 그래프 사용
description: 로그인한 커뮤니티 구성원이 활동을 팔로우하거나 팔로우할 수 있도록 페이지에 다음 구성 요소를 추가하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---

# 소셜 그래프 사용 {#using-social-graph}

## 소개 {#introduction}

커뮤니티 구성원이 [활동](activities.md)을 팔로우하고 팔로우할 수 있는 기능은 `Follow` 및 `Following` 구성 요소를 통해 설정됩니다.

`Follow` 구성 요소는 다른 리소스와 연결되어 있어야 하며 이 연결은 커뮤니티 구성원 및 기능에 대해 이미 설정되어 있습니다.

`Following` 구성 요소는 현재 멤버 뒤에 있거나 현재 멤버가 뒤에 있는 멤버를 나열할 뿐입니다. 구성원 간의 관계에 대한 이 소셜 그래프는 [커뮤니티 사이트](overview.md#communitiessites)에 대해 설정된 사용자 프로필에 포함되어 있습니다.

## 페이지에 다음 추가 {#adding-following-to-a-page}

작성자 모드에서 페이지에 `Following` 구성 요소를 추가하려면 구성 요소 `Communities / Following`을(를) 찾아 소셜 그래프가 표시될 페이지로 드래그합니다.

필요한 정보는 [커뮤니티 구성 요소 기본 사항](basics.md)을 참조하세요.

[필수 클라이언트측 라이브러리](essentials-socialgraph.md#essentials-for-client-side)가 포함된 경우 `Following` 구성 요소는 다음과 같이 표시됩니다.

![팔로우](assets/following.png)

## 다음 구성 {#configuring-following}

현재 속성을 설정하여 구성 요소가 `follows` 관계를 표시하는지 또는 `following` 관계를 표시하는지 확인해야 합니다.

## 추가 정보 {#additional-information}

자세한 내용은 개발자를 위한 [Social Graph Essentials](essentials-socialgraph.md) 페이지에서 확인할 수 있습니다.
