---
title: 세그멘테이션 구성
seo-title: 세그멘테이션 구성
description: AEM Campaign에 대한 세그멘테이션을 구성하는 방법을 배웁니다.
seo-description: AEM Campaign에 대한 세그멘테이션을 구성하는 방법을 배웁니다.
uuid: 604ca34d-cdb9-49ff-8f75-02a44b60a8a2
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: c68d5853-684f-42f2-a215-c1eaee06f58a
docset: aem65
exl-id: 6d759907-8796-4749-bd80-306ec7f2c819
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 3%

---

# 세그먼테이션 구성 {#configuring-segmentation}

>[!NOTE]
>
>이 문서에서는 Client Context와 함께 사용되는 대로 세그멘테이션의 구성을 다룹니다. Touch UI를 사용하여 ContextHub로 세그먼트를 구성하려면 [ContextHub](/help/sites-administering/segmentation.md)로 세그멘테이션 구성 을 참조하십시오.

세그먼테이션은 캠페인을 만들 때 중요하게 고려해야 하는 사항입니다. 세그먼테이션의 작동 방식과 주요 용어에 대한 자세한 내용은 [세그먼테이션 용어집](/help/sites-authoring/segmentation-overview.md)을 참조하십시오.

사이트 방문자와 달성하려는 목표에 대해 이미 수집한 정보에 따라 타깃팅된 컨텐츠에 필요한 세그먼트와 전략을 정의해야 합니다.

그런 다음 이러한 세그먼트를 사용하여 방문자에게 특별히 타깃팅된 콘텐츠를 제공합니다. 이 콘텐츠는 웹 사이트의 [캠페인](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md) 섹션에서 유지됩니다. 여기에 정의된 Teaser 페이지는 모든 페이지에서 Teaser 단락으로 포함될 수 있으며 전문 컨텐츠가 적용될 수 있는 방문자 세그먼트를 정의합니다.

AEM에서 세그먼트, 티저 및 캠페인을 쉽게 만들고 업데이트할 수 있습니다. 또한 정의 결과를 확인할 수 있습니다.

**세그먼트 편집기**&#x200B;를 사용하면 세그먼트를 쉽게 정의할 수 있습니다.

![](assets/segmenteditor.png)

각 세그먼트를 **편집** 하여 **제목**, **설명** 및 **증폭** 요소를 지정할 수 있습니다. 사이드킥을 사용하여 **AND** 및 **OR** 컨테이너를 추가하여 **세그먼트 논리**&#x200B;를 정의한 다음 필요한 **세그먼트 트레이트**&#x200B;를 추가하여 선택 기준을 정의할 수 있습니다.

## 증폭 인수 {#boost-factor}

각 세그먼트에는 가중치로 사용되는 **증폭** 매개 변수가 있습니다.숫자가 높을수록 숫자가 낮은 세그먼트가 선호되는 세그먼트가 선택됨을 나타냅니다.

* 최소값:`0`
* 최대값:`1000000`

## 세그먼트 논리 {#segment-logic}

기본적으로 다음 논리 컨테이너를 사용할 수 있으므로 세그먼트 선택 논리를 구성할 수 있습니다. 사이드 킥에서 편집기로 드래그할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td> AND 컨테이너<br /> </td>
   <td> 부울 AND 연산자입니다.<br /> </td>
  </tr>
  <tr>
   <td> OR 컨테이너<br /> </td>
   <td> 부울 OR 연산자입니다.</td>
  </tr>
 </tbody>
</table>

## 세그먼트 트레이트 {#segment-traits}

기본적으로 다음 세그먼트 트레이트를 사용할 수 있습니다.사이드 킥에서 편집기로 드래그할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td> IP 범위<br /> </td>
   <td>방문자가 가질 수 있는 IP 주소 범위를 정의합니다.<br /> </td>
  </tr>
  <tr>
   <td> 페이지 조회수<br /> </td>
   <td>페이지가 요청되는 횟수입니다.<br /> </td>
  </tr>
  <tr>
   <td> 페이지 속성<br /> </td>
   <td>방문한 페이지의 모든 속성입니다.<br /> </td>
  </tr>
  <tr>
   <td> 참조 키워드<br /> </td>
   <td>참조 웹 사이트의 정보와 일치하는 키워드입니다.<br /> </td>
  </tr>
  <tr>
   <td> 스크립트</td>
   <td>평가할 Javascript 식입니다.<br /> </td>
  </tr>
  <tr>
   <td> 세그먼트 참조 <br /> </td>
   <td>다른 세그먼트 정의에 대한 참조입니다.<br /> </td>
  </tr>
  <tr>
   <td> 태그 클라우드<br /> </td>
   <td>방문한 페이지의 태그와 일치할 태그입니다.<br /> </td>
  </tr>
  <tr>
   <td> 사용자 연령<br /> </td>
   <td>사용자 프로필에서 가져온 대로<br /> </td>
  </tr>
  <tr>
   <td> 사용자 속성<br /> </td>
   <td>사용자 프로필에서 사용할 수 있는 기타 모든 정보입니다. </td>
  </tr>
 </tbody>
</table>

부울 연산자 OR 및 AND([새 세그먼트 만들기](#creating-a-new-segment) 참조)를 사용하여 이러한 트레이트를 결합하여 이 세그먼트를 선택하는 정확한 시나리오를 정의할 수 있습니다.

전체 문이 true로 평가되면 이 세그먼트가 해결됩니다. 여러 세그먼트를 적용할 수 있는 경우 **[증폭](/help/sites-administering/campaign-segmentation.md#boost-factor)** 계수도 사용됩니다.

>[!CAUTION]
>
>세그먼트 편집기는 순환 참조를 확인하지 않습니다. 예를 들어 세그먼트 A는 다른 세그먼트 B를 참조하며 이 세그먼트 A는 차례로 세그먼트 A를 참조합니다. 세그먼트가 순환 참조를 포함하지 않는지 확인해야 합니다.

>[!NOTE]
>
>**_i18n** 접미사를 사용하는 속성은 개인화의 UI clientlib에 속하는 스크립트로 설정됩니다. 게시에 UI가 필요하지 않으므로 모든 UI 관련 clientlibs는 작성자에만 로드됩니다.
>
>따라서 이러한 속성을 사용하는 세그먼트를 만들 때는 일반적으로 **browserFamily_i18n** 대신 **browserFamily**&#x200B;을 사용해야 합니다.

### 새 세그먼트 만들기 {#creating-a-new-segment}

새 세그먼트를 정의하려면

1. 레일에서 **도구 > 작업 > 구성**&#x200B;을 선택합니다.
1. 왼쪽 창에서 **세분화** 페이지를 클릭하고 필요한 위치로 이동합니다.
1. **세그먼트** 템플릿을 사용하여 [새 페이지](/help/sites-authoring/editing-content.md#creatinganewpage)을 만듭니다.
1. 새 페이지를 열어 세그먼트 편집기를 확인합니다.

   ![](assets/screen_shot_2012-02-02at101726am.png)

1. 사이드 킥이나 컨텍스트 메뉴(일반적으로 마우스 오른쪽 단추 클릭)를 사용한 다음 **새로 만들기... 를 선택합니다.** 새 구성 요소 삽입 창을 열려면) 필요한 세그먼트 트레이트를 찾습니다. 그런 다음 **세그먼트 편집기**&#x200B;로 드래그하면 기본 **AND** 컨테이너에 표시됩니다.
1. 새 트레이트를 두 번 클릭하여 특정 매개 변수를 편집합니다.예를 들어 마우스 위치:

   ![](assets/screen_shot_2012-02-02at103135am.png)

1. **확인**&#x200B;을 클릭하여 정의를 저장합니다.
1. **세그먼트 정의를 편집하여**&#x200B;제목&#x200B;**,**&#x200B;설명&#x200B;**및**[&#x200B;증폭&#x200B;](#boost-factor)**인수를 제공할 수 있습니다.**

   ![](assets/screen_shot_2012-02-02at103547am.png)

1. 필요한 경우 트레이트를 더 추가합니다. **AND Container** 및 **OR Container** 구성 요소를 사용하여 **세그먼트 논리**&#x200B;에 부울 표현식을 만들 수 있습니다. 세그먼트 편집기를 사용하여 더 이상 필요하지 않은 트레이트나 컨테이너를 삭제하거나 문 내의 새 위치로 드래그할 수 있습니다.

### AND 및 OR 컨테이너 {#using-and-and-or-containers} 사용

AEM에서 복잡한 세그먼트를 만들 수 있습니다. 몇 가지 기본 사항을 인식하는 데 도움이 됩니다.

* 정의의 최상위 수준은 항상 처음에 만들어진 AND 컨테이너입니다.변경할 수 없지만 나머지 세그먼트 정의에는 영향을 주지 않습니다.
* 컨테이너의 중첩이 적절한지 확인합니다. 컨테이너는 부울 표현식의 대괄호로 볼 수 있습니다.

다음 예는 다음 중 한 방문자를 선택하는 데 사용됩니다.

16세에서 65세 사이의 남자

또는

16세에서 62세 사이의 여성

주 연산자가 OR이므로 **OR Container**&#x200B;로 시작해야 합니다. 이 내에 2개의 AND 문이 있으며, 이러한 각 트레이트에 대해 개별 트레이트를 추가할 수 있는 **AND Container** 가 필요합니다.

![](assets/screen_shot_2012-02-02at105145am.png)

## 세그먼트 응용 프로그램 테스트 {#testing-the-application-of-a-segment}

세그먼트가 정의되면 잠재적인 결과를 **[Client Context](/help/sites-administering/client-context.md)**&#x200B;의 도움을 받아 테스트할 수 있습니다.

1. 테스트할 세그먼트를 선택합니다.
1. **[Ctrl-Alt-C](/help/sites-authoring/page-authoring.md#keyboardshortcuts)**&#x200B;을 눌러 수집된 데이터를 표시하는 **[Client Context](/help/sites-administering/client-context.md)**&#x200B;를 엽니다. 테스트를 위해 특정 값을 **편집** 하거나 **로드** 다른 프로필을 사용하여 해당 값에 영향을 줄 수 있습니다.

1. 정의된 트레이트에 따라 현재 페이지에 사용할 수 있는 데이터가 세그먼트 정의와 일치하지 않을 수 있습니다. 일치 상태가 정의 아래에 표시됩니다.

예를 들어, 단순 세그먼트 정의는 사용자의 연령 및 성별을 기반으로 할 수 있습니다. 특정 프로필을 로드하면 세그먼트가 성공적으로 해결되었음을 나타냅니다.

![](assets/screen_shot_2012-02-02at105926am.png)

아님:

![](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>페이지 다시 로드에서만 대부분의 변경 사항이 적용되지만 모든 트레이트가 즉시 해결됩니다. 마우스 위치에 대한 변경 사항이 즉시 표시되므로 테스트 목적으로 유용합니다.

이러한 테스트는 컨텐츠 페이지에서 수행할 수도 있으며, **Teaser** 구성 요소와 함께 수행할 수도 있습니다.

티저 단락에 마우스를 올려 놓으면 적용된 세그먼트, 현재 해결되었는지 여부 및 현재 티저 인스턴스를 선택한 이유가 표시됩니다.

![](assets/chlimage_1-47.png)

### 세그먼트 사용 {#using-your-segment}

세그먼트는 현재 [캠페인](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md) 내에서 사용됩니다. 특정 타겟 대상에 표시되는 실제 컨텐츠를 유도하는 데 사용됩니다. 자세한 내용은 [세그먼트 이해](/help/sites-authoring/segmentation-overview.md) 를 참조하십시오.
