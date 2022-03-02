---
title: Adobe Target으로 경험 조각 내보내기
seo-title: Exporting Experience Fragments to Adobe Target
description: Adobe Target으로 경험 조각 내보내기
seo-description: Exporting Experience Fragments to Adobe Target
uuid: 2df0faab-5d5e-4fc1-93b3-28b7e6f3c306
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d4152b4d-531b-4b62-8807-a5bc5afe94c6
docset: aem65
exl-id: f2921349-de8f-4bc1-afa2-aeace99cfc5c
source-git-commit: 72012fa441edb01deb7e557b707fb068d8e9892e
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 2%

---

# Adobe Target으로 경험 조각 내보내기{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>이 페이지의 일부 기능을 사용하려면 AEM 6.5.3.0 이상을 적용해야 합니다.
>
>6.5.3.0:
>
>* **외부자 도메인** 이제 을(를) 선택할 수 있습니다.
   >  **참고:** 외부자 도메인은 Target으로 전송되는 경험 조각의 컨텐츠와만 관련되며 오퍼 컨텐츠 보기와 같은 메타데이터는 연관되지 않습니다.
>
>6.5.2.0:
>
>* 경험 조각을 다음 중 하나로 내보낼 수 있습니다.
   >
   >   * 기본 작업 영역입니다.
   >   * 클라우드 구성에 지정된 명명된 작업 공간입니다.
   >   * **참고:** 특정 작업 공간으로 내보내려면 Adobe Target Premium이 필요합니다.
>
>* AEM이 있어야 함 [ims를 사용하여 Adobe Target과 통합](/help/sites-administering/integration-target-ims.md).
>
>AEM 6.5.0.0 및 6.5.1.0:
>
>* AEM 경험 구성 요소는 Adobe Target의 기본 작업 공간으로 내보내집니다.
>* AEM은 [Adobe Target과 통합](/help/sites-administering/target.md).


내보낼 수 있습니다 [경험 조각](/help/sites-authoring/experience-fragments.md): Adobe Experience Manager(AEM)에서 만든 Adobe Target(Target)으로 이동합니다. 그런 다음 Target 활동에서 오퍼로 사용하여 경험을 규모에 맞게 테스트 및 개인화할 수 있습니다.

Adobe Target으로 경험 조각을 내보내는 데 사용할 수 있는 세 가지 형식 옵션이 있습니다.

* HTML(기본값): 웹 및 하이브리드 콘텐츠 전달 지원
* JSON: 헤드리스 컨텐츠 전달 지원
* HTML 및 JSON

AEM 경험 구성요소를 Adobe Target의 기본 작업 공간으로 내보내거나 Adobe Target의 사용자 지정 작업 공간으로 내보낼 수 있습니다. 이 작업은 Adobe 개발자 콘솔을 사용하여 수행됩니다. 이 콘솔에서 AEM을 사용해야 합니다. [ims를 사용하여 Adobe Target과 통합](/help/sites-administering/integration-target-ims.md).

>[!NOTE]
>
>Adobe Target 작업 공간은 Adobe Target 자체에 없습니다. Adobe IMS(Identity Management 시스템)에서 정의 및 관리된 다음, Adobe 개발자 콘솔의 통합을 사용하여 솔루션 간에 사용할 수 있도록 선택됩니다.

>[!NOTE]
>
>Adobe Target 작업 공간을 사용하여 조직(그룹) 구성원이 이 조직에 대한 오퍼와 활동만 만들고 관리할 수 있습니다. 다른 사용자에게 액세스 권한을 제공하지 않습니다. 예를 들어, 글로벌 관심사 내의 국가별 조직을 예로 들 수 있습니다.

>[!NOTE]
>
>자세한 내용은 다음을 참조하십시오.
>
>* [Adobe Target 개발](https://www.adobe.io/apis/experiencecloud/target.html)
>* [핵심 구성 요소 - 경험 조각](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)
>


## 전제 조건 {#prerequisites}

>[!CAUTION]
>
>이 페이지의 일부 기능을 사용하려면 AEM 6.5.3.0을 적용해야 합니다.

다양한 작업이 필요합니다.

1. 당신은 [ims를 사용하여 AEM과 Adobe Target 통합.](/help/sites-administering/integration-target-ims.md).
2. 경험 조각은 AEM 작성자 인스턴스에서 내보내지므로 다음 작업을 수행해야 합니다 [AEM Link Externalizer 구성](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer) 작성 인스턴스에서 경험 조각 내의 모든 참조가 웹 게재에 대해 외부화되었는지 확인합니다.

   >[!NOTE]
   >
   >기본적으로 적용되지 않은 링크 재작성의 경우, [경험 조각 링크 재작성기 공급자](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) 사용할 수 있습니다. 이를 통해 사용자 지정 규칙을 사용자 인스턴스에 대해 개발할 수 있습니다.

## 클라우드 구성 추가 {#add-the-cloud-configuration}

조각을 내보내기 전에 조각을 추가해야 합니다 **클라우드 구성** 대상 **Adobe Target** 조각 또는 폴더로 이동합니다. 이 경우 다음을 수행할 수도 있습니다.

* 내보내기에 사용할 형식 옵션을 지정합니다
* Target 작업 영역을 대상으로 선택
* 경험 조각에서 참조를 재작성하기 위한 외부 도우미 도메인을 선택합니다(선택 사항).

에서 필요한 옵션을 선택할 수 있습니다. **페이지 속성** 필요한 폴더 및/또는 조각의 유형 사양은 필요에 따라 상속됩니다.

1. 로 이동합니다 **경험 조각** 콘솔.

1. 열기 **페이지 속성** 해당 폴더 또는 조각에 사용할 수 있습니다.

   >[!NOTE]
   >
   >경험 조각 상위 폴더에 클라우드 구성을 추가하는 경우 구성이 모든 하위 폴더에 의해 상속됩니다.
   >
   >
   >경험 조각 자체에 클라우드 구성을 추가하는 경우, 구성은 모든 변형에서 상속됩니다.

1. 을(를) 선택합니다 **Cloud Services** 탭.

1. 아래 **Cloud Service 구성**, 선택 **Adobe Target** 드롭다운 목록에서 을 선택합니다.

   >[!NOTE]
   >
   >경험 조각 오퍼의 JSON 형식을 사용자 지정할 수 있습니다. 이렇게 하려면 고객 경험 조각 구성 요소를 정의한 다음 구성 요소 Sling 모델에서 해당 속성을 내보내는 방법에 주석을 답니다.
   >
   >핵심 구성 요소를 참조하십시오.
   >
   >[핵심 구성 요소 - 경험 조각](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)

   아래 **Adobe Target** 선택:

   * 적절한 구성
   * 필요한 형식 옵션
   * Adobe Target 작업 공간
   * 필요한 경우 - externalizer 도메인

   >[!CAUTION]
   >
   >외부 도우미 도메인은 선택 사항입니다.
   >
   > 내보낸 컨텐츠가 특정 컨텐츠를 가리키도록 하려면 AEM 외부화제를 구성합니다 *게시* 도메인. 자세한 내용은 [AEM Link Externalizer 구성](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer).
   >
   > 또한 외부자 도메인은 Target으로 전송되는 경험 조각의 컨텐츠와만 관련되며 오퍼 컨텐츠 보기와 같은 메타데이터는 연관되지 않습니다.

   예를 들어, 폴더의 경우:

   ![폴더 - Cloud Services](assets/xf-target-integration-01.png "폴더 - Cloud Services")

1. **저장 및 닫기**.

## Adobe Target으로 경험 조각 내보내기 {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>이미지와 같은 미디어 자산의 경우 참조만 Target에 내보내집니다. 자산 자체는 AEM Assets에 저장된 상태로 유지되며 AEM 게시 인스턴스에서 전달됩니다.
>
>이로 인해 Target으로 내보내기 전에 모든 관련 자산이 있는 경험 조각을 게시해야 합니다.

AEM에서 Target으로 경험 조각을 내보내려면(클라우드 구성을 지정한 후):

1. 경험 조각 콘솔로 이동합니다.
1. target으로 내보낼 경험 조각을 선택합니다.

   >[!NOTE]
   >
   >경험 조각 웹 변형이어야 합니다.

1. 탭/클릭 **Adobe Target으로 내보내기**.

   >[!NOTE]
   >
   >경험 조각을 이미 내보낸 경우 을(를) 선택합니다. **Adobe Target에서 업데이트**.

1. 탭/클릭 **게시하지 않고 내보내기** 또는 **게시** 필요한 경우.

   >[!NOTE]
   >
   >선택 **게시** 경험 조각을 즉시 게시하여 Target에 전송합니다.

1. 탭/클릭 **확인** 확인 대화 상자에서 확인할 수 있습니다.

   이제 경험 조각이 Target에 있어야 합니다.

   >[!NOTE]
   >
   >[다양한 세부 사항](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment) 내보낼 때 **목록 보기** 콘솔 및 **속성**.

   >[!NOTE]
   >
   >Adobe Target에서 경험 조각을 볼 때는 *마지막 수정 날짜* 보이는 날짜는 조각이 Adobe Target에 마지막으로 내보낸 날짜가 아니라 AEM에서 마지막으로 조각을 수정한 날짜입니다.

>[!NOTE]
>
>또는 페이지의 [페이지 정보](/help/sites-authoring/author-environment-tools.md#page-information) 메뉴 아래의 제품에서 사용할 수 있습니다.

## Adobe Target에서 경험 조각 사용 {#using-your-experience-fragments-in-adobe-target}

이전 작업을 수행하면 경험 조각이 Target의 오퍼 페이지에 표시됩니다. 여기 좀 보세요 [특정 Target 설명서](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html) 당신이 거기서 무엇을 이룰 수 있는지 배우기 위해.

>[!NOTE]
>
>Adobe Target에서 경험 조각을 볼 때는 *마지막 수정 날짜* 보이는 날짜는 조각이 Adobe Target에 마지막으로 내보낸 날짜가 아니라 AEM에서 마지막으로 조각을 수정한 날짜입니다.

## 이미 Adobe Target으로 내보낸 경험 구성요소 삭제 {#deleting-an-experience-fragment-already-exported-to-adobe-target}

이미 Target으로 내보낸 경험 조각을 삭제하면 Target의 오퍼에서 조각을 이미 사용하고 있는 경우 문제가 발생할 수 있습니다. 조각을 삭제하면 조각 컨텐츠가 AEM에 의해 전달될 때 오퍼를 사용할 수 없게 됩니다.

이러한 상황을 피하려면

* 경험 조각이 현재 활동에서 사용되지 않는 경우 AEM에서는 경고 메시지 없이 조각을 삭제할 수 있습니다.
* 경험 조각이 현재 Target의 활동에서 사용 중인 경우 오류 메시지는 AEM 사용자에게 조각을 삭제하면 활동에 발생할 수 있는 결과에 대해 경고합니다.

   AEM의 오류 메시지에는 사용자가 경험 조각을 삭제할 수 없습니다(강제). 경험 조각이 삭제되는 경우:

   * AEM 경험 조각을 사용한 Target 오퍼에 원치 않는 동작이 표시될 수 있습니다

      * 경험 조각 HTML이 Target에 푸시되었으므로 오퍼가 여전히 렌더링될 수 있습니다
      * 참조된 자산을 AEM에서도 삭제한 경우 경험 조각의 모든 참조가 제대로 작동하지 않을 수 있습니다.
   * 물론 경험 조각이 AEM에 더 이상 존재하지 않으므로 경험 구성요소를 추가로 수정할 수는 없습니다.
