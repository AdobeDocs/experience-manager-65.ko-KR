---
title: AEM 문제 해결
seo-title: AEM 문제 해결
description: AEM 관련 문제 해결에 대해 알아봅니다.
seo-description: AEM 관련 문제 해결에 대해 알아봅니다.
uuid: 72379531-915c-45d0-ba70-42b212665272
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6346cd93-1ca3-4510-9c31-a74c41017ddb
docset: aem65
translation-type: tm+mt
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538

---


# AEM 문제 해결 {#troubleshooting-aem}

다음 섹션에서는 AEM 사용 시 발생할 수 있는 몇 가지 문제와 이러한 문제를 해결하는 방법에 대한 제안을 다룹니다.

>[!NOTE]
>
>AEM에서 작성 문제를 해결하는 경우 작성자에 [대한 문제 해결을 참조하십시오.](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>문제가 발생하는 경우 인스턴스(릴리스 및 서비스 팩)에 대한 [알려진 문제](/help/release-notes/known-issues.md) 목록을 확인하는 것이 유용할 수 있습니다.

## 관리자를 위한 문제 해결 시나리오 {#troubleshooting-scenarios-for-administrators}

다음 표에서는 관리자가 문제를 해결해야 하는 문제에 대한 개요를 제공합니다.

<table>
 <tbody>
  <tr>
   <td><strong>역할</strong></td>
   <td><strong>문제 </strong></td>
  </tr>
  <tr>
   <td>시스템 관리자</td>
   <td><p>빠른 시작 jar를 두 번 클릭해도 아무런 효과가 없거나 다른 프로그램과 함께 jar 파일을 엽니다(예: 아카이브 관리자).</p> </td>
  </tr>
  <tr>
   <td><p>시스템 관리자</p> </td>
   <td><p>CRX에서 실행되는 내 애플리케이션에서 메모리 부족 오류가 발생합니다.</p> </td>
  </tr>
  <tr>
   <td><p>시스템 관리자</p> </td>
   <td><p>AEM CM Quickstart를 두 번 클릭하면 브라우저에 AEM 시작 화면이 표시되지 않습니다.</p> </td>
  </tr>
  <tr>
   <td><p>시스템 관리자</p> <p>관리자 사용자</p> </td>
   <td><p>스레드 덤프 만들기</p> </td>
  </tr>
  <tr>
   <td><p>시스템 관리자</p> <p>관리자 사용자</p> </td>
   <td><p>닫히지 않은 JCR 세션 확인</p> </td>
  </tr>
 </tbody>
</table>

## 설치 문제 {#installation-issues}

다음 [문제 해결 시나리오에](/help/sites-deploying/troubleshooting.md#common-installation-issues) 대한 자세한 내용은 일반적인 설치 문제를 참조하십시오.

* 빠른 시작 jar를 두 번 클릭해도 영향을 주지 않거나 JAR 파일이 다른 프로그램(예: 아카이브 관리자)에서 실행됩니다.
* CRX에서 애플리케이션을 실행하면 메모리 부족 오류가 발생합니다.
* AEM Quickstart를 두 번 클릭해도 AEM Welcome 화면이 브라우저에 표시되지 않습니다.

## 분석 문제 해결 방법 {#methods-for-troubleshooting-analysis}

### 스레드 덤프 만들기 {#making-a-thread-dump}

스레드 덤프는 현재 활성 상태인 모든 Java 스레드의 목록입니다. AEM이 제대로 응답하지 않으면 스레드 덤프가 교착 상태 또는 기타 문제를 식별하는 데 도움이 될 수 있습니다.

### Sling Thread Dumper 사용 {#using-sling-thread-dumper}

1. AEM **웹 콘솔을 엽니다**.예를 들어 에 `https://localhost:4502/system/console/`있습니다.
1. 상태 **탭**&#x200B;아래에서&#x200B;**스레드를** 선택합니다.

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### jstack(명령줄) 사용 {#using-jstack-command-line}

1. AEM Java 인스턴스의 PID(프로세스 ID)를 찾습니다.

   예를 들어 `ps -ef` 또는 를 사용할 수 `jps`있습니다.

1. 실행:

   `jstack <pid>`

1. 그러면 스레드 덤프가 표시됩니다.

>[!NOTE]
>
>출력 리디렉션을 사용하여 로그 파일에 스레드 덤프를 추가할 수 `>>` 있습니다.
>
>`jstack <pid> >> /path/to/logfile.log`

자세한 [내용은 JVM에서 스레드 덤프를](https://helpx.adobe.com/cq/kb/TakeThreadDump.html) 가져오는 방법을 참조하십시오.

### 닫히지 않은 JCR 세션 확인 {#checking-for-unclosed-jcr-sessions}

AEM WCM에 대한 기능이 개발되면 JCR 세션을 열 수 있습니다(데이터베이스 연결 열기와 비교). 열린 세션이 종료되지 않으면 시스템에서 다음과 같은 증상이 나타날 수 있습니다.

* 시스템 속도가 느려집니다.
* CacheManager가 많이 표시됩니다.resize로그 파일의 모든 항목;다음 숫자(size=&lt;x>)는 캐시 수를 보여주며 각 세션은 여러 개의 캐시를 엽니다.
* 때때로 시스템의 메모리가 부족합니다(심각도에 따라 몇 시간, 일 또는 몇 주 후).

닫히지 않은 세션을 분석하고 세션을 닫지 않는 코드를 확인하려면 기술 자료 문서 닫히지 않은 세션 [분석을 참조하십시오](https://helpx.adobe.com/crx/kb/AnalyzeUnclosedSessions.html).

### Adobe Experience Manager 웹 콘솔 사용 {#using-the-adobe-experience-manager-web-console}

OSGi 번들의 상태는 발생할 수 있는 문제를 조기에 나타낼 수 있습니다.

1. AEM **웹 콘솔을 엽니다**.예를 들어 에 `https://localhost:4502/system/console/`있습니다.
1. OSGI **탭 아래에서** 번들을 **선택합니다** .
1. 확인:

   * 번들의 상태. 비활성 또는 불만족인 경우 번들을 중지하고 다시 시작하십시오. 문제가 지속되는 경우 다른 방법을 사용하여 더 자세히 조사해야 할 수 있습니다.
   * 번들 중 하나라도 누락된 종속성이 있는지 여부. 이러한 세부 사항은 링크인 개별 번들 이름을 클릭하여 확인할 수 있습니다(다음 예에는 문제가 없음).

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)

