---
title: AEM 6.5의 스토리지 요소
seo-title: AEM 6.5의 스토리지 요소
description: AEM 6.5에서 사용 가능한 노드 스토리지 구현과 저장소 유지 관리 방법에 대해 알아봅니다.
seo-description: AEM 6.5에서 사용 가능한 노드 스토리지 구현과 저장소 유지 관리 방법에 대해 알아봅니다.
uuid: 3b018830-c42e-48e0-9b6f-cd230b02d914
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0aa2c22f-32bb-4e50-8328-63ed73c0f19e
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 1%

---


# AEM 6.5의 스토리지 요소{#storage-elements-in-aem}

이 문서에서는 다음을 다룹니다.

* [AEM 6의 스토리지 개요](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [저장소 유지 관리](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## AEM 6 {#overview-of-storage-in-aem}의 스토리지 개요

AEM 6의 가장 중요한 변화 중 하나는 저장소 수준의 혁신적인 기능입니다.

현재 AEM6에서는 두 개의 노드 스토리지 구현을 사용할 수 있습니다.Tar 저장소 및 MongoDB 저장소.

### Tar 저장소 {#tar-storage}

#### 새로 설치된 AEM 인스턴스 실행 중(Tar Storage {#running-a-freshly-installed-aem-instance-with-tar-storage})

>[!CAUTION]
>
>세그먼트 노드 저장소에 대한 PID가 org.apache.jackrabbit.oak에서 변경되었습니다.**plugins**.segment.SegmentNodeStoreService(AEM 6.3의 이전 버전 AEM 6 - org.apache.jackrabbit.oak.segment.SegmentNodeStoreService). 이 변경 사항을 반영하도록 필요한 구성을 조정하십시오.

기본적으로 AEM 6은 기본 구성 옵션을 사용하여 Tar 스토리지를 사용하여 노드와 바이너리를 저장합니다. 저장소 설정을 수동으로 구성하려면 아래 절차를 따르십시오.

1. AEM 6 빠른 시작 jar를 다운로드하여 새 폴더에 배치합니다.
1. 다음을 실행하여 AEM의 압축을 해제합니다.

   `java -jar cq-quickstart-6.jar -unpack`

1. 설치 디렉토리에 `crx-quickstart\install`이라는 폴더를 만듭니다.

1. 새로 만든 폴더에 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`이라는 파일을 만듭니다.

1. 파일을 편집하고 구성 옵션을 설정합니다. AEM Tar 스토리지 구현의 기초가 되는 세그먼트 노드 저장소에 대해 다음 옵션을 사용할 수 있습니다.

   * `repository.home`:다양한 저장소 관련 데이터가 저장되는 저장소 홈의 경로입니다. 기본적으로 세그먼트 파일은 crx-quickstart/segmentstore 디렉토리 아래에 저장됩니다.
   * `tarmk.size`:세그먼트의 최대 크기(MB)입니다. 기본값은 256MB입니다.

1. AEM 시작

### Mongo 저장소 {#mongo-storage}

#### Mongo Storage {#running-a-freshly-installed-aem-instance-with-mongo-storage}이(가) 있는 새로 설치된 AEM 인스턴스 실행

AEM 6은 아래 절차에 따라 MongoDB 스토리지와 함께 실행되도록 구성할 수 있습니다.

1. AEM 6 빠른 시작 jar를 다운로드하여 새 폴더에 넣습니다.
1. 다음 명령을 실행하여 AEM의 압축을 해제합니다.

   `java -jar cq-quickstart-6.jar -unpack`

1. MongoDB가 설치되어 있고 `mongod` 인스턴스가 실행 중인지 확인하십시오. 자세한 내용은 [Installing MongoDB](https://docs.mongodb.org/manual/installation/)를 참조하십시오.
1. 설치 디렉토리에 `crx-quickstart\install`이라는 폴더를 만듭니다.
1. `crx-quickstart\install` 디렉토리에서 사용할 구성 파일의 이름을 사용하여 노드 저장소를 구성합니다.

   AEM MongoDB 저장소 구현의 기반인 문서 노드 저장소에서는 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. 파일을 편집하고 구성 옵션을 설정합니다. 다음 옵션을 사용할 수 있습니다.

   * `mongouri`:Mongo  [](https://docs.mongodb.org/manual/reference/connection-string/) 데이터베이스에 연결하는 데 필요한 MongoURI입니다. 기본값은 입니다.`mongodb://localhost:27017`
   * `db`:Mongo 데이터베이스의 이름입니다. 기본적으로 새 AEM 6 설치에서는 데이터베이스 이름으로 **aem-author**&#x200B;를 사용합니다.
   * `cache`:캐시 크기(MB)입니다. DocumentNodeStore에서 사용되는 다양한 캐시 간에 배포됩니다. 기본값은 256입니다.
   * `changesSize`:비교 출력을 캐싱하는 데 Mongo에 사용된 제한적 컬렉션의 크기(MB)입니다. 기본값은 256입니다.
   * `customBlobStore`:사용자 지정 데이터 저장소가 사용됨을 나타내는 부울 값입니다. 기본값은 false입니다.

1. 사용할 데이터 저장소의 PID를 사용하여 구성 파일을 만들고 구성 옵션을 설정하기 위해 파일을 편집합니다. 자세한 내용은 [노드 저장소 및 데이터 저장소 구성](/help/sites-deploying/data-store-config.md)을 참조하십시오.

1. 다음을 실행하여 MongoDB 스토리지 백엔드로 AEM 6 jar를 시작합니다.

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   여기서 **`-r`**&#x200B;은 백엔드 실행 모드입니다. 이 예에서는 MongoDB 지원으로 시작됩니다.

#### 투명한 큰 페이지 {#disabling-transparent-huge-pages} 비활성화

Red Hat Linux는 THP(Transparent Huge Pages)라는 메모리 관리 알고리즘을 사용합니다. AEM에서 세밀하게 읽기 및 쓰기를 수행하는 동안 THP는 대규모 작업에 최적화되어 있습니다. 따라서 Tar 및 Mongo 저장소에서 THP를 모두 비활성화하는 것이 좋습니다. 알고리즘을 비활성화하려면 다음 단계를 수행합니다.

1. 원하는 텍스트 편집기에서 `/etc/grub.conf` 파일을 엽니다.
1. **grub.conf** 파일에 다음 줄을 추가합니다.

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
>* Red Hat Linux의 투명한 대형 페이지에 대한 자세한 내용은 이 [아티클](https://access.redhat.com/solutions/46111)을 참조하십시오.
>* Linux 튜닝 팁은 이 [아티클](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)을 참조하십시오.

>



## 저장소 {#maintaining-the-repository} 유지 관리

저장소의 각 업데이트는 새 컨텐츠 개정을 만듭니다. 따라서 각 업데이트를 통해 저장소의 크기가 증가합니다. 저장소 증가를 제어하지 않으려면 기존 수정 내용을 무료 디스크 리소스로 정리해야 합니다. 이 유지 관리 기능을 수정 기능이라고 합니다. 수정 정리 메커니즘은 저장소에서 오래된 데이터를 제거하여 디스크 공간을 다시 확보합니다. 개정 정리에 대한 자세한 내용은 [개정 정리 페이지](/help/sites-deploying/revision-cleanup.md)를 참조하십시오.
