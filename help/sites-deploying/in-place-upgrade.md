---
title: 즉석 업그레이드 수행
seo-title: 즉석 업그레이드 수행
description: 직접 업그레이드를 수행하는 방법을 알아봅니다.
seo-description: 직접 업그레이드를 수행하는 방법을 알아봅니다.
uuid: 478cb9db-1ea8-4bdb-b333-411dcbf2d927
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: fcb17227-ff1f-4b47-ae94-6b7f60923876
docset: aem65
translation-type: tm+mt
source-git-commit: a8deb66b23e6ddde9c5f6379ef4f766668336369

---


# 즉석 업그레이드 수행{#performing-an-in-place-upgrade}

>[!NOTE]
>
>이 페이지에서는 AEM 6.5에 대한 업그레이드 절차에 대해 설명합니다.응용 프로그램 서버에 배포된 설치가 있는 경우 Application Server 설치에 [대한 업그레이드 단계를 참조하십시오](/help/sites-deploying/app-server-upgrade.md).

## 업그레이드 전 단계 {#pre-upgrade-steps}

업그레이드를 실행하기 전에 몇 가지 단계를 완료해야 합니다. 자세한 [내용은 코드 및 사용자](/help/sites-deploying/upgrading-code-and-customizations.md) 정의 업그레이드 [및](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) 업그레이드 전 유지 관리작업을참조하십시오. 또한 시스템이 새 버전의 AEM에 대한 요구 사항을 충족하는지 확인하십시오. Pattern Detector를 통해 업그레이드의 복잡성을 파악하는 방법을 살펴볼 수 있고 업그레이드 계획의 업그레이드 범위 및 요구 [사항 섹션을](/help/sites-deploying/upgrade-planning.md) 참조하십시오.

## 마이그레이션 사전 요구 사항 {#migration-prerequisites}

* **** 최소 필수 Java 버전:마이그레이션 도구는 Java 버전 7 이상에서만 작동합니다. AEM 6.3 이상 버전의 경우 Oracle의 JRE 8 및 IBM의 JRE 7 &amp; 8만 지원됩니다.

* **** 업그레이드된 인스턴스:5.6 **세**&#x200B;버전 이상에서 업그레이드하는 경우 업그레이드 설명서의 6.0 버전에 설명된 절차에 따라 AEM 6.0으로 직접 업그레이드를 수행했는지 확인하십시오.

## AEM Quickstart jar 파일 준비 {#prep-quickstart-file}

1. 인스턴스가 실행 중인 경우 인스턴스를 중지합니다.

1. 새 AEM jar 파일을 다운로드하고 이를 사용하여 `crx-quickstart` 폴더 외부에 있는 이전 파일을 바꿉니다.

1. 다음을 실행하여 새로운 빠른 시작 jar의 압축을 해제합니다.

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## 컨텐츠 저장소 마이그레이션 {#content-repository-migration}

AEM 6.3에서 업그레이드하는 경우에는 이 마이그레이션이 필요하지 않습니다.6.3 이전 버전의 경우 Adobe는 AEM 6.3에 있는 Oak 세그먼트 Tar의 새 버전으로 저장소를 마이그레이션하는 데 사용할 수 있는 도구를 제공합니다.Quickstart 패키지의 일부로 제공되며 TarMK를 사용할 모든 업그레이드에 대해 필수입니다. MongoMK를 사용하는 환경에 대한 업그레이드는 저장소 마이그레이션이 필요하지 않습니다. For more information on what the benefits of the new Segment Tar format are, see the [Migrating to Oak Segment Tar FAQ](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

실제 마이그레이션은 표준 AEM quickstart jar 파일을 사용하여 수행되며, 업그레이드를 단순화하고 더욱 강력해지기 위해 crx2oak 도구를 실행하는 새로운 `-x crx2oak` 옵션으로 실행됩니다.

>[!NOTE]
>
>CRX2Oak Quickstart 확장 기능을 사용하여 TarMK 저장소 컨텐츠 마이그레이션을 수행하는 경우 **마이그레이션 명령줄에 다음을 추가하여** samplecontent runmode를 제거할 수 있습니다.
>
>* `--promote-runmode nosamplecontent`
>



실행해야 하는 명령을 결정하려면 다음 명령을 사용합니다.

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

다음 표에 나열된 프로필 및 플래그로 `<<YOUR_PROFILE>>` `<<ADDITIONAL_FLAGS>>` 및 대체되는 위치:

<table>
 <tbody>
  <tr>
   <td><strong>소스 저장소</strong></td>
   <td><strong>타겟 저장소</strong></td>
   <td><strong>프로필</strong></td>
   <td><strong>추가 플래그</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2 또는 TarMK( <code>FileDataStore</code></td>
   <td>TarMK</td>
   <td>segment-fds</td>
   <td>아래의 문제 해결 섹션을 참조하십시오.</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>MongoMK</td>
   <td>mongo-from-crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>TarMK 또는 crx2 <code>S3DataStore</code></td>
   <td>TarMK</td>
   <td>segment-custom-ds</td>
   <td>아래의 문제 해결 섹션을 참조하십시오.</td>
  </tr>
  <tr>
   <td>데이터 저장소가 없는 TarMK</td>
   <td>TarMK</td>
   <td>segment-no-ds</td>
   <td> </td>
  </tr>
  <tr>
   <td>MongoMK</td>
   <td>MongoMK</td>
   <td>마이그레이션은 필요하지 않습니다.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**위치:**

* `mongo-host` 은 MongoDB 서버 IP(예: 127.0.0.1)입니다.

* `mongo-port` 는 MongoDB 서버 포트입니다(예:27017년)

* `mongo-database-name` 데이터베이스 이름을 나타냅니다(예:aem-author)

**다음 시나리오에 대해 추가 스위치가 필요할 수도 있습니다.**

* Java 메모리 매핑이 올바르게 처리되지 않는 Windows 시스템에서 업그레이드를 수행하는 경우 `--disable-mmap` 매개 변수를 명령에 추가하십시오.

* Java 7을 사용하는 경우 매개 변수 바로 뒤에 `-XX:MaxPermSize=2048m` 매개 변수를 추가합니다 `-Xmx` .

crx2oak 도구 사용에 대한 추가 지침은 CRX2Oak [마이그레이션 도구 사용을 참조하십시오](/help/sites-deploying/using-crx2oak.md). 필요한 경우 빠른 시작을 압축 해제한 후 새 버전으로 직접 교체하여 crx2oak 도우미 JAR를 수동으로 업그레이드할 수 있습니다. AEM 설치 폴더의 위치는 다음과 같습니다. `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`Adobe CRX2Oak 마이그레이션 도구의 최신 버전은 다음 Adobe Repository에서 다운로드할 수 있습니다. [https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/)

마이그레이션이 성공적으로 완료되면 종료 코드가 0인 상태로 도구가 종료됩니다. 또한 AEM 설치 디렉토리에 있는 `upgrade.log` 파일에서 WARN 및 ERROR 메시지를 확인합니다. 이 메시지는 마이그레이션 중에 발생한 치명적인 오류를 나타낼 수 `crx-quickstart/logs` 있습니다.

폴더 아래에서 구성 파일을 `crx-quickstart/install` 확인합니다. 마이그레이션이 필요한 경우 대상 저장소를 반영하도록 업데이트됩니다.

**데이터 저장소에 대한 참고 사항:**

AEM 6.3 설치에 대한 새로운 `FileDataStore` 기본값이지만 외부 데이터 저장소를 사용할 필요는 없습니다. 외부 데이터 저장소를 프로덕션 배포를 위한 우수 사례로 사용하는 것이 좋지만 반드시 업그레이드해야 하는 것은 아닙니다. AEM 업그레이드에 이미 복잡성이 있으므로 데이터 저장소 마이그레이션을 수행하지 않고 업그레이드를 수행하는 것이 좋습니다. 원하는 경우 데이터 저장소 마이그레이션은 별도의 노력으로 이후에 실행될 수 있습니다.

## 마이그레이션 문제 해결 {#troubleshooting-migration-issues}

6.3에서 업그레이드하는 경우 이 섹션을 건너뛰십시오.제공된 crx2oak 프로파일은 대부분의 고객의 요구 사항을 충족해야 하지만 추가 매개 변수가 필요할 때가 있습니다. 마이그레이션 중에 오류가 발생하는 경우 추가 구성 옵션을 제공해야 하는 환경 측면이 있을 수 있습니다. 이러한 경우 다음 오류가 발생할 수 있습니다.

**외부 데이터 저장소가 지정되지 않았으므로 체크포인트는 복사되지 않습니다. 이렇게 하면 첫 번째 시작 시 전체 저장소 다시 색인화가 만들어집니다. —skip-checkpoint를 사용하여 강제 마이그레이션을 수행하거나 자세한 내용은 https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration을 참조하십시오.**

어떤 이유로 마이그레이션 프로세스가 데이터 저장소의 바이너리에 액세스해야 하며 이를 찾을 수 없습니다. 데이터 저장소 구성을 지정하려면 마이그레이션 명령 `<<ADDITIONAL_FLAGS>>` 부분에 다음 플래그를 포함하십시오.

**S3 데이터 저장소의 경우:**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

여기서 `/path/to/SharedS3DataStore.config` 는 S3 데이터 저장소 구성 파일의 경로를 나타내며 S3 데이터 저장소의 경로를 `/path/to/datastore` 나타냅니다.

**파일 데이터 저장소의 경우:**

```shell
--src-datastore=/path/to/datastore
```

여기서 `/path/to/datastore` 파일 데이터 저장소의 경로를 나타냅니다.

## 업그레이드 수행 {#performing-the-upgrade}

**S3를 사용하는 경우:**

1. 이전 버전의 S3 커넥터와 `crx-quickstart/install` 연결된 항아리 아래에 있는 항아리를 제거합니다.

1. https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/에서 1.8.x S3 커넥터의 최신 릴리스를 [파섹](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)

1. 패키지를 임시 폴더에 추출하고 폴더의 컨텐츠를 `jcr_root/libs/system/install``crx-quickstart/install` 폴더에 복사합니다.

### 올바른 업그레이드 시작 명령 확인 {#determining-the-correct-upgrade-start-command}

업그레이드를 실행하려면 jar 파일을 사용하여 AEM을 시작하여 인스턴스를 불러와야 합니다. 6.5로 업그레이드하려면 업그레이드 명령을 사용하여 선택할 수 있는 [게으른](/help/sites-deploying/lazy-content-migration.md) 컨텐츠 마이그레이션의 다른 컨텐츠 재구성 및 마이그레이션 옵션을 참조하십시오.

시작 스크립트에서 AEM을 시작하면 업그레이드가 시작되지 않습니다. 대부분의 고객은 시작 스크립트를 사용하여 AEM을 시작하고 메모리 설정, 보안 인증서 등과 같은 환경 구성에 대한 스위치를 포함하도록 이 시작 스크립트를 사용자 지정했습니다. 따라서 적절한 업그레이드 명령을 결정하려면 다음 절차를 따르는 것이 좋습니다.

1. 실행 중인 AEM 인스턴스에서 명령줄에서 다음을 실행합니다.

   ```shell
   ps -ef | grep java
   ```

1. AEM 프로세스를 찾습니다. 다음과 같이 표시됩니다.

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.2.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. 기존 jar( `crx-quickstart/app/aem-quickstart*.jar` 이 경우)의 경로를 폴더의 동위 항목인 새 jar로 대체하여 명령을 수정합니다 `crx-quickstart` . 이전 명령을 예로 사용하면 다음과 같은 명령을 사용할 수 있습니다.

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   이렇게 하면 모든 적절한 메모리 설정, 사용자 정의 런타임 및 기타 환경 매개 변수가 업그레이드를 위해 적용됩니다. 업그레이드가 완료된 후, 인스턴스는 향후 시작 시 초기 스크립트에서 시작할 수 있습니다.

## 업그레이드된 코드베이스 배포 {#deploy-upgraded-codebase}

업그레이드 절차가 완료되면 업데이트된 코드 베이스를 배포해야 합니다. AEM의 대상 버전에서 작동하도록 코드 베이스를 업데이트하는 단계는 업그레이드 코드 및 사용자 지정 [페이지에서](/help/sites-deploying/upgrading-code-and-customizations.md)찾을 수 있습니다.

## 업그레이드 후 확인 및 문제 해결 수행 {#perform-post-upgrade-check-troubleshooting}

업그레이드 [후 확인 및 문제 해결을 참조하십시오](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
