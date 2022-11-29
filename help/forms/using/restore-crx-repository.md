---
title: JEE 클러스터 서버에 적용할 수 있는 손상된 CRX 저장소를 복원할 수 없습니다.
description: 손상된 CRX 저장소를 복원하는 절차
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
source-git-commit: c4f776b08cb8cc8c6eea78a3757735e063bec20c
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 2%

---

# 손상된 CRX 저장소를 복원할 수 없습니다. {#unable-to-restore-corrupt-crx-repository}

## 문제 {#issue}

관계형 데이터베이스를 사용하는 JEE의 AEM Forms의 경우 AEM Forms 및 관계형 데이터베이스를 호스팅하는 시스템의 시간은 항상 절대 동기화되어야 합니다. 이러한 시스템의 시간이 동기화되지 않으면 JEE 서버에 있는 AEM Forms의 CRX 저장소에 액세스할 수 없게 될 수 있습니다. 손상된 것으로 나타나며 URL을 통해 액세스할 수 없게 될 수 있습니다. 다음 `AuthenticationsupportService missing` 오류가 기록됩니다.

## 사전 요구 사항 {#prerequisites}

아래에 언급된 단계를 수행하기 전에 CRX 저장소의 백업을 수행합니다.

## 솔루션 {#solution}

문제를 해결하려면 다음 단계를 수행하십시오.
1. 이동  `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. 을(를) 찾습니다 `oak-core` 번들로 구성되어 있는지 확인하고 실행 중인지 확인하십시오.

1. 를 다시 시작합니다. `oak-core` 실행 중이 아니면 번들입니다. If  ![일시 중지 단추](/help/forms/using/assets/stop.png) 아이콘이 앞에 있습니다. `oak-core` 번들로 묶은 다음 번들이 실행 중임을 나타냅니다.

1. 문제가 아직 해결되지 않으면 백업에서 CRX 저장소에서 복원하거나 백업을 사용할 수 없는 경우 CRX 저장소를 다시 빌드하십시오.


## 적용 대상 {#applies-to}

이 솔루션은 다음과 같은 경우에 적용됩니다.

* JEE 클러스터의 AEM Forms