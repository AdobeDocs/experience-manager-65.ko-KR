---
title: Adobe Campaign 양식 구성 요소를 사용하여 사용자 지정 AEM 페이지 템플릿 만들기
seo-title: Adobe Campaign 양식 구성 요소를 사용하여 사용자 지정 AEM 페이지 템플릿 만들기
description: Adobe Campaign 양식 구성 요소를 사용하는 사용자 정의 페이지 템플릿 만들기
seo-description: Adobe Campaign 양식 구성 요소를 사용하는 사용자 정의 페이지 템플릿 만들기
uuid: 8162ace2-b661-4c39-b0fb-288e1c035b9c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c3f6eed4-bbda-454a-88ce-c7f2041d4217
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 16%

---


# Adobe Campaign 양식 구성 요소를 사용하여 사용자 지정 AEM 페이지 템플릿 만들기{#creating-custom-aem-page-template-with-adobe-campaign-form-components}

이 페이지에서는 Geometrixx-outdoors 템플릿( `/apps/geometrixx-outdoors/components/page_campaign_profile`)의 구현 방법을 검사하여 [Adobe Campaign Form](/help/sites-authoring/adobe-campaign-components.md) 구성 요소를 사용하는 사용자 지정 페이지 템플릿을 작성하는 방법을 설명하고 사용자 지정 템플릿을 만들 때 필요한 중요한 정보를 알려줍니다.

>[!NOTE]
>
>[이메일 및 양식 샘플은 Geometrixx에서만 사용할 수 있습니다](/help/sites-developing/we-retail.md). 패키지 공유에서 샘플 Geometrixx 컨텐츠를 다운로드하십시오.

Adobe Campaign 양식 구성 요소를 사용하여 사용자 정의 AEM 페이지 템플릿을 만들려면 다음을 수행하십시오.

1. **올바른 resourceSuperType**

   페이지 구성 요소가 `mcm/campaign/components/profile`에서 상속되는지 확인하십시오.

   서버가 정보를 가져오고 저장하는 데 필요합니다.

   * `com.day.cq.mcm.campaign.servlets.TemplateListServlet`
   * `com.day.cq.mcm.campaign.servlets.SaveProfileServlet`

   ![chlimage_1-201](assets/chlimage_1-201.png)

1. **ClientContext 설정**

   clientcontext 설정( `/etc/designs/geometrixx-outdoors/jcr:content/page_campaign_profile`)을 보면 다음 설정이 표시됩니다.

   * ClientContext이 `/etc/clientcontext/campaign`을(를) 가리킵니다.
   * 추가 *config* 노드가 있습니다.

   ![chlimage_1-202](assets/chlimage_1-202.png)

1. **head.jsp(/apps/geometrixx-outdoors/components/page_campaign_profile/head.jsp)**

   **head.jsp**&#x200B;에 **clientcontext-config** 및 **cloudservice-hook**&#x200B;를 사용하는 라인이 표시됩니다.

   ```
   <cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub"/>
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
   ```

1. **body.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/body.jsp)**

   **body.jsp**&#x200B;에서 클라우드 서비스는 페이지 하단에 로드됩니다.

   ```
   <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
   ```

1. **캠페인 페이지 속성**

   Adobe Campaign 템플릿을 선택하려면 페이지 속성이 **캠페인** 탭으로 확장됩니다.

   `/apps/geometrixx-outdoors/components/page_campaign_profile/dialog/items/tabs/items/campaign`

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. **템플릿 설정**.

   템플릿( `/apps/geometrixx-outdoors/templates/campaign_profile/jcr:content`)에 다음 기본값이 표시됩니다.

   | **acMapping** | mapRecipient(Adobe Campaign 6.1용), 프로필(Adobe Campaign Standard용) |
   |---|---|
   | **acTemplateId** | 메일 |

   ![chlimage_1-204](assets/chlimage_1-204.png)

