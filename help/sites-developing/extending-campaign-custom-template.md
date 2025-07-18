---
title: Adobe Campaign 양식 구성 요소를 사용하여 사용자 지정 AEM 페이지 템플릿 만들기
description: Adobe Campaign 양식 구성 요소를 사용하는 사용자 지정 페이지 템플릿 작성
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: de5c634a-c0d7-4e69-b941-d2fbfe83117d
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
index: false
source-git-commit: 389d5fa8de320a7237fc8290992a33743b15db99
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 2%

---


# Adobe Campaign 양식 구성 요소를 사용하여 사용자 지정 AEM 페이지 템플릿 만들기{#creating-custom-aem-page-template-with-adobe-campaign-form-components}

이 페이지에서는 Geometrixx-outdoors 템플릿([)이 구현되는 방식을 검사하여 ](/help/sites-authoring/adobe-campaign-components.md)Adobe Campaign 양식`/apps/geometrixx-outdoors/components/page_campaign_profile` 구성 요소를 사용하는 사용자 지정 페이지 템플릿을 만드는 방법에 대해 설명하고 사용자 지정 템플릿을 만들 때 필요한 중요한 정보를 안내합니다.

>[!CAUTION]
>
>AEM 이메일 구성 요소는 더 이상 사용되지 않습니다. 콘텐츠와 스타일을 병합하는 이메일의 특성상 AEM에서 기본적으로 제공하는 이메일 구성 요소는 프로젝트에 필요한 모든 구성 요소로 사용자 지정 스타일을 구현해야 하므로 고객이 제한적으로 재사용할 수 있습니다.
>
>이메일 구성 요소는 프로젝트 수준에서 구현할 수 있으며, 더 이상 사용되지 않는 AEM 이메일 구성 요소는 이를 구현하는 방법을 보여 줍니다. 그러나 프로젝트에서 이러한 사용되지 않는 구성 요소는 사용하지 마십시오.


Adobe Campaign Form 구성 요소를 사용하여 사용자 지정 AEM 페이지 템플릿을 만들려면 다음 사항이 있는지 확인하십시오.

1. **올바른 resourceSuperType**

   페이지 구성 요소가 `mcm/campaign/components/profile`에서 상속되는지 확인하십시오.

   서블릿이 정보를 가져오고 저장하는 데 필요합니다.

   * `com.day.cq.mcm.campaign.servlets.TemplateListServlet`
   * `com.day.cq.mcm.campaign.servlets.SaveProfileServlet`

   ![chlimage_1-201](assets/chlimage_1-201.png)

1. **ClientContext 설정**

   Clientcontext 설정(`/etc/designs/geometrixx-outdoors/jcr:content/page_campaign_profile`)을 보면 다음 설정이 표시됩니다.

   * ClientContext이 `/etc/clientcontext/campaign`을(를) 가리킵니다.
   * 추가 *config* 노드도 있습니다.

   ![chlimage_1-202](assets/chlimage_1-202.png)

1. **head.jsp(/apps/geometrixx-outdoors/components/page_campaign_profile/head.jsp)**

   **head.jsp**&#x200B;에서 **clientcontext-config** 및 **cloudservice-hook**&#x200B;을(를) 사용하는 다음 줄이 표시됩니다.

   ```
   <cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub"/>
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
   ```

1. **body.jsp(/apps/geometrixx-outdoors/components/page_campaign_profile/body.jsp)**

   **body.jsp**&#x200B;에서 클라우드 서비스가 페이지 하단에 로드됩니다.

   ```
   <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
   ```

1. **캠페인 페이지 속성**

   Adobe Campaign 템플릿을 선택하려면 **Campaign** 탭으로 페이지 속성이 확장됩니다.

   `/apps/geometrixx-outdoors/components/page_campaign_profile/dialog/items/tabs/items/campaign`

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. **템플릿 설정**.

   템플릿( `/apps/geometrixx-outdoors/templates/campaign_profile/jcr:content`)에 다음 기본값이 표시됩니다.

   | **acMapping** | mapRecipient(Adobe Campaign 6.1용), 프로필(Adobe Campaign Standard용) |
   |---|---|
   | **acTemplateId** | 메일 |

   ![chlimage_1-204](assets/chlimage_1-204.png)
