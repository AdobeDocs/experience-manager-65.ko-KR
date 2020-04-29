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
source-git-commit: 3296db289b2e2f4ca0d1981597ada6ca1310bd46

---


# 소셜 그래프 사용 {#using-social-graph}

## 소개 {#introduction}

커뮤니티 구성원이 [활동을](activities.md) 따르고 따라야 하는 기능은 다음 두 가지 구성 요소를 통해 결정됩니다. `Follow` 및 `Following`Adobe

구성 `Follow` 요소는 다른 리소스와 연결되어 있어야 하며 이 연결은 이미 커뮤니티 구성원 및 기능에 대해 설정되었습니다.

구성 요소에는 현재 멤버를 팔로우하거나 현재 멤버를 팔로우하는 멤버가 나열됩니다. `Following` 구성원 간의 관계에 대한 이 소셜 그래프는 [커뮤니티 사이트에](overview.md#communitiessites)대해 설정된 사용자 프로필에 포함됩니다.

## 페이지에 팔로우 추가 {#adding-following-to-a-page}

작성 모드에서 페이지에 구성 요소를 추가하려면 구성 요소를 찾아 소셜 그래프가 표시되어야 하는 페이지에 `Following` `Communities / Following` 놓습니다.

필요한 정보를 보려면 커뮤니티 구성 [요소 기본 사항을 참조하십시오](basics.md).

필요한 [클라이언트측 라이브러리가](essentials-socialgraph.md#essentials-for-client-side) `Following` 포함되어 있으면 구성 요소가 표시되는 방식입니다.

![chlimage_1-447](assets/chlimage_1-447.png)

## 다음 구성 {#configuring-following}

현재, 속성을 설정하여 구성 요소에 `follows` 관계 또는 관계가 표시되는지 여부를 결정해야 합니다 `following` .

## 추가 정보 {#additional-information}

개발자를 위한 소셜 그래프 필수 [사항](essentials-socialgraph.md) 페이지에서 자세한 내용을 확인할 수 있습니다.
