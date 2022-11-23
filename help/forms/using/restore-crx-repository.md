---
title: JEE 클러스터 서버에 적용할 수 있는 손상된 CRX 저장소를 복원할 수 없습니다.
description: 손상된 CRX 저장소를 복원하는 절차
source-git-commit: a7d125503b0bd3c52cb3a959e2f0dde1a69cbe2b
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 1%

---

# 손상된 CRX 저장소를 복원할 수 없습니다. {#unable-to-restore-corrupt-crx-repository}

## 문제 {#issue}

RDB 지속성을 사용하여 JEE에 배포된 AEM Forms의 경우 AEM Forms 호스트 시스템과 데이터베이스 시스템이 절대 시간 동기화에 있어야 합니다. 하지만, 어떤 이유로 시계가 동기화에서 벗어나면 CRX 저장소가 손상되고 URL이 액세스할 수 없게 됩니다. 오류: `AuthenticationsupportService missing` 로그 파일에서 발생합니다.

## 솔루션 {#solution}

문제를 해결하려면 다음 단계를 수행하십시오.
1. 이동  [https://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).

1. 을(를) 찾습니다 `oak-core` 번들로 구성되어 있는지 확인하고 실행 중인지 확인하십시오.

1. 를 다시 시작합니다. `oak-core` 실행 중이 아니면 번들입니다. 일시 중지 단추가 `oak-core` 번들로 묶은 다음 번들이 실행 중임을 나타냅니다.

1. 문제가 해결되지 않으면 백업에서 CRX 저장소에서 복원하거나 백업을 사용할 수 없는 경우 CRX 저장소를 다시 빌드하십시오.

   >[!NOTE]
   >
   >위의 단계를 수행하기 전에 CRX 리포지토리의 백업을 수행합니다.

## 적용 대상 {#applies-to}

이 솔루션은 다음과 같은 경우에 적용됩니다.

* JEE 클러스터 서버의 AEM Forms


