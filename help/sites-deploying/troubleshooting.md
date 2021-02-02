---
title: 문제 해결
seo-title: 문제 해결
description: 이 문서에서는 AEM에서 발생할 수 있는 설치 문제 중 일부를 다룹니다.
seo-description: 이 문서에서는 AEM에서 발생할 수 있는 설치 문제 중 일부를 다룹니다.
uuid: 2ca898c3-b074-4ccd-a383-b92f226e6c14
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 5542de4e-6262-4300-9cf8-0eac79ba4f9a
translation-type: tm+mt
source-git-commit: 9b65f7194dc648ba9a6dbc127bc8d5951f126269
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 1%

---


# 문제 해결{#troubleshooting}

이 섹션에는 문제를 해결하는 데 도움이 되는 로그에 대한 자세한 정보가 포함되며 AEM에서 발생할 수 있는 일부 문제에 대한 정보도 포함합니다.

## 작성자 성능 문제 해결 {#troubleshoot-author-performance}

작성 인스턴스에서 느린 성능을 분석하는 것은 매우 복잡할 수 있습니다. 첫 번째 단계에서는 성능이 떨어지고 있는 기술 스택의 수준을 파악해야 합니다.

다음 의사 결정 트리는 병목 현상을 좁힐 수 있는 지침을 제공합니다.

![chlimage_1-75](assets/chlimage_1-75.png)

## 기본 최적화 {#basic-optimization}

![chlimage_1-76](assets/chlimage_1-76.png)

## 로그 파일 구성 및 감사 로그 {#configuring-log-files-and-audit-logs}

AEM은 설치 문제를 해결하기 위해 구성할 수 있는 세부 로그를 기록합니다. 자세한 내용은 [감사 레코드 및 로그 파일 작업](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) 섹션을 참조하십시오.

## 세부 정보 옵션 사용 {#using-the-verbose-option}

AEM WCM을 시작할 때 다음과 같이 명령줄에 -v (verbose) 옵션을 추가할 수 있습니다.java -jar cq-wcm-quickstart-&lt;version>.jar -v.

세부 정보 옵션은 콘솔에 일부 빠른 시작 로그 출력을 표시하므로 문제 해결에 사용할 수 있습니다.

## 일반적인 설치 문제 {#common-installation-issues}

다음 섹션에서는 설치 문제 및 해당 솔루션에 대해 설명합니다.

### 빠른 시작 jar를 두 번 클릭해도 아무런 효과가 없거나 다른 프로그램(예: 아카이브 관리자)이 있는 jar 파일을 엽니다 {#double-clicking-the-quickstart-jar-does-not-have-any-effect-or-opens-the-jar-file-with-another-program-for-example-archive-manager}

일반적으로 운영 체제의 데스크톱 환경이 확장명이 .jar인 파일을 열도록 구성된 방식에 문제가 있음을 나타냅니다. Java가 설치되어 있지 않거나 지원되지 않는 Java 버전을 사용하고 있음을 나타낼 수도 있습니다.

jar 파일이 유비쿼터스 ZIP 형식을 사용하므로 일부 아카이브 프로그램은 jar 파일을 아카이브 파일로 열도록 데스크탑을 자동으로 구성할 수 있습니다.

문제를 해결하려면 다음을 수행합니다.

* Java 버전 1.6이 설치되어 있는지 다시 확인하십시오.
* AEM WCM Quickstart에서 컨텍스트 메뉴(일반적으로 마우스 오른쪽 단추 클릭)를 선택하고 &quot;열기...&quot;를 선택합니다..&quot;
* Java 또는 Sun Java가 나열되었는지 확인하고 AEM WCM과 함께 실행해 보십시오. 여러 Java 버전이 설치되어 있는 경우 지원되는 버전을 선택하십시오.

   이 단계를 성공적으로 수행하고 운영 체제에서 항상 선택한 프로그램을 사용하여 .jar 파일을 실행하는 옵션을 제공하면 해당 프로그램을 선택합니다. 이제 두 번 클릭은 제대로 작동합니다.

* 경우에 따라 지원되는 Java 버전을 다시 설치하면 올바른 연결을 복원하는 데 도움이 됩니다.
* 이 문서의 초반부에서 설명한 대로 명령줄 또는 시작/중지 스크립트를 사용하여 항상 CRX를 실행할 수 있습니다.

### CRX에서 실행 중인 응용 프로그램에서 메모리 부족 오류가 발생합니다 {#my-application-running-on-crx-throws-out-of-memory-errors}.

>[!NOTE]
>
>[메모리 문제 분석](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)도 참조하십시오.


CRX 자체에는 메모리 풋프린트가 매우 적다. CRX 내에서 실행되는 응용 프로그램이 더 많은 메모리 요구 사항을 가지고 있거나 메모리 중심 작업(예: 큰 트랜잭션)을 요청하는 경우 CRX가 실행되는 JVM 인스턴스를 적절한 메모리 설정으로 시작해야 합니다.

Java 명령 옵션을 사용하여 JVM의 메모리 설정을 정의합니다(예: java -Xmx512m -jar crx&amp;ast;.jar로 heapsize를 512MB로 설정).

명령줄에서 AEM WCM을 시작하는 동안 메모리 설정 옵션을 지정합니다. AEM WCM 시작/중지 스크립트 또는 AEM WCM 시작 관리를 위한 사용자 정의 스크립트를 수정하여 필요한 메모리 설정을 정의할 수도 있습니다.

heapsize를 512MB로 이미 정의한 경우 더미 덤프를 만들어 메모리 문제를 더 분석할 수 있습니다.

메모리가 부족한 상태에서 더미 덤프를 자동으로 만들려면 다음 명령을 사용합니다.

java -Xmx256m -XX:+HeapDumpOnOutOfMemoryError -jar &amp;ast;.jar

더미 덤프 파일(**java_..)이 생성됩니다.프로세스가 메모리가 부족할 때마다 hprof**). 더미 덤프가 생성된 후에도 프로세스가 계속 실행될 수 있습니다. 일반적으로 한 더미 덤프 파일이 문제를 분석하는 데 충분합니다.

### AEM Quickstart를 두 번 클릭해도 AEM Welcome 화면이 브라우저에 표시되지 않습니다 {#the-aem-welcome-screen-does-not-display-in-the-browser-after-double-clicking-aem-quickstart}

특정 상황에서 저장소 자체가 성공적으로 실행되더라도 AEM WCM 시작 화면이 자동으로 표시되지 않습니다. 이는 운영 체제 설정, 브라우저 구성 또는 유사한 요인에 따라 달라질 수 있습니다.

일반적인 증상은 AEM WCM 빠른 시작 창에 &quot;AEM WCM 시작, 서버 시작을 기다리는 중...&quot;이 표시됩니다..&quot; 이 메시지가 상대적으로 긴 기간 동안 표시되는 경우 기본 4502 포트 또는 인스턴스가 실행 중인 포트를 사용하여 AEM WCM URL을 브라우저 창에 수동으로 입력합니다.http://localhost:4502/을 참조하십시오.

또한 로그는 브라우저가 시작되지 않는 이유를 알 수 있습니다.

AEM WCM Quickstart 창에 &quot;AEM WCM 실행 중&quot;이라는 메시지가 나타나며 브라우저가 자동으로 시작되지 않는 경우가 있습니다. 이 경우 AEM WCM 빠른 시작 창의 URL(하이퍼링크)을 클릭하거나 브라우저에 URL을 수동으로 입력합니다.

다른 모든 것이 실패할 경우 로그를 확인하여 발생한 상황을 확인합니다.

## 응용 프로그램 서버 {#troubleshooting-installations-with-an-application-server}을(를) 사용한 설치 문제 해결

### geometrixx-outdoor 페이지 {#page-not-found-returned-when-requesting-a-geometrixx-outdoor-page} 요청 시 페이지를 찾을 수 없음

**WebLogic 10.3.5 및 JBoss 5.1에 적용**

geometrixx-outdoors/en 페이지에 대한 요청이 404(페이지 찾을 수 없음)를 반환하는 경우 이러한 특정 응용 프로그램 서버에 필요한 sling.properties 파일에서 추가 sling 속성을 설정했는지 다시 확인할 수 있습니다.

자세한 내용은 *AEM 웹 응용 프로그램 배포* 단계를 참조하십시오.

### 응답 헤더 크기는 4Kb {#response-header-size-can-be-greater-than-kb}보다 클 수 있습니다.

502 오류는 웹 서버가 AEM HTTP 응답 헤더의 크기를 처리할 수 없음을 나타낼 수 있습니다. AEM은 4Kb보다 큰 쿠키를 포함하는 HTTP 응답 헤더를 생성할 수 있습니다. 최대 응답 헤더 크기가 4kb를 초과할 수 있도록 서블릿 컨테이너가 구성되어 있는지 확인합니다.

예를 들어 Tomcat 7.0의 경우 [HTTP Connector](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html)의 maxHttpHeaderSize 속성은 머리글 크기에 대한 제한을 제어합니다.

## Adobe Experience Manager {#uninstalling-adobe-experience-manager} 제거

AEM은 단일 디렉토리에 설치되므로 제거 유틸리티를 사용할 필요가 없습니다. AEM 제거 방법은 원하는 방법과 계속 사용하는 스토리지에 따라 다르지만, 전체 설치 디렉토리를 삭제하는 것만큼 간단하게 제거할 수 있습니다.

영구 스토리지가 설치 디렉토리에 포함되는 경우(예: 기본 TarPM 설치에서) 폴더를 삭제하면 데이터도 제거됩니다.

>[!NOTE]
>
>Adobe은 AEM을 삭제하기 전에 저장소를 백업하는 것이 좋습니다. 전체 &lt;cq-installation-directory>를 삭제하면 저장소가 삭제됩니다. 다른 폴더를 삭제하기 전에 저장소 데이터를 유지하려면 &lt;cq-installation-directory>/crx-quickstart/repository 폴더를 다른 위치로 이동하거나 복사하십시오.

AEM 설치 시 데이터베이스 서버와 같은 외부 저장소를 사용하는 경우 폴더를 제거해도 데이터가 자동으로 제거되지는 않지만 저장소 구성이 제거되므로 JCR 컨텐츠 복원이 어렵습니다.

### JSP 파일은 JBoss {#jsp-files-are-not-compiled-on-jboss}에서 컴파일되지 않습니다.

JBoss의 Experience Manager에 JSP 파일을 설치 또는 업데이트한 후 해당 서버가 컴파일되지 않은 경우 JBoss JSP 컴파일러가 올바르게 구성되어 있는지 확인합니다. 자세한 내용은
[JBoss](https://helpx.adobe.com/experience-manager/kb/jsps-dont-compile-jboss.html) 아티클의 JSP 컴파일 문제

### Java 11 {#the-website-does-not-load-or-fails-intermittently-with-java11}을(를) 사용하여 웹 사이트가 가끔씩 로드되지 않거나 실패합니다.

AEM 6.5가 Java 11에서 실행되는 것으로 알려진 문제가 있습니다. 이 경우 웹 사이트가 로드되지 않거나 간헐적으로 실패할 수 있습니다.

이러한 경우에는 아래 해결 방법을 따르십시오.

1. `crx-quickstart/conf/` 폴더 아래에서 `sling.properties` 파일을 엽니다.
1. 다음 줄을 찾습니다.

   `org.osgi.framework.bootdelegation=sun.,com.sun.`

1. 다음으로 바꿉니다.

   `org.osgi.framework.bootdelegation=sun.,com.sun.,jdk.internal.reflect,jdk.internal.reflect.*`

1. 인스턴스를 다시 시작합니다.