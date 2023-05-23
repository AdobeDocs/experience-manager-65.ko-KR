---
title: SRP를 사용하여 UGC에 액세스
seo-title: Accessing UGC with SRP
description: 사이트가 ASRP 또는 MSRP를 사용하도록 구성된 경우 실제 UGC는 AEM 노드 저장소(JCR)에 저장되지 않습니다
seo-description: When a site is configured to use ASRP or MSRP, the actual UGC is not be stored in AEM's node store (JCR)
uuid: 30549f93-e370-4b8b-a35a-69e05884227e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 72d4022c-43ba-49e0-b94c-f2beabaef64d
docset: aem65
exl-id: 1157366f-2cc5-46e4-8ec6-e66fe5d0a0f6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# SRP를 사용하여 UGC에 액세스 {#accessing-ugc-with-srp}

## SRP 정보 {#about-srp}

모든 AEM Communities 구성 요소 및 기능은 [소셜 구성 요소 프레임워크(SCF)](/help/communities/scf.md)모든 사용자 생성 콘텐츠(UGC)에 액세스하기 위해 SocialResourceProvider API를 호출합니다.

커뮤니티 사이트를 만들기 전에 [SRP(저장소 리소스 제공자)](/help/communities/working-with-srp.md) 은(는) 기본 구현과 일치하는 구현을 선택하도록 구성해야 합니다. [토폴로지](/help/communities/topologies.md). SRP 구현은 세 가지 스토리지 옵션을 기반으로 합니다.

1. [ASRP](/help/communities/asrp.md) - 주문형 Adobe 스토리지
1. [MSRP](/help/communities/msrp.md) - MongoDb
1. [JSRP](/help/communities/jsrp.md) - JCR

## UGC 저장소 정보 {#about-ugc-storage}

UGC 저장에 대해 알아야 할 중요한 것은 사이트가 ASRP 또는 MSRP를 사용하도록 구성된 경우 실제 UGC가 AEM에 저장되지 않는다는 것입니다 [노드 저장소](/help/sites-deploying/data-store-config.md) (JCR).

유용한 메타데이터를 제공하기 위해 UGC를 섀도우하는 노드가 JCR에 있을 수 있지만, 이러한 노드는 실제 UGC와 혼동되지 않는다.

다음을 참조하십시오 [저장소 리소스 제공자 개요.](/help/communities/srp.md)

## 우수 사례 {#best-practice}

사용자 지정 구성 요소를 개발할 때 개발자는 현재 선택한 토폴로지와 독립적으로 코드를 작성해야 하므로 향후 새 토폴로지로 이동할 수 있는 유연성을 유지합니다.

### JCR을 사용할 수 없다고 가정 {#assume-jcr-not-available}

JCR과 관련된 메서드는 피해야 합니다.

사용 방법:

* Sling API(Sling 리소스)

   * jcr 노드가 있다고 가정하지 마십시오

* OSGi 이벤트

   * jcr 이벤트가 있다고 가정하지 마십시오

* [소셜 리소스 유틸리티](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

피해야 할 방법:

* 노드 API
* JCR 이벤트
* 워크플로우 런처(JCR 이벤트 사용)

### 검색 컬렉션 사용 {#use-search-collections}

SRP마다 기본 쿼리 언어가 다를 수 있습니다. 의 메서드를 사용하는 것이 좋습니다. [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) 적절한 쿼리 언어를 실행하는 패키지입니다.

자세한 내용은 [Essentials 검색](/help/communities/search-implementation.md).

## 리소스 {#resources}

* [커뮤니티 콘텐츠 저장소](/help/communities/working-with-srp.md) - UGC 공통 저장소에 사용 가능한 SRP 선택 사항에 대해 설명합니다.
* [저장소 리소스 공급자 개요](/help/communities/srp.md) - 소개 및 저장소 사용 개요
* [SRP 및 UGC 필수 패키지](/help/communities/srp-and-ugc.md) - SRP 유틸리티 메서드 및 예제
* [Essentials 검색](/help/communities/search-implementation.md) - UGC 검색에 필수적인 정보
* [SocialUtils 리팩터링](/help/communities/socialutils.md) - 더 이상 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑
