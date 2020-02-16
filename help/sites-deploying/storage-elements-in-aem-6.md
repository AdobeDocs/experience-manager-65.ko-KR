---
title: AEM 6.5의 스토리지 요소
seo-title: AEM 6.5의 스토리지 요소
description: AEM 6.5에서 사용할 수 있는 노드 스토리지 구현과 저장소 유지 관리 방법에 대해 알아봅니다.
seo-description: AEM 6.5에서 사용할 수 있는 노드 스토리지 구현과 저장소 유지 관리 방법에 대해 알아봅니다.
uuid: 3b018830-c42e-48e0-9b6f-cd230b02d914
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0aa2c22f-32bb-4e50-8328-63ed73c0f19e
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# AEM 6.5의 스토리지 요소{#storage-elements-in-aem}

이 문서에서는 다음을 다룹니다.

* [AEM 6의 스토리지 개요](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [저장소 유지 관리](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## AEM 6의 스토리지 개요 {#overview-of-storage-in-aem}

AEM 6에서 가장 중요한 변경 사항 중 하나는 저장소 수준의 혁신적인 기능입니다.

현재 AEM6에서 사용할 수 있는 노드 스토리지 구현은 두 가지가 있습니다.Tar 스토리지 및 MongoDB 스토리지.

### Tar 스토리지 {#tar-storage}

#### Tar 저장소에서 새로 설치된 AEM 인스턴스 실행 {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>세그먼트 노드 저장소에 대한 PID가 org.apache.jackrabbit.oak에서 변경되었습니다.**plugins**.segment.SegmentNodeStoreService의 이전 버전에서 AEM 6.3의 org.apache.jackrabbit.oak.segment.SegmentNodeStoreService입니다.이 변경 사항을 반영하려면 필요한 구성을 조정해야 합니다.

기본적으로 AEM 6에서는 기본 구성 옵션을 사용하여 Tar 저장소를 사용하여 노드와 바이너리를 저장합니다. 저장소 설정을 수동으로 구성하려면 아래 절차를 따르십시오.

1. AEM 6 빠른 시작 jar를 다운로드하여 새 폴더에 배치합니다.
1. 다음을 실행하여 AEM의 압축을 해제합니다.

   `java -jar cq-quickstart-6.jar -unpack`

1. 설치 디렉토리에 이름이 지정된 폴더를 `crx-quickstart\install` 만듭니다.

1. 새로 만든 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` 폴더에서 호출된 파일을 만듭니다.

1. 파일을 편집하고 구성 옵션을 설정합니다. AEM의 Tar 스토리지 구현을 기반으로 하는 세그먼트 노드 저장소에 대해 다음 옵션을 사용할 수 있습니다.

   * `repository.home`:다양한 저장소 관련 데이터가 저장되는 저장소 홈의 경로입니다. 기본적으로 세그먼트 파일은 crx-quickstart/segmentstore 디렉토리 아래에 저장됩니다.
   * `tarmk.size`:세그먼트의 최대 크기(MB)입니다. 기본값은 256MB입니다.

1. AEM을 시작합니다.

### Mongo Storage {#mongo-storage}

#### Mongo Storage에서 새로 설치된 AEM 인스턴스 실행 {#running-a-freshly-installed-aem-instance-with-mongo-storage}

아래 절차에 따라 MongoDB 스토리지와 함께 실행되도록 AEM 6을 구성할 수 있습니다.

1. AEM 6 빠른 시작 jar를 다운로드하여 새 폴더에 배치합니다.
1. 다음 명령을 실행하여 AEM의 압축을 해제합니다.

   `java -jar cq-quickstart-6.jar -unpack`

1. MongoDB가 설치되어 있고 인스턴스가 실행 `mongod` 중인지 확인하십시오. 자세한 내용은 MongoDB [설치를 참조하십시오](https://docs.mongodb.org/manual/installation/).
1. 설치 디렉토리에 이름이 지정된 폴더를 `crx-quickstart\install` 만듭니다.
1. 디렉토리에 사용할 구성 파일의 이름을 사용하여 `crx-quickstart\install` 노드 저장소를 구성합니다.

   문서 노드 저장소(AEM의 MongoDB 스토리지 구현을 기반으로 함)는 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. 파일을 편집하고 구성 옵션을 설정합니다. 다음 옵션을 사용할 수 있습니다.

   * `mongouri`:Mongo [데이터베이스에](https://docs.mongodb.org/manual/reference/connection-string/) 연결하는 데 필요한 MongoURI입니다. 기본값은 입니다.`mongodb://localhost:27017`
   * `db`:Mongo 데이터베이스의 이름입니다. 기본적으로 새 AEM 6 설치에서는 **aem-author** 를 데이터베이스 이름으로 사용합니다.
   * `cache`:캐시 크기(MB)입니다. DocumentNodeStore에서 사용되는 다양한 캐시 간에 배포됩니다. 기본값은 256입니다.
   * `changesSize`:비교 출력을 캐싱하는 데 Mongo에 사용된 제한적 컬렉션 크기(MB)입니다. 기본값은 256입니다.
   * `customBlobStore`:사용자 지정 데이터 저장소가 사용됨을 나타내는 부울 값입니다. 기본값은 false입니다.

1. 사용할 데이터 저장소의 PID를 사용하여 구성 파일을 만들고 구성 옵션을 설정하기 위해 파일을 편집합니다. 자세한 내용은 노드 저장소 및 [데이터 저장소 구성을 참조하십시오](/help/sites-deploying/data-store-config.md).

1. 다음을 실행하여 MongoDB 스토리지 백엔드로 AEM 6 jar 시작:

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   백엔드 런타임 **`-r`** 모드는 어디입니까? 이 예제에서는 MongoDB 지원으로 시작합니다.

#### 투명한 큰 페이지 비활성화 {#disabling-transparent-huge-pages}

Red Hat Linux는 THP(Transparent Huge Pages)라는 메모리 관리 알고리즘을 사용합니다. AEM 파섹 따라서 Tar 및 Mongo 저장소에서 THP를 모두 비활성화하는 것이 좋습니다. 알고리즘을 비활성화하려면 다음 단계를 수행합니다.

1. 원하는 텍스트 편집기에서 파일을 엽니다 `/etc/grub.conf` .
1. grub.conf 파일에 다음 줄을 **추가합니다** .

   ```
   transparent_hugepage=never
   ```

1. 마지막으로 다음을 실행하여 설정이 적용되었는지 확인합니다.

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   THP가 비활성화된 경우 위 명령의 출력은 다음과 같아야 합니다.

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>또한 다음 리소스를 참조할 수도 있습니다.
>
>* Red Hat Linux의 투명한 대형 페이지에 대한 자세한 내용은 이 [문서를](https://access.redhat.com/solutions/46111)참조하십시오.
>* Linux 조정 팁은 이 [문서를](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)참조하십시오.
>



## 저장소 유지 관리 {#maintaining-the-repository}

저장소에 대한 각 업데이트는 새 컨텐츠 개정을 만듭니다. 따라서 각 업데이트를 통해 저장소의 크기가 증가합니다. 제어되지 않는 저장소 증가를 방지하려면 디스크 리소스를 무료로 사용할 수 있도록 이전 버전을 정리해야 합니다. 이 유지 관리 기능을 개정 청소라고 합니다. 수정 정리 메커니즘은 저장소에서 오래된 데이터를 제거하여 디스크 공간을 확보합니다. 개정 정리에 대한 자세한 내용은 수정 [페이지를](/help/sites-deploying/revision-cleanup.md)참조하십시오.
