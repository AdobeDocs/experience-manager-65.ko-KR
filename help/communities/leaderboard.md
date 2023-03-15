---
title: 리더보드 기본 사항
seo-title: Leaderboard Essentials
description: 리더보드 기능 개요
seo-description: Leaderboard feature overview
uuid: 815a6928-b147-496d-9751-13159ad1304d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 7449f99e-77d7-4c0f-96d5-b67d5e1f124a
exl-id: fd1b1749-13f9-4079-ae39-348676105852
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 5%

---

# 리더보드 기본 사항 {#leaderboard-essentials}

이 페이지에서는 리더보드 기능을 사용하는 데 필요한 기본 정보를 제공합니다.

페이지에 리더보드 구성 요소를 포함하기 전에 을 구성해야 합니다. [커뮤니티 점수 및 배지](implementing-scoring.md).

다음을 참조하십시오 [채점 및 배지 핵심 사항](configure-scoring.md).

## 클라이언트측 핵심 사항 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>소셜/게임화/구성 요소/hbs/리더보드</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>포함하기 쉬워</strong></a></td>
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
   <td>다음을 참조하십시오 <a href="enabling-leaderboard.md">리더보드 기능</a></td>
  </tr>
 </tbody>
</table>

* [클라이언트측 사용자 지정](client-customize.md)

### 파일 라이브러리 기능 {#file-library-function}

다음을 포함하는 커뮤니티 사이트 구조 [리더보드 기능](functions.md#leaderboard-function), 구성된 포함 `leaderboard` 구성 요소.
