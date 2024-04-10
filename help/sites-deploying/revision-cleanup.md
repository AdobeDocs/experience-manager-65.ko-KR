---
title: 개정 정리
description: Adobe Experience Manager 6.5에서 개정 정리 기능을 사용하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
feature: Administering
exl-id: e53c4c81-f62e-4b6d-929a-6649c8ced23c
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '5753'
ht-degree: 0%

---

# 개정 정리{#revision-cleanup}

## 소개 {#introduction}

저장소에 대한 각 업데이트는 콘텐츠 개정을 만듭니다. 결과적으로 각 업데이트마다 저장소 크기가 커집니다. 디스크 리소스를 확보하기 위해 이전 버전을 정리해야 합니다. 이는 통제되지 않는 저장소 증가를 방지하기 위해 중요합니다. 이 유지 관리 기능을 개정 정리 라고 합니다. Adobe Experience Manager(AEM) 6.0 이후 오프라인 루틴으로 사용할 수 있습니다.

AEM 6.3 이상에서는 온라인 수정 정리 라는 이 기능의 온라인 버전이 도입되었습니다. AEM 인스턴스를 종료해야 하는 오프라인 개정 정리와 비교하여 온라인 개정 정리는 AEM 인스턴스가 온라인 상태에 있는 동안 실행할 수 있습니다. 온라인 개정 정리는 기본적으로 켜져 있으며 개정 정리를 수행하는 데 권장되는 방법입니다.

**참고**: [비디오 보기](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/administration/use-online-revision-clean-up.html) 소개 및 온라인 개정 정리 사용 방법에 대해 설명합니다.

개정 정리 프로세스는 다음 세 단계로 구성됩니다. **추정치**, **압축**, 및 **정리**. 예상 값은 수집된 가비지 양을 기반으로 다음 단계(압축)를 실행할지 여부를 결정합니다. 압축 단계 세그먼트 및 tar 파일은 사용되지 않은 콘텐츠를 제외하고 다시 작성됩니다. 그런 다음 정리 단계에서는 포함될 수 있는 쓰레기를 포함한 이전 세그먼트를 제거합니다. 오프라인 모드는 추가 세그먼트가 수집되지 않도록 유지하는 AEM 작업 세트를 고려해야 하므로 일반적으로 더 많은 공간을 확보할 수 있습니다.

개정 정리에 대한 자세한 내용은 다음 링크를 참조하십시오.

* [온라인 개정 정리를 실행하는 방법](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)
* [온라인 개정 정리 FAQ](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)
* [오프라인 개정 정리를 실행하는 방법](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup)

또한 다음을 읽을 수 있습니다 [공식 Oak 설명서](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html).

### 오프라인 개정 정리가 아닌 온라인 개정 정리를 사용해야 하는 경우 {#when-to-use-online-revision-cleanup-as-opposed-to-offline-revision-cleanup}

**온라인 개정 정리는 개정 정리를 수행하는 권장 방법입니다.** 오프라인 수정 버전 정리는 예외적인 경우에만 사용해야 합니다. 예를 들어, 새 스토리지 형식으로 마이그레이션하기 전이나 Adobe 고객 지원 센터에서 요청할 경우 사용해야 합니다.

## 온라인 개정 정리를 실행하는 방법 {#how-to-run-online-revision-cleanup}

온라인 개정 정리 는 기본적으로 AEM 작성자 및 게시 인스턴스 모두에서 하루에 한 번 자동으로 실행되도록 구성됩니다. 사용자 활동이 가장 적은 기간 동안 유지 관리 기간을 정의하기만 하면 됩니다. 다음과 같이 온라인 개정 정리 작업을 구성할 수 있습니다.

1. 기본 AEM 창에서 **도구 - 작업 - 대시보드 - 유지 관리** 또는 브라우저가 다음을 가리키도록 합니다. `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 마우스로 가리키기 **일별 유지 관리 창** 을(를) 클릭하고 **설정** 아이콘.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 원하는 값(반복, 시작 시간, 종료 시간)을 입력하고 **저장**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

또는 개정 정리 작업을 수동으로 실행하려면 다음을 수행할 수 있습니다.

1. 다음으로 이동 **도구 - 작업 - 대시보드 - 유지 관리** 또는 을 바로 탐색하여 `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`
1. 다음을 클릭합니다. **일별 유지 관리 창**.
1. 마우스로 가리키기 **개정 정리** 아이콘.
1. 클릭 **실행**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

### 오프라인 개정 정리 후 온라인 개정 정리 실행 {#running-online-revision-cleanup-after-offline-revision-cleanup}

개정 정리 프로세스는 세대별로 오래된 개정을 회수합니다. 즉, 개정 정리를 실행할 때마다 새 생성이 생성되어 디스크에 보관됩니다. 그러나 오프라인 개정 정리가 한 세대를 유지하지만 온라인 개정 정리가 두 세대를 유지한다는 두 가지 개정 정리 유형에는 차이가 있습니다. 따라서 온라인 개정 정리를 실행할 때 **이후** 오프라인 개정 정리 다음 작업이 수행됩니다.

1. 첫 번째 온라인 수정 버전 정리가 실행된 후 저장소 크기는 두 배가 됩니다. 이 문제는 두 세대가 디스크에 저장되기 때문에 발생합니다.
1. 이후 실행 시 저장소는 새 세대가 생성되는 동안 일시적으로 증가하다가 온라인 개정 정리 프로세스가 이전 세대를 재호출함에 따라 첫 번째 실행 후 크기를 다시 유지하면서 안정됩니다.

또한 커밋 유형과 수에 따라 각 세대의 크기가 이전 세대와 비교하여 다를 수 있으므로 최종 크기는 한 실행에서 다른 실행으로 달라질 수 있습니다.

따라서 디스크의 크기를 처음 예상한 저장소 크기보다 최소 2~3배 크게 설정하는 것이 좋습니다.

## 전체 및 꼬리 압축 모드  {#full-and-tail-compaction-modes}

**AEM 6.5** introduces **두 가지 새로운 모드** 대상: **압축** 온라인 개정 정리 프로세스 단계:

* 다음 **완전 압축** 모드는 전체 저장소의 모든 세그먼트와 tar 파일을 재작성합니다. 따라서 이후의 정리 단계에서는 저장소의 최대 가비지 양을 제거할 수 있습니다. 전체 압축은 전체 저장소에 영향을 미치므로 완료하는 데 상당한 시스템 리소스와 시간이 필요합니다. 전체 압축은 AEM 6.3의 압축 단계에 해당합니다.
* 다음 **꼬리 압축** 모드는 저장소의 가장 최근 세그먼트와 tar 파일만 재작성합니다. 가장 최근 세그먼트 및 tar 파일은 마지막으로 전체 또는 테일 압축을 실행한 이후 추가된 파일입니다. 따라서 이후의 정리 단계에서는 저장소의 최근 부분에 포함된 휴지통만 제거할 수 있습니다. 꼬리 압축은 저장소의 일부에만 영향을 주므로 전체 압축보다 시스템 리소스와 완료 시간이 훨씬 적게 필요합니다.

이러한 압축 모드는 효율과 리소스 소비 간의 상충관계를 구성합니다. 테일 압축은 효율성이 떨어지지만 정상적인 시스템 운영에 미치는 영향도 적습니다. 반면 전체 압축은 더 효과적이지만 정상적인 시스템 작동에 더 큰 영향을 미칩니다.

또한 AEM 6.5는 압축 시 더욱 효율적인 콘텐츠 중복 제거 메커니즘을 도입하여 저장소의 디스크 내 풋프린트를 더욱 줄입니다.

아래 두 차트는 AEM 6.3에 비해 AEM 6.5에서 디스크의 평균 실행 시간 및 평균 풋프린트가 감소했음을 보여주는 내부 실험실 테스트 결과를 보여 줍니다.

![onrc-duration-6_4vs63](assets/onrc-duration-6_4vs63.png) ![segmentstore-6_4vs63](assets/segmentstore-6_4vs63.png)

### 전체 및 테일 압축 구성 방법 {#how-to-configure-full-and-tail-compaction}

기본 구성은 평일에는 꼬리 압축을 실행하고 일요일에는 전체 압축을 실행합니다. 새 구성 값을 사용하여 기본 구성을 변경할 수 있습니다 `full.gc.days` / `RevisionCleanupTask` [유지 관리 작업](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup).

을(를) 구성할 때 `full.gc.days` 값, 전체 압축은 값에 정의된 기간 동안 실행되며 테일 압축은 값에 정의되지 않은 기간 동안 실행됩니다. 예를 들어 전체 압축을 일요일에 실행하도록 구성한 경우 꼬리 압축은 월요일에서 토요일까지 실행됩니다. 예를 들어 전체 압축을 구성하여 매일 실행하면 꼬리 압축이 전혀 실행되지 않습니다.

또한 다음 사항을 고려하십시오.

* **꼬리 압축** 효율성이 떨어지고 정상적인 시스템 운영에 미치는 영향이 적습니다. 따라서 영업일 중에 실행되도록 설계되었습니다.
* **전체 압축** 보다 효과적이지만 정상적인 시스템 운영에 더 큰 영향을 미칩니다. 따라서 영업일 외에도 사용하기 위한 것입니다.
* 꼬리 압축과 전체 압축은 모두 사용량이 적은 시간 동안 실행되도록 예약해야 합니다.

### 문제 해결 {#troubleshooting}

새 압축 모드를 사용할 때는 다음 사항에 유의하십시오.

* 입출력 작업, 입출력 대기 CPU, 커밋 대기열 크기와 같은 입출력(I/O) 활동을 모니터링할 수 있습니다. 이렇게 하면 시스템이 I/O에 바인딩되고 있으며 업사이징이 필요한지 여부를 확인하는 데 도움이 됩니다.
* 다음 `RevisionCleanupTaskHealthCheck` 온라인 수정 버전 정리의 전체 상태를 나타냅니다. AEM 6.3에서와 동일한 방식으로 작동하며 전체 압축과 꼬리 압축을 구분하지 않습니다.
* 로그 메시지는 압축 모드에 대한 관련 정보를 전달합니다. 예를 들어, 온라인 개정 정리가 시작되면 해당 로그 메시지는 압축 모드를 나타냅니다. 또한, 경우에 따라 시스템에서 꼬리 압축을 실행하도록 예약되었을 때 전체 압축으로 되돌리고 로그 메시지는 이러한 변경을 나타냅니다. 아래의 로그 샘플은 압축 모드와 꼬리에서 전체 압축으로의 변화를 나타냅니다.

```
TarMK GC: running tail compaction
TarMK GC: no base state available, running full compaction instead
```

### 알려진 제한 사항 {#known-limitations}

경우에 따라 꼬리와 전체 압축 모드를 교대로 하면 정리 프로세스가 지연됩니다. 더 정확하게는 전체 압축 후 저장소가 증가합니다(크기가 두 배 증가). 저장소가 사전 전체 압축 크기 아래로 떨어지면 후속 테일 압축에서 추가 공간이 확보됩니다. 병렬 유지 관리 작업 실행도 피해야 합니다.

**디스크의 크기를 처음 예상한 저장소 크기보다 최소 2~3배 크게 조정하는 것이 좋습니다.**

## 온라인 개정 정리 FAQ {#online-revision-cleanup-frequently-asked-questions}

### AEM 6.5 업그레이드 고려 사항 {#aem-upgrade-considerations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td>질문 </td>
   <td>답변</td>
  </tr>
  <tr>
   <td>AEM 6.5로 업그레이드할 때 알아야 할 사항은 무엇입니까?</td>
   <td><p>TarMK의 지속성 형식은 AEM 6.5에서 변경됩니다. 이러한 변경 사항에는 사전 예방적 마이그레이션 단계가 필요하지 않습니다. 기존 저장소는 사용자에게 투명한 롤링 마이그레이션을 거칩니다. AEM 6.5(또는 관련 도구)가 저장소에 처음 액세스하면 마이그레이션 프로세스가 시작됩니다.</p> <p><strong>AEM 6.5 지속성 형식으로의 마이그레이션이 시작되면 저장소를 이전 AEM 6.3 지속성 형식으로 되돌릴 수 없습니다.</strong></p> </td>
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
   <td><strong>저장소를 마이그레이션해야 하는 이유는 무엇입니까?</strong></td>
   <td><p>AEM 6.3에서는 특히 온라인 수정 버전 정리의 성능과 효과를 개선하기 위해 스토리지 형식을 변경해야 했습니다. 이러한 변경 사항은 이전 버전과 호환되지 않으며, 이전 Oak 세그먼트로 만든 저장소(AEM 6.2 및 이전 버전)를 마이그레이션해야 합니다.</p> <p>스토리지 형식 변경의 추가적인 이점:</p>
    <ul>
     <li>확장성 향상(세그먼트 크기가 최적화됨).</li>
     <li>빠름 <a href="/help/sites-administering/data-store-garbage-collection.md" target="_blank">데이터 저장소 가비지 수집</a>.<br /> </li>
     <li>향후 개선을 위한 기반 작업</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>이전 Tar 포맷은 계속 지원됩니까?</strong></td>
   <td>새 Oak 세그먼트 Tar만 AEM 6.3 이상에서 지원됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>콘텐츠 마이그레이션이 항상 필수입니까?</strong></td>
   <td>예. 새 인스턴스로 시작하지 않으면 항상 콘텐츠를 마이그레이션해야 합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>6.3 이상으로 업그레이드하고 나중에 마이그레이션을 수행할 수 있습니까(예: 다른 유지 관리 기간 사용)?</strong></td>
   <td>아니요, 위에서 설명한 대로 컨텐츠 마이그레이션은 필수입니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>마이그레이션할 때 다운타임을 방지할 수 있습니까?</strong></td>
   <td>아니. 실행 중인 인스턴스에서 수행할 수 없는 일회성 작업입니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>실수로 잘못된 저장소 형식에 대해 를 실행하면 어떻게 됩니까?</strong></td>
   <td>oak-segment-tar 저장소에 대해 oak-segment 모듈을 실행하려고 하면 (또는 반대로) <em>IllegalStateException</em> "잘못된 세그먼트 형식"이라는 메시지가 포함된 경우. 데이터 손상이 발생하지 않습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>검색 색인의 색인 재지정이 필요합니까?</strong></td>
   <td>아니. oak-segment에서 oak-segment-tar로 마이그레이션하면 컨테이너 형식이 변경됩니다. 포함된 데이터는 영향을 받지 않으며 수정되지 않습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>마이그레이션 도중 및 마이그레이션 후에 필요한 예상 디스크 공간을 가장 잘 계산하는 방법</strong></td>
   <td>마이그레이션은 세그먼트 저장소를 새 형식으로 다시 만드는 것과 같습니다. 마이그레이션 중에 필요한 추가 디스크 공간을 예상하는 데 사용할 수 있습니다. 마이그레이션 후 이전 세그먼트 저장소를 삭제하여 공간을 다시 확보할 수 있습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>마이그레이션 기간을 가장 잘 예측하는 방법</strong></td>
   <td>다음과 같은 경우 마이그레이션 성능이 크게 개선될 수 있습니다. <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup">오프라인 개정 정리</a> 은 마이그레이션 전에 실행됩니다. 모든 고객은 업그레이드 프로세스의 전제 조건으로 실행하는 것이 좋습니다. 일반적으로 마이그레이션 전에 오프라인 개정 정리 작업이 실행되었다고 가정할 때 마이그레이션 기간은 오프라인 개정 정리 작업의 기간과 비슷해야 합니다.</td>
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
   <td><strong>온라인 수정 정리 는 얼마나 자주 실행해야 합니까?</strong></td>
   <td>하루에 한 번. 작업 대시보드의 기본 구성입니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 수정 사항 정리 유지 관리 작업의 시작 시간을 구성하려면 어떻게 해야 합니까?</strong></td>
   <td>다음을 참조하십시오. <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">온라인 개정 정리를 실행하는 방법</a> 섹션. </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 수정 버전 정리에 대해 초과해서는 안 되는 최대 빈도가 있습니까?</strong></td>
   <td>기본적으로 구성된 대로 하루에 한 번 온라인 개정 정리를 실행하는 것이 좋습니다.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 수정 버전 정리를 실행해야 하는 빈도를 결정하는 주요 지표는 무엇입니까?</strong></td>
   <td>온라인 수정 정리 가 유지 관리 작업으로 구성되고 매일 자동으로 실행되므로 빈도를 결정할 필요가 없습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 수정 정리 를 처음 실행할 때 공간을 회수하지 않는 이유는 무엇입니까?</strong></td>
   <td>온라인 개정 정리는 세대별로 이전 개정을 회수합니다. 개정 정리가 실행될 때마다 새 생성이 생성됩니다. 최소 2세대 이상 된 콘텐츠만 회수됩니다. 즉, 처음 실행할 때는 회수할 내용이 없습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>오프라인 개정 정리 후 실행할 때 첫 번째 온라인 개정 정리가 공간을 회수하지 않는 이유는 무엇입니까?</strong></td>
   <td><p>오프라인 수정 정리 에서는 온라인 수정 정리에 대해 최신 2세대와 비교하여 최신 세대를 제외한 모든 항목을 회수합니다. 새 저장소가 있는 경우, 오프라인 개정 정리 후 처음으로 실행할 때 회수할 수 있을 만큼 오래된 세대가 없으므로 온라인 개정 정리가 공간을 회수하지 않습니다.</p> <p>또한 의 "오프라인 개정 정리 후 온라인 개정 정리 실행" 섹션을 참조하십시오. <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">이 장</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>일반적으로 작성자와 게시의 온라인 수정 버전 정리 창이 서로 다릅니까?</strong></td>
   <td>이는 근무 시간 및 고객 온라인 존재의 트래픽 패턴에 따라 다릅니다. 유지 관리 기간은 최상의 정리 효과를 위해 기본 제작 시간 외에 구성해야 합니다. 여러 AEM 게시 인스턴스(TarMK 팜)의 경우, 온라인 개정 정리를 위한 유지 관리 창은 서로 엇갈려야 합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리를 실행하기 전에 사전 요구 사항이 있습니까?</strong></td>
   <td><p>온라인 개정 정리 는 AEM 6.3 이상 릴리스에서만 사용할 수 있습니다. 또한 이전 버전의 AEM을 사용하는 경우 새 버전으로 마이그레이션해야 합니다 <a href="/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar">Oak 세그먼트 Tar</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 수정 버전 정리 기간을 결정하는 요소는 무엇입니까?</strong></td>
   <td>요인은 다음과 같습니다.<br />
    <ul>
     <li>저장소 크기</li>
     <li>시스템 로드(분당 요청, 특히 쓰기 작업)</li>
     <li>활동 패턴(읽기 및 쓰기)</li>
     <li>하드웨어 사양(CPU 성능, 메모리, IOPS)</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리가 실행되는 동안 작성자가 계속 작업할 수 있습니까?</strong></td>
   <td>예. 온라인 개정 정리는 동시 쓰기를 처리할 수 있습니다. 그러나 온라인 수정 정리 는 동시 쓰기 트랜잭션 없이 더 빠르고 효율적으로 작동합니다. Adobe은 많은 트래픽이 없는 비교적 조용한 시간으로 온라인 수정 정리 유지 관리 작업을 예약할 것을 권장합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리를 실행할 때 디스크 공간 및 힙 메모리에 대한 최소 요구 사항은 무엇입니까?</strong></td>
   <td><p>온라인 수정 버전 정리 중에 디스크 공간이 계속 모니터링됩니다. 사용 가능한 디스크 공간이 위험 값 미만으로 떨어지면 프로세스가 취소됩니다. 임계값은 저장소의 현재 디스크 풋프린트의 25%이며 구성할 수 없습니다.</p> <p><strong>Adobe은 디스크의 크기를 처음 예상한 저장소 크기보다 최소 2~3배 크게 지정할 것을 권장합니다.</strong></p> <p>사용 가능한 힙 공간은 정리 프로세스 동안 지속적으로 모니터링됩니다. 사용 가능한 힙 공간이 임계값 아래로 떨어지는 경우 프로세스가 취소됩니다. 임계값은 org.apache.jackrabbit.oak.segment.SegmentNodeStoreService#MEMORY_THRESHOLD을 통해 구성됩니다. 기본값은 15%입니다.</p> <p>최소 압축 힙 크기 조정을 위한 Recommendations은 AEM 메모리 크기 조정 권장 사항과 분리되지 않습니다. 일반적으로 <strong>AEM 인스턴스가 사용 사례와 예상 페이로드를 처리할 수 있을 만큼 크기가 조정된 경우 정리 프로세스에서 충분한 메모리를 확보합니다.</strong></p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 수정 정리 를 실행하는 동안 예상되는 성능 영향은 무엇입니까?</strong></td>
   <td>온라인 수정 정리 는 일반적인 시스템 작업과 동시에 저장소에서 읽고 저장소에 쓰는 백그라운드 프로세스입니다. 특히, 짧은 시간 동안 저장소에 단독으로 액세스해야 하므로 다른 스레드가 저장소에 쓸 수 없습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 수정 정리 는 얼마나 오래 실행될 예정입니까?</strong></td>
   <td>내부적으로 수행된 최신 성능 테스트 Adobe에 따라 실행하는 데 2시간 이상 걸리지 않습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리가 더 오래 걸리는 경우 어떻게 해야 합니까?</strong></td>
   <td>
    <ul>
     <li>매일 실행되는지 확인합니다.<br /> </li>
     <li>Operations Dashboard에서 유지 관리 창을 적절하게 구성하여 최소 저장소 활동 중에 실행되도록 합니다.</li>
     <li>시스템 리소스(CPU, 메모리, I/O)를 확장합니다.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리가 구성된 유지 관리 기간을 초과하는 경우 어떻게 됩니까?</strong></td>
   <td>다른 유지 관리 작업이 실행을 지연하지 않는지 확인하십시오. 이 문제는 온라인 개정 정리보다 더 많은 유지 관리 작업이 동일한 유지 관리 창 내에서 실행되는 경우에 발생할 수 있습니다. 유지 관리 작업은 구성 가능한 순서 없이 순차적으로 실행됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>수정 가비지 수집을 건너뛴 이유는 무엇입니까?</strong></td>
   <td><p>수정 정리 는 정리할 쓰레기가 충분한지 여부를 결정하기 위해 추정 단계에 의존합니다. 추정기는 현재 크기를 마지막으로 압축된 저장소의 크기와 비교합니다. 크기가 구성된 델타를 초과하면 정리 가 실행됩니다. 델타 크기는 1GB로 설정됩니다. 즉, 마지막 정리 실행 이후 저장소 크기가 1GB 증가하지 않은 경우 새 개정 정리 반복을 건너뜁니다. </p> <p>다음은 예상 단계에 대한 관련 로그 항목입니다.</p>
    <ul>
     <li>개정 GC 실행: <em>크기 델타는 N% 또는 N/N(N/N 바이트)이므로 압축을 실행합니다.</em></li>
     <li>개정 GC는 <strong>아님</strong> 실행: <em>크기 델타는 N% 또는 N/N(N/N 바이트)이므로 지금은 압축을 건너뜁니다.</em></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>성능 영향이 너무 큰 경우 자동 압축을 안전하게 중단할 수 있습니까?</strong></td>
   <td>예. AEM 6.3부터 작업 대시보드 내의 유지 관리 작업 창 또는 JMX를 통해 안전하게 중지할 수 있습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>예약된 정리 작업 중에 AEM 인스턴스가 종료되면 프로세스가 안전하게 중단됩니까? 또는 압축이 완료될 때까지 종료가 차단됩니까?</strong></td>
   <td>개정 정리가 중단되고 저장소가 안전하게 종료됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 수정 버전 정리 중에 시스템이 충돌하면 어떻게 됩니까?</strong></td>
   <td>이러한 경우 데이터가 손상될 위험이 없습니다. 남은 쓰레기는 다음 실행으로 정리됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 수정 정리 를 실행하지 않으면 어떤 영향이 있습니까?</strong></td>
   <td>시간이 지남에 따라 성능이 저하됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>어떤 수정 사항이 수집되고 있습니까?</strong></td>
   <td>기본적으로 온라인 수정 정리 는 최소 24시간 이상 된 수정 사항만 수집합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>저장소에 동시 쓰기를 너무 많이 하면 어떻게 됩니까?</strong></td>
   <td><p>시스템에 쓰기 동시성이 있는 경우, 온라인 수정 버전 정리에서는 압축 주기의 끝에 변경 사항을 커밋할 수 있는 단독 쓰기 액세스 권한이 필요할 수 있습니다. 시스템이 <strong>forceCompact 모드</strong>에 자세히 설명된 대로 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html" target="_blank">Oak 설명서</a>. 강제 압축 중에 단독 쓰기 잠금을 획득하여 동시 쓰기 간섭 없이 변경 사항을 최종적으로 커밋합니다. 응답 시간에 대한 영향을 제한하기 위해 시간 초과 값을 정의할 수 있습니다. 이 값은 기본적으로 1분으로 설정되어 있습니다. 즉, 강제 압축이 1분 내에 완료되지 않으면 동시 커밋을 위해 압축 프로세스가 중단됩니다.</p> <p>힘 압축 기간은 다음 요인에 따라 다릅니다.</p>
    <ul>
     <li>하드웨어: 특히 IOPS입니다. 지속 시간은 IOPS가 높을수록 줄어듭니다.</li>
     <li>세그먼트 저장소 크기: 기간이 세그먼트 저장소 크기에 따라 늘어납니다.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>대기 인스턴스에서 온라인 개정 정리를 어떻게 실행합니까?</strong></p> </td>
   <td><p>콜드 대기 설정에서 기본 인스턴스만 온라인 개정 정리를 실행하도록 구성해야 합니다. 대기 인스턴스에서는 온라인 개정 정리를 특별히 예약할 필요가 없습니다.</p> <p>대기 인스턴스의 해당 작업은 자동 정리입니다. 이 작업은 온라인 개정 정리의 정리 단계에 해당합니다. 자동 정리는 기본 인스턴스에서 온라인 개정 정리를 실행한 후 대기 인스턴스에서 실행됩니다.</p> <p>예상 및 압축 단계는 대기 인스턴스에서 실행되지 않습니다.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>오프라인 수정 정리 가 온라인 수정 정리 보다 더 많은 디스크 공간을 확보할 수 있습니까?</strong></td>
   <td><p>오프라인 개정 정리는 즉시 이전 개정을 제거할 수 있지만 온라인 개정 정리는 응용 프로그램 스택에서 계속 참조하고 있는 이전 개정을 고려해야 합니다. 전자는 따라서 몇 번의 가비지 수집 주기 동안 효과가 상각되는 후자보다 더 적극적으로 쓰레기를 제거할 수 있습니다.</p> <p>또한 의 "오프라인 개정 정리 후 온라인 개정 정리 실행" 섹션을 참조하십시오. <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">이 장</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>메모리 매핑 파일 작업에 대한 고려 사항은?</td>
   <td>
    <ul>
     <li><strong>Windows 환경에서</strong>에서는 항상 일반 파일 액세스가 적용되므로 메모리 매핑 액세스가 사용되지 않습니다. 일반적인 권고 사항으로 사용 가능한 모든 RAM을 힙에 할당하고 segmentCache 크기를 늘려야 합니다. segmentCache.size 옵션을 org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config(예: segmentCache.size=20480)에 추가하여 segmentCache를 늘립니다. 운영 체제 및 기타 프로세스에 사용할 일부 RAM은 제외해야 합니다.</li>
     <li><strong>비 Windows 환경에서</strong>: 실제 메모리의 크기를 늘려 저장소의 메모리 매핑을 개선합니다.</li>
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
     <li>온라인 개정 정리가 활성화된 경우 디스크 공간을 모니터링해야 합니다. 디스크 공간이 부족하면 정리가 실행되지 않거나 미리 종료됩니다.</li>
     <li>로그에서 온라인 수정 정리 완료 시간을 확인합니다. 2시간 이상 걸리지 않습니다.</li>
     <li>체크포인트 수. 압축이 실행될 때 체크포인트가 3개 이상인 경우 체크포인트를 정리하는 것이 좋습니다.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리가 성공적으로 완료되었는지 확인하는 방법</strong></td>
   <td><p>로그를 확인하여 온라인 개정 정리가 성공적으로 완료되었는지 확인할 수 있습니다.</p> <p>예, "<code>TarMK GC #{}: compaction completed in {} ({} ms), after {} cycles</code>""는 메시지가 선행되지 않는 한 압축 단계가 성공적으로 완료되었음을 의미합니다."<code>TarMK GC #{}: compaction gave up compacting concurrent commits after {} cycles</code>"는 동시 로드가 너무 많음을 의미합니다.</p> <p>이에 따라 다음과 같은 메시지가 있습니다. "<code>TarMK GC #{}: cleanup completed in {} ({} ms</code>"정리 단계를 성공적으로 완료합니다.</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><strong>마지막 온라인 수정 버전 정리 실행의 통계는 어디에서 찾을 수 있습니까?</strong></td>
   <td><p>상태, 진행 상황 및 통계는 JMX(<code>SegmentRevisionGarbageCollection</code> MBean). 에 대한 자세한 내용은 <code>SegmentRevisionGarbageCollection</code> MBean, 다음을 읽습니다. <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">다음 단락</a>.</p> <p>진행률은 다음을 통해 추적할 수 있습니다. <code>EstimatedRevisionGCCompletion</code> 속성 <code>SegmentRevisionGarbageCollection MBean.</code></p> <p>다음을 사용하여 MBean의 참조를 가져올 수 있습니다. <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code>.</p> <p>통계는 마지막 시스템이 시작된 이후에만 사용할 수 있습니다. 외부 모니터링 도구를 사용하여 데이터를 AEM 가동 시간 이상으로 유지할 수 있습니다. 다음을 참조하십시오 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">외부 모니터링 도구의 예로 Nagios에 상태 검사를 첨부하기 위한 AEM 설명서</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>관련 로그 항목이란 무엇입니까?</strong></td>
   <td>
    <ul>
     <li>온라인 개정 정리가 시작됨/중지됨
      <ul>
       <li>온라인 수정 정리 는 예상, 압축 및 정리의 세 단계로 구성됩니다. 예상 값에 저장소에 충분한 쓰레기가 포함되지 않은 경우 압축 및 정리를 건너뛸 수 있습니다. 최신 버전의 AEM에서 "<code>TarMK GC #{}: estimation started</code>"는 추정의 시작을 나타냅니다. "<code>TarMK GC #{}: compaction started, strategy={}</code>압축의 시작을 표시하고 "T<code>arMK GC #{}: cleanup started. Current repository size is {} ({} bytes</code>정리 시작을 표시합니다.</li>
      </ul> </li>
     <li>수정 버전 정리로 인해 디스크 공간이 증가했습니다.
      <ul>
       <li>정리 단계가 완료될 때만 공간이 회수됩니다. 정리 단계 완료는 로그 메시지 "T"로 표시됩니다<code>arMK GC #{}: cleanup completed in {} ({} ms</code>". 사후 정리 크기는 다음과 같습니다. {} ({} 바이트) 및 공간 재확보 {} ({} 바이트)입니다. 압축 맵 두께/깊이: {}/{} ({} 바이트/{})."</li>
      </ul> </li>
     <li>수정 정리 중에 문제가 발생했습니다.
      <ul>
       <li>많은 실패 조건이 있으며, 모든 실패 조건이 "TarMK GC"로 시작하는 WARN 또는 ERROR 로그 메시지로 표시됩니다.</li>
      </ul> </li>
    </ul> <p>또한 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">오류 메시지를 기반으로 한 문제 해결</a> 아래 섹션.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 수정 정리 가 완료된 후 얼마나 많은 공간이 확보되었는지 확인하는 방법</strong></td>
   <td>정리 주기가 끝날 때 로그에 ""라는 메시지가 표시됩니다.<code>TarMK GC #3: cleanup completed</code>저장소 크기 및 회수된 쓰레기 양을 포함합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리가 완료된 후 저장소의 무결성을 확인하는 방법</strong></td>
   <td><p>온라인 개정 정리 후에는 저장소 무결성 검사가 필요하지 않습니다. </p> <p>하지만 정리 후 저장소 상태를 확인하기 위해 다음 작업을 수행할 수 있습니다.</p>
    <ul>
     <li>저장소 <a href="/help/sites-deploying/consistency-check.md" target="_blank">순회 점검</a></li>
     <li>정리 프로세스가 완료된 후 oak-run 도구를 사용하여 불일치를 확인합니다. 이 작업을 수행하는 방법에 대한 자세한 내용은 <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache 설명서.</a> 도구를 실행하기 위해 AEM을 종료할 필요는 없습니다.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 수정 버전 정리가 실패했는지 감지하는 방법 및 복구 단계는 무엇입니까?</strong></td>
   <td>실패 조건은 "TarMK GC"로 시작하는 WARN 또는 ERROR 로그 메시지로 표시됩니다. 또한 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">오류 메시지를 기반으로 한 문제 해결</a> 아래 섹션.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>개정 정리 상태 검사에서 노출되는 정보는 무엇입니까? 색상 코드 상태 수준은 언제 어떻게 기여합니까? </strong></td>
   <td><p>개정 정리 상태 검사는 의 일부입니다. <a href="/help/sites-administering/operations-dashboard.md#health-reports" target="_blank">작업 대시보드</a>.<br /> </p> <p>상태는 입니다. <strong>녹색</strong> 온라인 수정 정리 유지 관리 작업의 마지막 실행이 정상적으로 완료된 경우.</p> <p>다음과 같습니다. <strong>노랑</strong> 온라인 수정 정리 유지 관리 작업이 한 번 취소된 경우.<br /> </p> <p>다음과 같습니다. <strong>빨강</strong> 온라인 수정 정리 유지 관리 작업이 3번 연속으로 취소된 경우 <strong>이 경우 수동 상호 작용이 필요합니다</strong> 또는 온라인 수정 버전 정리가 다시 실패할 수 있습니다. 자세한 내용은 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-online-revision-cleanup">문제 해결</a> 아래 섹션.<br /> </p> <p>또한 시스템을 다시 시작하면 상태 검사 상태가 재설정됩니다. 따라서 새로 시작한 인스턴스는 개정 정리 상태 검사에서 녹색 상태를 표시합니다. 외부 모니터링 도구를 사용하여 데이터를 AEM 가동 시간 이상으로 유지할 수 있습니다. 다음을 참조하십시오 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios">외부 모니터링 도구의 예로 Nagios에 상태 검사를 첨부하기 위한 AEM 설명서</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>대기 인스턴스에서 자동 정리를 모니터링하는 방법</strong></p> </td>
   <td><p>상태, 진행 상황 및 통계는 <code>SegmentRevisionGarbageCollection</code> MBean. 다음을 참조하십시오 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">Oak 설명서</a>. </p> <p>다음을 사용하여 MBean의 참조를 가져올 수 있습니다. <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code>.</p> <p>통계는 마지막 시스템이 시작된 이후에만 사용할 수 있습니다. 외부 모니터링 도구를 사용하여 데이터를 AEM 가동 시간 이상으로 유지할 수 있습니다. 또한 다음을 참조하십시오. <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">외부 모니터링 도구의 예로 Nagios에 상태 검사를 첨부하기 위한 AEM 설명서</a>.</p> <p>로그 파일을 사용하여 자동 정리의 상태, 진행률 및 통계를 확인할 수도 있습니다.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>대기 인스턴스에서 자동 정리 중에 모니터링해야 하는 것은 무엇입니까?</strong></p> </td>
   <td>
    <ul>
     <li>자동 정리가 실행될 때 디스크 공간을 모니터링해야 합니다.</li>
     <li>2시간을 초과하지 않도록 하기 위한 완료 시간(로그를 통해)입니다.</li>
     <li>자동 정리가 실행된 후의 세그먼트 저장소 크기입니다. 대기 인스턴스의 segmentstore 크기는 기본 인스턴스의 segmentstore 크기와 거의 같아야 합니다.</li>
    </ul> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 온라인 개정 정리 문제 해결 {#troubleshooting-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>온라인 수정 정리 를 실행하지 않는 경우 발생할 수 있는 최악의 상황은 무엇입니까?</strong></td>
   <td>AEM 인스턴스의 디스크 공간이 부족하여 프로덕션이 중단될 수 있습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>게시 인스턴스에서 온라인 개정 정리를 실행하는 데 높은 사용자 트래픽이 문제가 됩니까?</strong></td>
   <td>높은 사용자 트래픽은 압축 단계를 성공적으로 완료할 수 있는지 여부에 영향을 줍니다.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>상태 검사 및 로그 항목에 따르면 온라인 수정 정리 가 세 번 연속 완료되지 않았습니다. 온라인 개정 정리를 성공적으로 완료하는 데 필요한 사항은 무엇입니까?</strong></td>
   <td>몇 가지 단계를 수행하여 문제를 찾아 해결할 수 있습니다.<br />
    <ul>
     <li>먼저 로그 항목을 확인합니다<br /> </li>
     <li>로그의 정보에 따라 적절한 조치를 취합니다.
      <ul>
       <li>로그에 누락된 5개의 압축 주기와 시간 제한이 표시되는 경우 <code>forceCompact</code> 저장소 쓰기 양이 적을 때 유지 관리 기간을 조용한 시간으로 예약합니다. 다음 위치에서 저장소 지표 모니터링 도구에서 저장소 쓰기를 확인할 수 있습니다. <em>https://serveraddress:serverport/libs/granite/operations/content/monitoring/page.html</em></li>
       <li>유지 관리 기간이 끝날 때 정리가 중지된 경우 유지 관리 작업 사용자 인터페이스에서 유지 관리 기간의 구성이 충분히 큰지 확인하십시오</li>
       <li>사용 가능한 힙 메모리가 부족한 경우 인스턴스에 충분한 메모리가 있는지 확인합니다.</li>
       <li>지연 반응이 있는 경우 세그먼테이션 스토어가 너무 커져 유지 관리 기간이 더 긴 경우에도 온라인 수정 정리 를 완료할 수 없습니다. 예를 들어 지난 주에 완료된 온라인 개정 정리가 실패한 경우 오프라인 유지 관리를 계획하고 오프라인 개정 정리를 실행하여 세그멘스토어를 관리 가능한 크기로 다시 가져오는 것이 좋습니다.</li>
      </ul> </li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>상태 검사 경고가 켜진 경우 수행해야 하는 작업</strong></td>
   <td>이전 점을 참조하십시오.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>예약된 유지 관리 기간 동안 온라인 개정 정리가 시간 초과되면 어떻게 됩니까?</strong></td>
   <td>온라인 개정 정리가 취소되고 남은 항목이 제거됩니다. 다음 번에 유지 관리 기간이 예약되면 다시 시작됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>원인 <code>SegmentNotFoundException</code> 로그인할 인스턴스 <code>error.log</code> 어떻게 회복할 수 있죠?</strong></td>
   <td><p>A <code>SegmentNotFoundException</code> 는 찾을 수 없는 스토리지 유닛(세그먼트)에 액세스하려고 할 때 TarMK에 의해 기록됩니다. 이 문제를 일으킬 수 있는 세 가지 시나리오가 있습니다.</p>
    <ol>
     <li>권장 액세스 메커니즘(예: Sling 및 JCR API)을 우회하고 하위 수준 API/SPI를 사용하여 저장소에 액세스한 다음 세그먼트의 유지 시간을 초과하는 애플리케이션입니다. 즉, 온라인 개정 정리(기본적으로 24시간)에서 허용하는 보존 시간보다 오래 엔티티에 대한 참조를 유지합니다. 이 경우는 일시적이며 데이터 손상으로 이어지지 않습니다. 복구하려면 oak-run 도구를 사용하여 예외의 일시적인 특성을 확인해야 합니다(oak-run 검사가 오류를 보고하지 않음). 이렇게 하려면 인스턴스를 오프라인 상태로 전환한 후 다시 시작해야 합니다.</li>
     <li>외부 이벤트로 인해 디스크의 데이터가 손상되었습니다. 이는 디스크 장애, 디스크 공간 부족 또는 필요한 데이터 파일의 우발적 수정일 수 있습니다. 이 경우 인스턴스를 오프라인으로 전환하고 oak-run 검사를 사용하여 복구해야 합니다. oak-run 검사를 수행하는 방법에 대한 자세한 내용은 다음을 참조하십시오 <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache 설명서</a>.</li>
     <li>다음을 통해 다른 모든 발생 문제 해결 <a href="https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support" target="_blank">Adobe 고객 지원 센터</a>.</li>
    </ol> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 오류 메시지를 기반으로 한 문제 해결 {#troubleshooting-based-on-error-messages}

온라인 개정 정리 프로세스 중에 문제가 발생하면 error.log가 장황합니다. 다음 매트릭스는 가장 일반적인 메시지를 설명하고 가능한 해결책을 제공하는 것을 목표로 합니다.

<!---| **Phase** |**Log Messages** |**Explanation** |**Next Steps** |
|---|---|---|---|
|   |  |  |  |
| Estimation |TarMK GC #2: estimation skipped because compaction is paused |The estimation phase is skipped when compaction is disabled on the system by configuration. |Enable Online Revision Cleanup. |
|   |TarMK GC #2: estimation interrupted: ${REASON}. Skipping compaction. |The estimation phase terminated prematurely. Some examples of events that could interrupt the estimation phase: not enough memory or disk space on the host system. |Depends on the given reason. |
| Compaction |TarMK GC #2: compaction paused |As long as the compaction phase is paused by configuration, neither the estimation phase nor the compaction phase will be executed. |Enable online revision cleanup. |
|   |TarMK GC #2: compaction cancelled: ${REASON}. |The compaction phase terminated prematurely. Some examples of events that could interrupt the compaction phase: not enough memory or disk space on the host system. Moreover, compaction can also be cancelled by shutting down the system or by explicitly cancelling it via administrative interfaces such as the Maintenance Window within the Operations Dashobard. |Depends on the given reason. |
|   |TarMK GC #2: compaction failed in 32.902 min (1974140 ms), after 5 cycles |This message does not mean that there was an unrecoverable error, but only that compaction was terminated after a certain amount of attempts. Also, read the [following paragraph](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes). |Read the following [Oak documentation](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes), and the last question of the [Running Online Revision Cleanup](/help/sites-deploying/revision-cleanup.md#running-online-revision-cleanup) section. |
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
    <td>예상</td>
    <td>TarMK GC #2: 압축이 일시 중지되었으므로 추정을 건너뛰었습니다.</td>
    <td>구성에 의해 시스템에서 압축을 비활성화하면 예상 단계를 건너뜁니다.</td>
    <td>온라인 개정 정리를 활성화합니다.</td>
  </td>
  </tr>
  <tr>
    <td>해당 사항 없음</td>
    <td>TarMK GC #2: 추정이 중단됨: ${REASON}. 압축을 건너뜁니다.</td>
    <td>예상 단계가 너무 빨리 종료되었습니다. 예상 단계를 방해할 수 있는 이벤트의 일부 예: 호스트 시스템의 메모리 또는 디스크 공간이 부족합니다.</td>
    <td>주어진 이유에 따라 다릅니다.</td>
  </td>
  </tr>
  <tr>
    <td>압축</td>
    <td>TarMK GC #2: 압축이 일시 중지되었습니다.</td>
    <td>구성에 의해 압축 단계가 일시 중지되는 한 추정 단계나 압축 단계가 실행되지 않습니다.</td>
    <td>온라인 개정 정리를 활성화합니다.</td>
  </td>
  </tr>
   <tr>
    <td>해당 사항 없음</td>
    <td>TarMK GC #2: 압축 취소됨: ${REASON}.</td>
    <td>압축 단계가 너무 빨리 종료되었습니다. 압축 단계를 방해할 수 있는 이벤트의 일부 예: 호스트 시스템의 메모리 또는 디스크 공간이 부족합니다. 또한 시스템을 종료하거나 작업 대시보드 내의 유지 관리 창과 같은 관리 인터페이스를 통해 명시적으로 취소하여 압축을 취소할 수도 있습니다.</td>
    <td>주어진 이유에 따라 다릅니다.</td>
  </td>
  </tr>
  <tr>
    <td>해당 사항 없음</td>
    <td>TarMK GC #2: 5사이클 후 32.902분(1974140ms)에 압축이 실패했습니다.</td>
    <td>이 메시지는 복구할 수 없는 오류가 있음을 의미하는 것이 아니라 몇 가지 시도 후 압축이 종료되었음을 의미합니다. 또한 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">다음 단락을 참조하십시오.</a></td>
    <td>다음 내용 읽기 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">Oak 설명서</a>및 온라인 개정 정리 실행 섹션의 마지막 질문입니다.</a></td>
  </td>
  </tr>
  <tr>
    <td>정리</td>
    <td>TarMK GC #2: 정리가 중단되었습니다.</td>
    <td>저장소를 종료하여 정리가 취소되었습니다. 일관성에 영향을 미치지 않을 것으로 예상됩니다. 또한 디스크 공간은 완전히 재확보되지 않을 수 있습니다. 다음 개정 정리 주기 동안 회수됩니다.</td>
    <td>저장소가 종료된 이유를 조사하고 앞으로 유지 관리 기간 동안 저장소를 종료하지 않도록 합니다.</td>
  </td>
  </tr>
  </tbody>
</table>

## 오프라인 개정 정리를 실행하는 방법 {#how-to-run-offline-revision-cleanup}

>[!CAUTION]
>
>AEM 설치의 Oak 코어 버전과 일치하는 버전 번호(주 버전 및 부 버전)가 있는 Oak-run 도구 릴리스를 사용하십시오. 예를 들어 AEM 인스턴스에 Oak 코어 버전 1.22.x가 있는 경우 최신 버전의 Oak-run tool 1.22.x를 사용해야 합니다.

Adobe은 라는 도구를 제공합니다. **Oak-run** 를 클릭하여 개정 버전 정리를 수행합니다. 다음 위치에서 다운로드할 수 있습니다.

[https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/)

이 도구는 수동으로 실행하여 저장소를 압축할 수 있는 실행 가능한 Jar입니다. 도구를 제대로 실행하려면 저장소를 종료해야 하므로 이 프로세스를 오프라인 수정 정리 라고 합니다. 유지 관리 기간에 따라 정리를 계획해야 합니다.

정리 프로세스의 성능을 높이는 방법에 대한 팁은 다음을 참조하십시오. [오프라인 개정 정리 성능 향상](/help/sites-deploying/revision-cleanup.md#increasing-the-performance-of-offline-revision-cleanup).

>[!NOTE]
>
>유지 관리가 수행되기 전에 이전 체크포인트를 지울 수도 있습니다 (아래 절차의 2단계와 3단계). 체크포인트가 100개를 초과하는 인스턴스에만 권장됩니다.

1. AEM 인스턴스의 최근 백업이 있는지 항상 확인하십시오.

   AEM을 종료합니다.

1. (선택 사항) 이전 체크포인트를 찾으려면 도구를 사용합니다.

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

oak-run 도구는 개정 정리 프로세스의 성능을 높이고 유지 관리 기간을 최대한 최소화하려는 몇 가지 기능을 소개합니다.

이 목록에는 아래 설명된 대로 여러 명령줄 매개 변수가 포함되어 있습니다.

* **-mmap.** true 또는 false로 설정할 수 있습니다. true로 설정하면 메모리 매핑 액세스가 사용됩니다. false로 설정하면 파일 액세스가 사용됩니다. 지정하지 않으면 64비트 시스템에서 메모리 매핑 액세스가 사용되고 32비트 시스템에서 파일 액세스가 사용됩니다. Windows에서는 항상 일반 파일 액세스가 적용되며 이 옵션은 무시됩니다. **이 매개 변수는 -Dtar.memoryMapped 매개 변수를 대체했습니다.**

* **-Dupdate.limit**. 디스크에 대한 임시 트랜잭션의 플러시에 대한 임계값을 정의합니다. 기본값은 10000입니다.

* **-Dcompress-interval**. 현재 맵을 압축할 때까지 유지할 압축 맵 항목 수입니다. 기본값은 1000000입니다. 사용 가능한 힙 메모리가 충분하다면 이 값을 더 높은 숫자로 늘려야 더 빠른 처리량을 얻을 수 있습니다. **이 매개 변수는 Oak 버전 1.6에서 제거되었으며 효과가 없습니다.**

* **-Dcompaction-progress-log**. 기록된 압축 노드 수입니다. 기본값은 150000이며, 이는 첫 번째 150000 압축된 노드가 작업 중에 기록됨을 의미합니다. 아래 설명된 다음 매개 변수와 함께 사용하십시오.

* **-Dtar.PersistCompactionMap.** 압축 맵 지속성을 위해 힙 메모리 대신 디스크 공간을 사용하려면 이 매개 변수를 true로 설정합니다. oak-run 도구 필요 **버전 1.4** 및 그 이상 자세한 내용은 의 질문 3을 참조하십시오. [오프라인 개정 정리 FAQ](/help/sites-deploying/revision-cleanup.md#offline-revision-cleanup-frequently-asked-questions) 섹션. **이 매개 변수는 Oak 버전 1.6에서 제거되었으며 효과가 없습니다.**

* **- 강제.** 강제 압축을 적용하고 일치하지 않는 세그먼트 스토어 버전을 무시합니다.

>[!CAUTION]
>
>사용 `--force` 매개 변수는 세그먼트 저장소를 이전 Oak 버전과 호환되지 않는 최신 버전으로 업그레이드합니다. 또한 다운그레이드는 불가능합니다. 일반적으로 이러한 매개 변수는 사용 방법에 대해 잘 알고 있는 경우에만 주의해서 사용해야 합니다.

사용 중인 매개 변수의 예:

```xml
java -Dupdate.limit=10000 -Dcompaction-progress-log=150000 -Dlogback.configurationFile=logback.xml -Xmx8g -jar oak-run-*.jar checkpoints <repository>
```

### 개정 정리를 트리거하는 추가 방법 {#additional-methods-of-triggering-revision-cleanup}

위에 제시된 방법 외에도 다음과 같이 JMX 콘솔을 사용하여 개정 정리 메커니즘을 트리거할 수도 있습니다.

1. 로 이동하여 JMX 콘솔 열기 [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)
1. 다음을 클릭합니다. **RevisionGarbageCollection** MBean.
1. 다음 창에서 다음을 클릭합니다. **startRevisionGC()** 그런 다음 **호출** 를 클릭하여 수정 가비지 수집 작업을 시작합니다.

### 오프라인 개정 정리 FAQ {#offline-revision-cleanup-frequently-asked-questions}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>오프라인 개정 정리 기간을 결정하는 요소는 무엇입니까?</strong></td>
   <td><p>저장소 크기와 정리해야 하는 수정 버전 수에 따라 정리 기간이 결정됩니다.</p> </td>
  </tr>
  <tr>
   <td><strong>수정 버전과 페이지 버전 간의 차이점은 무엇입니까?</strong></td>
   <td>
    <ul>
     <li><strong>Oak 수정 버전:</strong> Oak는 노드 및 속성으로 구성된 큰 트리 계층 구조에서 모든 콘텐츠를 구성합니다. 이 콘텐츠 트리의 각 스냅샷 또는 버전은 변경할 수 없으며, 트리 변경 사항은 새로운 수정 버전의 시퀀스로 표시됩니다. 일반적으로 각 콘텐츠 수정은 새 개정을 트리거합니다. 참조: <a href="https://jackrabbit.apache.org/dev/ngp.html" target="_blank"> 링크 따라가기</a>.</li>
     <li><strong>페이지 버전:</strong> 버전 관리는 특정 시점에 페이지의 "스냅샷"을 만듭니다. 일반적으로 새 버전은 페이지가 활성화될 때 생성됩니다. 자세한 내용은 <a href="/help/sites-authoring/working-with-page-versions.md" target="_blank">페이지 버전 사용</a>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>오프라인 수정 정리 작업이 8시간 이내에 완료되지 않으면 속도를 어떻게 높입니까?</strong></td>
   <td>개정 작업이 8시간 이내에 완료되지 않으면 <a href="/help/sites-administering/operations-dashboard.md#diagnosis-tools" target="_blank">스레드 덤프</a> 기본 핫스팟이 <code>InMemoryCompactionMap.findEntry</code>, oak-run 도구에서 다음 매개 변수를 사용하십시오 <strong>버전 1.4 </strong>이상: <code>-Dtar.PersistCompactionMap=true</code>. 다음 <code>-Dtar.PersistCompactionMap</code> 매개 변수가 Oak 버전 1.6에서 제거되었습니다.</td>
  </tr>
 </tbody>
</table>
