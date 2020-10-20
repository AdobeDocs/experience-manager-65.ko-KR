---
title: 성능 조정 [!DNL Assets].
description: 병목 현상을 [!DNL Experience Manager] 제거하고 성능을 최적화하기 위한 구성, 하드웨어, 소프트웨어 및 네트워크 구성 요소의 변경 사항 등에 대한 제안 및 지침 [!DNL Experience Manager Assets].
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: cc61b8473fb919a963eb73c015efbc2f06197ee8
workflow-type: tm+mt
source-wordcount: '2743'
ht-degree: 0%

---


<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] 성능 조정 가이드 {#assets-performance-tuning-guide}

설치 프로그램에는 다양한 하드웨어, 소프트웨어 및 네트워크 구성 요소가 포함되어 있습니다. [!DNL Experience Manager Assets] 배포 시나리오에 따라 성능 병목 현상을 제거하기 위해 하드웨어, 소프트웨어 및 네트워크 구성 요소에 대한 특정 구성 변경이 필요할 수 있습니다.

또한 특정 하드웨어 및 소프트웨어 최적화 지침을 찾아 준수함으로써 성능, 확장성 및 안정성 측면에서 예상되는 [!DNL Experience Manager Assets] 배포를 충족할 수 있는 사운드 기반을 구축할 수 있습니다.

성능이 저하되면 인터랙티브한 성능, 에셋 처리, 다운로드 속도 및 기타 영역에 대한 사용자 경험에 영향을 미칠 [!DNL Experience Manager Assets] 수 있습니다.

실제로 성능 최적화는 모든 프로젝트에 대한 타겟 지표를 설정하기 전에 수행하는 기본적인 작업입니다.

다음은 성능 문제가 사용자에게 영향을 미치기 전에 이를 발견하고 수정하는 주요 영역입니다.

## 플랫폼 {#platform}

Experience Manager은 여러 플랫폼에서 지원되지만 Linux 및 Windows 기반의 기본 툴에 대한 탁월한 지원이 제공되어 최적의 성능과 구현 용이성에 기여하고 있습니다. 배포의 높은 메모리 요구 사항을 충족하기 위해 64비트 운영 체제를 배포하는 것이 [!DNL Experience Manager Assets] 좋습니다. 모든 Experience Manager 배포과 마찬가지로 가능한 모든 곳에 TarMK를 구현해야 합니다. TarMK는 단일 작성자 인스턴스 이상으로 확장할 수 없지만 MongoMK보다 뛰어난 것으로 나타났습니다. TarMK 오프로드 인스턴스를 추가하여 배포의 워크플로우 처리 능력을 높일 수 [!DNL Experience Manager Assets] 있습니다.

### 임시 폴더 {#temp-folder}

자산 업로드 시간을 개선하려면 Java 임시 디렉터리에 고성능 저장소를 사용하십시오. Linux 및 Windows에서는 RAM 드라이브 또는 SSD를 사용할 수 있습니다. 클라우드 기반 환경에서는 동일한 고속 스토리지 유형을 사용할 수 있습니다. 예를 들어, Amazon EC2에서는 임시 폴더에 [임시 드라이브](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) 드라이브를 사용할 수 있습니다.

서버에 충분한 메모리가 있다고 가정할 경우 RAM 드라이브를 구성합니다. Linux에서 다음 명령을 실행하여 8GB RAM 드라이브를 만듭니다.

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

Windows OS의 경우 타사 드라이버를 사용하여 RAM 드라이브를 만들거나 SSD와 같은 고성능 스토리지를 사용합니다.

고성능 임시 볼륨이 준비되면 JVM 매개변수를 설정합니다 `-Djava.io.tmpdir`. 예를 들어 다음 스크립트에서 아래 JVM 매개 변수를 `CQ_JVM_OPTS` 변수에 추가할 수 `bin/start` 있습니다 [!DNL Experience Manager].

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java 구성 {#java-configuration}

### Java 버전 {#java-version}

Adobe은 최적의 성능을 위해 Java 8 [!DNL Experience Manager Assets] 에 배포하는 것이 좋습니다.

<!-- TBD: Link to the latest official word around Java.
-->

### JVM 매개 변수 {#jvm-parameters}

다음 JVM 매개변수를 설정합니다.

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## 데이터 저장소 및 메모리 구성 {#data-store-and-memory-configuration}

### 파일 데이터 저장소 구성 {#file-data-store-configuration}

세그먼트 저장소에서 데이터 저장소를 분리하는 것이 모든 [!DNL Experience Manager Assets] 사용자에게 좋습니다. 또한, `maxCachedBinarySize` 및 `cacheSizeInMB` 매개 변수를 구성하면 성능을 극대화할 수 있습니다. 캐시에 저장할 수 `maxCachedBinarySize` 있는 가장 작은 파일 크기로 설정합니다. 내 데이터 저장소에 사용할 메모리 내 캐시의 크기를 지정합니다 `cacheSizeInMB`. Adobe에서는 이 값을 총 더미 크기의 2-10% 사이에 설정하는 것이 좋습니다. 그러나 로드/성능 테스트는 이상적인 설정을 결정하는 데 도움이 될 수 있습니다.

### 버퍼링된 이미지 캐시의 최대 크기 구성 {#configure-the-maximum-size-of-the-buffered-image-cache}

대용량 에셋을 업로드할 때 메모리 소모에서 예상치 못한 스파이크가 발생할 수 [!DNL Adobe Experience Manager]있고 OutOfMemoryErrors로 JVM이 실패하는 것을 방지하려면 버퍼링된 이미지 캐시의 구성된 최대 크기를 줄입니다. 최대 더미(- `Xmx`매개 변수)가 5GB이고, Oak BlobCache가 1GB로 설정되고, 문서 캐시가 2GB로 설정되는 시스템이 있는 경우를 생각해 보십시오. 이 경우 버퍼링된 캐시는 최대 1.25GB와 메모리를 사용하므로 예상치 못한 스파이크에 대해 0.75GB 메모리만 남습니다.

OSGi 웹 콘솔에서 버퍼링된 캐시 크기를 구성합니다. 에서 `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`속성을 바이트 단위 `cq.dam.image.cache.max.memory` 로 설정합니다. 예를 들어 1073741824는 1GB(1024 x 1024 x 1024 = 1GB)입니다.

Experience Manager 6.1 SP1에서 이 속성을 구성하기 위해 `sling:osgiConfig` 노드를 사용하는 경우 데이터 유형을 길게 설정해야 합니다. 자세한 내용은 자산 업로드 중 [CQBufferedImageCache가 힙을 소비함을 참조하십시오](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html).

### 공유 데이터 저장소 {#shared-data-stores}

S3 또는 공유 파일 데이터 저장소를 구현하면 디스크 공간을 절약하고 대규모 구현에서 네트워크 처리량을 늘리는 데 도움이 될 수 있습니다. 공유 데이터 저장소 사용에 대한 장단점에 대한 자세한 내용은 [자산 크기 조정 가이드를 참조하십시오](/help/assets/assets-sizing-guide.md).

### S3 data store {#s-data-store}

다음 S3 Data Store 구성( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`)을 통해 Adobe은 기존 파일 데이터 저장소에서 12.8TB의 바이너리 대용량 개체(BLOB)를 고객 사이트의 S3 데이터 저장소에 추출했습니다.

```conf
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

Adobe은 많은 회사가 HTTP 트래픽을 탐지하는 방화벽을 가지고 있기 때문에 파일 업로드 및 손상에 부정적인 영향을 줄 수 있습니다. 대용량 파일 업로드의 경우 WiFi 네트워크에 대한 유선 연결이 빠르게 포화상태에 도달하는지 확인합니다. 네트워크 병목 현상 식별에 대한 지침은 [자산 크기 조정 가이드를 참조하십시오](/help/assets/assets-sizing-guide.md). 네트워크 토폴로지를 분석하여 네트워크 성능을 평가하려면 [자산 네트워크 고려 사항을 참조하십시오](/help/assets/assets-network-considerations.md).

기본적으로 네트워크 최적화 전략은 사용 가능한 대역폭과 인스턴스의 로드에 따라 [!DNL Experience Manager] 달라집니다. 방화벽 또는 프록시를 비롯한 일반적인 구성 옵션을 통해 네트워크 성능을 향상시킬 수 있습니다. 다음은 기억해야 할 몇 가지 핵심 사항입니다.

* 인스턴스 유형(작은, 보통, 큰)에 따라 Experience Manager 인스턴스에 충분한 네트워크 대역폭이 있는지 확인합니다. AWS에서 호스팅되는 경우 적절한 대역폭 할당 [!DNL Experience Manager] 이 특히 중요합니다.
* 인스턴스가 AWS에서 호스팅되는 경우 다양한 크기 조정 정책을 통해 혜택을 볼 수 있습니다. [!DNL Experience Manager] 사용자가 높은 부하를 예상할 경우 인스턴스 크기를 조정합니다. 중간 로드/저부하 시 크기를 조정합니다.
* HTTPS:대부분의 사용자에게는 HTTP 트래픽을 탐지하는 방화벽이 있으므로 업로드 작업 중에 파일을 업로드하거나 손상된 파일을 업로드하는 데 악영향을 미칠 수 있습니다.
* 대용량 파일 업로드:사용자가 네트워크에 유선 연결이 있는지 확인합니다(WiFi 연결 채도가 빠르게).

## 워크플로우 {#workflows}

### 일시적인 워크플로우 {#transient-workflows}

가능한 경우 [!UICONTROL DAM 자산 업데이트] 워크플로우를 일시적 으로 설정합니다. 이 경우 워크플로우는 일반적인 추적 및 보관 프로세스를 통과하지 않아도 되기 때문에 워크플로우를 처리하는 데 필요한 오버헤드가 크게 줄어듭니다.

1. 배포 `/miscadmin` 에서 [!DNL Experience Manager] 로 이동합니다 `https://[aem_server]:[port]/miscadmin`.

1. 도구 **[!UICONTROL > 워크플로우]** **** > **[!UICONTROL 모델]** > **[!UICONTROL dam을]**&#x200B;확장합니다.

1. DAM **[!UICONTROL 자산 업데이트를 엽니다]**. 부동 도구 패널에서 **[!UICONTROL 페이지]** 탭으로 이동한 다음 **[!UICONTROL 페이지 속성을 클릭합니다]**.

1. 임시 워크플로우 **[!UICONTROL 를]** 선택하고 **[!UICONTROL 확인을 클릭합니다]**.

   >[!NOTE]
   >
   >일부 기능은 일시적인 워크플로우를 지원하지 않습니다. 배포에서 이러한 기능을 [!DNL Assets] 필요로 하는 경우 임시 워크플로우를 구성하지 마십시오.

일시적인 워크플로우를 사용할 수 없는 경우, 워크플로우 제거를 정기적으로 실행하여 보관된 [!UICONTROL DAM 자산] 업데이트 워크플로우를 삭제하여 시스템 성능이 저하되지 않도록 합니다.

일반적으로 매주 삭제 워크플로우를 실행합니다. 그러나 대규모 자산 처리 중 등 리소스를 많이 사용하는 시나리오에서는 보다 자주 실행할 수 있습니다.

워크플로우 제거를 구성하려면 OSGi 콘솔을 통해 새 Adobe [화강암 워크플로우 제거] 구성을 추가하십시오. 그런 다음 매주 유지 관리 창의 일부로 워크플로우를 구성하고 예약합니다.

숙제가 너무 오래 진행되면 시간이 초과됩니다. 따라서 워크플로우가 많아 삭제 워크플로가 완료되지 못하는 상황을 방지하려면 제거 작업이 완료되어야 합니다.

예를 들어, 워크플로우 인스턴스 노드를 만드는 비임시 워크플로우를 여러 번 실행한 후, [ACS AEM Commons 워크플로우 제거를](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) 애드혹 기준으로 실행할 수 있습니다. Adobe [Granite Workflow Purge] 스케줄러가 실행되기를 기다리는 대신, 중복되고 완료된 워크플로우 인스턴스를 즉시 제거합니다.

### 최대 병렬 작업 {#maximum-parallel-jobs}

기본적으로 서버의 프로세서 수와 같은 최대 병렬 작업 수를 [!DNL Experience Manager] 실행합니다. 이 설정의 문제는 부하가 많은 기간 동안 모든 프로세서가 [!UICONTROL DAM 자산] 업데이트 워크플로우에 의해 사용되고 UI 응답성이 저하되고 서버 성능 및 안정성을 보호하는 다른 프로세스가 실행되지 [!DNL Experience Manager] 않는다는 것입니다. 다음 단계를 수행하여 서버에서 사용할 수 있는 프로세서의 절반으로 이 값을 설정하는 것이 좋습니다.

1. 작성자에서 [!DNL Experience Manager] 액세스합니다 `https://[aem_server]:[port]/system/console/slingevent`.

1. [ **[!UICONTROL MOCK] Click Edit on each workflow queue that is released to your implementation, for example]** Granite Temporary Workflow Queue ****.

1. 최대 병렬 작업 값을 **[!UICONTROL 업데이트하고]** 저장을 **[!UICONTROL 클릭합니다]**.

대기열을 사용 가능한 프로세서의 절반까지 설정하는 것은 시작할 수 있는 솔루션입니다. 하지만 You may be increase or decrease this number to achieve maximum throughput and tune it by environment. 임시 및 비임시 워크플로우뿐만 아니라 외부 워크플로우와 같은 다른 프로세스에 대한 별도의 대기열이 있습니다. 프로세서의 50%로 설정된 여러 대기열이 동시에 활성 상태인 경우 시스템이 빠르게 과부하가 발생할 수 있습니다. 많이 사용되는 큐는 사용자 구현마다 매우 다릅니다. 따라서 서버 안정성을 훼손하지 않고 효율성을 최대화하기 위해 이러한 구성 요소를 신중하게 구성해야 할 수 있습니다.

### DAM 자산 업데이트 구성 {#dam-update-asset-configuration}

DAM [!UICONTROL 자산] 업데이트 워크플로우에는 Scene7 PTIFF 생성 및 [!DNL Adobe InDesign Server] 통합과 같은 작업에 대해 구성된 전체 단계 세트가 포함되어 있습니다. 그러나 대부분의 사용자는 이러한 단계를 여러 번 수행하지 않아도 됩니다. Adobe에서는 [!UICONTROL DAM 자산 업데이트 워크플로우 모델의 사용자 지정 복사본을] 만들고 불필요한 단계를 제거하는 것이 좋습니다. 이 경우 새 모델을 가리키도록 [!UICONTROL DAM 자산] 업데이트 릴리즈를 업데이트합니다.

DAM 자산 [!UICONTROL 업데이트] 워크플로우를 집중적으로 실행하면 파일 데이터베이스의 크기가 크게 증가할 수 있습니다. Adobe에서 수행한 실험 결과를 통해 약 5500개의 워크플로가 8시간 이내에 수행되는 경우 데이터 저장소 크기가 약 400GB까지 증가할 수 있음을 알 수 있습니다.

데이터 저장소 가비지 수집 작업을 실행하면 데이터 저장소가 원래 크기로 복원됩니다.

일반적으로 데이터 저장소 가비지 수집 작업은 다른 예약된 유지 관리 작업과 함께 매주 실행됩니다.

디스크 공간이 제한되어 있고 [!UICONTROL DAM 자산] 업데이트 워크플로우를 집중적으로 실행하는 경우 가비지 수집 작업을 보다 자주 예약하는 것이 좋습니다.

#### 런타임 변환 생성 {#runtime-rendition-generation}

고객은 웹 사이트에서 다양한 크기와 포맷의 이미지를 사용하거나 비즈니스 파트너에게 배포할 수 있습니다. 각 변환은 저장소에서 자산의 풋프린트에 추가되므로 Adobe은 이 기능을 신중하게 사용하는 것이 좋습니다. 이미지를 처리 및 저장하는 데 필요한 리소스를 줄이기 위해 이러한 이미지를 통합 도중 변환보다는 런타임에 생성할 수 있습니다.

많은 사이트 고객은 이미지 크기가 조정되고 이미지가 요청될 때 이미지가 잘리는 이미지 서블릿을 구현하므로 게시 인스턴스에 추가 로드를 적용합니다. 그러나 이러한 이미지를 캐시하는 한 이러한 문제를 해결할 수 있습니다.

또 다른 방법은 Scene7 기술을 사용하여 이미지 조작을 완전히 포기하는 것입니다. 또한 인프라에서 변환 생성 책임을 넘겨받는 브랜드 포털뿐만 아니라 전체 게시 계층도 배포할 수 [!DNL Experience Manager] 있습니다.

#### ImageMagick {#imagemagick}

ImageMagick을 사용하여 [!UICONTROL 변환을 생성하기 위해 DAM 자산] 업데이트 워크플로우를 사용자 지정하는 경우, Adobe은 다음 `policy.xml` 파일을 수정할 것을 `/etc/ImageMagick/`권장합니다. 기본적으로 ImageMagick은 OS 볼륨에서 사용 가능한 전체 디스크 공간과 사용 가능한 메모리를 사용합니다. 이러한 리소스를 제한하려면 의 섹션 `policymap` 내에서 다음 구성 `policy.xml` 을 변경합니다.

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

또한 `configure.xml` 파일(또는 환경 변수 설정)에 있는 ImageMagick의 임시 폴더 경로 `MAGIC_TEMPORARY_PATH`를 충분한 공간 및 IOPS가 있는 디스크 파티션으로 설정합니다.

>[!CAUTION]
>
>ImageMagick이 사용 가능한 모든 디스크 공간을 사용하는 경우 구성이 잘못되면 서버가 불안정해집니다. ImageMagick을 사용하여 대용량 파일을 처리하는 데 필요한 정책 변경 사항이 [!DNL Experience Manager] 성능에 영향을 줄 수 있습니다. 자세한 내용은 ImageMagick [설치 및 구성을 참조하십시오](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>ImageMagick `policy.xml` 과 `configure.xml` 파일은 `/usr/lib64/ImageMagick-&#42;/config/` 대신 사용할 수 `/etc/ImageMagick/`있습니다.구성 파일의 위치는 [ImageMagick 설명서를](https://www.imagemagick.org/script/resources.php) 참조하십시오.

Adobe Managed Services(AMS) [!DNL Experience Manager] 를 사용하는 경우 대용량 PSD 또는 PSB 파일을 처리할 계획인 경우 Adobe 고객 지원 센터에 문의하십시오. Adobe 고객 지원 센터 담당자와 협력하여 AMS 배포에 대한 이러한 모범 사례를 구현하고 Adobe의 독점 포맷에 적합한 최상의 툴과 모델을 선택할 수 있습니다. [!DNL Experience Manager] 3000 x 23000픽셀이 넘는 매우 고해상도 PSB 파일을 처리하지 못할 수 있습니다.

### XMP writeback {#xmp-writeback}

XMP writeback은 메타데이터를 수정할 때마다 원래 자산 [!DNL Experience Manager]을 업데이트하므로 다음과 같은 결과가 발생합니다.

* 자산 자체가 수정됨
* 자산의 버전이 만들어집니다.
* [!UICONTROL 자산에 대해] DAM 업데이트 자산 실행

나열된 결과는 상당한 자원을 소모한다. 따라서, Adobe은 필요하지 않은 경우 XMP Writeback [을 비활성화할](https://helpx.adobe.com/experience-manager/kb/disable-xmp-writeback.html)것을 권장합니다.

워크플로우 플래그 실행이 선택된 경우 대량의 메타데이터를 가져오면 리소스를 많이 소모하는 XMP 쓰기 복구 활동이 발생할 수 있습니다. 다른 사용자의 성능에 영향을 주지 않도록 서버 사용량 감소 시 이러한 가져오기를 계획합니다.

## 복제 {#replication}

예를 들어 사이트 구현에서 자산을 많은 수의 게시 인스턴스로 복제할 경우 체인 복제를 사용하는 것이 좋습니다. 이 경우 작성자 인스턴스가 단일 게시 인스턴스로 복제되어 다른 게시 인스턴스로 복제되며 작성자 인스턴스가 더 확보됩니다.

### 체인 복제 구성 {#configure-chain-replication}

1. 복제를 연결하는 데 사용할 게시 인스턴스 선택
1. 해당 게시 인스턴스에서 다른 게시 인스턴스를 가리키는 복제 에이전트 추가
1. 이러한 각 복제 에이전트의 &quot;트리거&quot; 탭에서 &quot;수신&quot; 설정

>[!NOTE]
>
>Adobe에서는 자산 자동 활성화를 권장하지 않습니다. 그러나 필요한 경우, Adobe은 이를 워크플로우의 마지막 단계인 일반적으로 DAM 자산 업데이트 단계로 수행하는 것이 좋습니다.

## 검색 색인 {#search-indexes}

최신 서비스 팩 및 성능 관련 핫픽스는 시스템 색인에 대한 업데이트를 자주 포함하므로 구현해야 합니다. 색인 [최적화에 대한 성능 조정 팁을](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) 참조하십시오.

자주 실행하는 쿼리에 대한 사용자 정의 색인을 만듭니다. 자세한 내용은 슬로우 쿼리 [분석](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) 및 사용자 정의 인덱스 [를 만드는 방법을 참조하십시오](/help/sites-deploying/queries-and-indexing.md). 쿼리 및 색인 우수 사례에 대한 추가 인사이트를 보려면 쿼리 및 색인 작성 [우수 사례를 참조하십시오](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Lucene 인덱스 구성 {#lucene-index-configurations}

일부 최적화는 [!DNL Experience Manager Assets] 성능을 향상시키는 데 도움이 되는 Oak 인덱스 구성에서 수행할 수 있습니다. 색인 구성을 업데이트하여 다시 색인 지정 시간을 개선합니다.

1. CRXDe `/crx/de/index.jsp` 를 열고 관리 사용자로 로그인합니다.
1. 로 `/oak:index/lucene`이동합니다.
1. 값 `String[]` , `excludedPaths` 및 `/var`가 있는 속성을 `/etc/workflow/instances`추가합니다 `/etc/replication`.
1. 로 `/oak:index/damAssetLucene`이동합니다. 값이 있는 `String[]` 속성 `includedPaths` 을 추가합니다 `/content/dam`. 변경 사항을 저장합니다.

사용자가 PDF 문서의 텍스트를 검색하는 것과 같이 자산의 전체 텍스트 검색을 수행할 필요가 없으면 비활성화할 수 있습니다. 전체 텍스트 인덱싱을 비활성화하여 색인 성능을 향상시킬 수 있습니다. 텍스트 [!DNL Apache Lucene] 추출을 비활성화하려면 다음 단계를 수행합니다.

1. 인터페이스에서 [!DNL Experience Manager] 패키지 관리자에 액세스합니다 .
1. disable_indexingbinarytextextraction-10.zip에서 사용할 수 있는 패키지를 [업로드하고 설치합니다](assets/disable_indexingbinarytextextraction-10.zip).

### Guess Total {#guess-total}

큰 결과 집합을 생성하는 쿼리를 만들 때는 매개 변수를 사용하여 실행 시 많은 메모리 사용을 방지합니다. `guessTotal`

## 알려진 문제 {#known-issues}

### 대용량 파일 {#large-files}

의 대형 파일과 관련하여 알려진 두 가지 주요 문제가 있습니다 [!DNL Experience Manager]. 파일의 크기가 2GB 이상인 경우 콜드 대기 동기화를 실행하면 메모리 부족 문제가 발생할 수 있습니다. 대기 동기화가 실행되지 않는 경우도 있습니다. 다른 경우, 기본 인스턴스가 충돌합니다. 이 시나리오는 컨텐츠 패키지를 포함하여 2GB보다 큰 모든 파일 [!DNL Experience Manager] 에 적용됩니다.

마찬가지로 공유 S3 데이터 저장소를 사용하는 동안 파일의 크기가 2GB에 도달하면 파일이 캐시에서 파일 시스템으로 완전히 지속되는 데 시간이 걸릴 수 있습니다. 따라서 바이너리 없는 복제를 사용할 경우 복제가 완료되기 전에 바이너리 데이터가 지속되지 않았을 수 있습니다. 이러한 상황은 특히 데이터 사용 가능성이 중요한 경우에 문제를 초래할 수 있습니다.

## 성능 테스트 {#performance-testing}

모든 [!DNL Experience Manager] 배포의 경우 병목 현상을 신속하게 식별하고 해결할 수 있는 성능 테스트 시스템을 구축할 수 있습니다. 여기에 초점을 맞춰야 할 몇 가지 주요 영역들이 있습니다.

### 네트워크 테스트 {#network-testing}

고객의 모든 네트워크 성능 문제에 대해 다음 작업을 수행하십시오.

* 고객 네트워크 내에서 네트워크 성능 테스트
* Adobe 네트워크 내에서 네트워크 성능을 테스트합니다. AMS 고객의 경우 Adobe 네트워크에서 테스트를 위해 CSE와 함께 작업하십시오.
* 다른 액세스 포인트에서 네트워크 성능 테스트
* 네트워크 벤치마크 도구 사용
* 디스패처 테스트

### [!DNL Experience Manager] 배포 테스트 {#aem-deployment-testing}

효율적인 CPU 사용률 및 로드 공유를 통해 지연율을 최소화하고 높은 처리량을 얻으려면 [!DNL Experience Manager] 배포의 성능을 정기적으로 모니터링합니다. 특히:

* 배포에 대해 로드 테스트를 [!DNL Experience Manager] 실행합니다.
* 업로드 성능 및 UI 응답성을 모니터링합니다.

## [!DNL Experience Manager Assets] 성과 점검 목록 및 자산 관리 작업의 영향 {#checklist}

* HTTPS를 사용하여 모든 회사 HTTP 트래픽 스니퍼를 검색할 수 있습니다.
* 대용량 에셋을 업로드하려면 유선 연결을 사용하십시오.
* Java 8에 배포합니다.
* 최적의 JVM 매개변수를 설정합니다.
* 파일 시스템 DataStore 또는 S3 데이터 저장소를 구성합니다.
* 하위 자산 생성을 비활성화합니다. 이 옵션이 활성화되어 있으면 AEM 워크플로우는 여러 페이지 자산의 각 페이지에 대해 별도의 자산을 만듭니다. 이러한 각 페이지는 추가 디스크 공간, 버전 관리 및 추가 워크플로우 처리가 필요한 개별 자산입니다. 별도의 페이지가 필요하지 않은 경우 하위 자산 생성 및 페이지 추출 활동을 비활성화합니다.
* 일시적인 워크플로우 활성화
* [화강암] 워크플로우 큐를 조정하여 동시 작업을 제한합니다.
* 리소스 소비를 [!DNL ImageMagick] 제한하도록 구성합니다.
* DAM 자산 [!UICONTROL 업데이트 워크플로우에서 불필요한 단계를] 제거합니다.
* 워크플로우 및 버전 제거를 구성합니다.
* 최신 서비스 팩 및 핫픽스를 사용하여 색인을 최적화할 수 있습니다. 사용할 수 있는 추가적인 색인 최적화는 Adobe 고객 지원 센터에 문의하십시오.
* questionTotal을 사용하여 쿼리 성능을 최적화합니다.
* [!DNL Experience Manager] AEM 웹 콘솔 **[!UICONTROL 에서]** 일 CQ DAM MIME 유형 서비스 ****&#x200B;를 활성화하여 파일 내용에서 파일 유형을 검색하도록 구성한 경우 리소스 사용량이 많은 시간이므로 사용량이 적은 시간에 많은 파일을 일괄 업로드합니다.
