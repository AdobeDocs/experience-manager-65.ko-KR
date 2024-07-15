---
title: 작업 할당 단계에서 사용자 정의 이메일 템플릿 사용
description: 양식 워크플로우 이메일 알림에 대한 사용자 정의 이메일 템플릿
topic-tags: publish
docset: aem65
exl-id: d4035c91-ee8d-4f12-bdac-e3912be732d7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 1%

---

# 작업 할당 단계에서 사용자 정의 이메일 템플릿 사용{#use-custom-email-templates-in-an-assign-task-step}

작업 할당 단계를 사용하여 작업을 만들고 사용자 또는 그룹에 할당할 수 있습니다. 작업이 사용자 또는 그룹에 할당되면 정의된 사용자 또는 정의된 그룹의 각 구성원에게 이메일 알림이 전송됩니다. 일반적인 이메일 알림에는 할당된 작업의 링크 및 작업과 관련된 정보가 포함됩니다. 다음 이미지에는 샘플 이메일 알림이 표시됩니다.

![기본 제공 서식 파일이 포함된 전자 메일 알림](do-not-localize/default_email_template_new.png)

모양을 사용자 지정하고 이메일 알림에서 사용자 지정 메타데이터를 사용할 수 있습니다. AEM Forms에서는 이메일 알림에 대한 기본 제공 템플릿을 제공합니다. 기본 제공 템플릿을 사용자 정의하거나 템플릿을 처음부터 만들 수 있습니다.

전자 메일 알림 템플릿은 [HTML 전자 메일](https://en.wikipedia.org/wiki/HTML_email)을 기반으로 합니다. 이러한 이메일은 다양한 이메일 클라이언트와 화면 크기에 맞게 조정됩니다. 또한 이메일 스타일이 템플릿 내에서 정의됩니다.

다음 이미지는 사용자 지정된 이메일 알림을 표시합니다.

![사용자 지정 템플릿을 사용한 전자 메일 알림](do-not-localize/customized-email.png)

## 기존 템플릿 맞춤화 {#customize-the-existing-template}

AEM Forms에서는 이메일 알림용 템플릿을 기본적으로 제공합니다. 템플릿은 할당된 작업의 제목 설명, 기한, 우선 순위, 워크플로 이름 및 링크를 제공합니다. 템플릿을 사용자 정의하여 모양을 변경할 수 있습니다. 템플릿을 사용자 정의하려면 다음 단계를 수행하십시오.

1. 관리자 계정으로 CRXDE에 로그인합니다.

1. /libs/fd/dashboard/templates/email로 이동합니다.

1. htmlEmailTemplate.txt 파일을 엽니다. 여기에는 기본 템플릿이 포함되어 있습니다.

1. htmlEmailTemplate.txt 파일의 컨텐츠를 사용자 정의 컨텐츠로 바꿉니다.

   전자 메일 알림 템플릿이 [HTML 전자 메일](https://en.wikipedia.org/wiki/HTML_email)입니다. 기존 html 코드를 사용자 지정 코드로 대체하여 템플릿의 모양을 변경할 수 있습니다.

1. 파일을 저장합니다. 이제 사용자 지정된 템플릿을 사용할 준비가 되었습니다.

## 이메일 템플릿 만들기 {#create-an-email-template}

AEM Forms에서는 이메일 알림용 템플릿을 기본적으로 제공합니다. 템플릿은 할당된 작업의 제목 설명, 기한, 우선 순위, 워크플로 이름 및 링크를 제공합니다. 작업 단계 할당에 대한 사용자 지정 이메일 템플릿(자체 템플릿)을 추가할 수도 있습니다. 사용자 정의 이메일 템플릿을 추가하려면 다음 단계를 수행하십시오.

1. 관리자 계정으로 CRXDE에 로그인합니다.

1. /libs/fd/dashboard/templates/email로 이동합니다.

1. .txt 파일을 만듭니다. 예: EmailOnTaskAssign.txt

1. 사용자 지정 HTML 코드를 파일에 추가합니다.

   전자 메일 알림 템플릿이 [HTML 전자 메일](https://en.wikipedia.org/wiki/HTML_email)입니다. 파일에 사용자 지정 HTML 코드를 추가하여 템플릿을 만들 수 있습니다.

1. 파일을 저장합니다. 템플릿을 작업 할당 단계에서 사용할 준비가 되었습니다.

## 작업 할당 단계에서 이메일 템플릿 사용 {#use-an-email-template-in-an-assign-task-step}

기본적으로 작업 할당 단계는 기본 템플릿인 htmlEmailTemplate.txt를 사용하도록 구성됩니다. 사용자 지정 템플릿을 사용하도록 선택할 수 있습니다. 템플릿을 변경하려면 다음 작업을 수행하십시오.

1. 작업 할당 단계를 엽니다.

1. 담당자 > 이메일 템플릿 HTML 로 이동합니다.

1. 새로 만든 HTML 이메일 템플릿을 선택합니다.

1. 확인을 클릭합니다. 템플릿이 변경되었습니다.

전자 메일 알림도 [메타데이터](../../forms/using/use-metadata-in-email-notifications.md)를 사용합니다. 예를 들어 기한, 우선 순위, 워크플로우 이름 등이 있습니다. [사용자 지정 메타데이터](../../forms/using/use-metadata-in-email-notifications.md#using-custom-metadata-in-an-email-notification)를 사용하도록 템플릿을 구성할 수도 있습니다.
