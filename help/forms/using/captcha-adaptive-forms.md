---
title: 적응형 양식에서 CAPTCHA 사용
seo-title: 적응형 양식에서 CAPTCHA 사용
description: 적응형 양식에서 AEM CAPTCHA 또는 Google reCAPTCHA 서비스를 구성하는 방법을 알아봅니다.
seo-description: 적응형 양식에서 AEM CAPTCHA 또는 Google reCAPTCHA 서비스를 구성하는 방법을 알아봅니다.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---


# 적응형 양식에서 CAPTCHA 사용{#using-captcha-in-adaptive-forms}

CAPTCHA(Computers and Human Apart)는 컴퓨터 및 인간을 구분하기 위해 온라인 거래에서 일반적으로 사용되는 프로그램이다. 문제가 발생하고 사용자 응답을 평가하여 그것이 사이트와의 상호 작용인지 확인합니다. 이는 사용자가 테스트에 실패할 경우 진행할 수 없게 하고 보트가 스팸이나 악의적인 목적을 게시하지 못하도록 하여 온라인 거래를 안전하게 할 수 있도록 합니다.

AEM Forms은 적응형 양식의 CAPTCHA를 지원합니다. Google의 reCAPTCHA 서비스를 사용하여 CAPTCHA를 구현할 수 있습니다.

>[!NOTE]
>
>* AEM Forms은 reCaptcha v2만 지원합니다. 다른 버전은 지원되지 않습니다.
>* 적응형 양식의 CAPTCHA는 AEM Forms 앱의 오프라인 모드에서 지원되지 않습니다.

>



## Google에서 ReCAPTCHA 서비스 구성 {#google-recaptcha}

양식 작성자는 Google의 reCAPTCHA 서비스를 사용하여 적응형 양식에 CAPTCHA를 구현할 수 있습니다. 사이트를 보호하는 고급 CAPTCHA 기능을 제공합니다. reCAPTCHA의 작동 방식에 대한 자세한 내용은 [Google reCAPTCHA를 참조하십시오](https://developers.google.com/recaptcha/).

![Recaptcha](assets/recaptcha_new.png)

AEM Forms에서 reCAPTCHA 서비스를 구현하려면:

1. Google [에서 reCAPTCHA API 키 쌍을](https://www.google.com/recaptcha/admin) 얻습니다. 사이트 키와 비밀이 포함되어 있습니다.
1. 클라우드 서비스의 구성 컨테이너를 만듭니다.

   1. 도구 > **[!UICONTROL 일반 > 구성 브라우저로 이동합니다]**.
   1. 클라우드 구성에 대한 글로벌 폴더를 활성화하거나 이 단계를 건너뛰어 클라우드 서비스 구성에 대한 다른 폴더를 만들고 구성하려면 다음을 수행하십시오.

      1. 구성 브라우저에서 **[!UICONTROL 전역]** 폴더를 선택하고 속성을 **[!UICONTROL 누릅니다]**.

      1. 구성 속성 대화 상자에서 **[!UICONTROL 클라우드 구성을 활성화합니다]**.
      1. 저장 **[!UICONTROL 및 닫기를]** 눌러 구성을 저장하고 대화 상자를 종료합니다.
   1. 구성 브라우저에서 만들기를 **[!UICONTROL 누릅니다]**.
   1. 구성 만들기 대화 상자에서 폴더 제목을 지정하고 **[!UICONTROL 클라우드 구성을 활성화합니다]**.
   1. 만들기 **[!UICONTROL 를]** 눌러 클라우드 서비스 구성에 대해 활성화된 폴더를 만듭니다.


1. reCAPTCHA에 대한 클라우드 서비스를 구성합니다.

   1. AEM 작성 인스턴스에서 ![도구-1](assets/tools-1.png) > **Cloud Service으로 이동합니다**.
   1. reCAPTCHA **[!UICONTROL 를 누릅니다]**. 구성 페이지가 열립니다. 이전 단계에서 만든 구성 컨테이너를 선택하고 만들기를 **[!UICONTROL 누릅니다]**.
   1. reCAPTCHA 서비스의 이름, 사이트 키 및 암호 키를 지정하고 **[!UICONTROL 만들기를]** 탭하여 클라우드 서비스 구성을 만듭니다.
   1. 구성 요소 편집 대화 상자에서 1단계에서 얻은 사이트 및 비밀 키를 지정합니다. 설정 **저장을** 누른 다음 **확인을** 눌러 구성을 완료합니다.

   reCAPTCHA 서비스가 구성되면 적응형 양식에서 사용할 수 있습니다. 자세한 내용은 적응형 양식에서 [CAPTCHA 사용을 참조하십시오](#using-captcha).

## 적응형 양식에 CAPTCHA 사용 {#using-captcha}

적응형 양식에서 CAPTCHA를 사용하려면:

1. 편집 모드에서 응용 양식을 엽니다.

   >[!NOTE]
   >
   >응용 양식을 만들 때 선택한 구성 컨테이너에 reCAPTCHA 클라우드 서비스가 포함되어 있는지 확인합니다. 적응형 양식 속성을 편집하여 양식과 연관된 구성 컨테이너를 변경할 수도 있습니다.

1. 구성 요소 브라우저에서 Captcha **구성 요소를** 응용 양식으로 드래그하여 놓습니다.

   >[!NOTE]
   >
   >응용 양식에 둘 이상의 Captcha 구성 요소 사용은 지원되지 않습니다. 또한 지연 로딩으로 표시된 패널이나 조각에서 CAPTCHA를 사용하는 것이 좋습니다.

   >[!NOTE]
   >
   >Captcha는 시간에 따라 적용되며 1분 후에 만료됩니다. 따라서 응용 양식의 [제출] 단추 바로 앞에 Captcha 구성 요소를 배치하는 것이 좋습니다.

1. 추가한 Captcha 구성 요소를 선택하고 ![cmppr](assets/cmppr.png) 을 눌러 해당 속성을 편집합니다.
1. CAPTCHA 위젯의 제목을 지정합니다. The default value is **Captcha**. 제목을 표시하지 않으려면 **제목** 숨기기를 선택합니다.
1. Captcha **서비스** 드롭다운에서 Google **의 ReCAPTCHA 서비스에 설명된 대로 구성한 경우 reCaptcha를** 선택하여 reCAPTCHA 서비스를 [활성화합니다](#google-recaptcha). 설정 드롭다운에서 구성을 선택합니다. 또한 reCAPTCHA 위젯의 크기 **를** 표준 **** 또는요약으로선택합니다.

   >[!NOTE]
   >
   >기본 AEM **[!UICONTROL CAPTCHA]** 서비스는 더 이상 사용되지 않으므로 Captcha 서비스 드롭다운에서 기본값을 선택하지 마십시오.

1. 속성을 저장합니다.

reCAPTCHA 서비스는 응용 양식에서 활성화됩니다. 양식을 미리 보고 CAPTCHA가 작동하는 것을 확인할 수 있습니다.
