---
title: JBoss EAP 클러스터를 7.4.10에서 JEE의 AEM Forms용 7.4.23으로 업그레이드
description: JBoss EAP 클러스터를 7.4.10에서 JEE의 AEM Forms용 7.4.23으로 업그레이드하는 추가 단계입니다.
exl-id: 2c9e7f41-a8d6-4b03-8e5c-1a4f6d9e0b72
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms on JEE
role: User, Developer
source-git-commit: dffa92539a8205387d21d3873ab9424508182f19
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 1%

---

# JBoss EAP 클러스터를 7.4.10에서 JEE의 AEM Forms용 7.4.23으로 업그레이드 {#upgrade-jboss-eap-cluster-from-7-4-10-to-7-4-23}

## 개요 {#overview}

JBoss EAP 클러스터를 버전 7.4.10에서 JEE의 AEM Forms용 7.4.23으로 업그레이드하는 경우 독립형 업그레이드 단계 외에 추가 구성이 필요합니다. 새 JBoss 설치 시 캐시 로케이터, 마스터 슬레이브 인증, 호스트 바인딩 및 도메인 컨트롤러 구성과 같은 클러스터 관련 설정을 업데이트해야 합니다.

## 적용 대상 {#applies-to}

이 문서는 다음 경우에 적용됩니다.

* 클러스터 환경의 JBoss EAP 7.4.10에서 실행 중인 JEE의 AEM Forms
* Windows 및 Linux의 기본 슬레이브 JBoss EAP 구성

## 사전 요구 사항 {#prerequisites}

기존 설치에서 새 구성 파일로 연결 URL, 사용자 이름 및 암호를 복사하는 등 [JEE의 AEM Forms에 대해 JBoss EAP를 7.4.10에서 7.4.23으로 업그레이드](/help/forms/using/upgrade-jboss-eap-from-7-4-10-to-7-4-23.md)의 모든 단계를 완료합니다.

## 단계 {#steps}

다음과 같은 클러스터 관련 추가 단계를 수행합니다.

### domain.conf.bat 업데이트 {#update-domain-conf-bat}

1. `domain.conf.bat`에서 기존 설정의 로케이터 정보를 새 파일에 추가합니다.

   ```text
   set "JAVA_OPTS=%JAVA_OPTS% -Doak.documentMK.maxServerTimeDiffMillis=-1"
   set "JAVA_OPTS=%JAVA_OPTS% -Dadobe.cache.cluster-locators=<ip-address-master>[22345],<ip-address-slave>[22345]"
   set "JAVA_OPTS=%JAVA_OPTS% -DentityExpansionLimit=10000"
   ```

### 마스터-슬레이브 인증 구성 {#configure-master-slave-authentication}

1. 마스터 노드에서 마스터 슬레이브 인증을 위한 새 사용자를 만듭니다.
1. 슬레이브 노드에서 `host.xml`의 사용자 암호를 업데이트하십시오.

   ```xml
   <server-identities>
       <secret value="Y2hhbmdlaXQ="/>
   </server-identities>
   ```

### host.xml의 IP 주소 업데이트 {#update-ip-addresses-in-host-xml}

1. `host.xml`의 마스터 및 슬레이브 노드 모두에 대한 IP 주소를 업데이트하십시오.

   ```xml
   <interfaces>
       <interface name="management">
           <inet-address value="${jboss.bind.address.management:<ip-address>}"/>
       </interface>
       <interface name="public">
           <inet-address value="${jboss.bind.address:<ip-address>}"/>
       </interface>
   </interfaces>
   ```

### 도메인 구성에서 배포 제거 {#remove-deployments-from-domain-configuration}

1. 새 `domain_<db>.xml` 파일에 `<deployments>` 섹션이 없는지 확인하십시오.
1. 기존 구성에서 다음 블록을 복사하지 마십시오.

   ```xml
   <deployments>
       <deployment name="adobe-forms-ivs-jboss.ear" runtime-name="adobe-forms-ivs-jboss.ear"/>
       <deployment name="adobe-livecycle-cq-author.ear" runtime-name="adobe-livecycle-cq-author.ear"/>
       <deployment name="adobe-livecycle-jboss.ear" runtime-name="adobe-livecycle-jboss.ear"/>
       <deployment name="adobe-livecycle-native-jboss-x86_win32.ear" runtime-name="adobe-livecycle-native-jboss-x86_win32.ear"/>
       <deployment name="adobe-livecycle-native-jboss-x86_win64.ear" runtime-name="adobe-livecycle-native-jboss-x86_win64.ear"/>
       <deployment name="adobe-output-ivs-jboss.ear" runtime-name="adobe-output-ivs-jboss.ear"/>
       <deployment name="adobe-workspace-client.ear" runtime-name="adobe-workspace-client.ear"/>
   </deployments>
   ```

### 도메인 구성의 드라이버 클래스 업데이트 {#update-driver-class-in-domain-configuration}

1. 데이터베이스 엔진을 기반으로 `domain_<db>.xml`의 드라이버 클래스 섹션을 업데이트하십시오.

   **MSSQL:**

   ```xml
   <xa-datasource-class>com.microsoft.sqlserver.jdbc.SQLServerXADataSource</xa-datasource-class>
   ```

   **Oracle:**

   ```xml
   <xa-datasource-class>oracle.jdbc.xa.client.OracleXADataSource</xa-datasource-class>
   ```

### 슬레이브 노드에서 도메인 컨트롤러 업데이트 {#update-domain-controller-on-slave-nodes}

1. `host.xml`의 슬레이브 노드에서 마스터 IP 주소, 포트 `9999`, 사용자 이름 `slave1` 및 영역 `ManagementRealm`(으)로 도메인 컨트롤러 블록을 업데이트합니다.

   ```xml
   <remote host="<ip-address>" port="9999" username="slave1" realm="ManagementRealm"/>
   ```

### jboss-cli.xml 업데이트 {#update-jboss-cli-xml}

1. 마스터 노드와 슬레이브 노드 모두에서 `jboss-cli.xml`의 `<host>` 항목을 업데이트합니다.
