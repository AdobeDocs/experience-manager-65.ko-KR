---
title: AEM 6.5의 저장소 요소
seo-title: Storage Elements in AEM 6.5
description: AEM 6.5에서 사용할 수 있는 노드 저장소 구현 및 저장소 유지 관리 방법에 대해 알아봅니다.
seo-description: Learn about the node storage implementations available in AEM 6.5 and how to maintain the repository.
uuid: 3b018830-c42e-48e0-9b6f-cd230b02d914
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0aa2c22f-32bb-4e50-8328-63ed73c0f19e
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
exl-id: 52437eb5-f9fb-4945-9950-5a1562fe878d
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 1%

---

# AEM 6.5의 저장소 요소{#storage-elements-in-aem}

이 문서에서는 다음 사항을 다룹니다.

* [AEM 6의 스토리지 개요](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [저장소 유지 관리](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## AEM 6의 스토리지 개요 {#overview-of-storage-in-aem}

AEM 6에서 가장 중요한 변경 사항 중 하나는 저장소 수준의 혁신입니다.

현재 AEM6에서 사용할 수 있는 노드 스토리지 구현은 Tar 스토리지와 MongoDB 스토리지라는 두 가지가 있습니다.

### Tar 스토리지 {#tar-storage}

#### Tar 저장소를 사용하여 새로 설치된 AEM 인스턴스 실행 {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>세그먼트 노드 저장소의 PID가 org.apache.jackrabbit.oak에서 변경되었습니다.**plugins**&#x200B;이전 버전의 AEM 6에서 AEM 6.3의 org.apache.jackrabbit.oak.segment.SegmentNodeStoreService로 .segment.SegmentNodeStoreService. 변경 사항이 반영되도록 필요한 구성을 조정해야 합니다.

기본적으로 AEM 6은 기본 구성 옵션을 사용하여 Tar 저장소를 사용하여 노드 및 바이너리를 저장합니다. 다음을 수행하여 저장소 설정을 수동으로 구성할 수 있습니다.

1. AEM 6 quickstart jar를 다운로드하여 새 폴더에 저장합니다.
1. 다음을 실행하여 AEM 압축을 풉니다.

   `java -jar cq-quickstart-6.jar -unpack`

1. 다음 이름의 폴더 만들기 `crx-quickstart\install` 를 입력합니다.

1. 라는 파일 만들기 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` 을(를) 새로 만든 폴더에 추가합니다.

1. 파일을 편집하고 구성 옵션을 설정합니다. AEM Tar 저장소 구현의 기반이 되는 세그먼트 노드 저장소에 대해 다음 옵션을 사용할 수 있습니다.

   * `repository.home`: 다양한 저장소 관련 데이터가 저장되는 저장소 홈의 경로입니다. 기본적으로 세그먼트 파일은 crx-quickstart/segmentstore 디렉토리 아래에 저장됩니다.
   * `tarmk.size`: 세그먼트의 최대 크기(MB) 기본값은 256MB입니다.

1. AEM을 시작합니다.

### Mongo 스토리지 {#mongo-storage}

#### Mongo Storage로 새로 설치된 AEM 인스턴스 실행 {#running-a-freshly-installed-aem-instance-with-mongo-storage}

AEM 6은 다음 절차에 따라 MongoDB 스토리지로 실행되도록 구성할 수 있습니다.

1. AEM 6 quickstart jar를 다운로드하여 새 폴더에 저장합니다.
1. 다음 명령을 실행하여 AEM 압축을 해제합니다.

   `java -jar cq-quickstart-6.jar -unpack`

1. MongoDB가 설치되어 있고 의 인스턴스가 `mongod` 이(가) 실행 중입니다. 자세한 내용은 [MongoDB 설치 중](https://docs.mongodb.org/manual/installation/).
1. 다음 이름의 폴더 만들기 `crx-quickstart\install` 를 입력합니다.
1. 에서 사용할 구성의 이름으로 구성 파일을 만들어 노드 저장소를 구성합니다. `crx-quickstart\install` 디렉토리.

   AEM MongoDB 스토리지 구현의 기반이 되는 문서 노드 저장소는 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. 파일을 편집하고 구성 옵션을 설정합니다. 다음 옵션을 사용할 수 있습니다.

   * `mongouri`: [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) mongo 데이터베이스에 연결하는 데 필요합니다. 기본값은 입니다 `mongodb://localhost:27017`
   * `db`: Mongo 데이터베이스의 이름입니다. 기본적으로 새 AEM 6 설치는 **aem-author** 를 데이터베이스 이름으로 사용하십시오.
   * `cache`: 캐시 크기(메가바이트) 이 캐시 크기는 DocumentNodeStore에서 사용되는 다양한 캐시에 분산됩니다. 기본값은 256입니다.
   * `changesSize`: 비교 출력을 캐시하기 위해 Mongo에서 사용되는 캡핑된 컬렉션의 크기(MB)입니다. 기본값은 256입니다.
   * `customBlobStore`: 사용자 지정 데이터 저장소가 사용됨을 나타내는 부울 값입니다. 기본값은 false입니다.

1. 사용할 데이터 저장소의 PID로 구성 파일을 만들고 해당 파일을 편집하여 구성 옵션을 설정합니다. 자세한 내용은 [노드 저장소 및 데이터 저장소 구성](/help/sites-deploying/data-store-config.md).

1. 다음을 실행하여 MongoDB 스토리지 백엔드로 AEM 6 jar를 시작합니다.

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   백엔드 실행 모드가 다음과 같은 경우 **`-r`**, 예제는 MongoDB 지원으로 시작됩니다.

#### 투명한 대용량 페이지 비활성화 {#disabling-transparent-huge-pages}

Red Hat® Linux®는 THP(Transparent Huge Pages)라는 메모리 관리 알고리즘을 사용합니다. AEM은 세분화된 읽기 및 쓰기를 수행하지만 THP는 대규모 작업에 최적화되어 있습니다. 따라서 Tar 및 Mongo 스토리지에서 THP를 모두 비활성화하는 것이 좋습니다. 알고리즘을 비활성화하려면 다음 단계를 따르십시오.

1. 를 엽니다. `/etc/grub.conf` 원하는 텍스트 편집기의 파일입니다.
1. 다음 줄을 추가합니다. **grub.conf** 파일:

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
>다음 리소스를 참조하십시오.
>
>* Red Hat® Linux®의 Transparent Huge Pages에 대한 자세한 내용은 다음을 참조하십시오 [기사](https://access.redhat.com/solutions/46111).
* Linux® 조정 팁은 다음을 참조하십시오 [기사](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=ko-KR).
>

## 저장소 유지 관리 {#maintaining-the-repository}

저장소에 대한 각 업데이트는 콘텐츠 개정을 만듭니다. 결과적으로 각 업데이트 시 저장소의 크기가 커집니다. 저장소 증가를 제어하지 않으려면 디스크 리소스를 확보하기 위해 이전 버전을 정리해야 합니다. 이 유지 관리 기능을 개정 정리 라고 합니다. 개정 정리 메커니즘은 저장소에서 오래된 데이터를 제거하여 디스크 공간을 확보합니다. 개정 정리에 대한 자세한 내용은 [개정 정리 페이지](/help/sites-deploying/revision-cleanup.md).
