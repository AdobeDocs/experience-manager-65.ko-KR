---
title: 작업 할당 단계에서 사용자 지정 이메일 템플릿 사용
seo-title: 작업 할당 단계에서 사용자 지정 이메일 템플릿 사용
description: '양식 워크플로우 이메일 알림을 위한 사용자 정의 이메일 템플릿 '
seo-description: '양식 워크플로우 이메일 알림을 위한 사용자 정의 이메일 템플릿 '
uuid: ba453d54-813f-4a4f-a82e-1a6a28b6939c
topic-tags: publish
discoiquuid: 2ad4b7b5-2162-4599-af3f-9476f1256de6
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---


# 작업 할당 단계{#use-custom-email-templates-in-an-assign-task-step}에서 사용자 지정 이메일 템플릿 사용

작업 지정 단계를 사용하여 작업을 만들고 사용자 또는 그룹에 지정할 수 있습니다. 작업이 사용자 또는 그룹에 할당되면 정의된 사용자 또는 정의된 그룹의 각 구성원에게 이메일 알림이 전송됩니다. 일반적인 이메일 알림은 할당된 작업의 링크 및 작업과 관련된 정보를 포함합니다. 다음 이미지는 샘플 이메일 알림을 표시합니다.

![즉시 사용 가능한 템플릿으로 이메일 알림](do-not-localize/default_email_template_new.png)

모양을 사용자 정의하고 이메일 알림에 사용자 지정 메타데이터를 사용할 수 있습니다. AEM Forms은 이메일 알림에 대한 특별 템플릿을 제공합니다. 기본 템플릿을 사용자 정의하거나 처음부터 새 템플릿을 만들 수 있습니다.

이메일 알림 템플릿은 [HTML 이메일](https://en.wikipedia.org/wiki/HTML_email)을 기반으로 합니다. 이러한 이메일은 서로 다른 이메일 클라이언트와 화면 크기에 맞게 조정됩니다. 또한 이메일의 스타일이 템플릿 내에 정의됩니다.

다음 이미지는 사용자 지정된 이메일 알림을 표시합니다.

![사용자 지정 템플릿을 사용한 이메일 알림](do-not-localize/customized-email.png)

## 기존 템플릿 {#customize-the-existing-template} 사용자 지정

즉시 사용 가능한 AEM Forms은 이메일 알림에 대한 템플릿을 제공합니다. 템플릿은 할당된 작업의 제목 설명, 기한, 우선순위, 워크플로우 이름 및 링크를 제공합니다. 템플릿을 사용자 지정하여 모양을 변경할 수 있습니다. 템플릿을 사용자 정의하려면 다음 단계를 수행합니다.

1. 관리자 계정으로 CRXDE에 로그인합니다.

1. /libs/fd/dashboard/templates/email로 이동합니다.

1. htmlEmailTemplate.txt 파일을 엽니다. 기본 템플릿이 포함되어 있습니다.

1. htmlEmailTemplate.txt 파일의 컨텐츠를 사용자 정의 내용으로 바꿉니다.

   이메일 알림 템플릿은 [HTML 이메일](https://en.wikipedia.org/wiki/HTML_email)입니다. 기존 html 코드를 사용자 지정 코드로 변경하여 템플릿의 모양을 변경할 수 있습니다.

1. 파일을 저장합니다. 이제 사용자 지정된 템플릿을 사용할 수 있습니다.

## 이메일 템플릿 {#create-an-email-template} 만들기

즉시 사용 가능한 AEM Forms은 이메일 알림에 대한 템플릿을 제공합니다. 템플릿은 할당된 작업의 제목 설명, 기한, 우선순위, 워크플로우 이름 및 링크를 제공합니다. 할당 작업 단계에 대한 사용자 지정 이메일 템플릿(사용자 지정 템플릿)을 추가할 수도 있습니다. 사용자 지정 이메일 템플릿을 추가하려면 다음 단계를 수행하십시오.

1. 관리자 계정으로 CRXDE에 로그인합니다.

1. /libs/fd/dashboard/templates/email로 이동합니다.

1. .txt 파일을 만듭니다. 예: EmailOnTaskAssign.txt.

1. 파일에 사용자 정의 HTML 코드를 추가합니다.

   이메일 알림 템플릿은 [HTML 이메일](https://en.wikipedia.org/wiki/HTML_email)입니다. 파일에 사용자 지정 HTML 코드를 추가하여 새 템플릿을 만들 수 있습니다.

1. 파일을 저장합니다. 템플릿이 작업 지정 단계에서 사용할 준비가 되었습니다.

## 작업 할당 단계 {#use-an-email-template-in-an-assign-task-step}에서 이메일 템플릿 사용

기본 템플릿인 htmlEmailTemplate.txt를 사용하도록 할당 작업 단계가 구성되어 있습니다. 사용자 지정 템플릿을 사용하도록 선택할 수 있습니다. 템플릿을 변경하려면 다음을 수행하십시오.

1. 작업 지정 단계를 엽니다.

1. 할당자 > HTML 이메일 템플릿으로 이동합니다.

1. 새로 만든 HTML 이메일 템플릿을 선택합니다.

1. 확인을 클릭합니다. 템플릿이 변경되었습니다.

이메일 알림은 또한 [metadata](../../forms/using/use-metadata-in-email-notifications.md)를 사용합니다. 기한, 우선 순위, 워크플로우 이름 등과 같은 작업을 수행할 수 있습니다. [사용자 지정 메타데이터](../../forms/using/use-metadata-in-email-notifications.md#using-custom-metadata-in-an-email-notification)를 사용하도록 템플릿을 구성할 수도 있습니다.
