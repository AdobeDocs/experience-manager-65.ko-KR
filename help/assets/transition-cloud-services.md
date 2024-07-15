---
title: 폴더에 번역 클라우드 서비스 적용
description: Adobe Experience Manager의 폴더에 번역 클라우드 서비스를 적용합니다.
role: Admin
feature: Translation
exl-id: f17a33d7-eb2f-406b-8d6c-a3bf564c8702
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 45%

---

# 폴더에 번역 클라우드 서비스 적용 {#applying-translation-cloud-services-to-folders}

[!DNL Adobe Experience Manager]을(를) 사용하면 원하는 번역 공급업체에서 클라우드 기반 번역 서비스를 이용하여 에셋이 요구 사항에 따라 번역되도록 할 수 있습니다.

번역 클라우드 서비스를 에셋 폴더에 직접 적용하여 번역 워크플로 중에 활용할 수 있습니다.

## 번역 서비스 적용 {#applying-the-translation-services}

번역 클라우드 서비스를 자산 폴더에 직접 적용하면 번역 워크플로를 만들거나 업데이트할 때 번역 서비스를 구성할 필요가 없습니다.

1. [!DNL Assets] 사용자 인터페이스에서 번역 서비스를 적용할 폴더를 선택합니다.
1. 도구 모음에서 **[!UICONTROL 속성]**&#x200B;을 클릭하여 **[!UICONTROL 폴더 속성]** 페이지를 표시합니다.

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. Navigate to the **[!UICONTROL Cloud Services]** tab.
1. Cloud Service 구성 목록에서 원하는 번역 공급업체를 선택합니다. 예를 들어 Microsoft에서 번역 서비스를 이용하려면 **[!UICONTROL Microsoft 번역기]**&#x200B;를 선택하세요.

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. 번역 공급업체에 대한 커넥터를 선택합니다.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. 도구 모음에서 **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 **[!UICONTROL 확인]**&#x200B;을 클릭하여 대화 상자를 닫습니다.번역 서비스가 폴더에 적용됩니다.

## 사용자 지정 번역 커넥터 적용  {#applying-custom-translation-connector}

If you want to apply a custom connector for the translation services you want to use in translation workflows. To apply a custom connector, first install the connector from Package Manager. Then, configure the connector from the Cloud Services console. After you configure the connector, it is available in the list of connectors in the Cloud Services tab described in [Applying the translation services](transition-cloud-services.md#applying-the-translation-services). After you apply the custom connector and run translation workflows, the **[!UICONTROL Translation Summary]** tile of the translation project displays the connector details under the heads **[!UICONTROL Provider]** and **[!UICONTROL Method]**.

1. 패키지 관리자에서 커넥터를 설치합니다.
1. [!DNL Experience Manager] 로고를 클릭하고 **[!UICONTROL 도구]** > **[!UICONTROL 배포]** > **[!UICONTROL Cloud Service]**(으)로 이동합니다.
1. Locate the connector you installed under **[!UICONTROL Third Party Services]** in the **[!UICONTROL Cloud Services]** page.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. **[!UICONTROL 지금 구성]** 링크를 클릭하여 **[!UICONTROL 구성 만들기]** 대화 상자를 엽니다.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. 커넥터의 제목과 이름을 지정한 다음 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. The custom connector is available in the list of connectors in the **[!UICONTROL Cloud Services]** tab described in step 5 of [Applying the translation services](#applying-the-translation-services).
1. Run any translation workflow described in [Creating Translation Projects](translation-projects.md) after you apply the custom connector. Verify the details of the connector in the **[!UICONTROL Translation Summary]** tile of the translation project in the **[!UICONTROL Projects]** console.

   ![chlimage_1-220](assets/chlimage_1-220.png)
