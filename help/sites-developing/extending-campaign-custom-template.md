---
title: Adobe Campaign 양식 구성 요소를 사용하여 사용자 지정 AEM 페이지 템플릿 만들기
description: Adobe Campaign 양식 구성 요소를 사용하는 사용자 지정 페이지 템플릿 작성
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: de5c634a-c0d7-4e69-b941-d2fbfe83117d
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 10%

---

# Adobe Campaign 양식 구성 요소를 사용하여 사용자 지정 AEM 페이지 템플릿 만들기{#creating-custom-aem-page-template-with-adobe-campaign-form-components}

이 페이지에서는 을 사용하는 사용자 정의 페이지 템플릿을 작성하는 방법을 설명합니다. [Adobe Campaign 양식](/help/sites-authoring/adobe-campaign-components.md) Geometrixx-outdoors 템플릿( `/apps/geometrixx-outdoors/components/page_campaign_profile`)가 구현되었으며, 고유한 사용자 지정 템플릿을 만들 때 필요할 수 있는 중요한 정보를 가리킵니다.

>[!NOTE]
>
>[이메일 및 양식 샘플은 Geometrixx에서만 사용할 수 있습니다.](/help/sites-developing/we-retail.md). 패키지 공유에서 샘플 Geometrixx 콘텐츠를 다운로드합니다.

Adobe Campaign Form 구성 요소를 사용하여 사용자 지정 AEM 페이지 템플릿을 만들려면 다음을 수행해야 합니다.

1. **리소스 종류 수정**

   페이지 구성 요소가에서 상속을 받는지 확인합니다. `mcm/campaign/components/profile`.

   서블릿이 정보를 가져오고 저장하는 데 필요합니다.

   * `com.day.cq.mcm.campaign.servlets.TemplateListServlet`
   * `com.day.cq.mcm.campaign.servlets.SaveProfileServlet`

   ![chlimage_1-201](assets/chlimage_1-201.png)

1. **ClientContext 설정**

   clientcontext 설정을 볼 때( `/etc/designs/geometrixx-outdoors/jcr:content/page_campaign_profile`) 다음 설정이 표시됩니다.

   * ClientContext 대상 `/etc/clientcontext/campaign`
   * 추가 요금도 있습니다 *config* 노드.

   ![chlimage_1-202](assets/chlimage_1-202.png)

1. **head.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/head.jsp)**

   위치 **head.jsp**&#x200B;를 지정하는 경우 **clientcontext-config** 및 **cloudservice-hook**:

   ```
   <cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub"/>
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
   ```

1. **body.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/body.jsp)**

   위치 **body.jsp**, 클라우드 서비스는 페이지 하단에 로드됩니다.

   ```
   <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
   ```

1. **캠페인 페이지 속성**

   Adobe Campaign 템플릿을 선택하려면 페이지 속성이 **캠페인** 탭:

   `/apps/geometrixx-outdoors/components/page_campaign_profile/dialog/items/tabs/items/campaign`

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. **템플릿 설정**.

   템플릿( `/apps/geometrixx-outdoors/templates/campaign_profile/jcr:content`) 다음 기본값이 표시됩니다.

   | **acMapping** | mapRecipient(Adobe Campaign 6.1용), 프로필(Adobe Campaign Standard용) |
   |---|---|
   | **acTemplateId** | 메일 |

   ![chlimage_1-204](assets/chlimage_1-204.png)
