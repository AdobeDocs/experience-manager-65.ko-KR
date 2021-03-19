---
title: 업그레이드 전 유지 관리 작업
seo-title: 업그레이드 전 유지 관리 작업
description: AEM의 사전 업그레이드 작업에 대해 알아봅니다.
seo-description: AEM의 사전 업그레이드 작업에 대해 알아봅니다.
uuid: 5da1cfc7-8a10-47b1-aafb-2cd112e3f818
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 291c91e5-65ff-473d-ac11-3da480239e76
docset: aem65
feature: 업그레이드
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2159'
ht-degree: 0%

---


# 업그레이드 전 유지 관리 작업{#pre-upgrade-maintenance-tasks}

업그레이드를 시작하기 전에 다음과 같은 유지 관리 작업을 수행하여 시스템이 준비되고 문제가 발생하면 롤백할 수 있도록 해야 합니다.

* [충분한 디스크 공간 확인](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [AEM 전체 백업](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [/etc에 변경 내용 백업](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#backup-changes-etc)
* [quickstart.properties 파일 생성](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [워크플로우 구성 및 감사 로그 삭제](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [업그레이드 전 작업 설치, 구성 및 실행](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [사용자 정의 로그인 모듈 비활성화](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [/install 디렉토리에서 업데이트 제거](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [모든 콜드 대기 인스턴스 중지](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [사용자 지정 예약 작업 비활성화](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [오프라인 개정 정리 실행](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [데이터 저장소 가비지 수집 실행](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [필요한 경우 데이터베이스 스키마 업그레이드](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [업그레이드에 방해가 될 수 있는 사용자 삭제](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [로그 파일 회전](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## 충분한 디스크 공간 {#ensure-sufficient-disk-space} 확인

업그레이드를 실행할 때 컨텐츠 및 코드 업그레이드 활동 외에도 저장소 마이그레이션을 수행해야 합니다. 마이그레이션은 새 Segment Tar 형식으로 저장소의 사본을 만듭니다. 따라서 저장소 버전을 저장할 수 있는 디스크 공간이 충분해야 합니다.

## AEM {#fully-back-up-aem} 전체 백업

업그레이드를 시작하기 전에 AEM을 완전히 백업해야 합니다. 해당하는 경우 저장소, 응용 프로그램 설치, 데이터 저장소 및 Mongo 인스턴스를 백업하십시오. AEM 인스턴스 백업 및 복원에 대한 자세한 내용은 [백업 및 복원](/help/sites-administering/backup-and-restore.md)을 참조하십시오.

## /etc {#backup-changes-etc}에 대한 변경 사항 백업

업그레이드 프로세스는 저장소의 `/apps` 및 `/libs` 경로에서 기존 컨텐츠와 구성을 유지 관리하고 병합하는 데 유용합니다. Context Hub 구성을 포함하여 `/etc` 경로에 대한 변경 사항은 업그레이드 후 이러한 변경 사항을 다시 적용해야 하는 경우가 많습니다. 업그레이드는 `/var` 아래에서 병합할 수 없는 모든 변경 내용의 백업 복사본을 만들지만 업그레이드를 시작하기 전에 이러한 변경 내용을 수동으로 백업하는 것이 좋습니다.

## quickstart.properties 파일 {#generate-quickstart-properties} 생성

jar 파일에서 AEM을 시작하면 `quickstart.properties` 파일이 `crx-quickstart/conf` 아래에 생성됩니다. 이전에 시작 스크립트로만 AEM을 시작한 경우 이 파일이 제공되지 않으며 업그레이드가 실패합니다. 이 파일이 있는지 확인하고 jar 파일이 없으면 AEM을 jar 파일에서 다시 시작합니다.

## 워크플로 구성 및 감사 로그 제거 {#configure-wf-audit-purging}

`WorkflowPurgeTask` 및 `com.day.cq.audit.impl.AuditLogMaintenanceTask` 작업은 별도의 OSGi 구성이 필요하며 이 구성 요소가 없으면 작동하지 않습니다. 업그레이드 전 작업 실행 중에 오류가 발생하면 구성이 누락될 가능성이 높습니다. 따라서 이러한 작업을 실행하려면 반드시 OSGi 구성을 추가하거나 업그레이드 전 최적화 작업 목록에서 모두 제거해야 합니다. 워크플로우 제거 작업을 구성하는 설명서는 [워크플로우 인스턴스 관리](/help/sites-administering/workflows-administering.md)에서 찾을 수 있으며 감사 로그 유지 관리 작업 구성은 AEM 6](/help/sites-administering/operations-audit-log.md)의 감사 로그 유지 관리에서 확인할 수 있습니다.[

AEM 6.0의 감사 로그 제거와 CQ 5.6의 워크플로우 및 감사 로그 제거에 대해서는 [워크플로우 및 감사 노드 삭제](https://helpx.adobe.com/experience-manager/kb/howtopurgewf.html)를 참조하십시오.

## 업그레이드 전 작업 설치, 구성 및 실행 {#install-configure-run-pre-upgrade-tasks}

AEM의 사용자 정의 수준 때문에 일반적으로 환경에서는 업그레이드를 수행하는 동일한 방법을 사용하지 않습니다. 따라서 업그레이드를 위한 표준 절차를 만드는 것은 어려운 일입니다.

이전 버전에서는 AEM 업그레이드가 중단되거나 안전하게 다시 시작되지 않은 경우에도 문제가 있었습니다. 이로 인해 전체 업그레이드 절차를 다시 시작할 필요가 있거나 경고하지 않고 결함이 있는 업그레이드를 수행한 경우가 발생했습니다.

이러한 문제를 해결하기 위해 Adobe은 업그레이드 프로세스에 몇 가지 향상된 기능을 추가함으로써 보다 탄력적이고 사용자에게 익숙해질 수 있습니다. 수동으로 수행해야 했던 사전 업그레이드 유지 관리 작업은 최적화 및 자동화되었습니다. 또한 업그레이드 후 보고서가 추가되어 모든 문제가 보다 쉽게 발견될 수 있도록 프로세스를 철저히 조사할 수 있습니다.

업그레이드 전 유지 관리 작업은 현재 부분적으로 수동으로 또는 완전히 수행되는 다양한 인터페이스에 분산되어 있습니다. AEM 6.3에 도입된 사전 업그레이드 유지 관리 최적화를 통해 이러한 작업을 트리거할 수 있고 On-Demand 방식으로 결과를 검사할 수 있습니다.

업그레이드 전 최적화 단계에 포함된 모든 작업은 AEM 6.0 이상 버전의 모든 버전과 호환됩니다.

### {#how-to-set-it-up} 설정 방법

AEM 6.3 이상에서 업그레이드 전 유지 관리 최적화 작업은 quickstart jar에 포함됩니다. 이전 버전의 AEM 6에서 업그레이드하는 경우 패키지 관리자에서 다운로드할 수 있는 개별 패키지를 통해 사용할 수 있습니다.

다음 위치에서 패키지를 찾을 수 있습니다.

* [AEM 6.0에서 업그레이드하는 경우](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [AEM 6.1에서 업그레이드하는 경우](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [AEM 6.2에서 업그레이드하는 경우](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62)

### 사용 방법 {#how-to-use-it}

`PreUpgradeTasksMBean` OSGI 구성 요소는 한 번에 모두 실행할 수 있는 업그레이드 전 유지 관리 작업 목록과 함께 미리 구성되어 있습니다. 아래 절차에 따라 작업을 구성할 수 있습니다.

1. *https://serveraddress:serverport/system/console/configMgr*&#x200B;로 이동하여 웹 콘솔로 이동합니다.

1. &quot;**preupgradetasks**&quot;를 검색한 다음 일치하는 첫 번째 구성 요소를 클릭합니다. 구성 요소의 전체 이름은 `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`입니다.

1. 아래와 같이 실행해야 하는 유지 관리 작업 목록을 수정합니다.

   ![1487758925984](assets/1487758925984.png)

작업 목록은 인스턴스를 시작하는 데 사용되는 실행 모드에 따라 다릅니다. 다음은 각 유지 관리 작업이 설계된 실행 모드에 대한 설명입니다.

<table>
 <tbody>
  <tr>
   <td><strong>작업</strong></td>
   <td><strong>실행 모드</strong></td>
   <td><strong>메모</strong></td>
  </tr>
  <tr>
   <td><code>TarIndexMergeTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>DataStoreGarbageCollectionTask</code></td>
   <td>crx2</td>
   <td>마크와 소름 돋을 거야 공유 데이터 저장소의 경우 이 단계를 제거하고 실행 전에 <br />을(를) 수동으로 또는 적절하게 인스턴스를 준비하십시오.</td>
  </tr>
  <tr>
   <td><code>ConsistencyCheckTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>WorkflowPurgeTask</code></td>
   <td>crx2/crx3</td>
   <td>실행하기 전에 Adobe Granite Workflow Purge Configuration OSGi를 구성해야 합니다.</td>
  </tr>
  <tr>
   <td><code>GenerateBundlesListFileTask</code></td>
   <td>crx2/crx3</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>RevisionCleanupTask</code></td>
   <td>crx3</td>
   <td>AEM 6.0에서 6.2까지의 TarMK 인스턴스의 경우 오프라인 개정 정리를 대신 수동으로 실행하십시오.</td>
  </tr>
  <tr>
   <td><code>com.day.cq.audit.impl.AuditLogMaintenanceTask</code></td>
   <td>crx3</td>
   <td>실행 전에 감사 로그 삭제 스케줄러 OSGi 구성을 구성해야 합니다.</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>`DataStoreGarbageCollectionTask` 이 사용 시 표시 및 쓸개 단계에서 데이터 저장소 가비지 수집 작업을 호출하는 중입니다. 공유 데이터 저장소를 사용하는 배포의 경우 해당 항목을 다시 구성하거나 제대로 준비하거나 다른 인스턴스에서 참조하는 항목이 삭제되지 않도록 인스턴스를 준비해야 합니다. 이 사전 업그레이드 작업을 트리거하기 전에 모든 인스턴스에서 표시 단계를 수동으로 실행해야 할 수 있습니다.

### 업그레이드 전 상태 검사의 기본 구성 {#default-configuration-of-the-pre-upgrade-health-checks}

`PreUpgradeTasksMBeanImpl` OSGI 구성 요소는 `runAllPreUpgradeHealthChecks` 메서드가 호출될 때 실행하기 위해 업그레이드 전 상태 확인 태그 목록으로 사전 구성되어 있습니다.

* **system**  - granite maintenance checks에 사용되는 태그

* **업그레이드**  전 - 업그레이드 전에 실행하도록 설정할 수 있는 모든 상태 검사에 추가할 수 있는 사용자 지정 태그입니다.

목록을 편집할 수 있습니다. 태그 외에 더하기 **(+)** 및 빼기 **(-)** 단추를 사용하여 사용자 정의 태그를 더 추가하거나 기본 태그를 제거할 수 있습니다.

**MBean 메서드**

관리되는 빈 기능은 [JMX 콘솔](/help/sites-administering/jmx-console.md)을 사용하여 액세스할 수 있습니다.

다음을 통해 MBean에 액세스할 수 있습니다.

1. *https://serveraddress:serverport/system/console/jmx*&#x200B;의 JMX 콘솔로 이동
1. **PreUpgradeTasks**&#x200B;를 검색하고 결과를 클릭합니다.

1. **작업** 섹션에서 원하는 메서드를 선택하고 다음 창에서 **호출**&#x200B;을 선택합니다.

다음은 `PreUpgradeTasksMBeanImpl`에서 제공하는 사용 가능한 모든 메서드 목록입니다.

<table>
 <tbody>
  <tr>
   <td><strong>메서드 이름</strong></td>
   <td><strong>유형</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeTasksNames()</code></td>
   <td>정보</td>
   <td>사용 가능한 사전 업그레이드 유지 관리 작업 이름 목록을 표시합니다.</td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeHealthChecksTagNames()</code></td>
   <td>정보</td>
   <td>업그레이드 전 상태 검사 태그 이름 목록을 표시합니다.</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeTasks()</code></td>
   <td>작업</td>
   <td>목록에서 모든 업그레이드 전 유지 관리 작업을 실행합니다.</td>
  </tr>
  <tr>
   <td><code>runPreUpgradeTask(preUpgradeTaskName)</code></td>
   <td>작업</td>
   <td>매개 변수로 지정된 이름으로 업그레이드 전 유지 관리 작업을 실행합니다.</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td><code>runAllPreUpgradeTasksmaintenance</code> 작업이 현재 실행 중인지 확인합니다.</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>업그레이드 전 유지 관리 작업이 현재 실행 중인지 확인하고 <br /> 현재 실행 중인 작업의 이름이 포함된 배열을 반환합니다.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunTime(preUpgradeTaskName)</code></td>
   <td>작업</td>
   <td>업그레이드 전 유지 관리 작업의 정확한 실행 시간을 매개 변수로 지정된 이름으로 표시합니다.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunState(preUpgradeTaskName)</code></td>
   <td>작업</td>
   <td>업그레이드 전 유지 관리 작업의 마지막 실행 상태를 매개 변수로 지정된 이름으로 표시합니다.</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeHealthChecks(shutDownOnSuccess)</code></td>
   <td>작업</td>
   <td><p>모든 사전 업그레이드 상태 검사를 실행하고 상태 상태를 sling 홈 경로에 있는 <code>preUpgradeHCStatus.properties</code> 파일에 저장합니다. <code>shutDownOnSuccess</code> 매개 변수가 <code>true</code>으로 설정된 경우 AEM 인스턴스가 종료되지만 모든 업그레이드 전 상태 검사가 OK 상태인 경우에만 인스턴스가 종료됩니다.</p> <p>속성 파일은 향후 업그레이드에 대한 전제 조건으로 사용됩니다<br />. 업그레이드 전 상태 확인<br /> 실행에 실패하면 업그레이드 프로세스가 중지됩니다. 업그레이드 전 상태 검사 결과를 무시하고 업그레이드를 시작하려는 경우 파일을 삭제할 수 있습니다.<br /></p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>작업</td>
   <td>지정된 AEM 버전으로 업그레이드할 때 더 이상 만족하지 않는 가져온 모든 패키지를 나열합니다. <br /> 대상 AEM 버전은 매개 변수로 <br />이어야 합니다.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>MBean 메서드는 다음을 통해 호출할 수 있습니다.
>
>* JMX 콘솔
>* JMX에 연결하는 모든 외부 응용 프로그램
>* cURL

>



## 사용자 정의 로그인 모듈 비활성화 {#disable-custom-login-modules}

>[!NOTE]
>
>이 단계는 AEM 5 버전에서 업그레이드하는 경우에만 필요합니다. 이전 AEM 6 버전에서 업그레이드하려면 이 항목을 완전히 건너뛸 수 있습니다.

사용자 지정 `LoginModules`이(가) 저장소 수준에서 인증을 위해 구성되는 방식은 Apache Oak에서 기본적으로 변경되었습니다.

CRX2 구성을 사용한 AEM 버전에서는 `repository.xml` 파일에 배치되고 AEM 6부터는 웹 콘솔을 통해 Apache Felix JAAS Configuration Factory 서비스에서 수행됩니다.

따라서 업그레이드 후 Apache Oak에 대해 기존 구성을 비활성화하고 다시 만들어야 합니다.

다음 예제와 같이 `repository.xml`의 JAS 구성에 정의된 사용자 지정 모듈을 비활성화하려면 기본 `LoginModule`을 사용하도록 구성을 수정해야 합니다.

```xml
<Security >
             ....
          <!--
                 Use LoginModule authenticating against repository itself
                 -->
                 <LoginModule class = "com.day.crx.core.CRXLoginModule" >
                     <param name = "anonymousId" value = "anonymous" />
                     <param name = "adminId" value ="admin" />
                     <param name = "disableNTLMAuth" value = "true" />
                     <param name = "tokenExpiration" value = "43200000" />
                     <!-- param name="trust_credentials_attribute" value="d5b9167e95dad6e7d3b5d6fa8df48af8"/
                -->
                 </LoginModule >
         </ Security>
```

>[!NOTE]
>
>자세한 내용은 [외부 로그인 모듈 사용 인증](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)을 참조하십시오.
>
>AEM 6의 `LoginModule` 구성 예를 보려면 [AEM 6](/help/sites-administering/ldap-config.md)에서 LDAP 구성을 참조하십시오.

## /install 디렉토리 {#remove-updates-install-directory}에서 업데이트 제거

>[!NOTE]
>
>AEM 인스턴스를 종료한 후 crx-quickstart/install 디렉토리에서 패키지만 제거합니다. 이 단계는 사내 업그레이드 절차를 시작하기 전의 마지막 단계 중 하나입니다.

로컬 파일 시스템의 `crx-quickstart/install` 디렉토리를 통해 배포된 서비스 팩, 기능 팩 또는 핫픽스를 제거합니다. 따라서 업데이트가 완료된 후 새 AEM 버전 위에 이전 핫픽스 및 서비스 팩을 실수로 설치하지 못하게 됩니다.

## 모든 콜드 대기 인스턴스 중지 {#stop-tarmk-coldstandby-instance}

TarMK cold standby를 사용하는 경우 모든 cold standby 인스턴스를 중지합니다. 업그레이드 시 문제가 발생할 경우 온라인으로 다시 연결하는 효율적인 방법이 보장됩니다. 업그레이드가 성공적으로 완료되면 업그레이드된 기본 인스턴스에서 콜드 대기 인스턴스를 다시 빌드해야 합니다.

## 사용자 지정 예약 작업 비활성화 {#disable-custom-scheduled-jobs}

응용 프로그램 코드에 포함된 모든 OSGi 예약 작업을 비활성화합니다.

## 오프라인 개정 정리 실행 {#execute-offline-revision-cleanup}

>[!NOTE]
>
>이 단계는 TarMK 설치에 대해서만 필요합니다.

TarMK를 사용하는 경우 업그레이드하기 전에 오프라인 개정 정리를 실행해야 합니다. 이렇게 하면 저장소 마이그레이션 단계 및 후속 업그레이드 작업이 훨씬 더 빨리 실행되고 업그레이드가 완료된 후 온라인 개정 정리를 성공적으로 실행할 수 있습니다. 오프라인 개정 정리 실행에 대한 자세한 내용은 [오프라인 개정 정리 수행](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup)을 참조하십시오.

## 데이터 저장소 가비지 컬렉션 실행 {#execute-datastore-garbage-collection}

>[!NOTE]
>
>이 단계는 crx3를 실행하는 인스턴스에만 필요합니다.

CRX3 인스턴스에서 개정 정리를 실행한 후 데이터 저장소에서 참조되지 않은 부분을 제거하려면 데이터 저장소 가비지 컬렉션을 실행해야 합니다. 지침은 [데이터 저장소 가비지 컬렉션](/help/sites-administering/data-store-garbage-collection.md)의 설명서를 참조하십시오.

## 필요한 경우 데이터베이스 스키마 업그레이드 {#upgrade-the-database-schema-if-needed}

일반적으로 지속성을 위해 기본 Apache Oak 스택 AEM에서 사용하는 경우 필요한 경우 데이터베이스 스키마를 업그레이드합니다.

그러나 스키마를 자동으로 업그레이드할 수 없을 때 경우도 발생합니다. 이러한 환경은 매우 제한된 권한이 있는 사용자 아래에서 데이터베이스가 실행되고 있는 높은 보안 환경입니다. 이 경우 AEM에서는 이전 스키마를 계속 사용합니다.

이러한 문제가 발생하지 않도록 하려면 아래 절차에 따라 스키마를 업그레이드해야 합니다.

1. 업그레이드해야 하는 AEM 인스턴스를 종료합니다.
1. 데이터베이스 스키마를 업그레이드합니다. 이를 수행하려면 데이터베이스 유형에 대한 설명서를 참조하십시오.

   Oak가 스키마 업그레이드를 처리하는 방법에 대한 자세한 내용은 Apache 웹 사이트](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade)의 [이 페이지를 참조하십시오.

1. AEM 업그레이드를 계속 진행하십시오.

## {#delete-users-that-might-hinder-the-upgrade} 업그레이드에 방해가 될 수 있는 사용자 삭제

>[!NOTE]
>
>이 업그레이드 전 유지 관리 작업은 다음 경우에만 필요합니다.
>
>* AEM 6.3보다 오래된 AEM 버전에서 업그레이드하고 있습니다.
>* 업그레이드 중에 아래에 언급된 오류가 발생합니다.

>



서비스 사용자가 일반 사용자로 부적절하게 태그 지정된 이전 AEM 버전으로 끝날 수 있는 예외적인 경우도 있습니다.

이러한 경우 다음과 같은 메시지가 표시되므로 업그레이드가 실패합니다.

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

이 문제를 해결하려면 다음을 수행하십시오.

1. 프로덕션 트래픽에서 인스턴스 분리
1. 문제를 일으키는 사용자의 백업을 만듭니다. 이 작업은 패키지 관리자를 통해 수행할 수 있습니다. 자세한 내용은 [패키지를 사용한 작업 방법을 참조하십시오.](/help/sites-administering/package-manager.md)
1. 문제를 일으키는 사용자를 삭제합니다. 다음은 이 카테고리에 속하는 사용자 목록입니다.

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## 로그 파일 회전 {#rotate-log-files}

업그레이드를 시작하기 전에 현재 로그 파일을 보관하는 것이 좋습니다. 이렇게 하면 업그레이드 도중 및 업그레이드 후 로그 파일을 보다 손쉽게 모니터링하고 스캔하여 발생할 수 있는 모든 문제를 식별하고 해결할 수 있습니다.
