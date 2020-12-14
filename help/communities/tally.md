---
title: Tally Essentials
seo-title: Tally Essentials
description: 총계 클래스 개요
seo-description: 총계 클래스 개요
uuid: c369c6a1-9ced-4b5c-af43-8c03236eaa52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9941ba90-3d40-4c90-bca8-5db49603cbfa
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---


# Tally Essentials {#tally-essentials}

총계는 특정 제품 및 서비스의 가치를 평가하는 방법에 대한 멤버로부터 피드백을 수집하는 표준 방법을 제공하는 추상 클래스입니다. 익명의 피드백은 지원되지 않습니다. 사이트 방문자가 등록 및 로그인하여 피드백을 변경할 수 있습니다. 로그인 요구 사항은 여러 게시물을 방지하여 조정을 용이하게 하고 피드백 가치를 높입니다.

추상 집계 클래스를 확장하여 사용자 지정 집계 구성 요소를 만들 수 있습니다.

[](essentials-liking.md) 리칭은 긍정적인 의견을 표현하는 간단한 형태의 총계 수행이다.

[투표](essentials-voting.md) 는 긍정적이거나 부정적인 의견을 표현하는 간단한 형태의 총계 집행이다.

[등급](rating-basics.md) 은 긍정에서 부정으로 다양한 의견을 표현하는 스타제를 사용하는 총계 시행이다.

AEM 6.1부터는 투표 구성 요소를 더 이상 사용할 수 없습니다.

[](reviews-basics.md) 검토는  [](essentials-comments.md) 주석 및  [등급](rating-basics.md) 혼합의 SCF 구성 요소입니다.

## Essentials for Client-Side {#essentials-for-client-side}

* [클라이언트측 사용자 지정](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [총계 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [총점](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [서버측 사용자 정의](server-customize.md)

### 게시된 테이블 액세스(UGC) {#accessing-posted-tallies-ugc}

조정을 위한 표준 방법 중 하나를 사용하여 UGC를 중재해야 합니다.
[사용자 생성 콘텐츠 중재](moderate-ugc.md)를 참조하십시오.

AEM 6.1 Communities의 경우, UGC용 [공통 스토어](working-with-srp.md)를 사용하면 선택한 스토리지 옵션(예: ASRP, MSRP 또는 JSRP)에 상관없이 프로그램 방식으로 UGC에 액세스할 수 있습니다.

**저장소에서 UGC의 위치와 형식은 경고** 없이 변경될 수 있습니다.

다음을 참조하십시오.

* [스토리지 자원 공급자 개요](srp.md)  - 소개 및 저장소 사용 개요.
* [SRP 및 UGC Essentials](srp-and-ugc.md) - SRP 유틸리티 방법 및 예.
* [SRP](accessing-ugc-with-srp.md) - 코딩 가이드라인을 사용하여 UGC 액세스
* [SocialUtils 리팩토링](socialutils.md)  - 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.

