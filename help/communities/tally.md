---
title: Tally 기본 사항
description: Tally가 어떻게 특정 제품 및 서비스를 중요시하는지에 대한 구성원들의 피드백을 수집하는 표준 방법을 제공하는 추상 클래스인지에 대해 알아봅니다.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0b508df9-1a24-4728-a254-f913eeb9b391
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# Tally 기본 사항 {#tally-essentials}

Tally는 특정 제품과 서비스를 어떻게 중시하는지에 대한 구성원들의 피드백을 수집하는 표준 방법을 제공하는 추상 클래스이다. 익명 피드백은 지원되지 않습니다. 사이트 방문자가 참여하려면 등록하고 로그인해야 하며, 피드백을 변경하려면 로그인해야 합니다. 로그인 요구 사항은 중재를 용이하게 하고 여러 게시물을 방지하여 피드백의 가치를 향상시킵니다.

추상 tally 클래스를 확장하여 사용자 지정 tally 구성 요소를 만들 수 있습니다.

[좋아요](essentials-liking.md)는 긍정적인 의견을 표현하는 간단한 형식의 집계 구현입니다.

[투표](essentials-voting.md)는 긍정적 또는 부정적 의견을 표현하는 간단한 형식의 집계를 구현한 것입니다.

[등급](rating-basics.md)은(는) 긍정적인 의견부터 부정적인 의견까지 다양한 의견을 표현하는 데 별표를 사용하는 집계의 구현입니다.

AEM 6.1부터는 폴링 구성 요소를 더 이상 사용할 수 없습니다.

[리뷰](reviews-basics.md)은(는) [댓글](essentials-comments.md)과(와) [평점](rating-basics.md)의 하이브리드인 SCF 구성 요소입니다.

## 클라이언트측 핵심 사항 {#essentials-for-client-side}

* [클라이언트측 사용자 지정](client-customize.md)

## 서버측 Essentials {#essentials-for-server-side}

* [Tally API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Tally 끝점](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [서버측 사용자 지정](server-customize.md)

### 게시한 집계 액세스(UGC) {#accessing-posted-tallies-ugc}

UGC는 중재에 대한 표준 방법 중 하나를 사용하여 중재되어야 합니다.
[사용자 생성 콘텐츠 중재](moderate-ugc.md)를 참조하십시오.

AEM 6.1 커뮤니티에서 UGC에 대한 [일반 저장소](working-with-srp.md)를 사용하면 선택한 저장소 옵션(예: ASRP, MSRP 또는 JSRP)에 관계없이 UGC에 프로그래밍 방식으로 액세스할 수 있습니다.

**저장소에서 UGC의 위치 및 형식은 경고 없이 변경될 수 있습니다**.

다음을 참조하십시오.

* [저장소 리소스 공급자 개요](srp.md) - 소개 및 저장소 사용 개요.
* [SRP 및 UGC Essentials](srp-and-ugc.md) - SRP 유틸리티 메서드 및 예제.
* [SRP를 사용하여 UGC에 액세스](accessing-ugc-with-srp.md) - 코딩 지침.
* [SocialUtils 리팩터링](socialutils.md) - 더 이상 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.
