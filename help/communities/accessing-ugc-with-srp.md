---
title: SRP를 사용하여 UGC 액세스
seo-title: SRP를 사용하여 UGC 액세스
description: 사이트가 ASRP 또는 MSRP를 사용하도록 구성된 경우, 실제 UGC는 AEM 노드 스토어(JCR)에 저장되지 않습니다.
seo-description: 사이트가 ASRP 또는 MSRP를 사용하도록 구성된 경우, 실제 UGC는 AEM 노드 스토어(JCR)에 저장되지 않습니다.
uuid: 30549f93-e370-4b8b-a35a-69e05884227e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 72d4022c-43ba-49e0-b94c-f2beabaef64d
docset: aem65
translation-type: tm+mt
source-git-commit: 974d58efa560b90234d5121a11bdb445c7bf94cf
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---


# SRP {#accessing-ugc-with-srp}을(를) 사용하여 UGC 액세스

## SRP {#about-srp} 정보

모든 AEM Communities 구성 요소 및 기능은 SocialResourceProvider API를 호출하여 UGC(사용자 생성 콘텐츠)에 액세스하는 [소셜 구성 요소 프레임워크(SCF)](/help/communities/scf.md)에 구축됩니다.

커뮤니티 사이트를 만들기 전에 기존 [토폴로지](/help/communities/topologies.md)와 일치하는 구현을 선택하도록 [SRP)](/help/communities/working-with-srp.md)을(를) 구성해야 합니다. SRP 구현은 다음 3가지 스토리지 옵션을 기반으로 합니다.

1. [ASRP](/help/communities/asrp.md)  - Adobe on-demand 스토리지
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## UGC 스토리지 정보 {#about-ugc-storage}

UGC 저장에 대해 알아야 할 중요한 것은 사이트가 ASRP 또는 MSRP를 사용하도록 구성된 경우 실제 UGC는 AEM [노드 저장소](/help/sites-deploying/data-store-config.md)(JCR)에 저장되지 않습니다.

JCR에 유용한 메타데이터를 제공하기 위해 UGC를 그림자로 표시하는 노드가 있을 수 있지만 이러한 노드는 실제 UGC와 혼동하지 않도록 합니다.

[저장소 리소스 공급자 개요를 참조하십시오.](/help/communities/srp.md)

## 우수 사례 {#best-practice}

사용자 지정 구성 요소를 개발할 때 개발자는 현재 선택된 토폴로지와 독립적으로 코드를 작성하도록 주의하여 향후 새 토폴로지로 이동할 수 있는 유연성을 유지해야 합니다.

### JCR을 사용할 수 없다고 가정함 {#assume-jcr-not-available}

JCR에만 해당하는 메서드를 사용하지 않아야 합니다.

사용할 메서드:

* Sling API(Sling Resource)

   * JCR 노드가 있다고 가정하지 않음

* OSGi 이벤트

   * JCR 이벤트가 있다고 간주하지 않습니다.

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtiilities](/help/communities/socialutils.md#scfutilities-package)

피해야 할 메서드:

* 노드 API
* JCR 이벤트
* 워크플로우 래터(JCR 이벤트 사용)

### 검색 컬렉션 사용 {#use-search-collections}

서로 다른 SRP에는 서로 다른 기본 쿼리 언어가 있을 수 있습니다. 적절한 쿼리 언어를 실행하려면 [com.adobe.cq.sosocial.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) 패키지의 메서드를 사용하는 것이 좋습니다.

자세한 내용은 [Search Essentials](/help/communities/search-implementation.md)을 참조하십시오.

## 리소스 {#resources}

* [커뮤니티 컨텐츠 저장소](/help/communities/working-with-srp.md)  - UGC 공용 스토어에 사용할 수 있는 SRP에 대해 설명합니다.
* [스토리지 자원 공급자 개요](/help/communities/srp.md)  - 소개 및 저장소 사용 개요
* [SRP 및 UGC Essentials](/help/communities/srp-and-ugc.md) - SRP 유틸리티 방법 및 예제
* [Search Essentials](/help/communities/search-implementation.md)  - UGC 검색을 위한 필수 정보
* [SocialUtils 리팩토링](/help/communities/socialutils.md)  - 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑

