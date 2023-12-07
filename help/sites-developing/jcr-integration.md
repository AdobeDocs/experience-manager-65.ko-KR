---
title: JCR 통합
description: JCR 수준에서 Adobe Experience Manager과 통합해야 하는 시기에 대한 몇 가지 팁을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 170474c1-c7f4-446c-bda4-84768d44a078
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# JCR 통합{#jcr-integration}

## JCR API보다 Sling 리소스 API 선호 {#prefer-the-sling-resource-api-to-jcr-api}

Sling API는 JCR API보다 더 높은 추상적인 수준에서 작동합니다. 이를 통해 코드를 보다 재사용할 수 있고 기본 스토리지와는 독립적으로 사용할 수 있습니다. 따라서 필요한 경우 ResourceProvider 메커니즘을 통해 외부 가상 데이터를 더 쉽게 포함할 수 있습니다.

## 가능하면 쿼리 방지 {#avoid-queries-wherever-possible}

쿼리를 실행하는 것보다 저장소를 탐색하여 데이터를 검색하는 것이 항상 더 빠릅니다. 최종 사용자 쿼리나 전체 저장소에서 구조화된 컨텐츠를 찾아야 하는 등의 쿼리가 필요한 경우가 있지만 그 외의 모든 경우에는 필요한 노드로 이동하는 것이 좋습니다. 쿼리는 항상 탐색 구성 요소, &quot;최근 항목 목록&quot;, 항목 수 등과 같은 렌더링 논리에서 피해야 합니다. 이러한 경우 렌더링할 때 직접 사용할 수 있도록 계층 구조를 거침하거나 결과를 사전 캐시하는 것이 좋습니다.

## JCR 관찰 범위 제한 {#restrict-the-scope-of-jcr-observation}

저장소에서 이벤트를 수신할 때는 가능한 한 범위를 좁히는 것이 중요합니다. 예를 들어에서 이벤트를 수신하는 것이 훨씬 좋습니다. `/etc/mycompany` 듣는 것보다 `/etc`. 저장소 루트에서 이벤트를 수신하지 않습니다. 또한 콜백 메서드가 수행할 작업이 없을 때 가능한 한 빨리 실행되도록 합니다.

## JCR 관리자 액세스 사용 제거 {#eliminate-use-of-jcr-admin-access}

AEM 6부터는 ResourceResolverFactory에서 관리 세션을 가져오므로 로그인 관리는 더 이상 사용되지 않습니다. 대신, 이 유형의 액세스가 필요한 백 오피스 작업에 대해 서비스 계정을 만들어야 하며 ResourceResolverFactory를 사용하여 이 계정에 대한 ResourceResolver를 가져올 수 있습니다.
