---
title: AEM의 직렬화 문제 완화
seo-title: Mitigating serialization issues in AEM
description: AEM의 직렬화 문제를 완화하는 방법을 알아봅니다.
seo-description: Learn how to mitigate serialization issues in AEM.
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
exl-id: 01e9ab67-15e2-4bc4-9b8f-0c84bcd56862
source-git-commit: 614c4c88f3f09feb5a400ade9f45f634ac4fbcd5
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# AEM의 직렬화 문제 완화{#mitigating-serialization-issues-in-aem}

## 개요 {#overview}

Adobe의 AEM 팀은 오픈 소스 프로젝트와 긴밀하게 작업했다 [NotSoSerial](https://github.com/kantega/notsoserial) 에 설명된 취약점을 완화하는 데 도움이 됩니다. **CVE-2015-7501**. NotSoSerial는 [Apache 2 라이센스](https://www.apache.org/licenses/LICENSE-2.0) 및 는 자체 라이선스가 부여된 ASM 코드를 포함합니다 [BSD 유사 라이선스](https://asm.ow2.io/).

이 패키지에 포함된 에이전트 jar는 Adobe의 수정된 NotSoSerial 배포입니다.

NotSoSerial는 Java™ 레벨 문제에 대한 Java™ 레벨 솔루션이며 AEM에 특정하지 않습니다. 객체를 역직렬화하려고 하면 프리플라이트 검사가 추가됩니다. 이 검사는 방화벽 스타일, 허용 목록에 추가하다 또는 둘 다에 대해 클래스 이름을 차단 목록에 추가하다 테스트합니다. 기본의 제한된 클래스 수로 차단 목록에 추가하다 인해 가 테스트는 시스템 또는 코드에 영향을 주지 않을 수 있습니다.

기본적으로 에이전트는 현재 알려진 취약점 클래스에 대해 차단 목록에 추가하다 검사를 수행합니다. 이차단 목록에 추가하다는 이 유형의 취약성을 사용하는 현재 취약점 목록에서 사용자를 보호하기 위한 것입니다.

차단 목록에 추가하다 및 허용 목록에 추가하다는 [에이전트 구성](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) 섹션 을 참조하십시오.

에이전트는 알려진 최신 취약성 클래스를 완화하도록 돕기 위한 것입니다. 프로젝트가 신뢰할 수 없는 데이터를 deserialize하는 경우 서비스 거부 공격, 메모리 공격 및 알 수 없는 향후 deserialization 취약할 수 있습니다.

Adobe은 공식적으로 Java™ 6, 7 및 8을 지원합니다. 그러나 Adobe은 NotSoSerial도 Java™ 5을 지원한다는 것을 알고 있습니다.

## 에이전트 설치 {#installing-the-agent}

>[!NOTE]
>
>이전에 AEM 6.1용 serialization 핫픽스를 설치한 경우 Java™ 실행 줄에서 에이전트 시작 명령을 제거합니다.

1. 설치 **com.adobe.cq.cq-serialization-tester** 번들입니다.

1. 의 번들 웹 콘솔로 이동합니다. `https://server:port/system/console/bundles`
1. 직렬화 번들을 찾아 시작합니다. 이렇게 하면 NotSoSerial 에이전트가 자동으로 로드됩니다.

## 애플리케이션 서버에 에이전트 설치 {#installing-the-agent-on-application-servers}

NotSoSerial 에이전트는 응용 프로그램 서버에 대한 AEM의 표준 배포에 포함되지 않습니다. 그러나 AEM jar 배포에서 추출하여 애플리케이션 서버 설정과 함께 사용할 수 있습니다.

1. 먼저 AEM 빠른 시작 파일을 다운로드하고 추출합니다.

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. 새로 압축을 푼 AEM 빠른 시작 위치로 이동한 다음 를 복사합니다 `crx-quickstart/opt/notsoserial/` 폴더 `crx-quickstart` AEM 애플리케이션 서버 설치 폴더.

1. 소유권 변경 `/opt` 서버를 실행하는 사용자에게

   ```shell
   chown -R opt <user running the server>
   ```

1. 이 문서의 다음 섹션에 표시된 대로 에이전트가 제대로 활성화되었는지 구성 및 확인합니다.

## 에이전트 구성 {#configuring-the-agent}

기본 구성은 대부분의 설치에 적합합니다. 이 구성에는 알려진 원격 실행 취약성 클래스차단 목록에 추가하다의와 신뢰할 수 있는 데이터의 역직렬화가 안전한 패키지의 허용 목록에 추가하다 그룹이 포함됩니다.

방화벽 구성은 동적이며, 언제든지 다음과 같이 변경할 수 있습니다.

1. 의 웹 콘솔로 이동 `https://server:port/system/console/configMgr`
1. 검색 및 클릭 **Deserialization 방화벽 구성.**

   >[!NOTE]
   다음 URL에 액세스하여 구성 페이지에 직접 액세스할 수도 있습니다.
   * `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


이 구성에는 허용 목록에 추가하다, 차단 목록에 추가하다 역직렬화 로깅이 포함되어 있습니다.

**목록 허용**

허용 목록 섹션에서 이러한 목록은 deserialization에 허용되는 클래스 또는 패키지 접두사입니다. 고유한 클래스를 deserialize하는 경우 이 클래스에 클래스나 패키지를 허용 목록에 추가하다 추가하십시오.

**차단 목록**

블록 목록 섹션에서 역직렬화에는 허용되지 않는 클래스입니다. 이러한 클래스의 초기 집합은 원격 실행 공격에 취약하다고 판단되는 클래스로 제한됩니다. 이차단 목록에 추가하다는 허용 목록에 추가된 항목 전에 적용됩니다.

**진단 로깅**

진단 로깅 섹션에서 역직렬화가 발생할 때 기록할 여러 옵션을 선택할 수 있습니다. 이러한 옵션은 처음 사용할 때만 기록되며 이후 사용 시 다시 기록되지 않습니다.

기본값은 입니다. **class-name-only** deserialize하고 있는 클래스를 알려줍니다.

을 설정할 수도 있습니다 **전체 스택** deserialization이 수행되는 위치를 알리기 위해 첫 번째 deserialization 시도에서 Java™ 스택을 기록하는 옵션입니다. 이 옵션은 사용에서 역직렬화를 찾아 제거하는 데 유용합니다.

## 에이전트의 활성화 확인 {#verifying-the-agent-s-activation}

다음 URL에서 deserialization 에이전트의 구성을 확인할 수 있습니다.

* `https://server:port/system/console/healthcheck?tags=deserialization`

URL에 액세스하면 에이전트와 관련된 상태 확인 목록이 표시됩니다. 상태 검사가 전달되고 있는지 확인하여 에이전트가 제대로 활성화되었는지 확인할 수 있습니다. 실패한 경우 에이전트를 수동으로 로드해야 합니다.

에이전트 문제 해결에 대한 자세한 내용은 [동적 에이전트 로드 시 오류 처리](#handling-errors-with-dynamic-agent-loading) 아래의 제품에서 사용할 수 있습니다.

>[!NOTE]
추가할 경우 `org.apache.commons.collections.functors` 허용 목록에 추가하다에게 상태 검사가 항상 실패합니다.

## 동적 에이전트 로드 시 오류 처리 {#handling-errors-with-dynamic-agent-loading}

로그에 오류가 표시되거나 확인 단계에서 에이전트를 로드하는 데 문제가 감지되면 에이전트를 수동으로 로드합니다. 동적 로드를 위한 도구를 사용할 수 없으므로 JDK(Java™ Development Toolkit) 대신 JRE(Java™ Runtime Environment)를 사용하는 경우에도 이 워크플로우를 권장합니다.

에이전트를 수동으로 로드하려면 다음을 수행하십시오.

1. CQ jar의 JVM 시작 매개 변수를 편집하고 다음 옵션을 추가합니다.

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   포크된 JVM에서 에이전트가 활성화되지 않으므로 적절한 JVM 메모리 설정과 함께 -nofork CQ/AEM 옵션을 사용해야 합니다.

   >[!NOTE]
   NotSoSerial 에이전트 jar의 Adobe 배포은 `crx-quickstart/opt/notsoserial/` AEM 설치 폴더.

1. JVM 중지 및 재시작

1. 위에서 설명한 단계에 따라 에이전트의 활성화를 다시 확인합니다. [에이전트의 활성화 확인](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation).

## 기타 고려 사항 {#other-considerations}

IBM® JVM에서 실행 중인 경우 Java™ Attach API 지원에 대한 설명서를 참조하십시오. [이 위치](https://www.ibm.com/docs/en/sdk-java-technology/8?topic=documentation-java-attach-api).
