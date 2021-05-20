---
title: 성능 조정 [!DNL Assets].
description: ' [!DNL Experience Manager] 구성, 병목 현상을 제거하고 성능을 최적화하기 위한 하드웨어, 소프트웨어 및 네트워크 구성 요소의 변경 사항에 대한 제안 및 지침 [!DNL Experience Manager Assets]'
contentOwner: AG
mini-toc-levels: 1
role: Architect, Administrator
feature: 자산 관리
exl-id: 1d9388de-f601-42bf-885b-6a7c3236b97e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2743'
ht-degree: 0%

---

<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] 성능 조정 가이드  {#assets-performance-tuning-guide}

[!DNL Experience Manager Assets] 설정에는 많은 수의 하드웨어, 소프트웨어 및 네트워크 구성 요소가 포함되어 있습니다. 배포 시나리오에 따라 성능 병목 현상을 제거하기 위해 하드웨어, 소프트웨어 및 네트워크 구성 요소에 대한 특정 구성 변경이 필요할 수 있습니다.

또한 특정 하드웨어 및 소프트웨어 최적화 지침을 식별하고 준수하면 [!DNL Experience Manager Assets] 배포를 통해 성능, 확장성 및 안정성에 대한 기대치를 충족할 수 있는 건전한 기반을 구축할 수 있습니다.

[!DNL Experience Manager Assets]의 성능이 좋지 않으면 대화형 성능, 자산 처리, 다운로드 속도 및 기타 영역과 관련된 사용자 환경에 영향을 줄 수 있습니다.

실제로 성능 최적화는 모든 프로젝트에 대한 타겟 지표를 설정하기 전에 수행해야 하는 기본적인 작업입니다.

다음은 성능 문제가 사용자에게 영향을 주기 전에 발견하여 해결하는 특정 주요 포커스 영역입니다.

## 플랫폼 {#platform}

Experience Manager은 많은 플랫폼에서 지원되지만 Adobe은 Linux 및 Windows에서 기본 도구에 대한 가장 많은 지원을 발견하여 최적의 성능과 구현의 편의성을 제공합니다. 가장 좋은 방법은 [!DNL Experience Manager Assets] 배포의 높은 메모리 요구 사항을 충족하기 위해 64비트 운영 체제를 구축하는 것입니다. 모든 Experience Manager 배포과 마찬가지로 TarMK를 가능한 모든 곳에서 구현해야 합니다. TarMK는 단일 작성자 인스턴스를 넘어 확장할 수 없지만 MongoMK보다 성능이 뛰어난 것으로 나타났습니다. TarMK 오프로드 인스턴스를 추가하여 [!DNL Experience Manager Assets] 배포의 워크플로우 처리 능력을 높일 수 있습니다.

### 임시 폴더 {#temp-folder}

자산 업로드 시간을 개선하려면 Java 임시 디렉토리에 대한 고성능 저장소를 사용합니다. Linux 및 Windows에서는 RAM 드라이브 또는 SSD를 사용할 수 있습니다. 클라우드 기반 환경에서는 동등한 고속 스토리지 유형을 사용할 수 있습니다. 예를 들어 Amazon EC2에서는 [사용 후 드라이브](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) 드라이브를 임시 폴더에 사용할 수 있습니다.

서버에 충분한 메모리가 있다고 가정할 경우 RAM 드라이브를 구성합니다. Linux에서 다음 명령을 실행하여 8GB RAM 드라이브를 만듭니다.

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

Windows OS에서는 타사 드라이버를 사용하여 RAM 드라이브를 만들거나 SSD와 같은 고성능 스토리지를 사용합니다.

고성능 임시 볼륨이 준비되면 JVM 매개 변수 `-Djava.io.tmpdir`을 설정합니다. 예를 들어 [!DNL Experience Manager] 의 `bin/start` 스크립트에서 아래의 JVM 매개 변수를 `CQ_JVM_OPTS` 변수에 추가할 수 있습니다.

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java 구성 {#java-configuration}

### Java 버전 {#java-version}

Adobe은 최적의 성능을 위해 Java 8에 [!DNL Experience Manager Assets]을 배포할 것을 권장합니다.

<!-- TBD: Link to the latest official word around Java.
-->

### JVM 매개 변수 {#jvm-parameters}

다음 JVM 매개 변수를 설정합니다.

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`= 500000
* `-Doak.queryLimitReads`= 100000
* `-Dupdate.limit`= 250000
* `-Doak.fastQuerySize`=true

## 데이터 저장소 및 메모리 구성 {#data-store-and-memory-configuration}

### 파일 데이터 저장소 구성 {#file-data-store-configuration}

모든 [!DNL Experience Manager Assets] 사용자에게 세그먼트 저장소에서 데이터 저장소를 분리하는 것이 좋습니다. 또한 `maxCachedBinarySize` 및 `cacheSizeInMB` 매개 변수를 구성하면 성능을 극대화할 수 있습니다. `maxCachedBinarySize` 을 캐시에서 저장할 수 있는 가장 작은 파일 크기로 설정합니다. `cacheSizeInMB` 내의 데이터 저장소에 사용할 메모리 내 캐시의 크기를 지정합니다. Adobe은 이 값을 총 heap 크기의 2-10% 이내로 설정할 것을 권장합니다. 그러나 로드/성능 테스트는 이상적인 설정을 결정하는 데 도움이 될 수 있습니다.

### 버퍼된 이미지 캐시의 최대 크기 구성 {#configure-the-maximum-size-of-the-buffered-image-cache}

많은 양의 자산을 [!DNL Adobe Experience Manager]에 업로드할 때, 메모리 소비에서 예기치 않은 스파이크가 발생하고 JVM이 OutOfMemoryErrors로 실패하지 않도록 버퍼링된 이미지 캐시의 구성된 최대 크기를 줄입니다. 최대 힙이 5GB이고, Oak BlobCache가 1GB로 설정되고, 문서 캐시가 2GB로 설정되는 시스템을 예로 들어 보겠습니다. `Xmx` 이 경우 버퍼링된 캐시는 최대 1.25GB와 메모리가 필요하므로 예기치 않은 스파이크에 대해서는 0.75GB 메모리만 남게 됩니다.

OSGi 웹 콘솔에서 버퍼된 캐시 크기를 구성합니다. `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`에서 `cq.dam.image.cache.max.memory` 속성을 바이트 단위로 설정합니다. 예를 들어 1073741824은 1GB(1024 x 1024 x 1024 = 1GB)입니다.

Experience Manager 6.1 SP1에서 이 속성을 구성하기 위해 `sling:osgiConfig` 노드를 사용하는 경우 데이터 형식을 Long으로 설정해야 합니다. 자세한 내용은 [CQBufferedImageCache가 자산 업로드 중 힙을 사용합니다](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html).

### 공유 데이터 저장소 {#shared-data-stores}

S3 또는 공유 파일 데이터 저장소를 구현하면 디스크 공간을 절약하고 대규모 구현에서 네트워크 처리량을 늘리는 데 도움이 될 수 있습니다. 공유 데이터 저장소 사용의 장단점에 대한 자세한 내용은 [자산 크기 조정 가이드](/help/assets/assets-sizing-guide.md)를 참조하십시오.

### S3 데이터 저장소 {#s-data-store}

다음 S3 데이터 저장소 구성( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`)은 Adobe이 기존 파일 데이터 저장소에서 고객 사이트의 S3 데이터 저장소로 12.8TB의 바이너리 대용량 개체(BLOB)를 추출하는 데 도움이 되었습니다.

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

Adobe은 많은 회사에 HTTP 트래픽을 감지하는 방화벽이 있어 이 방화벽이 있어 파일 업로드와 손상이 발생할 수 있습니다. 대용량 파일 업로드를 위해서는 WiFi 네트워크가 빠르게 포화되는 것을 방지하기 때문에 사용자가 네트워크에 유선 연결을 가지고 있는지 확인합니다. 네트워크 병목 현상을 식별하는 방법에 대한 지침은 [자산 크기 조정 가이드](/help/assets/assets-sizing-guide.md)를 참조하십시오. 네트워크 토폴로지를 분석하여 네트워크 성능을 평가하려면 [자산 네트워크 고려 사항](/help/assets/assets-network-considerations.md)을 참조하십시오.

주로, 네트워크 최적화 전략은 사용 가능한 대역폭 및 [!DNL Experience Manager] 인스턴스의 로드에 따라 다릅니다. 방화벽 또는 프록시를 포함한 일반적인 구성 옵션은 네트워크 성능을 개선하는 데 도움이 될 수 있습니다. 다음은 기억해야 할 몇 가지 주요 사항입니다.

* 인스턴스 유형(작은, 중간, 큰)에 따라 Experience Manager 인스턴스에 충분한 네트워크 대역폭이 있는지 확인하십시오. [!DNL Experience Manager] 이 AWS에서 호스팅되는 경우 대역폭 할당이 특히 중요합니다.
* [!DNL Experience Manager] 인스턴스가 AWS에서 호스팅되는 경우 다양한 스케일링 정책을 통해 이점을 얻을 수 있습니다. 사용자가 높은 로드를 예상하는 경우 인스턴스의 크기를 변경합니다. 중간/낮은 로드를 위해 크기를 줄입니다.
* HTTPS:대부분의 사용자에게는 HTTP 트래픽을 감지하는 방화벽이 있으므로 업로드 작업 중에 파일 업로드나 손상된 파일의 업로드에 부정적인 영향을 줄 수 있습니다.
* 큰 파일 업로드:사용자가 네트워크에 유선 연결을 했는지 확인합니다(WiFi 연결이 빠르게 채워짐).

## 워크플로우 {#workflows}

### 임시 워크플로우 {#transient-workflows}

가능하면 [!UICONTROL DAM 자산 업데이트] 워크플로우를 임시 워크플로우로 설정합니다. 이 설정은 워크플로우가 일반적인 추적 및 보관 프로세스를 통과하지 않아도 되므로 워크플로우를 처리하는 데 필요한 오버헤드를 크게 줄입니다.

1. `https://[aem_server]:[port]/miscadmin`의 [!DNL Experience Manager] 배포에서 `/miscadmin`으로 이동합니다.

1. **[!UICONTROL 도구]** > **[!UICONTROL 워크플로우]** > **[!UICONTROL 모델]** > **[!UICONTROL dam]**&#x200B;을 확장합니다.

1. **[!UICONTROL DAM 자산 업데이트]**&#x200B;를 엽니다. 부동 도구 패널에서 **[!UICONTROL 페이지]** 탭으로 전환한 다음 **[!UICONTROL 페이지 속성]**&#x200B;을 클릭합니다.

1. **[!UICONTROL 임시 워크플로우]**&#x200B;를 선택하고 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >일부 기능은 임시 워크플로우를 지원하지 않습니다. [!DNL Assets] 배포에 이러한 기능이 필요한 경우 임시 워크플로우를 구성하지 마십시오.

임시 워크플로우를 사용할 수 없는 경우 정기적으로 워크플로우 제거를 실행하여 보관된 [!UICONTROL DAM 자산 업데이트] 워크플로우를 삭제하여 시스템 성능이 저하되지 않도록 하십시오.

일반적으로 매주 삭제 워크플로우를 실행합니다. 그러나 대규모 자산 수집 중과 같이 리소스를 많이 사용하는 시나리오에서는 더 자주 실행할 수 있습니다.

워크플로우 삭제를 구성하려면 OSGi 콘솔을 통해 새 Adobe Granite Workflow 제거 구성을 추가합니다. 그런 다음 워크플로우를 주별 유지 관리 창의 일부로 구성하고 예약합니다.

퍼징이 너무 오래 실행되면 시간이 초과됩니다. 따라서 많은 수의 워크플로우로 인해 워크플로우 제거를 완료하지 못하는 상황을 방지하려면 작업 제거를 완료해야 합니다.

예를 들어, 워크플로 인스턴스 노드를 만드는 많은 비임시 워크플로우를 실행한 후 임시 단위로 [ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html)를 실행할 수 있습니다. Granite Workflow 제거 스케줄러가 실행될 때까지 기다리지 않고 중복되고 완료된 워크플로우 인스턴스를 즉시 제거합니다.

### 최대 병렬 작업 {#maximum-parallel-jobs}

기본적으로 [!DNL Experience Manager]은(는) 서버의 프로세서 수와 동일한 최대 병렬 작업 수를 실행합니다. 이 설정의 문제는 로드가 많은 동안 모든 프로세서가 [!UICONTROL DAM Update Asset] 워크플로우에 의해 사용되고 UI 응답성이 느려지고 [!DNL Experience Manager] 가 서버 성능과 안정성을 보호하는 다른 프로세스를 실행하지 못하도록 한다는 것입니다. 이 값은 다음 단계를 수행하여 서버에서 사용할 수 있는 프로세서의 절반으로 설정하는 것이 좋습니다.

1. [!DNL Experience Manager] 작성자에서 `https://[aem_server]:[port]/system/console/slingevent`에 액세스합니다.

1. 구현과 관련된 각 워크플로우 큐(예: **[!UICONTROL Granite Transient Workflow 큐]**)에서 **[!UICONTROL 편집]**&#x200B;을 클릭합니다.

1. **[!UICONTROL 최대 병렬 작업]** 값을 업데이트하고 **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

대기열을 사용 가능한 프로세서의 절반으로 설정하는 것은 시작할 수 있는 솔루션입니다. 그러나 최대 처리량을 달성하고 환경에 따라 조정하려면 이 수를 늘리거나 줄여야 할 수도 있습니다. 외부 워크플로우와 같은 다른 프로세스뿐만 아니라 임시 및 임시 워크플로우에 대한 별도의 큐가 있습니다. 프로세서가 50%로 설정된 여러 개의 큐가 동시에 활성화되면 시스템이 빠르게 오버로드될 수 있습니다. 많이 사용되는 큐는 사용자 구현마다 매우 다릅니다. 따라서 서버 안정성을 손상시키지 않고 최대 효율성을 위해 신중하게 구성해야 할 수 있습니다.

### DAM 자산 구성 업데이트 {#dam-update-asset-configuration}

[!UICONTROL DAM 자산 업데이트] 워크플로우에는 Dynamic Media PTIFF 생성 및 [!DNL Adobe InDesign Server] 통합과 같은 작업에 대해 구성된 전체 단계 세트가 포함되어 있습니다. 그러나 대부분의 사용자는 이러한 단계 중 일부가 필요하지 않을 수 있습니다. Adobe은 [!UICONTROL DAM 자산 업데이트] 워크플로우 모델의 사용자 지정 복사본을 만들고 불필요한 단계를 제거하는 것이 좋습니다. 이 경우 [!UICONTROL DAM 자산 업데이트]에 대한 런처를 업데이트하여 새 모델을 가리킵니다.

[!UICONTROL DAM 자산 업데이트] 워크플로우를 집중적으로 실행하면 파일 데이터 저장소의 크기를 크게 늘릴 수 있습니다. Adobe에서 수행한 실험 결과에 따르면 약 5500 워크플로우가 8시간 내에 수행되는 경우 데이터 저장소 크기가 약 400GB까지 증가할 수 있습니다.

데이터 저장소 가비지 수집 작업을 실행한 후 데이터 저장소가 원래 크기로 복원됩니다.

일반적으로 데이터 저장소 가비지 수집 작업은 다른 예약된 유지 관리 작업과 함께 매주 실행됩니다.

디스크 공간이 제한되어 있고 [!UICONTROL DAM 자산 업데이트] 워크플로우를 집중적으로 실행하는 경우 가비지 수집 작업 예약을 더 자주 고려하십시오.

#### 런타임 변환 생성 {#runtime-rendition-generation}

고객은 웹 사이트에서 다양한 크기와 형식의 이미지를 사용하거나 비즈니스 파트너에게 배포할 수 있습니다. 각 표현물이 리포지토리에서 자산의 풋프린트에 추가되므로, 이 기능을 신중하게 사용하는 것이 좋습니다. 이미지를 처리하고 저장하는 데 필요한 리소스의 양을 줄이기 위해 이러한 이미지를 섭취 중 변환보다는 런타임 시 생성할 수 있습니다.

많은 Sites 고객은 요청 시 이미지의 크기를 조정하고 자르기를 수행하는 이미지 서블릿을 구현하여 게시 인스턴스에 추가 로드를 부과합니다. 그러나 이러한 이미지를 캐시하는 한 이러한 문제를 완화할 수 있습니다.

다른 방법은 Dynamic Media 기술을 사용하여 완전히 핸드오프 이미지 조작을 수행하는 것입니다. 또한 [!DNL Experience Manager] 인프라에서 렌디션 생성 책임을 맡을 뿐만 아니라 전체 게시 계층도 넘겨주는 Brand Portal을 배포할 수 있습니다.

#### ImageMagick {#imagemagick}

[!UICONTROL DAM 자산 업데이트] 워크플로우를 사용자 지정하여 ImageMagick를 사용하여 렌디션을 생성하는 경우 `/etc/ImageMagick/`에서 `policy.xml` 파일을 수정하는 것이 좋습니다. 기본적으로 ImageMagick는 OS 볼륨의 사용 가능한 전체 디스크 공간과 사용 가능한 메모리를 사용합니다. `policy.xml` 의 `policymap` 섹션 내에서 다음 구성을 변경하여 이러한 리소스를 제한합니다.

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

또한 `configure.xml` 파일에서 ImageMagick의 임시 폴더 경로를 설정하거나 환경 변수 `MAGIC_TEMPORARY_PATH`)를 충분한 공간 및 IOPS가 있는 디스크 파티션으로 설정합니다.

>[!CAUTION]
>
>ImageMagick가 사용 가능한 모든 디스크 공간을 사용하는 경우 구성이 잘못되면 서버가 불안정해질 수 있습니다. ImageMagick를 사용하여 큰 파일을 처리하는 데 필요한 정책 변경 사항은 [!DNL Experience Manager] 성능에 영향을 줄 수 있습니다. 자세한 내용은 [ImageMagick](/help/assets/best-practices-for-imagemagick.md) 설치 및 구성 을 참조하십시오.

>[!NOTE]
>
>ImageMagick `policy.xml` 및 `configure.xml` 파일은 `/etc/ImageMagick/` 대신 `/usr/lib64/ImageMagick-&#42;/config/`에서 사용할 수 있습니다.구성 파일의 위치는 [ImageMagick 설명서](https://www.imagemagick.org/script/resources.php)를 참조하십시오.

AMS(Adobe Managed Services)에서 [!DNL Experience Manager] 을(를) 사용하는 경우 대용량 PSD 또는 PSB 파일을 많이 처리할 계획이면 Adobe 고객 지원 센터에 문의하십시오. Adobe 고객 지원 담당자와 협력하여 AMS 배포에 대한 이러한 모범 사례를 구현하고 Adobe의 독점 형식에 가장 적합한 도구와 모델을 선택하십시오. [!DNL Experience Manager] 30000 x 23000 픽셀보다 큰 고해상도 PSB 파일을 처리할 수 없습니다.

### XMP 원본에 쓰기 {#xmp-writeback}

XMP 원본에 쓰기 기능은 [!DNL Experience Manager]에서 메타데이터가 수정될 때마다 원래 자산을 업데이트하므로, 다음과 같은 결과가 발생합니다.

* 자산 자체가 수정됨
* 자산의 버전이 만들어집니다
* [!UICONTROL DAM 자산 ] 업데이트 자산이 자산에 대해 실행됩니다

나열된 결과는 상당한 자원을 소모한다. 따라서 Adobe은 필요하지 않은 경우 [XMP 원본에 쓰기](https://helpx.adobe.com/experience-manager/kb/disable-xmp-writeback.html)를 사용하지 않도록 설정하는 것이 좋습니다.

워크플로우 실행 플래그를 선택하면 대량의 메타데이터를 가져오면 리소스 집약적인 XMP 원본에 쓰기 활동이 발생할 수 있습니다. 다른 사용자의 성능에 영향을 주지 않도록 서버 사용 공간을 적게 사용하는 동안 이러한 가져오기를 계획합니다.

## 복제 {#replication}

자산을 많은 수의 게시 인스턴스로 복제할 때(예: 사이트 구현에서) Adobe은 체인 복제를 사용하는 것을 권장합니다. 이 경우 작성자 인스턴스는 단일 게시 인스턴스로 복제되고, 이렇게 되면 다른 게시 인스턴스로 복제되어 작성자 인스턴스를 늘립니다.

### 체인 복제 구성 {#configure-chain-replication}

1. 복제 체인에 사용할 게시 인스턴스를 선택합니다
1. 해당 게시 인스턴스에서 다른 게시 인스턴스를 가리키는 복제 에이전트를 추가합니다
1. 이러한 각 복제 에이전트에서 &quot;Triggers&quot; 탭에서 &quot;On Receive&quot;를 활성화합니다

>[!NOTE]
>
>Adobe에서는 자산을 자동 활성화하지 않는 것이 좋습니다. 그러나 필요한 경우 Adobe에서 이를 워크플로우의 마지막 단계로 수행하는 것이 좋습니다(일반적으로 DAM 자산 업데이트).

## 인덱스 검색 {#search-indexes}

시스템 인덱스에 대한 업데이트를 포함하는 최신 서비스 팩](/help/release-notes/sp-release-notes.md) 및 성능 관련 핫픽스를 설치합니다. [ 일부 인덱스 최적화는 [성능 조정 팁](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)을 참조하십시오.

자주 실행하는 쿼리에 대한 사용자 지정 인덱스를 만듭니다. 자세한 내용은 [느린 쿼리 분석 방법](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) 및 [사용자 지정 인덱스 작성](/help/sites-deploying/queries-and-indexing.md)을 참조하십시오. 쿼리 및 색인 우수 사례에 대한 추가 인사이트를 보려면 [쿼리 및 색인 생성에 대한 우수 사례](/help/sites-deploying/best-practices-for-queries-and-indexing.md)를 참조하십시오.

### Lucene 인덱스 구성 {#lucene-index-configurations}

일부 최적화는 [!DNL Experience Manager Assets] 성능을 개선하는 데 도움이 되는 Oak 색인 구성에서 수행할 수 있습니다. 색인 구성을 업데이트하여 다시 색인화 시간을 개선합니다.

1. CRXDe `/crx/de/index.jsp`를 열고 관리 사용자로 로그인합니다.
1. `/oak:index/lucene`(으)로 이동합니다.
1. `/var`, `/etc/workflow/instances` 및 `/etc/replication` 값이 있는 `String[]` 속성을 추가합니다.`excludedPaths`
1. `/oak:index/damAssetLucene`(으)로 이동합니다. `/content/dam` 값을 사용하여 `String[]` 속성 `includedPaths`을 추가합니다. 변경 사항을 저장합니다.

사용자가 자산의 전체 텍스트 검색을 수행하지 않아도 됩니다(예: PDF 문서에서 텍스트를 검색하는 경우). 전체 텍스트 인덱스를 비활성화하여 인덱스 성능을 향상시킬 수 있습니다. [!DNL Apache Lucene] 텍스트 추출을 비활성화하려면 다음 단계를 수행합니다.

1. [!DNL Experience Manager] 인터페이스에서 [!UICONTROL 패키지 관리자]에 액세스합니다.
1. [disable_indexingbinarytextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip)에서 사용할 수 있는 패키지를 업로드하고 설치합니다.

### Guess Total {#guess-total}

큰 결과 세트를 생성하는 쿼리를 만들 때 `guessTotal` 매개 변수를 사용하여 실행할 때 메모리 사용량이 많은 것을 방지합니다.

## 알려진 문제 {#known-issues}

### 큰 파일 {#large-files}

[!DNL Experience Manager]에 있는 큰 파일과 관련하여 알려진 두 가지 주요 문제가 있습니다. 파일이 2GB보다 큰 크기에 도달하면 콜드 대기 동기화가 메모리 부족 상태로 발생할 수 있습니다. 대기 동기화가 실행되지 않는 경우도 있습니다. 다른 경우에는 기본 인스턴스가 충돌합니다. 이 시나리오는 컨텐츠 패키지를 포함하여 2GB보다 큰 [!DNL Experience Manager] 의 모든 파일에 적용됩니다.

마찬가지로 공유 S3 데이터 저장소를 사용하는 동안 파일의 크기가 2GB에 도달하면 파일이 캐시에서 파일 시스템으로 완전히 지속되는 데 시간이 걸릴 수 있습니다. 따라서 바이너리 없는 복제를 사용할 때 복제가 완료되기 전에 바이너리 데이터가 지속되지 않았을 수 있습니다. 이러한 경우 특히 데이터 가용성이 중요한 경우 문제가 발생할 수 있습니다.

## 성능 테스트 {#performance-testing}

모든 [!DNL Experience Manager] 배포에 대해 병목 현상을 신속하게 식별하고 해결할 수 있는 성능 테스트 시스템을 구축하십시오. 여기에 초점을 맞출 몇 가지 주요 영역들이 있습니다.

### 네트워크 테스트 {#network-testing}

고객의 모든 네트워크 성능 문제에 대해 다음 작업을 수행하십시오.

* 고객 네트워크 내에서 네트워크 성능 테스트
* Adobe 네트워크 내에서 네트워크 성능을 테스트합니다. AMS 고객의 경우 CSE와 협력하여 Adobe 네트워크에서 테스트합니다.
* 다른 액세스 포인트에서 네트워크 성능 테스트
* 네트워크 벤치마크 도구 사용
* 디스패처에 대해 테스트

### [!DNL Experience Manager] 배포 테스트  {#aem-deployment-testing}

효율적인 CPU 사용률 및 로드 공유를 통해 지연을 최소화하고 높은 처리량을 얻으려면 정기적으로 [!DNL Experience Manager] 배포 성능을 모니터링하십시오. 특히

* [!DNL Experience Manager] 배포에 대해 로드 테스트를 실행합니다.
* 업로드 성능 및 UI 응답성을 모니터링합니다.

## [!DNL Experience Manager Assets] 성능 검사 목록 및 자산 관리 작업의 영향 {#checklist}

* HTTPS를 활성화하여 기업의 HTTP 트래픽 스니퍼들을 파악합니다.
* 자산 업로드를 위해 유선 연결을 사용합니다.
* Java 8에 배포합니다.
* 최적의 JVM 매개 변수를 설정합니다.
* 파일 시스템 데이터 저장소 또는 S3 데이터 저장소를 구성합니다.
* 하위 자산 생성을 비활성화합니다. 활성화되어 있으면 AEM 워크플로우는 다중 페이지 자산의 각 페이지에 대해 별도의 자산을 만듭니다. 이러한 각 페이지는 추가 디스크 공간을 사용하고, 버전 관리를 필요로 하며, 추가 워크플로우 처리를 필요로 하는 개별 자산입니다. 별도의 페이지가 필요하지 않으면 하위 자산 생성 및 페이지 추출 활동을 비활성화합니다.
* 임시 워크플로우를 활성화합니다.
* Granite 워크플로우 큐를 조정하여 동시 작업을 제한합니다.
* 리소스 소비를 제한하려면 [!DNL ImageMagick]을 구성합니다.
* [!UICONTROL DAM 자산 업데이트] 워크플로우에서 불필요한 단계를 제거합니다.
* 워크플로우 및 버전 제거를 구성합니다.
* 최신 서비스 팩 및 핫픽스로 인덱스를 최적화합니다. 사용할 수 있는 추가 인덱스 최적화에 대해서는 Adobe 고객 지원 센터에 문의하십시오.
* guessTotal을 사용하여 쿼리 성능을 최적화합니다.
* 파일 컨텐츠에서 파일 유형을 검색하도록 [!DNL Experience Manager]을 구성하는 경우(**[!UICONTROL AEM Web Console]**&#x200B;에서 **[!UICONTROL Day CQ DAM MIME 유형 서비스]**&#x200B;를 활성화), 비스파이크 시간 동안 많은 파일을 리소스 집약이므로 대량으로 업로드하십시오.
