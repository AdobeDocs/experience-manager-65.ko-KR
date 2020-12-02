---
title: 로그 작업
seo-title: 로그 작업
description: 로그를 사용하여 AEM 문제를 해결하는 방법을 알아봅니다.
seo-description: 로그를 사용하여 AEM 문제를 해결하는 방법을 알아봅니다.
uuid: af8b7f50-c8d4-4760-9f00-3feb0b79ee4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: da92d751-6f14-4512-9d77-7ecf098bd58e
docset: aem65
translation-type: tm+mt
source-git-commit: 8b53e79e3a88f58423e99477db930a4912a1ba09
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 3%

---


# 로그 작업{#working-with-logs}

이 섹션에는 문제를 해결하는 데 도움이 되는 로그에 대한 자세한 정보가 포함되어 있습니다.

CRX는 자세한 로그를 기록합니다. 압축을 풀고 빠른 시작을 시작하면 다음 위치에서 로그를 찾을 수 있습니다.

* crx-quickstart/launchpad/logs
* crx-quickstart/server/logs
* crx-quickstart/logs

## 디버그 로그 수준 {#activating-the-debug-log-level} 활성화

기본 로그 수준은 INFO입니다. 즉, DEBUG 메시지는 기록되지 않습니다.

디버그 로그 수준을 활성화하려면 CRX 탐색기를 사용하여

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

property to debug. 로그를 많은 로그를 생성하므로 로그를 필요 이상으로 길게 DEBUG 로그 수준으로 남겨두지 마십시오.

디버그 파일의 한 줄은 대개 DEBUG로 시작하고 로그 수준, 설치 프로그램 작업 및 로그 메시지를 제공합니다. 예:

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

로그 수준은 다음과 같습니다.

| 0 | 치명적인 오류 | 작업이 실패했으며 설치 관리자를 계속할 수 없습니다. |
|---|---|---|
| 1 | 오류 | 작업이 실패했습니다. 설치가 진행되지만 CRX의 일부가 올바르게 설치되지 않아 작동하지 않습니다. |
| 2 | 경고 | 작업에 성공했지만 문제가 발생했습니다. CRX가 제대로 작동하지 않거나 작동하지 않을 수 있습니다. |
| 3 | 정보 | 그 행동은 성공했다. |

## 문제 해결에 사용되는 자세한 옵션 {#verbose-option-used-for-troubleshooting}

CRX를 시작할 때 다음과 같이 명령줄에 -v(세부 정보) 옵션을 추가할 수 있습니다.

` java -jar crx-<*version*>-<*edition*>.jar -v`

콘솔에 빠른 시작 로그 출력 중 일부를 표시하는 이 옵션을 사용하여 문제 해결을 위한 세부 정보 옵션을 사용하십시오.