---
title: 서버 설정 구성
description: 서버 설정 페이지에서는 전자 메일, 작업 알림 및 관리자 알림 설정에 액세스할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 362b7b91-c58b-4e47-a6ef-56a4b54a100c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '2631'
ht-degree: 0%

---

# 서버 설정 구성 {#configuring-server-settings}

서버 설정 페이지에서는 Forms Workflow의 다양한 설정에 액세스할 수 있습니다.

* **이메일 설정** 보내는 이메일 메시지와 해당 메시지에 사용되는 이메일 서버 설정을 활성화합니다. (참조: [이메일 설정 구성](configuring-server-settings.md#configuring-email-settings).)
* **작업 알림 설정** 최종 사용자 및 그룹이 작업과 관련하여 이메일 알림으로 받은 메시지를 활성화, 비활성화 또는 수정합니다. (참조: [사용자 및 그룹에 대한 알림 구성](configuring-server-settings.md#configuring-notifications-for-users-and-groups).)
* **관리자 알림 설정** 관리 작업을 위해 이메일 알림으로 전송된 메시지를 활성화, 비활성화 또는 수정합니다. (참조: [관리자용 알림 구성](configuring-server-settings.md#configuring-notifications-for-administrators).)

## 이메일 설정 구성 {#configuring-email-settings}

AEM Forms 사용자 및 관리자에게 이메일 메시지를 보내는 Forms 서버에 대한 이메일 계정을 지정할 수 있습니다. 이러한 이메일 메시지는 사용자에게 완료해야 하는 작업을 알리고, 기한에 도달한 작업을 사용자에게 알리고, 발생하는 프로세스 오류를 관리자에게 알리는 데 사용됩니다.

AEM Forms와 사용자 간에 전자 메일 메시지를 보낼 수 있도록 하려면 전자 메일 설정 페이지에서 발신 전자 메일 설정을 구성합니다. 발신 전자 메일은 SMTP 서버를 사용해야 합니다.

AEM Forms가 사용자로부터 들어오는 이메일 메시지를 수신하고 처리할 수 있도록 하려면 전체 작업 서비스에 대한 이메일 엔드포인트를 만듭니다. (참조: [전체 작업 서비스에 대한 이메일 엔드포인트 만들기](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)).

이메일을 필요로 하지 않고 프로세스를 디자인하고 구현하는 경우 이메일 설정 페이지에서 옵션을 구성할 필요가 없습니다.

### 발신 이메일 설정 구성 {#configure-outgoing-email-settings}

1. 관리 콘솔에서 서비스 > 양식 워크플로우 > 서버 설정 > 이메일 설정 을 클릭합니다.
1. 발신 메시지 사용을 선택합니다.
1. SMTP 서버 상자에 전자 메일 서버 이름 또는 IP 주소를 입력합니다. 양식 워크플로우의 모든 알림 이메일 메시지가 이 이메일 서버에서 전송됩니다.
1. 사용자 이름 및 암호 상자에 SMTP 서버에 인증이 필요할 때 사용할 로그인 이름과 암호를 입력합니다. 익명 로그인이 허용되는 경우 비워 둡니다.
1. 전자 메일 주소 상자에 Forms 워크플로우에서 보내는 전자 메일 메시지의 반환 주소로 사용할 전자 메일 주소를 입력합니다.

   >[!NOTE]
   >
   >Microsoft Exchange Server를 사용 중이고 이메일 주소가 잘못된 경우, Microsoft Exchange Server는 메일 그룹으로 이메일을 보내지 못합니다. 문제를 해결하려면 다음을 선택합니다 **외부 통신 사용** 옵션은 Microsoft Exchange 서버의 모든 배포 목록에 대해 별도로 제공됩니다.

1. 저장을 클릭합니다.

>[!NOTE]
>
>잘못된 정보를 입력하면 취소 를 클릭하여 이전에 표시된 페이지로 돌아갈 수 있습니다.

### AEM Forms Workspace를 사용하도록 이메일 템플릿 구성 {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>Flex Workspace는 AEM Forms 릴리스에서 더 이상 사용되지 않습니다.

기본적으로 AEM Forms에 의해 전송되는 이메일에는 (JEE에서는 AEM Forms가 더 이상 사용되지 않음) Flex Workspace에 대한 링크가 포함되어 있습니다. AEM Forms Workspace에 대한 링크가 있는 이메일을 보내도록 AEM Forms를 구성할 수 있습니다. AEM Forms Workspace의 이점(JEE에서 AEM Forms의 더 이상 사용되지 않음)에 대해 자세히 알아보려면 Flex Workspace를 참조하십시오. [이](/help/forms/using/features-html-workspace-available-flex.md) 기사.

1. 관리 콘솔에서 홈 > 서비스 > 양식 워크플로우 > 서버 설정 > 작업 알림 을 클릭합니다.
1. 작업 할당 템플릿을 엽니다.
1. 작업 알림의 템플릿을 다음으로 설정합니다. `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```java
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## 사용자 및 그룹에 대한 알림 구성 {#configuring-notifications-for-users-and-groups}

작업 알림 페이지에서 Forms Workflow가 사용자 및 그룹에 전송되는 이메일 알림을 생성하는 데 사용할 템플릿을 구성할 수 있습니다. Forms 워크플로우 변수를 사용하여 알림을 사용자 지정하고 서식을 지정할 수 있습니다.

사용자 및 그룹에 대해 다음 유형의 알림을 구성합니다.

* 알림 메시지
* 작업 할당
* 기한

그룹에 대한 이메일 알림을 생성하려면 사용자 관리에서 그룹에 대한 이메일 주소를 지정합니다. <!--Fix broken link See Setting up and organizing users -->Forms Workflow가 그룹에 이메일 알림을 보내면 지정된 이메일 주소를 가진 그룹 내의 각 구성원이 이메일 알림을 받습니다. 그룹의 구성원이 이메일 알림을 받고 작업을 요청하려면 이메일 알림에서 요청 링크를 클릭해야 합니다. 그러면 작업 영역에서 작업 세부 정보 페이지가 열립니다. 그곳에서 구성원은 작업 항목에 대해 청구 또는 청구 및 열람할 수 있다.

>[!NOTE]
>
>Flex Workspace는 AEM Forms 릴리스에서 더 이상 사용되지 않습니다.

### 사용자 또는 그룹에 대한 미리 알림 구성 {#configure-reminders-for-users-or-groups}

작업 완료 기한이 다가오면 할당된 사용자 또는 그룹에 미리 알림을 보낼 수 있습니다. 미리 알림이 전송되는 정확한 시기를 결정하는 규칙은 프로세스 개발자가 결정합니다.

1. 관리 콘솔에서 서비스 > Forms 워크플로 > 서버 설정 > 작업 알림 을 클릭합니다.
1. 알림 유형에서 미리 알림(사용자용) 또는 그룹 - 미리 알림(그룹용)을 클릭합니다.
1. 미리 알림 활성화 또는 그룹 - 미리 알림 활성화를 선택합니다.
1. (사용자 알림만 해당) 미리 알림 이메일 메시지에 양식 및 해당 데이터의 첨부 파일을 포함하려면 양식 데이터 포함을 선택합니다.
1. 제목 상자에 전자 메일 메시지의 제목 줄에 대한 텍스트를 입력합니다. 이 필드는 기본 텍스트로 미리 채워집니다. 이 필드 사용자 지정에 대한 자세한 내용은 [알림 콘텐츠 사용자 지정](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 알림 템플릿 상자에 전자 메일 메시지 본문의 텍스트를 입력합니다. 이 필드는 기본 텍스트로 미리 채워집니다. 이 필드 사용자 지정에 대한 자세한 내용은 [알림 콘텐츠 사용자 지정](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 메시지 형식 목록에서 이메일 메시지가 전송되는 형식(HTML 또는 텍스트)을 선택합니다. 기본 형식은 HTML 입니다.
1. 전자 메일 인코딩 목록에서 전자 메일 메시지에 사용할 인코딩 형식을 선택합니다. 기본값은 UTF-8이며, 일본 이외의 대부분의 사용자는 이 옵션을 사용합니다. 일본의 사용자는 ISO2022-JP를 선택할 수 있습니다.
1. 저장을 클릭합니다.

### 사용자 또는 그룹에 대한 작업 할당 알림 구성 {#configure-task-assignment-notifications-for-users-or-groups}

사용자나 그룹에 작업이 할당되면 작업 할당 알림을 보낼 수 있습니다.

1. 관리 콘솔에서 서비스 > Forms 워크플로 > 서버 설정 > 작업 알림 을 클릭합니다.
1. 알림 유형에서 사용자에 대한 작업 할당 또는 그룹에 대한 그룹 - 그룹에 대한 작업 할당을 클릭합니다.
1. 사용자에 대해 작업 할당 활성화 또는 그룹에 대해 그룹 - 작업 할당 활성화를 선택합니다.
1. (사용자 알림만 해당) 작업 할당 전자 메일 메시지에 양식 및 해당 데이터의 첨부 파일을 포함하려면 양식 데이터 포함을 선택합니다.
1. 제목 상자에 전자 메일 메시지의 제목 줄에 대한 텍스트를 입력합니다. 이 필드는 기본 텍스트로 미리 채워집니다. 이 필드 사용자 지정에 대한 자세한 내용은 [알림 콘텐츠 사용자 지정](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 알림 템플릿 상자에 전자 메일 메시지 본문의 텍스트를 입력합니다. 이 필드는 기본 텍스트로 미리 채워집니다. 이 필드 사용자 지정에 대한 자세한 내용은 [알림 콘텐츠 사용자 지정](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 메시지 형식 목록에서 이메일 메시지가 전송되는 형식(HTML 또는 텍스트)을 선택합니다. 기본 형식은 HTML 입니다.
1. 전자 메일 인코딩 목록에서 전자 메일 메시지에 사용할 인코딩 형식을 선택합니다. 기본값은 UTF-8이며, 일본 이외의 대부분의 사용자는 이 옵션을 사용합니다. 일본의 사용자는 ISO2022-JP를 선택할 수 있습니다.
1. 저장을 클릭합니다.

### 사용자 또는 그룹에 대한 기한 알림 구성 {#configure-deadline-notifications-for-users-or-groups}

할당된 작업에 대한 작업 기한이 지나면 사용자와 그룹에 기한 알림을 보낼 수 있습니다. 사용자가 할당된 작업에 대해 더 이상 조치를 취할 수 없기 때문에 기한 알림은 일반적으로 정보 제공용입니다.

1. 관리 콘솔에서 서비스 > Forms 워크플로 > 서버 설정 > 작업 알림 을 클릭합니다.
1. 알림 유형에서 기한(사용자용) 또는 그룹 - 기한(그룹용)을 클릭합니다.
1. 기한 활성화 또는 그룹 - 기한 활성화를 선택합니다.
1. 제목 상자에 전자 메일 메시지의 제목 줄에 대한 텍스트를 입력합니다. 이 필드는 기본 텍스트로 미리 채워집니다. 이 필드 사용자 지정에 대한 자세한 내용은 [알림 콘텐츠 사용자 지정](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 알림 템플릿 상자에 전자 메일 메시지 본문의 텍스트를 입력합니다. 이 필드는 기본 텍스트로 미리 채워집니다. 이 필드 사용자 지정에 대한 자세한 내용은 [알림 콘텐츠 사용자 지정](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 메시지 형식 목록에서 이메일 메시지가 전송되는 형식(HTML 또는 텍스트)을 선택합니다. 기본 형식은 HTML 입니다.
1. 전자 메일 인코딩 목록에서 전자 메일 메시지에 사용할 인코딩 형식을 선택합니다. 기본값은 UTF-8이며, 일본 이외의 대부분의 사용자는 이 옵션을 사용합니다. 일본의 사용자는 ISO2022-JP를 선택할 수 있습니다.
1. 저장을 클릭합니다.

### 모든 이메일에 대해 DO NOT DELETE 태그 숨기기 {#hide-the-do-not-delete-tag-for-all-emails}

사람 중심 프로세스로 전송되는 모든 이메일에서 DO NOT DELETE 추적 태그로 숨기도록 이메일을 구성할 수 있습니다.

<!-- 
For details, see [How to hide the 'DO-NOT-DELETE' tag with CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html) 
-->

## 관리자용 알림 구성 {#configuring-notifications-for-administrators}

양식 워크플로우에서 관리자에게 전송되는 이메일 알림을 생성하는 데 사용할 템플릿을 구성할 수 있습니다.

관리자를 위해 다음 유형의 알림을 구성할 수 있습니다.

* 정지된 분기
* 정지된 작업

### 정지된 분기 알림 구성 {#configure-stalled-branch-notifications}

분기가 중단된 경우(고의 또는 오류로 인해 계속 진행되지 않음) 관리자나 다른 사용자에게 이메일 알림이 전송되어 문제를 조사할 수 있습니다.

1. 관리 콘솔에서 서비스 > Forms 워크플로 > 서버 설정 > 관리자 알림 을 클릭합니다.
1. 알림 유형에서 정지된 분기를 클릭합니다.
1. 정지된 분기 사용을 선택합니다.
1. 이메일 주소 상자에 분기가 중단될 때 통지할 사용자 주소를 입력합니다. user@domain.com 형식을 사용하고 각 주소는 쉼표로 구분하십시오. 일반적으로 이 이메일 주소는 관리자 전용입니다.
1. 제목 상자에 전자 메일 메시지의 제목 줄에 대한 텍스트를 입력합니다. 이 필드는 기본 텍스트로 미리 채워집니다. 이 필드 사용자 지정에 대한 자세한 내용은 [알림 콘텐츠 사용자 지정](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 알림 템플릿 상자에 전자 메일 메시지 본문의 텍스트를 입력합니다. 이 필드는 기본 텍스트로 미리 채워집니다. 이 필드 사용자 지정에 대한 자세한 내용은 [알림 콘텐츠 사용자 지정](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 메시지 형식 목록에서 이메일 메시지가 전송되는 형식(HTML 또는 텍스트)을 선택합니다. 기본 형식은 HTML 입니다.
1. 전자 메일 인코딩 목록에서 전자 메일 메시지에 사용할 인코딩 형식을 선택합니다. 기본값은 UTF-8로, 일본 이외의 대부분의 사용자가 사용합니다. 일본의 사용자는 ISO2022-JP를 선택할 수 있습니다.
1. 저장을 클릭합니다.

### 정지된 작업 알림 구성 {#configure-stalled-operation-notifications}

작업이 중단된 경우(의도적 또는 오류로 인해 계속 진행되지 않음) 관리자나 문제를 조사할 수 있는 다른 사용자에게 이메일 알림이 전송될 수 있습니다.

1. 관리 콘솔에서 서비스 > Forms 워크플로 > 서버 설정 > 관리자 알림 을 클릭합니다.
1. 알림 유형에서 정지된 작업 을 클릭합니다.
1. 정지된 작업 활성화를 선택합니다.
1. 이메일 주소 상자에 작업이 중지될 때 통지할 사용자 주소를 입력합니다. user@domain.com 형식을 사용하고 각 주소는 쉼표로 구분하십시오. 일반적으로 이 이메일 주소는 관리자 전용입니다.
1. 제목 상자에 전자 메일 메시지의 제목 줄에 대한 텍스트를 입력합니다. 이 필드는 기본 텍스트로 미리 채워집니다. 이 필드 사용자 지정에 대한 자세한 내용은 [알림 콘텐츠 사용자 지정](configuring-server-settings.md#customizing-the-content-of-notifications)
1. 알림 템플릿 상자에 전자 메일 메시지 본문의 텍스트를 입력합니다. 이 필드는 기본 텍스트로 미리 채워집니다. 이 필드 사용자 지정에 대한 자세한 내용은 [알림 콘텐츠 사용자 지정](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 저장을 클릭합니다.

## 알림 콘텐츠 사용자 지정 {#customizing-the-content-of-notifications}

작업 알림 및 관리자 알림 페이지에는 알림 메시지를 사용자 지정할 수 있는 몇 가지 기능이 있습니다.

* 리치 텍스트 편집기
* 변수 선택기
* URL 생성

### 리치 텍스트 편집기 {#rich-text-editor}

HTML 템플릿 영역은 이메일 알림 메시지에 대한 알림을 생성할 수 있는 리치 텍스트 편집기입니다. 또한 알림 템플릿 상자 아래에 있는 글꼴 및 단락 서식 옵션을 제공합니다. 옵션에는 글꼴 유형, 크기, 스타일 및 색상, 단락 정렬 및 글머리 기호가 포함됩니다.

### URL 생성 {#url-generation}

작업 알림의 경우에만 Forms 워크플로에 사전 정의된 두 개의 URL 구성이 포함됩니다. 이 구성을 Url 생성 목록에서 알림 템플릿 상자로 드래그한 다음 사용자 정의할 수 있습니다.

* OpenTask는 미리 알림 및 작업 할당 알림 유형에 사용할 수 있습니다. 이 URL은 Workspace의 작업에 대한 링크를 제공하여 사용자가 이메일 알림에서 작업에 빠르게 액세스할 수 있도록 합니다. OpenTask URL을 Notification Template 상자로 드래그하면 URL의 형식은 다음과 같습니다.

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask는 그룹 - 미리 알림 및 그룹 - 작업 할당 알림 유형에 사용할 수 있습니다. 이 URL은 사용자가 작업 항목을 클레임하거나 클레임 및 열 수 있는 작업 영역의 작업 세부 정보 페이지에 대한 링크를 제공합니다. ClaimTask URL을 Notification Template 상자로 드래그하면 URL의 형식은 다음과 같습니다.

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>Flex Workspace는 AEM Forms 릴리스에서 더 이상 사용되지 않습니다.

솔루션이 클러스터된 환경에 배포된 경우 `@@notification-host@@` 클러스터 주소입니다.

`<`*포트* `>` 는 응용 프로그램 서버에 대한 HTTP 리스너의 포트 번호입니다. 지원되는 애플리케이션 서버에 대한 기본 HTTP 리스너 포트는 다음과 같습니다.

**JBos:** 8080

**Oracle WebLogic 서버:** 7001

**IBM WebSphere** 9080

이러한 URL이 올바르게 작동하도록 하려면 `<`*포트* `>` 사용자 환경에 적합한 포트 번호 사용.

>[!NOTE]
>
>Forms 이외의 사용자 지정 웹 애플리케이션을 사용하여 사용자에게 작업에 대한 액세스 권한을 제공하는 경우 대신 사용자 지정 애플리케이션에 적합한 URL 형식을 사용해야 합니다.

### 변수 선택기 {#variable-picker}

변수 선택기 목록에서는 제목 또는 알림 템플릿 상자로 드래그하여 놓을 수 있는 유용한 변수를 제공합니다. 제목 또는 알림 템플릿 상자에 변수를 놓으면 실제 양식 워크플로 변수 이름으로 변경되고 양쪽에 두 개의 @ 기호가 표시됩니다. 예를 들면 다음과 같습니다. `@@taskid@@`.

사용자 및 그룹에 대한 미리 알림, 작업 할당 및 기한의 경우 제목 및 알림 템플릿 상자에서 다음 변수를 사용할 수 있습니다.

**설명** Workbench에서 프로세스의 사용자 단계(시작점, 작업 할당 작업 또는 여러 작업 할당 작업)에 정의된 설명 속성의 내용.

**지침** Workbench에서 프로세스의 사용자 단계에서 정의한 작업 지침 속성의 컨텐츠입니다.

**notification-host** AEM Forms 애플리케이션 서버 의 호스트 이름입니다.

**process-name** 프로세스의 이름입니다.

**operation-name** 단계의 이름입니다.

**taskid** 현재 작업의 고유 식별자입니다.

**작업** 수신자가 클릭할 수 있는 유효한 경로의 번호 매기기 목록(예: 승인, 거부)을 생성합니다.

또한 그룹 미리 알림, 그룹 작업 할당 및 그룹 기한의 경우 다음을 사용할 수도 있습니다.

**group-name** 작업 항목이 할당된 그룹의 이름입니다.

>[!NOTE]
>
>변수에 값이 없으면 아무 것도 반환되지 않습니다.

정지된 분기의 경우 제목 및 알림 템플릿 상자에서 다음 변수를 사용할 수 있습니다.

**branch-id** 분기 식별자.

**process-id** 프로세스 인스턴스 식별자.

**notification-host** AEM Forms 애플리케이션 서버 의 호스트 이름입니다.

정지된 작업의 경우 제목 및 알림 템플릿 상자에서 다음 변수를 사용할 수 있습니다.

**action-id** 작업 식별자.

**branch-id** 분기 식별자.

**process-id** 프로세스 인스턴스 식별자.

**notification-host** AEM Forms 애플리케이션 서버 의 호스트 이름입니다.

### 제목 상자에서 변수 사용 {#using-a-variable-in-the-subject-box}

태스크 지정 통지의 제목 상자에 다음 텍스트를 입력하는 경우

`Please complete task @@taskid@@`

사용자는 작업(376)이 할당된 경우 다음 주체가 포함된 이메일 메시지를 수신한다.

`Please complete task 376`

### 알림 템플릿 상자에서 변수 사용 {#using-variables-in-the-notification-template-box}

정지된 분기 통지에 대한 통지 템플리트 상자에 다음 텍스트를 입력하는 경우

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

지점 번호가 4868이고 서버 이름이 인 경우 관리자는 다음 콘텐츠가 포함된 이메일 메시지를 수신합니다. `ServerXYZ`:

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## Business Activity Monitoring 연결 구성 {#configuring-business-activity-monitoring-connections}

Business Activity Monitoring 은 선택적 모듈로, 운영 및 주요 성능 지표를 실시간으로 파악할 수 있는 운영 대시보드 세트를 제공합니다.

BAM 구성 설정 페이지에서는 프로세스 관련 이벤트를 추적하고 해당 서버로 전송할 수 있도록 BAM을 실행하는 서버에 대한 연결을 설정합니다.

1. 관리 콘솔에서 서비스 > Forms 워크플로 > 서버 설정 > BAM 구성 설정 을 클릭합니다.
1. BAM 호스트 상자에 BAM을 실행하는 서버의 이름을 입력합니다. 기본값은 localhost입니다.
1. BAM 포트 상자에 BAM을 실행하는 서버에 연결하는 데 사용할 포트를 입력합니다. JBoss의 기본 BAM 포트는 8080이고 WebLogic은 7001이며 WebSphere는 9080입니다.
1. 서버 호스트 상자에 호스트 Forms 서버의 이름 또는 IP 주소를 입력합니다. 기본값은 localhost입니다.
1. 서버 포트 상자에 Forms 서버에서 사용하는 포트 번호를 입력합니다.
1. 사용자 이름 및 암호 상자에 적절한 사용자 ID와 암호를 입력하여 BAM 서버에 액세스합니다. 기본 사용자 이름은 CognosNowAdmin이고 기본 암호는 manager입니다.
1. 저장을 클릭합니다.
