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
source-git-commit: 88763b318e25efb16f61bc16530082877392c588
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 65%

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
>* AEM 경험 조각은 Adobe Target의 기본 작업 영역으로 내보내집니다.
>* [Adobe Target과 통합](/help/sites-administering/target.md)의 지침에 따라 Adobe Target과 AEM을 통합해야 합니다.


내보낼 수 있습니다 [경험 조각](/help/sites-authoring/experience-fragments.md): Adobe Experience Manager(AEM)에서 만든 Adobe Target(Target)으로 이동합니다. 그런 다음 Target 활동의 오퍼로 사용하여 경험을 대규모로 테스트하고 개인화할 수 있습니다.

Adobe Target으로 경험 조각을 내보내는 데 사용할 수 있는 세 가지 형식 옵션이 있습니다.

* HTML(기본값): 웹 및 하이브리드 콘텐츠 전송 지원
* JSON: 헤드리스 콘텐츠 전송 지원
* HTML 및 JSON

AEM 경험 구성요소를 Adobe Target의 기본 작업 공간으로 내보내거나 Adobe Target의 사용자 지정 작업 공간으로 내보낼 수 있습니다. 이 작업은 Adobe Developer 콘솔을 사용하여 수행됩니다. 이 경우 AEM이 [ims를 사용하여 Adobe Target과 통합](/help/sites-administering/integration-target-ims.md).

>[!NOTE]
>
>Adobe Target 작업 영역은 Adobe Target 자체에 존재하지 않습니다. Adobe IMS(Identity Management 시스템)에서 정의 및 관리된 다음, Adobe Developer 콘솔의 통합을 사용하여 솔루션 간에 사용하도록 선택됩니다.

>[!NOTE]
>
>Adobe Target 작업 영역을 사용하여 다른 사용자에게 액세스 권한을 제공하지 않고 조직(그룹)의 멤버가 해당 조직만을 위한 오퍼 및 활동을 만들고 관리하도록 할 수 있습니다. 예: 세계적으로 관심을 받는 국가별 조직

>[!NOTE]
>
>또한 자세한 내용은 다음을 참조하십시오.
>
>* [Adobe Target 개발](https://www.adobe.io/apis/experiencecloud/target.html)
>* [핵심 구성 요소 - 경험 조각](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/experience-fragment.html)
>


## 사전 요구 사항 {#prerequisites}

>[!CAUTION]
>
>이 페이지의 일부 기능을 사용하려면 AEM 6.5.3.0을 적용해야 합니다.

다음과 같은 다양한 작업을 수행해야 합니다.

1. 당신은 [ims를 사용하여 AEM과 Adobe Target 통합.](/help/sites-administering/integration-target-ims.md).
2. AEM 작성자 인스턴스에서 경험 조각을 내보내므로, 경험 조각 내의 모든 참조가 웹 전송에 대해 외부화되도록 작성자 인스턴스에서 [AEM 링크 외부화를 구성](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer)해야 합니다.

   >[!NOTE]
   >
   >여기에서 기본적으로 다루지 않는 링크 재작성은 [경험 조각 링크 재작성기 공급자](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html)를 사용할 수 있습니다. 이를 통해 맞춤화된 규칙을 인스턴스에 맞게 개발할 수 있습니다.

## 클라우드 구성 추가 {#add-the-cloud-configuration}

조각을 내보내기 전에 **Adobe Target**&#x200B;용 **클라우드 구성**&#x200B;을 조각 또는 폴더에 추가해야 합니다. 이렇게 하면 다음과 같은 작업도 수행할 수 있습니다.

* 내보내기에 사용할 형식 옵션 지정
* Target 작업 영역을 대상으로 선택
* 경험 조각의 참조 재작성을 위한 외부화 도메인 선택 (선택 사항)

필요한 옵션은 필요한 폴더 및/또는 조각의 **페이지 속성**&#x200B;에서 선택할 수 있습니다. 사양은 필요에 따라 상속됩니다.

1. **경험 조각** 콘솔로 이동합니다.

1. 적절한 폴더 또는 조각에 대한 **페이지 속성**&#x200B;을 엽니다.

   >[!NOTE]
   >
   >클라우드 구성을 경험 조각 상위 폴더에 추가하면 해당 구성은 모든 하위 폴더에 상속됩니다.
   >
   >
   >클라우드 구성을 경험 조각에 추가하면 해당 구성은 모든 변형에 상속됩니다.

1. **클라우드 서비스** 탭을 선택합니다.

1. **클라우드 서비스 구성** 아래의 드롭다운 목록에서 **Adobe Target**&#x200B;을 선택합니다.

   >[!NOTE]
   >
   >경험 조각 오퍼의 JSON 형식을 맞춤화할 수 있습니다. 이렇게 하려면 고객 경험 조각 구성 요소를 정의한 다음 구성 요소 Sling 모델에서 속성을 내보내는 방법에 대한 주석을 달아야 합니다.
   >
   >핵심 구성 요소를 참조하십시오.
   >
   >[핵심 구성 요소 - 경험 조각](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/experience-fragment.html)

   **Adobe Target**&#x200B;에서 다음을 선택합니다.

   * 적절한 구성
   * 필요한 형식 옵션
   * Adobe Target 작업 영역
   * 필요한 경우 - 외부화 도메인

   >[!CAUTION]
   >
   >외부화 도메인은 선택 사항입니다.
   >
   >내보낸 콘텐츠가 특정 *게시* 도메인을 가리키도록 하면 AEM 외부화가 구성됩니다. 자세한 내용은 [AEM 링크 외부화 구성](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer)을 참조하십시오.
   >
   >또한 외부화 도메인은 오퍼 콘텐츠 보기와 같은 메타데이터가 아닌 Target에 전송되는 경험 조각의 콘텐츠에만 관련이 있습니다.

   폴더의 경우 그 예는 다음과 같습니다.

   ![폴더 - 클라우드 서비스](assets/xf-target-integration-01.png "폴더 - 클라우드 서비스")

1. **저장 및 닫기**.

## Adobe Target으로 경험 조각 내보내기 {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>이미지와 같은 미디어 에셋의 경우 하나의 참조만 Target으로 가져올 수 있습니다. 에셋 자체는 AEM Assets 내에 저장되며 AEM 게시 인스턴스에서 전달됩니다.
>
>이로 인해 경험 조각 및 관련된 모든 에셋은 Target으로 내보내기 전에 게시되어야 합니다.

AEM에서 Target으로 경험 조각을 내보내려면(클라우드 구성 지정 이후):

1. 경험 조각 콘솔로 이동합니다.
1. Target으로 내보내고자 하는 경험 조각을 선택합니다.

   >[!NOTE]
   >
   >이는 경험 조각 웹 변형이어야 합니다.

1. **Adobe Target으로 내보내기**&#x200B;를 탭/클릭합니다.

   >[!NOTE]
   >
   >경험 조각을 이미 내보낸 경우 **Adobe Target에서 업데이트**&#x200B;를 선택합니다.

1. 필요에 따라 **게시하지 않고 내보내기** 또는 **게시**&#x200B;를 탭/클릭합니다.

   >[!NOTE]
   >
   >**게시**&#x200B;를 선택하면 경험 조각이 즉시 게시되며 Target에 전송됩니다.

1. 확인 대화 상자에서 **확인**&#x200B;을 탭/클릭합니다.

   이제 경험 조각은 Target에 있게 됩니다.

   >[!NOTE]
   >
   >내보내기에 대한 [다양한 세부 정보](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment)는 콘솔의 **목록 보기** 및 **속성**&#x200B;에서 볼 수 있습니다.

   >[!NOTE]
   >
   >Adobe Target에서 경험 조각을 볼 때 표시되는 *마지막 수정* 날짜는 조각을 Adobe Target으로 마지막으로 내보낸 날짜가 아닌 AEM에서 마지막으로 수정한 날짜입니다.

>[!NOTE]
>
>또는 [페이지 정보](/help/sites-authoring/author-environment-tools.md#page-information) 메뉴의 비슷한 명령을 사용하여 페이지 편집기에서 내보내기를 수행할 수 있습니다.

## Adobe Target에서 경험 조각 사용 {#using-your-experience-fragments-in-adobe-target}

이전 작업을 수행하면 경험 조각이 Target의 오퍼 페이지에 표시됩니다. 여기에서 수행할 수 있는 작업에 대해 알아보려면 [관련 Target 설명서](https://experiencecloud.adobe.com/resources/help/ko_KR/target/target/aem-experience-fragments.html)를 살펴보십시오.

>[!NOTE]
>
>Adobe Target에서 경험 조각을 볼 때 표시되는 *마지막 수정* 날짜는 조각을 Adobe Target으로 마지막으로 내보낸 날짜가 아닌 AEM에서 마지막으로 수정한 날짜입니다.

## 이미 Adobe Target으로 내보낸 경험 조각 삭제 {#deleting-an-experience-fragment-already-exported-to-adobe-target}

이미 Target으로 내보낸 경험 조각을 삭제하면 Target의 오퍼에서 해당 조각을 사용 중인 경우 문제가 발생할 수 있습니다. AEM에서 조각 콘텐츠를 전달 중이므로 조각을 삭제하면 오퍼를 사용할 수 없습니다.

이러한 상황을 방지하는 방법:

* 경험 조각이 현재 활동에서 사용되고 있지 않은 경우, 사용자는 AEM을 통해 경고 메시지 없이 조각을 삭제할 수 있습니다.
* 경험 조각이 현재 활동에서 사용되고 있는 경우, 조각 삭제가 활동에 미칠 수 있는 결과를 나타내는 경고 메시지가 AEM 사용자에게 표시됩니다.

   AEM에 오류 메시지가 표시되어도 사용자는 경험 조각을 삭제할 수 있습니다. 경험 조각을 삭제하면 다음과 같은 결과가 발생합니다.

   * AEM 경험 조각 및 Target 오퍼가 원하지 않은 동작을 수행할 수 있습니다.

      * 경험 조각 HTML이 Target으로 푸시되었으므로 해당 오퍼는 여전히 렌더링될 수 있습니다.
      * AEM에서 참조된 에셋을 삭제해도 경험 조각의 참조가 올바르게 작동하지 않을 수 있습니다.
   * 물론, AEM에 경험 조각이 더 이상 존재하지 않으므로 이후에 경험 조각을 수정할 수 없습니다.



## Target으로 내보낸 경험 조각에서 ClientLibs 제거 {#removing-clientlibs-from-fragments-exported-target}

경험 조각은 전체 html 태그와 필요한 모든 클라이언트 라이브러리(CSS/JS)를 포함하여 경험 조각 컨텐츠 작성자가 만든 것처럼 조각을 정확히 렌더링합니다. 이것은 디자인이 있습니다.

AEM에서 전달하는 페이지에서 Adobe Target과 함께 경험 조각 오퍼를 사용하는 경우 타깃팅된 페이지에 이미 필요한 모든 클라이언트 라이브러리가 포함되어 있습니다. 또한 경험 조각 오퍼에서 외부 html도 필요하지 않습니다(참조) [고려 사항](#considerations)).

다음은 경험 조각 오퍼에서 html의 의사 예입니다.

```html
<!DOCTYPE>
<html>
   <head>
      <title>…</title>
      <!-- all of the client libraries (css/js) -->
      …
   </head>
   <body>
        <!--/* Actual XF Offer content would appear here... */-->
   </body>
</html>
```

높은 수준에서 AEM이 경험 조각을 Adobe Target으로 내보낼 때 여러 개의 추가 Sling 선택기를 사용합니다. 예를 들어 내보낸 경험 조각의 URL은 다음과 같을 수 있습니다(알림) `nocloudconfigs.atoffer`):

* http://www.your-aem-instance.com/content/experience-fragments/my-offers/my-xf-offer.nocloudconfigs.atoffer.html

다음 `nocloudconfigs` 선택기는 HTL을 사용하여 정의되며, 다음 위치에서 복사하여 오버레이할 수 있습니다.

* /libs/cq/experience-fragments/components/xfpage/nocloudconfigs.html

다음 `atoffer` 선택기는 실제로 을 사용하여 사후 처리에 적용됩니다 [Sling Rewriter](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html). 둘 중 하나를 사용하여 클라이언트 라이브러리를 제거할 수 있습니다.

### 예 {#example}

이를 위해 다음을 사용하여 이 작업을 수행하는 방법을 설명하겠습니다 `nocloudconfigs`.

>[!NOTE]
>
>자세한 내용은 [편집 가능한 템플릿](/help/sites-developing/templates.md#editable-templates) 자세한 내용

#### 오버레이 {#overlays}

이 특정 예에서는 [오버레이](/help/sites-developing/overlays.md) 포함되면 클라이언트 라이브러리가 제거됩니다 *및* 외부 html. 경험 조각 템플릿 유형을 이미 작성했다고 가정합니다. 복사해야 하는 필수 파일 `/libs/cq/experience-fragments/components/xfpage/` 포함:

* `nocloudconfigs.html`
* `head.nocloudconfigs.html`
* `body.nocloudconfigs.html`

#### 템플릿 유형 오버레이 {#template-type-overlays}

이 예제에서는 다음 구조를 사용합니다.

![템플릿 유형 오버레이](assets/xf-target-integration-02.png "템플릿 유형 오버레이")

이러한 파일의 내용은 다음과 같습니다.

* `body.nocloudconfigs.html`

   ![body.nocloudconfigs.html](assets/xf-target-integration-03.png "body.nocloudconfigs.html")

* `head.nocloudconfigs.html`

   ![head.nocloudconfigs.html](assets/xf-target-integration-04.png "head.nocloudconfigs.html")

* `nocloudconfigs.html`

   ![nocloudconfigs.html](assets/xf-target-integration-05.png "nocloudconfigs.html")

>[!NOTE]
>
>를 사용하려면 `data-sly-unwrap` body 태그를 제거하려면 `nocloudconfigs.html`.

### 고려 사항 {#considerations}

Adobe Target에서 경험 조각 오퍼를 사용하여 AEM 사이트와 비 AEM 사이트를 모두 지원해야 하는 경우 두 개의 경험 조각(두 개의 다른 템플릿 유형)을 만들어야 합니다.

* clientlibs/extra html을 제거하는 오버레이가 있는 항목

* 오버레이가 없으므로 필수 clientlibs를 포함하는 것