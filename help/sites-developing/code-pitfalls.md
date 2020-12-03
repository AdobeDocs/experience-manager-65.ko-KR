---
title: 코드 함정
seo-title: 코드 함정
description: AEM 개발 시 피해야 할 일반적인 코딩 함선
seo-description: AEM 개발 시 피해야 할 일반적인 코딩 함선
uuid: e7413bdc-4889-45ff-bdcb-b0893d33a3b7
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 01362026-a696-4a5d-94e9-ea784eaa6e4b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 6%

---


# 코드 함정{#code-pitfalls}

## Java 코드 {#avoid-sling-bindings-in-java-code}에서 바인딩 방지

Sling Bindings는 90%의 경우에 서비스에 액세스하는 부적절한 방법입니다. 대신 *@Reference* 또는 *@Inserve* 주석을 사용해야 합니다.

## Java 코드 {#avoid-thread-interrupt-in-java-code}에서 Thread.interrupt를 피하십시오.

*Thread.* interrtis는 잘못된 시간에 호출될 때 Lucene 파일 및 영구 캐시 파일 등의 파일을 닫을 수 있으므로 위험합니다.

## Java 동기화를 ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}과 혼합하지 마십시오.

이 경우 코드가 결국 교착 상태가 될 수 있습니다.
