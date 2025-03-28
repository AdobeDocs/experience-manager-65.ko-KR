---
title: AEM 양식을 구성하여 도메인 정보 미리 가져오기
description: 깊게 중첩된 그룹으로 인해 응답 시간이 느려지거나 많은 그룹의 구성원인 경우 도메인 정보를 미리 가져오도록 AEM Forms를 구성합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: cf5283a5-dbfb-460d-a8bd-11cd15ab8640
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 0%

---

# AEM 양식을 구성하여 도메인 정보 미리 가져오기 {#configure-aem-forms-to-prefetchdomain-information}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인합니다.

사용자가 많은 그룹(예: 500개 이상)에 속하거나 그룹이 깊게 중첩된 경우(예: 30개 수준) 응답 시간이 느려질 수 있습니다. 이 문제가 발생하는 경우 특정 도메인에서 정보를 미리 가져오도록 AEM Forms를 구성할 수 있습니다.

1. 관리 콘솔에서 **[!UICONTROL 설정 > 사용자 관리 > 구성 > 구성 파일 가져오기 및 내보내기]**&#x200B;를 클릭합니다.
1. 현재 구성 설정을 파일로 내보내려면 **[!UICONTROL 내보내기]**&#x200B;를 클릭하고 구성 파일을 다른 위치에 저장하십시오.
1. 다음 노드 추가(굵게 표시됨):

   ```xml
    <node name="UM">
    <map/>
    <node name="PrincipalCache">
        <map>
            <entry key="principalCacheSize" value="1000"/>
            <entry key="principalCacheBatchFetchSize" value="10"/>
            <entry key="rebuildCacheAfterSync" value="true />
            <entry key="enableFullPrefetch" value="false"/>
            <entry key="principalCacheDomains" value="Domain_Name1/Domain_Name2/Domain_Name3"/>
        <map>
    </node>
    <node name="APSAuditService">
   ```

   이 예에서는 미리 가져오기에 대해 여러 도메인이 구성됩니다. 도메인 이름은 &quot;/&quot;로 구분됩니다. 이는 *Domain_Name1*, *Domain_Name2* 및 *Domain_Name3*&#x200B;과(와) 함께 위 예제에 나와 있습니다.

1. 업데이트된 파일을 가져오려면 사용자 관리에서 **[!UICONTROL 구성 > 구성 파일 가져오기 및 내보내기]**&#x200B;를 클릭합니다.
1. 파일을 찾으려면 **[!UICONTROL 찾아보기]**&#x200B;를 클릭하고 가져오기를 클릭한 다음 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.
