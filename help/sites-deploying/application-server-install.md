---
title: 애플리케이션 서버 설치
seo-title: Application Server Install
description: 애플리케이션 서버와 함께 AEM을 설치하는 방법을 알아봅니다.
seo-description: Learn how to install AEM with an application server.
uuid: c9571f80-6ed1-46fe-b7c3-946658dfc3f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6fdce35d-2709-41cc-87fb-27a4b867e960
exl-id: 3a90f1d2-e53f-4cc4-8122-024ad6500de0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 0%

---

# 애플리케이션 서버 설치{#application-server-install}

>[!NOTE]
>
>`JAR` 및 `WAR` AEM의 파일 유형은에서 릴리스됩니다. 이러한 형식은 Adobe이 커밋한 지원 수준을 수용하기 위해 품질 보증을 받습니다.

이 섹션에서는 애플리케이션 서버와 함께 AEM(Adobe Experience Manager)을 설치하는 방법을 설명합니다. 자세한 내용은 [지원되는 플랫폼](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) 섹션을 참조하십시오.

다음 응용 프로그램 서버의 설치 단계는 다음과 같습니다.

* [WebSphere 8.5](#websphere)
* [JBoss EAP 6.3.0/6.4.0](#jboss-eap)
* [Oracle WebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

웹 응용 프로그램 설치, 서버 구성 및 서버 시작 및 중지 방법에 대한 자세한 내용은 해당 응용 프로그램 서버 설명서를 참조하십시오.

>[!NOTE]
>
>WAR 배포에서 Dynamic Media을 사용하는 경우 다음을 참조하십시오. [Dynamic Media 설명서](/help/assets/config-dynamic.md#enabling-dynamic-media).

## 일반 설명 {#general-description}

### Application Server에 AEM 설치 시 기본 동작 {#default-behaviour-when-installing-aem-in-an-application-server}

AEM은 배포할 단일 전쟁 파일로 제공됩니다.

배포된 경우 기본적으로 다음 문제가 발생합니다.

* 실행 모드는 다음과 같습니다. `author`
* 인스턴스(저장소, Felix OSGI 환경, 번들 등)는 에 설치되어 있습니다. `${user.dir}/crx-quickstart`여기서 `${user.dir}` 는 현재 작업 디렉토리이며 crx-quickstart의 이 경로는 라고 합니다. `sling.home`

* 컨텍스트 루트는 전쟁 파일 이름(예: )입니다. `aem-6`

#### 구성 {#configuration}

다음과 같은 방법으로 기본 동작을 변경할 수 있습니다.

* 실행 모드 : 구성 `sling.run.modes` 의 매개 변수 `WEB-INF/web.xml` 배포 전 AEM 전쟁 파일 파일

* sling.home: 구성 `sling.home` 의 매개 변수 `WEB-INF/web.xml`배포 전 AEM 전쟁 파일 파일

* 컨텍스트 루트: AEM war 파일 이름 바꾸기

#### 설치 게시 {#publish-installation}

게시 인스턴스를 배포하려면 게시 실행 모드를 설정해야 합니다.

* AEM War 파일에서 WEB-INF/web.xml 파일의 압축을 해제합니다.
* sling.run.modes 매개 변수를 게시로 변경합니다.
* web.xml 파일을 AEM war 파일에 다시 채우기
* AEM 전쟁 파일 배포

#### 설치 확인 {#installation-check}

모두 설치되어 있는지 확인하려면 다음을 수행하십시오.

* 꼬리를 잡다 `error.log`모든 컨텐츠가 설치되었는지 확인하는 파일
* 검색 `/system/console` 모든 번들이 설치되어 있습니다.

#### 동일한 응용 프로그램 서버에 두 개의 인스턴스 {#two-instances-on-the-same-application-server}

데모 목적으로 하나의 애플리케이션 서버에 작성자 및 게시 인스턴스를 설치하는 것이 적절할 수 있습니다. 이에 대해 다음을 수행합니다.

1. 게시 인스턴스의 sling.home 변수 및 sling.run.modes 변수를 변경합니다.
1. AEM war 파일에서 WEB-INF/web.xml 파일의 압축을 해제합니다.
1. sling.home 매개 변수를 다른 경로로 변경합니다(절대 및 상대 경로가 가능).
1. 게시 인스턴스에 대해 게시하도록 sling.run.modes를 변경합니다.
1. web.xml 파일을 다시 채웁니다.
1. 전쟁 파일의 이름을 바꾸면 이름이 다릅니다. 예: 한 이름은 aemauthor.war로 변경하고 다른 이름은 aempublish.war로 변경합니다.
1. 예를 들어, 기본 AEM 인스턴스용(예: -Xmx3072m
1. 두 개의 웹 애플리케이션을 배포합니다.
1. 배포 후 두 웹 응용 프로그램을 중지합니다.
1. 작성자 및 게시 인스턴스 둘 다에서 sling.properties 파일에서 felix.service.urlhandler=false 속성이 false(기본값은 true로 설정됨)로 설정되어 있는지 확인합니다.
1. 두 웹 애플리케이션을 다시 시작합니다.

## 응용 프로그램 서버 설치 절차 {#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

배포하기 전에 [일반 설명](#general-description) 위에 표시됩니다.

**서버 준비**

* 기본 인증 헤더를 통과하도록 합니다.

   * AEM에서 사용자를 인증하는 한 가지 방법은 WebSphere 서버의 전역 관리 보안을 비활성화하여 다음과 같이 하는 것입니다. 보안 -> 전역 보안으로 이동하여 관리 보안 활성화 확인란의 선택을 취소하고 서버를 저장하고 다시 시작합니다.

* set `"JAVA_OPTS= -Xmx2048m"`
* 컨텍스트 루트 = / 를 사용하여 AEM을 설치하려면 먼저 기존 기본 웹 애플리케이션의 컨텍스트 루트를 변경해야 합니다

**AEM 웹 애플리케이션 배포**

* AEM 전쟁 파일 다운로드
* 필요한 경우 web.xml에서 구성을 만듭니다(일반 설명에서 위 사항 참조)

   * WEB-INF/web.xml 파일 압축 해제
   * sling.run.modes 매개 변수를 게시로 변경
   * sling.home 초기 매개 변수에 대한 주석을 해제하고 이 경로를 필요에 따라 설정합니다.
   * web.xml 파일 다시 추적

* AEM 전쟁 파일 배포

   * 컨텍스트 루트를 선택합니다. sling 실행 모드를 설정하려면 배포 마법사의 세부 단계를 선택한 다음 마법사의 6단계에서 지정해야 합니다.

* AEM 웹 애플리케이션 시작

#### JBoss EAP 6.3.0/6.4.0 {#jboss-eap}

배포하기 전에 [일반 설명](#general-description) 위에 표시됩니다.

**JBoss 서버 준비**

conf 파일(예: `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

에 배포 스캐너를 사용하여 AEM 웹 응용 프로그램을 설치하는 경우 `deployment-timeout,` 설정 `deployment-timeout` 인스턴스의 xml 파일에 있는 속성(예: `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**AEM 웹 애플리케이션 배포**

* JBoss 관리 콘솔에서 AEM 웹 애플리케이션을 업로드합니다.

* AEM 웹 응용 프로그램을 활성화합니다.

#### Oracle WebLogic 12.1.3/12.2 {#oracle-weblogic}

배포하기 전에 [일반 설명](#general-description) 위에 표시됩니다.

여기서는 관리 서버만 있는 간단한 서버 레이아웃을 사용합니다.

**WebLogic Server 준비**

* in `${myDomain}/config/config.xml`security-configuration 섹션에 를 추가합니다.

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` 다음 참조 [https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) 올바른 위치에 대해(기본적으로 섹션의 끝에 위치를 지정하도록 되어 있음)

* VM 메모리 설정 증가:

   * open `${myDomain}/bin/setDomainEnv.cmd` (resp.sh)WLS_MEM_ARGS를 검색하고, 예: 설정됨 `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * WebLogic Server 다시 시작

* 만들기 위치 `${myDomain}` 패키지 폴더 및 cq 폴더 내부 및 계획 폴더

**AEM 웹 애플리케이션 배포**

* AEM 전쟁 파일 다운로드
* ${myDomain}/packages/cq 폴더에 AEM war 파일을 넣습니다
* 구성 만들기 `WEB-INF/web.xml` 필요한 경우(일반 설명에서 위 사항 참조)

   * 압축 해제 `WEB-INF/web.xml`파일
   * sling.run.modes 매개 변수를 게시로 변경
   * sling.home 초기 매개 변수의 주석을 해제하고 필요한 대로 이 경로를 설정합니다(일반 설명 참조).
   * web.xml 파일 다시 추적

* AEM war 파일을 응용 프로그램으로 배포합니다(다른 설정의 경우 기본 설정을 사용).
* 설치하는 데 시간이 걸릴 수 있습니다.
* 일반 설명(예: error.log 추적)에서 위에서 언급한 대로 설치가 완료되었는지 확인합니다
* WebLogic에서 웹 응용 프로그램의 구성 탭에서 컨텍스트 루트를 변경할 수 있습니다 `/console`

#### Tomcat 8/8.5 {#tomcat}

배포하기 전에 [일반 설명](#general-description) 위에 표시됩니다.

* **Tomcat 서버 준비**

   * VM 메모리 설정 증가:

      * in `bin/catalina.bat` (resp) `catalina.sh` unix에서 다음 설정을 추가합니다.
      * `set "JAVA_OPTS= -Xmx2048m`
   * Tomcat은 설치 시 관리자 및 관리자 액세스를 허용하지 않습니다. 따라서 수동으로 편집해야 합니다 `tomcat-users.xml` 다음 계정에 대한 액세스를 허용합니다.

      * 편집 `tomcat-users.xml` 관리자 및 관리자에 대한 액세스 권한을 포함합니다. 구성은 다음 예와 유사해야 합니다.

         ```xml
         <?xml version='1.0' encoding='utf-8'?>
         <tomcat-users>
         role rolename="manager"/>
         role rolename="tomcat"/>
         <role rolename="admin"/>
         <role rolename="role1"/>
         <role rolename="manager-gui"/>
         <user username="both" password="tomcat" roles="tomcat,role1"/>
         <user username="tomcat" password="tomcat" roles="tomcat"/>
         <user username="admin" password="admin" roles="admin,manager-gui"/>
         <user username="role1" password="tomcat" roles="role1"/>
         </tomcat-users>
         ```
   * 컨텍스트 루트 &quot;/&quot;와 함께 AEM을 배포하려면 기존 ROOT 웹 앱의 컨텍스트 루트를 변경해야 합니다.

      * ROOT 웹 앱 중지 및 배포 취소
      * tomcat 웹 앱 폴더에서 ROOT.war 폴더의 이름을 변경합니다
      * 웹 앱 다시 시작
   * manager-gui를 사용하여 AEM 웹 애플리케이션을 설치하는 경우 기본적으로 50MB 업로드 크기만 허용하므로 업로드된 파일의 최대 크기를 늘려야 합니다. 이렇게 하면 manager 웹 응용 프로그램의 web.xml이 열립니다.

      `webapps/manager/WEB-INF/web.xml`

      최대 파일 크기와 최대 요청 크기를 최소 500MB로 늘린 후 다음을 참조하십시오 `multipart-config` 예 `web.xml` 파일.

      ```xml
      <multipart-config>
      <!-- 500MB max -->
      <max-file-size>524288000</max-file-size>
      <max-request-size>524288000</max-request-size>
      <file-size-threshold>0</file-size-threshold>
      </multipart-config>
      ```




* **AEM 웹 애플리케이션 배포**

   * AEM 전쟁 파일 다운로드
   * 필요한 경우 web.xml에서 구성을 만듭니다(일반 설명에서 위 사항 참조)

      * WEB-INF/web.xml 파일 압축 해제
      * sling.run.modes 매개 변수를 게시로 변경
      * sling.home 초기 매개 변수에 대한 주석을 해제하고 이 경로를 필요에 따라 설정합니다.
      * web.xml 파일 다시 추적
   * 루트 웹 앱으로 배포하려면 AEM war 파일의 이름을 ROOT.war로 변경하고, 컨텍스트 루트로 aemauthor.war로 이름을 변경합니다
   * tomcat 웹 앱 폴더에 복사합니다.
   * AEM이 설치될 때까지 대기


## 문제 해결 {#troubleshooting}

설치 중에 발생할 수 있는 문제를 처리하는 방법에 대한 자세한 내용은 다음을 참조하십시오.

* [문제 해결](/help/sites-deploying/troubleshooting.md)
