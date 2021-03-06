---
title: '"자습서:적응형 양식 게시"'
seo-title: '"자습서:적응형 양식 게시"'
description: 적응형 양식을 AEM 페이지로 게시하거나, 양식을 AEM Sites 페이지에 포함하거나, 외부 웹 페이지에 적응형 양식을 포함합니다
seo-description: 적응형 양식을 AEM 페이지로 게시하거나, 양식을 AEM Sites 페이지에 포함하거나, 외부 웹 페이지에 적응형 양식을 포함합니다
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
feature: 적응형 양식
exl-id: c039faec-f832-43d5-8a86-22afa3bef2a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 1%

---

# 자습서:적응형 양식 {#tutorial-publish-your-adaptive-form} 게시

![](do-not-localize/13-publish-your-adaptive-form-small.png)

이 자습서는 [첫 번째 적응형 양식 만들기](https://helpx.adobe.com/kr/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) 시리즈의 단계입니다. 전체 자습서 사용 사례를 이해하고, 수행하고, 시연하기 위해 시리즈를 시간 순서대로 따르는 것이 좋습니다.

적응형 양식이 준비되면 양식을 게시하여 최종 사용자가 사용할 수 있도록 할 수 있습니다. 최종 사용자는 모든 장치 및 인터넷 브라우저에서 게시된 양식을 열 수 있습니다. 적응형 양식이 게시되면 양식 및 관련 컨텐츠가 AEM 작성자 인스턴스에서 AEM 게시 인스턴스로 복사됩니다. 최종 사용자가 게시 인스턴스를 통해 양식을 사용할 수 있습니다.

적응형 양식을 게시할 수 있는 방법은 다음과 같습니다.

* [적응형 양식을 AEM 페이지로 게시](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [AEM Sites 페이지에 적응형 양식 포함](#embed-the-adaptive-form-in-an-aem-sites-page)
* [외부 웹 페이지에 적응형 양식 포함(AEM 외부에서 호스팅된 AEM이 아닌 웹 페이지)](../../forms/using/publish-your-adaptive-form.md)

## {#before-you-start} 시작 전에

* **[AEM Forms 게시 인스턴스 설정](https://helpx.adobe.com/kr/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**:게시 인스턴스는 게시 모드에서 실행 중인 AEM [!DNL Forms] 의 공개 인스턴스입니다. 프로덕션 환경에서 게시 인스턴스는 조직의 방화벽 외부에 있습니다.
* **[복제 및 역방향 복제 설정](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**:복제는 작성자 인스턴스의 컨텐츠를 게시 인스턴스에 복사하고 게시 인스턴스의 사용자 입력(예: 양식 입력)을 작성자 인스턴스에 반환합니다.

## 적응형 양식을 AEM 페이지로 게시 {#publish-the-adaptive-form-as-an-aem-page}

적응형 양식이 AEM 페이지로 게시되면 전체 웹 페이지에 게시된 양식만 포함됩니다. 적응형 양식의 URL을 사용하여 다른 웹 페이지에서 연결할 수 있습니다. **shipping-address-add-update-form** 적응형 양식을 AEM 페이지로 게시하려면 다음을 수행하십시오.

1. AEM [!DNL Forms] 작성자 인스턴스에 로그인하고 AEM [!DNL Forms] UI에서 shipping-address-add-update-form 적응형 양식을 찾습니다.
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. shipping-address-add-update-form 적응형 양식을 선택하고 **[!UICONTROL 게시]**&#x200B;를 누릅니다. 적응형 양식과 관련된 자산이 포함된 대화 상자가 표시됩니다. **[!UICONTROL 게시]**&#x200B;를 누릅니다. 적응형 양식이 게시되고 성공 대화 상자가 나타납니다.
1. 게시 인스턴스에서 양식을 엽니다. 최종 사용자가 양식을 작성하여 제출할 수 있습니다.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## AEM Sites 페이지에 적응형 양식 포함 {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms]을 사용하면 양식 개발자가 AEM [!DNL Sites] 페이지에 적응형 양식을 원활하게 포함할 수 있습니다. 포함된 적응형 양식은 완전히 기능하며 사용자는 페이지를 종료하지 않고 양식을 작성하고 제출할 수 있습니다. 따라서 사용자는 웹 페이지에서 다른 요소의 컨텍스트에 남아 있고 동시에 양식과 상호 작용할 수 있습니다.

AEM [!DNL Forms]은 AEM [!DNL Sites] 페이지에 적응형 양식을 포함할 구성 요소인 AEM [!DNL Forms] 컨테이너를 제공합니다. 기본적으로 구성 요소는 AEM [!DNL Sites] 컨테이너에 표시되지 않습니다. 다음 단계를 수행하여 AEM [!DNL Forms] 컨테이너 구성 요소를 활성화하고 AEM [!DNL Sites] 페이지에 적응형 양식을 포함합니다.

1. 편집할 We.Retail 사이트에서 페이지를 만들고 엽니다. 예: [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html) 적응형 양식이 [!DNL Sites] 페이지에 포함됩니다.

   기존 We.Retail [!DNL Site's] 페이지에 적응형 양식을 포함할 수도 있습니다. 예를 들어, ABOUT US 페이지 [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). 페이지를 만들 시간을 절약할 수 있습니다. 아래 단계에서는 새로 만든 페이지를 사용합니다.

   We.Retail 사이트는 AEM과 함께 제공됩니다. We.Retail 사이트가 설치되어 있지 않은 경우 를 참조하십시오.[](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html)

1. ![속성](assets/properties.png) 페이지 정보를 탭하고 새로 만든 We.Retail 사이트 페이지에서 **[!UICONTROL 템플릿 편집]** 옵션을 선택합니다. 페이지의 템플릿이 브라우저의 새 탭에 열립니다.
1. **[!UICONTROL 레이아웃 컨테이너]** 상자 내부를 탭하고 ![피드백 관리](assets/feedmanagement.png)를 탭합니다. **[!UICONTROL 허용된 구성 요소]** 탭에서 **[!UICONTROL 일반]** 아코디언을 확장하고 **[!UICONTROL AEM 양식]** 옵션을 선택한 다음 ![save_icon](assets/save_icon.svg)을 탭합니다. 페이지에 대해 AEM [!DNL Forms] 컨테이너 구성 요소가 활성화되어 있습니다.

1. 1단계에서 열린 AEM [!DNL Sites] 페이지가 포함된 브라우저 탭을 엽니다. **[!UICONTROL 구성 요소를 여기로 드래그하십시오.]** 상자를 탭하고 **+를 탭합니다.** 새  **[!UICONTROL 구성 요소 삽입]** 상자에서  **[!UICONTROL AEM 양식]**&#x200B;을 탭합니다. **[!UICONTROL AEM Forms 컨테이너]** 구성 요소가 페이지에 추가됩니다.
1. **[!UICONTROL AEM Forms 컨테이너]** 구성 요소를 탭하고 ![configure-icon](assets/configure-icon.svg)을 탭합니다. AEM [!DNL Forms] 컨테이너 속성이 있는 대화 상자가 나타납니다. **[!UICONTROL 자산 경로]** 필드에서 shipping-address-add-update-form 적응형 양식을 찾아 선택합니다. ![save_icon](assets/save_icon.svg)을 누릅니다. 적응형 양식이 페이지에 포함됩니다.
1. 적응형 양식과 [!DNL Sites] 페이지를 모두 게시합니다. 고려해야 할 몇 가지 사항은 다음과 같습니다.

   * AEM [!DNL Sites] 페이지를 처음 게시하고 포함된 양식이 포함된 경우 [!DNL Sites] 페이지와 포함된 양식을 게시합니다.
   * 게시된 사이트 페이지에 포함된 양식만 수정하는 경우 원래 양식을 게시하고 변경 사항이 게시된 사이트 페이지에 반영됩니다. 게시된 사이트 페이지에는 양식에 대한 참조가 포함되어 있으므로 페이지를 다시 게시할 필요가 없습니다.
   * [!DNL Sites] 페이지와 포함된 양식을 수정하는 경우 [!DNL Sites] 페이지와 양식을 다시 게시합니다.

      ![embed-in-aem-sites](assets/embed-in-aem-sites.png)
   배송 및 청구 주소 변경 양식이 AEM [!DNL Sites] 페이지에 추가되었습니다.

## 외부 웹 페이지에 적응형 양식 포함 {#embed-the-adaptive-form-in-an-external-webpage}

외부 웹 페이지에 JavaScript 몇 줄을 삽입하여 외부 웹 페이지(AEM 외부에 호스트된 비 AEM 웹 페이지)에 적응형 양식을 포함할 수 있습니다. JavaScript 코드는 적응형 양식 및 관련 리소스에 대해 AEM [!DNL Forms] 서버에 HTTP 요청을 보내고 적응형 양식을 웹 페이지에 추가합니다. 자세한 단계는 [적응형 양식을 외부 웹 페이지에 포함](/help/forms/using/embed-adaptive-form-external-web-page.md)을 참조하십시오.
