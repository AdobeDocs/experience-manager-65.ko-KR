---
title: 관념화 기본 사항
description: 포럼과 유사하지만 보다 공동 작업 느낌이 있는 커뮤니티의 관념화 기능 작업의 기본 사항에 대해 알아봅니다.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 7ad3592b-f8b5-45c0-97bc-15f781d7b811
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 3%

---

# 관념화 기본 사항 {#ideation-essentials}

이 페이지는 포럼과 유사하지만 초안으로 저장할 수 있는 기능과 공동 작업 환경을 갖춘 관념화 기능 작업에 필요한 필수 정보를 제공합니다.

## 클라이언트측 핵심 사항 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/ideation/components/hbs/ideation</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>포함 가능</strong></a></td>
   <td>아니요</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.voting<br /> cq.social.hbs.liking<br /> cq.social.hbs.ideation</td>
  </tr>
  <tr>
   <td> <strong>템플릿</strong></td>
   <td> /libs/social/ideation/components/hbs/ideation/ideation.hbs<br /> /libs/social/ideation/components/hbs/ideation/ideationlists.hbs<br /> /libs/social/ideation/components/hbs/ideation/composer.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/ideation/components/hbs/ideation/clientlibs/ideation.css</td>
  </tr>
  <tr>
   <td><strong> 속성</strong></td>
   <td><a href="ideation-feature.md">관념화 기능</a>을 참조하세요.</td>
  </tr>
 </tbody>
</table>

* [클라이언트측 사용자 지정](client-customize.md)

### 관념화 기능 {#ideation-function}

[Ideation 함수](functions.md#ideation-function)이(가) 포함된 커뮤니티 사이트 구조에는 구성된 `ideation` 구성 요소가 포함되어 있습니다.
