---
title: 개정 정리
seo-title: 개정 정리
description: AEM 6.3에서 개정 정리 기능을 사용하는 방법에 대해 알아봅니다.
seo-description: AEM 6.3에서 개정 정리 기능을 사용하는 방법에 대해 알아봅니다.
uuid: 321f5038-44b0-4f1e-a1aa-2d29074eed70
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: f03ebe60-88c0-4fc0-969f-949490a8e768
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# 개정 정리{#revision-cleanup}

## 소개 {#introduction}

저장소에 대한 각 업데이트는 새 컨텐츠 개정을 만듭니다. 따라서 각 업데이트를 통해 저장소의 크기가 증가합니다. 제어되지 않는 저장소 증가를 방지하려면 디스크 리소스를 무료로 사용할 수 있도록 이전 버전을 정리해야 합니다. 이 유지 관리 기능을 개정 청소라고 합니다. AEM 6.0 이후 오프라인 루틴으로 사용할 수 있습니다.

AEM 6.3에서는 온라인 개정 정리라는 기능의 온라인 버전이 도입되었습니다. AEM 인스턴스를 종료해야 하는 오프라인 개정 정리와 비교하여 AEM 인스턴스가 온라인 상태일 때 온라인 개정 정리가 실행될 수 있습니다. 온라인 개정 정리는 기본적으로 켜져 있으며 개정 정리를 수행하는 권장 방법입니다.

**참고**:온라인 [개정](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/revision-cleanup-technical-video-use.html) 정리 사용 방법에 대한 자세한 내용은 비디오를 참조하십시오.

개정 정리 프로세스는 다음 세 단계로 구성됩니다. **추정**, **합성** 및 **정리**. 추정은 다음 단계(compaction)를 실행할지 또는 수집될 수 있는 가비지 양을 기반으로 하지 않을지를 결정합니다. 구성 단계 세그먼트 및 tar 파일은 사용되지 않은 모든 컨텐츠를 제외하여 다시 작성됩니다. 정리 단계는 이후에 포함할 수 있는 쓰레기를 포함하여 이전 세그먼트를 제거합니다. 오프라인 모드는 추가 세그먼트가 수집되지 않도록 유지하는 AEM의 작업 세트를 고려해야 하기 때문에 일반적으로 더 많은 공간을 재확보할 수 있습니다.

개정 정리에 대한 자세한 내용은 다음 링크를 참조하십시오.

* [온라인 개정 정리 실행 방법](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)
* [온라인 개정 정리 FAQ](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)
* [오프라인 개정 정리 실행 방법](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup)

또한 [공식 Oak 설명서를 읽을 수도 있습니다.](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html)

### 오프라인 개정 정리가 아닌 온라인 개정 정리를 언제 사용해야 합니까? {#when-to-use-online-revision-cleanup-as-opposed-to-offline-revision-cleanup}

**온라인 개정 정리는 개정 정리를 수행하는 권장 방법입니다.** 오프라인 수정 사항은 예외적으로 사용해야 합니다. 예를 들어, 새 스토리지 포맷으로 마이그레이션하기 전이나 Adobe 고객 지원 센터에서 이를 요청해야 합니다.

## 온라인 개정 정리 실행 방법 {#how-to-run-online-revision-cleanup}

온라인 개정 정리는 기본적으로 AEM 작성자 및 게시 인스턴스 모두에서 하루에 한 번 자동으로 실행되도록 구성됩니다. 단, 사용자 활동이 가장 적은 기간 동안 유지 관리 창을 정의하기만 하면 됩니다. 다음과 같이 온라인 개정 정리 작업을 구성할 수 있습니다.

1. 기본 AEM 창에서 도구 - 작업 **- 대시보드 - 유지 관리로** 이동하거나 브라우저에서 다음 작업을 가리킵니다. `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 일별 유지 **관리 창** 위로 마우스를 가져간 후 설정 **아이콘을** 클릭합니다.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 원하는 값(되풀이, 시작 시간, 종료 시간)을 입력하고 저장을 **클릭합니다**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

또는 수정 정리 작업을 수동으로 실행하려면 다음을 수행할 수 있습니다.

1. 도구 **- 작업 - 대시보드 - 유지 관리로** 이동하거나 `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`
1. 일별 유지 **관리 창을 클릭합니다**.
1. 개정 정리 **아이콘을 마우스로 가리키십시오** .
1. 실행을 **클릭합니다**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

### 오프라인 개정 정리 후 온라인 개정 정리 실행 {#running-online-revision-cleanup-after-offline-revision-cleanup}

수정 정리 프로세스는 세대별로 이전 개정을 다시 요구합니다. 즉, 개정 정리를 실행할 때마다 새 생성이 만들어지고 디스크에 유지됩니다. 하지만 두 가지 수정 유형 간에는 차이가 있습니다.오프라인 개정 정리는 한 세대 동안 유지되며 온라인 개정 정리는 두 세대를 유지합니다. 따라서 오프라인 개정 정리 **후** 온라인 개정 정리를 실행하는 경우 다음 사항이 발생합니다.

1. 첫 번째 온라인 개정 정리 실행 후 저장소 크기가 두 배로 증가합니다. 이 문제는 디스크에 저장된 두 세대가 있기 때문에 발생합니다.
1. 이후 실행 동안, 온라인 개정 정리 프로세스가 이전 세대를 재구성하므로, 새로운 세대를 생성하는 동안 저장소가 일시적으로 확장되어 첫 번째 실행 이후에 있던 크기로 안정화됩니다.

또한 커밋의 유형 및 수에 따라 각 생성의 크기가 이전 생성과 비교할 때 달라질 수 있으므로 최종 크기는 한 실행과 다른 실행마다 다를 수 있습니다.

이 때문에, 처음에 예상 저장소 크기보다 최소 2~3배 큰 디스크 크기를 지정하는 것이 좋습니다.

## 전체 및 꼬리 구성 모드 {#full-and-tail-compaction-modes}

**AEM 6.5는** 온라인 개정 정리 프로세스의 **구성** 단계를 위한 **두 가지 새로운 모드를** 제공합니다.

* 전체 **구성** 모드는 전체 저장소의 모든 세그먼트 및 tar 파일을 다시 작성합니다. 이후 정리 단계에서는 저장소 전체에서 최대 가비지 양을 제거할 수 있습니다. 전체 압축은 전체 저장소에 영향을 주므로 상당한 양의 시스템 리소스와 완료 시간이 필요합니다. 전체 구성 요소는 AEM 6.3의 구성 요소에 해당합니다.
* 꼬리 **구성** 모드는 저장소에서 가장 최근 세그먼트와 tar 파일만 다시 기록합니다. 가장 최근 세그먼트와 tar 파일은 전체 또는 세부 구성 요소가 마지막으로 실행된 이후 추가된 파일입니다. 이후 정리 단계에서는 저장소의 최근 부분에만 포함된 쓰레기를 제거할 수 있습니다. 꼬리 구성 요소는 저장소의 일부에만 영향을 주므로 전체 구성 요소보다 시스템 리소스와 완료 시간이 훨씬 적게 필요합니다.

이러한 구성 모드는 효율성과 자원 소비 간의 상쇄 모드를 구성합니다.꼬리 구성 기능은 덜 효과적이지만 정상적인 시스템 운영에도 영향을 주지 않습니다. 반면 전체 구성 요소는 더 효과적이지만 일반적인 시스템 운영에 더 큰 영향을 줍니다.

또한 AEM 6.5는 구성 작업 중에 보다 효율적인 컨텐츠 중복 제거 메커니즘을 도입하여 저장소의 On-Disk 공간을 더욱 줄여줍니다.

아래 두 차트는 AEM 6.3과 비교하여 AEM 6.5에서 평균 실행 시간 단축 및 디스크의 평균 풋프린트 수를 보여주는 내부 실험 결과를 보여줍니다.

![onrc-duration-6_4vs63](assets/onrc-duration-6_4vs63.png)![segmentstore-6_4vs63](assets/segmentstore-6_4vs63.png)

### 전체 및 세부 구성 방법 {#how-to-configure-full-and-tail-compaction}

기본 구성은 주 일마다 세부 작업을 실행하고 일요일에는 전체 구성을 실행합니다. 기본 구성은 `full.gc.days` 유지 관리 작업의 `RevisionCleanupTask` [](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)새 구성 값을 사용하여 변경할 수 있습니다.

값을 구성하면 값에 정의된 일 동안 전체 구성 요소가 실행되고 값에 정의되지 않은 일 동안 세부 구성 요소가 실행됩니다. `full.gc.days` 예를 들어 일요일에 전체 구성 요소를 실행하도록 구성한 경우 월요일에서 토요일까지 종료 추적이 실행됩니다. 예를 들어, 전체 구성 요소가 해당 주의 매일 실행되도록 구성하면 테일 구성 요소가 전혀 실행되지 않습니다.

또한 다음 사항을 고려하십시오.

* **꼬리 구성** 기능은 덜 효과적이며 일반적인 시스템 운영에 미치는 영향이 적습니다. 따라서 영업일 중에 운영될 예정입니다.
* **전체 압축은** 더 효과적이지만 일반적인 시스템 운영에 더 큰 영향을 줍니다. 따라서 영업일 중에 사용하려고 합니다.
* 작업 중지 시간 동안 전체 구성 요소와 함께 실행 일정을 설정해야 합니다.

### 문제 해결 {#troubleshooting}

새로운 구성 모드를 사용할 때는 다음 사항에 유의하십시오.

* 입력/출력(I/O) 활동을 모니터링할 수 있습니다. 예:I/O 작업, CPU IO 대기 중, 큐 크기 커밋 이렇게 하면 시스템이 I/O 바인딩되고 있고 업사이징이 필요한지를 확인할 수 있습니다.
* 이 `RevisionCleanupTaskHealthCheck` 보고서는 온라인 수정 사항의 전체 상태 상태를 나타냅니다. AEM 6.3에서와 동일한 방식으로 작동하며 전체 구성 요소와 꼬리 구성 요소를 구별하지 않습니다.
* 로그 메시지에는 구성 모드에 대한 관련 정보가 들어 있습니다. 예를 들어 온라인 개정 정리가 시작되면 해당 로그 메시지에 구성 모드가 표시됩니다. 또한 일부 경우에 시스템은 테일 구성 작업을 실행하도록 예약되면 전체 구성 요소로 되돌려지며 로그 메시지에 이 변경 사항이 표시됩니다. 아래 로그 샘플은 구성 모드와 테일에서 전체 구성 요소로 변경된 내용을 나타냅니다.

```
TarMK GC: running tail compaction
TarMK GC: no base state available, running full compaction instead
```

### 알려진 제한 사항 {#known-limitations}

경우에 따라 테일 모드와 전체 구성 모드 간에 교대로 인해 정리 프로세스가 지연되기도 합니다. 보다 정확하게, 전체 구성 후 저장소가 확장됩니다(크기가 두 배로 늘어남). 저장소가 전체 사전 구성 크기 아래로 내려갈 때 후속 작업 시 추가 공간이 다시 배치됩니다. 동시 유지 관리 작업 수행도 피해야 합니다.

**디스크 크기를 처음에 예상 저장소 크기보다 최소 2~3배 정도 크게 지정하는 것이 좋습니다.**

## 온라인 개정 정리 FAQ {#online-revision-cleanup-frequently-asked-questions}

### AEM 6.5 업그레이드 고려 사항 {#aem-upgrade-considerations}

<table>
 <tbody>
  <tr>
   <td>질문 </td>
   <td>답변</td>
  </tr>
  <tr>
   <td>AEM 6.5로 업그레이드할 때 알아야 할 사항은 무엇입니까?</td>
   <td><p>TarMK의 지속성 형식은 AEM 6.5에서 변경됩니다.이러한 변경 사항은 사전 예방적 마이그레이션 단계가 필요하지 않습니다. 기존 저장소는 사용자에게 투명한 롤링 마이그레이션을 수행합니다. 마이그레이션 프로세스는 AEM 6.5(또는 관련 도구)가 처음으로 저장소에 액세스하면 시작됩니다.</p> <p><strong>AEM 6.5 지속성 포맷으로의 마이그레이션이 시작되면 저장소를 이전 AEM 6.3 지속성 포맷으로 다시 되돌릴 수 없습니다.</strong></p> </td>
  </tr>
 </tbody>
</table>

### Oak 세그먼트 Tar로 마이그레이션 {#migrating-to-oak-segment-tar}

<table>
 <tbody>
  <tr>
   <td><strong>질문</strong></td>
   <td><strong>답변</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>저장소를 마이그레이션해야 하는 이유는 무엇입니까?</strong></td>
   <td><p>AEM 6.3에서는 특히 온라인 개정 정리의 성능 및 효과를 개선하기 위해 스토리지 포맷에 대한 변경이 필요합니다. 이러한 변경 사항은 이전 버전과 호환되지 않으며, 이전 Oak 세그먼트(AEM 6.2 및 이전)로 만든 리포지토리는 마이그레이션해야 합니다.</p> <p>스토리지 포맷을 변경하면 다음과 같은 추가 이점을 얻을 수 있습니다.</p>
    <ul>
     <li>향상된 확장성(최적화된 세그먼트 크기).</li>
     <li>Faster <a href="/help/sites-administering/data-store-garbage-collection.md" target="_blank">Data Store Garbage Collection</a>.<br /> </li>
     <li>향후 개선을 위한 기본 작업</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>이전 Tar 형식은 여전히 지원됩니까?</strong></td>
   <td>새 Oak 세그먼트 Tar만 AEM 6.3에서 지원됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>컨텐츠 마이그레이션은 항상 필수 사항입니까?</strong></td>
   <td>예. 처음 인스턴스로 시작하지 않으면 항상 컨텐츠를 마이그레이션해야 합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>6.3으로 업그레이드할 수 있으며 나중에 마이그레이션할 수 있습니까(예: 다른 유지 관리 창 사용)?</strong></td>
   <td>아니요, 위에 설명한 바와 같이, 컨텐츠 마이그레이션은 필수입니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>마이그레이션할 때 다운타임을 방지할 수 있습니까?</strong></td>
   <td>아니오. 실행 중인 인스턴스에서 수행할 수 없는 일회성 작업입니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>잘못된 저장소 포맷에 부딪히면 어떻게 됩니까?</strong></td>
   <td>oak-segment-tar 저장소에 대해 oak-segment 모듈을 실행하려고 하면 "잘못된 세그먼트 형식"이라는 메시지와 함께 IllegalState <em>Exception</em> 이 시작되지 않습니다. 데이터 손상이 발생하지 않습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>검색 색인의 재색인이 필요합니까?</strong></td>
   <td>아니오. oak-segment에서 oak-segment-tar로 마이그레이션하면 컨테이너 형식이 변경됩니다. 포함된 데이터는 영향을 받지 않으며 수정되지 않습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>마이그레이션 중 및 후 필요한 예상 디스크 공간을 가장 잘 계산하려면 어떻게 해야 합니까?</strong></td>
   <td>마이그레이션은 세그먼트스토어를 새 형식으로 다시 만드는 것과 같습니다. 마이그레이션 시 필요한 추가 디스크 공간을 계산하는 데 사용할 수 있습니다. 마이그레이션 후 이전 세그먼트 저장소를 삭제하여 공간을 다시 확보할 수 있습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>마이그레이션 지속 시간을 가장 잘 예상하려면 어떻게 해야 합니까?</strong></td>
   <td>마이그레이션 전에 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup">오프라인 개정 정리</a> 작업이 실행되면 마이그레이션 성능이 크게 향상될 수 있습니다. 모든 고객은 업그레이드 프로세스의 사전 요구 사항으로 이를 실행해야 합니다. 일반적으로 마이그레이션 기간은 오프라인 수정 정리 작업이 마이그레이션 전에 실행되었다고 가정할 때 오프라인 개정 정리 작업의 기간과 비슷해야 합니다.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 온라인 개정 정리 실행 {#running-online-revision-cleanup}

<table>
 <tbody>
  <tr>
   <td><strong>질문</strong></td>
   <td><strong>답변</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리는 얼마나 자주 실행되어야 합니까?</strong></td>
   <td>매일 한 번. 작업 대시보드의 기본 구성입니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 유지 관리 작업의 시작 시간을 어떻게 구성할 수 있습니까?</strong></td>
   <td>온라인 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">개정 정리 실행 방법을</a> 참조하십시오. </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리를 위해 초과해서는 안 되는 최대 빈도가 있습니까?</strong></td>
   <td>기본적으로 구성된 대로 하루에 한 번 온라인 개정 정리를 실행하는 것이 좋습니다.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 실행 빈도를 결정하는 주요 지표는 무엇입니까?</strong></td>
   <td>온라인 개정 정리가 유지 관리 작업으로 구성되고 매일 자동으로 실행되므로 빈도를 확인할 필요가 없습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>처음 실행 시 온라인 수정 버전에서 공간을 다시 찾지 못하는 이유는 무엇입니까?</strong></td>
   <td>온라인 개정 정리 기능은 여러 세대에 걸쳐 이전 개정판을 다시 제공합니다. 개정 정리가 실행될 때마다 새로 생성이 생성됩니다. 최소 2세대 이전의 컨텐츠만 재확보됩니다. 즉, 첫 번째 실행에서는 재확보할 필요가 없습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>오프라인 개정 정리 후 실행할 때 첫 번째 온라인 개정 정리가 공간을 다시 확보하지 않는 이유는 무엇입니까?</strong></td>
   <td><p>오프라인 개정 정리 기능은 온라인 개정 정리를 위한 최신 2세대 간의 비교 데이터를 제외하고 모든 것을 회수하고 있습니다. 새 저장소의 경우 오프라인 개정 정리 이후 처음으로 실행될 때 재회수할 수 있는 이전 버전이 없으므로 온라인 개정 정리 기능은 공간을 다시 확보하지 않습니다.</p> <p>또한 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">이 장의</a>"오프라인 개정 정리 후 온라인 개정 정리 실행" 섹션을 참조하십시오.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>작성자 및 게시는 일반적으로 다른 온라인 개정 정리 창을 가지고 있습니까?</strong></td>
   <td>이는 근무 시간과 고객 온라인 프레젠스의 트래픽 패턴에 따라 다릅니다. 유지 관리 기간은 주 제작 시간 외에 구성되어야 최상의 정리 효과를 얻을 수 있습니다. 여러 AEM 게시 인스턴스(TarMK Farm)의 경우 온라인 개정 정리를 위한 유지 관리 기간이 서로 달라져야 합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리를 실행하기 전에 사전 요구 사항이 있습니까?</strong></td>
   <td><p>온라인 개정 정리는 AEM 6.3 이상 릴리스에서만 사용할 수 있습니다. 또한 이전 버전의 AEM을 사용하는 경우 새 Oak 세그먼트 Tar로 마이그레이션해야 <a href="/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar">합니다</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 기간을 결정하는 요인은 무엇입니까?</strong></td>
   <td>요인은 다음과 같습니다.<br />
    <ul>
     <li>저장소 크기</li>
     <li>시스템에 로드(분당 요청, 특히 쓰기 작업)</li>
     <li>활동 패턴(읽기 및 쓰기)</li>
     <li>하드웨어 사양(CPU 성능, 메모리, IOPS)</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리가 실행되는 동안 작성자가 계속 작업할 수 있습니까?</strong></td>
   <td>예. 온라인 개정 정리 기능은 동시 쓰기를 처리할 수 있습니다. 그러나 동시 쓰기 트랜잭션을 수행하지 않고도 온라인 개정 정리 작업을 보다 빠르고 효율적으로 수행할 수 있습니다. 온라인 개정 정리 유지 관리 작업을 많은 트래픽 없이 비교적 조용한 시간으로 예약하는 것이 좋습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 실행 시 디스크 공간 및 더미 메모리의 최소 요구 사항은 무엇입니까?</strong></td>
   <td><p>디스크 공간은 온라인 개정 정리 중에 지속적으로 모니터링됩니다. 사용 가능한 디스크 공간이 중요 값 아래로 떨어지면 프로세스가 취소됩니다. 중요한 값은 현재 저장소 디스크 공간의 25%이며 구성할 수 없습니다.</p> <p><strong>디스크 크기를 처음에 예상 저장소 크기보다 최소 2~3배 정도 크게 지정하는 것이 좋습니다.</strong></p> <p>정리 프로세스 동안 사용 가능한 더미 공간이 지속적으로 모니터링됩니다. 사용 가능한 더미 공간이 중요한 값 아래로 떨어지면 프로세스가 취소됩니다. 중요한 값은 org.apache.jackrabbit.oak.segment.SegmentNodeStoreService#MEMORY_THRESHOLD를 통해 구성됩니다. 기본값은 15%입니다.</p> <p>최소 구성 요소 힙에 대한 권장 사항은 AEM 메모리 크기 조정 권장 사항과 분리되지 않습니다. 일반적인 규칙으로:AEM <strong>인스턴스의 크기가 사용 사례 및 예상되는 페이로드를 처리할 수 있을 만큼 크다면 정리 프로세스는 충분한 메모리를 얻게 됩니다.</strong></p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리를 실행하는 동안 예상되는 성능 영향은 무엇입니까?</strong></td>
   <td>온라인 개정 정리는 일반적인 시스템 작업을 동시에 읽고 저장소에서 쓰는 백그라운드 프로세스입니다. 특히, 다른 스레드가 저장소에 기록되지 않도록 하려면 짧은 시간 동안 저장소에 대한 전용 액세스를 확보해야 할 수 있습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 시간이 얼마나 걸릴 예정입니까?</strong></td>
   <td>Adobe가 내부적으로 수행한 최신 성능 테스트에 따라 실행하는 데 2시간 이상 걸리지 않습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 시간이 더 오래 걸리는 경우 어떻게 해야 합니까?</strong></td>
   <td>
    <ul>
     <li>매일 실행되도록 합니다.<br /> </li>
     <li>Operations Dashboard에서 유지 관리 창을 구성하여 최소한의 저장소 활동 중에 실행되는지 확인합니다.</li>
     <li>시스템 리소스(CPU, 메모리, I/O)를 확장할 수 있습니다.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 작업이 구성된 유지 관리 창을 초과하는 경우 어떻게 됩니까?</strong></td>
   <td>다른 유지 관리 작업이 실행을 지연하지 않도록 하십시오. 동일한 유지 관리 기간 내에 온라인 개정 정리 작업보다 더 많은 유지 관리 작업이 실행되는 경우일 수 있습니다. 유지 관리 작업은 구성 가능한 주문 없이 순차적으로 수행됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>수정 가비지 수집이 생략된 이유는 무엇입니까?</strong></td>
   <td><p>개정 정리는 정리 가능한 쓰레기가 충분한지 결정하기 위해 예측 단계를 따릅니다. 견적 도구는 마지막으로 압축한 후 현재 크기를 저장소 크기와 비교합니다. 크기가 구성된 델타를 초과하면 정리가 실행됩니다. 크기 델타는 1GB로 설정됩니다. 이는 저장소 크기가 마지막 정리 실행 이후 1GB까지 증가하지 않은 경우 새 개정 정리 반복을 건너뜁니다. </p> <p>다음은 추정 단계에 대한 관련 로그 항목입니다.</p>
    <ul>
     <li>수정 버전 GC가 실행됩니다.크기 <em>델타는 N% 또는 N/N(N/N 바이트)이므로 압축 실행</em></li>
     <li>수정 GC가 <strong>실행되지 않습니다</strong> .크기 <em>델타가 N% 또는 N/N(N/N 바이트)이므로 지금 압축 풀기를 건너뜁니다.</em></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>성능 영향이 너무 높을 경우 자동 구현을 안전하게 중단할 수 있습니까?</strong></td>
   <td>예. AEM 6.3부터는 작업 대시보드 내의 유지 관리 작업 창이나 JMX를 통해 안전하게 중지할 수 있습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>예약된 정리 작업 중에 AEM 인스턴스가 종료되는 경우 프로세스가 안전하게 중단됩니까? 아니면 작업이 완료될 때까지 종료가 차단됩니까?</strong></td>
   <td>개정 정리가 중단되고 저장소가 안전하게 종료됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 중에 시스템이 충돌하는 경우 어떻게 됩니까?</strong></td>
   <td>이러한 경우에는 데이터 손상의 위험이 없습니다. 남은 쓰레기는 차후 달려가서 청소한다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리를 실행하지 않으면 어떤 영향이 있습니까?</strong></td>
   <td>시간 경과에 따른 성능 저하</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>어떤 수정 사항이 수집됩니까?</strong></td>
   <td>기본적으로 온라인 개정 정리는 24시간 이상 된 수정만 수집합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>저장소에 동시 쓰기가 너무 많은 경우 어떻게 됩니까?</strong></td>
   <td><p>시스템에 쓰기 동시성이 있는 경우 온라인 개정 정리 시 구성 주기가 끝날 때 변경 사항을 커밋하려면 전용 쓰기 액세스 권한이 필요할 수 있습니다. 시스템은 <strong>oak 설명서에</strong>자세히 설명된 대로 forceCompact 모드로 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html" target="_blank"></a>이동합니다. 강제 축소 작업 중에 동시 쓰기가 방해되지 않고 변경을 최종적으로 수행하기 위해 전용 쓰기 잠금이 획득됩니다. 응답 시간에 대한 영향을 제한하려면 시간 초과 값을 정의할 수 있습니다. 이 값은 기본적으로 1분으로 설정되어 있으므로, 1분 이내에 강제 압축이 완료되지 않으면 동시 커밋을 위해 구성 프로세스가 중단됩니다.</p> <p>힘 축소의 기간은 다음 요인에 따라 다릅니다.</p>
    <ul>
     <li>하드웨어:특히 IOPS 지속 시간은 더 많은 IOPS와 함께 줄어듭니다.</li>
     <li>세그먼트 저장소 크기:지속 시간은 세그먼트 저장소의 크기로 증가합니다.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>대기 인스턴스에서 온라인 개정 정리가 어떻게 실행됩니까?</strong></p> </td>
   <td><p>콜드 대기 설정에서 기본 인스턴스만 온라인 개정 정리를 실행하도록 구성해야 합니다. 대기 인스턴스에서 온라인 개정 정리를 구체적으로 예약할 필요가 없습니다.</p> <p>대기 인스턴스의 해당 작업은 자동 정리(Automatic Cleanup)입니다. 이 작업은 온라인 수정 정리 단계에 해당합니다. 자동 정리는 기본 인스턴스에서 온라인 개정 정리가 실행된 후 대기 인스턴스에서 실행됩니다.</p> <p>예측 및 비교 단계는 대기 인스턴스에서 실행되지 않습니다.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>오프라인 개정 정리 기능이 온라인 개정 정리 수보다 더 많은 디스크 공간을 확보할 수 있습니까?</strong></td>
   <td><p>오프라인 개정 정리 기능은 이전 수정을 즉시 제거할 수 있지만 온라인 개정 정리 기능은 애플리케이션 스택에서 계속 참조되는 이전 개정판을 고려해야 합니다. 따라서 몇 개의 가비지 수집 주기 동안 효과가 완화되는 후자보다 더 공격적으로 가비지를 제거할 수 있습니다.</p> <p>또한 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">이 장의</a>"오프라인 개정 정리 후 온라인 개정 정리 실행" 섹션을 참조하십시오.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>메모리 매핑 파일 작업에 대한 고려 사항이 있습니까?</td>
   <td>
    <ul>
     <li><strong>Windows 환경에서는</strong>메모리 매핑 액세스가 사용되지 않도록 항상 일반 파일 액세스가 적용됩니다. 일반적인 권고 사항으로 사용 가능한 모든 RAM을 힙에 할당해야 하며 segmentCache 크기를 늘려야 합니다. segmentCache.size 옵션을 org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config에 추가하여 segmentCache를 늘립니다(예: segmentCache.size=20480). 운영 체제 및 기타 프로세스에 사용할 RAM을 따로 남겨 두어야 합니다.</li>
     <li><strong>Windows 이외의 환경에서</strong>실제 메모리 크기를 늘려 저장소의 메모리 매핑을 개선합니다.</li>
    </ul> </td>
   <td>
    <ul>
     <li> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 온라인 수정 모니터링 {#monitoring-online-revision-cleanup}

<table>
 <tbody>
  <tr>
   <td><strong>온라인 개정 정리 중에 모니터링해야 할 사항은 무엇입니까?</strong></td>
   <td>
    <ul>
     <li>온라인 개정 정리를 사용하면 디스크 공간을 모니터링해야 합니다. 디스크 공간이 부족할 때 정리가 실행되지 않거나 미리 종료됩니다.</li>
     <li>온라인 개정 정리 완료 시간이 로그를 확인합니다. 2시간 이상 걸리지 않을 겁니다</li>
     <li>체크포인트 수. 구성 요소 실행 시 체크포인트가 3개 이상 있는 경우 체크포인트를 정리하는 것이 좋습니다.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리가 성공적으로 완료되었는지 확인하는 방법</strong></td>
   <td><p>로그를 확인하여 온라인 개정 정리가 성공적으로 완료되었는지 확인할 수 있습니다.</p> <p>예를 들어 "<code>TarMK GC #{}: compaction completed in {} ({} ms), after {} cycles</code>"는 "<code>TarMK GC #{}: compaction gave up compacting concurrent commits after {} cycles</code>"라는 메시지 앞에 오지 않는 한 성공적으로 완료된 구성 단계를 의미하며, 이는 동시 로드가 너무 많다는 것을 의미합니다.</p> <p>그에 따라 정리 단계의 성공적인 완료를 위한 "<code>TarMK GC #{}: cleanup completed in {} ({} ms</code>"라는 메시지가 있습니다.</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><strong>마지막 온라인 개정 정리 실행에 대한 통계는 어디에서 확인할 수 있습니까?</strong></td>
   <td><p>상태, 진행률 및 통계가 JMX(MBean)를 통해<code>SegmentRevisionGarbageCollection</code> 표시됩니다. MBean에 대한 자세한 <code>SegmentRevisionGarbageCollection</code> 내용은 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">다음 단락을</a>참조하십시오.</p> <p>진행 상태는 <code>EstimatedRevisionGCCompletion</code> <code>SegmentRevisionGarbageCollection MBean.</code></p> <p>를 사용하여 MBean의 참조를 얻을 수 <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection”</code>있습니다.</p> <p>통계는 마지막 시스템 시작 후에만 사용할 수 있습니다. 외부 모니터링 도구를 사용하여 AEM 가동 시간 이상으로 데이터를 유지할 수 있습니다. 외부 모니터링 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">도구의</a>예로 Nagios에 상태 확인을 첨부하는 방법은 AEM 설명서를 참조하십시오.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>관련 로그 항목이란 무엇입니까?</strong></td>
   <td>
    <ul>
     <li>온라인 수정 정리 시작/중지
      <ul>
       <li>온라인 개정 정리는 다음 세 단계로 구성됩니다.추정, 압축 및 정리 저장소에 충분한 쓰레기가 포함되어 있지 않으면 추계 시 완료 및 정리 작업을 건너뛸 수 있습니다. 최신 버전의 AEM에서 메시지 "<code>TarMK GC #{}: estimation started</code>"는 추정의 시작을 표시하며 "<code>TarMK GC #{}: compaction started, strategy={}</code>"은 컴포션의 시작을 나타내고 "T"는<code>arMK GC #{}: cleanup started. Current repository size is {} ({} bytes</code>정리 시작을 표시합니다.</li>
      </ul> </li>
     <li>수정 방법으로 확보한 디스크 공간
      <ul>
       <li>공간은 정리 단계가 완료될 때만 재확보됩니다. 정리 단계의 완료를 로그 메시지 "T"로 표시합니다<code>arMK GC #{}: cleanup completed in {} ({} ms</code>. 게시물 정리 크기는 {}({}바이트)이며 {}({}바이트)의 공간을 회수했습니다. 압축 맵 두께/깊이는 {}/{}({} 바이트/{})입니다."</li>
      </ul> </li>
     <li>수정 정리 중 문제가 발생했습니다.
      <ul>
       <li>많은 오류 조건이 있으며, 모두 "TarMK GC"로 시작하는 WARN 또는 ERROR 로그 메시지로 표시됩니다.</li>
      </ul> </li>
    </ul> <p>또한 아래의 오류 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">메시지에 따라 문제 해결</a> 섹션을 참조하십시오.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리가 완료된 후 재확보된 공간을 확인하는 방법?</strong></td>
   <td>정리 주기 끝에 로그에 메시지가 있습니다."<code>TarMK GC #3: cleanup completed</code>" 저장소 크기 및 매립된 가비지의 양을 포함합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리가 완료된 후 저장소의 무결성을 확인하는 방법?</strong></td>
   <td><p>온라인 개정 정리 후에는 저장소 무결성 검사가 필요하지 않습니다. </p> <p>하지만 정리 후 다음 작업을 수행하여 저장소 상태를 확인할 수 있습니다.</p>
    <ul>
     <li>저장소 <a href="/help/sites-deploying/consistency-check.md" target="_blank">탐색 검사</a></li>
     <li>정리 프로세스가 완료된 후 Oak-run 도구를 사용하여 불일치를 확인합니다. 이 방법에 대한 자세한 내용은 Apache 설명서를 <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">참조하십시오.</a> 도구를 실행하기 위해 AEM을 종료하지 않아도 됩니다.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 실패 여부와 복구 단계는 어떻게 검색합니까?</strong></td>
   <td>실패 조건은 "TarMK GC"로 시작하는 WARN 또는 ERROR 로그 메시지로 표시됩니다. 또한 아래의 오류 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">메시지에 따라 문제 해결</a> 섹션을 참조하십시오.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>개정 정리 상태 점검에 표시되는 정보는 무엇입니까? 색상 코딩된 상태 수준에 어떻게 언제 기여할 수 있습니까? </strong></td>
   <td><p>개정 정리 상태 확인은 작업 대시보드의 <a href="/help/sites-administering/operations-dashboard.md#health-reports" target="_blank">일부입니다</a>.<br /> </p> <p>온라인 개정 <strong>정리</strong> 유지 관리 작업의 마지막 실행이 완료되면 상태가 GREEN이 됩니다.</p> <p>온라인 개정 <strong>정리</strong> 유지 관리 작업이 한 번 취소되면 노란색이 됩니다.<br /> </p> <p>온라인 개정 <strong>정리</strong> 유지 관리 작업이 연속해서 3번 취소되면 RED가 됩니다. <strong>이 경우 수동 상호 작용이 필요하거나</strong> 온라인 개정 정리 작업이 다시 실패할 가능성이 높습니다. 자세한 내용은 아래 문제 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-online-revision-cleanup">해결</a> 섹션을 참조하십시오.<br /> </p> <p>시스템을 다시 시작한 후 상태 확인 상태가 재설정됩니다. 따라서 새로 다시 시작한 인스턴스는 개정 정리 상태 확인에 녹색 상태를 표시합니다. 외부 모니터링 도구를 사용하여 AEM 가동 시간 이상으로 데이터를 유지할 수 있습니다. 외부 모니터링 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios">도구의</a>예로 Nagios에 상태 확인을 첨부하는 방법은 AEM 설명서를 참조하십시오.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>대기 인스턴스에서 자동 정리를 모니터링하는 방법</strong></p> </td>
   <td><p>MBean을 사용하여 상태, 진행률 및 통계가 JMX를 통해 <code>SegmentRevisionGarbageCollection</code> 표시됩니다. 다음 Oak <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">설명서를</a>참조하십시오. </p> <p>를 사용하여 MBean의 참조를 얻을 수 <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection”</code>있습니다.</p> <p>통계는 마지막 시스템 시작 후에만 사용할 수 있습니다. 외부 모니터링 도구를 사용하여 AEM 가동 시간 이상으로 데이터를 유지할 수 있습니다. 또한 외부 모니터링 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">도구의</a>예로 Nagios에 상태 확인을 첨부하는 방법은 AEM 설명서를 참조하십시오.</p> <p>로그 파일을 사용하여 자동 정리 상태, 진행 및 통계를 확인할 수도 있습니다.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>대기 인스턴스에서 자동 정리 중에 모니터링해야 할 사항은 무엇입니까?</strong></p> </td>
   <td>
    <ul>
     <li>자동 정리를 실행할 때 디스크 공간을 모니터링해야 합니다.</li>
     <li>2시간이 초과되지 않도록 하기 위한 완료 시간(로그를 통해)</li>
     <li>자동 정리를 실행한 후 세그먼트스토어 크기입니다. 대기 인스턴스에 있는 세그먼트 저장소의 크기는 기본 인스턴스의 크기와 거의 같아야 합니다.</li>
    </ul> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 온라인 수정 문제 해결 {#troubleshooting-online-revision-cleanup}

<table>
 <tbody>
  <tr>
   <td><strong>온라인 개정 정리를 실행하지 않을 경우 발생할 수 있는 최악의 경우는 무엇입니까?</strong></td>
   <td>AEM 인스턴스는 디스크 공간이 부족하여 프로덕션 중단이 발생합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>게시 인스턴스에서 온라인 개정 정리를 실행하는 데 높은 사용자 트래픽이 문제가 됩니까?</strong></td>
   <td>사용자 트래픽이 높으면 구성 단계를 성공적으로 완료할 수 있는지 여부에 영향을 줍니다.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>상태 확인 및 로그 항목에 따르면 온라인 개정 정리가 연속해서 3번 완료되지 않았습니다. 온라인 개정 정리를 성공적으로 완료하려면 무엇이 필요합니까?</strong></td>
   <td>몇 가지 단계를 수행하여 문제를 찾아 수정할 수 있습니다.<br />
    <ul>
     <li>먼저 로그 항목을 확인합니다<br /> </li>
     <li>로그의 정보에 따라 적절한 작업을 수행합니다.
      <ul>
       <li>로그에 5개의 누락된 압축 주기와 <code>forceCompact</code> 주기 시간 초과가 표시되는 경우 저장소 쓰기의 양이 적은 조용한 시간으로 유지 관리 창을 예약합니다. https://serveraddress:serverport/libs/granite/operations/content/monitoring/page.html에 있는 저장소 지표 모니터링 도구에서 리포지토리 쓰기를 확인할 수 <em>있습니다</em></li>
       <li>유지 관리 기간이 끝날 때 정리가 중지되면 유지 관리 작업 사용자 인터페이스에서 유지 관리 창의 구성이 충분히 큰지 확인하십시오</li>
       <li>사용 가능한 더미 메모리가 충분하지 않은 경우 인스턴스에 충분한 메모리가 있는지 확인하십시오.</li>
       <li>늦게 발생하는 반응의 경우, 세그먼트스토어가 너무 많이 증가하여 온라인 개정 정리를 완료하지 못할 수 있습니다. 예를 들어, 지난 주에 완료된 온라인 개정 정리에 성공한 적이 없는 경우 오프라인 유지 관리를 계획하고 세그먼트 저장소를 관리 가능한 크기로 다시 가져오기 위해 오프라인 수정 정리를 실행하는 것이 좋습니다.</li>
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
   <td><strong>예약된 유지 관리 기간 동안 온라인 개정 정리 시간이 부족하면 어떻게 됩니까?</strong></td>
   <td>온라인 개정 정리가 취소되고 남은 음식은 제거됩니다. 다음 번에 유지 관리 기간이 예약되면 다시 시작됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>인스턴스 로그인은 <code>SegmentNotFoundException</code> <code>error.log</code> 무엇이며 어떻게 복구할 수 있습니까?</strong></td>
   <td><p>A <code>SegmentNotFoundException</code> 는 찾을 수 없는 스토리지 장치(세그먼트)에 액세스하려고 할 때 TarMK에 의해 기록됩니다. 다음과 같은 세 가지 시나리오가 있습니다.</p>
    <ol>
     <li>Sling 및 JCR API와 같은 권장 액세스 메커니즘을 우회하고 하위 수준의 API/SPI를 사용하여 저장소에 액세스한 다음 세그먼트의 보존 시간을 초과하는 응용 프로그램입니다. 즉, 엔티티에 대한 참조를 온라인 개정 정리(기본적으로 24시간)에서 허용하는 보존 시간보다 길게 유지합니다. 이러한 경우는 일시적인 현상이며 데이터 손상을 초래하지 않습니다. 복구하려면 Oak-run 도구를 사용하여 예외의 일시적 특성을 확인해야 합니다(Oak-run 검사가 오류를 보고하지 않아야 함). 이렇게 하려면 인스턴스를 오프라인으로 전환하고 나중에 다시 시작해야 합니다.</li>
     <li>외부 이벤트로 인해 디스크의 데이터가 손상되었습니다. 디스크 공간 부족 또는 필요한 데이터 파일의 실수로 수정 작업이 발생할 수 있습니다. 이 경우 인스턴스를 오프라인으로 전환하고 oak-run 검사를 사용하여 복구해야 합니다. oak-run 검사를 수행하는 방법에 대한 자세한 내용은 다음 Apache <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">설명서를</a>참조하십시오.</li>
     <li>다른 모든 경우는 Adobe 고객 지원 센터를 통해 <a href="https://helpx.adobe.com/marketing-cloud/contact-support.html" target="_blank">해결되어야 합니다</a>.</li>
    </ol> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 오류 메시지 기반 문제 해결 {#troubleshooting-based-on-error-messages}

온라인 개정 정리 프로세스 중에 사고가 발생하면 error.log가 자세히 표시됩니다. 다음 매트릭스는 가장 일반적인 메시지를 설명하고 가능한 솔루션을 제공하는 데 목적이 있습니다.

| **위상** | **로그 메시지** | **설명** | **다음 단계** |
|---|---|---|---|
|  |  |  |  |
| 추정 | TarMK GC #2:컴포지션이 일시 중지되어 예측을 건너뛰었습니다. | 구성에 따라 시스템에서 구성 요소가 비활성화되면 예측 단계를 건너뜁니다. | 온라인 개정 정리 사용을 참조하십시오. |
|  | TarMK GC #2:중단된 항목:${REASON}. 구성 요소를 건너뛰는 중입니다. | 예측 단계가 너무 일찍 종료되었습니다. 예측 단계를 방해할 수 있는 이벤트의 일부 예:호스트 시스템의 메모리 또는 디스크 공간이 부족합니다. | 주어진 이유에 따라 다릅니다. |
| Compaction | TarMK GC #2:컴포지션이 일시 중지됨 | 구성 단계에서 구성 단계를 일시 중지하면 예측 단계와 비교 단계가 실행되지 않습니다. | 온라인 개정 정리를 활성화합니다. |
|  | TarMK GC #2:comaction 취소됨:${REASON}. | 압축 단계가 너무 빨리 종료되었습니다. 구성 단계를 방해할 수 있는 이벤트의 일부 예:호스트 시스템의 메모리 또는 디스크 공간이 부족합니다. 또한 시스템을 종료하거나 작업 대시보드 내의 유지 관리 창과 같은 관리 인터페이스를 통해 명시적으로 취소하면 컴포션을 취소할 수 있습니다. | 주어진 이유에 따라 다릅니다. |
|  | TarMK GC #2:5회 후 32.902분(1974140ms)에 컴포션이 실패했습니다. | 이 메시지는 복구할 수 없는 오류가 있는 것은 아니지만 특정 시도 횟수 후에 압축이 종료된 것을 의미합니다. 또한 [다음 단락을](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes)읽으십시오. | 다음 Oak [설명서와](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes)Running Online Revision Cleanup [섹션의 마지막 질문을](/help/sites-deploying/revision-cleanup.md#running-online-revision-cleanup) 참조하십시오. |
| 정리 | TarMK GC #2:정리 중단 | 저장소를 종료하여 정리가 취소되었습니다. 일관성에 영향을 주지 않습니다. 또한 디스크 공간이 완전히 재확보되지 않을 가능성이 높습니다. 다음 개정 정리 주기 동안 복구됩니다. | 저장소가 종료된 이유를 조사하고 유지 관리 기간 동안 저장소를 종료하지 않도록 합니다. |

## 오프라인 개정 정리 실행 방법 {#how-to-run-offline-revision-cleanup}

>[!CAUTION]
>
>AEM 설치 시 사용하는 Oak 버전에 따라 다른 버전의 Oak 실행 도구를 사용해야 합니다. 도구를 사용하기 전에 아래 버전 요구 사항 목록을 확인하십시오.
>
>* Oak 버전 **1.0.0 - 1.0.11**&#x200B;또는&#x200B;**1.1.0 - 1.1.6**&#x200B;의 경우 Oak-run 버전** 1.0.11*
   >
   >
* Oak 버전의 **경우** AEM 설치의 Oak 코어와 일치하는 Oak 실행 버전을 사용하십시오.
>



Adobe는 개정 정리를 수행하기 **위해 Oak-run** 이라는 도구를 제공합니다. 다음 위치에서 다운로드할 수 있습니다.

[https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/)

이 도구는 저장소를 압축하기 위해 수동으로 실행할 수 있는 실행 가능한 jar입니다. 도구를 제대로 실행하려면 저장소를 종료해야 하므로 이 프로세스를 오프라인 개정 정리 방식이라고 합니다. 유지 관리 창에 따라 정리를 계획하십시오.

정리 프로세스의 성능을 높이는 방법에 대한 팁은 오프라인 수정 [성능 향상을 참조하십시오](/help/sites-deploying/revision-cleanup.md#increasing-the-performance-of-offline-revision-cleanup).

>[!NOTE]
>
>유지 관리가 수행되기 전에 이전 체크포인트를 지울 수도 있습니다(아래 절차의 2단계 및 3단계). 체크포인트가 100개가 넘는 인스턴스에만 권장됩니다.

1. 항상 AEM 인스턴스의 최근 백업이 있는지 확인합니다.

   AEM을 종료합니다.

1. (선택 사항) 도구를 사용하여 이전 체크포인트를 찾습니다.

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore
   ```

1. (선택 사항) 참조되지 않은 체크포인트를 삭제합니다.

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore rm-unreferenced
   ```

1. 구성 요소를 실행하고 완료될 때까지 기다립니다.

   ```xml
   java -jar -Dsun.arch.data.model=32 oak-run.jar compact install-folder/crx-quickstart/repository/segmentstore
   ```

### 오프라인 개정 정리 성능 향상 {#increasing-the-performance-of-offline-revision-cleanup}

Oak-run 툴은 수정 과정 성능을 높이고 유지 관리 기간을 최대한 최소화하기 위한 몇 가지 기능을 제공합니다.

목록에는 아래 설명된 대로 몇 가지 명령줄 매개 변수가 포함되어 있습니다.

* **-mmap.** 이 값을 true 또는 false로 설정할 수 있습니다. true로 설정하면 메모리 매핑 액세스가 사용됩니다. false로 설정하면 파일 액세스가 사용됩니다. 지정하지 않을 경우 메모리 매핑 액세스는 64비트 시스템에서 사용되고 파일 액세스는 32비트 시스템에서 사용됩니다. Windows에서는 일반 파일 액세스가 항상 적용되며 이 옵션은 무시됩니다. **이 매개 변수는 -Dtar.memoryMapped 매개 변수를 대체했습니다.**

* **-Dupdate.limit**. 디스크에 임시 트랜잭션 플러시의 임계값을 정의합니다. 기본값은 10000입니다.

* **-압축 간격**. 현재 맵을 압축할 때까지 유지할 컴포지션 맵 항목의 수입니다. 기본값은 1000000입니다. You should increase this value to an even higher number for faster throughput, if enough heap memory is available. **이 매개 변수는 Oak 버전 1.6에서 제거되었으며 아무런 영향을 주지 않습니다.**

* **-Dcompaction-progress-log**. 기록할 호환 노드의 수입니다. 기본값은 150000입니다. 즉, 작업 중에 처음 15000 호환 노드가 기록됩니다. 아래 설명된 다음 매개 변수와 함께 사용하십시오.

* **-Dtar.PersistCompactionMap.** compaction 맵 지속 시 더미 메모리 대신 디스크 공간을 사용하려면 이 매개 변수를 true로 설정합니다. Oak 실행 도구 **버전 1.4** 이상이 필요합니다. 자세한 내용은 오프라인 개정 정리 FAQ [섹션에서 질문 3을](/help/sites-deploying/revision-cleanup.md#offline-revision-cleanup-frequently-asked-questions) 참조하십시오. **이 매개 변수는 Oak 버전 1.6에서 제거되었으며 아무런 영향을 주지 않습니다.**

* **—force.** 강제 압축 및 일치하지 않는 세그먼트 저장소 버전을 무시합니다.

>[!CAUTION]
>
>이 `--force` 매개 변수를 사용하면 세그먼트 스토어가 이전 Oak 버전과 호환되지 않는 최신 버전으로 업그레이드됩니다. 또한 다운그레이드는 불가능하다는 것을 고려하십시오. 일반적인 규칙으로, 이러한 매개 변수를 사용하는 방법에 대해 알고 있는 경우에만 주의해서 사용해야 합니다.

사용 중인 매개 변수의 예:

```xml
java -Dupdate.limit=10000 -Dcompaction-progress-log=150000 -Dlogback.configurationFile=logback.xml -Xmx8g -jar oak-run-*.jar checkpoints <repository>
```

### 개정 정리 트리거 추가 방법 {#additional-methods-of-triggering-revision-cleanup}

위에서 설명한 방법 외에도 다음과 같이 JMX 콘솔을 사용하여 수정 메커니즘을 시작할 수 있습니다.

1. http://localhost:4502/system/console/jmx으로 이동하여 JMX 콘솔을 [엽니다](http://localhost:4502/system/console/jmx)
1. RevisionGarbageCollection **MBean을** 클릭합니다.
1. 다음 창에서 startRevisionGC() **를** 클릭한 다음 **호출** 을 클릭하여 수정 가비지 수집 작업을 시작합니다.

### 오프라인 개정 정리 FAQ {#offline-revision-cleanup-frequently-asked-questions}

<table>
 <tbody>
  <tr>
   <td><strong>오프라인 개정 정리 시간을 결정하는 요인은 무엇입니까?</strong></td>
   <td><p>저장소 크기 및 정리해야 하는 개정안의 양에 따라 정리 시간이 결정됩니다.</p> </td>
  </tr>
  <tr>
   <td><strong>개정과 페이지 버전의 차이는 무엇입니까?</strong></td>
   <td>
    <ul>
     <li><strong></strong> Oak 개정:Oak는 노드 및 속성으로 구성된 큰 트리 계층 구조의 모든 컨텐츠를 구성합니다. 이 컨텐츠 트리의 각 스냅샷 또는 개정은 변경할 수 없으며 트리 변경 사항은 새로운 수정 사항의 시퀀스로 표시됩니다. 일반적으로 각 컨텐츠 수정은 새 개정을 트리거합니다. 팔로우 <a href="https://jackrabbit.apache.org/dev/ngp.html" target="_blank"> 링크도</a>참조하십시오.</li>
     <li><strong></strong> 페이지 버전:버전 매기기를 통해 특정 시점의 페이지 "스냅샷"을 만들 수 있습니다. 일반적으로 페이지가 활성화되면 새 버전이 만들어집니다. 자세한 내용은 페이지 버전 <a href="/help/sites-authoring/working-with-page-versions.md" target="_blank">작업을 참조하십시오</a>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>8시간 이내에 완료되지 않으면 오프라인 개정 정리 작업의 속도를 높이는 방법</strong></td>
   <td>수정 작업이 8시간 내에 완료되지 않고 <a href="/help/sites-administering/operations-dashboard.md#diagnosis-tools" target="_blank">스레드 덤프가</a> 기본 핫스팟이 <code>InMemoryCompactionMap.findEntry</code>있음을 나타내는 경우, oak-run 도구 <strong>버전 1.4 </strong>이상에서 다음 매개 변수를 사용하십시오. <code>-Dtar.PersistCompactionMap=true</code>Adobe Oak 버전 1.6에서는 매개 변수가 <code>-Dtar.PersistCompactionMap</code> 제거되었습니다.</td>
  </tr>
 </tbody>
</table>

