---
title: 리더보드 기본 사항
description: Adobe Experience Manager 커뮤니티에서 순위표 구성 요소로 작업할 수 있도록 커뮤니티 점수 및 배지를 구성하는 방법에 대해 알아봅니다.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: fd1b1749-13f9-4079-ae39-348676105852
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 4%

---

# 리더보드 기본 사항 {#leaderboard-essentials}

이 페이지에서는 리더보드 기능을 사용하는 데 필요한 기본 정보를 제공합니다.

페이지에 순위표 구성 요소를 포함하기 전에 [커뮤니티 점수 및 배지](implementing-scoring.md)를 구성해야 합니다.

[채점 및 배지 기본 사항](configure-scoring.md)을 참조하세요.

## 클라이언트측 핵심 사항 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>소셜/게임화/구성 요소/hbs/리더보드</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>포함 가능</strong></a></td>
   <td>아니요</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.gamification.hbs.leaderboard</td>
  </tr>
  <tr>
   <td> <strong>템플릿</strong></td>
   <td> /libs/social/gamification/components/hbs/leaderboard/leaderboard.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/gamification/components/hbs/leaderboard/clientlibs/leaderboard.css</td>
  </tr>
  <tr>
   <td><strong> 속성</strong></td>
   <td><a href="enabling-leaderboard.md">순위표 기능</a> 보기</td>
  </tr>
 </tbody>
</table>

* [클라이언트측 사용자 지정](client-customize.md)

### 파일 라이브러리 기능 {#file-library-function}

[리더보드 함수](functions.md#leaderboard-function)이(가) 포함된 커뮤니티 사이트 구조에는 구성된 `leaderboard` 구성 요소가 포함되어 있습니다.
