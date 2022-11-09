---
title: "콘텐츠 재사용: 다중 사이트 관리자 및 라이브 카피"
seo-title: "Reusing Content: Multi Site Manager and Live Copy"
description: Live Copy 및 다중 사이트 관리자를 사용하여 컨텐츠를 재사용하는 방법에 대해 알아봅니다.
seo-description: Learn about reusing content with Live Copies and the Multi Site Manager.
uuid: 9f955226-8fc9-4357-b90c-c6896b0dc4b4
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: c21debc3-ecf4-4aa9-ab5a-18ddd5cf2fff
exl-id: 1e839845-fb5c-4200-8ec5-6ff744a96943
source-git-commit: 53c39e4aa250b18d4fae0327b313b18901677f2c
workflow-type: tm+mt
source-wordcount: '2664'
ht-degree: 32%

---

# 콘텐츠 재사용: 다중 사이트 관리자 및 라이브 카피{#reusing-content-multi-site-manager-and-live-copy}

MSM(Multi Site Manager)을 사용하면 여러 위치에서 동일한 사이트 콘텐츠를 사용할 수 있습니다. 이를 위해 MSM은 라이브 카피 기능을 사용합니다:

* MSM을 사용하여 다음과 같은 작업을 수행할 수 있습니다.

   * 콘텐츠를 한 번 만든 다음
   * 이 컨텐츠를 에 복사하고 다른 영역([live copy](#live-copies)) 내의 아무 곳에나 삽입할 수 있습니다.

* 그런 다음 MSM은 소스 컨텐츠와 Live Copy 간의 (라이브) 관계를 유지하여 다음과 같이 합니다.

   * 소스 컨텐츠를 변경하면 소스 및 Live Copy가 동기화됩니다(이러한 변경 사항을 Live Copy에도 적용).
   * 개별 하위 페이지 및/또는 구성 요소에 대한 라이브 관계를 연결을 끊음으로써 Live Copy의 컨텐츠를 조정할 수 있습니다. 이렇게 하면 소스 변경 사항이 더 이상 Live Copy에 적용되지 않습니다.

이 페이지와 다음 페이지에서는 관련 문제를 다룹니다.

* [라이브 카피 생성 및 동기화](/help/sites-administering/msm-livecopy.md)
* [라이브 카피 개요 콘솔](/help/sites-administering/msm-livecopy-overview.md)
* [라이브 카피 동기화 구성](/help/sites-administering/msm-sync.md)
* [MSM 롤아웃 충돌](/help/sites-administering/msm-rollout-conflicts.md)
* [MSM 모범 사례](/help/sites-administering/msm-best-practices.md)

## 가능한 시나리오 {#possible-scenarios}

MSM 및 Live Copy에 대한 사용 사례가 많습니다. 일부 시나리오는 다음과 같습니다.

* **다국적 - 글로벌 기업에서 로컬 회사까지**

   MSM이 지원하는 대표적인 사용 사례는 여러 다국적 동일 언어 사이트에서 콘텐츠를 재사용하는 것입니다. 이렇게 하면 국가 변형을 허용하는 동안 코어 컨텐츠를 다시 사용할 수 있습니다.

   예를 들어 미국의 고객을 위해 We.Retail 참조 사이트 샘플의 영어 섹션이 만들어집니다. 이 사이트의 대부분의 컨텐츠는 다양한 국가 및 문화의 영어를 사용하는 고객을 충족하는 다른 We.Retail 사이트에도 사용될 수 있습니다. 핵심 콘텐츠는 모든 사이트에 걸쳐 동일하게 유지되는 반면 지역적인 조정을 수행할 수 있습니다.

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
   >MSM은 콘텐츠를 번역하지 않습니다. 필요한 구조를 만들고 콘텐츠를 배포하는 데 사용됩니다.
   >
   >
   >자세한 내용은 [다국어 사이트의 컨텐츠 번역](/help/sites-administering/translation.md) 예를 확장하려는 경우

* **국제적 - 본사부터 지역 지사까지**

   또는 딜러망이 있는 회사는 개별 딜러를 위한 별도의 웹 사이트를 원할 수 있습니다. 각 사이트는 본사에서 제공하는 기본 사이트의 변형입니다. 이는 여러 지역 사무소가 있는 단일 회사 또는 중앙 프랜차이즈 본사와 여러 지역 프랜차이즈로 구성된 국제적인 프랜차이즈 시스템에 대한 것일 수 있습니다.

   본사는 핵심 정보를 제공할 수 있지만, 지역 엔티티는 여기에 연락처 세부 정보, 영업 시간 및 이벤트와 같은 로컬 정보를 추가할 수 있습니다.

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
   >및
   >
   >  * 개별 사본의 양을 조정해야 할 것입니다.


## UI의 MSM {#msm-from-the-ui}

MSM은 적절한 콘솔에서 다양한 옵션을 사용하여 UI에서 직접 액세스할 수 있습니다. 소개를 제공하려면 기본 위치가 다음과 같습니다.

* **사이트 생성**(**사이트**)

   * MSM은 일반적인 컨텐츠를 공유하는 여러 웹 사이트를 관리하는 데 도움이 됩니다. 예를 들어, 웹 사이트는 국제 대상을 위해 제공되므로 대부분의 컨텐츠는 각 개별 국가에 해당하는 컨텐츠의 하위 집합과 함께 모든 국가에서 일반적입니다. MSM을 통해 다음을 수행할 수 있습니다 [소스 사이트를 기반으로 하나 이상의 사이트를 자동으로 업데이트하는 live copy 만들기](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). 또한 이를 통해 일반적인 기본 구조를 적용하고, 여러 사이트에서 일반적인 콘텐츠를 사용하고, 공통적인 모양과 느낌을 유지하고, 사이트 간에 실제로 차이가 있는 콘텐츠를 관리하는 데 노력을 기울일 수 있습니다.
   * 소스를 지정하기 위해 사전 정의된 블루프린트 구성이 필요합니다.
   * (사전 정의된) 소스의 Live Copy를 만듭니다.
   * 사용자에게 **롤아웃** 버튼이 제공됩니다.

* **라이브 카피 만들기**(**Sites**)

   * MSM을 통해 다음을 수행할 수 있습니다 [웹 사이트의 개별 페이지 또는 하위 분기의 임시(일회성) 라이브 카피를 만듭니다](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page); 예를 들어 하위 분기를 복제하여 제품의 신규/업데이트된 버전에 대한 정보를 제공합니다.
   * 임시 Live Copy를 만듭니다(블루프린트 구성이 필요 없음).
   * 모든 페이지/분기의 Live Copy를 만드는 데 (즉시) 사용할 수 있습니다.
   * **동기화**&#x200B;가 필요합니다(**롤아웃** 버튼은 제공되지 않음).

* **속성 보기**(**사이트**)

   * 적절한 경우 이 옵션은 다음과 같은 작업을 수행하는 데 도움이 됩니다 [live copy 모니터링](/help/sites-administering/msm-livecopy.md#monitoring-your-live-copy) 관련 정보 제공 **Live Copy** y 또는 **블루프린트**.

* **참조**(**사이트**)

   * [참조](/help/sites-authoring/basic-handling.md#references) 레일은 적절한 작업에 대한 액세스 권한과 함께 **라이브 카피**&#x200B;에 대한 정보를 제공합니다.

* **라이브 카피 개요**(**사이트**)

   * 이 콘솔에서는 다음을 수행할 수 있습니다 [블루프린트 및 Live Copy 보기 및 관리](/help/sites-administering/msm-livecopy-overview.md).

* **블루프린트**(**도구** - **사이트**)

   * 이 콘솔에서는 다음을 수행할 수 있습니다 [블루프린트 구성 만들기 및 관리](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration).

>[!NOTE]
>
>MSM 기능의 특징은 몇 가지 다른 AEM 기능(예: 시작, 카탈로그)에 사용됩니다. 이 경우 live copy는 해당 기능에 의해 관리됩니다.

### 사용된 용어 {#terms-used}

다음 표에서는 MSM과 함께 사용되는 주요 용어에 대한 개요를 제공합니다. 이러한 내용은 후속 섹션 및 페이지에서 더 자세히 다룹니다.

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
   <td>블루프린트 및/또는 블루프린트 페이지의 동의어.</td>
  </tr>
  <tr>
   <td><strong>라이브 카피</strong></td>
   <td>롤아웃 구성에서 정의된 동기화 작업에 의해 관리되는 (소스의) 사본. </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>라이브 카피 구성</strong></td>
   <td>Live Copy에 대한 구성 세부 사항의 정의입니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>라이브 관계</strong><br /> </td>
   <td>주어진 리소스에 대한 상속의 유효 정의 소스와 Live Copy 간의 연결.<br /> </td>
   <td>소스에 대한 변경 사항을 Live Copy와 동기화할 수 있는지 확인합니다.</td>
  </tr>
  <tr>
   <td><strong>블루프린트</strong></td>
   <td>소스의 동의어.</td>
   <td>블루프린트 구성으로 정의할 수 있습니다.</td>
  </tr>
  <tr>
   <td><strong>블루프린트 구성</strong></td>
   <td>소스 경로를 지정하는 사전 정의된 구성.</td>
   <td>블루프린트 구성에서 블루프린트 페이지를 참조하면 롤아웃 명령을 사용할 수 있습니다.</td>
  </tr>
  <tr>
   <td><strong>동기화</strong></td>
   <td>소스와 라이브 카피 간의 컨텐츠 동기화를 위한 일반 용어입니다(두 방법 모두 사용) <strong>롤아웃</strong> 및 <strong>동기화</strong>).</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>롤아웃</strong><br /> </td>
   <td>소스에서 Live Copy에 동기화합니다.<br /> 작성자(블루프린트 페이지)나 시스템 이벤트(롤아웃 구성으로 정의됨)에 의해 트리거될 수 있습니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>롤아웃 구성</strong></td>
   <td>동기화될 속성, 그 방법 및 시기를 결정하는 규칙.</td>
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
     <li>모든 상속 취소 제거 및<br /> </li>
     <li>페이지를 소스 페이지와 동일한 상태로 되돌리기</li>
    </ul> <p>재설정은 페이지 속성, 단락 시스템 및 구성 요소에 적용한 변경 내용에 영향을 미칩니다.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>약식</strong></td>
   <td>단일 페이지의 Live Copy.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>딥</strong></td>
   <td>페이지의 Live Copy와 해당 하위 페이지.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>자세한 내용은 [Java API 개요](/help/sites-developing/extending-msm.md#overview-of-the-java-api) 객체 이름에 사용할 수 있습니다.

## 라이브 카피 {#live-copies}

MSM Live Copy는 원래 소스와의 라이브 관계가 유지 관리되는 특정 사이트 콘텐츠의 사본입니다.

* Live Copy는 소스의 컨텐츠를 상속합니다.
* 동기화는 소스가 변경될 때 실제 콘텐츠 이전을 수행합니다.
* Live Copy는 다음 중 하나로 간주할 수 있습니다.

   * 약식: 단일 페이지
   * 딥: 하위 페이지를 포함하는 페이지

* 롤아웃 구성이라고 하는 동기화 규칙은 동기화되는 속성과 동기화 발생 시기를 결정합니다.

이전의 예에서는 `/content/we-retail/language-masters/en`이 영어로 작성된 글로벌 마스터 사이트입니다. 이 사이트의 컨텐츠를 다시 사용하려면 MSM Live Copy가 만들어집니다.

* `/content/we-retail/language-masters/en` 아래의 콘텐츠는 소스입니다.

* 아래 컨텐츠 `/content/we-retail/language-masters/en` 아래에 복사됩니다 `/content/we-retail/us/en/`, `/content/we-retail/gb/en`, `/content/we-retail/ca/en`, 및 `/content/we-retail/au/en` 노드 아래에 나열됩니다. Live Copy입니다.

* 작성자는 `/content/we-retail/language-masters/en` 아래의 페이지에 변경 내용을 적용합니다.
* 트리거되면 MSM은 이러한 변경 사항을 Live Copy에 동기화합니다.

### 라이브 카피 - 구성 {#live-copies-composition}

>[!NOTE]
>
>이 섹션의 다이어그램과 설명은 잠재적인 Live Copy의 스냅샷을 나타냅니다. 이 스냅샷은 포괄적이지는 않지만 특정 특성을 강조하는 개요를 제공합니다.

처음에 Live Copy를 만들 때 선택한 소스 페이지는 Live Copy에서 1:1에 반영됩니다. 그런 다음 Live Copy 내에서 새로운 리소스(페이지 및/또는 단락)를 직접 만들 수도 있으므로 이러한 변형과 변형이 동기화에 미치는 영향을 이해하는 것이 좋습니다. 가능한 구성은 다음과 같습니다.

* [라이브 카피가 아닌 페이지를 포함하는 라이브 카피](#live-copy-with-non-live-copy-pages)
* [중첩 라이브 카피](#nested-live-copies)

Live Copy의 기본 양식은 다음과 같습니다.

* 선택한 소스 페이지를 1:1 기준으로 반영하는 Live Copy 페이지.
* 1개의 구성 정의
* 모든 리소스에 대해 정의된 라이브 관계:

   * Live Copy 리소스를 블루프린트/소스와 연결합니다.
   * 상속 및 롤아웃을 실현할 때 사용됩니다.

* 변경 내용은 요구 사항에 따라 [동기화](/help/sites-administering/msm-livecopy.md#synchronizing-your-live-copy)될 수 있습니다.

![chlimage_1-367](assets/chlimage_1-367.png)

#### 라이브 카피가 아닌 페이지를 포함하는 라이브 카피 {#live-copy-with-non-live-copy-pages}

AEM에서 Live Copy를 만들면 Live Copy 분기를 보고 탐색할 수 있으며 Live Copy 분기에서 일반적인 AEM 기능을 사용할 수 있습니다. 즉, 사용자나 프로세스는 Live Copy 분기(예: )에서 새 리소스(페이지 및/또는 단락)를 만들 수 있습니다. `myCanadaOnlyProduct`).

* 이러한 리소스는 소스/블루프린트 페이지와 라이브 관계가 없으며 동기화되지 않습니다.
* MSM이 특수 사례로 처리하는 시나리오가 발생할 수 있습니다. 예를 들어, 소스/블루프린트 및 Live Copy 분기 모두에서 위치 및 이름이 동일한 페이지를 만들 때(또는 프로세스). 이러한 상황에 대한 자세한 내용은 [MSM 롤아웃 충돌](/help/sites-administering/msm-rollout-conflicts.md)을 참조하십시오.

![chlimage_1-368](assets/chlimage_1-368.png)

#### 중첩 라이브 카피 {#nested-live-copies}

(또는 프로세스)에서 [기존 live copy 내의 새 페이지](#live-copy-with-non-live-copy-pages) 이 새 페이지를 다른 블루프린트의 live copy로 설정할 수도 있습니다. 이를 중첩된 Live Copy라고 하며, 여기서 두 번째(내부) Live Copy의 동작은 다음의 방식으로 첫 번째(외부) Live Copy의 영향을 받습니다.

* 최상위 Live Copy에 대해 트리거된 딥 롤아웃을 중첩된 Live Copy로 계속할 수 있습니다(예: 트리거가 일치하는 경우).
* 소스 사이의 모든 링크는 Live Copy 내에서 다시 작성됩니다.

   예를 들어, 두 번째에서 첫 번째 블루프린트로의 링크는 중첩된/두 번째 Live Copy에서 첫 번째 Live Copy로의 링크로 다시 작성됩니다.

![chlimage_1-369](assets/chlimage_1-369.png)

>[!NOTE]
>
>Live Copy 분기 내에서 페이지를 이동/이름을 변경하는 경우(내부적으로) 이 페이지는 중첩된 Live Copy로 처리되어 AEM에서 관계를 추적합니다.

#### 누적 라이브 카피 {#stacked-live-copies}

Live Copy를 얕은 Live Copy의 자식으로 만들 때 누적 Live Copy라고 합니다. 그것은 와 같은 방식으로 동작한다 [중첩된 Live Copy](#nested-live-copies).

### 소스, 블루프린트 및 블루프린트 구성 {#source-blueprints-and-blueprint-configurations}

페이지의 모든 페이지 또는 분기를 Live Copy 소스로 사용할 수 있습니다.

그러나 MSM을 사용하면 소스 경로를 지정하는 블루프린트 구성을 정의할 수도 있습니다. 블루프린트 구성을 사용할 때의 이점은 다음과 같습니다.

* 작성자가 **롤아웃** 블루프린트의 옵션 - 이 블루프린트에서 상속되는 라이브 카피에 대한 수정 사항을 푸시할 대상.
* 작성자가 사용할 수 있도록 허용 **사이트 만들기**; 언어를 쉽게 선택하고 live copy 구조를 구성할 수 있습니다.
* 블루프린트와 관계가 있는 Live Copy에 대한 기본 롤아웃 구성을 정의합니다.

Live Copy 소스는 일반 페이지 또는 블루프린트 구성으로 둘러싸인 페이지일 수 있습니다. 둘 다 유효한 사용 사례입니다.

소스는 Live Copy에 대한 블루프린트를 구성합니다. 다음의 경우 블루프린트가 정의됩니다.

* [블루프린트 구성 만들기](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)

   구성은 Live Copy를 만드는 데 사용할 페이지를 미리 정의합니다.

* [페이지의 Live Copy 만들기](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   Live Copy(소스 페이지)를 만드는 데 사용되는 페이지는 블루프린트 페이지입니다.

   소스 페이지는 블루프린트 구성으로 참조되거나 참조되지 않습니다.

### 롤아웃 및 동기화 {#rollout-and-synchronize}

롤아웃은 Live Copy를 소스와 동기화하는 중앙 MSM 작업입니다. 롤아웃은 수동으로 수행할 수도 있고 자동으로 수행할 수도 있습니다:

* [롤아웃 구성](#rollout-configurations)을 정의하여 특정 [이벤트](/help/sites-administering/msm-sync.md#rollout-triggers)가 롤아웃을 자동으로 발생시킬 수 있도록 할 수 있습니다.
* 블루프린트 페이지를 작성할 때 [롤아웃](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) live copy에 변경 사항을 푸시할 명령.

   **롤아웃** 명령은 블루프린트 구성에서 참조되는 블루프린트 페이지에서 사용할 수 있습니다.

   ![chlimage_1-370](assets/chlimage_1-370.png)

* Live Copy 페이지를 작성할 때 [동기화](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) 소스에서 live copy로 변경 사항을 가져오는 명령.

   다음 **동기화** 명령은 항상 live copy 페이지에서 사용할 수 있습니다(소스/블루프린트 페이지가 블루프린트 구성으로 감싸는지 여부에 관계없이).

   ![chlimage_1-371](assets/chlimage_1-371.png)

### 롤아웃 구성 {#rollout-configurations}

롤아웃 구성은 Live Copy가 소스 컨텐츠와 동기화되는 시기 및 방법을 정의합니다. 롤아웃 구성은 트리거와 하나 이상의 동기화 작업으로 구성됩니다.

* **트리거**

   트리거는 소스 페이지의 활성화와 같이 라이브 작업 동기화가 발생하는 이벤트입니다. MSM은 사용할 수 있는 트리거를 정의합니다.

* **동기화 작업**

   Live Copy에서 수행되어 소스와 동기화됩니다. 작업의 예로는 컨텐츠 복사, 하위 노드 순서 지정 및 Live Copy 페이지 활성화가 있습니다. MSM은 많은 동기화 작업을 제공합니다.

   >[!NOTE]
   >
   >Java API를 사용하여 인스턴스에 대한 사용자 정의 작업을 만들 수 있습니다.

롤아웃 구성을 다시 사용할 수 있으므로 두 개 이상의 Live Copy에서 동일한 롤아웃 구성을 사용할 수 있습니다. 표준 설치에는 여러 [롤아웃 구성](/help/sites-administering/msm-sync.md#installed-rollout-configurations)이 포함되어 있습니다.

### 롤아웃 충돌 {#rollout-conflicts}

롤아웃은 복잡해질 수 있습니다. 특히 작성자가 소스와 Live Copy 모두에서 컨텐츠를 편집할 때 복잡해질 수 있으므로 AEM에서 모든 작업을 처리하는 방법을 이해하는 것이 좋습니다 [롤아웃 중에 발생할 수 있는 충돌](/help/sites-administering/msm-rollout-conflicts.md).

### 상속 및 동기화 일시 중단 및 취소 {#suspending-and-cancelling-inheritance-and-synchronization}

Live Copy의 각 페이지 및 구성 요소는 라이브 관계를 통해 소스 페이지 및 구성 요소와 연결됩니다. 라이브 관계는 소스에서 Live Copy 컨텐츠의 동기화를 구성합니다.

다음을 수행할 수 있습니다 **일시 중단** 페이지 속성 및 구성 요소를 변경할 수 있도록 live copy 페이지에 대한 live copy 상속. 상속을 일시 중단하면 페이지 속성 및 구성 요소는 더 이상 소스와 동기화되지 않습니다.

개별 페이지 편집 시 작성자는 구성 요소에 대한 **상속을 취소**&#x200B;할 수 있습니다. 상속이 취소되면 라이브 관계가 일시 중단되고 해당 구성 요소에 대한 동기화가 수행되지 않습니다. 상속 및 동기화 취소 작업은 콘텐츠의 하위 섹션을 맞춤화해야 할 때 유용합니다.

### 라이브 카피 분리 {#detaching-a-live-copy}

다음을 수행할 수도 있습니다 [live copy 분리](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) 블루프린트에서 모든 연결을 제거하려면

>[!CAUTION]
>
>분리 작업은 영구적이며 취소가 불가능합니다.

분리는 Live Copy와 블루프린트 페이지 간의 라이브 관계를 영구적으로 제거합니다. 모든 MSM 관련 속성은 Live Copy에서 제거되고 Live Copy 페이지는 독립형 복사본이 됩니다.

>[!NOTE]
>
>자세한 내용은 [Live Copy 분리](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) 자세한 내용 하위 및 상위 페이지에 대한 관련 영향 포함.

## MSM 사용을 위한 표준 단계 {#standard-steps-for-using-msm}

다음 단계에서는 MSM을 사용하여 컨텐츠를 재사용하고 변경 사항을 Live Copy에 동기화하는 표준 절차를 설명합니다.

1. 소스 사이트의 콘텐츠를 개발합니다.
1. 사용할 롤아웃 구성을 결정합니다.

   1. MSM은 다양한 사용 사례를 충족할 수 있는 [여러 롤아웃 구성을 설치](/help/sites-administering/msm-sync.md#installed-rollout-configurations)합니다.
   1. 필요한 경우 [롤아웃 구성을 생성](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration)할 수 있습니다.

1. [사용할 롤아웃 구성을 지정](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use)해야 하는 위치를 결정하고 필요에 따라 구성합니다.
1. 필요한 경우 [블루프린트 구성 만들기](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration) 는 live copy의 소스 컨텐츠를 식별합니다.
1. [Live Copy 만들기](/help/sites-administering/msm-livecopy.md#creating-a-live-copy).
1. 필요에 따라 소스 콘텐츠를 변경합니다. 귀사에서 수립한 일반 콘텐츠 검토 및 승인 프로세스를 사용해야 합니다.
1. [롤아웃](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) 블루프린트 또는 [live copy 동기화](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) 변경 사항 포함.

## MSM 맞춤화 {#customizing-msm}

MSM은 콘텐츠를 공유할 때 발생할 수 있는 예외적인 복잡성에 맞게 구현을 조정할 수 있는 도구를 제공합니다:

* **사용자 지정 롤아웃 구성**
   [롤아웃 구성 만들기](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) 설치된 롤아웃 구성이 요구 사항을 충족하지 않는 경우 사용할 수 있는 모든 롤아웃 트리거 및 동기화 작업을 사용할 수 있습니다.

* **사용자 지정 동기화 작업**
   [사용자 지정 동기화 작업 만들기](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action) 설치된 작업이 특정 애플리케이션 요구 사항을 충족하지 않는 경우 MSM은 사용자 지정 동기화 작업을 만들기 위한 Java API를 제공합니다.

## 모범 사례 {#best-practices}

[MSM 모범 사례](/help/sites-administering/msm-best-practices.md) 페이지에는 구현과 관련된 중요한 정보가 포함되어 있습니다.
