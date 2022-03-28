---
title: Dynamic Media을 통해 컨텐츠 전달 네트워크 캐시를 무효화합니다.
description: CDN(Content Delivery Network) 캐시 콘텐츠를 무효화하면 캐시가 만료될 때까지 기다리는 대신 Dynamic Media에서 전달하는 자산을 빠르게 업데이트할 수 있습니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
feature: CDN Cache
exl-id: 23d3c274-0736-49f7-8d44-a56a55cfd06d
source-git-commit: b61157b0e9afa49ef72150ae0c1703a959d154be
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 1%

---


# Dynamic Media의 방식으로 CDN 캐시 무효화 {#invalidating-cdn-cache-for-dm-assets}

Dynamic Media 자산은 CDN(Content Delivery Network)에 의해 캐시되므로 고객에게 빠르게 전달할 수 있습니다. 그러나 그러한 자산을 업데이트할 때에는 이러한 변경 사항을 웹 사이트에서 즉시 적용할 수 있습니다. CDN 캐시를 지우거나 무효화하면 Dynamic Media에서 제공하는 자산을 빠르게 업데이트할 수 있습니다. TTL(Time To Live) 값(기본값 10시간)을 사용하여 캐시가 만료될 때까지 기다리는 대신 Dynamic Media 내에서 캐시가 몇 분 내에 만료되도록 요청을 보낼 수 있습니다.



>[!IMPORTANT]
>
>다음 단계는 Adobe Experience Manager 6.5, 서비스 팩 6(Experience Manager 6.5.6) 이상의 Dynamic Media - Scene7 모드에만 적용됩니다. 이 CDN 무효화 기능을 사용하려면 Adobe Experience Manager - Dynamic Media과 번들로 제공되는 기본 CDN을 사용해야 합니다. 다른 모든 사용자 지정 CDN은 이 기능에서 지원되지 않습니다.<br>Experience Manager 6.5, 서비스 팩 5(Experience Manager 6.5.5) 또는 이전 버전에서 Dynamic Media을 사용하는 경우 [Dynamic Media Classic을 통해 CDN 캐시 무효화](/help/assets/invalidate-cdn-cache-dm-classic.md).

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Caching overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**Dynamic Media 자산에 대해 CDN 캐시 컨텐츠를 무효화하려면:**

*2부 1: CDN 무효화 템플릿 만들기*

1. Experience Manager 6.5.6 이상에서 다음 위치로 이동합니다. **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL CDN 무효화]**.

   ![CDN 유효성 검사 기능](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. 설정 **[!UICONTROL CDN 무효화 템플릿]** 페이지에서 시나리오를 기준으로 다음 옵션 중 하나를 수행합니다.

   | 시나리오 | 옵션 |
   | --- | --- |
   | 이전에 Dynamic Media Classic을 사용하여 CDN 무효화 템플릿을 이미 만들었습니다. | 다음 **[!UICONTROL 템플릿 만들기]** 텍스트 필드는 템플릿 데이터로 미리 채워집니다. 이러한 경우 템플릿을 편집하거나 다음 단계를 계속 진행할 수 있습니다. |
   | 템플릿을 만들어야 합니다. 어떻게 들어가나요? | 에서 **[!UICONTROL 템플릿 만들기]** 텍스트 필드에 이미지 URL(이미지 사전 설정 또는 수정자 포함)을 참조하는 `<ID>`다음 예와 같이 특정 이미지 ID 대신<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>템플릿에 `<ID>`을 입력한 다음 Dynamic Media이 채워집니다 `https://<publishserver_name>/is/image/<company_name>/<ID>` 여기서 `<publishserver_name>` Dynamic Media Classic의 일반 설정에 정의된 게시 서버의 이름입니다. 다음 `<company_name>` 은 이 Experience Manager 인스턴스와 연결된 회사 루트 이름입니다. `<ID>` 는 무효화할 자산 선택기를 통해 선택한 자산입니다.<br>모든 사전 설정/수정자 게시물 `<ID>` 는 URL 정의에 있는 그대로 복사됩니다.<br>이미지만 - 즉, `/is/image` - 템플릿을 기준으로 자동 형식을 지정할 수 있습니다.<br>대상 `/is/content/`를 채울 때 자산 선택기를 사용하여 비디오 또는 PDF과 같은 자산을 추가해도 URL이 자동으로 생성되지 않습니다. 대신 CDN 무효화 템플릿에서 그러한 자산을 지정해야 하거나 또는 의 해당 자산에 URL을 수동으로 추가할 수 있습니다 *2부: CDN 무효화 옵션 설정*.<br>**예:**<br>&#x200B;이 첫 번째 예에서는 무효화 템플릿에 이 포함됩니다 `<ID>` 와 함께 `/is/content`. 예, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Dynamic Media이 이 경로를 기반으로 URL을 `<ID>` 무효화하려는 자산 선택기를 통해 선택한 자산<br>이 두 번째 예에서는 무효화 템플릿에 `/is/content` (자산 선택기에 종속되지 않음). 예, `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` 여기서 backpack은 자산 ID입니다.<br>Dynamic Media에서 지원되는 자산 형식은 무효화할 수 있습니다. 자산 파일 형식 *not* CDN 무효화에 대해 지원되는 형식은 PostScript®, Encapsulated PostScript®, Adobe Illustrator, Adobe InDesign, Microsoft® Powerpoint, Microsoft® Excel, Microsoft® Word 및 리치 텍스트 형식입니다.<br><br>・ 템플릿을 만들 때, 구문 및 오말에 주의하십시오. Dynamic Media에서는 템플릿 유효성 검사를 수행하지 않습니다.<br>・ CDN 무효화 템플릿은 최대 2500자의 텍스트를 저장할 수 있습니다.<br>・ 이 CDN 무효화 템플릿 또는 **[!UICONTROL URL 추가]** 텍스트 필드 *2부: CDN 무효화 옵션을 설정합니다.*<br>・ CDN 무효화 템플릿의 각 항목은 해당 행에 있어야 합니다.<br>・ 다음 CDN 무효화 템플릿 예제는 데모용입니다. |

   ![CDN 무효화 템플릿 - 만들기](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >CDN 무효화 템플릿은 최대 2500자의 텍스트를 저장할 수 있습니다.

1. 의 오른쪽 위 모서리에서 **[!UICONTROL CDN 무효화 템플릿]** 페이지를 선택하고 **[!UICONTROL 저장]**&#x200B;를 선택하고 을 선택합니다. **[!UICONTROL 확인]**.<br>

   *2부: CDN 무효화 옵션 설정*
   <br>

1. Experience Manager as a Cloud Service에서 **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL CDN 무효화]**.

   ![CDN 유효성 검사 기능](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. 설정 **[!UICONTROL CDN 무효화 - 세부 정보 추가]** 페이지에서 CDN 무효화에 대한 자산을 선택합니다.

   ![CDN 무효화 - 세부 정보 추가](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >옵션을 그대로 두기로 결정한 경우 **[!UICONTROL CDN에서 자산 관련 이미지 사전 설정 무효화]** *및* **[!UICONTROL 템플릿을 기준으로 무효화]** 이 옵션을 선택하지 않으면 선택한 자산의 기본 URL이 무효화되도록 만들어집니다. 이미지에만 이 옵션 배열을 사용합니다.


   | 옵션 | 설명 |
   | --- | --- |
   | **[!UICONTROL CDN에서 자산 관련 이미지 사전 설정 무효화]** | (선택 사항) 이 옵션을 선택하면 선택한 자산과 연결된 모든 이미지 사전 설정 URL이 캐시 무효화에 대해 자동 구성됩니다.<br>자산 및 관련 사전 정의된 사전 설정 URL은 무효화를 위해 자동으로 구성됩니다. 이 옵션은 이미지 자산에만 작동합니다. |
   | **[!UICONTROL 템플릿 기반 무효화]** | (선택 사항) URL 구성에 정의된 템플릿만 사용하려면 이 옵션을 선택합니다. |
   | **[!UICONTROL 자산 추가]** | 무효화할 자산을 선택하려면 자산 선택기를 사용합니다. 게시된 자산 또는 게시 취소된 자산을 선택할 수 있습니다.<br>CDN에서 캐싱은 자산 기반이 아닌 URL 기반입니다. 따라서 웹 사이트에 있는 전체 URL을 알고 있어야 합니다. 그러한 URL을 결정한 후 템플릿에 추가할 수 있습니다. 그런 다음 해당 자산을 선택하고 추가하고 한 단계에서 URL을 무효화할 수 있습니다. <br>다음 작업에 이 옵션 사용 **[!UICONTROL CDN에서 자산 관련 이미지 사전 설정 무효화]**, 또는 **[!UICONTROL 템플릿 기반 무효화]**&#x200B;또는 둘 다 사용할 수 있습니다. |
   | **[!UICONTROL URL 추가]** | 무효화하려는 CDN 캐시가 있는 Dynamic Media 자산에 전체 URL 경로를 수동으로 추가 또는 붙여 넣습니다. 에서 CDN 무효화 템플릿을 만들지 않은 경우 이 옵션을 사용합니다 ***2부 1: CDN 무효화 템플릿 만들기***&#x200B;무효화할 자산이 몇 개만 있습니다.<br>**중요 사항:** 추가하는 각 URL은 고유한 행에 있어야 합니다.<br>한 번에 최대 1000개의 URL을 무효화할 수 있습니다. 에 있는 URL 수가 **[!UICONTROL URL 추가]** 텍스트 필드가 1000보다 크므로 선택할 수 없습니다 **[!UICONTROL 다음]**. 이러한 경우 다음을 선택해야 합니다 **[!UICONTROL X]** 를 클릭하거나 수동으로 추가한 URL을 사용하여 무효화 목록에서 해당 자산을 삭제합니다.<br>CDN 무효화 템플릿 또는 이 템플릿의 이미지 스마트 자르기에 대한 URL을 지정합니다 **[!UICONTROL URL 추가]** 텍스트 필드. |

1. 페이지의 오른쪽 위 모서리 근처에 있는 를 선택합니다. **[!UICONTROL 다음]**.
1. 설정 **[!UICONTROL CDN 무효화 - 확인]** 페이지, **[!UICONTROL URL]** 목록 상자에서는 이전에 만든 CDN 무효화 템플릿과 방금 추가한 자산에서 생성된 하나 이상의 URL 목록을 볼 수 있습니다.

   예를 들어, 이전 단계에서 표시된 CDN 무효화 템플릿 예제를 사용하여 이름이 인 단일 자산을 추가했다고 가정합니다. `spinset`. 로 이동하는 경우 **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL CDN 무효화]**&#x200B;를 입력하면 다음 5개의 생성 URL이 **[!UICONTROL CDN 무효화 - 확인]** 사용자 인터페이스:

   ![CDN 무효화 - 확인](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   필요한 경우 을 선택합니다. **X** 를 눌러 무효화 프로세스에서 삭제합니다.

1. 페이지의 오른쪽 위 모서리 근처에 있는 를 선택합니다. **[!UICONTROL 제출]** cdn 무효화 프로세스를 시작합니다.

## CDN 무효화 오류 문제 해결

모든 경우, 전체 일괄 처리가 무효화를 위해 처리되거나 전체 일괄 처리가 실패합니다.

| 오류 | 설명 |
| --- | --- |
| *선택한 자산의 URL을 검색하지 못했습니다.* | 다음 시나리오가 충족되는 경우 발생합니다.<br>- Dynamic Media 구성을 찾을 수 없습니다.<br>- Dynamic Media 구성을 읽을 서비스 사용자를 검색하는 동안 예외가 있습니다.<br>- URL을 구성하는 데 사용되는 게시 서버 또는 회사 루트가 Dynamic Media 구성에 없습니다. |
| *일부 URL이 올바르게 정의되지 않았습니다. 수정하고 다시 제출합니다.* | IPS CDN 캐시 무효화 API가 다른 회사를 참조하는 오류를 반환하는 경우 발생합니다. 또는 IP에서 수행한 유효성 검사에 따라 URL이 유효하지 않은 경우 `cdnCacheInvalidation` API. |
| *CDN 캐시를 무효화하지 못했습니다.* | CDN 캐시 무효화 요청이 다른 이유로 실패할 경우 발생합니다. |
| *무효화할 URL을 입력하지 않았습니다.* | 에 URL이 없는 경우 발생합니다 **[!UICONTROL CDN 무효화 - 확인]** 페이지를 선택하고 **[!UICONTROL 제출]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
