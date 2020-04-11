---
title: '"자습서:적응형 양식 게시"'
seo-title: '"자습서:적응형 양식 게시"'
description: 적응형 양식을 AEM 페이지로 게시하거나, 양식을 AEM 사이트 페이지에 포함시키거나, 외부 웹 페이지에 적응형 양식을 포함시킵니다.
seo-description: 적응형 양식을 AEM 페이지로 게시하거나, 양식을 AEM 사이트 페이지에 포함시키거나, 외부 웹 페이지에 적응형 양식을 포함시킵니다.
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 자습서:적응형 양식 게시 {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

이 자습서는 첫 번째 적응형 [양식 만들기 시리즈의](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) 단계입니다. 전체 자습서 사용 사례를 이해하고, 실행하고, 시연하기 위해 시리즈를 시간 순서대로 따르는 것이 좋습니다.

적응형 양식이 준비되면 양식을 게시하여 최종 사용자가 사용할 수 있도록 할 수 있습니다. 최종 사용자는 게시된 양식을 모든 장치 및 인터넷 브라우저에서 열 수 있습니다. 적응형 양식이 게시되면 양식과 관련 컨텐츠가 AEM 작성자 인스턴스에서 AEM 게시 인스턴스로 복사됩니다. 이 양식은 게시 인스턴스를 통해 최종 사용자가 사용할 수 있게 됩니다.

적응형 양식을 게시하는 방법은 다음과 같습니다.

* [적응형 양식을 AEM 페이지로 게시](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [AEM Sites 페이지에 적응형 양식 포함](#embed-the-adaptive-form-in-an-aem-sites-page)
* [외부 웹 페이지에 적응형 양식 포함(AEM 외부에서 호스팅된 비AEM 웹 페이지)](../../forms/using/publish-your-adaptive-form.md)

## Before you start {#before-you-start}

* **[AEM Forms 게시 인스턴스를](https://helpx.adobe.com/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**설정합니다.게시 인스턴스는 게시 모드에서 실행 중인 AEM Forms의 공개 인스턴스입니다. 제작 환경에서는 게시 인스턴스가 조직의 방화벽 외부에 있습니다.
* **[복제 및 역방향 복제](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**설정:복제는 작성 인스턴스의 컨텐츠를 게시 인스턴스로 복사하고 게시 인스턴스의 사용자 입력(예: 양식 입력)을 작성자 인스턴스로 반환합니다.

## 적응형 양식을 AEM 페이지로 게시 {#publish-the-adaptive-form-as-an-aem-page}

응용 양식이 AEM 페이지로 게시되면 전체 웹 페이지에 게시된 양식만 포함됩니다. 응용 양식의 URL을 사용하여 다른 웹 페이지에서 연결할 수 있습니다. AEM 페이지로 **shipping-address-add-update-form** 적응형 양식을 게시하려면:

1. AEM Forms 작성자 인스턴스에 로그인하고 AEM Forms UI에서 shipping-address-add-update-form 적응형 양식을 찾습니다.
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. shipping-address-add-update-form 적응형 양식을 선택하고 게시를 **누릅니다**. 적응형 양식과 관련된 에셋이 포함된 대화 상자가 표시됩니다. 게시를 **누릅니다**. 적응형 양식이 게시되고 성공 대화 상자가 나타납니다.
1. 게시 인스턴스에서 양식을 엽니다. 이 양식은 최종 사용자가 입력하고 제출할 수 있습니다.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## AEM Sites 페이지에 적응형 양식 포함 {#embed-the-adaptive-form-in-an-aem-sites-page}

양식 개발자는 AEM Forms를 사용하여 적응형 양식을 AEM Sites 페이지에 매끄럽게 포함할 수 있습니다. 포함된 응용 양식이 완전히 작동하므로 사용자는 페이지를 종료하지 않고도 양식을 채우고 제출할 수 있습니다. 이 기능은 사용자가 웹 페이지에서 다른 요소의 컨텍스트에 남아 있고 양식과 동시에 상호 작용할 수 있도록 도와줍니다.

AEM Forms는 AEM Sites 페이지에 적응형 양식을 포함할 구성 요소인 AEM Forms 컨테이너를 제공합니다. 기본적으로 구성 요소는 AEM Sites 컨테이너에 표시되지 않습니다. AEM Forms 컨테이너 구성 요소를 활성화하고 AEM Sites 페이지에 적응형 양식을 포함하려면 다음 단계를 수행하십시오.

1. 편집할 페이지를 We.Retail 사이트에서 만들고 엽니다. 예: https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html [를 참조하십시오](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). 적응형 양식이 사이트 페이지에 포함됩니다.

   기존 We.Retail 사이트의 페이지에 적응형 양식을 포함할 수도 있습니다. 예를 들어, 미국 정보 페이지 https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html [을 참조하십시오](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). 페이지를 만드는 데 소요되는 시간을 절약할 수 있습니다. 아래 단계에서는 새로 만든 페이지를 사용합니다.

   We.Retail 사이트는 AEM과 함께 제공됩니다. We.Retail 사이트가 설치되어 있지 않은 경우 We.Retail [Reference Implementation을](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) 참조하십시오.

1. 속성 ![페이지 정보를 누르고 새로 만든 We.Retail](assets/properties.png) 사이트 페이지에서 **** 템플릿 편집 옵션을 선택합니다. 페이지의 템플릿이 브라우저의 새 탭에서 열립니다.
1. 레이아웃 **컨테이너** 상자 내부를 누르고 ![피드백 관리를](assets/feedmanagement.png)누릅니다. 허용된 구성 **요소** 탭에서 일반 **아코디언을** 확장하고 **AEM 양식** 옵션을 선택한 ![](assets/save_icon.svg)다음을누릅니다. AEM Forms 컨테이너 구성 요소는 페이지에 대해 활성화됩니다.

1. 1단계에서 열린 AEM Sites 페이지가 포함된 브라우저 탭을 엽니다. 구성 요소를 여기로 **드래그하십시오** 상자를 누르고 **+를 누릅니다.** 새 구성 **요소 삽입** 상자에서 AEM **양식을 탭합니다.** AEM **Forms** 컨테이너 구성 요소가 페이지에 추가됩니다.
1. AEM **Forms 컨테이너** 구성 요소를 탭하고 탭합니다 ![](assets/configure-icon.svg). AEM Forms 컨테이너의 속성이 있는 대화 상자가 나타납니다. 자산 **경로** 필드에서 shipping-address-add-update-form 적응형 양식을 찾아 선택합니다. 탭하기 ![](assets/save_icon.svg). 응용 양식이 페이지에 포함됩니다.
1. 적응형 양식과 사이트 페이지를 모두 게시합니다. 다음은 고려해야 할 몇 가지 사항입니다.

   * AEM 사이트 페이지를 처음으로 게시하고 포함된 양식을 포함하는 경우 사이트 페이지와 포함된 양식을 게시합니다.
   * 게시된 사이트 페이지에서 포함된 양식만 수정하는 경우 원본 양식을 게시하고 변경 사항이 게시된 사이트 페이지에 반영됩니다. 게시된 사이트 페이지에는 양식에 대한 참조가 포함되어 있으며 페이지를 다시 게시할 필요가 없습니다.
   * 사이트 페이지와 포함된 양식을 수정하는 경우 사이트 페이지와 양식을 다시 게시합니다.
   ![embed-in-aem-sites](assets/embed-in-aem-sites.png)

   배송 및 청구 주소 변경 양식이 AEM 사이트 페이지에 추가되었습니다.

## 외부 웹 페이지에 적응형 양식 포함 {#embed-the-adaptive-form-in-an-external-webpage}

외부 웹 페이지에 몇 줄의 JavaScript를 삽입하여 외부 웹 페이지(AEM 외부에 호스트된 비 AEM 웹 페이지)에 적응형 양식을 포함할 수 있습니다. JavaScript 코드는 적응형 양식 및 관련 리소스에 대해 AEM Forms 서버에 HTTP 요청을 보내고 적응형 양식을 웹 페이지에 추가합니다. 자세한 내용은 응용 양식을 외부 웹 페이지에 [포함을 참조하십시오](/help/forms/using/embed-adaptive-form-external-web-page.md).
