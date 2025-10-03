---
title: 서버 설정 구성
description: 서버 설정 페이지에서는 이메일, 작업 알림, 관리자 알림 설정에 액세스할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 362b7b91-c58b-4e47-a6ef-56a4b54a100c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '2643'
ht-degree: 100%

---

# 서버 설정 구성 {#configuring-server-settings}

서버 설정 페이지에서는 Forms Workflow의 다양한 설정에 액세스할 수 있습니다.

* **이메일 설정**&#x200B;에서는 발신 이메일 메시지를 활성화하고 해당 메시지에 사용되는 이메일 서버 설정을 관리할 수 있습니다. ([이메일 설정 구성](configuring-server-settings.md#configuring-email-settings)을 참조하십시오.)
* **작업 알림 설정**&#x200B;에서는 작업과 관련하여 최종 사용자 및 그룹에게 이메일 알림으로 전송되는 메시지를 활성화, 비활성화 또는 수정합니다. ([사용자 및 그룹에 대한 알림 구성](configuring-server-settings.md#configuring-notifications-for-users-and-groups)을 참조하십시오.)
* **관리자 알림 설정**&#x200B;에서는 관리 작업에 대한 이메일 알림으로 전송되는 메시지를 활성화, 비활성화 또는 수정합니다. ([관리자에 대한 알림 구성](configuring-server-settings.md#configuring-notifications-for-administrators)을 참조하십시오.)

## 이메일 설정 구성 {#configuring-email-settings}

Forms 서버의 이메일 계정을 지정할 수 있으며, 해당 계정을 통해 AEM Forms 사용자와 관리자에게 이메일 메시지를 보냅니다. 이 이메일 메시지는 완료해야 하는 작업을 사용자에게 알리고 상기시키며, 기한이 도래한 작업을 사용자에게 알리고, 발생한 프로세스 오류를 관리자에게 알리는 데 사용됩니다.

AEM Forms와 사용자 간에 이메일 메시지를 보낼 수 있도록 하려면 이메일 설정 페이지에서 발신 이메일 설정을 구성합니다. 발신 이메일은 SMTP 서버를 사용해야 합니다.

AEM Forms가 사용자로부터 수신되는 이메일 메시지를 받고 처리할 수 있도록 하려면 작업 완료 서비스에 대한 이메일 엔드포인트를 만듭니다. ([작업 완료 서비스에 대한 이메일 엔드포인트 만들기](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)를 참조하십시오.)

이메일이 필요하지 않은 방식으로 프로세스를 설계하고 구현한 경우 이메일 설정 페이지에서 어떤 옵션도 구성할 필요가 없습니다.

### 발신 이메일 설정 구성 {#configure-outgoing-email-settings}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

1. 관리 콘솔에서 서비스 > Forms Workflow > 서버 설정 > 이메일 설정을 클릭합니다.
1. 발신 메시지 활성화를 선택합니다.
1. SMTP 서버 상자에 이메일 서버 이름이나 IP 주소를 입력합니다. Forms Workflow의 모든 알림 이메일 메시지는 이 이메일 서버에서 전송됩니다.
1. 사용자 이름 및 암호 상자에 SMTP 서버에서 인증을 요구할 때 사용할 로그인 이름과 암호를 입력합니다. 익명 로그인이 허용되는 경우에는 비워 두십시오.
1. 이메일 주소 상자에 Forms Workflow가 보내는 이메일 메시지의 반송 주소로 사용할 이메일 주소를 입력합니다.

   >[!NOTE]
   >
   >Microsoft Exchange Server를 사용하고 있고 이메일 주소가 잘못된 경우 Microsoft Exchange Server에서 배포 목록에 이메일을 보내지 못합니다. 이 문제를 해결하려면 Microsoft Exchange Server의 모든 배포 목록에 대해 별도로 **외부 통신 활성화** 옵션을 선택하십시오.

1. 저장을 클릭합니다.

>[!NOTE]
>
>잘못된 정보를 입력한 경우 취소를 클릭하면 이전에 표시된 페이지로 돌아갈 수 있습니다.

### AEM Forms Workspace를 사용하도록 이메일 템플릿 구성 {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>Flex Workspace는 AEM Forms 릴리스에서 더 이상 사용되지 않습니다.

기본적으로 AEM Forms에서 보낸 이메일에는 Flex Workspace(JEE의 AEM Forms에서는 더 이상 사용되지 않음) 링크가 포함되어 있습니다. AEM Forms Workspace 링크가 포함된 이메일을 보내도록 AEM Forms를 구성할 수 있습니다. Flex Workspace(JEE의 AEM Forms에서는 더 이상 사용되지 않음)와 비교했을 때 AEM Forms Workspace의 이점에 대해 자세히 알아보려면 [이](/help/forms/using/features-html-workspace-available-flex.md) 문서를 참조하십시오.

1. 관리 콘솔에서 홈 > 서비스 > Forms Workflow > 서버 설정 > 작업 알림을 클릭합니다.
1. 작업 할당 템플릿을 엽니다.
1. 작업 알림 템플릿을 다음과 같이 설정합니다. `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```java
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## 사용자 및 그룹에 대한 알림 구성 {#configuring-notifications-for-users-and-groups}

작업 알림 페이지에서 Forms Workflow가 사용자 및 그룹에게 전송되는 이메일 알림을 생성하는 데 사용할 템플릿을 구성할 수 있습니다. Forms Workflow 변수를 사용하여 알림을 사용자 정의하고 형식을 지정할 수 있습니다.

사용자 및 그룹에 대해 다음 유형의 알림을 구성합니다.

* 미리 알림
* 작업 할당
* 기한

그룹에 대한 이메일 알림을 생성하려면 사용자 관리에서 그룹의 이메일 주소를 지정합니다. <!--Fix broken link See Setting up and organizing users -->Forms Workflow에서 그룹에 이메일 알림을 보내면 이메일 주소가 지정된 그룹 내 각 멤버가 이메일 알림을 받습니다. 그룹 멤버가 이메일 알림을 받고 작업을 클레임하려면 이메일 알림에 있는 클레임 링크를 클릭해야 합니다. 그러면 Workspace에서 작업 세부 정보 페이지가 열립니다. 여기에서 멤버는 작업 항목을 클레임하거나 클레임하고 열 수 있습니다.

>[!NOTE]
>
>Flex Workspace는 AEM Forms 릴리스에서 더 이상 사용되지 않습니다.

### 사용자 또는 그룹에 대한 알림 구성 {#configure-reminders-for-users-or-groups}

작업 완료 기한이 다가오면 할당된 사용자 또는 그룹에 미리 알림을 보낼 수 있습니다. 미리 알림이 정확히 언제 전송되는지 결정하는 규칙은 프로세스 개발자가 결정합니다.

1. 관리 콘솔에서 서비스 > Forms Workflow > 서버 설정 > 작업 알림을 클릭합니다.
1. 알림 유형에서 미리 알림(사용자의 경우) 또는 그룹 - 미리 알림(그룹의 경우)을 클릭합니다.
1. 미리 알림 활성화 또는 그룹 - 미리 알림 활성화를 선택합니다.
1. (사용자 알림만 해당) 양식과 해당 데이터의 첨부 파일을 미리 알림 이메일 메시지에 포함하려면 양식 데이터 포함을 선택합니다.
1. 제목 상자에 이메일 메시지의 제목 줄에 사용할 텍스트를 입력합니다. 이 필드에는 기본 텍스트가 미리 채워져 있습니다. 이 필드를 사용자 정의하는 방법에 대한 자세한 내용은 [알림 내용 사용자 정의](configuring-server-settings.md#customizing-the-content-of-notifications)를 참조하십시오.
1. 알림 템플릿 상자에 이메일 메시지 본문에 사용할 텍스트를 입력합니다. 이 필드에는 기본 텍스트가 미리 채워져 있습니다. 이 필드를 사용자 정의하는 방법에 대한 자세한 내용은 [알림 내용 사용자 정의](configuring-server-settings.md#customizing-the-content-of-notifications)를 참조하십시오.
1. 메시지 형식 목록에서 HTML 또는 텍스트 중에서 이메일 메시지가 전송되는 형식을 선택합니다. 기본 형식은 HTML입니다.
1. 이메일 인코딩 목록에서 이메일 메시지에 사용할 인코딩 형식을 선택합니다. 기본값은 UTF-8이며, 일본 외 지역의 사용자 대부분이 해당 형식을 사용합니다. 일본 사용자는 ISO2022-JP를 선택할 수 있습니다.
1. 저장을 클릭합니다.

### 사용자 또는 그룹에 대한 작업 할당 알림 구성 {#configure-task-assignment-notifications-for-users-or-groups}

사용자 또는 그룹에 작업이 할당되면 해당 사용자 또는 그룹에 작업 할당 알림을 보낼 수 있습니다.

1. 관리 콘솔에서 서비스 > Forms Workflow > 서버 설정 > 작업 알림을 클릭합니다.
1. 알림 유형에서 사용자의 경우 작업 할당 또는 그룹의 경우 그룹 - 작업 할당을 클릭합니다.
1. 사용자의 경우 작업 할당 활성화, 그룹의 경우 그룹 - 작업 할당 활성화를 선택합니다.
1. (사용자 알림만 해당) 양식과 해당 데이터의 첨부 파일을 작업 할당 이메일 메시지에 포함하려면 양식 데이터 포함을 선택합니다.
1. 제목 상자에 이메일 메시지의 제목 줄에 사용할 텍스트를 입력합니다. 이 필드에는 기본 텍스트가 미리 채워져 있습니다. 이 필드를 사용자 정의하는 방법에 대한 자세한 내용은 [알림 내용 사용자 정의](configuring-server-settings.md#customizing-the-content-of-notifications)를 참조하십시오.
1. 알림 템플릿 상자에 이메일 메시지 본문에 사용할 텍스트를 입력합니다. 이 필드에는 기본 텍스트가 미리 채워져 있습니다. 이 필드를 사용자 정의하는 방법에 대한 자세한 내용은 [알림 내용 사용자 정의](configuring-server-settings.md#customizing-the-content-of-notifications)를 참조하십시오.
1. 메시지 형식 목록에서 HTML 또는 텍스트 중에서 이메일 메시지가 전송되는 형식을 선택합니다. 기본 형식은 HTML입니다.
1. 이메일 인코딩 목록에서 이메일 메시지에 사용할 인코딩 형식을 선택합니다. 기본값은 UTF-8이며, 일본 외 지역의 사용자 대부분이 해당 형식을 사용합니다. 일본 사용자는 ISO2022-JP를 선택할 수 있습니다.
1. 저장을 클릭합니다.

### 사용자 또는 그룹에 대한 기한 알림 구성 {#configure-deadline-notifications-for-users-or-groups}

할당된 작업에 대한 조치를 취해야 하는 기한이 지나면 사용자 및 그룹에 기한 알림을 보낼 수 있습니다. 기한 알림은 일반적으로 사용자가 더 이상 할당된 작업에 대한 조치를 취할 수 없기 때문에 정보 제공 목적으로 전송됩니다.

1. 관리 콘솔에서 서비스 > Forms Workflow > 서버 설정 > 작업 알림을 클릭합니다.
1. 알림 유형에서 기한(사용자의 경우) 또는 그룹 - 기한(그룹의 경우)을 클릭합니다.
1. 기한 활성화 또는 그룹 - 기한 활성화를 선택합니다.
1. 제목 상자에 이메일 메시지의 제목 줄에 사용할 텍스트를 입력합니다. 이 필드에는 기본 텍스트가 미리 채워져 있습니다. 이 필드를 사용자 정의하는 방법에 대한 자세한 내용은 [알림 내용 사용자 정의](configuring-server-settings.md#customizing-the-content-of-notifications)를 참조하십시오.
1. 알림 템플릿 상자에 이메일 메시지 본문에 사용할 텍스트를 입력합니다. 이 필드에는 기본 텍스트가 미리 채워져 있습니다. 이 필드를 사용자 정의하는 방법에 대한 자세한 내용은 [알림 내용 사용자 정의](configuring-server-settings.md#customizing-the-content-of-notifications)를 참조하십시오.
1. 메시지 형식 목록에서 HTML 또는 텍스트 중에서 이메일 메시지가 전송되는 형식을 선택합니다. 기본 형식은 HTML입니다.
1. 이메일 인코딩 목록에서 이메일 메시지에 사용할 인코딩 형식을 선택합니다. 기본값은 UTF-8이며, 일본 외 지역의 사용자 대부분이 해당 형식을 사용합니다. 일본 사용자는 ISO2022-JP를 선택할 수 있습니다.
1. 저장을 클릭합니다.

### 모든 이메일에서 삭제 금지 태그 숨기기 {#hide-the-do-not-delete-tag-for-all-emails}

사람 중심 프로세스를 통해 전송되는 모든 이메일에서 삭제 금지 추적 태그를 숨기도록 이메일을 구성할 수 있습니다.

<!-- 
For details, see [How to hide the 'DO-NOT-DELETE' tag with CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html) 
-->

## 관리자에 대한 알림 구성 {#configuring-notifications-for-administrators}

Forms Workflow가 관리자에게 전송되는 이메일 알림을 생성하는 데 사용할 템플릿을 구성할 수 있습니다.

관리자에 대해 다음 유형의 알림을 구성합니다.

* 중단된 분기
* 중단된 작업

### 중단된 분기 알림 구성 {#configure-stalled-branch-notifications}

분기가 중단되는 경우(의도적으로 또는 오류로 인해 진행이 중단되는 경우) 관리자나 다른 사용자에게 이메일 알림을 보내 문제를 조사할 수 있습니다.

1. 관리 콘솔에서 서비스 > Forms Workflow > 서버 설정 > 관리자 알림을 클릭합니다.
1. 알림 유형에서 중단된 분기를 클릭합니다.
1. 중단된 분기 활성화를 선택합니다.
1. 이메일 주소 상자에 분기가 중단될 때 알림을 받을 사용자의 주소를 입력합니다. user@domain.com 형식을 사용하고 각 주소를 쉼표로 구분합니다. 일반적으로 이 이메일 주소는 관리자를 위한 것입니다.
1. 제목 상자에 이메일 메시지의 제목 줄에 사용할 텍스트를 입력합니다. 이 필드에는 기본 텍스트가 미리 채워져 있습니다. 이 필드를 사용자 정의하는 방법에 대한 자세한 내용은 [알림 내용 사용자 정의](configuring-server-settings.md#customizing-the-content-of-notifications)를 참조하십시오.
1. 알림 템플릿 상자에 이메일 메시지 본문에 사용할 텍스트를 입력합니다. 이 필드에는 기본 텍스트가 미리 채워져 있습니다. 이 필드를 사용자 정의하는 방법에 대한 자세한 내용은 [알림 내용 사용자 정의](configuring-server-settings.md#customizing-the-content-of-notifications)를 참조하십시오.
1. 메시지 형식 목록에서 HTML 또는 텍스트 중에서 이메일 메시지가 전송되는 형식을 선택합니다. 기본 형식은 HTML입니다.
1. 이메일 인코딩 목록에서 이메일 메시지에 사용할 인코딩 형식을 선택합니다. 기본값은 UTF-8이며, 일본 외 지역의 사용자 대부분이 해당 형식을 사용합니다. 일본 사용자는 ISO2022-JP를 선택할 수 있습니다.
1. 저장을 클릭합니다.

### 중단된 작업 알림 구성 {#configure-stalled-operation-notifications}

작업이 중단되는 경우(의도적으로 또는 오류로 인해 진행이 중단되는 경우) 관리자나 다른 사용자에게 이메일 알림을 보내 문제를 조사할 수 있습니다.

1. 관리 콘솔에서 서비스 > Forms Workflow > 서버 설정 > 관리자 알림을 클릭합니다.
1. 알림 유형에서 중단된 작업을 클릭합니다.
1. 중단된 작업 활성화를 선택합니다.
1. 이메일 주소 상자에 작업이 중단될 때 알림을 받을 사용자의 주소를 입력합니다. user@domain.com 형식을 사용하고 각 주소를 쉼표로 구분합니다. 일반적으로 이 이메일 주소는 관리자를 위한 것입니다.
1. 제목 상자에 이메일 메시지의 제목 줄에 사용할 텍스트를 입력합니다. 이 필드에는 기본 텍스트가 미리 채워져 있습니다. 이 필드를 사용자 정의하는 방법에 대한 자세한 내용은 [알림 내용 사용자 정의](configuring-server-settings.md#customizing-the-content-of-notifications)를 참조하십시오.
1. 알림 템플릿 상자에 이메일 메시지 본문에 사용할 텍스트를 입력합니다. 이 필드에는 기본 텍스트가 미리 채워져 있습니다. 이 필드를 사용자 정의하는 방법에 대한 자세한 내용은 [알림 내용 사용자 정의](configuring-server-settings.md#customizing-the-content-of-notifications)를 참조하십시오.
1. 저장을 클릭합니다.

## 알림 내용 사용자 정의 {#customizing-the-content-of-notifications}

작업 알림 및 관리자 알림 페이지에서는 알림 메시지를 사용자 정의할 수 있는 다양한 기능을 제공합니다.

* 서식 있는 텍스트 편집기
* 변수 선택기
* URL 생성

### 서식 있는 텍스트 편집기 {#rich-text-editor}

알림 템플릿 영역은 이메일 알림 메시지에 대한 HTML을 생성할 수 있는 서식 있는 텍스트 편집기입니다. 알림 템플릿 상자 아래에서 글꼴 및 단락 서식 옵션을 제공합니다. 이 옵션에는 글꼴 유형, 크기, 스타일, 색상, 단락 맞춤 및 글머리 기호가 포함됩니다.

### URL 생성 {#url-generation}

작업 알림의 경우에만 Forms Workflow에는 미리 정의된 URL 구성 두 개가 포함되어 있으며, 해당 구성을 URL 생성 목록에서 알림 템플릿 상자로 끌어다 놓은 후 사용자 정의할 수 있습니다.

* OpenTask는 미리 알림 및 작업 할당 알림 유형에 사용할 수 있습니다. 이 URL은 Workspace의 작업 링크를 제공하므로 사용자는 이메일 알림을 통해 빠르게 작업에 액세스할 수 있습니다. OpenTask URL을 알림 템플릿 상자로 끌어다 놓으면 해당 URL은 다음과 같은 형식이 됩니다.

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask는 그룹 - 미리 알림 및 그룹 - 작업 할당 알림 유형에 사용할 수 있습니다. 이 URL은 Workspace의 작업 세부 정보 페이지 링크를 제공하며, 사용자는 여기서 작업 항목을 클레임하거나 클레임하고 열 수 있습니다. ClaimTask URL을 알림 템플릿 상자로 끌어다 놓으면 해당 URL은 다음과 같은 형식이 됩니다.

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>Flex Workspace는 AEM Forms 릴리스에서 더 이상 사용되지 않습니다.

솔루션이 클러스터링된 환경에 배포된 경우 `@@notification-host@@`를 클러스터 주소로 바꾸십시오.

`<`*PORT* `>`는 애플리케이션 서버에 대한 HTTP 리스너의 포트 번호입니다. 지원되는 애플리케이션 서버의 기본 HTTP 리스너 포트는 다음과 같습니다.

**JBoss:** 8080

**Oracle WebLogic Server:** 7001

**IBM WebSphere:** 9080

해당 URL이 올바르게 작동하려면 `<`*PORT* `>`를 사용자 환경에 적합한 포트 번호로 바꾸십시오.

>[!NOTE]
>
>사용자에게 작업에 대한 액세스 권한을 제공하기 위해 Forms가 아닌 사용자 정의 웹 애플리케이션을 사용하는 경우 대신 사용자 정의 애플리케이션에 적합한 URL 형식을 사용해야 합니다.

### 변수 선택기 {#variable-picker}

변수 선택기 목록에서는 제목이나 알림 템플릿 상자로 끌어다 놓을 수 있는 유용한 변수를 제공합니다. 제목이나 알림 템플릿 상자에 변수를 놓으면 해당 변수는 양쪽에 @ 기호 두 개가 붙은 실제 Forms Workflow 변수 이름으로 변경됩니다(예: `@@taskid@@`).

사용자 및 그룹에 대한 미리 알림, 작업 할당, 기한의 경우 제목 및 알림 템플릿 상자에서 다음 변수를 사용할 수 있습니다.

**설명**: 워크벤치 프로세스의 사용자 단계(시작 지점, 작업 할당 작업, 여러 작업 할당 작업)에 정의된 설명 속성의 내용입니다.

**지침**: 워크벤치 프로세스의 사용자 단계에서 정의된 작업 지침 속성의 내용입니다.

**notification-host**: AEM Forms 애플리케이션 서버의 호스트 이름입니다.

**process-name**: 프로세스 이름입니다.

**operation-name**: 단계 이름입니다.

**taskid**: 현재 작업에 대한 고유 식별자입니다.

**actions**: 수신자가 클릭할 수 있는 유효한 경로(예: 승인, 거부)에 번호를 매긴 목록을 생성합니다.

또한 그룹 미리 알림, 그룹 작업 할당, 그룹 기한의 경우 다음 항목을 사용할 수 있습니다.

**group-name**: 작업 항목이 할당된 그룹 이름입니다.

>[!NOTE]
>
>변수에 값이 없으면 아무것도 반환되지 않습니다.

중단된 분기의 경우 제목 및 알림 템플릿 상자에서 다음 변수를 사용할 수 있습니다.

**branch-id**: 분기 식별자입니다.

**process-id**: 프로세스 인스턴스 식별자입니다.

**notification-host**: AEM Forms 애플리케이션 서버의 호스트 이름입니다.

중단된 작업의 경우 제목 및 알림 템플릿 상자에서 다음 변수를 사용할 수 있습니다.

**action-id**: 작업 식별자입니다.

**branch-id**: 분기 식별자입니다.

**process-id**: 프로세스 인스턴스 식별자입니다.

**notification-host**: AEM Forms 애플리케이션 서버의 호스트 이름입니다.

### 제목 상자에 변수 사용 {#using-a-variable-in-the-subject-box}

작업 할당 알림의 제목 상자에 다음 텍스트를 입력하는 경우:

`Please complete task @@taskid@@`

사용자에게 작업 376이 할당되는 경우 사용자는 다음 제목의 이메일 메시지를 받습니다.

`Please complete task 376`

### 알림 템플릿 상자에서 변수 사용 {#using-variables-in-the-notification-template-box}

중단된 분기 알림의 알림 템플릿 상자에 다음 텍스트를 입력하는 경우:

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

분기 번호가 4868이고 서버 이름이 `ServerXYZ`인 경우 관리자는 다음 내용이 포함된 이메일 메시지를 받습니다.

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## 비즈니스 활동 모니터링 연결 구성 {#configuring-business-activity-monitoring-connections}

옵션 모듈로 제공되는 비즈니스 활동 모니터링은 운영 및 주요 성과 지표에 대한 실시간 가시성을 제공하는 일련의 운영 대시보드를 제공합니다.

BAM 구성 설정 페이지에서 BAM을 실행하는 서버에 대한 연결을 설정하면 프로세스 관련 이벤트를 추적하여 해당 서버로 전송할 수 있습니다.

1. 관리 콘솔에서 서비스 > Forms Workflow > 서버 설정 > BAM 구성 설정을 클릭합니다.
1. BAM 호스트 상자에 BAM을 실행하는 서버 이름을 입력합니다. 기본값은 localhost입니다.
1. BAM 포트 상자에 BAM을 실행하는 서버에 연결하는 데 사용할 포트를 입력합니다. JBoss의 기본 BAM 포트는 8080, WebLogic은 7001, WebSphere는 9080입니다.
1. 서버 호스트 상자에 호스트 Forms 서버 이름이나 IP 주소를 입력합니다. 기본값은 localhost입니다.
1. 서버 포트 상자에 Forms 서버에서 사용하는 포트 번호를 입력합니다.
1. 사용자 이름 및 암호 상자에 BAM 서버에 액세스하는 데 적합한 사용자 ID와 암호를 입력합니다. 기본 사용자 이름은 CognosNowAdmin이고 기본 암호는 manager입니다.
1. 저장을 클릭합니다.
