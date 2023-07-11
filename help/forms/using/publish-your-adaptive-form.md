---
title: "자습서: 적응형 양식 게시"
seo-title: "Tutorial: Publish your adaptive form"
description: 적응형 양식을 AEM 페이지로 게시하거나, AEM Sites 페이지에 양식을 임베드하거나, 외부 웹 페이지에 적응형 양식을 임베드합니다
seo-description: Publish the adaptive form as an AEM page, embed the form to an AEM Sites page, or embed the adaptive form in an external webpage
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
feature: Adaptive Forms
exl-id: c039faec-f832-43d5-8a86-22afa3bef2a4
source-git-commit: e9f64722ba7df0a7f43aaf1005161483e04142f5
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 1%

---

# 자습서: 적응형 양식 게시 {#tutorial-publish-your-adaptive-form}

![영웅 이미지](do-not-localize/13-publish-your-adaptive-form-small.png)

이 튜토리얼의 단계는 다음과 같습니다. [첫 번째 적응형 양식 만들기](https://helpx.adobe.com/kr/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) 시리즈. 전체 자습서 사용 사례를 이해하고, 수행하고, 시연하려면 연대순으로 시리즈를 따르는 것이 좋습니다.

적응형 양식이 준비되면 양식을 게시하여 최종 사용자가 사용할 수 있도록 할 수 있습니다. 최종 사용자는 모든 장치 및 인터넷 브라우저에서 게시된 양식을 열 수 있습니다. 적응형 양식이 게시되면 양식 및 관련 콘텐츠가 AEM 작성자 인스턴스에서 AEM 게시 인스턴스로 복사됩니다. 최종 사용자는 게시 인스턴스를 통해 양식을 사용할 수 있습니다.

다음 방법으로 적응형 양식을 게시할 수 있습니다.

* [적응형 양식을 AEM 페이지로 게시](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [AEM Sites 페이지에 적응형 양식 포함](#embed-the-adaptive-form-in-an-aem-sites-page)
* [적응형 양식을 외부 웹 페이지(AEM 외부에 호스트된 비 AEM 웹 페이지)에 포함](../../forms/using/publish-your-adaptive-form.md)

## 시작하기 전 {#before-you-start}

* **[AEM Forms 게시 인스턴스 설정](https://helpx.adobe.com/kr/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**: 게시 인스턴스는 AEM의 공개 인스턴스입니다 [!DNL Forms] 게시 모드에서 실행 중입니다. 프로덕션 환경에서 게시 인스턴스는 조직의 방화벽 외부에 있습니다.
* **[복제 및 역방향 복제 설정](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**: 복제는 작성자 인스턴스의 콘텐츠를 게시 인스턴스로 복사하고 게시 인스턴스의 사용자 입력(예: 양식 입력)을 작성자 인스턴스로 반환합니다.

## 적응형 양식을 AEM 페이지로 게시 {#publish-the-adaptive-form-as-an-aem-page}

적응형 양식이 AEM 페이지로 게시되면 전체 웹 페이지에는 게시된 양식만 포함됩니다. 적응형 양식의 URL을 사용하여 다른 웹 페이지에서 연결할 수 있습니다. 게시하려면 **shipping-address-add-update-form** 적응형 양식을 AEM 페이지로:

1. AEM에 로그인 [!DNL Forms] 작성자 인스턴스 및 AEM에서 shipping-address-add-update-form 적응형 양식 찾기 [!DNL Forms] UI.
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. 배송 주소 추가 업데이트 양식 적응형 양식을 선택하고 을 누릅니다 **[!UICONTROL 게시]**. 적응형 양식과 관련된 자산이 포함된 대화 상자가 표시됩니다. 누르기 **[!UICONTROL 게시]**. 적응형 양식이 게시되고 성공 대화 상자가 나타납니다.
1. 게시 인스턴스에서 양식을 엽니다. 최종 사용자가 양식을 작성하여 제출할 수 있습니다.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## AEM Sites 페이지에 적응형 양식 포함 {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms] 양식 개발자가 AEM에 적응형 양식을 매끄럽게 임베드할 수 있습니다. [!DNL Sites] 페이지를 가리키도록 업데이트하는 중입니다. 임베드된 적응형 양식은 완전히 기능할 수 있으며, 사용자는 페이지를 종료하지 않고도 양식을 작성하고 제출할 수 있습니다. 사용자가 웹 페이지의 다른 요소 컨텍스트에 남아 있으면서 양식과 동시에 상호 작용하는 데 도움이 됩니다.

AEM [!DNL Forms] 구성 요소 제공, AEM [!DNL Forms] 컨테이너, 적응형 양식을 AEM에 포함 [!DNL Sites] 페이지를 가리키도록 업데이트하는 중입니다. 기본적으로 구성 요소는 AEM에 표시되지 않습니다 [!DNL Sites] 컨테이너. AEM을 활성화하려면 다음 단계를 수행하십시오 [!DNL Forms] 컨테이너 구성 요소 및 AEM에 적응형 양식 임베드 [!DNL Sites] 페이지:

1. 편집할 We.Retail 사이트에서 페이지를 만들고 엽니다. 예를 들어, [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). 적응형 양식은 [!DNL Sites] 페이지를 가리키도록 업데이트하는 중입니다.

   기존 We.Retail에 적응형 양식을 포함할 수도 있습니다 [!DNL Site's] 페이지를 가리키도록 업데이트하는 중입니다. 예: 미국 정보 페이지 [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). 페이지를 만드는 시간이 절약됩니다. 아래 단계에서는 새로 만든 페이지를 사용합니다.

   We.Retail 사이트에는 AEM이 함께 제공됩니다. We.Retail 사이트가 설치되어 있지 않으면 다음을 참조하십시오. [We.Retail 참조 구현](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) 사이트를 설치합니다.

1. 누르기 ![속성](assets/properties.png) 페이지 정보를 참조하고 **[!UICONTROL 템플릿 편집]** 새로 만든 We.Retail 사이트 페이지의 옵션 페이지의 템플릿이 브라우저의 새 탭에서 열립니다.
1. 내부를 탭합니다. **[!UICONTROL 레이아웃 컨테이너]** 상자 및 탭 ![영양 관리](assets/feedmanagement.png). 다음에서 **[!UICONTROL 허용된 구성 요소]** 탭을 확장하고 **[!UICONTROL 일반]** 아코디언에서 **[!UICONTROL AEM 양식]** 옵션 및 탭 ![save_icon](assets/save_icon.svg). 더 AEM [!DNL Forms] 페이지에 대해 컨테이너 구성 요소를 사용할 수 있습니다.

1. AEM이 포함된 브라우저 탭을 엽니다. [!DNL Sites] 1단계에서 페이지가 열렸습니다. 탭 **[!UICONTROL 여기에 구성 요소 드래그]** 상자 및 탭 **+.** 다음에서 **[!UICONTROL 새 구성 요소 삽입]** 상자, 탭 **[!UICONTROL AEM 양식]**. 다음 **[!UICONTROL AEM Forms 컨테이너]** 구성 요소가 페이지에 추가됩니다.
1. 탭 **[!UICONTROL AEM Forms 컨테이너]** 구성 요소 및 탭 ![configure-icon](assets/configure-icon.svg). AEM 속성이 있는 대화 상자 [!DNL Forms] 컨테이너가 나타납니다. 다음에서 **[!UICONTROL 자산 경로]** 필드에서 shipping-address-add-update-form 적응형 양식을 찾아 선택합니다. 누르기 ![save_icon](assets/save_icon.svg). 적응형 양식이 페이지에 임베드됩니다.
1. 적응형 양식 및 을 모두 게시합니다 [!DNL Sites] 페이지를 가리키도록 업데이트하는 중입니다. 다음은 고려해야 할 몇 가지 사항입니다.

   * AEM을 게시하는 경우 [!DNL Sites] 페이지가 처음 게시되고 임베드된 양식이 포함되면 [!DNL Sites] 페이지와 포함된 양식.
   * 게시된 사이트 페이지에 포함된 양식만 수정하는 경우 원래 양식을 게시하고 변경 사항은 게시된 사이트 페이지에 반영됩니다. 게시된 사이트 페이지에는 양식에 대한 참조가 포함되어 있으며 페이지를 다시 게시할 필요가 없습니다.
   * 을(를) 수정하는 경우 [!DNL Sites] 페이지 및 임베드된 양식, 다시 게시 [!DNL Sites] 페이지 및 양식입니다.

     ![aem-sites에 포함](assets/embed-in-aem-sites.png)

   AEM에 추가된 배송 및 청구 주소 변경 양식 [!DNL Sites] 페이지를 가리키도록 업데이트하는 중입니다.

## 외부 웹 페이지에 적응형 양식 포함 {#embed-the-adaptive-form-in-an-external-webpage}

외부 웹 페이지에 JavaScript의 몇 줄을 삽입하여 적응형 양식을 외부 웹 페이지(AEM 외부에서 호스트되는 비 AEM 웹 페이지)에 포함할 수 있습니다. JavaScript 코드가 AEM에 HTTP 요청을 전송합니다 [!DNL Forms] 적응형 양식 및 관련 리소스에 대한 서버이고 적응형 양식을 웹 페이지에 추가합니다. 자세한 단계는 를 참조하십시오. [외부 웹 페이지에 적응형 양식 포함](/help/forms/using/embed-adaptive-form-external-web-page.md).
