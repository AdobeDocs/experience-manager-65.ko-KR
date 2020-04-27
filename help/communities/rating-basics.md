---
title: 등급 필수
seo-title: 등급 필수
description: 등급 구성 요소 개요
seo-description: 등급 구성 요소 개요
uuid: 48ef61ad-be7a-4a6b-a284-23e5bb4f1671
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 7dc3ef57-05c3-45d4-ace3-bb3ba6ea768b
translation-type: tm+mt
source-git-commit: b7318370c45f37a7faf5434b2de3f145b8d64bce

---


# 등급 필수 {#rating-essentials}

집계 [](tally.md) 하위 클래스인 등급 구성 요소를 사용하면 커뮤니티 구성원이 웹 사이트의 기능을 평가할 수 있습니다.

동일한 페이지에 투표 구성 요소의 여러 인스턴스를 배치할 수 있습니다.각 인스턴스는 고유한 `tally name` 속성으로 구성해야 합니다.

등급 게시는 지원되지 않습니다. 사이트 방문자가 한 번만 등급에 참여하려면 등록하고 로그인해야 합니다. 로그인한 방문자(회원)는 언제든지 등급을 변경할 수 있습니다.

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/tally/components/hbs/rating</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>includable</strong></a></td>
   <td>예 - <i>디자인 </i>모드에서 속성을 편집할 수 있습니다.</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs를</strong></a></td>
   <td> cq.social.hbs.rating</td>
  </tr>
  <tr>
   <td> <strong>템플릿</strong></td>
   <td><p> /libs/social/tally/components/hbs/rating/rating.hbs<br /> /libs/social/tally/components/hbs/rating/display.hbs<br /> /libs/social/tally/components/hbs/rating/histogram.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/rating/clientlibs/ratingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>속성</strong></td>
   <td><p>등급 <a href="rating.md">사용 참조</a></p> </td>
  </tr>
 </tbody>
</table>

* [클라이언트측 사용자 정의](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [Tally API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Tally Endpoints](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [서버측 사용자 정의](server-customize.md)

### 게시된 등급(UGC) 액세스 {#accessing-posted-ratings-ugc}

UGC는 중재에 대한 표준 방법 중 하나를 사용하여 중재해야 합니다.
사용자 [생성 컨텐츠 중재를 참조하십시오](moderate-ugc.md).

AEM 6.1 Communities의 경우, UGC용 [공용 스토어를](working-with-srp.md) 사용하면 선택한 스토리지 옵션(예: ASRP, MSRP 또는 JSRP)에 상관없이 프로그래머틱 방식으로 UGC에 액세스할 수 있습니다.

**저장소에서 UGC의 위치와 형식은 경고**&#x200B;없이 변경될 수 있습니다.

다음을 참조하십시오.

* [스토리지 자원 공급자 개요](srp.md) - 소개 및 저장소 사용 개요
* [SRP 및 UGC Essentials](srp-and-ugc.md) - SRP 유틸리티 방법 및 예
* [SRP를 사용하여 UGC에](accessing-ugc-with-srp.md) 액세스 - 코딩 지침
* [SocialUtils 리팩토링](socialutils.md) - 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.

