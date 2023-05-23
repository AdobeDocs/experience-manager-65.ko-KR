---
title: 티저 및 전략
seo-title: Teasers and Strategies
description: 캠페인은 종종 티저를 메커니즘으로 사용하여 방문자 인구의 특정 세그먼트를 관심사에 초점을 맞춘 콘텐츠로 안내합니다. 하나 이상의 티저가 특정 캠페인에 대해 정의됩니다.
seo-description: Campaigns often use teasers as a mechanism to entice a specific segment of the visitor population through to content focused on their interests. One or more teasers are defined for a specific campaign.
uuid: c78ec858-4b0a-48d5-99b2-5ddd9e15183d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 7f378b94-5233-4358-8d93-a7b3386df00b
docset: aem65
exl-id: 27b8302c-250b-4ce6-b3cf-c938738f2d92
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 7%

---

# 티저 및 전략{#teasers-and-strategies}

캠페인은 종종 티저를 메커니즘으로 사용하여 방문자 인구의 특정 세그먼트를 관심사에 초점을 맞춘 콘텐츠로 안내합니다. 하나 이상의 티저가 특정 캠페인에 대해 정의됩니다.

>[!NOTE]
>
>티저 구성 요소는 AEM 6.2에서 더 이상 사용되지 않습니다. 다음을 사용하십시오. [Target 구성 요소](/help/sites-authoring/content-targeting-touch.md) 대신,

* **브랜드 페이지** 은 웹 사이트의 캠페인 섹션에 저장됩니다. 브랜드에는 개별 캠페인이 포함되어 있습니다.
* **캠페인 페이지** 은 웹 사이트의 캠페인 섹션에 저장됩니다. 각 캠페인에는 티저 정의가 유지되는 개별 페이지가 있습니다. 컨테이너 또는 개요 페이지에는 개별 티저 페이지에 대한 특정 정보와 통계도 포함되어 있습니다.

AEM 내의 티저는 다음과 같은 몇 가지 부분으로 구성됩니다.

* **티저 페이지** 은 해당 캠페인 페이지 아래에 저장되며, 티저 단락의 정의를 각 특정 캠페인에 사용할 수 있습니다. 이러한 정의는 티저 단락을 표시할 때 사용됩니다. 컨텐츠 변형을 포함하여 변형 및 부스트 요소를 선택하는 데 사용할 세그먼트입니다.
* 다음 **티저 구성 요소** 에서 바로 사용할 수 있으며, 콘텐츠 페이지에서 특정 티저 단락의 인스턴스를 만들 수 있습니다. 사이드 킥에서 티저 구성 요소를 드래그한 다음 티저 정의를 지정하여 자신만의 티저 단락을 만들 수 있습니다. **참고:** 티저 구성 요소는 AEM 6.2에서 더 이상 사용되지 않습니다. 다음을 사용하십시오. [Target 구성 요소](/help/sites-authoring/content-targeting-touch.md) 대신,
* **티저 단락** 는 콘텐츠 페이지 내 티저의 실제 인스턴스입니다. 이를 통해 관심사에 초점을 맞춘 콘텐츠를 통해 방문자 세그먼트를 유도합니다.
* 캠페인 콘텐츠가 보관된 페이지는 특정 방문자 세그먼트에 초점을 맞춥니다. 일반적으로 티저 단락은 방문자를 그러한 페이지로 안내합니다.

## 전략 {#strategies}

페이지에 티저 단락을 추가할 때는 **전략**.

이는 할당된 세그먼트가 모두 성공적으로 해결될 때 여러 티저를 선택할 수 있는 경우에 해당됩니다. 다음 **전략** 그런 다음 표시된 티저를 선택하는 데 사용되는 추가 기준을 지정합니다.

* **클릭스트림 점수**&#x200B;는 방문자의 클라이언트 컨텍스트 내에 있는 태그 및 관련 태그 히트(방문자가 각 태그가 들어 있는 페이지에서 클릭한 빈도를 표시)를 기반으로 합니다. 티저 페이지에 정의된 태그의 조회수가 비교됩니다.
* **무작위**, &quot;무작위&quot; 선택: 페이지에 대해 생성된 무작위 요소를 사용합니다. 다음 위치에서 볼 수 있습니다. [client context](/help/sites-administering/client-context.md).
* **첫 번째** 해결된 세그먼트 목록. 캠페인 컨테이너 페이지 내의 티저 순서입니다.

다음 [부스트 요소](/help/sites-administering/campaign-segmentation.md#boost-factor) 의 세그먼트는 선택 항목에도 영향을 줍니다. 이는 세그먼트 정의가 선택될 상대적 가능성을 증가/감소시키기 위해 세그먼트 정의에 추가된 가중 계수입니다.

다양한 선택 기준의 프로세스 및 상호 관계는 예제(티저가 필요한 대상자에게 도달하도록 하기 위해 사용할 수도 있는 메서드)를 사용하여 가장 잘 보여줍니다.

다음 세그먼트가 이미 생성되고 각각의 부스트 요소에 지정된 경우:

| 세그먼트 | 부스트 요소 |
|---|---|
| S1 | 0 |
| S2 | 0 |
| S3 | 10 |
| S4 | 30 |
| S5 | 0 |
| S6 | 100 |

그리고 다음과 같은 티저 정의를 사용합니다.

<table>
 <tbody>
  <tr>
   <td>캠페인</td>
   <td>티저</td>
   <td>할당된 세그먼트</td>
   <td>할당된 태그 </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1, S2</td>
   <td>비즈니스, 마케팅</td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T2 </td>
   <td>S1</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T3</td>
   <td>S3, S4</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T4</td>
   <td>S2, S5</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T5</td>
   <td>S1, S2, S6</td>
   <td>마케팅</td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T6</td>
   <td>S6</td>
   <td>상업<br /> </td>
  </tr>
 </tbody>
</table>

그런 다음 방문자에게 이 설정을 적용하면 다음이 수행됩니다.

* **S1**, **S2** 및 **S6** 확인 성공

* 태그 **마케팅** 3개 히트 있음
* 태그 **비즈니스** 6개 히트 있음

결과를 확인할 수 있습니다.

* 일치 성공 - 티저에 할당된 세그먼트 중 현재 방문자에 대해 성공적으로 해결된 세그먼트가 있습니까?
* 부스트 요소 - 적용 가능한 모든 세그먼트의 가장 높은 부스트 요소
* clickstream 점수 - 적용 가능한 모든 태그 히트에 대한 누적 합계

적절한 전략을 적용하기 전에 계산됩니다.

<table>
 <tbody>
  <tr>
   <td>캠페인</td>
   <td>티저</td>
   <td>할당된 세그먼트</td>
   <td>태그 </td>
   <td>일치합니까?</td>
   <td>결과 부스트 요소</td>
   <td>결과 클릭스트림 점수 </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1, S2</td>
   <td>비즈니스, 마케팅</td>
   <td>예</td>
   <td>0</td>
   <td>9</td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T2 </td>
   <td>S1</td>
   <td><br /> </td>
   <td>예</td>
   <td>0</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T3</td>
   <td>S3, S4</td>
   <td><br /> </td>
   <td>아니요</td>
   <td><br /> </td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T4</td>
   <td>S2, S5</td>
   <td><br /> </td>
   <td>예<br /> </td>
   <td>0<br /> </td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T5</td>
   <td>S1, S2, S6</td>
   <td>마케팅</td>
   <td>예</td>
   <td>100</td>
   <td>3</td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T6</td>
   <td>S6</td>
   <td>상업</td>
   <td>예</td>
   <td>100</td>
   <td>6 </td>
  </tr>
 </tbody>
</table>

이 값은 방문자가 다음에 따라 보게 될 티저를 결정하는 데 사용됩니다. **전략** 을 티저 단락에 적용합니다.

<table>
 <tbody>
  <tr>
   <td>전략</td>
   <td>결과 티저</td>
   <td>댓글</td>
  </tr>
  <tr>
   <td>처음</td>
   <td>T5</td>
   <td>T5 와 T6 만 세그먼트로 간주됩니다 <i>및</i> 가장 높은 부스트 요소를 가지고 있습니다. 반환된 목록은 T5, T6 순서이므로 T5 가 선택되어 표시됩니다.</td>
  </tr>
  <tr>
   <td>임의</td>
   <td>T5 또는 T6</td>
   <td>두 티저 모두 해결하는 세그먼트와 동일한 부스트 요소가 있습니다. 따라서 두 티저가 동일한 비율로 표시됩니다.</td>
  </tr>
  <tr>
   <td>클릭스트림 점수</td>
   <td>T6</td>
   <td><p>T1, T4, T5 및 T6에 대한 모든 세그먼트는 방문자에 대해 확인됩니다. T5 및 T6의 더 높은 부스트 인자는 T1 및 T4를 제외한다. 마지막으로 T6의 클릭스트림 점수가 높을수록 클릭스트림이 선택됩니다.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>위의 해상도 기법 이후에 여러 티저를 선택할 수 있는 경우, 내부 선택(임의)이 표시할 단일 티저를 선택합니다.
>
>예를 들어, 전략이 Clickstream Score이고 T5가 T6과 동일한 Clickstream Score(즉, 3 대신 6)를 가지면 내부 선택(임의)이 이 이 두 가지 중 하나를 선택하는 데 사용됩니다.

티저 페이지 / 단락은 특정 방문자 세그먼트를 관심사에 초점을 맞춘 콘텐츠로 유도하는 데 사용됩니다. 방문자가 선택할 수 있는 다양한 옵션을 제시하거나 특정 방문자 세그먼트를 기반으로 하는 하나의 티저 단락만 표시할 수 있습니다. 예를 들어, 표시되는 티저 단락은 방문자의 나이에 따라 달라질 수 있습니다.

일반적으로 티저 페이지는 다음 티저 페이지로 대체될 때까지 특정 기간 동안 지속되는 임시 작업입니다.

브랜드와 캠페인을 만든 후 티저 경험을 만들고 설정할 수 있습니다.

### 티저에 대한 터치포인트 만들기 {#creating-a-touchpoint-for-your-teaser}

>[!NOTE]
>
>티저 구성 요소는 AEM 6.2에서 더 이상 사용되지 않습니다. 다음을 사용하십시오. [Target 구성 요소](/help/sites-authoring/content-targeting-touch.md) 대신,

1. 캠페인 페이지로 이어지는 티저 단락을 배치할 콘텐츠 페이지로 이동합니다.
1. 추가 **티저** 구성 요소(다음에서 사용 가능) **개인화** (사이드 킥의 섹션)을 입력합니다. 처음 만들 때 캠페인 경로가 아직 구성되지 않았음을 표시합니다.

   ![chlimage_1](assets/chlimage_1.png)

1. 티저 구성 요소를 편집하여 다음을 추가합니다.

   * **캠페인 경로**
개별 티저 페이지가 들어 있는 캠페인 페이지 경로. 세그먼트는 표시되는 티저를 정확하게 결정합니다.

   * **[전략](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#strategies)**
여러 세그먼트가 정상적으로 배정될 때 선택에 사용되는 방법입니다.
   ![chlimage_1-1](assets/chlimage_1-1.png)

1. 클릭 **확인** 저장. 티저에 설정한 세그먼트와 현재 로그인한 사용자의 프로필에 따라 적절한 콘텐츠가 표시됩니다.

   ![chlimage_1-2](assets/chlimage_1-2.png)

1. 마우스를 티저 단락 위로 가져가면 물음표 아이콘(구성 요소의 오른쪽 하단)이 표시됩니다. 이 아이콘을 클릭하여 적용된 세그먼트와 현재 해결 여부를 확인합니다.

   ![chlimage_1-3](assets/chlimage_1-3.png)

### 티저 개요 {#teaser-overview}

MCM의 캠페인 보기는 물론, 캠페인 페이지에는 MCM에 연결된 티저에 대한 정보도 제공됩니다.

1. 다음에서 **웹 사이트** 콘솔을 누르고 캠페인 페이지를 엽니다. 예:

   `https://localhost:4502/content/campaigns/geometrixx-outdoors/storefront/summer.html`

   다음은 티저 정의 및 보기 통계에 대한 개요를 보여 줍니다.

   ![chlimage_1-4](assets/chlimage_1-4.png)
