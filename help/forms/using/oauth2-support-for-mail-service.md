---
title: Microsoft&reg(Forms JEE OAuth), Office 365 메일 서버 프로토콜에 대한 OAuth2 기반 인증 구성
description: Microsoft&reg(Forms JEE OAuth), Office 365 메일 서버 프로토콜에 대한 OAuth2 기반 인증 구성
exl-id: cd3da71f-892c-4fde-905f-71a64fb5d4e4
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 5%

---

# Microsoft® Office 365 메일 서버 프로토콜과 AEM Forms 통합 {#oauth2-support-for-the-microsoft-mail-server-protocols}

조직에서 이메일 요구 사항을 준수할 수 있도록 AEM Forms은 Microsoft® Office 365 메일 서버 프로토콜과의 통합을 위한 OAuth 2.0 지원을 제공합니다. Azure AD(Azure Active Directory) OAuth 2.0 인증 서비스를 사용하여 IMAP, POP 또는 SMTP 등의 다양한 프로토콜과 연결하고 Office 365 사용자의 전자 메일 데이터에 액세스할 수 있습니다. 다음은 OAuth 2.0 서비스를 통해 인증할 Microsoft® Office 365 메일 서버 프로토콜을 구성하는 단계별 지침입니다.

1. [https://portal.azure.com/](https://portal.azure.com/)에 로그인하고 검색 창에서 **Azure Active Directory**&#x200B;를 검색한 다음 결과를 클릭합니다.
또는 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)에서 바로 검색할 수 있습니다.
1. **추가** > **앱 등록** > **새 등록**&#x200B;을 클릭합니다.

   ![앱 등록](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. 요구 사항에 따라 정보를 입력한 다음, **등록**&#x200B;을 클릭합니다.
   ![지원되는 계정](/help/forms/using/assets/azure_suuportedaccountype.png)
위의 경우 **조직 디렉터리(모든 Azure AD 디렉터리 - 다중 테넌트)의 계정 및 개인 Microsoft® 계정(예: Skype, Xbox)** 옵션이 선택됩니다.

   >[!NOTE]
   >
   > * Adobe **조직 디렉터리(모든 Azure AD 디렉터리 - 다중 테넌트)** 응용 프로그램의 계정의 경우 개인 전자 메일 계정이 아닌 작업 계정을 사용하는 것이 좋습니다.
   > * **개인 Microsoft® 계정만** 응용 프로그램은 지원되지 않습니다.
   > * Adobe **다중 테넌트 및 개인 Microsoft® 계정** 응용 프로그램을 사용하는 것이 좋습니다.

1. 그런 다음 **증명서 및 보안**&#x200B;으로 이동하고, **신규 클라이언트 보안**&#x200B;을 클릭한 후 화면에 표시되는 단계에 따라 보안을 생성합니다. 나중에 사용할 수 있도록 이 암호 값을 메모해 두십시오.

   ![비밀 키](/help/forms/using/assets/azure_secretkey.png)

1. 권한을 추가하려면 새로 만든 앱으로 이동하여 **API 권한** > **권한 추가** > **Microsoft® 그래프** > **위임된 권한**&#x200B;을(를) 선택하십시오.
1. 앱의 아래 사용 권한에 대한 확인란을 선택하고 **사용 권한 추가**&#x200B;를 클릭합니다.

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![API 권한](/help/forms/using/assets/azure_apipermission.png)

1. **인증** > **플랫폼 추가** > **웹**&#x200B;을 선택하고 **리디렉션 URL** 섹션에서 아래 URI(Universal Resource Identifier)를 다음과 같이 추가합니다.
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   이 경우 `https://login.microsoftonline.com/common/oauth2/nativeclient`은(는) 리디렉션 URI로 사용됩니다.

1. 각 URL을 추가한 후 **구성**&#x200B;을 클릭하고 요구 사항에 따라 설정을 구성합니다.
   ![리디렉션 URI](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   > **액세스 토큰** 및 **ID 토큰** 확인란을 선택해야 합니다.

1. 왼쪽 창에서 **개요**&#x200B;를 클릭하고 나중에 사용할 수 있도록 **응용 프로그램(클라이언트) ID**, **디렉터리(테넌트) ID** 및 **클라이언트 암호**&#x200B;의 값을 복사합니다.

   ![개요](/help/forms/using/assets/azure_overview.png)

## 인증 코드 생성 {#generating-the-authorization-code}

다음으로, 다음 단계에 설명된 인증 코드를 생성해야 합니다.

1. `clientID`을(를) `<client_id>`(으)로, `redirect_uri`을(를) 애플리케이션의 리디렉션 URI로 바꾼 후 브라우저에서 다음 URL을 엽니다.

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

   >[!NOTE]
   >
   > 단일 테넌트 응용 프로그램이 있는 경우 인증 코드를 생성하기 위해 다음 URL에서 `common`을(를) `[tenantid]`(으)로 바꾸십시오. `https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/authorize?client_id=[[clientid]]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20openid%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login`

1. 위의 URL을 입력하면 로그인 화면으로 리디렉션됩니다.
   ![로그인 화면](/help/forms/using/assets/azure_loginscreen.png)

1. 이메일을 입력하고 **다음**&#x200B;을 클릭하면 앱 권한 화면이 나타납니다.

   ![권한 허용](/help/forms/using/assets/azure_permission.png)

1. 권한을 허용하면 새 URL로 리디렉션됩니다. `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. `<code>`의 값을 위 URL의 `0.ASY...`에서 위 URL의 `&session_state`(으)로 복사합니다.

## 새로 고침 토큰 생성 {#generating-the-refresh-token}

그런 다음 다음 다음 단계에 설명된 새로 고침 토큰을 생성해야 합니다.

1. 명령 프롬프트를 열고 다음 cURL 명령을 사용하여 refreshToken을 가져옵니다.

1. `clientID`, `client_secret` 및 `redirect_uri`을(를) `<code>` 값과 함께 응용 프로그램의 값으로 바꿉니다.

   `curl -H "ContentType application/x-www-form-urlencoded" -d "client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]" -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

   >[!NOTE]
   >
   > 단일 테넌트 응용 프로그램에서 새로 고침 토큰을 생성하려면 다음 cURL 명령을 사용하고 `common`을(를) 의 `[tenantid]`(으)로 바꿉니다.
   >`curl -H "ContentType application/x-www-form-urlencoded" -d "client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]" -X POST https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/token`

1. 새로 고침 토큰을 기록합니다.

## OAuth 2.0 지원을 통해 이메일 서비스 구성 {#configureemailservice}

이제 Admin UI에 로그인하여 최신 JEE 서버에서 전자 메일 서비스를 구성합니다.

1. **홈** > **서비스** > **응용 프로그램 및 서비스** > **서비스 관리** > **이메일 서비스**(으)로 이동하면 기본 인증을 위해 구성된 **구성 이메일 서비스** 창이 나타납니다.

   >[!NOTE]
   >
   > oAuth 2.0 인증 서비스를 사용하려면 **SMTP 서버에 인증이 필요한지 여부(SMTP 인증)** 확인란을 선택해야 합니다.

1. **oAuth 2.0 인증 설정**&#x200B;을(를) `True`(으)로 설정합니다.
1. Azure 포털에서 **클라이언트 ID** 및 **클라이언트 암호**&#x200B;의 값을 복사합니다.
1. 생성된 **새로 고침 토큰**&#x200B;의 값을 복사합니다.
1. **Workbench**&#x200B;에 로그인하고 **활동 선택기**&#x200B;에서 **전자 메일 1.0**&#x200B;을 검색합니다.
1. 이메일 1.0에서는 다음과 같이 세 가지 옵션을 사용할 수 있습니다.
   * **문서를 사용하여 보내기**: 전자 메일을 첨부 파일로 보냅니다.
   * **첨부 파일 맵으로 보내기**: 여러 첨부 파일이 있는 전자 메일을 보냅니다.
   * **수신**: IMAP에서 전자 메일을 받습니다.

   >[!NOTE]
   >
   >* 전송 보안 프로토콜의 유효한 값은 &#39;blank&#39;, &#39;SSL&#39; 또는 &#39;TLS&#39;입니다. oAuth 인증 서비스를 사용하도록 설정하려면 **SMTP 전송 보안** 및 **전송 보안 수신** 값을 **TLS**(으)로 설정하십시오.
   >* **POP3 프로토콜**&#x200B;은(는) 전자 메일 끝점을 사용하는 동안 OAuth에 대해 지원되지 않습니다.

   ![연결 설정](/help/forms/using/assets/oauth_connectionsettings.png)

1. **문서를 사용하여 보내기**&#x200B;를 선택하여 응용 프로그램을 테스트합니다.
1. **TO** 및 **From** 주소를 제공하십시오.
1. 애플리케이션을 호출하면 0Auth 2.0 인증을 사용하여 이메일이 전송됩니다.

   >[!NOTE]
   >
   >원하는 경우 Workbench에서 특정 프로세스에 대한 기본 인증으로 Auth 2.0 인증 설정을 변경할 수 있습니다. 이렇게 하려면 **연결 설정** 탭의 **전역 설정 사용**&#x200B;에서 **OAuth 2.0 인증** 값을 &#39;False&#39;로 설정하십시오.

## oAuth 작업 알림을 활성화하려면 {#enable_oauth_task}

1. **홈** > **서비스** > **양식 워크플로** > **서버 설정** > **전자 메일 설정**(으)로 이동
1. oAuth 작업 알림을 활성화하려면 **oAuth 활성화** 확인란을 선택하십시오.
1. Azure 포털에서 **클라이언트 ID** 및 **클라이언트 암호**&#x200B;의 값을 복사합니다.
1. 생성된 **새로 고침 토큰**&#x200B;의 값을 복사합니다.
1. 자세한 내용을 저장하려면 **저장**&#x200B;을 클릭하세요.

   ![작업 알림](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   > 작업 알림과 관련된 자세한 정보를 보려면 [여기를 클릭하세요](https://experienceleague.adobe.com/docs/experience-manager-65/content/forms/administrator-help/configuring-email-endpoints.html#create-an-email-endpoint-for-the-complete-task-service).

## 이메일 엔드포인트를 구성하려면 {#configure_email_endpoint}

1. **홈** > **서비스** > **응용 프로그램 및 서비스** > **끝점 관리**(으)로 이동
1. 전자 메일 끝점을 구성하려면 **oAuth 2.0 인증 설정**&#x200B;을 `True`(으)로 설정하십시오.
1. Azure 포털에서 **클라이언트 ID** 및 **클라이언트 암호**&#x200B;의 값을 복사합니다.
1. 생성된 **새로 고침 토큰**&#x200B;의 값을 복사합니다.
1. 자세한 내용을 저장하려면 **저장**&#x200B;을 클릭하세요.

   ![연결 설정](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   > 전자 메일 끝점 구성에 대한 자세한 내용을 보려면 [전자 메일 끝점 구성](https://experienceleague.adobe.com/docs/experience-manager-65/content/forms/administrator-help/configuring-email-endpoints.html)을 클릭하세요.

## 문제 해결 {#troubleshooting}

* 전자 메일 서비스가 제대로 작동하지 않는 경우 위에 설명된 대로 `Refresh Token`을(를) 다시 생성해 보십시오. 새 값을 배포하는 데 몇 분 정도 소요됩니다.

* Workbench를 사용하여 전자 메일 끝점에 전자 메일 서버 세부 정보를 구성하는 동안 오류가 발생했습니다. Workbench 대신 관리자 UI를 통해 끝점을 구성해 보십시오.
