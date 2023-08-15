---
title: MSM 롤아웃 충돌
seo-title: MSM Rollout Conflicts
description: 다중 사이트 관리자 롤아웃 충돌을 처리하는 방법에 대해 알아봅니다.
seo-description: Learn how to deal with Multi Site Manager rollout conflicts.
uuid: 7a640905-aae2-498e-b95c-2c73008fa1cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 16db5334-604f-44e2-9993-10d683dee5bb
feature: Multi Site Manager
exl-id: e145e79a-c363-4a33-b9f9-99502ed20563
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 25%

---

# MSM 롤아웃 충돌{#msm-rollout-conflicts}

블루프린트 분기 및 종속 라이브 카피 분기 모두에서 동일한 페이지 이름의 새 페이지를 만들면 충돌이 발생할 수 있습니다.

이러한 충돌은 롤아웃 시 처리 및 해결해야 합니다.

## 충돌 처리 {#conflict-handling}

블루프린트 및 라이브 카피 분기에 충돌하는 페이지가 있는 경우 MSM을 사용하여 처리 방법(또는 처리 여부)을 정의할 수 있습니다.

롤아웃을 차단하지 않도록 다음과 같은 정의를 사용할 수 있습니다.

* 롤아웃 시 우선 순위가 높은 페이지(블루프린트 또는 라이브 카피)
* 이름을 변경할 페이지(및 방법),
* 게시된 콘텐츠에 미치는 영향

  AEM의 기본 비헤이비어(기본 제공)는 게시된 콘텐츠에 영향을 주지 않는다는 것입니다. 따라서 라이브 카피 분기에 수동으로 생성된 페이지가 게시되어 있는 경우 해당 콘텐츠는 충돌 처리 및 롤아웃 이후에도 계속 게시됩니다.

표준 기능 이외에도 맞춤화된 충돌 핸들러를 추가하여 다른 규칙을 구현할 수 있습니다. 또한 개별 프로세스로 게시 작업을 허용할 수도 있습니다.

### 예시 상황 {#example-scenario}

다음 섹션에서는 새 페이지의 예를 사용합니다 `b`블루프린트 및 라이브 카피 분기 모두에 수동으로 만들어져서 다양한 충돌 해결 방법을 보여 줍니다.

* 블루프린트: `/b`

  마스터 페이지. 1개의 하위 페이지, bp-level-1을 가진 페이지.

* live copy: `/b`

  라이브 카피 분기에 수동으로 생성된 페이지(하위 페이지 1개 포함) `lc-level-1`.

   * 게시에서 하위 페이지와 함께 `/b`로 활성화됨.

**롤아웃 이전**

<table>
 <tbody>
  <tr>
   <td><strong>롤아웃 이전의 블루프린트</strong></td>
   <td><strong>롤아웃 이전의 live copy</strong></td>
   <td><strong>롤아웃 전 게시</strong></td>
  </tr>
  <tr>
   <td><code>b</code><br /> <br /> (블루프린트 분기에서 만들어짐, 롤아웃 준비 완료)<br /> </td>
   <td><code>b</code><br /> <br /> (라이브 카피 분기에 수동으로 생성됨)<br /> </td>
   <td><code>b</code><br /> <br /> (라이브 카피 분기에 수동으로 생성된 페이지 b의 콘텐츠 포함)</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code><br /> <br /> (라이브 카피 분기에 수동으로 생성됨)<br /> </td>
   <td><code> /lc-level-1</code><br /> <br /> (페이지 콘텐츠 포함)<br /> 라이브 카피 분기에 수동으로 생성된 하위 수준 1)</td>
  </tr>
 </tbody>
</table>

## 롤아웃 관리자 및 충돌 처리 {#rollout-manager-and-conflict-handling}

롤아웃 관리자를 사용하여 충돌 관리를 활성화 또는 비활성화할 수 있습니다.

다음을 사용하여 수행됩니다. [OSGi 구성](/help/sites-deploying/configuring-osgi.md) / **일별 CQ WCM 롤아웃 관리자**:

* **수동으로 만든 페이지와의 충돌 처리**:

  ( `rolloutmgr.conflicthandling.enabled`)

  롤아웃 관리자가 블루프린트에 존재하는 이름으로 라이브 카피에 생성된 페이지의 충돌을 처리해야 하는 경우 true로 설정합니다.

AEM이 [충돌 관리가 비활성화되었을 때 실행되는 사전 정의된 비헤이비어](#behavior-when-conflict-handling-deactivated).

## 충돌 핸들러 {#conflict-handlers}

AEM은 충돌 처리기를 사용하여 블루프린트에서 라이브 카피로 콘텐츠를 롤아웃할 때 발생하는 페이지 충돌을 해결합니다. 페이지 이름을 바꾸는 것은 이러한 충돌을 해결하는 일반적인 방법 중 하나입니다. 하나 이상의 충돌 핸들러를 작동하여 다양한 비헤이비어를 실행할 수 있습니다.

AEM은 다음을 제공합니다.

* [기본 충돌 핸들러](#default-conflict-handler):

   * `ResourceNameRolloutConflictHandler`

* [맞춤화된 핸들러](#customized-handlers) 구현 가능성.
* 각 개별 처리기의 우선 순위를 설정할 수 있는 서비스 순위 메커니즘. 순위가 가장 높은 서비스가 사용됩니다.

### 기본 충돌 핸들러 {#default-conflict-handler}

기본 충돌 핸들러:

* 이(가) 호출됨 `ResourceNameRolloutConflictHandler`

* 이 핸들러를 사용하면 블루프린트 페이지가 우선 순위를 갖습니다.
* 이 처리기의 서비스 순위가 낮게 설정되어 있습니다(&quot;의 기본값 아래). `service.ranking` 속성)을 사용하는 경우 맞춤화된 처리기에 더 높은 순위가 필요하다고 가정합니다. 그러나 순위는 유연성을 보장하기 위한 절대적인 최소 조건이 아닙니다.

이 충돌 핸들러를 사용하면 블루프린트가 우선 순위를 갖습니다. 라이브 카피 페이지 `/b` 라이브 카피 분기 내에서 다음으로 이동 `/b_msm_moved`.

* live copy: `/b`

  (라이브 카피 내에서) 로 이동합니다. `/b_msm_moved`. 이는 백업 역할을 하며 콘텐츠가 손실되지 않도록 합니다.

   * `lc-level-1`은 이동하지 않습니다.

* 블루프린트: `/b`

  라이브 카피 페이지로 롤아웃됨 `/b`.

   * `bp-level-1` 는 라이브 카피로 롤아웃됩니다.

**롤아웃 이후**

<table>
 <tbody>
  <tr>
   <td><strong>롤아웃 이후의 블루프린트</strong></td>
   <td><strong>롤아웃 이후의 라이브 카피</strong><br /> </td>
   <td></td>
   <td><strong>롤아웃 이후의 라이브 카피</strong><br /> <br /> <br /> </td>
   <td><strong>롤아웃 이후 게시</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code><br /> <br /> (롤아웃된 블루프린트 페이지 b의 콘텐츠가 있음)<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code><br /> <br /> (라이브 카피 분기에 수동으로 생성된 페이지 b의 콘텐츠가 있음)</td>
   <td><code>b</code><br /> <br /> (변경 내용 없음, 라이브 카피 분기에 수동으로 생성된 원본 페이지 b의 콘텐츠(이제 b_msm_moved라고 함)를 포함합니다.)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code><br /> <br /> (변경 내용 없음)</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code><br /> <br /> (변경 내용 없음)</td>
  </tr>
 </tbody>
</table>

### 맞춤화된 핸들러 {#customized-handlers}

맞춤화된 충돌 처리기를 사용하면 고유한 규칙을 구현할 수 있습니다. 서비스 순위 메커니즘을 사용하여 이들 핸들러가 다른 핸들러와 상호 작용하는 방법을 지정할 수도 있습니다.

맞춤화된 충돌 핸들러는

* 요구 사항에 따라 이름이 지정될 수 있습니다.
* 요구 사항에 따라 개발/구성할 수 있습니다. 예를 들어 라이브 카피 페이지가 우선 순위를 갖도록 핸들러를 개발할 수 있습니다.
* 를 사용하여 구성되도록 디자인할 수 있습니다. [OSGi 구성](/help/sites-deploying/configuring-osgi.md); 특히

   * **서비스 순위**:

     다른 충돌 처리기와 관련된 순서를 정의합니다( `service.ranking`).

     기본값은 0입니다.

### 충돌 처리가 비활성화되었을 때 실행되는 비헤이비어 {#behavior-when-conflict-handling-deactivated}

수동으로 설정하는 경우 [충돌 처리 비활성화](#rollout-manager-and-conflict-handling) 그러면 AEM은 충돌이 발생한 페이지에 어떤 조치도 취하지 않습니다(충돌이 발생하지 않은 페이지는 예상대로 롤아웃됨).

>[!CAUTION]
>
>AEM은 이 동작을 명시적으로 구성해야 하므로 충돌이 무시되고 있음을 표시하지 않으므로 필수 동작이라고 가정합니다.

이 경우 라이브 카피가 사실상 우선됩니다. 블루프린트 페이지 `/b` 은 복사되지 않으며 라이브 카피 페이지 `/b` 그대로 두었습니다.

* 블루프린트: `/b`

  복사되지 않고 무시됩니다.

* live copy: `/b`

  그대로 유지됩니다.

<table>
 <caption>
   롤아웃 이후
 </caption>
 <tbody>
  <tr>
   <td><strong>롤아웃 이후의 블루프린트</strong></td>
   <td><strong>롤아웃 이후의 라이브 카피</strong><br /> <br /> <br /> </td>
   <td><strong>롤아웃 이후 게시</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code><br /> <br /> (변경 내용 없음, 라이브 카피 분기에 수동으로 생성된 페이지 b의 콘텐츠가 있음)</td>
   <td><code>b</code><br /> <br /> (변경 내용 없음, 라이브 카피 분기에 수동으로 생성된 페이지 b의 콘텐츠 포함)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code><br /> </td>
   <td><code> /lc-level-1</code><br /> <br /> (변경 내용 없음)</td>
   <td><code> /lc-level-1</code><br /> <br /> (변경 내용 없음)</td>
  </tr>
 </tbody>
</table>

### 서비스 순위 {#service-rankings}

[OSGi](https://www.osgi.org/) 서비스 순위를 사용하여 개별 충돌 핸들러의 우선 순위를 정의할 수 있습니다.
