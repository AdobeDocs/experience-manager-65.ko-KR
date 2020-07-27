---
title: 도메인 정보를 프리페치하도록 AEM 양식 구성
seo-title: 도메인 정보를 프리페치하도록 AEM 양식 구성
description: 깊이 중첩된 그룹으로 인해 응답 시간이 느리거나 여러 그룹의 구성원인 경우 도메인 정보를 프리페치하도록 AEM 양식을 구성합니다.
seo-description: 깊이 중첩된 그룹으로 인해 응답 시간이 느리거나 여러 그룹의 구성원인 경우 도메인 정보를 프리페치하도록 AEM 양식을 구성합니다.
uuid: 53c8995e-3f9d-42e8-9f75-cee7debe6ce1
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f9a3f897-90c6-4942-8a86-aae510298f2a
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# 도메인 정보를 프리페치하도록 AEM 양식 구성 {#configure-aem-forms-to-prefetchdomain-information}

사용자가 많은 그룹(예: 500개 이상)에 속하거나 그룹이 깊이 중첩된 경우(예: 30개 수준) 응답 시간이 느려질 수 있습니다. 이 문제가 발생하는 경우 특정 도메인에서 정보를 프리페치하도록 AEM 양식을 구성할 수 있습니다.

1. 관리 콘솔에서 **[!UICONTROL 설정 > 사용자 관리 > 구성 > 구성 파일 가져오기 및 내보내기를 클릭합니다]**.
1. 현재 구성 설정을 파일로 내보내려면 내보내기를 **[!UICONTROL 클릭하고]** 구성 파일을 다른 위치에 저장합니다.
1. 다음 노드를 추가합니다(굵게 표시됨).

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

   이 예에서는 프리페치용으로 여러 도메인이 구성됩니다. 도메인 이름은 &quot;/&quot;로 구분됩니다. 위 예제에서 *Domain_Name1*, *Domain_Name2*&#x200B;및 *Domain_Name3을*&#x200B;사용할 수 있습니다.

1. 업데이트된 파일을 가져오려면 사용자 관리에서 구성 > 구성 파일 **[!UICONTROL 가져오기 및 내보내기를 클릭합니다]**.
1. 찾아보기를 **[!UICONTROL 클릭하여]** 파일을 찾은 다음 가져오기를 클릭한 다음 **[!UICONTROL 확인을 클릭합니다]**.

