---
title: Adobe Target으로 경험 조각 내보내기
seo-title: Adobe Target으로 경험 조각 내보내기
description: Adobe Target으로 경험 조각 내보내기
seo-description: Adobe Target으로 경험 조각 내보내기
uuid: 2df0faab-5d5e-4fc1-93b3-28b7e6f3c306
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d4152b4d-531b-4b62-8807-a5bc5afe94c6
docset: aem65
translation-type: tm+mt
source-git-commit: 410858ee7d1b8022070445937731644724a90155
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 0%

---


# 경험 조각을 Adobe Target{#exporting-experience-fragments-to-adobe-target}으로 내보내기

>[!CAUTION]
>
>이 페이지의 일부 기능을 사용하려면 AEM 6.5.3.0 응용 프로그램이 필요합니다.
>
>6.5.3.0
>
>* **이제 Externalizer** Domainscan이 선택됩니다.
   >  **참고:** Externalizer 도메인은 Target으로 전송된 경험 조각의 컨텐츠에만 관련되며 오퍼 컨텐츠 보기와 같은 메타데이터는 해당되지 않습니다.
>
>
6.5.2.0:
>
>* 경험 조각을 다음 중 하나로 내보낼 수 있습니다.
   >
   >   
   * 기본 작업 공간입니다.
   >   * 클라우드 구성에 지정된 명명된 작업 공간입니다.
   >   * **참고:** 특정 작업 영역으로 내보내려면 Adobe Target Premium이 필요합니다.
>
>* AEM은 Adobe I/O[을(를) 사용하여 Adobe Target과 통합되어야 합니다.](/help/sites-administering/integration-ims-adobe-io.md)

>
>

AEM 6.5.0.0 및 6.5.1.0:
>
>* AEM 경험 조각은 Adobe Target의 기본 작업 영역으로 내보내집니다.
>* AEM은 [Adobe Target과 통합](/help/sites-administering/target.md)의 지침에 따라 Adobe Target과 통합되어야 합니다.


Adobe Experience Manager(AEM)에서 만든 [경험 조각](/help/sites-authoring/experience-fragments.md)을 Adobe Target(Target)으로 내보낼 수 있습니다. 그런 다음 Target 활동에서 오퍼로 사용하여 경험을 규모에 맞게 테스트하고 개인화할 수 있습니다.

경험 조각을 Adobe Target으로 내보내는 데 사용할 수 있는 3가지 형식 옵션은 다음과 같습니다.

* HTML(기본값):웹 및 하이브리드 컨텐츠 전달 지원
* JSON:헤드리스 컨텐츠 전달 지원
* HTML 및 JSON

AEM 경험 조각을 Adobe Target의 기본 작업 영역으로 내보내거나 Adobe Target의 사용자 정의 작업 영역으로 내보낼 수 있습니다. 이 작업은 Adobe I/O을 통해 수행됩니다. 이 경우 AEM은 Adobe I/O[을 사용하여 Adobe Target과 통합되어야 합니다.](/help/sites-administering/integration-ims-adobe-io.md)

>[!NOTE]
>
>Adobe Target 작업 영역은 Adobe Target 자체에 없습니다. Adobe IMS(Identity Management System)에서 정의 및 관리된 다음 Adobe I/O 통합을 사용하는 솔루션 간에 사용하도록 선택됩니다.

>[!NOTE]
>
>Adobe Target 작업 영역을 사용하여 조직(그룹) 구성원이 이 조직에 대한 오퍼와 활동을 만들고 관리할 수 있습니다.다른 사용자에게 액세스 권한을 부여하지 않습니다. 예를 들어 글로벌 우려 범위에서 국가별 조직을 예로 들 수 있습니다.

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
>이 페이지의 일부 기능을 사용하려면 AEM 6.5.3.0 응용 프로그램이 필요합니다.

다양한 작업이 필요합니다.

1. Adobe I/O](/help/sites-administering/integration-ims-adobe-io.md)을(를) 사용하여 [AEM과 Adobe Target을 통합해야 합니다.
2. 경험 조각은 AEM 작성자 인스턴스에서 내보내기되므로, 경험 조각 내의 모든 참조가 웹 전달에 대해 외부화되어 있는지 확인하려면 작성자 인스턴스에서 [AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer)를 구성해야 합니다.

   >[!NOTE]
   >
   >기본적으로 포함되지 않은 링크 재작성의 경우 [경험 조각 링크 다시 작성자 공급자](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html)를 사용할 수 있습니다. 이를 통해 사용자 인스턴스에 대해 사용자 정의된 규칙을 개발할 수 있습니다.

## 클라우드 구성 {#add-the-cloud-configuration} 추가

조각을 내보내기 전에 **Adobe Target**&#x200B;에 대한 **클라우드 구성**&#x200B;을 조각 또는 폴더에 추가해야 합니다. 또한 다음과 같은 작업을 수행할 수 있습니다.

* 내보내기에 사용할 형식 옵션을 지정합니다.
* target 작업 영역을 대상으로 선택
* 경험 조각에서 참조를 다시 작성하기 위한 externalizer 도메인 선택(선택 사항)

필요한 옵션은 필요한 폴더 및/또는 조각의 **페이지 속성**&#x200B;에서 선택할 수 있습니다.사양은 필요에 따라 상속됩니다.

1. **경험 조각** 콘솔로 이동합니다.

1. 해당 폴더 또는 조각에 대해 **페이지 속성**&#x200B;을 엽니다.

   >[!NOTE]
   >
   >클라우드 구성을 경험 조각 상위 폴더에 추가하는 경우 모든 하위 폴더에 의해 구성이 상속됩니다.
   >
   >
   >클라우드 구성을 경험 조각 자체에 추가하는 경우, 구성은 모든 변수에서 상속됩니다.

1. **Cloud Services** 탭을 선택합니다.

1. **Cloud Service 구성**&#x200B;의 드롭다운 목록에서 **Adobe Target**&#x200B;을 선택합니다.

   >[!NOTE]
   >
   >경험 조각 오퍼의 JSON 형식을 사용자 정의할 수 있습니다. 이렇게 하려면 고객 경험 조각 구성 요소를 정의한 다음 구성 요소 슬링 모델에서 해당 속성을 내보내는 방법에 주석을 답니다.
   >
   >핵심 구성 요소를 참조하십시오.
   >
   >[핵심 구성 요소 - 경험 조각](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)

   **Adobe Target**&#x200B;에서 다음을 선택합니다.

   * 적절한 구성
   * 필수 형식 옵션
   * adobe target 작업 영역
   * 필요한 경우 - externalizer 도메인

   >[!CAUTION]
   >
   >externalizer 도메인은 선택 사항입니다.
   >
   > 내보낸 내용이 특정 *publish* 도메인을 가리키도록 하려면 AEM 외부도우미가 구성됩니다. 자세한 내용은 [AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer) 구성을 참조하십시오.
   >
   > 또한 Externalizer 도메인은 Target으로 전송된 경험 조각의 컨텐츠에만 관련되며 오퍼 컨텐츠 보기와 같은 메타데이터는 해당되지 않습니다.

   예를 들어 폴더의 경우:

   ![폴더 - 클라우드 ](assets/xf-target-integration-01.png "서비스 폴더 - Cloud Services")

1. **저장 및 닫기**.

## 경험 조각을 Adobe Target {#exporting-an-experience-fragment-to-adobe-target}으로 내보내기

>[!CAUTION]
>
>이미지와 같은 미디어 에셋의 경우 참조만 Target으로 내보내집니다. 자산 자체는 AEM Assets에 저장되어 AEM 게시 인스턴스에서 전달됩니다.
>
>이 때문에 Target으로 내보내기 전에 모든 관련 자산이 있는 경험 조각을 게시해야 합니다.

경험 조각을 AEM에서 Target으로 내보내려면(클라우드 구성을 지정한 후):

1. 경험 조각 콘솔로 이동합니다.
1. 타겟으로 내보낼 경험 조각을 선택합니다.

   >[!NOTE]
   >
   >경험 조각 웹 변형이어야 합니다.

1. **Adobe Target**&#x200B;로 내보내기를 탭/클릭합니다.

   >[!NOTE]
   >
   >경험 조각을 이미 내보낸 경우 Adobe Target **에서**&#x200B;업데이트를 선택합니다.

1. 필요에 따라 **또는**&#x200B;게시&#x200B;**를 게시하지 않고**&#x200B;내보내기를 탭/클릭합니다.

   >[!NOTE]
   >
   >**게시**&#x200B;를 선택하면 경험 조각이 바로 게시되어 Target에 전송됩니다.

1. 확인 대화 상자에서 **확인**&#x200B;을 탭/클릭합니다.

   이제 경험 조각이 Target 내에 있어야 합니다.

   >[!NOTE]
   >
   >[내보내기](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment) 의 다양한 세부 사항은 콘솔 및  **속성** 의 목록 보기에서 확인할 수  **있습니다**.

   >[!NOTE]
   >
   >Adobe Target에서 경험 조각을 볼 때, 마지막으로 수정된 날짜 *마지막으로 수정된 날짜* 는 조각을 Adobe Target으로 마지막으로 내보낸 날짜가 아니라 AEM에서 마지막으로 수정한 날짜입니다.

>[!NOTE]
>
>또는 [페이지 정보](/help/sites-authoring/author-environment-tools.md#page-information) 메뉴의 비교 명령을 사용하여 페이지 편집기에서 내보내기를 수행할 수 있습니다.

## Adobe Target {#using-your-experience-fragments-in-adobe-target}에서 경험 조각 사용

이전 작업을 수행한 후 경험 조각은 Target의 오퍼 페이지에 표시됩니다. 여기에서 얻을 수 있는 사항에 대해 알아보려면 [특정 Target 설명서](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html)를 살펴보십시오.

>[!NOTE]
>
>Adobe Target에서 경험 조각을 볼 때, 마지막으로 수정된 날짜 *마지막으로 수정된 날짜* 는 조각을 Adobe Target으로 마지막으로 내보낸 날짜가 아니라 AEM에서 마지막으로 수정한 날짜입니다.

## Adobe Target {#deleting-an-experience-fragment-already-exported-to-adobe-target}에 이미 내보낸 경험 조각 삭제

이미 Target으로 내보낸 경험 조각을 삭제하면 해당 단편이 Target의 오퍼에서 이미 사용되고 있는 경우 문제가 발생할 수 있습니다. 조각을 삭제하면 조각 컨텐츠가 AEM에 의해 배달되므로 오퍼를 사용할 수 없게 됩니다.

이러한 상황을 피하려면

* 경험 단편이 현재 활동에 사용되지 않는 경우 AEM에서는 경고 메시지 없이 단편을 삭제할 수 있습니다.
* Target의 활동에서 경험 조각을 현재 사용 중인 경우, 조각을 삭제하면 활동에 발생할 수 있는 결과에 대해 AEM 사용자에게 오류 메시지가 표시됩니다.

   AEM의 오류 메시지로 인해 사용자가 경험 조각을 삭제할 수 없습니다(강제-). 경험 조각이 삭제된 경우:

   * AEM 경험 조각의 Target 오퍼에 원하지 않는 동작이 표시될 수 있습니다.

      * 경험 조각 HTML이 Target으로 푸시되었기 때문에 오퍼는 여전히 렌더링됩니다
      * 참조된 자산이 AEM에서도 삭제된 경우 경험 조각의 모든 참조가 제대로 작동하지 않을 수 있습니다.
   * 물론 경험 조각은 AEM에 더 이상 존재하지 않으므로 경험 조각에 대한 추가 수정은 불가능합니다.