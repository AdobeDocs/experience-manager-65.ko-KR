---
title: Microsoft® Office 365 메일 서버 프로토콜에 대한 OAuth2 기반 인증 구성
description: Microsoft® Office 365 메일 서버 프로토콜에 대한 OAuth2 기반 인증 구성
exl-id: cd3da71f-892c-4fde-905f-71a64fb5d4e4
source-git-commit: d19de2955adef56570378a6d62ec0015718f9039
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 3%

---

# Microsoft® Office 365 메일 서버 프로토콜과 통합 {#oauth2-support-for-the-microsoft-mail-server-protocols}

조직에서 보안 이메일 요구 사항을 준수할 수 있도록 AEM Forms은 Microsoft® Office 365 메일 서버 프로토콜과의 통합을 위해 OAuth 2.0 지원을 제공합니다. Azure Active Directory(Azure AD) OAuth 2.0 인증 서비스를 사용하여 IMAP, POP 또는 SMTP와 같은 다양한 프로토콜과 연결하고 Office 365 사용자의 전자 메일 데이터에 액세스할 수 있습니다. 다음은 OAuth 2.0 서비스를 통해 인증하도록 Microsoft® Office 365 메일 서버 프로토콜을 구성하는 단계별 지침입니다.

1. 로그인 [https://portal.azure.com/](https://portal.azure.com/) 및 검색 **Azure Active Directory** 검색 막대에서 결과를 클릭합니다.
또는 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)에서 바로 검색할 수 있습니다.
1. 클릭 **추가** > **앱 등록** > **새 등록**

   ![앱 등록](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. 요구 사항에 따라 정보를 입력한 다음 **등록**.
   ![지원되는 계정](/help/forms/using/assets/azure_suuportedaccountype.png)
위의 경우 
**조직 디렉터리(모든 Azure AD 디렉터리 - 다중 임차인)와 개인 Microsoft® 계정(예: Skype, Xbox)의 계정** 옵션이 선택되어 있습니다.

   >[!NOTE]
   >
   > * 대상 **조직 디렉토리의 계정(모든 Azure AD 디렉토리 - 다중 임차인)** 개인 이메일 계정이 아닌 작업 계정을 사용하는 것이 좋습니다.
   > * **개인 Microsoft® 계정만** 응용 프로그램이 지원되지 않습니다.
   > * 을 사용하는 것이 좋습니다 **다중 임차인 및 개인 Microsoft® 계정** 응용 프로그램.


1. 다음으로 이동 **인증서 및 기밀**&#x200B;를 클릭합니다. **새 클라이언트 암호** 및 화면의 단계에 따라 암호를 만듭니다. 나중에 사용할 수 있도록 이 비밀 값을 반드시 기록하십시오.

   ![비밀 키](/help/forms/using/assets/azure_secretkey.png)

1. 권한을 추가하려면 새로 만든 앱으로 이동하여 를 선택합니다 **API 권한** > **권한 추가** > **Microsoft® 그래프** > **위임된 권한**
1. 앱의 아래 권한에 대한 확인란을 선택하고 를 클릭합니다 **권한 추가**:

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![API 권한](/help/forms/using/assets/azure_apipermission.png)

1. 선택 **인증** > **플랫폼 추가** > **웹**, 및에서 **리디렉션 Url** 섹션에서 아래의 URI(Universal Resource Identifier) 중 하나를 다음과 같이 추가합니다.
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   이 경우 `https://login.microsoftonline.com/common/oauth2/nativeclient` 리디렉션 URI로 사용됩니다.

1. 클릭 **구성** 각 URL을 추가하고 요구 사항에 따라 설정을 구성합니다.
   ![URI 리디렉션](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   > 선택해야 합니다 **액세스 토큰** 및 **ID 토큰** 확인란.

1. 클릭 **개요** 왼쪽 창에서 **애플리케이션(클라이언트) ID**, **디렉토리(테넌트) ID**, 및 **클라이언트 암호** 나중에 사용합니다.

   ![개요](/help/forms/using/assets/azure_overview.png)

## 인증 코드 생성 {#generating-the-authorization-code}

그런 다음 다음 다음 단계에 설명된 인증 코드를 생성해야 합니다.

1. 를 바꾼 후 브라우저에서 다음 URL을 엽니다 `clientID` 사용 `<client_id>` 및 `redirect_uri` 애플리케이션의 리디렉션 URI를 사용하여 다음을 수행합니다.

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

   >[!NOTE]
   >
   > 단일 테넌트 애플리케이션의 경우 `common` 사용 `[tenantid]` 인증 코드를 생성하기 위한 다음 URL에서: `https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/authorize?client_id=[[clientid]]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20openid%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login`

1. 위의 URL을 입력하면 로그인 화면으로 리디렉션됩니다.
   ![로그인 화면](/help/forms/using/assets/azure_loginscreen.png)

1. 이메일을 입력하고 **다음** 및 앱 권한 화면이 표시됩니다.

   ![권한 허용](/help/forms/using/assets/azure_permission.png)

1. 권한을 허용하면 다음과 같이 새 URL로 리디렉션됩니다. `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. 다음 값 복사 `<code>` 위의 URL에서 `0.ASY...` to `&session_state` 를 반환합니다.

## 새로 고침 토큰 생성 {#generating-the-refresh-token}

다음으로 다음 단계에 설명된 새로 고침 토큰을 생성해야 합니다.

1. 명령 프롬프트를 열고 다음 cURL 명령을 사용하여 refreshToken을 가져옵니다.

1. 바꾸기 `clientID`, `client_secret` 및 `redirect_uri` 와 함께 응용 프로그램의 값과 `<code>`:

   `curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

   >[!NOTE]
   >
   > 단일 테넌트 애플리케이션에서 새로 고침 토큰을 생성하려면 다음 cURL 명령을 사용하고 바꿉니다 `common` 사용 `[tenantid]` in:
   >`curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/token`

1. 새로 고침 토큰을 기록합니다.

## OAuth 2.0 지원을 통해 이메일 서비스 구성 {#configureemailservice}

이제 관리 UI에서 로그인하여 최신 JEE 서버에서 이메일 서비스를 구성해야 합니다.

1. 이동 **홈** > **서비스** > **애플리케이션 및 서비스** > **서비스 관리** > **이메일 서비스**, **구성 이메일 서비스** 기본 인증을 위해 구성된 창이 나타납니다.

   >[!NOTE]
   >
   > oAuth 2.0 인증 서비스를 활성화하려면 반드시 선택해야 합니다. **SMTP 서버에 인증이 필요한지 여부(SMTP 인증)** 확인란을 선택합니다.

1. 설정 **oAuth 2.0 인증 설정** 로서의 `True`.
1. 다음 값 복사 **클라이언트 ID** 및 **클라이언트 암호** Azure 포털
1. 생성된 값을 복사합니다. **토큰 새로 고침**.
1. 에 로그인합니다. **Workbench** 검색 및 검색 **이메일 1.0** 변환 전: **활동 선택기**.
1. 이메일 1.0에서는 다음 세 가지 옵션을 사용할 수 있습니다.
   * **문서로 보내기**: 단일 첨부 파일이 있는 전자 메일을 보냅니다.
   * **첨부 파일 맵으로 보내기**: 여러 첨부 파일이 있는 이메일을 보냅니다.
   * **수신**: IMAP에서 전자 메일을 받습니다.

   >[!NOTE]
   >
   >* 전송 보안 프로토콜의 유효한 값은 다음과 같습니다. &#39;blank&#39;, &#39;SSL&#39; 또는 &#39;TLS&#39;. 값을 설정해야 합니다. **SMTP 전송 보안** 및 **전송 보안 수신** to **TLS** oAuth 인증 서비스를 사용하도록 설정하는 중입니다.
   >* **POP3 프로토콜** 은 이메일 끝점을 사용하는 동안 OAuth에 대해 지원되지 않습니다.


   ![연결 설정](/help/forms/using/assets/oauth_connectionsettings.png)

1. 을(를) 선택하여 응용 프로그램을 테스트합니다. **문서로 보내기**.
1. 제공 **종료** 및 **From** 주소.
1. 0Auth 2.0 인증을 사용하여 응용 프로그램 및 전자 메일이 전송됩니다.

   >[!NOTE]
   >
   >워크벤치의 특정 프로세스에 대한 기본 인증으로 인증 2.0 인증 설정을 변경하려면 **OAuth 2.0 인증** 값 아래의 &#39;False&#39;입니다. **전역 설정 사용** 에서 **연결 설정** 탭.

## oAuth 작업 알림을 활성화하려면 {#enable_oauth_task}

1. 이동 **홈** > **서비스** > **양식 워크플로우** > **서버 설정** > **전자 메일 설정**
1. oAuth 작업 알림을 활성화하려면 **oAuth 활성화** 확인란을 선택합니다.
1. 다음 값 복사 **클라이언트 ID** 및 **클라이언트 암호** Azure 포털
1. 생성된 값을 복사합니다. **토큰 새로 고침**.
1. 클릭 **저장** 세부 사항을 저장합니다.

   ![작업 알림](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   > 작업 알림과 관련된 자세한 정보를 알아보려면 [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html#create-an-email-endpoint-for-the-complete-task-service).

## 전자 메일 끝점을 구성하려면 {#configure_email_endpoint}

1. 이동 **홈** > **서비스** > **애플리케이션 및 서비스** > **Endpoint Management**
1. 전자 메일 끝점을 구성하려면 을 설정합니다. **oAuth 2.0 인증 설정** 로서의 `True`.
1. 다음 값 복사 **클라이언트 ID** 및 **클라이언트 암호** Azure 포털
1. 생성된 값을 복사합니다. **토큰 새로 고침**.
1. 클릭 **저장** 세부 사항을 저장합니다.

   ![연결 설정](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   > 전자 메일 엔드포인트 구성에 대한 자세한 내용을 보려면 [전자 메일 끝점 구성](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html).

## 문제 해결 {#troubleshooting}

* 이메일 서비스가 제대로 작동하지 않는 경우 를 다시 생성해 보십시오 `Refresh Token` 위에 설명된 대로, 새 값을 배포하려면 몇 분이 걸립니다.

* Workbench를 사용하여 전자 메일 끝점에서 전자 메일 서버 세부 사항을 구성하는 동안 오류가 발생했습니다.Workbench 대신 Admin UI를 통해 끝점을 구성하세요.
