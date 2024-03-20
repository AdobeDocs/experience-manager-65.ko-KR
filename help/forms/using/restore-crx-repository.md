---
title: JEE 클러스터 서버에 적용할 수 있는 손상된 CRX 저장소를 복원할 수 없습니다.
description: 손상된 CRX 저장소를 복원하는 방법에 대한 단계를 알아봅니다.
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 1%

---

# 손상된 CRX 저장소를 복원할 수 없습니다. {#unable-to-restore-corrupt-crx-repository}

## 문제 {#issue}

관계형 데이터베이스를 사용하는 JEE의 AEM Forms의 경우, AEM Forms과 관계형 데이터베이스를 호스팅하는 컴퓨터의 시간은 항상 절대 동기화되어야 합니다. 이러한 시스템의 시간이 동기화되지 않으면 JEE 서버의 AEM Forms CRX 저장소에 액세스할 수 없게 됩니다. 손상된 것처럼 보이고 URL을 통해 액세스할 수 없게 될 수 있습니다. 다음 `AuthenticationsupportService missing` 오류가 기록됩니다.

## 사전 요구 사항 {#prerequisites}

아래 단계를 수행하기 전에 CRX 저장소를 백업하십시오.

## 솔루션 {#solution}

1. 다음으로 이동  `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. 를 찾습니다. `oak-core` 번들로 묶어 실행 중인지 확인합니다.

1. 다시 시작 `oak-core` 실행되지 않는 경우 번들입니다. If  ![일시 중지 단추](/help/forms/using/assets/stop.png) 아이콘은 `oak-core` 번들로 설정하면 번들이 실행 중 상태임을 나타냅니다.

1. 문제가 여전히 해결되지 않으면 백업에서 CRX-repository를 복원하거나 백업을 사용할 수 없는 경우 CRX-repository를 다시 빌드합니다.


## 적용 대상 {#applies-to}

이 솔루션은 JEE 클러스터의 AEM Forms에 적용됩니다.
