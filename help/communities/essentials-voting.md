---
title: 투표 기본 사항
description: 구성원이 의견을 표시하기 위해 위쪽 또는 아래쪽 화살표를 선택하여 특정 콘텐츠에 대한 등급을 지정할 수 있는 투표 구성 요소를 사용하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: e8ff751f-404a-498d-8e90-62a13ab593ff
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 1%

---

# 투표 기본 사항 {#voting-essentials}

투표 구성 요소인 [tally](tally.md) 하위 클래스는 구성원이 의견을 표시하기 위해 위쪽 또는 아래쪽 화살표를 선택하여 특정 콘텐츠에 대한 등급을 매길 수 있는 유용한 도구입니다.

동일한 페이지에 투표 구성 요소의 여러 인스턴스를 배치할 수 있습니다. 각 인스턴스는 고유한 `tally name` 속성으로 구성해야 합니다.

투표의 익명 게시는 지원되지 않습니다. 사이트 방문자가 한 번만 투표에 참여하려면 등록하고 로그인해야 합니다. 로그인한 방문자(구성원)는 언제든지 투표를 변경할 수 있습니다.

## 클라이언트측 핵심 사항 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/tally/components/hbs/voting</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>포함 가능</strong></a></td>
   <td>예 - 속성은 <i>디자인 </i> 모드에서 편집할 수 있습니다.</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong>템플릿</strong></td>
   <td><p> /libs/social/tally/components/hbs/voting/voting.hbs<br /> /libs/social/tally/components/hbs/voting/activity-title.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/voting/clientlibs/votingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>속성</strong></td>
   <td><p><a href="voting.md">투표 사용</a>을 참조하세요.</p> </td>
  </tr>
 </tbody>
</table>

* [클라이언트측 사용자 지정](client-customize.md)

## 서버측 Essentials {#essentials-for-server-side}

* [Tally API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Tally 끝점](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [서버측 사용자 지정](server-customize.md)

### UGC(게재된 투표 액세스) {#accessing-posted-voting-ugc}

UGC는 중재에 대한 표준 방법 중 하나를 사용하여 중재되어야 합니다.
[사용자 생성 콘텐츠 중재](moderate-ugc.md)를 참조하십시오.

AEM 6.1 커뮤니티에서 UGC에 대한 [일반 저장소](working-with-srp.md)를 사용하면 선택한 저장소 옵션(예: ASRP, MSRP 또는 JSRP)에 관계없이 UGC에 프로그래밍 방식으로 액세스할 수 있습니다.

**저장소에서 UGC의 위치 및 형식은 경고 없이 변경될 수 있습니다**.

다음을 참조하십시오.

* [저장소 리소스 공급자 개요](srp.md) - 소개 및 저장소 사용 개요.
* [SRP 및 UGC Essentials](srp-and-ugc.md) - SRP 유틸리티 메서드 및 예제.
* [SRP를 사용하여 UGC에 액세스](accessing-ugc-with-srp.md) - 코딩 지침.
* [SocialUtils 리팩터링](socialutils.md) - 더 이상 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.
