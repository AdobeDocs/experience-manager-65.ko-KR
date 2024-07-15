---
title: 등급 기본 사항
description: Tally 하위 클래스인 등급 구성 요소를 통해 로그인한 커뮤니티 구성원이 웹 사이트에서 기능을 평가하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 49456944-ff0d-4507-b3b8-143c90067573
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---

# 등급 기본 사항 {#rating-essentials}

[tally](tally.md) 하위 클래스인 등급 구성 요소를 사용하여 로그인한 커뮤니티 구성원이 웹 사이트의 기능에 대한 등급을 지정할 수 있습니다.

동일한 페이지에 투표 구성 요소의 여러 인스턴스를 배치할 수 있습니다. 각 인스턴스는 고유한 `tally name` 속성으로 구성해야 합니다.

등급의 익명 게시는 지원되지 않습니다. 사이트 방문자가 등급에 한 번만 참여하려면 등록하고 로그인해야 합니다. 로그인한 방문자(구성원)는 언제든지 등급을 변경할 수 있습니다.

## 클라이언트측 핵심 사항 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/tally/components/hbs/rating</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>포함 가능</strong></a></td>
   <td>예 - 속성은 <i>디자인 </i> 모드에서 편집할 수 있습니다.</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
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
   <td><p><a href="rating.md">등급 사용</a>을 참조하세요.</p> </td>
  </tr>
 </tbody>
</table>

* [클라이언트측 사용자 지정](client-customize.md)

## 서버측 Essentials {#essentials-for-server-side}

* [Tally API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Tally 끝점](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [서버측 사용자 지정](server-customize.md)

### UGC(게시된 등급)에 액세스 {#accessing-posted-ratings-ugc}

UGC는 중재에 대한 표준 방법 중 하나를 사용하여 중재되어야 합니다.
[사용자 생성 콘텐츠 중재](moderate-ugc.md)를 참조하십시오.

AEM 6.1 커뮤니티에서 UGC에 대한 [일반 저장소](working-with-srp.md)를 사용하면 선택한 저장소 옵션(예: ASRP, MSRP 또는 JSRP)에 관계없이 UGC에 프로그래밍 방식으로 액세스할 수 있습니다.

**저장소에서 UGC의 위치 및 형식은 경고 없이 변경될 수 있습니다**.

다음을 참조하십시오.

* [저장소 리소스 공급자 개요](srp.md) - 소개 및 저장소 사용 개요.
* [SRP 및 UGC Essentials](srp-and-ugc.md) - SRP 유틸리티 메서드 및 예제.
* [SRP를 사용하여 UGC에 액세스](accessing-ugc-with-srp.md) - 코딩 지침.
* [SocialUtils 리팩터링](socialutils.md) - 더 이상 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.
