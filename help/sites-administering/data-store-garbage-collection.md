---
title: 데이터 저장소 가비지 컬렉션
description: 디스크 공간을 확보하기 위해 데이터 저장소 가비지 수집을 구성하는 방법에 대해 알아봅니다.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: 0dc4a8ce-5b0e-4bc9-a6f5-df2a67149e22
source-git-commit: bd3c3c2f833e4d7e763e7726c5c75597523605d7
workflow-type: tm+mt
source-wordcount: '1892'
ht-degree: 0%

---

# 데이터 저장소 가비지 컬렉션 {#data-store-garbage-collection}

기존 WCM 에셋이 제거되면 기본 데이터 저장소 레코드에 대한 참조가 노드 계층 구조에서 제거될 수 있지만 데이터 저장소 레코드 자체는 유지됩니다. 참조되지 않은 이 데이터 저장소 레코드는 보존할 필요가 없는 &quot;가비지&quot;가 됩니다. 가비지 에셋이 여러 개 있는 경우, 이를 제거하여 공간을 보존하고 백업 및 파일 시스템 유지 관리 성능을 최적화하는 것이 좋습니다.

대부분의 경우 WCM 애플리케이션은 정보를 수집하지만 정보를 거의 자주 삭제하지 않는 경향이 있습니다. 새 이미지가 추가되지만 이전 버전을 대체하더라도 버전 제어 시스템은 이전 버전을 유지하고 필요한 경우 이전 버전으로 되돌릴 수 있습니다. 따라서 시스템에 추가되는 것으로 생각하는 대부분의 콘텐츠는 효과적으로 영구적으로 저장됩니다. 따라서 정리할 저장소의 &quot;가비지&quot;의 일반적인 소스는 무엇입니까?

AEM은 저장소를 여러 내부 및 하우스키핑 활동을 위한 저장소로 사용합니다.

* 패키지 빌드 및 다운로드
* 게시 복제를 위해 생성된 임시 파일
* 워크플로우 페이로드
* DAM 렌더링 중에 임시로 만들어진 자산

이러한 임시 개체가 데이터 저장소에 저장해야 할 만큼 충분히 크고 개체가 결국 사용 중단되면 데이터 저장소 레코드 자체는 &quot;가비지&quot;로 유지됩니다. 일반적인 WCM 작성자/게시 애플리케이션에서 이 유형의 가장 큰 가비지 소스는 일반적으로 게시 활성화 프로세스입니다. 데이터가 Publish에 복제되는 경우 데이터가 먼저 &quot;Durbo&quot;라는 효율적인 데이터 형식으로 컬렉션에 수집되고 아래의 저장소에 저장되는 경우 `/var/replication/data`. 데이터 번들은 종종 데이터 저장소에 대한 임계 크기보다 크므로 데이터 저장소 레코드로 저장됩니다. 복제가 완료되면 의 노드가 `/var/replication/data` 가 삭제되지만 데이터 저장소 레코드는 &quot;가비지&quot;로 유지됩니다.

복구 가능한 또 다른 가비지 소스는 패키지입니다. 다른 모든 것과 마찬가지로 패키지 데이터는 저장소에 저장되므로 데이터 저장소의 4KB 이상 패키지에 대해 저장됩니다. 개발 프로젝트 과정에서 또는 시스템을 유지 관리하는 동안 시간이 지남에 따라 패키지를 여러 번 빌드 및 다시 빌드할 수 있으며 각 빌드는 이전 빌드의 레코드를 고립시키는 새 데이터 저장소 레코드를 생성합니다.

## 데이터 저장소 가비지 수집은 어떻게 작동합니까? {#how-does-data-store-garbage-collection-work}

저장소가 외부 데이터 저장소로 구성된 경우 [데이터 저장소 가비지 수집이 자동으로 실행됩니다.](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) 주별 유지 관리 창의 일부로 사용됩니다. 시스템 관리자는 다음과 같은 작업을 수행할 수도 있습니다 [수동으로 데이터 저장소 가비지 수집 실행](#running-data-store-garbage-collection) 필요에 따라. 일반적으로 데이터 저장소 가비지 수집은 주기적으로 수행되는 것이 좋지만 데이터 저장소 가비지 수집을 계획할 때는 다음 요소를 고려해야 합니다.

* 데이터 저장소 가비지 수집은 시간이 걸리고 성능에 영향을 줄 수 있으므로 적절하게 계획해야 합니다.
* 데이터 저장소 가비지 레코드를 제거해도 정상 성능에 영향을 주지 않으므로 성능 최적화는 아닙니다.
* 스토리지 사용률과 백업 시간 등 관련 요인을 고려하지 않을 경우 데이터 저장소 가비지 수집이 안전하게 지연될 수 있습니다.

데이터 저장소 가비지 수집기는 먼저 프로세스가 시작될 때 현재 타임스탬프를 기록합니다. 그런 다음 다중 패스 마크/스윕 패턴 알고리즘을 사용하여 컬렉션을 수행합니다.

첫 번째 단계에서 데이터 저장소 가비지 수집기는 모든 저장소 콘텐츠를 포괄적으로 이동합니다. 데이터 저장소 레코드에 대한 참조가 있는 각 컨텐트 객체의 경우 파일 시스템에서 파일을 찾아 메타데이터 업데이트(MTIME 속성 또는 &quot;마지막으로 수정된 항목&quot; 수정)를 수행합니다. 이 시점에서 이 단계에서 액세스하는 파일은 초기 기준 타임스탬프보다 최신이 됩니다.

두 번째 단계에서 데이터 저장소 가비지 수집기는 &quot;찾기&quot;와 거의 동일한 방식으로 데이터 저장소의 물리적 디렉터리 구조를 통과합니다. 파일의 &quot;last modified&quot; 또는 MTIME 속성을 검사하고 다음과 같이 판단합니다.

* MTIME이 초기 기준 타임스탬프보다 최신인 경우 첫 번째 단계에서 파일을 찾았거나, 수집 프로세스가 진행되는 동안 저장소에 추가된 완전히 새로운 파일입니다. 이러한 경우 레코드가 활성 상태로 간주되며 파일이 삭제되지 않습니다.
* MTIME이 초기 기준선 타임스탬프 이전이면 파일은 활성 참조 파일이 아니며 이동식 쓰레기로 간주됩니다.

이 접근 방식은 개인 데이터 저장소가 있는 단일 노드에 적합합니다. 그러나 데이터 저장소가 공유될 수 있으며, 이렇게 하면 다른 저장소의 데이터 저장소 레코드에 대한 활성 라이브 참조를 확인하지 않고 활성 참조 파일을 실수로 제거할 수 있습니다. 시스템 관리자는 가비지 수집을 계획하기 전에 데이터 저장소의 공유 특성을 이해하고 데이터 저장소가 공유되지 않은 것으로 알려진 경우에만 간단한 기본 제공 데이터 저장소 가비지 수집 프로세스를 사용해야 합니다.

>[!NOTE]
>
>클러스터형 또는 공유 데이터 저장소 설정에서 가비지 수집을 수행할 때(Mongo 또는 Segment Tar 사용) 로그에 특정 Blob ID를 삭제할 수 없다는 경고가 표시될 수 있습니다. 이 문제는 이전 가비지 컬렉션에서 삭제된 blob ID가 ID 삭제에 대한 정보가 없는 다른 클러스터 또는 공유 노드에서 다시 잘못 참조되기 때문에 발생합니다. 결과적으로 가비지 수집이 수행되면 마지막 실행에서 이미 삭제된 ID를 삭제하려고 할 때 경고가 기록됩니다. 이 동작은 성능 또는 기능에 영향을 주지 않습니다.

## 데이터 저장소 가비지 수집 실행 {#running-data-store-garbage-collection}

AEM이 실행 중인 데이터 저장소 설정에 따라 데이터 저장소 가비지 수집을 실행하는 세 가지 방법이 있습니다.

1. 경유 [개정 정리](/help/sites-deploying/revision-cleanup.md) - 일반적으로 노드 저장소 정리에 사용되는 가비지 수집 메커니즘.

1. 경유 [데이터 저장소 가비지 수집](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-operations-dashboard) - 작업 대시보드에서 사용할 수 있는 외부 데이터 저장소용 가비지 수집 메커니즘입니다.
1. 를 통해 [JMX 콘솔](/help/sites-administering/jmx-console.md).

TarMK가 노드 저장소와 데이터 저장소로 모두 사용되는 경우, 개정 정리는 노드 저장소와 데이터 저장소의 가비지 수집에 사용될 수 있습니다. 그러나 파일 시스템 데이터 저장소와 같이 외부 데이터 저장소가 구성된 경우 데이터 저장소 가비지 수집은 수정 정리 와 별도로 명시적으로 트리거되어야 합니다. 데이터 저장소 가비지 수집은 작업 대시보드 또는 JMX 콘솔을 통해 트리거할 수 있습니다.

아래 표는 AEM 6에서 지원되는 모든 데이터 저장소 배포에 사용해야 하는 데이터 저장소 가비지 수집 유형을 보여 줍니다.

<table>
 <tbody>
  <tr>
   <td><strong>노드 저장소</strong><br /> </td>
   <td><strong>데이터 저장소</strong></td>
   <td><strong>가비지 수집 메커니즘</strong><br /> </td>
  </tr>
  <tr>
   <td>TarMk</td>
   <td>TarMk</td>
   <td>개정 정리(바이너리가 세그먼트 스토어에 인라인됨)</td>
  </tr>
  <tr>
   <td>TarMk</td>
   <td>외부 파일 시스템</td>
   <td><p>Operations Dashboard를 통한 데이터 저장소 가비지 수집 작업</p> <p>JMX 콘솔</p> </td>
  </tr>
  <tr>
   <td>몽고DB</td>
   <td>몽고DB</td>
   <td><p>Operations Dashboard를 통한 데이터 저장소 가비지 수집 작업</p> <p>JMX 콘솔</p> </td>
  </tr>
  <tr>
   <td>몽고DB</td>
   <td>외부 파일 시스템</td>
   <td><p>Operations Dashboard를 통한 데이터 저장소 가비지 수집 작업</p> <p>JMX 콘솔</p> </td>
  </tr>
 </tbody>
</table>

### 작업 대시보드를 통해 데이터 저장소 가비지 수집 실행 {#running-data-store-garbage-collection-via-the-operations-dashboard}

내장된 주간 유지 관리 창(다음을 통해 사용 가능) [작업 대시보드](/help/sites-administering/operations-dashboard.md)에는 일요일 오전 1시에 데이터 저장소 가비지 수집을 트리거하는 기본 제공 작업이 포함되어 있습니다.

이 시간 외에 데이터 저장소 가비지 수집을 실행해야 하는 경우 작업 대시보드를 통해 수동으로 트리거할 수 있습니다.

데이터 저장소 가비지 수집을 실행하기 전에 백업이 실행되고 있지 않은지 확인해야 합니다.

1. 다음 방법으로 작업 대시보드 열기 **탐색** > **도구** > **작업** > **유지 관리**.
1. 다음을 클릭합니다. **주간 유지 관리 창**.

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. 다음 항목 선택 **데이터 저장소 가비지 수집** 작업을 클릭한 다음 **실행** 아이콘.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 데이터 저장소 가비지 수집이 실행되고 상태가 대시보드에 표시됩니다.

   ![chlimage_1-66](assets/chlimage_1-66.png)

>[!NOTE]
>
>데이터 저장소 가비지 수집 작업은 외부 파일 데이터 저장소를 구성한 경우에만 표시됩니다. 다음을 참조하십시오 [AEM 6에서 노드 저장소 및 데이터 저장소 구성](/help/sites-deploying/data-store-config.md#file-data-store) 파일 데이터 저장소를 설정하는 방법에 대한 정보를 제공합니다.

### JMX 콘솔을 통해 데이터 저장소 가비지 수집 실행 {#running-data-store-garbage-collection-via-the-jmx-console}

이 섹션은 JMX 콘솔을 통해 데이터 저장소 가비지 수집을 수동으로 실행하는 방법에 대한 것입니다. 외부 데이터 저장소 없이 설치가 설정된 경우 설치에 적용되지 않습니다. 대신 아래에서 개정 정리를 실행하는 방법에 대한 지침을 참조하십시오. [저장소 유지 관리](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).

>[!NOTE]
>
>외부 데이터 저장소와 함께 TarMK를 실행하는 경우 가비지 수집이 유효하려면 먼저 수정 정리 를 실행해야 합니다.

가비지 수집을 실행하려면:

1. Apache Felix OSGi 관리 콘솔에서 다음을 강조 표시합니다. **기본** 탭하고 선택 **JMX** 다음 메뉴를 참조하십시오.
1. 그런 다음 을(를) 검색하고 **저장소 관리자** MBean(또는 다음으로 이동) `https://<host>:<port>/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Drepository+manager%2Ctype%3DRepositoryManagement`).
1. 클릭 **startDataStoreGC(부울 markOnly)**.
1. &quot; 입력`true`에 대해 &quot; `markOnly` 필요한 경우 매개 변수:

   | **옵션** | **설명** |
   |---|---|
   | 부울 markOnly | 표시 및 스윕 작업에서 참조를 표시하고 스윕하지 않으려면 true로 설정합니다. 이 모드는 기본 BlobStore가 여러 다른 저장소 간에 공유될 때 사용됩니다. 다른 모든 경우에 대해 전체 가비지 수집을 수행하려면 false로 설정하십시오. |

1. 클릭 **호출**. CRX는 가비지 수집을 실행하고 완료 시기를 나타냅니다.

>[!NOTE]
>
>데이터 저장소 가비지 수집은 지난 24시간 동안 삭제된 파일을 수집하지 않습니다.

>[!NOTE]
>
>데이터 저장소 가비지 수집 작업은 외부 파일 데이터 저장소를 구성한 경우에만 시작됩니다. 외부 파일 데이터 저장소가 구성되지 않은 경우 작업에서 메시지를 반환합니다 `Cannot perform operation: no service of type BlobGCMBean found` 호출 후. 다음을 참조하십시오 [AEM 6에서 노드 저장소 및 데이터 저장소 구성](/help/sites-deploying/data-store-config.md#file-data-store) 파일 데이터 저장소를 설정하는 방법에 대한 정보를 제공합니다.

## 데이터 저장소 가비지 수집 자동화 {#automating-data-store-garbage-collection}

가능하면 시스템에 부하가 적은 경우(예: 아침에) 데이터 저장소 가비지 수집을 실행해야 합니다.

내장된 주간 유지 관리 창(다음을 통해 사용 가능) [작업 대시보드](/help/sites-administering/operations-dashboard.md)에는 일요일 오전 1시에 데이터 저장소 가비지 수집을 트리거하는 기본 제공 작업이 포함되어 있습니다. 또한 현재 실행 중인 백업이 없는지 확인해야 합니다. 유지 관리 창의 시작은 필요에 따라 대시보드를 통해 사용자 정의할 수 있습니다.

>[!NOTE]
>
>동시에 실행하지 않는 이유는 오래된(및 사용되지 않은) 데이터 저장소 파일도 백업되기 때문에 이전 버전으로 롤백해야 하는 경우 바이너리가 여전히 백업에 있기 때문입니다.

작업 대시보드의 주간 유지 관리 창에서 데이터 저장소 가비지 수집을 실행하지 않으려면 Wget 또는 curl HTTP 클라이언트를 사용하여 자동화할 수도 있습니다. 다음은 curl을 사용하여 가비지 수집을 자동화하는 방법의 예입니다.

>[!CAUTION]
>
>다음 예에서 `curl` 명령에 인스턴스에 대해 다양한 매개 변수를 구성해야 할 수 있습니다. 예: 호스트 이름( `localhost`), 포트( `4502`), 관리자 암호( `xyz`)와 실제 데이터 저장소 가비지 수집에 대한 다양한 매개 변수.

다음은 명령줄을 통해 데이터 저장소 가비지 수집을 호출하는 curl 명령의 예입니다.

```shell
curl -u admin:admin -X POST --data markOnly=true  https://localhost:4503/system/console/jmx/org.apache.jackrabbit.oak"%"3Aname"%"3Drepository+manager"%"2Ctype"%"3DRepositoryManagement/op/startDataStoreGC/boolean
```

curl 명령은 즉시 반환됩니다.

## 데이터 저장소 일관성 확인 {#checking-data-store-consistency}

데이터 저장소 일관성 검사는 누락되었지만 여전히 참조되는 모든 데이터 저장소 바이너리를 보고합니다. 일관성 검사를 시작하려면 다음 단계를 수행합니다.

1. JMX 콘솔로 이동합니다. JMX 콘솔 사용 방법에 대한 자세한 내용은 [이 문서](/help/sites-administering/jmx-console.md#using-the-jmx-console).
1. 검색 **BlobGarbageCollection** Mbean을 누르고 클릭합니다.
1. 다음을 클릭합니다. `checkConsistency()` 링크를 클릭합니다.

일관성 검사가 완료되면 누락된 것으로 보고된 바이너리 수가 표시됩니다. 숫자가 0보다 큰 경우 `error.log` 누락된 바이너리에 대한 자세한 내용은 을 참조하십시오.

다음은 누락된 바이너리가 로그에 보고되는 방식에 대한 예입니다.

```xml
11:32:39.673 INFO [main] MarkSweepGarbageCollector.java:600 Consistency check found [1] missing blobs
```

```xml
11:32:39.673 WARN [main] MarkSweepGarbageCollector.java:602 Consistency check failure intheblob store : DataStore backed BlobStore [org.apache.jackrabbit.oak.plugins.blob.datastore.OakFileDataStore], check missing candidates in file /tmp/gcworkdir-1467352959243/gccand-1467352959243
```
