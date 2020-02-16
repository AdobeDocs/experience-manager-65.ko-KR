---
title: '"컨텐츠 재활용:Multi Site Manager and Live Copy"'
seo-title: '"컨텐츠 재활용:Multi Site Manager and Live Copy"'
description: Live Copy 및 Multi Site Manager를 사용하여 컨텐츠를 재사용하는 방법에 대해 학습합니다.
seo-description: Live Copy 및 Multi Site Manager를 사용하여 컨텐츠를 재사용하는 방법에 대해 학습합니다.
uuid: 9f955226-8fc9-4357-b90c-c6896b0dc4b4
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: c21debc3-ecf4-4aa9-ab5a-18ddd5cf2fff
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 컨텐츠 재활용:다중 사이트 관리자 및 Live Copy{#reusing-content-multi-site-manager-and-live-copy}

MSM(Multi Site Manager)을 사용하면 여러 위치에서 동일한 사이트 컨텐츠를 사용할 수 있습니다. MSM 파섹

* MSM을 사용하여 다음을 수행할 수 있습니다.

   * 한 번 만든 다음
   * 이 콘텐트를 같은 사이트나 다른 사이트의 다른 영역([Live Copy](#live-copies))에 복사하거나 다시 사용합니다.

* 그런 다음 MSM은 소스 컨텐츠와 Live Copy 간의 (라이브) 관계를 유지하여 다음과 같이 합니다.

   * 소스 컨텐츠를 변경하면 소스 및 Live Copy가 동기화됩니다(이러한 변경 사항을 Live Copy에도 적용).
   * 개별 하위 페이지 및/또는 구성 요소에 대한 라이브 관계를 끊어서 Live Copy 컨텐츠를 조정할 수 있습니다. 이렇게 하면 소스의 변경 사항이 Live Copy에 더 이상 적용되지 않습니다.

이 페이지와 다음 페이지에서는 관련 문제를 다룹니다.

* [Live Copy 만들기 및 동기화](/help/sites-administering/msm-livecopy.md)
* [Live Copy 개요 콘솔](/help/sites-administering/msm-livecopy-overview.md)
* [Live Copy 동기화 구성](/help/sites-administering/msm-sync.md)
* [MSM 롤아웃 충돌](/help/sites-administering/msm-rollout-conflicts.md)
* [MSM 우수 사례](/help/sites-administering/msm-best-practices.md)

## 가능한 시나리오 {#possible-scenarios}

MSM과 Live Copy에 대한 사용 사례가 많이 있으며, 다음과 같은 경우도 있습니다.

* **다국적 - 글로벌 - 로컬 회사**

   MSM에서 지원하는 일반적인 사용 사례 중 하나는 여러 다국적 동일 언어 사이트의 컨텐츠를 재사용하는 것입니다. 이를 통해 핵심 컨텐츠를 다시 사용할 수 있을 뿐만 아니라 국가 변형을 적용할 수 있습니다.

   예를 들어 We.Retail 참조 사이트 샘플의 영어 섹션은 미국 고객을 위해 만들어집니다. 이 사이트의 대부분의 컨텐츠는 다른 국가와 문화의 영어를 사용하는 고객을 대상으로 하는 다른 We.Retail 사이트에도 사용할 수 있습니다. 핵심 컨텐츠는 모든 사이트에서 동일하게 유지되지만 지역별 조정은 가능합니다.

   미국, 영국, 캐나다 및 호주 사이트에 다음 구조를 사용할 수 있습니다.

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
   >MSM 파섹 필요한 구조를 만들고 컨텐츠를 배포하는 데 사용됩니다.
   >
   >
   >이러한 [예를 확장하려면 다국어](/help/sites-administering/translation.md) 사이트에 대한 컨텐츠 번역을 참조하십시오.

* **전국 - 본사와 지방 지사**

   또는 딜러 네트워크가 있는 회사는 개별 딜러를 위해 별도의 웹 사이트를 원할 수 있습니다. 각 사이트는 본사에서 제공하는 기본 사이트의 변형입니다. 이는 여러 지역 사무소를 가진 단일 회사나 중앙 가맹업체와 여러 지역 가맹점사업자로 구성된 국가 프랜차이즈 시스템일 수 있습니다.

   본사는 핵심 정보를 제공할 수 있지만, 지역 개체는 연락처 세부 사항, 시작 시간 및 이벤트와 같은 로컬 정보를 추가할 수 있습니다.

   ```xml
   /content
       |- head-office-Berlin
       |- branch-Hamburg
       |- branch-Stuttgart
       |- branch-Munich
       |- branch-Frankfurt
   ```

* **여러 버전**

   또는 MSM을 사용하여 특정 하위 분기의 버전을 만들 수 있습니다. 예를 들어, 기본 정보가 일정하게 유지되고 업데이트된 기능만 변경해야 하는 특정 제품의 다른 버전에 대한 지원 하위 사이트 유지 세부 정보.

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
   >이러한 시나리오에서는 항상 간단한 카피를 만들거나 Live Copy를 사용할 것인지에 대한 질문이 있습니다.
   >
   >다음과 같은 균형이 있습니다.
   >
   >  * 여러 버전을 통해 업데이트해야 하는 핵심 컨텐츠 수입니다.
   >
   >대상:
   >
   >  * 개별 사본의 양을 조정할 필요가 있다.


## UI의 MSM {#msm-from-the-ui}

MSM은 해당 콘솔의 다양한 옵션을 사용하여 UI에서 직접 액세스할 수 있습니다. 소개를 제공하려면 기본 위치를 나열합니다.

* **사이트 만들기** (**사이트**)

   * MSM을 사용하면 일반적인 컨텐츠를 공유하는 여러 웹 사이트를 관리할 수 있습니다.예를 들어, 웹 사이트는 대부분의 컨텐츠가 모든 국가에서 공통으로 사용되는 것과 같이 각 개별 국가에 맞는 컨텐츠의 하위 세트가 있는 국제적인 고객을 위해 제공되는 경우가 많습니다. MSM을 사용하면 소스 사이트에 [따라 하나 이상의 사이트를 자동으로 업데이트하는 Live Copy를](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)만들 수 있습니다. 또한 공통 기본 구조를 적용하고, 여러 사이트에서 일반적인 컨텐츠를 사용하고, 일반적인 모양과 느낌을 유지하며, 실제로 서로 다른 컨텐츠를 관리하는 데 집중할 수 있습니다.
   * 소스를 지정하려면 미리 정의된 블루프린트 구성이 필요합니다.
   * (사전 정의된) 소스의 Live Copy를 만듭니다.
   * 사용자에게 롤아웃 **단추를 제공합니다** .

* **Live Copy 만들기** (**사이트**)

   * MSM을 사용하면 웹 사이트의 [개별 페이지 또는 하위 분기의 임시(일회성) Live Copy를](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)만들 수 있습니다.예를 들어, 하위 분기를 복제하여 제품의 신규/업데이트된 버전에 대한 정보를 제공합니다.
   * 임시 Live Copy를 만듭니다(블루프린트 구성은 필요 없음).
   * 페이지/분기의 Live Copy를 만드는 데 사용할 수 있습니다(즉시).
   * 동기화 **필요** (롤아웃 **단추를 제공하지 않음** ).

* **속성 보기** (**사이트**)

   * 적절한 경우 이 옵션을 사용하면 관련 Live Copy 또는 Blueprint에 대한 정보를 제공하여 Live Copy [](/help/sites-administering/msm-livecopy.md#monitoring-your-live-copy) 를 **모니터링할**&#x200B;수 **있습니다**.

* **참조** (**사이트**)

   * 참조 [레일은](/help/sites-authoring/basic-handling.md#references) Live Copy **에 대한 정보와** 해당 작업에 대한 액세스를 제공합니다.

* **Live Copy 개요** (**사이트**)

   * 이 콘솔에서는 블루프린트와 Live Copy를 [보고 관리할](/help/sites-administering/msm-livecopy-overview.md)수 있습니다.

* **Blueprint** (**도구** - **사이트**)

   * 이 콘솔에서는 블루프린트 구성을 [만들고 관리할 수 있습니다](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration).

>[!NOTE]
>
>MSM 기능의 측면이 다른 여러 AEM 기능(예: 론치, 카탈로그)에서 사용됩니다.이 경우 Live Copy는 해당 기능으로 관리됩니다.

### 사용된 용어 {#terms-used}

다음 표에서는 MSM과 함께 사용되는 주요 용어에 대한 개요를 제공합니다.이러한 내용은 후속 섹션 및 페이지에서 자세히 다룹니다.

<table>
 <tbody>
  <tr>
   <td><strong>기간</strong></td>
   <td><strong>정의</strong></td>
   <td><strong>자세한 내용</strong></td>
  </tr>
  <tr>
   <td><strong>소스</strong></td>
   <td>원본 페이지.</td>
   <td>Blueprint 및/또는 Blueprint 페이지와 비슷합니다.</td>
  </tr>
  <tr>
   <td><strong>Live Copy</strong></td>
   <td>롤아웃 구성에 의해 정의된 대로 동기화 작업으로 유지 관리되는 소스의 복사본. </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Live Copy 구성</strong></td>
   <td>Live Copy에 대한 구성 세부 사항의 정의입니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>라이브 관계</strong><br /> </td>
   <td>해당 리소스에 대한 상속의 유효 정의소스와 Live Copy 간의 연결.<br /> </td>
   <td>소스의 변경 사항을 Live Copy와 동기화할 수 있습니다.</td>
  </tr>
  <tr>
   <td><strong>Blueprint</strong></td>
   <td>소스와 동의어.</td>
   <td>블루프린트 구성으로 정의할 수 있습니다.</td>
  </tr>
  <tr>
   <td><strong>블루프린트 구성</strong></td>
   <td>소스 경로를 지정하는 사전 정의된 구성</td>
   <td>블루프린트 페이지가 블루프린트 구성에서 참조되면 롤아웃 명령을 사용할 수 있습니다.</td>
  </tr>
  <tr>
   <td><strong>동기화</strong></td>
   <td>소스 및 Live Copy 간에 컨텐츠를 동기화하는 일반 용어입니다(롤아웃 및 동기화 <strong>모두</strong> ) <strong></strong>.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>롤아웃</strong><br /> </td>
   <td>소스에서 Live Copy로 동기화합니다.<br /> 작성자(블루프린트 페이지)나 시스템 이벤트(롤아웃 구성에 의해 정의됨)에 의해 트리거될 수 있습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>롤아웃 구성</strong></td>
   <td>동기화할 속성, 방법 및 시기를 결정하는 규칙입니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>동기화</strong></td>
   <td>Live Copy 페이지에서 이루어진 수동 동기화 요청.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>상속</strong></td>
   <td>Live Copy 페이지/구성 요소는 동기화가 발생할 때 소스 페이지/구성 요소에서 컨텐츠를 상속합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>일시 중단</strong></td>
   <td>Live Copy와 해당 블루프린트 페이지 간의 라이브 관계를 일시적으로 제거합니다.</td>
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
     <li>모든 상속 취소 및<br /> </li>
     <li>페이지를 소스 페이지와 동일한 상태로 되돌립니다.</li>
    </ul> <p>재설정은 페이지 속성, 단락 시스템 및 구성 요소에 대한 모든 변경 사항에 영향을 줍니다.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>얕은</strong></td>
   <td>단일 페이지의 Live Copy.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>깊이</strong></td>
   <td>페이지의 Live Copy와 하위 페이지</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>개체 [이름에 대해서는 Java](/help/sites-developing/extending-msm.md#overview-of-the-java-api) API 개요를 참조하십시오.

## Live Copy {#live-copies}

MSM Live Copy는 원본 소스와의 라이브 관계가 유지되는 특정 사이트 컨텐츠의 사본입니다.

* Live Copy는 소스의 컨텐츠를 상속합니다.
* 동기화는 소스를 변경할 때 컨텐츠의 실제 전송을 수행합니다.
* Live Copy는 다음 중 하나로 간주할 수 있습니다.

   * 얕게:한 페이지
   * 깊이:페이지와 하위 페이지

* 롤아웃 구성이라고 하는 동기화 규칙은 동기화할 속성과 동기화 발생 시기를 결정합니다.

이전 예에서 는 `/content/we-retail/language-masters/en` 영어로 된 글로벌 마스터 사이트입니다. 이 사이트의 컨텐츠를 재사용하려면 MSM Live Copy가 만들어집니다.

* 아래 컨텐츠는 `/content/we-retail/language-masters/en` 소스입니다.

* 아래 `/content/we-retail/language-masters/en` 컨텐츠는 `/content/we-retail/us/en/`, `/content/we-retail/gb/en`노드 `/content/we-retail/ca/en`및 `/content/we-retail/au/en` 노드 아래에 복사됩니다. 이것들은 Live Copy입니다.

* 작성자는 아래 페이지를 변경합니다 `/content/we-retail/language-masters/en`.
* MSM이 트리거되면 이러한 변경 사항을 Live Copy에 동기화합니다.

### Live Copy - 구성 {#live-copies-composition}

>[!NOTE]
>
>이 섹션의 다이어그램과 설명은 잠재적 Live Copy 스냅샷을 나타냅니다. 포괄적이지는 않지만 특정 특성을 강조하기 위한 개요를 제공합니다.

Live Copy를 처음 만들 때 선택한 소스 페이지가 Live Copy에서 1:1로 반영됩니다. 이후에는 새로운 리소스(페이지 및/또는 단락)를 Live Copy 내에서 직접 만들 수 있으므로 이러한 변형 및 변경 사항이 동기화에 미치는 영향을 파악하는 것이 유용합니다. 가능한 컴포지션은 다음과 같습니다.

* [Live Copy가 아닌 페이지를 포함한 Live Copy](#live-copy-with-non-live-copy-pages)
* [중첩된 Live Copy](#nested-live-copies)

Live Copy의 기본 형식은 다음과 같습니다.

* 선택한 소스 페이지를 1:1로 반영하는 Live Copy 페이지.
* 하나의 구성 정의
* 모든 리소스에 대해 정의된 라이브 관계:

   * Live Copy 리소스를 블루프린트/소스와 연결합니다.
   * 상속과 롤아웃을 구현할 때 사용됩니다.

* 변경 사항은 요구 사항에 따라 [동기화할](/help/sites-administering/msm-livecopy.md#synchronizing-your-live-copy) 수 있습니다.

![chlimage_1-367](assets/chlimage_1-367.png)

#### Live Copy가 아닌 페이지를 포함한 Live Copy {#live-copy-with-non-live-copy-pages}

AEM에서 Live Copy를 만들 때 Live Copy 분기를 보고 탐색할 수 있으며 Live Copy 분기에서 일반적인 AEM 기능을 사용할 수 있습니다. 즉, Live Copy 분기(예:
     `myCanadaOnlyProduct`).

* 이러한 리소스는 소스/블루프린트 페이지와 라이브 관계가 없으며 동기화되지 않습니다.
* MSM이 특수 케이스로 처리하는 시나리오가 발생할 수 있습니다. 예를 들어, 소스/블루프린트 및 Live Copy 분기 모두에서 위치와 이름이 같은 페이지를 만들 때(또는 프로세스) 이러한 경우 자세한 내용은 [MSM 롤아웃](/help/sites-administering/msm-rollout-conflicts.md) 충돌을 참조하십시오.

![chlimage_1-368](assets/chlimage_1-368.png)

#### 중첩된 Live Copy {#nested-live-copies}

기존 Live Copy에서 [새 페이지를 만드는 경우(또는 프로세스)](#live-copy-with-non-live-copy-pages) 이 새 페이지를 다른 블루프린트의 Live Copy로 설정할 수도 있습니다. 이를 중첩 Live Copy라고 합니다. 여기서 두 번째(내부) Live Copy의 동작은 다음 방법으로 첫 번째(외부) Live Copy의 영향을 받습니다.

* 최상위 Live Copy에 대해 트리거된 심층 롤아웃을 중첩 Live Copy로 계속할 수 있습니다(예: 트리거가 일치하는 경우).
* 소스 사이의 모든 링크는 Live Copy 내에서 다시 작성됩니다.

   예를 들어 두 번째 Live Copy에서 첫 번째 Live Copy로의 링크는 두 번째 Live Copy의 링크로 다시 작성됩니다.

![chlimage_1-369](assets/chlimage_1-369.png)

>[!NOTE]
>
>Live Copy 분기 내에서 페이지를 이동/이름을 변경하는 경우(내부) 중첩된 Live Copy로 처리되어 AEM이 관계를 추적할 수 있게 됩니다.

#### 누적 Live Copy {#stacked-live-copies}

Live Copy를 약식 Live Copy의 자식으로 만들 때 Live Copy라고 합니다. 중첩된 Live Copy와 같은 방식으로 [작동합니다](#nested-live-copies).

### 소스, Blueprint 및 Blueprint 구성 {#source-blueprints-and-blueprint-configurations}

페이지의 모든 페이지 또는 분기를 Live Copy 소스로 사용할 수 있습니다.

그러나 MSM에서는 소스 경로를 지정하는 블루프린트 구성을 정의할 수도 있습니다. 블루프린트 구성을 사용하면 다음과 같은 이점이 있습니다.

* 작성자가 이 블루프린트에서 상속되는 **Live Copy에** 대한 수정 사항을 푸시할 수 있도록 블루프린트의 롤아웃 옵션을 사용할 수 있습니다.
* 작성자가 사이트 만들기를 **사용하도록 허용**;사용자는 언어를 쉽게 선택하고 Live Copy 구조를 구성할 수 있습니다.
* 블루프린트와 관련된 Live Copy의 기본 롤아웃 구성을 정의합니다.

Live Copy 소스는 일반 페이지 또는 블루프린트 구성으로 포함된 페이지일 수 있습니다. 둘 다 유효한 사용 사례입니다.

소스는 Live Copy의 청사진을 구성합니다. 다음과 같은 경우 청사진이 정의됩니다.

* [블루프린트 구성 만들기](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)

   구성은 Live Copy를 만드는 데 사용할 페이지를 미리 정의합니다.

* [페이지의 Live Copy 만들기](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   Live Copy를 만드는 데 사용되는 페이지(소스 페이지)는 블루프린트 페이지입니다.

   소스 페이지는 블루프린트 구성으로 참조되거나 참조되지 않을 수 있습니다.

### 롤아웃 및 동기화 {#rollout-and-synchronize}

롤아웃은 Live Copy를 소스와 동기화하는 중앙 MSM 작업입니다. 수동으로 롤아웃을 수행하거나 자동으로 수행할 수 있습니다.

* 특정 [이벤트로](#rollout-configurations) 인해 롤아웃이 자동으로 발생할 수 있도록 롤아웃 구성을 [](/help/sites-administering/msm-sync.md#rollout-triggers) 정의할 수 있습니다.
* 블루프린트 페이지를 작성할 때 롤아웃 [명령을 사용하여](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) 변경 내용을 Live Copy로 푸시할 수 있습니다.

   **Rollout** 명령은 블루프린트 구성으로 참조되는 블루프린트 페이지에서 사용할 수 있습니다.

   ![chlimage_1-370](assets/chlimage_1-370.png)

* Live Copy 페이지를 작성할 때 동기화 [명령을 사용하여](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) 소스에서 Live Copy로 변경 사항을 가져올 수 있습니다.

   동기화 **명령은** 소스/블루프린트 페이지가 블루프린트 구성으로 포함되어 있는지 여부에 관계없이 Live Copy 페이지에서 항상 사용할 수 있습니다.

   ![chlimage_1-371](assets/chlimage_1-371.png)

### 롤아웃 구성 {#rollout-configurations}

롤아웃 구성은 Live Copy가 소스 컨텐츠와 동기화되는 시기와 방법을 정의합니다. 롤아웃 구성은 트리거 및 하나 이상의 동기화 작업으로 구성됩니다.

* **트리거**

   트리거는 소스 페이지의 활성화와 같이 라이브 작업 동기화를 발생시키는 이벤트입니다. MSM은 사용할 수 있는 트리거를 정의합니다.

* **동기화 작업**

   Live Copy에서 수행되어 소스와 동기화됩니다. 예를 들어 컨텐츠 복사, 하위 노드 순서 지정 및 Live Copy 페이지 활성화가 있습니다. MSM은 여러 동기화 작업을 제공합니다.

   >[!NOTE]
   >
   >Java API 파섹

롤아웃 구성을 다시 사용할 수 있으므로 두 개 이상의 Live Copy에서 동일한 롤아웃 구성을 사용할 수 있습니다. 표준 설치에는 몇 가지 [롤아웃 구성이](/help/sites-administering/msm-sync.md#installed-rollout-configurations) 포함되어 있습니다.

### 롤아웃 충돌 {#rollout-conflicts}

특히 작성자가 소스 및 Live Copy 모두에서 컨텐츠를 편집하는 경우 롤아웃이 복잡해질 수 있으므로 롤아웃 [중에 발생할 수 있는 모든](/help/sites-administering/msm-rollout-conflicts.md)충돌을 AEM에서 처리하는 방법을 이해하는 것이 유용합니다.

### 상속 및 동기화 일시 중단 및 취소 {#suspending-and-cancelling-inheritance-and-synchronization}

Live Copy의 각 페이지 및 구성 요소는 라이브 관계를 통해 소스 페이지 및 구성 요소와 연결됩니다. 라이브 관계는 소스에서 Live Copy 컨텐츠의 동기화를 구성합니다.

페이지 **속성과** 구성 요소를 변경할 수 있도록 Live Copy 페이지에 대한 Live Copy 상속을 일시 중단할 수 있습니다. 상속을 일시 중단하면 페이지 속성 및 구성 요소가 더 이상 소스와 동기화되지 않습니다.

개별 페이지를 편집할 때 작성자는 구성 요소에 **대한 상속을** 취소할 수 있습니다. 상속이 취소되면 라이브 관계가 일시 중단되고 해당 구성 요소에 대한 동기화가 발생하지 않습니다. 상속 및 동기화 취소는 컨텐츠의 하위 섹션을 사용자 정의해야 할 때 유용합니다.

### Live Copy 분리 {#detaching-a-live-copy}

또한 Live Copy를 [블루프린트에서](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) 분리하여 모든 연결을 제거할 수 있습니다.

>[!CAUTION]
>
>분리 동작은 영구적이며 되돌릴 수 없습니다.

분리는 Live Copy와 해당 블루프린트 페이지 간의 라이브 관계를 영구적으로 제거합니다. 모든 MSM 관련 속성은 Live Copy에서 제거되고 Live Copy 페이지는 독립형 복사본이 됩니다.

>[!NOTE]
>
>자세한 [내용은 Live Copy](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) 분할을 참조하십시오.하위 및 상위 페이지에 관련된 영향을 포함합니다.

## MSM 사용을 위한 표준 단계 {#standard-steps-for-using-msm}

다음 단계에서는 MSM을 사용하여 컨텐츠를 재사용하고 변경 사항을 Live Copy에 동기화하는 표준 절차를 설명합니다.

1. 소스 사이트의 컨텐츠를 개발할 수 있습니다.
1. 사용할 롤아웃 구성을 결정합니다.

   1. MSM은 여러 사용 사례를 충족할 수 있는 여러 개의 롤아웃 구성을 [](/help/sites-administering/msm-sync.md#installed-rollout-configurations) 설치합니다.
   1. 필요한 경우 롤아웃 구성을 [만들](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) 수도 있습니다.

1. 필요에 따라 사용하고 [](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use) 구성할 롤아웃 구성을 지정해야 하는 위치를 결정합니다.
1. 필요한 경우 Live Copy의 소스 컨텐츠를 식별하는 블루프린트 구성을 [만듭니다](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration) .
1. [Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy)만들기
1. 필요에 따라 소스 컨텐츠를 변경합니다. 조직에서 설정한 일반적인 컨텐츠 검토 및 승인 프로세스를 사용해야 합니다.
1. [블루프린트를 롤아웃하거나](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) Live Copy를 [변경 사항과](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) 동기화할 수 있습니다.

## MSM 사용자 지정 {#customizing-msm}

MSM 파섹

* **사용자 지정 롤아웃 구성**
   [설치된 롤아웃 구성이 요구 사항을 충족하지 않을 때 롤아웃 구성을](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) 만듭니다. 사용 가능한 모든 롤아웃 트리거 및 동기화 작업을 사용할 수 있습니다.

* **사용자 지정 동기화 작업**
   [설치된 작업이 특정 애플리케이션 요구 사항을 충족하지 않을 때 사용자 정의 동기화 작업을](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action) 만듭니다. MSM 파섹

## 우수 사례 {#best-practices}

MSM [우수 사례](/help/sites-administering/msm-best-practices.md) 페이지에는 구현과 관련된 중요한 정보가 포함되어 있습니다.
