---
title: JEE에서 AEM Forms의 XXE, Struts 개발 모드 구성 및 원격 코드 실행 취약성 완화
description: JEE에서 AEM Forms의 XXE, 구성 및 원격 코드 실행 취약성 완화
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 9fade12f-a038-4fd6-8767-1c30966574c5
solution: Experience Manager, Experience Manager Forms
release-date: 2025-08-05T00:00:00Z
source-git-commit: cacad43c2c32a1a14de0ea5f845818018ba8b2ec
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 5%

---

# JEE에서 RCE(CVE-2025-49533), Struts 개발 모드 구성(CVE-2025-54253), XXE(CVE-2025-54254) 및 AEM Forms의 취약점 완화 {#mitigating-xxe-configuration-rce-vulnerabilities-aem-forms}

## 빠른 참조

| **영향 수준** | **영향을 받는 버전** | **권장 작업** |
|---|---|---|
| **중요** | JEE 서비스 팩 23의 AEM 6.5 Forms(6.5.23.0) | [최신 핫픽스 설치](#option-1-for-users-on-version-65230-install-latest-hotfix) |
| **중요** | JEE 서비스 팩 18~22의 AEM 6.5 Forms(6.5.18.0 - 6.5.22.0) | [수동으로 수정 사항 설치](#option-2-for-users-on-65180---65220-manual-hotfix-installation) |
| **중요** | JEE 서비스 팩 17(6.5.17.0) 또는 이전 버전의 AEM 6.5 Forms | 지원되는 서비스 팩 버전으로 업그레이드한 다음 새 버전에 대한 권장 완화 단계를 적용하십시오 |
| **영향을 받지 않음** | AEM Forms on OSGi, Workbench, Cloud Service | 필요한 작업 없음 |

**해결된 취약점:**

- 원격 코드 실행(CVE-2025-49533)
- 구성 보안 문제(CVE-2025-54253)
- XML 외부 엔티티(XXE) 처리(CVE-2025-54254)

## 개요

### 영향을 받는 사항

| 취약성 | 영향 | 영향을 받는 구성 요소 |
|---|---|---|
| **CVE-2025-49533**: 원격 코드 실행 | GetDocumentServlet에서 인증되지 않은 코드 실행 | JEE 서비스 팩 23(6.5.23.0) 및 이전 버전의 AEM 6.5 Forms |
| **CVE-2025-54253**: 구성 문제 | 관리자 UI에서 Struts 개발 모드 활성화됨 | JEE 서비스 팩 23(6.5.23.0) 및 이전 버전의 AEM 6.5 Forms |
| **CVE-2025-54254**: XXE 처리 | Document Security 모듈이 승인되지 않은 파일 액세스를 허용 | JEE 서비스 팩 23(6.5.23.0) 및 이전 버전의 AEM 6.5 Forms |


### 영향을 받지 않는 사항

- Experience Manager Forms Workbench (모든 버전)
- OSGi의 Experience Manager Forms(모든 버전)
- Experience Manager Forms as a Cloud Service

## 해결 옵션


### 시작하기에 앞서

변경하기 전에 수정하거나 업데이트하려는 EAR 파일 또는 DSC 파일을 백업하십시오.

- 배포 디렉터리에서 원본 EAR 또는 DSC 파일을 찾습니다.
- 파일을 배포 디렉터리 외부의 보안 백업 위치에 복사합니다.
- 업데이트를 진행하기 전에 백업이 완료되고 액세스할 수 있는지 확인하십시오.

이 주의 사항을 사용하면 업데이트 프로세스 중에 문제가 발생하는 경우 원래 상태를 복원할 수 있습니다.

### 옵션 1: (버전 6.5.23.0의 사용자용) 최신 핫픽스 설치

1. [6.5.23.0](/help/release-notes/aem-forms-hotfix.md)용 핫픽스를 다운로드합니다.
1. 표준 [핫픽스/패치 설치 지침](/help/release-notes/jee-patch-installer-65.md) 준수
1. IBM WebSphere 또는 Oracle WebLogic에서 Document Security(이전의 Rights Management)를 사용하는 경우 AEM Forms 서버를 시작하기 전에 다음 Java 시스템 속성(JVM 인수)을 설정하십시오.

   ```
   -Dcom.adobe.forms.jee.services.allowDoctypeDeclaration=true
   ```

1. 응용 프로그램 서버 다시 시작

### 옵션 2: (6.5.18.0 - 6.5.22.0의 사용자용) 수동 핫픽스 설치

+++6.5.18.0 - 6.5.22.0용 수동 핫픽스 설치

**1단계: 핫픽스 패키지 다운로드 및 추출**

- Adobe 소프트웨어 배포 포털에서 [ - 6.5.22.6.5.18.0용 ](/help/release-notes/aem-forms-hotfix.md)핫픽스를 다운로드합니다.
- 로컬에서 추출

**2단계: 올바른 버전 폴더로 이동**

- 환경에 설치된 서비스 팩 버전에 따라 일치하는 폴더로 이동합니다.

  서비스 팩 20의 예 폴더는 다음과 같습니다.

  ```
  <extracted-hotfix>/SP20/
  ```

**3단계: 배포 디렉터리 찾기**

- JEE 서버의 AEM Forms에서

  ```
  [AEM installation directory]/deploy
  ```

  예: `adobe/adobe-experience-manager-forms/deploy`



**4단계: EAR 파일 업데이트 및 바꾸기**

>[!BEGINTABS]

>[!TAB JBos]

1. `adobe-core-jboss.ear`을(를) 열고 `adminui.war`을(를) 다음으로 바꾸기

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adminui.war
   ```

   예, `adobe-xxe-configuration-hotfix/SP20/jboss/adminui.war`

1. `adobe-core-jboss.ear` 내에서 `lib/` 폴더로 이동하여 `adobe-uisupport.jar`을(를) 다음으로 바꾸기:

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   예, `adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`

1. 귀를 막아라. 변경 사항이 제대로 저장되었는지 확인합니다.


1. `adobe-edcserver-jboss.ear` 바꾸기

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adobe-edcserver-jboss.ear
   ```

   예, `adobe-xxe-configuration-hotfix/SP20/jboss/adobe-edcserver-jboss.ear`

1. `adobe-forms-jboss.ear` 바꾸기

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adobe-forms-jboss.ear
   ```

   예, `adobe-xxe-configuration-hotfix/SP20/jboss/adobe-forms-jboss.ear`



>[!TAB WebLogic]

1. `adobe-core-weblogic.ear`을(를) 열고 `adminui.war`을(를) 다음으로 바꾸기

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adminui.war
   ```

   예, `adobe-xxe-configuration-hotfix/SP20/weblogic/adminui.war`

1. `adobe-core-weblogic.ear` 내에서 `adobe-uisupport.jar`을(를) 다음으로 바꾸기:

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   예, `adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`

1. 귀를 막아라. 변경 사항이 제대로 저장되었는지 확인합니다.


1. `adobe-edcserver-weblogic.ear` 바꾸기

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adobe-edcserver-weblogic.ear
   ```

   예, `adobe-xxe-configuration-hotfix/SP20/weblogic/adobe-edcserver-weblogic.ear`

1. `adobe-forms-weblogic.ear` 바꾸기

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adobe-forms-weblogic.ear
   ```

   예, `adobe-xxe-configuration-hotfix/SP20/weblogic/adobe-forms-weblogic.ear`

>[!TAB WebSphere]

1. `adobe-core-websphere.ear`을(를) 열고 `adminui.war`을(를) 다음으로 바꾸기

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adminui.war
   ```

   예, `adobe-xxe-configuration-hotfix/SP20/websphere/adminui.war`

1. `adobe-core-websphere.ear` 내에서 `adobe-uisupport.jar`을(를) 다음으로 바꾸기:

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   예, `adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`

1. 귀를 막아라. 변경 사항이 제대로 저장되었는지 확인합니다.


1. `adobe-edcserver-websphere.ear` 바꾸기

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adobe-edcserver-websphere.ear
   ```

   예, `adobe-xxe-configuration-hotfix/SP20/websphere/adobe-edcserver-websphere.ear`

1. `adobe-forms-websphere.ear` 바꾸기

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adobe-forms-websphere.ear
   ```

   예, `adobe-xxe-configuration-hotfix/SP20/websphere/adobe-forms-websphere.ear`

>[!ENDTABS]



**5단계: `adobe-rightsmanagement-<appserver>-dsc.jar`파일을**(으)로 업데이트

```
adobe-xxe-configuration-hotfix/SP[version]/<appserver>/adobe-rightsmanagement-<appserver>-dsc.jar
```

예, `adobe-xxe-configuration-hotfix/SP20/jboss/adobe-rightsmanagement-jboss-dsc.jar`

**6단계: WebSphere 및 WebLogic에서 문서 보안을 위한 추가 구성**:

Document Security(이전의 Rights Management)를 사용하는 경우 AEM Forms 서버를 시작하기 전에 다음 Java 시스템 속성(JVM 인수)을 설정하십시오.

```
-Dcom.adobe.forms.jee.services.allowDoctypeDeclaration=true
```


**7단계: 구성 관리자 다시 실행**

- 구성 관리자를 실행하여 업데이트된 EAR을 다시 배포하고 핫픽스를 적용합니다

+++

### 옵션 3: (6.5.17.0 및 이전 버전의 사용자용) 업그레이드 경로

1. [지원되는 서비스 팩 버전으로 업그레이드](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)
1. 새 버전을 기준으로 위의 옵션 1 또는 옵션 2를 따르십시오.

## 참조

- [CWE-611: XML 외부 엔터티 참조를 잘못 제한합니다](https://cwe.mitre.org/data/definitions/611.html)
- [CWE-16: 구성](https://cwe.mitre.org/data/definitions/16.html)
- [OWASP XXE 방지 치트 시트](https://owasp.org/www-community/vulnerabilities/XML_External_Entity_XXE_Processing)
- [Adobe Experience Manager Forms 보안 모범 사례](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=ko)
