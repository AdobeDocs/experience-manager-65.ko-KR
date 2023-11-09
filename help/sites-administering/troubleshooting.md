---
title: 로그 작업
seo-title: Working with Logs
description: 로그 작업을 통해 AEM 문제를 해결하는 방법을 알아봅니다.
seo-description: Learn how to troubleshoot AEM by working with logs.
uuid: af8b7f50-c8d4-4760-9f00-3feb0b79ee4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: da92d751-6f14-4512-9d77-7ecf098bd58e
docset: aem65
exl-id: ab4fc41f-e0e9-4577-aab2-f0b4298f9a59
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 3%

---

# 로그 작업{#working-with-logs}

이 섹션에는 문제를 해결하는 데 도움이 되는 로그에 대한 자세한 정보가 포함되어 있습니다.

>[!NOTE]
>
>로그에 대한 자세한 내용은 다음을 참조하십시오.
>
>* [AEM의 감사 로그 유지 관리](/help/sites-administering/operations-audit-log.md)
>* [감사 레코드 및 로그 파일 작업](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)

CRX는 자세한 로그를 기록합니다. 압축을 풀고 빠른 시작을 시작하면 다음 위치에 로그가 있습니다.

* crx-quickstart/launchpad/logs
* crx-quickstart/server/logs
* crx-quickstart/logs

## DEBUG 로그 수준 활성화 {#activating-the-debug-log-level}

기본 로그 수준은 INFO입니다. 즉, DEBUG 메시지는 기록되지 않습니다.

디버그 로그 수준을 활성화하려면 CRX 탐색기를 사용하여

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

디버그할 속성입니다. DEBUG 로그 수준에서 로그를 필요 이상으로 오래 두지 마십시오. 로그 생성이 많기 때문입니다.

디버그 파일의 행은 일반적으로 DEBUG로 시작한 다음 로그 수준, 설치 관리자 작업 및 로그 메시지를 제공합니다. 예:

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

로그 수준은 다음과 같습니다.

| 0 | 치명적인 오류 | 작업이 실패하여 설치 관리자를 진행할 수 없습니다. |
|---|---|---|
| 1 | 오류 | 작업이 실패했습니다. 설치가 진행되지만 CRX의 일부가 올바르게 설치되지 않아 작동하지 않습니다. |
| 2 | 경고 | 작업이 성공했지만 문제가 발생했습니다. CRX가 제대로 작동할 수도 있고 작동하지 않을 수도 있습니다. |
| 3 | 정보 | 작업이 성공했습니다. |

## 문제 해결에 사용되는 상세 정보 옵션 {#verbose-option-used-for-troubleshooting}

CRX를 시작할 때 -v(verbose) 옵션을 다음과 같이 명령줄에 추가할 수 있습니다.

` java -jar crx-<*version*>-<*edition*>.jar -v`

이 옵션은 콘솔에 빠른 시작 로그 출력의 일부를 표시하므로 문제 해결을 위해 verbose 옵션을 사용합니다.
