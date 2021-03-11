---
title: 애플리케이션 서버 설치
seo-title: 애플리케이션 서버 설치
description: 응용 프로그램 서버와 함께 AEM을 설치하는 방법을 알아봅니다.
seo-description: 응용 프로그램 서버와 함께 AEM을 설치하는 방법을 알아봅니다.
uuid: c9571f80-6ed1-46fe-b7c3-946658dfc3f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6fdce35d-2709-41cc-87fb-27a4b867e960
translation-type: tm+mt
source-git-commit: 4090b1641467c6fb02b2fcce4df97b9fd5da4e2f
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 1%

---


# 애플리케이션 서버 설치{#application-server-install}

>[!NOTE]
>
>`JAR` AEM `WAR` 의 파일 유형은 이러한 형식은 Adobe이 커밋한 지원 수준을 충족하기 위해 품질 보증을 받습니다.


이 섹션에서는 응용 프로그램 서버와 함께 Adobe Experience Manager(AEM)을 설치하는 방법을 설명합니다. 개별 응용 프로그램 서버에 제공된 특정 지원 수준을 보려면 [지원되는 플랫폼](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) 섹션을 참조하십시오.

다음 응용 프로그램 서버의 설치 단계는 다음과 같습니다.

* [WebSphere 8.5](#websphere)
* [JBoss EAP 6.3.0/6.4.0](#jboss-eap)
* [Oracle WebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

웹 응용 프로그램, 서버 구성 및 서버 시작 및 중지 방법에 대한 자세한 내용은 해당 응용 프로그램 서버 설명서를 참조하십시오.

>[!NOTE]
>
>WAR 배포에 Dynamic Media을 사용하는 경우 [Dynamic Media 설명서](/help/assets/config-dynamic.md#enabling-dynamic-media)를 참조하십시오.

## 일반 설명 {#general-description}

### 응용 프로그램 서버 {#default-behaviour-when-installing-aem-in-an-application-server}에 AEM을 설치할 때의 기본 동작

AEM은 단일 배포 파일로 제공됩니다.

배포되는 경우 기본적으로 다음이 발생합니다.

* 실행 모드는 `author`입니다.
* 인스턴스(저장소, Felix OSGI 환경, 번들 등) `${user.dir}/crx-quickstart`에 설치되고 여기서 `${user.dir}`은(는) 현재 작업 디렉터리이며 crx-quickstart에 대한 이 경로는 `sling.home`라고 합니다.

* 컨텍스트 루트는 전쟁 파일 이름입니다(예: :).`aem-6`

#### 구성 {#configuration}

다음과 같은 방법으로 기본 동작을 변경할 수 있습니다.

* run mode :배포하기 전에 AEM war 파일의 `WEB-INF/web.xml` 파일에 있는 `sling.run.modes` 매개 변수를 구성합니다.

* sling.home:배포하기 전에 AEM 전쟁 파일의 `WEB-INF/web.xml`파일에 있는 `sling.home` 매개 변수를 구성합니다.

* 컨텍스트 루트:AEM war 파일 이름 변경

#### 설치 게시 {#publish-installation}

게시 인스턴스를 배포하려면 게시 실행 모드를 설정해야 합니다.

* AEM War 파일의 WEB-INF/web.xml파일을 압축 해제합니다.
* sling.run.modes 매개 변수를 게시로 변경
* web.xml 파일을 AEM war 파일로 저장
* AEM 전쟁 파일 배포

#### 설치 검사 {#installation-check}

모든 것이 설치되어 있는지 확인하려면 다음을 수행할 수 있습니다.

* `error.log`파일을 뒤틀어 모든 컨텐츠가 설치되었는지 확인
* `/system/console`에서 모든 번들이 설치되어 있는지 확인합니다.

#### 동일한 응용 프로그램 서버에 있는 인스턴스 두 개 {#two-instances-on-the-same-application-server}

데모용으로 하나의 애플리케이션 서버에 작성자 및 게시 인스턴스를 설치하는 것이 적절할 수 있습니다. 이렇게 하려면 다음을 수행합니다.

1. 게시 인스턴스의 sling.home 변수와 sling.run.modes 변수를 변경합니다.
1. AEM War 파일의 WEB-INF/web.xml 파일을 압축 해제합니다.
1. sling.home 매개 변수를 다른 패스로 변경합니다(절대 패스와 상대 경로가 가능함).
1. 게시 인스턴스에 대해 게시하도록 sling.run.modes를 변경합니다.
1. web.xml 파일을 반환합니다.
1. 전쟁 파일의 이름을 변경하여 이름이 다르게 지정합니다.예: 한 이름은 aemauthor.war로, 다른 이름은 aempublish.war로 바꿉니다.
1. 더 높은 메모리 설정(예: 기본 AEM 인스턴스의 경우:-Xmx3072m
1. 두 웹 애플리케이션을 배포합니다.
1. 배포 후 2개의 웹 응용 프로그램을 중지합니다.
1. author 및 publish 인스턴스는 sling.properties 파일에서 property felix.service.urlhandlhandlers=false가 false로 설정되도록 합니다(기본값은 true로 설정됨).
1. 두 웹 애플리케이션을 다시 시작합니다.

## 응용 프로그램 서버 설치 절차 {#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

배포가 실행되기 전에 위의 [일반 설명](#general-description)을 읽으십시오.

**서버 준비**

* 기본 인증 헤더가 전달하도록 허용:

   * AEM에서 사용자를 인증할 수 있는 한 가지 방법은 WebSphere 서버의 전역 관리 보안을 비활성화하는 것입니다.보안 -> 글로벌 보안으로 이동하고 관리 보안 활성화 체크 상자의 선택을 취소하고 서버를 저장하고 다시 시작합니다.

*  설정`"JAVA_OPTS= -Xmx2048m"`
* 컨텍스트 루트 = / 를 사용하여 AEM을 설치하려면 먼저 기존 기본 웹 애플리케이션의 컨텍스트 루트를 변경해야 합니다

**AEM 웹 애플리케이션 배포**

* AEM 전쟁 파일 다운로드
* 필요한 경우 web.xml에서 구성을 만듭니다(일반 설명에서 위 참조).

   * WEB-INF/web.xml 파일 압축 해제
   * 게시할 sling.run.modes 매개 변수 변경
   * sling.home의 초기 매개 변수에 주석을 달고 필요한 대로 이 경로를 설정합니다.
   * web.xml 파일 복구

* AEM 전쟁 파일 배포

   * 컨텍스트 루트 선택(sling run mode를 설정하려면 배포 마법사의 세부 단계를 선택한 다음 마법사의 6단계에서 지정합니다.)

* AEM 웹 응용 프로그램 시작

#### JBoss EAP 6.3.0/6.4.0 {#jboss-eap}

배포가 실행되기 전에 위의 [일반 설명](#general-description)을 읽으십시오.

**JBoss 서버 준비**

conf 파일에서 메모리 인수 설정(예:`standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

배포-scanner를 사용하여 AEM 웹 응용 프로그램을 설치하는 경우 인스턴스의 xml 파일에 `deployment-timeout` 속성을 설정하는 데 `deployment-timeout,`이(가) 좋을 수 있습니다(예: `configuration/standalone.xml)`:).

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**AEM 웹 애플리케이션 배포**

* JBoss 관리 콘솔에서 AEM 웹 응용 프로그램을 업로드합니다.

* AEM 웹 응용 프로그램을 활성화합니다.

#### Oracle WebLogic 12.1.3/12.2 {#oracle-weblogic}

배포가 실행되기 전에 위의 [일반 설명](#general-description)을 읽으십시오.

관리 서버만 있는 간단한 서버 레이아웃을 사용합니다.

**WebLogic Server 준비**

* `${myDomain}/config/config.xml`보안 구성 섹션에 추가:

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` https://xmlns.oracle.com/weblogic/domain/1.0/domain에서  [올바른 ](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) 위치 확인(기본적으로 섹션 끝에 위치를 지정함)을 참조하십시오.

* VM 메모리 설정 증가:

   * `${myDomain}/bin/setDomainEnv.cmd`(resp .sh)WLS_MEM_ARGS 검색, 설정(예: `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m` 설정)
   * WebLogic Server를 다시 시작합니다.

* `${myDomain}`에 패키지 폴더 및 cq 폴더 내에 그리고 계획 폴더에 만들기

**AEM 웹 애플리케이션 배포**

* AEM 전쟁 파일 다운로드
* AEM War 파일을 ${myDomain}/packages/cq 폴더에 넣습니다.
* 필요한 경우 `WEB-INF/web.xml`에서 구성을 만듭니다(일반 설명에서 위 참조).

   * `WEB-INF/web.xml`파일 압축 해제
   * 게시할 sling.run.modes 매개 변수 변경
   * sling.home 초기 매개 변수의 주석을 해제하고 이 경로를 필요한 대로 설정합니다(일반 설명 참조).
   * web.xml 파일 복구

* AEM 전쟁 파일을 애플리케이션으로 배포(다른 설정에 대해서는 기본 설정 사용)
* 설치에 시간이 걸릴 수 있습니다...
* 일반 설명(예: error.log 추적)에 위의 설명에 따라 설치가 완료되었는지 확인합니다.
* WebLogic `/console`에서 웹 응용 프로그램의 구성 탭에서 컨텍스트 루트를 변경할 수 있습니다.

#### Tomcat 8/8.5 {#tomcat}

배포가 실행되기 전에 위의 [일반 설명](#general-description)을 읽으십시오.

* **Tomcat 서버 준비**

   * VM 메모리 설정 증가:

      * `bin/catalina.bat`(unix의 경우 resp `catalina.sh`)에서 다음 설정을 추가합니다.
      * `set "JAVA_OPTS= -Xmx2048m`
   * Tomcat은 설치 시 관리자 또는 관리자 액세스를 지원하지 않습니다. 따라서 이러한 계정에 대한 액세스를 허용하려면 `tomcat-users.xml`을 수동으로 편집해야 합니다.

      * 관리자 및 관리자에 대한 액세스 권한을 포함하려면 `tomcat-users.xml`을(를) 편집합니다. 구성은 다음 예와 비슷해야 합니다.

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
   * 컨텍스트 루트가 &quot;/&quot;인 AEM을 배포하려면 기존 ROOT 웹 앱의 컨텍스트 루트를 변경해야 합니다.

      * ROOT 웹 앱 중지 및 배포 취소
      * tomcat의 webapps 폴더에서 ROOT.war 폴더 이름 변경
      * 웹 앱 다시 시작
   * 관리자-gui를 사용하여 AEM 웹 응용 프로그램을 설치하는 경우 업로드된 파일의 최대 크기를 늘려야 합니다. 기본적으로 50MB 업로드 크기만 허용됩니다. 이렇게 하면 관리자 웹 응용 프로그램의 web.xml이 열립니다.

      `webapps/manager/WEB-INF/web.xml`

      최대 파일 크기 및 최대 요청 크기를 최소 500MB로 늘리려면 `web.xml` 파일의 다음 `multipart-config` 예를 참조하십시오.

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
   * 필요한 경우 web.xml에서 구성을 만듭니다(일반 설명에서 위 참조).

      * WEB-INF/web.xml 파일 압축 해제
      * 게시할 sling.run.modes 매개 변수 변경
      * sling.home의 초기 매개 변수에 주석을 달고 필요한 대로 이 경로를 설정합니다.
      * web.xml 파일 복구
   * 루트 웹 앱으로 배포하려는 경우 AEM war 파일의 이름을 ROOT.war로 변경하고, 컨텍스트 루트로 aemauthor를 사용하려면 aemauthor.war로 이름을 변경합니다
   * tomcat의 webapps 폴더에 복사
   * AEM이 설치될 때까지 대기


## 문제 해결 {#troubleshooting}

설치 중에 발생할 수 있는 문제를 처리하는 방법에 대한 자세한 내용은 다음을 참조하십시오.

* [문제 해결](/help/sites-deploying/troubleshooting.md)
