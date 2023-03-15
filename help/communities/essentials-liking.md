---
title: 좋아요 기본 사항
seo-title: Liking Essentials
description: 좋아요 구성 요소 개요
seo-description: Liking component overview
uuid: 89f16859-c901-4090-8e16-363b95c508de
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f176c42b-b16b-42c9-af22-4b6421de5a90
pagetitle: Liking Essentials
exl-id: ef314385-cd5c-411c-91df-83691a81c1bc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 1%

---

# 좋아요 기본 사항 {#liking-essentials}

좋아요 구성 요소, a [계산](tally.md) 하위 클래스는 구성원이 하트 아이콘을 선택하기만 하면 특정 콘텐츠에 대한 긍정적인 의견을 표현할 수 있는 유용한 도구입니다.

동일한 페이지에 연결 구성 요소의 여러 인스턴스를 배치할 수 있습니다. 각 인스턴스는 고유한 인스턴스로 구성해야 합니다 `tally name` 속성.

유사한 항목의 익명 게시는 지원되지 않습니다. 사이트 방문자가 좋아요 참여하려면 등록하고 로그인해야 합니다. 로그인한 방문자(구성원)는 언제든지 켜거나 끌 수 있습니다.

## 클라이언트측 핵심 사항 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/tally/components/hbs/liking</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>포함하기 쉬워</strong></a></td>
   <td>예 - 다음 위치에서 편집 가능한 속성 <i>디자인 </i>모드</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs를</strong></a></td>
   <td> cq.social.hbs.liking</td>
  </tr>
  <tr>
   <td> <strong>템플릿</strong></td>
   <td><p> /libs/social/tally/components/hbs/liking/liking.hbs<br /> /libs/social/tally/components/hbs/liking/activity-icon.hbs<br /> /libs/social/tally/components/hbs/liking/activity-title.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/liking/clientlibs/likingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>속성</strong></td>
   <td><p>다음을 참조하십시오 <a href="liking.md">연결 사용</a></p> </td>
  </tr>
 </tbody>
</table>

* [클라이언트측 사용자 지정](client-customize.md)

## 서버측 Essentials {#essentials-for-server-side}

* [Tally API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Tally 끝점](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [서버측 사용자 지정](server-customize.md)

### UGC(게재된 투표 액세스) {#accessing-posted-voting-ugc}

UGC는 중재에 대한 표준 방법 중 하나를 사용하여 중재되어야 합니다.
다음을 참조하십시오 [사용자 생성 컨텐츠 중재](moderate-ugc.md).

AEM 6.1 커뮤니티에서 [공동 저장소](working-with-srp.md) ugc의 경우 선택한 스토리지 옵션(예: ASRP, MSRP 또는 JSRP)에 관계없이 UGC에 프로그래밍 방식으로 액세스하는 기능이 포함됩니다.

**저장소에서 UGC의 위치 및 형식은 경고 없이 변경될 수 있습니다**.

다음을 참조하십시오.

* [저장소 리소스 공급자 개요](srp.md) - 소개 및 저장소 사용 개요.
* [SRP 및 UGC 필수 패키지](srp-and-ugc.md) - SRP 유틸리티 메서드 및 예제.
* [SRP를 사용하여 UGC에 액세스](accessing-ugc-with-srp.md) - 코딩 지침
* [SocialUtils 리팩터링](socialutils.md) - 더 이상 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.
