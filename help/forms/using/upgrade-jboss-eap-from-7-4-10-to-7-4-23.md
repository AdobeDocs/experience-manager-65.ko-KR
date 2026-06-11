---
title: JBoss EAP를 7.4.10에서 JEE의 AEM Forms용 7.4.23으로 업그레이드
description: JBoss EAP를 7.4.10에서 7.4.23 for AEM Forms on JEE 독립형 환경으로 업그레이드하는 절차.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
exl-id: 8f4c2a91-6b3d-4e7f-9c12-5d8e1f0a2b34
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms Upgrade,AEM Forms on JEE
role: User, Developer
source-git-commit: 652162941dd716ae797ce50709e91757dad99054
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 3%

---

# JBoss EAP를 7.4.10에서 JEE의 AEM Forms용 7.4.23으로 업그레이드 {#upgrade-jboss-eap-from-7-4-10-to-7-4-23}

## 개요 {#overview}

JEE의 AEM Forms 독립형 환경에서 JBoss EAP를 버전 7.4.10에서 7.4.23으로 업그레이드합니다. 업그레이드를 수행하려면 구성 파일, 데이터베이스 자격 증명 및 CRX 저장소를 새 JBoss 설치로 마이그레이션하고 Configuration Manager를 실행하여 설치를 완료해야 합니다.

## 적용 대상 {#applies-to}

이 문서는 다음 경우에 적용됩니다.

* 독립형 환경에서 JBoss EAP 7.4.10에서 실행되는 JEE의 AEM Forms
* Windows 및 Linux의 턴키 및 부분 턴키 설치 모드

>[!NOTE]
>
> JBoss 클러스터 환경을 업그레이드하는 경우 먼저 이 문서의 단계를 완료한 다음 [JEE의 AEM Forms용 JBoss EAP 클러스터를 7.4.10에서 7.4.23으로 업그레이드](/help/forms/using/upgrade-jboss-eap-cluster-from-7-4-10-to-7-4-23.md)의 추가 단계를 수행하십시오.

## 사전 요구 사항 {#prerequisites}

시작하기 전에:

* [Adobe 소프트웨어 배포 포털](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 JBoss 7.4.23 패키지를 다운로드합니다.
* 대상 환경에 대한 관리 액세스 권한이 있는지 확인합니다.
* 기존 JBoss 설치의 전체 백업을 수행합니다.

## 단계 {#steps}

JBoss EAP를 7.4.10에서 7.4.23으로 업그레이드하려면 다음 단계를 수행하십시오.

### JBoss 다운로드 및 추출 {#download-and-extract-jboss}

1. Adobe 소프트웨어 배포 포털에서 JBoss 7.4.23 ZIP 패키지를 다운로드합니다.
1. 로컬 디렉토리에 ZIP 파일의 압축을 풉니다.
1. 기존 JBoss 설치 디렉토리의 정확한 이름과 일치하도록 추출된 JBoss 폴더의 이름을 변경합니다.

### 기존 설치 백업 {#back-up-the-existing-installation}

1. 현재 JBoss 설치 디렉토리의 전체 백업을 작성합니다.
1. 백업에 모든 구성 파일 및 사용자 정의 파일이 포함되어 있는지 확인합니다.

### 데이터베이스 파일 구성 {#configure-database-files}

1. 구성 디렉토리로 이동합니다.

   * Windows: `<JBoss_Home>\standalone\configuration`
   * Linux: `<JBoss_Home>/standalone/configuration`

1. 설치 모드에 따라 데이터베이스 파일을 구성합니다.

   **턴키 모드:**

   1. `lc_mysql.xml`의 이름을 `lc_turnkey.xml`(으)로 변경합니다.
   1. 다음 파일을 삭제합니다.

      * `lc_oracle.xml`
      * `lc_mssql.xml`

   **부분 턴키 모드:**

   1. 데이터베이스 엔진에 해당하는 `lc_db.xml` 파일만 유지합니다.
   1. 다른 두 개의 `lc_db.xml` 구성 파일을 삭제합니다.

### 데이터베이스 자격 증명 업데이트 {#update-database-credentials}

1. 백업된 JBoss 설치에서 `lc_turnkey.xml` 파일을 엽니다.
1. 다음 값을 복사합니다.

   * 데이터 소스 URL
   * 데이터베이스 사용자 이름
   * 데이터베이스 암호

1. 새 `lc_turnkey.xml` 파일에서 해당 항목을 업데이트합니다.

### CRX 저장소 마이그레이션 {#migrate-crx-repository}

1. 이전 JBoss 설치에서 다음 디렉토리로 이동합니다.

   `<old_jboss>\bin\`

1. `crx-quickstart` 폴더를 복사합니다.
1. 폴더를 다음 위치에 붙여넣습니다.

   `<new_jboss>\bin\`

### 구성 관리자 실행 {#run-configuration-manager}

1. 업그레이드된 JBoss 환경을 시작합니다.
1. LCM(LiveCycle Configuration Manager)을 시작합니다.
1. 전체 Configuration Manager 워크플로를 실행합니다.
1. 모든 구성 작업이 성공적으로 완료되었는지 확인합니다.

### 업그레이드 후 유효성 검사 {#post-upgrade-validation}

업그레이드 후 다음을 확인하십시오.

* 모든 서비스가 성공적으로 시작됩니다.
* 데이터베이스 연결이 확인되었습니다.
* 애플리케이션 기능이 검증되었습니다.
