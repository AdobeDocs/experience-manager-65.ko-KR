---
title: 자산 성능 조정 가이드
description: 병목 현상을 제거하고 AEM 자산의 성능을 최적화하기 위해 AEM 구성, 하드웨어, 소프트웨어 및 네트워크 구성 요소에 대한 변경 사항 제안 및 지침
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae

---


<!-- TBD: Formatting using backticks. Add UICONTROL tag. Redundant info as reviewed by engineering. -->

# 자산 성능 조정 가이드 {#assets-performance-tuning-guide}

AEM(Adobe Experience Manager) 자산 설정에는 다양한 하드웨어, 소프트웨어 및 네트워크 구성 요소가 포함되어 있습니다. 배포 시나리오에 따라 성능 병목 현상을 제거하려면 하드웨어, 소프트웨어 및 네트워크 구성 요소에 대한 특정 구성을 변경해야 할 수 있습니다.

또한 특정 하드웨어 및 소프트웨어 최적화 지침을 찾아 준수하는 것은 AEM 자산 배포를 통해 성능, 확장성 및 안정성 관련 요구 사항을 충족할 수 있는 사운드 기반을 구축하는 데 도움이 됩니다.

AEM Assets의 낮은 성능은 대화형 성능, 자산 처리, 다운로드 속도 및 기타 영역에 대한 사용자 경험에 영향을 줄 수 있습니다.

실제로 성능 최적화는 프로젝트에 대한 타겟 지표를 설정하기 전에 수행하는 기본적인 작업입니다.

다음은 성능 문제가 사용자에게 영향을 주기 전에 이를 발견하고 수정하는 데 중점을 두는 특정 주요 영역입니다.

## 플랫폼 {#platform}

AEM은 여러 플랫폼에서 지원되지만 Adobe는 Linux 및 Windows에서 기본 도구에 대한 최고의 지원을 발견했으며 이는 최적의 성능과 구현 용이성에 기여합니다. AEM Assets 배포의 높은 메모리 요구 사항을 충족하려면 64비트 운영 체제를 배포해야 합니다. 모든 AEM 배포와 마찬가지로 가능한 한 TarMK를 구현해야 합니다. TarMK 파섹 TarMK 오프로드 인스턴스를 추가하여 AEM Assets 배포의 워크플로우 처리 능력을 높일 수 있습니다.

### 임시 폴더 {#temp-folder}

자산 업로드 시간을 개선하려면 Java 임시 디렉토리에 고성능 저장소를 사용합니다. Linux 및 Windows에서 RAM 드라이브 또는 SSD를 사용할 수 있습니다. 클라우드 기반 환경에서는 동일한 고속 스토리지 유형을 사용할 수 있습니다. 예를 들어 Amazon EC2에서는 임시 폴더에 [임시 드라이브](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) 드라이브를 사용할 수 있습니다.

서버에 충분한 메모리가 있다고 가정할 경우 RAM 드라이브를 구성합니다. Linux에서 다음 명령을 실행하여 8GB RAM 드라이브를 만듭니다.

```
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

Windows OS의 경우 타사 드라이버를 사용하여 RAM 드라이브를 만들거나 SSD와 같은 고성능 스토리지를 사용할 수 있습니다.

고성능 임시 볼륨이 준비되면 JVM 매개 변수를 `-Djava.io.tmpdir`설정합니다. 예를 들어 AEM 스크립트의 `CQ_JVM_OPTS` 변수에 아래 JVM 매개 변수를 추가할 수 `bin/start` 있습니다.

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java 구성 {#java-configuration}

### Java 버전 {#java-version}

최적의 성능을 위해 Java 8에 AEM 자산을 배포하는 것이 좋습니다.

>[!NOTE]
>
>Oracle은 2015년 4월 Java 7에 대한 업데이트 릴리스를 중지했습니다.

### JVM 매개 변수 {#jvm-parameters}

다음 JVM 매개변수를 설정해야 합니다.

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## 데이터 저장소 및 메모리 구성 {#data-store-and-memory-configuration}

### 파일 데이터 저장소 구성 {#file-data-store-configuration}

모든 AEM Assets 사용자는 세그먼트 저장소에서 데이터 저장소를 분리하는 것이 좋습니다. 또한 `maxCachedBinarySize` 및 `cacheSizeInMB` 매개 변수를 구성하면 성능을 극대화할 수 있습니다. 캐시에 저장할 수 `maxCachedBinarySize` 있는 가장 작은 파일 크기로 설정합니다. 내 데이터 저장소에 사용할 메모리 내 캐시의 크기를 `cacheSizeInMB`지정합니다. Adobe에서는 이 값을 전체 더미 크기의 2-10% 사이로 설정하는 것이 좋습니다. 그러나 로드/성능 테스트는 이상적인 설정을 결정하는 데 도움이 될 수 있습니다.

### 버퍼링된 이미지 캐시의 최대 크기 구성 {#configure-the-maximum-size-of-the-buffered-image-cache}

Adobe Experience Manager에 대량의 자산을 업로드할 때, 메모리 소모에서 예상치 못한 스파이크를 허용하고 OutOfMemoryErrors로 JVM이 실패하는 것을 방지하려면 버퍼링된 이미지 캐시의 구성된 최대 크기를 줄입니다. 최대 더미(- `Xmx`매개 변수)가 5GB이고 Oak BlobCache가 1GB로 설정되고 문서 캐시가 2GB로 설정된 시스템이 있는 경우를 생각해 보십시오. 이 경우 버퍼링된 캐시는 최대 1.25GB와 메모리를 사용하므로 예상치 못한 스파이크에 대해 0.75GB 메모리만 남습니다.

OSGi 웹 콘솔에서 버퍼링된 캐시 크기를 구성합니다. 에서 `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`속성을 바이트 `cq.dam.image.cache.max.memory` 단위로 설정합니다. 예를 들어 1073741824는 1GB(1024 x 1024 x 1024 = 1GB)입니다.

AEM 6.1 SP1에서 이 속성을 구성하기 위해 `sling:osgiConfig` 노드를 사용하는 경우 데이터 유형을 길게 설정해야 합니다. 자세한 내용은 자산 업로드 [](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html)중에 CQBufferedImageCache가 힙을 소비함을 참조하십시오.

### 공유 데이터 저장소 {#shared-data-stores}

S3 또는 공유 파일 데이터 저장소를 구현하면 대규모 구현에서 디스크 공간을 절약하고 네트워크 처리량을 늘리는 데 도움이 될 수 있습니다. 공유 데이터 저장소 사용에 대한 장단점에 대한 자세한 내용은 자산 크기 [조정 안내서를 참조하십시오](/help/assets/assets-sizing-guide.md).

### S3 data store {#s-data-store}

Adobe는 다음 S3 Data Store 구성( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`)을 통해 기존 파일 데이터 저장소에서 12.8TB의 바이너리 대용량 개체(BLOB)를 고객 사이트의 S3 데이터 스토어로 추출할 수 있었습니다.

```
accessKey=<snip>
 secretKey=<snip>
 s3Bucket=<snip>
 s3Region=us-standard
 s3EndPoint=<a href="https://s3.amazonaws.com/">s3.amazonaws.com</a>
 connectionTimeout=120000
 socketTimeout=120000
 maxConnections=80
 writeThreads=60
 concurrentUploadsThreads=30
 asyncUploadLimit=30
 maxErrorRetry=1000
 path=/opt/author/crx-quickstart/repository/datastore
 s3RenameKeys=false
 s3Encryption=SSE_S3
 proactiveCaching=true
 uploadRetries=1000
 migrateFailuresCount=400
```

## 네트워크 최적화 {#network-optimization}

HTTP 트래픽을 탐지하는 방화벽이 있는 많은 회사에는 업로드 및 파일 손상에 부정적인 영향을 미치는 방화벽이 있으므로 HTTPS를 활성화하는 것이 좋습니다. 대용량 파일 업로드의 경우 WiFi 네트워크가 빠르게 포화되기 때문에 사용자가 네트워크에 유선 연결을 사용하는지 확인합니다. 네트워크 병목 현상을 식별하는 방법에 대한 지침은 자산 [크기 조정 안내서를 참조하십시오](/help/assets/assets-sizing-guide.md). 네트워크 토폴로지를 분석하여 네트워크 성능을 평가하려면 자산 네트워크 [고려 사항을 참조하십시오](/help/assets/assets-network-considerations.md).

기본적으로 네트워크 최적화 전략은 사용 가능한 대역폭과 AEM 인스턴스의 로드에 따라 달라집니다. 방화벽 또는 프록시를 비롯한 일반적인 구성 옵션을 사용하면 네트워크 성능을 향상시킬 수 있습니다. 다음은 기억해야 할 몇 가지 주요 사항입니다.

* 인스턴스 유형(작은, 보통, 큰)에 따라 AEM 인스턴스에 충분한 네트워크 대역폭이 있는지 확인합니다. AEM이 AWS에서 호스팅되는 경우 적절한 대역폭 할당이 특히 중요합니다.
* AEM 인스턴스가 AWS에서 호스팅되는 경우 다양한 크기 조정 정책을 통해 혜택을 받을 수 있습니다. 사용자가 높은 로드를 예상하는 경우 인스턴스 크기를 조정합니다. 보통/낮은 부하를 위해 다운로드합니다.
* HTTPS:대부분의 사용자에게는 HTTP 트래픽을 탐지하는 방화벽이 있으므로 업로드 작업 중에 파일을 업로드하거나 파일이 손상될 수 있습니다.
* 대용량 파일 업로드:사용자가 네트워크에 유선 연결을 사용하고 있는지 확인합니다(WiFi 연결 채도가 빠르게 증가).

## 워크플로우 {#workflows}

### 일시적인 워크플로우 {#transient-workflows}

가능한 경우 DAM 자산 [!UICONTROL 업데이트] 워크플로우를 일시적으로 설정합니다. 이 설정을 사용하면 워크플로우가 일반적인 추적 및 보관 프로세스를 통과하지 않아도 되므로 워크플로우를 처리하는 데 필요한 오버헤드가 크게 줄어듭니다.

>[!NOTE]
>
>기본적으로 AEM 6. [!UICONTROL 3에서] DAM 자산 업데이트 워크플로우는 일시적으로 설정됩니다.이 경우 다음 절차를 건너뛸 수 있습니다.

1. 의 AEM `/miscadmin` 인스턴스에서 탐색합니다 `https://[aem_server]:[port]/miscadmin`.
1. 도구 **[!UICONTROL > 워크플로우]** **[!UICONTROL >]** 모델 **[!UICONTROL >]****[!UICONTROL 댐을]**&#x200B;확장합니다.
1. DAM **[!UICONTROL 자산 업데이트를 엽니다]**. 부동 도구 패널에서 페이지 **[!UICONTROL 탭으로]** 전환한 다음 페이지 속성을 **[!UICONTROL 클릭합니다]**.
1. 임시 **[!UICONTROL 워크플로우를]** 선택하고 확인을 **[!UICONTROL 클릭합니다]**.

   >[!NOTE]
   >
   >일부 기능은 일시적인 워크플로우를 지원하지 않습니다. AEM 자산 배포에서 이러한 기능이 필요한 경우 일시적인 워크플로우를 구성하지 마십시오.

일시적인 워크플로우를 사용할 수 없는 경우 워크플로우 제거를 정기적으로 실행하여 보관된 DAM 자산 업데이트 [!UICONTROL 워크플로우를] 삭제하여 시스템 성능이 저하되지 않도록 하십시오.

일반적으로 매주 삭제 워크플로우를 실행합니다. 그러나 대규모 자산 처리 중과 같이 리소스를 많이 사용하는 시나리오에서는 보다 자주 실행할 수 있습니다.

워크플로우 제거를 구성하려면 OSGi 콘솔을 통해 새 Adobe Granite Workflow Purge 구성을 추가하십시오. 그런 다음 주간 유지 관리 창의 일부로 워크플로우를 구성하고 예약합니다.

제거가 너무 오래 실행되면 시간이 초과됩니다. 따라서 많은 수의 워크플로우로 인해 워크플로우의 제거를 완료하지 못하는 상황을 방지하려면 제거 작업이 완료되어야 합니다.

예를 들어, 워크플로 인스턴스 노드를 만드는 비일시적 워크플로우를 실행한 후 ACS AEM [Commons Workflow Remover를](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) 애드혹 기준으로 실행할 수 있습니다. Adobe Granite Workflow Purge 스케줄러가 실행될 때까지 기다리지 않고 중복되고 완료된 워크플로우 인스턴스를 즉시 제거합니다.

### 최대 병렬 작업 {#maximum-parallel-jobs}

기본적으로 AEM은 서버의 프로세서 수와 같은 최대 병렬 작업 수를 실행합니다. 이 설정의 문제는 부하가 많은 기간 동안 모든 프로세서가 DAM 자산 업데이트 워크플로우에 [!UICONTROL 사용되고] UI 응답성이 저하되고 서버 성능과 안정성을 보호하는 다른 프로세스가 실행되지 않는다는 것입니다. 다음 단계를 수행하여 이 값을 서버에서 사용할 수 있는 프로세서의 절반으로 설정하는 것이 좋습니다.

1. AEM 작성자의 경우 로 `https://[aem_server]:[port]/system/console/slingevent`이동합니다.
1. [ **[!UICONTROL MOCK]** ] Click Edit on each workflow queue that is related to your implementation, for example **[!UICONTROL Granite Workflow Queue]**.
1. 최대 병렬 작업 값을 **[!UICONTROL 업데이트하고]** 저장을 **[!UICONTROL 클릭합니다]**.

대기열을 사용 가능한 프로세서의 절반 수준으로 설정하는 것은 시작할 수 있는 솔루션입니다. 하지만, You may have to increase or decrease this number to achieve maximum throughput and tune it by environment. 임시 워크플로우와 비일시적 워크플로우에 대한 대기열은 물론 외부 워크플로우와 같은 다른 프로세스에 대해서도 별도의 대기열이 있습니다. 프로세서가 50%로 설정된 여러 개의 대기열이 동시에 활성 상태인 경우 시스템이 빠르게 오버로드될 수 있습니다. 많이 사용되는 대기열은 사용자 구현마다 매우 다양합니다. 따라서 서버 안정성을 훼손하지 않고 효율성을 최대화하기 위해 신중하게 구성해야 할 수 있습니다.

### DAM 자산 업데이트 구성 {#dam-update-asset-configuration}

DAM [!UICONTROL 자산] 업데이트 워크플로우에는 Scene7 PTIFF 생성 및 InDesign Server 통합과 같은 작업에 대해 구성된 전체 단계 세트가 포함되어 있습니다. 그러나 대부분의 사용자는 이러한 단계를 여러 번 수행하지 않아도 됩니다. DAM 자산 업데이트 워크플로우 모델의 사용자 [!UICONTROL 지정] 복사본을 만들고 불필요한 단계를 제거하는 것이 좋습니다. 이 경우 새 모델을 가리키도록 DAM [!UICONTROL 자산] 업데이트 런처를 업데이트합니다.

DAM 자산 [!UICONTROL 업데이트] 워크플로우를 집중적으로 실행하면 파일 데이터베이스의 크기가 크게 늘어날 수 있습니다. Adobe에서 수행한 실험 결과 약 8 시간 내에 5500개의 워크플로우가 수행되는 경우 데이터 저장소 크기가 약 400GB까지 증가할 수 있습니다.

데이터 저장소 가비지 수집 작업을 실행하면 데이터 저장소가 원래 크기로 복원됩니다.

일반적으로 데이터 저장소 가비지 수집 작업은 다른 예약된 유지 관리 작업과 함께 매주 실행됩니다.

디스크 공간이 제한되어 있고 DAM 자산 [!UICONTROL 업데이트] 워크플로우를 집중적으로 실행하는 경우 가비지 수집 작업을 보다 자주 예약하는 것이 좋습니다.

#### 런타임 변환 생성 {#runtime-rendition-generation}

고객은 다양한 크기와 형식의 이미지를 웹 사이트 또는 비즈니스 파트너에게 배포하기 위해 사용합니다. 각 변환은 저장소에서 자산의 풋프린트에 추가되므로 이 기능을 신중하게 사용하는 것이 좋습니다. 이미지를 처리 및 저장하는 데 필요한 리소스의 양을 줄이기 위해 이러한 이미지를 통합 도중 변환보다는 런타임에 생성할 수 있습니다.

많은 사이트 고객은 요청 시 이미지 크기를 조정하고 잘라내는 이미지 서블릿을 구현하여 게시 인스턴스에 추가 로드를 적용합니다. 그러나 이러한 이미지를 캐싱할 수 있는 한 이러한 문제를 해결할 수 있습니다.

또 다른 방법은 Scene7 기술을 사용하여 이미지 조작을 전적으로 수행하는 것입니다. 또한 AEM 인프라에서 변환 생성 책임을 인계받을 뿐만 아니라 전체 게시 티어인 브랜드 포털을 배포할 수 있습니다.

#### ImageMagick {#imagemagick}

ImageMagick을 사용하여 [!UICONTROL 표현물을 생성하기 위해 DAM 자산] 업데이트 워크플로우를 사용자 지정하는 경우, Adobe에서는 `policy.xml` 파일을 에서 수정하는 것이 좋습니다 `/etc/ImageMagick/`. 기본적으로 ImageMagick은 OS 볼륨에서 사용 가능한 전체 디스크 공간과 사용 가능한 메모리를 사용합니다. 의 `policymap` 섹션 내에서 다음 구성을 변경하여 이러한 리소스를 `policy.xml` 제한하십시오.

```xml
<policymap>
  <!-- <policy domain="system" name="precision" value="6"/> -->
  <policy domain="resource" name="temporary-path" value="/ephemeral0/imagemagick_tmp"/>
  <policy domain="resource" name="memory" value="1000MiB"/>
  <policy domain="resource" name="map" value="1000MiB"/>
  <!-- <policy domain="resource" name="area" value="1gb"/> -->
  <policy domain="resource" name="disk" value="10000MiB"/>
  <!-- <policy domain="resource" name="file" value="768"/> -->
  <policy domain="resource" name="thread" value="1"/>
  <policy domain="resource" name="throttle" value="50"/>
  <!-- <policy domain="resource" name="time" value="3600"/> -->
</policymap>
```

또한 `configure.xml` 파일에 있는 ImageMagick의 임시 폴더 경로를 충분한 공간 및 IOPS가 있는 디스크 파티션으로 설정(또는 환경 변수 `MAGIC_TEMPORARY_PATH`설정)합니다.

>[!CAUTION]
>
>ImageMagick이 사용 가능한 모든 디스크 공간을 사용하는 경우 구성이 잘못되면 서버가 불안정해질 수 있습니다.
>
>ImageMagick을 사용하여 대용량 파일을 처리하는 데 필요한 정책 변경 사항이 AEM 성능에 영향을 줄 수 있습니다. 자세한 내용은 ImageMagick [설치 및 구성을 참조하십시오](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>ImageMagick `policy.xml` 및 `configure.xml` 파일은 `/usr/lib64/ImageMagick-&#42;/config/` 대신 에서 사용할 수 있습니다. `/etc/ImageMagick/`구성 [파일의 위치는 ImageMagick 설명서를](https://www.imagemagick.org/script/resources.php) 참조하십시오.

>[!TIP]
>
>Adobe Managed Services(AMS)에서 Adobe Experience Manager를 사용하는 경우 대용량 PSD 또는 PSB 파일을 처리할 계획인 경우 Adobe 지원 센터에 문의하십시오. Adobe 고객 지원 센터 담당자와 협력하여 AMS 배포에 대한 이러한 모범 사례를 구현하고 Adobe의 독점 포맷에 적합한 최상의 툴과 모델을 선택할 수 있습니다.

### XMP writeback {#xmp-writeback}

XMP 원본에 의해 메타데이터가 AEM에서 수정될 때마다 원본 에셋이 업데이트되므로 다음과 같은 결과가 발생합니다.

* 자산 자체가 수정됨
* 자산의 버전이 만들어집니다.
* [!UICONTROL 자산에 대해 DAM] 업데이트 자산이 실행됩니다.

나열된 결과는 상당한 자원을 소모한다. 따라서 XMP 원본에 [대한](https://helpx.adobe.com/experience-manager/kb/disable-xmp-writeback.html)작성이 필요하지 않은 경우 비활성화할 것을 권장합니다.

많은 양의 메타데이터를 가져오면 실행 워크플로우 플래그가 선택된 경우 리소스가 많이 소모되는 XMP 쓰기 저장(writeback) 활동이 발생할 수 있습니다. 다른 사용자에 대한 성능에 영향을 주지 않도록 서버 사용량 감소 중에 이러한 가져오기를 계획합니다.

## 복제 {#replication}

예를 들어 사이트 구현에서 자산을 많은 수의 게시 인스턴스로 복제할 경우 체인 복제를 사용하는 것이 좋습니다. 이 경우 작성자 인스턴스는 단일 게시 인스턴스로 복제되어 다른 게시 인스턴스로 복제되므로 작성자 인스턴스를 늘립니다.

### 체인 복제 구성 {#configure-chain-replication}

1. 복제를 연결하는 데 사용할 게시 인스턴스를 선택합니다.
1. 해당 게시 인스턴스에서 다른 게시 인스턴스를 가리키는 복제 에이전트를 추가합니다.
1. 각 복제 에이전트에서 &quot;트리거&quot; 탭에서 &quot;수신&quot;을 활성화합니다.

>[!NOTE]
>
>Adobe에서는 에셋 자동 활성화를 권장하지 않습니다. 그러나 필요한 경우 Adobe에서는 이를 워크플로우의 마지막 단계로 수행하는 것이 좋습니다(일반적으로 DAM 자산 업데이트).

## 검색 인덱스 {#search-indexes}

최신 서비스 팩 및 성능 관련 핫픽스가 시스템 색인에 대한 업데이트를 자주 포함하므로 구현해야 합니다. 색인 [최적화에 대한 성능 조정 팁을](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) 참조하십시오.

자주 실행하는 쿼리에 대한 사용자 정의 인덱스를 만듭니다. 자세한 내용은 슬로우 쿼리 [분석 및](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) 사용자 정의 인덱스 [](/help/sites-deploying/queries-and-indexing.md)작성을 위한 방법을 참조하십시오. 쿼리 및 색인 우수 사례에 대한 추가 인사이트를 보려면 쿼리 및 [색인 작성 우수 사례를 참조하십시오](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Lucene 인덱스 구성 {#lucene-index-configurations}

일부 최적화는 AEM 자산 성능을 향상시키는 데 도움이 되는 Oak 인덱스 구성에서 수행할 수 있습니다. 색인 구성을 업데이트하여 다시 색인 지정 시간을 향상시킵니다.

1. CRXDe를 `/crx/de/index.jsp` 열고 관리 사용자로 로그인
1. 탐색 `/oak:index/lucene`
1. 값,[] 및 `excludedPaths` 등이 `/var`있는 String 속성을 `/etc/workflow/instances``/etc/replication`추가합니다.
1. 로 `/oak:index/damAssetLucene`이동합니다. 값이 `String[]` 있는 `includedPaths` 속성을 `/content/dam`추가합니다.
1. 저장.

(AEM6.1 및 6.2만 해당) ntBaseLucene 인덱스를 업데이트하여 자산 삭제 및 이동 성능을 개선합니다.

1. 탐색 `/oak:index/ntBaseLucene/indexRules/nt:base/properties`
1. 구조화되지 않은 노드 `slingResource` 및 `damResolvedPath` 아래의 두 개 추가 `/oak:index/ntBaseLucene/indexRules/nt:base/properties`
1. 노드에서 아래 속성을 설정합니다(여기서 `ordered` 및 `propertyIndex` 속성은 `Boolean`다음과 같습니다.

   ```
   slingResource
   name="sling:resource"
   ordered=false
   propertyIndex= true
   type="String"
   damResolvedPath
   name="dam:resolvedPath"
   ordered=false
   propertyIndex=true
   type="String"
   ```

1. 노드에서 속성을 `/oak:index/ntBaseLucene` 설정합니다 `reindex=true`. 모두 **[!UICONTROL 저장을 클릭합니다]**.
1. error.log를 모니터링하여 색인이 완료된 시점을 확인합니다.색인에 대한 색인 재설정이 완료되었습니다. [/oak:index/ntBaseLucene]
1. 다시 인덱스 속성이 false로 돌아가므로 CRXDe의 /oak:index/ntBaseLucene 노드를 새로 고침하여 인덱싱을 완료할 수도 있습니다
1. 색인화가 완료되면 CRXDe로 돌아가서 이 두 인덱스에서 &quot;type&quot; 속성을 disabled로 설정합니다

   * */oak:index/slingResource*
   * */oak:index/damResolvedPath*

1. &quot;모두 저장&quot;을 클릭합니다.

Lucene 텍스트 추출 비활성화:

사용자가 PDF 문서에 포함된 텍스트를 검색하는 등 자산의 내용을 검색할 필요가 없는 경우 이 기능을 비활성화하여 색인 성능을 향상시킬 수 있습니다.

1. AEM 패키지 관리자 /crx/packmgr/index.jsp으로 이동합니다.
1. 아래 패키지 업로드 및 설치

[파일 가져오기](assets/disable_indexingbinarytextextraction-10.zip)

### Guess Total {#guess-total}

큰 결과 집합을 생성하는 쿼리를 만들 때는 `guessTotal` 매개 변수를 사용하여 실행 시 많은 메모리 사용을 방지합니다.

## 알려진 문제 {#known-issues}

### 대용량 파일 {#large-files}

AEM에서 대용량 파일과 관련하여 알려진 두 가지 주요 문제가 있습니다. 파일의 크기가 2GB보다 크면 콜드 대기 동기화가 메모리 부족 상태로 실행될 수 있습니다. 대기 동기화가 실행되지 않는 경우가 있습니다. 다른 경우, 기본 인스턴스가 충돌합니다. 이 시나리오는 컨텐츠 패키지를 포함하여 2GB보다 큰 AEM의 모든 파일에 적용됩니다.

마찬가지로, 공유 S3 데이터 저장소를 사용하는 동안 파일 크기가 2GB에 도달하면 파일이 캐시에서 파일 시스템으로 완전히 지속되는 데 시간이 걸릴 수 있습니다. 따라서 바이너리 없는 복제를 사용할 경우 복제가 완료되기 전에 바이너리 데이터가 지속되지 않았을 수 있습니다. 이러한 상황은 특히 데이터 가용성이 중요한 경우 문제를 초래할 수 있습니다.

## 성능 테스트 {#performance-testing}

모든 AEM 배포의 경우 병목 현상을 신속하게 식별하고 해결할 수 있는 성능 테스트 시스템을 구축하십시오. 여기에 중점을 두어야 할 몇 가지 주요 영역이 있습니다.

### 네트워크 테스트 {#network-testing}

고객의 모든 네트워크 성능에 대한 우려 사항은 다음 작업을 수행하십시오.

* 고객 네트워크 내에서 네트워크 성능 테스트
* Adobe 네트워크 내에서 네트워크 성능을 테스트합니다. AMS 고객의 경우 CSE를 사용하여 Adobe 네트워크 내에서 테스트하십시오.
* 다른 액세스 포인트에서 네트워크 성능 테스트
* 네트워크 벤치마크 도구 사용
* 디스패처 테스트

### AEM 인스턴스 테스트 {#aem-instance-testing}

효율적인 CPU 사용률 및 로드 공유를 통해 지연을 최소화하고 높은 처리량을 얻으려면 AEM 인스턴스의 성능을 정기적으로 모니터링합니다. 특히:

* AEM 인스턴스에 대해 로드 테스트 실행
* 업로드 성능 및 UI 응답성 모니터링

## AEM Assets 성능 검사 목록 및 자산 관리 작업의 영향 {#checklist}

* HTTPS를 사용하여 모든 기업 HTTP 트래픽 스나이퍼 활용
* 대용량 에셋 업로드를 위해 유선 연결 사용
* Java 8에 배포합니다.
* 최적의 JVM 매개 변수 설정
* 파일 시스템 DataStore 또는 S3 DataStore 구성
* 일시적인 워크플로우 활성화
* [MOCK] Tune the Granite workflow queue to limit concurrent jobs
* 리소스 사용을 제한하도록 ImageMagick 구성
* DAM 자산 업데이트 [!UICONTROL 워크플로우에서 불필요한 단계] 제거
* 워크플로우 및 버전 제거 구성
* 최신 서비스 팩 및 핫픽스를 사용하여 색인을 최적화할 수 있습니다. 사용 가능한 추가적인 색인 최적화에 대해서는 Adobe 지원에 문의하십시오.
* guessTotal을 사용하여 쿼리 성능을 최적화합니다.
* AEM이 파일 컨텐츠에서 파일 유형을 검색하도록 구성하는 경우(AEM 웹 콘솔에서 **[!UICONTROL CQ DAM MIME]** 유형 서비스 활성화 **[!UICONTROL )]**&#x200B;사용량이 적은 시간 동안 많은파일을 일괄 업로드합니다.
