---
title: Application Server 설치 업그레이드 단계
description: 애플리케이션 서버를 통해 배포된 AEM의 인스턴스를 업그레이드하는 방법에 대해 알아봅니다.
feature: Upgrading
exl-id: 86dd10ae-7f16-40c8-84b6-91ff2973a523
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# Application Server 설치 업그레이드 단계{#upgrade-steps-for-application-server-installations}

이 섹션에서는 Application Server용 AEM 설치를 업데이트하기 위해 수행해야 하는 절차에 대해 설명합니다.

이 절차의 모든 예제에서는 Tomcat을 Application Server로 사용하며 AEM의 작업 버전이 이미 배포되어 있음을 의미합니다. 이 절차는 **AEM 버전 6.4에서 6.5**(으)로 수행된 업그레이드를 문서화하기 위한 것입니다.

1. 먼저 TomCat을 시작합니다. 대부분의 경우 터미널에서 이 명령을 실행하여 `./catalina.sh` 시작 스크립트를 실행하여 이 작업을 수행할 수 있습니다.

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. AEM 6.4가 이미 배포된 경우 다음에 액세스하여 번들이 올바르게 작동하는지 확인합니다.

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. 그런 다음 AEM 6.4 배포를 취소합니다. 이 작업은 TomCat 앱 관리자(`http://serveraddress:serverport/manager/html`)에서 수행할 수 있습니다.

1. 이제 crx2oak 마이그레이션 도구를 사용하여 저장소를 마이그레이션합니다. 이렇게 하려면 [이 위치](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)에서 최신 버전의 crx2oak를 다운로드하십시오.

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -jar crx2oak.jar --load-profile segment-fds
   ```

1. 다음을 수행하여 sling.properties 파일에서 필요한 속성을 삭제합니다.

   1. `crx-quickstart/launchpad/sling.properties`에 있는 파일을 엽니다.
   1. 단계 텍스트 다음 속성을 제거하고 파일을 저장합니다.

      1. `sling.installer.dir`

      1. `felix.cm.dir`

      1. `granite.product.version`

      1. `org.osgi.framework.system.packages`

      1. `osgi-core-packages`

      1. `osgi-compendium-services`

      1. `jre-*`

      1. `sling.run.mode.install.options`

1. 더 이상 필요하지 않은 파일 및 폴더를 제거합니다. 특별히 제거해야 하는 항목은 다음과 같습니다.

   * **시작 패드/시작 폴더**&#x200B;입니다. 터미널에서 다음 명령을 실행하여 삭제할 수 있습니다. `rm -rf crx-quickstart/launchpad/startup`

   * **base.jar 파일**: `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * **BootstrapCommandFile_timestamp.txt 파일**: `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

   * 다음을 실행하여 **sling.options.file**&#x200B;을(를) 제거합니다. `find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`

1. 이제 AEM 6.5와 함께 사용되는 노드 저장소 및 데이터 저장소를 만듭니다. `crx-quickstart\install` 아래에 다음 이름의 두 파일을 만들어 이 작업을 수행할 수 있습니다.

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   이 두 파일은 TarMK 노드 저장소 및 파일 데이터 저장소를 사용하도록 AEM을 구성합니다.

1. 사용 준비가 되도록 구성 파일을 편집합니다. 자세히 알아보기:

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`에 다음 줄을 추가하십시오.

     `customBlobStore=true`

   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`에 다음 줄을 추가합니다.

     ```
     path=./crx-quickstart/repository/datastore
     minRecordLength=4096
     ```

1. 이제 AEM 6.5 war 파일에서 실행 모드를 변경해야 합니다. 이를 위해 먼저 AEM 6.5 전쟁을 저장할 임시 폴더를 만듭니다. 이 예제의 폴더 이름은 `temp`입니다. war 파일이 복사되면 임시 폴더 내에서 를 실행하여 해당 내용을 추출합니다.

   ```
   jar xvf aem-quickstart-6.5.0.war
   ```

1. 콘텐츠가 추출되면 **WEB-INF** 폴더로 이동하여 web.xml 파일을 편집하여 실행 모드를 변경합니다. XML에서 설정된 위치를 찾으려면 `sling.run.modes` 문자열을 찾습니다. 찾으면 다음 코드 행에서 실행 모드를 변경합니다. 이 코드는 기본적으로 작성자로 설정됩니다.

   ```bash
   <param-value >author</param-value>
   ```

1. 위의 작성자 값을 변경하고 실행 모드를 `author,crx3,crx3tar`(으)로 설정하십시오. 코드의 최종 블록은 다음과 같아야 합니다.

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. 수정된 내용이 포함된 Jar를 다시 만듭니다.

   ```bash
   jar cvf aem65.war
   ```

1. 마지막으로, TomCat에 새로운 war 파일을 배포합니다.
