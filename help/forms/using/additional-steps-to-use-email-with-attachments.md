---
title: 첨부 파일이 있는 이메일을 받는 추가 단계
description: JEE 플랫폼에서 AEM Forms용 첨부 파일이 있는 이메일을 검색할 수 없는 경우 오류를 해결하는 방법에 대해 알아봅니다.
exl-id: 0d0713fb-d95a-4a95-91ef-9cdaea30e343
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 12%
---
# JEE 플랫폼에서 AEM Forms에 대한 첨부 파일이 있는 이메일을 가져올 수 없음{#unable-to-get-email-with-attachments}

이 문제는 다음 버전에 적용됩니다.

* Experience Manager 6.5 Forms

## 문제 {#issue}

사용자는 이메일을 통해 PDF 보내기 또는 제출 구성이 있는 첨부 파일 포함과 같은 작업을 수행할 수 없습니다.

## 솔루션 {#solution}

1. jar를 [java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar)(으)로 다운로드하고 다운로드한 jar 파일의 압축을 해제하여 매니페스트 파일을 가져옵니다.

1. 1단계에서 검색된 `java.mail-1.0.jar`의 매니페스트 파일을 사용하여 사용자 지정 jar 파일(`java.mail-1.5.jar`)을 만듭니다.

1. 매니페스트 파일을 열고 `1.5.0`의 모든 항목을 `1.5.6`(으)로, `Bundle-Version: 1.0`의 모든 항목을 `Bundle-Version:1.5`(으)로 바꾸기

1. `C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin` 폴더에서 다음 명령을 사용하여 사용자 지정 jar(`java.mail-1.5.jar`) 파일을 다음과 같이 만듭니다.
   `jar -cfm java.mail-1.5.jar manifest.mf`

   위의 명령에서 *manifest.mf*&#x200B;은(는) 매니페스트 파일의 이름이고 *java.mail-1.5.jar*&#x200B;은(는) 위 명령을 실행한 후 만들 파일의 이름입니다.

1. [javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1)을 다운로드합니다.

1. `http://<server name>:<port>/lc/system/console/bundles`(으)로 이동하여 이름이 `JavaMail API (com.sun.mail.javax.mail) version 1.6.2`인 번들을 삭제합니다.

1. 3단계에서 가져온 `java.mail-1.5.jar` 설치. 이 단계에서는 JEE 배포의 Sling 속성을 다시 시작합니다. `http://<server name>:<port>/lc/system/console/bundles`에 설치된 번들이 **Active**(으)로 상태를 표시할 때까지 기다립니다.

   >상태가 여전히 **InActive**&#x200B;인 경우 **서비스 콘솔**&#x200B;에서 **JBoss®**&#x200B;을(를) 다시 시작하십시오.


1. 5단계를 사용하여 다운로드한 `javax.mail-1.5.6.redhat-1.jar`파일을 설치합니다.

1. **서비스 콘솔**&#x200B;에서 **JBoss®**&#x200B;을(를) 중지하고 **Sling.properties** 파일에 다음 속성을 추가하십시오.
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. **JBoss®**&#x200B;을(를) 다시 시작합니다.

>[!NOTE]
>
> SDK를 다시 시작하려면 &#39;Ctrl+C&#39; 명령을 사용하는 것이 좋습니다. 예를 들어 Java 프로세스를 중지하는 것과 같은 대체 방법을 사용하여 AEM SDK를 다시 시작하면 AEM 개발 환경에서 불일치가 발생할 수 있습니다.
