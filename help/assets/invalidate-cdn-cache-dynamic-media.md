---
title: 다이내믹 미디어를 통해 CDN 캐시 무효화
description: CDN(Content Delivery Network) 캐시 컨텐츠를 무효화할 수 있으므로 캐시 만료가 기다리는 대신 다이내믹 미디어에서 제공하는 자산을 신속하게 업데이트할 수 있습니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: 54645149dc4968c1c4f85eedb5ce4d71f80c3b64
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 1%

---


# 다이내믹 미디어를 통해 CDN 캐시 무효화 {#invalidating-cdn-cache-for-dm-assets}

다이내믹 미디어 자산은 CDN(Content Delivery Network)에 의해 캐시되어 고객에게 빠르게 배달됩니다. 그러나 이러한 에셋을 업데이트할 때 해당 변경 사항이 웹 사이트에서 즉시 적용될 수 있습니다. CDN 캐시를 지우거나 무효화하면 Dynamic Media에서 제공하는 자산을 신속하게 업데이트할 수 있습니다. TTL(Time To Live) 값(기본값은 10시간)을 사용하여 캐시가 만료되기를 기다리는 대신 Dynamic Media 사용자 인터페이스에서 몇 분 내에 캐시가 만료되도록 요청을 보낼 수 있습니다.

>[!IMPORTANT]
>
>다음 단계는 Dynamic Media - AEM 6.5, 서비스 팩 6(AEM 6.5.6) 이상의 Scene7 모드에만 적용됩니다. 이 CDN 무효화 기능을 사용하려면 AEM Dynamic Media와 번들로 제공되는 기본 CDN을 사용해야 합니다.기타 모든 사용자 지정 CDN은 지원되지 않습니다.<br>AEM 6.5, 서비스 팩 5(AEM 6.5.5) 또는 이전 버전에서 Dynamic Media를 사용하는 경우 Dynamic Media Classic을 통해 [CDN 캐시 무효화에 있는 단계를 따릅니다.](/help/assets/invalidate-cdn-cache-dm-classic.md)

Dynamic [Media의 캐싱 개요를 참조하십시오](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**다이내믹 미디어 자산에 대해 CDN 캐시된 컨텐츠를 무효화하려면:**

*2부 1부:CDN 무효화 템플릿 만들기*

1. AEM 6.5.6 이상에서 **[!UICONTROL 도구 > 자산 > CDN 무효화를 누릅니다.]**

   ![CDN 유효성 검사 기능](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. CDN **[!UICONTROL 무효화 템플릿]** 페이지에서 시나리오에 따라 다음 옵션 중 하나를 수행합니다.

   | 시나리오 | 옵션 |
   | --- | --- |
   | 이전에 Dynamic Media Classic을 사용하여 CDN 무효화 템플릿을 이미 만들었습니다. | 템플릿 **[!UICONTROL 만들기]** 텍스트 필드는 템플릿 데이터로 미리 채워집니다. 이러한 경우 템플릿을 편집하거나 다음 단계를 계속 진행할 수 있습니다. |
   | 템플릿을 만들어야 합니다. 무엇을 입력해야 합니까? | 템플릿 **[!UICONTROL 만들기]** 텍스트 필드에 다음 예제와 같이 특정 이미지 ID 대신 참조하는 이미지 URL(이미지 사전 설정 또는 수정자 포함) `<ID>`을 입력합니다.<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>템플릿에 `<ID>`가 정의만 있는 경우 Dynamic Media는 Dynamic Media Classic의 일반 설정에 정의된 게시 서버 이름 `https://<publishserver_name>/is/image/<company_name>/<ID>` `<publishserver_name>` 의 위치를 채웁니다.이 AEM 인스턴스 `<company_name>` `<ID>` 와 연결된 회사 루트 이름이며, 무효화할 자산 선택기를 통해 선택한 자산입니다.<br>모든 사전 설정/수정자 게시물 `<ID>` 이 URL 정의에 있는 그대로 복사됩니다.<br>템플릿을 기반으로 자동으로 이미지 `/is/image` 를 만들 수 있습니다.<br>예를 `/is/content/`들어 자산 선택기를 사용하여 비디오 또는 PDF와 같은 에셋을 추가해도 URL이 자동으로 생성되지 않습니다. 대신 CDN 무효화 템플릿에서 이러한 자산을 지정해야 하거나, *제2부의 이러한 자산에 URL을 수동으로 추가할 수 있습니다.CDN 무효화 옵션*&#x200B;설정&#x200B;<br>**예:**<br>&#x200B;이 첫 번째 예에서 무효화 템플릿에는 자산 URL과 `<ID>` 함께 포함되어 `/is/content`있습니다. 예, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Dynamic Media는 이를 기반으로 한 URL을 형성하며, 무효화할 자산 선택기를 통해 자산을 선택합니다 `<ID>` .<br>이 두 번째 예에서 무효화 템플릿에는 웹 속성에 사용된 자산의 전체 URL이 포함되어 있습니다(자산 선택기에 `/is/content` 종속되지 않음). 예를 들어 배낭 `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` 은 자산 ID입니다.<br>Dynamic Media에서 지원되는 자산 형식은 무효화할 수 있습니다. CDN 무효화에 대해 *지원되지* 않는 에셋 파일 형식으로는 Postscript, Encapsulated Postscript, Adobe Illustrator, Adobe InDesign, Microsoft Powerpoint, Microsoft Excel, Microsoft Word 및 리치 텍스트 형식이 있습니다.<br>템플릿을 만들 때는 구문과 오타 문자에 주의를 기울여야 합니다.Dynamic Media에서는 템플릿 유효성 검사가 수행되지 않습니다.<br>이 CDN 무효화 템플릿 또는 2부의 URL **[!UICONTROL 추가]** 텍스트 필드에서 이미지 스마트 자르기에 대한 URL을 지정해야 *합니다.CDN 무효화 옵션 설정을 참조하십시오.*<br>**중요:**CDN 무효화 템플릿의 각 항목은 해당 줄에 있어야 합니다.<br>*다음 템플릿 예는 그림 목적으로만 사용됩니다.* |

   ![CDN 무효화 템플릿 - 만들기](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. CDN **[!UICONTROL 무효화 템플릿]** 페이지의 오른쪽 맨 위에서 **[!UICONTROL 저장을]**&#x200B;누른 다음 **[!UICONTROL 확인을누릅니다.]**<br>   *2부:CDN 무효화 옵션 설정*
   <br>

1. AEM에서 Cloud Service으로 **[!UICONTROL 도구 > 자산 > CDN 무효화를 누릅니다.]**

   ![CDN 유효성 검사 기능](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. CDN **[!UICONTROL 무효화 - 세부 사항]** 추가 페이지에서 CDN 무효화에 대한 자산을 선택합니다.

   ![CDN 무효화 - 세부 사항 추가](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >CDN **[!UICONTROL 에서 자산 관련 이미지 사전 설정 무효화 옵션]** 을 선택 취소하지 않고 *[템플릿* 기준 무효화]를 선택한 자산의 **** 기본 URL이 무효화되도록 만들어집니다. 이미지만 이 옵션 배열을 사용해야 합니다.


   | 옵션 | 설명 |
   | --- | --- |
   | **[!UICONTROL CDN에서 자산 관련 이미지 사전 설정 무효화]** | (선택 사항) 이 옵션을 선택하면 선택한 자산과 관련된 모든 이미지 사전 설정 URL이 캐시 무효화를 위해 자동 구성됩니다.<br>에셋 및 관련 사전 정의된 사전 설정 URL은 무효화를 위해 자동 구성됩니다. 이 옵션은 이미지 에셋에만 작동합니다. |
   | **[!UICONTROL 템플릿을 기반으로 한 무효화]** | (선택 사항) URL 정보에 대해 정의된 템플릿만 사용하려면 이 옵션을 선택합니다. |
   | **[!UICONTROL 자산 추가]** | 자산 선택기를 사용하여 무효화할 자산을 선택합니다. 게시되었거나 게시 취소된 자산을 선택할 수 있습니다.<br>CDN의 캐싱은 자산 기반이 아닌 URL 기반입니다. 따라서 웹 사이트에 있는 전체 URL을 알고 있어야 합니다. 해당 URL을 결정한 후 템플릿에 추가할 수 있습니다. 그런 다음 해당 자산을 선택하여 추가하고 한 번에 URL을 무효화할 수 있습니다. <br>CDN의 자산 관련 이미지 사전 설정 **[!UICONTROL 무효화 또는 템플릿]**&#x200B;기반 **[!UICONTROL 무효화]**&#x200B;또는 둘 다와 함께 이 옵션을 사용합니다. |
   | **[!UICONTROL URL 추가]** | 무효화하려는 CDN 캐시가 있는 다이내믹 미디어 자산에 전체 URL 경로를 수동으로 추가하거나 붙여 넣습니다. 2부 ***1에서 CDN 무효화 템플릿을 만들지 않은 경우 이 옵션을 사용합니다.CDN 무효화 템플릿***&#x200B;만들기와 무효화할 자산이 몇 개만 있습니다.<br>**중요:** 추가하는 각 URL은 해당 줄에 있어야 합니다.<br>한 번에 최대 1000개의 URL을 무효화할 수 있습니다. [URL **[!UICONTROL 추가] 텍스트 필드의 URL]** 수가 1000을 초과하는 경우 [다음]을 탭할 수 **[!UICONTROL 없습니다]**. 이러한 경우 선택한 자산의 오른쪽에 **[!UICONTROL X]** 또는 수동으로 추가한 URL을 눌러 무효화 목록에서 삭제해야 합니다.<br>CDN 무효화 템플릿 또는 이 URL **[!UICONTROL 추가]** 텍스트 필드에서 이미지 스마트 자르기의 URL을 지정해야 합니다. |

1. Near the upper-right corner of the page, tap **[!UICONTROL Next.]**
1. CDN 무효화 - **[!UICONTROL 확인]** 페이지의 **[!UICONTROL URL]** 목록 상자에 이전에 만든 CDN 무효화 템플릿과 방금 추가한 자산의 목록이 표시됩니다.

   예를 들어 이전 단계에 표시된 CDN 무효화 템플릿 예제를 사용하여 이름이 지정된 단일 자산을 추가했다고 가정합니다 `spinset`. [ **[!UICONTROL 도구] > [자산] > [CDN 무효화]** ]를 탭하면 **[!UICONTROL CDN [무효화] - [사용자 인터페이스 확인]** ]에서 다음 5개의 생성된 URL이 생성됩니다.

   ![CDN 무효화 - 확인](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   필요한 경우 URL 오른쪽의 **X** 를 눌러 무효화 프로세스에서 삭제합니다.

1. 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 제출을]** 탭하여 CDN 무효화 프로세스를 시작합니다.

## CDN 무효화 오류 문제 해결

모든 경우, 전체 배치가 무효화되도록 처리되거나 전체 배치가 실패합니다.

| 오류 | 설명 |
| --- | --- |
| *선택한 자산에 대한 URL을 검색하지 못했습니다.* | 다음 시나리오가 충족되면 발생합니다.<br>- Dynamic Media 구성을 찾을 수 없습니다.<br>- Dynamic Media 구성을 읽은 서비스 사용자를 검색하는 동안 예외가 있습니다.<br>- URL을 구성하는 데 사용되는 게시 서버 또는 회사 루트가 Dynamic Media 구성에 없습니다. |
| *일부 URL이 올바르게 정의되지 않았습니다. 수정 후 다시 제출하십시오.* | IPS CDN 캐시 무효화 API가 URL이 다른 회사를 참조하고 있거나 IPS cdnCacheInvalidation API가 수행하는 유효성 검사에 대해 URL이 유효하지 않은 오류를 반환하는 경우 발생합니다. |
| *CDN 캐시를 무효화하지 못했습니다.* | 다른 이유로 CDN 캐시 무효화 요청이 실패하는 경우 발생합니다. |
| *무효화할 URL이 입력되어 있지 않습니다.* | CDN 무효화 - **[!UICONTROL 확인]** 페이지에 URL이 없는 경우, 제출을 **[!UICONTROL 탭하면 발생합니다.]** |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
