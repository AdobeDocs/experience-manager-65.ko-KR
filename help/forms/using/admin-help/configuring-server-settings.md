---
title: 서버 설정 구성
seo-title: 서버 설정 구성
description: '[서버 설정] 페이지에서는 이메일, 작업 알림 및 관리자 알림 설정에 대한 액세스 권한을 제공합니다.'
seo-description: '[서버 설정] 페이지에서는 이메일, 작업 알림 및 관리자 알림 설정에 대한 액세스 권한을 제공합니다.'
uuid: 73b51ac0-56e5-4748-bb33-e3986c69eb2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e047a95e-0acb-438a-8d27-f005c0adc508
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2657'
ht-degree: 0%

---


# 서버 설정 구성 {#configuring-server-settings}

[서버 설정] 페이지에서는 양식 워크플로우에 대한 다양한 설정에 액세스할 수 있습니다.

* **발신** 이메일 메시지를 활성화하는 이메일 설정과 해당 메시지에 사용된 이메일 서버 설정이 포함되어 있습니다. ([이메일 설정 구성](configuring-server-settings.md#configuring-email-settings)을 참조하십시오.)
* **최종** 사용자 및 그룹에 보낸 작업과 관련된 메시지를 활성화, 비활성화 또는 수정하는 작업 알림 설정 ([사용자 및 그룹에 대한 알림 구성](configuring-server-settings.md#configuring-notifications-for-users-and-groups)을 참조하십시오.)
* **관리** 작업을 위해 이메일 알림으로 보낸 메시지를 활성화, 비활성화 또는 수정하는 관리자 알림 설정 (관리자[에 대한 알림 구성을 참조하십시오.)](configuring-server-settings.md#configuring-notifications-for-administrators)

## 이메일 설정 구성 {#configuring-email-settings}

AEM Forms 사용자 및 관리자에게 이메일 메시지를 보내는 양식 서버의 이메일 계정을 지정할 수 있습니다. 이러한 이메일 메시지는 완료해야 하는 작업을 사용자에게 알리고 사용자에게 마감 시간에 도달한 작업을 알려주고 관리자에게 프로세스 오류가 발생하는지 알려주는 데 사용됩니다.

AEM 양식과 사용자 간 이메일 메시지 전송을 활성화하려면 이메일 설정 페이지에서 발신 이메일 설정을 구성합니다. 보내는 전자 메일은 SMTP 서버를 사용해야 합니다.

AEM 양식에서 사용자의 수신 이메일 메시지를 수신하고 처리하려면 전체 작업 서비스에 대한 이메일 끝점을 만듭니다. ([전체 작업 서비스](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)에 대한 이메일 끝점 만들기를 참조하십시오.)

이메일 없이도 프로세스를 설계 및 구현한 경우 이메일 설정 페이지에서 옵션을 구성할 필요가 없습니다.

### 나가는 이메일 설정 구성 {#configure-outgoing-email-settings}

1. 관리 콘솔에서 서비스 > 양식 워크플로우 > 서버 설정 > 이메일 설정을 클릭합니다.
1. 발신 메시지 활성화를 선택합니다.
1. SMTP 서버 상자에 이메일 서버 이름 또는 IP 주소를 입력합니다. 양식 워크플로우의 모든 알림 이메일 메시지는 이 이메일 서버에서 전송됩니다.
1. 사용자 이름 및 암호 상자에 SMTP 서버에 인증이 필요한 경우 사용할 로그인 이름과 암호를 입력합니다. 익명 로그인이 허용되는 경우 비워 둡니다.
1. [이메일 주소] 상자에 양식 워크플로우가 보내는 이메일 메시지의 회신 주소로 사용할 이메일 주소를 입력합니다.

   >[!NOTE]
   >
   >Microsoft Exchange Server를 사용하고 있지만 전자 메일 주소가 잘못된 전자 메일 주소인 경우 Microsoft Exchange 서버에서 배포 목록에 전자 메일을 보내지 못합니다. 이 문제를 해결하려면 Microsoft Exchange 서버의 모든 배포 목록에 대해 별도로 **외부 통신 활성화** 옵션을 선택하십시오.

1. 저장을 클릭합니다.

>[!NOTE]
>
>잘못된 정보를 입력할 경우 취소를 클릭하여 이전에 표시된 페이지로 돌아갈 수 있습니다.

### AEM Forms 작업 공간 {#configuring-email-templates-to-use-html-workspace}을(를) 사용하도록 이메일 템플릿 구성

>[!NOTE]
>
>Flex 작업 공간은 AEM 양식 릴리스에서 더 이상 사용되지 않습니다.

기본적으로 AEM 양식에 의해 전송된 이메일에는 Flex 작업 공간에 대한 링크(JEE에서 AEM 양식에 대해 더 이상 사용되지 않음)가 포함됩니다. AEM Forms 작업 공간에 대한 링크가 포함된 이메일을 보내도록 AEM 양식을 구성할 수 있습니다. Flex 작업 공간에 대한 이점(JEE에서 AEM 양식에 대해 더 이상 사용되지 않음) AEM Forms 작업 공간에 대한 자세한 내용은 [이](/help/forms/using/features-html-workspace-available-flex.md) 문서를 참조하십시오.

1. 관리 콘솔에서 홈 > 서비스 > 양식 워크플로우 > 서버 설정 > 작업 알림을 클릭합니다.
1. 작업 할당 템플릿을 엽니다.
1. 작업 알림의 템플릿을 다음과 같이 설정합니다.`https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```java
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## 사용자 및 그룹에 대한 알림 구성 {#configuring-notifications-for-users-and-groups}

작업 알림 페이지에서, 양식 워크플로우가 사용자 및 그룹에 전송되는 이메일 알림을 생성하는 데 사용할 템플릿을 구성할 수 있습니다. 양식 워크플로우 변수를 사용하여 알림을 사용자 정의하고 서식을 지정할 수 있습니다.

사용자 및 그룹에 대해 다음 유형의 알림을 구성합니다.

* 미리 알림
* 작업 할당
* 최종 기한

그룹에 대한 이메일 알림을 생성하려면 [사용자 관리]에서 그룹의 이메일 주소를 지정합니다. <!--Fix broken link See Setting up and organizing users -->양식 워크플로우가 그룹에 이메일 알림을 전송하면 지정된 이메일 주소가 있는 그룹 내의 각 구성원이 이메일 알림을 받게 됩니다. 그룹 구성원이 이메일 알림을 받고 작업을 요청하려는 경우, 구성원은 이메일 알림의 청구 링크를 클릭해야 합니다. 그러면 작업 공간에서 작업 세부 사항 페이지가 열립니다. 여기서 회원은 요청하거나 요청하고 작업 항목을 열 수 있습니다.

>[!NOTE]
>
>Flex 작업 영역은 AEM 양식 릴리스에서 더 이상 사용되지 않습니다.

### 사용자 또는 그룹에 대한 미리 알림 구성 {#configure-reminders-for-users-or-groups}

작업 완료 기한이 다가오면 지정된 사용자 또는 그룹에 알림 메시지를 보낼 수 있습니다. 미리 알림 전송 시점을 정확하게 결정하는 규칙은 프로세스 개발자가 결정합니다.

1. 관리 콘솔에서 서비스 > Forms 워크플로우 > 서버 설정 > 작업 알림을 클릭합니다.
1. 알림 유형에서 미리 알림(사용자용) 또는 그룹 - 미리 알림(그룹용)을 클릭합니다.
1. 미리 알림 활성화 또는 그룹 - 미리 알림 활성화를 선택합니다.
1. (사용자 알림만 해당) 양식 및 해당 데이터의 첨부 파일을 미리 알림 이메일 메시지와 함께 포함하려면 양식 데이터 포함을 선택합니다.
1. 제목 상자에 이메일 메시지의 제목 줄에 대한 텍스트를 입력합니다. 이 필드는 기본 텍스트로 미리 채워집니다. 이 필드 사용자 지정에 대한 자세한 내용은 [알림 내용 사용자 지정을 참조하십시오](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 알림 템플릿 상자에 이메일 메시지 본문에 대한 텍스트를 입력합니다. 이 필드는 기본 텍스트로 미리 채워집니다. 이 필드 사용자 지정에 대한 자세한 내용은 [알림 내용 사용자 지정을 참조하십시오](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 메시지 형식 목록에서 이메일 메시지가 전송되는 형식(HTML 또는 텍스트)을 선택합니다. 기본 형식은 HTML입니다.
1. [이메일 인코딩] 목록에서 이메일 메시지에 사용할 인코딩 형식을 선택합니다. 기본값은 UTF-8로, 일본 이외의 다른 사용자가 사용합니다. 일본 사용자는 ISO2022-JP를 선택할 수 있습니다.
1. 저장을 클릭합니다.

### 사용자 또는 그룹 {#configure-task-assignment-notifications-for-users-or-groups}에 대한 작업 할당 알림 구성

작업이 할당되면 사용자 또는 그룹에 작업 할당 알림을 보낼 수 있습니다.

1. 관리 콘솔에서 서비스 > Forms 워크플로우 > 서버 설정 > 작업 알림을 클릭합니다.
1. 알림 유형에서 사용자 또는 그룹에 대한 그룹 - 작업 할당을 클릭합니다.
1. 사용자에 대해 작업 할당 활성화 또는 그룹에 대해 그룹 - 작업 할당 활성화를 선택합니다.
1. (사용자 알림만 해당) 양식 및 해당 데이터의 첨부 파일을 작업 할당 이메일 메시지와 함께 포함하려면 양식 데이터 포함을 선택합니다.
1. 제목 상자에 이메일 메시지의 제목 줄에 대한 텍스트를 입력합니다. 이 필드는 기본 텍스트로 미리 채워집니다. 이 필드 사용자 지정에 대한 자세한 내용은 [알림 내용 사용자 지정을 참조하십시오](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 알림 템플릿 상자에 이메일 메시지 본문에 대한 텍스트를 입력합니다. 이 필드는 기본 텍스트로 미리 채워집니다. 이 필드 사용자 지정에 대한 자세한 내용은 [알림 내용 사용자 지정을 참조하십시오](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 메시지 형식 목록에서 이메일 메시지가 전송되는 형식(HTML 또는 텍스트)을 선택합니다. 기본 형식은 HTML입니다.
1. [이메일 인코딩] 목록에서 이메일 메시지에 사용할 인코딩 형식을 선택합니다. 기본값은 UTF-8로, 일본 이외의 다른 사용자가 사용합니다. 일본 사용자는 ISO2022-JP를 선택할 수 있습니다.
1. 저장을 클릭합니다.

### 사용자 또는 그룹 {#configure-deadline-notifications-for-users-or-groups} 최종 기한 알림 구성

지정된 작업에 대한 작업 기한이 경과하면 최종 기한 알림을 사용자 및 그룹에 보낼 수 있습니다. 사용자가 지정된 작업에 더 이상 응답하지 않기 때문에 일반적으로 마감 알림 메시지는 정보 제공용입니다.

1. 관리 콘솔에서 서비스 > Forms 워크플로우 > 서버 설정 > 작업 알림을 클릭합니다.
1. 알림 유형에서 마감 시간(사용자) 또는 그룹 - 최종 기한(그룹)을 클릭합니다.
1. 마감 시간 활성화 또는 그룹 활성화 - 마감일을 선택합니다.
1. 제목 상자에 이메일 메시지의 제목 줄에 대한 텍스트를 입력합니다. 이 필드는 기본 텍스트로 미리 채워집니다. 이 필드 사용자 지정에 대한 자세한 내용은 [알림 내용 사용자 지정을 참조하십시오](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 알림 템플릿 상자에 이메일 메시지 본문에 대한 텍스트를 입력합니다. 이 필드는 기본 텍스트로 미리 채워집니다. 이 필드 사용자 지정에 대한 자세한 내용은 [알림 내용 사용자 지정을 참조하십시오](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 메시지 형식 목록에서 이메일 메시지가 전송되는 형식(HTML 또는 텍스트)을 선택합니다. 기본 형식은 HTML입니다.
1. [이메일 인코딩] 목록에서 이메일 메시지에 사용할 인코딩 형식을 선택합니다. 기본값은 UTF-8로, 일본 이외의 다른 사용자가 사용합니다. 일본 사용자는 ISO2022-JP를 선택할 수 있습니다.
1. 저장을 클릭합니다.

### 모든 이메일 {#hide-the-do-not-delete-tag-for-all-emails}에 대한 DO NOT DELETE 태그 숨기기

인간 중심 프로세스로 전송되는 모든 이메일의 DO NOT DELETE 추적 태그에 숨기도록 이메일을 구성할 수 있습니다. 자세한 내용은 [CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html)를 사용하여 &#39;DO-NOT-DELETE&#39; 태그를 숨기는 방법을 참조하십시오.

## 관리자에 대한 알림 구성{#configuring-notifications-for-administrators}

양식 워크플로우에서 관리자에게 전송되는 이메일 알림을 생성하는 데 사용할 템플릿을 구성할 수 있습니다.

관리자를 위한 다음 유형의 알림을 구성합니다.

* 막힌 나뭇가지
* 정지 작전

### 중단된 분기 알림 {#configure-stalled-branch-notifications} 구성

분기가 중단(의도적 또는 오류로 인해 진행 중단)하는 경우, 관리자나 다른 사용자에게 이메일 알림을 전송하면 해당 관리자가 문제를 조사할 수 있습니다.

1. 관리 콘솔에서 서비스 > Forms 워크플로우 > 서버 설정 > 관리자 알림을 클릭합니다.
1. 알림 유형에서 중단된 분기를 클릭합니다.
1. [중단된 분기 활성화]를 선택합니다.
1. [이메일 주소] 상자에 분기가 정지될 때 알릴 사용자의 주소를 입력합니다. user@domain.com 형식을 사용하고 각 주소를 쉼표로 구분합니다. 일반적으로 이 이메일 주소는 관리자용입니다.
1. 제목 상자에 이메일 메시지의 제목 줄에 대한 텍스트를 입력합니다. 이 필드는 기본 텍스트로 미리 채워집니다. 이 필드 사용자 지정에 대한 자세한 내용은 [알림 내용 사용자 지정을 참조하십시오](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 알림 템플릿 상자에 이메일 메시지 본문에 대한 텍스트를 입력합니다. 이 필드는 기본 텍스트로 미리 채워집니다. 이 필드 사용자 지정에 대한 자세한 내용은 [알림 내용 사용자 지정을 참조하십시오](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 메시지 형식 목록에서 이메일 메시지가 전송되는 형식(HTML 또는 텍스트)을 선택합니다. 기본 형식은 HTML입니다.
1. [이메일 인코딩] 목록에서 이메일 메시지에 사용할 인코딩 형식을 선택합니다. 기본값은 UTF-8로, 대부분의 일본 이외의 사용자가 사용합니다. 일본 사용자는 ISO2022-JP를 선택할 수 있습니다.
1. 저장을 클릭합니다.

### 중단된 작업 알림 {#configure-stalled-operation-notifications} 구성

작업이 중단(의도적 또는 오류로 인해 진행 중단)되면 관리자나 다른 사용자에게 이메일 알림을 전송하여 문제를 조사할 수 있습니다.

1. 관리 콘솔에서 서비스 > Forms 워크플로우 > 서버 설정 > 관리자 알림을 클릭합니다.
1. 알림 유형에서 중단 작업을 클릭합니다.
1. 중단된 작업 활성화를 선택합니다.
1. [이메일 주소] 상자에 작업이 중단되면 알릴 사용자의 주소를 입력합니다. user@domain.com 형식을 사용하고 각 주소를 쉼표로 구분합니다. 일반적으로 이 이메일 주소는 관리자용입니다.
1. 제목 상자에 이메일 메시지의 제목 줄에 대한 텍스트를 입력합니다. 이 필드는 기본 텍스트로 미리 채워집니다. 이 필드 사용자 지정에 대한 자세한 내용은 [알림 내용 사용자 지정을 참조하십시오.](configuring-server-settings.md#customizing-the-content-of-notifications)
1. 알림 템플릿 상자에 이메일 메시지 본문에 대한 텍스트를 입력합니다. 이 필드는 기본 텍스트로 미리 채워집니다. 이 필드 사용자 지정에 대한 자세한 내용은 [알림 내용 사용자 지정을 참조하십시오](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 저장을 클릭합니다.

## 알림 내용 사용자 지정 {#customizing-the-content-of-notifications}

[작업 알림] 및 [관리자 알림] 페이지에서는 알림 메시지를 사용자 정의할 수 있는 여러 가지 기능을 제공합니다.

* 리치 텍스트 편집기
* 변수 선택기
* URL 생성

### 리치 텍스트 편집기 {#rich-text-editor}

알림 템플릿 영역은 이메일 알림 메시지에 대한 HTML을 생성할 수 있는 리치 텍스트 편집기입니다. 글꼴 및 단락 서식 지정 옵션은 알림 템플릿 상자 아래에 있습니다. 이 옵션에는 글꼴 유형, 크기, 스타일, 색상, 단락 정렬 및 글머리 기호가 포함됩니다.

### URL 생성 {#url-generation}

작업 알림의 경우, Forms 워크플로우에는 [URL 생성] 목록에서 [알림 템플릿] 상자로 드래그한 다음 사용자 지정할 수 있는 두 개의 사전 정의된 URL 구성이 포함되어 있습니다.

* OpenTask는 미리 알림 및 작업 할당 알림 유형에 사용할 수 있습니다. 이 URL은 작업 공간의 작업에 대한 링크를 제공하므로 사용자는 이메일 알림에서 작업에 빠르게 액세스할 수 있습니다. OpenTask URL을 알림 템플릿 상자로 드래그하면 URL은 다음과 같은 형식으로 표시됩니다.

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask는 그룹 - 미리 알림 및 그룹 - 작업 지정 통지 유형에 사용할 수 있습니다. 이 URL은 사용자가 작업 항목을 요청하거나 요청하고 열 수 있는 작업 공간의 작업 세부 사항 페이지에 대한 링크를 제공합니다. ClaimTask URL을 알림 템플릿 상자로 드래그하면 URL의 형식은 다음과 같습니다.

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>Flex 작업 영역은 AEM 양식 릴리스에서 더 이상 사용되지 않습니다.

솔루션이 클러스터된 환경에 배포된 경우 `@@notification-host@@`을(를) 클러스터 주소로 교체하십시오.

`<`*포트* `>` 는 응용 프로그램 서버에 대한 HTTP 수신기의 포트 번호입니다. 지원되는 응용 프로그램 서버에 대한 기본 HTTP 수신기 포트는 다음과 같습니다.

**JBoss:** 8080

**Oracle WebLogic Server:** 7001

**IBM WebSphere:** 9080

이러한 URL이 올바르게 작동하도록 하려면 `<`*PORT* `>`를 환경에 적합한 포트 번호로 바꿉니다.

>[!NOTE]
>
>Forms 이외의 사용자 지정 웹 응용 프로그램을 사용하여 사용자에게 작업에 대한 액세스 권한을 제공하는 경우 사용자 지정 응용 프로그램에 적합한 URL 형식을 대신 사용해야 합니다.

### 변수 선택기 {#variable-picker}

변수 선택기 목록은 제목 또는 알림 템플릿 상자로 드래그하여 놓을 수 있는 유용한 변수를 제공합니다. [제목] 또는 [알림 템플릿] 상자에 변수를 놓으면 실제 양식 워크플로우 변수 이름에 두 개의 @ 기호가 있고(예: `@@taskid@@`) 양쪽에 변경됩니다.

사용자 및 그룹에 대한 미리 알림, 작업 할당 및 마감일 등의 경우 [제목] 및 [알림 템플릿] 상자에 다음 변수를 사용할 수 있습니다.

**설명** 워크벤치의 프로세스 사용자 단계(시작점, 작업 할당 작업 또는 복수 작업 지정 작업 작업)에 정의된 설명 속성의 컨텐츠입니다.

**지침** 워크벤치의 프로세스 사용자 단계에서 정의된 작업 지침 속성의 컨텐츠입니다.

**notification-** hostAEM forms 응용 프로그램 서버의 호스트 이름입니다.

**process-** name 프로세스의 이름입니다.

**operation-** name단계의 이름입니다.

**** tagkid현재 작업의 고유 식별자입니다.

**작업** 수신자가 클릭할 수 있는 유효한 경로(예: 승인, 거부)의 번호 매기기 목록을 만듭니다.

또한 그룹 미리 알림, 그룹 작업 지정 및 그룹 마감일 등의 경우 다음을 사용할 수도 있습니다.

**그룹** 이름작업 항목이 지정된 그룹의 이름입니다.

>[!NOTE]
>
>변수에 값이 없으면 아무 것도 반환되지 않습니다.

중단된 분기의 경우 [제목] 및 [알림 템플릿] 상자에 다음 변수를 사용할 수 있습니다.

**분기** id분기 식별자입니다.

**process-** id프로세스 인스턴스 식별자입니다.

**notification-** hostAEM forms 응용 프로그램 서버의 호스트 이름입니다.

중단된 작업의 경우 [제목] 및 [알림 템플릿] 상자에 다음 변수를 사용할 수 있습니다.

**action-** id작업 식별자입니다.

**분기** id분기 식별자입니다.

**process-** id프로세스 인스턴스 식별자입니다.

**notification-** hostAEM forms 응용 프로그램 서버의 호스트 이름입니다.

### 제목 상자 {#using-a-variable-in-the-subject-box}에서 변수 사용

작업 지정 알림에 대한 제목 상자에 다음 텍스트를 입력하는 경우:

`Please complete task @@taskid@@`

사용자에게 작업 376이 할당되면 다음과 같은 제목이 있는 이메일 메시지가 표시됩니다.

`Please complete task 376`

### 알림 템플릿 상자 {#using-variables-in-the-notification-template-box}의 변수 사용

중단된 분기 알림에 대한 알림 템플릿 상자에 다음 텍스트를 입력하는 경우:

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

분기 번호가 4868이고 서버 이름이 `ServerXYZ`인 경우 관리자는 다음 콘텐트가 포함된 이메일 메시지를 수신합니다.

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## 비즈니스 활동 모니터링 연결 구성 {#configuring-business-activity-monitoring-connections}

선택적 모듈인 비즈니스 활동 모니터링은 작업 및 주요 성능 지표를 실시간으로 확인할 수 있는 운영 대시보드 세트를 제공합니다.

[BAM 구성 설정] 페이지에서 BAM을 실행하는 서버에 대한 연결을 설정하여 프로세스 관련 이벤트를 추적하고 해당 서버로 전송할 수 있습니다.

1. 관리 콘솔에서 서비스 > Forms 워크플로우 > 서버 설정 > BAM 구성 설정을 클릭합니다.
1. BAM 호스트 상자에 BAM을 실행하는 서버의 이름을 입력합니다. 기본값은 localhost입니다.
1. BAM 포트 상자에 BAM을 실행하는 서버에 연결하는 데 사용할 포트를 입력합니다. JBoss의 기본 BAM 포트는 8080이고, WebLogic은 7001이고, WebSphere는 9080입니다.
1. [서버 호스트] 상자에 호스트 양식 서버의 이름 또는 IP 주소를 입력합니다. 기본값은 localhost입니다.
1. 서버 포트 상자에 양식 서버에서 사용하는 포트 번호를 입력합니다.
1. [사용자 이름 및 암호] 상자에 적절한 사용자 ID와 암호를 입력하여 BAM 서버에 액세스합니다. 기본 사용자 이름은 CognosNowAdmin이고 기본 암호는 manager입니다.
1. 저장을 클릭합니다.

