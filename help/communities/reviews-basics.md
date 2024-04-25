---
title: 리뷰 필수 사항
description: AEM Communities 리뷰가 하나 이상의 등급(집계) 구성 요소를 포함하는 댓글 시스템을 기반으로 하는 복합 구성 요소인 방법에 대해 알아봅니다.
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

# 리뷰 필수 사항 {#reviews-essentials}

이 기능은 함께 작동하는 두 가지 구성 요소인 리뷰와 리뷰 요약으로 구성됩니다.

리뷰는 하나 이상의 [평점](rating-basics.md)(집계) 구성 요소를 포함하는 댓글 시스템을](essentials-comments.md) 기반으로 하는 [복합 구성 요소입니다.

리뷰를 익명으로 게시하는 것은 지원되지 않습니다. 검토를 추가하려면 사이트 방문자가 등록하고 로그인해야 합니다. 로그인한 방문자(구성원)는 언제든지 리뷰를 업데이트할 수 있습니다.

## 클라이언트측 필수 사항 {#essentials-for-client-side}

### 리뷰 {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>Resourcetype</strong></td>
   <td>소셜/리뷰/구성 요소/HBS/리뷰</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>포함 가능</strong></a></td>
   <td>예 - 디자인 </i>모드에서 속성을 편집할 수 있습니다<i>.</td>
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
   <td> <strong>Css</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/clientlibs/review.css</td>
  </tr>
  <tr>
   <td><strong>속성</strong></td>
   <td>리뷰 사용을 참조하십시오 <a href="reviews.md"></a></td>
  </tr>
 </tbody>
</table>

### 요약 검토 {#review-summary}

| **Resourcetype** | 소셜/리뷰/구성 요소/HBS/요약 |
|---|---|
| [**포함 가능**](scf.md#add-or-include-a-communities-component) | 예 - *디자인 *모드에서 속성을 편집할 수 있습니다. |
| [**clientllibs**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **템플릿** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **Css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **속성** | 리뷰 사용을 참조하십시오 [](reviews.md) |

* [클라이언트측 사용자 지정](client-customize.md)

## 서버측 필수 사항 {#essentials-for-server-side}

* [API 검토](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [엔드포인트 검토](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [서버 측 사용자 지정](server-customize.md)

### 게시된 리뷰(UGC) 액세스 {#accessing-posted-reviews-ugc}

UGC는 표준 중재 방법 중 하나를 사용하여 중재해야 합니다.
사용자 생성 컨텐츠](moderate-ugc.md) 중재를 참조하십시오[.

AEM 6.1 Communities부터 UGC용 공통 스토어](working-with-srp.md)를 사용하면 [선택한 스토리지 옵션(예: ASRP, MSRP 또는 JSRP)에 관계없이 UGC에 프로그래밍 방식으로 액세스할 수 있습니다.

**저장소에서 UGC의 위치 및 포맷 및 형식은 경고** 없이 변경될 수 있습니다.

다음을 참조하십시오.

* [저장소 리소스 공급자 개요](srp.md) - 소개 및 저장소 사용 개요입니다.
* [SRP 및 UGC Essentials](srp-and-ugc.md) - SRP 유틸리티 메서드 및 예제.
* [SRP](accessing-ugc-with-srp.md) 로 UGC 액세스 - 코딩 지침.
* [SocialUtils 리팩토링](socialutils.md) - 더 이상 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.
