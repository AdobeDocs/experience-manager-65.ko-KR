---
title: 개정 정리
seo-title: Revision Cleanup
description: AEM 6.5에서 개정 정리 기능을 사용하는 방법을 알아봅니다.
seo-description: Learn how to use the Revision Cleanup functionality in AEM 6.5.
uuid: 321f5038-44b0-4f1e-a1aa-2d29074eed70
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: f03ebe60-88c0-4fc0-969f-949490a8e768
feature: Configuring
exl-id: e53c4c81-f62e-4b6d-929a-6649c8ced23c
source-git-commit: b7f9b5256e07d4bfbc0c3454e8d2fe112ea650e8
workflow-type: tm+mt
source-wordcount: '5918'
ht-degree: 0%

---

# 개정 정리{#revision-cleanup}

## 소개 {#introduction}

저장소에 대한 각 업데이트에서는 새 컨텐츠 개정을 만듭니다. 따라서 각 업데이트 시 저장소의 크기가 증가합니다. 저장소 증가를 제어하지 않으려면 사용 가능한 디스크 리소스를 위해 이전 버전을 정리해야 합니다. 이 유지 관리 기능을 개정 정리라고 합니다. AEM 6.0 이후 오프라인 루틴으로 사용할 수 있습니다.

AEM 6.3 이상에서는 온라인 개정 정리 라는 이 기능의 온라인 버전이 도입되었습니다. AEM 인스턴스를 종료해야 하는 오프라인 개정 정리 와 비교하여 AEM 인스턴스가 온라인 상태인 동안 온라인 개정 정리를 실행할 수 있습니다. 온라인 개정 정리 는 기본적으로 켜져 있으며 개정 정리를 수행하는 권장 방법입니다.

**참고**: [비디오를 참조하십시오](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/revision-cleanup-technical-video-use.html) 를 참조하십시오.

개정 정리 프로세스는 다음 세 단계로 구성됩니다. **측정**, **압축** 및 **정리**. 추정은 다음 단계(압축)를 실행할지 여부를 가비지 수집의 양을 기준으로 결정합니다. 압축 단계 세그먼트 및 tar 파일은 사용하지 않는 콘텐츠를 제외하고 다시 작성됩니다. 정리 단계는 이후에 포함할 수 있는 쓰레기를 포함하는 이전 세그먼트를 제거합니다. 오프라인 모드는 추가 세그먼트가 수집되지 않도록 하는 AEM 작업 세트를 고려해야 하므로 일반적으로 더 많은 공간을 확보할 수 있습니다.

개정 정리를 위한 자세한 내용은 다음 링크를 참조하십시오.

* [온라인 개정 정리 실행 방법](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)
* [온라인 개정 정리 FAQ](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)
* [오프라인 개정 정리 실행 방법](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup)

또한 [공식 Oak 문서입니다.](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html)

### 오프라인 개정 정리 대신 온라인 개정 정리를 언제 사용해야 합니까? {#when-to-use-online-revision-cleanup-as-opposed-to-offline-revision-cleanup}

**온라인 개정 정리 는 개정 정리를 수행하는 권장 방법입니다.** 오프라인 개정 정리 는 새로운 스토리지 형식으로 마이그레이션하기 전 또는 고객 지원 센터에서 이러한 작업을 요청받는 경우 등 특별한 기준으로만 사용해야 합니다.

## 온라인 개정 정리 실행 방법 {#how-to-run-online-revision-cleanup}

온라인 개정 정리 는 기본적으로 AEM 작성자 및 게시 인스턴스 둘 다에서 하루에 한 번 자동으로 실행되도록 구성됩니다. 최소한의 사용자 활동이 있는 기간 동안 유지 관리 창을 정의하기만 하면 됩니다. 다음과 같이 온라인 개정 정리 작업을 구성할 수 있습니다.

1. 기본 AEM 창에서 **도구 - 작업 - 대시보드 - 유지 관리** 또는 브라우저를 다음과 같은 위치로 보냅니다. `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 마우스로 가리키기 **일별 유지 관리 창** 을 클릭하고 **설정** 아이콘.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 원하는 값(되풀이, 시작 시간, 종료 시간)을 입력하고 **저장**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

또는 개정 정리 작업을 수동으로 실행하려면 다음을 수행할 수 있습니다.

1. 이동 **도구 - 작업 - 대시보드 - 유지 관리** 또는 직접 찾아보거나 `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`
1. 을(를) 클릭합니다. **일별 유지 관리 창**.
1. 마우스를 위에 놓으십시오 **개정 정리** 아이콘.
1. 클릭 **실행**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

### 오프라인 개정 정리 후 온라인 개정 정리 실행 {#running-online-revision-cleanup-after-offline-revision-cleanup}

개정 정리 프로세스는 세대별로 이전 개정을 다시 처리합니다. 즉, 개정 정리를 실행할 때마다 새로운 생성이 만들어지고 디스크에 유지됩니다. 그러나 두 가지 수정 정리 유형 간에는 차이가 있습니다. 오프라인 개정 정리를 사용하면 1세대, 온라인 개정 정리 시 2세대 간에 차이가 없습니다. 따라서 온라인 개정 정리를 실행할 때 **after** 오프라인 개정 정리:

1. 첫 번째 온라인 개정 정리 실행 후 저장소의 크기가 두 배로 증가합니다. 이런 일은 현재 디스크에 2세대 동안 보관되어 있기 때문입니다.
1. 온라인 개정 정리 프로세스는 이전 세대를 재실행함에 따라, 이후 실행 중에 새로운 생성이 생성되는 동안 저장소가 일시적으로 확장되고 첫 번째 실행 후 다시 원래 크기로 안정화됩니다.

또한 커밋 유형 및 횟수에 따라 각 생성의 크기가 이전 생성과 비교하여 다를 수 있으므로 최종 크기는 한 실행마다 다를 수 있습니다.

이러한 사실로 인해 디스크 크기를 최초 예상 저장소 크기보다 최소 2~3배 더 크게 하는 것이 좋습니다.

## 전체 및 테일 압축 모드  {#full-and-tail-compaction-modes}

**AEM 6.5** 소개 **새로운 모드** 대상 **압축** 온라인 개정 정리 프로세스의 단계:

* 다음 **완전한 압축** 모드는 전체 리포지토리의 모든 세그먼트와 tar 파일을 다시 기록합니다. 따라서 후속 정리 단계에서는 저장소에 있는 최대 가비지 양을 제거할 수 있습니다. 전체 압축은 전체 저장소에 영향을 주므로 상당한 양의 시스템 리소스와 완료 시간이 필요합니다. 전체 압축은 AEM 6.3의 압축 단계에 해당합니다.
* 다음 **테일 압축** 모드는 리포지토리의 가장 최근 세그먼트와 tar 파일만 다시 기록합니다. 가장 최근 세그먼트와 tar 파일은 전체 또는 세부 압축이 마지막으로 실행된 이후 추가된 세그먼트입니다. 따라서 후속 정리 단계에서는 저장소의 최근 부분에 포함된 쓰레기만 제거할 수 있습니다. 테일 압축은 저장소의 부분에만 영향을 주므로 전체 압축보다 시스템 리소스와 완료 시간이 상당히 적게 필요합니다.

이러한 압축 모드는 효율성과 자원 소비 간의 차단을 구성합니다. 테일 압축은 덜 효과적이지만 정상적인 시스템 운영에도 영향을 덜 줍니다. 반면 전체 압축은 효과적이지만 정상적인 시스템 운영에는 더 큰 영향을 줍니다.

또한 AEM 6.5에서는 압축 중에 더욱 효율적인 컨텐츠 중복 제거 메커니즘을 도입하여 저장소의 온디스크 공간을 더욱 줄여줍니다.

아래 두 차트는 AEM 6.3과 비교하여 AEM 6.5의 평균 실행 시간과 디스크의 평균 사용 공간을 감소시킨 내부 실험 테스트 결과를 보여줍니다.

![onrc-duration-6_4vs63](assets/onrc-duration-6_4vs63.png) ![segmentstore-6_4vs63](assets/segmentstore-6_4vs63.png)

### 전체 및 세부 압축을 구성하는 방법 {#how-to-configure-full-and-tail-compaction}

기본 구성은 주 일마다, 일요일에는 전체 압축이 실행됩니다. 기본 구성은 새 구성 값을 사용하여 변경할 수 있습니다 `full.gc.days` 의 `RevisionCleanupTask` [유지 작업](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup).

를 구성할 때 `full.gc.days` 값은 값에 정의되지 않은 일 동안 값과 테일 압축에 정의된 일 동안 전체 압축이 실행됩니다. 예를 들어 일요일에 전체 압축이 실행되도록 구성하는 경우 월요일부터 토요일까지 후속 압축이 실행됩니다. 예를 들어 매일 실행되도록 전체 압축을 구성하면 테일 압축이 전혀 실행되지 않습니다.

또한 다음 사항을 고려하십시오.

* **테일 압축** 이 기능은 효과적이지 않고 정상적인 시스템 운영에 미치는 영향이 적습니다. 따라서 영업일 동안 실행되도록 합니다.
* **전체 압축** 이 기능은 더 효과적이지만 정상적인 시스템 운영에도 더 큰 영향을 줍니다. 따라서 영업일 중에 사용하려고 합니다.
* 테일 압축과 전체 압축은 모두 비성수기 동안 실행되도록 예약해야 합니다.

### 문제 해결 {#troubleshooting}

새 압축 모드를 사용할 때는 다음 사항에 유의하십시오.

* 입출력(I/O) 활동을 모니터링할 수 있습니다. 예를 들면 다음과 같습니다. I/O 작업, IO 대기 중인 CPU, 커밋 큐 크기 이렇게 하면 시스템이 I/O로 바인딩되고 있고 업사이징이 필요한지 여부를 판별할 수 있습니다.
* 다음 `RevisionCleanupTaskHealthCheck` 온라인 개정 정리 의 전체 상태 상태를 나타냅니다. AEM 6.3에서와 동일한 방식으로 작동하며 전체 압축과 테일 압축을 구분하지 않습니다.
* 로그 메시지에는 압축 모드에 대한 관련 정보가 들어 있습니다. 예를 들어 온라인 개정 정리를 시작하면 해당 로그 메시지에 압축 모드가 표시됩니다. 또한 일부 경우에 따라 시스템이 테일 압축을 실행하도록 예약된 경우 전체 압축으로 복원되고 로그 메시지에 이 변경 사항이 표시됩니다. 아래의 로그 샘플은 압축 모드와 테일에서 전체 압축으로 변경 사항을 나타냅니다.

```
TarMK GC: running tail compaction
TarMK GC: no base state available, running full compaction instead
```

### 알려진 제한 사항 {#known-limitations}

경우에 따라 테일과 전체 압축 모드 간에 교대로 인해 정리 프로세스가 지연됩니다. 보다 정확하게 말하면 리포지토리는 전체 압축 후 증가합니다(크기는 두 배로 늘어남). 저장소가 전체 압축 크기 이하로 떨어질 때 추가 공간은 이후 테일 압축에서 회수됩니다. 병렬 유지 관리 작업 실행도 피해야 합니다.

**디스크 크기를 처음에 예상되는 저장소 크기보다 최소 2~3배 더 크게 하는 것이 좋습니다.**

## 온라인 개정 정리 FAQ {#online-revision-cleanup-frequently-asked-questions}

### AEM 6.5 업그레이드 고려 사항 {#aem-upgrade-considerations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td>질문 </td>
   <td>답변</td>
  </tr>
  <tr>
   <td>AEM 6.5로 업그레이드할 때 무엇을 알아야 합니까?</td>
   <td><p>TarMK의 지속성 형식은 AEM 6.5에서 변경됩니다. 이러한 변경 사항에는 사전 마이그레이션 단계가 필요하지 않습니다. 기존 리포지토리는 사용자에게 투명하게 롤링 마이그레이션을 수행합니다. AEM 6.5(또는 관련 도구)가 저장소에 처음 액세스하면 마이그레이션 프로세스가 시작됩니다.</p> <p><strong>AEM 6.5 지속성 포맷으로의 마이그레이션이 시작되면 리포지토리를 이전 AEM 6.3 지속성 형식으로 다시 되돌릴 수 없습니다.</strong></p> </td>
  </tr>
 </tbody>
</table>

### Oak 세그먼트 Tar로 마이그레이션 {#migrating-to-oak-segment-tar}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>질문</strong></td>
   <td><strong>답변</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>리포지토리를 마이그레이션해야 하는 이유는 무엇입니까?</strong></td>
   <td><p>AEM 6.3에서는 특히 온라인 개정 정리 성능 및 효율성을 향상시키기 위해 스토리지 포맷을 변경해야 했습니다. 이러한 변경 사항은 이전 버전과 호환되지 않으며, 이전 Oak 세그먼트(AEM 6.2 및 이전)로 생성된 리포지토리는 마이그레이션해야 합니다.</p> <p>스토리지 포맷을 변경하면 다음과 같은 이점을 얻을 수 있습니다.</p>
    <ul>
     <li>향상된 확장성(최적화된 세그먼트 크기).</li>
     <li>더 빠름 <a href="/help/sites-administering/data-store-garbage-collection.md" target="_blank">데이터 저장소 가비지 수집</a>.<br /> </li>
     <li>향후 개선 사항을 위한 기본 작업.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>이전 Tar 형식이 계속 지원됩니까?</strong></td>
   <td>새 Oak Segment Tar만 AEM 6.3 이상에서 지원됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>컨텐츠 마이그레이션은 항상 필수 사항입니까?</strong></td>
   <td>예. 새 인스턴스로 시작하지 않는 한 항상 컨텐츠를 마이그레이션해야 합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>6.3 이상으로 업그레이드하고 나중에 마이그레이션을 수행할 수 있습니까(예: 다른 유지 관리 창 사용)?</strong></td>
   <td>아니요. 위에서 설명한 대로 컨텐츠 마이그레이션은 필수입니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>마이그레이션할 때 다운타임을 피할 수 있습니까?</strong></td>
   <td>아니요. 실행 중인 인스턴스에서 수행할 수 없는 일회성 작업입니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>잘못된 저장소 형식에 대해 실수로 실행하면 어떻게 됩니까?</strong></td>
   <td>oak-segment-tar 저장소에 대해 oak-segment 모듈을 실행하려고 하면(또는 그 반대로), <em>IllegalStateException</em> 세그먼트 형식이 잘못되었습니다. 데이터가 손상되지 않습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>검색 색인의 재색인이 필요합니까?</strong></td>
   <td>아니요. oak-segment에서 oak-segment-tar로 마이그레이션하면 컨테이너 포맷의 변경 사항이 발생합니다. 포함된 데이터는 영향을 받지 않으며 수정되지 않습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>마이그레이션 중 및 이후에 필요한 예상 디스크 공간을 최상으로 계산하는 방법</strong></td>
   <td>마이그레이션은 세그먼트스토어를 새 형식으로 다시 만드는 것과 같습니다. 마이그레이션 중에 필요한 추가 디스크 공간을 추정하는 데 사용할 수 있습니다. 마이그레이션 후 이전 세그먼트 저장소를 삭제하여 공간을 다시 확보할 수 있습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>마이그레이션 기간을 가장 잘 추정하는 방법</strong></td>
   <td>다음과 같은 경우 마이그레이션 성능을 크게 향상시킬 수 있습니다 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup">오프라인 개정 정리</a> 가 마이그레이션 전에 실행됩니다. 모든 고객은 업그레이드 프로세스의 전제 조건으로 이를 실행하는 것이 좋습니다. 일반적으로, 오프라인 개정 정리 작업이 마이그레이션 전에 실행되었다고 가정할 경우 마이그레이션 기간은 오프라인 개정 정리 작업의 기간과 유사해야 합니다.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 온라인 개정 정리 실행 {#running-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>질문</strong></td>
   <td><strong>답변</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리를 얼마나 자주 실행해야 합니까?</strong></td>
   <td>매일 한 번. 작업 대시보드의 기본 구성입니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 유지 관리 작업의 시작 시간을 어떻게 구성할 수 있습니까?</strong></td>
   <td>자세한 내용은 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">온라인 개정 정리를 실행하는 방법</a> 섹션을 참조하십시오. </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 시 초과해서는 안 되는 최대 빈도가 있습니까?</strong></td>
   <td>기본적으로 구성된 대로 하루에 한 번 온라인 개정 정리를 실행하는 것이 좋습니다.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리를 실행해야 하는 빈도를 결정하는 주요 지표는 무엇입니까?</strong></td>
   <td>온라인 개정 정리를 유지 관리 작업으로 구성하고 매일 자동으로 실행하므로 빈도를 확인할 필요가 없습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>처음 실행될 때 온라인 개정 정리 가 공간을 다시 확보하지 않는 이유는 무엇입니까?</strong></td>
   <td>온라인 개정 정리 는 세대별로 이전 개정을 다시 청구합니다. 개정 정리를 실행할 때마다 새로운 생성이 생성됩니다. 최소 2세대인 컨텐츠만 재매립됩니다. 즉, 첫 번째 실행에서는 재확보 할 필요가 없습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>오프라인 개정 정리 후 실행될 때 첫 번째 온라인 개정 정리 가 공간을 다시 확보하지 못하는 이유는 무엇입니까?</strong></td>
   <td><p>오프라인 개정 정리 가 온라인 개정 정리를 위한 최신 2세대 버전과 비교하여 최신 세대를 제외한 모든 것을 되찾고 있습니다. 새 리포지토리의 경우, 재확보하기에 충분한 생성 시간이 없으므로 오프라인 개정 정리 후 처음으로 실행될 때 온라인 개정 정리 가 공간을 재확보하지 않습니다.</p> <p>또한 오프라인 개정 정리 후 온라인 개정 정리 실행 섹션을 참조하십시오 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">이 장</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>작성자와 게시에 일반적으로 다른 온라인 개정 정리 창이 있습니까?</strong></td>
   <td>이는 고객의 온라인 유무에 따른 근무 시간 및 트래픽 패턴에 따라 다릅니다. 유지 관리 기간은 주 생산 시간 외에 구성하여 최상의 정리 효과를 얻을 수 있도록 해야 합니다. 여러 AEM 게시 인스턴스(TarMK 팜)의 경우, 온라인 개정 정리를 위한 유지 관리 기간은 서로 달라야 합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리를 실행하기 전에 사전 요구 사항이 있습니까?</strong></td>
   <td><p>온라인 개정 정리 는 AEM 6.3 이상의 릴리스에서만 사용할 수 있습니다. 또한 이전 버전의 AEM을 사용하는 경우 새 버전으로 마이그레이션해야 합니다 <a href="/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar">Oak 세그먼트 Tar</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 기간을 결정하는 요소는 무엇입니까?</strong></td>
   <td>요소는 다음과 같습니다.<br />
    <ul>
     <li>저장소 크기</li>
     <li>시스템에 로드(분당 요청, 특히 쓰기 작업)</li>
     <li>활동 패턴(읽기 및 쓰기)</li>
     <li>하드웨어 사양(CPU 성능, 메모리, IOPS)</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리를 실행하는 동안 작성자가 계속 작동할 수 있습니까?</strong></td>
   <td>예. 온라인 개정 정리 기능은 동시 쓰기를 처리할 수 있습니다. 그러나 동시 쓰기 트랜잭션 없이 온라인 개정 정리 기능이 보다 빠르고 효율적으로 작동합니다. 많은 트래픽 없이 온라인 개정 정리 유지 관리 작업을 비교적 조용한 시간으로 예약하는 것이 좋습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Online Revision Cleanup을 실행할 때 디스크 공간 및 힙메모리의 최소 요구 사항은 무엇입니까?</strong></td>
   <td><p>온라인 개정 정리 중에 디스크 공간이 계속 모니터링됩니다. 사용 가능한 디스크 공간이 임계값보다 작은 경우 프로세스가 취소됩니다. 중요한 값은 리포지토리의 현재 디스크 사용 공간의 25%이며 구성할 수 없습니다.</p> <p><strong>디스크 크기를 처음에 예상되는 저장소 크기보다 최소 2~3배 더 크게 하는 것이 좋습니다.</strong></p> <p>정리 프로세스 중에 사용 가능한 힙이 계속 모니터링됩니다. 사용 가능한 힙이 임계값보다 작은 경우 프로세스가 취소됩니다. 중요 값은 org.apache.jackrabbit.oak.segment.SegmentNodeStoreService#MEMORY_THRESHOLD를 통해 구성됩니다. 기본값은 15입니다%.</p> <p>최소 압축 힙용 Recommendations은 AEM 메모리 크기 조정 권장 사항과 분리되지 않습니다. 일반적인 규칙으로: <strong>AEM 인스턴스의 크기가 사용 사례와 예상 페이로드를 처리할 수 있을 만큼 충분히 큰 경우 정리 프로세스는 충분한 메모리를 확보합니다.</strong></p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리를 실행하는 동안 예상되는 성능에 어떤 영향이 있습니까?</strong></td>
   <td>온라인 개정 정리 는 일반적인 시스템 작업과 동시에 저장소에서 읽고 저장소에 쓰는 백그라운드 프로세스입니다. 특히 다른 스레드가 리포지토리에 기록되지 않도록 짧은 시간 동안 리포지토리에 대한 단독 액세스 권한을 획득해야 할 수 있습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 가 얼마나 오래 실행됩니까?</strong></td>
   <td>내부적으로 수행한 최신 성능 테스트에 따라 실행하는 데 2시간 이상 걸리지 않습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 시간이 더 오래 걸리는 경우 어떻게 해야 합니까?</strong></td>
   <td>
    <ul>
     <li>매일 실행되도록 합니다.<br /> </li>
     <li>Operations Dashboard에서 유지 관리 창을 구성하여 최소 저장소 활동 중에 실행되도록 합니다.</li>
     <li>시스템 리소스(CPU, 메모리, I/O) 확장</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 기능이 구성된 유지 관리 창을 초과하는 경우 어떻게 됩니까?</strong></td>
   <td>다른 유지 관리 작업이 실행을 지연하지 않도록 하십시오. 동일한 유지 관리 기간 내에 온라인 개정 정리 보다 많은 유지 관리 작업이 실행되는 경우가 있을 수 있습니다. 유지 관리 작업은 구성 가능한 순서 없이 순차적으로 실행됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>수정 가비지 수집을 건너뛴 이유는 무엇입니까?</strong></td>
   <td><p>개정 정리 는 청소할 쓰레기가 충분한지 결정하기 위해 예측 단계를 사용합니다. 견적 도구 는 현재 크기를 마지막으로 압축한 후 저장소의 크기와 비교합니다. 크기가 구성된 델타를 초과하는 경우 정리를 실행합니다. 크기 델타는 1GB로 설정됩니다. 즉, 마지막 정리 실행 이후 저장소 크기가 1GB까지 증가하지 않은 경우 새 개정 정리 반복을 건너뜁니다. </p> <p>다음은 측정 단계에 대한 관련 로그 항목입니다.</p>
    <ul>
     <li>수정 GC가 실행됩니다. <em>크기 델타는 N% 또는 N/N(N/N 바이트)이므로 압축 실행</em></li>
     <li>버전 GC가 <strong>not</strong> 실행: <em>크기 델타는 N% 또는 N/N(N/N 바이트)이므로 현재 압축을 건너뜁니다</em></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>성능 영향이 너무 큰 경우 자동 압축을 안전하게 중단할 수 있습니까?</strong></td>
   <td>예. AEM 6.3은 작업 대시보드 또는 JMX를 통해 유지 관리 작업 창을 통해 안전하게 중지할 수 있습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>예약된 정리 작업 중에 AEM 인스턴스가 종료되면 프로세스가 안전하게 중단됩니까, 아니면 압축 작업이 완료될 때까지 종료가 차단됩니까?</strong></td>
   <td>개정 정리 가 중단되고 저장소가 안전하게 종료됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 중에 시스템이 충돌하면 어떻게 됩니까?</strong></td>
   <td>이런 경우에는 데이터 손상 위험이 없습니다. 남은 음식물은 다음 번 가보면 청소될 것이다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리를 실행하지 않으면 어떤 영향이 있습니까?</strong></td>
   <td>시간이 지남에 따라 성능이 저하됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>어떤 수정 버전을 수집하고 있습니까?</strong></td>
   <td>기본적으로 온라인 개정 정리 는 최소 24시간 경과한 버전만 수집합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>리포지토리에 동시 쓰기에서 너무 많은 간섭이 발생하는 경우 어떻게 됩니까?</strong></td>
   <td><p>시스템에 쓰기 동시성이 있는 경우, 온라인 개정 정리 시 압축 주기 종료 시 변경 사항을 커밋하려면 전용 쓰기 액세스 권한이 필요할 수 있습니다. 시스템이 <strong>forceCompact 모드</strong>를 참조하십시오. <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html" target="_blank">oak 설명서</a>. 강제 압축이 수행되는 동안 동시 쓰기가 방해되지 않고 변경 사항을 최종적으로 커밋하기 위해 단독 쓰기 잠금이 획득됩니다. 응답 시간에 미치는 영향을 제한하려면 시간 초과 값을 정의할 수 있습니다. 이 값은 기본적으로 1분으로 설정되어 있습니다. 즉, 1분 내에 압축 작업이 완료되지 않으면 동시 커밋을 위해 압축 프로세스가 중단됩니다.</p> <p>힘 컴팩트의 기간은 다음 요소에 따라 다릅니다.</p>
    <ul>
     <li>하드웨어: 특히 IOPS 지속 시간은 더 많은 IOPS로 줄어듭니다.</li>
     <li>세그먼트 저장소 크기: 지속 시간은 세그먼트 저장소의 크기에 따라 증가합니다.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>대기 인스턴스에서 온라인 개정 정리를 어떻게 실행합니까?</strong></p> </td>
   <td><p>콜드 대기 설정에서 기본 인스턴스만 온라인 개정 정리를 실행하도록 구성해야 합니다. 대기 인스턴스에서 온라인 개정 정리를 특별히 예약할 필요가 없습니다.</p> <p>대기 인스턴스의 해당 작업은 자동 정리(Automatic Cleanup)이며, 이는 온라인 개정 정리 단계의 정리 단계에 해당합니다. 기본 인스턴스에서 온라인 개정 정리를 실행한 후 대기 인스턴스에서 자동 정리가 실행됩니다.</p> <p>대기 인스턴스에서 측정 및 압축 단계가 실행되지 않습니다.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>오프라인 개정 정리를 통해 온라인 개정 정리 보다 더 많은 디스크 공간을 확보할 수 있습니까?</strong></td>
   <td><p>오프라인 개정 정리 는 응용 프로그램 스택에서 계속 참조되는 이전 개정을 고려해야 하는 동안 이전 개정을 즉시 제거할 수 있습니다. 따라서 일부 쓰레기 수거 주기 동안 효과가 상감되는 후자보다 더 적극적으로 쓰레기를 제거할 수 있다.</p> <p>또한 오프라인 개정 정리 후 온라인 개정 정리 실행 섹션을 참조하십시오 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">이 장</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>메모리 매핑 파일 작업에 대한 고려 사항이 있습니까?</td>
   <td>
    <ul>
     <li><strong>Windows 환경에서</strong>인 경우 메모리 매핑 액세스가 사용되지 않도록 항상 일반 파일 액세스가 적용됩니다. 일반적인 권고 사항으로 사용 가능한 모든 RAM을 힙에 할당하고 segmentCache 크기를 늘려야 합니다. segmentCache.size 옵션을 org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config(예: segmentCache.size=20480)에 추가하여 segmentCache를 증가시킵니다. 운영 체제 및 기타 프로세스에 사용할 RAM을 남겨 두어야 합니다.</li>
     <li><strong>Windows 이외의 환경에서</strong>를 눌러 실제 메모리 크기를 늘려 저장소의 메모리 매핑을 개선합니다.</li>
    </ul> </td>
   <td>
    <ul>
     <li> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 온라인 개정 정리 모니터링 {#monitoring-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>온라인 개정 정리 중에 모니터링해야 하는 것은 무엇입니까?</strong></td>
   <td>
    <ul>
     <li>온라인 개정 정리를 사용하는 경우 디스크 공간을 모니터링해야 합니다. 디스크 공간이 부족하면 정리 작업이 실행되지 않거나 미리 종료됩니다.</li>
     <li>로그에서 온라인 개정 정리 완료 시간을 확인합니다. 2시간 이상 걸리지 않을 겁니다</li>
     <li>체크포인트 수. 압축 실행 시 체크포인트가 3개 이상인 경우에는 체크포인트를 정리하는 것이 좋습니다.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리를 성공적으로 완료했는지 확인하는 방법</strong></td>
   <td><p>로그를 확인하여 온라인 개정 정리를 성공적으로 완료했는지 확인할 수 있습니다.</p> <p>예: "<code>TarMK GC #{}: compaction completed in {} ({} ms), after {} cycles</code>"은(는) 메시지 앞에 오지 않는 한 압축 단계를 성공적으로 완료했음을 의미합니다. "<code>TarMK GC #{}: compaction gave up compacting concurrent commits after {} cycles</code>"즉, 동시 로드가 너무 많다는 뜻입니다.</p> <p>이에 따라 "<code>TarMK GC #{}: cleanup completed in {} ({} ms</code>"을 눌러 정리 단계를 성공적으로 완료합니다.</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><strong>마지막 온라인 개정 정리 실행의 통계는 어디에서 찾을 수 있습니까?</strong></td>
   <td><p>JMX(<code>SegmentRevisionGarbageCollection</code> MBean). 에 대한 자세한 내용은 <code>SegmentRevisionGarbageCollection</code> MBean, <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">다음 단락을 참조하십시오.</a>.</p> <p>진행 상태는 <code>EstimatedRevisionGCCompletion</code> 의 속성 <code>SegmentRevisionGarbageCollection MBean.</code></p> <p>를 사용하여 MBean에 대한 참조를 얻을 수 있습니다. <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code>.</p> <p>통계는 마지막 시스템이 시작된 후에만 사용할 수 있습니다. 외부 모니터링 도구를 사용하여 AEM 작동 시간 이상으로 데이터를 유지할 수 있습니다. 자세한 내용은 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">외부 모니터링 도구의 예로 Nagios에 상태 검사를 첨부하기 위한 AEM 설명서입니다</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>관련 로그 항목이란 무엇입니까?</strong></td>
   <td>
    <ul>
     <li>온라인 개정 정리를 시작/중지했습니다.
      <ul>
       <li>온라인 개정 정리 는 다음 세 단계로 구성됩니다. 추정, 압축 및 정리 저장소에 충분한 쓰레기가 포함되어 있지 않으면 압축 및 정리를 건너뛸 수 있습니다. 최신 버전의 AEM에서는 "<code>TarMK GC #{}: estimation started</code>"는 추정의 시작을 표시합니다. "<code>TarMK GC #{}: compaction started, strategy={}</code>"는 압축의 시작을 표시하고 "T<code>arMK GC #{}: cleanup started. Current repository size is {} ({} bytes</code>정리 시작을 표시합니다.</li>
      </ul> </li>
     <li>개정 정리 후 디스크 공간이 확보되었습니다.
      <ul>
       <li>공간은 정리 단계가 완료된 경우에만 재확보됩니다. 정리 단계의 완료는 로그 메시지 "T"로 표시됩니다<code>arMK GC #{}: cleanup completed in {} ({} ms</code>". 사후 정리 크기는 {}({}바이트) 이고 공간 회수 {}({}바이트)입니다. 압축 맵 가중치/깊이는 {}/{}({}바이트/{})입니다.".</li>
      </ul> </li>
     <li>개정 정리 중 문제가 발생했습니다.
      <ul>
       <li>많은 오류 조건이 있으며 모두 "TarMK GC"로 시작하는 WARN 또는 ERROR 로그 메시지로 표시됩니다.</li>
      </ul> </li>
    </ul> <p>또한 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">오류 메시지 기반 문제 해결</a> 섹션을 참조하십시오.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리를 완료한 후 회수된 공간을 확인하는 방법</strong></td>
   <td>정리 주기 종료 시 로그에 메시지가 표시됩니다. "<code>TarMK GC #3: cleanup completed</code>저장소 크기 및 매립된 가비지 양이 포함됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리를 완료한 후 저장소의 무결성을 확인하는 방법</strong></td>
   <td><p>온라인 개정 정리 후에는 저장소 무결성 검사가 필요하지 않습니다. </p> <p>그러나 정리 후 다음 작업을 수행하여 저장소 상태를 확인할 수 있습니다.</p>
    <ul>
     <li>저장소 <a href="/help/sites-deploying/consistency-check.md" target="_blank">순회 검사</a></li>
     <li>정리 프로세스가 완료된 후 oak-run 도구를 사용하여 불일치를 확인합니다. 이 작업을 수행하는 방법에 대한 자세한 내용은 <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache 설명서.</a> 도구를 실행하기 위해 AEM을 종료할 필요가 없습니다.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 실패 여부와 복구할 단계는 어떻게 검색합니까?</strong></td>
   <td>오류 조건은 "TarMK GC"로 시작하는 WARN 또는 ERROR 로그 메시지로 표시됩니다. 또한 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">오류 메시지 기반 문제 해결</a> 섹션을 참조하십시오.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>개정 정리 상태 검사에서 어떤 정보가 표시됩니까? 색상 코딩된 상태 수준에 어떻게, 언제 기여합니까? </strong></td>
   <td><p>개정 정리 상태 확인은 <a href="/help/sites-administering/operations-dashboard.md#health-reports" target="_blank">작업 대시보드</a>.<br /> </p> <p>상태는 다음과 같습니다 <strong>녹색</strong> 온라인 개정 정리 유지 관리 작업의 마지막 실행이 완료된 경우</p> <p>그럴 겁니다 <strong>노란색</strong> 온라인 개정 정리 유지 관리 작업이 한 번 취소된 경우.<br /> </p> <p>그럴 겁니다 <strong>빨간색</strong> 온라인 개정 정리 유지 관리 작업이 연속적으로 3번 취소된 경우 <strong>이 경우 수동 상호 작용이 필요합니다</strong> 또는 온라인 개정 정리 작업이 다시 실패할 수 있습니다. 자세한 내용은 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-online-revision-cleanup">문제 해결</a> 섹션을 참조하십시오.<br /> </p> <p>시스템을 다시 시작한 후 상태 확인 상태가 재설정됩니다. 따라서 새로 다시 시작한 인스턴스는 개정 정리 상태 확인에서 녹색 상태를 표시합니다. 외부 모니터링 도구를 사용하여 AEM 작동 시간 이상으로 데이터를 유지할 수 있습니다. 자세한 내용은 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios">외부 모니터링 도구의 예로 Nagios에 상태 검사를 첨부하기 위한 AEM 설명서입니다</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>대기 인스턴스에서 자동 정리를 모니터링하는 방법</strong></p> </td>
   <td><p>Status, progress 및 statistics는 <code>SegmentRevisionGarbageCollection</code> MBean. 다음을 참조하십시오 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">Oak 설명서</a>. </p> <p>를 사용하여 MBean에 대한 참조를 얻을 수 있습니다. <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code>.</p> <p>통계는 마지막 시스템이 시작된 후에만 사용할 수 있습니다. 외부 모니터링 도구를 사용하여 AEM 작동 시간 이상으로 데이터를 유지할 수 있습니다. 자세한 내용은 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">외부 모니터링 도구의 예로 Nagios에 상태 검사를 첨부하기 위한 AEM 설명서입니다</a>.</p> <p>로그 파일을 사용하여 자동 정리 상태, 진행 상태 및 통계를 확인할 수도 있습니다.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>대기 인스턴스에서 자동 정리 중에 모니터링해야 하는 것은 무엇입니까?</strong></p> </td>
   <td>
    <ul>
     <li>자동 정리를 실행할 때 디스크 공간을 모니터링해야 합니다.</li>
     <li>2시간이 초과되지 않도록 하기 위한 완료 시간(로그를 통해)입니다.</li>
     <li>자동 정리 가 실행된 후의 세그먼트 저장소 크기입니다. 대기 인스턴스에 있는 세그먼트 저장소의 크기는 기본 인스턴스에 있는 세그먼트와 거의 같아야 합니다.</li>
    </ul> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 온라인 개정 정리 문제 해결 {#troubleshooting-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>온라인 개정 정리를 실행하지 않을 경우 발생할 수 있는 최악의 상황은 무엇입니까?</strong></td>
   <td>AEM 인스턴스에 디스크 공간이 부족해져 운영 중단이 발생합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>게시 인스턴스에서 온라인 개정 정리를 실행하는 데 높은 사용자 트래픽이 문제가 됩니까?</strong></td>
   <td>높은 사용자 트래픽은 압축 단계를 성공적으로 완료할 수 있는지 여부에 영향을 줍니다.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>상태 확인 및 로그 항목에 따르면 온라인 개정 정리 작업이 연속적으로 3번 완료되지 않았습니다. 온라인 개정 정리를 성공적으로 완료하려면 무엇이 필요합니까?</strong></td>
   <td>몇 가지 단계를 수행하여 문제를 찾고 수정할 수 있습니다.<br />
    <ul>
     <li>먼저 로그 항목을 확인합니다<br /> </li>
     <li>로그에 있는 정보에 따라 적절한 작업을 수행합니다.
      <ul>
       <li>로그에 5개의 콤팩트 사이클과 시간 제한이 누락된 경우 <code>forceCompact</code> 주기, 저장소 쓰기 양이 적은 경우 유지 관리 기간을 조용한 시간으로 예약합니다. 에 있는 저장소 지표 모니터링 도구에서 저장소 쓰기를 확인할 수 있습니다 <em>https://serveraddress:serverport/libs/granite/operations/content/monitoring/page.html</em></li>
       <li>유지 관리 기간이 끝날 때 정리를 중지한 경우 유지 관리 작업 사용자 인터페이스의 유지 관리 창 구성이 충분한지 확인합니다</li>
       <li>사용 가능한 heap 메모리가 부족한 경우 인스턴스에 충분한 메모리가 있는지 확인하십시오.</li>
       <li>늦게 반응하는 경우, 유지 관리 기간이 더 긴 경우에도 온라인 개정 정리를 완료하기 위해 세그먼트 저장소가 너무 늘어날 수 있습니다. 예를 들어 지난 주에 완료된 온라인 개정 정리를 성공적으로 수행하지 못한 경우 오프라인 유지 관리를 계획하고 세그먼트스토어를 관리하기 쉬운 크기로 다시 가져오기 위해 오프라인 개정 정리를 실행하는 것이 좋습니다.</li>
      </ul> </li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Healthcheck 경고가 켜지면 어떻게 해야 합니까?</strong></td>
   <td>이전 점을 참조하십시오.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>예약된 유지 관리 기간 동안 온라인 개정 정리 시간이 초과되면 어떻게 됩니까?</strong></td>
   <td>온라인 개정 정리 작업이 취소되고 남은 음식은 제거됩니다. 다음에 유지 관리 기간이 예약되면 다시 시작됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>원인 <code>SegmentNotFoundException</code> 로그인할 인스턴스 <code>error.log</code> 어떻게 회복할 수 있죠?</strong></td>
   <td><p>A <code>SegmentNotFoundException</code> 찾을 수 없는 스토리지 유닛(세그먼트)에 액세스하려고 하면 TarMK가 기록합니다. 이 문제를 일으킬 수 있는 세 가지 시나리오가 있습니다.</p>
    <ol>
     <li>권장 액세스 메커니즘(예: Sling 및 JCR API)을 우회하고 하위 수준 API/SPI를 사용하여 저장소에 액세스한 다음 세그먼트의 보존 시간을 초과하는 응용 프로그램입니다. 즉, 온라인 개정 정리(기본적으로 24시간)에서 허용하는 보존 시간보다 엔터티에 대한 참조를 유지합니다. 이 경우는 일시적이며 데이터 손상을 초래하지 않습니다. 복구하려면 oak-run 도구를 사용하여 예외의 임시 특성을 확인해야 합니다(oak-run 확인은 오류를 보고하지 않아야 함). 이렇게 하려면 인스턴스를 오프라인으로 전환하고 나중에 다시 시작해야 합니다.</li>
     <li>외부 이벤트로 인해 디스크의 데이터가 손상되었습니다. 디스크 공간 부족 또는 필요한 데이터 파일을 실수로 수정하는 디스크 오류일 수 있습니다. 이 경우 인스턴스를 오프라인으로 설정하고 oak-run 검사를 사용하여 복구해야 합니다. oak-run 검사를 수행하는 방법에 대한 자세한 내용은 다음을 참조하십시오 <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache 설명서</a>.</li>
     <li>다른 모든 발생 횟수는 <a href="https://helpx.adobe.com/kr/marketing-cloud/contact-support.html" target="_blank">고객 지원 Adobe</a>.</li>
    </ol> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 오류 메시지에 기반한 문제 해결 {#troubleshooting-based-on-error-messages}

온라인 개정 정리 프로세스 중에 사고가 발생하면 error.log가 자세히 표시됩니다. 다음 매트릭스는 가장 일반적인 메시지를 설명하고 가능한 솔루션을 제공하는 것을 목표로 합니다.

<!---| **Phase** |**Log Messages** |**Explanation** |**Next Steps** |
|---|---|---|---|
|   |  |  |  |
| Estimation |TarMK GC #2: estimation skipped because compaction is paused |The estimation phase is skipped when compaction is disabled on the system by configuration. |Enable Online Revision Cleanup. |
|   |TarMK GC #2: estimation interrupted: ${REASON}. Skipping compaction. |The estimation phase terminated prematurely. Some examples of events that could interrupt the estimation phase: not enough memory or disk space on the host system. |Depends on the given reason. |
| Compaction |TarMK GC #2: compaction paused |As long as the compaction phase is paused by configuration, neither the estimation phase nor the compaction phase will be executed. |Enable online revision cleanup. |
|   |TarMK GC #2: compaction cancelled: ${REASON}. |The compaction phase terminated prematurely. Some examples of events that could interrupt the compaction phase: not enough memory or disk space on the host system. Moreover, compaction can also be cancelled by shutting down the system or by explicitly cancelling it via administrative interfaces such as the Maintenance Window within the Operations Dashobard. |Depends on the given reason. |
|   |TarMK GC #2: compaction failed in 32.902 min (1974140 ms), after 5 cycles |This message doesn’t mean that there was an unrecoverable error, but only that compaction was terminated after a certain amount of attempts. Also, read the [following paragraph](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes). |Read the following [Oak documentation](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes), and the last question of the [Running Online Revision Cleanup](/help/sites-deploying/revision-cleanup.md#running-online-revision-cleanup) section. |
| Cleanup |TarMK GC #2: cleanup interrupted |Cleanup has been cancelled by shutting down the repository. No impact on consistency is expected. Also, disk space is most likely not reclaimed to full extent. It will be reclaimed during next revision cleanup cycle. |Investigate why repository has been shut down and going forward try to avoid shutting down the repository during maintenance windows. |-->

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>단계</th>
    <th>로그 메시지</th>
    <th>설명</th>
    <th>다음 단계</th>
  </tr>  
  <tr>
    <td>예측</td>
    <td>TarMK GC #2: 압축이 일시 중지되었으므로 예측을 건너뜁니다.</td>
    <td>구성에 의해 시스템에서 압축이 비활성화된 경우 추정 단계를 건너뜁니다.</td>
    <td>온라인 개정 정리를 활성화합니다.</td>
  </td>
  </tr>
  <tr>
    <td>N/A</td>
    <td>TarMK GC #2: 중단된 항목: ${REASON}. 압축을 건너뜁니다.</td>
    <td>추정 단계가 너무 빨리 종료되었습니다. 추정 단계를 방해할 수 있는 이벤트의 일부 예: 호스트 시스템의 메모리 또는 디스크 공간이 부족합니다.</td>
    <td>주어진 이유에 따라 다릅니다.</td>
  </td>
  </tr>
  <tr>
    <td>압축</td>
    <td>TarMK GC #2: 압축이 일시 중지되었습니다.</td>
    <td>구성 시 압축 단계가 일시 중지된 경우에는 추정 단계와 압축 단계가 실행되지 않습니다.</td>
    <td>온라인 개정 정리를 활성화합니다.</td>
  </td>
  </tr>
   <tr>
    <td>해당 없음</td>
    <td>TarMK GC #2: 압축 취소됨: ${REASON}.</td>
    <td>압축 단계가 너무 빨리 종료되었습니다. 압축 단계를 방해할 수 있는 이벤트의 일부 예: 호스트 시스템의 메모리 또는 디스크 공간이 부족합니다. 또한 시스템을 종료하거나 작업 대시보드 내의 유지 관리 창과 같은 관리 인터페이스를 통해 명시적으로 취소하여 압축 기능을 취소할 수도 있습니다.</td>
    <td>주어진 이유에 따라 다릅니다.</td>
  </td>
  </tr>
  <tr>
    <td>해당 없음</td>
    <td>TarMK GC #2: 5회 후 32.902분(1974140ms)에 압축이 실패했습니다.</td>
    <td>이 메시지는 복구할 수 없는 오류가 있다는 것을 의미하지는 않지만 특정 양의 시도 후에 압축만 종료되었습니다. 또한, <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">다음 단락을 참조하십시오.</a></td>
    <td>다음을 참조하십시오 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">Oak 설명서</a>, 및 온라인 개정 정리 실행 섹션의 마지막 질문입니다.</a></td>
  </td>
  </tr>
  <tr>
    <td>정리</td>
    <td>TarMK GC #2: 정리가 중단되었습니다.</td>
    <td>저장소를 종료하여 정리를 취소했습니다. 일관성에 영향을 주지 않습니다. 또한 디스크 공간은 최대한 복구되지 않을 가능성이 높습니다. 다음 개정 정리 주기 동안 회수됩니다.</td>
    <td>리포지토리가 종료된 이유를 조사하고 앞으로 유지 관리 기간 동안 리포지토리를 종료하지 않도록 합니다.</td>
  </td>
  </tr>
  </tbody>
</table>

## 오프라인 개정 정리 실행 방법 {#how-to-run-offline-revision-cleanup}

>[!CAUTION]
>
>AEM 설치에서 사용하는 Oak 버전에 따라 다른 버전의 Oak-run 도구를 사용해야 합니다. 도구를 사용하기 전에 아래 버전 요구 사항 목록을 확인하십시오.
>
>* Oak 버전용 **1.0.0~1.0.11**&#x200B;또는&#x200B;**1.1.0~1.1.6**, oak-run 버전** 1.0.11** 사용
>
>* Oak 버전용 **위 보다 최신**&#x200B;를 설정하는 경우 AEM 설치의 Oak 코어와 일치하는 Oak-run 버전을 사용합니다.
>


Adobe은 **Oak-run** 을 참조하십시오. 다음 위치에서 다운로드할 수 있습니다.

[https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/)

도구는 리포지토리를 압축하기 위해 수동으로 실행할 수 있는 실행 가능한 jar입니다. 도구를 제대로 실행하려면 리포지토리를 종료해야 하므로 이 프로세스를 오프라인 개정 정리 라고 합니다. 유지 관리 기간에 따라 정리를 계획해야 합니다.

정리 프로세스의 성능을 향상시키는 방법에 대한 팁은 다음을 참조하십시오 [오프라인 개정 정리 성능 향상](/help/sites-deploying/revision-cleanup.md#increasing-the-performance-of-offline-revision-cleanup).

>[!NOTE]
>
>유지 관리가 수행되기 전에 이전 체크포인트를 지울 수도 있습니다(아래 절차의 2단계 및 3단계). 체크포인트가 100개 이상인 인스턴스에만 권장됩니다.

1. 항상 AEM 인스턴스의 최근 백업이 있는지 확인하십시오.

   AEM을 종료합니다.

1. (선택 사항) 도구를 사용하여 이전 체크포인트를 찾습니다.

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore
   ```

1. (선택 사항) 그런 다음 참조되지 않은 체크포인트를 삭제합니다.

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore rm-unreferenced
   ```

1. 압축을 실행하고 완료될 때까지 기다립니다.

   ```xml
   java -jar -Dsun.arch.data.model=32 oak-run.jar compact install-folder/crx-quickstart/repository/segmentstore
   ```

### 오프라인 개정 정리 성능 향상 {#increasing-the-performance-of-offline-revision-cleanup}

oak-run 도구에서는 개정 정리 프로세스의 성능을 높이고 유지 관리 기간을 가능한 한 최소화하려는 몇 가지 기능을 도입합니다.

이 목록에는 아래 설명된 대로 여러 명령줄 매개 변수가 포함되어 있습니다.

* **-mmap.** 이를 true 또는 false로 설정할 수 있습니다. true로 설정하면 메모리 매핑 액세스가 사용됩니다. false로 설정하면 파일 액세스가 사용됩니다. 지정하지 않으면 64비트 시스템에서 메모리 매핑 액세스를 사용하고 32비트 시스템에서 파일 액세스를 사용합니다. Windows에서는 일반 파일 액세스가 항상 적용되며 이 옵션은 무시됩니다. **이 매개 변수는 -Dtar.memoryMapped 매개 변수를 대체했습니다.**

* **-Dupdate.limit**. 임시 트랜잭션 대 디스크 플러시 임계값을 정의합니다. 기본값은 10000입니다.

* **-Decompress-interval**. 현재 맵을 압축할 때까지 유지할 압축 맵 항목 수입니다. 기본값은 1000000입니다. 충분한 heap 메모리를 사용할 수 있는 경우 처리 속도를 높이기 위해 이 값을 더 높은 수로 늘려야 합니다. **이 매개 변수는 Oak 버전 1.6에서 제거되었으며 영향을 주지 않습니다.**

* **-Dcomaction-progress-log**. 기록될 압축 노드 수입니다. 기본값은 150000이며, 이 경우 작업 중에 첫 150000 압축 노드가 기록됩니다. 아래 설명된 다음 매개 변수와 함께 사용합니다.

* **-Dtar.PersistComactionMap을 참조하십시오.** 압축 맵 지속을 위해 heap 메모리 대신 디스크 공간을 사용하려면 이 매개 변수를 true로 설정합니다. oak-run 도구 필요 **버전 1.4** 더 높이 자세한 내용은 [오프라인 개정 정리 FAQ](/help/sites-deploying/revision-cleanup.md#offline-revision-cleanup-frequently-asked-questions) 섹션을 참조하십시오. **이 매개 변수는 Oak 버전 1.6에서 제거되었으며 영향을 주지 않습니다.**

* **- 강제.** 압축을 강제 적용하고 일치하지 않는 세그먼트 저장소 버전을 무시합니다.

>[!CAUTION]
>
>사용 `--force` 매개 변수는 세그먼트 저장소를 이전 Oak 버전과 호환되지 않는 최신 버전으로 업그레이드합니다. 또한 다운그레이드는 불가능합니다. 일반적으로 이러한 매개 변수는 사용하는 방법에 대해 알고 있는 경우에만 주의하고 사용해야 합니다.

사용 중인 매개 변수의 예:

```xml
java -Dupdate.limit=10000 -Dcompaction-progress-log=150000 -Dlogback.configurationFile=logback.xml -Xmx8g -jar oak-run-*.jar checkpoints <repository>
```

### 개정 정리를 트리거하는 추가 방법 {#additional-methods-of-triggering-revision-cleanup}

위에 표시된 방법 외에도 다음과 같이 JMX 콘솔을 사용하여 개정 정리 메커니즘을 트리거할 수도 있습니다.

1. 로 이동하여 JMX 콘솔을 엽니다. [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)
1. 을(를) 클릭합니다. **RevisionGarbageCollection** MBean.
1. 다음 창에서 **startRevisionGC()** 그리고 **호출** 수정 가비지 수집 작업을 시작합니다.

### 오프라인 개정 정리 FAQ {#offline-revision-cleanup-frequently-asked-questions}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>오프라인 개정 정리 기간을 결정하는 요소는 무엇입니까?</strong></td>
   <td><p>정리해야 하는 저장소 크기 및 개정 양이 정리 기간을 결정합니다.</p> </td>
  </tr>
  <tr>
   <td><strong>개정과 페이지 버전 간의 차이점은 무엇입니까?</strong></td>
   <td>
    <ul>
     <li><strong>Oak 개정:</strong> Oak는 노드와 속성으로 구성된 큰 트리 계층 구조로 모든 컨텐츠를 구성합니다. 이 컨텐츠 트리의 각 스냅샷 또는 버전은 변경할 수 없으며 트리 변경 사항은 새로운 수정 버전의 시퀀스로 표시됩니다. 일반적으로 각 콘텐츠 수정은 새 개정을 트리거합니다. 참조 - <a href="https://jackrabbit.apache.org/dev/ngp.html" target="_blank"> 팔로우 링크</a>.</li>
     <li><strong>페이지 버전:</strong> 버전 매기기를 통해 특정 시점의 페이지 "스냅샷"을 만들 수 있습니다. 일반적으로 페이지가 활성화되면 새 버전이 만들어집니다. 자세한 내용은 <a href="/help/sites-authoring/working-with-page-versions.md" target="_blank">페이지 버전 사용</a>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>8시간 이내에 완료되지 않는 경우 오프라인 개정 정리 작업의 속도를 높이는 방법</strong></td>
   <td>수정 작업이 8시간 이내에 완료되지 않고 <a href="/help/sites-administering/operations-dashboard.md#diagnosis-tools" target="_blank">스레드 덤프</a> 주 핫스팟이 <code>InMemoryCompactionMap.findEntry</code>를 채울 때는 oak-run 도구에 다음 매개 변수를 사용하십시오. <strong>버전 1.4 </strong>또는 이상: <code>-Dtar.PersistCompactionMap=true</code>. 다음 사항에 유의하십시오. <code>-Dtar.PersistCompactionMap</code> 매개 변수가 Oak 버전 1.6에서 제거되었습니다.</td>
  </tr>
 </tbody>
</table>
