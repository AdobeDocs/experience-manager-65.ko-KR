---
title: JEE 서버 클러스터에서 AEM Forms을 구성하고 문제를 해결하는 방법
description: JEE 서버 클러스터에서 Adobe Experience Manager(AEM) Forms을 구성하고 문제를 해결하는 방법에 대해 알아봅니다.
exl-id: 230fc2f1-e6e5-4622-9950-dae9449ed3f6
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '3959'
ht-degree: 0%

---

# JEE 서버 클러스터에서 AEM Forms 구성 및 문제 해결 {#configuring-troubleshooting-aem-forms-jee-server-cluster}

## 전제 조건 지식 {#prerequisites}

JEE의 Adobe Experience Manager(AEM) Forms, JBoss®, WebSphere® 및 WebLogic 애플리케이션 서버, Red Hat® Linux®, SUSE® Linux®, Microsoft® Windows, IBM® AIX® 또는 Sun Solaris™ 운영 체제, Oracle, IBM® DB2® 또는 SQL Server 데이터베이스 서버 및 웹 환경에 익숙합니다.

## 사용자 수준 {#user-level}

고급

JEE 클러스터의 AEM Forms은 JEE의 AEM Forms이 클러스터 장애에 복원력을 갖도록 설계된 토폴로지입니다. 또한 토폴로지를 통해 시스템 용량을 단일 노드의 기능 이상으로 확장할 수 있습니다. 클러스터는 여러 노드를 데이터를 공유하고 트랜잭션이 실행 중인 여러 노드에 걸쳐 실행되도록 하는 단일 논리 시스템으로 결합합니다. 클러스터는 워크로드의 조합을 처리하는 서비스의 조합을 지원할 수 있다는 점에서 JEE에서 AEM Forms을 확장하는 가장 일반적인 방법입니다. JEE의 AEM Forms 클러스터가 모든 유형의 배포에 가장 적합한 것은 아니며, 비클러스터형 서버 부하 분산 아키텍처가 적절할 수 있습니다.

이 문서에서는 JEE 클러스터에서 AEM Forms에 발생할 수 있는 특정 구성 요구 사항 및 잠재적인 문제 영역에 대해 설명합니다.

## 클러스터 안에 있는 것은 무엇입니까? {#what-is-in-cluster}

JEE의 AEM Forms 클러스터 노드는 서로 통신하고 정보를 공유하여 클러스터 전체가 하나의 일관된 구성 및 애플리케이션 상태를 가질 수 있도록 합니다. 클러스터 내의 정보 공유는 다른 컨텍스트에서 사용되는 여러 가지 다른 방식으로 동시에 수행됩니다. 기본 정보 공유 방법은 아래 그림과 같습니다.

![응용 프로그램 서버 클러스터](assets/application-server-cluster.jpg)

### 응용 프로그램 서버 클러스터 {#application-server-cluster}

JEE의 AEM Forms 클러스터는 기본 애플리케이션 서버의 클러스터링 기능에 의존합니다. 응용 프로그램 서버 클러스터는 클러스터 구성을 전체적으로 관리할 수 있도록 하며 소프트웨어 구성 요소가 클러스터 내에서 서로 찾을 수 있도록 하는 JNDI(Java™ Naming and Directory Interface)와 같은 낮은 수준의 클러스터 서비스를 제공합니다. 응용 프로그램 서버에 따라 응용 프로그램 서버에 있는 클러스터 서비스의 정교성과 기본 기술 종속성이 달라집니다. WebSphere® 및 WebLogic은 클러스터에 대한 정교한 관리 기능을 갖추고 있는 반면 JBoss®는 기본적인 접근 방식을 채택하고 있습니다.

### GemFire 캐시 {#gemfire-cache}

GemFire 캐시는 각 클러스터 노드에서 구현된 분산 캐시 메커니즘입니다. 노드들은 서로를 찾고 노드들 사이에서 일관성을 유지하는 단일 논리 캐시를 구축한다. 서로를 찾는 노드들이 결합하여 그림 1에서 클라우드로 표시된 단일 노드 캐시를 유지한다. GDS 및 데이터베이스와 달리 캐시는 순전히 개념적인 엔티티입니다. 실제 캐시된 콘텐츠는 메모리 및 `LC_TEMP` 각 클러스터 노드의 디렉토리.

### 데이터베이스 {#database}

JDBC 데이터 소스 IDP_DS, EDC_DS 등을 통해 액세스되는 JEE의 AEM Forms 데이터베이스는 클러스터의 모든 노드에서 공유됩니다. 진행 중인 트랜잭션, 진행 중인 트랜잭션과 연결된 사용자 데이터, 시스템 설정이 설정된 방법과 관련된 데이터 등 JEE의 AEM Forms 상태와 관련된 가장 영구적인 데이터는 이 데이터베이스에 있습니다.

### 글로벌 문서 스토리지 {#global-document-storage}

GDS(Global Document Storage)는 JEE의 AEM Forms 내에서 Document Manager(IDPDocument 클래스)가 사용하는 파일 시스템 기반 스토리지 영역입니다. GDS는 클러스터의 모든 노드에 액세스할 수 있어야 하는 단기 및 장기 파일을 저장합니다.

### 기타 항목 {#other-items}

이러한 주요 공유 자원 외에도 Quartz와 같이 특정 클러스터 동작이 있는 다른 항목들이 있다. Quartz는 JEE의 AEM Forms에서 사용하는 스케줄러 하위 시스템으로, 데이터베이스 테이블을 사용하여 무엇이 예약되었고 어떤 예약된 활동이 실행되고 있는지에 대한 지식을 보유합니다. Quartz는 단일 노드 설치 및 클러스터에 대해 다르게 구성해야 하며, JEE 설정의 다른 AEM Forms에서 쿠키를 가져옵니다.

## 일반적인 구성 문제 {#common-configuration}

JEE 클러스터에서 AEM Forms을 유지 관리하거나 문제를 해결할 때 가장 불만스러운 것 중 하나는 클러스터가 정상적인지 확인할 수 있는 단일 위치가 없다는 것입니다. 모든 것이 클러스터에서 잘 진행되고 있는지 확인하기 위해서는 약간의 조사와 분석이 필요하며, 클러스터 구성에 무엇이 잘못되었는지에 따라 클러스터 작동에 몇 가지 실패 모드가 있습니다. 아래 그림은 일부 공유 리소스가 잘못 공유되는 잘못 구성된 클러스터를 보여 줍니다.

![잘못 구성된 클러스터](assets/bad-configuration-cluster.png)

클러스터에서 JEE에서 AEM Forms을 실행하지 않으려는 경우에도 클러스터가 작동하는 방식 및 클러스터에서 찾고 확인할 수 있는 사항의 종류를 이해합니다. 그 이유는 JEE의 AEM Forms 일부 부분이 클러스터에서 잘못 작동하고 예상하지 못한 클러스터 동작을 수행한다는 신호를 받을 수 있기 때문입니다.

위 그림의 공유 구성에 문제가 있습니까? 다음 섹션에서는 이러한 문제에 대해 설명합니다.

### (1) GemFire 클러스터 구성 {#gemfire-cluster-configuration}

Gemfire 캐시에서 몇 가지 문제가 발생할 수 있습니다. 두 가지 일반적인 시나리오는 다음과 같습니다.

* 서로 찾을 수 있어야 하는 노드는 찾을 수 없습니다.

* 클러스터된 노드는 서로 찾을 수 있으며, 찾을 수 없는 경우 캐시를 공유할 수 있습니다.

클러스터링할 노드가 있는 경우 네트워크에서 서로를 찾아야 합니다. 기본적으로 이 작업은 멀티캐스트 UDP 메시지로 수행됩니다. 각 노드는 브로드캐스트 메시지가 있음을 알리는 메시지를 보내고, 이러한 메시지를 수신한 모든 노드는 발견한 다른 노드와 대화를 시작합니다. 이러한 종류의 자동 검색 방법은 일반적이며, 많은 종류의 소프트웨어와 기기가 이러한 방법을 수행합니다.

자동 검색의 한 가지 일반적인 문제는 멀티캐스트 메시지가 네트워크에 의해 필터링될 수 있다는 것입니다. 이는 네트워크 정책의 일부이거나 소프트웨어 방화벽 규칙으로 인해 또는 노드 사이에 존재하는 네트워크를 통해 라우팅할 수 없기 때문에 발생할 수 있습니다. 복잡한 네트워크에서 UDP 자동 검색을 작동시키기 어려운 일반적인 문제 때문에 프로덕션 배포에서는 대체 검색 방법인 TCP 로케이터를 사용하는 것이 일반적입니다. TCP 로케이터에 대한 일반적인 설명은 참조에서 확인할 수 있습니다.

**로케이터를 사용하는지 UDP를 사용하는지 어떻게 알 수 있습니까?**

다음 JVM 속성은 GemFire 캐시가 다른 노드를 찾는 데 사용하는 방법을 제어합니다.

멀티캐스트 설정:

* `adobe.cache.multicast-port`: 분산 시스템의 다른 구성원과 통신하는 데 사용되는 멀티캐스트 포트입니다. 0으로 설정하면 구성원 검색과 배포 모두에 대해 멀티캐스트가 비활성화됩니다.

* `gemfire.mcast-address` (선택 사항): Gemfire에서 사용하는 기본 IP 주소를 무시합니다.

TCP 로케이터 설정:

* `adobe.cache.cluster-locators`: 시스템 구성원이 실행 중인 로케이터와 통신하기 위해 사용하는 모든 로케이터에 대한 TCP 로케이터 및 TCP 로케이터 포트의 IP 주소/호스트 이름입니다.

목록에는 현재 사용 중인 모든 로케이터가 포함되어야 하며 클러스터 시스템의 모든 멤버에 대해 일관되게 구성해야 합니다.

TCP 로케이터 목록이 비어 있으면 로케이터가 사용되지 않고 멀티캐스트 메서드가 대신 사용됩니다.

**TCP 로케이터가 실행 중인지 확인하려면 어떻게 해야 합니까?**

먼저 TCP 로케이터가 사용 중이면 모든 클러스터 노드에서 다음 JVM 속성에 TCP 로케이터가 나열되어야 합니다.

`-Dadobe.cache.cluster-locators=aix01.adobe.com[22345],aix02.adobe.com[22345]`

JEE 클러스터 노드의 AEM Forms에서 로케이터를 실행할 필요가 없습니다. 원하는 경우 클러스터와 별도의 다른 시스템에서 실행할 수 있습니다. 둘 이상의 시스템에서 로케이터를 실행할 수 있습니다. 또한 로케이터의 단일 오류로 인해 클러스터 재시작에 문제가 발생할 수 있으므로 두 위치에서 로케이터를 실행하는 것이 가장 좋습니다. 로케이터를 실행하는 각 시스템에서 다음 명령을 사용하여 로케이터가 실행 중인지 확인할 수 있습니다.

`netstat -an | grep 22345`

예상 응답은 다음과 같아야 합니다.

`tcp 0 0 *.22345 *.* LISTEN`

또 다른 확인 명령은 다음과 같습니다.

`ps -ef | grep gemfire`

예상 응답은 다음과 같아야 합니다.

`livecycl 331984 1 0 10:14:51 pts/0 0:03 java -cp ./gemfire.jar: -Dgemfire.license-type=production -Dlocators=localhost[22345] com.gemstone.gemfire.distributed.Locator 22345`

**GemFire가 클러스터에 있다고 생각하는 노드를 어떻게 볼 수 있습니까?**

GemFire는 GemFire 캐시에서 어떤 클러스터 멤버가 발견되고 채택되었는지 진단하는 데 사용할 수 있는 로깅 정보를 생성합니다. 이 옵션을 사용하여 모든 올바른 클러스터 멤버가 검색되고 추가 클러스터 노드 검색이나 잘못된 클러스터 노드 검색이 발생하지 않는지 확인할 수 있습니다. GemFire의 로그 파일은 JEE의 구성된 AEM Forms 임시 디렉토리에 있습니다.

`.../LC_TEMP/adobeZZ__123456/Caching/Gemfire.log`

뒤에 오는 숫자 문자열 `adobeZZ_` 는 서버 노드에 고유하므로 임시 디렉터리의 실제 내용을 검색해야 합니다. 다음 두 문자 `adobe` 애플리케이션 서버 유형에 따라 다음 중 하나를 수행합니다. `wl`, `jb`, 또는 `ws`.

다음 샘플 로그는 두 노드 클러스터가 자신을 발견하면 어떤 일이 발생하는지를 보여 줍니다.

첫 번째 노드의 경우 AP-HP8:

```xml
[config 2011/08/05 09:28:09.143 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] This member, ap-hp8(4268):18763, is becoming group coordinator.
[info 2011/08/05 09:28:09.151 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Entered into membership in group GF6.5.1.17 with ID ap-hp8(4268)<v0>:18763/56449.
[info 2011/08/05 09:28:09.152 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Starting DistributionManager ap-hp8(4268)<v0>:18763/56449.
[info 2011/08/05 09:28:09.153 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449]
[info 2011/08/05 09:28:09.153 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:09.154 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] ap-hp8(4268)<v0>:18763/56449 is the elder and the only member.
[info 2011/08/05 09:28:09.163 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Did not hear back from any other system. I am the first one.
[info 2011/08/05 09:28:09.164 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] DistributionManager ap-hp8(4268)<v0>:18763/56449 started on 239.192.81.1[33456]. There were 0 other DMs. others: []
[info 2011/08/05 09:28:20.841 EDT GemfireCacheAdapter <Pooled Message Processor 1> tid=0xc4] New administration member detected at ap-hp7(2821)<v1>:19498/59136.
```

다른 노드인 AP-HP7:

```xml
[info 2011/08/05 09:28:09.830 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Attempting to join distributed system whose membership coordinator is ap-hp8(4268)<v0>:18763 using membership ID ap-hp7(2821):19498
[info 2011/08/05 09:28:10.058 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Entered into membership in group GF6.5.1.17 with ID ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.059 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Starting DistributionManager ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449, ap-hp7(2821)<v1>:19498/59136]
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp7(2821)<v1>:19498/59136>. Now there are 2 non-admin member(s).
[info 2011/08/05 09:28:10.128 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] DistributionManager ap-hp7(2821)<v1>:19498/59136 started on 239.192.81.1[33456]. There were 1 other DMs. others: [ap-hp8(4268)<v0>:18763/56449]
```

**만약 GemFire가 해서는 안 될 노드를 찾는 것이라면 어떻게 해야 할까?**

기업 네트워크를 공유하는 각 클러스터는 TCP 로케이터를 사용하는 경우 별도의 TCP 로케이터 집합을 사용하고, 멀티캐스트 UDP 구성을 사용하는 경우에는 별도의 UDP 포트 번호를 사용해야 합니다. UDP 자동 검색은 JEE의 AEM Forms에 대한 기본 구성이며 여러 클러스터에서 동일한 기본 포트를 사용하고 33456 때문에 통신을 시도하지 않아야 하는 클러스터가 예기치 않게 그럴 수 있습니다. 예를 들어, 프로덕션 클러스터와 QA 클러스터는 별도로 유지되어야 하지만 UDP 멀티캐스트를 통해 서로 연결될 수 있습니다.

GemFire가 부적절하게 클러스터링하는 네트워크에서 중복 포트를 발견할 수 있는 가장 일반적인 상황은 클러스터 Bootstrap 중에 발생합니다. Bootstrap 프로세스가 명확한 원인 없이 실패한다는 것을 알 수 있습니다. 일반적으로 다음과 같은 오류가 표시됩니다.

```xml
Caused by: com.ibm.ejs.container.UnknownLocalException: nested exception is: com.adobe.pof.schema.ObjectTypeNotFoundException: Object Type: dsc.sc_service_configuration not found.
                at com.adobe.pof.schema.POFDefaultDomain.getObjectType(POFDefaultDomain.java:93)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.serviceConfigAuditAttributeExists(DSCInitializerBean.java:225)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.installSchema(DSCInitializerBean.java:186)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.bootstrap(DSCInitializerBean.java:94)
                at com.adobe.idp.dsc.initializer.EJSLocalStatelessDSCInitializerBeanLocalEJB_7bb34e85.bootstrap(Unknown Source)
                at com.adobe.livecycle.bootstrap.bootstrappers.DSCBootstrapper.bootstrap(DSCBootstrapper.java:68)
```

이 경우 부트스트래퍼는 GemFire를 사용하여 필요한 테이블에 액세스하는 중입니다. 또한 JDBC를 통해 액세스한 테이블과 다른 기본 데이터베이스가 있는 다른 클러스터에서 온 GemFire가 반환한 캐시된 테이블 정보 간에 불일치가 발생합니다.

Bootstrap 중에 중복 포트가 표시되는 경우가 종종 있지만 이 상황은 나중에 나타날 수 있습니다. 이 문제는 다른 클러스터의 Bootstrap이 발생했을 때 클러스터가 중지된 후 다시 시작될 때 발생할 수 있습니다. 또는 네트워크 구성을 변경하여 멀티캐스트 목적으로 이전에 격리된 클러스터를 서로 볼 수 있도록 합니다.

이러한 상황을 진단하려면 GemFire 로그를 보고 예상 노드만 발견되는지 여부를 신중하게 고려하십시오. 문제를 해결하려면 를 변경해야 합니다. `adobe.cache.multicast-port` 속성을 한 개 또는 두 클러스터 모두에서 다른 값으로 설정합니다.

### 2) GDS 공유 {#gds-sharing}

GDS 공유는 JEE 자체의 AEM Forms 외부에서 O/S 수준에서 구성되며, 여기서 모든 클러스터 노드에서 동일한 공유 디렉터리 구조를 사용할 수 있도록 정렬해야 합니다. Windows 유형 시스템에서는 한 노드에서 다른 노드로 또는 NAS 어플라이언스와 같은 원격 파일 시스템에서 모든 노드로 파일 공유를 설정하여 이 작업을 수행할 수 있습니다. UNIX® 시스템에서 GDS 공유는 일반적으로 한 노드에서 다른 노드로 또는 NAS 어플라이언스에서 NFS 파일 공유를 통해 이루어집니다.

클러스터에 대해 가능한 실패 모드는 이 원격 파일 공유를 사용할 수 없게 되거나 약간의 문제가 있는 경우입니다. 네트워크 문제, 보안 설정 또는 잘못된 구성으로 인해 원격 마운트가 실패할 수 있습니다. 시스템 재부팅으로 인해 며칠 또는 몇 주 전에 이루어진 구성 변경 사항이 적용될 수 있으며 이로 인해 예기치 않은 문제가 발생할 수 있습니다.

**NFS 공유를 마운트하지 못하면 어떻게 됩니까?**

UNIX®에서 NFS 마운트를 디렉토리 구조에 매핑하는 방식을 사용하면 마운트에 장애가 발생하더라도 사용 가능한 GDS 디렉토리를 사용할 수 있습니다. 고려해야 할 사항:

* NAS 서버: NFS 공유 폴더 /u01/iapply/livecycle_gds
* 노드 1: /u01/iapply/livecycle_gds에 있는 공유 폴더(DB 서버에 호스팅)에 대한 마운트 지점
* 노드 2: /u01/iapply/livecycle_gds에 있는 공유 폴더(DB 서버에 호스팅)에 대한 마운트 지점

* LCES는 GDS 경로를 지정합니다. /u01/iapply/livecycle_gds

노드 1의 마운트가 실패하면 디렉토리 구조에 경로가 포함됩니다 `/u01/iapply/livecycle_gds` 을 지정하면 노드가 올바르게 실행되는 것처럼 보입니다. 그러나 GDS 콘텐츠가 실제로 다른 노드와 공유되지 않으므로 클러스터가 제대로 작동하지 않습니다. 이런 일이 일어날 수도 있고 일어나기도 하는데, 그 결과는 그 클러스터가 신비로운 방식으로 실패한다는 것이다.

가장 좋은 방법은 Linux® 마운트 지점이 GDS의 루트로 사용되지 않고 대신 일부 디렉토리가 GDS 루트로 사용되도록 하는 것입니다.

* NFS 서버가 있는 경우 다음 디렉토리가 있을 수 있습니다. /some/storage/lc_cluster_dev/LC_GDS
* 클러스터 노드에는 /u01/iapply/shared 마운트 지점이 있습니다.
* Mount nfs_server: /some/storage/lc_cluster_dev/u01/iapply/shared
* GDS를 /u01/iapply/shared/LC_GDS로 지정

이제 어떤 이유로든 마운트가 성공하지 못하면 기본 마운트 지점에 LC_GDS 디렉토리가 포함되지 않고 클러스터가 GDS를 찾을 수 없기 때문에 예상대로 실패합니다.

**모든 노드에 동일한 GDS가 표시되고 권한이 있는지 어떻게 확인할 수 있습니까?**

GDS 액세스 및 공유의 확인은 대화형 사용자로 각 노드에 액세스함으로써 가장 잘 수행됩니다. UNIX® 노드에 대한 SSH 또는 텔넷을 사용하거나 원격 데스크탑에서 Windows 시스템으로 이 작업을 수행할 수 있습니다. 각 노드에서 구성된 GDS 디렉토리 또는 파일 시스템으로 이동하고 다른 모든 노드에서 볼 수 있는 모든 노드에서 테스트 파일을 생성할 수 있어야 합니다.

JEE의 AEM Forms이 작동하는 사용자 ID에 주목하십시오. Windows 턴키 설치에서 로컬 관리자입니다. UNIX®에서 시작 스크립트나 애플리케이션 서버 구성에서 구성된 특정 서비스 사용자일 수 있습니다. 이 사용자 ID가 모든 노드에서 GDS 파일을 동일하게 만들고 조작할 수 있어야 합니다.

UNIX® 시스템에서 NFS 구성은 종종 루트 소유권이나 파일 및 객체에 대한 루트 액세스 권한을 불신하게 됩니다. 애플리케이션 서버를 루트 사용자로 실행하는 경우 NFS 서버, 파일을 마운트하는 노드 또는 둘 다에 옵션을 지정해야 할 수 있습니다. 이렇게 하면 한 노드가 만들고 다른 노드가 액세스하는 파일에 대해 쌍방향으로 액세스하고 제어할 수 있습니다.

### (3) 데이터베이스 공유 {#database-sharing}

클러스터가 올바르게 작동하려면 모든 클러스터 멤버가 동일한 데이터베이스를 공유해야 합니다. 이 문제를 해결할 수 있는 범위는 대략 다음과 같습니다.

* 실수로 IDP_DS, EDC_DS, AdobeDefaultSA_DS 또는 기타 필수 데이터 소스를 별도의 클러스터 노드에서 다르게 설정하여 노드가 서로 다른 데이터베이스를 가리키도록 할 수 있습니다.
* 실수로 데이터베이스를 공유하도록 여러 개별 노드를 설정하지 말아야 할 때.

응용 프로그램 서버에 따라 JDBC 연결이 클러스터 범위에서 정의되므로 다른 노드에서 다른 정의를 사용할 수 없는 것이 당연할 수 있습니다. 그러나 JBoss®에서는 IDP_DS와 같은 데이터 소스가 노드 1의 한 데이터베이스를 가리키고 노드 2의 다른 데이터베이스를 가리키도록 설정하는 것이 완전히 가능합니다.

반대의 문제가 더 일반적입니다. 즉, JEE 노드의 여러 독립형(또는 클러스터) AEM Forms이 의도하지 않은 경우 실수로 동일한 스키마를 가리키는 상황입니다. DBA가 JEE 데이터베이스의 연결 정보에 대한 단일 AEM Forms을 개발 및 QA 설정 팀에 모르게 제공할 때 가장 자주 발생합니다. 어느 팀도 DEV 및 QA 인스턴스에 별도의 데이터베이스가 필요하다는 것을 인식하지 못합니다.

## 응용 프로그램 서버 클러스터 {#application-server-cluster-1}

JEE 클러스터에서 성공적인 AEM Forms을 만들려면 애플리케이션 서버를 클러스터로 구성하고 제대로 작동해야 합니다. WebSphere® 및 WebLogic에서 이는 문서화된 간단한 프로세스입니다. JBoss®에서 클러스터 구성은 좀 더 실용적이며, 노드가 클러스터 역할을 하도록 구성되어 실제로 서로 찾고 통신하도록 하는 것이 문제가 될 수 있습니다. JBoss®는 내부적으로 UDP 멀티캐스트를 사용하여 피어 노드를 찾고 조정하는 JGroups에 의존합니다. GemFire에서 언급하는 문제 중 일부는 필요한 경우 노드가 서로 찾지 못하거나, 그렇지 않은 경우 노드가 서로 찾는 것과 같이 발생할 수 있습니다.

참조:

* [JBoss® 클러스터를 통한 고가용성 엔터프라이즈 서비스](https://docs.jboss.org/jbossas/jboss4guide/r4/html/cluster.chapt.html)

* [Oracle WebLogic Server-Using 클러스터](https://docs.oracle.com/cd/E12840_01/wls/docs103/pdf/cluster.pdf)

### JBoss®가 올바르게 클러스터링되는지 어떻게 확인할 수 있습니까? {#check-jboss-clustering}

JBoss®가 시작되면 클러스터 멤버가 검색되면 클러스터에 가입하는 노드에 대한 INFO 수준 메시지가 로그 파일/콘솔에 기록됩니다.

실행 시 -g 명령줄 옵션을 통해 클러스터 이름을 지정한 경우 다음과 유사한 메시지가 표시됩니다.

```xml
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster)
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster-HAPartitionCache)
and ones like:

[org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Number of cluster members: 1
2011-07-14 11:34:03,072 INFO  [org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Other members: 0
2011-07-14 11:34:03,138 INFO  [org.jboss.cache.RPCManagerImpl] (main) Received new cluster view: [10.36.34.44:55200|0] [10.36.34.44:55200]
2011-07-14 11:34:03,139 INFO  [org.jboss.cache.RPCManagerImpl] (main) Cache local address is 10.36.34.44:55200
```

### Quartz 스케줄러 {#quartz-scheduler}

일반적으로 AEM Forms on JEE가 클러스터에서 내부 Quartz 스케줄러를 사용하는 것은 일반적으로 AEM Forms on JEE의 전역 클러스터 구성을 자동으로 따르도록 하기 위한 것입니다. 그러나 TCP 로케이터가 멀티캐스트 자동 검색 대신 Gemfire에 사용되는 경우 Quartz의 자동 클러스터 구성이 실패하는 버그가 #2794033. 이 경우 Quartz가 비클러스터형 모드에서 잘못 실행됩니다. 이로 인해 쿼츠 테이블에 교착 상태와 데이터 손상이 발생합니다. 버전 8.2.x는 9.0보다 부작용이 더 심한데, 이는 쿼츠를 많이 사용하지 않지만 여전히 있기 때문이다.

이 문제에 대한 수정 사항은 다음과 같습니다. 8.2.1.2 QF2.143 및 9.0.0.2 QF2.44.

다음 두 속성을 모두 설정하는 해결 방법도 있습니다.

* `-Dadobe.cache.cluster.locators=xxx`

* `-Dadobe.cache.cluster-locators=xxx`

한 설정은 &quot;클러스터&quot;와 &quot;로케이터&quot; 사이에 마침표를 사용하고, 다른 설정은 하이픈을 사용합니다. 이는 구현하기가 쉽고 소프트웨어 패치를 적용하는 것보다 덜 위험하지만 인위적으로 혼란스러운 추가 구성 설정을 생성하는 것과 관련이 있습니다.

### Quartz가 단일 노드 또는 클러스터로 실행 중인지 확인하려면 어떻게 해야 합니까? {#check-quartz}

Quartz가 자체적으로 구성된 방법을 확인하려면 시작 중에 AEM Forms on JEE Scheduler 서비스에서 생성한 메시지를 확인해야 합니다. 이러한 메시지는 INFO 심각도에서 생성되며 메시지를 가져오려면 로그 수준을 조정하고 다시 시작해야 할 수 있습니다. AEM Forms on JEE 시작 시퀀스 내에서 Quartz 초기화는 다음 줄로 시작됩니다.

정보  `[com.adobe.idp.scheduler.SchedulerServiceImpl]` IDPSschedulerService onLoad 로그에서 이 첫 번째 줄을 찾는 것이 중요합니다. 그 이유는 일부 애플리케이션 서버에서도 Quartz를 사용하며, 해당 Quartz 인스턴스를 AEM Forms on JEE Scheduler 서비스에서 사용하는 인스턴스와 혼동하면 안 되기 때문입니다. 이는 스케줄러 서비스가 시작되고 있음을 나타내며, 스케줄러 서비스 다음에 오는 라인은 클러스터된 모드에서 제대로 시작되고 있는지 여부를 알려줍니다. 이 시퀀스에 여러 메시지가 나타나며 Quartz가 구성되는 방식을 보여 주는 마지막 &quot;시작됨&quot; 메시지입니다.

여기에 Quartz 인스턴스의 이름이 지정됩니다. `IDPSchedulerService_$_ap-hp8.ottperflab.adobe.com1312883903975`. 스케줄러의 Quartz 인스턴스 이름은 항상 문자열로 시작됩니다 `IDPSchedulerService_$_`. 이 끝에 추가된 문자열은 Quartz가 클러스터형 모드에서 실행 중인지 여부를 알려줍니다. 노드의 호스트 이름에서 생성된 긴 고유 식별자 및 여기에 있는 긴 숫자 문자열 `ap-hp8.ottperflab.adobe.com1312883903975`는 클러스터에서 작동 중임을 나타냅니다. 단일 노드로 작동하는 경우 식별자는 두 자리 숫자인 &quot;20&quot;입니다.

정보  `[org.quartz.core.QuartzScheduler]` 스케줄러 `IDPSchedulerService_$_20` 시작되었습니다.
각 노드의 스케줄러가 클러스터 모드에서 작동할지 여부를 독립적으로 결정하므로 이 검사는 모든 클러스터 노드에서 별도로 수행해야 합니다.

### Quartz가 잘못된 모드에서 실행 중이면 어떤 종류의 문제가 발생합니까? {#quartz-running-in-wrong-mode}

Quartz가 단일 노드로 실행되도록 설정되어 있지만 클러스터에서 실행 중이고 Quartz 데이터베이스 테이블을 다른 노드와 공유하는 경우 JEE Scheduler에서 AEM Forms이 불안정하게 작동합니다. 데이터베이스 교착 상태가 종종 발생합니다. 이는 이 상황에서 볼 수 있는 매우 일반적인 스택 추적입니다.

```xml
[1/20/11 10:40:57:584 EST] 00000035 ErrorLogger   E org.quartz.core.ErrorLogger schedulerError An error occured while marking executed job complete. job= 'Asynchronous.TaskFormDataSaved:12955380518320.5650479324757354'
 org.quartz.JobPersistenceException: Couldn't remove trigger: ORA-00060: deadlock detected while waiting for resource  [See nested exception: java.sql.SQLException: ORA-00060: deadlock detected while waiting for resource ]
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.removeTrigger(JobStoreSupport.java:1405)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.triggeredJobComplete(JobStoreSupport.java:2888)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport$38.execute(JobStoreSupport.java:2872)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport$40.execute(JobStoreSupport.java:3628)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.executeInNonManagedTXLock(JobStoreSupport.java:3662)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.executeInNonManagedTXLock(JobStoreSupport.java:3624)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.triggeredJobComplete(JobStoreSupport.java:2868)
        at org.quartz.core.QuartzScheduler.notifyJobStoreJobComplete(QuartzScheduler.java:1698)
        at org.quartz.core.JobRunShell.run(JobRunShell.java:273)
        at org.quartz.simpl.SimpleThreadPool$WorkerThread.run(SimpleThreadPool.java:529)
Caused by: java.sql.SQLException: ORA-00060: deadlock detected while waiting for resource
```

### 클러스터의 시스템 시계를 어떻게 동기화합니까? {#synchronize-system-clocks-cluster}

클러스터가 원활하게 작동하려면 모든 클러스터 노드의 시계가 긴밀하게 동기화되어야 합니다. 이 작업은 수작업으로 적절히 수행할 수 없으며 정기적으로 실행되는 일종의 시간 동기화 서비스로 수행해야 합니다. 모든 노드의 시계는 서로 1초 이내여야 합니다. 모범 사례는 클러스터 노드뿐만 아니라 로드 밸런서, 데이터베이스 서버, GDS NAS 서버 및 기타 구성 요소도 모두 동기화하도록 지시합니다.

Windows 시간 동기화는 도메인 컨트롤러에 적용되는 경향이 있습니다. UNIX® 시스템은 NTP를 사용하여 다른 시간 소스와 동기화할 수 있습니다. 가능하면 모든 시스템(JEE 노드의 AEM Forms 및 기타 시스템 구성 요소 모두)이 동일한 소스에 동기화하는 것이 가장 좋습니다.

가장 일시적인 테스트 환경에서도 노드의 시계를 수동으로 설정하는 것은 충분하지 않습니다. 시계를 수동으로 설정하면 정확한 동기화가 이루어지지 않으며 두 노드의 시계는 하루 동안만 상대 방향으로 이동할 수 있습니다. 신뢰할 수 있는 클러스터 작업을 위해서는 활성 시간 동기화 메커니즘이 필수적입니다.

### 로드 밸런서 {#load-balancer}

사용자 대화형 서비스를 제공하는 클러스터의 일반적인 요구 사항은 HTTP 요청을 클러스터 전체에 분산시키는 HTTP 로드 밸런서입니다. JEE의 AEM Forms 클러스터에서 로드 밸런서를 와 함께 성공적으로 사용하려면 다음을 구성해야 합니다.

* 세션 고정

* URL 재작성 규칙

* 노드 상태 검사

### 로드 밸런서 상태 확인 기능은 어떻게 해야 합니까? {#load-balancer-health-check}

일부 로드 밸런서는 로드 밸런싱되는 노드에 대해 주기적 상태 검사를 수행하도록 구성할 수 있습니다. 일반적으로 로드 밸런서가 액세스하려고 하는 애플리케이션 함수에 대한 URL입니다. 로드가 성공하면 노드가 정상 상태라고 가정하고 로드 밸런싱 세트에 유지됩니다. URL이 로드되지 않으면 노드에 오류가 있는 것으로 간주되어 세트에서 제거됩니다. 일반적으로 상태 확인 URL은 JEE AdminUI 로그인 페이지의 AEM Forms에 연결됩니다. 이는 클러스터 멤버에 대한 이상적인 상태 검사가 아니며 단기 프로세스를 구현하고 REST API URL을 상태 검사 기능으로 사용하는 것이 좋습니다.

## 임시 파일 경로 및 유사한 클러스터 설정 {#temporary-file-path-cluster-settings}

JEE의 AEM Forms 내의 특정 파일 경로 설정은 클러스터 전체에서 설정되며 모든 노드에서 동일한 유효 설정을 가지지만 각 노드에서 독립적으로 해석되어 로컬 파일을 참조합니다. 생각해 볼 핵심 사항은 글꼴 경로 설정과 임시 디렉터리 설정입니다. AdminUI 핵심 구성 화면(홈 > 설정 > 핵심 시스템 > 핵심 구성)으로 이동합니다.

다음 설정을 선택해야 합니다.

1. 임시 디렉토리 위치
1. Adobe 서버 글꼴 디렉토리 위치
1. Customer Fonts 디렉토리 위치
1. 시스템 글꼴 디렉토리 위치
1. 데이터 서비스 구성 파일의 위치

클러스터에는 이러한 각 구성 설정에 대해 단일 경로 설정만 있습니다. 예를 들어 임시 디렉토리 위치는 다음과 같을 수 있습니다. `/home/project/QA2/LC_TEMP`. 클러스터에서는 각 노드에 실제로 이 특정 경로에 액세스할 수 있어야 합니다. 한 노드에 예상 임시 파일 경로가 있고 다른 노드에는 없는 경우, 그렇지 않은 노드가 제대로 작동하지 않습니다.

이러한 파일 및 경로는 노드 간에 공유되거나 별도로 위치하거나 원격 파일 시스템에 있을 수 있지만 로컬 노드의 디스크 스토리지에 있는 로컬 복사본인 것이 좋습니다.

특히 임시 디렉토리 경로는 노드 간에 공유해서는 안 됩니다. GDS를 사용하여 임시 디렉터리가 공유되지 않고 있는지 확인하는 절차와 유사한 절차입니다. 각 노드로 이동하여 경로 설정이 나타내는 경로에 임시 파일을 만든 다음 다른 노드가 파일을 공유하지 않는지 확인합니다. 임시 디렉토리 경로는 가능한 경우 각 노드의 로컬 디스크 스토리지를 참조해야 하며 선택해야 합니다.

각 경로 설정에 대해 경로가 실제로 존재하고 JEE의 AEM Forms이 실행되는 유효 사용 ID를 사용하여 클러스터의 각 노드에서 액세스할 수 있는지 확인합니다. 글꼴 디렉토리 내용을 읽을 수 있어야 합니다. 임시 디렉터리는 읽기, 쓰기 및 제어를 허용해야 합니다.
