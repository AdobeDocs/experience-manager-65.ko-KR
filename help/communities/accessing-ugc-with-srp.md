---
title: SRP를 사용하여 UGC 액세스
seo-title: SRP를 사용하여 UGC 액세스
description: 사이트가 ASRP 또는 MSRP를 사용하도록 구성된 경우 실제 UGC는 AEM 노드 저장소(JCR)에 저장되지 않습니다
seo-description: 사이트가 ASRP 또는 MSRP를 사용하도록 구성된 경우 실제 UGC는 AEM 노드 저장소(JCR)에 저장되지 않습니다
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
source-wordcount: '366'
ht-degree: 0%

---

# SRP {#accessing-ugc-with-srp}으로 UGC에 액세스

## SRP {#about-srp} 정보

모든 AEM Communities 구성 요소 및 기능은 [SCF(소셜 구성 요소 프레임워크)](/help/communities/scf.md)에 구축됩니다. 이 프레임워크는 SocialResourceProvider API를 호출하여 모든 사용자 생성 콘텐츠(UGC)에 액세스합니다.

커뮤니티 사이트를 만들려면 [SRP(저장소 리소스 공급자)](/help/communities/working-with-srp.md)을(를) 구성하여 기본 [토폴로지](/help/communities/topologies.md)와 일치하는 구현을 선택해야 합니다. SRP 구현은 세 가지 스토리지 옵션을 기반으로 합니다.

1. [ASRP](/help/communities/asrp.md)  - 온디맨드 스토리지 Adobe
1. [MSRP](/help/communities/msrp.md)  - MongoDB
1. [JSRP](/help/communities/jsrp.md)  - JCR

## UGC 스토리지 정보 {#about-ugc-storage}

UGC 저장에 대해 알고 있어야 하는 중요한 것은 사이트가 ASRP 또는 MSRP를 사용하도록 구성된 경우 실제 UGC는 AEM [node store](/help/sites-deploying/data-store-config.md) (JCR)에 저장되지 않습니다.

JCR에 유용한 메타데이터를 제공하기 위해 UGC를 그림자로 표시하는 노드가 있을 수 있지만 이러한 노드는 실제 UGC와 혼동하지 않을 수 있습니다.

[저장소 리소스 공급자 개요를 참조하십시오.](/help/communities/srp.md)

## 우수 사례 {#best-practice}

사용자 지정 구성 요소를 개발할 때는 개발자는 현재 선택한 토폴로지와 독립적으로 코드를 작성하도록 주의하여 향후 새로운 토폴로지로 이동할 수 있는 유연성을 유지해야 합니다.

### JCR을 사용할 수 없다고 가정합니다 {#assume-jcr-not-available}

JCR에 관련된 메서드는 사용하지 않아야 합니다.

사용 방법 :

* Sling API(Sling Resource)

   * JCR 노드가 있다고 가정하지 마십시오

* OSGi 이벤트

   * jcr 이벤트가 있다고 가정하지 마십시오

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtiilities](/help/communities/socialutils.md#scfutilities-package)

피해야 할 방법 :

* 노드 API
* JCR 이벤트
* 워크플로우 런처(JCR 이벤트를 사용하는)

### 검색 컬렉션 사용 {#use-search-collections}

SRP마다 다른 기본 쿼리 언어를 사용할 수 있습니다. [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) 패키지의 메서드를 사용하여 적절한 쿼리 언어를 실행하는 것이 좋습니다.

자세한 내용은 [Search Essentials](/help/communities/search-implementation.md)를 참조하십시오.

## 리소스 {#resources}

* [커뮤니티 컨텐츠 저장소](/help/communities/working-with-srp.md)  - UGC 공용 저장소에 사용할 수 있는 SRP 선택에 대해 설명합니다.
* [저장소 리소스 공급자 개요](/help/communities/srp.md)  - 소개 및 저장소 사용 개요
* [SRP 및 UGC Essentials](/help/communities/srp-and-ugc.md)  - SRP 유틸리티 메서드 및 예제
* [Search Essentials](/help/communities/search-implementation.md)  - UGC 검색을 위한 필수 정보
* [SocialUtils 리팩터링](/help/communities/socialutils.md)  - 사용 중단된 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.
