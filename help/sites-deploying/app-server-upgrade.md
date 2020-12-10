---
title: 응용 프로그램 서버 설치 업그레이드 단계
seo-title: 응용 프로그램 서버 설치 업그레이드 단계
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
source-git-commit: f696b1081f14ba379cde51a3542a5b1b5f9668e2
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---


# 응용 프로그램 서버 설치 업그레이드 단계{#upgrade-steps-for-application-server-installations}

이 섹션에서는 Application Server 설치에 대한 AEM을 업데이트하려면 따라야 하는 절차에 대해 설명합니다.

이 절차의 모든 예제는 Tomcat을 응용 프로그램 서버로 사용하고 AEM의 작업 버전이 이미 배포되었다는 것을 의미합니다. 이 절차는 **AEM 버전 6.4에서 6.5**&#x200B;로 수행된 문서 업그레이드를 위한 것입니다.

1. 먼저 TomCat을 시작합니다. 대부분의 경우 터미널에서 이 명령을 실행하여 `./catalina.sh` 시작 스크립트를 실행하여 이를 수행할 수 있습니다.

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. AEM 6.4가 이미 배포된 경우 다음을 액세스하여 번들이 올바르게 작동하는지 확인합니다.

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. 다음으로 AEM 6.4를 배포하지 않습니다. 이 작업은 TomCat 앱 관리자(`http://serveraddress:serverport/manager/html`)에서 수행할 수 있습니다.

1. 이제 crx2oak 마이그레이션 도구를 사용하여 저장소를 마이그레이션합니다. 이를 위해 [이 위치](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak)에서 crx2oak 최신 버전을 다운로드합니다.

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -XX:MaxPermSize=2048M -jar crx2oak.jar --load-profile segment-fds
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

1. 더 이상 필요하지 않은 파일 및 폴더를 제거합니다. 구체적으로 제거해야 하는 항목은 다음과 같습니다.

   * **launchpad/startup 폴더**. 터미널에서 다음 명령을 실행하여 삭제할 수 있습니다.`rm -rf crx-quickstart/launchpad/startup`

   * **base.jar 파일**:`find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * **BootstrapCommandFile_timestamp.txt 파일**:`rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

   * 다음을 실행하여 **sling.options.file**&#x200B;을 제거합니다.`find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`

1. 이제 AEM 6.5와 함께 사용할 노드 저장소 및 데이터 저장소를 만듭니다. 이 작업을 수행하려면 `crx-quickstart\install` 아래에 다음 이름의 두 파일을 만듭니다.

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   이 두 파일은 AEM에서 TarMK 노드 스토어와 파일 데이터 저장소를 사용하도록 구성합니다.

1. 구성 파일을 편집하여 사용할 수 있도록 합니다. 자세한 내용:

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`에 다음 줄을 추가합니다.

      ```customBlobStore=true```

   * 그런 다음 `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`에 다음 줄을 추가합니다.

      ```
      path=./crx-quickstart/repository/datastore
      minRecordLength=4096
      ```

1. 이제 AEM 6.5 전쟁 파일의 실행 모드를 변경해야 합니다. 그렇게 하기 위해서, 먼저 AEM 6.5 전쟁을 수용할 임시 폴더를 만듭니다. 이 예제의 폴더 이름은 `temp`입니다. 전쟁 파일이 복사되면 임시 폴더 내에서 실행하여 콘텐트를 추출합니다.

   ```
   jar xvf aem-quickstart-6.5.0.war
   ```

1. 컨텐츠가 추출되면 **WEB-INF** 폴더로 이동하여 web.xml 파일을 편집하여 실행 모드를 변경합니다. XML에서 설정된 위치를 찾으려면 `sling.run.modes` 문자열을 찾습니다. 코드를 찾으면 기본적으로 작성하도록 설정되어 있는 다음 코드 줄의 실행 모드를 변경합니다.

   ```bash
   <param-value >author</param-value>
   ```

1. 위의 작성자 값을 변경하고 실행 모드를 다음으로 설정합니다.`author,crx3,crx3tar`. 코드의 마지막 블록은 다음과 같아야 합니다.

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. 수정된 내용으로 jar를 다시 만듭니다.

   ```bash
   jar cvf aem65.war
   ```

1. 마지막으로, TomCat에 새로운 전쟁 파일을 배포합니다.
