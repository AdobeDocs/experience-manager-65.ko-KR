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

조직에서 이메일 요구 사항을 준수할 수 있도록 AEM Forms은 Microsoft® Office 365 메일 서버 프로토콜과의 통합을 위한 OAuth 2.0 지원을 제공합니다. Azure AD(Azure Active Directory) OAuth 2.0 인증 서비스를 사용하여 IMAP, POP 또는 SMTP와 같은 다양한 프로토콜과 연결하고 Office 365 사용자의 전자 메일 데이터에 액세스할 수 있습니다. 다음은 OAuth 2.0 서비스를 통해 인증할 Microsoft® Office 365 메일 서버 프로토콜을 구성하는 단계별 지침입니다.

1. 로그인 [https://portal.azure.com/](https://portal.azure.com/) 및 검색 **Azure Active Directory** 검색 창에서 결과를 클릭합니다.
또는 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)에서 바로 검색할 수 있습니다.
1. 클릭 **추가** > **앱 등록** > **새 등록**

   ![앱 등록](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. 요구 사항에 따라 정보를 입력한 다음 **등록**.
   ![지원되는 계정](/help/forms/using/assets/azure_suuportedaccountype.png)
위의 경우, 
**조직 디렉터리(모든 Azure AD 디렉터리 - 다중 테넌트)의 계정 및 개인 Microsoft® 계정(예: Skype, Xbox)** 옵션이 선택되어 있습니다.

   >[!NOTE]
   >
   > * 대상 **조직 디렉터리(모든 Azure AD 디렉터리 - 다중 테넌트)의 계정** 애플리케이션에서는 개인 이메일 계정보다는 회사 계정을 사용하는 것이 좋습니다.
   > * **개인 Microsoft® 계정만** 응용 프로그램이 지원되지 않습니다.
   > * 를 사용하는 것이 좋습니다. **다중 임차인 및 개인 Microsoft® 계정** 응용 프로그램.


1. 다음으로 이동 **인증서 및 암호**, 클릭 **새 클라이언트 암호** 화면에 표시되는 단계에 따라 암호를 만드십시오. 나중에 사용할 수 있도록 이 암호 값을 메모해 두십시오.

   ![비밀 키](/help/forms/using/assets/azure_secretkey.png)

1. 권한을 추가하려면 새로 만든 앱으로 이동하여 **API 권한** > **권한 추가** > **Microsoft® 그래프** > **위임된 권한**
1. 앱에 대한 아래 권한 확인란을 선택하고 **권한 추가**:

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![API 권한](/help/forms/using/assets/azure_apipermission.png)

1. 선택 **인증** > **플랫폼 추가** > **웹**, 및 **리디렉션 Url** 섹션에서 아래 URI(Universal Resource Identifier)를 다음과 같이 추가합니다.
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   이 경우, `https://login.microsoftonline.com/common/oauth2/nativeclient` 는 리디렉션 URI로 사용됩니다.

1. 클릭 **구성** 각 URL을 추가하고 요구 사항에 따라 설정을 구성합니다.
   ![URI 리디렉션](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   > 다음을 선택해야 합니다. **토큰 액세스** 및 **ID 토큰** 확인란.

1. 클릭 **개요** 왼쪽 창에서 다음 값을 복사합니다. **애플리케이션(클라이언트) ID**, **디렉터리(테넌트) ID**, 및 **클라이언트 암호** 나중에 사용합니다.

   ![개요](/help/forms/using/assets/azure_overview.png)

## 인증 코드 생성 {#generating-the-authorization-code}

다음으로, 다음 단계에 설명된 인증 코드를 생성해야 합니다.

1. 을 교체한 후 브라우저에서 다음 URL을 엽니다. `clientID` (으)로 `<client_id>` 및 `redirect_uri` 애플리케이션의 리디렉션 URI로:

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

   >[!NOTE]
   >
   > 단일 테넌트 응용 프로그램의 경우 바꾸기 `common` (으)로 `[tenantid]` 인증 코드를 생성하기 위한 다음 URL: `https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/authorize?client_id=[[clientid]]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20openid%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login`

1. 위의 URL을 입력하면 로그인 화면으로 리디렉션됩니다.
   ![로그인 화면](/help/forms/using/assets/azure_loginscreen.png)

1. 이메일을 입력하고 **다음** 앱 권한 화면이 표시됩니다.

   ![권한 허용](/help/forms/using/assets/azure_permission.png)

1. 권한을 허용하면 다음과 같이 새 URL로 리디렉션됩니다. `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. 값 복사 `<code>` 의 상기 URL에서 `0.ASY...` 끝 `&session_state` 위의 URL에서

## 새로 고침 토큰 생성 {#generating-the-refresh-token}

그런 다음 다음 다음 단계에 설명된 새로 고침 토큰을 생성해야 합니다.

1. 명령 프롬프트를 열고 다음 cURL 명령을 사용하여 refreshToken을 가져옵니다.

1. 바꾸기 `clientID`, `client_secret` 및 `redirect_uri` ( 값 와 함께 애플리케이션 값 포함) `<code>`:

   `curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

   >[!NOTE]
   >
   > 단일 테넌트 응용 프로그램에서 새로 고침 토큰을 생성하려면 다음 cURL 명령을 사용하고 바꾸기 `common` (으)로 `[tenantid]` 위치:
   >`curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/token`

1. 새로 고침 토큰을 기록합니다.

## OAuth 2.0 지원을 통해 이메일 서비스 구성 {#configureemailservice}

이제 관리 UI에 로그인하여 최신 JEE 서버에서 이메일 서비스를 구성해야 합니다.

1. 다음으로 이동 **홈** > **서비스** > **애플리케이션 및 서비스** > **서비스 관리** > **이메일 서비스**, **구성 이메일 서비스** 기본 인증용으로 구성된 창이 나타납니다.

   >[!NOTE]
   >
   > oAuth 2.0 인증 서비스를 활성화하려면 다음을 선택해야 합니다. **SMTP 서버에 인증이 필요한지 여부(SMTP 인증)** 확인란.

1. 설정 **oAuth 2.0 인증 설정** 다음으로: `True`.
1. 다음 값 복사 **클라이언트 ID** 및 **클라이언트 암호** Azure 포털에서.
1. 생성된 값 복사 **토큰 새로 고침**.
1. 에 로그인합니다 **Workbench** 및 검색 **이메일 1.0** 출처: **활동 선택기**.
1. 이메일 1.0에서는 다음과 같이 세 가지 옵션을 사용할 수 있습니다.
   * **문서와 함께 보내기**: 단일 첨부 파일이 포함된 이메일을 전송합니다.
   * **첨부 파일 맵으로 보내기**: 여러 첨부 파일이 포함된 이메일을 보냅니다.
   * **수신**: IMAP에서 전자 메일을 받습니다.

   >[!NOTE]
   >
   >* 전송 보안 프로토콜에는 &#39;blank&#39;, &#39;SSL&#39; 또는 &#39;TLS&#39;와 같은 유효한 값이 있습니다. 다음 값을 설정해야 합니다. **SMTP 전송 보안** 및 **전송 보안 수신** 끝 **TLS** oAuth 인증 서비스를 사용하도록 설정하는 경우.
   >* **POP3 프로토콜** 은 이메일 엔드포인트를 사용하는 동안 OAuth에 대해 지원되지 않습니다.


   ![연결 설정](/help/forms/using/assets/oauth_connectionsettings.png)

1. 다음을 선택하여 애플리케이션 테스트 **문서와 함께 보내기**.
1. 제공 **종료** 및 **출처:** 주소.
1. 응용 프로그램을 호출하면 0Auth 2.0 인증을 사용하여 이메일이 전송됩니다.

   >[!NOTE]
   >
   >Workbench에서 특정 프로세스에 대한 기본 인증으로 Auth 2.0 인증 설정을 변경하려면 다음을 설정할 수 있습니다. **OAuth 2.0 인증** 다음에서 &#39;False&#39;로서의 값: **전역 설정 사용** 다음에서 **연결 설정** 탭.

## oAuth 작업 알림을 활성화하려면 {#enable_oauth_task}

1. 다음으로 이동 **홈** > **서비스** > **양식 워크플로우** > **서버 설정** > **이메일 설정**
1. oAuth 작업 알림을 활성화하려면 **oAuth 활성화** 확인란.
1. 다음 값 복사 **클라이언트 ID** 및 **클라이언트 암호** Azure 포털에서.
1. 생성된 값 복사 **토큰 새로 고침**.
1. 클릭 **저장** 세부 정보를 저장합니다.

   ![작업 알림](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   > 작업 알림과 관련된 자세한 정보를 보려면 [여기를 클릭하십시오](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html#create-an-email-endpoint-for-the-complete-task-service).

## 이메일 엔드포인트를 구성하려면 {#configure_email_endpoint}

1. 다음으로 이동 **홈** > **서비스** > **애플리케이션 및 서비스** > **끝점 관리**
1. 이메일 엔드포인트를 구성하려면 을 설정합니다. **oAuth 2.0 인증 설정** 다음으로: `True`.
1. 다음 값 복사 **클라이언트 ID** 및 **클라이언트 암호** Azure 포털에서.
1. 생성된 값 복사 **토큰 새로 고침**.
1. 클릭 **저장** 세부 정보를 저장합니다.

   ![연결 설정](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   > 이메일 엔드포인트 구성에 대한 자세한 내용을 보려면 을(를) 클릭합니다. [이메일 엔드포인트 구성](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html).

## 문제 해결 {#troubleshooting}

* 전자 메일 서비스가 제대로 작동하지 않는 경우. 재생성 시도 `Refresh Token` 위에서 설명한 대로. 새 값을 배포하는 데 몇 분 정도 소요됩니다.

* Workbench를 사용하여 전자 메일 끝점에 전자 메일 서버 세부 정보를 구성하는 동안 오류가 발생했습니다. Workbench 대신 관리 UI를 통해 끝점을 구성하십시오.
