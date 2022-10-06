---
title: MSM 롤아웃 충돌
seo-title: MSM Rollout Conflicts
description: 다중 사이트 관리자 롤아웃 충돌을 처리하는 방법을 알아봅니다.
seo-description: Learn how to deal with Multi Site Manager rollout conflicts.
uuid: 7a640905-aae2-498e-b95c-2c73008fa1cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 16db5334-604f-44e2-9993-10d683dee5bb
feature: Multi Site Manager
exl-id: e145e79a-c363-4a33-b9f9-99502ed20563
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 29%

---

# MSM 롤아웃 충돌{#msm-rollout-conflicts}

블루프린트 분기와 종속 Live Copy 분기 모두에서 페이지 이름이 동일한 새 페이지를 만들면 충돌이 발생할 수 있습니다.

이러한 충돌은 롤아웃 시 처리 및 해결해야 합니다.

## 충돌 처리 {#conflict-handling}

페이지가 충돌하는 경우(블루프린트 및 Live Copy 분기에) MSM을 사용하여 페이지를 처리하는 방법을 정의할 수 있습니다(또는 있더라도).

롤아웃을 차단하지 않도록 다음과 같은 정의를 사용할 수 있습니다.

* 롤아웃 중에 우선 순위가 있는 페이지(블루프린트 또는 live copy)
* 어떤 페이지의 이름을 바꿀(및 방법),
* 게시된 모든 컨텐츠에 미치는 영향

   AEM(즉시 사용 가능)의 기본 동작은 게시된 컨텐츠는 영향을 받지 않습니다. 따라서 Live Copy 분기에서 수동으로 만든 페이지가 게시되었더라도 충돌 처리 및 롤아웃 후에도 해당 컨텐츠가 계속 게시됩니다.

표준 기능 이외에도 맞춤화된 충돌 처리기를 추가하여 다른 규칙을 구현할 수 있습니다. 또한 개별 프로세스로 게시 작업을 허용할 수도 있습니다.

### 예시 상황 {#example-scenario}

다음 섹션에서는 새 페이지의 예를 사용합니다 `b`와 함께 블루프린트와 live copy 분기(수동으로 생성됨)에서 작성되어 다양한 충돌 해결 방법을 보여줍니다.

* 블루프린트: `/b`

   마스터 페이지 하위 페이지 1개, bp-level-1 사용.

* live copy: `/b`

   Live Copy 분기에서 수동으로 만든 페이지입니다. 하위 페이지 1개 사용 `lc-level-1`.

   * 게시에서 하위 페이지와 함께 `/b`로 활성화됨.

**롤아웃 이전**

<table>
 <tbody>
  <tr>
   <td><strong>롤아웃 전 블루프린트</strong></td>
   <td><strong>롤아웃 전 live copy</strong></td>
   <td><strong>롤아웃 전 게시</strong></td>
  </tr>
  <tr>
   <td><code>b</code> <br /> (블루프린트 분기에 만들어짐, 롤아웃 준비)<br /> </td>
   <td><code>b</code> <br /> (live copy 분기에 수동으로 생성됨)<br /> </td>
   <td><code>b</code> <br /> (live copy 분기에 수동으로 만든 페이지 b의 컨텐츠가 포함되어 있습니다.)</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> (live copy 분기에 수동으로 생성됨)<br /> </td>
   <td><code> /lc-level-1</code> <br /> (페이지의 컨텐츠 포함)<br /> live copy 분기에 수동으로 생성된 하위 수준-1)</td>
  </tr>
 </tbody>
</table>

## 롤아웃 관리자 및 충돌 처리 {#rollout-manager-and-conflict-handling}

롤아웃 관리자를 사용하여 충돌 관리를 활성화 또는 비활성화할 수 있습니다.

이 작업은 [OSGi 구성](/help/sites-deploying/configuring-osgi.md) 의 **Day CQ WCM Rollout Manager**:

* **수동으로 만든 페이지와 충돌 처리**:

   ( `rolloutmgr.conflicthandling.enabled`)

   롤아웃 관리자가 블루프린트에 있는 이름으로 Live Copy에서 만든 페이지의 충돌을 처리해야 하는 경우 true로 설정합니다.

AEM에 있음 [충돌 관리가 비활성화될 때 미리 정의된 동작](#behavior-when-conflict-handling-deactivated).

## 충돌 처리기 {#conflict-handlers}

AEM에서는 충돌 핸들러를 사용하여 블루프린트에서 Live Copy로 컨텐츠를 롤아웃할 때 존재하는 페이지 충돌을 해결합니다. 페이지 이름 바꾸기는 이러한 충돌을 해결하는 단일 방법입니다. 하나 이상의 충돌 처리기를 작동하여 다양한 비헤이비어를 실행할 수 있습니다.

AEM은 다음을 제공합니다.

* [기본 충돌 처리기](#default-conflict-handler):

   * `ResourceNameRolloutConflictHandler`

* [맞춤화된 처리기](#customized-handlers) 구현 가능성.
* 각 개별 처리기의 우선 순위를 설정할 수 있는 서비스 순위 메커니즘. 순위가 가장 높은 서비스가 사용됩니다.

### 기본 충돌 처리기 {#default-conflict-handler}

기본 충돌 처리기:

* 이 호출됨 `ResourceNameRolloutConflictHandler`

* 이 처리기를 사용하면 블루프린트 페이지가 우선 순위를 갖습니다.
* 이 처리기의 서비스 등급이 낮습니다(&quot;예: 아래에 있는 `service.ranking` 속성)을 지정할 때 사용자 지정된 처리기에 더 높은 등급이 필요합니다. 그러나 순위는 유연성을 보장하기 위한 절대적인 최소 조건이 아닙니다.

이 충돌 처리기를 사용하면 블루프린트가 우선 순위를 갖습니다. Live Copy 페이지 `/b` 가 (live copy 분기 내)로 이동됩니다. `/b_msm_moved`.

* live copy: `/b`

   (Live Copy 내에서)로 이동됩니다. `/b_msm_moved`. 이는 백업 역할을 하며 콘텐츠가 손실되지 않도록 합니다.

   * `lc-level-1`은 이동하지 않습니다.

* 블루프린트: `/b`

   Live Copy 페이지로 롤아웃됩니다. `/b`.

   * `bp-level-1` 가 livecopy로 롤아웃됩니다.

**롤아웃 이후**

<table>
 <tbody>
  <tr>
   <td><strong>롤아웃 후 블루프린트</strong></td>
   <td><strong>롤아웃 후 live copy</strong><br /> </td>
   <td></td>
   <td><strong>롤아웃 후 live copy</strong><br /> <br /> <br /> </td>
   <td><strong>롤아웃 후 게시</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> (롤아웃된 블루프린트 페이지 b의 컨텐츠가 있음)<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code> <br /> (live copy 분기에서 수동으로 만든 페이지 b의 컨텐츠가 있음)</td>
   <td><code>b</code> <br /> 변경 금지 는 live copy 분기에서 수동으로 만들어졌고 이제 b_msm_moved)인 원래 페이지 b의 컨텐츠를 포함합니다.<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> (변경 없음)</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code> <br /> (변경 없음)</td>
  </tr>
 </tbody>
</table>

### 맞춤화된 처리기 {#customized-handlers}

맞춤화된 충돌 처리기를 사용하면 나만의 규칙을 구현할 수 있습니다. 서비스 순위 메커니즘을 사용하여 이들 처리기가 다른 처리기와 상호 작용하는 방법을 지정할 수도 있습니다.

맞춤화된 충돌 처리기는

* 요구 사항에 따라 이름이 지정될 수 있습니다.
* 필요에 따라 개발/구성 예를 들어 live copy 페이지에 우선순위가 지정되도록 핸들러를 개발할 수 있습니다.
* 을 사용하여 구성할 수 있도록 설계할 수 있습니다. [OSGi 구성](/help/sites-deploying/configuring-osgi.md); 특히

   * **서비스 등급**:

      다른 충돌 핸들러와 관련된 순서를 정의합니다( `service.ranking`).

      기본값은 0입니다.

### 충돌 처리가 비활성화된 경우 동작 {#behavior-when-conflict-handling-deactivated}

수동으로 [충돌 처리 비활성화](#rollout-manager-and-conflict-handling) 그런 다음 AEM에서 충돌하는 페이지에 대해 작업을 수행하지 않습니다(충돌하지 않은 페이지가 예상대로 롤아웃됨).

>[!CAUTION]
>
>AEM에서는 이 동작을 명시적으로 구성해야 하므로 충돌이 무시되고 있음을 표시하지 않으므로 이 동작이 필수 동작이라고 가정합니다.

이 경우 Live Copy가 효과적으로 우선합니다. 블루프린트 페이지 `/b` 이 복사되지 않고 live copy 페이지 `/b` 은 그대로 둡니다.

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
   <td><strong>롤아웃 후 블루프린트</strong></td>
   <td><strong>롤아웃 후 live copy</strong><br /> <br /> <br /> </td>
   <td><strong>롤아웃 후 게시</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> 변경 금지 에는 live copy 분기에서 수동으로 만든 페이지 b의 컨텐츠가 있습니다.</td>
   <td><code>b</code> <br /> 변경 금지 live copy 분기에 수동으로 만든 페이지 b의 컨텐츠를 포함합니다.<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code> </td>
   <td><code> /lc-level-1</code> <br /> (변경 없음)</td>
   <td><code> /lc-level-1</code> <br /> (변경 없음)</td>
  </tr>
 </tbody>
</table>

### 서비스 순위 {#service-rankings}

[OSGi](https://www.osgi.org/) 서비스 순위를 사용하여 개별 충돌 처리기의 우선 순위를 정의할 수 있습니다.
