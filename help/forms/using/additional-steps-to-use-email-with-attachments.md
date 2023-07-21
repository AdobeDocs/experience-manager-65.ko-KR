---
title: 첨부 파일이 포함된 이메일을 받는 추가 단계
description: 첨부 파일이 포함된 이메일을 받는 추가 단계
exl-id: 0d0713fb-d95a-4a95-91ef-9cdaea30e343
source-git-commit: a56d5121a6ce11b42a6c30dae9e479564d16af27
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# JEE 플랫폼에서 AEM Forms에 대한 첨부 파일이 있는 이메일을 가져올 수 없음{#unable-to-get-email-with-attachments}

이 문제는 다음 버전에 적용됩니다.
* Experience Manager 6.5 Forms

## 문제 {#issue}

사용자는 이메일을 통해 PDF 보내기 또는 제출 구성이 있는 첨부 파일 포함과 같은 작업을 수행할 수 없습니다.

## 솔루션 {#solution}

1. jar를 다음으로 다운로드 [java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar) 다운로드한 jar 파일의 압축을 풀고 매니페스트 파일을 가져옵니다.

1. 다음의 매니페스트 파일 사용 `java.mail-1.0.jar` 사용자 지정 jar 파일(예: )을 만들기 위해 1단계에서 검색됨 `java.mail-1.5.jar`.

1. 매니페스트 파일을 열고 다음의 모든 항목을 바꿉니다. `1.5.0` 포함 `1.5.6` 및 `Bundle-Version: 1.0` 포함 `Bundle-Version:1.5`

1. 사용자 지정 jar 만들기(`java.mail-1.5.jar`)에서 다음 명령을 사용하여 파일을 생성합니다 `C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin` 폴더 이름:
   `jar -cfm java.mail-1.5.jar manifest.mf`

   위의 명령에서, *manifest.mf* 는 매니페스트 파일의 이름이며, *java.mail-1.5.jar* 는 위 명령을 실행한 후 만들 파일의 이름입니다.

1. 다운로드 [javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1).

1. 다음으로 이동 `http://<server name>:<port>/lc/system/console/bundles`및 이라는 이름의 번들 삭제 `JavaMail API (com.sun.mail.javax.mail) version 1.6.2`.

1. 설치 `java.mail-1.5.jar` 3단계에서 가져온 것입니다. 이 단계에서는 JEE 배포의 Sling 속성을 다시 시작합니다. 에 설치된 번들 대기 `http://<server name>:<port>/lc/system/console/bundles` 상태를 다음으로 표시 **활성**.

   >참고: 이 경우 상태는 여전히 입니다. **활성**, 다시 시작   **JBoss®** 다음에서 **서비스 콘솔**.


1. 설치 `javax.mail-1.5.6.redhat-1.jar`5단계를 사용하여 파일을 다운로드했습니다.

1. 중지 **JBoss®** 다음에서 **서비스 콘솔** 및 다음 속성을 추가할 위치 **Sling.properties** 파일:
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. 다시 시작 **JBoss®**.
