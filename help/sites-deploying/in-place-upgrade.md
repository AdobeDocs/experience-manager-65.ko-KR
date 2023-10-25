---
title: 즉석 업그레이드 수행
description: AEM 6.5용 즉각적 업그레이드를 수행하는 방법을 알아봅니다.
topic-tags: upgrading
feature: Upgrading
exl-id: aef6ef00-993c-4252-b0ad-ddc4917beaf7
source-git-commit: e54c1d422f2bf676e8a7b0f50a101e495c869c96
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 0%

---

# 즉석 업그레이드 수행{#performing-an-in-place-upgrade}

>[!NOTE]
>
>이 페이지에서는 AEM 6.5의 업그레이드 절차에 대해 간략히 설명합니다. 응용 프로그램 서버에 배포된 설치가 있는 경우 다음을 참조하십시오 [Application Server 설치 업그레이드 단계](/help/sites-deploying/app-server-upgrade.md).

## 업그레이드 전 단계 {#pre-upgrade-steps}

업그레이드를 실행하기 전에 완료해야 하는 몇 가지 단계가 있습니다. 다음을 참조하십시오 [코드 및 사용자 지정 업그레이드](/help/sites-deploying/upgrading-code-and-customizations.md) 및 [업그레이드 전 유지 관리 작업](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) 추가 정보. 또한 시스템이 새 AEM 버전에 대한 요구 사항을 충족하는지 확인하십시오. 패턴 감지기를 통해 업그레이드의 복잡성을 추정하는 방법을 확인하고 의 업그레이드 범위 및 요구 사항 섹션을 참조하십시오. [업그레이드 계획](/help/sites-deploying/upgrade-planning.md) 추가 정보.

<!--Finally, note that the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## 마이그레이션 사전 요구 사항 {#migration-prerequisites}

* **필요한 최소 Java 버전:** 마이그레이션 도구는 Java 버전 7 이상에서만 작동합니다. AEM 6.3 이상의 경우 Oracle의 JRE 8 및 IBM의 JRE 7 및 8만 지원됩니다.

* **업그레이드된 인스턴스:** 버전에서 업그레이드하는 경우 **5.6세 이상**&#x200B;를 설치한 후 업그레이드 설명서의 6.0 버전에 설명된 절차에 따라 AEM 6.0으로 바로 업그레이드를 수행했는지 확인하십시오.

## AEM Quickstart jar 파일 준비 {#prep-quickstart-file}

1. 실행 중인 경우 인스턴스를 중지합니다.

1. 새 AEM jar 파일을 다운로드하고 이 파일을 사용하여 `crx-quickstart` 폴더를 삭제합니다.

1. 다음을 실행하여 새 quickstart jar 압축을 해제합니다.

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## 콘텐츠 저장소 마이그레이션 {#content-repository-migration}

AEM 6.3에서 업그레이드하는 경우 이 마이그레이션이 필요하지 않습니다. 6.3 이전 버전의 경우, Adobe은 AEM 6.3에 있는 Oak Segment Tar의 새 버전으로 저장소를 마이그레이션하는 데 사용할 수 있는 도구를 제공합니다. 빠른 시작 패키지의 일부로 제공되며 TarMK를 사용할 업그레이드에 필수입니다. MongoMK를 사용하는 환경의 업그레이드에는 저장소 마이그레이션이 필요하지 않습니다. 새 세그먼트 Tar 형식의 이점에 대한 자세한 내용은 [Oak 세그먼트 Tar로 마이그레이션 FAQ](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

실제 마이그레이션은 새 파일과 함께 실행되는 표준 AEM quickstart jar 파일을 사용하여 수행됩니다. `-x crx2oak` 업그레이드를 단순화하고 보다 강력하게 만들기 위해 crx2oak 도구를 실행하는 옵션입니다.

>[!NOTE]
>
>CRX2Oak Quickstart 확장을 사용하여 TarMK 저장소 콘텐츠 마이그레이션을 수행하는 경우 **samplecontent** migration 명령줄에 다음을 추가하여 실행 모드:
>
>* `--promote-runmode nosamplecontent`
>

실행할 명령을 확인하려면 다음 명령을 사용합니다.

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

위치 `<<YOUR_PROFILE>>` 및 `<<ADDITIONAL_FLAGS>>` 은 다음 표에 나열된 프로필 및 플래그로 대체됩니다.

<table>
 <tbody>
  <tr>
   <td><strong>소스 저장소</strong></td>
   <td><strong>대상 저장소</strong></td>
   <td><strong>프로필</strong></td>
   <td><strong>추가 플래그</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2 또는 TarMK 포함 <code>FileDataStore</code></td>
   <td>TarMk</td>
   <td>segment-fds</td>
   <td>아래의 문제 해결 섹션을 참조하십시오.</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>몽고</td>
   <td>mongo-from-crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>TarMK 또는 crx2 포함 <code>S3DataStore</code></td>
   <td>TarMk</td>
   <td>segment-custom-ds</td>
   <td>아래의 문제 해결 섹션을 참조하십시오.</td>
  </tr>
  <tr>
   <td>데이터 저장소가 없는 TarMK</td>
   <td>TarMk</td>
   <td>segment-no-ds</td>
   <td> </td>
  </tr>
  <tr>
   <td>몽고</td>
   <td>몽고</td>
   <td>마이그레이션이 필요하지 않음</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**위치:**

* `mongo-host` 는 MongoDB 서버 IP입니다(예: 127.0.0.1).

* `mongo-port` 는 MongoDB 서버 포트입니다(예: 27017).

* `mongo-database-name` 데이터베이스 이름을 나타냅니다(예: aem-author).

**또한 다음과 같은 경우 추가 스위치가 필요할 수 있습니다.**

* Java 메모리 매핑이 올바르게 처리되지 않는 Windows 시스템에서 업그레이드를 수행하는 경우 `--disable-mmap` 매개 변수를 명령에 추가합니다.

crx2oak 도구 사용에 대한 추가 지침은 [CRX2Oak 마이그레이션 도구](/help/sites-deploying/using-crx2oak.md). crx2oak helper JAR은 필요한 경우 빠른 시작을 언포장한 후 수동으로 최신 버전으로 교체하여 수동으로 업그레이드할 수 있습니다. AEM 설치 폴더의 위치는 다음과 같습니다. `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. CRX2Oak 마이그레이션 도구의 최신 버전은 다음 Adobe 저장소에서 다운로드할 수 있습니다. [https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

마이그레이션이 성공적으로 완료되면 종료 코드가 0인 상태로 도구가 종료됩니다. 또한 WARN 및 ERROR 메시지를에서 확인합니다. `upgrade.log` 파일, 위치: `crx-quickstart/logs` AEM 설치 디렉토리에서 마이그레이션 중에 발생한 심각하지 않은 오류를 나타낼 수 있습니다.

아래에서 구성 파일 확인 `crx-quickstart/install` 폴더를 삭제합니다. 마이그레이션이 필요한 경우 대상 저장소를 반영하도록 업데이트됩니다.

**데이터 저장소에 대한 참고 사항:**

While `FileDataStore` 외부 데이터 저장소를 사용할 필요가 없으므로 AEM 6.3 설치에 대한 새로운 기본값입니다. 프로덕션 배포에 외부 데이터 저장소를 사용하는 것이 모범 사례로 권장되지만 업그레이드하기 위한 필수 조건은 아닙니다. AEM Adobe 업그레이드에 이미 존재하는 복잡성으로 인해 데이터 저장소 마이그레이션을 수행하지 않고 업그레이드를 수행하는 것이 좋습니다. 원하는 경우 나중에 별도의 작업으로 데이터 저장소 마이그레이션을 실행할 수 있습니다.

## 마이그레이션 문제 해결 {#troubleshooting-migration-issues}

6.3에서 업그레이드하는 경우 이 섹션을 건너뛰십시오. 제공된 crx2oak 프로필은 대부분의 고객의 요구를 충족해야 하지만, 추가 매개 변수가 필요한 경우가 있습니다. 마이그레이션 중에 오류가 발생하는 경우 추가 구성 옵션을 제공해야 하는 환경 측면이 있을 수 있습니다. 이 경우 다음 오류가 발생할 수 있습니다.

**외부 데이터 저장소가 지정되지 않았으므로 체크포인트가 복사되지 않습니다. 이렇게 하면 첫 번째 시작 시 전체 저장소가 리인덱싱됩니다. 사용 —체크포인트를 건너뛰어 마이그레이션을 강제로 수행하거나 https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration에서 자세한 내용을 확인하십시오.**

일부 이유로 마이그레이션 프로세스는 데이터 저장소의 바이너리에 액세스해야 하며 해당 바이너리를 찾을 수 없습니다. 데이터 저장소 구성을 지정하려면 다음 플래그를 `<<ADDITIONAL_FLAGS>>` 마이그레이션 명령의 일부:

**S3 데이터 저장소의 경우:**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

위치 `/path/to/SharedS3DataStore.config` 는 S3 데이터 저장소 구성 파일의 경로를 나타내고 `/path/to/datastore` 는 S3 데이터 저장소의 경로를 나타냅니다.

**파일 데이터 저장소의 경우:**

```shell
--src-datastore=/path/to/datastore
```

위치 `/path/to/datastore` 는 파일 데이터 저장소의 경로를 나타냅니다.

## 업그레이드 수행 {#performing-the-upgrade}

**S3를 사용하는 경우:**

1. 아래의 jar 제거 `crx-quickstart/install` 이전 버전의 S3 커넥터와 연결됩니다.

1. 에서 1.10.x S3 커넥터의 최신 릴리스를 다운로드합니다. [https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/)

1. 패키지를 임시 폴더로 추출하고 콘텐츠를 복사합니다. `jcr_root/libs/system/install` (으)로 `crx-quickstart/install` 폴더를 삭제합니다.

### 올바른 업그레이드 시작 명령 확인 {#determining-the-correct-upgrade-start-command}

업그레이드를 실행하려면 jar 파일을 사용하여 AEM을 시작하여 인스턴스를 불러오는 것이 중요합니다. 6.5로 업그레이드하려면에 있는 기타 콘텐츠 재구성 및 마이그레이션 옵션을 참조하십시오. [소극적 컨텐츠 마이그레이션](/help/sites-deploying/lazy-content-migration.md) 업그레이드 명령으로 선택할 수 있습니다.

>[!IMPORTANT]
>
>oracle Java 11(또는 일반적으로 Java 8보다 최신 버전)을 실행하는 경우 AEM을 시작할 때 명령줄에 스위치를 추가해야 합니다. 자세한 내용은 [Java 11 고려 사항](/help/sites-deploying/custom-standalone-install.md#java-considerations).

시작 스크립트에서 AEM을 시작하면 업그레이드가 시작되지 않습니다. 대부분의 고객은 시작 스크립트를 사용하여 AEM을 시작하고 메모리 설정, 보안 인증서 등과 같은 환경 구성을 위한 스위치를 포함하도록 이 시작 스크립트를 사용자 정의했습니다. 이러한 이유로 Adobe은 다음 절차에 따라 적절한 업그레이드 명령을 결정할 것을 권장합니다.

1. 실행 중인 AEM 인스턴스에서 명령줄에서 다음을 실행합니다.

   ```shell
   ps -ef | grep java
   ```

1. AEM 프로세스를 찾습니다. 다음과 같이 표시됩니다.

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.5.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. 기존 jar( )로 경로를 대체하여 명령을 수정합니다. `crx-quickstart/app/aem-quickstart*.jar` 이 경우) 의 형제 항목인 새 jar `crx-quickstart` 폴더를 삭제합니다. 이전 명령을 예로 들면 다음과 같습니다.

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   이렇게 하면 모든 적절한 메모리 설정, 사용자 지정 실행 모드 및 기타 환경 매개 변수가 업그레이드에 적용됩니다. 업그레이드가 완료되면 이후 시작의 시작 스크립트에서 인스턴스를 시작할 수 있습니다.

## 업그레이드된 코드베이스 배포 {#deploy-upgraded-codebase}

즉각적 업그레이드 프로세스가 완료되면 업데이트된 코드 베이스를 배포해야 합니다. AEM의 대상 버전에서 작동하도록 코드 베이스를 업데이트하는 단계는 에서 찾을 수 있습니다. [코드 및 사용자 지정 업그레이드 페이지](/help/sites-deploying/upgrading-code-and-customizations.md).

## 업그레이드 후 확인 및 문제 해결 수행 {#perform-post-upgrade-check-troubleshooting}

다음을 참조하십시오 [업그레이드 후 확인 및 문제 해결](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
