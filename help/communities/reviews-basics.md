---
title: 검토 핵심 사항
seo-title: 검토 핵심 사항
description: 요약 구성 요소 검토 및 검토
seo-description: 요약 구성 요소 검토 및 검토
uuid: 540c106e-ee3b-4261-82b2-a909d254dbf7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 62669a9d-2107-4644-a4bf-143d0ac148b3
exl-id: 91e0e245-a2f1-4bd7-b38f-7641fd94a547
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 1%

---

# 검토 필수 항목 {#reviews-essentials}

이 기능은 함께 작동하는 두 구성 요소로 구성됩니다.검토 및 검토 요약

리뷰는 하나 이상의 [rating](rating-basics.md) (tally) 구성 요소를 포함하는 [주석 시스템](essentials-comments.md)을 기반으로 하는 복합 구성 요소입니다.

검토의 익명 게시는 지원되지 않습니다. 사이트 방문자가 검토를 추가하려면 등록하고 로그인해야 합니다. 로그인한 방문자(구성원)는 언제든지 검토를 업데이트할 수 있습니다.

## 클라이언트측 {#essentials-for-client-side}에 대한 필수 사항

### 검토 {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>소셜/리뷰스/구성 요소/hbs/리뷰</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>포함 가능</strong></a></td>
   <td>예 - 속성은 <i>디자인 </i>모드에서 편집할 수 있습니다</td>
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
   <td><a href="reviews.md">검토 사용</a> 을 참조하십시오.</td>
  </tr>
 </tbody>
</table>

### 리뷰 요약 {#review-summary}

| **resourceType** | social/reviews/components/hbs/summary |
|---|---|
| [**포함 가능**](scf.md#add-or-include-a-communities-component) | 예 - 속성은 *디자인 *모드에서 편집할 수 있습니다. |
| [**clientlibs**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **템플릿** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **속성** | [검토 사용](reviews.md) 을 참조하십시오. |

* [클라이언트측 사용자 지정](client-customize.md)

## 서버측 {#essentials-for-server-side}에 대한 필수 사항

* [검토 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [검토 끝점](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [서버측 사용자 지정](server-customize.md)

### 게시된 검토 액세스(UGC) {#accessing-posted-reviews-ugc}

조정을 위한 표준 방법 중 하나를 사용하여 UGC가 중재되어야 합니다.
[사용자가 생성한 콘텐츠 중재](moderate-ugc.md)를 참조하십시오.

AEM 6.1 Communities에서 UGC용 [공용 스토어](working-with-srp.md)를 사용하면 선택한 저장소 옵션(예: ASRP, MSRP 또는 JSRP)에 관계없이 UGC에 프로그래밍 방식으로 액세스할 수 있습니다.

**저장소에서 UGC의 위치와 형식은 경고** 없이 변경될 수 있습니다.

다음을 참조하십시오.

* [저장소 리소스 공급자 개요](srp.md)  - 소개 및 저장소 사용 개요.
* [SRP 및 UGC Essentials](srp-and-ugc.md)  - SRP 유틸리티 메서드 및 예제.
* [SRP를 사용하여 UGC 액세스](accessing-ugc-with-srp.md)  - 코딩 지침.
* [SocialUtils 리팩터링](socialutils.md)  - 사용 중단된 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.
