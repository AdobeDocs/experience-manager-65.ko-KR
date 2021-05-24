---
title: AEM 인스턴스 모니터링 및 유지 관리
seo-title: AEM 인스턴스 모니터링 및 유지 관리
description: AEM 모니터링 방법을 알아봅니다.
seo-description: AEM 모니터링 방법을 알아봅니다.
uuid: 14466552-5c92-4730-a427-85675a2b121c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5d2364b7-4497-4f8b-85ef-6e780bfb8c36
docset: aem65
feature: 구성
exl-id: d3375935-090d-4052-8234-68ef4ddbab6a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '5892'
ht-degree: 1%

---

# AEM 인스턴스 모니터링 및 유지 관리{#monitoring-and-maintaining-your-aem-instance}

AEM 인스턴스가 배포되면 작업, 성능 및 무결성을 모니터링하고 유지 관리하는 데 특정 작업이 필요합니다.

여기서 중요한 요소는 잠재적인 문제를 인식하기 위해 시스템이 정상적인 조건에서 어떻게 표시되고 동작하는지 알아야 합니다. 이 작업은 시스템을 모니터링하고 일정 기간 정보를 수집하여 수행하는 것이 가장 좋습니다.

| 확인 | 고려 사항 | 댓글/작업 |
|---|---|---|
| 백업 계획 |  | [인스턴스 백업 방법](/help/sites-deploying/monitoring-and-maintaining.md#backups) 을 참조하십시오. |
| 재해 복구 계획 | 귀사의 재해 복구 지침 |  |
| 오류 추적 시스템은 보고 문제에 대해 사용할 수 있습니다. | 예를 들어 [bugzilla](https://www.bugzilla.org/), [jira](https://www.atlassian.com/software/jira/) 또는 기타 여러 항목 중 하나가 있습니다. |  |
| 파일 시스템을 모니터링하고 있습니다. | 사용 가능한 디스크 공간이 부족한 경우 CRX 리포지토리가 &quot;동결&quot;됩니다. 공간이 있으면 다시 시작됩니다. | &quot; 사용 가능한 공간이 부족하면 로그 파일에서 `*ERROR* LowDiskSpaceBlocker`&quot; 메시지를 볼 수 있습니다. |
| [로그 ](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) 파일을 모니터링하는 중입니다. |  |  |
| 시스템 모니터링이 백그라운드에서 계속 실행되고 있습니다. | CPU, 메모리, 디스크 및 네트워크 사용을 포함합니다. 예를 들어 iostat / vmstat / perfmon을 사용합니다. | 로그된 데이터는 시각화되며 성능 문제를 추적하는 데 사용할 수 있습니다. 원시 데이터도 액세스할 수 있습니다. |
| [AEM 성능을 모니터링하고 있습니다](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance). | [요청 카운터](/help/sites-deploying/monitoring-and-maintaining.md#request-counters)를 포함하여 트래픽 수준을 모니터링합니다. | 상당한 장기 손실과 장기 실적을 확인하고자 할 경우에는 상세한 조사를 하여야 한다. |
| [복제 에이전트](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-your-replication-agents)를 모니터링하고 있습니다. |  |  |
| 워크플로우 인스턴스를 정기적으로 삭제합니다. | 저장소 크기 및 워크플로우 성능. | [워크플로우 인스턴스 정규 삭제](/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances)를 참조하십시오. |

## 백업 {#backups}

다음을 백업하는 것이 좋습니다.

* 소프트웨어 설치 - 구성의 중요한 변경 전/후
* 리포지토리 내에 있는 컨텐츠 - 정기적으로

백업 정책을 따라야 할 것이며 백업 대상 및 백업 시기에 대한 추가 고려 사항이 있을 것입니다.

* 시스템 및 데이터의 중요성
* 소프트웨어 또는 데이터를 변경하는 빈도를 지정합니다.
* 데이터 볼륨때로 백업 수행 시간이 문제가 될 수 있습니다.
* 사용자가 온라인 상태일 때 백업을 수행할 수 있는지 여부그리고 가능하다면, 성능에 어떤 영향이 있을까요?
* 사용자의 지리적 분포즉, 언제 백업을 수행할 수 있습니까?
* 재해 복구 정책백업 데이터를 저장해야 하는 위치(예: 오프사이트, 특정 매체 등)에 대한 지침이 있습니까?

전체 백업은 정기적인 간격(예: 매일, 주별 또는 월별)으로 수행되며, 시간별, 일별 또는 주별 간에 증분 백업을 수행합니다.

>[!CAUTION]
>
>운영 인스턴스의 백업을 구현할 때 백업이 성공적으로 복원될 수 있도록 *테스트를 수행해야 합니다.*
>
>이렇게 하지 않으면 백업은 잠재적으로 무용지물이 될 수 있습니다(최악의 경우 시나리오).

>[!NOTE]
>
>백업 성능에 대한 자세한 내용은 [백업 성능](/help/sites-deploying/configuring-performance.md#backup-performance) 섹션을 참조하십시오.

### 소프트웨어 설치 백업 {#backing-up-your-software-installation}

설치 후 또는 구성의 중요한 변경 사항이 발생하면 소프트웨어 설치를 백업하십시오.

이렇게 하려면 [전체 리포지토리를 백업한 후 다음을 수행해야 합니다.](#backing-up-your-repository)

1. AEM을 중지합니다.
1. 파일 시스템에서 전체 `<cq-installation-dir>`를 백업합니다.

>[!CAUTION]
>
>타사 응용 프로그램 서버를 운영하는 경우 추가 폴더가 다른 위치에 있을 수 있으며 백업해야 할 수도 있습니다. 응용 프로그램 서버 설치에 대한 자세한 내용은 [응용 프로그램 서버와 AEM을 설치하는 방법](/help/sites-deploying/application-server-install.md)을 참조하십시오. [](/content/docs/en/aem/6-3/deploy/installing.md#installing adobe experience manager with application server)

>[!CAUTION]
>
>파일 데이터 저장소의 증분 백업이 지원됩니다.다른 구성 요소(예: Lucene 인덱스)에 대해 증분 백업을 사용하는 경우 삭제된 파일도 백업에서 삭제된 것으로 표시되는지 확인하십시오.

>[!NOTE]
>
>디스크 미러링을 백업 메커니즘으로 사용할 수도 있습니다.

### 리포지토리 백업 {#backing-up-your-repository}

CRX 설명서의 [백업 및 복원](/help/sites-administering/backup-and-restore.md) 섹션에서는 CRX 저장소의 백업과 관련된 모든 문제를 다룹니다.

온라인 &quot;핫&quot; 백업 만들기에 대한 자세한 내용은 [온라인 백업 만들기](/help/sites-administering/backup-and-restore.md#online-backup)를 참조하십시오.

## 버전 삭제 {#version-purging}

**버전 삭제** 도구는 저장소의 노드 버전 또는 노드 계층 구조를 삭제하기 위한 것입니다. 기본 목적은 이전 버전의 노드를 제거하여 저장소 크기를 줄이는 데 도움이 됩니다.

이 섹션에서는 AEM의 버전 관리 기능과 관련된 유지 관리 작업을 다룹니다. **제거 버전** 도구는 저장소의 노드 버전 또는 노드 계층 구조를 삭제하기 위한 것입니다. 기본 목적은 이전 버전의 노드를 제거하여 저장소 크기를 줄이는 데 도움이 됩니다.

### 개요 {#overview}

**버전 삭제** 도구는 **버전 지정** 아래의 **[도구](/help/sites-administering/tools-consoles.md) 콘솔**&#x200B;에서 사용하거나 다음 위치에서 직접 사용할 수 있습니다.

`https://<server>:<port>/etc/versioning/purge.html`

![screen_shot_2012-03-15at14418pm](assets/screen_shot_2012-03-15at14418pm.png)

**시작** 경로제거 작업을 수행해야 하는 절대 경로입니다. 저장소 트리 탐색기를 눌러 시작 경로를 선택할 수 있습니다.

**** 재귀데이터를 삭제할 때 재귀를 선택하여 한 노드에서 작업을 수행하거나 전체 계층 구조에서 작업 중 하나를 선택할 수 있습니다. 마지막 경우 지정된 경로가 계층의 루트 노드를 정의합니다.

**유지할 최대 버전** 노드에 유지할 최대 버전 수입니다. 이 숫자가 이 값을 초과하면 가장 오래된 버전이 삭제됩니다.

**최대 버전** 페이지노드 버전의 최대 페이지입니다. 버전의 페이지가 이 값을 초과하면 삭제됩니다.

**연습** 실행컨텐츠의 버전을 제거하는 것이 확실하고 백업을 복원하지 않으면 되돌릴 수 없으므로 제거 버전 도구에서는 삭제된 버전을 미리 볼 수 있는 연습 실행 모드를 제공합니다. 제거 프로세스의 연습 실행을 시작하려면 연습 실행을 누릅니다.

**** 삭제 시작 경로에 정의된 노드의 버전 삭제를 시작합니다.

### 웹 사이트 버전 삭제 {#purging-versions-of-a-web-site}

웹 사이트의 버전을 삭제하려면 다음과 같이 하십시오.

1. **[도구](/help/sites-administering/tools-consoles.md)** **콘솔**&#x200B;로 이동하고 **버전 지정**&#x200B;을 선택하고 **버전 삭제**&#x200B;를 두 번 클릭합니다.
1. 제거할 컨텐츠의 시작 경로(예:`/content/geometrixx-outdoors`)

   * 경로에 정의된 노드만 제거하려면 **재귀**&#x200B;를 선택 취소합니다.
   * 경로에 정의된 노드를 제거하려 하고 해당 하위 항목이 **재귀**&#x200B;를 선택합니다.

1. 유지할 최대 버전 수(각 노드에 대해)를 설정합니다. 이 설정을 사용하지 않으려면 비워 둡니다.

1. 유지할 일(각 노드에 대해) 최대 버전 페이지를 설정합니다. 이 설정을 사용하지 않으려면 비워 둡니다.

1. **연습 실행**&#x200B;을 클릭하여 제거 프로세스에서 수행할 작업을 미리 봅니다.
1. **제거**&#x200B;를 클릭하여 프로세스를 시작합니다.

>[!CAUTION]
>
>저장소를 복원하지 않으면 삭제된 노드를 되돌릴 수 없습니다. 구성을 관리해야 하므로 삭제하기 전에 항상 연습 실행을 수행하는 것이 좋습니다.

### 콘솔 {#analyzing-the-console} 분석

**Dry Run** 및 **Purge** 프로세스는 처리된 모든 노드를 나열합니다. 프로세스 중에 노드는 다음 상태 중 하나를 가질 수 있습니다.

* `ignore (not versionnable)`:노드는 버전 지정을 지원하지 않으며 프로세스 중에 무시됩니다.

* `ignore (no version)`:노드에 버전이 없으며 프로세스 중에 무시됩니다.

* `retained`:노드가 삭제되지 않습니다.
* `purged`:노드가 삭제됩니다.

또한 이 콘솔에서는 버전에 대한 유용한 정보를 제공합니다.

* `V 1.0`:버전 번호입니다.
* `V 1.0.1`*:별은 버전이 현재 버전임을 나타냅니다.

* `Thu Mar 15 2012 08:37:32 GMT+0100`:버전 날짜입니다.

다음 예에서

* 버전 버전이 2일을 초과하므로 **[!DNL Shirts]** 버전이 삭제됩니다.
* 버전 수가 5개를 초과하므로 **[!DNL Tonga Fashions!]** 버전이 삭제됩니다.

![global_version_screenshot](assets/global_version_screenshot.png)

## 감사 레코드 및 로그 파일 작업 {#working-with-audit-records-and-log-files}

AEM(Adobe Experience Manager)과 관련된 레코드 및 로그 파일을 감사하는 방법은 다양한 위치에서 찾을 수 있습니다. 찾을 수 있는 위치에 대한 개요를 제공하기 위해 다음 항목이 제공됩니다.

### 로그 작업 {#working-with-logs}

AEM WCM은 세부 로그를 기록합니다. 압축을 풀고 빠른 시작을 시작하면 로그를 찾을 수 있습니다.

* `<cq-installation-dir>/crx-quickstart/logs/`

* `<cq-installation-dir>/crx-quickstart/repository/`

#### 로그 파일 순환 {#log-file-rotation}

로그 파일 순환은 새 파일을 주기적으로 작성하여 파일 증가를 제한하는 프로세스를 말합니다. AEM에서 `error.log` 로그 파일은 지정된 규칙에 따라 하루에 한 번 회전됩니다.

* `error.log` 파일의 이름이 {original_filename} `.yyyy-MM-dd` 패턴에 따라 변경되었습니다. 예를 들어 2010년 7월 11일에 현재 로그 파일의 이름이 `error.log-2010-07-10`으로 변경된 다음 새 `error.og`이 만들어집니다.

* 이전 로그 파일은 삭제되지 않으므로 디스크 사용을 제한하기 위해 정기적으로 이전 로그 파일을 정리해야 합니다.

>[!NOTE]
>
>AEM 설치를 업그레이드하는 경우 AEM에서 더 이상 사용하지 않는 기존 로그 파일은 디스크에 유지됩니다. 위험없이 제거할 수 있습니다 모든 새 로그 항목이 새 로그 파일에 기록됩니다.

### 로그 파일 찾기 {#finding-the-log-files}

다양한 로그 파일은 AEM을 설치한 파일 서버에 저장됩니다.

* `<cq-installation-dir>/crx-quickstart/logs`

   * `access.log`
AEM WCM 및 리포지토리에 대한 모든 액세스 요청이 여기에 등록됩니다.

   * `audit.log`
중재 작업이 여기에 등록됩니다.

   * `error.log`
여기에 오류 메시지(다양한 수준의 심각도)가 등록됩니다.

   * [ `ImageServer-<PortId>-yyyy>-<mm>-<dd>.log`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/config-admin/server-logging/c-image-server-log.html)
이 로그는 이 활성화된 경우에만  [!DNL Dynamic Media] 사용됩니다. 내부 ImageServer 프로세스의 동작을 분석하는 데 사용되는 통계 및 분석 정보를 제공합니다.

   * `request.log`
각 액세스 요청은 응답과 함께 여기에 등록됩니다.

   * [ `s7access-<yyyy>-<mm>-<dd>.log`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/config-admin/server-logging/c-access-log.html)
이 로그는 이 활성화된 경우에만  [!DNL Dynamic Media] 사용됩니다. s7access 로그는 [!DNL Dynamic Media]에 대한 각 요청을 `/is/image` 및 `/is/content`에 기록합니다.

   * `stderr.log`
시작하는 동안 생성된 다양한 수준의 심각도를 나타내는 오류 메시지를 다시 포함합니다. 기본적으로 로그 수준은 
`Warning` ( `WARN`)

   * `stdout.log`
시작하는 동안 이벤트를 나타내는 로깅 메시지를 보류합니다.

   * `upgrade.log`
에서 실행되는 모든 업그레이드 작업의 로그를 제공합니다. 
`com.day.compat.codeupgrade` 및  `com.adobe.cq.upgradesexecutor` 패키지를 표시합니다.

* `<cq-installation-dir>/crx-quickstart/repository`

   * `revision.log`
저널링 정보 개정.

>[!NOTE]
>
>ImageServer 및 s7access 로그는 **system/console/status-Bundelist** 페이지에서 생성된 **Download Full **package에 포함되지 않습니다. 지원을 위해 [!DNL Dynamic Media] 문제가 있는 경우 고객 지원에 문의할 때 ImageServer 및 s7access 로그도 추가하시기 바랍니다.

### 디버그 로그 수준 {#activating-the-debug-log-level} 활성화

기본 로그 수준([Apache Sling 로깅 구성](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration))은 정보이므로 디버그 메시지가 기록되지 않습니다.

로거에 대한 디버그 로그 레벨을 활성화하려면 `org.apache.sling.commons.log.level` 속성을 리포지토리에서 디버깅하도록 설정합니다. 예를 들어 `/libs/sling/config/org.apache.sling.commons.log.LogManager`에서 [글로벌 Apache Sling 로깅](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)을 구성합니다.

>[!CAUTION]
>
>많은 로그 항목을 생성하므로 리소스를 소비하므로 디버그 로그 수준에서 로그를 필요한 기간보다 오래 두지 마십시오.

디버그 파일의 한 줄은 일반적으로 DEBUG로 시작하며 로그 수준, 설치 관리자 작업 및 로그 메시지를 제공합니다. 예:

```shell
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

로그 수준은 다음과 같습니다.

| 0 | 치명적인 오류 | 작업이 실패하여 설치 프로그램을 계속할 수 없습니다. |
|---|---|---|
| 1 | 오류 | 작업이 실패했습니다. 설치가 진행되지만 AEM WCM 일부가 제대로 설치되지 않아 작동하지 않습니다. |
| 2 | 경고 | 작업에 성공했지만 문제가 발생했습니다. AEM WCM이 제대로 작동하지 않거나 작동하지 않을 수 있습니다. |
| 3 | 정보 | 작업이 성공했습니다. |

### 사용자 지정 로그 파일 {#create-a-custom-log-file} 만들기

>[!NOTE]
>
>Adobe Experience Manager을 사용하여 작업하는 경우 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 여러 가지가 있습니다.자세한 내용 및 권장 방법은 [OSGi](/help/sites-deploying/configuring-osgi.md) 구성 을 참조하십시오.

특정 상황에서 다른 로그 수준으로 사용자 지정 로그 파일을 만들 수 있습니다. 다음 방법으로 저장소에서 이 작업을 수행할 수 있습니다.

1. 아직 존재하지 않는 경우 프로젝트 `/apps/<project-name>/config`에 대해 새 구성 폴더( `sling:Folder`)를 만드십시오.
1. `/apps/<project-name>/config`에서 새 [Apache Sling Logging Configuration](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingloggerconfigurationfactoryconfiguration)에 대한 노드를 만듭니다.

   * 이름:`org.apache.sling.commons.log.LogManager.factory.config-<identifier>`(로거이므로)

      여기서 `<identifier>`은(는) 인스턴스를 식별하기 위해 입력하는 자유 텍스트로 대체됩니다(이 정보를 생략할 수 없음).

      예, `org.apache.sling.commons.log.LogManager.factory.config-MINE`

   * 유형: `sling:OsgiConfig`
   >[!NOTE]
   >
   >기술적인 요구 사항은 아니지만 `<identifier>`을 고유하게 만드는 것이 좋습니다.

1. 이 노드에서 다음 속성을 설정합니다.

   * 이름: `org.apache.sling.commons.log.file`

      유형:문자열

      값:로그 파일을 지정합니다.예: `logs/myLogFile.log`

   * 이름: `org.apache.sling.commons.log.names`

      유형:문자열[] (문자열 + 다중)

      값:로거가 메시지를 기록할 OSGi 서비스를 지정합니다.예를 들어, 다음 항목이 모두 있습니다.

      * `org.apache.sling`
      * `org.apache.felix`
      * `com.day`
   * 이름: `org.apache.sling.commons.log.level`

      유형:문자열

      값:필요한 로그 수준( `debug`, `info`, `warn` 또는 `error`)을 지정하십시오.예: `debug`

   * 필요에 따라 다른 매개 변수를 구성합니다.

      * 이름: `org.apache.sling.commons.log.pattern`

         유형: `String`

         값:필요에 따라 로그 메시지 패턴을 지정합니다.예

         `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`
   >[!NOTE]
   >
   >`org.apache.sling.commons.log.pattern` 에서는 최대 6개의 인수를 지원합니다.
   >
   >{0} `java.util.Date` 유형의 타임스탬프
   >
   >로그 마커 {1}
   >
   >{2} 현재 스레드의 이름
   >
   >{3} 로거의 이름
   >
   >로그 수준 {4}
   >
   >로그 메시지 {5}
   >
   >로그 호출에 `Throwable`이 포함된 경우 stacktrace가 메시지에 추가됩니다.

   >[!CAUTION]
   >
   >org.apache.sling.commons.log.names에는 값이 있어야 합니다.

   >[!NOTE]
   >
   >로그 작성기 경로는 `crx-quickstart` 위치를 기준으로 합니다.
   >
   >따라서 다음과 같이 지정된 로그 파일입니다.
   >
   >`logs/thelog.log`
   >
   >쓰기 작업:
   >
   >`<cq-installation-dir>/crx-quickstart/logs/thelog.log`.
   >
   >그리고 다음과 같이 지정된 로그 파일입니다.
   >
   >`../logs/thelog.log`
   >
   >디렉토리에 쓰기:
   >
   >`<cq-installation-dir>/logs/`\
   >(즉, `<cq-installation-dir>/crx-quickstart/` 옆의)

1. 이 단계는 새 작성기가 필요한 경우에만 필요합니다(예: 기본 작성기와 다른 구성 사용).

   >[!CAUTION]
   >
   >기존 기본값이 적합하지 않은 경우에만 새 로깅 작성기 구성이 필요합니다.
   >
   >명시적 작성기가 구성되어 있지 않으면 시스템은 기본값으로 암시적 작성기를 자동으로 생성합니다.

   `/apps/<project-name>/config`에서 새 [Apache Sling 로깅 작성기 구성](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingwriterconfigurationfactoryconfiguration)에 대한 노드를 만듭니다.

   * 이름:`org.apache.sling.commons.log.LogManager.factory.writer-<identifier>` (작성기이므로)

      로거의 경우처럼 `<identifier>`은(는) 인스턴스를 식별하기 위해 입력하는 자유 텍스트로 대체됩니다(이 정보를 생략할 수 없음). 예, `org.apache.sling.commons.log.LogManager.factory.writer-MINE`

   * 유형: `sling:OsgiConfig`
   >[!NOTE]
   >
   >기술적인 요구 사항은 아니지만 `<identifier>`을 고유하게 만드는 것이 좋습니다.

   이 노드에서 다음 속성을 설정합니다.

   * 이름: `org.apache.sling.commons.log.file`

      유형: `String`

      값:로거에 지정된 파일과 일치하도록 로그 파일을 지정합니다.

      이 예제의 경우 `../logs/myLogFile.log`

   * 필요에 따라 다른 매개 변수를 구성합니다.

      * 이름: `org.apache.sling.commons.log.file.number`

         유형: `Long`

         값:보관하려는 로그 파일 수를 지정합니다.예: `5`

      * 이름: `org.apache.sling.commons.log.file.size`

         유형: `String`

         값:필요에 따라 크기/날짜별로 파일 회전을 제어합니다.예: `'.'yyyy-MM-dd`
   >[!NOTE]
   >
   >`org.apache.sling.commons.log.file.size` 다음 중 하나를 설정하여 로그 파일의 회전을 제어합니다.
   >
   >* 최대 파일 크기
   >* 시간/날짜 일정

   >
   >새 파일을 만들 시기(이름 패턴에 따라 이름이 변경된 기존 파일)를 나타냅니다.
   >
   >* 크기 제한은 숫자로 지정할 수 있습니다. 크기 표시기가 없으면 바이트 수로 적용되거나, 크기 표시기 중 하나( `KB`, `MB` 또는 `GB` )를 추가할 수 있습니다(대/소문자 구분은 무시됨).
   >* 시간/날짜 일정은 `java.util.SimpleDateFormat` 패턴으로 지정할 수 있습니다. 이 설정은 파일을 회전할 기간을 정의합니다.또한 회전된 파일(식별을 위해)에 추가된 접미사도 나타납니다.

   >
   >기본값은 &#39;.&#39;입니다.yyyy-MM-dd(일별 로그 순환용).
   >
   >따라서 예를 들어, 2010년 1월 20일 자정(또는 이 경우 후에 첫 번째 로그 메시지가 정확하면) ../logs/error.log 의 이름이 ../logs/error.log.2010-01-20으로 변경됩니다. 1월 21일에 대한 로깅은 다음 변경 시 롤오버될 때까지 (신규 및 비어 있음) ../logs/error.log 로 출력됩니다.
   >
   >| `'.'yyyy-MM` | 매월 초에 회전 |
   >|---|---|
   >| `'.'yyyy-ww` | 각 주의 첫 날에 회전이 가능합니다(로케일에 따라 다름). |
   >| `'.'yyyy-MM-dd` | 매일 자정에 순환하세요. |
   >| `'.'yyyy-MM-dd-a` | 매일 자정과 정오에 회전하세요. |
   >| `'.'yyyy-MM-dd-HH` | 매시간 맨 위에서 회전하세요. |
   >| `'.'yyyy-MM-dd-HH-mm` | 매 분 초에 회전하세요. |
   >
   >참고:시간/날짜를 지정할 때:
   > 1. 한 쌍의 작은 따옴표(&#39; &#39;) 내에 &quot;이스케이프&quot; 리터럴 텍스트를 포함해야 합니다.
      >
      >     
      이는 특정 문자가 패턴 문자로 해석되지 않도록 하기 위한 것입니다.
      >
      >  
   1. 옵션의 아무 곳에나 유효한 파일 이름에 사용할 수 있는 문자만 사용하십시오.


1. 선택한 도구로 새 로그 파일을 읽습니다.

   이 예제로 만든 로그 파일은 `../crx-quickstart/logs/myLogFile.log`입니다.

Felix 콘솔은 `../system/console/slinglog`에서 Sling 로그 지원에 대한 정보도 제공합니다.예: `https://localhost:4502/system/console/slinglog`

### 감사 레코드 찾기 {#finding-the-audit-records}

감사 기록은 누가 언제 무엇을 했는지 기록하기 위해 보관된다. AEM WCM 및 OSGi 이벤트 모두에 대해 다양한 감사 레코드가 생성됩니다.

#### AEM WCM 감사 레코드 페이지 작성 시 표시 {#aem-wcm-audit-records-shown-when-page-authoring}

1. 페이지를 엽니다.
1. 사이드 킥에서 잠금 아이콘이 있는 탭을 선택한 다음 **감사 로그.. 를 두 번 클릭합니다.**
1. 현재 페이지에 대한 감사 레코드 목록을 보여주는 새 창이 열립니다.

   ![screen_shot_2012-02-02at43601pm](assets/screen_shot_2012-02-02at43601pm.png)

1. 창을 닫으려면 **확인**&#x200B;을 클릭합니다.

#### AEM WCM 감사 레코드 {#aem-wcm-auditing-records-within-the-repository}

`/var/audit` 폴더 내에서 감사 레코드는 리소스에 따라 보관됩니다. 개별 레코드 및 개별 레코드가 포함된 정보를 볼 수 있을 때까지 드릴다운할 수 있습니다.

이러한 항목에는 페이지를 편집할 때 표시된 것과 동일한 정보가 있습니다.

#### 웹 콘솔에서 OSGi 감사 레코드 {#osgi-audit-records-from-the-web-console}

OSGi 이벤트는 AEM 웹 콘솔의 **구성 상태** 탭 -> **로그 파일** 탭에서 볼 수 있는 감사 레코드도 생성합니다.

![screen_shot_2012-02-13at50346pm](assets/screen_shot_2012-02-13at50346pm.png)

## 복제 에이전트 모니터링 {#monitoring-your-replication-agents}

[복제 큐](/help/sites-deploying/replication.md)를 모니터링하여 큐가 다운되거나 차단되는 시점을 감지할 수 있습니다. 이 경우 게시 인스턴스 또는 외부 시스템에 문제가 있을 수 있습니다.

* 모든 필요한 큐가 활성화됩니까?
* 비활성화된 큐가 여전히 필요합니까?
* 모든 `enabled` 큐에는 정상 작업을 나타내는 상태 `idle` 또는 `active`가 있어야 합니다.대기열은 수신자측에서 문제가 발생할 수 있는 경우 `blocked`일 수 없습니다.

* 큐 크기가 시간이 지남에 따라 증가하면 차단된 큐를 나타낼 수 있습니다.

복제 에이전트를 모니터하려면

1. AEM에서 **도구** 탭에 액세스합니다.
1. **복제**&#x200B;를 클릭합니다.
1. 해당 환경(왼쪽 또는 오른쪽 창)의 에이전트에 대한 링크를 두 번 클릭합니다.예: **작성자**&#x200B;의 에이전트.

   결과 창에는 대상 및 상태를 포함하여 작성 환경에 대한 모든 복제 에이전트에 대한 개요가 표시됩니다.

1. 해당 에이전트에 대한 자세한 정보를 표시하려면 해당 에이전트 이름(링크임)을 클릭합니다.

   ![chlimage_1](assets/chlimage_1.jpeg)

   여기에서 다음을 수행할 수 있습니다.

   * 에이전트가 활성화되어 있는지 확인합니다.
   * 복제 타겟을 확인합니다.
   * 복제 큐가 현재 활성 상태인지(활성화됨)를 확인하십시오.
   * 큐에 항목이 있는지 확인합니다.
   * **** 대기열 항목  **** 표시를 갱신하려면 새로 고침 또는 지우기이렇게 하면 항목이 큐에 들어가 나가는 것을 볼 수 있습니다.

   * **복제 에이전트** 의 작업 로그에 액세스하려면 로그를 봅니다.
   * **대상** 인스턴스에 대한 연결을 테스트합니다.
   * **필요한** 경우 큐 항목을 강제로 다시 시도합니다.

   >[!CAUTION]
   >
   >게시 인스턴스의 역방향 복제 출력소에 &quot;연결 테스트&quot; 링크를 사용하지 마십시오.
   >
   >Outbox 큐에 대해 복제 테스트가 수행되면 테스트 복제보다 오래된 모든 항목은 모든 역방향 복제를 사용하여 다시 처리됩니다.
   >
   >이러한 항목이 이미 큐에 있는 경우 다음 XPath JCR 쿼리로 해당 항목을 찾을 수 있으며 제거해야 합니다.
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

다시 솔루션을 개발하여 모든 복제 에이전트( `/etc/replication/author` 또는 `/etc/replication/publish` 아래에 있음)를 검색한 다음 에이전트( `enabled`, `disabled`)와 기본 큐( `active`, `idle`, `blocked`)의 상태를 확인할 수 있습니다.

## 성능 모니터링 {#monitoring-performance}

[성능 ](/help/sites-deploying/configuring-performance.md) 최적화는 개발 중 포커스를 받는 대화형 프로세스입니다. 배포 후에는 일반적으로 특정 간격이나 이벤트 후에 검토합니다.

최적화를 위해 정보를 수집하는 동안 사용되는 방법도 지속적인 모니터링에 사용할 수 있습니다.

>[!NOTE]
>
>성능을 개선하기 위해 사용할 수 있는 특정 [구성도 확인할 수 있습니다](/help/sites-deploying/configuring-performance.md#configuring-for-performance).

다음은 일반적인 성능 문제를 찾아 해결하는 방법과 함께 설명합니다.

| 영역 | 증상 | 용량 증가 | 볼륨을 줄이려면... |
|---|---|---|---|
| 클라이언트 | 높은 클라이언트 CPU 사용. | 더 높은 성능을 사용하여 클라이언트 CPU를 설치합니다. | (HTML) 레이아웃을 단순화합니다. |
|  | 서버 CPU 사용량이 적습니다. | 더 빠른 브라우저로 업그레이드하십시오. | 클라이언트 측 캐시를 개선합니다. |
|  | 어떤 고객은 빠르고, 느리기도 합니다. |  |  |
| 서버 |  |  |  |
| 네트워크 | 서버와 클라이언트 모두에서 CPU 사용량이 적습니다. | 네트워크 병목 현상을 제거합니다. | 클라이언트 캐시의 구성을 개선/최적화합니다. |
|  | 서버에서 로컬을 검색하는 속도가 비교적 빠릅니다. | 네트워크 대역폭을 늘립니다. | 웹 페이지의 &quot;가중치&quot;를 줄입니다(예: 이미지를 줄이고 최적화된 HTML). |
| 웹 서버 | 웹 서버의 CPU 사용량이 높습니다. | 웹 서버를 클러스터링합니다. | 페이지당 히트 수(방문)를 줄입니다. |
|  |  | 하드웨어 로드 밸런서를 사용합니다. |  |
| 애플리케이션 | 서버 CPU 사용량이 높습니다. | AEM 인스턴스를 클러스터링합니다. | CPU 및 메모리 돼지를 검색 및 제거(코드 검토, 타이밍 출력 등 사용) |
|  | 메모리 사용량이 많습니다. |  | 모든 수준에서 캐싱을 개선합니다. |
|  | 응답 시간이 적습니다. |  | 템플릿 및 구성 요소(예: 구조, 논리)를 최적화합니다. |
| 저장소 |  |  |  |
| 캐시 |  |  |  |

성능 문제는 연결 속도, CPU 로드 등 웹 사이트와 관련이 없는 여러 원인에서 발생할 수 있습니다.

또한 모든 방문자나 방문자의 하위 세트에만 영향을 줄 수 있습니다.

일반 성능을 최적화하거나 특정 문제를 해결하기 전에 이러한 모든 정보를 획득, 정렬 및 분석해야 합니다.

* 성능 문제가 발생하기 전:

   * 가능한 한 많은 정보를 수집하여 정상적인 상황에서 시스템에 대한 유용한 실무 지식을 쌓는다

* 성능 문제가 발생하는 경우:

   * 일반적인 성능이 뛰어난 다른 클라이언트에서 또는 서버 자체(가능한 경우)에서 하나 이상의 표준 웹 브라우저를 사용하여 복제해 보십시오
   * 적절한 시간 범위 내에서 시스템과 관련된 변경 사항이 변경되었는지, 그리고 이러한 변경 사항이 성능에 영향을 줄 수 있는지 확인하십시오
   * 다음과 같은 질문을 합니다.

      * 문제는 특정 시에만 발생합니까?
      * 특정 페이지에서만 문제가 발생합니까?
      * 다른 요청이 영향을 받습니까?
   * 정상적인 상황에서 시스템 지식과 비교할 수 있도록 가능한 많은 정보를 수집합니다.


### 성능 모니터링 및 분석 도구 {#tools-for-monitoring-and-analyzing-performance}

다음은 성능 모니터링 및 분석에 사용할 수 있는 몇 가지 도구에 대한 간략한 개요를 제공합니다.

이러한 항목 중 일부는 운영 체제에 따라 다릅니다.

<table>
 <tbody>
  <tr>
   <td>도구</td>
   <td>분석하는 데 사용됨..</td>
   <td>사용/추가 정보...</td>
  </tr>
  <tr>
   <td>request.log</td>
   <td>응답 시간 및 동시성.</td>
   <td><a href="#interpreting-the-request-log">request.log 해석</a>.</td>
  </tr>
  <tr>
   <td>트러스/구조</td>
   <td>페이지 로드</td>
   <td><p>시스템 호출과 신호를 추적하는 Unix/Linux 명령 로그 수준을 <code>INFO</code>로 늘립니다.</p> <p>요청당 페이지 로드 횟수, 페이지 등을 분석합니다.</p> </td>
  </tr>
  <tr>
   <td>스레드 덤프</td>
   <td>JVM 스레드를 관찰합니다. 연락처, 잠금 및 장기 러너를 식별합니다.</td>
   <td><p>운영 체제에 따라 다름:<br /> - Unix/Linux:<code>kill -QUIT &lt;<em>pid</em>&gt;</code><br /> - Windows(콘솔 모드):Ctrl-Break<br /> </p> <p>분석 도구는 <a href="https://java.net/projects/tda/">TDA</a>.<br />와 같이 사용할 수도 있습니다. </p> </td>
  </tr>
  <tr>
   <td>Heap 덤프</td>
   <td>메모리 부족 문제로 인해 성능이 저하됩니다.</td>
   <td><p>AEM에 대한 Java 호출에:<br /> <code>-XX:+HeapDumpOnOutOfMemoryError</code><br /> 옵션을 추가합니다.</p> <p>HotSpot VM이 포함된 Java SE 6용 <a href="https://java.sun.com/javase/6/webnotes/trouble/TSG-VM/html/clopts.html#gbzrr">문제 해결 설명서</a>를 참조하십시오.</p> </td>
  </tr>
  <tr>
   <td>시스템 호출</td>
   <td>시간 문제를 식별합니다.</td>
   <td><p><code>System.currentTimeMillis()</code> 또는 <code>com.day.util</code>.Timing을 호출하면 코드에서 또는 <a href="#html-comments">HTML-comments</a>를 통해 타임스탬프를 생성할 수 있습니다.</p> <p><strong>참고:</strong>  필요에 따라 활성화/비활성화할 수 있도록 구현해야 합니다.시스템이 제대로 가동되면 통계수집 오버헤드가 필요 없다.</p> </td>
  </tr>
  <tr>
   <td>Apache Bench</td>
   <td>메모리 누수를 확인하고 응답 시간을 선택적으로 분석합니다.</td>
   <td><p>기본 사용 방법은 다음과 같습니다.</p> <p><code>ab -k -n &lt;<em>requests</em>&gt; -c &lt;<em>concurrency</em>&gt; &lt;<em>url</em>&gt;</code></p> <p>자세한 내용은 <a href="#apache-bench">Apache Bench</a> 및 <a href="https://httpd.apache.org/docs/2.2/programs/ab.html">ab 매뉴얼 페이지</a>를 참조하십시오.</p> </td>
  </tr>
  <tr>
   <td>검색 분석</td>
   <td> </td>
   <td>검색 쿼리를 오프라인으로 실행하고, 쿼리의 응답 시간을 식별하고, 테스트 및 확인 결과 집합을 확인합니다.<br /> </td>
  </tr>
  <tr>
   <td>JMeter</td>
   <td>부하 및 기능 테스트.</td>
   <td><a href="https://jakarta.apache.org/jmeter/">https://jakarta.apache.org/jmeter/</a></td>
  </tr>
  <tr>
   <td>JProfiler</td>
   <td>심층적인 CPU 및 메모리 프로파일링.</td>
   <td><a href="https://www.ej-technologies.com/">https://www.ej-technologies.com/</a></td>
  </tr>
  <tr>
   <td>JConsole</td>
   <td>JVM 지표 및 스레드를 관찰합니다.</td>
   <td><p>사용:jconsole</p> <p><a href="https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html">jconsole</a> 및 <a href="#monitoring-performance-using-jconsole">JConsole</a>을 사용하여 성능 모니터링 을 참조하십시오.</p> <p><strong>참고:</strong> JDK 1.6을 사용하여 JConsole은 플러그인으로 확장 가능합니다.예를 들어 Top 또는 TDA(스레드 덤프 분석기)가 있습니다.</p> </td>
  </tr>
  <tr>
   <td>Java VisualVM</td>
   <td>JVM 지표, 스레드, 메모리 및 프로파일링을 관찰합니다.</td>
   <td><p>사용:jvisualvm 또는 visualvm<br /> </p> <p><a href="https://java.sun.com/javase/6/docs/technotes/tools/share/jvisualvm.html">jvisualvm</a>, <a href="https://visualvm.dev.java.net/">visualvm</a> 및 <a href="#monitoring-performance-using-j-visualvm">VisualVM</a>을 사용하여 성능 모니터링 을 참조하십시오.</p> <p><strong>참고:</strong> JDK 1.6을 사용하면 VisualVM을 플러그인으로 확장할 수 있습니다.</p> </td>
  </tr>
  <tr>
   <td>트러스/strace, lsof</td>
   <td>깊이 커널 호출 및 프로세스 분석(Unix)</td>
   <td>Unix/Linux 명령</td>
  </tr>
  <tr>
   <td>시간 통계</td>
   <td>페이지 렌더링에 대한 시간 통계 를 참조하십시오.</td>
   <td><p>페이지 렌더링에 대한 타이밍 통계를 보려면 <strong>Ctrl-Shift-U</strong>을 URL에 설정된 <code>?debugClientLibs=true</code>와 함께 사용할 수 있습니다.</p> </td>
  </tr>
  <tr>
   <td>CPU 및 메모리 프로파일링 도구<br /> </td>
   <td><a href="#interpreting-the-request-log">개발</a> 중 느린 요청을 분석할 때 사용됩니다.</td>
   <td>예: <a href="https://www.yourkit.com/">YourKit</a></td>
  </tr>
  <tr>
   <td><a href="#information-collection">정보 수집</a></td>
   <td>설치 진행 상태입니다.</td>
   <td>설치에 대해 가능한 한 많이 알고 있으면 성능 변화를 일으킬 수 있는 대상과 이러한 변경 사항이 정당한지 여부를 추적하는 데 도움이 됩니다. 중요한 변경 사항을 쉽게 볼 수 있도록 이러한 지표를 정기적으로 수집해야 합니다.</td>
  </tr>
 </tbody>
</table>

### request.log {#interpreting-the-request-log} 해석

이 파일은 AEM에 수행된 모든 요청에 대한 기본 정보를 등록합니다. 이 귀중한 결론에서 추출할 수 있습니다.

`request.log`은 요청이 얼마나 오래 걸리는지 확인할 수 있는 기본 제공 방법을 제공합니다. 개발 목적으로 `tail -f` `request.log` 및 느린 응답 시간을 관찰하는 것이 유용합니다. 더 큰 `request.log`을 분석하려면 [응답 시간](#using-rlog-jar-to-find-requests-with-long-duration-times)에 대해 정렬 및 필터링할 수 있는 `rlog.jar`를 사용하는 것이 좋습니다.

`request.log`에서 &quot;느린&quot; 페이지를 분리한 다음 개별적으로 조정하여 더 나은 성능을 제공하는 것이 좋습니다. 이 작업은 일반적으로 구성 요소당 성능 지표를 포함하거나 ` [yourkit](https://www.yourkit.com/)` 등의 성능 프로파일링 도구를 사용하여 수행됩니다.

#### 웹 사이트에서 트래픽 모니터링 {#monitoring-traffic-on-your-website}

요청 로그는 수행된 각 요청과 수행된 응답을 등록합니다.

```xml
09:43:41 [66] -> GET /author/y.html HTTP/1.1
09:43:41 [66] <- 200 text/html 797ms
```

특정 기간(예: 다양한 24시간 기간 이상) 내의 모든 GET 항목을 합하면 웹 사이트의 평균 트래픽에 대한 설명을 만들 수 있습니다.

#### request.log {#monitoring-response-times-with-the-request-log} 를 사용하여 응답 시간 모니터링

성능 분석을 위한 좋은 시작점은 요청 로그입니다.

`<cq-installation-dir>/crx-quickstart/logs/request.log`

로그는 다음과 같습니다(간단히 하기 위해 줄이 짧아짐).

```xml
31/Mar/2009:11:32:57 +0200 [379] -> GET /path/x HTTP/1.1
31/Mar/2009:11:32:57 +0200 [379] <- 200 text/html 33ms
31/Mar/2009:11:33:17 +0200 [380] -> GET /path/y HTTP/1.1
31/Mar/2009:11:33:17 +0200 [380] <- 200 application/json 39ms
```

이 로그에는 요청 또는 응답당 한 줄이 있습니다.

* 각 요청 또는 응답이 수행된 날짜입니다.
* 대괄호 안의 요청 수입니다. 이 숫자는 요청 및 응답에 대해 일치합니다.
* 요청인지(오른쪽 화살표) 아니면 응답(왼쪽 화살표)인지를 나타내는 화살표.
* 요청의 경우 다음 내용이 포함됩니다.

   * 메서드(일반적으로 GET, HEAD 또는 POST)
   * 요청한 페이지
   * 프로토콜

* 응답의 경우 다음 내용이 포함됩니다.

   * 상태 코드(200은 &quot;성공&quot;을 의미하며 404는 &quot;페이지를 찾을 수 없음&quot;을 의미합니다.
   * MIME 유형
   * 응답 시간

작은 스크립트를 사용하여 로그 파일에서 필요한 정보를 추출하고 원하는 통계를 취합할 수 있습니다. 여기에서 어떤 페이지 또는 페이지 유형이 느리는지, 그리고 전체 성능이 만족스러운지 확인할 수 있습니다.

#### request.log {#monitoring-search-response-times-with-the-request-log} 를 사용하여 검색 응답 시간 모니터링

검색 요청은 로그 파일에도 등록됩니다.

```xml
31/Mar/2009:11:35:34 +0200 [338] -> GET /author/playground/en/tools/search.html?query=dilbert&size=5&dispenc=utf-8 HTTP/1.1
31/Mar/2009:11:35:34 +0200 [338] <- 200 text/html 1562ms
```

따라서 위와 같이 스크립트를 사용하여 관련 정보를 추출하고 통계를 작성할 수 있습니다.

그러나 응답 시간을 결정한 후에는 요청에 시간이 걸리는 이유와 응답을 개선하기 위해 수행할 수 있는 작업을 분석해야 할 수 있습니다.

#### 동시 사용자 수 및 영향 모니터링 {#monitoring-the-number-and-impact-of-concurrent-users}

다시 `request.log`을 사용하여 동시 시청 및 시스템 반응을 모니터링할 수 있습니다.

부정적인 영향을 보기 전에 시스템에서 처리할 수 있는 동시 사용자 수를 판별하려면 테스트를 수행해야 합니다. 다시 스크립트를 사용하여 로그 파일에서 결과를 추출할 수 있습니다.

* 특정 시간 범위(예: 1분) 내에 수행되는 요청 수를 모니터링합니다
* 같은 시간에(가능한 한 가깝게) 동일한 요청을 수행하는 특정 수의 사용자의 효과를 테스트합니다.예: **저장**&#x200B;을 동시에 클릭하는 사용자 30명.

```xml
31/Mar/2009:11:45:29 +0200 [333] -> GET /author/libs/Personalize/content/statics.close.gif HTTP/1.1
31/Mar/2009:11:45:29 +0200 [334] -> GET /author/libs/Personalize/content/statics.detach.gif HTTP/1.1
31/Mar/2009:11:45:30 +0200 [335] -> GET /author/libs/CFC/content/imgs/logo.rZMNURccynWcTpCxyuBNiTCoiBMmw000.default.gif HTTP/1.1
31/Mar/2009:11:45:32 +0200 [335] <- 304 text/html 0ms
31/Mar/2009:11:45:33 +0200 [334] <- 200 image/gif 31ms
31/Mar/2009:11:45:38 +0200 [333] <- 200 image/gif 31ms
31/Mar/2009:11:45:42 +0200 [336] -> GET /author/libs/CFC/content/imgs/logo.rZMNURccynWcTZRXunQbbQtvuuCMbRRBuWXz0000.default.gif HTTP/1.1
31/Mar/2009:11:45:43 +0200 [337] -> GET /author/titlebar_bg.gif HTTP/1.1
31/Mar/2009:11:45:43 +0200 [336] <- 304 text/html 0ms
31/Mar/2009:11:45:44 +0200 [337] <- 304 text/html 0ms
```

### rlog.jar를 사용하여 기간이 긴 요청을 찾습니다 {#using-rlog-jar-to-find-requests-with-long-duration-times}

AEM에는 다음과 같은 위치에 있는 다양한 도우미 도구가 포함되어 있습니다.
`<cq-installation-dir>/crx-quickstart/opt/helpers`

이 중 하나인 `rlog.jar` 를 사용하여 요청이 가장 긴 시간에서 가장 짧은 시간 동안 지속 기간별로 표시되도록 `request.log` 을 빠르게 정렬할 수 있습니다.

다음 명령은 가능한 인수를 보여 줍니다.

```shell
$java -jar rlog.jar
Request Log Analyzer Version 21584 Copyright 2005 Day Management AG
Usage:
  java -jar rlog.jar [options] <filename>
Options:
  -h               Prints this usage.
  -n <maxResults>  Limits output to <maxResults> lines.
  -m <maxRequests> Limits input to <maxRequest> requests.
  -xdev            Exclude POST request to CRXDE.
```

예를 들어 `request.log` 파일을 매개 변수로 지정하여 실행하고 가장 긴 기간이 있는 10개의 첫 번째 요청을 표시할 수 있습니다.

```shell
$ java -jar ../opt/helpers/rlog.jar -n 10 request.log
*Info * Parsed 464 requests.
*Info * Time for parsing: 22ms
*Info * Time for sorting: 2ms
*Info * Total Memory: 1mb
*Info * Free Memory: 1mb
*Info * Used Memory: 0mb
------------------------------------------------------
     18051ms 31/Mar/2009:11:15:34 +0200 200 GET /content/geometrixx/en/company.html text/ html
      2198ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/cq/widgets.js application/x-javascript
      1981ms 31/Mar/2009:11:15:11 +0200 200 GET /libs/wcm/content/welcome.html text/html
      1973ms 31/Mar/2009:11:15:52 +0200 200 GET /content/campaigns/geometrixx.teasers..html text/html
      1883ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/security/cq-security.js application/x-javascript
      1876ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/tagging/widgets.js application/x-javascript
      1869ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/tagging/widgets/themes/default.js application/x-javascript
      1729ms 30/Mar/2009:16:45:56 +0200 200 GET /libs/wcm/content/welcome.html text/html; charset=utf-8
      1510ms 31/Mar/2009:11:15:34 +0200 200 GET /bin/wcm/contentfinder/asset/view.json/ content/dam?_dc=1238490934657&query=&mimeType=image&_charset_=utf-8 application/json
      1462ms 30/Mar/2009:17:23:08 +0200 200 GET /libs/wcm/content/welcome.html text/html; charset=utf-8
```

큰 데이터 샘플에서 이 작업을 수행해야 하는 경우 개별 `request.log` 파일을 연결해야 할 수 있습니다.

### Apache Bench {#apache-bench}

특수 사례(예: 가비지 수집 등)의 영향을 최소화하려면 `apachebench` 등의 도구를 사용하는 것이 좋습니다(예: 추가 설명서는 [ab](https://httpd.apache.org/docs/2.2/programs/ab.html) 참조). 이를 통해 메모리 누수를 식별하고 응답 시간을 선택적으로 분석할 수 있습니다.

Apache Bench는 다음과 같은 방법으로 사용할 수 있습니다.

```shell
$ ab -c 5 -k -n 1000 "https://localhost:4503/content/geometrixx/en/company.html"
This is ApacheBench, Version 2.3 <$Revision: 655654 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, https://www.zeustech.net/
Licensed to The Apache Software Foundation, https://www.apache.org/

Benchmarking localhost (be patient)
Completed 100 requests
Completed 200 requests
Completed 300 requests
Completed 400 requests
Completed 500 requests
Completed 600 requests
Completed 700 requests
Completed 800 requests
Completed 900 requests
Completed 1000 requests
Finished 1000 requests

Server Software: Day-Servlet-Engine/4.1.52
Server Hostname: localhost
Server Port: 4503

Document Path: /content/geometrixx/en/company.html
Document Length: 24127 bytes

Concurrency Level: 5
Time taken for tests: 69.766 seconds
Complete requests: 1000
Failed requests: 998
(Connect: 0, Receive: 0, Length: 998, Exceptions: 0)
Write errors: 0
Keep-Alive requests: 0
Total transferred: 24160923 bytes
HTML transferred: 24010923 bytes
Requests per second: 14.33 /sec (mean)
Time per request: 348.828 [ms] (mean)
Time per request: 69.766 [ms] (mean, across all concurrent requests)
Transfer rate: 338.20 [Kbytes/sec] received

Connection Times (ms)
min mean[+/-sd] median max
Connect: 0 1 3.9 0 58
Processing: 138 347 568.5 282 8106
Waiting: 137 344 568.1 281 8106
Total: 139 348 568.4 283 8106

Percentage of the requests served within a certain time (ms)
50% 283
66% 323
75% 356
80% 374
90% 439
95% 512
98% 1047
99% 1132
100% 8106 (longest request)
```

위의 숫자는 기본 AEM 설치에 포함된 대로 geometrixx 회사 페이지에 액세스하는 표준 MAcBook Pro 노트북(2010년 중반)에서 가져옵니다. 페이지는 매우 간단하지만 성능에 최적화되지 않았습니다.

`apachebench` 또한 모든 동시 요청에 대해 요청당 시간을 평균으로 표시합니다.참조:  `Time per request: 54.595 [ms]` (모든 동시 요청에 대해) 동시성 매개 변수 `-c`(한 번에 수행할 여러 요청의 수)의 값을 변경하여 효과를 볼 수 있습니다.

### 요청 카운터 {#request-counters}

요청 트래픽(특정 기간 동안의 요청 수)에 대한 정보는 인스턴스의 로드를 나타냅니다. 이 정보는 [request.log](#interpreting-the-request-log)에서 추출할 수 있지만 카운터를 사용하면 데이터 수집을 자동화하여 다음을 볼 수 있습니다.

* 활동의 중요한 차이점(즉, &quot;많은 요청&quot;과 &quot;낮은 활동&quot;을 구별함)
* 인스턴스를 사용하지 않는 경우
* 다시 시작(카운터는 0으로 다시 설정됨)

정보 수집을 자동화하기 위해 RequestFilter를 설치하여 모든 요청에서 카운터를 증가시킬 수도 있습니다. 여러 카운터를 다양한 기간에 사용할 수 있습니다.

수집된 정보는 다음을 나타내기 위해 사용할 수 있습니다.

* 활동에 대한 중요한 변경 사항
* 중복 인스턴스
* 다시 시작(0으로 다시 설정된 카운터)

### HTML 댓글 {#html-comments}

서버 성능을 위해 모든 프로젝트에 `html comments`이 포함된 것이 좋습니다. 좋은 사례가 많다.페이지를 선택하고 볼 페이지 소스를 열고 아래쪽으로 스크롤하여 다음과 같은 코드를 표시할 수 있습니다.

```xml
</body>
 </html>
        <!--
        Page took 58 milliseconds to be rendered by server
         -->
```

### JConsole {#monitoring-performance-using-jconsole}을 사용하여 성능 모니터링

도구 명령 `jconsole`은 JDK에서 사용할 수 있습니다.

1. AEM 인스턴스를 시작합니다.
1. 실행 `jconsole.`
1. AEM 인스턴스와 **Connect**&#x200B;를 선택합니다.

1. `Local` 애플리케이션 내에서 `com.day.crx.quickstart.Main`;개요가 기본값으로 표시됩니다.

   ![chlimage_1-1](assets/chlimage_1-1.png)

   이 후 다른 옵션을 선택할 수 있습니다.

### (J)VisualVM {#monitoring-performance-using-j-visualvm}을 사용하여 성능 모니터링

JDK 1.6 이후 도구 명령 `jvisualvm`을 사용할 수 있습니다. JDK 1.6을 설치한 후 다음을 수행할 수 있습니다.

1. AEM 인스턴스를 시작합니다.

   >[!NOTE]
   >
   >Java 5를 사용하는 경우 JVM을 시작하는 java 명령줄에 `-Dcom.sun.management.jmxremote` 인수를 추가할 수 있습니다. JMX는 Java 6에서 기본적으로 활성화되어 있습니다.

1. 다음 중 하나를 실행합니다.

   * `jvisualvm`:JDK 1.6 bin 폴더(테스트된 버전)에서
   * `visualvm`:VisualVM에서  [다운로드](https://visualvm.dev.java.net/)  가능(출혈 에지 버전)

1. `Local` 애플리케이션 내에서 `com.day.crx.quickstart.Main`;개요가 기본값으로 표시됩니다.

   ![chlimage_1-2](assets/chlimage_1-2.png)

   그런 다음 모니터를 포함한 다른 옵션을 선택할 수 있습니다.

   ![chlimage_1-3](assets/chlimage_1-3.png)

이 도구를 사용하여 스레드 덤프 및 메모리 헤드 덤프를 생성할 수 있습니다. 기술 지원 팀에서 이러한 정보를 요청하는 경우가 많습니다.

### 정보 수집 {#information-collection}

설치에 대해 가능한 한 많이 알고 있으면 성능 변화를 일으킬 수 있는 대상과 이러한 변경 사항이 정당한지 여부를 추적하는 데 도움이 됩니다. 중요한 변경 사항을 쉽게 볼 수 있도록 이러한 지표를 정기적으로 수집해야 합니다.

다음 정보가 유용할 수 있습니다.

* [몇 명의 작성자가 이 시스템을 사용하고 있습니까?](#how-many-authors-are-working-with-the-system)
* [일별 평균 페이지 활성화 수는 얼마입니까?](#what-is-the-average-number-of-page-activations-per-day)
* [현재 이 시스템에서 몇 개의 페이지를 유지 관리하고 있습니까?](#how-many-pages-do-you-currently-maintain-on-this-system)
* [MSM을 사용하는 경우 월별 평균 롤아웃 수는 얼마입니까?](#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month)
* [월별 Live Copy의 평균 수는 얼마입니까?](#what-is-the-average-number-of-live-copies-per-month)
* [AEM Assets을 사용하는 경우 현재 Assets에서 몇 개의 자산을 유지 관리하고 있습니까?](#ifyouusecqdamhowmanyassetsdoyoucurrentlymaintainincqdam)
* [자산의 평균 크기는 얼마입니까?](#what-is-the-average-size-of-the-assets)
* [현재 사용되는 템플릿 수는 몇 개입니까?](#how-many-templates-are-currently-used)
* [현재 사용되는 구성 요소는 몇 개입니까?](#how-many-components-are-currently-used)
* [최고 시간에 작성 시스템에 몇 개의 요청이 있습니까?](#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time)
* [최대 시간에 게시 시스템에 몇 개의 요청이 있습니까?](#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time)

#### 몇 명의 작성자가 이 시스템을 사용하고 있습니까?{#how-many-authors-are-working-with-the-system}

설치 이후 시스템을 사용한 작성자의 수를 보려면 다음 명령줄을 사용하십시오.

```shell
cd <cq-installation-dir>/crx-quickstart/logs
cut -d " " -f 3 access.log | sort -u | wc -l
```

주어진 날짜에 작업하는 작성자 수를 보려면 다음을 수행하십시오.

```shell
grep "<date>" access.log | cut -d " " -f 3 | sort -u | wc -l
```

#### 일별 평균 페이지 활성화 수는 얼마입니까?{#what-is-the-average-number-of-page-activations-per-day}

서버 설치 이후 저장소 쿼리를 사용한 총 페이지 활성화 수를 보려면CRXDE를 통해 - 도구 - 쿼리:

* **유형** `XPath`

* **경로** `/`

* **쿼리** `//element(*, cq:AuditEvent)[@cq:type='Activate']`

그런 다음 설치 후 경과된 일 수를 계산하여 평균을 계산합니다.

#### 현재 이 시스템에서 몇 개의 페이지를 유지 관리하고 있습니까?{#how-many-pages-do-you-currently-maintain-on-this-system}

현재 서버에 있는 페이지 수를 보려면 저장소 쿼리를 사용합니다.CRXDE를 통해 - 도구 - 쿼리:

* **유형** `XPath`

* **경로** `/`

* **쿼리** `//element(*, cq:Page)`

#### MSM을 사용하는 경우 월별 평균 롤아웃 수는 얼마입니까?{#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month}

설치 후 저장소 쿼리를 사용한 총 롤아웃 수를 확인하려면CRXDE를 통해 - 도구 - 쿼리:

* **유형** `XPath`

* **경로** `/`

* **쿼리** `//element(*, cq:AuditEvent)[@cq:type='PageRolledOut']`

설치 후 경과된 개월 수를 계산하여 평균을 계산합니다.

#### 월별 Live Copy의 평균 수는 얼마입니까?{#what-is-the-average-number-of-live-copies-per-month}

설치 후 저장소 쿼리를 사용한 총 라이브 카피 수를 확인하려면CRXDE를 통해 - 도구 - 쿼리:

* **유형** `XPath`

* **경로** `/`

* **쿼리** `//element(*, cq:LiveSyncConfig)`

설치 후 경과된 개월 수를 다시 사용하여 평균을 계산합니다.

#### AEM Assets을 사용하는 경우 현재 Assets에서 몇 개의 자산을 유지 관리하고 있습니까?{#if-you-use-aem-assets-how-many-assets-do-you-currently-maintain-in-assets}

현재 유지 관리하는 DAM 자산 수를 보려면 저장소 쿼리를 사용합니다.CRXDE를 통해 - 도구 - 쿼리:

* **유형** `XPath`
* **경로** `/`
* **쿼리** `/jcr:root/content/dam//element(*, dam:Asset)`

#### 자산의 평균 크기는 얼마입니까?{#what-is-the-average-size-of-the-assets}

`/var/dam` 폴더의 총 크기를 확인하려면:

1. WebDAV를 사용하여 리포지토리를 로컬 파일 시스템에 매핑합니다.

1. 명령줄 사용:

   ```shell
   cd /Volumes/localhost/var
   du -sh dam/
   ```

   평균 크기를 얻으려면 `/var/dam`에 있는 자산의 총 수로 전역 크기를 나눕니다(위에서 획득).

#### 현재 사용되는 템플릿 수는 몇 개입니까?{#how-many-templates-are-currently-used}

현재 서버에 있는 템플릿 수를 보려면 저장소 쿼리를 사용합니다.CRXDE를 통해 - 도구 - 쿼리:

* **유형** `XPath`
* **경로** `/`
* **쿼리** `//element(*, cq:Template)`

#### 현재 사용되는 구성 요소는 몇 개입니까?{#how-many-components-are-currently-used}

서버에 현재 있는 구성 요소 수를 보려면 저장소 쿼리를 사용합니다.CRXDE를 통해 - 도구 - 쿼리:

* **유형** `XPath`
* **경로** `/`
* **쿼리** `//element(*, cq:Component)`

#### 최고 시간에 작성 시스템에 몇 개의 요청이 있습니까?{#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time}

최대 시간에 작성 시스템에 있는 시간당 요청을 확인하려면:

1. 설치 이후의 총 요청 수를 확인하려면 명령줄을 사용합니다.

   ```shell
   cd <cq-installation-dir>/crx-quickstart/logs
   grep -R "\->" request.log | wc -l
   ```

1. 시작 및 종료 날짜를 결정하려면

   ```shell
   vim request.log
   G / 1G: for the last/first lines
   ```

   이 값을 사용하여 설치 후 경과된 시간 수를 계산한 다음 시간당 평균 요청 수를 계산합니다.

#### 최대 시간에 게시 시스템에 몇 개의 요청이 있습니까?{#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time}

게시 인스턴스에서 위의 절차를 반복합니다.

## 특정 시나리오 분석 {#analyzing-specific-scenarios}

다음은 특정 성능 문제가 발생하는지 여부를 확인할 사항에 대한 제안 목록입니다. 이 목록은 (불행히도) 완전히 포괄적이지 않습니다.

>[!NOTE]
>
>자세한 내용은 다음 문서를 참조하십시오.
>
>* [스레드 덤프](https://helpx.adobe.com/experience-manager/kb/TakeThreadDump.html)
>* [메모리 문제 분석](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)
>* [내장 프로파일러를 사용하여 분석](https://helpx.adobe.com/experience-manager/kb/AnalyzeUsingBuiltInProfiler.html)
>* [느린 및 차단된 프로세스 분석](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)

>



### 100% {#cpu-at} CPU

시스템의 CPU가 100%에서 지속적으로 실행되고 있는 경우 다음을 참조하십시오.

* 기술 자료:

   * [느린 및 차단된 프로세스 분석](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)

### 메모리 부족 {#out-of-memory}

개발 및 테스트 중에 이러한 오류를 탐지해야 하지만 특정 시나리오가 미끄러질 수 있습니다.

시스템에 메모리가 부족한 경우 성능 저하 및 하위 텍스트를 포함하는 오류 메시지를 포함하여 다양한 방법으로 볼 수 있습니다.

`java.lang.OutOfMemoryError`

이 경우 다음을 확인합니다.

* [AEM](/help/sites-deploying/deploy.md#getting-started)을 시작하는 데 사용되는 JVM 설정
* 기술 자료:

   * [메모리 문제 분석](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)

### 디스크 I/O {#disk-i-o}

시스템에 디스크 공간이 부족하거나 디스크 스래싱이 시작하는 것을 발견하면 다음을 참조하십시오.

* 디버그 정보 수집을 비활성화했는지 여부다음과 같은 다양한 위치에서 구성할 수 있습니다.

   * [Apache Sling JSP 스크립트 핸들러](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjspscripthandler)
   * [Apache Sling Java Script 핸들러](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjavascripthandler)
   * [Apache Sling 로깅 구성](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)
   * [CQ HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md#daycqhtmllibrarymanager)
   * [CQ WCM 디버그 필터](/help/sites-deploying/osgi-configuration-settings.md#daycqwcmdebugfilter)
   * [로거](/help/sites-deploying/monitoring-and-maintaining.md#activating-the-debug-log-level) [](/help/sites-deploying/configuring.md#loggersandwritersforindividualservices)

* [버전 삭제](/help/sites-deploying/version-purging.md)를 구성했는지 여부 및 방법
* 기술 자료:

   * [열려 있는 파일이 너무 많습니다.](https://helpx.adobe.com/experience-manager/kb/TooManyOpenFiles.html)
   * [저널에 디스크 공간이 너무 많이 소모됨](https://helpx.adobe.com/experience-manager/kb/JournalTooMuchDiskSpace.html)

### 정규 성능 저하 {#regular-performance-degradation}

재부팅한 후(1주일 이상) 인스턴스 성능이 저하되는 경우 다음을 확인할 수 있습니다.

* [메모리 부족](#outofmemory)
* 기술 자료:

   * [닫히지 않은 세션](https://helpx.adobe.com/experience-manager/kb/AnalyzeUnclosedSessions.html)

### JVM 조정 {#jvm-tuning}

JVM(Java Virtual Machine)은 튜닝(특히 Java 7 이후)과 관련하여 크게 향상되었습니다. 따라서 적절한 고정 JVM 크기를 지정하고 기본값을 사용하는 것이 종종 적절합니다.

기본 설정이 적합하지 않으면 JVM을 튜닝하기 전에 GC 성능을 모니터링하고 평가하는 방법을 설정하는 것이 중요합니다.여기에는 heap 크기, 알고리즘 및 기타 측면과 같은 모니터링 요소가 포함될 수 있습니다.

몇 가지 일반적인 선택 사항은 다음과 같습니다.

* VerboseGC:

   ```
   -verbose:gc \
    -Xloggc:$LOGS/verbosegc.log \
    -XX:+PrintGCDetails \
    -XX:+PrintGCDateStamps
   ```

다음과 같은 GC 시각화 도우미에서 결과 로그를 수집할 수 있습니다.

` [https://www.ibm.com/developerworks/library/j-ibmtools2/](https://www.ibm.com/developerworks/library/j-ibmtools2/)`

또는 JConsole:

* 이러한 설정은 &quot;광범위하게 열린&quot; JMX 연결을 위한 설정입니다.

   ```
   -Dcom.sun.management.jmxremote \
    -Dcom.sun.management.jmxremote.port=8889 \
    -Dcom.sun.management.jmxremote.authenticate=false \
    -Dcom.sun.management.jmxremote.ssl=false
   ```

* 그런 다음 JConsole을 사용하여 JVM에 연결합니다.다음을 참조하십시오.
   ` [https://docs.oracle.com/javase/6/docs/technotes/guides/management/jconsole.html](https://docs.oracle.com/javase/6/docs/technotes/guides/management/jconsole.html)`

이렇게 하면 사용 중인 메모리 양, 사용 중인 GC 알고리즘, 실행 시간 및 애플리케이션 성능에 어떤 영향을 주는지 확인할 수 있습니다. 이렇게 하지 않으면 튜닝은 &quot;임의로 사용하는 매듭들&quot;일 뿐입니다.

>[!NOTE]
>
>oracle의 VM에 대한 정보는 다음과 같습니다.
>
>[https://docs.oracle.com/javase/7/docs/technotes/guides/vm/server-class.html](https://docs.oracle.com/javase/7/docs/technotes/guides/vm/server-class.html)
