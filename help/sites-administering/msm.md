---
title: '"컨텐츠 재사용:Multi Site Manager and Live Copy"'
seo-title: '"컨텐츠 재사용:Multi Site Manager and Live Copy"'
description: Live Copy 및 다중 사이트 관리자를 사용하여 컨텐츠를 재사용하는 방법에 대해 알아봅니다.
seo-description: Live Copy 및 다중 사이트 관리자를 사용하여 컨텐츠를 재사용하는 방법에 대해 알아봅니다.
uuid: 9f955226-8fc9-4357-b90c-c6896b0dc4b4
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: c21debc3-ecf4-4aa9-ab5a-18ddd5cf2fff
exl-id: 1e839845-fb5c-4200-8ec5-6ff744a96943
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2684'
ht-degree: 1%

---

# 컨텐츠 재사용:다중 사이트 관리자 및 Live Copy{#reusing-content-multi-site-manager-and-live-copy}

MSM(Multi Site Manager)을 사용하면 여러 위치에서 동일한 사이트 콘텐츠를 사용할 수 있습니다. MSM은 Live Copy 기능을 사용하여 이를 달성합니다.

* MSM을 사용하면 다음 작업을 수행할 수 있습니다.

   * 한 번 컨텐츠를 만든 다음
   * 이 컨텐츠를 복사해 같은 사이트나 다른 사이트의 다른 영역([라이브 카피](#live-copies))에서 다시 사용합니다.

* 그런 다음 MSM은 소스 컨텐츠와 Live Copy 간의 (라이브) 관계를 유지하여 다음과 같이 합니다.

   * 소스 컨텐츠를 변경하면 소스 및 Live Copy가 동기화됩니다(이러한 변경 사항을 Live Copy에도 적용).
   * 개별 하위 페이지 및/또는 구성 요소에 대한 라이브 관계를 연결을 끊음으로써 Live Copy의 컨텐츠를 조정할 수 있습니다. 이렇게 하면 소스 변경 사항이 더 이상 Live Copy에 적용되지 않습니다.

이 페이지와 다음 페이지에서는 관련 문제를 다룹니다.

* [Live Copy 생성 및 동기화](/help/sites-administering/msm-livecopy.md)
* [Live Copy 개요 콘솔](/help/sites-administering/msm-livecopy-overview.md)
* [Live Copy 동기화 구성](/help/sites-administering/msm-sync.md)
* [MSM 롤아웃 충돌](/help/sites-administering/msm-rollout-conflicts.md)
* [MSM 우수 사례](/help/sites-administering/msm-best-practices.md)

## 가능한 시나리오 {#possible-scenarios}

MSM 및 Live Copy에 대한 사용 사례가 많습니다. 일부 시나리오는 다음과 같습니다.

* **다국적 - 글로벌 - 로컬 회사**

   MSM에서 지원하는 일반적인 사용 사례는 여러 다국적 동일 언어 사이트에서 컨텐츠를 재사용하는 것입니다. 이렇게 하면 국가 변형을 허용하는 동안 코어 컨텐츠를 다시 사용할 수 있습니다.

   예를 들어 미국의 고객을 위해 We.Retail 참조 사이트 샘플의 영어 섹션이 만들어집니다. 이 사이트의 대부분의 컨텐츠는 다양한 국가 및 문화의 영어를 사용하는 고객을 충족하는 다른 We.Retail 사이트에도 사용될 수 있습니다. 핵심 컨텐츠는 모든 사이트에서 동일하게 유지되지만 지역을 조정할 수 있습니다.

   다음 구조는 미국, 영국, 캐나다 및 오스트레일리아 사이트에 사용할 수 있습니다.

   ```xml
   /content
       |- we.retail
           |- language-masters
               |- en
       |- we.retail
           |- us
               |- en
       |- we.retail
           |- gb
               |- en
       |- we.retail
           |- ca
               |- en
       |- we.retail
           |- au
               |- en
   ```

   >[!NOTE]
   >
   >MSM은 콘텐츠를 번역하지 않습니다. 필요한 구조를 만들고 컨텐츠를 배포하는 데 사용됩니다.
   >
   >
   >이러한 예를 확장하려면 [다국어 사이트의 컨텐츠 번역](/help/sites-administering/translation.md)을 참조하십시오.

* **전국 - 지부간 본사**

   또는 딜러망이 있는 회사는 개별 딜러를 위한 별도의 웹 사이트를 원할 수 있습니다. 각 사이트는 본사에서 제공하는 기본 사이트의 변형입니다. 여러 지역 사무소가 있는 단일 회사 또는 중앙 가맹상과 다수의 지역 가맹점들로 구성된 국가 프랜차이즈 시스템일 수 있습니다.

   본사는 핵심 정보를 제공할 수 있지만, 지역 엔티티는 연락처 세부 사항, 개설 시간 및 이벤트와 같은 로컬 정보를 추가할 수 있습니다.

   ```xml
   /content
       |- head-office-Berlin
       |- branch-Hamburg
       |- branch-Stuttgart
       |- branch-Munich
       |- branch-Frankfurt
   ```

* **여러 버전**

   또는 MSM을 사용하여 특정 하위 분기의 버전을 만들 수 있습니다. 예를 들어, 기본 정보가 일정하게 유지되며 업데이트된 기능만 변경해야 하는 특정 제품의 다른 버전에 대한 세부 정보를 포함하는 지원 하위 사이트를 참조하십시오.

   ```xml
   /content
       |- support
           |- product X
               |- v5.0
               |- v4.0
               |- v3.0
               |- v2.0
               |- v1.0
   ```

   >[!NOTE]
   >
   >이러한 시나리오에는 항상 간단한 복사본을 만드는지 아니면 Live Copy를 사용할지를 묻는 질문이 있습니다.
   >
   >균형은 다음과 같습니다.
   >
   >  * 여러 버전에서 코어 콘텐츠를 업데이트해야 하는 양입니다.
   >
   >대상:
   >
   >  * 개별 사본의 양을 조정해야 할 것입니다.


## UI의 MSM {#msm-from-the-ui}

MSM은 해당 콘솔의 다양한 옵션을 사용하여 UI에서 직접 액세스할 수 있습니다. 소개를 제공하려면 기본 위치가 다음과 같습니다.

* **사이트 만들기** (**사이트**)

   * MSM은 일반적인 컨텐츠를 공유하는 여러 웹 사이트를 관리하는 데 도움이 됩니다.예를 들어, 웹 사이트는 국제 대상을 위해 제공되므로 대부분의 컨텐츠는 각 개별 국가에 해당하는 컨텐츠의 하위 집합과 함께 모든 국가에서 일반적입니다. MSM을 사용하면 [소스 사이트](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)를 기반으로 하나 이상의 사이트를 자동으로 업데이트하는 라이브 카피를 만들 수 있습니다. 또한 공통 기본 구조를 적용하고, 여러 사이트에서 공통 컨텐츠를 사용하고, 일반적인 모양과 느낌을 유지하고, 사이트 간에 실제로 다른 컨텐츠를 관리하는 데 주력할 수 있습니다.
   * 소스를 지정하려면 사전 정의된 블루프린트 구성이 필요합니다.
   * (사전 정의된) 소스의 Live Copy를 만듭니다.
   * 사용자에게 **롤아웃** 단추를 제공합니다.

* **Live Copy 만들기** (**Sites**)

   * MSM을 사용하면 웹 사이트](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page);예를 들어 하위 분기를 복제하여 제품의 신규/업데이트된 버전에 대한 정보를 제공합니다.[
   * 임시 Live Copy를 만듭니다(블루프린트 구성이 필요 없음).
   * 모든 페이지/분기의 Live Copy를 만드는 데 (즉시) 사용할 수 있습니다.
   * **동기화**(**롤아웃** 단추를 제공하지 않음)가 필요합니다.

* **속성 보기** (**사이트**)

   * 적절한 경우 이 옵션은 관련 **Live Copy** y 또는 **블루프린트**&#x200B;에 대한 정보를 제공하여 [Live Copy](/help/sites-administering/msm-livecopy.md#monitoring-your-live-copy)를 모니터링하는 데 도움이 됩니다.

* **참조** (**사이트**)

   * [참조](/help/sites-authoring/basic-handling.md#references) 레일은 적절한 작업에 대한 액세스 권한과 함께 **라이브 카피**&#x200B;에 대한 정보를 제공합니다.

* **Live Copy 개요** (**Sites**)

   * 이 콘솔에서는 [블루프린트와 해당 Live Copy](/help/sites-administering/msm-livecopy-overview.md)를 보고 관리할 수 있습니다.

* **블루프린트** (**도구**  -  **사이트**)

   * 이 콘솔에서는 [블루프린트 구성을 만들고 관리할 수 있습니다](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration).

>[!NOTE]
>
>MSM 기능의 특징은 몇 가지 다른 AEM 기능(예: 시작, 카탈로그)에 사용됩니다.이 경우 live copy는 해당 기능에 의해 관리됩니다.

### 사용된 용어 {#terms-used}

다음 표에서는 MSM과 함께 사용되는 주요 용어에 대한 개요를 제공합니다.이러한 내용은 후속 섹션 및 페이지에서 더 자세히 다룹니다.

<table>
 <tbody>
  <tr>
   <td><strong>용어</strong></td>
   <td><strong>정의</strong></td>
   <td><strong>자세한 내용</strong></td>
  </tr>
  <tr>
   <td><strong>소스</strong></td>
   <td>원래 페이지입니다.</td>
   <td>블루프린트 및/또는 블루프린트 페이지와 동의어</td>
  </tr>
  <tr>
   <td><strong>Live Copy</strong></td>
   <td>롤아웃 구성에 정의된 대로 동기화 작업에 의해 유지 관리되는 소스 의 사본. </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Live Copy 구성</strong></td>
   <td>Live Copy에 대한 구성 세부 사항의 정의입니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>라이브 관계</strong><br /> </td>
   <td>주어진 리소스에 대한 상속의 유효 정의소스와 라이브 카피 사이의 연결입니다.<br /> </td>
   <td>소스에 대한 변경 사항을 Live Copy와 동기화할 수 있는지 확인합니다.</td>
  </tr>
  <tr>
   <td><strong>블루프린트</strong></td>
   <td>소스와 동의어.</td>
   <td>블루프린트 구성으로 정의할 수 있습니다.</td>
  </tr>
  <tr>
   <td><strong>블루프린트 구성</strong></td>
   <td>소스 경로를 지정하는 사전 정의된 구성입니다.</td>
   <td>블루프린트 구성에서 블루프린트 페이지를 참조하면 롤아웃 명령을 사용할 수 있습니다.</td>
  </tr>
  <tr>
   <td><strong>동기화</strong></td>
   <td>소스와 Live Copy 간의 컨텐츠 동기화를 위한 일반 용어입니다( <strong>Rollout</strong> 및 <strong>동기화</strong> 모두 사용).</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>롤아웃</strong><br /> </td>
   <td>소스에서 Live Copy에 동기화합니다.<br /> 작성자(블루프린트 페이지)나 시스템 이벤트(롤아웃 구성으로 정의됨)에 의해 트리거될 수 있습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>롤아웃 구성</strong></td>
   <td>동기화할 속성, 방법 및 시기를 결정하는 규칙입니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>동기화</strong></td>
   <td>Livecopy 페이지에서 수행되는 동기화를 위한 수동 요청입니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>상속</strong></td>
   <td>동기화가 발생할 때 Live Copy 페이지/구성 요소는 소스 페이지/구성 요소의 컨텐츠를 상속합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>일시 중단</strong></td>
   <td>Live Copy와 블루프린트 페이지 간의 라이브 관계를 일시적으로 제거합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>분리</strong></td>
   <td>Live Copy와 블루프린트 페이지 간의 라이브 관계를 영구적으로 제거합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>재설정</strong></td>
   <td><p>Live Copy 페이지를 다음으로 재설정:</p>
    <ul>
     <li>모든 상속 취소 및<br /> 제거 </li>
     <li>페이지를 소스 페이지와 동일한 상태로 반환합니다.</li>
    </ul> <p>재설정은 페이지 속성, 단락 시스템 및 구성 요소에 수행한 변경 사항에 영향을 줍니다.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>얕은</strong></td>
   <td>단일 페이지의 Live Copy.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>깊이</strong></td>
   <td>페이지의 Live Copy와 해당 하위 페이지.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>개체 이름에 대해서는 [Java API](/help/sites-developing/extending-msm.md#overview-of-the-java-api)개요 를 참조하십시오.

## Live Copy {#live-copies}

MSM Live Copy는 원래 소스와의 라이브 관계가 유지 관리되는 특정 사이트 콘텐츠의 사본입니다.

* Live Copy는 소스의 컨텐츠를 상속합니다.
* 동기화는 소스에 변경 사항이 있을 때 실제 컨텐츠 전송을 수행합니다.
* Live Copy는 다음 중 하나로 간주할 수 있습니다.

   * 약식:단일 페이지
   * 깊이:페이지와 해당 하위 페이지

* 롤아웃 구성이라고 하는 동기화 규칙은 동기화되는 속성과 동기화 발생 시기를 결정합니다.

이전 예에서 `/content/we-retail/language-masters/en`은 영어로 된 글로벌 마스터 사이트입니다. 이 사이트의 컨텐츠를 다시 사용하려면 MSM Live Copy가 만들어집니다.

* `/content/we-retail/language-masters/en` 아래의 컨텐츠는 소스입니다.

* `/content/we-retail/language-masters/en` 아래의 컨텐츠는 `/content/we-retail/us/en/`, `/content/we-retail/gb/en`, `/content/we-retail/ca/en` 및 `/content/we-retail/au/en` 노드 아래에 복사됩니다. Live Copy입니다.

* 작성자가 `/content/we-retail/language-masters/en` 아래의 페이지를 변경합니다.
* 트리거되면 MSM은 이러한 변경 사항을 Live Copy에 동기화합니다.

### 라이브 카피 - 구성 {#live-copies-composition}

>[!NOTE]
>
>이 섹션의 다이어그램과 설명은 잠재적인 Live Copy의 스냅샷을 나타냅니다. 포괄적이지 않지만 특정 특성을 강조 표시하는 개요를 제공합니다.

처음에 Live Copy를 만들 때 선택한 소스 페이지는 Live Copy에서 1:1에 반영됩니다. 그런 다음 Live Copy 내에서 새로운 리소스(페이지 및/또는 단락)를 직접 만들 수도 있으므로 이러한 변형과 변형이 동기화에 미치는 영향을 이해하는 것이 좋습니다. 가능한 컴포지션은 다음과 같습니다.

* [Live Copy가 아닌 페이지가 있는 Live Copy](#live-copy-with-non-live-copy-pages)
* [중첩된 라이브 카피](#nested-live-copies)

Live Copy의 기본 양식은 다음과 같습니다.

* 선택한 소스 페이지를 1:1 기준으로 반영하는 Live Copy 페이지.
* 하나의 구성 정의입니다.
* 모든 리소스에 대해 정의된 라이브 관계:

   * Live Copy 리소스를 블루프린트/소스와 연결합니다.
   * 상속 및 롤아웃을 구현할 때 사용됩니다.

* 변경 사항은 요구 사항에 따라 [동기화된](/help/sites-administering/msm-livecopy.md#synchronizing-your-live-copy)일 수 있습니다.

![chlimage_1-367](assets/chlimage_1-367.png)

#### Live Copy가 아닌 페이지가 있는 Live Copy {#live-copy-with-non-live-copy-pages}

AEM에서 Live Copy를 만들면 Live Copy 분기를 보고 탐색할 수 있으며 Live Copy 분기에서 일반적인 AEM 기능을 사용할 수 있습니다. 즉, 사용자나 프로세스는 Live Copy 분기(예: )에서 새 리소스(페이지 및/또는 단락)를 만들 수 있습니다.`myCanadaOnlyProduct`)

* 이러한 리소스는 소스/블루프린트 페이지와 라이브 관계가 없으며 동기화되지 않습니다.
* MSM이 특별한 사례에 따라 처리하는 시나리오가 발생할 수 있습니다. 예를 들어, 소스/블루프린트 및 Live Copy 분기 모두에서 위치 및 이름이 동일한 페이지를 만들 때(또는 프로세스). 이러한 경우 자세한 내용은 [MSM 롤아웃 충돌](/help/sites-administering/msm-rollout-conflicts.md)을 참조하십시오.

![chlimage_1-368](assets/chlimage_1-368.png)

#### 중첩된 라이브 카피 {#nested-live-copies}

기존 Live Copy](#live-copy-with-non-live-copy-pages) 내에서 [새 페이지를 만들 때 이 새 페이지를 다른 블루프린트의 Live Copy로도 설정할 수 있습니다. 이를 중첩된 Live Copy라고 하며, 여기서 두 번째(내부) Live Copy의 동작은 다음의 방식으로 첫 번째(외부) Live Copy의 영향을 받습니다.

* 최상위 Live Copy에 대해 트리거된 딥 롤아웃을 중첩된 Live Copy로 계속할 수 있습니다(예: 트리거가 일치하는 경우).
* 소스 사이의 모든 링크는 Live Copy 내에서 다시 작성됩니다.

   예를 들어, 두 번째에서 첫 번째 블루프린트로의 링크는 중첩된/두 번째 Live Copy에서 첫 번째 Live Copy로의 링크로 다시 작성됩니다.

![chlimage_1-369](assets/chlimage_1-369.png)

>[!NOTE]
>
>Live Copy 분기 내에서 페이지를 이동/이름을 변경하는 경우(내부적으로) 이 페이지는 중첩된 Live Copy로 처리되어 AEM에서 관계를 추적합니다.

#### 누적 라이브 카피 {#stacked-live-copies}

Live Copy를 얕은 Live Copy의 자식으로 만들 때 누적 Live Copy라고 합니다. 이 변수는 [중첩된 Live Copy](#nested-live-copies)와 동일한 방식으로 동작합니다.

### 소스, 블루프린트 및 블루프린트 구성 {#source-blueprints-and-blueprint-configurations}

페이지의 모든 페이지 또는 분기를 Live Copy 소스로 사용할 수 있습니다.

그러나 MSM에서는 소스 경로를 지정하는 블루프린트 구성을 정의할 수도 있습니다. 블루프린트 구성을 사용하면 다음과 같은 이점이 있습니다.

* 작성자가 블루프린트에서 이 블루프린트에서 상속되는 Live Copy에 수정 사항을 푸시하기 위해 **롤아웃** 옵션을 사용할 수 있도록 허용합니다.
* 작성자가 **사이트 만들기**;를 사용하도록 허용언어를 쉽게 선택하고 live copy 구조를 구성할 수 있습니다.
* 블루프린트와 관계가 있는 Live Copy에 대한 기본 롤아웃 구성을 정의합니다.

Live Copy 소스는 일반 페이지 또는 블루프린트 구성으로 둘러싸인 페이지일 수 있습니다. 둘 다 유효한 사용 사례입니다.

소스는 Live Copy에 대한 블루프린트를 구성합니다. 블루프린트는 다음 중 하나를 수행할 때 정의됩니다.

* [블루프린트 구성 만들기](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)

   구성은 Live Copy를 만드는 데 사용할 페이지를 미리 정의합니다.

* [페이지의 Live Copy 만들기](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   Live Copy(소스 페이지)를 만드는 데 사용되는 페이지는 블루프린트 페이지입니다.

   소스 페이지는 블루프린트 구성으로 참조되거나 참조되지 않습니다.

### 롤아웃 및 동기화 {#rollout-and-synchronize}

롤아웃은 Live Copy를 소스와 동기화하는 중앙 MSM 작업입니다. 롤아웃을 수동으로 수행하거나 자동으로 수행할 수 있습니다.

* [롤아웃 구성](#rollout-configurations)을(를) 정의하여 특정 [events](/help/sites-administering/msm-sync.md#rollout-triggers)으로 인해 롤아웃이 자동으로 발생할 수 있습니다.
* 블루프린트 페이지를 작성할 때 [롤아웃](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) 명령을 사용하여 변경 사항을 Live Copy에 푸시할 수 있습니다.

   **블루프린트** 구성에서 참조하는 블루프린트 페이지에서 롤아웃 명령을 사용할 수 있습니다.

   ![chlimage_1-370](assets/chlimage_1-370.png)

* Live Copy 페이지를 작성할 때 [동기화](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) 명령을 사용하여 소스에서 Live Copy로 변경 사항을 가져올 수 있습니다.

   **동기화** 명령은 항상 Live Copy 페이지에서 사용할 수 있습니다(소스/블루프린트 페이지가 블루프린트 구성으로 감싸지는지 여부에 관계없이).

   ![chlimage_1-371](assets/chlimage_1-371.png)

### 롤아웃 구성 {#rollout-configurations}

롤아웃 구성은 Live Copy가 소스 컨텐츠와 동기화되는 시기 및 방법을 정의합니다. 롤아웃 구성은 트리거와 하나 이상의 동기화 작업으로 구성됩니다.

* **트리거**

   트리거는 소스 페이지의 활성화와 같이 라이브 작업 동기화가 발생하는 이벤트입니다. MSM은 사용할 수 있는 트리거를 정의합니다.

* **동기화 작업**

   Live Copy에서 수행되어 소스와 동기화됩니다. 작업의 예로는 컨텐츠 복사, 하위 노드 순서 지정 및 Live Copy 페이지 활성화가 있습니다. MSM은 많은 동기화 작업을 제공합니다.

   >[!NOTE]
   >
   >Java API를 사용하여 인스턴스에 대한 사용자 지정 작업을 만들 수 있습니다.

롤아웃 구성을 다시 사용할 수 있으므로 두 개 이상의 Live Copy에서 동일한 롤아웃 구성을 사용할 수 있습니다. 표준 설치에는 여러 [롤아웃 구성](/help/sites-administering/msm-sync.md#installed-rollout-configurations)이 포함되어 있습니다.

### 롤아웃 충돌 {#rollout-conflicts}

롤아웃은 복잡해질 수 있습니다. 특히 작성자가 소스와 Live Copy 모두에서 컨텐츠를 편집할 때 복잡해질 수 있습니다. 따라서 롤아웃](/help/sites-administering/msm-rollout-conflicts.md) 중에 발생할 수 있는 [충돌을 AEM에서 처리하는 방법을 이해하는 것이 유용합니다.

### 상속 및 동기화 일시 중단 및 취소 {#suspending-and-cancelling-inheritance-and-synchronization}

Live Copy의 각 페이지 및 구성 요소는 라이브 관계를 통해 소스 페이지 및 구성 요소와 연결됩니다. 라이브 관계는 소스에서 Live Copy 컨텐츠의 동기화를 구성합니다.

페이지 속성 및 구성 요소를 변경할 수 있도록 Live Copy 페이지에 대한 Live Copy 상속을 일시 중단&#x200B;**할 수 있습니다.** 상속을 일시 중단하면 페이지 속성 및 구성 요소가 더 이상 소스와 동기화되지 않습니다.

개별 페이지를 편집할 때 작성자는 구성 요소에 대해 **상속 취소**&#x200B;할 수 있습니다. 상속이 취소되면 라이브 관계가 일시 중단되고 해당 구성 요소에 대한 동기화가 발생하지 않습니다. 상속 및 동기화를 취소하면 컨텐츠의 하위 섹션을 사용자 지정해야 할 때 유용합니다.

### Live Copy {#detaching-a-live-copy} 분리

블루프린트에서 [Live Copy](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy)를 분리하여 모든 연결을 제거할 수도 있습니다.

>[!CAUTION]
>
>분리 작업은 영구적이고 비되돌릴 수 있습니다.

분리는 Live Copy와 블루프린트 페이지 간의 라이브 관계를 영구적으로 제거합니다. 모든 MSM 관련 속성은 Live Copy에서 제거되고 Live Copy 페이지는 독립형 복사본이 됩니다.

>[!NOTE]
>
>자세한 내용은 [Live Copy 분리](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) 를 참조하십시오.하위 및 상위 페이지에 대한 관련 영향 포함.

## MSM {#standard-steps-for-using-msm} 사용을 위한 표준 단계

다음 단계에서는 MSM을 사용하여 컨텐츠를 재사용하고 변경 사항을 Live Copy에 동기화하는 표준 절차를 설명합니다.

1. 소스 사이트의 컨텐츠를 개발합니다.
1. 사용할 롤아웃 구성을 결정합니다.

   1. MSM [은 많은 사용 사례를 충족할 수 있는 여러 롤아웃 구성](/help/sites-administering/msm-sync.md#installed-rollout-configurations)을 설치합니다.
   1. 필요한 경우 [롤아웃 구성을 생성](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration)할 수도 있습니다.

1. [을(를) 사용할 롤아웃 구성을 지정하고 필요에 따라 구성합니다.](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use)
1. 필요한 경우 Live Copy의 소스 컨텐츠를 식별하는 블루프린트 구성](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)을 만듭니다.[
1. [Live Copy를 만듭니다](/help/sites-administering/msm-livecopy.md#creating-a-live-copy).
1. 필요에 따라 소스 컨텐츠를 변경합니다. 조직에서 설정한 일반 컨텐츠 검토 및 승인 프로세스를 사용해야 합니다.
1. [블루프린트](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) 를 롤아웃하거나  [라이브 카피본을 ](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) 변경 사항과 동기화합니다.

## MSM {#customizing-msm} 사용자 지정

MSM은 컨텐츠를 공유할 때 발생할 수 있는 매우 복잡한 구현에 맞게 도구를 제공합니다.

* **사용자 지정 롤아웃 구성**
   [설치된 ](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) 롤아웃 구성이 요구 사항을 충족하지 않을 때 롤아웃 구성을 만듭니다. 사용 가능한 롤아웃 트리거 및 동기화 작업을 사용할 수 있습니다.

* **사용자 지정 동기화 작업**
   [설치된 작업](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action) 이 특정 애플리케이션 요구 사항을 충족하지 않을 경우 사용자 지정 동기화 작업을 생성합니다. MSM은 사용자 지정 동기화 작업을 만들기 위한 Java API를 제공합니다.

## 우수 사례 {#best-practices}

[MSM 우수 사례](/help/sites-administering/msm-best-practices.md) 페이지에는 구현과 관련된 중요한 정보가 포함되어 있습니다.
