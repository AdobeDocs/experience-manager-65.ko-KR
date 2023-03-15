---
title: Dynamic Media을 통해 컨텐츠 전달 네트워크 캐시 무효화
description: CDN(Content Delivery Network) 캐시 컨텐츠 무효화를 사용하면 캐시가 만료될 때까지 기다리지 않고 Dynamic Media에서 제공하는 자산을 빠르게 업데이트할 수 있습니다.
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
ht-degree: 2%

---


# Dynamic Media의 방식으로 CDN 캐시 무효화 {#invalidating-cdn-cache-for-dm-assets}

Dynamic Media 자산은 고객에게 빠르게 전달하기 위해 CDN(Content Delivery Network)에 의해 캐시됩니다. 그러나 이러한 자산을 업데이트할 때에는 해당 변경 사항이 즉시 웹 사이트에 적용되도록 해야 합니다. CDN 캐시를 지우거나 무효화하면 Dynamic Media에서 제공하는 에셋을 빠르게 업데이트할 수 있습니다. TTL(Time To Live) 값(기본값 10시간)을 사용하여 캐시가 만료될 때까지 기다리는 대신 Dynamic Media 내에서 요청을 보내 몇 분 내에 캐시가 만료되도록 할 수 있습니다.



>[!IMPORTANT]
>
>다음 단계는 Adobe Experience Manager 6.5, 서비스 팩 6(Experience Manager 6.5.6) 이상의 Dynamic Media - Scene7 모드에만 적용됩니다. 이 CDN 무효화 기능을 사용하려면 Adobe Experience Manager - Dynamic Media과 번들로 제공되는 기본 CDN을 사용해야 합니다. 다른 모든 사용자 지정 CDN은 이 기능에서 지원되지 않습니다.<br>Experience Manager 6.5, 서비스 팩 5(Experience Manager 6.5.5) 또는 이전 버전에서 Dynamic Media을 사용하는 경우 의 단계를 따릅니다 [Dynamic Media Classic을 통해 CDN 캐시 무효화](/help/assets/invalidate-cdn-cache-dm-classic.md).

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Caching overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**Dynamic Media 자산에 대한 CDN 캐시 콘텐츠를 무효화하려면 다음을 수행하십시오.**

*1부/2: CDN 무효화 템플릿 만들기*

1. 6.5.6 이상 Experience Manager에서 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]** > **[!UICONTROL CDN 무효화]**.

   ![CDN 유효성 검사 기능](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. 다음에서 **[!UICONTROL CDN 무효화 템플릿]** 페이지에서 시나리오에 따라 다음 옵션 중 하나를 수행합니다.

   | 시나리오 | 옵션 |
   | --- | --- |
   | 이전에 Dynamic Media Classic을 사용하여 CDN 무효화 템플릿을 이미 만들었습니다. | 다음 **[!UICONTROL 템플릿 만들기]** 텍스트 필드는 템플릿 데이터로 미리 채워집니다. 이러한 경우 템플릿을 편집하거나 다음 단계를 계속할 수 있습니다. |
   | 템플릿을 만들어야 합니다. 무엇을 입력해야 합니까? | 다음에서 **[!UICONTROL 템플릿 만들기]** 텍스트 필드에 이미지 사전 설정 또는 수정자를 포함한 이미지 URL을 입력합니다. `<ID>`: 다음 예제와 같이 특정 이미지 ID 대신<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>템플릿에 다음이 포함된 경우: `<ID>`: 그런 다음 Dynamic Media이 채워짐 `https://<publishserver_name>/is/image/<company_name>/<ID>` 위치 `<publishserver_name>` 는 Dynamic Media Classic의 일반 설정에 정의된 게시 서버의 이름입니다. 다음 `<company_name>` 은 이 Experience Manager 인스턴스와 연결된 회사 루트의 이름입니다. `<ID>` 는 자산 선택기를 통해 무효화하도록 선택한 자산입니다.<br>게시한 사전 설정/수정자 `<ID>` 은 URL 정의에 있는 그대로 복사됩니다.<br>이미지만 - 즉, `/is/image` - 템플릿을 기반으로 자동 형성될 수 있습니다.<br>대상 `/is/content/`, 에셋 선택기를 사용하여 비디오 또는 PDF과 같은 에셋을 추가해도 URL이 자동으로 생성되지 않습니다. 대신 이러한 자산을 CDN 무효화 템플릿에 지정하거나 의 이러한 자산에 URL을 수동으로 추가할 수 있습니다 *2부/2: CDN 무효화 옵션 설정*.<br>**예:**<br>&#x200B;이 첫 번째 예에서 무효화 템플릿은 다음을 포함합니다. `<ID>` 를 포함하는 자산 URL과 함께 `/is/content`. 예, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Dynamic Media은 을 사용하여 이 경로를 기반으로 URL을 형성합니다. `<ID>` 무효화할 에셋 선택기를 통해 선택한 에셋입니다.<br>이 두 번째 예에서 무효화 템플릿은 웹 속성에 사용되는 자산의 전체 URL을 포함합니다. `/is/content` (자산 선택기에 종속되지 않음). 예를 들어, `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` 여기서 backpack은 에셋 ID입니다.<br>Dynamic Media에서 지원되는 에셋 형식은 무효화할 수 있습니다. 다음과 같은 에셋 파일 유형 *아님* cdn 무효화에는 PostScript ®, 캡슐화된 PostScript ®, Adobe Illustrator, Adobe InDesign, Microsoft® Powerpoint, Microsoft® Excel, Microsoft® Word 및 리치 텍스트 형식 등이 지원됩니다.<br><br>· 템플릿을 만들 때 구문과 오타 내용에 주의해야 합니다. Dynamic Media에서는 템플릿 유효성 검사를 수행하지 않습니다.<br>· CDN 무효화 템플릿은 텍스트를 최대 2500자까지 저장할 수 있습니다.<br>· 이 CDN 무효화 템플릿 또는 **[!UICONTROL URL 추가]** 의 텍스트 필드 *2부: CDN 무효화 옵션 설정.*<br>· CDN 무효화 템플릿의 각 항목은 개별 행에 있어야 합니다.<br>· 다음 CDN 무효화 템플릿 예는 데모용으로만 사용할 수 있습니다. |

   ![CDN 무효화 템플릿 - 만들기](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >CDN 무효화 템플릿은 텍스트를 최대 2500자까지 저장할 수 있습니다.

1. 의 오른쪽 위 모서리에서 **[!UICONTROL CDN 무효화 템플릿]** 페이지, 선택 **[!UICONTROL 저장]**&#x200B;을 선택한 다음 을 선택합니다. **[!UICONTROL 확인]**.<br>

   *2부/2: CDN 무효화 옵션 설정*
   <br>

1. Experience Manager as a Cloud Service에서 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]** > **[!UICONTROL CDN 무효화]**.

   ![CDN 유효성 검사 기능](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. 다음에서 **[!UICONTROL CDN 무효화 - 세부 정보 추가]** 페이지에서 CDN 무효화에 대한 자산을 선택합니다.

   ![CDN 무효화 - 세부 정보 추가](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >옵션을 종료하기로 결정한 경우 **[!UICONTROL CDN에서 자산 관련 이미지 사전 설정 무효화]** *및* **[!UICONTROL 템플릿을 기반으로 무효화]** 선택하지 않으면 선택한 자산의 기본 URL이 무효화되도록 형성됩니다. 이 옵션 배열은 이미지에만 사용하십시오.


   | 옵션 | 설명 |
   | --- | --- |
   | **[!UICONTROL CDN에서 자산 관련 이미지 사전 설정 무효화]** | (선택 사항) 이 옵션을 선택하면 선택한 에셋과 모든 관련 이미지 사전 설정 URL이 캐시 무효화를 위해 자동으로 구성됩니다.<br>자산 및 자산과 연결된 사전 정의된 사전 설정 URL이 무효화를 위해 자동으로 형성됩니다. 이 옵션은 이미지 에셋에만 작동합니다. |
   | **[!UICONTROL 템플릿 기반 무효화]** | (선택 사항) URL 형성에 정의된 템플릿만 사용하려면 이 옵션을 선택합니다. |
   | **[!UICONTROL 자산 추가]** | 자산 선택기를 사용하여 무효화할 자산을 선택합니다. 게시된 에셋 또는 게시되지 않은 에셋을 선택할 수 있습니다.<br>CDN에서의 캐싱은 에셋 기반이 아닌 URL 기반입니다. 따라서 웹 사이트에 있는 전체 URL을 알고 있어야 합니다. 해당 URL을 결정한 후 템플릿에 추가할 수 있습니다. 그런 다음 해당 에셋을 선택하고 추가한 다음 한 단계에서 URL을 무효화할 수 있습니다. <br>이 옵션을 사용할 때 **[!UICONTROL CDN에서 자산 관련 이미지 사전 설정 무효화]**, 또는 **[!UICONTROL 템플릿 기반 무효화]**&#x200B;또는 둘 다. |
   | **[!UICONTROL URL 추가]** | CDN 캐시를 무효화하려는 Dynamic Media 에셋에 전체 URL 경로를 수동으로 추가하거나 붙여넣습니다. 에서 CDN 무효화 템플릿을 생성하지 않은 경우 이 옵션을 사용합니다. ***1부/2: CDN 무효화 템플릿 만들기***&#x200B;및 에는 무효화할 몇 개의 자산만 있습니다.<br>**중요 사항:** 추가하는 각 URL은 한 줄에 있어야 합니다.<br>주어진 시간에 최대 1000개의 URL을 무효화할 수 있습니다. 의 URL 수가 **[!UICONTROL URL 추가]** 텍스트 필드가 1000보다 크면 선택할 수 없습니다. **[!UICONTROL 다음]**. 이러한 경우 다음을 선택해야 합니다. **[!UICONTROL X]** 선택한 에셋의 오른쪽 또는 수동으로 추가한 URL을 사용하여 무효화 목록에서 삭제합니다.<br>CDN 무효화 템플릿 또는 다음 위치에 이미지 스마트 자르기에 대한 URL을 지정합니다 **[!UICONTROL URL 추가]** 텍스트 필드. |

1. 페이지의 오른쪽 상단 모서리 근처에서 을 선택합니다. **[!UICONTROL 다음]**.
1. 다음에서 **[!UICONTROL CDN 무효화 - 확인]** 페이지, **[!UICONTROL URL]** 목록 상자에는 이전에 만든 CDN 무효화 템플릿에서 생성된 하나 이상의 URL 목록과 방금 추가한 에셋이 표시됩니다.

   예를 들어 이전 단계에 표시된 CDN 무효화 템플릿 예제를 사용하여 라는 단일 에셋을 추가했다고 가정합니다 `spinset`. 다음으로 이동 시 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]** > **[!UICONTROL CDN 무효화]**&#x200B;를 입력하면 에 다음과 같은 5개의 URL이 생성됩니다. **[!UICONTROL CDN 무효화 - 확인]** 사용자 인터페이스:

   ![CDN 무효화 - 확인](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   필요한 경우 다음을 선택합니다 **X** 무효화 프로세스에서 삭제할 수 있도록 URL 오른쪽에 추가합니다.

1. 페이지의 오른쪽 상단 모서리 근처에서 을 선택합니다. **[!UICONTROL 제출]** cdn 무효화 프로세스를 시작합니다.

## CDN 무효화 오류 문제 해결

모든 경우에 전체 배치가 무효화되도록 처리되거나 전체 배치가 실패합니다.

| 오류 | 설명 |
| --- | --- |
| *선택한 자산에 대한 URL을 검색하지 못했습니다.* | 다음 시나리오 중 하나가 충족되면 발생합니다.<br>- Dynamic Media 구성을 찾을 수 없습니다.<br>- Dynamic Media 구성을 읽는 서비스 사용자를 검색하는 동안 예외가 발생했습니다.<br>- URL을 구성하는 데 사용되는 게시 서버 또는 회사 루트가 Dynamic Media 구성에 없습니다. |
| *일부 URL이 올바르게 정의되지 않았습니다. 수정하고 다시 제출합니다.* | IPS CDN 캐시 무효화 API가 URL이 다른 회사를 참조하는 오류를 반환하는 경우 발생합니다. 또는 IPS의 유효성 검사에 따라 URL이 유효하지 않은 경우 `cdnCacheInvalidation` API. |
| *CDN 캐시를 무효화하지 못했습니다.* | CDN 캐시 무효화 요청이 다른 이유로 실패하면 발생합니다. |
| *무효화하도록 입력한 URL이 없습니다.* | 에 URL이 없는 경우 발생합니다. **[!UICONTROL CDN 무효화 - 확인]** 페이지를 만든 다음 **[!UICONTROL 제출]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
