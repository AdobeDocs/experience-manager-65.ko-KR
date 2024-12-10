---
title: AEM 적응형 양식 6.5에서 턴스타일을 사용하는 방법
description: 턴스타일 서비스를 통해 손쉽게 양식 보안을 강화할 수 있습니다. 단계별 안내서가 포함되어 있습니다.
feature: Adaptive Forms, Foundation Components
role: User, Developer
exl-id: bed93ce3-89db-477a-8316-7598275e4bca
source-git-commit: 65425a4a779c6e7adffb1174c0076e03cbc54ac1
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 12%

---

# AEM Forms 환경과 턴스타일 연결 {#connect-your-forms-environment-with-turnstile-service}

<span class="preview">이 기능은 기능 전환 ID `FT_FORMS-12407`을(를) 기반으로 합니다. 기능을 활성화하려면 [기능 활성화 토글](/help/forms/using/enable-feature-toggle.md) 문서에 지정된 단계를 따르십시오. </span>

CAPTCHA(컴퓨터와 인간을 구분하기 위해 완전히 자동화된 공공 튜링 테스트)는 인간과 자동화된 프로그램 또는 봇을 구별하기 위해 온라인 거래에서 일반적으로 사용되는 프로그램입니다. 문제를 제기하고 사용자 응답을 평가하여 사이트와 상호 작용하는 것이 인간인지 봇인지 판단합니다. 테스트가 실패할 경우 사용자가 진행하지 못하도록 차단하고 봇이 스팸을 게시하거나 악의적인 목적으로 상호 작용하는 것을 방지하여 온라인 거래를 안전하게 할 수 있도록 도와줍니다.

AEM Forms 6.5는 다음 CAPTCHA 솔루션을 지원합니다.

* [Turnstile Captcha](/help/forms/using/integrate-adaptive-forms-turnstile.md)
* [Google recaptcha](/help/forms/using/captcha-adaptive-forms.md)
* [hCaptcha](/help/forms/using/integrate-adaptive-forms-hcaptcha.md)


<!-- ![Turnstile](assets/Turnstile-challenge.png)-->

## AEM Forms 환경과 Turnstile Captcha 통합

Cloudflare의 Turnstile Captcha는 자동화된 봇, 악의적인 공격, 스팸 및 원치 않는 자동화된 트래픽으로부터 양식 및 사이트를 보호하는 것을 목표로 하는 보안 조치입니다. 양식 제출을 허용하기 전에 양식 제출에 대한 확인란을 표시하여 사람인지 확인합니다.

>[!VIDEO](https://video.tv.adobe.com/v/3440940/)

### AEM Forms 환경을 Turnstile Captcha와 통합하기 위한 사전 요구 사항 {#prerequisite}

AEM Forms에 대해 Turnstile을 구성하려면 Turnstile 웹 사이트에서 [Turnstile 사이트 키 및 비밀 키](https://developers.cloudflare.com/turnstile/get-started/)를 가져와야 합니다.

### Turnstile 구성 {#steps-to-configure-hcaptcha}

AEM Forms을 Turnstile 서비스와 통합하려면 다음 단계를 수행하십시오.

1. AEM Forms 환경에서 구성 컨테이너를 만듭니다. 구성 컨테이너에는 AEM Forms을 외부 서비스에 연결하는 데 사용되는 클라우드 구성이 포함됩니다. 구성 컨테이너를 생성하려면:
   1. AEM Forms 환경을 엽니다.
   1. **[!UICONTROL 도구 > 일반 > 구성 브라우저]**&#x200B;로 이동합니다.
   1. 구성 브라우저에서 기존 폴더를 선택하거나 새 폴더를 만듭니다.
      * **새 폴더**&#x200B;를 만들고 클라우드 구성을 사용하려면:
         1. 구성 브라우저에서 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.
         1. 구성 만들기 대화 상자에서 이름, 제목을 지정하고 **[!UICONTROL 클라우드 구성]**&#x200B;을 확인합니다.
         1. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.
      * **기존 폴더**&#x200B;에 대해 클라우드 구성을 사용하려면:
         1. 구성 브라우저에서 폴더를 선택하고 **[!UICONTROL 속성]**&#x200B;을 클릭합니다.
         1. 구성 속성 대화 상자에서 **[!UICONTROL 클라우드 구성]**&#x200B;을 사용하도록 설정합니다.
         1. 구성을 저장하려면 **[!UICONTROL 저장 및 닫기]**&#x200B;를 클릭하십시오.

1. Cloud Service 구성:
   1. AEM 작성자 인스턴스에서 ![도구-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]**(으)로 이동한 다음 **[!UICONTROL 회전식]**을 클릭합니다.
      ![Cloud Service의 회전식 문](assets/turnstile-in-ui.png)
   1. 이전 섹션에서 설명한 대로 작성되거나 업데이트된 구성 컨테이너를 선택합니다. **[!UICONTROL 만들기]**를 클릭합니다.
      ![구성 Turnstile](assets/config-hcaptcha.png)
   1. **[!UICONTROL 위젯 유형]**&#x200B;을(를) 관리, 비대화형 또는 보이지 않는 것으로 지정하십시오.
   1. **[!UICONTROL 제목]**, **[!UICONTROL 이름]**&#x200B;과 같은 기타 세부 정보를 제공합니다.
   1. [필수 구성 요소에서 얻은](#prerequisite)턴스타일 서비스에 대해 **[!UICONTROL 사이트 키]** 및 **[!UICONTROL 비밀 키]**&#x200B;을(를) 지정하십시오.
   1. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.

      ![AEM Forms 환경을 Turnstile과 연결하도록 Cloud Service 구성](assets/config-turntstile.png)

   >[!NOTE]
   > 이미 턴스타일 유효성 검사를 위해 미리 채워져 있으므로 사용자는 클라이언트측 JavaScript 유효성 검사 URL 및 서버측 유효성 검사 URL을 수정할 필요가 없습니다.

   Turnstile Captcha 서비스가 구성되면 적응형 양식에서 사용할 수 있습니다.

## 적응형 양식 {#using-turnstile-aem-6.5}에서 Turnstile 사용

1. AEM Forms 환경을 엽니다.
1. **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**&#x200B;로 이동합니다.
1. 적응형 양식을 선택하고 **[!UICONTROL 속성]**&#x200B;을 클릭하세요. **[!UICONTROL 구성 컨테이너]**&#x200B;에서 Turnstile®에 대한 클라우드 구성을 선택하십시오.
1. **[!UICONTROL 저장 및 닫기]**&#x200B;를 클릭합니다.

   이러한 구성 컨테이너가 없는 경우 섹션 [AEM Forms 환경과 턴스타일 연결](#connect-your-forms-environment-with-turnstile-service)을 참조하여 구성 컨테이너를 만드는 방법을 알아보십시오.

   ![구성 컨테이너 선택](assets/captcha-properties.png)

1. 적응형 양식을 선택하고 **[!UICONTROL 편집]**&#x200B;을 클릭하여 편집기에서 적응형 양식을 엽니다.
1. 구성 요소 브라우저에서 **[!UICONTROL Captcha]** 구성 요소를 적응형 양식으로 드래그 앤 드롭합니다.
1. **[!UICONTROL 적응형 양식 회전식]** 구성 요소를 선택하고 속성 ![속성 아이콘](assets/configure-icon.svg) 아이콘을 클릭합니다. 속성 대화 상자가 열립니다. 다음 속성을 지정합니다.

   <!--![Turnstile v2](assets/turnstile-settings-v2.png)-->
   ![Cloudfare Turnstile v1](assets/turnstile-setting-v1.png)

   * **[!UICONTROL 제목]:** Captcha 구성 요소의 제목을 지정합니다. 양식 및 규칙 편집기에서 고유한 제목을 사용하여 양식 구성 요소를 쉽게 식별할 수 있습니다.
   * **[!UICONTROL 구성 설정]:** Turnstile에 대해 구성된 클라우드 구성을 선택하십시오.
   * **[!UICONTROL 유효성 검사 메시지]:** 양식 제출 또는 사용자 작업에서 Captcha의 유효성을 검사하기 위한 유효성 검사 메시지를 제공합니다.
   * **[!UICONTROL CAPTCHA 서비스]:** 양식 제출을 위한 CAPTCHA 서비스를 선택합니다. 여기서 Turnstile®을 선택합니다.
   * **[!UICONTROL 구성 설정]:** Turnstile®에 대해 구성된 클라우드 구성을 선택하십시오.
     >[!NOTE]
     >유사한 목적으로 환경에 여러 클라우드 구성을 가질 수 있습니다. 그러므로, 서비스를 신중하게 선택하십시오. 서비스가 목록에 없으면 [AEM Forms 환경을 Turnstile과 연결](#connect-your-forms-environment-with-turnstile-service)을 참조하여 AEM Forms 환경을 Turnstile 서비스와 연결하는 Cloud Service을 만드는 방법에 대해 알아보십시오.
   * **오류 메시지:** Captcha 제출이 실패할 때 사용자에게 표시할 오류 메시지를 제공합니다.
   * **Captcha 크기:** hCaptcha® 챌린지 대화 상자의 표시 크기를 선택할 수 있습니다. 작은 크기를 표시하려면 **[!UICONTROL Compact]** 옵션을 사용하고, 상대적으로 큰 크기의 hCaptcha® 문제 대화 상자를 표시하려면 **[!UICONTROL Normal]**&#x200B;을 사용하십시오.

1. **[!UICONTROL 완료]**&#x200B;를 선택합니다.


이제 양식 작성기가 성공적으로 턴스타일 서비스에 의해 제기된 문제를 지우는 합법적인 양식만 양식 제출이 허용됩니다.

![회전식 질문](assets/turnstile-challenge.png)


## 자주 묻는 질문

* **Q: 적응형 양식에서 두 개 이상의 Captcha 구성 요소를 사용할 수 있습니까?**
* **Ans:** 적응형 양식에서 둘 이상의 Captcha 구성 요소를 사용할 수 없습니다. 또한, 지연 로드로 표시된 조각 또는 패널에서는 Captcha 구성 요소를 사용하지 않는 것이 좋습니다.

## 추가 참조 {#see-also}

* [적응형 양식에서 CAPTCHA 사용](/help/forms/using/captcha-adaptive-forms.md)
* [적응형 양식에서 hCaptcha 사용](/help/forms/using/integrate-adaptive-forms-hcaptcha.md)
