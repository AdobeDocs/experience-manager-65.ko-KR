---
title: 적응형 양식에서 CAPTCHA 사용
seo-title: 적응형 양식에서 CAPTCHA 사용
description: 적응형 양식으로 AEM CAPTCHA 또는 Google reCAPTCHA 서비스를 구성하는 방법을 알아봅니다.
seo-description: 적응형 양식으로 AEM CAPTCHA 또는 Google reCAPTCHA 서비스를 구성하는 방법을 알아봅니다.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
feature: 적응형 양식
exl-id: 9b4219b8-d5eb-4099-b205-d98d84e0c249
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1291'
ht-degree: 0%

---

# 적응형 양식에서 CAPTCHA 사용{#using-captcha-in-adaptive-forms}

CAPTCHA(컴퓨터와 인간을 구분하기 위해 완전히 자동화된 공공 튜링 테스트)는 사람과 자동화된 프로그램 또는 보트를 구별하기 위해 온라인 트랜잭션에 자주 사용되는 프로그램입니다. 과제를 안고 사용자 응답을 평가하여 그것이 사람인지 아니면 사이트와 상호 작용하는 봇인지를 결정합니다. 따라서 테스트가 실패하면 사용자가 진행할 수 없고, 봇이 스팸 또는 악의적인 목적을 게시하지 못하도록 하여 온라인 거래를 안전하게 할 수 있습니다.

AEM Forms은 적응형 양식에서 CAPTCHA를 지원합니다. Google의 reCAPTCHA 서비스를 사용하여 CAPTCHA를 구현할 수 있습니다.

>[!NOTE]
>
>* AEM Forms은 reCaptcha v2만 지원합니다. 다른 버전은 지원되지 않습니다.
>* 적응형 양식의 CAPTCHA는 AEM Forms 앱의 오프라인 모드에서 지원되지 않습니다.

>



## Google에서 ReCAPTCHA 서비스 구성 {#google-recaptcha}

양식 작성자는 Google의 reCAPTCHA 서비스를 사용하여 적응형 양식에 CAPTCHA를 구현할 수 있습니다. 사이트를 보호하기 위한 고급 CAPTCHA 기능을 제공합니다. reCAPTCHA 작동 방식에 대한 자세한 내용은 [Google reCAPTCHA](https://developers.google.com/recaptcha/) 를 참조하십시오.

![Recaptcha](assets/recaptcha_new.png)

AEM Forms에서 reCAPTCHA 서비스를 구현하려면 다음을 수행하십시오.

1. Google에서 [reCAPTCHA API 키 쌍](https://www.google.com/recaptcha/admin)을 얻습니다. 사이트 키와 암호가 포함되어 있습니다.
1. 클라우드 서비스용 구성 컨테이너를 만듭니다.

   1. **[!UICONTROL 도구 > 일반 > 구성 브라우저]**&#x200B;로 이동합니다.
      * 자세한 내용은 [구성 브라우저](/help/sites-administering/configurations.md) 설명서를 참조하십시오.
   1. 클라우드 구성에 대한 글로벌 폴더를 활성화하려면 다음을 수행하십시오. 또는 이 단계를 건너뛰고 클라우드 서비스 구성에 대한 다른 폴더를 만들고 구성하려면 다음을 수행하십시오.

      1. 구성 브라우저에서 **[!UICONTROL 전역]** 폴더를 선택하고 **[!UICONTROL 속성]**&#x200B;을 누릅니다.

      1. 구성 속성 대화 상자에서 **[!UICONTROL 클라우드 구성]**&#x200B;을 활성화합니다.
      1. **[!UICONTROL 저장 및 닫기]**&#x200B;를 눌러 구성을 저장하고 대화 상자를 종료합니다.
   1. 구성 브라우저에서 **[!UICONTROL 만들기]**&#x200B;를 누릅니다.
   1. 구성 만들기 대화 상자에서 폴더의 제목을 지정하고 **[!UICONTROL 클라우드 구성]**&#x200B;을 활성화합니다.
   1. 클라우드 서비스 구성에 대해 활성화된 폴더를 만들려면 **[!UICONTROL 만들기]**&#x200B;를 탭합니다.


1. reCAPTCHA에 대한 클라우드 서비스를 구성합니다.

   1. AEM 작성자 인스턴스에서 ![도구-1](assets/tools-1.png) > **Cloud Services**&#x200B;로 이동합니다.
   1. **[!UICONTROL reCAPTCHA]**&#x200B;를 누릅니다. 구성 페이지가 열립니다. 이전 단계에서 만든 구성 컨테이너를 선택하고 **[!UICONTROL 만들기]**&#x200B;를 누릅니다.
   1. reCAPTCHA 서비스의 이름, 사이트 키 및 비밀 키를 지정하고 **[!UICONTROL 만들기]**&#x200B;를 탭하여 클라우드 서비스 구성을 만듭니다.
   1. 구성 요소 편집 대화 상자에서 1단계에서 얻은 사이트 및 비밀 키를 지정합니다. **설정 저장**&#x200B;을 탭한 다음, **확인**&#x200B;을 탭하여 구성을 완료합니다.

   reCAPTCHA 서비스가 구성되면 적응형 양식에서 사용할 수 있습니다. 자세한 내용은 적응형 양식에서 CAPTCHA 사용](#using-captcha)을 참조하십시오.[

## 적응형 양식에서 CAPTCHA 사용 {#using-captcha}

적응형 양식에 CAPTCHA를 사용하려면:

1. 편집 모드에서 적응형 양식을 엽니다.

   >[!NOTE]
   >
   >적응형 양식을 만들 때 선택한 구성 컨테이너에 reCAPTCHA 클라우드 서비스가 포함되어 있는지 확인합니다. 적응형 양식 속성을 편집하여 양식과 연결된 구성 컨테이너를 변경할 수도 있습니다.

1. 구성 요소 브라우저에서 **Captcha** 구성 요소를 적응형 양식으로 드래그합니다.

   >[!NOTE]
   >
   >적응형 양식에서 두 개 이상의 Captcha 구성 요소를 사용할 수 없습니다. 또한 지연 로딩으로 표시된 패널 또는 조각에서 CAPTCHA를 사용하지 않는 것이 좋습니다.

   >[!NOTE]
   >
   >Captcha는 시간에 민감하며 약 1분 후에 만료됩니다. 따라서 [제출] 단추 바로 앞에 Captcha 구성 요소를 적응형 양식으로 배치하는 것이 좋습니다.

1. 추가한 Captcha 구성 요소를 선택하고 ![cmppr](assets/cmppr.png)을 탭하여 해당 속성을 편집합니다.
1. CAPTCHA 위젯의 제목을 지정합니다. 기본값은 **Captcha**&#x200B;입니다. 제목을 표시하지 않으려면 **제목 숨기기**&#x200B;를 선택합니다.
1. **Captcha 서비스** 드롭다운에서 **reCaptcha** 를 선택하여 Google](#google-recaptcha)ReCAPTCHA 서비스에 설명된 대로 구성한 경우 reCAPTCHA 서비스를 활성화합니다. [ 설정 드롭다운에서 구성을 선택합니다. 또한 reCAPTCHA 위젯의 경우 크기를 **Normal** 또는 **Compact**&#x200B;로 선택합니다.

   >[!NOTE]
   >
   >기본 AEM CAPTCHA 서비스가 더 이상 사용되지 않으므로 Captcha 서비스 드롭다운에서 **[!UICONTROL 기본]**&#x200B;을 선택하지 마십시오.

1. 속성을 저장합니다.

reCAPTCHA 서비스는 적응형 양식에서 활성화됩니다. 양식을 미리 보고 CAPTCHA가 작동하는 것을 볼 수 있습니다.

### 규칙 {#show-hide-captcha}에 따라 CAPTCHA 구성 요소를 표시하거나 숨깁니다.

적응형 양식의 구성 요소에 적용하는 규칙에 따라 CAPTCHA 구성 요소를 표시하거나 숨기도록 선택할 수 있습니다. 구성 요소를 탭하고 ![규칙 편집](assets/edit-rules-icon.svg)을 선택한 다음, **[!UICONTROL 만들기]**&#x200B;를 탭하여 규칙을 만듭니다. 규칙 만들기에 대한 자세한 내용은 [규칙 편집기](rule-editor.md)를 참조하십시오.

예를 들어 양식의 통화 값 필드에 값이 25000 이상인 경우에만 CAPTCHA 구성 요소가 적응형 양식에 표시되어야 합니다.

양식에서 **[!UICONTROL 통화 값]** 필드를 탭하고 다음 규칙을 만듭니다.

![규칙 표시 또는 숨기기](assets/rules-show-hide-captcha.png)

### CAPTCHA 유효성 검사 {#validate-captcha}

양식을 제출할 때 적응형 양식의 CAPTCHA의 유효성을 검사하거나 사용자 작업 및 조건에 따라 CAPTCHA 유효성 검사를 수행할 수 있습니다.

#### 양식 제출 시 CAPTCHA 유효성 검사 {#validation-form-submission}

적응형 양식을 제출할 때 CAPTCHA를 자동으로 확인하려면:

1. CAPTCHA 구성 요소를 탭하고 ![cmppr](assets/configure-icon.svg)을 선택하여 구성 요소 속성을 확인합니다.
1. **[!UICONTROL CAPTCHA 유효성 검사]** 섹션에서 **[!UICONTROL 양식 제출 시 CAPTCHA 유효성 검사]**&#x200B;를 선택합니다.
1. ![완료](assets/save_icon.svg)를 눌러 구성 요소 속성을 저장합니다.

#### 사용자 작업 및 조건에 대한 CAPTCHA 유효성 검사 {#validate-captcha-user-action}

조건 및 사용자 작업을 기반으로 하여 CAPTCHA의 유효성을 검사하려면 다음을 수행하십시오.

1. CAPTCHA 구성 요소를 탭하고 ![cmppr](assets/configure-icon.svg)을 선택하여 구성 요소 속성을 확인합니다.
1. **[!UICONTROL CAPTCHA 유효성 검사]** 섹션에서 사용자 작업&#x200B;]**에서**[!UICONTROL  CAPTCHA 유효성 검사 를 선택합니다.
1. ![완료](assets/save_icon.svg)를 눌러 구성 요소 속성을 저장합니다.

[!DNL Experience Manager Forms] 사전  `ValidateCAPTCHA` 정의된 조건을 사용하여 CAPTCHA의 유효성을 확인하기 위한 API를 제공합니다. 사용자 지정 제출 작업을 사용하거나 적응형 양식의 구성 요소에 대한 규칙을 정의하여 API를 호출할 수 있습니다.

다음은 사전 정의된 조건을 사용하여 CAPTCHA의 유효성을 검사하는 `ValidateCAPTCHA` API의 예입니다.

```javascript
if (slingRequest.getParameter("numericbox1614079614831").length() >= 5) {
    	GuideCaptchaValidatorProvider apiProvider = sling.getService(GuideCaptchaValidatorProvider.class);
        String formPath = slingRequest.getResource().getPath();
        String captchaData = slingRequest.getParameter(GuideConstants.GUIDE_CAPTCHA_DATA);
        if (!apiProvider.validateCAPTCHA(formPath, captchaData).isCaptchaValid()){
            response.setStatus(400);
            return;
        }
    }
```

이 예는 `ValidateCAPTCHA` API가 양식을 채우는 동안 사용자가 지정한 숫자 상자의 자릿수가 5보다 큰 경우에만 양식에서 CAPTCHA의 유효성을 검사함을 의미합니다.

**옵션 1:사용자  [!DNL Experience Manager Forms] 지정 제출 작업을 사용하여 CAPTCHA의 유효성을 검사하려면 ValidateCAPTCHA API를 사용합니다**

다음 단계를 수행하여 `ValidateCAPTCHA` API를 사용하여 사용자 지정 제출 작업을 사용하여 CAPTCHA의 유효성을 검사하십시오.

1. `ValidateCAPTCHA` API를 포함하는 스크립트를 사용자 지정 제출 작업에 추가합니다. 사용자 지정 제출 작업에 대한 자세한 내용은 [응용 Forms에 대한 사용자 지정 제출 작업 만들기](custom-submit-action-form.md)를 참조하십시오.
1. 적응형 양식의 **[!UICONTROL 제출]** 속성의 **[!UICONTROL 제출 작업]** 드롭다운 목록에서 사용자 지정 제출 작업의 이름을 선택합니다.
1. **[!UICONTROL Submit]**&#x200B;을 누릅니다. CAPTCHA는 사용자 지정 제출 작업의 `ValidateCAPTCHA` API에 정의된 조건을 기반으로 유효성을 검사합니다.

**옵션 2:양식을  [!DNL Experience Manager Forms] 제출하기 전에 사용자 작업에서 CAPTCHA의 유효성을 검사하려면 ValidateCAPTCHA API를 사용합니다**

적응형 양식의 구성 요소에 규칙을 적용하여 `ValidateCAPTCHA` API를 호출할 수도 있습니다.

예를 들어 적응형 양식에 **[!UICONTROL CAPTCHA]** 유효성 검사 단추를 추가하고 단추 클릭으로 서비스를 호출하는 규칙을 만듭니다.

다음 그림은 **[!UICONTROL CAPTCHA 유효성 검사]** 단추를 클릭할 때 서비스를 호출하는 방법을 보여 줍니다.

![CAPTCHA 유효성 검사](assets/captcha-validation1.gif)

규칙 편집기를 사용하여 `ValidateCAPTCHA` API를 포함하는 사용자 지정 서블릿을 호출하고 유효성 검사 결과에 따라 적응형 양식의 제출 단추를 활성화 또는 비활성화할 수 있습니다.

마찬가지로 규칙 편집기를 사용하여 사용자 지정 메서드를 포함하여 적응형 양식에 CAPTCHA의 유효성을 검사할 수 있습니다.

### 사용자 지정 CAPTCHA 서비스 {#add-custom-captcha-service} 추가

[!DNL Experience Manager Forms] 는 reCAPTCHA를 CAPTCHA 서비스로 제공합니다. 그러나 **[!UICONTROL CAPTCHA 서비스]** 드롭다운 목록에 표시할 사용자 지정 서비스를 추가할 수 있습니다.

다음은 적응형 양식에 추가 CAPTCHA 서비스를 추가하기 위한 인터페이스의 샘플 구현입니다.

```javascript
package com.adobe.aemds.guide.service;

import org.osgi.annotation.versioning.ConsumerType;

/**
 * An interface to provide captcha validation at server side in Adaptive Form
 * This interface can be used to provide custom implementation for different captcha services.
 */
@ConsumerType
public interface GuideCaptchaValidator {
    /**
     * This method should define the actual validation logic of the captcha
     * @param captchaPropertyNodePath path to the node with CAPTCHA configurations inside form container
     * @param userResponseToken  The user response token provided by the CAPTCHA from client-side
     *
     * @return  {@link GuideCaptchaValidationResult} validation result of the captcha
     */
     GuideCaptchaValidationResult validateCaptcha(String captchaPropertyNodePath, String userResponseToken);

    /**
     * Returns the name of the captcha validator. This should be unique among the different implementations
     * @return  name of the captcha validator
     */
     String getCaptchaValidatorName();
}
```

`captchaPropertyNodePath` 는 Sling 저장소에 있는 CAPTCHA 구성 요소의 리소스 경로를 나타냅니다. CAPTCHA 구성 요소에 대한 세부 사항을 포함하려면 이 속성을 사용하십시오. 예를 들어 `captchaPropertyNodePath`에는 CAPTCHA 구성 요소에 구성된 reCAPTCHA 클라우드 구성에 대한 정보가 포함되어 있습니다. 클라우드 구성 정보는 reCAPTCHA 서비스를 구현하기 위한 **[!UICONTROL 사이트 키]** 및 **[!UICONTROL 비밀 키]** 설정을 제공합니다.

`userResponseToken` 는  `g_recaptcha_response` 양식에서 CAPTCHA를 해결한 후 생성된 를 나타냅니다.
