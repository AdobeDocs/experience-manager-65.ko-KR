---
title: 평가 필수
seo-title: 평가 필수
description: 검토 및 요약 구성 요소 검토
seo-description: 검토 및 요약 구성 요소 검토
uuid: 540c106e-ee3b-4261-82b2-a909d254dbf7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 62669a9d-2107-4644-a4bf-143d0ac148b3
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 평가 필수 {#reviews-essentials}

이 기능은 함께 작동하는 두 가지 구성 요소로 구성됩니다.검토 및 검토 요약

검토는 하나 이상의 [등급](essentials-comments.md) (합계) 구성 요소를 포함하는 [주석 시스템을](rating-basics.md) 기반으로 하는 합성 구성 요소입니다.

검토의 익명 게시는 지원되지 않습니다. 사이트 방문자가 검토를 추가하려면 등록하고 로그인해야 합니다. 로그인한 방문자(회원)는 언제든지 검토를 업데이트할 수 있습니다.

## Essentials for Client-Side {#essentials-for-client-side}

### 검토 {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/reviews/components/hbs/reviews</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>includable</strong></a></td>
   <td>예 - <i>디자인 </i>모드에서 속성을 편집할 수 있습니다.</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
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
   <td>검토 <a href="reviews.md">사용 참조</a></td>
  </tr>
 </tbody>
</table>

### 리뷰 요약 {#review-summary}

| **resourceType** | social/reviews/components/hbs/summary |
|---|---|
| [**includable **](scf.md#add-or-include-a-communities-component) | 예 - 속성은 *design *mode에서 편집할 수 있습니다. |
| [**clientlibs **](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **템플릿** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **속성** | 검토 [사용 참조](reviews.md) |

* [클라이언트측 사용자 정의](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API 검토](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [끝점 검토](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [서버측 사용자 정의](server-customize.md)

### 게시된 검토 액세스(UGC) {#accessing-posted-reviews-ugc}

UGC는 중재에 대한 표준 방법 중 하나를 사용하여 중재해야 합니다.
사용자 [생성 컨텐츠 중재를 참조하십시오](moderate-ugc.md).

AEM 6.1 Communities의 경우, UGC용 [공용 스토어를](working-with-srp.md) 사용하면 선택한 스토리지 옵션(예: ASRP, MSRP 또는 JSRP)에 상관없이 프로그래머틱 방식으로 UGC에 액세스할 수 있습니다.

**저장소에서 UGC의 위치와 형식은 경고**&#x200B;없이 변경될 수 있습니다.

다음을 참조하십시오.

* [스토리지 자원 공급자 개요](srp.md) - 소개 및 저장소 사용 개요
* [SRP 및 UGC Essentials](srp-and-ugc.md) - SRP 유틸리티 방법 및 예제
* [SRP를 사용하여 UGC](accessing-ugc-with-srp.md) 액세스 - 코딩 지침
* [SocialUtils 리팩토링](socialutils.md) - 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑

