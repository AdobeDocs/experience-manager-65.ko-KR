---
title: Tally Essentials
seo-title: Tally Essentials
description: 집계 클래스 개요
seo-description: Tally class overview
uuid: c369c6a1-9ced-4b5c-af43-8c03236eaa52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9941ba90-3d40-4c90-bca8-5db49603cbfa
exl-id: 0b508df9-1a24-4728-a254-f913eeb9b391
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Tally Essentials {#tally-essentials}

Tallic 클래스는 멤버로부터 특정 제품 및 서비스의 가치를 부여하는 방법에 대한 피드백을 수집하는 표준 방법을 제공하는 추상 클래스입니다. 익명 피드백은 지원되지 않습니다. 사이트 방문자가 등록을 하고 로그인하여 자신의 피드백을 변경해야 합니다. 로그인 요구 사항은 여러 게시물을 방지하여 조정을 용이하게 하고 피드백의 가치를 향상시킵니다.

추상 집계 클래스를 확장하여 사용자 지정 집계 구성 요소를 만들 수 있습니다.

[좋아요](essentials-liking.md) 그것은 긍정적인 의견을 표현하는 간단한 형태의 총계 구현이다.

[투표](essentials-voting.md) 그것은 긍정적이거나 부정적인 의견을 표현하는 간단한 형태의 총계 구현이다.

[등급](rating-basics.md) 긍정에서 부정까지 다양한 의견을 표현하는 스타제도를 활용하는 총계 구현이다.

AEM 6.1부터는 투표 구성 요소를 더 이상 사용할 수 없습니다.

[검토](reviews-basics.md) 는 의 하이브리드 SCF 구성 요소입니다 [댓글](essentials-comments.md) 및 [등급](rating-basics.md).

## 클라이언트측 핵심 사항 {#essentials-for-client-side}

* [클라이언트측 사용자 지정](client-customize.md)

## 서버측 핵심 사항 {#essentials-for-server-side}

* [총계 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [집계 끝점](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [서버측 사용자 지정](server-customize.md)

### 게시된 테이블 액세스(UGC) {#accessing-posted-tallies-ugc}

조정을 위한 표준 방법 중 하나를 사용하여 UGC가 중재되어야 합니다.
자세한 내용은 [사용자가 생성한 컨텐츠 중재](moderate-ugc.md).

AEM 6.1 Communities에서 [일반 상점](working-with-srp.md) UGC의 경우 선택한 저장소 옵션(예: ASRP, MSRP 또는 JSRP)에 관계없이 UGC에 프로그래밍 방식으로 액세스할 수 있습니다.

**저장소에서 UGC의 위치와 형식은 경고 없이 변경될 수 있습니다**.

다음을 참조하십시오.

* [저장소 리소스 공급자 개요](srp.md) - 소개 및 저장소 사용 개요.
* [SRP 및 UGC 핵심 사항](srp-and-ugc.md) - SRP 유틸리티 메서드 및 예입니다.
* [SRP를 사용하여 UGC 액세스](accessing-ugc-with-srp.md) - 코딩 지침
* [SocialUtils 리팩터링](socialutils.md) - 사용 중단된 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.
