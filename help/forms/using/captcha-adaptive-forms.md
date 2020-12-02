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
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 0%

---


# 응용 양식에 CAPTCHA 사용{#using-captcha-in-adaptive-forms}

CAPTCHA(Computers and Human Apart)는 컴퓨터 및 인간을 구분하기 위해 온라인 거래에서 일반적으로 사용되는 프로그램이다. 문제가 발생하고 사용자 응답을 평가하여 그것이 사이트와의 상호 작용인지 확인합니다. 이는 사용자가 테스트에 실패할 경우 진행할 수 없게 하고 보트가 스팸이나 악의적인 목적을 게시하지 못하도록 하여 온라인 거래를 안전하게 할 수 있도록 합니다.

AEM Forms은 적응형 양식의 CAPTCHA를 지원합니다. Google의 reCAPTCHA 서비스를 사용하여 CAPTCHA를 구현할 수 있습니다.

>[!NOTE]
>
>* AEM Forms은 reCaptcha v2만 지원합니다. 다른 버전은 지원되지 않습니다.
>* 적응형 양식의 CAPTCHA는 AEM Forms 앱의 오프라인 모드에서 지원되지 않습니다.

>



## Google {#google-recaptcha}에 의한 ReCAPTCHA 서비스 구성

양식 작성자는 Google의 reCAPTCHA 서비스를 사용하여 적응형 양식에 CAPTCHA를 구현할 수 있습니다. 사이트를 보호하는 고급 CAPTCHA 기능을 제공합니다. reCAPTCHA가 작동하는 방법에 대한 자세한 내용은 [Google reCAPTCHA](https://developers.google.com/recaptcha/)을 참조하십시오.

![Recaptcha](assets/recaptcha_new.png)

AEM Forms에서 reCAPTCHA 서비스를 구현하려면:

1. Google에서 [reCAPTCHA API 키 페어](https://www.google.com/recaptcha/admin)을 얻습니다. 사이트 키와 비밀이 포함되어 있습니다.
1. 클라우드 서비스의 구성 컨테이너를 만듭니다.

   1. **[!UICONTROL 도구 > 일반 > 구성 브라우저]**&#x200B;로 이동합니다.
      * 자세한 내용은 [구성 브라우저](/help/sites-administering/configurations.md) 설명서를 참조하십시오.
   1. 클라우드 구성에 대한 글로벌 폴더를 활성화하거나 이 단계를 건너뛰어 클라우드 서비스 구성에 대한 다른 폴더를 만들고 구성하려면 다음을 수행하십시오.

      1. 구성 브라우저에서 **[!UICONTROL global]** 폴더를 선택하고 **[!UICONTROL 속성]**&#x200B;을 탭합니다.

      1. 구성 속성 대화 상자에서 **[!UICONTROL 클라우드 구성]**&#x200B;을 활성화합니다.
      1. **[!UICONTROL 저장 및 닫기]**&#x200B;를 눌러 구성을 저장하고 대화 상자를 종료합니다.
   1. 구성 브라우저에서 **[!UICONTROL 만들기]**&#x200B;를 누릅니다.
   1. 구성 만들기 대화 상자에서 폴더의 제목을 지정하고 **[!UICONTROL 클라우드 구성]**&#x200B;을 활성화합니다.
   1. **[!UICONTROL 만들기]**&#x200B;를 눌러 클라우드 서비스 구성에 대해 활성화된 폴더를 만듭니다.


1. reCAPTCHA에 대한 클라우드 서비스를 구성합니다.

   1. AEM 작성자 인스턴스의 경우 ![tools-1](assets/tools-1.png) > **Cloud Services**&#x200B;으로 이동합니다.
   1. **[!UICONTROL reCAPTCHA]**&#x200B;을 누릅니다. 구성 페이지가 열립니다. 이전 단계에서 만든 구성 컨테이너를 선택하고 **[!UICONTROL 만들기]**&#x200B;를 누릅니다.
   1. reCAPTCHA 서비스의 이름, 사이트 키 및 암호 키를 지정하고 **[!UICONTROL 만들기]**&#x200B;를 눌러 클라우드 서비스 구성을 만듭니다.
   1. 구성 요소 편집 대화 상자에서 1단계에서 얻은 사이트 및 비밀 키를 지정합니다. **설정 저장**&#x200B;을 누른 다음 **OK**&#x200B;을 눌러 구성을 완료합니다.

   reCAPTCHA 서비스가 구성되면 적응형 양식에서 사용할 수 있습니다. 자세한 내용은 응용 양식에 [CAPTCHA 사용](#using-captcha)을 참조하십시오.

## 적응형 양식 {#using-captcha}에 CAPTCHA 사용

적응형 양식에서 CAPTCHA를 사용하려면:

1. 편집 모드에서 응용 양식을 엽니다.

   >[!NOTE]
   >
   >응용 양식을 만들 때 선택한 구성 컨테이너에 reCAPTCHA 클라우드 서비스가 포함되어 있는지 확인합니다. 적응형 양식 속성을 편집하여 양식과 연관된 구성 컨테이너를 변경할 수도 있습니다.

1. 구성 요소 브라우저에서 **Captcha** 구성 요소를 응용 양식으로 드래그하여 놓습니다.

   >[!NOTE]
   >
   >응용 양식에 둘 이상의 Captcha 구성 요소 사용은 지원되지 않습니다. 또한 지연 로딩으로 표시된 패널이나 조각에서 CAPTCHA를 사용하는 것이 좋습니다.

   >[!NOTE]
   >
   >Captcha는 시간에 따라 적용되며 1분 후에 만료됩니다. 따라서 응용 양식의 [제출] 단추 바로 앞에 Captcha 구성 요소를 배치하는 것이 좋습니다.

1. 추가한 Captcha 구성 요소를 선택하고 ![cmppr](assets/cmppr.png)을 눌러 해당 속성을 편집합니다.
1. CAPTCHA 위젯의 제목을 지정합니다. 기본값은 **Captcha**&#x200B;입니다. 제목을 표시하지 않으려면 **제목**&#x200B;을 선택합니다.
1. **Captcha service** 드롭다운에서 **reCaptcha**&#x200B;를 선택하여 Google](#google-recaptcha)의 [ReCAPTCHA 서비스에 설명된 대로 구성한 경우 reCAPTCHA 서비스를 활성화합니다. 설정 드롭다운에서 구성을 선택합니다. 또한 reCAPTCHA 위젯의 경우 크기를 **Normal** 또는 **Compact**&#x200B;으로 선택합니다.

   >[!NOTE]
   >
   >기본 AEM CAPTCHA 서비스가 더 이상 사용되지 않으므로 Captcha 서비스 드롭다운에서 **[!UICONTROL Default]**&#x200B;를 선택하지 마십시오.

1. 속성을 저장합니다.

reCAPTCHA 서비스는 응용 양식에서 활성화됩니다. 양식을 미리 보고 CAPTCHA가 작동하는 것을 확인할 수 있습니다.
