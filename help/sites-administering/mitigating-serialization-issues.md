---
title: AEM의 직렬화 문제 완화
description: AEM의 직렬화 문제를 완화하는 방법에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 01e9ab67-15e2-4bc4-9b8f-0c84bcd56862
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# AEM의 직렬화 문제 완화{#mitigating-serialization-issues-in-aem}

## 개요 {#overview}

Adobe의 AEM 팀은 오픈 소스 프로젝트와 긴밀히 협력했습니다 [NotSoSerial](https://github.com/kantega/notsoserial) 에 설명된 취약점을 완화하는 데 도움을 주다. **CVE-2015-7501**. NotSoSerial은 [Apache 2 라이센스](https://www.apache.org/licenses/LICENSE-2.0) 및 자체 라이선스가 부여된 ASM 코드 포함 [유사 라이선스](https://asm.ow2.io/).

이 패키지에 포함된 에이전트 jar는 Adobe이 수정한 NotSoSerial 배포입니다.

NotSoSerial은 Java™ 수준 문제에 대한 Java™ 수준 솔루션이며 AEM 전용이 아닙니다. 개체를 deserialize하려는 시도에 preflight 검사를 추가합니다. 허용 목록에 추가하다 차단 목록에 추가하다 이 검사는 클래스 이름을 방화벽에 대해 테스트하거나, 방화벽에 대해 테스트하거나, 또는 방화벽에 대해 테스트합니다. 기본 차단 목록의 제한된 클래스 수로 인해 이 테스트는 시스템에 영향을 주지 않거나 코드에 영향을 주지 않습니다.

기본적으로 에이전트는 현재 알려진 취약성 클래스에 대해 차단 목록에 추가하다 검사를 수행합니다. 이 차단 목록에 추가하다는 이러한 유형의 취약성 목록에서 여러분을 보호하기 위한 것입니다.

의 지침에 따라 차단 목록에 추가하다 및 허용 목록에 추가하다를 구성할 수 있습니다. [에이전트 구성](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) 이 문서의 섹션.

이 에이전트는 알려진 최신 취약한 계층을 완화하는 데 도움을 주기 위한 것입니다. 프로젝트가 신뢰할 수 없는 데이터를 역직렬화하는 경우에도 서비스 거부 공격, 메모리 부족 공격 및 알 수 없는 향후 역직렬화 공격에 취약할 수 있습니다.

Adobe은 공식적으로 Java™ 6, 7 및 8을 지원합니다. 그러나 NotSoSerial은 Java™ 5도 지원한다는 것이 Adobe의 이해입니다.

## 에이전트 설치 {#installing-the-agent}

>[!NOTE]
>
>AEM 6.1용 직렬화 핫픽스를 이전에 설치한 경우 Java™ 실행 라인에서 에이전트 시작 명령을 제거합니다.

1. 설치 **com.adobe.cq.cq-serialization-tester** 번들.

1. 의 번들 웹 콘솔로 이동합니다. `https://server:port/system/console/bundles`
1. 직렬화 번들을 찾아 시작합니다. 이렇게 하면 NotSoSerial 에이전트가 자동으로 로드됩니다.

## 애플리케이션 서버에 에이전트 설치 {#installing-the-agent-on-application-servers}

NotSoSerial 에이전트는 애플리케이션 서버용 AEM의 표준 배포에 포함되지 않습니다. 하지만 AEM jar 배포에서 추출하여 애플리케이션 서버 설정과 함께 사용할 수 있습니다.

1. 먼저 AEM 빠른 시작 파일을 다운로드하고 추출합니다.

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. 새로 압축 해제된 AEM 빠른 시작의 위치로 이동하여 `crx-quickstart/opt/notsoserial/` 폴더 위치: `crx-quickstart` AEM 애플리케이션 서버 설치 폴더.

1. 의 소유권 변경 `/opt` 서버를 실행 중인 사용자에게:

   ```shell
   chown -R opt <user running the server>
   ```

1. 이 문서의 다음 섹션에 표시된 대로 에이전트가 제대로 활성화되었는지 구성하고 확인합니다.

## 에이전트 구성 {#configuring-the-agent}

대부분의 설치에는 기본 구성이 적합합니다. 이 구성에는 알려진 원격 실행 취약한 클래스의 차단 목록 및 역직렬화(deserialization)가 안전한 신뢰할 수 있는 패키지의 허용 목록에 추가하다가 포함되어 있습니다.

방화벽 구성은 동적이며 언제든지 다음 방법으로 변경할 수 있습니다.

1. 의 웹 콘솔로 이동 `https://server:port/system/console/configMgr`
1. 검색 및 클릭 **Deserialization Firewall Configuration.**

   >[!NOTE]
   >
   >다음 위치의 URL에 액세스하여 구성 페이지에 직접 연결할 수도 있습니다.
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`

이 구성에는 허용 목록에 추가하다, 차단 목록에 추가하다 및 deserialization 로깅이 포함되어 있습니다.

**목록 허용**

허용 목록 섹션에서 이러한 목록은 deserialization에 허용되는 클래스 또는 패키지 접두사입니다. 사용자 고유의 클래스를 역직렬화하는 경우 클래스 또는 패키지를 이 허용 목록에 추가하다에 추가합니다.

**차단 목록**

블록 목록 섹션에는 deserialization이 허용되지 않는 클래스가 있습니다. 이러한 클래스의 초기 집합은 원격 실행 공격에 취약한 것으로 발견된 클래스로 제한된다. 나열된 모든 항목 앞에 차단 목록에 추가하다가 적용됩니다.

**진단 로깅**

진단 로깅 섹션에서 역직렬화가 발생할 때 기록할 몇 가지 옵션을 선택할 수 있습니다. 이러한 옵션은 처음 사용할 때만 기록되며 이후 사용할 때는 다시 기록되지 않습니다.

의 기본값 **클래스 이름 전용** deserialize되는 클래스를 알려줍니다.

다음을 설정할 수도 있습니다 **전체 스택** 첫 번째 역직렬화 시도의 Java™ 스택을 기록하여 역직렬화가 수행되는 위치를 알려주는 옵션입니다. 이 옵션은 사용에서 역직렬화를 찾아 제거하는 데 유용합니다.

## 에이전트의 활성화 확인 {#verifying-the-agent-s-activation}

다음 URL을 찾아 역직렬화 에이전트의 구성을 확인할 수 있습니다.

* `https://server:port/system/console/healthcheck?tags=deserialization`

URL에 액세스하면 에이전트와 관련된 상태 검사 목록이 표시됩니다. 상태 검사가 전달되고 있는지 확인하여 에이전트가 제대로 활성화되었는지 확인할 수 있습니다. 실패한 경우 에이전트를 수동으로 로드해야 합니다.

에이전트의 문제 해결에 대한 자세한 내용은 다음을 참조하십시오. [동적 에이전트 로드 시 오류 처리](#handling-errors-with-dynamic-agent-loading) 아래요.

>[!NOTE]
>
>을(를) 추가하면 `org.apache.commons.collections.functors` 허용 목록에 추가하다는 항상 실패한다.

## 동적 에이전트 로드 시 오류 처리 {#handling-errors-with-dynamic-agent-loading}

로그에 오류가 노출되거나 확인 단계에서 에이전트 로드 문제를 감지하면 에이전트를 수동으로 로드하십시오. JDK(Java™ Development Toolkit) 대신 JRE(Java™ Runtime Environment)를 사용하는 경우에도 동적 로드 도구를 사용할 수 없으므로 이 워크플로를 사용하는 것이 좋습니다.

에이전트를 수동으로 로드하려면 다음을 수행하십시오.

1. 다음 옵션을 추가하여 CQ jar의 JVM 시작 매개변수를 편집합니다.

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >포크된 JVM에서 에이전트가 활성화되지 않았으므로 적절한 JVM 메모리 설정과 함께 -nofork CQ/AEM 옵션도 사용해야 합니다.

   >[!NOTE]
   >
   >NotSoSerial 에이전트 jar의 Adobe 분포는 `crx-quickstart/opt/notsoserial/` AEM 설치 폴더.

1. JVM을 중지했다가 다시 시작합니다.

1. 위에서 설명한 단계에 따라 에이전트의 활성화를 다시 확인합니다. [에이전트의 활성화 확인](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation).

## 기타 고려 사항 {#other-considerations}

IBM® JVM에서 실행 중인 경우 Java™ Attach API 지원에 대한 설명서가에서 검토하십시오. [이 위치](https://www.ibm.com/docs/en/sdk-java-technology/8?topic=documentation-java-attach-api).
