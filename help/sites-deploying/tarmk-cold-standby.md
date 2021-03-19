---
title: TarMK Cold Standby를 사용하여 AEM을 실행하는 방법
seo-title: TarMK Cold Standby를 사용하여 AEM을 실행하는 방법
description: TarMK Cold Standby 설정을 생성, 구성 및 유지 관리하는 방법을 알아봅니다.
seo-description: TarMK Cold Standby 설정을 생성, 구성 및 유지 관리하는 방법을 알아봅니다.
uuid: 004fdf3e-517c-452b-8db1-a47d6b31d8ba
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9559e837-a87e-4ee7-8ca6-13b42c74e6bf
docset: aem65
feature: 구성
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2732'
ht-degree: 0%

---


# TarMK Cold Standby를 사용하여 AEM을 실행하는 방법{#how-to-run-aem-with-tarmk-cold-standby}

## 소개 {#introduction}

Tar Micro Kernel의 Cold Standby 용량을 사용하면 하나 이상의 대기 AEM 인스턴스가 기본 인스턴스에 연결할 수 있습니다. 동기화 프로세스는 기본 인스턴스에서 대기 인스턴스로만 수행됨을 의미합니다.

대기 인스턴스는 마스터 저장소의 Live Data Copy를 보장하고 어떤 이유로든 마스터를 사용할 수 없는 경우에 데이터 손실 없이 빠른 스위치를 제공하는 데 사용됩니다.

컨텐츠는 파일 또는 리포지토리 손상을 위해 무결성을 검사하지 않고 기본 인스턴스와 대기 인스턴스 간에 선형으로 동기화됩니다. 이러한 설계 때문에 대기 인스턴스는 기본 인스턴스의 정확한 복사본이며 기본 인스턴스에서 불일치를 완화시킬 수 없습니다.

>[!NOTE]
>
>Cold Standby 기능은 **author** 인스턴스에서 높은 가용성이 필요한 안전한 시나리오를 위한 것입니다. Tar 마이크로 커널을 사용하여 **publish** 인스턴스에 높은 가용성이 필요한 경우 Adobe은 게시 팜을 사용하는 것이 좋습니다.
>
>사용 가능한 추가 배포에 대한 자세한 내용은 [권장 배포](/help/sites-deploying/recommended-deploys.md) 페이지를 참조하십시오.

## 작동 방식 {#how-it-works}

기본 AEM 인스턴스에서 TCP 포트가 열려 들어오는 메시지를 수신하고 있습니다. 현재, 노예들이 주인에게 보낼 두 가지 유형의 메시지가 있습니다.

* 현재 헤드의 세그먼트 ID를 요청하는 메시지
* 지정된 ID의 세그먼트 데이터를 요청하는 메시지

대기 상태에서 기본 헤드의 현재 헤드의 세그먼트 ID를 정기적으로 요청합니다. 세그먼트를 로컬에 알 수 없는 경우 해당 세그먼트가 검색됩니다. 세그먼트가 이미 있는 경우 비교되고 필요한 경우 참조된 세그먼트도 요청됩니다.

>[!NOTE]
>
>대기 인스턴스는 동기화 전용 모드에서 실행 중이므로 요청 유형을 수신하지 않습니다. 대기 인스턴스에서 사용할 수 있는 유일한 섹션은 번들 및 서비스 구성을 용이하게 하기 위한 웹 콘솔입니다.

일반적인 TarMK Cold Standby 배포:

![chlimage_1](assets/chlimage_1.png)

## 기타 특성 {#other-characteristics}

### 견고함 {#robustness}

데이터 흐름은 연결과 네트워크 관련 문제를 자동으로 감지하고 처리하도록 설계되었습니다. 모든 패킷은 체크섬과 함께 번들되며 연결 또는 손상된 패킷에 문제가 발생하는 즉시 재시도 메커니즘이 트리거됩니다.

#### 공연 {#performance}

기본 인스턴스에서 TarMK Cold Standby를 사용하면 성능에 거의 영향을 미치지 않습니다. 추가 CPU 사용량은 매우 낮으며 추가 하드 디스크 및 네트워크 IO는 생산 및 성능 문제를 발생시키지 않아야 합니다.

대기 상태에서 동기화 프로세스 동안 높은 CPU 사용량이 발생할 수 있습니다. 절차가 다중 스레드되지 않기 때문에 여러 코어를 사용하여 속도를 높일 수 없습니다. 데이터를 변경 또는 전송하지 않으면 측정 가능한 작업이 없습니다. 연결 속도는 하드웨어 및 네트워크 환경에 따라 다르지만 저장소 또는 SSL 사용에 따라 다릅니다. 초기 동기화에 필요한 시간을 예측할 때 또는 주 노드에서 그 동안 많은 데이터가 변경되었을 때를 염두에 두어야 합니다.

#### 보안 {#security}

모든 인스턴스가 동일한 인트라넷 보안 영역에서 실행된다고 가정할 때 보안 침해의 위험이 크게 줄어듭니다. 그렇지만, 노드와 마스터 간의 SSL 연결을 활성화하여 추가 보안 레이어를 추가할 수 있습니다. 이렇게 하면 중간 사용자가 데이터를 노출할 가능성이 줄어듭니다.

또한 들어오는 요청의 IP 주소를 제한하여 연결할 수 있는 대기 인스턴스를 지정할 수 있습니다. 이를 통해 인트라넷의 어느 누구도 리포지토리를 복사할 수 없도록 할 수 있습니다.

>[!NOTE]
>
>Dispatcher와 Coldy Standby 설정의 일부인 서버 사이에 부하 균형 조정기를 추가하는 것이 좋습니다. 부하 균형 조정기는 일관성을 유지하고 Cold Standby 메커니즘 이외의 다른 방법으로 대기 인스턴스에서 콘텐트가 복사되지 않도록 사용자 트래픽이 **기본** 인스턴스에만 연결되도록 구성해야 합니다.

## AEM TarMK Cold Standby 설정 만들기 {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>세그먼트 노드 스토어 및 대기 스토어 서비스에 대한 PID가 다음과 같이 이전 버전과 비교하여 AEM 6.3에서 변경되었습니다.
>
>* from org.apache.jackrabbit.oak.**plugins**.segment.standby.store.StandbyStoreService - org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService
>* from org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService to org.apache.jackrabbit.oak.segment.SegmentNodeStoreService

>
>
이 변경 사항을 반영하려면 필요한 구성 조정을 해야 합니다.

TarMK Cold Standby 설정을 만들려면 우선 기본 폴더의 전체 설치 폴더의 파일 시스템 복사본을 새 위치에 수행하여 대기 인스턴스를 만들어야 합니다. 그런 다음 해당 역할( `primary` 또는 `standby`)을 지정하는 실행 모드로 각 인스턴스를 시작할 수 있습니다.

다음은 마스터 및 대기 인스턴스 한 개를 포함하는 설정을 만들기 위해 수행해야 하는 절차입니다.

1. AEM을 설치합니다.

1. 인스턴스를 종료하고 설치 폴더를 콜드 대기 인스턴스가 실행될 위치에 복사합니다. 다른 컴퓨터에서 실행되는 경우에도 각 폴더에 인스턴스를 구분하기 위해 설명하는 이름(예: *aem-primary* 또는 *aem-standby*)을 지정해야 합니다.
1. 기본 인스턴스의 설치 폴더로 이동하고 다음을 수행합니다.

   1. `aem-primary/crx-quickstart/install` 아래에 있는 이전 OSGi 구성을 확인하고 삭제합니다.

   1. `aem-primary/crx-quickstart/install` 아래에 `install.primary`이라는 폴더를 만듭니다.

   1. `aem-primary/crx-quickstart/install/install.primary` 아래에 사전 정의된 노드 저장소 및 데이터 저장소에 대한 필수 구성을 만듭니다.
   1. 같은 위치에 `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`이라는 파일을 만들고 그에 따라 구성합니다. 구성 옵션에 대한 자세한 내용은 [구성](/help/sites-deploying/tarmk-cold-standby.md#configuration)을 참조하십시오.

   1. 외부 데이터 저장소에서 AEM TarMK 인스턴스를 사용하는 경우 `aem-primary/crx-quickstart/install` 아래에 `crx3` 폴더를 만듭니다. `crx3`

   1. 데이터 저장소 구성 파일을 `crx3` 폴더에 배치합니다.

   예를 들어 외부 파일 데이터 저장소가 있는 AEM TarMK 인스턴스를 실행하는 경우 다음과 같은 구성 파일이 필요합니다.

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   아래에서 기본 인스턴스에 대한 샘플 구성을 확인할 수 있습니다.

   **샘플** **oforg.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   customBlobStore=B"true"
   standby=B"false"
   ```

   **org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config 샘플**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="primary"
   port=I"8023"
   ```

   **org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config 샘플**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. 기본 실행 모드를 지정해야 합니다.

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. **org.apache.jackrabbit.oak.segment** 패키지에 대한 새 Apache Sling 로깅 로거를 만듭니다. 로그 수준을 &quot;디버그&quot;로 설정하고 로그 출력을 */logs/tarmk-coldstandby.log*&#x200B;과 같은 별도의 로그 파일로 지정합니다. 자세한 내용은 [로깅](/help/sites-deploying/configure-logging.md)을 참조하십시오.
1. **standby** 인스턴스의 위치로 이동한 후 jar를 실행하여 시작합니다.
1. 기본 로깅 구성과 동일한 로깅 구성을 만듭니다. 그런 다음 인스턴스를 중지합니다.
1. 다음으로 대기 인스턴스를 준비합니다. 기본 인스턴스와 동일한 단계를 수행하여 이 작업을 수행할 수 있습니다.

   1. `aem-standby/crx-quickstart/install` 아래에 있을 수 있는 파일을 삭제합니다.
   1. `aem-standby/crx-quickstart/install` 아래에 `install.standby`이라는 새 폴더를 만듭니다.

   1. 다음 두 구성 파일을 만듭니다.

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   1. `aem-standby/crx-quickstart/install` 아래에 `crx3`이라는 새 폴더를 만듭니다.

   1. 데이터 저장소 구성을 만들고 `aem-standby/crx-quickstart/install/crx3` 아래에 배치합니다. 이 예에서 생성해야 하는 파일은 다음과 같습니다.

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
   1. 파일을 편집하고 필요한 구성을 만듭니다.

   다음은 일반적인 대기 인스턴스에 대한 샘플 구성 파일입니다.

   **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config 샘플**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   name="Oak-Tar"
   service.ranking=I"100"
   standby=B"true"
   customBlobStore=B"true"
   ```

   **org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config 샘플**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="standby"
   primary.host="127.0.0.1"
   port=I"8023"
   secure=B"false"
   interval=I"5"
   standby.autoclean=B"true"
   ```

   **org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config 샘플**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. 대기 실행 모드를 사용하여 **standby** 인스턴스를 시작합니다.

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

웹 콘솔을 통해 다음 방법으로 서비스를 구성할 수도 있습니다.

1. 웹 콘솔로 이동:*https://serveraddress:serverport/system/console/configMgr*
1. **Apache Jackrabbit Oak Segment Tar Cold Standby Service**&#x200B;라는 서비스를 찾고 두 번 클릭하여 설정을 편집합니다.
1. 설정을 저장하고, 새 설정을 적용할 수 있도록 인스턴스를 다시 시작합니다.

>[!NOTE]
>
>Sling 설정 웹 콘솔에서 **primary** 또는 **standby** 실행 모드가 있는지 확인하여 언제든지 인스턴스의 역할을 확인할 수 있습니다.
>
>이 작업은 *https://localhost:4502/system/console/status-slingsettings*&#x200B;로 이동하여 **&quot;실행 모드&quot;** 행을 확인하여 수행할 수 있습니다.

## 첫 번째 동기화 {#first-time-synchronization}

준비가 완료되고 대기 상태가 처음 시작된 후에는 대기 상태가 운영 환경에 도달하기 때문에 인스턴스 간에 네트워크 트래픽이 폭주합니다. 동기화 상태를 관찰하려면 로그를 참조할 수 있습니다.

대기 *tarmk-coldstandby.log*&#x200B;에 다음과 같은 항목이 표시됩니다.

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

대기 장치의 *error.log*&#x200B;에 다음과 같은 항목이 표시됩니다.

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

위의 로그 조각에서 *10.20.30.40*&#x200B;은 기본 IP 주소입니다.

**primary** *tarmk-coldstandby.log*&#x200B;에 다음과 같은 항목이 표시됩니다.

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message ‘s.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd’ from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

이 경우 로그에 언급된 &quot;client&quot;는 **standby** 인스턴스입니다.

이러한 항목이 로그에 표시되지 않으면 동기화 프로세스가 완료되었다고 해도 됩니다.

위의 항목은 폴링 메커니즘이 제대로 작동하는 것을 보여주지만, 폴링 중에 동기화된 데이터가 있는지 확인하는 데 유용합니다. 이렇게 하려면 다음과 같은 항목을 찾습니다.

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

또한 비공유 `FileDataStore`으로 실행 중인 경우 다음과 같은 메시지가 이진 파일이 제대로 전송되고 있는지 확인합니다.

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### 구성 {#configuration}

Cold Standby 서비스에 대해 다음 OSGi 설정을 사용할 수 있습니다.

* **영구 구성:** 활성화하면 기존 OSGi 구성 파일 대신 저장소에 구성이 저장됩니다. 운영 시스템에서 이 설정을 사용하지 않도록 설정하여 대기 상태에서 기본 구성을 가져올 수 없도록 하는 것이 좋습니다.

* **모드(`mode`):** 인스턴스의 실행 모드를 선택합니다.

* **포트(포트):통신** 에 사용할 포트입니다. 기본값은 `8023`입니다.

* **기본 호스트 (`primary.host`):** - 기본 인스턴스의 호스트입니다. 이 설정은 대기 모드에만 적용됩니다.
* **동기화 간격(`interval`):** - 이 설정은 동기화 요청 사이의 간격을 결정하며 대기 인스턴스에만 적용할 수 있습니다.

* **허용되는 IP 범위(`primary.allowed-client-ip-ranges`):** - 기본 IP 범위에서 연결을 허용합니다.
* **보안(`secure`):** SSL 암호화를 활성화합니다. 이 설정을 사용하려면 모든 인스턴스에서 활성화되어야 합니다.
* **대기 읽기 제한 시간(`standby.readtimeout`):대기 인스턴스에서** 실행된 요청에 대한 시간 초과(밀리초)입니다. 권장 시간 초과 설정은 43200000. 일반적으로 시간 초과를 최소 12시간 값으로 설정하는 것이 좋습니다.

* **대기 자동 정리(`standby.autoclean`):** 동기화 주기에 스토어 크기가 증가하는 경우 정리 방법을 호출합니다.

>[!NOTE]
>
>Offloading과 같은 서비스에 대해 독립적으로 액세스할 수 있도록 기본 및 대기 ID가 다른 저장소 ID를 갖는 것이 좋습니다.
>
>이 문제를 해결하는 가장 좋은 방법은 대기 상태에서 *sling.id* 파일을 삭제하고 인스턴스를 다시 시작하는 것입니다.

## 장애 조치 절차 {#failover-procedures}

어떤 이유로든 기본 인스턴스가 실패하는 경우 아래와 같이 시작 실행 모드를 변경하여 기본 역할을 수행하도록 대기 인스턴스 중 하나를 설정할 수 있습니다.

>[!NOTE]
>
>기본 인스턴스에 사용되는 설정과 일치하도록 구성 파일을 수정해야 합니다.

1. 대기 인스턴스가 설치된 위치로 이동하여 중지합니다.

1. 설정으로 부하 균형 조정기가 구성된 경우 이 시점에서 부하 균형 조정기의 구성에서 기본 부하 균형 조정기를 제거할 수 있습니다.
1. 대기 설치 폴더에서 `crx-quickstart` 폴더를 백업합니다. 새 대기 모드를 설정할 때 시작점으로 사용할 수 있습니다.

1. `primary` 실행 모드를 사용하여 인스턴스를 다시 시작합니다.

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 부하 균형 조정기에 새 기본 요소를 추가합니다.
1. 새 대기 인스턴스를 만들고 시작합니다. 자세한 내용은 [AEM TarMK Cold Standby Setup 만들기](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)에서 위의 절차를 참조하십시오.

## 콜드 대기 설정 {#applying-hotfixes-to-a-cold-standby-setup}에 핫픽스 적용

핫픽스를 콜드별 설정에 적용하는 권장되는 방법은 기본 인스턴스에 핫픽스를 설치한 다음 핫픽스가 설치된 새로운 coldStandby 인스턴스로 복제하는 것입니다.

아래 설명된 단계에 따라 이 작업을 수행할 수 있습니다.

1. JMX 콘솔로 이동하여 **org.apache.jackrabbit.oak를 사용하여 콜드 대기 인스턴스에서 동기화 프로세스를 중지합니다.상태(&quot;대기&quot;)**bean. 이 방법에 대한 자세한 내용은 [모니터링](#monitoring)의 섹션을 참조하십시오.
1. 콜드 대기 인스턴스를 중지합니다.
1. 기본 인스턴스에 핫픽스를 설치합니다. 핫픽스 설치 방법에 대한 자세한 내용은 [패키지로 작업하는 방법](/help/sites-administering/package-manager.md)을 참조하십시오.
1. 설치 후 인스턴스에 문제가 있는지 테스트합니다.
1. 설치 폴더를 삭제하여 cold standby 인스턴스를 제거합니다.
1. 기본 인스턴스를 중지하고 전체 설치 폴더의 파일 시스템 복사본을 cold standby 위치로 복제하여 복제합니다.
1. 새로 만든 클론을 콜드 대기 인스턴스로 재구성합니다. 자세한 내용은 [AEM TarMK Cold Standby Setup 만들기](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup) 를 참조하십시오.
1. 기본 및 콜드 대기 인스턴스를 모두 시작합니다.

## 모니터링 {#monitoring}

이 기능은 JMX 또는 MBeans를 사용하여 정보를 표시합니다. 이렇게 하면 [JMX 콘솔](/help/sites-administering/jmx-console.md)을 사용하여 대기 상태 및 마스터의 현재 상태를 검사할 수 있습니다. 이 정보는 `Status`라는 이름의 `type org.apache.jackrabbit.oak:type="Standby"`MBean에서 찾을 수 있습니다.

**대기**

대기 인스턴스를 관찰하면 하나의 노드가 표시됩니다. ID는 일반적으로 일반 UUID입니다.

이 노드에는 읽기 전용 속성이 5개 있습니다.

* `Running:` 동기화 프로세스가 실행 중인지 여부를 나타내는 부울 값입니다.

* `Mode:` 클라이언트:그 뒤에 인스턴스를 식별하는 데 사용되는 UUID가 표시됩니다. 이 UUID는 구성이 업데이트될 때마다 변경됩니다.

* `Status:` 현재 상태(예:  `running` 또는  `stopped`)의 텍스트 표현입니다.

* `FailedRequests:`연속 오류 수.
* `SecondsSinceLastSuccess:` 서버와의 마지막 통신이 성공한 이후 경과한 시간(초)입니다. 성공적인 통신이 이루어지지 않은 경우 `-1`이 표시됩니다.

다음과 같은 세 가지 잘못된 방법도 있습니다.

* `start():` 동기화 프로세스를 시작합니다.
* `stop():` 동기화 프로세스를 중지합니다.
* `cleanup():` 대기 상태에서 정리 작업을 실행합니다.

**기본**

기본 ID를 관찰하면 ID 값이 TarMK 대기 서비스가 사용하는 포트 번호입니다(기본적으로 8023). 대부분의 메서드와 속성은 대기 메서드와 동일하지만 일부는 다릅니다.

* `Mode:` 은 항상 값을 표시합니다 `primary`.

또한 마스터에 연결된 최대 10개의 클라이언트(대기 인스턴스)에 대한 정보를 검색할 수 있습니다. MBean ID는 인스턴스의 UUID입니다. 이러한 MBean에 대해 잘못된 방법이 없지만 매우 유용한 일부 읽기 전용 속성은 다음과 같습니다.

* `Name:` 클라이언트의 ID입니다.
* `LastSeenTimestamp:` 텍스트 표현에서 마지막 요청의 타임스탬프.
* `LastRequest:` 클라이언트의 마지막 요청.
* `RemoteAddress:` 클라이언트의 IP 주소입니다.
* `RemotePort:` 마지막 요청에 사용된 클라이언트의 포트입니다.
* `TransferredSegments:` 이 클라이언트로 전송된 총 세그먼트 수입니다.
* `TransferredSegmentBytes:`이 클라이언트로 전송된 총 바이트 수입니다.

## 콜드 대기 저장소 유지 관리 {#cold-standby-repository-maintenance}

### 개정 정리 {#revision-clean}

>[!NOTE]
>
>기본 인스턴스에서 [온라인 개정 정리](/help/sites-deploying/revision-cleanup.md)를 실행하는 경우 아래 표시된 수동 절차가 필요하지 않습니다. 또한 온라인 개정 정리를 사용하는 경우 대기 인스턴스에서 `cleanup ()` 작업이 자동으로 수행됩니다.

>[!NOTE]
>
>대기 상태에서 오프라인 개정 정리를 실행하지 마십시오. 필요하지 않으며 세그먼트 저장소 크기를 줄이지 않습니다.

Adobe은 시간이 지남에 따라 저장소가 과도하게 증가하는 것을 방지하기 위해 유지 관리를 정기적으로 실행할 것을 권장합니다. 콜드 대기 저장소 유지 관리를 수동으로 수행하려면 아래 단계를 따르십시오.

1. JMX 콘솔로 이동하고 **org.apache.jackrabbit.oak를 사용하여 대기 인스턴스의 대기 프로세스를 중지합니다.상태(&quot;대기&quot;)** 빈 이 방법에 대한 자세한 내용은 [모니터링](/help/sites-deploying/tarmk-cold-standby.md#monitoring)의 위 섹션을 참조하십시오.

1. 기본 AEM 인스턴스를 중지합니다.
1. 기본 인스턴스에서 oak 구성 도구를 실행합니다. 자세한 내용은 [저장소 유지 관리](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)를 참조하십시오.
1. 기본 인스턴스를 시작합니다.
1. 첫 번째 단계에서 설명한 대로 동일한 JMX bean을 사용하여 대기 인스턴스에서 대기 프로세스를 시작합니다.
1. 로그를 확인하고 동기화가 완료될 때까지 기다립니다. 현재 대기 저장소에서 상당한 규모의 성장을 볼 수 있습니다.
1. 첫 번째 단계에서 설명한 대로 동일한 JMX bean을 사용하여 대기 인스턴스에서 `cleanup()` 작업을 실행합니다.

오프라인 컴포지션이 저장소 내역을 효과적으로 다시 기록하므로 대기 인스턴스가 기본 인스턴스와 동기화를 완료하는 데 평소보다 시간이 더 오래 걸릴 수 있으므로 저장소에서 변경 사항을 계산하는 데 시간이 더 걸릴 수 있습니다. 또한 이 프로세스가 완료되면 대기 중인 저장소의 크기는 기본 저장소의 크기와 거의 같다는 점도 기억해야 합니다.

다른 방법으로, 기본 리포지토리는 운영 환경에서 구성 작업을 실행한 후 수동으로 대기 상태로 복사할 수 있으며, 기본적으로 컴포지션이 실행될 때마다 대기 저장소를 다시 작성할 수 있습니다.

### 데이터 저장소 가비지 컬렉션 {#data-store-garbage-collection}

파일 데이터 저장소 인스턴스에 대해 가비지 수집을 실행하는 것이 중요합니다. 그렇지 않으면 삭제된 바이너리는 파일 시스템에 남아 있어 결과적으로 드라이브를 채웁니다. 가비지 수집을 실행하려면 아래 절차를 따르십시오.

1. 섹션 [위](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance)에 설명된 대로 콜드 대기 저장소 유지 관리를 실행합니다.
1. 유지 관리 프로세스가 완료되고 인스턴스가 다시 시작된 후:

   * 기본 문서에서 [이 문서](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console)에 설명된 대로 관련 JMX bean을 통해 데이터 저장소 가비지 컬렉션을 실행합니다.
   * 대기 상태에서 데이터 저장소 가비지 컬렉션은 **BlobGarbageCollection** MBean - `startBlobGC()`을 통해서만 사용할 수 있습니다. **RepositoryManagement **MBean은 대기 상태에서 사용할 수 없습니다.

   >[!NOTE]
   >
   >공유 데이터 저장소를 사용하지 않는 경우, 가비지 수집은 먼저 기본 데이터 저장소에서 실행된 다음 대기 상태에서 실행해야 합니다.

