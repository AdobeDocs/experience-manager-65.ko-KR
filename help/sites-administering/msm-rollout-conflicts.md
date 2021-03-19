---
title: MSM 롤아웃 충돌
seo-title: MSM 롤아웃 충돌
description: 다중 사이트 관리자 롤아웃 충돌을 처리하는 방법을 알아봅니다.
seo-description: 다중 사이트 관리자 롤아웃 충돌을 처리하는 방법을 알아봅니다.
uuid: 7a640905-aae2-498e-b95c-2c73008fa1cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 16db5334-604f-44e2-9993-10d683dee5bb
feature: 다중 사이트 관리자
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 0%

---


# MSM 롤아웃 충돌{#msm-rollout-conflicts}

블루프린트 분기 및 종속 Live Copy 분기 모두에서 페이지 이름이 같은 새 페이지가 작성되면 충돌이 발생할 수 있습니다.

롤아웃 시 이러한 충돌을 처리하고 해결해야 합니다.

## 충돌 처리 {#conflict-handling}

페이지가 충돌하는 경우(블루프린트 및 Live Copy 분기에) MSM을 사용하여 페이지가 어떻게 처리되어야 하는지를 정의할 수 있습니다.

롤아웃이 차단되지 않도록 가능한 정의는 다음과 같습니다.

* 롤아웃 시 우선 순위를 가지는 페이지(블루프린트 또는 live copy)
* 이름을 변경할 페이지(및 방법),
* 게시된 모든 컨텐츠에 미치는 영향

   기본적으로 AEM(즉시 사용)의 기본 동작은 게시된 컨텐트에 영향을 주지 않습니다. 따라서 Live Copy 분기에 수동으로 만든 페이지가 게시되면 충돌 처리 및 롤아웃 후에도 해당 컨텐츠가 게시됩니다.

표준 기능 외에도 사용자 정의된 충돌 핸들러를 추가하여 다른 규칙을 구현할 수 있습니다. 또한 개별 프로세스로 게시 작업을 허용할 수 있습니다.

### 예제 시나리오 {#example-scenario}

다음 섹션에서는 블루프린트와 Live Copy 분기(수동으로 만들어짐)에서 만든 새 페이지 `b`의 예를 사용하여 다양한 충돌 해결 방법을 보여 줍니다.

* 블루프린트:`/b`

   마스터 페이지;하위 페이지 1개, bp-level-1로 채웁니다.

* live copy:`/b`

   Live Copy 분기에 수동으로 만든 페이지;하위 페이지가 1개인 경우 `lc-level-1`.

   * 하위 페이지와 함께 `/b` 게시에서 활성화됩니다.

**롤아웃 전**

<table>
 <tbody>
  <tr>
   <td><strong>롤아웃 전에 미리 보기</strong></td>
   <td><strong>롤아웃 전 라이브 복사</strong></td>
   <td><strong>롤아웃 전에 게시</strong></td>
  </tr>
  <tr>
   <td><code>b</code> <br /> (블루프린트 분기에 만들어짐, 롤아웃 준비)<br /> </td>
   <td><code>b</code> <br /> (live copy 분기에 수동으로 만들기)<br /> </td>
   <td><code>b</code> <br /> (live copy 분기에 수동으로 만든 페이지 b의 컨텐츠가 포함되어 있습니다.)</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> (live copy 분기에 수동으로 만들기)<br /> </td>
   <td><code> /lc-level-1</code> <br /> (live copy 분기에 수동으로 만든 페이지<br /> 하위 수준-1의 내용이 포함되어 있습니다.)</td>
  </tr>
 </tbody>
</table>

## 롤아웃 관리자 및 충돌 처리 {#rollout-manager-and-conflict-handling}

롤아웃 관리자를 사용하여 충돌 관리를 활성화 또는 비활성화할 수 있습니다.

이 작업은 **일 CQ WCM 롤아웃 관리자**&#x200B;의 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)을 사용하여 수행됩니다.

* **수동으로 만든 페이지와 충돌** 처리:

   ( `rolloutmgr.conflicthandling.enabled`)

   롤아웃 관리자가 Live Copy에서 만든 페이지와 블루프린트에 존재하는 이름이 충돌하는 문제를 처리해야 하는 경우 true로 설정합니다.

충돌 관리가 비활성화된 경우 AEM에는 [사전 정의된 동작이 있습니다](#behavior-when-conflict-handling-deactivated).

## 충돌 핸들러 {#conflict-handlers}

AEM에서는 블루프린트에서 Live Copy로 컨텐츠를 롤아웃할 때 존재하는 페이지 충돌을 해결하기 위해 충돌 핸들러를 사용합니다. 페이지 이름 바꾸기는 이러한 충돌을 해결하는 일반적인 방법 중 하나입니다. 둘 이상의 충돌 핸들러를 사용하여 여러 가지 비헤이비어를 선택할 수 있습니다.

AEM 제공 서비스:

* [기본 충돌 처리기](#default-conflict-handler):

   * `ResourceNameRolloutConflictHandler`

* [사용자 지정된 핸들러](#customized-handlers)를 구현할 수 있습니다.
* 각 개별 핸들러의 우선 순위를 설정할 수 있는 서비스 등급 메커니즘입니다. 등급이 가장 높은 서비스가 사용됩니다.

### 기본 충돌 처리기 {#default-conflict-handler}

기본 충돌 핸들러:

* `ResourceNameRolloutConflictHandler`이라고 함

* 이 핸들러를 사용하면 블루프린트 페이지에 우선 순위가 지정됩니다.
* 이 핸들러의 서비스 등급이 낮습니다(&quot;예:사용자 지정된 처리기에 높은 등급이 필요할 것으로 가정할 때 `service.ranking` 속성의 기본값 아래. 하지만, 등급은 필요한 경우 유연성을 보장하는 절대적인 최소값이 아닙니다.

이 충돌 핸들러는 블루프린트에 우선 순위를 지정합니다. Live Copy 페이지 `/b`이(가) Live Copy 분기 내에) `/b_msm_moved`로 이동되었습니다.

* live copy:`/b`

   Live Copy 내에서 `/b_msm_moved`으로 이동됩니다. 이렇게 하면 백업 기능이 수행되므로 내용이 손실되지 않습니다.

   * `lc-level-1` 가 이동되지 않았습니다.

* 블루프린트:`/b`

   Live Copy 페이지 `/b`에 롤아웃됩니다.

   * `bp-level-1` live copy로 롤아웃됩니다.

**롤아웃 후**

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
   <td><code>b</code> <br /> (롤아웃된 블루프린트 페이지 b의 내용이 있음)<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code> <br /> (live copy 분기에 수동으로 만든 페이지 b의 컨텐츠가 있음)</td>
   <td><code>b</code> <br /> 변경 없음는 live copy 분기에 수동으로 만들어졌고 이제 b_msm_moved라고 하는 원본 페이지의 컨텐츠를 포함합니다.<br /> </td>
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

### 사용자 지정된 핸들러 {#customized-handlers}

사용자 지정된 충돌 핸들러를 사용하여 고유한 규칙을 구현할 수 있습니다. 서비스 등급 메커니즘을 사용하여 다른 핸들러와 상호 작용하는 방법을 정의할 수도 있습니다.

사용자 지정된 충돌 핸들러는 다음과 같은 일을 할 수 있습니다.

* 필요에 따라 이름을 지정합니다.
* 사용자의 요구 사항에 따라 개발/구성예를 들어 Live Copy 페이지에 우선 순위가 지정되도록 핸들러를 개발할 수 있습니다.
* [OSGi 구성](/help/sites-deploying/configuring-osgi.md);을 사용하여 구성할 수 있습니다.특히 다음과 같은 경우에 해당됩니다.

   * **서비스 등급**:

      다른 충돌 핸들러( `service.ranking`)와 관련된 순서를 정의합니다.

      기본값은 0입니다.

### 충돌 처리가 비활성화된 경우 동작 {#behavior-when-conflict-handling-deactivated}

[충돌 처리 비활성화](#rollout-manager-and-conflict-handling)를 수동으로 수행하는 경우 AEM은 충돌하는 페이지에 대해 작업을 수행하지 않습니다(충돌 없는 페이지는 예상대로 롤아웃됨).

>[!CAUTION]
>
>AEM에서는 이 비헤이비어를 명시적으로 구성해야 하므로 충돌이 무시되고 있음을 표시하지 않으므로 이 동작이 필수 동작이라고 가정합니다.

이 경우 Live Copy가 효과적으로 우선합니다. 블루프린트 페이지 `/b`이(가) 복사되지 않고 Live Copy 페이지 `/b`은(는) 그대로 유지됩니다.

* 블루프린트:`/b`

   은 전혀 복사되지 않지만 무시됩니다.

* live copy:`/b`

   동일하게 유지

<table>
 <caption>
   롤아웃 후
 </caption>
 <tbody>
  <tr>
   <td><strong>롤아웃 후 블루프린트</strong></td>
   <td><strong>롤아웃 후 live copy</strong><br /> <br /> <br /> </td>
   <td><strong>롤아웃 후 게시</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> 변경 없음live copy 분기에 수동으로 만든 페이지 b의 컨텐츠가 있음)</td>
   <td><code>b</code> <br /> 변경 없음live copy 분기에 수동으로 만든 페이지 b의 컨텐츠를 포함합니다.)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code> </td>
   <td><code> /lc-level-1</code> <br /> (변경 없음)</td>
   <td><code> /lc-level-1</code> <br /> (변경 없음)</td>
  </tr>
 </tbody>
</table>

### 서비스 등급 {#service-rankings}

[OSGi](https://www.osgi.org/) 서비스 등급을 사용하여 개별 충돌 핸들러의 우선 순위를 정의할 수 있습니다.
