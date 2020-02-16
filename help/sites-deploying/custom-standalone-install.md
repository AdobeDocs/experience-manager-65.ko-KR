---
title: 사용자 지정 독립형 설치
seo-title: 사용자 지정 독립형 설치
description: 독립 실행형 AEM 인스턴스를 설치할 때 사용할 수 있는 옵션에 대해 알아봅니다.
seo-description: 독립 실행형 AEM 인스턴스를 설치할 때 사용할 수 있는 옵션에 대해 알아봅니다.
uuid: 83fc49d8-2c44-4bb2-988a-f29475066efc
contentOwner: Tyler Rushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: deae8ecb-a2ee-4442-97ca-98bfd1b85738
docset: aem65
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1

---


# 사용자 지정 독립형 설치{#custom-standalone-install}

이 섹션에서는 독립 실행형 AEM 인스턴스를 설치할 때 사용할 수 있는 옵션에 대해 설명합니다. AEM 6 [을](/help/sites-deploying/storage-elements-in-aem-6.md) 새로 설치한 후 백엔드 스토리지 유형을 선택하는 방법에 대한 자세한 내용은 스토리지 요소를 참조할 수 있습니다.

## 파일 이름을 변경하여 포트 번호 변경 {#changing-the-port-number-by-renaming-the-file}

AEM의 기본 포트는 4502입니다. 해당 포트를 사용할 수 없거나 이미 사용 중인 경우 Quickstart는 다음과 같이 첫 번째 사용 가능한 포트 번호를 사용하도록 자동으로 구성합니다.4502, 8080, 8081, 8082, 8083, 8084, 8085, 8888, 9362, `<*random*>`.

quickstart jar 파일의 이름을 변경하여 포트 번호를 설정할 수도 있습니다. 그러면 파일 이름에 포트 번호가 포함됩니다.예를 들어, `cq5-publish-p4503.jar` 또는 `cq5-author-p6754.jar`을 입력합니다.

quickstart jar 파일의 이름을 바꿀 때 따라야 할 다양한 규칙이 있습니다.

* 파일 이름을 바꿀 때는 `cq;` 에서와 같이 시작해야 합니다 `cq5-publish-p4503.jar`.

* 포트 번호 앞에 *항상* -p;cq5-publish-p4503.jar 또는 cq5-author-p6754.jar에 있는 경우를 예로 들 수 있습니다.

>[!NOTE]
>
>이는 포트 번호를 추출하는 데 사용되는 규칙을 완전히 채우는 데 대해 걱정할 필요가 없도록 하기 위한 것입니다.
>
>* 포트 번호는 4 또는 5자리여야 합니다.
>* 이 숫자는 대시 뒤에 와야 합니다.
>* 파일 이름에 다른 숫자가 있으면 포트 번호가 `-p`
>* 파일 이름의 시작 부분에 있는 &quot;cq5&quot; 접두사가 무시됩니다.
>



>[!NOTE]
>
>시작 명령의 `-port` 옵션을 사용하여 포트 번호를 변경할 수도 있습니다.

### Java 11 고려 사항 {#java-considerations}

Oracle Java 11(또는 일반적으로 Java 8 이후 버전)을 실행하는 경우 AEM을 시작할 때 명령줄에 추가 스위치를 추가해야 합니다.

* 다음 - `-add-opens` 스위치를 추가해야 `stdout.log`

```shell
--add-opens=java.desktop/com.sun.imageio.plugins.jpeg=ALL-UNNAMED --add-opens=java.base/sun.net.www.protocol.jrt=ALL-UNNAMED --add-opens=java.naming/javax.naming.spi=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/jdk.internal.loader=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED -Dnashorn.args=--no-deprecation-warning
```

* 또한 잠재적 성능 문제를 완화하려면 스위치를 `-XX:+UseParallelGC` 사용해야 합니다.

다음은 Java 11에서 AEM을 시작할 때 추가 JVM 매개 변수가 어떻게 표시되어야 하는지에 대한 예입니다.

```shell
-XX:+UseParallelGC --add-opens=java.desktop/com.sun.imageio.plugins.jpeg=ALL-UNNAMED --add-opens=java.base/sun.net.www.protocol.jrt=ALL-UNNAMED --add-opens=java.naming/javax.naming.spi=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/jdk.internal.loader=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED -Dnashorn.args=--no-deprecation-warning
```

마지막으로 AEM 6.3에서 업그레이드된 인스턴스를 실행 중인 경우 아래에서 다음 속성이 **true** 로 설정되어 있는지 확인하십시오 `sling.properties`.

* `felix.bootdelegation.implicit`

## 실행 모드 {#run-modes}

**실행 모드를** 사용하면 특정 용도로 AEM 인스턴스를 조정할 수 있습니다.예를 들어, 작성 또는 게시, 테스트, 개발, 인트라넷 등의 작업을 수행할 수 있습니다. 이러한 모드를 사용하면 샘플 컨텐츠 사용을 제어할 수 있습니다. 이 샘플 컨텐츠는 빠른 시작을 만들기 전에 정의되며 패키지, 구성 등을 포함할 수 있습니다. 이 기능은 샘플 컨텐츠 없이 설치를 간소화하고자 할 때 바로 바로 바로 설치할 수 있는 경우에 특히 유용합니다. 자세한 내용은 다음을 참조하십시오.

* [실행 모드](/help/sites-deploying/configure-runmodes.md)

## 파일 설치 공급자 추가 {#adding-a-file-install-provider}

기본적으로 폴더는 파일에 대해 `crx-quickstart/install` 감시됩니다.
이 폴더는 존재하지 않지만 런타임 시 간단히 만들 수 있습니다.

번들, 구성 또는 컨텐츠 패키지를 이 디렉토리에 넣으면 자동으로 선택하여 설치됩니다. 제거되면 제거됩니다.
번들, 컨텐츠 패키지 또는 구성을 저장소에 배치하는 또 다른 방법입니다.

이 기능은 다음과 같은 여러 사용 사례에서 특히 유용합니다.

* 개발 중에 파일 시스템에 내용을 삽입하는 것이 더 쉽습니다.
* 문제가 발생하면 웹 콘솔 및 저장소에 연결할 수 없습니다. 이 코드를 사용하면 이 디렉토리에 추가 번들을 넣을 수 있으며 번들을 설치해야 합니다.
* 빠른 시작을 시작하기 전에 `crx-quickstart/install` 폴더를 만들 수 있으며, 추가 패키지를 거기에 배치할 수 있습니다.

>[!NOTE]
>
>서버 [시작](https://helpx.adobe.com/experience-manager/kb/HowToInstallPackagesUsingRepositoryInstall.html) 시 CRX 패키지를 자동으로 설치하는 방법을 참조하십시오.

## Windows 서비스로 Adobe Experience Manager 설치 및 시작 {#installing-and-starting-adobe-experience-manager-as-a-windows-service}

>[!NOTE]
>
>관리자로 로그온하는 동안 다음 절차를 수행하거나 관리자로 실행 **컨텍스트 메뉴 선택을 사용하여 이러한 단계를 시작/** 실행해야 합니다.
>
>관리자 권한이 있는 사용자로 로그온하는 것이 **부족합니다**. 이러한 단계를 완료할 때 관리자로 로그온하지 않은 경우 액세스 거부 **오류가** 표시됩니다.

AEM을 Windows 서비스로 설치하고 시작하려면 다음을 수행하십시오.

1. 텍스트 편집기에서 crx-quickstart\opt\helpers\instsrv.bat 파일을 엽니다.
1. 64비트 Windows 서버를 구성하는 경우 운영 체제에 따라 runsrv의 모든 인스턴스를 다음 명령 중 하나로 바꿉니다.

   * prunsrv_amd64
   * prunsrv_ia64
   이 명령은 32비트 Java 대신 64비트 Java에서 Windows 서비스 데몬을 시작하는 적절한 스크립트를 호출합니다.

1. 프로세스가 두 개 이상의 프로세스로 변환되지 않도록 하려면 최대 더미 크기와 PermGen JVM 매개변수를 늘립니다. 명령을 `set jvm_options` 찾아 다음과 같이 값을 설정합니다.

   `set jvm_options=-XX:MaxPermSize=256M;-Xmx1792m`

1. 명령 프롬프트를 열고 현재 디렉토리를 AEM 설치의 crx-quickstart/opt/helpers 폴더로 변경하고 다음 명령을 입력하여 서비스를 생성합니다.

   `instsrv.bat cq5`

   서비스가 만들어졌는지 확인하려면 관리 도구 제어판에서 서비스를 열거나 명령 프롬프트에 `start services.msc` 입력합니다. cq5 서비스가 목록에 나타납니다.

1. 다음 중 하나를 수행하여 서비스를 시작합니다.

   * 서비스 제어판에서 cq5를 클릭하고 시작을 클릭합니다.
   ![chlimage_1-11](assets/chlimage_1-11.png)

   * 명령줄에서 net start cq5를 입력합니다.
   ![chlimage_1-12](assets/chlimage_1-12.png)

1. Windows는 서비스가 실행 중임을 나타냅니다. AEM이 시작되고 prunsrv 실행 파일이 작업 관리자에 나타납니다. 웹 브라우저에서 AEM으로 이동하여 AEM을 `https://localhost:4502` 시작합니다.

   ![chlimage_1-13](assets/chlimage_1-13.png)

>[!NOTE]
>
>instsrv.bat 파일의 속성 값은 Windows 서비스를 만들 때 사용됩니다. instsrv.bat에서 속성 값을 편집하는 경우 서비스를 제거한 다음 다시 설치해야 합니다.

>[!NOTE]
>
>AEM을 서비스로 설치할 때 Configuration Manager에서 로그 디렉토리의 절대 경로를 제공해야 `com.adobe.xmp.worker.files.ncomm.XMPFilesNComm` 합니다.

서비스를 제거하려면 서비스 **제어판** 또는 **명령줄에서** [중지] `instsrv.bat -uninstall cq5`를클릭하여 폴더를 찾아입력합니다. 서비스를 입력하면 서비스 **제어판의** 목록이나 명령줄의 목록에서 제거됩니다 `net start`.

## 임시 작업 디렉토리의 위치 재정의 {#redefining-the-location-of-the-temporary-work-directory}

java 컴퓨터의 임시 폴더의 기본 위치는 입니다 `/tmp`. 예를 들어 패키지를 빌드할 때 AEM에서는 이 폴더도 사용합니다.

임시 폴더의 위치(예: 사용 가능한 공간이 더 많은 디렉토리가 필요한 경우)를 변경하려면 JVM 매개변수를 추가하여 * `<new-tmp-path>`*를 정의합니다.

`-Djava.io.tmpdir="/<*new-tmp-path*>"`

다음 중 하나를 수행합니다.

* 서버 시작 명령줄
* serverctl 또는 시작 스크립트의 CQ_JVM_OPTS 환경 매개 변수

## Quickstart 파일에서 사용할 수 있는 추가 옵션 {#further-options-available-from-the-quickstart-file}

추가 옵션 및 이름 바꾸기 규칙은 -help 옵션을 통해 사용할 수 있는 빠른 시작 도움말 파일에 설명되어 있습니다. 도움말에 액세스하려면 다음을 입력합니다.

* `java -jar cq5-<*version*>.jar -help`

```shell
Loading quickstart properties: default
Loading quickstart properties: instance
Setting properties from filename '/Users/Desktop/AEM/cq-quickstart-5.6.0.jar'
--------------------------------------------------------------------------------
Adobe Experience Manager Quickstart (build 20130129)
--------------------------------------------------------------------------------
Usage:
 Use these options on the Quickstart command line.
--------------------------------------------------------------------------------

-help (--help,-h)
         Show this help message
-quickstart.server.port (-p,-port) <port>
         Set server port number
-contextpath (-c,-org.apache.felix.http.context_path) <contextpath>
         Set context path
-debug <port>
         Enable Java Debugging on port number; forces forking
-gui
         Show GUI if running on a terminal
-nobrowser (-quickstart.nobrowser)
         Do not open browser at startup
-unpack
         Unpack installation files only, do not start the server (implies
         -verbose)
-v (-verbose)
         Do not redirect stdout/stderr to files and do not close stdin
-nofork
         Do not fork the JVM, even if not running on a console
-fork
         Force forking the JVM if running on a console, using recommended
         default memory settings for the forked JVM.
-forkargs <args> [<args> ...]
         Additional arguments for the forked JVM, defaults to '-Xmx1024m
         -XX:MaxPermSize=256m '.  Use -- to specify values starting with -,
         example: '-forkargs -- -server'
-a (--interface) <interface>
         Optional IP address (interface) to bind to
-pt <string>
         Process type (main/fork) - do not use directly, used when forking a
         process
-r <string> [<string> [<string> [<string> [<string> [<string> [<string> [<string> [<string> [<string>]]]]]]]]]
         Runmode(s) - Use this to define the run mode(s)
-b <string>
         Base folder - defines the path under which the quickstart work folder
         is created
-low-mem-action <string>
         Low memory action - what to do if memory is insufficient at startup
-use-control-port
         Start a control port
-ll <level>
         Define launchpad log level (1 = error...4 = debug)
--------------------------------------------------------------------------------
Quickstart filename options
--------------------------------------------------------------------------------
Usage:
 Rename the jar file, including one of the patterns shown below, to set the
corresponding option. Command-line options have priority on these filename
patterns.
--------------------------------------------------------------------------------

-NNNN
         Include -NNNN.jar or -pNNNN in the renamed jar filename to run on port
         NNNN, for example: quickstart-8085.jar
-nobrowser
         Include -nobrowser in the renamed jar filename to avoid opening the
         browser at startup, example: quickstart-nobrowser-8085.jar
-publish
         Include -publish in the renamed jar filename to run cq5 in "publish"
         mode, example: cq5-publish-7502.jar
--------------------------------------------------------------------------------
The license.properties file
--------------------------------------------------------------------------------
  The license.properties file stores licensing information, created from the
  licensing form displayed on first startup and stored in the folder from where
  Quickstart is run.
--------------------------------------------------------------------------------
Log files
--------------------------------------------------------------------------------
  Once Quickstart has been unpacked and started, log files can be found under
  ./crx-quickstart/logs.
--------------------------------------------------------------------------------
```

## Amazon EC2 환경에 AEM 설치 {#installing-aem-in-the-amazon-ec-environment}

AEM을 Amazon Elastic Compute Cloud(EC2) 인스턴스에 설치할 때 작성자와 게시를 모두 EC2 인스턴스에 설치하는 경우 AEM Manager 인스턴스 [설치 절차에 따라 작성자 인스턴스가 올바르게 설치됩니다](#installinginstancesofaemmanager).그러나 게시 인스턴스는 작성자가 됩니다.

EC2 환경에 게시 인스턴스를 설치하기 전에 다음을 수행하십시오.

1. 인스턴스를 처음으로 시작하기 전에 게시 인스턴스에 대한 jar 파일의 압축을 해제합니다. 파일의 압축을 풀려면 다음 명령을 사용합니다.

   ```xml
   java -jar quickstart.jar -unpack
   ```

   >[!NOTE]
   >
   >인스턴스를 처음 시작한 **후** 모드를 변경하면 실행 모드를 변경할 수 없습니다.

1. 다음을 실행하여 인스턴스를 시작합니다.

   ```xml
   java -jar quickstart.jar -r publish
   ```

   >[!CAUTION]
   >
   >위의 명령을 실행하여 인스턴스를 압축 해제한 후 먼저 실행해야 합니다. 그렇지 않으면 quickstart.properties 채우기가 생성되지 않습니다. 이 파일이 없으면 향후 모든 AEM 업그레이드가 실패합니다.

1. bin **폴더에서** 시작 **** 스크립트를 열고 다음 섹션을 확인합니다.

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='author'
   fi
   ```

1. 실행 모드를 변경하여 파일을 **게시하고** 저장합니다.

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='publish'
   fi
   ```

1. 인스턴스를 중지하고 **시작** 스크립트를 실행하여 다시 시작합니다.

## 설치 확인 {#verifying-the-installation}

다음 링크를 사용하여 설치가 작동하는지 확인할 수 있습니다(모든 예는 인스턴스가 localhost의 포트 8080에서 실행 중이고, CRX는 /crx 및 Launchpad 아래에 설치되어 있는지 여부).

* `https://localhost:8080/crx/de`
CRXDE Lite 콘솔.

* `https://localhost:8080/system/console`
웹 콘솔.

## 설치 후 작업 {#actions-after-installation}

AEM WCM을 구성하는 방법은 여러 가지가 있지만 특정 작업을 수행하거나 설치 후 즉시 검토해야 합니다.

* 보안 [체크리스트를](/help/sites-administering/security-checklist.md) 참조하십시오.
* AEM WCM과 함께 설치되는 기본 사용자 및 그룹 목록을 검토합니다. 다른 계정에 대해 조치를 취할지 여부를 확인합니다. 자세한 내용은 보안 [및 사용자 관리를](/help/sites-administering/security.md) 참조하십시오.

## CRXDE Lite 및 웹 콘솔 액세스 {#accessing-crxde-lite-and-the-web-console}

AEM WCM 파섹

* [CRXDE](#accessing-crxde-lite) Lite - 저장소 액세스 및 관리에 사용
* [웹 콘솔](#accessing-the-web-console) - OSGi 번들(OSGi 콘솔이라고도 함)을 관리하거나 구성하는 데 사용됩니다.

### CRXDE Lite 액세스 {#accessing-crxde-lite}

CRXDE Lite를 열려면 시작 **화면에서 CRXDE** Lite를 선택하거나 브라우저를 사용하여

```
 https://<<i>host</i>>:<<i>port</i>>/crx/de/index.jsp
```

예를 들어,`https://localhost:4502/crx/de/index.jsp`

![instcq_crxdelite](assets/installcq_crxdelite.png)

#### 웹 콘솔 액세스 {#accessing-the-web-console}

Adobe CQ 웹 콘솔에 액세스하려면 시작 **화면에서** OSGi 콘솔을 선택하거나 브라우저를 사용하여

```
 https://<host>:<port>/system/console
```

예:번들 페이지에`https://localhost:4502/system/console`대해 또는`https://localhost:4502/system/console/bundles`

![chlimage_1-14](assets/chlimage_1-14.png)

자세한 [내용은 웹 콘솔과](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) OSGi 구성을 참조하십시오.

## 문제 해결 {#troubleshooting}

설치 중에 발생할 수 있는 문제를 처리하는 방법에 대한 자세한 내용은 다음을 참조하십시오.

* [문제 해결](/help/sites-deploying/troubleshooting.md)

## Uninstalling Adobe Experience Manager {#uninstalling-adobe-experience-manager}

AEM은 단일 디렉토리에 설치되므로 제거 유틸리티를 사용할 필요가 없습니다. AEM을 제거하는 방법은 수행하고자 하는 것과 사용하는 영구 스토리지에 따라 다르지만, 전체 설치 디렉토리를 삭제하는 것만큼 간단하게 제거할 수 있습니다.

예를 들어 기본 TarPM 설치 시 영구 저장소가 설치 디렉토리에 포함되어 있으면 폴더를 삭제하면 데이터도 제거됩니다.

>[!NOTE]
>
>AEM을 삭제하기 전에 저장소를 백업하는 것이 좋습니다. 전체 &lt;cq-installation-directory>를 삭제하면 저장소가 삭제됩니다. &lt;cq-installation-directory>/crx-quickstart/repository 폴더를 삭제하기 전에 저장소 데이터를 유지하려면 다른 폴더를 삭제하기 전에 다른 위치로 이동합니다.

AEM 설치가 외부 저장소(예: 데이터베이스 서버)를 사용하는 경우 폴더를 제거해도 데이터가 자동으로 제거되지는 않지만 저장소 구성이 제거되므로 JCR 컨텐츠를 복원하는 것이 어렵습니다.
