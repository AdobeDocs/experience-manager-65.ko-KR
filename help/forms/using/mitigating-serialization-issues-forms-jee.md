---
title: AEM Forms JEE의 직렬화 문제 완화 | ADOBE EXPERIENCE MANAGER
description: JDK 8에서 실행되는 AEM Forms JEE의 Java 역직렬화 문제를 완화하는 방법에 대해 알아봅니다.
solution: Experience Manager, Experience Manager Forms
feature: Security
version: Experience Manager 6.5
type: Documentation
role: Admin
source-git-commit: ec3941675081255879065c3be9d5af77474b2072
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---


# AEM Forms JEE의 직렬화 문제 완화 {#mitigating-serialization-issues-in-aem-forms-jee}

AEM Forms JEE에는 개체를 deserialize하기 전에 preflight 검사를 추가하는 deserialization 방화벽이 포함되어 있습니다. 이 검사는 클래스 이름을 차단 목록에 추가하다 스타일, 허용 목록에 추가하다 또는 둘 다에 대해 테스트하며 Java™ 역직렬화 공격을 통해 악용되는 것으로 알려진 클래스를 거부합니다. 기본 에이전트는 Adobe에서 수정한 오픈 소스 [NotSoSerial](https://github.com/kantega/notsoserial) 프로젝트 배포이며 [Apache 2 라이선스](https://www.apache.org/licenses/LICENSE-2.0)에 따라 라이선스가 부여되었습니다.

**JDK 11 이상**&#x200B;을 실행하는 설치에서 이 보호는 플랫폼의 기본 직렬화 필터링에 의해 활성화되며 수동 단계는 필요하지 않습니다. **JDK 8**&#x200B;을 실행하는 설치에서는 네이티브 직렬화 필터링이 효과적이지 않으므로 시작 시 에이전트를 JVM에 명시적으로 연결해야 합니다. 이 문서에서는 그 방법에 대해 설명합니다.

>[!NOTE]
>
>역직렬화 필터 상태 검사가 이미 서버에서 활성 상태로 보고한 경우([에이전트의 활성화 확인](#verifying-the-agents-activation) 참조) 응용 프로그램 서버가 이미 보호되어 있으므로 이 문서의 나머지 단계를 건너뛸 수 있습니다.

## 시작하기에 앞서 {#before-you-begin}

애플리케이션 서버가 실행되는 Java™ 버전을 확인합니다.

```shell
java -version
```

보고된 버전이 `1.8.x`(JDK 8)인 경우 이 문서의 단계가 적용됩니다. 11 이상인 경우 수동 작업이 필요하지 않습니다. [에이전트의 활성화 확인](#verifying-the-agents-activation)에 설명된 상태 검사를 사용하여 보호를 확인하십시오.

다음 단계에서 `<jee-installation-directory>`은(는) AEM Forms JEE 설치의 루트를 참조합니다.

## 에이전트 적용 {#applying-the-agent}

>[!IMPORTANT]
>
>이 단계를 수행하려면 애플리케이션 서버를 다시 시작해야 합니다. 영향을 받는 각 인스턴스에 적용합니다.

1. **현재 상태를 확인합니다.** 역직렬화 필터 상태 확인으로 이동합니다.

   ```text
   https://<server>:<port>/system/console/healthcheck?tags=deserialization
   ```

   검사가 활성으로 보고하면 인스턴스가 이미 보호되므로 추가 작업이 필요하지 않습니다. 실패할 경우 다음 단계를 계속 진행합니다.

1. **에이전트 JAR이 이미 있는지 확인합니다.** 다음 위치에서 `notsoserial.jar`을(를) 확인하십시오.

   ```text
   <jee-installation-directory>/crx-quickstart/opt/notsoserial/
   ```

1. **JAR가 없으면 추가합니다.** [`notsoserial.jar`](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/notsoserial.jar)을(를) 다운로드하고 각 인스턴스의 위 폴더에 복사합니다.

   ```text
   <jee-installation-directory>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >이 단계를 게시하기 전에 에이전트의 Forms JEE 배포에 대한 공식 Adobe 다운로드 위치로 바꿉니다.

1. 에이전트를 연결하려면 응용 프로그램 서버의 JVM 시작 매개 변수를 **업데이트**&#x200B;하십시오. Java™ 실행 라인에 다음 옵션을 추가합니다.

   ```shell
   -javaagent:<jee-installation-directory>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   Java™ 실행 라인의 정확한 위치는 애플리케이션 서버(예: JBoss, WebLogic 또는 WebSphere®)에 따라 다릅니다. AEM Forms JEE 애플리케이션 서버를 시작하는 데 사용되는 JVM 옵션에 옵션을 추가합니다.

1. JVM을 시작할 때 에이전트가 로드되도록 **JEE 서버를 다시 시작**&#x200B;합니다.

1. **다시 유효성 검사.** 상태 확인으로 다시 이동합니다.

   ```text
   https://<server>:<port>/system/console/healthcheck?tags=deserialization
   ```

   이제 상태 검사가 정상으로 보고됩니다.

## 에이전트의 활성화 확인 {#verifying-the-agents-activation}

다음 URL을 찾아 언제든지 역직렬화 에이전트의 구성을 확인할 수 있습니다.

```text
https://<server>:<port>/system/console/healthcheck?tags=deserialization
```

에이전트와 관련된 상태 검사 목록이 표시됩니다. 검사를 통과하면 에이전트가 제대로 활성화됩니다. JDK 8 인스턴스에서 실패한 경우 에이전트가 로드되지 않았으므로 [에이전트 적용](#applying-the-agent)의 단계를 사용하여 수동으로 첨부해야 합니다.

## 에이전트 구성 {#configuring-the-agent}

애플리케이션 서버의 Java™ 버전이 JDK 8로 실행되는 경우 아래 단계가 적용됩니다. [에이전트 적용](#applying-the-agent)의 단계를 사용하여 에이전트를 첨부 및 로드한 후 에이전트를 구성할 수 있습니다.

기본 구성은 대부분의 설치에 적합합니다. 여기에는 원격 이용 가능한 클래스 및 신뢰할 수 있는 데이터의 역직렬화가 안전한 차단 목록 패키지가 포함됩니다. 허용 목록에추가된 항목 앞에 차단 목록에 추가하다가 적용됩니다.

방화벽 구성은 동적이며 언제든지 변경할 수 있습니다.

1. `https://<server>:<port>/system/console/configMgr`의 웹 콘솔로 이동합니다.

1. **Deserialization Firewall Configuration**&#x200B;을 검색하여 클릭합니다.

이 구성에는 허용 목록, 차단 목록 및 진단 로깅 옵션이 포함되어 있습니다.

* **허용 목록** - 역직렬화가 허용되는 클래스 또는 패키지 접두사입니다. 고유한 클래스를 deserialize하는 경우 여기에 관련 클래스 또는 패키지를 추가하십시오.
* **차단 목록** - 역직렬화가 허용되지 않는 클래스입니다. 초기 집합은 원격 실행 공격에 취약한 것으로 발견되는 클래스로 제한된다.
* **진단 로깅** - 역직렬화가 발생할 때 기록하는 옵션입니다. 기본 **class-name-only**&#x200B;은(는) 역직렬화 중인 클래스를 보고합니다. **전체 스택** 옵션은 첫 번째 역직렬화 시도에 대해 Java™ 스택을 기록하며, 이는 사용에서 신뢰할 수 없는 역직렬화를 찾아 제거하는 데 유용합니다. 이러한 옵션은 처음 사용할 때만 기록됩니다.

## 기타 고려 사항 {#other-considerations}

* 에이전트는 현재 알려진 취약한 계층을 완화하기 위한 것입니다. 프로젝트가 신뢰할 수 없는 데이터를 deserialize하는 경우에도 서비스 거부, 메모리 부족 또는 알 수 없는 향후 deserialization 공격에 노출될 수 있습니다.
* JDK(Java™ Development Kit)가 아닌 JRE(Java™ Runtime Environment)에서 실행하는 경우 동적 에이전트를 로드하는 데 필요한 도구를 사용할 수 없으며 [에이전트 적용](#applying-the-agent)에 설명된 대로 시작 시 에이전트를 수동으로 연결해야 합니다.
* ® JVM에서 실행 중인 경우 Java™ Attach API 지원에 대한 설명서를 검토하십시오.
