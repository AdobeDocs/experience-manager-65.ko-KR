---
title: 코드 함정
description: AEM용으로 개발할 때 피해야 할 일반적인 코딩 위험
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: c448c5d5-def8-4c1a-8db4-41eb49d0cd20
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 4%
---
# 코드 함정{#code-pitfalls}

## Java 코드에서 Sling 바인딩 방지 {#avoid-sling-bindings-in-java-code}

슬링 바인딩은 90%의 경우 서비스에 액세스할 수 있는 부적절한 방법입니다. 대신 *@Reference* 또는 *@Inject* 주석을 사용해야 합니다.

## Java 코드에서 Thread.interrupt 방지 {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt*&#x200B;은(는) 잘못된 시간에 호출될 때 Lucene 파일 및 영구 캐시 파일을 포함한 파일을 닫을 수 있으므로 위험합니다.

## Java 동기화와 ReadWriteLocks 혼용 방지 {#avoid-mixing-java-synchronization-with-readwritelocks}

이로 인해 코드가 결국 교착 상태에 빠질 수 있는 경합 조건이 발생할 수 있습니다.
