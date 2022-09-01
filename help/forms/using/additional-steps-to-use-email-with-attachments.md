---
title: '첨부 파일과 함께 이메일을 가져오는 추가 단계 '
description: '첨부 파일과 함께 이메일을 가져오는 추가 단계   '
source-git-commit: 9ee8e79777b89fbf4d6e5b5fd1dbb1ef3bc9ad5d
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# JEE 플랫폼에서 AEM Forms용 첨부 파일이 있는 이메일을 가져올 수 없습니다.{#unable-to-get-email-with-attachments}

이 문제는 다음 버전에 적용됩니다.
* Experience Manager 6.5 Forms

## 문제 {#issue}

전자 메일을 통해 PDF 보내기 또는 제출 구성이 있는 첨부 파일 포함 등의 작업을 수행할 수 없습니다.

## 솔루션 {#solution}

1. jar를 로 다운로드합니다. [java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar) 다운로드한 jar 파일의 압축을 풀고 매니페스트 파일을 가져옵니다.

1. 매니페스트 파일 사용 `java.mail-1.0.jar` 1단계에서 검색하여 다음과 같은 새 사용자 지정 jar 파일을 만듭니다. `java.mail-1.5.jar`.

1. 매니페스트 파일을 열고 `1.5.0` with `1.5.6` 및 `Bundle-Version: 1.0` with `Bundle-Version:1.5`

1. 새 사용자 지정 jar 만들기(`java.mail-1.5.jar`)에서 다음 명령을 사용하여 `C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin` 폴더:
   `jar -cfm java.mail-1.5.jar manifest.mf`

   위의 명령에서 *manifest.mf* 매니페스트 파일 이름 및 *java.mail-1.5.jar* 는 위의 명령을 실행한 후 만들 파일의 이름입니다.

1. 다운로드 [javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1).

1. 다음으로 이동 `http://<server name>:<port>/lc/system/console/bundles`그리고 이름이 인 번들을 삭제합니다. `JavaMail API (com.sun.mail.javax.mail) version 1.6.2`.

1. 설치 `java.mail-1.5.jar` 3단계에서 얻습니다.  이 단계에서는 JEE 배포의 sling 속성을 다시 시작합니다. 에서 설치된 번들을 기다립니다. `http://<server name>:<port>/lc/system/console/bundles` 상태를 로 표시하려면 **활성**.

   >참고: 이 경우에도 상태는 여전히 입니다 **InActive**, 다시 시작   **JBoss** 에서 **서비스 콘솔**.


1. 설치 `javax.mail-1.5.6.redhat-1.jar`5단계를 사용하여 파일을 다운로드했습니다.

1. 정지 **JBoss** 에서 **서비스 콘솔** 및에 다음 속성을 추가합니다. **Sling.properties** 파일:
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. 다시 시작 **JBoss**.