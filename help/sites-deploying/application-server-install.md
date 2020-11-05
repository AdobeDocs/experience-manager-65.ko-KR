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
source-git-commit: 0a082d3cff66b82ef6de551a735a16a001446a1e
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 1%

---


# 애플리케이션 서버 설치{#application-server-install}

>[!NOTE]
>
>`JAR` aem `WAR` 의 파일 유형은 이러한 포맷은 Adobe의 지원 수준을 충족하기 위해 품질 보증을 받고 있습니다.


이 섹션에서는 응용 프로그램 서버와 함께 Adobe Experience Manager(AEM)을 설치하는 방법을 설명합니다. 개별 응용 프로그램 서버에 대해 [제공되는 특정 지원 수준을 확인하려면 지원되는 플랫폼](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) 섹션을 참조하십시오.

다음 응용 프로그램 서버의 설치 단계는 다음과 같습니다.

* [WebSphere 8.5](#websphere)
* [JBoss EAP 6.3.0/6.4.0](#jboss-eap)
* [Oracle WebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

웹 응용 프로그램, 서버 구성 및 서버 시작 및 중지 방법에 대한 자세한 내용은 해당 응용 프로그램 서버 설명서를 참조하십시오.

>[!NOTE]
>
>WAR 배포에서 Dynamic Media를 사용하는 경우 [다이내믹 미디어 설명서를 참조하십시오](/help/assets/config-dynamic.md#enabling-dynamic-media).

## 일반 설명 {#general-description}

### 응용 프로그램 서버에 AEM을 설치할 때의 기본 동작 {#default-behaviour-when-installing-aem-in-an-application-server}

AEM은 단일 전쟁 파일로 배포됩니다.

배포되는 경우 기본적으로 다음이 수행됩니다.

* 실행 모드는 `author`
* 인스턴스(저장소, Felix OSGI 환경, 번들 등) 가 현재 작업 디렉토리 `${user.dir}/crx-quickstart``${user.dir}` 에 설치되면 crx-quickstart에 대한 이 경로가 `sling.home`

* 컨텍스트 루트는 전쟁 파일 이름입니다(예: `aem-6`

#### 구성 {#configuration}

다음과 같이 기본 동작을 변경할 수 있습니다.

* run mode :배포하기 전에 AEM `sling.run.modes` war 파일의 `WEB-INF/web.xml` 파일에 매개 변수를 구성합니다.

* sling.home:배포하기 전에 AEM `sling.home` war 파일의 `WEB-INF/web.xml`파일에 매개 변수 구성

* 컨텍스트 루트:aem war 파일 이름 변경

#### 게시 설치 {#publish-installation}

게시 인스턴스를 배포하려면 게시 실행 모드를 설정해야 합니다.

* AEM war 파일의 WEB-INF/web.xml파일의 압축을 해제합니다.
* sling.run.modes 매개 변수를 변경하여 게시
* web.xml 파일을 AEM war 파일로 다시 저장
* AEM 전쟁 파일 배포

#### 설치 확인 {#installation-check}

모든 것이 설치되어 있는지 확인하려면 다음을 수행합니다.

* 모든 `error.log`컨텐츠가 설치되었는지 확인하기 위해 파일 뒷면
* 모든 번들 `/system/console` 이 설치되어 있는지 확인합니다.

#### 동일한 응용 프로그램 서버에 두 개의 인스턴스 {#two-instances-on-the-same-application-server}

데모용으로 하나의 애플리케이션 서버에 작성자 및 게시 인스턴스를 설치하는 것이 적절할 수 있습니다. 이를 위해 다음을 수행합니다.

1. 게시 인스턴스의 sling.home 변수와 sling.run.modes 변수를 변경합니다.
1. AEM war 파일에서 WEB-INF/web.xml 파일의 압축을 해제합니다.
1. sling.home 매개 변수를 다른 경로로 변경합니다(절대 및 상대 경로 가능).
1. 게시 인스턴스에 대해 게시하도록 sling.run.modes를 변경합니다.
1. web.xml 파일을 반환합니다.
1. 전쟁 파일의 이름을 변경하여 이름이 다르게 지정합니다.예: 한 이름은 aemauthor.war로, 다른 이름은 aempublish.war로 변경합니다.
1. 더 높은 메모리 설정(예: 기본 AEM 인스턴스의 경우:-Xmx3072m
1. 두 웹 애플리케이션을 배포합니다.
1. 배포 후 두 웹 응용 프로그램을 중지합니다.
1. author 및 publish 인스턴스는 sling.properties 파일에서 property felix.service.urlhandlhandlers=false가 false로 설정되도록 합니다(기본값은 true로 설정됨).
1. 두 웹 애플리케이션을 다시 시작합니다.

## 응용 프로그램 서버 설치 절차 {#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

배포하기 전에 위의 [일반 설명을](#general-description) 읽으십시오.

**서버 준비**

* 기본 인증 헤더가 통과하도록 허용:

   * AEM이 사용자를 인증하도록 하는 한 가지 방법은 WebSphere 서버의 전역 관리 보안을 비활성화하는 것입니다.보안 -> 글로벌 보안으로 이동하고 관리 보안 활성화 확인란의 선택을 취소하고 서버를 저장하고 다시 시작합니다.

*  설정`"JAVA_OPTS= -Xmx2048m"`
* 컨텍스트 루트 = / 를 사용하여 AEM을 설치하려면 먼저 기존 기본 웹 애플리케이션의 컨텍스트 루트를 변경해야 합니다

**AEM 웹 애플리케이션 배포**

* AEM war 파일 다운로드
* 필요한 경우 web.xml에서 구성을 만듭니다(일반 설명에서 위 참조).

   * WEB-INF/web.xml 파일 압축 해제
   * 게시할 sling.run.modes 매개 변수 변경
   * sling.home 초기 매개 변수의 주석을 해제하고 이 경로를 필요한 대로 설정합니다.
   * repack web.xml 파일

* AEM 전쟁 파일 배포

   * 컨텍스트 루트 선택(스링 실행 모드를 설정하려면 배포 마법사의 세부 단계를 선택한 다음 마법사의 6단계에서 지정합니다)

* AEM 웹 애플리케이션 시작

#### JBoss EAP 6.3.0/6.4.0 {#jboss-eap}

배포하기 전에 위의 [일반 설명을](#general-description) 읽으십시오.

**JBoss 서버 준비**

conf 파일에 메모리 인수를 설정합니다(예: `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

aem 웹 응용 프로그램을 설치하기 위해 deployment-scanner를 사용하는 경우 인스턴스의 xml 파일(예: `deployment-timeout,` 다음)에 해당 `deployment-timeout` `configuration/standalone.xml)`속성 세트를 늘리는 것이 좋습니다.

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**AEM 웹 애플리케이션 배포**

* JBoss 관리 콘솔에서 AEM 웹 응용 프로그램을 업로드합니다.

* AEM 웹 응용 프로그램을 활성화합니다.

#### Oracle WebLogic 12.1.3/12.2 {#oracle-weblogic}

배포하기 전에 위의 [일반 설명을](#general-description) 읽으십시오.

관리 서버만 있는 간단한 서버 레이아웃을 사용합니다.

**WebLogic Server 준비**

* 보안 구성 섹션에 `${myDomain}/config/config.xml`추가:

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd에서 [올바른 위치 확인](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) (기본적으로 섹션 끝에 위치를 지정함)을 참조하십시오.

* VM 메모리 설정 증가:

   * open `${myDomain}/bin/setDomainEnv.cmd` (resp.sh)WLS_MEM_ARGS 검색, 설정(예: set) `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * WebLogic Server 다시 시작

* 패키지 폴더 `${myDomain}` 와 cq 폴더 및 계획 폴더에 만들기

**AEM 웹 애플리케이션 배포**

* AEM war 파일 다운로드
* AEM war 파일을 ${myDomain}/packages/cq 폴더에 넣습니다.
* 구성 필요 `WEB-INF/web.xml` 가 있는 경우 설정(일반 설명 참조)

   * 파일 압축 `WEB-INF/web.xml`해제
   * 게시할 sling.run.modes 매개 변수 변경
   * sling.home 초기 매개 변수의 주석을 해제하고 이 경로를 필요한 대로 설정합니다(일반 설명 참조).
   * repack web.xml 파일

* AEM war 파일을 애플리케이션으로 배포(다른 설정에 대해서는 기본 설정 사용)
* 설치 시 시간이 걸릴 수 있습니다...
* 일반 설명(예: error.log 추적)에 위와 같이 설치가 완료되었는지 확인합니다.
* WebLogic에서 웹 응용 프로그램의 구성 탭에서 컨텍스트 루트를 변경할 수 있습니다 `/console`

#### Tomcat 8/8.5 {#tomcat}

배포하기 전에 위의 [일반 설명을](#general-description) 읽으십시오.

* **Tomcat 서버 준비**

   * VM 메모리 설정 증가:

      * (unix의 `bin/catalina.bat` 경우 결과 `catalina.sh` )에 다음 설정을 추가합니다.
      * `set "JAVA_OPTS= -Xmx2048m`
   * Tomcat은 설치 시 관리자 또는 관리자 액세스를 지원하지 않습니다. 따라서 이러한 계정에 대한 액세스를 허용하려면 수동으로 편집해야 `tomcat-users.xml` 합니다.

      * 관리자 및 관리자 액세스 권한 `tomcat-users.xml` 을 포함하도록 편집합니다. 구성은 다음 예와 비슷해야 합니다.

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
   * 컨텍스트 루트 &quot;/&quot;가 있는 AEM을 배포하려면 기존 ROOT 웹 앱의 컨텍스트 루트를 변경해야 합니다.

      * ROOT 웹 앱 중지 및 배포 취소
      * tomcat의 webapps 폴더에서 ROOT.war 폴더 이름 변경
      * 웹 앱 다시 시작
   * 관리자-gui를 사용하여 AEM 웹 응용 프로그램을 설치하는 경우 업로드된 파일의 최대 크기를 늘려야 합니다. 기본 업로드 크기는 50MB만 허용됩니다. 이렇게 하면 관리자 웹 응용 프로그램의 web.xml이 열립니다.

      `webapps/manager/WEB-INF/web.xml`

      최대 파일 크기 및 최대 요청 크기를 최소 500MB로 늘린 다음 `multipart-config` `web.xml` 파일 예제를 참조하십시오.

      ```xml
      <multipart-config>
      <!-- 500MB max -->
      <max-file-size>524288000</max-file-size>
      <max-request-size>524288000</max-request-size>
      <file-size-threshold>0</file-size-threshold>
      </multipart-config>
      ```




* **AEM 웹 애플리케이션 배포**

   * AEM war 파일 다운로드
   * 필요한 경우 web.xml에서 구성을 만듭니다(일반 설명에서 위 참조).

      * WEB-INF/web.xml 파일 압축 해제
      * 게시할 sling.run.modes 매개 변수 변경
      * sling.home 초기 매개 변수의 주석을 해제하고 이 경로를 필요한 대로 설정합니다.
      * repack web.xml 파일
   * 루트 웹 앱으로 배포하려는 경우 AEM war 파일의 이름을 ROOT.war로 변경하고, 컨텍스트 루트로 aemauthor를 만들려면 이 파일의 이름을 aemauthor.war로 변경합니다
   * tomcat의 webapps 폴더에 복사
   * aem이 설치될 때까지 대기


## 문제 해결 {#troubleshooting}

설치 시 발생할 수 있는 문제 처리에 대한 자세한 내용은 다음을 참조하십시오.

* [문제 해결](/help/sites-deploying/troubleshooting.md)
