---
title: Dynamic Media을 통해 CDN 캐시 무효화
description: CDN(Content Delivery Network) 캐시 콘텐츠를 무효화하면 캐시가 만료될 때까지 기다리는 대신 Dynamic Media에서 제공하는 자산을 빠르게 업데이트할 수 있습니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
role: Business Practitioner, Administrator
exl-id: 23d3c274-0736-49f7-8d44-a56a55cfd06d
feature: CDN 캐시
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '1366'
ht-degree: 1%

---

# Dynamic Media {#invalidating-cdn-cache-for-dm-assets}의 방식으로 CDN 캐시 무효화

Dynamic Media 자산은 CDN(Content Delivery Network)에 의해 캐시되므로 고객에게 빠르게 전달할 수 있습니다. 그러나 그러한 자산을 업데이트할 때에는 이러한 변경 사항을 웹 사이트에서 즉시 적용할 수 있습니다. CDN 캐시를 지우거나 무효화하면 Dynamic Media에서 제공하는 자산을 빠르게 업데이트할 수 있습니다. TTL(Time To Live) 값(기본값 10시간)을 사용하여 캐시가 만료될 때까지 기다리는 대신 Dynamic Media 내에서 캐시가 몇 분 내에 만료되도록 요청을 보낼 수 있습니다.

>[!NOTE]
>
>이 기능을 사용하려면 Adobe Experience Manager Dynamic Media과 함께 번들로 제공되는 기본 CDN을 사용해야 합니다. 다른 모든 사용자 지정 CDN은 이 기능에서 지원되지 않습니다.

>[!IMPORTANT]
>
>다음 단계는 Adobe Experience Manager 6.5, 서비스 팩 6(Experience Manager 6.5.6) 이상의 Dynamic Media - Scene7 모드에만 적용됩니다. 이 CDN 무효화 기능을 사용하려면 Experience Manager Dynamic Media과 번들로 제공되는 기본 CDN을 사용해야 합니다.다른 모든 사용자 지정 CDN은 지원되지 않습니다.<br>Experience Manager 6.5, 서비스 팩 5(Experience Manager 6.5.5) 또는 이전 버전에서 Dynamic Media을 사용하는 경우 Dynamic Media Classic [을 통해 CDN 캐시 무효화에 있는 단계를 수행합니다.](/help/assets/invalidate-cdn-cache-dm-classic.md)

Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)에서 [캐싱 개요 를 참조하십시오.

**Dynamic Media 자산에 대해 CDN 캐시 컨텐츠를 무효화하려면:**

*2부 1:CDN 무효화 템플릿 만들기*

1. Experience Manager 6.5.6 이상에서 **[!UICONTROL 도구 > Assets > CDN 무효화.]**&#x200B;를 누릅니다.

   ![CDN 유효성 검사 기능](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. **[!UICONTROL CDN 무효화 템플릿]** 페이지에서 시나리오에 따라 다음 옵션 중 하나를 수행합니다.

   | 시나리오 | 옵션 |
   | --- | --- |
   | Dynamic Media Classic을 사용하여 이전에 CDN 무효화 템플릿을 이미 만들었습니다. | **[!UICONTROL 템플릿 만들기]** 텍스트 필드는 템플릿 데이터로 미리 채워집니다. 이러한 경우 템플릿을 편집하거나 다음 단계를 계속 진행할 수 있습니다. |
   | 템플릿을 만들어야 합니다. 어떻게 들어가나요? | **[!UICONTROL 템플릿 만들기]** 텍스트 필드에 다음 예와 같이 특정 이미지 ID 대신 `<ID>`를 참조하는 이미지 URL(이미지 사전 설정 또는 수정자 포함)을 입력합니다.<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>템플릿에 `<ID>`만 포함되어 있으면 Dynamic Media은 `https://<publishserver_name>/is/image/<company_name>/<ID>`로 채워집니다. 여기서 `<publishserver_name>`은 Dynamic Media Classic의 일반 설정에 정의된 게시 서버의 이름입니다. `<company_name>`은 이 Experience Manager 인스턴스와 연결된 회사 루트의 이름이고 `<ID>`은 무효화할 자산 선택기를 통해 선택한 자산입니다.<br>모든 사전 설정/수정자  `<ID>` 게시물이 URL 정의에 있는 그대로 복사됩니다.<br>템플릿 `/is/image` 을 기반으로 이미지를 자동으로 만들 수 있습니다.<br>의  `/is/content/`경우 자산 선택기를 사용하여 비디오 또는 PDF와 같은 자산을 추가해도 URL이 자동으로 생성되지 않습니다. 대신 CDN 무효화 템플릿에서 그러한 자산을 지정해야 하거나 또는 수동으로 *2부:CDN 무효화 옵션 설정*.<br>**예:**<br>&#x200B;이 첫 번째 예에서는 무효화 템플릿에 이 `<ID>` 의 자산 URL과 함께 이  `/is/content`가 포함됩니다. 예, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Dynamic Media은 이 경로를 기반으로 URL을 형성하며 이 URL은 무효화하려는 자산 선택기를 통해 선택한 자산입니다.`<ID>`<br>이 두 번째 예에서 무효화 템플릿에는 자산 선택기에  `/is/content` 의존하지 않고 와 함께 웹 속성에 사용되는 자산의 전체 URL이 포함되어 있습니다. 예를 들어, `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` 여기서 backpack은 자산 ID입니다.<br>Dynamic Media에서 지원되는 자산 형식은 무효화할 수 있습니다. CDN 무효화에 대해 지원되지 않는 *은(는) PostScript®, Encapsulated PostScript®, Adobe Illustrator, Adobe InDesign, Microsoft Powerpoint, Microsoft Excel, Microsoft Word 및 리치 텍스트 형식이 포함되어 있습니다.*<br>템플릿을 만들 때는 구문과 오식에 주의하십시오.Dynamic Media에서는 템플릿 유효성 검사를 수행하지 않습니다.<br>이 CDN 무효화 템플릿 또는  **[!UICONTROL 2부의]** URL  *텍스트 추가 필드에서 이미지 스마트 자르기의 URL을 지정합니다.CDN 무효화 옵션을 설정합니다.*<br>**중요:**CDN 무효화 템플릿의 각 항목은 해당 행에 있어야 합니다.<br>*다음 템플릿 예제는 그림 용도로만 사용됩니다.* |

   ![CDN 무효화 템플릿 - 만들기](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. **[!UICONTROL CDN 무효화 템플릿]** 페이지의 오른쪽 위 모서리에서 **[!UICONTROL 저장]**&#x200B;을 탭한 다음 **[!UICONTROL 확인]**<br>을 탭합니다.

   *2부:CDN 무효화 옵션 설정*
   <br>

1. Cloud Service으로 Experience Manager에서 **[!UICONTROL 도구 > 자산 > CDN 무효화.]**&#x200B;를 누릅니다.

   ![CDN 유효성 검사 기능](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. **[!UICONTROL CDN 무효화 - 세부 정보 추가]** 페이지에서 CDN 무효화에 대한 자산을 선택합니다.

   ![CDN 무효화 - 세부 정보 추가](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >CDN ]***및***[!UICONTROL &#x200B;템플릿&#x200B;]**을 기준으로 무효화 옵션을 선택 취소하도록 선택한 자산의 기본 URL이 무효화되도록 하는 경우, 선택한 자산의 기본 URL이 무효화되도록 형성됩니다.**[!UICONTROL  이미지에만 이 옵션 배열을 사용합니다.


   | 옵션 | 설명 |
   | --- | --- |
   | **[!UICONTROL CDN에서 자산 관련 이미지 사전 설정 무효화]** | (선택 사항) 이 옵션을 선택하면 선택한 자산과 연결된 모든 이미지 사전 설정 URL이 캐시 무효화에 대해 자동 구성됩니다.<br>자산 및 관련 사전 정의된 사전 설정 URL은 무효화를 위해 자동으로 구성됩니다. 이 옵션은 이미지 자산에만 작동합니다. |
   | **[!UICONTROL 템플릿 기반 무효화]** | (선택 사항) URL 구성에 정의된 템플릿만 사용하려면 이 옵션을 선택합니다. |
   | **[!UICONTROL 자산 추가]** | 무효화할 자산을 선택하려면 자산 선택기를 사용합니다. 게시된 자산 또는 게시 취소된 자산을 선택할 수 있습니다.<br>CDN에서 캐싱은 자산 기반이 아닌 URL 기반입니다. 따라서 웹 사이트에 있는 전체 URL을 알고 있어야 합니다. 그러한 URL을 결정한 후 템플릿에 추가할 수 있습니다. 그런 다음 해당 자산을 선택하고 추가하고 한 단계에서 URL을 무효화할 수 있습니다. <br>CDN에서  **[!UICONTROL 자산 관련 이미지 사전 설정을 무효화하거나]**, 템플릿 기반 **[!UICONTROL 의 무효화]** 또는 둘 다에 이 옵션을 사용합니다. |
   | **[!UICONTROL URL 추가]** | 무효화하려는 CDN 캐시가 있는 Dynamic Media 자산에 전체 URL 경로를 수동으로 추가 또는 붙여 넣습니다. ***2의 1부에서 CDN 무효화 템플릿을 만들지 않은 경우 이 옵션을 사용합니다.CDN 무효화 템플릿*** 만들기에 사용할 자산이 몇 개만 있습니다.<br>**중요:**  추가하는 각 URL은 자체 줄에 있어야 합니다.<br>한 번에 최대 1000개의 URL을 무효화할 수 있습니다. **[!UICONTROL URL 추가]** 텍스트 필드의 URL 수가 1000개를 초과하는 경우 **[!UICONTROL 다음]**&#x200B;을(를) 탭할 수 없습니다. 이러한 경우 선택한 자산의 오른쪽에 있는 **[!UICONTROL X]**&#x200B;을 탭하거나 수동으로 추가한 URL을 탭하여 무효화 목록에서 삭제해야 합니다.<br>CDN 무효화 템플릿 또는 이 URL 텍스트 추가 필드에서 이미지 스마트 자르기의  **[!UICONTROL URL]** 을 지정합니다. |

1. 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 다음.]**
1. **[!UICONTROL CDN 무효화 - Confirm]** 페이지의 **[!UICONTROL URL]** 목록 상자에서, 이전에 만든 CDN 무효화 템플릿과 방금 추가한 자산에서 생성된 하나 이상의 URL 목록을 볼 수 있습니다.

   예를 들어, 이전 단계에 표시된 CDN 무효화 템플릿 예제를 사용하여 `spinset` 라는 단일 자산을 추가했다고 가정합니다. **[!UICONTROL 도구 > Assets > CDN 무효화]**&#x200B;를 탭하면 **[!UICONTROL CDN 무효화 - Confirm]** 사용자 인터페이스에 다음 5개의 생성된 URL이 표시됩니다.

   ![CDN 무효화 - 확인](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   필요한 경우 URL 오른쪽의 **X**&#x200B;을 탭하여 무효화 프로세스에서 삭제합니다.

1. 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL Submit]**&#x200B;을 눌러 CDN 무효화 프로세스를 시작합니다.

## CDN 무효화 오류 문제 해결

모든 경우, 전체 일괄 처리가 무효화를 위해 처리되거나 전체 일괄 처리가 실패합니다.

| 오류 | 설명 |
| --- | --- |
| *선택한 자산의 URL을 검색하지 못했습니다.* | 다음 시나리오 중 하나가 충족되는 경우 발생합니다.<br> - Dynamic Media 구성을 찾을 수 없습니다.<br>- Dynamic Media 구성을 읽을 서비스 사용자를 검색하는 동안 예외가 있습니다.<br>- URL을 구성하는 데 사용되는 게시 서버 또는 회사 루트가 Dynamic Media 구성에 없습니다. |
| *일부 URL이 올바르게 정의되지 않았습니다. 수정 및 다시 제출합니다.* | IPS CDN 캐시 무효화 API가 다른 회사를 참조하는 오류를 반환하는 경우 발생합니다. 또는 IPS `cdnCacheInvalidation` API에서 수행한 유효성 검사에 따라 URL이 유효하지 않은 경우 |
| *CDN 캐시를 무효화하지 못했습니다.* | CDN 캐시 무효화 요청이 다른 이유로 실패할 경우 발생합니다. |
| *무효화할 URL을 입력하지 않았습니다.* | **[!UICONTROL CDN 무효화 - Confirm]** 페이지에 URL이 없는 경우 **[!UICONTROL Submit.]**&#x200B;을 탭합니다. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
