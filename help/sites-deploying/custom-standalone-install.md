---
title: 사용자 지정 독립 실행형 설치
description: 독립형 AEM 인스턴스를 설치할 때 사용할 수 있는 옵션에 대해 알아봅니다.
content-type: reference
topic-tags: deploying
exl-id: d6484bb7-8123-4f42-96e8-aa441b1093f3
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 3effd4fa686ac89421ffe74e52bf34830ddd776c
workflow-type: tm+mt
source-wordcount: '1614'
ht-degree: 0%

---

# 사용자 지정 독립 실행형 설치{#custom-standalone-install}

이 섹션에서는 독립형 AEM 인스턴스를 설치할 때 사용할 수 있는 옵션에 대해 설명합니다. AEM 6을 새로 설치한 후 백엔드 저장소 유형을 선택하는 방법에 대한 자세한 내용은 [저장소 요소](/help/sites-deploying/storage-elements-in-aem-6.md)를 읽을 수도 있습니다.

## 파일 이름을 변경하여 포트 번호 변경 {#changing-the-port-number-by-renaming-the-file}

AEM의 기본 포트는 4502입니다. 해당 포트를 사용할 수 없거나 이미 사용 중인 경우 Quickstart는 사용 가능한 첫 번째 포트 번호를 사용하도록 자동으로 구성합니다. 4502, 8080, 8081, 8082, 8083, 8084, 8085, 8888, 9362, `<*random*>`.

Quickstart jar 파일의 이름을 바꾸어 포트 번호를 설정할 수도 있습니다. 그러면 파일 이름에 포트 번호가 포함됩니다(예: `cq5-publish-p4503.jar` 또는 `cq5-author-p6754.jar`).

quickstart jar 파일의 이름을 바꿀 때 따라야 할 다양한 규칙이 있습니다.

* 파일 이름을 바꿀 때는 `cq5-publish-p4503.jar`과(와) 같이 `cq;`(으)로 시작해야 합니다.

* cq5-publish-p4503.jar 또는 cq5-author-p6754.jar에서와 같이 *always*&#x200B;이(가) 포트 번호 접두사로 -p를 사용하는 것이 좋습니다.

>[!NOTE]
>
>이는 포트 번호 추출에 사용되는 규칙 이행에 대해 걱정할 필요가 없도록 하기 위한 것입니다.
>
>* 포트 번호는 4 또는 5자리여야 합니다.
>* 이 숫자는 대시 뒤에 와야 합니다.
>* 파일 이름에 다른 숫자가 있는 경우 포트 번호 앞에 `-p`이(가) 있어야 합니다.
>* 파일 이름의 시작 부분에 있는 &quot;cq5&quot; 접두사는 무시됩니다
>

>[!NOTE]
>
>start 명령의 `-port` 옵션을 사용하여 포트 번호를 변경할 수도 있습니다.

### Java 11 고려 사항 {#java-considerations}

Oracle Java 11(또는 일반적으로 Java 버전이 8보다 최신임)을 실행하는 경우 AEM을 시작할 때 명령줄에 스위치를 추가해야 합니다.

* `stdout.log`에서 관련 리플렉션 액세스 WARNING 메시지를 방지하려면 `-add-opens` 스위치를 추가해야 합니다.

```shell
--add-opens=java.desktop/com.sun.imageio.plugins.jpeg=ALL-UNNAMED --add-opens=java.base/sun.net.www.protocol.jrt=ALL-UNNAMED --add-opens=java.naming/javax.naming.spi=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/jdk.internal.loader=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED -Dnashorn.args=--no-deprecation-warning
```

* 또한 잠재적인 성능 문제를 완화하려면 `-XX:+UseParallelGC` 스위치를 사용해야 합니다.

다음은 Java 11에서 AEM을 시작할 때 추가 JVM 매개 변수가 어떻게 표시되어야 하는지에 대한 샘플입니다.

```shell
-XX:+UseParallelGC --add-opens=java.desktop/com.sun.imageio.plugins.jpeg=ALL-UNNAMED --add-opens=java.base/sun.net.www.protocol.jrt=ALL-UNNAMED --add-opens=java.naming/javax.naming.spi=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/jdk.internal.loader=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED -Dnashorn.args=--no-deprecation-warning
```

마지막으로, AEM 6.3에서 업그레이드된 인스턴스를 실행하는 경우 `sling.properties`에서 다음 속성이 **true**(으)로 설정되어 있는지 확인하십시오.

* `felix.bootdelegation.implicit`

## 실행 모드 {#run-modes}

**실행 모드**&#x200B;를 사용하면 작성자 또는 게시, 테스트, 개발, 인트라넷 등과 같은 특정 목적을 위해 AEM 인스턴스를 조정할 수 있습니다. 이러한 모드를 사용하면 샘플 콘텐츠의 사용을 제어할 수도 있습니다. 이 샘플 콘텐츠는 빠른 시작을 빌드하기 전에 정의되며 패키지, 구성 등을 포함할 수 있습니다. 이 기능은 샘플 콘텐츠 없이 설치를 희박하게 유지하려는 경우 프로덕션 준비 설치에 특히 유용합니다. 자세한 내용은 다음을 참조하십시오.

* [실행 모드](/help/sites-deploying/configure-runmodes.md)

## 파일 설치 공급자 추가 {#adding-a-file-install-provider}

기본적으로 `crx-quickstart/install` 폴더에는 파일이 표시됩니다.
이 폴더는 존재하지 않지만 런타임 시 만들 수 있습니다.

번들, 구성 또는 콘텐츠 패키지를 이 디렉토리에 넣으면 자동으로 선택되어 설치됩니다. 제거하면 제거됩니다.
이는 번들, 콘텐츠 패키지 또는 구성을 저장소에 저장하는 또 다른 방법입니다.

이는 몇 가지 사용 사례에 특히 유용합니다.

* 개발 중에 파일 시스템에 무언가를 넣는 것이 더 쉬울 수 있습니다.
* 문제가 발생하면 웹 콘솔과 저장소에 연결할 수 없습니다. 이를 통해 추가 번들을 이 디렉토리에 넣을 수 있으며 설치해야 합니다.
* `crx-quickstart/install` 폴더는 빠른 시작을 시작하기 전에 만들 수 있으며 추가 패키지를 넣을 수 있습니다.

## Adobe Experience Manager as a Windows Service 설치 및 시작 {#installing-and-starting-adobe-experience-manager-as-a-windows-service}

>[!NOTE]
>
>관리자로 로그온하는 동안 다음 절차를 수행하거나 **관리자로 실행** 상황에 맞는 메뉴 선택을 사용하여 이 절차를 시작/실행하십시오.
>
>관리자 권한이 있는 사용자로 로그온하는 것은 **부족함**&#x200B;입니다. 이 단계를 완료할 때 관리자로 로그온하지 않으면 **액세스 거부됨** 오류가 표시됩니다.

AEM as a Windows 서비스를 설치하고 시작하려면 다음을 수행하십시오.

1. 텍스트 편집기에서 crx-quickstart\opt\helpers\instsrv.bat 파일을 엽니다.
1. 64비트 Windows 서버를 구성하는 경우 운영 체제에 따라 prunsrv의 모든 인스턴스를 다음 명령 중 하나로 바꿉니다.

   * prunsrv_amd64
   * prunsrv_ia64

   이 명령은 32비트 Java 대신 64비트 Java로 Windows 서비스 데몬을 시작하는 적절한 스크립트를 호출합니다.

1. 프로세스가 두 개 이상의 프로세스로 바뀌지 않도록 하려면 PermGen JVM 매개 변수를 늘립니다. `set jvm_options` 명령을 찾아 다음과 같이 값을 설정합니다.

   `set jvm_options=-Xmx1792m`

1. 명령 프롬프트를 열고 현재 디렉터리를 AEM 설치의 crx-quickstart/opt/helpers 폴더로 변경하고 다음 명령을 입력하여 서비스를 만듭니다.

   `instsrv.bat cq5`

   서비스가 만들어졌는지 확인하려면 [관리 도구] 제어판에서 [서비스]를 열거나 명령 프롬프트에서 `start services.msc`을(를) 입력하십시오. cq5 서비스가 목록에 나타납니다.

1. 다음 중 하나를 수행하여 서비스를 시작합니다.

   * 서비스 제어판에서 cq5를 클릭하고 시작을 클릭합니다.

   ![chlimage_1-11](assets/chlimage_1-11.png)

   * 명령줄에 net start cq5를 입력합니다.

   ![chlimage_1-12](assets/chlimage_1-12.png)

1. Windows는 서비스가 실행 중임을 나타냅니다. AEM이 시작되고 작업 관리자에 prunsrv 실행 파일이 나타납니다. 웹 브라우저에서 AEM(예: `https://localhost:4502`)로 이동하여 AEM을 시작합니다.

   ![chlimage_1-13](assets/chlimage_1-13.png)

>[!NOTE]
>
>instsrv.bat 파일의 속성 값은 Windows 서비스를 만들 때 사용됩니다. instsrv.bat에서 속성 값을 편집하는 경우 서비스를 제거한 다음 다시 설치해야 합니다.

>[!NOTE]
>
>AEM as service를 설치할 때 Configuration Manager에서 `com.adobe.xmp.worker.files.ncomm.XMPFilesNComm`의 로그 디렉터리에 대한 절대 경로를 제공해야 합니다.

서비스를 제거하려면 **서비스** 제어판 또는 명령줄에서 **중지**&#x200B;를 클릭하고 폴더로 이동한 다음 `instsrv.bat -uninstall cq5`을(를) 입력하십시오. `net start`을(를) 입력하면 **서비스** 제어판의 목록 또는 명령줄의 목록에서 서비스가 제거됩니다.

## 임시 작업 디렉터리 위치 재정의 {#redefining-the-location-of-the-temporary-work-directory}

Java 컴퓨터의 임시 폴더의 기본 위치는 `/tmp`입니다. AEM은 패키지를 빌드할 때 이 폴더도 사용합니다.

임시 폴더의 위치를 변경하려면(예: 사용 가능한 공간이 더 많은 디렉터리가 필요한 경우) JVM 매개 변수를 추가하여 * `<new-tmp-path>`*을(를) 정의합니다.

`-Djava.io.tmpdir="/<*new-tmp-path*>"`

다음 중 하나를 수행합니다.

* 서버 시작 명령줄
* serverctl 또는 시작 스크립트의 CQ_JVM_OPTS 환경 매개 변수

## 빠른 시작 파일에서 사용할 수 있는 추가 옵션 {#further-options-available-from-the-quickstart-file}

추가 옵션 및 이름 바꾸기 규칙은 -help 옵션을 통해 사용할 수 있는 빠른 시작 도움말 파일에 설명되어 있습니다. 도움말에 액세스하려면 다음을 입력합니다.

* `java -jar cq-quickstart-6.5.0.jar -help`

>[!CAUTION]
>
>이러한 옵션은 AEM 6.5(6.5.0.0)의 원래 릴리스부터 유효합니다. 이후 SP 릴리즈에서는 변경이 가능합니다.

```shell
Loading quickstart properties: default
Loading quickstart properties: instance
Setting properties from filename '/Users/Desktop/AEM/cq-quickstart-6.5.0.jar'
--------------------------------------------------------------------------------
Adobe Experience Manager Quickstart (build 20190328)                            
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
-nointeractive
         Start with no interactivity                                            
-ll <level>
         Define launchpad log level (1 = error...4 = debug)                     
-n   
         Do not install shutdown hook                                           
-D<property>=<value>
         Additional framework properties.                                       
-listener-port <listener-port>
         Set listener port number                                               
-x <string>
         Run a Quickstart extension.                                            
  Options for executing Quickstart extensions:
                                                                                
    -xargs <arg> [<arg> ...]
         Construct an arguments list for a Quickstart extension (for example, -xargs -- 
         -arg1 val1 -arg2 val2).                                                
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
         Include -publish in the renamed jar filename to run in "publish" mode, 
         example: cq-publish-7502.jar                                           
-dynamicmedia
         Include -dynamicmedia in the renamed jar filename to run in            
         "dynamicmedia" mode, example: quickstart-dynamicmedia-4502.jar         
-dynamicmedia_scene7
         Include -dynamicmedia_scene7 in the renamed jar filename to run in     
         "dynamicmedia_scene7" mode, example:                                   
         quickstart-dynamicmedia_scene7-p4502.jar                               
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
  /Users/aemdocs/CQInstallationKits/AEM-65150-L8/crx-quickstart/logs.           
--------------------------------------------------------------------------------
```

## Amazon EC2 환경에 AEM 설치 {#installing-aem-in-the-amazon-ec-environment}

Amazon Elastic Compute Cloud(EC2) 인스턴스에 AEM을 설치할 때 EC2 인스턴스에 작성자와 게시를 모두 설치하면 작성자 인스턴스가 [AEM Manager의 인스턴스 설치](#installinginstancesofaemmanager)의 절차에 따라 올바르게 설치됩니다. 그러나 게시 인스턴스는 작성자가 됩니다.

EC2 환경에 게시 인스턴스를 설치하기 전에 다음을 수행하십시오.

1. 인스턴스를 처음 시작하기 전에 Publish 인스턴스에 대한 jar 파일의 압축을 풉니다. 파일의 압축을 풀려면 다음 명령을 사용합니다.

   ```xml
   java -jar quickstart.jar -unpack
   ```

   >[!NOTE]
   >
   >인스턴스를 처음 시작하는 **after** 모드를 변경하면 실행 모드를 변경할 수 없습니다.

1. 다음을 실행하여 인스턴스를 시작합니다.

   ```xml
   java -jar quickstart.jar -r publish
   ```

   >[!CAUTION]
   >
   >위의 명령을 실행하여 인스턴스의 압축을 푼 후에 먼저 인스턴스를 실행해야 합니다. 그렇지 않으면 quickstart.properties 채우기가 생성되지 않습니다. 이 파일이 없으면 향후 AEM 업그레이드가 실패합니다.

1. **bin** 폴더에서 **start** 스크립트를 열고 다음 섹션을 확인하십시오.

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='author'
   fi
   ```

1. 실행 모드를 **publish**(으)로 변경하고 파일을 저장합니다.

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='publish'
   fi
   ```

1. 인스턴스를 중지하고 **start** 스크립트를 실행하여 다시 시작하십시오.

## 설치 확인 {#verifying-the-installation}

다음 링크를 사용하여 설치가 작동하는지 확인할 수 있습니다(모든 예제는 인스턴스가 localhost의 포트 8080에서 실행 중이고 CRX이 /crx 아래에 설치되어 있으며 / 아래의 Launchpad에 설치되어 있음을 기반으로 함).

* `https://localhost:8080/crx/de`
CRXDE Lite 콘솔.

* `https://localhost:8080/system/console`
웹 콘솔.

## 설치 후 작업 {#actions-after-installation}

AEM WCM을 구성할 수 있는 많은 가능성이 있지만 특정 작업을 수행하거나 설치 후 즉시 검토해야 합니다.

* 시스템의 보안을 유지하는 데 필요한 작업은 [보안 확인 목록](/help/sites-administering/security-checklist.md)을 참조하세요.
* AEM WCM과 함께 설치된 기본 사용자 및 그룹 목록을 검토합니다. 다른 계정에 대해 작업을 수행할지 여부를 확인하십시오. 자세한 내용은 [보안 및 사용자 관리](/help/sites-administering/security.md)를 참조하십시오.

## CRXDE Lite 및 웹 콘솔 액세스 {#accessing-crxde-lite-and-the-web-console}

AEM WCM이 시작되면 다음에 액세스할 수도 있습니다.

* [CRXDE Lite](#accessing-crxde-lite) - 저장소에 액세스하고 관리하는 데 사용됨
* [웹 콘솔](#accessing-the-web-console) - OSGi 번들(OSGi 콘솔이라고도 함)을 관리하거나 구성하는 데 사용됩니다.

### CRXDE Lite 액세스 {#accessing-crxde-lite}

CRXDE Lite 시작 화면에서 **CRXDE Lite**&#x200B;을(를) 선택하거나 브라우저를 사용하여 다음 위치로 이동할 수 있습니다.

```
 https://<<i>host</i>>:<<i>port</i>>/crx/de/index.jsp
```

예:
`https://localhost:4502/crx/de/index.jsp`

![installcq_crxdelite](assets/installcq_crxdelite.png)

#### 웹 콘솔 액세스 {#accessing-the-web-console}

Adobe CQ 웹 콘솔에 액세스하려면 시작 화면에서 **OSGi 콘솔**&#x200B;을 선택하거나 브라우저를 사용하여 다음 위치로 이동할 수 있습니다.

```
 https://<host>:<port>/system/console
```

예:
`https://localhost:4502/system/console`
또는 번들 페이지의 경우
`https://localhost:4502/system/console/bundles`

![chlimage_1-14](assets/chlimage_1-14.png)

자세한 내용은 [웹 콘솔과 함께 OSGi 구성](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)을 참조하십시오.

## 문제 해결 {#troubleshooting}

설치 중에 발생할 수 있는 문제 처리에 대한 자세한 내용은 다음을 참조하십시오.

* [문제 해결](/help/sites-deploying/troubleshooting.md)

## Adobe Experience Manager 제거 {#uninstalling-adobe-experience-manager}

AEM은 단일 디렉터리에 설치되므로 제거 유틸리티가 필요하지 않습니다. AEM 제거 방법은 달성하려는 내용과 사용하는 영구 스토리지에 따라 다르지만 제거 방법은 전체 설치 디렉토리를 삭제하는 것만큼 간단할 수 있습니다.

영구 스토리지가 설치 디렉토리(예: 기본 TarPM 설치)에 포함된 경우 폴더를 삭제하면 데이터도 제거됩니다.

>[!NOTE]
>
>Adobe은 AEM을 삭제하기 전에 저장소를 백업하는 것을 적극 권장합니다. 전체 &lt;cq-installation-directory>를 삭제하면 저장소가 삭제됩니다. 삭제하기 전에 저장소 데이터를 유지하려면 다른 폴더를 삭제하기 전에 &lt;cq-installation-directory>/crx-quickstart/repository 폴더를 다른 위치로 이동하거나 복사하십시오.

AEM 설치 시 데이터베이스 서버와 같은 외부 스토리지를 사용하는 경우 폴더를 제거해도 데이터가 자동으로 제거되지는 않지만 스토리지 구성은 제거되므로 JCR 콘텐츠를 복원하기가 어렵습니다.
