---
title: AEM의 정리 문제 완화
seo-title: AEM의 정리 문제 완화
description: AEM 파섹
seo-description: AEM 파섹
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM의 정리 문제 완화{#mitigating-serialization-issues-in-aem}

## 개요 {#overview}

Adobe의 AEM 팀은 CVE-2015-7501 [에](https://github.com/kantega/notsoserial) 설명된 취약점 완화를 지원하기 위해 오픈 소스 프로젝트 NotSoSerial **와 긴밀하게 작업하고 있습니다**. NotSoSerial는 Apache [2 라이선스에](https://www.apache.org/licenses/LICENSE-2.0) 따라 라이선스가 부여되며 자체 BSD [유사 라이선스에](https://asm.ow2.org/license.html)따라 라이선스가 부여된 ASM 코드를 포함합니다.

이 패키지에 포함된 에이전트 jar는 Adobe의 수정된 NotSoSerial 배포입니다.

NotSoSerial는 Java 수준 문제에 대한 Java 수준 솔루션이며 AEM에 고유하지 않습니다. 또한 객체를 역직렬화하려는 시도에 프리플라이트 검사를 추가합니다. 이 검사는 방화벽 스타일 화이트 리스트 및/또는 블랙 리스트에 대해 클래스 이름을 테스트합니다. 기본 블랙리스트에 있는 클래스의 수가 제한되어 있으므로 시스템 또는 코드에 영향을 주지 않을 수 있습니다.

기본적으로 에이전트는 현재 알려진 취약한 계층에 대해 블랙 리스트 검사를 수행합니다. 이 블랙리스트는 이 유형의 취약점을 사용하는 현재 악용 목록으로부터 사용자를 보호하기 위한 것입니다.

블랙 리스트 및 화이트 리스트는 이 문서의 에이전트 구성 [섹션에 설명된 지침에 따라](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) 구성할 수 있습니다.

에이전트는 알려진 최신 취약점을 완화하는 데 도움이 되도록 설계되었습니다. 프로젝트가 신뢰할 수 없는 데이터를 역직렬화하는 경우 서비스 거부 공격, 메모리 부족 공격 및 알 수 없는 향후 역직렬화 악용에 여전히 취약할 수 있습니다.

Adobe는 공식적으로 Java 6, 7 및 8을 지원하지만 NotSoSerial도 Java 5를 지원한다는 점을 이해합니다.

## 에이전트 설치 {#installing-the-agent}

>[!NOTE]
>
>이전에 AEM 6.1에 대한 일련화 핫픽스를 설치한 경우 java 실행 라인에서 에이전트 시작 명령을 제거하십시오.

1. com.adobe.cq.cq **일련화 테스터** 번들을 설치합니다.

1. 번들 웹 콘솔로 이동 위치: `https://server:port/system/console/bundles`
1. 직렬화 번들을 찾아 시작합니다. 이 경우 NotSoSerial 에이전트가 동적으로 자동 로드됩니다.

## 응용 프로그램 서버에 에이전트 설치 {#installing-the-agent-on-application-servers}

NotSoSerial 에이전트는 응용 프로그램 서버용 AEM의 표준 배포에 포함되지 않습니다. 그러나 AEM jar 배포에서 추출하여 애플리케이션 서버 설정과 함께 사용할 수 있습니다.

1. 먼저 AEM 빠른 시작 파일을 다운로드하고 추출합니다.

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. 새로 압축을 푼 AEM 빠른 시작 위치로 이동한 다음 `crx-quickstart/opt/notsoserial/` 폴더를 AEM 애플리케이션 서버 설치의 `crx-quickstart` 폴더에 복사합니다.

1. 서버를 실행하는 `/opt` 사용자로 소유권을 변경합니다.

   ```shell
   chown -R opt <user running the server>
   ```

1. 이 문서의 다음 섹션에 표시된 대로 에이전트가 제대로 활성화되었는지 구성 및 확인합니다.

## 에이전트 구성 {#configuring-the-agent}

대부분의 설치에는 기본 구성이 적합합니다. 여기에는 알려진 원격 실행 취약점의 블랙 리스트 및 신뢰할 수 있는 데이터의 역직렬화가 비교적 안전해야 하는 패키지의 화이트 목록이 포함됩니다.

방화벽 구성은 동적이며, 언제든지 다음을 통해 변경할 수 있습니다.

1. 웹 콘솔 `https://server:port/system/console/configMgr`
1. Deserialization Firewall **Configuration을 검색하고 클릭합니다.**

   >[!NOTE]
   >
   >다음 위치의 URL에 액세스하여 구성 페이지에 직접 액세스할 수도 있습니다.
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


이 구성에는 화이트 리스트, 블랙 리스트 및 역직렬화 로깅이 포함되어 있습니다.

**화이트리스트**

화이트리스트 섹션에서 역직렬화를 위해 허용되는 클래스 또는 패키지 접두어가 있습니다. 고유한 클래스를 역직렬화하는 경우 이 화이트리스트에 클래스나 패키지를 추가해야 합니다.

**블랙리스트**

blacklisting 섹션에는 역직렬화에 허용되지 않는 클래스가 있습니다. 이러한 클래스의 초기 세트는 원격 실행 공격에 취약하다고 판단되는 클래스로 제한됩니다. 블랙리스트는 화이트리스트 등록 항목 이전에 적용됩니다.

**진단 로깅**

진단 로깅의 섹션에서 역직렬화가 수행될 때 기록할 여러 옵션을 선택할 수 있습니다. 처음 사용할 때만 기록되며 이후 사용 시 다시 로그인되지 않습니다.

기본적으로 **class-name-only** 는 deserialized되고 있는 클래스를 알려줍니다.

또한 **전체 스택** 옵션을 설정하여 역직렬화가 수행되는 위치를 알려주기 위해 첫 번째 역직렬화 시도에 대한 java 스택을 기록할 수 있습니다. 이 기능은 사용에서 역직렬화를 찾아 제거하는 데 유용합니다.

## 에이전트의 활성화 확인 {#verifying-the-agent-s-activation}

다음 URL을 검색하여 역직렬화 에이전트의 구성을 확인할 수 있습니다.

* `https://server:port/system/console/healthcheck?tags=deserialization`

URL에 액세스하면 에이전트와 관련된 상태 확인 목록이 표시됩니다. 상태 검사가 전달되고 있는지 확인하여 에이전트가 제대로 활성화되었는지 확인할 수 있습니다. 오류가 발생하면 에이전트를 수동으로 로드해야 할 수 있습니다.

에이전트 문제 해결에 대한 자세한 내용은 [아래의 동적 에이전트 로드 시 오류 처리를](#handling-errors-with-dynamic-agent-loading) 참조하십시오.

>[!NOTE]
>
>허용 목록에 `org.apache.commons.collections.functors` 추가하면 상태 검사가 항상 실패합니다.

## 다이내믹 에이전트 로드 시 오류 처리 {#handling-errors-with-dynamic-agent-loading}

로그에 오류가 표시되거나 확인 단계에서 에이전트를 로드하는 데 문제가 감지되면 에이전트를 수동으로 로드해야 할 수 있습니다. 동적 로딩 도구를 사용할 수 없으므로 JDK(Java Development Toolkit) 대신 JRE(Java Runtime Environment)를 사용하는 경우에도 권장됩니다.

에이전트를 수동으로 로드하려면 아래 지침을 따르십시오.

1. 다음 옵션을 추가하여 CQ jar의 JVM 시작 매개변수를 수정합니다.

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >이렇게 하려면 -nofork CQ/AEM 옵션과 적절한 JVM 메모리 설정을 함께 사용해야 합니다. 이 옵션은 JVM에서 에이전트가 활성화되지 않습니다.

   >[!NOTE]
   >
   >NotSoSerial 에이전트 jar의 Adobe 배포는 AEM 설치의 `crx-quickstart/opt/notsoserial/` 폴더에 있습니다.

1. JVM을 중지하고 다시 시작합니다.

1. Agent의 활성화 확인에 설명된 단계에 따라 [에이전트의 활성화를 다시 확인합니다](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation).

## 기타 고려 사항 {#other-considerations}

IBM JVM에서 실행 중인 경우 [이 위치의](https://www.ibm.com/support/knowledgecenter/SSSTCZ_2.0.0/com.ibm.rt.doc.20/user/attachapi.html)Java 첨부 API에 대한 지원에 대한 설명서를 참조하십시오.

