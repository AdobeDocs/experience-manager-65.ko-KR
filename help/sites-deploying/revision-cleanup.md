---
title: 개정 정리
seo-title: 개정 정리
description: AEM 6.3에서 수정 버전 정리 기능을 사용하는 방법을 알아봅니다.
seo-description: AEM 6.3에서 수정 버전 정리 기능을 사용하는 방법을 알아봅니다.
uuid: 321f5038-44b0-4f1e-a1aa-2d29074eed70
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: f03ebe60-88c0-4fc0-969f-949490a8e768
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6
workflow-type: tm+mt
source-wordcount: '5916'
ht-degree: 0%

---


# 개정 정리{#revision-cleanup}

## 소개 {#introduction}

저장소의 각 업데이트는 새 컨텐츠 개정을 만듭니다. 따라서 각 업데이트를 통해 저장소의 크기가 증가합니다. 저장소 증가를 제어하지 않으려면 기존 수정 내용을 무료 디스크 리소스로 정리해야 합니다. 이 유지 관리 기능을 수정 기능이라고 합니다. AEM 6.0부터 오프라인 루틴으로 이용할 수 있습니다.

AEM 6.3에서는 온라인 개정 정리라는 이 기능의 온라인 버전이 도입되었습니다. AEM 인스턴스가 종료되어야 하는 오프라인 개정 정리 기능과 비교하여 AEM 인스턴스가 온라인 상태일 때 온라인 개정 정리를 실행할 수 있습니다. 온라인 개정 정리는 기본적으로 설정되어 있으며, 개정 정리를 수행하는 권장되는 방법입니다.

**참고**: [온라인 ](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/revision-cleanup-technical-video-use.html) 개정 정리 사용 방법에 대한 자세한 내용은 비디오를 참조하십시오.

개정 정리 프로세스는&#x200B;**예측**, **compaction** 및 **정리**. 추정은 다음 단계(구성)를 실행할지 또는 수집할 수 있는 가비지 양을 기반으로 하지 않을지를 결정합니다. 비교 단계 중 세그먼트 및 tar 파일은 사용하지 않는 콘텐트를 제외하도록 다시 작성됩니다. 이후 정리 단계에서는 포함할 수 있는 쓰레기를 포함하여 이전 세그먼트를 제거합니다. 온라인 모드는 추가 세그먼트를 수집하지 않는 AEM 작업 세트를 고려해야 하기 때문에 오프라인 모드는 일반적으로 더 많은 공간을 재확보할 수 있습니다.

개정 정리에 대한 자세한 내용은 다음 링크를 참조하십시오.

* [온라인 개정 정리 실행 방법](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)
* [온라인 개정 정리 FAQ](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)
* [오프라인 개정 정리 실행 방법](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup)

또한 [공식 Oak 설명서를 읽을 수도 있습니다.](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html)

### 오프라인 개정 정리와 대조하여 온라인 개정 정리를 사용하는 경우{#when-to-use-online-revision-cleanup-as-opposed-to-offline-revision-cleanup}

**온라인 개정 정리는 개정 정리를 수행하는 권장되는 방법입니다.** 오프라인 수정 사항 정리는 새 스토리지 포맷으로 마이그레이션하기 전이나 Adobe 고객 지원 센터에서 요청하여 사용해야 하는 경우 예외적으로 사용해야 합니다.

## 온라인 개정 정리 실행 방법 {#how-to-run-online-revision-cleanup}

온라인 개정 정리 기능은 기본적으로 AEM 작성자 및 게시 인스턴스 모두에서 하루에 한 번 자동으로 실행되도록 구성되어 있습니다. 단, 사용자 활동이 가장 적은 기간 동안 유지 관리 창을 정의하기만 하면 됩니다. 다음과 같이 온라인 개정 정리 작업을 구성할 수 있습니다.

1. 주 AEM 창에서 **도구 - 작업 - 대시보드 - 유지 관리**&#x200B;로 이동하거나 브라우저를 다음과 같이 지정합니다.`https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. **일일 유지 관리 창** 위로 마우스를 가져간 후 **설정** 아이콘을 클릭합니다.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 원하는 값(되풀이, 시작 시간, 종료 시간)을 입력하고 **저장**&#x200B;을 클릭합니다.

   ![chlimage_1-92](assets/chlimage_1-92.png)

또는 개정 정리 작업을 수동으로 실행하려면 다음을 수행할 수 있습니다.

1. **도구 - 작업 - 대시보드 - 유지 관리**&#x200B;로 이동하거나 `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`로 바로 이동합니다.
1. **일일 유지 관리 창**&#x200B;을 클릭합니다.
1. **개정 정리** 아이콘 위로 마우스를 가져갑니다.
1. **실행**&#x200B;을 클릭합니다.

   ![chlimage_1-93](assets/chlimage_1-93.png)

### 오프라인 개정 정리 후 온라인 개정 정리 실행 {#running-online-revision-cleanup-after-offline-revision-cleanup}

수정 정리 프로세스는 세대별로 이전 개정을 다시 처리합니다. 즉, 개정 정리를 실행할 때마다 새 생성이 만들어지고 디스크에 보존됩니다. 하지만 두 가지 수정 유형 간에는 차이가 있습니다.오프라인 개정 정리는 한 세대를 유지하고 온라인 개정 정리는 2대를 유지합니다. 따라서 온라인 개정 정리 **after** 오프라인 개정 정리를 실행하면 다음과 같은 결과가 발생합니다.

1. 첫 번째 온라인 개정 정리 실행 후 저장소 크기가 두 배로 증가합니다. 이는 디스크에 2대가 남아 있기 때문입니다.
1. 온라인 개정 정리 프로세스가 이전 세대를 재해석함에 따라, 이후 실행 중에 저장소는 새로운 세대를 생성한 후 첫 번째 실행 이후에 있던 크기로 안정화하면서 일시적으로 증가합니다.

또한, 커밋의 유형 및 수에 따라 각 생성은 이전 생성과 비교하여 크기에 따라 달라질 수 있으므로 최종 크기는 한 실행과 다른 실행마다 다를 수 있습니다.

이 때문에 디스크를 처음에 예상 저장소 크기보다 최소 2~3배 더 크게 크기를 지정하는 것이 좋습니다.

## 전체 및 꼬리 구성 모드 {#full-and-tail-compaction-modes}

**AEM 6.5** 는 온라인 개정  **정리 프로세스의**   **** 구성 단계를 위한 두 가지 새로운 모델을 제공합니다.

* **전체 구성 요소** 모드는 전체 저장소의 모든 세그먼트 및 tar 파일을 다시 작성합니다. 이후 정리 단계에서는 저장소 전체에서 최대 가비지 양을 제거할 수 있습니다. 전체 압축은 전체 저장소에 영향을 주므로 상당한 양의 시스템 리소스와 완료 시간이 필요합니다. 전체 구성 요소는 AEM 6.3의 컴포지션 단계에 해당합니다.
* **꼬리 구성** 모드는 저장소의 최신 세그먼트와 tar 파일만 다시 기록합니다. 가장 최근 세그먼트와 tar 파일은 전체 또는 세부 구성 요소가 마지막으로 실행된 이후 추가된 파일입니다. 이후 정리 단계는 따라서 저장소의 최근 부분에 포함된 쓰레기만 제거할 수 있습니다. 꼬리 구성 요소는 저장소의 부분에만 영향을 주므로 전체 구성 요소보다 시스템 리소스와 완료 시간이 훨씬 적게 필요합니다.

이러한 구성 모드는 효율성과 자원 소비 간의 상쇄 효과를 구성합니다.꼬리 구성 기능은 덜 효과적이지만 정상적인 시스템 작동에 미치는 영향도 줄어듭니다. 반면 전체 구성 요소는 더 효과적이지만 정상적인 시스템 운영에 더 큰 영향을 줍니다.

또한 AEM 6.5는 구성 작업 시 보다 효율적인 컨텐츠 중복 제거 메커니즘을 도입하여 저장소의 디스크 공간 감소를 더욱 줄입니다.

아래 두 차트에서 AEM 6.3과 비교하여 AEM 6.5에서 평균 실행 시간과 디스크의 평균 풋프린트를 보여주는 내부 실험 결과를 소개합니다.

![onrc-duration-6_4vs63](assets/onrc-duration-6_4vs63.png) ![segmentstore-6_4vs63](assets/segmentstore-6_4vs63.png)

### 전체 및 세부 구성 요소 구성 방법 {#how-to-configure-full-and-tail-compaction}

기본 구성은 주 일마다 세부 작업을 실행하고 일요일에는 전체 구성을 실행합니다. 기본 구성은 `RevisionCleanupTask` [유지 관리 작업](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)의 새 구성 값 `full.gc.days`을 사용하여 변경할 수 있습니다.

`full.gc.days` 값을 구성하면 값 및 테일 컴포지션에 정의된 일 동안 전체 컴포지션이 실행된다는 점을 알고 있어야 합니다. 예를 들어 일요일에 전체 구성 요소를 실행하도록 구성한 경우 월요일부터 토요일까지 후속 작업이 실행됩니다. 예를 들어, 전체 컴포지션을 각 주의 매일 실행하도록 구성하면 테일 컴포지션이 전혀 실행되지 않습니다.

또한 다음 사항을 고려하십시오.

* **꼬리** 구성 요소는 덜 효과적이며 일반적인 시스템 운영에 미치는 영향은 더 적습니다. 따라서 영업일 중에 운영되도록 되어 있다.
* **전체** 구성 요소는 더 효과적이지만 정상적인 시스템 운영에 더 큰 영향을 줍니다. 따라서 영업일 중에 사용되도록 되어 있다.
* 꼬리 구성 요소와 전체 구성 요소는 사용량이 적은 시간에 실행되도록 예약해야 합니다.

### 문제 해결 {#troubleshooting}

새로운 구성 모드를 사용할 때는 다음 사항에 주의하십시오.

* 입력/출력(I/O) 활동을 모니터링할 수 있습니다. 예:I/O 작업, IO 대기 중인 CPU, 큐 크기 커밋 시스템이 I/O 바인딩되고 있으며 업사이징이 필요한지 여부를 결정하는 데 도움이 됩니다.
* `RevisionCleanupTaskHealthCheck`은 온라인 개정 정리의 전체 상태 상태를 나타냅니다. AEM 6.3에서와 같은 방식으로 작동하며 전체 또는 꼬리 구성 요소를 구별하지 않습니다.
* 로그 메시지에는 구성 모드에 대한 관련 정보가 들어 있습니다. 예를 들어 온라인 개정 정리가 시작되면 해당 로그 메시지는 구성 모드를 나타냅니다. 또한 일부 경우에 시스템은 테일 구성 작업을 실행하도록 예약한 경우 전체 컴포지션으로 되돌려지며 로그 메시지에 이 변경 사항이 표시됩니다. 아래 로그 샘플은 구성 모드와 테일에서 전체 구성 요소로의 변경을 나타냅니다.

```
TarMK GC: running tail compaction
TarMK GC: no base state available, running full compaction instead
```

### 알려진 제한 사항 {#known-limitations}

경우에 따라 테일 모드와 전체 구성 모드 간에 교대로 인해 정리 프로세스가 지연됩니다. 보다 정확하게, 전체 구성 후 저장소가 증가합니다(크기가 두 배로 표시됨). 저장소가 전체 사전 구성 크기 아래로 내려갈 때 이후 하위 컴포지션에서 추가 공간이 다시 배치됩니다. 동시 유지 관리 작업 수행도 피해야 합니다.

**디스크 크기를 최초 예상 저장소 크기보다 최소 2 또는 3배 정도 크게 지정하는 것이 좋습니다.**

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
   <td><p>TarMK의 지속성 형식은 AEM 6.5에서 변경됩니다. 이러한 변경 사항에는 사전 마이그레이션 단계가 필요하지 않습니다. 기존 리포지토리는 사용자에게 투명하게 롤링 마이그레이션을 수행합니다. AEM 6.5(또는 관련 도구)가 처음으로 저장소에 액세스하면 마이그레이션 프로세스가 시작됩니다.</p> <p><strong>AEM 6.5 지속성 포맷으로의 마이그레이션이 시작되면 리포지토리를 이전 AEM 6.3 지속성 포맷으로 되돌릴 수 없습니다.</strong></p> </td>
  </tr>
 </tbody>
</table>

### Oak 세그먼트 Tar {#migrating-to-oak-segment-tar}로 마이그레이션

<table>
 <tbody>
  <tr>
   <td><strong>질문</strong></td>
   <td><strong>답변</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>저장소를 마이그레이션해야 하는 이유는 무엇입니까?</strong></td>
   <td><p>AEM 6.3에서는 특히 온라인 개정 정리 작업의 성능과 효과를 개선하기 위해 스토리지 포맷을 변경해야 했습니다. 이러한 변경 사항은 이전 버전과 호환되지 않으며, 이전 Oak 세그먼트(AEM 6.2 및 이전)로 생성된 리포지토리는 마이그레이션되어야 합니다.</p> <p>스토리지 포맷 변경에 따른 추가 이점:</p>
    <ul>
     <li>향상된 확장성(최적화된 세그먼트 크기).</li>
     <li><a href="/help/sites-administering/data-store-garbage-collection.md" target="_blank">데이터 저장소 가비지 컬렉션</a>이 더 빨라졌습니다.<br /> </li>
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
   <td><strong>6.3으로 업그레이드하고 나중에 마이그레이션을 수행할 수 있습니까(예: 다른 유지 관리 창 사용)?</strong></td>
   <td>아니요, 위에서 설명한 바와 같이 컨텐츠 마이그레이션은 필수입니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>마이그레이션할 때 다운타임을 방지할 수 있습니까?</strong></td>
   <td>아니오. 실행 인스턴스에서 수행할 수 없는 일회성 작업입니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>잘못된 저장소 포맷에 우연히 부딪히면 어떻게 됩니까?</strong></td>
   <td>oak-segment-tar 저장소에 대해 oak-segment 모듈을 실행하려고 하면( 또는 그 반대) "잘못된 세그먼트 형식"이라는 메시지와 함께 <em>IllegalStateException</em>이(가) 시작되지 않습니다. 데이터 손상이 발생하지 않습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>검색 색인의 재색인이 필요합니까?</strong></td>
   <td>아니오. oak-segment에서 oak-segment-tar로 마이그레이션하면 컨테이너 형식이 변경됩니다. 포함된 데이터는 영향을 받지 않으며 수정되지 않습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>마이그레이션 중 및 후에 필요한 예상 디스크 공간을 최상으로 계산하는 방법</strong></td>
   <td>마이그레이션은 세그먼트스토어를 새 형식으로 다시 만드는 것과 같습니다. 마이그레이션 시 필요한 추가 디스크 공간을 예상하는 데 사용할 수 있습니다. 마이그레이션 후 이전 세그먼트 저장소를 삭제하여 공간을 다시 확보할 수 있습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>마이그레이션 기간을 가장 잘 예상하려면 어떻게 해야 합니까?</strong></td>
   <td>마이그레이션 전에 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup">오프라인 개정 정리</a>가 실행되면 마이그레이션 성능이 크게 향상될 수 있습니다. 모든 고객은 업그레이드 프로세스의 사전 요구 사항으로 이 소프트웨어를 실행해야 합니다. 일반적으로 마이그레이션 기간은 오프라인 수정 정리 작업이 마이그레이션 전에 실행되었다고 가정할 때 오프라인 개정 정리 작업의 기간과 비슷해야 합니다.</td>
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
   <td><strong>온라인 개정 정리를 실행하는 빈도</strong></td>
   <td>매일 한 번. 작업 대시보드의 기본 구성입니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 유지 관리 작업의 시작 시간을 어떻게 구성할 수 있습니까?</strong></td>
   <td><a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">온라인 개정 정리 실행 방법</a> 섹션을 참조하십시오. </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 시 초과해서는 안 되는 최대 빈도가 있습니까?</strong></td>
   <td>기본적으로 구성된 대로 하루에 한 번 온라인 개정 정리를 실행하는 것이 좋습니다.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리를 실행해야 하는 빈도를 결정하는 주요 지표는 무엇입니까?</strong></td>
   <td>온라인 개정 청소가 유지 관리 작업으로 구성되고 매일 자동으로 실행되므로 빈도를 확인할 필요가 없습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>처음 실행할 때 온라인 개정 정리 기능이 공간을 다시 확보할 수 없는 이유는 무엇입니까?</strong></td>
   <td>온라인 개정 클린은 몇 세대에 걸쳐 이전 개정판을 다시 처리합니다. 개정 정리가 실행될 때마다 새로 생성이 생성됩니다. 2세대 이상 된 컨텐츠만 재매립됩니다. 즉, 첫 번째 실행에서는 재확보할 필요가 없습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>오프라인 수정 정리 후 실행할 때 첫 번째 온라인 수정 정리 시 공간을 다시 찾지 못하는 이유는 무엇입니까?</strong></td>
   <td><p>오프라인 개정 청소가 온라인 개정 정리를 위한 최신 2세대 간에 비해 최신 세대를 제외한 모든 것을 회수하고 있습니다. 새 저장소의 경우 오프라인 개정 정리 이후 처음으로 실행될 때 되찾는 데 필요한 세대수가 없으므로 온라인 개정 정리에서는 공간을 다시 찾지 못합니다.</p> <p>또한 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">이 장</a>의 "오프라인 개정 정리 후 온라인 개정 정리 실행" 섹션을 읽으십시오.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>작성자 및 게시에 일반적으로 다른 온라인 개정 정리 창이 있습니까?</strong></td>
   <td>이는 근무시간과 고객이 온라인으로 방문한 트래픽 패턴에 따라 다릅니다. 주 생산 시간 외에 유지 관리 기간을 구성하여 최상의 정리 효과를 얻을 수 있습니다. 여러 AEM 게시 인스턴스(TarMK Farm)의 경우 온라인 개정 정리를 위한 유지 관리 기간이 서로 달라져야 합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리를 실행하기 전에 사전 요구 사항이 있습니까?</strong></td>
   <td><p>온라인 개정 정리는 AEM 6.3 이상 릴리스에서만 사용할 수 있습니다. 또한 이전 버전의 AEM을 사용 중인 경우 새로운 <a href="/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar">Oak Segment Tar</a>로 마이그레이션해야 합니다.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 기간을 결정하는 요인은 무엇입니까?</strong></td>
   <td>요소는 다음과 같습니다.<br />
    <ul>
     <li>저장소 크기</li>
     <li>시스템에 로드(분당 요청, 특히 쓰기 작업)</li>
     <li>활동 패턴(읽기/쓰기)</li>
     <li>하드웨어 사양(CPU 성능, 메모리, IOPS)</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리를 실행하는 동안 작성자가 계속 작업할 수 있습니까?</strong></td>
   <td>예. 온라인 개정 정리 서비스는 동시 쓰기를 처리할 수 있습니다. 그러나 동시 쓰기 트랜잭션을 사용하지 않고도 온라인 개정 정리 작업을 보다 빠르고 효율적으로 수행할 수 있습니다. 온라인 수정 정리 유지 관리 작업을 많은 트래픽 없이 비교적 조용한 시간으로 예약하는 것이 좋습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리를 실행할 때 디스크 공간 및 더미 메모리의 최소 요구 사항은 무엇입니까?</strong></td>
   <td><p>온라인 개정 정리 중에 디스크 공간이 지속적으로 모니터링됩니다. 사용 가능한 디스크 공간이 중요한 값 아래로 떨어지면 프로세스가 취소됩니다. 중요한 값은 저장소의 현재 디스크 풋프린트의 25%이며 구성할 수 없습니다.</p> <p><strong>디스크 크기를 최초 예상 저장소 크기보다 최소 2 또는 3배 정도 크게 지정하는 것이 좋습니다.</strong></p> <p>정리 프로세스 동안 사용 가능한 더미 공간이 지속적으로 모니터링됩니다. 사용 가능한 더미 공간이 중요한 값 아래로 떨어지면 프로세스가 취소됩니다. 중요한 값은 org.apache.jackrabbit.oak.segment.SegmentNodeStoreService#MEMORY_THRESHOLD를 통해 구성됩니다. 기본값은 15입니다%.</p> <p>최소 구성 요소 힙의 크기를 위한 Recommendations은 AEM 메모리 크기 권장 사항과 분리되지 않습니다. 일반적인 규칙으로:<strong>AEM 인스턴스의 크기가 사용 사례에 대응하기에 충분하고 이에 대한 페이로드를 예상하면 정리 프로세스에서 충분한 메모리를 얻습니다.</strong></p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리를 실행하는 동안 예상되는 성능 영향은 무엇입니까?</strong></td>
   <td>온라인 개정 정리 작업은 기본 시스템 작업을 동시에 읽고 저장소에 쓰는 백그라운드 프로세스입니다. 특히, 다른 스레드가 저장소에 기록되지 않도록 하려면 짧은 시간 동안 저장소에 대한 전용 액세스 권한을 획득해야 할 수 있습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 시간이 얼마나 걸립니까?</strong></td>
   <td>내부적으로 실시한 최신 성능 테스트에 따라 실행하는 데 2시간이 소요되지 않습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 시간이 더 오래 걸리는 경우 어떻게 해야 합니까?</strong></td>
   <td>
    <ul>
     <li>매일 실행되고 있는지 확인합니다.<br /> </li>
     <li>Operations Dashboard에서 유지 관리 기간을 적절히 구성하여 최소한의 저장소 활동 중에 실행되도록 하십시오.</li>
     <li>시스템 리소스 확장(CPU, 메모리, I/O)</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 작업이 구성된 유지 관리 창을 초과하는 경우 어떻게 됩니까?</strong></td>
   <td>다른 유지 관리 작업이 실행을 지연시키지 않도록 하십시오. 동일한 유지 관리 기간 내에 온라인 개정 정리 작업보다 더 많은 유지 관리 작업이 실행되는 경우일 수 있습니다. 유지 관리 작업은 구성 가능한 주문 없이 순차적으로 실행됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>수정 가비지 수집이 생략되는 이유는 무엇입니까?</strong></td>
   <td><p>수정 정리 작업은 정리 가능한 쓰레기가 충분한지 결정하기 위해 예측 단계에 의존합니다. 견적 도구는 마지막으로 압축한 후 현재 크기를 저장소의 크기와 비교합니다. 크기가 구성된 델타를 초과하는 경우 정리가 실행됩니다. 크기 델타는 1GB로 설정됩니다. 이는 저장소 크기가 마지막 정리 실행 이후 1GB까지 증가하지 않은 경우 새 개정 정리 반복을 건너뜁니다. </p> <p>다음은 예측 단계의 관련 로그 항목입니다.</p>
    <ul>
     <li>수정 GC가 실행됩니다.<em>크기 델타는 N% 또는 N/N(N/N 바이트)이므로 압축</em>을(를) 실행합니다.</li>
     <li>개정 GC는 <strong>을(를) 실행하지 않습니다.<em>크기 델타는 N% 또는 N/N(N/N 바이트)이므로 지금 필요한 구성 요소를 건너뜁니다.</em></strong></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>성능 영향이 너무 높을 경우 자동 컴포지션을 안전하게 중단할 수 있습니까?</strong></td>
   <td>예. AEM 6.3이므로 작업 대시보드 내의 유지 관리 작업 창 또는 JMX를 통해 안전하게 중지할 수 있습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>예약된 정리 작업 중에 AEM 인스턴스가 종료되는 경우 프로세스가 안전하게 중단됩니까 아니면 작업이 완료될 때까지 종료가 차단됩니까?</strong></td>
   <td>수정 정리 작업이 중단되고 저장소가 안전하게 종료됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 중에 시스템이 충돌할 경우 어떻게 됩니까?</strong></td>
   <td>이러한 경우에는 데이터 손상의 위험이 없습니다. 남은 음식물은 차후 청소된다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리를 실행하지 않으면 어떤 영향이 있습니까?</strong></td>
   <td>시간에 따른 성능 저하</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>어떤 수정본을 수집하고 있습니까?</strong></td>
   <td>기본적으로 온라인 개정 정리 기능은 24시간 이상 된 수정만 수집합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>저장소에 동시 쓰기가 너무 많은 경우 어떻게 됩니까?</strong></td>
   <td><p>시스템에 쓰기 동시성이 있는 경우 온라인 개정 정리 시 구성 주기가 끝날 때 변경 사항을 커밋하려면 전용 쓰기 액세스 권한이 필요할 수 있습니다. <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html" target="_blank">oak documentation</a>에 자세히 설명된 대로 시스템은 <strong>forceCompact mode</strong>로 이동합니다. 강제 압축이 진행되는 동안 동시 쓰기에 영향을 주지 않고 변경을 최종적으로 확정하기 위해 전용 쓰기 잠금을 획득합니다. 응답 시간에 대한 영향을 제한하려면 시간 초과 값을 정의할 수 있습니다. 이 값은 기본적으로 1분으로 설정되며, 즉 1분 이내에 강제 압축이 완료되지 않으면 동시 커밋에 유리한 구성 프로세스가 중단됩니다.</p> <p>힘 축소의 기간은 다음 요인에 따라 다릅니다.</p>
    <ul>
     <li>하드웨어:특히 IOPS 지속 시간은 더 많은 IOPS와 함께 줄어듭니다.</li>
     <li>세그먼트 저장소 크기:기간이 세그먼트 저장소의 크기로 증가합니다.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>대기 인스턴스에서 온라인 개정 청소가 어떻게 실행됩니까?</strong></p> </td>
   <td><p>콜드 대기 설정에서 기본 인스턴스만 온라인 개정 정리를 실행하도록 구성해야 합니다. 대기 인스턴스에서 온라인 개정 정리를 구체적으로 예약할 필요가 없습니다.</p> <p>대기 인스턴스의 해당 작업은 자동 정리 - 온라인 개정 정리 단계의 정리 단계에 해당합니다. 자동 정리는 기본 인스턴스에서 온라인 개정 정리가 실행된 후 대기 인스턴스에서 실행됩니다.</p> <p>대기 인스턴스에서 예측 및 비교 단계가 실행되지 않습니다.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>오프라인 개정 정리 시 온라인 개정 정리 수보다 더 많은 디스크 공간을 사용할 수 있습니까?</strong></td>
   <td><p>오프라인 개정 정리 기능은 애플리케이션 스택에서 계속 참조되고 있는 이전 수정에 대해 온라인 개정 정리 가 고려해야 하는 동안 이전 수정본을 즉시 제거할 수 있습니다. 따라서 일부 가비지 수집 주기 동안 효과가 완화되는 후자보다 더 공격적인 가비지를 제거할 수 있습니다.</p> <p>또한 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">이 장</a>의 "오프라인 개정 정리 후 온라인 개정 정리 실행" 섹션을 읽으십시오.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>메모리 매핑 파일 작업에 대한 고려 사항이 있습니까?</td>
   <td>
    <ul>
     <li><strong>Windows 환경에서</strong> 일반 파일 액세스 기능은 항상 적용되므로 메모리 매핑 액세스 기능은 사용되지 않습니다. 일반적인 조언 하나로 사용 가능한 모든 RAM을 힙에 할당해야 하며 segmentCache 크기를 늘려야 합니다. segmentCache.size 옵션을 org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config에 추가하여 segmentCache를 늘립니다(예: segmentCache.size=20480). 운영 체제 및 기타 프로세스에 필요한 RAM을 따로 사용하지 마십시오.</li>
     <li><strong>Windows가 아닌 환경에서</strong> 실제 메모리 크기를 늘려 저장소의 메모리 매핑을 향상시킵니다.</li>
    </ul> </td>
   <td>
    <ul>
     <li> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 온라인 개정 정리 모니터링 {#monitoring-online-revision-cleanup}

<table>
 <tbody>
  <tr>
   <td><strong>온라인 개정 정리 중에 모니터링해야 할 사항은 무엇입니까?</strong></td>
   <td>
    <ul>
     <li>온라인 개정 정리를 사용하는 경우 디스크 공간을 모니터링해야 합니다. 디스크 공간이 부족한 경우 정리가 실행되지 않거나 선제적으로 종료됩니다.</li>
     <li>온라인 개정 정리 완료 시간에 대한 로그를 확인합니다. 2시간 이상 걸리지 않을 겁니다</li>
     <li>체크포인트 수. 비교 실행 시 체크포인트가 3개 이상 있는 경우 체크포인트를 정리하는 것이 좋습니다.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리가 성공적으로 완료되었는지 확인하는 방법?</strong></td>
   <td><p>로그를 확인하여 온라인 개정 정리가 성공적으로 완료되었는지 확인할 수 있습니다.</p> <p>예를 들어 "<code>TarMK GC #{}: compaction completed in {} ({} ms), after {} cycles</code>"은 "<code>TarMK GC #{}: compaction gave up compacting concurrent commits after {} cycles</code>" 메시지 앞에 오지 않는 한 성공적으로 완료된 구성 단계를 의미합니다. 이는 동시 로드가 너무 많다는 것을 의미합니다.</p> <p>따라서 정리 단계를 성공적으로 완료하기 위한 메시지 "<code>TarMK GC #{}: cleanup completed in {} ({} ms</code>"이 있습니다.</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><strong>마지막 온라인 개정 정리 실행 통계를 어디에서 확인할 수 있습니까?</strong></td>
   <td><p>상태, 진행률 및 통계가 JMX(<code>SegmentRevisionGarbageCollection</code> MBean)을 통해 노출됩니다. <code>SegmentRevisionGarbageCollection</code> MBean에 대한 자세한 내용은 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">다음 단락</a>을 참조하십시오.</p> <p>진행 상태는<code>EstimatedRevisionGCCompletion</code> <code>SegmentRevisionGarbageCollection MBean.</code></p> <p><code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection”</code>을 사용하여 MBean의 참조를 얻을 수 있습니다.</p> <p>통계는 마지막 시스템이 시작된 후에만 사용할 수 있습니다. 외부 모니터링 도구를 활용하여 AEM의 가동 시간 이후 데이터를 유지할 수 있습니다. 외부 모니터링 도구</a>의 예로 Nagios에 상태 검사를 첨부하는 방법은 AEM 설명서를 참조하십시오.<a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank"></a></p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>관련 로그 항목이란 무엇입니까?</strong></td>
   <td>
    <ul>
     <li>온라인 수정 정리 시작/중지
      <ul>
       <li>온라인 개정 정리는 다음 세 단계로 구성됩니다.예측, 비교 및 정리 저장소에 충분한 쓰레기가 포함되어 있지 않으면 추정이 구성 및 정리 작업을 건너뛸 수 있습니다. AEM의 최신 버전에서 메시지 "<code>TarMK GC #{}: estimation started</code>"은 예측 시작을 나타내며, "<code>TarMK GC #{}: compaction started, strategy={}</code>"은 구성 요소의 시작을 나타내고 "T<code>arMK GC #{}: cleanup started. Current repository size is {} ({} bytes</code>"은 정리 시작을 표시합니다.</li>
      </ul> </li>
     <li>수정 정리를 통해 확보한 디스크 공간
      <ul>
       <li>공간은 정리 단계가 완료될 때만 재확보됩니다. 정리 단계의 완료를 로그 메시지 "T<code>arMK GC #{}: cleanup completed in {} ({} ms</code>"로 표시합니다. 게시물 정리 크기는 {}({}바이트)이고 공간은 {}({}바이트)입니다. 압축 맵 두께/깊이는 {}/{}({}바이트/{})입니다.".</li>
      </ul> </li>
     <li>수정 정리 중 문제가 발생했습니다.
      <ul>
       <li>많은 실패 조건이 있으며 모두 "TarMK GC"를 시작으로 WARN 또는 ERROR 로그 메시지로 표시됩니다.</li>
      </ul> </li>
    </ul> <p>또한 아래의 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">오류 메시지 기반 문제 해결</a> 섹션을 참조하십시오.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 청소가 완료된 후 얼마나 많은 공간을 재확보했는지 확인하는 방법?</strong></td>
   <td>정리 주기가 끝나는 로그에 메시지가 있습니다."<code>TarMK GC #3: cleanup completed</code>" 저장소 크기 및 매립된 가비지의 양을 포함합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리가 완료된 후 저장소의 무결성을 확인하는 방법?</strong></td>
   <td><p>온라인 개정 정리 후에는 저장소 무결성 검사가 필요하지 않습니다. </p> <p>하지만 정리 후 저장소 상태를 확인하기 위해 다음 작업을 수행할 수 있습니다.</p>
    <ul>
     <li>저장소 <a href="/help/sites-deploying/consistency-check.md" target="_blank">순회 검사</a></li>
     <li>정리 프로세스가 완료된 후에 oak-run 도구를 사용하여 불일치를 확인합니다. 이 방법에 대한 자세한 내용은 <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache 설명서를 참조하십시오.</a> 이 도구를 실행하기 위해 AEM을 종료하지 않아도 됩니다.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>온라인 개정 정리 실패 여부와 복구 단계는 어떻게 검색합니까?</strong></td>
   <td>실패 조건은 "TarMK GC"로 시작하는 WARN 또는 ERROR 로그 메시지로 표시됩니다. 또한 아래의 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">오류 메시지 기반 문제 해결</a> 섹션을 참조하십시오.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>개정 정리 상태 확인에 표시되는 정보는 무엇입니까? 색상 코딩된 상태 수준에 어떻게 언제 기여할 수 있습니까? </strong></td>
   <td><p>개정 정리 상태 검사는 <a href="/help/sites-administering/operations-dashboard.md#health-reports" target="_blank">작업 대시보드</a>의 일부입니다.<br /> </p> <p>온라인 개정 정리 유지 관리 작업의 마지막 실행이 완료된 경우 상태는 <strong>GREEN</strong>입니다.</p> <p>온라인 개정 정리 유지 관리 작업이 한 번 취소된 경우 <strong>YELLOW</strong>입니다.<br /> </p> <p>온라인 개정 정리 유지 관리 작업이 연속적으로 3번 취소된 경우 <strong>RED</strong>이 됩니다. <strong>이 경우 수동 상호 작용이 </strong> 필수 사항이며 온라인 개정 정리 작업이 다시 실패할 가능성이 높습니다. 자세한 내용은 아래의 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-online-revision-cleanup">문제 해결</a> 섹션을 참조하십시오.<br /> </p> <p>시스템을 다시 시작한 후 상태 확인 상태가 재설정됩니다. 따라서 새로 다시 시작한 인스턴스는 개정 정리 상태 점검에 녹색 상태를 표시합니다. 외부 모니터링 도구를 활용하여 AEM의 가동 시간 이후 데이터를 유지할 수 있습니다. 외부 모니터링 도구</a>의 예로 Nagios에 상태 검사를 첨부하는 방법은 AEM 설명서를 참조하십시오.<a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios"></a></p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>대기 인스턴스에서 자동 정리를 모니터링하는 방법</strong></p> </td>
   <td><p>상태, 진행률 및 통계는 <code>SegmentRevisionGarbageCollection</code> MBean을 사용하여 JMX를 통해 노출됩니다. 다음 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">Oak documentation</a>도 참조하십시오. </p> <p><code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection”</code>을 사용하여 MBean의 참조를 얻을 수 있습니다.</p> <p>통계는 마지막 시스템이 시작된 후에만 사용할 수 있습니다. 외부 모니터링 도구를 활용하여 AEM의 가동 시간 이후 데이터를 유지할 수 있습니다. 또한 외부 모니터링 도구</a>에 대한 예로 Nagios에 상태 검사를 첨부하는 방법은 AEM 설명서를 참조하십시오.<a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank"></a></p> <p>로그 파일을 사용하여 자동 정리 상태, 진행 상황 및 통계를 확인할 수도 있습니다.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>대기 인스턴스에서 자동 정리 중에 모니터링해야 하는 것은 무엇입니까?</strong></p> </td>
   <td>
    <ul>
     <li>자동 정리를 실행할 때 디스크 공간을 모니터링해야 합니다.</li>
     <li>2시간이 초과되지 않도록 하기 위한 완료 시간(로그를 통해)</li>
     <li>자동 정리를 실행한 후 세그먼트스토어 크기입니다. 대기 인스턴스에 있는 세그먼트 저장소의 크기는 기본 인스턴스의 세그먼트와 거의 같아야 합니다.</li>
    </ul> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 온라인 개정 정리 문제 해결 {#troubleshooting-online-revision-cleanup}

<table>
 <tbody>
  <tr>
   <td><strong>온라인 개정 정리를 실행하지 않으면 어떤 결과가 발생할 수 있습니까?</strong></td>
   <td>AEM 인스턴스는 디스크 공간이 부족해지며, 이로 인해 운영 중단이 발생합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>게시 인스턴스에서 온라인 개정 정리를 실행하는 데 높은 사용자 트래픽이 문제가 됩니까?</strong></td>
   <td>사용자 트래픽이 높으면 구성 단계를 성공적으로 완료할 수 있는지 여부에 영향을 줍니다.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>상태 확인 및 로그 항목에 따르면 온라인 개정 정리가 연속적으로 3번 성공적으로 완료되지 않았습니다. 온라인 개정 정리를 성공적으로 완료하려면 무엇이 필요합니까?</strong></td>
   <td>문제를 찾아 해결하기 위해 몇 단계를 진행할 수 있습니다.<br />
    <ul>
     <li>첫째, 로그 항목<br />을 확인합니다. </li>
     <li>로그의 정보에 따라 적절한 작업을 수행합니다.
      <ul>
       <li>로그에 5개의 누락된 압축 주기와 <code>forceCompact</code> 주기에서 시간 초과가 표시되는 경우 저장소 쓰기 수가 낮은 유지 관리 기간을 조용한 시간으로 예약합니다. <em>https://serveraddress:serverport/libs/granite/operations/content/monitoring/page.html</em>에 있는 저장소 지표 모니터링 도구에서 저장소 쓰기를 확인할 수 있습니다.</li>
       <li>유지 관리 기간이 끝날 때 정리가 중지된 경우 유지 관리 작업 사용자 인터페이스의 유지 관리 창 구성이 충분한지 확인하십시오</li>
       <li>사용 가능한 더미 메모리가 충분하지 않은 경우 인스턴스에 충분한 메모리가 있는지 확인하십시오.</li>
       <li>늦은 반응 시, 온라인 개정 정리를 완료하기 위해 더 긴 유지 관리 기간 내에도 세그먼트스토어가 너무 많이 증가할 수 있습니다. 예를 들어, 지난 주에 완료된 온라인 개정 청소에 성공한 적이 없으면 오프라인 유지 관리를 계획하고 세그먼트스토어를 관리 가능한 크기로 되돌리려면 오프라인 개정 정리를 실행하는 것이 좋습니다.</li>
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
   <td>온라인 개정 정리가 취소되고 남은 음식은 제거될 것입니다. 다음 번에 유지 관리 기간이 예약되면 다시 시작됩니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong><code>SegmentNotFoundException</code> 인스턴스가 <code>error.log</code>에 로그인하는 이유는 무엇이며 어떻게 복구합니까?</strong></td>
   <td><p>찾을 수 없는 스토리지 장치(세그먼트)에 액세스하려고 하면 TarMK가 <code>SegmentNotFoundException</code>를 기록합니다. 다음과 같은 세 가지 시나리오가 있습니다.</p>
    <ol>
     <li>권장되는 액세스 메커니즘(예: Sling 및 JCR API)을 우회하고 낮은 수준의 API/SPI를 사용하여 저장소에 액세스한 다음 세그먼트의 보존 시간을 초과하는 응용 프로그램입니다. 즉, 온라인 개정 정리(기본적으로 24시간)에서 허용하는 보존 시간보다 엔티티를 참조하게 됩니다. 이러한 경우는 일시적인 현상이며 데이터 손상을 야기하지 않습니다. 복구하려면 oak-run 도구를 사용하여 예외의 일시적 특성을 확인해야 합니다(oak-run 확인은 오류를 보고하지 않아야 함). 이 작업을 수행하려면 인스턴스를 오프라인으로 전환하고 나중에 다시 시작해야 합니다.</li>
     <li>외부 이벤트로 인해 디스크의 데이터가 손상되었습니다. 디스크 공간 부족 또는 필요한 데이터 파일을 실수로 수정하는 경우 디스크 장애가 발생할 수 있습니다. 이 경우 인스턴스를 오프라인으로 설정하고 oak-run 검사를 사용하여 복구해야 합니다. oak-run check를 수행하는 방법에 대한 자세한 내용은 다음 <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache documentation</a>을 참조하십시오.</li>
     <li>다른 모든 항목은 <a href="https://helpx.adobe.com/kr/marketing-cloud/contact-support.html" target="_blank">Adobe 고객 지원 센터</a>를 통해 해결되어야 합니다.</li>
    </ol> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 오류 메시지 기준 문제 해결 {#troubleshooting-based-on-error-messages}

온라인 개정 정리 프로세스 중에 사고가 발생하는 경우 error.log는 자세한 정보가 됩니다. 다음 매트릭스는 가장 일반적인 메시지를 설명하고 가능한 솔루션을 제공하는 것을 목표로 합니다.

| **위상** | **로그 메시지** | **설명** | **다음 단계** |
|---|---|---|---|
|  |  |  |  |
| 예측 | TarMK GC #2:컴포지션이 일시 중지되어 예측 생략됨 | 구성에 따라 시스템에서 컴포지션을 비활성화하면 예측 단계를 건너뛸 수 있습니다. | 온라인 개정 정리 사용을 참조하십시오. |
|  | TarMK GC #2:중단된 항목:${REASON}. 구성 요소를 건너뛰는 중입니다. | 예측 단계가 너무 일찍 종료되었습니다. 예측 단계를 방해할 수 있는 이벤트의 일부 예:호스트 시스템의 메모리 또는 디스크 공간이 부족합니다. | 주어진 이유에 따라 다릅니다. |
| 구성 요소 | TarMK GC #2:압축 일시 중지됨 | 구성 단계가 구성에 의해 일시 중지된 경우 예측 단계와 비교 단계가 실행되지 않습니다. | 온라인 개정 정리를 활성화합니다. |
|  | TarMK GC #2:취소됨:${REASON}. | 압축 단계가 너무 빨리 종료되었습니다. 구성 단계를 방해할 수 있는 이벤트의 일부 예:호스트 시스템의 메모리 또는 디스크 공간이 부족합니다. 또한 시스템을 종료하거나 작업 대시보드에 있는 유지 관리 창과 같은 관리 인터페이스를 통해 명시적으로 시스템을 취소하면 구성 요소를 취소할 수 있습니다. | 주어진 이유에 따라 다릅니다. |
|  | TarMK GC #2:5회 후 32.902분(1974140ms)에 컴패션이 실패했습니다. | 이 메시지는 복구할 수 없는 오류가 있음을 의미하지는 않지만 특정 횟수의 시도 후에 컴포지션이 종료되었음을 의미합니다. 또한 다음 단락](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes)을 읽으십시오.[ | 다음 [Oak documentation](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes)과 [온라인 개정 정리 실행](/help/sites-deploying/revision-cleanup.md#running-online-revision-cleanup) 섹션의 마지막 질문을 읽어 보십시오. |
| 정리 | TarMK GC #2:정리 중 | 저장소를 종료하여 정리가 취소되었습니다. 일관성에 영향을 주지 않습니다. 또한 디스크 공간은 완전히 재확보되지 않을 가능성이 높습니다. 다음 개정 정리 주기 동안 다시 회수됩니다. | 저장소가 종료된 이유를 확인하고 유지 관리 기간 동안 저장소를 종료하지 않도록 앞으로 시도합니다. |

## 오프라인 개정 정리 실행 방법 {#how-to-run-offline-revision-cleanup}

>[!CAUTION]
>
>AEM 설치 시 사용하는 Oak 버전에 따라 서로 다른 버전의 Oak 실행 도구를 사용해야 합니다. 도구를 사용하기 전에 아래 버전 요구 사항 목록을 확인하십시오.
>
>* Oak 버전 **1.0.0 ~ 1.0.11**&#x200B;이나&#x200B;**1.1.0 ~ 1.1.6**&#x200B;의 경우 Oak-run 버전** 1.0.11*
   >
   >
* Oak 버전 **이 위의**&#x200B;보다 최신 버전의 경우 AEM 설치의 Oak 코어와 일치하는 Oak 실행 버전을 사용하십시오.

>



Adobe은 개정 정리를 수행하기 위해 **Oak-run**&#x200B;이라는 도구를 제공합니다. 다음 위치에서 다운로드할 수 있습니다.

[https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/)

이 도구는 저장소를 압축하기 위해 수동으로 실행할 수 있는 실행 가능한 jar입니다. 도구를 제대로 실행하려면 저장소를 종료해야 하므로 이 프로세스를 오프라인 개정 정리 과정이라고 합니다. 유지 관리 창에 따라 정리를 계획해야 합니다.

정리 프로세스의 성능을 높이는 방법에 대한 팁은 [오프라인 개정 정리 성능 향상](/help/sites-deploying/revision-cleanup.md#increasing-the-performance-of-offline-revision-cleanup)을 참조하십시오.

>[!NOTE]
>
>유지 관리가 수행되기 전에 이전 체크포인트를 지울 수도 있습니다(아래 절차의 2단계 및 3단계). 체크포인트가 100개가 넘는 인스턴스에만 권장됩니다.

1. AEM 인스턴스의 최근 백업이 있는지 항상 확인하십시오.

   AEM을 종료합니다.

1. (선택 사항) 도구를 사용하여 이전 체크포인트를 찾습니다.

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore
   ```

1. (선택 사항) 그런 다음 참조되지 않은 체크포인트를 삭제합니다.

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore rm-unreferenced
   ```

1. 구성 요소를 실행하고 완료될 때까지 기다립니다.

   ```xml
   java -jar -Dsun.arch.data.model=32 oak-run.jar compact install-folder/crx-quickstart/repository/segmentstore
   ```

### 오프라인 개정 정리 성능 향상 {#increasing-the-performance-of-offline-revision-cleanup}

Oak-run 툴은 수정 정리 프로세스의 성능을 높이고 유지 관리 기간을 최대한 최소화하기 위해 몇 가지 기능을 도입합니다.

목록에는 아래 설명된 대로 여러 명령줄 매개 변수가 포함되어 있습니다.

* **-mmap.** 이 값을 true 또는 false로 설정할 수 있습니다. true로 설정하면 메모리 매핑 액세스가 사용됩니다. false로 설정하면 파일 액세스가 사용됩니다. 지정하지 않으면 메모리 매핑 액세스가 64비트 시스템에서 사용되고 파일 액세스 기능은 32비트 시스템에서 사용됩니다. Windows에서는 일반 파일 액세스가 항상 적용되며 이 옵션은 무시됩니다. **이 매개 변수는 -Dtar.memoryMapped 매개 변수를 대체했습니다.**

* **-Dupdate.limit**. 임시 트랜잭션을 디스크에 플러시할 임계값을 정의합니다. 기본값은 10000입니다.

* **-압축 간격**. 현재 맵을 압축할 때까지 유지할 컴포지션 맵 항목의 수입니다. 기본값은 1000000입니다. You should increase this value to an even higher number for faster throughput, if enough heap memory is available. **이 매개 변수는 Oak 버전 1.6에서 제거되었으며 아무런 효과가 없습니다.**

* **-Dcomaction-progress-log**. 기록할 호환 노드의 수입니다. 기본값은 150000입니다. 즉, 작업 중에 첫 번째 15000 호환 노드가 기록됩니다. 아래 설명된 다음 매개 변수와 함께 사용하십시오.

* **-Dtar.PersistCompactionMap.** 구성 맵 지속을 위해 더미 메모리 대신 디스크 공간을 사용하려면 이 매개 변수를 true로 설정합니다. Oak-run tool **versions 1.4** 이상이 필요합니다. 자세한 내용은 [오프라인 개정 정리 FAQ](/help/sites-deploying/revision-cleanup.md#offline-revision-cleanup-frequently-asked-questions) 섹션의 질문 3을 참조하십시오. **이 매개 변수는 Oak 버전 1.6에서 제거되었으며 아무런 효과가 없습니다.**

* **—force.** 비교 강제 적용 및 일치하지 않는 세그먼트 스토어 버전을 무시합니다.

>[!CAUTION]
>
>`--force` 매개 변수를 사용하면 세그먼트 스토어가 이전 Oak 버전과 호환되지 않는 최신 버전으로 업그레이드됩니다. 또한, 다운그레이드는 불가능하다는 것을 고려하십시오. 일반적으로 이러한 매개 변수를 사용하는 방법에 대해 알고 있는 경우에만 주의해서 사용해야 합니다.

사용 중인 매개 변수의 예:

```xml
java -Dupdate.limit=10000 -Dcompaction-progress-log=150000 -Dlogback.configurationFile=logback.xml -Xmx8g -jar oak-run-*.jar checkpoints <repository>
```

### 개정 정리 트리거 방법 {#additional-methods-of-triggering-revision-cleanup} 추가

위에 제시된 방법 외에도 다음과 같이 JMX 콘솔을 사용하여 개정 정리 메커니즘을 트리거할 수도 있습니다.

1. [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)으로 이동하여 JMX 콘솔을 엽니다.
1. **RevisionGarbageCollection** MBean을 클릭합니다.
1. 다음 창에서 **startRevisionGC()**&#x200B;를 클릭한 다음 **Invoke**&#x200B;를 클릭하여 수정 가비지 수집 작업을 시작합니다.

### 오프라인 개정 정리 FAQ {#offline-revision-cleanup-frequently-asked-questions}

<table>
 <tbody>
  <tr>
   <td><strong>오프라인 개정 정리 시간을 결정하는 요인은 무엇입니까?</strong></td>
   <td><p>저장소 크기 및 정리해야 하는 개정판의 양이 정리 시간을 결정합니다.</p> </td>
  </tr>
  <tr>
   <td><strong>개정과 페이지 버전의 차이점은 무엇입니까?</strong></td>
   <td>
    <ul>
     <li><strong>Oak 개정: </strong> Oak는 노드 및 속성으로 구성된 큰 트리 계층 구조의 모든 컨텐츠를 구성합니다. 이 컨텐츠 트리의 각 스냅샷 또는 개정은 변경할 수 없으며 트리 변경 사항은 새로운 수정 시퀀스로 표시됩니다. 일반적으로 각 컨텐츠 수정은 새 개정을 트리거합니다. <a href="https://jackrabbit.apache.org/dev/ngp.html" target="_blank"> 링크</a>도 참조하십시오.</li>
     <li><strong>페이지 버전:</strong> 버전 매기기를 통해 특정 시점의 페이지 "스냅샷"을 만들 수 있습니다. 일반적으로 페이지가 활성화되면 새 버전이 만들어집니다. 자세한 내용은 <a href="/help/sites-authoring/working-with-page-versions.md" target="_blank">페이지 버전 작업</a>을 참조하십시오.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>8시간 이내에 완료되지 않으면 오프라인 개정 정리 작업의 속도를 높이는 방법?</strong></td>
   <td>수정 작업이 8시간 이내에 완료되지 않고 <a href="/help/sites-administering/operations-dashboard.md#diagnosis-tools" target="_blank">스레드 dumps</a>에서 기본 핫스팟이 <code>InMemoryCompactionMap.findEntry</code>임을 나타내는 경우, oak-run tool <strong>versions 1.4 </strong>버전 이상에서 다음 매개 변수를 사용하십시오.<code>-Dtar.PersistCompactionMap=true</code>. Oak 버전 1.6에서는 <code>-Dtar.PersistCompactionMap</code> 매개 변수가 제거되었습니다.</td>
  </tr>
 </tbody>
</table>

