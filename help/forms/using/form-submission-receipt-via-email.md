---
title: 이메일을 통해 양식 제출 확인 보내기
seo-title: Sending a form submission acknowledgement via email
description: AEM Forms에서는 양식 제출 시 사용자에게 승인을 보내는 이메일 제출 작업을 구성할 수 있습니다.
seo-description: AEM Forms allows you to configure the email submit action that sends an acknowledgement to a user on submitting the form.
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
exl-id: bca4044a-18a9-4b97-92de-eff1e9a840f9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# 이메일을 통해 양식 제출 확인 보내기 {#sending-a-form-submission-acknowledgement-via-email}

## 적응형 양식 데이터 제출 {#adaptive-form-data-submission}

적응형 양식은 여러 가지 기본 제공 [작업 제출](../../forms/using/configuring-submit-actions.md) 다른 종단점에 양식 데이터를 제출하는 워크플로우입니다.

예: **[!UICONTROL 이메일 보내기]** 제출 작업은 적응형 양식을 성공적으로 제출할 때 이메일을 전송합니다. 양식 데이터와 이메일의 PDF을 보내도록 구성할 수도 있습니다.

이 문서에서는 적응형 양식에서 이메일 작업을 활성화하는 단계 및 제공하는 다양한 구성에 대해 자세히 설명합니다.

>[!NOTE]
>
>를 사용할 수도 있습니다 **[!UICONTROL 이메일을 통해 PDF 보내기]** 완료된 양식을 PDF 첨부 파일로 이메일로 보내는 옵션. 이 작업에 사용할 수 있는 구성 옵션은 **[!UICONTROL 이메일 보내기]** 작업. 이메일 PDF 작업은 XFA 기반 적응형 양식에만 사용할 수 있습니다

## 전자 메일 보내기 작업 {#email-action}

전자 메일 보내기 작업을 사용하면 작성자는 적응형 양식을 성공적으로 제출할 때 하나 이상의 수신자에게 전자 메일을 자동으로 보낼 수 있습니다.

>[!NOTE]
>
>전자 메일 보내기 작업을 사용하려면 다음에 설명된 대로 AEM 메일 서비스를 구성해야 합니다. [메일 서비스 구성](/help/sites-administering/notification.md#configuring-the-mail-service).

### 적응형 양식에서 이메일 보내기 작업 활성화 {#enabling-email-action-on-an-adaptive-form}

1. 에서 적응형 양식 열기 **[!UICONTROL 편집]** 모드.

1. 에서 **[!UICONTROL 컨텐츠]** 탭, 탭 **[!UICONTROL 양식 컨테이너]** 탭 ![구성](assets/configure-icon.svg) 적응형 양식 속성을 보려면

1. 에서 **[!UICONTROL 제출]** 섹션, **[!UICONTROL 이메일 보내기]** 에서 **[!UICONTROL 작업 제출]** 드롭다운 목록.

   ![작업 제출](assets/submission-actions.png)

1. 에서 유효한 이메일 ID를 지정합니다. **[!UICONTROL 종료]**, **[!UICONTROL CC]**, 및 **[!UICONTROL 숨은 참조]** 필드.

   이메일의 제목과 본문을 **[!UICONTROL 제목]** 및 **[!UICONTROL 이메일 템플릿]** 필드(각각)를 반환합니다.

   필드에 변수 자리 표시자를 지정할 수도 있습니다. 이 경우 최종 사용자가 양식을 성공적으로 제출할 때 필드 값이 처리됩니다. 자세한 내용은 [적응형 양식 필드 이름을 사용하여 전자 메일 콘텐츠를 동적으로 만들기](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   선택 **[!UICONTROL 첨부 파일 포함]** 양식에 첨부 파일이 포함되어 있고 이러한 파일을 전자 메일에 첨부하려는 경우

   >[!NOTE]
   >
   >을(를) 선택하는 경우 **[!UICONTROL 이메일을 통해 PDF 보내기]** 옵션을 사용하려면 첨부 포함 옵션을 선택해야 합니다.

1. 클릭 ![저장](assets/save_icon.svg) 변경 사항을 저장하려면 을 클릭합니다.

### 적응형 양식 필드 이름을 사용하여 전자 메일 콘텐츠를 동적으로 만들기 {#using-adaptive-form-field-names-to-dynamically-create-email-content}

적응형 양식의 필드 이름은 사용자가 양식을 제출한 후 해당 필드의 값으로 대체되는 자리 표시자라고 합니다.

에서 **[!UICONTROL 이메일 보내기]** 작업을 수행하면 작업이 수행될 때 처리되는 자리 표시자를 사용할 수 있습니다. 이것은 이메일의 헤더(예: **[!UICONTROL 종료]**, **[!UICONTROL CC]**, **[!UICONTROL 숨은 참조]**, **[!UICONTROL 제목]**)은 사용자가 양식을 제출할 때 생성됩니다.

자리 표시자를 정의하려면 `${<field name>}` 선택 후 필드에서 **[!UICONTROL 이메일 보내기]** 을 제출 작업으로 사용할 수 있습니다.

예를 들어 양식에 가 포함되어 있으면 **[!UICONTROL 이메일 주소]** 필드, 이름이 지정됨 `email_addr`의 경우 사용자의 이메일 ID를 캡처하기 위해에서 다음을 지정할 수 있습니다. **[!UICONTROL 종료]**, **[!UICONTROL CC]**, 또는 **[!UICONTROL 숨은 참조]** 필드.

`${email_addr}`

사용자가 양식을 제출하면 이메일이 `email_addr` 필드의 값을 지정합니다.

>[!NOTE]
>
>에서 필드 이름을 찾을 수 있습니다 **[!UICONTROL 편집]** 대화 상자를 엽니다.

변수 자리 표시자는 **[!UICONTROL 제목]** 및 **[!UICONTROL 이메일 템플릿]** 필드.

예:

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>반복 가능한 패널의 필드는 변수 자리 표시자로 사용할 수 없습니다.
