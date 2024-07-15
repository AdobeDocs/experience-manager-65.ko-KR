---
title: 이메일 알림 구성
description: Adobe Experience Manager에서 이메일 알림을 구성하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 918fcbbc-a78a-4fab-a933-f183ce6a907f
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '2037'
ht-degree: 9%

---


# 이메일 알림 구성{#configuring-email-notification}

AEM은 다음과 같은 사용자에게 이메일 알림을 보냅니다.

* 페이지 이벤트(예: 수정 또는 복제)를 구독했습니다. [알림 받은 편지함](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications) 섹션에서 이러한 이벤트를 구독하는 방법을 설명합니다.

* 포럼 이벤트를 구독했습니다.
* 워크플로우에서 단계를 수행해야 합니다. [참가자 단계](/help/sites-developing/workflows-step-ref.md#participant-step) 섹션에서는 워크플로우에서 전자 메일 알림을 트리거하는 방법을 설명합니다.

전제 조건:

* 사용자는 프로필에 유효한 이메일 주소가 정의되어 있어야 합니다.
* **일 CQ 메일 서비스**&#x200B;를 올바르게 구성해야 합니다.

사용자에게 알림이 전송되면 사용자는 프로필에 정의된 언어로 이메일을 수신하게 됩니다. 각 언어에는 사용자 지정할 수 있는 자체 템플릿이 있습니다. 새 언어에 대해 새 이메일 템플릿을 추가할 수 있습니다.

>[!NOTE]
>
>AEM을 사용하여 작업할 때 이러한 서비스에 대한 구성 설정을 관리할 수 있는 방법에는 몇 가지가 있습니다. 자세한 내용 및 권장 사례를 보려면 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)을 참조하십시오.

## 메일 서비스 구성 {#configuring-the-mail-service}

AEM에서 이메일을 보낼 수 있으려면 **일 CQ 메일 서비스**&#x200B;를 올바르게 구성해야 합니다. 웹 콘솔에서 구성을 볼 수 있습니다. AEM을 사용하여 작업할 때 이러한 서비스에 대한 구성 설정을 관리할 수 있는 방법에는 몇 가지가 있습니다. 자세한 내용 및 권장 사례를 보려면 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)을 참조하십시오.

다음과 같은 제한이 적용됩니다.

* **SMTP 서버 포트**&#x200B;는 25 이상이어야 합니다.

* **SMTP 서버 호스트 이름**&#x200B;은 비워 둘 수 없습니다.
* **&quot;보낸 사람&quot; 주소**&#x200B;은(는) 비워 둘 수 없습니다.

**일 CQ 메일 서비스**&#x200B;와 관련된 문제를 디버깅하기 위해 서비스 로그를 확인할 수 있습니다.

`com.day.cq.mailer.DefaultMailService`

웹 콘솔에서 구성은 다음과 같습니다.

![일별 CQ 메일 서비스 OSGi 구성 창](assets/chlimage_1-276.png)

## 이메일 알림 채널 구성 {#configuring-the-email-notification-channel}

페이지 또는 포럼 이벤트 알림을 구독하면 기본적으로 보낸 사람 이메일 주소가 `no-reply@acme.com`(으)로 설정됩니다. 웹 콘솔에서 **알림 전자 메일 채널** 서비스를 구성하여 이 값을 변경할 수 있습니다.

보낸 사람 전자 메일 주소를 구성하려면 `sling:OsgiConfig` 노드를 저장소에 추가하십시오. 다음 절차에 따라 CRXDE Lite을 사용하여 노드를 직접 추가합니다.

1. CRXDE Lite에서 응용 프로그램 폴더 아래에 `config` 폴더를 추가합니다.
1. 구성 폴더에 라는 노드를 추가합니다.

   `sling:OsgiConfig` 유형의 `com.day.cq.wcm.notification.email.impl.EmailChannel`

1. `String` 속성을 `email.from` 노드에 추가합니다. 값에 사용할 이메일 주소를 지정합니다.

1. **모두 저장**&#x200B;을 클릭합니다.

다음 절차를 사용하여 콘텐츠 패키지 소스 폴더의 노드를 정의합니다.

1. `jcr_root/apps/*app_name*/config folder`에서 이름이 `com.day.cq.wcm.notification.email.impl.EmailChannel.xml`인 파일을 만듭니다.

1. 노드를 나타내는 다음 XML을 추가합니다.

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. `email.from` 특성(`name@server.com`)의 값을 전자 메일 주소로 바꿉니다.

1. 파일을 저장합니다.

## 워크플로우 이메일 알림 서비스 구성 {#configuring-the-workflow-email-notification-service}

워크플로우 이메일 알림을 받을 때 보낸 사람 이메일 주소와 호스트 URL 접두어가 모두 기본값으로 설정됩니다. 웹 콘솔에서 **일 CQ 워크플로우 전자 메일 알림 서비스**&#x200B;를 구성하여 이러한 값을 변경할 수 있습니다. 이 경우 저장소에서 변경 사항을 유지하는 것이 좋습니다.

기본 구성은 웹 콘솔에서 다음과 같이 표시됩니다.

![일별 CQ 워크플로 전자 메일 알림 서비스 구성 창](assets/chlimage_1-277.png)

### 페이지 알림용 이메일 템플릿 {#email-templates-for-page-notification}

페이지 알림용 이메일 템플릿은 아래에 있습니다.

`/libs/settings/notification-templates/com.day.cq.wcm.core.page`

기본 영어 템플릿(`en.txt`)은 다음과 같이 정의됩니다.

```xml
subject=[CQ Page Event Notification]: Page Event

header=-------------------------------------------------------------------------------------\n \
Time: ${time}\n \
User: ${userFullName} (${userId})\n \
-------------------------------------------------------------------------------------\n\n

message=The following pages were affected by the event: \n \
 \n \
${modifications} \n \
 \n\n
footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### 페이지 알림을 위한 이메일 템플릿 맞춤화 {#customizing-email-templates-for-page-notification}

페이지 알림용 영어 이메일 템플릿을 사용자 정의하려면 다음 작업을 수행하십시오.

1. CRXDE에서 다음 파일을 엽니다.

   `/libs/settings/notification-templates/com.day.cq.wcm.core.page/en.txt`

1. 필요에 따라 파일을 수정합니다.
1. 변경 사항을 저장합니다.

템플릿에는 다음 형식이 필요합니다.

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

여기서 &lt;text_x>는 정적 텍스트와 동적 문자열 변수의 혼합일 수 있습니다. 페이지 알림을 위한 이메일 템플릿 내에서 다음 변수를 사용할 수 있습니다.

* `${time}`, 이벤트 날짜 및 시간입니다.

* `${userFullName}`, 이벤트를 트리거한 사용자의 전체 이름.

* `${userId}`, 이벤트를 트리거한 사용자의 ID입니다.
* `${modifications}`은(는) 페이지 이벤트의 형식과 페이지 경로를 다음 형식으로 설명합니다.

  &lt;페이지 이벤트 유형> => &lt;페이지 경로>

  예:

  PageModified => /content/geometrixx/en/products

### 워크플로우 알림용 이메일 템플릿 {#email-templates-for-workflow-notification}

워크플로우 알림용 이메일 템플릿(영어)은 다음 위치에 있습니다.

`/libs/settings/workflow/notification/email/default/en.txt`

이는 다음과 같이 정의됩니다.

```xml
subject=Workflow notification: ${event.EventType}

header=-------------------------------------------------------------------------------------\n \
Time: ${event.TimeStamp}\n \
Step: ${item.node.title}\n \
User: ${participant.name} (${participant.id})\n \
Workflow: ${model.title}\n \
-------------------------------------------------------------------------------------\n\n

message=Content: ${host.prefix}${payload.path.open}\n

footer=\n \
-------------------------------------------------------------------------------------\n \
View the overview in your ${host.prefix}/aem/inbox\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### 워크플로우 알림을 위한 이메일 템플릿 맞춤화 {#customizing-email-templates-for-workflow-notification}

워크플로우 이벤트 알림을 위한 영어 이메일 템플릿을 사용자 정의하려면 다음 작업을 수행하십시오.

1. CRXDE에서 다음 파일을 엽니다.

   `/libs/settings/workflow/notification/email/default/en.txt`

1. 필요에 따라 파일을 수정합니다.
1. 변경 사항을 저장합니다.

템플릿에는 다음 형식이 필요합니다.

```
subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

>[!NOTE]
>
>여기서 `<text_x>`은(는) 정적 텍스트와 동적 문자열 변수의 혼합일 수 있습니다. `<text_x>` 항목의 각 줄은 `<text_x>` 문자열 변수의 끝을 나타내는 경우 마지막 인스턴스를 제외하고 백슬래시(`\`)로 끝나야 합니다.
>
>템플릿 형식에 대한 자세한 내용은 Properties.load()](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-) 메서드의 [javadocs에서 찾을 수 있습니다.

`${payload.path.open}` 메서드가 작업 항목의 페이로드에 대한 경로를 표시합니다. 예를 들어 Sites의 페이지에 대해 `payload.path.open`은(는) `/bin/wcmcommand?cmd=open&path=…`과(와) 유사합니다.; 이는 서버 이름이 없기 때문에 템플릿에서 `${host.prefix}` 앞에 추가합니다.

이메일 템플릿 내에서 사용할 수 있는 변수는 다음과 같습니다.

* `${event.EventType}`, 이벤트 유형
* `${event.TimeStamp}`, 이벤트의 날짜 및 시간
* `${event.User}`, 이벤트를 트리거한 사용자
* `${initiator.home}`, 초기자 노드 경로

* `${initiator.name}`, 초기자 이름

* `${initiator.email}`, 시작자의 전자 메일 주소
* `${item.id}`, 작업 항목의 ID
* `${item.node.id}`, 이 작업 항목과 연결된 워크플로 모델의 노드 ID
* `${item.node.title}`, 작업 항목의 제목
* `${participant.email}`, 참가자의 전자 메일 주소
* `${participant.name}`, 참가자 이름
* `${participant.familyName}`, 참가자의 성
* `${participant.id}`, 참가자 ID
* `${participant.language}`, 참가자 언어
* `${instance.id}`, 워크플로 id
* `${instance.state}`, 워크플로 상태
* `${model.title}`, 워크플로 모델의 제목
* `${model.id}`, 워크플로 모델의 ID

* `${model.version}`, 워크플로 모델의 버전
* `${payload.data}`, 페이로드

* `${payload.type}`, 페이로드 유형
* `${payload.path}`, 페이로드 경로
* `${host.prefix}`, 호스트 접두사(예: `http://localhost:4502`)

### 새 언어에 대한 이메일 템플릿 추가 {#adding-an-email-template-for-a-new-language}

새 언어에 대한 템플릿을 추가하려면 다음 작업을 수행하십시오.

1. CRXDE에서 아래에 `<language-code>.txt` 파일을 추가하십시오.

   * `/libs/settings/notification-templates/com.day.cq.wcm.core.page` : 페이지 알림용
   * `/libs/settings/workflow/notification/email/default` : 워크플로 알림용

1. 파일을 언어에 맞게 조정합니다.
1. 변경 사항을 저장합니다.

>[!NOTE]
>
>전자 메일 템플릿에 대한 파일 이름으로 사용되는 `<language-code>`은(는) AEM에서 인식하는 두 글자 소문자 언어 코드여야 합니다. 언어 코드의 경우 AEM은 ISO-639-1을 사용합니다.

## AEM Assets 이메일 알림 구성 {#assetsconfig}

AEM Assets의 컬렉션이 공유되거나 공유되지 않으면 사용자는 AEM에서 이메일 알림을 받을 수 있습니다. 이메일 알림을 구성하려면 다음 단계를 수행합니다.

1. [메일 서비스 구성](/help/sites-administering/notification.md#configuring-the-mail-service)에서 설명한 대로 메일 서비스를 구성합니다.
1. 관리자로 AEM에 로그인합니다. **도구** > **작업** > **웹 콘솔**&#x200B;을 클릭하여 웹 콘솔 구성을 엽니다.
1. **일 CQ DAM 리소스 컬렉션 서블릿**&#x200B;을(를) 편집합니다. **전자 메일 보내기**&#x200B;를 선택합니다. **저장**&#x200B;을 클릭합니다.

## OAuth 설정 {#setting-up-oauth}

AEM은 조직이 보안 이메일 요구 사항을 준수할 수 있도록 통합 Mailer 서비스에 대한 OAuth2 지원을 제공합니다.

아래 설명된 대로 여러 이메일 공급자에 대한 OAuth를 구성할 수 있습니다.

>[!NOTE]
>
>이 절차는 Publish 인스턴스의 예입니다. 작성자 인스턴스에서 이메일 알림을 활성화하려면 작성자에 대해 동일한 단계를 수행해야 합니다.

### Gmail {#gmail}

1. `https://console.developers.google.com/projectcreate`에 프로젝트 만들기
1. 프로젝트를 선택한 다음 **API 및 서비스** - **대시보드 - 자격 증명**&#x200B;으로 이동합니다.
1. 요구 사항에 따라 OAuth 동의 화면 구성
1. 다음에 나오는 업데이트 화면에서 다음 두 범위를 추가합니다.
   * `https://mail.google.com/`
   * `https://www.googleapis.com//auth/gmail.send`
1. 범위를 추가한 후 왼쪽 메뉴에서 **자격 증명**(으)로 돌아간 다음 **자격 증명 만들기** - **OAuth 클라이언트 ID** - **데스크톱 앱**(으)로 이동합니다.
1. 클라이언트 ID 및 클라이언트 암호가 포함된 새 창이 열립니다.
1. 이러한 자격 증명을 저장합니다.

**AEM 측 구성**

>[!NOTE]
>
>Adobe Managed Service 고객은 고객 서비스 엔지니어와 협력하여 프로덕션 환경을 변경할 수 있습니다.

먼저 메일 서비스를 구성합니다.

1. `http://serveraddress:serverport/system/console/configMgr`(으)로 이동하여 AEM 웹 콘솔 열기
1. 찾은 다음 **일 CQ 메일 서비스**&#x200B;를 클릭합니다.
1. 다음 설정을 추가합니다.
   * SMTP 서버 호스트 이름: `smtp.gmail.com`
   * 요구 사항에 따라 SMTP 서버 포트: `25` 또는 `587`
   * **SMPT StarTLS 사용** 및 **SMTP에 StarTLS 필요**&#x200B;에 대한 확인란을 선택합니다.
   * **OAuth 흐름**&#x200B;을 확인하고 **저장**&#x200B;을 클릭하세요.

그런 다음 아래 절차에 따라 SMTP OAuth 공급자를 구성합니다.

1. `http://serveraddress:serverport/system/console/configMgr`(으)로 이동하여 AEM 웹 콘솔 열기
1. 찾은 다음 **CQ 메일 서버 SMTP OAuth2 공급자**&#x200B;를 클릭합니다
1. 다음과 같이 필요한 정보를 입력합니다.
   * 인증 URL: `https://accounts.google.com/o/oauth2/auth`
   * 토큰 URL: `https://accounts.google.com/o/oauth2/token`
   * 범위: `https://www.googleapis.com/auth/gmail.send` 및 `https://mail.google.com/`. 구성된 각 범위의 오른쪽에 있는 **+** 단추를 눌러 두 개 이상의 범위를 추가할 수 있습니다.
   * 클라이언트 ID 및 클라이언트 암호: 위 단락에서 설명한 대로 검색한 값으로 이러한 필드를 구성합니다.
   * 새로 고침 토큰 URL: `https://accounts.google.com/o/oauth2/token`
   * 새로 고침 토큰 만료: 절대 안 함
1. **저장**&#x200B;을 클릭합니다.

<!-- clarify refresh token expiry, currently not present in the UI -->

구성이 완료되면 설정은 다음과 같이 표시됩니다.

![CQ Mailer SMTP Oauth2 공급자 구성 창](assets/oauth-smtpprov2.png)

이제 OAuth 구성 요소를 활성화합니다. 다음을 통해 이 작업을 수행할 수 있습니다.

1. 다음 URL을 방문하여 구성 요소 콘솔로 이동: `http://serveraddress:serverport/system/console/components`
1. 다음 구성 요소를 찾습니다
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. 구성 요소 왼쪽에 있는 재생 아이콘을 누릅니다

   ![OAuthCodeGenerateServlet 및 OAuthCodeAccessTokenGenerator를 표시하는 구성 요소 목록](assets/oauth-components-play.png)

마지막으로 다음 방법으로 구성을 확인합니다.

1. Publish 인스턴스 주소로 이동하고 관리자로 로그인합니다.
1. 브라우저에서 새 탭을 열고 `http://serveraddress:serverport/services/mailer/oauth2/authorize`(으)로 이동합니다. SMTP 공급자의 페이지로 리디렉션됩니다(이 경우 Gmail).
1. 로그인 및 필요한 권한 부여에 대한 동의
1. 동의를 하면 토큰이 저장소에 저장됩니다. 게시 인스턴스의 URL `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`에 직접 액세스하여 `accessToken`에서 액세스할 수 있습니다.
1. 각 게시 인스턴스에 대해 위의 내용을 반복합니다

<!-- clarify if the ip/server address in the last procedure is that of the publish instance -->

### Microsoft Outlook {#microsoft-outlook}

1. [https://portal.azure.com/](https://portal.azure.com/)으로 이동한 다음 로그인합니다.
1. 검색창에서 **Azure Active Directory**&#x200B;를 검색한 다음, 결과를 클릭합니다. 또는 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)에서 바로 검색할 수 있습니다.
1. **앱 등록** - **신규 등록**&#x200B;을 클릭합니다.

   ![Microsoft Outlook을 구성할 때 새 등록 단추](assets/oauth-outlook1.png)

1. 요구 사항에 따라 정보를 입력한 다음 **등록**&#x200B;을 클릭합니다
1. 새로 생성된 앱으로 이동하여 **API 권한**&#x200B;을 선택합니다.
1. **권한 추가** - **그래프 권한** - **위임된 권한**&#x200B;으로 이동합니다.
1. 아래의 앱에 대한 권한을 선택한 다음 **권한 추가**&#x200B;를 클릭합니다.
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. **인증** - **플랫폼 추가** - **웹**(으)로 이동하고 **리디렉션 URL** 섹션에서 OAuth 코드 리디렉션을 위해 다음 URL을 추가한 다음 **구성**&#x200B;을 누릅니다.
   * `http://localhost:4503/services/mailer/oauth2/token`
1. 각 게시 인스턴스에 대해 위의 내용을 반복합니다
1. 요구 사항에 따라 설정 구성
1. 그런 다음 **인증서 및 암호**(으)로 이동하고 **새 클라이언트 암호**&#x200B;를 클릭한 다음 화면에 표시되는 단계에 따라 암호를 만드십시오. 나중에 사용할 수 있도록 이러한 보안 내용을 메모해 두십시오.
1. 왼쪽 창에서 **개요**&#x200B;를 누르고 나중에 사용할 수 있도록 **애플리케이션(클라이언트) ID** 및 **디렉터리(테넌트) ID**&#x200B;의 값을 복사합니다.

재점검하려면 AEM 측의 Mailer 서비스에 대한 OAuth2 구성에 대한 다음 정보가 있어야 합니다.

* 테넌트 ID로 구성되는 인증 URL 형식: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* 테넌트 ID로 구성되는 토큰 URL 형식: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 테넌트 ID로 구성되는 새로 고침 URL 형식: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 클라이언트 ID
* 클라이언트 보안

**AEM 측 구성**

다음으로 OAuth2 설정을 AEM과 통합합니다.

1. `http://serveraddress:serverport/system/console/configMgr`(으)로 이동하여 로컬 인스턴스의 웹 콘솔로 이동
1. **일별 CQ 메일 서비스**&#x200B;를 찾아 클릭하세요.
1. 다음 설정을 추가합니다.
   * SMTP 서버 호스트 이름: `smtp.office365.com`
   * SMTP 사용자: 이메일 형식의 사용자 이름
   * &quot;보낸 사람&quot; 주소: 발송자가 보낸 메시지의 &quot;보낸 사람:&quot; 필드에 사용할 이메일 주소
   * 요구 사항에 따라 SMTP 서버 포트: `25` 또는 `587`
   * **SMPT StarTLS 사용** 및 **SMTP에 StarTLS 필요**&#x200B;에 대한 확인란을 선택합니다.
   * **OAuth 흐름**&#x200B;을 확인하고 **저장**&#x200B;을 클릭하세요.
1. 찾은 다음 **CQ 메일 서버 SMTP OAuth2 공급자**&#x200B;를 클릭합니다
1. 다음과 같이 필요한 정보를 입력합니다.
   * [이 프로시저의 끝](#microsoft-outlook)에 설명된 대로 인증 URL, 토큰 URL 및 새로 고침 토큰 URL을 구성하여 입력합니다.
   * 클라이언트 ID 및 클라이언트 암호: 위에서 설명한 대로 검색한 값으로 이러한 필드를 구성합니다.
   * 구성에 다음 범위를 추가합니다.
      * openid
      * offline_access
      * `https://outlook.office365.com/Mail.Send`
      * `https://outlook.office365.com/Mail.Read`
      * `https://outlook.office365.com/SMTP.Send`
   * AuthCode 리디렉션 Url: `http://localhost:4503/services/mailer/oauth2/token`
   * 새로 고침 토큰 URL: 위의 토큰 URL과 동일한 값을 가져야 합니다.
1. **저장**&#x200B;을 클릭합니다.

구성이 완료되면 설정은 다음과 같이 표시됩니다.

![완료된 CQ Mailer SMTP OAuth2 구성](assets/oauth-outlook-smptconfig.png)

이제 OAuth 구성 요소를 활성화합니다. 다음을 통해 이 작업을 수행할 수 있습니다.

1. 다음 URL을 방문하여 구성 요소 콘솔로 이동: `http://serveraddress:serverport/system/console/components`
1. 다음 구성 요소를 찾습니다
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. 구성 요소 왼쪽에 있는 재생 아이콘을 누릅니다

![OAuthCodeGenerateServlet 및 OAuthCodeAccessTokenGenerator가 포함된 구성 요소 목록의 코드 조각](assets/oauth-components-play.png)

마지막으로 다음 방법으로 구성을 확인합니다.

1. Publish 인스턴스 주소로 이동하고 관리자로 로그인합니다.
1. 브라우저에서 새 탭을 열고 `http://serveraddress:serverport/services/mailer/oauth2/authorize`(으)로 이동합니다. 이렇게 하면 SMTP 공급자의 페이지로 리디렉션됩니다(이 경우 Outlook).
1. 로그인 및 필요한 권한 부여에 대한 동의
1. 동의를 하면 토큰이 저장소에 저장됩니다. 게시 인스턴스의 URL `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`에 직접 액세스하여 `accessToken`에서 액세스할 수 있습니다.
