---
title: TarMK Cold Standby를 사용하여 AEM을 실행하는 방법
seo-title: How to Run AEM with TarMK Cold Standby
description: TarMK 콜드 대기 설정을 생성, 구성 및 유지 관리하는 방법을 알아봅니다.
seo-description: Learn how to create, configure and maintain a TarMK Cold Standby setup.
uuid: 004fdf3e-517c-452b-8db1-a47d6b31d8ba
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9559e837-a87e-4ee7-8ca6-13b42c74e6bf
docset: aem65
feature: Configuring
exl-id: dadde3ee-d60c-4b87-9af0-a12697148161
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2730'
ht-degree: 0%

---

# TarMK Cold Standby를 사용하여 AEM을 실행하는 방법{#how-to-run-aem-with-tarmk-cold-standby}

## 소개 {#introduction}

Tar 마이크로 커널의 콜드 대기 용량을 사용하면 하나 이상의 대기 AEM 인스턴스가 기본 인스턴스에 연결할 수 있습니다. 동기화 프로세스는 기본 인스턴스에서 대기 인스턴스로만 수행됨을 의미합니다.

대기 인스턴스의 목적은 마스터 리포지토리의 Live Data Copy를 보장하고, 어떤 이유에서든 마스터를 사용할 수 없는 경우 데이터 손실 없이 빠른 전환을 보장하는 것입니다.

컨텐츠는 파일 또는 저장소 손상에 대한 무결성 검사 없이 기본 인스턴스와 대기 인스턴스 간에 선형 동기화됩니다. 이러한 설계로 인해 대기 인스턴스는 기본 인스턴스의 정확한 복사본이며, 기본 인스턴스의 불일치를 완화하지 못합니다.

>[!NOTE]
>
>Cold Standby 기능은 고가용성이 필요한 시나리오를 보호하기 위한 것입니다 **작성자** 인스턴스. 고가용성이 필요한 경우 **게시** Tar 마이크로 커널을 사용하는 인스턴스에서는 게시 팜을 사용하는 것이 좋습니다.
>
>사용 가능한 배포에 대한 자세한 내용은 [권장 배포](/help/sites-deploying/recommended-deploys.md) 페이지.

>[!NOTE]
>
>대기 인스턴스가 설정되거나 주 노드에서 파생된 경우, 관리 관련 활동의 경우 다음 콘솔에만 액세스할 수 있습니다.
>
>* OSGI 웹 콘솔
>
>다른 콘솔에는 액세스할 수 없습니다.

## 작동 방법 {#how-it-works}

기본 AEM 인스턴스에서 TCP 포트가 열려 들어오는 메시지를 수신하고 있습니다. 현재, 노예가 마스터에게 보낼 두 가지 유형의 메시지가 있습니다.

* 현재 헤드의 세그먼트 ID를 요청하는 메시지
* 지정된 ID로 세그먼트 데이터를 요청하는 메시지

대기자는 기본 헤드의 현재 헤드의 세그먼트 ID를 주기적으로 요청합니다. 세그먼트를 로컬에서 알 수 없는 경우 해당 세그먼트가 검색됩니다. 이미 존재하는 경우 세그먼트를 비교하고 필요한 경우 참조된 세그먼트도 요청합니다.

>[!NOTE]
>
>대기 인스턴스는 동기화 전용 모드에서 실행되고 있으므로 요청 유형을 수신하지 않습니다. 대기 인스턴스에서 사용할 수 있는 유일한 섹션은 번들과 서비스 구성을 용이하게 하기 위해 웹 콘솔입니다.

일반적인 TarMK 콜드 대기 배포:

![chlimage_1](assets/chlimage_1.png)

## 기타 특징 {#other-characteristics}

### 견고성 {#robustness}

데이터 흐름은 연결 및 네트워크 관련 문제를 자동으로 감지하고 처리하도록 설계되었습니다. 모든 패킷은 체크섬과 함께 번들로 제공되며, 연결 또는 손상된 패킷에 문제가 발생하는 즉시 다시 시도 메커니즘이 트리거됩니다.

#### 공연 {#performance}

기본 인스턴스에서 TarMK Cold Standby를 사용하면 성능에 거의 영향을 주지 않습니다. 추가 CPU 사용량이 매우 낮으며 추가 하드 디스크 및 네트워크 IO가 생성 및 성능 문제를 발생시키지 않아야 합니다.

대기 상태에서 동기화 프로세스 중에 높은 CPU 사용량이 발생할 수 있습니다. 절차가 다중 스레드되지 않기 때문에 여러 코어를 사용하여 속도를 높일 수 없습니다. 데이터가 변경되거나 전송되지 않으면 측정 가능한 활동이 없습니다. 연결 속도는 하드웨어 및 네트워크 환경에 따라 다르지만 저장소 또는 SSL 사용 크기에 따라 다릅니다. 초기 동기화에 필요한 시간을 예상하거나 기본 노드에서 그 동안 많은 데이터가 변경된 경우를 염두에 두어야 합니다.

#### 보안 {#security}

모든 인스턴스가 동일한 인트라넷 보안 영역에서 실행된다고 가정할 경우 보안 침해 위험이 크게 줄어듭니다. 그러나 슬레이브와 마스터 간의 SSL 연결을 활성화하여 추가 보안 계층을 추가할 수 있습니다. 이렇게 하면 중간 사람에게서 데이터가 손상될 가능성이 줄어듭니다.

또한 수신 요청의 IP 주소를 제한하여 연결할 수 있는 대기 인스턴스를 지정할 수 있습니다. 이를 통해 인트라넷에 있는 아무도 리포지토리를 복사할 수 없도록 할 수 있습니다.

>[!NOTE]
>
>Dispatcher와 Cold Standby 설정의 일부인 서버 사이에 로드 밸런서를 추가하는 것이 좋습니다. 로드 밸런서는 사용자 트래픽만 **기본** 예를 들어, 지속성을 보장하고 컨텐츠가 콜드 대기 메커니즘 이외의 다른 방법으로 대기 인스턴스에 복사되지 않도록 합니다.

## AEM TarMK 콜드 대기 설정 생성 {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>세그먼트 노드 저장소 및 대기 저장소 서비스에 대한 PID가 이전 버전과 비교하여 AEM 6.3에서 다음과 같이 변경되었습니다.
>
>* org.apache.jackrabbit.oak에서 생성합니다.**plugins**.segment.standby.store.StandbyStoreService to org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService
>* org.apache.jackrabbit.oak에서 생성합니다.**plugins**.segment.SegmentNodeStoreService to org.apache.jackrabbit.oak.segment.SegmentNodeStoreService
>
>이 변경 사항을 반영하려면 필요한 구성 조정을 해야 합니다.

TarMK 콜드 대기 설정을 만들려면 먼저 기본 전체 설치 폴더의 파일 시스템 복사본을 새 위치에 수행하여 대기 인스턴스를 만들어야 합니다. 그런 다음 해당 역할을 지정할 실행 모드로 각 인스턴스를 시작할 수 있습니다. `primary` 또는 `standby`).

다음은 하나의 마스터 및 하나의 대기 인스턴스로 설정을 생성하기 위해 수행해야 하는 절차입니다.

1. AEM을 설치합니다.

1. 인스턴스를 종료하고 설치 폴더를 콜드 대기 인스턴스가 실행될 위치에 복사합니다. 다른 시스템에서 실행 하더라도 각 폴더에 설명 이름을 지정합니다. *aem-primary* 또는 *aem-standby*)를 사용하여 인스턴스를 구분합니다.
1. 기본 인스턴스의 설치 폴더로 이동하고 다음을 수행합니다.

   1. 아래에 있는 이전 OSGi 구성을 확인하고 삭제합니다 `aem-primary/crx-quickstart/install`

   1. 라는 폴더를 만듭니다. `install.primary` 아래에 `aem-primary/crx-quickstart/install`

   1. 아래의 기본 노드 저장소 및 데이터 저장소에 필요한 구성을 만듭니다. `aem-primary/crx-quickstart/install/install.primary`
   1. 라는 파일을 만듭니다. `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config` 같은 위치에서 적절하게 구성합니다. 구성 옵션에 대한 자세한 내용은 [구성](/help/sites-deploying/tarmk-cold-standby.md#configuration).

   1. 외부 데이터 저장소와 함께 AEM TarMK 인스턴스를 사용하는 경우, 라는 폴더를 만드십시오 `crx3` 아래에 `aem-primary/crx-quickstart/install` 명명된 이름 `crx3`

   1. 데이터 저장소 구성 파일을 `crx3` 폴더를 입력합니다.

   예를 들어 외부 파일 데이터 저장소와 함께 AEM TarMK 인스턴스를 실행하는 경우 다음 구성 파일이 필요합니다.

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   아래에는 기본 인스턴스에 대한 샘플 구성이 나와 있습니다.

   **샘플** **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

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

1. 기본 실행 모드를 지정하도록 기본 실행 모드를 시작합니다.

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 에 대한 새 Apache Sling 로깅 로거를 만듭니다 **org.apache.jackrabbit.oak.segment** 패키지. 로그 레벨을 &quot;Debug&quot;로 설정하고 로그 출력을 다음과 같은 별도의 로그 파일로 지정합니다. */logs/tarmk-coldstandby.log*. 자세한 내용은 [로깅](/help/sites-deploying/configure-logging.md).
1. 의 위치로 이동합니다. **대기** 인스턴스 및 jar를 실행하여 시작합니다.
1. 기본 로깅 구성과 동일한 로깅 구성을 만듭니다. 그런 다음 인스턴스를 중지합니다.
1. 다음으로 대기 인스턴스를 준비합니다. 기본 인스턴스에 대해 와 동일한 단계를 수행하여 이 작업을 수행할 수 있습니다.

   1. 아래에 있는 파일을 모두 삭제합니다 `aem-standby/crx-quickstart/install`.
   1. 라는 새 폴더를 만듭니다. `install.standby` 아래에 `aem-standby/crx-quickstart/install`

   1. 라는 두 개의 구성 파일을 만듭니다.

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   1. 라는 새 폴더를 만듭니다. `crx3` 아래에 `aem-standby/crx-quickstart/install`

   1. 데이터 저장소 구성을 만들고 아래에 배치합니다. `aem-standby/crx-quickstart/install/crx3`. 이 예제에서 만들어야 하는 파일은 다음과 같습니다.

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

1. 시작 **대기** 대기 실행 모드를 사용하여 인스턴스:

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

웹 콘솔을 통해 다음 방법으로 서비스를 구성할 수도 있습니다.

1. 웹 콘솔로 이동: *https://serveraddress:serverport/system/console/configMgr*
1. 다음 서비스를 찾고 있습니다. **Apache Jackrabbit Oak Segment Tar Cold Standby Service** 설정을 편집하려면 두 번 클릭합니다.
1. 설정을 저장하고 인스턴스를 다시 시작하여 새 설정을 적용할 수 있습니다.

>[!NOTE]
>
>인스턴스의 존재를 확인하여 언제든지 인스턴스의 역할을 확인할 수 있습니다 **기본** 또는 **대기** Sling 설정 웹 콘솔에서 실행 모드.
>
>이 작업은 로 이동하여 수행할 수 있습니다. *https://localhost:4502/system/console/status-slingsettings* 그리고 **&quot;실행 모드&quot;** 줄.

## 첫 번째 동기화 {#first-time-synchronization}

준비가 완료되고 대기시간이 처음 시작되면, 대기 시간이 1차 인스턴스에 도달하기 때문에 인스턴스 간에 네트워크 트래픽이 폭주하게 됩니다. 로그에서 동기화 상태를 확인할 수 있습니다.

대기 상태에서 *tarmk-coldstandby.log*&#x200B;과 같은 항목이 표시됩니다.

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

대기실에서 *error.log*&#x200B;에는 다음과 같은 항목이 표시됩니다.

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

위의 로그 코드 조각에서 *10.20.30.40* 는 기본 IP 주소입니다.

에서 **기본** *tarmk-coldstandby.log*&#x200B;과 같은 항목이 표시됩니다.

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message ‘s.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd’ from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

이 경우 로그에 언급된 &quot;클라이언트&quot;는 **대기** 인스턴스.

이러한 항목이 로그에 표시되지 않으면 동기화 프로세스가 완료된 것으로 간주할 수 있습니다.

위의 항목에서는 폴링 메커니즘이 제대로 작동하는지 표시하지만 폴링 시 동기화되는 데이터가 있는지 확인하는 데 유용합니다. 이렇게 하려면 다음과 같은 항목을 찾습니다.

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

또한 비공유로 실행할 때 `FileDataStore`과 같은 메시지는 바이너리 파일이 제대로 전송되고 있는지 확인합니다.

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### 구성 {#configuration}

Cold Standby Service에 대해 다음 OSGi 설정을 사용할 수 있습니다.

* **Persist 구성:** 활성화된 경우 기존 OSGi 구성 파일 대신 저장소에 구성이 저장됩니다. 운영 시스템에서 이 설정을 사용하지 않도록 설정하여 대기 상태에서 기본 구성을 가져오지 않는 것이 좋습니다.

* **모드 (`mode`):** 인스턴스의 런타임 모드를 선택합니다.

* **포트(포트):** 통신에 사용할 포트입니다. 기본값은 `8023`입니다.

* **주 호스트 (`primary.host`):** - 기본 인스턴스의 호스트입니다. 이 설정은 대기에만 적용됩니다.
* **동기화 간격(`interval`):** - 이 설정은 동기화 요청 사이의 간격을 결정하고 대기 인스턴스에만 적용할 수 있습니다.

* **허용되는 IP 범위(`primary.allowed-client-ip-ranges`):** - 기본 IP에서 연결을 허용하는 IP 범위입니다.
* **보안(`secure`):** SSL 암호화를 활성화합니다. 이 설정을 사용하려면 모든 인스턴스에서 활성화되어야 합니다.
* **대기 읽기 시간 초과(`standby.readtimeout`):** 대기 인스턴스에서 실행된 요청에 대한 시간 제한(밀리초)입니다. 사용되는 기본값은 60000(1분)입니다.

* **대기 자동 정리(`standby.autoclean`):** 동기화 주기에서 저장소 크기가 증가하는 경우 정리 메서드를 호출합니다.

>[!NOTE]
>
>Offloading과 같은 서비스에 대해 독립적으로 식별할 수 있도록 기본 및 대기 ID에 서로 다른 저장소 ID가 있는 것이 좋습니다.
>
>이 문제를 해결하는 가장 좋은 방법은 를 삭제하는 것입니다. *sling.id* 대기 중인 파일을 실행하고 인스턴스를 다시 시작합니다.

## 페일오버 절차 {#failover-procedures}

어떤 이유로든 기본 인스턴스가 실패하는 경우, 다음과 같이 시작 실행 모드를 변경하여 기본 역할을 수행하도록 대기 인스턴스 중 하나를 설정할 수 있습니다.

>[!NOTE]
>
>또한 구성 파일이 기본 인스턴스에 사용되는 설정과 일치하도록 수정해야 합니다.

1. 대기 인스턴스가 설치된 위치로 이동하여 중지합니다.

1. 로드 밸런서가 설정으로 구성된 경우 이 시점에서 로드 밸런서의 구성에서 기본 밸런서를 제거할 수 있습니다.
1. 백업 `crx-quickstart` 대기 설치 폴더의 폴더입니다. 새 대기 모드를 설정할 때 시작 지점으로 사용할 수 있습니다.

1. 를 사용하여 인스턴스를 다시 시작합니다 `primary` 런타임 모드:

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 로드 밸런서에 새 기본 사항을 추가합니다.
1. 새 대기 인스턴스를 생성하고 시작합니다. 자세한 내용은 위의 절차를 참조하십시오 [AEM TarMK 콜드 대기 설정 생성](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup).

## 콜드 대기 설정에 핫픽스 적용 {#applying-hotfixes-to-a-cold-standby-setup}

핫픽스를 콜드 스탠바이 설정에 적용하는 데 권장되는 방법은 핫픽스를 기본 인스턴스에 설치한 다음 핫픽스가 설치된 새 콜드 대기 인스턴스에 복제하는 것입니다.

아래 설명된 절차에 따라 이 작업을 수행할 수 있습니다.

1. JMX 콘솔로 이동하여 **org.apache.jackrabbit.oak를 사용하여 콜드 대기 인스턴스에서 동기화 프로세스를 중지합니다. 상태(&quot;대기&quot;)**bean. 이 작업을 수행하는 방법에 대한 자세한 내용은 [모니터링](#monitoring).
1. 콜드 대기 인스턴스를 중지합니다.
1. 기본 인스턴스에 핫픽스를 설치합니다. 핫픽스 설치 방법에 대한 자세한 내용은 [패키지 작업 방법](/help/sites-administering/package-manager.md).
1. 설치 후 인스턴스에 문제를 테스트합니다.
1. 설치 폴더를 삭제하여 콜드 대기 인스턴스를 제거합니다.
1. 기본 인스턴스를 중지하고 전체 설치 폴더의 파일 시스템 복사본을 콜드 대기 위치로 복제하여 복제합니다.
1. 새로 생성된 클론을 콜드 대기 인스턴스로 재구성합니다. 자세한 내용은 [AEM TarMK 콜드 대기 설정 생성](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. 기본 및 콜드 대기 인스턴스를 모두 시작합니다.

## 모니터링 {#monitoring}

이 기능은 JMX 또는 MBeans를 사용하는 정보를 노출합니다. 이렇게 하면 를 사용하여 대기 및 마스터의 현재 상태를 검사할 수 있습니다 [JMX 콘솔](/help/sites-administering/jmx-console.md). 정보는 `type org.apache.jackrabbit.oak:type="Standby"`명명된 이름 `Status`.

**대기**

대기 인스턴스를 관찰하면 하나의 노드가 표시됩니다. 일반적으로 ID는 일반 UUID입니다.

이 노드에는 5개의 읽기 전용 속성이 있습니다.

* `Running:` 동기화 프로세스가 실행 중인지 여부를 나타내는 부울 값입니다.

* `Mode:` 클라이언트: 그 다음에 인스턴스를 식별하는 데 사용되는 UUID가 옵니다. 이 UUID는 구성이 업데이트될 때마다 변경됩니다.

* `Status:` 현재 상태의 텍스트 표현(예: `running` 또는 `stopped`).

* `FailedRequests:`연속 오류 수.
* `SecondsSinceLastSuccess:` 서버와 마지막으로 통신한 이후 경과된 시간(초)입니다. 표시됩니다 `-1` 성공적인 통신이 이루어지지 않은 경우.

다음 세 가지 호출 방법도 있습니다.

* `start():` 동기화 프로세스를 시작합니다.
* `stop():` 동기화 프로세스를 중지합니다.
* `cleanup():` 대기에서 정리 작업을 실행합니다.

**기본**

기본 설정은 ID 값이 TarMK 대기 서비스가 사용 중인 포트 번호(기본적으로 8023)인 MBean을 통해 일부 일반 정보를 표시합니다. 대부분의 메서드와 속성은 대기 방법과 동일하지만 일부는 다릅니다.

* `Mode:` 은 항상 값을 표시합니다 `primary`.

또한 마스터에 접속된 최대 10개의 클라이언트(대기 인스턴스)에 대한 정보를 검색할 수 있다. MBean ID는 인스턴스의 UUID입니다. 이러한 MBeans에 대한 호출 가능한 메서드는 없지만 매우 유용한 읽기 전용 속성입니다.

* `Name:` 클라이언트의 ID입니다.
* `LastSeenTimestamp:` 텍스트 표현에서 마지막 요청의 타임스탬프입니다.
* `LastRequest:` 클라이언트의 마지막 요청.
* `RemoteAddress:` 클라이언트의 IP 주소입니다.
* `RemotePort:` 클라이언트가 마지막 요청에 사용한 포트입니다.
* `TransferredSegments:` 이 클라이언트에 전송된 총 세그먼트 수입니다.
* `TransferredSegmentBytes:`이 클라이언트에 전송된 총 바이트 수입니다.

## 콜드 대기 저장소 유지 관리 {#cold-standby-repository-maintenance}

### 개정 정리 {#revision-clean}

>[!NOTE]
>
>실행 [온라인 개정 정리](/help/sites-deploying/revision-cleanup.md) 기본 인스턴스에서 아래 표시된 수동 절차가 필요하지 않습니다. 또한 온라인 개정 정리를 사용하는 경우 `cleanup ()` 대기 인스턴스에 대한 작업이 자동으로 수행됩니다.

>[!NOTE]
>
>대기 상태에서 오프라인 개정 정리를 실행하지 마십시오. 필요하지 않으며 세그먼트 저장소 크기를 줄이지 않습니다.

Adobe은 시간에 따른 과도한 저장소 증가를 방지하기 위해 정기적으로 유지 관리를 실행하는 것을 권장합니다. 콜드 대기 저장소 유지 관리를 수동으로 수행하려면 아래 단계를 수행하십시오.

1. JMX 콘솔로 이동하여 를 사용하여 대기 인스턴스에서 대기 프로세스를 중지합니다 **org.apache.jackrabbit.oak: 상태(&quot;대기&quot;)** 콩. 이 작업을 수행하는 방법에 대한 자세한 내용은 [모니터링](/help/sites-deploying/tarmk-cold-standby.md#monitoring).

1. 기본 AEM 인스턴스를 중지합니다.
1. 기본 인스턴스에서 oak 압축 도구를 실행합니다. 자세한 내용은 [저장소 유지 관리](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
1. 기본 인스턴스를 시작합니다.
1. 첫 번째 단계에서 설명한 것과 동일한 JMX bean을 사용하여 대기 인스턴스에서 대기 프로세스를 시작합니다.
1. 로그를 확인하고 동기화가 완료될 때까지 기다립니다. 현재 대기 저장소의 상당한 성장이 표시될 가능성이 있습니다.
1. 를 실행합니다. `cleanup()` 첫 번째 단계에 설명된 것과 동일한 JMX bean을 사용하여 대기 인스턴스에 대한 작업.

오프라인 압축이 저장소 기록을 효과적으로 다시 작성하므로 대기 인스턴스가 주 인스턴스와의 동기화를 완료하는 데 평소보다 오래 걸릴 수 있으므로 리포지토리의 변경 사항을 계산하는 데 더 많은 시간이 걸릴 수 있습니다. 또한 이 프로세스가 완료되면 대기 중인 저장소의 크기는 기본 저장소의 크기와 거의 동일하게 됩니다.

다른 방법으로는, 주 리포지토리를 운영 리포지토리에서 압축을 실행한 후 수동으로 대기 상태로 복사할 수 있으며, 기본적으로 압축이 실행될 때마다 대기를 재구축할 수 있습니다.

### 데이터 저장소 가비지 컬렉션 {#data-store-garbage-collection}

파일 데이터 저장소 인스턴스에서 가끔 가비지 수집을 실행하는 것이 중요합니다. 그렇지 않으면 삭제된 바이너리는 파일 시스템에 남아 있게 되어 결과적으로 드라이브를 채웁니다. 가비지 수집을 실행하려면 아래 절차를 따르십시오.

1. 섹션에 설명된 대로 콜드 대기 저장소 유지 관리 실행 [위](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance).
1. 유지 관리 프로세스가 완료되고 인스턴스가 다시 시작된 후:

   * 기본 모드에서 다음에 설명된 대로 관련 JMX bean을 통해 데이터 저장소 가비지 수집을 실행합니다. [이 문서](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console).
   * 대기 상태에서 데이터 저장소는 **BlobGarbageCollection** MBean - `startBlobGC()`. **RepositoryManagement **MBean은 대기 모드에서 사용할 수 없습니다.

   >[!NOTE]
   >
   >공유 데이터 저장소를 사용하지 않는 경우 가비지 수집은 먼저 기본 상태에서 실행한 다음 대기 상태에서 실행해야 합니다.
