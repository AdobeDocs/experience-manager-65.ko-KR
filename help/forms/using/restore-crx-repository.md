---
title: JEE 클러스터 서버에 적용할 수 있는 손상된 CRX 저장소를 복원할 수 없습니다.
description: 손상된 CRX 저장소를 복원하는 방법에 대한 단계를 알아봅니다.
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 1%

---

# 손상된 CRX 저장소를 복원할 수 없습니다. {#unable-to-restore-corrupt-crx-repository}

## 문제 {#issue}

관계형 데이터베이스를 사용하는 JEE의 AEM Forms의 경우, AEM Forms과 관계형 데이터베이스를 호스팅하는 컴퓨터의 시간은 항상 절대 동기화되어야 합니다. 이러한 시스템의 시간이 동기화되지 않으면 JEE 서버의 AEM Forms CRX 저장소에 액세스할 수 없게 됩니다. 손상된 것처럼 보이고 URL을 통해 액세스할 수 없게 될 수 있습니다. `AuthenticationsupportService missing` 오류가 기록됩니다.

## 사전 요구 사항 {#prerequisites}

아래 단계를 수행하기 전에 CRX 저장소를 백업하십시오.

## 솔루션 {#solution}

1. `https://[AEM Forms Server]:[port]/system/console/bundles`(으)로 이동합니다.

1. `oak-core` 번들을 찾아 실행 중인지 확인하십시오.

1. `oak-core` 번들이 실행되고 있지 않으면 다시 시작합니다. ![일시 중지 단추](/help/forms/using/assets/stop.png) 아이콘이 `oak-core` 번들 앞에 있으면 번들이 실행 중임을 나타냅니다.

1. 문제가 여전히 해결되지 않으면 백업에서 CRX-저장소를 복원하거나 백업을 사용할 수 없는 경우 CRX-저장소를 다시 빌드합니다.


## 적용 대상 {#applies-to}

이 솔루션은 JEE 클러스터의 AEM Forms에 적용됩니다.
