---
title: 애플리케이션 서버 설치 업그레이드 단계
seo-title: 애플리케이션 서버 설치 업그레이드 단계
description: 애플리케이션 서버를 통해 배포된 AEM 인스턴스를 업그레이드하는 방법을 알아봅니다.
seo-description: 애플리케이션 서버를 통해 배포된 AEM 인스턴스를 업그레이드하는 방법을 알아봅니다.
uuid: e4020966-737c-40ea-bfaa-c63ab9a29cee
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 1876d8d6-bffa-4a1c-99c0-f6001acea825
docset: aem65
translation-type: tm+mt
source-git-commit: 38ef8fc8d80009c8ca79aca9e45cf10bd70e1f1e

---


# 애플리케이션 서버 설치 업그레이드 단계{#upgrade-steps-for-application-server-installations}

이 섹션에서는 Application Server용 AEM을 업데이트하기 위해 수행해야 하는 절차에 대해 설명합니다.

이 절차의 모든 예는 JBoss를 응용 프로그램 서버로 사용하며, 이미 배포된 AEM의 작업 버전이 있음을 나타냅니다. 이 절차는 AEM 버전 5.6에서 **6.3으로**&#x200B;수행된 문서 업그레이드를 위한 것입니다.

1. 먼저 JBoss를 시작합니다. 대부분의 경우 터미널에서 이 명령을 실행하여 `standalone.sh` 시작 스크립트를 실행하면 됩니다.

   ```shell
   jboss-install-folder/bin/standalone.sh
   ```

1. AEM 5.6이 이미 배포된 경우 다음을 실행하여 번들이 제대로 작동하는지 확인합니다.

   ```shell
   wget https://<serveraddress:port>/cq/system/console/bundles
   ```

1. 다음으로, AEM 5.6의 배포를 취소합니다.

   ```shell
   rm jboss-install-folder/standalone/deployments/cq.war
   ```

1. JBoss를 중지합니다.

1. 이제 crx2oak 마이그레이션 툴을 사용하여 저장소를 마이그레이션합니다.

   ```shell
   java -jar crx2oak.jar crx-quickstart/repository/ crx-quickstart/oak-repository
   ```

   >[!NOTE]
   >
   >이 예에서 oak-repository는 새로 변환된 저장소가 상주하는 임시 디렉토리입니다. 이 단계를 수행하기 전에 최신 crx2oak.jar 버전이 있는지 확인합니다.

1. 다음을 수행하여 sling.properties 파일에서 필요한 속성을 삭제합니다.

   1. 다음 위치에 있는 파일을 엽니다. `crx-quickstart/launchpad/sling.properties`
   1. 단계 텍스트다음 속성을 제거하고 파일을 저장합니다.

      1. `sling.installer.dir`

      1. `felix.cm.dir`

      1. `granite.product.version`

      1. `org.osgi.framework.system.packages`

      1. `osgi-core-packages`

      1. `osgi-compendium-services`

      1. `jre-*`

      1. `sling.run.mode.install.options`

1. 더 이상 필요하지 않은 파일 및 폴더를 제거합니다. 구체적으로 제거해야 하는 항목은 다음과 같습니다.

   * 시작 **패드/시작 폴더**. 터미널에서 다음 명령을 실행하여 삭제할 수 있습니다. `rm -rf crx-quickstart/launchpad/startup`

   * base.jar 파일 ****: `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * BootstrapCommandFile **_timestamp.txt 파일**: `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

1. 새로 마이그레이션된 세그먼트스토어를 올바른 위치에 복사합니다.

   ```shell
   mv crx-quickstart/oak-repository/segmentstore crx-quickstart/repository/segmentstore
   ```

1. 데이터 저장소도 다음과 같이 복사합니다.

   ```shell
   mv crx-quickstart/repository/repository/datastore crx-quickstart/repository/datastore
   ```

1. 그런 다음 업그레이드된 새 인스턴스와 함께 사용할 OSGi 구성이 들어 있는 폴더를 만들어야 합니다. 특히 install이라는 폴더를 **crx-quickstart**&#x200B;아래에 만들어야 합니다.

1. 이제 AEM 6.3과 함께 사용할 노드 저장소 및 데이터 저장소를 만듭니다.crx-quickstart\install ****&#x200B;아래에 다음 이름으로 두 파일을 만들어 이 작업을 수행할 수 있습니다.

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`

   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`
   이 두 파일은 TarMK 노드 저장소 및 파일 데이터 저장소를 사용하도록 AEM을 구성합니다.

1. 구성 파일을 편집하여 사용할 수 있도록 합니다. 자세히 알아보기:

   * 다음 줄을 **org.apache.jackrabbit.oak.segmentNodeStoreService.config**&#x200B;에 추가합니다.\
      `customBlobStore=true`

   * 그런 다음 **org.apache.jackrabbit.plugins.blob.datastore.FileDataStore.config**&#x200B;에 다음 줄을 추가합니다.

      ```
      path=./crx-quickstart/repository/datastore
       minRecordLength=4096
      ```

1. 다음을 실행하여 crx2 실행 모드를 제거합니다.

   ```shell
   find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf {} \
   ```

1. 이제 AEM 6.3 전쟁 파일의 실행 모드를 변경해야 합니다. 이렇게 하려면 먼저 AEM 6.3 전쟁에 포함될 임시 폴더를 만듭니다. 이 예제의 폴더 이름은 **temp**&#x200B;입니다. 전쟁 파일이 복사되면 임시 폴더 내에서 실행하여 내용을 추출합니다.

   ```shell
   jar xvf aem-quickstart-6.3.0.war
   ```

1. 컨텐츠가 추출되면 WEB-INF **폴더로** 이동하여 `web.xml` 파일을 편집하여 실행 모드를 변경합니다. XML에서 설정된 위치를 찾으려면 `sling.run.modes` 문자열을 찾습니다. 코드를 찾으면 기본적으로 작성하도록 설정된 다음 코드 줄의 실행 모드를 변경합니다.

   ```shell
   <param-value >author</param-value>
   ```

1. 위의 작성자 값을 변경하고 실행 모드를 다음으로 설정합니다.author,crx3,crx3tar 코드의 마지막 블록은 다음과 같아야 합니다.

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. 수정된 내용으로 jar를 다시 만듭니다.

   ```shell
   jar cvf aem62.war
   ```

1. 마지막으로 새 전쟁 파일을 배포합니다.

   ```shell
   cp temp/aem62.war jboss-install-folder/standalone/deployments/aem61.war
   ```

