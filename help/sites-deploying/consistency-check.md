---
title: 일관성 및 순회 검사
seo-title: Consistency and Traversal Checks
description: 일관성 및 순회 검사를 수행하는 방법을 알아봅니다.
seo-description: Learn how to perform consistency and traversal checks.
uuid: 0304e378-7c60-4bf5-9052-d01149d2a6df
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: af9a3e9d-194a-42e5-be28-b238e0c1e55e
feature: Configuring
exl-id: 10dde29b-5dc7-4d4e-80ae-3d4fd0397f7e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# 일관성 및 순회 검사{#consistency-and-traversal-checks}

업그레이드 시 작업 영역 불일치로 인해 문제가 발생할 수 있습니다. 테스트 업그레이드를 실행하여 문제가 발생하는지 확인하거나 일관성 검사를 예방 조치로 실행할 수 있습니다.

작업 공간 불일치로 인해 실패한 테스트 업그레이드를 실행하면 crx-quickstart/logs/crx/error.log에 다음과 유사한 항목이 표시됩니다.

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## 일관성 검사 수행 {#perform-a-consistency-check}

일관성 검사를 수행하려면 JMX Mbean** com.adobe.granite(저장소)에 대한 관리 페이지로 **. AEM 기본 화면에서 다음 위치로 이동합니다.

**도구 > 웹 콘솔 > 메인(메뉴 모음) > JMX > com.adobe.granite(저장소)**

기본 설치에서는 다음 위치에 있습니다.  **[|표시|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

다음에서 **작업** 페이지의 섹션에는 다음 두 가지 메서드가 있습니다. **`traversalCheck`** 및 **`consistencyCheck`**. 검사를 실행하려면 작업을 클릭하고 원하는 매개 변수를 입력합니다.

![chlimage_1-117](assets/chlimage_1-117.png)
