---
title: 리뷰 Essentials
description: AEM Communities의 리뷰가 하나 이상의 등급(tally) 구성 요소가 포함된 댓글 시스템을 기반으로 하는 복합 구성 요소인 방법에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 91e0e245-a2f1-4bd7-b38f-7641fd94a547
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 1%

---

# 리뷰 Essentials {#reviews-essentials}

이 기능은 검토 및 검토 요약의 두 가지 구성 요소로 구성됩니다.

리뷰는 하나 이상의 [등급](rating-basics.md)(tally) 구성 요소를 포함하는 [댓글 시스템](essentials-comments.md)을 기반으로 하는 복합 구성 요소입니다.

검토의 익명 게시는 지원되지 않습니다. 리뷰를 추가하려면 사이트 방문자를 등록하고 로그인해야 합니다. 로그인한 방문자(구성원)는 언제든지 검토를 업데이트할 수 있습니다.

## 클라이언트측 핵심 사항 {#essentials-for-client-side}

### 리뷰 {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>소셜/리뷰/구성 요소/hbs/리뷰</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>포함 가능</strong></a></td>
   <td>예 - 속성은 <i>디자인 </i> 모드에서 편집할 수 있습니다.</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.reviews</td>
  </tr>
  <tr>
   <td> <strong>템플릿</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/reviews.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/review.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/status.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/toolbar.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/clientlibs/review.css</td>
  </tr>
  <tr>
   <td><strong>속성</strong></td>
   <td><a href="reviews.md">리뷰 사용</a> 보기</td>
  </tr>
 </tbody>
</table>

### 요약 검토 {#review-summary}

| **resourceType** | 소셜/리뷰/구성 요소/hbs/요약 |
|---|---|
| [**포함 가능**](scf.md#add-or-include-a-communities-component) | 예 - *디자인 *모드에서 속성을 편집할 수 있습니다. |
| [**clientllibs**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **템플릿** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **속성** | [리뷰 사용](reviews.md) 보기 |

* [클라이언트측 사용자 지정](client-customize.md)

## 서버측 Essentials {#essentials-for-server-side}

* [API 검토](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [끝점 검토](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [서버측 사용자 지정](server-customize.md)

### 게시된 리뷰 액세스(UGC) {#accessing-posted-reviews-ugc}

UGC는 중재에 대한 표준 방법 중 하나를 사용하여 중재되어야 합니다.
[사용자 생성 콘텐츠 중재](moderate-ugc.md)를 참조하십시오.

AEM 6.1 커뮤니티에서 UGC에 대한 [일반 저장소](working-with-srp.md)를 사용하면 선택한 저장소 옵션(예: ASRP, MSRP 또는 JSRP)에 관계없이 UGC에 프로그래밍 방식으로 액세스할 수 있습니다.

**저장소에서 UGC의 위치 및 형식은 경고 없이 변경될 수 있습니다**.

다음을 참조하십시오.

* [저장소 리소스 공급자 개요](srp.md) - 소개 및 저장소 사용 개요.
* [SRP 및 UGC Essentials](srp-and-ugc.md) - SRP 유틸리티 메서드 및 예제.
* [SRP를 사용하여 UGC에 액세스](accessing-ugc-with-srp.md) - 코딩 지침.
* [SocialUtils 리팩터링](socialutils.md) - 더 이상 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.
