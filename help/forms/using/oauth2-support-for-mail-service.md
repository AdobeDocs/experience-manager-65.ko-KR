---
title: 메일 서비스에 대한 OAuth2 지원
description: '메일 서비스에 대한 Oauth2 지원  '
source-git-commit: 081b0c70ceca0502cb84d7e1b68b0b12dc45a4e7
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 47%

---

# 메일 서비스에 대한 OAuth2 지원 {#oauth2-support-for-the-mail-service}

AEM as a Cloud Service는 조직의 이메일 요구 사항 보호 준수를 위해 통합 메일 서비스에 대한 OAuth2 지원을 제공합니다.

여러 이메일 공급자에 대해 OAuth를 구성할 수 있습니다. 다음은 Microsoft Office 365 Outlook과 함께 OAuth2를 통해 인증할 AEM 메일 서비스를 구성하는 방법에 대한 단계별 지침입니다. 다른 공급업체가 유사한 방식으로 구성될 수 있습니다.

## Microsoft Outlook {#microsoft-outlook}

1. [https://portal.azure.com/](https://portal.azure.com/)으로 이동한 다음 로그인합니다.
1. 검색창에서 **Azure Active Directory**&#x200B;를 검색한 다음 결과를 클릭합니다. 또는 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)에서 바로 검색할 수 있습니다.
1. **앱 등록** - **신규 등록**&#x200B;을 클릭합니다.

   ![](/help/forms/using/assets/outh_outlook.PNG)

1. 요구 사항에 따라 정보를 입력한 다음 **등록**&#x200B;을 클릭합니다.
1. 새로 생성된 앱으로 이동하여 **API 권한**&#x200B;을 선택합니다.
1. **권한 추가** - **그래프 권한** - **위임된 권한**&#x200B;으로 이동합니다.
1. 아래의 앱에 대한 권한을 선택한 다음 **권한 추가**&#x200B;를 클릭합니다.
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. **인증** - **플랫폼 추가** - **웹**&#x200B;으로 이동한 다음 **리디렉션 URL** 섹션에서 슬래시가 있는 URL과 슬래시가 없는 URL을 추가합니다.
   * `http://localhost/`
   * `http://localhost`
1. 각 URL을 추가한 후 **구성**&#x200B;을 눌러 요구 사항에 따라 설정을 구성합니다.
1. 다음으로 이동 **인증서 및 기밀**&#x200B;를 클릭하고 **새 클라이언트 암호** 및 화면의 단계에 따라 암호를 만듭니다. 나중에 사용할 수 있도록 이러한 보안 내용을 메모해 두십시오.
1. 누르기 **개요** 왼쪽 창에서 **애플리케이션(클라이언트) ID** 나중에 사용합니다.

다시 매핑하려면 AEM 측에서 Mail 서비스에 대해 OAuth2를 구성하려면 다음 정보가 필요합니다.

* 양식의 인증 URL: `https://login.microsoftonline.com/<ID>/oauth2/v2.0/authorize`
* 양식의 토큰 URL: `https://login.microsoftonline.com/<ID>/oauth2/v2.0/token`
* 양식에서 URL 새로 고침: `https://login.microsoftonline.com/<ID>/oauth2/v2.0/token`
* 클라이언트 ID
* 클라이언트 보안

### 새로 고침 토큰 생성 {#generating-the-refresh-token}

그런 다음 후속 단계에 설명된 대로 새로 고침 토큰을 생성해야 합니다.

다음 단계를 따라 이 작업을 수행할 수 있습니다.

1. 를 바꾼 후 브라우저에서 다음 URL을 엽니다 `clientID` 계정에 해당하는 값 사용:

   ```https://login.microsoftonline.com/common/oauth2/v2/authorize?client_id=<client_id>&scope=IMAP.AccessAsUser.A;;%20POP.AccessAsUser.All%20SMTP.Send%20User.Read&response_type=code&redirect-uri=http://loginmicrosoftonline.com/common/outh2/nativeclient&prompt=login```

1. 필요할 때마다 권한을 허용합니다.
1. 해당 URL은 다음 형식으로 구성된 새 위치로 리디렉션합니다. `http://localhost/?code=<code>&state=12345&session_state=4f984c6b-cc1f-47b9-81b2-66522ea83f81#`
1. 위 예의 `<code>` 값을 복사합니다.
1. 다음 cURL 명령을 사용하여 refreshToken을 가져옵니다. clientID, clientSecret을 사용자 계정의 값 및 값으로 바꿉니다 `<code>`:

   ```
   curl -H “ContentType application/x-www-form-urlencoded” -d 
   "client_id=<client-id>
   &scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All&code=M.R3_BAY.1bf609bf-25b3-2fcd-d910-02e02c53bc
   &grant_type=authorization_code
   &redirect_uri= https://login.microsoftonline.com/common/oauth2/nativeclient
   &client_secret=~1E8Q~cz-m6vgOb9m~SI.eF9jSVTbFUiP5f0” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token
   ```

1. refreshToken 및 accessToken을 기록해 두십시오.

### 토큰 확인 {#validating-the-tokens}

AEM측의 OAuth 구성을 진행하기에 앞서 아래 절차에 따라 accessToken 및 refreshToken을 확인하십시오.

1. 이전 절차에서 생성된 refreshToken을 사용하여 accessToken을 생성합니다. 다음과 같이 curl을 사용하여 값을 바꿀 수 있습니다 `<client_id>`,`<client_secret>` 함께 `<refreshToken>`:

   ```
   curl -H “ContentType application/x-www-form-urlencoded” -d 
   "client_id=<client_id>
   &scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All&code=<code>
   &grant_type=authorization_code
   &redirect_uri= https://login.microsoftonline.com/common/oauth2/nativeclient
   &client_secret=<client_secret>
   &refresh_token=<refresh_token” 
   -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token
   ```

1. accessToken을 사용하여 메일을 보내 제대로 작동하는지 확인하십시오.

>[!NOTE]
>
> [이 위치](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow)에서 Postman API 컬렉션을 가져올 수 있습니다.

### Auth2.0 지원을 통해 이메일 서비스 구성 {#configureemailservice}

이제 관리 UI에서 로그인하여 최신 JEE 서버에서 이메일 서비스를 구성해야 합니다.

1. 이동 **홈** - **서비스** - **애플리케이션 및 서비스** - **서비스 관리** - **이메일 서비스**
1. **구성 이메일 서비스** 창이 나타나고, 구성 **SMPT** 및 **IMP** 기본 인증을 위한 서버입니다.
1. Outlook 메일 인증 서비스를 사용하려면 **oAuth 2.0 인증 설정** 확인란을 선택합니다.
1. 다음 값 복사 **클라이언트 ID** 및 **클라이언트 암호** Azure 포털
1. 생성된 값을 복사합니다. **토큰 새로 고침**.
1. 클릭 **저장** 세부 사항을 저장합니다.
1. Workbench에 로그인 및 검색 **이메일 1.0** 변환 전: **활동 선택기**.
1. 이메일 1.0에서는 다음 세 가지 옵션을 사용할 수 있습니다.
   * **문서로 보내기**: 단일 첨부 파일이 있는 전자 메일을 보냅니다.
   * **첨부 파일 맵으로 보내기**: 여러 첨부 파일이 있는 이메일을 보냅니다.
   * **수신**: POP3 또는 IMAP에서 전자 메일을 받습니다.
1. 을(를) 선택하여 응용 프로그램을 테스트합니다. **문서로 보내기**
1. 제공 **종료** 및 **From** 주소.
1. oAuth2.0 인증을 사용하여 응용 프로그램 및 전자 메일이 전송됩니다.

>[!NOTE]
>
> Auth 2.0 인증 설정을 Workbench의 특정 프로세스에 대한 기본 인증으로 변경하려면 **oAuth2.0 인증** 확인란 아래의 **전역 설정 사용** 에서 **연결 설정** 탭.

### 문제 해결 {#troubleshooting}

메일 서비스가 제대로 작동하지 않으면 을(를) 다시 생성합니다 `refreshToken` 위에 설명된 대로, 새 값을 배포하려면 몇 분이 걸립니다.


