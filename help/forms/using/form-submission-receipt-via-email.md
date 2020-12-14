---
title: 이메일을 통해 양식 제출 확인 보내기
seo-title: 이메일을 통해 양식 제출 확인 보내기
description: AEM Forms에서는 양식 제출 시 사용자에게 승인을 보내는 이메일 제출 작업을 구성할 수 있습니다.
seo-description: AEM Forms에서는 양식 제출 시 사용자에게 승인을 보내는 이메일 제출 작업을 구성할 수 있습니다.
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
translation-type: tm+mt
source-git-commit: acc2a3977353386d7e1dfd1344a61d78812fe3fc
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---


# 전자 메일 {#sending-a-form-submission-acknowledgement-via-email}을(를) 통해 양식 제출 확인 보내기

## 적응형 양식 데이터 제출 {#adaptive-form-data-submission}

적응형 양식은 여러 다른 끝점에 양식 데이터를 제출하기 위한 몇 가지 기본 [제출 작업](../../forms/using/configuring-submit-actions.md) 워크플로우를 제공합니다.

예를 들어 **[!UICONTROL 이메일]** 전송 작업은 적응형 양식을 성공적으로 제출할 때 이메일을 보냅니다. 양식 데이터와 이메일에 PDF를 보내도록 구성할 수도 있습니다.

이 문서에서는 적응형 양식과 제공된 다양한 구성에 대해 이메일 작업을 활성화하는 단계에 대해 자세히 설명합니다.

>[!NOTE]
>
>**[!UICONTROL 전자 메일]**&#x200B;을 통해 PDF 보내기 옵션을 사용하여 완료된 양식을 전자 메일로 PDF 첨부 파일로 보낼 수도 있습니다. 이 작업에 사용할 수 있는 구성 옵션은 **[!UICONTROL 이메일 보내기]** 작업에 사용할 수 있는 옵션과 동일합니다. 이메일 PDF 동작은 XFA 기반 적응형 양식에만 사용할 수 있습니다.

## 이메일 작업 {#email-action} 보내기

전자 메일 보내기 작업을 사용하면 작성자가 응용 양식을 성공적으로 제출할 때 하나 이상의 수신자에게 전자 메일을 자동으로 보낼 수 있습니다.

>[!NOTE]
>
>이메일 보내기 작업을 사용하려면 [메일 서비스 구성](/help/sites-administering/notification.md#configuring-the-mail-service)에 설명된 대로 AEM 메일 서비스를 구성해야 합니다.

### 응용 양식 {#enabling-email-action-on-an-adaptive-form}에 전자 메일 보내기 작업을 사용하도록 설정합니다.

1. **[!UICONTROL 편집]** 모드에서 응용 양식을 엽니다.

1. **[!UICONTROL 컨텐트]** 탭에서 **[!UICONTROL 양식 컨테이너]**&#x200B;를 누르고 ![구성](assets/configure-icon.svg)을 눌러 적응형 양식 속성을 봅니다.

1. **[!UICONTROL 제출]** 섹션의 **[!UICONTROL 제출 작업]** 드롭다운 목록에서 **[!UICONTROL 이메일]**&#x200B;을 선택합니다.

   ![작업 제출](assets/submission-actions.png)

1. **[!UICONTROL 받는 사람]**, **[!UICONTROL CC]** 및 **[!UICONTROL 숨은 참조]** 필드에 유효한 이메일 ID를 지정합니다.

   **[!UICONTROL 제목]** 및 **[!UICONTROL 이메일 템플릿]** 필드에 각각 이메일의 제목과 본문을 지정합니다.

   필드에 변수 자리 표시자를 지정할 수도 있습니다. 이 경우 최종 사용자가 양식을 성공적으로 제출할 때 필드 값이 처리됩니다. 자세한 내용은 [적응형 양식 필드 이름을 사용하여 이메일 컨텐츠](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p)를 동적으로 만들기를 참조하십시오.

   양식에 첨부 파일이 포함되어 있고 이러한 파일을 전자 메일에 첨부하려는 경우 **[!UICONTROL 첨부 파일 포함]**&#x200B;을 선택합니다.

   >[!NOTE]
   >
   >**[!UICONTROL 이메일을 통해 PDF 보내기]** 옵션을 선택하는 경우 첨부 파일 포함 옵션을 선택해야 합니다.

1. ![저장](assets/save_icon.svg)을 클릭하여 변경 내용을 저장합니다.

### 적응형 양식 필드 이름을 사용하여 이메일 컨텐츠 {#using-adaptive-form-field-names-to-dynamically-create-email-content}을(를) 동적으로 만들기

적응형 양식의 필드 이름은 사용자가 양식을 제출한 후 해당 필드의 값으로 대체되는 자리 표시자라고 합니다.

**[!UICONTROL 이메일 보내기]** 동작에서는 작업이 수행될 때 처리되는 자리 표시자를 사용할 수 있습니다. 이것은 사용자가 양식을 제출할 때 이메일의 헤더(예: **[!UICONTROL To]**, **[!UICONTROL CC]**, **[!UICONTROL BCC]**, **[!UICONTROL 제목]**)가 생성됨을 의미합니다.

자리 표시자를 정의하려면 **[!UICONTROL 이메일]**&#x200B;을 제출 작업으로 선택한 후 필드에 `${<field name>}`을 지정합니다.

예를 들어, 양식에 사용자의 이메일 ID를 캡처하기 위해 이름이 `email_addr`인 **[!UICONTROL 이메일 주소]** 필드가 포함되어 있는 경우 **[!UICONTROL 받는 사람]**, **[!UICONTROL CC]** 또는 **[!UICONTROL BCC]** 필드에서 다음 항목을 지정할 수 있습니다.

`${email_addr}`

사용자가 양식을 제출하면 양식의 `email_addr` 필드에 입력한 이메일 ID로 이메일이 전송됩니다.

>[!NOTE]
>
>필드의 **[!UICONTROL 편집]** 대화 상자에서 필드 이름을 찾을 수 있습니다.

변수 자리 표시자는 **[!UICONTROL 제목]** 및 **[!UICONTROL 이메일 템플릿]** 필드에서도 사용할 수 있습니다.

예:

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>반복 가능한 패널의 필드는 변수 자리 표시자로 사용할 수 없습니다.

