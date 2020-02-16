---
title: 데이터 저장소 가비지 컬렉션
seo-title: 데이터 저장소 가비지 컬렉션
description: 디스크 공간을 확보하도록 데이터 저장소 가비지 컬렉션을 구성하는 방법에 대해 알아봅니다.
seo-description: 디스크 공간을 확보하도록 데이터 저장소 가비지 컬렉션을 구성하는 방법에 대해 알아봅니다.
uuid: 49488a81-986a-4d1a-96c8-aeb6595fc094
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5b1e46c5-7e56-433e-b62e-2a76ea7be0fd
docset: aem65
translation-type: tm+mt
source-git-commit: 0eda6ee61acf737abc91d1e5df731e719663b3f2

---


# 데이터 저장소 가비지 컬렉션 {#data-store-garbage-collection}

기존 WCM 자산이 제거되면 기본 데이터 저장소 레코드에 대한 참조가 노드 계층에서 제거될 수 있지만 데이터 저장소 레코드 자체는 유지됩니다. 이렇게 참조되지 않은 데이터 저장소 레코드는 유지되지 않는 &quot;가비지&quot;가 됩니다. 많은 가비지 에셋이 존재하는 경우 이러한 에셋을 제거하여 공간을 유지하고 백업 및 파일 시스템 유지 관리 성능을 최적화하는 것이 좋습니다.

대부분의 경우 WCM 애플리케이션은 정보를 수집하는 경향이 있지만 정보를 거의 자주 삭제하지 않습니다. 새 이미지가 추가되더라도 이전 버전을 대체하더라도 버전 제어 시스템은 여전히 이전 이미지를 유지하고 필요한 경우 다시 되돌리기를 지원합니다. 따라서 시스템에 추가한다고 생각하는 컨텐츠의 대부분은 사실상 영구적으로 저장됩니다. 그래서 우리가 정리하기를 원하는 보관소의 &quot;쓰레기&quot;의 일반적인 원천은 무엇일까요?

AEM 파섹

* 빌드 및 다운로드한 패키지
* 게시 복제를 위해 생성된 임시 파일
* 워크플로우 페이로드
* DAM 렌더링 중 일시적으로 만든 에셋

이러한 임시 개체가 데이터 저장소에 저장할 수 있을 만큼 충분히 큰 경우, 개체가 결국 사용되지 않으면 데이터 저장소 레코드 자체가 &quot;가비지&quot;로 유지됩니다. 일반적인 WCM 작성/게시 애플리케이션에서 이러한 유형의 가장 큰 가비지 소스는 일반적으로 게시 활성화 프로세스입니다. 데이터가 게시로 복제될 때, &quot;Durbo&quot;라는 효율적인 데이터 형식으로 컬렉션에 처음 수집되어 다음 보관소에 저장된 경우에 `/var/replication/data`발생합니다. 데이터 번들은 데이터 저장소의 중요한 크기 임계값보다 큰 경우가 많으므로 데이터 저장소 레코드로 저장됩니다. 복제가 완료되면 의 노드가 `/var/replication/data` 삭제되지만 데이터 저장소 레코드는 &quot;가비지&quot;로 유지됩니다.

복구할 수 있는 쓰레기의 또 다른 소스는 패키지입니다. 다른 모든 것과 마찬가지로 패키지 데이터는 저장소에 저장되므로 4KB보다 큰 패키지의 경우 데이터 저장소에 저장됩니다. 개발 프로젝트 또는 시스템 유지 과정에서 패키지를 여러 번 빌드하고 다시 빌드할 수 있으며, 각 빌드는 이전 빌드의 레코드를 결정하면서 새로운 데이터 저장소 레코드를 생성할 수 있습니다.

## 데이터 저장소 가비지 수집은 어떻게 작동합니까? {#how-does-data-store-garbage-collection-work}

저장소가 외부 데이터 저장소를 사용하여 구성된 경우 [데이터 저장소 가비지 수집은 주별 유지 관리 창의 일부로 자동으로](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) 실행됩니다. 시스템 관리자는 필요에 따라 데이터 저장소 가비지 수집을 수동으로 [](#running-data-store-garbage-collection) 실행할 수도 있습니다. 일반적으로 데이터 저장소 가비지 수집은 정기적으로 수행하는 것이 좋지만, 데이터 저장소 가비지 컬렉션 계획 시 다음 요인을 고려하는 것이 좋습니다.

* 데이터 저장소 가비지 컬렉션은 시간이 걸리고 성능에 영향을 줄 수 있으므로 이에 따라 계획해야 합니다.
* 데이터 저장소 가비지 레코드를 제거해도 정상적인 성능에 영향을 주지 않으므로 성능 최적화는 아닙니다.
* 스토리지 사용률 및 백업 시간과 같은 관련 요소가 중요하지 않은 경우 데이터 저장소 가비지 수집이 안전하게 지연될 수 있습니다.

데이터 저장소 가비지 수집기는 먼저 프로세스가 시작될 때 현재 타임스탬프를 기록합니다. 그런 다음 다중 패스 표시/쓸기 패턴 알고리즘을 사용하여 컬렉션이 수행됩니다.

첫 번째 단계에서는 데이터 저장소 가비지 수집기가 모든 저장소 컨텐츠에 대한 포괄적인 추적을 수행합니다. 데이터 저장소 레코드에 대한 참조가 있는 각 컨텐츠 객체에 대해 파일 시스템의 파일을 찾아 &quot;마지막 수정&quot; 또는 MTIME 속성을 수정하여 메타데이터 업데이트를 수행합니다. 이 시점에서 이 단계에서 액세스하는 파일은 초기 기준 타임스탬프보다 최신 상태가 됩니다.

두 번째 단계에서는 데이터 저장소 가비지 수집기가 데이터 저장소의 물리적 디렉토리 구조를 &quot;찾기&quot;와 거의 같은 방식으로 추적합니다. 파일의 &quot;마지막 수정&quot; 또는 MTIME 속성을 검사하여 다음 사항을 결정합니다.

* MTIME이 초기 기준선 타임스탬프보다 최신 상태인 경우, 파일이 첫 번째 단계에서 검색되었거나, 수집 프로세스가 진행되는 동안 저장소에 추가된 완전히 새로운 파일입니다. 이러한 경우 레코드가 활성화되고 파일이 삭제되지 않습니다.
* MTIME이 초기 기준 타임스탬프 앞에 있으면 파일이 활성 참조 파일이 아니며 제거 가능한 가비지로 간주됩니다.

이 방법은 개인 데이터 저장소가 있는 단일 노드에 대해 잘 작동합니다. 그러나 데이터 저장소가 공유될 수 있으며, 이 경우 다른 저장소의 데이터 저장소 레코드에 대한 활성 라이브 참조가 선택되지 않고 활성 참조된 파일이 실수로 제거될 수 있습니다. 시스템 관리자는 가비지 컬렉션을 계획하기 전에 데이터 저장소의 공유 특성을 이해하고 데이터 저장소가 공유되지 않는 것으로 알려진 경우 간단한 기본 제공 데이터 저장소 가비지 수집 프로세스만 사용해야 합니다.

>[!NOTE]
>
>Mongo 또는 Segment Tar를 사용하여 클러스터형 또는 공유 데이터 저장소 설정에서 가비지 수집을 수행할 때 로그에 특정 blob ID를 삭제할 수 없다는 경고가 표시될 수 있습니다. 이전 가비지 컬렉션에서 삭제된 Blob ID가 ID 삭제에 대한 정보가 없는 다른 클러스터 또는 공유 노드에서 다시 잘못 참조되기 때문입니다. 따라서 가비지 컬렉션이 수행되면 마지막 실행에서 이미 삭제된 ID를 삭제하려고 하면 경고가 기록됩니다. 이 동작은 성능 또는 기능에 영향을 주지 않습니다.

## Running Data Store Garbage Collection {#running-data-store-garbage-collection}

AEM이 실행 중인 데이터 저장소 설정에 따라 데이터 저장소 가비지 수집을 실행하는 방법에는 세 가지가 있습니다.

1. Via [Revision Cleanup](/help/sites-deploying/revision-cleanup.md) - 일반적으로 노드 저장소 정리에 사용되는 가비지 수집 메커니즘입니다.

1. Via [Data Store](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-operations-dashboard) Garbage Collection - 작업 대시보드에서 사용할 수 있는 외부 데이터 저장소에 대한 가비지 수집 메커니즘입니다.
1. JMX [콘솔을 통해](/help/sites-administering/jmx-console.md).

TarMK가 노드 저장소와 데이터 저장소와 함께 사용되는 경우, 노드 저장소와 데이터 저장소의 가비지 수집에는 수정 사항을 사용할 수 있습니다. 그러나 파일 시스템 데이터 저장소와 같이 외부 데이터 저장소가 구성된 경우 데이터 저장소 가비지 수집은 수정 내용과는 별도로 명시적으로 트리거되어야 합니다. 데이터 저장소 가비지 컬렉션은 작업 대시보드 또는 JMX 콘솔을 통해 트리거할 수 있습니다.

아래 표는 AEM 6에서 지원되는 모든 데이터 저장소 배포에 사용해야 하는 데이터 저장소 가비지 수집 유형을 보여줍니다.

<table>
 <tbody>
  <tr>
   <td><strong>노드 저장소</strong><br /> </td>
   <td><strong>데이터 저장소</strong></td>
   <td><strong>가비지 수집 메커니즘</strong><br /> </td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>TarMK</td>
   <td>수정(바이너리는 세그먼트 저장소와 함께 인라인)</td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>외부 파일 시스템</td>
   <td><p>작업 대시보드를 통한 데이터 저장소 가비지 수집 작업</p> <p>JMX 콘솔</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>MongoDB</td>
   <td><p>작업 대시보드를 통한 데이터 저장소 가비지 수집 작업</p> <p>JMX 콘솔</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>외부 파일 시스템</td>
   <td><p>작업 대시보드를 통한 데이터 저장소 가비지 수집 작업</p> <p>JMX 콘솔</p> </td>
  </tr>
 </tbody>
</table>

### 작업 대시보드를 통해 데이터 저장소 가비지 수집 실행 {#running-data-store-garbage-collection-via-the-operations-dashboard}

작업 대시보드를 통해 사용할 수 있는 기본 제공 [유지 관리](/help/sites-administering/operations-dashboard.md)창에는 일요일 오전 1시에 데이터 저장소 가비지 수집을 트리거하는 기본 제공 작업이 포함되어 있습니다.

이 시간 외에 데이터 저장소 가비지 수집을 실행해야 하는 경우 작업 대시보드를 통해 수동으로 트리거할 수 있습니다.

데이터 저장소 가비지 수집을 실행하기 전에 해당 시간에 실행 중인 백업이 없는지 확인해야 합니다.

1. 작업 대시보드를 엽니다. **-> 도구** -> **작업** **** -> **유지**&#x200B;관리작업을수행할수있습니다.
1. 주별 유지 관리 **창을 클릭하거나 탭합니다**.

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. 데이터 **저장소 가비지 수집** 작업을 선택한 다음 실행 **아이콘을 클릭하거나 탭합니다** .

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 데이터 저장소 가비지 수집이 실행되고 대시보드에 해당 상태가 표시됩니다.

   ![chlimage_1-66](assets/chlimage_1-66.png)

>[!NOTE]
>
>데이터 저장소 가비지 수집 작업은 외부 파일 데이터 저장소를 구성한 경우에만 표시됩니다. 파일 [데이터 저장소를 설정하는 방법에 대한 자세한 내용은 AEM 6의](/help/sites-deploying/data-store-config.md#file-data-store) 노드 저장소 및 데이터 저장소 구성을 참조하십시오.

### JMX 콘솔을 통해 데이터 저장소 가비지 수집 실행 {#running-data-store-garbage-collection-via-the-jmx-console}

이 섹션에서는 JMX 콘솔을 통해 데이터 저장소 가비지 수집을 수동으로 실행하는 방법에 대해 설명합니다. 외부 데이터 저장소 없이 설치가 설정된 경우 설치에 적용되지 않습니다. 대신 저장소 유지 관리에서 개정 정리를 실행하는 방법에 대한 [지침을 참조하십시오](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).

>[!NOTE]
>
>외부 데이터 저장소를 사용하여 TarMK를 실행하는 경우 가비지 수집이 유효하려면 먼저 개정 정리를 실행해야 합니다.

가비지 수집을 실행하려면:

1. Apache Felix OSGi Management Console에서 Main **탭을** 선택하고 **다음** 메뉴에서 JMX를선택합니다.
1. 그런 다음 저장소 관리자 MBean **을** 검색하고 클릭합니다(또는 로 `https://<host>:<port>/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Drepository+manager%2Ctype%3DRepositoryManagement`).
1. startDataStoreGC( **boolean markOnly)를 클릭합니다**.
1. 필요한 경우`true`매개 변수에 대해 &quot; `markOnly` &quot;를 입력합니다.

   | **Option** | **설명** |
   |---|---|
   | boolean markOnly | 참조의 표시만 표시하고 표시 및 쓸어 내주지 않도록 true로 설정합니다. 이 모드는 기본 BlobStore가 여러 다른 저장소 간에 공유될 때 사용됩니다. 다른 모든 경우 전체 가비지 수집을 수행하려면 false로 설정합니다. |

1. [호출] **을 클릭합니다**. CRX 파섹

>[!NOTE]
>
>데이터 저장소 가비지 컬렉션은 지난 24시간 동안 삭제된 파일을 수집하지 않습니다.

>[!NOTE]
>
>데이터 저장소 가비지 수집 작업은 외부 파일 데이터 저장소를 구성한 경우에만 시작됩니다. 외부 파일 데이터 저장소가 구성되지 않은 경우 호출한 `Cannot perform operation: no service of type BlobGCMBean found` 후 작업이 메시지를 반환합니다. 파일 [데이터 저장소를 설정하는 방법에 대한 자세한 내용은 AEM 6의](/help/sites-deploying/data-store-config.md#file-data-store) 노드 저장소 및 데이터 저장소 구성을 참조하십시오.

## Automating Data Store Garbage Collection {#automating-data-store-garbage-collection}

가능한 경우, 예를 들어 아침에 시스템에 로드가 거의 없을 때 데이터 저장소 가비지 수집을 실행해야 합니다.

작업 대시보드를 통해 사용할 수 있는 기본 제공 [유지 관리](/help/sites-administering/operations-dashboard.md)창에는 일요일 오전 1시에 데이터 저장소 가비지 수집을 트리거하는 기본 제공 작업이 포함되어 있습니다. 또한 현재 실행 중인 백업이 없는지 확인해야 합니다. 필요한 경우 대시보드를 통해 유지 관리 창의 시작을 사용자 지정할 수 있습니다.

>[!NOTE]
>
>동시에 실행하지 않는 이유는 이전(및 사용되지 않음) 데이터 저장소 파일도 백업되므로 이전 개정으로 롤백해야 하는 경우 바이너리는 여전히 백업에 있습니다.

작업 대시보드의 주별 유지 관리 창에서 데이터 저장소 가비지 수집을 실행하지 않으려면 wget 또는 curl HTTP 클라이언트를 사용하여 자동화할 수도 있습니다. 다음은 curl을 사용하여 백업을 자동화하는 방법의 예입니다.

>[!CAUTION]
>
>다음 예에서는 `curl` 인스턴스에 대해 다양한 매개 변수를 구성해야 할 수 있습니다.예를 들어, 실제 데이터 저장소 가비지 수집에 대한 호스트 이름( `localhost`), 포트( `4502`), 관리 암호( `xyz`) 및 다양한 매개 변수가 있습니다.

다음은 명령줄을 통해 데이터 저장소 가비지 수집을 호출하는 curl 명령의 예입니다.

```shell
curl -u admin:admin -X POST --data markOnly=true  https://localhost:4503/system/console/jmx/org.apache.jackrabbit.oak"%"3Aname"%"3Drepository+manager"%"2Ctype"%"3DRepositoryManagement/op/startDataStoreGC/boolean
```

curl 명령은 즉시 반환됩니다.

## 데이터 저장소 일관성 확인 {#checking-data-store-consistency}

데이터 저장소 일관성 검사는 누락되었지만 여전히 참조되는 모든 데이터 저장소 바이너리를 보고합니다. 일관성 검사를 시작하려면 다음 단계를 수행합니다.

1. JMX 콘솔로 이동합니다. JMX 콘솔을 사용하는 방법에 대한 자세한 내용은 [이 문서를](/help/sites-administering/jmx-console.md#using-the-jmx-console)참조하십시오.
1. BlobGarbageCollection **Mbean을** 검색하고 클릭합니다.
1. 링크를 `checkConsistency()` 클릭합니다.

일관성 검사가 완료되면 누락된 것으로 보고된 바이너리의 수가 메시지에 표시됩니다. 숫자가 0보다 큰 경우 누락된 바이너리에 대한 자세한 내용은 을 `error.log` 참조하십시오.

다음은 누락된 이진이 로그에 보고되는 방법의 예입니다.

```xml
11:32:39.673 INFO [main] MarkSweepGarbageCollector.java:600 Consistency check found [1] missing blobs
```

```xml
11:32:39.673 WARN [main] MarkSweepGarbageCollector.java:602 Consistency check failure intheblob store : DataStore backed BlobStore [org.apache.jackrabbit.oak.plugins.blob.datastore.OakFileDataStore], check missing candidates in file /tmp/gcworkdir-1467352959243/gccand-1467352959243
```

