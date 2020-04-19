---
title: AEM Forms 서버 성능 조정
seo-title: AEM Forms 서버 성능 조정
description: AEM Forms가 최적으로 수행되도록 하려면 캐시 설정 및 JVM 매개 변수를 세밀하게 조정할 수 있습니다. 또한 웹 서버를 사용하면 AEM Forms 배포의 성능을 향상시킬 수 있습니다.
seo-description: AEM Forms가 최적으로 수행되도록 하려면 캐시 설정 및 JVM 매개 변수를 세밀하게 조정할 수 있습니다. 또한 웹 서버를 사용하면 AEM Forms 배포의 성능을 향상시킬 수 있습니다.
uuid: bf23b62c-7559-4726-8f4e-cc8b1457e501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 38c0ec46-5686-4656-bfb4-7125ec194673
docset: aem65
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# AEM Forms 서버 성능 조정{#performance-tuning-of-aem-forms-server}

이 문서에서는 병목 현상을 줄이고 AEM Forms 배포의 성능을 최적화하기 위해 구현할 수 있는 전략 및 우수 사례에 대해 설명합니다.

## 캐시 설정 {#cache-settings}

AEM Web Configuration Console에서 모바일 양식 구성 **구성 요소를 사용하여 AEM Forms** 캐싱 전략을 구성하고 제어할 수 있습니다.

* (OSGi의 AEM Forms) `https://'[server]:[port]'/system/console/configMgr`
* (AEM Forms on JEE) `https://'[server]:[port]'/lc/system/console/configMgr`

캐싱에 사용할 수 있는 옵션은 다음과 같습니다.

* **없음**:아티팩트를 캐시하지 않도록 강제 적용합니다. 따라서 실제로 성능이 저하되고 캐시가 없기 때문에 메모리 가용성이 높아집니다.
* **보수적**:인라인 조각 및 이미지가 포함된 템플릿과 같이 양식을 렌더링하기 전에 생성된 중간 가공물만 캐시하도록 지시합니다.
* **공격적**:강제 적용은 [보존] 캐싱 수준의 모든 객체 외에도 렌더링된 HTML 컨텐츠를 포함하여 캐싱할 수 있는 거의 모든 객체를 캐시합니다. 최상의 성능을 얻을 수 있지만 캐시된 객체를 저장하는 데 더 많은 메모리를 사용합니다. 공격적인 캐싱 전략을 사용하면 렌더링된 컨텐츠가 캐싱될 때 양식을 렌더링할 때 일정한 시간 성능을 얻을 수 있습니다.

AEM Forms에 대한 기본 캐시 설정이 최적 성능을 달성하기에 충분하지 않을 수 있습니다. 따라서 다음 설정을 사용하는 것이 좋습니다.

* **캐시 전략**:공격적
* **캐시 크기** (양식 수):필요한 경우
* **최대 개체 크기**:필요한 경우

![모바일 양식 구성](assets/snap.png)

>[!NOTE]
>
>AEM Dispatcher를 사용하여 적응형 양식을 캐싱하는 경우, 사전 채워진 데이터가 있는 양식이 포함된 적응형 양식도 캐시합니다. 이러한 양식이 AEM Dispatcher 캐시에서 제공되는 경우 사용자에게 사전 채워진 데이터 또는 오래된 데이터를 제공할 수 있습니다. 따라서 AEM Dispatcher를 사용하여 사전 채워진 데이터를 사용하지 않는 적응형 양식을 캐시합니다. 또한 디스패처 캐시는 캐시된 조각을 자동으로 무효화하지 않습니다. 따라서 양식 조각을 캐시하는 데 사용하지 마십시오. 이러한 양식 및 조각은 적응형 양식 [캐시를](../../forms/using/configure-adaptive-forms-cache.md)사용합니다.

## JVM 매개 변수 {#jvm-parameters}

최적의 성능을 위해 다음 JVM `init` 인수를 사용하여 `Java heap` 및 `PermGen`를 구성하는 것이 좋습니다.

```java
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xms8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xmx8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:PermSize=256m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:MaxPermSize=1024m
```

>[!NOTE]
>
>권장 설정은 Windows 2008 R2 8 Core 및 Oracle HotSpot 1.7(64비트) JDK용이며 시스템 구성에 따라 확대되거나 축소되어야 합니다.

## 웹 서버 사용 {#using-a-web-server}

적응형 양식 및 HTML5 양식은 HTML5 형식으로 렌더링됩니다. 결과 출력은 양식의 양식 크기 및 이미지와 같은 요소에 따라 클 수 있습니다. 데이터 전송을 최적화하기 위해 요청을 제공하는 웹 서버를 사용하여 HTML 응답을 압축하는 것이 좋습니다. 이 방법을 사용하면 응답 크기, 네트워크 트래픽 및 서버와 클라이언트 시스템 간의 데이터를 스트리밍하는 데 필요한 시간이 줄어듭니다.

예를 들어 다음 단계를 수행하여 JBoss에서 Apache Web Server 2.0 32비트에서 압축을 활성화합니다.

>[!NOTE]
>
>다음 지침은 Apache Web Server 2.0 32비트 이외의 서버에는 적용되지 않습니다. 다른 서버에 대한 단계는 해당 제품 설명서를 참조하십시오.

다음 단계에서는 Apache 웹 서버와의 압축을 활성화하는 데 필요한 변경 사항을 보여 줍니다

**운영 체제에 적용 가능한 Apache 웹 서버 소프트웨어 얻기**

* Windows:apache HTTP Server 프로젝트 사이트에서 Apache 웹 서버를 다운로드합니다.
* Solaris 64비트:solaris용 Sunfreeware 웹 사이트에서 Apache 웹 서버를 다운로드합니다.
* Linux:apache 웹 서버는 Linux 시스템에 미리 설치되어 있습니다.

HTTP 프로토콜을 사용하여 CRX와 통신할 수 있습니다. 구성은 HTTP를 사용한 최적화를 위한 것입니다.

1. 다음 모듈 구성의 주석을 `APACHE_HOME/conf/httpd.conf` 파일에서 해제합니다.

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Linux의 경우 기본값은 `APACHE_HOME` 입니다 `/etc/httpd/`.

1. crx의 포트 4502에서 프록시를 구성합니다.
구성 파일에 다음 구성을 `APACHE_HOME/conf/httpd.conf` 추가합니다.

   ```java
   ProxyPass / https://<server>:4502/
   ProxyPassReverse / https://<server>:4502/
   ```

1. 압축 사용을 참조하십시오. 구성 파일에 다음 구성을 `APACHE_HOME/conf/httpd.conf` 추가합니다.

   **HTML5 양식**

   ```java
   <Location /content/xfaforms>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Don’t compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   **적응형 양식**

   ```java
   <Location /content/forms/af>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Don’t compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   crx 서버에 액세스하려면 를 `https://'server':80`사용합니다. 여기서 는 Apache 서버가 실행 중인 서버의 `server` 이름입니다.

## AEM Forms를 실행하는 서버에서 바이러스 백신 사용 {#using-an-antivirus-on-server-running-aem-forms}

바이러스 백신 소프트웨어를 실행하는 서버에서는 성능이 저하될 수 있습니다. 바이러스 백신(On-Access 스캔) 소프트웨어는 시스템의 모든 파일을 스캔합니다. 서버 및 AEM Forms의 성능이 저하될 수 있습니다.

성능을 개선하기 위해 바이러스 백신 소프트웨어에서 다음 AEM Forms 파일 및 폴더를 항상 설정(액세스 시) 스캔에서 제외하도록 할 수 있습니다.

* AEM 설치 디렉토리. 전체 디렉토리를 제외할 수 없는 경우 다음을 제외하십시오.

   * [AEM 설치 디렉토리]\crx-repository\temp
   * [AEM 설치 디렉토리]\crx-repository\repository
   * [AEM 설치 디렉토리]\crx-repository\launchpad

* 응용 프로그램 서버 임시 디렉토리. 기본 위치는 다음과 같습니다.

   * (Jboss) [AEM 설치 디렉토리]\jboss\standalone\tmp
   * (Weblogic) \Oracle\Middleware\user_projects\domains\LCDomain\servers\LCServer1\tmp
   * (Websphere) \Program Files\IBM\WebSphere\AppServer\profiles\AppSrv01\temp

* **(JEE의 AEM Forms 전용)** 전역 문서 저장소(GDS) 디렉토리. 기본 위치는 다음과 같습니다.

   * (JBoss) [appserver root]/server/&#39;server&#39;/svconcreative/DocumentStorage
   * (WebLogic) [appserverdomain]/&#39;server&#39;/adobe/LiveCycleServer/DocumentStorage
   * (WebSphere) [appserver root]/installedApps/adobe/&#39;server&#39;/DocumentStorage

* **(JEE의 AEM Forms 전용)** AEM Forms 서버 로그 및 임시 디렉토리 기본 위치는 다음과 같습니다.

   * 서버 로그 - [AEM Forms 설치 디렉토리]\Adobe\AEM forms\[app-server]\server\all\logs
   * 임시 디렉토리 - [AEM Forms 설치 디렉토리]\temp

>[!NOTE]
>
>* GDS 및 임시 디렉토리에 대해 다른 위치를 사용하는 경우 에서 AdminUI를 열고 홈 > 설정 > 핵심 시스템 `https://'[server]:[port]'/adminui`설정 > 핵심 구성으로 **** 이동하여 사용 중인 위치를 확인합니다.

* AEM Forms 서버가 제안된 디렉터리를 제외하고도 느리게 수행되는 경우 Java 실행 파일(java.exe)도 제외합니다.



