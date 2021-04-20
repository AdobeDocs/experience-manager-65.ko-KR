---
title: AEM 인스턴스 모니터링 및 유지 관리
seo-title: AEM 인스턴스 모니터링 및 유지 관리
description: AEM을 모니터링하는 방법을 학습합니다.
seo-description: AEM을 모니터링하는 방법을 학습합니다.
uuid: 14466552-5c92-4730-a427-85675a2b121c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5d2364b7-4497-4f8b-85ef-6e780bfb8c36
docset: aem65
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '5892'
ht-degree: 1%

---


# AEM 인스턴스 모니터링 및 유지 관리{#monitoring-and-maintaining-your-aem-instance}

AEM 인스턴스가 배포된 후 작업, 성능 및 무결성을 모니터링하고 유지 관리하는 데 특정 작업이 필요합니다.

여기서 중요한 요소는 잠재적인 문제를 인식하기 위해 시스템이 정상적인 조건에서 어떻게 보이고 동작하는지 알아야 합니다. 이것은 시스템을 모니터링하고 일정 기간 동안 정보를 수집하는 것이 가장 좋습니다.

| 확인 | 고려 사항 | 주석/작업 |
|---|---|---|
| 백업 플랜. |  | [인스턴스 백업 방법](/help/sites-deploying/monitoring-and-maintaining.md#backups)을 참조하십시오. |
| 재해 복구 계획 | 귀사의 재해 복구 가이드라인 |  |
| 오류 추적 시스템을 사용하여 문제를 보고할 수 있습니다. | 예: [bugzilla](https://www.bugzilla.org/), [jira](https://www.atlassian.com/software/jira/) 또는 기타 여러 항목 중 하나. |  |
| 파일 시스템을 모니터링하고 있습니다. | 사용 가능한 디스크 공간이 부족한 경우 CRX 저장소가 &quot;고정&quot;됩니다. 공간이 확보되면 다시 시작됩니다. | 사용 가능한 공간이 부족할 때 로그 파일에서 `*ERROR* LowDiskSpaceBlocker`&quot; 메시지를 볼 수 있습니다. |
| [로그 ](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) 파일을 모니터링하고 있습니다. |  |  |
| 시스템 모니터링은 백그라운드에서 계속 실행됩니다. | CPU, 메모리, 디스크 및 네트워크 사용을 포함합니다. 예를 들어 iostat / vmstat / perfmon을 사용합니다. | 기록된 데이터는 시각화되며 성능 문제를 추적하는 데 사용할 수 있습니다. 원시 데이터도 액세스할 수 있습니다. |
| [AEM 성능을 모니터링하고 있습니다](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance). | [요청 카운터](/help/sites-deploying/monitoring-and-maintaining.md#request-counters)를 포함하여 트래픽 수준을 모니터링합니다. | 현저한 실연이나 장기 실적이 확인되면 상세한 조사가 이루어져야 한다. |
| [복제 에이전트](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-your-replication-agents)를 모니터링하고 있습니다. |  |  |
| 워크플로우 인스턴스를 정기적으로 제거합니다. | 저장소 크기 및 워크플로우 성능 | 자세한 내용은 [워크플로우 인스턴스 정기적인 제거](/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances)를 참조하십시오. |

## 백업 {#backups}

다음을 수행하는 것이 좋습니다.

* 소프트웨어 설치 - 구성의 중요한 변경 전/후
* 저장소 내에 있는 컨텐츠 - 정기적으로

다음과 같은 백업 정책을 통해 백업해야 할 내용과 백업 시기를 추가로 고려해야 합니다.

* 시스템 및 데이터가 얼마나 중요한지
* 소프트웨어 또는 데이터를 변경하는 빈도
* 데이터의 양;백업을 수행하는 데 필요한 시간과 마찬가지로 용량에 문제가 있을 수 있습니다.
* 사용자가 온라인 상태에서 백업을 수행할 수 있는지 여부;그리고 가능하면 성능에 어떤 영향을 미칩니까?
* 사용자의 지리적 분포(영향을 최소화하려면 언제 백업해야 합니까?)
* 재해 복구 정책백업 데이터를 저장해야 하는 위치(예: 오프사이트, 특정 미디어 등)에 대한 지침이 있습니다.

종종 전체 백업이 정기적인 간격(예: 일별, 주별 또는 월별)으로 수행되고 증분 백업(예: 시간별, 일별 또는 주별) 사이에 수행됩니다.

>[!CAUTION]
>
>운영 인스턴스의 백업을 구현할 때 백업을 성공적으로 복원할 수 있도록 *테스트*&#x200B;를 수행해야 합니다.
>
>이렇게 하지 않으면 백업이 잠재적으로 무용지물이 됩니다(최악의 경우 시나리오).

>[!NOTE]
>
>백업 성능에 대한 자세한 내용은 [백업 성능](/help/sites-deploying/configuring-performance.md#backup-performance) 섹션을 참조하십시오.

### 소프트웨어 설치 백업 {#backing-up-your-software-installation}

설치 후 또는 구성의 중대한 변경 사항이 발생하면 소프트웨어 설치를 백업합니다.

이렇게 하려면 [전체 저장소를 백업한 후:](#backing-up-your-repository)

1. AEM을 중지합니다.
1. 파일 시스템에서 전체 `<cq-installation-dir>`를 백업합니다.

>[!CAUTION]
>
>타사 응용 프로그램 서버를 작동 중인 경우 다른 위치에 추가 폴더가 있을 수 있으며 백업해야 할 수도 있습니다. 응용 프로그램 서버 설치에 대한 자세한 내용은 [Application Server와 AEM 설치 방법](/help/sites-deploying/application-server-install.md)을 참조하십시오. [](/content/docs/en/aem/6-3/deploy/installing.md#installing adobe experience manager with application server)

>[!CAUTION]
>
>파일 데이터 저장소의 증분 백업이 지원됩니다.다른 구성 요소(예: Lucene 인덱스)에 대해 증분 백업을 사용하는 경우 삭제된 파일도 백업에서 삭제된 것으로 표시되는지 확인하십시오.

>[!NOTE]
>
>디스크 미러링도 백업 메커니즘으로 사용할 수 있습니다.

### 저장소 백업 {#backing-up-your-repository}

CRX 설명서의 [백업 및 복원](/help/sites-administering/backup-and-restore.md) 섹션에서는 CRX 저장소의 백업과 관련된 모든 문제를 다룹니다.

온라인 &quot;핫&quot; 백업을 만드는 방법에 대한 자세한 내용은 [온라인 백업 만들기](/help/sites-administering/backup-and-restore.md#online-backup)를 참조하십시오.

## 버전 제거 {#version-purging}

**삭제 버전** 도구는 저장소의 노드 버전이나 노드 계층 구조를 제거하기 위한 것입니다. 기본 목적은 노드의 이전 버전을 제거하여 저장소 크기를 줄이는 데 도움이 됩니다.

이 섹션에서는 AEM의 버전 관리 기능과 관련된 유지 관리 작업을 다룹니다. **삭제 버전** 도구는 저장소의 노드 버전이나 노드 계층 구조를 제거하기 위한 것입니다. 기본 목적은 노드의 이전 버전을 제거하여 저장소 크기를 줄이는 데 도움이 됩니다.

### 개요 {#overview}

**버전 삭제** 도구는 **버전 관리** 아래의 **[도구](/help/sites-administering/tools-consoles.md) 콘솔**&#x200B;에서 사용할 수 있으며 다음 위치에서 직접 사용할 수 있습니다.

`https://<server>:<port>/etc/versioning/purge.html`

![screen_shot_2012-03-15at14418pm](assets/screen_shot_2012-03-15at14418pm.png)

**시작** 경로삭제를 수행해야 하는 절대 경로입니다. 저장소 트리 탐색기를 클릭하여 시작 경로를 선택할 수 있습니다.

**재귀데이터** 를 제거할 때 재귀적을 선택하여 한 노드에서 작업을 수행하거나 전체 계층 구조에서 작업을 수행할 수 있습니다. 마지막 경우 지정된 경로는 계층의 루트 노드를 정의합니다.

**유지할 최대** 버전노드에 유지할 최대 버전 수입니다. 이러한 수가 이 값을 초과하면 가장 오래된 버전이 삭제됩니다.

**최대 버전** 페이지노드 버전의 최대 페이지입니다. 버전 사용 기간이 이 값을 초과하면 삭제됩니다.

**연습** 실행컨텐츠 버전을 제거하는 것이 확실하고 백업을 복원하지 않으면 되돌릴 수 없기 때문에 제거 버전 도구는 삭제된 버전을 미리 볼 수 있는 연습 실행 모드를 제공합니다. 제거 프로세스의 연습 실행을 실행하려면 연습 실행을 클릭합니다.

**** 제거시작 경로에 의해 정의된 노드에서 버전 제거를 시작합니다.

### 웹 사이트 버전 {#purging-versions-of-a-web-site} 제거

웹 사이트의 버전을 제거하려면 다음과 같이 하십시오.

1. **[도구](/help/sites-administering/tools-consoles.md)** **콘솔**&#x200B;로 이동하고 **버전 관리**&#x200B;을 선택하고 **버전 삭제**
1. 삭제할 컨텐츠의 시작 경로를 설정합니다(예:`/content/geometrixx-outdoors`).

   * 경로에 정의된 노드만 제거하려면 **재귀**&#x200B;를 선택 취소합니다.
   * 경로에 정의된 노드를 제거하고 해당 하위 멤버는 **재귀**&#x200B;를 선택합니다.

1. 유지할 최대 버전 수(각 노드에 대해)를 설정합니다. 이 설정을 사용하지 않으려면 비워 두십시오.

1. 유지할 일 수(각 노드에 대해)의 최대 버전 기간을 설정합니다. 이 설정을 사용하지 않으려면 비워 두십시오.

1. **연습 실행**&#x200B;을 클릭하여 제거 프로세스의 작업을 미리 봅니다.
1. **삭제**&#x200B;를 클릭하여 프로세스를 시작합니다.

>[!CAUTION]
>
>저장소를 복원하지 않으면 삭제된 노드를 되돌릴 수 없습니다. 구성을 관리해야 하므로 제거하기 전에 항상 연습 실행을 수행하는 것이 좋습니다.

### 콘솔 {#analyzing-the-console} 분석

**Dry Run** 및 **Purge** 프로세스는 처리된 모든 노드를 나열합니다. 이 프로세스 중에 노드는 다음 상태 중 하나를 가질 수 있습니다.

* `ignore (not versionnable)`:노드는 버전 지정을 지원하지 않으며 프로세스 중에 무시됩니다.

* `ignore (no version)`:노드에 버전이 없으며 프로세스 중에 무시됩니다.

* `retained`:노드가 삭제되지 않았습니다.
* `purged`:노드가 삭제됩니다.

또한 콘솔에 다음과 같은 버전에 대한 유용한 정보가 제공됩니다.

* `V 1.0`:버전 번호입니다.
* `V 1.0.1`*:별은 버전이 현재 버전임을 나타냅니다.

* `Thu Mar 15 2012 08:37:32 GMT+0100`:버전 날짜입니다.

다음 예에서:

* 버전 사용 기간이 2일 이상이므로 **[!DNL Shirts]** 버전이 삭제됩니다.
* 버전 수가 5보다 커서 **[!DNL Tonga Fashions!]** 버전이 삭제됩니다.

![global_version_스크린샷](assets/global_version_screenshot.png)

## 감사 레코드 및 로그 파일 작업 {#working-with-audit-records-and-log-files}

AEM(Adobe Experience Manager)과 관련된 기록 및 로그 파일은 다양한 위치에서 찾을 수 있습니다. 찾을 수 있는 항목의 개요를 알 수 있도록 다음 정보가 제공됩니다.

### 로그 작업 {#working-with-logs}

AEM WCM은 자세한 로그를 기록합니다. 압축을 풀고 Quickstart를 시작한 후 다음 위치에서 로그를 찾을 수 있습니다.

* `<cq-installation-dir>/crx-quickstart/logs/`

* `<cq-installation-dir>/crx-quickstart/repository/`

#### 로그 파일 순환 {#log-file-rotation}

로그 파일 회전은 새 파일을 주기적으로 만들어 파일 증가를 제한하는 프로세스를 말합니다. AEM에서 `error.log`이라는 로그 파일은 지정된 규칙에 따라 하루에 한 번 회전합니다.

* `error.log` 파일은 {original_filename} `.yyyy-MM-dd` 패턴에 따라 이름이 바뀝니다. 예를 들어 2010년 7월 11일에 현재 로그 파일의 이름이 `error.log-2010-07-10`으로 변경된 후 새 `error.og`이(가) 만들어집니다.

* 이전 로그 파일은 삭제되지 않으므로 디스크 사용을 제한하기 위해 정기적으로 이전 로그 파일을 정리하는 것은 사용자의 책임입니다.

>[!NOTE]
>
>AEM 설치를 업그레이드하는 경우 AEM에서 더 이상 사용하지 않는 기존 로그 파일은 디스크에 남아 있습니다. 위험 없이 제거할 수 있습니다. 모든 새 로그 항목이 새 로그 파일에 기록됩니다.

### 로그 파일 찾기 {#finding-the-log-files}

AEM을 설치한 파일 서버에 다양한 로그 파일이 보관됩니다.

* `<cq-installation-dir>/crx-quickstart/logs`

   * `access.log`
AEM WCM 및 저장소에 대한 모든 액세스 요청은 여기에 등록됩니다.

   * `audit.log`
중재 작업은 여기에서 등록됩니다.

   * `error.log`
여기에는 다양한 수준의 오류 메시지(심각도)가 등록되어 있습니다.

   * [ `ImageServer-<PortId>-yyyy>-<mm>-<dd>.log`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/config-admin/server-logging/c-image-server-log.html)
이 로그는 활성화된 경우에만  [!DNL Dynamic Media] 사용됩니다. 내부 ImageServer 프로세스의 동작을 분석하는 데 사용되는 통계 및 분석 정보를 제공합니다.

   * `request.log`
각 액세스 요청은 응답과 함께 여기에 등록됩니다.

   * [ `s7access-<yyyy>-<mm>-<dd>.log`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/config-admin/server-logging/c-access-log.html)
이 로그는 활성화된 경우에만  [!DNL Dynamic Media] 사용됩니다. s7access 로그는 [!DNL Dynamic Media] 및 `/is/content`에서 `/is/image`에 대한 각 요청을 기록합니다.

   * `stderr.log`
시작하는 동안 생성된 다양한 수준의 심각도에 대한 오류 메시지를 다시 표시합니다. 기본적으로 로그 수준은 
`Warning` ( `WARN`)

   * `stdout.log`
시작 중에 이벤트를 나타내는 로깅 메시지를 보류합니다.

   * `upgrade.log`
JavaScript 파일 내의 
`com.day.compat.codeupgrade` 및 패키지 `com.adobe.cq.upgradesexecutor` 를 선택합니다.

* `<cq-installation-dir>/crx-quickstart/repository`

   * `revision.log`
저널링 정보 개정

>[!NOTE]
>
>ImageServer 및 s7access 로그는 **system/console/status-Bundelist **페이지에서 생성되는 **Download Full **패키지에 포함되지 않습니다. 지원 목적으로 [!DNL Dynamic Media] 문제가 있는 경우 고객 지원에 문의할 때 ImageServer 및 s7access 로그도 추가하십시오.

### 디버그 로그 수준 {#activating-the-debug-log-level} 활성화

기본 로그 수준([Apache Sling 로깅 구성](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration))은 정보이므로 디버그 메시지가 기록되지 않습니다.

로거에 대한 디버그 로그 수준을 활성화하려면 저장소에서 디버깅할 속성 `org.apache.sling.commons.log.level`을 설정합니다. 예를 들어 `/libs/sling/config/org.apache.sling.commons.log.LogManager`에서 [전역 Apache Sling 로깅](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)을 구성합니다.

>[!CAUTION]
>
>로그 항목이 많이 생성되므로 로그 수준을 필요한 것보다 오래 두면 리소스가 소모됩니다.

디버그 파일의 한 줄은 일반적으로 DEBUG로 시작하고 로그 수준, 설치 프로그램 작업 및 로그 메시지를 제공합니다. 예:

```shell
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

로그 수준은 다음과 같습니다.

| 0 | 치명적인 오류 | 작업이 실패하여 설치 프로그램을 계속할 수 없습니다. |
|---|---|---|
| 1 | 오류 | 작업이 실패했습니다. 설치가 진행되지만 AEM WCM의 일부가 제대로 설치되지 않아 제대로 작동하지 않습니다. |
| 2 | 경고 | 작업에 성공했지만 문제가 발생했습니다. AEM WCM이 제대로 작동하지 않거나 않을 수 있습니다. |
| 3 | 정보 | 작업이 성공했습니다. |

### 사용자 지정 로그 파일 {#create-a-custom-log-file} 만들기

>[!NOTE]
>
>Adobe Experience Manager을 사용하여 작업할 때 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 여러 가지가 있습니다.자세한 내용 및 권장 방법은 [OSGi](/help/sites-deploying/configuring-osgi.md) 구성을 참조하십시오.

특정 상황에서는 로그 수준이 다른 사용자 정의 로그 파일을 만들 수 있습니다. 다음과 같은 방법으로 저장소에서 이 작업을 수행할 수 있습니다.

1. 아직 존재하지 않는 경우 프로젝트 `/apps/<project-name>/config`에 대한 새 구성 폴더( `sling:Folder`)를 만듭니다.
1. `/apps/<project-name>/config` 아래에서 새 [Apache Sling 로깅 로거 구성](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingloggerconfigurationfactoryconfiguration)에 대한 노드를 만듭니다.

   * 이름:`org.apache.sling.commons.log.LogManager.factory.config-<identifier>`(로거이므로)

      여기서 `<identifier>`은(는) 인스턴스를 식별하기 위해 입력한 자유 텍스트로 대체됩니다(이 정보를 생략할 수 없음).

      예, `org.apache.sling.commons.log.LogManager.factory.config-MINE`

   * 유형: `sling:OsgiConfig`
   >[!NOTE]
   >
   >기술적인 요구 사항은 아니지만 `<identifier>`을(를) 고유하게 만드는 것이 좋습니다.

1. 이 노드에서 다음 속성을 설정합니다.

   * 이름: `org.apache.sling.commons.log.file`

      유형:문자열

      값:로그 파일 지정;예를 들어 `logs/myLogFile.log`

   * 이름: `org.apache.sling.commons.log.names`

      유형:문자열[](문자열 + 다중)

      값:로거가 메시지를 기록할 OSGi 서비스를 지정합니다.예를 들어, 다음 모두

      * `org.apache.sling`
      * `org.apache.felix`
      * `com.day`
   * 이름: `org.apache.sling.commons.log.level`

      유형:문자열

      값:필요한 로그 수준 지정( `debug`, `info`, `warn` 또는 `error`);예를 들면 `debug`

   * 필요에 따라 다른 매개 변수를 구성합니다.

      * 이름: `org.apache.sling.commons.log.pattern`

         유형: `String`

         값:필요에 따라 로그 메시지의 패턴을 지정합니다.예를 들어

         `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`
   >[!NOTE]
   >
   >`org.apache.sling.commons.log.pattern` 최대 6개의 인수를 지원합니다.
   >
   >{0} `java.util.Date` 유형의 타임스탬프
   >
   >{1} 로그 마커
   >
   >{2} 현재 스레드의 이름
   >
   >{3} 로거 이름
   >
   >{4} 로그 수준
   >
   >로그 메시지 {5}
   >
   >로그 호출에 `Throwable`이(가) 포함된 경우 스택이 메시지에 추가됩니다.

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
   >쓰기 대상:
   >
   >`<cq-installation-dir>/crx-quickstart/logs/thelog.log`.
   >
   >및 다음과 같이 지정된 로그 파일:
   >
   >`../logs/thelog.log`
   >
   >디렉토리에 쓰기:
   >
   >`<cq-installation-dir>/logs/`\
   >(예: `<cq-installation-dir>/crx-quickstart/` 옆)

1. 이 단계는 새 작성기가 필요한 경우에만 필요합니다(예: 기본 작성기와 다른 구성).

   >[!CAUTION]
   >
   >새 로깅 작성자 구성은 기존 기본값이 적합하지 않을 때만 필요합니다.
   >
   >명시적 작성기가 구성되지 않은 경우 시스템은 기본값을 기반으로 암시적 작성기를 자동으로 생성합니다.

   `/apps/<project-name>/config` 아래에서 새 [Apache Sling 로깅 작성자 구성](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingwriterconfigurationfactoryconfiguration)에 대한 노드를 만듭니다.

   * 이름:`org.apache.sling.commons.log.LogManager.factory.writer-<identifier>` (작성기이므로)

      로거와 마찬가지로 `<identifier>`은(는) 인스턴스를 식별하기 위해 입력한 자유 텍스트로 대체됩니다(이 정보를 생략할 수 없음). 예, `org.apache.sling.commons.log.LogManager.factory.writer-MINE`

   * 유형: `sling:OsgiConfig`
   >[!NOTE]
   >
   >기술적인 요구 사항은 아니지만 `<identifier>`을(를) 고유하게 만드는 것이 좋습니다.

   이 노드에서 다음 속성을 설정합니다.

   * 이름: `org.apache.sling.commons.log.file`

      유형: `String`

      값:로거에 지정된 파일과 일치하도록 로그 파일을 지정합니다.

      이 예제의 경우 `../logs/myLogFile.log`.

   * 필요에 따라 다른 매개 변수를 구성합니다.

      * 이름: `org.apache.sling.commons.log.file.number`

         유형: `Long`

         값:보관할 로그 파일의 수를 지정합니다.예를 들어 `5`

      * 이름: `org.apache.sling.commons.log.file.size`

         유형: `String`

         값:파일 회전을 크기/날짜별로 제어하려면 필요에 따라 지정합니다.예를 들어 `'.'yyyy-MM-dd`
   >[!NOTE]
   >
   >`org.apache.sling.commons.log.file.size` 다음 중 하나를 설정하여 로그 파일의 회전을 제어합니다.
   >
   >* 최대 파일 크기
   >* 시간/날짜 일정

   >
   >를 클릭하여 새 파일을 언제 만들 것인지 지정합니다(그리고 이름 패턴에 따라 이름이 변경된 기존 파일).
   >
   >* 크기 제한은 숫자로 지정할 수 있습니다. 크기 표시기가 지정되지 않으면 바이트 수로 표시되거나 크기 표시기( `KB`, `MB` 또는 `GB`) 중 하나를 추가할 수 있습니다(대/소문자 무시).
   >* 시간/날짜 일정은 `java.util.SimpleDateFormat` 패턴으로 지정할 수 있습니다. 파일을 회전할 기간을 정의합니다.또한 회전된 파일(식별을 위해)에 접미사를 추가합니다.

   >
   >기본값은 &#39;.&#39;입니다.yyyy-MM-dd(일별 로그 회전의 경우).
   >
   >예를 들어, 2010년 1월 20일 자정(또는 이 시간 후 첫 번째 로그 메시지가 정확해지는 경우) ../logs/error.log은 ../logs/error.log.2010-01-20으로 이름이 변경됩니다. 1월 21일에 로깅은 다음 변경 시간에 롤오버될 때까지 ../logs/error.log으로 출력됩니다(새 및 비어 있음).
   >
   >| `'.'yyyy-MM` | 매월 초에 회전 |
   >|---|---|
   >| `'.'yyyy-ww` | 각 주의 첫째 날에 순환합니다(로케일에 따라 다름). |
   >| `'.'yyyy-MM-dd` | 매일 자정에 회전합니다. |
   >| `'.'yyyy-MM-dd-a` | 매일 자정과 정오에 회전합니다. |
   >| `'.'yyyy-MM-dd-HH` | 매 시간 맨 위에서 회전합니다. |
   >| `'.'yyyy-MM-dd-HH-mm` | 매분 초에 회전합니다. |
   >
   >참고:시간/날짜를 지정할 때:
   > 1. 단일 따옴표(&#39; &#39;); 쌍 내에서 리터럴 텍스트를 &quot;escape&quot;해야 합니다.
      >
      >     
      이는 특정 문자가 패턴 문자로 해석되지 않도록 하기 위한 것입니다.
      >
      >  
   1. 옵션의 아무 위치에서나 유효한 파일 이름에 허용되는 문자만 사용하십시오.


1. 선택한 도구를 사용하여 새 로그 파일을 읽습니다.

   이 예제에서 만든 로그 파일은 `../crx-quickstart/logs/myLogFile.log`입니다.

Felix Console은 `../system/console/slinglog`에서 Sling 로그 지원에 대한 정보도 제공합니다.예: `https://localhost:4502/system/console/slinglog`.

### 감사 레코드 찾기 {#finding-the-audit-records}

누가 언제 무엇을 했는지 기록하기 위해 감사 기록을 보유한다. AEM WCM 및 OSGi 이벤트 모두에 대해 다른 감사 레코드가 생성됩니다.

#### AEM WCM 페이지 작성 {#aem-wcm-audit-records-shown-when-page-authoring} 시 표시된 감사 레코드

1. 페이지를 엽니다.
1. 사이드 킥에서 잠금 아이콘이 있는 탭을 선택한 다음 **감사 로그...를 두 번 클릭합니다.**
1. 현재 페이지에 대한 감사 레코드 목록을 보여주는 새 창이 열립니다.

   ![screen_shot_2012-02-02at43601pm](assets/screen_shot_2012-02-02at43601pm.png)

1. 창을 닫으려면 **확인**&#x200B;을 클릭합니다.

#### AEM WCM 감사 기록 저장소 {#aem-wcm-auditing-records-within-the-repository}

`/var/audit` 폴더 내에 리소스에 따라 감사 레코드가 보관됩니다. 개별 레코드 및 포함된 정보를 볼 수 있을 때까지 드릴다운할 수 있습니다.

이러한 항목은 페이지를 편집할 때 표시되는 정보와 같습니다.

#### 웹 콘솔 {#osgi-audit-records-from-the-web-console}의 OSGi 감사 레코드

또한 OSGi 이벤트는 AEM 웹 콘솔의 **구성 상태** 탭 -> **로그 파일** 탭에서 볼 수 있는 감사 기록을 생성합니다.

![screen_shot_2012-02-13at50346pm](assets/screen_shot_2012-02-13at50346pm.png)

## 복제 에이전트 모니터링 {#monitoring-your-replication-agents}

[복제 큐](/help/sites-deploying/replication.md)를 모니터링하여 대기열이 다운되거나 차단되는 시간을 감지할 수 있습니다. 이러한 경우 게시 인스턴스 또는 외부 시스템에 문제가 있을 수 있습니다.

* 모든 필수 큐를 사용할 수 있습니까?
* 비활성화된 큐는 계속 필요합니까?
* 모든 `enabled` 큐에는 정상 작업을 나타내는 `idle` 또는 `active` 상태가 있어야 합니다.대기열은 수신자의 문제 징표인 `blocked`이어야 합니다.

* 시간 경과에 따라 큐의 크기가 증가하면 차단된 큐를 나타낼 수 있습니다.

복제 에이전트를 모니터링하려면:

1. AEM의 **도구** 탭에 액세스합니다.
1. **복제**&#x200B;를 클릭합니다.
1. 적절한 환경(왼쪽 또는 오른쪽 창)에 대한 에이전트 링크를 두 번 클릭합니다.예: **작성자**&#x200B;의 에이전트.

   결과 창에는 대상 및 상태를 포함하여 작성 환경에 대한 모든 복제 에이전트에 대한 개요가 표시됩니다.

1. 해당 에이전트 이름(링크임)을 클릭하여 해당 에이전트에 대한 자세한 정보를 표시합니다.

   ![chlimage_1](assets/chlimage_1.jpeg)

   여기에서 다음을 수행할 수 있습니다.

   * 에이전트가 활성화되어 있는지 확인합니다.
   * 복제 타겟을 확인합니다.
   * 복제 큐가 현재 활성 상태인지(활성화되었는지 여부)를 확인합니다.
   * 대기열에 항목이 있는지 확인합니다.
   * **대기열 항목** 표시를  **** 업데이트하려면 새로 고침 또는 Clearer;이렇게 하면 항목이 큐에 들어가 대기하지 않는 것을 볼 수 있습니다.

   * **복제 에이전트** 의 작업 로그에 액세스하려면 로그를 보십시오.
   * **대상** 인스턴스에 대한 연결 테스트를 참조하십시오.
   * **필요한** 경우 모든 큐 항목을 다시 테스트하십시오.

   >[!CAUTION]
   >
   >게시 인스턴스의 역방향 복제 출력 상자에 대해 &quot;연결 테스트&quot; 링크를 사용하지 마십시오.
   >
   >Outbox 큐에 대한 복제 테스트가 수행되는 경우 테스트 복제보다 오래된 항목은 모든 역방향 복제를 사용하여 다시 처리됩니다.
   >
   >이러한 항목이 이미 큐에 있는 경우 다음 XPath JCR 쿼리로 해당 항목을 찾을 수 있으며 제거해야 합니다.
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

다시 한 번 모든 복제 에이전트(`/etc/replication/author` 또는 `/etc/replication/publish` 아래에 있음)를 감지하는 솔루션을 개발한 다음 에이전트( `enabled`, `disabled`)와 기본 대기열( `active`, `idle`, `blocked`)의 상태를 확인할 수 있습니다.

## 모니터링 성능 {#monitoring-performance}

[성능 최적화](/help/sites-deploying/configuring-performance.md) 는 개발 중에 포커스를 받는 대화형 프로세스입니다. 배포 후에는 일반적으로 특정 간격이나 이벤트 후에 검토합니다.

최적화를 위한 정보를 수집하는 동안 사용되는 메서드를 지속적인 모니터링에 사용할 수도 있습니다.

>[!NOTE]
>
>성능](/help/sites-deploying/configuring-performance.md#configuring-for-performance)을 개선하는 데 사용할 수 있는 특정 [구성도 확인할 수 있습니다.

다음은 일반적인 성과 문제를 찾아 대응하는 방법에 대한 제안과 함께 나열하는 것입니다.

| 영역 | 증상 | 용량을 늘리기 위해... | 볼륨을 줄이는 방법... |
|---|---|---|---|
| 클라이언트 | 높은 클라이언트 CPU 사용. | 더 높은 성능을 가진 클라이언트 CPU를 설치합니다. | 레이아웃 간소화(HTML) |
|  | 서버 CPU 사용량이 낮습니다. | 더욱 빨라진 브라우저로 업그레이드 | 클라이언트측 캐시를 개선합니다. |
|  | 몇몇 고객들은 빠르고 느리기도 합니다. |  |  |
| 서버 |  |  |  |
| 네트워크 | 서버와 클라이언트 모두에서 CPU 사용량이 낮습니다. | 네트워크 병목 현상을 제거합니다. | 클라이언트 캐시 구성을 향상/최적화합니다. |
|  | 서버에서의 로컬 검색이(비교적) 빠르다. | 네트워크 대역폭 증가 | 웹 페이지의 &quot;무게&quot;(예: 이미지 감소, 최적화된 HTML) 감소 |
| 웹 서버 | 웹 서버의 CPU 사용량이 높습니다. | 웹 서버를 클러스터링합니다. | 페이지당 히트 수 감소(방문). |
|  |  | 하드웨어 부하 균형 조정기를 사용합니다. |  |
| 애플리케이션 | 서버 CPU 사용량이 높습니다. | AEM 인스턴스를 클러스터링합니다. | CPU 및 메모리 돼지를 검색하고 제거합니다(코드 검토, 시간 출력 등). |
|  | 메모리 사용량이 많습니다. |  | 모든 레벨의 캐싱 향상 |
|  | 낮은 응답 시간 |  | 템플릿 및 구성 요소(예: 구조, 논리) 최적화 |
| 저장소 |  |  |  |
| 캐시 |  |  |  |

성능 문제는 연결 속도 저하, CPU 로드 등 웹 사이트와 아무런 관련이 없는 여러 가지 원인에서 발생할 수 있습니다.

또한 모든 방문자 또는 일부 방문자에게 영향을 줄 수 있습니다.

일반 성능을 최적화하거나 특정 문제를 해결하려면 먼저 이 모든 정보를 확인하고 정렬하고 분석해야 합니다.

* 성능 문제가 발생하기 전:

   * 정상적 상황에서 시스템에 대한 좋은 지식을 쌓기 위해 가능한 한 많은 정보를 수집하다

* 성능 문제가 발생하는 경우:

   * 일반적인 성능이 우수한 다른 클라이언트 및/또는 서버 자체(가능한 경우)에서 표준 웹 브라우저 하나(또는 더 이상 필요)와 동일하게 구현해 보십시오.
   * 적절한 시간 공간 내에서 변경된 내용이 있는지, 그리고 이러한 변경 사항이 성능에 영향을 줄 수 있는지 확인합니다.
   * 다음과 같은 질문을 합니다.

      * 문제는 특정 시에만 발생합니까?
      * 문제는 특정 페이지에서만 발생합니까?
      * 다른 요청이 영향을 받습니까?
   * 정상적인 상황에서 시스템에 대한 귀하의 지식에 비교할 수 있도록 가능한 많은 정보를 수집하십시오.


### 성능 모니터링 및 분석 도구 {#tools-for-monitoring-and-analyzing-performance}

다음은 성능을 모니터링하고 분석하는 데 사용할 수 있는 일부 도구에 대한 간단한 개요를 제공합니다.

이 중 일부는 운영 체제에 따라 다릅니다.

<table>
 <tbody>
  <tr>
   <td>도구</td>
   <td>분석하는 데 사용됨..</td>
   <td>사용/추가 정보...</td>
  </tr>
  <tr>
   <td>request.log</td>
   <td>응답 시간 및 동시 시청</td>
   <td><a href="#interpreting-the-request-log">request.log 해석</a>.</td>
  </tr>
  <tr>
   <td>트러스/선</td>
   <td>페이지 로드</td>
   <td><p>Unix/Linux 명령을 사용하여 시스템 호출 및 신호를 추적합니다. 로그 수준을 <code>INFO</code>으로 늘립니다.</p> <p>요청당 페이지 로드 수, 어떤 페이지 등을 분석합니다.</p> </td>
  </tr>
  <tr>
   <td>스레드 덤프</td>
   <td>JVM 스레드를 관찰합니다. 연락처, 잠금 및 긴 달리기 선수를 식별합니다.</td>
   <td><p>운영 체제에 따라 다름:<br /> - Unix/Linux:<code>kill -QUIT &lt;<em>pid</em>&gt;</code><br /> - Windows(콘솔 모드):Ctrl-Break<br /> </p> <p>분석 도구도 사용할 수 있습니다(예: <a href="https://java.net/projects/tda/">TDA</a>).<br /> </p> </td>
  </tr>
  <tr>
   <td>더미 덤프</td>
   <td>메모리 부족 문제로 성능이 저하됩니다.</td>
   <td><p>AEM에 대한 java 호출에:<br /> <code>-XX:+HeapDumpOnOutOfMemoryError</code><br /> 옵션을 추가합니다.</p> <p>핫 스팟 VM</a>이 있는 Java SE 6에 대한 <a href="https://java.sun.com/javase/6/webnotes/trouble/TSG-VM/html/clopts.html#gbzrr">문제 해결 가이드를 참조하십시오.</a></p> </td>
  </tr>
  <tr>
   <td>시스템 호출</td>
   <td>시간 문제를 식별합니다.</td>
   <td><p><code>System.currentTimeMillis()</code> 또는 <code>com.day.util</code>.시간 설정은 코드에서 또는 <a href="#html-comments">HTML-comments</a>를 통해 타임스탬프를 생성하는 데 사용됩니다.</p> <p><strong>참고: </strong> 이러한 요구 사항은 필요에 따라 활성화/비활성화할 수 있도록 구현해야 합니다.시스템이 순조롭게 작동한다면 통계 수집을 위한 간접비는 필요하지 않을 것이다.</p> </td>
  </tr>
  <tr>
   <td>Apache Bench</td>
   <td>메모리 누수를 식별하고 선택적으로 응답 시간을 분석합니다.</td>
   <td><p>기본 사용:</p> <p><code>ab -k -n &lt;<em>requests</em>&gt; -c &lt;<em>concurrency</em>&gt; &lt;<em>url</em>&gt;</code></p> <p>자세한 내용은 <a href="#apache-bench">Apache Bench</a> 및 <a href="https://httpd.apache.org/docs/2.2/programs/ab.html">ab 매뉴얼 페이지</a>를 참조하십시오.</p> </td>
  </tr>
  <tr>
   <td>검색 분석</td>
   <td> </td>
   <td>오프라인으로 검색 쿼리를 실행하고 쿼리 응답 시간을 식별하고 테스트 및 결과 집합을 확인합니다.<br /> </td>
  </tr>
  <tr>
   <td>JMeter</td>
   <td>로드 및 기능 테스트.</td>
   <td><a href="https://jakarta.apache.org/jmeter/">https://jakarta.apache.org/jmeter/</a></td>
  </tr>
  <tr>
   <td>JProfiler</td>
   <td>심층 CPU 및 메모리 프로파일링</td>
   <td><a href="https://www.ej-technologies.com/">https://www.ej-technologies.com/</a></td>
  </tr>
  <tr>
   <td>JConsole</td>
   <td>JVM 측정 지표 및 스레드를 관찰합니다.</td>
   <td><p>사용:jconsole</p> <p><a href="https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html">jconsole</a> 및 <a href="#monitoring-performance-using-jconsole">JConsole</a>을 사용하여 성능 모니터링을 참조하십시오.</p> <p><strong>참고: </strong> JDK 1.6을 통해 JConsole은 플러그인으로 확장할 수 있습니다.예: Top 또는 TDA(스레드 덤프 분석기)</p> </td>
  </tr>
  <tr>
   <td>Java VisualVM</td>
   <td>JVM 측정 지표, 스레드, 메모리 및 프로파일링을 관찰합니다.</td>
   <td><p>사용:jvisualvm 또는 visualvm<br /> </p> <p><a href="https://java.sun.com/javase/6/docs/technotes/tools/share/jvisualvm.html">jvisualvm</a>, <a href="https://visualvm.dev.java.net/">visualvm</a> 및 <a href="#monitoring-performance-using-j-visualvm">VisualVM</a>을(를) 사용하여 성능 모니터링을 참조하십시오.</p> <p><strong>참고: </strong> JDK 1.6을 사용하면 VisualVM은 플러그인으로 확장할 수 있습니다.</p> </td>
  </tr>
  <tr>
   <td>truss/strace, lsof</td>
   <td>심도 있는 커널 호출 및 프로세스 분석(Unix).</td>
   <td>Unix/Linux 명령</td>
  </tr>
  <tr>
   <td>시간 통계</td>
   <td>페이지 렌더링을 위한 시간 통계를 참조하십시오.</td>
   <td><p>페이지 렌더링에 대한 시간 통계를 보려면 URL에 설정된 <code>?debugClientLibs=true</code>과 함께 <strong>Ctrl-Shift-U</strong>을 사용할 수 있습니다.</p> </td>
  </tr>
  <tr>
   <td>CPU 및 메모리 프로파일링 도구<br /> </td>
   <td><a href="#interpreting-the-request-log">개발</a> 중에 느린 요청을 분석할 때 사용됩니다.</td>
   <td>예: <a href="https://www.yourkit.com/">YourKit</a>.</td>
  </tr>
  <tr>
   <td><a href="#information-collection">정보 수집</a></td>
   <td>설치 진행 상태입니다.</td>
   <td>설치에 대해 가능한 한 많은 정보를 알고 있으면 성능 변경을 일으킬 수 있는 내용과 이러한 변경 사항이 정당한지 여부를 추적하는 데 도움이 됩니다. 중요한 변경 사항을 쉽게 확인할 수 있도록 이러한 지표를 정기적으로 수집해야 합니다.</td>
  </tr>
 </tbody>
</table>

### request.log {#interpreting-the-request-log} 해석

이 파일은 AEM에 대한 모든 요청에 대한 기본 정보를 등록합니다. 이 귀중한 결론으로부터 추출할 수 있다.

`request.log`은 요청이 걸리는 시간을 확인할 수 있는 기본 제공 방법을 제공합니다. 개발 목적으로 `tail -f` `request.log`에 유용하며 응답 시간이 느리도록 확인합니다. 더 큰 `request.log`을 분석하려면 [응답 시간에 대해 정렬 및 필터링할 수 있는 `rlog.jar`을 사용하는 것이 좋습니다](#using-rlog-jar-to-find-requests-with-long-duration-times).

&quot;슬로우&quot; 페이지를 `request.log`에서 분리한 다음 더 나은 성능을 위해 개별적으로 조정하는 것이 좋습니다. 일반적으로 구성 요소당 성능 지표를 포함하거나 ` [yourkit](https://www.yourkit.com/)`과 같은 성능 프로파일링 도구를 사용하여 수행됩니다.

#### 웹 사이트의 트래픽 모니터링 {#monitoring-traffic-on-your-website}

요청 로그는 각 요청이 수행된 응답과 함께 등록합니다.

```xml
09:43:41 [66] -> GET /author/y.html HTTP/1.1
09:43:41 [66] <- 200 text/html 797ms
```

특정 기간(예: 다양한 24시간 이상) 내의 모든 GET 항목을 합산하여 웹 사이트의 평균 트래픽에 대해 설명을 작성할 수 있습니다.

#### request.log {#monitoring-response-times-with-the-request-log}로 응답 시간 모니터링

성능 분석의 좋은 시작점은 요청 로그입니다.

`<cq-installation-dir>/crx-quickstart/logs/request.log`

로그는 다음과 같습니다(단순함을 위해 줄이 단축됨).

```xml
31/Mar/2009:11:32:57 +0200 [379] -> GET /path/x HTTP/1.1
31/Mar/2009:11:32:57 +0200 [379] <- 200 text/html 33ms
31/Mar/2009:11:33:17 +0200 [380] -> GET /path/y HTTP/1.1
31/Mar/2009:11:33:17 +0200 [380] <- 200 application/json 39ms
```

이 로그에는 요청이나 응답당 한 줄이 있습니다.

* 각 요청이나 응답이 이루어진 날짜입니다.
* 대괄호 안의 요청 수입니다. 이 숫자는 요청 및 응답에 일치합니다.
* 요청인지(오른쪽 화살표) 아니면 응답인지(왼쪽 화살표)를 나타내는 화살표.
* 요청의 경우 라인은 다음을 포함합니다.

   * 메서드(일반적으로 GET, HEAD 또는 POST)
   * 요청한 페이지
   * 프로토콜

* 응답의 경우 다음 항목이 포함됩니다.

   * 상태 코드(200은 &quot;성공&quot;을 의미하며 404는 &quot;페이지를 찾을 수 없음&quot;을 의미합니다.
   * MIME 유형
   * 응답 시간

작은 스크립트를 사용하여 로그 파일에서 필요한 정보를 추출하고 원하는 통계를 취합할 수 있습니다. 이 중에서 속도가 느린 페이지 또는 페이지 유형과 전체 성능이 만족스러운지 확인할 수 있습니다.

#### request.log {#monitoring-search-response-times-with-the-request-log}로 검색 응답 시간 모니터링

검색 요청은 로그 파일에도 등록됩니다.

```xml
31/Mar/2009:11:35:34 +0200 [338] -> GET /author/playground/en/tools/search.html?query=dilbert&size=5&dispenc=utf-8 HTTP/1.1
31/Mar/2009:11:35:34 +0200 [338] <- 200 text/html 1562ms
```

따라서 위와 같이 스크립트를 사용하여 관련 정보를 추출하고 통계를 작성할 수 있습니다.

그러나 응답 시간을 결정했으면 요청이 수행하는 데 시간이 걸리는 이유와 응답을 개선하기 위해 수행할 수 있는 작업을 분석해야 할 수 있습니다.

#### 동시 사용자의 수 및 영향 모니터링 {#monitoring-the-number-and-impact-of-concurrent-users}

다시 `request.log`을 사용하여 동시 시청 및 시스템 반응을 모니터링할 수 있습니다.

부정적인 영향을 보기 전에 시스템에서 처리할 수 있는 동시 사용자 수를 판별하려면 테스트를 수행해야 합니다. 다시 스크립트를 사용하여 로그 파일에서 결과를 추출할 수 있습니다.

* 특정 시간 범위(예: 1분) 내에서 수행된 요청 수 모니터링
* 동일한 요청을 동시에(가능한 한 가까이) 수행하는 특정 수의 사용자의 효과를 테스트합니다.예: **저장**&#x200B;을 동시에 클릭하는 30명의 사용자.

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

AEM에는
`<cq-installation-dir>/crx-quickstart/opt/helpers`

이러한 요청 중 하나인 `rlog.jar`을 사용하여 요청이 가장 긴 시간부터 가장 짧은 시간에 지속 시간으로 표시되도록 `request.log`을 빠르게 정렬할 수 있습니다.

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

예를 들어 `request.log` 파일을 매개 변수로 지정하여 실행하고 길이가 가장 긴 첫 번째 요청 10개를 표시할 수 있습니다.

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

특수 사례(예: 가비지 수집 등)의 영향을 최소화하려면 `apachebench`(추가 설명서는 [ab](https://httpd.apache.org/docs/2.2/programs/ab.html) 참조)과 같은 도구를 사용하여 메모리 누수를 식별하고 선택적으로 응답 시간을 분석하는 것이 좋습니다.

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

위의 숫자는 기본 AEM 설치에 포함되어 있는 geometrixx 회사 페이지에 액세스하는 표준 MAcBook Pro 랩탑(2010년 중반)에서 가져옵니다. 페이지는 매우 간단하지만 성능에 맞게 최적화되지 않았습니다.

`apachebench` 또한 모든 동시 요청에 대해 요청당 시간을 평균으로 표시합니다.자세한 내용은  `Time per request: 54.595 [ms]` (평균, 모든 동시 요청) 을 참조하십시오. 모든 효과를 보려면 동시 실행 매개 변수 `-c`(한 번에 수행할 여러 요청 수)의 값을 변경할 수 있습니다.

### 요청 카운터 {#request-counters}

요청 트래픽에 대한 정보(특정 기간 동안의 요청 수)는 인스턴스 로드를 나타냅니다. 이 정보는 [request.log](#interpreting-the-request-log)에서 추출할 수 있지만 카운터를 사용하면 데이터 수집을 자동화하여 다음과 같은 내용을 볼 수 있습니다.

* 활동(즉, &quot;많은 요청&quot;과 &quot;낮은 활동&quot;을 구별함)
* 인스턴스를 사용하지 않는 경우
* 다시 시작(카운터가 0으로 재설정됨)

정보 수집을 자동화하려면 RequestFilter를 설치하여 모든 요청에 대해 카운터를 늘릴 수도 있습니다. 여러 기간에 여러 카운터를 사용할 수 있습니다.

수집된 정보는 다음을 나타내기 위해 사용할 수 있습니다.

* 활동의 중대한 변화
* 중복된 인스턴스
* 다시 시작(0으로 재설정된 카운터)

### HTML 주석 {#html-comments}

서버 성능을 위해 모든 프로젝트에 `html comments`이 포함되는 것이 좋습니다. 좋은 사례가 적지 않다.페이지를 선택하고 볼 페이지 소스를 열고 아래쪽으로 스크롤할 수 있습니다. 다음과 같은 코드를 볼 수 있습니다.

```xml
</body>
 </html>
        <!--
        Page took 58 milliseconds to be rendered by server
         -->
```

### JConsole {#monitoring-performance-using-jconsole}을(를) 사용하여 성능 모니터링

도구 명령 `jconsole`은 JDK에서 사용할 수 있습니다.

1. AEM 인스턴스를 시작합니다.
1. 실행 `jconsole.`
1. AEM 인스턴스와 **Connect**&#x200B;를 선택합니다.

1. `Local` 응용 프로그램 내에서 `com.day.crx.quickstart.Main`;개요는 기본값으로 표시됩니다.

   ![chlimage_1-1](assets/chlimage_1-1.png)

   그 후에는 다른 옵션을 선택할 수 있습니다.

### (J)VisualVM {#monitoring-performance-using-j-visualvm}을(를) 사용하여 성능 모니터링

JDK 1.6부터 도구 명령 `jvisualvm`을 사용할 수 있습니다. JDK 1.6을 설치한 후 다음을 수행할 수 있습니다.

1. AEM 인스턴스를 시작합니다.

   >[!NOTE]
   >
   >Java 5를 사용하는 경우 JVM을 시작하는 java 명령줄에 `-Dcom.sun.management.jmxremote` 인수를 추가할 수 있습니다. JMX는 Java 6에서 기본적으로 활성화되어 있습니다.

1. 다음 중 하나를 실행합니다.

   * `jvisualvm`:JDK 1.6 bin 폴더(테스트된 버전)
   * `visualvm`:VisualVM [에서](https://visualvm.dev.java.net/)  다운로드 가능(Breding Edge 버전)

1. `Local` 응용 프로그램 내에서 `com.day.crx.quickstart.Main`;개요는 기본값으로 표시됩니다.

   ![chlimage_1-2](assets/chlimage_1-2.png)

   이후에는 모니터를 비롯한 다른 옵션을 선택할 수 있습니다.

   ![chlimage_1-3](assets/chlimage_1-3.png)

이 도구를 사용하여 스레드 덤프와 메모리 헤드 덤프를 생성할 수 있습니다. 이 정보는 기술 지원 팀에 의해 요청되는 경우가 많습니다.

### 정보 수집 {#information-collection}

설치에 대해 가능한 한 많은 정보를 알고 있으면 성능 변경을 일으킬 수 있는 내용과 이러한 변경 사항이 정당한지 여부를 추적하는 데 도움이 됩니다. 중요한 변경 사항을 쉽게 확인할 수 있도록 이러한 지표를 정기적으로 수집해야 합니다.

다음 정보가 유용할 수 있습니다.

* [몇 명의 작성자가 시스템을 사용하고 있습니까?](#how-many-authors-are-working-with-the-system)
* [일별 평균 페이지 활성화 수는 얼마입니까?](#what-is-the-average-number-of-page-activations-per-day)
* [이 시스템에서 현재 몇 페이지를 유지 관리하고 있습니까?](#how-many-pages-do-you-currently-maintain-on-this-system)
* [MSM을 사용하는 경우 월평균 롤아웃 수는 어떻게 됩니까?](#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month)
* [월평균 Live Copy 수는 얼마입니까?](#what-is-the-average-number-of-live-copies-per-month)
* [AEM Assets을 사용하는 경우 현재 자산에서 몇 개의 자산을 유지하고 있습니까?](#ifyouusecqdamhowmanyassetsdoyoucurrentlymaintainincqdam)
* [자산의 평균 크기는 얼마입니까?](#what-is-the-average-size-of-the-assets)
* [현재 사용된 템플릿 수는 얼마나 됩니까?](#how-many-templates-are-currently-used)
* [현재 사용되는 구성 요소 수는 얼마나 됩니까?](#how-many-components-are-currently-used)
* [최고 시간에 작성자 시스템에 몇 개의 요청이 있습니까?](#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time)
* [최대 시간에 게시 시스템에 몇 개의 요청이 있습니까?](#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time)

#### 몇 명의 작성자가 시스템을 사용하고 있습니까?{#how-many-authors-are-working-with-the-system}

설치 이후 시스템을 사용한 작성자 수를 보려면 명령줄을 사용합니다.

```shell
cd <cq-installation-dir>/crx-quickstart/logs
cut -d " " -f 3 access.log | sort -u | wc -l
```

주어진 날짜에 작업하는 작성자 수를 보려면:

```shell
grep "<date>" access.log | cut -d " " -f 3 | sort -u | wc -l
```

#### 일별 평균 페이지 활성화 수는 얼마입니까?{#what-is-the-average-number-of-page-activations-per-day}

서버 설치 이후 총 페이지 활성화 수를 보려면 저장소 쿼리를 사용합니다.CRXDE 사용 - 도구 - 쿼리:

* **유형** `XPath`

* **경로** `/`

* **쿼리** `//element(*, cq:AuditEvent)[@cq:type='Activate']`

그런 다음 설치 후 경과된 일 수를 계산하여 평균을 계산합니다.

#### 이 시스템에서 현재 몇 페이지를 유지 관리하고 있습니까?{#how-many-pages-do-you-currently-maintain-on-this-system}

현재 서버에 있는 페이지 수를 보려면 저장소 쿼리를 사용합니다.CRXDE 사용 - 도구 - 쿼리:

* **유형** `XPath`

* **경로** `/`

* **쿼리** `//element(*, cq:Page)`

#### MSM을 사용하는 경우 월평균 롤아웃 수는 어떻게 됩니까?{#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month}

설치 이후 총 롤아웃 수를 확인하려면 저장소 쿼리를 사용합니다.CRXDE 사용 - 도구 - 쿼리:

* **유형** `XPath`

* **경로** `/`

* **쿼리** `//element(*, cq:AuditEvent)[@cq:type='PageRolledOut']`

설치 후 경과된 개월 수를 계산하여 평균을 계산합니다.

#### 월평균 Live Copy 수는 얼마입니까?{#what-is-the-average-number-of-live-copies-per-month}

설치 후 저장소 쿼리를 사용한 전체 Live Copy 수를 확인하려면CRXDE 사용 - 도구 - 쿼리:

* **유형** `XPath`

* **경로** `/`

* **쿼리** `//element(*, cq:LiveSyncConfig)`

설치 후 경과된 개월 수를 다시 사용하여 평균을 계산합니다.

#### AEM Assets을 사용하는 경우 현재 자산에서 몇 개의 자산을 유지하고 있습니까?{#if-you-use-aem-assets-how-many-assets-do-you-currently-maintain-in-assets}

현재 유지 관리하고 있는 DAM 자산 수를 보려면 저장소 쿼리를 사용하십시오.CRXDE 사용 - 도구 - 쿼리:

* **유형** `XPath`
* **경로** `/`
* **쿼리** `/jcr:root/content/dam//element(*, dam:Asset)`

#### 자산의 평균 크기는 얼마입니까?{#what-is-the-average-size-of-the-assets}

`/var/dam` 폴더의 전체 크기를 확인하려면:

1. WebDAV를 사용하여 저장소를 로컬 파일 시스템에 매핑합니다.

1. 명령줄 사용:

   ```shell
   cd /Volumes/localhost/var
   du -sh dam/
   ```

   평균 크기를 얻으려면 `/var/dam`(위에서 획득)의 전체 자산 수로 전역 크기를 나누십시오.

#### 현재 사용된 템플릿 수는 얼마나 됩니까?{#how-many-templates-are-currently-used}

현재 서버에 있는 템플릿 수를 보려면 저장소 쿼리를 사용합니다.CRXDE 사용 - 도구 - 쿼리:

* **유형** `XPath`
* **경로** `/`
* **쿼리** `//element(*, cq:Template)`

#### 현재 사용되는 구성 요소 수는 얼마나 됩니까?{#how-many-components-are-currently-used}

현재 서버에 있는 구성 요소 수를 보려면 저장소 쿼리를 사용합니다.CRXDE 사용 - 도구 - 쿼리:

* **유형** `XPath`
* **경로** `/`
* **쿼리** `//element(*, cq:Component)`

#### 최고 시간에 작성자 시스템에 몇 개의 요청이 있습니까?{#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time}

최대 시간에 작성자 시스템에 있는 시간당 요청을 확인하려면:

1. 설치 이후 총 요청 수를 확인하려면 명령줄을 사용합니다.

   ```shell
   cd <cq-installation-dir>/crx-quickstart/logs
   grep -R "\->" request.log | wc -l
   ```

1. 시작 및 종료 날짜를 결정하려면:

   ```shell
   vim request.log
   G / 1G: for the last/first lines
   ```

   이 값을 사용하여 설치 후 경과한 시간, 시간당 평균 요청 수를 계산합니다.

#### 최대 시간에 게시 시스템에 몇 개의 요청이 있습니까?{#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time}

게시 인스턴스에서 위의 절차를 반복합니다.

## 특정 시나리오 분석 중 {#analyzing-specific-scenarios}

다음은 특정 성능 문제가 있는지 여부를 확인할 항목에 대한 제안 목록입니다. 목록이 완전히 포괄적인 것은 아니다.

>[!NOTE]
>
>자세한 내용은 다음 아티클을 참조하십시오.
>
>* [스레드 덤프](https://helpx.adobe.com/experience-manager/kb/TakeThreadDump.html)
>* [메모리 문제 분석](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)
>* [내장된 프로파일러를 사용하여 분석](https://helpx.adobe.com/experience-manager/kb/AnalyzeUsingBuiltInProfiler.html)
>* [느리거나 차단된 프로세스 분석](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)

>



### 100% {#cpu-at}의 CPU

시스템의 CPU가 100%로 계속 실행되고 있는 경우 다음을 참조하십시오.

* 기술 자료:

   * [슬로우 및 차단된 프로세스 분석](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)

### 메모리 부족 {#out-of-memory}

개발 및 테스트 중에 이러한 오류를 탐지해야 하지만 특정 시나리오는 미끄러질 수 있습니다.

시스템에 메모리가 부족한 경우 성능 저하 및 하위 텍스트를 포함하는 오류 메시지 등 다양한 방법으로 볼 수 있습니다.

`java.lang.OutOfMemoryError`

이러한 경우 다음을 확인하십시오.

* [AEM](/help/sites-deploying/deploy.md#getting-started)을 시작하는 데 사용되는 JVM 설정
* 기술 자료:

   * [메모리 문제 분석](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)

### 디스크 I/O {#disk-i-o}

시스템에 디스크 공간이 부족하거나 디스크 스래싱이 시작되는 경우 다음을 참조하십시오.

* 디버그 정보 수집을 비활성화했는지 여부;다음을 포함하여 다양한 위치에서 구성할 수 있습니다.

   * [Apache Sling JSP 스크립트 핸들러](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjspscripthandler)
   * [Apache Sling Java 스크립트 핸들러](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjavascripthandler)
   * [Apache Sling 로깅 구성](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)
   * [CQ HTML 라이브러리 관리자](/help/sites-deploying/osgi-configuration-settings.md#daycqhtmllibrarymanager)
   * [CQ WCM 디버그 필터](/help/sites-deploying/osgi-configuration-settings.md#daycqwcmdebugfilter)
   * [로거](/help/sites-deploying/monitoring-and-maintaining.md#activating-the-debug-log-level) [](/help/sites-deploying/configuring.md#loggersandwritersforindividualservices)

* [버전 삭제](/help/sites-deploying/version-purging.md)를 구성했는지 여부 및 방법
* 기술 자료:

   * [열려 있는 파일이 너무 많습니다.](https://helpx.adobe.com/experience-manager/kb/TooManyOpenFiles.html)
   * [저널에 디스크 공간이 너무 많이 소모됨](https://helpx.adobe.com/experience-manager/kb/JournalTooMuchDiskSpace.html)

### 정규 성능 저하 {#regular-performance-degradation}

각 재부팅 후(1주일 이상 후) 인스턴스 성능이 저하되는 경우 다음을 확인할 수 있습니다.

* [메모리 부족](#outofmemory)
* 기술 자료:

   * [닫히지 않은 세션](https://helpx.adobe.com/experience-manager/kb/AnalyzeUnclosedSessions.html)

### JVM 튜닝 {#jvm-tuning}

JVM(Java Virtual Machine)은 조정(특히 Java 7 이후)과 관련하여 크게 향상되었습니다. 이러한 이유로 적절한 고정 JVM 크기를 지정하고 기본값을 사용하는 것이 적절할 수 있습니다.

기본 설정이 적합하지 않으면 JVM을 조정하기 전에 GC 성능을 모니터링하고 평가하는 방법을 설정해야 합니다.이 작업에는 더미 크기, 알고리즘 및 기타 측면을 비롯한 모니터링 요소가 포함될 수 있습니다.

다음과 같은 일반적인 선택 사항이 있습니다.

* VerboseGC:

   ```
   -verbose:gc \
    -Xloggc:$LOGS/verbosegc.log \
    -XX:+PrintGCDetails \
    -XX:+PrintGCDateStamps
   ```

결과 로그는 다음과 같은 GC 시각화 도우미에서 인제스트할 수 있습니다.

` [https://www.ibm.com/developerworks/library/j-ibmtools2/](https://www.ibm.com/developerworks/library/j-ibmtools2/)`

또는 JConsole:

* 이러한 설정은 &quot;전체 열기&quot; JMX 연결에 사용됩니다.

   ```
   -Dcom.sun.management.jmxremote \
    -Dcom.sun.management.jmxremote.port=8889 \
    -Dcom.sun.management.jmxremote.authenticate=false \
    -Dcom.sun.management.jmxremote.ssl=false
   ```

* 그런 다음 JConsole과 JVM에 연결합니다.참조:
   ` [https://docs.oracle.com/javase/6/docs/technotes/guides/management/jconsole.html](https://docs.oracle.com/javase/6/docs/technotes/guides/management/jconsole.html)`

사용 중인 메모리 양, 사용 중인 GC 알고리즘, 실행 시간 및 애플리케이션 성능에 미치는 영향을 확인할 수 있습니다. 이렇게 하지 않으면 튜닝을 &quot;임의로 조작하는 손잡이&quot;로 만들 수 있습니다.

>[!NOTE]
>
>oracle VM의 경우 다음 정보도 있습니다.
>
>[https://docs.oracle.com/javase/7/docs/technotes/guides/vm/server-class.html](https://docs.oracle.com/javase/7/docs/technotes/guides/vm/server-class.html)
