---
title: 일관성 및 순회 검사
description: 일관성 및 순회 검사를 수행하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
feature: Configuring
exl-id: 10dde29b-5dc7-4d4e-80ae-3d4fd0397f7e
solution: Experience Manager, Experience Manager Sites
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 523b1ccd-901e-5e3b-9fa7-f3dfd82463d5
    internal-label: Configuring
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 6%
---
# 일관성 및 순회 검사{#consistency-and-traversal-checks}

업그레이드 시 작업 영역 불일치로 인한 문제가 발생할 수 있습니다. 테스트 업그레이드를 실행하여 문제가 있는지 확인하거나 예방 조치로 일관성 검사를 실행할 수 있습니다.

작업 공간 불일치로 인해 실패하는 테스트 업그레이드를 실행하면 crx-quickstart/logs/crx/error.log에 다음과 유사한 항목이 표시됩니다.

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## 일관성 검사 수행 {#perform-a-consistency-check}

일관성 검사를 수행하려면 JMX Mbean **com.adobe.granite(저장소)**&#x200B;에 대한 관리 페이지로 이동합니다. AEM 기본 화면에서 다음 위치로 이동합니다.

**도구 > 웹 콘솔 > 메인(메뉴 모음) > JMX > com.adobe.granite(저장소)**

기본 설치에서 찾을 수 있는 위치: **[|표시|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

페이지의 **작업** 섹션에서 **`traversalCheck`** 및 **`consistencyCheck`** 메서드를 찾습니다. 검사를 실행하려면 작업을 클릭하고 원하는 매개 변수를 입력합니다.

![chlimage_1-117](assets/chlimage_1-117.png)
