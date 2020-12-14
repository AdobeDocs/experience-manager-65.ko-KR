---
title: AEM 6에서 노드 저장소 및 데이터 저장소 구성
seo-title: AEM 6에서 노드 저장소 및 데이터 저장소 구성
description: 노드 저장소 및 데이터 저장소를 구성하는 방법과 데이터 저장소 가비지 수집을 수행하는 방법에 대해 알아봅니다.
seo-description: 노드 저장소 및 데이터 저장소를 구성하는 방법과 데이터 저장소 가비지 수집을 수행하는 방법에 대해 알아봅니다.
uuid: 1a58c0ba-1c32-4539-ad0d-0a27c8c4ff5e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: b97482f2-2791-4d14-ae82-388302d9eab3
docset: aem65
legacypath: /deploy/platform/data-store-config
translation-type: tm+mt
source-git-commit: 93cb84763cfd77b67a5dd1481caab79337f6e7c4
workflow-type: tm+mt
source-wordcount: '3423'
ht-degree: 1%

---


# AEM 6{#configuring-node-stores-and-data-stores-in-aem}에 노드 저장소 및 데이터 저장소 구성

## 소개 {#introduction}

Adobe Experience Manager(AEM)에서 이진 데이터는 컨텐츠 노드와는 독립적으로 저장할 수 있습니다. 이진 데이터는 데이터 저장소에 저장되는 반면 컨텐츠 노드는 노드 저장소에 저장됩니다.

데이터 스토어와 노드 스토어는 모두 OSGi 구성을 사용하여 구성할 수 있습니다. 각 OSGi 구성은 PID(영구 식별자)를 사용하여 참조됩니다.

## 구성 단계 {#configuration-steps}

노드 저장소와 데이터 저장소를 모두 구성하려면 다음 단계를 수행하십시오.

1. AEM quickstart JAR 파일을 해당 설치 디렉토리에 복사합니다.
1. 설치 디렉토리에 `crx-quickstart/install` 폴더를 만듭니다.
1. 먼저 `crx-quickstart/install` 디렉터리에 사용할 노드 저장소 옵션의 이름으로 구성 파일을 만들어 노드 저장소를 구성합니다.

   예를 들어, 문서 노드 저장소(AEM MongoMK 구현의 기반)는 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config` 파일을 사용합니다.

1. 파일을 편집하고 구성 옵션을 설정합니다.
1. 사용할 데이터 저장소의 PID를 사용하여 구성 파일을 만듭니다. 파일을 편집하여 구성 옵션을 설정합니다.

   >[!NOTE]
   >
   >구성 옵션은 [노드 저장소 구성](#node-store-configurations) 및 [데이터 저장소 구성](#data-store-configurations)을 참조하십시오.

1. AEM을 시작합니다.

## 노드 저장소 구성 {#node-store-configurations}

>[!CAUTION]
>
>최신 버전의 Oak에서는 OSGi 구성 파일에 대해 새로운 이름 지정 체계와 형식을 사용합니다. 새 이름 지정 체계를 사용하려면 구성 파일의 이름을 **.config**&#x200B;로 지정해야 하고 새 형식은 값을 입력해야 하며 여기에 [문서화되어야 합니다](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>
>이전 버전의 Oak에서 업그레이드하는 경우 먼저 `crx-quickstart/install` 폴더를 백업하십시오. 업그레이드 후 폴더의 컨텐츠를 업그레이드된 설치 프로그램으로 복원하고 구성 파일의 확장을 **.cfg**&#x200B;에서 **.config**&#x200B;로 수정합니다.
>
>**AEM 5.x** 설치에서 업그레이드할 준비를 위해 이 문서를 읽고 있는 경우 먼저 [업그레이드](https://docs.adobe.com/content/docs/en/aem/6-0/deploy/upgrade.html) 설명서를 참조하십시오.

### 세그먼트 노드 저장소 {#segment-node-store}

세그먼트 노드 저장소는 AEM6에서 Adobe의 TarMK 구현의 기반입니다. 구성에 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` PID를 사용합니다.

>[!CAUTION]
>
>세그먼트 노드 저장소에 대한 PID가 AEM 6.3에서 AEM 6의 `org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions`에서 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService`으로 변경되었습니다. 이 변경 사항을 반영하기 위해 필요한 구성 조정을 하십시오.

다음 옵션을 구성할 수 있습니다.

* `repository.home`:저장소 관련 데이터가 저장되는 저장소 홈의 경로입니다. 기본적으로 세그먼트 파일은 `crx-quickstart/segmentstore` 디렉토리 아래에 저장됩니다.

* `tarmk.size`:세그먼트의 최대 크기(MB)입니다. 기본 최대값은 256MB입니다.
* `customBlobStore`:사용자 지정 데이터 저장소가 사용되었음을 나타내는 부울 값입니다. AEM 6.3 이상 버전의 경우 기본값은 true입니다. AEM 6.3 이전에는 기본값이 false였습니다.

다음은 샘플 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` 파일입니다.

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### 문서 노드 저장소 {#document-node-store}

문서 노드 저장소는 AEM MongoMK 구현의 기반입니다. `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`* *PID를 사용합니다. 다음 구성 옵션을 사용할 수 있습니다.

* `mongouri`:Mongo  [](https://docs.mongodb.org/manual/reference/connection-string/) 데이터베이스에 연결하는 데 필요한 MongoURI입니다. 기본값은 입니다.`mongodb://localhost:27017`

* `db`:Mongo 데이터베이스의 이름입니다. 기본값은 기본 데이터베이스 이름으로 **Oak** ``. However, new AEM 6 installations use **aem-author** ``입니다.

* `cache`:캐시 크기(MB)입니다. DocumentNodeStore에서 사용되는 다양한 캐시 간에 배포됩니다. 기본값은 입니다.`256`

* `changesSize`:비교 출력을 캐싱하는 데 Mongo에 사용된 제한적 컬렉션의 크기(MB)입니다. 기본값은 입니다.`256`

* `customBlobStore`:사용자 지정 데이터 저장소가 사용됨을 나타내는 부울 값입니다. 기본값은 `false`입니다.

다음은 샘플 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config` 파일입니다.

```shell
#Mongo server details
mongouri="mongodb://localhost:27017"

#Name of Mongo database to use
db="aem-author"

#Store binaries in custom BlobStore
customBlobStore=B"false"
```

## 데이터 저장소 구성 {#data-store-configurations}

많은 바이너리를 처리할 때 성능을 최대화하기 위해 기본 노드 저장소 대신 외부 데이터 저장소를 사용하는 것이 좋습니다.

예를 들어 프로젝트에 많은 미디어 에셋이 필요한 경우 파일 또는 S3 데이터 저장소에 미디어 에셋을 저장하면 MongoDB에 직접 저장하는 것보다 더 빠르게 액세스할 수 있습니다.

파일 데이터 저장소는 MongoDB보다 성능이 우수하며 Mongo 백업 및 복원 작업은 많은 에셋으로 인해 느립니다.

다른 데이터 저장소 및 구성에 대한 세부 사항은 아래에 설명되어 있습니다.

>[!NOTE]
>
>사용자 지정 데이터 스토어를 활성화하려면 해당 노드 저장소 구성 파일([세그먼트 노드 저장소](/help/sites-deploying/data-store-config.md#segment-node-store) 또는 [문서 노드 저장소](/help/sites-deploying/data-store-config.md#document-node-store))에서 `customBlobStore`이(가) `true`으로 설정되어 있는지 확인해야 합니다.

### 파일 데이터 저장소 {#file-data-store}

이것은 Jackrabbit 2에 있는 [FileDataStore](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/core/data/FileDataStore.html)의 구현입니다. 이진 데이터를 파일 시스템에 일반 파일로 저장할 수 있습니다. `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore` PID를 사용합니다.

다음 구성 옵션을 사용할 수 있습니다.

* `repository.home`:다양한 저장소 관련 데이터가 저장되는 저장소 홈의 경로. 기본적으로 이진 파일은 `crx-quickstart/repository/datastore` 디렉토리 아래에 저장됩니다

* `path`:파일을 저장할 디렉토리 경로입니다. 지정한 경우 `repository.home` 값보다 우선합니다.

* `minRecordLength`:데이터 저장소에 저장된 파일의 최소 크기(바이트)입니다. 이 값보다 작은 바이너리 컨텐츠가 삽입됩니다.

>[!NOTE]
>
>NAS를 사용하여 공유 파일 데이터 저장소를 저장할 때는 성능 문제가 발생하지 않도록 고성능 디바이스만 사용해야 합니다.

## Amazon S3 데이터 저장소 {#amazon-s-data-store}

AEM은 Amazon의 Simple Storage Service(S3)에 데이터를 저장하도록 구성할 수 있습니다. 구성에 `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` PID를 사용합니다.

S3 데이터 저장소 기능을 활성화하려면 S3 데이터 저장소 커넥터가 포함된 기능 팩을 다운로드하여 설치해야 합니다. [Adobe 저장소](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)로 이동하여 기능 팩의 1.10.x 버전(예: com.adobe.granite.oak.s3connector-1.10.0.zip)에서 최신 버전을 다운로드합니다. 또한 [AEM 6.5 릴리스 노트](/help/release-notes/sp-release-notes.md) 페이지에 나열된 최신 AEM 서비스 팩을 다운로드하고 설치해야 합니다.

>[!NOTE]
>
>TarMK와 함께 AEM을 사용하는 경우 바이너리는 기본적으로 `FileDataStore`에 저장됩니다. S3 데이터 저장소에 TarMK를 사용하려면 `crx3tar-nofds` 실행 모드를 사용하여 AEM을 시작해야 합니다. 예:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

다운로드가 완료되면 다음과 같이 S3 커넥터를 설치하고 구성할 수 있습니다.

1. 기능 팩 zip 파일의 내용을 임시 폴더에 추출합니다.

1. 임시 폴더로 이동하여 다음 위치로 이동합니다.

   ```xml
   jcr_root/libs/system/install
   ```

   위 위치의 모든 내용을 `<aem-install>/crx-quickstart/install.`(으)로 복사

1. AEM이 Tar 또는 MongoDB 저장소에서 작동하도록 이미 구성된 경우 계속하기 전에 ***&lt;aem-install>***/*crx-quickstart*/*install* 폴더에서 기존 구성 파일을 제거하십시오. 제거해야 하는 파일은 다음과 같습니다.

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 기능 팩이 추출된 임시 위치로 돌아가서 다음 폴더의 내용을 복사합니다.

   * `jcr_root/libs/system/config`

   끝

   * `<aem-install>/crx-quickstart/install`

   현재 구성에 필요한 구성 파일만 복사해야 합니다. 전용 데이터 저장소와 공유 데이터 저장소 설정 모두에 대해 `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` 파일이 복사됩니다.

   >[!NOTE]
   >
   >클러스터 설정에서 클러스터의 모든 노드에서 위의 단계를 하나씩 수행합니다. 또한 모든 노드에 동일한 S3 설정을 사용해야 합니다.

1. 파일을 편집하고 설정에 필요한 구성 옵션을 추가합니다.
1. AEM을 시작합니다.

### 1.10.x S3 커넥터의 새 버전 {#upgrading-to-a-new-version-of-the-s-connector}으로 업그레이드

1.10.x S3 커넥터의 새 버전(예: 1.10.0에서 1.10.4)으로 업그레이드해야 하는 경우 다음 단계를 수행합니다.

1. AEM 인스턴스를 중지합니다.

1. AEM 설치 폴더의 `<aem-install>/crx-quickstart/install/15`으로 이동하여 해당 콘텐트를 백업합니다.
1. 백업 후 `<aem-install>/crx-quickstart/install/15` 폴더에 있는 모든 jar 파일을 삭제하여 이전 버전의 S3 Connector 및 해당 종속성을 삭제합니다. 예:

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >위에 표시된 파일 이름은 일러스트레이션 용도로만 사용됩니다.

1. [Adobe 저장소](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)에서 최신 버전의 1.8.x 기능 팩을 다운로드합니다.
1. 컨텐츠를 별도의 폴더에 압축 해제한 다음 `jcr_root/libs/system/install/15`으로 이동합니다.
1. jar 파일을 AEM 설치 폴더의 **&lt;aem-install>**/crx-quickstart/install/15에 복사합니다.
1. AEM을 시작하고 커넥터 기능을 확인합니다.

다음 옵션을 사용하여 구성 파일을 사용할 수 있습니다.

* accessKey:AWS 액세스 키.
* secretKey:AWS 비밀 액세스 키. **참고:** 또는  [IAM ](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) 롤셋을 인증에 사용할 수 있습니다. IAM 역할을 사용하는 경우 더 이상 `accessKey` 및 `secretKey`을 지정하지 않아도 됩니다.

* s3버킷:버킷 이름.
* s3영역:버킷 영역입니다.
* 경로:데이터 저장소의 경로입니다. 기본값은 **&lt;AEM install folder>/repository/datastore**&#x200B;입니다.
* minRecordLength:데이터 저장소에 저장해야 하는 개체의 최소 크기입니다. 최소/기본값은 **16KB입니다.**
* maxCachedBinarySize:이 크기보다 작거나 같은 바이너리는 메모리 캐시에 저장됩니다. 크기는 바이트 단위입니다. 기본값은 **17408 **(17KB)입니다.

* cacheSize:캐시의 크기입니다. 값이 바이트 단위로 지정됩니다. 기본값은 **64GB**&#x200B;입니다.
* 비밀:공유 데이터 저장소 설정에 바이너리 없는 복제를 사용하는 경우에만 사용됩니다.
* stagingSplitPercentage:비동기식 업로드를 준비하는 데 사용할 수 있도록 구성된 캐시 크기의 백분율입니다. 기본값은 **10**&#x200B;입니다.
* uploadThreads:비동기 업로드에 사용되는 업로드 스레드 수입니다. 기본값은 **10**&#x200B;입니다.
* stagingPurgeInterval:스테이징 캐시에서 완료된 업로드를 제거하는 간격(초)입니다. 기본값은 **300**&#x200B;초(5분)입니다.
* stagingRetryInterval:실패한 업로드에 대한 재시도 간격(초)입니다. 기본값은 **600**&#x200B;초(10분)입니다.

### 버킷 영역 옵션 {#bucket-region-options}

<table>
 <tbody>
  <tr>
   <td>미국 표준</td>
   <td><code>us-standard</code></td>
  </tr>
  <tr>
   <td>미국 서부</td>
   <td><code>us-west-2</code></td>
  </tr>
  <tr>
   <td>미국 서부(북부 캘리포니아)</td>
   <td><code>us-west-1</code></td>
  </tr>
  <tr>
   <td>EU(아일랜드)<br /> </td>
   <td><code>EU</code></td>
  </tr>
  <tr>
   <td>아시아 태평양(싱가포르)<br /> </td>
   <td><code>ap-southeast-1</code></td>
  </tr>
  <tr>
   <td>아시아 태평양(시드니)<br /> </td>
   <td><code>ap-southeast-2</code></td>
  </tr>
  <tr>
   <td>아시아 태평양(도쿄)</td>
   <td><code>ap-northeast-1</code></td>
  </tr>
  <tr>
   <td>남아메리카(상파울루)<br /> </td>
   <td><code>sa-east-1</code></td>
  </tr>
 </tbody>
</table>

**DataStore 캐싱**

>[!NOTE]
>
>`S3DataStore`, `CachingFileDataStore` 및 `AzureDataStore`의 DataStore 구현은 로컬 파일 시스템 캐싱을 지원합니다. `CachingFileDataStore` 구현은 DataStore가 NFS(네트워크 파일 시스템)에 있을 때 유용합니다.


이전 캐시 구현(Oak 1.6 이전)에서 업그레이드할 때 로컬 파일 시스템 캐시 디렉토리의 구조가 다릅니다. 이전 캐시 구조에서는 다운로드된 파일과 업로드된 파일이 모두 캐시 경로 아래에 바로 배치됩니다. 새 구조는 다운로드 및 업로드를 분리하여 캐시 경로 아래에 `upload` 및 `download`라는 두 개의 디렉토리에 저장합니다. 업그레이드 프로세스는 완벽해야 하며 보류 중인 업로드를 예약해야 하며 캐시에 이전에 다운로드한 파일은 초기화 시 캐시에 저장됩니다.

oak-run의 `datastorecacheupgrade` 명령을 사용하여 캐시를 오프라인으로 업그레이드할 수도 있습니다. 명령 실행 방법에 대한 자세한 내용은 Oak-run 모듈의 [readme](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md)를 확인하십시오.

캐시는 크기 제한이 있으며 cacheSize 매개 변수를 사용하여 구성할 수 있습니다.

**다운로드**

DataStore에서 로컬 캐시가 요청된 파일/blob의 레코드를 확인하기 전에 확인합니다. 캐시에 파일을 추가하는 동안 캐시가 구성된 제한을 초과하는 경우(`cacheSize` 매개 변수 참조) 일부 파일이 공간 재확보를 위해 제거됩니다.

**비동기 업로드**

캐시는 DataStore에 대한 비동기 업로드를 지원합니다. 파일은 로컬에서, 캐시(파일 시스템)에서 스테이징되며 비동기 작업이 파일을 업로드하기 시작합니다. 비동기 업로드 수는 스테이징 캐시의 크기에 따라 제한됩니다. 스테이징 캐시의 크기는 `stagingSplitPercentage` 매개 변수를 사용하여 구성합니다. 이 매개 변수는 스테이징 캐시에 사용할 캐시 크기의 백분율을 정의합니다. 또한 다운로드에 사용할 수 있는 캐시 백분율은 **(100 - `stagingSplitPercentage`) *`cacheSize`**&#x200B;로 계산됩니다.

비동기 업로드는 다중 스레드이며 스레드 수는 `uploadThreads` 매개 변수를 사용하여 구성됩니다.

업로드가 완료된 후 파일이 기본 다운로드 캐시로 이동됩니다. 스테이징 캐시 크기가 한도를 초과하면, 이전 비동기 업로드가 완료되고 스테이징 캐시에서 다시 공간을 사용할 수 있을 때까지 파일은 동기식으로 DataStore에 업로드됩니다. 업로드된 파일은 `stagingPurgeInterval` 매개 변수에 의해 간격이 구성된 주기적 작업에 의해 스테이징 영역에서 제거됩니다.

실패한 업로드(예: 네트워크 중단 때문에)는 다시 시도 대기열에 넣고 정기적으로 다시 시도합니다. 재시도 간격은 `stagingRetryInterval parameter`을 사용하여 구성됩니다.

#### Amazon S3 {#configuring-binaryless-replication-with-amazon-s}을(를) 사용하여 바이너리 없는 복제 구성

S3를 사용하여 바이너리 없는 복제를 구성하려면 다음 단계가 필요합니다.

1. 작성자 및 게시 인스턴스를 설치하고 제대로 시작되었는지 확인합니다.
1. *https://localhost:4502/etc/replication/agents.author/publish.html*&#x200B;에 대한 페이지를 열어 복제 에이전트 설정으로 이동합니다.
1. **설정** 섹션에서 **편집** 단추를 누릅니다.
1. **Serialization** 유형 옵션을 **이진 없음**&#x200B;으로 변경합니다.

1. 전송 URI에 &quot; `binaryless`= `true`&quot; 매개 변수를 추가합니다. 변경 후 uri는 다음과 유사해야 합니다.

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. 모든 작성 및 게시 인스턴스를 다시 시작하여 변경 사항을 적용할 수 있습니다.

#### S3 및 MongoDB {#creating-a-cluster-using-s-and-mongodb}을(를) 사용하여 클러스터 만들기

1. 다음 명령을 사용하여 CQ 빠른 시작을 압축 해제합니다.

   `java -jar cq-quickstart.jar -unpack`

1. AEM의 압축을 해제한 후 설치 디렉터리 *crx-quickstart*/*install*&#x200B;에 폴더를 만듭니다.

1. 다음 두 파일을 `crx-quickstart` 폴더 내에 만듭니다.

   * *org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService*.*config*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*.*config*

   파일을 만든 후 필요에 따라 구성 옵션을 추가합니다.

1. 위에 설명된 대로 S3 데이터 저장소에 필요한 2개의 번들을 설치합니다.
1. MongoDB가 설치되어 있고 `mongod` 인스턴스가 실행 중인지 확인합니다.
1. 다음 명령으로 AEM을 시작합니다.

   `java -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart.jar -r crx3,crx3mongo`

1. 두 번째 AEM 인스턴스에 대해 1-4단계를 반복합니다.
1. 두 번째 AEM 인스턴스를 시작합니다.

#### 공유 데이터 저장소 구성 {#configuring-a-shared-data-store}

1. 먼저 데이터 저장소를 공유하는 데 필요한 각 인스턴스에 대해 데이터 저장소 구성 파일을 만듭니다.

   * `FileDataStore`을(를) 사용하는 경우 `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` 파일을 만들고 `<aem-install>/crx-quickstart/install` 폴더에 배치합니다.

   * S3을 데이터 저장소로 사용하는 경우 위와 같이 `<aem-install>/crx-quickstart/install` 폴더에 `rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config`이라는 파일을 만듭니다.

1. 동일한 데이터 저장소를 가리키도록 각 인스턴스에서 데이터 저장소 구성 파일을 수정합니다. 자세한 내용은 [이 문서](/help/sites-deploying/data-store-config.md#data-store-configurations)를 참조하십시오.
1. 인스턴스가 기존 서버에서 복제된 경우 저장소가 오프라인 상태일 때 최신 Oak 실행 도구를 사용하여 새 인스턴스의 `clusterId`을 제거해야 합니다. 실행해야 하는 명령은 다음과 같습니다.

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >세그먼트 노드 저장소가 구성된 경우 저장소 경로를 지정해야 합니다. 기본적으로 경로는 `<aem-install-folder>/crx-quickstart/repository/segmentstore.`입니다. 문서 노드 저장소가 구성된 경우 [Mongo 연결 문자열 URI](https://docs.mongodb.org/manual/reference/connection-string/)를 사용할 수 있습니다.

   >[!NOTE]
   >
   >Oak 실행 도구는 다음 위치에서 다운로드할 수 있습니다.
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >AEM 설치 시 사용하는 Oak 버전에 따라 다른 버전의 도구를 사용해야 합니다. 도구를 사용하기 전에 아래 버전 요구 사항 목록을 확인하십시오.
   >
   >
   >
   >    * Oak 버전 **1.2.x**&#x200B;의 경우 Oak-run **1.2.12 이상** 사용
   >    * Oak 버전 **이 위의**&#x200B;보다 최신 버전의 경우 AEM 설치의 Oak 코어와 일치하는 Oak-run 버전을 사용합니다.


1. 마지막으로 구성을 확인합니다. 이를 수행하려면 공유 중인 각 저장소에서 데이터 저장소에 추가된 고유한 파일을 찾아야 합니다. 파일의 형식은 `repository-[UUID]`입니다. 여기서 UUID는 각 개별 저장소의 고유 식별자입니다.

   따라서 적절한 구성에는 데이터 저장소를 공유하는 저장소가 있을 만큼 고유한 파일이 있어야 합니다.

   파일은 데이터 저장소에 따라 다르게 저장됩니다.

   * `FileDataStore`의 경우 파일은 데이터 저장소 폴더의 루트 경로 아래에 만들어집니다.
   * `S3DataStore`의 경우 `META` 폴더 아래에 구성된 S3 버킷에 파일이 만들어집니다.

## Azure 데이터 저장소 {#azure-data-store}

AEM을 Microsoft Azure 저장소 서비스에 데이터를 저장하도록 구성할 수 있습니다. 구성에 `org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` PID를 사용합니다.

Azure 데이터 저장소 기능을 사용하려면 Azure 커넥터가 포함된 기능 팩을 다운로드하여 설치해야 합니다. [Adobe 저장소](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/)로 이동하고 1.6.x 버전의 기능 팩(예: com.adobe.granite.oak.azurebconnector-1.6.3.zip)에서 최신 버전을 다운로드합니다.

>[!NOTE]
>
>AEM과 TarMK를 함께 사용하면 이진 파일은 기본적으로 FileDataStore에 저장됩니다. Azure DataStore에서 TarMK를 사용하려면 `crx3tar-nofds` 실행 모드를 사용하여 AEM을 시작해야 합니다. 예:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

다운로드한 후에는 다음과 같이 Azure 커넥터를 설치하고 구성할 수 있습니다.

1. 기능 팩 zip 파일의 내용을 임시 폴더에 추출합니다.

1. 임시 폴더로 이동하여 `jcr_root/libs/system/install`의 내용을 `<aem-install>crx-quickstart/install` 폴더에 복사합니다.
1. AEM이 Tar 또는 MongoDB 저장소에서 작동하도록 이미 구성된 경우 계속하기 전에 `/crx-quickstart/install` 폴더에서 기존 구성 파일을 제거하십시오. 제거해야 하는 파일은 다음과 같습니다.

   MongoMK의 경우:

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   TarMK의 경우:

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 기능 팩이 추출된 임시 위치로 돌아가서 `jcr_root/libs/system/config`의 컨텐츠를 `<aem-install>/crx-quickstart/install` 폴더에 복사합니다.
1. 구성 파일을 편집하고 설정에 필요한 구성 옵션을 추가합니다.
1. AEM을 시작합니다.

다음 옵션을 사용하여 구성 파일을 사용할 수 있습니다.

* azureSas=&quot;&quot;:커넥터 버전 1.6.3에서 SAS(Azure Shared Access Signature) 지원이 추가되었습니다. **구성 파일에 SAS와 저장소 자격 증명이 모두 있으면 SAS에 우선 순위가 있습니다.** SAS에 대한 자세한 내용은  [공식 설명서를 참조하십시오](https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1). &#39;=&#39; 문자가 &#39;\=&#39;처럼 이스케이프되었는지 확인합니다.

* azureBlobEndpoint=&quot;&quot;:Azure Blob 끝점입니다. 예: https://&lt;storage-account>.blob.core.windows.net
* accessKey=&quot;&quot;:저장소 계정 이름입니다. Microsoft Azure 인증 자격 증명에 대한 자세한 내용은 [공식 설명서](https://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account)를 참조하십시오.

* secretKey=&quot;&quot;:저장소 액세스 키. &#39;=&#39; 문자가 &#39;\=&#39;처럼 이스케이프되었는지 확인합니다.
* container=&quot;&quot;:Microsoft Azure Blob 저장소 컨테이너 이름입니다. 컨테이너는 그룹 집합입니다. 자세한 내용은 [공식 설명서](https://msdn.microsoft.com/en-us/library/dd135715.aspx)를 참조하십시오.
* maxConnections=&quot;&quot;:작업당 동시 요청 수입니다. 기본값은 1입니다.
* maxErrorRetry=&quot;&quot;:요청당 재시도 횟수. 기본값은 3입니다.
* socketTimeout=&quot;&quot;:요청에 사용된 시간 초과 간격(밀리초)입니다. 기본값은 5분입니다.

위의 설정 외에 다음 설정도 구성할 수 있습니다.

* 경로:데이터 저장소의 경로입니다. 기본값은 입니다.`<aem-install>/repository/datastore.`
* RecordLength:데이터 저장소에 저장해야 하는 개체의 최소 크기입니다. 기본값은 16KB입니다.
* maxCachedBinarySize:이 크기보다 작거나 같은 바이너리는 메모리 캐시에 저장됩니다. 크기는 바이트 단위입니다. 기본값은 17408(17KB)입니다.
* cacheSize:캐시의 크기입니다. 값이 바이트 단위로 지정됩니다. 기본값은 64GB입니다.
* 비밀:공유 데이터 저장소 설정에 바이너리 없는 복제를 사용하는 경우에만 사용됩니다.
* stagingSplitPercentage:비동기식 업로드를 준비하는 데 사용할 수 있도록 구성된 캐시 크기의 백분율입니다. 기본값은 10입니다.
* uploadThreads:비동기 업로드에 사용되는 업로드 스레드 수입니다. 기본값은 10입니다.
* stagingPurgeInterval:스테이징 캐시에서 완료된 업로드를 제거하는 간격(초)입니다. 기본값은 300초(5분)입니다.
* stagingRetryInterval:실패한 업로드에 대한 재시도 간격(초)입니다. 기본값은 600초(10분)입니다.

>[!NOTE]
>
>모든 설정은 따옴표 사이에 넣어야 합니다. 예를 들면 다음과 같습니다.

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## 데이터 저장소 가비지 컬렉션 {#data-store-garbage-collection}

데이터 저장소 가비지 수집 프로세스는 데이터 저장소에서 사용되지 않는 파일을 제거하는 데 사용되므로 프로세스에서 중요한 디스크 공간을 확보합니다.

다음을 통해 데이터 저장소 가비지 수집을 실행할 수 있습니다.

1. *https://&lt;serveraddress:port>/system/console/jmx*&#x200B;에 있는 JMX 콘솔로 이동
1. **RepositoryManagement 검색 중.** Repository Manager MBean을 찾으면 이 MBean을 클릭하여 사용 가능한 옵션을 표시합니다.
1. 페이지 끝으로 스크롤하고 **startDataStoreGC(boolean markOnly)** 링크를 클릭합니다.
1. 다음 대화 상자에서 `markOnly` 매개 변수에 `false`을 입력한 다음 **호출**&#x200B;을 클릭합니다.

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >`markOnly` 매개 변수는 가비지 수집의 비우기 단계가 실행되는지 여부를 나타냅니다.

## 공유 데이터 저장소에 대한 데이터 저장소 가비지 컬렉션 {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>Mongo 또는 Segment Tar를 사용하여 클러스터형 또는 공유 데이터 저장소 설정에서 가비지 수집을 수행할 때 로그에 특정 Blob ID를 삭제할 수 없다는 경고가 표시될 수 있습니다. 이전 가비지 컬렉션에서 삭제된 blob ID가 ID 삭제에 대한 정보가 없는 다른 클러스터 또는 공유 노드에서 잘못 참조되기 때문에 이러한 오류가 발생합니다. 따라서 가비지 수집이 수행되면 마지막 실행에서 이미 삭제된 ID를 삭제하려고 하면 경고가 기록됩니다. 이 동작은 성능 또는 기능에 영향을 주지 않습니다.

최신 버전의 AEM에서는 둘 이상의 저장소에서 공유하는 데이터 저장소에서 데이터 저장소 가비지 컬렉션을 실행할 수 있습니다. 공유 데이터 저장소에서 데이터 저장소 가비지 컬렉션을 실행하려면 다음 단계를 수행하십시오.

1. 데이터 저장소를 공유하는 모든 저장소 인스턴스에서 데이터 저장소 가비지 수집에 대해 구성된 유지 관리 작업이 비활성화되어 있는지 확인합니다.
1. 데이터 저장소를 공유하는 모든&#x200B;**저장소 인스턴스에 대해 [이진 가비지 컬렉션](/help/sites-deploying/data-store-config.md#data-store-garbage-collection)에 설명된 단계를 개별적으로 실행합니다.** 그러나 [호출] 단추를 클릭하기 전에 `markOnly` 매개 변수에 `true`을 입력해야 합니다.

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. 모든 인스턴스에 대해 위의 절차를 완료한 후 다음 인스턴스의 **임의의**&#x200B;에서 데이터 저장소 가비지 수집을 다시 실행하십시오.

   1. JMX 콘솔로 이동하여 저장소 관리자 메뉴를 선택합니다.
   1. **startDataStoreGC(boolean markOnly)** 링크를 클릭합니다.
   1. 다음 대화 상자에서 `markOnly` 매개 변수에 대해 `false`을 다시 입력합니다.

   이렇게 하면 이전에 사용한 표시 단계를 사용하여 찾은 모든 파일이 수집되고 데이터 저장소에서 사용되지 않은 나머지 파일이 삭제됩니다.

