---
title: JCR 통합
seo-title: JCR 통합
description: JCR 수준에서 통합해야 하는 경우에 대한 팁
seo-description: JCR 수준에서 통합해야 하는 경우에 대한 팁
uuid: 11518baf-521e-471d-ad4f-2baa76075cfa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: e6647a11-a36e-4808-bb61-29b2895c6b1d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# JCR 통합{#jcr-integration}

## JCR API보다 Sling 리소스 API 선호 {#prefer-the-sling-resource-api-to-jcr-api}

Sling API 파섹 따라서 기본 스토리지와 상관없이 코드를 더 재사용 및 독립적으로 사용할 수 있습니다. 따라서 필요한 경우 ResourceProvider 메커니즘을 통해 외부 가상 데이터를 보다 쉽게 포함할 수 있습니다.

## 가능한 한 쿼리를 피하십시오 {#avoid-queries-wherever-possible}

쿼리를 실행하는 것보다 항상 저장소를 탐색하여 데이터를 검색하는 것이 더 빠릅니다. 최종 사용자 쿼리나 전체 저장소에서 구조화된 컨텐츠를 찾아야 하는 등 쿼리가 필요한 경우가 있지만 다른 모든 경우에는 필요한 노드로 이동하는 것이 좋습니다. 탐색 구성 요소, &quot;최근 항목 목록&quot;, 항목 수 등과 같은 렌더링 논리에서 쿼리는 항상 피해야 합니다. 이러한 경우 렌더링할 때 직접 사용할 수 있도록 계층 구조를 살펴보거나 결과를 미리 캐시하는 것이 좋습니다.

## JCR 관찰 범위 제한 {#restrict-the-scope-of-jcr-observation}

저장소에서 이벤트를 수신할 때는 범위를 최대한 좁히는 것이 중요합니다. 예를 들어, 이벤트를 청하는 것이 `/etc/mycompany` 듣는 것보다 훨씬 낫다 `/etc`. 저장소 루트에서 이벤트를 수신하지 마십시오. 또한 콜백 메서드가 수행할 작업이 없을 때 가능한 한 빨리 실행되어야 합니다.

## JCR 관리자 액세스 제거 {#eliminate-use-of-jcr-admin-access}

AEM 6부터 로그인 관리는 ResourceResolverFactory에서 관리 세션을 가져오는 것처럼 더 이상 사용되지 않습니다. 대신 이 유형의 액세스가 필요한 백 오피스 작업에 대한 서비스 계정을 만들어야 하며 ResourceResolverFactory를 사용하여 이 계정에 대한 ResourceResolver를 가져올 수 있습니다.
